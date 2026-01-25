---
source_url: https://learn.microsoft.com/en-us/azure/search/tutorial-csharp-search-query-integration
fetched_at: 2026-01-25T02:11:12.033529
---

# Step 4 - Explore the .NET search code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In the previous lessons, you added search to a static web app. This lesson highlights the essential steps that establish integration. If you're looking for a cheat sheet on how to integrate search into your web app, this article explains what you need to know.

## Azure SDK Azure.Search.Documents

The Function app uses the Azure SDK for Azure AI Search:

- NuGet:
[Azure.Search.Documents](https://www.nuget.org/packages/Azure.Search.Documents/) - Reference Documentation:
[Client Library](/en-us/dotnet/api/overview/azure/search)

The function app authenticates through the SDK to the cloud-based Azure AI Search API using your resource name, resource key, and index name. The secrets are stored in the static web app settings and pulled in to the function as environment variables.

## Configure secrets in a local.settings.json file

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "",
"FUNCTIONS_WORKER_RUNTIME": "dotnet-isolated",
"SearchApiKey": "",
"SearchServiceName": "",
"SearchIndexName": "good-books"
},
"Host": {
"CORS": "*"
}
}
```


## Azure Function: Search the catalog

The [Search API](https://github.com/Azure-Samples/azure-search-static-web-app/blob/main/api/Search.cs) takes a search term and searches across the documents in the search index, returning a list of matches. Through the Suggest API, partial strings are sent to the search engine as the user types, suggesting search terms such as book titles and authors across the documents in the search index, and returning a small list of matches.

The Azure function pulls in the search configuration information, and fulfills the query.

The search suggester, `sg`

, is defined in the [schema file](https://github.com/Azure-Samples/azure-search-static-web-app/blob/main/bulk-insert/BookSearchIndex.cs) used during bulk upload.

```
using Azure;
using Azure.Core.Serialization;
using Azure.Search.Documents;
using Azure.Search.Documents.Models;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Extensions.Logging;
using System.Net;
using System.Text.Json;
using System.Text.Json.Serialization;
using WebSearch.Models;
using SearchFilter = WebSearch.Models.SearchFilter;
namespace WebSearch.Function
{
public class Search
{
private static string searchApiKey = Environment.GetEnvironmentVariable("SearchApiKey", EnvironmentVariableTarget.Process);
private static string searchServiceName = Environment.GetEnvironmentVariable("SearchServiceName", EnvironmentVariableTarget.Process);
private static string searchIndexName = Environment.GetEnvironmentVariable("SearchIndexName", EnvironmentVariableTarget.Process) ?? "good-books";
private readonly ILogger<Lookup> _logger;
public Search(ILogger<Lookup> logger)
{
_logger = logger;
}
[Function("search")]
public async Task<HttpResponseData> RunAsync(
[HttpTrigger(AuthorizationLevel.Anonymous, "post")] HttpRequestData req,
FunctionContext executionContext)
{
string requestBody = await new StreamReader(req.Body).ReadToEndAsync();
var data = JsonSerializer.Deserialize<RequestBodySearch>(requestBody);
// Azure AI Search
Uri serviceEndpoint = new($"https://{searchServiceName}.search.windows.net/");
SearchClient searchClient = new(
serviceEndpoint,
searchIndexName,
new AzureKeyCredential(searchApiKey)
);
SearchOptions options = new()
{
Size = data.Size,
Skip = data.Skip,
IncludeTotalCount = true,
Filter = CreateFilterExpression(data.Filters)
};
options.Facets.Add("authors");
options.Facets.Add("language_code");
SearchResults<SearchDocument> searchResults = searchClient.Search<SearchDocument>(data.SearchText, options);
var facetOutput = new Dictionary<string, IList<FacetValue>>();
foreach (var facetResult in searchResults.Facets)
{
facetOutput[facetResult.Key] = facetResult.Value
.Select(x => new FacetValue { value = x.Value.ToString(), count = x.Count })
.ToList();
}
// Data to return
var output = new SearchOutput
{
Count = searchResults.TotalCount,
Results = searchResults.GetResults().ToList(),
Facets = facetOutput
};
var response = req.CreateResponse(HttpStatusCode.Found);
// Serialize data
var serializer = new JsonObjectSerializer(
new JsonSerializerOptions(JsonSerializerDefaults.Web));
await response.WriteAsJsonAsync(output, serializer);
return response;
}
public static string CreateFilterExpression(List<SearchFilter> filters)
{
if (filters is null or { Count: <= 0 })
{
return null;
}
List<string> filterExpressions = new();
List<SearchFilter> authorFilters = filters.Where(f => f.field == "authors").ToList();
List<SearchFilter> languageFilters = filters.Where(f => f.field == "language_code").ToList();
List<string> authorFilterValues = authorFilters.Select(f => f.value).ToList();
if (authorFilterValues.Count > 0)
{
string filterStr = string.Join(",", authorFilterValues);
filterExpressions.Add($"{"authors"}/any(t: search.in(t, '{filterStr}', ','))");
}
List<string> languageFilterValues = languageFilters.Select(f => f.value).ToList();
foreach (var value in languageFilterValues)
{
filterExpressions.Add($"language_code eq '{value}'");
}
return string.Join(" and ", filterExpressions);
}
}
}
```


## Client: Search from the catalog

Call the Azure Function in the React client at `\client\src\pages\Search\Search.jsx`

with the following code to search for books.

```
import React, { useEffect, useState, Suspense } from 'react';
import fetchInstance from '../../url-fetch';
import CircularProgress from '@mui/material/CircularProgress';
import { useLocation, useNavigate } from "react-router-dom";
import Results from '../../components/Results/Results';
import Pager from '../../components/Pager/Pager';
import Facets from '../../components/Facets/Facets';
import SearchBar from '../../components/SearchBar/SearchBar';
import "./Search.css";
export default function Search() {
let location = useLocation();
const navigate = useNavigate();
const [results, setResults] = useState([]);
const [resultCount, setResultCount] = useState(0);
const [currentPage, setCurrentPage] = useState(1);
const [q, setQ] = useState(new URLSearchParams(location.search).get('q') ?? "*");
const [top] = useState(new URLSearchParams(location.search).get('top') ?? 8);
const [skip, setSkip] = useState(new URLSearchParams(location.search).get('skip') ?? 0);
const [filters, setFilters] = useState([]);
const [facets, setFacets] = useState({});
const [isLoading, setIsLoading] = useState(true);
let resultsPerPage = top;
// Handle page changes in a controlled manner
function handlePageChange(newPage) {
setCurrentPage(newPage);
}
// Calculate skip value and fetch results when relevant parameters change
useEffect(() => {
// Calculate skip based on current page
const calculatedSkip = (currentPage - 1) * top;
// Only update if skip has actually changed
if (calculatedSkip !== skip) {
setSkip(calculatedSkip);
return; // Skip the fetch since skip will change and trigger another useEffect
}
// Proceed with fetch
setIsLoading(true);
const body = {
q: q,
top: top,
skip: skip,
filters: filters
};
fetchInstance('/api/search', { body, method: 'POST' })
.then(response => {
setResults(response.results);
setFacets(response.facets);
setResultCount(response.count);
setIsLoading(false);
})
.catch(error => {
console.log(error);
setIsLoading(false);
});
}, [q, top, skip, filters, currentPage]);
// pushing the new search term to history when q is updated
// allows the back button to work as expected when coming back from the details page
useEffect(() => {
navigate('/search?q=' + q);
setCurrentPage(1);
setFilters([]);
// eslint-disable-next-line react-hooks/exhaustive-deps
}, [q]);
let postSearchHandler = (searchTerm) => {
setQ(searchTerm);
}
// filters should be applied across entire result set,
// not just within the current page
const updateFilterHandler = (newFilters) => {
// Reset paging
setSkip(0);
setCurrentPage(1);
// Set filters
setFilters(newFilters);
};
return (
<main className="main main--search container-fluid">
<div className="row">
<div className="search-bar-column col-md-3">
<div className="search-bar-column-container">
<SearchBar postSearchHandler={postSearchHandler} query={q} width={false}></SearchBar>
</div>
<Facets facets={facets} filters={filters} setFilters={updateFilterHandler}></Facets>
</div>
<div className="search-bar-results">
{isLoading ? (
<div className="col-md-9">
<CircularProgress />
</div>
) : (
<div className="search-results-container">
<Results documents={results} top={top} skip={skip} count={resultCount} query={q}></Results>
<Pager className="pager-style" currentPage={currentPage} resultCount={resultCount} resultsPerPage={resultsPerPage} onPageChange={handlePageChange}></Pager>
</div>
)}
</div>
</div>
</main>
);
}
```


## Client: Suggestions from the catalog

The Suggest function API is called in the React app at `\client\src\components\SearchBar\SearchBar.jsx`

as part of the [Material UI's Autocomplete component](https://mui.com/material-ui/react-autocomplete/). This component uses the input text to search for authors and books that match the input text then displays those possible matches at selectable items in the drop-down list.

```
import React, { useState, useEffect } from 'react';
import { TextField, Autocomplete, Button, Box } from '@mui/material';
import fetchInstance from '../../url-fetch';
import './SearchBar.css';
export default function SearchBar({ postSearchHandler, query, width }) {
const [q, setQ] = useState(() => query || '');
const [suggestions, setSuggestions] = useState([]);
const search = (value) => {
postSearchHandler(value);
};
useEffect(() => {
if (q) {
const body = { q, top: 5, suggester: 'sg' };
fetchInstance('/api/suggest', { body, method: 'POST' })
.then(response => {
setSuggestions(response.suggestions.map(s => s.text));
})
.catch(error => {
console.log(error);
setSuggestions([]);
});
}
}, [q]);
const onInputChangeHandler = (event, value) => {
setQ(value);
};
const onChangeHandler = (event, value) => {
setQ(value);
search(value);
};
const onEnterButton = (event) => {
// if enter key is pressed
if (event.key === 'Enter') {
search(q);
}
};
return (
<div
className={width ? "search-bar search-bar-wide" : "search-bar search-bar-narrow"}
>
<Box className="search-bar-box">
<Autocomplete
className="autocomplete"
freeSolo
value={q}
options={suggestions}
onInputChange={onInputChangeHandler}
onChange={onChangeHandler}
disableClearable
renderInput={(params) => (
<TextField
{...params}
id="search-box"
className="form-control rounded-0"
placeholder="What are you looking for?"
onBlur={() => setSuggestions([])}
onClick={() => setSuggestions([])}
/>
)}
/>
<div className="search-button" >
<Button variant="contained" color="primary" onClick={() => {
search(q)
}
}>
Search
</Button>
</div>
</Box>
</div>
);
}
```


## Azure Function: Get specific document

The [Document Lookup API](https://github.com/Azure-Samples/azure-search-static-web-app/blob/main/api/Lookup.cs) takes an ID and returns the document object from the Search Index.

```
using Azure;
using Azure.Core.Serialization;
using Azure.Search.Documents;
using Azure.Search.Documents.Models;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Http;
using Microsoft.Extensions.Logging;
using System.Net;
using System.Text.Json;
using WebSearch.Models;
namespace WebSearch.Function
{
public class Lookup
{
private static string searchApiKey = Environment.GetEnvironmentVariable("SearchApiKey", EnvironmentVariableTarget.Process);
private static string searchServiceName = Environment.GetEnvironmentVariable("SearchServiceName", EnvironmentVariableTarget.Process);
private static string searchIndexName = Environment.GetEnvironmentVariable("SearchIndexName", EnvironmentVariableTarget.Process) ?? "good-books";
private readonly ILogger<Lookup> _logger;
public Lookup(ILogger<Lookup> logger)
{
_logger = logger;
}
[Function("lookup")]
public async Task<HttpResponseData> RunAsync(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
// Get Document Id
var query = System.Web.HttpUtility.ParseQueryString(req.Url.Query);
string documentId = query["id"].ToString();
// Azure AI Search
Uri serviceEndpoint = new($"https://{searchServiceName}.search.windows.net/");
SearchClient searchClient = new(
serviceEndpoint,
searchIndexName,
new AzureKeyCredential(searchApiKey)
);
var getDocumentResponse = await searchClient.GetDocumentAsync<SearchDocument>(documentId);
// Data to return
var output = new LookupOutput
{
Document = getDocumentResponse.Value
};
var response = req.CreateResponse(HttpStatusCode.Found);
// Serialize data
var serializer = new JsonObjectSerializer(
new JsonSerializerOptions(JsonSerializerDefaults.Web));
await response.WriteAsJsonAsync(output, serializer);
return response;
}
}
}
```


## Client: Get specific document

This function API is called in the React app at `\client\src\pages\Details\Details.jsx`

as part of component initialization:

```
import React, { useState, useEffect } from "react";
import { useParams } from 'react-router-dom';
import Rating from '@mui/material/Rating';
import CircularProgress from '@mui/material/CircularProgress';
import Tabs from '@mui/material/Tabs';
import Tab from '@mui/material/Tab';
import Box from '@mui/material/Box';
import fetchInstance from '../../url-fetch';
import "./Details.css";
function CustomTabPanel(props) {
const { children, value, index, ...other } = props;
return (
<div
className="tab-panel"
role="tabpanel"
hidden={value !== index}
id={`simple-tabpanel-${index}`}
aria-labelledby={`simple-tab-${index}`}
{...other}
// Ensure it takes full width
>
{value === index && <Box className="tab-panel-value">{children}</Box>}
</div>
);
}
export default function BasicTabs() {
const { id } = useParams();
const [document, setDocument] = useState({});
const [value, setValue] = React.useState(0);
const [isLoading, setIsLoading] = useState(true);
useEffect(() => {
setIsLoading(true);
fetchInstance('/api/lookup', { query: { id } })
.then(response => {
console.log(JSON.stringify(response))
const doc = response.document;
setDocument(doc);
setIsLoading(false);
})
.catch(error => {
console.log(error);
setIsLoading(false);
});
}, [id]);
const handleChange = (event, newValue) => {
setValue(newValue);
};
if (isLoading || !id || Object.keys(document).length === 0) {
return (
<div className="loading-container">
<CircularProgress />
<p>Loading...</p>
</div>
);
}
return (
<Box className="details-box-parent">
<Box className="details-tab-box-header">
<Tabs value={value} onChange={handleChange} aria-label="book-details-tabs">
<Tab label="Result" />
<Tab label="Raw Data" />
</Tabs>
</Box>
<CustomTabPanel value={value} index={0} className="tab-panel box-content">
<div className="card-body">
<h5 className="card-title">{document.original_title}</h5>
<img className="image" src={document.image_url} alt="Book cover"></img>
<p className="card-text">{document.authors?.join('; ')} - {document.original_publication_year}</p>
<p className="card-text">ISBN {document.isbn}</p>
<Rating name="half-rating-read" value={parseInt(document.average_rating)} precision={0.1} readOnly></Rating>
<p className="card-text">{document.ratings_count} Ratings</p>
</div>
</CustomTabPanel>
<CustomTabPanel value={value} index={1} className="tab-panel">
<div className="card-body text-left card-text details-custom-tab-panel-json-div" >
<pre><code>
{JSON.stringify(document, null, 2)}
</code></pre>
</div>
</CustomTabPanel>
</Box>
);
}
```


## C# models to support function app

The following models are used to support the functions in this app.

```
using Azure.Search.Documents.Models;
using System.Text.Json.Serialization;
namespace WebSearch.Models
{
public class RequestBodyLookUp
{
[JsonPropertyName("id")]
public string Id { get; set; }
}
public class RequestBodySuggest
{
[JsonPropertyName("q")]
public string SearchText { get; set; }
[JsonPropertyName("top")]
public int Size { get; set; }
[JsonPropertyName("suggester")]
public string SuggesterName { get; set; }
}
public class RequestBodySearch
{
[JsonPropertyName("q")]
public string SearchText { get; set; }
[JsonPropertyName("skip")]
public int Skip { get; set; }
[JsonPropertyName("top")]
public int Size { get; set; }
[JsonPropertyName("filters")]
public List<SearchFilter> Filters { get; set; }
}
public class SearchFilter
{
public string field { get; set; }
public string value { get; set; }
}
public class FacetValue
{
public string value { get; set; }
public long? count { get; set; }
}
class SearchOutput
{
[JsonPropertyName("count")]
public long? Count { get; set; }
[JsonPropertyName("results")]
public List<SearchResult<SearchDocument>> Results { get; set; }
[JsonPropertyName("facets")]
public Dictionary<String, IList<FacetValue>> Facets { get; set; }
}
class LookupOutput
{
[JsonPropertyName("document")]
public SearchDocument Document { get; set; }
}
public class BookModel
{
public string id { get; set; }
public decimal? goodreads_book_id { get; set; }
public decimal? best_book_id { get; set; }
public decimal? work_id { get; set; }
public decimal? books_count { get; set; }
public string isbn { get; set; }
public string isbn13 { get; set; }
public string[] authors { get; set; }
public decimal? original_publication_year { get; set; }
public string original_title { get; set; }
public string title { get; set; }
public string language_code { get; set; }
public double? average_rating { get; set; }
public decimal? ratings_count { get; set; }
public decimal? work_ratings_count { get; set; }
public decimal? work_text_reviews_count { get; set; }
public decimal? ratings_1 { get; set; }
public decimal? ratings_2 { get; set; }
public decimal? ratings_3 { get; set; }
public decimal? ratings_4 { get; set; }
public decimal? ratings_5 { get; set; }
public string image_url { get; set; }
public string small_image_url { get; set; }
}
}
```


## Next steps

To continue learning more about Azure AI Search development, try this next tutorial about indexing: