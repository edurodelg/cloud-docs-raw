---
merged_at: 2026-01-26T21:02:36.353194
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-cosmosdb_how-to-create-function-azure-cli.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cosmosdb.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb -->

# Azure Cosmos DB bindings for Azure Functions 1.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

This article explains how to work with [Azure Cosmos DB](/en-us/azure/cosmos-db/serverless-computing-database) bindings in Azure Functions. Azure Functions supports trigger, input, and output bindings for Azure Cosmos DB.

Keep these important considerations in mind when using the Azure Cosmos DB binding for the Functions v1.x runtime:

This article is for Azure Functions 1.x. We recommend that you run your functions on the most recent version of the Functions runtime. For information about how to use these bindings in the latest Functions runtime, see

[Azure Cosmos DB bindings for Azure Functions 2.x](functions-bindings-cosmosdb-v2).This binding was originally named DocumentDB. In Azure Functions version 1.x, only the trigger was renamed Azure Cosmos DB; the input binding, output binding, and NuGet package retain the DocumentDB name.

Azure Cosmos DB bindings are only supported for use with the SQL API. For all other Azure Cosmos DB APIs, you should access the database from your function by using the static client for your API, including

[Azure Cosmos DB for MongoDB](/en-us/azure/cosmos-db/mongodb-introduction),[Azure Cosmos DB for Apache Cassandra](/en-us/azure/cosmos-db/cassandra-introduction),[Azure Cosmos DB for Apache Gremlin](/en-us/azure/cosmos-db/graph-introduction), and[Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table-introduction).The Azure Cosmos DB bindings for the Functions v1.x runtime don't support Microsoft Entra authentication and managed identities. To improve security, you should upgrade to run on the latest version of the Functions runtime.


## Packages - Functions 1.x

The Azure Cosmos DB bindings for Functions version 1.x are provided in the [Microsoft.Azure.WebJobs.Extensions.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB) NuGet package, version 1.x. Source code for the bindings is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/v2.x/src/WebJobs.Extensions.DocumentDB) GitHub repository.

The following table lists how to add support for output binding in each development environment.

| Development environment | To add support in Functions 1.x |
|---|---|
| Local development: C# class library |
|

## Trigger

The Azure Cosmos DB Trigger uses the [Azure Cosmos DB Change Feed](/en-us/azure/cosmos-db/change-feed) to listen for inserts and updates across partitions. The change feed publishes inserts and updates, not deletions.

## Trigger - example

