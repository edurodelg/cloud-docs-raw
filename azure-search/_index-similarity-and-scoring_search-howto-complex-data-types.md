---
merged_at: 2026-01-25T02:11:58.529204
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index-similarity-and-scoring.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/index-similarity-and-scoring -->

# Relevance in keyword search (BM25 scoring)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the BM25 relevance scoring algorithm used to compute search scores for [full text search](search-lucene-query-architecture). BM25 relevance applies to full text search only. Filter queries, autocomplete and suggested queries, wildcard search, and fuzzy search queries aren't scored or ranked for relevance.

## Scoring algorithms used in full text search

Azure AI Search provides the following scoring algorithms for full text search:

| Algorithm | Usage | Range |
|---|---|---|
`BM25Similarity` |
Fixed algorithm on all search services created after July 2020. You can configure this algorithm, but you can't switch to an older one (classic). | Unbounded. |
`ClassicSimilarity` |
Default on older search services that predate July 2020. On older services, you can
|

Both BM25 and Classic are TF-IDF-like retrieval functions that use the term frequency (TF) and the inverse document frequency (IDF) as variables to calculate relevance scores for each document-query pair, which is then used for ranking results. While conceptually similar to classic, BM25 is rooted in probabilistic information retrieval that produces more intuitive matches, as measured by user research.

BM25 offers [advanced customization options](index-ranking-similarity), such as allowing the user to decide how the relevance score scales with the term frequency of matched terms.

## How BM25 ranking works

Relevance scoring refers to the computation of a search score (**@search.score**) that serves as an indicator of an item's relevance in the context of the current query. The range is unbounded. However, the higher the score, the more relevant the item.

