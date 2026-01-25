---
merged_at: 2026-01-25T03:18:14.053968
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-performance-analysis.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-performance-analysis -->

# Analyze performance in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes the tools, behaviors, and approaches for analyzing query and indexing performance in Azure AI Search.

This article applies to [classic search](search-what-is-azure-search#what-is-classic-search), full-text search scenarios only.

## Develop baseline numbers

In any large implementation, it's critical to do a performance benchmarking test of your Azure AI Search service before you roll it into production. You should test both the search query load that you expect, but also the expected data ingestion workloads (if possible, run both workloads simultaneously). Having benchmark numbers helps to validate the proper [search tier](search-sku-tier), [service configuration](search-capacity-planning), and expected [query latency](search-performance-analysis#average-query-latency).

To isolate the effects of a distributed service architecture, try testing on service configurations of one replica and one partition.

Note

For the Storage Optimized tiers (L1 and L2), you should expect a lower query throughput and higher latency than the Standard tiers.

## Use resource logging

The most important diagnostic tool at an administrator's disposal is [resource logging](monitor-azure-cognitive-search#azure-monitor-resource-logs). Resource logging is the collection of operational data and metrics about your search service. Resource logging is enabled through [Azure Monitor](/en-us/azure/azure-monitor/overview). There are costs associated with using Azure Monitor and storing data, but if you enable it for your service, it can be instrumental in investigating performance issues.

The following image shows the chain of events in a query request and response. Latency can occur at any one of them, whether during a network transfer, processing of content in the app services layer, or on a search service. A key benefit of resource logging is that activities are logged from the search service perspective, which means that the log can help you determine if the performance issue is due to problems with the query or indexing, or some other point of failure.


Resource logging gives you options for storing logged information. We recommend using [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview) so that you can execute advanced Kusto queries against the data to answer many questions about usage and performance.

On your search service portal pages, you can enable logging through **Diagnostic settings**, and then issue Kusto queries against Log Analytics by choosing **Logs**. To learn how to send resource logs to a Log Analytics workspace where you can analyze them with log queries, see [Collect and analyze resource logs from an Azure resource](/en-us/azure/azure-monitor/essentials/tutorial-resource-logs).

## Throttling behaviors

Throttling occurs when the search service is at capacity. Throttling can occur during queries or indexing. From the client side, an API call results in a 503 HTTP response when it has been throttled. During indexing, there's also the possibility of receiving a 207 HTTP response, which indicates that one or more items failed to index. This error is an indicator that the search service is getting close to capacity.

As a rule of thumb, try to quantify the amount of throttling and any patterns. For example, if one search query out of 500,000 is throttled, it might not be worth investigating. However, if a large percentage of queries is throttled over a period, this would be a greater concern. By looking at throttling over a period, it also helps to identify time frames where throttling might more likely occur and help you decide how to best accommodate that.

A simple fix to most throttling issues is to throw more resources at the search service (typically replicas for query-based throttling, or partitions for indexing-based throttling). However, increasing replicas or partitions adds cost, which is why it's important to know the reason why throttling is occurring at all. Investigating the conditions that cause throttling will be explained in the next several sections.

Below is an example of a Kusto query that can identify the breakdown of HTTP responses from the search service that has been under load. Over a 7-day period, the rendered bar chart shows that a relatively large percentage of the search queries were throttled, in comparison to the number of successful (200) responses.

```
AzureDiagnostics
| where TimeGenerated > ago(7d)
| summarize count() by resultSignature_d
| render barchart
```


Examining throttling over a specific time period can help you identify the times where throttling might occur more frequently. In the below example, a time series chart is used to show the number of throttled queries that occurred over a specified time frame. In this case, the throttled queries correlated with the times in with the performance benchmarking was performed.

```
let ['_startTime']=datetime('2024-02-25T20:45:07Z');
let ['_endTime']=datetime('2024-03-03T20:45:07Z');
let intervalsize = 1m;
AzureDiagnostics
| where TimeGenerated > ago(7d)
| where resultSignature_d != 403 and resultSignature_d != 404 and OperationName in ("Query.Search", "Query.Suggest", "Query.Lookup", "Query.Autocomplete")
| summarize
ThrottledQueriesPerMinute=bin(countif(OperationName in ("Query.Search", "Query.Suggest", "Query.Lookup", "Query.Autocomplete") and resultSignature_d == 503)/(intervalsize/1m), 0.01)
by bin(TimeGenerated, intervalsize)
| render timechart
```


## Measure individual queries

In some cases, it can be useful to test individual queries to see how they're performing. To do this, it's important to be able to see how long the search service takes to complete the work, as well as how long it takes to make the round-trip request from the client and back to the client. The diagnostics logs could be used to look up individual operations, but it might be easier to do this all from a REST client.

In the example below, a REST-based search query was executed. Azure AI Search includes in every response the number of milliseconds it takes to complete the query, visible in the Headers tab, in "elapsed-time". Next to Status at the top of the response, you'll find the round-trip duration, in this case, 125 milliseconds (ms). In the results section, the “Headers” tab was chosen. Using these two values, highlighted with a red box in the image below, we see the search service took 21 ms to complete the search query and the entire client round-trip request took 125 ms. By subtracting these two numbers we can determine that it took 104-ms additional time to transmit the search query to the search service and to transfer the search results back to the client.

This technique helps you isolate network latencies from other factors impacting query performance.


## Query rates

One potential reason for your search service to throttle requests is due to the sheer number of queries being performed where volume is captured as queries per second (QPS) or queries per minute (QPM). As your search service receives more QPS, it will typically take longer and longer to respond to those queries until it can no longer keep up, as which it will send back a throttling 503 HTTP response.

The following Kusto query shows query volume as measured in QPM, along with average duration of a query in milliseconds (AvgDurationMS) and the average number of documents (AvgDocCountReturned) returned in each one.

```
AzureDiagnostics
| where OperationName == "Query.Search" and TimeGenerated > ago(1d)
| extend MinuteOfDay = substring(TimeGenerated, 0, 16)
| project MinuteOfDay, DurationMs, Documents_d, IndexName_s
| summarize QPM=count(), AvgDuractionMs=avg(DurationMs), AvgDocCountReturned=avg(Documents_d) by MinuteOfDay
| order by MinuteOfDay desc
| render timechart
```


Tip

To reveal the data behind this chart, remove the line `| render timechart`

and then rerun the query.

## Impact of indexing on queries

An important factor to consider when looking at performance is that indexing uses the same resources as search queries. If you're indexing a large amount of content, you can expect to see latency grow as the service tries to accommodate both workloads.

If queries are slowing down, look at the timing of indexing activity to see if it coincides with query degradation. For example, perhaps an indexer is running a daily or hourly job that correlates with the decreased performance of the search queries.

This section provides a set of queries that can help you visualize the search and indexing rates. For these examples, the time range is set in the query. Be sure to indicate **Set in query** when running the queries in Azure portal.


### Average Query Latency

In the below query, an interval size of 1 minute is used to show the average latency of the search queries. From the chart, we can see that the average latency was low until 5:45pm and lasted until 5:53pm.

```
let intervalsize = 1m;
let _startTime = datetime('2024-02-23 17:40');
let _endTime = datetime('2024-02-23 18:00');
AzureDiagnostics
| where TimeGenerated between(['_startTime']..['_endTime']) // Time range filtering
| summarize AverageQueryLatency = avgif(DurationMs, OperationName in ("Query.Search", "Query.Suggest", "Query.Lookup", "Query.Autocomplete"))
by bin(TimeGenerated, intervalsize)
| render timechart
```


### Average Queries Per Minute (QPM)

The following query looks at the average number of queries per minute to ensure that there wasn't a spike in search requests that might have affected the latency. From the chart, we can see there's some variance, but nothing to indicate a spike in request count.

```
let intervalsize = 1m;
let _startTime = datetime('2024-02-23 17:40');
let _endTime = datetime('2024-02-23 18:00');
AzureDiagnostics
| where TimeGenerated between(['_startTime'] .. ['_endTime']) // Time range filtering
| summarize QueriesPerMinute=bin(countif(OperationName in ("Query.Search", "Query.Suggest", "Query.Lookup", "Query.Autocomplete"))/(intervalsize/1m), 0.01)
by bin(TimeGenerated, intervalsize)
| render timechart
```


### Indexing Operations Per Minute (OPM)

Here we'll look at the number of Indexing operations per minute. From the chart, we can see that a large amount of data was indexed started at 5:42 pm and ended at 5:50pm. This indexing began 3 minutes before the search queries started becoming latent and ended 3 minutes before the search queries were no longer latent.

From this insight, we can see that it took about 3 minutes for the search service to become busy enough for indexing to affect query latency. We can also see that after indexing completed, it took another 3 minutes for the search service to complete all the work from the newly indexed content, and for query latency to resolve.

```
let intervalsize = 1m;
let _startTime = datetime('2024-02-23 17:40');
let _endTime = datetime('2024-02-23 18:00');
AzureDiagnostics
| where TimeGenerated between(['_startTime'] .. ['_endTime']) // Time range filtering
| summarize IndexingOperationsPerSecond=bin(countif(OperationName == "Indexing.Index")/ (intervalsize/1m), 0.01)
by bin(TimeGenerated, intervalsize)
| render timechart
```


## Background service processing

It's common to see occasional spikes in query or indexing latency. Spikes might occur in response to indexing or high query rates, but could also occur during merge operations. Search indexes are stored in chunks - or shards. Periodically, the system merges smaller shards into large shards, which can help optimize service performance. This merge process also cleans up documents that have previously been marked for deletion from the index, resulting in the recovery of storage space.

Merging shards is fast, but also resource intensive and thus has the potential to degrade service performance. If you notice short bursts of query latency, and those bursts coincide with recent changes to indexed content, you can assume the latency is due to shard merge operations.

## Next steps

Review these articles related to analyzing service performance.


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-concept-intro.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-concept-intro -->

# AI enrichment in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, *AI enrichment* refers to integration with [Foundry Tools](/en-us/azure/ai-services/what-are-ai-services) to process content that isn't searchable in its raw form. Through enrichment, analysis and inference are used to create searchable content and structure where none previously existed.

Because Azure AI Search is used for text and vector queries, the purpose of AI enrichment is to improve the utility of your content in search-related scenarios. Raw content must be text or images (you can't enrich vectors), but the output of an enrichment pipeline can be vectorized and indexed in a search index using skills like [Text Split skill](cognitive-search-skill-textsplit) for chunking and [Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding) for vector encoding. For more information about using skills in vector scenarios, see [Integrated data chunking and embedding](vector-search-integrated-vectorization).

AI enrichment is based on [ skills](cognitive-search-working-with-skillsets).

[Built-in skills](cognitive-search-predefined-skills) tap Foundry Tools. They apply the following transformations and processing to raw content:

- Translation and language detection for multilingual search.
- Entity recognition to extract people names, places, and other entities from large chunks of text.
- Key phrase extraction to identify and output important terms.
- Optical character recognition (OCR) to recognize printed and handwritten text in binary files.
- Image analysis to describe image content and output the descriptions as searchable text fields.
- Text embeddings via Azure OpenAI for integrated vectorization.
- Multimodal embeddings via Azure Vision in Foundry Tools for text and image vectorization.

Custom skills run your external code. You can use custom skills for any custom processing you want to include in the pipeline.

AI enrichment is an extension of an [indexer pipeline](search-indexer-overview) that connects to Azure data sources. An enrichment pipeline has all of the components of an indexer pipeline (indexer, data source, index) and a [skillset](cognitive-search-working-with-skillsets) that specifies atomic enrichment steps.

The following diagram shows the progression of AI enrichment:


**Import** is the first step. Here, the indexer connects to a data source and pulls content (documents) into the search service. [Azure Blob Storage](/en-us/azure/storage/blobs/storage-blobs-overview) is the most common resource used in AI enrichment scenarios, but any supported data source can provide content.

**Enrich & Index** covers most of the AI enrichment pipeline:

Enrichment starts when the indexer

and extracts images and text. The type of processing that occurs next depends on your data and the skills you've added to a skillset. Images can be forwarded to[cracks documents](search-indexer-overview#document-cracking)[skills that perform image processing](cognitive-search-concept-image-scenarios). Text content is queued for text and natural language processing. Internally, skills create anthat collects transformations as they occur.[enriched document](cognitive-search-working-with-skillsets#enrichment-tree)Enriched content is generated during skillset execution and is temporary unless you save it. You can enable an

[enrichment cache](enrichment-cache-how-to-configure)to persist skill outputs for reuse in future skillset executions.To get content into a search index, the indexer must have mapping information for sending enriched content to target field.

[Field mappings](search-indexer-field-mappings)(explicit or implicit) set the data path from source data to a search index.[Output field mappings](cognitive-search-output-field-mapping)set the data path from enriched documents to an index.Indexing is the process wherein raw and enriched content is ingested into the physical data structures of a

[search index](search-what-is-an-index)(its files and folders). Lexical analysis and tokenization occur in this step.

**Exploration** is the last step. Output is always a [search index](search-what-is-an-index) that you can query from a client app. Output can optionally be a [knowledge store](knowledge-store-concept-intro) consisting of blobs and tables in Azure Storage that are accessed through data exploration tools or downstream processes. If you're creating a knowledge store, [projections](knowledge-store-projection-overview) determine the data path for enriched content. The same enriched content can appear in both indexes and knowledge stores.

## When to use AI enrichment

Enrichment is useful if raw content is unstructured text, image content, or content that needs language detection and translation. Applying AI through the [built-in skills](cognitive-search-predefined-skills) can unlock this content for full-text search and data science applications.

You can also create [custom skills](cognitive-search-create-custom-skill-example) to provide external processing.
Open-source, third-party, or first-party code can be integrated into the pipeline as a custom skill. Classification models that identify salient characteristics of various document types fall into this category, but any external package that adds value to your content could be used.

### Use-cases for built-in skills

Built-in skills are based on the Foundry Tools APIs: [Azure Vision](/en-us/azure/ai-services/computer-vision/) and [Azure Language](/en-us/azure/ai-services/language-service/overview). Unless your content input is small, you are expected to [attach a billable Microsoft Foundry resource](cognitive-search-attach-cognitive-services) to run larger workloads.

A [skillset](cognitive-search-defining-skillset) that's assembled using built-in skills is well suited for the following application scenarios:

**Image processing**skills include[Optical Character Recognition (OCR)](cognitive-search-skill-ocr)and identification of[visual features](cognitive-search-skill-image-analysis), such as facial detection, image interpretation, image recognition (famous people and landmarks), or attributes like image orientation. These skills create text representations of image content for full-text search in Azure AI Search.**Machine translation**is provided by the[Text Translation](cognitive-search-skill-text-translation)skill, often paired with[language detection](cognitive-search-skill-language-detection)for multi-language solutions.**Natural language processing**analyzes chunks of text. Skills in this category include[Entity Recognition](cognitive-search-skill-entity-recognition-v3),[Sentiment Detection (including opinion mining)](cognitive-search-skill-sentiment-v3), and[Personal Identifiable Information Detection](cognitive-search-skill-pii-detection). With these skills, unstructured text is mapped as searchable and filterable fields in an index.

### Use-cases for custom skills

[Custom skills](cognitive-search-create-custom-skill-example) execute external code that you provide and wrap in the [custom skill web interface](cognitive-search-custom-skill-interface). Several examples of custom skills can be found in the [azure-search-power-skills](https://github.com/Azure-Samples/azure-search-power-skills/blob/main/README.md) GitHub repository.

Custom skills aren’t always complex. For example, if you have an existing package that provides pattern matching or a document classification model, you can wrap it in a custom skill.

## Storing output

In Azure AI Search, an indexer saves the output it creates. A single indexer run can create up to three data structures that contain enriched and indexed output.

| Data store | Required | Location | Description |
|---|---|---|---|
|

[knowledge store](knowledge-store-concept-intro)[multimodal search scenarios](multimodal-search-overview#how-does-multimodal-search-work), you can save extracted images to the knowledge store and reference them at query time, allowing the images to be returned directly to client apps.[enrichment cache](enrichment-cache-how-to-configure)Indexes and knowledge stores are fully independent of each other. While you must attach an index to satisfy indexer requirements, if your sole objective is a knowledge store, you can ignore the index after it's populated.

## Exploring content

After you define and load a [search index](search-what-is-an-index) or [knowledge store](knowledge-store-concept-intro), you can explore its data.

### Query a search index

[Run queries](search-query-overview) to access the enriched content generated by the pipeline. The index is like any other you might create for Azure AI Search: you can supplement text analysis with custom analyzers, invoke fuzzy search queries, add filters, or experiment with scoring profiles to tune search relevance.

### Use data exploration tools on a knowledge store

In Azure Storage, a [knowledge store](knowledge-store-concept-intro) can assume the following forms: a blob container of JSON documents, a blob container of image objects, or tables in Table Storage. You can use [Storage Explorer](/en-us/azure/vs-azure-tools-storage-manage-with-storage-explorer), [Power BI](knowledge-store-connect-power-bi), or any app that connects to Azure Storage to access your content.

A blob container captures enriched documents in their entirety, which is useful if you're creating a feed into other processes.

A table is useful if you need slices of enriched documents, or if you want to include or exclude specific parts of the output. For analysis in Power BI, tables are the recommended data source for data exploration and visualization in Power BI.


## Availability and pricing

AI enrichment is available in regions that offer Foundry Tools. To check the availability of AI enrichment, see the [regions list](search-region-support).

Billing follows a Standard pricing model. Costs associated with built-in skills are incurred when you specify an Azure OpenAI in Foundry Models resource or Foundry resource key in the skillset. There are also costs associated with image extraction, as metered by Azure AI Search. However, text extraction and utility skills aren't billable. For more information, see [How you're charged for Azure AI Search](search-sku-manage-costs#how-youre-charged-for-the-base-service).

## Checklist: A typical workflow

An enrichment pipeline consists of [ indexers](search-indexer-overview) that have

[. Post-indexing, you can query an index to validate your results.](cognitive-search-working-with-skillsets)

*skillsets*Start with a subset of data in a [supported data source](search-indexer-overview#supported-data-sources). Indexer and skillset design is an iterative process. The work goes faster with a small representative data set.

Create a

[data source](/en-us/rest/api/searchservice/data-sources/create)that specifies a connection to your data.[Create a skillset](cognitive-search-defining-skillset). Unless your project is small, you should[attach a Foundry resource](cognitive-search-attach-cognitive-services). If you're[creating a knowledge store](knowledge-store-create-rest), define it within the skillset.[Create an index schema](search-how-to-create-search-index)that defines a search index.[Create and run the indexer](search-howto-create-indexers)to bring all of the previous components together. This step retrieves the data, runs the skillset, and loads the index.An indexer is also where you specify field mappings and output field mappings that set up the data path to a search index.

Optionally,

[enable enrichment caching](enrichment-cache-how-to-configure)in the indexer configuration. This step allows you to reuse existing enrichments later on.[Run queries](search-query-create)to evaluate results or[start a debug session](cognitive-search-how-to-debug-skillset)to work through any skillset issues.

To repeat any of the previous steps, [reset the indexer](search-howto-reindex) before you run it. Alternatively, you can delete and recreate the objects on each run (recommended if you're using the free tier). If you enabled caching, the indexer pulls from the cache if the source data is unchanged and if your edits to the pipeline don't invalidate the cache.
