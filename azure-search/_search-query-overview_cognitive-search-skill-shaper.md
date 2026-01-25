---
merged_at: 2026-01-25T03:18:13.779059
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-query-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-overview -->

# Querying in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search supports query constructs for a broad range of scenarios, from free-form text search, to highly specified query patterns, to vector search. All queries execute over a search index that stores searchable content.

## Types of queries

| Query form | Searchable content | Description |
|---|---|---|
|

[Vector search](vector-search-overview)[Hybrid search](hybrid-search-overview)[Agentic retrieval (preview)](agentic-retrieval-overview)The remainder of this article brings focus to the last category: classic queries that work on plain text and human-readable content, extracted intact from original source, used for filters and other specialized query forms. If you're creating a traditional search application that isn't using AI, this section explains the query methods that you can implement in your client code.

## Autocomplete and suggested queries

[Autocomplete or suggested results](search-add-autocomplete-suggestions) are alternatives to ** search** that fire successive query requests based on partial string inputs (after each character) in a search-as-you-type experience. You can use

**and**

`autocomplete`

**parameter together or separately, as described in**

`suggestions`

[this walkthrough](tutorial-csharp-type-ahead-and-suggestions), but you can't use them with

**. Both completed terms and suggested queries are derived from index contents. The engine never returns a string or suggestion that is nonexistent in your index. For more information, see**

`search`

[Autocomplete (REST API)](/en-us/rest/api/searchservice/documents/autocomplete-post)and

[Suggestions (REST API)](/en-us/rest/api/searchservice/documents/suggest-post).

## Filter search

Filters are widely used in apps that are based on Azure AI Search. On application pages, filters are often visualized as facets in link navigation structures for user-directed filtering. Filters are also used internally to expose slices of indexed content. For example, you might initialize a search page using a filter on a product category, or a language if an index contains fields in both English and French.

You might also need filters to invoke a specialized query form, as described in the following table. You can use a filter with an unspecified search (** search=***) or with a query string that includes terms, phrases, operators, and patterns.

| Filter scenario | Description |
|---|---|
| Range filters | In Azure AI Search, range queries are built using the filter parameter. For more information and examples, see
|

[faceted navigation](search-faceted-navigation)tree, users can select facets. When backed by filters, search results narrow on each click. Each facet is backed by a filter that excludes documents that no longer match the criteria provided by the facet.Note

Text that's used in a filter expression is not analyzed during query processing. The text input is presumed to be a verbatim case-sensitive character pattern that either succeeds or fails on the match. Filter expressions are constructed using [OData syntax](query-odata-filter-orderby-syntax) and passed in a ** filter** parameter in all

*filterable*fields in your index. For more information, see

[Filters in Azure AI Search](search-filters).

## Geospatial search

Geospatial search matches on a location's latitude and longitude coordinates for "find near me" or map-based search experience. In Azure AI Search, you can implement geospatial search by following these steps:

- Define a filterable field of one of these types:
[Edm.GeographyPoint, Collection(Edm.GeographyPoint, Edm.GeographyPolygon)](/en-us/rest/api/searchservice/supported-data-types). - Verify the incoming documents include the appropriate coordinates.
- After indexing is complete, build a query that uses a filter and a
[geo-spatial function](search-query-odata-geo-spatial-functions).

Geospatial search uses kilometers for distance. Coordinates are specified in this format: `(longitude, latitude`

).

Here's an example of a filter for geospatial search. This filter finds other `Location`

fields in the search index that have coordinates within a 300-kilometer radius of the geography point (in this example, Washington D.C.). It returns address information in the result, and includes an optional `facets`

clause for self-navigation based on location.

```
POST https://{{searchServiceName}}.search.windows.net/indexes/hotels-vector-quickstart/docs/search?api-version=2025-09-01
{
"count": true,
"search": "*",
"filter": "geo.distance(Location, geography'POINT(-77.03241 38.90166)') le 300",
"facets": [ "Address/StateProvince"],
"select": "HotelId, HotelName, Address/StreetAddress, Address/City, Address/StateProvince",
"top": 7
}
```


