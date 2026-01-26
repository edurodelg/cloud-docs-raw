---
merged_at: 2026-01-26T21:02:36.363770
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-azure-mysql-input____functions-diagnostics_functions-openapi_eae8d1.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-azure-mysql-input.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql-input -->

# Azure Database for MySQL input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When a function runs, the Azure Database for MySQL input binding retrieves data from a database and passes it to the input parameter of the function.

For information on setup and configuration, see the [overview](functions-bindings-azure-mysql).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples).

This section contains the following examples:

[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-c-oop)[HTTP trigger, get multiple rows from route data](#http-trigger-get-multiple-items-from-route-data-c-oop)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-c-oop)

The examples refer to a `Product`

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


### HTTP trigger, get a row by ID from a query string

The following example shows a C# function that retrieves a single record. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses a query string to specify the ID. That ID is used to retrieve a `Product`

record with the specified query.

Note

The HTTP query string parameter is case-sensitive.

```
using System.Collections.Generic;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Azure.Functions.Worker.Http;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.InputBindingIsolatedSamples
{
public static class GetProductById
{
[Function(nameof(GetProductById))]
public static IEnumerable<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproducts/{productId}")]
HttpRequestData req,
[MySqlInput("select * from Products where ProductId = @productId",
"MySqlConnectionString",
parameters: "@ProductId={productId}")]
IEnumerable<Product> products)
{
return products;
}
}
}
```


### HTTP trigger, get multiple rows from a route parameter

The following example shows a [C# function](functions-dotnet-class-library) that retrieves rows that the query returned. The function is [triggered by an HTTP request](functions-bindings-http-webhook-trigger) that uses route data to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

```
using System.Collections.Generic;
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.MySql;
using Microsoft.Azure.Functions.Worker.Http;
using AzureMySqlSamples.Common;
namespace AzureMySqlSamples.InputBindingIsolatedSamples
{
public static class GetProducts
{
[Function(nameof(GetProducts))]
public static IEnumerable<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproducts")]
HttpRequestData req,
[MySqlInput("select * from Products",
"MySqlConnectionString")]
IEnumerable<Product> products)
{
return products;
}
}
}
```


### HTTP trigger, delete rows

The following example shows a [C# function](functions-dotnet-class-library) that executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the MySQL database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


```
namespace AzureMySqlSamples.InputBindingSamples
{
public static class GetProductsStoredProcedure
{
[FunctionName(nameof(GetProductsStoredProcedure))]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproducts-storedprocedure/{cost}")]
HttpRequest req,
[MySql("DeleteProductsCost",
"MySqlConnectionString",
commandType: System.Data.CommandType.StoredProcedure,
parameters: "@Cost={cost}")]
IEnumerable<Product> products)
{
return new OkObjectResult(products);
}
}
}
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-java).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-java)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-java)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-java)

The examples refer to a `Product`

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
```


```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding in a Java function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

```
package com.function;
import com.function.Common.Product;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.mysql.annotation.CommandType;
import com.microsoft.azure.functions.mysql.annotation.MySqlInput;
import java.util.Optional;
public class GetProducts {
@FunctionName("GetProducts")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "getproducts}")
HttpRequestMessage<Optional<String>> request,
@MySqlInput(
name = "products",
commandText = "SELECT * FROM Products",
commandType = CommandType.Text,
connectionStringSetting = "MySqlConnectionString")
Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products).build();
}
}
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding in a Java function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

```
public class GetProductById {
@FunctionName("GetProductById")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "getproducts/{productid}")
HttpRequestMessage<Optional<String>> request,
@MySqlInput(
name = "products",
commandText = "SELECT * FROM Products WHERE ProductId= @productId",
commandType = CommandType.Text,
parameters = "@productId={productid}",
connectionStringSetting = "MySqlConnectionString")
Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products).build();
}
}
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding in a Java function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


```
public class DeleteProductsStoredProcedure {
@FunctionName("DeleteProductsStoredProcedure")
public HttpResponseMessage run(
@HttpTrigger(
name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "Deleteproducts-storedprocedure/{cost}")
HttpRequestMessage<Optional<String>> request,
@MySqlInput(
name = "products",
commandText = "DeleteProductsCost",
commandType = CommandType.StoredProcedure,
parameters = "@Cost={cost}",
connectionStringSetting = "MySqlConnectionString")
Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products).build();
}
}
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-js).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-javascript)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-javascript)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-javascript)

The examples refer to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const mysqlInput = input.generic({
commandText: 'select * from Products',
commandType: 'Text',
connectionStringSetting: 'MySqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and MySQL input binding function processed a request.');
const products = context.extraInputs.get(mysqlInput);
return {
jsonBody: products,
};
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [mysqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const mysqlInput = input.generic({
type: 'mysql',
commandText: 'select * from Products where Cost = @Cost',
parameters: '@Cost={Cost}',
commandType: 'Text',
connectionStringSetting: 'MySqlConnectionString'
})
app.http('GetProducts', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
route: 'getproducts/{cost}',
extraInputs: [mysqlInput],
handler: async (request, context) => {
const products = JSON.stringify(context.extraInputs.get(mysqlInput));
return {
status: 200,
body: products
};
}
});
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const mysqlInput = input.generic({
commandText: 'select * from Products where ProductId= @productId',
commandType: 'Text',
parameters: '@productId={productid}',
connectionStringSetting: 'MySqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and MySQL input binding function processed a request.');
const products = context.extraInputs.get(mysqlInput);
return {
jsonBody: products,
};
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [mysqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const mysqlInput = input.generic({
type: 'mysql',
commandText: 'select * from Products where ProductId= @productId',
commandType: 'Text',
parameters: '@productId={productid}',
connectionStringSetting: 'MySqlConnectionString'
})
app.http('GetProducts', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
route: 'getproducts/{productid}',
extraInputs: [mysqlInput],
handler: async (request, context) => {
const products = JSON.stringify(context.extraInputs.get(mysqlInput));
return {
status: 200,
body: products
};
}
});
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const mysqlInput = input.generic({
commandText: 'DeleteProductsCost',
commandType: 'StoredProcedure',
parameters: '@Cost={cost}',
connectionStringSetting: 'MySqlConnectionString',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log('HTTP trigger and MySQL input binding function processed a request.');
const products = context.extraInputs.get(mysqlInput);
return {
jsonBody: products,
};
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraInputs: [mysqlInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const mysqlInput = input.generic({
type: 'mysql',
commandText: 'DeleteProductsCost',
commandType: 'StoredProcedure',
parameters: '@Cost={cost}',
connectionStringSetting: 'MySqlConnectionString'
})
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
route: 'DeleteProductsByCost',
extraInputs: [mysqlInput],
handler: async (request, context) => {
const products = JSON.stringify(context.extraInputs.get(mysqlInput));
return {
status: 200,
body: products
};
}
});
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-powershell).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-powershell)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-powershell)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-powershell)

The examples refer to a database table:

```
DROP TABLE IF EXISTS Products;
CREATE TABLE Products (
ProductId int PRIMARY KEY,
Name varchar(100) NULL,
Cost int NULL
);
```


### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a PowerShell function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get"
],
"route": "getproducts/{cost}"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "products",
"type": "mysql",
"direction": "in",
"commandText": "select * from Products",
"commandType": "Text",
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
param($Request, $TriggerMetadata, $products)
Write-Host "PowerShell function with MySql Input Binding processed a request."
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $products
})
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding in a PowerShell function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

The following example is binding data in the function.json file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get"
],
"route": "getproducts/{productid}"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "products",
"type": "mysql",
"direction": "in",
"commandText": "select * from Products where ProductId= @productId",
"commandType": "Text",
"parameters": "MySqlConnectionString",
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
param($Request, $TriggerMetadata, $products)
Write-Host "PowerShell function with MySql Input Binding processed a request."
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $products
})
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a PowerShell function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = 'cost';
END
```


```
{
"bindings": [
{
"authLevel": "function",
"name": "Request",
"type": "httpTrigger",
"direction": "in",
"methods": [
"get"
],
"route": "deleteproducts-storedprocedure/{cost}"
},
{
"name": "response",
"type": "http",
"direction": "out"
},
{
"name": "products",
"type": "mysql",
"direction": "in",
"commandText": "DeleteProductsCost",
"commandType": "StoredProcedure",
"parameters": "@Cost={cost}",
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
param($Request, $TriggerMetadata, $products)
Write-Host "PowerShell function with MySql Input Binding processed a request."
Push-OutputBinding -Name response -Value ([HttpResponseContext]@{
StatusCode = [System.Net.HttpStatusCode]::OK
Body = $products
}
```


More samples for the Azure Database for MySQL input binding are available in the [GitHub repository](https://github.com/Azure/azure-functions-mysql-extension/tree/main/samples/samples-python).

This section contains the following examples:

[HTTP trigger, get multiple rows](#http-trigger-get-multiple-items-python)[HTTP trigger, get a row by ID from a query string](#http-trigger-look-up-id-from-query-string-python)[HTTP trigger, delete rows](#http-trigger-delete-one-or-multiple-rows-python)

The examples refer to a database table:

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

### HTTP trigger, get multiple rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a Python function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query and returns the results in the HTTP response.

The following example is sample Python code for the function_app.py file:

```
import azure.functions as func
import datetime
import json
import logging
app = func.FunctionApp()
@app.generic_trigger(arg_name="req", type="httpTrigger", route="getproducts/{cost}")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_input_binding(arg_name="products", type="mysql",
commandText= "select * from Products",
command_type="Text",
connection_string_setting="MySqlConnectionString")
def mysql_test(req: func.HttpRequest, products: func.MySqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), products))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, get a row by ID from a query string

The following example shows an Azure Database for MySQL input binding in a Python function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding reads from a query filtered by a parameter from the query string and returns the row in the HTTP response.

The following example is sample Python code for the function_app.py file:

```
import azure.functions as func
import datetime
import json
import logging
app = func.FunctionApp()
@app.generic_trigger(arg_name="req", type="httpTrigger", route="getproducts/{cost}")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_input_binding(arg_name="products", type="mysql",
commandText= "select * from Products where ProductId= @productId",
command_type="Text",
parameters= "@productId={productid}",
connection_string_setting="MySqlConnectionString")
def mysql_test(req: func.HttpRequest, products: func.MySqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), products))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, delete rows

The following example shows an Azure Database for MySQL input binding in a function.json file and a Python function that [an HTTP request triggers](functions-bindings-http-webhook-trigger). The binding executes a stored procedure with input from the HTTP request's query parameter.

The stored procedure `DeleteProductsCost`

must be created on the database. In this example, the stored procedure deletes a single record or all records, depending on the value of the parameter.

```
DROP PROCEDURE IF EXISTS DeleteProductsCost;
Create Procedure DeleteProductsCost(cost INT)
BEGIN
DELETE from Products where Products.cost = cost;
END
```


The following example is sample Python code for the function_app.py file:

```
import azure.functions as func
import datetime
import json
import logging
app = func.FunctionApp()
@app.generic_trigger(arg_name="req", type="httpTrigger", route="getproducts/{cost}")
@app.generic_output_binding(arg_name="$return", type="http")
@app.generic_input_binding(arg_name="products", type="mysql",
commandText= "DeleteProductsCost",
command_type="StoredProcedure",
parameters= "@Cost={cost}",
connection_string_setting="MySqlConnectionString")
def mysql_test(req: func.HttpRequest, products: func.MySqlRowList) -> func.HttpResponse:
rows = list(map(lambda r: json.loads(r.to_json()), products))
return func.HttpResponse(
json.dumps(rows),
status_code=200,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the `MySqlAttribute`

attribute to declare the MySQL bindings on the function. The attribute has the following properties:

| Attribute property | Description |
|---|---|
`CommandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`ConnectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
`CommandType` |
Required. A
`CommandType` |

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)

`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)

`StoredProcedure`

`Parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@MySQLInput`

annotation on parameters whose values would come from Azure Database for MySQL. This annotation supports the following elements:

| Element | Description |
|---|---|
`commandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. |
`commandType` |
Required. A
`CommandType` |

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)

`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)

`StoredProcedure`

`name`

`parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `input.generic()`

method:

| Property | Description |
|---|---|
`commandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

`commandType`

[value, which is](/en-us/dotnet/api/system.data.commandtype)`CommandType`

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)`StoredProcedure`

`parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).## Configuration

The following table explains the binding configuration properties that you set in the function.json file:

| Property | Description |
|---|---|
`type` |
Required. Must be set to `mysql` . |
`direction` |
Required. Must be set to `in` . |
`name` |
Required. The name of the variable that represents the query results in function code. |
`commandText` |
Required. The MySQL query command or name of the stored procedure that the binding executes. |
`connectionStringSetting` |
Required. The name of an app setting that contains the connection string for the database against which the query or stored procedure is executed. This value isn't the actual connection string and must instead resolve to an environment variable name. Optional keywords in the connection string value are
|

`commandType`

[value, which is](/en-us/dotnet/api/system.data.commandtype)`CommandType`

