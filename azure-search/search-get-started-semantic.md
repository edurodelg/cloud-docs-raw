---
source_url: https://learn.microsoft.com/en-us/azure/search/search-get-started-semantic
fetched_at: 2026-01-25T03:14:12.910806
---

# Quickstart: Semantic ranking

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you learn how to use [semantic ranking](semantic-search-overview) by adding a semantic configuration to a search index and adding semantic parameters to a query. You can use the hotels-sample-index or one of your own.

In Azure AI Search, semantic ranking is query-side functionality that uses machine reading comprehension from Microsoft to rescore search results, promoting the most semantically relevant matches to the top of the list. Depending on the content and the query, semantic ranking can [significantly improve search relevance](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/azure-cognitive-search-outperforming-vector-search-with-hybrid/ba-p/3929167) with minimal developer effort.

You can add a semantic configuration to an existing index with no rebuild requirement. Semantic ranking is most effective on text that's informational or descriptive.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).A

[new or existing index](search-how-to-create-search-index)with descriptive or verbose text fields that are attributed as retrievable. This quickstart assumes the[hotels-sample-index](search-get-started-portal).

## Configure access

You can connect to your Azure AI Search service using API keys or Microsoft Entra ID with role assignments. Keys are easier to start with, but roles are more secure. For more information, see [Connect to Azure AI Search using roles](search-security-rbac).

To configure role-based access:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Settings**>**Keys**.Under

**API Access control**, select**Role-based access control**or**Both**if you need time to transition clients to role-based access.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Assign the

**Search Service Contributor**and**Search Index Data Contributor**roles to your user account.

## Start with an index

This quickstart assumes an existing index and modifies it to include a semantic configuration. We recommend the [hotels-sample-index](search-get-started-portal) that you can create in minutes using an Azure portal wizard.

To start with an existing index:

Sign in to the

[Azure portal](https://portal.azure.com/)and find your search service.Under

**Search management**>**Indexes**, select the hotels-sample-index.Select

**Semantic configurations**to ensure the index doesn't have a semantic configuration.Select

**Search explorer**, and then select the**JSON view**.Paste the following JSON into the query editor.

`{ "search": "walking distance to live music", "select": "HotelId, HotelName, Description", "count": true }`

Select

**Search**to run the query.This query is a keyword search. The response should be similar to the following example, as scored by the default BM25 L1 ranker for full-text search.

For readability, the example only selects the

`HotelId`

,`HotelName`

, and`Description`

fields. The results contain verbatim matches on the query terms (`walking`

,`distance`

,`live`

,`music`

) or linguistic variants (`walk`

,`living`

).`"@odata.count": 13, "value": [ { "@search.score": 5.5153193, "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music." }, { "@search.score": 5.074317, "HotelId": "24", "HotelName": "Uptown Chic Hotel", "Description": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance." }, { "@search.score": 4.8959594, "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Cliff Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience." }, { "@search.score": 2.5966604, "HotelId": "35", "HotelName": "Bellevue Suites", "Description": "Comfortable city living in the very center of downtown Bellevue. Newly reimagined, this hotel features apartment-style suites with sleeping, living and work spaces. Located across the street from the Light Rail to downtown. Free shuttle to the airport." }, { "@search.score": 2.566386, "HotelId": "47", "HotelName": "Country Comfort Inn", "Description": "Situated conveniently at the north end of the village, the inn is just a short walk from the lake, offering reasonable rates and all the comforts home inlcuding living room suites and functional kitchens. Pets are welcome." }, { "@search.score": 2.2405157, "HotelId": "9", "HotelName": "Smile Up Hotel", "Description": "Experience the fresh, modern downtown. Enjoy updated rooms, bold style & prime location. Don't miss our weekend live music series featuring who's new/next on the scene." }, { "@search.score": 2.1737604, "HotelId": "8", "HotelName": "Foot Happy Suites", "Description": "Downtown in the heart of the business district. Close to everything. Leave your car behind and walk to the park, shopping, and restaurants. Or grab one of our bikes and take your explorations a little further." }, { "@search.score": 2.0364518, "HotelId": "31", "HotelName": "Country Residence Hotel", "Description": "All of the suites feature full-sized kitchens stocked with cookware, separate living and sleeping areas and sofa beds. Some of the larger rooms have fireplaces and patios or balconies. Experience real country hospitality in the heart of bustling Nashville. The most vibrant music scene in the world is just outside your front door." }, { "@search.score": 1.7595702, "HotelId": "49", "HotelName": "Swirling Currents Hotel", "Description": "Spacious rooms, glamorous suites and residences, rooftop pool, walking access to shopping, dining, entertainment and the city center. Each room comes equipped with a microwave, a coffee maker and a minifridge. In-room entertainment includes complimentary W-Fi and flat-screen TVs. " }, { "@search.score": 1.5502293, "HotelId": "15", "HotelName": "By the Market Hotel", "Description": "Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service." }, { "@search.score": 1.3302404, "HotelId": "42", "HotelName": "Rock Bottom Resort & Campground", "Description": "Rock Bottom is nestled on 20 unspoiled acres on a private cove of Rock Bottom Lake. We feature both lodging and campground accommodations to suit just about every taste. Even though we are out of the traffic of the city, getting there is only a short drive away." }, { "@search.score": 0.9050383, "HotelId": "38", "HotelName": "Lakeside B & B", "Description": "Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply." }, { "@search.score": 0.7334347, "HotelId": "39", "HotelName": "White Mountain Lodge & Suites", "Description": "Live amongst the trees in the heart of the forest. Hike along our extensive trail system. Visit the Natural Hot Springs, or enjoy our signature hot stone massage in the Cathedral of Firs. Relax in the meditation gardens, or join new friends around the communal firepit. Weekend evening entertainment on the patio features special guest musicians or poetry readings." } ]`


This query shows how the response looks *before* semantic ranking is applied. Later, you can run the same query after semantic ranking is configured to see how the response changes.

Tip

You can add a semantic configuration in the Azure portal. However, if you want to learn how to add a semantic configuration programmatically, continue with this quickstart.

## Set up the client

In this quickstart, you use an IDE and the [ Azure.Search.Documents](/en-us/dotnet/api/overview/azure/search.documents-readme) client library to add semantic ranking to an existing search index.

We recommend [Visual Studio](https://visualstudio.microsoft.com/vs/community/) for this quickstart.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-dotnet-samples/tree/main/quickstart-semantic-ranking) to start with a finished project or follow these steps to create your own.

### Install libraries

Start Visual Studio and open the

[quickstart-semantic-ranking.sln](https://github.com/Azure-Samples/azure-search-dotnet-samples/tree/main/quickstart-semantic-ranking)or create a new project using a console application template.In

**Tools**>**NuGet Package Manager**, select**Manage NuGet Packages for Solution...**.Select

**Browse**.Search for the

[Azure.Search.Documents package](https://www.nuget.org/packages/Azure.Search.Documents/)and select the latest stable version.Search for the

[Azure.Identity package](https://www.nuget.org/packages/Azure.Identity)and select the latest stable version.Select

**Install**to add the assembly to your project and solution.

### Sign in to Azure

If you signed in to the [Azure portal](https://portal.azure.com), you're signed into Azure. If you aren't sure, use the Azure CLI or Azure PowerShell to log in: `az login`

or `az connect`

. If you have multiple tenants and subscriptions, see [Quickstart: Connect without keys](search-get-started-rbac) for help on how to connect.

## Update the index

In this section, you update a search index to include a semantic configuration. The code gets the index definition from the search service and adds a semantic configuration.

Open the

[BuildIndex project](https://github.com/Azure-Samples/azure-search-dotnet-samples/tree/main/quickstart-semantic-ranking/BuildIndex)in Visual Studio. The program consists of the following code.This code uses a SearchIndexClient to update an index on your search service.

`class BuildIndex { static async Task Main(string[] args) { string searchServiceName = "PUT-YOUR-SEARCH-SERVICE-NAME-HERE"; string indexName = "hotels-sample-index"; string endpoint = $"https://{searchServiceName}.search.windows.net"; var credential = new Azure.Identity.DefaultAzureCredential(); await ListIndexesAsync(endpoint, credential); await UpdateIndexAsync(endpoint, credential, indexName); } // Print a list of all indexes on the search service // You should see hotels-sample-index in the list static async Task ListIndexesAsync(string endpoint, Azure.Core.TokenCredential credential) { try { var indexClient = new Azure.Search.Documents.Indexes.SearchIndexClient( new Uri(endpoint), credential ); var indexes = indexClient.GetIndexesAsync(); Console.WriteLine("Here's a list of all indexes on the search service. You should see hotels-sample-index:"); await foreach (var index in indexes) { Console.WriteLine(index.Name); } Console.WriteLine(); // Add an empty line for readability } catch (Exception ex) { Console.WriteLine($"Error listing indexes: {ex.Message}"); } } static async Task UpdateIndexAsync(string endpoint, Azure.Core.TokenCredential credential, string indexName) { try { var indexClient = new Azure.Search.Documents.Indexes.SearchIndexClient( new Uri(endpoint), credential ); // Get the existing definition of hotels-sample-index var indexResponse = await indexClient.GetIndexAsync(indexName); var index = indexResponse.Value; // Add a semantic configuration const string semanticConfigName = "semantic-config"; AddSemanticConfiguration(index, semanticConfigName); // Update the index with the new information var updatedIndex = await indexClient.CreateOrUpdateIndexAsync(index); Console.WriteLine("Index updated successfully."); // Print the updated index definition as JSON var refreshedIndexResponse = await indexClient.GetIndexAsync(indexName); var refreshedIndex = refreshedIndexResponse.Value; var jsonOptions = new JsonSerializerOptions { WriteIndented = true }; string indexJson = JsonSerializer.Serialize(refreshedIndex, jsonOptions); Console.WriteLine($"Here is the revised index definition:\n{indexJson}"); } catch (Exception ex) { Console.WriteLine($"Error updating index: {ex.Message}"); } } // This is the semantic configuration definition static void AddSemanticConfiguration(SearchIndex index, string semanticConfigName) { if (index.SemanticSearch == null) { index.SemanticSearch = new SemanticSearch(); } var configs = index.SemanticSearch.Configurations; if (configs == null) { throw new InvalidOperationException("SemanticSearch.Configurations is null and cannot be assigned. Your service must be Basic tier or higher."); } if (!configs.Any(c => c.Name == semanticConfigName)) { var prioritizedFields = new SemanticPrioritizedFields { TitleField = new SemanticField("HotelName"), ContentFields = { new SemanticField("Description") }, KeywordsFields = { new SemanticField("Tags") } }; configs.Add( new SemanticConfiguration( semanticConfigName, prioritizedFields ) ); Console.WriteLine($"Added new semantic configuration '{semanticConfigName}' to the index definition."); } else { Console.WriteLine($"Semantic configuration '{semanticConfigName}' already exists in the index definition."); } index.SemanticSearch.DefaultConfigurationName = semanticConfigName; } }`

Replace the search service URL with a valid endpoint.

Run the program.

Output is logged to a console window from

[Console.WriteLine](/en-us/dotnet/api/system.console.writeline). You should see messages for each step, including the JSON of the index schema with the new semantic configuration included.

## Run semantic queries

In this section, the program runs several semantic queries in sequence.

Open the

[QueryIndex project](https://github.com/Azure-Samples/azure-search-dotnet-samples/tree/main/quickstart-semantic-ranking/QueryIndex)in Visual Studio. The program consists of the following code.This code uses a SearchClient for sending queries to an index.

`class SemanticQuery { static async Task Main(string[] args) { string searchServiceName = "PUT-YOUR-SEARCH-SERVICE-NAME-HERE"; string indexName = "hotels-sample-index"; string endpoint = $"https://{searchServiceName}.search.windows.net"; var credential = new Azure.Identity.DefaultAzureCredential(); var client = new SearchClient(new Uri(endpoint), indexName, credential); // Query 1: Simple query string searchText = "walking distance to live music"; Console.WriteLine("\nQuery 1: Simple query using the search string 'walking distance to live music'."); await RunQuery(client, searchText, new SearchOptions { Size = 5, QueryType = SearchQueryType.Simple, IncludeTotalCount = true, Select = { "HotelId", "HotelName", "Description" } }); Console.WriteLine("Press Enter to continue to the next query..."); Console.ReadLine(); // Query 2: Semantic query (no captions, no answers) Console.WriteLine("\nQuery 2: Semantic query (no captions, no answers) for 'walking distance to live music'."); var semanticOptions = new SearchOptions { Size = 5, QueryType = SearchQueryType.Semantic, SemanticSearch = new SemanticSearchOptions { SemanticConfigurationName = "semantic-config" }, IncludeTotalCount = true, Select = { "HotelId", "HotelName", "Description" } }; await RunQuery(client, searchText, semanticOptions); Console.WriteLine("Press Enter to continue to the next query..."); Console.ReadLine(); // Query 3: Semantic query with captions Console.WriteLine("\nQuery 3: Semantic query with captions."); var captionsOptions = new SearchOptions { Size = 5, QueryType = SearchQueryType.Semantic, SemanticSearch = new SemanticSearchOptions { SemanticConfigurationName = "semantic-config", QueryCaption = new QueryCaption(QueryCaptionType.Extractive) { HighlightEnabled = true } }, IncludeTotalCount = true, Select = { "HotelId", "HotelName", "Description" } }; // Add the field(s) you want captions for to the QueryCaption.Fields collection captionsOptions.HighlightFields.Add("Description"); await RunQuery(client, searchText, captionsOptions, showCaptions: true); Console.WriteLine("Press Enter to continue to the next query..."); Console.ReadLine(); // Query 4: Semantic query with answers // This query uses different search text designed for an answers scenario string searchText2 = "what's a good hotel for people who like to read"; searchText = searchText2; // Update searchText for the next query Console.WriteLine("\nQuery 4: Semantic query with a verbatim answer from the Description field for 'what's a good hotel for people who like to read'."); var answersOptions = new SearchOptions { Size = 5, QueryType = SearchQueryType.Semantic, SemanticSearch = new SemanticSearchOptions { SemanticConfigurationName = "semantic-config", QueryAnswer = new QueryAnswer(QueryAnswerType.Extractive) }, IncludeTotalCount = true, Select = { "HotelId", "HotelName", "Description" } }; await RunQuery(client, searchText2, answersOptions, showAnswers: true); static async Task RunQuery( SearchClient client, string searchText, SearchOptions options, bool showCaptions = false, bool showAnswers = false) { try { var response = await client.SearchAsync<SearchDocument>(searchText, options); if (showAnswers && response.Value.SemanticSearch?.Answers != null) { Console.WriteLine("Extractive Answers:"); foreach (var answer in response.Value.SemanticSearch.Answers) { Console.WriteLine($" {answer.Highlights}"); } Console.WriteLine(new string('-', 40)); } await foreach (var result in response.Value.GetResultsAsync()) { var doc = result.Document; // Print captions first if available if (showCaptions && result.SemanticSearch?.Captions != null) { foreach (var caption in result.SemanticSearch.Captions) { Console.WriteLine($"Caption: {caption.Highlights}"); } } Console.WriteLine($"HotelId: {doc.GetString("HotelId")}"); Console.WriteLine($"HotelName: {doc.GetString("HotelName")}"); Console.WriteLine($"Description: {doc.GetString("Description")}"); Console.WriteLine($"@search.score: {result.Score}"); // Print @search.rerankerScore if available if (result.SemanticSearch != null && result.SemanticSearch.RerankerScore.HasValue) { Console.WriteLine($"@search.rerankerScore: {result.SemanticSearch.RerankerScore.Value}"); } Console.WriteLine(new string('-', 40)); } } catch (Exception ex) { Console.WriteLine($"Error querying index: {ex.Message}"); } } } }`

Replace the search service URL with a valid endpoint.

Run the program.

Output is logged to a console window from

[Console.WriteLine](/en-us/dotnet/api/system.console.writeline). You should see search results for each query.

### Output for semantic query (no captions or answers)

This output is from the semantic query, with no captions or answers. The query string is 'walking distance to live music'.

Here, the initial results from the term query are rescored using the semantic ranking models. For this particular dataset and query, the first several results are in similar positions. The effects of semantic ranking are more pronounced in the remainder of the results.

```
HotelId: 24
HotelName: Uptown Chic Hotel
Description: Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance.
@search.score: 5.074317
@search.rerankerScore: 2.613231658935547
----------------------------------------
HotelId: 2
HotelName: Old Century Hotel
Description: The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music.
@search.score: 5.5153193
@search.rerankerScore: 2.271434783935547
----------------------------------------
HotelId: 4
HotelName: Sublime Palace Hotel
Description: Sublime Cliff Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience.
@search.score: 4.8959594
@search.rerankerScore: 1.9861756563186646
----------------------------------------
HotelId: 39
HotelName: White Mountain Lodge & Suites
Description: Live amongst the trees in the heart of the forest. Hike along our extensive trail system. Visit the Natural Hot Springs, or enjoy our signature hot stone massage in the Cathedral of Firs. Relax in the meditation gardens, or join new friends around the communal firepit. Weekend evening entertainment on the patio features special guest musicians or poetry readings.
@search.score: 0.7334347
@search.rerankerScore: 1.9615401029586792
----------------------------------------
HotelId: 15
HotelName: By the Market Hotel
Description: Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service.
@search.score: 1.5502293
@search.rerankerScore: 1.9085469245910645
----------------------------------------
Press Enter to continue to the next query...
```


### Output for a semantic query with captions

Here are the results for the query that adds captions with hit highlighting.

```
Caption: Chic hotel near the city. High-rise hotel in downtown, within walking distance to<em> theaters, </em>art galleries, restaurants and shops. Visit<em> Seattle Art Museum </em>by day, and then head over to<em> Benaroya Hall </em>to catch the evening's concert performance.
HotelId: 24
HotelName: Uptown Chic Hotel
Description: Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance.
@search.score: 5.074317
@search.rerankerScore: 2.613231658935547
----------------------------------------
Caption:
HotelId: 2
HotelName: Old Century Hotel
Description: The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music.
@search.score: 5.5153193
@search.rerankerScore: 2.271434783935547
----------------------------------------
Caption: Sublime Cliff Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within<em> short walking distance </em>to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort,.
HotelId: 4
HotelName: Sublime Palace Hotel
Description: Sublime Cliff Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience.
@search.score: 4.8959594
@search.rerankerScore: 1.9861756563186646
----------------------------------------
Caption: Live amongst the trees in the heart of the forest. Hike along our extensive trail system. Visit the Natural Hot Springs, or enjoy our signature hot stone massage in the Cathedral of Firs. Relax in the meditation gardens, or join new friends around the communal firepit. Weekend<em> evening entertainment </em>on the patio features special<em> guest musicians </em>or.
HotelId: 39
HotelName: White Mountain Lodge & Suites
Description: Live amongst the trees in the heart of the forest. Hike along our extensive trail system. Visit the Natural Hot Springs, or enjoy our signature hot stone massage in the Cathedral of Firs. Relax in the meditation gardens, or join new friends around the communal firepit. Weekend evening entertainment on the patio features special guest musicians or poetry readings.
@search.score: 0.7334347
@search.rerankerScore: 1.9615401029586792
----------------------------------------
Caption: Book now and Save up to 30%. Central location. <em>Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood.</em> Brand new rooms. Impeccable service.
HotelId: 15
HotelName: By the Market Hotel
Description: Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service.
@search.score: 1.5502293
@search.rerankerScore: 1.9085469245910645
----------------------------------------
Press Enter to continue to the next query...
```


### Output for semantic answers

The final query returns a semantic answer. Notice that we changed the query string for this example: 'what's a good hotel for people who like to read'.

Semantic ranker can produce an answer to a query string that has the characteristics of a question. The generated answer is extracted verbatim from your content so it won't include composed content like what you might expect from a chat completion model. If the semantic answer isn't useful for your scenario, you can omit `semantic_answers`

from your code.

To produce a semantic answer, the question and answer must be closely aligned, and the model must find content that clearly answers the question. If potential answers fail to meet a confidence threshold, the model doesn't return an answer. For demonstration purposes, the question in this example is designed to get a response so that you can see the syntax.

Recall that answers are *verbatim content* pulled from your index and might be missing phrases that a user would expect to see. To get *composed answers* as generated by a chat completion model, considering using a [RAG pattern](retrieval-augmented-generation-overview) or [agentic retrieval](agentic-retrieval-overview).

```
Extractive Answers:
Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the<em> library </em>by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply.
----------------------------------------
HotelId: 1
HotelName: Stay-Kay City Hotel
Description: This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities.
@search.score: 2.0361428
@search.rerankerScore: 2.124817371368408
----------------------------------------
HotelId: 16
HotelName: Double Sanctuary Resort
Description: 5 star Luxury Hotel - Biggest Rooms in the city. #1 Hotel in the area listed by Traveler magazine. Free WiFi, Flexible check in/out, Fitness Center & espresso in room.
@search.score: 3.759768
@search.rerankerScore: 2.0705394744873047
----------------------------------------
HotelId: 38
HotelName: Lakeside B & B
Description: Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply.
@search.score: 0.7308748
@search.rerankerScore: 2.041472911834717
----------------------------------------
HotelId: 2
HotelName: Old Century Hotel
Description: The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music.
@search.score: 3.391012
@search.rerankerScore: 2.0231292247772217
----------------------------------------
HotelId: 15
HotelName: By the Market Hotel
Description: Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service.
@search.score: 1.3198771
@search.rerankerScore: 2.021622657775879
----------------------------------------
```


In this quickstart, you learn how to use [semantic ranking](semantic-search-overview) by adding a semantic configuration to a search index and adding semantic parameters to a query. You can use the hotels-sample-index or one of your own.

In Azure AI Search, semantic ranking is query-side functionality that uses machine reading comprehension from Microsoft to rescore search results, promoting the most semantically relevant matches to the top of the list. Depending on the content and the query, semantic ranking can [significantly improve search relevance](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/azure-cognitive-search-outperforming-vector-search-with-hybrid/ba-p/3929167) with minimal developer effort.

You can add a semantic configuration to an existing index with no rebuild requirement. Semantic ranking is most effective on text that's informational or descriptive.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).A

[new or existing index](search-how-to-create-search-index)with descriptive or verbose text fields that are attributed as retrievable. This quickstart assumes the[hotels-sample-index](search-get-started-portal).

## Configure access

You can connect to your Azure AI Search service using API keys or Microsoft Entra ID with role assignments. Keys are easier to start with, but roles are more secure. For more information, see [Connect to Azure AI Search using roles](search-security-rbac).

To configure role-based access:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Settings**>**Keys**.Under

**API Access control**, select**Role-based access control**or**Both**if you need time to transition clients to role-based access.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Assign the

**Search Service Contributor**and**Search Index Data Contributor**roles to your user account.

## Start with an index

This quickstart assumes an existing index and modifies it to include a semantic configuration. We recommend the [hotels-sample-index](search-get-started-portal) that you can create in minutes using an Azure portal wizard.

To start with an existing index:

Sign in to the

[Azure portal](https://portal.azure.com/)and find your search service.Under

**Search management**>**Indexes**, select the hotels-sample-index.Select

**Semantic configurations**to ensure the index doesn't have a semantic configuration.Select

**Search explorer**, and then select the**JSON view**.Paste the following JSON into the query editor.

`{ "search": "walking distance to live music", "select": "HotelId, HotelName, Description", "count": true }`

Select

**Search**to run the query.This query is a keyword search. The response should be similar to the following example, as scored by the default BM25 L1 ranker for full-text search.

For readability, the example only selects the

`HotelId`

,`HotelName`

, and`Description`

fields. The results contain verbatim matches on the query terms (`walking`

,`distance`

,`live`

,`music`

) or linguistic variants (`walk`

,`living`

).`"@odata.count": 13, "value": [ { "@search.score": 5.5153193, "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music." }, { "@search.score": 5.074317, "HotelId": "24", "HotelName": "Uptown Chic Hotel", "Description": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance." }, { "@search.score": 4.8959594, "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Cliff Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience." }, { "@search.score": 2.5966604, "HotelId": "35", "HotelName": "Bellevue Suites", "Description": "Comfortable city living in the very center of downtown Bellevue. Newly reimagined, this hotel features apartment-style suites with sleeping, living and work spaces. Located across the street from the Light Rail to downtown. Free shuttle to the airport." }, { "@search.score": 2.566386, "HotelId": "47", "HotelName": "Country Comfort Inn", "Description": "Situated conveniently at the north end of the village, the inn is just a short walk from the lake, offering reasonable rates and all the comforts home inlcuding living room suites and functional kitchens. Pets are welcome." }, { "@search.score": 2.2405157, "HotelId": "9", "HotelName": "Smile Up Hotel", "Description": "Experience the fresh, modern downtown. Enjoy updated rooms, bold style & prime location. Don't miss our weekend live music series featuring who's new/next on the scene." }, { "@search.score": 2.1737604, "HotelId": "8", "HotelName": "Foot Happy Suites", "Description": "Downtown in the heart of the business district. Close to everything. Leave your car behind and walk to the park, shopping, and restaurants. Or grab one of our bikes and take your explorations a little further." }, { "@search.score": 2.0364518, "HotelId": "31", "HotelName": "Country Residence Hotel", "Description": "All of the suites feature full-sized kitchens stocked with cookware, separate living and sleeping areas and sofa beds. Some of the larger rooms have fireplaces and patios or balconies. Experience real country hospitality in the heart of bustling Nashville. The most vibrant music scene in the world is just outside your front door." }, { "@search.score": 1.7595702, "HotelId": "49", "HotelName": "Swirling Currents Hotel", "Description": "Spacious rooms, glamorous suites and residences, rooftop pool, walking access to shopping, dining, entertainment and the city center. Each room comes equipped with a microwave, a coffee maker and a minifridge. In-room entertainment includes complimentary W-Fi and flat-screen TVs. " }, { "@search.score": 1.5502293, "HotelId": "15", "HotelName": "By the Market Hotel", "Description": "Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service." }, { "@search.score": 1.3302404, "HotelId": "42", "HotelName": "Rock Bottom Resort & Campground", "Description": "Rock Bottom is nestled on 20 unspoiled acres on a private cove of Rock Bottom Lake. We feature both lodging and campground accommodations to suit just about every taste. Even though we are out of the traffic of the city, getting there is only a short drive away." }, { "@search.score": 0.9050383, "HotelId": "38", "HotelName": "Lakeside B & B", "Description": "Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply." }, { "@search.score": 0.7334347, "HotelId": "39", "HotelName": "White Mountain Lodge & Suites", "Description": "Live amongst the trees in the heart of the forest. Hike along our extensive trail system. Visit the Natural Hot Springs, or enjoy our signature hot stone massage in the Cathedral of Firs. Relax in the meditation gardens, or join new friends around the communal firepit. Weekend evening entertainment on the patio features special guest musicians or poetry readings." } ]`


This query shows how the response looks *before* semantic ranking is applied. Later, you can run the same query after semantic ranking is configured to see how the response changes.

Tip

You can add a semantic configuration in the Azure portal. However, if you want to learn how to add a semantic configuration programmatically, continue with this quickstart.

## Set up the client

In this quickstart, you use an IDE and the [ @azure/search-documents](https://www.npmjs.com/package/@azure/search-documents) client library to add semantic ranking to an existing search index.

The quickstart assumes the following is available on your computer:

[Visual Studio Code](https://code.visualstudio.com/)for this quickstart.[Node.js](https://nodejs.org/)(LTS) for running the sample.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-javascript-samples/tree/main/quickstart-semantic-ranking-js) to start with a finished project or follow these steps to create your own.

### Set up local development environment

Start Visual Studio Code in a new directory.

`mkdir semantic-ranking-quickstart && cd semantic-ranking-quickstart code .`

Create a new package for ESM modules in your project directory.

`npm init -y npm pkg set type=module`

Install packages, including

[azure-search-documents](/en-us/javascript/api/%40azure/search-documents).`npm install @azure/identity @azure/search-documents dotenv`

Create

`.env`

, and provide your search service endpoint. You can get the endpoint from the Azure portal on the search service**Overview**page.`AZURE_SEARCH_ENDPOINT=YOUR-SEARCH-SERVICE-ENDPOINT AZURE_SEARCH_INDEX_NAME=hotels-sample-index SEMANTIC_CONFIGURATION_NAME=semantic-config`

Create a

`src`

directory in your project directory.`mkdir src`


### Sign in to Azure

If you signed in to the [Azure portal](https://portal.azure.com), you're signed into Azure. If you aren't sure, use the Azure CLI or Azure PowerShell to log in: `az login`

or `az connect`

. If you have multiple tenants and subscriptions, see [Quickstart: Connect without keys](search-get-started-rbac) for help on how to connect.

## Create a common authentication file

Create a file in `./src`

called `config.ts`

to read the `.env`

file and hold the environment variables and authentication credential. Copy in the following code; don't change it. This file will be used by all the other files in this quickstart.

```
import { DefaultAzureCredential } from "@azure/identity";
// Configuration - use environment variables
export const searchEndpoint = process.env.AZURE_SEARCH_ENDPOINT || "PUT-YOUR-SEARCH-SERVICE-ENDPOINT-HERE";
export const indexName = process.env.AZURE_SEARCH_INDEX_NAME || "hotels-sample-index";
export const semanticConfigurationName = process.env.SEMANTIC_CONFIGURATION_NAME || "semantic-config";
// Create credential
export const credential = new DefaultAzureCredential();
console.log(`Using Azure Search endpoint: ${searchEndpoint}`);
console.log(`Using index name: ${indexName}\n\n`);
```


## Get the index schema

In this section, you get settings for the existing `hotels-sample-index`

index on your search service.

Create a file in

`./src`

called`getIndexSettings.js`

and copy in the following code.`import { SearchIndexClient } from "@azure/search-documents"; import { searchEndpoint, indexName, credential } from "./config.js"; const indexClient = new SearchIndexClient(searchEndpoint, credential); console.log('Getting semantic search index settings...'); // Get the existing schema const index = await indexClient.getIndex(indexName); console.log(`Index name: ${index.name}`); console.log(`Number of fields: ${index.fields.length}`); for(const field of index.fields) { console.log(`Field: ${field.name}, Type: ${field.type}, Searchable: ${field.searchable}`); } if(index.semanticSearch && index.semanticSearch.configurations) { console.log(`Semantic search configurations: ${index.semanticSearch.configurations.length}`); for(const config of index.semanticSearch.configurations) { console.log(`Configuration name: ${config.name}`); console.log(`Title field: ${config.prioritizedFields.titleField?.name}`); } } else { console.log("No semantic configuration exists for this index."); }`

Run the code.

`node -r dotenv/config src/getIndexSettings.js`

Output is the name of the index, list of fields, and a statement indicating whether a semantic configuration exists. For the purposes of this quickstart, the message should say

`No semantic configuration exists for this index`

.

## Update the index with a semantic configuration

Create a file in

`./src`

called`updateIndexSettings.js`

and copy in the following code to add a semantic configuration to the existing`hotels-sample-index`

index on your search service. No search documents are deleted by this operation and your index is still operational after the configuration is added.`import { SearchIndexClient } from "@azure/search-documents"; import { searchEndpoint, indexName, credential, semanticConfigurationName } from "./config.js"; try { const indexClient = new SearchIndexClient(searchEndpoint, credential); const existingIndex = await indexClient.getIndex(indexName); const fields = { titleField: { name: "HotelName" }, keywordsFields: [{ name: "Tags" }], contentFields: [{ name: "Description" }] }; const newSemanticConfiguration = { name: semanticConfigurationName, prioritizedFields: fields }; // Add the new semantic configuration to the existing index if (existingIndex.semanticSearch && existingIndex.semanticSearch.configurations) { existingIndex.semanticSearch.configurations.push(newSemanticConfiguration); } else { const configExists = existingIndex.semanticSearch?.configurations?.some( config => config.name === semanticConfigurationName ); if (!configExists) { existingIndex.semanticSearch = { configurations: [newSemanticConfiguration] }; } } await indexClient.createOrUpdateIndex(existingIndex); const updatedIndex = await indexClient.getIndex(indexName); console.log(`Semantic configurations:`); console.log("-".repeat(40)); if (updatedIndex.semanticSearch && updatedIndex.semanticSearch.configurations) { for (const config of updatedIndex.semanticSearch.configurations) { console.log(`Configuration name: ${config.name}`); console.log(`Title field: ${config.prioritizedFields.titleField?.name}`); console.log(`Keywords fields: ${config.prioritizedFields.keywordsFields?.map(f => f.name).join(", ")}`); console.log(`Content fields: ${config.prioritizedFields.contentFields?.map(f => f.name).join(", ")}`); console.log("-".repeat(40)); } } else { console.log("No semantic configurations found."); } console.log("Semantic configuration updated successfully."); } catch (error) { console.error("Error updating semantic configuration:", error); }`

Run the code.

`node -r dotenv/config src/updateIndexSettings.js`

Output is the semantic configuration you just added,

`Semantic configuration updated successfully.`

.

## Run semantic queries

Once the `hotels-sample-index`

index has a semantic configuration, you can run queries that include semantic parameters.

Create a file in

`./src`

called`semanticQuery.js`

and copy in the following code to create a semantic query of the index. This is the minimum requirement for invoking semantic ranking.`import { SearchClient } from "@azure/search-documents"; import { credential, searchEndpoint, indexName, semanticConfigurationName } from "./config.js"; const searchClient = new SearchClient( searchEndpoint, indexName, credential ); const results = await searchClient.search("walking distance to live music", { queryType: "semantic", semanticSearchOptions: { configurationName: semanticConfigurationName }, select: ["HotelId", "HotelName", "Description"] }); let rowNumber = 1; for await (const result of results.results) { // Log each result const doc = result.document; const score = result.score; const rerankerScoreDisplay = result.rerankerScore; console.log(`Search result #${rowNumber++}:`); console.log(` Re-ranker Score: ${rerankerScoreDisplay}`); console.log(` HotelId: ${doc.HotelId}`); console.log(` HotelName: ${doc.HotelName}`); console.log(` Description: ${doc.Description || 'N/A'}\n`); }`

Run the code.

`node -r dotenv/config src/semanticQuery.js`

Output should consist of 13 documents, ordered by the

`rerankerScoreDisplay`

.

### Return captions

Optionally, you can add captions to extract portions of the text and apply hit highlighting to the important terms and phrases. This query adds captions.

Create a file in

`./src`

called`semanticQueryReturnCaptions.js`

and copy in the following code to add captions to the query.`import { SearchClient } from "@azure/search-documents"; import { credential, searchEndpoint, indexName, semanticConfigurationName } from "./config.js"; const searchClient = new SearchClient( searchEndpoint, indexName, credential ); console.log(`Using semantic configuration: ${semanticConfigurationName}`); console.log("Search query: walking distance to live music"); const results = await searchClient.search("walking distance to live music", { queryType: "semantic", semanticSearchOptions: { configurationName: semanticConfigurationName, captions: { captionType: "extractive", highlight: true } }, select: ["HotelId", "HotelName", "Description"], }); console.log(`Found ${results.count} results with semantic search\n`); let rowNumber = 1; for await (const result of results.results) { // Log each result const doc = result.document; const rerankerScoreDisplay = result.rerankerScore; console.log(`Search result #${rowNumber++}:`); console.log(` Re-ranker Score: ${rerankerScoreDisplay}`); console.log(` HotelName: ${doc.HotelName}`); console.log(` Description: ${doc.Description || 'N/A'}\n`); // Caption handling with better debugging const captions = result.captions; if (captions && captions.length > 0) { const caption = captions[0]; if (caption.highlights) { console.log(` Caption with highlights: ${caption.highlights}`); } else if (caption.text) { console.log(` Caption text: ${caption.text}`); } else { console.log(` Caption exists but has no text or highlights content`); } } else { console.log(" No captions found for this result"); } console.log("-".repeat(60)); }`

Run the code.

`node -r dotenv/config src/semanticQueryReturnCaptions.js`

Output should include a new caption element alongside search field. Captions are the most relevant passages in a result. If your index includes larger chunks of text, a caption is helpful for extracting the most interesting sentences.

`Search result #1: Re-ranker Score: 2.613231658935547 HotelName: Uptown Chic Hotel Description: Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance. Caption with highlights: Chic hotel near the city. High-rise hotel in downtown, within walking distance to<em> theaters, </em>art galleries, restaurants and shops. Visit<em> Seattle Art Museum </em>by day, and then head over to<em> Benaroya Hall </em>to catch the evening's concert performance.`


### Return semantic answers

In this final query, return semantic answers.

Semantic ranker can produce an answer to a query string that has the characteristics of a question. The generated answer is extracted verbatim from your content so it won't include composed content like what you might expect from a chat completion model. If the semantic answer isn't useful for your scenario, you can omit `semantic_answers`

from your code.

To produce a semantic answer, the question and answer must be closely aligned, and the model must find content that clearly answers the question. If potential answers fail to meet a confidence threshold, the model doesn't return an answer. For demonstration purposes, the question in this example is designed to get a response so that you can see the syntax.

Create a file in

`./src`

called`semanticAnswer.js`

and copy in the following code to get semantic answers.`import { SearchClient } from "@azure/search-documents"; import { credential, searchEndpoint, indexName, semanticConfigurationName } from "./config.js"; const searchClient = new SearchClient( searchEndpoint, indexName, credential ); const results = await searchClient.search("What's a good hotel for people who like to read", { queryType: "semantic", semanticSearchOptions: { configurationName: semanticConfigurationName, captions: { captionType: "extractive" }, answers: { answerType: "extractive" } }, select: ["HotelName", "Description", "Category"] }); console.log(`Answers:\n\n`); let rowNumber = 1; // Extract semantic answers from the search results const semanticAnswers = results.answers; for (const answer of semanticAnswers || []) { console.log(`Semantic answer result #${rowNumber++}:`); if (answer.highlights) { console.log(`Semantic Answer: ${answer.highlights}`); } else { console.log(`Semantic Answer: ${answer.text}`); } console.log(`Semantic Answer Score: ${answer.score}\n\n`); } console.log(`Search Results:\n\n`); rowNumber = 1; // Iterate through the search results for await (const result of results.results) { // Log each result const doc = result.document; const rerankerScoreDisplay = result.rerankerScore; console.log(`Search result #${rowNumber++}:`); console.log(`${rerankerScoreDisplay}`); console.log(`${doc.HotelName}`); console.log(`${doc.Description || 'N/A'}`); const captions = result.captions; if (captions && captions.length > 0) { const caption = captions[0]; if (caption.highlights) { console.log(`Caption: ${caption.highlights}\n`); } else { console.log(`Caption: ${caption.text}\n`); } } }`

Run the code.

`node -r dotenv/config src/semanticAnswer.js`

Output should look similar to the following example, where the best answer to question is pulled from one of the results.

Recall that answers are

*verbatim content*pulled from your index and might be missing phrases that a user would expect to see. To get*composed answers*as generated by a chat completion model, considering using a[RAG pattern](retrieval-augmented-generation-overview)or[agentic retrieval](agentic-retrieval-overview).`Semantic answer result #1: Semantic Answer: Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the<em> library </em>by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply. Semantic Answer Score: 0.9829999804496765`


In this quickstart, you learn how to use [semantic ranking](semantic-search-overview) by adding a semantic configuration to a search index and adding semantic parameters to a query. You can use the hotels-sample-index or one of your own.

In Azure AI Search, semantic ranking is query-side functionality that uses machine reading comprehension from Microsoft to rescore search results, promoting the most semantically relevant matches to the top of the list. Depending on the content and the query, semantic ranking can [significantly improve search relevance](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/azure-cognitive-search-outperforming-vector-search-with-hybrid/ba-p/3929167) with minimal developer effort.

You can add a semantic configuration to an existing index with no rebuild requirement. Semantic ranking is most effective on text that's informational or descriptive.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).A

[new or existing index](search-how-to-create-search-index)with descriptive or verbose text fields that are attributed as retrievable. This quickstart assumes the[hotels-sample-index](search-get-started-portal).

## Configure access

You can connect to your Azure AI Search service using API keys or Microsoft Entra ID with role assignments. Keys are easier to start with, but roles are more secure. For more information, see [Connect to Azure AI Search using roles](search-security-rbac).

To configure role-based access:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Settings**>**Keys**.Under

**API Access control**, select**Role-based access control**or**Both**if you need time to transition clients to role-based access.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Assign the

**Search Service Contributor**and**Search Index Data Contributor**roles to your user account.

## Start with an index

This quickstart assumes an existing index and modifies it to include a semantic configuration. We recommend the [hotels-sample-index](search-get-started-portal) that you can create in minutes using an Azure portal wizard.

To start with an existing index:

Sign in to the

[Azure portal](https://portal.azure.com/)and find your search service.Under

**Search management**>**Indexes**, select the hotels-sample-index.Select

**Semantic configurations**to ensure the index doesn't have a semantic configuration.Select

**Search explorer**, and then select the**JSON view**.Paste the following JSON into the query editor.

`{ "search": "walking distance to live music", "select": "HotelId, HotelName, Description", "count": true }`

Select

**Search**to run the query.This query is a keyword search. The response should be similar to the following example, as scored by the default BM25 L1 ranker for full-text search.

For readability, the example only selects the

`HotelId`

,`HotelName`

, and`Description`

fields. The results contain verbatim matches on the query terms (`walking`

,`distance`

,`live`

,`music`

) or linguistic variants (`walk`

,`living`

).`"@odata.count": 13, "value": [ { "@search.score": 5.5153193, "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music." }, { "@search.score": 5.074317, "HotelId": "24", "HotelName": "Uptown Chic Hotel", "Description": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance." }, { "@search.score": 4.8959594, "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Cliff Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience." }, { "@search.score": 2.5966604, "HotelId": "35", "HotelName": "Bellevue Suites", "Description": "Comfortable city living in the very center of downtown Bellevue. Newly reimagined, this hotel features apartment-style suites with sleeping, living and work spaces. Located across the street from the Light Rail to downtown. Free shuttle to the airport." }, { "@search.score": 2.566386, "HotelId": "47", "HotelName": "Country Comfort Inn", "Description": "Situated conveniently at the north end of the village, the inn is just a short walk from the lake, offering reasonable rates and all the comforts home inlcuding living room suites and functional kitchens. Pets are welcome." }, { "@search.score": 2.2405157, "HotelId": "9", "HotelName": "Smile Up Hotel", "Description": "Experience the fresh, modern downtown. Enjoy updated rooms, bold style & prime location. Don't miss our weekend live music series featuring who's new/next on the scene." }, { "@search.score": 2.1737604, "HotelId": "8", "HotelName": "Foot Happy Suites", "Description": "Downtown in the heart of the business district. Close to everything. Leave your car behind and walk to the park, shopping, and restaurants. Or grab one of our bikes and take your explorations a little further." }, { "@search.score": 2.0364518, "HotelId": "31", "HotelName": "Country Residence Hotel", "Description": "All of the suites feature full-sized kitchens stocked with cookware, separate living and sleeping areas and sofa beds. Some of the larger rooms have fireplaces and patios or balconies. Experience real country hospitality in the heart of bustling Nashville. The most vibrant music scene in the world is just outside your front door." }, { "@search.score": 1.7595702, "HotelId": "49", "HotelName": "Swirling Currents Hotel", "Description": "Spacious rooms, glamorous suites and residences, rooftop pool, walking access to shopping, dining, entertainment and the city center. Each room comes equipped with a microwave, a coffee maker and a minifridge. In-room entertainment includes complimentary W-Fi and flat-screen TVs. " }, { "@search.score": 1.5502293, "HotelId": "15", "HotelName": "By the Market Hotel", "Description": "Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service." }, { "@search.score": 1.3302404, "HotelId": "42", "HotelName": "Rock Bottom Resort & Campground", "Description": "Rock Bottom is nestled on 20 unspoiled acres on a private cove of Rock Bottom Lake. We feature both lodging and campground accommodations to suit just about every taste. Even though we are out of the traffic of the city, getting there is only a short drive away." }, { "@search.score": 0.9050383, "HotelId": "38", "HotelName": "Lakeside B & B", "Description": "Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply." }, { "@search.score": 0.7334347, "HotelId": "39", "HotelName": "White Mountain Lodge & Suites", "Description": "Live amongst the trees in the heart of the forest. Hike along our extensive trail system. Visit the Natural Hot Springs, or enjoy our signature hot stone massage in the Cathedral of Firs. Relax in the meditation gardens, or join new friends around the communal firepit. Weekend evening entertainment on the patio features special guest musicians or poetry readings." } ]`


This query shows how the response looks *before* semantic ranking is applied. Later, you can run the same query after semantic ranking is configured to see how the response changes.

Tip

You can add a semantic configuration in the Azure portal. However, if you want to learn how to add a semantic configuration programmatically, continue with this quickstart.

## Set up the client

In this quickstart, you use an IDE and the [ Azure AI Search Java SDK](https://search.maven.org/artifact/com.azure/azure-search-documents) client library to add semantic ranking to an existing search index.

The quickstart assumes the following is available on your computer:

[Visual Studio Code](https://code.visualstudio.com/)with Java extensions or IntelliJ IDEA[Java 21 (LTS)](/en-us/java/openjdk/install).[Maven](https://maven.apache.org/download.cgi).

### Set up local development environment

Create a new Maven project directory.

`mkdir semantic-ranking-quickstart && cd semantic-ranking-quickstart code .`

Create a

`pom.xml`

file with required dependencies.`<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd"> <modelVersion>4.0.0</modelVersion> <groupId>com.azure.search</groupId> <artifactId>semantic-ranking-quickstart</artifactId> <version>1.0-SNAPSHOT</version> <properties> <maven.compiler.source>21</maven.compiler.source> <maven.compiler.target>21</maven.compiler.target> <project.build.sourceEncoding>UTF-8</project.build.sourceEncoding> </properties> <dependencies> <dependency> <groupId>com.azure</groupId> <artifactId>azure-search-documents</artifactId> <version>11.7.8</version> </dependency> <dependency> <groupId>com.azure</groupId> <artifactId>azure-identity</artifactId> <version>1.17.0</version> </dependency> </dependencies> </project>`

Compile the project to resolve the dependencies.

`mvn compile`

Create the source directory structure.

`mkdir -p src/main/java/com/azure/search/quickstart mkdir -p src/main/resources`

Create an

`application.properties`

file in the`src/main/resources`

directory and provide your search service endpoint. You can get the endpoint from the Azure portal on the search service**Overview**page.`azure.search.endpoint=YOUR-SEARCH-SERVICE-ENDPOINT azure.search.index.name=hotels-sample-index semantic.configuration.name=semantic-config`


### Sign in to Azure

If you signed in to the [Azure portal](https://portal.azure.com), you're signed into Azure. If you aren't sure, use the Azure CLI to log in: `az login`

. If you have multiple tenants and subscriptions, see [Quickstart: Connect without keys](search-get-started-rbac) for help on how to connect.

## Create a common configuration class

Create a `SearchConfig.java`

file in the `src/main/java/com/azure/search/quickstart`

directory to read the properties file and hold the configuration values and authentication credential.

```
package com.azure.search.quickstart;
import com.azure.identity.DefaultAzureCredential;
import com.azure.identity.DefaultAzureCredentialBuilder;
import java.io.IOException;
import java.io.InputStream;
import java.util.Properties;
public class SearchConfig {
private static final Properties properties = new Properties();
static {
try (InputStream input = SearchConfig.class.getClassLoader()
.getResourceAsStream("application.properties")) {
properties.load(input);
} catch (IOException e) {
throw new RuntimeException(
"Failed to load application.properties", e);
}
}
public static final String SEARCH_ENDPOINT =
properties.getProperty("azure.search.endpoint");
public static final String INDEX_NAME =
properties.getProperty("azure.search.index.name");
public static final String SEMANTIC_CONFIG_NAME =
properties.getProperty("semantic.configuration.name");
public static final DefaultAzureCredential CREDENTIAL =
new DefaultAzureCredentialBuilder().build();
static {
System.out.println("Using Azure Search endpoint: " + SEARCH_ENDPOINT);
System.out.println("Using index name: " + INDEX_NAME + "\n");
}
}
```


## Get the index schema

In this section, you get settings for the existing `hotels-sample-index`

index on your search service.

Create a

`GetIndexSettings.java`

file in the`src/main/java/com/azure/search/quickstart`

directory.`package com.azure.search.quickstart; import com.azure.search.documents.indexes.SearchIndexClientBuilder; import com.azure.search.documents.indexes.models.SearchField; import com.azure.search.documents.indexes.models.SearchIndex; import com.azure.search.documents.indexes.models.SemanticConfiguration; import com.azure.search.documents.indexes.models.SemanticField; import com.azure.search.documents.indexes.models.SemanticSearch; public class GetIndexSettings { public static void main(String[] args) { var indexClient = new SearchIndexClientBuilder() .endpoint(SearchConfig.SEARCH_ENDPOINT) .credential(SearchConfig.CREDENTIAL) .buildClient(); System.out.println("Getting semantic search index settings..."); SearchIndex index = indexClient.getIndex(SearchConfig.INDEX_NAME); System.out.println("Index name: " + index.getName()); System.out.println("Number of fields: " + index.getFields().size()); for (SearchField field : index.getFields()) { System.out.printf("Field: %s, Type: %s, Searchable: %s%n", field.getName(), field.getType(), field.isSearchable()); } SemanticSearch semanticSearch = index.getSemanticSearch(); if (semanticSearch != null && semanticSearch.getConfigurations() != null) { System.out.println("Semantic search configurations: " + semanticSearch.getConfigurations().size()); for (SemanticConfiguration config : semanticSearch.getConfigurations()) { System.out.println("Configuration name: " + config.getName()); SemanticField titleField = config.getPrioritizedFields().getTitleField(); if (titleField != null) { System.out.println("Title field: " + titleField.getFieldName()); } } } else { System.out.println( "No semantic configuration exists for this index."); } System.exit(0); } }`

Compile and run the code.

`mvn compile exec:java -Dexec.mainClass="com.azure.search.quickstart.GetIndexSettings"`

Output is the name of the index, list of fields, and a statement indicating whether a semantic configuration exists. For the purposes of this quickstart, the message should say

`No semantic configuration exists for this index`

.

## Update the index with a semantic configuration

Create an

`UpdateIndexSettings.java`

file in the`src/main/java/com/azure/search/quickstart`

directory to add a semantic configuration to the existing`hotels-sample-index`

index on your search service.`package com.azure.search.quickstart; import com.azure.search.documents.indexes.SearchIndexClientBuilder; import com.azure.search.documents.indexes.models.SearchIndex; import com.azure.search.documents.indexes.models.SemanticConfiguration; import com.azure.search.documents.indexes.models.SemanticField; import com.azure.search.documents.indexes.models.SemanticPrioritizedFields; import com.azure.search.documents.indexes.models.SemanticSearch; import java.util.ArrayList; import java.util.List; public class UpdateIndexSettings { public static void main(String[] args) { try { var indexClient = new SearchIndexClientBuilder() .endpoint(SearchConfig.SEARCH_ENDPOINT) .credential(SearchConfig.CREDENTIAL) .buildClient(); SearchIndex existingIndex = indexClient.getIndex(SearchConfig.INDEX_NAME); // Create prioritized fields for semantic configuration var prioritizedFields = new SemanticPrioritizedFields() .setTitleField(new SemanticField("HotelName")) .setKeywordsFields(List.of(new SemanticField("Tags"))) .setContentFields(List.of(new SemanticField("Description"))); var newSemanticConfiguration = new SemanticConfiguration( SearchConfig.SEMANTIC_CONFIG_NAME, prioritizedFields); // Add the semantic configuration to the index SemanticSearch semanticSearch = existingIndex.getSemanticSearch(); if (semanticSearch == null) { semanticSearch = new SemanticSearch(); existingIndex.setSemanticSearch(semanticSearch); } List<SemanticConfiguration> configurations = semanticSearch.getConfigurations(); if (configurations == null) { configurations = new ArrayList<>(); semanticSearch.setConfigurations(configurations); } // Check if configuration already exists boolean configExists = configurations.stream() .anyMatch(config -> SearchConfig.SEMANTIC_CONFIG_NAME .equals(config.getName())); if (!configExists) { configurations.add(newSemanticConfiguration); } indexClient.createOrUpdateIndex(existingIndex); SearchIndex updatedIndex = indexClient.getIndex(SearchConfig.INDEX_NAME); System.out.println("Semantic configurations:"); System.out.println("-".repeat(40)); SemanticSearch updatedSemanticSearch = updatedIndex.getSemanticSearch(); if (updatedSemanticSearch != null && updatedSemanticSearch.getConfigurations() != null) { for (SemanticConfiguration config : updatedSemanticSearch.getConfigurations()) { System.out.println("Configuration name: " + config.getName()); SemanticPrioritizedFields fields = config.getPrioritizedFields(); if (fields.getTitleField() != null) { System.out.println("Title field: " + fields.getTitleField().getFieldName()); } if (fields.getKeywordsFields() != null) { List<String> keywords = fields.getKeywordsFields().stream() .map(SemanticField::getFieldName) .toList(); System.out.println("Keywords fields: " + String.join(", ", keywords)); } if (fields.getContentFields() != null) { List<String> content = fields.getContentFields().stream() .map(SemanticField::getFieldName) .toList(); System.out.println("Content fields: " + String.join(", ", content)); } System.out.println("-".repeat(40)); } } else { System.out.println("No semantic configurations found."); } System.out.println("Semantic configuration updated successfully."); System.exit(0); } catch (Exception e) { System.err.println("Error updating semantic configuration: " + e.getMessage()); } } }`

Compile and run the code.

`mvn compile exec:java -Dexec.mainClass="com.azure.search.quickstart.UpdateIndexSettings"`

Output is the semantic configuration you just added,

`Semantic configuration updated successfully.`

.

## Run semantic queries

After the `hotels-sample-index`

index has a semantic configuration, you can run queries that include semantic parameters.

Create a

`SemanticQuery.java`

file in the`src/main/java/com/azure/search/quickstart`

directory to create a semantic query of the index.`package com.azure.search.quickstart; import com.azure.search.documents.SearchClientBuilder; import com.azure.search.documents.SearchDocument; import com.azure.search.documents.models.QueryType; import com.azure.search.documents.models.SearchOptions; import com.azure.search.documents.models.SearchResult; import com.azure.search.documents.models.SemanticSearchOptions; import com.azure.search.documents.util.SearchPagedIterable; public class SemanticQuery { public static void main(String[] args) { var searchClient = new SearchClientBuilder() .endpoint(SearchConfig.SEARCH_ENDPOINT) .indexName(SearchConfig.INDEX_NAME) .credential(SearchConfig.CREDENTIAL) .buildClient(); var searchOptions = new SearchOptions() .setQueryType(QueryType.SEMANTIC) .setSemanticSearchOptions(new SemanticSearchOptions() .setSemanticConfigurationName(SearchConfig.SEMANTIC_CONFIG_NAME)) .setSelect("HotelId", "HotelName", "Description"); SearchPagedIterable results = searchClient.search( "walking distance to live music", searchOptions, null); int rowNumber = 1; for (SearchResult result : results) { var document = result.getDocument(SearchDocument.class); double rerankerScore = result.getSemanticSearch().getRerankerScore(); System.out.printf("Search result #%d:%n", rowNumber++); System.out.printf(" Re-ranker Score: %.2f%n", rerankerScore); System.out.printf(" HotelId: %s%n", document.get("HotelId")); System.out.printf(" HotelName: %s%n", document.get("HotelName")); System.out.printf(" Description: %s%n%n", document.get("Description") != null ? document.get("Description") : "N/A"); } System.exit(0); } }`

Compile and run the code.

`mvn compile exec:java -Dexec.mainClass="com.azure.search.quickstart.SemanticQuery"`

Output should consist of 13 documents, ordered by the reranker score.


### Return captions

Optionally, you can add captions to extract portions of the text and apply hit highlighting to the important terms and phrases.

Create a

`SemanticQueryWithCaptions.java`

file in the`src/main/java/com/azure/search/quickstart`

directory.`package com.azure.search.quickstart; import com.azure.search.documents.SearchClientBuilder; import com.azure.search.documents.SearchDocument; import com.azure.search.documents.models.QueryCaption; import com.azure.search.documents.models.QueryCaptionResult; import com.azure.search.documents.models.QueryCaptionType; import com.azure.search.documents.models.QueryType; import com.azure.search.documents.models.SearchOptions; import com.azure.search.documents.models.SearchResult; import com.azure.search.documents.models.SemanticSearchOptions; import com.azure.search.documents.util.SearchPagedIterable; import java.util.List; public class SemanticQueryWithCaptions { public static void main(String[] args) { var searchClient = new SearchClientBuilder() .endpoint(SearchConfig.SEARCH_ENDPOINT) .indexName(SearchConfig.INDEX_NAME) .credential(SearchConfig.CREDENTIAL) .buildClient(); System.out.println("Using semantic configuration: " + SearchConfig.SEMANTIC_CONFIG_NAME); System.out.println("Search query: walking distance to live music"); var searchOptions = new SearchOptions() .setQueryType(QueryType.SEMANTIC) .setSemanticSearchOptions(new SemanticSearchOptions() .setSemanticConfigurationName(SearchConfig.SEMANTIC_CONFIG_NAME) .setQueryCaption(new QueryCaption(QueryCaptionType.EXTRACTIVE) .setHighlightEnabled(true))) .setSelect("HotelId", "HotelName", "Description"); SearchPagedIterable results = searchClient.search( "walking distance to live music", searchOptions, null); System.out.printf("Found results with semantic search%n%n"); int rowNumber = 1; for (SearchResult result : results) { var document = result.getDocument(SearchDocument.class); double rerankerScore = result.getSemanticSearch().getRerankerScore(); System.out.printf("Search result #%d:%n", rowNumber++); System.out.printf(" Re-ranker Score: %.2f%n", rerankerScore); System.out.printf(" HotelName: %s%n", document.get("HotelName")); System.out.printf(" Description: %s%n%n", document.get("Description") != null ? document.get("Description") : "N/A"); // Handle captions List<QueryCaptionResult> captions = result.getSemanticSearch().getQueryCaptions(); if (captions != null && !captions.isEmpty()) { QueryCaptionResult caption = captions.get(0); if (caption.getHighlights() != null && !caption.getHighlights().trim().isEmpty()) { System.out.printf(" Caption with highlights: %s%n", caption.getHighlights()); } else if (caption.getText() != null && !caption.getText().trim().isEmpty()) { System.out.printf(" Caption text: %s%n", caption.getText()); } else { System.out.println( " Caption exists but has no text or highlights content"); } } else { System.out.println(" No captions found for this result"); } System.out.println("-".repeat(60)); } System.exit(0); } }`

Compile and run the code.

`mvn compile exec:java -Dexec.mainClass="com.azure.search.quickstart.SemanticQueryWithCaptions"`

Output should include a new caption element alongside search field. Captions are the most relevant passages in a result. If your index includes larger chunks of text, a caption is helpful for extracting the most interesting sentences.

`Search result #1: Re-ranker Score: 2.613231658935547 HotelName: Uptown Chic Hotel Description: Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance. Caption with highlights: Chic hotel near the city. High-rise hotel in downtown, within walking distance to<em> theaters, </em>art galleries, restaurants and shops. Visit<em> Seattle Art Museum </em>by day, and then head over to<em> Benaroya Hall </em>to catch the evening's concert performance.`


### Return semantic answers

In this final query, return semantic answers.

Semantic ranker can produce an answer to a query string that has the characteristics of a question. The generated answer is extracted verbatim from your content so it won't include composed content like what you might expect from a chat completion model.

To produce a semantic answer, the question and answer must be closely aligned, and the model must find content that clearly answers the question. If potential answers fail to meet a confidence threshold, the model doesn't return an answer. For demonstration purposes, the question in this example is designed to get a response so that you can see the syntax.

Create a

`SemanticAnswer.java`

file in the`src/main/java/com/azure/search/quickstart`

directory.`package com.azure.search.quickstart; import com.azure.search.documents.SearchClientBuilder; import com.azure.search.documents.SearchDocument; import com.azure.search.documents.models.QueryAnswer; import com.azure.search.documents.models.QueryAnswerResult; import com.azure.search.documents.models.QueryAnswerType; import com.azure.search.documents.models.QueryCaption; import com.azure.search.documents.models.QueryCaptionResult; import com.azure.search.documents.models.QueryCaptionType; import com.azure.search.documents.models.QueryType; import com.azure.search.documents.models.SearchOptions; import com.azure.search.documents.models.SearchResult; import com.azure.search.documents.models.SemanticSearchOptions; import com.azure.search.documents.util.SearchPagedIterable; import java.util.List; public class SemanticAnswer { public static void main(String[] args) { var searchClient = new SearchClientBuilder() .endpoint(SearchConfig.SEARCH_ENDPOINT) .indexName(SearchConfig.INDEX_NAME) .credential(SearchConfig.CREDENTIAL) .buildClient(); var searchOptions = new SearchOptions() .setQueryType(QueryType.SEMANTIC) .setSemanticSearchOptions(new SemanticSearchOptions() .setSemanticConfigurationName(SearchConfig.SEMANTIC_CONFIG_NAME) .setQueryCaption(new QueryCaption(QueryCaptionType.EXTRACTIVE)) .setQueryAnswer(new QueryAnswer(QueryAnswerType.EXTRACTIVE))) .setSelect("HotelName", "Description", "Category"); SearchPagedIterable results = searchClient.search( "What's a good hotel for people who like to read", searchOptions, null); System.out.println("Answers:\n"); // Extract semantic answers List<QueryAnswerResult> semanticAnswers = results.getSemanticResults().getQueryAnswers(); int answerNumber = 1; if (semanticAnswers != null) { for (QueryAnswerResult answer : semanticAnswers) { System.out.printf("Semantic answer result #%d:%n", answerNumber++); if (answer.getHighlights() != null && !answer.getHighlights().trim().isEmpty()) { System.out.printf("Semantic Answer: %s%n", answer.getHighlights()); } else { System.out.printf("Semantic Answer: %s%n", answer.getText()); } System.out.printf("Semantic Answer Score: %.2f%n%n", answer.getScore()); } } System.out.println("Search Results:\n"); int rowNumber = 1; // Iterate through search results for (SearchResult result : results) { var document = result.getDocument(SearchDocument.class); double rerankerScore = result.getSemanticSearch().getRerankerScore(); System.out.printf("Search result #%d:%n", rowNumber++); System.out.printf("Re-ranker Score: %.2f%n", rerankerScore); System.out.printf("Hotel: %s%n", document.get("HotelName")); System.out.printf("Description: %s%n", document.get("Description") != null ? document.get("Description") : "N/A"); List<QueryCaptionResult> captions = result.getSemanticSearch().getQueryCaptions(); if (captions != null && !captions.isEmpty()) { QueryCaptionResult caption = captions.get(0); if (caption.getHighlights() != null && !caption.getHighlights().trim().isEmpty()) { System.out.printf("Caption: %s%n%n", caption.getHighlights()); } else { System.out.printf("Caption: %s%n%n", caption.getText()); } } else { System.out.println(); } } System.exit(0); } }`

Compile and run the code.

`mvn compile exec:java -Dexec.mainClass="com.azure.search.quickstart.SemanticAnswer"`

Output should look similar to the following example, where the best answer to question is pulled from one of the results.

Recall that answers are

*verbatim content*pulled from your index and might be missing phrases that a user would expect to see. To get*composed answers*as generated by a chat completion model, considering using a[RAG pattern](retrieval-augmented-generation-overview)or[agentic retrieval](agentic-retrieval-overview).`Semantic answer result #1: Semantic Answer: Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the<em> library </em>by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply. Semantic Answer Score: 0.9829999804496765`


In this quickstart, you learn how to use [semantic ranking](semantic-search-overview) by adding a semantic configuration to a search index and adding semantic parameters to a query. You can use the hotels-sample-index or one of your own.

In Azure AI Search, semantic ranking is query-side functionality that uses machine reading comprehension from Microsoft to rescore search results, promoting the most semantically relevant matches to the top of the list. Depending on the content and the query, semantic ranking can [significantly improve search relevance](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/azure-cognitive-search-outperforming-vector-search-with-hybrid/ba-p/3929167) with minimal developer effort.

You can add a semantic configuration to an existing index with no rebuild requirement. Semantic ranking is most effective on text that's informational or descriptive.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).A

[new or existing index](search-how-to-create-search-index)with descriptive or verbose text fields that are attributed as retrievable. This quickstart assumes the[hotels-sample-index](search-get-started-portal).

## Configure access

You can connect to your Azure AI Search service using API keys or Microsoft Entra ID with role assignments. Keys are easier to start with, but roles are more secure. For more information, see [Connect to Azure AI Search using roles](search-security-rbac).

To configure role-based access:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Settings**>**Keys**.Under

**API Access control**, select**Role-based access control**or**Both**if you need time to transition clients to role-based access.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Assign the

**Search Service Contributor**and**Search Index Data Contributor**roles to your user account.

## Start with an index

This quickstart assumes an existing index and modifies it to include a semantic configuration. We recommend the [hotels-sample-index](search-get-started-portal) that you can create in minutes using an Azure portal wizard.

To start with an existing index:

Sign in to the

[Azure portal](https://portal.azure.com/)and find your search service.Under

**Search management**>**Indexes**, select the hotels-sample-index.Select

**Semantic configurations**to ensure the index doesn't have a semantic configuration.Select

**Search explorer**, and then select the**JSON view**.Paste the following JSON into the query editor.

`{ "search": "walking distance to live music", "select": "HotelId, HotelName, Description", "count": true }`

Select

**Search**to run the query.This query is a keyword search. The response should be similar to the following example, as scored by the default BM25 L1 ranker for full-text search.

For readability, the example only selects the

`HotelId`

,`HotelName`

, and`Description`

fields. The results contain verbatim matches on the query terms (`walking`

,`distance`

,`live`

,`music`

) or linguistic variants (`walk`

,`living`

).`"@odata.count": 13, "value": [ { "@search.score": 5.5153193, "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music." }, { "@search.score": 5.074317, "HotelId": "24", "HotelName": "Uptown Chic Hotel", "Description": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance." }, { "@search.score": 4.8959594, "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Cliff Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience." }, { "@search.score": 2.5966604, "HotelId": "35", "HotelName": "Bellevue Suites", "Description": "Comfortable city living in the very center of downtown Bellevue. Newly reimagined, this hotel features apartment-style suites with sleeping, living and work spaces. Located across the street from the Light Rail to downtown. Free shuttle to the airport." }, { "@search.score": 2.566386, "HotelId": "47", "HotelName": "Country Comfort Inn", "Description": "Situated conveniently at the north end of the village, the inn is just a short walk from the lake, offering reasonable rates and all the comforts home inlcuding living room suites and functional kitchens. Pets are welcome." }, { "@search.score": 2.2405157, "HotelId": "9", "HotelName": "Smile Up Hotel", "Description": "Experience the fresh, modern downtown. Enjoy updated rooms, bold style & prime location. Don't miss our weekend live music series featuring who's new/next on the scene." }, { "@search.score": 2.1737604, "HotelId": "8", "HotelName": "Foot Happy Suites", "Description": "Downtown in the heart of the business district. Close to everything. Leave your car behind and walk to the park, shopping, and restaurants. Or grab one of our bikes and take your explorations a little further." }, { "@search.score": 2.0364518, "HotelId": "31", "HotelName": "Country Residence Hotel", "Description": "All of the suites feature full-sized kitchens stocked with cookware, separate living and sleeping areas and sofa beds. Some of the larger rooms have fireplaces and patios or balconies. Experience real country hospitality in the heart of bustling Nashville. The most vibrant music scene in the world is just outside your front door." }, { "@search.score": 1.7595702, "HotelId": "49", "HotelName": "Swirling Currents Hotel", "Description": "Spacious rooms, glamorous suites and residences, rooftop pool, walking access to shopping, dining, entertainment and the city center. Each room comes equipped with a microwave, a coffee maker and a minifridge. In-room entertainment includes complimentary W-Fi and flat-screen TVs. " }, { "@search.score": 1.5502293, "HotelId": "15", "HotelName": "By the Market Hotel", "Description": "Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service." }, { "@search.score": 1.3302404, "HotelId": "42", "HotelName": "Rock Bottom Resort & Campground", "Description": "Rock Bottom is nestled on 20 unspoiled acres on a private cove of Rock Bottom Lake. We feature both lodging and campground accommodations to suit just about every taste. Even though we are out of the traffic of the city, getting there is only a short drive away." }, { "@search.score": 0.9050383, "HotelId": "38", "HotelName": "Lakeside B & B", "Description": "Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply." }, { "@search.score": 0.7334347, "HotelId": "39", "HotelName": "White Mountain Lodge & Suites", "Description": "Live amongst the trees in the heart of the forest. Hike along our extensive trail system. Visit the Natural Hot Springs, or enjoy our signature hot stone massage in the Cathedral of Firs. Relax in the meditation gardens, or join new friends around the communal firepit. Weekend evening entertainment on the patio features special guest musicians or poetry readings." } ]`


This query shows how the response looks *before* semantic ranking is applied. Later, you can run the same query after semantic ranking is configured to see how the response changes.

Tip

You can add a semantic configuration in the Azure portal. However, if you want to learn how to add a semantic configuration programmatically, continue with this quickstart.

## Set up the client

In this quickstart, use a Jupyter notebook and the [ azure-search-documents](/en-us/python/api/overview/azure/search-documents-readme) library in the Azure SDK for Python to learn about semantic ranking.

We recommend [Visual Studio Code](https://code.visualstudio.com/download) with Python 3.10 or later and the [Python extension](https://code.visualstudio.com/docs/languages/python) for this quickstart.

Tip

You can [download a finished notebook](https://github.com/Azure-Samples/azure-search-python-samples/tree/main/Quickstart-Semantic-Ranking) to start with a finished project or follow these steps to create your own.

We recommend a virtual environment for this quickstart:

Start Visual Studio Code.

Open the

**semantic-ranking-quickstart.ipynb**file or create a new notebook.Open the Command Palette by using

**Ctrl+Shift+P**.Search for

**Python: Create Environment**.Select

`Venv.`

Select a Python interpreter. Choose 3.10 or later.


It can take a minute to set up. If you run into problems, see [Python environments in VS Code](https://code.visualstudio.com/docs/python/environments).

### Install packages and set environment variables

Install packages, including

[azure-search-documents](/en-us/python/api/azure-search-documents).`! pip install -r requirements.txt --quiet`

Rename

`sample.env`

to`.env`

, and provide your search service endpoint. You can get the endpoint from the Azure portal on the search service**Overview**page.`AZURE_SEARCH_ENDPOINT=https://your-search-service.search.windows.net AZURE_SEARCH_INDEX_NAME=hotels-sample-index`


### Sign in to Azure

If you signed in to the [Azure portal](https://portal.azure.com), you're signed into Azure. If you aren't sure, use the Azure CLI or Azure PowerShell to log in: `az login`

or `az connect`

. If you have multiple tenants and subscriptions, see [Quickstart: Connect without keys](search-get-started-rbac) for help on how to connect.

## Update the index

In this section, you update a search index to include a semantic configuration. The code gets the index definition from the search service and adds a semantic configuration.

Open the

[semantic-ranking-quickstart.ipynb](https://github.com/Azure-Samples/azure-search-python-samples/blob/main/Quickstart-Semantic-Ranking/semantic-ranking-quickstart.ipynb)file in Visual Studio Code or create a new file.Provide the variables used in the solution.

`# Provide variables from dotenv import load_dotenv from azure.identity import DefaultAzureCredential, get_bearer_token_provider import os load_dotenv(override=True) # Take environment variables from .env. # The following variables from your .env file are used in this notebook search_endpoint = os.environ["AZURE_SEARCH_ENDPOINT"] credential = DefaultAzureCredential() token_provider = get_bearer_token_provider(credential, "https://search.azure.com/.default") index_name = os.getenv("AZURE_SEARCH_INDEX", "hotels-sample-index")`

Create a SearchIndexClient and get the existing hotels-sample-index.

`from azure.search.documents.indexes import SearchIndexClient from azure.identity import DefaultAzureCredential import os # Initialize the client (similar to what you already have) search_endpoint = os.environ["AZURE_SEARCH_ENDPOINT"] credential = DefaultAzureCredential() index_name = "hotels-sample-index" # or use your existing index_name variable # Create the SearchIndexClient index_client = SearchIndexClient(endpoint=search_endpoint, credential=credential) try: # Get the existing index schema index = index_client.get_index(index_name) print(f"Index name: {index.name}") print(f"Number of fields: {len(index.fields)}") # Print field details for field in index.fields: print(f"Field: {field.name}, Type: {field.type}, Searchable: {field.searchable}") # Access semantic configuration if it exists if index.semantic_search and index.semantic_search.configurations: for config in index.semantic_search.configurations: print(f"Semantic config: {config.name}") if config.prioritized_fields.title_field: print(f"Title field: {config.prioritized_fields.title_field.field_name}") else: print("No semantic configuration exists for this index") except Exception as ex: print(f"Error retrieving index: {ex}")`

Run the code.

Output is the name of the index, list of fields, and a statement indicating whether a semantic configuration exists. For the purposes of this quickstart, the message should say "No semantic configuration exists for this index".

Add a semantic configuration to an existing hotels-sample-index on your search service. No search documents are deleted by this operation and your index is still operational after the configuration is added.

`# Add semantic configuration to hotels-sample-index and display updated index details from azure.search.documents.indexes.models import ( SemanticConfiguration, SemanticField, SemanticPrioritizedFields, SemanticSearch ) try: # Get the existing index existing_index = index_client.get_index(index_name) # Create a new semantic configuration new_semantic_config = SemanticConfiguration( name="semantic-config", prioritized_fields=SemanticPrioritizedFields( title_field=SemanticField(field_name="HotelName"), keywords_fields=[SemanticField(field_name="Tags")], content_fields=[SemanticField(field_name="Description")] ) ) # Add semantic configuration to the index if existing_index.semantic_search is None: existing_index.semantic_search = SemanticSearch(configurations=[new_semantic_config]) else: # Check if configuration already exists config_exists = any(config.name == "semantic-config" for config in existing_index.semantic_search.configurations) if not config_exists: existing_index.semantic_search.configurations.append(new_semantic_config) # Update the index result = index_client.create_or_update_index(existing_index) # Get the updated index and display detailed information updated_index = index_client.get_index(index_name) print("Semantic configurations:") print("-" * 40) if updated_index.semantic_search and updated_index.semantic_search.configurations: for config in updated_index.semantic_search.configurations: print(f" Configuration: {config.name}") if config.prioritized_fields.title_field: print(f" Title field: {config.prioritized_fields.title_field.field_name}") if config.prioritized_fields.keywords_fields: keywords = [kf.field_name for kf in config.prioritized_fields.keywords_fields] print(f" Keywords fields: {', '.join(keywords)}") if config.prioritized_fields.content_fields: content = [cf.field_name for cf in config.prioritized_fields.content_fields] print(f" Content fields: {', '.join(content)}") print() else: print(" No semantic configurations found") print("✅ Semantic configuration successfully added!") except Exception as ex: print(f"❌ Error adding semantic configuration: {ex}")`

Run the code.

Output is the semantic configuration you just added.


## Run semantic queries

Once the index has a semantic configuration, you can run queries that include semantic parameters.

Create a SearchClient and a query request that includes the semantic query type and the semantic configuration. This is the minimum requirement for invoking semantic ranking.

`# Set up the search client search_client = SearchClient(endpoint=search_endpoint, index_name=index_name, credential=credential) # Runs a semantic query (runs a BM25-ranked query, rescoring and promoting the most semantically relevant matches to the top) results = search_client.search(query_type='semantic', semantic_configuration_name='semantic-config', search_text="walking distance to live music", select='HotelId,HotelName,Description', query_caption='extractive') for result in results: print(result["@search.reranker_score"]) print(result["HotelId"]) print(result["HotelName"]) print(f"Description: {result['Description']}")`

Run the code.

Output should consist of 13 documents, ordered by the

`"@search.reranker_score"`

.

### Return captions

Optionally, you can add captions to extract portions of the text and apply hit highlighting to the important terms and phrases. This query adds captions.

Add

`captions`

to the query.`# Runs a semantic query that returns captions results = search_client.search(query_type='semantic', semantic_configuration_name='semantic-config', search_text="walking distance to live music", select='HotelName,HotelId,Description', query_caption='extractive') for result in results: print(result["@search.reranker_score"]) print(result["HotelId"]) print(result["HotelName"]) print(f"Description: {result['Description']}") captions = result["@search.captions"] if captions: caption = captions[0] if caption.highlights: print(f"Caption: {caption.highlights}\n") else: print(f"Caption: {caption.text}\n")`

Run the code.

Output should include a new caption element alongside search field. Captions are the most relevant passages in a result. If your index includes larger chunks of text, a caption is helpful for extracting the most interesting sentences.

`2.613231658935547 24 Uptown Chic Hotel Description: Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance. Caption: Chic hotel near the city. High-rise hotel in downtown, within walking distance to<em> theaters, </em>art galleries, restaurants and shops. Visit<em> Seattle Art Museum </em>by day, and then head over to<em> Benaroya Hall </em>to catch the evening's concert performance.`


### Return semantic answers

In this final query, return semantic answers.

Semantic ranker can produce an answer to a query string that has the characteristics of a question. The generated answer is extracted verbatim from your content so it won't include composed content like what you might expect from a chat completion model. If the semantic answer isn't useful for your scenario, you can omit `semantic_answers`

from your code.

To produce a semantic answer, the question and answer must be closely aligned, and the model must find content that clearly answers the question. If potential answers fail to meet a confidence threshold, the model doesn't return an answer. For demonstration purposes, the question in this example is designed to get a response so that you can see the syntax.

Add

`answers`

to the query.`# Run a semantic query that returns semantic answers results = search_client.search(query_type='semantic', semantic_configuration_name='semantic-config', search_text="what's a good hotel for people who like to read", select='HotelName,Description,Category', query_caption='extractive', query_answer="extractive",) semantic_answers = results.get_answers() for answer in semantic_answers: if answer.highlights: print(f"Semantic Answer: {answer.highlights}") else: print(f"Semantic Answer: {answer.text}") print(f"Semantic Answer Score: {answer.score}\n") for result in results: print(result["@search.reranker_score"]) print(result["HotelName"]) print(f"Description: {result['Description']}") captions = result["@search.captions"] if captions: caption = captions[0] if caption.highlights: print(f"Caption: {caption.highlights}\n") else: print(f"Caption: {caption.text}\n")`

Run the code.

Output should look similar to the following example, where the best answer to question is pulled from one of the results.

Recall that answers are

*verbatim content*pulled from your index and might be missing phrases that a user would expect to see. To get*composed answers*as generated by a chat completion model, considering using a[RAG pattern](retrieval-augmented-generation-overview)or[agentic retrieval](agentic-retrieval-overview).`Semantic Answer: Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the<em> library </em>by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply. Semantic Answer Score: 0.9829999804496765 2.124817371368408 1 Stay-Kay City Hotel Description: This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities. Caption: This classic hotel is<em> fully-refurbished </em>and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities. 2.0705394744873047 16 Double Sanctuary Resort Description: 5 star Luxury Hotel - Biggest Rooms in the city. #1 Hotel in the area listed by Traveler magazine. Free WiFi, Flexible check in/out, Fitness Center & espresso in room. Caption: <em>5 star Luxury Hotel </em>-<em> Biggest </em>Rooms in the city. #1 Hotel in the area listed by Traveler magazine. Free WiFi, Flexible check in/out, Fitness Center & espresso in room. 2.041472911834717 38 Lakeside B & B Description: Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply. Caption: Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the<em> library </em>by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply. 2.084540843963623 Double Sanctuary Resort Description: 5 star Luxury Hotel - Biggest Rooms in the city. #1 Hotel in the area listed by Traveler magazine. Free WiFi, Flexible check in/out, Fitness Center & espresso in room. Caption: <em>5 star Luxury Hotel </em>-<em> Biggest </em>Rooms in the<em> city. #1 </em>Hotel in the area listed by Traveler magazine. Free WiFi, Flexible check in/out, Fitness Center & espresso in room. ...`


In this quickstart, you learn how to use [semantic ranking](semantic-search-overview) by adding a semantic configuration to a search index and adding semantic parameters to a query. You can use the hotels-sample-index or one of your own.

In Azure AI Search, semantic ranking is query-side functionality that uses machine reading comprehension from Microsoft to rescore search results, promoting the most semantically relevant matches to the top of the list. Depending on the content and the query, semantic ranking can [significantly improve search relevance](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/azure-cognitive-search-outperforming-vector-search-with-hybrid/ba-p/3929167) with minimal developer effort.

You can add a semantic configuration to an existing index with no rebuild requirement. Semantic ranking is most effective on text that's informational or descriptive.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).A

[new or existing index](search-how-to-create-search-index)with descriptive or verbose text fields that are attributed as retrievable. This quickstart assumes the[hotels-sample-index](search-get-started-portal).

## Configure access

You can connect to your Azure AI Search service using API keys or Microsoft Entra ID with role assignments. Keys are easier to start with, but roles are more secure. For more information, see [Connect to Azure AI Search using roles](search-security-rbac).

To configure role-based access:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Settings**>**Keys**.Under

**API Access control**, select**Role-based access control**or**Both**if you need time to transition clients to role-based access.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Assign the

**Search Service Contributor**and**Search Index Data Contributor**roles to your user account.

## Start with an index

This quickstart assumes an existing index and modifies it to include a semantic configuration. We recommend the [hotels-sample-index](search-get-started-portal) that you can create in minutes using an Azure portal wizard.

To start with an existing index:

Sign in to the

[Azure portal](https://portal.azure.com/)and find your search service.Under

**Search management**>**Indexes**, select the hotels-sample-index.Select

**Semantic configurations**to ensure the index doesn't have a semantic configuration.Select

**Search explorer**, and then select the**JSON view**.Paste the following JSON into the query editor.

`{ "search": "walking distance to live music", "select": "HotelId, HotelName, Description", "count": true }`

Select

**Search**to run the query.This query is a keyword search. The response should be similar to the following example, as scored by the default BM25 L1 ranker for full-text search.

For readability, the example only selects the

`HotelId`

,`HotelName`

, and`Description`

fields. The results contain verbatim matches on the query terms (`walking`

,`distance`

,`live`

,`music`

) or linguistic variants (`walk`

,`living`

).`"@odata.count": 13, "value": [ { "@search.score": 5.5153193, "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music." }, { "@search.score": 5.074317, "HotelId": "24", "HotelName": "Uptown Chic Hotel", "Description": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance." }, { "@search.score": 4.8959594, "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Cliff Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience." }, { "@search.score": 2.5966604, "HotelId": "35", "HotelName": "Bellevue Suites", "Description": "Comfortable city living in the very center of downtown Bellevue. Newly reimagined, this hotel features apartment-style suites with sleeping, living and work spaces. Located across the street from the Light Rail to downtown. Free shuttle to the airport." }, { "@search.score": 2.566386, "HotelId": "47", "HotelName": "Country Comfort Inn", "Description": "Situated conveniently at the north end of the village, the inn is just a short walk from the lake, offering reasonable rates and all the comforts home inlcuding living room suites and functional kitchens. Pets are welcome." }, { "@search.score": 2.2405157, "HotelId": "9", "HotelName": "Smile Up Hotel", "Description": "Experience the fresh, modern downtown. Enjoy updated rooms, bold style & prime location. Don't miss our weekend live music series featuring who's new/next on the scene." }, { "@search.score": 2.1737604, "HotelId": "8", "HotelName": "Foot Happy Suites", "Description": "Downtown in the heart of the business district. Close to everything. Leave your car behind and walk to the park, shopping, and restaurants. Or grab one of our bikes and take your explorations a little further." }, { "@search.score": 2.0364518, "HotelId": "31", "HotelName": "Country Residence Hotel", "Description": "All of the suites feature full-sized kitchens stocked with cookware, separate living and sleeping areas and sofa beds. Some of the larger rooms have fireplaces and patios or balconies. Experience real country hospitality in the heart of bustling Nashville. The most vibrant music scene in the world is just outside your front door." }, { "@search.score": 1.7595702, "HotelId": "49", "HotelName": "Swirling Currents Hotel", "Description": "Spacious rooms, glamorous suites and residences, rooftop pool, walking access to shopping, dining, entertainment and the city center. Each room comes equipped with a microwave, a coffee maker and a minifridge. In-room entertainment includes complimentary W-Fi and flat-screen TVs. " }, { "@search.score": 1.5502293, "HotelId": "15", "HotelName": "By the Market Hotel", "Description": "Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service." }, { "@search.score": 1.3302404, "HotelId": "42", "HotelName": "Rock Bottom Resort & Campground", "Description": "Rock Bottom is nestled on 20 unspoiled acres on a private cove of Rock Bottom Lake. We feature both lodging and campground accommodations to suit just about every taste. Even though we are out of the traffic of the city, getting there is only a short drive away." }, { "@search.score": 0.9050383, "HotelId": "38", "HotelName": "Lakeside B & B", "Description": "Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply." }, { "@search.score": 0.7334347, "HotelId": "39", "HotelName": "White Mountain Lodge & Suites", "Description": "Live amongst the trees in the heart of the forest. Hike along our extensive trail system. Visit the Natural Hot Springs, or enjoy our signature hot stone massage in the Cathedral of Firs. Relax in the meditation gardens, or join new friends around the communal firepit. Weekend evening entertainment on the patio features special guest musicians or poetry readings." } ]`


This query shows how the response looks *before* semantic ranking is applied. Later, you can run the same query after semantic ranking is configured to see how the response changes.

Tip

You can add a semantic configuration in the Azure portal. However, if you want to learn how to add a semantic configuration programmatically, continue with this quickstart.

## Set up the client

In this quickstart, you use a REST client and the [Azure AI Search REST APIs](/en-us/rest/api/searchservice) to configure and use a semantic ranker.

We recommend [Visual Studio Code](https://code.visualstudio.com/download) with a [REST client extension](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) for this quickstart.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/Quickstart-semantic-ranking) to start with a finished project or follow these steps to create your own.

Start Visual Studio Code and open the

[semantic-index-update.rest](https://github.com/Azure-Samples/azure-search-rest-samples/blob/main/Quickstart-semantic-ranking/semantic-index-update.rest)file or create a new file.At the top, set environment variables for your search service, authorization, and index name.

For @searchURL, sign in to the Azure portal and copy the URL from the search service

**Overview**page.For @personalAccessToken, follow the instructions in

[Connect without keys](search-get-started-rbac)to get your personal access token.

To test the connection, send your first request.

`### List existing indexes by name (verify the connection) GET {{searchUrl}}/indexes?api-version=2025-09-01&$select=name HTTP/1.1 Authorization: Bearer {{personalAccessToken}}`

Select

**Send Request**.Output for this GET request returns a list of existing indexes. You should get an HTTP 200 Success status code and a list of indexes, including hotels-sample-index used in this quickstart.


## Update the index

To update an index using the REST API, you must provide the entire schema, plus the modifications you want to make. This request provides hotels-sample-index schema, plus the semantic configuration. The modification consists of the following JSON.

```
"semantic": {
"configurations": [
{
"name": "semantic-config",
"rankingOrder": "BoostedRerankerScore",
"prioritizedFields": {
"titleField": { "fieldName": "HotelName" },
"prioritizedContentFields": [{ "fieldName": "Description" }],
"prioritizedKeywordsFields": [{ "fieldName": "Tags" }]
}
}
]
}
```


Formulate a PUT request specifying the index name, operation, and full JSON schema. All required elements of the schema must be present. This request includes the full schema for hotels-sample-index plus the semantic configuration.

`PUT {{searchUrl}}/indexes/hotels-sample-index?api-version=2025-09-01 HTTP/1.1 Content-Type: application/json Authorization: Bearer {{personalAccessToken}} { "name": "hotels-sample-index", "fields": [ { "name": "HotelId", "type": "Edm.String", "searchable": false, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true, "key": true }, { "name": "HotelName", "type": "Edm.String", "searchable": true, "filterable": false, "retrievable": true, "stored": true, "sortable": false, "facetable": false, "analyzer": "en.microsoft" }, { "name": "Description", "type": "Edm.String", "searchable": true, "filterable": false, "retrievable": true, "stored": true, "sortable": false, "facetable": false, "analyzer": "en.microsoft" }, { "name": "Description_fr", "type": "Edm.String", "searchable": true, "filterable": false, "retrievable": true, "stored": true, "sortable": false, "facetable": false, "analyzer": "fr.microsoft" }, { "name": "Category", "type": "Edm.String", "searchable": true, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true, "analyzer": "en.microsoft" }, { "name": "Tags", "type": "Collection(Edm.String)", "searchable": true, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true, "analyzer": "en.microsoft" }, { "name": "ParkingIncluded", "type": "Edm.Boolean", "searchable": false, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true }, { "name": "LastRenovationDate", "type": "Edm.DateTimeOffset", "searchable": false, "filterable": false, "retrievable": true, "stored": true, "sortable": true, "facetable": false }, { "name": "Rating", "type": "Edm.Double", "searchable": false, "filterable": true, "retrievable": true, "stored": true, "sortable": true, "facetable": true }, { "name": "Address", "type": "Edm.ComplexType", "fields": [ { "name": "StreetAddress", "type": "Edm.String", "searchable": true, "filterable": false, "retrievable": true, "stored": true, "sortable": false, "facetable": false, "analyzer": "en.microsoft" }, { "name": "City", "type": "Edm.String", "searchable": true, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true, "analyzer": "en.microsoft" }, { "name": "StateProvince", "type": "Edm.String", "searchable": true, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true, "analyzer": "en.microsoft" }, { "name": "PostalCode", "type": "Edm.String", "searchable": true, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true, "analyzer": "en.microsoft" }, { "name": "Country", "type": "Edm.String", "searchable": true, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true, "analyzer": "en.microsoft" }]}, { "name": "Location", "type": "Edm.GeographyPoint", "searchable": false, "filterable": true, "retrievable": true, "stored": true, "sortable": true, "facetable": false }, { "name": "Rooms", "type": "Collection(Edm.ComplexType)", "fields": [ { "name": "Description", "type": "Edm.String", "searchable": true, "filterable": false, "retrievable": true, "stored": true, "sortable": false, "facetable": false, "analyzer": "en.microsoft" }, { "name": "Description_fr", "type": "Edm.String", "searchable": true, "filterable": false, "retrievable": true, "stored": true, "sortable": false, "facetable": false, "analyzer": "fr.microsoft" }, { "name": "Type", "type": "Edm.String", "searchable": true, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true, "analyzer": "en.microsoft" }, { "name": "BaseRate", "type": "Edm.Double", "searchable": false, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true }, { "name": "BedOptions", "type": "Edm.String", "searchable": true, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true, "analyzer": "en.microsoft" }, { "name": "SleepsCount", "type": "Edm.Int64", "searchable": false, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true }, { "name": "SmokingAllowed", "type": "Edm.Boolean", "searchable": false, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true }, { "name": "Tags", "type": "Collection(Edm.String)", "searchable": true, "filterable": true, "retrievable": true, "stored": true, "sortable": false, "facetable": true, "analyzer": "en.microsoft" }]}, { "name": "id", "type": "Edm.String", "searchable": false, "filterable": false, "retrievable": false, "stored": true, "sortable": false, "facetable": false }, { "name": "rid", "type": "Edm.String", "searchable": false, "filterable": false, "retrievable": false, "stored": true, "sortable": false, "facetable": false }], "scoringProfiles": [], "suggesters": [], "analyzers": [], "normalizers": [], "tokenizers": [], "tokenFilters": [], "charFilters": [], "similarity": { "@odata.type": "#Microsoft.Azure.Search.BM25Similarity" }, "semantic": { "configurations": [ { "name": "semantic-config", "rankingOrder": "BoostedRerankerScore", "prioritizedFields": { "titleField": { "fieldName": "HotelName" }, "prioritizedContentFields": [ { "fieldName": "Description" } ], "prioritizedKeywordsFields": [ { "fieldName": "Tags" } ] } } ] } }`

Select

**Send Request**.Output for this POST request is an

`HTTP 200 Success`

status message.

## Run semantic queries

Required semantic parameters include `query_type`

and `semantic_configuration_name`

. Here's an example of a basic semantic query using the minimum parameters.

Open the

[semantic-query.rest](https://github.com/Azure-Samples/azure-search-rest-samples/blob/main/Quickstart-semantic-ranking/semantic-query.rest)file or create a new file.At the top of the file, set environment variables for your search service, authorization, and index name.

For @searchURL, sign in to the Azure portal and copy the URL from the search service

**Overview**page.For @personalAccessToken, follow the instructions in

[Connect without keys](search-get-started-rbac)to get your personal access token.

Test the connection with a GET request that returns the hotels-sample-index.

`GET {{searchUrl}}/indexes/hotels-sample-index?api-version=2025-09-01 HTTP/1.1 Authorization: Bearer {{personalAccessToken}}`

Send a query that includes the semantic query type and configuration name.

`POST {{searchUrl}}/indexes/hotels-sample-index/docs/search?api-version=2025-09-01 HTTP/1.1 Content-Type: application/json Authorization: Bearer {{personalAccessToken}} { "search": "walking distance to live music", "select": "HotelId, HotelName, Description", "count": true, "top": 7, "queryType": "simple" }`

Output consists of JSON search results. Thirteen hotels match the query. The top seven are included in this example.

`{ "@odata.count": 13, "@search.answers": [], "value": [ { "@search.score": 5.074317, "@search.rerankerScore": 2.613231658935547, "HotelId": "24", "HotelName": "Uptown Chic Hotel", "Description": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance." }, { "@search.score": 5.5153193, "@search.rerankerScore": 2.271434783935547, "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music." }, { "@search.score": 4.8959594, "@search.rerankerScore": 1.9861756563186646, "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Cliff Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience." }, { "@search.score": 0.7334347, "@search.rerankerScore": 1.9615401029586792, "HotelId": "39", "HotelName": "White Mountain Lodge & Suites", "Description": "Live amongst the trees in the heart of the forest. Hike along our extensive trail system. Visit the Natural Hot Springs, or enjoy our signature hot stone massage in the Cathedral of Firs. Relax in the meditation gardens, or join new friends around the communal firepit. Weekend evening entertainment on the patio features special guest musicians or poetry readings." }, { "@search.score": 1.5502293, "@search.rerankerScore": 1.9085469245910645, "HotelId": "15", "HotelName": "By the Market Hotel", "Description": "Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service." }, { "@search.score": 1.7595702, "@search.rerankerScore": 1.90234375, "HotelId": "49", "HotelName": "Swirling Currents Hotel", "Description": "Spacious rooms, glamorous suites and residences, rooftop pool, walking access to shopping, dining, entertainment and the city center. Each room comes equipped with a microwave, a coffee maker and a minifridge. In-room entertainment includes complimentary W-Fi and flat-screen TVs. " }, { "@search.score": 2.0364518, "@search.rerankerScore": 1.9012802839279175, "HotelId": "31", "HotelName": "Country Residence Hotel", "Description": "All of the suites feature full-sized kitchens stocked with cookware, separate living and sleeping areas and sofa beds. Some of the larger rooms have fireplaces and patios or balconies. Experience real country hospitality in the heart of bustling Nashville. The most vibrant music scene in the world is just outside your front door." } ] }`


### Return captions

Optionally, you can add captions to extract portions of the text and apply hit highlighting to the important terms and phrases. This query adds captions that include hit highlighting.

Add the

`captions`

parameter and send the request.`POST {{searchUrl}}/indexes/hotels-sample-index/docs/search?api-version=2025-09-01 HTTP/1.1 Content-Type: application/json Authorization: Bearer {{personalAccessToken}} { "search": "walking distance to live music", "select": "HotelId, HotelName, Description", "count": true, "queryType": "semantic", "semanticConfiguration": "semantic-config", "captions": "extractive|highlight-true" }`

Output consists of the same results, with the addition of

`"@search.captions"`

. Here's the JSON for a single document. Each match includes search scores, captions in plain text and highlight formatting, and the select fields.`{ "@search.score": 5.074317, "@search.rerankerScore": 2.613231658935547, "@search.captions": [ { "text": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance.", "highlights": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to<em> theaters, </em>art galleries, restaurants and shops. Visit<em> Seattle Art Museum </em>by day, and then head over to<em> Benaroya Hall </em>to catch the evening's concert performance." } ], "HotelId": "24", "HotelName": "Uptown Chic Hotel", "Description": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance." }`


### Return semantic answers

In this final query, return semantic answers.

Semantic ranker can produce an answer to a query string that has the characteristics of a question. The generated answer is extracted verbatim from your content so it won't include composed content like what you might expect from a chat completion model. If the semantic answer isn't useful for your scenario, you can omit `semantic_answers`

from your code.

To produce a semantic answer, the question and answer must be closely aligned, and the model must find content that clearly answers the question. If potential answers fail to meet a confidence threshold, the model doesn't return an answer. For demonstration purposes, the question in this example is designed to get a response so that you can see the syntax.

Formulate the request using a search string that asks a question.

`POST {{searchUrl}}/indexes/hotels-sample-index/docs/search?api-version=2025-09-01 HTTP/1.1 Content-Type: application/json Authorization: Bearer {{personalAccessToken}} { "search": "what's a good hotel for people who like to read", "select": "HotelId, HotelName, Description", "count": true, "queryType": "semantic", "semanticConfiguration": "semantic-config" "answers": "extractive" }`

Output consists of 41 results for the new query, with "@search.answers" for the question in the query about hotels for people who like to read.

Recall that answers are

*verbatim content*pulled from your index and might be missing phrases that a user would expect to see. To get*composed answers*as generated by a chat completion model, considering using a[RAG pattern](retrieval-augmented-generation-overview)or[agentic retrieval](agentic-retrieval-overview).In this example, the answer is considered as a strong fit for the question.

`{ "@odata.count": 41, "@search.answers": [ { "key": "38", "text": "Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply.", "highlights": "Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the<em> library </em>by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply.", "score": 0.9829999804496765 } ], "value": [ { "@search.score": 2.0361428, "@search.rerankerScore": 2.124817371368408, "HotelId": "1", "HotelName": "Stay-Kay City Hotel", "Description": "This classic hotel is fully-refurbished and ideally located on the main commercial artery of the city in the heart of New York. A few minutes away is Times Square and the historic centre of the city, as well as other places of interest that make New York one of America's most attractive and cosmopolitan cities." }, { "@search.score": 3.759768, "@search.rerankerScore": 2.0705394744873047, "HotelId": "16", "HotelName": "Double Sanctuary Resort", "Description": "5 star Luxury Hotel - Biggest Rooms in the city. #1 Hotel in the area listed by Traveler magazine. Free WiFi, Flexible check in/out, Fitness Center & espresso in room." }, { "@search.score": 0.7308748, "@search.rerankerScore": 2.041472911834717, "HotelId": "38", "HotelName": "Lakeside B & B", "Description": "Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply." }, { "@search.score": 3.391012, "@search.rerankerScore": 2.0231292247772217, "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music." }, { "@search.score": 1.3198771, "@search.rerankerScore": 2.021622657775879, "HotelId": "15", "HotelName": "By the Market Hotel", "Description": "Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service." }, { "@search.score": 1.3983066, "@search.rerankerScore": 2.005582809448242, "HotelId": "5", "HotelName": "Red Tide Hotel", "Description": "On entering this charming hotel in Scarlet Harbor, you'll notice an uncommon blend of antiques, original artwork, and contemporary comforts that give this hotel its signature look. Each suite is furnished to accentuate the views and unique characteristics of the building's classic architecture. No two suites are alike. However, all guests are welcome in the mezzanine plaza, the surrounding gardens, and the northside terrace for evening refreshments." }, { "@search.score": 1.4815493, "@search.rerankerScore": 1.9739465713500977, "HotelId": "24", "HotelName": "Uptown Chic Hotel", "Description": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance." } ] }`


In this quickstart, you learn how to use [semantic ranking](semantic-search-overview) by adding a semantic configuration to a search index and adding semantic parameters to a query. You can use the hotels-sample-index or one of your own.

In Azure AI Search, semantic ranking is query-side functionality that uses machine reading comprehension from Microsoft to rescore search results, promoting the most semantically relevant matches to the top of the list. Depending on the content and the query, semantic ranking can [significantly improve search relevance](https://techcommunity.microsoft.com/t5/azure-ai-services-blog/azure-cognitive-search-outperforming-vector-search-with-hybrid/ba-p/3929167) with minimal developer effort.

You can add a semantic configuration to an existing index with no rebuild requirement. Semantic ranking is most effective on text that's informational or descriptive.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).A

[new or existing index](search-how-to-create-search-index)with descriptive or verbose text fields that are attributed as retrievable. This quickstart assumes the[hotels-sample-index](search-get-started-portal).

## Configure access

You can connect to your Azure AI Search service using API keys or Microsoft Entra ID with role assignments. Keys are easier to start with, but roles are more secure. For more information, see [Connect to Azure AI Search using roles](search-security-rbac).

To configure role-based access:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Settings**>**Keys**.Under

**API Access control**, select**Role-based access control**or**Both**if you need time to transition clients to role-based access.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Assign the

**Search Service Contributor**and**Search Index Data Contributor**roles to your user account.

## Start with an index

This quickstart assumes an existing index and modifies it to include a semantic configuration. We recommend the [hotels-sample-index](search-get-started-portal) that you can create in minutes using an Azure portal wizard.

To start with an existing index:

Sign in to the

[Azure portal](https://portal.azure.com/)and find your search service.Under

**Search management**>**Indexes**, select the hotels-sample-index.Select

**Semantic configurations**to ensure the index doesn't have a semantic configuration.Select

**Search explorer**, and then select the**JSON view**.Paste the following JSON into the query editor.

`{ "search": "walking distance to live music", "select": "HotelId, HotelName, Description", "count": true }`

Select

**Search**to run the query.This query is a keyword search. The response should be similar to the following example, as scored by the default BM25 L1 ranker for full-text search.

For readability, the example only selects the

`HotelId`

,`HotelName`

, and`Description`

fields. The results contain verbatim matches on the query terms (`walking`

,`distance`

,`live`

,`music`

) or linguistic variants (`walk`

,`living`

).`"@odata.count": 13, "value": [ { "@search.score": 5.5153193, "HotelId": "2", "HotelName": "Old Century Hotel", "Description": "The hotel is situated in a nineteenth century plaza, which has been expanded and renovated to the highest architectural standards to create a modern, functional and first-class hotel in which art and unique historical elements coexist with the most modern comforts. The hotel also regularly hosts events like wine tastings, beer dinners, and live music." }, { "@search.score": 5.074317, "HotelId": "24", "HotelName": "Uptown Chic Hotel", "Description": "Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance." }, { "@search.score": 4.8959594, "HotelId": "4", "HotelName": "Sublime Palace Hotel", "Description": "Sublime Cliff Hotel is located in the heart of the historic center of Sublime in an extremely vibrant and lively area within short walking distance to the sites and landmarks of the city and is surrounded by the extraordinary beauty of churches, buildings, shops and monuments. Sublime Cliff is part of a lovingly restored 19th century resort, updated for every modern convenience." }, { "@search.score": 2.5966604, "HotelId": "35", "HotelName": "Bellevue Suites", "Description": "Comfortable city living in the very center of downtown Bellevue. Newly reimagined, this hotel features apartment-style suites with sleeping, living and work spaces. Located across the street from the Light Rail to downtown. Free shuttle to the airport." }, { "@search.score": 2.566386, "HotelId": "47", "HotelName": "Country Comfort Inn", "Description": "Situated conveniently at the north end of the village, the inn is just a short walk from the lake, offering reasonable rates and all the comforts home inlcuding living room suites and functional kitchens. Pets are welcome." }, { "@search.score": 2.2405157, "HotelId": "9", "HotelName": "Smile Up Hotel", "Description": "Experience the fresh, modern downtown. Enjoy updated rooms, bold style & prime location. Don't miss our weekend live music series featuring who's new/next on the scene." }, { "@search.score": 2.1737604, "HotelId": "8", "HotelName": "Foot Happy Suites", "Description": "Downtown in the heart of the business district. Close to everything. Leave your car behind and walk to the park, shopping, and restaurants. Or grab one of our bikes and take your explorations a little further." }, { "@search.score": 2.0364518, "HotelId": "31", "HotelName": "Country Residence Hotel", "Description": "All of the suites feature full-sized kitchens stocked with cookware, separate living and sleeping areas and sofa beds. Some of the larger rooms have fireplaces and patios or balconies. Experience real country hospitality in the heart of bustling Nashville. The most vibrant music scene in the world is just outside your front door." }, { "@search.score": 1.7595702, "HotelId": "49", "HotelName": "Swirling Currents Hotel", "Description": "Spacious rooms, glamorous suites and residences, rooftop pool, walking access to shopping, dining, entertainment and the city center. Each room comes equipped with a microwave, a coffee maker and a minifridge. In-room entertainment includes complimentary W-Fi and flat-screen TVs. " }, { "@search.score": 1.5502293, "HotelId": "15", "HotelName": "By the Market Hotel", "Description": "Book now and Save up to 30%. Central location. Walking distance from the Empire State Building & Times Square, in the Chelsea neighborhood. Brand new rooms. Impeccable service." }, { "@search.score": 1.3302404, "HotelId": "42", "HotelName": "Rock Bottom Resort & Campground", "Description": "Rock Bottom is nestled on 20 unspoiled acres on a private cove of Rock Bottom Lake. We feature both lodging and campground accommodations to suit just about every taste. Even though we are out of the traffic of the city, getting there is only a short drive away." }, { "@search.score": 0.9050383, "HotelId": "38", "HotelName": "Lakeside B & B", "Description": "Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the library by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply." }, { "@search.score": 0.7334347, "HotelId": "39", "HotelName": "White Mountain Lodge & Suites", "Description": "Live amongst the trees in the heart of the forest. Hike along our extensive trail system. Visit the Natural Hot Springs, or enjoy our signature hot stone massage in the Cathedral of Firs. Relax in the meditation gardens, or join new friends around the communal firepit. Weekend evening entertainment on the patio features special guest musicians or poetry readings." } ]`


This query shows how the response looks *before* semantic ranking is applied. Later, you can run the same query after semantic ranking is configured to see how the response changes.

Tip

You can add a semantic configuration in the Azure portal. However, if you want to learn how to add a semantic configuration programmatically, continue with this quickstart.

## Set up the client

In this quickstart, you use an IDE and the [ @azure/search-documents](https://www.npmjs.com/package/@azure/search-documents) client library to add semantic ranking to an existing search index.

The quickstart assumes the following is available on your computer:

[Visual Studio Code](https://code.visualstudio.com/)for this quickstart.[Node.js](https://nodejs.org/)(LTS) for running the sample.[TypeScript](https://www.typescriptlang.org/)for writing the sample code.

Tip

You can download the [source code](https://github.com/Azure-Samples/azure-search-javascript-samples/tree/main/quickstart-semantic-ranking-ts) to start with a finished project or follow these steps to create your own.

### Set up local development environment

Start Visual Studio Code in a new directory.

`mkdir semantic-ranking-quickstart && cd semantic-ranking-quickstart code .`

Create a new package for ESM modules in your project directory.

`npm init -y npm pkg set type=module`

Install development packages, including

[azure-search-documents](/en-us/javascript/api/%40azure/search-documents).`npm install @azure/identity @azure/search-documents dotenv`

Install development dependency packages.

`npm install dotenv @types/node --save-dev`

Create a

`tsconfig.json`

file in your project directory to enable ESM modules and set the module resolution.`{ "compilerOptions": { "target": "es2022", "module": "esnext", "moduleResolution": "bundler", "rootDir": "./src", "outDir": "./dist/", "esModuleInterop": true, "forceConsistentCasingInFileNames": true, "strict": true, "skipLibCheck": true, "declaration": true, "sourceMap": true, "resolveJsonModule": true, "moduleDetection": "force", "allowSyntheticDefaultImports": true, "verbatimModuleSyntax": false }, "include": [ "src/**/*.ts" ], "exclude": [ "node_modules/**/*", "**/*.spec.ts" ] }`

Update

`package.json`

to include a script for building TypeScript files. Add the following line to the`scripts`

section.`"build": "tsc"`

Create

`.env`

, and provide your search service endpoint. You can get the endpoint from the Azure portal on the search service**Overview**page.`AZURE_SEARCH_ENDPOINT=YOUR-SEARCH-SERVICE-ENDPOINT AZURE_SEARCH_INDEX_NAME=hotels-sample-index SEMANTIC_CONFIGURATION_NAME=semantic-config`

Create a

`src`

directory in your project directory.`mkdir src`


### Sign in to Azure

If you signed in to the [Azure portal](https://portal.azure.com), you're signed into Azure. If you aren't sure, use the Azure CLI or Azure PowerShell to log in: `az login`

or `az connect`

. If you have multiple tenants and subscriptions, see [Quickstart: Connect without keys](search-get-started-rbac) for help on how to connect.

## Create a common authentication file

Create a file in `./src`

called `config.ts`

to read the `.env`

file and hold the environment variables and authentication credential. Copy in the following code; don't change it. This file will be used by all the other files in this quickstart.

```
import { DefaultAzureCredential } from "@azure/identity";
// Configuration - use environment variables
export const searchEndpoint = process.env.AZURE_SEARCH_ENDPOINT || "PUT-YOUR-SEARCH-SERVICE-ENDPOINT-HERE";
export const indexName = process.env.AZURE_SEARCH_INDEX_NAME || "hotels-sample-index";
export const semanticConfigurationName = process.env.SEMANTIC_CONFIGURATION_NAME || "semantic-config";
// Create credential
export const credential = new DefaultAzureCredential();
console.log(`Using Azure Search endpoint: ${searchEndpoint}`);
console.log(`Using index name: ${indexName}\n\n`);
// Hotel document interface
export interface HotelDocument {
"@search.action"?: string;
HotelId: string;
HotelName: string;
Description: string;
Category: string;
Tags: string[];
ParkingIncluded: string;
LastRenovationDate: string;
Rating: number;
Address: {
StreetAddress: string;
City: string;
StateProvince: string;
PostalCode: string;
Country: string;
};
}
```


## Get the index schema

In this section, you get settings for the existing `hotels-sample-index`

index on your search service.

Create a file in

`./src`

called`getIndexSettings.ts`

and copy in the following code.`import { SearchIndexClient } from "@azure/search-documents"; import { searchEndpoint, indexName, credential } from "./config.js"; const indexClient = new SearchIndexClient(searchEndpoint, credential); console.log('Updating semantic search index...'); // Get the existing schema const index = await indexClient.getIndex(indexName); console.log(`Index name: ${index.name}`); console.log(`Number of fields: ${index.fields.length}`); for(const field of index.fields) { // @ts-ignore console.log(`Field: ${field.name}, Type: ${field.type}, Searchable: ${field.searchable}`); } if(index.semanticSearch && index.semanticSearch.configurations) { console.log(`Semantic search configurations: ${index.semanticSearch.configurations.length}`); for(const config of index.semanticSearch.configurations) { console.log(`Configuration name: ${config.name}`); console.log(`Title field: ${config.prioritizedFields.titleField?.name}`); } } else { console.log("No semantic configuration exists for this index."); }`

Run the code.

`npm run build && node -r dotenv/config dist/getIndexSettings.js`

Output is the name of the index, list of fields, and a statement indicating whether a semantic configuration exists. For the purposes of this quickstart, the message should say

`No semantic configuration exists for this index`

.

## Update the index with a semantic configuration

Create a file in

`./src`

called`updateIndexSettings.ts`

and copy in the following code to add a semantic configuration to the existing`hotels-sample-index`

index on your search service. No search documents are deleted by this operation and your index is still operational after the configuration is added.`import { SearchIndexClient, SemanticConfiguration, SemanticPrioritizedFields, SemanticField } from "@azure/search-documents"; import { searchEndpoint, indexName, credential, semanticConfigurationName } from "./config.js"; try { const indexClient = new SearchIndexClient(searchEndpoint, credential); const existingIndex = await indexClient.getIndex(indexName); const fields: SemanticPrioritizedFields = { titleField: { name: "HotelName" }, keywordsFields: [{ name: "Tags" }] as SemanticField[], contentFields: [{ name: "Description" }] as SemanticField[] } const newSemanticConfiguration: SemanticConfiguration = { name: semanticConfigurationName, prioritizedFields: fields }; // Add the new semantic configuration to the existing index if (existingIndex.semanticSearch && existingIndex.semanticSearch.configurations) { existingIndex.semanticSearch.configurations.push(newSemanticConfiguration); } else { const configExists = existingIndex.semanticSearch?.configurations?.some( config => config.name === semanticConfigurationName ); if (!configExists) { existingIndex.semanticSearch = { configurations: [newSemanticConfiguration] }; } } await indexClient.createOrUpdateIndex(existingIndex); const updatedIndex = await indexClient.getIndex(indexName); console.log(`Semantic configurations:`); console.log("-".repeat(40)); if (updatedIndex.semanticSearch && updatedIndex.semanticSearch.configurations) { for (const config of updatedIndex.semanticSearch.configurations) { console.log(`Configuration name: ${config.name}`); console.log(`Title field: ${config.prioritizedFields.titleField?.name}`); console.log(`Keywords fields: ${config.prioritizedFields.keywordsFields?.map(f => f.name).join(", ")}`); console.log(`Content fields: ${config.prioritizedFields.contentFields?.map(f => f.name).join(", ")}`); console.log("-".repeat(40)); } } else { console.log("No semantic configurations found."); } console.log("Semantic configuration updated successfully."); } catch (error) { console.error("Error updating semantic configuration:", error); }`

Run the code.

`npm run build && node -r dotenv/config dist/updateIndexSettings.js`

Output is the semantic configuration you just added,

`Semantic configuration updated successfully.`

.

## Run semantic queries

Once the `hotels-sample-index`

index has a semantic configuration, you can run queries that include semantic parameters.

Create a file in

`./src`

called`semanticQuery.ts`

and copy in the following code to create a semantic query of the index. This is the minimum requirement for invoking semantic ranking.`import { SearchClient } from "@azure/search-documents"; import { HotelDocument, credential, searchEndpoint, indexName, semanticConfigurationName } from "./config.js"; const searchClient = new SearchClient<HotelDocument>( searchEndpoint, indexName, credential ); const results = await searchClient.search("walking distance to live music", { queryType: "semantic", semanticSearchOptions: { configurationName: semanticConfigurationName }, select: ["HotelId", "HotelName", "Description"] }); let rowNumber = 1; for await (const result of results.results) { // Log each result const doc = result.document; const score = result.score; const rerankerScoreDisplay = result.rerankerScore; console.log(`Search result #${rowNumber++}:`); console.log(` Re-ranker Score: ${rerankerScoreDisplay}`); console.log(` HotelId: ${doc.HotelId}`); console.log(` HotelName: ${doc.HotelName}`); console.log(` Description: ${doc.Description || 'N/A'}\n`); }`

Run the code.

`npm run build && node -r dotenv/config dist/semanticQuery.js`

Output should consist of 13 documents, ordered by the

`rerankerScoreDisplay`

.

### Return captions

Optionally, you can add captions to extract portions of the text and apply hit highlighting to the important terms and phrases. This query adds captions.

Create a file in

`./src`

called`semanticQueryReturnCaptions.ts`

and copy in the following code to add captions to the query.`import { SearchClient } from "@azure/search-documents"; import { HotelDocument, credential, searchEndpoint, indexName, semanticConfigurationName } from "./config.js"; const searchClient = new SearchClient<HotelDocument>( searchEndpoint, indexName, credential ); // Debug info console.log(`Using semantic configuration: ${semanticConfigurationName}`); console.log("Search query: walking distance to live music"); const results = await searchClient.search("walking distance to live music", { queryType: "semantic", semanticSearchOptions: { configurationName: semanticConfigurationName, captions: { captionType: "extractive", highlight: true } }, select: ["HotelId", "HotelName", "Description"], }); console.log(`Found ${results.count} results with semantic search\n`); let rowNumber = 1; for await (const result of results.results) { // Log each result const doc = result.document; const rerankerScoreDisplay = result.rerankerScore; console.log(`Search result #${rowNumber++}:`); console.log(` Re-ranker Score: ${rerankerScoreDisplay}`); console.log(` HotelName: ${doc.HotelName}`); console.log(` Description: ${doc.Description || 'N/A'}\n`); // Caption handling with better debugging const captions = result.captions; if (captions && captions.length > 0) { const caption = captions[0]; if (caption.highlights) { console.log(` Caption with highlights: ${caption.highlights}`); } else if (caption.text) { console.log(` Caption text: ${caption.text}`); } else { console.log(` Caption exists but has no text or highlights content`); } } else { console.log(" No captions found for this result"); } console.log("-".repeat(60)); }`

Run the code.

`npm run build && node -r dotenv/config dist/semanticQueryReturnCaptions.js`

Output should include a new caption element alongside search field. Captions are the most relevant passages in a result. If your index includes larger chunks of text, a caption is helpful for extracting the most interesting sentences.

`Search result #1: Re-ranker Score: 2.613231658935547 HotelName: Uptown Chic Hotel Description: Chic hotel near the city. High-rise hotel in downtown, within walking distance to theaters, art galleries, restaurants and shops. Visit Seattle Art Museum by day, and then head over to Benaroya Hall to catch the evening's concert performance. Caption with highlights: Chic hotel near the city. High-rise hotel in downtown, within walking distance to<em> theaters, </em>art galleries, restaurants and shops. Visit<em> Seattle Art Museum </em>by day, and then head over to<em> Benaroya Hall </em>to catch the evening's concert performance.`


### Return semantic answers

In this final query, return semantic answers.

Semantic ranker can produce an answer to a query string that has the characteristics of a question. The generated answer is extracted verbatim from your content so it won't include composed content like what you might expect from a chat completion model. If the semantic answer isn't useful for your scenario, you can omit `semantic_answers`

from your code.

To produce a semantic answer, the question and answer must be closely aligned, and the model must find content that clearly answers the question. If potential answers fail to meet a confidence threshold, the model doesn't return an answer. For demonstration purposes, the question in this example is designed to get a response so that you can see the syntax.

Create a file in

`./src`

called`semanticAnswer.ts`

and copy in the following code to get semantic answers.`import { SearchClient } from "@azure/search-documents"; import { HotelDocument, credential, searchEndpoint, indexName, semanticConfigurationName } from "./config.js"; const searchClient = new SearchClient<HotelDocument>( searchEndpoint, indexName, credential ); const results = await searchClient.search("What's a good hotel for people who like to read", { queryType: "semantic", semanticSearchOptions: { configurationName: semanticConfigurationName, captions: { captionType: "extractive" }, answers: { answerType: "extractive" } }, select: ["HotelName", "Description", "Category"] }); console.log(`Answers:\n\n`); let rowNumber = 1; // Extract semantic answers from the search results const semanticAnswers = results.answers; for (const answer of semanticAnswers || []) { console.log(`Semantic answer result #${rowNumber++}:`); if (answer.highlights) { console.log(`Semantic Answer: ${answer.highlights}`); } else { console.log(`Semantic Answer: ${answer.text}`); } console.log(`Semantic Answer Score: ${answer.score}\n\n`); } console.log(`Search Results:\n\n`); rowNumber = 1; // Iterate through the search results for await (const result of results.results) { // Log each result const doc = result.document; const rerankerScoreDisplay = result.rerankerScore; console.log(`Search result #${rowNumber++}:`); console.log(`${rerankerScoreDisplay}`); console.log(`${doc.HotelName}`); console.log(`${doc.Description || 'N/A'}`); const captions = result.captions; if (captions && captions.length > 0) { const caption = captions[0]; if (caption.highlights) { console.log(`Caption: ${caption.highlights}\n`); } else { console.log(`Caption: ${caption.text}\n`); } } }`

Run the code.

`npm run build && node -r dotenv/config dist/semanticAnswer.js`

Output should look similar to the following example, where the best answer to question is pulled from one of the results.

Recall that answers are

*verbatim content*pulled from your index and might be missing phrases that a user would expect to see. To get*composed answers*as generated by a chat completion model, considering using a[RAG pattern](retrieval-augmented-generation-overview)or[agentic retrieval](agentic-retrieval-overview).`Semantic answer result #1: Semantic Answer: Nature is Home on the beach. Explore the shore by day, and then come home to our shared living space to relax around a stone fireplace, sip something warm, and explore the<em> library </em>by night. Save up to 30 percent. Valid Now through the end of the year. Restrictions and blackouts may apply. Semantic Answer Score: 0.9829999804496765`


## Clean up resources

When you're working in your own subscription, it's a good idea at the end of a project to identify whether you still need the resources you created. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.

You can find and manage resources in the Azure portal, using the **All resources** or **Resource groups** link in the left-navigation pane.

## Related content

In this quickstart, you learned how to invoke semantic ranking on an existing index. We recommend trying semantic ranking on your own indexes as a next step. The following articles can help you get started.