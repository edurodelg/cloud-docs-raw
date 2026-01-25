---
merged_at: 2026-01-25T02:11:58.454886
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-index-size.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-index-size -->

# Vector index size and limits

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For each vector field, Azure AI Search constructs an internal vector index using the algorithm parameters specified on the field. Because Azure AI Search imposes quotas on vector index size, you should know how to estimate and monitor vector size to ensure you stay under the limits.

Internally, the physical data structures of a search index include:

- Raw content (used for retrieval patterns requiring nontokenized content)
- Inverted indexes (used for searchable text fields)
- Vector indexes (used for searchable vector fields)

This article explains the limits for the internal vector indexes that back each of your vector fields.

Tip

[Vector optimization techniques](vector-search-how-to-configure-compression-storage) are generally available. Use capabilities like narrow data types, scalar and binary quantization, and elimination of redundant storage to reduce your vector quota and storage quota consumption.

## Key points about quota and vector index size

Vector index size is measured in bytes.

The total storage of your service contains all of your vector index files. Azure AI Search maintains different copies of vector index files for different purposes. We offer other options to reduce the

[storage overhead of vector indexes](vector-search-how-to-storage-options)by eliminating some of these copies.Vector quotas are enforced on the search service as a whole, per partition. If you add partitions, vector quota also increases. Per-partition vector quotas are higher on newer services. For more information, see

