---
merged_at: 2026-01-25T03:18:13.774678
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: index-ranking-similarity.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/index-ranking-similarity -->

# Configure BM25 relevance scoring

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, learn how to configure the [BM25 relevance scoring algorithm](https://en.wikipedia.org/wiki/Okapi_BM25) used by Azure AI Search for full text search queries. It also explains how to enable BM25 on older search services.

BM25 applies to:

- Queries that use the
`search`

parameter for full text search, on text fields having a`searchable`

attribution. - Scoring is scoped to
`searchFields`

, or to all`searchable`

fields if`searchFields`

is null.

The search engine uses BM25 to calculate a **@searchScore** for each match in a given query. Matching documents are ranked by their search score, with the top results returned in the query response. It's possible to get some [score variation](index-similarity-and-scoring#score-variation) in results, even from the same query executing over the same search index, but usually these variations are small and don't change the overall ranking of results.

BM25 has defaults for weighting term frequency and document length. You can customize these properties if the defaults aren't suited to your content. Configuration changes are scoped to individual indexes, which means you can adjust relevance scoring based on the characteristics of each index.

## Default scoring algorithm

Depending on the age of your search service, Azure AI Search supports two [scoring algorithms](index-similarity-and-scoring) for a full text search query:

- Okapi BM25 algorithm (after July 15, 2020)
- Classic similarity algorithm (before July 15, 2020)

BM25 ranking is the default because it tends to produce search rankings that align better with user expectations. It includes [parameters](#set-bm25-parameters) for tuning results based on factors such as document size. For search services created after July 2020, BM25 is the only scoring algorithm. If you try to set "similarity" to ClassicSimilarity on a new service, an HTTP 400 error is returned because that algorithm isn't supported by the service.

For older services, classic similarity remains the default algorithm. Older services can [upgrade to BM25](#enable-bm25-scoring-on-older-services) on a per-index basis. When switching from classic to BM25, you can expect to see some differences how search results are ordered.

## Set BM25 parameters

BM25 ranking provides two parameters for tuning the relevance score calculation.

Use a

[Create or Update Index](/en-us/rest/api/searchservice/indexes/create)request to set BM25 parameters:`PUT [service-name].search.windows.net/indexes/[index-name]?api-version=2025-09-01&allowIndexDowntime=true { "similarity": { "@odata.type": "#Microsoft.Azure.Search.BM25Similarity", "b" : 0.75, "k1" : 1.2 } }`

If the index is live, append the

`allowIndexDowntime=true`

URI parameter on the request, shown on the previous example.Because Azure AI Search doesn't allow updates to a live index, you need to take the index offline so that the parameters can be added. Indexing and query requests fail while the index is offline. The duration of the outage is the amount of time it takes to update the index, usually no more than several seconds. When the update is complete, the index comes back automatically.

Set

`"b"`

and`"k1"`

to custom values, and then send the request.Property Type Description k1 number Controls the scaling function between the term frequency of each matching terms to the final relevance score of a document-query pair. Values are usually 0.0 to 3.0, with 1.2 as the default.

A value of 0.0 represents a "binary model", where the contribution of a single matching term is the same for all matching documents, regardless of how many times that term appears in the text. Larger k1 values allow the score to continue to increase as more instances of the same term is found in the document.

Using a larger k1 value is important in cases where multiple terms are included in a search query. In those cases, you might want to favor documents matching more query terms, over documents that only match a single term, multiple times. For example, when querying for the terms "Apollo Spaceflight", you might want to lower the score of an article about Greek Mythology that contains the term "Apollo" a few dozen times, without mentions of "Spaceflight", relative to another article that explicitly mentions both "Apollo" and "Spaceflight" a handful of times only.b number Controls how the length of a document affects the relevance score. Values are between 0 and 1, with 0.75 as the default.

A value of 0.0 means the length of the document doesn't influence the score. A value of 1.0 means the effect of term frequency on relevance score is normalized by the document's length.

Normalizing the term frequency by the document's length is useful in cases where you want to penalize longer documents. In some cases, longer documents (such as a complete novel), are more likely to contain many irrelevant terms, compared to shorter documents.

## Enable BM25 scoring on older services

If you're running a search service that was created from March 2014 through July 15, 2020, you can enable BM25 by setting a "similarity" property on new indexes. The property is only exposed on new indexes, so if you want BM25 on an existing index, you must drop and [rebuild the index](search-howto-reindex) with a "similarity" property set to `Microsoft.Azure.Search.BM25Similarity`

.

Once an index exists with a "similarity" property, you can switch between `BM25Similarity`

or `ClassicSimilarity`

.

The following links describe the Similarity property in the Azure SDKs.

| Client library | Similarity property |
|---|---|
| .NET |
|

[SearchIndex.setSimilarity](/en-us/java/api/com.azure.search.documents.indexes.models.searchindex.setsimilarity)[SearchIndex.Similarity](/en-us/javascript/api/@azure/search-documents/searchindex#similarity)[similarity property on SearchIndex](/en-us/python/api/azure-search-documents/azure.search.documents.indexes.models.searchindex)### REST example

You can also use the [REST API](/en-us/rest/api/searchservice/indexes/create). The following example creates a new index with the "similarity" property set to BM25:

```
PUT [service-name].search.windows.net/indexes/[index name]?api-version=2025-09-01
{
"name": "indexName",
"fields": [
{
"name": "id",
"type": "Edm.String",
"key": true
},
{
"name": "name",
"type": "Edm.String",
"searchable": true,
"analyzer": "en.lucene"
},
...
],
"similarity": {
"@odata.type": "#Microsoft.Azure.Search.BM25Similarity"
}
}
```


---

<!-- DOCUMENTO FUSIONADO: agentic-retrieval-how-to-set-retrieval-reasoning-effort.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-set-retrieval-reasoning-effort -->

# Set the retrieval reasoning effort

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

In agentic retrieval, you can specify the level of large language model (LLM) processing for query planning and answer formulation. Use the `retrievalReasoningEffort`

property to set LLM processing levels that affect costs and latency. Extra LLM processing improves relevancy, but it also takes longer and uses billable LLM resources. You can set this property in a knowledge base or on a retrieve request.

Levels of reasoning effort include:

| Level | Effort |
|---|---|
`minimal` |
No LLM processing. You provide the query. |
`low` |
Runs a single pass of LLM-based query planning and knowledge source selection. This is the default. The LLM analyzes the query and breaks it into component parts as needed. |
`medium` |
Adds deeper search and an enhanced retrieval stack to agentic retrieval to maximize completeness. |

## Prerequisites

Azure AI Search in any

[region that provides agentic retrieval](search-region-support).Familiarity with

[agentic retrieval concepts and workflow](agentic-retrieval-overview).[A knowledge base](agentic-retrieval-how-to-create-knowledge-base)and a[knowledge source](agentic-knowledge-source-overview).[Visual Studio Code](https://code.visualstudio.com/)with the[REST Client extension](https://marketplace.visualstudio.com/items?itemName=humao.rest-client). You can also use a preview package of an Azure SDK that provides the latest knowledge source REST APIs.

## Set retrievalReasoningEffort in a knowledge base

To establish the default behavior, set the property in the knowledge base.

Use

[Create or Update Knowledge Base](/en-us/rest/api/searchservice/knowledge-bases/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)to set the`retrievalReasoningEffort`

.Add the

`retrievalReasoningEffort`

property. The following JSON shows the syntax. For more information about knowledge bases, see[Create a knowledge base](agentic-retrieval-how-to-create-knowledge-base).`"retrievalReasoningEffort": { /* no other parameters when effort is minimal */ "kind": "low" }`


## Set retrievalReasoningEffort in a retrieve request

To override the default on a query-by-query basis, set the property in the retrieve request.

Modify a

[retrieve action](/en-us/rest/api/searchservice/knowledge-retrieval/retrieve?view=rest-searchservice-2025-11-01-preview&preserve-view=true)to override the knowledge base`retrievalReasoningEffort`

default.Add the

`retrievalReasoningEffort`

property. A retrieve request might look similar to the following example.`{ "messages": [ /* trimmed for brevity */ ], "retrievalReasoningEffort": { "kind": "low" }, "outputMode": "answerSynthesis", "maxRuntimeInSeconds": 30, "maxOutputSize": 6000 }`


## Choose a retrieval reasoning effort

| Level | Description | Recommendation | Limits |
|---|---|---|---|
`minimal` |
Disables LLM-based query planning to deliver the lowest cost and latency for agentic retrieval. It issues direct text and vector searches across the knowledge sources listed in the knowledge base, and returns the best-matching passages. Because all knowledge sources in the knowledge base are always searched and no query expansion is performed, behavior is predictable and easy to control. It also means the `alwaysQueryKnowledgeSource` property on a retrieve request is ignored. |
Use "minimal" for migrations from the
|

`outputMode`

must be set to `extractiveData`

. [Answer synthesis](agentic-retrieval-how-to-answer-synthesis)and[web knowledge](agentic-knowledge-source-how-to-web)aren't supported.`low`

Maximum three subqueries from a maximum of three knowledge sources.

Maximum of 50 documents for semantic ranking, and 10 documents if the semantic ranker uses L3 classification.

`medium`

[high-precision semantic classifier](search-relevance-overview)evaluates the retrieved documents to determined whether further processing and L3 ranking is required. If the initial results from the first pass are insufficiently relevant to the query, a follow-up iteration is performed using a revised query plan. This revised query plan takes the previous results into account and iterates by fine-tuning queries, broadening terms, or adding other knowledge sources such as the web. It also increases resource limits compared to low and minimal effort. This reasoning level optimizes for relevance rather than exhaustive recall.Medium isn't available in all agentic retrieval regions. See the list in the next section for available regions. 10,000 answer tokens.

Maximum of five subqueries from a maximum of five knowledge sources.

Maximum of 50 documents for semantic ranking, and 20 documents if the semantic ranker uses L3 classification.

### Medium retrieval and iterative search

A medium retrieval reasoning effort provides iterative search if initial results aren't sufficiently relevant. An extra *semantic classifier model* is called to determine if a second iteration is necessary.

The semantic classifier performs the following:

Recognizes when there's enough context to answer the question.

Retries on insufficient results, using existing information for context. New queries might drill down for more focused detail, or broaden the search. The activity log in the response shows the generated queries used for a more comprehensive answer.

Rescores using L3 classification. The range is identical to L2 ranking, an absolute range of zero through 4.0.


There's only one retry. Each iteration adds latency and cost, so the system constrains retry to one pass. A second iteration adds input tokens to the query pipeline, which adds to the overall billable input token count.

Iteration can reuse or choose different sources. The second pass selects the most promising knowledge resource to provide the missing information.

### Regions supporting medium retrieval reasoning effort

You can set a medium retrieval reasoning effort if your search service is in one of the following regions.

- East US 2
- East US
- South Central US
- West US 3
- West US 2
- West US
- Germany West Central
- North Europe
- Switzerland North
- Sweden Central
- Spain Central
- UK South
- Korea Central
- Japan East
- Southeast Asia
