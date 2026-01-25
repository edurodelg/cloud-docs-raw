---
merged_at: 2026-01-25T02:11:58.430132
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-what-is-data-import.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-what-is-data-import -->

# Data import in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, queries execute over your content that's loaded into a [search index](search-what-is-an-index). This article describes the two basic workflows for populating an index: *push* your data into the index programmatically, or *pull* in the data using a [search indexer](search-indexer-overview).

Both approaches load documents from an external data source. Although you can create an empty index, it's not queryable until you add the content.

Note

If [AI enrichment](cognitive-search-concept-intro) or [integrated vectorization](vector-search-integrated-vectorization) are solution requirements, you must use the pull model (indexers) to load an index. Skillsets are attached to indexers and don't run independently.

## Pushing data to an index

Push model is an approach that uses APIs to upload documents into an existing search index. You can upload documents individually or in batches up to 1000 per batch, or 16 MB per batch, whichever limit comes first.

Key benefits include:

No restrictions on data source type. The payload must be composed of JSON documents that map to your index schema, but the data can be sourced from anywhere.

No restrictions on frequency of execution. You can push changes to an index as often as you like. For applications having low latency requirements (for example, when the index needs to be in sync with product inventory fluctuations), the push model is your only option.

Connectivity and the secure retrieval of documents are fully under your control. In contrast, indexer connections are authenticated using the security features provided in Azure AI Search.


### How to push data to an Azure AI Search index

Use the following APIs to load single or multiple documents into an index:

[Index Documents (REST API)](/en-us/rest/api/searchservice/documents)[IndexDocumentsAsync (Azure SDK for .NET)](/en-us/dotnet/api/azure.search.documents.searchclient.indexdocumentsasync)or[SearchIndexingBufferedSender](/en-us/dotnet/api/azure.search.documents.searchindexingbufferedsender-1)[IndexDocumentsBatch (Azure SDK for Python)](/en-us/python/api/azure-search-documents/azure.search.documents.indexdocumentsbatch)or[SearchIndexingBufferedSender](/en-us/python/api/azure-search-documents/azure.search.documents.searchindexingbufferedsender)[IndexDocumentsBatch (Azure SDK for Java)](/en-us/java/api/com.azure.search.documents.indexes.models.indexdocumentsbatch)or[SearchIndexingBufferedSender](/en-us/java/api/com.azure.search.documents.searchindexingbufferedasyncsender)[IndexDocumentsBatch (Azure SDK for JavaScript](/en-us/javascript/api/@azure/search-documents/indexdocumentsbatch)or[SearchIndexingBufferedSender](/en-us/javascript/api/@azure/search-documents/searchindexingbufferedsender)

There's no support for pushing data via the Azure portal.

For an introduction to the push APIs, see:

[Quickstart: Full-text search](search-get-started-text)[C# Tutorial: Optimize indexing with the push API](tutorial-optimize-indexing-push-api)[REST Quickstart: Create an Azure AI Search index using PowerShell](search-get-started-text)

### Indexing actions: upload, merge, mergeOrUpload, delete

You can control the type of indexing action on a per-document basis, specifying whether the document should be uploaded in full, merged with existing document content, or deleted.

Whether you use the REST API or an Azure SDK, the following document operations are supported for data import:

**Upload**, similar to an "upsert" where the document is inserted if it's new, and updated or replaced if it exists. If the document is missing values that the index requires, the document field's value is set to null.**merge**updates a document that already exists, and fails a document that can't be found. Merge replaces existing values. For this reason, be sure to check for collection fields that contain multiple values, such as fields of type`Collection(Edm.String)`

. For example, if a`tags`

field starts with a value of`["budget"]`

and you execute a merge with`["economy", "pool"]`

, the final value of the`tags`

field is`["economy", "pool"]`

. It won't be`["budget", "economy", "pool"]`

.**mergeOrUpload**behaves like**merge**if the document exists, and**upload**if the document is new.**delete**removes the entire document from the index. If you want to remove an individual field, use**merge**instead, setting the field in question to null.

## Pulling data into an index

The pull model uses *indexers* connecting to a supported data source, automatically uploading the data into your index. Indexers from Microsoft are available for these platforms:

[Azure Blob storage](search-how-to-index-azure-blob-storage)[Azure Table storage](search-how-to-index-azure-tables)[Azure Data Lake Storage Gen2](search-how-to-index-azure-data-lake-storage)[Azure Files (preview)](search-file-storage-integration)[Azure Cosmos DB](search-how-to-index-cosmosdb-sql)[Azure SQL Database, SQL Managed Instance, and SQL Server on Azure VMs](search-how-to-index-sql-database)[Microsoft OneLake files and shortcuts](search-how-to-index-onelake-files)[SharePoint in Microsoft 365 (preview)](search-how-to-index-sharepoint-online)

You can use third-party connectors, developed and maintained by Microsoft partners. For more information and links, see [Data source gallery](search-data-sources-gallery).

Indexers connect an index to a data source (usually a table, view, or equivalent structure), and map source fields to equivalent fields in the index. During execution, the rowset is automatically transformed to JSON and loaded into the specified index. All indexers support schedules so that you can specify how frequently the data is to be refreshed. Most indexers provide change tracking if the data source supports it. By tracking changes and deletes to existing documents in addition to recognizing new documents, indexers remove the need to actively manage the data in your index.

### How to pull data into an Azure AI Search index

Use the following tools and APIs for indexer-based indexing:

- Azure portal:
[Import wizards](search-import-data-portal) - REST APIs:
[Create Indexer (REST)](/en-us/rest/api/searchservice/indexers/create),[Create Data Source (REST)](/en-us/rest/api/searchservice/data-sources/create),[Create Index (REST)](/en-us/rest/api/searchservice/indexes/create) - Azure SDK for .NET:
[SearchIndexer](/en-us/dotnet/api/azure.search.documents.indexes.models.searchindexer),[SearchIndexerDataSourceConnection](/en-us/dotnet/api/azure.search.documents.indexes.models.searchindexerdatasourceconnection),[SearchIndex](/en-us/dotnet/api/azure.search.documents.indexes.models.searchindex), - Azure SDK for Python:
[SearchIndexer](/en-us/python/api/azure-search-documents/azure.search.documents.indexes.models.searchindexer),[SearchIndexerDataSourceConnection](/en-us/python/api/azure-search-documents/azure.search.documents.indexes.models.searchindexerdatasourceconnection),[SearchIndex](/en-us/python/api/azure-search-documents/azure.search.documents.indexes.models.searchindex), - Azure SDK for Java:
[SearchIndexer](/en-us/java/api/com.azure.search.documents.indexes.models.searchindexer),[SearchIndexerDataSourceConnection](/en-us/java/api/com.azure.search.documents.indexes.models.searchindexerdatasourceconnection),[SearchIndex](/en-us/java/api/com.azure.search.documents.indexes.models.searchindex), - Azure SDK for JavaScript:
[SearchIndexer](/en-us/javascript/api/@azure/search-documents/searchindexer),[SearchIndexerDataSourceConnection](/en-us/javascript/api/@azure/search-documents/searchindexerdatasourceconnection),[SearchIndex](/en-us/javascript/api/@azure/search-documents/searchindex),

Indexer functionality is exposed in the Azure portal, the [REST API](/en-us/rest/api/searchservice/indexers/create), and the [.NET SDK](/en-us/dotnet/api/azure.search.documents.indexes.searchindexerclient).

An advantage to using the Azure portal is that Azure AI Search can usually generate a default index schema by reading the metadata of the source dataset.

## Verify data import with Search explorer

A quick way to perform a preliminary check on the document upload is to use [ Search explorer](search-explorer) in the Azure portal.


The explorer lets you query an index without having to write any code. The search experience is based on default settings, such as the [simple syntax](/en-us/rest/api/searchservice/simple-query-syntax-in-azure-search) and default [searchMode query parameter](/en-us/rest/api/searchservice/documents/search-post). Results are returned in JSON so that you can inspect the entire document.

Here's an example query that you can run in Search Explorer in JSON view. The "HotelId" is the document key of the hotels-sample-index. The filter provides the document ID of a specific document:

```
{
"search": "*",
"filter": "HotelId eq '50'"
}
```


If you're using REST, this [Look up query](search-query-simple-examples#example-2-look-up-by-id) achieves the same purpose.


---

<!-- DOCUMENTO FUSIONADO: search-monitor-queries.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-monitor-queries -->

# Monitor query requests in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to measure query performance and volume using built-in metrics and diagnostic logging. It also explains how to get the query strings entered by application users.

The Azure portal shows basic metrics about query latency, query load (QPS), and throttling. Historical data that feeds into these metrics can be accessed in the Azure portal for 30 days. For longer retention, or to report on operational data and query strings, you must [enable diagnostic logging](search-monitor-enable-logging) and choose a storage option for persisting logged operations and metrics. We recommend **Log Analytics workspace** as a destination for logged operations. Kusto queries and data exploration target a Log Analytics workspace.

Conditions that maximize the integrity of data measurement include:

Use a billable service (a service created at either the Basic or a Standard tier). The free service is shared by multiple subscribers, which introduces a certain amount of volatility as loads shift.

Use a single replica and partition, if possible, to create a contained and isolated environment. If you use multiple replicas, query metrics are averaged across multiple nodes, which can lower the precision of results. Similarly, multiple partitions mean that data is divided, with the potential that some partitions might have different data if indexing is also underway. When you tune query performance, a single node and partition gives a more stable environment for testing.


## Query volume (QPS)

Volume is measured as **Search Queries Per Second** (QPS), a built-in metric that can be reported as an average, count, minimum, or maximum values of queries that execute within a one-minute window. One-minute intervals (TimeGrain = "PT1M") for metrics is fixed within the system.

Azure AI Search retains 30-days of metrics data by default. You can enable logging for longer retention. QPS is available in the Azure portal, in the **Monitoring** tab of your search service.


To learn more about the SearchQueriesPerSecond metric, see [Search queries per second](monitor-azure-cognitive-search-data-reference#search-queries-per-second).

## Query performance

Service-wide, query performance is measured as *search latency* and *throttled queries*. These metrics are also available on the **Monitoring** tab.

### Search latency

Search latency indicates how long a query takes to complete. To learn more about the SearchLatency metric, see [Search latency](monitor-azure-cognitive-search-data-reference#search-latency).

Consider the following example of **Search Latency** metrics: 86 queries were sampled, with an average duration of 23.26 milliseconds. A minimum of 0 indicates some queries were dropped. The longest running query took 1000 milliseconds to complete. Total execution time was 2 seconds.

### Throttled queries

Throttled queries refers to queries that are dropped instead of processed. In most cases, throttling is a normal part of running the service. It isn't necessarily an indication that there's something wrong. To learn more about the ThrottledSearchQueriesPercentage metric, see [Throttled search queries percentage](monitor-azure-cognitive-search-data-reference#throttled-search-queries-percentage).

In the following screenshot, the first number is the count (or number of metrics sent to the log). Other aggregations, which appear at the top or when hovering over the metric, include average, maximum, and total. In this sample, no requests were dropped.

## Explore metrics in the Azure portal

For a quick look at the current numbers, the **Monitoring** tab on the service Overview page shows three metrics (**Search latency**, **Search queries per second (per search unit)**, **Throttled Search Queries Percentage**) over fixed intervals measured in hours, days, and weeks, with the option of changing the aggregation type.

For deeper exploration, open metrics explorer from the **Monitoring** menu so that you can layer, zoom in, and visualize data to explore trends or anomalies. Learn more about metrics explorer by completing this [tutorial on creating a metrics chart](/en-us/azure/azure-monitor/essentials/tutorial-metrics).

Under the Monitoring section, select

**Metrics**to open the metrics explorer with the scope set to your search service.Under Metric, choose one from the dropdown list and review the list of available aggregations for a preferred type. The aggregation defines how the collected values are sampled over each time interval.

In the top-right corner, set the time interval.

Choose a visualization. The default is a line chart.

Layer more aggregations by choosing

**Add metric**and selecting different aggregations.Zoom into an area of interest on the line chart. Put the mouse pointer at the beginning of the area, select and hold the left mouse button, drag to the other side of area, and release the button. The chart zooms in on that time range.


## Return query strings entered by users

When you enable resource logging, the system captures query requests in the **AzureDiagnostics** table. As a prerequisite, you must have already specified [a destination for logged operations](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings), either a log analytics workspace or another storage option.

Under the Monitoring section, select

**Logs**to open up an empty query window in Log Analytics.Run the following expression to search

`Query.Search`

operations, returning a tabular result set consisting of the operation name, query string, the index queried, and the number of documents found. The last two statements exclude query strings consisting of an empty or unspecified search, over a sample index, which cuts down the noise in your results.`AzureDiagnostics | project OperationName, Query_s, IndexName_s, Documents_d | where OperationName == "Query.Search" | where Query_s != "?api-version=2025-09-01&search=*" | where IndexName_s != "hotels-sample-index"`

Optionally, set a Column filter on

*Query_s*to search over a specific syntax or string. For example, you could filter over*is equal to*`?api-version=2025-09-01&search=*&%24filter=HotelName`

.

While this technique works for ad hoc investigation, building a report lets you consolidate and present the query strings in a layout more conducive to analysis.

## Identify long-running queries

Add the duration column to get the numbers for all queries, not just those that are picked up as a metric. Sorting this data shows you which queries take the longest to complete.

Under the Monitoring section, select

**Logs**to query for log information.Run the following basic query to return queries, sorted by duration in milliseconds. The longest-running queries are at the top.

`AzureDiagnostics | project OperationName, resultSignature_d, DurationMs, Query_s, Documents_d, IndexName_s | where OperationName == "Query.Search" | sort by DurationMs`


## Create a metric alert

A [metric alert](/en-us/azure/azure-monitor/alerts/alerts-types#metric-alerts) establishes a threshold for sending a notification or triggering a corrective action that you define in advance. You can create alerts related to query execution, but you can also create them for resource health, search service configuration changes, skill execution, and document processing (indexing).

All thresholds are user-defined, so you should have an idea of what activity level should trigger the alert.

For query monitoring, it's common to create a metric alert for search latency and throttled queries. If you know *when* queries are dropped, you can look for remedies that reduce load or increase capacity. For example, if throttled queries increase during indexing, you could postpone it until query activity subsides.

If you're pushing the limits of a particular replica-partition configuration, setting up alerts for query volume thresholds (QPS) is also helpful.

Under

**Monitoring**, select**Alerts**and then select**Create alert rule**.Under Condition, select

**Add**.Configure signal logic. For signal type, choose

**metrics**and then select the signal.After selecting the signal, you can use a chart to visualize historical data for an informed decision on how to proceed with setting up conditions.

Next, scroll down to Alert logic. For proof-of-concept, you could specify an artificially low value for testing purposes.

Next, specify or create an Action Group. This is the response to invoke when the threshold is met. It might be a push notification or an automated response.

Last, specify Alert details. Name and describe the alert, assign a severity value, and specify whether to create the rule in an enabled or disabled state.


If you specified an email notification, you receive an email from "Microsoft Azure" with a subject line of "Azure: Activated Severity: 3 `<your rule name>`

".

## Next steps

If you haven't done so already, review the fundamentals of search service monitoring to learn about the full range of oversight capabilities.
