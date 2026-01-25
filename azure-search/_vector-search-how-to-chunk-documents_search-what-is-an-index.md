---
merged_at: 2026-01-25T02:11:58.480737
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-how-to-chunk-documents.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-chunk-documents -->

# Chunk large documents for agentic retrieval and vector search in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Partitioning large documents into smaller chunks can help you stay under the maximum token input limits of chat completion and embedding models. For example, the maximum length of input text for the [Azure OpenAI](/en-us/azure/ai-services/openai/how-to/embeddings) text-embedding-3-small model is 8,191 tokens. Given that each token is around four characters of text for common OpenAI models, this maximum limit is equivalent to around 6,000 words of text. If you're using these models to generate embeddings, it's critical that the input text stays under the limit.

Chat completion models have the same input token restrictions, so chunking is helpful for retrieval augmented generation (RAG) or agentic retrieval as well. Partitioning your content into chunks helps you meet input token requirements and prevents data loss due to truncation.

Azure AI Search has built-in solutions for chunking content, and also for vectorizing chunked content if you're using vector search. The built-in approach takes a dependency on [built-in indexers](search-indexer-overview) and [skillsets](vector-search-integrated-vectorization) that enable text splitting and embeddings generation. If you can't use integrated vectorization, this article describes some alternative approaches for chunking your content.

Tip

If you're chunking content for agentic retrieval, several knowledge sources can generate a full indexer pipeline that chunks and optionally vectorizes your content. The indexer, data source definition, skillset, and are created for you based on information in your knowledge source definition. Knowledge sources with this capability include [Azure blob](agentic-knowledge-source-how-to-blob) and [OneLake](agentic-knowledge-source-how-to-onelake).

## Common chunking techniques

Chunking is only required if the source documents are too large for the maximum input size imposed by models, but it's also beneficial if content is poorly represented as a single vector. Consider a wiki page that covers numerous varied sub-topics. The entire page might be small enough to meet model input requirements, but you might get better results if you chunk at a finer grain.

Here are some common chunking techniques, associated with built-in features if you use [indexers](search-indexer-overview) and [skills](cognitive-search-working-with-skillsets).

| Approach | Usage | Built-in functionality |
|---|---|---|
| Fixed-size chunks | Define a fixed size that's sufficient for semantically meaningful paragraphs (for example, 200 words or 600 characters) and allows for some overlap (for example, 10-15% of the content) can produce good chunks as input for embedding vector generators. |
|

[Document Layout skill](cognitive-search-skill-document-intelligence-layout)or[Text Split skill](cognitive-search-skill-textsplit)(splitting by sentences).[Azure Content Understanding skill](cognitive-search-skill-content-understanding)(semantic chunking with markdown output)*chunking*but it can sometimes achieve the same objective.[Index Markdown blobs and files](search-how-to-index-azure-blob-markdown),[one-to-many indexing](search-how-to-index-azure-blob-one-to-many), or[Index JSON blobs and files](search-how-to-index-azure-blob-json)### Content overlap considerations

When you chunk data based on fixed size, overlapping a small amount of text between chunks can help maintaining continuity and context. We recommend starting with a chunk size of 512 tokens (approximately 2,000 characters) and an initial overlap of 25%, which equals 128 tokens. This overlap ensures smoother transitions between chunks without excessive duplication.

The optimal overlap may vary depending on your content type and use case. For example, highly structured data may require less overlap, while conversational or narrative text may benefit from more.

### Factors for chunking data

When it comes to chunking data, think about these factors:

Shape and density of your documents. If you need intact text or passages, larger chunks and variable chunking that preserves sentence structure can produce better results.

User queries: Larger chunks and overlapping strategies help preserve context and semantic richness for queries that target specific information.

Large Language Models (LLM) have performance guidelines for chunk size. Find a chunk size that works best for all of the models you're using. For instance, if you use models for summarization and embeddings, choose an optimal chunk size that works for both.


### How chunking fits into the workflow

If you have large documents, insert a chunking step into indexing and query workflows that breaks up large text. When using [integrated vectorization](vector-search-integrated-vectorization), a default chunking strategy using the [Text Split skill](cognitive-search-skill-textsplit) is common. You can also apply a custom chunking strategy using a [custom skill](cognitive-search-custom-skill-web-api). See [this code reference](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/indexers/document-intelligence-custom-skill/document-intelligence-custom-skill.ipynb) for a semantic chunking example using a custom skill. Some external libraries that provide chunking include:

Most libraries provide common chunking techniques for fixed size, variable size, or a combination. You can also specify an overlap that duplicates a small amount of content in each chunk for context preservation.

