---
merged_at: 2026-01-25T03:18:14.046847
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-filters.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-filters -->

# Filters in keyword search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A *filter* provides value-based criteria for including or excluding content before query execution for keyword search, or before or after query execution for vector search. Filters are applied to nonvector fields, but can be used in vector search if documents include nonvector fields. For example, for indexes organized around chunked content, you might have parent-level fields or metadata fields that can be filtered.

This article explains filtering for keyword search. For more information about vectors, see [Add a filter in a vector query](vector-search-filters).

A filter is specified using [OData filter expression syntax](search-query-odata-filter). In contrast with keyword and vector search, a filter succeeds only if the match is exact.

## When to use a filter

Filters are foundational to several search experiences, including "find near me" geospatial search, faceted navigation, and security filters that show only those documents a user is allowed to see. If you implement any one of these experiences, a filter is required. It's the filter attached to the search query that provides the geolocation coordinates, the facet category selected by the user, or the security ID of the requester.

Common scenarios include:

Slice search results based on content in the index. Given a schema with hotel location, categories, and amenities, you might create a filter to explicitly match on criteria (in Seattle, on the water, with a view).

Implement a search experience comes with a filter dependency:

[Faceted navigation](search-faceted-navigation)uses a filter to pass back the facet category selected by the user.[Geospatial search](search-query-odata-geo-spatial-functions)uses a filter to pass coordinates of the current location in "find near me" apps and functions that match within an area or by distance.[Security filters](search-security-trimming-for-azure-search)pass security identifiers as filter criteria, where a match in the index serves as a proxy for access rights to the document.

Do a "numbers search". Numeric fields are retrievable and can appear in search results, but they aren't searchable (subject to full text search) individually. If you need selection criteria based on numeric data, use a filter.


## How filters are executed

At query time, a filter parser accepts criteria as input, converts the expression into atomic Boolean expressions represented as a tree, and then evaluates the filter tree over filterable fields in an index.

Filtering occurs in tandem with search, qualifying which documents to include in downstream processing for document retrieval and relevance scoring. When paired with a search string, the filter effectively reduces the recall set of the subsequent search operation. When used alone (for example, when the query string is empty where `search=*`

), the filter criteria is the sole input.

## How filters are defined

Filters apply to text and numeric (nonvector) content on fields that are attributed as `filterable`

.

Filters are OData expressions, articulated in the [filter syntax](search-query-odata-filter) supported by Azure AI Search.

You can specify one filter for each **search** operation, but the filter itself can include multiple fields, multiple criteria, and if you use an ** ismatch** function, multiple full-text search expressions. In a multi-part filter expression, you can specify predicates in any order (subject to the rules of operator precedence). There's no appreciable gain in performance if you try to rearrange predicates in a particular sequence.

One of the limits on a filter expression is the maximum size limit of the request. The entire request, inclusive of the filter, can be a maximum of 16 MB for POST, or 8 KB for GET. There's also a limit on the number of clauses in your filter expression. A good rule of thumb is that if you have hundreds of clauses, you are at risk of running into the limit. We recommend designing your application in such a way that it doesn't generate filters of unbounded size.

The following examples represent prototypical filter definitions in several APIs.

```
POST https://[service name].search.windows.net/indexes/hotels/docs/search?api-version=2025-09-01
{
"search": "*",
"filter": "Rooms/any(room: room/BaseRate lt 150.0)",
"select": "HotelId, HotelName, Rooms/Description, Rooms/BaseRate"
}
```


```
options = new SearchOptions()
{
Filter = "Rating gt 4",
OrderBy = { "Rating desc" }
};
```


## Filter patterns

The following examples illustrate several usage patterns for filter scenarios. For more ideas, see [OData expression syntax > Examples](search-query-odata-filter#examples).

Standalone

**$filter**, without a query string, useful when the filter expression is able to fully qualify documents of interest. Without a query string, there's no lexical or linguistic analysis, no scoring, and no ranking. Notice the search string is just an asterisk, which means "match all documents".`{ "search": "*", "filter": "Rooms/any(room: room/BaseRate ge 60 and room/BaseRate lt 300) and Address/City eq 'Honolulu" }`

Combination of query string and

**$filter**, where the filter creates the subset, and the query string provides the term inputs for full text search over the filtered subset. The addition of terms (walking distance theaters) introduces search scores in the results, where documents that best match the terms are ranked higher. Using a filter with a query string is the most common usage pattern.`{ "search": "walking distance theaters", "filter": "Rooms/any(room: room/BaseRate ge 60 and room/BaseRate lt 300) and Address/City eq 'Seattle'" }`

Compound queries, separated by "or", each with its own filter criteria (for example, 'beagles' in 'dog' or 'siamese' in 'cat'). Expressions combined with

`or`

are evaluated individually, with the union of documents matching each expression sent back in the response. This usage pattern is achieved through the`search.ismatchscoring`

function. You can also use the nonscoring version,`search.ismatch`

.`# Match on hostels rated higher than 4 OR 5-star motels. $filter=search.ismatchscoring('hostel') and Rating ge 4 or search.ismatchscoring('motel') and Rating eq 5 # Match on 'luxury' or 'high-end' in the description field OR on category exactly equal to 'Luxury'. $filter=search.ismatchscoring('luxury | high-end', 'Description') or Category eq 'Luxury'&$count=true`

It's also possible to combine full-text search via

`search.ismatchscoring`

with filters using`and`

instead of`or`

, but this is functionally equivalent to using the`search`

and`$filter`

parameters in a search request. For example, the following two queries produce the same result:`$filter=search.ismatchscoring('pool') and Rating ge 4 search=pool&$filter=Rating ge 4`


## Field requirements for filtering

In the REST API, filterable is *on* by default for simple fields. Filterable fields increase index size; be sure to set `"filterable": false`

for fields that you don't plan to actually use in a filter. For more information about settings for field definitions, see [Create Index](/en-us/rest/api/searchservice/indexes/create).

In the Azure SDKs, filterable is *off* by default. You can make a field filterable by setting the [IsFilterable property](/en-us/dotnet/api/azure.search.documents.indexes.models.searchfield.isfilterable) of the corresponding [SearchField](/en-us/dotnet/api/azure.search.documents.indexes.models.searchfield) object to `true`

. In the next example, the attribute is set on the `Rating`

property of a model class that maps to the index definition.

```
[SearchField(IsFilterable = true, IsSortable = true, IsFacetable = true)]
public double? Rating { get; set; }
```


### Making an existing field filterable

You can't modify existing fields to make them filterable. Instead, you need to add a new field, or rebuild the index. For more information about rebuilding an index or repopulating fields, see [How to rebuild an Azure AI Search index](search-howto-reindex).

## Text filter fundamentals

Text filters match string fields against literal strings that you provide in the filter: `$filter=Category eq 'Resort and Spa'`


Unlike full-text search, there's no lexical analysis or word-breaking for text filters, so comparisons are for exact matches only. For example, assume a field *f* contains "sunny day", `$filter=f eq 'sunny'`

doesn't match, but `$filter=f eq 'sunny day'`

will.

Text strings are case-sensitive, which means text filters are case sensitive by default. For example, `$filter=f eq 'Sunny day'`

won't find "sunny day". However, you can use a [normalizer](search-normalizers) to make it so filtering isn't case sensitive.

### Approaches for filtering on text

| Approach | Description | When to use |
|---|---|---|
`search.in` |

[security filters](search-security-trimming-for-azure-search)and for any filters where many raw text values need to be matched with a string field. The**search.in**function is designed for speed and is much faster than explicitly comparing the field against each string using`eq`

and `or`

.`search.ismatch`

**search.ismatch**(or its scoring equivalent,**search.ismatchscoring**) when you want multiple search-filter combinations in one request. You can also use it for a*contains*filter to filter on a partial string within a larger string.`$filter=field operator string`

## Numeric filter fundamentals

Numeric fields aren't `searchable`

in the context of full text search. Only strings are subject to full text search. For example, if you enter 99.99 as a search term, you won't get back items priced at $99.99. Instead, you would see items that have the number 99 in string fields of the document. Thus, if you have numeric data, the assumption is that you'll use them for filters, including ranges, facets, groups, and so forth.

Documents that contain numeric fields (price, size, SKU, ID) provide those values in search results if the field is marked `retrievable`

. The point here's that full text search itself isn't applicable to numeric field types.

## Next steps

First, try **Search explorer** in the Azure portal to submit queries with **$filter** parameters. The [real-estate-sample index](search-get-started-portal) provides interesting results for the following filtered queries when you paste them into the search bar:

```
# Geo-filter returning documents within 5 kilometers of Redmond, Washington state
# Use $count=true to get a number of hits returned by the query
# Use $select to trim results, showing values for named fields only
# Use search=* for an empty query string. The filter is the sole input
search=*&$count=true&$select=description,city,postCode&$filter=geo.distance(location,geography'POINT(-122.121513 47.673988)') le 5
# Numeric filters use comparison like greater than (gt), less than (lt), not equal (ne)
# Include "and" to filter on multiple fields (baths and bed)
# Full text search is on John Leclerc, matching on John or Leclerc
search=John Leclerc&$count=true&$select=source,city,postCode,baths,beds&$filter=baths gt 3 and beds gt 4
# Text filters can also use comparison operators
# Wrap text in single or double quotes and use the correct case
# Full text search is on John Leclerc, matching on John or Leclerc
search=John Leclerc&$count=true&$select=source,city,postCode,baths,beds&$filter=city gt 'Seattle'
```


To work with more examples, see [OData Filter Expression Syntax > Examples](search-query-odata-filter#examples).


---

<!-- DOCUMENTO FUSIONADO: search-query-create.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-create -->

# Create a full text query in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you're building a query for [full text search](search-lucene-query-architecture), this article provides steps for setting up the request. It also introduces a query structure, and explains how field attributes and linguistic analyzers can affect query outcomes.

## Prerequisites

An Azure AI Search service (any tier).

[Create a service](search-create-service-portal)or[find an existing one](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).A

[search index](search-how-to-create-search-index)with string fields attributed as*searchable*. You can also use an[index alias](search-how-to-alias)as the endpoint of your query request.Permissions to query the index:

**Key-based authentication**: A[query API key](search-security-api-keys)for your search service.**Role-based authentication**:[Search Index Data Reader](search-security-rbac)role.

For SDK development, install the Azure Search client library:

- Python:
[azure-search-documents](https://pypi.org/project/azure-search-documents/) - .NET:
[Azure.Search.Documents](https://www.nuget.org/packages/Azure.Search.Documents/) - JavaScript:
[@azure/search-documents](https://www.npmjs.com/package/@azure/search-documents) - Java:
[azure-search-documents](https://central.sonatype.com/artifact/com.azure/azure-search-documents)

- Python:

Tip

For a quick code example, skip to [Example of a full text query request](#example-of-a-full-text-query-request).

## Example of a full text query request

In Azure AI Search, a query is a read-only request against the docs collection of a single search index, with parameters that both inform query execution and shape the response coming back.

A full text query is specified in a `search`

parameter and consists of terms, quote-enclosed phrases, and operators. Other parameters add more definition to the request.

The following [Search POST REST API](/en-us/rest/api/searchservice/documents/search-post) call illustrates a query request using `search`

and other parameters.

```
POST https://[service name].search.windows.net/indexes/hotels-sample-index/docs/search?api-version=2025-09-01
{
"search": "NY +view",
"queryType": "simple",
"searchMode": "all",
"searchFields": "HotelName, Description, Address/City, Address/StateProvince, Tags",
"select": "HotelName, Description, Address/City, Address/StateProvince, Tags",
"top": 10,
"count": true
}
```


**Reference:** [Search POST](/en-us/rest/api/searchservice/documents/search-post)

### Key points

provides the match criteria, usually whole terms or phrases, with or without operators. Any field that is attributed as`search`

*searchable*in the index schema is within scope for a search operation.sets the parser:`queryType`

*simple*,*full*. The[default simple query parser](search-query-simple-examples)is optimal for full text search. The[full Lucene query parser](search-query-lucene-examples)is for advanced query constructs like regular expressions, proximity search, fuzzy and wildcard search. This parameter can also be set to*semantic*for[semantic ranking](semantic-search-overview)for advanced semantic modeling on the query response.specifies whether matches are based on`searchMode`

*all*criteria (favors precision) or*any*criteria (favors recall) in the expression. The default is*any*. If you anticipate heavy use of Boolean operators, which is more likely in indexes that contain large text blocks (a content field or long descriptions), be sure to test queries with the`searchMode=Any|All`

parameter to evaluate the impact of that setting on Boolean search.constrains query execution to specific searchable fields. During development, it's helpful to use the same field list for select and search. Otherwise a match might be based on field values that you can't see in the results, creating uncertainty as to why the document was returned.`searchFields`


Parameters used to shape the response:

specifies which fields to return in the response. Only fields marked as`select`

*retrievable*in the index can be used in a select statement.returns the specified number of best-matching documents. In this example, only 10 hits are returned. You can use top and skip (not shown) to page the results.`top`

tells you how many documents in the entire index match overall, which can be more than what are returned. Valid values are "true" or "false". Defaults to "false". Count is accurate if the index is stable, but will under or over-report any documents that are actively added, updated, or deleted. If you’d like to get only the count without any documents, you can use $top=0.`count`

is used if you want to sort results by a value, such as a rating or location. Otherwise, the default is to use the relevance score to rank results. A field must be attributed as`orderby`

*sortable*to be a candidate for this parameter.

## Choose a client

For early development and proof-of-concept testing, start with the Azure portal or a REST client or a Jupyter notebook. These approaches are interactive, useful for targeted testing, and help you assess the effects of different properties without having to write any code.

To call search from within an app, use the `Azure.Document.Search`

client libraries in the Azure SDKs for .NET, Java, JavaScript, and Python.

In the Azure portal, when you open an index, you can work with Search Explorer alongside the index JSON definition in side-by-side tabs for easy access to field attributes. Check the **Fields** table to see which ones are searchable, sortable, filterable, and facetable while testing queries.

Sign in to the

[Azure portal](https://portal.azure.com)and[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).In your service, select

**Indexes**and choose an index.An index opens to the

tab so that you can query right away. Switch to**Search explorer****JSON view**to specify query syntax.Here's a full text search query expression that works for the Hotels sample index:

`{ "search": "pool spa +airport", "queryType": "simple", "searchMode": "any", "searchFields": "Description, Tags", "select": "HotelName, Description, Tags", "top": 10, "count": true }`

**Reference:**[Search POST](/en-us/rest/api/searchservice/documents/search-post)The following screenshot illustrates the query and response:


## Choose a query type: simple | full

If your query is full text search, a query parser is used to process any text that's passed as search terms and phrases. Azure AI Search offers two query parsers.

The simple parser understands the

[simple query syntax](query-simple-syntax). This parser was selected as the default for its speed and effectiveness in free form text queries. The syntax supports common search operators (AND, OR, NOT) for term and phrase searches, and prefix (`*`

) search (as in`sea*`

for Seattle and Seaside). A general recommendation is to try the simple parser first, and then move on to full parser if application requirements call for more powerful queries.The

[full Lucene query syntax](query-lucene-syntax#bkmk_syntax), enabled when you add`queryType=full`

to the request, is based on the[Apache Lucene Parser](https://lucene.apache.org/core/6_6_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html).

Full syntax and simple syntax overlap to the extent that both support the same prefix and Boolean operations, but the full syntax provides more operators. In full, there are more operators for Boolean expressions, and more operators for advanced queries such as fuzzy search, wildcard search, proximity search, and regular expressions.

## Choose query methods

Search is fundamentally a user-driven exercise, where terms or phrases are collected from a search box, or from click events on a page. The following table summarizes the mechanisms by which you can collect user input, along with the expected search experience.

| Input | Experience |
|---|---|
|

**Search**to send the request. Search can be used with filters on the same request, but not with autocomplete or suggestions.[Autocomplete method](/en-us/rest/api/searchservice/documents/autocomplete-post)**Search**to send that query to the service.[Suggestions method](/en-us/rest/api/searchservice/documents/suggest-post)[Faceted navigation](/en-us/rest/api/searchservice/documents/search-post#searchrequest)`search=*`

to populate a faceted navigation tree composed of every possible category. A faceted navigation structure is created from a query response, but it's also a mechanism for expressing the next query. n REST API reference, `facets`

is documented as a query parameter of a Search Documents operation, but it can be used without the `search`

parameter.[Filter method](/en-us/rest/api/searchservice/documents/search-post#searchrequest)`$filter`

is documented as a query parameter of a Search Documents operation, but it can be used without the `search`

parameter.## Effect of field attributes on queries

If you're familiar with [query types and composition](search-query-overview), you might remember that the parameters on a query request depend on field attributes in an index. For example, only fields marked as *searchable* and *retrievable* can be used in queries and search results. When setting the `search`

, `filter`

, and `orderby`

parameters in your request, you should check attributes to avoid unexpected results.

In the following screenshot of the [hotels sample index](search-get-started-portal), only the last two fields **LastRenovationDate** and **Rating** are *sortable*, a requirement for use in an `"$orderby"`

only clause.


For field attribute definitions, see [Create Index (REST API)](/en-us/rest/api/searchservice/indexes/create).

## Effect of tokens on queries

During indexing, the search engine uses a text analyzer on strings to maximize the potential for finding a match at query time. At a minimum, strings are lower-cased, but depending on the analyzer, might also undergo lemmatization and stop word removal. Larger strings or compound words are typically broken up by whitespace, hyphens, or dashes, and indexed as separate tokens.

The key point is that what you think your index contains, and what's actually in it, can be different. If queries don't return expected results, you can inspect the tokens created by the analyzer through the [Analyze Text (REST API)](/en-us/rest/api/searchservice/indexes/analyze). For more information about tokenization and the effect on queries, see [Partial term search and patterns with special characters](search-query-partial-matching).

## Troubleshoot queries

The following table lists common query issues and how to resolve them.

| Issue | Cause | Resolution |
|---|---|---|
| Empty results | No documents match query terms. | Verify field is marked searchable in schema. Use
|
| Unexpected results | Query matches unintended fields. | Use `searchFields` to limit which fields are searched. |
| Too many results | Query is too broad. | Add filters, use `searchMode=all` , or add required terms with `+` operator. |
| Results not ranked as expected | Relevance scoring doesn't match expectations. | Consider
|

`*`

) suffix or check analyzer behavior with Analyze Text API.*filterable*.`filterable: true`

on the field.## Related content

Now that you have a better understanding of how query requests work, try the following quickstarts for hands-on experience.
