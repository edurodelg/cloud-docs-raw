---
merged_at: 2026-01-25T02:11:58.404419
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: agentic-retrieval-how-to-answer-synthesis.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/agentic-retrieval-how-to-answer-synthesis -->

# Use answer synthesis for citation-backed responses in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

By default, a [knowledge base](agentic-retrieval-how-to-create-knowledge-base) in Azure AI Search performs *data extraction*, which returns raw grounding chunks from your knowledge sources. Data extraction is useful for retrieving specific information but lacks the context and reasoning necessary for complex queries.

You can instead enable *answer synthesis*, which uses the LLM specified in your knowledge base to answer queries in natural language. Each answer includes citations to the retrieved sources and follows any instructions you provide, such as using bulleted lists.

You can enable answer synthesis in two ways:

- On the knowledge base (becomes the default for all queries)
- On individual retrieval requests (overrides the default)

Important

The

`minimal`

retrieval reasoning effort disables LLM processing, so it's incompatible with answer synthesis in both knowledge base definitions and retrieval requests. For more information, see[Set the retrieval reasoning effort](agentic-retrieval-how-to-set-retrieval-reasoning-effort).Answer synthesis incurs pay-as-you-go charges from Azure OpenAI, which is based on the number of input and output tokens. Charges appear under the LLM assigned to the knowledge base. For more information, see

