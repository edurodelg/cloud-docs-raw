---
merged_at: 2026-01-25T02:11:58.456039
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-normalizers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-normalizers -->

# Text normalization for case-insensitive filtering, faceting and sorting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, a *normalizer* is a component that pre-processes text for keyword matching over fields marked as "filterable", "facetable", or "sortable". In contrast with full text "searchable" fields that are paired with [text analyzers](search-analyzers), content that's created for filter-facet-sort operations doesn't undergo analysis or tokenization. Omission of text analysis can produce unexpected results when casing and character differences show up, which is why you need a normalizer to homogenize variations in your content.

By applying a normalizer, you can achieve light text transformations that improve results:

- Consistent casing (such as all lowercase or uppercase)
- Normalize accents and diacritics like ö or ê to ASCII equivalent characters "o" and "e"
- Map characters like
`-`

and whitespace into a user-specified character

## Benefits of normalizers

Searching and retrieving documents from a search index requires matching the query input to the contents of the document. Matching is either over tokenized content, as is the case when you invoke "search", or over non-tokenized content if the request is a [filter](search-query-odata-filter), [facet](search-faceted-navigation), or [orderby](search-query-odata-orderby) operation.

Because non-tokenized content is also not analyzed, small differences in the content are evaluated as distinctly different values. Consider the following examples:

`$filter=City eq 'Las Vegas'`

will only return documents that contain the exact text`"Las Vegas"`

and exclude documents with`"LAS VEGAS"`

and`"las vegas"`

, which is inadequate when the use-case requires all documents regardless of the casing.`search=*&facet=City,count:5`

will return`"Las Vegas"`

,`"LAS VEGAS"`

and`"las vegas"`

as distinct values despite being the same city.`search=usa&$orderby=City`

will return the cities in lexicographical order:`"Las Vegas"`

,`"Seattle"`

,`"las vegas"`

, even if the intent is to order the same cities together irrespective of the case.

A normalizer, which is invoked during indexing and query execution, adds light transformations that smooth out minor differences in text for filter, facet, and sort scenarios. In the previous examples, the variants of `"Las Vegas"`

would be processed according to the normalizer you select (for example, all text is lower-cased) for more uniform results.

## How to specify a normalizer

Normalizers are specified in an index definition, on a per-field basis, on text fields (`Edm.String`

and `Collection(Edm.String)`

) that have at least one of "filterable", "sortable", or "facetable" properties set to true. Setting a normalizer is optional and is null by default. We recommend evaluating predefined normalizers before configuring a custom one.

Normalizers can only be specified when you add a new field to the index, so if possible, try to assess the normalization needs upfront and assign normalizers in the initial stages of development when dropping and recreating indexes is routine.

When creating a field definition in the

