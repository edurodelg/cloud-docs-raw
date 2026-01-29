---
merged_at: 2026-01-29T15:49:53.269257
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob-output -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-monitor-log-analytics -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/develop-python-worker-extensions -->

# Develop Python worker extensions for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

Starting with Python 3.13, python worker extensions will no longer be supported.

Azure Functions lets you integrate custom behaviors as part of Python function execution. This feature enables you to create business logic that customers can easily use in their own function apps. Worker extensions are supported in both the v1 and v2 Python programming models.

In this tutorial, you'll learn how to:

- Create an application-level Python worker extension for Azure Functions.
- Consume your extension in an app the way your customers do.
- Package and publish an extension for consumption.

## Prerequisites

Before you start, you must meet these requirements:

[Python 3.7 or above](https://www.python.org/downloads). To check the full list of supported Python versions in Azure Functions, see the[Python developer guide](functions-reference-python#supported-python-versions).The

[Azure Functions Core Tools](functions-run-local#v2), version 4.0.5095 or later, which supports using the extension with the[v2 Python programming model](functions-reference-python). Check your version with`func --version`

.[Visual Studio Code](https://code.visualstudio.com/)installed on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).

## Create the Python Worker extension

The extension you create reports the elapsed time of an HTTP trigger invocation in the console logs and in the HTTP response body.

### Folder structure

The folder for your extension project should be like the following structure:

```
<python_worker_extension_root>/
| - .venv/
| - python_worker_extension_timer/
| | - __init__.py
| - setup.py
| - readme.md
```


| Folder/file | Description |
|---|---|
.venv/ |
(Optional) Contains a Python virtual environment used for local development. |
python_worker_extension/ |
Contains the source code of the Python worker extension. This folder contains the main Python module to be published into PyPI. |
setup.py |
Contains the metadata of the Python worker extension package. |
readme.md |
Contains the instruction and usage of your extension. This content is displayed as the description in the home page in your PyPI project. |

### Configure project metadata

First you create `setup.py`

, which provides essential information about your package. To make sure that your extension is distributed and integrated into your customer's function apps properly, confirm that `'azure-functions >= 1.7.0, < 2.0.0'`

is in the `install_requires`

section.

In the following template, you should change `author`

, `author_email`

, `install_requires`

, `license`

, `packages`

, and `url`

fields as needed.

```
from setuptools import find_packages, setup
setup(
name='python-worker-extension-timer',
version='1.0.0',
author='Your Name Here',
author_email='your@email.here',
classifiers=[
'Intended Audience :: End Users/Desktop',
'Development Status :: 5 - Production/Stable',
'Intended Audience :: End Users/Desktop',
'License :: OSI Approved :: Apache Software License',
'Programming Language :: Python',
'Programming Language :: Python :: 3.7',
'Programming Language :: Python :: 3.8',
'Programming Language :: Python :: 3.9',
'Programming Language :: Python :: 3.10',
],
description='Python Worker Extension Demo',
include_package_data=True,
long_description=open('readme.md').read(),
install_requires=[
'azure-functions >= 1.7.0, < 2.0.0',
# Any additional packages that will be used in your extension
],
extras_require={},
license='MIT',
packages=find_packages(where='.'),
url='https://your-github-or-pypi-link',
zip_safe=False,
)
```


Next, you'll implement your extension code in the application-level scope.

### Implement the timer extension

Add the following code in `python_worker_extension_timer/__init__.py`

to implement the application-level extension:

```
import typing
from logging import Logger
from time import time
from azure.functions import AppExtensionBase, Context, HttpResponse
class TimerExtension(AppExtensionBase):
"""A Python worker extension to record elapsed time in a function invocation
"""
@classmethod
def init(cls):
# This records the starttime of each function
cls.start_timestamps: typing.Dict[str, float] = {}
@classmethod
def configure(cls, *args, append_to_http_response:bool=False, **kwargs):
# Customer can use TimerExtension.configure(append_to_http_response=)
# to decide whether the elapsed time should be shown in HTTP response
cls.append_to_http_response = append_to_http_response
@classmethod
def pre_invocation_app_level(
cls, logger: Logger, context: Context,
func_args: typing.Dict[str, object],
*args, **kwargs
) -> None:
logger.info(f'Recording start time of {context.function_name}')
cls.start_timestamps[context.invocation_id] = time()
@classmethod
def post_invocation_app_level(
cls, logger: Logger, context: Context,
func_args: typing.Dict[str, object],
func_ret: typing.Optional[object],
*args, **kwargs
) -> None:
if context.invocation_id in cls.start_timestamps:
# Get the start_time of the invocation
start_time: float = cls.start_timestamps.pop(context.invocation_id)
end_time: float = time()
# Calculate the elapsed time
elapsed_time = end_time - start_time
logger.info(f'Time taken to execute {context.function_name} is {elapsed_time} sec')
# Append the elapsed time to the end of HTTP response
# if the append_to_http_response is set to True
if cls.append_to_http_response and isinstance(func_ret, HttpResponse):
func_ret._HttpResponse__body += f' (TimeElapsed: {elapsed_time} sec)'.encode()
```


This code inherits from [AppExtensionBase](https://github.com/Azure/azure-functions-python-library/blob/dev/azure/functions/extension/app_extension_base.py) so that the extension applies to every function in the app. You could have also implemented the extension on a function-level scope by inheriting from [FuncExtensionBase](https://github.com/Azure/azure-functions-python-library/blob/dev/azure/functions/extension/func_extension_base.py).

The `init`

method is a class method that's called by the worker when the extension class is imported. You can do initialization actions here for the extension. In this case, a hash map is initialized for recording the invocation start time for each function.

The `configure`

method is customer-facing. In your readme file, you can tell your customers when they need to call `Extension.configure()`

. The readme should also document the extension capabilities, possible configuration, and usage of your extension. In this example, customers can choose whether the elapsed time is reported in the `HttpResponse`

.

The `pre_invocation_app_level`

method is called by the Python worker before the function runs. It provides the information from the function, such as function context and arguments. In this example, the extension logs a message and records the start time of an invocation based on its invocation_id.

Similarly, the `post_invocation_app_level`

is called after function execution. This example calculates the elapsed time based on the start time and current time. It also overwrites the return value of the HTTP response.

### Create a readme.md

Create a readme.md file in the root of your extension project. This file contains the instructions and usage of your extension. The readme.md content is displayed as the description in the home page in your PyPI project.

```
# Python Worker Extension Timer
In this file, tell your customers when they need to call `Extension.configure()`.
The readme should also document the extension capabilities, possible configuration,
and usage of your extension.
```


## Consume your extension locally

Now that you've created an extension, you can use it in an app project to verify it works as intended.

### Create an HTTP trigger function

Create a new folder for your app project and navigate to it.

From the appropriate shell, such as Bash, run the following command to initialize the project:

`func init --python`

Use the following command to create a new HTTP trigger function that allows anonymous access:

`func new -t HttpTrigger -n HttpTrigger -a anonymous`


### Activate a virtual environment

Create a Python virtual environment, based on OS as follows:

Activate the Python virtual environment, based on OS as follows:


### Configure the extension

Install remote packages for your function app project using the following command:

`pip install -r requirements.txt`

Install the extension from your local file path, in editable mode as follows:

`pip install -e <PYTHON_WORKER_EXTENSION_ROOT>`

In this example, replace

`<PYTHON_WORKER_EXTENSION_ROOT>`

with the root file location of your extension project.When a customer uses your extension, they'll instead add your extension package location to the requirements.txt file, as in the following examples:

Open the local.settings.json project file and add the following field to

`Values`

:`"PYTHON_ENABLE_WORKER_EXTENSIONS": "1"`

When running in Azure, you instead add

`PYTHON_ENABLE_WORKER_EXTENSIONS=1`

to the[app settings in the function app](functions-how-to-use-azure-function-app-settings#settings).Add following two lines before the

`main`

function in*__init.py__*file for the v1 programming model, or in the*function_app.py*file for the v2 programming model:`from python_worker_extension_timer import TimerExtension TimerExtension.configure(append_to_http_response=True)`

This code imports the

`TimerExtension`

module and sets the`append_to_http_response`

configuration value.

### Verify the extension

From your app project root folder, start the function host using

`func host start --verbose`

. You should see the local endpoint of your function in the output as`https://localhost:7071/api/HttpTrigger`

.In the browser, send a GET request to

`https://localhost:7071/api/HttpTrigger`

. You should see a response like the following, with the**TimeElapsed**data for the request appended.`This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response. (TimeElapsed: 0.0009996891021728516 sec)`


## Publish your extension

After you've created and verified your extension, you still need to complete these remaining publishing tasks:

- Choose a license.
- Create a readme.md and other documentation.
- Publish the extension library to a Python package registry or a version control system (VCS).

To publish your extension to PyPI:

Run the following command to install

`twine`

and`wheel`

in your default Python environment or a virtual environment:`pip install twine wheel`

Remove the old

`dist/`

folder from your extension repository.Run the following command to generate a new package inside

`dist/`

:`python setup.py sdist bdist_wheel`

Run the following command to upload the package to PyPI:

`twine upload dist/*`

You may need to provide your PyPI account credentials during upload. You can also test your package upload with

`twine upload -r testpypi dist/*`

. For more information, see the[Twine documentation](https://twine.readthedocs.io/en/stable/).

After these steps, customers can use your extension by including your package name in their requirements.txt.

For more information, see the [official Python packaging tutorial](https://packaging.python.org/tutorials/packaging-projects/).

## Examples

You can view completed sample extension project from this article in the

[python_worker_extension_timer](https://github.com/Azure-Samples/python-worker-extension-timer)sample repository.OpenCensus integration is an open-source project that uses the extension interface to integrate telemetry tracing in Azure Functions Python apps. See the

[opencensus-python-extensions-azure](https://github.com/census-ecosystem/opencensus-python-extensions-azure/tree/main/extensions/functions)repository to review the implementation of this Python worker extension.

## Next steps

For more information about Azure Functions Python development, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistantcreate-output -->

# Azure OpenAI assistant create output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI assistant create output binding allows you to create a new assistant chat bot from your function code execution.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI assistants, see [Azure OpenAI Assistants API](/en-us/azure/ai-services/openai/concepts/assistants).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
/// <summary>
/// HTTP PUT function that creates a new assistant chat bot with the specified ID.
/// </summary>
[Function(nameof(CreateAssistant))]
public static async Task<CreateChatBotOutput> CreateAssistant(
[HttpTrigger(AuthorizationLevel.Anonymous, "put", Route = "assistants/{assistantId}")] HttpRequestData req,
string assistantId)
{
string instructions =
"""
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
""";
using StreamReader reader = new(req.Body);
string request = await reader.ReadToEndAsync();
return new CreateChatBotOutput
{
HttpResponse = new ObjectResult(new { assistantId }) { StatusCode = 201 },
ChatBotCreateRequest = new AssistantCreateRequest(assistantId, instructions)
{
ChatStorageConnectionSetting = DefaultChatStorageConnectionSetting,
CollectionName = DefaultCollectionName,
},
};
}
public class CreateChatBotOutput
{
[AssistantCreateOutput()]
public AssistantCreateRequest? ChatBotCreateRequest { get; set; }
[HttpResult]
public IActionResult? HttpResponse { get; set; }
}
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
/**
* The default storage account setting for the table storage account.
* This constant is used to specify the connection string for the table storage
* account
* where chat data will be stored.
*/
final String DEFAULT_CHATSTORAGE = "AzureWebJobsStorage";
/**
* The default collection name for the table storage account.
* This constant is used to specify the collection name for the table storage
* account
* where chat data will be stored.
*/
final String DEFAULT_COLLECTION = "ChatState";
/*
* HTTP PUT function that creates a new assistant chat bot with the specified ID.
*/
@FunctionName("CreateAssistant")
public HttpResponseMessage createAssistant(
@HttpTrigger(
name = "req",
methods = {HttpMethod.PUT},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "assistants/{assistantId}")
HttpRequestMessage<Optional<String>> request,
@BindingName("assistantId") String assistantId,
@AssistantCreate(name = "AssistantCreate") OutputBinding<AssistantCreateRequest> message,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String instructions = "Don't make assumptions about what values to plug into functions.\n" +
"Ask for clarification if a user request is ambiguous.";
AssistantCreateRequest assistantCreateRequest = new AssistantCreateRequest(assistantId, instructions);
assistantCreateRequest.setChatStorageConnectionSetting(DEFAULT_CHATSTORAGE);
assistantCreateRequest.setCollectionName(DEFAULT_COLLECTION);
message.setValue(assistantCreateRequest);
JSONObject response = new JSONObject();
response.put("assistantId", assistantId);
return request.createResponseBuilder(HttpStatus.CREATED)
.header("Content-Type", "application/json")
.body(response.toString())
.build();
}
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
const { app, input, output } = require("@azure/functions");
const CHAT_STORAGE_CONNECTION_SETTING = "AzureWebJobsStorage";
const COLLECTION_NAME = "ChatState";
const chatBotCreateOutput = output.generic({
type: 'assistantCreate'
})
app.http('CreateAssistant', {
methods: ['PUT'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraOutputs: [chatBotCreateOutput],
handler: async (request, context) => {
const assistantId = request.params.assistantId
const instructions =
`
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
`
const createRequest = {
id: assistantId,
instructions: instructions,
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
}
context.extraOutputs.set(chatBotCreateOutput, createRequest)
return { status: 202, jsonBody: { assistantId: assistantId } }
}
})
```


```
import { HttpRequest, InvocationContext, app, input, output } from "@azure/functions"
const CHAT_STORAGE_CONNECTION_SETTING = "AzureWebJobsStorage";
const COLLECTION_NAME = "ChatState";
const chatBotCreateOutput = output.generic({
type: 'assistantCreate'
})
app.http('CreateAssistant', {
methods: ['PUT'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraOutputs: [chatBotCreateOutput],
handler: async (request: HttpRequest, context: InvocationContext) => {
const assistantId = request.params.assistantId
const instructions =
`
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
`
const createRequest = {
id: assistantId,
instructions: instructions,
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
}
context.extraOutputs.set(chatBotCreateOutput, createRequest)
return { status: 202, jsonBody: { assistantId: assistantId } }
}
})
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

Here's the *function.json* file for Create Assistant:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"route": "assistants/{assistantId}",
"methods": [
"put"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"type": "assistantCreate",
"direction": "out",
"dataType": "string",
"name": "Requests"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

{{This comes from the example code comment}}

```
using namespace System.Net
param($Request, $TriggerMetadata)
$assistantId = $Request.params.assistantId
$instructions = "Don't make assumptions about what values to plug into functions."
$instructions += "\nAsk for clarification if a user request is ambiguous."
$create_request = @{
"id" = $assistantId
"instructions" = $instructions
"chatStorageConnectionSetting" = "AzureWebJobsStorage"
"collectionName" = "ChatState"
}
Push-OutputBinding -Name Requests -Value (ConvertTo-Json $create_request)
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::Accepted
Body = (ConvertTo-Json @{ "assistantId" = $assistantId})
Headers = @{
"Content-Type" = "application/json"
}
})
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
DEFAULT_CHAT_STORAGE_SETTING = "AzureWebJobsStorage"
DEFAULT_CHAT_COLLECTION_NAME = "ChatState"
@apis.function_name("CreateAssistant")
@apis.route(route="assistants/{assistantId}", methods=["PUT"])
@apis.assistant_create_output(arg_name="requests")
def create_assistant(
req: func.HttpRequest, requests: func.Out[str]
) -> func.HttpResponse:
assistantId = req.route_params.get("assistantId")
instructions = """
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
"""
create_request = {
"id": assistantId,
"instructions": instructions,
"chatStorageConnectionSetting": DEFAULT_CHAT_STORAGE_SETTING,
"collectionName": DEFAULT_CHAT_COLLECTION_NAME,
}
requests.set(json.dumps(create_request))
response_json = {"assistantId": assistantId}
return func.HttpResponse(
json.dumps(response_json), status_code=202, mimetype="application/json"
)
```


## Attributes

Apply the `CreateAssistant`

attribute to define an assistant create output binding, which supports these parameters:

| Parameter | Description |
|---|---|
Id |
The identifier of the assistant to create. |
Instructions |
Optional. The instructions that are provided to assistant to follow. |
ChatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
CollectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Annotations

The `CreateAssistant`

annotation enables you to define an assistant create output binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the output binding. |
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Decorators

During the preview, define the output binding as a `generic_output_binding`

binding of type `createAssistant`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chat_storage_connection_setting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collection_name |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `CreateAssistant` . |
direction |
Must be `out` . |
name |
The name of the output binding. |
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Usage

See the [Example section](#example) for complete examples.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-queue-trigger -->

# Azure Queue storage trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The queue storage trigger runs a function as messages are added to Azure Queue storage.

Azure Queue storage scaling decisions for the Consumption and Premium plans are done via target-based scaling. For more information, see [Target-based scaling](functions-target-based-scaling).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

Use the queue trigger to start a function when a new item is received on a queue. The queue message is provided as input to the function.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a [C# function](dotnet-isolated-process-guide) that polls the `input-queue`

queue and writes several messages to an output queue each time a queue item is processed.

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


The following Java example shows a storage queue trigger function, which logs the triggered message placed into queue `myqueuename`

.

```
@FunctionName("queueprocessor")
public void run(
@QueueTrigger(name = "msg",
queueName = "myqueuename",
connection = "myconnvarname") String message,
final ExecutionContext context
) {
context.getLogger().info(message);
}
```


The following example shows a queue trigger [TypeScript function](functions-reference-node?tabs=typescript). The function polls the `myqueue-items`

queue and writes a log each time a queue item is processed.

```
import { app, InvocationContext } from '@azure/functions';
export async function storageQueueTrigger1(queueItem: unknown, context: InvocationContext): Promise<void> {
context.log('Storage queue function processed work item:', queueItem);
context.log('expirationTime =', context.triggerMetadata.expirationTime);
context.log('insertionTime =', context.triggerMetadata.insertionTime);
context.log('nextVisibleTime =', context.triggerMetadata.nextVisibleTime);
context.log('id =', context.triggerMetadata.id);
context.log('popReceipt =', context.triggerMetadata.popReceipt);
context.log('dequeueCount =', context.triggerMetadata.dequeueCount);
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
handler: storageQueueTrigger1,
});
```


The [usage](#usage) section explains `queueItem`

. The [message metadata section](#message-metadata) explains all of the other variables shown.

The following example shows a queue trigger [JavaScript function](functions-reference-node). The function polls the `myqueue-items`

queue and writes a log each time a queue item is processed.

```
const { app } = require('@azure/functions');
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
handler: (queueItem, context) => {
context.log('Storage queue function processed work item:', queueItem);
context.log('expirationTime =', context.triggerMetadata.expirationTime);
context.log('insertionTime =', context.triggerMetadata.insertionTime);
context.log('nextVisibleTime =', context.triggerMetadata.nextVisibleTime);
context.log('id =', context.triggerMetadata.id);
context.log('popReceipt =', context.triggerMetadata.popReceipt);
context.log('dequeueCount =', context.triggerMetadata.dequeueCount);
},
});
```


The [usage](#usage) section explains `queueItem`

. The [message metadata section](#message-metadata) explains all of the other variables shown.

The following example demonstrates how to read a queue message passed to a function via a trigger.

A Storage queue trigger is defined in *function.json* file where `type`

is set to `queueTrigger`

.

```
{
"bindings": [
{
"name": "QueueItem",
"type": "queueTrigger",
"direction": "in",
"queueName": "messages",
"connection": "MyStorageConnectionAppSetting"
}
]
}
```


The code in the *Run.ps1* file declares a parameter as `$QueueItem`

, which allows you to read the queue message in your function.

```
# Input bindings are passed in via param block.
param([string] $QueueItem, $TriggerMetadata)
# Write out the queue message and metadata to the information log.
Write-Host "PowerShell queue trigger function processed work item: $QueueItem"
Write-Host "Queue item expiration time: $($TriggerMetadata.ExpirationTime)"
Write-Host "Queue item insertion time: $($TriggerMetadata.InsertionTime)"
Write-Host "Queue item next visible time: $($TriggerMetadata.NextVisibleTime)"
Write-Host "ID: $($TriggerMetadata.Id)"
Write-Host "Pop receipt: $($TriggerMetadata.PopReceipt)"
Write-Host "Dequeue count: $($TriggerMetadata.DequeueCount)"
```


The following example demonstrates how to read a queue message passed to a function via a trigger. The example depends on whether you use the v1 or v2 Python programming model.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="QueueFunc")
@app.queue_trigger(arg_name="msg", queue_name="inputqueue",
connection="storageAccountConnectionString") # Queue trigger
@app.queue_output(arg_name="outputQueueItem", queue_name="outqueue",
connection="storageAccountConnectionString") # Queue output binding
def test_function(msg: func.QueueMessage,
outputQueueItem: func.Out[str]) -> None:
logging.info('Python queue trigger function processed a queue item: %s',
msg.get_body().decode('utf-8'))
outputQueueItem.set('hello')
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the [QueueTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Extensions.Storage/Queues/QueueTriggerAttribute.cs) to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#queue-trigger).

In [C# class libraries](dotnet-isolated-process-guide), the attribute's constructor takes the name of the queue to monitor, as shown in the following example:

```
[Function(nameof(QueueInputOutputFunction))]
[QueueOutput("output-queue")]
public string[] QueueInputOutputFunction([QueueTrigger("input-queue")] Album myQueueItem, FunctionContext context)
```


This example also demonstrates setting the [connection string setting](#connections) in the attribute itself.

## Annotations

The `QueueTrigger`

annotation gives you access to the queue that triggers the function. The following example makes the queue message available to the function via the `message`

parameter.

```
package com.function;
import com.microsoft.azure.functions.annotation.*;
import java.util.Queue;
import com.microsoft.azure.functions.*;
public class QueueTriggerDemo {
@FunctionName("QueueTriggerDemo")
public void run(
@QueueTrigger(name = "message", queueName = "messages", connection = "MyStorageConnectionAppSetting") String message,
final ExecutionContext context
) {
context.getLogger().info("Queue message: " + message);
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

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using decorators, the following properties on the `queue_trigger`

decorator define the Queue Storage trigger:

| Property | Description |
|---|---|
`arg_name` |
Declares the parameter name in the function signature. When the function is triggered, this parameter's value has the contents of the queue message. |
`queue_name` |
Declares the queue name in the storage account. |
`connection` |
Points to the storage account connection string. |

For Python functions defined by using function.json, see the Configuration section.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.storageQueue()`

method.

| Property | Description |
|---|---|
queueName |
The name of the queue to poll. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Queues. See
|

The following table explains the binding configuration properties that you set in the *function.json* file and the `QueueTrigger`

attribute.

| function.json property | Description |
|---|---|
type |
Must be set to `queueTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
In the function.json file only. Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that contains the queue item payload in the function code. |
queueName |
The name of the queue to poll. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Queues. See
|

See the [Example section](#example) for complete examples.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

Note

Functions expect a *base64* encoded string. Any adjustments to the encoding type (in order to prepare data as a *base64* encoded string) need to be implemented in the calling service.

The usage of the Queue trigger depends on the extension package version, and the C# modality used in your function app, which can be one of these modes:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see usage details for the mode and version.

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

The [QueueTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.queuetrigger) annotation gives you access to the queue message that triggered the function.

Access the queue message via string parameter that matches the name designated by binding's `name`

parameter in the *function.json* file.

Access the queue message via the parameter typed as [QueueMessage](/en-us/python/api/azure-functions/azure.functions.queuemessage).

## Metadata

The queue trigger provides several [metadata properties](functions-bindings-expressions-patterns#trigger-metadata). These properties can be used as part of binding expressions in other bindings or as parameters in your code, for language workers that provide this access to message metadata.

The message metadata properties are members of the [CloudQueueMessage](/en-us/dotnet/api/microsoft.azure.storage.queue.cloudqueuemessage) class.

The message metadata properties can be accessed from `context.triggerMetadata`

.

The message metadata properties can be accessed from the passed `$TriggerMetadata`

parameter.

| Property | Type | Description |
|---|---|---|
`QueueTrigger` |
`string` |
Queue payload (if a valid string). If the queue message payload is a string, `QueueTrigger` has the same value as the variable named by the `name` property in function.json. |
`DequeueCount` |
`long` |
The number of times this message has been dequeued. |
`ExpirationTime` |
`DateTimeOffset` |
The time that the message expires. |
`Id` |
`string` |
Queue message ID. |
`InsertionTime` |
`DateTimeOffset` |
The time that the message was added to the queue. |
`NextVisibleTime` |
`DateTimeOffset` |
The time that the message will next be visible. |
`PopReceipt` |
`string` |
The message's pop receipt. |

The following message metadata properties can be accessed from the passed binding parameter (`msg`

in previous [examples](#example)).

| Property | Description |
|---|---|
`body` |
Queue payload as a string. |
`dequeue_count` |
The number of times this message has been dequeued. |
`expiration_time` |
The time that the message expires. |
`id` |
Queue message ID. |
`insertion_time` |
The time that the message was added to the queue. |
`time_next_visible` |
The time that the message will next be visible. |
`pop_receipt` |
The message's pop receipt. |

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

[Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor),[Storage Queue Data Message Sender](../role-based-access-control/built-in-roles#storage-queue-data-message-sender)## Poison messages

When a queue trigger function fails, Azure Functions retries the function up to five times for a given queue message, including the first try. If all five attempts fail, the functions runtime adds a message to a queue named *<originalqueuename>-poison*. You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.

To handle poison messages manually, check the [dequeueCount](#message-metadata) of the queue message.

## Peek lock

The peek-lock pattern happens automatically for queue triggers, using the visibility mechanics provided by the storage service. As messages are dequeued by the triggered function, they're marked as invisible. Execution of a queue triggered function can have one of these results on message in the queue:

- Function execution completes successfully and the message is deleted from the queue.
- Function execution fails and the Functions host updates the visibility of the message based on the
`visibilityTimeout`

[setting in the host.json file](functions-bindings-storage-queue#host-json). The default visibility timeout is zero, which means that the message immediately reappears in the queue for reprocessing. Use the`visibilityTimeout`

setting to delay the reprocessing of messages that fail to process. This timeout setting applies to all queue triggered functions in the function app. - The Functions host crashes during function execution. When this uncommon event occurs, the host can't apply the
`visibilityTimeout`

to the message being processed. Instead, the message is left with the default 10 minute timeout set by the storage service. After 10 minutes, the message reappears in the queue for reprocessing. This service-defined default timeout can't be changed.

## Polling algorithm

The queue trigger implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.

The algorithm uses the following logic:

- When a message is found, the runtime waits 100 milliseconds and then checks for another message.
- When no message is found, it waits about 200 milliseconds before trying again.
- After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.
- The maximum wait time is configurable via the
`maxPollingInterval`

property in the[host.json file](functions-host-json-v1#queues).

During local development, the maximum polling interval defaults to two seconds.

Note

In regards to billing when hosting function apps in the Consumption plan, you are not charged for time spent polling by the runtime.

## Concurrency

When there are multiple queue messages waiting, the queue trigger retrieves a batch of messages and invokes function instances concurrently to process them. By default, the batch size is 16. When the number being processed gets down to 8, the runtime gets another batch and starts processing those messages. So the maximum number of concurrent messages being processed per function on one virtual machine (VM) is 24. This limit applies separately to each queue-triggered function on each VM. If your function app scales out to multiple VMs, each VM waits for triggers and attempt to run functions. For example, if a function app scales out to 3 VMs, the default maximum number of concurrent instances of one queue-triggered function is 72.

The batch size and the threshold for getting a new batch are configurable in the [host.json file](functions-host-json#queues). If you want to minimize parallel execution for queue-triggered functions in a function app, you can set the batch size to 1. This setting eliminates concurrency only so long as your function app runs on a single virtual machine (VM).

The queue trigger automatically prevents a function from processing a queue message multiple times simultaneously.

## host.json properties

The host.json file contains settings that control queue trigger behavior. See the [host.json settings](functions-bindings-storage-queue#host-json) section for details regarding available settings.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-site-updates -->

# Site update strategies in Flex Consumption

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you host your app with Azure Functions in the [Flex Consumption plan](flex-consumption-plan), you can control how updates are deployed to running instances. A site update occurs whenever you deploy code, modify application settings, or change other configuration properties. The Flex Consumption plan provides a site configuration setting (`SiteUpdateStrategy`

) that you can use to control whether your function app experiences downtime during these updates and how in-progress executions are handled.

The Flex Consumption plan currently supports these update strategies:

**Recreate**: Functions restarts all running instances after replacing your code with the latest version. This approach might cause brief downtime while instances are recycled and preserves the default behavior from other Azure Functions hosting plans.**Rolling update**(preview): Provides zero-downtime deployments by draining and replacing instances in batches. In-progress executions complete naturally without forced termination.

Important

The rolling update strategy is currently in preview and isn't recommended for production apps. Review the current [limitations and considerations](flex-consumption-site-updates#rolling-update-strategy-considerations) before enabling this strategy in any production app.

## Strategy comparison

This table compares the two site update strategies:

| Consideration | Recreate | Rolling update |
|---|---|---|
| Downtime | Brief downtime as your app scales out from zero after the restart | No period of downtime |
| In-progress executions | Forcefully terminated | Allowed to complete within the
|

✔ Brief downtime is acceptable.

✔ You're deploying breaking changes and need a clean restart.

✔ Your functions are stateless and can handle interruptions.

✔ You have long-running or critical functions that can't be interrupted.

✔ Your changes are backward-compatible.

✔ You must preserve in-progress executions.

## Update strategy behaviors

This table compares the update process of the two strategies:

**Recreate strategy**:

**Rolling update strategy**:

- A site update (code or configuration changes) is applied to your function app.
- The recreate strategy is triggered to update running instances with the new changes.
- The platform forcefully restarts all live and draining instances.
- The scaling system immediately begins provisioning new instances with the updated version (original instances might still be deprovisioning in the background).

- A site update (code or configuration changes) is applied to your function app.
- The rolling update strategy is triggered to update running instances with the new changes.
- The platform assigns all live instances to batches.
- At regular intervals, the platform drains one batch of instances. Draining prevents instances from accepting new events while allowing in-progress executions to complete (up to the one hour maximum execution time).
- Simultaneously, the scaling platform provisions new instances running the updated version to replace the draining capacity.
- This process continues until all live instances are running the updated version.

This table compares the key characteristics of the two strategies:

**Recreate strategy**:

**Rolling update strategy**:

**Brief downtime**: Your app is unavailable while instances restart and scale out**Execution interruption**: In-progress executions are terminated immediately**No completion signal**: Monitor instance logs to track when original instances stop emitting logs

**Zero downtime**: deployments are done in batches so that executions complete without forced termination.**Asynchronous operations**: Draining and scale-out happen simultaneously without waiting for each other to complete. The scale-out isn't guaranteed to occur before the next drain interval.**Overlapping updates**: You can initiate additional rolling updates while one is in progress. All non-latest instances are drained, and only the newest version is scaled out.**Dynamic scaling**: The platform adjusts instance count based on current demand during the update.**Platform managed capacity**: When demand increases, the platform provisions more instances than it drains. When demand decreases, it creates only the necessary instances to meet current needs. This approach ensures continuous availability while optimizing resource usage.

## Rolling update strategy considerations

Keep these current behaviors and limitations in mind when using the rolling update strategy. This list is maintained during the preview period and could change as the feature approaches general availability (GA).

**Platform-managed parameters**: The platform controls the parameters (such as batch count, instances per batch, number of batches, and drain intervals) that determine rolling update behaviors. These parameters might change before GA to optimize performance and reliability.**No real-time monitoring**: There's currently no visibility into how many instances are draining, how many batches remain, or current progress percentages.**No completion signal**: However, you can monitor instance logs to estimate when an update completes.**Single-instance scenarios**: Apps running on one instance experience brief downtime similar to recreate, though in-progress executions still complete.**Durable Functions**: Because mixing versions during updates can cause unexpected behavior in a Durable orchestration, use an explicit[orchestration version match strategy](durable/durable-functions-orchestration-versioning).**Infrastructure as Code**: Deploying code and configuration changes together triggers multiple rolling updates that might overlap.**Backward compatibility**: Make sure that your changes work with the previous version during the rolling update transition period.

## Configure your update strategy

You can set the update strategy for your app using the `SiteUpdateStrategy`

site setting, which is a child of `functionAppConfig`

. By default, `SiteUpdateStrategy.type`

is set to `Recreate`

. Currently, only Bicep and ARM templates with API version `2023-12-01`

or later support changing this property.

```
functionAppConfig: {
...
siteUpdateStrategy: {
type: 'RollingUpdate'
}
...
}
```


Changes to the site update strategy take effect at the next site update. For example, changing `type`

from `Recreate`

to `RollingUpdate`

uses the recreate strategy for that update. All subsequent site updates then use rolling updates.

## Monitoring site updates

During the public preview, there's no built-in completion signal for site updates. You can use KQL queries in Application Insights as a best-effort approach to estimate rolling update progress.

### Monitoring rolling update progress

These KQL queries provide a best-effort estimate of rolling update progress by tracking instance turnover in Application Insights logs. This approach has significant limitations and shouldn't be relied upon for production automation:

```
// Rolling update completion check
let deploymentStart = datetime('2025-10-30T19:00:00Z'); // Set to your deployment start time
let checkInterval = 10s; // How often you run this query
let buffer = 30s; // Safety buffer for instance detection
//
// Get original instances (active before deployment)
let originalInstances =
traces
| where timestamp between ((deploymentStart - buffer) .. deploymentStart)
| where cloud_RoleInstance != ""
| summarize by InstanceId = cloud_RoleInstance;
//
// Get currently active instances
let currentInstances =
traces
| where timestamp >= now() - checkInterval
| where cloud_RoleInstance != ""
| summarize by InstanceId = cloud_RoleInstance;
//
// Check completion status
currentInstances
| join kind=leftouter (originalInstances | extend IsOriginal = true) on InstanceId
| extend IsOriginal = isnotnull(IsOriginal)
| summarize
OriginalStillActiveInstances = make_set_if(InstanceId, IsOriginal),
NewInstances = make_set_if(InstanceId, not(IsOriginal)),
OriginalStillActiveCount = countif(IsOriginal),
NewCount = countif(not(IsOriginal)),
TotalOriginal = toscalar(originalInstances | count)
| extend
RollingUpdateComplete = iff(OriginalStillActiveCount == 0, "YES", "NO"),
PercentComplete = round(100.0 * (1.0 - todouble(OriginalStillActiveCount) / todouble(TotalOriginal)), 1)
| project RollingUpdateComplete, PercentComplete, OriginalStillActiveCount, NewCount
```


How to use this query for estimation:

- Paste this query in the Logs blade of the Application Insights resource associated with your function app.
- Set
`deploymentStart`

to the timestamp when your site update returns success. - Run the query periodically to estimate progress. Set the polling interval to be at least as long as your average function execution time, and ensure the
`checkInterval`

variable in the query matches this polling frequency. - The query returns approximate values:
`RollingUpdateComplete`

: Best estimate of whether all original instances are replaced`PercentComplete`

: Estimated percentage of original instances that are replaced`OriginalStillActiveCount`

: Estimated number of original instances still running`NewCount`

: Number of new instances currently active


Keep these limitations in mind when using these queries:

**Timing gap**: The`deploymentStart`

time represents when your site update returns success, but the actual rolling update might not start immediately. During this gap, any scale-out events provision instances running the original version. Since the query only tracks instances active at`deploymentStart`

, it doesn't monitor these new original-version instances, potentially causing false completion signals.**Log-based detection**: This approach relies on application logs to infer instance state rather than directly querying instance status. Instances might be running but not actively logging, leading to false completion signals when original instances are still active but didn't emit logs within the`checkInterval`

window.

**Recommendation for production**: Use rolling updates when zero-downtime deployments are critical. Ensure your deployment pipelines don't require waiting for update completion before proceeding to subsequent steps. Use recreate when you need faster, more predictable update timing and can tolerate brief downtime.

## FAQ

**I'm used to deployment slots for zero downtime deployments. How do rolling updates differ?**

- Unlike deployment slots, rolling updates require no additional infrastructure. Set
`siteUpdateStrategy.type`

to`"RollingUpdate"`

for zero-downtime deployments. - Rolling updates preserve in-progress executions, while deployment slots terminate them during swaps.
[Certain site properties](functions-deployment-slots#manage-settings)and sticky settings can't be swapped and require modifying the production slot directly. - Unlike deployment slots, rolling updates don't provide a separate environment for you to canary test changes or route a percentage of live traffic to. If you need these features, use a plan that supports deployment slots, like Elastic Premium, or manage separate Flex Consumption apps behind a traffic manager.

**How do I roll back a site update?**

- There's currently no feature to roll back a site update. If a rollback is necessary, initiate another site update with the previous state of code or configuration.

**How are timer triggers handled?**

- Timer triggers maintain their singleton nature. Once a timer-triggered function app is marked for drain, new timer functions run on the latest version.

**I'm seeing runtime errors during the rolling update...what went wrong?**

- If new instances fail to start or encounter runtime errors, the issue is likely in the application code, dependencies, configuration settings, or environment variables that you modified.
- To resolve the issue, redeploy your last known healthy version to restore the runtime. Then test your proposed changes in a development or staging environment before reattempting. Review error logs to identify what specific change caused the issue.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-integrate-storage-queue-output-binding -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-java-gradle -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-sql-trigger -->

# Azure SQL trigger for Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure SQL trigger uses [SQL change tracking](/en-us/sql/relational-databases/track-changes/about-change-tracking-sql-server) functionality to monitor a SQL table for changes and trigger a function when a row is created, updated, or deleted. For configuration details for change tracking for use with the Azure SQL trigger, see [Set up change tracking](#set-up-change-tracking-required). For information on setup details of the Azure SQL extension for Azure Functions, see the [SQL binding overview](functions-bindings-azure-sql).

The Azure SQL trigger scaling decisions for the [Consumption and Premium plans](functions-scale) are done via target-based scaling. For more information, see [Target-based scaling](functions-target-based-scaling) and review the [Azure Functions hosting options](functions-scale).

Note

Support for Consumption plans requires [release v3.1.284 or later](https://github.com/Azure/azure-functions-sql-extension/releases) of the [Azure SQL bindings for Azure Functions](functions-bindings-azure-sql).

## Functionality Overview

The Azure SQL trigger binding uses a polling loop to check for changes, triggering the user function when changes are detected. At a high level, the loop looks like this:

```
while (true) {
1. Get list of changes on table - up to a maximum number controlled by the Sql_Trigger_MaxBatchSize setting
2. Trigger function with list of changes
3. Wait for delay controlled by Sql_Trigger_PollingIntervalMs setting
}
```


Changes are processed in the order that their changes were made, with the oldest changes being processed first. A couple notes about change processing:

- If changes to multiple rows are made at once the exact order that they’re sent to the function is based on the order returned by the CHANGETABLE function
- Changes are "batched" together for a row. If multiple changes are made to a row between each iteration of the loop then only a single change entry exists for that row which will show the difference between the last processed state and the current state
- If changes are made to a set of rows, and then another set of changes are made to half of those same rows, then the half of the rows that weren't changed a second time are processed first. This processing logic is due to the above note with the changes being batched - the trigger will only see the "last" change made and use that for the order it processes them in

Note

Azure SQL change tracking can detect row-level changes in tables that use encryption technologies such as Always Encrypted or Transparent Data Encryption (TDE). However, the Azure SQL trigger doesn’t decrypt or expose encrypted column values in the change payload. The trigger can detect that a change occurred but can’t access the decrypted data for those columns.

For more information on change tracking and how it's used by applications such as Azure SQL triggers, see [work with change tracking](/en-us/sql/relational-databases/track-changes/work-with-change-tracking-sql-server) .

Important

For optimal security, you should use Microsoft Entra ID with managed identities for connections between Functions and Azure SQL Database. Managed identities make your app more secure by eliminating secrets from your application deployments, such as credentials in the connection strings, server names, and ports being used. You can learn how to use managed identities in this tutorial, [Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).

## Example usage

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-outofproc).

The example refers to a `ToDoItem`

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


[Change tracking](#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds to a `IReadOnlyList<SqlChange<T>>`

, a list of `SqlChange`

objects each with two properties:

**Item:**the item that was changed. The type of the item should follow the table schema as seen in the`ToDoItem`

class.**Operation:**a value from`SqlChangeOperation`

enum. The possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a [C# function](functions-dotnet-class-library) that is invoked when there are changes to the `ToDo`

table:

```
using System;
using System.Collections.Generic;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
namespace AzureSQL.ToDo
{
public static class ToDoTrigger
{
[Function("ToDoTrigger")]
public static void Run(
[SqlTrigger("[dbo].[ToDo]", "SqlConnectionString")]
IReadOnlyList<SqlChange<ToDoItem>> changes,
FunctionContext context)
{
var logger = context.GetLogger("ToDoTrigger");
foreach (SqlChange<ToDoItem> change in changes)
{
ToDoItem toDoItem = change.Item;
logger.LogInformation($"Change operation: {change.Operation}");
logger.LogInformation($"Id: {toDoItem.Id}, Title: {toDoItem.title}, Url: {toDoItem.url}, Completed: {toDoItem.completed}");
}
}
}
}
```


## Example usage

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-java).

The example refers to a `ToDoItem`

class, a `SqlChangeToDoItem`

class, a `SqlChangeOperation`

enum, and a corresponding database table:

In a separate file `ToDoItem.java`

:

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


In a separate file `SqlChangeToDoItem.java`

:

```
package com.function;
public class SqlChangeToDoItem {
public ToDoItem item;
public SqlChangeOperation operation;
public SqlChangeToDoItem() {
}
public SqlChangeToDoItem(ToDoItem Item, SqlChangeOperation Operation) {
this.Item = Item;
this.Operation = Operation;
}
}
```


In a separate file `SqlChangeOperation.java`

:

```
package com.function;
import com.google.gson.annotations.SerializedName;
public enum SqlChangeOperation {
@SerializedName("0")
Insert,
@SerializedName("1")
Update,
@SerializedName("2")
Delete;
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


[Change tracking](#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds to a `SqlChangeToDoItem[]`

, an array of `SqlChangeToDoItem`

objects each with two properties:

**item:**the item that was changed. The type of the item should follow the table schema as seen in the`ToDoItem`

class.**operation:**a value from`SqlChangeOperation`

enum. The possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a Java function that is invoked when there are changes to the `ToDo`

table:

```
package com.function;
import com.microsoft.azure.functions.ExecutionContext;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.sql.annotation.SQLTrigger;
import com.function.Common.SqlChangeToDoItem;
import com.google.gson.Gson;
import java.util.logging.Level;
public class ProductsTrigger {
@FunctionName("ToDoTrigger")
public void run(
@SQLTrigger(
name = "todoItems",
tableName = "[dbo].[ToDo]",
connectionStringSetting = "SqlConnectionString")
SqlChangeToDoItem[] todoItems,
ExecutionContext context) {
context.getLogger().log(Level.INFO, "SQL Changes: " + new Gson().toJson(changes));
}
}
```


## Example usage

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-powershell).

The example refers to a `ToDoItem`

database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


[Change tracking](#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds to `todoChanges`

, a list of objects each with two properties:

**item:**the item that was changed. The structure of the item will follow the table schema.**operation:**the possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a PowerShell function that is invoked when there are changes to the `ToDo`

table.

The following is binding data in the function.json file:

```
{
"name": "todoChanges",
"type": "sqlTrigger",
"direction": "in",
"tableName": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($todoChanges)
# The output is used to inspect the trigger binding parameter in test methods.
# Use -Compress to remove new lines and spaces for testing purposes.
$changesJson = $todoChanges | ConvertTo-Json -Compress
Write-Host "SQL Changes: $changesJson"
```


## Example usage

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-js).

The example refers to a `ToDoItem`

database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


[Change tracking](#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds `todoChanges`

, an array of objects each with two properties:

**item:**the item that was changed. The structure of the item will follow the table schema.**operation:**the possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a JavaScript function that is invoked when there are changes to the `ToDo`

table.

The following is binding data in the function.json file:

```
{
"name": "todoChanges",
"type": "sqlTrigger",
"direction": "in",
"tableName": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample JavaScript code for the function in the `index.js`

file:

```
module.exports = async function (context, todoChanges) {
context.log(`SQL Changes: ${JSON.stringify(todoChanges)}`)
}
```


## Example usage

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-python).

The example refers to a `ToDoItem`

database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


[Change tracking](#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds to a variable `todoChanges`

, a list of objects each with two properties:

**item:**the item that was changed. The structure of the item will follow the table schema.**operation:**the possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a Python function that is invoked when there are changes to the `ToDo`

table.

The following is sample python code for the function_app.py file:

```
import json
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="ToDoTrigger")
@app.sql_trigger(arg_name="todo",
table_name="ToDo",
connection_string_setting="SqlConnectionString")
def todo_trigger(todo: str) -> None:
logging.info("SQL Changes: %s", json.loads(todo))
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [SqlTrigger](https://github.com/Azure/azure-functions-sql-extension/blob/main/src/TriggerBinding/SqlTriggerAttribute.cs) attribute to declare the SQL trigger on the function, which has the following properties:

| Attribute property | Description |
|---|---|
TableName |
Required. The name of the table monitored by the trigger. |
ConnectionStringSetting |
Required. The name of an app setting that contains the connection string for the database containing the table monitored for changes. The connection string setting name corresponds to the application setting (in `local.settings.json` for local development) that contains the
|
LeasesTableName |
Optional. Name of the table used to store leases. If not specified, the leases table name will be Leases_{FunctionId}_{TableId}. More information on how this is generated can be found
|

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@SQLTrigger`

annotation (`com.microsoft.azure.functions.sql.annotation.SQLTrigger`

) on parameters whose value would come from Azure SQL. This annotation supports the following elements:

| Element | Description |
|---|---|
name |
Required. The name of the parameter that the trigger binds to. |
tableName |
Required. The name of the table monitored by the trigger. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database containing the table monitored for changes. The connection string setting name corresponds to the application setting (in `local.settings.json` for local development) that contains the
|
LeasesTableName |
Optional. Name of the table used to store leases. If not specified, the leases table name will be Leases_{FunctionId}_{TableId}. More information on how this is generated can be found
|

## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
name |
Required. The name of the parameter that the trigger binds to. |
type |
Required. Must be set to `sqlTrigger` . |
direction |
Required. Must be set to `in` . |
tableName |
Required. The name of the table monitored by the trigger. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database containing the table monitored for changes. The connection string setting name corresponds to the application setting (in `local.settings.json` for local development) that contains the
|
LeasesTableName |
Optional. Name of the table used to store leases. If not specified, the leases table name will be Leases_{FunctionId}_{TableId}. More information on how this is generated can be found
|

## Optional Configuration

The following optional settings can be configured for the SQL trigger for local development or for cloud deployments.

### host.json

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

| Setting | Default | Description |
|---|---|---|
MaxBatchSize |
100 | The maximum number of changes processed with each iteration of the trigger loop before being sent to the triggered function. |
PollingIntervalMs |
1000 | The delay in milliseconds between processing each batch of changes. (1000 ms is 1 second) |
MaxChangesPerWorker |
1000 | The upper limit on the number of pending changes in the user table that are allowed per application-worker. If the count of changes exceeds this limit, it might result in a scale-out. The setting only applies for Azure Function Apps with
|

#### Example host.json file

Here is an example host.json file with the optional settings:

```
{
"version": "2.0",
"extensions": {
"Sql": {
"MaxBatchSize": 300,
"PollingIntervalMs": 1000,
"MaxChangesPerWorker": 100
}
},
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
},
"logLevel": {
"default": "Trace"
}
}
}
```


### local.setting.json

The local.settings.json file stores app settings and settings used by local development tools. Settings in the local.settings.json file are used only when you're running your project locally. When you publish your project to Azure, be sure to also add any required settings to the app settings for the function app.

Important

Because the local.settings.json may contain secrets, such as connection strings, you should never store it in a remote repository. Tools that support Functions provide ways to synchronize settings in the local.settings.json file with the [app settings](functions-how-to-use-azure-function-app-settings#settings) in the function app to which your project is deployed.

| Setting | Default | Description |
|---|---|---|
Sql_Trigger_BatchSize |
100 | The maximum number of changes processed with each iteration of the trigger loop before being sent to the triggered function. |
Sql_Trigger_PollingIntervalMs |
1000 | The delay in milliseconds between processing each batch of changes. (1000 ms is 1 second) |
Sql_Trigger_MaxChangesPerWorker |
1000 | The upper limit on the number of pending changes in the user table that are allowed per application-worker. If the count of changes exceeds this limit, it might result in a scale-out. The setting only applies for Azure Function Apps with
|

#### Example local.settings.json file

Here is an example local.settings.json file with the optional settings:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_WORKER_RUNTIME": "dotnet",
"SqlConnectionString": "",
"Sql_Trigger_MaxBatchSize": 300,
"Sql_Trigger_PollingIntervalMs": 1000,
"Sql_Trigger_MaxChangesPerWorker": 100
}
}
```


## Set up change tracking (required)

Setting up change tracking for use with the Azure SQL trigger requires two steps. These steps can be completed from any SQL tool that supports running queries, including [Visual Studio Code](/en-us/sql/tools/visual-studio-code/mssql-extensions), [Azure Data Studio](/en-us/azure-data-studio/download-azure-data-studio) or [SQL Server Management Studio](/en-us/sql/ssms/download-sql-server-management-studio-ssms).

Enable change tracking on the SQL database, substituting

`your database name`

with the name of the database where the table to be monitored is located:`ALTER DATABASE [your database name] SET CHANGE_TRACKING = ON (CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);`

The

`CHANGE_RETENTION`

option specifies the time period for which change tracking information (change history) is kept. The retention of change history by the SQL database might affect trigger functionality. For example, if the Azure Function is turned off for several days and then resumed, the database will contain the changes that occurred in past two days in the above setup example.The

`AUTO_CLEANUP`

option is used to enable or disable the clean-up task that removes old change tracking information. If a temporary problem that prevents the trigger from running, turning off auto cleanup can be useful to pause the removal of information older than the retention period until the problem is resolved.More information on change tracking options is available in the

[SQL documentation](/en-us/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server).Enable change tracking on the table, substituting

`your table name`

with the name of the table to be monitored (changing the schema if appropriate):`ALTER TABLE [dbo].[your table name] ENABLE CHANGE_TRACKING;`

The trigger needs to have read access on the table being monitored for changes and to the change tracking system tables. Each function trigger has an associated change tracking table and leases table in a schema

`az_func`

. These tables are created by the trigger if they don't yet exist. More information on these data structures is available in the Azure SQL binding library[documentation](https://github.com/Azure/azure-functions-sql-extension/blob/main/docs/BindingsOverview.md#internal-state-tables).

## Enable runtime-driven scaling

Optionally, your functions can scale automatically based on the number of changes that are pending to be processed in the user table. To allow your functions to scale properly on the Premium plan when using SQL triggers, you need to enable runtime scale monitoring.

In the Azure portal, in your function app, select

**Configuration**.On the

**Function runtime settings**tab, for**Runtime Scale Monitoring**, select**On**.

## Retry support

Further information on the SQL trigger [retry support](https://github.com/Azure/azure-functions-sql-extension/blob/main/docs/BindingsOverview.md#retry-support-for-trigger-bindings) and [leases tables](https://github.com/Azure/azure-functions-sql-extension/blob/main/docs/TriggerBinding.md#internal-state-tables) is available in the GitHub repository.

### Startup retries

If an exception occurs during startup then the host runtime automatically attempts to restart the trigger listener with an exponential backoff strategy. These retries continue until either the listener is successfully started or the startup is canceled.

### Broken connection retries

If the function successfully starts but then an error causes the connection to break (such as the server going offline) then the function continues to try and reopen the connection until the function is either stopped or the connection succeeds. If the connection is successfully re-established then it picks up processing changes where it left off.

Note that these retries are outside the built-in idle connection retry logic that SqlClient has which can be configured with the `ConnectRetryCount`

and `ConnectRetryInterval`

[connection string options](/en-us/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-core-5.0&preserve-view=true#Microsoft_Data_SqlClient_SqlConnection_ConnectionString). The built-in idle connection retries are attempted first and if those fail to reconnect then the trigger binding attempts to re-establish the connection itself.

### Function exception retries

If an exception occurs in the user function when processing changes then the batch of rows currently being processed are retried again in 60 seconds. Other changes are processed as normal during this time, but the rows in the batch that caused the exception are ignored until the timeout period has elapsed.

If the function execution fails five times in a row for a given row then that row is completely ignored for all future changes. Because the rows in a batch aren't deterministic, rows in a failed batch might end up in different batches in subsequent invocations. This means that not all rows in the failed batch will necessarily be ignored. If other rows in the batch were the ones causing the exception, the "good" rows might end up in a different batch that doesn't fail in future invocations.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-storage-queue-vs-code -->

# Connect Azure Functions to Azure Storage using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you connect Azure services and other resources to functions without having to write your own integration code. These *bindings*, which represent both input and output, are declared within the function definition. Data from bindings is provided to the function as parameters. A *trigger* is a special type of input binding. Although a function has only one trigger, it can have multiple input and output bindings. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

In this article, you learn how to use Visual Studio Code to connect Azure Storage to the function you created in the previous quickstart article. The output binding that you add to this function writes data from the HTTP request to a message in an Azure Queue storage queue.

Most bindings require a stored connection string that Functions uses to access the bound service. To make it easier, you use the storage account that you created with your function app. The connection to this account is already stored in an app setting named `AzureWebJobsStorage`

.

Note

This article currently supports [Node.js v4 for Functions](functions-reference-node?pivots=nodejs-model-v4).

## Configure your local environment

Before you begin, you must meet the following requirements:

Install the

[Azure Storage extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage).Install

[Azure Storage Explorer](https://storageexplorer.com/). Storage Explorer is a tool that you'll use to examine queue messages generated by your output binding. Storage Explorer is supported on macOS, Windows, and Linux-based operating systems.

- Install
[.NET Core CLI tools](/en-us/dotnet/core/tools/?tabs=netcore2x).

- Complete the steps in
[part 1 of Create a function in Azure using Visual Studio Code](how-to-create-function-vs-code).

This article assumes that you're already signed in to your Azure subscription from Visual Studio Code. You can sign in by running `Azure: Sign In`

from the command palette.

## Download the function app settings

In the [previous quickstart article](how-to-create-function-vs-code?pivot=programming-language-csharp), you created a function app in Azure along with the required storage account. The connection string for this account is stored securely in the app settings in Azure. In this article, you write messages to a Storage queue in the same account. To connect to your storage account when running the function locally, you must download app settings to the *local.settings.json* file.

Press

`F1`to open the command palette, then search for and run the command`Azure Functions: Download Remote Settings...`

.Choose the function app you created in the previous article. Select

**Yes to all**to overwrite the existing local settings.Important

Because the

*local.settings.json*file contains secrets, it never gets published, and is excluded from the source control.Copy the value

`AzureWebJobsStorage`

, which is the key for the storage account connection string value. You use this connection to verify that the output binding works as expected.

## Register binding extensions

Because you're using a Queue storage output binding, you must have the Storage bindings extension installed before you run the project.

Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles is already enabled in the *host.json* file at the root of the project, which should look like the following example:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[3.*, 4.0.0)"
}
}
```


Now, you can add the storage output binding to your project.

Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles is already enabled in the *host.json* file at the root of the project, which should look like the following example:

```
{
"version": "2.0",
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


Now, you can add the storage output binding to your project.

Except for HTTP and timer triggers, bindings are implemented as extension packages. Run the following [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window to add the Storage extension package to your project.

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues --prerelease
```


Now, you can add the storage output binding to your project.

## Add an output binding

To write to an Azure Storage queue:

Add an

`extraOutputs`

property to the binding configuration`{ methods: ['GET', 'POST'], extraOutputs: [sendToQueue], // add output binding to HTTP trigger authLevel: 'function', handler: () => {} }`

Add a

`output.storageQueue`

function above the`app.http`

call`const sendToQueue = output.storageQueue({ queueName: 'outqueue', connection: 'AzureWebJobsStorage', });`


To write to an Azure Storage queue:

Add an

`extraOutputs`

property to the binding configuration`{ methods: ['GET', 'POST'], extraOutputs: [sendToQueue], // add output binding to HTTP trigger authLevel: 'function', handler: () => {} }`

Add a

`output.storageQueue`

function above the`app.http`

call`const sendToQueue: StorageQueueOutput = output.storageQueue({ queueName: 'outqueue', connection: 'AzureWebJobsStorage', });`


In Functions, each type of binding requires a `direction`

, `type`

, and unique `name`

. The way you define these attributes depends on the language of your function app.

Binding attributes are defined in the *function.json* file for a given function. Depending on the binding type, additional properties may be required. The [queue output configuration](functions-bindings-storage-queue-output#configuration) describes the fields required for an Azure Storage queue binding. The extension makes it easy to add bindings to the *function.json* file.

To create a binding, right-click (Ctrl+click on macOS) the `function.json`

file in your HttpTrigger folder and choose **Add binding...**. Follow the prompts to define the following binding properties for the new binding:

| Prompt | Value | Description |
|---|---|---|
Select binding direction |
`out` |
The binding is an output binding. |
Select binding with direction... |
`Azure Queue Storage` |
The binding is an Azure Storage queue binding. |
The name used to identify this binding in your code |
`msg` |
Name that identifies the binding parameter referenced in your code. |
The queue to which the message will be sent |
`outqueue` |
The name of the queue that the binding writes to. When the queueName doesn't exist, the binding creates it on first use. |
Select setting from "local.setting.json" |
`AzureWebJobsStorage` |
The name of an application setting that contains the connection string for the Storage account. The `AzureWebJobsStorage` setting contains the connection string for the Storage account you created with the function app. |

A binding is added to the `bindings`

array in your *function.json*, which should look like the following:

```
"name": "msg",
"queueName": "outqueue",
"connection": "AzureWebJobsStorage"
}
]
}
```


Binding attributes are defined by decorating specific function code in the *function_app.py* file. You use the `queue_output`

decorator to add an [Azure Queue storage output binding](/en-us/azure/azure-functions/functions-bindings-triggers-python#azure-queue-storage-output-binding).

By using the `queue_output`

decorator, the binding direction is implicitly 'out' and type is Azure Storage Queue. Add the following decorator to your function code in *HttpExample\function_app.py*:

```
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
```


In this code, `arg_name`

identifies the binding parameter referenced in your code, `queue_name`

is name of the queue that the binding writes to, and `connection`

is the name of an application setting that contains the connection string for the Storage account. In quickstarts you use the same storage account as the function app, which is in the `AzureWebJobsStorage`

setting. When the `queue_name`

doesn't exist, the binding creates it on first use.

In a C# project, the bindings are defined as binding attributes on the function method. Specific definitions depend on whether your app runs in-process (C# class library) or in an isolated worker process.

Open the *HttpExample.cs* project file and add the following `MultiResponse`

class:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The `MultiResponse`

class allows you to write to a storage queue named `outqueue`

and an HTTP success message. Multiple messages could be sent to the queue because the `QueueOutput`

attribute is applied to a string array.

The `Connection`

property sets the connection string for the storage account. In this case, you could omit `Connection`

because you're already using the default storage account.

In a Java project, the bindings are defined as binding annotations on the function method. The *function.json* file is then autogenerated based on these annotations.

Browse to the location of your function code under *src/main/java*, open the *Function.java* project file, and add the following parameter to the `run`

method definition:

```
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
```


The `msg`

parameter is an [ OutputBinding<T>](/en-us/java/api/com.microsoft.azure.functions.outputbinding) type, which represents a collection of strings that are written as messages to an output binding when the function completes. In this case, the output is a storage queue named

`outqueue`

. The connection string for the Storage account is set by the `connection`

method. Rather than the connection string itself, you pass the application setting that contains the Storage account connection string.The `run`

method definition should now look like the following example:

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
```


## Add code that uses the output binding

After the binding is defined, you can use the `name`

of the binding to access it as an attribute in the function signature. By using an output binding, you don't have to use the Azure Storage SDK code for authentication, getting a queue reference, or writing data. The Functions runtime and queue output binding do those tasks for you.

Add code that uses the output binding object on `context.extraOutputs`

to create a queue message. Add this code before the return statement.

```
context.extraOutputs.set(sendToQueue, [msg]);
```


At this point, your function could look as follows:

```
const { app, output } = require('@azure/functions');
const sendToQueue = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [sendToQueue],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


Add code that uses the output binding object on `context.extraOutputs`

to create a queue message. Add this code before the return statement.

```
context.extraOutputs.set(sendToQueue, [msg]);
```


At this point, your function could look as follows:

```
import {
app,
output,
HttpRequest,
HttpResponseInit,
InvocationContext,
StorageQueueOutput,
} from '@azure/functions';
const sendToQueue: StorageQueueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
export async function HttpExample(
request: HttpRequest,
context: InvocationContext,
): Promise<HttpResponseInit> {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
}
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: HttpExample,
});
```


Add code that uses the `Push-OutputBinding`

cmdlet to write text to the queue using the `msg`

output binding. Add this code before you set the OK status in the `if`

statement.

```
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
```


At this point, your function must look as follows:

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
if ($name) {
# Write the $name value to the queue,
# which is the name passed to the function.
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
$status = [HttpStatusCode]::OK
$body = "Hello $name"
}
else {
$status = [HttpStatusCode]::BadRequest
$body = "Please pass a name on the query string or in the request body."
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = $status
Body = $body
})
```


Update *HttpExample\function_app.py* to match the following code, add the `msg`

parameter to the function definition and `msg.set(name)`

under the `if name:`

statement:

```
import azure.functions as func
import logging
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
name = req.params.get('name')
if not name:
try:
req_body = req.get_json()
except ValueError:
pass
else:
name = req_body.get('name')
if name:
msg.set(name)
return func.HttpResponse(f"Hello, {name}. This HTTP triggered function executed successfully.")
else:
return func.HttpResponse(
"This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.",
status_code=200
)
```


The `msg`

parameter is an instance of the [ azure.functions.Out class](/en-us/python/api/azure-functions/azure.functions.out). The

`set`

method writes a string message to the queue. In this case, it's the `name`

passed to the function in the URL query string.Replace the existing `HttpExample`

class with the following code:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpExample");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = "Welcome to Azure Functions!";
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
// Return a response to both HTTP trigger and storage output binding.
return new MultiResponse()
{
// Write a single message.
Messages = new string[] { message },
HttpResponse = response
};
}
}
```


Now, you can use the new `msg`

parameter to write to the output binding from your function code. Add the following line of code before the success response to add the value of `name`

to the `msg`

output binding.

```
msg.setValue(name);
```


When you use an output binding, you don't have to use the Azure Storage SDK code for authentication, getting a queue reference, or writing data. The Functions runtime and queue output binding do those tasks for you.

Your `run`

method should now look like the following example:

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("name");
String name = request.getBody().orElse(query);
if (name == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Please pass a name on the query string or in the request body").build();
} else {
// Write the name to the message queue.
msg.setValue(name);
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
}
}
```


## Update the tests

Because the archetype also creates a set of tests, you need to update these tests to handle the new `msg`

parameter in the `run`

method signature.

Browse to the location of your test code under *src/test/java*, open the *Function.java* project file, and replace the line of code under `//Invoke`

with the following code.

```
@SuppressWarnings("unchecked")
final OutputBinding<String> msg = (OutputBinding<String>)mock(OutputBinding.class);
final HttpResponseMessage ret = new Function().run(req, msg, context);
```


## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure. If you don't already have Core Tools installed locally, you are prompted to install it the first time you run your project.

To call your function, press

`F5`to start the function app project. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you don't already have Core Tools installed, select

**Install**to install Core Tools when prompted to do so.

If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to**WSL Bash**.With the Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the`HttpExample`

function and choose**Execute Function Now...**.In the

**Enter request body**, press`Enter`to send a request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in the

**Terminal**panel.Press

`Ctrl + C`to stop Core Tools and disconnect the debugger.

## Run the function locally

As in the previous article, press

`F5`to start the function app project and Core Tools.With the Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Ctrl-click on Mac) the`HttpExample`

function and select**Execute Function Now...**.In the

**Enter request body**, you see the request message body value of`{ "name": "Azure" }`

. Press`Enter`to send this request message to your function.After a response is returned, press

`Ctrl + C`to stop Core Tools.

Because you're using the storage connection string, your function connects to the Azure storage account when running locally. A new queue named **outqueue** is created in your storage account by the Functions runtime when the output binding is first used. You'll use Storage Explorer to verify that the queue was created along with the new message.

### Connect Storage Explorer to your account

Skip this section if you've already installed Azure Storage Explorer and connected it to your Azure account.

Run the

[Azure Storage Explorer](https://storageexplorer.com/)tool, select the connect icon on the left, and select**Add an account**.In the

**Connect**dialog, choose**Add an Azure account**, choose your**Azure environment**, and then select**Sign in...**.

After you successfully sign in to your account, you see all of the Azure subscriptions associated with your account. Choose your subscription and select **Open Explorer**.

### Examine the output queue

In Visual Studio Code, press

`F1`to open the command palette, then search for and run the command`Azure Storage: Open in Storage Explorer`

and choose your storage account name. Your storage account opens in the Azure Storage Explorer.Expand the

**Queues**node, and then select the queue named**outqueue**.The queue contains the message that the queue output binding created when you ran the HTTP-triggered function. If you invoked the function with the default

`name`

value of*Azure*, the queue message is*Name passed to the function: Azure*.Run the function again, send another request, and you see a new message in the queue.


Now, it's time to republish the updated function app to Azure.

## Redeploy and verify the updated app

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure Functions: Deploy to function app...`

.Choose the function app that you created in the first article. Because you're redeploying your project to the same app, select

**Deploy**to dismiss the warning about overwriting files.After the deployment completes, you can again use the

**Execute Function Now...**feature to trigger the function in Azure. This command automatically retrieves the function access key and uses it when calling the HTTP trigger endpoint.Again

[view the message in the storage queue](#examine-the-output-queue)to verify that the output binding generates a new message in the queue.

## Clean up resources

In Azure, *resources* refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You've created resources to complete these quickstarts. You may be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You've updated your HTTP triggered function to write data to a Storage queue. Now you can learn more about developing Functions using Visual Studio Code:
