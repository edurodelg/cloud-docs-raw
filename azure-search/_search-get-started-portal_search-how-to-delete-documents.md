---
merged_at: 2026-01-25T03:18:14.060874
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-get-started-portal.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-get-started-portal -->

# Quickstart: Full-text search in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The **Import data (new)** wizard now supports keyword search, which was previously only available in the **Import data** wizard. We recommend the new wizard for an improved search experience. For more information about how we're consolidating the wizards, see [Import data wizards in the Azure portal](search-import-data-portal).

In this quickstart, you use the **Import data (new)** wizard and sample data about fictitious hotels to get started with [full-text search](search-lucene-query-architecture), also known as keyword search. The wizard requires no code to create an index, helping you write interesting queries within minutes.

The wizard creates multiple objects on your search service, including a searchable index, an indexer, and a data source connection for automated data retrieval. At the end of this quickstart, you review each object.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An

[Azure AI Search service](search-create-service-portal). You can use the Free tier for this quickstart.An

[Azure Storage account](/en-us/azure/storage/common/storage-account-create). Use Azure Blob Storage or Azure Data Lake Storage Gen2 (storage account with a hierarchical namespace) on a standard performance (general-purpose v2) account. To avoid bandwidth charges, use the same region as Azure AI Search.Familiarity with the wizard. See

[Import data wizards in the Azure portal](search-import-data-portal).

### Check for network access

