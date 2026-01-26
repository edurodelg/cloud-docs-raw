---
merged_at: 2026-01-26T23:29:57.712609
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-http-webhook-trigger -->

# Azure Functions HTTP trigger

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The HTTP trigger lets you invoke a function with an HTTP request. You can use an HTTP trigger to build serverless APIs and respond to webhooks.

The default return value for an HTTP-triggered function is:

`HTTP 204 No Content`

with an empty body in Functions 2.x and higher`HTTP 200 OK`

with an empty body in Functions 1.x

To modify the HTTP response, configure an [output binding](functions-bindings-http-webhook-output).

For more information about HTTP bindings, see the [overview](functions-bindings-http-webhook) and [output binding reference](functions-bindings-http-webhook-output).

Tip

If you plan to use the HTTP or WebHook bindings, plan to avoid port exhaustion that can be caused by improper instantiation of `HttpClient`

. For more information, see [How to manage connections in Azure Functions](manage-connections).

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

The code in this article defaults to .NET Core syntax, used in Functions version 2.x and higher. For information on the 1.x syntax, see the [1.x functions templates](https://github.com/Azure/azure-functions-templates/tree/v1.x/Functions.Templates/Templates).

The following example shows an HTTP trigger that returns a "hello, world" response as an [IActionResult](/en-us/dotnet/api/microsoft.aspnetcore.mvc.iactionresult), using [ASP.NET Core integration in .NET Isolated](dotnet-isolated-process-guide#aspnet-core-integration):

```
[Function("HttpFunction")]
public IActionResult Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get")] HttpRequest req)
{
return new OkObjectResult($"Welcome to Azure Functions, {req.Query["name"]}!");
}
```


The following example shows an HTTP trigger that returns a "hello world" response as an [HttpResponseData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httpresponsedata) object:

```
[Function(nameof(HttpFunction))]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger(nameof(HttpFunction));
logger.LogInformation("message logged");
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString("Welcome to .NET isolated worker !!");
return response;
}
```


This section contains the following examples:

[Read parameter from the query string](#read-parameter-from-the-query-string)[Read body from a POST request](#read-body-from-a-post-request)[Read parameter from a route](#read-parameter-from-a-route)[Read POJO body from a POST request](#read-pojo-body-from-a-post-request)

The following examples show the HTTP trigger binding.

#### Read parameter from the query string

This example reads a parameter, named `id`

, from the query string, and uses it to build a JSON document returned to the client, with content type `application/json`

.

```
@FunctionName("TriggerStringGet")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
final ExecutionContext context) {
// Item list
context.getLogger().info("GET parameters are: " + request.getQueryParameters());
// Get named parameter
String id = request.getQueryParameters().getOrDefault("id", "");
// Convert and display
if (id.isEmpty()) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from to the client
// Generate document
final String name = "fake_name";
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(jsonDocument)
.build();
}
}
```


#### Read body from a POST request

This example reads the body of a POST request, as a `String`

, and uses it to build a JSON document returned to the client, with content type `application/json`

.

```
@FunctionName("TriggerStringPost")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
final ExecutionContext context) {
// Item list
context.getLogger().info("Request body is: " + request.getBody().orElse(""));
// Check request body
if (!request.getBody().isPresent()) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from to the client
// Generate document
final String body = request.getBody().get();
final String jsonDocument = "{\"id\":\"123456\", " +
"\"description\": \"" + body + "\"}";
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(jsonDocument)
.build();
}
}
```


#### Read parameter from a route

This example reads a mandatory parameter, named `id`

, and an optional parameter `name`

from the route path, and uses them to build a JSON document returned to the client, with content type `application/json`

.

```
@FunctionName("TriggerStringRoute")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "trigger/{id}/{name=EMPTY}") // name is optional and defaults to EMPTY
HttpRequestMessage<Optional<String>> request,
@BindingName("id") String id,
@BindingName("name") String name,
final ExecutionContext context) {
// Item list
context.getLogger().info("Route parameters are: " + id);
// Convert and display
if (id == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from to the client
// Generate document
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(jsonDocument)
.build();
}
}
```


#### Read POJO body from a POST request

Here's the code for the `ToDoItem`

class, referenced in this example:

```
public class ToDoItem {
private String id;
private String description;
public ToDoItem(String id, String description) {
this.id = id;
this.description = description;
}
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


This example reads the body of a POST request. The request body gets automatically de-serialized into a `ToDoItem`

object, and is returned to the client, with content type `application/json`

. The `ToDoItem`

parameter is serialized by the Functions runtime as it is assigned to the `body`

property of the `HttpMessageResponse.Builder`

class.

```
@FunctionName("TriggerPojoPost")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<ToDoItem>> request,
final ExecutionContext context) {
// Item list
context.getLogger().info("Request body is: " + request.getBody().orElse(null));
// Check request body
if (!request.getBody().isPresent()) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Document not found.")
.build();
}
else {
// return JSON from to the client
// Generate document
final ToDoItem body = request.getBody().get();
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(body)
.build();
}
}
```


The following example shows an HTTP trigger [TypeScript function](functions-reference-node?tabs=typescript). The function looks for a `name`

parameter either in the query string or the body of the [HTTP request](functions-reference-node?tabs=typescript&pivots=nodejs-model-v4#http-request).

```
import { app, HttpRequest, HttpResponseInit, InvocationContext } from '@azure/functions';
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text()) || 'world';
return { body: `Hello, ${name}!` };
}
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: httpTrigger1,
});
```


The following example shows an HTTP trigger [JavaScript function](functions-reference-node). The function looks for a `name`

parameter either in the query string or the body of the [HTTP request](functions-reference-node?tabs=javascript&pivots=nodejs-model-v4#http-request).

```
const { app } = require('@azure/functions');
app.http('httpTrigger1', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: async (request, context) => {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text()) || 'world';
return { body: `Hello, ${name}!` };
},
});
```


The following example shows a trigger binding in a *function.json* file and a [PowerShell function](functions-reference-powershell). The function looks for a `name`

parameter either in the query string or the body of the HTTP request.

```
{
"bindings": [
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
}
]
}
```


```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$name = $Request.Query.Name
if (-not $name) {
$name = $Request.Body.Name
}
$body = "This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response."
if ($name) {
$body = "Hello, $name. This HTTP triggered function executed successfully."
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $body
})
```


This example is an HTTP triggered function that uses [HTTP streams](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#http-streams-1) to return chunked response data. You might use these capabilities to support scenarios like sending event data through a pipeline for real time visualization or detecting anomalies in large sets of data and providing instant notifications.

```
import time
import azure.functions as func
from azurefunctions.extensions.http.fastapi import Request, StreamingResponse
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
def generate_sensor_data():
"""Generate real-time sensor data."""
for i in range(10):
# Simulate temperature and humidity readings
temperature = 20 + i
humidity = 50 + i
yield f"data: {{'temperature': {temperature}, 'humidity': {humidity}}}\n\n"
time.sleep(1)
@app.route(route="stream", methods=[func.HttpMethod.GET])
async def stream_sensor_data(req: Request) -> StreamingResponse:
"""Endpoint to stream real-time sensor data."""
return StreamingResponse(generate_sensor_data(), media_type="text/event-stream")
```


To learn more, including how to enable HTTP streams in your project, see [HTTP streams](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#http-streams-1).

This example shows a trigger binding and a Python function that uses the binding. The function looks for a `name`

parameter either in the query string or the body of the HTTP request.

```
import azure.functions as func
import logging
app = func.FunctionApp()
@app.function_name(name="HttpTrigger1")
@app.route(route="hello", auth_level=func.AuthLevel.ANONYMOUS)
def test_function(req: func.HttpRequest) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
return func.HttpResponse(
"This HTTP triggered function executed successfully.",
status_code=200
)
```


## Attributes

Both the [isolated worker model](dotnet-isolated-process-guide) and the [in-process model](functions-dotnet-class-library) use the `HttpTriggerAttribute`

to define the trigger binding. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#http-trigger).

In [isolated worker model](dotnet-isolated-process-guide) function apps, the `HttpTriggerAttribute`

supports the following parameters:

| Parameters | Description |
|---|---|
AuthLevel |
Determines what keys, if any, need to be present on the request in order to invoke the function. For supported values, see
|

**Methods**[customize the HTTP endpoint](#customize-the-http-endpoint).**Route**`<functionname>`

. For more information, see [customize the HTTP endpoint](#customize-the-http-endpoint).## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties for a trigger are defined in the `route`

decorator, which adds HttpTrigger and HttpOutput binding:

| Property | Description |
|---|---|
`route` |
Route for the http endpoint. If None, it will be set to function name if present or user-defined python function name. |
`trigger_arg_name` |
Argument name for HttpRequest. The default value is 'req'. |
`binding_arg_name` |
Argument name for HttpResponse. The default value is '$return'. |
`methods` |
A tuple of the HTTP methods to which the function responds. |
`auth_level` |
Determines what keys, if any, need to be present on the request in order to invoke the function. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [HttpTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.httptrigger) annotation, which supports the following settings:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.http()`

method.

| Property | Description |
|---|---|
authLevel |
Determines what keys, if any, need to be present on the request in order to invoke the function. For supported values, see
|

**methods**[customize the HTTP endpoint](#customize-the-http-endpoint).**route**`<functionname>`

. For more information, see [customize the HTTP endpoint](#customize-the-http-endpoint).The following table explains the trigger configuration properties that you set in the *function.json* file, which differs by runtime version.

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Required - must be set to `httpTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code for the request or request body. |
authLevel |
Determines what keys, if any, need to be present on the request in order to invoke the function. For supported values, see
|

**methods**[customize the HTTP endpoint](#customize-the-http-endpoint).**route**`<functionname>`

. For more information, see [customize the HTTP endpoint](#customize-the-http-endpoint).## Usage

This section details how to configure your HTTP trigger function binding.

The [HttpTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.httptrigger) annotation should be applied to a method parameter of one of the following types:

[HttpRequestMessage<T>](/en-us/java/api/com.microsoft.azure.functions.httprequestmessage).- Any native Java types such as int, String, byte[].
- Nullable values using Optional.
- Any plain-old Java object (POJO) type.

### Payload

The trigger input type is declared as one of the following types:

| Type | Description |
|---|---|
|

*Use of this type requires that the app is configured with*[ASP.NET Core integration in .NET Isolated](dotnet-isolated-process-guide#aspnet-core-integration).This gives you full access to the request object and overall HttpContext.

[HttpRequestData](/en-us/dotnet/api/microsoft.azure.functions.worker.http.httprequestdata)When the trigger parameter is of type `HttpRequestData`

or `HttpRequest`

, custom types can also be bound to other parameters using `Microsoft.Azure.Functions.Worker.Http.FromBodyAttribute`

. Use of this attribute requires [ Microsoft.Azure.Functions.Worker.Extensions.Http version 3.1.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Http). This is a different type than the similar attribute in

`Microsoft.AspNetCore.Mvc`

. When using ASP.NET Core integration, you need a fully qualified reference or `using`

statement. This example shows how to use the attribute to get just the body contents while still having access to the full `HttpRequest`

, using ASP.NET Core integration:```
using Microsoft.AspNetCore.Http;
using Microsoft.AspNetCore.Mvc;
using Microsoft.Azure.Functions.Worker;
namespace AspNetIntegration
{
public class BodyBindingHttpTrigger
{
[Function(nameof(BodyBindingHttpTrigger))]
public IActionResult Run([HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequest req,
[Microsoft.Azure.Functions.Worker.Http.FromBody] Person person)
{
return new OkObjectResult(person);
}
}
public record Person(string Name, int Age);
}
```


### Customize the HTTP endpoint

By default when you create a function for an HTTP trigger, the function is addressable with a route of the form:

```
https://<APP_NAME>.azurewebsites.net/api/<FUNCTION_NAME>
```


You can customize this route using the optional `route`

property on the HTTP trigger's input binding. You can use any [ASP.NET Core Route Constraint](/en-us/aspnet/core/fundamentals/routing#route-constraints) with your parameters.

The following function code accepts two parameters `category`

and `id`

in the route and writes a response using both parameters.

```
[Function("HttpTrigger1")]
public static HttpResponseData Run([HttpTrigger(AuthorizationLevel.Function, "get", "post",
Route = "products/{category:alpha}/{id:int?}")] HttpRequestData req, string category, int? id,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpTrigger1");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = String.Format($"Category: {category}, ID: {id}");
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
return response;
}
```


Route parameters are defined using the `route`

setting of the `HttpTrigger`

annotation. The following function code accepts two parameters `category`

and `id`

in the route and writes a response using both parameters.

```
package com.function;
import java.util.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.*;
public class HttpTriggerJava {
public HttpResponseMessage<String> HttpTrigger(
@HttpTrigger(name = "req",
methods = {"get"},
authLevel = AuthorizationLevel.FUNCTION,
route = "products/{category:alpha}/{id:int}") HttpRequestMessage<String> request,
@BindingName("category") String category,
@BindingName("id") int id,
final ExecutionContext context) {
String message = String.format("Category %s, ID: %d", category, id);
return request.createResponseBuilder(HttpStatus.OK).body(message).build();
}
}
```


As an example, the following TypeScript code defines a `route`

property for an HTTP trigger with two parameters, `category`

and `id`

. The example reads the parameters from the request and returns their values in the response.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext } from '@azure/functions';
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const category = request.params.category;
const id = request.params.id;
return { body: `Category: ${category}, ID: ${id}` };
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
route: 'products/{category:alpha}/{id:int?}',
handler: httpTrigger1,
});
```


As an example, the following JavaScript code defines a `route`

property for an HTTP trigger with two parameters, `category`

and `id`

. The example reads the parameters from the request and returns their values in the response.

```
const { app } = require('@azure/functions');
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
route: 'products/{category:alpha}/{id:int?}',
handler: async (request, context) => {
const category = request.params.category;
const id = request.params.id;
return { body: `Category: ${category}, ID: ${id}` };
},
});
```


As an example, the following code defines a `route`

property for an HTTP trigger with two parameters, `category`

and `id`

:

Route parameters declared in the *function.json* file are accessible as a property of the `$Request.Params`

object.

```
$Category = $Request.Params.category
$Id = $Request.Params.id
$Message = "Category:" + $Category + ", ID: " + $Id
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = $Message
})
```


The function execution context is exposed via a parameter declared as `func.HttpRequest`

. This instance allows a function to access data route parameters, query string values and methods that allow you to return HTTP responses.

Once defined, the route parameters are available to the function by calling the `route_params`

method.

```
import logging
import azure.functions as func
def main(req: func.HttpRequest) -> func.HttpResponse:
category = req.route_params.get('category')
id = req.route_params.get('id')
message = f"Category: {category}, ID: {id}"
return func.HttpResponse(message)
```


Using this configuration, the function is now addressable with the following route instead of the original route.

```
https://<APP_NAME>.azurewebsites.net/api/products/electronics/357
```


This configuration allows the function code to support two parameters in the address, *category* and *ID*. For more information on how route parameters are tokenized in a URL, see [Routing in ASP.NET Core](/en-us/aspnet/core/fundamentals/routing#route-constraint-reference).

By default, all function routes are prefixed with `api`

. You can also customize or remove the prefix using the `extensions.http.routePrefix`

property in your [host.json](functions-host-json) file. The following example removes the `api`

route prefix by using an empty string for the prefix in the *host.json* file.

```
{
"extensions": {
"http": {
"routePrefix": ""
}
}
}
```


### Using route parameters

Route parameters that defined a function's `route`

pattern are available to each binding. For example, if you have a route defined as `"route": "products/{id}"`

then a table storage binding can use the value of the `{id}`

parameter in the binding configuration.

The following configuration shows how the `{id}`

parameter is passed to the binding's `rowKey`

.

```
import { app, HttpRequest, HttpResponseInit, input, InvocationContext } from '@azure/functions';
const tableInput = input.table({
connection: 'MyStorageConnectionAppSetting',
partitionKey: 'products',
tableName: 'products',
rowKey: '{id}',
});
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
return { jsonBody: context.extraInputs.get(tableInput) };
}
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
route: 'products/{id}',
extraInputs: [tableInput],
handler: httpTrigger1,
});
```


```
const { app, input } = require('@azure/functions');
const tableInput = input.table({
connection: 'MyStorageConnectionAppSetting',
partitionKey: 'products',
tableName: 'products',
rowKey: '{id}',
});
app.http('httpTrigger1', {
methods: ['GET'],
authLevel: 'anonymous',
route: 'products/{id}',
extraInputs: [tableInput],
handler: async (request, context) => {
return { jsonBody: context.extraInputs.get(tableInput) };
},
});
```


```
{
"type": "table",
"direction": "in",
"name": "product",
"partitionKey": "products",
"tableName": "products",
"rowKey": "{id}"
}
```


When you use route parameters, an `invoke_URL_template`

is automatically created for your function. Your clients can use the URL template to understand the parameters they need to pass in the URL when calling your function using its URL. Navigate to one of your HTTP-triggered functions in the [Azure portal](https://portal.azure.com) and select **Get function URL**.

You can programmatically access the `invoke_URL_template`

by using the Azure Resource Manager APIs for [List Functions](/en-us/rest/api/appservice/webapps/listfunctions) or [Get Function](/en-us/rest/api/appservice/webapps/getfunction).

### HTTP streams

You can now stream requests to and responses from your HTTP endpoint in Node.js v4 function apps. For more information, see [HTTP streams](functions-reference-node?pivots=nodejs-model-v4#http-streams).

### HTTP streams

HTTP streams support in Python lets you accept and return data from your HTTP endpoints using FastAPI request and response APIs enabled in your functions. These APIs enable the host to process data in HTTP messages as chunks instead of having to read an entire message into memory.

### Prerequisites

[Azure Functions runtime](functions-versions?pivots=programming-language-python)version 4.34.1, or a later version.[Python](https://www.python.org/downloads/)version 3.8, or a later[supported version](functions-reference-python?tabs=get-started&pivots=python-mode-decorators#supported-python-versions).

Important

HTTP streams is only supported for the Python v2 programming model.

### Enable HTTP streams

HTTP streams are disabled by default. You need to enable this feature in your application settings and also update your code to use the FastAPI package. Note that when enabling HTTP streams, the function app will default to using HTTP streaming, and the original HTTP functionality will not work.

Add the

`azurefunctions-extensions-http-fastapi`

extension package to the`requirements.txt`

file in the project, which should include at least these packages:`azure-functions azurefunctions-extensions-http-fastapi`

Add this code to the

`function_app.py`

file in the project, which imports the FastAPI extension:`from azurefunctions.extensions.http.fastapi import Request, StreamingResponse`

When you deploy to Azure, add the following

[application setting](functions-how-to-use-azure-function-app-settings#settings)in your function app:`"PYTHON_ENABLE_INIT_INDEXING": "1"`

When running locally, you also need to add these same settings to the

`local.settings.json`

project file.

### HTTP streams examples

After you enable the HTTP streaming feature, you can create functions that stream data over HTTP.

This example is an HTTP triggered function that receives and processes streaming data from a client in real time. It demonstrates streaming upload capabilities that can be helpful for scenarios like processing continuous data streams and handling event data from IoT devices.

```
import azure.functions as func
from azurefunctions.extensions.http.fastapi import JSONResponse, Request
app = func.FunctionApp(http_auth_level=func.AuthLevel.FUNCTION)
@app.route(route="streaming_upload", methods=[func.HttpMethod.POST])
async def streaming_upload(req: Request) -> JSONResponse:
"""Handle streaming upload requests."""
# Process each chunk of data as it arrives
async for chunk in req.stream():
process_data_chunk(chunk)
# Once all data is received, return a JSON response indicating successful processing
return JSONResponse({"status": "Data uploaded and processed successfully"})
def process_data_chunk(chunk: bytes):
"""Process each data chunk."""
# Add custom processing logic here
pass
```


### Calling HTTP streams

You must use an HTTP client library to make streaming calls to a function's FastAPI endpoints. The client tool or browser you're using might not natively support streaming or could only return the first chunk of data.

You can use a client script like this to send streaming data to an HTTP endpoint:

```
import httpx # Be sure to add 'httpx' to 'requirements.txt'
import asyncio
async def stream_generator(file_path):
chunk_size = 2 * 1024 # Define your own chunk size
with open(file_path, 'rb') as file:
while chunk := file.read(chunk_size):
yield chunk
print(f"Sent chunk: {len(chunk)} bytes")
async def stream_to_server(url, file_path):
timeout = httpx.Timeout(60.0, connect=60.0)
async with httpx.AsyncClient(timeout=timeout) as client:
response = await client.post(url, content=stream_generator(file_path))
return response
async def stream_response(response):
if response.status_code == 200:
async for chunk in response.aiter_raw():
print(f"Received chunk: {len(chunk)} bytes")
else:
print(f"Error: {response}")
async def main():
print('helloworld')
# Customize your streaming endpoint served from core tool in variable 'url' if different.
url = 'http://localhost:7071/api/streaming_upload'
file_path = r'<file path>'
response = await stream_to_server(url, file_path)
print(response)
if __name__ == "__main__":
asyncio.run(main())
```


Important

If you are using HTTP streams, all HTTP functions in the app need to use streaming. Combining streaming and non-streaming HTTP functions within the same app is not supported.

### Working with client identities

If your function app is using [App Service Authentication / Authorization](../app-service/overview-authentication-authorization), you can view information about authenticated clients from your code. This information is available as [request headers injected by the platform](../app-service/configure-authentication-user-identities#access-user-claims-in-app-code).

You can also read this information from binding data.

Note

Access to authenticated client information is currently only available for .NET languages. It also isn't supported in version 1.x of the Functions runtime.

Information regarding authenticated clients is available as a [ClaimsPrincipal](/en-us/dotnet/api/system.security.claims.claimsprincipal), which is available as part of the request context as shown in the following example:

The authenticated user is available via [HTTP Headers](../app-service/configure-authentication-user-identities#access-user-claims-in-app-code).

The authenticated user is available via [HTTP Headers](../app-service/configure-authentication-user-identities#access-user-claims-in-app-code).

### Authorization level

The authorization level is a string value that indicates the kind of [authorization key](#authorization-keys) that's required to access the function endpoint. For an HTTP triggered function, the authorization level can be one of the following values:

| Level value | Description |
|---|---|
anonymous |
No access key is required. |
function |
A function-specific key is required to access the endpoint. |
admin |
The master key is required to access the endpoint. |

When a level isn't explicitly set, authorization defaults to the `function`

level.

When a level isn't explicitly set, the default authorization depends on the version of the Node.js model:

### Function access keys

Functions lets you use access keys to make it harder to access your function endpoints. Unless the authorization level on an HTTP triggered function is set to `anonymous`

, requests must include an access key in the request. For more information, see [Work with access keys in Azure Functions](function-keys-how-to).

### Access key authorization

Most HTTP trigger templates require an access key in the request. So your HTTP request normally looks like the following URL:

```
https://<APP_NAME>.azurewebsites.net/api/<FUNCTION_NAME>?code=<API_KEY>
```


Function apps that run in containers use the domain of the container host. For an example HTTP endpoint hosted in Azure Container Apps, see the example in [this Container Apps hosting article](functions-deploy-container-apps#verify-your-functions-on-azure).

The key can be included in a query string variable named `code`

, as mentioned earlier. It can also be included in an `x-functions-key`

HTTP header. The value of the key can be any function key defined for the function, or any host key.

You can allow anonymous requests, which don't require keys. You can also require that the master key is used. You change the default authorization level by using the `authLevel`

property in the binding JSON.

Note

When running functions locally, authorization is disabled regardless of the specified authorization level setting. After publishing to Azure, the `authLevel`

setting in your trigger is enforced. Keys are still required when running [locally in a container](functions-create-container-registry#build-the-container-image-and-verify-locally).

### Webhooks

Note

Webhook mode is only available for version 1.x of the Functions runtime. This change was made to improve the performance of HTTP triggers in version 2.x and higher.

In version 1.x, webhook templates provide another validation for webhook payloads. In version 2.x and higher, the base HTTP trigger still works and is the recommended approach for webhooks.

#### WebHook type

The `webHookType`

binding property indicates the type if webhook supported by the function, which also dictates the supported payload. The webhook type can be one of the following values:

| Type value | Description |
|---|---|
`genericJson` |
A general-purpose webhook endpoint without logic for a specific provider. This setting restricts requests to only those using HTTP POST and with the `application/json` content type. |
`github` |
The function responds to
`authLevel` property with GitHub webhooks. |

`slack`

[Slack webhooks](https://api.slack.com/outgoing-webhooks). Don't use the`authLevel`

property with Slack webhooks.When setting the `webHookType`

property, don't also set the `methods`

property on the binding.

#### GitHub webhooks

To respond to GitHub webhooks, first create your function with an HTTP Trigger, and set the **webHookType** property to `github`

. Then copy its URL and API key into the **Add webhook** page of your GitHub repository.

#### Slack webhooks

The Slack webhook generates a token for you instead of letting you specify it, so you must configure a function-specific key with the token from Slack. See [Authorization keys](#authorization-keys).

### Webhooks and keys

Webhook authorization is handled by the webhook receiver component, part of the HTTP trigger, and the mechanism varies based on the webhook type. Each mechanism does rely on a key. By default, the function key named "default" is used. To use a different key, configure the webhook provider to send the key name with the request in one of the following ways:

**Query string**: The provider passes the key name in the`clientid`

query string parameter, such as`https://<APP_NAME>.azurewebsites.net/api/<FUNCTION_NAME>?clientid=<KEY_NAME>`

.**Request header**: The provider passes the key name in the`x-functions-clientid`

header.

## Invoke HTTP triggers

You can invoke your HTTP-triggered functions using an HTTP client. The examples in this section use [ curl](https://github.com/curl/curl), but you can use any HTTP client tool that keeps your data secure. For more information, see

[HTTP test tools](functions-develop-local#http-test-tools).

The request you need to make might be different between a local version of your code and when hosted in Azure. By default, when you run your project using the Azure Functions Core Tools, access key authorization requirements are removed. However, any requirements you've configured will still be enforced when hosted.

### Invoke locally

The [Azure Functions Core Tools](functions-develop-local) registers a `localhost`

endpoint for your function app, which you can use to invoke your functions. During application startup, the specific port being used is displayed in the console. The output also lists the available functions, and for each HTTP-triggered function, the output also includes the function's route template.

Use this information to construct the URL to provide to your API client. You also need to specify any headers, parameters, and request body information your function requires. The following example sends an HTTP POST request with a JSON body:

```
curl --request POST http://localhost:7071/api/Function1 --header "Content-Type: application/json" --data '{"message":"test data"}'
```


### Invoke in Azure

When invoking an HTTP-triggered function hosted in Azure, you need to consider your networking configuration. The HTTP client must have network access to the app, so if you have [inbound networking restrictions](functions-networking-options#inbound-networking-features) enabled, the client might need to be within a virtual network or specific IP ranges. Your domain configuration determines the base URL you need to use for the request.

Note

Newly created function apps can generate a unique default host name that uses the naming convention `<app-name>-<random-hash>.<region>.azurewebsites.net`

. An example is `myapp-ds27dh7271aah175.westus-01.azurewebsites.net`

. Existing app names remain unchanged.

For more information, see the [blog post about creating an app with a unique default host name](https://techcommunity.microsoft.com/blog/appsonazureblog/secure-unique-default-hostnames-ga-on-app-service-web-apps-and-public-preview-on/4303571).

Unless you selected the anonymous [authorization level](#http-auth) in your trigger definition, your request may also need to [include an access key](function-keys-how-to#use-access-keys).

The following example sends an HTTP POST request with a function body, including the access key in the query string:

```
curl --request POST "https://<your-function-app-base-url>/api/Function1?code=<your-function-key>" --header "Content-Type: application/json" --data '{"message":"test data"}'
```


## Content types

Passing binary and form data to a non-C# function requires that you use the appropriate content-type header. Supported content types include `octet-stream`

for binary data and [multipart types](https://www.iana.org/assignments/media-types/media-types.xhtml#multipart).

#### Known issues

In non-C# functions, requests sent with the content-type `image/jpeg`

results in a `string`

value passed to the function. In cases like these, you can manually convert the `string`

value to a byte array to access the raw binary data.

### Limits

The HTTP request size and URL lengths are both limited based on [settings defined in the host](https://github.com/Azure/azure-functions-host/blob/dev/src/WebJobs.Script.WebHost/web.config#L19). For more information, see [Service limits](functions-scale#service-limits).

If a function that uses the HTTP trigger doesn't complete within 230 seconds, the [Azure Load Balancer](../app-service/faq-availability-performance-application-issues#why-does-my-request-time-out-after-230-seconds-) will time out and return an HTTP 502 error. The function will continue running but will be unable to return an HTTP response. For long-running functions, we recommend that you follow async patterns and return a location where you can ping the status of the request. For information about how long a function can run, see [Scale and hosting - Consumption plan](functions-scale#timeout).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-function-resource-manager -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-queue-output -->

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
