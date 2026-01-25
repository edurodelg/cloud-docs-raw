---
merged_at: 2026-01-25T15:41:11.641753
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-reliable-event-processing_functions-bindings-cosmosdb-v2_opentelemet_b54673.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-reliable-event-processing_functions-bindings-cosmosdb-v2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-reliable-event-processing.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-reliable-event-processing -->

# Reliable event processing with Azure Functions and Event Hubs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to build robust, reliable serverless solutions using Azure Functions with Azure Event Hubs triggers. This article covers best practices for checkpoints, error handling, and implementing circuit breaker patterns to ensure no events are lost and your event-driven applications remain stable and resilient.

## Challenges of event streams in distributed systems

Consider a system that sends events at a constant rate of 100 events per second. At this rate, within minutes multiple parallel instances can consume the incoming 100 events every second.

However, consider these challenges to consuming an event stream:

- An event publisher sends a corrupt event.
- Your function code encounters an unhandled exception.
- A downstream system goes offline and blocks event processing.

Unlike an Azure Queue storage trigger, which locks messages during processing, Azure Event Hubs reads, per partition, from a single point in the stream. This read behavior, which is more like a video player, provides the desired benefits of high-throughput, multiple consumer groups, and replay-ability. Events are read, forward or backward, from a checkpoint, but you must move the pointer to process new events. For more information, see [Checkpoint](../event-hubs/event-processor-balance-partition-load#checkpoint) in the Event Hubs documentation.

When errors occur in a stream and you choose not to advance the pointer, further event processing is blocked. In other words, should you stop the pointer to deal with an issue processing a single event, the unprocessed events begin piling up.

Functions avoids deadlocks by always advancing the stream's pointer, regardless of success or failure. Because the pointer keeps advancing, your functions need to deal with failures appropriately.

## How the Event Hubs trigger consumes events

Azure Functions consumes events from an event hub by cycling through the following steps:

- A pointer is created and persisted in Azure Storage for each partition of the event hub.
- New events are received in a batch (by default), and the host tries to trigger the function supplying a the batch of events for processing.
- When the function completes execution, with or without exceptions, the pointer is advanced and a checkpoint is saved to the default host storage account.
- Should conditions prevent function execution from completing, the host can't advance the pointer. When the pointer can't advance, subsequent executions reprocess the same events.

This behavior reveals a few important points:

Unhandled exceptions might cause you to lose events:

Function executions that raise an exception continue to progress the pointer. Setting a

[retry policy](#retry-policies)or other retry logic delays advancing the pointer until the entire retry completes.Functions guarantees

*at-least-once*delivery:Your code and dependent systems might need to account for the fact that the same event could be processed twice. For more information, see

[Designing Azure Functions for identical input](functions-idempotent).

## Handling exceptions

While all function code should include a [try/catch block](functions-bindings-error-pages) at the highest level of code, having a `catch`

block is even more important for functions that consume Event Hubs events. That way, when an exception is raised, the catch block handles the error before the pointer progresses.

## Retry mechanisms and policies

Because many exceptions in the cloud are transient, the first step in error handling is always to retry the operation. You can apply built-in retry policies or define your own retry logic.

### Retry policies

Functions provides built-in retry policies for Event Hubs. When using retry policies, you simply raise a new exception and the host try to process the event again based on the defined policy. This retry behavior requires version 5.x or later of the Event Hubs extension. For more information, see [Retry policies](functions-bindings-error-pages#retry-policies).

### Custom retry logic

You can also define your own retry logic in the function itself. For example, you could implement a policy that follows a workflow illustrated by the following rules:

- Try to process an event three times (potentially with a delay between retries).
- If the eventual outcome of all retries is a failure, then add an event to a queue so processing can continue on the stream.
- Corrupt or unprocessed events are then handled later.

Note

[Polly](https://github.com/App-vNext/Polly) is an example of a resilience and transient-fault-handling library for C# applications.

## Nonexception errors

Some issues can occur without an exception being raised. For example, consider a case where a request times out or the instance running the function crashes. When a function fails to complete without an exception, the offset pointer is never advanced. If the pointer doesn't advance, then any instance that runs after a failed execution continues to read the same events. This situation provides an *at-least-once* guarantee.

The assurance that every event is processed at least one time implies that some events could be processed more than once. Your function apps need to be aware of this possibility and must be built around the [principles of idempotency](functions-idempotent).

## Handling failure states

Your app might be able to acceptably handle a few errors in event processing. However, you should also be prepared to handle persistent failure state, which might occur as a result of failures in downstream processing. In such a failure state, such as a downstream data store being offline, your function should stop triggering on events until the system reaches a healthy state.

### Circuit breaker pattern

When you implement the *circuit breaker* pattern, your app can effectively pause event processing and then resume it at a later time after issues are resolved.

There are two components required to implement a circuit breaker in an event stream process:

- Shared state across all instances to track and monitor health of the circuit.
- A primary process that can manage the circuit state, as either
`open`

or`closed`

.

Implementation details can vary, but to share state among instances you need a storage mechanism. You can store state in Azure Storage, a Redis cache, or any other persistent service that can be accessed by your function app instances.

Both [Durable Functions](durable/durable-functions-overview) and [Azure Logic Apps](../logic-apps/logic-apps-overview) provide infrastructure to manage workflows and circuit states. This article describes using Logic Apps to pause and restart function executions, giving you the control required to implement the circuit breaker pattern.

### Define a failure threshold across instances

Persisted shared external state is required to monitor the health of the circuit when multiple instances are processing events simultaneously. You can then monitor this persisted state based on rules that indicate a failure state, such as:

When there are more than 100 event failures within a 30-second period across all instances, break the circuit to stop triggering on new events.


The implementation details for this monitoring logic vary depending on your specific app needs, but in general you must create a system that:

- Logs failures to persisted storage.
- Inspect the rolling count when new failures are logged to determine if the event failure threshold is met.
- When this threshold is met, emit an event telling the system to break the circuit.

### Managing circuit state with Azure Logic Apps

Azure Logic Apps comes with built-in connectors to different services, features, and stateful orchestrations, and it's a natural choice to manage circuit state. After detecting when a circuit must break, you can build a logic app to implement this workflow:

- Trigger an Event Grid workflow that stops the function processing.
- Send a notification email that includes an option to restart the workflow.

To learn how to disable and reenable specific functions using app settings, see [How to disable functions in Azure Functions](disable-function).

The email recipient can investigate the health of the circuit and, when appropriate, restart the circuit via a link in the notification email. As the workflow restarts the function, events are processed from the last event hub checkpoint.

When you use this approach, no events are lost, events are processed in order, and you can break the circuit as long as necessary.

## Migration strategies for Event Grid triggers

When you migrate an existing function app between regions or between some plans, you must recreate the app during the migration process. In this case, during the migration process, you might have two apps that are both able to consume from the same event stream and write to the same output destination.

You should consider [using consumer groups](../event-hubs/event-hubs-features#consumer-groups) to avoid event data loss or duplication during the migration process:

Create a new consumer group for the new target app.

Configure the trigger in the new app to use this new consumer group.

This allows both apps to process events independently during validation.

Validate that the new app is processing events correctly.

Stop the original app or remove its subscription/consumer group.


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cosmosdb-v2.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2 -->

# Azure Cosmos DB trigger and bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to work with [Azure Cosmos DB](/en-us/azure/cosmos-db/serverless-computing-database) bindings in Azure Functions. Azure Functions supports trigger, input, and output bindings for Azure Cosmos DB. For an end-to-end scenario that uses the Azure Cosmos DB extension, see [Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions](scenario-database-changes-azure-cosmosdb).

| Action | Type |
|---|---|
| Run a function when an Azure Cosmos DB document is created or modified |
|

[Input binding](functions-bindings-cosmosdb-v2-input)[Output binding](functions-bindings-cosmosdb-v2-output)Important

This version of the Azure Cosmos DB binding extension supports [Azure Functions version 4.x](functions-versions). If your app still uses version 1.x of the Functions runtime, instead see [Azure Cosmos DB bindings for Azure Functions 1.x](functions-bindings-cosmosdb).
In the Functions v1.x runtime, this binding was originally named `DocumentDB`

.

## Supported APIs

This table indicates how to connect to the various Azure Cosmos DB APIs from your function code:

## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The process for installing the extension varies depending on the extension version:

This version of the Azure Cosmos DB bindings extension introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.CosmosDB/), version 4.x.

If you're writing your application using F#, you must also configure this extension as part of the app's [startup configuration](dotnet-isolated-process-guide#start-up-and-configuration). In the call to `ConfigureFunctionsWorkerDefaults()`

or `ConfigureFunctionsWebApplication()`

, add a delegate that takes an `IFunctionsWorkerApplication`

parameter. Then within the body of that delegate, call `ConfigureCosmosDBExtension()`

on the object:

```
let hostBuilder = new HostBuilder()
hostBuilder.ConfigureFunctionsWorkerDefaults(fun (context: HostBuilderContext) (appBuilder: IFunctionsWorkerApplicationBuilder) ->
appBuilder.ConfigureCosmosDBExtension() |> ignore
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

Because of schema changes in the Azure Cosmos DB SDK, version 4.x of the Azure Cosmos DB extension requires [azure-functions-java-library V3.0.0](https://central.sonatype.com/artifact/com.microsoft.azure.functions/azure-functions-java-library/3.0.0) for Java functions.

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to types from [Microsoft.Azure.Cosmos](/en-us/dotnet/api/microsoft.azure.cosmos)is in preview.

**Cosmos DB trigger**

When you want the function to process a single document, the Cosmos DB trigger can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions tries to deserialize the JSON data of the document from the Cosmos DB change feed into a plain-old CLR object (POCO) type. |

When you want the function to process a batch of documents, the Cosmos DB trigger can bind to the following types:

| Type | Description |
|---|---|
`IEnumerable<T>` where `T` is a JSON serializable type |
An enumeration of entities included in the batch. Each entry represents one document from the Cosmos DB change feed. |

**Cosmos DB input binding**

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

**Cosmos DB output binding**

When you want the function to write to a single document, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | An object representing the JSON content of a document. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple documents, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is JSON serializable type |
An array containing multiple documents. Each entry represents one document. |

For other output scenarios, create and use a [CosmosClient](/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) with other types from [Microsoft.Azure.Cosmos](/en-us/dotnet/api/microsoft.azure.cosmos) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Type support for Azure Cosmos is in Preview. Follow the [Python SDK Bindings for CosmosDB Sample](https://github.com/Azure-Samples/azure-functions-cosmosdb-sdk-bindings-python) to get started with SDK Types for Cosmos in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| CosmosDB input |
|

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_containerproxy/function_app.py)`ContainerProxy`

[,](https://github.com/Azure/azure-functions-python-extensions/tree/dev/azurefunctions-extensions-bindings-cosmosdb/samples/cosmosdb_samples_cosmosclient/function_app.py)`CosmosClient`

`DatabaseProxy`

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Azure Cosmos DB |
|

## host.json settings

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

```
{
"version": "2.0",
"extensions": {
"cosmosDB": {
"connectionMode": "Gateway",
"userAgentSuffix": "MyDesiredUserAgentStamp"
}
}
}
```


| Property | Default | Description |
|---|---|---|
connectionMode |
`Gateway` |
The connection mode used by the function when connecting to the Azure Cosmos DB service. Options: `Direct` connects directly to backend replicas over TCP and can provide lower latency, and `Gateway` routes requests through a front-end gateway over HTTPS. For more information, see
|
userAgentSuffix |
n/a | Adds the specified string value to all requests made by the trigger or binding to the service. This makes it easier for you to track the activity in Azure Monitor, based on a specific function app and filtering by `User Agent` . |


---

<!-- DOCUMENTO FUSIONADO: opentelemetry-howto.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/opentelemetry-howto -->

# Use OpenTelemetry with Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure your function app to export log and trace data in an OpenTelemetry format. Azure Functions generates telemetry data on your function executions from both the Functions host process and the language-specific worker process in which your function code runs. By default, this telemetry data is sent to Application Insights by using the Application Insights SDK. However, you can choose to export this data by using OpenTelemetry semantics. While you can still use an OpenTelemetry format to send your data to Application Insights, you can now also export the same data to any other OpenTelemetry-compliant endpoint.

You can obtain these benefits by enabling OpenTelemetry in your function app:

- Correlates data across traces and logs being generated both at the host and in your application code.
- Enables consistent, standards-based generation of exportable telemetry data.
- Integrates with other providers that can consume OpenTelemetry-compliant data.

Keep these considerations in mind when using this article:

Try the

[OpenTelemetry tutorial](monitor-functions-opentelemetry-distributed-tracing), which is designed to help you get started quickly with OpenTelemetry and Azure Functions. This article uses the Azure Developer CLI (`azd`

) to create and deploy a function app that uses OpenTelemetry integration for distributed tracing.Because this article is targeted at your development language of choice, remember to choose the correct language at the top of the article.


- OpenTelemetry currently isn't supported for
[C# in-process apps](functions-dotnet-class-library).

- OpenTelemetry is enabled at the function app level, both in host configuration (
`host.json`

) and in your code project. Functions also provides a client optimized experience for exporting OpenTelemetry data from your function code that's running in a language-specific worker process.

## Enable OpenTelemetry in the Functions host

When you enable OpenTelemetry output in the function app's `host.json`

file, your host exports OpenTelemetry output regardless of the language stack used by your app.

To enable OpenTelemetry output from the Functions host, update the [host.json file](functions-host-json) in your code project to add a `"telemetryMode": "OpenTelemetry"`

element to the root collection. With OpenTelemetry enabled, your host.json file might look like this:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
...
}
```


## Configure application settings

When you enable OpenTelemetry in the `host.json`

file, the app's environment variables determine the endpoints for sending data based on which OpenTelemetry-supported application settings are available.

Create specific application settings in your function app based on the OpenTelemetry output destination. When you provide connection settings for both Application Insights and an OpenTelemetry protocol (OTLP) exporter, OpenTelemetry data is sent to both endpoints.

** APPLICATIONINSIGHTS_CONNECTION_STRING**: the connection string for an Application Insights workspace. When this setting exists, OpenTelemetry data is sent to that workspace. Use the same setting to connect to Application Insights without OpenTelemetry enabled. If your app doesn't already have this setting, you might need to

[Enable Application Insights integration](configure-monitoring#enable-application-insights-integration).

** JAVA_APPLICATIONINSIGHTS_ENABLE_TELEMETRY**: set to

`true`

so that the Functions host allows the Java worker process to stream OpenTelemetry logs directly, which prevents duplicate host-level entries.** PYTHON_APPLICATIONINSIGHTS_ENABLE_TELEMETRY**: set to

`true`

so that the Functions host allows the Python worker process to stream OpenTelemetry logs directly, which prevents duplicate host-level entries.## Enable OpenTelemetry in your app

After you configure the Functions host to use OpenTelemetry, update your application code to output OpenTelemetry data. When you enable OpenTelemetry in both the host and your application code, you get better correlation between traces and logs that the Functions host process and your language worker process emit.

How you instrument your application to use OpenTelemetry depends on your target OpenTelemetry endpoint:

Examples in this article assume your app uses `IHostApplicationBuilder`

, which is available in version 2.x and later version of [Microsoft.Azure.Functions.Worker](/en-us/dotnet/api/microsoft.extensions.hosting.ihostapplicationbuilder). For more information, see [Version 2.x](dotnet-isolated-process-guide#version-2x) in the C# isolated worker model guide.

Run these commands to install the required assemblies in your app:

`dotnet add package Microsoft.Azure.Functions.Worker.OpenTelemetry dotnet add package OpenTelemetry.Extensions.Hosting dotnet add package Azure.Monitor.OpenTelemetry.Exporter`

In your Program.cs project file, add this

`using`

statement:`using Azure.Monitor.OpenTelemetry.Exporter;`

Configure OpenTelemetry based on whether your project startup uses

`IHostBuilder`

or`IHostApplicationBuilder`

. The latter was introduced in v2.x of the .NET isolated worker model extension.In

*program.cs*, add this line of code after`ConfigureFunctionsWebApplication`

:`builder.Services.AddOpenTelemetry() .UseFunctionsWorkerDefaults() .UseAzureMonitorExporter();`

You can export to both OpenTelemetry endpoints from the same app.


Add the required libraries to your app. The way you add libraries depends on whether you deploy using Maven or Kotlin and if you want to also send data to Application Insights.

`<dependency> <groupId>com.microsoft.azure.functions</groupId> <artifactId>azure-functions-java-opentelemetry</artifactId> <version>1.0.0</version> </dependency> <dependency> <groupId>com.azure</groupId> <artifactId>azure-monitor-opentelemetry-autoconfigure</artifactId> <version>1.2.0</version> </dependency>`

(Optional) Add this code to create custom spans:

`import com.microsoft.azure.functions.opentelemetry.FunctionsOpenTelemetry; import io.opentelemetry.api.trace.Span; import io.opentelemetry.api.trace.SpanKind; import io.opentelemetry.context.Scope; Span span = FunctionsOpenTelemetry.startSpan( "com.contoso.PaymentFunction", // tracer name "validateCharge", // span name null, // parent = current context SpanKind.INTERNAL); try (Scope ignored = span.makeCurrent()) { // business logic here } finally { span.end(); }`


Install these npm packages in your project:

`npm install @opentelemetry/api npm install @opentelemetry/auto-instrumentations-node npm install @azure/monitor-opentelemetry-exporter npm install @azure/functions-opentelemetry-instrumentation`


Create a code file in your project, copy and paste the following code in this new file, and save the file as

`src/index.js`

:`const { AzureFunctionsInstrumentation } = require('@azure/functions-opentelemetry-instrumentation'); const { AzureMonitorLogExporter, AzureMonitorTraceExporter } = require('@azure/monitor-opentelemetry-exporter'); const { getNodeAutoInstrumentations, getResourceDetectors } = require('@opentelemetry/auto-instrumentations-node'); const { registerInstrumentations } = require('@opentelemetry/instrumentation'); const { detectResourcesSync } = require('@opentelemetry/resources'); const { LoggerProvider, SimpleLogRecordProcessor } = require('@opentelemetry/sdk-logs'); const { NodeTracerProvider, SimpleSpanProcessor } = require('@opentelemetry/sdk-trace-node'); const resource = detectResourcesSync({ detectors: getResourceDetectors() }); const tracerProvider = new NodeTracerProvider({ resource }); tracerProvider.addSpanProcessor(new SimpleSpanProcessor(new AzureMonitorTraceExporter())); tracerProvider.register(); const loggerProvider = new LoggerProvider({ resource }); loggerProvider.addLogRecordProcessor(new SimpleLogRecordProcessor(new AzureMonitorLogExporter())); registerInstrumentations({ tracerProvider, loggerProvider, instrumentations: [getNodeAutoInstrumentations(), new AzureFunctionsInstrumentation()], });`

Update the

`main`

field in your package.json file to include the new`src/index.js`

file. For example:`"main": "src/{index.js,functions/*.js}"`


Create a code file in your project, copy and paste the following code in this new file, and save the file as

`src/index.ts`

:`import { AzureFunctionsInstrumentation } from '@azure/functions-opentelemetry-instrumentation'; import { AzureMonitorLogExporter, AzureMonitorTraceExporter } from '@azure/monitor-opentelemetry-exporter'; import { getNodeAutoInstrumentations, getResourceDetectors } from '@opentelemetry/auto-instrumentations-node'; import { registerInstrumentations } from '@opentelemetry/instrumentation'; import { detectResourcesSync } from '@opentelemetry/resources'; import { LoggerProvider, SimpleLogRecordProcessor } from '@opentelemetry/sdk-logs'; import { NodeTracerProvider, SimpleSpanProcessor } from '@opentelemetry/sdk-trace-node'; const resource = detectResourcesSync({ detectors: getResourceDetectors() }); const tracerProvider = new NodeTracerProvider({ resource }); tracerProvider.addSpanProcessor(new SimpleSpanProcessor(new AzureMonitorTraceExporter())); tracerProvider.register(); const loggerProvider = new LoggerProvider({ resource }); loggerProvider.addLogRecordProcessor(new SimpleLogRecordProcessor(new AzureMonitorLogExporter())); registerInstrumentations({ tracerProvider, loggerProvider, instrumentations: [getNodeAutoInstrumentations(), new AzureFunctionsInstrumentation()], });`

Update the

`main`

field in your package.json file to include the output of this new`src/index.ts`

file, which might look like this:`"main": "dist/src/{index.js,functions/*.js}"`


Important

OpenTelemetry output to Application Insights from the language worker isn't currently supported for PowerShell apps. You might instead want to use an OTLP exporter endpoint. When you configure your host for OpenTelemetry output to Application Insights, the logs generated by the PowerShell worker process are still forwarded, but distributed tracing isn't supported at this time.

These instructions only apply for an OTLP exporter:

Add an application setting named

`OTEL_FUNCTIONS_WORKER_ENABLED`

with value of`True`

.Create an

[app-level](functions-reference-powershell#including-modules-in-app-content)in the root of your app and run the following command:`Modules`

folder`Save-Module -Name AzureFunctions.PowerShell.OpenTelemetry.SDK`

This command installs the required

`AzureFunctions.PowerShell.OpenTelemetry.SDK`

module directly in your app. You can't use the`requirements.psd1`

file to automatically install this dependency because[managed dependencies](functions-reference-powershell#dependency-management)isn't currently supported in the[Flex Consumption plan](flex-consumption-plan)preview.Add this code to your profile.ps1 file:

`Import-Module AzureFunctions.PowerShell.OpenTelemetry.SDK -Force -ErrorAction Stop Initialize-FunctionsOpenTelemetry`


Make sure these libraries are in your

`requirements.txt`

file, whether from uncommenting or adding yourself:`azure-monitor-opentelemetry`

Add this code to your

`function_app.py`

main entry point file:If you already added

`PYTHON_APPLICATIONINSIGHTS_ENABLE_TELEMETRY=true`

in your application settings, you can skip this step. To manually enable Application Insights collection without automatic instrumentation, add this code to your app:`from azure.monitor.opentelemetry import configure_azure_monitor configure_azure_monitor()`

Review

[Azure monitor Distro usage](https://github.com/Azure/azure-sdk-for-python/tree/main/sdk/monitor/azure-monitor-opentelemetry#usage)documentation for options on how to further configure the SDK.

## Considerations for OpenTelemetry

When you export your data by using OpenTelemetry, keep these considerations in mind.

The Azure portal supports

`Recent function invocation`

traces only if the telemetry is sent to Azure Monitor.When you configure the host to use OpenTelemetry, the Azure portal doesn't support log streaming.

If you set

`telemetryMode`

to`OpenTelemetry`

, the configuration in the`logging.applicationInsights`

section of host.json doesn't apply.

Custom spans automatically include all resource attributes and use the exporters configured in your app.

When your app runs outside Azure, including during local development, the resource detector sets the

`service.name`

attribute to`java-function-app`

by default.Use these Java Virtual Machine (JVM) flags to silence telemetry when running locally during unit tests:

`-Dotel.traces.exporter=none`

`-Dotel.metrics.exporter=none`

`-Dotel.logs.exporter=none`


- You don't need to manually register middleware; the Java worker autodiscovers
`OpenTelemetryInvocationMiddleware`

.

## Resource detectors and semantic conventions

In Azure Functions, resource attributes describe the function app process and its environment. Span attributes describe a single invocation.

### Default behavior (no action required)

In Azure Functions on App Service, resource detectors typically populate common attributes automatically, including:

`service.name`

(defaults to the function app name)- Azure cloud attributes such as
`cloud.provider`

,`cloud.region`

, and`cloud.resource_id`


In most cases, these defaults are sufficient for correct Application Map grouping and Azure context.

### When to override `service.name`

(Cloud Role Name)

Override only if you need a different, stable node name in Application Insights (Application Map grouping), for example to normalize naming across slots or environments.

Set `OTEL_SERVICE_NAME`

to override the detected value:

```
export OTEL_SERVICE_NAME="my-function-app"
```


### Invocation span attributes (usually automatic)

You won’t have to set these manually unless you’re creating a custom invocation span.

`faas.name`

(function name)`faas.trigger`

(for example`http`

,`servicebus`

,`eventhubs`

)`faas.execution`

(invocation/execution identifier)

Important

Function apps can host multiple functions in one process. Do not put function-specific values on the resource. Put per-invocation identity on spans.

Note

When running locally (Functions Core Tools) or in containerized/self-hosted environments where Azure metadata is unavailable, `service.name`

may default to a generic value. Set `OTEL_SERVICE_NAME`

locally to match production naming.

## Troubleshooting

When you export your data by using OpenTelemetry, keep these common issues and solutions in mind.

### Log filtering

To correctly configure log filtering in your function app, you need to understand the difference between the host process and the worker process.

The *host process* is the Azure Functions runtime that manages triggers, scaling, and emits system-level telemetry such as initialization logs, request traces, and runtime health information.

The *worker process* is language specific, executes your function code, and produces application logs and telemetry independently.

Important

Filters defined in host.json apply only to logs generated by the host process. You must use language-specific OpenTelemetry settings to filter logs from the worker process.

**Example: Filter host logs for all providers in host.json**

Use this approach to set a global log level across all providers managed by the host:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
"logging": {
"logLevel": {
"default": "Warning"
}
}
}
```


**Example: Filter logs only for the OpenTelemetry logger provider**

Use this approach to target only the OpenTelemetry logger provider while leaving other providers (such as console or file logging) unaffected:

```
{
"version": "2.0",
"telemetryMode": "OpenTelemetry",
"logging": {
"OpenTelemetry": {
"logLevel": {
"default": "Warning"
}
}
}
}
```


### Console logging

The Functions host automatically captures anything written to stdout or stderr and forwards it to the telemetry pipeline. If you also use a ConsoleExporter or write directly to console in your code, duplicate logs can occur in your telemetry data.

Note

To avoid duplicate telemetry entries, don't add ConsoleExporter or write to console in production code.

### Microsoft Entra authentication

When you use Microsoft Entra authentication with OpenTelemetry, you must configure authentication separately for both the host process and the worker process.

To configure authentication for the host process, see [Require Microsoft Entra authentication](configure-monitoring#require-microsoft-entra-authentication).

To configure authentication for the worker process, see [Enable Microsoft Entra authentication](/en-us/azure/azure-monitor/app/azure-ad-authentication).

### Resource attributes support

Resource attributes support in Azure Monitor is currently in preview. To enable this feature, set the `OTEL_DOTNET_AZURE_MONITOR_ENABLE_RESOURCE_METRICS`

environment variable to `true`

. This setting ingests resource attributes into the custom metrics table.

### Duplicate request telemetry

The host process automatically emits request telemetry. If the worker process is also instrumented with request tracking libraries (for example, AspNetCoreInstrumentation in .NET), the same request is reported twice.

Note

Since the Azure Monitor Distro typically includes AspNetCoreInstrumentation in .NET and similar instrumentation in other languages, avoid using the Azure Monitor distro in the worker process to prevent duplicate telemetry.

### Logging scopes not included

By default, the worker process doesn't include scopes in its logs. To enable scopes, you must configure this setting explicitly in the worker. The following example shows how to enable scopes in .NET Isolated:

```
builder.Logging.AddOpenTelemetry(b => b.IncludeScopes = true);
```


### Missing request telemetry

Triggers such as HTTP, Service Bus, and Event Hubs depend on context propagation for distributed tracing. With parent-based sampling as the default behavior, request telemetry isn't generated when the incoming request or message isn't sampled.

### Duplicate OperationId

In Azure Functions, the `OperationId`

used for correlating telemetry comes directly from the `traceparent`

value in the incoming request or message. If multiple calls reuse the same `traceparent`

value, they all get the same `OperationId`

.

### Configure OpenTelemetry with environment variables

You can configure OpenTelemetry behavior by using its standard environment variables. These variables provide a consistent way to control behavior across different languages and runtimes. You can adjust sampling strategies, exporter settings, and resource attributes. For more information about supported environment variables, see the [OpenTelemetry documentation](https://opentelemetry.io/docs/languages/sdk-configuration/).

### Use diagnostics to troubleshoot monitoring issues

[Azure Functions diagnostics](functions-diagnostics) in the Azure portal is a useful resource for detecting and diagnosing potential monitoring-related issues.

To access diagnostics in your app:

In the

[Azure portal](https://portal.azure.com), go to your function app resource.In the left pane, select

**Diagnose and solve problems**and search for the*Function App missing telemetry Application Insights or OpenTelemetry*workflow.Select this workflow, choose your ingestion method, and select

**Next**.Review the guidelines and any recommendations provided by the troubleshooter.


## Next steps

Learn more about OpenTelemetry and monitoring Azure Functions:


---

<!-- DOCUMENTO FUSIONADO: _functions-custom-handlers__functions-bindings-openai-assistant-trigger_function_b8ad7f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-custom-handlers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-custom-handlers -->

# Azure Functions custom handlers

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions executes your app code by using language-specific handlers. These language-specific handlers allow Functions to support [most key languages](supported-languages) by default. However, you might need to run code in another language or package.

Custom handlers are lightweight web servers that receive events from the Azure Functions host process. You can use custom handlers to deploy to Azure Functions any code project that supports HTTP primitives.

Custom handlers are best suited for situations where you want to:

- Implement a function app in a language that's not currently offered out-of-the-box, such as Go or Rust.
- Implement a function app in a runtime that's not currently featured by default, such as Deno.
[Deploy a server](#deploy-self-hosted-mcp-servers)built with the standard MCP SDKs to Azure Functions.

With custom handlers, you can use [triggers and input and output bindings](functions-triggers-bindings) via [extension bundles](functions-bindings-register).

Get started with Azure Functions custom handlers with [quickstarts in Go and Rust](create-first-function-vs-code-other).

## Overview

The following diagram shows the relationship between the Functions host and a web server implemented as a custom handler.

- Each event triggers a request sent to the Functions host. An event is any trigger that Azure Functions supports.
- The Functions host then issues a
[request payload](#request-payload)to the web server. The payload holds trigger and input binding data and other metadata for the function. - The web server executes the individual function, and returns a
[response payload](#response-payload)to the Functions host. - The Functions host passes data from the response to the function's output bindings for processing.

An Azure Functions app implemented as a custom handler must configure the *host.json*, *local.settings.json*, and *function.json* files according to a few conventions.

## Deploy self-hosted MCP servers

Custom handlers also enables you to host MCP servers that you build by using official MCP SDKs in Azure Functions. Custom handlers provides a simple and streamlined experience for hosting your MCP servers in Azure. For more information, see [Self-hosted remote MCP server on Azure Functions](self-hosted-mcp-servers).

Note

The ability to have Azure Functions host MCP servers you create using official MCP SDKs is currently in preview.

## Application structure

To implement a custom handler, your application needs the following aspects:

- A
*host.json*file at the root of your app - A
*local.settings.json*file at the root of your app - A
*function.json*file for each function (inside a folder that matches the function name) - A command, script, or executable that runs a web server

The following diagram shows how these files look on the file system for a function named "MyQueueFunction" and a custom handler executable named *handler.exe*.

```
| /MyQueueFunction
| function.json
|
| host.json
| local.settings.json
| handler.exe
```


### Configuration

You configure the application through the *host.json* and *local.settings.json* files.

#### host.json

*host.json* directs the Functions host where to send requests by pointing to a web server that can process HTTP events.

Define a custom handler by configuring the *host.json* file with details on how to run the web server through the `customHandler`

section.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
}
}
```


The `customHandler`

section points to a target as defined by the `defaultExecutablePath`

. The execution target can be a command, executable, or file where the web server is implemented.

Use the `arguments`

array to pass any arguments to the executable. Arguments support expansion of environment variables (application settings) by using `%%`

notation.

You can also change the working directory used by the executable with `workingDirectory`

.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "app/handler.exe",
"arguments": [
"--database-connection-string",
"%DATABASE_CONNECTION_STRING%"
],
"workingDirectory": "app"
}
}
}
```


##### Bindings support

Standard triggers along with input and output bindings are available by referencing [extension bundles](functions-bindings-register) in your *host.json* file.

#### local.settings.json

*local.settings.json* defines application settings used when running the function app locally. Because it might contain secrets, exclude *local.settings.json* from source control. In Azure, use application settings instead.

For custom handlers, set `FUNCTIONS_WORKER_RUNTIME`

to `Custom`

in *local.settings.json*.

```
{
"IsEncrypted": false,
"Values": {
"FUNCTIONS_WORKER_RUNTIME": "Custom"
}
}
```


### Function metadata

When you use a custom handler, the *function.json* contents are the same as when you define a function in any other context. The only requirement is that you must place *function.json* files in a folder named to match the function name.

The following *function.json* configures a function that has a queue trigger and a queue output binding. Because it's in a folder named *MyQueueFunction*, it defines a function named *MyQueueFunction*.

**MyQueueFunction/function.json**

```
{
"bindings": [
{
"name": "myQueueItem",
"type": "queueTrigger",
"direction": "in",
"queueName": "messages-incoming",
"connection": "AzureWebJobsStorage"
},
{
"name": "$return",
"type": "queue",
"direction": "out",
"queueName": "messages-outgoing",
"connection": "AzureWebJobsStorage"
}
]
}
```


### Request payload

When the Functions host receives a queue message, it sends an HTTP post request to the custom handler with a payload in the body.

The following code shows a sample request payload. The payload includes a JSON structure with two members: `Data`

and `Metadata`

.

The `Data`

member includes keys that match input and trigger names as defined in the bindings array in the *function.json* file.

The `Metadata`

member includes [metadata generated from the event source](functions-bindings-expressions-patterns#trigger-metadata).

```
{
"Data": {
"myQueueItem": "{ message: \"Message sent\" }"
},
"Metadata": {
"DequeueCount": 1,
"ExpirationTime": "2019-10-16T17:58:31+00:00",
"Id": "800ae4b3-bdd2-4c08-badd-f08e5a34b865",
"InsertionTime": "2019-10-09T17:58:31+00:00",
"NextVisibleTime": "2019-10-09T18:08:32+00:00",
"PopReceipt": "AgAAAAMAAAAAAAAAAgtnj8x+1QE=",
"sys": {
"MethodName": "QueueTrigger",
"UtcNow": "2019-10-09T17:58:32.2205399Z",
"RandGuid": "24ad4c06-24ad-4e5b-8294-3da9714877e9"
}
}
}
```


### Response payload

By convention, function responses are formatted as key/value pairs. Supported keys include:

| Data type | Remarks | |
|---|---|---|
`Outputs` |
object | Holds response values as defined by the `bindings` array in function.json.For instance, if a function is configured with a queue output binding named "myQueueOutput", then `Outputs` contains a key named `myQueueOutput` , which the custom handler sets to the messages that it sends to the queue. |
`Logs` |
array | Messages that appear in the Functions invocation logs. When running in Azure, messages appear in Application Insights. |
`ReturnValue` |
string | Used to provide a response when an output is configured as `$return` in the function.json file. |

This table shows an example of a response payload.

```
{
"Outputs": {
"res": {
"body": "Message enqueued"
},
"myQueueOutput": [
"queue message 1",
"queue message 2"
]
},
"Logs": [
"Log message 1",
"Log message 2"
],
"ReturnValue": "{\"hello\":\"world\"}"
}
```


## Examples

You can implement custom handlers in any language that supports receiving HTTP events. The following examples show how to implement a custom handler by using the Go programming language.

### Function with bindings

This example shows a function named `order`

that accepts a `POST`

request with a payload representing a product order. When you post an order to the function, it creates a Queue Storage message and returns an HTTP response.

#### Implementation

In a folder named *order*, the *function.json* file configures the HTTP-triggered function.

**order/function.json**

```
{
"bindings": [
{
"type": "httpTrigger",
"direction": "in",
"name": "req",
"methods": ["post"]
},
{
"type": "http",
"direction": "out",
"name": "res"
},
{
"type": "queue",
"name": "message",
"direction": "out",
"queueName": "orders",
"connection": "AzureWebJobsStorage"
}
]
}
```


This function is defined as an [HTTP triggered function](functions-bindings-http-webhook-trigger) that returns an [HTTP response](functions-bindings-http-webhook-output) and outputs a [Queue storage](functions-bindings-storage-queue-output) message.

At the root of the app, the *host.json* file is configured to run an executable file named `handler.exe`

(`handler`

in Linux or macOS).

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


This is the HTTP request sent to the Functions runtime.

```
POST http://127.0.0.1:7071/api/order HTTP/1.1
Content-Type: application/json
{
"id": 1005,
"quantity": 2,
"color": "black"
}
```


The Functions runtime sends the following HTTP request to the custom handler:

```
POST http://127.0.0.1:<FUNCTIONS_CUSTOMHANDLER_PORT>/order HTTP/1.1
Content-Type: application/json
{
"Data": {
"req": {
"Url": "http://localhost:7071/api/order",
"Method": "POST",
"Query": "{}",
"Headers": {
"Content-Type": [
"application/json"
]
},
"Params": {},
"Body": "{\"id\":1005,\"quantity\":2,\"color\":\"black\"}"
}
},
"Metadata": {
}
}
```


Note

Some portions of the payload were removed for brevity.

*handler.exe* is the compiled Go custom handler program that runs a web server and responds to function invocation requests from the Functions host.

```
package main
import (
"encoding/json"
"fmt"
"log"
"net/http"
"os"
)
type InvokeRequest struct {
Data map[string]json.RawMessage
Metadata map[string]interface{}
}
type InvokeResponse struct {
Outputs map[string]interface{}
Logs []string
ReturnValue interface{}
}
func orderHandler(w http.ResponseWriter, r *http.Request) {
var invokeRequest InvokeRequest
d := json.NewDecoder(r.Body)
d.Decode(&invokeRequest)
var reqData map[string]interface{}
json.Unmarshal(invokeRequest.Data["req"], &reqData)
outputs := make(map[string]interface{})
outputs["message"] = reqData["Body"]
resData := make(map[string]interface{})
resData["body"] = "Order enqueued"
outputs["res"] = resData
invokeResponse := InvokeResponse{outputs, nil, nil}
responseJson, _ := json.Marshal(invokeResponse)
w.Header().Set("Content-Type", "application/json")
w.Write(responseJson)
}
func main() {
customHandlerPort, exists := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT")
if !exists {
customHandlerPort = "8080"
}
mux := http.NewServeMux()
mux.HandleFunc("/order", orderHandler)
fmt.Println("Go server Listening on: ", customHandlerPort)
log.Fatal(http.ListenAndServe(":"+customHandlerPort, mux))
}
```


In this example, the custom handler runs a web server to handle HTTP events and listens for requests via the `FUNCTIONS_CUSTOMHANDLER_PORT`

.

Even though the Functions host receives the original HTTP request at `/api/order`

, it invokes the custom handler by using the function name (its folder name). In this example, the function is defined at the path of `/order`

. The host sends the custom handler an HTTP request at the path of `/order`

.

When you send `POST`

requests to this function, the trigger data and function metadata are available via the HTTP request body. You can access the original HTTP request body in the payload's `Data.req.Body`

.

The function's response is formatted into key/value pairs where the `Outputs`

member holds a JSON value where the keys match the outputs as defined in the *function.json* file.

This is an example payload that this handler returns to the Functions host.

```
{
"Outputs": {
"message": "{\"id\":1005,\"quantity\":2,\"color\":\"black\"}",
"res": {
"body": "Order enqueued"
}
},
"Logs": null,
"ReturnValue": null
}
```


By setting the `message`

output equal to the order data that came in from the request, the function outputs that order data to the configured queue. The Functions host also returns the HTTP response configured in `res`

to the caller.

### HTTP-only function

For HTTP-triggered functions with no additional bindings or outputs, you might want your handler to work directly with the HTTP request and response instead of the custom handler [request](#request-payload) and [response](#response-payload) payloads. You can configure this behavior in *host.json* by using the `enableProxyingHttpRequest`

setting, which supports response streaming.

Important

The primary purpose of the custom handlers feature is to enable languages and runtimes that don't currently have first-class support on Azure Functions. While you might be able to run web applications by using custom handlers, Azure Functions isn't a standard reverse proxy. Some components of the HTTP request, such as certain headers and routes, might be restricted. Your application might also experience excessive [cold start](event-driven-scaling#cold-start).

To address these circumstances, consider running your web apps on [Azure App Service](../app-service/overview).

The following example demonstrates how to configure an HTTP-triggered function with no additional bindings or outputs. The scenario implemented in this example features a function named `hello`

that accepts a `GET`

or `POST`

.

#### Implementation

In a folder named *hello*, the *function.json* file configures the HTTP-triggered function.

**hello/function.json**

```
{
"bindings": [
{
"type": "httpTrigger",
"authLevel": "function",
"direction": "in",
"name": "req",
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


The function is configured to accept both `GET`

and `POST`

requests, and the result value is provided through an argument named `res`

.

At the root of the app, the *host.json* file is configured to run `handler.exe`

and `enableProxyingHttpRequest`

is set to `true`

.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
},
"enableProxyingHttpRequest": true
}
}
```


The following is a POST request to the Functions host. The Functions host then sends the request to the custom handler.

```
POST http://127.0.0.1:7071/api/hello HTTP/1.1
Content-Type: application/json
{
"message": "Hello World!"
}
```


The *handler.go* file implements a web server and HTTP function.

```
package main
import (
"fmt"
"io/ioutil"
"log"
"net/http"
"os"
)
func helloHandler(w http.ResponseWriter, r *http.Request) {
w.Header().Set("Content-Type", "application/json")
if r.Method == "GET" {
w.Write([]byte("hello world"))
} else {
body, _ := ioutil.ReadAll(r.Body)
w.Write(body)
}
}
func main() {
customHandlerPort, exists := os.LookupEnv("FUNCTIONS_CUSTOMHANDLER_PORT")
if !exists {
customHandlerPort = "8080"
}
mux := http.NewServeMux()
mux.HandleFunc("/api/hello", helloHandler)
fmt.Println("Go server Listening on: ", customHandlerPort)
log.Fatal(http.ListenAndServe(":"+customHandlerPort, mux))
}
```


In this example, the custom handler creates a web server to handle HTTP events and listens for requests via the `FUNCTIONS_CUSTOMHANDLER_PORT`

.

`GET`

requests are handled by returning a string, and `POST`

requests have access to the request body.

The route for the order function here is `/api/hello`

, same as the original request.

Note

The `FUNCTIONS_CUSTOMHANDLER_PORT`

isn't the public facing port used to call the function. The Functions host uses this port to call the custom handler.

## Deploying

You can deploy a custom handler to every Azure Functions hosting option. If your handler requires operating system or platform dependencies (such as a language runtime), you might need to use a [custom container](functions-how-to-custom-container).

When you create a function app in Azure for custom handlers, select .NET Core as the stack.

To deploy a custom handler app by using Azure Functions Core Tools, run the following command.

```
func azure functionapp publish $functionAppName
```


Note

Ensure all files required to run your custom handler are in the folder and included in the deployment. If your custom handler is a binary executable or has platform-specific dependencies, ensure these files match the target deployment platform.

## Restrictions

- The custom handler web server needs to start within 60 seconds.

## Samples

For examples of how to implement functions in a variety of different languages, see the [custom handler samples GitHub repo](https://github.com/Azure-Samples/functions-custom-handlers).

## Troubleshooting and support

### Trace logging

If your custom handler process fails to start or if it has problems communicating with the Functions host, increase the function app's log level to `Trace`

to see more diagnostic messages from the host.

To change the function app's default log level, configure the `logLevel`

setting in the `logging`

section of *host.json*.

```
{
"version": "2.0",
"customHandler": {
"description": {
"defaultExecutablePath": "handler.exe"
}
},
"logging": {
"logLevel": {
"default": "Trace"
}
}
}
```


The Functions host outputs extra log messages, including information related to the custom handler process. Use the logs to investigate problems starting your custom handler process or invoking functions in your custom handler.

Locally, logs are printed to the console.

In Azure, [query Application Insights traces](analyze-telemetry-data#query-telemetry-data) to view the log messages. If your app produces a high volume of logs, only a subset of log messages are sent to Application Insights. [Disable sampling](configure-monitoring#configure-sampling) to ensure all messages are logged.

### Test custom handler in isolation

Custom handler apps are web server processes, so it might be helpful to start them on their own and test function invocations by sending mock [HTTP requests](#request-payload). For sending HTTP requests with payloads, make sure to choose a tool that keeps your data secure. For more information, see [HTTP test tools](functions-develop-local#http-test-tools).

You can also use this strategy in your CI/CD pipelines to run automated tests on your custom handler.

### Execution environment

Custom handlers run in the same environment as a typical Azure Functions app. Test your handler to ensure the environment contains all the dependencies it needs to run. For apps that require additional dependencies, you might need to run them by using a [custom container image](functions-how-to-custom-container) hosted on Azure Functions [Premium plan](functions-premium-plan).

### Get support

If you need help on a function app with custom handlers, you can submit a request through regular support channels. However, due to the wide variety of possible languages used to build custom handlers apps, support isn't unlimited.

Support is available if the Functions host has problems starting or communicating with the custom handler process. For problems specific to the inner workings of your custom handler process, such as issues with the chosen language or framework, our Support Team can't provide assistance in this context.

## Next steps

Get started building an Azure Functions app in Go or Rust with the [custom handlers quickstart](create-first-function-vs-code-other).


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-openai-assistant-trigger_functions-integrate-store-unstructu_1b9a90.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-openai-assistant-trigger.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistant-trigger -->

# Azure OpenAI assistant trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI assistant trigger lets you run your code based on custom chat bot or skill request made to an assistant.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI assistants, see [Azure OpenAI Assistants API](/en-us/azure/ai-services/openai/concepts/assistants).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
[Function(nameof(AddTodo))]
public Task AddTodo([AssistantSkillTrigger("Create a new todo task")] string taskDescription)
{
if (string.IsNullOrEmpty(taskDescription))
{
throw new ArgumentException("Task description cannot be empty");
}
this.logger.LogInformation("Adding todo: {task}", taskDescription);
string todoId = Guid.NewGuid().ToString()[..6];
return this.todoManager.AddTodoAsync(new TodoItem(todoId, taskDescription));
}
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
/**
* Called by the assistant to create new todo tasks.
*/
@FunctionName("AddTodo")
public void addTodo(
@AssistantSkillTrigger(
name = "assistantSkillCreateTodo",
functionDescription = "Create a new todo task"
) String taskDescription,
final ExecutionContext context) {
if (taskDescription == null || taskDescription.isEmpty()) {
throw new IllegalArgumentException("Task description cannot be empty");
}
context.getLogger().info("Adding todo: " + taskDescription);
String todoId = UUID.randomUUID().toString().substring(0, 6);
TodoItem todoItem = new TodoItem(todoId, taskDescription);
todoManager.addTodo(todoItem);
}
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
const { app, trigger } = require("@azure/functions");
const { TodoItem, CreateTodoManager } = require("../services/todoManager");
const { randomUUID } = require('crypto');
const todoManager = CreateTodoManager()
app.generic('AddTodo', {
trigger: trigger.generic({
type: 'assistantSkillTrigger',
functionDescription: 'Create a new todo task'
}),
handler: async (taskDescription, context) => {
if (!taskDescription) {
throw new Error('Task description cannot be empty')
}
context.log(`Adding todo: ${taskDescription}`)
const todoId = randomUUID().substring(0, 6)
return todoManager.AddTodo(new TodoItem(todoId, taskDescription))
}
})
```


```
import { InvocationContext, app, trigger } from "@azure/functions"
import { TodoItem, ITodoManager, CreateTodoManager } from "../services/todoManager"
import { randomUUID } from 'crypto';
const todoManager: ITodoManager = CreateTodoManager()
app.generic('AddTodo', {
trigger: trigger.generic({
type: 'assistantSkillTrigger',
functionDescription: 'Create a new todo task'
}),
handler: async (taskDescription: string, context: InvocationContext) => {
if (!taskDescription) {
throw new Error('Task description cannot be empty')
}
context.log(`Adding todo: ${taskDescription}`)
const todoId = randomUUID().substring(0, 6)
return todoManager.AddTodo(new TodoItem(todoId, taskDescription))
}
})
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

Here's the *function.json* file for Add Todo:

```
{
"bindings": [
{
"name": "TaskDescription",
"type": "assistantSkillTrigger",
"dataType": "string",
"direction": "in",
"functionDescription": "Create a new todo task"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

```
using namespace System.Net
param($TaskDescription, $TriggerMetadata)
$ErrorActionPreference = "Stop"
if (-not $TaskDescription) {
throw "Task description cannot be empty"
}
Write-Information "Adding todo: $TaskDescription"
$todoID = [Guid]::NewGuid().ToString().Substring(0, 5)
Add-Todo $todoId $TaskDescription
```


This example demonstrates how to create an assistant that adds a new todo task to a database. The trigger has a static description of `Create a new todo task`

used by the model. The function itself takes a string, which represents a new task to add. When executed, the function adds the task as a new todo item in a custom item store and returns a response from the store.

```
@skills.function_name("AddTodo")
@skills.assistant_skill_trigger(
arg_name="taskDescription", function_description="Create a new todo task"
)
def add_todo(taskDescription: str) -> None:
if not taskDescription:
raise ValueError("Task description cannot be empty")
logging.info(f"Adding todo: {taskDescription}")
todo_id = str(uuid.uuid4())[0:6]
todo_manager.add_todo(TodoItem(id=todo_id, task=taskDescription))
return
```


## Attributes

Apply the `AssistantSkillTrigger`

attribute to define an assistant trigger, which supports these parameters:

| Parameter | Description |
|---|---|
FunctionDescription |
Gets the description of the assistant function, which is provided to the model. |
FunctionName |
Optional. Gets or sets the name of the function called by the assistant. |
ParameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Annotations

The `AssistantSkillTrigger`

annotation enables you to define an assistant trigger, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the input binding. |
functionDescription |
Gets the description of the assistant function, which is provided to the model. |
functionName |
Optional. Gets or sets the name of the function called by the assistant. |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Decorators

During the preview, define the input binding as a `generic_trigger`

binding of type `assistantSkillTrigger`

, which supports these parameters:

| Parameter | Description |
|---|---|
function_description |
Gets the description of the assistant function, which is provided to the model. |
function_name |
Optional. Gets or sets the name of a function called by the assistant. |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `AssistantSkillTrigger` . |
direction |
Must be `in` . |
name |
The name of the trigger. |
functionName |
Gets or sets the name of the function called by the assistant. |
functionDescription |
Gets the description of the assistant function, which is provided to the language model. |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
type |
Must be `AssistantSkillTrigger` . |
name |
The name of the trigger. |
functionName |
Gets or sets the name of the function called by the assistant. |
functionDescription |
Gets the description of the assistant function, which is provided to the LLM |
parameterDescriptionJson |
Optional. Gets or sets a JSON description of the function parameter, which is provided to the model. For more information, see
|

See the [Example section](#example) for complete examples.

## Usage

When `parameterDescriptionJson`

JSON value isn't provided, it's autogenerated. For more information on the syntax of this object, see the [OpenAI API documentation](https://platform.openai.com/docs/api-reference/chat/create#chat-create-tools).


---

<!-- DOCUMENTO FUSIONADO: functions-integrate-store-unstructured-data-cosmosdb.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-integrate-store-unstructured-data-cosmosdb -->

# Store unstructured data using Azure Functions and Azure Cosmos DB

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Cosmos DB](https://azure.microsoft.com/services/cosmos-db/) is a great way to store unstructured and JSON data. Combined with Azure Functions, Azure Cosmos DB makes storing data quick and easy with much less code than required for storing data in a relational database.

Note

At this time, the Azure Cosmos DB trigger, input bindings, and output bindings work with SQL API and Graph API accounts only.

In Azure Functions, input and output bindings provide a declarative way to connect to external service data from your function. In this article, learn how to update an existing function to add an output binding that stores unstructured data in an Azure Cosmos DB document.

## Prerequisites

To complete this tutorial:

This article uses as its starting point the resources created in [Create your first function in the Azure portal](functions-create-function-app-portal). If you haven't already done so, complete these steps now to create your function app.

## Create an Azure Cosmos DB account

You must have an Azure Cosmos DB account that uses the SQL API before you create the output binding.

From the Azure portal menu or the

**Home page**, select**Create a resource**.Search for

**Azure Cosmos DB**. Select**Create**>**Azure Cosmos DB**.On the

**Create an Azure Cosmos DB account**page, select the**Create**option within the**Azure Cosmos DB for NoSQL**section.Azure Cosmos DB provides several APIs:

- NoSQL, for document data
- PostgreSQL
- MongoDB, for document data
- Apache Cassandra
- Table
- Apache Gremlin, for graph data

To learn more about the API for NoSQL, see

[Welcome to Azure Cosmos DB](/en-us/azure/cosmos-db/introduction).In the

**Create Azure Cosmos DB Account**page, enter the basic settings for the new Azure Cosmos DB account.Setting Value Description Subscription Subscription name Select the Azure subscription that you want to use for this Azure Cosmos DB account. Resource Group Resource group name Select a resource group, or select **Create new**, then enter a unique name for the new resource group.Account Name A unique name Enter a name to identify your Azure Cosmos DB account. Because *documents.azure.com*is appended to the name that you provide to create your URI, use a unique name. The name can contain only lowercase letters, numbers, and the hyphen (-) character. It must be 3-44 characters.Location The region closest to your users Select a geographic location to host your Azure Cosmos DB account. Use the location that is closest to your users to give them the fastest access to the data. Capacity mode **Provisioned throughput**or**Serverless**Select **Provisioned throughput**to create an account in[provisioned throughput](/en-us/azure/cosmos-db/set-throughput)mode. Select**Serverless**to create an account in[serverless](/en-us/azure/cosmos-db/serverless)mode.Apply Azure Cosmos DB free tier discount **Apply**or**Do not apply**With Azure Cosmos DB free tier, you get the first 1000 RU/s and 25 GB of storage for free in an account. Learn more about [free tier](https://azure.microsoft.com/pricing/details/cosmos-db/).Limit total account throughput Selected or not Limit the total amount of throughput that can be provisioned on this account. This limit prevents unexpected charges related to provisioned throughput. You can update or remove this limit after your account is created. You can have up to one free tier Azure Cosmos DB account per Azure subscription and must opt in when creating the account. If you don't see the option to apply the free tier discount, another account in the subscription has already been enabled with free tier.

Note

The following options are not available if you select

**Serverless**as the**Capacity mode**:- Apply Free Tier Discount
- Limit total account throughput

In the

**Global Distribution**tab, configure the following details. You can leave the default values for this quickstart:Setting Value Description Geo-Redundancy Disable Enable or disable global distribution on your account by pairing your region with a pair region. You can add more regions to your account later. Multi-region Writes Disable Multi-region writes capability allows you to take advantage of the provisioned throughput for your databases and containers across the globe. Availability Zones Disable Availability Zones help you further improve availability and resiliency of your application. Note

The following options are not available if you select

**Serverless**as the**Capacity mode**in the previous**Basics**page:- Geo-redundancy
- Multi-region Writes

Optionally, you can configure more details in the following tabs:

**Networking**. Configure[access from a virtual network](/en-us/azure/cosmos-db/how-to-configure-vnet-service-endpoint).**Backup Policy**. Configure either[periodic](/en-us/azure/cosmos-db/periodic-backup-restore-introduction)or[continuous](/en-us/azure/cosmos-db/provision-account-continuous-backup)backup policy.**Encryption**. Use either service-managed key or a[customer-managed key](/en-us/azure/cosmos-db/how-to-setup-cmk#create-a-new-azure-cosmos-account).**Tags**. Tags are name/value pairs that enable you to categorize resources and view consolidated billing by applying the same tag to multiple resources and resource groups.

Select

**Review + create**.Review the account settings, and then select

**Create**. It takes a few minutes to create the account. Wait for the portal page to display**Your deployment is complete**.Select

**Go to resource**to go to the Azure Cosmos DB account page.

## Add an output binding

In the Azure portal, navigate to and select the function app you created previously.

Select

**Functions**, and then select the HttpTrigger function.Select

**Integration**and**+ Add output**.Use the

**Create Output**settings as specified in the table:Setting Suggested value Description **Binding Type**Azure Cosmos DB Name of the binding type to select to create the output binding to Azure Cosmos DB. **Document parameter name**taskDocument Name that refers to the Azure Cosmos DB object in code. **Database name**taskDatabase Name of database to save documents. **Collection name**taskCollection Name of the database collection. **If true, creates the Azure Cosmos DB database and collection**Yes The collection doesn't already exist, so create it. **Azure Cosmos DB account connection**New setting Select **New**, then choose**Azure Cosmos DB Account**and the**Database account**you created earlier, and then select**OK**. Creates an application setting for your account connection. This setting is used by the binding to connection to the database.Select

**OK**to create the binding.

## Update the function code

Replace the existing function code with the following code, in your chosen language:

Replace the existing C# function with the following code:

```
#r "Newtonsoft.Json"
using Microsoft.AspNetCore.Mvc;
using Microsoft.AspNetCore.Http;
using Microsoft.Extensions.Logging;
public static IActionResult Run(HttpRequest req, out object taskDocument, ILogger log)
{
string name = req.Query["name"];
string task = req.Query["task"];
string duedate = req.Query["duedate"];
// We need both name and task parameters.
if (!string.IsNullOrEmpty(name) && !string.IsNullOrEmpty(task))
{
taskDocument = new
{
name,
duedate,
task
};
return (ActionResult)new OkResult();
}
else
{
taskDocument = null;
return (ActionResult)new BadRequestResult();
}
}
```


This code sample reads the HTTP Request query strings and assigns them to fields in the `taskDocument`

object. The `taskDocument`

binding sends the object data from this binding parameter to be stored in the bound document database. The database is created the first time the function runs.

## Test the function and database

Select

**Test/Run**. Under**Query**, select**+ Add parameter**and add the following parameters to the query string:`name`

`task`

`duedate`


Select

**Run**and verify that a 200 status is returned.In the Azure portal, search for and select

**Azure Cosmos DB**.Choose your Azure Cosmos DB account, then select

**Data Explorer**.Expand the

**TaskCollection**nodes, select the new document, and confirm that the document contains your query string values, along with some additional metadata.

You've successfully added a binding to your HTTP trigger to store unstructured data in an Azure Cosmos DB instance.

## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

## Next steps

For more information about binding to an Azure Cosmos DB instance, see [Azure Functions Azure Cosmos DB bindings](functions-bindings-cosmosdb).

[Azure Functions triggers and bindings concepts](functions-triggers-bindings)

Learn how Functions integrates with other services.[Azure Functions developer reference](functions-reference)

Provides more technical information about the Functions runtime and a reference for coding functions and defining triggers and bindings.[Code and test Azure Functions locally](functions-develop-local)

Describes the options for developing your functions locally.
