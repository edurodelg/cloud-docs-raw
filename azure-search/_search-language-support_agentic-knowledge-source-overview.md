---
merged_at: 2026-01-25T03:18:13.797057
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-language-support.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-language-support -->

# Create an index for multiple languages in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you have strings in multiple languages, you can use [vector search](vector-search-overview) to represent multilingual content mathematically, which is the more modern approach. Alternatively, if you aren't using vectors, you can attach [language analyzers](index-add-language-analyzers#supported-language-analyzers) that analyze strings using linguistic rules of a specific language during indexing and query execution. With a language analyzer, you get better handling of diacritics, character variants, punctuation, and word root forms.

Azure AI Search supports Microsoft and Lucene analyzers. By default, the search engine uses Standard Lucene, which is language agnostic. If testing indicates that the default analyzer is insufficient, replace it with a language analyzer.

In Azure AI Search, the two patterns for supporting multiple languages include:

Create language-specific indexes where all of the human readable content is in the same language, and all searchable string fields are attributed to use the same

[language analyzer](index-add-language-analyzers).Create a blended index with language-specific versions of each field (for example, description_en, description_fr, description_ko), and then constrain full text search to just those fields at query time. This approach is useful for scenarios where language variants are only needed on a few fields, like a description.


This article focuses on steps and best practices for configuring and querying language-specific fields in a blended index:

- Define a string field for each language variant.
- Set a language analyzer on each field.
- On the query request, set the
`searchFields`

parameter to specific fields, and then use`select`

to return just those fields that have compatible content.

Note

If you're using large language models in a retrieval augmented generated (RAG) pattern, you can engineer the prompt to return translated strings. That scenario is out of scope for this article.

## Prerequisites

Language analysis applies to fields of type `Edm.String`

that are `searchable`

, and that contain localized text. If you also need text translation, review the next section to see if AI enrichment meets your needs.

Non-string fields and non-searchable string fields don't undergo lexical analysis and aren't tokenized. Instead, they're stored and returned verbatim.

## Add text translation

This article assumes translated strings already exist. If that's not the case, you can attach Foundry Tools to an [enrichment pipeline](cognitive-search-concept-intro), invoking text translation during indexing. Text translation takes a dependency on the indexer feature and Foundry Tools, but all setup is done within Azure AI Search.

To add text translation, follow these steps:

Verify your content is in a

