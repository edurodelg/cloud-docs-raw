---
merged_at: 2026-01-25T15:41:11.651638
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-storage-blob-output_monitor-functions.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-storage-blob-output.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-output -->

# Azure Blob storage output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The output binding allows you to modify and delete blob storage data in an Azure Function.

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
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
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

#### HTTP trigger, using OutputBinding (Java)

The following example shows a Java function that uses the `HttpTrigger`

annotation to receive a parameter containing the name of a file in a blob storage container. The `BlobInput`

annotation then reads the file and passes its contents to the function as a `byte[]`

. The `BlobOutput`

annotation binds to `OutputBinding outputItem`

, which is then used by the function to write the contents of the input blob to the configured storage container.

```
@FunctionName("copyBlobHttp")
@StorageAccount("Storage_Account_Connection_String")
public HttpResponseMessage copyBlobHttp(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@BlobInput(
name = "file",
dataType = "binary",
path = "samples-workitems/{Query.file}")
byte[] content,
@BlobOutput(
name = "target",
path = "myblob/{Query.file}-CopyViaHttp")
OutputBinding<String> outputItem,
final ExecutionContext context) {
// Save blob to outputItem
outputItem.setValue(new String(content, StandardCharsets.UTF_8));
// build HTTP response with size of requested blob
return request.createResponseBuilder(HttpStatus.OK)
.body("The size of \"" + request.getQueryParameters().get("file") + "\" is: " + content.length + " bytes")
.build();
}
```


#### Queue trigger, using function return value (Java)

The following example shows a Java function that uses the `QueueTrigger`

annotation to receive a message containing the name of a file in a blob storage container. The `BlobInput`

annotation then reads the file and passes its contents to the function as a `byte[]`

. The `BlobOutput`

annotation binds to the function return value, which is then used by the runtime to write the contents of the input blob to the configured storage container.

```
@FunctionName("copyBlobQueueTrigger")
@StorageAccount("Storage_Account_Connection_String")
@BlobOutput(
name = "target",
path = "myblob/{queueTrigger}-Copy")
public String copyBlobQueue(
@QueueTrigger(
name = "filename",
dataType = "string",
queueName = "myqueue-items")
String filename,
@BlobInput(
name = "file",
path = "samples-workitems/{queueTrigger}")
String content,
final ExecutionContext context) {
context.getLogger().info("The content of \"" + filename + "\" is: " + content);
return content;
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@BlobOutput`

annotation on function parameters whose value would be written to an object in blob storage. The parameter type should be `OutputBinding<T>`

, where `T`

is any native Java type or a POJO.

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


The following example demonstrates how to create a copy of an incoming blob as the output from a [PowerShell function](functions-reference-powershell).

In the function's configuration file (*function.json*), the `trigger`

metadata property is used to specify the output blob name in the `path`

properties.

Note

To avoid infinite loops, make sure your input and output paths are different.

```
{
"bindings": [
{
"name": "myInputBlob",
"path": "data/{trigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "in",
"type": "blobTrigger"
},
{
"name": "myOutputBlob",
"type": "blob",
"path": "data/copy/{trigger}",
"connection": "MyStorageConnectionAppSetting",
"direction": "out"
}
],
"disabled": false
}
```


Here's the PowerShell code:

```
# Input bindings are passed in via param block.
param([byte[]] $myInputBlob, $TriggerMetadata)
Write-Host "PowerShell Blob trigger function Processed blob Name: $($TriggerMetadata.Name)"
Push-OutputBinding -Name myOutputBlob -Value $myInputBlob
```


The following example shows blob input and output bindings. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

The code creates a copy of a blob.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="BlobOutput1")
@app.route(route="file")
@app.blob_input(arg_name="inputblob",
path="sample-workitems/test.txt",
connection="<BLOB_CONNECTION_SETTING>")
@app.blob_output(arg_name="outputblob",
path="newblob/test.txt",
connection="<BLOB_CONNECTION_SETTING>")
def main(req: func.HttpRequest, inputblob: str, outputblob: func.Out[str]):
logging.info(f'Python Queue trigger function processed {len(inputblob)} bytes')
outputblob.set(inputblob)
return "ok"
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#blob-output).

The `BlobOutputAttribute`

constructor takes the following parameters:

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
`dataType` |
For dynamically typed languages, specifies the underlying data type. Possible values are `string` , `binary` , or `stream` . For more detail, refer to the
|

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

The `@BlobOutput`

attribute gives you access to the blob that triggered the function. If you use a byte array with the attribute, set `dataType`

to `binary`

