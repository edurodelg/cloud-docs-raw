---
merged_at: 2026-01-26T23:29:57.721302
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/add-bindings-existing-function -->

# Connect functions to Azure services using bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a function, language-specific trigger code is added in your project from a set of trigger templates. If you want to connect your function to other services by using input or output bindings, you have to add specific binding definitions in your function. To learn more about bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

## Local development

When you develop functions locally, you need to update the function code to add bindings. For languages that use function.json, [Visual Studio Code](#visual-studio-code) provides tooling to add bindings to a function.

### Manually add bindings based on examples

When adding a binding to an existing function, you need to add binding-specific attributes to the function definition in code.

When adding a binding to an existing function, you need to add binding-specific annotations to the function definition in code.

When adding a binding to an existing function, you need to update the function code and add a definition to the function.json configuration file.

When adding a binding to an existing function, you need update the function definition, depending on your model:

The following example shows the function definition after adding a [Queue Storage output binding](functions-bindings-storage-queue-output) to an [HTTP triggered function](functions-bindings-http-webhook-trigger):

Because an HTTP triggered function also returns an HTTP response, the function returns a `MultiResponse`

object, which represents both the HTTP and queue output.

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequest req,
FunctionContext executionContext)
{
```


This example is the definition of the `MultiResponse`

object that includes the output binding:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public IActionResult HttpResponse { get; set; }
}
```


When applying that example to your own project, you might need to change `HttpRequest`

to `HttpRequestData`

and `IActionResult`

to `HttpResponseData`

, depending on if you are using [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) or not.

Messages are sent to the queue when the function completes. The way you define the output binding depends on your process model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=csharp#manually-add-bindings-based-on-examples).

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
```


For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=java#manually-add-bindings-based-on-examples).

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


The way you define the output binding depends on the version of your Node.js model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=javascript#manually-add-bindings-based-on-examples).

```
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
```


For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=powershell#manually-add-bindings-based-on-examples).

```
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
```


The way you define the output binding depends on the version of your Python model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=python#manually-add-bindings-based-on-examples).

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


The way you define the output binding depends on the version of your Node.js model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=typescript#manually-add-bindings-based-on-examples).

Use the following table to find examples of specific binding types that you can use to guide you in updating an existing function. First, choose the language tab that corresponds to your project.

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

[Link](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python)[Trigger](functions-bindings-cosmosdb-v2-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-cosmosdb-v2-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-cosmosdb-v2-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-cosmosdb)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-python#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-python#examples)[Trigger](functions-bindings-azure-sql-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-azure-sql-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-azure-sql-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python)[Trigger](functions-bindings-event-grid-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-grid-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-hubs-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-hubs-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-iot-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-iot-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-http-azd)[Trigger](functions-bindings-storage-queue-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-storage-queue-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-rabbitmq-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-rabbitmq-output?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-sendgrid?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-service-bus-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-service-bus-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-service-bus)[Trigger](functions-bindings-signalr-service-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-signalr-service-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-signalr-service-output?tabs=python-v2&pivots=programming-language-python)[Input](functions-bindings-storage-table-input?tabs=python-v2&pivots=programming-language-python)[Output](functions-bindings-storage-table-output?tabs=python-v2&pivots=programming-language-python)[Trigger](functions-bindings-timer?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-twilio?tabs=python-v2&pivots=programming-language-python#example)### Visual Studio Code

When you use Visual Studio Code to develop your function and your function uses a function.json file, the Azure Functions extension can automatically add a binding to an existing function.json file. To learn more, see [Add input and output bindings](functions-develop-vs-code#add-input-and-output-bindings).

## Azure portal

When you develop your functions in the [Azure portal](https://portal.azure.com), you add input and output bindings in the **Integrate** tab for a given function. The new bindings are added to either the function.json file or to the method attributes, depending on your language. The following articles show examples of how to add bindings to an existing function in the portal:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob -->

# Azure Blob storage bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with [Azure Storage](../storage/) via [triggers and bindings](functions-triggers-bindings). Integrating with Blob storage allows you to build functions that react to changes in blob data as well as read and write values.

| Action | Type |
|---|---|
| Run a function as blob storage data changes |
|

[Input binding](functions-bindings-storage-blob-input)[Output binding](functions-bindings-storage-blob-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [Azure.Storage.Blobs](/en-us/dotnet/api/azure.storage.blobs). Learn more about how these new types are different from `WindowsAzure.Storage`

and `Microsoft.Azure.Storage`

and how to migrate to them from the [Azure.Storage.Blobs Migration Guide](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/storage/Azure.Storage.Blobs/AzureStorageNetMigrationV12.md).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs), version 5.x or later.

Using the .NET CLI:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs
```


Note

Azure Blobs, Azure Queues, and Azure Tables now use separate extensions and are referenced individually. For example, to use the triggers and bindings for all three services in your .NET isolated-process app, you should add the following packages to your project:

[Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs)[Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues)[Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables)

Previously, the extensions shipped together as [Microsoft.Azure.Functions.Worker.Extensions.Storage, version 4.x](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/4.0.4). This same package also has a [5.x version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/5.0.0), which references the split packages for blobs and queues only. When upgrading your package references from older versions, you may therefore need to additionally reference the new [Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) NuGet package. Also, when referencing these newer split packages, make sure you are not referencing an older version of the combined storage package, as this will result in conflicts from two definitions of the same bindings.

If you're writing your application using F#, you must also configure this extension as part of the app's [startup configuration](dotnet-isolated-process-guide#start-up-and-configuration). In the call to `ConfigureFunctionsWorkerDefaults()`

or `ConfigureFunctionsWebApplication()`

, add a delegate that takes an `IFunctionsWorkerApplication`

parameter. Then within the body of that delegate, call `ConfigureBlobStorageExtension()`

on the object:

```
let hostBuilder = new HostBuilder()
hostBuilder.ConfigureFunctionsWorkerDefaults(fun (context: HostBuilderContext) (appBuilder: IFunctionsWorkerApplicationBuilder) ->
appBuilder.ConfigureBlobStorageExtension() |> ignore
) |> ignore
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

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below.

**Blob trigger**

The blob trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Blob input binding**

When you want the function to process a single blob, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)1When you want the function to process multiple blobs from a container, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` or `List<T>` where `T` is one of the single blob input binding types |
An array or list of multiple blobs. Each entry represents one blob from the container. You can also bind to any interfaces implemented by these types, such as `IEnumerable<T>` . |
1 |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/6.0.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Blob output binding**

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

## SDK Binding Types

SDK Types for Azure Storage Blob are generally available! Follow the [Python SDK Bindings for Blob Sample](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python) to get started with SDK Types for Blob in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| Blob trigger |
|

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_blobclient/function_app.py)`BlobClient`

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py)`ContainerClient`

`StorageStreamDownloader`

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient),[ContainerClient](/en-us/python/api/azure-storage-blob/azure.storage.blob.containerclient),[StorageStreamDownloader](/en-us/python/api/azure-storage-blob/azure.storage.blob.storagestreamdownloader)[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_blobclient/function_app.py)`BlobClient`

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py)`ContainerClient`

`StorageStreamDownloader`

## host.json settings

This section describes the function app configuration settings available for functions that use this binding. These settings only apply when using extension version 5.0.0 and higher. The example host.json file below contains only the version 2.x+ settings for this binding. For more information about function app configuration settings in versions 2.x and later versions, see [host.json reference for Azure Functions](functions-host-json).

Note

This section doesn't apply to extension versions before 5.0.0. For those earlier versions, there aren't any function app-wide configuration settings for blobs.

```
{
"version": "2.0",
"extensions": {
"blobs": {
"maxDegreeOfParallelism": 4,
"poisonBlobThreshold": 1
}
}
}
```


| Property | Default | Description |
|---|---|---|
| maxDegreeOfParallelism | 8 * (the number of available cores) | The integer number of concurrent invocations allowed for all blob-triggered functions in a given function app. The minimum allowed value is 1. |
| poisonBlobThreshold | 5 | The integer number of times to try processing a message before moving it to the poison queue. The minimum allowed value is 1. |

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/container-concepts -->

# Linux container support in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you plan and develop your individual functions to run in Azure Functions, you're typically focused on the code itself. Azure Functions makes it easy to deploy just your code project to a function app in Azure. When you deploy your project to a Linux function app, your code runs in a container that is created for you automatically and seamlessly integrates with Functions management tools.

Functions also supports containerized function app deployments. In a containerized deployment, you create your own function app instance in a local Docker container from a supported based image. You can then deploy this *containerized* function app to a hosting environment in Azure. Creating your own function app container lets you customize or otherwise control the immediate runtime environment of your function code.

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

## Container hosting options

There are several options for hosting your containerized function apps in Azure:

| Hosting option | Benefits |
|---|---|
|
Azure Functions provides integrated support for developing, deploying, and managing containerized function apps on
Recommended hosting option for containerized function apps n Azure. |

**Azure Arc-enabled Kubernetes clusters (preview)***Hosting Azure Functions containers on Azure Arc-enabled Kubernetes clusters is currently in preview.*For more information, see[Working with containers and Azure Functions](functions-how-to-custom-container?pivots=azure-arc).[Azure Functions](functions-how-to-custom-container?pivots=azure-functions#azure-portal-create-using-containers)[Elastic Premium](functions-premium-plan)or an[App Service (Dedicated)](dedicated-plan)plan. Use Container Apps hosting for rich container support from Container Apps. Premium plan hosting provides you with the benefits of dynamic scaling. You might want to use Dedicated plan hosting to take advantage of existing unused App Service plan resources.[Kubernetes](functions-kubernetes-keda)[KEDA](https://keda.sh)(Kubernetes-based Event Driven Autoscaling) pairs seamlessly with the Azure Functions runtime and tooling to provide event driven scale in Kubernetes.**Important:**Kubernetes hosting of your containerized function apps, either by using KEDA or by direct deployment, is an open-source effort that you can use free of cost.*Best-effort*support for this hosting scenario is provided only by contributors and by the community. You're responsible for maintaining your own function app containers in a cluster, even when deploying them to Azure Kubernetes Service (AKS).## Feature support comparison

The degree to which various features and behaviors of Azure Functions are supported when running your function app in a container depends on the container hosting option you choose.

| Feature/behavior |
|
|---|

[Container Apps (direct)](../container-apps/overview)

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)

[Kubernetes](functions-kubernetes-keda)