[Availability and pricing of agentic retrieval](agentic-retrieval-overview#availability-and-pricing).

## Prerequisites

A knowledge base that uses the

[2025-11-01-preview syntax](agentic-retrieval-how-to-migrate).[Visual Studio Code](https://code.visualstudio.com/)with the[REST Client extension](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)or a preview Azure SDK package that provides the knowledge base REST APIs.

## Enable answer synthesis on a knowledge base

This section explains how to enable answer synthesis on an existing knowledge base. Although you can use this configuration for new knowledge bases, knowledge base creation is beyond the scope of this article.

To enable answer synthesis on a knowledge base:

Use the 2025-11-01-preview of

[Knowledge Base - Create or Update (REST API)](/en-us/rest/api/searchservice/knowledge-bases/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true)to formulate the request.In the body of the request, set

`outputMode`

to`answerSynthesis`

.(Optional) Use

`answerInstructions`

to customize the answer output. Our example instructs the knowledge base to`Use concise bulleted lists`

.

```
@search-url = <YOUR SEARCH SERVICE URL>
@api-key = <YOUR API KEY>
@knowledge-base-name = <YOUR KNOWLEDGE BASE NAME>
### Enable answer synthesis on a knowledge base
PUT {{search-url}}/knowledgebases/{{knowledge-base-name}}?api-version=2025-11-01-preview HTTP/1.1
Content-Type: application/json
api-key: {{api-key}}
{
"name": "{{knowledge-base-name}}",
"knowledgeSources": [ ... // OMITTED FOR BREVITY ],
"models": [ ... // OMITTED FOR BREVITY ],
"outputMode": "answerSynthesis",
"answerInstructions": "Use concise bulleted lists"
}
```


Note

This example assumes that you're using key-based authentication for local proof-of-concept testing. We recommend role-based access control for production workloads. For more information, see [Connect to Azure AI Search using roles](search-security-rbac).

## Enable answer synthesis on a retrieval request

For per-query control over the response format, you can enable answer synthesis at query time. This approach overrides the default output mode specified in the knowledge base.

To enable answer synthesis on a retrieval request:

Use the 2025-11-01-preview of

[Knowledge Retrieval - Retrieve (REST API)](/en-us/rest/api/searchservice/knowledge-retrieval/retrieve?view=rest-searchservice-2025-11-01-preview&preserve-view=true)to formulate the request.In the body of the request, set

`outputMode`

to`answerSynthesis`

.

```
@search-url = <YOUR SEARCH SERVICE URL>
@api-key = <YOUR API KEY>
@knowledge-base-name = <YOUR KNOWLEDGE BASE NAME>
### Enable answer synthesis on a retrieval request
POST {{search-url}}/knowledgebases/{{knowledge-base-name}}/retrieve?api-version=2025-11-01-preview HTTP/1.1
Content-Type: application/json
api-key: {{api-key}}
{
"messages": [
{
"role": "user",
"content": [
{
"type": "text",
"text": "What is healthcare?"
}
]
}
],
"outputMode": "answerSynthesis"
}
```


Note

This example assumes that you're using key-based authentication for local proof-of-concept testing. We recommend role-based access control for production workloads. For more information, see [Connect to Azure AI Search using roles](search-security-rbac).

## Get a synthesized answer

When answer synthesis is enabled, [Knowledge Retrieval - Retrieve (REST API)](/en-us/rest/api/searchservice/knowledge-retrieval/retrieve?view=rest-searchservice-2025-11-01-preview&preserve-view=true) returns a natural-language answer based on the instructions you optionally specified in the knowledge base. Citations to your knowledge sources are formatted as `[ref_id:<number>]`

.

For example, if your instructions are `Use concise bulleted lists`

and your query is `What is healthcare?`

, the response might look like this:

```
{
"response": [
{
"content": [
{
"type": "text",
"text": "- Healthcare encompasses various services provided to patients and the general population ... // TRIMMED FOR BREVITY"
}
]
}
]
}
```


The full `text`

output is as follows:

```
"- Healthcare encompasses various services provided to patients and the general population, including primary health services, hospital care, dental care, mental health services, and alternative health services [ref_id:1].\n- It involves the delivery of safe, effective, patient-centered care through different modalities, such as in-person encounters, shared medical appointments, and group education sessions [ref_id:0].\n- Behavioral health is a significant aspect of healthcare, focusing on the connection between behavior and overall health, including mental health and substance use [ref_id:2].\n- The healthcare system aims to ensure quality of care, access to providers, and accountability for positive outcomes while managing costs effectively [ref_id:2].\n- The global health system is evolving to address complex health needs, emphasizing the importance of cross-sectoral collaboration and addressing social determinants of health [ref_id:4]."
```


Depending on your knowledge base's configuration, the response might include other information, such as activity logs and reference arrays. For more information, see [Create a knowledge base](agentic-retrieval-how-to-create-knowledge-base).


---

<!-- DOCUMENTO FUSIONADO: hybrid-search-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/hybrid-search-overview -->

# Hybrid search using vectors and full text in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Hybrid search is a single query request configured for both full-text and vector queries. It runs against a search index that contains searchable, plain-text content and generated embeddings. For query purposes, hybrid search:

- Is a single query request that includes both
`search`

and`vectors`

query parameters. - Runs full-text search and vector search in parallel.
- Merges results from each query by using
[Reciprocal Rank Fusion (RRF)](hybrid-search-ranking).

This article explains the concepts, benefits, and limitations of hybrid search. Links at the end provide usage instructions and next steps. You can also watch the [embedded video](#why-use-hybrid-search) for an explanation of how hybrid retrieval contributes to high-quality generative search applications.

## Why use hybrid search?

Hybrid search combines the strengths of vector search and keyword search. The advantage of vector search is finding information that's conceptually similar to your search query, even if there are no keyword matches in the inverted index. The advantage of keyword or full-text search is precision, with the ability to apply optional semantic ranking that improves the quality of the initial results. Some scenarios, such as querying over product codes, highly specialized jargon, dates, and people's names, perform better with keyword search because it can identify exact matches.

Benchmark testing on real-world and benchmark datasets indicates that hybrid retrieval with semantic ranker offers significant benefits in search relevance.

The following video explains how hybrid retrieval gives you optimal grounding data for generating useful AI responses.

## How does hybrid search work?

In a search index, vector fields containing embeddings coexist with textual and numerical fields. You can formulate hybrid queries that execute simultaneously. Hybrid queries take advantage of existing text-based functionality like filtering, faceting, sorting, scoring profiles, and [semantic ranking](semantic-search-overview) on your text fields, while executing a similarity search against vectors in a single search request.

Hybrid search combines results from both full-text and vector queries, which use different ranking functions such as BM25 for text, and Hierarchical Navigable Small World (HNSW) and exhaustive K Nearest Neighbors (eKNN) for vectors. An [RRF](hybrid-search-ranking) algorithm merges the results. The query response provides just one result set, using RRF to rank the unified results.

## Structure of a hybrid query

Hybrid search relies on a search index that contains fields of various [data types](/en-us/rest/api/searchservice/supported-data-types), including plain text and numbers, geo coordinates if you want geospatial search, and vectors to mathematically represent a chunk of text. You can use almost all query capabilities in Azure AI Search with a vector query, except for pure text client-side interactions, such as autocomplete and suggestions.

A representative hybrid query might look like the following. For brevity, the vector queries have placeholder values.

```
POST https://{{searchServiceName}}.search.windows.net/indexes/hotels-vector-quickstart/docs/search?api-version=2025-09-01
content-type: application/JSON
{
"count": true,
"search": "historic hotel walk to restaurants and shopping",
"select": "HotelId, HotelName, Category, Description, Address/City, Address/StateProvince",
"filter": "geo.distance(Location, geography'POINT(-77.03241 38.90166)') le 300",
"vectorFilterMode": "postFilter",
"facets": [ "Address/StateProvince"],
"vectorQueries": [
{
"kind": "vector",
"vector": [ <array of embeddings> ]
"k": 50,
"fields": "DescriptionVector",
"exhaustive": true,
"oversampling": 20
},
{
"kind": "vector",
"vector": [ <array of embeddings> ]
"k": 50,
"fields": "Description_frVector",
"exhaustive": false,
"oversampling": 10
}
],
"skip": 0,
"top": 10,
"queryType": "semantic",
"queryLanguage": "en-us",
"semanticConfiguration": "my-semantic-config"
}
```


**Key points:**

`search`

specifies a single full-text search query.`vectorQueries`

specifies vector queries, which can be multiple, targeting multiple vector fields. If the embedding space includes multilingual content, vector queries can find the match with no language analyzers or translation required. If you're using semantic ranker, set`k`

to 50 to maximize its inputs.`select`

specifies which fields to return in results, which should be human-readable text fields if you're showing them to users or sending them to a large language model (LLM).`filters`

can specify geospatial search or other inclusion and exclusion criteria, such as whether parking is included. The geospatial query in this example finds hotels within a 300-kilometer radius of Washington D.C. You can apply the filter at the beginning or end of query processing. If you're using semantic ranker, you probably want post-filtering as the last step, but you should test to confirm which behavior is best for your queries.`facets`

can be used to compute facet buckets over results that are returned from hybrid queries.`queryType=semantic`

invokes[semantic ranker](semantic-search-overview), applying machine reading comprehension to surface more relevant search results. Semantic ranking is optional. If you aren't using this feature, remove the last three lines of the hybrid query.

Filters and facets target data structures within the index that are distinct from the inverted indexes used for full-text search and the vector indexes used for vector search. As such, when filters and faceted operations execute, the search engine can apply the operational result to the hybrid search results in the response.

Notice how there's no `orderby`

in the query. Explicit sort orders override relevanced-ranked results, so if you want similarity and BM25 relevance, omit sorting in your query.

A response from the query might look like the following JSON.

```
{
"@odata.count": 3,
"@search.facets": {
"Address/StateProvince": [
{
"count": 1,
"value": "NY"
},
{
"count": 1,
"value": "VA"
}
]
},
"value": [
{
"@search.score": 0.03333333507180214,
"@search.rerankerScore": 2.5229012966156006,
"HotelId": "49",
"HotelName": "Swirling Currents Hotel",
"Description": "Spacious rooms, glamorous suites and residences, rooftop pool, walking access to shopping, dining, entertainment and the city center.",
"Category": "Luxury",
"Address": {
"City": "Arlington",
"StateProvince": "VA"
}
},
{
"@search.score": 0.032522473484277725,
"@search.rerankerScore": 2.111117362976074,
"HotelId": "48",
"HotelName": "Nordick's Valley Motel",
"Description": "Only 90 miles (about 2 hours) from the nation's capital and nearby most everything the historic valley has to offer. Hiking? Wine Tasting? Exploring the caverns? It's all nearby and we have specially priced packages to help make our B&B your home base for fun while visiting the valley.",
"Category": "Boutique",
"Address": {
"City": "Washington D.C.",
"StateProvince": null
}
}
]
}
```