## Chunking examples

The following examples demonstrate how chunking strategies are applied to [NASA's Earth at Night e-book](https://github.com/Azure-Samples/azure-search-sample-data/blob/main/nasa-e-book/earth_at_night_508.pdf) PDF file:

### Text Split skill example

Integrated data chunking through [Text Split skill](cognitive-search-skill-textsplit) is generally available.

This section describes built-in data chunking using a skills-driven approach and [Text Split skill parameters](cognitive-search-skill-textsplit#skill-parameters).

A sample notebook for this example can be found on the [azure-search-vector-samples](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/data-chunking/textsplit-data-chunking-example.ipynb) repository.
Set `textSplitMode`

to break up content into smaller chunks:

`pages`

(default). Chunks are made up of multiple sentences.`sentences`

. Chunks are made up of single sentences. What constitutes a "sentence" is language dependent. In English, standard sentence ending punctuation such as`.`

or`!`

is used. The language is controlled by the`defaultLanguageCode`

parameter.

The `pages`

parameter adds extra parameters:

`maximumPageLength`

defines the maximum number of characters1or tokens2in each chunk. The text splitter avoids breaking up sentences, so the actual character count depends on the content.`pageOverlapLength`

defines how many characters from the end of the previous page are included at the start of the next page. If set, this must be less than half the maximum page length.`maximumPagesToTake`

defines how many pages / chunks to take from a document. The default value is 0, which means to take all pages or chunks from the document.

1 Characters don't align to the definition of a [token](/en-us/azure/ai-services/openai/concepts/prompt-engineering#space-efficiency). The number of tokens measured by the LLM might be different than the character size measured by the Text Split skill with the character fixed-size.

2 Token chunking is available in the [2025-11-01-preview](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true) and includes extra parameters for specifying a tokenizer and any tokens that shouldn't be split up during chunking.

The following table shows how the choice of parameters affects the total chunk count from the Earth at Night e-book:

`textSplitMode` |
`maximumPageLength` |
`pageOverlapLength` |
Total Chunk Count |
|---|---|---|---|
`pages` |
1000 | 0 | 172 |
`pages` |
1000 | 200 | 216 |
`pages` |
2000 | 0 | 85 |
`pages` |
2000 | 500 | 113 |
`pages` |
5000 | 0 | 34 |
`pages` |
5000 | 500 | 38 |
`sentences` |
N/A | N/A | 13361 |

Using a `textSplitMode`

of `pages`

results in most chunks having total character counts close to `maximumPageLength`

. Chunk character count varies due to differences on where sentence boundaries fall inside the chunk. Chunk token length varies due to differences in the contents of the chunk.

The optimal choice of parameters depends on how the chunks are used. For most applications, it's recommended to start with the following default parameters, when using number of characters:

`textSplitMode` |
`maximumPageLength` |
`pageOverlapLength` |
|---|---|---|
`pages` |
2000 | 500 |

### LangChain data chunking example

LangChain provides document loaders and text splitters. This example shows you how to load a PDF, get token counts, and set up a text splitter. Getting token counts helps you make an informed decision on chunk sizing.

A sample notebook for this example can be found on the [azure-search-vector-samples](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/data-chunking/langchain-data-chunking-example.ipynb) repository.

```
from langchain_community.document_loaders import PyPDFLoader
loader = PyPDFLoader("./data/earth_at_night_508.pdf")
pages = loader.load()
print(len(pages))
```


Output indicates 200 documents or pages in the PDF.

To get an estimated token count for these pages, use TikToken.

```
import tiktoken
tokenizer = tiktoken.get_encoding('cl100k_base')
def tiktoken_len(text):
tokens = tokenizer.encode(
text,
disallowed_special=()
)
return len(tokens)
tiktoken.encoding_for_model('gpt-4.1-mini')
# create the length function
token_counts = []
for page in pages:
token_counts.append(tiktoken_len(page.page_content))
min_token_count = min(token_counts)
avg_token_count = int(sum(token_counts) / len(token_counts))
max_token_count = max(token_counts)
# print token counts
print(f"Min: {min_token_count}")
print(f"Avg: {avg_token_count}")
print(f"Max: {max_token_count}")
```


Output indicates that no pages have zero tokens, the average token length per page is 189 tokens, and the maximum token count of any page is 1,583.

Knowing the average and maximum token size gives you insight into setting chunk size. Although you could use the standard recommendation of 2,000 characters with a 500 character overlap, in this case it makes sense to go lower given the token counts of the sample document. In fact, setting an overlap value that's too large can result in no overlap appearing at all.

```
from langchain.text_splitter import RecursiveCharacterTextSplitter
# split documents into text and embeddings
text_splitter = RecursiveCharacterTextSplitter(
chunk_size=1000,
chunk_overlap=200,
length_function=len,
is_separator_regex=False
)
chunks = text_splitter.split_documents(pages)
print(chunks[20])
print(chunks[21])
```


Output for two consecutive chunks shows the text from the first chunk overlapping onto the second chunk. Output is lightly edited for readability.

`'x Earth at NightForeword\nNASA’s Earth at Night explores the brilliance of our planet when it is in darkness. \n It is a compilation of stories depicting the interactions between science and \nwonder, and I am pleased to share this visually stunning and captivating exploration of \nour home planet.\nFrom space, our Earth looks tranquil. The blue ethereal vastness of the oceans \nharmoniously shares the space with verdant green land—an undercurrent of gentle-ness and solitude. But spending time gazing at the images presented in this book, our home planet at night instantly reveals a different reality. Beautiful, filled with glow-ing communities, natural wonders, and striking illumination, our world is bustling with activity and life.**\nDarkness is not void of illumination. It is the contrast, the area between light and'** metadata={'source': './data/earth_at_night_508.pdf', 'page': 9}`


`'**Darkness is not void of illumination. It is the contrast, the area between light and **\ndark, that is often the most illustrative. Darkness reminds me of where I came from and where I am now—from a small town in the mountains, to the unique vantage point of the Nation’s capital. Darkness is where dreamers and learners of all ages peer into the universe and think of questions about themselves and their space in the cosmos. Light is where they work, where they gather, and take time together.\nNASA’s spacefaring satellites have compiled an unprecedented record of our \nEarth, and its luminescence in darkness, to captivate and spark curiosity. These missions see the contrast between dark and light through the lenses of scientific instruments. Our home planet is full of complex and dynamic cycles and processes. These soaring observers show us new ways to discern the nuances of light created by natural and human-made sources, such as auroras, wildfires, cities, phytoplankton, and volcanoes.' metadata={'source': './data/earth_at_night_508.pdf', 'page': 9}`


### Custom skill

A [fixed-sized chunking and embedding generation sample](https://github.com/Azure-Samples/azure-search-power-skills/blob/main/Vector/EmbeddingGenerator/README.md) demonstrates both chunking and vector embedding generation using [Azure OpenAI](/en-us/azure/ai-services/openai/) embedding models. This sample uses an [Azure AI Search custom skill](cognitive-search-custom-skill-web-api) in the [Power Skills repo](https://github.com/Azure-Samples/azure-search-power-skills/tree/main#readme) to wrap the chunking step.


---

<!-- DOCUMENTO FUSIONADO: search-what-is-an-index.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-what-is-an-index -->

# Search indexes in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, a *search index* is your searchable content, available to the search engine for indexing, agentic search, full-text search, vector search, hybrid search, and filtered queries. An index is defined by a schema and saved to the search service, with data ingestion following as a second step. Indexed content exists within your search service, apart from your primary external data stores, which is necessary for the millisecond response times expected in modern search applications. Except for indexer-driven indexing scenarios, the search service never connects to or queries your external source data.

This article covers the key concepts for creating and managing a search index, including:

- Content (documents and schema)
- Physical data structure
- Basic operations

Tip

Want to get started right away? See [Create a search index](search-how-to-create-search-index).

## Schema of a search index

In Azure AI Search, indexes contain *search documents*. Conceptually, a document is a single unit of searchable data in your index. For example, a retailer might have a document for each product, a university might have a document for each class, a travel site might have a document for each hotel and destination, and so forth. Mapping these concepts to more familiar database equivalents: a *search index* equates to a *table*, and *documents* are roughly equivalent to *rows* in a table.

The structure of a document is determined by the *index schema*, as illustrated in the following example. The "fields" collection is typically the largest part of an index, where each field is named, assigned a [data type](/en-us/rest/api/searchservice/Supported-data-types), and attributed with allowable behaviors that determine how it's used.

```
{
"name": "name_of_index, unique across the service",
"description" : "Health plan coverage for standard and premium plans for Northwind and Contoso employees."
"fields": [
{
"name": "name_of_field",
"type": "Edm.String | Collection(Edm.String) | Collection(Edm.Single) | Edm.Int32 | Edm.Int64 | Edm.Double | Edm.Boolean | Edm.DateTimeOffset | Edm.GeographyPoint",
"searchable": true (default where applicable) | false (only Edm.String and Collection(Edm.String) fields can be searchable),
"filterable": true (default) | false,
"sortable": true (default where applicable) | false (Collection(Edm.String) fields cannot be sortable),
"facetable": true (default where applicable) | false (Edm.GeographyPoint fields cannot be facetable),
"key": true | false (default, only Edm.String fields can be keys),
"retrievable": true (default) | false,
"analyzer": "name_of_analyzer_for_search_and_indexing", (only if 'searchAnalyzer' and 'indexAnalyzer' are not set)
"searchAnalyzer": "name_of_search_analyzer", (only if 'indexAnalyzer' is set and 'analyzer' is not set)
"indexAnalyzer": "name_of_indexing_analyzer", (only if 'searchAnalyzer' is set and 'analyzer' is not set)
"normalizer": "name_of_normalizer", (applies to fields that are filterable)
"synonymMaps": "name_of_synonym_map", (optional, only one synonym map per field is currently supported)
"dimensions": "number of dimensions used by an embedding models", (applies to vector fields only, of type Collection(Edm.Single))
"vectorSearchProfile": "name_of_vector_profile" (indexes can have many configurations, a field can use just one)
}
],
"suggesters": [ ],
"scoringProfiles": [ ],
"analyzers":(optional)[ ... ],
"charFilters":(optional)[ ... ],
"tokenizers":(optional)[ ... ],
"tokenFilters":(optional)[ ... ],
"defaultScoringProfile": (optional) "...",
"corsOptions": (optional) { },
"encryptionKey":(optional){ },
"semantic":(optional){ },
"vectorSearch":(optional){ }
}
```


Other elements are collapsed for brevity, but the following links provide details:

[suggesters](index-add-suggesters)support type-ahead queries like autocomplete.[scoringProfiles](index-add-scoring-profiles)are used for relevance tuning.[analyzers](search-analyzers)are used to process strings into tokens according to linguistic rules or other characteristics supported by the analyzer.[corsOptions](search-how-to-create-search-index#corsoptions), or Cross-origin remote scripting (CORS), is used for apps that issues requests from different domains.[encryptionKey](search-security-manage-encryption-keys)configures double-encryption of sensitive content in the index.[semantic](semantic-how-to-query-request)configures semantic reranking in full text and hybrid search.[vectorSearch](vector-search-how-to-create-index)configures vector fields and queries.

### Field definitions

A search document is defined by the "fields" collection in the body of [Create Index request](/en-us/rest/api/searchservice/indexes/create). You need fields for document identification (keys), storing searchable text, and fields for supporting filters, facets, and sorting. You might also need fields for data that a user never sees. For example, you might want fields for profit margins or marketing promotions that you can use in a scoring profile to boost a search score.

If incoming data is hierarchical in nature, you can represent it within an index as a [complex type](search-howto-complex-data-types), used for nested structures. The sample data set, [Hotels](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels), illustrates complex types using an Address (contains multiple subfields) that has a one-to-one relationship with each hotel, and a Rooms complex collection, where multiple rooms are associated with each hotel.

### Field attributes

Field attributes determine how a field is used, such as whether it's used in full text search, faceted navigation, sort operations, and so forth.

String fields are often marked as "searchable" and "retrievable". Fields used to narrow search results include "sortable", "filterable", and "facetable".

| Attribute | Description |
|---|---|
| "searchable" | Full-text or vector searchable. Text fields are subject to lexical analysis such as word-breaking during indexing. If you set a searchable field to a value like "sunny day", internally it's split into the individual tokens "sunny" and "day". For details, see
|

`Edm.String`

or `Collection(Edm.String)`

don't undergo word-breaking, so comparisons are for exact matches only. For example, if you set such a field f to "sunny day", `$filter=f eq 'sunny'`

finds no matches, but `$filter=f eq 'sunny day'`

will.`Collection(Edm.String)`

can't be "sortable".`Edm.GeographyPoint`

. Fields of type `Edm.String`

that are filterable, "sortable", or "facetable" can be at most 32 kilobytes in length. For details, see [Create Index (REST API)](/en-us/rest/api/searchservice/indexes/create).`Edm.String`

.*profit margin*) as a filter, sorting, or scoring mechanism, but don't want the field to be visible to the end user. This attribute must be`true`

for `key`

fields.Although you can add new fields at any time, existing field definitions are locked in for the lifetime of the index. For this reason, developers typically use the Azure portal for creating simple indexes, testing ideas, or using the Azure portal pages to look up a setting. Frequent iteration over an index design is more efficient if you follow a code-based approach so that you can rebuild the index easily.

Note

The APIs you use to build an index have varying default behaviors. For the [REST APIs](/en-us/rest/api/searchservice/indexes/create), most attributes are enabled by default (for example, "searchable" and "retrievable" are true for string fields) and you often only need to set them if you want to turn them off. For the .NET SDK, the opposite is true. On any property you do not explicitly set, the default is to disable the corresponding search behavior unless you specifically enable it.

## Physical structure and size

In Azure AI Search, the physical structure of an index is largely an internal implementation. You can access its schema, load and query its content, monitor its size, and manage its capacity. However, Microsoft manages the infrastructure and physical data structures stored with your search service.

You can monitor index size on the **Search management > Indexes** page in the Azure portal. Alternatively, you can issue a [GET INDEX request](/en-us/rest/api/searchservice/indexes/get) against your search service or a [Service Statistics request](/en-us/rest/api/searchservice/get-service-statistics/get-service-statistics) to check the value of storage size.

The size of an index is determined by the:

- Quantity and composition of your documents.
- Attributes on individual fields: "retrievable" doesn't bloat your index, but "filterable", "sortable", "facetable" consume more storage for storing non-tokenized text.
- Index configuration. Specifically, whether you include suggesters or specialized
[analyzers](search-analyzers). If you use the edgeNgram tokenizer to store verbatim sequences of characters (`a, ab, abc, abcd`

), the index is larger than if you use the standard analyzer.

Document composition and quantity are determined by what you choose to import. Remember that a search index should only contain content that's useful for your search application. If source data includes binary fields, omit those fields unless you're using AI enrichment to crack and analyze the content to create text-searchable information.

Field attributes determine behaviors. To support those behaviors, the indexing process creates the necessary data structures. For example, for a field of type `Edm.String`

, "searchable" invokes [full-text search](search-lucene-query-architecture), which scans inverted indexes for the tokenized term. In contrast, a "filterable" or "sortable" attribute supports iteration over unmodified strings.

[ Suggesters](index-add-suggesters) are constructs that support type-ahead or autocomplete queries. When you include a suggester, the indexing process creates the data structures necessary for verbatim character matches. Suggesters are implemented at the field level, so choose only those fields that are reasonable for type-ahead.

## Basic operations and interaction

Now that you have a better idea of what an index is, this section introduces index runtime operations, including connecting to and securing a single index.

Note

There's no portal or API support for moving or copying an index. Typically, you either point your application deployment to a different search service (using the same index name) or revise the name to create a copy on your current search service and then build it.

### Index isolation

In Azure AI Search, you work with one index at a time. All index-related operations target a single index. There's no concept of related indexes or the joining of independent indexes for either indexing or querying.

### Continuously available

An index is immediately available for queries as soon as the first document is indexed, but it's not fully operational until all documents are indexed. Internally, an index is [distributed across partitions and executes on replicas](search-capacity-planning#concepts-search-units-replicas-partitions). The physical index is managed internally. You manage the logical index.

An index is continuously available and can't be paused or taken offline. Because it's designed for continuous operation, updates to its content and additions to the index itself happen in real time. If a request coincides with a document update, queries might temporarily return incomplete results.

Query continuity exists for document operations, such as refreshing or deleting, and for modifications that don't affect the existing structure or integrity of an index, such as adding new fields. Structural updates, such as changing existing fields, are typically managed using a drop-and-rebuild workflow in a development environment or by creating a new version of the index on the production service.

To avoid an [index rebuild](search-howto-reindex), some customers who are making small changes "version" a field by creating a new one that coexists with a previous version. Over time, this leads to orphaned content by way of obsolete fields and obsolete custom analyzer definitions, especially in a production index that's expensive to replicate. You can address these issues during planned updates to the index as part of index lifecycle management.

### Endpoint connection and security

All indexing and query requests target an index. Endpoints are usually one of the following:

| Endpoint | Connection and access control |
|---|---|
`<your-service>.search.windows.net/indexes` |
Targets the indexes collection. Used when creating, listing, or deleting an index. Admin rights are required for these operations and available through admin
|

`<your-service>.search.windows.net/indexes/<your-index>/docs`

#### How to connect to Azure AI Search

[Start with the Azure portal](https://portal.azure.com). Azure subscribers, or the person who created the search service, can manage the search service in the Azure portal. An Azure subscription requires Contributor or above permissions to create or delete services. This permission level is sufficient for fully managing a search service in the Azure portal.Try other clients for programmatic access. We recommend the quickstarts for first steps:


## Next steps

You can get hands-on experience creating an index using almost any sample or walkthrough for Azure AI Search. For starters, you could choose any of the quickstarts from the table of contents.

But you'll also want to become familiar with methodologies for loading an index with data. Index definition and data import strategies are defined in tandem. The following articles provide more information about creating and loading an index.
