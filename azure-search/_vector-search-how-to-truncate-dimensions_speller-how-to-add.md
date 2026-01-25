---
merged_at: 2026-01-25T02:11:58.381768
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-how-to-truncate-dimensions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-truncate-dimensions -->

# Truncate dimensions using MRL compression

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Exercise the ability to use fewer dimensions on text-embedding-3 models. On Azure OpenAI, text-embedding-3 models are retrained on the [Matryoshka Representation Learning](https://arxiv.org/abs/2205.13147) (MRL) technique that produces multiple vector representations at different levels of compression. This approach produces faster searches and reduced storage costs with minimal loss of semantic information.

In Azure AI Search, MRL support supplements [scalar and binary quantization](vector-search-how-to-quantization). When you use either quantization method, you can specify a `truncationDimension`

property on your vector fields to reduce the dimensionality of text embeddings.

MRL multilevel compression saves on vector storage and improves query response times for vector queries based on text embeddings. In Azure AI Search, MRL support is only offered together with another method of quantization. Using binary quantization with MRL provides the maximum vector index size reduction. To achieve maximum storage reduction, use binary quantization with MRL and set `stored`

to `false`

.

Warning

If you set `stored`

to `false`

, vector data is lost during partial document updates unless you provide the entire vector in each update. Set `stored`

to `true`

to avoid this issue. For more information, see [Eliminate optional vector instances from storage](vector-search-how-to-storage-options).

## Prerequisites

A text-embedding-3 model, such as text-embedding-3-small or text-embedding-3-large.

[New vector fields](vector-search-how-to-create-index)of type`Edm.Half`

or`Edm.Single`

. You can't add MRL compression to an existing field.[Scalar or binary quantization](vector-search-how-to-quantization). Truncated dimensions can be set only when scalar or binary quantization is configured. We recommend binary quantization for MRL compression.

### Supported clients

You can use the REST APIs or Azure SDK packages to implement MRL compression. At this time, there's no Azure portal or Microsoft Foundry support.

- Check the change logs for each Azure SDK package for feature support:
[Python](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/search/azure-search-documents/CHANGELOG.md),[.NET](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/search/Azure.Search.Documents/CHANGELOG.md),[Java](https://github.com/Azure/azure-sdk-for-java/blob/azure-search-documents_11.1.3/sdk/search/azure-search-documents/CHANGELOG.md),[JavaScript](https://github.com/Azure/azure-sdk-for-js/blob/main/sdk/search/search-documents/CHANGELOG.md).

## Use MRL-extended text embeddings

MRL is built into the text embedding model you're already using. To use MRL capabilities in Azure AI Search:

Use

[Create or Update Index](/en-us/rest/api/searchservice/indexes/create-or-update)or an equivalent API to specify the index schema.[Add vector fields](vector-search-how-to-create-index)to the index definition.Specify a

`vectorSearch.compressions`

object in your index definition.Include a quantization method, either scalar or binary (recommended).

Include the

`truncationDimension`

parameter and set it to 512. If you're using the text-embedding-3-large model, you can set it as low as 256.Include a vector profile that specifies the HNSW algorithm and the vector compression object.

Assign the vector profile to a vector field of type

`Edm.Half`

or`Edm.Single`

in the fields collection.

There are no query-side modifications for using an MRL-capable text embedding model. MRL support doesn't affect integrated vectorization, text-to-query conversions at query time, semantic ranking, and other relevance-enhancement features, such as reranking with original vectors and oversampling.

Although indexing is slower due to the extra steps, queries are faster.

## Example: Vector search configuration that supports MRL

The following example illustrates a vector search configuration that meets the requirements and recommendations of MRL.

`truncationDimension`

is a compression property. It specifies how much to shrink the vector graph in memory together with a compression method like scalar or binary compression. We recommend 1,024 or higher for `truncationDimension`

with binary quantization. A dimensionality of less than 1,000 degrades the quality of search results when using MRL and binary compression.

```
{
"vectorSearch": {
"profiles": [
{
"name": "use-bq-with-mrl",
"compression": "use-mrl,use-bq",
"algorithm": "use-hnsw"
}
],
"algorithms": [
{
"name": "use-hnsw",
"kind": "hnsw",
"hnswParameters": {
"m": 4,
"efConstruction": 400,
"efSearch": 500,
"metric": "cosine"
}
}
],
"compressions": [
{
"name": "use-mrl",
"kind": "binaryQuantization",
"rescoringOptions": {
"enableRescoring": true,
"defaultOversampling": 10,
"rescoreStorageMethod": "preserveOriginals"
},
"truncationDimension": 1024
},
{
"name": "use-bq",
"kind": "binaryQuantization",
"rescoringOptions": {
"enableRescoring": true,
"defaultOversampling": 10,
"rescoreStorageMethod": "discardOriginals"
}
}
]
}
}
```


Here's an example of a [fully specified vector field definition](/en-us/rest/api/searchservice/indexes/create-or-update#searchfield) that satisfies the requirements for MRL. Recall that vector fields must:

Be of type

`Edm.Half`

or`Edm.Single`

.Have a

`vectorSearchProfile`

property that specifies the algorithm and compression settings.Have a

`dimensions`

property that specifies the number of dimensions for scoring and ranking results. Its value should be the dimensions limit of the model you're using (1,536 for text-embedding-3-small).

```
{
"name": "text_vector",
"type": "Collection(Edm.Single)",
"searchable": true,
"filterable": false,
"retrievable": false,
"stored": false,
"sortable": false,
"facetable": false,
"key": false,
"indexAnalyzer": null,
"searchAnalyzer": null,
"analyzer": null,
"normalizer": null,
"dimensions": 1536,
"vectorSearchProfile": "use-bq-with-mrl",
"vectorEncoding": null,
"synonymMaps": []
}
```


---

<!-- DOCUMENTO FUSIONADO: speller-how-to-add.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/speller-how-to-add -->

# Add spell check to queries in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Spell correction is in public preview under [supplemental terms of use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). It's available through the Azure portal, preview REST APIs, and beta versions of Azure SDK libraries.

You can improve recall by spell-correcting words in a query before they reach the search engine. The `speller`

parameter is supported for all text (non-vector) query types.

## Prerequisites

A search service at the Basic tier or higher, in any region.

An existing search index with content in a

[supported language](#supported-languages).[A query request](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2024-05-01-preview&preserve-view=true)that has`speller=lexicon`

and`queryLanguage`

set to a[supported language](#supported-languages). Spell check works on strings passed in the`search`

parameter. It's not supported for filters, fuzzy search, wildcard search, regular expressions, or vector queries.

Use a search client that supports preview APIs on the query request. You can use a [REST client](search-get-started-text) or beta releases of the Azure SDKs.

| Client library | Versions |
|---|---|
| REST API | Versions 2020-06-30-Preview and later. We recommend the latest preview API:
|

[version 11.7.0-beta.4](https://www.nuget.org/packages/Azure.Search.Documents/11.7.0-beta.4)[version 11.8.0-beta.7](https://central.sonatype.com/artifact/com.azure/azure-search-documents/11.8.0-beta.7)[version 11.3.0-beta.8](https://www.npmjs.com/package/@azure/search-documents/v/11.3.0-beta.8)[version 11.6.0b12](https://pypi.org/project/azure-search-documents/11.6.0b12/)## Spell correction with simple search

The following example uses the [hotels-sample-index](search-get-started-portal) to demonstrate spell correction on a simple text query. Without spell correction, the query returns zero results. With correction, the query returns one result for Johnson's family-oriented resort.

```
POST https://[service name].search.windows.net/indexes/hotels-sample-index/docs/search?api-version=2025-11-01-preview
{
"search": "famly acitvites",
"speller": "lexicon",
"queryLanguage": "en-us",
"queryType": "simple",
"select": "HotelId,HotelName,Description,Category,Tags",
"count": true
}
```


## Spell correction with full Lucene

Spelling correction occurs on individual query terms that undergo text analysis, which is why you can use the speller parameter with some Lucene queries, but not others.

- Incompatible query forms that bypass text analysis include: wildcard, regex, fuzzy
- Compatible query forms include: fielded search, proximity, term boosting

This example uses fielded search over the Category field, with full Lucene syntax, and a misspelled query term. By including speller, the typo in "Suiite" is corrected and the query succeeds.

```
POST https://[service name].search.windows.net/indexes/hotels-sample-index/docs/search?api-version=2025-11-01-preview
{
"search": "Category:(Resort and Spa) OR Category:Suiite",
"queryType": "full",
"speller": "lexicon",
"queryLanguage": "en-us",
"select": "Category",
"count": true
}
```


## Spell correction with semantic ranking

This query, with typos in every term except one, undergoes spelling corrections to return relevant results. To learn more, see [Configure semantic ranker](semantic-how-to-query-request).

```
POST https://[service name].search.windows.net/indexes/hotels-sample-index/docs/search?api-version=2025-11-01-preview
{
"search": "hisotoric hotell wiht great restrant nad wiifi",
"queryType": "semantic",
"speller": "lexicon",
"queryLanguage": "en-us",
"searchFields": "HotelName,Tags,Description",
"select": "HotelId,HotelName,Description,Category,Tags",
"count": true
}
```


## Supported languages

Valid values for `queryLanguage`

can be found in the following table, copied from the list of [supported languages (REST API reference)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-11-01-preview&tabs=HTTP#querylanguage&preserve-view=true).

| Language | queryLanguage |
|---|---|
| English [EN] | EN, EN-US (default) |
| Spanish [ES] | ES, ES-ES (default) |
| French [FR] | FR, FR-FR (default) |
| German [DE] | DE, DE-DE (default) |
| Dutch [NL] | NL, NL-BE, NL-NL (default) |

Note

Previously, while semantic ranker was in public preview, the `queryLanguage`

parameter was also used for semantic ranking. Semantic ranker is now language-agnostic.

### Language analyzer considerations

Indexes that contain non-English content often use [language analyzers](index-add-language-analyzers) on non-English fields to apply the linguistic rules of the native language.

When adding spell check to content that also undergoes language analysis, you can achieve better results using the same language for each indexing and query processing step. For example, if a field's content was indexed using the "fr.microsoft" language analyzer, then queries and spell check should all use a French lexicon or language library of some form.

To recap how language libraries are used in Azure AI Search:

Language analyzers can be invoked during indexing and query execution, and are either Apache Lucene (for example, "de.lucene") or Microsoft ("de.microsoft).

Language lexicons invoked during spell check are specified using one of the language codes in the

[supported language](#supported-languages)table.

In a query request, the value assigned to `queryLanguage`

applies to `speller`

.

Note

Language consistency across various property values is only a concern if you are using language analyzers. If you are using language-agnostic analyzers (such as keyword, simple, standard, stop, whitespace, or `standardasciifolding.lucene`

), then the `queryLanguage`

value can be whatever you want.

While content in a search index can be composed in multiple languages, the query input is most likely in one. The search engine doesn't check for compatibility of `queryLanguage`

, language analyzer, and the language in which content is composed, so be sure to scope queries accordingly to avoid producing incorrect results.
