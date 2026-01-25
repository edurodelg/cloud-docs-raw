---
merged_at: 2026-01-25T15:41:11.658171
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-host-json___configure-encrypt-at-rest-using-cmk_self-hosted-mcp-serve_15bc64.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-host-json.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-host-json -->

# host.json reference for Azure Functions 2.x and later

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The host.json metadata file contains configuration options that affect all functions in a function app instance. This article lists the settings that are available starting with version 2.x of the Azure Functions runtime.

Note

This article is for Azure Functions 2.x and later versions. For a reference of host.json in Functions 1.x, see [host.json reference for Azure Functions 1.x](functions-host-json-v1).

Other function app configuration options are managed depending on where the function app runs:

**Deployed to Azure**: in your[application settings](functions-app-settings)**On your local computer**: in the[local.settings.json](functions-develop-local#local-settings-file)file.

Configurations in host.json related to bindings are applied equally to each function in the function app.

You can also [override or apply settings per environment](#override-hostjson-values) using application settings.

## Sample host.json file

The following sample *host.json* file for version 2.x+ has all possible options specified (excluding any that are for internal use only).

```
{
"version": "2.0",
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
},
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
},
"extensions": {
"blobs": {},
"cosmosDb": {},
"durableTask": {},
"eventHubs": {},
"http": {},
"queues": {},
"sendGrid": {},
"serviceBus": {}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
},
"functions": [ "QueueProcessor", "GitHubWebHook" ],
"functionTimeout": "00:05:00",
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
},
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"Function.MyFunction": "Information",
"default": "None"
},
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"maxTelemetryItemsPerSecond" : 20,
"evaluationInterval": "01:00:00",
"initialSamplingPercentage": 100.0,
"samplingPercentageIncreaseTimeout" : "00:00:01",
"samplingPercentageDecreaseTimeout" : "00:00:01",
"minSamplingPercentage": 0.1,
"maxSamplingPercentage": 100.0,
"movingAverageRatio": 1.0,
"excludedTypes" : "Dependency;Event",
"includedTypes" : "PageView;Trace"
},
"dependencyTrackingOptions": {
"enableSqlCommandTextInstrumentation": true
},
"enableLiveMetrics": true,
"enableDependencyTracking": true,
"enablePerformanceCountersCollection": true,
"httpAutoCollectionOptions": {
"enableHttpTriggerExtendedInfoCollection": true,
"enableW3CDistributedTracing": true,
"enableResponseHeaderInjection": true
},
"snapshotConfiguration": {
"agentEndpoint": null,
"captureSnapshotMemoryWeight": 0.5,
"failedRequestLimit": 3,
"handleUntrackedExceptions": true,
"isEnabled": true,
"isEnabledInDeveloperMode": false,
"isEnabledWhenProfiling": true,
"isExceptionSnappointsEnabled": false,
"isLowPrioritySnapshotUploader": true,
"maximumCollectionPlanSize": 50,
"maximumSnapshotsRequired": 3,
"problemCounterResetInterval": "24:00:00",
"provideAnonymousTelemetry": true,
"reconnectInterval": "00:15:00",
"shadowCopyFolder": null,
"shareUploaderProcess": true,
"snapshotInLowPriorityThread": true,
"snapshotsPerDayLimit": 30,
"snapshotsPerTenMinutesLimit": 1,
"tempFolder": null,
"thresholdForSnapshotting": 1,
"uploaderProxy": null
}
}
},
"managedDependency": {
"enabled": true
},
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
},
"telemetryMode": "OpenTelemetry",
"watchDirectories": [ "Shared", "Test" ],
"watchFiles": [ "myFile.txt" ]
}
```


The following sections of this article explain each top-level property. All are optional unless otherwise indicated.

## aggregator

Specifies how many function invocations are aggregated when [calculating metrics for Application Insights](configure-monitoring#configure-the-aggregator).

```
{
"aggregator": {
"batchSize": 1000,
"flushTimeout": "00:00:30"
}
}
```


| Property | Default | Description |
|---|---|---|
| batchSize | 1000 | Maximum number of requests to aggregate. |
| flushTimeout | 00:00:30 | Maximum time period to aggregate. |

Function invocations are aggregated when the first of the two limits are reached.

## applicationInsights

This setting is a child of [logging](#logging).

Controls options for Application Insights, including [sampling options](configure-monitoring#configure-sampling).

For the complete JSON structure, see the earlier [example host.json file](#sample-hostjson-file).

Note

Log sampling may cause some executions to not show up in the Application Insights monitor blade. To avoid log sampling, add `excludedTypes: "Request"`

to the `samplingSettings`

value.

| Property | Default | Description |
|---|---|---|
| samplingSettings | n/a | See
|

[applicationInsights.dependencyTrackingOptions](#applicationinsightsdependencytrackingoptions).[applicationInsights.samplingSettings.excludedTypes](#applicationinsightssamplingsettings), For more information, see see[Select and filter your metrics](/en-us/azure/azure-monitor/app/live-stream#select-and-filter-your-metrics).[applicationInsights.httpAutoCollectionOptions](#applicationinsightshttpautocollectionoptions).[applicationInsights.snapshotConfiguration](#applicationinsightssnapshotconfiguration).### applicationInsights.samplingSettings

For more information about these settings, see [Sampling in Application Insights](/en-us/azure/azure-monitor/app/sampling).

| Property | Default | Description |
|---|---|---|
| isEnabled | true | Enables or disables sampling. |
| maxTelemetryItemsPerSecond | 20 | The target number of telemetry items logged per second on each server host. If your app runs on many hosts, reduce this value to remain within your overall target rate of traffic. |
| evaluationInterval | 01:00:00 | The interval at which the current rate of telemetry is reevaluated. Evaluation is performed as a moving average. You might want to shorten this interval if your telemetry is liable to sudden bursts. |
| initialSamplingPercentage | 100.0 | The initial sampling percentage applied at the start of the sampling process to dynamically vary the percentage. Don't reduce value while you're debugging. |
| samplingPercentageIncreaseTimeout | 00:00:01 | When the sampling percentage value changes, this property determines how soon afterwards Application Insights is allowed to raise sampling percentage again to capture more data. |
| samplingPercentageDecreaseTimeout | 00:00:01 | When the sampling percentage value changes, this property determines how soon afterwards Application Insights is allowed to lower sampling percentage again to capture less data. |
| minSamplingPercentage | 0.1 | As sampling percentage varies, this property determines the minimum allowed sampling percentage. |
| maxSamplingPercentage | 100.0 | As sampling percentage varies, this property determines the maximum allowed sampling percentage. |
| movingAverageRatio | 1.0 | In the calculation of the moving average, the weight assigned to the most recent value. Use a value equal to or less than 1. Smaller values make the algorithm less reactive to sudden changes. |
| excludedTypes | null | A semi-colon delimited list of types that you don't want to be sampled. Recognized types are: `Dependency` , `Event` , `Exception` , `PageView` , `Request` , and `Trace` . All instances of the specified types are transmitted; the types that aren't specified are sampled. |
| includedTypes | null | A semi-colon delimited list of types that you want to be sampled; an empty list implies all types. Type listed in `excludedTypes` override types listed here. Recognized types are: `Dependency` , `Event` , `Exception` , `PageView` , `Request` , and `Trace` . Instances of the specified types are sampled; the types that aren't specified or implied are transmitted without sampling. |

### applicationInsights.httpAutoCollectionOptions

| Property | Default | Description |
|---|---|---|
| enableHttpTriggerExtendedInfoCollection | true | Enables or disables extended HTTP request information for HTTP triggers: incoming request correlation headers, multi-instrumentation keys support, HTTP method, path, and response. |
| enableW3CDistributedTracing | true | Enables or disables support of W3C distributed tracing protocol (and turns on legacy correlation schema). Enabled by default if `enableHttpTriggerExtendedInfoCollection` is true. If `enableHttpTriggerExtendedInfoCollection` is false, this flag applies to outgoing requests only, not incoming requests. |
| enableResponseHeaderInjection | true | Enables or disables injection of multi-component correlation headers into responses. Enabling injection allows Application Insights to construct an Application Map to when several instrumentation keys are used. Enabled by default if `enableHttpTriggerExtendedInfoCollection` is true. This setting doesn't apply if `enableHttpTriggerExtendedInfoCollection` is false. |

### applicationInsights.dependencyTrackingOptions

| Property | Default | Description |
|---|---|---|
| enableSqlCommandTextInstrumentation | false | Enables collection of the full text of SQL queries, which is disabled by default. For more information on collecting SQL query text, see
|

### applicationInsights.snapshotConfiguration

For more information on snapshots, see [Debug snapshots on exceptions in .NET apps](/en-us/azure/azure-monitor/app/snapshot-debugger) and [Troubleshoot problems enabling Application Insights Snapshot Debugger or viewing snapshots](/en-us/troubleshoot/azure/azure-monitor/app-insights/snapshot-debugger-troubleshoot).

| Property | Default | Description |
|---|---|---|
| agentEndpoint | null | The endpoint used to connect to the Application Insights Snapshot Debugger service. If null, a default endpoint is used. |
| captureSnapshotMemoryWeight | 0.5 | The weight given to the current process memory size when checking if there's enough memory to take a snapshot. The expected value is a greater than 0 proper fraction (0 < CaptureSnapshotMemoryWeight < 1). |
| failedRequestLimit | 3 | The limit on the number of failed requests to request snapshots before the telemetry processor is disabled. |
| handleUntrackedExceptions | true | Enables or disables tracking of exceptions that aren't tracked by Application Insights telemetry. |
| isEnabled | true | Enables or disables snapshot collection |
| isEnabledInDeveloperMode | false | Enables or disables snapshot collection is enabled in developer mode. |
| isEnabledWhenProfiling | true | Enables or disables snapshot creation even if the Application Insights Profiler is collecting a detailed profiling session. |
| isExceptionSnappointsEnabled | false | Enables or disables filtering of exceptions. |
| isLowPrioritySnapshotUploader | true | Determines whether to run the SnapshotUploader process at below normal priority. |
| maximumCollectionPlanSize | 50 | The maximum number of problems that we can track at any time in a range from one to 9999. |
| maximumSnapshotsRequired | 3 | The maximum number of snapshots collected for a single problem, in a range from one to 999. A problem may be thought of as an individual throw statement in your application. Once the number of snapshots collected for a problem reaches this value, no more snapshots will be collected for that problem until problem counters are reset (see `problemCounterResetInterval` ) and the `thresholdForSnapshotting` limit is reached again. |
| problemCounterResetInterval | 24:00:00 | How often to reset the problem counters in a range from one minute to seven days. When this interval is reached, all problem counts are reset to zero. Existing problems that have already reached the threshold for doing snapshots, but haven't yet generated the number of snapshots in `maximumSnapshotsRequired` , remain active. |
| provideAnonymousTelemetry | true | Determines whether to send anonymous usage and error telemetry to Microsoft. This telemetry may be used if you contact Microsoft to help troubleshoot problems with the Snapshot Debugger. It's also used to monitor usage patterns. |
| reconnectInterval | 00:15:00 | How often we reconnect to the Snapshot Debugger endpoint. Allowable range is one minute to one day. |
| shadowCopyFolder | null | Specifies the folder to use for shadow copying binaries. If not set, the folders specified by the following environment variables are tried in order: Fabric_Folder_App_Temp, LOCALAPPDATA, APPDATA, TEMP. |
| shareUploaderProcess | true | If true, only one instance of SnapshotUploader will collect and upload snapshots for multiple apps that share the InstrumentationKey. If set to false, the SnapshotUploader will be unique for each (ProcessName, InstrumentationKey) tuple. |
| snapshotInLowPriorityThread | true | Determines whether or not to process snapshots in a low IO priority thread. Creating a snapshot is a fast operation but, in order to upload a snapshot to the Snapshot Debugger service, it must first be written to disk as a minidump. That happens in the SnapshotUploader process. Setting this value to true uses low-priority IO to write the minidump, which won't compete with your application for resources. Setting this value to false speeds up minidump creation at the expense of slowing down your application. |
| snapshotsPerDayLimit | 30 | The maximum number of snapshots allowed in one day (24 hours). This limit is also enforced on the Application Insights service side. Uploads are rate limited to 50 per day per application (that is, per instrumentation key). This value helps prevent creating additional snapshots that will eventually be rejected during upload. A value of zero removes the limit entirely, which isn't recommended. |
| snapshotsPerTenMinutesLimit | 1 | The maximum number of snapshots allowed in 10 minutes. Although there's no upper bound on this value, exercise caution increasing it on production workloads because it could impact the performance of your application. Creating a snapshot is fast, but creating a minidump of the snapshot and uploading it to the Snapshot Debugger service is a much slower operation that will compete with your application for resources (both CPU and I/O). |
| tempFolder | null | Specifies the folder to write minidumps and uploader log files. If not set, then %TEMP%\Dumps is used. |
| thresholdForSnapshotting | 1 | How many times Application Insights needs to see an exception before it asks for snapshots. |
| uploaderProxy | null | Overrides the proxy server used in the Snapshot Uploader process. You may need to use this setting if your application connects to the internet via a proxy server. The Snapshot Collector runs within your application's process and will use the same proxy settings. However, the Snapshot Uploader runs as a separate process and you may need to configure the proxy server manually. If this value is null, then Snapshot Collector will attempt to autodetect the proxy's address by examining `System.Net.WebRequest.DefaultWebProxy` and passing on the value to the Snapshot Uploader. If this value isn't null, then autodetection isn't used and the proxy server specified here will be used in the Snapshot Uploader. |

## blobs

Configuration settings can be found in [Storage blob triggers and bindings](functions-bindings-storage-blob#hostjson-settings).

## console

This setting is a child of [logging](#logging). It controls the console logging when not in debugging mode.

```
{
"logging": {
...
"console": {
"isEnabled": false,
"DisableColors": true
},
...
}
}
```


| Property | Default | Description |
|---|---|---|
| DisableColors | false | Suppresses log formatting in the container logs on Linux. Set to true if you're seeing unwanted ANSI control characters in the container logs when running on Linux. |
| isEnabled | false | Enables or disables console logging. |

## Azure Cosmos DB

Configuration settings can be found in [Azure Cosmos DB triggers and bindings](functions-bindings-cosmosdb-v2#hostjson-settings).

## customHandler

Configuration settings for a custom handler. For more information, see [Azure Functions custom handlers](functions-custom-handlers#configuration).

```
"customHandler": {
"description": {
"defaultExecutablePath": "server",
"workingDirectory": "handler",
"arguments": [ "--port", "%FUNCTIONS_CUSTOMHANDLER_PORT%" ]
},
"enableForwardingHttpRequest": false
}
```


| Property | Default | Description |
|---|---|---|
| defaultExecutablePath | n/a | The executable to start as the custom handler process. It's a required setting when using custom handlers and its value is relative to the function app root. |
| workingDirectory | function app root |
The working directory in which to start the custom handler process. It's an optional setting and its value is relative to the function app root. |
| arguments | n/a | An array of command line arguments to pass to the custom handler process. |
| enableForwardingHttpRequest | false | If set, all functions that consist of only an HTTP trigger and HTTP output is forwarded the original HTTP request instead of the custom handler
|

## durableTask

Configuration setting can be found in [bindings for Durable Functions](durable/durable-functions-bindings#host-json).

## concurrency

Enables dynamic concurrency for specific bindings in your function app. For more information, see [Dynamic concurrency](functions-concurrency#dynamic-concurrency).

```
{
"concurrency": {
"dynamicConcurrencyEnabled": true,
"snapshotPersistenceEnabled": true
}
}
```


| Property | Default | Description |
|---|---|---|
| dynamicConcurrencyEnabled | false | Enables dynamic concurrency behaviors for all triggers supported by this feature, which is off by default. |
| snapshotPersistenceEnabled | true | Learned concurrency values are periodically persisted to storage so new instances start from those values instead of starting from 1 and having to redo the learning. |

## eventHub

Configuration settings can be found in [Event Hub triggers and bindings](functions-bindings-event-hubs#host-json).

## extensions

Property that returns an object that contains all of the binding-specific settings, such as [http](#http) and [eventHub](#eventhub).

## extensionBundle

Extension bundles let you add a compatible set of Functions binding extensions to your function app. To learn more, see [Extension bundles for local development](extension-bundles).

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

The following properties are available in `extensionBundle`

:

| Property | Description |
|---|---|
`id` |
The namespace for Azure Functions extension bundles. |
`version` |
The version range of the bundle to install. The Azure Functions runtime always chooses the maximum permissible version that the version range or interval defines. For example, a `version` value range of `[4.0.0, 5.0.0)` allows all bundle versions from 4.0.0 up to (but not including) 5.0.0. For more information, see the
|

Tip

You might also see the version range defined in your *host.json* as `[4.*, 5.0.0)`

, which is interpreted the same as `[4.0.0, 5.0.0)`

.

## functions

A list of functions that the job host runs. An empty array means run all functions. Intended for use only when [running locally](functions-run-local). In function apps in Azure, you should instead follow the steps in [How to disable functions in Azure Functions](disable-function) to disable specific functions rather than using this setting.

```
{
"functions": [ "QueueProcessor", "GitHubWebHook" ]
}
```


## functionTimeout

Indicates the timeout duration for all function executions. It follows the [timespan string format](/en-us/dotnet/fundamentals/runtime-libraries/system-timespan-parse). A value of `-1`

indicates unbounded execution, but keeping a fixed upper bound is recommended.

```
{
"functionTimeout": "00:05:00"
}
```


The format of the timespan string needs to follow the syntax `[d.]hh:mm:ss`

and the valid values are:

- d = days (optional)
- hh = hours (0–23)
- mm = minutes (0–59)
- ss = seconds (0–59)

Tip

When you need to set a 24-hour timeout, you must define it as one day (`"1.00:00:00"`

) instead of 24 hours (`"24:00:00"`

). You might also use `"23:59:59"`

.

For more information on the default and maximum values for specific plans, see [Function app timeout duration](functions-scale#timeout).

## healthMonitor

Configuration settings for [Host health monitor](https://github.com/Azure/azure-webjobs-sdk-script/wiki/Host-Health-Monitor).

```
{
"healthMonitor": {
"enabled": true,
"healthCheckInterval": "00:00:10",
"healthCheckWindow": "00:02:00",
"healthCheckThreshold": 6,
"counterThreshold": 0.80
}
}
```


| Property | Default | Description |
|---|---|---|
| enabled | true | Specifies whether the feature is enabled. |
| healthCheckInterval | 10 seconds | The time interval between the periodic background health checks. |
| healthCheckWindow | 2 minutes | A sliding time window used in conjunction with the `healthCheckThreshold` setting. |
| healthCheckThreshold | 6 | Maximum number of times the health check can fail before a host recycle is initiated. |
| counterThreshold | 0.80 | The threshold at which a performance counter will be considered unhealthy. |

## http

Configuration settings can be found in [http triggers and bindings](functions-bindings-http-webhook#hostjson-settings).

## logging

Controls the logging behaviors of the function app, including Application Insights.

```
"logging": {
"fileLoggingMode": "debugOnly",
"logLevel": {
"Function.MyFunction": "Information",
"default": "None"
},
"console": {
...
},
"applicationInsights": {
...
}
}
```


| Property | Default | Description |
|---|---|---|
| fileLoggingMode | debugOnly | Determines the file logging behavior when running in Azure. Options are `never` , `always` , and `debugOnly` . This setting isn't used when running locally. When possible, you should use Application Insights when debugging your functions in Azure. Using `always` negatively impacts your app's cold start behavior and data throughput. The default `debugOnly` setting generates log files when you're debugging using the Azure portal. |
| logLevel | n/a | Object that defines the log category filtering for functions in the app. This setting lets you filter logging for specific functions. For more information, see
|

[console](#console)logging setting.[applicationInsights](#applicationinsights)setting.## managedDependency

Managed dependency is a feature that is currently only supported with PowerShell based functions. It enables dependencies to be automatically managed by the service. When the `enabled`

property is set to `true`

, the `requirements.psd1`

file is processed. Dependencies are updated when any minor versions are released. For more information, see [Managed dependency](functions-reference-powershell#dependency-management) in the PowerShell article.

```
{
"managedDependency": {
"enabled": true
}
}
```


## queues

Configuration settings can be found in [Storage queue triggers and bindings](functions-bindings-storage-queue#host-json).

## sendGrid

Configuration setting can be found in [SendGrid triggers and bindings](functions-bindings-sendgrid#host-json).

## serviceBus

Configuration setting can be found in [Service Bus triggers and bindings](functions-bindings-service-bus).

## singleton

Configuration settings for Singleton lock behavior. For more information, see [GitHub issue about singleton support](https://github.com/Azure/azure-webjobs-sdk-script/issues/912).

```
{
"singleton": {
"lockPeriod": "00:00:15",
"listenerLockPeriod": "00:01:00",
"listenerLockRecoveryPollingInterval": "00:01:00",
"lockAcquisitionTimeout": "00:01:00",
"lockAcquisitionPollingInterval": "00:00:03"
}
}
```


| Property | Default | Description |
|---|---|---|
| lockPeriod | 00:00:15 | The period that function level locks are taken for. The locks auto-renew. |
| listenerLockPeriod | 00:01:00 | The period that listener locks are taken for. |
| listenerLockRecoveryPollingInterval | 00:01:00 | The time interval used for listener lock recovery if a listener lock couldn't be acquired on startup. |
| lockAcquisitionTimeout | 00:01:00 | The maximum amount of time the runtime will try to acquire a lock. |
| lockAcquisitionPollingInterval | n/a | The interval between lock acquisition attempts. |

## telemetryMode

*This feature is currently in preview.*

Used to enable output of logs and traces in an OpenTelemetry output format to one or more endpoints that support OpenTelemetry. When this setting is set to `OpenTelemetry`

, OpenTelemetry output is used. By default without this setting, all logs, traces, and events are sent to Application Insights using the standard outputs. For more information, see [Use OpenTelemetry with Azure Functions](opentelemetry-howto).

## version

This value indicates the schema version of host.json. The version string `"version": "2.0"`

is required for a function app that targets the v2 runtime, or a later version. There are no host.json schema changes between v2 and v3.

## watchDirectories

A set of [shared code directories](functions-reference-csharp#watched-directories) that should be monitored for changes. Ensures that when code in these directories is changed, the changes are picked up by your functions.

```
{
"watchDirectories": [ "Shared" ]
}
```


## watchFiles

An array of one or more names of files that are monitored for changes that require your app to restart. This guarantees that when code in these files is changed, the updates are picked up by your functions.

```
{
"watchFiles": [ "myFile.txt" ]
}
```


## Override host.json values

There may be instances where you wish to configure or modify specific settings in a host.json file for a specific environment, without changing the host.json file itself. You can override specific host.json values by creating an equivalent value as an application setting. When the runtime finds an application setting in the format `AzureFunctionsJobHost__path__to__setting`

, it overrides the equivalent host.json setting located at `path.to.setting`

in the JSON. When expressed as an application setting, the dot (`.`

) used to indicate JSON hierarchy is replaced by a double underscore (`__`

).

For example, say that you wanted to disable Application Insight sampling when running locally. If you changed the local host.json file to disable Application Insights, this change might get pushed to your production app during deployment. The safer way to do this is to instead create an application setting as `"AzureFunctionsJobHost__logging__applicationInsights__samplingSettings__isEnabled":"false"`

in the `local.settings.json`

file. You can see this in the following `local.settings.json`

file, which doesn't get published:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "{storage-account-connection-string}",
"FUNCTIONS_WORKER_RUNTIME": "{language-runtime}",
"AzureFunctionsJobHost__logging__applicationInsights__samplingSettings__isEnabled":"false"
}
}
```


Overriding host.json settings using environment variables follows the ASP.NET Core naming conventions. When the element structure includes an array, the numeric array index should be treated as an additional element name in this path. For more information, see [Naming of environment variables](/en-us/aspnet/core/fundamentals/configuration/#naming-of-environment-variables).


---

<!-- DOCUMENTO FUSIONADO: __configure-encrypt-at-rest-using-cmk_self-hosted-mcp-servers_scenario-database-_b75e88.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _configure-encrypt-at-rest-using-cmk_self-hosted-mcp-servers.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: configure-encrypt-at-rest-using-cmk.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/configure-encrypt-at-rest-using-cmk -->

# Encrypt your application data at rest using customer-managed keys

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Encrypting your function app's application data at rest requires an Azure Storage Account and an Azure Key Vault. These services are used when you run your app from a deployment package.

[Azure Storage provides encryption at rest](../storage/common/storage-service-encryption). You can use system-provided keys or your own, customer-managed keys. This is where your application data is stored when it's not running in a function app in Azure.[Running from a deployment package](run-functions-from-deployment-package)is a deployment feature of App Service. It allows you to deploy your site content from an Azure Storage Account using a Shared Access Signature (SAS) URL.[Key Vault references](../app-service/app-service-key-vault-references)are a security feature of App Service. It allows you to import secrets at runtime as application settings. Use this to encrypt the SAS URL of your Azure Storage Account.

## Set up encryption at rest

### Create an Azure Storage account

First, [create an Azure Storage account](../storage/common/storage-account-create) and [encrypt it with customer managed keys](../storage/common/customer-managed-keys-overview). Once the storage account is created, use the [Azure Storage Explorer](../vs-azure-tools-storage-manage-with-storage-explorer) to upload package files.

Next, use the Storage Explorer to [generate an SAS](../vs-azure-tools-storage-manage-with-storage-explorer?tabs=windows#generate-a-sas-in-storage-explorer).

Note

Save this SAS URL, this is used later to enable secure access of the deployment package at runtime.

### Configure running from a package from your storage account

Once you upload your file to Blob storage and have an SAS URL for the file, set the `WEBSITE_RUN_FROM_PACKAGE`

application setting to the SAS URL. The following example does it by using Azure CLI:

```
az webapp config appsettings set --name <app-name> --resource-group <resource-group-name> --settings WEBSITE_RUN_FROM_PACKAGE="<your-SAS-URL>"
```


Adding this application setting causes your function app to restart. After the app has restarted, browse to it and make sure that the app has started correctly using the deployment package. If the application didn't start correctly, see the [Run from package troubleshooting guide](run-functions-from-deployment-package#troubleshooting).

### Encrypt the application setting using Key Vault references

Now you can replace the value of the `WEBSITE_RUN_FROM_PACKAGE`

application setting with a Key Vault reference to the SAS-encoded URL. This keeps the SAS URL encrypted in Key Vault, which provides an extra layer of security.

Use the following

command to create a Key Vault instance.`az keyvault create`

`az keyvault create --name "Contoso-Vault" --resource-group <group-name> --location eastus`

Follow

[these instructions to grant your app access](../app-service/app-service-key-vault-references#grant-your-app-access-to-a-key-vault)to your key vault:Use the following

command to add your external URL as a secret in your key vault:`az keyvault secret set`

`az keyvault secret set --vault-name "Contoso-Vault" --name "external-url" --value "<SAS-URL>"`

Use the following

command to create the`az webapp config appsettings set`

`WEBSITE_RUN_FROM_PACKAGE`

application setting with the value as a Key Vault reference to the external URL:`az webapp config appsettings set --settings WEBSITE_RUN_FROM_PACKAGE="@Microsoft.KeyVault(SecretUri=https://Contoso-Vault.vault.azure.net/secrets/external-url/<secret-version>"`

The

`<secret-version>`

will be in the output of the previous`az keyvault secret set`

command.

Updating this application setting causes your function app to restart. After the app has restarted, browse to it make sure it has started correctly using the Key Vault reference.

## How to rotate the access token

It is best practice to periodically rotate the SAS key of your storage account. To ensure the function app does not inadvertently lose access, you must also update the SAS URL in Key Vault.

Rotate the SAS key by navigating to your storage account in the Azure portal. Under

**Settings**>**Access keys**, select the icon to rotate the SAS key.Copy the new SAS URL, and use the following command to set the updated SAS URL in your key vault:

`az keyvault secret set --vault-name "Contoso-Vault" --name "external-url" --value "<SAS-URL>"`

Update the key vault reference in your application setting to the new secret version:

`az webapp config appsettings set --settings WEBSITE_RUN_FROM_PACKAGE="@Microsoft.KeyVault(SecretUri=https://Contoso-Vault.vault.azure.net/secrets/external-url/<secret-version>"`

The

`<secret-version>`

will be in the output of the previous`az keyvault secret set`

command.

## How to revoke the function app's data access

There are two methods to revoke the function app's access to the storage account.

### Rotate the SAS key for the Azure Storage account

If the SAS key for the storage account is rotated, the function app will no longer have access to the storage account, but it will continue to run with the last downloaded version of the package file. Restart the function app to clear the last downloaded version.

### Remove the function app's access to Key Vault

You can revoke the function app's access to the site data by disabling the function app's access to Key Vault. To do this, remove the access policy for the function app's identity. This is the same identity you created earlier while configuring key vault references.

## Summary

Your application files are now encrypted at rest in your storage account. When your function app starts, it retrieves the SAS URL from your key vault. Finally, the function app loads the application files from the storage account.

If you need to revoke the function app's access to your storage account, you can either revoke access to the key vault or rotate the storage account keys, both of which invalidate the SAS URL.

## Frequently Asked Questions

### Is there any additional charge for running my function app from the deployment package?

Only the cost associated with the Azure Storage Account and any applicable egress charges.

### How does running from the deployment package affect my function app?

- Running your app from the deployment package makes
`wwwroot/`

read-only. Your app receives an error when it attempts to write to this directory. - TAR and GZIP formats are not supported.
- This feature is not compatible with local cache.


---

<!-- DOCUMENTO FUSIONADO: self-hosted-mcp-servers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/self-hosted-mcp-servers -->

# Self-hosted remote MCP server on Azure Functions (public preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions provides two ways of hosting remote MCP servers:

- MCP servers created with the
[Functions MCP extension](functions-bindings-mcp) - MCP servers built with the
[official MCP SDKs](https://modelcontextprotocol.io/docs/sdk)

With the first approach, you can use the Azure Functions programming model with triggers and bindings to build the MCP server. Then, you can host the server remotely by deploying it to a Function app.

If you already have an MCP server created with the official MCP SDKs and just want to host it remotely, the second approach likely suits your needs. You don't need to make any code changes to the server to host it on Azure Functions. Instead, you can add the required Functions artifacts, and the server is ready to be deployed. As such, these servers are referred to as *self-hosted MCP servers*.


This article provides an overview of self-hosted MCP servers and links to relevant articles and samples.

## Custom handlers

Self-hosted MCP servers deploy to the Azure Functions platform as *custom handlers*. Custom handlers are lightweight web servers that receive events from the Functions host. They provide a way to run on the Functions platform applications built with frameworks different from the Functions programming model or in languages not supported out-of-the-box. For more information, see [Azure Functions custom handlers](functions-custom-handlers).

When you deploy an MCP SDK based server to Azure Functions, you must include a *host.json* in your project. The minimal *host.json* looks like this:

```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "python",
"arguments": ["Path to main script file, e.g. hello_world.py"]
},
"port": "<MCP server port>"
}
}
```


```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "npm",
"arguments": ["run", "start"]
},
"port": "<MCP server port>"
}
}
```


```
{
"version": "2.0",
"configurationProfile": "mcp-custom-handler",
"customHandler": {
"description": {
"defaultExecutablePath": "dotnet",
"arguments": ["Path to the compiled DLL, e.g. HelloWorld.dll"]
},
"port": "<MCP server port>"
}
}
```


Note

Because the payload deployed to Azure Functions is the content of the `bin/output`

directory, the path to the compiled DLL is relative to that directory, *not* to the project root.

Example not yet available.

Using a `configuration Profile`

value of `mcp-custom-handler`

automatically configures these Functions host settings, which are required for running your MCP server in Azure Functions:

`http.enableProxying`

to`true`

`http.routes`

to`[{ "route": "{*route}" }]`

`extensions.http.routePrefix`

to`""`


This example shows a host.json file with extra custom handler properties set equivalent to using the `mcp-custom-handler`

profile:

```
{
"version": "2.0",
"extensions": {
"http": {
"routePrefix": ""
}
},
"customHandler": {
"description": {
"defaultExecutablePath": "",
"arguments": [""]
},
"http": {
"enableProxying": true,
"defaultAuthorizationLevel": "anonymous",
"routes": [
{
"route": "{*route}",
// Default authorization level is `defaultAuthorizationLevel`
},
{
"route": "admin/{*route}",
"authorizationLevel": "admin"
}
]
}
}
}
```


This table explains the properties of `customHandler.http`

, along with default values:

| Property | What it does | Default value |
|---|---|---|
`enableProxying` |
Controls how the Azure Functions host handles HTTP requests to custom handlers. When `enableProxying` is set to `true` , the Functions host acts as a reverse proxy and forwards the entire HTTP request (including headers, body, query parameters) directly to the custom handler. This setting gives the custom handler full access to the original HTTP request details. When `enableProxying` is `false` , the Functions host processes the request first and transforms it into the Azure Functions request/response format before passing it to the custom handler. |
`false` |
`defaultAuthorizationLevel` |
Controls the authentication requirement for accessing custom handler endpoints. For example, `function` requires a function-specific API key to access. For more information, see
|
`function` |
`route` |
Specifies the URL path pattern that the custom handler responds to. `{*route}` matches any URL path (such as `/` , `/mcp` , `/api/tools` , or `/anything/nested/path` ) and forwards the request to the custom handler. |
`{*route}` |

## Built-in server authentication

OAuth-based authentication and authorization provided by the App Service platform implements the requirements of the [MCP authorization specification](https://modelcontextprotocol.io/specification/2025-06-18/basic/authorization), such as issuing 401 challenge and exposing the Protected Resource Metadata (PRM) document. When you enable built-in authentication, clients attempting to access the server are redirected to identity providers like Microsoft Entra ID for authentication before connecting.

For more information, see [Configure built-in server authorization (preview)](../app-service/configure-authentication-mcp) and [Hosting MCP servers on Azure Functions](functions-mcp-tutorial).

## Azure AI Foundry agent integrations

Agents in Azure AI Foundry can be [configured to use tools](functions-mcp-tutorial#configure-azure-ai-foundry-agent-to-use-your-tools) in MCP servers hosted in Azure Functions.

## Register your server in Azure API Center

When you register your MCP server in Azure API Center, you create a private organizational tool catalog. This approach is recommended for sharing MCP servers across your organization with consistent governance and discoverability. For more information, see [Register MCP servers hosted in Azure Functions in Azure API Center](register-mcp-server-api-center).

## Public preview support

The ability to host your own SDK-based MCP servers in Functions is currently in preview and supports these features:

**Stateless**servers that use the**streamable-http**transport. If you need your server to be stateful, consider using the Functions MCP extension.- Servers implemented with the Python, TypeScript, C#, or Java MCP SDKs.
- When running the project locally, you must use the Azure Functions Core Tools (
`func start`

command). You can't currently use`F5`

to start running with the debugger. - Servers must be hosted as
[Flex Consumption plan](flex-consumption-plan)apps.

## Samples

Not yet available.


---

<!-- DOCUMENTO FUSIONADO: scenario-database-changes-azure-sqldb.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-database-changes-azure-sqldb -->

# Quickstart: Respond to Azure SQL Database changes using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this Quickstart, you use Visual Studio Code to build an app that responds to changes in an Azure SQL Database table. After testing the code locally, you deploy it to a new serverless function app running in a Flex Consumption plan in Azure Functions.

The project source uses the Azure Developer CLI (azd) extension with Visual Studio Code to simplify initializing and verifying your project code locally, and deploying your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

Important

While responding to [changes in an Azure SQL database](functions-bindings-azure-mysql-trigger) is supported for all languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code. This extension requires[Azure Functions Core Tools](functions-run-local). When this tool isn't available locally, the extension tries to install it by using a package-based installer. You can also install or update the Core Tools package by running`Azure Functions: Install or Update Azure Functions Core Tools`

from the command palette. If you don't have npm or Homebrew installed on your local computer, you must instead[manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

- The
[Azure Developer CLI extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.azure-dev)for Visual Studio Code.

- The
[SQL Server (mssql) extension](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql)for Visual Studio Code.

## Initialize the project

You can use the `azd init`

command from the command palette to create a local Azure Functions code project from a template.

In Visual Studio Code, open a folder or workspace in which you want to create your project.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Initialize App (init)`

, and then choose**Select a template**.When prompted, search for and select

`Azure Functions with SQL Triggers and Bindings`

.When prompted, enter a unique environment name, such as

`sqldbchanges`

.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

This command pulls the project files from the [template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql) and initializes the project in the current folder or workspace. In `azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

Before you can run your app locally, you must create the resources in Azure.

## Create Azure resources

This project is configured to use the `azd provision`

command to create a function app in a Flex Consumption plan, along with other required Azure resources that follow current best practices.

In Visual Studio Code, press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Sign In with Azure Developer CLI`

, and then sign in using your Azure account.Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Provision Azure resources (provision)`

to create the required Azure resources.When prompted in the Terminal window, provide these required deployment parameters:

Prompt Description Select an Azure Subscription to use Select the subscription in which you want your resources to be created. *location*deployment parameterAzure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. *vnetEnabled*deployment parameterWhile the template supports creating resources inside a virtual network, to simplify deployment and testing, choose `False`

.

The `azd provision`

command uses your response to these prompts with the Bicep configuration files to create and configure these required Azure resources, following the latest best practices:

- Flex Consumption plan and function app
- Azure SQL Database (default name: ToDo)
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)

Post-provision hooks also generate the *local.settings.json* file, which is required to run locally. This file contains the settings required to connect to your database in Azure.

## Review the code (optional)

The sample defines two functions:

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`httptrigger-sql-output` |
|

`ToDo`

table.`ToDoTrigger`

[sql_trigger.cs](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql/blob/main/sql_trigger.cs)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [ToDoItem.cs](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-sql/blob/main/ToDoItem.cs).

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`http_trigger_sql_output` |
|

`ToDo`

table.`httptrigger-sql-output`

[sql_trigger_todo](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql/blob/main/function_app.py#L15C5-L15C21)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [todo_item.py](https://github.com/Azure-Samples/functions-quickstart-python-azd-sql/blob/main/todo_item.py).

| Function name | Code file | Trigger type | Description |
|---|---|---|---|
`httpTriggerSqlOutput` |
|

`ToDo`

table.`sqlTriggerToDo`

[sql_trigger.ts](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql/blob/main/src/functions/sql_trigger.ts)`ToDo`

table for row-level changes and returns an object that represents the changed row.The `ToDoItem`

type is defined in [ToDoItem.ts](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-sql/blob/main/src/models/ToDoItem.ts).

Both functions use the app-level `AZURE_SQL_CONNECTION_STRING_KEY_*`

environment variables that define an identity-based connection to the Azure SQL Database instance using Microsoft Entra ID authentication. These environment variables are created for you both in Azure (function app settings) and locally (local.settings.json) during the `azd provision`

operation.

## Connect to the SQL database

You can use the SQL Server (mssql) extension for Visual Studio Code to connect to the new database. This extension helps you make updates in the `ToDo`

table to run the SQL trigger function.

Press

`F1`and in the command palette search for and run the command`MS SQL: Add Connection`

.In the

**Connection dialog**, change**Input type**to**Browse Azure**and then set these remaining options:Option Choose Description **Server**Your SQL Server instance By default, all servers accessible to your Azure account are displayed. Use **Subscription**,**Resource group**, and**Location**to help filter the servers list.**Database**`ToDo`

The database created during the provisioning process. **Authentication type****Microsoft Entra ID**If you aren't already signed-in, select **Sign in**and sign in to your Azure account.**Tenant ID**The specific account tenant. If your account has more than one tenant, choose the correct tenant for your subscription. Select

**Connect**to connect to your database. The connection uses your local user account, which is granted admin permissions in the hosting server and mapped to`dbo`

in the database.In the

**SQL Server**view, locate and expand**Connections**and then your new server in SQL Server explorer. Expand**Tables**and verify that the`ToDo`

table exists. If it doesn't exist, you might need run`azd provision`

again and check for errors.

## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to your new function app in Azure.

Press

`F1`and in the command palette search for and run the command`Azurite: Start`

.To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar.The

**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel, and you can see the name of the function that's running locally.

With the app running, you can verify and debug both function triggers.

To verify the HTTP trigger function that writes to a SQL output binding:

Copy this JSON object, which you can also find in the

`test.http`

project file:`{ "id": "11111111-1111-1111-1111-111111111111", "order": 1, "title": "Test Todo Item", "url": "https://example.com", "completed": false }`

This data represents a row that you insert in your SQL database when you call the HTTP endpoint. The output binding translates the data object into an

`INSERT`

operation in the database.With the app running, in the

**Azure**view under**Workspace**expand**Local project**>**Functions**.Right-select your HTTP function (or

`Ctrl`+click on macOS), select**Execute function now**, paste the copied JSON data, and press`Enter`.The function handles the HTTP request and writes the item to the connected SQL database and returns the created object.

Back in the SQL Server explorer, right-select the

`ToDo`

table (or`Ctrl`+click on macOS), and choose**Select Top 1000**. When the query executes, it returns the inserted or updated row.Repeat Step 3 and resend the same data object with the same ID. This time, the output binding performs an

`UPDATE`

operation instead of an`INSERT`

and modifies the existing row in the database.

When you're done, type `Ctrl`+`C` in the terminal to stop the Core Tools process.

## Deploy to Azure

You can run the `azd deploy`

command from Visual Studio Code to deploy the project code to your already provisioned resources in Azure.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Deploy to Azure (deploy)`

.The

`azd deploy`

command packages and deploys your code to the deployment container. The app is then started and runs in the deployed package.After the command completes successfully, your app is running in Azure. Make a note of the

`Endpoint`

value, which is the URL of your function app running in Azure.

## Invoke the function on Azure

In Visual Studio Code, press

`F1`and in the command palette search for and run the command`Azure: Open in portal`

, select`Function app`

, and choose your new app. Sign in with your Azure account, if necessary.Select

**Log stream**in the left pane, which connects to the Application Insights logs for your app.Return to Visual Studio Code to run both the functions in Azure.


Press

`F1`to open the command palette, search for and run the command`Azure Functions: Execute Function Now...`

.Search for and select your remote function app from the list, then select the HTTP trigger function.

As before, paste your JSON object data in

**Enter payload body**and press`Enter`.`{ "id": "11111111-1111-1111-1111-111111111111", "order": 1, "title": "Test Todo Item", "url": "https://example.com", "completed": false }`

To perform an

`INSERT`

instead of an`UPDATE`

, replace the`id`

with a new GUID value.Return to the portal and view the execution output in the log window.


## Clean up resources

When you're done working with your function app and related resources, you can use this command to delete the function app and its related resources from Azure and avoid incurring any further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without a confirmation from you.

This command doesn't affect your local code project.


---

<!-- DOCUMENTO FUSIONADO: ___functions-bindings-warmup_functions-bindings-cache-trigger-redislist_function_7fe6b7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __functions-bindings-warmup_functions-bindings-cache-trigger-redislist_functions_cecfc5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-warmup_functions-bindings-cache-trigger-redislist.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-warmup.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-warmup -->

# Azure Functions warmup trigger

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to work with the warmup trigger in Azure Functions. A warmup trigger is invoked when an instance is added to scale a running function app. The warmup trigger lets you define a function that runs when a new instance of your function app is started. You can use a warmup trigger to preload custom dependencies so your functions are ready to start processing requests immediately. Some actions for a warmup trigger might include opening connections, loading dependencies, or running any other custom logic before your app begins receiving traffic.

The following considerations apply when using a warmup trigger:

- There can be only one warmup trigger function per function app, and it can't be invoked after the instance is already running.
- The name of the function that is the warmup trigger for your app should be
`warmup`

(case-insensitive). - The warmup trigger isn't available to apps running on the
[Consumption plan](consumption-plan). - The warmup trigger isn't supported on version 1.x of the Functions runtime.
- Support for the warmup trigger is provided by default in all development environments. You don't have to manually install the package or register the extension.
- The warmup trigger is only called during scale-out operations, not during restarts or other nonscaling startups. Make sure your logic can load all required dependencies without relying on the warmup trigger. Lazy loading is a good pattern to achieve this goal.
- Dependencies created by warmup trigger should be shared with other functions in your app. To learn more, see
[Static clients](manage-connections#static-clients). - If the
[built-in authentication](../app-service/overview-authentication-authorization)(also known as Easy Auth) is used,[HTTPS Only](../app-service/configure-ssl-bindings#enforce-https)should be enabled for the warmup trigger to get invoked.

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a [C# function](dotnet-isolated-process-guide) that runs on each new instance when added to your app.

```
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public static class Warmup
{
[Function(nameof(Warmup))]
public static void Run([WarmupTrigger] object warmupContext, FunctionContext context)
{
var logger = context.GetLogger(nameof(Warmup));
logger.LogInformation("Function App instance is now warm!");
}
}
}
```


The following example shows a warmup trigger that runs when each new instance is added to your app.

```
@FunctionName("Warmup")
public void warmup( @WarmupTrigger Object warmupContext, ExecutionContext context) {
context.getLogger().info("Function App instance is warm.");
}
```


The following example shows a [JavaScript function](functions-reference-node) with a warmup trigger that runs on each new instance when added to your app:

```
const { app } = require('@azure/functions');
app.warmup('warmupTrigger', {
handler: (warmupContext, context) => {
context.log('Function App instance is warm.');
},
});
```


The following example shows a [TypeScript function](functions-reference-node) with a warmup trigger that runs on each new instance when added to your app:

```
import { app, InvocationContext, WarmupContext } from '@azure/functions';
export async function warmupFunction(warmupContext: WarmupContext, context: InvocationContext): Promise<void> {
context.log('Function App instance is warm.');
}
app.warmup('warmup', {
handler: warmupFunction,
});
```


Here's the *function.json* file:

```
{
"bindings": [
{
"type": "warmupTrigger",
"direction": "in",
"name": "warmupContext"
}
]
}
```


PowerShell example code pending.

The following example shows a warmup trigger in a *function.json* file and a [Python function](functions-reference-python) that runs on each new instance when it'is added to your app.

Your function must be named `warmup`

(case-insensitive) and there can only be one warmup function per app.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.warm_up_trigger('warmup')
def warmup(warmup) -> None:
logging.info('Function App instance is warm')
```


For more information, see [Configuration](#configuration).

## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the `WarmupTrigger`

attribute to define the function. C# script instead uses a [function.json configuration file](#configuration).

Use the `WarmupTrigger`

attribute to define the function. This attribute has no parameters.

## Annotations

Warmup triggers don't require annotations. Just use a name of `warmup`

(case-insensitive) for the `FunctionName`

annotation.

## Configuration

## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Required - must be set to `warmupTrigger` . |
direction |
Required - must be set to `in` . |
name |
Required - the variable name used in function code. A `name` of `warmupContext` is recommended for the binding parameter. |

See the [Example section](#example) for complete examples.

## Usage

The following considerations apply to using a warmup function in C#:

- Your function must be named
`warmup`

(case-insensitive) using the`Function`

attribute. - A return value attribute isn't required.
- Use the
`Microsoft.Azure.Functions.Worker.Extensions.Warmup`

package - You can pass an object instance to the function.

Your function must be named `warmup`

(case-insensitive) using the `FunctionName`

annotation.

The function type in function.json must be set to `warmupTrigger`

.


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cache-trigger-redislist.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redislist -->

# RedisListTrigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The `RedisListTrigger`

pops new elements from a list and surfaces those entries to the function.

For more information about Azure Cache for Redis triggers and bindings, [Redis Extension for Azure Functions](https://github.com/Azure/azure-functions-redis-extension/tree/main).

## Scope of availability for functions triggers

| Trigger Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Lists | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

Redis triggers aren't currently supported for functions running on a [Consumption plan](consumption-plan) or a [Flex Consumption plan](flex-consumption-plan).

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

The following sample polls the key `listTest`

.:

```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisListTrigger
{
public class SimpleListTrigger
{
private readonly ILogger<SimpleListTrigger> logger;
public SimpleListTrigger(ILogger<SimpleListTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(SimpleListTrigger))]
public void Run(
[RedisListTrigger(Common.connectionStringSetting, "listTest")] string entry)
{
logger.LogInformation(entry);
}
}
}
```


The following sample polls the key `listTest`

at a localhost Redis instance at `redisLocalhost`

:

```
package com.function.RedisListTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SimpleListTrigger {
@FunctionName("SimpleListTrigger")
public void run(
@RedisListTrigger(
name = "req",
connection = "redisConnectionString",
key = "listTest",
pollingIntervalInMs = 1000,
maxBatchSize = 1)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample uses the same `index.js`

file, with binding data in the `function.json`

file.

Here's the `index.js`

file:

```
module.exports = async function (context, entry) {
context.log(entry);
}
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This sample uses the same `run.ps1`

file, with binding data in the `function.json`

file.

Here's the `run.ps1`

file:

```
param($entry, $TriggerMetadata)
Write-Host $entry
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


This sample uses the same `__init__.py`

file, with binding data in the `function.json`

file.

The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

Here's the `__init__.py`

file:

```
import logging
def main(entry: str):
logging.info(entry)
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisListTrigger",
"listPopFromBeginning": true,
"connection": "redisConnectionString",
"key": "listTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


## Attributes

| Parameter | Description | Required | Default |
|---|---|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Key`

`INameResolver`

.`PollingIntervalInMs`

`1000`

`MessagesPerWorker`

`100`

`Count`

`COUNT`

argument in [and](https://redis.io/commands/lpop/)`LPOP`

[.](https://redis.io/commands/rpop/)`RPOP`

`10`

`ListPopFromBeginning`

[, or to pop entries from the end using](https://redis.io/commands/lpop/)`LPOP`

[.](https://redis.io/commands/rpop/)`RPOP`

`true`

## Annotations

| Parameter | Description | Required | Default |
|---|---|---|---|
`name` |
"entry" | ||
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`listPopFromBeginning`

`true`

## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json Property | Description | Optional | Default |
|---|---|---|---|
`type` |
Name of the trigger. | No | |
`listPopFromBeginning` |
Whether to delete the stream entries after the function has run. Set to `true` . |
Yes | `true` |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`INameResolver`

.`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`name`

`direction`

`in`

.See the Example section for complete examples.

## Usage

The `RedisListTrigger`

pops new elements from a list and surfaces those entries to the function. The trigger polls Redis at a configurable fixed interval, and uses [ LPOP](https://redis.io/commands/lpop/) and

[to pop entries from the lists.](https://redis.io/commands/rpop/)

`RPOP`

| Type | Description |
|---|---|
`byte[]` |
The message from the channel. |
`string` |
The message from the channel. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel from a `string` into a custom type. |


---

<!-- DOCUMENTO FUSIONADO: functions-container-apps-hosting.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-container-apps-hosting -->

# Azure Container Apps hosting of Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

A new hosting method for running Azure Functions directly in Azure Container Apps is now available. See [Native Azure Functions Support in Azure Container Apps](https://techcommunity.microsoft.com/blog/appsonazureblog/announcing-native-azure-functions-support-in-azure-container-apps/4414039). This integration allows you to use the full features and capabilities of Azure Container Apps. You also benefit from the functions programming model and simplicity of autoscaling provided by Azure Functions.

We recommend this approach for most new workloads. For more information, see [Azure Functions on Azure Container Apps](../container-apps/functions-overview).

Azure Functions provides integrated support for developing, deploying, and managing containerized function apps on [Azure Container Apps](../container-apps/overview). Use Azure Container Apps to host your function app containers when you need to run your event-driven functions in Azure in the same environment as other microservices, APIs, websites, workflows, or any container hosted programs. Container Apps hosting lets you run your functions in a fully managed, Kubernetes-based environment with built-in support for open-source monitoring, mTLS, Dapr, and Kubernetes Event-driven Autoscaling (KEDA).

You can write your function code in any [language stack supported by Functions](supported-languages). You can use the same Functions triggers and bindings with event-driven scaling. You can also use existing Functions client tools and the Azure portal to create containers, deploy function app containers to Container Apps, and configure continuous deployment.

Container Apps integration also means that network and observability configurations, which are defined at the Container App environment level, apply to your function app as they do to all microservices running in a Container Apps environment. You also get the other cloud-native capabilities of Container Apps, including KEDA, Dapr, Envoy. You can still use Application Insights to monitor your functions executions, and your function app can access the same virtual networking resources provided by the environment.

For a general overview of container hosting options for Azure Functions, see [Linux container support in Azure Functions](container-concepts).

## Hosting and workload profiles

There are two primary plans for Container Apps: a serverless [Consumption plan](../container-apps/plans#consumption) and a [Dedicated plan](../container-apps/plans#dedicated). Both can be used in Workload profiles environment types, with workload profiles determining the compute and memory resources available to your apps. A workload profile determines the amount of compute and memory resources available to container apps deployed in an environment. These profiles are configured to fit the different needs of your applications.

The Consumption workload profile is the default profile added to every Workload profiles environment type. You can add Dedicated workload profiles to your environment as you create an environment or after it's created. To learn more about workload profiles, see [Workload profiles in Azure Container Apps](../container-apps/workload-profiles-overview).

Container Apps hosting of containerized function apps is supported in all [regions that support Container Apps](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/?products=container-apps).

If your app doesn't have specific hardware requirements, you can run your environment either in a Consumption plan or in a Dedicated plan using the default Consumption workload profile. When running functions on Container Apps, you're charged only for the Container Apps usage. For more information, see the [Azure Container Apps pricing page](https://azure.microsoft.com/pricing/details/container-apps/).

Azure Functions on Azure Container Apps supports GPU-enabled hosting in the Dedicated plan with workload profiles.

To learn how to create and deploy a function app container to Container Apps in the default Consumption plan, see [Create your first containerized functions on Azure Container Apps](functions-deploy-container-apps).

To learn how to create a Container Apps environment with workload profiles and deploy a function app container to a specific workload, see [Container Apps workload profiles](functions-how-to-custom-container#container-apps-workload-profiles).

## Functions in containers

To use Container Apps hosting, your code must run on a function app in a Linux container that you create and maintain. Functions maintains a set of [language-specific base images](https://mcr.microsoft.com/catalog?search=functions) that you can use to generate your containerized function apps.

When you create a code project using [Azure Functions Core Tools](functions-run-local) and include the [ --docker option](functions-core-tools-reference#func-init), Core Tools generates the Dockerfile with the correct base image, which you can use as a starting point when creating your container.

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

When you make changes to your functions code, you must rebuild and republish your container image. For more information, see [Update an image in the registry](functions-how-to-custom-container#update-an-image-in-the-registry).

## Deployment options

Azure Functions currently supports the following methods of deploying a containerized function app to Azure Container Apps:

[Apache Maven](https://github.com/microsoft/azure-maven-plugins/wiki/Azure-Functions:-Configuration-Details#properties-for-azure-container-apps-hosting-of-azure-functions)[ARM templates](/en-us/azure/templates/microsoft.web/sites?pivots=deployment-language-arm-template)[Azure CLI](functions-deploy-container-apps)[Azure Developer CLI (azd)](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/azdtemplates)[Azure Functions Core Tools](functions-run-local#deploy-containers)[Azure Pipeline tasks](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/AzurePipelineTasks)[Azure portal](https://aka.ms/funconacablade)[Bicep files](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/Biceptemplates)[GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/GitHubActions)[Visual Studio Code](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/VSCode%20Sample)

You can continuously deploy your containerized apps from source code using either [Azure Pipelines](functions-how-to-azure-devops?pivots=v1#deploy-a-container) or [GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/GitHubActions). The continuous deployment feature of Functions isn't currently supported when deploying to Container Apps.

## Managed identity authorization

For the best security, you should connect to remote services using Microsoft Entra authentication and managed identity authorization. You can use managed identities for these connections:

When running in Container Apps, you can use Microsoft Entra ID with managed identities for all binding extensions that support managed identities. Currently, only these binding extensions support event-driven scaling when using managed identity authentication:

- Azure Event Hubs
- Azure Queue Storage
- Azure Service Bus

For other bindings, use fixed replicas when using managed identity authentication. For more information, see the [Functions developer guide](functions-reference#connections).

## Virtual network integration

When you host your function apps in a Container Apps environment, your functions are able to take advantage of both internally and externally accessible virtual networks. To learn more about environment networks, see [Networking in Azure Container Apps environment](../container-apps/networking).

## Event-driven scaling

All Functions triggers can be used in your containerized function app. However, only these triggers can dynamically scale (from zero instances) based on received events when running in a Container Apps environment:

- Azure Cosmos DB (KEDA connection)
- Azure Event Grid
- Azure Event Hubs
- Azure Blob Storage (Event Grid based)
- Azure Queue Storage
- Azure Service Bus
- Durable Functions (MSSQL storage provider)
- HTTP
- Kafka
- Timer

Azure Functions on Container Apps is designed to configure the scale parameters and rules as per the event target. You don't need to worry about configuring the KEDA scaled objects. You can still set minimum and maximum replica count when creating or modifying your function app. The following Azure CLI command sets the minimum and maximum replica count when creating a new function app in a Container Apps environment from an Azure Container Registry:

```
az functionapp create --name <APP_NAME> --resource-group <MY_RESOURCE_GROUP> --max-replicas 15 --min-replicas 1 --storage-account <STORAGE_NAME> --environment MyContainerappEnvironment --image <LOGIN_SERVER>/azurefunctionsimage:v1 --registry-username <USERNAME> --registry-password <SECURE_PASSWORD> --registry-server <LOGIN_SERVER>
```


The following command sets the same minimum and maximum replica count on an existing function app:

```
az functionapp config container set --name <APP_NAME> --resource-group <MY_RESOURCE_GROUP> --max-replicas 15 --min-replicas 1
```


## Managed resource groups

Azure Functions on Container Apps runs your containerized function app resources in specially managed resource groups. These managed resource groups help protect the consistency of your apps by preventing unintended or unauthorized modification or deletion of resources in the managed group, even by service principals.

A managed resource group is created for you the first time you create function app resources in a Container Apps environment. Container Apps resources required by your containerized function app run in this managed resource group. Any other function apps that you create in the same environment use this existing group.

A managed resource group gets removed automatically after all function app container resources are removed from the environment. While the managed resource group is visible, any attempts to modify or remove the managed resource group result in an error. To remove a managed resource group from an environment, remove all of the function app container resources and it gets removed for you.

If you run into any issues with these managed resource groups, you should contact support.

## Application logging

You can monitor your containerized function app hosted in Container Apps using Azure Monitor Application Insights in the same way you do with apps hosted by Azure Functions. For more information, see [Monitor Azure Functions](monitor-functions).

For bindings that support event-driven scaling, scale events are logged as `FunctionsScalerInfo`

and `FunctionsScalerError`

events in your Log Analytics workspace. For more information, see [Application Logging in Azure Container Apps](../container-apps/logging).

## Considerations for Container Apps hosting

Keep in mind the following considerations when deploying your function app containers to Container Apps:

- These limitations apply to Kafka triggers:
- The protocol value of
`ssl`

isn't supported when hosted on Container Apps. Use a[different protocol value](functions-bindings-kafka-trigger?pivots=programming-language-csharp#attributes). - For a Kafka trigger to dynamically scale when connected to Event Hubs, the
`username`

property must resolve to an application setting that contains the actual username value. When the default`$ConnectionString`

value is used, the Kafka trigger isn't able to cause the app to scale dynamically.

- The protocol value of
- For the built-in Container Apps
[policy definitions](../container-apps/policy-reference#policy-definitions), currently only environment-level policies apply to Azure Functions containers. - By default, a containerized function app monitors port 80 for incoming requests. If your app must use a different port, use the
to change this default port.`WEBSITES_PORT`

application setting - You aren't currently able to use built-in continuous deployment features when hosting on Container Apps. You must instead deploy from source code using either
[Azure Pipelines](functions-how-to-azure-devops?pivots=v1#deploy-a-container)or[GitHub Actions](https://github.com/Azure/azure-functions-on-container-apps/tree/main/samples/GitHubActions). - You currently can't move a Container Apps hosted function app deployment between resource groups or between subscriptions. Instead, you would have to recreate the existing containerized app deployment in a new resource group, subscription, or region.
- When using Container Apps, you don't have direct access to the lower-level Kubernetes APIs.
- The
`containerapp`

extension conflicts with the`appservice-kube`

extension in Azure CLI. If you have previously published apps to Azure Arc, run`az extension list`

and make sure that`appservice-kube`

isn't installed. If it is, you can remove it by running`az extension remove -n appservice-kube`

.


---

<!-- DOCUMENTO FUSIONADO: __functions-bindings-event-grid_functions-create-maven-intellij__functions-bindi_de312e.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-event-grid_functions-create-maven-intellij.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-event-grid.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-event-grid -->

# Azure Event Grid bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This reference shows how to connect to Azure Event Grid using Azure Functions triggers and bindings.

Event Grid is an Azure service that sends HTTP requests to notify you about events that happen in publishers. A *publisher* is the service or resource that originates the event. For example, an Azure blob storage account is a publisher, and [a blob upload or deletion is an event](../storage/blobs/storage-blob-event-overview). Some [Azure services have built-in support for publishing events to Event Grid](../event-grid/concepts#event-sources).

Event *handlers* receive and process events. Azure Functions is one of several [Azure services that have built-in support for handling Event Grid events](../event-grid/overview#event-handlers). Functions provides an Event Grid trigger, which invokes a function when an event is received from Event Grid. A similar output binding can be used to send events from your function to an [Event Grid custom topic](../event-grid/post-to-custom-topic).

You can also use an HTTP trigger to handle Event Grid Events. To learn more, see [Receive events to an HTTP endpoint](../event-grid/receive-events). We recommend using the Event Grid trigger over HTTP trigger.

| Action | Type |
|---|---|
| Run a function when an Event Grid event is dispatched |
|

[Output binding](functions-bindings-event-grid-output)[HTTP endpoint](../event-grid/receive-events)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

Add the extension to your project by installing the [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventGrid), version 3.x.

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

Considerations for the Event Grid extension:

- Event Grid extension versions earlier than 3.x don't support
[CloudEvents schema](../event-grid/cloudevents-schema#azure-functions). To consume this schema, instead use an HTTP trigger. - The Event Grid output binding is only available for Functions 2.x and higher.

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below. Support for binding to `Stream`

, and to types from [Azure.Messaging](/en-us/dotnet/api/azure.messaging) is in preview.

**Event Grid trigger**

When you want the function to process a single event, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | Functions tries to deserialize the JSON data of the event into a plain-old CLR object (POCO) type. |
`string` |
The event as a string. |
1 |

[CloudEvent](/en-us/dotnet/api/azure.messaging.cloudevent)1[EventGridEvent](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridevent)1When you want the function to process a batch of events, the Event Grid trigger can bind to the following types:

| Type | Description |
|---|---|
`CloudEvent[]` 1,`EventGridEvent[]` 1,`string[]` ,`BinaryData[]` 1 |
An array of events from the batch. Each entry represents one event. |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.EventGrid 3.3.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.EventGrid/3.3.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Event Grid output binding**

When you want the function to write a single event, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The event as a string. |
`byte[]` |
The bytes of the event message. |
| JSON serializable types | An object representing a JSON event. Functions tries to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write multiple events, the Event Grid output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single event types |
An array containing multiple events. Each entry represents one event. |

For other output scenarios, create and use an [EventGridPublisherClient](/en-us/dotnet/api/azure.messaging.eventgrid.eventgridpublisherclient) with other types from [Azure.Messaging.EventGrid](/en-us/dotnet/api/azure.messaging.eventgrid) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## host.json settings

The Event Grid trigger uses a webhook HTTP request, which can be configured using the same [ host.json settings as the HTTP Trigger](functions-bindings-http-webhook#hostjson-settings).

## Next steps

- If you have questions, submit an issue to the team
[here](https://github.com/Azure/azure-sdk-for-net/issues) [Event Grid trigger](functions-bindings-event-grid-trigger)[Event Grid output binding](functions-bindings-event-grid-output)[Run a function when an Event Grid event is dispatched](functions-bindings-event-grid-trigger)[Dispatch an Event Grid event](functions-bindings-event-grid-trigger)


---

<!-- DOCUMENTO FUSIONADO: functions-create-maven-intellij.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-maven-intellij -->

# Create your first Java function in Azure using IntelliJ

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Java and IntelliJ to create an Azure function.

Specifically, this article shows you:

- How to create an HTTP-triggered Java function in an IntelliJ IDEA project.
- Steps for testing and debugging the project in the integrated development environment (IDE) on your own computer.
- Instructions for deploying the function project to Azure Functions.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - An
[Azure supported Java Development Kit (JDK)](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17 or 21. (Java 21 is currently supported on Linux only) - An
[IntelliJ IDEA](https://www.jetbrains.com/idea/download/)Ultimate Edition or Community Edition installed [Maven 3.5.0+](https://maven.apache.org/download.cgi)- Latest
[Function Core Tools](https://github.com/Azure/azure-functions-core-tools)

## Install plugin and sign in

To install the Azure Toolkit for IntelliJ and then sign in, follow these steps:

In IntelliJ IDEA's

**Settings/Preferences**dialog (Ctrl+Alt+S), select**Plugins**. Then, find the**Azure Toolkit for IntelliJ**in the**Marketplace**and select**Install**. After it's installed, select**Restart**to activate the plugin.To sign in to your Azure account, open the

**Azure Explorer**sidebar, and then select the**Azure Sign In**icon in the bar on top (or from the IDEA menu, select**Tools > Azure > Azure Sign in**).In the

**Azure Sign In**window, select**OAuth 2.0**, and then select**Sign in**. For other sign-in options, see[Sign-in instructions for the Azure Toolkit for IntelliJ](/en-us/azure/developer/java/toolkit-for-intellij/sign-in-instructions).In the browser, sign in with your account and then go back to IntelliJ. In the

**Select Subscriptions**dialog box, select the subscriptions that you want to use, then select**Select**.

## Create your local project

To use Azure Toolkit for IntelliJ to create a local Azure Functions project, follow these steps:

Open IntelliJ IDEA's

**Welcome**dialog, select**New Project**to open a new project wizard, then select**Azure Functions**.Select

**Http Trigger**, then select**Next**and follow the wizard to go through all the configurations in the following pages. Confirm your project location, then select**Finish**. IntelliJ IDEA then opens your new project.

## Run the project locally

To run the project locally, follow these steps:

Important

You must have the JAVA_HOME environment variable set correctly to the JDK directory that is used during code compiling using Maven. Make sure that the version of the JDK is at least as high as the `Java.version`

setting.

Navigate to

*src/main/java/org/example/functions/HttpTriggerJava.java*to see the code generated. Beside line 17, you should see a green**Run**button. Select it and then select**Run 'Functions-azur...'**. You should see your function app running locally with a few logs.You can try the function by accessing the displayed endpoint from browser, such as

`http://localhost:7071/api/HttpTriggerJava?name=Azure`

.The log is also displayed in your IDEA. Stop the function app by selecting

**Stop**.

## Debug the project locally

To debug the project locally, follow these steps:

Select the

**Debug**button in the toolbar. If you don't see the toolbar, enable it by choosing**View**>**Appearance**>**Toolbar**.Select line 20 of the file

*src/main/java/org/example/functions/HttpTriggerJava.java*to add a breakpoint. Access the endpoint`http://localhost:7071/api/HttpTriggerJava?name=Azure`

again and you should find that the breakpoint is hit. You can then try more debug features like**Step**,**Watch**, and**Evaluation**. Stop the debug session by selecting**Stop**.

## Create the function app in Azure

Use the following steps create a function app and related resources in your Azure subscription:

In Azure Explorer in your IDEA, right-click

**Function App**and then select**Create**.Select

**More Settings**and provide the following information at the prompts:Prompt Selection **Subscription**Choose the subscription to use. **Resource Group**Choose the resource group for your function app. **Name**Specify the name for a new function app. Here you can accept the default value. **Platform**Select **Windows-Java 17**or another platform as appropriate.**Region**For better performance, choose a [region](https://azure.microsoft.com/regions/)near you.**Hosting Options**Choose the hosting options for your function app. **Plan**Choose the App Service plan pricing tier you want to use, or select **+**to create a new App Service plan.Important

To create your app in the Flex Consumption plan, select

**Flex Consumption**. The[Flex Consumption plan](flex-consumption-plan)is currently in preview.Select

**OK**. A notification is displayed after your function app is created.

## Deploy your project to Azure

To deploy your project to Azure, follow these steps:

Select and expand the Azure icon in IntelliJ Project explorer, then select

**Deploy to Azure -> Deploy to Azure Functions**.You can select the function app from the previous section. To create a new one, select

**+**on the**Function**line. Type in the function app name and choose the proper platform. Here, you can accept the default value. Select**OK**and the new function app you created is automatically selected. Select**Run**to deploy your functions.

## Manage function apps from IDEA

To manage your function apps with **Azure Explorer** in your IDEA, follow these steps:

Select

**Function App**to see all your function apps listed.Select one of your function apps, then right-click and select

**Show Properties**to open the detail page.Right-click your

**HttpTrigger-Java**function app, then select**Trigger Function in Browser**. You should see that the browser is opened with the trigger URL.

## Add more functions to the project

To add more functions to your project, follow these steps:

Right-click the package

**org.example.functions**and select**New -> Azure Function Class**.Fill in the class name

**HttpTest**and select**HttpTrigger**in the create function class wizard, then select**OK**to create. In this way, you can create new functions as you want.

## Cleaning up functions

Select one of your function apps using **Azure Explorer** in your IDEA, then right-click and select **Delete**. This command might take several minutes to run. When it's done, the status refreshes in **Azure Explorer**.

## Next steps

You've created a Java project with an HTTP triggered function, run it on your local machine, and deployed it to Azure. Now, extend your function by continuing to the following article:


---

<!-- DOCUMENTO FUSIONADO: _functions-bindings-cache-trigger-redisstream_functions-bindings-openai.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: functions-bindings-cache-trigger-redisstream.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cache-trigger-redisstream -->

# RedisStreamTrigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The `RedisStreamTrigger`

reads new entries from a stream and surfaces those elements to the function.

## Scope of availability for functions triggers

| Trigger Type | Azure Managed Redis | Azure Cache for Redis |
|---|---|---|
| Streams | Yes | Yes |

Important

When using Azure Managed Redis or the Enterprise tiers of Azure Cache for Redis, use port 10000 rather than port 6380 or 6379.

Important

Redis triggers aren't currently supported for functions running on a [Consumption plan](consumption-plan) or a [Flex Consumption plan](/en-us/azure/azure-functions/flex-consumption-plan).

Important

The Node.js v4 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Important

The Python v2 model for Functions isn't yet supported by the Azure Cache for Redis extension. For more details about how the v2 model works, refer to the [Azure Functions Python developer guide](functions-reference-python?pivots=python-mode-decorators).

## Example

Important

For .NET functions, using the *isolated worker* model is recommended over the *in-process* model. For a comparison of the *in-process* and *isolated worker* models, see differences between the *isolated worker* model and the *in-process* model for .NET on Azure Functions.

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
using Microsoft.Extensions.Logging;
namespace Microsoft.Azure.Functions.Worker.Extensions.Redis.Samples.RedisStreamTrigger
{
internal class SimpleStreamTrigger
{
private readonly ILogger<SimpleStreamTrigger> logger;
public SimpleStreamTrigger(ILogger<SimpleStreamTrigger> logger)
{
this.logger = logger;
}
[Function(nameof(SimpleStreamTrigger))]
public void Run(
[RedisStreamTrigger(Common.connectionStringSetting, "streamKey")] string entry)
{
logger.LogInformation(entry);
}
}
}
```


```
package com.function.RedisStreamTrigger;
import com.microsoft.azure.functions.*;
import com.microsoft.azure.functions.annotation.*;
import com.microsoft.azure.functions.redis.annotation.*;
public class SimpleStreamTrigger {
@FunctionName("SimpleStreamTrigger")
public void run(
@RedisStreamTrigger(
name = "req",
connection = "redisConnectionString",
key = "streamTest",
pollingIntervalInMs = 1000,
maxBatchSize = 1)
String message,
final ExecutionContext context) {
context.getLogger().info(message);
}
}
```


This sample uses the same `index.js`

file, with binding data in the `function.json`

file.

Here's the `index.js`

file:

```
module.exports = async function (context, entry) {
context.log(entry);
}
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisStreamTrigger",
"connection": "redisConnectionString",
"key": "streamTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "index.js"
}
```


This sample uses the same `run.ps1`

file, with binding data in the `function.json`

file.

Here's the `run.ps1`

file:

```
param($entry, $TriggerMetadata)
Write-Host ($entry | ConvertTo-Json)
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisStreamTrigger",
"connection": "redisConnectionString",
"key": "streamTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "run.ps1"
}
```


The Python v1 programming model requires you to define bindings in a separate *function.json* file in the function folder. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-configuration#programming-model).

This sample uses the same `__init__.py`

file, with binding data in the `function.json`

file.

Here's the `__init__.py`

file:

```
import logging
def main(entry: str):
logging.info(entry)
```


From `function.json`

, here's the binding data:

```
{
"bindings": [
{
"type": "redisStreamTrigger",
"connection": "redisConnectionString",
"key": "streamTest",
"pollingIntervalInMs": 1000,
"maxBatchSize": 16,
"name": "entry",
"direction": "in"
}
],
"scriptFile": "__init__.py"
}
```


## Attributes

| Parameters | Description | Required | Default |
|---|---|---|---|
`Connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`Key`

`PollingIntervalInMs`

`1000`

`MessagesPerWorker`

`100`

`Count`

`10`

`DeleteAfterProcess`

`false`

## Annotations

| Parameter | Description | Required | Default |
|---|---|---|---|
`name` |
`entry` |
Yes | |
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`deleteAfterProcess`

`false`

## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json Properties | Description | Required | Default |
|---|---|---|---|
`type` |
Yes | ||
`deleteAfterProcess` |
Optional | `false` |
|
`connection` |
The name of the
`<cacheName>.redis.cache.windows.net:6380,password...` |

`key`

`pollingIntervalInMs`

`1000`

`messagesPerWorker`

`100`

`count`

`10`

`name`

`direction`

See the Example section for complete examples.

## Usage

The `RedisStreamTrigger`

Azure Function reads new entries from a stream and surfaces those entries to the function.

The trigger polls Redis at a configurable fixed interval, and uses [ XREADGROUP](https://redis.io/commands/xreadgroup/) to read elements from the stream.

The consumer group for all instances of a function is the name of the function, that is, `SimpleStreamTrigger`

for the [StreamTrigger sample](https://github.com/Azure/azure-functions-redis-extension/blob/main/samples/dotnet/RedisStreamTrigger/SimpleStreamTrigger.cs).

Each functions instance uses the [ WEBSITE_INSTANCE_ID](/en-us/azure/app-service/reference-app-settings?tabs=kudu%2Cdotnet#scaling) or generates a random GUID to use as its consumer name within the group to ensure that scaled out instances of the function don't read the same messages from the stream.

| Type | Description |
|---|---|
`byte[]` |
The message from the channel. |
`string` |
The message from the channel. |
`Custom` |
The trigger uses Json.NET serialization to map the message from the channel from a `string` into a custom type. |


---

<!-- DOCUMENTO FUSIONADO: functions-bindings-openai.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai -->

# Azure OpenAI extension for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI extension for Azure Functions implements a set of triggers and bindings that enable you to easily integrate features and behaviors of [Azure OpenAI in Foundry Models](/en-us/azure/ai-services/openai/overview) into your function code executions.

Azure Functions is an event-driven compute service that provides a set of [triggers and bindings](functions-triggers-bindings) to easily connect with other Azure services.

With the integration between Azure OpenAI and Functions, you can build functions that can:

| Action | Trigger/binding type |
|---|---|
| Use a standard text prompt for content completion |
|

[Azure OpenAI assistant trigger](functions-bindings-openai-assistant-trigger)[Azure OpenAI assistant create output binding](functions-bindings-openai-assistantcreate-output)[Azure OpenAI assistant post input binding](functions-bindings-openai-assistantpost-input)[Azure OpenAI assistant query input binding](functions-bindings-openai-assistantquery-input)[Azure OpenAI embeddings input binding](functions-bindings-openai-embeddings-input)[Azure OpenAI embeddings store output binding](functions-bindings-openai-embeddingsstore-output)[Azure OpenAI semantic search input binding](functions-bindings-openai-semanticsearch-input)## Install extension

The extension NuGet package you install depends on the C# mode [in-process](functions-dotnet-class-library) or [isolated worker process](dotnet-isolated-process-guide) you're using in your function app:

Add the Azure OpenAI extension to your project by installing the [Microsoft.Azure.Functions.Worker.Extensions.OpenAI](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI) NuGet package, which you can do using the .NET CLI:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.OpenAI --prerelease
```


When using a vector database for storing content, you should also install at least one of these NuGet packages:

- Azure AI Search:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.AzureAISearch](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.AzureAISearch) - Azure Cosmos DB for MongoDB vCore:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBSearch](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBSearch) - Azure Cosmos DB for NoSQL:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBSearch](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.CosmosDBNoSQLSearch) - Azure Data Explorer:
[Microsoft.Azure.Functions.Worker.Extensions.OpenAI.Kusto](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.OpenAI.Kusto)

## Install bundle

To be able to use this preview binding extension in your app, you must reference a preview extension bundle that includes it.

Add or replace the following code in your `host.json`

file, which specifically targets the latest [preview version of the 4.x bundle](https://github.com/Azure/azure-functions-extension-bundles/releases?q=preview+NOT+experimental&expanded=true):

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle.Preview",
"version": "[4.0.0, 5.0.0)"
}
}
```


Select the previous link to verify that the latest preview bundle version does contain the preview extension.

## Connecting to OpenAI

To use the Azure OpenAI binding extension, you need to specify a connection to OpenAI. This connection is defined using application settings, and the `AIConnectionName`

property of the trigger or binding. You can also use environment variables to define key-based connections.

We recommend that you use managed identity-based connections and the `AIConnectionName`

property.

The OpenAI bindings have an `AIConnectionName`

property that you can use to specify the `<ConnectionNamePrefix>`

for this group of app settings that define the connection to Azure OpenAI:

| Setting name | Description |
|---|---|
`<CONNECTION_NAME_PREFIX>__endpoint` |
Sets the URI endpoint of the Azure OpenAI in Foundry Models. This setting is always required. |
`<CONNECTION_NAME_PREFIX>__clientId` |
Sets the specific user-assigned identity to use when obtaining an access token. Requires that `<CONNECTION_NAME_PREFIX>__credential` is set to `managedidentity` . The property accepts a client ID corresponding to a user-assigned identity assigned to the application. It's invalid to specify both a Resource ID and a client ID. If not specified, the system-assigned identity is used. This property is used differently in
`credential` shouldn't be set. |
`<CONNECTION_NAME_PREFIX>__credential` |
Defines how an access token is obtained for the connection. Use `managedidentity` for managed identity authentication. This value is only valid when a managed identity is available in the hosting environment. |
`<CONNECTION_NAME_PREFIX>__managedIdentityResourceId` |
When `credential` is set to `managedidentity` , this property can be set to specify the resource Identifier to be used when obtaining a token. The property accepts a resource identifier corresponding to the resource ID of the user-defined managed identity. It's invalid to specify both a resource ID and a client ID. If neither are specified, the system-assigned identity is used. This property is used differently in
`credential` shouldn't be set. |
`<CONNECTION_NAME_PREFIX>__key` |
Sets the shared secret key required to access the endpoint of Azure OpenAI using key-based authentication. As a security best practice, you should always use Microsoft Entra ID with managed identities for authentication. |

Consider these managed identity connection settings when then `AIConnectionName`

property is set to `myAzureOpenAI`

:

`myAzureOpenAI__endpoint=https://contoso.openai.azure.com/`

`myAzureOpenAI__credential=managedidentity`

`myAzureOpenAI__clientId=aaaaaaaa-bbbb-cccc-1111-222222222222`


At runtime, these settings are collectively interpreted by the host as a single `myAzureOpenAI`

setting like this:

```
"myAzureOpenAI":
{
"endpoint": "https://contoso.openai.azure.com/",
"credential": "managedidentity",
"clientId": "aaaaaaaa-bbbb-cccc-1111-222222222222"
}
```


When using managed identities, make sure to add your identity to the [Cognitive Services OpenAI User](../role-based-access-control/built-in-roles/ai-machine-learning#cognitive-services-openai-user) role.

When running locally, you must add these settings to the *local.settings.json* project file. For more information, see [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

For more information, see [Work with application settings](functions-how-to-use-azure-function-app-settings#settings).