[for a query and](/en-us/dotnet/api/system.data.commandtype#fields)`Text`

[for a stored procedure.](/en-us/dotnet/api/system.data.commandtype#fields)`StoredProcedure`

`parameters`

`@param1=param1,@param2=param2`

. The parameter name and parameter value can't contain a comma (`,`

) or an equal sign (`=`

).When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The attribute's constructor takes the MySQL command text, the command type, parameters, and the name of the connection string setting. The command can be a MySQL query with the command type `System.Data.CommandType.Text`

or a stored procedure name with the command type `System.Data.CommandType.StoredProcedure`

. The name of the connection string setting corresponds to the application setting (in local.settings.json for local development) that contains the [connection string](https://dev.mysql.com/doc/connector-net/en/connector-net-connections-string.html) to Azure Database for MySQL.

If an exception occurs when an Azure Database for MySQL input binding is executed, the function code stops running. The result might be an error code, such as an HTTP trigger that returns a 500 error code.


---

<!-- DOCUMENTO FUSIONADO: ___functions-diagnostics_functions-openapi-definition_functions-create-ai-enable_02bde4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-diagnostics_functions-openapi-definition_functions-create-ai-enabled_d7ffdc.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-diagnostics_functions-openapi-definition.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-diagnostics.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-diagnostics -->

# Azure Functions diagnostics overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you’re running a function app, you want to be prepared for any issues that may arise, from 4xx errors to trigger failures. Azure Functions diagnostics is an intelligent and interactive experience to help you troubleshoot your function app with no configuration or extra cost. When you do run into issues with your function app, Azure Functions diagnostics points out what’s wrong. It guides you to the right information to more easily and quickly troubleshoot and resolve the issue. This article shows you the basics of how to use Azure Functions diagnostics to more quickly diagnose and solve common function app issues.

## Start Azure Functions diagnostics

To start Azure Functions diagnostics:

Navigate to your function app in the

[Azure portal](https://portal.azure.com).Select

**Diagnose and solve problems**to open Azure Functions diagnostics.Choose a category that best describes the issue of your function app by using the keywords in the homepage tile. You can also type a keyword that best describes your issue in the search bar. For example, you could type

`execution`

to see a list of diagnostic reports related to your function app execution and open them directly from the homepage.

## Use the Interactive interface

Once you select a homepage category that best aligns with your function app's problem, Azure Functions diagnostics' interactive interface, named Genie, can guide you through diagnosing and solving problem of your app. You can use the tile shortcuts provided by Genie to view the full diagnostic report of the problem category that you're interested in. The tile shortcuts provide you a direct way of accessing your diagnostic metrics.


After selecting a tile, you can see a list of topics related to the issue described in the tile. These topics provide snippets of notable information from the full report. Select any of these topics to investigate the issues further. Also, you can select **View Full Report** to explore all the topics on a single page.


## View a diagnostic report

After you choose a topic, you can view a diagnostic report specific to your function app. Diagnostic reports use status icons to indicate if there are any specific issues with your app. You see detailed description of the issue, recommended actions, related-metrics, and helpful docs. Customized diagnostic reports are generated from a series of checks run on your function app. Diagnostic reports can be a useful tool for pinpointing problems in your function app and guiding you towards resolving the issue.

## Find the problem code

For script-based functions, you can use **Function Execution and Errors** under **Function App Down or Reporting Errors** to narrow down on the line of code causing exceptions or errors. You can use this tool for getting to the root cause and fixing issues from a specific line of code. This option isn't available for precompiled C# and Java functions.


## Next steps

You can ask questions or provide feedback on Azure Functions diagnostics at [UserVoice](https://feedback.azure.com/d365community/forum/9df02822-f224-ec11-b6e6-000d3a4f0da0). Include `[Diag]`

in the title of your feedback.


---

<!-- DOCUMENTO FUSIONADO: functions-openapi-definition.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-openapi-definition -->

# Expose serverless APIs from HTTP endpoints using Azure API Management

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with Azure API Management in the portal to let you expose your HTTP trigger function endpoints as REST APIs. These APIs are described using an OpenAPI definition. This JSON (or YAML) file contains information about what operations are available in an API. It includes details about how the request and response data for the API should be structured. By integrating your function app, you can have API Management generate these OpenAPI definitions.

This article shows you how to integrate your function app with API Management. This integration works for function apps developed in any [supported language](supported-languages). You can also [import your function app from Azure API Management](../api-management/import-function-app-as-api).

For C# class library functions, you can also [use Visual Studio](openapi-apim-integrate-visual-studio) to create and publish serverless API that integrate with API Management.

## Create the API Management instance

To create an API Management instance linked to your function app:

Select the function app, choose

**API Management**from the left menu, and then select**Create new**under**API Management**.Use the API Management settings as specified in the following table:

Setting Suggested value Description **Subscription**Your subscription The subscription under which this new resource is created. [Resource group](../azure-resource-manager/management/overview)myResourceGroup The same resource as your function app, which should get set for you. **Region**Location of the service Consider choosing the same location as your function app. **Resource name**Globally unique name A name is generated based on the name of your function app. **Organization name**Contoso The name of the organization used in the developer portal and for email notifications. **Administrator email**your email Email that received system notifications from API Management. **Pricing tier**Consumption Consumption tier isn't available in all regions. For complete pricing details, see the [API Management pricing page](https://azure.microsoft.com/pricing/details/api-management/)Choose

**Review + create**and then**Create**to create the API Management instance, which may take several minutes.

## Import functions

After the API Management instance is created, you can import your HTTP triggered function endpoints. This example imports an endpoint named TurbineRepair.

In the API Management page, select

**Link API**.The

**Import Azure Functions**opens with the**TurbineRepair**function highlighted. Choose**Select**to continue.In the

**Create from Function App**page, accept the defaults, and then select**Create**. Azure creates the API for the function.

## Download the OpenAPI definition

After your functions have been imported, you can download the OpenAPI definition from the API Management instance.

Select

**Download OpenAPI definition**at the top of the page.Save the downloaded JSON file, and then open it. Review the definition.


## Next steps

You can now refine the definition in API Management in the portal. You can also [learn more about API Management](../api-management/api-management-key-concepts).


---

<!-- DOCUMENTO FUSIONADO: functions-create-ai-enabled-apps.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-ai-enabled-apps -->

# Use AI tools and models in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides serverless compute resources that integrate with AI and Azure services to streamline building cloud-hosted intelligent applications. This article provides a survey of the breadth of AI-related scenarios, integrations, and other AI resources that you can use in your function apps.

Consider using Azure Functions in your AI-enabled experiences for these scenarios:

| Scenario | Description |
|---|---|
|

[Agentic workflows](#agentic-workflows)[Retrieval-augmented generation (RAG)](#retrieval-augmented-generation)Select one of these scenarios to learn more in this article.

This article is language-specific, so make sure you choose your programming language at the [top of the page](#top).

## Tools and MCP servers

AI models and agents use *function calling* to request external resources known as *tools*. Function calling lets models and agents dynamically invoke specific functionality based on the context of a conversation or task.

Functions is particularly well-suited for implementing function calling in agentic workflows because it efficiently scales to handle demand and provides [binding extensions](functions-triggers-bindings) that simplify connecting agents with remote Azure services. When you build or host AI tools in Functions, you also get serverless pricing models and platform security features.

The Model Context Protocol (MCP) is the industry standard for interacting with remote servers. It provides a standardized way for AI models and agents to communicate with external systems. An MCP server lets these AI clients efficiently determine the tools and capabilities of an external system.

Azure Functions currently supports exposing your function code by using these types of tools:

| Tool type | Description |
|---|---|
|

[Queue-based Azure Functions tool](#queue-based-azure-functions-tools)### Remote MCP servers

Functions supports these options for creating and hosting remote MCP servers:

- Use the
[MCP binding extension](functions-bindings-mcp)to create and host custom MCP servers as you would any other function app. - Self host MCP servers created by using the official MCP SDKs.
*This hosting option is currently in preview.*

Here's a comparison of the current MCP server hosting options provided by Functions:

| Feature |
|
|---|

*[Functions triggers and bindings](functions-triggers-bindings)Python

TypeScript

JavaScript

Java

Python

TypeScript

Java

[MCP binding extension](functions-bindings-mcp)[Custom handlers](functions-custom-handlers)*Configuration details for self-hosted MCP servers change during the preview.

Here are some options to help you get started hosting MCP servers in Functions:

| Options | MCP binding extensions | Self-hosted MCP servers |
|---|---|---|
| Documentation |
|

[Remote custom MCP server](https://github.com/Azure-Samples/remote-mcp-functions-dotnet)[Weather server](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-dotnet)[HelloTool](https://github.com/Azure/azure-functions-templates/tree/dev/Functions.Templates/Templates/McpToolTrigger-CSharp-Isolated)| Options | MCP binding extensions | Self-hosted MCP servers |
|---|---|---|
| Documentation |
|

[Remote custom MCP server](https://github.com/Azure-Samples/remote-mcp-functions-python)[Weather server](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-python)| Options | MCP binding extensions | Self-hosted MCP servers |
|---|---|---|
| Documentation |
|

[Remote custom MCP server](https://github.com/Azure-Samples/remote-mcp-functions-typescript)[Weather server](https://github.com/Azure-Samples/mcp-sdk-functions-hosting-node)| Options | MCP binding extensions | Self-hosted MCP servers |
|---|---|---|
| Documentation |
|

| Options | MCP binding extensions | Self-hosted MCP servers |
|---|---|---|
| Documentation |
|

PowerShell isn't currently supported for either MCP server hosting option.

### Queue-based Azure Functions tools

In addition to MCP servers, you can implement AI tools by using Azure Functions with queue-based communication. Azure AI Foundry provides Azure Functions-specific tools that enable asynchronous function calling by using message queues. With these tools, AI agents interact with your code by using messaging patterns.

This tool approach is ideal for AI Foundry scenarios that require:

- Reliable message delivery and processing
- Decoupling between AI agents and function execution
- Built-in retry and error handling capabilities
- Integration with existing Azure messaging infrastructure

Here are some reference samples for function calling scenarios:

Uses an

[Azure AI Foundry Agent Service]client to call a custom remote MCP server implemented by using Azure Functions.

Uses function calling features for agents in Azure AI SDKs to implement custom function calling.


## Agentic workflows

AI-driven processes often determine how to interact with models and other AI assets. However, some scenarios require a higher level of predictability or well-defined steps. These directed agentic workflows orchestrate separate tasks or interactions that agents must follow.

The [Durable Functions extension](durable/durable-functions-overview) helps you take advantage of the strengths of Functions to create multistep, long-running operations with built-in fault tolerance. These workflows work well for your directed agentic workflows. For example, a trip planning solution might first gather requirements from the user, search for plan options, obtain user approval, and finally make required bookings. In this scenario, you can build an agent for each step and then coordinate their actions as a workflow using Durable Functions.

For more workflow scenario ideas, see [Application patterns](durable/durable-functions-overview#application-patterns) in Durable Functions.

## Retrieval-augmented generation

Because Functions can handle multiple events from various data sources simultaneously, it's an effective solution for real-time AI scenarios, like RAG systems that require fast data retrieval and processing. Rapid event-driven scaling reduces the latency your customers experience, even in high-demand situations.

Here are some reference samples for RAG-based scenarios:

For RAG, you can use SDKs, including Azure Open AI and Azure SDKs, to build your scenarios. ::: zone-end


Shows you how to create a friendly chat bot that issues simple prompts, receives text completions, and sends messages, all in a stateful session using the

[OpenAI binding extension].

## AI tools and frameworks for Azure Functions

Functions lets you build apps in your preferred language and use your favorite libraries. Because of this flexibility, you can use a wide range of AI libraries and frameworks in your AI-enabled function apps.

Here are some key Microsoft AI frameworks you should be aware of:

| Framework/library | Description |
|---|---|
|

[Azure AI Foundry Agent Service](/en-us/azure/ai-foundry/agents/overview)[Azure AI Services SDKs](/en-us/azure/ai-foundry/)Functions also lets your apps reference third-party libraries and frameworks, so you can use all of your favorite AI tools and libraries in your AI-enabled functions.


---

<!-- DOCUMENTO FUSIONADO: functions-premium-plan.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-premium-plan -->

# Azure Functions Premium plan

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Functions Elastic Premium plan is a dynamic scale hosting option for function apps. For other hosting plan options, see [Azure Functions hosting options](functions-scale).

Important

Azure Functions can run on the Azure App Service platform. In the App Service platform, plans that host Premium plan function apps are referred to as *Elastic* Premium plans, with SKU names like `EP1`

. If you choose to run your function app on a Premium plan, make sure to create a plan with an SKU name that starts with "E", such as `EP1`

. App Service plan SKU names that start with "P", such as `P1V2`

(Premium V2 Small plan), are actually [Dedicated hosting plans](dedicated-plan). Because they are Dedicated and not Elastic Premium, plans with SKU names starting with "P" won't scale dynamically and may increase your costs.

Premium plan hosting provides the following benefits for your functions:

*Always ready*and*prewarmed*instances to avoid cold starts- Virtual network connectivity
- Support for
[longer runtime durations](#longer-run-duration) [Choice of Premium instance sizes](#available-instance-skus)- More predictable pricing, compared with the Consumption plan
- High-density app allocation for plans with multiple function apps
- Support for
[Linux container deployments](container-concepts)

When you use the Premium plan, you add and remove instances of the Azure Functions host based on the number of incoming events, just like the [Flex Consumption plan](flex-consumption-plan) and the [Consumption plan](consumption-plan). You can deploy multiple function apps to the same Premium plan. You can configure the compute instance size, base plan size, and maximum plan size.

## Billing

You pay for the Premium plan based on the number of core seconds and memory allocated across instances. This billing model differs from the Consumption plan, which bills you based on per-second resource consumption and executions. The Premium plan has no execution charge. This billing model results in a minimum monthly cost per active plan, whether the function is active or idle. All function apps in a Premium plan share allocated instances. For more information, see [Azure Functions pricing](https://azure.microsoft.com/pricing/details/functions/).

Note

Every premium plan always has at least one active (billed) instance.

## Create a Premium plan

When you create a function app in the Azure portal, the Consumption plan is the default. To create a function app that runs in a Premium plan, you must explicitly create or choose an Azure Functions Premium hosting plan by using one of the *Elastic Premium* versions. You host the function app you create in this plan. The Azure portal makes it easy to create both the Premium plan and the function app at the same time. You can run more than one function app in the same Premium plan, but they must both run on the same operating system (Windows or Linux).

The following articles show you how to programmatically create a function app with a Premium plan:

## Eliminate cold starts

When events or executions don't occur in the Consumption plan, your app might scale to zero instances. When new events arrive, the system must create a new instance that runs your app. Specializing new instances takes time, depending on the app. This extra latency on the first call is often called a [cold start](event-driven-scaling#cold-start).

The Premium plan provides two features that work together to effectively eliminate cold starts in your functions: *always ready instances* and *prewarmed instances*. Always ready instances are a category of preallocated instances unaffected by scaling, and the prewarmed instances are a buffer as you scale due to HTTP events.

When events begin to trigger the app, the system first routes them to the always ready instances. As the function becomes active due to HTTP events, other instances warm as a buffer. These buffered instances are called prewarmed instances. This buffer reduces cold start for new instances required during scale.

### Always ready instances

In the Premium plan, you can have your app always ready on a specified number of instances. Your app runs continuously on those instances, regardless of load. If load exceeds what your always ready instances can handle, the app adds more instances as necessary, up to your specified maximum.

This app-level setting also controls your plan's minimum instances. For example, consider three function apps in the same Premium plan. When two of your apps have always ready instance count set to one, and the third app is set to five, the minimum number for your whole plan is five. This number also reflects the minimum number of instances for which your plan is billed. The maximum number of always ready instances supported per app is 20.

You can configure the number of always ready instances in the Azure portal by selecting your **Function App**, going to the **App Service plan** > **Scale Out** menu option on the left, and editing the **App Scale out** options. In the function app edit window, always ready instances are specific to that app.

### Prewarmed instances

The prewarmed instance count setting provides warmed instances as a buffer during HTTP scale and activation events. Prewarmed instances continue to buffer until the maximum scale-out limit is reached. The default prewarmed instance count is 1 and, for most scenarios, keep this value as 1.

Consider a less common scenario, such as an app running in a custom container. Because custom containers have a long warm-up time, you might consider increasing this buffer of prewarmed instances. A prewarmed instance becomes active only after all active instances are in use.

You can also define a warmup trigger that runs during the prewarming process. You can use a warmup trigger to preload custom dependencies during the prewarming process so your functions are ready to start processing requests immediately. To learn more, see [Azure Functions warmup trigger](functions-bindings-warmup).

Consider this example that shows how always ready instances and prewarmed instances work together. A premium function app has two always ready instances configured, and the default of one prewarmed instance.


- When the app is idle and no events are triggering, the app is provisioned and running with two instances. At this time, you're billed for the two always ready instances but aren't billed for a prewarmed instance because no prewarmed instance is allocated.
- As your application starts receiving HTTP traffic, requests are load balanced across the two always ready instances. As soon as those two instances start processing events, an instance is added to fill the prewarmed buffer. The app is now running with three provisioned instances: the two always ready instances, and the third prewarmed and inactive buffer. You're billed for the three instances.
- As load increases and your app needs more instances to handle HTTP traffic, that prewarmed instance swaps to an active instance. HTTP load is now routed to all three instances, and a fourth instance is instantly provisioned to fill the prewarmed buffer.
- This sequence of scaling and prewarming continues until the maximum instance count for the app is reached or load decreases causing the platform to scale back in after a period. No instances are prewarmed or activated beyond the maximum.

You can't change the prewarmed instance count setting in the portal. You must instead use the Azure CLI or Azure PowerShell.

### Maximum function app instances

In addition to the [plan maximum burst count](#plan-and-sku-settings), you can configure a per-app maximum. You configure the app maximum by using the [app scale limit](event-driven-scaling#limit-scale-out). The maximum app scale-out limit can't exceed the maximum burst instances of the plan.

## Private network connectivity

Function apps deployed to a Premium plan can take advantage of [virtual network integration for web apps](../app-service/overview-vnet-integration). When configured, your app can communicate with resources within your virtual network or secured via service endpoints. You can also use IP restrictions on the app to restrict incoming traffic.

When assigning a subnet to your function app in a Premium plan, you need a subnet with enough IP addresses for each potential instance. You need an IP block with at least 100 available addresses.

For more information, see [Integrate Azure Functions with a virtual network](functions-create-vnet).

## Rapid elastic scale

The same rapid scaling logic as the Flex Consumption and Consumption plans automatically adds more compute instances for your app. Apps in the same App Service Plan scale independently from one another based on the needs of an individual app. However, Functions apps in the same App Service Plan share VM resources to help reduce costs, when possible. The number of apps associated with a VM depends on the footprint of each app and the size of the VM.

To learn more about how scaling works, see [Event-driven scaling in Azure Functions](event-driven-scaling).

## Longer run duration

Functions in a Consumption plan are limited to 10 minutes for a single execution. In the Premium plan, the run duration defaults to 30 minutes to prevent runaway executions. However, you can [modify the host.json configuration](functions-host-json#functiontimeout) to make the duration unbounded for Premium plan apps, with the following limitations:

- Platform upgrades can trigger a managed shutdown and halt the function execution with a grace period of 10 minutes.
- An idle timer stops the worker after 60 minutes with no new executions.
[Scale-in behavior](event-driven-scaling#scale-in-behaviors)can cause worker shutdown after 60 minutes.[Slot swaps](functions-deployment-slots)can terminate executions on the source and target slots during the swap.

## Migration

If you have an existing function app, you can use Azure CLI commands to migrate your app between a Consumption plan and a Premium plan on Windows. The specific commands depend on the direction of the migration. For more information, see [Plan migration](functions-how-to-use-azure-function-app-settings#plan-migration).

This migration isn't supported on Linux.

## Premium plan settings

When you create the plan, you set two plan size settings: the minimum number of instances (or plan size) and the maximum burst limit.

If your app needs more instances beyond the always ready instances, it can continue to scale out until the number of instances reaches the plan maximum burst limit, or the app maximum scale-out limit if you set it. You pay for instances only while they're running and allocated to you, on a per-second basis. The platform makes its best effort at scaling your app out to the defined maximum limits.

You can configure the plan size in the Azure portal by selecting your **Function App** deployed to that plan, going to the **App Service plan** > **Scale Up** menu options on the left, and choosing a larger plan size. To increase the maximum burst limit, choose the **Scale Out** menu option and edit the **Plan Scale out** > **Maximum burst** option.

The minimum for every Premium plan is at least one instance. The actual minimum number of instances is determined based on the always ready instances requested by apps in the plan. For example, if app A requests five always ready instances, and app B requests two always ready instances in the same plan, the minimum plan size is determined as five. App A runs on all five instances, and app B runs on two.

Important

You're charged for each instance allocated in the minimum instance count whether or not functions are executing.

In most circumstances, this autocalculated minimum is sufficient. However, scaling beyond the minimum occurs at a best effort. It's possible, though unlikely, that at a specific time scale-out could be delayed if other instances are unavailable. By setting a minimum higher than the autocalculated minimum, you reserve instances in advance of scale-out.

You can configure the minimum instances in the Azure portal by selecting your **Function App** deployed to that plan, going to the **App Service plan** > **Scale Out** menu option on the left, and editing the **Plan Scale out** > **Minimum Instances** option.

### Available instance SKUs

When you create or scale your plan, choose from three instance sizes. You're billed for the total number of cores and memory you provision, per second for each instance allocated to you. Your app can automatically scale out to multiple instances as needed.

| SKU | Cores | Memory | Storage |
|---|---|---|---|
| EP1 | 1 | 3.5 GB | 250 GB |
| EP2 | 2 | 7 GB | 250 GB |
| EP3 | 4 | 14 GB | 250 GB |

### Memory usage considerations

Running on a machine with more memory doesn't always mean that your function app uses all available memory.

For example, a JavaScript function app is constrained by the default memory limit in Node.js. To increase this fixed memory limit, add the app setting `languageWorkers:node:arguments`

with a value of `--max-old-space-size=<max memory in MB>`

.

For plans with more than 4 GB of memory, set the Bitness Platform Setting to `64 Bit`

under [General settings](../app-service/configure-common#configure-general-settings).

## Region max scale-out

The following table lists currently supported maximum scale-out values for a single plan in each region and OS configuration:

| Region | Windows | Linux |
|---|---|---|
| Australia Central | 100 | 20 |
| Australia Central 2 | 100 | Not Available |
| Australia East | 100 | 40 |
| Australia Southeast | 100 | 20 |
| Brazil South | 100 | 20 |
| Canada Central | 100 | 100 |
| Central India | 100 | 20 |
| Central US | 100 | 100 |
| China East 2 | 20 | 20 |
| China North 2 | 20 | 20 |
| China North 3 | 20 | 20 |
| East Asia | 100 | 20 |
| East US | 100 | 100 |
| East US 2 | 80 | 100 |
| France Central | 100 | 60 |
| Germany West Central | 100 | 20 |
| Israel Central | 100 | 20 |
| Italy North | 100 | 20 |
| Japan East | 100 | 20 |
| Japan West | 100 | 20 |
| Jio India West | 100 | 20 |
| Korea Central | 100 | 20 |
| Korea South | 40 | 20 |
| Mexico Central | 20 | 20 |
| North Central US | 100 | 20 |
| North Europe | 100 | 100 |
| Norway East | 100 | 20 |
| South Africa North | 100 | 20 |
| South Africa West | 20 | 20 |
| South Central US | 100 | 100 |
| South India | 100 | Not Available |
| Southeast Asia | 100 | 20 |
| Spain Central | 20 | 20 |
| Switzerland North | 100 | 20 |
| Switzerland West | 100 | 20 |
| UAE North | 100 | 100 |
| UK South | 100 | 100 |
| UK West | 100 | 20 |
| USGov Arizona | 20 | 20 |
| USGov Texas | 20 | Not Available |
| USGov Virginia | 80 | 20 |
| West Central US | 100 | 20 |
| West Europe | 100 | 100 |
| West India | 100 | 20 |
| West US | 100 | 100 |
| West US 2 | 100 | 20 |
| West US 3 | 100 | 20 |

For more information, see [Products available by region](https://azure.microsoft.com/global-infrastructure/services/?products=functions).


---

<!-- DOCUMENTO FUSIONADO: functions-reference-node.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reference-node -->

# Azure Functions Node.js developer guide

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This guide is an introduction to developing Azure Functions using JavaScript or TypeScript. The article assumes that you have already read the [Azure Functions developer guide](functions-reference).

Important

The content of this article changes based on your choice of the Node.js programming model in the selector at the top of this page. The version you choose should match the version of the [ @azure/functions](https://www.npmjs.com/package/@azure/functions) npm package you're using in your app. If you don't have that package listed in your

`package.json`

, the default is v3. Learn more about the differences between v3 and v4 in the [migration guide](functions-node-upgrade-v4).

As a Node.js developer, you might also be interested in one of the following articles:

| Getting started | Concepts | Guided learning |
|---|---|---|

## Considerations

- The Node.js programming model shouldn't be confused with the Azure Functions runtime:
**Programming model**: Defines how you author your code and is specific to JavaScript and TypeScript.**Runtime**: Defines underlying behavior of Azure Functions and is shared across all languages.

- The version of the programming model is strictly tied to the version of the
npm package. It's versioned independently of the`@azure/functions`

[runtime](functions-versions). Both the runtime and the programming model use the number 4 as their latest major version, but that's a coincidence. - You can't mix the v3 and v4 programming models in the same function app. As soon as you register one v4 function in your app, any v3 functions registered in
*function.json*files are ignored.

## Supported versions

The following table shows each version of the Node.js programming model along with its supported versions of the Azure Functions runtime and Node.js.

|
|---|

[Functions Runtime Version](functions-versions)

[Node.js Version](https://github.com/nodejs/release#release-schedule)

[Functions Versions](functions-versions)for more info.[Functions Versions](functions-versions)for more info.## Folder structure

The required folder structure for a JavaScript project looks like the following example:

```
<project_root>/
| - .vscode/
| - node_modules/
| - myFirstFunction/
| | - index.js
| | - function.json
| - mySecondFunction/
| | - index.js
| | - function.json
| - .funcignore
| - host.json
| - local.settings.json
| - package.json
```


The main project folder, *<project_root>*, can contain the following files:

**.vscode/**: (Optional) Contains the stored Visual Studio Code configuration. To learn more, see[Visual Studio Code settings](https://code.visualstudio.com/docs/getstarted/settings).**myFirstFunction/function.json**: Contains configuration for the function's trigger, inputs, and outputs. The name of the directory determines the name of your function.**myFirstFunction/index.js**: Stores your function code. To change this default file path, see[using scriptFile](#using-scriptfile).**.funcignore**: (Optional) Declares files that shouldn't get published to Azure. Usually, this file contains*.vscode/*to ignore your editor setting,*test/*to ignore test cases, and*local.settings.json*to prevent local app settings being published.**host.json**: Contains configuration options that affect all functions in a function app instance. This file does get published to Azure. Not all options are supported when running locally. To learn more, see[host.json](functions-host-json).**local.settings.json**: Used to store app settings and connection strings when it's running locally. This file doesn't get published to Azure. To learn more, see[local.settings.file](functions-develop-local#local-settings-file).**package.json**: Contains configuration options like a list of package dependencies, the main entrypoint, and scripts.

The recommended folder structure for a JavaScript project looks like the following example:

```
<project_root>/
| - .vscode/
| - node_modules/
| - src/
| | - functions/
| | | - myFirstFunction.js
| | | - mySecondFunction.js
| - test/
| | - functions/
| | | - myFirstFunction.test.js
| | | - mySecondFunction.test.js
| - .funcignore
| - host.json
| - local.settings.json
| - package.json
```


The main project folder, *<project_root>*, can contain the following files:

**.vscode/**: (Optional) Contains the stored Visual Studio Code configuration. To learn more, see[Visual Studio Code settings](https://code.visualstudio.com/docs/getstarted/settings).**src/functions/**: The default location for all functions and their related triggers and bindings.**test/**: (Optional) Contains the test cases of your function app.**.funcignore**: (Optional) Declares files that shouldn't get published to Azure. Usually, this file contains*.vscode/*to ignore your editor setting,*test/*to ignore test cases, and*local.settings.json*to prevent local app settings being published.**host.json**: Contains configuration options that affect all functions in a function app instance. This file does get published to Azure. Not all options are supported when running locally. To learn more, see[host.json](functions-host-json).**local.settings.json**: Used to store app settings and connection strings when it's running locally. This file doesn't get published to Azure. To learn more, see[local.settings.file](functions-develop-local#local-settings-file).**package.json**: Contains configuration options like a list of package dependencies, the main entrypoint, and scripts.

## Registering a function

The v3 model registers a function based on the existence of two files. First, you need a `function.json`

file located in a folder one level down from the root of your app. Second, you need a JavaScript file that [exports](https://nodejs.org/api/modules.html#modules_module_exports) your function. By default, the model looks for an `index.js`

file in the same folder as your `function.json`

. If you're using TypeScript, you must use the [ scriptFile](#using-scriptfile) property in

`function.json`

to point to the compiled JavaScript file. To customize the file location or export name of your function, see [configuring your function's entry point](functions-reference-node#configure-function-entry-point).

The function you export should always be declared as an [ async function](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Statements/async_function) in the v3 model. You can export a synchronous function, but then you must call

[to signal that your function is completed, which is deprecated and not recommended.](#contextdone)

`context.done()`

Your function is passed an [invocation context](#invocation-context) as the first argument and your

[inputs](#inputs)as the remaining arguments.

The following example is a simple function that logs that it was triggered and responds with `Hello, world!`

:

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"name": "req",
"authLevel": "anonymous",
"methods": ["get", "post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
}
]
}
```


```
module.exports = async function (context, request) {
context.log("Http function was triggered.");
context.res = { body: "Hello, world!" };
};
```


The programming model loads your functions based on the `main`

field in your `package.json`

. You can set the `main`

field to a single file or multiple files by using a [glob pattern](https://wikipedia.org/wiki/Glob_(programming)). The following table shows example values for the `main`

field:

| Example | Description |
|---|---|
`src/index.js` |
Register functions from a single root file. |
`src/functions/*.js` |
Register each function from its own file. |
`src/{index.js,functions/*.js}` |
A combination where you register each function from its own file, but you still have a root file for general app-level code. |

In order to register a function, you must import the `app`

object from the `@azure/functions`

npm module and call the method specific to your trigger type. The first argument when registering a function is the function name. The second argument is an `options`

object specifying configuration for your trigger, your handler, and any other inputs or outputs. In some cases where trigger configuration isn't necessary, you can pass the handler directly as the second argument instead of an `options`

object.

Registering a function can be done from any file in your project, as long as that file is loaded (directly or indirectly) based on the `main`

field in your `package.json`

file. The function should be registered at a global scope because you can't register functions once executions start.

The following example is a simple function that logs that it was triggered and responds with `Hello, world!`

:

```
const { app } = require("@azure/functions");
app.http("helloWorld1", {
methods: ["POST", "GET"],
handler: async (request, context) => {
context.log("Http function was triggered.");
return { body: "Hello, world!" };
},
});
```


## Inputs and outputs

Your function is required to have exactly one primary input called the trigger. It might also have secondary inputs and/or outputs. Inputs and outputs are configured in your `function.json`

files and are also referred to as [bindings](functions-triggers-bindings).

### Inputs

Inputs are bindings with `direction`

set to `in`

. The main difference between a trigger and a secondary input is that the `type`

for a trigger ends in `Trigger`

, for example type [ blobTrigger](functions-bindings-storage-blob-trigger) vs type

[. Most functions only use a trigger, and not many secondary input types are supported.](functions-bindings-storage-blob-input)

`blob`

Inputs can be accessed in several ways:

Use the arguments in the same order that they're defined in*[Recommended]*As arguments passed to your function:`function.json`

. The`name`

property defined in`function.json`

doesn't need to match the name of your argument, although we recommend it for the sake of organization.`module.exports = async function (context, myTrigger, myInput, myOtherInput) { ... };`


**As properties of**Use the key matching the:`context.bindings`

`name`

property defined in`function.json`

.`module.exports = async function (context) { context.log("This is myTrigger: " + context.bindings.myTrigger); context.log("This is myInput: " + context.bindings.myInput); context.log("This is myOtherInput: " + context.bindings.myOtherInput); };`


### Outputs

Outputs are bindings with `direction`

set to `out`

and can be set in several ways:

If you're using an async function, you can return the value directly. You must change the*[Recommended for single output]*Return the value directly:`name`

property of the output binding to`$return`

in`function.json`

like in the following example:`{ "name": "$return", "type": "http", "direction": "out" }`

`module.exports = async function (context, request) { return { body: "Hello, world!", }; };`


If you're using an async function, you can return an object with a property matching the name of each binding in your*[Recommended for multiple outputs]*Return an object containing all outputs:`function.json`

. The following example uses output bindings named "httpResponse" and "queueOutput":`{ "name": "httpResponse", "type": "http", "direction": "out" }, { "name": "queueOutput", "type": "queue", "direction": "out", "queueName": "helloworldqueue", "connection": "storage_APPSETTING" }`

`module.exports = async function (context, request) { let message = "Hello, world!"; return { httpResponse: { body: message, }, queueOutput: message, }; };`


**Set values on**If you're not using an async function or you don't want to use the previous options, you can set values directly on`context.bindings`

:`context.bindings`

, where the key matches the name of the binding. The following example uses output bindings named "httpResponse" and "queueOutput":`{ "name": "httpResponse", "type": "http", "direction": "out" }, { "name": "queueOutput", "type": "queue", "direction": "out", "queueName": "helloworldqueue", "connection": "storage_APPSETTING" }`

`module.exports = async function (context, request) { let message = "Hello, world!"; context.bindings.httpResponse = { body: message, }; context.bindings.queueOutput = message; };`


### Bindings data type

You can use the `dataType`

property on an input binding to change the type of your input. However, the approach has some limitations:

- In Node.js, only
`string`

and`binary`

are supported (`stream`

isn't) - For HTTP inputs, the
`dataType`

property is ignored. Instead, use properties on the`request`

object to get the body in your desired format. For more information, see[HTTP request](#http-request).

In the following example of a [storage queue trigger](functions-bindings-storage-queue-trigger), the default type of `myQueueItem`

is a `string`

, but if you set `dataType`

to `binary`

, the type changes to a Node.js `Buffer`

.

```
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"queueName": "helloworldqueue",
"connection": "storage_APPSETTING",
"dataType": "binary"
}
```


```
const { Buffer } = require("node:buffer");
module.exports = async function (context, myQueueItem) {
if (typeof myQueueItem === "string") {
context.log("myQueueItem is a string");
} else if (Buffer.isBuffer(myQueueItem)) {
context.log("myQueueItem is a buffer");
}
};
```


Your function is required to have exactly one primary input called the trigger. It might also have secondary inputs, a primary output called the return output, and/or secondary outputs. Inputs and outputs are also referred to as [bindings](functions-triggers-bindings) outside the context of the Node.js programming model. Before v4 of the model, these bindings were configured in `function.json`

files.

### Trigger input

The trigger is the only required input or output. For most trigger types, you register a function by using a method on the `app`

object named after the trigger type. You can specify configuration specific to the trigger directly on the `options`

argument. For example, an HTTP trigger allows you to specify a route. During execution, the value corresponding to this trigger is passed in as the first argument to your handler.

```
const { app } = require('@azure/functions');
app.http('helloWorld1', {
route: 'hello/world',
handler: async (request, context) => {
...
}
});
```


### Return output

The return output is optional, and in some cases configured by default. For example, an HTTP trigger registered with `app.http`

is configured to return an HTTP response output automatically. For most output types, you specify the return configuration on the `options`

argument with the help of the `output`

object exported from the `@azure/functions`

module. During execution, you set this output by returning it from your handler.

The following example uses a [timer trigger](functions-bindings-timer) and a [storage queue output](functions-bindings-storage-queue-output):

```
const { app, output } = require('@azure/functions');
app.timer('timerTrigger1', {
schedule: '0 */5 * * * *',
return: output.storageQueue({
connection: 'storage_APPSETTING',
...
}),
handler: (myTimer, context) => {
return { hello: 'world' }
}
});
```


### Extra inputs and outputs

In addition to the trigger and return, you might specify extra inputs or outputs on the `options`

argument when registering a function. The `input`

and `output`

objects exported from the `@azure/functions`

module provide type-specific methods to help construct the configuration. During execution, you get or set the values with `context.extraInputs.get`

or `context.extraOutputs.set`

, passing in the original configuration object as the first argument.

The following example is a function triggered by a [storage queue](functions-bindings-storage-queue-trigger), with an extra [storage blob input](functions-bindings-storage-blob-input) that is copied to an extra [storage blob output](functions-bindings-storage-blob-output). The queue message should be the name of a file and replaces `{queueTrigger}`

as the blob name to be copied, with the help of a [binding expression](functions-bindings-expressions-patterns).

```
const { app, input, output } = require("@azure/functions");
const blobInput = input.storageBlob({
connection: "storage_APPSETTING",
path: "helloworld/{queueTrigger}",
});
const blobOutput = output.storageBlob({
connection: "storage_APPSETTING",
path: "helloworld/{queueTrigger}-copy",
});
app.storageQueue("copyBlob1", {
queueName: "copyblobqueue",
connection: "storage_APPSETTING",
extraInputs: [blobInput],
extraOutputs: [blobOutput],
handler: (queueItem, context) => {
const blobInputValue = context.extraInputs.get(blobInput);
context.extraOutputs.set(blobOutput, blobInputValue);
},
});
```


### Generic inputs and outputs

The `app`

, `trigger`

, `input`

, and `output`

objects exported by the `@azure/functions`

module provide type-specific methods for most types. For all the types that aren't supported, a `generic`

method is provided to allow you to manually specify the configuration. The `generic`

method can also be used if you want to change the default settings provided by a type-specific method.

The following example is a simple HTTP triggered function using generic methods instead of type-specific methods.

```
const { app, output, trigger } = require("@azure/functions");
app.generic("helloWorld1", {
trigger: trigger.generic({
type: "httpTrigger",
methods: ["GET", "POST"],
}),
return: output.generic({
type: "http",
}),
handler: async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
return { body: `Hello, world!` };
},
});
```


## SDK types

Several binding extensions now enable you to work directly with the Azure SDK types.

### Azure Blob storage

SDK bindings capability in Azure Functions enables you to work directly with the Azure Blob storage SDK types like `BlobClient`

and `ContainerClient`

instead of raw data. This provides full access to all SDK methods when working with blobs.

To configure your project to work with SDK types:

- Add the
`@azure/functions-extensions-blob`

extension preview packages to the`package.json`

file in the project, which should include at least these packages:

```
"dependencies": {
"@azure/functions": "4.7.2-preview",
"@azure/functions-extensions-blob": "0.2.0-preview"
},
```


- Add
`enableHttpStream: true`

in your`app.setup`

to support streaming types:

```
import { app } from '@azure/functions';
app.setup({
enableHttpStream: true,
});
```


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


Keep these considerations in mind when working with SDK types:

- Always have
`import "@azure/functions-extensions-blob"`

first in your files to ensure side effects run. - Set
`sdkBinding: true`

in your binding configuration. - Use the appropriate client type for your operation:
`blobClient`

for operations on a single blob`containerClient`

for operations on a container

- Handle errors appropriately with
`try`

/`catch`

blocks - For large blob operations, consider using streaming methods to avoid memory issues.

For more information, see these [Blob Storage SDK Bindings for Node.js Samples](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-nodejs):
for more examples on how to incorporate SDK Bindings for Blob into your function app.

### Azure Service Bus

This example uses the SDK type [ ServiceBusReceivedMessage](/en-us/javascript/api/@azure/service-bus/servicebusreceivedmessage) obtained from

`ServiceBusMessageContext`

provided by the Service Bus trigger:```
import '@azure/functions-extensions-servicebus'; // Ensure the Service Bus extension is imported
import { app, InvocationContext } from '@azure/functions';
import { ServiceBusMessageContext } from '@azure/functions-extensions-servicebus';
//This a SDKbinding = true
export async function serviceBusQueueTrigger(
serviceBusMessageContext: ServiceBusMessageContext,
context: InvocationContext
): Promise<void> {
const message = serviceBusMessageContext.messages[0];
context.log(message);
// Get current retry count from custom properties, default to 0
const currentRetryCount = message.applicationProperties?.retryCnt ? parseInt(message.applicationProperties.retryCnt as string) : 0;
context.log(`Current retry count: ${currentRetryCount}`);
if (currentRetryCount >= 3) {
// After 3 retries, complete the message to remove it from the queue
context.log(`Maximum retry count (3) reached. Completing message to prevent infinite loop.`);
await serviceBusMessageContext.actions.complete(message);
context.log('Message completed after maximum retries');
} else {
// Abandon with updated retry count
const newRetryCount = currentRetryCount + 1;
const propertiesToModify = {
retryCnt: newRetryCount.toString(),
lastRetryTime: new Date().toISOString(),
errorMessage: "Processing failed"
};
context.log(`Abandoning message with retry count: ${newRetryCount}`);
await serviceBusMessageContext.actions.abandon(message, propertiesToModify);
}
context.log('triggerMetadata: ', context.triggerMetadata);
context.log('Message body:', message.body);
}
app.serviceBusQueue('serviceBusQueueTrigger1', {
connection: 'ServiceBusConnection',
queueName: 'testqueue',
sdkBinding: true,
autoCompleteMessages: false,
cardinality: 'many',
handler: serviceBusQueueTrigger,
});
```


For another example using SDK types see the [exponential backoff strategy sample](https://github.com/Azure/azure-functions-nodejs-extensions/blob/main/azure-functions-nodejs-extensions-servicebus/samples/serviceBusTriggerExponentialBackOff/src/functions/serviceBusTopicTrigger.ts).

## Invocation context

Each invocation of your function is passed an invocation `context`

object, used to read inputs, set outputs, write to logs, and read various metadata. In the v3 model, the context object is always the first argument passed to your handler.

The `context`

object has the following properties:

| Property | Description |
|---|---|
`invocationId` |
The ID of the current function invocation. |
`executionContext` |
See
|

`bindings`

[bindings](#contextbindings).`bindingData`

[event hub trigger](functions-bindings-event-hubs-trigger)has an`enqueuedTimeUtc`

property.`traceContext`

[.](https://www.w3.org/TR/trace-context/)`Trace Context`

`bindingDefinitions`

`function.json`

.`req`

[HTTP request](#http-request).`res`

[HTTP response](#http-response).### context.executionContext

The `context.executionContext`

object has the following properties:

| Property | Description |
|---|---|
`invocationId` |
The ID of the current function invocation. |
`functionName` |
The name of the function that is being invoked. The name of the folder containing the `function.json` file determines the name of the function. |
`functionDirectory` |
The folder containing the `function.json` file. |
`retryContext` |
See
|

#### context.executionContext.retryContext

The `context.executionContext.retryContext`

object has the following properties:

| Property | Description |
|---|---|
`retryCount` |
A number representing the current retry attempt. |
`maxRetryCount` |
Maximum number of times an execution is retried. A value of `-1` means to retry indefinitely. |
`exception` |
Exception that caused the retry. |

### context.bindings

The `context.bindings`

object is used to read inputs or set outputs. The following example is a [storage queue trigger](functions-bindings-storage-queue-trigger), which uses `context.bindings`

to copy a [storage blob input](functions-bindings-storage-blob-input) to a [storage blob output](functions-bindings-storage-blob-output). The queue message's content replaces `{queueTrigger}`

as the file name to be copied, with the help of a [binding expression](functions-bindings-expressions-patterns).

```
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"connection": "storage_APPSETTING",
"queueName": "helloworldqueue"
},
{
"name": "myInput",
"type": "blob",
"direction": "in",
"connection": "storage_APPSETTING",
"path": "helloworld/{queueTrigger}"
},
{
"name": "myOutput",
"type": "blob",
"direction": "out",
"connection": "storage_APPSETTING",
"path": "helloworld/{queueTrigger}-copy"
}
```


```
module.exports = async function (context, myQueueItem) {
const blobValue = context.bindings.myInput;
context.bindings.myOutput = blobValue;
};
```


### context.done

The `context.done`

method is deprecated. Before async functions were supported, you would signal your function is done by calling `context.done()`

:

```
module.exports = function (context, request) {
context.log("this pattern is now deprecated");
context.done();
};
```


We recommend that you remove the call to `context.done()`

and mark your function as async so that it returns a promise (even if you don't `await`

anything). As soon as your function finishes (in other words, the returned promise resolves), the v3 model knows your function is done.

```
module.exports = async function (context, request) {
context.log("you don't need context.done or an awaited call");
};
```


Each invocation of your function is passed an invocation `context`

object, with information about your invocation and methods used for logging. In the v4 model, the `context`

object is typically the second argument passed to your handler.

The `InvocationContext`

class has the following properties:

| Property | Description |
|---|---|
`invocationId` |
The ID of the current function invocation. |
`functionName` |
The name of the function. |
`extraInputs` |
Used to get the values of extra inputs. For more information, see
|

`extraOutputs`

[extra inputs and outputs](#extra-inputs-and-outputs).`retryContext`

[retry context](#retry-context).`traceContext`

[.](https://www.w3.org/TR/trace-context/)`Trace Context`

`triggerMetadata`

[event hub trigger](functions-bindings-event-hubs-trigger)has an`enqueuedTimeUtc`

property.`options`

### Retry context

The `retryContext`

object has the following properties:

| Property | Description |
|---|---|
`retryCount` |
A number representing the current retry attempt. |
`maxRetryCount` |
Maximum number of times an execution is retried. A value of `-1` means to retry indefinitely. |
`exception` |
Exception that caused the retry. |

For more information, see [ retry-policies](functions-bindings-errors#retry-policies).

## Logging

In Azure Functions, it's recommended to use `context.log()`

to write logs. Azure Functions integrates with Azure Application Insights to better capture your function app logs. Application Insights, part of Azure Monitor, provides facilities for collection, visual rendering, and analysis of both application logs and your trace outputs. To learn more, see [monitoring Azure Functions](functions-monitoring).

Note

If you use the alternative Node.js `console.log`

method, those logs are tracked at the app-level and will *not* be associated with any specific function. We *highly recommend* that your use `context`

for logging instead of `console`

so that all logs are associated with a specific function.

The following example writes a log at the default "information" level, including the invocation ID:

```
context.log(`Something has happened. Invocation ID: "${context.invocationId}"`);
```


### Log levels

In addition to the default `context.log`

method, the following methods are available that let you write logs at specific levels:

| Method | Description |
|---|---|
`context.log.error()` |
Writes an error-level event to the logs. |
`context.log.warn()` |
Writes a warning-level event to the logs. |
`context.log.info()` |
Writes an information-level event to the logs. |
`context.log.verbose()` |
Writes a trace-level event to the logs. |

| Method | Description |
|---|---|
`context.trace()` |
Writes a trace-level event to the logs. |
`context.debug()` |
Writes a debug-level event to the logs. |
`context.info()` |
Writes an information-level event to the logs. |
`context.warn()` |
Writes a warning-level event to the logs. |
`context.error()` |
Writes an error-level event to the logs. |

### Configure log level

Azure Functions lets you define the threshold level to be used when tracking and viewing logs. To set the threshold, use the `logging.logLevel`

property in the `host.json`

file. This property lets you define a default level applied to all functions, or a threshold for each individual function. To learn more, see [How to configure monitoring for Azure Functions](configure-monitoring).

## Track custom data

By default, Azure Functions writes output as traces to Application Insights. For more control, you can instead use the [Application Insights Node.js SDK](https://github.com/microsoft/applicationinsights-node.js) to send custom data to your Application Insights instance.

```
const appInsights = require("applicationinsights");
appInsights.setup();
const client = appInsights.defaultClient;
module.exports = async function (context, request) {
// Use this with 'tagOverrides' to correlate custom logs to the parent function invocation.
var operationIdOverride = {
"ai.operation.id": context.traceContext.traceparent,
};
client.trackEvent({
name: "my custom event",
tagOverrides: operationIdOverride,
properties: { customProperty2: "custom property value" },
});
client.trackException({
exception: new Error("handled exceptions can be logged with this method"),
tagOverrides: operationIdOverride,
});
client.trackMetric({
name: "custom metric",
value: 3,
tagOverrides: operationIdOverride,
});
client.trackTrace({
message: "trace message",
tagOverrides: operationIdOverride,
});
client.trackDependency({
target: "http://dbname",
name: "select customers proc",
data: "SELECT * FROM Customers",
duration: 231,
resultCode: 0,
success: true,
dependencyTypeName: "ZSQL",
tagOverrides: operationIdOverride,
});
client.trackRequest({
name: "GET /customers",
url: "http://myserver/customers",
duration: 309,
resultCode: 200,
success: true,
tagOverrides: operationIdOverride,
});
};
```


The `tagOverrides`

parameter sets the `operation_Id`

to the function's invocation ID. This setting enables you to correlate all of the automatically generated and custom logs for a given function invocation.

## HTTP triggers

HTTP and webhook triggers use request and response objects to represent HTTP messages.

HTTP and webhook triggers use `HttpRequest`

and `HttpResponse`

objects to represent HTTP messages. The classes represent a subset of the [fetch standard](https://developer.mozilla.org/docs/Web/API/fetch), using Node.js's [ undici](https://undici.nodejs.org/) package.

### HTTP Request

The request can be accessed in several ways:

**As the second argument to your function:**`module.exports = async function (context, request) { context.log(`Http function processed request for url "${request.url}"`);`


**From the**`context.req`

property:`module.exports = async function (context, request) { context.log(`Http function processed request for url "${context.req.url}"`);`


**From the named input bindings:**This option works the same as any non HTTP binding. The binding name in`function.json`

must match the key on`context.bindings`

, or "request1" in the following example:`{ "name": "request1", "type": "httpTrigger", "direction": "in", "authLevel": "anonymous", "methods": ["get", "post"] }`

`module.exports = async function (context, request) { context.log(`Http function processed request for url "${context.bindings.request1.url}"`);`


The `HttpRequest`

object has the following properties:

| Property | Type | Description |
|---|---|---|
`method` |
`string` |
HTTP request method used to invoke this function. |
`url` |
`string` |
Request URL. |
`headers` |
`Record<string, string>` |
HTTP request headers. This object is case sensitive. It's recommended to use `request.getHeader('header-name')` instead, which is case insensitive. |
`query` |
`Record<string, string>` |
Query string parameter keys and values from the URL. |
`params` |
`Record<string, string>` |
Route parameter keys and values. |
`user` |
`HttpRequestUser \| null` |
Object representing logged-in user, either through Functions authentication, SWA Authentication, or null when no such user is logged in. |
`body` |
`Buffer \| string \| any` |
If the media type is "application/octet-stream" or "multipart/*", `body` is a Buffer. If the value is a JSON parse-able string, `body` is the parsed object. Otherwise, `body` is a string. |
`rawBody` |
`string` |
The body as a string. Despite the name, this property doesn't return a Buffer. |
`bufferBody` |
`Buffer` |
The body as a buffer. |

The request can be accessed as the first argument to your handler for an HTTP triggered function.

```
async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
```


The `HttpRequest`

object has the following properties:

| Property | Type | Description |
|---|---|---|
`method` |
`string` |
HTTP request method used to invoke this function. |
`url` |
`string` |
Request URL. |
`headers` |
`Headers` |

`query`

`URLSearchParams`

`params`

`Record<string, string>`

`user`

`HttpRequestUser \| null`

`body`

`ReadableStream \| null`

`bodyUsed`

`boolean`

In order to access a request or response's body, the following methods can be used:

| Method | Return Type |
|---|---|
`arrayBuffer()` |
`Promise<ArrayBuffer>` |

`blob()`

`Promise<Blob>`

`formData()`

`Promise<FormData>`

`json()`

`Promise<unknown>`

`text()`

`Promise<string>`

Note

The body functions can be run only once. Subsequent calls resolve with empty strings/ArrayBuffers.

### HTTP Response

The response can be set in several ways:

**Set the**`context.res`

property:`module.exports = async function (context, request) { context.res = { body: `Hello, world!` };`


**Return the response:**If your function is async and you set the binding name to`$return`

in your`function.json`

, you can return the response directly instead of setting it on`context`

.`{ "type": "http", "direction": "out", "name": "$return" }`

`module.exports = async function (context, request) { return { body: `Hello, world!` };`


**Set the named output binding:**This option works the same as any non HTTP binding. The binding name in`function.json`

must match the key on`context.bindings`

, or "response1" in the following example:`{ "type": "http", "direction": "out", "name": "response1" }`

`module.exports = async function (context, request) { context.bindings.response1 = { body: `Hello, world!` };`


**Call**This option is deprecated. It implicitly calls`context.res.send()`

:`context.done()`

and can't be used in an async function.`module.exports = function (context, request) { context.res.send(`Hello, world!`);`


If you create a new object when setting the response, that object must match the `HttpResponseSimple`

interface, which has the following properties:

| Property | Type | Description |
|---|---|---|
`headers` |
`Record<string, string>` (optional) |
HTTP response headers. |
`cookies` |
`Cookie[]` (optional) |
HTTP response cookies. |
`body` |
`any` (optional) |
HTTP response body. |
`statusCode` |
`number` (optional) |
HTTP response status code. If not set, defaults to `200` . |
`status` |
`number` (optional) |
The same as `statusCode` . This property is ignored if `statusCode` is set. |

You can also modify the `context.res`

object without overwriting it. The default `context.res`

object uses the `HttpResponseFull`

interface, which supports the following methods in addition to the `HttpResponseSimple`

properties:

| Method | Description |
|---|---|
`status()` |
Sets the status. |
`setHeader()` |
Sets a header field. NOTE: `res.set()` and `res.header()` are also supported and do the same thing. |
`getHeader()` |
Get a header field. NOTE: `res.get()` is also supported and does the same thing. |
`removeHeader()` |
Removes a header. |
`type()` |
Sets the "content-type" header. |
`send()` |
This method is deprecated. It sets the body and calls `context.done()` to indicate a sync function is finished. NOTE: `res.end()` is also supported and does the same thing. |
`sendStatus()` |
This method is deprecated. It sets the status code and calls `context.done()` to indicate a sync function is finished. |
`json()` |
This method is deprecated. It sets the "content-type" to "application/json", sets the body, and calls `context.done()` to indicate a sync function is finished. |

The response can be set in several ways:

**As a simple interface with type**This option is the most concise way of returning responses.`HttpResponseInit`

:`return { body: `Hello, world!` };`


The `HttpResponseInit`

interface has the following properties:

| Property | Type | Description |
|---|---|---|
`body` |
`BodyInit` (optional) |
HTTP response body as one of
`ArrayBuffer` |

[,](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array)

`AsyncIterable<Uint8Array>`

[,](https://developer.mozilla.org/docs/Web/API/Blob)

`Blob`

[,](https://developer.mozilla.org/docs/Web/API/FormData)

`FormData`

[,](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/Uint8Array)

`Iterable<Uint8Array>`

[,](https://developer.mozilla.org/docs/Web/JavaScript/Reference/Global_Objects/ArrayBuffer)

`NodeJS.ArrayBufferView`

[,](https://developer.mozilla.org/docs/Web/API/URLSearchParams)

`URLSearchParams`

`null`

, or `string`

.`jsonBody`

`any`

(optional)`HttpResponseInit.body`

property is ignored in favor of this property.`status`

`number`

(optional)`200`

.`headers`

[(optional)](https://developer.mozilla.org/docs/Web/API/Headers)`HeadersInit`

`cookies`

`Cookie[]`

(optional)**As a class with type**This option provides helper methods for reading and modifying various parts of the response like the headers.`HttpResponse`

:`const response = new HttpResponse({ body: `Hello, world!` }); response.headers.set("content-type", "application/json"); return response;`


The `HttpResponse`

class accepts an optional `HttpResponseInit`

as an argument to its constructor and has the following properties:

| Property | Type | Description |
|---|---|---|
`status` |
`number` |
HTTP response status code. |
`headers` |
`Headers` |

`cookies`

`Cookie[]`

`body`

`ReadableStream | null`

`bodyUsed`

`boolean`

## HTTP streams

HTTP streams is a feature that makes it easier to process large data, stream OpenAI responses, deliver dynamic content, and support other core HTTP scenarios. It lets you stream requests to and responses from HTTP endpoints in your Node.js function app. Use HTTP streams in scenarios where your app requires real-time exchange and interaction between client and server over HTTP. You can also use HTTP streams to get the best performance and reliability for your apps when using HTTP.

Important

HTTP streams aren't supported in the v3 model. [Upgrade to the v4 model](functions-node-upgrade-v4) to use the HTTP streaming feature.
The existing `HttpRequest`

and `HttpResponse`

types in programming model v4 already support various ways of handling the message body, including as a stream.

### Prerequisites

- The
version 4.3.0 or later.`@azure/functions`

npm package [Azure Functions runtime](functions-versions)version 4.28 or later.[Azure Functions Core Tools](functions-run-local)version 4.0.5530 or a later version, which contains the correct runtime version.

### Enable streams

Use these steps to enable HTTP streams in your function app in Azure and in your local projects:

If you plan to stream large amounts of data, modify the

setting in Azure. The default maximum body size allowed is`FUNCTIONS_REQUEST_BODY_SIZE_LIMIT`

`104857600`

, which limits your requests to a size of ~100 MB.For local development, also add

`FUNCTIONS_REQUEST_BODY_SIZE_LIMIT`

to the[local.settings.json file](functions-develop-local#local-settings-file).Add the following code to your app in any file included by your

[main field](functions-reference-node#registering-a-function).`const { app } = require("@azure/functions"); app.setup({ enableHttpStream: true });`


### Stream examples

This example shows an HTTP triggered function that receives data via an HTTP POST request, and the function streams this data to a specified output file:

```
const { app } = require('@azure/functions');
const { createWriteStream } = require('fs');
const { Writable } = require('stream');
app.http('httpTriggerStreamRequest', {
methods: ['POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
const writeStream = createWriteStream('<output file path>');
await request.body.pipeTo(Writable.toWeb(writeStream));
return { body: 'Done!' };
},
});
```


This example shows an HTTP triggered function that streams a file's content as the response to incoming HTTP GET requests:

```
const { app } = require('@azure/functions');
const { createReadStream } = require('fs');
app.http('httpTriggerStreamResponse', {
methods: ['GET'],
authLevel: 'anonymous',
handler: async (request, context) => {
const body = createReadStream('<input file path>');
return { body };
},
});
```


For a ready-to-run sample app using streams, check out this example on [GitHub](https://github.com/Azure-Samples/azure-functions-nodejs-stream).

### Stream considerations

- Use
`request.body`

to obtain the maximum benefit from using streams. You can still continue to use methods like`request.text()`

, which always return the body as a string.

## Hooks

Hooks aren't supported in the v3 model. [Upgrade to the v4 model](functions-node-upgrade-v4) to use hooks.

Use a hook to execute code at different points in the Azure Functions lifecycle. Hooks are executed in the order they're registered and can be registered from any file in your app. There are currently two scopes of hooks, "app" level and "invocation" level.

### Invocation hooks

Invocation hooks are executed once per invocation of your function, either before in a `preInvocation`

hook or after in a `postInvocation`

hook. By default your hook executes for all trigger types, but you can also filter by type. The following example shows how to register an invocation hook and filter by trigger type:

```
const { app } = require('@azure/functions');
app.hook.preInvocation((context) => {
if (context.invocationContext.options.trigger.type === 'httpTrigger') {
context.invocationContext.log(
`preInvocation hook executed for http function ${context.invocationContext.functionName}`
);
}
});
app.hook.postInvocation((context) => {
if (context.invocationContext.options.trigger.type === 'httpTrigger') {
context.invocationContext.log(
`postInvocation hook executed for http function ${context.invocationContext.functionName}`
);
}
});
```


The first argument to the hook handler is a context object specific to that hook type.

The `PreInvocationContext`

object has the following properties:

| Property | Description |
|---|---|
`inputs` |
The arguments passed to the invocation. |
`functionHandler` |
The function handler for the invocation. Changes to this value affect the function itself. |
`invocationContext` |
The
|

`hookData`

The `PostInvocationContext`

object has the following properties:

| Property | Description |
|---|---|
`inputs` |
The arguments passed to the invocation. |
`result` |
The result of the function. Changes to this value affect the overall result of the function. |
`error` |
The error thrown by the function, or null/undefined if there's no error. Changes to this value affect the overall result of the function. |
`invocationContext` |
The
|

`hookData`

### App hooks

App hooks are executed once per instance of your app, either during startup in an `appStart`

hook or during termination in an `appTerminate`

hook. App terminate hooks have a limited time to execute and don't execute in all scenarios.

The Azure Functions runtime currently [doesn't support](https://github.com/Azure/azure-functions-host/issues/8222) context logging outside of an invocation. Use the Application Insights [npm package](https://www.npmjs.com/package/applicationinsights) to log data during app level hooks.

The following example registers app hooks:

```
const { app } = require('@azure/functions');
app.hook.appStart((context) => {
// add your logic here
});
app.hook.appTerminate((context) => {
// add your logic here
});
```


The first argument to the hook handler is a context object specific to that hook type.

The `AppStartContext`

object has the following properties:

| Property | Description |
|---|---|
`hookData` |
The recommended place to store and share data between hooks in the same scope. You should use a unique property name so that it doesn't conflict with other hooks' data. |

The `AppTerminateContext`

object has the following properties:

| Property | Description |
|---|---|
`hookData` |
The recommended place to store and share data between hooks in the same scope. You should use a unique property name so that it doesn't conflict with other hooks' data. |

## Scaling and concurrency

By default, Azure Functions automatically monitors the load on your application and creates more host instances for Node.js as needed. Azure Functions uses built-in (not user configurable) thresholds for different trigger types to decide when to add instances, such as the age of messages and queue size for QueueTrigger. For more information, see [How the Consumption and Premium plans work](event-driven-scaling).

This scaling behavior is sufficient for many Node.js applications. For CPU-bound applications, you can improve performance further by using multiple language worker processes. You can increase the number of worker processes per host from the default of 1 up to a max of 10 by using the [FUNCTIONS_WORKER_PROCESS_COUNT](functions-app-settings#functions_worker_process_count) application setting. Azure Functions then tries to evenly distribute simultaneous function invocations across these workers. This behavior makes it less likely that a CPU-intensive function blocks other functions from running. The setting applies to each host that Azure Functions creates when scaling out your application to meet demand.

Warning

Use the `FUNCTIONS_WORKER_PROCESS_COUNT`

setting with caution. Multiple processes running in the same instance can lead to unpredictable behavior and increase function load times. If you use this setting, we *highly recommend* that you offset these downsides by [running from a package file](run-functions-from-deployment-package).

## Node version

You can see the current version that the runtime is using by logging `process.version`

from any function. See [ supported versions](#supported-versions) for a list of Node.js versions supported by each programming model.

### Setting the Node version

The way that you upgrade your Node.js version depends on the OS on which your function app runs.

When it runs on Windows, the Node.js version is set by the [ WEBSITE_NODE_DEFAULT_VERSION](functions-app-settings#website_node_default_version) application setting. This setting can be updated either by using the Azure CLI or in the Azure portal.

For more information about Node.js versions, see [Supported versions](#supported-versions).

Before upgrading your Node.js version, make sure your function app is running on the latest version of the Azure Functions runtime. If you need to upgrade your runtime version, see [Migrate apps from Azure Functions version 3.x to version 4.x](migrate-version-3-version-4?pivots=programming-language-javascript).

Run the Azure CLI [ az functionapp config appsettings set](/en-us/cli/azure/functionapp/config#az-functionapp-config-appsettings-set) command to update the Node.js version for your function app running on Windows:

```
az functionapp config appsettings set --settings WEBSITE_NODE_DEFAULT_VERSION=~22 \
--name <FUNCTION_APP_NAME> --resource-group <RESOURCE_GROUP_NAME>
```


This sets the [ WEBSITE_NODE_DEFAULT_VERSION application setting](functions-app-settings#website_node_default_version) the supported LTS version of

`~22`

.After changes are made, your function app restarts. To learn more about Functions support for Node.js, see [Language runtime support policy](language-support-policy).

## Environment variables

Environment variables can be useful for operational secrets (connection strings, keys, endpoints, etc.) or environmental settings such as profiling variables. You can add environment variables in both your local and cloud environments and access them through `process.env`

in your function code.

The following example logs the `WEBSITE_SITE_NAME`

environment variable:

```
module.exports = async function (context) {
context.log(`WEBSITE_SITE_NAME: ${process.env["WEBSITE_SITE_NAME"]}`);
};
```


```
async function timerTrigger1(myTimer, context) {
context.log(`WEBSITE_SITE_NAME: ${process.env["WEBSITE_SITE_NAME"]}`);
}
```


### In local development environment

When you run locally, your functions project includes a [ local.settings.json file](functions-run-local), where you store your environment variables in the

`Values`

object.```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "",
"FUNCTIONS_WORKER_RUNTIME": "node",
"CUSTOM_ENV_VAR_1": "hello",
"CUSTOM_ENV_VAR_2": "world"
}
}
```


### In Azure cloud environment

When you run in Azure, the function app lets you set and use [Application settings](functions-app-settings), such as service connection strings, and exposes these settings as environment variables during execution.

There are several ways that you can add, update, and delete function app settings:

Changes to function app settings require your function app to be restarted.

### Worker environment variables

There are several Functions environment variables specific to Node.js:

#### languageWorkers**node**arguments

This setting allows you to specify custom arguments when starting your Node.js process. It's most often used locally to start the worker in debug mode, but can also be used in Azure if you need custom arguments.

Warning

If possible, avoid using `languageWorkers__node__arguments`

in Azure because it can have a negative effect on cold start times. Rather than using prewarmed workers, the runtime has to start a new worker from scratch with your custom arguments.

#### logging**logLevel**Worker

This setting adjusts the default log level for Node.js-specific worker logs. By default, only warning or error logs are shown, but you can set it to `information`

or `debug`

to help diagnose issues with the Node.js worker. For more information, see [configuring log levels](configure-monitoring#configure-log-levels).

## ECMAScript modules (preview)

Note

As ECMAScript modules are currently a preview feature in Node.js 14 or higher in Azure Functions.

[ECMAScript modules](https://nodejs.org/docs/latest-v14.x/api/esm.html#esm_modules_ecmascript_modules) (ES modules) are the new official standard module system for Node.js. So far, the code samples in this article use the CommonJS syntax. When running Azure Functions in Node.js 14 or higher, you can choose to write your functions using ES modules syntax.

To use ES modules in a function, change its filename to use a `.mjs`

extension. The following *index.mjs* file example is an HTTP triggered function that uses ES modules syntax to import the `uuid`

library and return a value.

```
import { v4 as uuidv4 } from "uuid";
async function httpTrigger1(context, request) {
context.res.body = uuidv4();
}
export default httpTrigger;
```


```
import { v4 as uuidv4 } from "uuid";
async function httpTrigger1(request, context) {
return { body: uuidv4() };
}
app.http("httpTrigger1", {
methods: ["GET", "POST"],
handler: httpTrigger1,
});
```


## Configure function entry point

The `function.json`

properties `scriptFile`

and `entryPoint`

can be used to configure the location and name of your exported function. The `scriptFile`

property is required when you're using TypeScript and should point to the compiled JavaScript.

### Using `scriptFile`


By default, a JavaScript function is executed from `index.js`

, a file that shares the same parent directory as its corresponding `function.json`

.

`scriptFile`

can be used to get a folder structure that looks like the following example:

```
<project_root>/
| - node_modules/
| - myFirstFunction/
| | - function.json
| - lib/
| | - sayHello.js
| - host.json
| - package.json
```


The `function.json`

for `myFirstFunction`

should include a `scriptFile`

property pointing to the file with the exported function to run.

```
{
"scriptFile": "../lib/sayHello.js",
"bindings": [
...
]
}
```


### Using `entryPoint`


In the v3 model, a function must be exported using `module.exports`

in order to be found and run. By default, the function that executes when triggered is the only export from that file, the export named `run`

, or the export named `index`

. The following example sets `entryPoint`

in `function.json`

to a custom value, "logHello":

```
{
"entryPoint": "logHello",
"bindings": [
...
]
}
```


```
async function logHello(context) {
context.log("Hello, world!");
}
module.exports = { logHello };
```


## Local debugging

We recommend that you use VS Code for local debugging, which starts your Node.js process in debug mode automatically and attaches to the process for you. For more information, see [run the function locally](how-to-create-function-vs-code?pivot=programming-language-javascript#run-the-function-locally).

If you're using a different tool for debugging or want to start your Node.js process in debug mode manually, add `"languageWorkers__node__arguments": "--inspect"`

under `Values`

in your [local.settings.json](functions-develop-local#local-settings-file). The `--inspect`

argument tells Node.js to listen for a debug client, on port 9229 by default. For more information, see the [Node.js debugging guide](https://nodejs.org/en/learn/getting-started/debugging).

## Recommendations

This section describes several impactful patterns for Node.js apps that we recommend you follow.

### Choose single-vCPU App Service plans

When you create a function app that uses the App Service plan, we recommend that you select a single-vCPU plan rather than a plan with multiple vCPUs. Today, Functions runs Node.js functions more efficiently on single-vCPU VMs, and using larger VMs doesn't produce the expected performance improvements. When necessary, you can manually scale out by adding more single-vCPU VM instances, or you can enable autoscale. For more information, see [Scale instance count manually or automatically](/en-us/azure/azure-monitor/autoscale/autoscale-get-started?toc=/azure/app-service/toc.json).

### Run from a package file

When you develop Azure Functions in the serverless hosting model, cold starts are a reality. *Cold start* refers to the first time your function app starts after a period of inactivity, taking longer to start up. For Node.js apps with large dependency trees in particular, cold start can be significant. To speed up the cold start process, [run your functions as a package file](run-functions-from-deployment-package) when possible. Many deployment methods use this model by default, but if you're experiencing large cold starts you should check to make sure you're running this way.

### Use a single static client

When you use a service-specific client in an Azure Functions application, don't create a new client with every function invocation because you can hit connection limits. Instead, create a single, static client in the global scope. For more information, see [managing connections in Azure Functions](manage-connections).

### Use `async`

and `await`


When writing Azure Functions in Node.js, you should write code using the `async`

and `await`

keywords. Writing code using `async`

and `await`

instead of callbacks or `.then`

and `.catch`

with Promises helps avoid two common problems:

- Throwing uncaught exceptions that
[crash the Node.js process](https://nodejs.org/api/process.html#process_warning_using_uncaughtexception_correctly), potentially affecting the execution of other functions. - Unexpected behavior, such as missing logs from
`context.log`

, caused by asynchronous calls that aren't properly awaited.

In the following example, the asynchronous method `fs.readFile`

is invoked with an error-first callback function as its second parameter. This code causes both of the issues previously mentioned. An exception that isn't explicitly caught in the correct scope can crash the entire process (issue #1). Returning without ensuring the callback finishes means the http response sometimes has an empty body (issue #2).

```
// DO NOT USE THIS CODE
const { app } = require('@azure/functions');
const fs = require('fs');
app.http('httpTriggerBadAsync', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
let fileData;
fs.readFile('./helloWorld.txt', (err, data) => {
if (err) {
context.error(err);
// BUG #1: This will result in an uncaught exception that crashes the entire process
throw err;
}
fileData = data;
});
// BUG #2: fileData is not guaranteed to be set before the invocation ends
return { body: fileData };
},
});
```


In the following example, the asynchronous method `fs.readFile`

is invoked with an error-first callback function as its second parameter. This code causes both of the issues previously mentioned. An exception that isn't explicitly caught in the correct scope can crash the entire process (issue #1). Calling the deprecated `context.done()`

method outside of the scope of the callback can signal the function is finished before the file is read (issue #2). In this example, calling `context.done()`

too early results in missing log entries starting with `Data from file:`

.

```
// NOT RECOMMENDED PATTERN
const fs = require("fs");
module.exports = function (context) {
fs.readFile("./hello.txt", (err, data) => {
if (err) {
context.log.error("ERROR", err);
// BUG #1: This will result in an uncaught exception that crashes the entire process
throw err;
}
context.log(`Data from file: ${data}`);
// context.done() should be called here
});
// BUG #2: Data is not guaranteed to be read before the Azure Function's invocation ends
context.done();
};
```


Use the `async`

and `await`

keywords to help avoid both of these issues. Most APIs in the Node.js ecosystem have been converted to support promises in some form. For example, starting in v14, Node.js provides an `fs/promises`

API to replace the `fs`

callback API.

In the following example, any unhandled exceptions thrown during the function execution only fail the individual invocation that raised the exception. The `await`

keyword means that steps following `readFile`

only execute after it's complete.

```
// Recommended pattern
const { app } = require('@azure/functions');
const fs = require('fs/promises');
app.http('httpTriggerGoodAsync', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
try {
const fileData = await fs.readFile('./helloWorld.txt');
return { body: fileData };
} catch (err) {
context.error(err);
// This rethrown exception will only fail the individual invocation, instead of crashing the whole process
throw err;
}
},
});
```


With `async`

and `await`

, you also don't need to call the `context.done()`

callback.

```
// Recommended pattern
const fs = require("fs/promises");
module.exports = async function (context) {
let data;
try {
data = await fs.readFile("./hello.txt");
} catch (err) {
context.log.error("ERROR", err);
// This rethrown exception will be handled by the Functions Runtime and will only fail the individual invocation
throw err;
}
context.log(`Data from file: ${data}`);
};
```


## Troubleshoot

See the [Node.js Troubleshoot guide](functions-node-troubleshoot).

## Next steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-best-practices -->

# Best practices for reliable Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions is an event-driven, compute-on-demand service that extends the existing Azure App Service application platform. It adds capabilities to implement code triggered by events occurring in Azure, in a partner service, and in on-premises systems. By using Functions, you can build solutions that connect to data sources or messaging solutions, which makes it easier to process and react to events. Functions runs in Azure data centers, which are complex with many integrated components. In a hosted cloud environment, it's expected that VMs can occasionally restart or move, and systems upgrades occur. Your functions apps also likely depend on external APIs, Azure Services, and other databases, which are also prone to periodic unreliability.

This article details some best practices for designing and deploying efficient function apps that remain healthy and perform well in a cloud-based environment.

## Choose the correct hosting plan

When you create a function app in Azure, you must choose a hosting plan for your app. The plan you choose affects performance, reliability, and cost. Azure Functions provides the following hosting plans:

When possible, use the [Flex Consumption plan](flex-consumption-plan) to host your dynamic scale apps.

In the context of the App Service platform, the *Premium* plan that dynamically hosts your functions is the Elastic Premium plan (EP). Other Dedicated (App Service) plans are called Premium. For more information, see [Azure Functions Premium plan](functions-premium-plan).

The hosting plan you choose determines the following behaviors:

- How your function app scales based on demand and how instance allocation is managed.
- The resources available to each function app instance.
- Support for advanced functionality, such as Azure Virtual Network connectivity.

For more information about choosing the correct hosting plan and a detailed comparison between the plans, see [Azure Functions hosting options](functions-scale).

Choose the correct plan when you create your function app. Functions provides a limited ability to switch your hosting plan, primarily between Consumption and Elastic Premium plans. For more information, see [Plan migration](functions-how-to-use-azure-function-app-settings?tabs=portal#plan-migration).

## Configure storage correctly

Functions requires a storage account be associated with your function app. The Functions host uses the storage account connection for operations such as managing triggers and logging function executions. It's also used when dynamically scaling function apps. For more information, see [Storage considerations for Azure Functions](storage-considerations).

A misconfigured file system or storage account in your function app can affect the performance and availability of your functions. For help with troubleshooting an incorrectly configured storage account, see the [storage troubleshooting](functions-recover-storage-account) article.

### Storage connection settings

Function apps that scale dynamically can run either from an Azure Files endpoint in your storage account or from the file servers associated with your scaled-out instances. This behavior is controlled by the following application settings:

The Premium plan and the Consumption plan on Windows support these settings. The Flex Consumption plan doesn't require these settings and uses a Blob storage container to host deployment packages instead of an Azure Files share.

When you create your function app in the Azure portal or by using Azure CLI or Azure PowerShell, you create these settings for your function app when needed. When you create your resources from an Azure Resource Manager template (ARM template), you need to also include `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

in the template.

On your first deployment using an ARM template, don't include `WEBSITE_CONTENTSHARE`

, which is generated for you.

You can use the following ARM template examples to help correctly configure these settings:

[Consumption plan](https://azure.microsoft.com/resources/templates/function-app-create-dynamic/)[Dedicated plan](https://azure.microsoft.com/resources/templates/function-app-create-dedicated/)[Premium plan with VNET integration](https://azure.microsoft.com/resources/templates/function-premium-vnet-integration/)[Consumption plan with a deployment slot](https://azure.microsoft.com/resources/templates/function-app-create-dynamic-slot/)

Important

The Azure Files service doesn't currently support identity-based connections. The Flex Consumption plan fully supports managed identities. For more information, see [Create an app without Azure Files](storage-considerations#create-an-app-without-azure-files).

### Storage account configuration

When creating a function app, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage. Functions relies on Azure Storage for operations such as managing triggers and logging function executions. The storage account connection string for your function app is found in the `AzureWebJobsStorage`

and `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

application settings.

Keep in mind the following considerations when creating this storage account:

To reduce latency, create the storage account in the same region as the function app.

To improve performance in production, use a separate storage account for each function app. This aspect is especially true with Durable Functions and Event Hubs triggered functions.

For Event Hubs triggered functions, don't use an account with

[Data Lake Storage enabled](https://github.com/Azure/azure-functions-eventhubs-extension/issues/81).

### Handling large data sets

When running on Linux, you can add extra storage by mounting a file share. Mounting a share is a convenient way for a function to process a large existing data set. For more information, see [Mount file shares](storage-considerations#mount-file-shares).

## Organize your functions

As part of your solution, you likely develop and publish multiple functions. These functions are often combined into a single function app, but they can also run in separate function apps. In Premium and Dedicated (App Service) hosting plans, multiple function apps can also share the same resources by running in the same plan. How you group your functions and function apps can affect the performance, scaling, configuration, deployment, and security of your overall solution.

For Consumption and Premium plan, all functions in a function app are dynamically scaled together.

For more information on how to organize your functions, see [Function organization best practices](performance-reliability#function-organization-best-practices).

## Optimize deployments

When you deploy a function app, remember that the unit of deployment for functions in Azure is the function app. You deploy all functions in a function app at the same time, usually from the same deployment package.

Consider these options for a successful deployment:

Have your functions run from the deployment package. This

[run from package approach](run-functions-from-deployment-package)provides the following benefits:- Reduces the risk of file copy locking problems.
- Can be deployed directly to a production app and doesn't trigger a restart.
- All files in the package are available to your app.
- Improves the performance of ARM template deployments.
- Might reduce cold-start times, particularly for JavaScript functions with large npm package trees.

Consider using

[continuous deployment](functions-continuous-deployment)to connect deployments to your source control solution. Continuous deployments also let you run from the deployment package.For

[Premium plan hosting](functions-premium-plan), consider adding a warmup trigger to reduce latency when new instances are added. For more information, see[Azure Functions warm-up trigger](functions-bindings-warmup).To minimize deployment downtime, use deployment slots for Consumption, Premium, and Dedicated plans. Or, configure rolling updates for zero-downtime deployments in the Flex Consumption plan. For more information, see

[Azure Functions deployment slots](functions-deployment-slots)and[site update strategies in Flex Consumption](flex-consumption-site-updates).

## Write robust functions

Follow design principles that help with the general performance and availability of your functions. These principles include:

[Avoid long running functions](performance-reliability#avoid-long-running-functions)[Plan cross-function communication](performance-reliability#cross-function-communication)[Write functions to be stateless](performance-reliability#write-functions-to-be-stateless)[Write defensive functions](performance-reliability#write-defensive-functions)

Transient failures are common in cloud computing, so use a [retry pattern](/en-us/azure/architecture/patterns/retry) when accessing cloud-based resources. Many triggers and bindings already implement retry.

Prioritize integration testing by continuously testing your functions in the context of the full application and in your build automation pipelines.

## Design for security

Consider security during the planning phase, not after your functions are ready. For more information, see [Securing Azure Functions](security-concepts).

## Consider concurrency

As demand builds on your function app because of incoming events, Consumption and Premium plans scale out the function apps. It's important to understand how your function app responds to load and how the triggers can be configured to handle incoming events. For a general overview, see [Event-driven scaling in Azure Functions](event-driven-scaling).

Dedicated (App Service) plans require you to provide scaling for your function apps.

### Worker process count

In some cases, it's more efficient to handle the load by creating multiple processes, called language worker processes, in the instance before scale-out. The [FUNCTIONS_WORKER_PROCESS_COUNT](functions-app-settings#functions_worker_process_count) setting controls the maximum number of language worker processes allowed. The default for this setting is `1`

, which means that multiple processes aren't used. After the maximum number of processes are reached, the function app scales out to more instances to handle the load. This setting doesn't apply for [C# class library functions](functions-dotnet-class-library), which run in the host process.

When you use `FUNCTIONS_WORKER_PROCESS_COUNT`

on a Premium plan or Dedicated (App Service) plan, consider the number of cores provided by your plan. For example, the Premium plan `EP2`

provides two cores, so you should start with a value of `2`

and increase by two as needed, up to the maximum.

### Trigger configuration

When you plan for throughput and scaling, understand how the different types of triggers process events. Some triggers give you control over batching behaviors and concurrency. Adjusting these values can help each instance scale appropriately for the demands of the invoked functions. You apply these configuration options to all triggers in a function app, and maintain them in the host.json file for the app. For settings details, see the Configuration section of the specific trigger reference.

To learn more about how Functions processes message streams, see [Azure Functions reliable event processing](functions-reliable-event-processing).

### Plan for connections

Connection limits apply to function apps running in [Consumption plan](consumption-plan). These limits apply to each instance. Because of these limits and as a general best practice, optimize your outbound connections from your function code. For more information, see [Manage connections in Azure Functions](manage-connections).

### Language-specific considerations

For your language of choice, keep in mind the following considerations:

[Use cancellation tokens](functions-dotnet-class-library?#cancellation-tokens)(in-process only).

## Maximize availability

Cold start is a key consideration for serverless architectures. For more information, see [Cold starts](event-driven-scaling#cold-start). If cold start is a concern for your scenario, see [Understanding serverless cold start](https://azure.microsoft.com/blog/understanding-serverless-cold-start/).

Both Flex Consumption and Premium plans are recommended for reducing cold starts while maintaining dynamic scale. Use the following guidance to reduce cold starts and improve availability in all hosting plans.

| Plan | Guidance |
|---|---|
Flex Consumption plan |
•
•
|

**Premium plan**[Implement a Warmup trigger in your function app](functions-bindings-warmup)•

[Set the values for Always-Ready instances and Max Burst limit](functions-premium-plan#plan-and-sku-settings)•

[Use virtual network trigger support when using non-HTTP triggers on a virtual network](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers)**Dedicated plans**[Run on at least two instances with Azure App Service Health Check enabled](../app-service/monitor-instances-health-check)•

[Implement autoscaling](/en-us/azure/architecture/best-practices/auto-scaling)**Consumption plan**•

[Review the](event-driven-scaling#limit-scale-out)`functionAppScaleLimit`

setting, which can limit scale-out• Check for a Daily Usage Quota (GB-Sec) limit set during development and testing. Consider removing this limit in production environments.

## Monitor effectively

Azure Functions offers built-in integration with Azure Application Insights to monitor your function execution and traces written from your code. For more information, see [Monitor executions in Azure Functions](functions-monitoring). Azure Monitor also provides facilities for monitoring the health of the function app itself. For more information, see [Monitor Azure Functions](monitor-functions).

Be aware of the following considerations when using Application Insights integration to monitor your functions:

Remove the

[AzureWebJobsDashboard](functions-app-settings#azurewebjobsdashboard)application setting. This setting was supported in older versions of Functions. Removing`AzureWebJobsDashboard`

improves the performance of your functions.Review the

[Application Insights logs](analyze-telemetry-data). If data you expect to find is missing, consider adjusting the sampling settings to better capture your monitoring scenario. Use the`excludedTypes`

setting to exclude certain types from sampling, such as`Request`

or`Exception`

. For more information, see[Configure sampling](configure-monitoring?tabs=v2#configure-sampling).

Azure Functions also allows you to [send system-generated and user-generated logs to Azure Monitor Logs](functions-monitor-log-analytics). Integration with Azure Monitor Logs is currently in preview.

## Build in redundancy

Your business needs might require that your functions always be available, even during a data center outage. To learn how to use a multiregional approach to keep your critical functions always running, see [Reliability in Azure Functions](/en-us/azure/reliability/reliability-functions).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-dotnet-dependency-injection -->

# Use dependency injection in .NET Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions supports the dependency injection (DI) software design pattern, which is a technique to achieve [Inversion of Control (IoC)](/en-us/dotnet/standard/modern-web-apps-azure-architecture/architectural-principles#dependency-inversion) between classes and their dependencies.

Dependency injection in Azure Functions is built on the .NET Core Dependency Injection features. Familiarity with

[.NET Core dependency injection](/en-us/aspnet/core/fundamentals/dependency-injection)is recommended. There are differences in how you override dependencies and how configuration values are read with Azure Functions on the Consumption plan.Support for dependency injection begins with Azure Functions 2.x.

Dependency injection patterns differ depending on whether your C# functions run

[in-process](functions-dotnet-class-library)or[out-of-process](dotnet-isolated-process-guide).

Important

The guidance in this article applies only to [C# class library functions](functions-dotnet-class-library), which run in-process with the runtime. This custom dependency injection model doesn't apply to [.NET isolated functions](dotnet-isolated-process-guide), which lets you run .NET functions out-of-process. The .NET isolated worker process model relies on regular ASP.NET Core dependency injection patterns. To learn more, see [Dependency injection](dotnet-isolated-process-guide#dependency-injection) in the .NET isolated worker process guide.

## Prerequisites

Before you can use dependency injection, you must install the following NuGet packages:

[Microsoft.NET.Sdk.Functions](https://www.nuget.org/packages/Microsoft.NET.Sdk.Functions/)package version 1.0.28 or later[Microsoft.Extensions.DependencyInjection](https://www.nuget.org/packages/Microsoft.Extensions.DependencyInjection/)(currently, only version 2.x or later supported)

## Register services

To register services, create a method to configure and add components to an `IFunctionsHostBuilder`

instance. The Azure Functions host creates an instance of `IFunctionsHostBuilder`

and passes it directly into your method.

Warning

For function apps running in the Consumption or Premium plans, modifications to configuration values used in triggers can cause scaling errors. Any changes to these properties by the `FunctionsStartup`

class results in a function app startup error.

Injection of `IConfiguration`

can lead to unexpected behavior. To learn more about adding configuration sources, see [Customizing configuration sources](#customizing-configuration-sources).

To register the method, add the `FunctionsStartup`

assembly attribute that specifies the type name used during startup.

```
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Extensions.DependencyInjection;
[assembly: FunctionsStartup(typeof(MyNamespace.Startup))]
namespace MyNamespace;
public class Startup : FunctionsStartup
{
public override void Configure(IFunctionsHostBuilder builder)
{
builder.Services.AddHttpClient();
builder.Services.AddSingleton<IMyService>((s) => {
return new MyService();
});
builder.Services.AddSingleton<ILoggerProvider, MyLoggerProvider>();
}
}
```


This example uses the [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http/) package required to register an `HttpClient`

at startup.

### Caveats

A series of registration steps run before and after the runtime processes the startup class. Therefore, keep in mind the following items:

*The startup class is meant for only setup and registration.*Avoid using services registered at startup during the startup process. For instance, don't try to log a message in a logger that is being registered during startup. This point of the registration process is too early for your services to be available for use. After the`Configure`

method is run, the Functions runtime continues to register other dependencies, which can affect how your services operate.*The dependency injection container only holds explicitly registered types*. The only services available as injectable types are what are set up in the`Configure`

method. As a result, Functions-specific types like`BindingContext`

and`ExecutionContext`

aren't available during setup or as injectable types.*Configuring ASP.NET authentication isn't supported*. The Functions host configures ASP.NET authentication services to properly expose APIs for core lifecycle operations. Other configurations in a custom`Startup`

class can override this configuration, causing unintended consequences. For example, calling`builder.Services.AddAuthentication()`

can break authentication between the portal and the host, leading to messages such as[Azure Functions runtime is unreachable](functions-recover-storage-account#aspnet-authentication-overrides).

## Use injected dependencies

Constructor injection is used to make your dependencies available in a function. The use of constructor injection requires that you don't use static classes for injected services or for your function classes.

The following sample demonstrates how the `IMyService`

and `HttpClient`

dependencies are injected into an HTTP-triggered function.

```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Extensions.Logging;
using System.Net.Http;
using System.Threading.Tasks;
namespace MyNamespace;
public class MyHttpTrigger
{
private readonly HttpClient _client;
private readonly IMyService _service;
public MyHttpTrigger(IHttpClientFactory httpClientFactory, IMyService service)
{
this._client = httpClientFactory.CreateClient();
this._service = service;
}
[FunctionName("MyHttpTrigger")]
public async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Function, "get", "post", Route = null)] HttpRequest req,
ILogger log)
{
var response = await _client.GetAsync("https://microsoft.com");
var message = _service.GetMessage();
return new OkObjectResult("Response from function with injected dependencies.");
}
}
```


This example uses the [Microsoft.Extensions.Http](https://www.nuget.org/packages/Microsoft.Extensions.Http/) package required to register an `HttpClient`

at startup.

## Service lifetimes

Azure Functions apps provide the same service lifetimes as [ASP.NET Dependency Injection](/en-us/aspnet/core/fundamentals/dependency-injection#service-lifetimes). For a Functions app, the different service lifetimes behave as follows:

**Transient**: Transient services are created upon each resolution of the service.**Scoped**: The scoped service lifetime matches a function execution lifetime. Scoped services are created once per function execution. Later requests for that service during the execution reuse the existing service instance.**Singleton**: The singleton service lifetime matches the host lifetime and is reused across function executions on that instance. Singleton lifetime services are recommended for connections and clients, for example`DocumentClient`

or`HttpClient`

instances.

View or download a [sample of different service lifetimes](https://github.com/Azure/azure-functions-dotnet-extensions/tree/main/src/samples/DependencyInjection/Scopes) on GitHub.

## Logging services

If you need your own logging provider, register a custom type as an instance of [ ILoggerProvider](/en-us/dotnet/api/microsoft.extensions.logging.iloggerfactory), which is available through the

[Microsoft.Extensions.Logging.Abstractions](https://www.nuget.org/packages/Microsoft.Extensions.Logging.Abstractions/)NuGet package.

Application Insights is added by Azure Functions automatically.

Warning

- Don't add
`AddApplicationInsightsTelemetry()`

to the services collection, which registers services that conflict with services provided by the environment. - Don't register your own
`TelemetryConfiguration`

or`TelemetryClient`

if you're using the built-in Application Insights functionality. If you need to configure your own`TelemetryClient`

instance, create one via the injected`TelemetryConfiguration`

as shown in[Log custom telemetry in C# functions](functions-dotnet-class-library?tabs=v2,cmd#log-custom-telemetry-in-c-functions).

### ILogger<T> and ILoggerFactory

The host injects `ILogger<T>`

and `ILoggerFactory`

services into constructors. However, by default these new logging filters are filtered out of the function logs. You need to modify the `host.json`

file to opt in to extra filters and categories.

The following example demonstrates how to add an `ILogger<HttpTrigger>`

with logs that are exposed to the host.

```
namespace MyNamespace;
public class HttpTrigger
{
private readonly ILogger<HttpTrigger> _log;
public HttpTrigger(ILogger<HttpTrigger> log)
{
_log = log;
}
[FunctionName("HttpTrigger")]
public async Task<IActionResult> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)] HttpRequest req)
{
_log.LogInformation("C# HTTP trigger function processed a request.");
// ...
}
```


The following example `host.json`

file adds the log filter.

```
{
"version": "2.0",
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
},
"logLevel": {
"MyNamespace.HttpTrigger": "Information"
}
}
}
```


For more information about log levels, see [Configure log levels](configure-monitoring#configure-log-levels).

## Function app provided services

The function host registers many services. The following services are safe to take as a dependency in your application:

| Service Type | Lifetime | Description |
|---|---|---|
`Microsoft.Extensions.Configuration.IConfiguration` |
Singleton | Runtime configuration |
`Microsoft.Azure.WebJobs.Host.Executors.IHostIdProvider` |
Singleton | Responsible for providing the ID of the host instance |

If there are other services you want to take a dependency on, [create an issue and propose them on GitHub](https://github.com/azure/azure-functions-host).

### Overriding host services

Overriding services provided by the host is currently not supported. If there are services you want to override, [create an issue and propose them on GitHub](https://github.com/azure/azure-functions-host).

## Working with options and settings

Values defined in [app settings](functions-how-to-use-azure-function-app-settings#settings) are available in an `IConfiguration`

instance, which allows you to read app settings values in the startup class.

You can extract values from the `IConfiguration`

instance into a custom type. Copying the app settings values to a custom type makes it easy test your services by making these values injectable. Settings read into the configuration instance must be simple key/value pairs. For functions running in an Elastic Premium plan, application setting names can only contain letters, numbers (`0-9`

), periods (`.`

), colons (`:`

) and underscores (`_`

). For more information, see [App setting considerations](functions-app-settings#app-setting-considerations).

Consider the following class that includes a property named consistent with an app setting:

```
public class MyOptions
{
public string MyCustomSetting { get; set; }
}
```


And a `local.settings.json`

file that might structure the custom setting as follows:

```
{
"IsEncrypted": false,
"Values": {
"MyOptions:MyCustomSetting": "Foobar"
}
}
```


From inside the `Startup.Configure`

method, you can extract values from the `IConfiguration`

instance into your custom type using the following code:

```
builder.Services.AddOptions<MyOptions>()
.Configure<IConfiguration>((settings, configuration) =>
{
configuration.GetSection("MyOptions").Bind(settings);
});
```


Calling `Bind`

copies values that have matching property names from the configuration into the custom instance. The options instance is now available in the IoC container to inject into a function.

The options object is injected into the function as an instance of the generic `IOptions`

interface. Use the `Value`

property to access the values found in your configuration.

```
using System;
using Microsoft.Extensions.Options;
public class HttpTrigger
{
private readonly MyOptions _settings;
public HttpTrigger(IOptions<MyOptions> options)
{
_settings = options.Value;
}
}
```


For more information, see [Options pattern in ASP.NET Core](/en-us/aspnet/core/fundamentals/configuration/options).

## Using ASP.NET Core user secrets

When you develop your app locally, ASP.NET Core provides a [Secret Manager tool](/en-us/aspnet/core/security/app-secrets#secret-manager) that allows you to store secret information outside the project root. It makes it less likely that secrets are accidentally committed to source control. Azure Functions Core Tools (version 3.0.3233 or later) automatically reads secrets created by the ASP.NET Core Secret Manager.

To configure a .NET Azure Functions project to use user secrets, run the following command in the project root.

```
dotnet user-secrets init
```


Then use the `dotnet user-secrets set`

command to create or update secrets.

```
dotnet user-secrets set MySecret "my secret value"
```


To access user secrets values in your function app code, use `IConfiguration`

or `IOptions`

.

## Customizing configuration sources

To specify other configuration sources, override the `ConfigureAppConfiguration`

method in your function app's `StartUp`

class.

The following sample adds configuration values from both base and optional environment-specific app settings files.

```
using System.IO;
using Microsoft.Azure.Functions.Extensions.DependencyInjection;
using Microsoft.Extensions.Configuration;
using Microsoft.Extensions.DependencyInjection;
[assembly: FunctionsStartup(typeof(MyNamespace.Startup))]
namespace MyNamespace;
public class Startup : FunctionsStartup
{
public override void ConfigureAppConfiguration(IFunctionsConfigurationBuilder builder)
{
FunctionsHostBuilderContext context = builder.GetContext();
builder.ConfigurationBuilder
.AddJsonFile(Path.Combine(context.ApplicationRootPath, "appsettings.json"), optional: true, reloadOnChange: false)
.AddJsonFile(Path.Combine(context.ApplicationRootPath, $"appsettings.{context.EnvironmentName}.json"), optional: true, reloadOnChange: false)
.AddEnvironmentVariables();
}
public override void Configure(IFunctionsHostBuilder builder)
{
}
}
```


Add configuration providers to the `ConfigurationBuilder`

property of `IFunctionsConfigurationBuilder`

. For more information on using configuration providers, see [Configuration in ASP.NET Core](/en-us/aspnet/core/fundamentals/configuration/#configuration-providers).

A `FunctionsHostBuilderContext`

is obtained from `IFunctionsConfigurationBuilder.GetContext()`

. Use this context to retrieve the current environment name and resolve the location of configuration files in your function app folder.

By default, configuration files such as `appsettings.json`

aren't automatically copied to the function app's output folder. Update your `.csproj`

file to match the following sample to ensure the files are copied.

```
<None Update="appsettings.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
</None>
<None Update="appsettings.Development.json">
<CopyToOutputDirectory>PreserveNewest</CopyToOutputDirectory>
<CopyToPublishDirectory>Never</CopyToPublishDirectory>
</None>
```


## Next steps

For more information, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-target-based-scaling -->

# Target-based scaling

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Target-based scaling provides a fast and intuitive scaling model for customers and is currently supported for these binding extensions:

[Apache Kafka](#apache-kafka)[Azure Cosmos DB](#azure-cosmos-db)[Azure Event Hubs](#event-hubs)[Azure Queue Storage](#storage-queues)[Azure Service Bus (queue and topics)](#service-bus-queues-and-topics)

Target-based scaling replaces the previous Azure Functions incremental scaling model as the default for these extension types. Incremental scaling added or removed a maximum of one worker at [each new instance rate](event-driven-scaling#understanding-scaling-behaviors), with complex decisions for when to scale. In contrast, target-based scaling allows scale up of four instances at a time, and the scaling decision is based on a simple target-based equation:

In this equation, *event source length* refers to the number of events that must be processed. The default *target executions per instance* values come from the Software Development Kits (SDKs) used by the Azure Functions extensions. You don't need to make any changes for target-based scaling to work.

## Considerations

The following considerations apply when using target-based scaling:

- Target-based scaling is enabled by default for function apps on the
[Consumption plan](consumption-plan),[Flex Consumption plan](flex-consumption-plan), and[Elastic Premium plans](functions-premium-plan). Event-driven scaling isn't supported when running on[Dedicated (App Service) plans](dedicated-plan). - Target-based scaling is enabled by default starting with version 4.19.0 of the Functions runtime.
- When you use target-based scaling, scale limits are still honored. For more information, see
[Limit scale out](event-driven-scaling#limit-scale-out). - To achieve the most accurate scaling based on metrics, use only one target-based triggered function per function app. You should also consider running in a Flex Consumption plan, which offers
[per-function scaling](flex-consumption-plan#per-function-scaling). - When multiple functions in the same function app are all requesting to scale out at the same time, a sum across those functions is used to determine the change in desired instances. Functions requesting to scale out override functions requesting to scale in.
- When there are scale-in requests without any scale-out requests, the max scale in value is used.

## Opting out

Target-based scaling is enabled by default for function apps hosted on a Consumption plan or on a Premium plans. To disable target-based scaling and fall back to incremental scaling, add the following app setting to your function app:

| App Setting | Value |
|---|---|
`TARGET_BASED_SCALING_ENABLED` |
0 |

## Customizing target-based scaling

You can make the scaling behavior more or less aggressive based on your app's workload by adjusting *target executions per instance*. Each extension has different settings that you can use to set *target executions per instance*.

This table summarizes the `host.json`

values that are used for the *target executions per instance* values and the defaults:

| Extension | host.json values | Default Value |
|---|---|---|
| Event Hubs (Extension v5.x+) | extensions.eventHubs.maxEventBatchSize | 100* |
| Event Hubs (Extension v3.x+) | extensions.eventHubs.eventProcessorOptions.maxBatchSize | 10 |
| Event Hubs (if defined) | extensions.eventHubs.targetUnprocessedEventThreshold | n/a |
| Service Bus (Extension v5.x+, Single Dispatch) | extensions.serviceBus.maxConcurrentCalls | 16 |
| Service Bus (Extension v5.x+, Single Dispatch Sessions Based) | extensions.serviceBus.maxConcurrentSessions | 8 |
| Service Bus (Extension v5.x+, Batch Processing) | extensions.serviceBus.maxMessageBatchSize | 1000 |
| Service Bus (Functions v2.x+, Single Dispatch) | extensions.serviceBus.messageHandlerOptions.maxConcurrentCalls | 16 |
| Service Bus (Functions v2.x+, Single Dispatch Sessions Based) | extensions.serviceBus.sessionHandlerOptions.maxConcurrentSessions | 2000 |
| Service Bus (Functions v2.x+, Batch Processing) | extensions.serviceBus.batchOptions.maxMessageCount | 1000 |
| Storage Queue | extensions.queues.batchSize | 16 |

* The default `maxEventBatchSize`

changed in [v6.0.0](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs/6.0.0) of the `Microsoft.Azure.WebJobs.Extensions.EventHubs`

package. In earlier versions, this value was 10.

For some binding extensions, the *target executions per instance* configuration is set using a function attribute:

| Extension | Function trigger setting | Default Value |
|---|---|---|
| Apache Kafka | `lagThreshold` |
1000 |
| Azure Cosmos DB | `maxItemsPerInvocation` |
100 |

To learn more, see the [example configurations for the supported extensions](#supported-extensions).

## Premium plan with runtime scale monitoring enabled

When [runtime scale monitoring](functions-networking-options#elastic-premium-plan-with-virtual-network-triggers) is enabled the extensions themselves handle dynamic scaling because the [scale controller](event-driven-scaling#runtime-scaling) doesn't have access to services secured by a virtual network. After you enable runtime scale monitoring, you'll need to upgrade your extension packages to these minimum versions to unlock the extra target-based scaling functionality:

| Extension Name | Minimum Version Needed |
|---|---|
| Apache Kafka | 3.9.0 |
| Azure Cosmos DB | 4.1.0 |
| Event Hubs | 5.2.0 |
| Service Bus | 5.9.0 |
| Storage Queue | 5.1.0 |

## Dynamic concurrency support

Target-based scaling introduces faster scaling, and uses defaults for *target executions per instance*. When using Service Bus, Storage queues, or Kafka, you can also enable [dynamic concurrency](functions-concurrency#dynamic-concurrency). In this configuration, the _target execution per instance value is determined automatically by the dynamic concurrency feature. It starts with limited concurrency and identifies the best setting over time.

## Supported extensions

The way in which you configure target-based scaling in your host.json file depends on the specific extension type. This section provides the configuration details for the extensions that currently support target-based scaling.

### Service Bus queues and topics

The Service Bus extension support three execution models, determined by the `IsBatched`

and `IsSessionsEnabled`

attributes of your Service Bus trigger. The default value for `IsBatched`

and `IsSessionsEnabled`

is `false`

.

| Execution Model | IsBatched | IsSessionsEnabled | Setting Used for target executions per instance |
|---|---|---|---|
| Single dispatch processing | false | false | maxConcurrentCalls |
| Single dispatch processing (session-based) | false | true | maxConcurrentSessions |
| Batch processing | true | false | maxMessageBatchSize or maxMessageCount |

Note

**Scale efficiency:** For the Service Bus extension, use *Manage* rights on resources for the most efficient scaling. With *Listen* rights, scaling reverts to incremental scale because the queue or topic length can't be used to inform scaling decisions. To learn more about setting rights in Service Bus access policies, see [Shared Access Authorization Policy](../service-bus-messaging/service-bus-sas#shared-access-authorization-policies).

#### Single dispatch processing

In this model, each invocation of your function processes a single message. The `maxConcurrentCalls`

setting governs *target executions per instance*. The specific setting depends on the version of the Service Bus extension.

Modify the `host.json`

setting `maxConcurrentCalls`

, as in the following example:

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"maxConcurrentCalls": 16
}
}
}
```


#### Single dispatch processing (session-based)

In this model, each invocation of your function processes a single message. However, depending on the number of active sessions for your Service Bus topic or queue, each instance leases one or more sessions. The specific setting depends on the version of the Service Bus extension.

Modify the `host.json`

setting `maxConcurrentSessions`

to set *target executions per instance*, as in the following example:

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"maxConcurrentSessions": 8
}
}
}
```


#### Batch processing

In this model, each invocation of your function processes a batch of messages. The specific setting depends on the version of the Service Bus extension.

Modify the `host.json`

setting `maxMessageBatchSize`

to set *target executions per instance*, as in the following example:

```
{
"version": "2.0",
"extensions": {
"serviceBus": {
"maxMessageBatchSize": 1000
}
}
}
```


### Event Hubs

For Azure Event Hubs, Azure Functions scales based on the number of unprocessed events distributed across all the partitions in the event hub within a list of valid instance counts. By default, the `host.json`

attributes used for *target executions per instance* are `maxEventBatchSize`

and `maxBatchSize`

. However, if you choose to fine-tune target-based scaling, you can define a separate parameter `targetUnprocessedEventThreshold`

that overrides to set *target executions per instance* without changing the batch settings. If `targetUnprocessedEventThreshold`

is set, the total unprocessed event count is divided by this value to determine the number of instances, which is then be rounded up to a worker instance count that creates a balanced partition distribution.

Warning

Setting `batchCheckpointFrequency`

above 1 for hosting plans supported by [target based scaling](#considerations) can cause incorrect scaling behavior. The platform calculates unprocessed events as "current position - checkpointed position", which may incorrectly indicate unprocessed messages when batches have been processed but not yet checkpointed, preventing proper scale-in when no messages remain.

#### Scaling Behavior and Stability

For Event Hubs, frequent scale-in and scale-out operations can trigger partition rebalancing, which leads to processing delays and increased latency. To mitigate this:

- The platform uses a predefined list of valid worker counts to guide scaling decisions.
- The platform ensures that scaling is stable and deliberate, avoiding disruptive changes to partition assignments.
- If the desired worker count isn't in the valid list—for example, 17, the system automatically selects the next largest valid count, which in this case is 32. Additionally, to prevent rapid repeated scaling, scale-in requests are throttled for 3 minutes after the last scale-up. This delay helps reduce unnecessary rebalancing and contributes to maintaining throughput efficiency.

#### Valid Instance Counts for Event Hubs

For each Event Hubs partition count, we calculate a corresponding list of valid instance counts to ensure optimal distribution and efficient scaling. These counts are chosen to align well with partitioning and concurrency requirements:

| Partition Count | Valid Instance Counts |
|---|---|
| 1 | [1] |
| 2 | [1, 2] |
| 4 | [1, 2, 4] |
| 8 | [1, 2, 3, 4, 8] |
| 10 | [1, 2, 3, 4, 5, 10] |
| 16 | [1, 2, 3, 4, 5, 6, 8, 16] |
| 32 | [1, 2, 3, 4, 5, 6, 7, 8, 9, 11, 16, 32] |

These predefined counts help ensure that instances are distributed as evenly as possible across partitions, minimizing idle or overloaded workers.

Note

Note: For Premium and Dedicated event hub tiers the partition count can exceed 32, allowing for larger valid instance count sets. These tiers support higher throughput and scalability, and the valid worker count list is extended accordingly to evenly distribute event hub partitions across instances. Also, since Event Hubs is a partitioned workload, the number of partitions in your event hub is the limit for the maximum target instance count.

#### Event Hubs settings

The specific setting depends on the version of the Event Hubs extension.

Modify the `host.json`

setting `maxEventBatchSize`

to set *target executions per instance*, as in the following example:

```
{
"version": "2.0",
"extensions": {
"eventHubs": {
"maxEventBatchSize" : 100
}
}
}
```


When defined in `host.json`

, `targetUnprocessedEventThreshold`

is used as *target executions per instance* instead of `maxEventBatchSize`

, as in the following example:

```
{
"version": "2.0",
"extensions": {
"eventHubs": {
"targetUnprocessedEventThreshold": 153
}
}
}
```


### Storage Queues

For **v2.x+** of the Storage extension, modify the `host.json`

setting `batchSize`

to set *target executions per instance*:

```
{
"version": "2.0",
"extensions": {
"queues": {
"batchSize": 16
}
}
}
```


Note

**Scale efficiency:** For the storage queue extension, messages with [visibilityTimeout](/en-us/rest/api/storageservices/put-message#uri-parameters) are still counted in *event source length* by the Storage Queue APIs. This can cause overscaling of your function app. Consider using Service Bus queues que scheduled messages, [limiting scale out](event-driven-scaling#limit-scale-out), or not using visibilityTimeout for your solution.

### Azure Cosmos DB

Azure Cosmos DB uses a function-level attribute, `MaxItemsPerInvocation`

. The way you set this function-level attribute depends on your function language.

For a compiled C# function, set `MaxItemsPerInvocation`

in your trigger definition, as shown in the following examples for an in-process C# function:

```
namespace CosmosDBSamplesV2
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
collectionName: "Items",
MaxItemsPerInvocation: 100,
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


Note

Since Azure Cosmos DB is a partitioned workload, the number of physical partitions in your container is the limit for the target instance count. To learn more about Azure Cosmos DB scaling, see [physical partitions](/en-us/azure/cosmos-db/nosql/change-feed-processor#dynamic-scaling) and [lease ownership](/en-us/azure/cosmos-db/nosql/change-feed-processor#dynamic-scaling).

### Apache Kafka

The Apache Kafka extension uses a function-level attribute, `LagThreshold`

. For Kafka, the number of *desired instances* is calculated based on the total consumer lag divided by the `LagThreshold`

setting. For a given lag, reducing the lag threshold increases the number of desired instances.

The way you set this function-level attribute depends on your function language. This example sets the threshold to `100`

.

For a compiled C# function, set `LagThreshold`

in your trigger definition, as shown in the following examples for an in-process C# function for a Kafka Event Hubs trigger:

```
[FunctionName("KafkaTrigger")]
public static void Run(
[KafkaTrigger("BrokerList",
"topic",
Username = "$ConnectionString",
Password = "%EventHubConnectionString%",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain,
ConsumerGroup = "$Default",
LagThreshold = 100)] KafkaEventData<string> kevent, ILogger log)
{
log.LogInformation($"C# Kafka trigger function processed a message: {kevent.Value}");
}
```


## Next steps

To learn more, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-mysql-output -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-event-grid-blob-trigger -->

# Tutorial: Trigger Azure Functions on blob containers by using an event subscription

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Previous versions of the Azure Functions Blob Storage trigger poll your storage container for changes. More recent versions of the Blob Storage extension (5.x+) instead use an Event Grid event subscription on the container. This event subscription reduces latency by triggering your function instantly as changes occur in the subscribed container.

This article shows how to create a function that runs based on events raised when a blob is added to a container. You use Visual Studio Code for local development and to validate your code before deploying your project to Azure.

- Create an event-based Blob Storage triggered function in a new project.
- Validate locally within Visual Studio Code by using the Azurite emulator.
- Create a blob storage container in a new storage account in Azure.
- Create a function app in the Flex Consumption plan.
- Create an event subscription to the new blob container.
- Deploy and validate your function code in Azure.

This article supports version 4 of the Node.js programming model for Azure Functions.

This article supports version 2 of the Python programming model for Azure Functions.

This article creates a C# app that runs in isolated worker mode, which supports .NET 8.0.

Tip

This tutorial shows you how to create an app that runs on the [Flex Consumption plan](flex-consumption-plan). The Flex Consumption plan only supports the event-based version of the Blob Storage trigger.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Node.js 14.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code. This extension installs[Azure Functions Core Tools](functions-run-local)for you the first time you locally run your functions.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).The

[Java Development Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17 or 21(Linux).[Apache Maven](https://maven.apache.org), version 3.0 or above.[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code.

[Azure Storage extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage)for Visual Studio Code.

Note

The Azure Storage extension for Visual Studio Code is in preview.

## Create a Blob triggered function

When you create a Blob Storage trigger function by using Visual Studio Code, you also create a new project. You need to edit the function to consume an event subscription as the source, rather than use the regular polled container.

In Visual Studio Code, press F1 to open the command palette, enter

`Azure Functions: Create Function...`

, and select**Create new project**.For your project workspace, select a directory location. Make sure that you either create a new folder or choose an empty folder for the project workspace.

Don't choose a project folder that's already part of a workspace.

At the prompts, provide the following information:

Prompt Action **Select a language**Select `C#`

.**Select a .NET runtime**Select `.NET 8.0 Isolated LTS`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Provide a namespace**Enter `My.Functions`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language**Select `Python`

.**Select a Python programming model**Select `Model V2`

**Select a Python interpreter to create a virtual environment**Select your preferred Python interpreter. If an option isn't shown, enter the full path to your Python binary. **Select a template for your project's first function**Select `Blob trigger`

. (The event-based template isn't yet available.)**Provide a function name**Enter `EventGridBlobTrigger`

.**The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language**Select `Java`

.**Select a version of Java**Select `Java 11`

or`Java 8`

, the Java version on which your functions run in Azure and that you've locally verified.**Provide a group ID**Select `com.function`

.**Provide an artifact ID**Select `EventGridBlobTrigger`

(or the default).**Provide a version**Select `1.0-SNAPSHOT`

.**Provide a package name**Select `com.function`

.**Provide an app name**Accept the generated name starting with `EventGridBlobTrigger`

.**Select the build tool for Java project**Select `Maven`

.**Select how you would like to open your project**Select `Open in current window`

.An HTTP triggered function (

`HttpExample`

) is created for you. You won't use this function and must instead create a new function.Prompt Action **Select a language for your function project**Select `TypeScript`

.**Select a TypeScript programming model**Select `Model V4`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language for your function project**Select `JavaScript`

.**Select a JavaScript programming model**Select `Model V4`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `eventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.Prompt Action **Select a language for your function project**Select `PowerShell`

.**Select a template for your project's first function**Select `Azure Blob Storage trigger (using Event Grid)`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription, if needed. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.**Select how you would like to open your project**Select `Open in current window`

.

In the command palette, enter

`Azure Functions: Create Function...`

and select`EventGridBlobTrigger`

. If you don't see this template, first select**Change template filter**>**All**.At the prompts, provide the following information:

Prompt Action **Provide a package name**Select `com.function`

.**Provide a function name**Enter `EventGridBlobTrigger`

.**Select setting from "local.settings.json"**Select `Create new local app setting`

.**Select subscription**Select your subscription. **Select a storage account**Use Azurite emulator for local storage. **The path within your storage account that the trigger will monitor**Accept the default value `samples-workitems`

.

You now have a function that can be triggered by events in a Blob Storage container.

## Update the trigger source

You need to switch the trigger source from the default Blob trigger source (container polling) to an event subscription source.

Open the function_app.py project file. You see a definition for the

`EventGridBlobTrigger`

function with the`blob_trigger`

decorator applied.Update the decorator by adding

`source = "EventGrid"`

. Your function should now look something like this:`@app.blob_trigger(arg_name="myblob", source="EventGrid", path="samples-workitems", connection="<STORAGE_ACCOUNT>") def EventGridBlobTrigger(myblob: func.InputStream): logging.info(f"Python blob trigger function processed blob" f"Name: {myblob.name}" f"Blob Size: {myblob.length} bytes")`

In this definition,

`source = "EventGrid"`

indicates that an event subscription to the`samples-workitems`

blob container is used as the source of the event that starts the trigger.

## (Optional) Review the code

Open the generated `EventGridBlobTrigger.cs`

file. You see a definition for an `EventGridBlobTrigger`

function that looks something like this:

```
[Function(nameof(EventGridBlobTriggerCSharp))]
public async Task Run([BlobTrigger("PathValue/{name}", Source = BlobTriggerSource.EventGrid, Connection = "ConnectionValue")] Stream stream, string name)
{
using var blobStreamReader = new StreamReader(stream);
var content = await blobStreamReader.ReadToEndAsync();
_logger.LogInformation("C# Blob Trigger (using Event Grid) processed blob\n Name: {name} \n Data: {content}", name, content);
}
```


In this definition, `Source = BlobTriggerSource.EventGrid`

indicates that an event subscription to the blob container (in the example `PathValue`

) is the source of the event that starts the trigger.

Open the generated `EventGridBlobTrigger.java`

file. You see a definition for an `EventGridBlobTrigger`

function that looks something like this:

```
@FunctionName("EventGridBlobTrigger")
@StorageAccount("<STORAGE_ACCOUNT>")
public void run(
@BlobTrigger(name = "content", source = "EventGrid", path = "samples-workitems/{name}", dataType = "binary") byte[] content,
@BindingName("name") String name,
final ExecutionContext context
) {
context.getLogger().info("Java Blob trigger function processed a blob. Name: " + name + "\n Size: " + content.length + " Bytes");
}
```


In this definition, `source = EventGrid`

indicates that an event subscription to the `samples-workitems`

blob container is the source of the event that starts the trigger.

In the `EventGridBlobTrigger`

folder, open the `function.json`

file and find a binding definition like this with a `type`

of `blobTrigger`

and a `source`

of `EventGrid`

:

```
{
"bindings": [
{
"name": "InputBlob",
"type": "blobTrigger",
"direction": "in",
"path": "samples-workitems/{name}",
"source": "EventGrid",
"connection":""
}
]
}
```


The `path`

indicates that the `samples-workitems`

blob container is the source of the event that starts the trigger.

Open the generated `EventGridBlobTrigger.js`

file. You see a definition for a function that looks something like this:

```
const { app } = require('@azure/functions');
app.storageBlob('storageBlobTrigger1', {
path: 'samples-workitems/{name}',
connection: 'MyStorageAccountAppSetting',
source: 'EventGrid',
handler: (blob, context) => {
context.log(
`Storage blob function processed blob "${context.triggerMetadata.name}" with size ${blob.length} bytes`
);
},
});
```


In this definition, a `source`

of `EventGrid`

indicates that an event subscription to the `samples-workitems`

blob container is the source of the event that starts the trigger.

Open the generated `EventGridBlobTrigger.ts`

file. You see a definition for a function that looks something like this:

```
import { app, InvocationContext } from '@azure/functions';
export async function storageBlobTrigger1(blob: Buffer, context: InvocationContext): Promise<void> {
context.log(
`Storage blob function processed blob "${context.triggerMetadata.name}" with size ${blob.length} bytes`
);
}
app.storageBlob('storageBlobTrigger1', {
path: 'samples-workitems/{name}',
connection: 'MyStorageAccountAppSetting',
source: 'EventGrid',
handler: storageBlobTrigger1,
});
```


In this definition, a `source`

of `EventGrid`

indicates that an event subscription to the `samples-workitems`

blob container is the source of the event that starts the trigger.

## Upgrade the Storage extension

To use the Event Grid-based Blob Storage trigger, you need version 5.x or later of the Azure Functions Storage extension.

To upgrade your project to the required extension version, run this [ dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs
```


Open the

`host.json`

project file, and review the`extensionBundle`

element.If

`extensionBundle.version`

isn't at least`3.3.0`

, replace the`extensionBundle`

element with this version:`"extensionBundle": { "id": "Microsoft.Azure.Functions.ExtensionBundle", "version": "[4.0.0, 5.0.0)" }`


## Prepare local storage emulation

Visual Studio Code uses Azurite to emulate Azure Storage services when running locally. Use Azurite to emulate the Azure Blob Storage service during local development and testing.

If you haven't already done so, install the

[Azurite v3 extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=Azurite.azurite).Verify that the

*local.settings.json*file has`"UseDevelopmentStorage=true"`

set for`AzureWebJobsStorage`

. This setting tells Core Tools to use Azurite instead of a real storage account connection when running locally.Press F1 to open the command palette, type

`Azurite: Start Blob Service`

, and press enter. This action starts the Azurite Blob Storage service emulator.Select the Azure icon in the Activity bar, expand

**Workspace**>**Attached Storage Accounts**>**Local Emulator**, right-click**Blob Containers**, select**Create Blob Container...**, enter the name`samples-workitems`

, and press Enter.Expand

**Blob Containers**>**samples-workitems**and select**Upload files...**.Choose a file to upload to the locally emulated container. Your function processes this file later to verify and debug your function code. A text file might work best with the Blob trigger template code.


## Run the function locally

With a file in emulated storage, you can run your function to simulate an event raised by an Event Grid subscription. The event info passed to your trigger depends on the file you added to the local container.

Set any breakpoints and press F5 to start your project for local debugging. Azure Functions Core Tools should be running in your Terminal window.

Back in the Azure area, expand

**Workspace**>**Local Project**>**Functions**, right-click the function, and select**Execute Function Now...**.In the request body dialog, type

`samples-workitems/<TEST_FILE_NAME>`

, replacing`<TEST_FILE_NAME>`

with the name of the file you uploaded in the local storage emulator.Press Enter to run the function. The value you provided is the path to your blob in the local emulator. This string gets passed to your trigger in the request payload, which simulates the payload when an event subscription calls your function to report a blob being added to the container.

Review the output of this function execution. You should see in the output the name of the file and its contents logged. If you set any breakpoints, you might need to continue the execution.


Now that you've successfully validated your function code locally, it's time to publish the project to a new function app in Azure.

## Prepare the Azure Storage account

Event subscriptions to Azure Storage require a general-purpose v2 storage account. You can use the Azure Storage extension for Visual Studio Code to create this storage account.

In Visual Studio Code, press F1 to open the command palette and enter

`Azure Storage: Create Storage Account...`

. Provide this information when prompted:Prompt Action **Enter the name of the new storage account**Provide a globally unique name. Storage account names must have 3 to 24 characters in length with only lowercase letters and numbers. For easier identification, use the same name for the resource group and the function app name. **Select a location for new resources**For better performance, choose a [region near you](https://azure.microsoft.com/regions/).The extension creates a general-purpose v2 storage account with the name you provide. The same name is also used for the resource group that contains the storage account. The Event Grid-based Blob Storage trigger requires a general-purpose v2 storage account.

Press F1 again and in the command palette enter

`Azure Storage: Create Blob Container...`

. Provide this information when prompted:Prompt Action **Select a resource**Select the general-purpose v2 storage account that you created. **Enter a name for the new blob container**Enter `samples-workitems`

, which is the container name referenced in your code project.

Your function app also needs a storage account to run. For simplicity, this tutorial uses the same storage account for your blob trigger and your function app. However, in production, you might want to use a separate storage account with your function app. For more information, see [Storage considerations for Azure Functions](storage-considerations).

## Create the function app

Use these steps to create a function app in the Flex Consumption plan. When you host your app in a Flex Consumption plan, Blob Storage triggers must use event subscriptions.

In the command palette, enter

**Azure Functions: Create function app in Azure...(Advanced)**.Follow the prompts and provide this information:

Prompt Selection **Enter a globally unique name for the new function app**Type a globally unique name that identifies your new function app and then select Enter. Valid characters for a function app name are `a-z`

,`0-9`

, and`-`

.**Select a hosting plan**Choose **Flex Consumption**, which is the recommended[hosting plan](functions-scale)for serverless hosting.**Select a location for new resources**Select a location in a [region](https://azure.microsoft.com/regions/)near you or near other services that your functions access.**Select a runtime stack**Select the language version you currently run locally. **Select an instance size**Select **512**. You can always[change the instance size](flex-consumption-how-to#configure-instance-memory)setting to a larger size later.**Enter the maximum instance count**Select the default value of **100**, which limits the total scale-out of your app. You can also choose a different value between 40 and 1,000.**Select a resource group**Select **Create new resource group**and accept the default or enter another name for the new group that's unique in your subscription.**Select resource authentication type**Select **Managed identity**so that your app connects to remote resources by using Microsoft Entra ID authentication instead of using shared secrets (connection strings and keys), which are less secure.**Select a user assigned identity**Select **Create new user-assigned identity**.**Select a location for new resources**Select the same region as the storage account you created. If for some reason this region isn't supported by the Flex Consumption play, it isn't displayed. In that case, choose a nearby [region](https://azure.microsoft.com/regions/)instead. For more information, see[View currently supported regions](flex-consumption-how-to#view-currently-supported-regions).**Select a storage account**Choose the name of the storage account you created. **Select an Application Insights resource for your app**Choose **Create new Application Insights resource**and at the prompt provide the name for the instance used to store runtime data from your functions.A notification appears after your function app is created. Select

**View Output**in this notification to view the creation results, including the Azure resources that you created.

## Deploy your function code

Important

Deploying to an existing function app always overwrites the contents of that app in Azure.

In the command palette, enter and then select

**Azure Functions: Deploy to Function App**.Select the function app you just created. When prompted about overwriting previous deployments, select

**Deploy**to deploy your function code to the new function app resource.When deployment is completed, select

**View Output**to view the creation and deployment results, including the Azure resources that you created. If you miss the notification, select the bell icon in the lower-right corner to see it again.

## Update application settings

Because the publishing process doesn't automatically upload required application settings from the `local.settings.json`

file, you must upload them to your function app so that your function runs correctly in Azure.

In the command palette, enter

`Azure Functions: Download Remote Settings...`

, and in the**Select a resource**prompt choose the name of your function app.When prompted that the

`AzureWebJobsStorage`

setting already exists, select**Yes**to overwrite the local emulator setting with the actual storage account connection string from Azure.In the

`local.settings.json`

file, replace the local emulator setting with same connection string used for`AzureWebJobsStorage`

.Remove the

`FUNCTIONS_WORKER_RUNTIME`

entry, which isn't supported in a Flex Consumption plan.In the command palette, enter

`Azure Functions: Upload Local Settings...`

, and in the**Select a resource**prompt choose the name of your function app.

Now both the Functions host and the trigger share the same storage account.

## Build the endpoint URL

To create an event subscription, you need to provide Event Grid with the URL of the specific endpoint to report Blob Storage events. This *blob extension* URL is composed of these parts:

| Part | Example |
|---|---|
| Base function app URL | `https://<FUNCTION_APP_NAME>.azurewebsites.net` |
| Blob-specific path | `/runtime/webhooks/blobs` |
| Function query string | `?functionName=Host.Functions.<FUNCTION_NAME>` |
| Blob extension access key | `&code=<BLOB_EXTENSION_KEY>` |

While your app connects to the storage account by using Microsoft Entra ID authentication, the blob extension access key helps protect your blob extension webhook from unauthorized access. To find your blob extension access key:

In Visual Studio Code, select the Azure icon in the Activity bar. In

**Resources**, expand your subscription, expand**Function App**, right-click the function app you created, and select**Open in portal**.Under

**Functions**in the left menu, select**App keys**.Under

**System keys**, select the key named**blobs_extension**, and copy the key**Value**.Include this value in the query string of the new endpoint URL.

Create a new endpoint URL for the Blob Storage trigger based on the following example:

`https://<FUNCTION_APP_NAME>.azurewebsites.net/runtime/webhooks/blobs?functionName=Host.Functions.EventGridBlobTrigger&code=<BLOB_EXTENSION_KEY>`

In this example, replace

`<FUNCTION_APP_NAME>`

with the name of your function app, and`<BLOB_EXTENSION_KEY>`

with the value you got from the portal. If you used a different name for your function, replace`EventGridBlobTrigger`

with that function name.

You can now use this endpoint URL to create an event subscription.

## Create the event subscription

An event subscription, powered by Azure Event Grid, raises events based on changes in the subscribed blob container. This event is then sent to the blob extension endpoint for your function. After you create an event subscription, you can't update the endpoint URL.

In Visual Studio Code, choose the Azure icon in the Activity bar. In

**Resources**, expand your subscription, expand**Storage accounts**, right-click the storage account you created earlier, and select**Open in portal**.Sign in to the

[Azure portal](https://portal.azure.com)and make a note of the**Resource group**for your storage account. Create your other resources in the same group to make it easier to clean up resources when you're done.Select the

**Events**option from the left menu.In the

**Events**window, select the**+ Event Subscription**button, and provide values from the following table into the**Basic**tab:Setting Suggested value Description **Name***myBlobEventSub*Name that identifies the event subscription. Use the name to quickly find the event subscription. **Event Schema****Event Grid Schema**Use the default schema for events. **System Topic Name***samples-workitems-blobs*Name for the topic, which represents the container. The topic is created with the first subscription, and you use it for future event subscriptions. **Filter to Event Types***Blob Created***Endpoint Type****Web Hook**The blob storage trigger uses a web hook endpoint. **Endpoint**Your Azure-based URL endpoint Use the URL endpoint that you built, which includes the key value. Select

**Confirm selection**to validate the endpoint URL.Select the

**Filters**tab and provide the following information to the prompts:Setting Suggested value Description **Enable subject filtering***Enabled*Enables filtering on which blobs can trigger the function. **Subject Begins With**`/blobServices/default/containers/<CONTAINER_NAME>/blobs/<BLOB_PREFIX>`

Replace `<CONTAINER_NAME`

and`<BLOB_PREFIX>`

with values you choose. This setting triggers the subscription only for blobs that start with`BLOB_PREFIX`

and are in the`CONTAINER_NAME`

container.**Subject Ends With***.txt*Ensures that the function is only triggered by blobs ending with `.txt`

.For more information on filtering to specific blobs, see

[Event Filtering for Azure Event Hubs](../event-grid/event-filtering).Select

**Create**to create the event subscription.

## Upload a file to the container

You can upload a file from your computer to your blob storage container by using Visual Studio Code.

In Visual Studio Code, press F1 to open the command palette and type

`Azure Storage: Upload Files...`

.In the

**Open**dialog box, choose a file, preferably a text file, and select**Upload**.Provide the following information at the prompts:

Setting Suggested value Description **Enter the destination directory of this upload**default Accept the default value of `/`

, which is the container root.**Select a resource**Storage account name Choose the name of the storage account you created in a previous step. **Select a resource type****Blob Containers**You're uploading to a blob container. **Select Blob Container****samples-workitems**This value is the name of the container you created in a previous step.

Browse your local file system to find a file to upload, then select the **Upload** button to upload the file.

## Verify the function in Azure

When you upload a file to the **samples-workitems** container, the function triggers. You can verify the function by checking the following items on the Azure portal:

In your storage account, go to the

**Events**page, select**Event Subscriptions**, and you should see that an event was delivered. There might be up to a five-minute delay for the event to show up on the chart.Back in your function app page in the portal, under

**Functions**find your function and select**Invocations and more**. You should see traces written from your successful function execution.

## Clean up resources

When you continue to the [next step](#next-steps) and add an Azure Storage queue binding to your function, you'll need to keep all your resources in place to build on what you've already done.

Otherwise, you can use the following steps to delete the function app and its related resources to avoid incurring any further costs.

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


For more information about Functions costs, see [Estimating Consumption plan costs](functions-consumption-costs).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-output-publish -->

# Dapr Publish output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr publish output binding allows you to publish a message to a Dapr topic during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).The following example demonstrates using a Dapr publish output binding to perform a Dapr publish operation to a pub/sub component and topic.

```
[FunctionName("PublishOutputBinding")]
public static void Run(
[HttpTrigger(AuthorizationLevel.Function, "post", Route = "topic/{topicName}")] HttpRequest req,
[DaprPublish(PubSubName = "%PubSubName%", Topic = "{topicName}")] out DaprPubSubEvent pubSubEvent,
ILogger log)
{
string requestBody = new StreamReader(req.Body).ReadToEnd();
pubSubEvent = new DaprPubSubEvent(requestBody);
}
```


The following example creates a `"TransferEventBetweenTopics"`

function using the `DaprPublishOutput`

binding with an [ DaprTopicTrigger](functions-bindings-dapr-trigger-topic):

```
@FunctionName("TransferEventBetweenTopics")
public String run(
@DaprTopicTrigger(
pubSubName = "%PubSubName%",
topic = "A")
String request,
@DaprPublishOutput(
pubSubName = "%PubSubName%",
topic = "B")
OutputBinding<String> payload,
final ExecutionContext context) throws JsonProcessingException {
context.getLogger().info("Java function processed a TransferEventBetweenTopics request from the Dapr Runtime.");
}
```


In the following example, the Dapr publish output binding is paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('PublishOutputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['POST'],
route: "topic/{topicName}",
name: "req"
}),
return: daprPublishOutput,
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const payload = await request.text();
context.log(JSON.stringify(payload));
return { payload: payload };
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprPublish`

:

```
{
"bindings":
{
"type": "daprPublish",
"direction": "out",
"name": "pubEvent",
"pubsubname": "%PubSubName%",
"topic": "B"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System
using namespace Microsoft.Azure.WebJobs
using namespace Microsoft.Extensions.Logging
using namespace Microsoft.Azure.WebJobs.Extensions.Dapr
using namespace Newtonsoft.Json.Linq
# Example to use Dapr Service Invocation Trigger and Dapr State Output binding to persist a new state into statestore
param (
$subEvent
)
Write-Host "PowerShell function processed a TransferEventBetweenTopics request from the Dapr Runtime."
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $subEvent["data"]
$messageFromTopicA = "Transfer from Topic A: $jsonString".Trim()
$publish_output_binding_req_body = @{
"payload" = $messageFromTopicA
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name pubEvent -Value $publish_output_binding_req_body
```


The following example shows a Dapr Publish output binding, which uses the [v2 Python programming model](functions-reference-python). To use `daprPublish`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="TransferEventBetweenTopics")
@app.dapr_topic_trigger(arg_name="subEvent", pub_sub_name="%PubSubName%", topic="A", route="A")
@app.dapr_publish_output(arg_name="pubEvent", pub_sub_name="%PubSubName%", topic="B")
def main(subEvent, pubEvent: func.Out[bytes]) -> None:
logging.info('Python function processed a TransferEventBetweenTopics request from the Dapr Runtime.')
subEvent_json = json.loads(subEvent)
payload = "Transfer from Topic A: " + str(subEvent_json["data"])
pubEvent.set(json.dumps({"payload": payload}).encode('utf-8'))
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprPublish`

to define a Dapr publish output binding, which supports these parameters:

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
PubSubName |
The name of the Dapr pub/sub to send the message. | ✔️ | ✔️ |
Topic |
The name of the Dapr topic to send the message. | ✔️ | ✔️ |
Payload |
Required. The message being published. |
❌ | ✔️ |

## Annotations

The `DaprPublishOutput`

annotation allows you to have a function access a published message.

| Element | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pubSubName |
The name of the Dapr pub/sub to send the message. | ✔️ | ✔️ |
topic |
The name of the Dapr topic to send the message. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pubsubname |
The name of the publisher component service. | ✔️ | ✔️ |
topic |
The name/identifier of the publisher topic. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pubsubname |
The name of the publisher component service. | ✔️ | ✔️ |
topic |
The name/identifier of the publisher topic. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

The following table explains the binding configuration properties for `@dapp.dapr_publish_output`

that you set in your Python code.

| Property | Description | Can be sent via Attribute | Can be sent via RequestBody |
|---|---|---|---|
pub_sub_name |
The name of the publisher event. | ✔️ | ✔️ |
topic |
The publisher topic name/identifier. | ✔️ | ✔️ |
payload |
Required. The message being published. |
❌ | ✔️ |

If properties are defined in both Attributes and `RequestBody`

, priority is given to data provided in `RequestBody`

.

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr publish output binding, start by setting up a Dapr pub/sub component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprPublish`

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-register -->

# Register Azure Functions binding extensions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Functions runtime natively runs HTTP and timer triggers. The behaviors of the other supported [triggers and bindings](functions-triggers-bindings) are implemented in separate extension packages.

Projects that use a .NET class library use binding extensions that are installed in the project as NuGet packages.

Extension bundles allow non-.NET apps to use binding extensions without having to interact with .NET infrastructure.

## Extension bundles

Extension bundles add a predefined set of compatible binding extensions to your function app. Extension bundles are versioned. Each version contains a specific set of binding extensions that are verified to work together. Select a bundle version based on the extensions that you need in your app.

When you create an Azure Functions project from a non-.NET template, extension bundles are already enabled in the app's `host.json`

file.

When possible, use the latest version range to obtain optimal app performance and access to the latest features. To learn more about extension bundles, see [Azure Functions extension bundles](extension-bundles).

In the unlikely event that you can't use an extension bundle, you must instead explicitly install extensions.

## Explicitly install extensions

For projects that use a compiled C# class library, you install the NuGet packages for the extensions that you need as you normally would in your apps. For more information, see the [Visual Studio Code developer guide](functions-develop-vs-code?tabs=csharp#install-binding-extensions) or the [Visual Studio developer guide](functions-develop-vs#add-bindings).

Make sure to obtain the correct package, because the namespace differs depending on the execution model:

| Execution model | Namespace |
|---|---|
|

`Microsoft.Azure.Functions.Worker.Extensions.*`

[In-process](functions-dotnet-class-library)`Microsoft.Azure.WebJobs.Extensions.*`

Azure Functions provides extension bundles for non-.NET projects. These bundles contain a full set of binding extensions that are verified to be compatible. If you're having compatibility problems between two or more binding extensions, review compatible combinations of extension versions. For supported combinations of binding extensions, see the [release page for extension bundles](https://github.com/Azure/azure-functions-extension-bundles/releases).

There are cases when you can't use extension bundles, such as when you need to use a specific prerelease version of a specific extension. In these rare cases, you must manually install any required binding extensions in a C# project file that references the specific extensions that your app requires.

To manually install binding extensions:

Remove the extension bundle reference from your

`host.json`

file.Use the

command in Azure Functions Core Tools to generate the required`func extensions install`

`extensions.csproj`

file in the root of your local project.For portal-only development, you need to manually create an

`extensions.csproj`

file in the root of your function app in Azure. To learn more, see[Manually install extensions](functions-how-to-use-azure-function-app-settings#manually-install-extensions).Edit the

`extensions.csproj`

file by explicitly adding a`PackageReference`

element for every specific binding extension and version that your app requires.Validate your app functionality locally and then redeploy your project, including

`extensions.csproj`

, to your function app in Azure.

As soon as possible, you should [switch your app back to using the latest supported extension bundle](extension-bundles#define-an-extension-bundle-reference).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/errors-diagnostics/diagnostic-events/azfd0013 -->

# AZFD0013: The configured runtime does not match the worker runtime metadata found in the deployed function app artifacts

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This event occurs when a function app has a `FUNCTIONS_WORKER_RUNTIME`

setting specifying a language stack, but a payload for a different stack is deployed to it.

| Value | |
|---|---|
Event ID |
AZFD0013 |
Severity |
Warning or Error |

## Event description

The `FUNCTIONS_WORKER_RUNTIME`

application setting indicates the language or language stack on which the function app runs, such as `python`

. For more information on valid values, see the [ FUNCTIONS_WORKER_RUNTIME](../../functions-app-settings#functions_worker_runtime) reference. The deployed application must correspond with the provided value. If there is a mismatch, it means that either the value of

`FUNCTIONS_WORKER_RUNTIME`

is incorrect, or that an unexpected payload was deployed to the application.This event may appear for apps that were previously using inconsistent and undefined behavior to continue running while in a mismatch state. Follow the instructions in this article to resolve the event for these applications. Doing so allows these apps to take advantage of performance enhancements and ensure that they can continue to operate as expected.

.NET apps undergoing a [migration from the in-process model to the isolated worker](../../migrate-dotnet-to-isolated-model) may encounter this event temporarily during that process. When `FUNCTIONS_WORKER_RUNTIME`

is updated to `dotnet-isolated`

, but the application is still using an in-process model payload, this event may appear until the migration is completed. See the migration guidance for instructions on using deployment slots to prevent this event from appearing in your production environment.

## How to resolve the event

The event message indicates the current value of `FUNCTIONS_WORKER_RUNTIME`

and the detected runtime metadata from the app payload. These values must be aligned, either by deploying an application payload of the appropriate type or by updating the setting to an expected value

For most applications, the correct resolution is to update the value of [ FUNCTIONS_WORKER_RUNTIME](../../functions-app-settings#functions_worker_runtime). To do so, on your function app in Azure, set the

`FUNCTIONS_WORKER_RUNTIME`

[application setting](../../functions-how-to-use-azure-function-app-settings#settings)to the expected value for your application payload. The expected value is not necessarily the same as the detected runtime metadata, though in many cases it will be. Use the following table to determine the correct value to use:

| Detected payload | Expected `FUNCTIONS_WORKER_RUNTIME` value |
|---|---|
`CSharp` |
`dotnet` |
`custom` |
`custom` |
`dotnet` |
`dotnet` |
`dotnet-isolated` |
`dotnet-isolated` |
`java` |
`java` |
`node` |
`node` |
`powershell` |
`powershell` |
`python` |
`python` |
Any multi-stack payload1 |
`dotnet` |

1 A multi-stack payload is a comma-separated list of stack values. Multi-stack payloads are only supported for [Logic Apps Standard](../../../logic-apps/single-tenant-overview-compare).

When running locally in the Azure Functions Core Tools, you should also add `FUNCTIONS_WORKER_RUNTIME`

to the [local.settings.json file](../../functions-develop-local#local-settings-file).

For apps following a migration guide, see that guide for relevant instructions. [Migrating .NET applications to the isolated worker model](../../migrate-dotnet-to-isolated-model) involves first setting `FUNCTIONS_WORKER_RUNTIME`

to `dotnet-isolated`

before deploying the updated application payload, and this event may appear temporarily between those steps.

## When to suppress the event

This event shouldn't be suppressed.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/openapi-apim-integrate-visual-studio -->

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
