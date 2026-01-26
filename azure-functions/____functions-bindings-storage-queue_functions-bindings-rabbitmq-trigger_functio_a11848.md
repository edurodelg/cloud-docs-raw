---
merged_at: 2026-01-26T21:02:36.330007
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-queue -->

# Azure Queue storage trigger and bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions can run as new Azure Queue storage messages are created and can write queue messages within a function.

| Action | Type |
|---|---|
| Run a function as queue storage data changes |
|

[Output binding](functions-bindings-storage-queue-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [Azure.Storage.Queues](/en-us/dotnet/api/azure.storage.queues).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues), version 5.x.

Using the .NET CLI:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues
```


Note

Azure Blobs, Azure Queues, and Azure Tables now use separate extensions and are referenced individually. For example, to use the triggers and bindings for all three services in your .NET isolated-process app, you should add the following packages to your project:

[Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs)[Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues)[Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables)

Previously, the extensions shipped together as [Microsoft.Azure.Functions.Worker.Extensions.Storage, version 4.x](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/4.0.4). This same package also has a [5.x version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/5.0.0), which references the split packages for blobs and queues only. When upgrading your package references from older versions, you may therefore need to additionally reference the new [Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) NuGet package. Also, when referencing these newer split packages, make sure you are not referencing an older version of the combined storage package, as this will result in conflicts from two definitions of the same bindings.

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

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Azure.Storage.Queues](/en-us/dotnet/api/azure.storage.queues) is in preview.

**Queue trigger**

The queue trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message content as a string. Use when the message is simple text.. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | When a queue message contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BinaryData](/en-us/dotnet/api/system.binarydata)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues 5.2.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues/5.2.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Queue output binding**

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

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

Note

For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1).

```
{
"version": "2.0",
"extensions": {
"queues": {
"maxPollingInterval": "00:00:02",
"visibilityTimeout" : "00:00:30",
"batchSize": 16,
"maxDequeueCount": 5,
"newBatchThreshold": 8,
"messageEncoding": "base64"
}
}
}
```


| Property | Default | Description |
|---|---|---|
| maxPollingInterval | 00:01:00 | The maximum interval between queue polls. The minimum interval is 00:00:00.100 (100 ms). Intervals increment up to `maxPollingInterval` . The default value of `maxPollingInterval` is 00:01:00 (1 min). `maxPollingInterval` must not be less than 00:00:00.100 (100 ms). In Functions 2.x and later, the data type is a `TimeSpan` . In Functions 1.x, it is in milliseconds. |
| visibilityTimeout | 00:00:00 | The time interval between retries when processing of a message fails. |
| batchSize | 16 | The number of queue messages that the Functions runtime retrieves simultaneously and processes in parallel. When the number being processed gets down to the `newBatchThreshold` , the runtime gets another batch and starts processing those messages. So the maximum number of concurrent messages being processed per function is `batchSize` plus `newBatchThreshold` . This limit applies separately to each queue-triggered function. If you want to avoid parallel execution for messages received on one queue, you can set `batchSize` to 1. However, this setting eliminates concurrency as long as your function app runs only on a single virtual machine (VM). If the function app scales out to multiple VMs, each VM could run one instance of each queue-triggered function.The maximum `batchSize` is 32. |
| maxDequeueCount | 5 | The number of times to try processing a message before moving it to the poison queue. |
| newBatchThreshold | N*batchSize/2 | Whenever the number of messages being processed concurrently gets down to this number, the runtime retrieves another batch.`N` represents the number of vCPUs available when running on App Service or Premium Plans. Its value is `1` for the Consumption Plan. |
| messageEncoding | base64 | This setting is only available in
`base64` and `none` . |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-rabbitmq-trigger -->

# RabbitMQ trigger for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use the RabbitMQ trigger to respond to messages from a RabbitMQ queue.

Note

The RabbitMQ bindings are only fully supported on [Elastic Premium](functions-premium-plan) and [Dedicated (App Service)](dedicated-plan) plans. [Flex Consumption](flex-consumption-plan) and [Consumption](consumption-plan) plans aren't yet supported.

RabbitMQ bindings aren't supported by the Azure Functions v1.x runtime.

For information on setup and configuration details, see the [overview](functions-bindings-rabbitmq).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

```
[Function(nameof(RabbitMQFunction))]
[RabbitMQOutput(QueueName = "destinationQueue", ConnectionStringSetting = "RabbitMQConnection")]
public static string Run([RabbitMQTrigger("queue", ConnectionStringSetting = "RabbitMQConnection")] string item,
FunctionContext context)
{
var logger = context.GetLogger(nameof(RabbitMQFunction));
logger.LogInformation(item);
var message = $"Output message created at {DateTime.Now}";
return message;
}
```


The following Java function uses the `@RabbitMQTrigger`

annotation from the [Java RabbitMQ types](https://mvnrepository.com/artifact/com.microsoft.azure.functions/azure-functions-java-library-rabbitmq) to describe the configuration for a RabbitMQ queue trigger. The function grabs the message placed on the queue and adds it to the logs.

```
@FunctionName("RabbitMQTriggerExample")
public void run(
@RabbitMQTrigger(connectionStringSetting = "rabbitMQConnectionAppSetting", queueName = "queue") String input,
final ExecutionContext context)
{
context.getLogger().info("Java HTTP trigger processed a request." + input);
}
```


The following example shows a RabbitMQ trigger binding in a *function.json* file and a [JavaScript function](functions-reference-node) that uses the binding. The function reads and logs a RabbitMQ message.

Here's the binding data in the *function.json* file:

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "rabbitMQTrigger",
"direction": "in",
"queueName": "queue",
"connectionStringSetting": "rabbitMQConnectionAppSetting"
}
]
}
```


Here's the JavaScript script code:

```
module.exports = async function (context, myQueueItem) {
context.log('JavaScript RabbitMQ trigger function processed work item', myQueueItem);
};
```


The following example demonstrates how to read a RabbitMQ queue message via a trigger.

A RabbitMQ binding is defined in *function.json* where *type* is set to `RabbitMQTrigger`

.

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"name": "myQueueItem",
"type": "rabbitMQTrigger",
"direction": "in",
"queueName": "queue",
"connectionStringSetting": "rabbitMQConnectionAppSetting"
}
]
}
```


```
import logging
import azure.functions as func
def main(myQueueItem) -> None:
logging.info('Python RabbitMQ trigger function processed a queue item: %s', myQueueItem)
```


PowerShell examples aren't currently available.

## Attributes

Both [isolated worker process](dotnet-isolated-process-guide) and [in-process](functions-dotnet-class-library) C# libraries use `RabbitMQTriggerAttribute`

to define the function, where specific properties of the attribute depend on the extension version.

The attribute's constructor accepts these parameters:

| Parameter | Description |
|---|---|
QueueName |
Name of the queue from which to receive messages. |
HostName |
This parameter is no longer supported and is ignored. It will be removed in a future version. |
ConnectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**UserNameSetting****PasswordSetting****Port**`5672`

.## Annotations

The `RabbitMQTrigger`

annotation allows you to create a function that runs when a RabbitMQ message is created.

The annotation supports the following configuration options:

| Parameter | Description |
|---|---|
queueName |
Name of the queue from which to receive messages. |
connectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**disableCertificateValidation**`true`

indicating that certificate validation should be disabled. Default value is `false`

. Not recommended for production. Does not apply when SSL is disabled.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `RabbitMQTrigger` . |
direction |
Must be set to `in` . |
name |
The name of the variable that represents the queue in function code. |
queueName |
Name of the queue from which to receive messages. |
connectionStringSetting |
The name of the app setting that contains the connection string for your RabbitMQ server. This setting only takes an app setting key name, you can't directly set a connection string value. For more information, see
|

**disableCertificateValidation**`true`

indicating that certificate validation should be disabled. Default value is `false`

. Not recommended for production. Does not apply when SSL is disabled.When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

See the [Example section](#example) for complete examples.

## Usage

The parameter type supported by the RabbitMQ trigger depends on the C# modality used.

The RabbitMQ bindings currently support only string and serializable object types when running in an isolated process.

The queue message is available via `context.bindings.<NAME>`

where `<NAME>`

matches the name defined in function.json. If the payload is JSON, the value is deserialized into an object.

### Connections

Important

The RabbitMQ binding doesn't support Microsoft Entra authentication and managed identities. You can use Azure Key Vault to centrally managed your RabbitMQ connection strings. To learn more, see [Manage Connections](manage-connections).

Starting with version 2.x of the extension, `hostName`

, `userNameSetting`

, and `passwordSetting`

are no longer supported to define a connection to the RabbitMQ server. You must instead use `connectionStringSetting`

.

The `connectionStringSetting`

property can only accept the name of a key-value pair in app settings. You can't directly set a connection string value in the binding.

For example, when you have set `connectionStringSetting`

to `rabbitMQConnection`

in your binding definition, your function app must have an app setting named `rabbitMQConnection`

that returns either a connection value like `amqp://myuser:***@contoso.rabbitmq.example.com:5672`

or an [Azure Key Vault reference](../app-service/app-service-key-vault-references).

When running locally, you must also have the key value for `connectionStringSetting`

defined in your *local.settings.json* file. Otherwise, your app can't connect to the service from your local computer and an error occurs.

### Dead letter queues

Dead letter queues and exchanges can't be controlled or configured from the RabbitMQ trigger. To use dead letter queues, pre-configure the queue used by the trigger in RabbitMQ. Refer to the [RabbitMQ documentation](https://www.rabbitmq.com/dlx.html).

### Enable Runtime Scaling

In order for the RabbitMQ trigger to scale out to multiple instances, the **Runtime Scale Monitoring** setting must be enabled.

In the portal, this setting can be found under **Configuration** > **Function runtime settings** for your function app.


In the Azure CLI, you can enable **Runtime Scale Monitoring** by using this command:

```
az resource update -resource-group <RESOURCE_GROUP> -name <APP_NAME>/config/web \
--set properties.functionsRuntimeScaleMonitoringEnabled=1 \
--resource-type Microsoft.Web/sites
```


### Monitoring a RabbitMQ endpoint

To monitor your queues and exchanges for a certain RabbitMQ endpoint:

