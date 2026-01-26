---
merged_at: 2026-01-26T23:29:57.715054
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-input -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions-opentelemetry-distributed-tracing -->

# Tutorial: Monitor Azure Functions with OpenTelemetry distributed tracing

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article demonstrates OpenTelemetry support in Azure Function, which enables distributed tracing across multiple function calls by using integrated Application Insights and OpenTelemetry support. To help you get started, an Azure Developer CLI (`azd`

) template is used to create your code project as well as the Azure deployment in which to run your app.

In this tutorial, you use the `azd`

tool to:

- Initialize an OpenTelemetry-enabled project from a template.
- Review the code that enables OpenTelemetry integration.
- Run and verify your OpenTelemetry-enabled app locally.
- Create a function app and related resources in Azure.
- Deploy your code project to the function app in Azure.
- Verify distributed tracing in Application Insights.

The required Azure resources created by this template follow current best practices for secure and scalable function app deployments in Azure. The same `azd`

command also deploys your code project to your new function app in Azure.

By default, the Flex Consumption plan follows a *pay-for-what-you-use* billing model, which means completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Important

This article currently supports only C#, Python, and TypeScript. To complete the quickstart, select one of these supported languages at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template that includes OpenTelemetry distributed tracing.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-python-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-typescript-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-dotnet-azd-otel -e flexquickstart-otel`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-otel)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name also appears in the name of the resource group you create in Azure.

## Review the code

The template creates a complete distributed tracing scenario with three functions that work together. Let's review the key OpenTelemetry-related aspects:

### OpenTelemetry configuration

The `src/otel-sample/host.json`

