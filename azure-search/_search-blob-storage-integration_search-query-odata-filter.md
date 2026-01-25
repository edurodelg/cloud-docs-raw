---
merged_at: 2026-01-25T03:18:14.037951
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-blob-storage-integration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-blob-storage-integration -->

# Search over Azure Blob Storage content

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Searching across the variety of content types stored in Azure Blob Storage can be a difficult problem to solve, but [Azure AI Search](search-what-is-azure-search) provides deep integration at the content layer, extracting and inferring textual information, which can then be queried in a search index.

In this article, review the basic workflow for extracting content and metadata from blobs and sending it to a [search index](search-what-is-an-index) in Azure AI Search. The resulting index can be queried using full text search or vector search. Optionally, you can send processed blob content to a [knowledge store](knowledge-store-concept-intro) for non-search scenarios.

Note

Already familiar with the workflow and composition? [Configure a blob indexer](search-how-to-index-azure-blob-storage) is your next step.

## What it means to add search over blob data

Azure AI Search is a standalone search service that supports indexing and query workloads over user-defined indexes that contain your private searchable content hosted in the cloud. Co-locating your searchable content with the query engine in the cloud is necessary for performance, returning results at a speed users have come to expect from search queries.

Azure AI Search integrates with Azure Blob Storage at the indexing layer, importing your blob content as search documents that are indexed into *inverted indexes* and other query structures that support free-form text queries, vector queries, and filter expressions. Because your blob content is indexed into a search index, you can use the full range of query features in Azure AI Search to find information in your blob content.

Inputs are your blobs, in a single container, in Azure Blob Storage. Blobs can be almost any kind of text data. If your blobs contain images, you can add [AI enrichment](cognitive-search-concept-intro) to create and extract text and features from images.

Output is always an Azure AI Search index, used for fast text search, retrieval, and exploration in client applications. In between is the indexing pipeline architecture itself. The pipeline is based on the *indexer* feature, discussed further on in this article.

Once the index is created and populated, it exists independently of your blob container, but you can rerun indexing operations to refresh your index based on changed documents. Timestamp information on individual blobs is used for change detection. You can opt for either scheduled execution or on-demand indexing as the refresh mechanism.

## Resources used in a blob-search solution

You need Azure AI Search, Azure Blob Storage, and a client. Azure AI Search is typically one of several components in a solution, where your application code issues query API requests and handles the response. You might also write application code to handle indexing, although for proof-of-concept testing and impromptu tasks, it's common to use the Azure portal as the search client.

Within Blob Storage, you'll need a container that provides source content. You can set file inclusion and exclusion criteria, and specify which parts of a blob are indexed in Azure AI Search.

You can start directly in your Storage Account portal page.

In the left navigation page under

**Data management**, select**Azure AI Search**to select or create a search service.Use an

[import wizard](search-get-started-skillset)to extract and optionally create searchable content from your blobs. The workflow creates an indexer, data source, index, and optional skillset on your Azure AI Search service.Use

[Search explorer](search-explorer)in the search portal page to query your content.

The wizard is the best place to start, but you'll discover more flexible options when you [configure a blob indexer](search-how-to-index-azure-blob-storage) yourself. You can use a [REST client](search-get-started-text). [Tutorial: Index and search semi-structured data (JSON blobs)](search-semi-structured-data) walks you through the steps of calling the REST API.

## How blobs are indexed

By default, most blobs are indexed as a single search document in the index, including blobs with structured content, such as JSON or CSV, which are indexed as a single chunk of text. However, for JSON or CSV documents that have an internal structure (delimiters), you can assign parsing modes to generate individual search documents for each line or element:

A compound or embedded document (such as a ZIP archive, a Word document with embedded Outlook email containing attachments, or an .MSG file with attachments) is also indexed as a single document. For example, all images extracted from the attachments of an .MSG file will be returned in the normalized_images field. If you have images, consider adding [AI enrichment](cognitive-search-concept-intro) to get more search utility from that content.

Textual content of a document is extracted into a string field named "content". You can also extract standard and user-defined metadata.

Note