- Enable the
[RabbitMQ management plugin](https://www.rabbitmq.com/management.html) - Browse to
`http://{node-hostname}:15672`

and log in with your user name and password.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-data-explorer-input -->

# Azure Data Explorer input bindings for Azure Functions (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Data Explorer input binding retrieves data from a database.

## Examples

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

More samples for the Azure Data Explorer input binding (out of process) are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-outofproc).

This section contains the following examples:

The examples refer to a `Product`

class and the Products table, both of which are defined in the previous sections.

### HTTP trigger, get row by ID from query string

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single record. The function is triggered by an HTTP request that uses a query string to specify the ID. That ID is used to retrieve a `Product`

record with the specified query.

Note

The HTTP query string parameter is case sensitive.

```
using System.Text.Json.Nodes;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Kusto;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common;
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.InputBindingSamples
{
public static class GetProductsQuery
{
[Function("GetProductsQuery")]
public static JsonArray Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproductsquery")] HttpRequestData req,
[KustoInput(Database: "productsdb",
KqlCommand = "declare query_parameters (productId:long);Products | where ProductID == productId",
KqlParameters = "@productId={Query.productId}",Connection = "KustoConnectionString")] JsonArray products)
{
return products;
}
}
}
```


### HTTP trigger, get multiple rows from route parameter

The following example shows a [C# function](functions-dotnet-class-library) that retrieves records returned by the query (based on the name of the product, in this case). The function is triggered by an HTTP request that uses route data to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Kusto;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.OutputBindingSamples.Common;
namespace Microsoft.Azure.WebJobs.Extensions.Kusto.SamplesOutOfProc.InputBindingSamples
{
public static class GetProductsFunction
{
[Function("GetProductsFunction")]
public static IEnumerable<Product> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = "getproductsfn/{name}")] HttpRequestData req,
[KustoInput(Database: "productsdb",
KqlCommand = "declare query_parameters (name:string);GetProductsByName(name)",
KqlParameters = "@name={name}",Connection = "KustoConnectionString")] IEnumerable<Product> products)
{
return products;
}
}
}
```


More samples for the Java Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-java).

This section contains the following examples:

The examples refer to a `Product`

class (in a separate file `Product.java`

) and a corresponding database table.

```
package com.microsoft.azure.kusto.common;
import com.fasterxml.jackson.annotation.JsonProperty;
public class Product {
@JsonProperty("ProductID")
public long ProductID;
@JsonProperty("Name")
public String Name;
@JsonProperty("Cost")
public double Cost;
public Product() {
}
public Product(long ProductID, String name, double Cost) {
this.ProductID = ProductID;
this.Name = name;
this.Cost = Cost;
}
}
```


### HTTP trigger, get multiple rows

The example uses a route parameter to specify the name of the ID of the products. All matching products are retrieved from the products table.

```
package com.microsoft.azure.kusto.inputbindings;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.kusto.annotation.KustoInput;
import com.microsoft.azure.kusto.common.Product;
import java.util.Optional;
public class GetProducts {
@FunctionName("GetProducts")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {
HttpMethod.GET}, authLevel = AuthorizationLevel.ANONYMOUS, route = "getproducts/{productId}") HttpRequestMessage<Optional<String>> request,
@KustoInput(name = "getjproducts", kqlCommand = "declare query_parameters (productId:long);Products | where ProductID == productId",
kqlParameters = "@productId={productId}", database = "productsdb", connection = "KustoConnectionString") Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products)
.build();
}
}
```


### HTTP trigger, get row by ID from query string

The following example shows a query for the products table by the product name. The function is triggered by an HTTP request that uses a query string to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

```
package com.microsoft.azure.kusto.inputbindings;
import com.microsoft.azure.functions.HttpMethod;
import com.microsoft.azure.functions.HttpRequestMessage;
import com.microsoft.azure.functions.HttpResponseMessage;
import com.microsoft.azure.functions.HttpStatus;
import com.microsoft.azure.functions.annotation.AuthorizationLevel;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.annotation.HttpTrigger;
import com.microsoft.azure.functions.kusto.annotation.KustoInput;
import com.microsoft.azure.kusto.common.Product;
import java.util.Optional;
public class GetProductsQueryString {
@FunctionName("GetProductsQueryString")
public HttpResponseMessage run(@HttpTrigger(name = "req", methods = {
HttpMethod.GET}, authLevel = AuthorizationLevel.ANONYMOUS, route = "getproducts") HttpRequestMessage<Optional<String>> request,
@KustoInput(name = "getjproductsquery", kqlCommand = "declare query_parameters (name:string);GetProductsByName(name)",
kqlParameters = "@name={Query.name}", database = "productsdb", connection = "KustoConnectionString") Product[] products) {
return request.createResponseBuilder(HttpStatus.OK).header("Content-Type", "application/json").body(products)
.build();
}
}
```


More samples for the Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-node).

This section contains the following examples:

The examples refer to a database table:

### HTTP trigger, get multiple rows

The following example shows an Azure Data Explorer input binding in a *function.json* file and a JavaScript function that reads from a query and returns the results in the HTTP response.

The following binding data is in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"get"
],
"route": "getproducts/{productId}"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "productget",
"type": "kusto",
"database": "productsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (productId:long);Products | where ProductID == productId",
"kqlParameters": "@productId={productId}",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample JavaScript code:

```
module.exports = async function (context, req, productget) {
return {
status: 200,
body: productget
};
}
```


### HTTP trigger, get row by name from query string

The following example shows a query for the products table by the product name. The function is triggered by an HTTP request that uses a query string to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

The following binding data is in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"get"
],
"route": "getproductsfn"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "productfnget",
"type": "kusto",
"database": "productsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (name:string);GetProductsByName(name)",
"kqlParameters": "@name={Query.name}",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample JavaScript code:

```
module.exports = async function (context, req, producproductfngettget) {
return {
status: 200,
body: productfnget
};
}
```


More samples for the Azure Data Explorer input binding are available in the [GitHub repository](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python).

This section contains the following examples:

### HTTP trigger, get multiple rows

The following example shows an Azure Data Explorer input binding in a *function.json* file and a Python function that reads from a query and returns the results in the HTTP response.

The following binding data is in the *function.json* file:

```
{
"scriptFile": "__init__.py",
"bindings": [
{
"authLevel": "Anonymous",
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": [
"get"
],
"route": "getproducts/{productId}"
},
{
"type": "http",
"direction": "out",
"name": "$return"
},
{
"name": "productsdb",
"type": "kusto",
"database": "sdktestsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (productId:long);Products | where ProductID == productId",
"kqlParameters": "@productId={Query.productId}",
"connection": "KustoConnectionString"
}
]
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample Python code:

```
import azure.functions as func
from Common.product import Product
def main(req: func.HttpRequest, products: str) -> func.HttpResponse:
return func.HttpResponse(
products,
status_code=200,
mimetype="application/json"
)
```


### HTTP trigger, get row by ID from query string

The following example shows a query for the products table by the product name. The function is triggered by an HTTP request that uses a query string to specify the value of a query parameter. That parameter is used to filter the `Product`

records in the specified query.

The following binding data is in the *function.json* file:

```
{
"bindings": [
{
"authLevel": "function",
"name": "req",
"direction": "in",
"type": "httpTrigger",
"methods": [
"get"
],
"route": "getproductsfn"
},
{
"name": "$return",
"type": "http",
"direction": "out"
},
{
"name": "productfnget",
"type": "kusto",
"database": "productsdb",
"direction": "in",
"kqlCommand": "declare query_parameters (name:string);GetProductsByName(name)",
"kqlParameters": "@name={Query.name}",
"connection": "KustoConnectionString"
}
],
"disabled": false
}
```


The [configuration](#configuration) section explains these properties.

The following snippet is sample Python code:

```
import azure.functions as func
def main(req: func.HttpRequest, products: str) -> func.HttpResponse:
return func.HttpResponse(
products,
status_code=200,
mimetype="application/json"
)
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [KustoAttribute](https://github.com/Azure/Webjobs.Extensions.Kusto/blob/main/src/KustoAttribute.cs) attribute to declare the Azure Data Explorer bindings on the function, which has the following properties.

| Attribute property | Description |
|---|---|
| Database | Required. The database against which the query must be executed. |
| Connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| KqlCommand | Required. The `KqlQuery` parameter that must be executed. Can be a KQL query or a KQL function call. |
| KqlParameters | Optional. Parameters that act as predicate variables for `KqlCommand` . For example, "@name={name},@Id={id}", where {name} and {id} are substituted at runtime with actual values acting as predicates. The parameter name and the parameter value can't contain a comma (`,` ) or an equal sign (`=` ). |
| ManagedServiceIdentity | Optional. You can use a managed identity to connect to Azure Data Explorer. To use a system managed identity, use "system." Any other identity names are interpreted as a user managed identity. |

## Annotations

The [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime) uses the [ @KustoInput](https://github.com/Azure/Webjobs.Extensions.Kusto/blob/main/java-library/src/main/java/com/microsoft/azure/functions/kusto/annotation/KustoInput.java) annotation (

`com.microsoft.azure.functions.kusto.annotation.KustoInput`

).| Element | Description |
|---|---|
| name | Required. The name of the variable that represents the query results in function code. |
| database | Required. The database against which the query must be executed. |
| connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| kqlCommand | Required. The `KqlQuery` parameter that must be executed. Can be a KQL query or a KQL function call. |
| kqlParameters | Optional. Parameters that act as predicate variables for `KqlCommand` . For example, "@name={name},@Id={id}", where {name} and {id} are substituted at runtime with actual values acting as predicates. The parameter name and the parameter value can't contain a comma (`,` ) or an equal sign (`=` ). |
| managedServiceIdentity | A managed identity can be used to connect to Azure Data Explorer. To use a system managed identity, use "system." Any other identity names are interpreted as a user managed identity. |

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
| type | Required. Must be set to `kusto` . |
| direction | Required. Must be set to `in` . |
| name | Required. The name of the variable that represents the query results in function code. |
| database | Required. The database against which the query must be executed. |
| connection | Required. The name of the variable that holds the connection string, resolved through environment variables or through function app settings. Defaults to look up on the variable `KustoConnectionString` . At runtime, this variable is looked up against the environment. Documentation on the connection string is at
`"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId` . |
| kqlCommand | Required. The `KqlQuery` parameter that must be executed. Can be a KQL query or a KQL function call. |
| kqlParameters | Optional. Parameters that act as predicate variables for `KqlCommand` . For example, "@name={name},@Id={id}", where {name} and {id} are substituted at runtime with actual values acting as predicates. The parameter name and the parameter value can't contain a comma (`,` ) or an equal sign (`=` ). |
| managedServiceIdentity | A managed identity can be used to connect to Azure Data Explorer. To use a system managed identity, use "system." Any other identity names are interpreted as a user managed identity. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

The attribute's constructor takes the database and the attributes `KQLCommand`

and `KQLParameters`

and the connection setting name. The KQL command can be a KQL statement or a KQL function. The connection string setting name corresponds to the application setting (in `local.settings.json`

for local development) that contains the [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For example: `"KustoConnectionString": "Data Source=https://your_cluster.kusto.windows.net;Database=your_Database;Fed=True;AppClientId=your_AppId;AppKey=your_AppKey;Authority Id=your_TenantId`

. Queries executed by the input binding are parameterized. The values provided in the KQL parameters are used at runtime.

Important

For optimal security, your function app should use managed identities when connecting to Azure Data Explorer instead of using a connection string, which contains keys. For more information, see [Kusto connection strings](/en-us/azure/data-explorer/kusto/api/connection-strings/kusto). For mananaged identity-based connections, you must set the `managedServiceIdentity`

property in the binding definition.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-kafka-output -->

# Apache Kafka output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The output binding enables an Azure Functions app to send messages to a Kafka topic.

Important

Kafka bindings are available for Functions on the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium Plan](functions-premium-plan), and [Dedicated (App Service) plan](dedicated-plan). They are only supported on version 4.x of the Functions runtime.

## Example

How you use the binding depends on the C# modality in your function app. You can use one of the following modalities:

A compiled C# function that uses an [isolated worker process class library](dotnet-isolated-process-guide) that runs in a process that's separate from the runtime.

The attributes you use depend on the specific event provider.

The following example uses a custom return type named `MultipleOutputType`

, which consists of an HTTP response and a Kafka output.

```
[Function("KafkaOutput")]
public static MultipleOutputType Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
string message = req.FunctionContext
.BindingContext
.BindingData["message"]
.ToString();
var response = req.CreateResponse(HttpStatusCode.OK);
return new MultipleOutputType()
{
Kevent = message,
HttpResponse = response
};
}
```


In the `MultipleOutputType`

class, `Kevent`

is the output binding variable for the Kafka binding.

```
public class MultipleOutputType
{
[KafkaOutput("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain
)]
public string Kevent { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


To send a batch of events, pass a string array to the output type, as shown in the following example:

```
[Function("KafkaOutputMany")]
public static MultipleOutputTypeForBatch Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
var response = req.CreateResponse(HttpStatusCode.OK);
string[] messages = new string[2];
messages[0] = "one";
messages[1] = "two";
return new MultipleOutputTypeForBatch()
{
Kevents = messages,
HttpResponse = response
};
}
```


The string array is defined as the `Kevents`

property on the class, and the output binding is defined on this property:

```
public class MultipleOutputTypeForBatch
{
[KafkaOutput("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain
)]
public string[] Kevents { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The following function adds headers to the Kafka output data:

```
[Function("KafkaOutputWithHeaders")]
public static MultipleOutputType Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
string message = req.FunctionContext
.BindingContext
.BindingData["message"]
.ToString();
string kevent = "{ \"Offset\":364,\"Partition\":0,\"Topic\":\"kafkaeventhubtest1\",\"Timestamp\":\"2022-04-09T03:20:06.591Z\", \"Value\": \"" + message + "\", \"Headers\": [{ \"Key\": \"test\", \"Value\": \"dotnet-isolated\" }] }";
var response = req.CreateResponse(HttpStatusCode.OK);
return new MultipleOutputType()
{
Kevent = kevent,
HttpResponse = response
};
}
```


For a complete set of working .NET examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/dotnet-isolated/confluent).

The usage of the output binding depends on your version of the Node.js programming model.

In the Node.js v4 model, you define your output binding directly in your function code. For more information, see the [Azure Functions Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4).

In these examples, the event providers are either Confluent or Azure Event Hubs. These examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const queryName = request.query.get("name");
const parsedbody = JSON.parse(body);
const name = queryName || parsedbody.name || "world";
context.extraOutputs.set(kafkaOutput, `Hello, ${parsedbody.name}!`);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


To send events in a batch, send an array of messages, as shown in these examples:

```
const { app, output } = require("@azure/functions");
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
async function kafkaOutputManyWithHttp(request, context) {
context.log(`Http function processed request for url "${request.url}"`);
const queryName = request.query.get("name");
const body = await request.text();
const parsedbody = body ? JSON.parse(body) : {};
parsedbody.name = parsedbody.name || "world";
const name = queryName || parsedbody.name;
context.extraOutputs.set(kafkaOutput, `Message one. Hello, ${name}!`);
context.extraOutputs.set(kafkaOutput, `Message two. Hello, ${name}!`);
return {
body: `Messages sent to kafka.`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputManyWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputManyWithHttp,
});
```


These examples show how to send an event message with headers to a Kafka topic:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const parsedbody = JSON.parse(body);
// assuming body is of the format { "key": "key", "value": {JSON object} }
context.extraOutputs.set(
kafkaOutput,
`{ "Offset":364,"Partition":0,"Topic":"test-topic","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "${JSON.stringify(
parsedbody.value
).replace(/"/g, '\\"')}", "Key":"${
parsedbody.key
}", "Headers": [{ "Key": "language", "Value": "javascript" }] }`
);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


For a complete set of working JavaScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/javascript-v4/src/functions).

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const queryName = request.query.get("name");
const parsedbody = JSON.parse(body);
const name = queryName || parsedbody.name || "world";
context.extraOutputs.set(kafkaOutput, `Hello, ${parsedbody.name}!`);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


To send events in a batch, send an array of messages, as shown in these examples:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputManyWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const queryName = request.query.get("name");
const body = await request.text();
const parsedbody = body ? JSON.parse(body) : {};
parsedbody.name = parsedbody.name || "world";
const name = queryName || parsedbody.name;
context.extraOutputs.set(kafkaOutput, `Message one. Hello, ${name}!`);
context.extraOutputs.set(kafkaOutput, `Message two. Hello, ${name}!`);
return {
body: `Messages sent to kafka.`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputManyWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputManyWithHttp,
});
```


These examples show how to send an event message with headers to a Kafka topic:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const parsedbody = JSON.parse(body);
// assuming body is of the format { "key": "key", "value": {JSON object} }
context.extraOutputs.set(
kafkaOutput,
`{ "Offset":364,"Partition":0,"Topic":"test-topic","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "${JSON.stringify(
parsedbody.value
).replace(/"/g, '\\"')}", "Key":"${
parsedbody.key
}", "Headers": [{ "Key": "language", "Value": "typescript" }] }`
);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


For a complete set of working TypeScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/typescript-v4/src/functions).

The specific properties of the function.json file depend on your event provider, which in these examples are either Confluent or Azure Event Hubs. The following examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

The following function.json defines the trigger for the specific provider in these examples:

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
]
},
{
"type": "kafka",
"name": "outputMessage",
"brokerList": "BrokerList",
"topic": "topic",
"username" : "%ConfluentCloudUserName%",
"password" : "%ConfluentCloudPassword%",
"protocol": "SASLSSL",
"authenticationMode": "PLAIN",
"direction": "out"
},
{
"type": "http",
"direction": "out",
"name": "Response"
}
]
}
```


The following code sends a message to the topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
$message
Push-OutputBinding -Name outputMessage -Value ($message)
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
})
```


The following code sends multiple messages as an array to the same topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
$message = @("one", "two")
Push-OutputBinding -Name outputMessage -Value ($message)
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
})
```


The following example shows how to send an event message with headers to the same Kafka topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
if (-not $message) {
$message = $Request.Body.Message
}
$kevent = @{
Offset = 364
Partition = 0
Topic = "kafkaeventhubtest1"
Timestamp = "2022-04-09T03:20:06.591Z"
Value = $message
Headers= @(@{
Key= "test"
Value= "powershell"
}
)
}
Push-OutputBinding -Name Message -Value $kevent
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = 'ok'
})
```


For a complete set of working PowerShell examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/powershell/).

The usage of the output binding depends on your version of the Python programming model.

In the Python v2 model, you define your output binding directly in your function code using decorators. For more information, see the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

These examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

```
input_msg = req.params.get('message')
outputMessage.set(input_msg)
return 'OK'
@KafkaOutput.function_name(name="KafkaOutputMany")
@KafkaOutput.route(route="kafka_output_many")
@KafkaOutput.kafka_output(arg_name="outputMessage", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain", data_type="string")
def kafka_output_many(req: func.HttpRequest, outputMessage: func.Out[str] ) -> func.HttpResponse:
outputMessage.set(json.dumps(['one', 'two']))
return 'OK'
```


To send events in a batch, send an array of messages, as shown in these examples:

```
@KafkaOutput.route(route="kafka_output_with_headers")
@KafkaOutput.kafka_output(arg_name="out", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain")
def kafka_output_with_headers(req: func.HttpRequest, out: func.Out[str]) -> func.HttpResponse:
message = req.params.get('message')
kevent = { "Offset":0,"Partition":0,"Topic":"dummy","Timestamp":"2022-04-09T03:20:06.591Z", "Value": message, "Headers": [{ "Key": "test", "Value": "python" }] }
out.set(json.dumps(kevent))
return 'OK'
@KafkaOutput.function_name(name="KafkaOutputManyWithHeaders")
@KafkaOutput.route(route="kafka_output_many_with_headers")
@KafkaOutput.kafka_output(arg_name="out", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain")
def kafka_output_many_with_headers(req: func.HttpRequest, out: func.Out[str]) -> func.HttpResponse:
kevent = [{ "Offset": 364, "Partition":0,"Topic":"kafkaeventhubtest1","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "one", "Headers": [{ "Key": "test", "Value": "python" }] },
```


These examples show how to send an event message with headers to a Kafka topic:

For a complete set of working Python examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/python-v2/).

The annotations you use to configure the output binding depend on the specific event provider.

The following function sends a message to the Kafka topic.

```
@FunctionName("KafkaOutput")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<String> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("message");
String message = request.getBody().orElse(query);
context.getLogger().info("Message:" + message);
output.setValue(message);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
```


The following example shows how to send multiple messages to a Kafka topic.

```
@FunctionName("KafkaOutputMany")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<String[]> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String[] messages = new String[2];
messages[0] = "one";
messages[1] = "two";
output.setValue(messages);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
}
```


In this example, the output binding parameter is changed to string array.

The last example uses these `KafkaEntity`

and `KafkaHeader`

classes:

```
public class KafkaEntity {
public int Offset;
public int Partition;
public String Timestamp;
public String Topic;
public String Value;
public KafkaHeaders Headers[];
public KafkaEntity(int Offset, int Partition, String Topic, String Timestamp, String Value,KafkaHeaders[] headers) {
this.Offset = Offset;
this.Partition = Partition;
this.Topic = Topic;
this.Timestamp = Timestamp;
this.Value = Value;
this.Headers = headers;
}
```


```
public class KafkaHeaders{
public String Key;
public String Value;
public KafkaHeaders(String key, String value) {
this.Key = key;
this.Value = value;
}
```


The following example function sends a message with headers to a Kafka topic.

```
@FunctionName("KafkaOutputWithHeaders")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<KafkaEntity> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("message");
String message = request.getBody().orElse(query);
KafkaHeaders[] headers = new KafkaHeaders[1];
headers[0] = new KafkaHeaders("test", "java");
KafkaEntity kevent = new KafkaEntity(364, 0, "topic", "2022-04-09T03:20:06.591Z", message, headers);
output.setValue(kevent);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
}
```


For a complete set of working Java examples for Confluent, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/java/confluent/src/main/java/com/contoso/kafka).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `Kafka`

attribute to define the function trigger.

The following table explains the properties you can set by using this attribute:

| Parameter | Description |
|---|---|
BrokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**Topic****AvroSchema****KeyAvroSchema****KeyDataType**`KeyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**MaxMessageBytes**`1`

.**BatchSize**`10000`

.**EnableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

**MessageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**RequestTimeoutMs**`5000`

.**MaxRetries**`2`

. Retrying may cause reordering, unless `EnableIdempotence`

is set to `true`

.**AuthenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

, and `OAuthBearer`

.**Username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**SslCaLocation****SslCertificateLocation****SslKeyLocation****SslKeyPassword****SslCertificatePEM**[Connections](#connections)for more information.**SslKeyPEM**[Connections](#connections)for more information.**SslCaPEM**[Connections](#connections)for more information.**SslCertificateandKeyPEM**[Connections](#connections)for more information.**SchemaRegistryUrl**[Connections](#connections)for more information.**SchemaRegistryUsername**[Connections](#connections)for more information.**SchemaRegistryPassword**[Connections](#connections)for more information.**OAuthBearerMethod**`oidc`

and `default`

.**OAuthBearerClientId**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**OAuthBearerClientSecret**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**OAuthBearerScope****OAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.**OAuthBearerExtensions**`oidc`

method is used. For example: `supportFeatureX=true,organizationId=sales-emea`

.## Annotations

The `KafkaOutput`

annotation enables you to create a function that writes to a specific topic. Supported options include the following elements:

| Element | Description |
|---|---|
name |
The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**avroSchema**[Currently not supported for Java](https://github.com/Azure/azure-functions-java-library/issues/198).)**maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

.**authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

function.json property |
Description |
|---|---|
type |
Set to `kafka` . |
direction |
Set to `out` . |
name |
The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****avroSchema****keyAvroSchema****keyDataType**`keyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

.**authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****sslCertificatePEM**[Connections](#connections)for more information.**sslKeyPEM**[Connections](#connections)for more information.**sslCaPEM**[Connections](#connections)for more information.**sslCertificateandKeyPEM**[Connections](#connections)for more information.**schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.**oAuthBearerMethod**`oidc`

and `default`

.**oAuthBearerClientId**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**oAuthBearerClientSecret**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**oAuthBearerScope****oAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file. Python uses snake_case naming conventions for configuration properties.

function.json property |
Description |
|---|---|
type |
Set to `kafka` . |
direction |
Set to `out` . |
name |
The name of the variable that represents the brokered data in function code. |
broker_list |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****avroSchema****maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

.**authentication_mode**`NOTSET`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NOTSET`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****schema_registry_url**[Connections](#connections)for more information.**schema_registry_username**[Connections](#connections)for more information.**schema_registry_password**[Connections](#connections)for more information.**o_auth_bearer_method**`oidc`

and `default`

.**o_auth_bearer_client_id**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**o_auth_bearer_client_secret**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**o_auth_bearer_scope****o_auth_bearer_token_endpoint_url**`oidc`

method is used. See [Connections](#connections)for more information.Note

Certificate PEM-related properties and Avro key-related properties aren't yet available in the Python library.

## Usage

The offset, partition, and timestamp for the event are generated at runtime. You can set only the value and headers inside the function. You set the topic in the function.json file.

Make sure you have access to the Kafka topic where you want to write. You configure the binding with access and connection credentials to the Kafka topic.

In a Premium plan, you must enable runtime scale monitoring for the Kafka output to scale out to multiple instances. To learn more, see [Enable runtime scaling](functions-bindings-kafka#enable-runtime-scaling).

For a complete set of supported host.json settings for the Kafka trigger, see [host.json settings](functions-bindings-kafka#hostjson-settings).

## Connections

Store all connection information required by your triggers and bindings in application settings, not in the binding definitions in your code. This guidance applies to credentials, which you should never store in your code.

Important

Credential settings must reference an [application setting](functions-how-to-use-azure-function-app-settings#settings). Don't hard-code credentials in your code or configuration files. When running locally, use the [local.settings.json file](functions-develop-local#local-settings-file) for your credentials, and don't publish the local.settings.json file.

When connecting to a managed Kafka cluster provided by [Confluent in Azure](https://www.confluent.io/azure/), you can use one of the following authentication methods.

Note

When using the Flex Consumption plan, file location-based certificate authentication properties (`SslCaLocation`

, `SslCertificateLocation`

, `SslKeyLocation`

) aren't supported. Instead, use the PEM-based certificate properties (`SslCaPEM`

, `SslCertificatePEM`

, `SslKeyPEM`

, `SslCertificateandKeyPEM`

) or store certificates in Azure Key Vault.

#### Schema Registry

To make use of schema registry provided by Confluent in Kafka Extension, set the following credentials:

| Setting | Recommended Value | Description |
|---|---|---|
SchemaRegistryUrl |
`SchemaRegistryUrl` |
URL of the schema registry service used for schema management. Usually of the format `https://psrc-xyz.us-east-2.aws.confluent.cloud` |
SchemaRegistryUsername |
`CONFLUENT_API_KEY` |
Username for basic auth on schema registry (if required). |
SchemaRegistryPassword |
`CONFLUENT_API_SECRET` |
Password for basic auth on schema registry (if required). |

#### Username/Password authentication

While using this form of authentication, make sure that `Protocol`

is set to either `SaslPlaintext`

or `SaslSsl`

, `AuthenticationMode`

is set to `Plain`

, `ScramSha256`

or `ScramSha512`

and, if the CA cert being used is different from the default ISRG Root X1 cert, make sure to update `SslCaLocation`

or `SslCaPEM`

.

| Setting | Recommended value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
Username |
`ConfluentCloudUsername` |
App setting named `ConfluentCloudUsername` contains the API access key from the Confluent Cloud web site. |
Password |
`ConfluentCloudPassword` |
App setting named `ConfluentCloudPassword` contains the API secret obtained from the Confluent Cloud web site. |
SslCaPEM |
`SSLCaPemCertificate` |
App setting named `SSLCaPemCertificate` that contains the CA certificate as a string in PEM format. The value should follow the standard format, for example: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----` . |

#### SSL authentication

Ensure that `Protocol`

is set to `SSL`

.

| Setting | Recommended Value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
SslCaPEM |
`SslCaCertificatePem` |
App setting named `SslCaCertificatePem` that contains PEM value of the CA certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslCertificatePEM |
`SslClientCertificatePem` |
App setting named `SslClientCertificatePem` that contains PEM value of the client certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslKeyPEM |
`SslClientKeyPem` |
App setting named `SslClientKeyPem` that contains PEM value of the client private key as a string. The value should follow the standard format: `-----BEGIN PRIVATE KEY-----\nMII...JQ==\n-----END PRIVATE KEY-----` |
SslCertificateandKeyPEM |
`SslClientCertificateAndKeyPem` |
App setting named `SslClientCertificateAndKeyPem` that contains PEM value of the client certificate and client private key concatenated as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----\n-----BEGIN PRIVATE KEY-----\nMIIE....BM=\n-----END PRIVATE KEY-----` |
SslKeyPassword |
`SslClientKeyPassword` |
App setting named `SslClientKeyPassword` that contains the password for the private key (if any). |

#### OAuth authentication

When using OAuth authentication, configure the OAuth-related properties in your binding definitions.

The string values you use for these settings must be present as [application settings in Azure](functions-how-to-use-azure-function-app-settings#settings) or in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file) during local development.

You should also set the `Protocol`

and `AuthenticationMode`

in your binding definitions.

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-recover-storage-account_functions-bindings-signalr-service_functions_e0b6a3.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-recover-storage-account_functions-bindings-signalr-service.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-recover-storage-account.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-recover-storage-account -->

# Troubleshoot error: "Azure Functions Runtime is unreachable"

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article helps you troubleshoot the following error string that appears in the Azure portal:

"Error: Azure Functions Runtime is unreachable. Click here for details on storage configuration."


This issue occurs when the Functions runtime can't start. The most common reason for this is that the function app lost access to its storage account. For more information, see [Storage account requirements](storage-considerations#storage-account-requirements).

The rest of this article helps you troubleshoot specific causes of this error, including how to identify and resolve each case.

## Storage account was deleted

Every function app requires a storage account that is used by the Functions host to operate. If that default host storage account is deleted, your function app won't run.

Start by looking up your storage account name in your application settings. Either `AzureWebJobsStorage`

or `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

contains the name of your storage account as part of a connection string. For more information, see [App settings reference for Azure Functions](functions-app-settings#azurewebjobsstorage).

Search for your storage account in the Azure portal to see whether it still exists. If it has been deleted, re-create the storage account and replace your storage connection strings. Your function code is lost, and you need to redeploy it.

## Storage account application settings were deleted

In the preceding step, if you can't find a storage account connection string, it was likely deleted or overwritten. Deleting application settings most commonly happens when you're using deployment slots or Azure Resource Manager scripts to set application settings.

### Required application settings

- Required:
- Required for Elastic Premium and Consumption plan functions:

For more information, see [App settings reference for Azure Functions](functions-app-settings).

### Guidance

- Don't check
**slot setting**for any of these settings. If you swap deployment slots, the function app breaks. - Don't modify these settings as part of automated deployments.
- These settings must be provided and valid at creation time. An automated deployment that doesn't contain these settings results in a function app that doesn't run, even if the settings are added later.

## Storage account credentials are invalid

The previously discussed storage account connection strings must be updated if you regenerate storage keys. For more information about storage key management, see [Create an Azure Storage account](../storage/common/storage-account-create).

## Storage account is inaccessible

Your function app must be able to access the storage account. Common issues that block a function app's access to a storage account are:

The function app is deployed to your App Service Environment (ASE) without the correct network rules to allow traffic to and from the storage account.

The storage account firewall is enabled and not configured to allow traffic to and from functions. For more information, see

[Configure Azure Storage firewalls and virtual networks](../storage/common/storage-network-security?toc=/azure/storage/files/toc.json).Verify that the

`allowSharedKeyAccess`

setting is set to`true`

, which is its default value. For more information, see[Prevent Shared Key authorization for an Azure Storage account](../storage/common/shared-key-authorization-prevent?tabs=portal#verify-that-shared-key-access-is-not-allowed).

## Daily execution quota is full

If you have a daily execution quota configured, your function app is temporarily disabled, which causes many of the portal controls to become unavailable.

To verify the quota in the [Azure portal](https://portal.azure.com), select **Platform Features** > **Function App Settings** in your function app. If you're over the **Daily Usage Quota** that you set, the following message is displayed:

"The Function App has reached daily usage quota and has been stopped until the next 24 hours time frame."


To resolve this issue, remove or increase the daily quota, and then restart your app. Otherwise, the execution of your app is blocked until the next day.

## App is behind a firewall

Your function app might be unreachable for either of the following reasons:

Your function app is hosted in an

[internally load balanced App Service Environment](../app-service/environment/create-ilb-ase)and it's configured to block inbound internet traffic.Your function app has

[inbound IP restrictions](functions-networking-options#inbound-networking-features)that are configured to block internet access.

The Azure portal makes calls directly to the running app to fetch the list of functions, and it makes HTTP calls to the Kudu endpoint. Platform-level settings under the **Platform Features** tab are still available.

To verify your ASE configuration:

- Go to the network security group (NSG) of the subnet where the ASE resides.
- Validate the inbound rules to allow traffic that's coming from the public IP of the computer where you're accessing the application.

You can also use the portal from a computer that's connected to the virtual network that's running your app or to a virtual machine that's running in your virtual network.

For more information about inbound rule configuration, see [Networking considerations for an App Service Environment](../app-service/environment/network-info#network-security-groups).

## Container errors on Linux

For function apps that run on Linux in a container, the `Azure Functions runtime is unreachable`

error can occur as a result of problems with the container. Use the following procedure to review the container logs for errors:

Navigate to the Kudu endpoint for the function app, which is located at

`https://<FUNCTION_APP>.scm.azurewebsites.net`

, where`<FUNCTION_APP>`

is the name of your app.Download the Docker logs .zip file and review the contents on your local computer.

Check for any logged errors that indicate that the container is unable to start successfully.


## Container image unavailable

Errors can occur when the container image being referenced is unavailable or fails to start correctly. Check for any logged errors that indicate that the container is unable to start successfully.

You need to correct any errors that prevent the container from starting for the function app run correctly.

When the container image can't be found, you see a `manifest unknown`

error in the Docker logs. In this case, you can use the Azure CLI commands documented at [How to target Azure Functions runtime versions](set-runtime-version?tabs=azurecli#manual-version-updates-on-linux) to change the container image being referenced. If you've deployed a [custom container image](functions-how-to-custom-container), you need to fix the image and redeploy the updated version to the referenced registry.

## App container has conflicting ports

Your function app might be in an unresponsive state due to conflicting port assignment upon startup. This situation can happen in the following cases:

- Your container has separate services running where one or more services are tying to bind to the same port as the function app.
- You added an Azure Hybrid Connection that shares the same port value as the function app.

By default, the container in which your function app runs uses port `:80`

. When other services in the same container are also trying to using port `:80`

, the function app can fail to start. If your logs show port conflicts, change the default ports.

## Host ID collision

Starting with version 3.x of the Functions runtime, [host ID collision](storage-considerations#host-id-considerations) are detected and logged as a warning. In version 4.x, an error is logged and the host is stopped. If the runtime can't start for your function app, [review the logs](analyze-telemetry-data). If there's a warning or an error about host ID collisions, follow the mitigation steps in [Host ID considerations](storage-considerations#host-id-considerations).

## Read-only app settings

Changing any *read-only* [App Service application settings](../app-service/reference-app-settings#app-environment) can put your function app into an unreachable state.

## ASP.NET authentication overrides

*Applies only to C# apps running in-process with the Functions host.*

Configuring ASP.NET authentication in a Functions startup class can override services that are required for the Azure portal to communicate with the host. This includes, but isn't limited to, any calls to `AddAuthentication()`

. If the host's authentication services are overridden and the portal can't communicate with the host, it considers the app unreachable. This issue might result in errors such as: `No authentication handler is registered for the scheme 'ArmToken'.`


## Next steps

Learn about monitoring your function apps:


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-signalr-service.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service -->

# SignalR Service bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to authenticate and send real-time messages to clients connected to [Azure SignalR Service](https://azure.microsoft.com/services/signalr-service/) by using SignalR Service bindings in Azure Functions. Azure Functions runtime version 2.x and higher supports input and output bindings for SignalR Service.

| Action | Type |
|---|---|
| Handle messages from SignalR Service |
|

[Input binding](functions-bindings-signalr-service-input)[Output binding](functions-bindings-signalr-service-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.SignalRService/).

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

## Add dependency

To use the SignalR Service annotations in Java functions, you need to add a dependency to the *azure-functions-java-library-signalr* artifact (version 1.0 or higher) to your *pom.xml* file.

```
<dependency>
<groupId>com.microsoft.azure.functions</groupId>
<artifactId>azure-functions-java-library-signalr</artifactId>
<version>1.0.0</version>
</dependency>
```


## Connections

You can use [connection string](#connection-string) or [Microsoft Entra identity](#identity-based-connections) to connect to Azure SignalR Service.

### Connection string

For instructions on how to retrieve the connection string for your Azure SignalR Service, see [Connection strings in Azure SignalR Service](../azure-signalr/concept-connection-string#how-to-get-connection-strings)

This connection string should be stored in an application setting with a name `AzureSignalRConnectionString`

. You can customize the application setting name with the `connectionStringSetting`

property of the binding configuration.

### Identity-based connections

If you're using version 1.7.0 or higher, instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis).

First of all, you should make sure your Microsoft Entra identity has role [SignalR Service Owner](../role-based-access-control/built-in-roles#signalr-service-owner).

Then you would define settings with a common prefix `AzureSignalRConnectionString`

. You can customize prefix name with the `connectionStringSetting`

property of the binding configuration.

In this mode, the settings include following items:

| Property | Environment variable template | Description | Required | Example value |
|---|---|---|---|---|
| Service URI | `AzureSignalRConnectionString__serviceUri` |
The URI of your service endpoint. When you only configure "Service URI", the extensions would attempt to use
|

`AzureSignalRConnectionString__credential`

`managedidentity`

if your deployed Azure Function intends to use managed identity authentication. This value is only valid when a managed identity is available in the hosting environment.`AzureSignalRConnectionString__clientId`

`credential`

is set to `managedidentity`

, this property can be set to specify the user-assigned identity to be used when obtaining a token. The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a Resource ID and a client ID. If not specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.`AzureSignalRConnectionString__managedIdentityResourceId`

`credential`

is set to `managedidentity`

, this property can be set to specify the resource Identifier to be used when obtaining a token. The property accepts a resource identifier corresponding to the resource ID of the user-defined managed identity. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.Note

When using `local.settings.json`

file at local, [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp), or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for identity-based connections, replace `__`

with `:`

in the setting name to ensure names are resolved correctly.

For example, `AzureSignalRConnectionString:serviceUri`

.

#### Multiple endpoints setting

You can also configure multiple endpoints and specify identity settings per endpoint.

In this case, prefix your settings with `Azure__SignalR__Endpoints__{endpointName}`

. The `{endpointName}`

is an arbitrary name assigned by you to associate a group of settings to a service endpoint. The prefix `Azure__SignalR__Endpoints__{endpointName}`

can't be customized by `connectionStringSetting`

property.

| Property | Environment variable template | Description | Required | Example value |
|---|---|---|---|---|
| Service URI | `Azure__SignalR__Endpoints__{endpointName}__serviceUri` |
The URI your service endpoint. When you only configure "Service URI", the extensions would attempt to use
|

`Azure__SignalR__Endpoints__{endpointName}__type`

`Primary`

. Valid values are `Primary`

and `Secondary`

, case-insensitive.`Secondary`

`Azure__SignalR__Endpoints__{endpointName}__credential`

`managedidentity`

if your deployed Azure Function intends to use managed identity authentication. This value is only valid when a managed identity is available in the hosting environment.`Azure__SignalR__Endpoints__{endpointName}__clientId`

`credential`

is set to `managedidentity`

, this property can be set to specify the user-assigned identity to be used when obtaining a token. The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a Resource ID and a client ID. If not specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.`Azure__SignalR__Endpoints__{endpointName}__managedIdentityResourceId`

`credential`

is set to `managedidentity`

, this property can be set to specify the resource Identifier to be used when obtaining a token. The property accepts a resource identifier corresponding to the resource ID of the user-defined managed identity. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used. This property is used differently in [local development scenarios](functions-reference#local-development-with-identity-based-connections), when`credential`

shouldn't be set.For more information about multiple endpoints, see [Scale SignalR Service with multiple instances](../azure-signalr/signalr-howto-scale-multi-instances?pivots=serverless-mode#for-signalr-functions-extensions)

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

## Next steps

For details on how to configure and use SignalR Service and Azure Functions together, refer to [Azure Functions development and configuration with Azure SignalR Service](../azure-signalr/signalr-concept-serverless-development-config).


---

<!-- DOCUMENTO FUSIONADO: functions-deploy-container.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-deploy-container -->

# Create your first containerized Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you create a function app running in a Linux container and deploy it to Azure Functions.

Deploying your function code to Azure Functions in a container requires [Premium plan](functions-premium-plan) or [Dedicated (App Service) plan](dedicated-plan) hosting. Completing this article incurs costs of a few US dollars in your Azure account, which you can minimize by [cleaning-up resources](#clean-up-resources) when you're done.

Tip

When you need to run your event-driven functions in Azure in the same environment as other microservices, APIs, websites, workflows, or any container hosted programs, consider instead hosting your containerized function apps in Azure Container Apps. Functions provides integrated support for developing, deploying, and managing containerized function apps on Container Apps. For more information, see [Azure Container Apps hosting of Azure Functions](../container-apps/functions-overview).

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


## Create supporting Azure resources for your function

Before you can deploy your container to Azure, you need to create three resources:

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A
[Storage account](../storage/common/storage-account-create), which is used to maintain state and other information about your functions. - A function app, which provides the environment for executing your function code. A function app maps to your local function project and lets you group functions as a logical unit for easier management, deployment, and sharing of resources.

Important

This article currently shows how to connect to both the Azure Storage account and your container registry by using connection strings and other shared secret credentials. For the best security, you should instead use only a managed identity-based connection to both your storage account and to Azure Container Registry using Microsoft Entra authentication. For more information, see the [Functions developer guide](functions-reference#connections).

Use the following commands to create these items. Both Azure CLI and PowerShell are supported. To create your Azure resources using Azure PowerShell, you also need the [Az PowerShell module](/en-us/powershell/azure/install-az-ps), version 5.9.0 or later.

If you haven't done already, sign in to Azure.

`az login`

The

command signs you into your Azure account.`az login`

Create a resource group named

`AzureFunctionsContainers-rg`

in your chosen region.`az group create --name AzureFunctionsContainers-rg --location <REGION>`

The

command creates a resource group. In the above command, replace`az group create`

`<REGION>`

with a region near you, using an available region code returned from the[az account list-locations](/en-us/cli/azure/account#az-account-list-locations)command.Create a general-purpose storage account in your resource group and region.

`az storage account create --name <STORAGE_NAME> --location <REGION> --resource-group AzureFunctionsContainers-rg --sku Standard_LRS`

The

command creates the storage account.`az storage account create`

In the previous example, replace

`<STORAGE_NAME>`

with a name that is appropriate to you and unique in Azure Storage. Storage names must contain 3 to 24 characters numbers and lowercase letters only.`Standard_LRS`

specifies a general-purpose account[supported by Functions](storage-considerations#storage-account-requirements).Use the command to create a Premium plan for Azure Functions named

`myPremiumPlan`

in the**Elastic Premium 1**pricing tier (`--sku EP1`

), in your`<REGION>`

, and in a Linux container (`--is-linux`

).`az functionapp plan create --resource-group AzureFunctionsContainers-rg --name myPremiumPlan --location <REGION> --number-of-workers 1 --sku EP1 --is-linux`

We use the Premium plan here, which can scale as needed. For more information about hosting, see

[Azure Functions hosting plans comparison](functions-scale). For more information on how to calculate costs, see the[Functions pricing page](https://azure.microsoft.com/pricing/details/functions/).The command also creates an associated Azure Application Insights instance in the same resource group, with which you can monitor your function app and view logs. For more information, see

[Monitor Azure Functions](functions-monitoring). The instance incurs no costs until you activate it.

## Create and configure a function app on Azure with the image

A function app on Azure manages the execution of your functions in your Azure Functions hosting plan. In this section, you use the Azure resources from the previous section to create a function app from an image in a container registry and configure it with a connection string to Azure Storage.

Create a function app using the following command, depending on your container registry:

`az functionapp create --name <APP_NAME> --storage-account <STORAGE_NAME> --resource-group AzureFunctionsContainers-rg --plan myPremiumPlan --image <LOGIN_SERVER>/azurefunctionsimage:v1.0.0 --registry-username <USERNAME> --registry-password <SECURE_PASSWORD>`

In this example, replace

`<STORAGE_NAME>`

with the name you used in the previous section for the storage account. Also, replace`<APP_NAME>`

with a globally unique name appropriate to you and`<DOCKER_ID>`

or`<LOGIN_SERVER>`

with your Docker Hub account ID or Container Registry server, respectively. When you're deploying from a custom container registry, the image name indicates the URL of the registry.When you first create the function app, it pulls the initial image from your Docker Hub. You can also

[Enable continuous deployment](functions-how-to-custom-container#enable-continuous-deployment-to-azure)to Azure from your container registry.Tip

You can use the

in the`DisableColor`

setting*host.json*file to prevent ANSI control characters from being written to the container logs.Use the following command to get the connection string for the storage account you created:

`az storage account show-connection-string --resource-group AzureFunctionsContainers-rg --name <STORAGE_NAME> --query connectionString --output tsv`

The connection string for the storage account is returned by using the

command.`az storage account show-connection-string`

Important

This article currently shows how to connect to the default storage account by using a connection string. For the best security, you should instead create a managed identity-based connection to Azure Storage using Microsoft Entra authentication. For more information, see the

[Functions developer guide](functions-reference#connections).Replace

`<STORAGE_NAME>`

with the name of the storage account you created earlier.Use the following command to add the setting to the function app:

`az functionapp config appsettings set --name <APP_NAME> --resource-group AzureFunctionsContainers-rg --settings AzureWebJobsStorage=<CONNECTION_STRING>`

The

command creates the setting.`az functionapp config appsettings set`

In this command, replace

`<APP_NAME>`

with the name of your function app and`<CONNECTION_STRING>`

with the connection string from the previous step. The connection should be a long encoded string that begins with`DefaultEndpointProtocol=`

.The function can now use this connection string to access the storage account.


## Verify your functions on Azure

With the image deployed to your function app in Azure, you can now invoke the function through HTTP requests.

Run the following

command to get the URL of your new function:`az functionapp function show`

`az functionapp function show --resource-group AzureFunctionsContainers-rg --name <APP_NAME> --function-name HttpExample --query invokeUrlTemplate`

Replace

`<APP_NAME>`

with the name of your function app.

- Use the URL you just obtained to call the
`HttpExample`

function endpoint, appending the query string`?name=Functions`

.

- Use the URL you just obtained to call the
`HttpExample`

function endpoint.

When you navigate to this URL, the browser must display similar output as when you ran the function locally.

## Clean up resources

If you want to continue working with Azure Function using the resources you created in this article, you can leave all those resources in place. Because you created a Premium Plan for Azure Functions, you'll incur one or two USD per day in ongoing costs.

To avoid ongoing costs, delete the `AzureFunctionsContainers-rg`

resource group to clean up all the resources in that group:

```
az group delete --name AzureFunctionsContainers-rg
```


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-kafka-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-kafka-output -->

# Apache Kafka output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The output binding enables an Azure Functions app to send messages to a Kafka topic.

Important

Kafka bindings are available for Functions on the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium Plan](functions-premium-plan), and [Dedicated (App Service) plan](dedicated-plan). They are only supported on version 4.x of the Functions runtime.

## Example

How you use the binding depends on the C# modality in your function app. You can use one of the following modalities:

A compiled C# function that uses an [isolated worker process class library](dotnet-isolated-process-guide) that runs in a process that's separate from the runtime.

The attributes you use depend on the specific event provider.

The following example uses a custom return type named `MultipleOutputType`

, which consists of an HTTP response and a Kafka output.

```
[Function("KafkaOutput")]
public static MultipleOutputType Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
string message = req.FunctionContext
.BindingContext
.BindingData["message"]
.ToString();
var response = req.CreateResponse(HttpStatusCode.OK);
return new MultipleOutputType()
{
Kevent = message,
HttpResponse = response
};
}
```


In the `MultipleOutputType`

class, `Kevent`

is the output binding variable for the Kafka binding.

```
public class MultipleOutputType
{
[KafkaOutput("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain
)]
public string Kevent { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


To send a batch of events, pass a string array to the output type, as shown in the following example:

```
[Function("KafkaOutputMany")]
public static MultipleOutputTypeForBatch Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
var response = req.CreateResponse(HttpStatusCode.OK);
string[] messages = new string[2];
messages[0] = "one";
messages[1] = "two";
return new MultipleOutputTypeForBatch()
{
Kevents = messages,
HttpResponse = response
};
}
```


The string array is defined as the `Kevents`

property on the class, and the output binding is defined on this property:

```
public class MultipleOutputTypeForBatch
{
[KafkaOutput("BrokerList",
"topic",
Username = "ConfluentCloudUserName",
Password = "ConfluentCloudPassword",
Protocol = BrokerProtocol.SaslSsl,
AuthenticationMode = BrokerAuthenticationMode.Plain
)]
public string[] Kevents { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The following function adds headers to the Kafka output data:

```
[Function("KafkaOutputWithHeaders")]
public static MultipleOutputType Output(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", Route = null)] HttpRequestData req,
FunctionContext executionContext)
{
var log = executionContext.GetLogger("HttpFunction");
log.LogInformation("C# HTTP trigger function processed a request.");
string message = req.FunctionContext
.BindingContext
.BindingData["message"]
.ToString();
string kevent = "{ \"Offset\":364,\"Partition\":0,\"Topic\":\"kafkaeventhubtest1\",\"Timestamp\":\"2022-04-09T03:20:06.591Z\", \"Value\": \"" + message + "\", \"Headers\": [{ \"Key\": \"test\", \"Value\": \"dotnet-isolated\" }] }";
var response = req.CreateResponse(HttpStatusCode.OK);
return new MultipleOutputType()
{
Kevent = kevent,
HttpResponse = response
};
}
```


For a complete set of working .NET examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/dotnet-isolated/confluent).

The usage of the output binding depends on your version of the Node.js programming model.

In the Node.js v4 model, you define your output binding directly in your function code. For more information, see the [Azure Functions Node.js developer guide](functions-reference-node?pivots=nodejs-model-v4).

In these examples, the event providers are either Confluent or Azure Event Hubs. These examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const queryName = request.query.get("name");
const parsedbody = JSON.parse(body);
const name = queryName || parsedbody.name || "world";
context.extraOutputs.set(kafkaOutput, `Hello, ${parsedbody.name}!`);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


To send events in a batch, send an array of messages, as shown in these examples:

```
const { app, output } = require("@azure/functions");
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
async function kafkaOutputManyWithHttp(request, context) {
context.log(`Http function processed request for url "${request.url}"`);
const queryName = request.query.get("name");
const body = await request.text();
const parsedbody = body ? JSON.parse(body) : {};
parsedbody.name = parsedbody.name || "world";
const name = queryName || parsedbody.name;
context.extraOutputs.set(kafkaOutput, `Message one. Hello, ${name}!`);
context.extraOutputs.set(kafkaOutput, `Message two. Hello, ${name}!`);
return {
body: `Messages sent to kafka.`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputManyWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputManyWithHttp,
});
```


These examples show how to send an event message with headers to a Kafka topic:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const parsedbody = JSON.parse(body);
// assuming body is of the format { "key": "key", "value": {JSON object} }
context.extraOutputs.set(
kafkaOutput,
`{ "Offset":364,"Partition":0,"Topic":"test-topic","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "${JSON.stringify(
parsedbody.value
).replace(/"/g, '\\"')}", "Key":"${
parsedbody.key
}", "Headers": [{ "Key": "language", "Value": "javascript" }] }`
);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


For a complete set of working JavaScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/javascript-v4/src/functions).

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const queryName = request.query.get("name");
const parsedbody = JSON.parse(body);
const name = queryName || parsedbody.name || "world";
context.extraOutputs.set(kafkaOutput, `Hello, ${parsedbody.name}!`);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


To send events in a batch, send an array of messages, as shown in these examples:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputManyWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const queryName = request.query.get("name");
const body = await request.text();
const parsedbody = body ? JSON.parse(body) : {};
parsedbody.name = parsedbody.name || "world";
const name = queryName || parsedbody.name;
context.extraOutputs.set(kafkaOutput, `Message one. Hello, ${name}!`);
context.extraOutputs.set(kafkaOutput, `Message two. Hello, ${name}!`);
return {
body: `Messages sent to kafka.`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputManyWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputManyWithHttp,
});
```


These examples show how to send an event message with headers to a Kafka topic:

```
import {
app,
HttpRequest,
HttpResponseInit,
InvocationContext,
output,
} from "@azure/functions";
const kafkaOutput = output.generic({
type: "kafka",
direction: "out",
topic: "topic",
brokerList: "%BrokerList%",
username: "ConfluentCloudUsername",
password: "ConfluentCloudPassword",
protocol: "saslSsl",
authenticationMode: "plain",
});
export async function kafkaOutputWithHttp(
request: HttpRequest,
context: InvocationContext
): Promise<HttpResponseInit> {
context.log(`Http function processed request for url "${request.url}"`);
const body = await request.text();
const parsedbody = JSON.parse(body);
// assuming body is of the format { "key": "key", "value": {JSON object} }
context.extraOutputs.set(
kafkaOutput,
`{ "Offset":364,"Partition":0,"Topic":"test-topic","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "${JSON.stringify(
parsedbody.value
).replace(/"/g, '\\"')}", "Key":"${
parsedbody.key
}", "Headers": [{ "Key": "language", "Value": "typescript" }] }`
);
context.log(
`Sending message to kafka: ${context.extraOutputs.get(kafkaOutput)}`
);
return {
body: `Message sent to kafka with value: ${context.extraOutputs.get(
kafkaOutput
)}`,
status: 200,
};
}
const extraOutputs = [];
extraOutputs.push(kafkaOutput);
app.http("kafkaOutputWithHttp", {
methods: ["GET", "POST"],
authLevel: "anonymous",
extraOutputs,
handler: kafkaOutputWithHttp,
});
```


For a complete set of working TypeScript examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/typescript-v4/src/functions).

The specific properties of the function.json file depend on your event provider, which in these examples are either Confluent or Azure Event Hubs. The following examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

The following function.json defines the trigger for the specific provider in these examples:

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
]
},
{
"type": "kafka",
"name": "outputMessage",
"brokerList": "BrokerList",
"topic": "topic",
"username" : "%ConfluentCloudUserName%",
"password" : "%ConfluentCloudPassword%",
"protocol": "SASLSSL",
"authenticationMode": "PLAIN",
"direction": "out"
},
{
"type": "http",
"direction": "out",
"name": "Response"
}
]
}
```


The following code sends a message to the topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
$message
Push-OutputBinding -Name outputMessage -Value ($message)
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
})
```


The following code sends multiple messages as an array to the same topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
$message = @("one", "two")
Push-OutputBinding -Name outputMessage -Value ($message)
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
})
```


The following example shows how to send an event message with headers to the same Kafka topic:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$message = $Request.Query.Message
if (-not $message) {
$message = $Request.Body.Message
}
$kevent = @{
Offset = 364
Partition = 0
Topic = "kafkaeventhubtest1"
Timestamp = "2022-04-09T03:20:06.591Z"
Value = $message
Headers= @(@{
Key= "test"
Value= "powershell"
}
)
}
Push-OutputBinding -Name Message -Value $kevent
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::OK
Body = 'ok'
})
```


For a complete set of working PowerShell examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/powershell/).

The usage of the output binding depends on your version of the Python programming model.

In the Python v2 model, you define your output binding directly in your function code using decorators. For more information, see the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

These examples show a Kafka output binding for a function that an HTTP request triggers and sends data from the request to the Kafka topic.

```
input_msg = req.params.get('message')
outputMessage.set(input_msg)
return 'OK'
@KafkaOutput.function_name(name="KafkaOutputMany")
@KafkaOutput.route(route="kafka_output_many")
@KafkaOutput.kafka_output(arg_name="outputMessage", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain", data_type="string")
def kafka_output_many(req: func.HttpRequest, outputMessage: func.Out[str] ) -> func.HttpResponse:
outputMessage.set(json.dumps(['one', 'two']))
return 'OK'
```


To send events in a batch, send an array of messages, as shown in these examples:

```
@KafkaOutput.route(route="kafka_output_with_headers")
@KafkaOutput.kafka_output(arg_name="out", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain")
def kafka_output_with_headers(req: func.HttpRequest, out: func.Out[str]) -> func.HttpResponse:
message = req.params.get('message')
kevent = { "Offset":0,"Partition":0,"Topic":"dummy","Timestamp":"2022-04-09T03:20:06.591Z", "Value": message, "Headers": [{ "Key": "test", "Value": "python" }] }
out.set(json.dumps(kevent))
return 'OK'
@KafkaOutput.function_name(name="KafkaOutputManyWithHeaders")
@KafkaOutput.route(route="kafka_output_many_with_headers")
@KafkaOutput.kafka_output(arg_name="out", topic="KafkaTopic", broker_list="KafkaBrokerList", username="KafkaUsername", password="KafkaPassword", protocol="SaslSsl", authentication_mode="Plain")
def kafka_output_many_with_headers(req: func.HttpRequest, out: func.Out[str]) -> func.HttpResponse:
kevent = [{ "Offset": 364, "Partition":0,"Topic":"kafkaeventhubtest1","Timestamp":"2022-04-09T03:20:06.591Z", "Value": "one", "Headers": [{ "Key": "test", "Value": "python" }] },
```


These examples show how to send an event message with headers to a Kafka topic:

For a complete set of working Python examples, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/blob/dev/samples/python-v2/).

The annotations you use to configure the output binding depend on the specific event provider.

The following function sends a message to the Kafka topic.

```
@FunctionName("KafkaOutput")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<String> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("message");
String message = request.getBody().orElse(query);
context.getLogger().info("Message:" + message);
output.setValue(message);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
```


The following example shows how to send multiple messages to a Kafka topic.

```
@FunctionName("KafkaOutputMany")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<String[]> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String[] messages = new String[2];
messages[0] = "one";
messages[1] = "two";
output.setValue(messages);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
}
```


In this example, the output binding parameter is changed to string array.

The last example uses these `KafkaEntity`

and `KafkaHeader`

classes:

```
public class KafkaEntity {
public int Offset;
public int Partition;
public String Timestamp;
public String Topic;
public String Value;
public KafkaHeaders Headers[];
public KafkaEntity(int Offset, int Partition, String Topic, String Timestamp, String Value,KafkaHeaders[] headers) {
this.Offset = Offset;
this.Partition = Partition;
this.Topic = Topic;
this.Timestamp = Timestamp;
this.Value = Value;
this.Headers = headers;
}
```


```
public class KafkaHeaders{
public String Key;
public String Value;
public KafkaHeaders(String key, String value) {
this.Key = key;
this.Value = value;
}
```


The following example function sends a message with headers to a Kafka topic.

```
@FunctionName("KafkaOutputWithHeaders")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> request,
@KafkaOutput(
name = "kafkaOutput",
topic = "topic",
brokerList="%BrokerList%",
username = "%ConfluentCloudUsername%",
password = "ConfluentCloudPassword",
authenticationMode = BrokerAuthenticationMode.PLAIN,
// sslCaLocation = "confluent_cloud_cacert.pem", // Enable this line for windows.
protocol = BrokerProtocol.SASLSSL
) OutputBinding<KafkaEntity> output,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("message");
String message = request.getBody().orElse(query);
KafkaHeaders[] headers = new KafkaHeaders[1];
headers[0] = new KafkaHeaders("test", "java");
KafkaEntity kevent = new KafkaEntity(364, 0, "topic", "2022-04-09T03:20:06.591Z", message, headers);
output.setValue(kevent);
return request.createResponseBuilder(HttpStatus.OK).body("Ok").build();
}
```


For a complete set of working Java examples for Confluent, see the [Kafka extension repository](https://github.com/Azure/azure-functions-kafka-extension/tree/dev/samples/java/confluent/src/main/java/com/contoso/kafka).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `Kafka`

attribute to define the function trigger.

The following table explains the properties you can set by using this attribute:

| Parameter | Description |
|---|---|
BrokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**Topic****AvroSchema****KeyAvroSchema****KeyDataType**`KeyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**MaxMessageBytes**`1`

.**BatchSize**`10000`

.**EnableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

**MessageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**RequestTimeoutMs**`5000`

.**MaxRetries**`2`

. Retrying may cause reordering, unless `EnableIdempotence`

is set to `true`

.**AuthenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

, and `OAuthBearer`

.**Username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**Protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**SslCaLocation****SslCertificateLocation****SslKeyLocation****SslKeyPassword****SslCertificatePEM**[Connections](#connections)for more information.**SslKeyPEM**[Connections](#connections)for more information.**SslCaPEM**[Connections](#connections)for more information.**SslCertificateandKeyPEM**[Connections](#connections)for more information.**SchemaRegistryUrl**[Connections](#connections)for more information.**SchemaRegistryUsername**[Connections](#connections)for more information.**SchemaRegistryPassword**[Connections](#connections)for more information.**OAuthBearerMethod**`oidc`

and `default`

.**OAuthBearerClientId**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**OAuthBearerClientSecret**`OAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**OAuthBearerScope****OAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.**OAuthBearerExtensions**`oidc`

method is used. For example: `supportFeatureX=true,organizationId=sales-emea`

.## Annotations

The `KafkaOutput`

annotation enables you to create a function that writes to a specific topic. Supported options include the following elements:

| Element | Description |
|---|---|
name |
The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****dataType**`string`

, the input is treated as just a string. When `binary`

, the message is received as binary data, and Functions tries to deserialize it to an actual parameter type byte[].**avroSchema**[Currently not supported for Java](https://github.com/Azure/azure-functions-java-library/issues/198).)**maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

.**authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

function.json property |
Description |
|---|---|
type |
Set to `kafka` . |
direction |
Set to `out` . |
name |
The name of the variable that represents the brokered data in function code. |
brokerList |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****avroSchema****keyAvroSchema****keyDataType**`keyAvroSchema`

is set, this value is generic record. Accepted values are `Int`

, `Long`

, `String`

, and `Binary`

.**maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

.**authenticationMode**`NotSet`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`AuthenticationMode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NotSet`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****sslCertificatePEM**[Connections](#connections)for more information.**sslKeyPEM**[Connections](#connections)for more information.**sslCaPEM**[Connections](#connections)for more information.**sslCertificateandKeyPEM**[Connections](#connections)for more information.**schemaRegistryUrl**[Connections](#connections)for more information.**schemaRegistryUsername**[Connections](#connections)for more information.**schemaRegistryPassword**[Connections](#connections)for more information.**oAuthBearerMethod**`oidc`

and `default`

.**oAuthBearerClientId**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**oAuthBearerClientSecret**`oAuthBearerMethod`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**oAuthBearerScope****oAuthBearerTokenEndpointUrl**`oidc`

method is used. See [Connections](#connections)for more information.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file. Python uses snake_case naming conventions for configuration properties.

function.json property |
Description |
|---|---|
type |
Set to `kafka` . |
direction |
Set to `out` . |
name |
The name of the variable that represents the brokered data in function code. |
broker_list |
(Required) The list of Kafka brokers to which the output is sent. See
|

**topic****avroSchema****maxMessageBytes**`1`

.**batchSize**`10000`

.**enableIdempotence**`true`

, guarantees that messages are successfully produced exactly once and in the original produce order, with a default value of `false`

.**messageTimeoutMs**`300000`

. A time of `0`

is infinite. This value is the maximum time used to deliver a message (including retries). Delivery error occurs when either the retry count or the message timeout are exceeded.**requestTimeoutMs**`5000`

.**maxRetries**`2`

. Retrying might cause reordering, unless `EnableIdempotence`

is set to `true`

.**authentication_mode**`NOTSET`

(default), `Gssapi`

, `Plain`

, `ScramSha256`

, `ScramSha512`

.**username**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**password**`authentication_mode`

is `Gssapi`

. See [Connections](#connections)for more information.**protocol**`NOTSET`

(default), `plaintext`

, `ssl`

, `sasl_plaintext`

, `sasl_ssl`

.**sslCaLocation****sslCertificateLocation****sslKeyLocation****sslKeyPassword****schema_registry_url**[Connections](#connections)for more information.**schema_registry_username**[Connections](#connections)for more information.**schema_registry_password**[Connections](#connections)for more information.**o_auth_bearer_method**`oidc`

and `default`

.**o_auth_bearer_client_id**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client ID. See [Connections](#connections)for more information.**o_auth_bearer_client_secret**`o_auth_bearer_method`

is set to `oidc`

, this specifies the OAuth bearer client secret. See [Connections](#connections)for more information.**o_auth_bearer_scope****o_auth_bearer_token_endpoint_url**`oidc`

method is used. See [Connections](#connections)for more information.Note

Certificate PEM-related properties and Avro key-related properties aren't yet available in the Python library.

## Usage

The offset, partition, and timestamp for the event are generated at runtime. You can set only the value and headers inside the function. You set the topic in the function.json file.

Make sure you have access to the Kafka topic where you want to write. You configure the binding with access and connection credentials to the Kafka topic.

In a Premium plan, you must enable runtime scale monitoring for the Kafka output to scale out to multiple instances. To learn more, see [Enable runtime scaling](functions-bindings-kafka#enable-runtime-scaling).

For a complete set of supported host.json settings for the Kafka trigger, see [host.json settings](functions-bindings-kafka#hostjson-settings).

## Connections

Store all connection information required by your triggers and bindings in application settings, not in the binding definitions in your code. This guidance applies to credentials, which you should never store in your code.

Important

Credential settings must reference an [application setting](functions-how-to-use-azure-function-app-settings#settings). Don't hard-code credentials in your code or configuration files. When running locally, use the [local.settings.json file](functions-develop-local#local-settings-file) for your credentials, and don't publish the local.settings.json file.

When connecting to a managed Kafka cluster provided by [Confluent in Azure](https://www.confluent.io/azure/), you can use one of the following authentication methods.

Note

When using the Flex Consumption plan, file location-based certificate authentication properties (`SslCaLocation`

, `SslCertificateLocation`

, `SslKeyLocation`

) aren't supported. Instead, use the PEM-based certificate properties (`SslCaPEM`

, `SslCertificatePEM`

, `SslKeyPEM`

, `SslCertificateandKeyPEM`

) or store certificates in Azure Key Vault.

#### Schema Registry

To make use of schema registry provided by Confluent in Kafka Extension, set the following credentials:

| Setting | Recommended Value | Description |
|---|---|---|
SchemaRegistryUrl |
`SchemaRegistryUrl` |
URL of the schema registry service used for schema management. Usually of the format `https://psrc-xyz.us-east-2.aws.confluent.cloud` |
SchemaRegistryUsername |
`CONFLUENT_API_KEY` |
Username for basic auth on schema registry (if required). |
SchemaRegistryPassword |
`CONFLUENT_API_SECRET` |
Password for basic auth on schema registry (if required). |

#### Username/Password authentication

While using this form of authentication, make sure that `Protocol`

is set to either `SaslPlaintext`

or `SaslSsl`

, `AuthenticationMode`

is set to `Plain`

, `ScramSha256`

or `ScramSha512`

and, if the CA cert being used is different from the default ISRG Root X1 cert, make sure to update `SslCaLocation`

or `SslCaPEM`

.

| Setting | Recommended value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
Username |
`ConfluentCloudUsername` |
App setting named `ConfluentCloudUsername` contains the API access key from the Confluent Cloud web site. |
Password |
`ConfluentCloudPassword` |
App setting named `ConfluentCloudPassword` contains the API secret obtained from the Confluent Cloud web site. |
SslCaPEM |
`SSLCaPemCertificate` |
App setting named `SSLCaPemCertificate` that contains the CA certificate as a string in PEM format. The value should follow the standard format, for example: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----` . |

#### SSL authentication

Ensure that `Protocol`

is set to `SSL`

.

| Setting | Recommended Value | Description |
|---|---|---|
BrokerList |
`BootstrapServer` |
App setting named `BootstrapServer` contains the value of bootstrap server found in Confluent Cloud settings page. The value resembles `xyz-xyzxzy.westeurope.azure.confluent.cloud:9092` . |
SslCaPEM |
`SslCaCertificatePem` |
App setting named `SslCaCertificatePem` that contains PEM value of the CA certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslCertificatePEM |
`SslClientCertificatePem` |
App setting named `SslClientCertificatePem` that contains PEM value of the client certificate as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII...JQ==\n-----END CERTIFICATE-----` |
SslKeyPEM |
`SslClientKeyPem` |
App setting named `SslClientKeyPem` that contains PEM value of the client private key as a string. The value should follow the standard format: `-----BEGIN PRIVATE KEY-----\nMII...JQ==\n-----END PRIVATE KEY-----` |
SslCertificateandKeyPEM |
`SslClientCertificateAndKeyPem` |
App setting named `SslClientCertificateAndKeyPem` that contains PEM value of the client certificate and client private key concatenated as a string. The value should follow the standard format: `-----BEGIN CERTIFICATE-----\nMII....JQ==\n-----END CERTIFICATE-----\n-----BEGIN PRIVATE KEY-----\nMIIE....BM=\n-----END PRIVATE KEY-----` |
SslKeyPassword |
`SslClientKeyPassword` |
App setting named `SslClientKeyPassword` that contains the password for the private key (if any). |

#### OAuth authentication

When using OAuth authentication, configure the OAuth-related properties in your binding definitions.

The string values you use for these settings must be present as [application settings in Azure](functions-how-to-use-azure-function-app-settings#settings) or in the `Values`

collection in the [local.settings.json file](functions-develop-local#local-settings-file) during local development.

You should also set the `Protocol`

and `AuthenticationMode`

in your binding definitions.