file enables OpenTelemetry for the Functions host:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
"extensions": {
"serviceBus": {
"maxConcurrentCalls": 10
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


The key setting `"telemetryMode": "OpenTelemetry"`

enables distributed tracing across function calls.

The `src/OTelSample/host.json`

file enables OpenTelemetry for the Functions host:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
"logging": {
"OpenTelemetry": {
"logLevel": {
"Host.General": "Warning"
}
}
}
}
```


The key setting `"telemetryMode": "OpenTelemetry"`

enables distributed tracing across function calls.

### Dependencies for OpenTelemetry

The `src/otel-sample/requirements.txt`

file includes the necessary packages for OpenTelemetry integration:

```
azure-functions
azure-monitor-opentelemetry
requests
```


The `azure-monitor-opentelemetry`

package provides the OpenTelemetry integration with Application Insights.

The `src/otel-sample/package.json`

file includes the necessary packages for OpenTelemetry integration:

```
{
"dependencies": {
"@azure/functions": "^4.0.0",
"@azure/functions-opentelemetry-instrumentation": "^0.1.0",
"@azure/monitor-opentelemetry-exporter": "^1.0.0",
"axios": "^1.6.0"
}
}
```


The `@azure/functions-opentelemetry-instrumentation`

and `@azure/monitor-opentelemetry-exporter`

packages provide the OpenTelemetry integration with Application Insights.

The `.csproj`

file includes the necessary packages for OpenTelemetry integration:

```
<PackageReference Include="Azure.Monitor.OpenTelemetry.Exporter" Version="1.4.0" />
<PackageReference Include="Microsoft.Azure.Functions.Worker.OpenTelemetry" Version="1.4.0" />
<PackageReference Include="OpenTelemetry.Instrumentation.Http" Version="1.10.0" />
```


These packages provide the OpenTelemetry integration with Application Insights and HTTP instrumentation for distributed tracing.

### Function implementation

The functions in `src/otel-sample/function_app.py`

demonstrate a distributed tracing flow:

#### First HTTP Function

```
@app.function_name("first_http_function")
@app.route(route="first_http_function", auth_level=func.AuthLevel.ANONYMOUS)
def first_http_function(req: func.HttpRequest) -> func.HttpResponse:
logging.info('Python HTTP trigger function (first) processed a request.')
# Call the second function
base_url = f"{req.url.split('/api/')[0]}/api"
second_function_url = f"{base_url}/second_http_function"
response = requests.get(second_function_url)
second_function_result = response.text
result = {
"message": "Hello from the first function!",
"second_function_response": second_function_result
}
return func.HttpResponse(
json.dumps(result),
status_code=200,
mimetype="application/json"
)
```


#### Second HTTP Function

```
@app.function_name("second_http_function")
@app.route(route="second_http_function", auth_level=func.AuthLevel.ANONYMOUS)
@app.service_bus_queue_output(arg_name="outputsbmsg", queue_name="%ServiceBusQueueName%",
connection="ServiceBusConnection")
def second_http_function(req: func.HttpRequest, outputsbmsg: func.Out[str]) -> func.HttpResponse:
logging.info('Python HTTP trigger function (second) processed a request.')
message = "This is the second function responding."
# Send a message to the Service Bus queue
queue_message = "Message from second HTTP function to trigger ServiceBus queue processing"
outputsbmsg.set(queue_message)
logging.info('Sent message to ServiceBus queue: %s', queue_message)
return func.HttpResponse(
message,
status_code=200
)
```


#### Service Bus Queue Trigger

```
@app.service_bus_queue_trigger(arg_name="azservicebus", queue_name="%ServiceBusQueueName%",
connection="ServiceBusConnection")
def servicebus_queue_trigger(azservicebus: func.ServiceBusMessage):
logging.info('Python ServiceBus Queue trigger start processing a message: %s',
azservicebus.get_body().decode('utf-8'))
time.sleep(5) # Simulate processing work
logging.info('Python ServiceBus Queue trigger end processing a message')
```


The OpenTelemetry configuration is set up in `src/otel-sample/index.ts`

:

```
import { AzureFunctionsInstrumentation } from '@azure/functions-opentelemetry-instrumentation';
import { AzureMonitorTraceExporter, AzureMonitorLogExporter } from '@azure/monitor-opentelemetry-exporter';
import { getNodeAutoInstrumentations, getResourceDetectors } from '@opentelemetry/auto-instrumentations-node';
import { registerInstrumentations } from '@opentelemetry/instrumentation';
import { detectResources } from '@opentelemetry/resources';
import { LoggerProvider, SimpleLogRecordProcessor } from '@opentelemetry/sdk-logs';
import { NodeTracerProvider, SimpleSpanProcessor } from '@opentelemetry/sdk-trace-node';
const resource = detectResources({ detectors: getResourceDetectors() });
const tracerProvider = new NodeTracerProvider({
resource,
spanProcessors: [new SimpleSpanProcessor(new AzureMonitorTraceExporter())]
});
tracerProvider.register();
const loggerProvider = new LoggerProvider({
resource,
processors: [new SimpleLogRecordProcessor(new AzureMonitorLogExporter())],
});
registerInstrumentations({
tracerProvider,
loggerProvider,
instrumentations: [getNodeAutoInstrumentations(), new AzureFunctionsInstrumentation()],
});
```


The functions are defined in the `src/otel-sample/src/functions`

folder:

#### First HTTP Function

```
export async function firstHttpFunction(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log("TypeScript HTTP trigger function (first) processed a request.");
try {
// Call the second function
const baseUrl = request.url.split("/api/")[0];
const secondFunctionUrl = `${baseUrl}/api/second_http_function`;
const response = await axios.get(secondFunctionUrl);
const secondFunctionResult = response.data;
const result = {
message: "Hello from the first function!",
second_function_response: secondFunctionResult,
};
return {
status: 200,
body: JSON.stringify(result),
headers: { "Content-Type": "application/json" },
};
} catch (error) {
return {
status: 500,
body: JSON.stringify({ error: "Failed to process request" }),
};
}
}
```


#### Second HTTP Function

```
export async function secondHttpFunction(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log("TypeScript HTTP trigger function (second) processed a request.");
const message = "This is the second function responding.";
// Send a message to the Service Bus queue
const queueMessage =
"Message from second HTTP function to trigger ServiceBus queue processing";
context.extraOutputs.set(serviceBusOutput, queueMessage);
context.log("Sent message to ServiceBus queue:", queueMessage);
return {
status: 200,
body: message,
};
}
```


#### Service Bus Queue Trigger

```
export async function serviceBusQueueTrigger(
message: unknown,
context: InvocationContext
): Promise<void> {
context.log("TypeScript ServiceBus Queue trigger start processing a message:", message);
// Simulate processing time
await new Promise((resolve) => setTimeout(resolve, 5000));
context.log("TypeScript ServiceBus Queue trigger end processing a message");
}
```


The OpenTelemetry configuration is set up in `src/OTelSample/Program.cs`

:

```
using Azure.Monitor.OpenTelemetry.Exporter;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.OpenTelemetry;
using OpenTelemetry.Trace;
var builder = FunctionsApplication.CreateBuilder(args);
builder.ConfigureFunctionsWebApplication();
builder.Logging.AddOpenTelemetry(logging =>
{
logging.IncludeFormattedMessage = true;
logging.IncludeScopes = true;
});
builder.Services.AddOpenTelemetry()
.WithTracing(tracing =>
{
tracing.AddHttpClientInstrumentation();
});
builder.Services.AddOpenTelemetry().UseAzureMonitorExporter();
builder.Services.AddOpenTelemetry().UseFunctionsWorkerDefaults();
builder.Services.AddHttpClient();
builder.Build().Run();
```


The functions are defined in separate class files:

#### First HTTP Function

```
public class FirstHttpTrigger
{
private readonly ILogger<FirstHttpTrigger> _logger;
private readonly IHttpClientFactory _httpClientFactory;
public FirstHttpTrigger(ILogger<FirstHttpTrigger> logger, IHttpClientFactory httpClientFactory)
{
_logger = logger;
_httpClientFactory = httpClientFactory;
}
[Function("first_http_function")]
public async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestData req)
{
_logger.LogInformation("first_http_function function processed a request.");
var baseUrl = $"{req.Url.AbsoluteUri.Split("/api/")[0]}/api";
var targetUri = $"{baseUrl}/second_http_function";
var client = _httpClientFactory.CreateClient();
var response = await client.GetAsync(targetUri);
var content = await response.Content.ReadAsStringAsync();
return new OkObjectResult($"Called second_http_function, status: {response.StatusCode}, content: {content}");
}
}
```


#### Second HTTP Function

```
public class SecondHttpTrigger
{
private readonly ILogger<SecondHttpTrigger> _logger;
public SecondHttpTrigger(ILogger<SecondHttpTrigger> logger)
{
_logger = logger;
}
[Function("second_http_function")]
public MultiResponse Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestData req)
{
_logger.LogInformation("second_http_function function processed a request.");
return new MultiResponse
{
Messages = new string[] { "Hello" },
HttpResponse = req.CreateResponse(System.Net.HttpStatusCode.OK)
};
}
}
public class MultiResponse
{
[ServiceBusOutput("%ServiceBusQueueName%", Connection = "ServiceBusConnection")]
public string[]? Messages { get; set; }
[HttpResult]
public HttpResponseData? HttpResponse { get; set; }
}
```


#### Service Bus Queue Trigger

```
public class ServiceBusQueueTrigger
{
private readonly ILogger<ServiceBusQueueTrigger> _logger;
public ServiceBusQueueTrigger(ILogger<ServiceBusQueueTrigger> logger)
{
_logger = logger;
}
[Function("servicebus_queue_trigger")]
public async Task Run(
[ServiceBusTrigger("%ServiceBusQueueName%", Connection = "ServiceBusConnection")]
ServiceBusReceivedMessage message,
ServiceBusMessageActions messageActions)
{
_logger.LogInformation("Message ID: {id}", message.MessageId);
_logger.LogInformation("Message Body: {body}", message.Body);
// Complete the message
await messageActions.CompleteMessageAsync(message);
}
}
```


### Distributed tracing flow

This architecture creates a complete distributed tracing scenario, with this behavior:

**First HTTP function**receives an HTTP request and calls the second HTTP function**Second HTTP function**responds and sends a message to Service Bus**Service Bus trigger**processes the message with a delay to simulate processing work

Key aspects of the OpenTelemetry implementation:

**OpenTelemetry integration**: The`host.json`

file enables OpenTelemetry with`"telemetryMode": "OpenTelemetry"`

**Function chaining**: The first function calls the second using HTTP requests, creating correlated traces**Service Bus integration**: The second function outputs to Service Bus, which triggers the third function**Anonymous authentication**: The HTTP functions use`auth_level=func.AuthLevel.ANONYMOUS`

, so no function keys are required

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-python-azd-otel).

**OpenTelemetry integration**: The`index.ts`

file configures OpenTelemetry with Azure Monitor exporters for traces and logs**Function chaining**: The first function calls the second using axios with automatic trace propagation**Service Bus integration**: The second function outputs to Service Bus using output bindings, which triggers the third function**Managed identity**: All Service Bus connections use managed identity instead of connection strings**Processing simulation**: The 5-second delay in the Service Bus trigger simulates message processing work

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-otel).

**OpenTelemetry integration**: The`Program.cs`

file configures OpenTelemetry with Azure Monitor exporter**Function chaining**: The first function calls the second using HttpClient with OpenTelemetry instrumentation**Service Bus integration**: The second function outputs to Service Bus using output bindings, which triggers the third function**Managed identity**: All Service Bus connections use managed identity instead of connection strings**.NET 8 Isolated Worker**: Uses the latest Azure Functions .NET Isolated Worker model for better performance and flexibility

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-otel).

After you verify your functions locally, it's time to publish them to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy this project to a new function app in a Flex Consumption plan in Azure with OpenTelemetry support.

Tip

This project includes a set of Bicep files that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices, including managed identity connections.

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

):- Azure Functions Flex Consumption plan and function app with OpenTelemetry enabled
- Azure Storage (required) and Application Insights (recommended)
- Service Bus namespace and queue for distributed tracing demonstration
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)

Package and deploy your code to the deployment container (equivalent to

`azd deploy`

). The app is then started and runs in the deployed package.

After the command completes successfully, you see links to the resources you created.


## Test distributed tracing

Now you can test the OpenTelemetry distributed tracing functionality by calling your deployed functions and observing the telemetry in Application Insights.

### Invoke the function on Azure

You can invoke your function endpoints in Azure by making HTTP requests to their URLs. Since the HTTP functions in this template are configured with anonymous access, no function keys are required.

In your local terminal or command prompt, run this command to get the function app name and construct the URL:

`APP_NAME=$(azd env get-value AZURE_FUNCTION_NAME) echo "Function URL: https://$APP_NAME.azurewebsites.net/api/first_http_function"`

The

`azd env get-value`

command gets your function app name from the local environment.Test the function in your browser by navigating to the URL:

`https://your-function-app.azurewebsites.net/api/first_http_function`

Replace

`your-function-app`

with your actual function app name from the previous step. This single request creates a distributed trace that flows through all three functions.

### View distributed tracing in Application Insights

After invoking the function, you can observe the complete distributed trace in Application Insights:

Note

It might take a few minutes for telemetry data to appear in Application Insights after invoking your function. If you don't see data immediately, wait a few minutes and refresh the view.

Go to your Application Insights resource in the Azure portal (you can find it in the same resource group as your function app).

Open the

**Application map**to see the distributed trace across all three functions. You should see the flow from the HTTP request through your functions and to Service Bus.Check the

**Transaction search**to find your request and see the complete trace timeline. Search for transactions from your function app.Select a specific transaction to see the end-to-end trace that shows:

- The HTTP request to
`first_http_function`

- The internal HTTP call to
`second_http_function`

- The Service Bus message being sent
- The
`servicebus_queue_trigger`

processing the message from Service Bus

- The HTTP request to
In the trace details, you can see:

**Timing information**: How long each step took**Dependencies**: The connections between functions**Logs**: Application logs correlated with the trace**Performance metrics**: Response times and throughput


This example demonstrates end-to-end distributed tracing across multiple Azure Functions with OpenTelemetry integration, providing complete visibility into your application's behavior and performance.

## Redeploy your code

Run the `azd up`

command as many times as you need to both provision your Azure resources and deploy code updates to your function app.

Note

The latest deployment package always overwrites deployed code files.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that the command uses when creating Azure resources.

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-mcp-tutorial -->

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
