---
merged_at: 2026-01-26T21:02:36.366729
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-azure-sql-input__functions-bindings-azure-mysql-output_opena_f416d2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-azure-sql-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-sql-input -->

# Azure SQL input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When a function runs, the Azure SQL input binding retrieves data from a database and passes it to the input parameter of the function.

For information on setup and configuration details, see the [overview](functions-bindings-azure-sql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-outofproc).

This section contains the following examples:

[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-c-oop)[HTTP trigger, get multiple rows from route data](#http-trigger-get-multiple-items-from-route-data-c-oop)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-c-oop)

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


### HTTP trigger, get row by ID from query string

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single record. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses a query string to specify the ID. That ID is used to retrieve a `ToDoItem`

record with the specified query.

Note

The HTTP query string parameter is case-sensitive.

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Azure.Functions.Worker.Http;
namespace AzureSQLSamples
{
public static class GetToDoItem
{
[FunctionName("GetToDoItem")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "gettodoitem")]
HttpRequest req,
[SqlInput(commandText: "select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id",
commandType: System.Data.CommandType.Text,
parameters: "@Id={Query.id}",
connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItem)
{
return new OkObjectResult(toDoItem.FirstOrDefault());
}
}
}
```


### HTTP trigger, get multiple rows from route parameter

The following example shows a [C# function](functions-dotnet-class-library) that retrieves documents returned by the query. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses route data to specify the value of a query parameter. That parameter is used to filter the `ToDoItem`

records in the specified query.

```
using System.Collections.Generic;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Azure.Functions.Worker.Http;
namespace AzureSQLSamples
{
public static class GetToDoItems
{
[FunctionName("GetToDoItems")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "gettodoitems/{priority}")]
HttpRequest req,
[SqlInput(commandText: "select [Id], [order], [title], [url], [completed] from dbo.ToDo where [Priority] > @Priority",
commandType: System.Data.CommandType.Text,
parameters: "@Priority={priority}",
connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItems)
{
return new OkObjectResult(toDoItems);
}
}
}
```


### HTTP trigger, delete rows

The following example shows a [C# function](functions-dotnet-class-library) that executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the SQL database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
namespace AzureSQL.ToDo
{
public static class DeleteToDo
{
// delete all items or a specific item from querystring
// returns remaining items
// uses input binding with a stored procedure DeleteToDo to delete items and return remaining items
[FunctionName("DeleteToDo")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "delete", Route = "DeleteFunction")] HttpRequest req,
ILogger log,
[SqlInput(commandText: "DeleteToDo", commandType: System.Data.CommandType.StoredProcedure,
parameters: "@Id={Query.id}", connectionStringSetting: "SqlConnectionString")]
IEnumerable<ToDoItem> toDoItems)
{
return new OkObjectResult(toDoItems);
}
}
}
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-java).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-java)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-java)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-java)

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


### HTTP trigger, get multiple rows

The following example shows a SQL input binding in a Java function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

```
package com.function;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.sql.annotation.SQLInput;
import java.util.Optional;
public class GetToDoItems {
@FunctionName("GetToDoItems")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@SQLInput(
name = "toDoItems",
commandText = "SELECT * FROM dbo.ToDo",
commandType = "Text",
connectionStringSetting = "SqlConnectionString")
ToDoItem[] toDoItems) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(toDoItems).build();
}
}
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding in a Java function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

```
public class GetToDoItem {
@FunctionName("GetToDoItem")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@SQLInput(
name = "toDoItems",
commandText = "SELECT * FROM dbo.ToDo",
commandType = "Text",
parameters = "@Id={Query.id}",
connectionStringSetting = "SqlConnectionString")
ToDoItem[] toDoItems) {
ToDoItem toDoItem = toDoItems[0];
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(toDoItem).build();
}
}
```


### HTTP trigger, delete rows

The following example shows a SQL input binding in a Java function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
public class DeleteToDo {
@FunctionName("DeleteToDo")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@SQLInput(
name = "toDoItems",
commandText = "dbo.DeleteToDo",
commandType = "StoredProcedure",
parameters = "@Id={Query.id}",
connectionStringSetting = "SqlConnectionString")
ToDoItem[] toDoItems) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(toDoItems).build();
}
}
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-js).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-javascript)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-javascript)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-javascript)

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


### HTTP trigger, get multiple rows

The following example shows a SQL input binding that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo',
commandType: 'Text',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo',
commandType: 'Text',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: (request, context) => {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
},
});
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id',
commandType: 'Text',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItem = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItem,
};
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const sqlInput = input.sql({
commandText: 'select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id',
commandType: 'Text',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: (request, context) => {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItem = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItem,
};
},
});
```


### HTTP trigger, delete rows

The following example shows a SQL input binding that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const sqlInput = input.sql({
commandText: 'DeleteToDo',
commandType: 'StoredProcedure',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const sqlInput = input.sql({
commandText: 'DeleteToDo',
commandType: 'StoredProcedure',
parameters: '@Id={Query.id}',
connectionStringSetting: 'SqlConnectionString',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
extraInputs: [sqlInput],
handler: (request, context) => {
context.log('HTTP trigger and SQL input binding function processed a request.');
const toDoItems = context.extraInputs.get(sqlInput);
return {
jsonBody: toDoItems,
};
},
});
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-powershell).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-powershell)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-powershell)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-powershell)

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


### HTTP trigger, get multiple rows

The following example shows a SQL input binding in a function.json file and a PowerShell function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
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
"direction": "in",
"commandText": "select [Id], [order], [title], [url], [completed] from dbo.ToDo",
"commandType": "Text",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request, $todoItems)
Write-Host "PowerShell function with SQL Input Binding processed a request."
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $todoItems
})
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding in a PowerShell function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

The following is binding data in the function.json file:

```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"name": "todoItem",
"type": "sql",
"direction": "in",
"commandText": "select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id",
"commandType": "Text",
"parameters": "@Id = {Query.id}",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request, $todoItem)
Write-Host "PowerShell function with SQL Input Binding processed a request."
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $todoItem
})
```


### HTTP trigger, delete rows

The following example shows a SQL input binding in a function.json file and a PowerShell function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


```
{
"authLevel": "anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
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
"direction": "in",
"commandText": "DeleteToDo",
"commandType": "StoredProcedure",
"parameters": "@Id = {Query.id}",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($Request, $todoItems)
Write-Host "PowerShell function with SQL Input Binding processed a request."
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $todoItems
})
```


More samples for the Azure SQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-python).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-python)[HTTP trigger, get row by ID from query string](#http-trigger-look-up-id-from-query-string-python)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-python)

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


### HTTP trigger, get multiple rows

The following example shows a SQL input binding in a function.json file and a Python function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query and returns the results in the HTTP response.

The following python code is a sample function_app.py file:

```
import json
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="GetToDo")
@app.route(route="gettodo")
@app.sql_input(arg_name="todo",
command_text="select [Id], [order], [title], [url], [completed] from dbo.ToDo",
command_type="Text",
connection_string_setting="SqlConnectionString")
def get_todo(req: func.HttpRequest, todo: func.SqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), todo))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, get row by ID from query string

The following example shows a SQL input binding in a Python function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It reads from a query, which is filtered by a parameter from the query string, and it returns the row in the HTTP response.

The following python code is a sample function_app.py file:

```
import json
import logging
import azure.functions as func
from azure.functions.decorators.core import DataType
app = func.FunctionApp()
@app.function_name(name="GetToDo")
@app.route(route="gettodo/{id}")
@app.sql_input(arg_name="todo",
command_text="select [Id], [order], [title], [url], [completed] from dbo.ToDo where Id = @Id",
command_type="Text",
parameters="@Id={id}",
connection_string_setting="SqlConnectionString")
def get_todo(req: func.HttpRequest, todo: func.SqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), todo))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, delete rows

The following example shows a SQL input binding in a function.json file and a Python function that is [triggered by an HTTP](functions-bindings-http-webhook-trigger) request. It executes a stored procedure with input from the HTTP request query parameter.

The stored procedure `dbo.DeleteToDo`

must be created on the database. In this example, the stored procedure deletes a single record or all records depending on the value of the parameter.

```
CREATE PROCEDURE [dbo].[DeleteToDo]
@Id NVARCHAR(100)
AS
DECLARE @UID UNIQUEIDENTIFIER = TRY_CAST(@ID AS UNIQUEIDENTIFIER)
IF @UId IS NOT NULL AND @Id != ''
BEGIN
DELETE FROM dbo.ToDo WHERE Id = @UID
END
ELSE
BEGIN
DELETE FROM dbo.ToDo WHERE @ID = ''
END
SELECT [Id], [order], [title], [url], [completed] FROM dbo.ToDo
GO
```


The following python code is a sample function_app.py file:

```
import json
import logging
import azure.functions as func
from azure.functions.decorators.core import DataType
app = func.FunctionApp()
@app.function_name(name="DeleteToDo")
@app.route(route="deletetodo/{id}")
@app.sql_input(arg_name="todo",
command_text="DeleteToDo",
command_type="StoredProcedure",
parameters="@Id={id}",
connection_string_setting="SqlConnectionString")
def get_todo(req: func.HttpRequest, todo: func.SqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), todo))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [SqlAttribute](https://github.com/Azure/azure-functions-sql-extension/blob/main/src/SqlAttribute.cs) attribute to declare the SQL bindings on the function, which has the following properties:

| Attribute property | Description |
|---|---|
CommandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
ConnectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
CommandType |
Required. A
|

**Parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@SQLInput`

annotation (`com.microsoft.azure.functions.sql.annotation.SQLInput`

) on parameters whose value would come from Azure SQL. This annotation supports the following elements:

| Element | Description |
|---|---|
commandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
commandType |
Required. A
|

**name****parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `input.sql()`

method.

| Property | Description |
|---|---|
commandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

**commandType**[CommandType](/en-us/dotnet/api/system.data.commandtype)value, which is[Text](/en-us/dotnet/api/system.data.commandtype#fields)for a query and[StoredProcedure](/en-us/dotnet/api/system.data.commandtype#fields)for a stored procedure.**parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
type |
Required. Must be set to `sql` . |
direction |
Required. Must be set to `in` . |
name |
Required. The name of the variable that represents the query results in function code. |
commandText |
Required. The Transact-SQL query command or name of the stored procedure executed by the binding. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is being executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

**commandType**[CommandType](/en-us/dotnet/api/system.data.commandtype)value, which is[Text](/en-us/dotnet/api/system.data.commandtype#fields)for a query and[StoredProcedure](/en-us/dotnet/api/system.data.commandtype#fields)for a stored procedure.**parameters**`@param1=param1,@param2=param2`

. The parameter name and the parameter value can't contain a comma (`,`

) or an equals sign (`=`

).When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The binding definition includes the SQL command text, the command type, parameters, and the connection string setting name. The command can be a Transact-SQL (T-SQL) query with the command type `System.Data.CommandType.Text`

or stored procedure name with the command type `System.Data.CommandType.StoredProcedure`

. The connection string setting name corresponds to the application setting (in `local.settings.json`

for local development) that contains the [connection string](/en-us/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-core-5.0&preserve-view=true#Microsoft_Data_SqlClient_SqlConnection_ConnectionString) to the Azure SQL or SQL Server instance.

Important

For optimal security, you should use Microsoft Entra ID with managed identities for connections between Functions and Azure SQL Database. Managed identities make your app more secure by eliminating secrets from your application deployments, such as credentials in the connection strings, server names, and ports being used. You can learn how to use managed identities in this tutorial, [Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).

Queries executed by the input binding are [parameterized](/en-us/dotnet/api/microsoft.data.sqlclient.sqlparameter) in Microsoft.Data.SqlClient to reduce the risk of [SQL injection](/en-us/sql/relational-databases/security/sql-injection) from the parameter values passed into the binding.

If an exception occurs when a SQL input binding is executed, then the function code doesn't execute. This behavior may result in an error code being returned, such as an HTTP trigger returning a 500 error code.


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-azure-mysql-output_openapi-apim-integrate-visual-studio.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-azure-mysql-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql-output -->

# Azure Database for MySQL output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use the Azure Database for MySQL output binding to write to a database.

For information on setup and configuration, see the [overview](functions-bindings-azure-mysql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

This section contains the following example:

The example refers to a `Product`

class and a corresponding database table:

```
namespace AzureMySqlSamples.Common
{
public class Product
{
public int? ProductId { get; set; }
public string Name { get; set; }
public int Cost { get; set; }
public override bool Equals(object obj)
}
}
```


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write one record

The following example shows a [C# function](functions-dotnet-class-library) that adds a record to a database, by using data provided in an HTTP `POST`

request as a JSON body.

```
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Azure.Functions.Worker.Http;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.OutputBindingSamples
{
public static class AddProduct
{
[FunctionName(nameof(AddProduct))]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "post", Route = "addproduct")]
[FromBody] Product prod,
[MySql("Products", "MySqlConnectionString")] out Product product)
{
product = prod;
return new CreatedResult($"/api/addproduct", product);
}
}
}
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-java).

This section contains the following example:

The example refers to a `Product`

class and a corresponding database table:

```
package com.function.Common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class Product {
@JsonProperty("ProductId")
private int ProductId;
@JsonProperty("Name")
private String Name;
@JsonProperty("Cost")
private int Cost;
public Product() {
}
public Product(int productId, String name, int cost) {
ProductId = productId;
Name = name;
Cost = cost;
}
}
```


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write a record to a table

The following example shows an Azure Database for MySQL output binding in a Java function that adds a record to a table, by using data provided in an HTTP `POST`

request as a JSON body. The function takes an additional dependency on the [com.google.code.gson](https://github.com/google/gson) library to parse the JSON body.

```
<dependency>
<groupId>com.google.code.gson</groupId>
<artifactId>gson</artifactId>
<version>2.10.1</version>
</dependency>
```


```
package com.function;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.OutputBinding;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.mysql.annotation.MySqlOutput;
import com.fasterxml.jackson.core.JsonParseException;
import com.fasterxml.jackson.databind.JsonMappingException;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.function.Common.Product;
import java.io.IOException;
import java.util.Optional;
public class AddProduct {
@FunctionName("AddProduct")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "addproduct")
HttpRequestMessage<Optional<String>> request,
@MySqlOutput(
name = "product",
commandText = "Products",
connectionStringSetting = "MySqlConnectionString")
OutputBinding<Product> product) throws JsonParseException, JsonMappingException, IOException {
String json = request.getBody().get();
ObjectMapper mapper = new ObjectMapper();
Product p = mapper.readValue(json, Product.class);
product.setValue(p);
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(product).build();
}
}
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

This section contains the following example:

The example refers to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write records to a table

The following example shows an Azure Database for MySQL output binding that adds records to a table, by using data provided in an HTTP `POST`

request as a JSON body.

```
const { app, output } = require('@azure/functions');
const mysqlOutput = output.generic({
type: 'mysql',
commandText: 'Products',
connectionStringSetting: 'MySqlConnectionString'
})
// Upsert the product, which will insert it into the Products table if the primary key (ProductId) for that item doesn't exist.
// If it does, update it to have the new name and cost.
app.http('AddProduct', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [mysqlOutput],
handler: async (request, context) => {
// Note that this expects the body to be a JSON object or array of objects that have a property
// matching each of the columns in the table to upsert to.
const product = await request.json();
context.extraOutputs.set(mysqlOutput, product);
return {
status: 201,
body: JSON.stringify(product)
};
}
});
```


```
const { app, output } = require('@azure/functions');
const mysqlOutput = output.generic({
type: 'mysql',
commandText: 'Products',
connectionStringSetting: 'MySqlConnectionString'
})
// Upsert the product, which will insert it into the Products table if the primary key (ProductId) for that item doesn't exist.
// If it does, update it to have the new name and cost.
app.http('AddProduct', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [mysqlOutput],
handler: async (request, context) => {
// Note that this expects the body to be a JSON object or array of objects that have a property
// matching each of the columns in the table to upsert to.
const product = await request.json();
context.extraOutputs.set(mysqlOutput, product);
return {
status: 201,
body: JSON.stringify(product)
};
}
});
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-powershell).

This section contains the following example:

The example refers to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, write records to a table

The following example shows an Azure Database for MySQL output binding in a function.json file and a PowerShell function that adds records to a table, by using data provided in an HTTP `POST`

request as a JSON body.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"direction": "in",
"type": "httpTrigger",
"methods": [
"post"
],
"route": "addproduct"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "product",
"type": "mysql",
"direction": "out",
"commandText": "Products",
"connectionStringSetting": "MySqlConnectionString"
}
],
"disabled": false
}
```


The [Configuration](#configuration) section explains these properties.

The following example is sample PowerShell code for the function in the run.ps1 file:

```
using namespace System.Net
# Trigger binding data passed in via parameter block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell function with MySql Output Binding processed a request."
# Note that this expects the body to be a JSON object or array of objects
# that have a property matching each of the columns in the table to upsert to.
$req_body = $Request.Body
# Assign the value that you want to pass to the MySQL output binding.
# The -Name value corresponds to the name property in the function.json file for the binding.
Push-OutputBinding -Name product -Value $req_body
# Assign the value to return as the HTTP response.
# The -Name value matches the name property in the function.json file for the binding.
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


More samples for the Azure Database for MySQL output binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-python).

This section contains the following example:

The example refers to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


Note

You must use Azure Functions version 1.22.0b4 for Python.

### HTTP trigger, write records to a table

The following example shows an Azure Database for MySQL output binding in a function.json file and a Python function that adds records to a table, by using data provided in an HTTP `POST`

request as a JSON body.

The following example is sample Python code for the function_app.py file:

```
import json
import azure.functions as func
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.generic_trigger(arg_name="req", type="httpTrigger", route="addproduct")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_output_binding(arg_name="r", type="mysql",
command_text="Products",
connection_string_setting="MySqlConnectionString")
def mysql_output(req: func.HttpRequest, r: func.Out[func.MySqlRow]) \
-> func.HttpResponse:
body = json.loads(req.get_body())
row = func.MySqlRow.from_dict(body)
r.set(row)
return func.HttpResponse(
body=req.get_body(),
status_code=201,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the `MySqlAttribute`

attribute to declare the MySQL bindings on the function, which has the following properties:

| Attribute property | Description |
|---|---|
`CommandText` |
Required. The name of the table that the binding writes to. |
`ConnectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@MySQLOutput`

annotation on parameters whose value would come from Azure Database for MySQL. This annotation supports the following elements:

| Element | Description |
|---|---|
`commandText` |
Required. The name of the table that the binding writes to. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |
`name` |
Required. The unique name of the function binding. |

## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.generic()`

method:

| Property | Description |
|---|---|
`commandText` |
Required. The name of the table that the binding writes to. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |

## Configuration

The following table explains the binding configuration properties that you set in the function.json file:

| Property | Description |
|---|---|
`type` |
Required. Must be set to `Mysql` . |
`direction` |
Required. Must be set to `out` . |
`name` |
Required. The name of the variable that represents the entity in function code. |
`commandText` |
Required. The name of the table that the binding writes to. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database to which data is written. This value isn't the actual connection string and must instead resolve to an environment variable. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

Note