Azure AI Search imposes [indexer limits](search-limits-quotas-capacity#indexer-limits) on how much text it extracts depending on the pricing tier. A warning will appear in the indexer status response if documents are truncated.

## Use a blob indexer for content extraction

An *indexer* is a data-source-aware subservice in Azure AI Search, equipped with internal logic for sampling data, reading and retrieving data and metadata, and serializing data from native formats into JSON documents for subsequent import.

Blobs in Azure Storage are indexed using the [blob indexer](search-how-to-index-azure-blob-storage). You can invoke this indexer by using the **Azure AI Search** command in Azure Storage, an [import wizard](search-import-data-portal) in the Azure portal, a REST API, or the .NET SDK. In code, you use this indexer by setting the type, and by providing connection information that includes an Azure Storage account along with a blob container. You can subset your blobs by creating a virtual directory, which you can then pass as a parameter, or by filtering on a file type extension.

An indexer ["cracks a document"](search-indexer-overview#document-cracking), opening a blob to inspect content. After connecting to the data source, it's the first step in the pipeline. For blob data, this is where PDF, Office docs, and other content types are detected. Document cracking with text extraction is no charge. If your blobs contain image content, images are ignored unless you [add AI enrichment](cognitive-search-concept-intro). Standard indexing applies only to text content.

The Azure blob indexer comes with configuration parameters and supports change tracking if the underlying data provides sufficient information. You can learn more about the core functionality in [Index data from Azure Blob Storage](search-how-to-index-azure-blob-storage).

### Supported access tiers

Blob storage [access tiers](/en-us/azure/storage/blobs/access-tiers-overview) include hot, cool, cold, and archive. Indexers can retrieve blobs on hot, cool, and cold access tiers.

### Supported content types

By running a blob indexer over a container, you can extract text and metadata from the following content types with a single query:

- CSV (see
[Indexing CSV blobs](search-how-to-index-azure-blob-csv)) - EML
- EPUB
- GZ
- HTML
- JSON (see
[Indexing JSON blobs](search-how-to-index-azure-blob-json)) - KML (XML for geographic representations)
- Markdown
- Microsoft Office formats: DOCX/DOC/DOCM, XLSX/XLS/XLSM, PPTX/PPT/PPTM, MSG (Outlook emails), XML (both 2003 and 2006 WORD XML)
- Open Document formats: ODT, ODS, ODP
- Plain text files (see also
[Indexing plain text](search-how-to-index-azure-blob-plaintext)) - RTF
- XML
- ZIP

### Controlling which blobs are indexed

You can control which blobs are indexed, and which are skipped, by the blob's file type or by setting properties on the blob themselves, causing the indexer to skip over them.

Include specific file extensions by setting `"indexedFileNameExtensions"`

to a comma-separated list of file extensions (with a leading dot). Exclude specific file extensions by setting `"excludedFileNameExtensions"`

to the extensions that should be skipped. If the same extension is in both lists, it's excluded from indexing.

```
PUT /indexers/[indexer name]?api-version=2025-09-01
{
"parameters" : {
"configuration" : {
"indexedFileNameExtensions" : ".pdf, .docx",
"excludedFileNameExtensions" : ".png, .jpeg"
}
}
}
```


### Add "skip" metadata the blob

The indexer configuration parameters apply to all blobs in the container or folder. Sometimes, you want to control how *individual blobs* are indexed.

Add the following metadata properties and values to blobs in Blob Storage. When the indexer encounters this property, it skips the blob or its content in the indexing run.

| Property name | Property value | Explanation |
|---|---|---|
| "AzureSearch_Skip" | `"true"` |
Instructs the blob indexer to completely skip the blob. Neither metadata nor content extraction is attempted. This is useful when a particular blob fails repeatedly and interrupts the indexing process. |
| "AzureSearch_SkipContent" | `"true"` |
This is equivalent to the `"dataToExtract": "allMetadata"` setting described
|

### Indexing blob metadata

A common scenario that makes it easy to sort through blobs of any content type is to [index both custom metadata and system properties](search-blob-metadata-properties) for each blob. In this way, information for all blobs is indexed regardless of document type, stored in an index in your search service. Using your new index, you can then proceed to sort, filter, and facet across all Blob storage content.

Note

Blob Index tags are natively indexed by the Blob storage service and exposed for querying. If your blobs' key/value attributes require indexing and filtering capabilities, Blob Index tags should be used instead of metadata.

To learn more about Blob Index, see [Manage and find data on Azure Blob Storage with Blob Index](/en-us/azure/storage/blobs/storage-manage-find-blobs).

## Search blob content in a search index

The output of an indexer is a search index, used for interactive exploration using free text and filtered queries in a client app. For initial exploration and verification of content, we recommend starting with [Search Explorer](search-explorer) in the Azure portal to examine document structure. In Search explorer, you can use:

A more permanent solution is to gather query inputs and present the response as search results in a client application.


---

<!-- DOCUMENTO FUSIONADO: search-query-odata-filter.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-odata-filter -->

# OData $filter syntax in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, the **$filter** parameter specifies inclusion or exclusion criteria for returning matches in search results. This article describes the OData syntax of **$filter** and provides examples.

Field path construction and constants are described in the [OData language overview in Azure AI Search](query-odata-filter-orderby-syntax). For more information about filter scenarios, see [Filters in Azure AI Search](search-filters).

## Syntax

A filter in the OData language is a Boolean expression, which in turn can be one of several types of expression, as shown by the following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)):

```
boolean_expression ::=
collection_filter_expression
| logical_expression
| comparison_expression
| boolean_literal
| boolean_function_call
| '(' boolean_expression ')'
| variable
/* This can be a range variable in the case of a lambda, or a field path. */
variable ::= identifier | field_path
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

The types of Boolean expressions include:

- Collection filter expressions using
`any`

or`all`

. These apply filter criteria to collection fields. For more information, see[OData collection operators in Azure AI Search](search-query-odata-collection-operators). - Logical expressions that combine other Boolean expressions using the operators
`and`

,`or`

, and`not`

. For more information, see[OData logical operators in Azure AI Search](search-query-odata-logical-operators). - Comparison expressions, which compare fields or range variables to constant values using the operators
`eq`

,`ne`

,`gt`

,`lt`

,`ge`

, and`le`

. For more information, see[OData comparison operators in Azure AI Search](search-query-odata-comparison-operators). Comparison expressions are also used to compare distances between geo-spatial coordinates using the`geo.distance`

function. For more information, see[OData geo-spatial functions in Azure AI Search](search-query-odata-geo-spatial-functions). - The Boolean literals
`true`

and`false`

. These constants can be useful sometimes when programmatically generating filters, but otherwise don't tend to be used in practice. - Calls to Boolean functions, including:
`geo.intersects`

, which tests whether a given point is within a given polygon. For more information, see[OData geo-spatial functions in Azure AI Search](search-query-odata-geo-spatial-functions).`search.in`

, which compares a field or range variable with each value in a list of values. For more information, see[OData](search-query-odata-search-in-function).`search.in`

function in Azure AI Search`search.ismatch`

and`search.ismatchscoring`

, which execute full-text search operations in a filter context. For more information, see[OData full-text search functions in Azure AI Search](search-query-odata-full-text-search-functions).

- Field paths or range variables of type
`Edm.Boolean`

. For example, if your index has a Boolean field called`IsEnabled`

and you want to return all documents where this field is`true`

, your filter expression can just be the name`IsEnabled`

. - Boolean expressions in parentheses. Using parentheses can help to explicitly determine the order of operations in a filter. For more information on the default precedence of the OData operators, see the next section.

### Operator precedence in filters

If you write a filter expression with no parentheses around its sub-expressions, Azure AI Search will evaluate it according to a set of operator precedence rules. These rules are based on which operators are used to combine sub-expressions. The following table lists groups of operators in order from highest to lowest precedence:

| Group | Operator(s) |
|---|---|
| Logical operators | `not` |
| Comparison operators | `eq` , `ne` , `gt` , `lt` , `ge` , `le` |
| Logical operators | `and` |
| Logical operators | `or` |

An operator that is higher in the above table will "bind more tightly" to its operands than other operators. For example, `and`

is of higher precedence than `or`

, and comparison operators are of higher precedence than either of them, so the following two expressions are equivalent:

```
Rating gt 0 and Rating lt 3 or Rating gt 7 and Rating lt 10
((Rating gt 0) and (Rating lt 3)) or ((Rating gt 7) and (Rating lt 10))
```


The `not`

operator has the highest precedence of all -- even higher than the comparison operators. That's why if you try to write a filter like this:

```
not Rating gt 5
```


You'll get this error message:

```
Invalid expression: A unary operator with an incompatible type was detected. Found operand type 'Edm.Int32' for operator kind 'Not'.
```


This error happens because the operator is associated with just the `Rating`

field, which is of type `Edm.Int32`

, and not with the entire comparison expression. The fix is to put the operand of `not`

in parentheses:

```
not (Rating gt 5)
```


### Filter size limitations

There are limits to the size and complexity of filter expressions that you can send to Azure AI Search. The limits are based roughly on the number of clauses in your filter expression. A good guideline is that if you have hundreds of clauses, you are at risk of exceeding the limit. We recommend designing your application in such a way that it doesn't generate filters of unbounded size.

Tip

Using [the search.in function](search-query-odata-search-in-function) instead of long disjunctions of equality comparisons can help avoid the filter clause limit, since a function call counts as a single clause.

## Examples

Find all hotels with at least one room with a base rate less than $200 that are rated at or above 4:

```
$filter=Rooms/any(room: room/BaseRate lt 200.0) and Rating ge 4
```


Find all hotels other than "Sea View Motel" that have been renovated since 2010:

```
$filter=HotelName ne 'Sea View Motel' and LastRenovationDate ge 2010-01-01T00:00:00Z
```


Find all hotels that were renovated in 2010 or later. The datetime literal includes time zone information for Pacific Standard Time:

```
$filter=LastRenovationDate ge 2010-01-01T00:00:00-08:00
```


Find all hotels that have parking included and where all rooms are non-smoking:

```
$filter=ParkingIncluded and Rooms/all(room: not room/SmokingAllowed)
```


- OR -

```
$filter=ParkingIncluded eq true and Rooms/all(room: room/SmokingAllowed eq false)
```


Find all hotels that are Luxury or include parking and have a rating of 5:

```
$filter=(Category eq 'Luxury' or ParkingIncluded eq true) and Rating eq 5
```


Find all hotels with the tag "wifi" in at least one room (where each room has tags stored in a `Collection(Edm.String)`

field):

```
$filter=Rooms/any(room: room/Tags/any(tag: tag eq 'wifi'))
```


Find all hotels with any rooms:

```
$filter=Rooms/any()
```


Find all hotels that don't have rooms:

```
$filter=not Rooms/any()
```


Find all hotels within 10 kilometers of a given reference point (where `Location`

is a field of type `Edm.GeographyPoint`

):

```
$filter=geo.distance(Location, geography'POINT(-122.131577 47.678581)') le 10
```


Find all hotels within a given viewport described as a polygon (where `Location`

is a field of type Edm.GeographyPoint). The polygon must be closed, meaning the first and last point sets must be the same. Also, [the points must be listed in counterclockwise order](/en-us/rest/api/searchservice/supported-data-types#Anchor_1).

```
$filter=geo.intersects(Location, geography'POLYGON((-122.031577 47.578581, -122.031577 47.678581, -122.131577 47.678581, -122.031577 47.578581))')
```


Find all hotels where the "Description" field is null. The field will be null if it was never set, or if it was explicitly set to null:

```
$filter=Description eq null
```


Find all hotels with name equal to either 'Sea View motel' or 'Budget hotel'). These phrases contain spaces, and space is a default delimiter. You can specify an alternative delimiter in single quotes as the third string parameter:

```
$filter=search.in(HotelName, 'Sea View motel,Budget hotel', ',')
```


Find all hotels with name equal to either 'Sea View motel' or 'Budget hotel' separated by '|'):

```
$filter=search.in(HotelName, 'Sea View motel|Budget hotel', '|')
```


Find all hotels where all rooms have the tag 'wifi' or 'tub':

```
$filter=Rooms/any(room: room/Tags/any(tag: search.in(tag, 'wifi, tub')))
```


Find a match on phrases within a collection, such as 'heated towel racks' or 'hairdryer included' in tags.

```
$filter=Rooms/any(room: room/Tags/any(tag: search.in(tag, 'heated towel racks,hairdryer included', ','))
```


Find documents with the word "waterfront". This filter query is identical to a [search request](/en-us/rest/api/searchservice/documents/search-post) with `search=waterfront`

.

```
$filter=search.ismatchscoring('waterfront')
```


Find documents with the word "hostel" and rating greater or equal to 4, or documents with the word "motel" and rating equal to 5. This request couldn't be expressed without the `search.ismatchscoring`

function since it combines full-text search with filter operations using `or`

.

```
$filter=search.ismatchscoring('hostel') and rating ge 4 or search.ismatchscoring('motel') and rating eq 5
```


Find documents without the word "luxury".

```
$filter=not search.ismatch('luxury')
```


Find documents with the phrase "ocean view" or rating equal to 5. The `search.ismatchscoring`

query will be executed only against fields `HotelName`

and `Description`

. Documents that matched only the second clause of the disjunction will be returned too -- hotels with `Rating`

equal to 5. Those documents will be returned with score equal to zero to make it clear that they didn't match any of the scored parts of the expression.

```
$filter=search.ismatchscoring('"ocean view"', 'Description,HotelName') or Rating eq 5
```


Find hotels where the terms "hotel" and "airport" are no more than five words apart in the description, and where all rooms are non-smoking. This query uses the [full Lucene query language](query-lucene-syntax).

```
$filter=search.ismatch('"hotel airport"~5', 'Description', 'full', 'any') and not Rooms/any(room: room/SmokingAllowed)
```


Find documents that have a word that starts with the letters "lux" in the Description field. This query uses [prefix search](query-simple-syntax#prefix-queries) in combination with `search.ismatch`

.

```
$filter=search.ismatch('lux*', 'Description')
```
