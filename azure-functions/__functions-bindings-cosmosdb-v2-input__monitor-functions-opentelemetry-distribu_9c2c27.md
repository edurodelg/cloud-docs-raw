---
merged_at: 2026-01-28T07:43:39.511264
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-container-registry -->

# Create a function app in a local Linux container

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Azure Functions Core tools to create your first function in a Linux container on your local computer, verify the function locally, and then publish the containerized function to a container registry. From a container registry, you can easily deploy your containerized functions to Azure.

For a complete example of deploying containerized functions to Azure, which include the steps in this article, see one of the following articles:

[Create your first containerized Azure Functions on Azure Container Apps](../container-apps/functions-usage)[Create your first containerized Azure Functions](functions-deploy-container)

You can also create a function app in the Azure portal by using an existing containerized function app from a container registry. For more information, see [Azure portal create using containers](functions-how-to-custom-container#azure-portal-create-using-containers).

## Choose your development language

First, you use Azure Functions tools to create your project code as a function app in a Docker container using a language-specific Linux base image. Make sure to select your language of choice at the top of the article.

Core Tools automatically generates a Dockerfile for your project that uses the most up-to-date version of the correct base image for your functions language. You should regularly update your container from the latest base image and redeploy from the updated version of your container. For more information, see [Creating containerized function apps](functions-how-to-custom-container#creating-containerized-function-apps).

## Prerequisites

Before you begin, you must have the following requirements in place:

Install the

[.NET 8.0 SDK](https://dotnet.microsoft.com/download).Install

[Azure Functions Core Tools](functions-run-local#v2)version 4.0.5198, or a later version.

- Install
[Azure Functions Core Tools](functions-run-local#v2)version 4.x.

- Install a version of
[Node.js](https://nodejs.org/)that is[supported by Azure Functions](functions-reference-node#supported-versions).

- Install a version of Python that is
[supported by Azure Functions](functions-reference-python#supported-python-versions).

- Install the
[.NET 6 SDK](https://dotnet.microsoft.com/download).

Install a version of the

[Java Developer Kit](/en-us/azure/developer/java/fundamentals/java-jdk-long-term-support)that is[supported by Azure Functions](functions-reference-java#supported-versions).Install

[Apache Maven](https://maven.apache.org)version 3.0 or above.

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.4 or a later version.

If you don't have an [Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create an [Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

To publish the containerized function app image you create to a container registry, you need a Docker ID and [Docker](https://docs.docker.com/install/) running on your local computer. If you don't have a Docker ID, you can [create a Docker account](https://hub.docker.com/signup).

You also need to complete the [Create a container registry](/en-us/azure/container-registry/container-registry-get-started-portal#create-a-container-registry) section of the Container Registry quickstart to create a registry instance. Make a note of your fully qualified login server name.

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

## Create and test the local functions project

In a terminal or command prompt, run the following command for your chosen language to create a function app project in the current folder:

```
func init --worker-runtime dotnet-isolated --docker
```


```
func init --worker-runtime node --language javascript --docker
```


```
func init --worker-runtime powershell --docker
```


```
func init --worker-runtime python --docker
```


```
func init --worker-runtime node --language typescript --docker
```


In an empty folder, run the following command to generate the Functions project from a [Maven archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html):

```
mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -DarchetypeArtifactId=azure-functions-archetype -DjavaVersion=8 -Ddocker
```


The `-DjavaVersion`

parameter tells the Functions runtime which version of Java to use. Use `-DjavaVersion=11`

if you want your functions to run on Java 11. When you don't specify `-DjavaVersion`

, Maven defaults to Java 8. For more information, see [Java versions](functions-reference-java#java-versions).

Important

The `JAVA_HOME`

environment variable must be set to the install location of the correct version of the JDK to complete this article.

Maven asks you for values needed to finish generating the project on deployment. Follow the prompts and provide the following information:

| Prompt | Value | Description |
|---|---|---|
groupId |
`com.fabrikam` |
A value that uniquely identifies your project across all projects, following the
|

**artifactId**`fabrikam-functions`

**version**`1.0-SNAPSHOT`

**package**`com.fabrikam.functions`

Type `Y`

or press Enter to confirm.

Maven creates the project files in a new folder named *artifactId*, which in this example is `fabrikam-functions`

.

The `--docker`

option generates a *Dockerfile* for the project, which defines a suitable container for use with Azure Functions and the selected runtime.

Navigate into the project folder:

```
cd fabrikam-functions
```


Use the following command to add a function to your project, where the `--name`

argument is the unique name of your function and the `--template`

argument specifies the function's trigger. `func new`

creates a C# code file in your project.

```
func new --name HttpExample --template "HTTP trigger"
```


Use the following command to add a function to your project, where the `--name`

argument is the unique name of your function and the `--template`

argument specifies the function's trigger. `func new`

creates a subfolder matching the function name that contains a configuration file named *function.json*.

```
func new --name HttpExample --template "HTTP trigger"
```


To test the function locally, start the local Azure Functions runtime host in the root of the project folder.

```
func start
```


```
func start
```


```
npm install
npm start
```


```
mvn clean package
mvn azure-functions:run
```


After you see the `HttpExample`

endpoint written to the output, navigate to that endpoint. You should see a welcome message in the response output.

After you see the `HttpExample`

endpoint written to the output, navigate to `http://localhost:7071/api/HttpExample?name=Functions`

. The browser must display a "hello" message that echoes back `Functions`

, the value supplied to the `name`

query parameter.

Press **Ctrl**+**C** (**Command**+**C** on macOS) to stop the host.

## Build the container image and verify locally

(Optional) Examine the *Dockerfile* in the root of the project folder. The *Dockerfile* describes the required environment to run the function app on Linux. The complete list of supported base images for Azure Functions can be found in the [Azure Functions base image page](https://hub.docker.com/_/microsoft-azure-functions-base).

In the root project folder, run the [docker build](https://docs.docker.com/engine/reference/commandline/build/) command, provide a name as `azurefunctionsimage`

, and tag as `v1.0.0`

. Replace `<DOCKER_ID>`

with your Docker Hub account ID. This command builds the Docker image for the container.

```
docker build --tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 .
```


When the command completes, you can run the new container locally.

To verify the build, run the image in a local container using the [docker run](https://docs.docker.com/engine/reference/commandline/run/) command, replace `<DOCKER_ID>`

again with your Docker Hub account ID, and add the ports argument as `-p 8080:80`

:

```
docker run -p 8080:80 -it <DOCKER_ID>/azurefunctionsimage:v1.0.0
```


After the image starts in the local container, browse to `http://localhost:8080/api/HttpExample`

, which must display the same greeting message as before. Because the HTTP triggered function you created uses anonymous authorization, you can call the function running in the container without having to obtain an access key. For more information, see [authorization keys](functions-bindings-http-webhook-trigger#authorization-keys).

After the image starts in the local container, browse to `http://localhost:8080/api/HttpExample?name=Functions`

, which must display the same "hello" message as before. Because the HTTP triggered function you created uses anonymous authorization, you can call the function running in the container without having to obtain an access key. For more information, see [authorization keys](functions-bindings-http-webhook-trigger#authorization-keys).

After verifying the function app in the container, press **Ctrl**+**C** (**Command**+**C** on macOS) to stop execution.

## Publish the container image to a registry

To make your container image available for deployment to a hosting environment, you must push it to a container registry. As a security best practice, you should use an Azure Container Registry instance and enforce managed identity-based connections. Docker Hub requires you to authenticate using shared secrets, which make your deployments more vulnerable.

Azure Container Registry is a private registry service for building, storing, and managing container images and related artifacts. You should use a private registry service for publishing your containers to Azure services.

Use this command to sign in to your registry instance using your current Azure credentials:

`az acr login --name <REGISTRY_NAME>`

In the previous command, replace

`<REGISTRY_NAME>`

with the name of your Container Registry instance.Use this command to tag your image with the fully qualified name of your registry login server:

`docker tag <DOCKER_ID>/azurefunctionsimage:v1.0.0 <LOGIN_SERVER>/azurefunctionsimage:v1.0.0`

Replace

`<LOGIN_SERVER>`

with the fully qualified name of your registry login server and`<DOCKER_ID>`

with your Docker ID.Use this command to push the container to your registry instance:

`docker push <LOGIN_SERVER>/azurefunctionsimage:v1.0.0`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/machine-learning-pytorch -->

# Tutorial: Deploy a pre-trained image classification model to Azure Functions with PyTorch

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Python, PyTorch, and Azure Functions to load a pre-trained model for classifying an image based on its contents. Because you do all work locally and create no Azure resources in the cloud, there's no cost to complete this tutorial.

- Initialize a local environment for developing Azure Functions in Python.
- Import a pre-trained PyTorch machine learning model into a function app.
- Build a serverless HTTP API for classifying an image as one of 1000 ImageNet
[classes](https://gist.github.com/yrevar/942d3a0ac09ec9e5eb3a). - Consume the API from a web app.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). [Python 3.7.4 or above](https://www.python.org/downloads/release/python-374/). (Python 3.8.x and Python 3.6.x are also verified with Azure Functions.)- The
[Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools) - A code editor such as
[Visual Studio Code](https://code.visualstudio.com/)

### Prerequisite check

- In a terminal or command window, run
`func --version`

to check that the Azure Functions Core Tools are version 2.7.1846 or later. - Run
`python --version`

(Linux/macOS) or`py --version`

(Windows) to check your Python version reports 3.7.x.

## Clone the tutorial repository

In a terminal or command window, clone the following repository using Git:

`git clone https://github.com/Azure-Samples/functions-python-pytorch-tutorial.git`

Navigate into the folder and examine its contents.

`cd functions-python-pytorch-tutorial`

*start*is your working folder for the tutorial.*end*is the final result and full implementation for your reference.*resources*contains the machine learning model and helper libraries.*frontend*is a website that calls the function app.


## Create and activate a Python virtual environment

Navigate to the *start* folder and run the following commands to create and activate a virtual environment named `.venv`

.

```
cd start
python -m venv .venv
source .venv/bin/activate
```


If Python didn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


You run all subsequent commands in this activated virtual environment. (To exit the virtual environment, run `deactivate`

.)

## Create a local functions project

In Azure Functions, a function project is a container for one or more individual functions that each responds to a specific trigger. All functions in a project share the same local and hosting configurations. In this section, you create a function project that contains a single boilerplate function named `classify`

that provides an HTTP endpoint. You add more specific code in a later section.

In the

*start*folder, use the Azure Functions Core Tools to initialize a Python function app:`func init --worker-runtime python`

After initialization, the

*start*folder contains various files for the project, including configurations files named[local.settings.json](functions-develop-local#local-settings-file)and[host.json](functions-host-json). Because*local.settings.json*can contain secrets downloaded from Azure, the file is excluded from source control by default in the*.gitignore*file.Tip

Because a function project is tied to a specific runtime, all the functions in the project must be written with the same language.

Add a function to your project by using the following command, where the

`--name`

argument is the unique name of your function and the`--template`

argument specifies the function's trigger.`func new`

create a subfolder matching the function name that contains a code file appropriate to the project's chosen language and a configuration file named*function.json*.`func new --name classify --template "HTTP trigger"`

This command creates a folder matching the name of the function,

*classify*. In that folder are two files:*__init__.py*, which contains the function code, and*function.json*, which describes the function's trigger and its input and output bindings. For details on the contents of these files, see[Programming model](functions-reference-python?pivots=python-mode-configuration#programming-model)in the Python developer guide.

## Run the function locally

Start the function by starting the local Azure Functions runtime host in the

*start*folder:`func start`

Once you see the

`classify`

endpoint appear in the output, navigate to the URL,`http://localhost:7071/api/classify?name=Azure`

. The message "Hello Azure!" should appear in the output.Use

**Ctrl**-**C**to stop the host.

## Import the PyTorch model and add helper code

To modify the `classify`

function to classify an image based on its contents, you use a pre-trained [ResNet](https://arxiv.org/abs/1512.03385) model. The pre-trained model, which comes from [PyTorch](https://pytorch.org/hub/pytorch_vision_resnet/), classifies an image into 1 of 1000 [ImageNet classes](https://gist.github.com/yrevar/942d3a0ac09ec9e5eb3a). You then add some helper code and dependencies to your project.

In the

*start*folder, run the following command to copy the prediction code and labels into the*classify*folder.`cp ../resources/predict.py classify cp ../resources/labels.txt classify`

Verify that the

*classify*folder contains files named*predict.py*and*labels.txt*. If not, check that you ran the command in the*start*folder.Open

*start/requirements.txt*in a text editor and add the dependencies required by the helper code, which should look like:`azure-functions requests -f https://download.pytorch.org/whl/torch_stable.html torch==1.13.0+cpu torchvision==0.14.0+cpu`

Tip

The versions of torch and torchvision must match values listed in the version table of the

[PyTorch vision repo](https://github.com/pytorch/vision).Save

*requirements.txt*, then run the following command from the*start*folder to install the dependencies.`pip install --no-cache-dir -r requirements.txt`


Installation may take a few minutes, during which time you can proceed with modifying the function in the next section.

Tip

On Windows, you may encounter the error, "Could not install packages due to an EnvironmentError: [Errno 2] No such file or directory:" followed by a long pathname to a file like

sharded_mutable_dense_hashtable.cpython-37.pyc. Typically, this error happens because the depth of the folder path becomes too long. In this case, set the registry key`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem@LongPathsEnabled`

to`1`

to enable long paths. Alternately, check where your Python interpreter is installed. If that location has a long path, try reinstalling in a folder with a shorter path.

## Update the function to run predictions

Open

*classify/__init__.py*in a text editor and add the following lines after the existing`import`

statements to import the standard JSON library and the*predict*helpers:`import logging import azure.functions as func import json # Import helper script from .predict import predict_image_from_url`

Replace the entire contents of the

`main`

function with the following code:`def main(req: func.HttpRequest) -> func.HttpResponse: image_url = req.params.get('img') logging.info('Image URL received: ' + image_url) results = predict_image_from_url(image_url) headers = { "Content-type": "application/json", "Access-Control-Allow-Origin": "*" } return func.HttpResponse(json.dumps(results), headers = headers)`

This function receives an image URL in a query string parameter named

`img`

. It then calls`predict_image_from_url`

from the helper library to download and classify the image using the PyTorch model. The function then returns an HTTP response with the results.Important

Because this HTTP endpoint is called by a web page hosted on another domain, the response includes an

`Access-Control-Allow-Origin`

header to satisfy the browser's Cross-Origin Resource Sharing (CORS) requirements.In a production application, change

`*`

to the web page's specific origin for added security.Save your changes, then assuming that dependencies have finished installing, start the local function host again with

`func start`

. Be sure to run the host in the*start*folder with the virtual environment activated. Otherwise the host will start, but you'll see errors when invoking the function.`func start`

In a browser, open the following URL to invoke the function with the URL of a Bernese Mountain Dog image and confirm that the returned JSON classifies the image as a Bernese Mountain Dog.

`http://localhost:7071/api/classify?img=https://raw.githubusercontent.com/Azure-Samples/functions-python-pytorch-tutorial/master/resources/assets/Bernese-Mountain-Dog-Temperament-long.jpg`

Keep the host running because you use it in the next step.


### Run the local web app front end to test the function

To test invoking the function endpoint from another web app, there's a simple app in the repository's *frontend* folder.

Open a new terminal or command prompt and activate the virtual environment (as described earlier under

[Create and activate a Python virtual environment](#create-and-activate-a-python-virtual-environment)).Navigate to the repository's

*frontend*folder.Start an HTTP server with Python:

`python -m http.server`

In a browser, navigate to

`localhost:8000`

, then enter one of the following photo URLs into the textbox, or use the URL of any publicly accessible image.`https://raw.githubusercontent.com/Azure-Samples/functions-python-pytorch-tutorial/master/resources/assets/Bernese-Mountain-Dog-Temperament-long.jpg`

`https://github.com/Azure-Samples/functions-python-pytorch-tutorial/blob/master/resources/assets/bald-eagle.jpg?raw=true`

`https://raw.githubusercontent.com/Azure-Samples/functions-python-pytorch-tutorial/master/resources/assets/penguin.jpg`


Select

**Submit**to invoke the function endpoint to classify the image.If the browser reports an error when you submit the image URL, check the terminal in which you're running the function app. If you see an error like "No module found 'PIL'", you may have started the function app in the

*start*folder without first activating the virtual environment you created earlier. If you still see errors, run`pip install -r requirements.txt`

again with the virtual environment activated and look for errors.

## Clean up resources

Because the entirety of this tutorial runs locally on your machine, there are no Azure resources or services to clean up.

## Next steps

In this tutorial, you learned how to build and customize an HTTP API endpoint with Azure Functions to classify images using a PyTorch model. You also learned how to call the API from a web app. You can use the techniques in this tutorial to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.

See also:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-identity-based-connections-tutorial-2 -->

# Tutorial: Use identity-based connections instead of secrets with triggers and bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This tutorial shows you how to configure Azure Functions to connect to Azure Service Bus queues by using managed identities, instead of secrets stored in the function app settings. The tutorial is a continuation of the [Create a function app without default storage secrets in its definition](functions-identity-based-connections-tutorial) tutorial. To learn more about identity-based connections, see [Configure an identity-based connection.](functions-reference#configure-an-identity-based-connection).

While the procedures shown work generally for all languages, this tutorial currently supports C# class library functions on Windows specifically.

In this tutorial, you learn how to:

- Create a Service Bus namespace and queue.
- Configure your function app with a managed identity.
- Create a role assignment granting that identity permission to read from the Service Bus queue.
- Create and deploy a function app with a Service Bus trigger.
- Verify your identity-based connection to the Service Bus.

## Prerequisite

[Azure Functions Core Tools](functions-run-local#v2)version 4.x.Complete the previous tutorial:

[Create a function app with identity-based connections](functions-identity-based-connections-tutorial).

## Create a Service Bus namespace and queue

In the

[Azure portal](https://portal.azure.com), choose**Create a resource (+)**.On the

**Create a resource**page, search for and select**Service Bus**, and then select**Create**.On the

**Basics**page, use the following table to configure the Service Bus namespace settings. Use the default values for the remaining options.Option Suggested value Description **Subscription**Your subscription The subscription under which your resources are created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The resource group you created with your function app. **Namespace name**Globally unique name The namespace of your instance from which to trigger your function. Because the namespace is publicly accessible, you must use a name that is globally unique across Azure. The name must also be between 6 and 50 characters in length, contain only alphanumeric characters and dashes, and can't start with a number. [Location](https://azure.microsoft.com/regions/)myFunctionRegion The region where you created your function app. **Pricing tier**Basic The basic Service Bus tier. Select

**Review + create**. After validation finishes, select**Create**.After deployment completes, select

**Go to resource**.In your new Service Bus namespace, select

**+ Queue**to add a queue.Enter

**myinputqueue**as the new queue's name and select**Create**.

Now that you have a queue, you can add a role assignment to the managed identity of your function app.

## Configure your Service Bus trigger with a managed identity

To use Service Bus triggers with identity-based connections, you need to add the **Azure Service Bus Data Receiver** role assignment to the managed identity in your function app. This role is required when using managed identities to trigger off of your Service Bus namespace. You can also add your own account to this role, which makes it possible to connect to the Service Bus namespace during local testing.

Note

Role requirements for using identity-based connections vary depending on the service and how you are connecting to it. Needs vary across triggers, input bindings, and output bindings. For more information about specific role requirements, see the trigger and binding documentation for the service.

In your Service Bus namespace that you created, select

**Access control (IAM)**. This page is where you can view and configure who has access to the resource.Select

**+ Add**and select**Add role assignment**.Search for

**Azure Service Bus Data Receiver**, select it, and then select**Next**.On the

**Members**tab, under**Assign access to**, choose**Managed Identity**Select

**Select members**to open the**Select managed identities**panel.Confirm that the

**Subscription**is the one in which you created the resources earlier.In the

**Managed identity**selector, choose**Function App**from the**System-assigned managed identity**category. The**Function App**label might have a number in parentheses next to it, indicating the number of apps in the subscription with system-assigned identities.Your app should appear in a list below the input fields. If you don't see it, you can use the

**Select**box to filter the results with your app's name.Select your application. It should move down into the

**Selected members**section. Select**Select**.Back on the

**Add role assignment**screen, select**Review + assign**. Review the configuration, and then select**Review + assign**.

You've granted your function app access to the Service Bus namespace using managed identities.

## Connect to the Service Bus in your function app

In the portal, search for the function app you created in the

[previous tutorial](functions-identity-based-connections-tutorial), or browse to it in the**Function App**page.In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, select**+ Add**to create a setting. Use the information in the following table to enter the**Name**and**Value**for the new setting:Name Value Description **ServiceBusConnection__fullyQualifiedNamespace**<SERVICE_BUS_NAMESPACE>.servicebus.windows.net This setting connects your function app to the Service Bus using an identity-based connection instead of secrets. Select

**Apply**, and then select**Apply**and**Confirm**to save your changes and restart the app function.

Note

When you use [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator, such as `:`

or `/`

, in place of the `__`

to ensure names are resolved correctly.

For example, `ServiceBusConnection:fullyQualifiedNamespace`

.

Now that you've prepared the function app to connect to the Service Bus namespace using a managed identity, you can add a new function that uses a Service Bus trigger to your local project.

## Add a Service Bus triggered function

Run the

`func init`

command, as follows, to create a functions project in a folder named LocalFunctionProj with the specified runtime:`func init LocalFunctionProj --dotnet`

Navigate to the project folder:

`cd LocalFunctionProj`

In the root project folder, run the following command:

`dotnet add package Microsoft.Azure.WebJobs.Extensions.ServiceBus --version 5.2.0`

This command replaces the default version of the Service Bus extension package with a version that supports managed identities.

Run the following command to add a Service Bus triggered function to the project:

`func new --name ServiceBusTrigger --template ServiceBusQueueTrigger`

This command adds the code for a new Service Bus trigger and a reference to the extension package. You need to add a Service Bus namespace connection setting for this trigger.

Open the new

*ServiceBusTrigger.cs*project file and replace the`ServiceBusTrigger`

class with the following code:`public static class ServiceBusTrigger { [FunctionName("ServiceBusTrigger")] public static void Run([ServiceBusTrigger("myinputqueue", Connection = "ServiceBusConnection")]string myQueueItem, ILogger log) { log.LogInformation($"C# ServiceBus queue trigger function processed message: {myQueueItem}"); } }`

This code sample updates the queue name to

`myinputqueue`

, which is the same name as you queue you created earlier. It also sets the name of the Service Bus connection to`ServiceBusConnection`

. This name is the Service Bus namespace used by the identity-based connection`ServiceBusConnection__fullyQualifiedNamespace`

you configured in the portal.

Note

If you try to run your functions now using `func start`

, you'll receive an error. This is because you don't have an identity-based connection defined locally. If you want to run your function locally, set the app setting `ServiceBusConnection__fullyQualifiedNamespace`

in `local.settings.json`

as you did in [the previous section](#connect-to-the service-bus-in-your-function-app). In addition, you need to assign the role to your developer identity. For more information, see [local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

Note

When using [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp) or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for Managed Identity connections, setting names should use a valid key separator such as `:`

or `/`

in place of the `__`

to ensure names are resolved correctly.

For example, `ServiceBusConnection:fullyQualifiedNamespace`

.

## Publish the updated project

Run the following command to locally generate the files needed for the deployment package:

`dotnet publish --configuration Release`

Browse to the

`\bin\Release\netcoreapp3.1\publish`

subfolder and create a .zip file from its contents.Publish the .zip file by running the following command, replacing the

`FUNCTION_APP_NAME`

,`RESOURCE_GROUP_NAME`

, and`PATH_TO_ZIP`

parameters as appropriate:`az functionapp deploy -n FUNCTION_APP_NAME -g RESOURCE_GROUP_NAME --src-path PATH_TO_ZIP`


Now that you've updated the function app with the new trigger, you can verify that it works using the identity.

## Validate your changes

In the portal, search for

`Application Insights`

and select**Application Insights**under**Services**.In

**Application Insights**, browse or search for your named instance.In your instance, select

**Live Metrics**under**Investigate**.Keep the previous tab open, and open the Azure portal in a new tab. In your new tab, navigate to your Service Bus namespace, select

**Queues**from the left menu.Select your queue named

`myinputqueue`

.Select

**Service Bus Explorer**from the left menu.Send a test message.

Select your open

**Live Metrics**tab and see the Service Bus queue execution.

Congratulations! You have successfully set up your Service Bus queue trigger with a managed identity.

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

## Next steps

In this tutorial, you created a function app with identity-based connections.

Advance to the next article to learn how to manage identity.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/disable-function -->

# How to disable functions in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to disable a function in Azure Functions. To *disable* a function means to make the runtime ignore the event intended to trigger the function. This ability lets you prevent a specific function from running without having to modify and republish the entire function app.

You can disable a function in place by creating an app setting in the format `AzureWebJobs.<FUNCTION_NAME>.Disabled`

set to `true`

. You can create and modify this application setting in several ways, including by using the [Azure CLI](/en-us/cli/azure/), [Azure PowerShell](/en-us/powershell/azure/), and from your function's **Overview** tab in the [Azure portal](https://portal.azure.com).

Note

Changing application settings causes your function app to restart by default across all hosting plans. For zero-downtime deployments when changing settings, use the [Flex Consumption plan](flex-consumption-plan) with [rolling updates as the site update strategy](flex-consumption-site-updates). For other hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments) for guidance on minimizing downtime.

## Disable a function

Use one of these modes to create an app setting that disables an example function named `QueueTrigger`

:

Use the **Enable** and **Disable** buttons on the function's **Overview** page. These buttons work by changing the value of the `AzureWebJobs.QueueTrigger.Disabled`

app setting. The function-specific app setting is created the first time a function is disabled.

Even when you publish to your function app from a local project, you can still use the portal to disable functions in the function app.

Note

Disabled functions can still be run by calling the REST endpoint using a master key. To learn more, see [Run a disabled function](#run-a-disabled-function). This means that a disabled function still runs when started from the **Test/Run** window in the portal using the **master (Host key)**.

## Disable functions in a slot

By default, app settings also apply to apps running in deployment slots. You can, however, override the app setting used by the slot by setting a slot-specific app setting. For example, you might want a function to be active in production but not during deployment testing. It's common to disable timer triggered functions in slots to prevent simultaneous executions.

To disable a function only in the staging slot:

Navigate to the slot instance of your function app by selecting **Deployment slots** under **Deployment**, choosing your slot, and selecting **Functions** in the slot instance. Choose your function, then use the **Enable** and **Disable** buttons on the function's **Overview** page. These buttons work by changing the value of the `AzureWebJobs.<FUNCTION_NAME>.Disabled`

app setting. This function-specific setting is created the first time you disable the function.

You can also directly add the app setting named `AzureWebJobs.<FUNCTION_NAME>.Disabled`

with value of `true`

in the **Configuration** for the slot instance. When you add a slot-specific app setting, make sure to check the **Deployment slot setting** box. This option maintains the setting value with the slot during swaps.

To learn more, see [Azure Functions Deployment slots](functions-deployment-slots).

## Run a disabled function

You can still cause a disabled function to run by supplying the master access key (`_master`

) in a REST request to the endpoint URL of the disabled function. In this way, you can develop and validate functions in Azure in a disabled state while preventing them from being accessed by others. Using any other type of key in the request returns an HTTP 404 response.

Caution

Due to the elevated permissions in your function app granted by the master key, you shouldn't share this key with third parties or distribute it in native client applications. Use caution when choosing the admin HTTP access level for your function endpoints.

To learn more about the master key, see [Understand keys](function-keys-how-to#understand-keys). To learn more about calling non-HTTP triggered functions, see [Manually run a non HTTP-triggered function](functions-manually-run-non-http).

## Disable functions locally

Functions can be disabled in the same way when running locally. To disable a function named `QueueTrigger`

, add an entry to the Values collection in the local.settings.json file, as follows:

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "python",
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"AzureWebJobs.QueueTrigger.Disabled": true
}
}
```


## Considerations

Keep the following considerations in mind when you disable functions:

When you disable an HTTP triggered function by using the methods described in this article, the endpoint can still be accessed when running on your local computer and

[in the portal](#run-a-disabled-function).At this time, function names that contain a hyphen (

`-`

) can't be disabled when running on Linux. If you plan to disable your functions when running on Linux, don't use hyphens in your function names.

## Next steps

This article is about disabling automatic triggers. For more information about triggers, see [Triggers and bindings](functions-triggers-bindings).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-kubernetes-keda -->

# Azure Functions on Kubernetes with KEDA

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Functions runtime provides flexibility in hosting where and how you want. [KEDA](https://keda.sh) (Kubernetes-based Event Driven Autoscaling) pairs seamlessly with the Azure Functions runtime and tooling to provide event driven scale in Kubernetes.

Important

Running your containerized function apps on Kubernetes, either by using KEDA or by direct deployment, is an open-source effort that you can use free of cost. Best-effort support is provided by contributors and from the community by using [GitHub issues in the Azure Functions repository](https://github.com/Azure/Azure-Functions/issues). Please use these issues to report bugs and raise feature requests.

For fully-supported Kubernetes deployments, instead consider [Azure Container Apps hosting of Azure Functions](../container-apps/functions-overview).

## How Kubernetes-based functions work

The Azure Functions service is made up of two key components: a runtime and a scale controller. The Functions runtime runs and executes your code. The runtime includes logic on how to trigger, log, and manage function executions. The Azure Functions runtime can run *anywhere*. The other component is a scale controller. The scale controller monitors the rate of events that are targeting your function, and proactively scales the number of instances running your app. To learn more, see [Azure Functions scale and hosting](functions-scale).

Kubernetes-based Functions provides the Functions runtime in a [Docker container](functions-create-container-registry) with event-driven scaling through KEDA. KEDA can scale in to zero instances (when no events are occurring) and out to *n* instances. It does this by exposing custom metrics for the Kubernetes autoscaler (Horizontal Pod Autoscaler). Using Functions containers with KEDA makes it possible to replicate serverless function capabilities in any Kubernetes cluster. These functions can also be deployed using [Azure Kubernetes Services (AKS) virtual nodes](/en-us/azure/aks/virtual-nodes-cli) feature for serverless infrastructure.

## Managing KEDA and functions in Kubernetes

To run Functions on your Kubernetes cluster, you must install the KEDA component. You can install this component in one of the following ways:

Azure Functions Core Tools: using the

.`func kubernetes install`

commandHelm: there are various ways to install KEDA in any Kubernetes cluster, including Helm. Deployment options are documented on the

[KEDA site](https://keda.sh/docs/deploy/).

## Deploying a function app to Kubernetes

You can deploy any function app to a Kubernetes cluster running KEDA. Since your functions run in a Docker container, your project needs a Dockerfile. You can create a Dockerfile by using the [ --docker option](functions-core-tools-reference#func-init) when calling

`func init`

to create the project. If you forgot to create your Dockerfile, you can always call `func init`

again from the root of your code project.(Optional) If you need to create your Dockerfile, use the

command with the`func init`

`--docker-only`

option:`func init --docker-only`

To learn more about Dockerfile generation, see the

reference.`func init`

Use the

command to build your image and deploy your containerized function app to Kubernetes:`func kubernetes deploy`

`func kubernetes deploy --name <name-of-function-deployment> --registry <container-registry-username>`

In this example, replace

`<name-of-function-deployment>`

with the name of your function app. The deploy command performs these tasks:- The Dockerfile created earlier is used to build a local image for your containerized function app.
- The local image is tagged and pushed to the container registry where the user is logged in.
- A manifest is created and applied to the cluster that defines a Kubernetes
`Deployment`

resource, a`ScaledObject`

resource, and`Secrets`

, which includes environment variables imported from your`local.settings.json`

file.


### Deploying a function app from a private registry

The previous deployment steps work for private registries as well. If you're pulling your container image from a private registry, include the `--pull-secret`

flag that references the Kubernetes secret holding the private registry credentials when running `func kubernetes deploy`

.

## Removing a function app from Kubernetes

After deploying you can remove a function by removing the associated `Deployment`

, `ScaledObject`

, an `Secrets`

created.

```
kubectl delete deploy <name-of-function-deployment>
kubectl delete ScaledObject <name-of-function-deployment>
kubectl delete secret <name-of-function-deployment>
```


## Uninstalling KEDA from Kubernetes

You can remove KEDA from your cluster in one of the following ways:

Azure Functions Core Tools: using the

.`func kubernetes remove`

commandHelm: see the uninstall steps

[on the KEDA site](https://keda.sh/docs/deploy/).

## Supported triggers in KEDA

KEDA has support for the following Azure Function triggers:

### HTTP Trigger support

You can use Azure Functions that expose HTTP triggers, but KEDA doesn't directly manage them. You can use the KEDA prometheus trigger to [scale HTTP Azure Functions from one to n instances](https://dev.to/anirudhgarg_99/scale-up-and-down-a-http-triggered-function-app-in-kubernetes-using-keda-4m42).

## Next Steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-service-bus -->

# Azure Service Bus bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with [Azure Service Bus](https://azure.microsoft.com/services/service-bus) via [triggers and bindings](functions-triggers-bindings). Integrating with Service Bus allows you to build functions that react to and send queue or topic messages.

| Action | Type |
|---|---|
| Run a function when a Service Bus queue or topic message is created |
|

[Output binding](functions-bindings-service-bus-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.servicebus).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [Azure.Messaging.ServiceBus](/en-us/dotnet/api/azure.messaging.servicebus).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.ServiceBus), version 5.x.

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

**Service Bus trigger**

When you want the function to process a single message, the Service Bus trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message as a string. Use when the message is simple text. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | When an event contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

When binding to

`ServiceBusReceivedMessage`

, you can optionally also include a parameter of type [ServiceBusMessageActions](https://github.com/Azure/azure-functions-dotnet-worker/blob/main/extensions/Worker.Extensions.ServiceBus/src/ServiceBusMessageActions.cs)1,2to perform[message settlement](../service-bus-messaging/message-transfers-locks-settlement#peeklock)actions.When you want the function to process a batch of messages, the Service Bus trigger can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single message types |
An array of events from the batch. Each entry represents one event. When binding to `ServiceBusReceivedMessage[]` , you can optionally also include a parameter of type
1,2 to perform
|

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.ServiceBus 5.14.1 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.ServiceBus/5.14.1) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

2 When using `ServiceBusMessageActions`

, set the [ AutoCompleteMessages property of the trigger attribute](functions-bindings-service-bus-trigger#attributes) to

`false`

. This prevents the runtime from attempting to complete messages after a successful function invocation.**Service Bus output binding**

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

## SDK Binding Types

SDK Types for Azure Service Bus are in Preview. Follow the [Python SDK Bindings for Service Bus Sample](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-servicebus/samples/README.md) to get started with SDK Types for Service Bus in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| ServiceBus trigger |
|

`ServiceBusReceivedMessage`

## host.json settings

This section describes the configuration settings available for this binding, which depends on the runtime and extension version.

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"clientRetryOptions":{
"mode": "exponential",
"tryTimeout": "00:01:00",
"delay": "00:00:00.80",
"maxDelay": "00:01:00",
"maxRetries": 3
},
"prefetchCount": 0,
"transportType": "amqpWebSockets",
"webProxy": "https://proxyserver:8080",
"autoCompleteMessages": true,
"maxAutoLockRenewalDuration": "00:05:00",
"maxConcurrentCalls": 16,
"maxConcurrentSessions": 8,
"maxMessageBatchSize": 1000,
"minMessageBatchSize": 1,
"maxBatchWaitTime": "00:00:30",
"sessionIdleTimeout": "00:01:00",
"enableCrossEntityTransactions": false
}
}
}
```


The `clientRetryOptions`

settings only apply to interactions with the Service Bus service. They don't affect retries of function executions. For more information, see [Retries](functions-bindings-error-pages#retries).

| Property | Default | Description |
|---|---|---|
mode |
`Exponential` |
The approach to use for calculating retry delays. The default exponential mode retries attempts with a delay based on a back-off strategy where each attempt increases the wait duration before retrying. The `Fixed` mode retries attempts at fixed intervals with each delay having a consistent duration. |
tryTimeout |
`00:01:00` |
The maximum duration to wait for an operation per attempt. |
delay |
`00:00:00.80` |
The delay or back-off factor to apply between retry attempts. |
maxDelay |
`00:01:00` |
The maximum delay to allow between retry attempts |
maxRetries |
`3` |
The maximum number of retry attempts before considering the associated operation to have failed. |
prefetchCount |
`0` |
Gets or sets the number of messages that the message receiver can simultaneously request. |
transportType |
amqpTcp | The protocol and transport that is used for communicating with Service Bus. Available options: `amqpTcp` , `amqpWebSockets` |
webProxy |
n/a | The proxy to use for communicating with Service Bus over web sockets. A proxy cannot be used with the `amqpTcp` transport. |
autoCompleteMessages |
`true` |
Determines whether or not to automatically complete messages after successful execution of the function. |
maxAutoLockRenewalDuration |
`00:05:00` |
The maximum duration within which the message lock will be renewed automatically. This setting only applies for functions that receive a single message at a time and doesn't apply to functions receiving a batch of messages. For batches, the maximum duration is set
|

**maxConcurrentCalls**`16`

`16`

means that the maximum number of concurrent calls per instance is really `32`

(or `2 * 16`

). This setting is used only when the `isSessionsEnabled`

property or attribute on [the trigger](functions-bindings-service-bus-trigger)is set to`false`

. This setting only applies for functions that receive a single message at a time as opposed to in a batch.**maxConcurrentSessions**`8`

`isSessionsEnabled`

property or attribute on [the trigger](functions-bindings-service-bus-trigger)is set to`true`

. This setting only applies for functions that receive a single message at a time.**maxMessageBatchSize**`1000`

**minMessageBatchSize**1`1`

`maxMessageBatchSize`

. The minimum size isn't strictly guaranteed. A partial batch is dispatched when a full batch can't be prepared before the

`maxBatchWaitTime`

has elapsed.**maxBatchWaitTime**1`00:00:30`

`minMessageBatchSize`

is larger than 1 and is ignored otherwise. If less than `minMessageBatchSize`

messages were available before the wait time elapses, the function is invoked with a partial batch. The longest allowed wait time is 50% of the entity message lock duration, meaning the maximum allowed is 2 minutes and 30 seconds. Otherwise, you may get lock exceptions. **NOTE:**This interval is not a strict guarantee for the exact timing on which the function is invoked. There is a small margin of error due to timer precision.**sessionIdleTimeout****enableCrossEntityTransactions**`false`

1 Using `minMessageBatchSize`

and `maxBatchWaitTime`

requires [v5.10.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ServiceBus/5.10.0) of the `Microsoft.Azure.WebJobs.Extensions.ServiceBus`

package, or a later version.

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/how-to-create-function-vs-code -->

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
