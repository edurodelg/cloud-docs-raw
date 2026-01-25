---
merged_at: 2026-01-25T02:11:58.424366
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-overview -->

# Vector search in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Vector search is an information retrieval approach that supports indexing and querying over numeric representations of content. Because the content is numeric rather than plain text, matching is based on vectors that are most similar to the query vector. This approach enables matching across:

- Semantic or conceptual likeness. For example, "dog" and "canine" are conceptually similar but linguistically distinct.
- Multilingual content, such as "dog" in English and "hund" in German.
- Multiple content types, such as "dog" in plain text and an image of a dog.

This article provides an overview of vector search in Azure AI Search, including supported scenarios, availability, and integration with other Azure services.

Tip

Want to get started right away? Follow these steps:

[Provide embeddings](vector-search-how-to-generate-embeddings)for your index or[generate embeddings](vector-search-integrated-vectorization)in an indexer pipeline.[Create a vector index](vector-search-how-to-create-index).[Run vector queries](vector-search-how-to-query).

## What scenarios can vector search support?

Vector search supports the following scenarios:

**Similarity search**. Encode text using embedding models or open-source models, such as OpenAI embeddings or SBERT, respectively. You then retrieve documents using queries that are also encoded as vectors.. Azure AI Search defines hybrid search as the execution of vector search and[Hybrid search](hybrid-search-overview)[keyword search](search-lucene-query-architecture)in the same request. Vector support is implemented at the field level. If an index contains vector and nonvector fields, you can write a query that targets both. The queries execute in parallel, and the results are merged into a single response and ranked accordingly.. Encode text and images using multimodal embeddings, such as[Multimodal search](multimodal-search-overview)[OpenAI CLIP](https://github.com/openai/CLIP)or[GPT-4 Turbo with Vision](/en-us/azure/ai-services/openai/whats-new#gpt-4-turbo-with-vision-now-available)in Azure OpenAI, and then query an embedding space composed of vectors from both content types.**Multilingual search**. Azure AI Search is designed for extensibility. If you have embedding models and chat models trained in multiple languages, you can call them through custom or built-in skills on the indexing side or vectorizers on the query side. For more control over text translation, use the[multi-language capabilities](search-language-support)supported by Azure AI Search for nonvector content in hybrid search scenarios.**Filtered vector search**. A query request can include a vector query and a[filter expression](search-filters). Filters apply to text and numeric fields. They're useful for metadata filters and for including or excluding search results based on filter criteria. Although a vector field isn't filterable, you can set up a filterable text or numeric field. The search engine can process the filter before or after executing the vector query.**Vector database**. Azure AI Search stores the data that you query over. Use it as a[pure vector index](vector-store)when you need long-term memory or a knowledge base, grounding data for the[retrieval-augmented generation (RAG)](retrieval-augmented-generation-overview)architecture, or an app that uses vectors.

## How does vector search work?

Azure AI Search supports indexing, storing, and querying vector embeddings from a search index. The following diagram shows the indexing and query workflows for vector search.

On the indexing side, Azure AI Search uses a [nearest neighbors algorithm](vector-search-ranking) to place similar vectors close together in an index. Internally, it creates [vector indexes](vector-store) for each vector field.

How you get embeddings from your source content into Azure AI Search depends on your processing approach:

For internal processing, Azure AI Search offers

[integrated data chunking and vectorization](vector-search-integrated-vectorization)in an indexer pipeline. You provide the necessary resources, such as endpoints and connection information for Azure OpenAI. Azure AI Search then makes the calls and handles the transitions. This approach requires an indexer, a supported data source, and a skillset that drives chunking and embedding.For external processing, you can

[generate embeddings](vector-search-how-to-generate-embeddings)outside of Azure AI Search and push the prevectorized content directly into[vector fields](vector-search-how-to-create-index)in your search index.

On the query side, your client app collects user input, typically through a prompt. You can add an encoding step to vectorize the input and then send the vector query to your Azure AI Search index for similarity search. As with indexing, you can use [integrated vectorization](vector-search-integrated-vectorization) to encode the query. For either approach, Azure AI Search returns documents with the requested `k`

nearest neighbors (kNN) in the results.

Azure AI Search supports [hybrid scenarios](hybrid-search-overview) that run vector and keyword search in parallel and return a unified result set, which often provides better results than vector or keyword search alone. For hybrid search, both vector and nonvector content are ingested into the same index for queries that run simultaneously.

## Availability and pricing

Vector search is available in [all regions](search-region-support) and on [all tiers](search-sku-tier) at no extra charge. However, generating embeddings or using AI enrichment for vectorization might incur charges from the model provider.

For portal and programmatic access to vector search, you can use:

- The
in the Azure portal.**Import data (new)**wizard - The
[Search Service REST APIs](/en-us/rest/api/searchservice). - The Azure SDKs for
[.NET](https://www.nuget.org/packages/Azure.Search.Documents),[Python](https://pypi.org/project/azure-search-documents), and[JavaScript](https://www.npmjs.com/package/@azure/search-documents). [Other Azure offerings](#azure-integration-and-related-services), such as Microsoft Foundry.

Note

Some search services created before January 1, 2019 don't support vector workloads. If you try to add a vector field to a schema and get an error, it's a result of outdated services. In this situation, you must create a new search service to try out the vector feature.

Search services created after April 3, 2024 offer

[higher quotas for vector indexes](vector-search-index-size). If you have an older service, you might be able to[upgrade your service](search-how-to-upgrade)for higher vector quotas.

## Azure integration and related services

Azure AI Search is deeply integrated across the Azure AI platform. The following table lists products that are useful in vector workloads.

| Product | Integration |
|---|---|
| Azure OpenAI | Azure OpenAI provides embedding models and chat models. Demos and samples target the
|

[Image Retrieval Vectorize Image API](/en-us/azure/ai-services/computer-vision/how-to/image-retrieval#call-the-vectorize-image-api)supports vectorization of image content. We recommend this API for generating embeddings for images.*indexed*that points to a search index containing vector fields and a vectorizer. You can then parent the knowledge source to a[knowledge source](agentic-knowledge-source-overview)*and*[knowledge base](agentic-retrieval-how-to-create-knowledge-base)[connect the knowledge base to Foundry Agent Service](/en-us/azure/ai-foundry/agents/how-to/tools/knowledge-retrieval), providing your agents with vector search results for enhanced knowledge retrieval.[indexers](search-indexer-overview)to automate data ingestion, and then use[integrated vectorization](vector-search-integrated-vectorization)to generate embeddings. Azure AI Search can automatically index vector data from[Azure blob indexers](search-how-to-index-azure-blob-storage),[Azure Cosmos DB for NoSQL indexers](search-how-to-index-cosmosdb-sql),[Azure Data Lake Storage Gen2](search-how-to-index-azure-data-lake-storage),[Azure Table Storage](search-how-to-index-azure-tables), and[Microsoft OneLake](search-how-to-index-onelake-files). For more information, see[Add vector fields to a search index](vector-search-how-to-create-index).It's also commonly used in open-source frameworks like [LangChain](https://js.langchain.com/docs/integrations/vectorstores/azure_aisearch).


---

<!-- DOCUMENTO FUSIONADO: search-synonyms.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-synonyms -->

# Add synonyms in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

On a search service, a synonym map associates equivalent terms, expanding the scope of a query without the user having to actually provide the term. For example, assuming *dog*, *canine*, and *puppy* are mapped synonyms, a query on *canine* matches on a document containing *dog*. You might create multiple synonym maps for different languages, such as English and French versions, or lexicons if your content includes technical jargon, slang, or obscure terminology.

Some key points about synonym maps:

- A synonym map is a top-level resource that can be created once and used by many indexes.
- A synonym map applies to string fields.
- You can create and assign a synonym map at any time with no disruption to indexing or queries.
- Your
[service tier](search-limits-quotas-capacity#synonym-limits)sets the limits on how many synonym maps you can create. - Your search service can have multiple synonym maps, but within an index, a field definition can only have one synonym map assignment.

## Create a synonym map

A synonym map consists of name, format, and rules that function as synonym map entries. The only format that's supported is `solr`

, and the `solr`

format determines rule construction.

To create a synonym map, do so programmatically. the Azure portal doesn't support synonym map definitions.

Use the [Create Synonym Map (REST API)](/en-us/rest/api/searchservice/synonym-maps/create) to create a synonym map.

```
POST /synonymmaps?api-version=2025-09-01
{
"name": "geo-synonyms",
"format": "solr",
"synonyms": "
USA, United States, United States of America\n
Washington, Wash., WA => WA\n"
}
```


### Define rules

Mapping rules adhere to the open-source synonym filter specification of Apache Solr, described in this document: [SynonymGraphFilter](https://cwiki.apache.org/confluence/display/solr/Filter+Descriptions#FilterDescriptions-SynonymGraphFilter). The `solr`

format supports two kinds of rules:

equivalency (where terms are equal substitutes in the query)

explicit mappings (where terms are mapped to one explicit term)


Each rule is delimited by the new line character (`\n`

). You can define up to 5,000 rules per synonym map in a free service and 20,000 rules per map in other tiers. Each rule can have up to 20 expansions, or items in a rule. For more information, see [Synonym limits](search-limits-quotas-capacity#synonym-limits).

Query parsers automatically lower-case any upper or mixed case terms. To preserve special characters in the string, such as a comma or dash, add the appropriate escape characters when creating the synonym map.

### Equivalency rules

Rules for equivalent terms are comma-delimited within the same rule. In the first example, a query on *USA* expands to *USA* OR *"United States"* OR *"United States of America."* Notice that if you want to match on a phrase, the query itself must be a quote-enclosed phrase query.

In the equivalence case, a query for *dog* expands the query to also include *puppy* and *canine*.

```
{
"format": "solr",
"synonyms": "
USA, United States, United States of America\n
dog, puppy, canine\n
coffee, latte, cup of joe, java\n"
}
```


### Explicit mapping

Rules for an explicit mapping are denoted by an arrow `=>`

. When specified, a term sequence of a search query that matches the left-hand side of `=>`

is replaced with the alternatives on the right-hand side at query time.

In the explicit case, a query for *Washington*, *Wash.* or *WA* is rewritten as *WA*, and the query engine only looks for matches on the term *WA*. Explicit mapping only applies in the direction specified, and doesn't rewrite the query *WA* to *Washington* in this case.

```
{
"format": "solr",
"synonyms": "
Washington, Wash., WA => WA\n
California, Calif., CA => CA\n"
}
```


### Escaping special characters

Synonyms are analyzed during query processing just like any other query term, which means that rules for reserved and special characters apply to the terms in your synonym map. The list of characters that require escaping varies between the simple syntax and full syntax:

[simple syntax](query-simple-syntax)`+ | " ( ) ' \`

[full syntax](query-lucene-syntax)`+ - & | ! ( ) { } [ ] ^ " ~ * ? : \ /`


To preserve characters that the default analyzer discards, substitute an analyzer that preserves them. Some choices include Microsoft natural [language analyzers](index-add-language-analyzers), which preserves hyphenated words, or a custom analyzer for more complex patterns. For more information, see [Partial terms, patterns, and special characters](search-query-partial-matching).

The following example shows an example of how to escape a character with a backslash:

```
{
"format": "solr",
"synonyms": "WA\, USA, WA, Washington\n"
}
```


Since the backslash is itself a special character in other languages like JSON and C#, you probably need to double-escape it. Here's an example in JSON:

```
{
"format":"solr",
"synonyms": "WA\\, USA, WA, Washington"
}
```


## Manage synonym maps

You can update a synonym map without disrupting query and indexing workloads. However, once you add a synonym map to a field, if you then delete a synonym map, any query that includes the fields in question fails with a 404 error.

Creating, updating, and deleting a synonym map is always a whole-document operation. You can't update or delete parts of the synonym map incrementally. Updating even a single rule requires a reload.

## Assign synonyms to fields

After you create the synonym map, assign it to a field in your index. To assign synonym maps, do so programmatically. the Azure portal doesn't support synonym map field associations.

- A field must be of type
`Edm.String`

or`Collection(Edm.String)`

- A field must have
`"searchable":true`

- A field can have only one synonym map

If the synonym map exists on the search service, it's used on the next query, with no reindexing or rebuild required.

Use the [Create or Update Index (REST API)](/en-us/rest/api/searchservice/indexes/create-or-update) to modify a field definition.

```
PUT /indexes?api-version=2025-09-01
{
"name":"hotels-sample-index",
"fields":[
{
"name":"description",
"type":"Edm.String",
"searchable":true,
"synonymMaps":[
"en-synonyms"
]
},
{
"name":"description_fr",
"type":"Edm.String",
"searchable":true,
"analyzer":"fr.microsoft",
"synonymMaps":[
"fr-synonyms"
]
}
]
}
```


## Query on equivalent or mapped fields

A synonym field assignment doesn't change how you write queries. After the synonym map assignment, the only difference is that if a query term exists in the synonym map, the search engine either expands or rewrites the term or phrase, depending on the rule.

## How synonyms are used during query execution

Synonyms are a query expansion technique that supplements the contents of an index with equivalent terms, but only for fields that have a synonym assignment. If a field-scoped query *excludes* a synonym-enabled field, you don't see matches from the synonym map.

For synonym-enabled fields, synonyms are subject to the same text analysis as the associated field. For example, if a field is analyzed using the standard Lucene analyzer, synonym terms are also subject to the standard Lucene analyzer at query time. If you want to preserve punctuation, such as periods or dashes, in the synonym term, apply a content-preserving analyzer on the field.

Internally, the synonyms feature rewrites the original query with synonyms by using the OR operator. For this reason, hit highlighting and scoring profiles treat the original term and synonyms as equivalent.

Synonyms apply to free-form text queries only and aren't supported for filters, facets, autocomplete, or suggestions. Autocomplete and suggestions are based only on the original term; synonym matches don't appear in the response.

If you have an existing index in a development (nonproduction) environment, experiment with a small dictionary to see how the addition of synonyms changes the search experience, including impact on scoring profiles, hit highlighting, and suggestions.

### Wildcard searches

Synonym expansions don't apply to wildcard search terms; prefix, fuzzy, and regex terms aren't expanded.

If you need to do a single query that applies synonym expansion and wildcard, regex, or fuzzy searches, you can combine the queries using the OR syntax. For example, to combine synonyms with wildcards for simple query syntax, the term would be `<query> | <query>*`

.
