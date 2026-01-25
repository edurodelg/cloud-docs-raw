---
source_url: https://learn.microsoft.com/en-us/azure/search/hybrid-search-how-to-query
fetched_at: 2026-01-25T02:04:13.581323
---

# Create a hybrid query in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Hybrid search](hybrid-search-overview) combines text (keyword) and vector queries in a single search request. Both queries execute in parallel. The results are merged and reordered by new search scores, using [Reciprocal Rank Fusion (RRF)](hybrid-search-ranking) to return a unified result set. In many cases, [per benchmark tests](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/azure-ai-search-outperforming-vector-search-with-hybrid-retrieval-and-reranking/3929167), hybrid queries with semantic ranking return the most relevant results.

In this article, learn how to:

- Set up a basic hybrid request
- Add parameters and filters
- Improve relevance using semantic ranking or vector weights
- Optimize query behaviors by controlling inputs (
`maxTextRecallSize`

)

By the end of this article, you can execute hybrid queries that combine keyword and vector search with optional semantic ranking.

Tip

For immediate code examples, skip to [Set up a hybrid query](#set-up-a-hybrid-query).

## Prerequisites

An Azure subscription.

[Create one for free](https://azure.microsoft.com/free/).An Azure AI Search service.

[Create a service](search-create-service-portal)or[find an existing service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).A search index containing

`searchable`

vector and nonvector fields. We recommend theto create an index quickly. Otherwise, see**Import data (new)**wizard[Create an index](search-how-to-create-search-index)and[Add vector fields to a search index](vector-search-how-to-create-index).**Permissions**: You need**Search Index Data Reader**to query an index. To create or update an index, you need**Search Index Data Contributor**. For more information, see[Connect using roles](search-security-rbac).**SDK installation (optional)**:- Python:
`pip install azure-search-documents`

- C#:
`dotnet add package Azure.Search.Documents`


- Python:
(Optional) If you want the

[semantic ranker](semantic-search-overview), your search service must have the[semantic ranker enabled](semantic-how-to-enable-disable).(Optional) If you want built-in text-to-vector conversion of a query string,

[create and assign a vectorizer](vector-search-how-to-configure-vectorizer)to vector fields in the search index.

## Choose an API or tool

Search Explorer in the Azure portal (supports both stable and preview API search syntax) has a JSON view that lets you paste in a hybrid request.

Newer stable or preview packages of the Azure SDKs (see change logs for SDK feature support).

[Stable REST APIs](/en-us/rest/api/searchservice/documents/search-post)or a recent preview API version if you're using preview features like[maxTextRecallSize and countAndFacetMode(preview)](#set-maxtextrecallsize-and-countandfacetmode).For readability, we use REST examples to explain how the APIs work. You can use a REST client like Visual Studio Code with the REST extension to build hybrid queries. You can also use the Azure SDKs. For more information, see

[Quickstart: Vector search](search-get-started-vector).

## Set up a hybrid query

This section explains the basic structure of a hybrid query and how to set one up in either Search Explorer or for execution in a REST client.

Results are returned in plain text, including vectors in fields marked as `retrievable`

. Because numeric vectors aren't useful in search results, choose other fields in the index as a proxy for the vector match. For example, if an index has "descriptionVector" and "descriptionText" fields, the query can match on "descriptionVector" but the search result can show "descriptionText". Use the `select`

parameter to specify only human-readable fields in the results.

Sign in to the

[Azure portal](https://portal.azure.com)and find your search service.Under

**Search management**>**Indexes**, select an index that has vectors and non-vector content.[Search Explorer](search-explorer)is the first tab.Under

**View**, switch to**JSON view**so that you can paste in a vector query.Replace the default query template with a hybrid query. A basic hybrid query has a text query specified in

`search`

, and a vector query specified under`vectorQueries.vector`

. The text query and vector query can be equivalent or divergent, but it's common for them to share the same intent.This example is from the

[vector quickstart](https://raw.githubusercontent.com/Azure-Samples/azure-search-rest-samples/refs/heads/main/Quickstart-vectors/az-search-quickstart-vectors.rest)that has vector and nonvector content, and several query examples. For brevity, the vector is truncated in this article.`{ "search": "historic hotel walk to restaurants and shopping", "vectorQueries": [ { "vector": [0.01944167, 0.0040178085, -0.007816401 ... <remaining values omitted> ], "k": 7, "fields": "DescriptionVector", "kind": "vector", "exhaustive": true } ] }`

Select

**Search**.Tip

Search results are easier to read if you hide the vectors. In

**Query Options**, turn on**Hide vector values in search results**.Here's another version of the query. This one adds a

`count`

for the number of matches found, a`select`

parameter for choosing specific fields, and a`top`

parameter to return the top seven results.`{ "count": true, "search": "historic hotel walk to restaurants and shopping", "select": "HotelId, HotelName, Category, Tags, Description", "top": 7, "vectorQueries": [ { "vector": [0.01944167, 0.0040178085, -0.007816401 ... <remaining values omitted> ], "k": 7, "fields": "DescriptionVector", "kind": "vector", "exhaustive": true } ] }`


## Set maxTextRecallSize and countAndFacetMode

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

A hybrid query can be tuned to control how much of each subquery contributes to the combined results. Setting `maxTextRecallSize`

specifies how many BM25-ranked results are passed to the hybrid ranking model.

If you use `maxTextRecallSize`

, you might also want to set `CountAndFacetMode`

. This parameter determines whether the `count`

and `facets`

should include all documents that matched the search query, or only those documents retrieved within the `maxTextRecallSize`

window. The default value is "countAllResults".

We recommend the [latest preview REST API](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true) for setting these options.

Tip

Another approach for hybrid query tuning is [vector weighting](vector-search-how-to-query#vector-weighting), used to increase the importance of vector queries in the request.

Use

[Search - POST (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true)or[Search - GET (preview)](/en-us/rest/api/searchservice/documents/search-get?view=rest-searchservice-2025-11-01-preview&preserve-view=true)to specify preview parameters.Add a

`hybridSearch`

query parameter object to set the maximum number of documents recalled through the BM25-ranked results of a hybrid query. It has two properties:`maxTextRecallSize`

specifies the number of BM25-ranked results to provide to the Reciprocal Rank Fusion (RRF) ranker used in hybrid queries. The default is 1,000. The maximum is 10,000.`countAndFacetMode`

reports the counts for the BM25-ranked results (and for facets if you're using them). The default is all documents that match the query. Optionally, you can scope "count" to the`maxTextRecallSize`

.

Set

`maxTextRecallSize`

:Decrease

`maxTextRecallSize`

if vector similarity search is generally outperforming the text-side of the hybrid query.Increase

`maxTextRecallSize`

if you have a large index, and the default isn't capturing a sufficient number of results. With a larger BM25-ranked result set, you can also set`top`

,`skip`

, and`next`

to retrieve portions of those results.


The following REST examples show two use-cases for setting `maxTextRecallSize`

.

The first example reduces `maxTextRecallSize`

to 100, limiting the text side of the hybrid query to just 100 document. It also sets `countAndFacetMode`

to include only those results from `maxTextRecallSize`

.

```
POST https://[service-name].search.windows.net/indexes/[index-name]/docs/search?api-version=2025-11-01-preview
{
"vectorQueries": [
{
"kind": "vector",
"vector": [1.0, 2.0, 3.0],
"fields": "my_vector_field",
"k": 10
}
],
"search": "hello world",
"hybridSearch": {
"maxTextRecallSize": 100,
"countAndFacetMode": "countRetrievableResults"
}
}
```


The second example raises `maxTextRecallSize`

to 5,000. It also uses top, skip, and next to pull results from large result sets. In this case, the request pulls in BM25-ranked results starting at position 1,500 through 2,000 as the text query contribution to the RRF composite result set.

```
POST https://[service-name].search.windows.net/indexes/[index-name]/docs/search?api-version=2025-11-01-preview
{
"vectorQueries": [
{
"kind": "vector",
"vector": [1.0, 2.0, 3.0],
"fields": "my_vector_field",
"k": 10
}
],
"search": "hello world",
"top": 500,
"skip": 1500,
"next": 500,
"hybridSearch": {
"maxTextRecallSize": 5000,
"countAndFacetMode": "countRetrievableResults"
}
}
```


**Reference**: [hybridSearch](/en-us/rest/api/searchservice/documents/search-post#hybridsearch) | [maxTextRecallSize](/en-us/rest/api/searchservice/documents/search-post#hybridsearch) | [countAndFacetMode](/en-us/rest/api/searchservice/documents/search-post#hybridsearch)

## Examples of hybrid queries

This section has multiple query examples that illustrate hybrid query patterns.

### Example: Hybrid search with filter

This example adds a filter, which is applied to the `filterable`

nonvector fields of the search index.

```
POST https://{{search-service-name}}.search.windows.net/indexes/{{index-name}}/docs/search?api-version=2025-09-01
Content-Type: application/json
api-key: {{admin-api-key}}
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
"k": 10
}
],
"search": "historic hotel walk to restaurants and shopping",
"vectorFilterMode": "preFilter",
"filter": "ParkingIncluded",
"top": "10"
}
```


**Key points:**

Filters are applied to the content of filterable fields. In this example, the ParkingIncluded field is a boolean and it's marked as

`filterable`

in the index schema.In hybrid queries, filters can be applied before query execution to reduce the query surface or after query execution to trim results.

`"preFilter"`

is the default. To use`postFilter`

or`strictPostFilter`

(preview), set the[filter processing mode](vector-search-filters)as shown in this example.When you postfilter query results, the number of results might be less than top-n.


**Reference**: [filter](/en-us/rest/api/searchservice/documents/search-post#searchrequest) | [vectorFilterMode](/en-us/rest/api/searchservice/documents/search-post#vectorfiltermode)

### Example: Hybrid search with filters targeting vector subqueries (preview)

Using the [latest preview REST API](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true), you can override a global filter on the search request by applying a secondary filter that targets just the vector subqueries in a hybrid request.

This feature provides fine-grained control by ensuring that filters only influence the vector search results, leaving keyword-based search results unaffected.

The targeted filter fully overrides the global filter, including any filters used for [security trimming](search-security-trimming-for-azure-search) or geospatial search. In cases where global filters are required, such as security trimming, you must explicitly include these filters in both the top-level filter and in each vector-level filter to ensure security and other constraints are consistently enforced.

To apply targeted vector filters:

Use the

[latest preview Search Documents REST API](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true#request-body)or an Azure SDK beta package that provides the feature.Modify a query request, adding a new

`vectorQueries.filterOverride`

parameter set to an[OData filter expression](search-query-odata-filter).

Here's an example of hybrid query that adds a filter override. The global filter "Rating gt 3" is replaced at run time by the `filterOverride`

.

```
POST https://{{search-service-name}}.search.windows.net/indexes/{{index-name}}/docs/search?api-version=2025-11-01-preview
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
"filterOverride": "Address/City eq 'Seattle'",
"k": 10
}
],
"search": "historic hotel walk to restaurants and shopping",
"select": "HotelName, Description, Address/City, Rating",
"filter": "Rating gt 3",
"debug": "vector",
"top": 10
}
```


### Example: Semantic hybrid search

Assuming that you [have semantic ranker](semantic-how-to-enable-disable) and your index definition includes a [semantic configuration](semantic-how-to-query-request), you can formulate a query that includes vector search and keyword search, with semantic ranking over the merged result set. Optionally, you can add captions and answers.

Whenever you use semantic ranking with vectors, make sure `k`

is set to 50. Semantic ranker uses up to 50 matches as input. Specifying less than 50 deprives the semantic ranking models of necessary inputs.

```
POST https://{{search-service-name}}.search.windows.net/indexes/{{index-name}}/docs/search?api-version=2025-09-01
Content-Type: application/json
api-key: {{admin-api-key}}
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
"k": 50
}
],
"search": "historic hotel walk to restaurants and shopping",
"select": "HotelName, Description, Tags",
"queryType": "semantic",
"semanticConfiguration": "my-semantic-config",
"captions": "extractive",
"answers": "extractive",
"top": "50"
}
```


**Key points:**

Semantic ranker accepts up to 50 results from the merged response.

"queryType" and "semanticConfiguration" are required.

"captions" and "answers" are optional. Values are extracted from verbatim text in the results. An answer is only returned if the results include content having the characteristics of an answer to the query.


**Reference**: [queryType](/en-us/rest/api/searchservice/documents/search-post#querytype) | [semanticConfiguration](/en-us/rest/api/searchservice/documents/search-post#searchrequest) | [captions](/en-us/rest/api/searchservice/documents/search-post#querycaption) | [answers](/en-us/rest/api/searchservice/documents/search-post#queryanswer)

### Example: Semantic hybrid search with filter

Here's the last query in the collection. It's the same semantic hybrid query as the previous example, but with a filter.

```
POST https://{{search-service-name}}.search.windows.net/indexes/{{index-name}}/docs/search?api-version=2025-09-01
Content-Type: application/json
api-key: {{admin-api-key}}
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
"k": 50
}
],
"search": "historic hotel walk to restaurants and shopping",
"select": "HotelName, Description, Tags",
"queryType": "semantic",
"semanticConfiguration": "my-semantic-config",
"captions": "extractive",
"answers": "extractive",
"filter": "ParkingIncluded",
"vectorFilterMode": "preFilter",
"top": "50"
}
```


**Key points:**

The filter mode can affect the number of results available to the semantic reranker. As a best practice, it's smart to give the semantic ranker the maximum number of documents (50). If prefilters or postfilters are too selective, you might be underserving the semantic ranker by giving it fewer than 50 documents to work with.

`preFilter`

is applied before query execution. If prefilter reduces the search area to 100 documents, the vector query executes over the`DescriptionVector`

field for those 100 documents, returning the k=50 best matches. Those 50 matching documents then pass to RRF for merged results, and then to semantic ranker.`postFilter`

is applied after query execution. If k=50 returns 50 matches on the vector query side, followed by a post-filter applied to the 50 matches, your results are reduced by the number of documents that meet filter criteria. This leaves you with fewer than 50 documents to pass to semantic ranker. Keep this in mind if you're using semantic ranking. The semantic ranker works best if it has 50 documents as input.`strictPostFilter`

(preview) is applied on the unfiltered top-`k`

results after query execution. It always returns less than or equal to`k`

documents. If the unfiltered k=50 returns 50 unfiltered results, and the filter matches 30 documents, only 30 documents are returned in the result set, even if the index has more than 30 documents that match the filter. Since this mode has the greatest reduction in recall, we don't recommend that you use it with semantic ranker.

## Configure a query response

When you're setting up the hybrid query, think about the response structure. The search engine ranks the matching documents and returns the most relevant results. The response is a flattened rowset. Parameters on the query determine which fields are in each row and how many rows are in the response.

### Fields in a response

Search results are composed of `retrievable`

fields from your search index. A result is either:

- All
`retrievable`

fields (a REST API default). - Fields explicitly listed in a
`select`

parameter on the query.

The examples in this article used a `select`

statement to specify text (nonvector) fields in the response.

Note

Vectors aren't reverse engineered into human readable text, so avoid returning them in the response. Instead, choose nonvector fields that are representative of the search document. For example, if the query targets a "DescriptionVector" field, return an equivalent text field if you have one ("Description") in the response.

### Number of results

A query might match to any number of documents, as many as all of them if the search criteria are weak (for example "search=*" for a null query). Because it's seldom practical to return unbounded results, you should specify a maximum for the *overall response*:

`"top": n`

results for keyword-only queries (no vector)`"k": n`

results for vector-only queries`"top": n`

results for hybrid queries (with or without semantic) that include a "search" parameter

Both `k`

and `top`

are optional. Unspecified, the default number of results in a response is 50. You can set `top`

and `skip`

to [page through more results](search-pagination-page-layout#paging-results) or change the default.

Note

If you're using hybrid search in 2024-05-01-preview API, you can control the number of results from the keyword query using [maxTextRecallSize](#set-maxtextrecallsize-and-countandfacetmode). Combine this with a setting for `k`

to control the representation from each search subsystem (keyword and vector).

### Semantic ranker results

Note

The semantic ranker can take up to 50 results.

If you're using semantic ranker in 2024-05-01-preview or later, it's a best practice to set `k`

and `maxTextRecallSize`

to sum to at least 50 total. You can then restrict the results returned to the user with the `top`

parameter.

If you're using semantic ranker in previous APIs do the following:

- For keyword-only search (no vectors) set
`top`

to 50 - For hybrid search set
`k`

to 50, to ensure that the semantic ranker gets at least 50 results.

### Ranking

Multiple sets are created for hybrid queries, with or without the optional [semantic reranking](semantic-search-overview). Ranking of results is computed by Reciprocal Rank Fusion (RRF).

In this section, compare the responses between single vector search and simple hybrid search for the top result. The different ranking algorithms, HNSW's similarity metric and RRF is this case, produce scores that have different magnitudes. This behavior is by design. RRF scores can appear quite low, even with a high similarity match. Lower scores are a characteristic of the RRF algorithm. In a hybrid query with RRF, more of the reciprocal of the ranked documents are included in the results, given the relatively smaller score of the RRF ranked documents, as opposed to pure vector search.

**Single Vector Search**: @search.score for results ordered by cosine similarity (default vector similarity distance function).

```
{
"@search.score": 0.8399121,
"HotelId": "49",
"HotelName": "Swirling Currents Hotel",
"Description": "Spacious rooms, glamorous suites and residences, rooftop pool, walking access to shopping, dining, entertainment and the city center.",
"Category": "Luxury",
"Address": {
"City": "Arlington"
}
}
```


**Hybrid Search**: @search.score for hybrid results ranked using Reciprocal Rank Fusion.

```
{
"@search.score": 0.032786883413791656,
"HotelId": "49",
"HotelName": "Swirling Currents Hotel",
"Description": "Spacious rooms, glamorous suites and residences, rooftop pool, walking access to shopping, dining, entertainment and the city center.",
"Category": "Luxury",
"Address": {
"City": "Arlington"
}
}
```


## Troubleshoot hybrid queries

Use the following table to diagnose common issues with hybrid queries.

| Issue | Possible cause | Resolution |
|---|---|---|
| Empty results | Vector field name mismatch or missing index data | Verify `fields` in `vectorQueries` matches a vector field in your index schema. Check that documents contain vector data. |
| Low RRF scores | Normal RRF behavior | RRF scores are inherently lower than similarity scores. A score of 0.03 can still indicate a strong match. |
| Vector results dominate | Text query underperforming | Increase `maxTextRecallSize` to include more BM25 results, or adjust vector weighting. |
| Text results dominate | Vector similarity too low | Check embedding quality. Ensure query vector uses the same model as document vectors. |
| Semantic ranker returns fewer results | Insufficient input documents | Set `k` to at least 50 when using semantic ranking. Check that filters aren't too restrictive. |
| Filter not applied to vectors | Using global filter only | For vector-specific filtering, use `filterOverride` in the vector query (preview). |
| Unexpected field in results | `select` parameter missing |
Add `select` to specify which fields to return. Exclude vector fields for readability. |

## Related content

[Hybrid search overview](hybrid-search-overview)[Hybrid search ranking with RRF](hybrid-search-ranking)[Vector search how-to](vector-search-how-to-query)[Semantic ranking](semantic-how-to-query-request)[Vector search filters](vector-search-filters)- Review vector demo code for
[Python](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-python),[C#](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-dotnet), or[JavaScript](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-javascript)