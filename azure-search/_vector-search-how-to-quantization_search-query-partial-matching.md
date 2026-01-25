---
merged_at: 2026-01-25T03:18:14.109258
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-how-to-quantization.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-quantization -->

# Compress vectors using scalar or binary quantization

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search supports scalar and binary quantization for reducing the size of vectors in a search index. Quantization is recommended because it reduces both memory and disk storage for float16 and float32 embeddings. To offset the effects of lossy compression, you can add oversampling and rescoring.

To use built-in quantization, follow these steps:

- Start with
[vector fields and a](vector-search-how-to-create-index)to an index`vectorSearch`

configuration - Add
`vectorSearch.compressions`

- Add a
`scalarQuantization`

or`binaryQuantization`

configuration and give it a name - Set optional properties to mitigate the effects of lossy indexing
- Create a new vector profile that uses the named configuration
- Create a new vector field having the new vector profile
- Load the index with float32 or float16 data that's quantized during indexing with the configuration you defined
- Optionally,
[query quantized data](#query-a-quantized-vector-field-using-oversampling)using the oversampling parameter. If the vector field doesn't specify oversampling in its definition, you can add it at query time.

Tip

[Azure AI Search: Cut Vector Costs Up To 92.5% with New Compression Techniques](https://aka.ms/AISearch-cut-cost) compares compression strategies and explains savings in storage and costs. It also includes metrics for measuring relevance based on Normalized discounted cumulative gain (NDCG), demonstrating that you can compress your data without sacrificing search quality.

## Prerequisites

[Vector fields in a search index](vector-search-how-to-create-index), with a`vectorSearch`

configuration specifying either the Hierarchical Navigable Small Worlds (HNSW) or exhaustive K-Nearest Neighbor (KNN) algorithm, and a new vector profile.

## Supported quantization techniques

Quantization applies to vector fields receiving float-type vectors. In the examples in this article, the field's data type is `Collection(Edm.Single)`

for incoming float32 embeddings, but float16 is also supported. When the vectors are received on a field with compression configured, the engine performs quantization to reduce the footprint of the vector data in memory and on disk.

Two types of quantization are supported:

Scalar quantization compresses float values into narrower data types. AI Search currently supports int8, which is 8 bits, reducing vector index size fourfold.

Binary quantization converts floats into binary bits, which takes up 1 bit. This results in up to 28 times reduced vector index size.


Note

While free services support quantization, they don't demonstrate the full storage savings due to the limited storage quota.

### How scalar quantization works in Azure AI Search

Scalar quantization reduces the resolution of each number within each vector embedding. Instead of describing each number as a 16-bit or 32-bit floating point number, it uses an 8-bit integer. It identifies a range of numbers (typically 99th percentile minimum and maximum) and divides them into a finite number of levels or bin, assigning each bin an identifier. In 8-bit scalar quantization, there are 2^8, or 256, possible bins.

Each component of the vector is mapped to the closest representative value within this set of quantization levels in a process akin to rounding a real number to the nearest integer. In the quantized 8-bit vector, the identifier number stands in place of the original value. After quantization, each vector is represented by an array of identifiers for the bins to which its components belong. These quantized vectors require much fewer bits to store compared to the original vector, thus reducing storage requirements and memory footprint.

### How binary quantization works in Azure AI Search

Binary quantization compresses high-dimensional vectors by representing each component as a single bit, either 0 or 1. This method drastically reduces the memory footprint and accelerates vector comparison operations, which are crucial for search and retrieval tasks. Benchmark tests show up to 96% reduction in vector index size.

It's particularly effective for embeddings with dimensions greater than 1024. For smaller dimensions, we recommend testing the quality of binary quantization, or trying scalar instead. Additionally, we’ve found binary quantization performs very well when embeddings are centered around zero. Most popular embedding models offered by OpenAI, Cohere, and Mistral are centered around zero.

## Supported rescoring techniques

Rescoring is an optional technique used to offset information loss due to vector quantization. During query execution, it uses oversampling to pick up extra vectors, and supplemental information to rescore initial results found by the query. Supplemental information is either uncompressed original full-precision vectors - or for binary quantization only - you have the option of rescoring using the binary quantized document candidates against the query vector.

Only HNSW graphs allow rescoring. Exhaustive KNN doesn't support rescoring because by definition, all vectors are scanned at query time, which makes rescoring and oversampling irrelevant.

Rescoring options are specified in the index, but you can invoke rescoring at query time by adding the oversampling query parameter.

| Object | Properties |
|---|---|
| Index | Add
`RescoringOptions` |

`RescoringOptions`

.`oversampling`

on [or](/en-us/rest/api/searchservice/documents/search-post#rawvectorquery)`RawVectorQuery`

[definitions. Adding](/en-us/rest/api/searchservice/documents/search-post#vectorizabletextquery)`VectorizableTextQuery`

`oversampling`

invokes rescoring at query time.Note

Rescoring parameter names have changed over the last several releases. If you're using an older preview API, review the [upgrade instructions](search-api-migration#upgrade-to-2024-11-01-preview) for addressing breaking changes.

The generalized process for rescoring is:

- The vector query executes over compressed vector fields.
- The vector query returns the top k oversampled candidates.
- Oversampled k candidates are rescored using either the uncompressed original vectors for scalar quantization, or the dot product of binary quantization.
- After rescoring, results are adjusted so that more relevant matches appear first.

Oversampling for scalar quantized vectors requires the availability of the original full precision vectors. Oversampling for binary quantized vectors can use either full precision vectors (`preserveOriginals`

) or the dot product of the binary vector (`discardOriginals`

). If you're optimizing vector storage, make sure to keep the full precision vectors in the index if you need them for rescoring purposes. For more information, see [Eliminate optional vector instances from storage](vector-search-how-to-storage-options).

## Add "compressions" to a search index

This section explains how to specify a `vectorsSearch.compressions`

section in the index. The following example shows a partial index definition with a fields collection that includes a vector field.

The compression example includes both `scalarQuantization`

or `binaryQuantization`

. You can specify as many compression configurations as you need, and then assign the ones you want to a vector profile.

Syntax for `vectorSearch.Compressions`

varies between stable and preview REST APIs, with the preview adding more options for storage optimization, plus changes to existing syntax. Backwards compatibility is preserved through internal API mappings, but we recommend adopting the newer properties in code that targets 2024-11-01-preview and future versions.

Use the [Create Index](/en-us/rest/api/searchservice/indexes/create) or [Create or Update Index](/en-us/rest/api/searchservice/indexes/create-or-update) REST API to configure compression settings.

```
POST https://[servicename].search.windows.net/indexes?api-version=2025-09-01
{
"name": "my-index",
"description": "This is a description of this index",
"fields": [
{ "name": "Id", "type": "Edm.String", "key": true, "retrievable": true, "searchable": true, "filterable": true },
{ "name": "content", "type": "Edm.String", "retrievable": true, "searchable": true },
{ "name": "vectorContent", "type": "Collection(Edm.Single)", "retrievable": false, "searchable": true, "dimensions": 1536,"vectorSearchProfile": "vector-profile-1"},
],
"vectorSearch": {
"profiles": [
{
"name": "vector-profile-1",
"algorithm": "use-hnsw",
"compression": "use-scalar"
}
],
"algorithms": [
{
"name": "use-hnsw",
"kind": "hnsw",
"hnswParameters": { },
"exhaustiveKnnParameters": null
}
],
"compressions": [
{
"scalarQuantizationParameters": {
"quantizedDataType": "int8"
},
"name": "mySQ8",
"kind": "scalarQuantization",
"rescoringOptions": {
"enableRescoring": true,
"defaultOversampling": 10,
"rescoreStorageMethod": "preserveOriginals"
},
"truncationDimension": 2
},
{
"name": "myBQC",
"kind": "binaryQuantization",
"rescoringOptions": {
"enableRescoring": true,
"defaultOversampling": 10,
"rescoreStorageMethod": "discardOriginals"
},
"truncationDimension": 2
}
]
},
}
```


**Key points**:

`kind`

must be set to`scalarQuantization`

or`binaryQuantization`

.`rescoringOptions`

are a collection of properties used to offset lossy compression by rescoring query results using the original full-precision vectors that exist prior to quantization. For rescoring to work, you must have the vector instance that provides this content. Setting`rescoreStorageMethod`

to`discardOriginals`

prevents you from using`enableRescoring`

or`defaultOversampling`

. For more information about vector storage, see[Eliminate optional vector instances from storage](vector-search-how-to-storage-options).`"rescoreStorageMethod": "preserveOriginals"`

rescores vector search results with the original full-precision vectors can result in adjustments to search score and rankings, promoting the more relevant matches as determined by the rescoring step. For binary quantization, you can set`rescoreStorageMethod`

to`discardOriginals`

to further reduce storage, without reducing quality. Original vectors aren't needed for binary quantization.`defaultOversampling`

considers a broader set of potential results to offset the reduction in information from quantization. The formula for potential results consists of the`k`

in the query, with an oversampling multiplier. For example, if the query specifies a`k`

of 5, and oversampling is 20, then the query effectively requests 100 documents for use in reranking, using the original uncompressed vector for that purpose. Only the top`k`

reranked results are returned. This property is optional. Default is 4.`quantizedDataType`

is optional and applies to scalar quantization only. If you add it, it must be set to`int8`

. This is the only primitive data type supported for scalar quantization at this time. Default is`int8`

.`truncationDimension`

taps inherent capabilities of the text-embedding-3 models to "encode information at different granularities and allows a single embedding to adapt to the computational constraints of downstream tasks" (see[Matryoshka Representation Learning](https://arxiv.org/abs/2205.13147)). You can use truncated dimensions with or without rescoring options. For more information about how this feature is implemented in Azure AI Search, see[Truncate dimensions using MRL compression](vector-search-how-to-truncate-dimensions).

## Add the vector search algorithm

You can use the HNSW or eKNN algorithm in the 2024-11-01-preview REST API or later. For the stable version, use HNSW only. If you want rescoring, you must choose HNSW.

```
"vectorSearch": {
"profiles": [ ],
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
"compressions": [ <see previous section>]
}
```


## Create and assign a new vector profile

To use a new quantization configuration, you must create a *new* vector profile. Creation of a new vector profile is necessary for building compressed indexes in memory. Your new profile uses HNSW.

In the same index definition, create a new vector profile and add a compression property and an algorithm. Here are two profiles, one for each quantization approach.

`"vectorSearch": { "profiles": [ { "name": "vector-profile-hnsw-scalar", "compression": "use-scalar", "algorithm": "use-hnsw", "vectorizer": null }, { "name": "vector-profile-hnsw-binary", "compression": "use-binary", "algorithm": "use-hnsw", "vectorizer": null } ], "algorithms": [ <see previous section> ], "compressions": [ <see previous section> ] }`

Assign a vector profile to a

*new*vector field. The data type of the field is either float32 or float16.In Azure AI Search, the Entity Data Model (EDM) equivalents of float32 and float16 types are

`Collection(Edm.Single)`

and`Collection(Edm.Half)`

, respectively.`{ "name": "vectorContent", "type": "Collection(Edm.Single)", "searchable": true, "retrievable": true, "dimensions": 1536, "vectorSearchProfile": "vector-profile-hnsw-scalar", }`

[Load the index](search-what-is-data-import)using indexers for pull model indexing, or APIs for push model indexing.

## Query a quantized vector field using oversampling

Query syntax for a compressed or quantized vector field is the same as for noncompressed vector fields, unless you want to override parameters associated with oversampling and rescoring. You can add an `oversampling`

parameter to invoke oversampling and rescoring at query time.

Use [Search Documents](/en-us/rest/api/searchservice/documents/search-post) for the request.

Recall that the [vector compression definition](vector-search-how-to-quantization) in the index has settings for `enableRescoring`

, `rescoreStorageMethod`

, and `defaultOversampling`

to mitigate the effects of lossy compression. You can override the default values to vary the behavior at query time. For example, if `defaultOversampling`

is 10.0, you can change it to something else in the query request.

You can set the oversampling parameter even if the index doesn't explicitly have rescoring options or `defaultOversampling`

definition. Providing `oversampling`

at query time overrides the index settings for that query and executes the query with an effective `enableRescoring`

as true.

```
POST https://[service-name].search.windows.net/indexes/demo-index/docs/search?api-version=2025-09-01
{
"vectorQueries": [
{
"kind": "vector",
"vector": [8, 2, 3, 4, 3, 5, 2, 1],
"fields": "myvector",
"oversampling": 12.0,
"k": 5
}
]
}
```


**Key points**:

Oversampling applies to vector fields that undergo vector compression, per the vector profile assignment.

Oversampling in the query overrides the

`defaultOversampling`

value in the index, or invokes oversampling and rescoring at query time, even if the index's compression configuration didn't specify oversampling or reranking options.


---

<!-- DOCUMENTO FUSIONADO: search-query-partial-matching.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-partial-matching -->

# Partial term search and patterns with special characters (hyphens, wildcard, regex, patterns)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A *partial term search* refers to queries consisting of term fragments, where instead of a whole term, you might have just the beginning, middle, or end of term (sometimes referred to as prefix, infix, or suffix queries). A partial term search might include a combination of fragments, often with special characters such as hyphens, dashes, or slashes that are part of the query string. Common use-cases include parts of a phone number, URL, codes, or hyphenated compound words.

Partial terms and special characters can be problematic if the index doesn't have a token representing the text fragment you want to search for. During the [lexical analysis phase](search-lucene-query-architecture#stage-2-lexical-analysis) of keyword indexing (assuming the default standard analyzer), special characters are discarded, compound words are split up, and whitespace is deleted. If you're searching for a text fragment that was modified during lexical analysis, the query fails because no match is found. Consider this example: a phone number like `+1 (425) 703-6214`

(tokenized as `"1"`

, `"425"`

, `"703"`

, `"6214"`

) won't show up in a `"3-62"`

query because that content doesn't actually exist in the index.

The solution is to invoke an analyzer during indexing that preserves a complete string, including spaces and special characters if necessary, so that you can include the spaces and characters in your query string. Having a whole, untokenized string enables pattern matching for "starts with" or "ends with" queries, where the pattern you provide can be evaluated against a term that isn't transformed by lexical analysis.

If you need to support search scenarios that call for analyzed and non-analyzed content, consider creating two fields in your index, one for each scenario. One field undergoes lexical analysis. The second field stores an intact string, using a content-preserving analyzer that emits whole-string tokens for pattern matching.

## About partial term search

Azure AI Search scans for whole tokenized terms in the index and won't find a match on a partial term unless you include wildcard placeholder operators (`*`

and `?`

), or format the query as a regular expression.

Partial terms are specified using these techniques:

[Regular expression queries](query-lucene-syntax#bkmk_regex)can be any regular expression that is valid under Apache Lucene.[Wildcard operators with prefix matching](query-simple-syntax#prefix-search)refers to a generally recognized pattern that includes the beginning of a term, followed by`*`

or`?`

suffix operators, such as`search=cap*`

matching on "Cap'n Jack's Waterfront Inn" or "Highline Capital". Prefixing matching is supported in both simple and full Lucene query syntax.[Wildcard with infix and suffix matching](query-lucene-syntax#bkmk_wildcard)places the`*`

and`?`

operators inside or at the beginning of a term, and requires regular expression syntax (where the expression is enclosed with forward slashes). For example, the query string (`search=/.*numeric.*/`

) returns results on "alphanumeric" and "alphanumerical" as suffix and infix matches.

For regular expression, wildcard, and fuzzy search, analyzers aren't used at query time. For these query forms, which the parser detects by the presence of operators and delimiters, the query string is passed to the engine without lexical analysis. For these query forms, the analyzer specified on the field is ignored.

Note

When a partial query string includes characters, such as slashes in a URL fragment, you might need to add escape characters. In JSON, a forward slash `/`

is escaped with a backward slash `\`

. As such, `search=/.*microsoft.com\/azure\/.*/`

is the syntax for the URL fragment "microsoft.com/azure/".

## Solving partial/pattern search problems

When you need to search on fragments or patterns or special characters, you can override the default analyzer with a custom analyzer that operates under simpler tokenization rules, retaining the entire string in the index.

The approach looks like this:

- Define a second field to store an intact version of the string (assuming you want analyzed and non-analyzed text at query time)
- Evaluate and choose among the various analyzers that emit tokens at the right level of granularity
- Assign the analyzer to the field
- Build and test the index

## 1 - Create a dedicated field

Analyzers determine how terms are tokenized in an index. Since analyzers are assigned on a per-field basis, you can create fields in your index to optimize for different scenarios. For example, you might define "featureCode" and "featureCodeRegex" to support regular full text search on the first, and advanced pattern matching on the second. The analyzers assigned to each field determine how the contents of each field are tokenized in the index.

```
{
"name": "featureCode",
"type": "Edm.String",
"retrievable": true,
"searchable": true,
"analyzer": null
},
{
"name": "featureCodeRegex",
"type": "Edm.String",
"retrievable": true,
"searchable": true,
"analyzer": "my_custom_analyzer"
},
```


## 2 - Set an analyzer

When choosing an analyzer that produces whole-term tokens, the following analyzers are common choices:

| Analyzer | Behaviors |
|---|---|
|

[keyword](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/core/KeywordAnalyzer.html)[whitespace](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/core/WhitespaceAnalyzer.html)[custom analyzer](index-add-custom-analyzers)A recommended combination is the

[keyword tokenizer](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/core/KeywordTokenizer.html)with a[lower-case token filter](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/core/LowerCaseFilter.html). By itself, the built-in[keyword analyzer](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/core/KeywordAnalyzer.html)doesn't lower-case any upper-case text, which can cause queries to fail. A custom analyzer gives you a mechanism for adding the lower-case token filter.Using a REST client, you can add the [Test Analyzer REST call](/en-us/rest/api/searchservice/indexes/analyze) to inspect tokenized output.

The index must exist on the search service, but it can be empty. Given an existing index and a field containing dashes or partial terms, you can try various analyzers over specific terms to see what tokens are emitted.

First, check the Standard analyzer to see how terms are tokenized by default.

`{ "text": "SVP10-NOR-00", "analyzer": "standard" }`

Evaluate the response to see how the text is tokenized within the index. Notice how each term is lower-cased, hyphens removed, and substrings broken up into individual tokens. Only those queries that match on these tokens will return this document in the results. A query that includes "10-NOR" will fail.

`{ "tokens": [ { "token": "svp10", "startOffset": 0, "endOffset": 5, "position": 0 }, { "token": "nor", "startOffset": 6, "endOffset": 9, "position": 1 }, { "token": "00", "startOffset": 10, "endOffset": 12, "position": 2 } ] }`

Now modify the request to use the

`whitespace`

or`keyword`

analyzer:`{ "text": "SVP10-NOR-00", "analyzer": "keyword" }`

This time, the response consists of a single token, upper-cased, with dashes preserved as a part of the string. If you need to search on a pattern or a partial term such as "10-NOR", the query engine now has the basis for finding a match.

`{ "tokens": [ { "token": "SVP10-NOR-00", "startOffset": 0, "endOffset": 12, "position": 0 } ] }`


Important

Be aware that query parsers often lower-case terms in a search expression when building the query tree. If you are using an analyzer that does not lower-case text inputs during indexing, and you are not getting expected results, this could be the reason. The solution is to add a lower-case token filter, as described in the "Use custom analyzers" section below.

## 3 - Configure an analyzer

Whether you're evaluating analyzers or moving forward with a specific configuration, you'll need to specify the analyzer on the field definition, and possibly configure the analyzer itself if you aren't using a built-in analyzer. When swapping analyzers, you typically need to rebuild the index (drop, recreate, and reload).

### Use built-in analyzers

Built-in analyzers can be specified by name on an `analyzer`

property of a field definition, with no extra configuration required in the index. The following example demonstrates how you would set the `whitespace`

analyzer on a field.

For other scenarios and to learn more about other built-in analyzers, see [Built-in analyzers](index-add-custom-analyzers#built-in-analyzers).

```
{
"name": "phoneNumber",
"type": "Edm.String",
"key": false,
"retrievable": true,
"searchable": true,
"analyzer": "whitespace"
}
```


### Use custom analyzers

If you're using a [custom analyzer](index-add-custom-analyzers), define it in the index with a user-defined combination of tokenizer, token filter, with possible configuration settings. Next, reference it on a field definition, just as you would a built-in analyzer.

When the objective is whole-term tokenization, a custom analyzer that consists of a **keyword tokenizer** and **lower-case token filter** is recommended.

- The keyword tokenizer creates a single token for the entire contents of a field.
- The lowercase token filter transforms upper-case letters into lower-case text. Query parsers typically lowercase any uppercase text inputs. Lower-casing homogenizes the inputs with the tokenized terms.

The following example illustrates a custom analyzer that provides the keyword tokenizer and a lowercase token filter.

```
{
"fields": [
{
"name": "accountNumber",
"analyzer":"myCustomAnalyzer",
"type": "Edm.String",
"searchable": true,
"filterable": true,
"retrievable": true,
"sortable": false,
"facetable": false
}
],
"analyzers": [
{
"@odata.type":"#Microsoft.Azure.Search.CustomAnalyzer",
"name":"myCustomAnalyzer",
"charFilters":[],
"tokenizer":"keyword_v2",
"tokenFilters":["lowercase"]
}
],
"tokenizers":[],
"charFilters": [],
"tokenFilters": []
}
```


Note

The `keyword_v2`

tokenizer and `lowercase`

token filter are known to the system and using their default configurations, which is why you can reference them by name without having to define them first.

## 4 - Build and test

Once you've defined an index with analyzers and field definitions that support your scenario, load documents that have representative strings so that you can test partial string queries.

Use a REST client to query partial terms and special characters described in this article.

The previous sections explained the logic. This section steps through each API you should call when testing your solution.

[Delete Index](/en-us/rest/api/searchservice/indexes/delete)removes an existing index of the same name so that you can recreate it.[Create Index](/en-us/rest/api/searchservice/indexes/create)creates the index structure on your search service, including analyzer definitions and fields with an analyzer specification.[Load Documents](/en-us/rest/api/searchservice/documents)imports documents having the same structure as your index, as well as searchable content. After this step, your index is ready to query or test.[Test Analyzer](/en-us/rest/api/searchservice/indexes/analyze)was introduced in[Set an analyzer](#set-an-analyzer). Test some of the strings in your index using various analyzers to understand how terms are tokenized.[Search Documents](/en-us/rest/api/searchservice/documents/search-post)explains how to construct a query request, using either[simple syntax](query-simple-syntax)or[full Lucene syntax](query-lucene-syntax)for wildcard and regular expressions.For partial term queries, such as querying "3-6214" to find a match on "+1 (425) 703-6214", you can use the simple syntax:

`search=3-6214&queryType=simple`

.For infix and suffix queries, such as querying "num" or "numeric to find a match on "alphanumeric", use the full Lucene syntax and a regular expression:

`search=/.*num.*/&queryType=full`


## Optimizing prefix and suffix queries

Matching prefixes and suffixes using the default analyzer requires additional query features. Prefixes require [wildcard search](query-lucene-syntax#bkmk_wildcard) and suffixes require [regular expression search](query-lucene-syntax#bkmk_regex). Both of these features can reduce query performance.

The following example adds an [ EdgeNGramTokenFilter](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/ngram/EdgeNGramTokenizer.html) to make prefix or suffix matches faster. Tokens are generated in 2-25 character combinations that include characters. Here's an example progression from two to seven tokens: MS, MSF, MSFT, MSFT/, MSFT/S, MSFT/SQ, MSFT/SQL.

`EdgeNGramTokenFilter`

requires a `side`

parameter which determines which side of the string character combinations are generated from. Use `front`

for prefix queries and `back`

for suffix queries.Extra tokenization results in a larger index. If you have sufficient capacity to accommodate the larger index, this approach with its faster response time might be the best solution.

```
{
"fields": [
{
"name": "accountNumber_prefix",
"indexAnalyzer": "ngram_front_analyzer",
"searchAnalyzer": "keyword",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"retrievable": true,
"sortable": false,
"facetable": false
},
{
"name": "accountNumber_suffix",
"indexAnalyzer": "ngram_back_analyzer",
"searchAnalyzer": "keyword",
"type": "Edm.String",
"searchable": true,
"filterable": false,
"retrievable": true,
"sortable": false,
"facetable": false
}
],
"analyzers": [
{
"@odata.type":"#Microsoft.Azure.Search.CustomAnalyzer",
"name":"ngram_front_analyzer",
"charFilters":[],
"tokenizer":"keyword_v2",
"tokenFilters":["lowercase", "front_edgeNGram"]
},
{
"@odata.type":"#Microsoft.Azure.Search.CustomAnalyzer",
"name":"ngram_back_analyzer",
"charFilters":[],
"tokenizer":"keyword_v2",
"tokenFilters":["lowercase", "back_edgeNGram"]
}
],
"tokenizers":[],
"charFilters": [],
"tokenFilters": [
{
"@odata.type":"#Microsoft.Azure.Search.EdgeNGramTokenFilterV2",
"name":"front_edgeNGram",
"minGram": 2,
"maxGram": 25,
"side": "front"
},
{
"@odata.type":"#Microsoft.Azure.Search.EdgeNGramTokenFilterV2",
"name":"back_edgeNGram",
"minGram": 2,
"maxGram": 25,
"side": "back"
}
]
}
```


To search for account numbers that start with `123`

, we can use the following query:

```
{
"search": "123",
"searchFields": "accountNumber_prefix"
}
```


To search for account numbers that end with `456`

, we can use the following query:

```
{
"search": "456",
"searchFields": "accountNumber_suffix"
}
```


## Next steps

This article explains how analyzers both contribute to query problems and solve query problems. As a next step, take a closer look at analyzers affect indexing and query processing.