. Refer to the [output example](#example) for details.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `output.storageBlob()`

method.

| Property | Description |
|---|---|
path |
The path to the blob container. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

The following table explains the binding configuration properties that you set in the *function.json* file.

| Property | Description |
|---|---|
type |
Must be set to `blob` . |
direction |
Must be set to `out` for an output binding. Exceptions are noted in the
|
name |
The name of the variable that represents the blob in function code. Set to `$return` to reference the function return value. |
path |
The path to the blob container. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Blobs. See
|

See the [Example section](#example) for complete examples.

## Usage

The binding types supported by blob output depend on the extension package version and the C# modality used in your function app.

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

Binding to `string`

, or `Byte[]`

is only recommended when the blob size is small. This is recommended because the entire blob contents are loaded into memory. For most blobs, use a `Stream`

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

The `@BlobOutput`

attribute gives you access to the blob that triggered the function. If you use a byte array with the attribute, set `dataType`

to `binary`

. Refer to the [output example](#example) for details.

Access the blob data via a parameter that matches the name designated by binding's name parameter in the *function.json* file.

You can declare function parameters as the following types to write out to blob storage:

- Strings as
`func.Out[str]`

- Streams as
`func.Out[func.InputStream]`


Refer to the [output example](#example) for details.

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

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Blob |
|


---

<!-- DOCUMENTO FUSIONADO: monitor-functions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions -->

# Monitor Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes:

- The types of monitoring data you can collect for this service.
- Ways to analyze that data.

Note

If you're already familiar with this service and/or Azure Monitor and just want to know how to analyze monitoring data, see the [Analyze](#analyze-monitoring-data) section near the end of this article.

When you have critical applications and business processes that rely on Azure resources, you need to monitor and get alerts for your system. The Azure Monitor service collects and aggregates metrics and logs from every component of your system. Azure Monitor provides you with a view of availability, performance, and resilience, and notifies you of issues. You can use the Azure portal, PowerShell, Azure CLI, REST API, or client libraries to set up and view monitoring data.

- For more information on Azure Monitor, see the
[Azure Monitor overview](/en-us/azure/azure-monitor/overview). - For more information on how to monitor Azure resources in general, see
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource).

## Insights

Some services in Azure have a built-in monitoring dashboard in the Azure portal that provides a starting point for monitoring your service. These dashboards are called *insights*, and you can find them in the **Insights Hub** of Azure Monitor in the Azure portal.

### Application Insights

Azure Functions has built-in integration with Application Insights to monitor function executions. For detailed information about how to integrate, configure, and use Application Insights to monitor Azure Functions, see the following articles:

[Monitor executions in Azure Functions](functions-monitoring)[Configure monitoring for Azure Functions](configure-monitoring)[Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data)[Monitor Azure Functions with Application Insights](/en-us/azure/azure-monitor/app/monitor-functions)

## Resource types

Azure uses the concept of resource types and IDs to identify everything in a subscription. Resource types are also part of the resource IDs for every resource running in Azure. For example, one resource type for a virtual machine is `Microsoft.Compute/virtualMachines`

. For a list of services and their associated resource types, see [Resource providers](/en-us/azure/azure-resource-manager/management/azure-services-resource-providers).

Azure Monitor similarly organizes core monitoring data into metrics and logs based on resource types, also called *namespaces*. Different metrics and logs are available for different resource types. Your service might be associated with more than one resource type.

For more information about the resource types for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference).

## Data storage

For Azure Monitor:

- Metrics data is stored in the Azure Monitor metrics database.
- Log data is stored in the Azure Monitor logs store. Log Analytics is a tool in the Azure portal that can query this store.
- The Azure activity log is a separate store with its own interface in the Azure portal.

You can optionally route metric and activity log data to the Azure Monitor logs store. You can then use Log Analytics to query the data and correlate it with other log data.

Many services can use diagnostic settings to send metric and log data to other storage locations outside Azure Monitor. Examples include Azure Storage, [hosted partner systems](/en-us/azure/partner-solutions/overview), and [non-Azure partner systems, by using Event Hubs](/en-us/azure/azure-monitor/essentials/stream-monitoring-data-event-hubs).

For detailed information on how Azure Monitor stores data, see [Azure Monitor data platform](/en-us/azure/azure-monitor/platform/data-platform).

## Azure Monitor platform metrics

Azure Monitor provides platform metrics for most services. These metrics are:

- Individually defined for each namespace.
- Stored in the Azure Monitor time-series metrics database.
- Lightweight and capable of supporting near real-time alerting.
- Used to track the performance of a resource over time.

**Collection:** Azure Monitor collects platform metrics automatically. No configuration is required.

**Routing:** You can also route some platform metrics to Azure Monitor Logs / Log Analytics so you can query them with other log data. Check the **DS export** setting for each metric to see if you can use a diagnostic setting to route the metric to Azure Monitor Logs / Log Analytics.

- For more information, see the
[Metrics diagnostic setting](/en-us/azure/azure-monitor/essentials/diagnostic-settings#metrics). - To configure diagnostic settings for a service, see
[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings).

For a list of all metrics it's possible to gather for all resources in Azure Monitor, see [Supported metrics in Azure Monitor](/en-us/azure/azure-monitor/platform/metrics-supported).

For a list of available metrics for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference#metrics).

Note

App Service metrics (Microsoft.Web/sites) aren't available when your function app runs on Linux in a [Consumption plan](consumption-plan).

## Azure Monitor resource logs

Resource logs provide insight into operations that were done by an Azure resource. Logs are generated automatically, but you must route them to Azure Monitor logs to save or query them. Logs are organized in categories. A given namespace might have multiple resource log categories.

**Collection:** Resource logs aren't collected and stored until you create a *diagnostic setting* and route the logs to one or more locations. When you create a diagnostic setting, you specify which categories of logs to collect. There are multiple ways to create and maintain diagnostic settings, including the Azure portal, programmatically, and though Azure Policy.

**Routing:** The suggested default is to route resource logs to Azure Monitor Logs so you can query them with other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information, see [Azure resource logs](/en-us/azure/azure-monitor/essentials/resource-logs) and [Resource log destinations](/en-us/azure/azure-monitor/essentials/diagnostic-settings#destinations).

For detailed information about collecting, storing, and routing resource logs, see [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

For a list of all available resource log categories in Azure Monitor, see [Supported resource logs in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-logs/logs-index).

All resource logs in Azure Monitor have the same header fields, followed by service-specific fields. The common schema is outlined in [Azure Monitor resource log schema](/en-us/azure/azure-monitor/essentials/resource-logs-schema).

Azure Functions integrates with Azure Monitor Logs to monitor functions. For detailed instructions on how to set up diagnostic settings to configure and route resource logs, see [Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/platform/diagnostic-settings).


For the available resource log categories, their associated Log Analytics tables, and the logs schemas for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference#resource-logs).

Important

Application Insights processes telemetry in batches. When a batch payload is too large or contains unescaped special characters, log entries might be dropped. To help prevent data loss:

- Limit individual log messages to 10,000 characters, especially when you log large XML or JSON payloads.
- Escape special characters in log data.
- Summarize or truncate large payloads before you log them.

## Azure activity log

The activity log contains subscription-level events that track operations for each Azure resource as seen from outside that resource; for example, creating a new resource or starting a virtual machine.

**Collection:** Activity log events are automatically generated and collected in a separate store for viewing in the Azure portal.

**Routing:** You can send activity log data to Azure Monitor Logs so you can analyze it alongside other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information on how to route the activity log, see [Overview of the Azure activity log](/en-us/azure/azure-monitor/essentials/activity-log).

## Other logs

Azure Functions also offers the ability to collect more than Azure Monitor resource logs. To view a near real time stream of application log files generated by your function running in Azure, you can connect to Application Insights and use Live Metrics Stream. Or, you can use the App Service platform built-in log streaming to view a stream of application log files. For more information, see [Enable streaming execution logs in Azure Functions](streaming-logs).

## Analyze monitoring data

There are many tools for analyzing monitoring data.

### Azure Monitor tools

Azure Monitor supports the following basic tools:

[Metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started), a tool in the Azure portal that allows you to view and analyze metrics for Azure resources. For more information, see[Analyze metrics with Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started).[Log Analytics](/en-us/azure/azure-monitor/learn/quick-create-workspace), a tool in the Azure portal that allows you to query and analyze log data by using the[Kusto query language (KQL)](/en-us/azure/data-explorer/kusto/query). For more information, see[Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/get-started-queries).The

[activity log](/en-us/azure/azure-monitor/essentials/activity-log), which has a user interface in the Azure portal for viewing and basic searches. To do more in-depth analysis, you have to route the data to Azure Monitor logs and run more complex queries in Log Analytics.

Tools that allow more complex visualization include:

[Dashboards](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards)that let you combine different kinds of data into a single pane in the Azure portal.[Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview), customizable reports that you can create in the Azure portal. Workbooks can include text, metrics, and log queries.[Grafana](/en-us/azure/azure-monitor/visualize/grafana-plugin), an open platform tool that excels in operational dashboards. You can use Grafana to create dashboards that include data from multiple sources other than Azure Monitor.[Power BI](/en-us/azure/azure-monitor/logs/log-powerbi), a business analytics service that provides interactive visualizations across various data sources. You can configure Power BI to automatically import log data from Azure Monitor to take advantage of these visualizations.

### Azure Monitor export tools

You can get data out of Azure Monitor into other tools by using the following methods:

**Metrics:**Use the[REST API for metrics](/en-us/rest/api/monitor/operation-groups)to extract metric data from the Azure Monitor metrics database. The API supports filter expressions to refine the data retrieved. For more information, see[Azure Monitor REST API reference](/en-us/rest/api/monitor/filter-syntax).**Logs:**Use the REST API or the[associated client libraries](/en-us/azure/azure-monitor/logs/api/overview).Another option is the

[workspace data export](/en-us/azure/azure-monitor/logs/logs-data-export?tabs=portal).

To get started with the REST API for Azure Monitor, see [Azure monitoring REST API walkthrough](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough?tabs=portal).

### Analyze metrics for Azure Functions

Functions provides these two dynamic scale plans that support serverless hosting:

Provides fast horizontal scaling, with flexible compute options, virtual network integration, and full support for connections using Microsoft Entra ID authentication. In this plan, instances dynamically scale out based on configured per-instance concurrency, incoming events, and per-function workloads for optimal efficiency. Flex Consumption is the recommended plan for serverless hosting. For more information, see [Azure Functions Flex Consumption plan hosting](flex-consumption-plan).

The app-level metrics available to your app depend on the type of consumption plan you use.

These Azure Monitor metrics are related to Flex Consumption plan billing:

| Metric | Description | Meter calculation |
|---|---|---|
On Demand Function Execution Count |
Total number of function executions in on demand instances. | `OnDemandFunctionExecutionCount` relates to the On Demand Total Executions meter. |
Always Ready Function Execution Count |
Total number of function executions in always ready instances. | `AlwaysReadyFunctionExecutionCount` relates to the Always Ready Total Executions meter. |
On Demand Function Execution Units |
Total MB-milliseconds from on demand instances while actively executing functions. | `OnDemandFunctionExecutionUnits / 1,024,000` is the On Demand Execution Time meter, in GB-seconds. |
Always Ready Function Execution Units |
Total MB-milliseconds from always ready instances while actively executing functions. | `AlwaysReadyFunctionExecutionUnits / 1,024,000` is the Always Ready Execution Time meter, in GB-seconds. |
Always Ready Units |
The total MB-milliseconds of always ready instances assigned to the app, whether or not functions are actively executing. | `AlwaysReadyUnits / 1,024,000` is the Always Ready Baseline meter, in GB-seconds. |

For more information, see [Azure Functions monitoring data reference](monitor-functions-reference).

To better understand the costs of your functions, use Azure Monitor to view cost-related metrics that your function apps generate. You can view Monitor metrics by using one of these tools:

Use [Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started) to view cost-related data for your Flex Consumption plan function apps in a graphical format.

In the

[Azure portal](https://portal.azure.com), go to your function app.In the left panel, scroll down to

**Monitoring**and select**Metrics**.From

**Metric**, select**On Demand Function Execution Count**and**Sum**for**Aggregation**. This selection adds the sum of the execution counts during the chosen period to the chart.Select

**Add metric**and add**On Demand Function Execution Units**,**Always Ready Function Execution Count**,**Always Ready Function Execution Units**, and**Always Ready Units**to the chart.

The resulting chart contains the totals for all the Flex Consumption execution metrics in the chosen time range, which in this example is a custom time range.

Because the number of On Demand Function Execution Units is greater than On Demand Function Execution Count, and there were no [always ready instances](flex-consumption-plan#always-ready-instances) on the app, the chart just shows On Demand Function Execution Units.

This chart shows a total of 3.54 billion `On Demand Function Execution Units`

consumed in a 16-minute period, measured in MB-milliseconds. To convert to GB-seconds, divide by 1,024,000. In this example, the function app consumed `3,540,000,000 / 1,024,000 = 3,457.03`

GB-seconds. You can take this value and multiply it by the current price of On Demand Execution Time on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/), which gives you the cost of these 16 minutes, assuming you already used any free grants of execution time. You can use this same calculation with the The Always Ready Function Execution Units metric and the Always Ready Execution Time billing meter cost, as well as with the Always Ready Units metric and the Always Ready Baseline billing meter cost, to find out the GB-seconds costs for always ready instances.

To calculate the On Demand Total Executions cost, take the On Demand Function Execution Count sum for the same time period, convert to millions, and then multiply by the On Demand Total Executions price on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/). For example, 2,100 executions in the example above converts to `0.0021`

million executions. You can use this same calculation with the Always Ready Function Execution Count metric and the Always Ready Total Executions billing meter to find out the cost for executions handled by always ready instance.

To learn more about estimating costs for these plans, see [Estimating consumption plan costs](functions-consumption-costs).

### Analyze logs for Azure Functions

Azure Functions writes all logs to the **FunctionAppLogs** table under **LogManagement** in the Log Analytics workspace where you send the data. You can use Kusto queries to query the data.


## Kusto queries

You can analyze monitoring data in the Azure Monitor Logs / Log Analytics store by using the Kusto query language (KQL).

Important

When you select **Logs** from the service's menu in the portal, Log Analytics opens with the query scope set to the current service. This scope means that log queries will only include data from that type of resource. If you want to run a query that includes data from other Azure services, select **Logs** from the **Azure Monitor** menu. See [Log query scope and time range in Azure Monitor Log Analytics](/en-us/azure/azure-monitor/logs/scope) for details.

For a list of common queries for any service, see the [Log Analytics queries interface](/en-us/azure/azure-monitor/logs/queries).

The following sample queries can help you monitor all your functions app logs:

```
FunctionAppLogs
| order by TimeGenerated desc
```


```
FunctionAppLogs
| project TimeGenerated, HostInstanceId, Message, _ResourceId
| order by TimeGenerated desc
```


The following sample query can help you monitor a specific functions app's logs:

```
FunctionAppLogs
| where FunctionName == "<Function name>"
| order by TimeGenerated desc
```


The following sample query can help you monitor exceptions on all your functions app logs:

```
FunctionAppLogs
| where ExceptionDetails != ""
| order by TimeGenerated asc
```


The following sample query can help you monitor exceptions on a specific functions app's logs:

```
FunctionAppLogs
| where ExceptionDetails != ""
| where FunctionName == "<Function name>"
| order by TimeGenerated desc
```


## Alerts

Azure Monitor alerts proactively notify you when specific conditions are found in your monitoring data. Alerts allow you to identify and address issues in your system before your customers notice them. For more information, see [Azure Monitor alerts](/en-us/azure/azure-monitor/alerts/alerts-overview).

There are many sources of common alerts for Azure resources. For examples of common alerts for Azure resources, see [Sample log alert queries](/en-us/azure/azure-monitor/alerts/alerts-log-alert-query-samples). The [Azure Monitor Baseline Alerts (AMBA)](https://aka.ms/amba) site provides a semi-automated method of implementing important platform metric alerts, dashboards, and guidelines. The site applies to a continually expanding subset of Azure services, including all services that are part of the Azure Landing Zone (ALZ).

The common alert schema standardizes the consumption of Azure Monitor alert notifications. For more information, see [Common alert schema](/en-us/azure/azure-monitor/alerts/alerts-common-schema).

### Types of alerts

You can alert on any metric or log data source in the Azure Monitor data platform. There are many different types of alerts depending on the services you're monitoring and the monitoring data you're collecting. Different types of alerts have various benefits and drawbacks. For more information, see [Choose the right monitoring alert type](/en-us/azure/azure-monitor/alerts/alerts-types).

The following list describes the types of Azure Monitor alerts you can create:

[Metric alerts](/en-us/azure/azure-monitor/alerts/alerts-types#metric-alerts)evaluate resource metrics at regular intervals. Metrics can be platform metrics, custom metrics, logs from Azure Monitor converted to metrics, or Application Insights metrics. Metric alerts can also apply multiple conditions and dynamic thresholds.[Log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#log-alerts)allow users to use a Log Analytics query to evaluate resource logs at a predefined frequency.[Activity log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#activity-log-alerts)trigger when a new activity log event occurs that matches defined conditions. Resource Health alerts and Service Health alerts are activity log alerts that report on your service and resource health.

Some Azure services also support [smart detection alerts](/en-us/azure/azure-monitor/alerts/alerts-types#smart-detection-alerts), [Prometheus alerts](/en-us/azure/azure-monitor/alerts/alerts-types#prometheus-alerts), or [recommended alert rules](/en-us/azure/azure-monitor/alerts/alerts-manage-alert-rules#enable-recommended-alert-rules-in-the-azure-portal).

For some services, you can monitor at scale by applying the same metric alert rule to multiple resources of the same type that exist in the same Azure region. Individual notifications are sent for each monitored resource. For supported Azure services and clouds, see [Monitor multiple resources with one alert rule](/en-us/azure/azure-monitor/alerts/alerts-types#monitor-multiple-resources-with-one-alert-rule).

Note

If you're creating or running an application that runs on your service, [Azure Monitor application insights](/en-us/azure/azure-monitor/overview#application-insights) might offer more types of alerts.

### Azure Functions alert rules

The following table lists common and recommended alert rules for Azure Functions. These alerts are just recommendations. You can set alerts for any metric, log entry, or activity log entry listed in the [Monitoring data reference for Azure Functions](monitor-functions-reference).

| Alert type | Condition | Description |
|---|---|---|
| Metric | Average connections | When number of connections exceed a set value |
| Metric | HTTP 404 | When HTTP 404 responses exceed a set value |
| Metric | HTTP Server Errors | When HTTP 5xx errors exceed a set value |
| Activity Log | Create or update function app | When app is created or updated |
| Activity Log | Delete function app | When app is deleted |
| Activity Log | Restart function app | When app is restarted |
| Activity Log | Stop function app | When app is stopped |

### Advisor recommendations

For some services, if critical conditions or imminent changes occur during resource operations, an alert displays on the service **Overview** page in the portal. You can find more information and recommended fixes for the alert in **Advisor recommendations** under **Monitoring** in the left menu. During normal operations, no advisor recommendations display.

For more information on Azure Advisor, see [Azure Advisor overview](/en-us/azure/advisor/advisor-overview).

## Related content

For more information about monitoring Azure Functions, see the following articles:

[Azure Functions monitoring data reference](monitor-functions-reference)provides a reference of the metrics, logs, and other important values available for your function app.[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)gives general details about monitoring Azure resources.[Monitor executions in Azure Functions](functions-monitoring)details how to monitor a function app.[How to configure monitoring for Azure Functions](configure-monitoring)describes how to configure monitoring.[Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data)describes how to view and query the data being collected from a function app.


---

<!-- DOCUMENTO FUSIONADO: _functions-monitor-log-analytics__event-driven-scaling__functions-bindings-dapr-_046c74.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-monitor-log-analytics.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-monitor-log-analytics -->

# Monitor Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes:

- The types of monitoring data you can collect for this service.
- Ways to analyze that data.

Note

If you're already familiar with this service and/or Azure Monitor and just want to know how to analyze monitoring data, see the [Analyze](#analyze-monitoring-data) section near the end of this article.

When you have critical applications and business processes that rely on Azure resources, you need to monitor and get alerts for your system. The Azure Monitor service collects and aggregates metrics and logs from every component of your system. Azure Monitor provides you with a view of availability, performance, and resilience, and notifies you of issues. You can use the Azure portal, PowerShell, Azure CLI, REST API, or client libraries to set up and view monitoring data.

- For more information on Azure Monitor, see the
[Azure Monitor overview](/en-us/azure/azure-monitor/overview). - For more information on how to monitor Azure resources in general, see
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource).

## Insights

Some services in Azure have a built-in monitoring dashboard in the Azure portal that provides a starting point for monitoring your service. These dashboards are called *insights*, and you can find them in the **Insights Hub** of Azure Monitor in the Azure portal.

### Application Insights

Azure Functions has built-in integration with Application Insights to monitor function executions. For detailed information about how to integrate, configure, and use Application Insights to monitor Azure Functions, see the following articles:

[Monitor executions in Azure Functions](functions-monitoring)[Configure monitoring for Azure Functions](configure-monitoring)[Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data)[Monitor Azure Functions with Application Insights](/en-us/azure/azure-monitor/app/monitor-functions)

## Resource types

Azure uses the concept of resource types and IDs to identify everything in a subscription. Resource types are also part of the resource IDs for every resource running in Azure. For example, one resource type for a virtual machine is `Microsoft.Compute/virtualMachines`

. For a list of services and their associated resource types, see [Resource providers](/en-us/azure/azure-resource-manager/management/azure-services-resource-providers).

Azure Monitor similarly organizes core monitoring data into metrics and logs based on resource types, also called *namespaces*. Different metrics and logs are available for different resource types. Your service might be associated with more than one resource type.

For more information about the resource types for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference).

## Data storage

For Azure Monitor:

- Metrics data is stored in the Azure Monitor metrics database.
- Log data is stored in the Azure Monitor logs store. Log Analytics is a tool in the Azure portal that can query this store.
- The Azure activity log is a separate store with its own interface in the Azure portal.

You can optionally route metric and activity log data to the Azure Monitor logs store. You can then use Log Analytics to query the data and correlate it with other log data.

Many services can use diagnostic settings to send metric and log data to other storage locations outside Azure Monitor. Examples include Azure Storage, [hosted partner systems](/en-us/azure/partner-solutions/overview), and [non-Azure partner systems, by using Event Hubs](/en-us/azure/azure-monitor/essentials/stream-monitoring-data-event-hubs).

For detailed information on how Azure Monitor stores data, see [Azure Monitor data platform](/en-us/azure/azure-monitor/platform/data-platform).

## Azure Monitor platform metrics

Azure Monitor provides platform metrics for most services. These metrics are:

- Individually defined for each namespace.
- Stored in the Azure Monitor time-series metrics database.
- Lightweight and capable of supporting near real-time alerting.
- Used to track the performance of a resource over time.

**Collection:** Azure Monitor collects platform metrics automatically. No configuration is required.

**Routing:** You can also route some platform metrics to Azure Monitor Logs / Log Analytics so you can query them with other log data. Check the **DS export** setting for each metric to see if you can use a diagnostic setting to route the metric to Azure Monitor Logs / Log Analytics.

- For more information, see the
[Metrics diagnostic setting](/en-us/azure/azure-monitor/essentials/diagnostic-settings#metrics). - To configure diagnostic settings for a service, see
[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings).

For a list of all metrics it's possible to gather for all resources in Azure Monitor, see [Supported metrics in Azure Monitor](/en-us/azure/azure-monitor/platform/metrics-supported).

For a list of available metrics for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference#metrics).

Note

App Service metrics (Microsoft.Web/sites) aren't available when your function app runs on Linux in a [Consumption plan](consumption-plan).

## Azure Monitor resource logs

Resource logs provide insight into operations that were done by an Azure resource. Logs are generated automatically, but you must route them to Azure Monitor logs to save or query them. Logs are organized in categories. A given namespace might have multiple resource log categories.

**Collection:** Resource logs aren't collected and stored until you create a *diagnostic setting* and route the logs to one or more locations. When you create a diagnostic setting, you specify which categories of logs to collect. There are multiple ways to create and maintain diagnostic settings, including the Azure portal, programmatically, and though Azure Policy.

**Routing:** The suggested default is to route resource logs to Azure Monitor Logs so you can query them with other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information, see [Azure resource logs](/en-us/azure/azure-monitor/essentials/resource-logs) and [Resource log destinations](/en-us/azure/azure-monitor/essentials/diagnostic-settings#destinations).

For detailed information about collecting, storing, and routing resource logs, see [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

For a list of all available resource log categories in Azure Monitor, see [Supported resource logs in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-logs/logs-index).

All resource logs in Azure Monitor have the same header fields, followed by service-specific fields. The common schema is outlined in [Azure Monitor resource log schema](/en-us/azure/azure-monitor/essentials/resource-logs-schema).

Azure Functions integrates with Azure Monitor Logs to monitor functions. For detailed instructions on how to set up diagnostic settings to configure and route resource logs, see [Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/platform/diagnostic-settings).


For the available resource log categories, their associated Log Analytics tables, and the logs schemas for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference#resource-logs).

Important

Application Insights processes telemetry in batches. When a batch payload is too large or contains unescaped special characters, log entries might be dropped. To help prevent data loss:

- Limit individual log messages to 10,000 characters, especially when you log large XML or JSON payloads.
- Escape special characters in log data.
- Summarize or truncate large payloads before you log them.

## Azure activity log

The activity log contains subscription-level events that track operations for each Azure resource as seen from outside that resource; for example, creating a new resource or starting a virtual machine.

**Collection:** Activity log events are automatically generated and collected in a separate store for viewing in the Azure portal.

**Routing:** You can send activity log data to Azure Monitor Logs so you can analyze it alongside other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information on how to route the activity log, see [Overview of the Azure activity log](/en-us/azure/azure-monitor/essentials/activity-log).

## Other logs

Azure Functions also offers the ability to collect more than Azure Monitor resource logs. To view a near real time stream of application log files generated by your function running in Azure, you can connect to Application Insights and use Live Metrics Stream. Or, you can use the App Service platform built-in log streaming to view a stream of application log files. For more information, see [Enable streaming execution logs in Azure Functions](streaming-logs).

## Analyze monitoring data

There are many tools for analyzing monitoring data.

### Azure Monitor tools

Azure Monitor supports the following basic tools:

[Metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started), a tool in the Azure portal that allows you to view and analyze metrics for Azure resources. For more information, see[Analyze metrics with Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started).[Log Analytics](/en-us/azure/azure-monitor/learn/quick-create-workspace), a tool in the Azure portal that allows you to query and analyze log data by using the[Kusto query language (KQL)](/en-us/azure/data-explorer/kusto/query). For more information, see[Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/get-started-queries).The

[activity log](/en-us/azure/azure-monitor/essentials/activity-log), which has a user interface in the Azure portal for viewing and basic searches. To do more in-depth analysis, you have to route the data to Azure Monitor logs and run more complex queries in Log Analytics.

Tools that allow more complex visualization include:

[Dashboards](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards)that let you combine different kinds of data into a single pane in the Azure portal.[Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview), customizable reports that you can create in the Azure portal. Workbooks can include text, metrics, and log queries.[Grafana](/en-us/azure/azure-monitor/visualize/grafana-plugin), an open platform tool that excels in operational dashboards. You can use Grafana to create dashboards that include data from multiple sources other than Azure Monitor.[Power BI](/en-us/azure/azure-monitor/logs/log-powerbi), a business analytics service that provides interactive visualizations across various data sources. You can configure Power BI to automatically import log data from Azure Monitor to take advantage of these visualizations.

### Azure Monitor export tools

You can get data out of Azure Monitor into other tools by using the following methods:

**Metrics:**Use the[REST API for metrics](/en-us/rest/api/monitor/operation-groups)to extract metric data from the Azure Monitor metrics database. The API supports filter expressions to refine the data retrieved. For more information, see[Azure Monitor REST API reference](/en-us/rest/api/monitor/filter-syntax).**Logs:**Use the REST API or the[associated client libraries](/en-us/azure/azure-monitor/logs/api/overview).Another option is the

[workspace data export](/en-us/azure/azure-monitor/logs/logs-data-export?tabs=portal).

To get started with the REST API for Azure Monitor, see [Azure monitoring REST API walkthrough](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough?tabs=portal).

### Analyze metrics for Azure Functions

Functions provides these two dynamic scale plans that support serverless hosting:

Provides fast horizontal scaling, with flexible compute options, virtual network integration, and full support for connections using Microsoft Entra ID authentication. In this plan, instances dynamically scale out based on configured per-instance concurrency, incoming events, and per-function workloads for optimal efficiency. Flex Consumption is the recommended plan for serverless hosting. For more information, see [Azure Functions Flex Consumption plan hosting](flex-consumption-plan).

The app-level metrics available to your app depend on the type of consumption plan you use.

These Azure Monitor metrics are related to Flex Consumption plan billing:

| Metric | Description | Meter calculation |
|---|---|---|
On Demand Function Execution Count |
Total number of function executions in on demand instances. | `OnDemandFunctionExecutionCount` relates to the On Demand Total Executions meter. |
Always Ready Function Execution Count |
Total number of function executions in always ready instances. | `AlwaysReadyFunctionExecutionCount` relates to the Always Ready Total Executions meter. |
On Demand Function Execution Units |
Total MB-milliseconds from on demand instances while actively executing functions. | `OnDemandFunctionExecutionUnits / 1,024,000` is the On Demand Execution Time meter, in GB-seconds. |
Always Ready Function Execution Units |
Total MB-milliseconds from always ready instances while actively executing functions. | `AlwaysReadyFunctionExecutionUnits / 1,024,000` is the Always Ready Execution Time meter, in GB-seconds. |
Always Ready Units |
The total MB-milliseconds of always ready instances assigned to the app, whether or not functions are actively executing. | `AlwaysReadyUnits / 1,024,000` is the Always Ready Baseline meter, in GB-seconds. |

For more information, see [Azure Functions monitoring data reference](monitor-functions-reference).

To better understand the costs of your functions, use Azure Monitor to view cost-related metrics that your function apps generate. You can view Monitor metrics by using one of these tools:

Use [Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started) to view cost-related data for your Flex Consumption plan function apps in a graphical format.

In the

[Azure portal](https://portal.azure.com), go to your function app.In the left panel, scroll down to

**Monitoring**and select**Metrics**.From

**Metric**, select**On Demand Function Execution Count**and**Sum**for**Aggregation**. This selection adds the sum of the execution counts during the chosen period to the chart.Select

**Add metric**and add**On Demand Function Execution Units**,**Always Ready Function Execution Count**,**Always Ready Function Execution Units**, and**Always Ready Units**to the chart.

The resulting chart contains the totals for all the Flex Consumption execution metrics in the chosen time range, which in this example is a custom time range.

Because the number of On Demand Function Execution Units is greater than On Demand Function Execution Count, and there were no [always ready instances](flex-consumption-plan#always-ready-instances) on the app, the chart just shows On Demand Function Execution Units.

This chart shows a total of 3.54 billion `On Demand Function Execution Units`

consumed in a 16-minute period, measured in MB-milliseconds. To convert to GB-seconds, divide by 1,024,000. In this example, the function app consumed `3,540,000,000 / 1,024,000 = 3,457.03`

GB-seconds. You can take this value and multiply it by the current price of On Demand Execution Time on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/), which gives you the cost of these 16 minutes, assuming you already used any free grants of execution time. You can use this same calculation with the The Always Ready Function Execution Units metric and the Always Ready Execution Time billing meter cost, as well as with the Always Ready Units metric and the Always Ready Baseline billing meter cost, to find out the GB-seconds costs for always ready instances.

To calculate the On Demand Total Executions cost, take the On Demand Function Execution Count sum for the same time period, convert to millions, and then multiply by the On Demand Total Executions price on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/). For example, 2,100 executions in the example above converts to `0.0021`

million executions. You can use this same calculation with the Always Ready Function Execution Count metric and the Always Ready Total Executions billing meter to find out the cost for executions handled by always ready instance.

To learn more about estimating costs for these plans, see [Estimating consumption plan costs](functions-consumption-costs).

### Analyze logs for Azure Functions

Azure Functions writes all logs to the **FunctionAppLogs** table under **LogManagement** in the Log Analytics workspace where you send the data. You can use Kusto queries to query the data.


## Kusto queries

You can analyze monitoring data in the Azure Monitor Logs / Log Analytics store by using the Kusto query language (KQL).

Important

When you select **Logs** from the service's menu in the portal, Log Analytics opens with the query scope set to the current service. This scope means that log queries will only include data from that type of resource. If you want to run a query that includes data from other Azure services, select **Logs** from the **Azure Monitor** menu. See [Log query scope and time range in Azure Monitor Log Analytics](/en-us/azure/azure-monitor/logs/scope) for details.

For a list of common queries for any service, see the [Log Analytics queries interface](/en-us/azure/azure-monitor/logs/queries).

The following sample queries can help you monitor all your functions app logs:

```
FunctionAppLogs
| order by TimeGenerated desc
```


```
FunctionAppLogs
| project TimeGenerated, HostInstanceId, Message, _ResourceId
| order by TimeGenerated desc
```


The following sample query can help you monitor a specific functions app's logs:

```
FunctionAppLogs
| where FunctionName == "<Function name>"
| order by TimeGenerated desc
```


The following sample query can help you monitor exceptions on all your functions app logs:

```
FunctionAppLogs
| where ExceptionDetails != ""
| order by TimeGenerated asc
```


The following sample query can help you monitor exceptions on a specific functions app's logs:

```
FunctionAppLogs
| where ExceptionDetails != ""
| where FunctionName == "<Function name>"
| order by TimeGenerated desc
```


## Alerts

Azure Monitor alerts proactively notify you when specific conditions are found in your monitoring data. Alerts allow you to identify and address issues in your system before your customers notice them. For more information, see [Azure Monitor alerts](/en-us/azure/azure-monitor/alerts/alerts-overview).

There are many sources of common alerts for Azure resources. For examples of common alerts for Azure resources, see [Sample log alert queries](/en-us/azure/azure-monitor/alerts/alerts-log-alert-query-samples). The [Azure Monitor Baseline Alerts (AMBA)](https://aka.ms/amba) site provides a semi-automated method of implementing important platform metric alerts, dashboards, and guidelines. The site applies to a continually expanding subset of Azure services, including all services that are part of the Azure Landing Zone (ALZ).

The common alert schema standardizes the consumption of Azure Monitor alert notifications. For more information, see [Common alert schema](/en-us/azure/azure-monitor/alerts/alerts-common-schema).

### Types of alerts

You can alert on any metric or log data source in the Azure Monitor data platform. There are many different types of alerts depending on the services you're monitoring and the monitoring data you're collecting. Different types of alerts have various benefits and drawbacks. For more information, see [Choose the right monitoring alert type](/en-us/azure/azure-monitor/alerts/alerts-types).

The following list describes the types of Azure Monitor alerts you can create:

[Metric alerts](/en-us/azure/azure-monitor/alerts/alerts-types#metric-alerts)evaluate resource metrics at regular intervals. Metrics can be platform metrics, custom metrics, logs from Azure Monitor converted to metrics, or Application Insights metrics. Metric alerts can also apply multiple conditions and dynamic thresholds.[Log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#log-alerts)allow users to use a Log Analytics query to evaluate resource logs at a predefined frequency.[Activity log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#activity-log-alerts)trigger when a new activity log event occurs that matches defined conditions. Resource Health alerts and Service Health alerts are activity log alerts that report on your service and resource health.

Some Azure services also support [smart detection alerts](/en-us/azure/azure-monitor/alerts/alerts-types#smart-detection-alerts), [Prometheus alerts](/en-us/azure/azure-monitor/alerts/alerts-types#prometheus-alerts), or [recommended alert rules](/en-us/azure/azure-monitor/alerts/alerts-manage-alert-rules#enable-recommended-alert-rules-in-the-azure-portal).

For some services, you can monitor at scale by applying the same metric alert rule to multiple resources of the same type that exist in the same Azure region. Individual notifications are sent for each monitored resource. For supported Azure services and clouds, see [Monitor multiple resources with one alert rule](/en-us/azure/azure-monitor/alerts/alerts-types#monitor-multiple-resources-with-one-alert-rule).

Note

If you're creating or running an application that runs on your service, [Azure Monitor application insights](/en-us/azure/azure-monitor/overview#application-insights) might offer more types of alerts.

### Azure Functions alert rules

The following table lists common and recommended alert rules for Azure Functions. These alerts are just recommendations. You can set alerts for any metric, log entry, or activity log entry listed in the [Monitoring data reference for Azure Functions](monitor-functions-reference).

| Alert type | Condition | Description |
|---|---|---|
| Metric | Average connections | When number of connections exceed a set value |
| Metric | HTTP 404 | When HTTP 404 responses exceed a set value |
| Metric | HTTP Server Errors | When HTTP 5xx errors exceed a set value |
| Activity Log | Create or update function app | When app is created or updated |
| Activity Log | Delete function app | When app is deleted |
| Activity Log | Restart function app | When app is restarted |
| Activity Log | Stop function app | When app is stopped |

### Advisor recommendations

For some services, if critical conditions or imminent changes occur during resource operations, an alert displays on the service **Overview** page in the portal. You can find more information and recommended fixes for the alert in **Advisor recommendations** under **Monitoring** in the left menu. During normal operations, no advisor recommendations display.

For more information on Azure Advisor, see [Azure Advisor overview](/en-us/azure/advisor/advisor-overview).

## Related content

For more information about monitoring Azure Functions, see the following articles:

[Azure Functions monitoring data reference](monitor-functions-reference)provides a reference of the metrics, logs, and other important values available for your function app.[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)gives general details about monitoring Azure resources.[Monitor executions in Azure Functions](functions-monitoring)details how to monitor a function app.[How to configure monitoring for Azure Functions](configure-monitoring)describes how to configure monitoring.[Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data)describes how to view and query the data being collected from a function app.


---

<!-- DOCUMENTO FUSIONADO: _event-driven-scaling__functions-bindings-dapr-trigger-svc-invoke_functions-bind_07a69f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: event-driven-scaling.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/event-driven-scaling -->

# Event-driven scaling in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In the Consumption, Flex Consumption, and Premium plans, Azure Functions scales resources by adding more instances based on the number of events that trigger a function.

The way in which your function app scales depends on the hosting plan:

**Consumption plan:**Each instance of the Functions host in the Consumption plan is limited, typically to 1.5 GB of memory and one CPU. An instance of the host supports the entire function app. As such, all functions within a function app that share resources in an instance are scaled at the same time. When function apps share the same Consumption plan, they're still scaled independently.**Flex Consumption plan:**The plan uses a deterministic per-function scaling strategy. Each function is scaled independently, except for HTTP, Blob, and Durable Functions triggered functions which scale in their own groups. For more information, see[Per-function scaling](#per-function-scaling). These instances are then scaled based on the concurrency of your requests.**Premium plan:**The specific size of the Premium plan determines the available memory and CPU for all apps in that plan on that instance. The plan scales out its instances based on the scaling needs of the apps in the plan, and the apps scale within the plan as needed.

Function code files are stored on Azure Files shares on the function's main storage account. When you delete the main storage account of the function app, the function code files are deleted and can't be recovered.

## Runtime scaling

Azure Functions uses a component called the *scale controller* to monitor the rate of events and determine whether to scale out or scale in. The scale controller uses heuristics for each trigger type. For example, when you're using an Azure Queue storage trigger, it uses [target-based scaling](functions-target-based-scaling).

The unit of scale for Azure Functions is the function app. When the function app is scaled out, more resources are allocated to run multiple instances of the Azure Functions host. Conversely, as compute demand is reduced, the scale controller removes function host instances. The number of instances is eventually "scaled in" when no functions are running within a function app.


## Cold Start

Should your function app become idle for a few minutes, the platform might decide to scale the number of instances on which your app runs down to zero. The next request has the added latency of scaling from zero to one. This latency is referred to as a *cold start*. The number of dependencies required by your function app can affect the cold start time. Cold start is more of an issue for synchronous operations, such as HTTP triggers that must return a response. If cold starts are impacting your functions, consider using a plan other than the Consumption. The other plans offer these strategies to mitigate or eliminate cold starts:

[Premium plan](functions-premium-plan#eliminate-cold-starts): supports both prewarmed instances and always ready instances, with a minimum of one instance.[Flex Consumption plan](flex-consumption-plan#always-ready-instances): supports an optional number of always ready instances, which can be defined on a per instance scaling basis.[Dedicated plan](dedicated-plan#always-on): the plan itself doesn't scale dynamically, but you can run your app continuously when the**Always on**setting is enabled.

## Understanding scaling behaviors

Scaling can vary based on several factors, and apps scale differently based on the triggers and language selected. There are a few intricacies of scaling behaviors to be aware of:

**Maximum instances:**A single function app only scales out to a[maximum allowed by the plan](functions-scale#scale). However, a single instance[can process more than one message or request at a time](functions-concurrency#concurrency-in-azure-functions). You can[specify a lower maximum](#limit-scale-out)to throttle scale as required.**New instance rate:**For HTTP triggers, new instances are allocated, at most, once per second. For non-HTTP triggers, new instances are allocated, at most, once every 30 seconds. Scaling is faster when running in a[Premium plan](functions-premium-plan).**Target-based scaling:**Target-based scaling provides a fast and intuitive scaling model for customers. Currently, this scaling method is supported for Service Bus queues and topics, Storage queues, Event Hubs, Apache Kafka, and Azure Cosmos DB extensions. Make sure to review[target-based scaling](functions-target-based-scaling)to understand their scaling behavior.**Per-function scaling:**With some notable exceptions, functions running in the Flex Consumption plan scale on independent instances. The exceptions include HTTP triggers and Blob storage (Event Grid) triggers. Each of these trigger types scale together as a group on the same instances. Likewise, the triggers of all Durable Functions also share instances and scale together. For more information, see[per-function scaling](#per-function-scaling).**Maximum monitored triggers:**Currently, the scale controller can only monitor up to 100 triggers to making scaling decisions. When your app has more than 100 event-based triggers, scale decisions are made based on only the first 100 triggers that execute. For more information, see[Best practices and patterns for scalable apps](#best-practices-and-patterns-for-scalable-apps).

## Limit scale-out

You might decide to restrict the maximum number of instances an app can use for scale-out. This limitation is most common for cases where a downstream component like a database has limited throughput. For the maximum scale limits when running the various hosting plans, see [Scale limits](functions-scale#scale).

### Flex Consumption plan

By default, apps running in a Flex Consumption plan have limit of `100`

overall instances. Currently the lowest maximum instance count value is `40`

, and the highest supported maximum instance count value is `1000`

. When you use the [ az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create) command to create a function app in the Flex Consumption plan, use the

`--maximum-instance-count`

parameter to set this maximum instance count for of your app.While you can change the maximum instance count of Flex Consumption apps up to 1000, the quota limit for your apps is reached before reaching that number. Review [Regional subscription memory quotas](flex-consumption-plan#regional-subscription-memory-quotas) for more details.

This example creates an app with a maximum instance count of `200`

:

```
az functionapp create --resource-group <RESOURCE_GROUP> --name <APP_NAME> --storage <STORAGE_ACCOUNT_NAME> --runtime <LANGUAGE_RUNTIME> --runtime-version <RUNTIME_VERSION> --flexconsumption-location <REGION> --maximum-instance-count 200
```


This example uses the [ az functionapp scale config set](/en-us/cli/azure/functionapp/scale/config#az-functionapp-scale-config-set) command to change the maximum instance count for an existing app to

`150`

:```
az functionapp scale config set --resource-group <RESOURCE_GROUP> --name <APP_NAME> --maximum-instance-count 150
```


### Consumption/Premium plans

In a Consumption or Elastic Premium plan, you can specify a lower maximum limit for your app by modifying the value of the `functionAppScaleLimit`

site configuration setting. The `functionAppScaleLimit`

can be set to `0`

or `null`

for unrestricted, or a valid value between `1`

and the app maximum.

```
az resource update --resource-type Microsoft.Web/sites -g <RESOURCE_GROUP> -n <FUNCTION_APP-NAME>/config/web --set properties.functionAppScaleLimit=<SCALE_LIMIT>
```


## Scale-in behaviors

Event-driven scaling automatically reduces capacity when demand for your functions is reduced. It makes this reduction by draining instances of their current function executions and then removes those instances. This behavior is logged as drain mode. The grace period for functions that are currently executing can extend up to 10 minutes for Consumption plan apps and up to 60 minutes for Flex Consumption and Premium plan apps. Event-driven scaling and this behavior don't apply to Dedicated plan apps.

The following considerations apply for scale-in behaviors:

- For apps running on Windows in a Consumption plan, only apps created after May 2021 have drain mode behaviors enabled by default.
- To enable graceful shutdown for functions using the Service Bus trigger, use version 4.2.0 or a later version of the
[Service Bus Extension](functions-bindings-service-bus).

## Per-function scaling

*Applies only to the Flex Consumption plan*.

The [Flex Consumption plan](flex-consumption-plan) is unique in that it implements a *per-function scaling* behavior. In per-function scaling, except for HTTP triggers, Blob (Event Grid) triggers, and Durable Functions, all other function trigger types in your app scale on independent instances. HTTP triggers in your app all scale together as a group on the same instances, as do all Blob (Event Grid), and all Durable Functions triggers, which have their own shared instances.

Consider a function app hosted by a Flex Consumption plan that has the following functions:

| function1 | function2 | function3 | function4 | function5 | function6 | function7 |
|---|---|---|---|---|---|---|
| HTTP trigger | HTTP trigger | Orchestration trigger (Durable) | Activity trigger (Durable) | Service Bus trigger | Service Bus trigger | Event Hubs trigger |

In this example:

- The two HTTP triggered functions (
`function1`

and`function2`

) both run together on their own instances and scale together according to[HTTP concurrency settings](flex-consumption-how-to#set-http-concurrency-limits). - The two Durable functions (
`function3`

and`function4`

) both run together on their own instances and scale together based on[configured concurrency throttles](durable/durable-functions-perf-and-scale#concurrency-throttles). - The Service bus triggered function
`function5`

runs in its own and is scaled independently according to the[target-based scaling rules for Service Bus queues and topics](functions-target-based-scaling#service-bus-queues-and-topics). - The Service bus triggered function
`function6`

runs in its own and is scaled independently according to the[target-based scaling rules for Service Bus queues and topics](functions-target-based-scaling#service-bus-queues-and-topics). - The Event Hubs trigger (
`function7`

) runs in its own instances and is scaled independently according to the[target-based scaling rules for Event Hubs](functions-target-based-scaling#event-hubs).

## Best practices and patterns for scalable apps

There are many aspects of a function app that impacts how it scales, including host configuration, runtime footprint, and resource efficiency. For more information, see the [scalability section of the performance considerations article](performance-reliability#scalability-best-practices). You should also be aware of how connections behave as your function app scales. For more information, see [How to manage connections in Azure Functions](manage-connections).

If your app has more than 100 functions that use event-based triggers, consider breaking the app into one or more apps, where each app has less than 100 event-based functions.

For more information on scaling in Python and Node.js, see the **Scaling and performance** section of the [Azure Functions Python developer guide](functions-reference-python) and the **Scaling and concurrency** section of the [Azure Functions Node.js developer guide](functions-reference-node).

## Next steps

To learn more, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-dapr-trigger-svc-invoke_functions-bindings-dapr-input-state.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-dapr-trigger-svc-invoke.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-trigger-svc-invoke -->

# Dapr Service Invocation trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions can be triggered on a Dapr service invocation using the following Dapr events.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("CreateNewOrder")]
public static void Run(
[DaprServiceInvocationTrigger] JObject payload,
[DaprState("%StateStoreName%", Key = "order")] out JToken order,
ILogger log)
{
log.LogInformation("C# function processed a CreateNewOrder request from the Dapr Runtime.");
// payload must be of the format { "data": { "value": "some value" } }
order = payload["data"];
}
```


Here's the Java code for the Dapr Service Invocation trigger:

```
@FunctionName("CreateNewOrder")
public String run(
@DaprServiceInvocationTrigger(
methodName = "CreateNewOrder")
)
```


Use the `app`

object to register the `daprInvokeOutput`

:

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

Here's the *function.json* file for `daprServiceInvocationTrigger`

:

```
{
"bindings": [
{
"type": "daprServiceInvocationTrigger",
"name": "payload",
"direction": "in"
}
]
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
param (
$payload
)
# C# function processed a CreateNewOrder request from the Dapr Runtime.
Write-Host "PowerShell function processed a CreateNewOrder request from the Dapr Runtime."
# Payload must be of the format { "data": { "value": "some value" } }
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $payload| ConvertTo-Json
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name order -Value $payload["data"]
```


The following example shows a Dapr Service Invocation trigger, which uses the [v2 Python programming model](functions-reference-python). To use the `daprServiceInvocationTrigger`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="RetrieveOrder")
@app.dapr_service_invocation_trigger(arg_name="payload", method_name="RetrieveOrder")
@app.dapr_state_input(arg_name="data", state_store="statestore", key="order")
def main(payload, data: str) :
# Function should be invoked with this command: dapr invoke --app-id functionapp --method RetrieveOrder --data '{}'
logging.info('Python function processed a RetrieveOrder request from the Dapr Runtime.')
logging.info(data)
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprServiceInvocationTrigger`

to trigger a Dapr service invocation binding, which supports the following properties.

| Parameter | Description |
|---|---|
MethodName |
Optional. The name of the method the Dapr caller should use. If not specified, the name of the function is used as the method name. |

## Annotations

The `DaprServiceInvocationTrigger`

annotation allows you to create a function that gets invoked by Dapr runtime.

| Element | Description |
|---|---|
methodName |
The method name. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
type |
Must be set to `daprServiceInvocationTrigger` . |
name |
The name of the variable that represents the Dapr data in function code. |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
type |
Must be set to `daprServiceInvocationTrigger` . |
name |
The name of the variable that represents the Dapr data in function code. |

See the [Example section](#example) for complete examples.

## Usage

To use a Dapr Service Invocation trigger, learn more about which components to use with the Service Invocation trigger and how to set them up in the official Dapr documentation.

To use the `daprServiceInvocationTrigger`

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

<!-- DOCUMENTO FUSIONADO: functions-bindings-dapr-input-state.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-input-state -->

# Dapr State input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr state input binding allows you to read Dapr state during a function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("StateInputBinding")]
public static IActionResult Run(
[HttpTrigger(AuthorizationLevel.Function, "get", Route = "state/{key}")] HttpRequest req,
[DaprState("statestore", Key = "{key}")] string state,
ILogger log)
{
log.LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult(state);
}
```


The following example creates a `"RetrieveOrder"`

function using the `DaprStateInput`

binding with the [ DaprServiceInvocationTrigger](functions-bindings-dapr-trigger-svc-invoke):

```
@FunctionName("RetrieveOrder")
public String run(
@DaprServiceInvocationTrigger(
methodName = "RetrieveOrder")
String payload,
@DaprStateInput(
stateStore = "%StateStoreName%",
key = "order")
String product,
final ExecutionContext context)
```


In the following example, the Dapr invoke input binding is added as an `extraInput`

and paired with an HTTP trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('StateInputBinding', {
trigger: trigger.generic({
type: 'httpTrigger',
authLevel: 'anonymous',
methods: ['GET'],
route: "state/{key}",
name: "req"
}),
extraInputs: [daprStateInput],
handler: async (request, context) => {
context.log("Node HTTP trigger function processed a request.");
const daprStateInputValue = context.extraInputs.get(daprStateInput);
// print the fetched state value
context.log(daprStateInputValue);
return daprStateInputValue;
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprState`

:

```
{
"bindings":
{
"type": "daprState",
"direction": "in",
"key": "order",
"stateStore": "%StateStoreName%",
"name": "order"
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
param (
$payload, $order
)
# C# function processed a CreateNewOrder request from the Dapr Runtime.
Write-Host "PowerShell function processed a RetrieveOrder request from the Dapr Runtime."
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $order | ConvertTo-Json
Write-Host "$jsonString"
```


The following example shows a Dapr State input binding, which uses the [v2 Python programming model](functions-reference-python). To use the `daprState`

binding alongside the `daprServiceInvocationTrigger`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="RetrieveOrder")
@app.dapr_service_invocation_trigger(arg_name="payload", method_name="RetrieveOrder")
@app.dapr_state_input(arg_name="data", state_store="statestore", key="order")
def main(payload, data: str) :
# Function should be invoked with this command: dapr invoke --app-id functionapp --method RetrieveOrder --data '{}'
logging.info('Python function processed a RetrieveOrder request from the Dapr Runtime.')
logging.info(data)
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprState`

to read Dapr state into your function, which supports these parameters:

| Parameter | Description |
|---|---|
StateStore |
The name of the state store to retrieve state. |
Key |
The name of the key to retrieve from the specified state store. |

## Annotations

The `DaprStateInput`

annotation allows you to read Dapr state into your function.

| Element | Description |
|---|---|
stateStore |
The name of the Dapr state store. |
key |
The state store key value. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
stateStore |
The name of the state store. |
key |
The name of the key to retrieve from the specified state store. |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
key |
The name of the key to retrieve from the specified state store. |
stateStore |
The name of the state store. |

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr state input binding, start by setting up a Dapr state store component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprState`

in Python v2, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`
