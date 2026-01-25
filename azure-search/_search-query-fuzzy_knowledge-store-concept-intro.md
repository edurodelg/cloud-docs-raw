---
merged_at: 2026-01-25T03:18:13.803781
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-query-fuzzy.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-fuzzy -->

# Fuzzy search to correct misspellings and typos

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search supports fuzzy search, a type of query that compensates for typos and misspelled terms in the input string. Fuzzy search scans for terms having a similar composition. Expanding search to cover near-matches has the effect of autocorrecting a typo when the discrepancy is just a few misplaced characters.

## What is fuzzy search?

It's a query expansion exercise that produces a match on terms having a similar composition. When a fuzzy search is specified, the search engine builds a graph (based on [deterministic finite automaton theory](https://en.wikipedia.org/wiki/Deterministic_finite_automaton)) of similarly composed terms, for all whole terms in the query. For example, if your query includes three terms `"university of washington"`

, a graph is created for every term in the query `search=university~ of~ washington~`

(there's no stop-word removal in fuzzy search, so `"of"`

gets a graph).

The graph consists of up to 50 expansions, or permutations, of each term, capturing both correct and incorrect variants in the process. The engine then returns the topmost relevant matches in the response.

For a term like "university", the graph might have `"unversty, universty, university, universe, inverse"`

. Any documents that match on those in the graph are included in results. In contrast with other queries that analyze the text to handle different forms of the same word ("mice" and "mouse"), the comparisons in a fuzzy query are taken at face value without any linguistic analysis on the text. "Universe" and "inverse", which are semantically different, will match because the syntactic discrepancies are small.

A match succeeds if the discrepancies are limited to two or fewer edits, where an edit is an inserted, deleted, substituted, or transposed character. The string correction algorithm that specifies the differential is the [Damerau-Levenshtein distance](https://en.wikipedia.org/wiki/Damerau%E2%80%93Levenshtein_distance) metric. It's described as the "minimum number of operations (insertions, deletions, substitutions, or transpositions of two adjacent characters) required to change one word into the other".

In Azure AI Search:

Fuzzy query applies to whole terms. Phrases aren't supported directly but you can specify a fuzzy match on each term of a multi-part phrase through AND constructions. For example,

`search=dr~ AND cleanin~`

. This query expression finds matches on "dry cleaning".The default distance of an edit is 2. A value of

`~0`

signifies no expansion (only the exact term is considered as a match), but you could specify`~1`

for one degree of difference, or one edit.A fuzzy query can expand a term up to 50 permutations. This limit isn't configurable, but you can effectively reduce the number of expansions by decreasing the edit distance to 1.

Responses consist of documents containing a relevant match (up to 50).


During query processing, fuzzy queries don't undergo [lexical analysis](search-lucene-query-architecture#stage-2-lexical-analysis). The query input is added directly to the query tree and expanded to create a graph of terms. The only transformation performed is lower casing.

Collectively, the graphs are submitted as match criteria against tokens in the index. As you can imagine, fuzzy search is inherently slower than other query forms. The size and complexity of your index can determine whether the benefits are enough to offset the latency of the response.

Note

Because fuzzy search tends to be slow, it might be worthwhile to investigate alternatives such as n-gram indexing, with its progression of short character sequences (two and three character sequences for bigram and trigram tokens). Depending on your language and query surface, n-gram might give you better performance. The trade-off is that n-gram indexing is very storage intensive and generates much bigger indexes.

Another alternative, which you could consider if you want to handle just the most egregious cases, would be a [synonym map](search-synonyms). For example, mapping "search" to "serach, serch, sarch", or "retrieve" to "retreive".

## Indexing for fuzzy search

String fields that are attributed as "searchable" are candidates for fuzzy search.

Analyzers aren't used to create an expansion graph, but that doesn't mean analyzers should be ignored in fuzzy search scenarios. Analyzers are important for tokenization during indexing, where tokens in the inverted indexes are used for matching against the graph.

As always, if test queries aren't producing the matches you expect, experiment with different indexing analyzers. For example, try a [language analyzer](index-add-language-analyzers) to see if you get better results. Some languages, particularly those with vowel mutations, can benefit from the inflection and irregular word forms generated by the Microsoft natural language processors. In some cases, using the right language analyzer can make a difference in whether a term is tokenized in a way that is compatible with the value provided by the user.

## How to invoke fuzzy search

Fuzzy queries are constructed using the full Lucene query syntax, invoking the [full Lucene query parser](https://lucene.apache.org/core/6_6_1/queryparser/org/apache/lucene/queryparser/classic/package-summary.html), and appending a tilde character `~`

after each whole term entered by the user.

Here's an example of a query request that invokes fuzzy search. It includes four terms, two of which are misspelled:

```
POST https://[service name].search.windows.net/indexes/hotels-sample-index/docs/search?api-version=2025-09-01
{
"search": "seatle~ waterfront~ view~ hotle~",
"queryType": "full",
"searchMode": "any",
"searchFields": "HotelName, Description",
"select": "HotelName, Description, Address/City,",
"count": "true"
}
```


Set the query type to the full Lucene syntax (

`queryType=full`

).Provide the query string where each term is followed by a tilde (

`~`

) operator at the end of each whole term (`search=<string>~`

). An expansion graph is created for every term in the query input.Include an optional parameter, a number between 0 and 2 (default), if you want to specify the edit distance (

`~1`

). For example, "blue~" or "blue~1" would return "blue", "blues", and "glue".

Optionally, you can improve query performance by scoping the request to specific fields. Use the `searchFields`

parameter to specify which fields to search. You can also use the `select`

property to specify which fields are returned in the query response.

## Testing fuzzy search

For simple testing, we recommend [Search explorer](search-explorer) or a [REST client](search-get-started-text) for iterating over a query expression. Both tools are interactive, which means you can quickly step through multiple variants of a term and evaluate the responses that come back.

When results are ambiguous, [hit highlighting](search-pagination-page-layout#hit-highlighting) can help you identify the match in the response.

Note

The use of hit highlighting to identify fuzzy matches has limitations and only works for basic fuzzy search. If your index has scoring profiles, or if you layer the query with more syntax, hit highlighting might fail to identify the match.

### Example 1: fuzzy search with the exact term

Assume the following string exists in a `"Description"`

field in a search document: `"Test queries with special characters, plus strings for MSFT, SQL and Java."`


Start with a fuzzy search on "special" and add hit highlighting to the Description field:

```
search=special~&highlight=Description
```


In the response, because you added hit highlighting, formatting is applied to "special" as the matching term.

```
"@search.highlights": {
"Description": [
"Test queries with <em>special</em> characters, plus strings for MSFT, SQL and Java."
]
}
```


Try the request again, misspelling "special" by taking out several letters (`"pe"`

):

```
search=scial~&highlight=Description
```


So far, no change to the response. Given the default of 2 degrees distance, removing two characters `"pe"`

from "special" still allows for a successful match on that term.

```
"@search.highlights": {
"Description": [
"Test queries with <em>special</em> characters, plus strings for MSFT, SQL and Java."
]
}
```


Trying one more request, further modify the search term by taking out one last character for a total of three deletions (from "special" to `"scal"`

):

```
search=scal~&highlight=Description
```


Notice that the same response is returned, but now instead of matching on "special", the fuzzy match is on "SQL".

```
"@search.score": 0.4232868,
"@search.highlights": {
"Description": [
"Mix of special characters, plus strings for MSFT, <em>SQL</em>, 2019, Linux, Java."
]
}
```


The point of this expanded example is to illustrate the clarity that hit highlighting can bring to ambiguous results. In all cases, the same document is returned. Had you relied on document IDs to verify a match, you might have missed the shift from "special" to "SQL".


---

<!-- DOCUMENTO FUSIONADO: knowledge-store-concept-intro.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/knowledge-store-concept-intro -->

# Knowledge store in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

*Knowledge stores* are secondary storage that exists in Azure Storage and contain the outputs of Azure AI Search skillsets. They're separate from knowledge sources and knowledge bases, which are used in [agentic retrieval](agentic-retrieval-overview) workflows.

Knowledge store is secondary storage for [AI-enriched content created by a skillset](cognitive-search-concept-intro) in Azure AI Search. In Azure AI Search, an indexing job always sends output to a search index, but if you attach a skillset to an indexer, you can optionally also send AI-enriched output to a container or table in Azure Storage. A knowledge store can be used for independent analysis or downstream processing in non-search scenarios like knowledge mining.

The two outputs of indexing, a search index and knowledge store, are mutually exclusive products of the same pipeline. They're derived from the same inputs and contain the same data, but their content is structured, stored, and used in different applications.


Physically, a knowledge store is [Azure Storage](/en-us/azure/storage/common/storage-account-overview), either Azure Table Storage, Azure Blob Storage, or both. Any tool or process that can connect to Azure Storage can consume the contents of a knowledge store. There's no query support in Azure AI Search for retrieving content from a knowledge store.

When viewed through Azure portal, a knowledge store looks like any other collection of tables, objects, or files. The following screenshot shows a knowledge store composed of three tables. You can adopt a naming convention, such as a `kstore`

prefix, to keep your content together.


## Benefits of knowledge store

The primary benefits of a knowledge store are two-fold: flexible access to content, and the ability to shape data.

Unlike a search index that can only be accessed through queries in Azure AI Search, a knowledge store is accessible to any tool, app, or process that supports connections to Azure Storage. This flexibility opens up new scenarios for consuming the analyzed and enriched content produced by an enrichment pipeline.

The same skillset that enriches data can also be used to shape data. Some tools like Power BI work better with tables, whereas a data science workload might require a complex data structure in a blob format. Adding a [Shaper skill](cognitive-search-skill-shaper) to a skillset gives you control over the shape of your data. You can then pass these shapes to projections, either tables or blobs, to create physical data structures that align with the data's intended use.

The following video explains both of these benefits and more.

## Knowledge store definition

A knowledge store is defined inside a skillset definition and it has two components:

A connection string to Azure Storage

that determine whether the knowledge store consists of tables, objects or files. The projections element is an array. You can create multiple sets of table-object-file combinations within one knowledge store.**Projections**`"knowledgeStore": { "storageConnectionString":"<YOUR-AZURE-STORAGE-ACCOUNT-CONNECTION-STRING>", "projections":[ { "tables":[ ], "objects":[ ], "files":[ ] } ] }`


The type of projection you specify in this structure determines the type of storage used by knowledge store, but not its structure. Fields in tables, objects, and files are determined by Shaper skill output if you're creating the knowledge store programmatically, or by the Import data wizard if you're using the Azure portal.

`tables`

project enriched content into Table Storage. Define a table projection when you need tabular reporting structures for inputs to analytical tools or export as data frames to other data stores. You can specify multiple`tables`

within the same projection group to get a subset or cross section of enriched documents. Within the same projection group, table relationships are preserved so that you can work with all of them.Projected content isn't aggregated or normalized. The following screenshot shows a table, sorted by key phrase, with the parent document indicated in the adjacent column. In contrast with data ingestion during indexing, there's no linguistic analysis or aggregation of content. Plural forms and differences in casing are considered unique instances.

`objects`

project JSON document into Blob storage. The physical representation of an`object`

is a hierarchical JSON structure that represents an enriched document.`files`

project image files into Blob storage. A`file`

is an image extracted from a document, transferred intact to Blob storage. Although it's named "files", it shows up in Blob Storage, not file storage.

## Create a knowledge store

To create knowledge store, use the Azure portal or an API.

You need [Azure Storage](/en-us/azure/storage/), a [skillset](cognitive-search-working-with-skillsets), and an [indexer](search-indexer-overview). Because indexers require a search index, you also need to provide an [index definition](search-how-to-create-search-index).

Go with the Azure portal approach for the fastest route to a finished knowledge store. Or, choose the REST API for a deeper understanding of how objects are defined and related.

[ Create your first knowledge store in four steps](knowledge-store-create-portal) using the

**Import data**wizard.

Define a data source that contains the data you want to enrich.

Define a skillset. The skillset specifies enrichment steps and the knowledge store.

Define an index schema. You might not need one, but indexers require it. The wizard can infer an index.

Complete the wizard. Data extraction, enrichment, and knowledge store creation occur in this last step.


The wizard automates several tasks. Specifically, both data shaping and projections (definitions of physical data structures in Azure Storage) are created for you.

## Connect with apps

Once enriched content exists in storage, any tool or technology that connects to Azure Storage can be used to explore, analyze, or consume the contents. The following list is a start:

[Storage Explorer](/en-us/azure/storage/blobs/quickstart-storage-explorer)or Storage browser in the Azure portal to view enriched document structure and content. Consider this as your baseline tool for viewing knowledge store contents.[Power BI](knowledge-store-connect-power-bi)for reporting and analysis.[Azure Data Factory](/en-us/azure/data-factory/)for further manipulation.

## Content lifecycle

Each time you run the indexer and skillset, the knowledge store is updated if the skillset or underlying source data has changed. Any changes picked up by the indexer are propagated through the enrichment process to the projections in the knowledge store, ensuring that your projected data is a current representation of content in the originating data source.

Note

While you can edit the data in the projections, any edits will be overwritten on the next pipeline invocation, assuming the document in source data is updated.

### Changes in source data

For data sources that support change tracking, an indexer will process new and changed documents, and bypass existing documents that have already been processed. Timestamp information varies by data source, but in a blob container, the indexer looks at the `lastmodified`

date to determine which blobs need to be ingested.

### Changes to a skillset

If you're making changes to a skillset, you should [enable caching of enriched documents](enrichment-cache-how-to-configure) to reuse existing enrichments where possible.

Without incremental caching, the indexer will always process documents in order of the high water mark, without going backwards. For blobs, the indexer would process blobs sorted by `lastModified`

, regardless of any changes to indexer settings or the skillset. If you change a skillset, previously processed documents aren't updated to reflect the new skillset. Documents processed after the skillset change will use the new skillset, resulting in index documents being a mix of old and new skillsets.

With incremental caching, and after a skillset update, the indexer will reuse any enrichments that are unaffected by the skillset change. Upstream enrichments are pulled from cache, as are any enrichments that are independent and isolated from the skill that was changed.

### Deletions

Although an indexer creates and updates structures and content in Azure Storage, it doesn't delete them. Projections continue to exist even when the indexer or skillset is deleted. As the owner of the storage account, you should delete a projection if it's no longer needed.

## Next steps

Knowledge store offers persistence of enriched documents, useful when designing a skillset, or the creation of new structures and content for consumption by any client applications capable of accessing an Azure Storage account.

The simplest approach for creating enriched documents is [through the Azure portal](knowledge-store-create-portal), but a REST client and REST APIs can provide more insight into how objects are created and referenced programmatically.