The search score is computed based on statistical properties of the string input and the query itself. Azure AI Search finds documents that match on search terms (some or all, depending on [searchMode](/en-us/rest/api/searchservice/documents/search-post#searchrequest)), favoring documents that contain many instances of the search term. The search score goes up even higher if the term is rare across the data index, but common within the document. The basis for this approach to computing relevance is known as *TF-IDF or* term frequency-inverse document frequency.

Search scores can be repeated throughout a result set. When multiple hits have the same search score, the ordering of the same scored items is undefined and not stable. Run the query again, and you might see items shift position, especially if you're using the free service or a billable service with multiple replicas. Given two items with an identical score, there's no guarantee that one appears first.

To break the tie among repeating scores, you can add an [ $orderby clause](search-query-odata-orderby) to first order by score, then order by another sortable field (for example,

`$orderby=search.score() desc,Rating desc`

).Only fields marked as `searchable`

in the index, or `searchFields`

in the query, are used for scoring. Only fields marked as `retrievable`

, or fields specified in `select`

in the query, are returned in search results, along with their search score.

Note

A `@search.score = 1`

indicates an un-scored or un-ranked result set. The score is uniform across all results. Un-scored results occur when the query form is fuzzy search, wildcard or regex queries, or an empty search (`search=*`

, sometimes paired with filters, where the filter is the primary means for returning a match).

The following video segment fast-forwards to an explanation of the generally available ranking algorithms used in Azure AI Search. You can watch the full video for more background.

## Scores in a text results

Whenever results are ranked, ** @search.score** property contains the value used to order the results.

The following table identifies the scoring property, algorithm, and range.

| Search method | Parameter | Scoring algorithm | Range |
|---|---|---|---|
| full text search | `@search.score` |
BM25 algorithm, using the
|

### Score variation

Search scores convey general sense of relevance, reflecting the strength of match relative to other documents in the same result set. But scores aren't always consistent from one query to the next, so as you work with queries, you might notice small discrepancies in how search documents are ordered. There are several explanations for why this might occur.

| Cause | Description |
|---|---|
| Identical scores | If multiple documents have the same score, any one of them might appear first. |
| Data volatility | Index content varies as you add, modify, or delete documents. Term frequencies will change as index updates are processed over time, affecting the search scores of matching documents. |
| Multiple replicas | For services using multiple replicas, queries are issued against each replica in parallel. The index statistics used to calculate a search score are calculated on a per-replica basis, with results merged and ordered in the query response. Replicas are mostly mirrors of each other, but statistics can differ due to small differences in state. For example, one replica might have deleted documents contributing to their statistics, which were merged out of other replicas. Typically, differences in per-replica statistics are more noticeable in smaller indexes. The following section provides more information about this condition. |

## Sharding effects on query results

A *shard* is a chunk of an index. Azure AI Search subdivides an index into *shards* to make the process of adding partitions faster (by moving shards to new search units). On a search service, shard management is an implementation detail and nonconfigurable, but knowing that an index is sharded helps to understand the occasional anomalies in ranking and autocomplete behaviors:

Ranking anomalies: Search scores are computed at the shard level first, and then aggregated up into a single result set. Depending on the characteristics of shard content, matches from one shard might be ranked higher than matches in another one. If you notice counter intuitive rankings in search results, it's most likely due to the effects of sharding, especially if indexes are small. You can avoid these ranking anomalies by choosing to

[compute scores globally across the entire index](index-similarity-and-scoring#scoring-statistics-and-sticky-sessions), but doing so will incur a performance penalty.Autocomplete anomalies: Autocomplete queries, where matches are made on the first several characters of a partially entered term, accept a fuzzy parameter that forgives small deviations in spelling. For autocomplete, fuzzy matching is constrained to terms within the current shard. For example, if a shard contains "Microsoft" and a partial term of "micro" is entered, the search engine will match on "Microsoft" in that shard, but not in other shards that hold the remaining parts of the index.


The following diagram shows the relationship between replicas, partitions, shards, and search units. It shows an example of how a single index is spanned across four search units in a service with two replicas and two partitions. Each of the four search units stores only half of the shards of the index. The search units in the left column store the first half of the shards, comprising the first partition, while those in the right column store the second half of the shards, comprising the second partition. Since there are two replicas, there are two copies of each index shard. The search units in the top row store one copy, comprising the first replica, while those in the bottom row store another copy, comprising the second replica.


The diagram above is only one example. Many combinations of partitions and replicas are possible, up to a maximum of 36 total search units.

Note

The number of replicas and partitions divides evenly into 12 (specifically, 1, 2, 3, 4, 6, 12). Azure AI Search pre-divides each index into 12 shards so that it can be spread in equal portions across all partitions. For example, if your service has three partitions and you create an index, each partition will contain four shards of the index. How Azure AI Search shards an index is an implementation detail, subject to change in future releases. Although the number is 12 today, you shouldn't expect that number to always be 12 in the future.

## Scoring statistics and sticky sessions

For scalability, Azure AI Search distributes each index horizontally through a sharding process, which means that [portions of an index are physically separate](#sharding-effects-on-query-results).

By default, the score of a document is calculated based on statistical properties of the data *within a shard*. This approach is generally not a problem for a large corpus of data, and it provides better performance than having to calculate the score based on information across all shards. That said, using this performance optimization could cause two very similar documents (or even identical documents) to end up with different relevance scores if they end up in different shards.

If you prefer to compute the score based on the statistical properties across all shards, you can do so by adding `scoringStatistics=global`

as a [query parameter](/en-us/rest/api/searchservice/documents/search-post) (or add `"scoringStatistics": "global"`

as a body parameter of the [query request](/en-us/rest/api/searchservice/documents/search-post)).

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2025-09-01
{
"search": "<query string>",
"scoringStatistics": "global"
}
```


Using `scoringStatistics`

will ensure that all shards in the same replica provide the same results. That said, different replicas can be slightly different from one another as they're always getting updated with the latest changes to your index. In some scenarios, you might want your users to get more consistent results during a "query session". In such scenarios, you can provide a `sessionId`

as part of your queries. The `sessionId`

is a unique string that you create to refer to a unique user session.

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2025-09-01
{
"search": "<query string>",
"sessionId": "<string>"
}
```


As long as the same `sessionId`

is used, a best-effort attempt is made to target the same replica, increasing the consistency of results your users will see.

Note

Reusing the same `sessionId`

values repeatedly can interfere with the load balancing of the requests across replicas and adversely affect the performance of the search service. The value used as sessionId can't start with a '_' character.

## Relevance tuning

In Azure AI Search, for keyword search and the text portion of a hybrid query, you can configure BM25 algorithm parameters plus tune search relevance and boost search scores through the following mechanisms.

| Approach | Implementation | Description |
|---|---|---|
|

[Scoring profiles](index-add-scoring-profiles)[Semantic ranking](semantic-search-overview)[featuresMode parameter](#featuresmode-parameter-preview)[custom scoring solution](https://github.com/Azure-Samples/search-ranking-tutorial).## featuresMode parameter (preview)

Note

The `featuresMode`

parameter isn't documented in the REST APIs, but you can use it on a preview REST API call to Search Documents for text (Keyword) search that's BM25-ranked.

[Search Documents (preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true) requests support a `featuresMode`

parameter that provides more detail about a BM25 relevance score at the field level. Whereas the `@searchScore`

is calculated for the document all-up (how relevant is this document in the context of this query), featuresMode reveals information about individual fields, as expressed in a `@search.features`

structure. The structure contains all fields used in the query (either specific fields through **searchFields** in a query, or all fields attributed as **searchable** in an index).

Valid values for featuresMode:

- "none" (default). No feature-level scoring details are returned.
- "enabled". Returns detailed scoring breakdowns per field

For each field, `@search.features`

give you the following values:

- Number of unique tokens found in the field
- Similarity score, or a measure of how similar the content of the field is, relative to the query term
- Term frequency, or the number of times the query term was found in the field

This parameter is especially useful when you're trying to understand why certain documents rank higher or lower in search results. It helps explain how different fields contribute to the overall score.

For a query that targets a "description" field, a request might look like this:

```
POST {{baseUrl}}/indexes/hotels-sample-index/docs/search?api-version=2025-11-01-preview HTTP/1.1
Content-Type: application/json
Authorization: Bearer {{accessToken}}
{
"search": "lake view",
"select": "HotelId, HotelName, Tags, Description",
"featuresMode": "enabled",
"searchFields": "Description, Tags",
"count": true
}
```


A response that includes `@search.features`

might look like the following example.

```
"value": [
{
"@search.score": 3.0860271,
"@search.features": {
"Description": {
"uniqueTokenMatches": 2.0,
"similarityScore": 3.0860272,
"termFrequency": 2.0
}
},
"HotelName": "Downtown Mix Hotel",
"Description": "Mix and mingle in the heart of the city. Shop and dine, mix and mingle in the heart of downtown, where fab lake views unite with a cheeky design.",
"Tags": [
"air conditioning",
"laundry service",
"free wifi"
]
},
{
"@search.score": 2.7294855,
"@search.features": {
"Description": {
"uniqueTokenMatches": 1.0,
"similarityScore": 1.6023184,
"termFrequency": 1.0
},
"Tags": {
"uniqueTokenMatches": 1.0,
"similarityScore": 1.1271671,
"termFrequency": 1.0
}
},
"HotelName": "Ocean Water Resort & Spa",
"Description": "New Luxury Hotel for the vacation of a lifetime. Bay views from every room, location near the pier, rooftop pool, waterfront dining & more.",
"Tags": [
"view",
"pool",
"restaurant"
]
}
]
```


You can consume these data points in [custom scoring solutions](https://github.com/Azure-Samples/search-ranking-tutorial) or use the information to debug search relevance problems.

## Number of ranked results in a full text query response

By default, if you aren't using pagination, the search engine returns the top 50 highest ranking matches for full text search. You can use the `top`

parameter to return a smaller or larger number of items (up to 1,000 in a single response). You can use `skip`

and `next`

to page results. Paging determines the number of results on each logical page and supports content navigation. For more information, see [Shape search results](search-pagination-page-layout).

If your full text query is part of a [hybrid query](hybrid-search-how-to-query), you can [set maxTextRecallSize](hybrid-search-how-to-query#set-maxtextrecallsize-and-countandfacetmode) to increase or decrease the number of results from the text side of the query.

Full text search is subject to a maximum limit of 1,000 matches (see [API response limits](search-limits-quotas-capacity#api-response-limits)). Once 1,000 matches are found, the search engine no longer looks for more.


---

<!-- DOCUMENTO FUSIONADO: search-howto-complex-data-types.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-howto-complex-data-types -->

# Model complex data types in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

External datasets used to populate an Azure AI Search index can come in many shapes. Sometimes they include hierarchical or nested substructures. Examples might include multiple addresses for a single customer, multiple colors and sizes for a single product, multiple authors of a single book, and so on. In modeling terms, you might see these structures referred to as *complex*, *compound*, *composite*, or *aggregate* data types. The term Azure AI Search uses for this concept is **complex type**. In Azure AI Search, complex types are modeled using **complex fields**. A complex field is a field that contains children (subfields) which can be of any data type, including other complex types. This works in a similar way as structured data types in a programming language.

Complex fields represent either a single object in the document, or an array of objects, depending on the data type. Fields of type `Edm.ComplexType`

represent single objects, while fields of type `Collection(Edm.ComplexType)`

represent arrays of objects.

Azure AI Search natively supports complex types and collections. These types allow you to model almost any JSON structure in an Azure AI Search index. In previous versions of Azure AI Search APIs, only flattened row sets could be imported. In the newest version, your index can now more closely correspond to source data. In other words, if your source data has complex types, your index can have complex types also.

To get started, we recommend the [hotels data set](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels), which you can load using an [import wizard](search-get-started-portal) in the Azure portal. The wizard detects complex types in the source and suggests an index schema based on the detected structures.

Note

Support for complex types became generally available starting in `api-version=2019-05-06`

.

If your search solution is built on earlier workarounds of flattened datasets in a collection, you should change your index to include complex types as supported in the newest API version. For more information about upgrading API versions, see [Upgrade to the newest REST API version](search-api-migration) or [Upgrade to the newest .NET SDK version](/en-us/previous-versions/azure/search/search-dotnet-sdk-migration-version-9).

## Example of a complex structure

The following JSON document is composed of simple fields and complex fields. Complex fields, such as `Address`

and `Rooms`

, have subfields. `Address`

has a single set of values for those subfields, since it's a single object in the document. In contrast, `Rooms`

has multiple sets of values for its subfields, one for each object in the collection.

```
{
"HotelId": "1",
"HotelName": "Stay-Kay City Hotel",
"Description": "Ideally located on the main commercial artery of the city in the heart of New York.",
"Tags": ["Free wifi", "on-site parking", "indoor pool", "continental breakfast"],
"Address": {
"StreetAddress": "677 5th Ave",
"City": "New York",
"StateProvince": "NY"
},
"Rooms": [
{
"Description": "Budget Room, 1 Queen Bed (Cityside)",
"RoomNumber": 1105,
"BaseRate": 96.99,
},
{
"Description": "Deluxe Room, 2 Double Beds (City View)",
"Type": "Deluxe Room",
"BaseRate": 150.99,
}
. . .
]
}
```


## Create complex fields

As with any index definition, you can use the Azure portal, [REST API](/en-us/rest/api/searchservice/indexes/create), or [.NET SDK](/en-us/dotnet/api/azure.search.documents.indexes.models.searchindex) to create a schema that includes complex types.

Other Azure SDKs provide samples in [Python](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/search/azure-search-documents/samples/sample_index_crud_operations.py), [Java](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/src/samples/java/com/azure/search/documents/indexes/CreateIndexExample.java), and [JavaScript](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/samples/v11/javascript/indexOperations.js).

Sign in to the

[Azure portal](https://portal.azure.com).On the search service

**Overview**page, select the**Indexes**tab.Open an existing index or create a new index.

Select the

**Fields**tab, and then select**Add field**. An empty field is added. If you're working with an existing fields collection, scroll down to set up the field.Give the field a name and set the type to either

`Edm.ComplexType`

or`Collection(Edm.ComplexType)`

.Select the ellipses on the far right, and then select either

**Add field**or**Add subfield**, and then assign attributes.

### Complex collection limits

During indexing, you can have a maximum of 3,000 elements across all complex collections within a single document. An element of a complex collection is a member of that collection. For Rooms (the only complex collection in the Hotel example), each room is an element. In the example above, if the "Stay-Kay City Hotel" had 500 rooms, the hotel document would have 500 room elements. For nested complex collections, each nested element is also counted, in addition to the outer (parent) element.

This limit applies only to complex collections, and not complex types (like Address) or string collections (like Tags).

## Update complex fields

All of the [reindexing rules](search-howto-reindex) that apply to fields in general still apply to complex fields. Adding a new field to a complex type doesn't require an index rebuild, but most other modifications do require a rebuild.

### Structural updates to the definition

You can add new subfields to a complex field at any time without the need for an index rebuild. For example, adding "ZipCode" to `Address`

or "Amenities" to `Rooms`

is allowed, just like adding a top-level field to an index. Existing documents have a null value for new fields until you explicitly populate those fields by updating your data.

Notice that within a complex type, each subfield has a type and can have attributes, just as top-level fields do

### Data updates

Updating existing documents in an index with the `upload`

action works the same way for complex and simple fields: all fields are replaced. However, `merge`

(or `mergeOrUpload`

when applied to an existing document) doesn't work the same across all fields. Specifically, `merge`

doesn't support merging elements within a collection. This limitation exists for collections of primitive types and complex collections. To update a collection, you need to retrieve the full collection value, make changes, and then include the new collection in the Index API request.

## Search complex fields in text queries

Free-form search expressions work as expected with complex types. If any searchable field or subfield anywhere in a document matches, then the document itself is a match.

Queries get more nuanced when you have multiple terms and operators, and some terms have field names specified, as is possible with the [Lucene syntax](query-lucene-syntax). For example, this query attempts to match two terms, "Portland" and "OR", against two subfields of the Address field:


`search=Address/City:Portland AND Address/State:OR`


Queries like this are *uncorrelated* for full-text search, unlike filters. In filters, queries over subfields of a complex collection are correlated using range variables in [ any or all](search-query-odata-collection-operators). The Lucene query above returns documents containing both "Portland, Maine" and "Portland, Oregon", along with other cities in Oregon. This happens because each clause applies to all values of its field in the entire document, so there's no concept of a "current subdocument". For more information on this, see


[Understanding OData collection filters in Azure AI Search](search-query-understand-collection-filters).

## Search complex fields in RAG queries

A RAG pattern passes search results to a chat model for generative AI and conversational search. By default, search results passed to an LLM are a flattened rowset. However, if your index has complex types, your query can provide those fields if you first convert the search results to JSON, and then pass the JSON to the LLM.

A partial example illustrates the technique:

- Indicate the fields you want in the prompt or in the query
- Make sure the fields are searchable and retrievable in the index
- Select the fields for the search results
- Format the results as JSON
- Send the request for chat completion to the model provider

```
import json
# Query is the question being asked. It's sent to the search engine and the LLM.
query="Can you recommend a few hotels that offer complimentary breakfast? Tell me their description, address, tags, and the rate for one room they have which sleep 4 people."
# Set up the search results and the chat thread.
# Retrieve the selected fields from the search index related to the question.
selected_fields = ["HotelName","Description","Address","Rooms","Tags"]
search_results = search_client.search(
search_text=query,
top=5,
select=selected_fields,
query_type="semantic"
)
sources_filtered = [{field: result[field] for field in selected_fields} for result in search_results]
sources_formatted = "\n".join([json.dumps(source) for source in sources_filtered])
response = openai_client.chat.completions.create(
messages=[
{
"role": "user",
"content": GROUNDED_PROMPT.format(query=query, sources=sources_formatted)
}
],
model=AZURE_DEPLOYMENT_MODEL
)
print(response.choices[0].message.content)
```


For the end-to-end example, see [classic RAG in Azure AI Search](https://github.com/Azure-Samples/azure-search-classic-rag/blob/main/README.md).

## Select complex fields

The `$select`

parameter is used to choose which fields are returned in search results. To use this parameter to select specific subfields of a complex field, include the parent field and subfield separated by a slash (`/`

).


`$select=HotelName, Address/City, Rooms/BaseRate`


Fields must be marked as Retrievable in the index if you want them in search results. Only fields marked as Retrievable can be used in a `$select`

statement.

## Filter, facet, and sort complex fields

The same [OData path syntax](query-odata-filter-orderby-syntax) used for filtering and fielded searches can also be used for faceting, sorting, and selecting fields in a search request. For complex types, rules apply that govern which subfields can be marked as sortable or facetable. For more information on these rules, see the [Create Index API reference](/en-us/rest/api/searchservice/indexes/create).

### Faceting subfields

Any subfield can be marked as facetable unless it is of type `Edm.GeographyPoint`

or `Collection(Edm.GeographyPoint)`

.

The document counts returned in the facet results are calculated for the parent document (a hotel), not the subdocuments in a complex collection (rooms). For example, suppose a hotel has 20 rooms of type "suite". Given this facet parameter `facet=Rooms/Type`

, the facet count is one for the hotel, not 20 for the rooms.

### Sorting complex fields

Sort operations apply to documents (Hotels) and not subdocuments (Rooms). When you have a complex type collection, such as Rooms, it's important to realize that you can't sort on Rooms at all. In fact, you can't sort on any collection.

Sort operations work when fields have a single value per document, whether the field is a simple field, or a subfield in a complex type. For example, `Address/City`

is allowed to be sortable because there's only one address per hotel, so `$orderby=Address/City`

sorts hotels by city.

### Filtering on complex fields

You can refer to subfields of a complex field in a filter expression. Just use the same [OData path syntax](query-odata-filter-orderby-syntax) that's used for faceting, sorting, and selecting fields. For example, the following filter returns all hotels in Canada:


`$filter=Address/Country eq 'Canada'`


To filter on a complex collection field, you can use a **lambda expression** with the [ any and all operators](search-query-odata-collection-operators). In that case, the


**range variable**of the lambda expression is an object with subfields. You can refer to those subfields with the standard OData path syntax. For example, the following filter returns all hotels with at least one deluxe room and all nonsmoking rooms:


`$filter=Rooms/any(room: room/Type eq 'Deluxe Room') and Rooms/all(room: not room/SmokingAllowed)`


As with top-level simple fields, simple subfields of complex fields can only be included in filters if they have the **filterable** attribute set to `true`

in the index definition. For more information, see the [Create Index API reference](/en-us/rest/api/searchservice/indexes/create).

### Workaround for the complex collection limit

Recall that Azure AI Search limits complex objects in a collection to 3,000 objects per document. Exceeding this limit results in the following message:

```
A collection in your document exceeds the maximum elements across all complex collections limit.
The document with key '1052' has '4303' objects in collections (JSON arrays).
At most '3000' objects are allowed to be in collections across the entire document.
Remove objects from collections and try indexing the document again."
```


If you need more than 3,000 items, you can pipe (`|`

) or use any form of delimiter to delimit the values, concatenate them, and store them as a delimited string. There's no limitation on the number of strings stored in an array. Storing complex values as strings bypasses the complex collection limitation.

To illustrate, assume you have a `"searchScope`

" array with more than 3,000 elements:

```
"searchScope": [
{
"countryCode": "FRA",
"productCode": 1234,
"categoryCode": "C100"
},
{
"countryCode": "USA",
"productCode": 1235,
"categoryCode": "C200"
}
. . .
]
```


The workaround for storing the values as a delimited string might look like this:

```
"searchScope": [
"|FRA|1234|C100|",
"|FRA|*|*|",
"|*|1234|*|",
"|*|*|C100|",
"|FRA|*|C100|",
"|*|1234|C100|"
]
```


Storing all of the search variants in the delimited string is helpful in search scenarios where you want to search for items that have just "FRA" or "1234" or another combination within the array.

Here's a filter formatting snippet in C# that converts inputs into searchable strings:

```
foreach (var filterItem in filterCombinations)
{
var formattedCondition = $"searchScope/any(s: s eq '{filterItem}')";
combFilter.Append(combFilter.Length > 0 ? " or (" + formattedCondition + ")" : "(" + formattedCondition + ")");
}
```


The following list provides inputs and search strings (outputs) side by side:

For "FRA" county code and the "1234" product code, the formatted output is

`|FRA|1234|*|`

.For "1234" product code, the formatted output is

`|*|1234|*|`

.For "C100" category code, the formatted output is

`|*|*|C100|`

.

Only provide the wildcard (`*`

) if you're implementing the string array workaround. Otherwise, if you're using a complex type, your filter might look like this example:

```
var countryFilter = $"searchScope/any(ss: search.in(countryCode ,'FRA'))";
var catgFilter = $"searchScope/any(ss: search.in(categoryCode ,'C100'))";
var combinedCountryCategoryFilter = "(" + countryFilter + " and " + catgFilter + ")";
```


If you implement the workaround, be sure to test extensively.

## Next steps

Use an import wizard with sample data to guide you through creating, loading, and querying an index.
