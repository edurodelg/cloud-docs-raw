---
source_url: https://learn.microsoft.com/en-us/azure/search/index-projections-concept-intro
fetched_at: 2026-01-25T02:09:04.359664
---

# Define an index projection for parent-child indexing

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For indexes containing chunked documents, an *index projection* specifies how parent-child content is mapped to fields in a search index for one-to-many indexing. Through an index projection, you can send content to:

A single index, where the parent fields repeat for each chunk, but the grain of the index is at the chunk level. The

[classic RAG example](https://github.com/Azure-Samples/azure-search-classic-rag/blob/main/README.md)shows this approach.Two or more indexes, where the parent index has fields related to the parent document, and the child index is organized around chunks. The child index is the primary search corpus, but the parent index could be used for

[lookup queries](/en-us/rest/api/searchservice/documents/get)when you want to retrieve the parent fields of a particular chunk, or for independent queries.

Most implementations are a single index organized around chunks with parent fields, such as the document filename, repeating for each chunk. However, the system is designed to support separate and multiple child indexes if that's your requirement. Azure AI Search doesn't support index joins so your application code must handle which index to use.

An index projection is defined in a [skillset](cognitive-search-working-with-skillsets). It's responsible for coordinating the indexing process that sends chunks of content to a search index, along with the parent content associated with each chunk. It improves how native data chunking works by giving your more options for controlling how parent-child content is indexed.

This article explains how to create a single index schema and indexer projection patterns for one-to-many indexing.

## Prerequisites

An index (one or more) that accepts the output of the indexer pipeline.

A

[supported data source](search-indexer-overview#supported-data-sources)having content that you want to chunk. It can be vector or nonvector content.A skill that splits content into chunks, either the

[Text Split skill](cognitive-search-skill-textsplit)or a custom skill that provides equivalent functionality.

The skillset contains the indexer projection that shapes the data for one-to-many indexing. A skillset could also have other skills, such as an embedding skill like [AzureOpenAIEmbedding](cognitive-search-skill-azure-openai-embedding) if your scenario includes integrated vectorization.

### Dependency on indexer processing

One-to-many indexing takes a dependency on skillsets and indexer-based indexing that includes the following four components:

- A data source
- One or more indexes for your searchable content
- A skillset that contains an index projection*
- An indexer

Your data can originate from any supported data source, but the assumption is that the content is large enough that you want to chunk it, and the reason for chunking it is that you're implementing a RAG pattern that provides grounding data to a chat model. Or, you're implementing vector search and need to meet the smaller input size requirements of embedding models.

Indexers load indexed data into a predefined index. How you define the schema and whether to use one or more indexes is the first decision to make in a one-to-many indexing scenario. The next section covers index design.

## Create an index for one-to-many indexing

Whether you create one index for chunks that repeat parent values, or separate indexes for parent-child field placement, the primary index used for searching is designed around data chunks. It must have the following fields:

A document key field uniquely identifying each document. It must be defined as type

`Edm.String`

with the`keyword`

analyzer.A field associating each chunk with its parent. It must be of type

`Edm.String`

. It can't be the document key field, and must have`filterable`

set to true. It's referred to as parent_id in the examples and as a[projected key value](#projected-key-value)in this article.Other fields for content, such as text or vectorized chunk fields.


An index must exist on the search service before you create the skillset or run the indexer.

### Single index schema inclusive of parent and child fields

A single index designed around chunks with parent content repeating for each chunk is the predominant pattern for RAG and vector search scenarios. The ability to associate the correct parent content with each chunk is enabled through index projections.

The following schema is an example that meets the requirements for index projections. In this example, parent fields are the parent_id and the title. Child fields are the vector and nonvector vector chunks. The chunk_id is the document ID of this index. The parent_id and title repeat for every chunk in the index.

You can use the Azure portal, REST APIs, or an Azure SDK to [create an index](search-how-to-load-search-index).

```
{
"name": "my_consolidated_index",
"fields": [
{"name": "chunk_id", "type": "Edm.String", "key": true, "filterable": true, "analyzer": "keyword"},
{"name": "parent_id", "type": "Edm.String", "filterable": true},
{"name": "title", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "retrievable": true},
{"name": "chunk", "type": "Edm.String","searchable": true,"retrievable": true},
{"name": "chunk_vector", "type": "Collection(Edm.Single)", "searchable": true, "retrievable": false, "stored": false, "dimensions": 1536, "vectorSearchProfile": "hnsw"}
],
"vectorSearch": {
"algorithms": [{"name": "hsnw", "kind": "hnsw", "hnswParameters": {}}],
"profiles": [{"name": "hsnw", "algorithm": "hnsw"}]
}
}
```


## Add index projections to a skillset

Index projections are defined inside a skillset definition and are primarily defined as an array of `selectors`

, where each selector corresponds to a different target index on the search service. This section starts with syntax and examples for context, followed by [parameter reference](#parameter-reference).

Choose a tab for the various API syntax. There's currently no portal support for setting up projections, other than editing the skillset JSON definition. Refer to the REST example for JSON.

Index projections are generally available. We recommend the most recent stable API:

Here's an example payload for an index projections definition that you might use to project individual pages output by the [Text Split skill](cognitive-search-skill-textsplit) as their own documents in the search index.

```
"indexProjections": {
"selectors": [
{
"targetIndexName": "my_consolidated_index",
"parentKeyFieldName": "parent_id",
"sourceContext": "/document/pages/*",
"mappings": [
{
"name": "chunk",
"source": "/document/pages/*",
"sourceContext": null,
"inputs": []
},
{
"name": "chunk_vector",
"source": "/document/pages/*/chunk_vector",
"sourceContext": null,
"inputs": []
},
{
"name": "title",
"source": "/document/title",
"sourceContext": null,
"inputs": []
}
]
}
],
"parameters": {
"projectionMode": "skipIndexingParentDocuments"
}
}
```


### Parameter reference

| Index projection parameters | Definition |
|---|---|
`selectors` |
Parameters for the main search corpus, usually the one designed around chunks. |
`projectionMode` |
An optional parameter providing instructions to the indexer. The only valid value for this parameter is `skipIndexingParentDocuments` , and it's used when the chunk index is the primary search corpus and you need to specify whether parent fields are indexed as extra search documents within the chunked index. If you don't set `skipIndexingParentDocuments` , you get extra search documents in your index that are null for chunks, but populated with parent fields only. For example, if five documents contribute 100 chunks to the index, then the number of documents in the index is 105. The five documents created or parent fields have nulls for chunk (child) fields, making them substantially different from the bulk of the documents in the index. We recommend `projectionMode` set to `skipIndexingParentDocument` . |

Selectors have the following parameters as part of their definition.

| Selector parameters | Definition |
|---|---|
`targetIndexName` |
The name of the index into which index data is projected. It's either the single chunked index with repeating parent fields, or it's the child index if you're using
|

`parentKeyFieldName`

`sourceContext`

[Skill context and input annotation language](cognitive-search-skill-annotation-language).`mappings`

`name`

: The name of the field in the search index that the data should be indexed into. `source`

: The enrichment annotation path that the data should be pulled from. Each

`mapping`

can also recursively define data with an optional `sourceContext`

and `inputs`

field, similar to the [knowledge store](knowledge-store-concept-intro)or[Shaper Skill](cognitive-search-skill-shaper). Depending on your application, these parameters allow you to shape data into fields of type`Edm.ComplexType`

in the search index. Some LLMs don't accept a complex type in search results, so the LLM you're using determines whether a complex type mapping is helpful or not.The `mappings`

parameter is important. You must explicitly map every field in the child index, except for the ID fields such as document key and the parent ID.

This requirement is in contrast with other field mapping conventions in Azure AI Search. For some data source types, the indexer can implicitly map fields based on similar names, or known characteristics (for example, blob indexers use the unique metadata storage path as the default document key). However, for indexer projections, you must explicitly specify every field mapping on the "many" side of the relationship.

Do not create a field mapping for the parent key field. Doing so disrupts change tracking and synchronized data refresh.

## Handling parent documents

Now that you've seen several patterns for one-to-many indexings, lets compare key differences about each option. Index projections effectively generate "child" documents for each "parent" document that runs through a skillset. You have several choices for handling the "parent" documents.

To send parent and child documents to separate indexes, set the

`targetIndexName`

for your indexer definition to the parent index, and set the`targetIndexName`

in the index projection selector to the child index.To keep parent and child documents in the same index, set the indexer

`targetIndexName`

and the index projection`targetIndexName`

to the same index.To avoid creating parent search documents and ensuring the index contains only child documents of a uniform grain, set the

`targetIndexName`

for both the indexer definition and the selector to the same index, but add an extra`parameters`

object after`selectors`

, with a`projectionMode`

key set to`skipIndexingParentDocuments`

, as shown here:`"indexProjections": { "selectors": [ ... ], "parameters": { "projectionMode": "skipIndexingParentDocuments" } }`


## Review field mappings

Indexers are affiliated with three different types of field mappings. Before you run the indexer, check your field mappings and know when to use each type.

[Field mappings](search-indexer-field-mappings) are defined in an indexer and used to map a source field to an index field. Field mappings are used for data paths that lift data from the source and pass it in for indexing, with no intermediate skills processing step. Typically, an indexer can automatically map fields that have the same name and type. Explicit field mappings are only required when there's discrepancies. In one-to-many indexing and the patterns discussed thus far, you might not need field mappings.

[Output field mappings](cognitive-search-output-field-mapping) are defined in an indexer and used to map enriched content generated by a skillset to a field into the main index. In the one-to-many patterns covered in this article, it is a single index schema that includes parent and child fields. The parent index is sparse, with just a title field. The title field isn't populated with content from the skillset processing, so we don't need an output field mapping.

Indexer projection field mappings are used to map skillset-generated content to fields in the child index. In cases where the child index also includes parent fields (as in the [consolidated index solution](#single-index-schema-inclusive-of-parent-and-child-fields)), you should set up field mappings for every field that has content, including the parent-level title field, assuming you want the title to show up in each chunked document. If you're using [separate parent and child indexes](#example-of-separate-parent-child-indexes), the indexer projections should have field mappings for just the child-level fields.

Note

Both output field mappings and indexer projection field mappings accept enriched document tree nodes as source inputs. Knowing how to specify a path to each node is essential to setting up the data path. To learn more about path syntax, see [Reference a path to enriched nodes](cognitive-search-concept-annotations-syntax) and [skillset definition](cognitive-search-working-with-skillsets#skillset-definition) for examples.

## Run the indexer

Once you have created a data source, indexes, and skillset, you're ready to [create and run the indexer](search-howto-create-indexers#run-the-indexer). This step puts the pipeline into execution.

You can query your search index after processing concludes to test your solution.

## Content lifecycle

Depending on the underlying data source, an indexer can usually provide ongoing change tracking and deletion detection. This section explains the content lifecycle of one-to-many indexing as it relates to data refresh.

For data sources that provide change tracking and deletion detection, an indexer process can pick up changes in your source data. Each time you run the indexer and skillset, the index projections are updated if the skillset or underlying source data has changed. Any changes picked up by the indexer are propagated through the enrichment process to the projections in the index, ensuring that your projected data is a current representation of content in the originating data source. Data refresh activity is captured in a projected key value for each chunk. This value gets updated when the underlying data changes.

Note

While you can manually edit the data in the projected documents using the [index push API](search-how-to-load-search-index), you should avoid doing so. Manual updates to an index are overwritten on the next pipeline invocation, assuming the document in source data is updated and the data source has change tracking or deletion detection enabled.

### Updated content

If you add new content to your data source, new chunks or child documents are added to the index on the next indexer run.

If you modify existing content in the data source, chunks are updated incrementally in the search index if the data source you're using supports change tracking and deletion detection. For example, if a word or sentence changes in a document, the chunk in the target index that contains that word or sentence is updated on the next indexer run. Other types of updates, such as changing a field type and some attributions, aren't supported for existing fields. For more information about allowed updates, see [Update an index schema](search-howto-reindex#update-an-index-schema).

Some data sources like [Azure Storage](search-how-to-index-azure-blob-changed-deleted) support change and deletion tracking by default, based on the timestamp. Other data sources such as [Microsoft OneLake](search-how-to-index-onelake-files), [Azure SQL](search-how-to-index-sql-database), or [Azure Cosmos DB](search-how-to-index-cosmosdb-sql) must be configured for change tracking.

### Deleted content

If the source content no longer exists (for example, if text is shortened to have fewer chunks), the corresponding child document in the search index is deleted. The remaining child documents also get their key updated to include a new hash value, even if their content didn't otherwise change.

If a parent document is completely deleted from the datasource, the corresponding child documents only get deleted if the deletion is detected by a `dataDeletionDetectionPolicy`

defined on the datasource definition. If you don't have a `dataDeletionDetectionPolicy`

configured and need to delete a parent document from the datasource, then you should manually delete the child documents if they're no longer wanted.

### Projected key value

To ensure data integrity for updated and deleted content, data refresh in one-to-many indexing relies on a *projected key value* on the "many" side. If you're using integrated vectorization or the [ Import data (new) wizard](search-import-data-portal), the projected key value is the

`parent_id`

field in a chunked or "many" side of the index.A projected key value is a unique identifier that the indexer generates for each document. It ensures uniqueness and allows for change and deletion tracking to work correctly. This key contains the following segments:

- A random hash to guarantee uniqueness. This hash changes if the parent document is updated on subsequent indexer runs.
- The parent document's key.
- The enrichment annotation path that identifies the context that that document was generated from.

For example, if you split a parent document with key value "aa1b22c33" into four pages, and then each of those pages is projected as its own document via index projections:

- aa1b22c33
- aa1b22c33_pages_0
- aa1b22c33_pages_1
- aa1b22c33_pages_2

If the parent document is updated in the source data, perhaps resulting in more chunked pages, the random hash changes, more pages are added, and the content of each chunk is updated to match whatever is in the source document.

## Example of separate parent-child indexes

This section shows examples for separate parent and child indexes. It's an uncommon pattern, but it's possible you might have application requirements that are best met using this approach. In this scenario, you're projecting parent-child content into two separate indexes.

Each schema has the fields for its particular grain, with the parent ID field common to both indexes for use in a [lookup query](/en-us/rest/api/searchservice/documents/get). The primary search corpus is the child index, but then issue a lookup query to retrieve the parent fields for each match in the result. Azure AI Search doesn't support joins at query time, so your application code or orchestration layer would need to merge or collate results that can be passed to an app or process.

The parent index has a parent_id field and title. The parent_id is the document key. You don't need vector search configuration unless you want to vectorize fields at the parent document level.

```
{
"name": "my-parent-index",
"fields": [
{"name": "parent_id", "type": "Edm.String", "filterable": true},
{"name": "title", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "retrievable": true},
]
}
```


The child index has the chunked fields, plus the parent_id field. If you're using integrated vectorization, scoring profiles, semantic ranker, or analyzers you would set these in the child index.

```
{
"name": "my-child-index",
"fields": [
{"name": "chunk_id", "type": "Edm.String", "key": true, "filterable": true, "analyzer": "keyword"},
{"name": "parent_id", "type": "Edm.String", "filterable": true},
{"name": "chunk", "type": "Edm.String","searchable": true,"retrievable": true},
{"name": "chunk_vector", "type": "Collection(Edm.Single)", "searchable": true, "retrievable": false, "stored": false, "dimensions": 1536, "vectorSearchProfile": "hnsw"}
],
"vectorSearch": {
"algorithms": [{"name": "hsnw", "kind": "hnsw", "hnswParameters": {}}],
"profiles": [{"name": "hsnw", "algorithm": "hnsw"}]
},
"scoringProfiles": [],
"semanticConfiguration": [],
"analyzers": []
}
```


Here's an example of an index projection definition that specifies the data path the indexer should use to index content. It specifies the child index name in the index projection definition, and it specifies the mappings of every child or chunk-level field. This is the only place the child index name is specified.

```
"indexProjections": {
"selectors": [
{
"targetIndexName": "my-child-index",
"parentKeyFieldName": "parent_id",
"sourceContext": "/document/pages/*",
"mappings": [
{
"name": "chunk",
"source": "/document/pages/*",
"sourceContext": null,
"inputs": []
},
{
"name": "chunk_vector",
"source": "/document/pages/*/chunk_vector",
"sourceContext": null,
"inputs": []
}
]
}
]
}
```


The indexer definition specifies the components of the pipeline. In the indexer definition, the index name to provide is the parent index. If you need field mappings for the parent-level fields, define them in outputFieldMappings. For one-to-many indexing that uses separate indexes, the indexer definition might look like the following example.

```
{
"name": "my-indexer",
"dataSourceName": "my-ds",
"targetIndexName": "my-parent-index",
"skillsetName" : "my-skillset"
"parameters": { },
"fieldMappings": (optional) Maps fields in the underlying data source to fields in an index,
"outputFieldMappings" : (required) Maps skill outputs to fields in an index,
}
```


## Next step

Data chunking and one-to-many indexing are part of the classic RAG pattern in Azure AI Search. Continue on to the following tutorial and code sample to learn more about it.