[index](/en-us/rest/api/searchservice/indexes/create), set the "normalizer" property to one of the following values: a[predefined normalizer](#predefined-normalizers)such as "lowercase", or a custom normalizer (defined in the same index schema).`"fields": [ { "name": "Description", "type": "Edm.String", "retrievable": true, "searchable": true, "filterable": true, "analyzer": "en.microsoft", "normalizer": "lowercase" ... } ]`

Custom normalizers are defined in the "normalizers" section of the index first, and then assigned to the field definition as shown in the previous step. For more information, see

[Create Index](/en-us/rest/api/searchservice/indexes/create)and also[Add custom normalizers](#add-custom-normalizers).`"fields": [ { "name": "Description", "type": "Edm.String", "retrievable": true, "searchable": true, "analyzer": null, "normalizer": "my_custom_normalizer" },`


Note

To change the normalizer of an existing field, [rebuild the index](search-howto-reindex) entirely (you cannot rebuild individual fields).

A good workaround for production indexes, where rebuilding indexes is costly, is to create a new field identical to the old one but with the new normalizer, and use it in place of the old one. Use [Update Index](/en-us/rest/api/searchservice/indexes/create-or-update) to incorporate the new field and [mergeOrUpload](/en-us/rest/api/searchservice/documents) to populate it. Later, as part of planned index servicing, you can clean up the index to remove obsolete fields.

## Predefined and custom normalizers

Azure AI Search provides built-in normalizers for common use-cases along with the capability to customize as required.

| Category | Description |
|---|---|
|

[Custom normalizers](#add-custom-normalizers)1(1) Custom normalizers don't specify tokenizers since normalizers always produce a single token.

## Test a normalizer

You can use the [Test Analyzer (REST)](/en-us/rest/api/searchservice/indexes/analyze) to see how a normalizer processes an input.

**Request**

```
POST https://[search service name].search.windows.net/indexes/[index name]/analyze?api-version=[api-version]
Content-Type: application/json
api-key: [admin key]
{
"normalizer":"asciifolding",
"text": "Vis-à-vis means Opposite"
}
```


**Response**

```
HTTP/1.1 200 OK
{
"tokens": [
{
"token": "Vis-a-vis means Opposite",
"startOffset": 0,
"endOffset": 24,
"position": 0
}
]
}
```


## Normalizers reference

### Predefined normalizers

Name |
Description and Options |
|---|---|
| standard | Lowercases the text followed by asciifolding. |
| lowercase | Transforms characters to lowercase. |
| uppercase | Transforms characters to uppercase. |
| asciifolding | Transforms characters that aren't in the Basic Latin Unicode block to their ASCII equivalent, if one exists. For example, changing `à` to `a` . |
| elision | Removes elision from beginning of the tokens. |

### Supported char filters

Normalizers support two character filters that are identical to their counterparts in [custom analyzer character filters](index-add-custom-analyzers#CharFilter):

### Supported token filters

The list below shows the token filters supported for normalizers and is a subset of the overall [token filters used in custom analyzers](index-add-custom-analyzers#TokenFilters).

[arabic_normalization](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/ar/ArabicNormalizationFilter.html)[asciifolding](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/miscellaneous/ASCIIFoldingFilter.html)[cjk_width](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/cjk/CJKWidthFilter.html)[elision](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/util/ElisionFilter.html)[german_normalization](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/de/GermanNormalizationFilter.html)[hindi_normalization](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/hi/HindiNormalizationFilter.html)[indic_normalization](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/in/IndicNormalizationFilter.html)[persian_normalization](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/fa/PersianNormalizationFilter.html)[scandinavian_normalization](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/miscellaneous/ScandinavianNormalizationFilter.html)[scandinavian_folding](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/miscellaneous/ScandinavianFoldingFilter.html)[sorani_normalization](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/ckb/SoraniNormalizationFilter.html)[lowercase](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/core/LowerCaseFilter.html)[uppercase](https://lucene.apache.org/core/6_6_1/analyzers-common/org/apache/lucene/analysis/core/UpperCaseFilter.html)

## Add custom normalizers

Custom normalizers are [defined within the index schema](/en-us/rest/api/searchservice/indexes/create). The definition includes a name, a type, one or more character filters and token filters. The character filters and token filters are the building blocks for a custom normalizer and responsible for the processing of the text. These filters are applied from left to right.

The `token_filter_name_1`

is the name of token filter, and `char_filter_name_1`

and `char_filter_name_2`

are the names of char filters (see [supported token filters](#supported-token-filters) and [supported char filters](#supported-char-filters)tables below for valid values).

```
"normalizers":(optional)[
{
"name":"name of normalizer",
"@odata.type":"#Microsoft.Azure.Search.CustomNormalizer",
"charFilters":[
"char_filter_name_1",
"char_filter_name_2"
],
"tokenFilters":[
"token_filter_name_1"
]
}
],
"charFilters":(optional)[
{
"name":"char_filter_name_1",
"@odata.type":"#char_filter_type",
"option1": "value1",
"option2": "value2",
...
}
],
"tokenFilters":(optional)[
{
"name":"token_filter_name_1",
"@odata.type":"#token_filter_type",
"option1": "value1",
"option2": "value2",
...
}
]
```


Custom normalizers can be added during index creation or later by updating an existing one. Adding a custom normalizer to an existing index requires the "allowIndexDowntime" flag to be specified in [Update Index](/en-us/rest/api/searchservice/indexes/create-or-update) and will cause the index to be unavailable for a few seconds.

## Custom normalizer example

The example below illustrates a custom normalizer definition with corresponding character filters and token filters. Custom options for character filters and token filters are specified separately as named constructs, and then referenced in the normalizer definition as illustrated below.

A custom normalizer named "my_custom_normalizer" is defined in the "normalizers" section of the index definition.

The normalizer is composed of two character filters and three token filters: elision, lowercase, and customized asciifolding filter "my_asciifolding".

The first character filter "map_dash" replaces all dashes with underscores while the second one "remove_whitespace" removes all spaces.


```
{
"name":"myindex",
"fields":[
{
"name":"id",
"type":"Edm.String",
"key":true,
"searchable":false,
},
{
"name":"city",
"type":"Edm.String",
"filterable": true,
"facetable": true,
"normalizer": "my_custom_normalizer"
}
],
"normalizers":[
{
"name":"my_custom_normalizer",
"@odata.type":"#Microsoft.Azure.Search.CustomNormalizer",
"charFilters":[
"map_dash",
"remove_whitespace"
],
"tokenFilters":[
"my_asciifolding",
"elision",
"lowercase",
]
}
],
"charFilters":[
{
"name":"map_dash",
"@odata.type":"#Microsoft.Azure.Search.MappingCharFilter",
"mappings":["-=>_"]
},
{
"name":"remove_whitespace",
"@odata.type":"#Microsoft.Azure.Search.MappingCharFilter",
"mappings":["\\u0020=>"]
}
],
"tokenFilters":[
{
"name":"my_asciifolding",
"@odata.type":"#Microsoft.Azure.Search.AsciiFoldingTokenFilter",
"preserveOriginal":true
}
]
}
```


---

<!-- DOCUMENTO FUSIONADO: retrieval-augmented-generation-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/retrieval-augmented-generation-overview -->

# Retrieval-augmented Generation (RAG) in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Retrieval-augmented Generation (RAG) is a pattern that extends LLM capabilities by grounding responses in your proprietary content. While conceptually simple, RAG implementations face significant challenges.

## The challenges of RAG

| Challenge | Description |
|---|---|
Query understanding |
Modern users ask complex, conversational, or vague questions with assumed context. Traditional keyword search fails when queries don't match document terminology. For RAG, an information retrieval system must understand intent, not just match words. |
Multi-source data access |
Enterprise content spans SharePoint, databases, blob storage, and other platforms. Creating a unified search corpus without disrupting data operations is essential. |
Token constraints |
LLMs accept limited token inputs. Your retrieval system must return highly relevant, concise results - not exhaustive document dumps. |
Response time expectations |
Users expect AI-powered answers in seconds, not minutes. The retrieval system must balance thoroughness with speed. |
Security and governance |
Opening private content to LLMs requires granular access control. Users and agents must only retrieve authorized content. |

## How Azure AI Search meets RAG challenges

Azure AI Search provides two approaches designed specifically for these RAG challenges:

: A complete RAG pipeline with LLM-assisted query planning, multi-source access, and structured responses optimized for agent consumption.[Agentic retrieval](#modern-rag-with-agentic-retrieval)(preview): The proven approach using hybrid search and semantic ranking, ideal for simpler requirements or when generally available (GA) features are required.[Classic RAG pattern](#classic-rag-pattern-for-azure-ai-search)

The following sections explain how each approach solves specific RAG challenges.

### Solving query understanding challenges

**The problem:** Users ask "What's our PTO policy for remote workers hired after 2023?" but documents say "time off," "telecommute," and "recent hires."

**Agentic retrieval solution:**

- LLM analyzes the question and generates multiple targeted subqueries.
- Decomposes complex questions into focused searches.
- Uses conversation history to understand context.
- Parallel execution across knowledge sources.

**Classic RAG solution:**

- Hybrid queries combine keyword and vector search for better recall.
- Semantic ranking re-scores results based on meaning, not just keywords.
- Vector similarity search matches concepts, not exact terms.

[Learn more about query planning](agentic-retrieval-how-to-set-retrieval-reasoning-effort).

### Solving multisource data challenges

**The problem:** HR policies in SharePoint, benefits in databases, company news on web pages - creating copies disrupts governance and routine data operations.

**Agentic retrieval solution:**

- Knowledge bases unify multiple knowledge sources.
- Direct query against remote SharePoint and Bing (no indexing needed) to supplement index content.
- Retrieval instructions guide the LLM to appropriate data sources.
- Automatic indexing pipeline generation for Azure Blob, OneLake, ingested SharePoint content, ingested other external content.
- Single query interface and query plan across all sources.

**Classic RAG solution:**

- Indexers pull from more than 10 Azure data sources.
- Skills pipeline for chunking, vectorization, image verbalization, and analysis.
- Incremental indexing keeps content fresh.
- You control what's indexed and how.

[Learn more about knowledge sources](agentic-knowledge-source-overview).

### Solving token constraint challenges

**The problem:** GPT-4 accepts about 128k tokens, but you have 10,000 pages of documentation. Sending everything wastes tokens and degrades quality.

**Agentic retrieval solution:**

- Returns a structured response with only the most relevant chunks
- Built-in citation tracking shows provenance
- Query activity log explains what was searched
- Optional answer synthesis reduces token usage further

**Classic RAG solution:**

- Semantic ranking identifies the top 50 most relevant results
- Configurable result limits (top-k for vectors, top-n for text) and minimum thresholds
- Scoring profiles boost critical content
- Select statement controls which fields are returned

[Learn more about relevance tuning](#maximize-relevance-and-recall).

### Solving response time challenges

**The problem:** Users expect answers in 3-5 seconds, but you're querying multiple sources with complex processing.

**Agentic retrieval solution:**

- Parallel subquery execution (not sequential)
- Adjustable reasoning effort (minimal/low/medium)
- Pre-built semantic ranking (no extra orchestration)

**Classic RAG solution:**

- Millisecond query response times
- Single-shot queries reduce complexity
- You control timeout and retry logic
- Simpler architecture with fewer failure points

### Solving security challenges

**The problem:** Finance data should only be accessible to finance team, even when an executive asks the chatbot.

**Agentic retrieval solution:**

- Knowledge source-level access control
- Inherits SharePoint permissions for queries against remote SharePoint
- Inherits Microsoft Entra ID permission metadata for indexed content from Azure Storage
- Filter-based security at query time for other data sources
- Network isolation via private endpoints

**Classic RAG solution:**

- Document-level security trimming
- Inherits Microsoft Entra ID permission metadata for indexed content from Azure Storage
- Filter-based security at query time for other data sources
- Network isolation via private endpoints

### Modern RAG with agentic retrieval

Azure AI Search is a [proven solution for RAG workloads](https://github.com/Azure-Samples/azure-search-openai-demo/blob/main/README.md). It now provides [agentic retrieval](search-what-is-azure-search#what-is-agentic-retrieval), a specialized pipeline designed specifically for RAG patterns. This approach uses LLMs to intelligently break down complex user queries into focused subqueries, executes them in parallel, and returns structured responses optimized for chat completion models.

Agentic retrieval represents the evolution from traditional single-query RAG patterns to multi-query intelligent retrieval, providing:

- Context-aware query planning using conversation history
- Parallel execution of multiple focused subqueries
- Structured responses with grounding data, citations, and execution metadata
- Built-in semantic ranking for optimal relevance
- Optional answer synthesis that uses an LLM-formulated answer in the query response

You need new objects for this pipeline: one or more knowledge sources, a knowledge base, and the retrieve action that you call from application code, such as a tool that works with your AI agent.

For new RAG implementations, start with [agentic retrieval](agentic-retrieval-overview). For existing solutions, consider migrating to take advantage of improved accuracy and context understanding.

### Classic RAG pattern for Azure AI Search

Classic RAG uses the [original query execution architecture](search-what-is-azure-search#what-is-classic-search) where your application sends a single query to Azure AI Search and orchestrates the handoff to an LLM separately. Your deployed LLM formulates an answer using the flattened result set from the query. This approach is simpler with fewer components, and faster because there's no LLM involvement in query planning.

For detailed information about implementing classic RAG, see the [azure-search-classic-rag repository](https://github.com/Azure-Samples/azure-search-classic-rag/blob/main/README.md).

## Content preparation for RAG

RAG quality depends on how you prepare content for retrieval. Azure AI Search supports:

| Content challenge | How Azure AI Search helps |
|---|---|
Large documents |
Automatic chunking (built-in or via skills) |
Multiple languages |
More than 50 language analyzers for text, multilingual vectors |
Images and PDFs |
OCR, image analysis, image verbalization, document extraction skills |
Need for similarity search |
Integrated vectorization (Azure OpenAI, Azure Vision in Foundry Tools, custom) |
Terminology mismatches |
Synonym maps, semantic ranking |

**For agentic retrieval:** Use [knowledge sources](agentic-knowledge-source-overview) that auto-generate chunking and vectorization pipelines.

**For classic RAG:** Use [indexers and skillsets](search-indexer-overview) to build custom pipelines, or push pre-processed content via the [push API](search-what-is-data-import).

### Maximize relevance and recall

How do you provide the best grounding data for LLM answer formulation? It's a combination of having appropriate content, smart queries, and query logic that can identify the best chunks for answering a question.

During indexing, use chunking to subdivide large documents so that portions can be matched on independently. Include a vectorization step to create embeddings used for vector queries.

On the query side, to ensure the most relevant results for your RAG implementation:

[Use hybrid queries](hybrid-search-overview)that combine keyword (nonvector) and vector search for maximum recall. In a hybrid query, if you double down on the same input, a text string and its vector equivalent generate parallel queries for keywords and similarity search, returning the most relevant matches from each query type in a unified result set.[Use semantic ranking](semantic-ranking), built into agentic retrieval, optional for classic RAG.[Apply scoring profiles](index-add-scoring-profiles)to boost specific fields or criteria.Fine-tune with vector query parameters for

[vector weighting](vector-search-how-to-query#vector-weighting)and[minimum thresholds](vector-search-how-to-query#set-thresholds-to-exclude-low-scoring-results-preview).

For more information, see [hybrid search](hybrid-search-overview) and [semantic ranking](semantic-ranking).

## Choose between agentic retrieval and classic RAG

**Use agentic retrieval when:**

- Your client is an agent or chatbot.
- You need the highest possible relevance and accuracy.
- Your queries are complex or conversational.
- You want structured responses with citations and query details.
- You're building new RAG implementations.

**Use classic RAG when:**

- You need generally available (GA) features only.
- Simplicity and speed are priorities over advanced relevance.
- You have existing orchestration code you want to preserve.
- You need fine-grained control over the query pipeline.

A RAG solution that includes agents and Azure AI Search can benefit from [Foundry IQ](https://techcommunity.microsoft.com/blog/azure-ai-foundry-blog/foundry-iq-unlocking-ubiquitous-knowledge-for-agents/4470812), as an agent's single endpoint to a knowledge layer that provides grounding data. Foundry IQ uses agentic retrieval.

Learn more about [classic search](search-what-is-azure-search#what-is-classic-search), [agentic retrieval](search-what-is-azure-search#what-is-agentic-retrieval), and [how they compare](search-what-is-azure-search#how-they-compare).

## How to get started

There are many ways to get started, including code-first solutions and demos.
