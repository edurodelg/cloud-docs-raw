---
merged_at: 2026-01-25T02:11:58.351267
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-query-odata-orderby.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-odata-orderby -->

# OData $orderby syntax in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, the **$orderby** parameter specifies a custom sort order for search results. This article describes the OData syntax of **$orderby** and provides examples.

Field path construction and constants are described in the [OData language overview in Azure AI Search](query-odata-filter-orderby-syntax). For more information about sorting behaviors, see [Ordering results](search-pagination-page-layout#ordering-results).

## Syntax

The **$orderby** parameter accepts a comma-separated list of up to 32 **order-by clauses**. The syntax of an order-by clause is described by the following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)):

```
order_by_clause ::= (field_path | sortable_function) ('asc' | 'desc')?
sortable_function ::= geo_distance_call | 'search.score()'
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

Each clause has sort criteria, optionally followed by a sort direction (`asc`

for ascending or `desc`

for descending). If you don't specify a direction, the default is ascending. If there are null values in the field, null values appear first if the sort is `asc`

and last if the sort is `desc`

.

The sort criteria can either be the path of a `sortable`

field or a call to either the [ geo.distance](search-query-odata-geo-spatial-functions) or the

[functions.](search-query-odata-search-score-function)

`search.score`

For string fields, the default [ASCII sort order](https://en.wikipedia.org/wiki/ASCII#Printable_characters) and default [Unicode sort order](https://en.wikipedia.org/wiki/List_of_Unicode_characters) will be used. By default, sorting is case sensitive but you can use a [normalizer](search-normalizers) to preprocess the text before sorting to change this behavior. You can also use an `asciifolding`

normalizer to convert non-ASCII characters to their ASCII equivalent, if one exists.

If multiple documents have the same sort criteria and the `search.score`

function isn't used (for example, if you sort by a numeric `Rating`

field and three documents all have a rating of 4), ties will be broken by document score in descending order. When document scores are the same (for example, when there's no full-text search query specified in the request), then the relative ordering of the tied documents is indeterminate.

You can specify multiple sort criteria. The order of expressions determines the final sort order. For example, to sort descending by score, followed by Rating, the syntax would be `$orderby=search.score() desc,Rating desc`

.

The syntax for `geo.distance`

in **$orderby** is the same as it is in **$filter**. When using `geo.distance`

in **$orderby**, the field to which it applies must be of type `Edm.GeographyPoint`

and it must also be `sortable`

.

The syntax for `search.score`

in **$orderby** is `search.score()`

. The function `search.score`

doesn't take any parameters.

## Examples

Sort hotels ascending by base rate:

```
$orderby=BaseRate asc
```


Sort hotels descending by rating, then ascending by base rate (remember that ascending is the default):

```
$orderby=Rating desc,BaseRate
```


Sort hotels descending by rating, then ascending by distance from the given coordinates:

```
$orderby=Rating desc,geo.distance(Location, geography'POINT(-122.131577 47.678581)') asc
```


Sort hotels in descending order by search.score and rating, and then in ascending order by distance from the given coordinates. Between two hotels with identical relevance scores and ratings, the closest one is listed first:

```
$orderby=search.score() desc,Rating desc,geo.distance(Location, geography'POINT(-122.131577 47.678581)') asc
```


---

<!-- DOCUMENTO FUSIONADO: tutorial-csharp-create-load-index.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/tutorial-csharp-create-load-index -->

# Step 2 - Create and load the search index

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Continue to build your search-enabled website by following these steps:

- Create a new index
- Load data

The program uses [Azure.Search.Documents](https://www.nuget.org/packages/Azure.Search.Documents/) in the Azure SDK for .NET:

Before you start, make sure you have room on your search service for a new index. The free tier limit is three indexes. The Basic tier limit is 15.

## Prepare the bulk import script for Search

In Visual Studio Code, open the

`Program.cs`

file in the subdirectory,`azure-search-static-web-app/bulk-insert`

, replace the following variables with your own values to authenticate with the Azure Search SDK.- YOUR-SEARCH-SERVICE-NAME (not the full URL)
- YOUR-SEARCH-ADMIN-API-KEY (see
[Find API keys](search-security-api-keys#find-existing-keys))

`using Azure; using Azure.Search.Documents; using Azure.Search.Documents.Indexes; using Azure.Search.Documents.Indexes.Models; using AzureSearch.BulkInsert; using ServiceStack; const string BOOKS_URL = "https://raw.githubusercontent.com/Azure-Samples/azure-search-sample-data/main/good-books/books.csv"; const string SEARCH_ENDPOINT = "https://YOUR-SEARCH-RESOURCE-NAME.search.windows.net"; const string SEARCH_KEY = "YOUR-SEARCH-ADMIN-KEY"; const string SEARCH_INDEX_NAME = "good-books"; Uri searchEndpointUri = new(SEARCH_ENDPOINT); SearchClient client = new( searchEndpointUri, SEARCH_INDEX_NAME, new AzureKeyCredential(SEARCH_KEY)); SearchIndexClient clientIndex = new( searchEndpointUri, new AzureKeyCredential(SEARCH_KEY)); await CreateIndexAsync(clientIndex); await BulkInsertAsync(client); static async Task CreateIndexAsync(SearchIndexClient clientIndex) { Console.WriteLine("Creating (or updating) search index"); SearchIndex index = new BookSearchIndex(SEARCH_INDEX_NAME); var result = await clientIndex.CreateOrUpdateIndexAsync(index); Console.WriteLine(result); } static async Task BulkInsertAsync(SearchClient client) { Console.WriteLine("Download data file"); using HttpClient httpClient = new(); var csv = await httpClient.GetStringAsync(BOOKS_URL); Console.WriteLine("Reading and parsing raw CSV data"); var books = csv.ReplaceFirst("book_id", "id").FromCsv<List<BookModel>>(); Console.WriteLine("Uploading bulk book data"); _ = await client.UploadDocumentsAsync(books); Console.WriteLine("Finished bulk inserting book data"); }`

Open an integrated terminal in Visual Studio Code for the project directory's subdirectory,

`azure-search-static-web-app/bulk-insert`

.Run the following command to install the dependencies.

`dotnet restore`


## Run the bulk import script for Search

Still in the same subdirectory (

`azure-search-static-web-app/bulk-insert`

), run the program:`dotnet run`

As the code runs, the console displays progress. You should see the following output.

`Creating (or updating) search index Status: 201, Value: Azure.Search.Documents.Indexes.Models.SearchIndex Download data file Reading and parsing raw CSV data Uploading bulk book data Finished bulk inserting book data`


## Review the new search index

Once the upload completes, the search index is ready to use. Review your new index in Azure portal.

In Azure portal,

[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).On the left, select

**Search Management > Indexes**, and then select the good-books index.By default, the index opens in the

**Search Explorer**tab. Select**Search**to return documents from the index.

## Rollback bulk import file changes

Use the following git command in the Visual Studio Code integrated terminal at the `bulk-insert`

directory to roll back the changes to the `Program.cs`

file. They aren't needed to continue the tutorial and you shouldn't save or push your API keys or search service name to your repo.

```
git checkout .
```
