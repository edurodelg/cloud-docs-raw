---
merged_at: 2026-01-26T21:02:36.335247
merged_files: 2
---


---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-table-output -->

# Azure Tables output bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Use an Azure Tables output binding to write entities to a table in [Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table/introduction) or [Azure Table Storage](../storage/tables/table-storage-overview).

For information on setup and configuration details, see the [overview](functions-bindings-storage-table)

Note

This output binding only supports creating new entities in a table. If you need to update an existing entity from your function code, instead use an Azure Tables SDK directly.

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

## Example

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following `MyTableData`

class represents a row of data in the table:

```
public class MyTableData : Azure.Data.Tables.ITableEntity
{
public string Text { get; set; }
public string PartitionKey { get; set; }
public string RowKey { get; set; }
public DateTimeOffset? Timestamp { get; set; }
public ETag ETag { get; set; }
}
```


The following function, which is started by a Queue Storage trigger, writes a new `MyDataTable`

entity to a table named **OutputTable**.

```
[Function("TableFunction")]
[TableOutput("OutputTable", Connection = "AzureWebJobsStorage")]
public static MyTableData Run(
[QueueTrigger("table-items")] string input,
[TableInput("MyTable", "<PartitionKey>", "{queueTrigger}")] MyTableData tableInput,
FunctionContext context)
{
var logger = context.GetLogger("TableFunction");
logger.LogInformation($"PK={tableInput.PartitionKey}, RK={tableInput.RowKey}, Text={tableInput.Text}");
return new MyTableData()
{
PartitionKey = "queue",
RowKey = Guid.NewGuid().ToString(),
Text = $"Output record with rowkey {input} created at {DateTime.Now}"
};
}
```


The following example shows a Java function that uses an HTTP trigger to write a single table row.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() {return this.PartitionKey;}
public void setPartitionKey(String key) {this.PartitionKey = key; }
public String getRowKey() {return this.RowKey;}
public void setRowKey(String key) {this.RowKey = key; }
public String getName() {return this.Name;}
public void setName(String name) {this.Name = name; }
}
public class AddPerson {
@FunctionName("addPerson")
public HttpResponseMessage get(
@HttpTrigger(name = "postPerson", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION, route="persons/{partitionKey}/{rowKey}") HttpRequestMessage<Optional<Person>> request,
@BindingName("partitionKey") String partitionKey,
@BindingName("rowKey") String rowKey,
@TableOutput(name="person", partitionKey="{partitionKey}", rowKey = "{rowKey}", tableName="%MyTableName%", connection="MyConnectionString") OutputBinding<Person> person,
final ExecutionContext context) {
Person outPerson = new Person();
outPerson.setPartitionKey(partitionKey);
outPerson.setRowKey(rowKey);
outPerson.setName(request.getBody().get().getName());
person.setValue(outPerson);
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(outPerson)
.build();
}
}
```


The following example shows a Java function that uses an HTTP trigger to write multiple table rows.

```
public class Person {
private String PartitionKey;
private String RowKey;
private String Name;
public String getPartitionKey() {return this.PartitionKey;}
public void setPartitionKey(String key) {this.PartitionKey = key; }
public String getRowKey() {return this.RowKey;}
public void setRowKey(String key) {this.RowKey = key; }
public String getName() {return this.Name;}
public void setName(String name) {this.Name = name; }
}
public class AddPersons {
@FunctionName("addPersons")
public HttpResponseMessage get(
@HttpTrigger(name = "postPersons", methods = {HttpMethod.POST}, authLevel = AuthorizationLevel.FUNCTION, route="persons/") HttpRequestMessage<Optional<Person[]>> request,
@TableOutput(name="person", tableName="%MyTableName%", connection="MyConnectionString") OutputBinding<Person[]> persons,
final ExecutionContext context) {
persons.setValue(request.getBody().get());
return request.createResponseBuilder(HttpStatus.OK)
.header("Content-Type", "application/json")
.body(request.getBody().get())
.build();
}
}
```


The following example shows a table output binding that writes multiple table entities.

```
import { app, HttpRequest, HttpResponseInit, InvocationContext, output } from '@azure/functions';
const tableOutput = output.table({
tableName: 'Person',
connection: 'MyStorageConnectionAppSetting',
});
interface PersonEntity {
PartitionKey: string;
RowKey: string;
Name: string;
}
export async function httpTrigger1(request: HttpRequest, context: InvocationContext): Promise<HttpResponseInit> {
const rows: PersonEntity[] = [];
for (let i = 1; i < 10; i++) {
rows.push({
PartitionKey: 'Test',
RowKey: i.toString(),
Name: `Name ${i}`,
});
}
context.extraOutputs.set(tableOutput, rows);
return { status: 201 };
}
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [tableOutput],
handler: httpTrigger1,
});
```


```
const { app, output } = require('@azure/functions');
const tableOutput = output.table({
tableName: 'Person',
connection: 'MyStorageConnectionAppSetting',
});
app.http('httpTrigger1', {
methods: ['POST'],
authLevel: 'anonymous',
extraOutputs: [tableOutput],
handler: async (request, context) => {
const rows = [];
for (let i = 1; i < 10; i++) {
rows.push({
PartitionKey: 'Test',
RowKey: i.toString(),
Name: `Name ${i}`,
});
}
context.extraOutputs.set(tableOutput, rows);
return { status: 201 };
},
});
```


The following example demonstrates how to write multiple entities to a table from a function.

Binding configuration in *function.json*:

```
{
"bindings": [
{
"name": "InputData",
"type": "manualTrigger",
"direction": "in"
},
{
"tableName": "Person",
"connection": "MyStorageConnectionAppSetting",
"name": "TableBinding",
"type": "table",
"direction": "out"
}
],
"disabled": false
}
```


PowerShell code in *run.ps1*:

```
param($InputData, $TriggerMetadata)
foreach ($i in 1..10) {
Push-OutputBinding -Name TableBinding -Value @{
PartitionKey = 'Test'
RowKey = "$i"
Name = "Name $i"
}
}
```


The following example demonstrates how to use the Table storage output binding. Configure the `table`

binding in the *function.json* by assigning values to `name`

, `tableName`

, `partitionKey`

, and `connection`

:

The following function generates a unique UUI for the `rowKey`

value and persists the message into Table storage.

```
import logging
import uuid
import json
import azure.functions as func
app = func.FunctionApp()
@app.route(route="table_out_binding")
@app.table_output(arg_name="message",
connection="AzureWebJobsStorage",
table_name="messages")
def table_out_binding(req: func.HttpRequest, message: func.Out[str]):
row_key = str(uuid.uuid4())
data = {
"Name": "Output binding message",
"PartitionKey": "message",
"RowKey": row_key
}
table_json = json.dumps(data)
message.set(table_json)
return table_json
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#table-output).

