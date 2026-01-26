---
merged_at: 2026-01-26T21:02:36.343127
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cosmosdb-v2-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-input -->

# Azure Cosmos DB input binding for Azure Functions 2.x and higher

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cosmos DB input binding uses the SQL API to retrieve one or more Azure Cosmos DB documents and passes them to the input parameter of the function. The document ID or query parameters can be determined based on the trigger that invokes the function.

For information on setup and configuration details, see the [overview](functions-bindings-cosmosdb-v2).

Note

When the collection is [partitioned](/en-us/azure/cosmos-db/partitioning-overview#logical-partitions), lookup operations must also specify the partition key value.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

Unless otherwise noted, examples in this article target version 3.x of the [Azure Cosmos DB extension](functions-bindings-cosmosdb-v2). For use with extension version 4.x, you need to replace the string `collection`

in property and attribute names with `container`

.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

This section contains examples that require version 3.x of Azure Cosmos DB extension and 5.x of Azure Storage extension. If not already present in your function app, add reference to the following NuGet packages:

The examples refer to a simple `ToDoItem`

type:

```
[Function(nameof(DocByIdFromJSON))]
public void DocByIdFromJSON(
[QueueTrigger("todoqueueforlookup")] ToDoItemLookup toDoItemLookup,
[CosmosDBInput(
databaseName: "ToDoItems",
containerName: "Items",
Connection = "CosmosDBConnection",
Id = "{ToDoItemId}",
PartitionKey = "{ToDoItemPartitionKeyValue}")] ToDoItem toDoItem)
{
_logger.LogInformation($"C# Queue trigger function processed Id={toDoItemLookup?.ToDoItemId} Key={toDoItemLookup?.ToDoItemPartitionKeyValue}");
if (toDoItem == null)
{
_logger.LogInformation($"ToDo item not found");
}
else
{
_logger.LogInformation($"Found ToDo item, Description={toDoItem.Description}");
}
}
```


### Queue trigger, look up ID from JSON

The following example shows a function that retrieves a single document. The function is triggered by a JSON message in the storage queue. The queue trigger parses the JSON into an object of type `ToDoItemLookup`

, which contains the ID and partition key value to retrieve. That ID and partition key value are used to return a `ToDoItem`

document from the specified database and collection.

```
[Function(nameof(DocByIdFromJSON))]
public void DocByIdFromJSON(
[QueueTrigger("todoqueueforlookup")] ToDoItemLookup toDoItemLookup,
[CosmosDBInput(
databaseName: "ToDoItems",
containerName: "Items",
Connection = "CosmosDBConnection",
Id = "{ToDoItemId}",
PartitionKey = "{ToDoItemPartitionKeyValue}")] ToDoItem toDoItem)
{
_logger.LogInformation($"C# Queue trigger function processed Id={toDoItemLookup?.ToDoItemId} Key={toDoItemLookup?.ToDoItemPartitionKeyValue}");
if (toDoItem == null)
{
_logger.LogInformation($"ToDo item not found");
}
else
{
_logger.LogInformation($"Found ToDo item, Description={toDoItem.Description}");
}
}
```


This section contains the following examples:

[HTTP trigger, look up ID from query string - String parameter](#http-trigger-look-up-id-from-query-string---string-parameter-java)[HTTP trigger, look up ID from query string - POJO parameter](#http-trigger-look-up-id-from-query-string---pojo-parameter-java)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-java)[HTTP trigger, look up ID from route data, using SqlQuery](#http-trigger-look-up-id-from-route-data-using-sqlquery-java)[HTTP trigger, get multiple docs from route data, using SqlQuery](#http-trigger-get-multiple-docs-from-route-data-using-sqlquery-java)

The examples refer to a simple `ToDoItem`

type:

```
public class ToDoItem {
private String id;
private String description;
public String getId() {
return id;
}
public String getDescription() {
return description;
}
@Override
public String toString() {
return "ToDoItem={id=" + id + ",description=" + description + "}";
}
}
```


### HTTP trigger, look up ID from query string - String parameter

The following example shows a Java function that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a document from the specified database and collection, in String form.

```
public class DocByIdFromQueryString {
@FunctionName("DocByIdFromQueryString")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBInput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
id = "{Query.id}",
partitionKey = "{Query.partitionKeyValue}",
connectionStringSetting = "Cosmos_DB_Connection_String")
Optional<String> item,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
context.getLogger().info("String from the database is " + (item.isPresent() ? item.get() : null));
// Convert and display
if (!item.isPresent()) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from Cosmos. Alternatively, we can parse the JSON string
// and return an enriched JSON object.
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(item.get())
.build();
}
}
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBInput`

annotation on function parameters whose value would come from Azure Cosmos DB. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

### HTTP trigger, look up ID from query string - POJO parameter

The following example shows a Java function that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value used to retrieve a document from the specified database and collection. The document is then converted to an instance of the `ToDoItem`

POJO previously created, and passed as an argument to the function.

```
public class DocByIdFromQueryStringPojo {
@FunctionName("DocByIdFromQueryStringPojo")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBInput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
id = "{Query.id}",
partitionKey = "{Query.partitionKeyValue}",
connectionStringSetting = "Cosmos_DB_Connection_String")
ToDoItem item,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
context.getLogger().info("Item from the database is " + item);
// Convert and display
if (item == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(item)
.build();
}
}
}
```


### HTTP trigger, look up ID from route data

The following example shows a Java function that retrieves a single document. The function is triggered by an HTTP request that uses a route parameter to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a document from the specified database and collection, returning it as an `Optional<String>`

.

```
public class DocByIdFromRoute {
@FunctionName("DocByIdFromRoute")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "todoitems/{partitionKeyValue}/{id}")
HttpRequestMessage<Optional<String>> request,
@CosmosDBInput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
id = "{id}",
partitionKey = "{partitionKeyValue}",
connectionStringSetting = "Cosmos_DB_Connection_String")
Optional<String> item,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
context.getLogger().info("String from the database is " + (item.isPresent() ? item.get() : null));
// Convert and display
if (!item.isPresent()) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from Cosmos. Alternatively, we can parse the JSON string
// and return an enriched JSON object.
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(item.get())
.build();
}
}
}
```


### HTTP trigger, look up ID from route data, using SqlQuery

The following example shows a Java function that retrieves a single document. The function is triggered by an HTTP request that uses a route parameter to specify the ID to look up. That ID is used to retrieve a document from the specified database and collection, converting the result set to a `ToDoItem[]`

, since many documents may be returned, depending on the query criteria.

Note

If you need to query by just the ID, it is recommended to use a lookup, like the [previous examples](#http-trigger-look-up-id-from-query-string---pojo-parameter-java), as it consumes less [request units](/en-us/azure/cosmos-db/request-units). Point read operations (GET) are [more efficient](/en-us/azure/cosmos-db/optimize-cost-reads-writes) than queries by ID.

```
public class DocByIdFromRouteSqlQuery {
@FunctionName("DocByIdFromRouteSqlQuery")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "todoitems2/{id}")
HttpRequestMessage<Optional<String>> request,
@CosmosDBInput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
sqlQuery = "select * from Items r where r.id = {id}",
connectionStringSetting = "Cosmos_DB_Connection_String")
ToDoItem[] item,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
context.getLogger().info("Items from the database are " + item);
// Convert and display
if (item == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(item)
.build();
}
}
}
```


### HTTP trigger, get multiple docs from route data, using SqlQuery

The following example shows a Java function that retrieves multiple documents. The function is triggered by an HTTP request that uses a route parameter `desc`

to specify the string to search for in the `description`

field. The search term is used to retrieve a collection of documents from the specified database and collection, converting the result set to a `ToDoItem[]`

and passing it as an argument to the function.

```
public class DocsFromRouteSqlQuery {
@FunctionName("DocsFromRouteSqlQuery")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "todoitems3/{desc}")
HttpRequestMessage<Optional<String>> request,
@CosmosDBInput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
sqlQuery = "select * from Items r where contains(r.description, {desc})",
connectionStringSetting = "Cosmos_DB_Connection_String")
ToDoItem[] items,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
context.getLogger().info("Number of items from the database is " + (items == null ? 0 : items.length));
// Convert and display
if (items == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("No documents found.")
.build();
}
else {
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(items)
.build();
}
}
}
```


This section contains the following examples that read a single document by specifying an ID value from various sources:

[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-typescript)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-typescript)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-typescript)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-get-multiple-docs-using-sqlquery-typescript)

### Queue trigger, look up ID from JSON

The following example shows a [TypeScript function](functions-reference-node?tabs=typescript) that reads a single document and updates the document's text value.

```
import { app, input, InvocationContext, output } from '@azure/functions';
const cosmosInput = input.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
id: '{queueTrigger}',
partitionKey: '{queueTrigger}',
connectionStringSetting: 'MyAccount_COSMOSDB',
});
const cosmosOutput = output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: false,
partitionKey: '{queueTrigger}',
connectionStringSetting: 'MyAccount_COSMOSDB',
});
interface MyDocument {
text: string;
}
export async function storageQueueTrigger1(queueItem: unknown, context: InvocationContext): Promise<void> {
const doc = <MyDocument>context.extraInputs.get(cosmosInput);
doc.text = 'This was updated!';
context.extraOutputs.set(cosmosOutput, doc);
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [cosmosInput],
extraOutputs: [cosmosOutput],
handler: storageQueueTrigger1,
});
```


### HTTP trigger, look up ID from query string

The following example shows a [TypeScript function](functions-reference-node?tabs=typescript) that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const cosmosInput = input.cosmosDB({
databaseName: 'ToDoItems',
collectionName: 'Items',
id: '{Query.id}',
partitionKey: '{Query.partitionKeyValue}',
connectionStringSetting: 'CosmosDBConnection',
});
interface ToDoDocument {
description: string;
}
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const toDoItem = <ToDoDocument>context.extraInputs.get(cosmosInput);
if (!toDoItem) {
return {
status: 404,
body: 'ToDo item not found',
};
} else {
return {
body: `Found ToDo item, Description=${toDoItem.description}`,
};
}
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [cosmosInput],
handler: httpTrigger1,
});
```


### HTTP trigger, look up ID from route data

The following example shows a [TypeScript function](functions-reference-node?tabs=typescript) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const cosmosInput = input.cosmosDB({
databaseName: 'ToDoItems',
collectionName: 'Items',
id: '{id}',
partitionKey: '{partitionKeyValue}',
connectionStringSetting: 'CosmosDBConnection',
});
interface ToDoDocument {
description: string;
}
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const toDoItem = <ToDoDocument>context.extraInputs.get(cosmosInput);
if (!toDoItem) {
return {
status: 404,
body: 'ToDo item not found',
};
} else {
return {
body: `Found ToDo item, Description=${toDoItem.description}`,
};
}
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
route: 'todoitems/{partitionKeyValue}/{id}',
extraInputs: [cosmosInput],
handler: httpTrigger1,
});
```


### Queue trigger, get multiple docs, using SqlQuery

The following example shows a [TypeScript function](functions-reference-node?tabs=typescript) that retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.

The queue trigger provides a parameter `departmentId`

. A queue message of `{ "departmentId" : "Finance" }`

would return all records for the finance department.

```
import { app, input, InvocationContext } from '@azure/functions';
const cosmosInput = input.cosmosDB({
databaseName: 'MyDb',
collectionName: 'MyCollection',
sqlQuery: 'SELECT * from c where c.departmentId = {departmentId}',
connectionStringSetting: 'CosmosDBConnection',
});
interface MyDocument {}
export async function storageQueueTrigger1(queueItem: unknown, context: InvocationContext): Promise<void> {
const documents = <MyDocument[]>context.extraInputs.get(cosmosInput);
for (const document of documents) {
// operate on each document
}
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [cosmosInput],
handler: storageQueueTrigger1,
});
```


This section contains the following examples that read a single document by specifying an ID value from various sources:

[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-javascript)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-javascript)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-javascript)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-get-multiple-docs-using-sqlquery-javascript)

### Queue trigger, look up ID from JSON

The following example shows a [JavaScript function](functions-reference-node) that reads a single document and updates the document's text value.

```
const { app, input, output } = require('@azure/functions');
const cosmosInput = input.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
id: '{queueTrigger}',
partitionKey: '{queueTrigger}',
connectionStringSetting: 'MyAccount_COSMOSDB',
});
const cosmosOutput = output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: false,
partitionKey: '{queueTrigger}',
connectionStringSetting: 'MyAccount_COSMOSDB',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [cosmosInput],
extraOutputs: [cosmosOutput],
handler: (queueItem, context) => {
const doc = context.extraInputs.get(cosmosInput);
doc.text = 'This was updated!';
context.extraOutputs.set(cosmosOutput, doc);
},
});
```


### HTTP trigger, look up ID from query string

The following example shows a [JavaScript function](functions-reference-node) that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

```
const { app, input } = require('@azure/functions');
const cosmosInput = input.cosmosDB({
databaseName: 'ToDoItems',
collectionName: 'Items',
id: '{Query.id}',
partitionKey: '{Query.partitionKeyValue}',
connectionStringSetting: 'CosmosDBConnection',
});
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [cosmosInput],
handler: (request, context) => {
const toDoItem = context.extraInputs.get(cosmosInput);
if (!toDoItem) {
return {
status: 404,
body: 'ToDo item not found',
};
} else {
return {
body: `Found ToDo item, Description=${toDoItem.Description}`,
};
}
},
});
```


### HTTP trigger, look up ID from route data

The following example shows a [JavaScript function](functions-reference-node) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

```
const { app, input } = require('@azure/functions');
const cosmosInput = input.cosmosDB({
databaseName: 'ToDoItems',
collectionName: 'Items',
id: '{id}',
partitionKey: '{partitionKeyValue}',
connectionStringSetting: 'CosmosDBConnection',
});
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
route: 'todoitems/{partitionKeyValue}/{id}',
extraInputs: [cosmosInput],
handler: (request, context) => {
const toDoItem = context.extraInputs.get(cosmosInput);
if (!toDoItem) {
return {
status: 404,
body: 'ToDo item not found',
};
} else {
return {
body: `Found ToDo item, Description=${toDoItem.Description}`,
};
}
},
});
```


### Queue trigger, get multiple docs, using SqlQuery

The following example shows a [JavaScript function](functions-reference-node) that retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.

The queue trigger provides a parameter `departmentId`

. A queue message of `{ "departmentId" : "Finance" }`

would return all records for the finance department.

```
const { app, input } = require('@azure/functions');
const cosmosInput = input.cosmosDB({
databaseName: 'MyDb',
collectionName: 'MyCollection',
sqlQuery: 'SELECT * from c where c.departmentId = {departmentId}',
connectionStringSetting: 'CosmosDBConnection',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'outqueue',
connection: 'MyStorageConnectionAppSetting',
extraInputs: [cosmosInput],
handler: (queueItem, context) => {
const documents = context.extraInputs.get(cosmosInput);
for (const document of documents) {
// operate on each document
}
},
});
```


[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-ps)[HTTP trigger, look up ID from query string](#http-trigger-id-query-string-ps)[HTTP trigger, look up ID from route data](#http-trigger-id-route-data-ps)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-multiple-docs-sqlquery-ps)

### Queue trigger, look up ID from JSON

The following example demonstrates how to read and update a single Azure Cosmos DB document. The document's unique identifier is provided through JSON value in a queue message.

The Azure Cosmos DB input binding is listed first in the list of bindings found in the function's configuration file (*function.json*).

```
{
"name": "InputDocumentIn",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"id": "{queueTrigger_payload_property}",
"partitionKey": "{queueTrigger_payload_property}",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in"
},
{
"name": "InputDocumentOut",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"createIfNotExists": false,
"partitionKey": "{queueTrigger_payload_property}",
"connectionStringSetting": "CosmosDBConnection",
"direction": "out"
}
```


The *run.ps1* file has the PowerShell code which reads the incoming document and outputs changes.

```
param($QueueItem, $InputDocumentIn, $TriggerMetadata)
$Document = $InputDocumentIn
$Document.text = 'This was updated!'
Push-OutputBinding -Name InputDocumentOut -Value $Document
```


### HTTP trigger, look up ID from query string

The following example demonstrates how to read and update a single Azure Cosmos DB document from a web API. The document's unique identifier is provided through a querystring parameter from the HTTP request, as defined in the binding's `"Id": "{Query.Id}"`

property.

The Azure Cosmos DB input binding is listed first in the list of bindings found in the function's configuration file (*function.json*).

```
{
"bindings": [
{
"type": "cosmosDB",
"name": "ToDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in",
"Id": "{Query.id}",
"PartitionKey": "{Query.partitionKeyValue}"
},
{
"authLevel": "anonymous",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
]
},
{
"name": "Response",
"type": "http",
"direction": "out"
},
],
"disabled": false
}
```


The *run.ps1* file has the PowerShell code which reads the incoming document and outputs changes.

```
using namespace System.Net
param($Request, $ToDoItem, $TriggerMetadata)
Write-Host 'PowerShell HTTP trigger function processed a request'
if (-not $ToDoItem) {
Write-Host 'ToDo item not found'
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::NotFound
Body = $ToDoItem.Description
})
} else {
Write-Host "Found ToDo item, Description=$($ToDoItem.Description)"
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $ToDoItem.Description
})
}
```


### HTTP trigger, look up ID from route data

The following example demonstrates how to read and update a single Azure Cosmos DB document from a web API. The document's unique identifier is provided through a route parameter. The route parameter is defined in the HTTP request binding's `route`

property and referenced in the Azure Cosmos DB `"Id": "{Id}"`

binding property.

The Azure Cosmos DB input binding is listed first in the list of bindings found in the function's configuration file (*function.json*).

```
{
"bindings": [
{
"type": "cosmosDB",
"name": "ToDoItem",
"databaseName": "ToDoItems",
"collectionName": "Items",
"connectionStringSetting": "CosmosDBConnection",
"direction": "in",
"Id": "{id}",
"PartitionKey": "{partitionKeyValue}"
},
{
"authLevel": "anonymous",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get",
"post"
],
"route": "todoitems/{partitionKeyValue}/{id}"
},
{
"name": "Response",
"type": "http",
"direction": "out"
}
],
"disabled": false
}
```


The *run.ps1* file has the PowerShell code which reads the incoming document and outputs changes.

```
using namespace System.Net
param($Request, $ToDoItem, $TriggerMetadata)
Write-Host 'PowerShell HTTP trigger function processed a request'
if (-not $ToDoItem) {
Write-Host 'ToDo item not found'
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::NotFound
Body = $ToDoItem.Description
})
} else {
Write-Host "Found ToDo item, Description=$($ToDoItem.Description)"
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $ToDoItem.Description
})
}
```


### Queue trigger, get multiple docs, using SqlQuery

The following example demonstrates how to read multiple Azure Cosmos DB documents. The function's configuration file (*function.json*) defines the binding properties, which includes the `sqlQuery`

. The SQL statement provided to the `sqlQuery`

property selects the set of documents provided to the function.

```
{
"name": "Documents",
"type": "cosmosDB",
"direction": "in",
"databaseName": "MyDb",
"collectionName": "MyCollection",
"sqlQuery": "SELECT * from c where c.departmentId = {departmentId}",
"connectionStringSetting": "CosmosDBConnection"
}
```


The *run1.ps1* file has the PowerShell code which reads the incoming documents.

```
param($QueueItem, $Documents, $TriggerMetadata)
foreach ($Document in $Documents) {
# operate on each document
}
```


This section contains the following examples that read a single document by specifying an ID value from various sources:

[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-python)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-python)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-python)[Queue trigger, get multiple docs, using SqlQuery](#queue-trigger-get-multiple-docs-using-sqlquery-python)

The examples depend on whether you use the [v1 or v2 Python programming model](functions-reference-python).

### Using SDK-Type Bindings for Cosmos DB (Preview)

This example uses SDK types to directly access the underlying [ CosmosClient](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_cosmosclient/function_app.py) object provided by the Cosmos DB input binding:

The function loops through all the databases and logs their IDs.

```
import logging
import azure.functions as func
import azurefunctions.extensions.bindings.cosmosdb as cosmos
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.route(route="cosmos")
@app.cosmos_db_input(arg_name="client",
connection="CosmosDBConnection",
database_name=None,
container_name=None)
def get_docs(req: func.HttpRequest, client: cosmos.CosmosClient):
databases = client.list_databases()
for db in databases:
logging.info(f"Found database with ID: {db.get('id')}")
return "ok"
```


For examples of using other SDK types, see the [ ContainerProxy](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_containerproxy/function_app.py) and

[samples. For a step-by-step tutorial on how to include SDK-type bindings in your function app, follow the](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_databaseproxy/function_app.py)

`DatabaseProxy`

[Python SDK Bindings for CosmosDB Sample](https://github.com/Azure-Samples/azure-functions-cosmosdb-sdk-bindings-python).

To learn more, including what other SDK type bindings are supported, see [SDK type bindings](functions-reference-python#sdk-type-bindings).

### Queue trigger, look up ID from JSON

The following example shows an Azure Cosmos DB input binding. The function reads a single document and updates the document's text value.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.queue_trigger(arg_name="msg",
queue_name="outqueue",
connection="AzureWebJobsStorage")
@app.cosmos_db_input(arg_name="documents",
database_name="MyDatabase",
collection_name="MyCollection",
id="{msg.payload_property}",
partition_key="{msg.payload_property}",
connection_string_setting="MyAccount_COSMOSDB")
@app.cosmos_db_output(arg_name="outputDocument",
database_name="MyDatabase",
collection_name="MyCollection",
connection_string_setting="MyAccount_COSMOSDB")
def test_function(msg: func.QueueMessage,
inputDocument: func.DocumentList,
outputDocument: func.Out[func.Document]):
doc = inputDocument[0]
doc["text"] = "This was updated!"
outputDocument.set(doc)
print(f"Updated document.")
```


### HTTP trigger, look up ID from query string

The following example shows a function that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

### HTTP trigger, look up ID from route data

The following example shows a function that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID and partition key value to look up. That ID and partition key value are used to retrieve a `ToDoItem`

document from the specified database and collection.

### Queue trigger, get multiple docs, using SqlQuery

The following example shows an Azure Cosmos DB input binding Python function that uses the binding. The function retrieves multiple documents specified by a SQL query, using a queue trigger to customize the query parameters.

The queue trigger provides a parameter `departmentId`

. A queue message of `{ "departmentId" : "Finance" }`

would return all records for the finance department.

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#azure-cosmos-db-v2-input).

| Attribute property | Description |
|---|---|
Connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being queried. For more information, see
|

**DatabaseName****ContainerName****PartitionKey**[partitioned](/en-us/azure/cosmos-db/partitioning-overview#logical-partitions)containers.**Id**[binding expressions](functions-bindings-expressions-patterns). Don't set both the`Id`

and `SqlQuery`

properties. If you don't set either one, the entire container is retrieved.**SqlQuery**`SELECT * FROM c where c.departmentId = {departmentId}`

. Don't set both the `Id`

and `SqlQuery`

properties. If you don't set either one, the entire container is retrieved.**PreferredLocations**`East US,South Central US,North Europe`

.## Decorators

*Applies only to the Python v2 programming model.*

Python v2 functions are defined using the `cosmos_db_input`

decorator, which supports these properties, depending on the extension version:

| Property | Description |
|---|---|
`arg_name` |
The variable name used in function code that represents the list of documents with changes. |
`database_name` |
The name of the Azure Cosmos DB database with the collection being monitored. |
`container_name` |
The name of the Azure Cosmos DB collection being monitored. |
`connection` |
The connection string of the Azure Cosmos DB being monitored. |
`partition_key` |
The partition key of the Azure Cosmos DB being monitored. |
`id` |
The ID of the document to retrieve. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBInput`

annotation on parameters that read from Azure Cosmos DB. The annotation supports the following properties:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

| function.json property | Description |
|---|---|
type |
Must be set to `cosmosDB` . |
direction |
Must be set to `in` . |
name |
The variable name used in function code that represents the list of documents with changes. |
connection |
The name of an app setting or setting container that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****partitionKey**[partitioned](/en-us/azure/cosmos-db/partitioning-overview#logical-partitions)containers.**id**[binding expressions](functions-bindings-expressions-patterns). Don't set both the`id`

and `sqlQuery`

properties. If you don't set either one, the entire container is retrieved.**sqlQuery**`SELECT * FROM c where c.departmentId = {departmentId}`

. Don't set both the `id`

and `sqlQuery`

properties. If you don't set either one, the entire container is retrieved.**preferredLocations**`East US,South Central US,North Europe`

.See the [Example section](#example) for complete examples.

## Usage

When the function exits successfully, any changes made to the input document are automatically persisted.

The parameter type supported by the Cosmos DB input binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to process a single document, the Cosmos DB input binding can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions attempts to deserialize the JSON data of the document into a plain-old CLR object (POCO) type. |

When you want the function to process multiple documents from a query, the Cosmos DB input binding can bind to the following types:

| Type | Description |
|---|---|
`IEnumerable<T>` where `T` is a JSON serializable type |
An enumeration of entities returned by the query. Each entry represents one document. |
1 |

[Database](/en-us/dotnet/api/microsoft.azure.cosmos.database)1[Container](/en-us/dotnet/api/microsoft.azure.cosmos.container)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.CosmosDB 4.4.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.CosmosDB/4.4.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), the [@CosmosDBInput](/en-us/java/api/com.microsoft.azure.functions.annotation.cosmosdbinput) annotation exposes Azure Cosmos DB data to the function. This annotation can be used with native Java types, POJOs, or nullable values using `Optional<T>`

.

Updates to documents are not made automatically upon function exit. To update documents in a function use an [output binding](functions-bindings-cosmosdb-v2-input). See the [PowerShell example](#example) for more detail.

Data is made available to the function via a `DocumentList`

parameter. Changes made to the document are not automatically persisted.
Functions also support Python SDK type bindings for Azure Cosmos, which lets you work with data using these underlying SDK types:

Important

Support for CosmosDB SDK types for Python is in Preview and is only supported for the Python v2 programming model. For more information, see

[SDK types in Python].

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


---

<!-- DOCUMENTO FUSIONADO: ___functions-networking-faq_functions-bindings-cache_extension-bundles_functions_4d8aa7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-networking-faq_functions-bindings-cache_extension-bundles.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-networking-faq_functions-bindings-cache.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-networking-faq.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-networking-faq -->

# Frequently asked questions about networking in Azure Functions

This article lists frequently asked questions about networking in Azure Functions. For a more comprehensive overview, see [Functions networking options](functions-networking-options).

## How do I set a static IP in Functions?

Deploying a function in an App Service Environment is the primary way to have static inbound and outbound IP addresses for your functions. For details on using an App Service Environment, start with the article [Create and use an internal load balancer with an App Service Environment](../app-service/environment/create-ilb-ase).

You can also use a virtual network NAT gateway to route outbound traffic through a public IP address that you control. To learn more, see [Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway](functions-how-to-use-nat-gateway).

## How do I restrict internet access to my function?

You can restrict internet access in a couple of ways:

[Private endpoints](functions-networking-options#private-endpoints): Restrict inbound traffic to your function app by private link over your virtual network, effectively blocking inbound traffic from the public internet.[IP restrictions](../app-service/app-service-ip-restrictions): Restrict inbound traffic to your function app by IP range.- Under IP restrictions, you are also able to configure
[Service Endpoints](../virtual-network/virtual-network-service-endpoints-overview), which restrict your Function to only accept inbound traffic from a particular virtual network.

- Under IP restrictions, you are also able to configure
- Removal of all HTTP triggers. For some applications, it's enough to simply avoid HTTP triggers and use any other event source to trigger your function.

Keep in mind that the Azure portal editor requires direct access to your running function. Any code changes through the Azure portal will require the device you're using to browse the portal to have its IP added to the approved list. But you can still use anything under the platform features tab with network restrictions in place.

## How do I restrict my function app to a virtual network?

You are able to restrict **inbound** traffic for a function app to a virtual network using [Service Endpoints](functions-networking-options#use-service-endpoints). This configuration still allows the function app to make outbound calls to the internet.

To completely restrict a function such that all traffic flows through a virtual network, you can use a [private endpoints](functions-networking-options#private-endpoints) with outbound virtual network integration or an App Service Environment. To learn more, see [Integrate Azure Functions with an Azure virtual network by using private endpoints](functions-create-vnet).

## How can I access resources in a virtual network from a function app?

You can access resources in a virtual network from a running function by using virtual network integration. For more information, see [Virtual network integration](functions-networking-options#virtual-network-integration).

## How do I access resources protected by service endpoints?

By using virtual network integration you can access service-endpoint-secured resources from a running function. For more information, see [virtual network integration](functions-networking-options#virtual-network-integration).

## How can I trigger a function from a resource in a virtual network?

You are able to allow HTTP triggers to be called from a virtual network using [Service Endpoints](functions-networking-options#use-service-endpoints) or [Private Endpoint connections](functions-networking-options#private-endpoints).

You can also trigger a function from all other resources in a virtual network by deploying your function app to a Premium plan, App Service plan, or App Service Environment. See [non-HTTP virtual network triggers](functions-networking-options#virtual-network-triggers-non-http)
for more information

## How can I deploy my function app in a virtual network?

Deploying to an App Service Environment is the only way to create a function app that's wholly inside a virtual network. For details on using an internal load balancer with an App Service Environment, start with the article [Create and use an internal load balancer with an App Service Environment](../app-service/environment/create-ilb-ase).

For scenarios where you need only one-way access to virtual network resources, or less comprehensive network isolation, see the [Functions networking overview](functions-networking-options).

## Next steps

To learn more about networking and functions:

[Follow the tutorial about getting started with virtual network integration](functions-create-vnet)[Learn more about the networking options in Azure Functions](functions-networking-options)[Learn more about virtual network integration with App Service and Functions](../app-service/overview-vnet-integration)[Learn more about virtual networks in Azure](../virtual-network/virtual-networks-overview)[Enable more networking features and control with App Service Environments](../app-service/environment/intro)


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cache.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache -->

# Overview of Azure functions for Azure Redis

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to use either Azure Managed Redis or Azure Cache for Redis with Azure Functions to create optimized serverless and event-driven architectures.

Azure Functions provides an event-driven programming model where triggers and bindings are key features. With Azure Functions, you can easily build event-driven serverless applications. Azure Redis services (Azure Managed Redis and Azure Cache for Redis) provide a set of building blocks and best practices for building distributed applications, including microservices, state management, pub/sub messaging, and more.

Azure Redis can be used as a trigger for Azure Functions, allowing you to initiate a serverless workflow. This functionality can be highly useful in data architectures like a write-behind cache, or any event-based architectures.

You can integrate Azure Redis and Azure Functions to build functions that react to events from Azure Redis or external systems.

| Action | Direction |
|---|---|
|

[Trigger on Redis lists](functions-bindings-cache-trigger-redislist)[Trigger on Redis streams](functions-bindings-cache-trigger-redisstream)[Read a cached value](functions-bindings-cache-input)[Write a values to cache](functions-bindings-cache-output)## Scope of availability for functions triggers and bindings

| Tier | Azure Cache for Redis (Basic, Standard, Premium, Enterprise, Enterprise Flash) | Azure Managed Redis (Memory Optimized, Basic, Compute Optimized, Flash Optimized) |
|---|---|---|
| Pub/Sub | Yes | Yes |
| Lists | Yes | Yes |
| Streams | Yes | Yes |
| Bindings | Yes | Yes |

Important

Redis triggers are currently only supported for functions running in either a [Elastic Premium plan](functions-premium-plan) or a dedicated [App Service plan](dedicated-plan).

## Install extension

Functions run in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing [this NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Redis).

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Redis
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

## Update packages

Add the [Azure Functions Java Redis Annotations package](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-redis) to your project by updating the `pom.xml`

file to add this dependency:

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-redis</artifactId>
<version>1.0.0</version>
</dependency>
```


## Redis connection string

Azure Redis triggers and bindings have a required property that indicates the application setting or collection name that contains cache connection information. The Redis trigger or binding looks for an environmental variable holding the connection string with the name passed to the `Connection`

parameter.

In local development, the `Connection`

can be defined using the [local.settings.json](/en-us/azure/azure-functions/functions-develop-local#local-settings-file) file. When deployed to Azure, [application settings](/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings) can be used.

When connecting to a cache instance with an Azure function, you can use one of these kinds of connections in your deployments:

A user-assigned managed identity must be associated with your function app, and that identity must also be granted explicit permissions in your cache service. For more information, see [Use Microsoft Entra ID for cache authentication](/en-us/azure/azure-cache-for-redis/cache-azure-active-directory-for-authentication).

These examples show the key name and value of app settings required to connect to each cache service based on the kind of client authentication, assuming that the `Connection`

property in the binding is set to `Redis`

.

```
"Redis__redisHostName": "<cacheName>.<region>.redis.azure.net",
"Redis__principalId": "<principalId>",
"Redis__clientId": "<clientId>"
```


---

<!-- DOCUMENTO FUSIONADO: extension-bundles.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/extension-bundles -->

# Azure Functions extension bundles

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how extension bundles enable your function code to use all of the [triggers and bindings that Azure Functions supports](functions-triggers-bindings). You also learn about the support levels and policies for your apps when you use extension bundles.

This article applies only to Azure Functions developers who use non-.NET languages. To learn how to add binding extensions directly to your C# function apps, see [Register Azure Functions binding extensions](functions-bindings-register).

## Overview

Extension bundles add a predefined set of compatible binding extensions to your function app. A bundle contains all of the binding extensions currently supported by Functions. Extension bundles are versioned. Each version contains a specific set of binding extension versions that are verified to work together.

You should always use the latest bundle version in your app, when possible.

When you create an Azure Functions project from a non-.NET template, extension bundles are already enabled in the app's `host.json`

file.

## Define an extension bundle reference

You define an extension bundle reference in the `host.json`

project file by adding an `extensionBundle`

section, as in this example:

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

## Bundle versions

This table lists all `Microsoft.Azure.Functions.ExtensionBundle`

versions and the current [support state](#extension-bundles-support-policy):

| Bundle version | Version in host.json | Support state* |
|---|---|---|
|

`[4.0.0, 5.0.0)`

`[4.*, 5.0.0)`

[3.x](https://github.com/Azure/azure-functions-extension-bundles/blob/main-v3/src/Microsoft.Azure.Functions.ExtensionBundle/extensions.json)`[3.3.0, 4.0.0)`

[2.x](https://github.com/Azure/azure-functions-extension-bundles/blob/main-v2/src/Microsoft.Azure.Functions.ExtensionBundle/extensions.json)`[2.*, 3.0.0)`

[1.x](https://github.com/Azure/azure-functions-extension-bundles/blob/v1.x/src/Microsoft.Azure.Functions.ExtensionBundle/extensions.json)`[1.*, 2.0.0)`

* Deprecated bundle versions can include deprecated binding extension versions. For optimal supportability and reliability, you should [upgrade to bundle version 4.x](#upgrade-extension-bundles).

By default, extension bundles are defined via version ranges, which guarantees that the latest minor bundle version is used. Select a version link in the table to review the `extensions.json`

file that defines the latest bundle for that major version.

## Considerations for extension bundles

Keep these considerations in mind when you work with extension bundles:

- When possible, you should set a
`version`

range value in`host.json`

from the preceding table, such as`[4.0.0, 5.0.0)`

, instead of defining a custom range. - Use the latest version range to obtain optimal app performance and access to the latest features.
- In the unlikely event that you can't use an extension bundle, you must instead
[explicitly install extensions](functions-bindings-register#explicitly-install-extensions). - When updating the extensions used by a deployed app, Functions downloads new extension versions from the
`cdn.functions.azure.com`

endpoint. For extension updates to succeed, the`cdn.functions.azure.com`

endpoint must be accessible to your function app.

## Upgrade extension bundles

It's important to keep your bundle version up-to-date so that your apps can continue to be eligible for new features, security patches, and performance optimizations.

To upgrade your app to the most recent bundle, edit the host.json file in the root of your app project. Set the value of `extensionBundle.version`

to `[4.0.0,5.0.0)`

, which should look like this in your host.json file:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


Keep these considerations in mind when upgrading the extension bundle version used by your app:

- The contents of the latest 4.x bundle can always be found at
[this release page in the repo](https://github.com/Azure/azure-functions-extension-bundles/releases/latest). - Review the reference documentation for any extensions used by your app to look for any breaking changes between versions. For the list of extension versions included in the default bundle, see the
`extension.json`

project file linked[from this table](#bundle-versions). You can review the[bundle releases page](https://github.com/Azure/azure-functions-extension-bundles/releases)in the bundles repo for specific bundle version tags. - Always verify your app locally after upgrading the bundle version to ensure compatibility with the updated extensions. You can use the
[func start](functions-core-tools-reference#func-start)command in Azure Functions Core Tools or F5 in Visual Studio or Visual Studio Code to run your function app locally. - The way that you trigger extensions to be updated based on changes to the bundle version in the host.json file depends on your app environment:
- Local project: extensions are updated locally when Core Tools starts, either from the
`func start`

command or when debugging in your development tools. - Function app: extensions are updated when you deploy the updated host.json file to your function app in Azure.

- Local project: extensions are updated locally when Core Tools starts, either from the

## Extension bundles support policy

Major version releases of an extension bundle can occur when there are breaking change updates in one of the contained binding extensions. These extension breaking changes require updates to the bundle to remain compatible with the underlying Azure SDKs. Upgrading the bundle ensures your apps continue to receive new features, performance improvements, and full product support.

Note

Because extension bundle updates are driven by updates in the underlying Azure SDKs, the support cycle for extension bundles generally follows the [support policies of the underlying Azure SDKs](https://azure.github.io/azure-sdk/policies_support.html).

Microsoft notifies you when an extension bundle or a binding extension version is deprecated. These notifications might appear in different parts of your Functions experience, such as in host logs, Application Insights tables, or the Azure portal. When you encounter these notifications, you must start the process of planning for and upgrading your function apps to the latest supported extension bundle version.

The support cycle of extension bundles follows these distinct phases:

| Phase | Description |
|---|---|
Preview |
Prerelease versions of specific binding extensions are maintained in a preview extension bundle (`Microsoft.Azure.Functions.ExtensionBundle.Preview` ). You can use this preview extension bundle to take advantage of preview extensions and new behaviors in existing extensions before they reach general availability (GA). For more information, see
|
Active |
The most recent major version of extension bundles is considered to be the active version. We recommend this version for your function apps. |
Deprecation |
The bundle version is superseded by a more recent release and is now deprecated. After a bundle is deprecated, it only receives critical bug fixes and security updates for a limited overlap period. This overlap is typically at least 12 months, which gives you time to plan, test, and upgrade your apps to the latest bundle version. Function apps that continue to use a deprecated bundle can still run on the platform. However, to ensure access to new features, performance improvements, security patches, and full support, you must upgrade your function apps to a supported bundle version. |

You can view the extension bundle versions and their included extensions in the [Azure Functions extension bundles repository](https://github.com/Azure/azure-functions-extension-bundles/releases). You can also view the Azure SDK releases page for an inventory of all Functions extensions. You can find individual .NET packages on [NuGet.org](https://nuget.org/).

## Work with preview extension bundles

Keep these considerations in mind when you choose to use a non-GA extension bundle:

- Preview bundles can include features that are still under development and not yet ready for production use. They're intended for evaluation and testing in nonproduction environments.
- Breaking changes occur between preview versions without prior notice. They can include changes to:
- Trigger and binding definitions.
- Extensions included in the preview.
- Performance characteristics and stability.

- Security updates might require you to upgrade versions.
- You must completely test preview bundles in nonproduction environments and avoid using preview bundles in production. When you must use a preview bundle in production, take these extra precautions:
- Pin your bundle to a specific, well-tested bundle version instead of to a range. Pinning prevents automatic upgrading of your bundle version before you have a chance to verify the update in a nonproduction environment.
- Move your app to using a GA bundle version as soon as the functionality becomes available in a fully supported bundle release.

- To stay informed about bundle updates, including moving from preview to GA, you should:
- Monitor releases of preview bundle versions on the
[release page for extension bundles](https://github.com/Azure/azure-functions-extension-bundles/releases). - Monitor
[extension-specific reference documentation](functions-triggers-bindings). - Review the NuGet package versions of specific preview extensions that you're using.
- Track significant updates or changes in the change logs published on NuGet.org for each preview extension.

- Monitor releases of preview bundle versions on the

## Related content

- To learn more about binding extensions, see
[Register Azure Functions binding extensions](functions-bindings-register).


---

<!-- DOCUMENTO FUSIONADO: functions-mcp-tutorial.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-mcp-tutorial -->

# Tutorial: Host an MCP server on Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to host remote [Model Context Protocol](https://modelcontextprotocol.io/docs/getting-started/intro) (MCP) servers on Azure Functions. You also learn how to use built-in authentication to configure server endpoint authorization and better secure your AI tools.

There are two ways to host a remote MCP server in Azure Functions:

| MCP server option | Description | Best for... |
|---|---|---|
MCP extension server |

[Azure Functions MCP extension](functions-bindings-mcp)to create custom MCP servers, where the extension trigger lets you define your tool endpoints. These servers are supported in all Functions languages and are developed, deployed, and managed as any other function app.[bindings-based programming model](functions-triggers-bindings).**Self-hosted server**Note

The ability to have Azure Functions host MCP servers you create using official MCP SDKs is currently in preview.

This tutorial covers both MCP server options supported by Functions. Select the tab that best fits your scenario.

In this tutorial, you use Visual Studio Code to:

- Create an MCP server project using the MCP extension.
- Run and verify your MCP server locally.
- Create a function app in Azure.
- Deploy your MCP server project.
- Enable built-in authentication.

Important

This article currently supports only C#, Python, and TypeScript. To complete the quickstart, select one of these supported languages at the top of the article.

This article supports version 4 of the Node.js programming model for Azure Functions.

This article supports version 2 of the Python programming model for Azure Functions.

## Prerequisites

[Visual Studio Code](https://code.visualstudio.com/)with these extensions:[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions). This extension requires[Azure Functions Core Tools](functions-run-local)and tries to install it when it's not available.

[Azure CLI](/en-us/cli/azure/install-azure-cli). You can also run Azure CLI commands in[Azure Cloud Shell](../cloud-shell/overview).An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Create your MCP server project

Use Visual Studio Code to locally create an MCP server project in your preferred language.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create New Project...`

.Choose the directory location for your project workspace and choose

**Select**. You should either create a new folder or choose an empty folder for the project workspace. Don't choose a project folder that is already part of a workspace.

Provide the following information at the prompts:

Prompt Selection **Select a project type**Choose `C#`

.**Select a .NET runtime**Choose `.NET 8.0 LTS`

.**Select a template for your project's first function**Choose `MCP Tool trigger`

.**Provide a function name**Type `McpTrigger`

.**Provide a namespace**Type `My.Functions`

.**Authorization level**Choose `FUNCTION`

, which requires access key when connecting to the remote MCP server.**Select how you would like to open your project**Choose `Open in current window`

.

Provide the following information at the prompts:

Prompt Selection **Select a project type**Choose `TypeScript`

.**Select a template for your project's first function**Choose `MCP Tool trigger`

.**Provide a function name**Type `mcpToolTrigger`

.**Authorization level**Choose `FUNCTION`

, which requires access key when connecting to the remote MCP server.**Select how you would like to open your project**Choose `Open in current window`

.

Provide the following information at the prompts:

Prompt Selection **Select a project type**Choose `Python`

.**Select a Python interpreter to create a virtual environment**Choose your preferred Python interpreter. If an option isn't shown, type in the full path to your Python binary. **Select a template for your project's first function**Choose `MCP Tool trigger`

.**Name of the function you want to create**Enter `mcp_trigger`

.**Authorization level**Choose `FUNCTION`

, which requires access key when connecting to the remote MCP server.**Select how you would like to open your project**Choose `Open in current window`

.

Using this information, Visual Studio Code generates a code project for an MCP server trigger. You can view the local project files in the Explorer.

## Start the MCP server locally

Function apps need a storage component to run. Before starting the server, start the local storage emulator:

In

*local.setting.json*, ensure you have`"AzureWebJobsStorage": "UseDevelopmentStorage=true"`

.In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run the server locally.

To start running locally, press

`F5`.

Function apps need a storage component to run. Before starting the server, start the local storage emulator:

In

*local.setting.json*, ensure you have`"AzureWebJobsStorage": "UseDevelopmentStorage=true"`

.In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run the server locally.

To start running locally, press

`F5`.

Function apps need a storage component to run. Before starting the server, start the local storage emulator:

In

*local.setting.json*, ensure you have`"AzureWebJobsStorage": "UseDevelopmentStorage=true"`

.In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run the server locally.

To start running locally, press

`F5`.

## Test the server

Find the

`.vscode`

directory and open`mcp.json`

. The editor should add the server's connection info.Start the server by selecting the

**Start**button above server name.When you connect to the server, you see the number of tools available above the server name.

Open Visual Studio Code Copilot chat in agent mode, then ask a question. For example, "Greet with #your-local-server-name". This question ensures Copilot uses the server to help answer the question.

When Copilot requests to run a tool from the local MCP server, select

**Allow**.Disconnect from the server when you finish testing by selecting

**Stop**, and`Cntrl+C`

to stop running it locally.

Tip

In the Copilot chat window, select the tool icon in the bottom to see the list of servers and tools available for the chat. Ensure the local MCP server is checked when testing.

## Remote MCP server authorization

There are two ways to reduce or prevent unauthorized use of your remote MCP server endpoints:

| Method | Description |
|---|---|
| Built-in server authentication (preview) | Functions includes built-in
|

`Anonymous`

access level to disable access keys in your server when using OAuth-based authentication.Note

This tutorial contains detailed configuration instructions for the built-in server authorization and authentication feature, which might also be referred to as *App Service Authentication* in other articles. You can find an overview of the feature and some usage guidance in the [Configure built-in server authorization (preview)](../app-service/configure-authentication-mcp) article.

## Disable key-based authentication

The built-in server authorization feature is a component separate from Azure Functions. When using server authentication, it's best to first disable key-based authentication by allowing anonymous access.

To disable host-based authentication in your MCP server, set `system.webhookAuthorizationLevel`

to `Anonymous`

in the `host.json`

file:

```
{
"version": "2.0",
"extensions": {
"mcp": {
...
"system": {
"webhookAuthorizationLevel": "Anonymous"
}
}
}
}
```


## Create the function app in Azure

Create a function app in the Flex Consumption plan in Azure that hosts your MCP server.

In the

[Azure portal](https://portal.azure.com), from the menu or the**Home**page, select**Create a resource**.Select

**Get started**and then**Create**under**Function App**.Under

**Select a hosting option**, choose**Flex Consumption**>**Select**.On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription in which you create your new function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. **Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

.**Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access. Unsupported regions aren't displayed. For more information, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Runtime stack**Preferred language Choose one of the supported language runtime stacks. In-portal editing using Visual Studio Code for the Web is currently only available for Node.js, PowerShell, and Python apps. C# class library and Java functions must be [developed locally](functions-develop-local#local-development-environments).**Version**Language version Choose a supported version of your language runtime stack. **Instance size**Default Determines the amount of instance memory allocated for each instance of your app. For more information, see [Instance sizes](flex-consumption-plan#instance-sizes).On the

**Storage**page, accept the default behavior of creating a new[default host storage account](storage-considerations)or choose to use an existing storage account.

On the

**Monitoring**page, make sure that**Enable Application Insights**is selected. Accept the default to create a new Application Insights instance, or else choose to use an existing instance. When you create an Application Insights instance, you're also asked to select a Log Analytics**Workspace**.On the

**Authentication**page, change the**Authentication type**to**Managed identity**for all resources. With this option, a user-assigned managed identity is also created that your app uses to access these Azure resources using Microsoft Entra ID authentication. Managed identities with Microsoft Entra ID provides the highest level of security for connecting to Azure resources.Accept the default options in the remaining tabs and then select

**Review + create**to review the app configuration you chose.When you're satisfied, select

**Create**to provision and deploy the function app and related resources.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

## Deploy the MCP server project

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

Python apps also require you to add this app setting:

`PYTHONPATH=/home/site/wwwroot/.python_packages/lib/site-packages`

.

Now you can deploy the server project:

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

When deployment finishes, you should see a notification in Visual Studio Code about connecting to the server. Select the **Connect** button to have the editor set up server connection information in `mcp.json`

.

## Enable built-in server authorization and authentication

The following instruction shows how to enable the built-in authorization and authentication feature on the server app and configures Microsoft Entra ID as the identity provider. When done, you test by connecting to the server in Visual Studio Code and see that you're prompted to authenticate before connecting.

### Configure authentication on server app

Open the server app on the Azure portal, and select

**Settings**>**Authentication**from the left menu.Select

**Add identity provider**>**Microsoft**as the identity provider.For

**Choose a tenant for your application and its users**, select**Workforce configuration (current tenant)**.Under

**App registration:**use these settings:Setting Selection **App registration type****Create new app registration****Name**Enter a descriptive name for your app **Client secret expiration****Recommended: 180 days****Supported account types****Current tenant - Single tenant**Under

**Additional checks:**, for**Client application requirement**select**Allow requests from specific client applications**, select the pencil icon, add the Visual Studio Code client ID`aebc6443-996d-45c2-90f0-388ff96faa56`

, and select**OK**. Leave the other sections as they are.Under

**App Service authentication settings**use these settings:Setting Selection **Restrict access****Require authentication****Unauthenticated requests****HTTP 401 Unauthorized: recommended for APIs****Token store**Check the box, which allows token refresh Select

**Add**. After settings propagate, you should see the following result:

### Preauthorize Visual Studio Code as client

Select the name of the Entra app next to

**Microsoft**. This action takes you to the**Overview**of the Entra app resource.On the left menu, find

**Manage -> Expose an API**.Under

**Authorized client applications**, select**+Add a client application**.Enter Visual Studio Code's client ID:

`aebc6443-996d-45c2-90f0-388ff96faa56`

.Select the box in front of the scope that looks like

`api://abcd123-efg456-hijk-7890123/user_impersonation`

.Select

**Add application**.

### Configure protected resource metadata (preview)

In the same

**Expose an API**view, find the**Scopes**section, and copy the scope that allows admins and users to consent to the Entra app. This value looks like`api://abcd123-efg456-hijk-7890123/user_impersonation`

.Run the same command as previous to add the setting

`WEBSITE_AUTH_PRM_DEFAULT_WITH_SCOPES`

:`az functionapp config appsettings set --name <function-app-name> --resource-group <resource-group-name> --settings "WEBSITE_AUTH_PRM_DEFAULT_WITH_SCOPES=<scope>"`

Also in the

**Expose an API**view, find the**Application ID URI**(looks like`api://abcd123-efg456-hijk-7890123`

) on the top and save for later step.

## Connect to server

Open `mcp.json`

inside the `.vscode`

directory.

When you select **Connect** in the pop-up after deployment, Visual Studio Code populates the file with server connection information.

If you miss that step, you can also open **Output** (`Ctrl/Cmd+Shift+U`

) to find the in-line connection button at the end of deployment logs.

You can also manually add connection information:

Get the server domain by running the following command:

`az functionapp show --name <FUNCTION_APP_NAME> --resource-group <RESOURCE_GROUP_NAME> --query "defaultHostName" --output tsv`

In Visual Studio Code, open command palette, search for and run the

**MCP: Add Server...**command, and then follow these prompts:Prompt Suggestion Type of server to be added **HTTP**URL of your MCP server `https://<FUNCTION_APP_NAME>.azurewebsites.azurewebsites.net/runtime/webhooks/mcp`

**Server name****remote-mcp-server**Where to install the server **Workspace**Visual Studio Code opens the

`mcp.json`

setting file for you.

Follow the instructions in the next section to connect to server depending on how you configured the authentication.

### With built-in authentication and authorization

Start the remote server by selecting the

**Start**button above the server name.When prompted about authentication with Microsoft, select

**Allow**, then sign in with your email (the one used to log into Azure portal).When you successfully connect to the server, you see the number of tools available above the server name.

Open Visual Studio Code Copilot chat in agent mode, then ask a question. For example,

`Greet with #your-remote-mcp-server-name`

.Stop server when finish testing.


To understand in detail what happens when Visual Studio Code tries to connect to the remote MCP server, see [Server authorization protocol](#server-authorization-protocol).

### With access key

If you don't enable built-in authentication and authorization and instead want to connect to your MCP server by using an access key, the `mcp.json`

should contain Functions access key in the request headers of a server registration.

Visual Studio automatically populates the access key when you start the server.

The `mcp.json`

file should look like the following example:

```
{
"servers": {
"remote-mcp-server": {
"type": "http",
"url": "https://${input:functionapp-domain}/runtime/webhooks/mcp",
"headers": {
"x-functions-key": "${input:functions-key}"
}
}
},
"inputs": [
{
"type": "promptString",
"id": "functions-key",
"description": "Functions App Key",
"password": true
},
{
"type": "promptString",
"id": "functionapp-domain",
"description": "The domain of the function app.",
"password": false
}
]
}
```


If you want to find the access key yourself, go to the Function app on Azure portal. On the left menu, find **Functions -> App keys**. Under the System keys section, find the one named *mcp_extension*.

Tip

To see connection logs, go to the server name, then select **More** > **Show Output**. For more details on the interaction between the client (Visual Studio Code) and the remote MCP server, select the gear icon and pick **Trace**.


## Configure Azure AI Foundry agent to use your tools

You can configure an [agent on Azure AI Foundry](/en-us/azure/ai-foundry/agents/quickstart) to use tools exposed by MCP servers hosted on Azure Functions.

In the Foundry portal, find the agent you want to configure with MCP servers hosted on Functions.

Under

**Tools**, select the**Add**button, then select**+ Add a new tool**.Select the

**Custom**tab, then select**Model Context Protocol (MCP)**and the**Create**button.Fill in the following information:

- Name: Name of the server
- Remote MCP Server endpoint:
- MCP extension server:
`https://<server domain>/runtime/webhooks/mcp`

- Self-hosted server:
`https://<server domain>/mcp`


- MCP extension server:
- Authentication: Choose "Microsoft Entra"
- Type: Choose "Project Managed Identity"
- Audience: This is the Entra App ID URI from
[Configure protected resource metadata](#configure-protected-resource-metadata-preview)

For example:

Select

**Connect**.Test by asking a question that can be answered with the help of a server tool in the chat window.


## Server authorization protocol

In the debug output from Visual Studio Code, you see a series of requests and responses as the MCP client and server interact. When you use the built-in MCP server authorization, you see the following sequence of events:

- The editor sends an initialization request to the MCP server.
- The MCP server responds with an error indicating that authorization is required. The response includes a pointer to the protected resource metadata (PRM) for the application. The built-in authorization feature generates the PRM for the server app.
- The editor fetches the PRM and uses it to identify the authorization server.
- The editor attempts to obtain authorization server metadata (ASM) from a well-known endpoint on the authorization server.
- Microsoft Entra ID doesn't support ASM on the well-known endpoint, so the editor falls back to using the OpenID Connect metadata endpoint to obtain the ASM. It tries to discover this by inserting the well-known endpoint before any other path information.
- The OpenID Connect specifications actually defined the well-known endpoint as being after path information, and that's where Microsoft Entra ID hosts it. So the editor tries again with that format.
- The editor successfully retrieves the ASM. It then uses this information with its own client ID to perform a sign-in. At this point, the editor prompts you to sign in and consent to the application.
- Assuming you successfully sign in and consent, the editor completes the authentication. It repeats the intialization request to the MCP server, this time including an authorization token in the request. This reattempt isn't visible at the Debug output level, but you can see it in the Trace output level.
- The MCP server validates the token and responds with a successful response to the initialization request. The standard MCP flow continues from this point, ultimately resulting in discovery of the MCP tool defined in this sample.

## Troubleshooting

If you run into trouble, ask GitHub Copilot for help. Here are some specific ideas for troubleshooting:

No other ideas at this time. Remember to ask Copilot chat about any errors that occur.

## Next steps

Learn how to [register Azure Functions-hosted MCP servers on Azure API Center](register-mcp-server-api-center).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-other -->

# Quickstart: Create and deploy function code to Azure using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Visual Studio Code to create a function that responds to HTTP requests from a template. Use GitHub Copilot to improve the generated function code, verify code updates locally, and then deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Use Visual Studio Code to create a [custom handler](functions-custom-handlers) function that responds to HTTP requests. After verifying the code locally, you deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Custom handlers can be used to create functions in any language or runtime by running an HTTP server process. This article supports both Go and Rust.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Make sure to select your preferred development language at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17, or 21 (Linux-only).[Apache Maven](https://maven.apache.org), version 3.0 or above.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

## Install or update Core Tools

The Azure Functions extension for Visual Studio Code integrates with Azure Functions Core Tools so that you can run and debug your functions locally in Visual Studio Code using the Azure Functions runtime. Before getting started, it's a good idea to install Core Tools locally or update an existing installation to use the latest version.

In Visual Studio Code, select F1 to open the command palette, and then search for and run the command **Azure Functions: Install or Update Core Tools**.

This command tries to either start a package-based installation of the latest version of Core Tools or update an existing package-based installation. If you don't have npm or Homebrew installed on your local computer, you must instead [manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

## Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project in your preferred language. Later in the article, you update, run, and then publish your function code to Azure.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create New Project...`

.Choose the directory location for your project workspace and choose

**Select**. You should either create a new folder or choose an empty folder for the project workspace. Don't choose a project folder that is already part of a workspace.Provide the following information at the prompts:

Prompt Selection **Select a language**Choose `C#`

.**Select a .NET runtime**Choose `.NET 8.0 LTS`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Provide a namespace**Type `My.Functions`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Java`

.**Select a version of Java**Choose `Java 8`

,`Java 11`

,`Java 17`

or`Java 21`

, the Java version on which your functions run in Azure. Choose a Java version that you've verified locally.**Provide a group ID**Choose `com.function`

.**Provide an artifact ID**Choose `myFunction`

.**Provide a version**Choose `1.0-SNAPSHOT`

.**Provide a package name**Choose `com.function`

.**Provide an app name**Choose `myFunction-12345`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Select the build tool for Java project**Choose `Maven`

.**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `JavaScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `TypeScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Python`

.**Select a Python interpreter to create a virtual environment**Choose your preferred Python interpreter. If an option isn't shown, type in the full path to your Python binary. **Select a template for your project's first function**Choose `HTTP trigger`

.**Name of the function you want to create**Enter `HttpExample`

.**Authorization level**Choose `FUNCTION`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `PowerShell`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `Custom Handler`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Using this information, Visual Studio Code generates a code project for Azure Functions with an HTTP trigger function endpoint. You can view the local project files in the Explorer. To learn more about files that are created, see

[Generated project files](functions-develop-vs-code?tabs=javascript#generated-project-files).

In the local.settings.json file, update the

`AzureWebJobsStorage`

setting as in the following example:`"AzureWebJobsStorage": "UseDevelopmentStorage=true",`

This setting tells the local Functions host to use the storage emulator for the storage connection required by the Python v2 model. When you publish your project to Azure, this setting uses the default storage account instead. If you use an Azure Storage account during local development, set your storage account connection string here.


## Start the emulator

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run your function locally.


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

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure.

To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the Output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to

**WSL Bash**.With Core Tools still running in

**Terminal**, choose the Azure icon in the activity bar. In the**Workspace**area, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the new function and choose**Execute Function Now...**.In

**Enter request body**you see the request message body value of`{ "name": "Azure" }`

. Press Enter to send this request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in

**Terminal**panel.With the

**Terminal**panel focused, press`Ctrl + C`to stop Core Tools and disconnect the debugger.

After you verify that the function runs correctly on your local computer, you can optionally use AI tools, such as GitHub Copilot in Visual Studio Code, to update template-generated function code.

## Use AI to normalize and validate input

This example prompt for Copilot Chat updates the existing function code to retrieve parameters from either the query string or JSON body. It applies formatting or type conversions and returns the parameters as JSON in the response:

```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Make sure that any added packages are compatible with the version of the packages already in the project
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Update the FunctionTest.java file to test the new logic.
```


You can customize your prompt to add specifics as needed. Then run the app again locally and verify that it works as expected after the code changes. This time, use a message body like:

```
{ "name": "devon torres", "email": "torres.devon@contoso.com", "age": "34" }
```


Tip

GitHub Copilot is powered by AI, so surprises and mistakes are possible. If you encounter any errors during execution, paste the error message in the chat window, select **Agent** mode, and ask Copilot to help resolve the error. For more information, see [Copilot FAQs](https://aka.ms/copilot-general-use-faqs).

When running in **Agent** mode, the results of this customization depend on the specific tools available to your agent.

When you're satisfied with your app, use Visual Studio Code to publish the project directly to Azure.

After you verify that the function runs correctly on your local computer, use Visual Studio Code to publish the project directly to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Compile the custom handler for Azure

In this section, you compile your project for deployment to Azure in a function app running Linux. In most cases, you need to recompile your binary and adjust your configuration to match the target platform before publishing it to Azure.

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Run the function in Azure

Press

`F1`to display the command palette, then search for and run the command`Azure Functions:Execute Function Now...`

. If prompted, select your subscription.Select your new function app resource and

`HttpExample`

as your function.In

**Enter request body**type`{ "name": "Contoso", "email": "me@contoso.com", "age": "34" }`

, then press Enter to send this request message to your function.When the function executes in Azure, the response is displayed in the notification area. Expand the notification to review the full response.


## Troubleshooting

Use the following table to resolve the most common issues encountered when using this article.

| Problem | Solution |
|---|---|
| Can't create a local function project? | Make sure you have the
|

[Azure Functions Core Tools installed](functions-run-local?tabs=node).When running on Windows, make sure that the default terminal shell for Visual Studio Code isn't set to WSL Bash.

## Clean up resources

When you continue to the [next step](#next-steps) and add an Azure Storage queue binding to your function, you'll need to keep all your resources in place to build on what you've already done.

Otherwise, you can use the following steps to delete the function app and its related resources to avoid incurring any further costs.

- In Visual Studio Code, select the Azure icon to open the Azure explorer.
- In the Resource Groups section, find your resource group.
- Right-click the resource group and select
**Delete**.

To learn more about Functions costs, see [Estimating Consumption plan costs](functions-consumption-costs).

## Next steps

You used [Visual Studio Code](functions-develop-vs-code) to create a function app with a simple HTTP-triggered function. In the next articles, you expand that function by connecting to either Azure Cosmos DB or Azure Storage. To learn more about connecting to other Azure services, see [Add bindings to an existing function in Azure Functions](add-bindings-existing-function). If you want to learn more about security, see [Securing Azure Functions](security-concepts).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-vs-code-python -->

# Quickstart: Create and deploy function code to Azure using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Visual Studio Code to create a function that responds to HTTP requests from a template. Use GitHub Copilot to improve the generated function code, verify code updates locally, and then deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Use Visual Studio Code to create a [custom handler](functions-custom-handlers) function that responds to HTTP requests. After verifying the code locally, you deploy it to the serverless Flex Consumption hosting plan in Azure Functions.

Custom handlers can be used to create functions in any language or runtime by running an HTTP server process. This article supports both Go and Rust.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Make sure to select your preferred development language at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17, or 21 (Linux-only).[Apache Maven](https://maven.apache.org), version 3.0 or above.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

## Install or update Core Tools

The Azure Functions extension for Visual Studio Code integrates with Azure Functions Core Tools so that you can run and debug your functions locally in Visual Studio Code using the Azure Functions runtime. Before getting started, it's a good idea to install Core Tools locally or update an existing installation to use the latest version.

In Visual Studio Code, select F1 to open the command palette, and then search for and run the command **Azure Functions: Install or Update Core Tools**.

This command tries to either start a package-based installation of the latest version of Core Tools or update an existing package-based installation. If you don't have npm or Homebrew installed on your local computer, you must instead [manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

## Create your local project

In this section, you use Visual Studio Code to create a local Azure Functions project in your preferred language. Later in the article, you update, run, and then publish your function code to Azure.

In Visual Studio Code, press

`F1`to open the command palette. Search for and run the command`Azure Functions: Create New Project...`

.Choose the directory location for your project workspace and choose

**Select**. You should either create a new folder or choose an empty folder for the project workspace. Don't choose a project folder that is already part of a workspace.Provide the following information at the prompts:

Prompt Selection **Select a language**Choose `C#`

.**Select a .NET runtime**Choose `.NET 8.0 LTS`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Provide a namespace**Type `My.Functions`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Java`

.**Select a version of Java**Choose `Java 8`

,`Java 11`

,`Java 17`

or`Java 21`

, the Java version on which your functions run in Azure. Choose a Java version that you've verified locally.**Provide a group ID**Choose `com.function`

.**Provide an artifact ID**Choose `myFunction`

.**Provide a version**Choose `1.0-SNAPSHOT`

.**Provide a package name**Choose `com.function`

.**Provide an app name**Choose `myFunction-12345`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Select the build tool for Java project**Choose `Maven`

.**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `JavaScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `TypeScript`

.**Select a JavaScript programming model**Choose `Model V4`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language**Choose `Python`

.**Select a Python interpreter to create a virtual environment**Choose your preferred Python interpreter. If an option isn't shown, type in the full path to your Python binary. **Select a template for your project's first function**Choose `HTTP trigger`

.**Name of the function you want to create**Enter `HttpExample`

.**Authorization level**Choose `FUNCTION`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `PowerShell`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Prompt Selection **Select a language for your function project**Choose `Custom Handler`

.**Select a template for your project's first function**Choose `HTTP trigger`

.**Provide a function name**Type `HttpExample`

.**Authorization level**Choose `Function`

, which requires an access key to call your function endpoint. For more information, see[Authorization level](functions-bindings-http-webhook-trigger#http-auth).**Select how you would like to open your project**Choose `Open in current window`

.Using this information, Visual Studio Code generates a code project for Azure Functions with an HTTP trigger function endpoint. You can view the local project files in the Explorer. To learn more about files that are created, see

[Generated project files](functions-develop-vs-code?tabs=javascript#generated-project-files).

In the local.settings.json file, update the

`AzureWebJobsStorage`

setting as in the following example:`"AzureWebJobsStorage": "UseDevelopmentStorage=true",`

This setting tells the local Functions host to use the storage emulator for the storage connection required by the Python v2 model. When you publish your project to Azure, this setting uses the default storage account instead. If you use an Azure Storage account during local development, set your storage account connection string here.


## Start the emulator

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azurite: Start`

.Check the bottom bar and verify that Azurite emulation services are running. If so, you can now run your function locally.


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

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure.

To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the Output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to

**WSL Bash**.With Core Tools still running in

**Terminal**, choose the Azure icon in the activity bar. In the**Workspace**area, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the new function and choose**Execute Function Now...**.In

**Enter request body**you see the request message body value of`{ "name": "Azure" }`

. Press Enter to send this request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in

**Terminal**panel.With the

**Terminal**panel focused, press`Ctrl + C`to stop Core Tools and disconnect the debugger.

After you verify that the function runs correctly on your local computer, you can optionally use AI tools, such as GitHub Copilot in Visual Studio Code, to update template-generated function code.

## Use AI to normalize and validate input

This example prompt for Copilot Chat updates the existing function code to retrieve parameters from either the query string or JSON body. It applies formatting or type conversions and returns the parameters as JSON in the response:

```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Make sure that any added packages are compatible with the version of the packages already in the project
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
```


```
Modify the function to accept name, email, and age from the JSON body of the
request. If any of these parameters are missing from the query string, read
them from the JSON body. Return all three parameters in the JSON response,
applying these rules:
Title-case the name
Lowercase the email
Convert age to an integer if possible, otherwise return "not provided"
Use sensible defaults if any parameter is missing
Update the FunctionTest.java file to test the new logic.
```


You can customize your prompt to add specifics as needed. Then run the app again locally and verify that it works as expected after the code changes. This time, use a message body like:

```
{ "name": "devon torres", "email": "torres.devon@contoso.com", "age": "34" }
```


Tip

GitHub Copilot is powered by AI, so surprises and mistakes are possible. If you encounter any errors during execution, paste the error message in the chat window, select **Agent** mode, and ask Copilot to help resolve the error. For more information, see [Copilot FAQs](https://aka.ms/copilot-general-use-faqs).

When running in **Agent** mode, the results of this customization depend on the specific tools available to your agent.

When you're satisfied with your app, use Visual Studio Code to publish the project directly to Azure.

After you verify that the function runs correctly on your local computer, use Visual Studio Code to publish the project directly to Azure.

## Sign in to Azure

Before you can create Azure resources or publish your app, you must sign in to Azure.

If you aren't already signed in, in the

**Activity bar**, select the Azure icon. Then under**Resources**, select**Sign in to Azure**.If you're already signed in and can see your existing subscriptions, go to the next section. If you don't yet have an Azure account, select

**Create an Azure Account**. Students can select**Create an Azure for Students Account**.When you are prompted in the browser, select your Azure account and sign in by using your Azure account credentials. If you create a new account, you can sign in after your account is created.

After you successfully sign in, you can close the new browser window. The subscriptions that belong to your Azure account are displayed in the side bar.


## Create the function app in Azure

In this section, you create a function app in the Flex Consumption plan along with related resources in your Azure subscription. Many of the resource creation decisions are made for you based on default behaviors. For more control over the created resources, you must instead [create your function app with advanced options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).

In Visual Studio Code, select F1 to open the command palette. At the prompt (

`>`

), enter and then select**Azure Functions: Create Function App in Azure**.At the prompts, provide the following information:

Prompt Action **Select subscription**Select the Azure subscription to use. The prompt doesn't appear when you have only one subscription visible under **Resources**.**Enter a new function app name**Enter a globally unique name that's valid in a URL path. The name you enter is validated to make sure that it's unique in Azure Functions. **Select a location for new resources**Select an Azure region. For better performance, select a [region](https://azure.microsoft.com/regions/)near you. Only regions supported by Flex Consumption plans are displayed.**Select a runtime stack**Select the language version you currently run locally. **Select resource authentication type**Select **Managed identity**, which is the most secure option for connecting to the[default host storage account](storage-considerations#storage-account-guidance).In the

**Azure: Activity Log**panel, the Azure extension shows the status of individual resources as they're created in Azure.When the function app is created, the following related resources are created in your Azure subscription. The resources are named based on the name you entered for your function app.

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A function app, which provides the environment for executing your function code. A function app lets you group functions as a logical unit for easier management, deployment, and sharing of resources within the same hosting plan.
- An Azure App Service plan, which defines the underlying host for your function app.
- A standard
[Azure Storage account](../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your function app. - An Application Insights instance that's connected to the function app, and which tracks the use of your functions in the app.
- A user-assigned managed identity that's added to the
[Storage Blob Data Contributor](/en-us/azure/role-based-access-control/built-in-roles/storage#storage-blob-data-contributor)role in the new default host storage account.

A notification is displayed after your function app is created and the deployment package is applied.

Tip

By default, the Azure resources required by your function app are created based on the name you enter for your function app. By default, the resources are created with the function app in the same, new resource group. If you want to customize the names of the associated resources or reuse existing resources,

[publish the project with advanced create options](functions-develop-vs-code?tabs=advanced-options#publish-to-azure).- A

## Compile the custom handler for Azure

In this section, you compile your project for deployment to Azure in a function app running Linux. In most cases, you need to recompile your binary and adjust your configuration to match the target platform before publishing it to Azure.

## Deploy the project to Azure

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Run the function in Azure

Press

`F1`to display the command palette, then search for and run the command`Azure Functions:Execute Function Now...`

. If prompted, select your subscription.Select your new function app resource and

`HttpExample`

as your function.In

**Enter request body**type`{ "name": "Contoso", "email": "me@contoso.com", "age": "34" }`

, then press Enter to send this request message to your function.When the function executes in Azure, the response is displayed in the notification area. Expand the notification to review the full response.


## Troubleshooting

Use the following table to resolve the most common issues encountered when using this article.

| Problem | Solution |
|---|---|
| Can't create a local function project? | Make sure you have the
|

[Azure Functions Core Tools installed](functions-run-local?tabs=node).When running on Windows, make sure that the default terminal shell for Visual Studio Code isn't set to WSL Bash.

## Clean up resources

When you continue to the [next step](#next-steps) and add an Azure Storage queue binding to your function, you'll need to keep all your resources in place to build on what you've already done.

Otherwise, you can use the following steps to delete the function app and its related resources to avoid incurring any further costs.

- In Visual Studio Code, select the Azure icon to open the Azure explorer.
- In the Resource Groups section, find your resource group.
- Right-click the resource group and select
**Delete**.

To learn more about Functions costs, see [Estimating Consumption plan costs](functions-consumption-costs).

## Next steps

You used [Visual Studio Code](functions-develop-vs-code) to create a function app with a simple HTTP-triggered function. In the next articles, you expand that function by connecting to either Azure Cosmos DB or Azure Storage. To learn more about connecting to other Azure services, see [Add bindings to an existing function in Azure Functions](add-bindings-existing-function). If you want to learn more about security, see [Securing Azure Functions](security-concepts).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-service-bus-output -->

# Azure Service Bus output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Azure Service Bus output binding to send queue or topic messages.

For information on setup and configuration details, see the [overview](functions-bindings-service-bus).

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

This code defines and initializes the `ILogger`

:

```
private readonly ILogger<ServiceBusReceivedMessageFunctions> _logger;
public ServiceBusReceivedMessageFunctions(ILogger<ServiceBusReceivedMessageFunctions> logger)
{
_logger = logger;
}
```


This example shows a [C# function](dotnet-isolated-process-guide) that receives a message and writes it to a second queue:

```
[Function(nameof(ServiceBusReceivedMessageFunction))]
[ServiceBusOutput("outputQueue", Connection = "ServiceBusConnection")]
public string ServiceBusReceivedMessageFunction(
[ServiceBusTrigger("queue", Connection = "ServiceBusConnection")] ServiceBusReceivedMessage message)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
_logger.LogInformation("Message Content-Type: {contentType}", message.ContentType);
var outputMessage = $"Output message created at {DateTime.Now}";
return outputMessage;
}
```


This example uses an HTTP trigger with an `OutputType`

object to both send an HTTP response and write the output message.

```
[Function("HttpSendMsg")]
public async Task<OutputType> Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req, FunctionContext context)
{
_logger.LogInformation($"C# HTTP trigger function processed a request for {context.InvocationId}.");
HttpResponseData response = req.CreateResponse(HttpStatusCode.OK);
await response.WriteStringAsync("HTTP response: Message sent");
return new OutputType()
{
OutputEvent = "MyMessage",
HttpResponse = response
};
}
```


This code defines the multiple output type `OutputType`

, which includes the Service Bus output binding definition on `OutputEvent`

:

```
public class OutputType
{
[ServiceBusOutput("TopicOrQueueName", Connection = "ServiceBusConnection")]
public string OutputEvent { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The following example shows a Java function that sends a message to a Service Bus queue `myqueue`

when triggered by an HTTP request.

```
@FunctionName("httpToServiceBusQueue")
@ServiceBusQueueOutput(name = "message", queueName = "myqueue", connection = "AzureServiceBusConnection")
public String pushToQueue(
@HttpTrigger(name = "request", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
final String message,
@HttpOutput(name = "response") final OutputBinding<T> result ) {
result.setValue(message + " has been sent.");
return message;
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@QueueOutput`

annotation on function parameters whose value would be written to a Service Bus queue. The parameter type should be `OutputBinding<T>`

, where `T`

is any native Java type of a plan old Java object (POJO).

Java functions can also write to a Service Bus topic. The following example uses the `@ServiceBusTopicOutput`

annotation to describe the configuration for the output binding.

```
@FunctionName("sbtopicsend")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@ServiceBusTopicOutput(name = "message", topicName = "mytopicname", subscriptionName = "mysubscription", connection = "ServiceBusConnection") OutputBinding<String> message,
final ExecutionContext context) {
String name = request.getBody().orElse("Azure Functions");
message.setValue(name);
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
}
```


The following example shows a timer triggered [TypeScript function](functions-reference-node?tabs=typescript) that sends a queue message every 5 minutes.

```
import { app, InvocationContext, output, Timer } from '@azure/functions';
export async function timerTrigger1(myTimer: Timer, context: InvocationContext): Promise<string> {
const timeStamp = new Date().toISOString();
return `Message created at: ${timeStamp}`;
}
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.serviceBusQueue({
queueName: 'testqueue',
connection: 'MyServiceBusConnection',
}),
handler: timerTrigger1,
});
```


To output multiple messages, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
const message = `Message created at: ${timeStamp}`;
return [`1: ${message}`, `2: ${message}`];
```


The following example shows a timer triggered [JavaScript function](functions-reference-node) that sends a queue message every 5 minutes.

```
const { app, output } = require('@azure/functions');
const serviceBusOutput = output.serviceBusQueue({
queueName: 'testqueue',
connection: 'MyServiceBusConnection',
});
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: serviceBusOutput,
handler: (myTimer, context) => {
const timeStamp = new Date().toISOString();
return `Message created at: ${timeStamp}`;
},
});
```


To output multiple messages, return an array instead of a single object. For example:

```
const timeStamp = new Date().toISOString();
const message = `Message created at: ${timeStamp}`;
return [`1: ${message}`, `2: ${message}`];
```


The following example shows a Service Bus output binding in a *function.json* file and a [PowerShell function](functions-reference-powershell) that uses the binding.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"type": "serviceBus",
"direction": "out",
"connection": "AzureServiceBusConnectionString",
"name": "outputSbMsg",
"queueName": "outqueue",
"topicName": "outtopic"
}
]
}
```


Here's the PowerShell that creates a message as the function's output.

```
param($QueueItem, $TriggerMetadata)
Push-OutputBinding -Name outputSbMsg -Value @{
name = $QueueItem.name
employeeId = $QueueItem.employeeId
address = $QueueItem.address
}
```


The following example demonstrates how to write out to a Service Bus topics and Service Bus queues in Python. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

This example shows how to write out to a Service Bus topic.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.route(route="put_message")
@app.service_bus_topic_output(arg_name="message",
connection="AzureServiceBusConnectionString",
topic_name="outTopic")
def main(req: func.HttpRequest, message: func.Out[str]) -> func.HttpResponse:
input_msg = req.params.get('message')
message.set(input_msg)
return 'OK'
```


This example shows how to write out to a Service Bus queue.

```
import azure.functions as func
app = func.FunctionApp()
@app.route(route="put_message")
@app.service_bus_queue_output(
arg_name="msg",
connection="AzureServiceBusConnectionString",
queue_name="outqueue")
def put_message(req: func.HttpRequest, msg: func.Out[str]):
msg.set(req.get_body().decode('utf-8'))
return 'OK'
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the output binding. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#service-bus-output).

In [C# class libraries](dotnet-isolated-process-guide), use the [ServiceBusOutputAttribute](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.ServiceBus/src/ServiceBusOutputAttribute.cs) to define the queue or topic written to by the output.

The following table explains the properties you can set using the attribute:

| Property | Description |
|---|---|
EntityType |
Sets the entity type as either `Queue` for sending messages to a queue or `Topic` when sending messages to a topic. |
QueueOrTopicName |
Name of the topic or queue to send messages to. Use `EntityType` to set the destination type. |
Connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `service_bus_topic_output`

:

| Property | Description |
|---|---|
`arg_name` |
The name of the variable that represents the queue or topic message in function code. |
`queue_name` |
Name of the queue. Set only if sending queue messages, not for a topic. |
`topic_name` |
Name of the topic. Set only if sending topic messages, not for a queue. |
`connection` |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `ServiceBusQueueOutput`

and `ServiceBusTopicOutput`

annotations are available to write a message as a function output. The parameter decorated with these annotations must be declared as an `OutputBinding<T>`

where `T`

is the type corresponding to the message's type.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `output.serviceBusQueue()`

method.

| Property | Description |
|---|---|
queueName |
Name of the queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

The following table explains the properties that you can set on the `options`

object passed to the `output.serviceBusTopic()`

method.

| Property | Description |
|---|---|
topicName |
Name of the topic. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

The following table explains the binding configuration properties that you set in the *function.json* file and the `ServiceBus`

attribute.

| function.json property | Description |
|---|---|
type |
Must be set to `serviceBus` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that represents the queue or topic message in function code. Set to "$return" to reference the function return value. |
queueName |
Name of the queue. Set only if sending queue messages, not for a topic. |
topicName |
Name of the topic. Set only if sending topic messages, not for a queue. |
connection |
The name of an app setting or setting collection that specifies how to connect to Service Bus. See
|

**accessRights**(v1 only)`manage`

and `listen`

. The default is `manage`

, which indicates that the `connection`

has the **Manage**permission. If you use a connection string that doesn't have the**Manage**permission, set`accessRights`

to "listen". Otherwise, the Functions runtime might fail trying to do operations that require manage rights. In Azure Functions version 2.x and higher, this property isn't available because the latest version of the Service Bus SDK doesn't support manage operations.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

All C# modalities and extension versions support the following output parameter types:

| Type | Description |
|---|---|
|
Use when the message to write is simple text. When the parameter value is null when the function exits, Functions doesn't create a message. |
byte[] |
Use for writing binary data messages. When the parameter value is null when the function exits, Functions doesn't create a message. |
Object |
When a message contains JSON, Functions serializes the object into a JSON message payload. When the parameter value is null when the function exits, Functions creates a message with a null object. |

Messaging-specific parameter types contain extra message metadata and aren't compatible with JSON serialization. As a result, it isn't possible to use `ServiceBusMessage`

with the output binding in the isolated model. The specific types supported by the output binding depend on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write a single message, the Service Bus output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message as a string. Use when the message is simple text. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | An object representing the message. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple messages, the Service Bus output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single message types |
An array containing multiple message. Each entry represents one message. |

For other output scenarios, create and use a [ServiceBusClient](/en-us/dotnet/api/azure.messaging.servicebus.servicebusclient) with other types from [Azure.Messaging.ServiceBus](/en-us/dotnet/api/azure.messaging.servicebus) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

In Azure Functions 1.x, the runtime creates the queue if it doesn't exist and you have set `accessRights`

to `manage`

. In Azure Functions version 2.x and higher, the queue or topic must already exist; if you specify a queue or topic that doesn't exist, the function fails.

Use the [Azure Service Bus SDK](../service-bus-messaging/) rather than the built-in output binding.

Output to the Service Bus is available via the `Push-OutputBinding`

cmdlet where you pass arguments that match the name designated by binding's name parameter in the *function.json* file.

The output function parameter must be defined as `func.Out[str]`

or `func.Out[bytes]`

. Refer to the [output example](#example) for details.
Alternatively, you can use the [Azure Service Bus SDK](../service-bus-messaging/) rather than the built-in output binding.

For a complete example, see [the examples section](#example).

## Connections

The `connection`

property is a reference to environment configuration which specifies how the app should connect to Service Bus. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string, follow the steps shown at [Get the management credentials](../service-bus-messaging/service-bus-dotnet-get-started-with-queues#get-the-connection-string). The connection string must be for a Service Bus namespace, not limited to a specific queue or topic.

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name. For example, if you set `connection`

to "MyServiceBus", the Functions runtime looks for an app setting that is named "AzureWebJobsMyServiceBus". If you leave `connection`

empty, the Functions runtime uses the default Service Bus connection string in the app setting that is named "AzureWebJobsServiceBus".

### Identity-based connections

If you are using [version 5.x or higher of the extension](functions-bindings-service-bus?extensionv5), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the `connection`

property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Fully Qualified Namespace | `<CONNECTION_NAME_PREFIX>__fullyQualifiedNamespace` |
The fully qualified Service Bus namespace. | <service_bus_namespace>.servicebus.windows.net |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `<CONNECTION_NAME_PREFIX>:fullyQualifiedNamespace`

.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your topics and queues at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Service Bus extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
Trigger1 |
|

[Azure Service Bus Data Sender](../role-based-access-control/built-in-roles#azure-service-bus-data-sender)1 For triggering from Service Bus topics, the role assignment needs to have effective scope over the Service Bus subscription resource. If only the topic is included, an error will occur. Some clients, such as the Azure portal, don't expose the Service Bus subscription resource as a scope for role assignment. In such cases, the Azure CLI may be used instead. To learn more, see [Azure built-in roles for Azure Service Bus](../service-bus-messaging/service-bus-managed-service-identity#resource-scope).

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Service Bus |
|

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr -->

# Dapr Extension for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr Extension for Azure Functions is a set of tools and services that allow developers to easily integrate Azure Functions with the [Distributed Application Runtime (Dapr)](https://docs.dapr.io/) platform.

Azure Functions is an event-driven compute service that provides a set of [triggers and bindings](functions-triggers-bindings) to easily connect with other Azure services. Dapr provides a set of building blocks and best practices for building distributed applications, including microservices, state management, pub/sub messaging, and more.

With the integration between Dapr and Functions, you can build functions that react to events from Dapr or external systems.

| Action | Direction | Type |
|---|---|---|
| Trigger on a Dapr input binding | N/A |
|

[daprServiceInvocationTrigger](functions-bindings-dapr-trigger-svc-invoke)[daprTopicTrigger](functions-bindings-dapr-trigger-topic)[daprState](functions-bindings-dapr-input-state)[daprSecret](functions-bindings-dapr-input-secret)[daprState](functions-bindings-dapr-output-state)[daprInvoke](functions-bindings-dapr-output-invoke)[daprPublish](functions-bindings-dapr-output-publish)[daprBinding](functions-bindings-dapr-output)## Install extension

The extension NuGet package you install depends on the C# mode [in-process](functions-dotnet-class-library) or [isolated worker process](dotnet-isolated-process-guide) you're using in your function app:

This extension is available by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Dapr), version 1.0.0.

Using the .NET CLI:

```
dotnet add package Microsoft.Azure.WebJobs.Extensions.Dapr
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

## Dapr enablement

You can configure Dapr using various [arguments and annotations][dapr-args] based on the runtime context. You can configure Dapr for Azure Functions through two channels:

- Infrastructure as Code (IaC) templates, as in Bicep or Azure Resource Manager (ARM) templates
- The Azure portal

When using an IaC template, specify the following arguments in the `properties`

section of the container app resource definition.

```
DaprConfig: {
enabled: true
appId: '${envResourceNamePrefix}-funcapp'
appPort: 3001
httpReadBufferSize: ''
httpMaxRequestSize: ''
logLevel: ''
enableApiLogging: true
}
```


The above Dapr configuration values are considered application-scope changes. When you run a container app in multiple-revision mode, changes to these settings won't create a new revision. Instead, all existing revisions are restarted to ensure they're configured with the most up-to-date values.

When configuring Dapr using the Azure portal, navigate to your function app and select **Dapr** from the left-side menu:


## Dapr ports and listeners

When you're triggering a function from Dapr, the extension exposes port `3001`

automatically to listen to incoming requests from the Dapr sidecar.

Important

Port `3001`

is only exposed and listened to if a Dapr trigger is defined in the function app. When using Dapr, the sidecar waits to receive a response from the defined port before completing instantiation. *Do not* define the `dapr.io/port`

annotation or `--app-port`

unless you have a trigger. Doing so may lock your application from the Dapr sidecar.

If you're only using input and output bindings, port `3001`

doesn't need to be exposed or defined.

By default, when Azure Functions tries to communicate with Dapr, it calls Dapr over the port resolved from the environment variable `DAPR_HTTP_PORT`

. If that variable is null, it defaults to port `3500`

.

You can override the Dapr address used by input and output bindings by setting the `DaprAddress`

property in the `function.json`

for the binding (or the attribute). By default, it uses `http://localhost:{DAPR_HTTP_PORT}`

.

The function app still exposes another port and endpoint for things like HTTP triggers, which locally defaults to `7071`

, but in a container, defaults to `80`

.

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An in-process class library is a compiled C# function runs in the same process as the Functions runtime.

The Dapr Extension supports parameter types according to the table below.

| Binding | Parameter types |
|---|---|
| Dapr trigger |
|

[daprState](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/input-bindings.md#state-input-binding)[daprSecret](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/input-bindings.md#state-input-binding)[daprState](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/output-bindings.md#topic-publish-output-binding)[daprInvoke](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/output-bindings.md#service-invocation-output-binding)[daprPublish](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/output-bindings.md#topic-publish-output-binding)[daprBinding](https://github.com/Azure/azure-functions-dapr-extension/blob/master/docs/output-bindings.md#topic-publish-output-binding)For examples using these types, see [the GitHub repository for the extension](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/dotnet-azurefunction).

## Try out the Dapr Extension for Azure Functions

Learn how to use the Dapr Extension for Azure Functions via the provided samples.

| Samples | Description |
|---|---|
|

`HttpTrigger`

.[Dapr Kafka](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/python-v2-azurefunction#3-dapr-binding)[.NET In-process](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/dotnet-azurefunction)[.NET Isolated](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/dotnet-isolated-azurefunction)## Try out the Dapr Extension for Azure Functions

Learn how to use the Dapr Extension for Azure Functions via the provided samples.

| Samples | Description |
|---|---|
|

## Try out the Dapr Extension for Azure Functions

Learn how to use the Dapr Extension for Azure Functions via the provided samples.

| Samples | Description |
|---|---|
|

`HttpTrigger`

.[Dapr Kafka](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/python-v2-azurefunction#3-dapr-binding)[JavaScript](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/javascript-azurefunction)## Try out the Dapr Extension for Azure Functions

Learn how to use the Dapr Extension for Azure Functions via the provided samples.

| Samples | Description |
|---|---|
|

## Try out the Dapr Extension for Azure Functions

Learn how to use the Dapr Extension for Azure Functions via the provided samples.

| Samples | Description |
|---|---|
|

[Python v1](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/python-azurefunction)[Python v2](https://github.com/Azure/azure-functions-dapr-extension/tree/master/samples/python-v2-azurefunction)## Troubleshooting

This section describes how to troubleshoot issues that can occur when using the Dapr extension for Azure Functions.

### Ensure Dapr is enabled in your environment

If you're using Dapr bindings and triggers in Azure Functions, and Dapr isn't enabled in your environment, you might receive the error message: `Dapr sidecar isn't present. Please see (https://aka.ms/azure-functions-dapr-sidecar-missing) for more information.`

To enable Dapr in your environment:

If your Azure Function is deployed in Azure Container Apps, refer to

[Dapr enablement instructions for the Dapr extension for Azure Functions](functions-bindings-dapr#dapr-enablement).If your Azure Function is deployed in Kubernetes, verify that your

[deployment's YAML configuration](https://github.com/azure/azure-functions-dapr-extension/blob/master/deploy/kubernetes/kubernetes-deployment.md#sample-kubernetes-deployment)has the following annotations:`annotations: ... dapr.io/enabled: "true" dapr.io/app-id: "functionapp" # You should only set app-port if you are using a Dapr trigger in your code. dapr.io/app-port: "<DAPR_APP_PORT>" ...`

If you're running your Azure Function locally, run the following command to ensure you're

[running the function app with Dapr](https://github.com/azure/azure-functions-dapr-extension/tree/master/samples/python-v2-azurefunction#step-2---run-function-app-with-dapr):`dapr run --app-id functionapp --app-port <DAPR_APP_PORT> --components-path <COMPONENTS_PATH> -- func host start`


### Verify app-port value in Dapr configuration

The Dapr extension for Azure Functions starts an HTTP server on port `3001`

by default. You can configure this port using the [ DAPR_APP_PORT environment variable](https://docs.dapr.io/reference/environment/).

If you provide an incorrect app port value when running an Azure Functions app, you might receive the error message: `The Dapr sidecar is configured to listen on port {portInt}, but the app server is running on port {appPort}. This may cause unexpected behavior. For more information, visit [this link](https://aka.ms/azfunc-dapr-app-config-error).`

To resolve this error message:

In your container app's Dapr settings:

If you're using a Dapr trigger in your code, verify that the app port is set to

`3001`

or to the value of the`DAPR_APP_PORT`

environment variable.If you're

*not*using a Dapr trigger in your code, verify that the app port is*not*set. It should be empty.

Verify that you provide the correct app port value in the Dapr configuration.

If you're using Azure Container Apps, specify the app port in Bicep:

`DaprConfig: { ... appPort: <DAPR_APP_PORT> ... }`

If you're using a Kubernetes environment, set the

`dapr.io/app-port`

annotation:`annotations: ... dapr.io/app-port: "<DAPR_APP_PORT>" ...`

If you're developing locally, verify you set

`--app-port`

when running the function app with Dapr:`dapr run --app-id functionapp --app-port <DAPR_APP_PORT> --components-path <COMPONENTS_PATH> -- func host start`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-hubs -->

# Azure Event Hubs trigger and bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with [Azure Event Hubs](../event-hubs/event-hubs-about) bindings for Azure Functions. Azure Functions supports trigger and output bindings for Event Hubs.

| Action | Type |
|---|---|
| Respond to events sent to an event hub event stream. |
|

[Output binding](functions-bindings-event-hubs-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs), version 6.x.

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

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following options:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Azure.Messaging.EventHubs] is in preview.

**Event Hubs trigger**

When you want the function to process a single event, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | When an event contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

If you are migrating from any older versions of the Event Hubs SDKs, note that this version drops support for the legacy

`Body`

type in favor of [EventBody](/en-us/dotnet/api/azure.messaging.eventhubs.eventdata.eventbody).When you want the function to process a batch of events, the Event Hubs trigger can bind to the following types:

| Type | Description |
|---|---|
`string[]` |
An array of events from the batch, as strings. Each entry represents one event. |
`EventData[]` 1 |
An array of events from the batch, as instances of
|

`T[]`

where `T`

is a JSON serializable type11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventHubs 5.5.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventHubs/5.5.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Event Hubs output binding**

When you want the function to write a single event, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. Use when the event is simple text. |
`byte[]` |
The bytes of the event. |
| JSON serializable types | An object representing the event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Hubs output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventHubProducerClient](/en-us/dotnet/api/azure.messaging.eventhubs.producer.eventhubproducerclient) with other types from [Azure.Messaging.EventHubs](/en-us/dotnet/api/azure.messaging.eventhubs) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Types for Azure EventHub are in Preview. Follow the [Python SDK Bindings for EventHub Sample](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python) to get started with SDK Types for Event Hubs in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| EventHub trigger |
|

`EventData`

## host.json settings

The [host.json](functions-host-json#eventhub) file contains settings that control behavior for the Event Hubs trigger. The configuration is different depending on the extension version.

```
{
"version": "2.0",
"extensions": {
"eventHubs": {
"maxEventBatchSize" : 100,
"minEventBatchSize" : 25,
"maxWaitTime" : "00:05:00",
"batchCheckpointFrequency" : 1,
"prefetchCount" : 300,
"transportType" : "amqpWebSockets",
"webProxy" : "https://proxyserver:8080",
"customEndpointAddress" : "amqps://company.gateway.local",
"targetUnprocessedEventThreshold" : 75,
"initialOffsetOptions" : {
"type" : "fromStart",
"enqueuedTimeUtc" : ""
},
"clientRetryOptions":{
"mode" : "exponential",
"tryTimeout" : "00:01:00",
"delay" : "00:00:00.80",
"maximumDelay" : "00:01:00",
"maximumRetries" : 3
}
}
}
}
```


| Property | Default | Description |
|---|---|---|
maxEventBatchSize2 |
100 | The maximum number of events included in a batch for a single invocation. Must be at least 1. |
minEventBatchSize1 |
1 | The minimum number of events desired in a batch. The minimum applies only when the function is receiving multiple events and must be less than `maxEventBatchSize` .The minimum size isn't strictly guaranteed. A partial batch is dispatched when a full batch can't be prepared before the `maxWaitTime` has elapsed. Partial batches are also likely for the first invocation of the function after scaling takes place. |
maxWaitTime1 |
00:01:00 | The maximum interval that the trigger should wait to fill a batch before invoking the function. The wait time is only considered when `minEventBatchSize` is larger than 1 and is otherwise ignored. If less than `minEventBatchSize` events were available before the wait time elapses, the function is invoked with a partial batch. The longest allowed wait time is 10 minutes.NOTE: This interval is not a strict guarantee for the exact timing on which the function is invoked. There is a small margin of error due to timer precision. When scaling takes place, the first invocation with a partial batch may occur more quickly or may take up to twice the configured wait time. |
| batchCheckpointFrequency | 1 | The number of batches to process before creating a checkpoint for the event hub.NOTE: Setting this value above 1 for hosting plans supported by
|
| prefetchCount | 300 | The number of events that is eagerly requested from Event Hubs and held in a local cache to allow reads to avoid waiting on a network operation |
| transportType | amqpTcp | The protocol and transport that is used for communicating with Event Hubs. Available options: `amqpTcp` , `amqpWebSockets` |
| webProxy | null | The proxy to use for communicating with Event Hubs over web sockets. A proxy cannot be used with the `amqpTcp` transport. |
| customEndpointAddress | null | The address to use when establishing a connection to Event Hubs, allowing network requests to be routed through an application gateway or other path needed for the host environment. The fully qualified namespace for the event hub is still needed when a custom endpoint address is used, and it must be specified explicitly or via the connection string. |
targetUnprocessedEventThreshold1 |
null | The desired number of unprocessed events per function instance. The threshold is used in target-based scaling to override the default scaling threshold inferred from the `maxEventBatchSize` option. When set, the total unprocessed event count is divided by this value to determine the number of function instances needed. The instance count is rounded up to a number that creates a balanced partition distribution. |
| initialOffsetOptions/type | fromStart | The location in the event stream to start processing when a checkpoint does not exist in storage. Applies to all partitions. For more information, see the
`fromStart` , `fromEnd` , `fromEnqueuedTime` |

`initialOffsetOptions/type`

is configured as `fromEnqueuedTime`

, this setting is mandatory. Supports time in any format supported by [DateTime.Parse()](/en-us/dotnet/standard/base-types/parsing-datetime), such as`2020-10-26T20:31Z`

. For clarity, you should also specify a timezone. When timezone isn't specified, Functions assumes the local timezone of the machine running the function app, which is UTC when running on Azure.`exponential`

, `fixed`

1 Using `minEventBatchSize`

and `maxWaitTime`

requires [v5.3.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/5.3.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package, or a later version.

2 The default `maxEventBatchSize`

changed in [v6.0.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/6.0.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package. In earlier versions, this was 10.

The `clientRetryOptions`

are used to retry operations between the Functions host and Event Hubs (such as fetching events and sending events). Refer to guidance on [Azure Functions error handling and retries](functions-bindings-error-pages#retries) for information on applying retry policies to individual functions.

For a reference of host.json in Azure Functions 2.x and beyond, see [host.json reference for Azure Functions](functions-host-json).
