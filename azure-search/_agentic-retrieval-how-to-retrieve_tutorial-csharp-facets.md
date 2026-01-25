---
merged_at: 2026-01-25T03:18:14.110843
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: agentic-retrieval-how-to-retrieve.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-retrieve -->

# Retrieve data by using a knowledge base in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In an agentic retrieval multi-query pipeline, query execution is through the [ retrieve action](/en-us/rest/api/searchservice/knowledge-retrieval/retrieve?view=rest-searchservice-2025-11-01-preview&preserve-view=true) on a knowledge base that invokes parallel query processing. This request structure is updated for the new 2025-11-01-preview, which introduces breaking changes from previous previews. For help with breaking changes, see

[Migrate your agentic retrieval code](agentic-retrieval-how-to-migrate).

This article explains how to set up a retrieve action. It also describes the three components of the retrieval response:

*extracted response for the LLM**referenced results**query activity*

A retrieve request can include instructions for query processing that override the default instructions set on the knowledge base. A retrieve action has core parameters that are supported on any request, plus parameters that are specific to a knowledge source.

You can also use optional [answer synthesis](agentic-retrieval-how-to-answer-synthesis) to bring LLM answer formulation into the query pipeline, returning a concise or formatted answer to an agent or app.

## Prerequisites

A

[supported knowledge source](agentic-knowledge-source-overview#supported-knowledge-sources)that wraps a searchable index or points to an external source for native data retrieval.A

[knowledge base](agentic-retrieval-how-to-create-knowledge-base)that represents one or more knowledge sources. If you want intelligent query planning and answer formulation, include a chat completion model.Azure AI Search in any

[region that provides agentic retrieval](search-region-support).Permissions on Azure AI Search. Roles for retrieving content include

**Search Index Data Reader**for running queries. To support an outbound call from a search service to a chat completion model, you must configure a managed identity for the search service, and it must have**Cognitive Services User**permissions on the Azure OpenAI resource. For more information about local testing and obtaining access tokens, see[Quickstart: Connect without keys](search-get-started-rbac).API version requirements. To create or use a knowledge base, use the

[2025-11-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true)data plane REST API. Or, use a preview package of an Azure SDK that provides knowledge base APIs:[Python](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/search/azure-search-documents/CHANGELOG.md),[.NET](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/search/Azure.Search.Documents/CHANGELOG.md#1170-beta3-2025-03-25),[Java](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/CHANGELOG.md).

To follow the steps in this guide, we recommend [Visual Studio Code](https://code.visualstudio.com/download) with a [REST client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client) for sending REST API calls to Azure AI Search.

## Set up the retrieve action

Specify a retrieve action on a [knowledge base](agentic-retrieval-how-to-create-knowledge-base). The knowledge base has one or more knowledge sources. Retrieval can return a synthesized answer in natural language or raw grounding chunks from the knowledge sources.

Review your knowledge base definition to understand which knowledge sources are in scope.

Review your knowledge sources to understand their parameters and configuration.

Use the

[2025-11-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true)data plane REST API or an Azure SDK preview package to call retrieve.

For knowledge sources that have default retrieval instructions, you can override the defaults in the retrieve request.

### Retrieval from a search index

For knowledge sources that target a search index, all `searchable`

fields are in scope for query execution. If the index includes vector fields, your index should have a valid [vectorizer definition](vector-search-how-to-configure-vectorizer) so that the agentic retrieval engine can vectorize the query inputs. Otherwise, vector fields are ignored. The implied query type is `semantic`

, and there's no search mode.

The input for the retrieval route is chat conversation history in natural language, where the `messages`

array contains the conversation. The agentic retrieval engine supports messages only if the [retrieval reasoning effort](agentic-retrieval-how-to-set-retrieval-reasoning-effort) is either low or medium.

```
@search-url=<YOUR SEARCH SERVICE URL>
@accessToken=<YOUR PERSONAL ID>
# Send grounding request
POST https://{{search-url}}/knowledgebases/{{knowledge-base-name}}/retrieve?api-version=2025-11-01-preview
Content-Type: application/json
Authorization: Bearer {{accessToken}}
{
"messages" : [
{
"role" : "assistant",
"content" : [
{ "type" : "text", "text" : "You can answer questions about the Earth at night.
Sources have a JSON format with a ref_id that must be cited in the answer.
If you do not have the answer, respond with 'I do not know'." }
]
},
{
"role" : "user",
"content" : [
{ "type" : "text", "text" : "Why is the Phoenix nighttime street grid is so sharply visible from space, whereas large stretches of the interstate between midwestern cities remain comparatively dim?" }
]
}
],
"knowledgeSourceParams": [
{
"filterAddOn": null,
"knowledgeSourceName": "earth-at-night-blob-ks",
"kind": "searchIndex"
}
]
}
```


### Responses

Successful retrieval returns a `200 OK`

status code. If the knowledge base fails to retrieve from one or more knowledge sources, a `206 Partial Content`

status code returns. The response only includes results from sources that succeeded. Details about the partial response appear as [errors in the activity array](#review-the-activity-array).

### Retrieve parameters

| Name | Description | Type | Editable | Required |
|---|---|---|---|---|
`messages` |
Articulates the messages sent to a chat completion model. The message format is similar to Azure OpenAI APIs. | Object | Yes | No |
`role` |
Defines where the message came from, for example either `assistant` or `user` . The model you use determines which roles are valid. |
String | Yes | No |
`content` |
The message or prompt sent to the LLM. It must be text in this preview. | String | Yes | No |
`knowledgeSourceParams` |

## Examples

Retrieve requests vary depending on the knowledge sources and whether you want to override a default configuration. Here are several examples that illustrate a range of requests.

### Example: Override default reasoning effort and set request limits

This example specifies [answer formulation](agentic-retrieval-how-to-answer-synthesis), so `retrievalReasoningEffort`

must be "low" or "medium".

```
POST {{url}}/knowledgebases/kb-override/retrieve?api-version={{api-version}}
api-key: {{key}}
Content-Type: application/json
{
"messages": [
{
"role": "user",
"content": [
{ "type": "text", "text": "What companies are in the financial sector?" }
]
}
],
"retrievalReasoningEffort": { "kind": "low" },
"outputMode": "answerSynthesis",
"maxRuntimeInSeconds": 30,
"maxOutputSize": 6000
}
```


### Example: Set references for each knowledge source

This example uses the default reasoning effort specified in the knowledge base. The focus of this example is specification of how much information to include in the response.

```
POST {{url}}/knowledgebases/kb-medium-example/retrieve?api-version={{api-version}}
api-key: {{key}}
Content-Type: application/json
{
"messages": [
{
"role": "user",
"content": [
{ "type": "text", "text": "What companies are in the financial sector?" }
]
}
],
"includeActivity": true,
"knowledgeSourceParams": [
{
"knowledgeSourceName": "demo-financials-ks",
"kind": "searchIndex",
"includeReferences": true,
"includeReferenceSourceData": true
},
{
"knowledgeSourceName": "demo-communicationservices-ks",
"kind": "searchIndex",
"includeReferences": false,
"includeReferenceSourceData": false
},
{
"knowledgeSourceName": "demo-healthcare=ks",
"kind": "searchIndex",
"includeReferences": true,
"includeReferenceSourceData": false,
"alwaysQuerySource": true
}
]
}
```


Note

If you're retrieving content from a OneLake or indexed SharePoint knowledge source, set `includeReferenceSourceData`

to `true`

to include the source document URL in the citation.

### Example: minimal reasoning effort

In this example, there's no chat completion model for intelligent query planning or answer formulation. The query string goes to the agentic retrieval engine for keyword search or hybrid search.

```
POST {{url}}/knowledgebases/kb-minimal/retrieve?api-version={{api-version}}
api-key: {{key}}
Content-Type: application/json
{
"intents": [
{
"type": "semantic",
"search": "what is a brokerage"
}
]
}
```


## Review the extracted response

The *extracted response* is a single unified string that you typically pass to an LLM. The LLM consumes it as grounding data and uses it to formulate a response. Your API call to the LLM includes the unified string and instructions for the model, such as whether to use the grounding exclusively or as a supplement.

The body of the response is also structured in the chat message style format. Currently, in this preview release, the content is serialized JSON.

```
"response": [
{
"role": "assistant",
"content": [
{
"type": "text",
"text": "[{\"ref_id\":0,\"title\":\"Urban Structure\",\"terms\":\"Location of Phoenix, Grid of City Blocks, Phoenix Metropolitan Area at Night\",\"content\":\"<content chunk redacted>\"}]"
}
]
}
]
```


**Key points**:

`content.text`

is a JSON array. It's a single string composed of the most relevant documents (or chunks) found in the search index, given the query and chat history inputs. This array is your grounding data that a chat completion model uses to formulate a response to the user's question.This portion of the response consists of 200 chunks or fewer, excluding any results that fail to meet the minimum threshold of a 2.5 reranker score.

The string starts with the reference ID of the chunk (used for citation purposes), and any fields specified in the semantic configuration of the target index. In this example, assume the semantic configuration in the target index has a "title" field, a "terms" field, and a "content" field.

`content.type`

has one valid value in this preview:`text`

.

Note

The `maxOutputSize`

property on the [knowledge base](agentic-retrieval-how-to-create-knowledge-base) determines the length of the string.

## Review the activity array

The activity array outputs the query plan, which helps you track the operations performed when executing the request. It also provides operational transparency so you can understand the billing implications and frequency of resource invocations.

The output includes the following components.

| Section | Description |
|---|---|
| modelQueryPlanning | For knowledge bases that use an LLM for query planning, this section reports on the token counts used for input, and the token count for the subqueries. |
| source-specific activity | For each knowledge source included in the query, report on elapsed time and which arguments were used in the query, including the semantic ranker. Knowledge source types include `searchIndex` , `azureBlob` , and other
|
| agenticReasoningEffort | For each retrieve action, you can specify the degree of LLM support. Use minimal to bypass an LLM, low for constrained LLM processing, and medium for full LLM processing. |
| modelAnswerSynthesis | For knowledge bases that specify answer formulation, this section reports on the token count for formulating the answer, and the token count of the answer output. |

The output reports on the token consumption for agentic reasoning during retrieval at the specified [retrieval reasoning effort](agentic-retrieval-how-to-set-retrieval-reasoning-effort).

The output also includes the following information:

- Subqueries sent to the retrieval pipeline.
- Errors for any retrieval failures, such as inaccessible knowledge sources.

Here's an example of an activity array.

```
"activity": [
{
"type": "modelQueryPlanning",
"id": 0,
"inputTokens": 2302,
"outputTokens": 109,
"elapsedMs": 2396
},
{
"type": "searchIndex",
"id": 1,
"knowledgeSourceName": "demo-financials-ks",
"queryTime": "2025-11-04T19:25:23.683Z",
"count": 26,
"elapsedMs": 1137,
"searchIndexArguments": {
"search": "List of companies in the financial sector according to SEC GICS classification",
"filter": null,
"sourceDataFields": [ ],
"searchFields": [ ],
"semanticConfigurationName": "en-semantic-config"
}
},
{
"type": "searchIndex",
"id": 2,
"knowledgeSourceName": "demo-healthcare-ks",
"queryTime": "2025-11-04T19:25:24.186Z",
"count": 17,
"elapsedMs": 494,
"searchIndexArguments": {
"search": "List of companies in the financial sector according to SEC GICS classification",
"filter": null,
"sourceDataFields": [ ],
"searchFields": [ ],
"semanticConfigurationName": "en-semantic-config"
}
},
{
"type": "agenticReasoning",
"id": 3,
"retrievalReasoningEffort": {
"kind": "low"
},
"reasoningTokens": 103368
},
{
"type": "modelAnswerSynthesis",
"id": 4,
"inputTokens": 5821,
"outputTokens": 344,
"elapsedMs": 3837
}
]
```


## Review the references array

The `references`

array comes directly from the underlying grounding data. It includes the `sourceData`

used to generate the response. It consists of every document that the agentic retrieval engine finds and semantically ranks. Fields in the `sourceData`

include an `id`

and semantic fields: `title`

, `terms`

, and `content`

.

The `id`

acts as a reference ID for an item within a specific response. It's not the document key in the search index. You use it for providing citations.

The purpose of this array is to provide a chat message style structure for easy integration. For example, if you want to serialize the results into a different structure or you require some programmatic manipulation of the data before you returned it to the user.

You can also get the structured data from the source data object in the references array to manipulate it however you see fit.

Here's an example of the references array.

```
"references": [
{
"type": "AzureSearchDoc",
"id": "0",
"activitySource": 2,
"docKey": "earth_at_night_508_page_104_verbalized",
"sourceData": null
},
{
"type": "AzureSearchDoc",
"id": "1",
"activitySource": 2,
"docKey": "earth_at_night_508_page_105_verbalized",
"sourceData": null
}
]
```


Note

If you're retrieving content from a OneLake or indexed SharePoint knowledge source, set `includeReferenceSourceData`

to `true`

on the retrieve request to get the source document URL in the citation.


---

<!-- DOCUMENTO FUSIONADO: tutorial-csharp-facets.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/tutorial-csharp-facets -->

# Tutorial: Add faceted navigation using the .NET SDK

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Facets enable self-directed navigation by providing a set of links for filtering results. In this tutorial, a faceted navigation structure is placed on the left side of the page, with labels and clickable text to trim the results.

In this tutorial, you learn how to:

- Set model properties as
*IsFacetable* - Add facet navigation to your app

## Overview

Facets are based on fields in your search index. A query request that includes facet=[string] provides the field to facet by. It's common to include multiple facets, such as `&facet=category&facet=amenities`

, each one separated by an ampersand (&) character. Implementing a faceted navigation structure requires that you specify both facets and filters. The filter is used on a click event to narrow results. For example, clicking "budget" filters the results based on that criteria.

This tutorial extends the paging project created in the [Add paging to search results](/en-us/azure/search/tutorial-csharp-paging) tutorial.

A finished version of the code in this tutorial can be found in the following project:

## Prerequisites

[2a-add-paging (GitHub)](https://github.com/Azure-Samples/azure-search-sample-archive/tree/main/create-first-app/v11)solution. This project can either be your own version built from the previous tutorial or a copy from GitHub.

## Set model properties as IsFacetable

In order for a model property to be located in a facet search, it must be tagged with **IsFacetable**.

Examine the

**Hotel**class.**Category**and**Tags**, for example, are tagged as**IsFacetable**, but**HotelName**and**Description**are not.`public partial class Hotel { [SimpleField(IsFilterable = true, IsKey = true)] public string HotelId { get; set; } [SearchableField(IsSortable = true)] public string HotelName { get; set; } [SearchableField(AnalyzerName = LexicalAnalyzerName.Values.EnLucene)] public string Description { get; set; } [SearchableField(AnalyzerName = LexicalAnalyzerName.Values.FrLucene)] [JsonPropertyName("Description_fr")] public string DescriptionFr { get; set; } [SearchableField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public string Category { get; set; } [SearchableField(IsFilterable = true, IsFacetable = true)] public string[] Tags { get; set; } [SimpleField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public bool? ParkingIncluded { get; set; } [SimpleField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public DateTimeOffset? LastRenovationDate { get; set; } [SimpleField(IsFilterable = true, IsSortable = true, IsFacetable = true)] public double? Rating { get; set; } public Address Address { get; set; } [SimpleField(IsFilterable = true, IsSortable = true)] public GeographyPoint Location { get; set; } public Room[] Rooms { get; set; } }`

We will not be changing any tags as part of this tutorial, so close the hotel.cs file unaltered.

Note

A facet search will throw an error if a field requested in the search is not tagged appropriately.


## Add facet navigation to your app

For this example, we are going to enable the user to select one category of hotel, or one amenity, from lists of links shown to the left of the results. The user starts by entering some search text, then progressively narrow the results of the search by selecting a category or amenity.

It's the controller's job to pass the lists of facets to the view. To maintain the user selections as the search progresses, we use temporary storage as the mechanism for preserving state.

### Add filter strings to the SearchData model

Open the SearchData.cs file, and add string properties to the

**SearchData**class, to hold the facet filter strings.`public string categoryFilter { get; set; } public string amenityFilter { get; set; }`


### Add the Facet action method

The home controller needs one new action, **Facet**, and updates to its existing **Index** and **Page** actions, and to the **RunQueryAsync** method.

Replace the

**Index(SearchData model)**action method.`public async Task<ActionResult> Index(SearchData model) { try { // Ensure the search string is valid. if (model.searchText == null) { model.searchText = ""; } // Make the search call for the first page. await RunQueryAsync(model, 0, 0, "", "").ConfigureAwait(false); } catch { return View("Error", new ErrorViewModel { RequestId = "1" }); } return View(model); }`

Replace the

**PageAsync(SearchData model)**action method.`public async Task<ActionResult> PageAsync(SearchData model) { try { int page; // Calculate the page that should be displayed. switch (model.paging) { case "prev": page = (int)TempData["page"] - 1; break; case "next": page = (int)TempData["page"] + 1; break; default: page = int.Parse(model.paging); break; } // Recover the leftMostPage. int leftMostPage = (int)TempData["leftMostPage"]; // Recover the filters. string catFilter = TempData["categoryFilter"].ToString(); string ameFilter = TempData["amenityFilter"].ToString(); // Recover the search text. model.searchText = TempData["searchfor"].ToString(); // Search for the new page. await RunQueryAsync(model, page, leftMostPage, catFilter, ameFilter); } catch { return View("Error", new ErrorViewModel { RequestId = "2" }); } return View("Index", model); }`

Add a

**FacetAsync(SearchData model)**action method, to be activated when the user clicks on a facet link. The model will contain either a category or amenity search filter. Add it after the**PageAsync**action.`public async Task<ActionResult> FacetAsync(SearchData model) { try { // Filters set by the model override those stored in temporary data. string catFilter; string ameFilter; if (model.categoryFilter != null) { catFilter = model.categoryFilter; } else { catFilter = TempData["categoryFilter"].ToString(); } if (model.amenityFilter != null) { ameFilter = model.amenityFilter; } else { ameFilter = TempData["amenityFilter"].ToString(); } // Recover the search text. model.searchText = TempData["searchfor"].ToString(); // Initiate a new search. await RunQueryAsync(model, 0, 0, catFilter, ameFilter).ConfigureAwait(false); } catch { return View("Error", new ErrorViewModel { RequestId = "2" }); } return View("Index", model); }`


### Set up the search filter

When a user selects a certain facet, for example, they click on the **Resort and Spa** category, then only hotels that are specified as this category should be returned in the results. To narrow a search in this way, we need to set up a *filter*.

Replace the

**RunQueryAsync**method with the following code. Primarily, it takes a category filter string, and an amenity filter string, and sets the**Filter**parameter of the**SearchOptions**.`private async Task<ActionResult> RunQueryAsync(SearchData model, int page, int leftMostPage, string catFilter, string ameFilter) { InitSearch(); string facetFilter = ""; if (catFilter.Length > 0 && ameFilter.Length > 0) { // Both facets apply. facetFilter = $"{catFilter} and {ameFilter}"; } else { // One, or zero, facets apply. facetFilter = $"{catFilter}{ameFilter}"; } var options = new SearchOptions { Filter = facetFilter, SearchMode = SearchMode.All, // Skip past results that have already been returned. Skip = page * GlobalVariables.ResultsPerPage, // Take only the next page worth of results. Size = GlobalVariables.ResultsPerPage, // Include the total number of results. IncludeTotalCount = true, }; // Return information on the text, and number, of facets in the data. options.Facets.Add("Category,count:20"); options.Facets.Add("Tags,count:20"); // Enter Hotel property names into this list, so only these values will be returned. options.Select.Add("HotelName"); options.Select.Add("Description"); options.Select.Add("Category"); options.Select.Add("Tags"); // For efficiency, the search call should be asynchronous, so use SearchAsync rather than Search. model.resultList = await _searchClient.SearchAsync<Hotel>(model.searchText, options).ConfigureAwait(false); // This variable communicates the total number of pages to the view. model.pageCount = ((int)model.resultList.TotalCount + GlobalVariables.ResultsPerPage - 1) / GlobalVariables.ResultsPerPage; // This variable communicates the page number being displayed to the view. model.currentPage = page; // Calculate the range of page numbers to display. if (page == 0) { leftMostPage = 0; } else if (page <= leftMostPage) { // Trigger a switch to a lower page range. leftMostPage = Math.Max(page - GlobalVariables.PageRangeDelta, 0); } else if (page >= leftMostPage + GlobalVariables.MaxPageRange - 1) { // Trigger a switch to a higher page range. leftMostPage = Math.Min(page - GlobalVariables.PageRangeDelta, model.pageCount - GlobalVariables.MaxPageRange); } model.leftMostPage = leftMostPage; // Calculate the number of page numbers to display. model.pageRange = Math.Min(model.pageCount - leftMostPage, GlobalVariables.MaxPageRange); // Ensure Temp data is stored for the next call. TempData["page"] = page; TempData["leftMostPage"] = model.leftMostPage; TempData["searchfor"] = model.searchText; TempData["categoryFilter"] = catFilter; TempData["amenityFilter"] = ameFilter; // Return the new view. return View("Index", model); }`

Notice that the

**Category**and**Tags**properties are added to the list of**Select**items to return. This addition is not a requirement for facet navigation to work, but we use this information to verify the filters are working correctly.

### Add lists of facet links to the view

The view is going to require some significant changes.

Start by opening the hotels.css file (in the wwwroot/css folder), and add the following classes.

`.facetlist { list-style: none; } .facetchecks { width: 250px; display: normal; color: #666; margin: 10px; padding: 5px; } .facetheader { font-size: 10pt; font-weight: bold; color: darkgreen; }`

For the view, organize the output into a table, to neatly align the facet lists on the left, and the results on the right. Open the index.cshtml file. Replace the entire contents of the HTML <body> tags, with the following code.

`<body> @using (Html.BeginForm("Index", "Home", FormMethod.Post)) { <table> <tr> <td></td> <td> <h1 class="sampleTitle"> <img src="~/images/azure-logo.png" width="80" /> Hotels Search - Facet Navigation </h1> </td> </tr> <tr> <td></td> <td> <!-- Display the search text box, with the search icon to the right of it.--> <div class="searchBoxForm"> @Html.TextBoxFor(m => m.searchText, new { @class = "searchBox" }) <input value="" class="searchBoxSubmit" type="submit"> </div> </td> </tr> <tr> <td valign="top"> <div id="facetplace" class="facetchecks"> @if (Model != null && Model.resultList != null) { List<string> categories = Model.resultList.Facets["Category"].Select(x => x.Value.ToString()).ToList(); if (categories.Count > 0) { <h5 class="facetheader">Category:</h5> <ul class="facetlist"> @for (var c = 0; c < categories.Count; c++) { var facetLink = $"{categories[c]} ({Model.resultList.Facets["Category"][c].Count})"; <li> @Html.ActionLink(facetLink, "FacetAsync", "Home", new { categoryFilter = $"Category eq '{categories[c]}'" }, null) </li> } </ul> } List<string> tags = Model.resultList.Facets["Tags"].Select(x => x.Value.ToString()).ToList(); if (tags.Count > 0) { <h5 class="facetheader">Amenities:</h5> <ul class="facetlist"> @for (var c = 0; c < tags.Count; c++) { var facetLink = $"{tags[c]} ({Model.resultList.Facets["Tags"][c].Count})"; <li> @Html.ActionLink(facetLink, "FacetAsync", "Home", new { amenityFilter = $"Tags/any(t: t eq '{tags[c]}')" }, null) </li> } </ul> } } </div> </td> <td valign="top"> <div id="resultsplace"> @if (Model != null && Model.resultList != null) { // Show the result count. <p class="sampleText"> @Model.resultList.TotalCount Results </p> var results = Model.resultList.GetResults().ToList(); @for (var i = 0; i < results.Count; i++) { string amenities = string.Join(", ", results[i].Document.Tags); string fullDescription = results[i].Document.Description; fullDescription += $"\nCategory: {results[i].Document.Category}"; fullDescription += $"\nAmenities: {amenities}"; // Display the hotel name and description. @Html.TextAreaFor(m => results[i].Document.HotelName, new { @class = "box1" }) @Html.TextArea($"desc{i}", fullDescription, new { @class = "box2" }) } } </div> </td> </tr> <tr> <td></td> <td valign="top"> @if (Model != null && Model.pageCount > 1) { // If there is more than one page of results, show the paging buttons. <table> <tr> <td class="tdPage"> @if (Model.currentPage > 0) { <p class="pageButton"> @Html.ActionLink("|<", "PageAsync", "Home", new { paging = "0" }, null) </p> } else { <p class="pageButtonDisabled">|<</p> } </td> <td class="tdPage"> @if (Model.currentPage > 0) { <p class="pageButton"> @Html.ActionLink("<", "PageAsync", "Home", new { paging = "prev" }, null) </p> } else { <p class="pageButtonDisabled"><</p> } </td> @for (var pn = Model.leftMostPage; pn < Model.leftMostPage + Model.pageRange; pn++) { <td class="tdPage"> @if (Model.currentPage == pn) { // Convert displayed page numbers to 1-based and not 0-based. <p class="pageSelected">@(pn + 1)</p> } else { <p class="pageButton"> @Html.ActionLink((pn + 1).ToString(), "PageAsync", "Home", new { paging = @pn }, null) </p> } </td> } <td class="tdPage"> @if (Model.currentPage < Model.pageCount - 1) { <p class="pageButton"> @Html.ActionLink(">", "PageAsync", "Home", new { paging = "next" }, null) </p> } else { <p class="pageButtonDisabled">></p> } </td> <td class="tdPage"> @if (Model.currentPage < Model.pageCount - 1) { <p class="pageButton"> @Html.ActionLink(">|", "PageAsync", "Home", new { paging = Model.pageCount - 1 }, null) </p> } else { <p class="pageButtonDisabled">>|</p> } </td> </tr> </table> } </td> </tr> </table> } </body>`

Notice the use of the

**Html.ActionLink**call. This call communicates valid filter strings to the controller, when the user clicks a facet link.

### Run and test the app

The advantage of facet navigation to the user is that they can narrow searches with a single click, which we can show in the following sequence.

Run the app, type "airport" as the search text. Verify that the list of facets appears neatly to the left. These facets are all that apply to hotels that have "airport" in their text data, with a count of how often they occur.

Click the

**Resort and Spa**category. Verify all results are in this category.Click the

**continental breakfast**amenity. Verify all results are still in the "Resort and Spa" category, with the selected amenity.Try selecting any other category, then one amenity, and view the narrowing results. Then try the other way around, one amenity, then one category. Send an empty search to reset the page.

Note

When one selection is made in a facet list (such as category) it will override any previous selection within the category list.


## Takeaways

Consider the following takeaways from this project:

- It is imperative to mark each facetable field with the
**IsFacetable**property for inclusion in facet navigation. - Facets are combined with filters to reduce the results.
- Facets are cumulative, with each selection building on the previous one to further narrow results.

## Next steps

In the next tutorial, we look at ordering results. Up to this point, results are ordered simply in the order that they are located in the database.
