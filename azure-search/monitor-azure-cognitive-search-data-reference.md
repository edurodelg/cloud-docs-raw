---
source_url: https://learn.microsoft.com/en-us/azure/search/monitor-azure-cognitive-search-data-reference
fetched_at: 2026-01-25T02:10:48.550714
---

# Azure AI Search monitoring data reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article contains all the monitoring reference information for this service.

See [Monitor Azure AI Search](monitor-azure-cognitive-search) for details on the data you can collect for Azure AI Search and how to use it.

## Metrics

This section lists all the automatically collected platform metrics for this service. These metrics are also part of the global list of [all platform metrics supported in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index#supported-metrics-per-resource-type).

For information on metric retention, see [Azure Monitor Metrics overview](/en-us/azure/azure-monitor/essentials/data-platform-metrics#retention-of-metrics).

### Supported metrics for Microsoft.Search/searchServices

The following table lists the metrics available for the Microsoft.Search/searchServices resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Document processed countNumber of documents processed |
`DocumentsProcessedCount` |
Count | Total (Sum), Count | `DataSourceName` , `Failed` , `IndexerName` , `IndexName` , `SkillsetName` |
PT1M | Yes |
Search LatencyAverage search latency for the search service |
`SearchLatency` |
Seconds | Average | <none> | PT1M | Yes |
Search queries per secondSearch queries per second for the search service |
`SearchQueriesPerSecond` |
CountPerSecond | Average | <none> | PT1M | Yes |
Skill execution invocation countNumber of skill executions |
`SkillExecutionCount` |
Count | Total (Sum), Count | `DataSourceName` , `Failed` , `IndexerName` , `SkillName` , `SkillsetName` , `SkillType` |
PT1M | Yes |
Throttled search queries percentagePercentage of search queries that were throttled for the search service |
`ThrottledSearchQueriesPercentage` |
Percent | Average | <none> | PT1M | Yes |

#### Search queries per second

This metric shows the average of the search queries per second (QPS) for the search service. It's common for queries to execute in milliseconds, so only queries that measure as seconds appear in a metric like QPS. The minimum is the lowest value for search queries per second that was registered during that minute. Maximum is the highest value. Average is the aggregate across the entire minute.

| Aggregation type | Description |
|---|---|
| Average | The average number of seconds within a minute during which query execution occurred. |
| Count | The number of metrics emitted to the log within the one-minute interval. |
| Maximum | The highest number of search queries per second registered during a minute. |
| Minimum | The lowest number of search queries per second registered during a minute. |
| Sum | The sum of all queries executed within the minute. |

For example, within one minute, you might have a pattern like this: one second of high load that is the maximum for SearchQueriesPerSecond, followed by 58 seconds of average load, and finally one second with only one query, which is the minimum.

Another example: if a node emits 100 metrics, where the value of each metric is 40, then "Count" is 100, "Sum" is 4000, "Average" is 40, and "Max" is 40.

#### Search latency

Search latency indicates how long a query takes to complete.

| Aggregation type | Latency |
|---|---|
| Average | Average query duration in milliseconds. |
| Count | The number of metrics emitted to the log within the one-minute interval. |
| Maximum | Longest running query in the sample. |
| Minimum | Shortest running query in the sample. |
| Total | Total execution time of all queries in the sample, executing within the interval (one minute). |

#### Throttled search queries percentage

This metric refers to queries that are dropped instead of processed. Throttling occurs when the number of requests in execution exceed capacity. You might see an increase in throttled requests when a replica is taken out of rotation or during indexing. Both query and indexing requests are handled by the same set of resources.

The service determines whether to drop requests based on resource consumption. The percentage of resources consumed across memory, CPU, and disk IO are averaged over a period of time. If this percentage exceeds a threshold, all requests to the index are throttled until the volume of requests is reduced.

Depending on your client, a throttled request is indicated in these ways:

- A service returns an error
`"You are sending too many requests. Please try again later."`

- A service returns a 503 error code indicating the service is currently unavailable.
- If you're using the Azure portal (for example, Search Explorer), the query is dropped silently and you need to select
**Search**again.

To confirm throttled queries, use **Throttled search queries** metric. You can explore metrics in the Azure portal or create an alert metric as described in this article. For queries that were dropped within the sampling interval, use *Total* to get the percentage of queries that didn't execute.

| Aggregation type | Throttling |
|---|---|
| Average | Percentage of queries dropped within the interval. |
| Count | The number of metrics emitted to the log within the one-minute interval. |
| Maximum | Percentage of queries dropped within the interval. |
| Minimum | Percentage of queries dropped within the interval. |
| Total | Percentage of queries dropped within the interval. |

For **Throttled Search Queries Percentage**, minimum, maximum, average and total, all have the same value: the percentage of search queries that were throttled, from the total number of search queries during one minute.

## Metric dimensions

For information about what metric dimensions are, see [Multi-dimensional metrics](/en-us/azure/azure-monitor/platform/data-platform-metrics#multi-dimensional-metrics).

Azure AI Search has dimensions associated with the following metrics that capture a count of documents or skills that were executed.

| Metric name | Description | Dimensions | Sample use cases |
|---|---|---|---|
Document processed count |
Shows the number of indexer processed documents. | Data source name, failed, index name, indexer name, skillset name | Can be referenced as a rough measure of throughput (number of documents processed by indexer over time) - Set up to alert on failed documents |
Skill execution invocation count |
Shows the number of skill invocations. | Data source name, failed, index name, indexer name, skill name, skill type, skillset name | Reference to ensure skills are invoked as expected by comparing relative invocation numbers between skills and number of skill invocations to the number of documents. - Set up to alert on failed skill invocations |

| Dimension name | Description |
|---|---|
DataSourceName |
A named data source connection used during indexer execution. Valid values are one of the
|

**Failed****IndexerName****IndexName****SkillsetName****SkillName****SkillType**## Resource logs

This section lists the types of resource logs you can collect for this service. The section pulls from the list of [all resource logs category types supported in Azure Monitor](/en-us/azure/azure-monitor/platform/resource-logs-schema).

### Supported resource logs for Microsoft.Search/searchServices

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`OperationLogs`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

## Azure Monitor Logs tables

This section lists the Azure Monitor Logs tables relevant to this service, which are available for query by Log Analytics using Kusto queries. The tables contain resource log data and possibly more depending on what is collected and routed to them.

### Search Services

Microsoft.Search/searchServices

| Table | Description |
|---|---|
|

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)[search-specific properties](#resource-log-search-props), and the[search-specific operations](#resource-log-search-ops)listed in the schema reference section.[AzureMetrics](/en-us/azure/azure-monitor/reference/tables/azuremetrics)### Resource log tables

The following table lists the properties of resource logs in Azure AI Search. The resource logs are collected into Azure Monitor Logs or Azure Storage. In Azure Monitor, logs are collected in the AzureDiagnostics table under the resource provider name of `Microsoft.Search`

.

| Azure Storage field or property | Azure Monitor Logs property | Description |
|---|---|---|
| time | TIMESTAMP | The date and time (UTC) when the operation occurred. |
| resourceId | Concat("/", "/subscriptions", SubscriptionId, "resourceGroups", ResourceGroupName, "providers/Microsoft.Search/searchServices", ServiceName) | The Azure AI Search resource for which logs are enabled. |
| category | "OperationLogs" | Log categories include `Audit` , `Operational` , `Execution` , and `Request` . |
| operationName | Name | Name of the operation. The operation name can be `Indexes.ListIndexStatsSummaries` , `Indexes.Get` , `Indexes.Stats` , `Indexers.List` , `Query.Search` , `Query.Suggest` , `Query.Lookup` , `Query.Autocomplete` , `CORS.Preflight` , `Indexes.Update` , `Indexes.Prototype` , `ServiceStats` , `DataSources.List` , `Indexers.Warmup` . |
| durationMS | DurationMilliseconds | The duration of the operation, in milliseconds. |
| operationVersion | ApiVersion | The API version used on the request. |
| resultType | (Failed) ? "Failed" : "Success" | The type of response. |
| resultSignature | Status | The HTTP response status of the operation. |
| properties | Properties | Any extended properties related to this category of events. |

## Activity log

The linked table lists the operations that can be recorded in the activity log for this service. These operations are a subset of [all the possible resource provider operations in the activity log](/en-us/azure/role-based-access-control/resource-provider-operations).

For more information on the schema of activity log entries, see [Activity Log schema](/en-us/azure/azure-monitor/essentials/activity-log-schema).

The following table lists common operations related to Azure AI Search that may be recorded in the activity log. For a complete listing of all Microsoft.Search operations, see [Microsoft.Search resource provider operations](/en-us/azure/role-based-access-control/resource-provider-operations#microsoftsearch).

| Operation | Description |
|---|---|
| Get Admin Key | Any operation that requires administrative rights is logged as a "Get Admin Key" operation. |
| Get Query Key | Any read-only operation against the documents collection of an index. |
| Regenerate Admin Key | A request to regenerate either the primary or secondary admin API key. |

Common entries include references to API keys - generic informational notifications like *Get Admin Key* and *Get Query keys*. These activities indicate requests that were made using the admin key (create or delete objects) or query key, but don't show the request itself. For information of this grain, you must configure resource logging.

Alternatively, you might gain some insight through change history. In the Azure portal, select the activity to open the detail page and then select "Change history" for information about the underlying operation.

## Other schemas

The following schemas are in use for this service.

If you're building queries or custom reports, the data structures that contain Azure AI Search resource logs conform to the following schemas.

For resource logs sent to blob storage, each blob has one root object called **records** containing an array of log objects. Each blob contains records for all the operations that took place during the same hour.

### Resource log schema

All resource logs available through Azure Monitor share a [common top-level schema](/en-us/azure/azure-monitor/essentials/resource-logs-schema#top-level-common-schema). Azure AI Search supplements with [more properties](#resource-log-search-props) and [operations](#resource-log-search-ops) that are unique to a search service.

The following example illustrates a resource log that includes common properties (TimeGenerated, Resource, Category, and so forth) and search-specific properties (OperationName and OperationVersion).

| Name | Type | Description and example |
|---|---|---|
| TimeGenerated | Datetime | Timestamp of the operation. For example: `2021-12-07T00:00:43.6872559Z` |
| Resource | String | Resource ID. For example: `/subscriptions/<your-subscription-id>/resourceGroups/<your-resource-group-name>/providers/Microsoft.Search/searchServices/<your-search-service-name>` |
| Category | String | "OperationLogs". This value is a constant. OperationLogs is the only category used for resource logs. |
| OperationName | String | The name of the operation (see the
`Query.Search` |

`2025-09-01`

`200`

#### Properties schema

The following properties are specific to Azure AI Search.

| Name | Type | Description and example |
|---|---|---|
| Description_s | String | The operation's endpoint. For example: `GET /indexes('content')/docs` |
| Documents_d | Int | Number of documents processed. |
| IndexName_s | String | Name of the index associated with the operation. |
| Query_s | String | The query parameters used in the request. For example: `?search=beach access&$count=true&api-version=2025-09-01` |

#### OperationName values (logged operations)

The following operations can appear in a resource log.

| OperationName | Description |
|---|---|
| DataSources.* | Applies to indexer data sources. Can be Create, Delete, Get, List. |
| DebugSessions.* | Applies to a debug session. Can be Create, Delete, Get, List, Start, and Status. |
| DebugSessions.DocumentStructure | An enriched document is loaded into a debug session. |
| DebugSessions.RetrieveIndexerExecutionHistoricalData | A request for indexer execution details. |
| DebugSessions.RetrieveProjectedIndexerExecutionHistoricalData | Execution history for enrichments projected to a knowledge store. |
| Indexers.* | Applies to an indexer. Can be Create, Delete, Get, List, and Status. |
| Indexes.* | Applies to a search index. Can be Create, Delete, Get, List. |
| indexes.Prototype | This index is created by the Import Data wizard. |
| Indexing.Index | This operation is a call to
|

[Query types and composition](search-query-overview).[Query types and composition](search-query-overview).[Query types and composition](search-query-overview).[Query types and composition](search-query-overview).[Get Service Statistics](/en-us/rest/api/searchservice/get-service-statistics/get-service-statistics), either called directly or implicitly to populate a portal overview page when it's loaded or refreshed.## Related content

- See
[Monitor Azure AI Search](monitor-azure-cognitive-search)for a description of monitoring Azure AI Search. - See
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)for details on monitoring Azure resources.