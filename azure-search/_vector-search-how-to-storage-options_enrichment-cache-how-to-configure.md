---
merged_at: 2026-01-25T02:11:58.434976
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-how-to-storage-options.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-storage-options -->

# Eliminate optional vector instances from storage

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search stores multiple copies of vector fields that are used in specific workloads. If your search scenarios don't require all of these copies, you can omit storage for that workload.

Use cases where an extra copy is used include:

- Returning raw vectors in a query response or supporting incremental updates to vector content.
- Rescoring compressed (quantized) vectors as a query optimization technique.

Removing storage is irreversible and requires reindexing if you want it back.

## Prerequisites

[Vector fields in a search index](vector-search-how-to-create-index), with a`vectorSearch`

configuration specifying either the Hierarchical Navigable Small Worlds (HNSW) or exhaustive K-Nearest Neighbor (KNN) algorithm, and a new vector profile.

## How vector fields are stored

| Instance | Usage | Required for search | How removed |
|---|---|---|---|
| Vectors in the
|

`merge`

or `mergeOrUpload`

indexing actions. Also used to return "retrievable" vectors in the query response.`stored`

property to false.1`preserveOriginals`

rescoring on an oversampled candidate set of results from ANN search. This applies to vector fields that undergo [scalar or binary quantization](vector-search-how-to-quantization), and it applies to queries using the HNSW graph. If you're using eKNN, all vectors are in scope for the query, so rescoring has no effect and thus not supported.`rescoringOptions.rescoreStorageMethod`

property to `discardOriginals`

in `vectorSearch.compressions`

.1 This copy is also for internal index operations and for exhaustive KNN search in older API versions, on indexes created using the 2023 APIs. On newer indexes, an eKNN-configured field consists of full-precision vectors so no extra copy is needed.

## Remove source vectors (JSON data)

In a vector field definition, `stored`

is a boolean property that determines whether storage is allocated for retrievable vector content obtained during indexing (the source instance). By default, `stored`

is set to `true`

. If you don't need raw vector content in a query response, changing `stored`

to `false`

can save up to 50% storage per field.

Considerations for setting `"stored": false`

:

Because vectors aren't human readable, you can generally omit them from results sent to LLMs in RAG scenarios or from results rendered on a search page. However, you should keep them if you're using vectors in a downstream process that consumes vector content.

If your indexing strategy uses

[partial document updates](search-howto-reindex#update-content), such as`merge`

or`mergeOrUpload`

on an existing document, setting`"stored": false`

prevents content updates to those fields during the merge. You must include the entire vector field (and nonvector fields you're updating) in each reindexing operation. Otherwise, the vector data is lost without an error or warning. To avoid this risk altogether, set`"stored": true`

.

Important

Setting the `"stored": false`

attribution is irreversible. This property can only be set when you create the index and is only allowed on vector fields. Updating an existing index with new vector fields can't set this property to `false`

. If you want retrievable vector content later, you must drop and rebuild the index or create and load a new field that has the new attribution.

For new vector fields in a search index, set `"stored": false`

to permanently remove retrievable storage for the vector field. The following example shows a vector field definition with the `stored`

property.

```
PUT https://[service-name].search.windows.net/indexes/demo-index?api-version=2025-09-01@search.rerankerBoostedScore
Content-Type: application/json
api-key: [admin key]
{
"name": "demo-index",
"fields": [
{
"name": "vectorContent",
"type": "Collection(Edm.Single)",
"retrievable": false,
"stored": false,
"dimensions": 1536,
"vectorSearchProfile": "vectorProfile"
}
]
}
```


### Summary of key points

Applies to fields that have a

[vector data type](/en-us/rest/api/searchservice/supported-data-types#edm-data-types-for-vector-fields).Affects storage on disk, not memory, and has no effect on queries. Query execution uses a separate vector index that's unaffected by the

`stored`

property because that copy of the vector is always stored.The

`stored`

property is set during index creation on vector fields and is irreversible. If you want retrievable content later, you must drop and rebuild the index or create and load a new field that has the new attribution.Defaults are

`"stored": true`

and`"retrievable": false`

. In a default configuration, a retrievable copy is stored but isn't automatically returned in results. When`stored`

is`true`

, you can toggle`retrievable`

between`true`

and`false`

at any time without having to rebuild an index. When`stored`

is`false`

,`retrievable`

must be`false`

and can't be changed.

## Remove full-precision vectors

Original full-precision vectors are used in rescoring operations over compressed (quantized) vectors. The intent of rescoring is to mitigate the loss in information due to compression. The effect of rescoring is retrieval of a larger set of candidate documents from the compressed index, with recomputation of similarity scores using the original vectors or the dot product. For rescoring to work, original vectors must be retained in storage for certain scenarios. As a result, while quantization reduces memory usage (vector index size usage), it slightly increases storage requirements since both compressed and original vectors are stored. The extra storage is approximately equal to the size of the compressed index.

Rescoring requirements by quantization approach:

Rescoring of scalar quantized vectors requires retention of the original full-precision vectors.

Rescoring of binary quantized vectors can use either the original full-precision vectors, or the dot product of the binary embedding, which produces high quality search results, without having to reference full-precision vectors in the index.


Rescoring recommendations:

For scalar quantization, preserve original full-precision vectors in the index because they're required for rescore.

For binary quantization, either preserve original full-precision vectors for the highest quality of rescoring, or discard full-precision vectors if you want to rescore based on the dot product of the binary embeddings.


The `rescoreStorageMethod`

property controls whether full-precision vectors are stored. In `vectorSearch.compressions`

, the `rescoreStorageMethod`

property is set to `preserveOriginals`

by default, which retains full-precision vectors for [oversampling and rescoring capabilities](vector-search-how-to-quantization#add-compressions-to-a-search-index) to reduce the effect of lossy compression on the HNSW graph. If you don't need rescoring, of if you used binary quantization and the dot product for rescoring, you can reduce vector storage by setting `rescoreStorageMethod`

to `discardOriginals`

.

Important

Setting the `rescoreStorageMethod`

property is irreversible and can adversely affect search quality, although the degree depends on the compression method and any mitigations you apply.

To set this property:

Use

[Create Index](/en-us/rest/api/searchservice/indexes/create)or[Create or Update Index](/en-us/rest/api/searchservice/indexes/create-or-update)REST APIs, or an Azure SDK.Add a

`vectorSearch`

section to your index with profiles, algorithms, and compressions.Under

`vectorSearch.compressions`

, add`rescoringOptions`

with`enableRescoring`

set to true,`defaultOversampling`

set to a positive integer, and`rescoreStorageMethod`

set to`discardOriginals`

for binary quantization and`preserveOriginals`

for scalar quantization.`PUT https://[service-name].search.windows.net/indexes/demo-index?api-version=2025-09-01 { "name": "demo-index", "fields": [. . . ], . . . "vectorSearch": { "profiles": [ { "name": "myVectorProfile-1", "algorithm": "myHnsw", "compression": "myScalarQuantization" }, { "name": "myVectorProfile-2", "algorithm": "myHnsw", "compression": "myBinaryQuantization" } ], "algorithms": [ { "name": "myHnsw", "kind": "hnsw", "hnswParameters": { "metric": "cosine", "m": 4, "efConstruction": 400, "efSearch": 500 }, "exhaustiveKnnParameters": null } ], "compressions": [ { "name": "myScalarQuantization", "kind": "scalarQuantization", "rescoringOptions": { "enableRescoring": true, "defaultOversampling": 10, "rescoreStorageMethod": "preserveOriginals" }, "scalarQuantizationParameters": { "quantizedDataType": "int8" }, "truncationDimension": null }, { "name": "myBinaryQuantization", "kind": "binaryQuantization", "rescoringOptions": { "enableRescoring": true, "defaultOversampling": 10, "rescoreStorageMethod": "discardOriginals" }, "truncationDimension": null } ] } }`


Note

Vector storage strategies have been evolving over the last several releases. Index creation date and API version determine your storage options. For example, in the 2024-11-01-preview, if you set `discardOriginals`

to remove full-precision vectors, there was no rescoring for binary quantization because the dot product approach wasn't available. We recommend using the latest APIs for the best mitigation options.


---

<!-- DOCUMENTO FUSIONADO: enrichment-cache-how-to-configure.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/enrichment-cache-how-to-configure -->

# Configure an enrichment cache

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This feature is in public preview under [supplemental terms of use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). [Preview REST APIs](/en-us/rest/api/searchservice/index-preview) support this feature.

This article explains how to add caching to an enrichment pipeline so that you can modify downstream enrichment steps without having to rebuild in full every time. By default, a skillset is stateless, and changing any part of its composition requires a full rerun of the indexer. With an *enrichment cache*, the indexer can determine which parts of the document tree must be refreshed based on changes detected in the skillset or indexer definitions. Existing processed output is preserved and reused wherever possible.

Cached content is placed in Azure Storage using account information that you provide. The container, named `ms-az-search-indexercache-<alpha-numerc-string>`

, is created when you run the indexer. It should be considered an internal component managed by your search service and must not be modified.

## Prerequisites

[Azure Storage](/en-us/azure/storage/common/storage-account-create)for storing cached enrichments. The storage account must be[general purpose v2](/en-us/azure/storage/common/storage-account-overview#types-of-storage-accounts).[For blob indexing only](search-how-to-index-azure-blob-storage), if you need synchronized document removal from both the cache and index when blobs are deleted from your data source, enable a[deletion policy](search-how-to-index-azure-blob-changed-deleted)in the indexer. Without this policy, document deletion from the cache isn't supported.

You should be familiar with setting up indexers and skillsets. Start with [indexer overview](search-indexer-overview) and then continue on to [skillsets](cognitive-search-working-with-skillsets) to learn about enrichment pipelines.

## Limitations

Caution

If you're using the [SharePoint indexer (Preview)](search-how-to-index-sharepoint-online), you should avoid incremental enrichment. Under certain circumstances, the cache becomes invalid, requiring an [indexer reset and full rebuild](search-howto-run-reset-indexers), should you choose to reload it.

## Permissions

Azure AI Search needs write-access to Azure Storage. If you're using a managed identity for your search service, make sure it's assigned to the **Storage Blob Data Contributor** and **Storage Table Data Contributor** roles. For more information, see [Connect to Azure Storage using a managed identity (Azure AI Search)](search-howto-managed-identities-storage).

## Enable on new indexers

You can use the Azure portal, preview APIs, or preview Azure SDK packages to enable an enrichment cache on an indexer.

On the left, select

**Indexers**, and then select**Add indexer**.Provide an indexer name and an existing index, data source, and skillset.

Enable incremental caching and set the Azure Storage account.


## Enable on existing indexers

For existing indexers that already have a skillset, use the following steps to add caching. As a one-time operation, reset and rerun the indexer in full to load the cache.

### Step 1: Get the indexer definition

Start with a valid, work indexer that has these components: data source, skillset, index. Using an API client, send a [GET Indexer](/en-us/rest/api/searchservice/indexers/get?view=rest-searchservice-2025-11-01-preview&preserve-view=true) request to retrieve the indexer. When you use the preview API version to the GET the indexer, a `cache`

property set to null is added to the definition automatically.

```
GET https://[YOUR-SEARCH-SERVICE].search.windows.net/indexers/[YOUR-INDEXER-NAME]?api-version=2025-11-01-preview
Content-Type: application/json
api-key: [YOUR-ADMIN-KEY]
```


### Step 2: Set the cache property

In the index definition, modify `cache`

to include the following required and optional properties:

- (Required)
`storageConnectionString`

must be set to an Azure Storage connection string. - (Optional)
`enableReprocessing`

boolean property (`true`

by default), indicates that incremental enrichment is enabled. Set to`false`

if you want to suspend incremental processing while other resource-intensive operations, such as indexing new documents, are underway and then switch back to`true`

later.

```
POST https://[service name].search.windows.net/indexers?api-version=2025-11-01-preview
{
"name": "<YOUR-INDEXER-NAME>",
"targetIndexName": "<YOUR-INDEX-NAME>",
"dataSourceName": "<YOUR-DATASOURCE-NAME>",
"skillsetName": "<YOUR-SKILLSET-NAME>",
`cache` : {
"storageConnectionString" : "<YOUR-STORAGE-ACCOUNT-CONNECTION-STRING>",
"enableReprocessing": true
},
"fieldMappings" : [],
"outputFieldMappings": [],
"parameters": []
}
```


### Step 3: Reset the indexer

[Reset Indexer](/en-us/rest/api/searchservice/indexers/reset) is required when setting up incremental enrichment for existing indexers to ensure all documents are in a consistent state. You can use the Azure portal or an API client for this task.

```
POST https://[YOUR-SEARCH-SERVICE].search.windows.net/indexers/[YOUR-INDEXER-NAME]/reset?api-version=2025-11-01-preview
Content-Type: application/json
api-key: [YOUR-ADMIN-KEY]
```


### Step 4: Save the indexer

[Update Indexer](/en-us/rest/api/searchservice/indexers/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) with a PUT request, where the body of the request includes `cache`

.

```
PUT https://[YOUR-SEARCH-SERVICE].search.windows.net/indexers/[YOUR-INDEXER-NAME]?api-version=2025-11-01-preview
Content-Type: application/json
api-key: [YOUR-ADMIN-KEY]
{
"name" : "<YOUR-INDEXER-NAME>",
...
`cache`: {
"storageConnectionString": "<YOUR-STORAGE-ACCOUNT-CONNECTION-STRING>",
"enableReprocessing": true
}
}
```


If you now issue another GET request on the indexer, the response from the service includes an `ID`

property in the cache object. The string is appended to the name of the container containing all the cached results and intermediate state of each document processed by this indexer. The ID is used to uniquely name the cache in Blob storage.

```
`cache`: {
"ID": "<ALPHA-NUMERIC STRING>",
"enableReprocessing": true,
"storageConnectionString": "DefaultEndpointsProtocol=https;AccountName=<YOUR-STORAGE-ACCOUNT>;AccountKey=<YOUR-STORAGE-KEY>;EndpointSuffix=core.windows.net"
}
```


### Step 5: Run the indexer

To run indexer, you can use the Azure portal or the API. In the Azure portal, from the indexers list, select the indexer and select **Run**. One advantage to using the Azure portal is that you can monitor indexer status, note the duration of the job, and how many documents are processed. Portal pages are refreshed every few minutes.

Alternatively, you can use REST to [run the indexer](/en-us/rest/api/searchservice/indexers/run):

```
POST https://[YOUR-SEARCH-SERVICE].search.windows.net/indexers/[YOUR-INDEXER-NAME]/run?api-version=2025-11-01-preview
Content-Type: application/json
api-key: [YOUR-ADMIN-KEY]
```


Note

A reset and rerun of the indexer results in a full rebuild so that content can be cached. All cognitive enrichments will be rerun on all documents. Reusing enriched content from the cache begins after the cache is loaded.

## Check for cached output

Find the cache in Azure Storage, under Blob container. The container name is `ms-az-search-indexercache-<some-alphanumeric-string>`

.

A cache is created and used by an indexer. Its content isn't human readable.

To verify whether the cache is operational, modify a skillset and run the indexer, then compare before-and-after metrics for execution time and document counts.

Skillsets that include image analysis and Optical Character Recognition (OCR) of scanned documents make good test cases. If you modify a downstream text skill or any skill that isn't image-related, the indexer can retrieve all of the previously processed image and OCR content from cache, updating and processing only the text-related changes indicated by your edits. You can expect to see fewer documents in the indexer execution document count, shorter execution times, and fewer charges on your bill.

The [file set](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/ai-enrichment-mixed-media) used in [cog-search-demo tutorials](tutorial-skillset) is a useful test case because it contains 14 files of various formats JPG, PNG, HTML, DOCX, PPTX, and other types. Change `en`

to `es`

or another language in the text translation skill for proof-of-concept testing of incremental enrichment.

## Common errors

The following error occurs if you forget to specify a preview API version on the request:

`"The request is invalid. Details: indexer : A resource without a type name was found, but no expected type was specified. To allow entries without type information, the expected type must also be specified when the model is specified."`


A 400 Bad Request error will also occur if you're missing an indexer requirement. The error message specifies any missing dependencies.

## Next step

Incremental enrichment is applicable on indexers that contain skillsets, providing reusable content for both indexes and knowledge stores. The following link provides more information about cache management.
