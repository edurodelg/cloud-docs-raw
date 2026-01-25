---
merged_at: 2026-01-25T03:18:14.057049
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: semantic-how-to-query-request.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/semantic-how-to-query-request -->

# Add semantic ranking to queries in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can apply semantic ranking to text queries, hybrid queries, and vector queries if your search documents contain string fields and the [vector query has a text representation](vector-search-how-to-query#query-with-integrated-vectorization) in the search document.

This article explains how to invoke the semantic ranker on queries. It assumes you're using the most recent stable or preview APIs. For help with older versions, see [Migrate semantic ranking code](semantic-code-migration).

## Prerequisites

[Azure AI Search](search-create-service-portal)in any[region that provides semantic ranking](search-region-support), with[semantic ranker enabled](semantic-how-to-enable-disable).An existing search index with a

[semantic configuration](semantic-how-to-configure)and rich text content.Familiarity with

[semantic ranking](semantic-search-overview).

Note

Captions and answers are extracted verbatim from text in the search document. The semantic subsystem uses machine reading comprehension to recognize content having the characteristics of a caption or answer, but doesn't compose new sentences or phrases except in the case of [query rewrite](semantic-how-to-query-rewrite). For this reason, content that includes explanations or definitions work best for semantic ranking. If you want chat-style interaction with generated responses, see [Agentic retrieval](agentic-retrieval-overview) or [Retrieval Augmented Generation (RAG)](retrieval-augmented-generation-overview).

## Choose a client

You can use any of the following tools and SDKs to build a query that uses semantic ranking:

[Azure portal](https://portal.azure.com), using the index designer to add a semantic configuration.[Visual Studio Code](https://code.visualstudio.com/download)with a[REST client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)[Azure SDK for .NET](https://www.nuget.org/packages/Azure.Search.Documents)[Azure SDK for Python](https://pypi.org/project/azure-search-documents)[Azure SDK for Java](https://central.sonatype.com/artifact/com.azure/azure-search-documents)[Azure SDK for JavaScript](https://www.npmjs.com/package/@azure/search-documents)

## Avoid features that bypass relevance scoring

A few query capabilities bypass relevance scoring, which makes them incompatible with semantic ranking. If your query logic includes the following features, you can't semantically rank your results:

A query with

`search=*`

or an empty search string, such as pure filter-only query, won't work because there's nothing to measure semantic relevance against and so the search scores are zero. The query must provide terms or phrases that can be evaluated during processing, and that produces search documents that are scored for relevance. Scored results are inputs to the semantic ranker.Sorting (orderBy clauses) on specific fields overrides search scores and a semantic score. Given that the semantic score is supposed to provide the ranking, adding an orderby clause results in an HTTP 400 error if you apply semantic ranking over ordered results.


## Set up the query

By default, queries don't use semantic ranking. To use semantic ranking, two different parameters can be used. Each parameter supports a different set of query formats.

All semantic queries, whether specified through `search`

plus `queryType`

, or through `semanticQuery`

, must be plain text and they can't be empty. As you can see from the table below, the `queryType-semantic`

parameter supports a subset of query formats.

| Parameter |
|
|---|

[Simple text search syntax](query-simple-syntax)

[Full text search syntax](query-lucene-syntax)

[Vector search](vector-search-how-to-query)

[Hybrid Search](hybrid-search-how-to-query)

[Semantic answers](semantic-answers)and captions

`queryType-semantic`

1`semanticQuery="<your plain text query>"`

21 `queryType=semantic`

can't support explicit `simple`

or `full`

values because the `queryType`

parameter is being used for `semantic`

. The effective query behaviors are the defaults of the simple parser.

2 The `semanticQuery`

parameter can be used for all query types. However, it isn't supported in the Azure portal [Search Explorer](search-explorer).

Regardless of the parameter chosen, the index should contain text fields with rich semantic content and a [semantic configuration](semantic-how-to-configure).

[Search explorer](search-explorer) includes options for semantic ranking. Recall that you can't set the `semanticQuery`

parameter in the Azure portal.

Sign in to the

[Azure portal](https://portal.azure.com).Open a search index and select

**Search explorer**.Select

**Query options**. If you already defined a semantic configuration, it's selected by default. If you don't have one,[create a semantic configuration](semantic-how-to-configure)for your index.Enter a query, such as "historic hotel with good food", and select

**Search**.Alternatively, select

**JSON view**and paste definitions into the query editor. The Azure portal doesn't support using`semanticQuery`

, so setting`queryType`

to`"semantic"`

is required:JSON example for setting query type to semantic that you can paste into the view:

`{ "search": "funky or interesting hotel with good food on site", "count": true, "queryType": "semantic", "semanticConfiguration": "my-semantic-config", "captions": "extractive|highlight-true", "answers": "extractive|count-3", "highlightPreTag": "<strong>", "highlightPostTag": "</strong>", "select": "HotelId,HotelName,Description,Category" }`


## Evaluate the response

Only the top 50 matches from the initial results can be semantically ranked. As with all queries, a response is composed of all fields marked as retrievable, or just those fields listed in the `select`

parameter. A response includes the original relevance score, and might also include a count, or batched results, depending on how you formulated the request.

In semantic ranking, the response has more elements: a new [semantically ranked relevance score](semantic-search-overview#how-results-are-scored), an optional caption in plain text and with highlights, and an optional [answer](semantic-answers). If your results don't include these extra elements, then your query might be misconfigured. As a first step towards troubleshooting the problem, check the semantic configuration to ensure it's specified in both the index definition and query.

In a client app, you can structure the search page to include a caption as the description of the match, rather than the entire contents of a specific field. This approach is useful when individual fields are too dense for the search results page.

The response for the above example query (*"interesting hotel with restaurant on site and cozy lobby or shared area"*) returns three answers (`"answers": "extractive|count-e"`

). Captions are returned because the "captions" property is set, with plain text and highlighted versions. If an answer can't be determined, it's omitted from the response. For brevity, this example shows just the three answers and the three highest scoring results from the query.

```
{
"@odata.count": 29,
"@search.answers": [
{
"key": "24",
"text": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance.",
"highlights": "Chic hotel near the city. <strong>High-rise hotel in downtown, </strong>within<strong> walking distance to </strong>theaters, art<strong> galleries, restaurants and shops.</strong> Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance.",
"score": 0.9340000152587891
},
{
"key": "40",
"text": "Only 8 miles from Downtown. On-site bar/restaurant, Free hot breakfast buffet, Free wireless internet, All non-smoking hotel. Only 15 miles from airport.",
"highlights": "Only 8 miles from Downtown. <strong>On-site bar/restaurant, Free hot breakfast buffet, Free wireless internet, </strong>All non-smoking<strong> hotel.</strong> Only 15 miles from airport.",
"score": 0.9210000038146973
},
{
"key": "38",
"text": "Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply.",
"highlights": "Nature is Home on the beach. Explore the shore by day, and then come home to our<strong> shared living space </strong>to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply.",
"score": 0.9200000166893005
}
],
"value": [
{
"@search.score": 3.2328331,
"@search.rerankerScore": 2.575303316116333,
"@search.captions": [
{
"text": "The best of old town hospitality combined with views of the river and cool breezes off the prairie. Our penthouse suites offer views for miles and the rooftop plaza is open to all guests from sunset to 10 p.m. Enjoy a complimentary continental breakfast in the lobby, and free Wi-Fi throughout the hotel.",
"highlights": "The best of old town hospitality combined with views of the river and cool breezes off the prairie. Our<strong> penthouse </strong>suites offer views for miles and the rooftop<strong> plaza </strong>is open to all guests from sunset to 10 p.m. Enjoy a<strong> complimentary continental breakfast in the lobby, </strong>and free Wi-Fi<strong> throughout </strong>the hotel."
}
],
"HotelId": "50",
"HotelName": "Head Wind Resort",
"Description": "The best of old town hospitality combined with views of the river and cool breezes off the prairie. Our penthouse suites offer views for miles and the rooftop plaza is open to all guests from sunset to 10 p.m. Enjoy a complimentary continental breakfast in the lobby, and free Wi-Fi throughout the hotel.",
"Category": "Suite"
},
{
"@search.score": 0.632956,
"@search.rerankerScore": 2.5425150394439697,
"@search.captions": [
{
"text": "Every stay starts with a warm cookie. Amenities like the Counting Sheep sleep experience, our Wake-up glorious breakfast buffet and spacious workout facilities await.",
"highlights": "Every stay starts with a warm cookie. Amenities like the<strong> Counting Sheep sleep experience, </strong>our<strong> Wake-up glorious breakfast buffet and spacious workout facilities </strong>await."
}
],
"HotelId": "34",
"HotelName": "Lakefront Captain Inn",
"Description": "Every stay starts with a warm cookie. Amenities like the Counting Sheep sleep experience, our Wake-up glorious breakfast buffet and spacious workout facilities await.",
"Category": "Budget"
},
{
"@search.score": 3.7076726,
"@search.rerankerScore": 2.4554927349090576,
"@search.captions": [
{
"text": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance.",
"highlights": "Chic hotel near the city. <strong>High-rise hotel in downtown, </strong>within<strong> walking distance to </strong>theaters, art<strong> galleries, restaurants and shops.</strong> Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance."
}
],
"HotelId": "24",
"HotelName": "Uptown Chic Hotel",
"Description": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance.",
"Category": "Suite"
},
. . .
]
}
```


## Expected workloads

For semantic ranking, you should expect a search service to support up to 10 concurrent queries per replica.

The service throttles semantic ranking requests if volumes are too high. An error message that includes these phrases indicate the service is at capacity for semantic ranking:

```
Error in search query: Operation returned an invalid status 'Partial Content'`
@search.semanticPartialResponseReason`
CapacityOverloaded
```


If you anticipate consistent throughput requirements near, at, or higher than this level, please file a support ticket so that we can provision for your workload.

## Next steps

Semantic ranking can be used in hybrid queries that combine keyword search and vector search into a single request and a unified response.


---

<!-- DOCUMENTO FUSIONADO: query-odata-filter-orderby-syntax.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/query-odata-filter-orderby-syntax -->

# OData language overview for $filter, $orderby, and $select in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

# OData language overview for

This article provides an overview of the OData expression language used in `$filter`

, `$order-by`

, and `$select`

expressions for keyword search in Azure AI Search over numeric and string (nonvector) fields.

The language is presented "bottom-up" starting with the most basic elements. The OData expressions that you can construct in a query request range from simple to highly complex, but they all share common elements. Shared elements include:

**Field paths**, which refer to specific fields of your index.**Constants**, which are literal values of a certain data type.

Once you understand these common concepts, you can continue with the top-level syntax for each expression:

expressions are evaluated during query parsing, constraining search to specific fields or adding match criteria used during index scans.**$filter**expressions are applied as a post-processing step over a result set to sort the documents that are returned.**$orderby**expressions determine which document fields are included in the result set.**$select**

The syntax of these expressions is distinct from the [simple](query-simple-syntax) or [full](query-lucene-syntax) query syntax used in the **search** parameter, although there's some overlap in the syntax for referencing fields.

For examples in other languages such as Python or C#, see the examples in the [azure-search-vector-samples](https://github.com/Azure/azure-search-vector-samples) repository.

Note

Terminology in Azure AI Search differs from the [OData standard](https://www.odata.org/documentation/) in a few ways. What we call a **field** in Azure AI Search is called a **property** in OData, and similarly for **field path** versus **property path**. An **index** containing **documents** in Azure AI Search is referred to more generally in OData as an **entity set** containing **entities**. The Azure AI Search terminology is used throughout this reference.

## Field paths

The following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) defines the grammar of field paths.

```
field_path ::= identifier('/'identifier)*
identifier ::= [a-zA-Z_][a-zA-Z_0-9]*
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

A field path is composed of one or more **identifiers** separated by slashes. Each identifier is a sequence of characters that must start with an ASCII letter or underscore, and contain only ASCII letters, digits, or underscores. The letters can be upper- or lower-case.

An identifier can refer either to the name of a field, or to a **range variable** in the context of a [collection expression](search-query-odata-collection-operators) (`any`

or `all`

) in a filter. A range variable is like a loop variable that represents the current element of the collection. For complex collections, that variable represents an object, which is why you can use field paths to refer to subfields of the variable. This is analogous to dot notation in many programming languages.

Examples of field paths are shown in the following table:

| Field path | Description |
|---|---|
`HotelName` |
Refers to a top-level field of the index |
`Address/City` |
Refers to the `City` subfield of a complex field in the index; `Address` is of type `Edm.ComplexType` in this example |
`Rooms/Type` |
Refers to the `Type` subfield of a complex collection field in the index; `Rooms` is of type `Collection(Edm.ComplexType)` in this example |
`Stores/Address/Country` |
Refers to the `Country` subfield of the `Address` subfield of a complex collection field in the index; `Stores` is of type `Collection(Edm.ComplexType)` and `Address` is of type `Edm.ComplexType` in this example |
`room/Type` |
Refers to the `Type` subfield of the `room` range variable, for example in the filter expression `Rooms/any(room: room/Type eq 'deluxe')` |
`store/Address/Country` |
Refers to the `Country` subfield of the `Address` subfield of the `store` range variable, for example in the filter expression `Stores/any(store: store/Address/Country eq 'Canada')` |

The meaning of a field path differs depending on the context. In filters, a field path refers to the value of a *single instance* of a field in the current document. In other contexts, such as **$orderby**, **$select**, or in [fielded search in the full Lucene syntax](query-lucene-syntax#bkmk_fields), a field path refers to the field itself. This difference has some consequences for how you use field paths in filters.

Consider the field path `Address/City`

. In a filter, this refers to a single city for the current document, like "San Francisco". In contrast, `Rooms/Type`

refers to the `Type`

subfield for many rooms (like "standard" for the first room, "deluxe" for the second room, and so on). Since `Rooms/Type`

doesn't refer to a *single instance* of the subfield `Type`

, it can't be used directly in a filter. Instead, to filter on room type, you would use a [lambda expression](search-query-odata-collection-operators) with a range variable, like this:

```
Rooms/any(room: room/Type eq 'deluxe')
```


In this example, the range variable `room`

appears in the `room/Type`

field path. That way, `room/Type`

refers to the type of the current room in the current document. This is a single instance of the `Type`

subfield, so it can be used directly in the filter.

### Using field paths

Field paths are used in many parameters of the [Azure AI Search REST APIs](/en-us/rest/api/searchservice/). The following table lists all the places where they can be used, plus any restrictions on their usage:

| API | Parameter name | Restrictions |
|---|---|---|
|

`suggesters/sourceFields`

[Create](/en-us/rest/api/searchservice/indexes/create)or[Update](/en-us/rest/api/searchservice/indexes/create-or-update)Index`scoringProfiles/text/weights`

**searchable**fields[Create](/en-us/rest/api/searchservice/indexes/create)or[Update](/en-us/rest/api/searchservice/indexes/create-or-update)Index`scoringProfiles/functions/fieldName`

**filterable**fields[Search](/en-us/rest/api/searchservice/documents/search-post)`search`

when `queryType`

is `full`

**searchable**fields[Search](/en-us/rest/api/searchservice/documents/search-post)`facet`

**facetable**fields[Search](/en-us/rest/api/searchservice/documents/search-post)`highlight`

**searchable**fields[Search](/en-us/rest/api/searchservice/documents/search-post)`searchFields`

**searchable**fields[Suggest](/en-us/rest/api/searchservice/documents/suggest-post)and[Autocomplete](/en-us/rest/api/searchservice/documents/autocomplete-post)`searchFields`

[suggester](index-add-suggesters)[Search](/en-us/rest/api/searchservice/documents/search-post),[Suggest](/en-us/rest/api/searchservice/documents/suggest-post), and[Autocomplete](/en-us/rest/api/searchservice/documents/autocomplete-post)`$filter`

**filterable**fields[Search](/en-us/rest/api/searchservice/documents/search-post)and[Suggest](/en-us/rest/api/searchservice/documents/suggest-post)`$orderby`

**sortable**fields[Search](/en-us/rest/api/searchservice/documents/search-post),[Suggest](/en-us/rest/api/searchservice/documents/suggest-post), and[Lookup](/en-us/rest/api/searchservice/documents/get)`$select`

**retrievable**fields## Constants

Constants in OData are literal values of a given [Entity Data Model (EDM)](/en-us/dotnet/framework/data/adonet/entity-data-model) type. See [Supported data types](/en-us/rest/api/searchservice/supported-data-types) for a list of supported types in Azure AI Search. Constants of collection types aren't supported.

The following table shows examples of constants for each of the nonvector data types that support OData expressions:

| Data type | Example constants |
|---|---|
`Edm.Boolean` |
`true` , `false` |
`Edm.DateTimeOffset` |
`2019-05-06T12:30:05.451Z` |
`Edm.Double` |
`3.14159` , `-1.2e7` , `NaN` , `INF` , `-INF` |
`Edm.GeographyPoint` |
`geography'POINT(-122.131577 47.678581)'` |
`Edm.GeographyPolygon` |
`geography'POLYGON((-122.031577 47.578581, -122.031577 47.678581, -122.131577 47.678581, -122.031577 47.578581))'` |
`Edm.Int32` |
`123` , `-456` |
`Edm.Int64` |
`283032927235` |
`Edm.String` |
`'hello'` |

### Escaping special characters in string constants

String constants in OData are delimited by single quotes. If you need to construct a query with a string constant that might itself contain single quotes, you can escape the embedded quotes by doubling them.

For example, a phrase with an unformatted apostrophe like "Alice's car" would be represented in OData as the string constant `'Alice''s car'`

.

Important

When constructing filters programmatically, it's important to remember to escape string constants that come from user input. This is to mitigate the possibility of [injection attacks](https://wikipedia.org/wiki/SQL_injection), especially when using filters to implement [security trimming](search-security-trimming-for-azure-search).

### Constants syntax

The following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) defines the grammar for most of the constants shown in the above table. The grammar for geo-spatial types can be found in [OData geo-spatial functions in Azure AI Search](search-query-odata-geo-spatial-functions).

```
constant ::=
string_literal
| date_time_offset_literal
| integer_literal
| float_literal
| boolean_literal
| 'null'
string_literal ::= "'"([^'] | "''")*"'"
date_time_offset_literal ::= date_part'T'time_part time_zone
date_part ::= year'-'month'-'day
time_part ::= hour':'minute(':'second('.'fractional_seconds)?)?
zero_to_fifty_nine ::= [0-5]digit
digit ::= [0-9]
year ::= digit digit digit digit
month ::= '0'[1-9] | '1'[0-2]
day ::= '0'[1-9] | [1-2]digit | '3'[0-1]
hour ::= [0-1]digit | '2'[0-3]
minute ::= zero_to_fifty_nine
second ::= zero_to_fifty_nine
fractional_seconds ::= integer_literal
time_zone ::= 'Z' | sign hour':'minute
sign ::= '+' | '-'
/* In practice integer literals are limited in length to the precision of
the corresponding EDM data type. */
integer_literal ::= digit+
float_literal ::=
sign? whole_part fractional_part? exponent?
| 'NaN'
| '-INF'
| 'INF'
whole_part ::= integer_literal
fractional_part ::= '.'integer_literal
exponent ::= 'e' sign? integer_literal
boolean_literal ::= 'true' | 'false'
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

## Building expressions from field paths and constants

Field paths and constants are the most basic part of an OData expression, but they're already full expressions themselves. In fact, the **$select** parameter in Azure AI Search is nothing but a comma-separated list of field paths, and **$orderby** isn't much more complicated than **$select**. If you happen to have a field of type `Edm.Boolean`

in your index, you can even write a filter that is nothing but the path of that field. The constants `true`

and `false`

are likewise valid filters.

However, it's more common to have complex expressions that refer to more than one field and constant. These expressions are built in different ways depending on the parameter.

The following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) defines the grammar for the **$filter**, **$orderby**, and **$select** parameters. These are built up from simpler expressions that refer to field paths and constants:

```
filter_expression ::= boolean_expression
order_by_expression ::= order_by_clause(',' order_by_clause)*
select_expression ::= '*' | field_path(',' field_path)*
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

## Next steps

The **$orderby** and **$select** parameters are both comma-separated lists of simpler expressions. The **$filter** parameter is a Boolean expression that is composed of simpler subexpressions. These subexpressions are combined using logical operators such as [ and, or, and not](search-query-odata-logical-operators), comparison operators such as


[, and collection operators such as](search-query-odata-comparison-operators)

`eq`

, `lt`

, `gt`

, and so on[.](search-query-odata-collection-operators)

`any`

and `all`

The **$filter**, **$orderby**, and **$select** parameters are explored in more detail in the following articles:
