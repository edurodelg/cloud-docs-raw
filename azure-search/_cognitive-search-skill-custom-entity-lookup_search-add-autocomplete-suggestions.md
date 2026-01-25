---
merged_at: 2026-01-25T02:11:58.478689
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-custom-entity-lookup.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-custom-entity-lookup -->

# Custom Entity Lookup cognitive skill

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The **Custom Entity Lookup** skill is used to detect or recognize entities that you define. During skillset execution, the skill looks for text from a custom, user-defined list of words and phrases. The skill uses this list to label any matching entities found within source documents. The skill also supports a degree of fuzzy matching that can be applied to find matches that are similar but not exact.

Note

This skill isn't bound to a Foundry Tools API but requires a Foundry Tools key to allow more than 20 transactions. This skill is [metered by Azure AI Search](https://azure.microsoft.com/pricing/details/search/#pricing).

## @odata.type

Microsoft.Skills.Text.CustomEntityLookupSkill

## Data limits

- The maximum input record size supported is 256 MB. If you need to break up your data before sending it to the custom entity lookup skill, consider using the
[Text Split skill](cognitive-search-skill-textsplit). If you do use a text split skill, set the page length to 5000 for the best performance. - The maximum size of the custom entity definition is 10 MB if it's provided as an external file, specified through the "entitiesDefinitionUri" parameter.
- If the entities are defined inline using the "inlineEntitiesDefinition" parameter, the maximum size is 10 KB.

## Skill parameters

Parameters are case sensitive.

| Parameter name | Description |
|---|---|
`entitiesDefinitionUri` |
Path to an external JSON or CSV file containing all the target text to match against. This entity definition is read at the beginning of an indexer run; any updates to this file mid-run won't be realized until subsequent runs. This file must be accessible over HTTPS. See
|

`inlineEntitiesDefinition`