[Vector index size limits](search-limits-quotas-capacity#vector-index-size-limits).Not all algorithms consume vector index size quota. Vector quotas are established based on memory requirements of Approximate Nearest Neighbor (ANN) search. Vector fields created with the Hierarchical Navigable Small World (HNSW) algorithm need to reside in memory during query execution because of the random-access nature of graph-based traversals. Vector fields using the exhaustive K-Nearest Neighbors (KNN) algorithm are loaded into memory dynamically in pages during query execution and thus don't consume vector quota.


## Check partition size and quantity

If you aren't sure what your search service limits are, here are two ways to get that information:

In the Azure portal, on the search service

**Overview**page, both the**Properties**tab and**Usage**tab show partition size and storage, and also vector quota and vector index size.In the Azure portal, on the

**Scale**page, you can review the number and size of partitions.

Your vector limit varies depending on your [service creation date](search-how-to-upgrade#check-your-service-creation-or-upgrade-date).

## Check vector index size

A request for vector metrics is a data plane operation. You can use the Azure portal, REST APIs, or Azure SDKs to get vector usage at the service level through service statistics and for individual indexes.

#### Vector size per index

To get vector index size per index, select **Search management** > **Indexes** to view a list of indexes and the document count, the size of in-memory vector indexes, and total index size as stored on disk.

Recall that vector quota is based on memory constraints. For vector indexes created using the HNSW algorithm, all searchable vector indexes are permanently loaded into memory. For indexes created using the exhaustive KNN algorithm, vector indexes are loaded in chunks, sequentially, during query time. There's no memory residency requirement for exhaustive KNN indexes. The lifetime of the loaded pages in memory is similar to text search and there are no other metrics applicable to exhaustive KNN indexes other than total storage.

The following screenshot shows two versions of the same vector index. One version is created using HNSW algorithm, where the vector graph is memory resident. Another version is created using exhaustive KNN algorithm. With exhaustive KNN, there's no specialized in-memory vector index, so the portal shows 0 MB for vector index size. Those vectors still exist and are counted in overall storage size, but they don’t occupy the in-memory resource that the vector index size metric is tracking.

#### Vector size per service

To get vector index size for the search service as a whole, select the **Overview** page's **Usage** tab. Portal pages refresh every few minutes so if you recently updated an index, wait a bit before checking results.

The following screenshot is for an older Standard 1 (S1) search service, configured for one partition and one replica.

Storage quota is a disk constraint, and it's inclusive of all indexes (vector and nonvector) on a search service.

Vector index size quota is a memory constraint. It's the amount of memory required to load all internal vector indexes created for each vector field on a search service.


The screenshot indicates that indexes (vector and nonvector) consume almost 460 megabytes of available disk storage. Vector indexes consume almost 93 megabytes of memory at the service level.

Quotas for both storage and vector index size increase or decrease as you add or remove partitions. If you change the partition count, the tile shows a corresponding change in storage and vector quota.

Note

On disk, vector indexes aren't 93 megabytes. Vector indexes on disk take up about three times more space than vector indexes in memory. See [How vector fields affect disk storage](#how-vector-fields-affect-disk-storage) for details.

## Factors affecting vector index size

There are three major components that affect the size of your internal vector index:

- Raw size of the data
- Overhead from the selected algorithm
- Overhead from deleting or updating documents within the index

### Raw size of the data

Each vector is usually an array of single-precision floating-point numbers, in a field of type `Collection(Edm.Single)`

.

Vector data structures require storage, represented in the following calculation as the "raw size" of your data. Use this *raw size* to estimate the vector index size requirements of your vector fields.

The dimensionality of one vector determines its storage size. Multiply the size of one vector by the number of documents containing that vector field to obtain the *raw size*:

`raw size = (number of documents) * (dimensions of vector field) * (size of data type)`


| EDM data type | Size of the data type |
|---|---|
`Collection(Edm.Single)` |
4 bytes |
`Collection(Edm.Half)` |
2 bytes |
`Collection(Edm.Int16)` |
2 bytes |
`Collection(Edm.SByte)` |
1 byte |

### Memory overhead from the selected algorithm

Every ANN algorithm generates extra data structures in memory to enable efficient searching. These structures consume extra space within memory.

**For the HNSW algorithm, the memory overhead ranges between 1% and 20% for uncompressed float32 (Edm.Single) vectors.**

As dimensionality increases, the memory overhead percentage decreases. This occurs because the raw size of the vectors increases in size while the other data structures, which store graph connectivity information, remain a fixed size for a given `m`

. As a result, the relative impact of these extra data structures diminishes in relation to the overall vector size.

The memory overhead increases with larger values of the HNSW parameter `m`

, which specifies the number of bi-directional links created for each new vector during index construction. This happens because each link contributes approximately 8 to 10 bytes per document, and the total overhead scales proportionally with `m`

.

The following table summarizes the overhead percentages observed in internal tests for *uncompressed* vector fields:

| Dimensions | HNSW parameter (m) | Overhead percentage |
|---|---|---|
| 96 | 4 | 20% |
| 200 | 4 | 8% |
| 768 | 4 | 2% |
| 1536 | 4 | 1% |
| 3072 | 4 | 0.5% |

These results demonstrate the relationship between dimensions, HNSW parameter `m`

, and memory overhead for the HNSW algorithm.

For vector fields that use compression techniques, such as [scalar or binary quantization](vector-search-how-to-quantization), the overhead percentage appears to consume a greater percentage of the total vector index size. As the size of the data decreases, the relative impact of the fixed-size data structures used to store graph connectivity information becomes more significant.

### Overhead from deleting or updating documents within the index

When a document with a vector field is either deleted or updated (updates are internally represented as a delete and insert operation), the underlying document is marked as deleted and skipped during subsequent queries. As new documents are indexed and the internal vector index grows, the system cleans up these deleted documents and reclaims the resources. This means you'll likely observe a lag between deleting documents and the underlying resources being freed.

We refer to this as the *deleted documents ratio*. Since the deleted documents ratio depends on the indexing characteristics of your service, there's no universal heuristic to estimate this parameter, and there's no API or script that returns the ratio in effect for your service. We observe that half of our customers have a deleted documents ratio less than 10%. If you tend to perform high-frequency deletions or updates, then you might observe a higher deleted documents ratio.

This is another factor impacting the size of your vector index. Unfortunately, we don't have a mechanism to surface your current deleted documents ratio.

## Estimate total size of data in memory

Taking the previously described factors into account, to estimate the total size of your vector index, use the following calculation:

`(raw_size) * (1 + algorithm_overhead (in percent)) * (1 + deleted_docs_ratio (in percent))`


For example, to calculate the **raw_size**, let's assume you're using a popular Azure OpenAI model, `text-embedding-ada-002`

with 1,536 dimensions. This means one document would consume 1,536 `Edm.Single`

(floats), or 6,144 bytes since each `Edm.Single`

is 4 bytes. 1,000 documents with a single, 1,536-dimensional vector field would consume in total 1000 docs x 1536 floats/doc = 1,536,000 floats, or 6,144,000 bytes.

If you have multiple vector fields, you need to perform this calculation for each vector field within your index and add them all together. For example, 1,000 documents with **two** 1,536-dimensional vector fields, consume 1000 docs x **2 fields** x 1536 floats/doc x 4 bytes/float = 12,288,000 bytes.

To obtain the **vector index size**, multiply this **raw_size** by the **algorithm overhead** and **deleted document ratio**. If your algorithm overhead for your chosen HNSW parameters is 10% and your deleted document ratio is 10%, then we get: `6.144 MB * (1 + 0.10) * (1 + 0.10) = 7.434 MB`

.

## How vector fields affect disk storage

Most of this article provides information about the size of vectors in memory. For information about the storage overhead of vector indexes, see [Eliminate optional vector instances from storage](vector-search-how-to-storage-options).


---

<!-- DOCUMENTO FUSIONADO: search-how-to-index-logic-apps.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-index-logic-apps -->

# Use an Azure Logic Apps workflow for automated indexing in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, you can use the [ Import data (new) wizard](search-get-started-portal-import-vectors) in the Azure portal to create a logic app workflow that indexes and vectorizes your content. This capability is equivalent to an

[indexer](search-indexer-overview)and data source that generates an indexing pipeline and creates searchable content.

After you create a workflow in the wizard, you can manage the workflow in Azure Logic Apps alongside your other workflows. Behind the scenes, the wizard follows a workflow template that pulls in (ingests) content from a source for indexing in AI Search. The connectors used in this scenario are prebuilt and already exist in Azure Logic Apps, so the workflow template just provides details for those connectors to create connections to the data source, AI Search, and other items to complete the ingestion workflow.

## Key features

Azure Logic Apps integration in Azure AI Search adds support for:

[More data sources](search-data-sources-gallery)from Microsoft and other providers- Integrated vectorization
- Scheduled or on-demand indexing
- Change detection of new and existing documents

The **Import data (new)** wizard inputs include:

- A supported data source
- A supported text embedding model

After the wizard completes, you have the following components:

| Component | Location | Description |
|---|---|---|
| Search index | Azure AI Search | Contains indexed content from a supported Logic Apps connector. The index schema is a default index created by the wizard. You can add extra elements, such as scoring profile or semantic configuration, but you can't change existing fields. You view, manage, and access the search index on Azure AI Search. |
| Logic app resource and workflow | Azure Logic Apps | You can view the running workflow, or you can open the designer in Azure Logic Apps to edit the workflow, as you regularly do if you'd started from Azure Logic Apps instead. You can edit and extend the workflow, but exercise caution so as to not break the indexing pipeline. The workflow created by the wizard uses the Consumption hosting option. |
| Logic app templates | Azure Logic Apps | Up to two templates created per workflow: one for on-demand indexing, and a second template for scheduled indexing. You can modify the indexing schedule in the Index multiple documents step of the workflow. |

## Prerequisites

Review the following requirements before you start:

You must be an

**Owner**or**Contributor**in your Azure subscription, with permissions to create resources.Azure AI Search, Basic pricing tier or higher if you want to use a search service identity for connections to an Azure data source, otherwise you can use any tier, subject to tier limits.

Azure OpenAI, with a

[supported embedding model](#supported-models)deployment. Vectorization is integrated into the workflow. If you don't need vectors, you can ignore the fields or try another indexing strategy.Azure Logic Apps is a

[supported region](#supported-regions). It should have a[system-assigned managed identity](/en-us/azure/logic-apps/authenticate-with-managed-identity)if you want to use Microsoft Entra ID authentication on connections rather than API keys.

Note

A logic app workflow is a billable resource. For more information, see [Azure Logic Apps pricing](/en-us/azure/logic-apps/logic-apps-pricing).

### Supported regions

End-to-end functionality is available in the following regions, which provide the data source connection, document cracking, document chunks, support for Azure OpenAI embedding models, and the built-in indexing support for pulling the data. The following regions for Azure Logic Apps provide the `ParseDocument`

action upon which indexing integration is based.

- East US
- East US 2
- South Central US
- West US 2
- West US 3
- Brazil South
- Australia East
- East Asia
- Southeast Asia
- North Europe
- Sweden Central
- UK South

### Supported models

The logic app path through the **Import data (new)** wizard supports a selection of embedding models.

Deploy one of the following [embedding models](/en-us/azure/ai-services/openai/concepts/models#embeddings) on Azure OpenAI for your end-to-end workflow.

- text-embedding-3-small
- text-embedding-3-large
- text-embedding-ada-002

### Supported connectors

The following connectors are useful for indexing unstructured data, as a complement to classic indexers that primarily target structured data.

### Supported actions

Logic apps integration includes the following indexing actions. For more information, see [Connect to Foundry Tools from workflows in Azure Logic Apps](/en-us/azure/logic-apps/connectors/azure-ai#ingest-data-workflow).

- Check for new data.
- Get the data. An HTTP action that retrieves the uploaded document using the file URL from the trigger output.
- Compose document details. A Data Operations action that concatenates various items.
- Create token string. A Data Operations action that produces a token string using the output from the Compose action.
- Create content chunks. A Data Operations action that splits the token string into pieces, based on either the number of characters or tokens per content chunk.
- Convert tokenized data to JSON. A Data Operations action that converts the token string chunks into a JSON array.
- Select JSON array items. A Data Operations action that selects multiple items from the JSON array.
- Generate the embeddings. An Azure OpenAI action that creates embeddings for each JSON array item.
- Select embeddings and other information. A Data Operations action that selects embeddings and other document information.
- Index the data. An Azure AI Search action that indexes the data based on each selected embedding.

It also supports the following query actions:

- Wait for input prompt. A trigger that either polls or waits for new data to arrive, either based on a scheduled recurrence or in response to specific events respectively.
- Input system message for the model. A Data Operations action that provides input to train the model.
- Input sample questions and responses. A Data Operations action that provides sample customer questions and associated roles to train the model.
- Input system message for search query. A Data Operations action that provides search query input to train the model.
- Generate search query. An Inline Code action that uses JavaScript to create a search query for the vector store, based on the outputs from the preceding Compose actions.
- Convert query to embedding. An Azure OpenAI action that connects to the chat completion API, which guarantees reliable responses in chat conversations.
- Get an embedding. An Azure OpenAI action that gets a single vector embedding.
- Search the vector database. An Azure AI Search action that executes searches in the vector store.
- Create prompt. An Inline Code action that uses JavaScript to build prompts.
- Perform chat completion. An Azure OpenAI action that connects to the chat completion API, which guarantees reliable responses in chat conversations.
- Return a response. A Request action that returns the results to the caller when you use the Request trigger.

## Limitations

- The search index is generated using a fixed schema (document ID, content, and vectorized content), with text extraction only. You can
[modify the index](#modify-existing-objects)as long as the update doesn't affect existing fields. - Vectorization supports text embedding only.
- Deletion detection isn't supported. You must manually
[delete orphaned documents](search-how-to-delete-documents#delete-a-single-document)from the index. - Duplicate documents in the search index are a known issue in this preview. Consider deleting objects and starting over if this becomes an issue.
- No support for private endpoints in the logic app workflow created by the portal wizard. The workflow is hosted using the
and is subject to its constraints. To use the**Consumption**hosting option**Standard**hosting option, use a programmatic approach to creating the workflow. - All actions are generally available except for

## Create a logic app workflow

Follow these steps to create a logic app workflow for indexing content in Azure AI Search.

Start the

**Import data (new)**wizard in the Azure portal.Choose a

[supported Azure Logic Apps connector](#supported-connectors).In

**Connect to your data**, provide a name prefix used for the search index and workflow. Having a common name helps you manage them together.Specify the indexing frequency. If you choose on a schedule, a template that includes a scheduling option is used to create the workflow. You can modify the indexing schedule in the

**Index multiple documents**step of the workflow after it's created.Select an authentication type where the logic app workflow connects to the search engine and starts the indexing process. The workflow can connect using

[Azure AI Search API keys](search-security-api-keys)or the wizard can create a role assignment that grants permissions to the Logic Apps system-assigned managed identity, assuming one exists.Select

**Next**to continue to the next page.In

**Vectorize your text**, provide the model deployment and Azure OpenAI connection information. Choose the subscription and service, a[supported text embedding model](#supported-models), and the authentication type that the workflow uses to connect to Azure OpenAI.Select

**Next**to continue to the next page. Review the configuration.Select

**Create**to begin processing.The workflow runs as a serverless workflow in Logic Apps (Consumption), separate from the AI Search service.

Confirm index creation in the Azure portal, in the

**Indexes**page in Azure AI Search.[Search Explorer](search-explorer)is the first tab. Select**Search**to return some content.

## Modify existing objects

You can make the following modifications to a search index without breaking indexing:

You can make the following updates to a workflow without breaking indexing:

- Modify
**List files in folder**to change the number of documents sent to indexing. - Modify
**Chunk Text**to vary token inputs. The recommended token size is 512 tokens for most scenarios. - Modify
**Chunk Text**to add a page overlap length. - Modify
**Index multiple documents**step to control indexing frequency if you chose scheduled indexing in the wizard.

In logic apps designer, review the workflow and each step in the indexing pipeline. The workflow specifies document extraction, default document chunking ([Text Split skill](cognitive-search-skill-textsplit)), embedding ([Azure OpenAI embedding skill](cognitive-search-skill-azure-openai-embedding)), output field mappings, and finally indexing.

## Template and workflow management

The wizard creates templates and workflows when you specify a Logic Apps indexer. To create and manage them, including template deletion, use the logic app designer. The Azure portal search service dashboard doesn't provide template or workflow management, and currently there's no programmatic support in Azure AI Search APIs.