The following example shows an [in-process C# function](functions-dotnet-class-library) that is invoked when there are inserts or updates in the specified database and collection.

```
using Microsoft.Azure.Documents;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
namespace CosmosDBSamplesV1
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
TraceWriter log)
{
if (documents != null && documents.Count > 0)
{
log.Info($"Documents modified: {documents.Count}");
log.Info($"First document Id: {documents[0].Id}");
}
}
}
}
```


## Trigger - attributes

For [in-process C# class libraries](functions-dotnet-class-library), use the [CosmosDBTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) attribute.

The attribute's constructor takes the database name and collection name. For information about those settings and other properties that you can configure, see [Trigger - configuration](#trigger---configuration). Here's a `CosmosDBTrigger`

attribute example in a method signature:

```
[FunctionName("DocumentUpdates")]
public static void Run(
[CosmosDBTrigger("database", "collection", ConnectionStringSetting = "myCosmosDB")]
IReadOnlyList<Document> documents,
TraceWriter log)
{
...
}
```


For a complete example, see [Trigger - C# example](#trigger).

## Trigger - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDBTrigger`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `cosmosDBTrigger` . |
direction |
n/a | Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
name |
n/a | The variable name used in function code that represents the list of documents with changes. |
connectionStringSetting |
ConnectionStringSetting |
The name of an app setting that contains the connection string used to connect to the Azure Cosmos DB account being monitored. |
databaseName |
DatabaseName |
The name of the Azure Cosmos DB database with the collection being monitored. |
collectionName |
CollectionName |
The name of the collection being monitored. |
leaseConnectionStringSetting |
LeaseConnectionStringSetting |
(Optional) The name of an app setting that contains the connection string to the service which holds the lease collection. When not set, the `connectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
leaseDatabaseName |
LeaseDatabaseName |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. This parameter is automatically set when the binding is created in the portal. |
leaseCollectionName |
LeaseCollectionName |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
createLeaseCollectionIfNotExists |
CreateLeaseCollectionIfNotExists |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
leasesCollectionThroughput |
LeasesCollectionThroughput |
(Optional) Defines the amount of Request Units to assign when the leases collection is created. This setting is only used When `createLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
leaseCollectionPrefix |
LeaseCollectionPrefix |
(Optional) When set, it adds a prefix to the leases created in the Lease collection for this Function, effectively allowing two separate Azure Functions to share the same Lease collection by using different prefixes. |
feedPollDelay |
FeedPollDelay |
(Optional) When set, it defines, in milliseconds, the delay in between polling a partition for new changes on the feed, after all current changes are drained. Default is 5000 (5 seconds). |
leaseAcquireInterval |
LeaseAcquireInterval |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
leaseExpirationInterval |
LeaseExpirationInterval |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
leaseRenewInterval |
LeaseRenewInterval |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
checkpointFrequency |
CheckpointFrequency |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
maxItemsPerInvocation |
MaxItemsPerInvocation |
(Optional) When set, it customizes the maximum amount of items received per Function call. |
startFromBeginning |
StartFromBeginning |
(Optional) When set, it tells the Trigger to start reading changes from the beginning of the history of the collection instead of the current time. This only works the first time the Trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this to `true` when there are leases already created has no effect. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Trigger - usage

The trigger requires a second collection that it uses to store *leases* over the partitions. Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `LeaseCollectionPrefix`

for each function. Otherwise, only one of the functions will be triggered. For information about the prefix, see the [Configuration section](#trigger---configuration).

The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself. If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.

## Input

The Azure Cosmos DB input binding uses the SQL API to retrieve one or more Azure Cosmos DB documents and passes them to the input parameter of the function. The document ID or query parameters can be determined based on the trigger that invokes the function.

## Input - example

This section contains the following examples:

[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-c)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-c)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-c)[HTTP trigger, look up ID from route data, using SqlQuery](#http-trigger-look-up-id-from-route-data-using-sqlquery-c)[HTTP trigger, get multiple docs, using SqlQuery](#http-trigger-get-multiple-docs-using-sqlquery-c)[HTTP trigger, get multiple docs, using DocumentClient](#http-trigger-get-multiple-docs-using-documentclient-c)

The examples refer to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV1
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


### Queue trigger, look up ID from JSON

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by a queue message that contains a JSON object. The queue trigger parses the JSON into an object named `ToDoItemLookup`

, which contains the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
namespace CosmosDBSamplesV1
{
public class ToDoItemLookup
{
public string ToDoItemId { get; set; }
}
}
```


```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromJSON
{
[FunctionName("DocByIdFromJSON")]
public static void Run(
[QueueTrigger("todoqueueforlookup")] ToDoItemLookup toDoItemLookup,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
Id = "{ToDoItemId}")]ToDoItem toDoItem,
TraceWriter log)
{
log.Info($"C# Queue trigger function processed Id={toDoItemLookup?.ToDoItemId}");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
}
}
}
```


### HTTP trigger, look up ID from query string

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromQueryString
{
[FunctionName("DocByIdFromQueryString")]
public static HttpResponseMessage Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
Id = "{Query.id}")] ToDoItem toDoItem,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, look up ID from route data

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromRouteData
{
[FunctionName("DocByIdFromRouteData")]
public static HttpResponseMessage Run(
[HttpTrigger(
AuthorizationLevel.Anonymous, "get", "post",
Route = "todoitems/{id}")]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
Id = "{id}")] ToDoItem toDoItem,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, look up ID from route data, using SqlQuery

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromRouteDataUsingSqlQuery
{
[FunctionName("DocByIdFromRouteDataUsingSqlQuery")]
public static HttpResponseMessage Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post",
Route = "todoitems2/{id}")]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
SqlQuery = "select * from ToDoItems r where r.id = {id}")] IEnumerable<ToDoItem> toDoItems,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
foreach (ToDoItem toDoItem in toDoItems)
{
log.Info(toDoItem.Description);
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, get multiple docs, using SqlQuery

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a list of documents. The function is triggered by an HTTP request. The query is specified in the `SqlQuery`

attribute property.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocsBySqlQuery
{
[FunctionName("DocsBySqlQuery")]
public static HttpResponseMessage Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]
HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
SqlQuery = "SELECT top 2 * FROM c order by c._ts desc")]
IEnumerable<ToDoItem> toDoItems,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
foreach (ToDoItem toDoItem in toDoItems)
{
log.Info(toDoItem.Description);
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, get multiple docs, using DocumentClient (C#)

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a list of documents. The function is triggered by an HTTP request. The code uses a `DocumentClient`

instance provided by the Azure Cosmos DB binding to read a list of documents. The `DocumentClient`

instance could also be used for write operations.

```
using Microsoft.Azure.Documents.Client;
using Microsoft.Azure.Documents.Linq;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System;
using System.Linq;
using System.Net;
using System.Net.Http;
using System.Threading.Tasks;
namespace CosmosDBSamplesV1
{
public static class DocsByUsingDocumentClient
{
[FunctionName("DocsByUsingDocumentClient")]
public static async Task<HttpResponseMessage> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection")] DocumentClient client,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
Uri collectionUri = UriFactory.CreateDocumentCollectionUri("ToDoItems", "Items");
string searchterm = req.GetQueryNameValuePairs()
.FirstOrDefault(q => string.Compare(q.Key, "searchterm", true) == 0)
.Value;
if (searchterm == null)
{
return req.CreateResponse(HttpStatusCode.NotFound);
}
log.Info($"Searching for word: {searchterm} using Uri: {collectionUri.ToString()}");
IDocumentQuery<ToDoItem> query = client.CreateDocumentQuery<ToDoItem>(collectionUri)
.Where(p => p.Description.Contains(searchterm))
.AsDocumentQuery();
while (query.HasMoreResults)
{
foreach (ToDoItem result in await query.ExecuteNextAsync())
{
log.Info(result.Description);
}
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


## Input - attributes

In [in-process C# class libraries](functions-dotnet-class-library), use the [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) attribute.

The attribute's constructor takes the database name and collection name. For information about those settings and other properties that you can configure, see [the following configuration section](#input---configuration).

## Input - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `DocumentDB`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `documentdb` . |
direction |
n/a | Must be set to `in` . |
name |
n/a | Name of the binding parameter that represents the document in the function. |
databaseName |
DatabaseName |
The database containing the document. |
collectionName |
CollectionName |
The name of the collection that contains the document. |
id |
Id |
The ID of the document to retrieve. This property supports
id and sqlQuery properties. If you don't set either one, the entire collection is retrieved. |

**sqlQuery****SqlQuery**`SELECT * FROM c where c.departmentId = {departmentId}`

. Don't set both the **id**and**sqlQuery**properties. If you don't set either one, the entire collection is retrieved.**connection****ConnectionStringSetting****partitionKey****PartitionKey**When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Input - usage

When the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.

## Output

The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.

## Output - example

This section contains the following examples:

- Queue trigger, write one doc
- Queue trigger, write docs using
`IAsyncCollector`


The examples refer to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV1
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


### Queue trigger, write one doc

The following example shows a [C# function](functions-dotnet-class-library) that adds a document to a database, using data provided in message from Queue storage.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System;
namespace CosmosDBSamplesV1
{
public static class WriteOneDoc
{
[FunctionName("WriteOneDoc")]
public static void Run(
[QueueTrigger("todoqueueforwrite")] string queueMessage,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection")]out dynamic document,
TraceWriter log)
{
document = new { Description = queueMessage, id = Guid.NewGuid() };
log.Info($"C# Queue trigger function inserted one row");
log.Info($"Description={queueMessage}");
}
}
}
```


### Queue trigger, write docs using IAsyncCollector

The following example shows a [C# function](functions-dotnet-class-library) that adds a collection of documents to a database, using data provided in a queue message JSON.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Threading.Tasks;
namespace CosmosDBSamplesV1
{
public static class WriteDocsIAsyncCollector
{
[FunctionName("WriteDocsIAsyncCollector")]
public static async Task Run(
[QueueTrigger("todoqueueforwritemulti")] ToDoItem[] toDoItemsIn,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection")]
IAsyncCollector<ToDoItem> toDoItemsOut,
TraceWriter log)
{
log.Info($"C# Queue trigger function processed {toDoItemsIn?.Length} items");
foreach (ToDoItem toDoItem in toDoItemsIn)
{
log.Info($"Description={toDoItem.Description}");
await toDoItemsOut.AddAsync(toDoItem);
}
}
}
}
```


## Output - attributes

In [in-process C# class libraries](functions-dotnet-class-library), use the [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) attribute.

The attribute's constructor takes the database name and collection name. For information about those settings and other properties that you can configure, see [Output - configuration](#output---configuration). Here's a `DocumentDB`

attribute example in a method signature:

```
[FunctionName("QueueToDocDB")]
public static void Run(
[QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
[DocumentDB("ToDoList", "Items", Id = "id", ConnectionStringSetting = "myCosmosDB")] out dynamic document)
{
...
}
```


For a complete example, see [Output](#output).

## Output - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `DocumentDB`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `documentdb` . |
direction |
n/a | Must be set to `out` . |
name |
n/a | Name of the binding parameter that represents the document in the function. |
databaseName |
DatabaseName |
The database containing the collection where the document is created. |
collectionName |
CollectionName |
The name of the collection where the document is created. |
createIfNotExists |
CreateIfNotExists |
A boolean value to indicate whether the collection is created when it doesn't exist. The default is false because new collections are created with reserved throughput, which has cost implications. For more information, see the
|
partitionKey |
PartitionKey |
When `CreateIfNotExists` is true, defines the partition key path for the created collection. |
collectionThroughput |
CollectionThroughput |
When `CreateIfNotExists` is true, defines the
|
connection |
ConnectionStringSetting |
The name of the app setting containing your Azure Cosmos DB connection string. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Output - usage

By default, when you write to the output parameter in your function, a document is created in your database. This document has an automatically generated GUID as the document ID. You can specify the document ID of the output document by specifying the `id`

property in the JSON object passed to the output parameter.

Note

When you specify the ID of an existing document, it gets overwritten by the new output document.

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Azure Cosmos DB |
|


---

<!-- DOCUMENTO FUSIONADO: how-to-create-function-azure-cli.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/how-to-create-function-azure-cli -->

# Quickstart: Create a function in Azure from the command line

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use local command-line tools to create a function that responds to HTTP requests. After verifying your code locally, you deploy it to a serverless Flex Consumption hosting plan in Azure Functions.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Make sure to select your preferred development language at the top of the article.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[Java 17 Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure)- If you use another
[supported version of Java](supported-languages?pivots=programming-language-java#languages-by-runtime-version), you must update the project's pom.xml file. - The
`JAVA_HOME`

environment variable must be set to the install location of the correct version of the Java Development Kit (JDK).

- If you use another
[Apache Maven 3.8.x](https://maven.apache.org)

The

, used to parse JSON output, and is also available in Azure Cloud Shell.`jq`

command line JSON processor

## Install the Azure Functions Core Tools

The recommended way to install Core Tools depends on the operating system of your local development computer.

The following steps use a Windows installer (MSI) to install Core Tools v4.x. For more information about other package-based installers, see the [Core Tools readme](https://github.com/Azure/azure-functions-core-tools/blob/v4.x/README.md#windows).

Download and run the Core Tools installer, based on your version of Windows:

[v4.x - Windows 64-bit](https://go.microsoft.com/fwlink/?linkid=2174087)(Recommended.[Visual Studio Code debugging](functions-develop-vs-code#debugging-functions-locally)requires 64-bit.)[v4.x - Windows 32-bit](https://go.microsoft.com/fwlink/?linkid=2174159)

If you previously used Windows installer (MSI) to install Core Tools on Windows, you should uninstall the old version from Add Remove Programs before installing the latest version.

Tip

To install Core Tools on [Windows Subsystem for Linux (WSL)](/en-us/windows/wsl/install), follow the instructions on the Linux tab.

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

## Create a local code project and function

In Azure Functions, your code project is an app that contains one or more individual functions that each respond to a specific trigger. All functions in a project share the same configurations and are deployed as a unit to Azure. In this section, you create a code project that contains a single function.

In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime dotnet-isolated`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime node --language javascript`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime powershell`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime python`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime node --language typescript`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime custom`


In an empty folder, run this

`mvn`

command to generate the code project from an Azure Functions[Maven archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html):`mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -DarchetypeArtifactId=azure-functions-archetype -DjavaVersion=17`

Important

- Use
`-DjavaVersion=11`

if you want your functions to run on Java 11. To learn more, see[Java versions](functions-reference-java#java-versions). - Set the
`JAVA_HOME`

environment variable to the install location of the correct version of the JDK to complete this article.

- Use
Maven asks you for values needed to finish generating the project on deployment.


Provide the following values when prompted:Prompt Value Description **groupId**`com.fabrikam`

A value that uniquely identifies your project across all projects, following the [package naming rules](https://docs.oracle.com/javase/specs/jls/se6/html/packages.html#7.7)for Java.**artifactId**`fabrikam-functions`

A value that is the name of the jar, without a version number. **version**`1.0-SNAPSHOT`

Choose the default value. **package**`com.fabrikam`

A value that is the Java package for the generated function code. Use the default. Type

`Y`

or press Enter to confirm.Maven creates the project files in a new folder with a name of

*artifactId*, which in this example is`fabrikam-functions`

.Navigate into the project folder:

`cd fabrikam-functions`

You can review the template-generated code for your new HTTP trigger function in

*Function.java*in the*\src\main\java\com\fabrikam*project directory.

Use this

command to add a function to your project:`func new`

`func new --name HttpExample --template "HTTP trigger" --authlevel "function"`

A new code file is added to your project. In this case, the

`--name`

argument is the unique name of your function (`HttpExample`

) and the`--template`

argument specifies an HTTP trigger.

The project root folder contains various files for the project, including configurations files named [local.settings.json](functions-develop-local#local-settings-file) and [host.json](functions-host-json). Because *local.settings.json* can contain secrets downloaded from Azure, the file is excluded from source control by default in the *.gitignore* file.

## Create and build your function

The *function.json* file in the *HttpExample* folder declares an HTTP trigger function. You complete the function by adding a handler and compiling it into an executable.

Press

`Ctrl + N`(`Cmd + N`on macOS) to create a new file. Save it as*handler.go*in the function app root (in the same folder as*host.json*).In

*handler.go*, add the following code and save the file. This is your Go custom handler.`package main import ( "fmt" "log" "net/http" "os" ) func helloHandler(w http.ResponseWriter, r *http.Request) { message := "This HTTP triggered function executed successfully. Pass a name in the query string for a personalized response.\n" name := r.URL.Query().Get("name") if name != "" { message = fmt.Sprintf("Hello, %s. This HTTP triggered function executed successfully.\n", name) } fmt.Fprint(w, message) } func main() { listenAddr := ":8080" if val, ok := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT"); ok { listenAddr = ":" + val } http.HandleFunc("/api/HttpExample", helloHandler) log.Printf("About to listen on %s. Go to https://127.0.0.1%s/", listenAddr, listenAddr) log.Fatal(http.ListenAndServe(listenAddr, nil)) }`

Press

`Ctrl + Shift + ``or select*New Terminal*from the*Terminal*menu to open a new integrated terminal in VS Code.Compile your custom handler using the following command. An executable file named

`handler`

(`handler.exe`

on Windows) is output in the function app root folder.`go build handler.go`


## Configure your function app

The function host needs to be configured to run your custom handler binary when it starts.

Open

*host.json*.In the

`customHandler.description`

section, set the value of`defaultExecutablePath`

to`handler`

(on Windows, set it to`handler.exe`

).In the

`customHandler`

section, add a property named`enableForwardingHttpRequest`

and set its value to`true`

. For functions consisting of only an HTTP trigger, this setting simplifies programming by allow you to work with a typical HTTP request instead of the custom handler[request payload](functions-custom-handlers#request-payload).Confirm the

`customHandler`

section looks like this example. Save the file.`"customHandler": { "description": { "defaultExecutablePath": "handler", "workingDirectory": "", "arguments": [] }, "enableForwardingHttpRequest": true }`


The function app is configured to start your custom handler executable.

## Run the function locally

Verify your new function by running the project locally and calling the function endpoint.

Use this command to start the local Azure Functions runtime host in the root of the project folder:

`func start`

`npm install npm start`

`mvn clean package mvn azure-functions:run`

Toward the end of the output, the following lines appear:

... Now listening on: http://0.0.0.0:7071 Application started. Press Ctrl+C to shut down. Http Functions: HttpExample: [GET,POST] http://localhost:7071/api/HttpExample ...

Copy the URL of your

`HttpExample`

function from this output to a browser and browse to the function URL. You should receive a success response with a "hello world" message.Note

Because access key authorization isn't enforced when running locally, the function URL returned doesn't include the access key value and you don't need it to call your function.

When you're done, use

**Ctrl**+**C**and choose`y`

to stop the functions host.

## Create supporting Azure resources for your function

Before you can deploy your function code to Azure, you need to create these resources:

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A default
[Storage account](../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your functions. - A
[user-assigned managed identity](/en-us/azure/active-directory/managed-identities-azure-resources/overview), which the Functions host uses to connect to the default storage account. - A function app, which provides the environment for executing your function code. A function app maps to your local function project and lets you group functions as a logical unit for easier management, deployment, and sharing of resources.

Use the Azure CLI commands in these steps to create the required resources.

If you haven't done so already, sign in to Azure:

`az login`

The

command signs you into your Azure account. Skip this step when running in Azure Cloud Shell.`az login`

If you haven't already done so, use this

command to install the Application Insights extension:`az extension add`

`az extension add --name application-insights`

Use this

[az group create](/en-us/cli/azure/group#az-group-create)command to create a resource group named`AzureFunctionsQuickstart-rg`

in your chosen region:`az group create --name "AzureFunctionsQuickstart-rg" --location "<REGION>"`

In this example, replace

`<REGION>`

with a region near you that supports the Flex Consumption plan. Use the[az functionapp list-flexconsumption-locations](/en-us/cli/azure/functionapp#az-functionapp-list-flexconsumption-locations)command to view the list of currently supported regions.Use this

[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)command to create a general-purpose storage account in your resource group and region:`az storage account create --name <STORAGE_NAME> --location "<REGION>" --resource-group "AzureFunctionsQuickstart-rg" \ --sku "Standard_LRS" --allow-blob-public-access false --allow-shared-key-access false`

In this example, replace

`<STORAGE_NAME>`

with a name that is appropriate to you and unique in Azure Storage. Names must contain three to 24 characters numbers and lowercase letters only.`Standard_LRS`

specifies a general-purpose account, which is[supported by Functions](storage-considerations#storage-account-requirements). This new account can only be accessed by using Microsoft Entra-authenticated identities that have been granted permissions to specific resources.Use this script to create a user-assigned managed identity, parse the returned JSON properties of the object using

`jq`

, and grant`Storage Blob Data Owner`

permissions in the default storage account:`output=$(az identity create --name "func-host-storage-user" --resource-group "AzureFunctionsQuickstart-rg" --location <REGION> \ --query "{userId:id, principalId: principalId, clientId: clientId}" -o json) userId=$(echo $output | jq -r '.userId') principalId=$(echo $output | jq -r '.principalId') clientId=$(echo $output | jq -r '.clientId') storageId=$(az storage account show --resource-group "AzureFunctionsQuickstart-rg" --name <STORAGE_NAME> --query 'id' -o tsv) az role assignment create --assignee-object-id $principalId --assignee-principal-type ServicePrincipal \ --role "Storage Blob Data Owner" --scope $storageId`

If you don't have the

`jq`

utility in your local Bash shell, it's available in Azure Cloud Shell. In this example, replace`<STORAGE_NAME>`

and`<REGION>`

with your default storage account name and region, respectively.The

[az identity create](/en-us/cli/azure/identity#az-identity-create)command creates an identity named`func-host-storage-user`

. The returned`principalId`

is used to assign permissions to this new identity in the default storage account by using thecommand. The`az role assignment create`

command is used to obtain the storage account ID.`az storage account show`

Use this

[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)command to create the function app in Azure:`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime dotnet-isolated --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime java --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime node --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime python --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime python --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime other --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

In this example, replace these placeholders with the appropriate values:

`<APP_NAME>`

: a globally unique name appropriate to you. The`<APP_NAME>`

is also the default DNS domain for the function app.`<STORAGE_NAME>`

: the name of the account you used in the previous step.`<REGION>`

: your current region.`<LANGUAGE_VERSION>`

: use the same[supported language stack version](supported-languages)you verified locally, when applicable.

This command creates a function app running in your specified language runtime on Linux in the

[Flex Consumption Plan](flex-consumption-plan), which is free for the amount of usage you incur here. The command also creates an associated Azure Application Insights instance in the same resource group, with which you can use to monitor your function app executions and view logs. For more information, see[Monitor Azure Functions](functions-monitoring). The instance incurs no costs until you activate it.Use this script to add your user-assigned managed identity to the

[Monitoring Metrics Publisher](../role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher)role in your Application Insights instance:`appInsights=$(az monitor app-insights component show --resource-group "AzureFunctionsQuickstart-rg" \ --app <APP_NAME> --query "id" --output tsv) principalId=$(az identity show --name "func-host-storage-user" --resource-group "AzureFunctionsQuickstart-rg" \ --query principalId -o tsv) az role assignment create --role "Monitoring Metrics Publisher" --assignee $principalId --scope $appInsights`

In this example, replace

`<APP_NAME>`

with the name of your function app. The[az role assignment create](/en-us/cli/azure/role/assignment#az-role-assignment-create)command adds your user to the role. The resource ID of your Application Insights instance and the principal ID of your user are obtained by using the[az monitor app-insights component show](/en-us/cli/azure/monitor/app-insights/component#az-monitor-app-insights-component-show)andcommands, respectively.`az identity show`


## Update application settings

To enable the Functions host to connect to the default storage account by using shared secrets, replace the `AzureWebJobsStorage`

connection string setting with several settings that are prefixed with `AzureWebJobsStorage__`

. These settings define a complex setting that your app uses to connect to storage and Application Insights with a user-assigned managed identity.

Use this script to get the client ID of the user-assigned managed identity and uses it to define managed identity connections to both storage and Application Insights:

`clientId=$(az identity show --name func-host-storage-user \ --resource-group AzureFunctionsQuickstart-rg --query 'clientId' -o tsv) az functionapp config appsettings set --name <APP_NAME> --resource-group "AzureFunctionsQuickstart-rg" \ --settings AzureWebJobsStorage__accountName=<STORAGE_NAME> \ AzureWebJobsStorage__credential=managedidentity AzureWebJobsStorage__clientId=$clientId \ APPLICATIONINSIGHTS_AUTHENTICATION_STRING="ClientId=$clientId;Authorization=AAD"`

In this script, replace

`<APP_NAME>`

and`<STORAGE_NAME>`

with the names of your function app and storage account, respectively.Run the

[az functionapp config appsettings delete](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-delete)command to remove the existing`AzureWebJobsStorage`

connection string setting, which contains a shared secret key:`az functionapp config appsettings delete --name <APP_NAME> --resource-group "AzureFunctionsQuickstart-rg" --setting-names AzureWebJobsStorage`

In this example, replace

`<APP_NAME>`

with the names of your function app.

At this point, the Functions host can connect to the storage account securely by using managed identities instead of shared secrets. You can now deploy your project code to the Azure resources.

## Deploy the function project to Azure

After you've successfully created your function app in Azure, you're now ready to deploy your local functions project by using the [ func azure functionapp publish](functions-run-local#project-file-deployment) command.

In your root project folder, run this

command:`func azure functionapp publish`

`func azure functionapp publish <APP_NAME>`

In this example, replace

`<APP_NAME>`

with the name of your app. A successful deployment shows results similar to the following output (truncated for simplicity):... Getting site publishing info... Creating archive for current directory... Performing remote build for functions project. ... Deployment successful. Remote build succeeded! Syncing triggers... Functions in msdocs-azurefunctions-qs: HttpExample - [httpTrigger] Invoke url: https://msdocs-azurefunctions-qs.azurewebsites.net/api/httpexample

In your local terminal or command prompt, run this command to get the URL endpoint value, including the access key:

`func azure functionapp list-functions <APP_NAME> --show-keys`

In this example, again replace

`<APP_NAME>`

with the name of your app.Copy the returned endpoint URL and key, which you use to invoke the function endpoint.


## Update the pom.xml file

After you successfully create your function app in Azure, update the pom.xml file so that Maven can deploy to your new app. Otherwise, Maven creates a new set of Azure resources during deployment.

In Azure Cloud Shell, use this

command to get the deployment container URL and ID of the new user-assigned managed identity:`az functionapp show`

`az functionapp show --name <APP_NAME> --resource-group AzureFunctionsQuickstart-rg \ --query "{userAssignedIdentityResourceId: properties.functionAppConfig.deployment.storage.authentication.userAssignedIdentityResourceId, \ containerUrl: properties.functionAppConfig.deployment.storage.value}"`

In this example, replace

`<APP_NAME>`

with the names of your function app.In the project root directory, open the pom.xml file in a text editor, locate the

`properties`

element, and update these specific property values:Property name Value `java.version`

Use the same [supported language stack version](supported-languages)you verified locally, such as`17`

.`azure.functions.maven.plugin.version`

`1.37.1`

`azure.functions.java.library.version`

`3.1.0`

`functionAppName`

The name of your function app in Azure. Find the

`configuration`

section of the`azure-functions-maven-plugin`

and replace it with this XML fragment:`<configuration> <appName>${functionAppName}</appName> <resourceGroup>AzureFunctionsQuickstart-rg</resourceGroup> <pricingTier>Flex Consumption</pricingTier> <region>....</region> <runtime> <os>linux</os> <javaVersion>${java.version}</javaVersion> </runtime> <deploymentStorageAccount>...</deploymentStorageAccount> <deploymentStorageResourceGroup>AzureFunctionsQuickstart-rg</deploymentStorageResourceGroup> <deploymentStorageContainer>...</deploymentStorageContainer> <storageAuthenticationMethod>UserAssignedIdentity</storageAuthenticationMethod> <userAssignedIdentityResourceId>...</userAssignedIdentityResourceId> <appSettings> <property> <name>FUNCTIONS_EXTENSION_VERSION</name> <value>~4</value> </property> </appSettings> </configuration>`

In the new

`configuration`

element, make these specific replacements of the ellipses (`...`

) values:Configuration Value `region`

The region code of your existing function app, such as `eastus`

.`deploymentStorageAccount`

The name of your storage account. `deploymentStorageContainer`

The name of the deployment share, which comes after the `\`

in the`containerUrl`

value you obtained.`userAssignedIdentityResourceId`

The fully qualified resource ID of your managed identity, which you obtained. Save your changes to the

*pom.xml*file.

You can now use Maven to deploy your code project to your existing app.

## Deploy the function project to Azure

From the command prompt, run this command:

`mvn clean package azure-functions:deploy`

After your deployment succeeds, run this Core Tools command to get the URL endpoint value, including the access key:

`func azure functionapp list-functions <APP_NAME> --show-keys`

In this example, again replace

`<APP_NAME>`

with the name of your app.Copy the returned endpoint URL and key, which you use to invoke the function endpoint.


## Invoke the function on Azure

Because your function uses an HTTP trigger and supports GET requests, you invoke it by making an HTTP request to its URL using the function-level access key. It's easiest to execute a GET request in a browser.

Paste the URL and access key you copied into a browser address bar.

The endpoint URL should look something like this example:

`https://contoso-app.azurewebsites.net/api/httpexample?code=aabbccdd...`


In this case, you must also provide an access key in the query string when making a GET request to the endpoint URL. Using an access key is recommended to limit access from random clients. When making a POST request using an HTTP client, you should instead provide the access key in the `x-functions-key`

header.

When you navigate to this URL, the browser should display similar output as when you ran the function locally.

## Clean up resources

If you continue to the [next step](#next-steps) and add an Azure Storage queue output binding, keep all your resources in place as you'll build on what you've already done.

Otherwise, use the following command to delete the resource group and all its contained resources to avoid incurring further costs.

```
az group delete --name AzureFunctionsQuickstart-rg
```


---

<!-- DOCUMENTO FUSIONADO: ___functions-integrate-storage-queue-output-binding_functions-create-first-java-_48fe9d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-integrate-storage-queue-output-binding_functions-create-first-java-g_6d477a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-integrate-storage-queue-output-binding_functions-create-first-java-gr_b0867a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-integrate-storage-queue-output-binding.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-integrate-storage-queue-output-binding -->

# Add messages to an Azure Storage queue using Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, input and output bindings provide a declarative way to make data from external services available to your code. In this article, you use an output binding to create a message in a queue when an HTTP request triggers a function. You use Azure storage container to view the queue messages that your function creates.

## Prerequisites

An Azure subscription. If you don't have one, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.Follow the directions in

[Create your first function in the Azure portal](functions-create-function-app-portal), omitting the**Clean up resources**step, to create the function app and function to use in this article.

## Add an output binding

In this section, you use the portal UI to add an Azure Queue Storage output binding to the function you created in the prerequisites. This binding makes it possible to write minimal code to create a message in a queue. You don't need to write code for such tasks as opening a storage connection, creating a queue, or getting a reference to a queue. The Azure Functions runtime and queue output binding take care of those tasks for you.

In the Azure portal, search for and select the function app that you created in

[Create your first function from the Azure portal](functions-get-started).In your function app, select the function that you created.

Select

**Integration**, and then select**+ Add output**.Select the

**Azure Queue Storage**binding type and add the settings as specified in the table that follows this screenshot:Setting Suggested value description **Message parameter name**outputQueueItem The name of the output binding parameter. **Queue name**outqueue The name of the queue to connect to in your storage account. **Storage account connection**AzureWebJobsStorage You can use the existing storage account connection used by your function app or create a new one. Select

**OK**to add the binding.

Now that you have an output binding defined, you need to update the code to use the binding to add messages to a queue.

## Add code that uses the output binding

In this section, you add code that writes a message to the output queue. The message includes the value passed to the HTTP trigger in the query string. For example, if the query string includes `name=Azure`

, the queue message is *Name passed to the function: Azure*.

In your function, select

**Code + Test**to display the function code in the editor.Update the function code, according to your function language:

Add an

**outputQueueItem**parameter to the method signature as shown in the following example:`public static async Task<IActionResult> Run(HttpRequest req, ICollector<string> outputQueueItem, ILogger log) { ... }`

In the body of the function, just before the

`return`

statement, add code that uses the parameter to create a queue message:`outputQueueItem.Add("Name passed to the function: " + name);`

Select

**Save**to save your changes.

## Test the function

After the code changes are saved, select

**Test**.Confirm that your test matches this screenshot, and then select

**Run**.Notice that the

**Request body**contains the`name`

value*Azure*. This value appears in the queue message created when the function is invoked.As an alternative to selecting

**Run**, you can call the function by entering a URL in a browser and specifying the`name`

value in the query string. This browser method is shown in[Create your first function from the Azure portal](functions-get-started).Check the logs to make sure that the function succeeded.

A new queue named

**outqueue**is created in your storage account by the Functions runtime when the output binding is first used. You use storage account to verify that the queue and a message in it were created.

### Find the storage account connected to AzureWebJobsStorage

In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, select**AzureWebJobsStorage**.Locate and make note of the account name.


### Examine the output queue

In the resource group for your function app, select the storage account that you're using.

Under

**Queue service**, select**Queues**, and select the queue named**outqueue**.The queue contains the message that the queue output binding created when you ran the HTTP-triggered function. If you invoked the function with the default

`name`

value of*Azure*, the queue message is*Name passed to the function: Azure*.Run the function again.

A new message appears in the queue.


## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

## Related content

In this article, you added an output binding to an existing function. For more information about binding to Queue Storage, see [Queue Storage trigger and bindings](functions-bindings-storage-queue).

[Azure Functions triggers and bindings concepts](functions-triggers-bindings)

Learn how Functions integrates with other services.[Azure Functions developer reference](functions-reference)

Provides more technical information about the Functions runtime and a reference for coding functions and defining triggers and bindings.[Code and test Azure Functions locally](functions-develop-local)

Describes the options for developing your functions locally.


---

<!-- DOCUMENTO FUSIONADO: functions-create-first-java-gradle.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-java-gradle -->

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

<!-- DOCUMENTO FUSIONADO: functions-bindings-storage-blob.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob -->

# Azure Blob storage bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with [Azure Storage](../storage/) via [triggers and bindings](functions-triggers-bindings). Integrating with Blob storage allows you to build functions that react to changes in blob data as well as read and write values.

| Action | Type |
|---|---|
| Run a function as blob storage data changes |
|

[Input binding](functions-bindings-storage-blob-input)[Output binding](functions-bindings-storage-blob-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [Azure.Storage.Blobs](/en-us/dotnet/api/azure.storage.blobs). Learn more about how these new types are different from `WindowsAzure.Storage`

and `Microsoft.Azure.Storage`

and how to migrate to them from the [Azure.Storage.Blobs Migration Guide](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/storage/Azure.Storage.Blobs/AzureStorageNetMigrationV12.md).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs), version 5.x or later.

Using the .NET CLI:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs
```


Note

Azure Blobs, Azure Queues, and Azure Tables now use separate extensions and are referenced individually. For example, to use the triggers and bindings for all three services in your .NET isolated-process app, you should add the following packages to your project:

[Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs)[Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues)[Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables)

Previously, the extensions shipped together as [Microsoft.Azure.Functions.Worker.Extensions.Storage, version 4.x](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/4.0.4). This same package also has a [5.x version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/5.0.0), which references the split packages for blobs and queues only. When upgrading your package references from older versions, you may therefore need to additionally reference the new [Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) NuGet package. Also, when referencing these newer split packages, make sure you are not referencing an older version of the combined storage package, as this will result in conflicts from two definitions of the same bindings.

If you're writing your application using F#, you must also configure this extension as part of the app's [startup configuration](dotnet-isolated-process-guide#start-up-and-configuration). In the call to `ConfigureFunctionsWorkerDefaults()`

or `ConfigureFunctionsWebApplication()`

, add a delegate that takes an `IFunctionsWorkerApplication`

parameter. Then within the body of that delegate, call `ConfigureBlobStorageExtension()`

on the object:

```
let hostBuilder = new HostBuilder()
hostBuilder.ConfigureFunctionsWorkerDefaults(fun (context: HostBuilderContext) (appBuilder: IFunctionsWorkerApplicationBuilder) ->
appBuilder.ConfigureBlobStorageExtension() |> ignore
) |> ignore
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

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below.

**Blob trigger**

The blob trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Blob input binding**

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

**Blob output binding**

When you want the function to write to a single blob, the blob output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | An object representing the content of a JSON blob. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple blobs, the blob output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single blob output binding types |
An array containing content for multiple blobs. Each entry represents the content of one blob. |

For other output scenarios, create and use a [BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient) or [BlobContainerClient](/en-us/dotnet/api/azure.storage.blobs.blobcontainerclient) with other types from [Azure.Storage.Blobs](/en-us/dotnet/api/azure.storage.blobs) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Types for Azure Storage Blob are generally available! Follow the [Python SDK Bindings for Blob Sample](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python) to get started with SDK Types for Blob in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| Blob trigger |
|

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_blobclient/function_app.py)`BlobClient`

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py)`ContainerClient`

`StorageStreamDownloader`

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient),[ContainerClient](/en-us/python/api/azure-storage-blob/azure.storage.blob.containerclient),[StorageStreamDownloader](/en-us/python/api/azure-storage-blob/azure.storage.blob.storagestreamdownloader)[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_blobclient/function_app.py)`BlobClient`

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py)`ContainerClient`

`StorageStreamDownloader`

## host.json settings

This section describes the function app configuration settings available for functions that use this binding. These settings only apply when using extension version 5.0.0 and higher. The example host.json file below contains only the version 2.x+ settings for this binding. For more information about function app configuration settings in versions 2.x and later versions, see [host.json reference for Azure Functions](functions-host-json).

Note

This section doesn't apply to extension versions before 5.0.0. For those earlier versions, there aren't any function app-wide configuration settings for blobs.

```
{
"version": "2.0",
"extensions": {
"blobs": {
"maxDegreeOfParallelism": 4,
"poisonBlobThreshold": 1
}
}
}
```


| Property | Default | Description |
|---|---|---|
| maxDegreeOfParallelism | 8 * (the number of available cores) | The integer number of concurrent invocations allowed for all blob-triggered functions in a given function app. The minimum allowed value is 1. |
| poisonBlobThreshold | 5 | The integer number of times to try processing a message before moving it to the poison queue. The minimum allowed value is 1. |


---

<!-- DOCUMENTO FUSIONADO: _container-concepts_functions-monitoring.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: container-concepts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/container-concepts -->

# Linux container support in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you plan and develop your individual functions to run in Azure Functions, you're typically focused on the code itself. Azure Functions makes it easy to deploy just your code project to a function app in Azure. When you deploy your project to a Linux function app, your code runs in a container that is created for you automatically and seamlessly integrates with Functions management tools.

Functions also supports containerized function app deployments. In a containerized deployment, you create your own function app instance in a local Docker container from a supported based image. You can then deploy this *containerized* function app to a hosting environment in Azure. Creating your own function app container lets you customize or otherwise control the immediate runtime environment of your function code.

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

## Container hosting options

There are several options for hosting your containerized function apps in Azure:

| Hosting option | Benefits |
|---|---|
|
Azure Functions provides integrated support for developing, deploying, and managing containerized function apps on
Recommended hosting option for containerized function apps n Azure. |

**Azure Arc-enabled Kubernetes clusters (preview)***Hosting Azure Functions containers on Azure Arc-enabled Kubernetes clusters is currently in preview.*For more information, see[Working with containers and Azure Functions](functions-how-to-custom-container?pivots=azure-arc).[Azure Functions](functions-how-to-custom-container?pivots=azure-functions#azure-portal-create-using-containers)[Elastic Premium](functions-premium-plan)or an[App Service (Dedicated)](dedicated-plan)plan. Use Container Apps hosting for rich container support from Container Apps. Premium plan hosting provides you with the benefits of dynamic scaling. You might want to use Dedicated plan hosting to take advantage of existing unused App Service plan resources.[Kubernetes](functions-kubernetes-keda)[KEDA](https://keda.sh)(Kubernetes-based Event Driven Autoscaling) pairs seamlessly with the Azure Functions runtime and tooling to provide event driven scale in Kubernetes.**Important:**Kubernetes hosting of your containerized function apps, either by using KEDA or by direct deployment, is an open-source effort that you can use free of cost.*Best-effort*support for this hosting scenario is provided only by contributors and by the community. You're responsible for maintaining your own function app containers in a cluster, even when deploying them to Azure Kubernetes Service (AKS).## Feature support comparison

The degree to which various features and behaviors of Azure Functions are supported when running your function app in a container depends on the container hosting option you choose.

| Feature/behavior |
|
|---|

[Container Apps (direct)](../container-apps/overview)

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)

[Kubernetes](functions-kubernetes-keda)

[Event-driven scaling](event-driven-scaling)5[scale rules](../container-apps/scale-app#scale-rules))1123[Scale-to-zero instances](event-driven-scaling#scale-in-behaviors)6678[Core Tools deployment](functions-run-local#deploy-containers)`func kubernetes`

[Revisions](../container-apps/revisions)[Yes](../container-apps/revisions)[Deployment slots](functions-deployment-slots)[Streaming logs](streaming-logs)[Yes](../container-apps/log-streaming)[Yes](../container-apps/log-streaming)[Console access](../container-apps/container-console)[Yes](../container-apps/container-console)[Kudu](functions-how-to-custom-container#enable-ssh-connections))[Kudu](functions-how-to-custom-container#enable-ssh-connections))[using](https://kubernetes.io/docs/reference/kubectl/))`kubectl`

[Scale rules](../container-apps/scale-app#scale-rules)[Always-ready/pre-warmed instances](functions-premium-plan#eliminate-cold-starts)[App Service authentication](../app-service/overview-authentication-authorization)[Yes](../container-apps/authentication)[Custom domain names](../app-service/app-service-web-tutorial-custom-domain)[Yes](../container-apps/custom-domains-certificates)[Private key certificates](../app-service/overview-tls)[Yes](../container-apps/custom-domains-certificates)[Yes](../container-apps/networking)[Yes](/en-us/azure/reliability/reliability-azure-container-apps)[Yes](../container-apps/troubleshooting#use-the-diagnose-and-solve-problems-tool)[Yes](../container-apps/troubleshooting#use-the-diagnose-and-solve-problems-tool)[Yes](functions-diagnostics)[Yes](functions-diagnostics)[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[Configurable memory/CPU count](../container-apps/workload-profiles-overview)[Yes](../container-apps/billing#consumption-plan)[Yes](../container-apps/billing#consumption-plan)[Container Apps billing](../container-apps/billing)[Container Apps billing](../container-apps/billing)[Premium plan billing](functions-premium-plan#billing)[Dedicated plan billing](dedicated-plan#billing)[AKS pricing](/en-us/azure/aks/free-standard-pricing-tiers)- On Container Apps, the default is 10 instances, but you can set the
[maximum number of replicas](../container-apps/scale-app#scale-definition), which has an overall maximum of 1000. This setting is honored as long as there's enough cores quota available. When you create your function app from the Azure portal, you're limited to 300 instances. - In some regions, Linux apps on a Premium plan can scale to 100 instances. For more information, see the
[Premium plan article](functions-premium-plan#region-max-scale-out). - For specific limits for the various App Service plan options, see the
[App Service plan limits](../azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits). - Requires
[KEDA](functions-kubernetes-keda); supported by most triggers. To learn which triggers support event-driven scaling, see[Considerations for Container Apps hosting](functions-container-apps-hosting#considerations-for-container-apps-hosting). - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to zero, the default timeout depends on the specific triggers used in the app. - There's no maximum execution timeout duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors), and a grace period of 10 minutes is given during platform updates. - Requires the App Service plan be set to
[Always On](dedicated-plan#always-on). A grace period of 10 minutes is given during platform updates.

## Maintaining custom containers

When creating your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific and are found in the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container.

Choose your base image based on the language stack you're using in your function app. The following table provides examples for each stack. In general, the tag should start with `4-`

to indicate the V4 Functions runtime. When new minor versions are released, this tag will be updated to point to the new version. As you periodically rebuild your custom image, you will pull the new versions through that same tag, allowing your app to have the same updates. You shouldn't use tags that specify minor runtime versions, as these will not receive updates, and your app will potentially remain on an unpatched version, no matter how often you rebuild your custom image.

| Language Stack | Example recommended base image tags |
|---|---|
| .NET (isolated worker model) | `mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0` or`mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0-appservice` (These examples target .NET 8. Select the appropriate image for the .NET version you need.) |
| .NET (legacy in-process model) | `mcr.microsoft.com/azure-functions/dotnet:4-dotnet8.0` or`mcr.microsoft.com/azure-functions/dotnet:4-dotnet8.0-appservice` (Support will end for the in-process model on November 10, 2026. You should
|
| Java | `mcr.microsoft.com/azure-functions/java:4-java21` or`mcr.microsoft.com/azure-functions/java:4-java21-appservice` (These examples target Java 21. Select the appropriate image for the Java version you need.) |
| Node.js (JavaScript or TypeScript) | `mcr.microsoft.com/azure-functions/node:4-node22` or`mcr.microsoft.com/azure-functions/node:4-node22-appservice` (These examples target Node.js 22. Select the appropriate image for the Node.js version you need.) |
| PowerShell | `mcr.microsoft.com/azure-functions/powershell:4-powershell7.4` or`mcr.microsoft.com/azure-functions/powershell:4-powershell7.4-appservice` (These examples target PowerShell 7.4. Select the appropriate image for the PowerShell version you need.) |
| Python | `mcr.microsoft.com/azure-functions/python:4-python3.12` or`mcr.microsoft.com/azure-functions/python:4-python3.12-appservice` (These examples target Python 3.12. Select the appropriate image for the Python version you need.) |
| Custom handlers / other | `mcr.microsoft.com/azure-functions/base:4` or`mcr.microsoft.com/azure-functions/base:4-appservice` |

Base images ending in `-appservice`

enable SSH and remote debugging from the platform. Unless you need these capabilities, you can use the base images without the `-appservice`

suffix.

Important

It isn't sufficient to just have one of the above tags in your Dockerfile. You need to regularly pull the latest image from that tag so that your custom image can be rebuilt to include the latest updates. If you don't pull the latest image and rebuild, your app will continue to run on the old base image.

When you create or deploy your own containerized app using a custom image, you're responsible for making sure that your custom image staying up-to-date with our released base images. In addition to new features and improvements, these base image updates can also include security updates that are critical for your app. To ensure your app is protected, make sure you're staying up to date. You should regularly pull the latest version of the base image, rebuild your custom container image, and redeploy your app to use it.

In some cases, we're required to make platform-level changes that could mean that an app in a custom container using an old base image might stop working properly. For such major changes, we roll out updated images well in advance so that apps that take regular updates aren't negatively impacted. To avoid potential problems with your apps running in custom containers, make sure you don't fall too far behind the latest minor version released. During a support case, should we determine that your app is experiencing problems because it's on an older or unsupported version, we do request that you update your container to the latest base image version before continuing with support.

## Getting started

Use these links to get started working with Azure Functions in Linux containers:

| I want to... | See article: |
|---|---|
| Create my first containerized functions |
|


---

<!-- DOCUMENTO FUSIONADO: functions-monitoring.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-monitoring -->

# Monitor executions in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Functions](functions-overview) offers built-in integration with Azure Application Insights to monitor functions executions. This article provides an overview of the monitoring capabilities provided by Azure for monitoring Azure Functions.

Application Insights collects log, performance, and error data. By automatically detecting performance anomalies and featuring powerful analytics tools, you can more easily diagnose issues and better understand how your functions are used. These tools are designed to help you continuously improve performance and usability of your functions. You can even use Application Insights during local function app project development. For more information, see [Introduction to Application Insights](/en-us/azure/azure-monitor/app/app-insights-overview).

As Application Insights instrumentation is built into Azure Functions, you need a valid instrumentation key to connect your function app to an Application Insights resource. The instrumentation key is added to your application settings as you create your function app resource in Azure. If your function app doesn't already have this key, you can [set it manually](configure-monitoring#enable-application-insights-integration).

You can also monitor the function app itself by using Azure Monitor. To learn more, see [Monitor Azure Functions](monitor-functions).

## Application Insights pricing and limits

You can try out Application Insights integration with Azure Functions for free featuring a daily limit to how much data is processed for free.

If you enable Applications Insights during development, you might hit this limit during testing. Azure provides portal and email notifications when you're approaching your daily limit. If you miss those alerts and hit the limit, new logs don't appear in Application Insights queries. Be aware of the limit to avoid unnecessary troubleshooting time. For more information, see [Application Insights billing](/en-us/azure/azure-monitor/logs/cost-logs#application-insights-billing).

Important

Application Insights has a [sampling](/en-us/azure/azure-monitor/app/sampling) feature that can protect you from producing too much telemetry data on completed executions at times of peak load. Sampling is enabled by default. If you appear to be missing data, you might need to adjust the sampling settings to fit your particular monitoring scenario. To learn more, see [Configure sampling](configure-monitoring#configure-sampling).

## Application Insights integration

Typically, you create an Application Insights instance when you create your function app. In this case, the instrumentation key required for the integration is already set as an application setting named `APPINSIGHTS_INSTRUMENTATIONKEY`

. If for some reason your function app doesn't have the instrumentation key set, you need to [enable Application Insights integration](configure-monitoring#enable-application-insights-integration).

Important

Sovereign clouds, such as Azure Government, require the use of the Application Insights connection string (`APPLICATIONINSIGHTS_CONNECTION_STRING`

) instead of the instrumentation key. To learn more, see the [APPLICATIONINSIGHTS_CONNECTION_STRING reference](functions-app-settings#applicationinsights_connection_string).

The following table details the supported features of Application Insights available for monitoring your function apps:

| Azure Functions runtime version | 1.x | 4.x+ |
|---|---|---|
Automatic collection of |
||
| • Requests | ✓ | ✓ |
| • Exceptions | ✓ | ✓ |
| • Performance Counters | ✓ | ✓ |
| • Dependencies | ||
| — HTTP | ✓ | |
| — Service Bus | ✓ | |
| — Event Hubs | ✓ | |
| — SQL* | ✓ | |
Supported features |
||
| • QuickPulse/LiveMetrics | Yes | Yes |
| — Secure Control Channel | Yes | |
| • Sampling | Yes | Yes |
| • Heartbeats | Yes | |
Correlation |
||
| • Service Bus | Yes | |
| • Event Hubs | Yes | |
Configurable |
||
| •
|

* To enable the collection of SQL query string text, see [Enable SQL query collection](configure-monitoring#enable-sql-query-collection).

## Collecting telemetry data

With Application Insights integration enabled, telemetry data is sent to your connected Application Insights instance. This data includes logs generated by the Functions host, traces written from your functions code, and performance data.

Note

In addition to data from your functions and the Functions host, you can also collect data from the [Functions scale controller](#scale-controller-logs).

### Log levels and categories

When you write traces from your application code, you should assign a log level to the traces. Log levels provide a way for you to limit the amount of data that is collected from your traces.

A *log level* is assigned to every log. The value is an integer that indicates relative importance:

| LogLevel | Code | Description |
|---|---|---|
| Trace | 0 | Logs that contain the most detailed messages. These messages might contain sensitive application data. These messages are disabled by default and should never be enabled in a production environment. |
| Debug | 1 | Logs that are used for interactive investigation during development. These logs should primarily contain information useful for debugging and have no long-term value. |
| Information | 2 | Logs that track the general flow of the application. These logs should have long-term value. |
| Warning | 3 | Logs that highlight an abnormal or unexpected event in the application flow, but don't otherwise cause the application execution to stop. |
| Error | 4 | Logs that highlight when the current flow of execution is stopped because of a failure. These errors should indicate a failure in the current activity, not an application-wide failure. |
| Critical | 5 | Logs that describe an unrecoverable application or system crash, or a catastrophic failure that requires immediate attention. |
| None | 6 | Disables logging for the specified category. |

The [ host.json file](functions-host-json) configuration determines how much logging a functions app sends to Application Insights.

To learn more about log levels, see [Configure log levels](configure-monitoring#configure-log-levels).

By assigning logged items to a category, you have more control over telemetry generated from specific sources in your function app. Categories make it easier to run analytics over collected data. Traces written from your function code are assigned to individual categories based on the function name. To learn more about categories, see [Configure categories](configure-monitoring#configure-categories).

### Custom telemetry data

In [C#](functions-dotnet-class-library#log-custom-telemetry-in-c-functions), [JavaScript](functions-reference-node#track-custom-data), and [Python](functions-reference-python#logging-and-monitoring), you can use an Application Insights SDK to write custom telemetry data.

### Dependencies

Starting with version 2.x of Functions, Application Insights automatically collects data on dependencies for bindings that use certain client SDKs. Application Insights collects data on the following dependencies:

- Azure Cosmos DB
- Azure Event Hubs
- Azure Service Bus
- Azure Storage services (Blob, Queue, and Table)

HTTP requests and database calls using `SqlClient`

are also captured. For the complete list of dependencies supported by Application Insights, see [automatically tracked dependencies](/en-us/azure/azure-monitor/app/asp-net-dependencies#automatically-tracked-dependencies).

Application Insights generates an *application map* of collected dependency data. The following is an example of an application map of an HTTP trigger function with a Queue storage output binding.


Dependencies are written at the `Information`

level. If you filter at `Warning`

or above, you don't see the dependency data. Also, automatic collection of dependencies happens at a non-user scope. To capture dependency data, make sure the level is set to at least `Information`

outside the user scope (`Function.<YOUR_FUNCTION_NAME>.User`

) in your host.

In addition to automatic dependency data collection, you can also use one of the language-specific Application Insights SDKs to write custom dependency information to the logs. For an example how to write custom dependencies, see one of the following language-specific examples:

[Log custom telemetry in C# functions](functions-dotnet-class-library#log-custom-telemetry-in-c-functions)[Log custom telemetry in JavaScript functions](functions-reference-node#track-custom-data)[Log custom telemetry in Python functions](functions-reference-python#logging-and-monitoring)

### Performance Counters

Automatic collection of Performance Counters isn't supported when running on Linux.

## Writing to logs

The way that you write to logs and the APIs you use depend on the language of your function app project. See the developer guide for your language to learn more about writing logs from your functions.

## Analyze data

By default, the data collected from your function app is stored in Application Insights. In the [Azure portal](https://portal.azure.com), Application Insights provides an extensive set of visualizations of your telemetry data. You can drill into error logs and query events and metrics. To learn more, including basic examples of how to view and query your collected data, see [Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data).

## Streaming Logs

While developing an application, you often want to see what's being written to the logs in near real time when running in Azure.

There are two ways to view a stream of the log data being generated by your function executions.

**Built-in log streaming**: the App Service platform lets you view a stream of your application log files. This stream is equivalent to the output seen when you debug your functions during[local development](functions-develop-local)and when you use the**Test**tab in the portal. All log-based information is displayed. For more information, see[Stream logs](../app-service/troubleshoot-diagnostic-logs#stream-logs). This streaming method supports only a single instance, and can't be used with an app running on Linux in a Consumption plan.**Live Metrics Stream**: when your function app is[connected to Application Insights](configure-monitoring#enable-application-insights-integration), you can view log data and other metrics in near real time in the Azure portal using[Live Metrics Stream](/en-us/azure/azure-monitor/app/live-stream). Use this method when monitoring functions running on multiple-instances or on Linux in a Consumption plan. This method uses[sampled data](configure-monitoring#configure-sampling).

Log streams can be viewed both in the portal and in most local development environments. To learn how to enable log streams, see [Enable streaming execution logs in Azure Functions](streaming-logs).

## Diagnostic logs

Application Insights lets you export telemetry data to long-term storage or other analysis services.

Because Functions also integrates with Azure Monitor, you can also use diagnostic settings to send telemetry data to various destinations, including Azure Monitor logs. To learn more, see [Monitor Azure Functions](functions-monitor-log-analytics).

## Scale controller logs

The [Azure Functions scale controller](event-driven-scaling#runtime-scaling) monitors instances of the Azure Functions host on which your app runs. This controller makes decisions about when to add or remove instances based on current performance. You can have the scale controller emit logs to Application Insights to better understand the decisions the scale controller is making for your function app. You can also store the generated logs in Blob storage for analysis by another service.

To enable this feature, you add an application setting named `SCALE_CONTROLLER_LOGGING_ENABLED`

to your function app settings. To learn how, see [Configure scale controller logs](configure-monitoring#configure-scale-controller-logs).

## Azure Monitor metrics

In addition to log-based telemetry data collected by Application Insights, you can also get data about how the function app is running from [Azure Monitor Metrics](/en-us/azure/azure-monitor/essentials/data-platform-metrics). To learn more, see [Monitor Azure Functions](monitor-functions).

## Report issues

To report an issue with Application Insights integration in Functions, or to make a suggestion or request, [create an issue in GitHub](https://github.com/Azure/Azure-Functions/issues/new).

## Next steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-terraform -->

# Quickstart: Create and deploy Azure Functions resources from Terraform

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use Terraform to create a function app in a Flex Consumption plan in Azure Functions, along with other required Azure resources. The Flex Consumption plan provides serverless hosting that lets you run your code on demand without explicitly provisioning or managing infrastructure. The function app runs on Linux and is configured to use Azure Blob storage for code deployments.

[Terraform](https://www.terraform.io) enables the definition, preview, and deployment of cloud infrastructure. Using Terraform, you create configuration files using [HCL syntax](https://developer.hashicorp.com/terraform/language/syntax/configuration). The HCL syntax allows you to specify the cloud provider - such as Azure - and the elements that make up your cloud infrastructure. After you create your configuration files, you create an *execution plan* that allows you to preview your infrastructure changes before they're deployed. Once you verify the changes, you apply the execution plan to deploy the infrastructure.

- Create an Azure resource group with a unique name.
- Generate a random string of 13 lowercase letters to name resources.
- Create a storage account in Azure.
- Create a blob storage container in the storage account.
- Create a Flex Consumption plan in Azure Functions.
- Create a function app with a Flex Consumption plan in Azure.
- Output the names of the resource group, storage account, service plan, function app, and Azure Functions Flex Consumption plan.

## Prerequisites

- Create an Azure account with an active subscription. You can
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). [Install and configure Terraform](/en-us/azure/developer/terraform/quickstart-configure).[Install the Azure CLI](/en-us/cli/azure/install-azure-cli)to obtain the subscription ID or run in[Azure Cloud Shell](/en-us/azure/cloud-shell/overview).

## Implement the Terraform code

The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/101-azure-functions). You can view the log file containing the [test results from current and previous versions of Terraform](https://github.com/Azure/terraform/tree/master/quickstart/101-azure-functions/TestRecord.md). See more [articles and sample code showing how to use Terraform to manage Azure resources](/en-us/azure/terraform).

Create a directory in which to test and run the sample Terraform code, and make it the current directory.

Create a file named

`main.tf`

, and insert the following code:`# This Terraform configuration creates a Flex Consumption plan app in Azure Functions # with the required Storage account and Blob Storage deployment container. # Create a random pet to generate a unique resource group name resource "random_pet" "rg_name" { prefix = var.resource_group_name_prefix } # Create a resource group resource "azurerm_resource_group" "example" { location = var.resource_group_location name = random_pet.rg_name.id } # Random String for unique naming of resources resource "random_string" "name" { length = 8 special = false upper = false lower = true numeric = false } # Create a storage account resource "azurerm_storage_account" "example" { name = coalesce(var.sa_name, random_string.name.result) resource_group_name = azurerm_resource_group.example.name location = azurerm_resource_group.example.location account_tier = var.sa_account_tier account_replication_type = var.sa_account_replication_type } # Create a storage container resource "azurerm_storage_container" "example" { name = "example-flexcontainer" storage_account_id = azurerm_storage_account.example.id container_access_type = "private" } # Create a Log Analytics workspace for Application Insights resource "azurerm_log_analytics_workspace" "example" { name = coalesce(var.ws_name, random_string.name.result) location = azurerm_resource_group.example.location resource_group_name = azurerm_resource_group.example.name sku = "PerGB2018" retention_in_days = 30 } # Create an Application Insights instance for monitoring resource "azurerm_application_insights" "example" { name = coalesce(var.ai_name, random_string.name.result) location = azurerm_resource_group.example.location resource_group_name = azurerm_resource_group.example.name application_type = "web" workspace_id = azurerm_log_analytics_workspace.example.id } # Create a service plan resource "azurerm_service_plan" "example" { name = coalesce(var.asp_name, random_string.name.result) resource_group_name = azurerm_resource_group.example.name location = azurerm_resource_group.example.location sku_name = "FC1" os_type = "Linux" } # Create a function app resource "azurerm_function_app_flex_consumption" "example" { name = coalesce(var.fa_name, random_string.name.result) resource_group_name = azurerm_resource_group.example.name location = azurerm_resource_group.example.location service_plan_id = azurerm_service_plan.example.id storage_container_type = "blobContainer" storage_container_endpoint = "${azurerm_storage_account.example.primary_blob_endpoint}${azurerm_storage_container.example.name}" storage_authentication_type = "StorageAccountConnectionString" storage_access_key = azurerm_storage_account.example.primary_access_key runtime_name = var.runtime_name runtime_version = var.runtime_version maximum_instance_count = 50 instance_memory_in_mb = 2048 site_config { } }`

Create a file named

`outputs.tf`

, and insert the following code:`output "resource_group_name" { value = azurerm_resource_group.example.name } output "sa_name" { value = azurerm_storage_account.example.name } output "asp_name" { value = azurerm_service_plan.example.name } output "fa_name" { value = azurerm_function_app_flex_consumption.example.name } output "fa_url" { value = "https://${azurerm_function_app_flex_consumption.example.name}.azurewebsites.net" }`

Create a file named

`providers.tf`

, and insert the following code:`terraform { required_version = ">=1.0" required_providers { azurerm = { source = "hashicorp/azurerm" version = "~>4.0" } random = { source = "hashicorp/random" version = "~>3.0" } } } provider "azurerm" { features {} }`

Create a file named

`variables.tf`

, and insert the following code:`variable "resource_group_name" { type = string default = "" description = "The name of the Azure resource group. If blank, a random name will be generated." } variable "resource_group_name_prefix" { type = string default = "rg" description = "Prefix of the resource group name that's combined with a random ID so name is unique in your Azure subscription." } variable "resource_group_location" { type = string default = "eastus" description = "Location of the resource group." } variable "sa_account_tier" { description = "The tier of the storage account. Possible values are Standard and Premium." type = string default = "Standard" } variable "sa_account_replication_type" { description = "The replication type of the storage account. Possible values are LRS, GRS, RAGRS, and ZRS." type = string default = "LRS" } variable "sa_name" { description = "The name of the storage account. If blank, a random name will be generated." type = string default = "" } variable "ws_name" { description = "The name of the Log Analytics workspace. If blank, a random name will be generated." type = string default = "" } variable "ai_name" { description = "The name of the Application Insights instance. If blank, a random name will be generated." type = string default = "" } variable "asp_name" { description = "The name of the App Service Plan. If blank, a random name will be generated." type = string default = "" } variable "fa_name" { description = "The name of the Function App. If blank, a random name will be generated." type = string default = "" } variable "runtime_name" { description = "The name of the language worker runtime." type = string default = "node" # Allowed: dotnet-isolated, java, node, powershell, python } variable "runtime_version" { description = "The version of the language worker runtime." type = string default = "20" # Supported versions: see https://aka.ms/flexfxversions }`

Use this Azure CLI command to set the

`ARM_SUBSCRIPTION_ID`

environment variable to the ID of your current subscription:`export ARM_SUBSCRIPTION_ID=$(az account show --query "id" --output tsv)`

You must have this variable set for Terraform to be able to authenticate to your Azure subscription.


## Initialize Terraform

Run [terraform init](https://www.terraform.io/docs/commands/init.html) to initialize the Terraform deployment. This command downloads the Azure provider required to manage your Azure resources.

```
terraform init -upgrade
```


**Key points:**

- The
`-upgrade`

parameter upgrades the necessary provider plugins to the newest version that complies with the configuration's version constraints.

## Create a Terraform execution plan

Run [terraform plan](https://www.terraform.io/docs/commands/plan.html) to create an execution plan.

```
terraform plan -out main.tfplan -var="runtime_name=dotnet-isolated" -var="runtime_version=8"
```


```
terraform plan -out main.tfplan -var="runtime_name=powershell" -var="runtime_version=7.4"
```


```
terraform plan -out main.tfplan -var="runtime_name=python" -var="runtime_version=3.12"
```


```
terraform plan -out main.tfplan -var="runtime_name=java" -var="runtime_version=21"
```


```
terraform plan -out main.tfplan -var="runtime_name=node" -var="runtime_version=20"
```


Make sure that `runtime_version`

matches the language stack version you verified locally. Select your preferred language stack at the [top](#top) of the article.

**Key points:**

- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

## Apply a Terraform execution plan

Run [terraform apply](https://www.terraform.io/docs/commands/apply.html) to apply the execution plan to your cloud infrastructure.

```
terraform apply main.tfplan
```


**Key points:**

- The example
`terraform apply`

command assumes you previously ran`terraform plan -out main.tfplan`

. - If you specified a different filename for the
`-out`

parameter, use that same filename in the call to`terraform apply`

. - If you didn't use the
`-out`

parameter, call`terraform apply`

without any parameters.

## Verify the results

The `outputs.tf`

file returns these values for your new function app:

| Value | Description |
|---|---|
`resource_group_name` |
The name of the resource group you created. |
`sa_name` |
The name of the Azure storage account required by the Functions host. |
`asp_name` |
The name of the Flex Consumption plan that hosts your new app. |
`fa_name` |
The name of your new function app. |
`fa_url` |
The URL of your new function app endpoint. |

Open a browser and browse to the URL location in `fa_url`

. You can also use the [terraform output](https://developer.hashicorp.com/terraform/cli/commands/output) command to review these values at a later time.


## Clean up resources

When you no longer need the resources created via Terraform, do the following steps:

Run

[terraform plan](https://www.terraform.io/docs/commands/plan.html)and specify the`destroy`

flag.`terraform plan -destroy -out main.destroy.tfplan`

**Key points:**- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

- The
Run

[terraform apply](https://www.terraform.io/docs/commands/apply.html)to apply the execution plan.`terraform apply main.destroy.tfplan`


## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure](/en-us/azure/developer/terraform/troubleshoot).

## Next steps

You can now deploy a code project to the function app resources you created in Azure.

You can create, verify, and deploy a code project to your new function app from these local environments:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-bicep -->

# Quickstart: Create and deploy Azure Functions resources using Bicep

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use Bicep to create a function app in a Flex Consumption plan in Azure, along with its required Azure resources. The function app provides a serverless execution context for your function code executions. The app uses Microsoft Entra ID with managed identities to connect to other Azure resources.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

[Bicep](/en-us/azure/azure-resource-manager/bicep/overview) is a domain-specific language (DSL) that uses declarative syntax to deploy Azure resources. It provides concise syntax, reliable type safety, and support for code reuse. Bicep offers the best authoring experience for your infrastructure-as-code solutions in Azure.

After you create the function app, you can deploy your Azure Functions project code to that app. A final code deployment step is outside the scope of this quickstart article.

## Prerequisites

### Azure account

Before you begin, you must have an Azure account with an active subscription. [Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Review the Bicep file

The Bicep file used in this quickstart is from an [Azure Quickstart Template](https://github.com/Azure/azure-quickstart-templates/blob/master/quickstarts/microsoft.web/function-app-flex-managed-identities/main.bicep).

```
/* This Bicep file creates a function app running in a Flex Consumption plan
that connects to Azure Storage by using managed identities with Microsoft Entra ID. */
//********************************************
// Parameters
//********************************************
@description('Primary region for all Azure resources.')
@minLength(1)
param location string = resourceGroup().location
@description('Language runtime used by the function app.')
@allowed(['dotnet-isolated','python','java', 'node', 'powerShell'])
param functionAppRuntime string = 'dotnet-isolated' //Defaults to .NET isolated worker
@description('Target language version used by the function app.')
@allowed(['3.10','3.11', '7.4', '8.0', '9.0', '10', '11', '17', '20'])
param functionAppRuntimeVersion string = '8.0' //Defaults to .NET 8.
@description('The maximum scale-out instance count limit for the app.')
@minValue(40)
@maxValue(1000)
param maximumInstanceCount int = 100
@description('The memory size of instances used by the app.')
@allowed([2048,4096])
param instanceMemoryMB int = 2048
@description('A unique token used for resource name generation.')
@minLength(3)
param resourceToken string = toLower(uniqueString(subscription().id, location))
@description('A globally unique name for your deployed function app.')
param appName string = 'func-${resourceToken}'
//********************************************
// Variables
//********************************************
// Generates a unique container name for deployments.
var deploymentStorageContainerName = 'app-package-${take(appName, 32)}-${take(resourceToken, 7)}'
// Key access to the storage account is disabled by default
var storageAccountAllowSharedKeyAccess = false
// Define the IDs of the roles we need to assign to our managed identities.
var storageBlobDataOwnerRoleId = 'b7e6dc6d-f1e8-4753-8033-0f276bb0955b'
var storageBlobDataContributorRoleId = 'ba92f5b4-2d11-453d-a403-e96b0029c9fe'
var storageQueueDataContributorId = '974c5e8b-45b9-4653-ba55-5f855dd0fb88'
var storageTableDataContributorId = '0a9a7e1f-b9d0-4cc4-a60d-0319b160aaa3'
var monitoringMetricsPublisherId = '3913510d-42f4-4e42-8a64-420c390055eb'
//********************************************
// Azure resources required by your function app.
//********************************************
resource logAnalytics 'Microsoft.OperationalInsights/workspaces@2023-09-01' = {
name: 'log-${resourceToken}'
location: location
properties: any({
retentionInDays: 30
features: {
searchVersion: 1
}
sku: {
name: 'PerGB2018'
}
})
}
resource applicationInsights 'Microsoft.Insights/components@2020-02-02' = {
name: 'appi-${resourceToken}'
location: location
kind: 'web'
properties: {
Application_Type: 'web'
WorkspaceResourceId: logAnalytics.id
DisableLocalAuth: true
}
}
resource storage 'Microsoft.Storage/storageAccounts@2023-05-01' = {
name: 'st${resourceToken}'
location: location
kind: 'StorageV2'
sku: { name: 'Standard_LRS' }
properties: {
accessTier: 'Hot'
allowBlobPublicAccess: false
allowSharedKeyAccess: storageAccountAllowSharedKeyAccess
dnsEndpointType: 'Standard'
minimumTlsVersion: 'TLS1_2'
networkAcls: {
bypass: 'AzureServices'
defaultAction: 'Allow'
}
publicNetworkAccess: 'Enabled'
}
resource blobServices 'blobServices' = {
name: 'default'
properties: {
deleteRetentionPolicy: {}
}
resource deploymentContainer 'containers' = {
name: deploymentStorageContainerName
properties: {
publicAccess: 'None'
}
}
}
}
resource userAssignedIdentity 'Microsoft.ManagedIdentity/userAssignedIdentities@2023-01-31' = {
name: 'uai-data-owner-${resourceToken}'
location: location
}
resource roleAssignmentBlobDataOwner 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, storage.id, userAssignedIdentity.id, 'Storage Blob Data Owner')
scope: storage
properties: {
roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', storageBlobDataOwnerRoleId)
principalId: userAssignedIdentity.properties.principalId
principalType: 'ServicePrincipal'
}
}
resource roleAssignmentBlob 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, storage.id, userAssignedIdentity.id, 'Storage Blob Data Contributor')
scope: storage
properties: {
roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', storageBlobDataContributorRoleId)
principalId: userAssignedIdentity.properties.principalId
principalType: 'ServicePrincipal'
}
}
resource roleAssignmentQueueStorage 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, storage.id, userAssignedIdentity.id, 'Storage Queue Data Contributor')
scope: storage
properties: {
roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', storageQueueDataContributorId)
principalId: userAssignedIdentity.properties.principalId
principalType: 'ServicePrincipal'
}
}
resource roleAssignmentTableStorage 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, storage.id, userAssignedIdentity.id, 'Storage Table Data Contributor')
scope: storage
properties: {
roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', storageTableDataContributorId)
principalId: userAssignedIdentity.properties.principalId
principalType: 'ServicePrincipal'
}
}
resource roleAssignmentAppInsights 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(subscription().id, applicationInsights.id, userAssignedIdentity.id, 'Monitoring Metrics Publisher')
scope: applicationInsights
properties: {
roleDefinitionId: subscriptionResourceId('Microsoft.Authorization/roleDefinitions', monitoringMetricsPublisherId)
principalId: userAssignedIdentity.properties.principalId
principalType: 'ServicePrincipal'
}
}
//********************************************
// Function app and Flex Consumption plan definitions
//********************************************
resource appServicePlan 'Microsoft.Web/serverfarms@2024-04-01' = {
name: 'plan-${resourceToken}'
location: location
kind: 'functionapp'
sku: {
tier: 'FlexConsumption'
name: 'FC1'
}
properties: {
reserved: true
}
}
resource functionApp 'Microsoft.Web/sites@2024-04-01' = {
name: appName
location: location
kind: 'functionapp,linux'
identity: {
type: 'UserAssigned'
userAssignedIdentities: {
'${userAssignedIdentity.id}':{}
}
}
properties: {
serverFarmId: appServicePlan.id
httpsOnly: true
siteConfig: {
minTlsVersion: '1.2'
}
functionAppConfig: {
deployment: {
storage: {
type: 'blobContainer'
value: '${storage.properties.primaryEndpoints.blob}${deploymentStorageContainerName}'
authentication: {
type: 'UserAssignedIdentity'
userAssignedIdentityResourceId: userAssignedIdentity.id
}
}
}
scaleAndConcurrency: {
maximumInstanceCount: maximumInstanceCount
instanceMemoryMB: instanceMemoryMB
}
runtime: {
name: functionAppRuntime
version: functionAppRuntimeVersion
}
}
}
resource configAppSettings 'config' = {
name: 'appsettings'
properties: {
AzureWebJobsStorage__accountName: storage.name
AzureWebJobsStorage__credential : 'managedidentity'
AzureWebJobsStorage__clientId: userAssignedIdentity.properties.clientId
APPINSIGHTS_INSTRUMENTATIONKEY: applicationInsights.properties.InstrumentationKey
APPLICATIONINSIGHTS_AUTHENTICATION_STRING: 'ClientId=${userAssignedIdentity.properties.clientId};Authorization=AAD'
}
}
}
```


This deployment file creates these Azure resources needed by a function app that securely connects to Azure services:

: creates your function app.**Microsoft.Web/sites**: creates a serverless Flex Consumption hosting plan for your app.**Microsoft.Web/serverfarms**: creates an Azure Storage account, which is required by Functions.**Microsoft.Storage/storageAccounts**: creates an Application Insights instance for monitoring your app.**Microsoft.Insights/components**: creates a workspace required by Application Insights.**Microsoft.OperationalInsights/workspaces**: creates a user-assigned managed identity that's used by the app to authenticate with other Azure services using Microsoft Entra.**Microsoft.ManagedIdentity/userAssignedIdentities**: creates role assignments to the user-assigned managed identity, which provide the app with least-privilege access when connecting to other Azure services.**Microsoft.Authorization/roleAssignments**

Deployment considerations:

- The storage account is used to store important app data, including the application code deployment package. This deployment creates a storage account that is accessed using Microsoft Entra ID authentication and managed identities. Identity access is granted on a least-permissions basis.
- The Bicep file defaults to creating a C# app that uses .NET 8 in an isolated process. For other languages, use the
`functionAppRuntime`

and`functionAppRuntimeVersion`

parameters to specify the specific language and version on which to run your app. Make sure to select your programming language at the[top](#top)of the article.

## Deploy the Bicep file

Save the Bicep file as

**main.bicep**to your local computer.Deploy the Bicep file using either Azure CLI or Azure PowerShell.

`az group create --name exampleRG --location <SUPPORTED_REGION> az deployment group create --resource-group exampleRG --template-file main.bicep --parameters functionAppRuntime=dotnet-isolated functionAppRuntimeVersion=8.0`

`az group create --name exampleRG --location <SUPPORTED_REGION> az deployment group create --resource-group exampleRG --template-file main.bicep --parameters functionAppRuntime=java functionAppRuntimeVersion=17`

`az group create --name exampleRG --location <SUPPORTED_REGION> az deployment group create --resource-group exampleRG --template-file main.bicep --parameters functionAppRuntime=node functionAppRuntimeVersion=20`

`az group create --name exampleRG --location <SUPPORTED_REGION> az deployment group create --resource-group exampleRG --template-file main.bicep --parameters functionAppRuntime=python functionAppRuntimeVersion=3.11`

`az group create --name exampleRG --location <SUPPORTED_REGION> az deployment group create --resource-group exampleRG --template-file main.bicep --parameters functionAppRuntime=powerShell functionAppRuntimeVersion=7.4`

In this example, replace

`<SUPPORTED_REGION>`

with a region that[supports the Flex Consumption plan](flex-consumption-how-to#view-currently-supported-regions).When the deployment finishes, you should see a message indicating the deployment succeeded.


## Validate the deployment

Use Azure CLI or Azure PowerShell to validate the deployment.

```
az resource list --resource-group exampleRG
```


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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-sql-output -->

# Azure SQL output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure SQL output binding lets you write to a database.

For information on setup and configuration details, see the [overview](functions-bindings-azure-sql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-outofproc).

This section contains the following examples:

The examples refer to a `ToDoItem`

class and a corresponding database table:

```
namespace AzureSQL.ToDo
{
public class ToDoItem
{
public Guid Id { get; set; }
public int? order { get; set; }
public string title { get; set; }
public string url { get; set; }
public bool? completed { get; set; }
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


To return [multiple output bindings](dotnet-isolated-process-guide#multiple-output-bindings) in our samples, we create a custom return type:

```
public static class OutputType
{
[SqlOutput("dbo.ToDo", connectionStringSetting: "SqlConnectionString")]
public static ToDoItem ToDoItem { get; set; }
public static HttpResponseData HttpResponse { get; set; }
}
```


### HTTP trigger, write one record

The following example shows a [C# function](functions-dotnet-class-library) that adds a record to a database, using data provided in an HTTP POST request as a JSON body. The return object is the `OutputType`

class we created to handle both an HTTP response and the SQL output binding.

```
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
namespace AzureSQL.ToDo
{
public static class PostToDo
{
// create a new ToDoItem from body object
// uses output binding to insert new item into ToDo table
[FunctionName("PostToDo")]
public static async Task<OutputType> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "PostFunction")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("PostToDo");
logger.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
ToDoItem toDoItem = JsonConvert.DeserializeObject<ToDoItem>(requestBody);
// generate a new id for the todo item
toDoItem.Id = Guid.NewGuid();
// set Url from env variable ToDoUri
toDoItem.url = Environment.GetEnvironmentVariable("ToDoUri")+"?id="+toDoItem.Id.ToString();
// if completed is not provided, default to false
if (toDoItem.completed == null)
{
toDoItem.completed = false;
}
return new OutputType()
{
ToDoItem = toDoItem,
HttpResponse = req.CreateResponse(System.Net.HttpStatusCode.Created)
}
}
}
public static class OutputType
{
[SqlOutput("dbo.ToDo", connectionStringSetting: "SqlConnectionString")]
public ToDoItem ToDoItem { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
}
```


### HTTP trigger, write to two tables

The following example shows a [C# function](functions-dotnet-class-library) that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings.

```
CREATE TABLE dbo.RequestLog (
Id int identity(1,1) primary key,
RequestTimeStamp datetime2 not null,
ItemCount int not null
)
```


To use an extra output binding, we add a class for `RequestLog`

and modify our `OutputType`

class:

```
using System;
using System.Collections.Generic;
using System.IO;
using System.Threading.Tasks;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
namespace AzureSQL.ToDo
{
public static class PostToDo
{
// create a new ToDoItem from body object
// uses output binding to insert new item into ToDo table
[FunctionName("PostToDo")]
public static async Task<OutputType> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "PostFunction")] HttpRequestData req,
FunctionContext executionContext)
{
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
ToDoItem toDoItem = JsonConvert.DeserializeObject<ToDoItem>(requestBody);
// generate a new id for the todo item
toDoItem.Id = Guid.NewGuid();
// set Url from env variable ToDoUri
toDoItem.url = Environment.GetEnvironmentVariable("ToDoUri")+"?id="+toDoItem.Id.ToString();
// if completed is not provided, default to false
if (toDoItem.completed == null)
{
toDoItem.completed = false;
}
requestLog = new RequestLog();
requestLog.RequestTimeStamp = DateTime.Now;
requestLog.ItemCount = 1;
return new OutputType()
{
ToDoItem = toDoItem,
RequestLog = requestLog,
HttpResponse = req.CreateResponse(System.Net.HttpStatusCode.Created)
}
}
}
public class RequestLog {
public DateTime RequestTimeStamp { get; set; }
public int ItemCount { get; set; }
}
public static class OutputType
{
[SqlOutput("dbo.ToDo", connectionStringSetting: "SqlConnectionString")]
public ToDoItem ToDoItem { get; set; }
[SqlOutput("dbo.RequestLog", connectionStringSetting: "SqlConnectionString")]
public RequestLog RequestLog { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
}
```


More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-java).

This section contains the following examples:

The examples refer to a `ToDoItem`

class (in a separate file `ToDoItem.java`

) and a corresponding database table:

```
package com.function;
import java.util.UUID;
public class ToDoItem {
public UUID Id;
public int order;
public String title;
public String url;
public boolean completed;
public ToDoItem() {
}
public ToDoItem(UUID Id, int order, String title, String url, boolean completed) {
this.Id = Id;
this.order = order;
this.title = title;
this.url = url;
this.completed = completed;
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, write a record to a table

The following example shows a SQL output binding in a Java function that adds a record to a table, using data provided in an HTTP POST request as a JSON body. The function takes another dependency on the [com.google.code.gson](https://github.com/google/gson) library to parse the JSON body.

```
<dependency>
<groupId>com.google.code.gson</groupId>
<artifactId>gson</artifactId>
<version>2.10.1</version>
</dependency>
```


```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.sql.annotation.SQLOutput;
import com.google.gson.Gson;
import java.util.Optional;
public class PostToDo {
@FunctionName("PostToDo")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@SQLOutput(
name = "toDoItem",
commandText = "dbo.ToDo",
connectionStringSetting = "SqlConnectionString")
OutputBinding<ToDoItem> output) {
String json = request.getBody().get();
Gson gson = new Gson();
ToDoItem newToDo = gson.fromJson(json, ToDoItem.class);
newToDo.Id = UUID.randomUUID();
output.setValue(newToDo);
return request.createResponseBuilder(HttpStatus.CREATED).header("Content-Type", "application/json").body(output).build();
}
}
```


### HTTP trigger, write to two tables

The following example shows a SQL output binding in a JavaS function that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings. The function takes another dependency on the [com.google.code.gson](https://github.com/google/gson) library to parse the JSON body.

```
<dependency>
<groupId>com.google.code.gson</groupId>
<artifactId>gson</artifactId>
<version>2.10.1</version>
</dependency>
```


The second table, `dbo.RequestLog`

, corresponds to the following definition:

```
CREATE TABLE dbo.RequestLog (
Id INT IDENTITY(1,1) PRIMARY KEY,
RequestTimeStamp DATETIME2 NOT NULL DEFAULT(GETDATE()),
ItemCount INT NOT NULL
)
```


and Java class in `RequestLog.java`

:

```
package com.function;
import java.util.Date;
public class RequestLog {
public int Id;
public Date RequestTimeStamp;
public int ItemCount;
public RequestLog() {
}
public RequestLog(int Id, Date RequestTimeStamp, int ItemCount) {
this.Id = Id;
this.RequestTimeStamp = RequestTimeStamp;
this.ItemCount = ItemCount;
}
}
```


```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.sql.annotation.SQLOutput;
import com.google.gson.Gson;
import java.util.Optional;
public class PostToDoWithLog {
@FunctionName("PostToDoWithLog")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@SQLOutput(
name = "toDoItem",
commandText = "dbo.ToDo",
connectionStringSetting = "SqlConnectionString")
OutputBinding<ToDoItem> output,
@SQLOutput(
name = "requestLog",
commandText = "dbo.RequestLog",
connectionStringSetting = "SqlConnectionString")
OutputBinding<RequestLog> outputLog,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String json = request.getBody().get();
Gson gson = new Gson();
ToDoItem newToDo = gson.fromJson(json, ToDoItem.class);
newToDo.Id = UUID.randomUUID();
output.setValue(newToDo);
RequestLog newLog = new RequestLog();
newLog.ItemCount = 1;
outputLog.setValue(newLog);
return request.createResponseBuilder(HttpStatus.CREATED).header("Content-Type", "application/json").body(output).build();
}
}
```


More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-js).

This section contains the following examples:

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, write records to a table

The following example shows a SQL output binding that adds records to a table, using data provided in an HTTP POST request as a JSON body.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const sqlOutput = output.sql({
commandText: 'dbo.ToDo',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL output binding function processed a request.');
const body = await request.json();
context.extraOutputs.set(sqlOutput, body);
return { status: 201 };
}
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [sqlOutput],
handler: httpTrigger1,
});
```


```
const { app, output } = require('@azure/functions');
const sqlOutput = output.sql({
commandText: 'dbo.ToDo',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [sqlOutput],
handler: async (request, context) => {
context.log('HTTP trigger and SQL output binding function processed a request.');
const body = await request.json();
context.extraOutputs.set(sqlOutput, body);
return { status: 201 };
},
});
```


### HTTP trigger, write to two tables

The following example shows a SQL output binding that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings.

The second table, `dbo.RequestLog`

, corresponds to the following definition:

```
CREATE TABLE dbo.RequestLog (
Id int identity(1,1) primary key,
RequestTimeStamp datetime2 not null,
ItemCount int not null
)
```


```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const sqlTodoOutput = output.sql({
commandText: 'dbo.ToDo',
connectionStringSetting: 'SqlConnectionString',
});
const sqlRequestLogOutput = output.sql({
commandText: 'dbo.RequestLog',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL output binding function processed a request.');
const newLog = {
RequestTimeStamp: Date.now(),
ItemCount: 1,
};
context.extraOutputs.set(sqlRequestLogOutput, newLog);
const body = await request.json();
context.extraOutputs.set(sqlTodoOutput, body);
return { status: 201 };
}
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [sqlTodoOutput, sqlRequestLogOutput],
handler: httpTrigger1,
});
```


```
const { app, output } = require('@azure/functions');
const sqlTodoOutput = output.sql({
commandText: 'dbo.ToDo',
connectionStringSetting: 'SqlConnectionString',
});
const sqlRequestLogOutput = output.sql({
commandText: 'dbo.RequestLog',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [sqlTodoOutput, sqlRequestLogOutput],
handler: async (request, context) => {
context.log('HTTP trigger and SQL output binding function processed a request.');
const newLog = {
RequestTimeStamp: Date.now(),
ItemCount: 1,
};
context.extraOutputs.set(sqlRequestLogOutput, newLog);
const body = await request.json();
context.extraOutputs.set(sqlTodoOutput, body);
return { status: 201 };
},
});
```


More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-powershell).

This section contains the following examples:

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, write records to a table

The following example shows a SQL output binding in a function.json file and a PowerShell function that adds records to a table, using data provided in an HTTP POST request as a JSON body.

The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItems",
"type": "sql",
"direction": "out",
"commandText": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
```powershell
using namespace System.Net
param($Request)
Write-Host "PowerShell function with SQL Output Binding processed a request."
# Update req_body with the body of the request
$req_body = $Request.Body
# Assign the value we want to pass to the SQL Output binding.
# The -Name value corresponds to the name property in the function.json for the binding
Push-OutputBinding -Name todoItems -Value $req_body
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


### HTTP trigger, write to two tables

The following example shows a SQL output binding in a function.json file and a PowerShell function that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings.

The second table, `dbo.RequestLog`

, corresponds to the following definition:

```
CREATE TABLE dbo.RequestLog (
Id int identity(1,1) primary key,
RequestTimeStamp datetime2 not null,
ItemCount int not null
)
```


The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItems",
"type": "sql",
"direction": "out",
"commandText": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
},
{
"name": "requestLog",
"type": "sql",
"direction": "out",
"commandText": "dbo.RequestLog",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request)
Write-Host "PowerShell function with SQL Output Binding processed a request."
# Update req_body with the body of the request
$req_body = $Request.Body
$new_log = @{
RequestTimeStamp = [DateTime]::Now
ItemCount = 1
}
Push-OutputBinding -Name todoItems -Value $req_body
Push-OutputBinding -Name requestLog -Value $new_log
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


More samples for the Azure SQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-python).

This section contains the following examples:

The examples refer to a database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


### HTTP trigger, write records to a table

The following example shows a SQL output binding in a function.json file and a Python function that adds records to a table, using data provided in an HTTP POST request as a JSON body.

The following is sample python code for the function_app.py file:

```
import json
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="AddToDo")
@app.route(route="addtodo")
@app.sql_output(arg_name="todo",
command_text="[dbo].[ToDo]",
connection_string_setting="SqlConnectionString")
def add_todo(req: func.HttpRequest, todo: func.Out[func.SqlRow]) -> func.HttpResponse:
body = json.loads(req.get_body())
row = func.SqlRow.from_dict(body)
todo.set(row)
return func.HttpResponse(
body=req.get_body(),
status_code=201,
mimetype="application/json"
)
```


### HTTP trigger, write to two tables

The following example shows a SQL output binding in a function.json file and a Python function that adds records to a database in two different tables (`dbo.ToDo`

and `dbo.RequestLog`

), using data provided in an HTTP POST request as a JSON body and multiple output bindings.

The second table, `dbo.RequestLog`

, corresponds to the following definition:

```
CREATE TABLE dbo.RequestLog (
Id int identity(1,1) primary key,
RequestTimeStamp datetime2 not null,
ItemCount int not null
)
```


The following is sample python code for the function_app.py file:

```
from datetime import datetime
import json
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="PostToDo")
@app.route(route="posttodo")
@app.sql_output(arg_name="todoItems",
command_text="[dbo].[ToDo]",
connection_string_setting="SqlConnectionString")
@app.sql_output(arg_name="requestLog",
command_text="[dbo].[RequestLog]",
connection_string_setting="SqlConnectionString")
def add_todo(req: func.HttpRequest, todoItems: func.Out[func.SqlRow], requestLog: func.Out[func.SqlRow]) -> func.HttpResponse:
logging.info('Python HTTP trigger and SQL output binding function processed a request.')
try:
req_body = req.get_json()
rows = func.SqlRowList(map(lambda r: func.SqlRow.from_dict(r), req_body))
except ValueError:
pass
requestLog.set(func.SqlRow({
"RequestTimeStamp": datetime.now().isoformat(),
"ItemCount": 1
}))
if req_body:
todoItems.set(rows)
return func.HttpResponse(
"OK",
status_code=201,
mimetype="application/json"
)
else:
return func.HttpResponse(
"Error accessing request body",
status_code=400
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [SqlAttribute](https://github.com/Azure/azure-functions-sql-extension/blob/main/src/SqlAttribute.cs) attribute to declare the SQL bindings on the function, which has the following properties:

| Attribute property | Description |
|---|---|
CommandText |
Required. The name of the table being written to by the binding. |
ConnectionStringSetting |
Required. The name of an app setting that contains the connection string for the database to which data is being written. This value isn't the actual connection string and must instead resolve to an environment variable. |

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@SQLOutput`

annotation (`com.microsoft.azure.functions.sql.annotation.SQLOutput`

) on parameters whose value would come from Azure SQL. This annotation supports the following elements:

| Element | Description |
|---|---|
commandText |
Required. The name of the table being written to by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database to which data is being written. This value isn't the actual connection string and must instead resolve to an environment variable. |
name |
Required. The unique name of the function binding. |

## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.sql()`

method.

| Property | Description |
|---|---|
commandText |
Required. The name of the table being written to by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database to which data is being written. This value isn't the actual connection string and must instead resolve to an environment variable. Optional keywords in the connection string value are
|

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Required. Must be set to `sql` . |
direction |
Required. Must be set to `out` . |
name |
Required. The name of the variable that represents the entity in function code. |
commandText |
Required. The name of the table being written to by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database to which data is being written. This value isn't the actual connection string and must instead resolve to an environment variable. Optional keywords in the connection string value are
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The `CommandText`

property is the name of the table where the data is to be stored. The connection string setting name corresponds to the application setting that contains the [connection string](/en-us/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-core-5.0&preserve-view=true#Microsoft_Data_SqlClient_SqlConnection_ConnectionString) to the Azure SQL or SQL Server instance.

Important

For optimal security, you should use Microsoft Entra ID with managed identities for connections between Functions and Azure SQL Database. Managed identities make your app more secure by eliminating secrets from your application deployments, such as credentials in the connection strings, server names, and ports being used. You can learn how to use managed identities in this tutorial, [Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).

The output bindings use the T-SQL [MERGE](/en-us/sql/t-sql/statements/merge-transact-sql) statement which requires [SELECT](/en-us/sql/t-sql/statements/merge-transact-sql#permissions) permissions on the target database.

If an exception occurs when a SQL output binding is executed, then the function code stops executing. This behavior may result in an error code being returned, such as an HTTP trigger returning a 500 error code. If the `IAsyncCollector`

is used in a .NET function, then the function code can handle exceptions throw by the call to `FlushAsync()`

.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/update-language-versions -->

# Update language stack versions in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, support for a language stack is limited to [specific versions](functions-versions#languages). As new versions become available, you might want to update your function apps to take advantage of new features. Support in Functions also ends for older versions and typically aligns with community end-of-support timelines. For more information, see the [language runtime support policy](language-support-policy). For supported versions of various languages, see [Languages by runtime version](supported-languages#languages-by-runtime-version).

To help ensure your function apps continue to receive support, follow the instructions in this article to update them to the latest available versions. The way that you update your function app depends on several factors:

- The language you use to develop your function apps. Make sure to select your programming language at the top of this article.
- The operating system on which your function app runs in Azure: Windows or Linux.
- The
[hosting plan](functions-scale).

Note

This article shows you how to update the .NET version of a function app that uses the [isolated worker model](dotnet-isolated-process-guide). If your function app runs on an older version of .NET and uses the [in-process model](functions-dotnet-class-library), consider the following options:

## Prepare your function app

Before you update the stack configuration for your function app in Azure, complete the tasks in the following sections.

### Review dependencies

Before updating language versions, review these potential dependencies:

**Extension bundles**: Verify that your`host.json`

file references a compatible[extension bundle version](functions-bindings-register#extension-bundles). Version 4.x bundles are recommended for most scenarios.

**Binding extensions**: Update any explicit binding extension references to versions compatible with your new language version.**Package dependencies**: Review and update all package dependencies to versions that support your target language version.**Local tools**: Ensure your local development tools, such as Azure Functions Core Tools, SDKs, and IDEs, support the new language version.

### Verify your function app locally

Test and verify your function app code locally on the new target version.

Use these steps to update the project on your local computer:

Ensure that the

[target version of the .NET SDK is installed](https://dotnet.microsoft.com/download/dotnet).If you're targeting a preview version, see

[Functions guidance for preview .NET versions](dotnet-isolated-process-guide#preview-net-versions)to ensure that the version is supported. Using .NET previews might require more steps.Update your references to the latest versions of

[Microsoft.Azure.Functions.Worker](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker/)and[Microsoft.Azure.Functions.Worker.Sdk](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Sdk/).Update your project's target framework to the new version. For C# projects, you must update the

`<TargetFramework>`

element in the*.csproj*file. For more information about your version, see[Target frameworks](/en-us/dotnet/standard/frameworks).Changing your project's target framework might also require changes to parts of your toolchain, outside project code. For example, in Visual Studio Code, you might need to update the

`azureFunctions.deploySubpath`

extension setting in your user settings or your project's*.vscode/settings.json*file. Check for any dependencies on the framework version that exist outside your project code, as part of build steps or a continuous integration and continuous delivery (CI/CD) pipeline.Make any updates to your project code that the new .NET version requires. Check the version's release notes for specific information. You can also use the

[.NET Upgrade Assistant](/en-us/dotnet/core/porting/upgrade-assistant-overview)to help update your code in response to changes across major versions.

After you make those changes, rebuild your project and test it to confirm your function app runs as expected.

### Move to the latest Functions runtime

Make sure your function app runs on the latest version of the Functions runtime (version 4.x). You can determine the runtime version either in the Azure portal or by using the Azure CLI.

Use these steps to determine your Functions runtime version:

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**.Go to the

**Function runtime settings**tab and check the**Runtime version**value. Your function app should run on version 4.x of the Functions runtime (`~4`

).

If you need to update your function app to version 4.x, see [Migrate apps from Azure Functions version 1.x to version 4.x](migrate-version-1-version-4) or [Migrate apps from Azure Functions version 3.x to version 4.x](migrate-version-3-version-4). Follow the instructions in those articles rather than just changing the `FUNCTIONS_EXTENSION_VERSION`

setting.

### Publish function app updates

If you updated your function app to run correctly on the new version, publish the function app updates before you update the stack configuration for your function app.

Tip

To streamline the update process, minimize downtime for your function apps, and provide a potential version for rollback, publish your updated function app to a staging slot. For more information, see [Azure Functions deployment slots](functions-deployment-slots#add-a-slot).

When you publish your updated function app to a staging slot, make sure to follow the slot-specific update instructions in the rest of this article. You later swap the updated staging slot into production.

### Consider using slots

Before updating your function app's language version, create a [deployment slot](functions-deployment-slots#add-a-slot) to use for testing and deployment. This approach minimizes downtime and provides an easy rollback option if issues occur. The examples in this article use a staging slot named `staging`

.

**Flex Consumption plan**: Slots aren't currently supported. You should first verify your updated code in a non-production function app. When deploying to a running app, you might be able to use the rolling update strategy. For more information, see [Site update strategies in Flex Consumption](flex-consumption-site-updates).

Important

The rolling update strategy is currently in preview and isn't recommended for production apps. Review the current [limitations and considerations](flex-consumption-site-updates#rolling-update-strategy-considerations) before enabling this strategy in any production app.

## Update the stack configuration

The way that you update the stack configuration depends on whether your function app runs on Windows or on Linux in Azure.

When you use a [staging slot](functions-deployment-slots), make sure to target your updates to the correct slot.

Use the following steps to update the Java version:

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**. If you have a staging slot, select the specific slot.On the

**General settings**tab, update**Java Version**to the desired version.Select

**Save**. When you're notified about a restart, select**Continue**.

Use the following steps to update the .NET version:

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**. If you have a staging slot, select the specific slot.On the

**General settings**tab, update**.NET Version**to the desired version.Select

**Save**. When you're notified about a restart, select**Continue**.

Use the following steps to update the Node.js version:

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**. If you have a staging slot, select the specific slot.On the

**General settings**tab, update**Node.js Version**to the desired version.Select

**Save**. When you're notified about a restart, select**Continue**. This change updates theapplication setting.`WEBSITE_NODE_DEFAULT_VERSION`


Use the following steps to update the PowerShell version:

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**. If you have a staging slot, select the specific slot.On the

**General settings**tab, update**PowerShell Core Version**to the desired version.Select

**Save**. When you're notified about a restart, select**Continue**.

The portal doesn't support Python apps on Windows. Go to the **Linux** tab instead.

Your function app restarts after you update the version.

Note

During the restart, your function app is unavailable for a brief period, typically 30-60 seconds. If you update a production function app directly (without using a staging slot), plan for this downtime during a maintenance window. The restart terminates any in-flight requests, and new requests fail until the app restarts successfully.

## Verify the update

After your function app restarts, verify that the language version update was successful.

In the

[Azure portal](https://portal.azure.com), locate and select your function app. On the side menu, select**Settings**>**Configuration**.On the

**General settings**tab, verify that the language version displays the new version you selected.Select

**Overview**on the side menu and confirm that the**Status**shows as**Running**.

After verifying the version, also verify that your functions work as expected.

## Swap slots

If you use a staging slot to deploy your code project and update your settings, swap the staging slot into production. For more information, see [Swap slots](functions-deployment-slots#swap-slots).

## Troubleshooting

If you experience issues after updating the language version, use the following guidance to resolve common problems:

### Function app doesn't start

**Symptoms:** The function app status shows as **Stopped** or continuously restarts.

**Solutions:**

Check the application logs in the Azure portal:

- Navigate to your function app and select
**Monitoring**>**Log stream**. - Look for error messages related to runtime or language version mismatches.

- Navigate to your function app and select
Verify that all dependencies are compatible with the new language version:

- For .NET, ensure NuGet packages support the target framework.
- For Python, check that package versions in
`requirements.txt`

are compatible. - For Node.js, verify
`package.json`

dependencies support the new Node version.

Check the

[extension bundle version](functions-bindings-register#extension-bundles)in your`host.json`

file. Older bundles might not support newer language versions.

### Functions fail with runtime errors

**Symptoms:** Individual functions fail when triggered, with errors in the logs.

**Solutions:**

Review breaking changes for your language version:

- See
[Breaking changes in .NET](/en-us/dotnet/core/compatibility/breaking-changes)for your target version.

- Review
[Java release notes](https://www.oracle.com/java/technologies/javase-downloads.html)for migration guidance.

- Check
[Node.js release notes](https://nodejs.org/en/about/previous-releases)for breaking changes.

- See
[What's new in Python](https://docs.python.org/3/whatsnew/)for version-specific changes.

- Review
[PowerShell release notes](/en-us/powershell/scripting/whats-new/overview)for changes.

- See
Update binding extensions to versions compatible with your new language version.

Test functions locally with the new language version before redeploying.


### Extension version conflicts

**Symptoms:** Errors that mention "extension" or "binding" version incompatibilities.

**Solutions:**

Update the

[extension bundle](functions-bindings-register#extension-bundles)version in`host.json`

to version 4.x or later.`{ "version": "2.0", "extensionBundle": { "id": "Microsoft.Azure.Functions.ExtensionBundle", "version": "[4.*, 5.0.0)" } }`

For .NET projects that use explicit extension references, update all

`Microsoft.Azure.WebJobs.Extensions.*`

packages to their latest versions.

### Rolling back the update

If you need to revert to the previous language version:

If you used a staging slot:

- Swap the staging slot back to production.
- Update the staging slot back to the previous version for future attempts.

If you updated production directly:

- Follow the same update steps in this article but specify your previous language version.
- Redeploy your previous code version.

Monitor your function app to ensure it returns to normal operation.


Tip

To avoid issues, always test language version updates in a staging slot before applying them to production. Create a backup of your function app configuration before making changes.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid-trigger -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/deployment-zip-push -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-identity-access-azure-sql-with-managed-identity -->

# Tutorial: Connect a function app to Azure SQL with managed identity and SQL bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides a [managed identity](../active-directory/managed-identities-azure-resources/overview), which is a turn-key solution for securing access to [Azure SQL Database](/en-us/azure/sql-database/) and other Azure services. Managed identities make your app more secure by eliminating secrets from your app, such as credentials in the connection strings. In this tutorial, you'll add managed identity to an Azure Function that utilizes [Azure SQL bindings](functions-bindings-azure-sql). A sample Azure Function project with SQL bindings is available in the [ToDo backend example](/en-us/samples/azure-samples/azure-sql-binding-func-dotnet-todo/todo-backend-dotnet-azure-sql-bindings-azure-functions/).

When you're finished with this tutorial, your Azure Function will connect to Azure SQL database without the need of username and password.

An overview of the steps you'll take:

## Grant database access to Microsoft Entra user

First enable Microsoft Entra authentication to SQL database by assigning a Microsoft Entra user as the Active Directory admin of the server. This user is different from the Microsoft account you used to sign up for your Azure subscription. It must be a user that you created, imported, synced, or invited into Microsoft Entra ID. For more information on allowed Microsoft Entra users, see [Microsoft Entra features and limitations in SQL database](/en-us/azure/azure-sql/database/authentication-aad-overview#azure-ad-features-and-limitations).

Enabling Microsoft Entra authentication can be completed via the Azure portal, PowerShell, or Azure CLI. Directions for Azure CLI are below and information completing this via Azure portal and PowerShell is available in the [Azure SQL documentation on Microsoft Entra authentication](/en-us/azure/azure-sql/database/authentication-aad-configure).

If your Microsoft Entra tenant doesn't have a user yet, create one by following the steps at

[Add or delete users using Microsoft Entra ID](../active-directory/fundamentals/add-users-azure-active-directory).Find the object ID of the Microsoft Entra user using the

and replace`az ad user list`

*<user-principal-name>*. The result is saved to a variable.For Azure CLI 2.37.0 and newer:

`azureaduser=$(az ad user list --filter "userPrincipalName eq '<user-principal-name>'" --query [].id --output tsv)`

For older versions of Azure CLI:

`azureaduser=$(az ad user list --filter "userPrincipalName eq '<user-principal-name>'" --query [].objectId --output tsv)`

Tip

To see the list of all user principal names in Microsoft Entra ID, run

`az ad user list --query [].userPrincipalName`

.Add this Microsoft Entra user as an Active Directory admin using

command in the Cloud Shell. In the following command, replace`az sql server ad-admin create`

*<server-name>*with the server name (without the`.database.windows.net`

suffix).`az sql server ad-admin create --resource-group myResourceGroup --server-name <server-name> --display-name ADMIN --object-id $azureaduser`


For more information on adding an Active Directory admin, see [Provision a Microsoft Entra administrator for your server](/en-us/azure/azure-sql/database/authentication-aad-configure#provision-azure-ad-admin-sql-database)

## Enable system-assigned managed identity on Azure Function

In this step we'll add a system-assigned identity to the Azure Function. In later steps, this identity will be given access to the SQL database.

To enable system-assigned managed identity in the Azure portal:

- Create an Azure Function in the portal as you normally would. Navigate to it in the portal.
- Scroll down to the Settings group in the left navigation.
- Select Identity.
- Within the System assigned tab, switch Status to On. Click Save.


For information on enabling system-assigned managed identity through Azure CLI or PowerShell, check out more information on [using managed identities with Azure Functions](../app-service/overview-managed-identity?tabs=dotnet&toc=/azure/azure-functions/toc.json#add-a-system-assigned-identity).

Tip

For user-assigned managed identity, switch to the User Assigned tab. Click Add and select a Managed Identity. For more information on creating user-assigned managed identity, see the [Manage user-assigned managed identities](../active-directory/managed-identities-azure-resources/how-manage-user-assigned-managed-identities).

## Grant SQL database access to the managed identity

In this step we'll connect to the SQL database with a Microsoft Entra user account and grant the managed identity access to the database.

Open your preferred SQL tool and login with a Microsoft Entra user account (such as the Microsoft Entra user we assigned as administrator). This can be accomplished in Cloud Shell with the SQLCMD command.

`sqlcmd -S <server-name>.database.windows.net -d <db-name> -U <aad-user-name> -P "<aad-password>" -G -l 30`

In the SQL prompt for the database you want, run the following commands to grant permissions to your function. For example,

`CREATE USER [<identity-name>] FROM EXTERNAL PROVIDER; ALTER ROLE db_datareader ADD MEMBER [<identity-name>]; ALTER ROLE db_datawriter ADD MEMBER [<identity-name>]; GO`

*<identity-name>*is the name of the managed identity in Microsoft Entra ID. If the identity is system-assigned, the name is always the same as the name of your Function app.

## Configure Azure Function SQL connection string

In the final step we'll configure the Azure Function SQL connection string to use Microsoft Entra managed identity authentication.

The connection string setting name is identified in our Functions code as the binding attribute "ConnectionStringSetting", as seen in the SQL input binding [attributes and annotations](functions-bindings-azure-sql-input?pivots=programming-language-csharp#attributes).

In the application settings of our Function App the SQL connection string setting should be updated to follow this format:

`Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; Database=testdb`


*testdb* is the name of the database we're connecting to and *demo.database.windows.net* is the name of the server we're connecting to.

Tip

For user-assigned managed identity, use `Server=demo.database.windows.net; Authentication=Active Directory Managed Identity; User Id=ClientIdOfManagedIdentity; Database=testdb`

.

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