In [C# class libraries](dotnet-isolated-process-guide), the `TableInputAttribute`

supports the following properties:

| Attribute property | Description |
|---|---|
TableName |
The name of the table to which to write. |
PartitionKey |
The partition key of the table entity to write. |
RowKey |
The row key of the table entity to write. |
Connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the [TableOutput](https://github.com/Azure/azure-functions-java-library/blob/master/src/main/java/com/microsoft/azure/functions/annotation/TableOutput.java/) annotation on parameters to write values into your tables. The attribute supports the following elements:

| Element | Description |
|---|---|
name |
The variable name used in function code that represents the table or entity. |
dataType |
Defines how Functions runtime should treat the parameter value. To learn more, see
|

**tableName****partitionKey****rowKey****connection**[Connections](#connections).## Configuration

The following table explains the properties that you can set on the `options`

object passed to the `output.table()`

method.

| Property | Description |
|---|---|
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `table` . This property is set automatically when you create the binding in the Azure portal. |
direction |
Must be set to `out` . This property is set automatically when you create the binding in the Azure portal. |
name |
The variable name used in function code that represents the table or entity. Set to `$return` to reference the function return value. |
tableName |
The name of the table to which to write. |
partitionKey |
The partition key of the table entity to write. |
rowKey |
The row key of the table entity to write. |
connection |
The name of an app setting or setting collection that specifies how to connect to the table service. See
|

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to your table service. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections)

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string for tables in Azure Table storage, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage). To obtain a connection string for tables in Azure Cosmos DB for Table, follow the steps shown at the [Azure Cosmos DB for Table FAQ](/en-us/azure/cosmos-db/table/table-api-faq#what-is-the-connection-string-that-i-need-to-use-to-connect-to-the-api-for-table-).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage". If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [the Tables API extension](functions-bindings-storage-table#table-api-extension), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). This only applies when accessing tables in Azure Storage. To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Table Service URI | `<CONNECTION_NAME_PREFIX>__tableServiceUri` 1 |
The data plane URI of the Azure Storage table service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.table.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__serviceUri`

can be used as an alias. If both forms are provided, the `tableServiceUri`

form is used. The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables.

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables in Azure Storage. The URI can only designate the table service. As an alternative, you can provide a URI specifically for each service under the same prefix, allowing a single connection to be used.

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You'll need to create a role assignment that provides access to your Azure Storage table service at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) aren't sufficient. The following table shows built-in roles that are recommended when using the Azure Tables extension against Azure Storage in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles (Azure Storage1) |
|---|---|
| Input binding |
|

[Storage Table Data Contributor](../role-based-access-control/built-in-roles#storage-table-data-contributor)1 If your app is instead connecting to tables in Azure Cosmos DB for Table, using an identity isn't supported and the connection must use a connection string.

## Usage

The usage of the binding depends on the extension package version, and the C# modality used in your function app, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see usage details for the mode and version.

When you want the function to write to a single entity, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
| A JSON serializable type that implements [ITableEntity] | Functions attempts to serialize a plain-old CLR object (POCO) type as the entity. The type must implement [ITableEntity] or have a string `RowKey` property and a string `PartitionKey` property. |

When you want the function to write to multiple entities, the Azure Tables output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single entity types |
An array containing multiple entities. Each entry represents one entity. |

For other output scenarios, create and use a [TableClient](/en-us/dotnet/api/azure.data.tables.tableclient) with other types from [Azure.Data.Tables](/en-us/dotnet/api/azure.data.tables) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

There are two options for outputting a Table storage row from a function by using the [TableStorageOutput](/en-us/java/api/com.microsoft.azure.functions.annotation.tableoutput) annotation:

| Options | Description |
|---|---|
Return value |
By applying the annotation to the function itself, the return value of the function persists as a Table storage row. |
Imperative |
To explicitly set the table row, apply the annotation to a specific parameter of the type
`OutputBinding<T>` |

`T`

includes the `PartitionKey`

and `RowKey`

properties. You can accompany these properties by implementing `ITableEntity`

or inheriting `TableEntity`

.To write to table data, use the `Push-OutputBinding`

cmdlet, set the `-Name TableBinding`

parameter and `-Value`

parameter equal to the row data. See the [PowerShell example](#example) for more detail.

There are two options for outputting a Table storage row message from a function:

| Options | Description |
|---|---|
Return value |
Set the `name` property in function.json to `$return` . With this configuration, the function's return value persists as a Table storage row. |
Imperative |
Pass a value to the
`set` is persisted as table row. |

For specific usage details, see [Example](#example).

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Table |
|

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-scale -->

# Azure Functions hosting options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a function app in Azure, you must choose a hosting option for your app. Azure provides you with these hosting options for your function code:

| Hosting option | Service | Availability | Container support |
|---|---|---|---|
|
Azure Functions | Generally available (GA) | None |
|
Azure Functions | GA | Linux |
|
Azure Functions | GA | Linux |
|
Azure Container Apps | GA | Linux |
|
Azure Functions | Windows - GA Linux - Retired |
None |

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

The Azure App Service infrastructure on both Linux and Windows virtual machines facilitates the Azure Functions hosting options. The hosting option you choose dictates the following behaviors:

- How your function app is scaled.
- The resources available to each function app instance.
- Support for advanced functionality, such as Azure Virtual Network connectivity.
- Support for Linux containers.

The plan you choose also impacts the costs for running your function code. For more information, see [Billing](#billing).

This article provides a detailed comparison between the various hosting options. To learn more about running and managing your function code in Linux containers, see [Linux container support in Azure Functions](container-concepts).

## Overview of plans

The following table summarizes the benefits of the various options for Azure functions hosting.

| Option | Benefits |
|---|---|
|
Experience fast horizontal scaling, with flexible compute options, virtual network integration, and serverless pay-as-you-go billing. In the Flex Consumption plan, function instances dynamically scale out (up to 1,000) based on configured per-instance concurrency, incoming events, and per-function workloads for optimal efficiency. Consider the Flex Consumption plan when: ✔ You need a serverless host for your function code, paying only for on-demand executions. ✔ You require virtual network connectivity for secure access to Azure resources. ✔ Your workloads are variable and can go from no activity to demanding rapid, event-driven scaling. ✔ You want to customize compute with memory sizes (512 MB, 2,048 MB, or 4,096 MB) and reduce cold starts via one or more pre-provisioned (always-ready) instances. |
|
Automatically scales based on demand using prewarmed workers, which run applications with no delay after being idle, runs on more powerful instances, and connects to virtual networks. Consider the Azure Functions Premium plan in the following situations: ✔ Your function apps run continuously, or nearly continuously. ✔ You want more control of your instances and want to deploy multiple function apps on the same plan with event-driven scaling. ✔ You have a high number of small executions and a high execution bill, but low GB seconds in the Consumption plan. ✔ You need more CPU or memory options than are provided by consumption plans. ✔ Your code needs to run longer than the maximum execution time allowed on the Consumption plan. ✔ You require virtual network connectivity for secure access to Azure resources. ✔ You want to provide a custom Linux image in which to run your functions. |
|
Run your functions within an App Service plan at regular
Best for long-running scenarios where
✔ You have existing and underutilized virtual machines that are already running other App Service instances. ✔ You must have fully predictable billing, or you need to manually scale instances. ✔ You want to run multiple web apps and function apps on the same plan ✔ You need access to larger compute size choices. ✔ Full compute isolation and secure network access provided by an App Service Environment (ASE). ✔ Very high memory usage and high scale (ASE). |

[Container Apps](../container-apps/functions-overview)Use the Azure Functions programming model to build event-driven, serverless, cloud native function apps. Run your functions alongside other microservices, APIs, websites, and workflows as container-hosted programs. Consider hosting your functions on Container Apps in the following situations:

✔ You want control of the container image and want to package custom libraries with your function code to support line-of-business apps.

✔ You need to migrate code execution from on-premises or legacy apps to cloud native microservices running in containers.

✔ When you want to avoid the overhead and complexity of managing Kubernetes clusters and dedicated compute.

✔ Your functions need high-end processing power provided by dedicated GPU compute resources.

[Consumption plan](consumption-plan)On the Consumption plan, function instances are dynamically added and removed based on the number of incoming events.

Consider the Consumption plan when:

✔ You have a dependency on Windows. For example, using the v1 runtime, the full .NET Framework, or Windows-specific features like certain PowerShell modules.

✔ You want a serverless billing model and pay only when your functions are running.

The remaining tables in this article compare hosting options based on various features and behaviors.

## Operating system support

This table shows operating system support for the hosting options.

| Hosting | Linux1 deployment |
Windows2 deployment |
|---|---|---|
|
✅ Code-only ❌ Container (not supported) |
❌ Not supported |
|
✅ Code-only ✅ Container |
✅ Code-only |
|
✅ Code-only ✅ Container |
✅ Code-only |
|
✅ Container-only | ❌ Not supported |
3 |
✅ Code-only (Retired) ❌ Container (not supported) |
✅ Code-only |

- Linux is the only supported operating system for the
[Python runtime stack](functions-reference-python). - Windows deployments are code-only. Azure Functions doesn't currently support Windows containers.
- The ability to run your app on Linux in a Consumption plan will be retired on 30 September 2028. For more information, see
[Consumption plan](consumption-plan).

## Function app timeout duration

The `functionTimeout`

property in the [host.json](functions-host-json#functiontimeout) project file sets the timeout duration for functions in a function app. This property applies specifically to function executions. After the trigger starts function execution, the function needs to return or respond within the timeout duration. When an execution exceeds this duration, a timeout error occurs and the language worker process restarts. For C# apps running in-process, the host process itself restarts. To avoid timeouts and subsequent process restarts, it's important to [write robust functions](functions-best-practices#write-robust-functions). For more information, see [Improve Azure Functions performance and reliability](performance-reliability#make-sure-background-tasks-complete).

The following table shows the default and maximum values (in minutes) for specific plans:

| Plan | Default | Maximum1 |
|---|---|---|
|
30 | Unbounded2 |
|
304 |
Unbounded2 |
|
304 |
Unbounded3 |
|
30 | Unbounded5 |
|
5 | 10 |

- Regardless of the function app timeout setting, 230 seconds is the maximum amount of time that an HTTP triggered function can take to respond to a request. This limit exists because of the
[default idle timeout of Azure Load Balancer](../app-service/faq-availability-performance-application-issues#why-does-my-request-time-out-after-230-seconds). For longer processing times, consider using the[Durable Functions async pattern](durable/durable-functions-overview#async-http)or[defer the actual work and return an immediate response](performance-reliability#avoid-long-running-functions). - There's no maximum execution timeout duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors)for the Flex Consumption and Premium plans, and a grace period of 10 minutes is given during platform updates. - Requires the App Service plan be set to
[Always On](/en-us/azure/azure-functions/dedicated-plan#always-on). A grace period of 10 minutes is given during platform updates. - The default timeout for version 1.x of the Functions host runtime is
*unbounded*. - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to zero, the default timeout depends on the specific triggers used in the app.

These values assume that the Azure Functions host process starts and runs correctly. There's a maximum timeout of 60 seconds for the language-specific worker process to also start. The worker process startup timeout isn't currently configurable.

## Language support

For details on current native language stack support in Functions, see [Supported languages in Azure Functions](supported-languages).

## Scale

The following table compares the scaling behaviors of the various hosting plans.

Maximum instances are given on a per-function app (Consumption) or per-plan (Premium/Dedicated) basis, unless otherwise indicated.

| Plan | Scale out | Max # instances |
|---|---|---|
|
Fast event-driven scaling decisions are calculated on a per-function basis, called
|

1[Premium plan](functions-premium-plan)[Event driven](event-driven-scaling). Scale out automatically, even during periods of high load. Azure Functions infrastructure scales CPU and memory resources by adding more instances of the Functions host, based on the number of events that its functions are triggered on.**Windows:**1006**Linux:**20-1002,6[Dedicated plan](dedicated-plan)3100 (ASE)

[Container Apps](../container-apps/functions-overview)[Event driven](event-driven-scaling). Scale out automatically, even during periods of high load. Azure Functions infrastructure scales CPU and memory resources by adding more instances of the Functions host, based on the number of events that its functions are triggered on.4[Consumption plan](consumption-plan)[Event driven](event-driven-scaling). Automatic scale based on the source of events. Functions infrastructure scales resources by adding more instances of the function host, based on the number of incoming trigger events.**Windows:**200**Linux:**1005- Flex Consumption plan has a regional subscription quota that limits the total memory usage of all instances across a given region. For more information, see
[Regional subscription memory quotas](flex-consumption-plan#regional-subscription-memory-quotas). Flex Consumption plans currently only support Linux. - In some regions, Linux apps on a Premium plan can scale to 100 instances. For more information, see the
[Premium plan article](functions-premium-plan#region-max-scale-out). - For specific limits for the various App Service plan options, see the
[App Service plan limits](../azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits). - On Container Apps, the default is 10 instances, but you can set the
[maximum number of replicas](../container-apps/scale-app#scale-definition), which has an overall maximum of 1000. This setting is honored as long as there's enough cores quota available. For more information, see[Quotas for Azure Container Apps](/en-us/azure/container-apps/quotas). When you create your function app from the Azure portal, you're limited to 300 instances. - During scale-out, there's currently a limit of 500 instances per subscription per hour for Linux apps on a Consumption plan.
- For private endpoint restricted http triggers, scaling out is limited to at most 20 instances.

## Cold start behavior

| Plan | Details |
|---|---|
|
Improved cold start even when scaled to zero. Supports
|

[Premium plan](functions-premium-plan)[always ready instances](functions-premium-plan#always-ready-instances)to avoid cold starts by letting you maintain one or more*perpetually warm*instances.[Dedicated plan](dedicated-plan)[Container Apps](../container-apps/functions-overview)[minimum number of replicas](../container-apps/scale-app#scale-definition):• When set to zero: apps can scale to zero when idle and some requests might have more latencies at startup.

• When set to one or more: the host process runs continuously, which means that cold start isn't an issue.

[Consumption plan](consumption-plan)## Service limits

| Resource |
|
|---|

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)/

[ASE](../app-service/environment/overview)

[Container Apps](../container-apps/functions-overview)

[Consumption plan](consumption-plan)

[time-out duration](/en-us/azure/azure-functions/functions-scale#timeout)(min)116[time-out duration](/en-us/azure/azure-functions/functions-scale#timeout)(min)99217[App Service limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits)333[ACU](/en-us/azure/virtual-machines/acu)per instance10[varies](/en-us/azure/container-apps/billing)14[varies](/en-us/azure/container-apps/billing)1511181344[App Service plans](/en-us/azure/app-service/overview-hosting-plans)[region](https://azure.microsoft.com/global-infrastructure/regions/)[Deployment slots](/en-us/azure/azure-functions/functions-deployment-slots)per app121157116,788[TSL/SSL support](/en-us/azure/app-service/configure-ssl-bindings)Notes on service limits:

- By default, the time-out for the Functions 1.x runtime in an App Service plan is unbounded.
- Requires the App Service plan be set to
[Always On](/en-us/azure/azure-functions/dedicated-plan#always-on). Pay at standard[rates](https://azure.microsoft.com/pricing/details/app-service/). A grace period of 10 minutes is given for HTTP triggered functions during platform updates but not for other triggers. - These limits are
[set in the host](https://github.com/Azure/azure-functions-host/blob/dev/src/WebJobs.Script.WebHost/web.config). - The actual number of function apps that you can host depends on the activity of the apps, the size of the machine instances, and the corresponding resource utilization.
- The storage limit is the total content size in temporary storage across all apps in the same App Service plan. For Consumption plans on Linux, the storage is currently 1.5 GB.
- Consumption plan uses an Azure Files share for persisted storage. When you provide your own Azure Files share, the specific share size limits depend on the storage account you set for
[WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](/en-us/azure/azure-functions/functions-app-settings#website_contentazurefileconnectionstring). - On Linux, you must
[explicitly mount your own Azure Files share](/en-us/azure/azure-functions/storage-considerations#mount-file-shares). - When your function app is hosted in a
[Consumption plan](/en-us/azure/azure-functions/consumption-plan), only the CNAME option is supported. For function apps in a[Premium plan](/en-us/azure/azure-functions/functions-premium-plan)or an[App Service plan](/en-us/azure/azure-functions/dedicated-plan), you can map a custom domain using either a CNAME or an A record. - There's no maximum execution time-out duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors)and 10 minutes during platform updates. - Workers are roles that host customer apps. Workers are available in three fixed sizes: One vCPU/3.5 GB RAM; Two vCPU/7 GB RAM; Four vCPU/14 GB RAM.
- See
[App Service limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#app-service-limits)for details. - Including the production slot.
- There's currently a limit of 5,000 function apps in a given subscription.
- Flex Consumption plan instance sizes are currently defined as 512 MB, 2,048 MB, or 4,096 MB. For more information, see
[Instance memory](/en-us/azure/azure-functions/flex-consumption-plan#instance-sizes). - For details, see
[Scale](functions-scale#scale)in the Hosting comparison article. - When the
[minimum number of replicas](/en-us/azure/container-apps/scale-app#scale-definition)is set to zero, the default time-out depends on the specific triggers used in the app. - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to one or more.

## Networking features

| Feature |
|
|---|

[Consumption plan](consumption-plan)

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)/

[ASE](../app-service/environment/intro)

[Container Apps](../container-apps/functions-overview)

1

[Inbound IP restrictions](functions-networking-options#inbound-networking-features)[Inbound Private Endpoints](functions-networking-options#inbound-networking-features)[Virtual network integration](functions-networking-options#virtual-network-integration)23[Outbound IP restrictions](functions-networking-options#outbound-ip-restrictions)- For more information, see
[Networking in Azure Container Apps environment](../container-apps/networking). - There are special considerations when working with
[virtual network triggers](functions-networking-options#virtual-network-triggers-non-http). - Only the Dedicated/ASE plan supports gateway-required virtual network integration.

## Billing

| Plan | Details |
|---|---|
|
Billing is based on number of executions, the memory of instances when they're actively executing functions, plus the cost of any
|

[Premium plan](functions-premium-plan)[Dedicated plan](dedicated-plan)For an ASE, there's a flat monthly rate that pays for the infrastructure and doesn't change with the size of the environment. There's also a cost per App Service plan vCPU. All apps hosted in an ASE are in the Isolated pricing model. For more information, see the

[ASE overview article](../app-service/environment/overview#pricing).[Container Apps](../container-apps/functions-overview)[Billing in Azure Container Apps](../container-apps/billing).[Consumption plan](consumption-plan)For a direct cost comparison between dynamic hosting plans (Consumption, Flex Consumption, and Premium), see the [Azure Functions pricing page](https://azure.microsoft.com/pricing/details/functions/). For pricing of the various Dedicated plan options, see the [App Service pricing page](https://azure.microsoft.com/pricing/details/app-service). For pricing Container Apps hosting, see [Azure Container Apps pricing](https://azure.microsoft.com/pricing/details/container-apps/).

## Limitations for creating new function apps in an existing resource group

In some cases, when trying to create a new hosting plan for your function app in an existing resource group you might receive one of the following errors:

- The pricing tier isn't allowed in this resource group
- <SKU_name> workers aren't available in resource group <resource_group_name>

These errors can occur when the following conditions are met:

- You create a function app in an existing resource group that has yet to contain another function app or web app. For example, Linux Consumption apps aren't supported in the same resource group as Linux Dedicated or Linux Premium plans.
- Your new function app is created in the same region as the previous app.
- The previous app is in some way incompatible with your new app. This incompatibility can occur between versions, operating systems, or is due to other platform-level features, such as availability zone support.

Function app and web app plans are mapped to different pools of resources when they're created. Different plans require a different set of infrastructure capabilities. When you create an app in a resource group, that resource group is mapped and assigned to a specific pool of resources. If you try to create another plan in that resource group and the mapped pool doesn't have the required resources, the previously mentioned errors occur.

If this situation happens, create your function app and hosting plan in a new resource group instead.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-networking-options -->

# Azure Functions networking options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes the networking features available across the hosting options for Azure Functions. The following networking options can be categorized as inbound and outbound networking features. Inbound features allow you to restrict access to your app, whereas outbound features allow you to connect your app to resources secured by a virtual network and control how outbound traffic is routed.

The [hosting models](functions-scale) have different levels of network isolation available. Choosing the correct one helps you meet your network isolation requirements.

| Feature |
|
|---|

[Consumption plan](consumption-plan)

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)/

[ASE](../app-service/environment/intro)

[Container Apps](../container-apps/functions-overview)

1

[Inbound IP restrictions](functions-networking-options#inbound-networking-features)[Inbound Private Endpoints](functions-networking-options#inbound-networking-features)[Virtual network integration](functions-networking-options#virtual-network-integration)23[Outbound IP restrictions](functions-networking-options#outbound-ip-restrictions)- For more information, see
[Networking in Azure Container Apps environment](../container-apps/networking). - There are special considerations when working with
[virtual network triggers](functions-networking-options#virtual-network-triggers-non-http). - Only the Dedicated/ASE plan supports gateway-required virtual network integration.

## Quickstart resources

Use the following resources to quickly get started with Azure Functions networking scenarios. These resources are referenced throughout the article.

- ARM templates, Bicep files, and Terraform templates:
- ARM templates only:
- Tutorials:

## Inbound networking features

The following features let you filter inbound requests to your function app.

### Inbound access restrictions

You can use access restrictions to define a priority-ordered list of IP addresses that are allowed or denied access to your app. The list can include IPv4 and IPv6 addresses, or specific virtual network subnets using [service endpoints](#use-service-endpoints). When there are one or more entries, an implicit "deny all" exists at the end of the list. IP restrictions work with all function-hosting options.

Access restrictions are available in the [Flex Consumption plan](flex-consumption-plan), [Elastic Premium](functions-premium-plan), [Consumption](consumption-plan), and [App Service](dedicated-plan).

Note

With network restrictions in place, you can deploy only from within your virtual network, or when you put the IP address of the machine you're using to access the Azure portal on the **Safe Recipients** list. However, you can still manage the function using the portal.

To learn more, see [Azure App Service static access restrictions](../app-service/app-service-ip-restrictions).

### Private endpoints

[Azure Private Endpoint](../private-link/private-endpoint-overview) is a network interface that connects you privately and securely to a service powered by Azure Private Link. Private Endpoint uses a private IP address from your virtual network, effectively bringing the service into your virtual network.

You can use Private Endpoint for your functions hosted in the [Flex Consumption](flex-consumption-plan), [Elastic Premium](functions-premium-plan), and [Dedicated (App Service)](dedicated-plan) plans.

If you want to make calls to Private Endpoints, then you must make sure that your DNS lookups resolve to the private endpoint. You can enforce this behavior in one of the following ways:

- Integrate with Azure DNS private zones. When your virtual network doesn't have a custom DNS server, this is done automatically.
- Manage the private endpoint in the DNS server used by your app. To manage a private endpoint, you must know the endpoint address and use an A record to reference the endpoint you're trying to reach.
- Configure your own DNS server to forward to
[Azure DNS private zones](../dns/private-dns-privatednszone).

To learn more, see [using Private Endpoints for Web Apps](../app-service/networking/private-endpoint).

To call other services that have a private endpoint connection, such as storage or service bus, be sure to configure your app to make [outbound calls to private endpoints](#private-endpoints). For more details on using private endpoints with the storage account for your function app, visit [restrict your storage account to a virtual network](#restrict-your-storage-account-to-a-virtual-network).

### Service endpoints

Using service endpoints, you can restrict many Azure services to selected virtual network subnets to provide a higher level of security. Regional virtual network integration enables your function app to reach Azure services that are secured with service endpoints. This configuration is supported on all [plans](functions-scale#networking-features) that support virtual network integration. Follow these steps to access a secured service endpoint:

- Configure regional virtual network integration with your function app to connect to a specific subnet.
- Go to the destination service and configure service endpoints against the integration subnet.

To learn more, see [Virtual network service endpoints](../virtual-network/virtual-network-service-endpoints-overview).

#### Use Service Endpoints

To restrict access to a specific subnet, create a restriction rule with a **Virtual Network** type. You can then select the subscription, virtual network, and subnet that you want to allow or deny access to.

If service endpoints aren't already enabled with `Microsoft.Web`

for the subnet that you selected, they're automatically enabled unless you select the **Ignore missing Microsoft.Web service endpoints** check box. The scenario where you might want to enable service endpoints on the app but not the subnet depends mainly on whether you have the permissions to enable them on the subnet.

If you need someone else to enable service endpoints on the subnet, select the **Ignore missing Microsoft.Web service endpoints** check box. Your app is configured for service endpoints, which you enable later on the subnet.

You can't use service endpoints to restrict access to apps that run in an App Service Environment. When your app is in an App Service Environment, you can control access to it by applying IP access rules.

To learn how to set up service endpoints, see [Establish Azure Functions private site access](functions-create-private-site-access).

## Outbound networking features

You can use the features in this section to manage outbound connections made by your app.

### Virtual network integration

This section details the features that Functions supports to control data outbound from your app.

Virtual network integration gives your function app access to resources in your virtual network. Once integrated, your app routes outbound traffic through the virtual network. This allows your app to access private endpoints or resources with rules allowing traffic from only select subnets. When the destination is an IP address outside of the virtual network, the source IP will still be sent from the one of the addresses listed in your app's properties, unless you've configured a NAT Gateway.

Azure Functions supports two kinds of virtual network integration:

[Regional virtual network integration](#regional-virtual-network-integration)for apps running on the[Flex Consumption](flex-consumption-plan),[Elastic Premium](functions-premium-plan),[Dedicated (App Service)](dedicated-plan), and[Container Apps](functions-container-apps-hosting)hosting plans (recommended)[Gateway-required virtual network integration](../app-service/configure-gateway-required-vnet-integration)for apps running on the[Dedicated (App Service)](dedicated-plan)hosting plan

To learn how to set up virtual network integration, see [Enable virtual network integration](#enable-virtual-network-integration).

### Regional virtual network integration

Using regional virtual network integration enables your app to access:

- Resources in the same virtual network as your app.
- Resources in virtual networks peered to the virtual network your app is integrated with.
- Service endpoint secured services.
- Resources across Azure ExpressRoute connections.
- Resources across peered connections, which include Azure ExpressRoute connections.
- Private endpoints

When you use regional virtual network integration, you can use the following Azure networking features:

: You can block outbound traffic with an NSG that's placed on your integration subnet. The inbound rules don't apply because you can't use virtual network integration to provide inbound access to your app.[Network security groups (NSGs)](#network-security-groups): You can place a route table on the integration subnet to send outbound traffic where you want.[Route tables (UDRs)](#routes)

Note

When you route all of your outbound traffic into your virtual network, it's subject to the NSGs and UDRs that are applied to your integration subnet. When virtual network integrated, your function app's outbound traffic to public IP addresses is still sent from the addresses that are listed in your app properties, unless you provide routes that direct the traffic elsewhere.

Regional virtual network integration isn't able to use port 25.

Considerations for the [Flex Consumption](flex-consumption-plan) plan:

- The app and the virtual network must be in the same region.
- Ensure that the
`Microsoft.App`

Azure resource provider is enabled for your subscription by[following these instructions](../azure-resource-manager/management/resource-providers-and-types#register-resource-provider). This is needed for subnet delegation. The Azure portal and Azure CLI enforce this registration when you create a Flex Consumption app, since virtual network integration can be enabled at any point after your app is created. - The subnet delegation required when running in a Flex Consumption plan is
`Microsoft.App/environments`

. This differs from the Elastic Premium and Dedicated (App Service) plans, which have a different delegation requirement. - You can plan for 40 IP addresses to be used at the most for one function app, even if the app scales beyond 40. For example, if you have 15 Flex Consumption function apps that are integrated in the same subnet, you must plan for 15x40 = 600 IP addresses used at the most. This limit is subject to change, and isn't enforced.
- The subnet can't already be in use for other purposes (like private or service endpoints, or
[delegated](../virtual-network/subnet-delegation-overview)to any other hosting plan or service). While you can share the same subnet with multiple Flex Consumption apps, the networking resources are shared across these function apps, which can lead to one app impacting the performance of others on the same subnet. - You can't share the same subnet between a Container Apps environment and a Flex Consumption app.
- The Flex Consumption plan currently doesn't support subnets with names that contain underscore (
`_`

) characters.

Considerations for the [Elastic Premium](functions-premium-plan), [Dedicated (App Service)](dedicated-plan), and [Container Apps](functions-container-apps-hosting) plans:

- The feature is available for Elastic Premium and App Service Premium V2 and Premium V3. It's also available in Standard but only from newer App Service deployments. If you are on an older deployment, you can only use the feature from a Premium V2 App Service plan. If you want to make sure you can use the feature in a Standard App Service plan, create your app in a Premium V3 App Service plan. Those plans are only supported on our newest deployments. You can scale down if you desire after that.
- The feature can't be used by Isolated plan apps that are in an App Service Environment.
- The app and the virtual network must be in the same region.
- The feature requires an unused subnet that's a /28 or larger in an Azure Resource Manager virtual network.
- The integration subnet can be used by only one App Service plan.
- You can have up to two regional virtual network integrations per App Service plan. Multiple apps in the same App Service plan can use the same integration subnet.
- The subnet can't already be in use for other purposes (like private or service endpoints, or
[delegated](../virtual-network/subnet-delegation-overview)to the Flex Consumption plan or any other service). While you can share the same subnet with multiple apps in the same App Service plan, the networking resources are shared across these function apps, which can lead to one app impacting the performance of others on the same subnet. - You can't delete a virtual network with an integrated app. Remove the integration before you delete the virtual network.
- You can't change the subscription of an app or a plan while there's an app that's using regional virtual network integration.

### Enable virtual network integration

In your function app in the

[Azure portal](https://portal.azure.com), select**Networking**, then under**VNet Integration**select**Click here to configure**.Select

**Add VNet**.The drop-down list contains all of the Azure Resource Manager virtual networks in your subscription in the same region. Select the virtual network you want to integrate with.

The Flex Consumption and Elastic Premium hosting plans only support regional virtual network integration. If the virtual network is in the same region, either create a new subnet or select an empty, pre-existing subnet.

To select a virtual network in another region, you must have a virtual network gateway provisioned with point to site enabled. Virtual network integration across regions is only supported for Dedicated plans, but global peerings work with regional virtual network integration.


During the integration, your app is restarted. When integration is finished, you see details on the virtual network you're integrated with. By default, Route All is enabled, and all traffic is routed into your virtual network.

If you prefer to only have your private traffic ([RFC1918](https://datatracker.ietf.org/doc/html/rfc1918#section-3) traffic) routed, follow the steps in this [App Service article](../app-service/overview-vnet-integration#application-routing).

### Subnets

Virtual network integration depends on a dedicated subnet. When you provision a subnet, Azure reserves the first five IP addresses for internal use. The way remaining IP addresses are consumed depends on your hosting plan. Since subnet size can't be changed after assignment, use a subnet that's large enough to accommodate whatever scale your app might reach.

#### Elastic Premium and Dedicated Plans

In Elastic Premium and Dedicated (App Service) plans, each running instance of your function app consumes one IP address from the subnet. When you scale up or down, the required address space may temporarily double to accommodate the transition. If multiple apps share the same subnet, the total IP address usage is the sum of all instances across those apps, plus the temporary doubling during scaling events.

**IP Consumption Scenarios**

| Scenario | IP Address Consumption |
|---|---|
| 1 app, 1 instance | 1 IP address |
| 1 app, 5 instances | 5 IP addresses |
| 1 app, scaling from 5 to 10 instances | Up to 20 IP addresses (temporary, during scale operation) |
| 3 apps, 5 instances each | 15 IP addresses |

**CIDR Range Recommendations**

| CIDR block size | Max available addresses | Max horizontal scale (instances)1 |
|---|---|---|
| /28 | 11 | 5 |
| /27 | 27 | 13 |
| /26 | 59 | 29 |
| /25 | 123 | 612 |
| /24 | 251 | 1253 |

1Assumes that you need to scale up or down in either size or SKU at some point.

2 Although the number of IP addresses supports 61 instances, individual apps on the Dedicated plan have a [30 instance maximum](functions-scale#scale).

2 Although the number of IP addresses supports 125 instances, individual apps on the Elastic Premium plan have a [100 instance maximum](functions-scale#scale).

**Additional Considerations**

For function apps on the Elastic Premium or Dedicated plans:

- To avoid any issues with subnet capacity for Functions Elastic Premium plans, you should use a /24 with 256 addresses for Windows and a /26 with 64 addresses for Linux. When creating subnets in Azure portal as part of integrating with the virtual network, a minimum size of /24 and /26 is required for Windows and Linux respectively.
- Each App Service plan can support up to two subnets that can be used for VNet integration. Multiple apps from a single App Service plan can join the same subnet, but apps from a different plan can't use that same subnet.

#### Flex Consumption Plan

In the Flex Consumption plan, outbound network traffic from function app instances are routed through shared gateways that are dedicated to the subnet. Each shared gateway consumes 1 IP address from the subnet. Regardless of how many apps are integrated with a single subnet, at most 27 shared gateways (27 IP addresses) will be used to support all instances. When selecting a subnet size, what matters is the total number of instances across all apps integrated with the subnet. When a subnet is used for too many instances or for apps performing I/O intensive workloads, network capacity issues may occur such as increased average latency and timeouts. The scale-out of apps will not be affected.

A /27 subnet size (27 usable IP addresses) is recommended to support a single function app, which can scale-out to a maximum of 1,000 instances.

If you expect your single function app to scale beyond 1,000 instances or expect the total instance count of multiple function apps to exceed 1,000 instances, then use a /26 subnet and contact the product group to request an increase to your maximum instance count.

Important

Integrating Flex Consumption function apps with a subnet size less than /27 or integrating multiple apps with a /27 size subnet reduces the available outbound network capacity for them. If you plan to do so, load test your apps with production-scale workloads to ensure network capacity constraints are not observed.

**IP Consumption Scenarios**

| Scenario | Maximum IP Address Consumption |
|---|---|
| 1 app | Up to 27 IP addresses (/27 subnet size) |
| 2 apps | Up to 27 IP addresses (/27 subnet size) |
| 10 apps | Up to 27 IP addresses (/27 subnet size) |

### Network security groups

You can use [network security groups](../virtual-network/network-security-groups-overview) to control traffic between resources in your virtual network. For example, you can create a security rule that blocks your app's outbound traffic from reaching a resource in your virtual network or from leaving the network. These security rules apply to apps that have configured virtual network integration. To block traffic to public addresses, you must have virtual network integration and Route All enabled. The inbound rules in an NSG don't apply to your app because virtual network integration affects only outbound traffic from your app.

To control inbound traffic to your app, use the Access Restrictions feature. An NSG that's applied to your integration subnet is in effect regardless of any routes applied to your integration subnet. If your function app is virtual network integrated with [Route All](../app-service/configure-vnet-integration-routing#configure-application-routing) enabled, and you don't have any routes that affect public address traffic on your integration subnet, all of your outbound traffic is still subject to NSGs assigned to your integration subnet. When Route All isn't enabled, NSGs are only applied to RFC1918 traffic.

### Routes

You can use route tables to route outbound traffic from your app to wherever you want. By default, route tables only affect your RFC1918 destination traffic. When [Route All](../app-service/overview-vnet-integration#application-routing) is enabled, all of your outbound calls are affected. When Route All is disabled, only private traffic (RFC1918) is affected by your route tables. Routes that are set on your integration subnet won't affect replies to inbound app requests. Common destinations can include firewall devices or gateways.

If you want to route all outbound traffic on-premises, you can use a route table to send all outbound traffic to your ExpressRoute gateway. If you do route traffic to a gateway, be sure to set routes in the external network to send any replies back.

Border Gateway Protocol (BGP) routes also affect your app traffic. If you have BGP routes from something like an ExpressRoute gateway, your app outbound traffic is affected. By default, BGP routes affect only your RFC1918 destination traffic. When your function app is virtual network integrated with **Route All** enabled, all outbound traffic can be affected by your BGP routes.

### Outbound IP restrictions

Outbound IP restrictions are available in a Flex Consumption plan, Elastic Premium plan, App Service plan, or App Service Environment. You can configure outbound restrictions for the virtual network where your App Service Environment is deployed.

When you integrate a function app in an Elastic Premium plan or an App Service plan with a virtual network, the app can still make outbound calls to the internet by default. By integrating your function app with a virtual network with Route All enabled, you force all outbound traffic to be sent into your virtual network, where network security group rules can be used to restrict traffic. For Flex Consumption all traffic is already routed through the virtual network and **Route All** isn't needed.

To learn how to control the outbound IP using a virtual network, see [Tutorial: Control Azure Functions outbound IP with an Azure virtual network NAT gateway](functions-how-to-use-nat-gateway).

### Azure DNS private zones

After your app integrates with your virtual network, it uses the same DNS server that your virtual network is configured with and will work with the Azure DNS private zones linked to the virtual network.

### Automation

The following APIs let you programmatically manage regional virtual network integrations:

**Azure CLI**: Use thecommands to add, list, or remove a regional virtual network integration.`az functionapp vnet-integration`

**ARM templates**: Regional virtual network integration can be enabled by using an Azure Resource Manager template. For a full example, see[this Functions quickstart template](https://azure.microsoft.com/resources/templates/function-premium-vnet-integration/).

## Hybrid Connections

[Hybrid Connections](../azure-relay/relay-hybrid-connections-protocol) is a feature of Azure Relay that you can use to access application resources in other networks. It provides access from your app to an application endpoint. You can't use it to access your application. Hybrid Connections is available to functions that run on Windows in all but the Consumption plan.

As used in Azure Functions, each hybrid connection correlates to a single TCP host and port combination. This means that the hybrid connection's endpoint can be on any operating system and any application as long as you're accessing a TCP listening port. The Hybrid Connections feature doesn't know or care what the application protocol is or what you're accessing. It just provides network access.

To learn more, see the [App Service documentation for Hybrid Connections](../app-service/app-service-hybrid-connections). These same configuration steps support Azure Functions.

Important

Hybrid Connections is only supported when your function app runs on Windows. Linux apps aren't supported.

## Connecting to Azure Services through a virtual network

Virtual network integration enables your function app to access resources in a virtual network. This section overviews things you should consider when attempting to connect your app to certain services.

### Restrict your storage account to a virtual network

Note

To quickly deploy a function app with private endpoints enabled on the storage account, refer to the following template: [Function app with Azure Storage private endpoints](https://github.com/Azure/azure-quickstart-templates/tree/master/quickstarts/microsoft.web/function-app-storage-private-endpoints).

When you create a function app, you must create or link to a general-purpose Azure Storage account that supports Blob, Queue, and Table storage. You can replace this storage account with one that is secured with service endpoints or private endpoints.

You can use a network restricted storage account with function apps on the Flex Consumption, Elastic Premium, and Dedicated (App Service) plans; the Consumption plan isn't supported. For Elastic Premium and Dedicated plans, you have to ensure that private [content share routing](../app-service/configure-vnet-integration-routing#content-share) is configured. To learn how to configure your function app with a storage account secured with a virtual network, see [Restrict your storage account to a virtual network](configure-networking-how-to#restrict-your-storage-account-to-a-virtual-network).

### Use Key Vault references

You can use Azure Key Vault references to use secrets from Azure Key Vault in your Azure Functions application without requiring any code changes. Azure Key Vault is a service that provides centralized secrets management, with full control over access policies and audit history.

If virtual network integration is configured for the app, [Key Vault references](../app-service/app-service-key-vault-references) can be used to retrieve secrets from a network-restricted vault.

### Virtual network triggers (non-HTTP)

Your workload might require your app to be triggered from an event source protected by a virtual network. There's two options if you want your app to dynamically scale based on the number of events received from non-HTTP trigger sources:

- Run your function app in a
[Flex Consumption](flex-consumption-plan). - Run your function app in an
[Elastic Premium plan](functions-premium-plan)and enable virtual network trigger support.

Function apps running on the [Dedicated (App Service)](dedicated-plan) plans don't dynamically scale based on events. Rather, scale out is dictated by [autoscale](dedicated-plan#scaling) rules you define.

#### Elastic Premium plan with virtual network triggers

The [Elastic Premium plan](functions-premium-plan) lets you create functions that are triggered by services secured by a virtual network. These non-HTTP triggers are known as *virtual network triggers*.

By default, virtual network triggers don't cause your function app to scale beyond their prewarmed instance count. However, certain extensions support virtual network triggers that cause your function app to scale dynamically. You can enable this *dynamic scale monitoring* in your function app for supported extensions in one of these ways:

In the

[Azure portal](https://portal.azure.com), navigate to your function app.Under

**Settings**select**Configuration**, then in the**Function runtime settings**tab set**Runtime Scale Monitoring**to**On**.Select

**Save**to update the function app configuration and restart the app.


Tip

Enabling the monitoring of virtual network triggers can affect the performance of your application, though the impact is likely to be small.

Support for dynamic scale monitoring of virtual network triggers isn't available in version 1.x of the Functions runtime.

The extensions in this table support dynamic scale monitoring of virtual network triggers. To get the best scaling performance, you should upgrade to versions that also support [target-based scaling](functions-target-based-scaling#premium-plan-with-runtime-scale-monitoring-enabled).

| Extension (minimum version) | Runtime scale monitoring only | With
|
|---|

[Microsoft.Azure.WebJobs.Extensions.CosmosDB](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.CosmosDB)[Microsoft.Azure.WebJobs.Extensions.DurableTask](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DurableTask)[Microsoft.Azure.WebJobs.Extensions.EventHubs](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.EventHubs)[Microsoft.Azure.WebJobs.Extensions.ServiceBus](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.ServiceBus)[Microsoft.Azure.WebJobs.Extensions.Storage](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.Storage/)** Queue storage only.

Important

When you enable virtual network trigger monitoring, only triggers for these extensions can cause your app to scale dynamically. You can still use triggers from extensions that aren't in this table, but they won't cause scaling beyond their prewarmed instance count. For a complete list of all trigger and binding extensions, see [Triggers and bindings](functions-triggers-bindings#supported-bindings).

#### App Service plan and App Service Environment with virtual network triggers

When your function app runs in either an App Service plan or an App Service Environment, you can write functions that are triggered by resources secured by a virtual network. For your functions to get triggered correctly, your app must be connected to a virtual network with access to the resource defined in the trigger connection.

For example, assume you want to configure Azure Cosmos DB to accept traffic only from a virtual network. In this case, you must deploy your function app in an App Service plan that provides virtual network integration with that virtual network. Integration enables a function to be triggered by that Azure Cosmos DB resource.

## Testing considerations

When testing functions in a function app with private endpoints, you must do your testing from within the same virtual network, such as on a virtual machine (VM) in that network. To use the **Code + Test** option in the portal from that VM, you need to add following [CORS origins](functions-how-to-use-azure-function-app-settings?tabs=portal#cors) to your function app:

`https://functions-next.azure.com`

`https://functions-staging.azure.com`

`https://functions.azure.com`

`https://portal.azure.com`


When you restrict access to your function app with private endpoints or any other access restriction, you also must add the service tag `AzureCloud`

to the allowed list. To update the allowed list:

Navigate to your function app and select

**Settings**>**Networking**and then select**Inbound access configuration**>**Public network access**.Make sure that

**Public network access**is set to**Enabled from select virtual networks and IP addresses**.**Add a rule**under Site access and rules:Select

`Service Tag`

as the Source settings**Type**and`AzureCloud`

as the**Service Tag**.Make sure the action is

**Allow**, and set your desired name and priority.


## Troubleshooting

The feature is easy to set up, but that doesn't mean your experience will be problem free. If you encounter problems accessing your desired endpoint, there are some utilities you can use to test connectivity from the app console. There are two consoles that you can use. One is the Kudu console, and the other is the console in the Azure portal. To reach the Kudu console from your app, go to **Tools** > **Kudu**. You can also reach the Kudo console at [sitename].scm.azurewebsites.net. After the website loads, go to the **Debug console** tab. To get to the Azure portal-hosted console from your app, go to **Tools** > **Console**.

#### Tools

In native Windows apps, the tools **ping**, **nslookup**, and **tracert** won't work through the console because of security constraints (they work in [custom Windows containers](../app-service/quickstart-custom-container)). To fill the void, two separate tools are added. To test DNS functionality, we added a tool named **nameresolver.exe**. The syntax is:

```
nameresolver.exe hostname [optional: DNS Server]
```


You can use nameresolver to check the hostnames that your app depends on. This way you can test if you have anything misconfigured with your DNS or perhaps don't have access to your DNS server. You can see the DNS server that your app uses in the console by looking at the environmental variables WEBSITE_DNS_SERVER and WEBSITE_DNS_ALT_SERVER.

Note

The nameresolver.exe tool currently doesn't work in custom Windows containers.

You can use the next tool to test for TCP connectivity to a host and port combination. This tool is called **tcpping** and the syntax is:

```
tcpping.exe hostname [optional: port]
```


The **tcpping** utility tells you if you can reach a specific host and port. It can show success only if there's an application listening at the host and port combination, and there's network access from your app to the specified host and port.

#### Debug access to virtual network-hosted resources

A number of things can prevent your app from reaching a specific host and port. Most of the time it's one of these things:

**A firewall is in the way.**If you have a firewall in the way, you hit the TCP timeout. The TCP timeout is 21 seconds in this case. Use the**tcpping**tool to test connectivity. TCP timeouts can be caused by many things beyond firewalls, but start there.**DNS isn't accessible.**The DNS timeout is 3 seconds per DNS server. If you have two DNS servers, the timeout is 6 seconds. Use nameresolver to see if DNS is working. You can't use nslookup, because that doesn't use the DNS your virtual network is configured with. If inaccessible, you could have a firewall or NSG blocking access to DNS or it could be down.

If those items don't answer your problems, look first for things like:

**Regional virtual network integration**

- Is your destination a non-RFC1918 address and you don't have
**Route All**enabled? - Is there an NSG blocking egress from your integration subnet?
- If you're going across Azure ExpressRoute or a VPN, is your on-premises gateway configured to route traffic back up to Azure? If you can reach endpoints in your virtual network but not on-premises, check your routes.
- Do you have enough permissions to set delegation on the integration subnet? During regional virtual network integration configuration, your integration subnet is delegated to Microsoft.Web/serverFarms. The VNet integration UI delegates the subnet to Microsoft.Web/serverFarms automatically. If your account doesn't have sufficient networking permissions to set delegation, you'll need someone who can set attributes on your integration subnet to delegate the subnet. To manually delegate the integration subnet, go to the Azure Virtual Network subnet UI and set the delegation for Microsoft.Web/serverFarms.

**Gateway-required virtual network integration**

- Is the point-to-site address range in the RFC 1918 ranges (10.0.0.0-10.255.255.255 / 172.16.0.0-172.31.255.255 / 192.168.0.0-192.168.255.255)?
- Does the gateway show as being up in the portal? If your gateway is down, then bring it back up.
- Do certificates show as being in sync, or do you suspect that the network configuration was changed? If your certificates are out of sync or you suspect that a change was made to your virtual network configuration that wasn't synced with your ASPs, select
**Sync Network**. - If you're going across a VPN, is the on-premises gateway configured to route traffic back up to Azure? If you can reach endpoints in your virtual network but not on-premises, check your routes.
- Are you trying to use a coexistence gateway that supports both point to site and ExpressRoute? Coexistence gateways aren't supported with virtual network integration.

Debugging networking issues is a challenge because you can't see what's blocking access to a specific host:port combination. Some causes include:

- You have a firewall up on your host that prevents access to the application port from your point-to-site IP range. Crossing subnets often requires public access.
- Your target host is down.
- Your application is down.
- You had the wrong IP or hostname.
- Your application is listening on a different port than what you expected. You can match your process ID with the listening port by using "netstat -aon" on the endpoint host.
- Your network security groups are configured in such a manner that they prevent access to your application host and port from your point-to-site IP range.

You don't know what address your app actually uses. It could be any address in the integration subnet or point-to-site address range, so you need to allow access from the entire address range.

More debug steps include:

- Connect to a VM in your virtual network and attempt to reach your resource host:port from there. To test for TCP access, use the PowerShell command
**Test-NetConnection**. The syntax is:

```
Test-NetConnection hostname [optional: -Port]
```


- Bring up an application on a VM and test access to that host and port from the console from your app by using
**tcpping**.

#### On-premises resources

If your app can't reach a resource on-premises, check if you can reach the resource from your virtual network. Use the **Test-NetConnection** PowerShell command to check for TCP access. If your VM can't reach your on-premises resource, your VPN or ExpressRoute connection might not be configured properly.

If your virtual network-hosted VM can reach your on-premises system but your app can't, the cause is likely one of the following reasons:

- Your routes aren't configured with your subnet or point-to-site address ranges in your on-premises gateway.
- Your network security groups are blocking access for your point-to-site IP range.
- Your on-premises firewalls are blocking traffic from your point-to-site IP range.
- You're trying to reach a non-RFC 1918 address by using the regional virtual network integration feature.

#### Deleting the App Service plan or web app before disconnecting the VNet integration

If you deleted the web app or the App Service plan without disconnecting the VNet integration first, you will not be able to do any update/delete operations on the virtual network or subnet that was used for the integration with the deleted resource. A subnet delegation 'Microsoft.Web/serverFarms' will remain assigned to your subnet and will prevent the update/delete operations.

In order to do update/delete the subnet or virtual network again you need to re-create the VNet integration and then disconnect it:

- Re-create the App Service plan and web app (it is mandatory to use the exact same web app name as before).
- Navigate to the 'Networking' blade on the web app and configure the VNet integration.
- After the VNet integration is configured, select the 'Disconnect' button.
- Delete the App Service plan or web app.
- Update/Delete the subnet or virtual network.

If you still encounter issues with the VNet integration after following the steps above, please contact Microsoft Support.

### Network troubleshooter

You can also use the Network troubleshooter to resolve connection issues. To open the network troubleshooter, go to the app in the Azure portal. Select **Diagnostic and solve problem**, and then search for **Network troubleshooter**.

**Connection issues** - It checks the status of the virtual network integration, including checking if the Private IP has been assigned to all instances of the plan and the DNS settings. If a custom DNS isn't configured, default Azure DNS is applied. The troubleshooter also checks for common Function app dependencies including connectivity for Azure Storage and other binding dependencies.


**Configuration issues** - This troubleshooter checks if your subnet is valid for virtual network integration.


**Subnet/VNet deletion issue** - This troubleshooter checks if your subnet has any locks and if it has any unused Service Association Links that might be blocking the deletion of the VNet/subnet.

## Next steps

To learn more about networking and Azure Functions:

[Follow the tutorial about getting started with virtual network integration](functions-create-vnet)[Read the Functions networking FAQ](functions-networking-faq)[Learn more about virtual network integration with App Service/Functions](../app-service/overview-vnet-integration)[Learn more about virtual networks in Azure](../virtual-network/virtual-networks-overview)[Enable more networking features and control with App Service Environments](../app-service/environment/intro)[Connect to individual on-premises resources without firewall changes by using Hybrid Connections](../app-service/app-service-hybrid-connections)
