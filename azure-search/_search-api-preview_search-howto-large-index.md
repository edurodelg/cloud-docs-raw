---
merged_at: 2026-01-25T02:11:58.462011
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-api-preview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-api-preview -->

# Preview features in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article identifies all data plane and control plane features in public preview. This list is helpful for checking feature status. It also explains how to call a preview REST API.

Preview API versions are cumulative and roll up to the next preview. We recommend always using the latest preview APIs for full access to all preview features.

Preview features are removed from this list if they're retired or transition to general availability. For announcements regarding general availability and retirement, see [Service Updates](https://azure.microsoft.com/updates/?product=search) or [What's New](whats-new).

## Data plane preview features

| Feature | Description | Availability |
|---|---|---|
Agentic retrieval |

The pipeline involves one or more [knowledge sources](agentic-knowledge-source-overview#supported-knowledge-sources) within a [knowledge base](agentic-retrieval-how-to-create-knowledge-base), whose [response payload](agentic-retrieval-how-to-retrieve) provides full transparency into the query plan and reference data.

To get started, see [Quickstart: Agentic retrieval](search-get-started-agentic-retrieval) (programmatic) or [Quickstart: Agentic retrieval in the Azure portal](get-started-portal-agentic-retrieval).

[Knowledge Sources (preview)](/en-us/rest/api/searchservice/knowledge-sources?view=rest-searchservice-2025-11-01-preview&preserve-view=true),[Knowledge bases (preview)](/en-us/rest/api/searchservice/knowledge-bases?view=rest-searchservice-2025-11-01-preview&preserve-view=true),[Knowledge Retrieval (preview)](/en-us/rest/api/searchservice/knowledge-retrieval?view=rest-searchservice-2025-11-01-preview&preserve-view=true), and the Azure portal**Purview index configuration**[Create or Update Index (preview)](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Scoring function aggregation**[Create or Update Index (preview)](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Facet aggregations**[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Improved indexer runtime tracking information**[Get Service Statistics (preview)](/en-us/rest/api/searchservice/get-service-statistics/get-service-statistics?view=rest-searchservice-2025-11-01-preview&preserve-view=true)and[Get Status - Indexers (preview)](/en-us/rest/api/searchservice/get-service-statistics/get-service-statistics?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Strict postfiltering for vector queries**`strictPostFilter`

mode to the `vectorFilterMode`

parameter. When specified, filters are applied after the global top-`k`

vector results are identified, ensuring that returned documents are a subset of the unfiltered results.[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Multivector support**[Create or Update Index (preview)](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Document-level access control**[Create or Update Index (preview)](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**GenAI Prompt skill***image verbalization*, using an LLM to describe images and send the description to a searchable field in your index.[Create or Update Skillset (preview)](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**flightingOptIn parameter in a semantic configuration**[Create or Update Index (preview)](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2025-03-01-preview&preserve-view=true)**Facet hierarchies, aggregations, and facet filters**[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-03-01-preview&preserve-view=true)**Query rewrite in the semantic reranker**[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true)[.](cognitive-search-attach-cognitive-services)**Keyless billing for Azure AI skills processing**[Create or Update Skillset (preview)](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Markdown parsing mode**[Create or Update Indexer (preview)](/en-us/rest/api/searchservice/indexers/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Target filters in a hybrid search to just the vector queries**`filterOverride`

parameter provides the behaviors.[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Text Split skill (token chunking)**`unit`

parameter lets you specify token chunking. You can now chunk by token length, setting the length to a value that makes sense for your embedding model. You can also specify the tokenizer and any tokens that shouldn't be split during data chunking.[Create or Update Skillset (preview)](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Azure Vision multimodal embedding skill**[Create or Update Skillset (preview)](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Azure Machine Learning (AML) skill**[Create or Update Skillset (preview)](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Incremental enrichment cache**[Create or Update Indexer (preview)](/en-us/rest/api/searchservice/indexers/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**Azure Files indexer**[Azure Files](https://azure.microsoft.com/services/storage/files/).[Create or Update Data Source (preview)](/en-us/rest/api/searchservice/data-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**SharePoint indexer**[Sign up](https://aka.ms/azure-cognitive-search/indexer-preview)to enable the feature.[Create or Update Data Source (preview)](/en-us/rest/api/searchservice/data-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)or the Azure portal.**MySQL indexer**[Sign up](https://aka.ms/azure-cognitive-search/indexer-preview)to enable the feature.[Create or Update Data Source (preview)](/en-us/rest/api/searchservice/data-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true),[.NET SDK 11.2.1](/en-us/dotnet/api/azure.search.documents.indexes.models.searchindexerdatasourcetype.mysql), and Azure portal**Azure Cosmos DB for MongoDB indexer**[Sign up](https://aka.ms/azure-cognitive-search/indexer-preview)to enable the feature.[Create or Update Data Source (preview)](/en-us/rest/api/searchservice/data-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)or the Azure portal.**Azure Cosmos DB for Apache Gremlin indexer**[Sign up](https://aka.ms/azure-cognitive-search/indexer-preview)to enable the feature.[Create or Update Data Source (preview)](/en-us/rest/api/searchservice/data-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true).**Native blob soft delete**[Create or Update Data Source (preview)](/en-us/rest/api/searchservice/data-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true).**Reset Documents**[Reset Documents (preview)](/en-us/rest/api/searchservice/indexers/reset-docs?view=rest-searchservice-2025-11-01-preview&preserve-view=true).**speller**[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true).**featuresMode parameter**[custom scoring solutions](https://github.com/Azure-Samples/search-ranking-tutorial).[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**vectorQueries.threshold parameter**[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**hybridSearch.maxTextRecallSize and countAndFacetMode parameters**[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true)**moreLikeThis**[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true)## Control plane preview features

Currently, there are no control plane features in preview.

## Preview features in Azure SDKs

Preview features in Azure SDKs are available through preview packages. To determine which preview features are available in a specific package version, see the SDK's change log:

[Change log for Azure SDK for .NET](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/search/Azure.Search.Documents/CHANGELOG.md)[Change log for Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/CHANGELOG.md)[Change log for Azure SDK for JavaScript](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/CHANGELOG.md)[Change log for Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/search/azure-search-documents/CHANGELOG.md).

## Using preview features

You can access experimental features through preview REST API versions or preview SDK packages. Some features might also be available in the Azure portal. For more information about availability, see [Data plane preview features](#data-plane-preview-features) and [Control plane preview features](#control-plane-preview-features).

The following statements apply to preview features:

- Preview features are available under
[Supplemental Terms of Use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/), without a service level agreement. - Preview features might undergo breaking changes if a redesign is required.
- Sometimes preview features don't make it into a GA release.

If you write code against a preview API, you should prepare to upgrade that code to newer API versions when they roll out. We maintain an [Upgrade REST APIs](search-api-migration) document to make that step easier.

## How to call a preview REST API

Preview REST APIs are accessed through the api-version parameter on the URI. Older previews are still operational but become stale over time and aren't updated with new features or bug fixes.

For data plane operations on content, is the most recent preview version. The following example shows the syntax for

`2025-11-01-preview`

[Indexes GET (preview)](/en-us/rest/api/searchservice/indexes/get?view=rest-searchservice-2025-11-01-preview&preserve-view=true):

```
GET {endpoint}/indexes('{indexName}')?api-version=2025-11-01-Preview
```


For management operations on the search service, is the most recent preview version. The following example shows the syntax for Update Service 2025-05-01-preview version.

`2025-05-01-preview`

```
PATCH https://management.azure.com/subscriptions/subid/resourceGroups/rg1/providers/Microsoft.Search/searchServices/mysearchservice?api-version=2025-05-01-preview
{
"tags": {
"app-name": "My e-commerce app",
"new-tag": "Adding a new tag"
},
"properties": {
"replicaCount": 2
}
}
```


---

<!-- DOCUMENTO FUSIONADO: search-howto-large-index.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-howto-large-index -->

# Index large data sets in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you need to index large or complex data sets in your search solution, this article explores strategies to accommodate long-running processes on Azure AI Search.

These strategies assume familiarity with the [two basic approaches for importing data](search-what-is-data-import): *pushing* data into an index, or *pulling* in data from a supported data source using a [search indexer](search-indexer-overview). If your scenario involves computationally intensive [AI enrichment](cognitive-search-concept-intro), then indexers are required, given the skillset dependency on indexers.

This article complements [Tips for better performance](search-performance-tips), which offers best practices on index and query design. A well-designed index that includes only the fields and attributes you need is an important prerequisite for large-scale indexing.

We recommend using a search service created after April 3, 2024 for [higher storage per partition](search-limits-quotas-capacity#service-limits). Older services can also be [upgraded to benefit from higher partition storage](search-how-to-upgrade).

Note

The strategies described in this article assume a single large data source. If your solution requires indexing from multiple data sources, see [Index multiple data sources in Azure AI Search](/en-us/samples/azure-samples/azure-search-dotnet-scale/multiple-data-sources/) for a recommended approach.

## Index data using the push APIs

*Push* APIs, such as the [Documents Index REST API](/en-us/rest/api/searchservice/documents) or the [IndexDocuments method (Azure SDK for .NET)](/en-us/dotnet/api/azure.search.documents.searchclient.indexdocuments), are the most prevalent form of indexing in Azure AI Search. For solutions that use a push API, the strategy for long-running indexing has one or both of the following components:

- Batching documents
- Managing threads

### Batch multiple documents per request

A simple mechanism for indexing a large quantity of data is to submit multiple documents or records in a single request. As long as the entire payload is under 16 MB, a request can handle up to 1,000 documents in a bulk upload operation. These limits apply whether you're using the [Documents Index REST API](/en-us/rest/api/searchservice/documents) or the [IndexDocuments method](/en-us/dotnet/api/azure.search.documents.searchclient.indexdocuments) in the .NET SDK. Using either API, you can package 1,000 documents in the body of each request.

Batching documents significantly shortens the amount of time it takes to work through a large data volume. Determining the optimal batch size for your data is a key component of optimizing indexing speeds. The two primary factors influencing the optimal batch size are:

- The schema of your index
- The size of your data

Because the optimal batch size depends on your index and your data, the best approach is to test different batch sizes to determine which one results in the fastest indexing speeds for your scenario. For sample code to test batch sizes using the .NET SDK, see [Tutorial: Optimize indexing with the push API](tutorial-optimize-indexing-push-api).

### Manage threads and a retry strategy

Indexers have built-in thread management, but when you're using the push APIs, your application code needs to manage threads. Make sure there are sufficient threads to make full use of the available capacity, especially if you recently [upgraded your service](search-how-to-upgrade), [switched to a higher pricing tier](search-capacity-planning#change-your-pricing-tier), or [increased partitions](search-capacity-planning#add-or-remove-partitions-and-replicas).

[Increase the number of concurrent threads](tutorial-optimize-indexing-push-api#use-multiple-threadsworkers)in your client code.As you ramp up the requests hitting the search service, you might encounter

[HTTP status codes](/en-us/rest/api/searchservice/http-status-codes)indicating the request didn't fully succeed. During indexing, two common HTTP status codes are:**503 Service Unavailable**: This error means that the system is under heavy load and your request can't be processed at this time.**207 Multi-Status**: This error means that some documents succeeded, but at least one failed.

To handle failures, requests should be retried using an

[exponential backoff retry strategy](/en-us/dotnet/architecture/microservices/implement-resilient-applications/implement-retries-exponential-backoff).

The Azure .NET SDK automatically retries 503s and other failed requests, but you need to implement your own logic to retry 207s. Open-source tools such as [Polly](https://github.com/App-vNext/Polly) can also be used to implement a retry strategy.

## Use indexers and the pull APIs

[Indexers](search-indexer-overview) have several capabilities that are useful for long-running processes:

- Batching documents
- Parallel indexing over partitioned data
- Scheduling and change detection for indexing only new and changed documents over time

Indexer schedules can resume processing at the last known stopping point. If data isn't fully indexed within the processing window, the indexer picks up wherever it left off on the next run, assuming you're using a data source that provides change detection.

Partitioning data into smaller individual data sources enables parallel processing. You can break up source data, such as into multiple containers in Azure Blob Storage, [create a data source](/en-us/rest/api/searchservice/data-sources/create) for each partition, and then [run the indexers in parallel](search-howto-run-reset-indexers), subject to the number of search units of your search service.

### Check indexer batch size

As with the push API, indexers allow you to configure the number of items per batch. For indexers based on the [Create Indexer REST API](/en-us/rest/api/searchservice/indexers/create), you can set the `batchSize`

argument to customize this setting to better match the characteristics of your data.

Default batch sizes are data-source specific. Azure SQL Database and Azure Cosmos DB have a default batch size of 1,000. In contrast, Azure Blob and SharePoint (Preview) indexing sets batch size at 10 documents in recognition of the larger average document size.

### Schedule indexers for long-running processes

Indexer scheduling is an important mechanism for processing large data sets and for accommodating slow-running processes like image analysis in an enrichment pipeline.

Typically, indexer processing runs within a two-hour window. If the indexing workload takes days rather than hours to complete, you can put the indexer on a consecutive, recurring schedule that starts every two hours. Assuming the data source has [change tracking enabled](search-howto-create-indexers#change-detection-and-internal-state), the indexer resumes processing where it last left off. At this cadence, an indexer can work its way through a document backlog over a series of days until all unprocessed documents are processed. This pattern is especially important during the initial run or when indexing large blob containers, where the blob listing phase alone can take multiple hours or days. During this time, the indexer would show no blobs being processed, but unless an error is reported, it is likely still iterating through the blob list. Document processing and enrichment begin only after this phase completes, and this behavior is expected.

```
{
"dataSourceName" : "hotels-ds",
"targetIndexName" : "hotels-idx",
"schedule" : { "interval" : "PT2H", "startTime" : "2024-01-01T00:00:00Z" }
}
```


When there are no longer any new or updated documents in the data source, indexer execution history reports `0/0`

documents processed, and no processing occurs.

For more information about setting schedules, see [Create Indexer REST API](/en-us/rest/api/searchservice/indexers/create) or see [Schedule indexers for Azure AI Search](search-howto-schedule-indexers).

Note

Some indexers that run on an older runtime architecture have a 24-hour rather than 2-hour maximum processing window. The two-hour limit is for newer content processors that run in an [internally managed multitenant environment](search-howto-run-reset-indexers#indexer-execution-environment). Whenever possible, Azure AI Search tries to offload indexer and skillset processing to the multitenant environment. If the indexer can't be migrated, it runs in the private environment and it can run for as long as 24 hours. If you're scheduling an indexer that exhibits these characteristics, assume a 24-hour processing window.

### Run indexers in parallel

If you partition your data, you can create multiple indexer-data-source combinations that pull from each data source and write to the same search index. Because each indexer is distinct, you can run them at the same time, populating a search index more quickly than if you ran them sequentially.

Make sure you have sufficient capacity. One search unit in your service can run one indexer at any given time. Creating multiple indexers is only useful if they can run in parallel.

The number of indexing jobs that can run simultaneously varies for text-based and skills-based indexing. For more information, see [Indexer execution](search-howto-run-reset-indexers#indexer-execution).

If your data source is an [Azure Blob Storage container](/en-us/azure/storage/blobs/storage-blobs-introduction#containers) or [Azure Data Lake Storage Gen 2](/en-us/azure/storage/blobs/storage-blobs-introduction#about-azure-data-lake-storage-gen2), enumerating a large number of blobs can take a long time (even hours) until this operation is completed. As a result, your indexer's *documents succeeded* count doesn't appear to increase during that time and it might seem it's not making any progress, when it is. If you would like document processing to go faster for a large number of blobs, consider partitioning your data into multiple containers and create parallel indexers pointing to a single index.

Sign in to the

[Azure portal](https://portal.azure.com)and check the number of search units used by your search service. Select**Settings**>**Scale**to view the number at the top of the page. The number of indexers that run in parallel is approximately equal to the number of search units.Partition source data among multiple containers or multiple virtual folders inside the same container.

Create multiple

[data sources](/en-us/rest/api/searchservice/data-sources/create), one for each partition, paired to its own[indexer](/en-us/rest/api/searchservice/indexers/create).Specify the same target search index in each indexer.

Schedule the indexers.

Review indexer status and execution history for confirmation.


There are some risks associated with parallel indexing. First, recall that indexing doesn't run in the background, increasing the likelihood that queries are throttled or dropped.

Second, Azure AI Search doesn't lock the index for updates. Concurrent writes are managed, invoking a retry if a particular write doesn't succeed on first attempt, but you might notice an increase in indexing failures.

Although multiple indexer-data-source sets can target the same index, be careful of indexer runs that can overwrite existing values in the index. If a second indexer-data-source targets the same documents and fields, any values from the first run are overwritten. Field values are replaced in full; an indexer can't merge values from multiple runs into the same field.

## Index big data on Spark

If you have a big data architecture and your data is on a Spark cluster, we recommend [SynapseML for loading and indexing data](search-synapseml-cognitive-services). The tutorial includes steps for calling Foundry Tools for AI enrichment, but you can also use the AzureSearchWriter API for text indexing.
