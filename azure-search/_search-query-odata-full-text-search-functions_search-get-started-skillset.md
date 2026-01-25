---
merged_at: 2026-01-25T02:11:58.459497
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-query-odata-full-text-search-functions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-odata-full-text-search-functions -->

# OData full-text search functions in Azure AI Search - search.ismatch and search.ismatchscoring

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

# OData full-text search functions in Azure AI Search -

Azure AI Search supports full-text search in the context of [OData filter expressions](query-odata-filter-orderby-syntax) via the `search.ismatch`

and `search.ismatchscoring`

functions. These functions allow you to combine full-text search with strict Boolean filtering in ways that aren't possible just by using the top-level `search`

parameter of the [Search API](/en-us/rest/api/searchservice/documents/search-post).

Note

The `search.ismatch`

and `search.ismatchscoring`

functions are only supported in filters in the [Search API](/en-us/rest/api/searchservice/documents/search-post). They aren't supported in the [Suggest](/en-us/rest/api/searchservice/documents/suggest-post) or [Autocomplete](/en-us/rest/api/searchservice/documents/autocomplete-post) APIs.

## Syntax

The following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) defines the grammar of the `search.ismatch`

and `search.ismatchscoring`

functions:

```
search_is_match_call ::=
'search.ismatch'('scoring')?'(' search_is_match_parameters ')'
search_is_match_parameters ::=
string_literal(',' string_literal(',' query_type ',' search_mode)?)?
query_type ::= "'full'" | "'simple'"
search_mode ::= "'any'" | "'all'"
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

### search.ismatch

The `search.ismatch`

function evaluates a full-text search query as a part of a filter expression. Matching documents are returned in the result set. The following overloads of this function are available:

`search.ismatch(search)`

`search.ismatch(search, searchFields)`

`search.ismatch(search, searchFields, queryType, searchMode)`


The parameters are defined in the following table:

| Parameter name | Type | Description |
|---|---|---|
`search` |
`Edm.String` |
The search query (in either
|

`searchFields`

`Edm.String`

[fielded search](query-lucene-syntax#bkmk_fields)in the`search`

parameter, the field specifiers in the Lucene query override any fields specified in this parameter.`queryType`

`Edm.String`

`'simple'`

or `'full'`

; defaults to `'simple'`

. Specifies what query language was used in the `search`

parameter.`searchMode`

`Edm.String`

`'any'`

or `'all'`

, defaults to `'any'`

. Indicates whether any or all of the search terms in the `search`

parameter must be matched in order to count the document as a match. When you use the [Lucene Boolean operators](query-lucene-syntax#bkmk_boolean)in the`search`

parameter, they take precedence over this parameter.All the above parameters are equivalent to the corresponding [search request parameters in the Search API](/en-us/rest/api/searchservice/documents/search-post).

The `search.ismatch`

function returns a value of type `Edm.Boolean`

, which allows you to compose it with other filter subexpressions using the Boolean [logical operators](search-query-odata-logical-operators).

Note

Azure AI Search doesn't support using `search.ismatch`

or `search.ismatchscoring`

inside lambda expressions. This means it isn't possible to write filters over collections of objects that can correlate full-text search matches with strict filter matches on the same object. For more information on this limitation as well as examples, see [Troubleshooting collection filters in Azure AI Search](search-query-troubleshoot-collection-filters). For more in-depth information on why this limitation exists, see [Understanding collection filters in Azure AI Search](search-query-understand-collection-filters).

### search.ismatchscoring

The `search.ismatchscoring`

function, like the `search.ismatch`

function, returns `true`

for documents that match the full-text search query passed as a parameter. The difference between them is that the relevance score of documents matching the `search.ismatchscoring`

query contributes to the overall document score, whereas for `search.ismatch`

, the document score doesn't change. The following overloads of this function are available with parameters identical to those of `search.ismatch`

:

`search.ismatchscoring(search)`

`search.ismatchscoring(search, searchFields)`

`search.ismatchscoring(search, searchFields, queryType, searchMode)`


Both the `search.ismatch`

and `search.ismatchscoring`

functions can be used in the same filter expression.

## Examples

Find documents with the word "waterfront". This filter query is identical to a [search request](/en-us/rest/api/searchservice/documents/search-post) with `search=waterfront`

.

```
search.ismatchscoring('waterfront')
```


Here's the full query syntax for this request, which you can run in Search Explorer in the Azure portal. Output consists of matches on waterfront, water, and front.

```
{
"search": "*",
"select": "HotelId, HotelName, Description",
"searchMode": "all",
"queryType": "simple",
"count": true,
"filter": "search.ismatchscoring('waterfront')"
}
```


Find documents with the word "pool" and rating greater or equal to 4, or documents with the word "motel" and equal to 3.2. Note, this request couldn't be expressed without the `search.ismatchscoring`

function.

```
search.ismatchscoring('pool') and Rating ge 4 or search.ismatchscoring('motel') and Rating eq 3.2
```


Here's the full query syntax for this request for Search Explorer. Output consists of matches on hotels with pools having a rating greater than 4, *or* motels with a rating equal to 3.2.

```
{
"search": "*",
"select": "HotelId, HotelName, Description, Tags, Rating",
"searchMode": "all",
"queryType": "simple",
"count": true,
"filter": "search.ismatchscoring('pool') and Rating ge 4 or search.ismatchscoring('motel') and Rating eq 3.2"
}
```


Find documents without the word "luxury".

```
not search.ismatch('luxury')
```


Here's the full query syntax for this request. Output consists of matches on the term luxury.

```
{
"search": "*",
"select": "HotelId, HotelName, Description, Tags, Rating",
"searchMode": "all",
"queryType": "simple",
"count": true,
"filter": "not search.ismatch('luxury')"
}
```


Find documents with the phrase "ocean" or rating equal to 3.2. The `search.ismatchscoring`

query is executed only against fields `HotelName`

and `Description`

.

Here's the full query syntax for this request. Documents that match only the second clause of the disjunction are returned too (specifically, hotels with `Rating`

equal to `3.2`

). To make it clear that those documents didn't match any of the scored parts of the expression, they're returned with score equal to zero.

```
{
"search": "*",
"select": "HotelId, HotelName, Description, Rating",
"searchMode": "all",
"queryType": "full",
"count": true,
"filter": "search.ismatchscoring('ocean', 'Description,HotelName') or Rating eq 3.2"
}
```


Output consists of 4 matches: hotels that mention "ocean" in the Description or Hotel Name, or hotels with a rating of 3.2. Notice the search score of zero for matches on the second clause.

```
{
"@odata.count": 4,
"value": [
{
"@search.score": 1.6076145,
"HotelId": "18",
"HotelName": "Ocean Water Resort & Spa",
"Description": "New Luxury Hotel for the vacation of a lifetime. Bay views from every room, location near the pier, rooftop pool, waterfront dining & more.",
"Rating": 4.2
},
{
"@search.score": 1.0594962,
"HotelId": "41",
"HotelName": "Windy Ocean Motel",
"Description": "Oceanfront hotel overlooking the beach features rooms with a private balcony and 2 indoor and outdoor pools. Inspired by the natural beauty of the island, each room includes an original painting of local scenes by the owner. Rooms include a mini fridge, Keurig coffee maker, and flatscreen TV. Various shops and art entertainment are on the boardwalk, just steps away.",
"Rating": 3.5
},
{
"@search.score": 0,
"HotelId": "40",
"HotelName": "Trails End Motel",
"Description": "Only 8 miles from Downtown. On-site bar/restaurant, Free hot breakfast buffet, Free wireless internet, All non-smoking hotel. Only 15 miles from airport.",
"Rating": 3.2
},
{
"@search.score": 0,
"HotelId": "26",
"HotelName": "Planetary Plaza & Suites",
"Description": "Extend Your Stay. Affordable home away from home, with amenities like free Wi-Fi, full kitchen, and convenient laundry service.",
"Rating": 3.2
}
]
}
```


Find documents where the terms "hotel" and "airport" are within 5 words from each other in the description of the hotel, and where smoking isn't allowed in at least some of the rooms.

```
search.ismatch('"hotel airport"~5', 'Description', 'full', 'any') and Rooms/any(room: not room/SmokingAllowed)
```


Here's the full query syntax. To run in Search Explorer, escape the interior quotation marks with a backslash character.

```
{
"search": "*",
"select": "HotelId, HotelName, Description, Tags, Rating",
"searchMode": "all",
"queryType": "simple",
"count": true,
"filter": "search.ismatch('\"hotel airport\"~5', 'Description', 'full', 'any') and Rooms/any(room: not room/SmokingAllowed)"
}
```


Output consists of a single document where the terms "hotel" and "airport" are within 5 words distance. Smoking is allowed for several rooms in most hotels, including the one in this search result.

```
{
"@odata.count": 1,
"value": [
{
"@search.score": 1,
"HotelId": "40",
"HotelName": "Trails End Motel",
"Description": "Only 8 miles from Downtown. On-site bar/restaurant, Free hot breakfast buffet, Free wireless internet, All non-smoking hotel. Only 15 miles from airport.",
"Tags": [
"bar",
"free wifi",
"restaurant"
],
"Rating": 3.2
}
]
}
```


Find documents that have a word that starts with the letters "lux" in the Description field. This query uses [prefix search](query-simple-syntax#prefix-queries) in combination with `search.ismatch`

.

```
search.ismatch('lux*', 'Description')
```


Here's a full query:

```
{
"search": "*",
"select": "HotelId, HotelName, Description, Tags, Rating",
"searchMode": "all",
"queryType": "simple",
"count": true,
"filter": "search.ismatch('lux*', 'Description')"
}
```


Output consists of the following matches.

```
{
"@odata.count": 4,
"value": [
{
"@search.score": 1,
"HotelId": "18",
"HotelName": "Ocean Water Resort & Spa",
"Description": "New Luxury Hotel for the vacation of a lifetime. Bay views from every room, location near the pier, rooftop pool, waterfront dining & more.",
"Tags": [
"view",
"pool",
"restaurant"
],
"Rating": 4.2
},
{
"@search.score": 1,
"HotelId": "13",
"HotelName": "Luxury Lion Resort",
"Description": "Unmatched Luxury. Visit our downtown hotel to indulge in luxury accommodations. Moments from the stadium and transportation hubs, we feature the best in convenience and comfort.",
"Tags": [
"bar",
"concierge",
"restaurant"
],
"Rating": 4.1
},
{
"@search.score": 1,
"HotelId": "16",
"HotelName": "Double Sanctuary Resort",
"Description": "5 star Luxury Hotel - Biggest Rooms in the city. #1 Hotel in the area listed by Traveler magazine. Free WiFi, Flexible check in/out, Fitness Center & espresso in room.",
"Tags": [
"view",
"pool",
"restaurant",
"bar",
"continental breakfast"
],
"Rating": 4.2
},
{
"@search.score": 1,
"HotelId": "14",
"HotelName": "Twin Vortex Hotel",
"Description": "New experience in the making. Be the first to experience the luxury of the Twin Vortex. Reserve one of our newly-renovated guest rooms today.",
"Tags": [
"bar",
"restaurant",
"concierge"
],
"Rating": 4.4
}
]
}
```


---

<!-- DOCUMENTO FUSIONADO: search-get-started-skillset.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-get-started-skillset -->

# Quickstart: Create a skillset in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The **Import data (new)** wizard now supports keyword search, which was previously only available in the **Import data** wizard. We recommend the new wizard for an improved search experience. For more information about how we're consolidating the wizards, see [Import data wizards in the Azure portal](search-import-data-portal).

In this quickstart, you learn how a skillset in Azure AI Search adds optical character recognition (OCR), image analysis, language detection, text merging, and entity recognition to generate text-searchable content in an index.

You can run the **Import data (new)** wizard in the Azure portal to apply skills that create and transform textual content during indexing. The input is your raw data, usually blobs in Azure Storage. The output is a searchable index containing AI-generated image text, captions, and entities. You can then query generated content in the Azure portal using [ Search explorer](search-explorer).

Before you run the wizard, you create a few resources and upload sample files.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An Azure AI Search service.

[Create a service](search-create-service-portal)or[find an existing service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)in your current subscription. You can use a free service for this quickstart.An

[Azure Storage account](/en-us/azure/storage/common/storage-account-create). Use Azure Blob Storage on a standard performance (general-purpose v2) account. To avoid bandwidth charges, use the same region as Azure AI Search.

Note

This quickstart uses [Foundry Tools](https://azure.microsoft.com/services/cognitive-services/) for AI enrichment. Because the workload is small, Foundry Tools is tapped behind the scenes for free processing up to 20 transactions. Therefore, you don't need to create a Microsoft Foundry resource.

## Prepare sample data

In this section, you create an Azure Storage container to store sample data consisting of various file types, including images and application files that aren't full-text searchable in their native formats.

To prepare the sample data for this quickstart:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your Azure Storage account.From the left pane, select

**Data storage**>**Containers**.Create a container, and then upload the

[sample data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/ai-enrichment-mixed-media)to the container.

## Run the wizard

To run the wizard:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.On the

**Overview**page, select**Import data (new)**.Select

**Azure Blob Storage**for the data source.Select

**Keyword search**.

### Step 1: Create a data source

Azure AI Search requires a connection to a data source for content ingestion and indexing. In this case, the data source is your Azure Storage account.

To create the data source:

On the

**Connect to your data**page, select your Azure subscription.Select your storage account, and then select the container you created.

Select

**Next**.

If you get `Error detecting index schema from data source`

, the indexer that powers the wizard can't connect to your data source. The data source most likely has security protections. Try the following solutions, and then rerun the wizard.

| Security feature | Solution |
|---|---|
| Resource requires Azure roles, or its access keys are disabled. |
|

[Create an inbound rule for Azure AI Search and the Azure portal](search-indexer-howto-access-ip-restricted).[Connect over a private endpoint](search-indexer-howto-access-private).### Step 2: Add cognitive skills

The next step is to configure AI enrichment to invoke OCR, image analysis, and entity recognition.

OCR and image analysis are available for blobs in Azure Blob Storage and Azure Data Lake Storage (ADLS) Gen2 and for image content in Microsoft OneLake. Images can be standalone files or embedded images in a PDF or other files.

To add the skills:

Select

**Extract entities**, and then select the gear icon.Select and save the following checkboxes:

**Persons****Locations****Organizations**

Select

**Extract text from images**, and then select the gear icon.Select and save the following checkboxes:

**Generate tags****Categorize content**

Leave the

**Use a free AI service (limited enrichments)**checkbox selected.The sample data consists of 14 files, so the free allotment of 20 transactions on Foundry Tools is sufficient.

Select

**Next**.

### Step 3: Configure the index

An index contains your searchable content. The wizard can usually create the schema by sampling the data source. In this step, you review the generated schema and potentially revise any settings.

For this quickstart, the wizard sets reasonable defaults:

Default fields are based on metadata properties of existing blobs and new fields for the enrichment output, such as

`persons`

,`locations`

, and`organizations`

. Data types are inferred from metadata and by data sampling.Default document key is

`metadata_storage_path`

, which is selected because the field contains unique values.Default field attributes are based on the skills you selected. For example, fields created by the Entity Recognition skill (

`persons`

,`locations`

, and`organizations`

) are**Retrievable**,**Filterable**,**Facetable**, and**Searchable**. To view and change these attributes, select a field, and then select**Configure field**.**Retrievable**fields can be returned in results, while**Searchable**fields support full-text search. Use**Filterable**if you want to use fields in a filter expression.Marking a field as

**Retrievable**doesn't mean that the field*must*appear in search results. You can control which fields are returned by using the`select`

query parameter.

After you review the index schema, select **Next**.

### Step 4: Skip advanced settings

The wizard offers advanced settings for semantic ranking and index scheduling, which are beyond the scope of this quickstart. Skip this step by selecting **Next**.

### Step 5: Review and create objects

The last step is to review your configuration and create the index, indexer, and data source on your search service. The indexer automates the process of extracting content from your data source, loading the index, and driving skillset execution.

To review and create the objects:

Accept the default

**Objects name prefix**.Review the object configurations.

AI enrichment, semantic ranker, and indexer scheduling are either disabled or set to their default values because you skipped their wizard steps.

Select

**Create**to simultaneously create the objects and run the indexer.

## Monitor status

You can monitor the creation of the indexer in the Azure portal. Skills-based indexing takes longer than text-based indexing, especially OCR and image analysis.

To monitor the progress of the indexer:

From the left pane, select

**Indexers**.Select your indexer from the list.

Select

**Success**(or**Failed**) to view execution details.

In this quickstart, there are a few warnings, including `Could not execute skill because one or more skill input was invalid.`

This warning tells you that a PNG file in the data source doesn't provide a text input to Entity Recognition. It occurs because the upstream OCR skill didn't recognize any text in the image and couldn't provide a text input to the downstream Entity Recognition skill.

Warnings are common in skillset execution. As you become familiar with how skills iterate over your data, you might begin to notice patterns and learn which warnings are safe to ignore.

## Query in Search explorer

To query your index:

From the left pane, select

**Indexes**.Select your index from the list. If the index has zero documents or storage, wait for the Azure portal to refresh.

On the

**Search explorer**tab, enter a search string, such as`satya nadella`

.

The search bar accepts keywords, quote-enclosed phrases, and operators. For example: `"Satya Nadella" +"Bill Gates" +"Steve Ballmer"`


Results are returned as verbose JSON, which can be hard to read, especially in large documents. Here are tips for searching in this tool:

- Switch to the JSON view to specify parameters that shape results.
- Add
`select`

to limit the fields in results. - Add
`count`

to show the number of matches. - Use Ctrl-F to search within the JSON for specific properties or terms.

Here's some JSON you can paste into the view:

```
{
"search": "\"Satya Nadella\" +\"Bill Gates\" +\"Steve Ballmer\"",
"count": true,
"select": "merged_content, persons"
}
```


Tip

Query strings are case sensitive, so if you get an "unknown field" message, check **Fields** or **Index Definition (JSON)** to verify the name and case.

## Takeaways

You've created your first skillset and learned the basic steps of skills-based indexing.

Some key concepts that we hope you picked up include the dependencies. A skillset is bound to an indexer, and indexers are Azure and source-specific. Although this quickstart uses Azure Blob Storage, other Azure data sources are available. For more information, see [Indexers in Azure AI Search](search-indexer-overview).

Another important concept is that skills operate over content types, and when you use heterogeneous content, some inputs are skipped. Also, large files or fields might exceed the indexer limits of your service tier. It's normal to see warnings when these events occur.

The output is routed to a search index, and there's a mapping between name-value pairs created during indexing and individual fields in your index. Internally, the wizard sets up [an enrichment tree](cognitive-search-concept-annotations-syntax) and defines a [skillset](cognitive-search-defining-skillset), establishing the order of operations and general flow. These steps are hidden in the wizard, but when you start writing code, these concepts become important.

Finally, you learned that you can verify content by querying the index. Ultimately, Azure AI Search provides a searchable index that you can query using either [simple](/en-us/rest/api/searchservice/simple-query-syntax-in-azure-search) or [fully extended query syntax](/en-us/rest/api/searchservice/lucene-query-syntax-in-azure-search). An index containing enriched fields is like any other. You can incorporate standard or [custom analyzers](search-analyzers), [scoring profiles](/en-us/rest/api/searchservice/add-scoring-profiles-to-a-search-index), [synonyms](search-synonyms), [faceted navigation](search-faceted-navigation), geo-search, and other Azure AI Search features.

## Clean up resources

When you're working in your own subscription, it's a good idea at the end of a project to identify whether you still need the resources you created. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.

You can find and manage resources in the Azure portal by selecting **All resources** or **Resource groups** from the left pane.

If you used a free service, remember that you're limited to three indexes, indexers, and data sources. You can delete individual items in the Azure portal to stay under the limit.

## Next step

You can use the Azure portal, REST APIs, or an Azure SDK to create skillsets. Try the REST APIs by using a REST client and more sample data:
