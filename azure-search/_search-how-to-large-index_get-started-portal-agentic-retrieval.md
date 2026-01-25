---
merged_at: 2026-01-25T02:11:58.463251
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-how-to-large-index.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-large-index -->

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


---

<!-- DOCUMENTO FUSIONADO: get-started-portal-agentic-retrieval.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/get-started-portal-agentic-retrieval -->

# Quickstart: Agentic retrieval in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In this quickstart, you use [agentic retrieval](agentic-retrieval-overview) in the Azure portal to create a conversational search experience powered by documents indexed in Azure AI Search and large language models (LLMs) from Azure OpenAI in Foundry Models.

The portal guides you through the process of creating the following objects:

A

*knowledge source*that references a container in Azure Blob Storage. When you create a blob knowledge source, Azure AI Search automatically generates an index and other pipeline objects to ingest and enrich your content for agentic retrieval.A

*knowledge base*that uses agentic retrieval to infer the underlying information need, plan and execute subqueries, and formulate a natural-language answer using the optional answer synthesis output mode.

Afterwards, you test the knowledge base by submitting a complex query that requires information from multiple documents and reviewing the synthesized answer.

Important

The portal now uses the 2025-11-01-preview REST APIs for knowledge sources and knowledge bases. If you previously created agentic retrieval objects in the portal, those objects use the 2025-08-01-preview and are subject to breaking changes. We recommend that you [migrate existing objects and code](agentic-retrieval-how-to-migrate) as soon as possible.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An

[Azure AI Search service](search-create-service-portal)in any[region that provides agentic retrieval](search-region-support).A

[Microsoft Foundry project](/en-us/azure/ai-foundry/how-to/create-projects)and resource. When you create a project, the resource is automatically created.For text-to-vector conversion, an embedding model

[deployed to your project](/en-us/azure/ai-foundry/how-to/deploy-models-openai). You can use any`text-embedding`

model, such as`text-embedding-3-large`

.For query planning and answer generation, an LLM

[deployed to your project](/en-us/azure/ai-foundry/how-to/deploy-models-openai). You can use any[portal-supported LLM](#supported-llms).

### Supported LLMs

Although agentic retrieval [programmatically supports several LLMs](agentic-retrieval-how-to-create-knowledge-base#supported-models), the portal currently supports the following LLMs:

`gpt-4o`

`gpt-4o-mini`

`gpt-5`

`gpt-5-mini`

`gpt-5-nano`


## Configure access

Before you begin, make sure you have permissions to access content and operations. We recommend Microsoft Entra ID for authentication and role-based access for authorization. You must be an **Owner** or **User Access Administrator** to assign roles. If roles aren't feasible, use [key-based authentication](search-security-api-keys) instead.

To configure access for this quickstart, select each of the following tabs.

Azure AI Search provides the agentic retrieval pipeline. Configure access for yourself and your search service to read and write data, interact with other Azure services, and run the pipeline.

On your Azure AI Search service:

[Assign the following roles](search-security-rbac)to yourself.**Search Service Contributor****Search Index Data Contributor****Search Index Data Reader**


Important

Agentic retrieval has two token-based billing models:

- Billing from Azure AI Search for agentic retrieval.
- Billing from Azure OpenAI for query planning and answer synthesis.

For more information, see [Availability and pricing of agentic retrieval](agentic-retrieval-overview#availability-and-pricing).

## Prepare sample data

This quickstart uses sample JSON documents from NASA's Earth at Night e-book, but you can also use your own files. The documents describe general science topics and images of Earth at night as observed from space.

To prepare the sample data for this quickstart:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your Azure Blob Storage account.From the left pane, select

**Data storage**>**Containers**.Create a container named

**earth-at-night-data**.Upload the

[sample JSON documents](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/nasa-e-book/earth-at-night-json)to the container.

## Create a knowledge source

A knowledge source is a reusable reference to your source data. In this section, you create a [blob knowledge source](agentic-knowledge-source-how-to-blob), which triggers the creation of a *data source*, *skillset*, *index*, and *indexer* to automate data indexing and enrichment. You review these objects in a later section.

You also configure a *vectorizer*, which uses your deployed embedding model to convert text into vectors and match documents based on semantic similarity. The vectorizer, vector fields, and vectors will be added to the auto-generated index.

To create the knowledge source for this quickstart:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Agentic retrieval**>**Knowledge sources**.Select

**Add knowledge source**>**Add knowledge source**.Select

**Azure blob**.Enter

**earth-at-night-ks**for the name, and then select your subscription, storage account, and container with the sample data.Select the

**Authenticate using managed identity**checkbox. Leave the identity type as**System-assigned**.Select

**Add vectorizer**.Select

**Azure AI Foundry**for the kind, and then select your subscription, project, and embedding model deployment.Select

**System assigned identity**for the authentication type.Create the knowledge source.


## Create a knowledge base

A knowledge base uses your knowledge source and deployed LLM to orchestrate agentic retrieval. When a user submits a complex query, the LLM generates subqueries that are sent simultaneously to your knowledge source. Azure AI Search then semantically ranks the results for relevance and combines the best results into a single, unified response.

The output mode determines how the knowledge base formulates answers. You can either use extractive data for verbatim content or [answer synthesis](agentic-retrieval-how-to-answer-synthesis) for natural-language answer generation. By default, the portal uses answer synthesis.

To create the knowledge base for this quickstart:

From the left pane, select

**Agentic retrieval**>**Knowledge bases**.Select

**Add knowledge base**>**Add knowledge base**.Enter

**earth-at-night-kb**for the name.Under

**Chat completion model**, select**Add model deployment**.Select

**Azure AI Foundry**for the kind, and then select your subscription, project, and LLM deployment.Select

**System assigned identity**for the authentication type.Save the model deployment.

Under

**Knowledge sources**, select**earth-at-night-ks**.Create the knowledge base.


## Test agentic retrieval

The portal provides a chat playground where you can submit `retrieve`

requests to the knowledge base, whose responses include references to your knowledge sources and debug information about the retrieval process.

To query the knowledge base:

Use the chat box to send the following query.

`Why do suburban belts display larger December brightening than urban cores even though absolute light levels are higher downtown? Why is the Phoenix nighttime street grid is so sharply visible from space, whereas large stretches of the interstate between midwestern cities remain comparatively dim?`

Review the synthesized, citation-backed answer, which should be similar to the following example.

`Suburban belts show larger December brightening in satellite nighttime lights than urban cores mainly because of relative (percentage) change effects and differences in how light is used and distributed. Areas with lower baseline light (suburbs, residential streets) can increase lighting use or reflect more light in winter and so show a bigger percent change, while bright urban cores are already near sensor saturation so their relative increase is small. The retrieved material explains that brightest lights are generally the most urbanized but not necessarily the most populated, and that poor or low‑light areas can have large populations but low availability or use of electric lights; thus lower‑light suburbs can exhibit larger relative changes when seasonal lighting rises.`

Select the debug icon to review the activity log, which should be similar to the following JSON.

`[ { "type": "modelQueryPlanning", "id": 0, "inputTokens": 1518, "outputTokens": 284, "elapsedMs": 3001 }, { "type": "azureBlob", "id": 1, "knowledgeSourceName": "earth-at-night-ks", "queryTime": "2025-12-12T18:54:28.792Z", "count": 1, "elapsedMs": 456, "azureBlobArguments": { "search": "causes of December brightening in satellite nighttime lights suburban vs urban cores" } }, { "type": "azureBlob", "id": 2, "knowledgeSourceName": "earth-at-night-ks", "queryTime": "2025-12-12T18:54:29.389Z", "count": 3, "elapsedMs": 596, "azureBlobArguments": { "search": "factors affecting seasonal variation in nighttime lights December winter brightening suburban belts urban cores" } }, { "type": "azureBlob", "id": 3, "knowledgeSourceName": "earth-at-night-ks", "queryTime": "2025-12-12T18:54:29.862Z", "count": 6, "elapsedMs": 472, "azureBlobArguments": { "search": "why is Phoenix street grid highly visible at night from space compared to dim interstates in the Midwest reasons lighting patterns road lighting urban form" } }, { "type": "agenticReasoning", "id": 4, "retrievalReasoningEffort": { "kind": "low" }, "reasoningTokens": 111243 }, { "type": "modelAnswerSynthesis", "id": 5, "inputTokens": 7514, "outputTokens": 1058, "elapsedMs": 12334 } ]`

The activity log offers insight into the steps taken during retrieval, including query planning and execution, semantic ranking, and answer synthesis. For more information, see

[Review the activity array](agentic-retrieval-how-to-retrieve#review-the-activity-array).

## Review the created objects

Azure AI Search automatically generates a data source, skillset, index, and indexer for each blob knowledge source. These objects form an end-to-end pipeline for data ingestion, enrichment, chunking, and vectorization. You can review these objects to learn how your data is processed for agentic retrieval.

To review the auto-generated objects:

From the left pane, select

**Search management**.Check the data source to verify the connection to your blob storage container.

Check the skillset to see how your content is chunked and vectorized using your embedding model.

Check the index to see how your content is indexed and exposed for retrieval, including which fields are searchable and filterable and which fields store vectors for similarity search.

Check the indexer for success or failure messages. Connection or quota errors appear here.


## Clean up resources

When you work in your own subscription, it's a good idea to finish a project by determining whether you still need the resources you created. Resources that are left running can cost you money.

In the Azure portal, you can manage your Azure AI Search, Azure Blob Storage, and Foundry resources by selecting **All resources** or **Resource groups** from the left pane.

You can also delete the knowledge source and knowledge base on their respective portal pages. When you delete the knowledge source, the portal prompts you to delete the associated data source, skillset, index, and indexer.