[Event-driven scaling](event-driven-scaling)5[scale rules](../container-apps/scale-app#scale-rules))1123[Scale-to-zero instances](event-driven-scaling#scale-in-behaviors)6678[Core Tools deployment](functions-run-local#deploy-containers)`func kubernetes`

[Revisions](../container-apps/revisions)[Yes](../container-apps/revisions)[Deployment slots](functions-deployment-slots)[Streaming logs](streaming-logs)[Yes](../container-apps/log-streaming)[Yes](../container-apps/log-streaming)[Console access](../container-apps/container-console)[Yes](../container-apps/container-console)[Kudu](functions-how-to-custom-container#enable-ssh-connections))[Kudu](functions-how-to-custom-container#enable-ssh-connections))[using](https://kubernetes.io/docs/reference/kubectl/))`kubectl`

[Scale rules](../container-apps/scale-app#scale-rules)[Always-ready/pre-warmed instances](functions-premium-plan#eliminate-cold-starts)[App Service authentication](../app-service/overview-authentication-authorization)[Yes](../container-apps/authentication)[Custom domain names](../app-service/app-service-web-tutorial-custom-domain)[Yes](../container-apps/custom-domains-certificates)[Private key certificates](../app-service/overview-tls)[Yes](../container-apps/custom-domains-certificates)[Yes](../container-apps/networking)[Yes](/en-us/azure/reliability/reliability-azure-container-apps)[Yes](../container-apps/troubleshooting#use-the-diagnose-and-solve-problems-tool)[Yes](../container-apps/troubleshooting#use-the-diagnose-and-solve-problems-tool)[Yes](functions-diagnostics)[Yes](functions-diagnostics)[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[Configurable memory/CPU count](../container-apps/workload-profiles-overview)[Yes](../container-apps/billing#consumption-plan)[Yes](../container-apps/billing#consumption-plan)[Container Apps billing](../container-apps/billing)[Container Apps billing](../container-apps/billing)[Premium plan billing](functions-premium-plan#billing)[Dedicated plan billing](dedicated-plan#billing)[AKS pricing](/en-us/azure/aks/free-standard-pricing-tiers)- On Container Apps, the default is 10 instances, but you can set the
[maximum number of replicas](../container-apps/scale-app#scale-definition), which has an overall maximum of 1000. This setting is honored as long as there's enough cores quota available. When you create your function app from the Azure portal, you're limited to 300 instances. - In some regions, Linux apps on a Premium plan can scale to 100 instances. For more information, see the
[Premium plan article](functions-premium-plan#region-max-scale-out). - For specific limits for the various App Service plan options, see the
[App Service plan limits](../azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits). - Requires
[KEDA](functions-kubernetes-keda); supported by most triggers. To learn which triggers support event-driven scaling, see[Considerations for Container Apps hosting](functions-container-apps-hosting#considerations-for-container-apps-hosting). - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to zero, the default timeout depends on the specific triggers used in the app. - There's no maximum execution timeout duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors), and a grace period of 10 minutes is given during platform updates. - Requires the App Service plan be set to
[Always On](dedicated-plan#always-on). A grace period of 10 minutes is given during platform updates.

## Maintaining custom containers

When creating your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific and are found in the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container.

Choose your base image based on the language stack you're using in your function app. The following table provides examples for each stack. In general, the tag should start with `4-`

to indicate the V4 Functions runtime. When new minor versions are released, this tag will be updated to point to the new version. As you periodically rebuild your custom image, you will pull the new versions through that same tag, allowing your app to have the same updates. You shouldn't use tags that specify minor runtime versions, as these will not receive updates, and your app will potentially remain on an unpatched version, no matter how often you rebuild your custom image.

| Language Stack | Example recommended base image tags |
|---|---|
| .NET (isolated worker model) | `mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0` or`mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0-appservice` (These examples target .NET 8. Select the appropriate image for the .NET version you need.) |
| .NET (legacy in-process model) | `mcr.microsoft.com/azure-functions/dotnet:4-dotnet8.0` or`mcr.microsoft.com/azure-functions/dotnet:4-dotnet8.0-appservice` (Support will end for the in-process model on November 10, 2026. You should
|
| Java | `mcr.microsoft.com/azure-functions/java:4-java21` or`mcr.microsoft.com/azure-functions/java:4-java21-appservice` (These examples target Java 21. Select the appropriate image for the Java version you need.) |
| Node.js (JavaScript or TypeScript) | `mcr.microsoft.com/azure-functions/node:4-node22` or`mcr.microsoft.com/azure-functions/node:4-node22-appservice` (These examples target Node.js 22. Select the appropriate image for the Node.js version you need.) |
| PowerShell | `mcr.microsoft.com/azure-functions/powershell:4-powershell7.4` or`mcr.microsoft.com/azure-functions/powershell:4-powershell7.4-appservice` (These examples target PowerShell 7.4. Select the appropriate image for the PowerShell version you need.) |
| Python | `mcr.microsoft.com/azure-functions/python:4-python3.12` or`mcr.microsoft.com/azure-functions/python:4-python3.12-appservice` (These examples target Python 3.12. Select the appropriate image for the Python version you need.) |
| Custom handlers / other | `mcr.microsoft.com/azure-functions/base:4` or`mcr.microsoft.com/azure-functions/base:4-appservice` |

Base images ending in `-appservice`

enable SSH and remote debugging from the platform. Unless you need these capabilities, you can use the base images without the `-appservice`

suffix.

Important

It isn't sufficient to just have one of the above tags in your Dockerfile. You need to regularly pull the latest image from that tag so that your custom image can be rebuilt to include the latest updates. If you don't pull the latest image and rebuild, your app will continue to run on the old base image.

When you create or deploy your own containerized app using a custom image, you're responsible for making sure that your custom image staying up-to-date with our released base images. In addition to new features and improvements, these base image updates can also include security updates that are critical for your app. To ensure your app is protected, make sure you're staying up to date. You should regularly pull the latest version of the base image, rebuild your custom container image, and redeploy your app to use it.

In some cases, we're required to make platform-level changes that could mean that an app in a custom container using an old base image might stop working properly. For such major changes, we roll out updated images well in advance so that apps that take regular updates aren't negatively impacted. To avoid potential problems with your apps running in custom containers, make sure you don't fall too far behind the latest minor version released. During a support case, should we determine that your app is experiencing problems because it's on an older or unsupported version, we do request that you update your container to the latest base image version before continuing with support.

## Getting started

Use these links to get started working with Azure Functions in Linux containers:

| I want to... | See article: |
|---|---|
| Create my first containerized functions |
|

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb -->

# Azure Cosmos DB bindings for Azure Functions 1.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

This article explains how to work with [Azure Cosmos DB](/en-us/azure/cosmos-db/serverless-computing-database) bindings in Azure Functions. Azure Functions supports trigger, input, and output bindings for Azure Cosmos DB.

Keep these important considerations in mind when using the Azure Cosmos DB binding for the Functions v1.x runtime:

This article is for Azure Functions 1.x. We recommend that you run your functions on the most recent version of the Functions runtime. For information about how to use these bindings in the latest Functions runtime, see

[Azure Cosmos DB bindings for Azure Functions 2.x](functions-bindings-cosmosdb-v2).This binding was originally named DocumentDB. In Azure Functions version 1.x, only the trigger was renamed Azure Cosmos DB; the input binding, output binding, and NuGet package retain the DocumentDB name.

Azure Cosmos DB bindings are only supported for use with the SQL API. For all other Azure Cosmos DB APIs, you should access the database from your function by using the static client for your API, including

[Azure Cosmos DB for MongoDB](/en-us/azure/cosmos-db/mongodb-introduction),[Azure Cosmos DB for Apache Cassandra](/en-us/azure/cosmos-db/cassandra-introduction),[Azure Cosmos DB for Apache Gremlin](/en-us/azure/cosmos-db/graph-introduction), and[Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table-introduction).The Azure Cosmos DB bindings for the Functions v1.x runtime don't support Microsoft Entra authentication and managed identities. To improve security, you should upgrade to run on the latest version of the Functions runtime.


## Packages - Functions 1.x

The Azure Cosmos DB bindings for Functions version 1.x are provided in the [Microsoft.Azure.WebJobs.Extensions.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB) NuGet package, version 1.x. Source code for the bindings is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/v2.x/src/WebJobs.Extensions.DocumentDB) GitHub repository.

The following table lists how to add support for output binding in each development environment.

| Development environment | To add support in Functions 1.x |
|---|---|
| Local development: C# class library |
|

## Trigger

The Azure Cosmos DB Trigger uses the [Azure Cosmos DB Change Feed](/en-us/azure/cosmos-db/change-feed) to listen for inserts and updates across partitions. The change feed publishes inserts and updates, not deletions.

## Trigger - example

The following example shows an [in-process C# function](functions-dotnet-class-library) that is invoked when there are inserts or updates in the specified database and collection.

```
using Microsoft.Azure.Documents;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
namespace CosmosDBSamplesV1
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
LeaseCollectionName = "leases",
CreateLeaseCollectionIfNotExists = true)]IReadOnlyList<Document> documents,
TraceWriter log)
{
if (documents != null && documents.Count > 0)
{
log.Info($"Documents modified: {documents.Count}");
log.Info($"First document Id: {documents[0].Id}");
}
}
}
}
```


## Trigger - attributes

For [in-process C# class libraries](functions-dotnet-class-library), use the [CosmosDBTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) attribute.

The attribute's constructor takes the database name and collection name. For information about those settings and other properties that you can configure, see [Trigger - configuration](#trigger---configuration). Here's a `CosmosDBTrigger`

attribute example in a method signature:

```
[FunctionName("DocumentUpdates")]
public static void Run(
[CosmosDBTrigger("database", "collection", ConnectionStringSetting = "myCosmosDB")]
IReadOnlyList<Document> documents,
TraceWriter log)
{
...
}
```


For a complete example, see [Trigger - C# example](#trigger).

## Trigger - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDBTrigger`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `cosmosDBTrigger` . |
direction |
n/a | Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
name |
n/a | The variable name used in function code that represents the list of documents with changes. |
connectionStringSetting |
ConnectionStringSetting |
The name of an app setting that contains the connection string used to connect to the Azure Cosmos DB account being monitored. |
databaseName |
DatabaseName |
The name of the Azure Cosmos DB database with the collection being monitored. |
collectionName |
CollectionName |
The name of the collection being monitored. |
leaseConnectionStringSetting |
LeaseConnectionStringSetting |
(Optional) The name of an app setting that contains the connection string to the service which holds the lease collection. When not set, the `connectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
leaseDatabaseName |
LeaseDatabaseName |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. This parameter is automatically set when the binding is created in the portal. |
leaseCollectionName |
LeaseCollectionName |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
createLeaseCollectionIfNotExists |
CreateLeaseCollectionIfNotExists |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
leasesCollectionThroughput |
LeasesCollectionThroughput |
(Optional) Defines the amount of Request Units to assign when the leases collection is created. This setting is only used When `createLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
leaseCollectionPrefix |
LeaseCollectionPrefix |
(Optional) When set, it adds a prefix to the leases created in the Lease collection for this Function, effectively allowing two separate Azure Functions to share the same Lease collection by using different prefixes. |
feedPollDelay |
FeedPollDelay |
(Optional) When set, it defines, in milliseconds, the delay in between polling a partition for new changes on the feed, after all current changes are drained. Default is 5000 (5 seconds). |
leaseAcquireInterval |
LeaseAcquireInterval |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
leaseExpirationInterval |
LeaseExpirationInterval |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
leaseRenewInterval |
LeaseRenewInterval |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
checkpointFrequency |
CheckpointFrequency |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
maxItemsPerInvocation |
MaxItemsPerInvocation |
(Optional) When set, it customizes the maximum amount of items received per Function call. |
startFromBeginning |
StartFromBeginning |
(Optional) When set, it tells the Trigger to start reading changes from the beginning of the history of the collection instead of the current time. This only works the first time the Trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this to `true` when there are leases already created has no effect. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Trigger - usage

The trigger requires a second collection that it uses to store *leases* over the partitions. Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `LeaseCollectionPrefix`

for each function. Otherwise, only one of the functions will be triggered. For information about the prefix, see the [Configuration section](#trigger---configuration).

The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself. If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.

## Input

The Azure Cosmos DB input binding uses the SQL API to retrieve one or more Azure Cosmos DB documents and passes them to the input parameter of the function. The document ID or query parameters can be determined based on the trigger that invokes the function.

## Input - example

This section contains the following examples:

[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-c)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-c)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-c)[HTTP trigger, look up ID from route data, using SqlQuery](#http-trigger-look-up-id-from-route-data-using-sqlquery-c)[HTTP trigger, get multiple docs, using SqlQuery](#http-trigger-get-multiple-docs-using-sqlquery-c)[HTTP trigger, get multiple docs, using DocumentClient](#http-trigger-get-multiple-docs-using-documentclient-c)

The examples refer to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV1
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


### Queue trigger, look up ID from JSON

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by a queue message that contains a JSON object. The queue trigger parses the JSON into an object named `ToDoItemLookup`

, which contains the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
namespace CosmosDBSamplesV1
{
public class ToDoItemLookup
{
public string ToDoItemId { get; set; }
}
}
```


```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromJSON
{
[FunctionName("DocByIdFromJSON")]
public static void Run(
[QueueTrigger("todoqueueforlookup")] ToDoItemLookup toDoItemLookup,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
Id = "{ToDoItemId}")]ToDoItem toDoItem,
TraceWriter log)
{
log.Info($"C# Queue trigger function processed Id={toDoItemLookup?.ToDoItemId}");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
}
}
}
```


### HTTP trigger, look up ID from query string

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromQueryString
{
[FunctionName("DocByIdFromQueryString")]
public static HttpResponseMessage Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
Id = "{Query.id}")] ToDoItem toDoItem,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, look up ID from route data

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromRouteData
{
[FunctionName("DocByIdFromRouteData")]
public static HttpResponseMessage Run(
[HttpTrigger(
AuthorizationLevel.Anonymous, "get", "post",
Route = "todoitems/{id}")]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
Id = "{id}")] ToDoItem toDoItem,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, look up ID from route data, using SqlQuery

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromRouteDataUsingSqlQuery
{
[FunctionName("DocByIdFromRouteDataUsingSqlQuery")]
public static HttpResponseMessage Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post",
Route = "todoitems2/{id}")]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
SqlQuery = "select * from ToDoItems r where r.id = {id}")] IEnumerable<ToDoItem> toDoItems,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
foreach (ToDoItem toDoItem in toDoItems)
{
log.Info(toDoItem.Description);
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, get multiple docs, using SqlQuery

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a list of documents. The function is triggered by an HTTP request. The query is specified in the `SqlQuery`

attribute property.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocsBySqlQuery
{
[FunctionName("DocsBySqlQuery")]
public static HttpResponseMessage Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]
HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
SqlQuery = "SELECT top 2 * FROM c order by c._ts desc")]
IEnumerable<ToDoItem> toDoItems,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
foreach (ToDoItem toDoItem in toDoItems)
{
log.Info(toDoItem.Description);
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, get multiple docs, using DocumentClient (C#)

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a list of documents. The function is triggered by an HTTP request. The code uses a `DocumentClient`

instance provided by the Azure Cosmos DB binding to read a list of documents. The `DocumentClient`

instance could also be used for write operations.

```
using Microsoft.Azure.Documents.Client;
using Microsoft.Azure.Documents.Linq;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System;
using System.Linq;
using System.Net;
using System.Net.Http;
using System.Threading.Tasks;
namespace CosmosDBSamplesV1
{
public static class DocsByUsingDocumentClient
{
[FunctionName("DocsByUsingDocumentClient")]
public static async Task<HttpResponseMessage> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection")] DocumentClient client,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
Uri collectionUri = UriFactory.CreateDocumentCollectionUri("ToDoItems", "Items");
string searchterm = req.GetQueryNameValuePairs()
.FirstOrDefault(q => string.Compare(q.Key, "searchterm", true) == 0)
.Value;
if (searchterm == null)
{
return req.CreateResponse(HttpStatusCode.NotFound);
}
log.Info($"Searching for word: {searchterm} using Uri: {collectionUri.ToString()}");
IDocumentQuery<ToDoItem> query = client.CreateDocumentQuery<ToDoItem>(collectionUri)
.Where(p => p.Description.Contains(searchterm))
.AsDocumentQuery();
while (query.HasMoreResults)
{
foreach (ToDoItem result in await query.ExecuteNextAsync())
{
log.Info(result.Description);
}
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


## Input - attributes

In [in-process C# class libraries](functions-dotnet-class-library), use the [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) attribute.

The attribute's constructor takes the database name and collection name. For information about those settings and other properties that you can configure, see [the following configuration section](#input---configuration).

## Input - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `DocumentDB`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `documentdb` . |
direction |
n/a | Must be set to `in` . |
name |
n/a | Name of the binding parameter that represents the document in the function. |
databaseName |
DatabaseName |
The database containing the document. |
collectionName |
CollectionName |
The name of the collection that contains the document. |
id |
Id |
The ID of the document to retrieve. This property supports
id and sqlQuery properties. If you don't set either one, the entire collection is retrieved. |

**sqlQuery****SqlQuery**`SELECT * FROM c where c.departmentId = {departmentId}`

. Don't set both the **id**and**sqlQuery**properties. If you don't set either one, the entire collection is retrieved.**connection****ConnectionStringSetting****partitionKey****PartitionKey**When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Input - usage

When the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.

## Output

The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.

## Output - example

This section contains the following examples:

- Queue trigger, write one doc
- Queue trigger, write docs using
`IAsyncCollector`


The examples refer to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV1
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


### Queue trigger, write one doc

The following example shows a [C# function](functions-dotnet-class-library) that adds a document to a database, using data provided in message from Queue storage.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System;
namespace CosmosDBSamplesV1
{
public static class WriteOneDoc
{
[FunctionName("WriteOneDoc")]
public static void Run(
[QueueTrigger("todoqueueforwrite")] string queueMessage,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection")]out dynamic document,
TraceWriter log)
{
document = new { Description = queueMessage, id = Guid.NewGuid() };
log.Info($"C# Queue trigger function inserted one row");
log.Info($"Description={queueMessage}");
}
}
}
```


### Queue trigger, write docs using IAsyncCollector

The following example shows a [C# function](functions-dotnet-class-library) that adds a collection of documents to a database, using data provided in a queue message JSON.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Threading.Tasks;
namespace CosmosDBSamplesV1
{
public static class WriteDocsIAsyncCollector
{
[FunctionName("WriteDocsIAsyncCollector")]
public static async Task Run(
[QueueTrigger("todoqueueforwritemulti")] ToDoItem[] toDoItemsIn,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection")]
IAsyncCollector<ToDoItem> toDoItemsOut,
TraceWriter log)
{
log.Info($"C# Queue trigger function processed {toDoItemsIn?.Length} items");
foreach (ToDoItem toDoItem in toDoItemsIn)
{
log.Info($"Description={toDoItem.Description}");
await toDoItemsOut.AddAsync(toDoItem);
}
}
}
}
```


## Output - attributes

In [in-process C# class libraries](functions-dotnet-class-library), use the [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) attribute.

The attribute's constructor takes the database name and collection name. For information about those settings and other properties that you can configure, see [Output - configuration](#output---configuration). Here's a `DocumentDB`

attribute example in a method signature:

```
[FunctionName("QueueToDocDB")]
public static void Run(
[QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
[DocumentDB("ToDoList", "Items", Id = "id", ConnectionStringSetting = "myCosmosDB")] out dynamic document)
{
...
}
```


For a complete example, see [Output](#output).

## Output - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `DocumentDB`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `documentdb` . |
direction |
n/a | Must be set to `out` . |
name |
n/a | Name of the binding parameter that represents the document in the function. |
databaseName |
DatabaseName |
The database containing the collection where the document is created. |
collectionName |
CollectionName |
The name of the collection where the document is created. |
createIfNotExists |
CreateIfNotExists |
A boolean value to indicate whether the collection is created when it doesn't exist. The default is false because new collections are created with reserved throughput, which has cost implications. For more information, see the
|
partitionKey |
PartitionKey |
When `CreateIfNotExists` is true, defines the partition key path for the created collection. |
collectionThroughput |
CollectionThroughput |
When `CreateIfNotExists` is true, defines the
|
connection |
ConnectionStringSetting |
The name of the app setting containing your Azure Cosmos DB connection string. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Output - usage

By default, when you write to the output parameter in your function, a document is created in your database. This document has an automatically generated GUID as the document ID. You can specify the document ID of the output document by specifying the `id`

property in the JSON object passed to the output parameter.

Note

When you specify the ID of an existing document, it gets overwritten by the new output document.

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Azure Cosmos DB |
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/how-to-create-function-azure-cli -->

# Quickstart: Create a function in Azure from the command line

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you use local command-line tools to create a function that responds to HTTP requests. After verifying your code locally, you deploy it to a serverless Flex Consumption hosting plan in Azure Functions.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

Make sure to select your preferred development language at the top of the article.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

[Java 17 Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure)- If you use another
[supported version of Java](supported-languages?pivots=programming-language-java#languages-by-runtime-version), you must update the project's pom.xml file. - The
`JAVA_HOME`

environment variable must be set to the install location of the correct version of the Java Development Kit (JDK).

- If you use another
[Apache Maven 3.8.x](https://maven.apache.org)

The

, used to parse JSON output, and is also available in Azure Cloud Shell.`jq`

command line JSON processor

## Install the Azure Functions Core Tools

The recommended way to install Core Tools depends on the operating system of your local development computer.

The following steps use a Windows installer (MSI) to install Core Tools v4.x. For more information about other package-based installers, see the [Core Tools readme](https://github.com/Azure/azure-functions-core-tools/blob/v4.x/README.md#windows).

Download and run the Core Tools installer, based on your version of Windows:

[v4.x - Windows 64-bit](https://go.microsoft.com/fwlink/?linkid=2174087)(Recommended.[Visual Studio Code debugging](functions-develop-vs-code#debugging-functions-locally)requires 64-bit.)[v4.x - Windows 32-bit](https://go.microsoft.com/fwlink/?linkid=2174159)

If you previously used Windows installer (MSI) to install Core Tools on Windows, you should uninstall the old version from Add Remove Programs before installing the latest version.

Tip

To install Core Tools on [Windows Subsystem for Linux (WSL)](/en-us/windows/wsl/install), follow the instructions on the Linux tab.

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

## Create a local code project and function

In Azure Functions, your code project is an app that contains one or more individual functions that each respond to a specific trigger. All functions in a project share the same configurations and are deployed as a unit to Azure. In this section, you create a code project that contains a single function.

In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime dotnet-isolated`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime node --language javascript`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime powershell`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime python`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime node --language typescript`


In a terminal or command prompt, run this

command to create a function app project in the current folder:`func init`

`func init --worker-runtime custom`


In an empty folder, run this

`mvn`

command to generate the code project from an Azure Functions[Maven archetype](https://maven.apache.org/guides/introduction/introduction-to-archetypes.html):`mvn archetype:generate -DarchetypeGroupId=com.microsoft.azure -DarchetypeArtifactId=azure-functions-archetype -DjavaVersion=17`

Important

- Use
`-DjavaVersion=11`

if you want your functions to run on Java 11. To learn more, see[Java versions](functions-reference-java#java-versions). - Set the
`JAVA_HOME`

environment variable to the install location of the correct version of the JDK to complete this article.

- Use
Maven asks you for values needed to finish generating the project on deployment.


Provide the following values when prompted:Prompt Value Description **groupId**`com.fabrikam`

A value that uniquely identifies your project across all projects, following the [package naming rules](https://docs.oracle.com/javase/specs/jls/se6/html/packages.html#7.7)for Java.**artifactId**`fabrikam-functions`

A value that is the name of the jar, without a version number. **version**`1.0-SNAPSHOT`

Choose the default value. **package**`com.fabrikam`

A value that is the Java package for the generated function code. Use the default. Type

`Y`

or press Enter to confirm.Maven creates the project files in a new folder with a name of

*artifactId*, which in this example is`fabrikam-functions`

.Navigate into the project folder:

`cd fabrikam-functions`

You can review the template-generated code for your new HTTP trigger function in

*Function.java*in the*\src\main\java\com\fabrikam*project directory.

Use this

command to add a function to your project:`func new`

`func new --name HttpExample --template "HTTP trigger" --authlevel "function"`

A new code file is added to your project. In this case, the

`--name`

argument is the unique name of your function (`HttpExample`

) and the`--template`

argument specifies an HTTP trigger.

The project root folder contains various files for the project, including configurations files named [local.settings.json](functions-develop-local#local-settings-file) and [host.json](functions-host-json). Because *local.settings.json* can contain secrets downloaded from Azure, the file is excluded from source control by default in the *.gitignore* file.

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

Verify your new function by running the project locally and calling the function endpoint.

Use this command to start the local Azure Functions runtime host in the root of the project folder:

`func start`

`npm install npm start`

`mvn clean package mvn azure-functions:run`

Toward the end of the output, the following lines appear:

... Now listening on: http://0.0.0.0:7071 Application started. Press Ctrl+C to shut down. Http Functions: HttpExample: [GET,POST] http://localhost:7071/api/HttpExample ...

Copy the URL of your

`HttpExample`

function from this output to a browser and browse to the function URL. You should receive a success response with a "hello world" message.Note

Because access key authorization isn't enforced when running locally, the function URL returned doesn't include the access key value and you don't need it to call your function.

When you're done, use

**Ctrl**+**C**and choose`y`

to stop the functions host.

## Create supporting Azure resources for your function

Before you can deploy your function code to Azure, you need to create these resources:

- A
[resource group](../azure-resource-manager/management/overview), which is a logical container for related resources. - A default
[Storage account](../storage/common/storage-account-create), which is used by the Functions host to maintain state and other information about your functions. - A
[user-assigned managed identity](/en-us/azure/active-directory/managed-identities-azure-resources/overview), which the Functions host uses to connect to the default storage account. - A function app, which provides the environment for executing your function code. A function app maps to your local function project and lets you group functions as a logical unit for easier management, deployment, and sharing of resources.

Use the Azure CLI commands in these steps to create the required resources.

If you haven't done so already, sign in to Azure:

`az login`

The

command signs you into your Azure account. Skip this step when running in Azure Cloud Shell.`az login`

If you haven't already done so, use this

command to install the Application Insights extension:`az extension add`

`az extension add --name application-insights`

Use this

[az group create](/en-us/cli/azure/group#az-group-create)command to create a resource group named`AzureFunctionsQuickstart-rg`

in your chosen region:`az group create --name "AzureFunctionsQuickstart-rg" --location "<REGION>"`

In this example, replace

`<REGION>`

with a region near you that supports the Flex Consumption plan. Use the[az functionapp list-flexconsumption-locations](/en-us/cli/azure/functionapp#az-functionapp-list-flexconsumption-locations)command to view the list of currently supported regions.Use this

[az storage account create](/en-us/cli/azure/storage/account#az-storage-account-create)command to create a general-purpose storage account in your resource group and region:`az storage account create --name <STORAGE_NAME> --location "<REGION>" --resource-group "AzureFunctionsQuickstart-rg" \ --sku "Standard_LRS" --allow-blob-public-access false --allow-shared-key-access false`

In this example, replace

`<STORAGE_NAME>`

with a name that is appropriate to you and unique in Azure Storage. Names must contain three to 24 characters numbers and lowercase letters only.`Standard_LRS`

specifies a general-purpose account, which is[supported by Functions](storage-considerations#storage-account-requirements). This new account can only be accessed by using Microsoft Entra-authenticated identities that have been granted permissions to specific resources.Use this script to create a user-assigned managed identity, parse the returned JSON properties of the object using

`jq`

, and grant`Storage Blob Data Owner`

permissions in the default storage account:`output=$(az identity create --name "func-host-storage-user" --resource-group "AzureFunctionsQuickstart-rg" --location <REGION> \ --query "{userId:id, principalId: principalId, clientId: clientId}" -o json) userId=$(echo $output | jq -r '.userId') principalId=$(echo $output | jq -r '.principalId') clientId=$(echo $output | jq -r '.clientId') storageId=$(az storage account show --resource-group "AzureFunctionsQuickstart-rg" --name <STORAGE_NAME> --query 'id' -o tsv) az role assignment create --assignee-object-id $principalId --assignee-principal-type ServicePrincipal \ --role "Storage Blob Data Owner" --scope $storageId`

If you don't have the

`jq`

utility in your local Bash shell, it's available in Azure Cloud Shell. In this example, replace`<STORAGE_NAME>`

and`<REGION>`

with your default storage account name and region, respectively.The

[az identity create](/en-us/cli/azure/identity#az-identity-create)command creates an identity named`func-host-storage-user`

. The returned`principalId`

is used to assign permissions to this new identity in the default storage account by using thecommand. The`az role assignment create`

command is used to obtain the storage account ID.`az storage account show`

Use this

[az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create)command to create the function app in Azure:`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime dotnet-isolated --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime java --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime node --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime python --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime python --runtime-version <LANGUAGE_VERSION> --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

`az functionapp create --resource-group "AzureFunctionsQuickstart-rg" --name <APP_NAME> --flexconsumption-location <REGION> \ --runtime other --storage-account <STORAGE_NAME> \ --deployment-storage-auth-type UserAssignedIdentity --deployment-storage-auth-value "func-host-storage-user"`

In this example, replace these placeholders with the appropriate values:

`<APP_NAME>`

: a globally unique name appropriate to you. The`<APP_NAME>`

is also the default DNS domain for the function app.`<STORAGE_NAME>`

: the name of the account you used in the previous step.`<REGION>`

: your current region.`<LANGUAGE_VERSION>`

: use the same[supported language stack version](supported-languages)you verified locally, when applicable.

This command creates a function app running in your specified language runtime on Linux in the

[Flex Consumption Plan](flex-consumption-plan), which is free for the amount of usage you incur here. The command also creates an associated Azure Application Insights instance in the same resource group, with which you can use to monitor your function app executions and view logs. For more information, see[Monitor Azure Functions](functions-monitoring). The instance incurs no costs until you activate it.Use this script to add your user-assigned managed identity to the

[Monitoring Metrics Publisher](../role-based-access-control/built-in-roles/monitor#monitoring-metrics-publisher)role in your Application Insights instance:`appInsights=$(az monitor app-insights component show --resource-group "AzureFunctionsQuickstart-rg" \ --app <APP_NAME> --query "id" --output tsv) principalId=$(az identity show --name "func-host-storage-user" --resource-group "AzureFunctionsQuickstart-rg" \ --query principalId -o tsv) az role assignment create --role "Monitoring Metrics Publisher" --assignee $principalId --scope $appInsights`

In this example, replace

`<APP_NAME>`

with the name of your function app. The[az role assignment create](/en-us/cli/azure/role/assignment#az-role-assignment-create)command adds your user to the role. The resource ID of your Application Insights instance and the principal ID of your user are obtained by using the[az monitor app-insights component show](/en-us/cli/azure/monitor/app-insights/component#az-monitor-app-insights-component-show)andcommands, respectively.`az identity show`


## Update application settings

To enable the Functions host to connect to the default storage account by using shared secrets, replace the `AzureWebJobsStorage`

connection string setting with several settings that are prefixed with `AzureWebJobsStorage__`

. These settings define a complex setting that your app uses to connect to storage and Application Insights with a user-assigned managed identity.

Use this script to get the client ID of the user-assigned managed identity and uses it to define managed identity connections to both storage and Application Insights:

`clientId=$(az identity show --name func-host-storage-user \ --resource-group AzureFunctionsQuickstart-rg --query 'clientId' -o tsv) az functionapp config appsettings set --name <APP_NAME> --resource-group "AzureFunctionsQuickstart-rg" \ --settings AzureWebJobsStorage__accountName=<STORAGE_NAME> \ AzureWebJobsStorage__credential=managedidentity AzureWebJobsStorage__clientId=$clientId \ APPLICATIONINSIGHTS_AUTHENTICATION_STRING="ClientId=$clientId;Authorization=AAD"`

In this script, replace

`<APP_NAME>`

and`<STORAGE_NAME>`

with the names of your function app and storage account, respectively.Run the

[az functionapp config appsettings delete](/en-us/cli/azure/functionapp/config/appsettings#az-functionapp-config-appsettings-delete)command to remove the existing`AzureWebJobsStorage`

connection string setting, which contains a shared secret key:`az functionapp config appsettings delete --name <APP_NAME> --resource-group "AzureFunctionsQuickstart-rg" --setting-names AzureWebJobsStorage`

In this example, replace

`<APP_NAME>`

with the names of your function app.

At this point, the Functions host can connect to the storage account securely by using managed identities instead of shared secrets. You can now deploy your project code to the Azure resources.

## Deploy the function project to Azure

After you've successfully created your function app in Azure, you're now ready to deploy your local functions project by using the [ func azure functionapp publish](functions-run-local#project-file-deployment) command.

In your root project folder, run this

command:`func azure functionapp publish`

`func azure functionapp publish <APP_NAME>`

In this example, replace

`<APP_NAME>`

with the name of your app. A successful deployment shows results similar to the following output (truncated for simplicity):... Getting site publishing info... Creating archive for current directory... Performing remote build for functions project. ... Deployment successful. Remote build succeeded! Syncing triggers... Functions in msdocs-azurefunctions-qs: HttpExample - [httpTrigger] Invoke url: https://msdocs-azurefunctions-qs.azurewebsites.net/api/httpexample

In your local terminal or command prompt, run this command to get the URL endpoint value, including the access key:

`func azure functionapp list-functions <APP_NAME> --show-keys`

In this example, again replace

`<APP_NAME>`

with the name of your app.Copy the returned endpoint URL and key, which you use to invoke the function endpoint.


## Update the pom.xml file

After you successfully create your function app in Azure, update the pom.xml file so that Maven can deploy to your new app. Otherwise, Maven creates a new set of Azure resources during deployment.

In Azure Cloud Shell, use this

command to get the deployment container URL and ID of the new user-assigned managed identity:`az functionapp show`

`az functionapp show --name <APP_NAME> --resource-group AzureFunctionsQuickstart-rg \ --query "{userAssignedIdentityResourceId: properties.functionAppConfig.deployment.storage.authentication.userAssignedIdentityResourceId, \ containerUrl: properties.functionAppConfig.deployment.storage.value}"`

In this example, replace

`<APP_NAME>`

with the names of your function app.In the project root directory, open the pom.xml file in a text editor, locate the

`properties`

element, and update these specific property values:Property name Value `java.version`

Use the same [supported language stack version](supported-languages)you verified locally, such as`17`

.`azure.functions.maven.plugin.version`

`1.37.1`

`azure.functions.java.library.version`

`3.1.0`

`functionAppName`

The name of your function app in Azure. Find the

`configuration`

section of the`azure-functions-maven-plugin`

and replace it with this XML fragment:`<configuration> <appName>${functionAppName}</appName> <resourceGroup>AzureFunctionsQuickstart-rg</resourceGroup> <pricingTier>Flex Consumption</pricingTier> <region>....</region> <runtime> <os>linux</os> <javaVersion>${java.version}</javaVersion> </runtime> <deploymentStorageAccount>...</deploymentStorageAccount> <deploymentStorageResourceGroup>AzureFunctionsQuickstart-rg</deploymentStorageResourceGroup> <deploymentStorageContainer>...</deploymentStorageContainer> <storageAuthenticationMethod>UserAssignedIdentity</storageAuthenticationMethod> <userAssignedIdentityResourceId>...</userAssignedIdentityResourceId> <appSettings> <property> <name>FUNCTIONS_EXTENSION_VERSION</name> <value>~4</value> </property> </appSettings> </configuration>`

In the new

`configuration`

element, make these specific replacements of the ellipses (`...`

) values:Configuration Value `region`

The region code of your existing function app, such as `eastus`

.`deploymentStorageAccount`

The name of your storage account. `deploymentStorageContainer`

The name of the deployment share, which comes after the `\`

in the`containerUrl`

value you obtained.`userAssignedIdentityResourceId`

The fully qualified resource ID of your managed identity, which you obtained. Save your changes to the

*pom.xml*file.

You can now use Maven to deploy your code project to your existing app.

## Deploy the function project to Azure

From the command prompt, run this command:

`mvn clean package azure-functions:deploy`

After your deployment succeeds, run this Core Tools command to get the URL endpoint value, including the access key:

`func azure functionapp list-functions <APP_NAME> --show-keys`

In this example, again replace

`<APP_NAME>`

with the name of your app.Copy the returned endpoint URL and key, which you use to invoke the function endpoint.


## Invoke the function on Azure

Because your function uses an HTTP trigger and supports GET requests, you invoke it by making an HTTP request to its URL using the function-level access key. It's easiest to execute a GET request in a browser.

Paste the URL and access key you copied into a browser address bar.

The endpoint URL should look something like this example:

`https://contoso-app.azurewebsites.net/api/httpexample?code=aabbccdd...`


In this case, you must also provide an access key in the query string when making a GET request to the endpoint URL. Using an access key is recommended to limit access from random clients. When making a POST request using an HTTP client, you should instead provide the access key in the `x-functions-key`

header.

When you navigate to this URL, the browser should display similar output as when you ran the function locally.

## Clean up resources

If you continue to the [next step](#next-steps) and add an Azure Storage queue output binding, keep all your resources in place as you'll build on what you've already done.

Otherwise, use the following command to delete the resource group and all its contained resources to avoid incurring further costs.

```
az group delete --name AzureFunctionsQuickstart-rg
```