For this quickstart, all of the preceding resources must have public access enabled so that the Azure portal nodes can access them. Otherwise, the wizard fails. After the wizard runs, you can enable firewalls and private endpoints on the integration components for security. For more information, see [Secure connections in the import wizards](search-import-data-portal#secure-connections).

### Check for space

Many customers start with a free search service, which is limited to three indexes, three indexers, and three data sources. This quickstart creates one of each, so before you begin, make sure you have room for extra objects.

On the **Overview** page, select **Usage** to see how many indexes, indexers, and data sources you currently have.

## Prepare sample data

This quickstart uses a JSON document that contains metadata for 50 fictitious hotels, but you can also use your own files.

To prepare the sample data for this quickstart:

Download the

`HotelsData_toAzureBlobs.json`

file from the[azure-search-sample-data](https://github.com/Azure-Samples/azure-search-sample-data/blob/main/hotels/HotelsData_toAzureBlobs.json)repo.Sign in to the

[Azure portal](https://portal.azure.com/)and select your Azure Storage account.From the left pane, select

**Data storage**>**Containers**.Create a container named

**hotels-sample**.Upload the

`HotelsData_toAzureBlobs.json`

file to the container.

## Run the wizard

The wizard walks you through several configuration steps. This section covers each step in sequence.

### Start the wizard

To start the wizard for this quickstart:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.On the

**Overview**page, select**Import data (new)**.Select your data source:

**Azure Blob Storage**or**Azure Data Lake Storage Gen2**.Select

**Keyword search**.

### Connect to a data source

Azure AI Search requires a connection to a data source for content ingestion and indexing. In this case, the data source is your Azure Storage account.

To connect to the sample data:

On the

**Connect to your data**page, select your Azure subscription.Select your storage account, and then select the

**hotels-sample**container.Select

**JSON array**for the parsing mode.Select

**Next**.

### Skip AI enrichment

The wizard supports skillset creation and [AI enrichment](cognitive-search-concept-intro) during indexing, which are beyond the scope of this quickstart. Skip this step by selecting **Next**.

Tip

For a similar walkthrough that focuses on AI enrichment, see [Quickstart: Create a skillset in the Azure portal](search-get-started-skillset).

### Configure the index

Based on the structure and content of the sample hotel data, the wizard infers a schema for your search index.

To configure the index:

For each of the following fields, select

**Configure field**, and then set the respective attributes.Fields Attributes `HotelId`

Key, Retrievable, Filterable, Sortable, Searchable `HotelName`

,`Category`

Retrievable, Filterable, Sortable, Searchable `Description`

,`Description_fr`

Retrievable, Searchable `Tags`

Retrievable, Filterable, Searchable `ParkingIncluded`

,`IsDeleted`

Retrievable, Filterable, Facetable `LastRenovationDate`

,`Rating`

,`Location`

Retrievable, Filterable, Sortable `Address.StreetAddress`

,`Rooms.Description`

,`Rooms.Description_fr`

Retrievable, Searchable `Address.City`

,`Address.StateProvince`

,`Address.PostalCode`

,`Address.Country`

Retrievable, Filterable, Facetable, Searchable, Sortable `Rooms.Type`

,`Rooms.BedOptions`

,`Rooms.Tags`

Retrievable, Filterable, Facetable, Searchable `Rooms.BaseRate`

,`Rooms.SleepsCount`

,`Rooms.SmokingAllowed`

Retrievable, Filterable, Facetable Select

**Next**.

At a minimum, the index requires a name and a collection of fields. The wizard scans for unique string fields and marks one as the document key, which uniquely identifies each document in the index.

Each field has a name, [data type](/en-us/rest/api/searchservice/supported-data-types), and attributes that control how the field is used in the index. You can enable or disable the following attributes:

| Attribute | Description | Applicable data types |
|---|---|---|
| Retrievable | Fields returned in a query response. | Strings and integers |
| Filterable | Fields that accept a filter expression. | Strings and integers |
| Sortable | Fields that accept an orderby expression. | Strings and integers |
| Facetable | Fields used in a faceted navigation structure. | Strings and integers |
| Searchable | Fields used in full-text search. Strings are searchable, but numeric and Boolean fields are often marked as not searchable. | Strings |

Attributes affect storage in different ways. For example, filterable fields consume extra storage, while retrievable fields don't. For more information about attributes and data types, see [Configure field definitions](/en-us/azure/search/search-how-to-create-search-index#configure-field-definitions).

If you want autocomplete or suggested queries, specify **Suggesters**.

### Skip advanced settings

The wizard offers advanced settings for semantic ranking and index scheduling, which are beyond the scope of this quickstart. Skip this step by selecting **Next**.

### Finish the wizard

The last step is to review your configuration and create the index, indexer, and data source on your search service. The indexer automates the process of extracting content from your data source and loading it into the index, enabling keyword search.

To finish the wizard:

Change the object name prefix to

**hotels-sample**.Review the object configurations.

AI enrichment, semantic ranker, and indexer scheduling are either disabled or set to their default values because you skipped their wizard steps.

Select

**Create**to simultaneously create the objects and run the indexer.

## Monitor indexer progress

You can monitor the creation of the indexer and index in the Azure portal. The **Overview** page provides links to the objects created on your search service.

To monitor the progress of the indexer:

From the left pane, select

**Indexers**.Find

**hotels-sample-indexer**in the list.It can take a few minutes for the results to update. You should see the newly created indexer with a status of

**In progress**or**Success**. The list also shows the number of documents indexed.

## Check search index results

From the left pane, select

**Indexes**.Select

**hotels-sample-index**. If the index has zero documents or storage, wait for the Azure portal to refresh.Select the

**Fields**tab to view the index schema.Check which fields are

**Filterable**or**Sortable**so that you know what queries to write.

## Add or change fields

On the **Fields** tab, you can create a field by selecting **Add field** and specifying a name, [supported data type](/en-us/rest/api/searchservice/supported-data-types), and attributes.

Changing existing fields is more difficult. Existing fields have a physical representation in the search index, so they aren't modifiable, not even in code. To fundamentally change an existing field, you must create a new field to replace the original. You can add other constructs, such as scoring profiles and CORS options, to an index at any time.

Review the index definition options to understand what you can and can't edit during index design. If an option appears dimmed, you can't modify or delete it.

## Query with Search explorer

You now have a search index that can be queried using [ Search explorer](search-explorer), which sends REST calls that conform to

[Documents - Search Post (REST API)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&preserve-view=true). This tool supports

[simple query syntax](/en-us/rest/api/searchservice/simple-query-syntax-in-azure-search)and

[full Lucene query syntax](/en-us/rest/api/searchservice/lucene-query-syntax-in-azure-search)for keyword search.

To query your search index:

On the

**Search explorer**tab, enter text to search on.To jump to nonvisible areas of the output, use the mini map.

To specify syntax, switch to the JSON view.


## Example queries for hotels-sample index

The following examples assume the JSON view and the latest preview REST API version.

Tip

The JSON view supports intellisense for parameter name completion. Place your cursor inside the JSON view and enter a space character to see a list of all query parameters. You can also enter a letter, like `s`

, to see only the query parameters that begin with that letter.

Intellisense doesn't exclude invalid parameters, so use your best judgment.

### Filter examples

Parking, tags, renovation date, rating, and location are filterable.

```
{
"search": "beach OR spa",
"select": "HotelId, HotelName, Description, Rating",
"count": true,
"top": 10,
"filter": "Rating gt 4"
}
```


Boolean filters assume "true" by default.

```
{
"search": "beach OR spa",
"select": "HotelId, HotelName, Description, Rating",
"count": true,
"top": 10,
"filter": "ParkingIncluded"
}
```


Geospatial search is filter based. The `geo.distance`

function filters all results for positional data based on the specified `Location`

and `geography'POINT`

coordinates. The query seeks hotels within five kilometers of the latitude and longitude coordinates `-122.12 47.67`

, which is "Redmond, Washington, USA." The query displays the total number of matches `&$count=true`

with the hotel names and address locations.

```
{
"search": "*",
"select": "HotelName, Address/City, Address/StateProvince",
"count": true,
"top": 10,
"filter": "geo.distance(Location, geography'POINT(-122.12 47.67)') le 5"
}
```


### Full Lucene syntax examples

The default syntax is [simple syntax](query-simple-syntax), but if you want fuzzy search, term boosting, or regular expressions, specify the [full syntax](query-lucene-syntax).

```
{
"queryType": "full",
"search": "seatle~",
"select": "HotelId, HotelName,Address/City, Address/StateProvince",
"count": true
}
```


Misspelled query terms, like `seatle`

instead of `Seattle`

, don't return matches in a typical search. The `queryType=full`

parameter invokes the full Lucene query parser, which supports the tilde (`~`

) operand. When you use these parameters, the query performs a fuzzy search for the specified keyword and matches on terms that are similar but not an exact match.

Take a minute to try these example queries on your index. For more information, see [Querying in Azure AI Search](search-query-overview).

## Clean up resources

When you work in your own subscription, it's a good idea at the end of a project to identify whether you still need the resources you created. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.

In the Azure portal, you can find and manage resources by selecting **All resources** or **Resource groups** from the left pane.

Note

If you're using a free search service, remember that the limit is three indexes, three indexers, and three data sources. You can delete individual objects in the Azure portal to stay under the limit.

## Next step

Try an Azure portal wizard to generate a ready-to-use web app that runs in a browser. Use this wizard on the small index you created in this quickstart, or use [sample data](https://github.com/Azure-Samples/azure-search-sample-data) for a richer search experience.


---

<!-- DOCUMENTO FUSIONADO: search-how-to-delete-documents.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-delete-documents -->

# Delete documents in a search index

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to delete whole documents from a search index on Azure AI Search using REST APIs or Azure SDKs. It covers these tasks:

- Understand when manual deletion is required
- Identify specific documents to delete
- Get document counts and storage metrics
- Delete a single or orphaned document
- Delete documents in bulk
- Confirm deletion

Tip

For a quick single-document delete, skip to [Delete a single document](#delete-a-single-document).

## Prerequisites

An Azure AI Search service (any tier).

[Create a service](search-create-service-portal)or[find an existing one](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).An existing search index with documents to delete. This article assumes you already

[created an index](search-how-to-create-search-index)and[loaded documents](search-how-to-load-search-index).Permissions to delete documents:

**Key-based authentication**: An[admin API key](search-security-api-keys)for your search service.**Role-based authentication**:[Search Index Data Contributor](search-security-rbac)role or the`Microsoft.Search/searchServices/indexes/documents/delete`

permission.

For SDK development, install the Azure Search client library:

- Python:
[azure-search-documents](https://pypi.org/project/azure-search-documents/) - .NET:
[Azure.Search.Documents](https://www.nuget.org/packages/Azure.Search.Documents/) - JavaScript:
[@azure/search-documents](https://www.npmjs.com/package/@azure/search-documents) - Java:
[azure-search-documents](https://central.sonatype.com/artifact/com.azure/azure-search-documents)

- Python:

## Understand when manual deletion is required

Manual document deletion is necessary when you use the [push mode approach to indexing](search-what-is-data-import#pushing-data-to-an-index), where application code handles data import and drives indexing.

You also need manual document deletion if you use [Logic Apps to load an index (preview)](search-how-to-index-logic-apps#limitations).

You might also need manual document deletion in indexer-driven workloads if search documents become "orphaned" from source documents. An important benefit of indexers is automated content retrieval and synchronization via the change and deletion detection features of the target data source. All of the supported data sources provide some level of detection. But in some cases, synchronized deletion is predicated on a soft-delete strategy where you flag a source document (or record) for deletion, run the indexer to delete the indexed content, and only after the index is updated do you physically delete the source content. If source content is deleted first, you have *orphan documents* in the search index. You must manually delete orphan documents in your index to re-establish parity between source and indexed content.

The following links provide more information about change and deletion detection for each data source in indexer-driven workloads.

[Azure Storage](search-how-to-index-azure-blob-changed-deleted)[Azure SQL](search-how-to-index-sql-database#indexing-new-changed-and-deleted-rows)[Azure Cosmos DB](search-how-to-index-cosmosdb-sql#indexing-deleted-documents)[Azure Database for MySQL (preview)](search-how-to-index-mysql#indexing-deleted-rows)[SharePoint indexer](search-how-to-index-sharepoint-online)[OneLake indexer](search-how-to-index-onelake-files#supported-tasks)

## Identify specific documents for deletion

All documents are uniquely identified by a [document key](search-how-to-create-search-index#document-keys) in a search index. To delete a document, you must identify which field is the document key and provide the key on the deletion request.

In the Azure portal, you can view the fields of each index. Document keys are string fields and are denoted with a key icon to make them easier to spot.

### Find the document key

Once you know which field is the document key, you can get the key value by running a query that returns the key field in the search results.

In this example, the search string is used to find the document in the index, and the select statement determines what fields are in the results. The "HotelId" is the document key in this example.

```
POST https://[service name].search.windows.net/indexes/hotels-sample-index/docs/search?api-version=2025-09-01
{
"search": "this query has terms that pertain to the document I want to delete",
"select": "HotelName, HotelId",
"count": true
}
```


Results for this keyword search are the top 50 by default. If the document you want to delete satisfies the search criteria, you should see it (and it's key) in the results. Make sure the query includes a descriptive field that helps you confirm you have the correct document.

```
{
"@odata.count": 50,
"value": [
{
"@search.score": 4.5116634,
"HotelId": "18",
"HotelName": "Ocean Water Resort & Spa"
}
...
]
}
```


A simple string is straightforward, but if the index uses a base-64 encoded field, or if search documents were generated from a `parsingMode`

setting, you might be working with values that you aren't familiar with. If you're working with chunked documents create by an indexer, the document key is often a generated "chunked_id" composed of a long sequence of numbers and letters.

## Look up a specific document

Now that you have the document key, run a [look up query](/en-us/rest/api/searchservice/documents/get) that retrieves the entire document. If the document is a chunk, you should see the ID of the parent document. The document key is included as a query parameter.

The first example returns the hotel having a document key value of `18`

.

```
GET https://[service name].search.windows.net/indexes/hotels-sample-index/docs('18')&api-version=2025-09-01
```


The second example returns a chunk document. The "chunk_id" is the document key.

```
GET https://[service name].search.windows.net/indexes/chunking-example-index/docs('aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb')&api-version=2025-09-01
```


The response from the second example includes all fields, which you should review to ensure you know what you're deleting. Fields that include parent information are useful if you need to manually reindex a single parent document into constituent chunked documents in the search index.

```
{
"chunk_id": "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb",
"parent_id": "bbbbbbbb-1111-2222-3333-cccccccccccc",
"chunk": "Unpopulated Slopes of an Active Volcano\u2014Naples, Italy ... 90\n\nDazzling Coastlines\u2014Italy ... .92\n\nLiving on Fertile Land\u2014Nile River, Egypt ... 94\n\n\n\n vii",
"title": "earth_at_night_508.pdf",
"text_vector": [ <omitted> ]
}
```


Tip

Use a [REST client](search-get-started-text?tabs=keyless,windows&pivots=rest#query-the-index), an Azure SDK client library, or a [command line tool](search-get-started-text?tabs=keyless,windows&pivots=powershell#query-the-index) to run a lookup query. The Azure portal doesn't support GET requests for a query.

## Get document counts and storage metrics

Before you delete documents, get initial metrics for the index document count and storage so that you can confirm deletion later.

You can get document counts and index storage using:

- The Azure portal, under
**Search management**>**Indexes**. - The
[Indexes - Get Statistics](/en-us/rest/api/searchservice/indexes/get-statistics)REST API

Here's an example response:

```
{
"documentCount": 12,
"storageSize": 123456,
"vectorIndexSize": 123456
}
```


## Delete a single document

Use the

[Documents - Index](/en-us/rest/api/searchservice/documents)REST API with a delete`@search.action`

to remove it from the search index.Formulate a POST call specifying the index name and the

`docs/index`

endpoint.Make sure the body of the request includes the key of the document you want to delete.

`POST https://[service name].search.windows.net/indexes/hotels-sample-index/docs/index?api-version=2025-09-01 Content-Type: application/json api-key: [admin key] { "value": [ { "@search.action": "delete", "id": "18" } ] }`

Send the request.

The following table explains the various per-document

[status codes](/en-us/rest/api/searchservice/http-status-codes)that can be returned in the response. Some status codes indicate problems with the request itself, while others indicate temporary error conditions. The latter you should retry after a delay.Status code Meaning Retryable Notes 200 Document was successfully deleted. n/a Delete operations are [idempotent](https://en.wikipedia.org/wiki/Idempotence). That is, even if a document key doesn't exist in the index, attempting a delete operation with that key results in a 200 status code.400 There was an error in the document that prevented it from being deleted. No The error message in the response provides details. 422 The index is temporarily unavailable because it was updated with the 'allowIndexDowntime' flag set to 'true'. Yes Wait for index to become available. 503 Your search service is temporarily unavailable, possibly due to heavy load. Yes Your code should wait before retrying in this case or you risk prolonging the service unavailability. Note

If your client code frequently encounters a 207 response, one possible reason is that the system is under load. You can confirm this by checking the

`statusCode`

property for 503. If so, we recommend throttling indexing requests. Otherwise, if indexing traffic doesn't subside, the system could start rejecting all requests with 503 errors.You can resend the

[Lookup query](/en-us/rest/api/searchservice/documents/get)to confirm the deletion. You should get a 404 document not found message.`GET https://[service name].search.windows.net/indexes/hotel-sample-index/docs/18?api-version=2025-09-01`


**Reference:** [Documents - Index](/en-us/rest/api/searchservice/documents)

A successful delete request returns HTTP 200 (OK). The response body contains status for each document:

```
{
"value": [
{ "key": "18", "status": true, "statusCode": 200 }
]
}
```


## Delete documents in bulk

Use the

[Documents - Index](/en-us/rest/api/searchservice/documents)REST API with a delete`@search.action`

to remove it from the search index. Formulate a POST call specifying the index name and the`docs/index`

endpoint.Make sure the body of the request includes the keys of all of the documents you want to delete.

`POST https://[service name].search.windows.net/indexes/hotels-sample-index/docs/index?api-version=2025-09-01 Content-Type: application/json api-key: [admin key] { "value": [ { "@search.action": "delete", "id": "doc1" }, { "@search.action": "delete", "id": "doc2" } ] }`


**Batch limits**: It is recommended to limit batches to 1,000 documents or roughly 16 MB per request to ensure optimal performance.**Idempotency**: Deletion is idempotent; if you attempt to delete a document ID that does not exist, the API will still return a 200 OK status.**Latency**: Documents are not always removed instantly from storage. A background process performs the physical deletion every few minutes.**Vector storage**: Deleting documents does not immediately free up vector storage quotas. It takes several minutes for physical deletion. For immediate reclamation of vector space, you may need to drop and rebuild the index.

**Reference:** [Documents - Index](/en-us/rest/api/searchservice/documents)

## Verify document deletion

After deleting documents, verify the deletion was successful.

- In the Azure portal, open the search service
**Overview**page. - Select
**Search management**>**Indexes**. - Check the
**Document count**column for your index. - Wait a few minutes and refresh if the count hasn't changed (deletion is asynchronous).

Deleting a document doesn't immediately free up space in the index. Every few minutes, a background process performs the physical deletion. Whether you use the Azure portal or the Get Statistics API to return index statistics, you can expect a small delay before the deletion is reflected in the Azure portal and API metrics.

## Troubleshoot document deletion

The following table lists common issues when deleting documents and how to resolve them.

| Issue | Cause | Resolution |
|---|---|---|
| Document count unchanged | Deletion is asynchronous. Background process runs every few minutes. | Wait 2-3 minutes and refresh. Check index statistics again. |
| 400 Bad Request | Invalid document key or malformed request body. | Verify the document key field name matches your index schema. Check JSON syntax. |
| 403 Forbidden | Insufficient permissions. | Use an admin API key or ensure your identity has Search Index Data Contributor role. |
| 404 Not Found on index | Index name is incorrect or doesn't exist. | Verify the index name in your request URL. |
| Storage not reclaimed | Physical deletion happens asynchronously in background. | Wait several minutes. For immediate vector storage reclamation, drop and rebuild the index. |
| Orphaned documents remain | Source documents deleted before indexer ran with deletion detection. | Manually delete orphaned documents using their document keys. |
