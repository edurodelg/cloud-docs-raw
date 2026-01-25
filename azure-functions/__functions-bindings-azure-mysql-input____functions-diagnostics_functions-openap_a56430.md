---
merged_at: 2026-01-25T15:41:11.660954
merged_files: 2
---

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
