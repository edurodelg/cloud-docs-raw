---
merged_at: 2026-01-25T02:11:58.437574
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index-add-suggesters.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/index-add-suggesters -->

# Configure a suggester for autocomplete and suggestions in a query

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, typeahead or "search-as-you-type" is enabled by using a *suggester*. A suggester is a configuration in an index that specifies which fields should be used to populate autocomplete and suggested matches. These fields undergo extra tokenization, generating prefix sequences to support matches on partial terms. For example, a suggester that includes a `city`

field with a value for *Seattle* has prefix combinations of *sea*, *seat*, *seatt*, and *seattl* to support typeahead.

Matches on partial terms can be either an autocompleted query or a suggested match. The same suggester supports both experiences.

## Typeahead experiences

Typeahead in Azure AI Search can be either *autocomplete*, which completes a partial input for a whole term query, or *suggestions* that invite click through to a particular match. Autocomplete produces a query. Suggestions produce a matching document.

The following screenshot illustrates both. Autocomplete anticipates a potential term, finishing *tw* with *in*. Suggestions are mini search results, where a field like `hotel name`

represents a matching hotel search document from the index. For suggestions, you can surface any field that provides descriptive information.


You can use these features separately or together. To implement these behaviors in Azure AI Search, there's an index and query component.

Add a suggester to a search index definition. The remainder of this article focuses on creating a suggester.

Call a suggester-enabled query, in the form of a suggestion request or autocomplete request, by using one of the APIs listed in

[Use a suggester](#how-to-use-a-suggester).

Search-as-you-type is enabled on a per-field basis for string fields. You can implement both typeahead behaviors within the same search solution if you want an experience similar to the one indicated in the screenshot. Both requests target the *documents* collection of a specific index, and responses are returned after a user provides at least a three-character input string.

## How to create a suggester

To create a suggester, add one to an [index definition](/en-us/rest/api/searchservice/indexes/create). A suggester takes a name and a collection of fields over which the typeahead experience is enabled. The best time to create a suggester is when you're also defining the field that uses it.

Use string fields only.

If the string field is part of a complex type (for example, a City field within Address), include the parent in the field path:

`"Address/City"`

(REST, C#, and Python), or`["Address"]["City"]`

(JavaScript).Use the default standard Lucene analyzer (

`"analyzer": null`

) or a[language analyzer](index-add-language-analyzers)(for example,`"analyzer": "fr.microsoft"`

) on the field.

If you try to create a suggester using preexisting fields, the API disallows it. Prefixes are generated during indexing, when partial terms in two or more character combinations are tokenized alongside whole terms. Given that existing fields are already tokenized, you have to rebuild the index if you want to add them to a suggester. For more information, see [Update or rebuild an index in Azure AI Search](search-howto-reindex).

### Choose fields

Although a suggester has several properties, it's primarily a collection of string fields for which you're enabling a search-as-you-type experience. There's one suggester for each index, so the suggester list must include all fields that contribute content for both suggestions and autocomplete.

Autocomplete benefits from a larger pool of fields to draw from because the extra content has more term completion potential.

Suggestions, on the other hand, produce better results when your field choice is selective. Remember that the suggestion is a proxy for a search document so pick fields that best represent a single result. Names, titles, or other unique fields that distinguish among multiple matches work best. If fields consist of repetitive values, the suggestions consist of identical results and a user won't know which one to choose.

To satisfy both search-as-you-type experiences, add all of the fields that you need for autocomplete, but then use `select`

, `top`

, `filter`

, and `searchFields`

to control results for suggestions.

### Choose analyzers

Your choice of an analyzer determines how fields are tokenized and prefixed. For example, for a hyphenated string like *context-sensitive*, using a language analyzer results in these token combinations: *context*, *sensitive*, *context-sensitive*. Had you used the standard Lucene analyzer, the hyphenated string wouldn't exist.

When evaluating analyzers, consider using the [Analyze Text API](/en-us/rest/api/searchservice/indexes/analyze) for insight into how terms are processed. Once you build an index, you can try various analyzers on a string to view token output.

Fields that use [custom analyzers](index-add-custom-analyzers) or [built-in analyzers](index-add-custom-analyzers#built-in-analyzers), (except for standard Lucene) are explicitly disallowed to prevent poor outcomes.

Note

If you need to work around the analyzer constraint, for example if you need a keyword or ngram analyzer for certain query scenarios, you should use two separate fields for the same content. This allows one of the fields to have a suggester, while the other can be set up with a custom analyzer configuration. If you're using an indexer, you can map a source field to two different index fields to support multiple configuations.

## Create using the Azure portal

In the Azure portal, you can specify a suggester when you select **Add index**.

- Select
**Add index**and add a string field. - Set field attribution to
**Searchable**. - Select an analyzer.
- Once fields are defined, select
**Autocomplete settings**. - Select the searchable string fields for which you want to enable an autocomplete experience.

## Create using REST

In the REST API, add suggesters by using [Create Index](/en-us/rest/api/searchservice/indexes/create).

```
{
"name": "hotels-sample-index",
"fields": [
. . .
{
"name": "HotelName",
"type": "Edm.String",
"facetable": false,
"filterable": false,
"key": false,
"retrievable": true,
"searchable": true,
"sortable": false,
"analyzer": "en.microsoft",
"indexAnalyzer": null,
"searchAnalyzer": null,
"synonymMaps": [],
"fields": []
},
],
"suggesters": [
{
"name": "sg",
"searchMode": "analyzingInfixMatching",
"sourceFields": ["HotelName"]
}
],
"scoringProfiles": [
. . .
]
}
```


## Create using .NET

In C#, define a [SearchSuggester object](/en-us/dotnet/api/azure.search.documents.indexes.models.searchsuggester). `Suggesters`

is a collection on a SearchIndex object, but it can only take one item. Add a suggester to the index definition.

```
private static void CreateIndex(string indexName, SearchIndexClient indexClient)
{
FieldBuilder fieldBuilder = new FieldBuilder();
var searchFields = fieldBuilder.Build(typeof(Hotel));
var definition = new SearchIndex(indexName, searchFields);
var suggester = new SearchSuggester("sg", new[] { "HotelName", "Category", "Address/City", "Address/StateProvince" });
definition.Suggesters.Add(suggester);
indexClient.CreateOrUpdateIndex(definition);
}
```


## Property reference

| Property | Description |
|---|---|
| name | Specified in the suggester definition, but also called on an Autocomplete or Suggestions request. |
| sourceFields | Specified in the suggester definition. It's a list of one or more fields in the index that are the source of the content for suggestions. Fields must be of type `Edm.String` . If an analyzer is specified on the field, it must be a named lexical analyzer listed on
As a best practice, specify only those fields that lend themselves to an expected and appropriate response, whether it's a completed string in a search bar or a dropdown list. A hotel name is a good candidate because it has precision. Verbose fields like descriptions and comments are too dense. Similarly, repetitive fields, such as categories and tags, are less effective. In the examples, we include category anyway to demonstrate that you can include multiple fields. |
| searchMode | REST-only parameter, but also visible in the Azure portal. This parameter isn't available in the .NET SDK. It indicates the strategy used to search for candidate phrases. The only mode currently supported is `analyzingInfixMatching` , which currently matches on the beginning of a term. |

## Use a suggester

A suggester is used in a query. After a suggester is created, call one of the following APIs for a search-as-you-type experience:

In a search application, client code should use a library like [jQuery UI Autocomplete](https://jqueryui.com/autocomplete/) to collect the partial query and provide the match. For more information about this task, see [Add autocomplete or suggested results to client code](search-add-autocomplete-suggestions).

API usage is illustrated in the following call to the Autocomplete REST API. There are two takeaways from this example. First, as with all queries, the operation is against the documents collection of an index and the query includes a `search`

parameter, which in this case provides the partial query. Second, you must add `suggesterName`

to the request. If a suggester isn't defined in the index, calls to autocomplete or suggestions fail.

```
POST /indexes/myxboxgames/docs/autocomplete?search&api-version=2025-09-01
{
"search": "minecraf",
"suggesterName": "sg"
}
```


## Sample code

To learn how to use an open source Suggestions package for partial term completion in the client app, see [Explore the .NET search code](tutorial-csharp-search-query-integration).

## Next step

Learn more about request formulation.


---

<!-- DOCUMENTO FUSIONADO: semantic-answers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/semantic-answers -->

# Return a semantic answer in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When invoking [semantic ranking and captions](semantic-how-to-query-request), you can optionally extract content from the top-matching documents that "answers" the query directly. One or more answers can be included in the response, which you can then render on a search page to improve the user experience of your app.

A semantic answer is verbatim content in your search index that a reading comprehension model has recognized as an answer to the query posed in the request. It's not a generated answer. For guidance on a chat-style user interaction model that uses generative AI to compose answers from your content, see [Retrieval Augmented Generation (RAG)](retrieval-augmented-generation-overview).

In this article, learn how to request a semantic answer, unpack the response, and find out what content characteristics are most conducive to producing high-quality answers.

## Prerequisites

All prerequisites that apply to [semantic queries](semantic-how-to-query-request#prerequisites) also apply to answers, including [service tier and region](semantic-search-overview#availability-and-pricing).

Query logic must include the semantic query parameters "queryType=semantic", plus the "answers" parameter. Required parameters are discussed in this article.

Query strings entered by the user must be recognizable as a question (what, where, when, how).

Search documents in the index must contain text having the characteristics of an answer, and that text must exist in one of the fields listed in the

[semantic configuration](semantic-how-to-configure). For example, given a query "what is a hash table", if none of the fields in the semantic configuration contain passages that include "A hash table is ...", then it's unlikely an answer is returned.

## What is a semantic answer?

A semantic answer is a substructure of a [semantic query response](semantic-how-to-query-request). It consists of one or more verbatim passages from a search document, formulated as an answer to a query that looks like a question. To return an answer, phrases or sentences must exist in a search document that have the language characteristics of an answer, and the query itself must be posed as a question.

Azure AI Search uses a machine reading comprehension model to recognize and pick the best answer. The model produces a set of potential answers from the available content, and when it reaches a high enough confidence level, it proposes one as an answer.

Answers are returned as an independent, top-level object in the query response payload that you can choose to render on search pages, along side search results. Structurally, it's an array element within the response consisting of text, a document key, and a confidence score.

## Formulate a REST query for "answers"

To return a semantic answer, the query must have the semantic `"queryType"`

, `"queryLanguage"`

, `"semanticConfiguration"`

, and the `"answers"`

parameters. Specifying these parameters doesn't guarantee an answer, but the request must include them for answer processing to occur.

```
{
"search": "how do clouds form",
"queryType": "semantic",
"queryLanguage": "en-us",
"semanticConfiguration": "my-semantic-config",
"answers": "extractive|count-3",
"captions": "extractive|highlight-true",
"count": "true"
}
```


A query string must not be null and should be formulated as question.

`"queryType"`

must be set to "semantic.`"queryLanguage"`

must be one of the values from the[supported languages list (REST API)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2024-05-01-preview&preserve-view=true#querylanguage).A

`"semanticConfiguration"`

determines which string fields provide tokens to the extraction model. The same fields that produce captions also produce answers. See[Create a semantic configuration](semantic-how-to-configure)for details.For

`"answers"`

, parameter construction is`"answers": "extractive"`

, where the default number of answers returned is one. You can increase the number of answers by adding a`count`

as shown in the above example, up to a maximum of 10. Whether you need more than one answer depends on the user experience of your app, and how you want to render results.

## Unpack an "answer" from the response

Answers are provided in the `"@search.answers"`

array, which appears first in the query response. Each answer in the array includes:

- Document key
- Text or content of the answer, in plain text or with formatting
- Confidence score

If an answer is indeterminate, the response shows up as `"@search.answers": []`

. The answers array is followed by the value array, which is the standard response in a semantic query.

Given the query "how do clouds form" which can be directed at an index built on [content from the NASA Earth Book](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/nasa-e-book), the following example illustrates a verbatim answer (found on page 38):

```
{
"@search.answers": [
{
"key": "4123",
"text": "Sunlight heats the land all day, warming that moist air and causing it to rise high into the atmosphere until it cools and condenses into water droplets. Clouds generally form where air is ascending (over land in this case), but not where it is descending (over the river).",
"highlights": "Sunlight heats the land all day, warming that moist air and causing it to rise high into the atmosphere until it cools and condenses into water droplets. Clouds generally form<em> where air is ascending</em> (over land in this case), but not where it is<em> descending</em> (over the river).",
"score": 0.94639826
}
],
"value": [
{
"@search.score": 0.5479723,
"@search.rerankerScore": 1.0321671911515296,
"@search.captions": [
{
"text": "Like all clouds, it forms when the air reaches its dew point—the temperature at which an air mass is cool enough for its water vapor to condense into liquid droplets. This false-color image shows valley fog, which is common in the Pacific Northwest of North America.",
"highlights": "Like all<em> clouds</em>, it<em> forms</em> when the air reaches its dew point—the temperature at which an air mass is cool enough for its water vapor to condense into liquid droplets. This false-color image shows valley<em> fog</em>, which is common in the Pacific Northwest of North America."
}
],
"title": "Earth Atmosphere",
"content": "Fog is essentially a cloud lying on the ground. Like all clouds, it forms when the air reaches its dew point—the temperature at \n\nwhich an air mass is cool enough for its water vapor to condense into liquid droplets.\n\nThis false-color image shows valley fog, which is common in the Pacific Northwest of North America. On clear winter nights, the \n\nground and overlying air cool off rapidly, especially at high elevations. Cold air is denser than warm air, and it sinks down into the \n\nvalleys. The moist air in the valleys gets chilled to its dew point, and fog forms. If undisturbed by winds, such fog may persist for \n\ndays. The Terra satellite captured this image of foggy valleys northeast of Vancouver in February 2010.\n\n\n",
"locations": [
"Pacific Northwest",
"North America",
"Vancouver"
]
}
]
}
```


When designing a search results page that includes answers, be sure to handle cases where answers aren't found.

Within @search.answers:

**"key"**is the document key or ID of the match. Given a document key, you can use[Lookup Document](/en-us/rest/api/searchservice/documents/get)API to retrieve any or all parts of the search document to include on the search page or a detail page.**"text"**and**"highlights"**provide identical content, in both plain text and with highlights.By default, highlights are styled as

`<em>`

, which you can override using the existing highlightPreTag and highlightPostTag parameters. As noted elsewhere, the substance of an answer is verbatim content from a search document. The extraction model looks for characteristics of an answer to find the appropriate content, but doesn't compose new language in the response.**"score"**is a confidence score that reflects the strength of the answer. If there are multiple answers in the response, this score is used to determine the order. Top answers and top captions can be derived from different search documents, where the top answer originates from one document, and the top caption from another, but in general the same documents appear in the top positions within each array.

Answers are followed by the **"value"** array, which always includes scores, captions, and any fields that are retrievable by default. If you specified the select parameter, the "value" array is limited to the fields that you specified. See [Configure semantic ranker](semantic-how-to-configure) for details.

## Tips for producing high-quality answers

For best results, return semantic answers on a document corpus having the following characteristics:

The "semanticConfiguration" must include fields that offer sufficient text in which an answer is likely to be found. Fields more likely to contain answers should be listed first in "prioritizedContentFields". Only verbatim text from a document can appear as an answer.

Query strings must not be null (search=

`*`

) and the string should have the characteristics of a question, such as "what is" or "how to", as opposed to a keyword search consisting of terms or phrases in arbitrary order. If the query string doesn't appear to be a question, answer processing is skipped, even if the request specifies "answers" as a query parameter.Semantic extraction and summarization have limits over how many tokens per document can be analyzed in a timely fashion. In practical terms, if you have large documents that run into hundreds of pages, try to break up the content into smaller documents first.