[supported data source](search-indexer-overview#supported-data-sources).[Create a data source](search-howto-create-indexers#prepare-external-data)that points to your content.[Create a skillset](cognitive-search-defining-skillset)that includes the[Text Translation skill](cognitive-search-skill-text-translation).The Text Translation skill takes a single string as input. If you have multiple fields, can create a skillset that calls Text Translation multiple times, once for each field. Alternatively, you can use the

[Text Merger skill](cognitive-search-skill-textmerger)to consolidate the content of multiple fields into one long string.Create an index that includes fields for translated strings. Most of this article covers index design and field definitions for indexing and querying multi-language content.

[Attach a Microsoft Foundry resource](cognitive-search-attach-cognitive-services)to your skillset.[Create and run the indexer](search-howto-create-indexers), and then apply the guidance in this article to query just the fields of interest.

Tip

Text translation is built into the [Import data wizard](search-get-started-skillset). If you have a [supported data source](search-indexer-overview#supported-data-sources) with text you'd like to translate, you can step through the wizard to try out the language detection and translation functionality before writing any code.

## Define fields for content in different languages

In Azure AI Search, queries target a single index. Developers who want to provide language-specific strings in a single search experience typically define dedicated fields to store the values: one field for English strings, one for French, and so on.

The `analyzer`

property on a field definition is used to set the [language analyzer](index-add-language-analyzers). It's used for both indexing and query execution.

```
{
"name": "hotels-sample-index",
"fields": [
{
"name": "Description",
"type": "Edm.String",
"retrievable": true,
"searchable": true,
"analyzer": "en.microsoft"
},
{
"name": "Description_fr",
"type": "Edm.String",
"retrievable": true,
"searchable": true,
"analyzer": "fr.microsoft"
}
]
}
```


## Build and load an index

An intermediate step is [building and populating the index](search-get-started-text) before formulating a query. We mention this step here for completeness. One way to determine index availability is by checking the indexes list in the [portal](https://portal.azure.com).

## Constrain the query and trim results

Parameters on the query are used to limit search to specific fields and then trim the results of any fields not helpful to your scenario.

| Parameters | Purpose |
|---|---|
`searchFields` |
Limits full text search to the list of named fields. |
`select` |
Trims the response to include only the fields you specify. By default, all retrievable fields are returned. The `select` parameter lets you choose which ones to return. |

Given a goal of constraining search to fields containing French strings, you would use `searchFields`

to target the query at fields containing strings in that language.

Specifying the analyzer on a query request isn't necessary. A language analyzer on the field definition determines text analysis during query execution. For queries that specify multiple fields, each invoking different language analyzers, the terms or phrases are processed concurrently by the assigned analyzers for each field.

By default, a search returns all fields that are marked as retrievable. As such, you might want to exclude fields that don't conform to the language-specific search experience you want to provide. Specifically, if you limited search to a field with French strings, you probably want to exclude fields with English strings from your results. Using the `select`

query parameter gives you control over which fields are returned to the calling application.

#### Example in REST

```
POST https://[service name].search.windows.net/indexes/hotels-sample-index/docs/search?api-version=2025-09-01
{
"search": "animaux acceptés",
"searchFields": "Tags, Description_fr",
"select": "HotelName, Description_fr, Address/City, Address/StateProvince, Tags",
"count": "true"
}
```


#### Example in C#

```
private static void RunQueries(SearchClient srchclient)
{
SearchOptions options;
SearchResults<Hotel> response;
options = new SearchOptions()
{
IncludeTotalCount = true,
Filter = "",
OrderBy = { "" }
};
options.Select.Add("HotelId");
options.Select.Add("HotelName");
options.Select.Add("Description_fr");
options.SearchFields.Add("Tags");
options.SearchFields.Add("Description_fr");
response = srchclient.Search<Hotel>("*", options);
WriteDocuments(response);
}
```


## Boost language-specific fields

Sometimes the language of the agent issuing a query isn't known, in which case the query can be issued against all fields simultaneously. IA preference for results in a certain language can be defined using [scoring profiles](index-add-scoring-profiles). In the example below, matches found in the description in French are scored higher relative to matches in other languages:

```
"scoringProfiles": [
{
"name": "frenchFirst",
"text": {
"weights": { "description_fr": 2 }
}
}
]
```


You would then include the scoring profile in the search request:

```
POST /indexes/hotels/docs/search?api-version=2025-09-01
{
"search": "pets allowed",
"searchFields": "Tags, Description_fr",
"select": "HotelName, Tags, Description_fr",
"scoringProfile": "frenchFirst",
"count": "true"
}
```


---

<!-- DOCUMENTO FUSIONADO: agentic-knowledge-source-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/agentic-knowledge-source-overview -->

# What is a knowledge source?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

A knowledge source specifies the content used for agentic retrieval. It either encapsulates a search index populated by external data, or it's a direct connection to a remote target such as Bing or SharePoint that's queried directly. A knowledge source is a required definition in a knowledge base.

Create a knowledge source as a top-level resource on your search service. Each knowledge source points to exactly one data structure, either a search index that

[meets the criteria for agentic retrieval](agentic-retrieval-how-to-create-index)or a supported external resource.Reference one or more knowledge sources in a

[knowledge base](agentic-retrieval-how-to-create-knowledge-base). In an agentic retrieval pipeline, you can query against multiple knowledge sources in a single request. Subqueries are generated for each knowledge source. Top results are returned in the retrieval response.For certain knowledge sources, you can use a knowledge source definition to generate a full indexer pipeline (data source, skillset, indexer, and index) that works for agentic retrieval. Instead of creating multiple objects manually, the information in the knowledge source is used to generate all objects, including a populated, chunked, and searchable index.


Make sure you have at least one knowledge source before creating a knowledge base. The full specification of a knowledge source and a knowledge base can be found in the [preview REST API reference](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true).

## Working with a knowledge source

Creation path: first create a knowledge source, then create a knowledge base.

Deletion path: update or delete knowledge bases to remove references to a knowledge source, and then delete the knowledge source last.

A knowledge source, its index, and the knowledge base must all exist on the same search service. External content is either accessed over the public internet (Bing) or in a Microsoft tenant (remote SharePoint).


## Supported knowledge sources

In this preview, you can create the following knowledge sources:

| Kind | Indexed or remote |
|---|---|
`"searchIndex"` API |

[generates an indexer pipeline that pulls from a blob container.](/en-us/rest/api/searchservice/knowledge-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true#azureblobknowledgesource)`"azureBlob"`

API[generates an indexer pipeline that pulls from a lakehouse.](/en-us/rest/api/searchservice/knowledge-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true#indexedonelakeknowledgesource)`"indexedOneLake"`

API[generates an indexer pipeline that pulls from a SharePoint site.](/en-us/rest/api/searchservice/knowledge-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true#indexedsharepointknowledgesource)`"indexedSharePoint"`

API[retrieves content directly from SharePoint.](/en-us/rest/api/searchservice/knowledge-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true#remotesharepointknowledgesource)`"remoteSharePoint"`

API[retrieves real-time grounding data from Microsoft Bing.](/en-us/rest/api/searchservice/knowledge-sources/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true#webknowledgesource)`"webParameters"`

APIIndexed knowledge sources point to a target index on Azure AI Search. Query execution is local to the search engine on your search service. Keyword (full text search), vector, and hybrid query capabilities are used for retrieving data from indexed knowledge sources.

You access remote knowledge sources at query time. The agentic retrieval engine calls the retrieval APIs that are native to the platform (Bing or SharePoint APIs).

All retrieved content, whether indexed or remote, is pulled into the ranking pipeline in Azure AI Search where it's scored for relevance, merged (assuming multiple queries), reranked, and returned in the retrieval response.

## Creating knowledge sources

Create knowledge sources as standalone objects. Then, specify them in a [knowledge base](agentic-retrieval-how-to-create-knowledge-base) within a ["knowledgeSources" array](/en-us/rest/api/searchservice/knowledge-bases/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true#knowledgesourcereference).

To create objects on a search service, you need [ Search Service Contributor permissions](search-security-rbac). If you're using a knowledge source that creates an indexer pipeline, you also need

**Search Index Data Contributor**permissions to load an index. Alternatively, you can

[use an API admin key](search-security-api-keys)instead of roles.

Use the REST API or an Azure SDK preview package to create a knowledge source. Azure portal support is available for select knowledge sources. The following links provide instructions for creating a knowledge source:

[How to create a search index knowledge source (wraps an existing index)](agentic-knowledge-source-how-to-search-index)[How to create a blob knowledge source (generates an indexer pipeline)](agentic-knowledge-source-how-to-blob)[How to create a OneLake knowledge source (generates an indexer pipeline)](agentic-knowledge-source-how-to-onelake)[How to create a SharePoint (indexed) knowledge source (generates an indexer pipeline)](agentic-knowledge-source-how-to-sharepoint-indexed)[How to create a SharePoint (remote) knowledge source (queries SharePoint directly)](agentic-knowledge-source-how-to-sharepoint-remote)[How to create a Web Knowledge Source resource (connects to Bing's public endpoint)](agentic-knowledge-source-how-to-web)

After you create the knowledge source, reference it in a knowledge base.

## Using knowledge sources

You can explicitly control knowledge source usage by setting `alwaysQuery`

on the knowledge source definition or through steering instructions used during query planning. Steering instructions refer to descriptions on an index, or explicit retrieval instructions in the knowledge source, that provide guidance on when to use the index. Query planning happens when you use a low or medium [retrieval reasoning effort from the LLM](agentic-retrieval-how-to-set-retrieval-reasoning-effort). For a minimal reasoning effort, all knowledge sources listed in the knowledge base are in scope for every query. For low and medium, the knowledge base and the LLM can determine at query time which knowledge sources are likely to provide the best search corpus.

Knowledge source selection logic is based on these factors:

Is

`alwaysQuery`

set? If yes, the knowledge source is always used on every query.The

`name`

of the knowledge source.The

`description`

of an index, assuming an indexed knowledge source.The

`retrievalInstructions`

specified in the[retrieve action](agentic-retrieval-how-to-retrieve)or in the[knowledge base definition](/en-us/rest/api/searchservice/knowledge-bases/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)provides guidance that includes or excludes a knowledge source. It's similar to a prompt. You can specify brevity, tone, and formatting as a retrieval instruction.on a knowledge base also affects query output and what goes in the response.`outputMode`


### Use a retrieval reasoning effort to control LLM usage

Not all solutions benefit from LLM query planning and execution. If simplicity and speed outweigh the benefits the LLM query planning and context engineering provide, specify a minimal reasoning effort to prevent LLM processing in your pipeline.

For low and medium, the level of LLM processing is either a balanced or maximal approach that improves relevance. For more information, see [Set the retrieval reasoning effort](agentic-retrieval-how-to-set-retrieval-reasoning-effort).

Note

If you used `attemptFastPath`

in the previous preview, that approach is now replaced by `retrievalReasoningEffort`

set to `minimal`

.