[Custom Entity Definition](#custom-entity-definition-format)below for expected JSON schema.`defaultLanguageCode`

`da, de, en, es, fi, fr, it, pt`

. The default is English (`en`

). If you pass a `languagecode-countrycode`

format, only the `languagecode`

part of the format is used.`globalDefaultCaseSensitive`

`defaultCaseSensitive`

value of an entity isn't specified, this value will become the `defaultCaseSensitive`

value for that entity.`globalDefaultAccentSensitive`

`defaultAccentSensitive`

value of an entity isn't specified, this value will become the `defaultAccentSensitive`

value for that entity.`globalDefaultFuzzyEditDistance`

`defaultFuzzyEditDistance`

value of an entity isn't specified, this value will become the `defaultFuzzyEditDistance`

value for that entity.## Skill inputs

| Input name | Description |
|---|---|
`text` |
The text to analyze. |
`languageCode` |
Optional. Default is `"en"` . |

## Skill outputs

| Output name | Description |
|---|---|
`entities` |
An array of complex types that contains the following fields:
|

## Custom entity definition format

There are three approaches for providing the list of custom entities to the Custom Entity Lookup skill:

- .CSV file (UTF-8 encoded)
- .JSON file (UTF-8 encoded)
- Inline within the skill definition

If the definition file is in a .CSV or .JSON file, provide the full path in the "entitiesDefinitionUri" parameter. The file is downloaded at the start of each indexer run. It must remain accessible until the indexer stops.

If you're using an inline definition, specify it under the "inlineEntitiesDefinition" skill parameter.

Note

Indexers support specialized parsing modes for JSON and CSV files. When using the custom entity lookup skill, keep "parsingMode" set to "default". The skill expects JSON and CSV in an unparsed state.

### CSV format

You can provide the definition of the custom entities to look for in a Comma-Separated Value (CSV) file by providing the path to the file and setting it in the "entitiesDefinitionUri" skill parameter. The path should be at an https location. The definition file can be up to 10 MB in size.

The CSV format is simple. Each line represents a unique entity, as shown below:

```
Bill Gates, BillG, William H. Gates
Microsoft, MSFT
Satya Nadella
```


In this case, there are three entities that can be returned (Bill Gates, Satya Nadella, Microsoft). Aliases follow after the main entity. A match on an alias is bundled under the primary entity. For example, if the string "William H. Gates" is found in a document, a match for the "Bill Gates" entity will be returned.

### JSON format

You can provide the definition of the custom entities to look for in a JSON file as well. The JSON format gives you a bit more flexibility since it allows you to define matching rules per term. For instance, you can specify the fuzzy matching distance (Damerau-Levenshtein distance) for each term or whether the matching should be case-sensitive or not.

Just like with CSV files, you need to provide the path to the JSON file and set it in the "entitiesDefinitionUri" skill parameter. The path should be at an https location. The definition file can be up to 10 MB in size.

The most basic JSON custom entity list definition can be a list of entities to match:

```
[
{
"name" : "Bill Gates"
},
{
"name" : "Microsoft"
},
{
"name" : "Satya Nadella"
}
]
```


More complex definitions can provide a user-defined ID, description, type, subtype, and aliases. If an alias term is matched, the entity will be returned as well:

```
[
{
"name" : "Bill Gates",
"description" : "Microsoft founder." ,
"aliases" : [
{ "text" : "William H. Gates", "caseSensitive" : false },
{ "text" : "BillG", "caseSensitive" : true }
]
},
{
"name" : "Xbox One",
"type": "Hardware",
"subtype" : "Gaming Device",
"id" : "4e36bf9d-5550-4396-8647-8e43d7564a76",
"description" : "The Xbox One product"
},
{
"name" : "LinkedIn" ,
"description" : "The LinkedIn company",
"id" : "differentIdentifyingScheme123",
"fuzzyEditDistance" : 0
},
{
"name" : "Microsoft" ,
"description" : "Microsoft Corporation",
"id" : "differentIdentifyingScheme987",
"defaultCaseSensitive" : false,
"defaultFuzzyEditDistance" : 1,
"aliases" : [
{ "text" : "MSFT", "caseSensitive" : true }
]
}
]
```


The tables below describe the configuration parameters you can set when defining custom entities:

| Field name | Description |
|---|---|
`name` |
The top-level entity descriptor. Matches in the skill output will be grouped by this name, and it should represent the "normalized" form of the text being found. |
`description` |
(Optional) This field can be used as a passthrough for custom metadata about the matched text(s). The value of this field will appear with every match of its entity in the skill output. |
`type` |
(Optional) This field can be used as a passthrough for custom metadata about the matched text(s). The value of this field will appear with every match of its entity in the skill output. |
`subtype` |
(Optional) This field can be used as a passthrough for custom metadata about the matched text(s). The value of this field will appear with every match of its entity in the skill output. |
`id` |
(Optional) This field can be used as a passthrough for custom metadata about the matched text(s). The value of this field will appear with every match of its entity in the skill output. |
`caseSensitive` |
(Optional) Defaults to false. Boolean value denoting whether comparisons with the entity name should be sensitive to character casing. Sample case insensitive matches of "Microsoft" could be: microsoft, microSoft, MICROSOFT |
`accentSensitive` |
(Optional) Defaults to false. Boolean value denoting whether accented and unaccented letters such as 'é' and 'e' should be identical. |
`fuzzyEditDistance` |
(Optional) Defaults to 0. Maximum value of 5. Denotes the acceptable number of divergent characters that would still constitute a match with the entity name. The smallest possible fuzziness for any given match is returned. For instance, if the edit distance is set to 3, "Windows 10" would still match "Windows", "Windows10" and "windows 7". When case sensitivity is set to false, case differences do NOT count towards fuzziness tolerance, but otherwise do. |
`defaultCaseSensitive` |
(Optional) Changes the default case sensitivity value for this entity. It can be used to change the default value of all aliases caseSensitive values. |
`defaultAccentSensitive` |
(Optional) Changes the default accent sensitivity value for this entity. It can be used to change the default value of all aliases accentSensitive values. |
`defaultFuzzyEditDistance` |
(Optional) Changes the default fuzzy edit distance value for this entity. It can be used to change the default value of all aliases fuzzyEditDistance values. |
`aliases` |
(Optional) An array of complex objects that can be used to specify alternative spellings or synonyms to the root entity name. |

| Alias properties | Description |
|---|---|
`text` |
The alternative spelling or representation of some target entity name. |
`caseSensitive` |
(Optional) Acts the same as root entity "caseSensitive" parameter above, but applies to only this one alias. |
`accentSensitive` |
(Optional) Acts the same as root entity "accentSensitive" parameter above, but applies to only this one alias. |
`fuzzyEditDistance` |
(Optional) Acts the same as root entity "fuzzyEditDistance" parameter above, but applies to only this one alias. |

### Inline format

In some cases, it may be more convenient to embed the custom entity definition so that its inline with the skill definition. You can use the same JSON format as the one described above, except that it's included within the skill definition. Only configurations that are less than 10 KB in size (serialized size) can be defined inline.

## Sample skill definition

A sample skill definition using an inline format is shown below:

```
{
"@odata.type": "#Microsoft.Skills.Text.CustomEntityLookupSkill",
"context": "/document",
"inlineEntitiesDefinition":
[
{
"name" : "Bill Gates",
"description" : "Microsoft founder." ,
"aliases" : [
{ "text" : "William H. Gates", "caseSensitive" : false },
{ "text" : "BillG", "caseSensitive" : true }
]
},
{
"name" : "Xbox One",
"type": "Hardware",
"subtype" : "Gaming Device",
"id" : "4e36bf9d-5550-4396-8647-8e43d7564a76",
"description" : "The Xbox One product"
}
],
"inputs": [
{
"name": "text",
"source": "/document/content"
}
],
"outputs": [
{
"name": "entities",
"targetName": "matchedEntities"
}
]
}
```


Alternatively, you can point to an external entities definition file. A sample skill definition using the `entitiesDefinitionUri`

format is shown below:

```
{
"@odata.type": "#Microsoft.Skills.Text.CustomEntityLookupSkill",
"context": "/document",
"entitiesDefinitionUri": "https://myblobhost.net/keyWordsConfig.csv",
"inputs": [
{
"name": "text",
"source": "/document/content"
}
],
"outputs": [
{
"name": "entities",
"targetName": "matchedEntities"
}
]
}
```


## Sample index definition

This section provides a sample index definition. Both "entities" and "matches" are arrays of complex types. You can have multiple entities per document, and multiple matches for each entity.

```
{
"name": "entities",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "name",
"type": "Edm.String",
"facetable": false,
"filterable": false,
"retrievable": true,
"searchable": true,
"sortable": false,
},
{
"name": "id",
"type": "Edm.String",
"facetable": false,
"filterable": false,
"retrievable": true,
"searchable": false,
"sortable": false,
},
{
"name": "description",
"type": "Edm.String",
"facetable": false,
"filterable": false,
"retrievable": true,
"searchable": true,
"sortable": false,
},
{
"name": "type",
"type": "Edm.String",
"facetable": true,
"filterable": true,
"retrievable": true,
"searchable": false,
"sortable": false,
},
{
"name": "subtype",
"type": "Edm.String",
"facetable": true,
"filterable": true,
"retrievable": true,
"searchable": false,
"sortable": false,
},
{
"name": "matches",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "text",
"type": "Edm.String",
"facetable": false,
"filterable": false,
"retrievable": true,
"searchable": true,
"sortable": false,
},
{
"name": "offset",
"type": "Edm.Int32",
"facetable": true,
"filterable": true,
"retrievable": true,
"sortable": false,
},
{
"name": "length",
"type": "Edm.Int32",
"facetable": true,
"filterable": true,
"retrievable": true,
"sortable": false,
},
{
"name": "matchDistance",
"type": "Edm.Double",
"facetable": true,
"filterable": true,
"retrievable": true,
"sortable": false,
}
]
}
]
}
```


## Sample input data

```
{
"values": [
{
"recordId": "1",
"data":
{
"text": "The company, Microsoft, was founded by Bill Gates. Microsoft's gaming console is called Xbox",
"languageCode": "en"
}
}
]
}
```


## Sample output

```
{
"values" :
[
{
"recordId": "1",
"data" : {
"entities": [
{
"name" : "Microsoft",
"description" : "This document refers to Microsoft the company",
"id" : "differentIdentifyingScheme987",
"matches" : [
{
"text" : "microsoft",
"offset" : 13,
"length" : 9,
"matchDistance" : 0
},
{
"text" : "Microsoft",
"offset" : 49,
"length" : 9,
"matchDistance" : 0
}
]
},
{
"name" : "Bill Gates",
"description" : "William Henry Gates III, founder of Microsoft.",
"matches" : [
{
"text" : "Bill Gates",
"offset" : 37,
"length" : 10,
"matchDistance" : 0
}
]
}
]
}
}
]
}
```


## Warnings

`"Reached maximum capacity for matches, skipping all further duplicate matches."`


This warning will be emitted if the number of matches detected is greater than the maximum allowed. No more duplicate matches will be returned. If you need a higher threshold, you can file a [support ticket](https://portal.azure.com/#create/Microsoft.Support) for assistance with your individual use case.


---

<!-- DOCUMENTO FUSIONADO: search-add-autocomplete-suggestions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-add-autocomplete-suggestions -->

# Add autocomplete and search suggestions in client apps

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Search-as-you-type is a common technique for improving query productivity. In Azure AI Search, this experience is supported through *autocomplete*, which finishes a term or phrase based on partial input (for example, completing *micro* with *microchip*, *microscope*, *microsoft*, and any other micro matches). A second user experience is *suggestions*, which produces a short list of matching documents (for example, returning book titles with an ID so that you can link to a detail page about that book). Both autocomplete and suggestions are predicated on a match in the index. The service doesn't offer autocompleted queries or suggestions that return zero results.

To implement these experiences in Azure AI Search:

- Add a
`suggester`

to an index schema. - Build a query that calls the
[Autocomplete API](/en-us/rest/api/searchservice/documents/autocomplete-post)or[Suggestions API](/en-us/rest/api/searchservice/documents/suggest-post)on the request. - Add a UI control to handle search-as-you-type interactions in your client app. We recommend using an existing JavaScript library for this purpose.

In Azure AI Search, autocompleted queries and suggested results are retrieved from the search index, from selected fields that you register with a suggester. A suggester is part of the index, and it specifies which fields provide content that either completes a query, suggests a result, or does both. When the index is created and loaded, a suggester data structure is created internally to store prefixes used for matching on partial queries. For suggestions, choosing suitable fields that are unique, or at least not repetitive, is essential to the experience. For more information, see [Configure a suggester](index-add-suggesters).

The remainder of this article is focused on queries and client code. It uses JavaScript and C# to illustrate key points. REST API examples are used to concisely present each operation. For end-to-end code samples, see [Add search to a web site with .NET](tutorial-csharp-overview).

## Set up a request

Elements of a request include one of the search-as-you-type APIs, a partial query, and a suggester. The following script illustrates components of a request, using the Autocomplete REST API as an example.

```
POST /indexes/myxboxgames/docs/autocomplete?search&api-version=2025-09-01
{
"search": "minecraf",
"suggesterName": "sg"
}
```


The `suggesterName`

parameter gives you the suggester-aware fields used to complete terms or suggestions. For suggestions in particular, the field list should be composed of suggestions that offer clear choices among matching results. On a site that sells computer games, the field might be the game title.

The `search`

parameter provides the partial query, where characters are fed to the query request through the jQuery Autocomplete control. In the previous example, *minecraf* is a static illustration of what the control might pass in.

The APIs don't impose minimum length requirements on the partial query; it can be as little as one character. However, jQuery Autocomplete provides a minimum length. A minimum of two or three characters is typical.

Matches are on the beginning of a term anywhere in the input string. Given *the quick brown fox*, both autocomplete and suggestions match on partial versions of *the*, *quick*, *brown*, or *fox* but not on partial infix terms like *rown* or *ox*. Furthermore, each match sets the scope for downstream expansions. A partial query of *quick br* matches on *quick brown* or *quick bread*, but neither *brown* or *bread* by themselves would be a match unless quick* precedes them.

### APIs for search-as-you-type

Follow these links for the REST and .NET SDK reference pages:

## Structure a response

Responses for autocomplete and suggestions are what you might expect for the pattern: [Autocomplete](/en-us/rest/api/searchservice/documents/autocomplete-post#responses) returns a list of terms, [Suggestions](/en-us/rest/api/searchservice/documents/suggest-post#response) returns terms plus a document ID so that you can fetch the document (use the [Lookup Document API](/en-us/rest/api/searchservice/documents/get) to fetch the specific document for a detail page).

Responses are shaped by the parameters on the request:

For autocomplete, set the

[autocompleteMode](/en-us/rest/api/searchservice/documents/autocomplete-post#autocompletemode)to determine whether text completion occurs on one or two terms.For suggestions, set

[$select](/en-us/rest/api/searchservice/documents/suggest-post#request-body)to return fields containing unique or differentiating values, such as names and description. Avoid fields that contain duplicate values (such as a category or city).

The following parameters apply to both autocomplete and suggestions, but are more applicable to suggestions, especially when a suggester includes multiple fields.

| Parameter | Usage |
|---|---|
| searchFields | Constrain the query to specific fields. |
| $filter | Apply match criteria on the result set (`$filter=Category eq 'ActionAdventure'` ). |
| $top | Limit the results to a specific number (`$top=5` ). |

## Add user interaction code

Autofilling a query term or dropping down a list of matching links requires user interaction code, typically JavaScript, that can consume requests from external sources, such as autocomplete or suggestion queries against an Azure Search Cognitive index.

Although you could write this code natively, it's easier to use functions from existing JavaScript library, such as one of the following.

[Autocomplete widget (jQuery UI)](https://jqueryui.com/autocomplete/)appears in the suggestion code snippet. You can create a search box, and then reference it in a JavaScript function that uses the autocomplete widget. Properties on the widget set the source (an autocomplete or suggestions function), minimum length of input characters before action is taken, and positioning.[XDSoft Autocomplete plug-in](https://xdsoft.net/jqplugins/autocomplete/)appears in the autocomplete code snippet.[Suggestions](https://www.npmjs.com/package/suggestions)appears in the[Add search to web sites tutorial](tutorial-csharp-overview)and code sample.

Use these libraries in the client to create a search box that supports both suggestions and autocomplete. Inputs collected in the search box can then be paired with suggestions and autocomplete actions on the search service.

## Suggestions

This section walks you through an implementation of suggested results, starting with the search box definition. It also shows how and script that invokes the first JavaScript autocomplete library referenced in this article.

### Create a search box

Assuming the [jQuery UI Autocomplete library](https://jqueryui.com/autocomplete/) and an MVC project in C#, you could define the search box using JavaScript in the *Index.cshtml* file. The library adds the search-as-you-type interaction to the search box by making asynchronous calls to the MVC controller to retrieve suggestions.

In *Index.cshtml* inside the folder *\Views\Home*, a line to create a search box might be as follows:

```
<input class="searchBox" type="text" id="searchbox1" placeholder="search">
```


This example is a simple input text box with a class for styling, an ID to be referenced by JavaScript, and placeholder text.

Within the same file, embed JavaScript that references the search box. The following function calls the Suggest API, which requests suggested matching documents based on partial term inputs:

```
$(function () {
$("#searchbox1").autocomplete({
source: "/home/suggest?highlights=false&fuzzy=false&",
minLength: 3,
position: {
my: "left top",
at: "left-23 bottom+10"
}
});
});
```


The `source`

tells the jQuery UI Autocomplete function where to get the list of items to show under the search box. Since this project is an MVC project, it calls the `Suggest`

function in *HomeController.cs* that contains the logic for returning query suggestions. This function also passes a few parameters to control highlights, fuzzy matching, and term. The autocomplete JavaScript API adds the term parameter.

The `minLength: 3`

ensures that recommendations are only shown when there are at least three characters in the search box.

### Enable fuzzy matching

Fuzzy search allows you to get results based on close matches even if the user misspells a word in the search box. The edit distance is 1, which means there can be a maximum discrepancy of one character between the user input and a match.

```
source: "/home/suggest?highlights=false&fuzzy=true&",
```


### Enable highlighting

Highlighting applies font style to the characters in the result that correspond to the input. For example, if the partial input is *micro*, the result would appear as **micro**soft, **micro**scope, and so forth. Highlighting is based on the `HighlightPreTag`

and `HighlightPostTag`

parameters, defined inline with the `Suggest`

function.

```
source: "/home/suggest?highlights=true&fuzzy=true&",
```


### Suggest function

If you're using C# and an MVC application, the *HomeController.cs* file in the *Controllers* directory is where you might create a class for suggested results. In .NET, a `Suggest`

function is based on the [SuggestAsync method](/en-us/dotnet/api/azure.search.documents.searchclient.suggestasync). For more information about the .NET SDK, see [How to use Azure AI Search from a .NET Application](search-howto-dotnet-sdk).

The `InitSearch`

method creates an authenticated HTTP index client to the Azure AI Search service. Properties on the [SuggestOptions](/en-us/dotnet/api/azure.search.documents.suggestoptions) class determine which fields are searched and returned in the results, the number of matches, and whether fuzzy matching is used.

For autocomplete, fuzzy matching is limited to one edit distance (one omitted or misplaced character). Fuzzy matching in autocomplete queries can sometimes produce unexpected results depending on index size and [how it's sharded](index-similarity-and-scoring#sharding-effects-on-query-results).

```
public async Task<ActionResult> SuggestAsync(bool highlights, bool fuzzy, string term)
{
InitSearch();
var options = new SuggestOptions()
{
UseFuzzyMatching = fuzzy,
Size = 8,
};
if (highlights)
{
options.HighlightPreTag = "<b>";
options.HighlightPostTag = "</b>";
}
// Only one suggester can be specified per index.
// The suggester for the Hotels index enables autocomplete/suggestions on the HotelName field only.
// During indexing, HotelNames are indexed in patterns that support autocomplete and suggested results.
var suggestResult = await _searchClient.SuggestAsync<Hotel>(term, "sg", options).ConfigureAwait(false);
// Convert the suggest query results to a list that can be displayed in the client.
List<string> suggestions = suggestResult.Value.Results.Select(x => x.Text).ToList();
// Return the list of suggestions.
return new JsonResult(suggestions);
}
```


The `SuggestAsync`

function takes two parameters that determine whether hit highlights are returned or fuzzy matching is used in addition to the search term input. Up to eight matches can be included in suggested results. The method creates a [SuggestOptions object](/en-us/dotnet/api/azure.search.documents.suggestoptions), which is then passed to the Suggest API. The result is then converted to JSON so it can be shown in the client.

## Autocomplete

So far, the search UX code has been centered on suggestions. The next code block shows autocomplete, using the XDSoft jQuery UI Autocomplete function, passing in a request for Azure AI Search autocomplete. As with the suggestions, in a C# application, code that supports user interaction goes in *index.cshtml*.

```
$(function () {
// using modified jQuery Autocomplete plugin v1.2.8 https://xdsoft.net/jqplugins/autocomplete/
// $.autocomplete -> $.autocompleteInline
$("#searchbox1").autocompleteInline({
appendMethod: "replace",
source: [
function (text, add) {
if (!text) {
return;
}
$.getJSON("/home/autocomplete?term=" + text, function (data) {
if (data && data.length > 0) {
currentSuggestion2 = data[0];
add(data);
}
});
}
]
});
// complete on TAB and clear on ESC
$("#searchbox1").keydown(function (evt) {
if (evt.keyCode === 9 /* TAB */ && currentSuggestion2) {
$("#searchbox1").val(currentSuggestion2);
return false;
} else if (evt.keyCode === 27 /* ESC */) {
currentSuggestion2 = "";
$("#searchbox1").val("");
}
});
});
```


### Autocomplete function

Autocomplete is based on the [AutocompleteAsync method](/en-us/dotnet/api/azure.search.documents.searchclient.autocompleteasync). As with suggestions, this code block would go in the *HomeController.cs* file.

```
public async Task<ActionResult> AutoCompleteAsync(string term)
{
InitSearch();
// Setup the autocomplete parameters.
var ap = new AutocompleteOptions()
{
Mode = AutocompleteMode.OneTermWithContext,
Size = 6
};
var autocompleteResult = await _searchClient.AutocompleteAsync(term, "sg", ap).ConfigureAwait(false);
// Convert the autocompleteResult results to a list that can be displayed in the client.
List<string> autocomplete = autocompleteResult.Value.Results.Select(x => x.Text).ToList();
return new JsonResult(autocomplete);
}
```


The Autocomplete function takes the search term input. The method creates an [AutoCompleteParameters object](/en-us/rest/api/searchservice/documents/autocomplete-post). The result is then converted to JSON so it can be shown in the client.

## Next step

The following tutorial demonstrates a search-as-you-type experience.
