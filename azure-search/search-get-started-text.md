---
source_url: https://learn.microsoft.com/en-us/azure/search/search-get-started-text
fetched_at: 2026-01-25T03:10:32.666532
---

# Quickstart: Full-text search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use the Azure.Search.Documents client library to create, load, and query a search index with sample data for [full-text search](search-lucene-query-architecture). Full-text search uses Apache Lucene for indexing and queries and the BM25 ranking algorithm for scoring results.

This quickstart uses fictional hotel data from the [azure-search-sample-data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels/hotel-json-documents) repo to populate the index.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-dotnet-samples/tree/main/quickstart-keyword-search) to start with a finished project or follow these steps to create your own.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An Azure AI Search service.

[Create a service](search-create-service-portal)if you don't have one. For this quickstart, you can use a free service.

## Microsoft Entra ID prerequisites

For the recommended keyless authentication with Microsoft Entra ID, you must:

Install the

[Azure CLI](/en-us/cli/azure/install-azure-cli).Assign the

`Search Service Contributor`

and`Search Index Data Contributor`

roles to your user account. You can assign roles in the Azure portal under**Access control (IAM)**>**Add role assignment**. For more information, see[Connect to Azure AI Search using roles](search-security-rbac).

## Get service information

You need to retrieve the following information to authenticate your application with your Azure AI Search service:

| Variable name | Value |
|---|---|
`SEARCH_API_ENDPOINT` |
This value can be found in the Azure portal. Select your search service and then from the left menu, select Overview. The Url value under Essentials is the endpoint that you need. An example endpoint might look like `https://mydemo.search.windows.net` . |

Learn more about [keyless authentication](/en-us/azure/search/keyless-connections) and [setting environment variables](/en-us/azure/ai-services/cognitive-services-environment-variables).

## Set up

Create a new folder

`full-text-quickstart`

to contain the application and open Visual Studio Code in that folder with the following command:`mkdir full-text-quickstart && cd full-text-quickstart`

Create a new console application with the following command:

`dotnet new console`

Install the Azure AI Search client library (

[Azure.Search.Documents](/en-us/dotnet/api/overview/azure/search.documents-readme)) for .NET with:`dotnet add package Azure.Search.Documents`

For the

**recommended**keyless authentication with Microsoft Entra ID, install the[Azure.Identity](https://www.nuget.org/packages/Azure.Identity)package with:`dotnet add package Azure.Identity`

For the

**recommended**keyless authentication with Microsoft Entra ID, sign in to Azure with the following command:`az login`


## Create, load, and query a search index

In the prior [set up](#set-up) section, you created a new console application and installed the Azure AI Search client library.

In this section, you add code to create a search index, load it with documents, and run queries. You run the program to see the results in the console. For a detailed explanation of the code, see the [Explaining the code](#explaining-the-code) section.

The sample code in this quickstart uses Microsoft Entra ID for the recommended keyless authentication. If you prefer to use an API key, you can replace the `DefaultAzureCredential`

object with a `AzureKeyCredential`

object.

```
Uri serviceEndpoint = new Uri($"https://<Put your search service NAME here>.search.windows.net/");
DefaultAzureCredential credential = new();
```


In

*Program.cs*, paste the following code. Edit the`serviceName`

and`apiKey`

variables with your search service name and admin API key.`using System; using Azure; using Azure.Identity; using Azure.Search.Documents; using Azure.Search.Documents.Indexes; using Azure.Search.Documents.Indexes.Models; using Azure.Search.Documents.Models; namespace AzureSearch.Quickstart { class Program { static void Main(string[] args) { // Your search service endpoint Uri serviceEndpoint = new Uri($"https://<Put your search service NAME here>.search.windows.net/"); // Use the recommended keyless credential instead of the AzureKeyCredential credential. DefaultAzureCredential credential = new(); //AzureKeyCredential credential = new AzureKeyCredential("Your search service admin key"); // Create a SearchIndexClient to send create/delete index commands SearchIndexClient searchIndexClient = new SearchIndexClient(serviceEndpoint, credential); // Create a SearchClient to load and query documents string indexName = "hotels-quickstart"; SearchClient searchClient = new SearchClient(serviceEndpoint, indexName, credential); // Delete index if it exists Console.WriteLine("{0}", "Deleting index...\n"); DeleteIndexIfExists(indexName, searchIndexClient); // Create index Console.WriteLine("{0}", "Creating index...\n"); CreateIndex(indexName, searchIndexClient); SearchClient ingesterClient = searchIndexClient.GetSearchClient(indexName); // Load documents Console.WriteLine("{0}", "Uploading documents...\n"); UploadDocuments(ingesterClient); // Wait 2 secondsfor indexing to complete before starting queries (for demo and console-app purposes only) Console.WriteLine("Waiting for indexing...\n"); System.Threading.Thread.Sleep(2000); // Call the RunQueries method to invoke a series of queries Console.WriteLine("Starting queries...\n"); RunQueries(searchClient); // End the program Console.WriteLine("{0}", "Complete. Press any key to end this program...\n"); Console.ReadKey(); } // Delete the hotels-quickstart index to reuse its name private static void DeleteIndexIfExists(string indexName, SearchIndexClient searchIndexClient) { searchIndexClient.GetIndexNames(); { searchIndexClient.DeleteIndex(indexName); } } // Create hotels-quickstart index private static void CreateIndex(string indexName, SearchIndexClient searchIndexClient) { FieldBuilder fieldBuilder = new FieldBuilder(); var searchFields = fieldBuilder.Build(typeof(Hotel)); var definition = new SearchIndex(indexName, searchFields); var suggester = new SearchSuggester("sg", new[] { "HotelName", "Category", "Address/City", "Address/StateProvince" }); definition.Suggesters.Add(suggester); searchIndexClient.CreateOrUpdateIndex(definition); } // Upload documents in a single Upload request. private static void UploadDocuments(SearchClient searchClient) { IndexDocumentsBatch<Hotel> batch = IndexDocumentsBatch.Create( IndexDocumentsAction.Upload( new Hotel() { HotelId = "1", HotelName = "Stay-Kay City Hotel", Description = "This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities.", Category = "Boutique", Tags = new[] { "view", "air conditioning", "concierge" }, ParkingIncluded = false, LastRenovationDate = new DateTimeOffset(2022, 1, 18, 0, 0, 0, TimeSpan.Zero), Rating = 3.6, Address = new Address() { StreetAddress = "677 5th Ave", City = "New York", StateProvince = "NY", PostalCode = "10022", Country = "USA" } }), IndexDocumentsAction.Upload( new Hotel() { HotelId = "2", HotelName = "Old Century Hotel", Description = "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music.", Category = "Boutique", Tags = new[] { "pool", "free wifi", "concierge" }, ParkingIncluded = false, LastRenovationDate = new DateTimeOffset(2019, 2, 18, 0, 0, 0, TimeSpan.Zero), Rating = 3.60, Address = new Address() { StreetAddress = "140 University Town Center Dr", City = "Sarasota", StateProvince = "FL", PostalCode = "34243", Country = "USA" } }), IndexDocumentsAction.Upload( new Hotel() { HotelId = "3", HotelName = "Gastronomic Landscape Hotel", Description = "The Gastronomic Hotel stands out for its culinary excellence under the management of William Dough, who advises on and oversees all of the Hotel’s restaurant services.", Category = "Suite", Tags = new[] { "restaurant", "bar", "continental breakfast" }, ParkingIncluded = true, LastRenovationDate = new DateTimeOffset(2015, 9, 20, 0, 0, 0, TimeSpan.Zero), Rating = 4.80, Address = new Address() { StreetAddress = "3393 Peachtree Rd", City = "Atlanta", StateProvince = "GA", PostalCode = "30326", Country = "USA" } }), IndexDocumentsAction.Upload( new Hotel() { HotelId = "4", HotelName = "Sublime Palace Hotel", Description = "Sublime Palace Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience.", Category = "Boutique", Tags = new[] { "concierge", "view", "air conditioning" }, ParkingIncluded = true, LastRenovationDate = new DateTimeOffset(2020, 2, 06, 0, 0, 0, TimeSpan.Zero), Rating = 4.60, Address = new Address() { StreetAddress = "7400 San Pedro Ave", City = "San Antonio", StateProvince = "TX", PostalCode = "78216", Country = "USA" } }) ); try { IndexDocumentsResult result = searchClient.IndexDocuments(batch); } catch (Exception) { // If for some reason any documents are dropped during indexing, you can compensate by delaying and // retrying. This simple demo just logs the failed document keys and continues. Console.WriteLine("Failed to index some of the documents: {0}"); } } // Run queries, use WriteDocuments to print output private static void RunQueries(SearchClient searchClient) { SearchOptions options; SearchResults<Hotel> response; // Query 1 Console.WriteLine("Query #1: Search on empty term '*' to return all documents, showing a subset of fields...\n"); options = new SearchOptions() { IncludeTotalCount = true, Filter = "", OrderBy = { "" } }; options.Select.Add("HotelId"); options.Select.Add("HotelName"); options.Select.Add("Rating"); response = searchClient.Search<Hotel>("*", options); WriteDocuments(response); // Query 2 Console.WriteLine("Query #2: Search on 'hotels', filter on 'Rating gt 4', sort by Rating in descending order...\n"); options = new SearchOptions() { Filter = "Rating gt 4", OrderBy = { "Rating desc" } }; options.Select.Add("HotelId"); options.Select.Add("HotelName"); options.Select.Add("Rating"); response = searchClient.Search<Hotel>("hotels", options); WriteDocuments(response); // Query 3 Console.WriteLine("Query #3: Limit search to specific fields (pool in Tags field)...\n"); options = new SearchOptions() { SearchFields = { "Tags" } }; options.Select.Add("HotelId"); options.Select.Add("HotelName"); options.Select.Add("Tags"); response = searchClient.Search<Hotel>("pool", options); WriteDocuments(response); // Query 4 - Use Facets to return a faceted navigation structure for a given query // Filters are typically used with facets to narrow results on OnClick events Console.WriteLine("Query #4: Facet on 'Category'...\n"); options = new SearchOptions() { Filter = "" }; options.Facets.Add("Category"); options.Select.Add("HotelId"); options.Select.Add("HotelName"); options.Select.Add("Category"); response = searchClient.Search<Hotel>("*", options); WriteDocuments(response); // Query 5 Console.WriteLine("Query #5: Look up a specific document...\n"); Response<Hotel> lookupResponse; lookupResponse = searchClient.GetDocument<Hotel>("3"); Console.WriteLine(lookupResponse.Value.HotelId); // Query 6 Console.WriteLine("Query #6: Call Autocomplete on HotelName...\n"); var autoresponse = searchClient.Autocomplete("sa", "sg"); WriteDocuments(autoresponse); } // Write search results to console private static void WriteDocuments(SearchResults<Hotel> searchResults) { foreach (SearchResult<Hotel> result in searchResults.GetResults()) { Console.WriteLine(result.Document); } Console.WriteLine(); } private static void WriteDocuments(AutocompleteResults autoResults) { foreach (AutocompleteItem result in autoResults.Results) { Console.WriteLine(result.Text); } Console.WriteLine(); } } }`

In the same folder, create a new file named

*Hotel.cs*and paste the following code. This code defines the structure of a hotel document.`using System; using System.Text.Json.Serialization; using Azure.Search.Documents.Indexes; using Azure.Search.Documents.Indexes.Models; namespace AzureSearch.Quickstart { public partial class Hotel { [SimpleField(IsKey = true, IsFilterable = true)] public string HotelId { get; set; } [SearchableField(IsSortable = true)] public string HotelName { get; set; } [SearchableField(AnalyzerName = LexicalAnalyzerName.Values.EnLucene)] public string Description { get; set; } [SearchableField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public string Category { get; set; } [SearchableField(IsFilterable = true, IsFacetable = true)] public string[] Tags { get; set; } [SimpleField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public bool? ParkingIncluded { get; set; } [SimpleField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public DateTimeOffset? LastRenovationDate { get; set; } [SimpleField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public double? Rating { get; set; } [SearchableField] public Address Address { get; set; } } }`

Create a new file named

*Hotel.cs*and paste the following code to define the structure of a hotel document. Attributes on the field determine how it's used in an application. For example, the`IsFilterable`

attribute must be assigned to every field that supports a filter expression.`using System; using System.Text.Json.Serialization; using Azure.Search.Documents.Indexes; using Azure.Search.Documents.Indexes.Models; namespace AzureSearch.Quickstart { public partial class Hotel { [SimpleField(IsKey = true, IsFilterable = true)] public string HotelId { get; set; } [SearchableField(IsSortable = true)] public string HotelName { get; set; } [SearchableField(AnalyzerName = LexicalAnalyzerName.Values.EnLucene)] public string Description { get; set; } [SearchableField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public string Category { get; set; } [SearchableField(IsFilterable = true, IsFacetable = true)] public string[] Tags { get; set; } [SimpleField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public bool? ParkingIncluded { get; set; } [SimpleField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public DateTimeOffset? LastRenovationDate { get; set; } [SimpleField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public double? Rating { get; set; } [SearchableField] public Address Address { get; set; } } }`

Create a new file named

*Address.cs*and paste the following code to define the structure of an address document.`using Azure.Search.Documents.Indexes; namespace AzureSearch.Quickstart { public partial class Address { [SearchableField(IsFilterable = true)] public string StreetAddress { get; set; } [SearchableField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public string City { get; set; } [SearchableField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public string StateProvince { get; set; } [SearchableField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public string PostalCode { get; set; } [SearchableField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public string Country { get; set; } } }`

Create a new file named

*Hotel.Methods.cs*and paste the following code to define a`ToString()`

override for the`Hotel`

class.`using System; using System.Text; namespace AzureSearch.Quickstart { public partial class Hotel { public override string ToString() { var builder = new StringBuilder(); if (!String.IsNullOrEmpty(HotelId)) { builder.AppendFormat("HotelId: {0}\n", HotelId); } if (!String.IsNullOrEmpty(HotelName)) { builder.AppendFormat("Name: {0}\n", HotelName); } if (!String.IsNullOrEmpty(Description)) { builder.AppendFormat("Description: {0}\n", Description); } if (!String.IsNullOrEmpty(Category)) { builder.AppendFormat("Category: {0}\n", Category); } if (Tags != null && Tags.Length > 0) { builder.AppendFormat("Tags: [ {0} ]\n", String.Join(", ", Tags)); } if (ParkingIncluded.HasValue) { builder.AppendFormat("Parking included: {0}\n", ParkingIncluded.Value ? "yes" : "no"); } if (LastRenovationDate.HasValue) { builder.AppendFormat("Last renovated on: {0}\n", LastRenovationDate); } if (Rating.HasValue) { builder.AppendFormat("Rating: {0}\n", Rating); } if (Address != null && !Address.IsEmpty) { builder.AppendFormat("Address: \n{0}\n", Address.ToString()); } return builder.ToString(); } } }`

Create a new file named

*Address.Methods.cs*and paste the following code to define a`ToString()`

override for the`Address`

class.`using System; using System.Text; using System.Text.Json.Serialization; namespace AzureSearch.Quickstart { public partial class Address { public override string ToString() { var builder = new StringBuilder(); if (!IsEmpty) { builder.AppendFormat("{0}\n{1}, {2} {3}\n{4}", StreetAddress, City, StateProvince, PostalCode, Country); } return builder.ToString(); } [JsonIgnore] public bool IsEmpty => String.IsNullOrEmpty(StreetAddress) && String.IsNullOrEmpty(City) && String.IsNullOrEmpty(StateProvince) && String.IsNullOrEmpty(PostalCode) && String.IsNullOrEmpty(Country); } }`

Build and run the application with the following command:

`dotnet run`


Output includes messages from [Console.WriteLine](/en-us/dotnet/api/system.console.writeline), with the addition of query information and results.

## Explaining the code

In the previous sections, you created a new console application and installed the Azure AI Search client library. You added code to create a search index, load it with documents, and run queries. You ran the program to see the results in the console.

In this section, we explain the code you added to the console application.

### Create a search client

In *Program.cs*, you created two clients:

[SearchIndexClient](/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient)creates the index.[SearchClient](/en-us/dotnet/api/azure.search.documents.searchclient)loads and queries an existing index.

Both clients need the search service endpoint and credentials described previously in the [Get service information](#get-service-information) section.

The sample code in this quickstart uses Microsoft Entra ID for the recommended keyless authentication. If you prefer to use an API key, you can replace the `DefaultAzureCredential`

object with a `AzureKeyCredential`

object.

```
Uri serviceEndpoint = new Uri($"https://<Put your search service NAME here>.search.windows.net/");
DefaultAzureCredential credential = new();
```


```
static void Main(string[] args)
{
// Your search service endpoint
Uri serviceEndpoint = new Uri($"https://<Put your search service NAME here>.search.windows.net/");
// Use the recommended keyless credential instead of the AzureKeyCredential credential.
DefaultAzureCredential credential = new();
//AzureKeyCredential credential = new AzureKeyCredential("Your search service admin key");
// Create a SearchIndexClient to send create/delete index commands
SearchIndexClient searchIndexClient = new SearchIndexClient(serviceEndpoint, credential);
// Create a SearchClient to load and query documents
string indexName = "hotels-quickstart";
SearchClient searchClient = new SearchClient(serviceEndpoint, indexName, credential);
// REDACTED FOR BREVITY . . .
}
```


### Create an index

This quickstart builds a Hotels index that you load with hotel data and execute queries against. In this step, you define the fields in the index. Each field definition includes a name, data type, and attributes that determine how the field is used.

In this example, synchronous methods of the *Azure.Search.Documents* library are used for simplicity and readability. However, for production scenarios, you should use asynchronous methods to keep your app scalable and responsive. For example, you would use [CreateIndexAsync](/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient.createindexasync) instead of [CreateIndex](/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient.createindex).

#### Define the structures

You created two helper classes, *Hotel.cs* and *Address.cs*, to define the structure of a hotel document and its address. The `Hotel`

class includes fields for a hotel ID, name, description, category, tags, parking, renovation date, rating, and address. The `Address`

class includes fields for street address, city, state/province, postal code, and country/region.

In the *Azure.Search.Documents* client library, you can use [SearchableField](/en-us/dotnet/api/azure.search.documents.indexes.models.searchablefield) and [SimpleField](/en-us/dotnet/api/azure.search.documents.indexes.models.simplefield) to streamline field definitions. Both are derivatives of a [SearchField](/en-us/dotnet/api/azure.search.documents.indexes.models.searchfield) and can potentially simplify your code:

`SimpleField`

can be any data type, is always non-searchable (ignored for full text search queries), and is retrievable (not hidden). Other attributes are off by default, but can be enabled. You might use a`SimpleField`

for document IDs or fields used only in filters, facets, or scoring profiles. If so, be sure to apply any attributes that are necessary for the scenario, such as`IsKey = true`

for a document ID. For more information, see[SimpleFieldAttribute.cs](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/search/Azure.Search.Documents/src/Indexes/SimpleFieldAttribute.cs)in source code.`SearchableField`

must be a string, and is always searchable and retrievable. Other attributes are off by default, but can be enabled. Because this field type is searchable, it supports synonyms and the full complement of analyzer properties. For more information, see the[SearchableFieldAttribute.cs](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/search/Azure.Search.Documents/src/Indexes/SearchableFieldAttribute.cs)in source code.

Whether you use the basic `SearchField`

API or either one of the helper models, you must explicitly enable filter, facet, and sort attributes. For example, [IsFilterable](/en-us/dotnet/api/azure.search.documents.indexes.models.searchfield.isfilterable), [IsSortable](/en-us/dotnet/api/azure.search.documents.indexes.models.searchfield.issortable), and [IsFacetable](/en-us/dotnet/api/azure.search.documents.indexes.models.searchfield.isfacetable) must be explicitly attributed, as shown in the previous sample.

#### Create the search index

In *Program.cs*, you create a [SearchIndex](/en-us/dotnet/api/azure.search.documents.indexes.models.searchindex) object, and then call the [CreateIndex](/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient.createindex) method to express the index in your search service. The index also includes a [SearchSuggester](/en-us/dotnet/api/azure.search.documents.indexes.models.searchsuggester) to enable autocomplete on the specified fields.

```
// Create hotels-quickstart index
private static void CreateIndex(string indexName, SearchIndexClient searchIndexClient)
{
FieldBuilder fieldBuilder = new FieldBuilder();
var searchFields = fieldBuilder.Build(typeof(Hotel));
var definition = new SearchIndex(indexName, searchFields);
var suggester = new SearchSuggester("sg", new[] { "HotelName", "Category", "Address/City", "Address/StateProvince" });
definition.Suggesters.Add(suggester);
searchIndexClient.CreateOrUpdateIndex(definition);
}
```


### Load documents

Azure AI Search searches over content stored in the service. In this step, you load JSON documents that conform to the hotel index you created.

In Azure AI Search, search documents are data structures that are both inputs to indexing and outputs from queries. As obtained from an external data source, document inputs might be rows in a database, blobs in Blob storage, or JSON documents on disk. In this example, we're taking a shortcut and embedding JSON documents for four hotels in the code itself.

When uploading documents, you must use an [IndexDocumentsBatch](/en-us/dotnet/api/azure.search.documents.models.indexdocumentsbatch-1) object. An `IndexDocumentsBatch`

object contains a collection of [Actions](/en-us/dotnet/api/azure.search.documents.models.indexdocumentsbatch-1.actions), each of which contains a document and a property telling Azure AI Search what action to perform ([upload, merge, delete, and mergeOrUpload](/en-us/azure/search/search-what-is-data-import#indexing-actions)).

In *Program.cs*, you create an array of documents and index actions, and then pass the array to `IndexDocumentsBatch`

. The following documents conform to the hotels-quickstart index, as defined by the hotel class.

```
// Upload documents in a single Upload request.
private static void UploadDocuments(SearchClient searchClient)
{
IndexDocumentsBatch<Hotel> batch = IndexDocumentsBatch.Create(
IndexDocumentsAction.Upload(
new Hotel()
{
HotelId = "1",
HotelName = "Stay-Kay City Hotel",
Description = "This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities.",
Category = "Boutique",
Tags = new[] { "view", "air conditioning", "concierge" },
ParkingIncluded = false,
LastRenovationDate = new DateTimeOffset(2022, 1, 18, 0, 0, 0, TimeSpan.Zero),
Rating = 3.6,
Address = new Address()
{
StreetAddress = "677 5th Ave",
City = "New York",
StateProvince = "NY",
PostalCode = "10022",
Country = "USA"
}
}),
// REDACTED FOR BREVITY
}
```


Once you initialize the [IndexDocumentsBatch](/en-us/dotnet/api/azure.search.documents.models.indexdocumentsbatch-1) object, you can send it to the index by calling [IndexDocuments](/en-us/dotnet/api/azure.search.documents.searchclient.indexdocuments) on your [SearchClient](/en-us/dotnet/api/azure.search.documents.searchclient) object.

You load documents using SearchClient in `Main()`

, but the operation also requires admin rights on the service, which is typically associated with SearchIndexClient. One way to set up this operation is to get SearchClient through `SearchIndexClient`

(`searchIndexClient`

in this example).

```
SearchClient ingesterClient = searchIndexClient.GetSearchClient(indexName);
// Load documents
Console.WriteLine("{0}", "Uploading documents...\n");
UploadDocuments(ingesterClient);
```


Because we have a console app that runs all commands sequentially, we add a 2-second wait time between indexing and queries.

```
// Wait 2 seconds for indexing to complete before starting queries (for demo and console-app purposes only)
Console.WriteLine("Waiting for indexing...\n");
System.Threading.Thread.Sleep(2000);
```


The 2-second delay compensates for indexing, which is asynchronous, so that all documents can be indexed before the queries are executed. Coding in a delay is typically only necessary in demos, tests, and sample applications.

### Search an index

You can get query results as soon as the first document is indexed, but actual testing of your index should wait until all documents are indexed.

This section adds two pieces of functionality: query logic, and results. For queries, use the [Search](/en-us/dotnet/api/azure.search.documents.searchclient.search) method. This method takes search text (the query string) and other [options](/en-us/dotnet/api/azure.search.documents.searchoptions).

The [SearchResults](/en-us/dotnet/api/azure.search.documents.models.searchresults-1) class represents the results.

In *Program.cs*, the `WriteDocuments`

method prints search results to the console.

```
// Write search results to console
private static void WriteDocuments(SearchResults<Hotel> searchResults)
{
foreach (SearchResult<Hotel> result in searchResults.GetResults())
{
Console.WriteLine(result.Document);
}
Console.WriteLine();
}
private static void WriteDocuments(AutocompleteResults autoResults)
{
foreach (AutocompleteItem result in autoResults.Results)
{
Console.WriteLine(result.Text);
}
Console.WriteLine();
}
```


#### Query example 1

The `RunQueries`

method executes queries and returns results. Results are Hotel objects. This sample shows the method signature and the first query. This query demonstrates the `Select`

parameter that lets you compose the result using selected fields from the document.

```
// Run queries, use WriteDocuments to print output
private static void RunQueries(SearchClient searchClient)
{
SearchOptions options;
SearchResults<Hotel> response;
// Query 1
Console.WriteLine("Query #1: Search on empty term '*' to return all documents, showing a subset of fields...\n");
options = new SearchOptions()
{
IncludeTotalCount = true,
Filter = "",
OrderBy = { "" }
};
options.Select.Add("HotelId");
options.Select.Add("HotelName");
options.Select.Add("Address/City");
response = searchClient.Search<Hotel>("*", options);
WriteDocuments(response);
// REDACTED FOR BREVITY
}
```


#### Query example 2

In the second query, search on a term, add a filter that selects documents where *Rating* is greater than 4, and then sort by Rating in descending order. Filter is a boolean expression that is evaluated over [IsFilterable](/en-us/dotnet/api/azure.search.documents.indexes.models.searchfield.isfilterable) fields in an index. Filter queries either include or exclude values. As such, there's no relevance score associated with a filter query.

```
// Query 2
Console.WriteLine("Query #2: Search on 'hotels', filter on 'Rating gt 4', sort by Rating in descending order...\n");
options = new SearchOptions()
{
Filter = "Rating gt 4",
OrderBy = { "Rating desc" }
};
options.Select.Add("HotelId");
options.Select.Add("HotelName");
options.Select.Add("Rating");
response = searchClient.Search<Hotel>("hotels", options);
WriteDocuments(response);
```


#### Query example 3

The third query demonstrates `searchFields`

, used to scope a full text search operation to specific fields.

```
// Query 3
Console.WriteLine("Query #3: Limit search to specific fields (pool in Tags field)...\n");
options = new SearchOptions()
{
SearchFields = { "Tags" }
};
options.Select.Add("HotelId");
options.Select.Add("HotelName");
options.Select.Add("Tags");
response = searchClient.Search<Hotel>("pool", options);
WriteDocuments(response);
```


#### Query example 4

The fourth query demonstrates `facets`

, which can be used to structure a faceted navigation structure.

```
// Query 4
Console.WriteLine("Query #4: Facet on 'Category'...\n");
options = new SearchOptions()
{
Filter = ""
};
options.Facets.Add("Category");
options.Select.Add("HotelId");
options.Select.Add("HotelName");
options.Select.Add("Category");
response = searchClient.Search<Hotel>("*", options);
WriteDocuments(response);
```


#### Query example 5

In the fifth query, return a specific document. A document lookup is a typical response to `OnClick`

event in a result set.

```
// Query 5
Console.WriteLine("Query #5: Look up a specific document...\n");
Response<Hotel> lookupResponse;
lookupResponse = searchClient.GetDocument<Hotel>("3");
Console.WriteLine(lookupResponse.Value.HotelId);
```


#### Query example 6

The last query shows the syntax for autocomplete, simulating a partial user input of *sa* that resolves to two possible matches in the sourceFields associated with the suggester you defined in the index.

```
// Query 6
Console.WriteLine("Query #6: Call Autocomplete on HotelName that starts with 'sa'...\n");
var autoresponse = searchClient.Autocomplete("sa", "sg");
WriteDocuments(autoresponse);
```


#### Summary of queries

The previous queries show multiple [ways of matching terms in a query](/en-us/azure/search/search-query-overview#types-of-queries): full-text search, filters, and autocomplete.

Full text search and filters are performed using the [SearchClient.Search](/en-us/dotnet/api/azure.search.documents.searchclient.search) method. A search query can be passed in the `searchText`

string, while a filter expression can be passed in the [Filter](/en-us/dotnet/api/azure.search.documents.searchoptions.filter) property of the [SearchOptions](/en-us/dotnet/api/azure.search.documents.searchoptions) class. To filter without searching, just pass `"*"`

for the `searchText`

parameter of the [Search](/en-us/dotnet/api/azure.search.documents.searchclient.search) method. To search without filtering, leave the `Filter`

property unset, or don't pass in a `SearchOptions`

instance at all.

In this quickstart, you use the Azure.Search.Documents client library to create, load, and query a search index with sample data for [full-text search](search-lucene-query-architecture). Full-text search uses Apache Lucene for indexing and queries and the BM25 ranking algorithm for scoring results.

This quickstart uses fictional hotel data from the [azure-search-sample-data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels/hotel-json-documents) repo to populate the index.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-java-samples/tree/main/quickstart-keyword-search) to start with a finished project or follow these steps to create your own.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An Azure AI Search service.

[Create a service](search-create-service-portal)if you don't have one. For this quickstart, you can use a free service.

## Microsoft Entra ID prerequisites

For the recommended keyless authentication with Microsoft Entra ID, you must:

Install the

[Azure CLI](/en-us/cli/azure/install-azure-cli).Assign the

`Search Service Contributor`

and`Search Index Data Contributor`

roles to your user account. You can assign roles in the Azure portal under**Access control (IAM)**>**Add role assignment**. For more information, see[Connect to Azure AI Search using roles](search-security-rbac).

## Get service information

You need to retrieve the following information to authenticate your application with your Azure AI Search service:

| Variable name | Value |
|---|---|
`SEARCH_API_ENDPOINT` |
This value can be found in the Azure portal. Select your search service and then from the left menu, select Overview. The Url value under Essentials is the endpoint that you need. An example endpoint might look like `https://mydemo.search.windows.net` . |

Learn more about [keyless authentication](/en-us/azure/search/keyless-connections) and [setting environment variables](/en-us/azure/ai-services/cognitive-services-environment-variables).

## Set up

The sample in this quickstart works with the Java Runtime. Install a Java Development Kit such as [Azul Zulu OpenJDK](https://www.azul.com/downloads/?package=jdk). The [Microsoft Build of OpenJDK](https://www.microsoft.com/openjdk) or your preferred JDK should also work.

Install

[Apache Maven](https://maven.apache.org/install.html). Then run`mvn -v`

to confirm successful installation.Create a new

`pom.xml`

file in the root of your project, and copy the following code into it:`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"> <modelVersion>4.0.0</modelVersion> <groupId>azure.search.sample</groupId> <artifactId>azuresearchquickstart</artifactId> <version>1.0.0-SNAPSHOT</version> <build> <sourceDirectory>src</sourceDirectory> <plugins> <plugin> <artifactId>maven-compiler-plugin</artifactId> <version>3.7.0</version> <configuration> <source>1.8</source> <target>1.8</target> </configuration> </plugin> </plugins> </build> <dependencies> <dependency> <groupId>junit</groupId> <artifactId>junit</artifactId> <version>4.11</version> <scope>test</scope> </dependency> <dependency> <groupId>com.azure</groupId> <artifactId>azure-search-documents</artifactId> <version>11.7.3</version> </dependency> <dependency> <groupId>com.azure</groupId> <artifactId>azure-core</artifactId> <version>1.53.0</version> </dependency> <dependency> <groupId>com.azure</groupId> <artifactId>azure-identity</artifactId> <version>1.15.1</version> </dependency> </dependencies> </project>`

Install the dependencies including the Azure AI Search client library (

[Azure.Search.Documents](/en-us/java/api/overview/azure/search)) for Java and[Azure Identity client library for Java](https://mvnrepository.com/artifact/com.azure/azure-identity)with:`mvn clean dependency:copy-dependencies`

For the

**recommended**keyless authentication with Microsoft Entra ID, sign in to Azure with the following command:`az login`


## Create, load, and query a search index

In the prior [set up](#set-up) section, you installed the Azure AI Search client library and other dependencies.

In this section, you add code to create a search index, load it with documents, and run queries. You run the program to see the results in the console. For a detailed explanation of the code, see the [Explaining the code](#explaining-the-code) section.

The sample code in this quickstart uses Microsoft Entra ID for the recommended keyless authentication. If you prefer to use an API key, you can replace the `DefaultAzureCredential`

object with a `AzureKeyCredential`

object.

```
String searchServiceEndpoint = "https://<Put your search service NAME here>.search.windows.net/";
DefaultAzureCredential credential = new DefaultAzureCredentialBuilder().build();
```


Create a new file named

*App.java*and paste the following code into*App.java*:`import java.util.Arrays; import java.util.ArrayList; import java.time.OffsetDateTime; import java.time.ZoneOffset; import java.time.LocalDateTime; import java.time.LocalDate; import java.time.LocalTime; import com.azure.core.util.Configuration; import com.azure.core.util.Context; import com.azure.identity.DefaultAzureCredential; import com.azure.identity.DefaultAzureCredentialBuilder; import com.azure.search.documents.SearchClient; import com.azure.search.documents.SearchClientBuilder; import com.azure.search.documents.indexes.SearchIndexClient; import com.azure.search.documents.indexes.SearchIndexClientBuilder; import com.azure.search.documents.indexes.models.IndexDocumentsBatch; import com.azure.search.documents.models.SearchOptions; import com.azure.search.documents.indexes.models.SearchIndex; import com.azure.search.documents.indexes.models.SearchSuggester; import com.azure.search.documents.util.AutocompletePagedIterable; import com.azure.search.documents.util.SearchPagedIterable; public class App { public static void main(String[] args) { // Your search service endpoint "https://<Put your search service NAME here>.search.windows.net/"; // Use the recommended keyless credential instead of the AzureKeyCredential credential. DefaultAzureCredential credential = new DefaultAzureCredentialBuilder().build(); //AzureKeyCredential credential = new AzureKeyCredential("<Your search service admin key>"); // Create a SearchIndexClient to send create/delete index commands SearchIndexClient searchIndexClient = new SearchIndexClientBuilder() .endpoint(searchServiceEndpoint) .credential(credential) .buildClient(); // Create a SearchClient to load and query documents String indexName = "hotels-quickstart-java"; SearchClient searchClient = new SearchClientBuilder() .endpoint(searchServiceEndpoint) .credential(credential) .indexName(indexName) .buildClient(); // Create Search Index for Hotel model searchIndexClient.createOrUpdateIndex( new SearchIndex(indexName, SearchIndexClient.buildSearchFields(Hotel.class, null)) .setSuggesters(new SearchSuggester("sg", Arrays.asList("HotelName")))); // Upload sample hotel documents to the Search Index uploadDocuments(searchClient); // Wait 2 seconds for indexing to complete before starting queries (for demo and console-app purposes only) System.out.println("Waiting for indexing...\n"); try { Thread.sleep(2000); } catch (InterruptedException e) { } // Call the RunQueries method to invoke a series of queries System.out.println("Starting queries...\n"); RunQueries(searchClient); // End the program System.out.println("Complete.\n"); } // Upload documents in a single Upload request. private static void uploadDocuments(SearchClient searchClient) { var hotelList = new ArrayList<Hotel>(); var hotel = new Hotel(); hotel.hotelId = "1"; hotel.hotelName = "Stay-Kay City Hotel"; hotel.description = "This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities."; hotel.category = "Boutique"; hotel.tags = new String[] { "view", "air conditioning", "concierge" }; hotel.parkingIncluded = false; hotel.lastRenovationDate = OffsetDateTime.of(LocalDateTime.of(LocalDate.of(2022, 1, 18), LocalTime.of(0, 0)), ZoneOffset.UTC); hotel.rating = 3.6; hotel.address = new Address(); hotel.address.streetAddress = "677 5th Ave"; hotel.address.city = "New York"; hotel.address.stateProvince = "NY"; hotel.address.postalCode = "10022"; hotel.address.country = "USA"; hotelList.add(hotel); hotel = new Hotel(); hotel.hotelId = "2"; hotel.hotelName = "Old Century Hotel"; hotel.description = "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music.", hotel.category = "Boutique"; hotel.tags = new String[] { "pool", "free wifi", "concierge" }; hotel.parkingIncluded = false; hotel.lastRenovationDate = OffsetDateTime.of(LocalDateTime.of(LocalDate.of(2019, 2, 18), LocalTime.of(0, 0)), ZoneOffset.UTC); hotel.rating = 3.60; hotel.address = new Address(); hotel.address.streetAddress = "140 University Town Center Dr"; hotel.address.city = "Sarasota"; hotel.address.stateProvince = "FL"; hotel.address.postalCode = "34243"; hotel.address.country = "USA"; hotelList.add(hotel); hotel = new Hotel(); hotel.hotelId = "3"; hotel.hotelName = "Gastronomic Landscape Hotel"; hotel.description = "The Gastronomic Hotel stands out for its culinary excellence under the management of William Dough, who advises on and oversees all of the Hotel’s restaurant services."; hotel.category = "Suite"; hotel.tags = new String[] { "restaurant", "bar", "continental breakfast" }; hotel.parkingIncluded = true; hotel.lastRenovationDate = OffsetDateTime.of(LocalDateTime.of(LocalDate.of(2015, 9, 20), LocalTime.of(0, 0)), ZoneOffset.UTC); hotel.rating = 4.80; hotel.address = new Address(); hotel.address.streetAddress = "3393 Peachtree Rd"; hotel.address.city = "Atlanta"; hotel.address.stateProvince = "GA"; hotel.address.postalCode = "30326"; hotel.address.country = "USA"; hotelList.add(hotel); hotel = new Hotel(); hotel.hotelId = "4"; hotel.hotelName = "Sublime Palace Hotel"; hotel.description = "Sublime Palace Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience."; hotel.category = "Boutique"; hotel.tags = new String[] { "concierge", "view", "air conditioning" }; hotel.parkingIncluded = true; hotel.lastRenovationDate = OffsetDateTime.of(LocalDateTime.of(LocalDate.of(2020, 2, 06), LocalTime.of(0, 0)), ZoneOffset.UTC); hotel.rating = 4.60; hotel.address = new Address(); hotel.address.streetAddress = "7400 San Pedro Ave"; hotel.address.city = "San Antonio"; hotel.address.stateProvince = "TX"; hotel.address.postalCode = "78216"; hotel.address.country = "USA"; hotelList.add(hotel); var batch = new IndexDocumentsBatch<Hotel>(); batch.addMergeOrUploadActions(hotelList); try { searchClient.indexDocuments(batch); } catch (Exception e) { e.printStackTrace(); // If for some reason any documents are dropped during indexing, you can compensate by delaying and // retrying. This simple demo just logs failure and continues System.err.println("Failed to index some of the documents"); } } // Write search results to console private static void WriteSearchResults(SearchPagedIterable searchResults) { searchResults.iterator().forEachRemaining(result -> { Hotel hotel = result.getDocument(Hotel.class); System.out.println(hotel); }); System.out.println(); } // Write autocomplete results to console private static void WriteAutocompleteResults(AutocompletePagedIterable autocompleteResults) { autocompleteResults.iterator().forEachRemaining(result -> { String text = result.getText(); System.out.println(text); }); System.out.println(); } // Run queries, use WriteDocuments to print output private static void RunQueries(SearchClient searchClient) { // Query 1 System.out.println("Query #1: Search on empty term '*' to return all documents, showing a subset of fields...\n"); SearchOptions options = new SearchOptions(); options.setIncludeTotalCount(true); options.setFilter(""); options.setOrderBy(""); options.setSelect("HotelId", "HotelName", "Address/City"); WriteSearchResults(searchClient.search("*", options, Context.NONE)); // Query 2 System.out.println("Query #2: Search on 'hotels', filter on 'Rating gt 4', sort by Rating in descending order...\n"); options = new SearchOptions(); options.setFilter("Rating gt 4"); options.setOrderBy("Rating desc"); options.setSelect("HotelId", "HotelName", "Rating"); WriteSearchResults(searchClient.search("hotels", options, Context.NONE)); // Query 3 System.out.println("Query #3: Limit search to specific fields (pool in Tags field)...\n"); options = new SearchOptions(); options.setSearchFields("Tags"); options.setSelect("HotelId", "HotelName", "Tags"); WriteSearchResults(searchClient.search("pool", options, Context.NONE)); // Query 4 System.out.println("Query #4: Facet on 'Category'...\n"); options = new SearchOptions(); options.setFilter(""); options.setFacets("Category"); options.setSelect("HotelId", "HotelName", "Category"); WriteSearchResults(searchClient.search("*", options, Context.NONE)); // Query 5 System.out.println("Query #5: Look up a specific document...\n"); Hotel lookupResponse = searchClient.getDocument("3", Hotel.class); System.out.println(lookupResponse.hotelId); System.out.println(); // Query 6 System.out.println("Query #6: Call Autocomplete on HotelName that starts with 's'...\n"); WriteAutocompleteResults(searchClient.autocomplete("s", "sg")); } }`

Create a new file named

*Hotel.java*and paste the following code into*Hotel.java*:`import com.azure.search.documents.indexes.SearchableField; import com.azure.search.documents.indexes.SimpleField; import com.fasterxml.jackson.annotation.JsonInclude; import com.fasterxml.jackson.annotation.JsonProperty; import com.fasterxml.jackson.core.JsonProcessingException; import com.fasterxml.jackson.databind.ObjectMapper; import com.fasterxml.jackson.annotation.JsonInclude.Include; import java.time.OffsetDateTime; /** * Model class representing a hotel. */ @JsonInclude(Include.NON_NULL) public class Hotel { /** * Hotel ID */ @JsonProperty("HotelId") @SimpleField(isKey = true) public String hotelId; /** * Hotel name */ @JsonProperty("HotelName") @SearchableField(isSortable = true) public String hotelName; /** * Description */ @JsonProperty("Description") @SearchableField(analyzerName = "en.microsoft") public String description; /** * Category */ @JsonProperty("Category") @SearchableField(isFilterable = true, isSortable = true, isFacetable = true) public String category; /** * Tags */ @JsonProperty("Tags") @SearchableField(isFilterable = true, isFacetable = true) public String[] tags; /** * Whether parking is included */ @JsonProperty("ParkingIncluded") @SimpleField(isFilterable = true, isSortable = true, isFacetable = true) public Boolean parkingIncluded; /** * Last renovation time */ @JsonProperty("LastRenovationDate") @SimpleField(isFilterable = true, isSortable = true, isFacetable = true) public OffsetDateTime lastRenovationDate; /** * Rating */ @JsonProperty("Rating") @SimpleField(isFilterable = true, isSortable = true, isFacetable = true) public Double rating; /** * Address */ @JsonProperty("Address") public Address address; @Override public String toString() { try { return new ObjectMapper().writeValueAsString(this); } catch (JsonProcessingException e) { e.printStackTrace(); return ""; } } }`

Create a new file named

*Address.java*and paste the following code into*Address.java*:`import com.azure.search.documents.indexes.SearchableField; import com.fasterxml.jackson.annotation.JsonInclude; import com.fasterxml.jackson.annotation.JsonProperty; import com.fasterxml.jackson.annotation.JsonInclude.Include; /** * Model class representing an address. */ @JsonInclude(Include.NON_NULL) public class Address { /** * Street address */ @JsonProperty("StreetAddress") @SearchableField public String streetAddress; /** * City */ @JsonProperty("City") @SearchableField(isFilterable = true, isSortable = true, isFacetable = true) public String city; /** * State or province */ @JsonProperty("StateProvince") @SearchableField(isFilterable = true, isSortable = true, isFacetable = true) public String stateProvince; /** * Postal code */ @JsonProperty("PostalCode") @SearchableField(isFilterable = true, isSortable = true, isFacetable = true) public String postalCode; /** * Country */ @JsonProperty("Country") @SearchableField(isFilterable = true, isSortable = true, isFacetable = true) public String country; }`

Run your new console application:

`javac Address.java App.java Hotel.java -cp ".;target\dependency\*" java -cp ".;target\dependency\*" App`


## Explaining the code

In the previous sections, you created a new console application and installed the Azure AI Search client library. You added code to create a search index, load it with documents, and run queries. You ran the program to see the results in the console.

In this section, we explain the code you added to the console application.

### Create a search client

In *App.java* you created two clients:

- SearchIndexClient creates the index.
- SearchClient loads and queries an existing index.

Both clients need the search service endpoint and credentials described previously in the resource information section.

The sample code in this quickstart uses Microsoft Entra ID for the recommended keyless authentication. If you prefer to use an API key, you can replace the `DefaultAzureCredential`

object with a `AzureKeyCredential`

object.

```
String searchServiceEndpoint = "https://<Put your search service NAME here>.search.windows.net/";
DefaultAzureCredential credential = new DefaultAzureCredentialBuilder().build();
```


```
public static void main(String[] args) {
// Your search service endpoint
String searchServiceEndpoint = "https://<Put your search service NAME here>.search.windows.net/";
// Use the recommended keyless credential instead of the AzureKeyCredential credential.
DefaultAzureCredential credential = new DefaultAzureCredentialBuilder().build();
//AzureKeyCredential credential = new AzureKeyCredential("Your search service admin key");
// Create a SearchIndexClient to send create/delete index commands
SearchIndexClient searchIndexClient = new SearchIndexClientBuilder()
.endpoint(searchServiceEndpoint)
.credential(credential)
.buildClient();
// Create a SearchClient to load and query documents
String indexName = "hotels-quickstart-java";
SearchClient searchClient = new SearchClientBuilder()
.endpoint(searchServiceEndpoint)
.credential(credential)
.indexName(indexName)
.buildClient();
// Create Search Index for Hotel model
searchIndexClient.createOrUpdateIndex(
new SearchIndex(indexName, SearchIndexClient.buildSearchFields(Hotel.class, null))
.setSuggesters(new SearchSuggester("sg", Arrays.asList("HotelName"))));
// REDACTED FOR BREVITY . . .
}
```


### Create an index

This quickstart builds a Hotels index that you load with hotel data and execute queries against. In this step, you define the fields in the index. Each field definition includes a name, data type, and attributes that determine how the field is used.

In this example, synchronous methods of the *Azure.Search.Documents* library are used for simplicity and readability. However, for production scenarios, you should use asynchronous methods to keep your app scalable and responsive. For example, you would use [CreateIndexAsync](/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient.createindexasync) instead of [CreateIndex](/en-us/dotnet/api/azure.search.documents.indexes.searchindexclient.createindex).

#### Define the structures

You created two helper classes, *Hotel.java* and *Address.java*, to define the structure of a hotel document and its address. The Hotel class includes fields for a hotel ID, name, description, category, tags, parking, renovation date, rating, and address. The Address class includes fields for street address, city, state/province, postal code, and country/region.

In the Azure.Search.Documents client library, you can use [SearchableField](/en-us/java/api/com.azure.search.documents.indexes.searchablefield) and [SimpleField](/en-us/java/api/com.azure.search.documents.indexes.simplefield) to streamline field definitions.

`SimpleField`

can be any data type, is always non-searchable (ignored for full text search queries), and is retrievable (not hidden). Other attributes are off by default, but can be enabled. You might use a SimpleField for document IDs or fields used only in filters, facets, or scoring profiles. If so, be sure to apply any attributes that are necessary for the scenario, such as IsKey = true for a document ID.`SearchableField`

must be a string, and is always searchable and retrievable. Other attributes are off by default, but can be enabled. Because this field type is searchable, it supports synonyms and the full complement of analyzer properties.

Whether you use the basic `SearchField`

API or either one of the helper models, you must explicitly enable filter, facet, and sort attributes. For example, `isFilterable`

, `isSortable`

, and `isFacetable`

must be explicitly attributed, as shown in the previous sample.

#### Create the search index

In `App.java`

, you create a `SearchIndex`

object in the `main`

method, and then call the `createOrUpdateIndex`

method to create the index in your search service. The index also includes a `SearchSuggester`

to enable autocomplete on the specified fields.

```
// Create Search Index for Hotel model
searchIndexClient.createOrUpdateIndex(
new SearchIndex(indexName, SearchIndexClient.buildSearchFields(Hotel.class, null))
.setSuggesters(new SearchSuggester("sg", Arrays.asList("HotelName"))));
```


### Load documents

Azure AI Search searches over content stored in the service. In this step, you load JSON documents that conform to the hotel index you created.

In Azure AI Search, search documents are data structures that are both inputs to indexing and outputs from queries. As obtained from an external data source, document inputs might be rows in a database, blobs in Blob storage, or JSON documents on disk. In this example, we're taking a shortcut and embedding JSON documents for four hotels in the code itself.

When uploading documents, you must use an [IndexDocumentsBatch](/en-us/java/api/com.azure.search.documents.indexes.models.indexdocumentsbatch) object. An `IndexDocumentsBatch`

object contains a collection of [IndexActions](/en-us/java/api/com.azure.search.documents.models.indexaction), each of which contains a document and a property telling Azure AI Search what action to perform (upload, merge, delete, and mergeOrUpload).

In `App.java`

, you create documents and index actions, and then pass them to `IndexDocumentsBatch`

. The following documents conform to the hotels-quickstart index, as defined by the hotel class.

```
private static void uploadDocuments(SearchClient searchClient)
{
var hotelList = new ArrayList<Hotel>();
var hotel = new Hotel();
hotel.hotelId = "1";
hotel.hotelName = "Stay-Kay City Hotel";
hotel.description = "This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities.",
hotel.category = "Boutique";
hotel.tags = new String[] { "view", "air conditioning", "concierge" };
hotel.parkingIncluded = false;
hotel.lastRenovationDate = OffsetDateTime.of(LocalDateTime.of(LocalDate.of(2022, 1, 18), LocalTime.of(0, 0)), ZoneOffset.UTC);
hotel.rating = 3.6;
hotel.address = new Address();
hotel.address.streetAddress = "677 5th Ave";
hotel.address.city = "New York";
hotel.address.stateProvince = "NY";
hotel.address.postalCode = "10022";
hotel.address.country = "USA";
hotelList.add(hotel);
// REDACTED FOR BREVITY
var batch = new IndexDocumentsBatch<Hotel>();
batch.addMergeOrUploadActions(hotelList);
try
{
searchClient.indexDocuments(batch);
}
catch (Exception e)
{
e.printStackTrace();
// If for some reason any documents are dropped during indexing, you can compensate by delaying and
// retrying. This simple demo just logs failure and continues
System.err.println("Failed to index some of the documents");
}
}
```


Once you initialize the `IndexDocumentsBatch`

object, you can send it to the index by calling [indexDocuments](/en-us/java/api/com.azure.search.documents.searchclient#com-azure-search-documents-searchclient-indexdocuments(com-azure-search-documents-indexes-models-indexdocumentsbatch(-))) on your `SearchClient`

object.

You load documents using SearchClient in `main()`

, but the operation also requires admin rights on the service, which is typically associated with SearchIndexClient. One way to set up this operation is to get SearchClient through `SearchIndexClient`

(`searchIndexClient`

in this example).

```
uploadDocuments(searchClient);
```


Because we have a console app that runs all commands sequentially, we add a 2-second wait time between indexing and queries.

```
// Wait 2 seconds for indexing to complete before starting queries (for demo and console-app purposes only)
System.out.println("Waiting for indexing...\n");
try
{
Thread.sleep(2000);
}
catch (InterruptedException e)
{
}
```


The 2-second delay compensates for indexing, which is asynchronous, so that all documents can be indexed before the queries are executed. Coding in a delay is typically only necessary in demos, tests, and sample applications.

### Search an index

You can get query results as soon as the first document is indexed, but actual testing of your index should wait until all documents are indexed.

This section adds two pieces of functionality: query logic and results. For queries, use the Search method. This method takes search text (the query string) and other options.

In `App.java`

, the `WriteDocuments`

method prints search results to the console.

```
// Write search results to console
private static void WriteSearchResults(SearchPagedIterable searchResults)
{
searchResults.iterator().forEachRemaining(result ->
{
Hotel hotel = result.getDocument(Hotel.class);
System.out.println(hotel);
});
System.out.println();
}
// Write autocomplete results to console
private static void WriteAutocompleteResults(AutocompletePagedIterable autocompleteResults)
{
autocompleteResults.iterator().forEachRemaining(result ->
{
String text = result.getText();
System.out.println(text);
});
System.out.println();
}
```


#### Query example 1

The `RunQueries`

method executes queries and returns results. Results are Hotel objects. This sample shows the method signature and the first query. This query demonstrates the `Select`

parameter that lets you compose the result using selected fields from the document.

```
// Run queries, use WriteDocuments to print output
private static void RunQueries(SearchClient searchClient)
{
// Query 1
System.out.println("Query #1: Search on empty term '*' to return all documents, showing a subset of fields...\n");
SearchOptions options = new SearchOptions();
options.setIncludeTotalCount(true);
options.setFilter("");
options.setOrderBy("");
options.setSelect("HotelId", "HotelName", "Address/City");
WriteSearchResults(searchClient.search("*", options, Context.NONE));
}
```


#### Query example 2

In the second query, search on a term, add a filter that selects documents where Rating is greater than 4, and then sort by *Rating* in descending order. Filter is a boolean expression that is evaluated over `isFilterable`

fields in an index. Filter queries either include or exclude values. As such, there's no relevance score associated with a filter query.

```
// Query 2
System.out.println("Query #2: Search on 'hotels', filter on 'Rating gt 4', sort by Rating in descending order...\n");
options = new SearchOptions();
options.setFilter("Rating gt 4");
options.setOrderBy("Rating desc");
options.setSelect("HotelId", "HotelName", "Rating");
WriteSearchResults(searchClient.search("hotels", options, Context.NONE));
```


#### Query example 3

The third query demonstrates `searchFields`

, used to scope a full text search operation to specific fields.

```
// Query 3
System.out.println("Query #3: Limit search to specific fields (pool in Tags field)...\n");
options = new SearchOptions();
options.setSearchFields("Tags");
options.setSelect("HotelId", "HotelName", "Tags");
WriteSearchResults(searchClient.search("pool", options, Context.NONE));
```


#### Query example 4

The fourth query demonstrates `facets`

, which can be used to structure a faceted navigation structure.

```
// Query 4
System.out.println("Query #4: Facet on 'Category'...\n");
options = new SearchOptions();
options.setFilter("");
options.setFacets("Category");
options.setSelect("HotelId", "HotelName", "Category");
WriteSearchResults(searchClient.search("*", options, Context.NONE));
```


#### Query example 5

In the fifth query, return a specific document.

```
// Query 5
System.out.println("Query #5: Look up a specific document...\n");
Hotel lookupResponse = searchClient.getDocument("3", Hotel.class);
System.out.println(lookupResponse.hotelId);
System.out.println();
```


#### Query example 6

The last query shows the syntax for autocomplete, simulating a partial user input of *s* that resolves to two possible matches in the `sourceFields`

associated with the suggester you defined in the index.

```
// Query 6
System.out.println("Query #6: Call Autocomplete on HotelName that starts with 's'...\n");
WriteAutocompleteResults(searchClient.autocomplete("s", "sg"));
```


#### Summary of queries

The previous queries show multiple ways of matching terms in a query: full-text search, filters, and autocomplete.

Full text search and filters are performed using the [SearchClient.search](/en-us/java/api/com.azure.search.documents.searchclient#com-azure-search-documents-searchclient-search(java-lang-string)) method. A search query can be passed in the `searchText`

string, while a filter expression can be passed in the `filter`

property of the [SearchOptions](/en-us/java/api/com.azure.search.documents.models.searchoptions) class. To filter without searching, just pass "*" for the `searchText`

parameter of the `search`

method. To search without filtering, leave the `filter`

property unset, or don't pass in a `SearchOptions`

instance at all.

In this quickstart, you use the Azure.Search.Documents client library to create, load, and query a search index with sample data for [full-text search](search-lucene-query-architecture). Full-text search uses Apache Lucene for indexing and queries and the BM25 ranking algorithm for scoring results.

This quickstart uses fictional hotel data from the [azure-search-sample-data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels/hotel-json-documents) repo to populate the index.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-javascript-samples/tree/main/quickstart-keyword-search) to start with a finished project or follow these steps to create your own.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An Azure AI Search service.

[Create a service](search-create-service-portal)if you don't have one. For this quickstart, you can use a free service.

## Microsoft Entra ID prerequisites

For the recommended keyless authentication with Microsoft Entra ID, you must:

Install the

[Azure CLI](/en-us/cli/azure/install-azure-cli).Assign the

`Search Service Contributor`

and`Search Index Data Contributor`

roles to your user account. You can assign roles in the Azure portal under**Access control (IAM)**>**Add role assignment**. For more information, see[Connect to Azure AI Search using roles](search-security-rbac).

## Get service information

You need to retrieve the following information to authenticate your application with your Azure AI Search service:

| Variable name | Value |
|---|---|
`SEARCH_API_ENDPOINT` |
This value can be found in the Azure portal. Select your search service and then from the left menu, select Overview. The Url value under Essentials is the endpoint that you need. An example endpoint might look like `https://mydemo.search.windows.net` . |

Learn more about [keyless authentication](/en-us/azure/search/keyless-connections) and [setting environment variables](/en-us/azure/ai-services/cognitive-services-environment-variables).

## Set up

Create a new folder

`full-text-quickstart`

to contain the application and open Visual Studio Code in that folder with the following command:`mkdir full-text-quickstart && cd full-text-quickstart`

Create the

`package.json`

with the following command:`npm init -y`

Install the Azure AI Search client library (

[Azure.Search.Documents](/en-us/javascript/api/overview/azure/search-documents-readme)) for JavaScript with:`npm install @azure/search-documents`

For the

**recommended**passwordless authentication, install the Azure Identity client library with:`npm install @azure/identity`


## Create, load, and query a search index

In the prior [set up](#set-up) section, you installed the Azure AI Search client library and other dependencies.

In this section, you add code to create a search index, load it with documents, and run queries. You run the program to see the results in the console. For a detailed explanation of the code, see the [Explaining the code](#explaining-the-code) section.

The sample code in this quickstart uses Microsoft Entra ID for the recommended keyless authentication. If you prefer to use an API key, you can replace the `DefaultAzureCredential`

object with a `AzureKeyCredential`

object.

```
String searchServiceEndpoint = "https://<Put your search service NAME here>.search.windows.net/";
DefaultAzureCredential credential = new DefaultAzureCredentialBuilder().build();
```


Create a new file named

*index.js*and paste the following code into*index.js*:`// Import from the @azure/search-documents library import { SearchIndexClient, odata } from "@azure/search-documents"; // Import from the Azure Identity library import { DefaultAzureCredential } from "@azure/identity"; // Importing the hotels sample data import hotelData from './hotels.json' assert { type: "json" }; // Load the .env file if it exists import * as dotenv from "dotenv"; dotenv.config(); // Defining the index definition const indexDefinition = { "name": "hotels-quickstart", "fields": [ { "name": "HotelId", "type": "Edm.String", "key": true, "filterable": true }, { "name": "HotelName", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": true, "facetable": false }, { "name": "Description", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false, "analyzerName": "en.lucene" }, { "name": "Description_fr", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false, "analyzerName": "fr.lucene" }, { "name": "Category", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "Tags", "type": "Collection(Edm.String)", "searchable": true, "filterable": true, "sortable": false, "facetable": true }, { "name": "ParkingIncluded", "type": "Edm.Boolean", "filterable": true, "sortable": true, "facetable": true }, { "name": "LastRenovationDate", "type": "Edm.DateTimeOffset", "filterable": true, "sortable": true, "facetable": true }, { "name": "Rating", "type": "Edm.Double", "filterable": true, "sortable": true, "facetable": true }, { "name": "Address", "type": "Edm.ComplexType", "fields": [ { "name": "StreetAddress", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "searchable": true }, { "name": "City", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "StateProvince", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "PostalCode", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "Country", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true } ] } ], "suggesters": [ { "name": "sg", "searchMode": "analyzingInfixMatching", "sourceFields": [ "HotelName" ] } ] }; async function main() { // Your search service endpoint const searchServiceEndpoint = "https://<Put your search service NAME here>.search.windows.net/"; // Use the recommended keyless credential instead of the AzureKeyCredential credential. const credential = new DefaultAzureCredential(); //const credential = new AzureKeyCredential(Your search service admin key); // Create a SearchIndexClient to send create/delete index commands const searchIndexClient = new SearchIndexClient(searchServiceEndpoint, credential); // Creating a search client to upload documents and issue queries const indexName = "hotels-quickstart"; const searchClient = searchIndexClient.getSearchClient(indexName); console.log('Checking if index exists...'); await deleteIndexIfExists(searchIndexClient, indexName); console.log('Creating index...'); let index = await searchIndexClient.createIndex(indexDefinition); console.log(`Index named ${index.name} has been created.`); console.log('Uploading documents...'); let indexDocumentsResult = await searchClient.mergeOrUploadDocuments(hotelData['value']); console.log(`Index operations succeeded: ${JSON.stringify(indexDocumentsResult.results[0].succeeded)} `); // waiting one second for indexing to complete (for demo purposes only) sleep(1000); console.log('Querying the index...'); console.log(); await sendQueries(searchClient); } async function deleteIndexIfExists(searchIndexClient, indexName) { try { await searchIndexClient.deleteIndex(indexName); console.log('Deleting index...'); } catch { console.log('Index does not exist yet.'); } } async function sendQueries(searchClient) { // Query 1 console.log('Query #1 - search everything:'); let searchOptions = { includeTotalCount: true, select: ["HotelId", "HotelName", "Rating"] }; let searchResults = await searchClient.search("*", searchOptions); for await (const result of searchResults.results) { console.log(`${JSON.stringify(result.document)}`); } console.log(`Result count: ${searchResults.count}`); console.log(); // Query 2 console.log('Query #2 - search with filter, orderBy, and select:'); let state = 'FL'; searchOptions = { filter: odata `Address/StateProvince eq ${state}`, orderBy: ["Rating desc"], select: ["HotelId", "HotelName", "Rating"] }; searchResults = await searchClient.search("wifi", searchOptions); for await (const result of searchResults.results) { console.log(`${JSON.stringify(result.document)}`); } console.log(); // Query 3 console.log('Query #3 - limit searchFields:'); searchOptions = { select: ["HotelId", "HotelName", "Rating"], searchFields: ["HotelName"] }; searchResults = await searchClient.search("sublime palace", searchOptions); for await (const result of searchResults.results) { console.log(`${JSON.stringify(result.document)}`); } console.log(); // Query 4 console.log('Query #4 - limit searchFields and use facets:'); searchOptions = { facets: ["Category"], select: ["HotelId", "HotelName", "Rating"], searchFields: ["HotelName"] }; searchResults = await searchClient.search("*", searchOptions); for await (const result of searchResults.results) { console.log(`${JSON.stringify(result.document)}`); } console.log(); // Query 5 console.log('Query #5 - Lookup document:'); let documentResult = await searchClient.getDocument('3'); console.log(`HotelId: ${documentResult.HotelId}; HotelName: ${documentResult.HotelName}`); console.log(); } function sleep(ms) { return new Promise(resolve => setTimeout(resolve, ms)); } main().catch((err) => { console.error("The sample encountered an error:", err); });`

Create a file named

*hotels.json*and paste the following code into*hotels.json*:`{ "value": [ { "HotelId": "1", "HotelName": "Stay-Kay City Hotel", "Description": "This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities.", "Category": "Boutique", "Tags": ["view", "air conditioning", "concierge"], "ParkingIncluded": false, "LastRenovationDate": "2022-01-18T00:00:00Z", "Rating": 3.6, "Address": { "StreetAddress": "677 5th Ave", "City": "New York", "StateProvince": "NY", "PostalCode": "10022" } }, { "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music.", "Category": "Boutique", "Tags": ["pool", "free wifi", "concierge"], "ParkingIncluded": "false", "LastRenovationDate": "2019-02-18T00:00:00Z", "Rating": 3.6, "Address": { "StreetAddress": "140 University Town Center Dr", "City": "Sarasota", "StateProvince": "FL", "PostalCode": "34243" } }, { "HotelId": "3", "HotelName": "Gastronomic Landscape Hotel", "Description": "The Gastronomic Hotel stands out for its culinary excellence under the management of William Dough, who advises on and oversees all of the Hotel’s restaurant services.", "Category": "Suite", "Tags": ["restaurant", "bar", "continental breakfast"], "ParkingIncluded": "true", "LastRenovationDate": "2015-09-20T00:00:00Z", "Rating": 4.8, "Address": { "StreetAddress": "3393 Peachtree Rd", "City": "Atlanta", "StateProvince": "GA", "PostalCode": "30326" } }, { "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Palace Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience.", "Category": "Boutique", "Tags": ["concierge", "view", "air conditioning"], "ParkingIncluded": true, "LastRenovationDate": "2020-02-06T00:00:00Z", "Rating": 4.6, "Address": { "StreetAddress": "7400 San Pedro Ave", "City": "San Antonio", "StateProvince": "TX", "PostalCode": "78216" } } ] }`

Create a file named

*hotels_quickstart_index.json*and paste the following code into*hotels_quickstart_index.json*:`{ "name": "hotels-quickstart", "fields": [ { "name": "HotelId", "type": "Edm.String", "key": true, "filterable": true }, { "name": "HotelName", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": true, "facetable": false }, { "name": "Description", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false, "analyzerName": "en.lucene" }, { "name": "Category", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "Tags", "type": "Collection(Edm.String)", "searchable": true, "filterable": true, "sortable": false, "facetable": true }, { "name": "ParkingIncluded", "type": "Edm.Boolean", "filterable": true, "sortable": true, "facetable": true }, { "name": "LastRenovationDate", "type": "Edm.DateTimeOffset", "filterable": true, "sortable": true, "facetable": true }, { "name": "Rating", "type": "Edm.Double", "filterable": true, "sortable": true, "facetable": true }, { "name": "Address", "type": "Edm.ComplexType", "fields": [ { "name": "StreetAddress", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "searchable": true }, { "name": "City", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "StateProvince", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "PostalCode", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "Country", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true } ] } ], "suggesters": [ { "name": "sg", "searchMode": "analyzingInfixMatching", "sourceFields": [ "HotelName" ] } ] }`

Sign in to Azure with the following command:

`az login`

Run the JavaScript code with the following command:

`node index.js`


## Explaining the code

### Create index

The *hotels_quickstart_index.json* file defines how Azure AI Search works with the documents you load in the next step. Each field is identified by a `name`

and has a specified `type`

. Each field also has a series of index attributes that specify whether Azure AI Search can search, filter, sort, and facet upon the field. Most of the fields are simple data types, but some, like `AddressType`

are complex types that allow you to create rich data structures in your index. You can read more about [supported data types](/en-us/rest/api/searchservice/supported-data-types) and index attributes described in [Create Index (REST)](/en-us/rest/api/searchservice/indexes/create).

With our index definition in place, we want to import *hotels_quickstart_index.json* at the top of *index.js* so the main function can access the index definition.

```
const indexDefinition = require('./hotels_quickstart_index.json');
```


Within the main function, we then create a `SearchIndexClient`

, which is used to create and manage indexes for Azure AI Search.

```
const indexClient = new SearchIndexClient(endpoint, new AzureKeyCredential(apiKey));
```


Next, we want to delete the index if it already exists. This operation is a common practice for test/demo code.

We do this by defining a simple function that tries to delete the index.

```
async function deleteIndexIfExists(indexClient, indexName) {
try {
await indexClient.deleteIndex(indexName);
console.log('Deleting index...');
} catch {
console.log('Index does not exist yet.');
}
}
```


To run the function, we extract the index name from the index definition and pass the `indexName`

along with the `indexClient`

to the `deleteIndexIfExists()`

function.

```
const indexName = indexDefinition["name"];
console.log('Checking if index exists...');
await deleteIndexIfExists(indexClient, indexName);
```


After that, we're ready to create the index with the `createIndex()`

method.

```
console.log('Creating index...');
let index = await indexClient.createIndex(indexDefinition);
console.log(`Index named ${index.name} has been created.`);
```


### Load documents

In Azure AI Search, documents are data structures that are both inputs to indexing and outputs from queries. You can push such data to the index or use an [indexer](/en-us/azure/search/search-indexer-overview). In this case, we'll programmatically push the documents to the index.

Document inputs might be rows in a database, blobs in Blob storage, or, as in this sample, JSON documents on disk. Similar to what we did with the `indexDefinition`

, we also need to import `hotels.json`

at the top of *index.js* so that the data can be accessed in our main function.

```
const hotelData = require('./hotels.json');
```


To index data into the search index, we now need to create a `SearchClient`

. While the `SearchIndexClient`

is used to create and manage an index, the `SearchClient`

is used to upload documents and query the index.

There are two ways to create a `SearchClient`

. The first option is to create a `SearchClient`

from scratch:

```
const searchClient = new SearchClient(endpoint, indexName, new AzureKeyCredential(apiKey));
```


Alternatively, you can use the `getSearchClient()`

method of the `SearchIndexClient`

to create the `SearchClient`

:

```
const searchClient = indexClient.getSearchClient(indexName);
```


Now that the client is defined, upload the documents into the search index. In this case, we use the `mergeOrUploadDocuments()`

method, which uploads the documents or merges them with an existing document if a document with the same key already exists.

```
console.log('Uploading documents...');
let indexDocumentsResult = await searchClient.mergeOrUploadDocuments(hotelData['value']);
console.log(`Index operations succeeded: ${JSON.stringify(indexDocumentsResult.results[0].succeeded)}`);
```


### Search an index

With an index created and documents uploaded, you're ready to send queries to the index. In this section, we send five different queries to the search index to demonstrate different pieces of query functionality available to you.

The queries are written in a `sendQueries()`

function that we call in the main function as follows:

```
await sendQueries(searchClient);
```


Queries are sent using the `search()`

method of `searchClient`

. The first parameter is the search text and the second parameter specifies search options.

#### Query example 1

The first query searches `*`

, which is equivalent to searching everything and selects three of the fields in the index. It's a best practice to only `select`

the fields you need because pulling back unnecessary data can add latency to your queries.

The `searchOptions`

for this query also has `includeTotalCount`

set to `true`

, which returns the number of matching results found.

```
async function sendQueries(searchClient) {
console.log('Query #1 - search everything:');
let searchOptions = {
includeTotalCount: true,
select: ["HotelId", "HotelName", "Rating"]
};
let searchResults = await searchClient.search("*", searchOptions);
for await (const result of searchResults.results) {
console.log(`${JSON.stringify(result.document)}`);
}
console.log(`Result count: ${searchResults.count}`);
// remaining queries go here
}
```


The remaining queries outlined below should also be added to the `sendQueries()`

function. They're separated here for readability.

#### Query example 2

In the next query, we specify the search term `"wifi"`

and also include a filter to only return results where the state is equal to `'FL'`

. Results are also ordered by the Hotel's `Rating`

.

```
console.log('Query #2 - Search with filter, orderBy, and select:');
let state = 'FL';
searchOptions = {
filter: odata`Address/StateProvince eq ${state}`,
orderBy: ["Rating desc"],
select: ["HotelId", "HotelName", "Rating"]
};
searchResults = await searchClient.search("wifi", searchOptions);
for await (const result of searchResults.results) {
console.log(`${JSON.stringify(result.document)}`);
}
```


#### Query example 3

Next, the search is limited to a single searchable field using the `searchFields`

parameter. This approach is a great option to make your query more efficient if you know you're only interested in matches in certain fields.

```
console.log('Query #3 - Limit searchFields:');
searchOptions = {
select: ["HotelId", "HotelName", "Rating"],
searchFields: ["HotelName"]
};
searchResults = await searchClient.search("Sublime Palace", searchOptions);
for await (const result of searchResults.results) {
console.log(`${JSON.stringify(result.document)}`);
}
console.log();
```


#### Query example 4

Another common option to include in a query is `facets`

. Facets allow you to build out filters on your UI to make it easy for users to know what values they can filter down to.

```
console.log('Query #4 - Use facets:');
searchOptions = {
facets: ["Category"],
select: ["HotelId", "HotelName", "Rating"],
searchFields: ["HotelName"]
};
searchResults = await searchClient.search("*", searchOptions);
for await (const result of searchResults.results) {
console.log(`${JSON.stringify(result.document)}`);
}
```


#### Query example 5

The final query uses the `getDocument()`

method of the `searchClient`

. This allows you to efficiently retrieve a document by its key.

```
console.log('Query #5 - Lookup document:');
let documentResult = await searchClient.getDocument(key='3')
console.log(`HotelId: ${documentResult.HotelId}; HotelName: ${documentResult.HotelName}`)
```


#### Summary of queries

The previous queries show multiple ways of matching terms in a query: full-text search, filters, and autocomplete.

Full text search and filters are performed using the `searchClient.search`

method. A search query can be passed in the `searchText`

string, while a filter expression can be passed in the `filter`

property of the `SearchOptions`

class. To filter without searching, just pass "*" for the `searchText`

parameter of the `search`

method. To search without filtering, leave the `filter`

property unset, or don't pass in a `SearchOptions`

instance at all.

In this quickstart, you use PowerShell and the [Azure AI Search REST APIs](/en-us/rest/api/searchservice/) to create, load, and query a search index for [full-text search](search-lucene-query-architecture). Full-text search uses Apache Lucene for indexing and queries and the BM25 ranking algorithm for scoring results.

This quickstart uses fictional hotel data from the [azure-search-sample-data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels/hotel-json-documents) repo to populate the index.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-powershell-samples/tree/main/Quickstart) to start with a finished project or follow these steps to create your own.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An Azure AI Search service.

[Create a service](search-create-service-portal)or[find an existing service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)in your current subscription. For this quickstart, you can use a free service.The

[Azure CLI](/en-us/cli/azure/install-azure-cli)for keyless authentication with Microsoft Entra ID.[PowerShell 7.3](https://github.com/PowerShell/PowerShell)or later. This quickstart uses[Invoke-RestMethod](/en-us/powershell/module/Microsoft.PowerShell.Utility/Invoke-RestMethod)to make REST API calls.

## Configure access

You can connect to your Azure AI Search service using API keys or Microsoft Entra ID with role assignments. Keys are easier to start with, but roles are more secure.

To configure the recommended role-based access:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Settings**>**Keys**.Under

**API Access control**, select**Both**.This option enables both key-based and keyless authentication. After you assign roles, you can return to this step and select

**Role-based access control**.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Assign the

**Search Service Contributor**and**Search Index Data Contributor**roles to your user account.

For more information, see [Connect to Azure AI Search using roles](search-security-rbac).

## Get endpoint

In the next section, you specify the following endpoint to establish a connection to your Azure AI Search service. These steps assume that you [configured role-based access](#configure-access).

To get your service endpoint:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Overview**.Make a note of the URL, which should be similar to

`https://my-service.search.windows.net`

.

## Connect to Azure AI Search

Before you can make REST API calls to your Azure AI Search service, you must authenticate and connect to the service. You perform the following steps in PowerShell, which supports the Azure CLI commands used in steps two and three.

To connect to your search service:

On your local system, open PowerShell.

Sign in to your Azure subscription. If you have multiple subscriptions, select the one that contains your search service.

`az login`

Create a

`$token`

object to store your access token.`$token = az account get-access-token --resource https://search.azure.com/ --query accessToken --output tsv`

Create a

`$headers`

object to store your token and content type.`$headers = @{ 'Authorization' = "Bearer $token" 'Content-Type' = 'application/json' 'Accept' = 'application/json' }`

You only need to set the header once per session, but you must add it to each request.

Create a

`$url`

object that targets the indexes collection on your search service. Replace`<YOUR-SEARCH-SERVICE>`

with the value you obtained in[Get endpoint](#get-endpoint).`$url = "<YOUR-SEARCH-SERVICE>/indexes?api-version=2025-09-01&`$select=name"`

Run

`Invoke-RestMethod`

to send a GET request to your search service. Include`ConvertTo-Json`

to view responses from the service.`Invoke-RestMethod -Uri $url -Headers $headers | ConvertTo-Json`

If your service is empty and has no indexes, the response is similar to the following example. Otherwise, you see a JSON representation of index definitions.

`{ "@odata.context": "https://my-service.search.windows.net/$metadata#indexes", "value": [ ] }`


## Create a search index

Before you add content to Azure AI Search, you must create an index to define how the content is stored and structured. An index is conceptually similar to a table in a relational database, but it's specifically designed for search operations, such as full-text search.

Run the following commands in the same PowerShell session you started in the previous section.

To create an index:

Create a

`$body`

object to define the index schema.`$body = @" { "name": "hotels-quickstart", "fields": [ {"name": "HotelId", "type": "Edm.String", "key": true, "filterable": true}, {"name": "HotelName", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": true, "facetable": false}, {"name": "Description", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false, "analyzer": "en.lucene"}, {"name": "Category", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true}, {"name": "Tags", "type": "Collection(Edm.String)", "searchable": true, "filterable": true, "sortable": false, "facetable": true}, {"name": "ParkingIncluded", "type": "Edm.Boolean", "filterable": true, "sortable": true, "facetable": true}, {"name": "LastRenovationDate", "type": "Edm.DateTimeOffset", "filterable": true, "sortable": true, "facetable": true}, {"name": "Rating", "type": "Edm.Double", "filterable": true, "sortable": true, "facetable": true}, {"name": "Address", "type": "Edm.ComplexType", "fields": [ {"name": "StreetAddress", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "searchable": true}, {"name": "City", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true}, {"name": "StateProvince", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true}, {"name": "PostalCode", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true}, {"name": "Country", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true} ] } ] } "@`

Update the

`$url`

object to target the new index. Replace`<YOUR-SEARCH-SERVICE>`

with the value you obtained in[Get endpoint](#get-endpoint).`$url = "<YOUR-SEARCH-SERVICE>/indexes/hotels-quickstart?api-version=2025-09-01"`

Run

`Invoke-RestMethod`

to create the index on your search service.`Invoke-RestMethod -Uri $url -Headers $headers -Method Put -Body $body | ConvertTo-Json`

The response should contain the JSON representation of the index schema.


### About the create index request

This quickstart calls [Indexes - Create (REST API)](/en-us/rest/api/searchservice/indexes/create) to build a search index named `hotels-quickstart`

and its physical data structures on your search service.

Within the index schema, the `fields`

collection defines the structure of hotel documents. Each field has a `name`

, data `type`

, and attributes that determine its behavior during indexing and queries. The `HotelId`

field is marked as the key, which Azure AI Search requires to uniquely identify each document in an index.

Key points about the index schema:

Use string fields (

`Edm.String`

) to make numeric data full-text searchable. Other[supported data types](/en-us/rest/api/searchservice/supported-data-types), such as`Edm.Int32`

, are filterable, sortable, facetable, and retrievable but aren't searchable.Most of our fields are simple data types, but you can define complex types to represent nested data, such as the

`Address`

field.Field attributes determine allowed actions. The REST APIs allow

[many actions by default](/en-us/rest/api/searchservice/indexes/create#request-body). For example, all strings are searchable and retrievable. With the REST APIs, you might only use attributes if you need to disable a behavior.

## Load the index

Newly created indexes are empty. To populate an index and make it searchable, you must upload JSON documents that conform to the index schema.

In Azure AI Search, documents serve as both inputs for indexing and outputs for queries. For simplicity, this quickstart provides sample hotel documents as inline JSON. In production scenarios, however, content is often pulled from connected data sources and transformed into JSON using [indexers](search-indexer-overview).

To upload documents to your index:

Create a

`$body`

object to store the JSON payload of four sample documents.`$body = @" { "value": [ { "@search.action": "upload", "HotelId": "1", "HotelName": "Stay-Kay City Hotel", "Description": "This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities.", "Category": "Boutique", "Tags": [ "view", "air conditioning", "concierge" ], "ParkingIncluded": false, "LastRenovationDate": "2022-01-18T00:00:00Z", "Rating": 3.60, "Address": { "StreetAddress": "677 5th Ave", "City": "New York", "StateProvince": "NY", "PostalCode": "10022", "Country": "USA" } }, { "@search.action": "upload", "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music.", "Category": "Boutique", "Tags": [ "pool", "free wifi", "concierge" ], "ParkingIncluded": false, "LastRenovationDate": "2019-02-18T00:00:00Z", "Rating": 3.60, "Address": { "StreetAddress": "140 University Town Center Dr", "City": "Sarasota", "StateProvince": "FL", "PostalCode": "34243", "Country": "USA" } }, { "@search.action": "upload", "HotelId": "3", "HotelName": "Gastronomic Landscape Hotel", "Description": "The Gastronomic Hotel stands out for its culinary excellence under the management of William Dough, who advises on and oversees all of the Hotel’s restaurant services.", "Category": "Suite", "Tags": [ "restaurant", "bar", "continental breakfast" ], "ParkingIncluded": true, "LastRenovationDate": "2015-09-20T00:00:00Z", "Rating": 4.80, "Address": { "StreetAddress": "3393 Peachtree Rd", "City": "Atlanta", "StateProvince": "GA", "PostalCode": "30326", "Country": "USA" } }, { "@search.action": "upload", "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Palace Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience.", "Category": "Boutique", "Tags": [ "concierge", "view", "air conditioning" ], "ParkingIncluded": true, "LastRenovationDate": "2020-02-06T00:00:00Z", "Rating": 4.60, "Address": { "StreetAddress": "7400 San Pedro Ave", "City": "San Antonio", "StateProvince": "TX", "PostalCode": "78216", "Country": "USA" } } ] } "@`

Update the

`$url`

object to target the indexing endpoint. Replace`<YOUR-SEARCH-SERVICE>`

with the value you obtained in[Get endpoint](#get-endpoint).`$url = "<YOUR-SEARCH-SERVICE>/indexes/hotels-quickstart/docs/index?api-version=2025-09-01"`

Run

`Invoke-RestMethod`

to send the upload request to your search service.`Invoke-RestMethod -Uri $url -Headers $headers -Method Post -Body $body | ConvertTo-Json`

The response should contain the key and status of each uploaded document.


### About the upload request

This quickstart calls [Documents - Index (REST API)](/en-us/rest/api/searchservice/documents/) to add four sample hotel documents to your index. Compared to the previous request, the URI is extended to include the `docs`

collection and `index`

operation.

Each document in the `value`

array represents a hotel and contains fields that match the index schema. The `@search.action`

parameter specifies the operation to perform for each document. Our example uses `upload`

, which adds the document if it doesn't exist or updates the document if it does exist.

## Query the index

Now that documents are loaded into your index, you can use full-text search to find specific terms or phrases within their fields.

To run a full-text query against your index:

Update the

`$url`

object to specify search parameters. Replace`<YOUR-SEARCH-SERVICE>`

with the value you obtained in[Get endpoint](#get-endpoint).`$url = '<YOUR-SEARCH-SERVICE>/indexes/hotels-quickstart/docs?api-version=2025-09-01&search=attached restaurant&searchFields=Description,Tags&$select=HotelId,HotelName,Tags,Description&$count=true'`

Run

`Invoke-RestMethod`

to send the query request to your search service.`Invoke-RestMethod -Uri $url -Headers $headers | ConvertTo-Json`

The response should be similar to the following example, which shows one matching hotel document, its relevance score, and its selected fields.

`{ "@odata.context": "https://my-service.search.windows.net/indexes('hotels-quickstart')/$metadata#docs(*)", "@odata.count": 1, "value": [ { "@search.score": 0.5575875, "HotelId": "3", "HotelName": "Gastronomic Landscape Hotel", "Description": "The Gastronomic Hotel stands out for its culinary excellence under the management of William Dough, who advises on and oversees all of the Hotel's restaurant services.", "Tags": "restaurant bar continental breakfast" } ] }`


### About the query request

This quickstart calls [Documents - Search Post (REST API)](/en-us/rest/api/searchservice/documents/search-post) to find hotel documents that match your search criteria. The URI still targets the `docs`

collection but no longer includes the `index`

operation.

Full-text search requests always include a `search`

parameter that contains the query text. The query text can include one or more terms, phrases, or operators. In addition to `search`

, you can specify other parameters to refine the search behavior and results.

Our query searches for the terms "attached restaurant" in the `Description`

and `Tags`

fields of each hotel document. The `$select`

parameter limits the fields returned in the response to `HotelId`

, `HotelName`

, `Tags`

, and `Description`

. The `$count`

parameter requests the total number of matching documents.

#### Other query examples

Run the following commands to explore the query syntax. You can perform string searches, use `$filter`

expressions, limit result sets, select specific fields, and more. Remember to replace `<YOUR-SEARCH-SERVICE>`

with the value you obtained in [Get endpoint](#get-endpoint).

```
# Query example 1
# Search the index for the terms 'restaurant' and 'wifi'
# Return only the HotelName, Description, and Tags fields
$url = '<YOUR-SEARCH-SERVICE>/indexes/hotels-quickstart/docs?api-version=2025-09-01&search=restaurant wifi&$count=true&$select=HotelName,Description,Tags'
# Query example 2
# Use a filter to find hotels rated 4 or higher
# Return only the HotelName and Rating fields
$url = '<YOUR-SEARCH-SERVICE>/indexes/hotels-quickstart/docs?api-version=2025-09-01&search=*&$filter=Rating gt 4&$select=HotelName,Rating'
# Query example 3
# Take the top two results
# Return only the HotelName and Category fields
$url = '<YOUR-SEARCH-SERVICE>/indexes/hotels-quickstart/docs?api-version=2025-09-01&search=boutique&$top=2&$select=HotelName,Category'
# Query example 4
# Sort by a specific field (Address/City) in ascending order
# Return only the HotelName, Address/City, Tags, and Rating fields
$url = '<YOUR-SEARCH-SERVICE>/indexes/hotels-quickstart/docs?api-version=2025-09-01&search=pool&$orderby=Address/City asc&$select=HotelName, Address/City, Tags, Rating'
```


In this quickstart, you use the Azure.Search.Documents client library to create, load, and query a search index with sample data for [full-text search](search-lucene-query-architecture). Full-text search uses Apache Lucene for indexing and queries and the BM25 ranking algorithm for scoring results.

This quickstart uses fictional hotel data from the [azure-search-sample-data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels/hotel-json-documents) repo to populate the index.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/Quickstart-Keyword-Search) to start with a finished project or follow these steps to create your own.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An Azure AI Search service.

[Create a service](search-create-service-portal)if you don't have one. For this quickstart, you can use a free service.[Visual Studio Code](https://code.visualstudio.com/download)with the[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)or an equivalent IDE with Python 3.10 or later. If you haven't installed a suitable version of Python, follow the instructions in the[VS Code Python Tutorial](https://code.visualstudio.com/docs/python/python-tutorial#_install-a-python-interpreter).

## Microsoft Entra ID prerequisites

For the recommended keyless authentication with Microsoft Entra ID, you must:

Install the

[Azure CLI](/en-us/cli/azure/install-azure-cli).Assign the

`Search Service Contributor`

and`Search Index Data Contributor`

roles to your user account. You can assign roles in the Azure portal under**Access control (IAM)**>**Add role assignment**. For more information, see[Connect to Azure AI Search using roles](search-security-rbac).

## Get service information

You need to retrieve the following information to authenticate your application with your Azure AI Search service:

| Variable name | Value |
|---|---|
`SEARCH_API_ENDPOINT` |
This value can be found in the Azure portal. Select your search service and then from the left menu, select Overview. The Url value under Essentials is the endpoint that you need. An example endpoint might look like `https://mydemo.search.windows.net` . |

Learn more about [keyless authentication](/en-us/azure/search/keyless-connections) and [setting environment variables](/en-us/azure/ai-services/cognitive-services-environment-variables).

## Set up your environment

You run the sample code in a Jupyter notebook. So, you need to set up your environment to run Jupyter notebooks.

Download or copy the

[sample notebook from GitHub](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/Quickstart-Keyword-Search).Open the notebook in Visual Studio Code.

Create a new Python environment to use to install the packages you need for this tutorial.

Important

Don't install packages into your global python installation. You should always use a virtual or conda environment when installing python packages, otherwise you can break your global install of Python.

It can take a minute to set up. If you run into problems, see

[Python environments in VS Code](https://code.visualstudio.com/docs/python/environments).Install Jupyter notebooks and the IPython Kernel for Jupyter notebooks if you don't have them already.

`pip install jupyter pip install ipykernel python -m ipykernel install --user --name=.venv`

Select the notebook kernel.

- In the top right corner of the notebook, select
**Select Kernel**. - If you see
`.venv`

in the list, select it. If you don't see it, select**Select Another Kernel**>**Python environments**>`.venv`

.

- In the top right corner of the notebook, select

## Create, load, and query a search index

In this section, you add code to create a search index, load it with documents, and run queries. You run the program to see the results in the console. For a detailed explanation of the code, see the [Explaining the code](#explaining-the-code) section.

Make sure the notebook is open in the

`.venv`

kernel as described in the previous section.Run the first code cell to install the required packages, including

[azure-search-documents](/en-us/python/api/azure-search-documents).`! pip install azure-search-documents==11.6.0b1 --quiet ! pip install azure-identity --quiet ! pip install python-dotenv --quiet`

Replace contents of the second code cell with the following code depending on your authentication method.

Note

The sample code in this quickstart uses Microsoft Entra ID for the recommended keyless authentication. If you prefer to use an API key, you can replace the

`DefaultAzureCredential`

object with a`AzureKeyCredential`

object.`from azure.core.credentials import AzureKeyCredential from azure.identity import DefaultAzureCredential, AzureAuthorityHosts search_endpoint: str = "https://<Put your search service NAME here>.search.windows.net/" authority = AzureAuthorityHosts.AZURE_PUBLIC_CLOUD credential = DefaultAzureCredential(authority=authority) index_name: str = "hotels-quickstart-python"`

Remove the following two lines from the

**Create an index**code cell. Credentials are already set in the previous code cell.`from azure.core.credentials import AzureKeyCredential credential = AzureKeyCredential(search_api_key)`

Run the

**Create an index**code cell to create a search index.Run the remaining code cells sequentially to load documents and run queries.


## Explaining the code

### Create an index

`SearchIndexClient`

is used to create and manage indexes for Azure AI Search. Each field is identified by a `name`

and has a specified `type`

.

Each field also has a series of index attributes that specify whether Azure AI Search can search, filter, sort, and facet upon the field. Most of the fields are simple data types, but some, like `AddressType`

are complex types that allow you to create rich data structures in your index. You can read more about [supported data types](/en-us/rest/api/searchservice/supported-data-types) and index attributes described in [Create Index (REST)](/en-us/rest/api/searchservice/indexes/create).

### Create a documents payload and upload documents

Use an [index action](/en-us/python/api/azure-search-documents/azure.search.documents.models.indexaction) for the operation type, such as upload or merge-and-upload. Documents originate from the [HotelsData](https://github.com/Azure-Samples/azure-search-sample-data/blob/main/hotels/HotelsData_toAzureSearch.JSON) sample on GitHub.

### Search an index

You can get query results as soon as the first document is indexed, but actual testing of your index should wait until all documents are indexed.

Use the *search* method of the [search.client class](/en-us/python/api/azure-search-documents/azure.search.documents.searchclient).

The sample queries in the notebook are:

- Basic query: Executes an empty search (
`search=*`

), returning an unranked list (search score = 1.0) of arbitrary documents. Because there are no criteria, all documents are included in results. - Term query: Adds whole terms to the search expression ("wifi"). This query specifies that results contain only those fields in the
`select`

statement. Limiting the fields that come back minimizes the amount of data sent back over the wire and reduces search latency. - Filtered query: Add a filter expression, returning only those hotels with a rating greater than four, sorted in descending order.
- Fielded scoping: Add
`search_fields`

to scope query execution to specific fields. - Facets: Generate facets for positive matches found in search results. There are no zero matches. If search results don't include the term
*wifi*, then*wifi*doesn't appear in the faceted navigation structure. - Look up a document: Return a document based on its key. This operation is useful if you want to provide drill through when a user selects an item in a search result.
- Autocomplete: Provide potential matches as the user types into the search box. Autocomplete uses a suggester (
`sg`

) to know which fields contain potential matches to suggester requests. In this quickstart, those fields are`Tags`

,`Address/City`

,`Address/Country`

. To simulate autocomplete, pass in the letters*sa*as a partial string. The autocomplete method of[SearchClient](/en-us/python/api/azure-search-documents/azure.search.documents.searchclient)sends back potential term matches.

### Remove the index

If you're finished with this index, you can delete it by running the **Clean up** code cell. Deleting unnecessary indexes frees up space for stepping through more quickstarts and tutorials.

In this quickstart, you use the [Azure AI Search REST APIs](/en-us/rest/api/searchservice) to create, load, and query a search index for [full-text search](search-lucene-query-architecture). Full-text search uses Apache Lucene for indexing and queries and the BM25 ranking algorithm for scoring results.

This quickstart uses fictional hotel data from the [azure-search-sample-data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels/hotel-json-documents) repo to populate the index.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/Quickstart-keyword-search) to start with a finished project or follow these steps to create your own.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An Azure AI Search service.

[Create a service](search-create-service-portal)or[find an existing service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)in your current subscription. For this quickstart, you can use a free service.The

[Azure CLI](/en-us/cli/azure/install-azure-cli)for keyless authentication with Microsoft Entra ID.[Visual Studio Code](https://code.visualstudio.com/download)with the[REST Client extension](https://marketplace.visualstudio.com/items?itemName=humao.rest-client).

## Configure access

You can connect to your Azure AI Search service using API keys or Microsoft Entra ID with role assignments. Keys are easier to start with, but roles are more secure.

To configure the recommended role-based access:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Settings**>**Keys**.Under

**API Access control**, select**Both**.This option enables both key-based and keyless authentication. After you assign roles, you can return to this step and select

**Role-based access control**.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Assign the

**Search Service Contributor**and**Search Index Data Contributor**roles to your user account.

For more information, see [Connect to Azure AI Search using roles](search-security-rbac).

## Get endpoint and token

In the next section, you specify the following endpoint and token to establish a connection to your Azure AI Search service. These steps assume that you [configured role-based access](#configure-access).

To get your service endpoint and token:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Overview**.Make a note of the URL, which should be similar to

`https://my-service.search.windows.net`

.On your local system, open a terminal.

Sign in to your Azure subscription. If you have multiple subscriptions, select the one that contains your search service.

`az login`

Make a note of your Microsoft Entra token.

`az account get-access-token --scope https://search.azure.com/.default`


## Set up your file

Before you can make REST API calls to your Azure AI Search service, you must create a file to store your service endpoint, authentication token, and eventual requests. The REST Client extension in Visual Studio Code supports this task.

To set up your request file:

On your local system, open Visual Studio Code.

Create a

`.rest`

or`.http`

file.Paste the following placeholders and request into the file.

`@baseUrl = PUT-YOUR-SEARCH-SERVICE-ENDPOINT-HERE @token = PUT-YOUR-PERSONAL-IDENTITY-TOKEN-HERE ### List existing indexes by name GET {{baseUrl}}/indexes?api-version=2025-09-01 HTTP/1.1 Authorization: Bearer {{token}}`

Replace the

`@baseUrl`

and`@token`

placeholders with the values you obtained in[Get endpoint and token](#get-endpoint-and-token). Don't include quotation marks.Under

`### List existing indexes by name`

, select**Send Request**.A response should appear in an adjacent pane. If you have existing indexes, they're listed. Otherwise, the list is empty. If the HTTP code is

`200 OK`

, you're ready for the next steps.

## Create a search index

Before you add content to Azure AI Search, you must create an index to define how the content is stored and structured. An index is conceptually similar to a table in a relational database, but it's specifically designed for search operations, such as full-text search.

To create an index:

Paste the following request into your file.

`### Create a new index POST {{baseUrl}}/indexes?api-version=2025-09-01 HTTP/1.1 Content-Type: application/json Authorization: Bearer {{token}} { "name": "hotels-quickstart", "fields": [ {"name": "HotelId", "type": "Edm.String", "key": true, "filterable": true}, {"name": "HotelName", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": true, "facetable": false}, {"name": "Description", "type": "Edm.String", "searchable": true, "filterable": false, "sortable": false, "facetable": false, "analyzer": "en.lucene"}, {"name": "Category", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true}, {"name": "Tags", "type": "Collection(Edm.String)", "searchable": true, "filterable": true, "sortable": false, "facetable": true}, {"name": "ParkingIncluded", "type": "Edm.Boolean", "filterable": true, "sortable": true, "facetable": true}, {"name": "LastRenovationDate", "type": "Edm.DateTimeOffset", "filterable": true, "sortable": true, "facetable": true}, {"name": "Rating", "type": "Edm.Double", "filterable": true, "sortable": true, "facetable": true}, {"name": "Address", "type": "Edm.ComplexType", "fields": [ {"name": "StreetAddress", "type": "Edm.String", "filterable": false, "sortable": false, "facetable": false, "searchable": true}, {"name": "City", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true}, {"name": "StateProvince", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true}, {"name": "PostalCode", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true}, {"name": "Country", "type": "Edm.String", "searchable": true, "filterable": true, "sortable": true, "facetable": true} ] } ] }`

Under

`### Create a new index`

, select**Send Request**.You should receive an

`HTTP/1.1 201 Created`

response whose body contains the JSON representation of the index schema.

### About the create index request

This quickstart calls [Indexes - Create (REST API)](/en-us/rest/api/searchservice/indexes/create) to build a search index named `hotels-quickstart`

and its physical data structures on your search service.

Within the index schema, the `fields`

collection defines the structure of hotel documents. Each field has a `name`

, data `type`

, and attributes that determine its behavior during indexing and queries. The `HotelId`

field is marked as the key, which Azure AI Search requires to uniquely identify each document in an index.

Key points about the index schema:

Use string fields (

`Edm.String`

) to make numeric data full-text searchable. Other[supported data types](/en-us/rest/api/searchservice/supported-data-types), such as`Edm.Int32`

, are filterable, sortable, facetable, and retrievable but aren't searchable.Most of our fields are simple data types, but you can define complex types to represent nested data, such as the

`Address`

field.Field attributes determine allowed actions. The REST APIs allow

[many actions by default](/en-us/rest/api/searchservice/indexes/create#request-body). For example, all strings are searchable and retrievable. With the REST APIs, you might only use attributes if you need to disable a behavior.

## Load the index

Newly created indexes are empty. To populate an index and make it searchable, you must upload JSON documents that conform to the index schema.

In Azure AI Search, documents serve as both inputs for indexing and outputs for queries. For simplicity, this quickstart provides sample hotel documents as inline JSON. In production scenarios, however, content is often pulled from connected data sources and transformed into JSON using [indexers](search-indexer-overview).

To upload documents to your index:

Paste the following request into your file.

`### Upload documents POST {{baseUrl}}/indexes/hotels-quickstart/docs/index?api-version=2025-09-01 HTTP/1.1 Content-Type: application/json Authorization: Bearer {{token}} { "value": [ { "@search.action": "upload", "HotelId": "1", "HotelName": "Stay-Kay City Hotel", "Description": "This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities.", "Category": "Boutique", "Tags": [ "view", "air conditioning", "concierge" ], "ParkingIncluded": false, "LastRenovationDate": "2022-01-18T00:00:00Z", "Rating": 3.60, "Address": { "StreetAddress": "677 5th Ave", "City": "New York", "StateProvince": "NY", "PostalCode": "10022", "Country": "USA" } }, { "@search.action": "upload", "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music.", "Category": "Boutique", "Tags": [ "pool", "free wifi", "concierge" ], "ParkingIncluded": false, "LastRenovationDate": "2019-02-18T00:00:00Z", "Rating": 3.60, "Address": { "StreetAddress": "140 University Town Center Dr", "City": "Sarasota", "StateProvince": "FL", "PostalCode": "34243", "Country": "USA" } }, { "@search.action": "upload", "HotelId": "3", "HotelName": "Gastronomic Landscape Hotel", "Description": "The Gastronomic Hotel stands out for its culinary excellence under the management of William Dough, who advises on and oversees all of the Hotel's restaurant services.", "Category": "Suite", "Tags": [ "restaurant", "bar", "continental breakfast" ], "ParkingIncluded": true, "LastRenovationDate": "2015-09-20T00:00:00Z", "Rating": 4.80, "Address": { "StreetAddress": "3393 Peachtree Rd", "City": "Atlanta", "StateProvince": "GA", "PostalCode": "30326", "Country": "USA" } }, { "@search.action": "upload", "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Palace Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience.", "Category": "Luxury", "Tags": [ "concierge", "view", "air conditioning" ], "ParkingIncluded": true, "LastRenovationDate": "2020-02-06T00:00:00Z", "Rating": 4.60, "Address": { "StreetAddress": "7400 San Pedro Ave", "City": "San Antonio", "StateProvince": "TX", "PostalCode": "78216", "Country": "USA" } } ] }`

Under

`### Upload documents`

, select**Send Request**.You should receive an

`HTTP/1.1 200 OK`

response whose body contains the key and status of each uploaded document.

### About the upload request

This quickstart calls [Documents - Index (REST API)](/en-us/rest/api/searchservice/documents/) to add four sample hotel documents to your index. Compared to the previous request, the URI is extended to include the `docs`

collection and `index`

operation.

Each document in the `value`

array represents a hotel and contains fields that match the index schema. The `@search.action`

parameter specifies the operation to perform for each document. Our example uses `upload`

, which adds the document if it doesn't exist or updates the document if it does exist.

## Query the index

Now that documents are loaded into your index, you can use full-text search to find specific terms or phrases within their fields.

To run a full-text query against your index:

Paste the following request into your file.

`### Run a query POST {{baseUrl}}/indexes/hotels-quickstart/docs/search?api-version=2025-09-01 HTTP/1.1 Content-Type: application/json Authorization: Bearer {{token}} { "search": "attached restaurant", "select": "HotelId, HotelName, Tags, Description", "searchFields": "Description, Tags", "count": true }`

Under

`### Run a query`

, select**Send Request**.You should receive an

`HTTP/1.1 200 OK`

response similar to the following example, which shows one matching hotel document, its relevance score, and its selected fields.`{ "@odata.context": "https://my-service.search.windows.net/indexes('hotels-quickstart')/$metadata#docs(*)", "@odata.count": 1, "value": [ { "@search.score": 0.5575875, "HotelId": "3", "HotelName": "Gastronomic Landscape Hotel", "Description": "The Gastronomic Hotel stands out for its culinary excellence under the management of William Dough, who advises on and oversees all of the Hotel\u2019s restaurant services.", "Tags": [ "restaurant", "bar", "continental breakfast" ] } ] }`


### About the query request

This quickstart calls [Documents - Search Post (REST API)](/en-us/rest/api/searchservice/documents/search-post) to find hotel documents that match your search criteria. The URI now targets the `/docs/search`

operation.

Full-text search requests always include a `search`

parameter that contains the query text. The query text can include one or more terms, phrases, or operators. In addition to `search`

, you can specify other parameters to refine the search behavior and results.

Our query searches for the terms "attached restaurant" in the `Description`

and `Tags`

fields of each hotel document. The `select`

parameter limits the fields returned in the response to `HotelId`

, `HotelName`

, `Tags`

, and `Description`

. The `count`

parameter requests the total number of matching documents.

In this quickstart, you use the Azure.Search.Documents client library to create, load, and query a search index with sample data for [full-text search](search-lucene-query-architecture). Full-text search uses Apache Lucene for indexing and queries and the BM25 ranking algorithm for scoring results.

This quickstart uses fictional hotel data from the [azure-search-sample-data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels/hotel-json-documents) repo to populate the index.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-javascript-samples/tree/main/quickstart-keyword-search) to start with a finished project or follow these steps to create your own.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - An Azure AI Search service.
[Create a service](search-create-service-portal)if you don't have one. For this quickstart, you can use a free service.

## Microsoft Entra ID prerequisites

For the recommended keyless authentication with Microsoft Entra ID, you must:

Install the

[Azure CLI](/en-us/cli/azure/install-azure-cli).Assign the

`Search Service Contributor`

and`Search Index Data Contributor`

roles to your user account. You can assign roles in the Azure portal under**Access control (IAM)**>**Add role assignment**. For more information, see[Connect to Azure AI Search using roles](search-security-rbac).

## Get service information

You need to retrieve the following information to authenticate your application with your Azure AI Search service:

| Variable name | Value |
|---|---|
`SEARCH_API_ENDPOINT` |
This value can be found in the Azure portal. Select your search service and then from the left menu, select Overview. The Url value under Essentials is the endpoint that you need. An example endpoint might look like `https://mydemo.search.windows.net` . |

Learn more about [keyless authentication](/en-us/azure/search/keyless-connections) and [setting environment variables](/en-us/azure/ai-services/cognitive-services-environment-variables).

## Set up

Create a new folder

`full-text-quickstart`

to contain the application and open Visual Studio Code in that folder with the following command:`mkdir full-text-quickstart && cd full-text-quickstart`

Create the

`package.json`

with the following command:`npm init -y`

Update the

`package.json`

to ECMAScript with the following command:`npm pkg set type=module`

Install the Azure AI Search client library (

[Azure.Search.Documents](/en-us/javascript/api/overview/azure/search-documents-readme)) for JavaScript with:`npm install @azure/search-documents`

For the

**recommended**passwordless authentication, install the Azure Identity client library with:`npm install @azure/identity`


## Create, load, and query a search index

In the prior [set up](#set-up) section, you installed the Azure AI Search client library and other dependencies.

In this section, you add code to create a search index, load it with documents, and run queries. You run the program to see the results in the console. For a detailed explanation of the code, see the [Explaining the code](#explaining-the-code) section.

The sample code in this quickstart uses Microsoft Entra ID for the recommended keyless authentication. If you prefer to use an API key, you can replace the `DefaultAzureCredential`

object with a `AzureKeyCredential`

object.

```
const searchServiceEndpoint = "https://<Put your search service NAME here>.search.windows.net/";
const credential = new DefaultAzureCredential();
```


Create a new file named

*index.ts*and paste the following code into*index.ts*:`// Import from the @azure/search-documents library import { SearchIndexClient, SearchClient, SearchFieldDataType, AzureKeyCredential, odata, SearchIndex } from "@azure/search-documents"; // Import from the Azure Identity library import { DefaultAzureCredential } from "@azure/identity"; // Importing the hotels sample data import hotelData from './hotels.json' assert { type: "json" }; // Load the .env file if it exists import * as dotenv from "dotenv"; dotenv.config(); // Defining the index definition const indexDefinition: SearchIndex = { "name": "hotels-quickstart", "fields": [ { "name": "HotelId", "type": "Edm.String" as SearchFieldDataType, "key": true, "filterable": true }, { "name": "HotelName", "type": "Edm.String" as SearchFieldDataType, "searchable": true, "filterable": false, "sortable": true, "facetable": false }, { "name": "Description", "type": "Edm.String" as SearchFieldDataType, "searchable": true, "filterable": false, "sortable": false, "facetable": false, "analyzerName": "en.lucene" }, { "name": "Category", "type": "Edm.String" as SearchFieldDataType, "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "Tags", "type": "Collection(Edm.String)", "searchable": true, "filterable": true, "sortable": false, "facetable": true }, { "name": "ParkingIncluded", "type": "Edm.Boolean", "filterable": true, "sortable": true, "facetable": true }, { "name": "LastRenovationDate", "type": "Edm.DateTimeOffset", "filterable": true, "sortable": true, "facetable": true }, { "name": "Rating", "type": "Edm.Double", "filterable": true, "sortable": true, "facetable": true }, { "name": "Address", "type": "Edm.ComplexType", "fields": [ { "name": "StreetAddress", "type": "Edm.String" as SearchFieldDataType, "filterable": false, "sortable": false, "facetable": false, "searchable": true }, { "name": "City", "type": "Edm.String" as SearchFieldDataType, "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "StateProvince", "type": "Edm.String" as SearchFieldDataType, "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "PostalCode", "type": "Edm.String" as SearchFieldDataType, "searchable": true, "filterable": true, "sortable": true, "facetable": true }, { "name": "Country", "type": "Edm.String" as SearchFieldDataType, "searchable": true, "filterable": true, "sortable": true, "facetable": true } ] } ], "suggesters": [ { "name": "sg", "searchMode": "analyzingInfixMatching", "sourceFields": [ "HotelName" ] } ] }; async function main() { // Your search service endpoint const searchServiceEndpoint = "https://<Put your search service NAME here>.search.windows.net/"; // Use the recommended keyless credential instead of the AzureKeyCredential credential. const credential = new DefaultAzureCredential(); //const credential = new AzureKeyCredential(Your search service admin key); // Create a SearchIndexClient to send create/delete index commands const searchIndexClient: SearchIndexClient = new SearchIndexClient( searchServiceEndpoint, credential ); // Creating a search client to upload documents and issue queries const indexName: string = "hotels-quickstart"; const searchClient: SearchClient<any> = searchIndexClient.getSearchClient(indexName); console.log('Checking if index exists...'); await deleteIndexIfExists(searchIndexClient, indexName); console.log('Creating index...'); let index: SearchIndex = await searchIndexClient.createIndex(indexDefinition); console.log(`Index named ${index.name} has been created.`); console.log('Uploading documents...'); let indexDocumentsResult = await searchClient.mergeOrUploadDocuments(hotelData['value']); console.log(`Index operations succeeded: ${JSON.stringify(indexDocumentsResult.results[0].succeeded)} `); // waiting one second for indexing to complete (for demo purposes only) sleep(1000); console.log('Querying the index...'); console.log(); await sendQueries(searchClient); } async function deleteIndexIfExists(searchIndexClient: SearchIndexClient, indexName: string) { try { await searchIndexClient.deleteIndex(indexName); console.log('Deleting index...'); } catch { console.log('Index does not exist yet.'); } } async function sendQueries(searchClient: SearchClient<any>) { // Query 1 console.log('Query #1 - search everything:'); let searchOptions: any = { includeTotalCount: true, select: ["HotelId", "HotelName", "Rating"] }; let searchResults = await searchClient.search("*", searchOptions); for await (const result of searchResults.results) { console.log(`${JSON.stringify(result.document)}`); } console.log(`Result count: ${searchResults.count}`); console.log(); // Query 2 console.log('Query #2 - search with filter, orderBy, and select:'); let state = 'FL'; searchOptions = { filter: odata`Address/StateProvince eq ${state}`, orderBy: ["Rating desc"], select: ["HotelId", "HotelName", "Rating"] }; searchResults = await searchClient.search("wifi", searchOptions); for await (const result of searchResults.results) { console.log(`${JSON.stringify(result.document)}`); } console.log(); // Query 3 console.log('Query #3 - limit searchFields:'); searchOptions = { select: ["HotelId", "HotelName", "Rating"], searchFields: ["HotelName"] }; searchResults = await searchClient.search("sublime palace", searchOptions); for await (const result of searchResults.results) { console.log(`${JSON.stringify(result.document)}`); } console.log(); // Query 4 console.log('Query #4 - limit searchFields and use facets:'); searchOptions = { facets: ["Category"], select: ["HotelId", "HotelName", "Rating"], searchFields: ["HotelName"] }; searchResults = await searchClient.search("*", searchOptions); for await (const result of searchResults.results) { console.log(`${JSON.stringify(result.document)}`); } console.log(); // Query 5 console.log('Query #5 - Lookup document:'); let documentResult = await searchClient.getDocument('3'); console.log(`HotelId: ${documentResult.HotelId}; HotelName: ${documentResult.HotelName}`); console.log(); } function sleep(ms: number) { return new Promise(resolve => setTimeout(resolve, ms)); } main().catch((err) => { console.error("The sample encountered an error:", err); });`

Create a file named

*hotels.json*and paste the following code into*hotels.json*:`{ "value": [ { "HotelId": "1", "HotelName": "Stay-Kay City Hotel", "Description": "This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities.", "Category": "Boutique", "Tags": ["view", "air conditioning", "concierge"], "ParkingIncluded": false, "LastRenovationDate": "2022-01-18T00:00:00Z", "Rating": 3.6, "Address": { "StreetAddress": "677 5th Ave", "City": "New York", "StateProvince": "NY", "PostalCode": "10022" } }, { "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music.", "Category": "Boutique", "Tags": ["pool", "free wifi", "concierge"], "ParkingIncluded": "false", "LastRenovationDate": "2019-02-18T00:00:00Z", "Rating": 3.6, "Address": { "StreetAddress": "140 University Town Center Dr", "City": "Sarasota", "StateProvince": "FL", "PostalCode": "34243" } }, { "HotelId": "3", "HotelName": "Gastronomic Landscape Hotel", "Description": "The Gastronomic Hotel stands out for its culinary excellence under the management of William Dough, who advises on and oversees all of the Hotel’s restaurant services.", "Category": "Suite", "Tags": ["restaurant, "bar", "continental breakfast"], "ParkingIncluded": "true", "LastRenovationDate": "2015-09-20T00:00:00Z", "Rating": 4.8, "Address": { "StreetAddress": "3393 Peachtree Rd", "City": "Atlanta", "StateProvince": "GA", "PostalCode": "30326" } }, { "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Palace Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience.", "Category": "Boutique", "Tags": ["concierge", "view", "air conditioning"], "ParkingIncluded": true, "LastRenovationDate": "2020-02-06T00:00:00Z", "Rating": 4.6, "Address": { "StreetAddress": "7400 San Pedro Ave", "City": "San Antonio", "StateProvince": "TX", "PostalCode": "78216" } } ] }`

Create the

`tsconfig.json`

file to transpile the TypeScript code and copy the following code for ECMAScript.`{ "compilerOptions": { "module": "NodeNext", "target": "ES2022", // Supports top-level await "moduleResolution": "NodeNext", "skipLibCheck": true, // Avoid type errors from node_modules "strict": true // Enable strict type-checking options }, "include": ["*.ts"] }`

Transpile from TypeScript to JavaScript.

`tsc`

Sign in to Azure with the following command:

`az login`

Run the JavaScript code with the following command:

`node index.js`


## Explaining the code

### Create index

Create a file *hotels_quickstart_index.json*. This file defines how Azure AI Search works with the documents you load in the next step. Each field is identified by a `name`

and has a specified `type`

. Each field also has a series of index attributes that specify whether Azure AI Search can search, filter, sort, and facet upon the field. Most of the fields are simple data types, but some, like `AddressType`

are complex types that allow you to create rich data structures in your index. You can read more about [supported data types](/en-us/rest/api/searchservice/supported-data-types) and index attributes described in [Create Index (REST)](/en-us/rest/api/searchservice/indexes/create).

We want to import *hotels_quickstart_index.json* so the main function can access the index definition.

```
import indexDefinition from './hotels_quickstart_index.json';
interface HotelIndexDefinition {
name: string;
fields: SimpleField[] | ComplexField[];
suggesters: SearchSuggester[];
};
const hotelIndexDefinition: HotelIndexDefinition = indexDefinition as HotelIndexDefinition;
```


Within the main function, we then create a `SearchIndexClient`

, which is used to create and manage indexes for Azure AI Search.

```
const indexClient = new SearchIndexClient(endpoint, new AzureKeyCredential(apiKey));
```


Next, we want to delete the index if it already exists. This operation is a common practice for test/demo code.

We do this by defining a simple function that tries to delete the index.

```
async function deleteIndexIfExists(indexClient: SearchIndexClient, indexName: string): Promise<void> {
try {
await indexClient.deleteIndex(indexName);
console.log('Deleting index...');
} catch {
console.log('Index does not exist yet.');
}
}
```


To run the function, we extract the index name from the index definition and pass the `indexName`

along with the `indexClient`

to the `deleteIndexIfExists()`

function.

```
// Getting the name of the index from the index definition
const indexName: string = hotelIndexDefinition.name;
console.log('Checking if index exists...');
await deleteIndexIfExists(indexClient, indexName);
```


After that, we're ready to create the index with the `createIndex()`

method.

```
console.log('Creating index...');
let index = await indexClient.createIndex(hotelIndexDefinition);
console.log(`Index named ${index.name} has been created.`);
```


### Load documents

In Azure AI Search, documents are data structures that are both inputs to indexing and outputs from queries. You can push such data to the index or use an [indexer](/en-us/azure/search/search-indexer-overview). In this case, we'll programmatically push the documents to the index.

Document inputs might be rows in a database, blobs in Blob storage, or, as in this sample, JSON documents on disk. You can either download [hotels.json](https://github.com/Azure-Samples/azure-search-javascript-samples/blob/main/quickstart/hotels.json) or create your own *hotels.json* file with the following content:

Similar to what we did with the indexDefinition, we also need to import `hotels.json`

at the top of *index.ts* so that the data can be accessed in our main function.

```
import hotelData from './hotels.json';
interface Hotel {
HotelId: string;
HotelName: string;
Description: string;
Category: string;
Tags: string[];
ParkingIncluded: string | boolean;
LastRenovationDate: string;
Rating: number;
Address: {
StreetAddress: string;
City: string;
StateProvince: string;
PostalCode: string;
};
};
const hotels: Hotel[] = hotelData["value"];
```


To index data into the search index, we now need to create a `SearchClient`

. While the `SearchIndexClient`

is used to create and manage an index, the `SearchClient`

is used to upload documents and query the index.

There are two ways to create a `SearchClient`

. The first option is to create a `SearchClient`

from scratch:

```
const searchClient = new SearchClient<Hotel>(endpoint, indexName, new AzureKeyCredential(apiKey));
```


Alternatively, you can use the `getSearchClient()`

method of the `SearchIndexClient`

to create the `SearchClient`

:

```
const searchClient = indexClient.getSearchClient<Hotel>(indexName);
```


Now that the client is defined, upload the documents into the search index. In this case, we use the `mergeOrUploadDocuments()`

method, which uploads the documents or merges them with an existing document if a document with the same key already exists. Then check that the operation succeeded because at least the first document exists.

```
console.log("Uploading documents...");
const indexDocumentsResult = await searchClient.mergeOrUploadDocuments(hotels);
console.log(`Index operations succeeded: ${JSON.stringify(indexDocumentsResult.results[0].succeeded)}`);
```


Run the program again with `tsc && node index.ts`

. You should see a slightly different set of messages from those you saw in Step 1. This time, the index *does* exist, and you should see a message about deleting it before the app creates the new index and posts data to it.

Before we run the queries in the next step, define a function to have the program wait for one second. This is done just for test/demo purposes to ensure the indexing finishes and that the documents are available in the index for our queries.

```
function sleep(ms: number): Promise<void> {
return new Promise((resolve) => setTimeout(resolve, ms));
}
```


To have the program wait for one second, call the `sleep`

function:

```
sleep(1000);
```


### Search an index

With an index created and documents uploaded, you're ready to send queries to the index. In this section, we send five different queries to the search index to demonstrate different pieces of query functionality available to you.

The queries are written in a `sendQueries()`

function that we call in the main function as follows:

```
await sendQueries(searchClient);
```


Queries are sent using the `search()`

method of `searchClient`

. The first parameter is the search text and the second parameter specifies search options.

#### Query example 1

The first query searches `*`

, which is equivalent to searching everything and selects three of the fields in the index. It's a best practice to only `select`

the fields you need because pulling back unnecessary data can add latency to your queries.

The `searchOptions`

for this query also has `includeTotalCount`

set to `true`

, which will return the number of matching results found.

```
async function sendQueries(
searchClient: SearchClient<Hotel>
): Promise<void> {
// Query 1
console.log('Query #1 - search everything:');
const selectFields: SearchFieldArray<Hotel> = [
"HotelId",
"HotelName",
"Rating",
];
const searchOptions1 = {
includeTotalCount: true,
select: selectFields
};
let searchResults = await searchClient.search("*", searchOptions1);
for await (const result of searchResults.results) {
console.log(`${JSON.stringify(result.document)}`);
}
console.log(`Result count: ${searchResults.count}`);
// remaining queries go here
}
```


The remaining queries outlined below should also be added to the `sendQueries()`

function. They're separated here for readability.

#### Query example 2

In the next query, we specify the search term `"wifi"`

and also include a filter to only return results where the state is equal to `'FL'`

. Results are also ordered by the Hotel's `Rating`

.

```
console.log('Query #2 - search with filter, orderBy, and select:');
let state = 'FL';
const searchOptions2 = {
filter: odata`Address/StateProvince eq ${state}`,
orderBy: ["Rating desc"],
select: selectFields
};
searchResults = await searchClient.search("wifi", searchOptions2);
for await (const result of searchResults.results) {
console.log(`${JSON.stringify(result.document)}`);
}
```


#### Query example 3

Next, the search is limited to a single searchable field using the `searchFields`

parameter. This approach is a great option to make your query more efficient if you know you're only interested in matches in certain fields.

```
console.log('Query #3 - limit searchFields:');
const searchOptions3 = {
select: selectFields,
searchFields: ["HotelName"] as const
};
searchResults = await searchClient.search("Sublime Palace", searchOptions3);
for await (const result of searchResults.results) {
console.log(`${JSON.stringify(result.document)}`);
}
```


#### Query example 4

Another common option to include in a query is `facets`

. Facets allow you to provide self-directed drilldown from the results in your UI. The facets results can be turned into checkboxes in the result pane.

```
console.log('Query #4 - limit searchFields and use facets:');
const searchOptions4 = {
facets: ["Category"],
select: selectFields,
searchFields: ["HotelName"] as const
};
searchResults = await searchClient.search("*", searchOptions4);
for await (const result of searchResults.results) {
console.log(`${JSON.stringify(result.document)}`);
}
```


#### Query example 5

The final query uses the `getDocument()`

method of the `searchClient`

. This allows you to efficiently retrieve a document by its key.

```
console.log('Query #5 - Lookup document:');
let documentResult = await searchClient.getDocument('3')
console.log(`HotelId: ${documentResult.HotelId}; HotelName: ${documentResult.HotelName}`)
```


#### Summary of queries

The previous queries show multiple ways of matching terms in a query: full-text search, filters, and autocomplete.

Full text search and filters are performed using the `searchClient.search`

method. A search query can be passed in the `searchText`

string, while a filter expression can be passed in the `filter`

property of the `SearchOptions`

class. To filter without searching, just pass "*" for the `searchText`

parameter of the `search`

method. To search without filtering, leave the `filter`

property unset, or don't pass in a `SearchOptions`

instance at all.

## Clean up resources

When working in your own subscription, it's a good idea to finish a project by determining whether you still need the resources you created. Resources that are left running can cost you money. You can delete resources individually, or you can delete the resource group to delete the entire set of resources.

In the [Azure portal](https://portal.azure.com/), you can find and manage resources by selecting **All resources** or **Resource groups** from the left pane.

If you're using a free service, remember that you're limited to three indexes, indexers, and data sources. You can delete individual items in the Azure portal to stay under the limit.