For more information and examples, see [Geospatial search example](search-query-simple-examples#example-6-geospatial-search).

## Document look-up

In contrast with the previously described query forms, this one retrieves a single [search document by ID](/en-us/rest/api/searchservice/documents/get), with no corresponding index search or scan. Only the one document is requested and returned. When a user selects an item in search results, retrieving the document and populating a details page with fields is a typical response, and a document look-up is the operation that supports it.

## Advanced search: fuzzy, wildcard, proximity, regex

An advanced query form depends on the Full Lucene parser and operators that trigger a specific query behavior.

| Query type | Usage | Examples and more information |
|---|---|---|
|

**parameter,**`search`

`queryType=full`

[Fielded search example](search-query-lucene-examples#example-1-fielded-search)[fuzzy search](query-lucene-syntax#bkmk_fuzzy)**parameter,**`search`

`queryType=full`

[Fuzzy search example](search-query-lucene-examples#example-2-fuzzy-search)[proximity search](query-lucene-syntax#bkmk_proximity)**parameter,**`search`

`queryType=full`

[Proximity search example](search-query-lucene-examples#example-3-proximity-search)[term boosting](query-lucene-syntax#bkmk_termboost)**parameter,**`search`

`queryType=full`

[Term boosting example](search-query-lucene-examples#example-4-term-boosting)[regular expression search](query-lucene-syntax#bkmk_regex)**parameter,**`search`

`queryType=full`

[Regular expression example](search-query-lucene-examples#example-5-regex)[wildcard or prefix search](query-lucene-syntax#bkmk_wildcard)**parameter with ***`search`

**or**`~`

**,**`?`

`queryType=full`

`~`

) or single character (`?`

). [Wildcard search example](search-query-lucene-examples#example-6-wildcard-search)## Next steps

For a closer look at query implementation, review the examples for each syntax. If you're new to full text search, a closer look at what the query engine does might be an equally good choice.


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-shaper.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-shaper -->

# Shaper cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Shaper** skill is used to reshape or modify the structure of the [in-memory enrichment tree](cognitive-search-working-with-skillsets#enrichment-tree) created by a skillset. If skill outputs can't be mapped directly to search fields, you can add a **Shaper** skill to create the data shape you need for your search index or knowledge store.

Primary use-cases for this skill include:

You're populating a knowledge store. The physical structure of the tables and objects of a knowledge store are defined through projections. A

**Shaper**skill adds granularity by creating data shapes that can be pushed to the projections.You want to map multiple skill outputs into a single structure in your search index, usually a

[complex type](search-howto-complex-data-types), as described in[scenario 1](#scenario-1-complex-types).Skills produce multiple outputs, but you want to combine into a single field (it doesn't have to be a complex type), as described in

[scenario 2](#scenario-2-input-consolidation). For example, combining titles and authors into a single field.Skills produce multiple outputs with child elements, and you want to combine them. This use-case is illustrated in

[scenario 3](#nested-complex-types).

The output name of a **Shaper** skill is always "output". Internally, the pipeline can map a different name, such as "analyzedText" as shown in the examples below, but the **Shaper** skill itself returns "output" in the response. This might be important if you are debugging enriched documents and notice the naming discrepancy, or if you build a custom skill and are structuring the response yourself.

Note

This skill isn't bound to Foundry Tools. It's nonbillable and has no Foundry Tools key requirement.

## @odata.type

Microsoft.Skills.Util.ShaperSkill

## Scenario 1: complex types

Consider a scenario where you want to create a structure called *analyzedText* that has two members: *text* and *sentiment*, respectively. In an index, a multi-part searchable field is called a *complex type* and it's often created when source data has a corresponding complex structure that maps to it.

However, another approach for creating complex types is through the **Shaper** skill. By including this skill in a skillset, the in-memory operations during skillset processing can output data shapes with nested structures, which can then be mapped to a complex type in your index.

The following example skill definition provides the member names as the input.

```
{
"@odata.type": "#Microsoft.Skills.Util.ShaperSkill",
"context": "/document/content/phrases/*",
"inputs": [
{
"name": "text",
"source": "/document/content/phrases/*"
},
{
"name": "sentiment",
"source": "/document/content/phrases/*/sentiment"
}
],
"outputs": [
{
"name": "output",
"targetName": "analyzedText"
}
]
}
```


### Sample index

A skillset is invoked by an indexer, and an indexer requires an index. A complex field representation in your index might look like the following example.

```
"name":"my-index",
"fields":[
{ "name":"myId", "type":"Edm.String", "key":true, "filterable":true },
{ "name":"analyzedText", "type":"Edm.ComplexType",
"fields":[
{
"name":"text",
"type":"Edm.String",
"facetable":false,
"filterable":false,
"searchable":true,
"sortable":false },
{
"name":"sentiment",
"type":"Edm.Double",
"facetable":true,
"filterable":true,
"searchable":true,
"sortable":true }
}
```


### Skill input

An incoming JSON document providing usable input for this **Shaper** skill could be:

```
{
"values": [
{
"recordId": "1",
"data": {
"text": "this movie is awesome",
"sentiment": 0.9
}
}
]
}
```


### Skill output

The **Shaper** skill generates a new element called *analyzedText* with the combined elements of *text* and *sentiment*. This output conforms to the index schema. It will be imported and indexed in an Azure AI Search index.

```
{
"values": [
{
"recordId": "1",
"data":
{
"analyzedText":
{
"text": "this movie is awesome" ,
"sentiment": 0.9
}
}
}
]
}
```


## Scenario 2: input consolidation

In another example, imagine that at different stages of pipeline processing, you have extracted the title of a book, and chapter titles on different pages of the book. You could now create a single structure composed of these various outputs.

The **Shaper** skill definition for this scenario might look like the following example:

```
{
"@odata.type": "#Microsoft.Skills.Util.ShaperSkill",
"context": "/document",
"inputs": [
{
"name": "title",
"source": "/document/content/title"
},
{
"name": "chapterTitles",
"source": "/document/content/pages/*/chapterTitles/*/title"
}
],
"outputs": [
{
"name": "output",
"targetName": "titlesAndChapters"
}
]
}
```


### Skill output

In this case, the **Shaper** flattens all chapter titles to create a single array.

```
{
"values": [
{
"recordId": "1",
"data": {
"titlesAndChapters": {
"title": "How to be happy",
"chapterTitles": [
"Start young",
"Laugh often",
"Eat, sleep and exercise"
]
}
}
}
]
}
```


## Scenario 3: input consolidation from nested contexts

Imagine you have chapter titles and chapter numbers of a book and have run entity recognition and key phrases on the contents and now need to aggregate results from the different skills into a single shape with the chapter name, entities, and key phrases.

This example adds an optional `sourceContext`

property to the "chapterTitles" input. The `source`

and `sourceContext`

properties are mutually exclusive. If the input is at the context of the skill, you can use `source`

. If the input is at a *different* context than the skill context, use `sourceContext`

. The `sourceContext`

requires you to define a nested input, where each input has a `source`

that identifies the specific element used to populate the named node.

The **Shaper** skill definition for this scenario might look like the following example:

```
{
"@odata.type": "#Microsoft.Skills.Util.ShaperSkill",
"context": "/document",
"inputs": [
{
"name": "title",
"source": "/document/content/title"
},
{
"name": "chapterTitles",
"sourceContext": "/document/content/pages/*/chapterTitles/*",
"inputs": [
{
"name": "title",
"source": "/document/content/pages/*/chapterTitles/*/title"
},
{
"name": "number",
"source": "/document/content/pages/*/chapterTitles/*/number"
}
]
}
],
"outputs": [
{
"name": "output",
"targetName": "titlesAndChapters"
}
]
}
```


### Skill output

In this case, the **Shaper** creates a complex type. This structure exists in-memory. If you want to save it to a [knowledge store](knowledge-store-concept-intro), you should create a projection in your skillset that defines storage characteristics.

```
{
"values": [
{
"recordId": "1",
"data": {
"titlesAndChapters": {
"title": "How to be happy",
"chapterTitles": [
{ "title": "Start young", "number": 1},
{ "title": "Laugh often", "number": 2},
{ "title": "Eat, sleep and exercise", "number": 3}
]
}
}
}
]
}
```
