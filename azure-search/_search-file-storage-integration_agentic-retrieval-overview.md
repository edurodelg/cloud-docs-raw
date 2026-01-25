---
merged_at: 2026-01-25T02:11:58.476175
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-file-storage-integration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-file-storage-integration -->

# Index data from Azure Files

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Azure Files indexer is currently in public preview under [Supplemental Terms of Use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). Use a [preview REST API](/en-us/rest/api/searchservice/search-service-api-versions#preview-versions) to create the indexer data source.

In this article, learn how to configure an [ indexer](search-indexer-overview) that imports content from Azure Files and makes it searchable in Azure AI Search. Inputs to the indexer are your files in a single share. Output is a search index with searchable content and metadata stored in individual fields.

To configure and run the indexer, you can use:

[Search Service preview REST APIs](/en-us/rest/api/searchservice), any preview version.- An Azure SDK package, any version.
in the Azure portal.**Import data**wizardin the Azure portal.**Import data (new)**wizard

## Prerequisites

[Azure Files](/en-us/azure/storage/files/storage-how-to-use-files-portal), Transaction Optimized tier.An

[SMB file share](/en-us/azure/storage/files/files-smb-protocol)providing the source content.[NFS shares](/en-us/azure/storage/files/files-nfs-protocol#support-for-azure-storage-features)are not supported.Files containing text. If you have binary data, you can include

[AI enrichment](cognitive-search-concept-intro)for image analysis.Read permissions on Azure Storage. A "full access" connection string includes a key that grants access to the content.

Use a

[REST client](search-get-started-text)to formulate REST calls similar to the ones shown in this article.

## Supported tasks

You can use this indexer for the following tasks:

**Data indexing and incremental indexing:**The indexer can index files and associated metadata from tables. It detects new and updated files and metadata through built-in change detection. You can configure data refresh on a schedule or on demand.**Deletion detection:**The indexer can[detect deletions through custom metadata](search-how-to-index-azure-blob-changed-deleted).**Applied AI through skillsets:**[Skillsets](cognitive-search-concept-intro)are fully supported by the indexer. This includes key features like[integrated vectorization](vector-search-integrated-vectorization)that adds data chunking and embedding steps.**Parsing modes:**The indexer supports[JSON parsing modes](search-how-to-index-azure-blob-json)if you want to parse JSON arrays or lines into individual search documents. It also supports[Markdown parsing mode](search-how-to-index-azure-blob-markdown).**Compatibility with other features:**The indexer is designed to work seamlessly with other indexer features, such as[debug sessions](cognitive-search-debug-session),[indexer cache for incremental enrichments](enrichment-cache-how-to-configure), and[knowledge store](knowledge-store-concept-intro).

## Supported document formats

The Azure Files indexer can extract text from the following document formats:

- CSV (see
[Indexing CSV blobs](search-how-to-index-azure-blob-csv)) - EML
- EPUB
- GZ
- HTML
- JSON (see
[Indexing JSON blobs](search-how-to-index-azure-blob-json)) - KML (XML for geographic representations)
- Markdown
- Microsoft Office formats: DOCX/DOC/DOCM, XLSX/XLS/XLSM, PPTX/PPT/PPTM, MSG (Outlook emails), XML (both 2003 and 2006 WORD XML)
- Open Document formats: ODT, ODS, ODP
- Plain text files (see also
[Indexing plain text](search-how-to-index-azure-blob-plaintext)) - RTF
- XML
- ZIP

## How Azure Files are indexed

By default, most files are indexed as a single search document in the index, including files with structured content, such as JSON or CSV, which are indexed as a single chunk of text.

A compound or embedded document (such as a ZIP archive, a Word document with embedded Outlook email containing attachments, or an .MSG file with attachments) is also indexed as a single document. For example, all images extracted from the attachments of an .MSG file will be returned in the normalized_images field. If you have images, consider adding [AI enrichment](cognitive-search-concept-intro) to get more search utility from that content.

Textual content of a document is extracted into a string field named "content". You can also extract standard and user-defined metadata.

## Define the data source

The data source definition specifies the data to index, credentials, and policies for identifying changes in the data. A data source is defined as an independent resource so that it can be used by multiple indexers.

You can use 2020-06-30-preview or later for "type": `"azurefile"`

. We recommend the latest preview API.

[Create a data source](/en-us/rest/api/searchservice/indexers/create?view=rest-searchservice-2024-05-01-preview&preserve-view=true)to set its definition, using a preview API for "type":`"azurefile"`

.`POST /datasources?api-version=2024-05-01-preview { "name" : "my-file-datasource", "type" : "azurefile", "credentials" : { "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<account name>;AccountKey=<account key>;" }, "container" : { "name" : "my-file-share", "query" : "<optional-directory-name>" } }`

Set "type" to

`"azurefile"`

(required).Set "credentials" to an Azure Storage connection string. The next section describes the supported formats.

Set "container" to the root file share, and use "query" to specify any subfolders.


A data source definition can also include [soft deletion policies](search-how-to-index-azure-blob-changed-deleted), if you want the indexer to delete a search document when the source document is flagged for deletion.

### Supported credentials and connection strings

Indexers can connect to a file share using the following connections.

| Full access storage account connection string |
|---|
`{ "connectionString" : "DefaultEndpointsProtocol=https;AccountName=<your storage account>;AccountKey=<your account key>;" }` |
You can get the connection string from the Storage account page in Azure portal by selecting Access keys in the left pane. Make sure to select a full connection string and not just a key. |

## Add search fields to an index

In the [search index](search-what-is-an-index), add fields to accept the content and metadata of your Azure files.

[Create or update an index](/en-us/rest/api/searchservice/indexes/create-or-update)to define search fields that will store file content and metadata.`POST /indexes?api-version=2025-09-01 { "name" : "my-search-index", "fields": [ { "name": "ID", "type": "Edm.String", "key": true, "searchable": false }, { "name": "content", "type": "Edm.String", "searchable": true, "filterable": false }, { "name": "metadata_storage_name", "type": "Edm.String", "searchable": false, "filterable": true, "sortable": true }, { "name": "metadata_storage_path", "type": "Edm.String", "searchable": false, "filterable": true, "sortable": true }, { "name": "metadata_storage_size", "type": "Edm.Int64", "searchable": false, "filterable": true, "sortable": true }, { "name": "metadata_storage_content_type", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true } ] }`

Create a document key field ("key": true). For blob content, the best candidates are metadata properties. Metadata properties often include characters, such as

`/`

and`-`

, that are invalid for document keys. The indexer automatically encodes the key metadata property, with no configuration or field mapping required.(default) full path to the object or file`metadata_storage_path`

usable only if names are unique`metadata_storage_name`

A custom metadata property that you add to blobs. This option requires that your blob upload process adds that metadata property to all blobs. Since the key is a required property, any blobs that are missing a value will fail to be indexed. If you use a custom metadata property as a key, avoid making changes to that property. Indexers will add duplicate documents for the same blob if the key property changes.


Add a "content" field to store extracted text from each file through the blob's "content" property. You aren't required to use this name, but doing so lets you take advantage of implicit field mappings.

Add fields for standard metadata properties. In file indexing, the standard metadata properties are the same as blob metadata properties. The Azure Files indexer automatically creates internal field mappings for these properties that converts hyphenated property names to underscored property names. You still have to add the fields you want to use the index definition, but you can omit creating field mappings in the data source.

**metadata_storage_name**(`Edm.String`

) - the file name. For example, if you have a file /my-share/my-folder/subfolder/resume.pdf, the value of this field is`resume.pdf`

.**metadata_storage_path**(`Edm.String`

) - the full URI of the file, including the storage account. For example,`https://myaccount.file.core.windows.net/my-share/my-folder/subfolder/resume.pdf`

**metadata_storage_content_type**(`Edm.String`

) - content type as specified by the code you used to upload the file. For example,`application/octet-stream`

.**metadata_storage_last_modified**(`Edm.DateTimeOffset`

) - last modified timestamp for the file. Azure AI Search uses this timestamp to identify changed files, to avoid reindexing everything after the initial indexing.**metadata_storage_size**(`Edm.Int64`

) - file size in bytes.**metadata_storage_content_md5**(`Edm.String`

) - MD5 hash of the file content, if available.**metadata_storage_sas_token**(`Edm.String`

) - A temporary SAS token that can be used by[custom skills](cognitive-search-custom-skill-interface)to get access to the file. This token shouldn't be stored for later use as it might expire.


## Configure and run the Azure Files indexer

Once the index and data source have been created, you're ready to create the indexer. Indexer configuration specifies the inputs, parameters, and properties controlling run time behaviors.

[Create or update an indexer](/en-us/rest/api/searchservice/indexers/create-or-update)by giving it a name and referencing the data source and target index:`POST /indexers?api-version=2025-09-01 { "name" : "my-file-indexer", "dataSourceName" : "my-file-datasource", "targetIndexName" : "my-search-index", "parameters": { "batchSize": null, "maxFailedItems": null, "maxFailedItemsPerBatch": null, "configuration": { "indexedFileNameExtensions" : ".pdf,.docx", "excludedFileNameExtensions" : ".png,.jpeg" } }, "schedule" : { }, "fieldMappings" : [ ] }`

In the optional "configuration" section, provide any inclusion or exclusion criteria. If left unspecified, all files in the file share are retrieved.

If both

`indexedFileNameExtensions`

and`excludedFileNameExtensions`

parameters are present, Azure AI Search first looks at`indexedFileNameExtensions`

, then at`excludedFileNameExtensions`

. If the same file extension is present in both lists, it will be excluded from indexing.[Specify field mappings](search-indexer-field-mappings)if there are differences in field name or type, or if you need multiple versions of a source field in the search index.In file indexing, you can often omit field mappings because the indexer has built-in support for mapping the "content" and metadata properties to similarly named and typed fields in an index. For metadata properties, the indexer will automatically replace hyphens

`-`

with underscores in the search index.See

[Create an indexer](search-howto-create-indexers)for more information about other properties.

An indexer runs automatically when it's created. You can prevent this by setting "disabled" to true. To control indexer execution, [run an indexer on demand](search-howto-run-reset-indexers) or [put it on a schedule](search-howto-schedule-indexers).

## Check indexer status

To monitor the indexer status and execution history, send a [Get Indexer Status](/en-us/rest/api/searchservice/indexers/get-status) request:

```
GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
```


The response includes status and the number of items processed. It should look similar to the following example:

```
{
"status":"running",
"lastResult": {
"status":"success",
"errorMessage":null,
"startTime":"2022-02-21T00:23:24.957Z",
"endTime":"2022-02-21T00:36:47.752Z",
"errors":[],
"itemsProcessed":1599501,
"itemsFailed":0,
"initialTrackingState":null,
"finalTrackingState":null
},
"executionHistory":
[
{
"status":"success",
"errorMessage":null,
"startTime":"2022-02-21T00:23:24.957Z",
"endTime":"2022-02-21T00:36:47.752Z",
"errors":[],
"itemsProcessed":1599501,
"itemsFailed":0,
"initialTrackingState":null,
"finalTrackingState":null
},
... earlier history items
]
}
```


Execution history contains up to 50 of the most recently completed executions, which are sorted in the reverse chronological order so that the latest execution comes first.

## Next steps

You can now [run the indexer](search-howto-run-reset-indexers), [monitor status](search-monitor-indexers), or [schedule indexer execution](search-howto-schedule-indexers). The following articles apply to indexers that pull content from Azure Storage:


---

<!-- DOCUMENTO FUSIONADO: agentic-retrieval-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-overview -->

# Agentic retrieval in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

What is agentic retrieval? In Azure AI Search, *agentic retrieval* is a new multi-query pipeline designed for complex questions posed by users or agents in chat and copilot apps. It's intended for [Retrieval Augmented Generation (RAG)](retrieval-augmented-generation-overview) patterns and agent-to-agent workflows.

Here's what it does:

Uses a large language model (LLM) to break down a complex query into smaller, focused subqueries for better coverage over your indexed content. Subqueries can include chat history for extra context.

Runs subqueries in parallel. Each subquery is semantically reranked to promote the most relevant matches.

Combines the best results into a unified response that an LLM can use to generate answers with your proprietary content.

The response is modular yet comprehensive in how it also includes a query plan and source documents. You can choose to use just the search results as grounding data, or invoke the LLM to formulate an answer.


This high-performance pipeline helps you generate high quality grounding data (or an answer) for your chat application, with the ability to answer complex questions quickly.

Programmatically, agentic retrieval is supported through a new [Knowledge Base object](/en-us/rest/api/searchservice/knowledge-bases?view=rest-searchservice-2025-11-01-preview&preserve-view=true) in the 2025-11-01-preview and in Azure SDK preview packages that provide the feature. A knowledge base's retrieval response is designed for downstream consumption by other agents and chat apps.

## Why use agentic retrieval

There are two use cases for agentic retrieval. First, it's the basis of the [Foundry IQ experience](/en-us/azure/ai-foundry/agents/how-to/tools/knowledge-retrieval) in the Microsoft Foundry (new) portal. It provides the knowledge layer for agent solutions in Microsoft Foundry. Second, it's the basis for custom agentic solutions that you create using the Azure AI Search APIs.

You should use agentic retrieval when you want to provide agents and apps with the most relevant content for answering harder questions, leveraging chat context and your proprietary content.

The *agentic* aspect is a reasoning step in query planning processing that's performed by a supported large language model (LLM) that you provide. The LLM analyzes the entire chat thread to identify the underlying information need. Instead of a single, catch-all query, the LLM breaks down compound questions into focused subqueries based on: user questions, chat history, and parameters on the request. The subqueries target your indexed documents (plain text and vectors) in Azure AI Search. This hybrid approach ensures you surface both keyword matches and semantic similarities at once, dramatically improving recall.

The *retrieval* component is the ability to run subqueries simultaneously, merge results, semantically rank results, and return a three-part response that includes grounding data for the next conversation turn, reference data so that you can inspect the source content, and an activity plan that shows query execution steps.

Query expansion and parallel execution, plus the retrieval response, are the key capabilities of agentic retrieval that make it the best choice for generative AI (RAG) applications.

Agentic retrieval adds latency to query processing, but it makes up for it by adding these capabilities:

- Reads in chat history as an input to the retrieval pipeline.
- Deconstructs a complex query that contains multiple "asks" into component parts. For example: "find me a hotel near the beach, with airport transportation, and that's within walking distance of vegetarian restaurants."
- Rewrites an original query into multiple subqueries using synonym maps (optional) and LLM-generated paraphrasing.
- Corrects spelling mistakes.
- Executes all subqueries simultaneously.
- Outputs a unified result as a single string. Alternatively, you can extract parts of the response for your solution. Metadata about query execution and reference data is included in the response.

Agentic retrieval invokes the entire query processing pipeline multiple times for each subquery, but it does so in parallel, preserving the efficiency and performance necessary for a reasonable user experience.

Note

Including an LLM in query planning adds latency to a query pipeline. You can mitigate the effects by using faster models, such as gpt-4o-mini, and summarizing the message threads. You can minimize latency and costs by setting properties that limit LLM processing. You can also exclude LLM processing altogether for just text and hybrid search and your own query planning logic.

## Architecture and workflow

Agentic retrieval is designed for conversational search experiences that use an LLM to intelligently break down complex queries. The system coordinates multiple Azure services to deliver comprehensive search results.

### How it works

The agentic retrieval process works as follows:

**Workflow initiation**: Your application calls a knowledge base with retrieve action that provides a query and conversation history.**Query planning**: A knowledge base sends your query and conversation history to an LLM, which analyzes the context and breaks down complex questions into focused subqueries. This step is automated and not customizable.**Query execution**: The knowledge base sends the subqueries to your knowledge sources. All subqueries run simultaneously and can be keyword, vector, and hybrid search. Each subquery undergoes semantic reranking to find the most relevant matches. References are extracted and retained for citation purposes.**Result synthesis**: The system combines all results into a unified response with three parts: merged content, source references, and execution details.

Your search index determines query execution and any optimizations that occur during query execution. Specifically, if your index includes searchable text and vector fields, a hybrid query executes. If the only searchable field is a vector field, then only pure vector search is used. The index semantic configuration, plus optional scoring profiles, synonym maps, analyzers, and normalizers (if you add filters) are all used during query execution. You must have named defaults for a semantic configuration and a scoring profile.

### Required components

| Component | Service | Role |
|---|---|---|
LLM |
Azure OpenAI | Creates subqueries from conversation context and later uses grounding data for answer generation |
Knowledge base |
Azure AI Search | Orchestrates the pipeline, connecting to your LLM and managing query parameters |
Knowledge source |
Azure AI Search | Wraps the search index with properties pertaining to knowledge base usage |
Search index |
Azure AI Search | Stores your searchable content (text and vectors) with semantic configuration |
Semantic ranker |
Azure AI Search | Required component that reranks results for relevance (L2 reranking) |

### Integration requirements

Your application drives the pipeline by calling the knowledge base and handling the response. The pipeline returns grounding data that you pass to an LLM for answer generation in your conversation interface. For implementation details, see [Tutorial: Build an end-to-end agentic retrieval solution](agentic-retrieval-how-to-create-pipeline).

Note

Only gpt-4o, gpt-4.1, and gpt-5 series models are supported for query planning. You can use any model for final answer generation.

## How to get started

To create an agentic retrieval solution, you can use the Azure portal, the latest preview REST APIs, or a preview Azure SDK package that provides the functionality.

Currently, the portal only supports creating search index and blob knowledge sources. Other types of knowledge sources must be created programmatically.

[Quickstart: Agentic retrieval in the Azure portal](get-started-portal-agentic-retrieval)[Quickstart: Agentic retrieval](search-get-started-agentic-retrieval)(C#, Java, JavaScript, Python, TypeScript, REST)

## Availability and pricing

Agentic retrieval is available in [selected regions](search-region-support). Knowledge sources and knowledge bases also have [maximum limits](search-limits-quotas-capacity#agentic-retrieval-limits) that vary by service tier.

It has a dependency on premium features. If you disable semantic ranker for your search service, you effectively disable agentic retrieval.

| Plan | Description |
|---|---|
| Free | A free tier search service provides 50 million free agentic reasoning tokens per month. On higher tiers, you can choose between the free plan (default) and the standard plan. |
| Standard | The standard plan is pay-as-you-go pricing once the monthly free quota is consumed. After the free quota is used up, you are charged an additional fee for each additional one million agentic reasoning tokens. You aren't notified when the transition occurs. For more information about charges by currency, see the
|

Token-based billing for LLM-based query planning and [answer synthesis](agentic-retrieval-how-to-answer-synthesis) (optional) is pay-as-you-go in Azure OpenAI. It's token based for both input and output tokens. The model you assign to the knowledge base is the one [charged for token usage](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/#pricing). For example, if you use gpt-4o, the token charge appears in the bill for gpt-4o.

Token-based billing for agentic retrieval is the number of tokens returned by each subquery.

| Aspect | Classic single-query pipeline | Agentic retrieval multi-query pipeline |
|---|---|---|
| Unit | Query based (1,000 queries) per unit of currency | Token based (1 million tokens per unit of currency) |
| Cost per unit | Uniform cost per query | Uniform cost per token |
| Cost estimation | Estimate query count | Estimate token usage |
| Free tier | 1,000 free queries | 50 million free tokens |

### Example: Estimate costs

Agentic retrieval has two billing models: billing from Azure OpenAI (query planning and, if enabled, answer synthesis) and billing from Azure AI Search for agentic retrieval.

This pricing example omits answer synthesis, but helps illustrate the estimation process. Your costs could be lower. For the actual price of transactions, see [Azure OpenAI pricing](https://azure.microsoft.com/pricing/details/cognitive-services/openai-service/#pricing).

#### Estimated billing costs for query planning

To estimate the query plan costs as pay-as-you-go in Azure OpenAI, let's assume gpt-4o-mini:

- 15 cents for 1 million input tokens.
- 60 cents for 1 million output tokens.
- 2,000 input tokens for average chat conversation size.
- 350 tokens for average output plan size.

#### Estimated billing costs for query execution

To estimate agentic retrieval token counts, start with an idea of what an average document in your index looks like. For example, you might approximate:

- 10,000 chunks, where each chunk is one to two paragraphs of a PDF.
- 500 tokens per chunk.
- Each subquery reranks up to 50 chunks.
- On average, there are three subqueries per query plan.

#### Calculating price of execution

Assume we make 2,000 agentic retrievals with three subqueries per plan. This gives us about 6,000 total queries.

Rerank 50 chunks per subquery, which is 300,000 total chunks.

Average chunk is 500 tokens, so the total tokens for reranking is 150 million.

Given a hypothetical price of 0.022 per token, $3.30 is the total cost for reranking in US dollars.

Moving on to query plan costs: 2,000 input tokens multiplied by 2,000 agentic retrievals equal 4 million input tokens for a total of 60 cents.

Estimate the output costs based on an average of 350 tokens. If we multiply 350 by 2,000 agentic retrievals, we get 700,000 output tokens total for a total of 42 cents.


Putting it all together, you'd pay about $3.30 for agentic retrieval in Azure AI Search, 60 cents for input tokens in Azure OpenAI, and 42 cents for output tokens in Azure OpenAI, for $1.02 for query planning total. The combined cost for the full execution is $4.32.

#### Tips for controlling costs

Review the activity log in the response to find out what queries were issued to which sources and the parameters used. You can reissue those queries against your indexes and use a public tokenizer to estimate tokens and compare to API-reported usage. Precise reconstruction of a query or response isn't guaranteed however. Factors include the type of knowledge source, such as public web data or a remote SharePoint knowledge source that's predicated on a user identity, which can affect query reproduction.

Reduce the number of knowledge sources (indexes); consolidating content can lower fan-out and token volume.

Lower the reasoning effort to reduce LLM usage during query planning and query expansion (iterative search).

Organize content so the most relevant information can be found with fewer sources and documents (For example, curated summaries or tables).
