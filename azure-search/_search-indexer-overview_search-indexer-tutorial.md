---
merged_at: 2026-01-25T03:18:14.079370
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-indexer-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-indexer-overview -->

# Indexers in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An *indexer* in Azure AI Search is a crawler that extracts textual data from cloud data sources and populates a search index using field-to-field mappings between source data and a search index. This approach is sometimes referred to as a 'pull model' because the search service pulls data in without you having to write any code that adds data to an index.

Indexers also drive [skillset execution and AI enrichment](cognitive-search-concept-intro), where you can configure skills to integrate extra processing of content en route to an index. A few examples are OCR over image files, text split skill for data chunking, and calling embedding models to generate vectors for vector search.

Indexers target [supported data sources](#supported-data-sources). An indexer configuration specifies a data source (origin) and a search index (destination). Several sources, such as Azure Blob Storage, have more indexer configuration properties specific to that content type.

You can run indexers on demand or on a recurring data refresh schedule that runs as often as every five minutes. More frequent updates preclude the use of indexers, requiring that you implement a ['push model'](search-what-is-data-import) that simultaneously pushes data to both Azure AI Search and your external data source for data synchronization.

A search service runs one indexer job per search unit. If you need concurrent processing, make sure you have [sufficient replicas](/en-us/azure/search/search-capacity-planning#add-or-reduce-replicas-and-partitions). Indexers don't run in the background, so you might detect more query throttling than usual if the service is under pressure.

## Indexer scenarios and use cases

You can use an indexer as the sole means for data ingestion, or in combination with other techniques. The following table summarizes the main scenarios.

| Scenario | Strategy |
|---|---|
| Single data source | This pattern is the simplest: one data source is the sole content provider for a search index. Most supported data sources provide some form of change detection so that subsequent indexer runs pick up the difference when content is added or updated in the source. |
| Multiple data sources | An indexer specification can have only one data source, but the search index itself can accept content from multiple sources, where each indexer job brings new content from a different data provider. Each source can contribute its share of full documents, or populate selected fields in each document. For a closer look at this scenario, see
|

[Cross-region scale out of Azure AI Search](search-multi-region#data-synchronization)is a variation of this scenario. You might have copies of the same search index in different regions. To synchronize search index content, you could have multiple indexers pulling from the same data source, where each indexer targets a different search index in each region.[Parallel indexing](search-howto-large-index#parallel-indexing)of very large data sets also requires a multi-indexer strategy, where each indexer targets a subset of the data.[skillset execution and AI enrichment](cognitive-search-concept-intro). Content transforms are defined in a[skillset](cognitive-search-working-with-skillsets)that you attach to the indexer. You can use skills to[incorporate data chunking and vectorization](vector-search-integrated-vectorization).You should plan on creating one indexer for every target index and data source combination. You can have multiple indexers writing into the same index, and you can reuse the same data source for multiple indexers. However, an indexer can only consume one data source at a time, and can only write to a single index. As the following graphic illustrates, one data source provides input to one indexer, which then populates a single index:


Although you can only use one indexer at a time, resources can be used in different combinations. The main takeaway of the next illustration is to notice is that a data source can be paired with more than one indexer, and multiple indexers can write to same index.


## Supported data sources

Indexers crawl data stores on Azure and outside of Azure.

[Azure Blob Storage](search-how-to-index-azure-blob-storage)[Azure Cosmos DB](search-how-to-index-cosmosdb-sql)[Azure Data Lake Storage Gen2](search-how-to-index-azure-data-lake-storage)[Azure SQL Database](search-how-to-index-sql-database)[Azure Table Storage](search-how-to-index-azure-tables)[Azure SQL Managed Instance](search-how-to-index-sql-managed-instance)[Microsoft OneLake](search-how-to-index-onelake-files)[SQL Server on Azure Virtual Machines](search-how-to-index-sql-server)[Azure Files](search-file-storage-integration)(in preview)[Azure MySQL](search-how-to-index-mysql)(in preview)[SharePoint in Microsoft 365](search-how-to-index-sharepoint-online)(in preview)[Azure Cosmos DB for MongoDB](search-how-to-index-cosmosdb-mongodb)(in preview)[Azure Cosmos DB for Apache Gremlin](search-how-to-index-cosmosdb-gremlin)(in preview)

Azure Cosmos DB for Cassandra is not supported.

Indexers accept flattened row sets, such as a table or view, or items in a container or folder. In most cases, it creates one search document per row, record, or item.

Indexer connections to remote data sources can be made using standard Internet connections (public) or encrypted private connections when you use a shared private link. You can also set up connections to authenticate using a managed identity. For more information about secure connections, see [Indexer access to content protected by Azure network security features](search-indexer-securing-resources) and [Connect to a data source using a managed identity](search-how-to-managed-identities).

## Stages of indexing

On an initial run, when the index is empty, an indexer will read in all of the data provided in the table or container. On subsequent runs, the indexer can usually detect and retrieve just the data that has changed. For blob data, change detection is automatic. For other data sources like Azure SQL or Azure Cosmos DB, change detection must be enabled.

For each document it receives, an indexer implements or coordinates multiple steps, from document retrieval to a final search engine "handoff" for indexing. Optionally, an indexer also drives [skillset execution and outputs](cognitive-search-concept-intro), assuming a skillset is defined.


### Stage 1: Document cracking

Document cracking is the process of opening files and extracting content. Text-based content can be extracted from files on a service, rows in a table, or items in container or collection.

You can also enable image extraction during document cracking for an [extra fee](https://azure.microsoft.com/pricing/details/search/). This is disabled by default and can be enabled via the `imageAction`

property in the [indexer parameters configuration](/en-us/rest/api/searchservice/indexers/create-or-update). Review some [image scenarios](cognitive-search-concept-image-scenarios) for indexer image handling.

Depending on the data source, the indexer will try different operations to extract potentially indexable content:

When the document is a file with embedded images, such as a PDF, the indexer extracts text, images, and metadata. Indexers can open files from

[Azure Blob Storage](search-how-to-index-azure-blob-storage#supported-document-formats),[Azure Data Lake Storage Gen2](search-how-to-index-azure-data-lake-storage#supported-document-formats), and[SharePoint](search-how-to-index-sharepoint-online#supported-document-formats).When the document is a record in

[Azure SQL](search-how-to-index-sql-database), the indexer will extract non-binary content from each field in each record.When the document is a record in

[Azure Cosmos DB](search-how-to-index-cosmosdb-sql), the indexer will extract non-binary content from fields and subfields from the Azure Cosmos DB document.

Note that the document cracking process can also be triggered later during the optional [skillset execution](cognitive-search-concept-intro) stage, using skillsets, for data transformation. Adding a skillset with [image skills](cognitive-search-concept-image-scenarios) allows document cracking to extract images and queue them for processing.

### Stage 2: Field mappings

An indexer extracts text from a source field and sends it to a destination field in an index or knowledge store. When field names and data types coincide, the path is clear. However, you might want different names or types in the output, in which case you need to tell the indexer how to map the field.

To [specify field mappings](search-indexer-field-mappings), enter the source and destination fields in the indexer definition.

Field mapping occurs after document cracking, but before transformations, when the indexer is reading from the source documents. When you define a field mapping, the value of the source field is sent as-is to the destination field with no modifications.

### Stage 3: Skillset execution

Skillset execution is an optional step that invokes built-in or custom AI processing. Skillsets can add optical character recognition (OCR) or other forms of image analysis if the content is binary. Skillsets can also add natural language processing. For example, you can add text translation or key phrase extraction.

Whatever the transformation, skillset execution is where enrichment occurs. If an indexer is a pipeline, you can think of a [skillset](cognitive-search-defining-skillset) as a "pipeline within the pipeline".

### Stage 4: Output field mappings

If you include a skillset, you'll need to [specify output field mappings](cognitive-search-output-field-mapping) in the indexer definition. The output of a skillset is manifested internally as a tree structure referred to as an *enriched document*. Output field mappings allow you to select which parts of this tree to map into fields in your index.

Despite the similarity in names, output field mappings and field mappings build associations from different sources. Field mappings associate the content of source field to a destination field in a search index. Output field mappings associate the content of an internal enriched document (skill outputs) to destination fields in the index. Unlike field mappings, which are considered optional, an output field mapping is required for any transformed content that should be in the index.

The next image shows a sample indexer [debug session](cognitive-search-debug-session) representation of the indexer stages: document cracking, field mappings, skillset execution, and output field mappings.

## Basic workflow

Indexers can offer features that are unique to the data source. In this respect, some aspects of indexer or data source configuration will vary by indexer type. However, all indexers share the same basic composition and requirements. Steps that are common to all indexers are covered below.

### Step 1: Create a data source

Indexers require a *data source* object that provides a connection string and possibly credentials. Data sources are independent objects. Multiple indexers can use the same data source object to load more than one index at a time.

You can create a data source using any of these approaches:

- Using the Azure portal, on the
**Data sources**tab of your search service pages, select**Add data source**to specify the data source definition. - Using the Azure portal, the
[Import data wizard](search-import-data-portal)outputs a data source. - Using the REST APIs, call
[Create Data Source](/en-us/rest/api/searchservice/data-sources/create). - Using the Azure SDK for .NET, call
[SearchIndexerDataSourceConnection class](/en-us/dotnet/api/azure.search.documents.indexes.models.searchindexerdatasourceconnection)

### Step 2: Create an index

An indexer will automate some tasks related to data ingestion, but creating an index is generally not one of them. As a prerequisite, you must have a predefined index that contains corresponding target fields for any source fields in your external data source. Fields need to match by name and data type. If not, you can [define field mappings](search-indexer-field-mappings) to establish the association.

For more information, see [Create an index](search-how-to-create-search-index).

### Step 3: Create and run (or schedule) the indexer

An indexer definition consists of properties that uniquely identify the indexer, specify which data source and index to use, and provide other configuration options that influence run time behaviors, including whether the indexer runs on demand or on a schedule.

Any errors or warnings about data access or skillset validation will occur during indexer execution. Until indexer execution starts, dependent objects such as data sources, indexes, and skillsets are passive on the search service.

For more information, see [Create an indexer](search-howto-create-indexers)

After the first indexer run, you can [rerun it on demand](search-howto-run-reset-indexers) or [set up a schedule](search-howto-schedule-indexers).

You can monitor [indexer status in the Azure portal](search-monitor-indexers) or through [Get Indexer Status API](/en-us/rest/api/searchservice/indexers/get-status). You should also [run queries on the index](search-query-create) to verify the result is what you expected.

Indexers don't have dedicated processing resources. Based on this, indexers' status may show as idle before running (depending on other jobs in the queue) and run times may not be predictable. Other factors define indexer performance as well, such as document size, document complexity, image analysis, among others.

## Next steps

Now that you've been introduced to indexers, a next step is to review indexer properties and parameters, scheduling, and indexer monitoring. Alternatively, you could return to the list of [supported data sources](#supported-data-sources) for more information about a specific source.


---

<!-- DOCUMENTO FUSIONADO: search-indexer-tutorial.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-indexer-tutorial -->

# Tutorial: Index Azure SQL data using the .NET SDK

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn how to configure an [indexer](search-indexer-overview) to extract searchable data from Azure SQL Database and send it to a search index in Azure AI Search.

In this tutorial, you use C# and the [Azure SDK for .NET](/en-us/dotnet/api/overview/azure/search) to:

- Create a data source that connects to Azure SQL Database
- Create an indexer
- Run an indexer to load data into an index
- Query an index as a verification step

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). [Azure SQL Database](https://azure.microsoft.com/services/sql-database/)using SQL Server authentication.[Azure AI Search](search-what-is-azure-search).[Create a service](search-create-service-portal)or[find an existing service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)in your current subscription.[Visual Studio](https://visualstudio.microsoft.com/downloads/).

Note

You can use a free search service for this tutorial. The Free tier limits you to three indexes, three indexers, and three data sources. This tutorial creates one of each. Before you start, make sure you have room on your service to accept the new resources.

## Download files

Source code for this tutorial is in the [DotNetHowToIndexer](https://github.com/Azure-Samples/search-dotnet-getting-started/tree/master/DotNetHowToIndexers) folder in the [Azure-Samples/search-dotnet-getting-started](https://github.com/Azure-Samples/search-dotnet-getting-started) GitHub repository.

## Create services

This tutorial uses Azure AI Search for indexing and queries and Azure SQL Database as an external data source. If possible, create both services in the same region and resource group for proximity and manageability. In practice, Azure SQL Database can be in any region.

### Start with Azure SQL Database

This tutorial provides the *hotels.sql* file in the sample download to populate the database. Azure AI Search consumes flattened rowsets, such as one generated from a view or query. The SQL file in the sample solution creates and populates a single table.

If you have an existing Azure SQL Database resource, you can add the hotels table to it starting at the **Open query** step.

[Create an Azure SQL database](/en-us/azure/azure-sql/database/single-database-create-quickstart). Server configuration for the database is important:Choose the SQL Server authentication option that prompts you to specify a username and password. You need this for the ADO.NET connection string used by the indexer.

Choose a public connection, which makes this tutorial easier to complete. Public isn't recommended for production, and we recommend

[deleting this resource](#clean-up-resources)at the end of the tutorial.

In the Azure portal, go to the new resource.

[Add a firewall rule that allows access from your client](/en-us/azure/azure-sql/database/firewall-create-server-level-portal-quickstart). You can run`ipconfig`

from a command prompt to get your IP address.Use the Query editor to load the sample data. On the navigation pane, select

**Query editor (preview)**and enter the username and password of the server admin.If you get an access denied error, copy the client IP address from the error message, open the network security page for the server, and add an inbound rule that allows access from your client.

In Query editor, select

**Open query**and navigate to the location of*hotels.sql*file on your local computer.Select the file and select

**Open**. The script should look similar to the following screenshot:Select

**Run**to execute the query. In the**Results**pane, you should see a query succeeded message for three rows.To return a rowset from this table, you can execute the following query as a verification step:

`SELECT * FROM Hotels`

Copy the ADO.NET connection string for the database. Under

**Settings**>**Connection Strings**, copy the ADO.NET connection string, which should be similar to the following example:`Server=tcp:<YOUR-DATABASE-NAME>.database.windows.net,1433;Initial Catalog=hotels-db;Persist Security Info=False;User ID=<YOUR-USER-NAME>;Password=<YOUR-PASSWORD>;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;`


You'll need this connection string to set up your environment in the next step.

### Azure AI Search

The next component is Azure AI Search, which you can [create in the Azure portal](search-create-service-portal). You can use the Free tier to complete this tutorial.

### Get an admin key and URL for Azure AI Search

API calls require the service URL and an access key. A search service is created with both, so if you added Azure AI Search to your subscription, follow these steps to get the necessary information:

Sign in to the

[Azure portal](https://portal.azure.com). On your service**Overview**page, copy the endpoint URL. An example endpoint might look like`https://mydemo.search.windows.net`

.On

**Settings**>**Keys**, get an admin key for full rights on the service. There are two interchangeable admin keys, provided for business continuity in case you need to roll one over. You can use either key on requests to add, modify, or delete objects.

## Set up your environment

Start Visual Studio and open

*DotNetHowToIndexers.sln*.In Solution Explorer, open

*appsettings.json*to provide connection information.For

`SearchServiceEndPoint`

, if the full URL on your service**Overview**page is`https://my-demo-service.search.windows.net`

, provide the entire URL.For

`AzureSqlConnectionString`

, the string format is similar to`"Server=tcp:<your-database-name>.database.windows.net,1433;Initial Catalog=hotels-db;Persist Security Info=False;User ID=<your-user-name>;Password=<your-password>;MultipleActiveResultSets=False;Encrypt=True;TrustServerCertificate=False;Connection Timeout=30;"`

.`{ "SearchServiceEndPoint": "<placeholder-search-full-url>", "SearchServiceAdminApiKey": "<placeholder-admin-key-for-search-service>", "AzureSqlConnectionString": "<placeholder-ADO.NET-connection-string", }`

Replace the user password in the SQL connection string with a valid password. While the database and usernames will copy over, you must enter the password manually.


## Create the pipeline

Indexers require a data source object and an index. The relevant code is in two files:

*hotel.cs*contains a schema that defines the index*Program.cs*contains functions for creating and managing structures in your service

### In hotel.cs

The index schema defines the fields collection, including attributes specifying allowed operations, such as whether a field is full-text searchable, filterable, or sortable, as shown in the following field definition for `HotelName`

. A [SearchableField](/en-us/dotnet/api/azure.search.documents.indexes.models.searchablefield) is, by definition, full-text searchable. Other attributes are explicitly assigned.

```
. . .
[SearchableField(IsFilterable = true, IsSortable = true)]
[JsonPropertyName("hotelName")]
public string HotelName { get; set; }
. . .
```


A schema can also include other elements, such as scoring profiles for boosting a search score and custom analyzers. However, for this tutorial, the schema is sparsely defined, consisting only of fields found in the sample datasets.

### In Program.cs

The main program includes logic for creating [an indexer client](/en-us/dotnet/api/azure.search.documents.indexes.models.searchindexer), an index, a data source, and an indexer. The code checks for and deletes existing resources of the same name, assuming that you might run this program multiple times.

The data source object is configured with settings that are specific to Azure SQL Database resources, including [partial or incremental indexing](search-how-to-index-sql-database#CaptureChangedRows) for using the built-in [change detection features](/en-us/sql/relational-databases/track-changes/about-change-tracking-sql-server) of Azure SQL. The source demo hotels database in Azure SQL has a "soft delete" column named **IsDeleted**. When this column is set to true in the database, the indexer removes the corresponding document from the Azure AI Search index.

```
Console.WriteLine("Creating data source...");
var dataSource =
new SearchIndexerDataSourceConnection(
"hotels-sql-ds",
SearchIndexerDataSourceType.AzureSql,
configuration["AzureSQLConnectionString"],
new SearchIndexerDataContainer("hotels"));
indexerClient.CreateOrUpdateDataSourceConnection(dataSource);
```


An indexer object is platform agnostic, where configuration, scheduling, and invocation are the same regardless of the source. This example indexer includes a schedule and a reset option that clears the indexer history. It also calls a method to create and run the indexer immediately. To create or update an indexer, use [CreateOrUpdateIndexerAsync](/en-us/dotnet/api/azure.search.documents.indexes.searchindexerclient.createorupdateindexerasync).

```
Console.WriteLine("Creating Azure SQL indexer...");
var schedule = new IndexingSchedule(TimeSpan.FromDays(1))
{
StartTime = DateTimeOffset.Now
};
var parameters = new IndexingParameters()
{
BatchSize = 100,
MaxFailedItems = 0,
MaxFailedItemsPerBatch = 0
};
// Indexer declarations require a data source and search index.
// Common optional properties include a schedule, parameters, and field mappings
// The field mappings below are redundant due to how the Hotel class is defined, but
// we included them anyway to show the syntax
var indexer = new SearchIndexer("hotels-sql-idxr", dataSource.Name, searchIndex.Name)
{
Description = "Data indexer",
Schedule = schedule,
Parameters = parameters,
FieldMappings =
{
new FieldMapping("_id") {TargetFieldName = "HotelId"},
new FieldMapping("Amenities") {TargetFieldName = "Tags"}
}
};
await indexerClient.CreateOrUpdateIndexerAsync(indexer);
```


Indexer runs are usually scheduled, but during development, you might want to run the indexer immediately using [RunIndexerAsync](/en-us/dotnet/api/azure.search.documents.indexes.searchindexerclient.runindexerasync).

```
Console.WriteLine("Running Azure SQL indexer...");
try
{
await indexerClient.RunIndexerAsync(indexer.Name);
}
catch (RequestFailedException ex) when (ex.Status == 429)
{
Console.WriteLine("Failed to run indexer: {0}", ex.Message);
}
```


## Build the solution

Select **F5** to build and run the solution. The program executes in debug mode. A console window reports the status of each operation.


Your code runs locally in Visual Studio, connecting to your search service on Azure, which in turn connects to Azure SQL Database and retrieves the dataset. With this many operations, there are several potential points of failure. If you get an error, check the following conditions first:

Search service connection information that you provide is the full URL. If you only entered the service name, operations stop at index creation, with a failure to connect error.

Database connection information in

*appsettings.json*. It should be the ADO.NET connection string obtained from the Azure portal, modified to include a username and password that are valid for your database. The user account must have permission to retrieve data. Your local client IP address must be allowed inbound access through the firewall.Resource limits. Recall that the Free tier has limits of three indexes, indexers, and data sources. A service at the maximum limit can't create new objects.


## Search

Use the Azure portal to verify object creation, and then use **Search explorer** to query the index.

Sign in to the

[Azure portal](https://portal.azure.com)and go to your search service. From the left pane, open each page to verify the objects are created.**Indexes**,**Indexers**, and**Data Sources**should have**hotels-sql-idx**,**hotels-sql-indexer**, and**hotels-sql-ds**, respectively.On the

**Indexes**tab, select the**hotels-sql-idx**index. On the hotels page,**Search explorer**is the first tab.Select

**Search**to issue an empty query.The three entries in your index are returned as JSON documents. Search explorer returns documents in JSON so that you can view the entire structure.

[Switch to](search-explorer#start-search-explorer)so that you can enter query parameters.**JSON view**`{ "search": "river", "count": true }`

This query invokes full text search on the term

`river`

. The result includes a count of the matching documents. Returning the count of matching documents is helpful in testing scenarios where you have a large index with thousands or millions of documents. In this case, only one document matches the query.Enter parameters that limit search results to fields of interest.

`{ "search": "river", "select": "hotelId, hotelName, baseRate, description", "count": true }`

The query response is reduced to selected fields, resulting in more concise output.


## Reset and rerun

In the early experimental stages of development, the most practical approach for design iteration is to delete the objects from Azure AI Search and allow your code to rebuild them. Resource names are unique. Deleting an object lets you recreate it using the same name.

The sample code for this tutorial checks for existing objects and deletes them so that you can rerun your code.

You can also use the Azure portal to delete indexes, indexers, and data sources.

## Clean up resources

When you're working in your own subscription, at the end of a project, it's a good idea to remove the resources that you no longer need. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.

You can find and manage resources in the Azure portal, using the All resources or Resource groups link in the left-navigation pane.

## Next steps

Now that you're familiar with the basics of SQL Database indexing, take a closer look at indexer configuration:
