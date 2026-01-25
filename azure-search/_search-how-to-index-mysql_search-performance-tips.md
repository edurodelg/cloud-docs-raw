---
merged_at: 2026-01-25T02:11:58.468757
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-how-to-index-mysql.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-index-mysql -->

# Index data from Azure Database for MySQL Flexible Server

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

MySQL support is currently in public preview under [Supplemental Terms of Use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). We recommend the latest preview API. There is currently no portal support.

In this article, learn how to configure an [ indexer](search-indexer-overview) that imports content from Azure Database for MySQL and makes it searchable in Azure AI Search. Inputs to the indexer are rows from a single table or view. Output is a search index with searchable content in individual fields.

This article supplements [ Create an indexer](search-howto-create-indexers) with information that's specific to indexing from Azure Database for MySQL Flexible Server. It uses the REST APIs to demonstrate a three-part workflow common to all indexers: create a data source, create an index, create an indexer. Data extraction occurs when you submit the Create Indexer request.

When configured to include a high water mark and soft deletion, the indexer takes all changes, uploads, and deletes for your MySQL database. It reflects these changes in your search index. Data extraction occurs when you submit the Create Indexer request.

## Prerequisites

[Register for the preview](https://aka.ms/azure-cognitive-search/indexer-preview)to provide scenario feedback. You can access the feature automatically after form submission.[Azure Database for MySQL Flexible Server](/en-us/azure/mysql/flexible-server/overview)and sample data. Data must reside in a table or view. A primary key is required. If you're using a view, it must have a[high water mark column](#DataChangeDetectionPolicy).Read permissions. A

*full access*connection string includes a key that grants access to the content, but if you're using Azure roles, make sure the[search service managed identity](search-how-to-managed-identities)has**Reader**permissions on MySQL.A

[REST client](search-get-started-text)to create the data source, index, and indexer.You can also use the

[Azure SDK for .NET](/en-us/dotnet/api/azure.search.documents.indexes.models.searchindexerdatasourcetype.mysql). You can't use the Azure portal for indexer creation, but you can manage indexers and data sources once they're created.

## Preview limitations

Currently, change tracking and deletion detection aren't working if the date or timestamp is uniform for all rows. This limitation is a known issue to be addressed in an update to the preview. Until this issue is addressed, don’t add a skillset to the MySQL indexer.

The preview doesn’t support geometry types and blobs.

As noted, there’s no portal support for indexer creation, but a MySQL indexer and data source can be managed in the Azure portal once they exist. For example, you can edit the definitions, and reset, run, or schedule the indexer.

## Define the data source

The data source definition specifies the data to index, credentials, and policies for identifying changes in the data. The data source is defined as an independent resource so that it can be used by multiple indexers.

[Create or Update Data Source](/en-us/rest/api/searchservice/data-sources/create?view=rest-searchservice-2025-11-01-preview&preserve-view=true) specifies the definition. Be sure to use a preview REST API when creating the data source.

```
{
"name" : "hotel-mysql-ds",
"description" : "[Description of MySQL data source]",
"type" : "mysql",
"credentials" : {
"connectionString" :
"Server=[MySQLServerName].MySQL.database.azure.com; Port=3306; Database=[DatabaseName]; Uid=[UserName]; Pwd=[Password]; SslMode=Preferred;"
},
"container" : {
"name" : "[TableName]"
},
"dataChangeDetectionPolicy" : {
"@odata.type": "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
"highWaterMarkColumnName": "[HighWaterMarkColumn]"
}
}
```


**Key points**:

Set

`type`

to`"mysql"`

(required).Set

`credentials`

to an ADO.NET connection string. You can find connection strings in Azure portal, on the**Connection strings**page for MySQL.Set

`container`

to the name of the table.Set

if data is volatile and you want the indexer to pick up just the new and updated items on subsequent runs.`dataChangeDetectionPolicy`

Set

if you want to remove search documents from a search index when the source item is deleted.`dataDeletionDetectionPolicy`


Note

For the container name property, the value is restricted to only allow letters, numbers, underscores (_), dots (.), single dashes (-), and square brackets ([])

## Create an index

[Create or Update Index](/en-us/rest/api/searchservice/indexes/create?view=rest-searchservice-2025-11-01-preview&preserve-view=true) specifies the index schema:

```
{
"name" : "hotels-mysql-ix",
"fields": [
{ "name": "ID", "type": "Edm.String", "key": true, "searchable": false },
{ "name": "HotelName", "type": "Edm.String", "searchable": true, "filterable": false },
{ "name": "Category", "type": "Edm.String", "searchable": false, "filterable": true, "sortable": true },
{ "name": "City", "type": "Edm.String", "searchable": false, "filterable": true, "sortable": true },
{ "name": "Description", "type": "Edm.String", "searchable": false, "filterable": false, "sortable": false }
]
}
```


If the primary key in the source table matches the document key (in this case, "ID"), the indexer imports the primary key as the document key.

### Mapping data types

The following table maps the MySQL database to Azure AI Search equivalents. For more information, see [Supported data types (Azure AI Search)](/en-us/rest/api/searchservice/supported-data-types).

Note

The preview does not support geometry types and blobs.

| MySQL data types | Azure AI Search field types |
|---|---|
`bool` , `boolean` |
Edm.Boolean, Edm.String |
`tinyint` , `smallint` , `mediumint` , `int` , `integer` , `year` |
Edm.Int32, Edm.Int64, Edm.String |
`bigint` |
Edm.Int64, Edm.String |
`float` , `double` , `real` |
Edm.Double, Edm.String |
`date` , `datetime` , `timestamp` |
Edm.DateTimeOffset, Edm.String |
`char` , `varchar` , `tinytext` , `mediumtext` , `text` , `longtext` , `enum` , `set` , `time` |
Edm.String |
| unsigned numerical data, serial, decimal, dec, bit, blob, binary, geometry | N/A |

## Configure and run the MySQL indexer

Once the index and data source have been created, you're ready to create the indexer. Indexer configuration specifies the inputs, parameters, and properties controlling run time behaviors.

[Create or update an indexer](/en-us/rest/api/searchservice/indexers/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) by giving it a name and referencing the data source and target index:

```
{
"name" : "hotels-mysql-idxr",
"dataSourceName" : "hotels-mysql-ds",
"targetIndexName" : "hotels-mysql-ix",
"disabled": null,
"schedule": null,
"parameters": {
"batchSize": null,
"maxFailedItems": null,
"maxFailedItemsPerBatch": null,
"base64EncodeKeys": null,
"configuration": { }
},
"fieldMappings" : [ ],
"encryptionKey": null
}
```


**Key points**:

[Specify field mappings](search-indexer-field-mappings)if there are differences in field name or type, or if you need multiple versions of a source field in the search index.An indexer runs automatically when it's created. You can prevent it from running by setting

`disabled`

to`true`

. To control indexer execution,[run an indexer on demand](search-howto-run-reset-indexers)or[put it on a schedule](search-howto-schedule-indexers).

## Check indexer status

Send a [Get Indexer Status](/en-us/rest/api/searchservice/indexers/get-status?view=rest-searchservice-2025-11-01-preview&preserve-view=true) request to monitor indexer execution:

```
GET https://myservice.search.windows.net/indexers/myindexer/status?api-version=2025-11-01-preview
Content-Type: application/json
api-key: [admin key]
```


The response includes status and the number of items processed. It should look similar to the following example:

```
{
"status":"running",
"lastResult": {
"status":"success",
"errorMessage":null,
"startTime":"2024-02-21T00:23:24.957Z",
"endTime":"2024-02-21T00:36:47.752Z",
"errors":[],
"itemsProcessed":1599501,
"itemsFailed":0,
"initialTrackingState":null,
"finalTrackingState":null
},
"executionHistory":
[
{
"status":"success",
"errorMessage":null,
"startTime":"2024-02-21T00:23:24.957Z",
"endTime":"2024-02-21T00:36:47.752Z",
"errors":[],
"itemsProcessed":1599501,
"itemsFailed":0,
"initialTrackingState":null,
"finalTrackingState":null
},
... earlier history items
]
}
```


Execution history contains up to 50 of the most recently completed executions, which are sorted in the reverse chronological order so that the latest execution comes first.

## Indexing new and changed rows

Once an indexer has fully populated a search index, you might want subsequent indexer runs to incrementally index just the new and changed rows in your database.

To enable incremental indexing, set the `dataChangeDetectionPolicy`

property in your data source definition. This property tells the indexer which change tracking mechanism is used on your data.

For Azure Database for MySQL indexers, the only supported policy is the [ HighWaterMarkChangeDetectionPolicy](/en-us/dotnet/api/azure.search.documents.indexes.models.highwatermarkchangedetectionpolicy).

An indexer's change detection policy relies on having a *high water mark* column that captures the row version, or the date and time when a row was last updated. It's often a `DATE`

, `DATETIME`

, or `TIMESTAMP`

column at a granularity sufficient for meeting the requirements of a high water mark column.

In your MySQL database, the high water mark column must meet the following requirements:

- All data inserts must specify a value for the column.
- All updates to an item also change the value of the column.
- The value of this column increases with each insert or update.
- Queries with the following
`WHERE`

and`ORDER BY`

clauses can be executed efficiently:`WHERE [High Water Mark Column] > [Current High Water Mark Value] ORDER BY [High Water Mark Column]`


The following example shows a [data source definition](#define-the-data-source) with a change detection policy:

```
{
"name" : "[Data source name]",
"type" : "mysql",
"credentials" : { "connectionString" : "[connection string]" },
"container" : { "name" : "[table or view name]" },
"dataChangeDetectionPolicy" : {
"@odata.type" : "#Microsoft.Azure.Search.HighWaterMarkChangeDetectionPolicy",
"highWaterMarkColumnName" : "[last_updated column name]"
}
}
```


Important

If you're using a view, you must set a high water mark policy in your indexer data source.

If the source table does not have an index on the high water mark column, queries used by the MySQL indexer might time out. In particular, the `ORDER BY [High Water Mark Column]`

clause requires an index to run efficiently when the table contains many rows.

## Indexing deleted rows

When rows are deleted from the table or view, you normally want to delete those rows from the search index as well. However, if the rows are physically removed from the table, an indexer has no way to infer the presence of records that no longer exist. The solution is to use a *soft-delete* technique to logically delete rows without removing them from the table. Add a column to your table or view and mark rows as deleted using that column.

Given a column that provides deletion state, an indexer can be configured to remove any search documents for which deletion state is set to `true`

. The configuration property that supports this behavior is a data deletion detection policy, which is specified in the [data source definition](#define-the-data-source) as follows:

```
{
…,
"dataDeletionDetectionPolicy" : {
"@odata.type" : "#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy",
"softDeleteColumnName" : "[a column name]",
"softDeleteMarkerValue" : "[the value that indicates that a row is deleted]"
}
}
```


The `softDeleteMarkerValue`

must be a string. For example, if you have an integer column where deleted rows are marked with the value 1, use `"1"`

. If you have a `BIT`

column where deleted rows are marked with the Boolean true value, use the string literal `True`

or `true`

(the case doesn't matter).

## Next steps

You can now [run the indexer](search-howto-run-reset-indexers), [monitor status](search-monitor-indexers), or [schedule indexer execution](search-howto-schedule-indexers). The following articles apply to indexers that pull content from Azure MySQL:


---

<!-- DOCUMENTO FUSIONADO: search-performance-tips.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-performance-tips -->

# Tips for better performance in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article is a collection of tips and best practices for boosting query and indexing performance for keyword search. Knowing which factors are most likely to affect search performance can help you avoid inefficiencies and get the most out of your search service. Some key factors include:

- Index composition (schema and size)
- Query design
- Service capacity (tier, and the number of replicas and partitions)

Note

Looking for strategies on high volume indexing? See [Index large data sets in Azure AI Search](search-howto-large-index).

## Index size and schema

Queries run faster on smaller indexes. This is partly a function of having fewer fields to scan, but it's also due to how the system caches content for future queries. After the first query, some content remains in memory where it's searched more efficiently. Because index size tends to grow over time, one best practice is to periodically revisit index composition, both schema and documents, to look for content reduction opportunities. However, if the index is right-sized, the only other calibration you can make is to increase capacity by [upgrading your service](search-how-to-upgrade), [adding replicas](search-capacity-planning#add-or-remove-partitions-and-replicas), or [switching to a higher pricing tier](search-capacity-planning#change-your-pricing-tier). The section "[Tip: Switch to a Standard S2 tier](#tip-switch-to-a-standard-s2-tier)" discusses the scale up versus scale out decision.

Schema complexity can also adversely affect indexing and query performance. Excessive field attribution builds in limitations and processing requirements. [Complex types](search-howto-complex-data-types) take longer to index and query. The next few sections explore each condition.

### Tip: Be selective in field attribution

A common mistake that administrators and developers make when creating a search index is selecting all available properties for the fields, as opposed to only selecting just the properties that are needed. For example, if a field doesn't need to be full text searchable, skip that field when setting the searchable attribute.


Support for filters, facets, and sorting can quadruple storage requirements. If you add suggesters, storage requirements go up even more. For an illustration on the impact of attributes on storage, see [Attributes and index size](search-what-is-an-index#index-size).

Summarized, the ramifications of over-attribution include:

Degradation of indexing performance due to the extra work required to process the content in the field, and then store it within the search inverted index (set the "searchable" attribute only on fields that contain searchable content).

Creates a larger surface that each query has to cover. All fields marked as searchable are scanned in a full text search.

Increases operational costs due to extra storage. Filtering and sorting requires additional space for storing original (non-analyzed) strings. Avoid setting filterable or sortable on fields that don't need it.

In many cases, over attribution limits the capabilities of the field. For example, if a field is facetable, filterable, and searchable, you can only store 16 KB of text within a field, whereas a searchable field can hold up to 16 MB of text.


Note

Only unnecessary attribution should be avoided. Filters and facets are often essential to the search experience, and in cases where filters are used, you frequently need sorting so that you can order the results (filters by themselves return in an unordered set).

### Tip: Consider alternatives to complex types

Complex data types are useful when data has a complicated nested structure, such as the parent-child elements found in JSON documents. The downside of complex types is the extra storage requirements and additional resources required to index the content, in comparison to non-complex data types.

In some cases, you can avoid these tradeoffs by mapping a complex data structure to a simpler field type, such as a Collection. Alternatively, you might opt for flattening a field hierarchy into individual root-level fields.


## Query design

Query composition and complexity are one of the most important factors for performance, and query optimization can drastically improve performance. When designing queries, think about the following points:

**Number of searchable fields.**Each additional searchable field results in more work for the search service. You can limit the fields being searched at query time using the "searchFields" parameter. It's best to specify only the fields that you care about to improve performance.**Amount of data being returned.**Retrieving a large amount content can make queries slower. When structuring a query, return only those fields that you need to render the results page, and then retrieve remaining fields using the[Lookup API](/en-us/rest/api/searchservice/documents/get)once a user selects a match.**Use of partial term searches.**[Partial term searches](search-query-partial-matching), such as prefix search, fuzzy search, and regular expression search, are more computationally expensive than typical keyword searches, as they require full index scans to produce results.**Number of facets.**Adding facets to queries requires aggregations for each query. Requesting a higher "count" for a facet also requires extra work by the service. In general, only add the facets that you plan to render in your app and avoid requesting a high count for facets unless necessary.**High skip values.**Setting the`$skip`

parameter to a high value (for example, in the thousands) increases search latency because the engine is retrieving and ranking a larger volume of documents for each request. For performance reasons, it's best to avoid high`$skip`

values and use other techniques instead, such as filtering, to retrieve large numbers of documents.**Limit high cardinality fields.**A*high cardinality field*refers to a facetable or filterable field that has a significant number of unique values, and as a result, consumes significant resources when computing results. For example, setting a Product ID or Description field as facetable and filterable would count as high cardinality because most of the values from document to document are unique.

### Tip: Use search functions instead overloading filter criteria

As a query uses increasingly [complex filter criteria](search-query-odata-filter#filter-size-limitations), the performance of the search query will degrade. Consider the following example that demonstrates the use of filters to trim results based on a user identity:

```
$filter= userid eq 123 or userid eq 234 or userid eq 345 or userid eq 456 or userid eq 567
```


In this case, the filter expressions are used to check whether a single field in each document is equal to one of many possible values of a user identity. You're most likely to find this pattern in applications that implement [security trimming](search-security-trimming-for-azure-search) (checking a field containing one or more principal IDs against a list of principal IDs representing the user issuing the query).

A more efficient way to execute filters that contain a large number of values is to use [ search.in function](search-query-odata-search-in-function), as shown in this example:

```
search.in(userid, '123,234,345,456,567', ',')
```


### Tip: Add partitions for slow individual queries

When query performance is slowing down in general, adding more replicas frequently solves the issue. But what if the problem is a single query that takes too long to complete? In this scenario, adding replicas won't help, but more partitions might. A partition splits data across extra computing resources. Two partitions split data in half, a third partition splits it into thirds, and so forth.

One positive side-effect of adding partitions is that slower queries sometimes perform faster due to parallel computing. We've noted parallelization on low selectivity queries, such as queries that match many documents, or facets providing counts over a large number of documents. Since significant computation is required to score the relevancy of the documents, or to count the numbers of documents, adding extra partitions helps queries complete faster.

To add partitions, use the [Azure portal](search-capacity-planning#add-or-remove-partitions-and-replicas), [PowerShell](search-manage-powershell), [Azure CLI](search-manage-azure-cli), or a management SDK.

## Service capacity

A service is overburdened when queries take too long or when the service starts dropping requests. If this happens, you can address the problem by upgrading the service or by adding capacity.

The tier of your search service and the number of replicas/partitions also have a large impact on performance. Each progressively higher tier provides faster CPUs and more memory, both of which have a positive impact on performance.

### Tip: Create a new high capacity search service

Basic and Standard services created [in supported regions](search-limits-quotas-capacity#service-limits) after April 3, 2024 have more storage per partition than older services. If you have an older service, check if you can [upgrade your service](search-how-to-upgrade) to benefit from more capacity at the same billing rate. If an upgrade isn't available, review the [tier service limits](search-limits-quotas-capacity#service-limits) to see if the same tier on a newer service gives you the necessary storage.

### Tip: Switch to a Standard S2 tier

The Standard S1 search tier is often where customers start. A common pattern for S1 services is that indexes grow over time, which requires more partitions. More partitions lead to slower response times, so more replicas are added to handle the query load. As you can imagine, the cost of running an S1 service has now progressed to levels beyond the initial configuration.

At this juncture, an important question to ask is whether it would be beneficial to [switch to a higher pricing tier](search-capacity-planning#change-your-pricing-tier), as opposed to progressively increasing the number of partitions or replicas of the current service.

Consider the following topology as an example of a service that has taken on increasing levels of capacity:

- Standard S1 tier
- Index Size: 190 GB
- Partition Count: 8 (on S1, partition size is 25 GB per partition)
- Replica Count: 2
- Total Search Units: 16 (8 partitions x 2 replicas)
- Hypothetical Retail Price: ~$4,000 USD / month (assume 250 USD x 16 search units)

Suppose the service administrator is still seeing higher latency rates and is considering adding another replica. This would change the replica count from 2 to 3 and as a result change the Search Unit count to 24 and a resulting price of $6,000 USD/month.

However, if the administrator chose to move to a Standard S2 tier the topology would look like:

- Standard S2 tier
- Index Size: 190 GB
- Partition Count: 2 (on S2, partition size is 100 GB per partition)
- Replica Count: 2
- Total Search Units: 4 (2 partitions x 2 replicas)
- Hypothetical Retail Price: ~$4,000 USD / month (1,000 USD x 4 search units)

As this hypothetical scenario illustrates, you can have configurations on lower tiers that result in similar costs as if you had opted for a higher tier in the first place. However, higher tiers come with premium storage, which makes indexing faster. Higher tiers also have much more compute power, as well as extra memory. For the same costs, you could have more powerful infrastructure backing the same index.

An important benefit of added memory is that more of the index can be cached, resulting in lower search latency, and a greater number of queries per second. With this extra power, the administrator might not need to even need to increase the replica count and could potentially pay less than by staying on the S1 service.

### Tip: Consider alternatives to regular expression queries

[Regular expression queries](query-lucene-syntax#bkmk_regex) or regex can be particularly expensive. While they can be very useful for advanced searches, execution can require a lot of processing power, especially if the regular expression is complicated or if you're searching through a large amount of data. All of these factors contribute to high search latency. As a mitigation, try to simplify the regular expression or break the complex query down into smaller, more manageable queries.

## Next steps

Review these other articles related to service performance:
