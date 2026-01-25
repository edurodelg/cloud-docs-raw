---
merged_at: 2026-01-25T02:11:58.428552
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-concept-annotations-syntax.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-concept-annotations-syntax -->

# Reference a path to enriched nodes using context and source properties an Azure AI Search skillset

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

During skillset execution, the engine builds an in-memory [enrichment tree](cognitive-search-working-with-skillsets#enrichment-tree) that captures each enrichment, such as recognized entities or translated text. In this article, learn how to reference an enrichment node in the enrichment tree so that you can pass output to downstream skills or specify an output field mapping for a search index field.

This article uses examples to illustrate various scenarios. For the full syntax, see [Skill context and input annotation language](cognitive-search-skill-annotation-language).

## Background concepts

Before reviewing the syntax, let's revisit a few important concepts to better understand the examples provided later in this article.

| Term | Description |
|---|---|
| "enriched document" | An enriched document is an in-memory structure that collects skill output as it's created and it holds all enrichments related to a document. Think of an enriched document as a tree. Generally, the tree starts at the root document level, and each new enrichment is created from a previous node as its child. |
| "node" | Within an enriched document, a node (sometimes referred to as an "annotation") is specific output such as the "text" or "layoutText" of the OCR skill, or an original source field value such as the content of a product ID field, or metadata copied from the source such as metadata_storage_path from blobs in Azure Storage. |
| "context" | The scope of enrichment, which is either the entire document, a portion of a document (pages or sentences), or if you're working with images, the extracted images from a document. By default, the enrichment context is at the `"/document"` level, scoped to individual documents contained in the data source. When a skill runs, the outputs of that skill become
|

## Paths for different scenarios

Paths are specified in the "context" and "source" properties of a skillset, and in the [output field mappings](cognitive-search-output-field-mapping) in an indexer.


The example in the screenshot illustrates the path for an item in an Azure Cosmos DB collection.

`context`

path is`/document/HotelId`

because the collection is partitioned into documents by the`/HotelId`

field.`source`

path is`/document/Description`

because the skill is a translation skill, and the field that you want to translate is the`Description`

field in each document.

All paths start with `/document`

. An enriched document is created in the "document cracking" stage of indexer execution, when the indexer opens a document or reads in a row from the data source. Initially, the only node in an enriched document is the [root node ( /document)](cognitive-search-skill-annotation-language#document-root), and it's the node from which all other enrichments occur.

The following list includes several common examples:

`/document`

is the root node and indicates an entire blob in Azure Storage, or a row in a SQL table.`/document/{key}`

is the syntax for a document or item in an Azure Cosmos DB collection, where`{key}`

is the actual key, such as`/document/HotelId`

in the previous example.`/document/content`

specifies the "content" property of a JSON blob.`/document/{field}`

is the syntax for an operation performed on a specific field, such as translating the`/document/Description`

field, seen in the previous example.`/document/pages/*`

or`/document/sentences/*`

become the context if you're breaking a large document into smaller chunks for processing. If "context" is`/document/pages/*`

, the skill executes once over each page in the document. Because there might be more than one page or sentence, you can append`/*`

to catch them all.`/document/normalized_images/*`

is created during document cracking if the document contains images. All paths to images start with normalized_images. Since there are often multiple images embedded in a document, append`/*`

.

Examples in the remainder of this article are based on the "content" field generated automatically by [Azure blob indexers](search-how-to-index-azure-blob-storage) as part of the [document cracking](search-indexer-overview#document-cracking) phase. When referring to documents from a Blob container, use a format such as `"/document/content"`

, where the "content" field is part of the "document".

## Example 1: Simple annotation reference

In Azure Blob Storage, suppose you have various files containing references to people's names that you want to extract using entity recognition. In the following skill definition, `"/document/content"`

is the textual representation of the entire document, and "people" is an extraction of full names for entities identified as persons.

Because the default context is `"/document"`

, the list of people can now be referenced as `"/document/people"`

. In this specific case `"/document/people"`

is an annotation, which could now be mapped to a field in an index, or used in another skill in the same skillset.

```
{
"@odata.type": "#Microsoft.Skills.Text.V3.EntityRecognitionSkill",
"categories": [ "Person"],
"defaultLanguageCode": "en",
"inputs": [
{
"name": "text",
"source": "/document/content"
}
],
"outputs": [
{
"name": "persons",
"targetName": "people"
}
]
}
```


## Example 2: Reference an array within a document

This example builds on the previous one, showing you how to invoke an enrichment step multiple times over the same document. Assume the previous example generated an array of strings with 10 people names from a single document. A reasonable next step might be a second enrichment that extracts the last name from a full name. Because there are 10 names, you want this step to be called 10 times in this document, once for each person.

To invoke the right number of iterations, set the context as `"/document/people/*"`

, where the asterisk (`"*"`

) represents all the nodes in the enriched document as descendants of `"/document/people"`

. Although this skill is only defined once in the skills array, it's called for each member within the document until all members are processed.

```
{
"@odata.type": "#Microsoft.Skills.Custom.WebApiSkill",
"description": "Fictitious skill that gets the last name from a full name",
"uri": "http://names.azurewebsites.net/api/GetLastName",
"context" : "/document/people/*",
"defaultLanguageCode": "en",
"inputs": [
{
"name": "fullname",
"source": "/document/people/*"
}
],
"outputs": [
{
"name": "lastname",
"targetName": "last"
}
]
}
```


When annotations are arrays or collections of strings, you might want to target specific members rather than the array as a whole. The previous example generates an annotation called `"last"`

under each node represented by the context. If you want to refer to this family of annotations, you could use the syntax `"/document/people/*/last"`

. If you want to refer to a particular annotation, you could use an explicit index: `"/document/people/1/last`

" to reference the last name of the first person identified in the document. Notice that in this syntax arrays are "0 indexed".

## Example 3: Reference members within an array

Sometimes you need to group all annotations of a particular type to pass them to a particular skill. Consider a hypothetical custom skill that identifies the most common last name from all the last names extracted in Example 2. To provide just the last names to the custom skill, specify the context as `"/document"`

and the input as `"/document/people/*/lastname"`

.

Notice that the cardinality of `"/document/people/*/lastname"`

is larger than that of document. There might be 10 lastname nodes while there's only one document node for this document. In that case, the system will automatically create an array of `"/document/people/*/lastname"`

containing all of the elements in the document.

```
{
"@odata.type": "#Microsoft.Skills.Custom.WebApiSkill",
"description": "Fictitious skill that gets the most common string from an array of strings",
"uri": "http://names.azurewebsites.net/api/MostCommonString",
"context" : "/document",
"inputs": [
{
"name": "strings",
"source": "/document/people/*/lastname"
}
],
"outputs": [
{
"name": "mostcommon",
"targetName": "common-lastname"
}
]
}
```


## Tips for annotation path troubleshooting

If you're having trouble with specifying skill inputs, these tips might help you move forward:

[Run the Import data wizard](search-import-data-portal)over your data to review the skillset definitions and field mappings that the wizard generates.[Start a debug session](cognitive-search-how-to-debug-skillset)on a skillset to view the structure of an enriched document. You can edit the paths and other parts of the skill definition, and then run the skill to validate your changes.


---

<!-- DOCUMENTO FUSIONADO: hybrid-search-ranking.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/hybrid-search-ranking -->

# Relevance scoring in hybrid search using Reciprocal Rank Fusion (RRF)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Reciprocal Rank Fusion (RRF) is an algorithm that evaluates the search scores from multiple, previously ranked results to produce a unified result set. In Azure AI Search, RRF is used when two or more queries execute in parallel. Namely, for [hybrid queries](hybrid-search-overview) and for [multiple vector queries](vector-search-overview). Each individual query produces a ranked result set, and RRF merges and homogenizes the rankings into a single result set for the query response.

RRF is based on the concept of *reciprocal rank*, which is the inverse of the rank of the first relevant document in a list of search results. The goal of the technique is to take into account the position of the items in the original rankings and give higher importance to items that are ranked higher in multiple lists. This approach can help improve the overall quality and reliability of the final ranking, making it more useful for the task of fusing multiple ordered search results.

## How RRF ranking works

RRF works by taking the search results from multiple methods, assigning a reciprocal rank score to each document in the results, and then combining the scores to create a new ranking. The concept is that documents appearing in the top positions across multiple search methods are likely to be more relevant and should be ranked higher in the combined result.

Here's a simple explanation of the RRF process:

Get ranked search results from multiple queries running in parallel.

Assign reciprocal rank scores for results in each of the ranked lists. RRF generates a new

`@search.score`

for each match in each result set. For each document in the search results, the engine assigns a reciprocal rank score based on its position in the list. The score is calculated as`1/(rank + k)`

, where`rank`

is the position of the document in the list and`k`

is a constant. Experiments show the algorithm performs best when you set`k`

to a small value, such as 60.**Note that this**`k`

value is a constant in the RRF algorithm and entirely separate from the`k`

that controls the number of nearest neighbors.Combine scores. For each document, the engine sums the reciprocal rank scores obtained from each search system, producing a combined score for each document.

The engine ranks documents based on combined scores and sorts them. The resulting list is the fused ranking.


Only fields marked as `searchable`

in the index, or `searchFields`

in the query, are used for scoring. Only fields marked as `retrievable`

, or fields specified in `select`

in the query, are returned in search results, along with their search score.

### Parallel query execution

RRF is used anytime there's more than one query execution. The following examples illustrate query patterns where parallel query execution occurs:

- A full-text query, plus one vector query (simple hybrid scenario), equals two query executions.
- A full-text query, plus one vector query targeting two vector fields, equals three query executions.
- A full-text query, plus two vector queries targeting five vector fields, equals 11 query executions.

## Scores in hybrid search results

Whenever results are ranked, the `@search.score`

property contains the value used to order the results. Scores are generated by ranking algorithms that vary for each method. Each algorithm has its own range and magnitude.

The following chart identifies the scoring property returned on each match, algorithm, and range of scores for each relevance ranking algorithm. For more information and a diagram of the scoring workflow, see [Relevance in Azure AI Search](search-relevance-overview).

| Search method | Parameter | Scoring algorithm | Range |
|---|---|---|---|
| full-text search | `@search.score` |
BM25 algorithm | No upper limit. |
| vector search | `@search.score` |
HNSW algorithm, using the similarity metric specified in the HNSW configuration. | 0.333 - 1.00 (Cosine), 0 to 1 for Euclidean and DotProduct. |
| hybrid search | `@search.score` |
RRF algorithm | Upper limit is bounded by the number of queries being fused, with each query contributing a maximum of approximately `1/k` to the RRF score (this is the `k` parameter in the RRF algorithm, not the vector query). For example, merging three queries produces higher RRF scores than if only two search results are merged. |
| semantic ranking | `@search.rerankerScore` |
Semantic ranking | 0.00 - 4.00 |

Semantic ranking occurs after RRF merging of results. Its score (`@search.rerankerScore`

) is always reported separately in the query response. Semantic ranker can rerank full text and hybrid search results, assuming those results include fields having semantically rich content. It can rerank pure vector queries if the search documents include text fields that contain semantically relevant content.

## Unpack a search score into subscores

You can deconstruct a search score to view its subscores. For vector queries, this information can help you determine an appropriate value for [vector weighting](vector-search-how-to-query#vector-weighting) or [setting minimum thresholds](vector-search-how-to-query#set-thresholds-to-exclude-low-scoring-results-preview).

To get subscores:

Use the

[Search Documents REST API](/en-us/rest/api/searchservice/documents/search-post#request-body)or an Azure SDK package that provides the feature.Modify a query request, adding a new

`debug`

parameter set to either`vector`

,`semantic`

if using semantic ranker, or`all`

.

Here's an example of hybrid query that returns subscores in debug mode:

```
POST https://{{search-service-name}}.search.windows.net/indexes/{{index-name}}/docs/search?api-version=2025-09-01
{
"vectorQueries": [
{
"vector": [
-0.009154141,
0.018708462,
. . .
-0.02178128,
-0.00086512347
],
"fields": "DescriptionVector",
"kind": "vector",
"exhaustive": true,
"k": 10
},
{
"vector": [
-0.009154141,
0.018708462,
. . .
-0.02178128,
-0.00086512347
],
"fields": "DescriptionVector",
"kind": "vector",
"exhaustive": true,
"k": 10
}
],
"search": "historic hotel walk to restaurants and shopping",
"select": "HotelName, Description, Address/City",
"debug": "vector",
"top": 10
}
```


## Weighted scores

You can also [weight vector queries](vector-search-how-to-query#vector-weighting) to increase or decrease their importance in a hybrid query.

Recall that when computing RRF for a certain document, the search engine looks at the rank of that document for each result set where it shows up. Assume a document shows up in three separate search results, where the results are from two vector queries and one text BM25-ranked query. The position of the document varies in each result.

| Match found | Position in results | @search.score | weight multiplier | @search.score (weighted) |
|---|---|---|---|---|
| vector results one | position 1 | 0.8383955 | 0.5 | 0.41919775 |
| vector results two | position 5 | 0.81514114 | 2.0 | 1.63028228 |
| BM25 results | position 10 | 0.8577363 | NA | 0.8577363 |

The document's position in each result set corresponds to an initial score, which is added up to create the final RRF score for that document.

If you add vector weighting, the initial scores are subject to a weighting multiplier that increases or decreases the score. The default is 1.0, which means no weighting and the initial score is used as-is in RRF scoring. However, if you add a weight of 0.5, the score is reduced and that result becomes less important in the combined ranking. Conversely, if you add a weight of 2.0, the score becomes a larger factor in the overall RRF score.

In this example, the `@search.score`

(weighted) values go to the RRF ranking model.

## Number of ranked results in a hybrid query response

By default, if you aren't using pagination, the search engine returns the top 50 highest ranking matches for full-text search, and the most similar `k`

matches for vector search. In a hybrid query, `top`

determines the number of results in the response. Based on defaults, the top 50 highest ranked matches of the unified result set are returned.

Often, the search engine finds more results than `top`

and `k`

. To return more results, use the paging parameters `top`

, `skip`

, and `next`

. Paging is how you determine the number of results on each logical page and navigate through the full payload. You can [set maxTextRecallSize](hybrid-search-how-to-query#set-maxtextrecallsize-and-countandfacetmode) to larger values (the default is 1,000) to return more results from the text side of hybrid query.

By default, full-text search is subject to a maximum limit of 1,000 matches (see [API response limits](search-limits-quotas-capacity#api-response-limits)). Once 1,000 matches are found, the search engine no longer looks for more.

For more information, see [How to work with search results](search-pagination-page-layout).