The output binding supports all special characters, including dollar sign ($), backtick (`), hyphen (-), and underscore (_). For more information, see the [MySQL community documentation](https://dev.mysql.com/doc/refman/8.0/en/identifiers.html).

A programming language might define member attributes that contain special characters that it supports. For example, C# has a few limitations for defining [variables](/en-us/dotnet/csharp/fundamentals/coding-style/identifier-names).

Otherwise, you can use `JObject`

for the output binding that covers all special characters. You can follow a [detailed example on GitHub](https://github.com/Azure/azure-functions-mysql-extension/blob/main/samples/samples-csharp/OutputBindingSamples/AddProductJObject.cs).

## Usage

The `CommandText`

property is the name of the table where the data is stored. The name of the connection string setting corresponds to the application setting that contains the connection string to Azure Database for MySQL.

If an exception occurs when a MySQL input binding is executed, the function code won't run. The result might be an error code, such as an HTTP trigger that returns a 500 error code.


---

<!-- DOCUMENTO FUSIONADO: openapi-apim-integrate-visual-studio.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/openapi-apim-integrate-visual-studio -->

# Create serverless APIs in Visual Studio using Azure Functions and API Management integration

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

REST APIs are often described using an OpenAPI definition (formerly known as Swagger) file. This file contains information about operations in an API and how the request and response data for the API should be structured.

In this tutorial, you learn how to:

- Create the code project in Visual Studio
- Install the OpenAPI extension
- Add an HTTP trigger endpoint, which includes OpenAPI definitions
- Test function APIs locally using built-in OpenAPI functionality
- Publish project to a function app in Azure
- Enable API Management integration
- Download the OpenAPI definition file

The serverless function you create provides an API that lets you determine whether an emergency repair on a wind turbine is cost-effective. Since you create both the function app and API Management instance in a consumption tier, your cost for completing this tutorial is minimal.

## Prerequisites

[Visual Studio 2022](https://azure.microsoft.com/downloads/). Make sure you select the**Azure development**workload during installation.An active

[Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing), create a[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create the code project

The Azure Functions project template in Visual Studio creates a project that you can publish to a function app in Azure. You'll also create an HTTP triggered function from a template that supports OpenAPI definition file (formerly Swagger file) generation.

From the Visual Studio menu, select

**File**>**New**>**Project**.In

**Create a new project**, enter*functions*in the search box, choose the**Azure Functions**template, and then select**Next**.In

**Configure your new project**, enter a**Project name**for your project like`TurbineRepair`

, and then select**Create**.For the

**Create a new Azure Functions application**settings, select one of these options for**Functions worker**, where the option you choose depends on your chosen process model:**.NET 8.0 Isolated (Long Term Support)**: Your C# functions run in the isolated worker model, which is recommended. For more information, see the[isolated worker model guide](dotnet-isolated-process-guide).For the rest of the options, use the values in the following table:

Setting Value Description **Function template****Empty**This creates a project without a trigger, which gives you more control over the name of the HTTP triggered function when you add it later. **Use Azurite for runtime storage account (AzureWebJobsStorage)****Selected**You can use the emulator for local development of HTTP trigger functions. Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. **Authorization level****Function**When running in Azure, clients must provide a key when accessing the endpoint. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Select

**Create**to create the function project.

Next, you update the project by installing the OpenAPI extension for Azure Functions, which enables the discoverability of API endpoints in your app.

## Install the OpenAPI extension

To install the OpenAPI extension:

From the

**Tools**menu, select**NuGet Package Manager**>**Package Manager Console**.In the console, run the following

[Install-Package](/en-us/nuget/tools/ps-ref-install-package)command to install the OpenAPI extension:`NuGet\Install-Package Microsoft.Azure.Functions.Worker.Extensions.OpenApi -Version 1.5.1`

You might need to update the

[specific version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenApi), based on your version of .NET.

Now, you can add your HTTP endpoint function.

## Add an HTTP endpoint function

In a C# class library, the bindings used by the function are defined by applying attributes in the code. To create a function with an HTTP trigger:

In

**Solution Explorer**, right-click your project node and select**Add**>**New Azure Function**.Enter

**Turbine.cs**for the class, and then select**Add**.Choose the

**Http trigger**template, set**Authorization level**to**Function**, and then select**Add**. A Turbine.cs code file is added to your project that defines a new function endpoint with an HTTP trigger.

Now you can replace the HTTP trigger template code with code that implements the Turbine function endpoint, along with attributes that use OpenAPI to define endpoint.

## Update the function code

The function uses an HTTP trigger that takes two parameters:

| Parameter name | Description |
|---|---|
hours |
The estimated time to make a turbine repair, up to the nearest whole hour. |
capacity |
The capacity of the turbine, in kilowatts. |

The function then calculates how much a repair costs, and how much revenue the turbine could make in a 24-hour period. Parameters are supplied either in the query string or in the payload of a POST request.

In the Turbine.cs project file, replace the contents of the class generated from the HTTP trigger template with the following code, which depends on your process model:

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.WebJobs.Extensions.OpenApi.Core.Attributes;
using Microsoft.Azure.WebJobs.Extensions.OpenApi.Core.Enums;
using Microsoft.Extensions.Logging;
using Microsoft.OpenApi.Models;
using Newtonsoft.Json;
using System.Net;
namespace TurbineRepair
{
public class Turbine
{
const double revenuePerkW = 0.12;
const double technicianCost = 250;
const double turbineCost = 100;
private readonly ILogger<Turbine> _logger;
public Turbine(ILogger<Turbine> logger)
{
_logger = logger;
}
[Function("TurbineRepair")]
[OpenApiOperation(operationId: "Run")]
[OpenApiSecurity("function_key", SecuritySchemeType.ApiKey, Name = "code", In = OpenApiSecurityLocationType.Query)]
[OpenApiRequestBody("application/json", typeof(RequestBodyModel),
Description = "JSON request body containing { hours, capacity}")]
[OpenApiResponseWithBody(statusCode: HttpStatusCode.OK, contentType: "application/json", bodyType: typeof(string),
Description = "The OK response message containing a JSON result.")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = null)] HttpRequest req,
ILogger log)
{
// Get request body data.
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
dynamic? data = JsonConvert.DeserializeObject(requestBody);
int? capacity = data?.capacity;
int? hours = data?.hours;
// Return bad request if capacity or hours are not passed in
if (capacity == null || hours == null)
{
return new BadRequestObjectResult("Please pass capacity and hours in the request body");
}
// Formulas to calculate revenue and cost
double? revenueOpportunity = capacity * revenuePerkW * 24;
double? costToFix = hours * technicianCost + turbineCost;
string repairTurbine;
if (revenueOpportunity > costToFix)
{
repairTurbine = "Yes";
}
else
{
repairTurbine = "No";
};
return new OkObjectResult(new
{
message = repairTurbine,
revenueOpportunity = "$" + revenueOpportunity,
costToFix = "$" + costToFix
});
}
public class RequestBodyModel
{
public int Hours { get; set; }
public int Capacity { get; set; }
}
}
}
```


This function code returns a message of `Yes`

or `No`

to indicate whether an emergency repair is cost-effective. It also returns the revenue opportunity that the turbine represents and the cost to fix the turbine.

## Run and verify the API locally

When you run the function, the OpenAPI endpoints make it easy to try out the function locally using a generated page. You don't need to provide function access keys when running locally.

Press F5 to start the project. When Functions runtime starts locally, a set of OpenAPI and Swagger endpoints are shown in the output, along with the function endpoint.

In your browser, open the RenderSwaggerUI endpoint, which should look like

`http://localhost:7071/api/swagger/ui`

. A page is rendered, based on your OpenAPI definitions.Select

**POST**>**Try it out**, enter values for`hours`

and`capacity`

either as query parameters or in the JSON request body, and select**Execute**.When you enter integer values like 6 for

`hours`

and 2500 for`capacity`

, you get a JSON response that looks like the following example:

Now you have a function that determines the cost-effectiveness of emergency repairs. Next, you publish your project and API definitions to Azure.

## Publish the project to Azure

Before you can publish your project, you must have a function app in your Azure subscription. Visual Studio publishing creates a function app the first time you publish your project. It can also create an API Management instance that integrates with your function app to expose the TurbineRepair API.

In

**Solution Explorer**, right-click the project and select**Publish**and in**Target**, select**Azure**then**Next**.For the

**Specific target**, choose**Azure Function App (Windows)**to create a function app that runs on Windows, then select**Next**.In

**Function Instance**, choose**+ Create a new Azure Function...**.Create a new instance using the values specified in the following table:

Setting Value Description **Name**Globally unique name Name that uniquely identifies your new function app. Accept this name or enter a new name. Valid characters are: `a-z`

,`0-9`

, and`-`

.**Subscription**Your subscription The Azure subscription to use. Accept this subscription or select a new one from the drop-down list. [Resource group](../azure-resource-manager/management/overview)Name of your resource group The resource group in which to create your function app. Select an existing resource group from the drop-down list or choose **New**to create a new resource group.[Plan Type](functions-scale)Consumption When you publish your project to a function app that runs in a [Consumption plan](consumption-plan), you pay only for executions of your functions app. Other hosting plans incur higher costs.**Location**Location of the service Choose a **Location**in a[region](https://azure.microsoft.com/regions/)near you or other services your functions access.[Azure Storage](storage-considerations)General-purpose storage account An Azure Storage account is required by the Functions runtime. Select **New**to configure a general-purpose storage account. You can also choose an existing account that meets the[storage account requirements](storage-considerations#storage-account-requirements).Select

**Create**to create a function app and its related resources in Azure. Status of resource creation is shown in the lower left of the window.Back in

**Functions instance**, make sure that**Run from package file**is checked. Your function app is deployed using[Zip Deploy](functions-deployment-technologies#zip-deploy)with[Run-From-Package](run-functions-from-deployment-package)mode enabled. This deployment method is recommended for your functions project, since it results in better performance.Select

**Next**, and in**API Management**page, also choose**+ Create an API Management API**.Create an

**API in API Management**by using values in the following table:Setting Value Description **API name**TurbineRepair Name for the API. **Subscription name**Your subscription The Azure subscription to use. Accept this subscription or select a new one from the drop-down list. **Resource group**Name of your resource group Select the same resource group as your function app from the drop-down list. **API Management service**New instance Select **New**to create a new API Management instance in the same location in the serverless tier. Select**OK**to create the instance.Select

**Create**to create the API Management instance with the TurbineRepair API from the function integration.Select

**Finish**and after the publish profile creation process completes, select**Close**.Verify the Publish page now says

**Ready to publish**, and then select**Publish**to deploy the package containing your project files to your new function app in Azure.After the deployment completes, the root URL of the function app in Azure is shown in the

**Publish**tab.

## Get the function access key

In the

**Publish**tab, select the ellipses (**...**) next to**Hosting**and select**Open in Azure portal**. The function app you created is opened in the Azure portal in your default browser.Under

**Functions**on the**Overview page**, select >**Turbine**then select**Function keys**.Under

**Function keys**, select the*copy to clipboard*icon next to the**default**key. You can now set this key you copied in API Management so that it can access the function endpoint.

## Configure API Management

In the function app page, expand

**API**and select**API Management**.If the function app isn't already connected to the new API Management instance, select it under

**API Management**, select**API**>**OpenAPI Document on Azure Functions**, make sure**Import functions**is checked, and select**Link API**. Make sure that only**TurbineRepair**is selected for import and then**Select**.Select

**Go to API Management**at the top of the page, and in the API Management instance, expand**APIs**.Under

**APIs**>**All APIs**, select**OpenAPI Document on Azure Functions**>**POST Run**, then under**Inbound processing**select**Add policy**>**Set query parameters**.Below

**Inbound processing**, in**Set query parameters**, type`code`

for**Name**, select**+Value**, paste in the copied function key, and select**Save**. API Management includes the function key when it passes calls through to the function endpoint.

Now that the function key is set, you can call the `turbine`

API endpoint to verify that it works when hosted in Azure.

## Verify the API in Azure

In the API, select the

**Test**tab and then**POST Run**, enter the following code in the**Request body**>**Raw**, and select**Send**:`{ "hours": "6", "capacity": "2500" }`

As before, you can also provide the same values as query parameters.

Select

**Send**, and then view the**HTTP response**to verify the same results are returned from the API.

## Download the OpenAPI definition

If your API works as expected, you can download the OpenAPI definition for the new hosted APIs from API Management.

-
- Under
**APIs**, select**OpenAPI Document on Azure Functions**, select the ellipses (**...**), and select**Export**.

- Under
Choose the means of API export, including OpenAPI files in various formats. You can also

[export APIs from Azure API Management to the Power Platform](../api-management/export-api-power-platform).

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group.

From the Azure portal menu or **Home** page, select **Resource groups**. Then, on the **Resource groups** page, select the group you created.

On the **myResourceGroup** page, make sure that the listed resources are the ones you want to delete.

Select **Delete resource group**, type the name of your group in the text box to confirm, and then select **Delete**.

## Next steps

You've used Visual Studio 2022 to create a function that's self-documenting because of the [OpenAPI Extension](https://github.com/Azure/azure-functions-openapi-extension) and integrated with API Management. You can now refine the definition in API Management in the portal. You can also [learn more about API Management](../api-management/api-management-key-concepts).


---

<!-- DOCUMENTO FUSIONADO: _functions-reference-powershell__functions-how-to-use-azure-function-app-setting_fbc43b.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-reference-powershell.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-powershell -->

# Azure Functions PowerShell developer guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides details about how you write Azure Functions using PowerShell.

A PowerShell Azure function (function) is represented as a PowerShell script that executes when triggered. Each function script has a related `function.json`

file that defines how the function behaves, such as how it's triggered and its input and output parameters. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

Like other kinds of functions, PowerShell script functions take in parameters that match the names of all the input bindings defined in the `function.json`

file. A `TriggerMetadata`

parameter is also passed that contains additional information on the trigger that started the function.

This article assumes that you have already read the [Azure Functions developer guide](functions-reference). It also assumes that you completed the [Functions quickstart for PowerShell](how-to-create-function-vs-code?pivot=programming-language-powershell) to create your first PowerShell function.

## Folder structure

The required folder structure for a PowerShell project looks like the following. This default can be changed. For more information, see the [scriptFile](#configure-function-scriptfile) section.

```
PSFunctionApp
| - MyFirstFunction
| | - run.ps1
| | - function.json
| - MySecondFunction
| | - run.ps1
| | - function.json
| - Modules
| | - myFirstHelperModule
| | | - myFirstHelperModule.psd1
| | | - myFirstHelperModule.psm1
| | - mySecondHelperModule
| | | - mySecondHelperModule.psd1
| | | - mySecondHelperModule.psm1
| - local.settings.json
| - host.json
| - requirements.psd1
| - profile.ps1
| - extensions.csproj
| - bin
```


At the root of the project, there's a shared [ host.json](functions-host-json) file that can be used to configure the function app. Each function has a folder with its own code file (.ps1) and binding configuration file (

`function.json`

). The name of the function.json file's parent directory is always the name of your function.Certain bindings require the presence of an `extensions.csproj`

file. Binding extensions, required in [version 2.x and later versions](functions-versions) of the Functions runtime, are defined in the `extensions.csproj`

file, with the actual library files in the `bin`

folder. When developing locally, you must [register binding extensions](extension-bundles). When you develop functions in the Azure portal, this registration is done for you.

In PowerShell Function Apps, you might optionally have a `profile.ps1`

which runs when a function app starts to run (otherwise know as a * cold start*). For more information, see

[PowerShell profile](#powershell-profile).

## Defining a PowerShell script as a function

By default, the Functions runtime looks for your function in `run.ps1`

, where `run.ps1`

shares the same parent directory as its corresponding `function.json`

.

Your script is passed several arguments on execution. To handle these parameters, add a `param`

block to the top of your script as in the following example:

```
# $TriggerMetadata is optional here. If you don't need it, you can safely remove it from the param block
param($MyFirstInputBinding, $MySecondInputBinding, $TriggerMetadata)
```


### TriggerMetadata parameter

The `TriggerMetadata`

parameter is used to supply additional information about the trigger. This metadata varies from binding to binding but they all contain a `sys`

property that contains the following data:

```
$TriggerMetadata.sys
```


| Property | Description | Type |
|---|---|---|
| UtcNow | When, in UTC, the function was triggered | DateTime |
| MethodName | The name of the Function that was triggered | string |
| RandGuid | a unique guid to this execution of the function | string |

Every trigger type has a different set of metadata. For example, the `$TriggerMetadata`

for `QueueTrigger`

contains the `InsertionTime`

, `Id`

, `DequeueCount`

, among other things. For more information on the queue trigger's metadata, go to the [official documentation for queue triggers](functions-bindings-storage-queue-trigger#message-metadata). Check the documentation on the [triggers](functions-triggers-bindings) you're working with to see what comes inside the trigger metadata.

## Bindings

In PowerShell, [bindings](functions-triggers-bindings) are configured and defined in a function's function.json. Functions interact with bindings in many ways.

### Reading trigger and input data

Trigger and input bindings are read as parameters passed to your function. Input bindings have a `direction`

set to `in`

in function.json. The `name`

property defined in `function.json`

is the name of the parameter, in the `param`

block. Since PowerShell uses named parameters for binding, the order of the parameters doesn't matter. However, it's a best practice to follow the order of the bindings defined in the `function.json`

.

```
param($MyFirstInputBinding, $MySecondInputBinding)
```


### Writing output data

In Functions, an output binding has a `direction`

set to `out`

in the function.json. You can write to an output binding by using the `Push-OutputBinding`

cmdlet, which is available to the Functions runtime. In all cases, the `name`

property of the binding as defined in `function.json`

corresponds to the `Name`

parameter of the `Push-OutputBinding`

cmdlet.

The following example shows how to call `Push-OutputBinding`

in your function script:

```
param($MyFirstInputBinding, $MySecondInputBinding)
Push-OutputBinding -Name myQueue -Value $myValue
```


You can also pass in a value for a specific binding through the pipeline.

```
param($MyFirstInputBinding, $MySecondInputBinding)
Produce-MyOutputValue | Push-OutputBinding -Name myQueue
```


`Push-OutputBinding`

behaves differently based on the value specified for `-Name`

:

When the specified name can't be resolved to a valid output binding, then an error is thrown.

When the output binding accepts a collection of values, you can call

`Push-OutputBinding`

repeatedly to push multiple values.When the output binding only accepts a singleton value, calling

`Push-OutputBinding`

a second time raises an error.

#### Push-OutputBinding syntax

The following are valid parameters for calling `Push-OutputBinding`

:

| Name | Type | Position | Description |
|---|---|---|---|
`-Name` |
String | 1 | The name of the output binding you want to set. |
`-Value` |
Object | 2 | The value of the output binding you want to set, which is accepted from the pipeline ByValue. |
`-Clobber` |
SwitchParameter | Named | (Optional) When specified, forces the value to be set for a specified output binding. |

The following common parameters are also supported:

`Verbose`

`Debug`

`ErrorAction`

`ErrorVariable`

`WarningAction`

`WarningVariable`

`OutBuffer`

`PipelineVariable`

`OutVariable`


For more information, see [About CommonParameters](/en-us/powershell/module/microsoft.powershell.core/about/about_commonparameters).

#### Push-OutputBinding example: HTTP responses

An HTTP trigger returns a response using an output binding named `response`

. In the following example, the output binding of `response`

has the value of "output #1":

```
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "output #1"
})
```


Because the output is to HTTP, which accepts a singleton value only, an error is thrown when `Push-OutputBinding`

is called a second time.

```
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "output #2"
})
```


For outputs that only accept singleton values, you can use the `-Clobber`

parameter to override the old value instead of trying to add to a collection. The following example assumes that you have already added a value. By using `-Clobber`

, the response from the following example overrides the existing value to return a value of "output #3":

```
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "output #3"
}) -Clobber
```


#### Push-OutputBinding example: Queue output binding

`Push-OutputBinding`

is used to send data to output bindings, such as an [Azure Queue storage output binding](functions-bindings-storage-queue-output). In the following example, the message written to the queue has a value of "output #1":

```
Push-OutputBinding -Name outQueue -Value "output #1"
```


The output binding for a Storage queue accepts multiple output values. In this case, calling the following example after the first writes to the queue a list with two items: "output #1" and "output #2".

```
Push-OutputBinding -Name outQueue -Value "output #2"
```


The following example, when called after the previous two, adds two more values to the output collection:

```
Push-OutputBinding -Name outQueue -Value @("output #3", "output #4")
```


When written to the queue, the message contains these four values: "output #1", "output #2", "output #3", and "output #4".

#### Get-OutputBinding cmdlet

You can use the `Get-OutputBinding`

cmdlet to retrieve the values currently set for your output bindings. This cmdlet retrieves a hashtable that contains the names of the output bindings with their respective values.

The following example uses `Get-OutputBinding`

to return current binding values:

```
Get-OutputBinding
```


```
Name Value
---- -----
MyQueue myData
MyOtherQueue myData
```


`Get-OutputBinding`

also contains a parameter called `-Name`

, which can be used to filter the returned binding, as in the following example:

```
Get-OutputBinding -Name MyQ*
```


```
Name Value
---- -----
MyQueue myData
```


Wildcards (*) are supported in `Get-OutputBinding`

.

## Logging

Logging in PowerShell functions works like regular PowerShell logging. You can use the logging cmdlets to write to each output stream. Each cmdlet maps to a log level used by Functions.

| Functions logging level | Logging cmdlet |
|---|---|
| Error | `Write-Error` |
| Warning | `Write-Warning` |
| Information | `Write-Information` `Write-Host` `Write-Output` Writes to the `Information` log level. |
| Debug | `Write-Debug` |
| Trace | `Write-Progress` `Write-Verbose` |

In addition to these cmdlets, anything written to the pipeline is redirected to the `Information`

log level and displayed with the default PowerShell formatting.

Important

Using the `Write-Verbose`

or `Write-Debug`

cmdlets isn't enough to see verbose and debug level logging. You must also configure the log level threshold, which declares what level of logs you actually care about. To learn more, see [Configure the function app log level](#configure-the-function-app-log-level).

### Configure the function app log level

Azure Functions lets you define the threshold level to make it easy to control the way Functions writes to the logs. To set the threshold for all traces written to the console, use the `logging.logLevel.default`

property in the [ host.json file](functions-host-json). This setting applies to all functions in your function app.

The following example sets the threshold to enable verbose logging for all functions, but sets the threshold to enable debug logging for a function named `MyFunction`

:

```
{
"logging": {
"logLevel": {
"Function.MyFunction": "Debug",
"default": "Trace"
}
}
}
```


For more information, see [host.json reference](functions-host-json).

### Viewing the logs

If your Function App is running in Azure, you can use Application Insights to monitor it. Read [monitoring Azure Functions](functions-monitoring) to learn more about viewing and querying function logs.

If you're running your Function App locally for development, logs default to the file system. To see the logs in the console, set the `AZURE_FUNCTIONS_ENVIRONMENT`

environment variable to `Development`

before starting the Function App.

## Triggers and bindings types

There are many triggers and bindings available to you to use with your function app. For the full list of triggers and bindings, see [Supported bindings](functions-triggers-bindings#supported-bindings).

All triggers and bindings are represented in code as a few real data types:

- Hashtable
- string
- byte[]
- int
- double
- HttpRequestContext
- HttpResponseContext

The first five types in this list are standard .NET types. The last two are used only by the [HttpTrigger trigger](#http-triggers-and-bindings).

Each binding parameter in your functions must be one of these types.

### HTTP triggers and bindings

HTTP and webhook triggers and HTTP output bindings use request and response objects to represent the HTTP messaging.

#### Request object

The request object that is passed into the script is of the type `HttpRequestContext`

, which has the following properties:

| Property | Description | Type |
|---|---|---|
`Body` |
An object that contains the body of the request. `Body` is serialized into the best type based on the data. For example, if the data is JSON, it's passed in as a hashtable. If the data is a string, it's passed in as a string. |
object |
`Headers` |
A dictionary that contains the request headers. | Dictionary<string,string>* |
`Method` |
The HTTP method of the request. | string |
`Params` |
An object that contains the routing parameters of the request. | Dictionary<string,string>* |
`Query` |
An object that contains the query parameters. | Dictionary<string,string>* |
`Url` |
The URL of the request. | string |

* All `Dictionary<string,string>`

keys are case-insensitive.

#### Response object

The response object that you should send back is of the type `HttpResponseContext`

, which has the following properties:

| Property | Description | Type |
|---|---|---|
`Body` |
An object that contains the body of the response. | object |
`ContentType` |
A short hand for setting the content type for the response. | string |
`Headers` |
An object that contains the response headers. | Dictionary or Hashtable |
`StatusCode` |
The HTTP status code of the response. | string or int |

#### Accessing the request and response

When you work with HTTP triggers, you can access the HTTP request the same way you would with any other input binding. It's in the `param`

block.

Use an `HttpResponseContext`

object to return a response, as shown in the following example:

`function.json`


```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"authLevel": "anonymous"
},
{
"type": "http",
"direction": "out",
"name": "Response"
}
]
}
```


`run.ps1`


```
param($req, $TriggerMetadata)
$name = $req.Query.Name
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = "Hello $name!"
})
```


The result of invoking this function would be:

```
irm http://localhost:5001?Name=Functions
Hello Functions!
```


### Type-casting for triggers and bindings

For certain bindings like the blob binding, you're able to specify the type of the parameter.

For example, to have data from Blob storage supplied as a string, add the following type cast to my `param`

block:

```
param([string] $myBlob)
```


## PowerShell profile

In PowerShell, there's the concept of a PowerShell profile. If you're not familiar with PowerShell profiles, see [About profiles](/en-us/powershell/module/microsoft.powershell.core/about/about_profiles).

In PowerShell Functions, the profile script is executed once per PowerShell worker instance in the app when first deployed and after being idled ([cold start](#cold-start). When concurrency is enabled by setting the [PSWorkerInProcConcurrencyUpperBound](#concurrency) value, the profile script is run for each runspace created.

When you create a function app using tools, such as Visual Studio Code and Azure Functions Core Tools, a default `profile.ps1`

is created for you. The default profile is maintained
[on the Core Tools GitHub repository](https://github.com/Azure/azure-functions-core-tools/blob/main/src/Cli/func/StaticResources/profile.ps1)
and contains:

- Automatic MSI authentication to Azure.
- The ability to turn on the Azure PowerShell
`AzureRM`

PowerShell aliases if you would like.

## PowerShell versions

The following table shows the PowerShell versions available to each major version of the Functions runtime, and the .NET version required:

| Functions version | PowerShell version | .NET version |
|---|---|---|
| 4.x | PowerShell 7.4 | .NET 8 |
| 4.x | PowerShell 7.2 (support ending) | .NET 6 |

You can see the current version by printing `$PSVersionTable`

from any function.

To learn more about Azure Functions runtime support policy, refer to this [article](language-support-policy)

Note

Support for PowerShell 7.2 in Azure Functions ends on November 8, 2024. You might have to resolve some breaking changes when upgrading your PowerShell 7.2 functions to run on PowerShell 7.4. Follow this [migration guide](https://github.com/Azure/azure-functions-powershell-worker/wiki/Upgrading-your-Azure-Function-Apps-to-run-on-PowerShell-7.4) to upgrade to PowerShell 7.4.

### Running local on a specific version

When you run PowerShell functions locally, you need to add the setting `"FUNCTIONS_WORKER_RUNTIME_VERSION" : "7.4"`

to the `Values`

array in the local.setting.json file in the project root. When running locally on PowerShell 7.4, your local.settings.json file looks like the following example:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "",
"FUNCTIONS_WORKER_RUNTIME": "powershell",
"FUNCTIONS_WORKER_RUNTIME_VERSION" : "7.4"
}
}
```


Note

In PowerShell Functions, the value "~7" for FUNCTIONS_WORKER_RUNTIME_VERSION refers to "7.0.x". We don't automatically upgrade PowerShell Function apps that have "~7" to "7.4". Going forward, for PowerShell Function Apps, we require that apps specify both the major and minor version they want to target. It's necessary to mention "7.4" if you want to target "7.4.x"

### Changing the PowerShell version

Take these considerations into account before you migrate your PowerShell function app to PowerShell 7.4:

Because the migration might introduce breaking changes in your app, review this

[migration guide](https://github.com/Azure/azure-functions-powershell-worker/wiki/Upgrading-your-Azure-Function-Apps-to-run-on-PowerShell-7.4)before upgrading your app to PowerShell 7.4.Make sure that your function app is running on the latest version of the Functions runtime in Azure, which is version 4.x. For more information, see

[View the current runtime version](set-runtime-version#view-the-current-runtime-version).

Use the following steps to change the PowerShell version used by your function app. You can perform this operation either in the Azure portal or by using PowerShell.

In the

[Azure portal](https://portal.azure.com), browse to your function app.Under

**Settings**, choose**Configuration**. In the**General settings**tab, locate the**PowerShell version**.Choose your desired

**PowerShell Core version**and select**Save**. When warned about the pending restart choose**Continue**. The function app restarts on the chosen PowerShell version.

Note

Azure Functions support for PowerShell 7.4 is generally available (GA). You might see PowerShell 7.4 still indicated as preview in the Azure portal, but this value will be updated soon to reflect the GA status.

The function app restarts after the change is made to the configuration.

## Dependency management

Managing modules in Azure Functions written in PowerShell can be approached in two ways: using the Managed Dependencies feature or including the modules directly in your app content. Each method has its own advantages, and choosing the right one depends on your specific needs.

### Choosing the right module management approach

**Why use the Managed Dependencies feature?**

**Simplified initial installation**: Automatically handles module installation based on your`requirements.psd1`

file.**Auto-upgrades**: Modules are updated automatically, including security fixes, without requiring manual intervention.

**Why include modules in app content?**

**No dependency on the PowerShell Gallery**: Modules are bundled with your app, eliminating external dependencies.**More control**: Avoids the risk of regressions caused by automatic upgrades, giving you full control over which module versions are used.**Compatibility**: Works on Flex Consumption and is recommended for other Linux SKUs.

### Managed Dependencies feature

The Managed Dependencies feature allows Azure Functions to automatically download and manage PowerShell modules specified in the `requirements.psd1`

file. This feature is enabled by default in new PowerShell function apps.

#### Configuring requirements.psd1

To use Managed Dependencies in Azure Functions with PowerShell, you need to configure a `requirements.psd1`

file. This file specifies the modules your function requires, and Azure Functions automatically downloads and updates these modules to ensure that your environment stays up-to-date.

Here's how to set up and configure the `requirements.psd1`

file:

- Create a
`requirements.psd1`

file in the root directory of your Azure Function if one doesn't already exist. - Define the modules and their versions in a PowerShell data structure.

Example `requirements.psd1`

file:

```
@{
'Az' = '9.*' # Specifies the Az module and will use the latest version with major version 9
}
```


### Including modules in app content

For more control over your module versions and to avoid dependencies on external resources, you can include modules directly in your function app’s content.

To include custom modules:

**Create a**at the root of your function app.`Modules`

folder`mkdir ./Modules`

**Copy modules to the**using one of the following methods:`Modules`

folder**If modules are already available locally**:`Copy-Item -Path /mymodules/mycustommodule -Destination ./Modules -Recurse`

**Using**:`Save-Module`

to retrieve from the PowerShell Gallery`Save-Module -Name MyCustomModule -Path ./Modules`

**Using**:`Save-PSResource`

from the`PSResourceGet`

module`Save-PSResource -Name MyCustomModule -Path ./Modules`


Your function app should have the following structure:

```
PSFunctionApp
| - MyFunction
| | - run.ps1
| | - function.json
| - Modules
| | - MyCustomModule
| | - MyOtherCustomModule
| | - MySpecialModule.psm1
| - local.settings.json
| - host.json
| - requirements.psd1
```


When you start your function app, the PowerShell language worker adds this `Modules`

folder to the `$env:PSModulePath`

so that you can rely on module autoloading just as you would in a regular PowerShell script.

Note

If your function app is under source control, you should confirm that all the content in the Modules folder that you add isn't excluded by .gitignore. For example, if one of your modules has a bin folder that is getting excluded, you would want to modify the .gitignore by replacing `bin`

with

```
**/bin/**
!Modules/**
```


### Troubleshooting Managed Dependencies

#### Enabling Managed Dependencies

In order for Managed Dependencies to function, the feature must be enabled in host.json:

```
{
"managedDependency": {
"enabled": true
}
}
```


#### Target specific versions

When targeting specific module versions, it’s important to follow both of the following steps to ensure the correct module version is loaded:

**Specify the module version in**`requirements.psd1`

:`@{ 'Az.Accounts' = '1.9.5' }`

**Add an import statement to**`profile.ps1`

:`Import-Module Az.Accounts -RequiredVersion '1.9.5'`


Following these steps ensures the specified version is loaded when your function starts.

#### Configure specific Managed Dependency interval settings

You can configure how Managed Dependencies are downloaded and installed using the following app settings:

| Setting | Default Value | Description |
|---|---|---|
MDMaxBackgroundUpgradePeriod |
`7.00:00:00` (seven days) |
Controls the background update period for PowerShell function apps. |
MDNewSnapshotCheckPeriod |
`01:00:00` (one hour) |
Specifies how often the PowerShell worker checks for updates. |
MDMinBackgroundUpgradePeriod |
`1.00:00:00` (one day) |
Minimum time between upgrade checks. |

#### Dependency management considerations

**Internet Access**: Managed Dependencies require access to`https://www.powershellgallery.com`

to download modules. Ensure that your environment allows this access, including modifying firewall/VNet rules as needed. The required endpoints are described in[Troubleshooting Cmdlets](/en-us/powershell/gallery/how-to/getting-support/troubleshooting-cmdlets#required-network-endpoints). These endpoints can be added to the allow list, as required.**License Acceptance**: Managed Dependencies doesn't support modules that require license acceptance.**Flex Consumption Plan**: The Managed Dependencies feature isn't supported in the Flex Consumption plan. Use custom modules instead.**Module Locations**: On your local computer, modules are typically installed in one of the globally available folders in your`$env:PSModulePath`

. When running in Azure, the`$env:PSModulePath`

for a PowerShell function app differs from`$env:PSModulePath`

in a regular PowerShell script and contains both the`Modules`

folder uploaded with your app contents and a separate location managed by Managed Dependencies.

## Environment variables

In Functions, [app settings](functions-app-settings), such as service connection strings, are exposed as environment variables during execution. You can access these settings using `$env:NAME_OF_ENV_VAR`

, as shown in the following example:

```
param($myTimer)
Write-Host "PowerShell timer trigger function ran! $(Get-Date)"
Write-Host $env:AzureWebJobsStorage
Write-Host $env:WEBSITE_SITE_NAME
```


There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

When running locally, app settings are read from the [local.settings.json](functions-develop-local#local-settings-file) project file.

## Concurrency

By default, the Functions PowerShell runtime can only process one invocation of a function at a time. However, this concurrency level might not be sufficient in the following situations:

- When you're trying to handle a large number of invocations at the same time.
- When you have functions that invoke other functions inside the same function app.

There are a few concurrency models that you could explore depending on the type of workload:

Increase

`FUNCTIONS_WORKER_PROCESS_COUNT`

. Increasing this setting allows handling function invocations in multiple processes within the same instance, which introduces certain CPU and memory overhead. In general, I/O-bound functions don't suffer from this overhead. For CPU-bound functions, the impact might be significant.Increase the

`PSWorkerInProcConcurrencyUpperBound`

app setting value. Increasing this setting allows creating multiple runspaces within the same process, which significantly reduces CPU and memory overhead.

You set these environment variables in the [app settings](functions-app-settings) of your function app.

Depending on your use case, Durable Functions might significantly improve scalability. To learn more, see [Durable Functions application patterns](durable/durable-functions-overview?tabs=powershell#application-patterns).

Note

You might get "requests are being queued due to no available runspaces" warnings. This message isn't an error. The message is telling you that requests are being queued. They're handled when the previous requests are completed.

### Considerations for using concurrency

PowerShell is a *single_threaded* scripting language by default. However, concurrency can be added by using multiple PowerShell runspaces in the same process. The number of runspaces created, and therefore the number of concurrent threads per worker, is limited by the `PSWorkerInProcConcurrencyUpperBound`

application setting. By default, the number of runspaces is set to 1,000 in version 4.x of the Functions runtime. In versions 3.x and below, the maximum number of runspaces is set to 1. The throughput of your function app is affected by the amount of CPU and memory available in the selected plan.

Azure PowerShell uses some *process-level* contexts and state to help save you from excess typing. However, if you turn on concurrency in your function app and invoke actions that change state, you could end up with race conditions. These race conditions are difficult to debug because one invocation relies on a certain state and the other invocation changed the state.

There's immense value in concurrency with Azure PowerShell, since some operations can take a considerable amount of time. However, you must proceed with caution. If you suspect that you're experiencing a race condition, set the PSWorkerInProcConcurrencyUpperBound app setting to `1`

and instead use [language worker process level isolation](functions-app-settings#functions_worker_process_count) for concurrency.

## Configure function scriptFile

By default, a PowerShell function is executed from `run.ps1`

, a file that shares the same parent directory as its corresponding `function.json`

.

The `scriptFile`

property in the `function.json`

can be used to get a folder structure that looks like the following example:

```
FunctionApp
| - host.json
| - myFunction
| | - function.json
| - lib
| | - PSFunction.ps1
```


In this case, the `function.json`

for `myFunction`

includes a `scriptFile`

property referencing the file with the exported function to run.

```
{
"scriptFile": "../lib/PSFunction.ps1",
"bindings": [
// ...
]
}
```


## Use PowerShell modules by configuring an entryPoint

PowerShell functions in this article are shown with the default `run.ps1`

script file generated by the templates.
However, you can also include your functions in PowerShell modules. You can reference your specific function code in the module by using the `scriptFile`

and `entryPoint`

fields in the function.json` configuration file.

In this case, `entryPoint`

is the name of a function or cmdlet in the PowerShell module referenced in `scriptFile`

.

Consider the following folder structure:

```
FunctionApp
| - host.json
| - myFunction
| | - function.json
| - lib
| | - PSFunction.psm1
```


Where `PSFunction.psm1`

contains:

```
function Invoke-PSTestFunc {
param($InputBinding, $TriggerMetadata)
Push-OutputBinding -Name OutputBinding -Value "output"
}
Export-ModuleMember -Function "Invoke-PSTestFunc"
```


In this example, the configuration for `myFunction`

includes a `scriptFile`

property that references `PSFunction.psm1`

, which is a PowerShell module in another folder. The `entryPoint`

property references the `Invoke-PSTestFunc`

function, which is the entry point in the module.

```
{
"scriptFile": "../lib/PSFunction.psm1",
"entryPoint": "Invoke-PSTestFunc",
"bindings": [
// ...
]
}
```


With this configuration, the `Invoke-PSTestFunc`

gets executed exactly as a `run.ps1`

would.

## Considerations for PowerShell functions

When you work with PowerShell functions, be aware of the considerations in the following sections.

### Cold Start

When developing Azure Functions in the [serverless hosting model](consumption-plan), cold starts are a reality. *Cold start* refers to period of time it takes for your function app to start running to process a request. Cold start happens more frequently in the Consumption plan because your function app gets shut down during periods of inactivity.

#### Avoid using Install-Module

Running `Install-Module`

in your function script on each invocation can cause performance issues. Instead, use `Save-Module`

or `Save-PSResource`

before publishing your function app to bundle the necessary modules.

For more information, see [Dependency management](#dependency-management).

## Next steps

For more information, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: _functions-how-to-use-azure-function-app-settings_functions-bindings-openai-embe_1835db.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-how-to-use-azure-function-app-settings.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-how-to-use-azure-function-app-settings -->

# Manage your function app

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, a function app provides the execution context for your individual functions. Function app behaviors apply to all functions hosted by a given function app. All functions in a function app must be of the same [language](supported-languages).

Individual functions in a function app are deployed together and are scaled together. All functions in the same function app share resources, per instance, as the function app scales.

Connection strings, environment variables, and other application settings are defined separately for each function app. Any data that must be shared between function apps should be stored externally in a persisted store.

## Get started in the Azure portal

Note

Because of limitations on editing function code in the [Azure portal](https://portal.azure.com), you should develop your functions locally and publish your code project to a function app in Azure. For more information, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal)

To view the app settings in your function app, follow these steps:

Sign in to the

[Azure portal](https://portal.azure.com)using your Azure account. Search for your function app and select it.In the left pane of your function app, expand

**Settings**, select**Environment variables**, and then select the**App settings**tab.

## Work with application settings

In addition to the predefined app settings used by Azure Functions, you can create any number of app settings, as required by your function code. For more information, see [App settings reference for Azure Functions](functions-app-settings).

These settings are stored encrypted. For more information, see [App settings security](security-concepts#application-settings).

You can manage app settings from the [Azure portal](functions-how-to-use-azure-function-app-settings?tabs=portal#settings), and by using the [Azure CLI](functions-how-to-use-azure-function-app-settings?tabs=azurecli#settings) and [Azure PowerShell](functions-how-to-use-azure-function-app-settings?tabs=powershell#settings). You can also manage app settings from [Visual Studio Code](functions-develop-vs-code#application-settings-in-azure) and from [Visual Studio](functions-develop-vs#function-app-settings).

Note

Changing application settings causes your function app to restart by default across all hosting plans. For zero-downtime deployments when changing settings, use the [Flex Consumption plan](flex-consumption-plan) with [rolling updates as the site update strategy](flex-consumption-site-updates). For other hosting plans, see [optimize deployments](functions-best-practices#optimize-deployments) for guidance on minimizing downtime.

To view your app settings, see [Get started in the Azure portal](#get-started-in-the-azure-portal).

The **App settings** tab maintains settings that are used by your function app:

### Use application settings

The function app settings values can also be read in your code as environment variables. For more information, see the Environment variables section of these language-specific reference articles:

When you develop a function app locally, you must maintain local copies of these values in the *local.settings.json* project file. For more information, see [Local settings file](functions-develop-local#local-settings-file).

## FTPS deployment settings

Azure Functions supports deploying project code to your function app by using FTPS. Because this deployment method requires you to [sync triggers](functions-deployment-technologies#trigger-syncing), it isn't recommended. To securely transfer project files, always use FTPS and not FTP.

To get the credentials required for FTPS deployment, use one of these methods:

You can get the FTPS publishing credentials in the Azure portal by downloading the publishing profile for your function app.

Important

The publishing profile contains important security credentials. Always secure the downloaded file on your local computer.

To download the publishing profile of your function app:

In the

[Azure portal](https://portal.azure.com), locate the page for your function app, expand**Settings**>**Configuration**in the left column.In the

**Configuration**page, select the**General settings**tab and make sure that**SCM Basic Auth Publishing Credentials**is turned**On**. When this setting is**Off**, you can't use publish profiles, so select**On**and then**Save**.Go back to the function app's

**Overview**page, and then select**Get publish profile**.Save and copy the contents of the file.


- In the file, locate the
`publishProfile`

element with the attribute`publishMethod="FTP"`

. In this element, the`publishUrl`

,`userName`

, and`userPWD`

attributes contain the target URL and credentials for FTPS publishing.

## Hosting plan type

When you create a function app, you also create a hosting plan in which the app runs. A plan can have one or more function apps. The functionality, scaling, and pricing of your functions depend on the type of plan. For more information, see [Azure Functions hosting options](functions-scale).

You can determine the type of plan being used by your function app from the Azure portal, or by using the Azure CLI or Azure PowerShell APIs.

The following values indicate the plan type:

| Plan type | Azure portal | Azure CLI/PowerShell |
|---|---|---|
|

**Consumption**`Dynamic`

[Premium](functions-premium-plan)**ElasticPremium**`ElasticPremium`

[Dedicated (App Service)](dedicated-plan)To determine the type of plan used by your function app, see the

**App Service Plan**in the**Overview**page of the function app in the[Azure portal](https://portal.azure.com).To see the pricing tier, select the name of the

**App Service Plan**, and then select**Settings > Properties**from the left pane.

## Plan migration

You can migrate a function app between a Consumption plan and a Premium plan on Windows.

Tip

We recommend you migrate your Consumption plan app to run in a Flex Consumption plan instead of a Premium plan. Migration to the Flex Consumption plan is the only migration option for a Linux Consumption plan app. For more information, see [Migrate Consumption plan apps to the Flex Consumption plan](migration/migrate-plan-consumption-to-flex).

When migrating between plans, keep in mind the following considerations:

- Direct migration to a Dedicated (App Service) plan isn't supported.
- Migration isn't supported on Linux.
- The source plan and the target plan must be in the same resource group and geographical region. For more information, see
[Move an app to another App Service plan](../app-service/app-service-plan-manage#move-an-app-to-another-app-service-plan). - The specific CLI commands depend on the direction of the migration.
- Downtime in your function executions occurs as the function app is migrated between plans.
- State and other app-specific content is maintained, because the same Azure Files share is used by the app both before and after migration.

You can migrate your plan using these tools:

You can use the [Azure portal](https://portal.azure.com) to switch to a different plan.

Choose the direction of the migration for your app on Windows.

## Development limitations in the Azure portal

The following table shows the operating systems and languages that support in-portal editing:

| Language | Flex Consumption | Premium | Dedicated | Consumption |
|---|---|---|---|---|
| C# | ||||
| Java | ||||
| JavaScript (Node.js) | ✔ | ✔ | Windows-only | |
| Python | Linux-only | Linux-only | Linux-only | |
| PowerShell | Windows-only | Windows-only | Windows-only | |
| TypeScript (Node.js) |

Consider these limitations when you develop your functions in the [Azure portal](https://portal.azure.com):

- In-portal editing is supported only for functions that were created or last modified in the Azure portal.
- In-portal editing is supported only for
[JavaScript](functions-reference-node),[PowerShell](functions-reference-powershell),[Python](functions-reference-python), and[C# script](functions-reference-csharp)(in-process) functions. - In-portal editing isn't currently supported by the
[Flex Consumption plan](flex-consumption-plan#considerations). - The ability to run your apps on Linux in a Consumption plan is planned for retirement. For more information, see
[Azure Functions Consumption plan hosting](consumption-plan). - When you deploy code to a function app from outside the Azure portal, you can no longer edit any of the code for that function app in the portal. In this case, just continue using
[local development](functions-develop-local). - For Python, development with custom modules isn't currently supported in the portal. To add custom modules to your function app, you must
[develop your app locally](functions-develop-local). - For compiled C# functions and Java functions, you can create the function app and related resources in the portal. However, you must create the functions code project locally and then publish it to Azure.

When possible, develop your functions locally and publish your code project to a function app in Azure. For more information, see [Code and test Azure Functions locally](functions-develop-local).

## Manually install extensions

C# class library functions can include the NuGet packages for [binding extensions](functions-bindings-register) directly in the class library project. For other non-.NET languages and C# script, you should [use extension bundles](extension-bundles). If you must manually install extensions, you can do so by [using Azure Functions Core Tools](functions-core-tools-reference#func-extensions-install) locally. If you can't use extension bundles and are only able to work in the portal, you need to use [Advanced Tools (Kudu)](#kudu) to manually create the extensions.csproj file directly in the site. Make sure to first remove the `extensionBundle`

element from the *host.json* file.

This same process works for any other file you need to add to your app.

Important

When possible, don't edit files directly in your function app in Azure. We recommend [downloading your app files locally](deployment-zip-push#download-your-function-app-files), using [Core Tools to install extensions](functions-core-tools-reference#func-extensions-install) and other packages, validating your changes, and then [republishing your app using Core Tools](functions-run-local#publish) or one of the other [supported deployment methods](functions-deployment-technologies#deployment-methods).

The Functions editor built into the Azure portal lets you update your function code and configuration files directly in the portal:

Select your function app, then under

**Functions**, select**Functions**.Choose your function and select

**Code + test**under**Developer**.Choose your file to edit and select

**Save**when you finish.

Files in the root of the app, such as function.proj or extensions.csproj need to be created and edited by using the [Advanced Tools (Kudu)](#kudu):

Select your function app, expand

**Development tools**, and then select**Advanced tools**>**Go**.If prompted, sign in to the Source Control Manager (SCM) site with your Azure credentials.

From the

**Debug console**menu, choose**CMD**.Navigate to

`.\site\wwwroot`

, select the plus (**+**) button at the top, and select**New file**.Give the file a name, such as

`extensions.csproj`

, and then press Enter.Select the edit button next to the new file, add or update code in the file, and then select

**Save**.For a project file like

*extensions.csproj*, run the following command to rebuild the extensions project:`dotnet build extensions.csproj`


## Platform features

Function apps run in the Azure App Service platform, which maintains them. As such, your function apps have access to most of the features of Azure's core web hosting platform. When you use the [Azure portal](https://portal.azure.com), the left pane is where you access the many features of the App Service platform that you can use in your function apps.

The following matrix indicates Azure portal feature support by hosting plan and operating system:

| Feature | Consumption plan | Flex Consumption plan | Premium plan | Dedicated plan |
|---|---|---|---|---|
|

Linux:

**X****X**[App Service editor](#editor)Linux:

**X****X**Linux:

**X**Linux:

**X**[Backups](../app-service/manage-backup)**X****X****X**[Console](#console)Linux:

**X****X**Linux: SSH

Linux: SSH

The rest of this article focuses on the following features in the portal that are useful for your function apps:

For more information about how to work with App Service settings, see [Configure Azure App Service Settings](../app-service/configure-common).

### App Service editor

The App Service editor is an advanced in-portal editor that you can use to modify JSON configuration files and code files alike. Choosing this option launches a separate browser tab with a basic editor. This editor enables you to integrate with the Git repository, run and debug code, and modify function app settings. This editor provides an enhanced development environment for your functions compared with the built-in function editor.

We recommend that you consider developing your functions on your local computer. When you develop locally and publish to Azure, your project files are read-only in the Azure portal. For more information, see [Code and test Azure Functions locally](functions-develop-local).

### Console

The in-portal console is an ideal developer tool when you prefer to interact with your function app from the command line. Common commands include directory and file creation and navigation, as well as executing batch files and scripts.

When developing locally, we recommend using the [Azure Functions Core Tools](functions-run-local) and the [Azure CLI](/en-us/cli/azure/).

### Advanced tools (Kudu)

The advanced tools for App Service (also known as Kudu) provide access to advanced administrative features of your function app. From Kudu, you manage system information, app settings, environment variables, site extensions, HTTP headers, and server variables. You can also launch **Kudu** by browsing to the SCM endpoint for your function app, for example: `https://<myfunctionapp>.scm.azurewebsites.net/`

.

### Deployment Center

When you use a source control solution to develop and maintain your functions code, Deployment Center lets you build and deploy from source control. Your project is built and deployed to Azure when you make updates. For more information, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

### Cross-origin resource sharing

To prevent malicious code execution on the client, modern browsers block requests from web applications to resources running in a separate domain. [Cross-origin resource sharing (CORS)](https://developer.mozilla.org/docs/Web/HTTP/CORS) lets an `Access-Control-Allow-Origin`

header declare which origins are allowed to call endpoints on your function app.

When you configure the **Allowed origins** list for your function app, the `Access-Control-Allow-Origin`

header is automatically added to all responses from HTTP endpoints in your function app.

If there's another domain entry, the wildcard (*) is ignored.

### Authentication

When functions use an HTTP trigger, you can require calls to first be authenticated. App Service supports Microsoft Entra authentication and sign-in with social providers, such as Facebook, Microsoft, and X. For information about configuring specific authentication providers, see [Azure App Service authentication overview](../app-service/overview-authentication-authorization).


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-openai-embeddingsstore-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-embeddingsstore-output -->

# Azure OpenAI embeddings store output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI embeddings store output binding allows you to write files to a semantic document store that can be referenced later in a semantic search.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about semantic ranking in Azure AI Search, see [Semantic ranking in Azure AI Search](/en-us/azure/search/semantic-search-overview).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example writes an HTTP input stream to a semantic document store at the provided URL.

```
public class EmbeddingsRequest
{
[JsonPropertyName("url")]
public string? Url { get; set; }
}
[Function("IngestFile")]
public static async Task<EmbeddingsStoreOutputResponse> IngestFile(
[HttpTrigger(AuthorizationLevel.Function, "post")] HttpRequestData req)
{
using StreamReader reader = new(req.Body);
string request = await reader.ReadToEndAsync();
EmbeddingsStoreOutputResponse badRequestResponse = new()
{
HttpResponse = new BadRequestResult(),
SearchableDocument = new SearchableDocument(string.Empty)
};
if (string.IsNullOrWhiteSpace(request))
{
return badRequestResponse;
}
EmbeddingsRequest? requestBody = JsonSerializer.Deserialize<EmbeddingsRequest>(request);
if (string.IsNullOrWhiteSpace(requestBody?.Url))
{
throw new ArgumentException("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
if (!Uri.TryCreate(requestBody.Url, UriKind.Absolute, out Uri? uri))
{
return badRequestResponse;
}
string filename = Path.GetFileName(uri.AbsolutePath);
return new EmbeddingsStoreOutputResponse
{
HttpResponse = new OkObjectResult(new { status = HttpStatusCode.OK }),
SearchableDocument = new SearchableDocument(filename)
};
}
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

```
@FunctionName("IngestFile")
public HttpResponseMessage ingestFile(
@HttpTrigger(
name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<EmbeddingsRequest> request,
@EmbeddingsStoreOutput(name="EmbeddingsStoreOutput", input = "{url}", inputType = InputType.Url,
storeConnectionName = "AISearchEndpoint", collection = "openai-index",
embeddingsModel = "%EMBEDDING_MODEL_DEPLOYMENT_NAME%") OutputBinding<EmbeddingsStoreOutputResponse> output,
final ExecutionContext context) throws URISyntaxException {
if (request.getBody() == null || request.getBody().getUrl() == null)
{
throw new IllegalArgumentException("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
URI uri = new URI(request.getBody().getUrl());
String filename = Paths.get(uri.getPath()).getFileName().toString();
EmbeddingsStoreOutputResponse embeddingsStoreOutputResponse = new EmbeddingsStoreOutputResponse(new SearchableDocument(filename));
output.setValue(embeddingsStoreOutputResponse);
JSONObject response = new JSONObject();
response.put("status", "success");
response.put("title", filename);
return request.createResponseBuilder(HttpStatus.CREATED)
.header("Content-Type", "application/json")
.body(response)
.build();
}
public class EmbeddingsStoreOutputResponse {
private SearchableDocument searchableDocument;
public EmbeddingsStoreOutputResponse(SearchableDocument searchableDocument) {
this.searchableDocument = searchableDocument;
}
public SearchableDocument getSearchableDocument() {
return searchableDocument;
}
}
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

```
const embeddingsStoreOutput = output.generic({
type: "embeddingsStore",
input: "{url}",
inputType: "url",
connectionName: "AISearchEndpoint",
collection: "openai-index",
embeddingsModel: "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
});
app.http('IngestFile', {
methods: ['POST'],
authLevel: 'function',
extraOutputs: [embeddingsStoreOutput],
handler: async (request, context) => {
let requestBody = await request.json();
if (!requestBody || !requestBody.url) {
throw new Error("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
let uri = requestBody.url;
let url = new URL(uri);
let fileName = path.basename(url.pathname);
context.extraOutputs.set(embeddingsStoreOutput, { title: fileName });
let response = {
status: "success",
title: fileName
};
return { status: 202, jsonBody: response }
}
});
```


```
interface EmbeddingsRequest {
url?: string;
}
const embeddingsStoreOutput = output.generic({
type: "embeddingsStore",
input: "{url}",
inputType: "url",
connectionName: "AISearchEndpoint",
collection: "openai-index",
embeddingsModel: "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
});
app.http('IngestFile', {
methods: ['POST'],
authLevel: 'function',
extraOutputs: [embeddingsStoreOutput],
handler: async (request, context) => {
let requestBody: EmbeddingsRequest | null = await request.json();
if (!requestBody || !requestBody.url) {
throw new Error("Invalid request body. Make sure that you pass in {\"url\": value } as the request body.");
}
let uri = requestBody.url;
let url = new URL(uri);
let fileName = path.basename(url.pathname);
context.extraOutputs.set(embeddingsStoreOutput, { title: fileName });
let response = {
status: "success",
title: fileName
};
return { status: 202, jsonBody: response }
}
});
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

Here's the *function.json* file for ingesting files:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"post"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"name": "EmbeddingsStoreOutput",
"type": "embeddingsStore",
"direction": "out",
"input": "{url}",
"inputType": "Url",
"storeConnectionName": "AISearchEndpoint",
"collection": "openai-index",
"embeddingsModel": "%EMBEDDING_MODEL_DEPLOYMENT_NAME%"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($Request, $TriggerMetadata)
$ErrorActionPreference = 'Stop'
$inputJson = $Request.Body
if (-not $inputJson -or -not $inputJson.Url) {
throw 'Invalid request body. Make sure that you pass in {\"url\": value } as the request body.'
}
$uri = [URI]$inputJson.Url
$filename = [System.IO.Path]::GetFileName($uri.AbsolutePath)
Push-OutputBinding -Name EmbeddingsStoreOutput -Value @{
"title" = $filename
}
$response = @{
"status" = "success"
"title" = $filename
}
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $response
Headers = @{
"Content-Type" = "application/json"
}
})
```


This example writes an HTTP input stream to a semantic document store at the provided URL.

```
@app.function_name("IngestFile")
@app.route(methods=["POST"])
@app.embeddings_store_output(
arg_name="requests",
input="{url}",
input_type="url",
store_connection_name="AISearchEndpoint",
collection="openai-index",
embeddings_model="%EMBEDDING_MODEL_DEPLOYMENT_NAME%",
)
def ingest_file(
req: func.HttpRequest, requests: func.Out[str]
) -> func.HttpResponse:
user_message = req.get_json()
if not user_message:
return func.HttpResponse(
json.dumps({"message": "No message provided"}),
status_code=400,
mimetype="application/json",
)
file_name_with_extension = os.path.basename(user_message["url"])
title = os.path.splitext(file_name_with_extension)[0]
create_request = {"title": title}
requests.set(json.dumps(create_request))
response_json = {"status": "success", "title": title}
return func.HttpResponse(
json.dumps(response_json), status_code=200, mimetype="application/json"
)
```


## Attributes

Apply the `EmbeddingsStoreOutput`

attribute to define an embeddings store output binding, which supports these parameters:

| Parameter | Description |
|---|---|
Input |
The input string for which to generate embeddings. |
AIConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
EmbeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
MaxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
MaxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
InputType |
Optional. Gets the type of the input. |
StoreConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
Collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Annotations

The `EmbeddingsStoreOutput`

annotation enables you to define an embeddings store output binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the output binding. |
input |
The input string for which to generate embeddings. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
maxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
inputType |
Optional. Gets the type of the input. |
storeConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Decorators

During the preview, define the output binding as a `generic_output_binding`

binding of type `semanticSearch`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
input |
The input string for which to generate embeddings. |
ai_connection_name |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddings_model |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
max_overlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
input_type |
Gets the type of the input. |
store_connection_name |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `embeddingsStore` . |
direction |
Must be `out` . |
name |
The name of the output binding. |
input |
The input string for which to generate embeddings. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
maxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
inputType |
Optional. Gets the type of the input. |
storeConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
input |
The input string for which to generate embeddings. |
aiConnectionName |
Optional. Gets or sets the name of the configuration section for AI service connectivity settings. For Azure OpenAI: If specified, looks for "Endpoint" and "Key" values in this configuration section. If not specified or the section doesn't exist, falls back to environment variables: AZURE_OPENAI_ENDPOINT and AZURE_OPENAI_KEY. For user-assigned managed identity authentication, this property is required. For OpenAI service (non-Azure), set the OPENAI_API_KEY environment variable. |
embeddingsModel |
Optional. The ID of the model to use, which defaults to `text-embedding-ada-002` . You shouldn't change the model for an existing database. For more information, see
|
maxChunkLength |
Optional. The maximum number of characters used for chunking the input. For more information, see
|
maxOverlap |
Optional. Gets or sets the maximum number of characters to overlap between chunks. |
inputType |
Optional. Gets the type of the input. |
storeConnectionName |
The name of an app setting or environment variable that contains the connection string value. This property supports binding expressions. |
collection |
The name of the collection or table or index to search. This property supports binding expressions. |

## Usage

See the [Example section](#example) for complete examples.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-storage-queue-triggered-function -->

# Create a function triggered by Azure Queue storage

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to create a function that is triggered when messages are submitted to an Azure Storage queue.

Note

In-portal editing is only supported for JavaScript, PowerShell, and C# Script functions.
Python in-portal editing is supported only when running in the Consumption plan.
To create a C# Script app that supports in-portal editing, you must choose a runtime **Version** that supports the **in-process model**.

When possible, you should [develop your functions locally](functions-develop-local).

To learn more about the limitations on editing function code in the Azure portal, see [Development limitations in the Azure portal](functions-how-to-use-azure-function-app-settings#development-limitations-in-the-azure-portal).

## Prerequisites

- An Azure subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create an Azure Function app

From the Azure portal menu or the

**Home**page, select**Create a resource**.In the

**New**page, select**Function App**.Under

**Select a hosting option**, select**Consumption**>**Select**to create your app in the default**Consumption**plan. In this[serverless](https://azure.microsoft.com/overview/serverless-computing/)hosting option, you pay only for the time your functions run.[Premium plan](functions-premium-plan)also offers dynamic scaling. When you run in an App Service plan, you must manage the[scaling of your function app](functions-scale).On the

**Basics**page, use the function app settings as specified in the following table:Setting Suggested value Description **Subscription**Your subscription The subscription under which you create your new function app. [Resource Group](../azure-resource-manager/management/overview)*myResourceGroup*Name for the new resource group in which you create your function app. You should create a new resource group because there are [known limitations when creating new function apps in an existing resource group](functions-scale#limitations-for-creating-new-function-apps-in-an-existing-resource-group).**Function App name**Globally unique name Name that identifies your new function app. Valid characters are `a-z`

(case insensitive),`0-9`

, and`-`

. To guarantee a unique app name, you can optionally enable**Secure unique default hostname**, which is currently in preview.**Runtime stack**Preferred language Choose a runtime that supports your favorite function programming language. In-portal editing is only available for JavaScript, PowerShell, Python, TypeScript, and C# script.

To create a C# Script app that supports in-portal editing, you must choose a runtime**Version**that supports the**in-process model**.

C# class library and Java functions must be[developed locally](functions-develop-local#local-development-environments).**Version**Version number Choose the version of your installed runtime. **Region**Preferred region Select a [region](https://azure.microsoft.com/regions/)that's near you or near other services that your functions can access.**Operating system**Windows An operating system is preselected for you based on your runtime stack selection, but you can change the setting if necessary. In-portal editing is only supported on Windows. Accept the default options in the remaining tabs, including the default behavior of creating a new storage account on the

**Storage**tab and a new Application Insight instance on the**Monitoring**tab. You can also choose to use an existing storage account or Application Insights instance.Select

**Review + create**to review the app configuration you chose, and then select**Create**to provision and deploy the function app.Select the

**Notifications**icon in the upper-right corner of the portal and watch for the**Deployment succeeded**message.Select

**Go to resource**to view your new function app. You can also select**Pin to dashboard**. Pinning makes it easier to return to this function app resource from your dashboard.

Next, you create a function in the new function app.

## Create a Queue triggered function

In your function app, select

**Overview**, and then select**+ Create**under**Functions**.Under

**Select a template**, scroll down and choose the**Azure Queue Storage trigger**template.In

**Template details**, configure the new trigger with the settings as specified in this table, then select**Create**:Setting Suggested value Description **Job type**Append to app You only see this setting for a Python v2 app. **Name**Unique in your function app Name of this queue triggered function. **Queue name**myqueue-items Name of the queue to connect to in your Storage account. **Storage account connection**AzureWebJobsStorage You can use the storage account connection already being used by your function app, or create a new one. Azure creates the Queue Storage triggered function based on the provided values. Next, you connect to your Azure storage account and create the

**myqueue-items**storage queue.

## Create the queue

Return to the

**Overview**page for your function app, select your**Resource group**, then find and select the storage account in your resource group.In the storage account page, select

**Data storage**>**Queues**>**+ Queue**.In the

**Name**field, type`myqueue-items`

, and then select**Create**.Select the new

**myqueue-items**queue, which you use to test the function by adding a message to the queue.

## Test the function

In a new browser window, return to your function app page and select

**Log stream**, which displays real-time logging for your app.In the

**myqueue-items**queue, select**Add message**, type "Hello World!" in**Message text**, and select**OK**.Go back to your function app logs and verify that the function ran to process the message from the queue.

Back in your storage queue, select

**Refresh**and verify that the message has been processed and is no longer in the queue.

## Clean up resources

Other quickstarts in this collection build upon this quickstart. If you plan to work with subsequent quickstarts, tutorials, or with any of the services you've created in this quickstart, don't clean up the resources.

*Resources* in Azure refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You've created resources to complete these quickstarts. You might be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In the Azure portal, go to the

**Resource group**page.To get to that page from the function app page, select the

**Overview**tab, and then select the link under**Resource group**.To get to that page from the dashboard, select

**Resource groups**, and then select the resource group that you used for this article.In the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**and follow the instructions.Deletion might take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You have created a function that runs when a message is added to a storage queue. For more information about Queue storage triggers, see [Azure Functions Storage queue bindings](functions-bindings-storage-queue).

Now that you have a created your first function, let's add an output binding to the function that writes a message back to another queue.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/event-grid-how-tos -->

# How to work with Event Grid triggers and bindings in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides built-in integration with Azure Event Grid by using [triggers and bindings](functions-triggers-bindings). This article shows you how to configure and locally evaluate your Event Grid trigger and bindings. For more information about Event Grid trigger and output binding definitions and examples, see one of the following reference articles:

[Azure Event Grid bindings Overview](functions-bindings-event-grid)[Azure Event Grid trigger for Azure Functions](functions-bindings-event-grid-trigger)[Azure Event Grid output binding for Azure Functions](functions-bindings-event-grid-output)

## Create an event subscription

To start receiving Event Grid HTTP requests, you need a subscription to events raised by Event Grid. Event subscriptions specify the endpoint URL that invokes the function. When you create an event subscription from your function's **Integration** tab in the [Azure portal](https://portal.azure.com), the URL is supplied for you. When you programmatically create an event subscription or when you create the event subscription from Event Grid, you'll need to provide the endpoint. The endpoint URL contains a system key, which you must obtain from Functions administrator REST APIs.

## Get the webhook endpoint URL

The URL endpoint for your Event Grid triggered function depends on the version of the Functions runtime. The following example shows the version-specific URL pattern:

```
https://{functionappname}.azurewebsites.net/runtime/webhooks/eventgrid?functionName={functionname}&code={systemkey}
```


Note

There is a version of the Blob storage trigger that also uses event subscriptions. The endpoint URL for this kind of Blob storage trigger has a path of `/runtime/webhooks/blobs`

, whereas the path for an Event Grid trigger would be `/runtime/webhooks/EventGrid`

. For a comparison of options for processing blobs, see [Trigger on a blob container](storage-considerations#trigger-on-a-blob-container).

## Obtain the system key

The URL endpoint you construct includes a system key value. The system key is an authorization key, specific to the Event Grid webhook, that must be included in a request to the endpoint URL for an Event Grid trigger. The following section explains how to get the system key.

You can also get the master key for your function app from **Functions** > **App keys** in the portal.

Caution

The master key provides administrator access to your function app. Don't share this key with third parties or distribute it in native client applications.

For more information, see [Work with access keys in Azure Functions](function-keys-how-to).

You can get the system key from your function app by using the following administrator APIs (HTTP GET):

```
http://{functionappname}.azurewebsites.net/admin/host/systemkeys/eventgrid_extension?code={masterkey}
```


This REST API is an administrator API, so it requires your function app [master key](function-keys-how-to). Don't confuse the system key (for invoking an Event Grid trigger function) with the master key (for performing administrative tasks on the function app). When you subscribe to an Event Grid topic, be sure to use the system key.

Here's an example of the response that provides the system key:

```
{
"name": "eventgridextensionconfig_extension",
"value": "{the system key for the function}",
"links": [
{
"rel": "self",
"href": "{the URL for the function, without the system key}"
}
]
}
```


## Create the subscription

You can create an event subscription either from the [Azure portal](https://portal.azure.com) or by using the Azure CLI.

For functions that you develop in the Azure portal with the Event Grid trigger, select **Integration** then choose the **Event Grid Trigger** and select **Create Event Grid subscription**.


When you select this link, the portal opens the **Create Event Subscription** page with the current trigger endpoint already defined.


For more information about how to create subscriptions by using the Azure portal, see [Create custom event - Azure portal](../event-grid/custom-event-quickstart-portal) in the Event Grid documentation.

For more information about how to create a subscription, see [the blob storage quickstart](../storage/blobs/storage-blob-event-quickstart#subscribe-to-your-storage-account) or the other Event Grid quickstarts.

## Local testing with viewer web app

To test an Event Grid trigger locally, you have to get Event Grid HTTP requests delivered from their origin in the cloud to your local machine. One way to do that is by capturing requests online and manually resending them on your local machine:

[Create a viewer web app](#create-a-viewer-web-app)that captures event messages.[Create an Event Grid subscription](#create-an-event-grid-subscription)that sends events to the viewer app.[Generate a request](#generate-a-request)and copy the request body from the viewer app.[Manually post the request](#manually-post-the-request)to the localhost URL of your Event Grid trigger function.

To send an HTTP post request, you need an HTTP test tool. Make sure to choose a tool that keeps your data secure. For more information, see [HTTP test tools](functions-develop-local#http-test-tools).

When you're done testing, you can use the same subscription for production by updating the endpoint. Use the [ az eventgrid event-subscription update](/en-us/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-update) Azure CLI command.

## Create a viewer web app

To simplify capturing event messages, you can deploy a [pre-built web app](https://github.com/Azure-Samples/azure-event-grid-viewer) that displays the event messages. The deployed solution includes an App Service plan, an App Service web app, and source code from GitHub.

Select **Deploy to Azure** to deploy the solution to your subscription. In the Azure portal, provide values for the parameters.

The deployment may take a few minutes to complete. After the deployment has succeeded, view your web app to make sure it's running. In a web browser, navigate to:
`https://<your-site-name>.azurewebsites.net`


You see the site but no events have been posted to it yet.

## Create an Event Grid subscription

Create an Event Grid subscription of the type you want to test, and give it the URL from your web app as the endpoint for event notification. The endpoint for your web app must include the suffix `/api/updates/`

. So, the full URL is `https://<your-site-name>.azurewebsites.net/api/updates`


For information about how to create subscriptions by using the Azure portal, see [Create custom event - Azure portal](../event-grid/custom-event-quickstart-portal) in the Event Grid documentation.

## Generate a request

Trigger an event that will generate HTTP traffic to your web app endpoint. For example, if you created a blob storage subscription, upload or delete a blob. When a request shows up in your web app, copy the request body.

The subscription validation request will be received first; ignore any validation requests, and copy the event request.

## Manually post the request

Run your Event Grid function locally. The `Content-Type`

and `aeg-event-type`

headers are required to be manually set, while and all other values can be left as default.

Use your HTTP test tool to create an HTTP POST request:

Set a

`Content-Type: application/json`

header.Set an

`aeg-event-type: Notification`

header.Paste the RequestBin data into the request body.

Send an HTTP POST request to the endpoint that manually starts the Event Grid trigger.


The `functionName`

parameter must be the name specified in the `FunctionName`

attribute.

The Event Grid trigger function executes and shows logs similar to the following example:

## Next steps

To learn more about Event Grid with Functions, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-continuous-deployment -->

# Continuous deployment for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions enables you to continuously deploy the changes made in a source control repository to a connected function app. This [source control integration](functions-deployment-technologies#source-control) enables a workflow in which a code update triggers build, packaging, and deployment from your project to Azure.

You should always configure continuous deployment for a staging slot and not for the production slot. When you use the production slot, code updates are pushed directly to production without being verified in Azure. Instead, enable continuous deployment to a staging slot, verify updates in the staging slot, and after everything runs correctly you can [swap the staging slot code into production](functions-deployment-slots#swap-slots). If you connect to a production slot, make sure that only production-quality code makes it into the integrated code branch.

Steps in this article show you how to configure continuous code deployments to your function app in Azure by using the Deployment Center in the Azure portal. You can also [configure continuous integration using the Azure CLI](/en-us/cli/azure/functionapp/deployment). These steps can target either a staging or a production slot.

Azure Functions supports these sources for continuous deployment to your app:

Maintain your project code in [Azure Repos](https://azure.microsoft.com/services/devops/repos/), one of the services in Azure DevOps. Supports both Git and Team Foundation Version Control. Used with the [Azure Pipelines build provider](functions-continuous-deployment?tabs=azure-repos*zure-pipelines#build-providers). For more information, see [What is Azure Repos?](/en-us/azure/devops/repos/get-started/what-is-repos).

You can also connect your function app to an external Git repository, but this option requires a manual synchronization. For more information about deployment options, see [Deployment technologies in Azure Functions](functions-deployment-technologies).

Note

Continuous deployment options covered in this article are specific to code-only deployments. For containerized function app deployments, see the **Enable continuous deployment of containers to Azure** section in [Work with containers and Azure Functions](functions-how-to-custom-container).

## Requirements

The unit of deployment for functions in Azure is the function app. For continuous deployment to succeed, the directory structure of your project must be compatible with the basic folder structure that Azure Functions expects. When you create your code project using Azure Functions Core Tools, Visual Studio Code, or Visual Studio, the Azure Functions templates are used to create code projects with the correct directory structure. All functions in a function app are deployed at the same time and in the same package.

After you enable continuous deployment, access to function code in the Azure portal is configured as *read-only* because the *source of truth* is known to reside elsewhere.

Note

The Deployment Center doesn't support enabling continuous deployment for a function app with [inbound network restrictions](functions-networking-options?#inbound-networking-features). You need to instead configure the build provider workflow directly in GitHub or Azure Pipelines. These workflows also require you to use a virtual machine in the same virtual network as the function app as either a [self-hosted agent (Azure Pipelines)](/en-us/azure/devops/pipelines/agents/agents#self-hosted-agents) or a [self-hosted runner (GitHub)](https://docs.github.com/actions/hosting-your-own-runners/managing-self-hosted-runners/about-self-hosted-runners).

## Select a build provider

Building your code project is part of the deployment process. The specific build process depends on your specific language stack, operating system, and hosting plan. Builds can be done locally or remotely, again depending on your specific hosting. For more information, see [Remote build](functions-deployment-technologies#remote-build).

Important

For increased security, consider using a build provider that supports managed identities, including Azure Pipelines and GitHub Actions. The App Service (Kudu) service requires you to [enable basic authentication](#enable-basic-authentication-for-deployments) and work with text-based credentials.

Azure Functions supports these build providers:

Azure Pipelines is one of the services in Azure DevOps and the default build provider for Azure Repos projects. You can also use Azure Pipelines to build projects from GitHub. In Azure Pipelines, there's an [ AzureFunctionApp](/en-us/azure/devops/pipelines/tasks/reference/azure-function-app-v2) task designed specifically for deploying to Azure Functions. This task provides you with control over how the project gets built, packaged, and deployed. Azure Pipelines supports managed identities.

Keep the strengths and limitations of these providers in mind when you enable source control integration. You might need to change your repository source type to take advantage of a specific provider.

## Configure continuous deployment

The [Azure portal](https://portal.azure.com) provides a **Deployment center** for your function apps, which makes it easier to configure continuous deployment. The specific way you configure continuous deployment depends both on the type of source control repository in which your code resides and the [build provider](#build-providers) you choose.

In the [Azure portal](https://portal.azure.com), browse to your function app page and select **Deployment Center** under **Deployment** on the left pane.


Select the **Source** repository type where your project code is being maintained from one of these supported options:

Deployments from Azure Repos that use Azure Pipelines are defined in the [Azure DevOps portal](https://go.microsoft.com/fwlink/?linkid=2245703) and not from your function app. For a step-by-step guide for creating an Azure Pipelines-based deployment from Azure Repos, see [Continuous delivery with Azure Pipelines](functions-how-to-azure-devops).

After deployment finishes, all code from the specified source is deployed to your app. At that point, changes in the deployment source trigger a deployment of those changes to your function app in Azure.

## Enable continuous deployment during app creation

Currently, you can configure continuous deployment from GitHub using GitHub Actions when you create your function app in the Azure portal. You can make this setting on the **Deployment** tab in the **Create Function App** page.

If you want to use a different deployment source or build provider for continuous integration. First, create your function app, and then return to the portal and [set up continuous integration in the Deployment Center](#credentials).

## Enable basic authentication for deployments

In some cases, your function app is created with basic authentication access to the `scm`

endpoint disabled. This blocks publishing by all methods that can't use managed identities to access the `scm`

endpoint. The publishing impacts of having the `scm`

endpoint disabled are detailed in [Deploy without basic authentication](../app-service/configure-basic-auth-disable#deploy-without-basic-authentication).

Important

When you use basic authentication, credentials are sent in clear text. To protect these credentials, you must only access the `scm`

endpoint over an encrypted connection (HTTPS) when using basic authentication. For more information, see [Secure deployment](security-concepts#secure-deployment).

To enable basic authentication to the `scm`

endpoint:

In the

[Azure portal](https://portal.azure.com), go to your function app.On the app's left menu, select

**Settings**>**Configuration**>**General settings**.Set

**SCM Basic Auth Publishing Credentials**to**On**, and then select**Save**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub-trigger -->

# Azure Web PubSub trigger binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use Azure Web PubSub trigger to handle client events from Azure Web PubSub service.

The trigger endpoint pattern would be as follows, which should be set in Web PubSub service side (Portal: settings -> event handler -> URL Template). In the endpoint pattern, the query part `code=<API_KEY>`

is **REQUIRED** when you're using Azure Function App for [security](function-keys-how-to#understand-keys) reasons. The key can be found in **Azure portal**. Find your function app resource and navigate to **Functions** -> **App keys** -> **System keys** -> **webpubsub_extension** after you deploy the function app to Azure. Though, this key isn't needed when you're working with local functions.

```
<Function_App_Url>/runtime/webhooks/webpubsub?code=<API_KEY>
```


## Example

The following sample shows how to handle user events from clients.

```
[Function("Broadcast")]
public static void Run(
[WebPubSubTrigger("<hub>", WebPubSubEventType.User, "message")] UserEventRequest request, ILogger log)
{
log.LogInformation($"Request from: {request.ConnectionContext.UserId}");
log.LogInformation($"Request message data: {request.Data}");
log.LogInformation($"Request message dataType: {request.DataType}");
}
```


`WebPubSubTrigger`

binding also supports return value in synchronize scenarios, for example, system `Connect`

and user event, when server can check and deny the client request, or send messages to the caller directly. `Connect`

event respects `ConnectEventResponse`

and `EventErrorResponse`

, and user event respects `UserEventResponse`

and `EventErrorResponse`

, rest types not matching current scenario is ignored.

```
[Function("Broadcast")]
public static UserEventResponse Run(
[WebPubSubTrigger("<hub>", WebPubSubEventType.User, "message")] UserEventRequest request)
{
return new UserEventResponse("[SYSTEM ACK] Received.");
}
```


```
const { app, trigger } = require('@azure/functions');
const wpsTrigger = trigger.generic({
type: 'webPubSubTrigger',
name: 'request',
hub: '<hub>',
eventName: 'message',
eventType: 'user'
});
app.generic('message', {
trigger: wpsTrigger,
handler: async (request, context) => {
context.log('Request from: ', request.connectionContext.userId);
context.log('Request message data: ', request.data);
context.log('Request message dataType: ', request.dataType);
}
});
```


`WebPubSubTrigger`

binding also supports return value in synchronize scenarios, for example, system `Connect`

and user event, when server can check and deny the client request, or send message to the request client directly. In JavaScript weakly typed language, it's deserialized regarding the object keys. And `EventErrorResponse`

has the highest priority compare to rest objects, that if `code`

is in the return, then it's parsed to `EventErrorResponse`

.

Note

Complete samples for this language are pending.

Note

The Web PubSub extensions for Java isn't supported yet.

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Required - must be set to `webPubSubTrigger` . |
direction |
n/a | Required - must be set to `in` . |
name |
n/a | Required - the variable name used in function code for the parameter that receives the event data. |
hub |
Hub | Required - the value must be set to the name of the Web PubSub hub for the function to be triggered. We support set the value in attribute as higher priority, or it can be set in app settings as a global value. |
eventType |
WebPubSubEventType | Required - the value must be set as the event type of messages for the function to be triggered. The value should be either `user` or `system` . |
eventName |
EventName | Required - the value must be set as the event of messages for the function to be triggered. For `system` event type, the event name should be in `connect` , `connected` , `disconnected` . For user-defined subprotocols, the event name is `message` . For system supported subprotocol `json.webpubsub.azure.v1.` , the event name is user-defined event name. |
clientProtocols |
ClientProtocols | Optional - specifies which client protocol can trigger the Web PubSub trigger functions. The following case-insensitive values are valid: `all` : Accepts all client protocols. Default value. `webPubSub` : Accepts only Web PubSub protocols. `mqtt` : Accepts only MQTT protocols. |
connection |
Connection | Optional - the name of an app settings or setting collection that specifies the upstream Azure Web PubSub service. The value is used for signature validation. And the value is auto resolved with app settings `WebPubSubConnectionString` by default. And `null` means the validation isn't needed and always succeed. |

Important

For optimal security, your function app should use managed identities when connecting to the Web PubSub service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize a managed identity request by using Microsoft Entra ID](../azure-web-pubsub/howto-authorize-from-managed-identity).

## Usages

In C#, `WebPubSubEventRequest`

is type recognized binding parameter, rest parameters are bound by parameter name. Check following table for available parameters and types.

In weakly typed language like JavaScript, `name`

in `function.json`

is used to bind the trigger object regarding following mapping table. And respect `dataType`

in `function.json`

to convert message accordingly when `name`

is set to `data`

as the binding object for trigger input. All the parameters can be read from `context.bindingData.<BindingName>`

and is `JObject`

converted.

| Binding Name | Binding Type | Description | Properties |
|---|---|---|---|
| request | `WebPubSubEventRequest` |
Describes the upstream request | Property differs by different event types, including derived classes `ConnectEventRequest` , `MqttConnectEventRequest` , `ConnectedEventRequest` , `MqttConnectedEventRequest` , `UserEventRequest` , `DisconnectedEventRequest` , and `MqttDisconnectedEventRequest` . |
| connectionContext | `WebPubSubConnectionContext` |
Common request information | EventType, EventName, Hub, ConnectionId, UserId, Headers, Origin, Signature, States |
| data | `BinaryData` ,`string` ,`Stream` ,`byte[]` |
Request message data from client in user `message` event |
- |
| dataType | `WebPubSubDataType` |
Request message dataType, which supports `binary` , `text` , `json` |
- |
| claims | `IDictionary<string, string[]>` |
User Claims in system `connect` request |
- |
| query | `IDictionary<string, string[]>` |
User query in system `connect` request |
- |
| subprotocols | `IList<string>` |
Available subprotocols in system `connect` request |
- |
| clientCertificates | `IList<ClientCertificate>` |
A list of certificate thumbprint from clients in system `connect` request |
- |
| reason | `string` |
Reason in system `disconnected` request |
- |

Important

In C#, multiple types supported parameter **MUST** be put in the first, i.e. `request`

or `data`

that other than the default `BinaryData`

type to make the function binding correctly.

### Return response

`WebPubSubTrigger`

respects customer returned response for synchronous events of `connect`

and user event. Only matched response is sent back to service, otherwise, it's ignored. Besides, `WebPubSubTrigger`

return object supports users to `SetState()`

and `ClearStates()`

to manage the metadata for the connection. And the extension merges the results from return value with the original ones from request `WebPubSubConnectionContext.States`

. Value in existing key is overwrite and value in new key is added.

| Return Type | Description | Properties |
|---|---|---|
`ConnectEventResponse` |

`connect`

event`UserEventResponse`

`EventErrorResponse`

`*WebPubSubEventResponse`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/configure-monitoring -->

# How to configure monitoring for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Application Insights to better enable you to monitor your function apps. Application Insights, a feature of Azure Monitor, is an extensible Application Performance Management (APM) service that collects data generated by your function app, including information your app writes to logs. Application Insights integration is typically enabled when your function app is created. If your app doesn't have the instrumentation key set, you must first [enable Application Insights integration](#enable-application-insights-integration).

You can use Application Insights without any custom configuration. However, the default configuration can result in high volumes of data. If you're using a Visual Studio Azure subscription, you might hit your data cap for Application Insights. For information about Application Insights costs, see [Application Insights billing](/en-us/azure/azure-monitor/logs/cost-logs#application-insights-billing). For more information, see [Solutions with high-volume of telemetry](#solutions-with-high-volume-of-telemetry).

In this article, you learn how to configure and customize the data that your functions send to Application Insights. You can set common logging configurations in the * host.json* file. By default, these settings also govern custom logs emitted by your code. However, in some cases this behavior can be disabled in favor of options that give you more control over logging. For more information, see

[Custom application logs](#custom-application-logs).

Note

You can use specially configured application settings to represent specific settings in a *host.json* file for a particular environment. Doing so lets you effectively change *host.json* settings without needing to republish the *host.json* file in your project. For more information, see [Override host.json values](functions-host-json#override-hostjson-values).

## Custom application logs

By default, custom application logs you write are sent to the Functions host, which then sends them to Application Insights under the [Worker category](#configure-categories). Some language stacks allow you to instead send the logs directly to Application Insights, which gives you full control over how logs you write are emitted. In this case, the logging pipeline changes from `worker -> Functions host -> Application Insights`

to `worker -> Application Insights`

.

The following table summarizes the configuration options available for each stack:

| Language stack | Where to configure custom logs |
|---|---|
| .NET (in-process model) | `host.json` |
| .NET (isolated model) | Default (send custom logs to the Functions host): `host.json` To send logs directly to Application Insights, see:
|
| Node.js | `host.json` |
| Python | `host.json` |
| Java | Default (send custom logs to the Functions host): `host.json` To send logs directly to Application Insights, see:
|
| PowerShell | `host.json` |

When you configure custom application logs to be sent directly, the host no longer emits them, and `host.json`

no longer controls their behavior. Similarly, the options exposed by each stack apply only to custom logs, and they don't change the behavior of the other runtime logs described in this article. In this case, to control the behavior of all logs, you might need to make changes in both configurations.

## Configure categories

The Azure Functions logger includes a *category* for every log. The category indicates which part of the runtime code or your function code wrote the log. Categories differ between version 1.x and later versions.

Category names are assigned differently in Functions compared to other .NET frameworks. For example, when you use `ILogger<T>`

in ASP.NET, the category is the name of the generic type. C# functions also use `ILogger<T>`

, but instead of setting the generic type name as a category, the runtime assigns categories based on the source. For example:

- Entries related to running a function are assigned a category of
`Function.<FUNCTION_NAME>`

. - Entries created by user code inside the function, such as when calling
`logger.LogInformation()`

, are assigned a category of`Function.<FUNCTION_NAME>.User`

.

The following table describes the main categories of logs that the runtime creates:

| Category | Table | Description |
|---|---|---|
`Function` |
traces |
Includes function started and completed logs for all function runs. For successful runs, these logs are at the `Information` level. Exceptions are logged at the `Error` level. The runtime also creates `Warning` level logs, such as when queue messages are sent to the
|
`Function.<YOUR_FUNCTION_NAME>` |
dependencies |
Dependency data is automatically collected for some services. For successful runs, these logs are at the `Information` level. For more information, see
`Error` level. The runtime also creates `Warning` level logs, such as when queue messages are sent to the
|
`Function.<YOUR_FUNCTION_NAME>` |
customMetricscustomEvents |
C# and JavaScript SDKs lets you collect custom metrics and log custom events. For more information, see
|

`Function.<YOUR_FUNCTION_NAME>`

**traces**`Information`

level. Exceptions are logged at the `Error`

level. The runtime also creates `Warning`

level logs, such as when queue messages are sent to the [poison queue](functions-bindings-storage-queue-trigger#poison-messages).`Function.<YOUR_FUNCTION_NAME>.User`

**traces**[Writing to logs](functions-monitoring#writing-to-logs).`Host.Aggregator`

**customMetrics**[configurable](#configure-the-aggregator)period of time. The default period is 30 seconds or 1,000 results, whichever comes first. Examples are the number of runs, success rate, and duration. All of these logs are written at the`Information`

level. If you filter at `Warning`

or higher, you don't see any of this data.`Host.Results`

**requests**`Information`

level. If you filter at `Warning`

or higher, you don't see any of this data.`Microsoft`

**traces**`Worker`

**traces**`Microsoft.*`

category, such as `Microsoft.Azure.WebJobs.Script.Workers.Rpc.RpcFunctionInvocationDispatcher`

. These logs are written at the `Information`

level.Note

For .NET class library functions, these categories assume you're using `ILogger`

and not `ILogger<T>`

. For more information, see the [Functions ILogger documentation](functions-dotnet-class-library#ilogger).

The **Table** column indicates to which table in Application Insights the log is written.

## Configure log levels

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

For each category, you indicate the minimum log level to send. The *host.json* settings vary depending on the [Functions runtime version](functions-versions).

The following examples define logging based on the following rules:

- The default logging level is set to
`Warning`

to prevent[excessive logging](#solutions-with-high-volume-of-telemetry)for unanticipated categories. `Host.Aggregator`

and`Host.Results`

are set to lower levels. Setting logging levels too high (especially higher than`Information`

) can result in loss of metrics and performance data.- Logging for function runs is set to
`Information`

. If necessary, you can[override](functions-host-json#override-hostjson-values)this setting in local development to`Debug`

or`Trace`

.

```
{
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"default": "Warning",
"Host.Aggregator": "Trace",
"Host.Results": "Information",
"Function": "Information"
}
}
}
```


If * host.json* includes multiple logs that start with the same string, the more defined logs ones are matched first. Consider the following example that logs everything in the runtime, except

`Host.Aggregator`

, at the `Error`

level:```
{
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"default": "Information",
"Host": "Error",
"Function": "Error",
"Host.Aggregator": "Information"
}
}
}
```


You can use a log level setting of `None`

to prevent any logs from being written for a category.

Caution

Azure Functions integrates with Application Insights by storing telemetry events in Application Insights tables. If you set a category log level to any value different from `Information`

, it prevents the telemetry from flowing to those tables, and you won't be able to see related data in the **Application Insights** and **Function Monitor** tabs.

For example, for the previous samples:

- If you set the
`Host.Results`

category to the`Error`

log level, Azure gathers only host execution telemetry events in the`requests`

table for failed function executions, preventing the display of host execution details of successful executions in both the**Application Insights**and**Function Monitor**tabs. - If you set the
`Function`

category to the`Error`

log level, it stops gathering function telemetry data related to`dependencies`

,`customMetrics`

, and`customEvents`

for all the functions, preventing you from viewing any of this data in Application Insights. Azure gathers only`traces`

logged at the`Error`

level.

In both cases, Azure continues to collect errors and exceptions data in the **Application Insights** and **Function Monitor** tabs. For more information, see [Solutions with high-volume of telemetry](#solutions-with-high-volume-of-telemetry).

## Configure the aggregator

As noted in the previous section, the runtime aggregates data about function executions over a period of time. The default period is 30 seconds or 1,000 runs, whichever comes first. You can configure this setting in the * host.json* file. For example:

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


## Configure sampling

Application Insights has a [sampling](/en-us/azure/azure-monitor/app/sampling) feature that can protect you from producing too much telemetry data on completed executions at times of peak load. When the rate of incoming executions exceeds a specified threshold, Application Insights starts to randomly ignore some of the incoming executions. The default setting for maximum number of executions per second is 20 (five in version 1.x). You can configure sampling in [ host.json](functions-host-json#applicationinsights). Here's an example:

```
{
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 20,
"excludedTypes": "Request;Exception"
}
}
}
}
```


You can exclude certain types of telemetry from sampling. In this example, data of type `Request`

and `Exception`

is excluded from sampling. It ensures that *all* function executions (requests) and exceptions are logged while other types of telemetry remain subject to sampling.

If your project uses a dependency on the Application Insights SDK to do manual telemetry tracking, you might experience unusual behavior if your sampling configuration differs from the sampling configuration in your function app. In such cases, use the same sampling configuration as the function app. For more information, see [Sampling in Application Insights](/en-us/azure/azure-monitor/app/sampling).

## Enable SQL query collection

Application Insights automatically collects data on dependencies for HTTP requests, database calls, and for several bindings. For more information, see [Dependencies](functions-monitoring#dependencies). For SQL calls, the name of the server and database is always collected and stored, but SQL query text isn't collected by default. You can use `dependencyTrackingOptions.enableSqlCommandTextInstrumentation`

to enable SQL query text logging by using the following settings (at a minimum) in your [host.json file](functions-host-json#applicationinsightsdependencytrackingoptions):

```
"logging": {
"applicationInsights": {
"enableDependencyTracking": true,
"dependencyTrackingOptions": {
"enableSqlCommandTextInstrumentation": true
}
}
}
```


For more information, see [Advanced SQL tracking to get full SQL query](/en-us/azure/azure-monitor/app/asp-net-dependencies#advanced-sql-tracking-to-get-full-sql-query).

## Configure scale controller logs

*This feature is in preview.*

You can have the [Azure Functions scale controller](event-driven-scaling#runtime-scaling) emit logs to either Application Insights or to Blob storage to better understand the decisions the scale controller is making for your function app.

To enable this feature, add an application setting named `SCALE_CONTROLLER_LOGGING_ENABLED`

to your function app settings. The following value of the setting must be in the format `<DESTINATION>:<VERBOSITY>`

. For more information, see the following table:

| Property | Description |
|---|---|
`<DESTINATION>` |
The destination to which logs are sent. Valid values are `AppInsights` and `Blob` .When you use `AppInsights` , ensure that the
When you set the destination to `Blob` , logs are created in a blob container named `azure-functions-scale-controller` in the default storage account set in the `AzureWebJobsStorage` application setting. |
`<VERBOSITY>` |
Specifies the level of logging. Supported values are `None` , `Warning` , and `Verbose` .When set to `Verbose` , the scale controller logs a reason for every change in the worker count, and information about the triggers that factor into those decisions. Verbose logs include trigger warnings and the hashes used by the triggers before and after the scale controller runs. |

Tip

Keep in mind that while you leave scale controller logging enabled, it impacts the [potential costs of monitoring your function app](functions-monitoring#application-insights-pricing-and-limits). Consider enabling logging until you collect enough data to understand how the scale controller is behaving, and then disabling it.

For example, the following Azure CLI command turns on verbose logging from the scale controller to Application Insights:

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--settings SCALE_CONTROLLER_LOGGING_ENABLED=AppInsights:Verbose
```


In this example, replace `<FUNCTION_APP_NAME>`

and `<RESOURCE_GROUP_NAME>`

with the name of your function app and the resource group name, respectively.

The following Azure CLI command disables logging by setting the verbosity to `None`

:

```
az functionapp config appsettings set --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--settings SCALE_CONTROLLER_LOGGING_ENABLED=AppInsights:None
```


You can also disable logging by removing the `SCALE_CONTROLLER_LOGGING_ENABLED`

setting using the following Azure CLI command:

```
az functionapp config appsettings delete --name <FUNCTION_APP_NAME> \
--resource-group <RESOURCE_GROUP_NAME> \
--setting-names SCALE_CONTROLLER_LOGGING_ENABLED
```


With scale controller logging enabled, you're now able to [query your scale controller logs](analyze-telemetry-data#query-scale-controller-logs).

## Enable Application Insights integration

For a function app to send data to Application Insights, it needs to connect to the Application Insights resource using **only one** of these application settings:

| Setting name | Description |
|---|---|
`APPLICATIONINSIGHTS_CONNECTION_STRING` |
This setting is recommended and is required when your Application Insights instance runs in a sovereign cloud. The connection string supports other
|

`APPINSIGHTS_INSTRUMENTATIONKEY`

When you create your function app in the [Azure portal](functions-get-started) from the command line by using [Azure Functions Core Tools](how-to-create-function-azure-cli?pivots=programming-language-csharp) or [Visual Studio Code](how-to-create-function-vs-code?pivot=programming-language-csharp), Application Insights integration is enabled by default. The Application Insights resource has the same name as your function app, and is created either in the same region or in the nearest region.

### Require Microsoft Entra authentication

You can use the [ APPLICATIONINSIGHTS_AUTHENTICATION_STRING](functions-app-settings#applicationinsights_authentication_string) setting to enable connections to Application Insights using Microsoft Entra authentication. This creates a consistent authentication experience across all Application Insights pipelines, including Profiler and Snapshot Debugger, as well as from the Functions host and language-specific agents.

Note

There's currently no Microsoft Entra ID authentication support for local development.

When Ingesting data in a sovereign cloud, Microsoft Entra ID authentication isn't available when using the Application Insights SDK. OpenTelemetry-based data collection supports Microsoft Entra ID authentication across all cloud environments, including sovereign clouds.

The value contains either `Authorization=AAD`

for a system-assigned managed identity or `ClientId=<YOUR_CLIENT_ID>;Authorization=AAD`

for a user-assigned managed identity. The managed identity must already be available to the function app, with an assigned role equivalent to [Monitoring Metrics Publisher](/en-us/azure/role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher). For more information, see [Microsoft Entra authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication).

The [ APPLICATIONINSIGHTS_CONNECTION_STRING](functions-app-settings#applicationinsights_connection_string) setting is still required.

Note

When using `APPLICATIONINSIGHTS_AUTHENTICATION_STRING`

to connect to Application Insights using Microsoft Entra authentication, you should also [Disable local authentication for Application Insights](/en-us/azure/azure-monitor/app/azure-ad-authentication#disable-local-authentication). This configuration requires Microsoft Entra authentication in order for telemetry to be ingested into your workspace.

### New function app in the portal

To review the Application Insights resource being created, select it to expand the **Application Insights** window. You can change the **New resource name** or select a different **Location** in an [Azure geography](https://azure.microsoft.com/global-infrastructure/geographies/) where you want to store your data.


When you select **Create**, an Application Insights resource is created with your function app, which has the `APPLICATIONINSIGHTS_CONNECTION_STRING`

set in application settings. Everything is ready to go.

### Add to an existing function app

If an Application Insights resource wasn't created with your function app, use the following steps to create the resource. You can then add the connection string from that resource as an [application setting](functions-how-to-use-azure-function-app-settings#settings) in your function app.

In the

[Azure portal](https://portal.azure.com), search for and select**function app**, and then select your function app.Select the

**Application Insights is not configured**banner at the top of the window. If you don't see this banner, then your app might already have Application Insights enabled.Expand

**Change your resource**and create an Application Insights resource by using the settings specified in the following table:Setting Suggested value Description **New resource name**Unique app name It's easiest to use the same name as your function app, which must be unique in your subscription. **Location**West Europe If possible, use the same [region](https://azure.microsoft.com/regions/)as your function app, or the one that's close to that region.Select

**Apply**.The Application Insights resource is created in the same resource group and subscription as your function app. After the resource is created, close the

**Application Insights**window.In your function app, expand

**Settings**, and then select**Environment variables**. In the**App settings**tab, if you see an app setting named`APPLICATIONINSIGHTS_CONNECTION_STRING`

, Application Insights integration is enabled for your function app running in Azure. If this setting doesn't exist, add it by using your Application Insights connection string as the value.

Note

Older function apps might use `APPINSIGHTS_INSTRUMENTATIONKEY`

instead of `APPLICATIONINSIGHTS_CONNECTION_STRING`

. When possible, update your app to use the connection string instead of the instrumentation key.

## Disable built-in logging

Early versions of Functions used built-in monitoring, which is no longer recommended. When you enable Application Insights, disable the built-in logging that uses Azure Storage. The built-in logging is useful for testing with light workloads, but isn't intended for high-load production use. For production monitoring, we recommend Application Insights. If you use built-in logging in production, the logging record might be incomplete because of throttling on Azure Storage.

To disable built-in logging, delete the `AzureWebJobsDashboard`

app setting. For more information about how to delete app settings in the Azure portal, see the **Application settings** section of [How to manage a function app](functions-how-to-use-azure-function-app-settings#settings). Before you delete the app setting, ensure that no existing functions in the same function app use the setting for Azure Storage triggers or bindings.

## Solutions with high volume of telemetry

Function apps are an essential part of solutions that can cause high volumes of telemetry, such as IoT solutions, rapid event driven solutions, high load financial systems, and integration systems. In this case, you should consider extra configuration to reduce costs while maintaining observability.

The generated telemetry can be consumed in real-time dashboards, alerting, detailed diagnostics, and so on. Depending on how the generated telemetry is consumed, you need to define a strategy to reduce the volume of data generated. This strategy allows you to properly monitor, operate, and diagnose your function apps in production. Consider the following options:

**Use the correct table plan**:[Table plans](/en-us/azure/azure-monitor/logs/data-platform-logs#table-plans)help you manage data costs by controlling how often you use the data in a table and the kind of analysis you need to perform. To reduce costs, you can choose the`Basic`

plan, which does lack some features available in the`Analytics`

plan.**Use sampling**: As mentioned[previously](#configure-sampling), sampling helps to dramatically reduce the volume of telemetry events ingested while maintaining a statistically correct analysis. It could happen that even using sampling you still get a high volume of telemetry. Inspect the options that[adaptive sampling](/en-us/azure/azure-monitor/app/sampling#configuring-adaptive-sampling-for-aspnet-applications)provides to you. For example, set the`maxTelemetryItemsPerSecond`

to a value that balances the volume generated with your monitoring needs. Keep in mind that the telemetry sampling is applied per host executing your function app.**Default log level**: Use`Warning`

or`Error`

as the default value for all telemetry categories. Later, you can decide which[categories](#configure-categories)you want to set at the`Information`

level, so that you can monitor and diagnose your functions properly.**Tune your functions telemetry**: With the default log level set to`Error`

or`Warning`

, no detailed information from each function is gathered (dependencies, custom metrics, custom events, and traces). For those functions that are key for production monitoring, define an explicit entry for the`Function.<YOUR_FUNCTION_NAME>`

category and set it to`Information`

, so that you can gather detailed information. To avoid gathering[user-generated logs](functions-monitoring#writing-to-logs)at the`Information`

level, set the`Function.<YOUR_FUNCTION_NAME>.User`

category to the`Error`

or`Warning`

log level.**Host.Aggregator category**: As described in[configure categories](#configure-categories), this category provides aggregated information of function invocations. The information from this category is gathered in the Application Insights`customMetrics`

table, and is shown in the function**Overview**tab in the Azure portal. Depending on how you configure the aggregator, consider that there can be a delay, determined by the`flushTimeout`

setting, in the telemetry gathered. If you set this category to a value different from`Information`

, you stop gathering the data in the`customMetrics`

table and don't display metrics in the function**Overview**tab.The following screenshot shows

`Host.Aggregator`

telemetry data displayed in the function**Overview**tab:The following screenshot shows

`Host.Aggregator`

telemetry data in Application Insights`customMetrics`

table:**Host.Results category**: As described in[configure categories](#configure-categories), this category provides the runtime-generated logs indicating the success or failure of a function invocation. The information from this category is gathered in the Application Insights`requests`

table, and is shown in the function**Monitor**tab and in different Application Insights dashboards (Performance, Failures, and so on). If you set this category to a value different than`Information`

, you gather only telemetry generated at the log level defined (or higher). For example, setting it to`error`

results in tracking requests data only for failed executions.The following screenshot shows the

`Host.Results`

telemetry data displayed in the function**Monitor**tab:The following screenshot shows

`Host.Results`

telemetry data displayed in Application Insights Performance dashboard:**Host.Aggregator vs Host.Results**: Both categories provide good insights about function executions. If needed, you can remove the detailed information from one of these categories, so that you can use the other for monitoring and alerting. Here's a sample:

```
{
"version": "2.0",
"logging": {
"logLevel": {
"default": "Warning",
"Function": "Error",
"Host.Aggregator": "Error",
"Host.Results": "Information",
"Function.Function1": "Information",
"Function.Function1.User": "Error"
},
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond": 1,
"excludedTypes": "Exception"
}
}
}
}
```


With this configuration:

The default value for all functions and telemetry categories is set to

`Warning`

(including Microsoft and Worker categories). So, by default, all errors and warnings generated by runtime and custom logging are gathered.The

`Function`

category log level is set to`Error`

, so for all functions, by default, only exceptions and error logs are gathered. Dependencies, user-generated metrics, and user-generated events are skipped.For the

`Host.Aggregator`

category, as it's set to the`Error`

log level, aggregated information from function invocations isn't gathered in the`customMetrics`

Application Insights table, and information about executions counts (total, successful, and failed) aren't shown in the function overview dashboard.For the

`Host.Results`

category, all the host execution information is gathered in the`requests`

Application Insights table. All the invocations results are shown in the function Monitor dashboard and in Application Insights dashboards.For the function called

`Function1`

, we set the log level to`Information`

. So, for this concrete function, all the telemetry is gathered (dependency, custom metrics, and custom events). For the same function, we set the`Function1.User`

category (user-generated traces) to`Error`

, so only custom error logging is gathered.Note

Configuration per function isn't supported in v1.x of the Functions runtime.

Sampling is configured to send one telemetry item per second per type, excluding the exceptions. This sampling happens for each server host running our function app. So, if we have four instances, this configuration emits four telemetry items per second per type and all the exceptions that might occur.

Note

Metric counts such as request rate and exception rate are adjusted to compensate for the sampling rate, so that they show approximately correct values in Metric Explorer.


Tip

Experiment with different configurations to ensure that you cover your requirements for logging, monitoring, and alerting. Also, ensure that you have detailed diagnostics in case of unexpected errors or malfunctioning.

## Overriding monitoring configuration at runtime

Finally, there could be situations where you need to quickly change the logging behavior of a certain category in production, and you don't want to make a whole deployment just for a change in the *host.json* file. For such cases, you can override the [host.json values](functions-host-json#override-hostjson-values).

To configure these values at App settings level (and avoid redeployment on just *host.json* changes), you should override specific `host.json`

values by creating an equivalent value as an application setting. When the runtime finds an application setting in the format `AzureFunctionsJobHost__path__to__setting`

, it overrides the equivalent `host.json`

setting located at `path.to.setting`

in the JSON. When expressed as an application setting, a double underscore (`__`

) replaces the dot (`.`

) used to indicate JSON hierarchy. For example, you can use the following app settings to configure individual function log levels in `host.json`

.

| Host.json path | App setting |
|---|---|
| logging.logLevel.default | AzureFunctionsJobHost__logging__logLevel__default |
| logging.logLevel.Host.Aggregator | AzureFunctionsJobHost__logging__logLevel__Host.Aggregator |
| logging.logLevel.Function | AzureFunctionsJobHost__logging__logLevel__Function |
| logging.logLevel.Function.Function1 | AzureFunctionsJobHost__logging__logLevel__Function.Function1 |
| logging.logLevel.Function.Function1.User | AzureFunctionsJobHost__logging__logLevel__Function.Function1.User |

You can override the settings directly at the Azure portal Function App Configuration pane or by using an Azure CLI or PowerShell script.

```
az functionapp config appsettings set --name MyFunctionApp --resource-group MyResourceGroup --settings "AzureFunctionsJobHost__logging__logLevel__Host.Aggregator=Information"
```


Note

Overriding the `host.json`

through changing app settings will restart your function app.
App settings that contain a period aren't supported when running on Linux in an Elastic Premium plan or a Dedicated (App Service) plan. In these hosting environments, you should continue to use the *host.json* file.

## Monitor function apps using Health check

You can use the Health Check feature to monitor function apps on the Premium (Elastic Premium) and Dedicated (App Service) plans. Health check isn't an option for the Flex Consumption and Consumption plans. To learn how to configure it, see [Monitor App Service instances using Health check](../app-service/monitor-instances-health-check). Your function app should have an HTTP trigger function that responds with an HTTP status code of 200 on the same endpoint as configured on the `Path`

parameter of the health check. You can also have that function perform extra checks to ensure that dependent services are reachable and working.

## Related content

For more information about monitoring, see:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output-invoke -->

# Dapr Invoke output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr invoke output binding allows you to invoke another Dapr application during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using a Dapr invoke output binding to perform a Dapr service invocation operation hosted in another Dapr-ized application. In this example, the function acts like a proxy.

```
[FunctionName("InvokeOutputBinding")]
public static async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = "invoke/{appId}/{methodName}")] HttpRequest req,
[DaprInvoke(AppId = "{appId}", MethodName = "{methodName}", HttpVerb = "post")] IAsyncCollector<InvokeMethodParameters> output,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
var outputContent = new InvokeMethodParameters
{
Body = requestBody
};
await output.AddAsync(outputContent);
return new OkResult();
}
```


The following example creates a `"InvokeOutputBinding"`

function using the `DaprInvokeOutput`

binding with an `HttpTrigger`

:

```
@FunctionName("InvokeOutputBinding")
public String run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "invoke/{appId}/{methodName}")
HttpRequestMessage<Optional<String>> request,
@DaprInvokeOutput(
appId = "{appId}",
methodName = "{methodName}",
httpVerb = "post")
OutputBinding<String> payload,
final ExecutionContext context)
```


In the following example, the Dapr invoke output binding is paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('InvokeOutputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['POST'],
route: "invoke/{appId}/{methodName}",
name: "req"
}),
return: daprInvokeOutput,
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const payload = await request.text();
context.log(JSON.stringify(payload));
return { body: payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprInvoke`

:

```
{
"bindings":
{
"type": "daprInvoke",
"direction": "out",
"appId": "{appId}",
"methodName": "{methodName}",
"httpVerb": "post",
"name": "payload"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($req, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "Powershell InvokeOutputBinding processed a request."
$req_body = $req.Body
$invoke_output_binding_req_body = @{
"body" = $req_body
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name payload -Value $invoke_output_binding_req_body
Push-OutputBinding -Name res -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $req_body
})
```


The following example shows a Dapr Invoke output binding, which uses the [v2 Python programming model](functions-reference-python). To use `daprInvoke`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="InvokeOutputBinding")
@app.route(route="invoke/{appId}/{methodName}", auth_level=dapp.auth_level.ANONYMOUS)
@app.dapr_invoke_output(arg_name = "payload", app_id = "{appId}", method_name = "{methodName}", http_verb = "post")
def main(req: func.HttpRequest, payload: func.Out[str] ) -> str:
# request body must be passed this way "{\"body\":{\"value\":{\"key\":\"some value\"}}}" to use the InvokeOutputBinding, all the data must be enclosed in body property.
logging.info('Python function processed a InvokeOutputBinding request from the Dapr Runtime.')
body = req.get_body()
logging.info(body)
if body is not None:
payload.set(body)
else:
logging.info('req body is none')
return 'ok'
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprInvoke`

attribute to define a Dapr invoke output binding, which supports these parameters:

| Parameter | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
AppId |
The Dapr app ID to invoke. | ✔️ | ✔️ |
MethodName |
The method name of the app to invoke. | ✔️ | ✔️ |
HttpVerb |
Optional. HTTP verb to use of the app to invoke. Default is `POST` . |
✔️ | ✔️ |
Body |
Required. The body of the request. |
❌ | ✔️ |

## Annotations

The `DaprInvokeOutput`

annotation allows you to have your function invoke and listen to an output binding.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methodName |
The name of the method variable. | ✔️ | ✔️ |
httpVerb |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methods |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
appId |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
methodName |
The name of the method variable. | ✔️ | ✔️ |
httpVerb |
Post or get. | ✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_invoke_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
app_id |
The app ID of the application involved in the invoke binding. | ✔️ | ✔️ |
method_name |
The name of the method variable. | ✔️ | ✔️ |
http_verb |
Set to `post` or `get` . |
✔️ | ✔️ |
body |
Required. The body of the request. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr service invocation output binding, learn more about [how to use Dapr service invocation in the official Dapr documentation](https://docs.dapr.io/developing-applications/building-blocks/service-invocation/).

To use the `daprInvoke`

in Python v2, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/ip-addresses -->

# IP addresses in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the following concepts related to IP addresses of function apps:

- Locating the IP addresses currently in use by a function app.
- Conditions that cause function app IP addresses to change.
- Restricting the IP addresses that can access a function app.
- Defining dedicated IP addresses for a function app.

IP addresses are associated with function apps, not with individual functions. Incoming HTTP requests can't use the inbound IP address to call individual functions; they must use the default domain name (functionappname.azurewebsites.net) or a custom domain name.

## Function app inbound IP address

Each function app starts out by using a single inbound IP address. When a function app runs in a Consumption or Premium plan, more inbound IP addresses might be added as event-driven scale-out occurs. To find the inbound IP address or addresses being used by your app, use the `nslookup`

utility from your local computer, as in the following example:

```
nslookup <APP_NAME>.azurewebsites.net
```


In this example, replace `<APP_NAME>`

with your function app name. If your app uses a [custom domain name](../app-service/app-service-web-tutorial-custom-domain), use `nslookup`

for that custom domain name instead.

## Function app outbound IP addresses

Each function app has a set of available outbound IP addresses. Any outbound connection from a function, such as to a back-end database, uses one of the available outbound IP addresses as the origin IP address. You can't know beforehand which IP address a given connection uses. For this reason, your back-end service must open its firewall to all of the function app's outbound IP addresses.

Tip

For some platform-level features such as [Key Vault references](../app-service/app-service-key-vault-references), the origin IP might not be one of the outbound IPs, and you shouldn't configure the target resource to rely on these specific addresses. We recommend that the app instead uses a virtual network integration, because the platform routes traffic to the target resource through that network.

To find the outbound IP addresses available to a function app:

- Sign in to the
[Azure Resource Explorer](https://resources.azure.com). - Select
**subscriptions**> {your subscription} >**providers**>**Microsoft.Web**>**sites**. - In the JSON panel, find the site with an
`id`

property that ends in the name of your function app. - See
`outboundIpAddresses`

and`possibleOutboundIpAddresses`

.

The set of `outboundIpAddresses`

is currently available to the function app. The set of `possibleOutboundIpAddresses`

includes IP addresses that are available only if the function app [scales to other pricing tiers](#outbound-ip-address-changes).

Note

When a function app that runs on the [Consumption plan](consumption-plan) or the [Premium plan](functions-premium-plan) is scaled, a new range of outbound IP addresses might be assigned. When running on either of these plans, you can't rely on the reported outbound IP addresses to create a definitive allowlist. To be able to include all potential outbound addresses used during dynamic scaling, you need to add the entire data center to your allowlist.

## Data center outbound IP addresses

If you need to add the outbound IP addresses used by your function apps to an allowlist, another option is to add the function apps' data center (Azure region) to an allowlist. You can [download a JSON file that lists IP addresses for all Azure data centers](https://www.microsoft.com/en-us/download/details.aspx?id=56519). Then find the JSON fragment that applies to the region that your function app runs in.

For example, the following JSON fragment is what the allowlist for Western Europe might look like:

```
{
"name": "AzureCloud.westeurope",
"id": "AzureCloud.westeurope",
"properties": {
"changeNumber": 9,
"region": "westeurope",
"platform": "Azure",
"systemService": "",
"addressPrefixes": [
"13.69.0.0/17",
"13.73.128.0/18",
... Some IP addresses not shown here
"213.199.180.192/27",
"213.199.183.0/24"
]
}
}
```


For information about when this file is updated and when the IP addresses change, expand the **Details** section of the [Download Center page](https://www.microsoft.com/en-us/download/details.aspx?id=56519).

## Inbound IP address changes

The inbound IP address **might** change when you:

- Delete a function app and recreate it in a different resource group.
- Delete the last function app in a resource group and region combination, and re-create it.
- Delete a TLS binding, such as during
[certificate renewal](../app-service/configure-ssl-certificate#renew-an-expiring-certificate).

When your function app runs in a [Consumption plan](consumption-plan) or in a [Premium plan](functions-premium-plan), the inbound IP address might also change even when you haven't taken any actions such as the ones here.

## Outbound IP address changes

The relative stability of the outbound IP address depends on the hosting plan.

### Consumption and Premium plans

Because of autoscaling behaviors, the outbound IP can change at any time when running on a [Consumption plan](consumption-plan) or in a [Premium plan](functions-premium-plan).

If you need to control the outbound IP address of your function app, such as when you need to add it to an allowlist, consider implementing a [virtual network NAT gateway](#virtual-network-nat-gateway-for-outbound-static-ip) while running in a Premium hosting plan. You can also do this by running in a Dedicated (App Service) plan.

### Dedicated plans

When a function app runs on Dedicated (App Service) plans, the set of available outbound IP addresses for a function app might change when you:

- Take any action that can change the inbound IP address.
- Change your Dedicated (App Service) plan pricing tier. The list of all possible outbound IP addresses your app can use, for all pricing tiers, is in the
`possibleOutboundIPAddresses`

property. See[Find outbound IPs](#find-outbound-ip-addresses).

#### Forcing an outbound IP address change

Use the following procedure to deliberately force an outbound IP address change in a Dedicated (App Service) plan:

Scale your App Service plan up or down between Standard and Premium v2 pricing tiers.

Wait 10 minutes.

Scale back to where you started.


## IP address restrictions

You can configure a list of IP addresses that you want to allow or deny access to a function app. For more information, see [Azure App Service access restrictions](../app-service/app-service-ip-restrictions).

## Dedicated IP addresses

There are several strategies to explore when your function app requires static, dedicated IP addresses.

### Virtual network NAT gateway for outbound static IP

You can control the IP address of outbound traffic from your functions by using a virtual network NAT gateway to direct traffic through a static public IP address. You can use this topology when running in a [Premium plan](functions-premium-plan) or in a [Dedicated hosting plan](dedicated-plan). To learn more, see [Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway](functions-how-to-use-nat-gateway).

### App Service Environments

For full control over the IP addresses, both inbound and outbound, we recommend [App Service Environments](../app-service/environment/intro) (the [Isolated tier](https://azure.microsoft.com/pricing/details/app-service/) of App Service plans). For more information, see [App Service Environment overview](../app-service/environment/overview).

To find out if your function app runs in an App Service Environment:

- Sign in to the
[Azure portal](https://portal.azure.com). - Navigate to the function app.
- Select the
**Overview**tab. - The App Service plan tier appears under
**App Service plan/pricing tier**. The App Service Environment pricing tier is**Isolated**.

The App Service Environment `sku`

is `Isolated`

.

## Next steps

A common cause of IP changes is function app scale changes. [Learn more about function app scaling](functions-scale).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/create-first-function-azure-developer-cli -->

# Quickstart: Build a scalable web API using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use Azure Developer command-line tools to build a scalable web API with function endpoints that respond to HTTP requests. After testing the code locally, you deploy it to a new serverless function app you create running in a Flex Consumption plan in Azure Functions.

The project source uses the Azure Developer CLI (azd) to simplify deploying your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

By default, the Flex Consumption plan follows a *pay-for-what-you-use* billing model, which means completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[Java 17 Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure)- If you use another
[supported version of Java](supported-languages?pivots=programming-language-java#languages-by-runtime-version), you must update the project's pom.xml file. - The
`JAVA_HOME`

environment variable must be set to the install location of the correct version of the Java Development Kit (JDK).

- If you use another
[Apache Maven 3.8.x](https://maven.apache.org)

- A
[secure HTTP test tool](functions-develop-local#http-test-tools)for sending requests with JSON payloads to your function endpoints. This article uses`curl`

.

## Initialize the project

Use the `azd init`

command to create a local Azure Functions code project from a template.

In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-dotnet-azd -e httpendpoint-dotnet`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.Run this command to navigate to the

`http`

app folder:`cd http`

Create a file named

*local.settings.json*in the`http`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template azure-functions-java-flex-consumption-azd -e httpendpoint-java`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/azure-functions-java-flex-consumption-azd)and initializes the project in the current folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.Run this command to navigate to the

`http`

app folder:`cd http`

Create a file named

*local.settings.json*in the`http`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "java" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-javascript-azd -e httpendpoint-js`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-javascript-azd)and initializes the project in the root folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the root folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "node" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-powershell-azd -e httpendpoint-ps`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-powershell-azd)and initializes the project in the root folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. It's also used in the name of the resource group you create in Azure.Run this command to navigate to the

`src`

app folder:`cd src`

Create a file named

*local.settings.json*in the`src`

folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "powershell", "FUNCTIONS_WORKER_RUNTIME_VERSION": "7.2" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-typescript-azd -e httpendpoint-ts`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd)and initializes the project in the root folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the root folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "node" } }`

This file is required when running locally.


In your local terminal or command prompt, run this

`azd init`

command in an empty folder:`azd init --template functions-quickstart-python-http-azd -e httpendpoint-py`

This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-http-azd)and initializes the project in the root folder. The`-e`

flag sets a name for the current environment. In`azd`

, the environment maintains a unique deployment context for your app, and you can define more than one. The environment name is also used in the name of the resource group you create in Azure.Create a file named

*local.settings.json*in the root folder that contains this JSON data:`{ "IsEncrypted": false, "Values": { "AzureWebJobsStorage": "UseDevelopmentStorage=true", "FUNCTIONS_WORKER_RUNTIME": "python" } }`

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

`mvn clean package mvn azure-functions:run`

`npm install func start`

`npm install npm start`

When the Functions host starts in your local project folder, it writes the URL endpoints of your HTTP triggered functions to the terminal output.

Note

Because access key authorization isn't enforced when running locally, the function URL returned doesn't include the access key value and you don't need it to call your function.

In your browser, go to the

`httpget`

endpoint, which should look like this URL:From a new terminal or command prompt window, run this

`curl`

command to send a POST request with a JSON payload to the`httppost`

endpoint:`curl -i http://localhost:7071/api/httppost -H "Content-Type: text/json" -d @testdata.json`

`curl -i http://localhost:7071/api/httppost -H "Content-Type: text/json" -d "@src/functions/testdata.json"`

This command reads JSON payload data from the

`testdata.json`

project file. You can find examples of both HTTP requests in the`test.http`

project file.When you're done, press Ctrl+C in the terminal window to stop the

`func.exe`

host process.

- Run
`deactivate`

to shut down the virtual environment.

## Review the code (optional)

You can review the code that defines the two HTTP trigger function endpoints:

```
[Function("httpget")]
public IActionResult Run([HttpTrigger(AuthorizationLevel.Function, "get")]
HttpRequest req,
string name)
{
var returnValue = string.IsNullOrEmpty(name)
? "Hello, World."
: $"Hello, {name}.";
_logger.LogInformation($"C# HTTP trigger function processed a request for {returnValue}.");
return new OkObjectResult(returnValue);
}
```


```
@FunctionName("httpget")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.FUNCTION)
HttpRequestMessage<Optional<String>> request,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String name = Optional.ofNullable(request.getQueryParameters().get("name")).orElse("World");
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
}
```


```
const { app } = require('@azure/functions');
app.http('httpget', {
methods: ['GET'],
authLevel: 'function',
handler: async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || await request.text() || 'world';
return { body: `Hello, ${name}!` };
}
});
```


```
import { app, HttpRequest, HttpResponseInit, InvocationContext } from "@azure/functions";
export async function httpGetFunction(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || await request.text() || 'world';
return { body: `Hello, ${name}!` };
};
app.http('httpget', {
methods: ['GET'],
authLevel: 'function',
handler: httpGetFunction
});
```


This `function.json`

file defines the `httpget`

function:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"methods": [
"get"
],
"route": "httpget"
},
{
"type": "http",
"direction": "out",
"name": "Response"
}
]
}
```


This `run.ps1`

file implements the function code:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters
$name = $Request.Query.name
$body = "This HTTP triggered function executed successfully. Pass a name in the query string for a personalized response."
if ($name) {
$body = "Hello, $name. This HTTP triggered function executed successfully."
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $body
})
```


```
@app.route(route="httpget", methods=["GET"])
def http_get(req: func.HttpRequest) -> func.HttpResponse:
name = req.params.get("name", "World")
logging.info(f"Processing GET request. Name: {name}")
return func.HttpResponse(f"Hello, {name}!")
```


You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd).

You can review the complete template project [here](https://github.com/Azure-Samples/azure-functions-java-flex-consumption-azd).

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-javascript-azd).

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-typescript-azd).

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-powershell-azd).

You can review the complete template project [here](https://github.com/Azure-Samples/functions-quickstart-python-http-azd).

After you verify your functions locally, it's time to publish them to Azure.

## Deploy to Azure

This project is configured to use the `azd up`

command to deploy this project to a new function app in a Flex Consumption plan in Azure.

Tip

The project includes a set of Bicep files (in the `infra`

folder) that `azd`

uses to create a secure deployment to a Flex consumption plan that follows best practices.

Run this command to have

`azd`

create the required Azure resources in Azure and deploy your code project to the new function app:`azd up`

The root folder contains the

`azure.yaml`

definition file required by`azd`

.If you're not already signed in, you're asked to authenticate with your Azure account.

When prompted, provide these required deployment parameters:

Parameter Description *Azure subscription*Subscription in which your resources are created. *Azure location*Azure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. *vnetEnabled*Choose *False*. When set to*True*the deployment creates your function app in a new virtual network.The

`azd up`

command uses your responses to these prompts with the Bicep configuration files to complete these deployment tasks:Create and configure these required Azure resources (equivalent to

`azd provision`

):- Flex Consumption plan and function app
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)
- (Option) Virtual network to securely run both the function app and the other Azure resources

Package and deploy your code to the deployment container (equivalent to

`azd deploy`

). The app is then started and runs in the deployed package.

After the command completes successfully, you see links to the resources you created.


## Invoke the function on Azure

You can now invoke your function endpoints in Azure by making HTTP requests to their URLs by using your HTTP test tool or from the browser (for GET requests). When your functions run in Azure, access key authorization is enforced, and you must provide a function access key with your request.

You can use the Core Tools to get the URL endpoints of your functions running in Azure.

In your local terminal or command prompt, run these commands to get the URL endpoint values:

`$APP_NAME = azd env get-value AZURE_FUNCTION_NAME func azure functionapp list-functions $APP_NAME --show-keys`

The

`azd env get-value`

command gets your function app name from the local environment. When you use the`--show-keys`

option with`func azure functionapp list-functions`

, the returned**Invoke URL:**value for each endpoint includes a function-level access key.As before, use your HTTP test tool to validate these URLs in your function app running in Azure.


## Redeploy your code

Run the `azd up`

command as many times as you need to both provision your Azure resources and deploy code updates to your function app.

Note

Deployed code files are always overwritten by the latest deployment package.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that you used when creating Azure resources.

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-triggers-bindings -->

# Azure Functions triggers and bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn the high-level concepts surrounding triggers and bindings for functions.

Triggers cause a function to run. A trigger defines how a function is invoked, and a function must have exactly one trigger. Triggers can also pass data into your function, as you would with method calls.

Binding to a function is a way of declaratively connecting your functions to other resources. Bindings either pass data into your function (an *input binding*) or enable you to write data out from your function (an *output binding*) by using *binding parameters*. Your function trigger is essentially a special type of input binding.

You can mix and match bindings to suit your function's specific scenario. Bindings are optional, and a function might have one or multiple input and/or output bindings.

Triggers and bindings let you avoid hardcoding access to other services. Your function receives data (for example, the content of a queue message) in function parameters. You send data (for example, to create a queue message) by using the return value of the function.

Consider the following examples of how you could implement functions:

| Example scenario | Trigger | Input binding | Output binding |
|---|---|---|---|
| A new queue message arrives, which runs a function to write to another queue. | Queue* |
None |
Queue* |
| A scheduled job reads Azure Blob Storage contents and creates a new Azure Cosmos DB document. | Timer | Blob Storage | Azure Cosmos DB |
| Azure Event Grid is used to read an image from Blob Storage and a document from Azure Cosmos DB to send an email. | Event Grid | Blob Storage and Azure Cosmos DB | SendGrid |

* Represents different queues.

These examples aren't meant to be exhaustive, but they illustrate how you can use triggers and bindings together. For a more comprehensive set of scenarios, see [Azure Functions scenarios](functions-scenarios).

Tip

Azure Functions doesn't require you to use input and output bindings to connect to Azure services. You can always create an Azure SDK client in your code and use it instead for your data transfers. For more information, see [Connect to services](functions-reference#connect-to-services).

## Trigger and binding definitions

The following example shows an HTTP-triggered function with an output binding that writes a message to an Azure Storage queue.

For C# class library functions, you configure triggers and bindings by decorating methods and parameters with C# attributes. The specific attribute that you apply might depend on the C# runtime model:

The HTTP trigger (`HttpTrigger`

) is defined on the `Run`

method for a function named `HttpExample`

that returns a `MultiResponse`

object:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
```


This example shows the `MultiResponse`

object definition. The object definition returns `HttpResponse`

to the HTTP request and writes a message to a storage queue by using a `QueueOutput`

binding:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


For more information, see the [C# guide for isolated worker models](dotnet-isolated-process-guide#methods-recognized-as-functions).

Legacy C# script functions use a `function.json`

definition file. For more information, see the [Azure Functions C# script (.csx) developer reference](functions-reference-csharp).

For Java functions, you configure triggers and bindings by annotating specific methods and parameters. This HTTP trigger (`@HttpTrigger`

) is defined on the `run`

method for a function named `HttpExample`

. The function writes to a storage queue named `outqueue`

that the `@QueueOutput`

annotation defines on the `msg`

parameter:

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
```


For more information, see the [Java developer guide](functions-reference-java#triggers-and-annotations).

The way that you define triggers and bindings for Node.js functions depends on the specific version of Node.js for Azure Functions:

In Node.js for Azure Functions version 4, you configure triggers and bindings by using objects exported from the `@azure/functions`

module. For more information, see the [Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4#inputs-and-outputs).

The `http`

method on the exported `app`

object defines an HTTP trigger. The `storageQueue`

method on `output`

defines an output binding on this trigger.

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


The `http`

method on the exported `app`

object defines an HTTP trigger. The `storageQueue`

method on `output`

defines an output binding on this trigger.

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


This example `function.json`

file defines the function:

```
{
"authLevel": "function",
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
"name": "msg",
"queueName": "outqueue",
"connection": "AzureWebJobsStorage"
}
]
}
```


For more information, see the [PowerShell developer guide](functions-reference-powershell#bindings).

The way that the function is defined depends on the version of Python for Azure Functions:

In Python for Azure Functions version 2, you define the function directly in code by using decorators:

```
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
```


## Binding considerations

Not all services support both input and output bindings. See your specific binding extension for

[specific code examples for bindings](#code-examples-for-bindings).Triggers and bindings are defined differently depending on the development language. Make sure to select your language at the

[top](#top)of this article.Trigger and binding names are limited to alphanumeric characters and

`_`

, the underscore.

## Task to add bindings to a function

You can connect your function to other services by using input or output bindings. Add a binding by adding its specific definitions to your function. To learn how, see [Add bindings to an existing function in Azure Functions](add-bindings-existing-function).

Azure Functions supports multiple bindings, which must be configured correctly. For example, a function can read data from a queue (input binding) and write data to a database (output binding) simultaneously.

## Supported bindings

This table shows the bindings that are supported in the major versions of the Azure Functions runtime:

| Type | 4.x1 |
1.x2 |
Trigger | Input | Output |
|---|---|---|---|---|---|
|

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)[Azure Data Explorer](functions-bindings-azure-data-explorer)[Azure SQL](functions-bindings-azure-sql)[Dapr](functions-bindings-dapr)4[Event Grid](functions-bindings-event-grid)[Event Hubs](functions-bindings-event-hubs)[HTTP and webhooks](functions-bindings-http-webhook)[IoT Hub](functions-bindings-event-iot)[Kafka](functions-bindings-kafka)3[Mobile Apps](functions-bindings-mobile-apps)[Model Context Protocol](functions-bindings-mcp)[Notification Hubs](functions-bindings-notification-hubs)[Queue Storage](functions-bindings-storage-queue)[Redis](functions-bindings-cache)[RabbitMQ](functions-bindings-rabbitmq)3[SendGrid](functions-bindings-sendgrid)[Service Bus](functions-bindings-service-bus)[Azure SignalR Service](functions-bindings-signalr-service)[Table Storage](functions-bindings-storage-table)[Timer](functions-bindings-timer)[Twilio](functions-bindings-twilio)- Register all bindings except HTTP and timer. See
[Register Azure Functions binding extensions](functions-bindings-register). This step isn't required when using version 1.x of the Functions runtime. [Support ends for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1).[Migrate your apps to version 4.x](migrate-version-1-version-4)for full support.- Triggers aren't supported in the Consumption plan. This binding type requires
[runtime-driven triggers](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers). - This binding type is supported in Kubernetes, Azure IoT Edge, and other self-hosted modes only.

For information about which bindings are in preview or are approved for production use, see [Supported languages](supported-languages).

Specific versions of binding extensions are supported only while the underlying service SDK is supported. Changes to support in the underlying service SDK version affect the support for the consuming extension.

## SDK types

Azure Functions binding extensions use Azure service SDKs to connect to Azure services. The specific SDK types used by bindings can affect how you work with the data in your functions. Some bindings support SDK-specific types that provide richer functionality and better integration with the service, while others use more generic types like strings or byte arrays. When available, using SDK-specific types can provide benefits such as better type safety, easier data manipulation, and access to service-specific features.

This table indicates binding extensions that currently support SDK types:

| Extension | Types | Support level |
|---|---|---|
|

`BlobClient`

`BlobContainerClient`

`BlockBlobClient`

`PageBlobClient`

`AppendBlobClient`

Input: GA

[Azure Cosmos DB](functions-bindings-cosmosdb-v2?tabs=isolated-process,extensionv4&pivots=programming-language-csharp#binding-types)`CosmosClient`

`Database`

`Container`

[Azure Event Grid](functions-bindings-event-grid?tabs=isolated-process,extensionv3&pivots=programming-language-csharp#binding-types)`CloudEvent`

`EventGridEvent`

[Azure Event Hubs](functions-bindings-event-hubs?tabs=isolated-process,extensionv5&pivots=programming-language-csharp#binding-types)`EventData`

`EventHubProducerClient`

[Azure Queue Storage](functions-bindings-storage-queue?tabs=isolated-process,extensionv5&pivots=programming-language-csharp#binding-types)`QueueClient`

`QueueMessage`

[Azure Service Bus](functions-bindings-service-bus?tabs=isolated-process,extensionv5&pivots=programming-language-csharp#binding-types)`ServiceBusClient`

`ServiceBusReceiver`

`ServiceBusSender`

`ServiceBusMessage`

[Azure Table Storage](functions-bindings-storage-table?tabs=isolated-process,table-api&pivots=programming-language-csharp#binding-types)`TableClient`

`TableEntity`

Considerations for SDK types:

- When using
[binding expressions](functions-bindings-expressions-patterns)that rely on trigger data, SDK types for the trigger itself cannot be used. - For output scenarios where you might use an SDK type, create and work with SDK clients directly instead of using an output binding.
- The Azure Cosmos DB trigger uses the
[Azure Cosmos DB change feed](/en-us/azure/cosmos-db/change-feed)and exposes change feed items as JSON-serializable types. As a result, SDK types aren't supported for this trigger.

For more information, see [SDK types](dotnet-isolated-process-guide#sdk-types) in the C# developer guide.

| Extension | Types | Support level | Samples |
|---|---|---|---|
|

`BlobClient`

`ContainerClient`

`StorageStreamDownloader`

Input: GA

[Quickstart](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python)`BlobClient`

`ContainerClient`

`StorageStreamDownloader`

[Azure Cosmos DB](functions-bindings-cosmosdb-v2)`CosmosClient`

`DatabaseProxy`

`ContainerProxy`

[Quickstart](https://github.com/Azure-Samples/azure-functions-cosmosdb-sdk-bindings-python)`ContainerProxy`

`CosmosClient`

`DatabaseProxy`

[Azure Event Hubs](functions-bindings-event-hubs)`EventData`

[Quickstart](https://github.com/Azure-Samples/azure-functions-eventhub-sdk-bindings-python)`EventData`

[Azure Service Bus](functions-bindings-service-bus)`ServiceBusReceivedMessage`

[Quickstart](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-servicebus/samples/README.md)`ServiceBusReceivedMessage`

Considerations for SDK types:

- For output scenarios where you might use an SDK type, create and work with SDK clients directly instead of using an output binding.
- The Azure Cosmos DB trigger uses the
[Azure Cosmos DB change feed](/en-us/azure/cosmos-db/change-feed)and exposes change feed items as JSON-serializable types. As a result, SDK types aren't supported for this trigger.

SDK types are supported only when using the Python v2 programming model. For more information, see [SDK type bindings](functions-reference-python#sdk-type-bindings) in the Python developer guide.

| Extension | Types | Support level |
|---|---|---|
|

`BlobClient`

`ContainerClient`

`ReadableStream`

[Azure Service Bus](functions-bindings-service-bus)`ServiceBusClient`

`ServiceBusReceiver`

`ServiceBusSender`

`ServiceBusMessage`

SDK types are supported only when using the Node v4 programming model. For more information, see [SDK types](functions-reference-node#sdk-types) in the Node.js developer guide.

| Extension | Types | Support level |
|---|---|---|
|

`BlobClient`

`BlobContainerClient`

For more information, see [SDK types](functions-reference-java#sdk-types) in the Java developer guide.

Important

SDK types aren't currently supported for PowerShell apps.

## Code examples for bindings

Use the following table to find more examples of specific binding types that show you how to work with bindings in your functions. First, choose the language tab that corresponds to your project.

Binding code for C# depends on the [specific process model](dotnet-isolated-process-guide#benefits-of-the-isolated-worker-model).

| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/storage/Microsoft.Azure.WebJobs.Extensions.Storage.Blobs)[Trigger](functions-bindings-cosmosdb-v2-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-cosmosdb-v2-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-cosmosdb-v2-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-csharp#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-csharp#examples)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-csharp)[Trigger](functions-bindings-azure-sql-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-azure-sql-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-azure-sql-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](/en-us/samples/azure-samples/azure-sql-binding-func-dotnet-todo/todo-backend-dotnet-azure-sql-bindings-azure-functions/)[Trigger](functions-bindings-event-grid-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-grid-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Trigger](functions-bindings-event-hubs-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-hubs-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-event-iot-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-iot-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-http-webhook-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd)[Trigger](functions-bindings-storage-queue-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-storage-queue-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/storage/Microsoft.Azure.WebJobs.Extensions.Storage.Queues/samples/functionapp)[Trigger](functions-bindings-rabbitmq-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-rabbitmq-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-sendgrid?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-service-bus-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-service-bus-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/servicebus/Microsoft.Azure.WebJobs.Extensions.ServiceBus)[Trigger](functions-bindings-signalr-service-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-signalr-service-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-signalr-service-output?tabs=isolated-process&pivots=programming-language-csharp)[Input](functions-bindings-storage-table-input?tabs=isolated-process&pivots=programming-language-csharp)[Output](functions-bindings-storage-table-output?tabs=isolated-process&pivots=programming-language-csharp)[Trigger](functions-bindings-timer?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Output](functions-bindings-twilio?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-java#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-java#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/java-functions-eventhub-cosmosdb)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-java#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-java#examples)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-java)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-java#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-java#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-java#example)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-java#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-java#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-java#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-java#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-java#example)[Output](functions-bindings-sendgrid?pivots=programming-language-java#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-java#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-java#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-java#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-java)[Input](functions-bindings-storage-table-input?pivots=programming-language-java)[Output](functions-bindings-storage-table-output?pivots=programming-language-java)[Trigger](functions-bindings-timer?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Output](functions-bindings-twilio?pivots=programming-language-java#example)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-nodejs)[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-javascript#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-add-output-binding-cosmosdb-cli-v4-programming-model)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-javascript#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-javascript#examples)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-javascript#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-node)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-typescript)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-add-output-binding-storage-queue-cli-v4-programming-model)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-javascript#example)[Output](functions-bindings-sendgrid?pivots=programming-language-javascript#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/azure-functions-servicebus-sdk-bindings-nodejs/tree/main/serviceBusSampleWithComplete)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-javascript#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-javascript)[Input](functions-bindings-storage-table-input?pivots=programming-language-javascript)[Output](functions-bindings-storage-table-output?pivots=programming-language-javascript)[Trigger](functions-bindings-timer?pivots=programming-language-javascript#example)[Output](functions-bindings-twilio?pivots=programming-language-javascript#example)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-powershell#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-powershell#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-powershell#example)[Link](https://github.com/Azure-Samples/functions-quickstart-powershell-azd)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-powershell#example)[Output](functions-bindings-sendgrid?pivots=programming-language-powershell#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-powershell#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-powershell)[Input](functions-bindings-storage-table-input?pivots=programming-language-powershell)[Output](functions-bindings-storage-table-output?pivots=programming-language-powershell)[Trigger](functions-bindings-timer?pivots=programming-language-powershell#example)[Output](functions-bindings-twilio?pivots=programming-language-powershell#example)Binding code for Python depends on the Python model version.

| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python)[Trigger](functions-bindings-cosmosdb-v2-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-cosmosdb-v2-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-cosmosdb-v2-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-cosmosdb)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-python#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-python#examples)[Trigger](functions-bindings-azure-sql-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-azure-sql-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-azure-sql-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python)[Trigger](functions-bindings-event-grid-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-grid-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-hubs-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-hubs-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-iot-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-iot-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-http-azd)[Trigger](functions-bindings-storage-queue-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-storage-queue-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-rabbitmq-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-rabbitmq-output?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-sendgrid?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-service-bus-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-service-bus-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-service-bus)[Trigger](functions-bindings-signalr-service-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-signalr-service-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-signalr-service-output?tabs=python-v2&pivots=programming-language-python)[Input](functions-bindings-storage-table-input?tabs=python-v2&pivots=programming-language-python)[Output](functions-bindings-storage-table-output?tabs=python-v2&pivots=programming-language-python)[Trigger](functions-bindings-timer?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-twilio?tabs=python-v2&pivots=programming-language-python#example)## Custom bindings

You can create custom input and output bindings. Bindings must be authored in .NET, but they can be consumed from any supported language. For more information about creating custom bindings, see [Creating custom input and output bindings](https://github.com/Azure/azure-webjobs-sdk/wiki/Creating-custom-input-and-output-bindings).
