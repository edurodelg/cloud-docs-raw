---
merged_at: 2026-01-25T02:11:58.384921
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: semantic-how-to-configure.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/semantic-how-to-configure -->

# Configure semantic ranker and return captions in search results

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Semantic ranking iterates over an initial result set, applying an L2 ranking methodology that promotes the most semantically relevant results to the top of the stack. You can also get semantic captions, with highlights over the most relevant terms and phrases, and [semantic answers](semantic-answers).

This article explains how to configure a search index for semantic reranking.

Note

If you have existing code that calls preview or previous API versions, see [Migrate semantic ranking code](semantic-code-migration) for help with modifying your code.

## Prerequisites

Azure AI Search in any

[region that provides semantic ranking](search-region-support).Semantic ranker

[enabled on your search service](semantic-how-to-enable-disable).An existing search index with rich text content. Semantic ranking applies to strings (nonvector) fields and works best on content that is informational or descriptive.


## Choose a client

You can specify a semantic configuration on new or existing indexes, using any of the following tools and software development kits (SDKs) to add a semantic configuration:

[Azure portal](https://portal.azure.com), using the index designer to add a semantic configuration.[Visual Studio Code](https://code.visualstudio.com/download)with the[REST client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)and a[Create or Update Index (REST) API](/en-us/rest/api/searchservice/indexes/create-or-update).[Azure SDK for .NET](https://www.nuget.org/packages/Azure.Search.Documents)[Azure SDK for Python](https://pypi.org/project/azure-search-documents)[Azure SDK for Java](https://central.sonatype.com/artifact/com.azure/azure-search-documents)[Azure SDK for JavaScript](https://www.npmjs.com/package/@azure/search-documents)

## Add a semantic configuration

Some workloads create a semantic configuration automatically. If you're using [agentic retrieval](agentic-retrieval-overview) and a [knowledge source that indexes content](agentic-knowledge-source-overview#supported-knowledge-sources) on Azure AI Search, your generated index already has a semantic configuration that works for your content.

For other workloads, you can set up a semantic configuration yourself. A *semantic configuration* is a section in your index that establishes the field inputs used for semantic ranking. You can add or update a semantic configuration at any time, no rebuild necessary. If you create multiple configurations, you can specify a default. At query time, specify a semantic configuration on a [query request](semantic-how-to-query-request), or leave it blank to use the default.

You can create up to 100 semantic configurations in a single index.

A semantic configuration has a name and the following properties:

| Property | Characteristics |
|---|---|
| Title field | A short string, ideally under 25 words. This field could be the title of a document, name of a product, or a unique identifier. If you don't have suitable field, leave it blank. |
| Content fields | Longer chunks of text in natural language form, subject to
|

You can only specify one title field, but you can have as many content and keyword fields as you like. For content and keyword fields, list the fields in priority order because lower priority fields might get truncated.

Across all semantic configuration properties, the fields you assign must be:

- Attributed as
`searchable`

and`retrievable`

- Strings of type
`Edm.String`

,`Collection(Edm.String)`

, string subfields of`Edm.ComplexType`


Sign in to the

[Azure portal](https://portal.azure.com)and navigate to a search service that has[semantic ranking enabled](semantic-how-to-enable-disable).From

**Indexes**on the left-navigation pane, select an index.Select

**Semantic configurations**and then select**Add semantic configuration**.On the

**New semantic configuration**page, enter a semantic configuration name and select the fields to use in the semantic configuration. Only searchable and retrievable string fields are eligible. Make sure to list content fields and keyword fields in priority order.Select

**Save**to save the configuration settings.Select

**Save**again on the index page to save the semantic configuration in the index.

## Opt in for prerelease semantic ranking models

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Using [previewREST APIs](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true) and preview Azure SDKs that provide the property, you can optionally configure an index to use prerelease semantic ranking models if one is deployed in your region. There's no mechanism for knowing if a prerelease is available, or if it was used on specific query. For this reason, we recommend that you use this property in test environments, and only if you're interested in trying out the very latest semantic ranking models.

The configuration property is `"flightingOptIn": true`

, and it's set in the semantic configuration section of an index. The property is null or false by default. You can set it true on a create or update request at any time, and it affects semantic queries moving forward, assuming the query stipulates a semantic configuration that includes the property.

```
PUT https://myservice.search.windows.net/indexes('hotels')?allowIndexDowntime=False&api-version=2025-11-01-preview
{
"name": "hotels",
"fields": [ ],
"scoringProfiles": [ ],
"defaultScoringProfile": "geo",
"suggesters": [ ],
"analyzers": [ ],
"corsOptions": { },
"encryptionKey": { },
"similarity": { },
"semantic": {
"configurations": [
{
"name": "semanticHotels",
"prioritizedFields": {
"titleField": {
"fieldName": "hotelName"
},
"prioritizedContentFields": [
{
"fieldName": "description"
},
{
"fieldName": "description_fr"
}
],
"prioritizedKeywordsFields": [
{
"fieldName": "tags"
},
{
"fieldName": "category"
}
],
"flightingOptIn": true
}
}
]
},
"vectorSearch": { }
}
```


## Next steps

Test your semantic configuration by running a semantic query.


---

<!-- DOCUMENTO FUSIONADO: vector-search-how-to-generate-embeddings.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-generate-embeddings -->

# Generate embeddings for search queries and documents

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search doesn't host embedding models, so you're responsible for creating vectors for query inputs and outputs. Choose one of the following approaches:

| Approach | Description |
|---|---|
|

[push prevectorized documents](vector-search-how-to-create-index#load-vector-data-for-indexing)into vector fields in a search index. For querying, you[provide precomputed vectors](#generate-an-embedding-for-an-improvised-query)to the search engine. For demos of this approach, see the[azure-search-vector-samples](https://github.com/Azure/azure-search-vector-samples/tree/main)GitHub repository.We recommend integrated vectorization for most scenarios. Although you can use any supported embedding model, this article uses Azure OpenAI models for illustration.

## How embedding models are used in vector queries

Embedding models generate vectors for both query inputs and query outputs. Query inputs include:

**Text or images that are converted to vectors during query processing**. As part of integrated vectorization, a[vectorizer](vector-search-how-to-configure-vectorizer)performs this task.**Precomputed vectors**. You can generate these vectors by passing the query input to an embedding model of your choice. To avoid[rate limiting](/en-us/azure/ai-services/openai/quotas-limits), implement retry logic in your workload. Our[Python demo](https://github.com/Azure/azure-search-vector-samples/tree/93c839591bf92c2f10001d287871497b0f204a7c/demo-python)uses[tenacity](https://pypi.org/project/tenacity/).

Based on the query input, the search engine retrieves matching documents from your search index. These documents are the query outputs.

Your search index must already contain documents with one or more vector fields populated by embeddings. You can create these embeddings through integrated or manual vectorization. To ensure accurate results, use the same embedding model for indexing and querying.

## Tips for embedding model integration

**Identify use cases**. Evaluate specific use cases where embedding model integration for vector search features adds value to your search solution. Examples include[multimodal search](multimodal-search-overview)or matching image content with text content, multilingual search, and similarity search.**Design a chunking strategy**. Embedding models have limits on the number of tokens they accept, so[data chunking](vector-search-how-to-chunk-documents)is necessary for large files.**Optimize cost and performance**. Vector search is resource intensive and subject to maximum limits, so vectorize only the fields that contain semantic meaning.[Reduce vector size](vector-search-how-to-configure-compression-storage)to store more vectors for the same price.**Choose the right embedding model**. Select a model for your use case, such as word embeddings for text-based searches or image embeddings for visual searches. Consider pretrained models, such as text-embedding-ada-002 from OpenAI or the Image Retrieval REST API from[Azure Vision in Foundry Tools](/en-us/azure/ai-services/computer-vision/how-to/image-retrieval).**Normalize vector lengths**. To improve the accuracy and performance of similarity search, normalize vector lengths before you store them in a search index. Most pretrained models are already normalized.**Fine-tune the model**. If needed, fine-tune the model on your domain-specific data to improve its performance and relevance to your search application.**Test and iterate**. Continuously test and refine the embedding model integration to achieve your desired search performance and user satisfaction.

## Create resources in the same region

Although integrated vectorization with Azure OpenAI embedding models doesn't require resources to be in the same region, using the same region can improve performance and reduce latency.

To use the same region for your resources:

Check the

[regional availability of Azure AI Search](search-region-support).Create an Azure OpenAI resource and Azure AI Search service in the same region.


Tip

Want to use [semantic ranking](semantic-how-to-query-request) for [hybrid queries](hybrid-search-overview) or a machine learning model in a [custom skill](cognitive-search-custom-skill-interface) for [AI enrichment](cognitive-search-concept-intro)? Choose an Azure AI Search region that provides those features.

## Choose an embedding model in Foundry

When you add knowledge to an agent workflow in the [Foundry portal](https://ai.azure.com/?cid=learnDocs), you have the option of creating a search index. A wizard guides you through the steps.

One step involves selecting an embedding model to vectorize your plain text content. The following models are supported:

- text-embedding-3-small
- text-embedding-3-large
- text-embedding-ada-002
- Cohere-embed-v3-english
- Cohere-embed-v3-multilingual

Your model must already be deployed, and you must have permission to access it. For more information, see [Deployment overview for Foundry Models](/en-us/azure/ai-foundry/concepts/deployments-overview).

## Generate an embedding for an improvised query

If you don't want to use integrated vectorization, you can manually generate an embedding and paste it into the `vectorQueries.vector`

property of a vector query. For more information, see [Create a vector query in Azure AI Search](vector-search-how-to-query).

The following examples assume the text-embedding-ada-002 model. Replace `YOUR-API-KEY`

and `YOUR-OPENAI-RESOURCE`

with your Azure OpenAI resource details.

```
using System;
using System.Net.Http;
using System.Text;
using System.Threading.Tasks;
using Newtonsoft.Json;
class Program
{
static async Task Main(string[] args)
{
var apiKey = "YOUR-API-KEY";
var apiBase = "https://YOUR-OPENAI-RESOURCE.openai.azure.com";
var apiVersion = "2024-02-01";
var engine = "text-embedding-ada-002";
var client = new HttpClient();
client.DefaultRequestHeaders.Add("Authorization", $"Bearer {apiKey}");
var requestBody = new
{
input = "How do I use C# in VS Code?"
};
var response = await client.PostAsync(
$"{apiBase}/openai/deployments/{engine}/embeddings?api-version={apiVersion}",
new StringContent(JsonConvert.SerializeObject(requestBody), Encoding.UTF8, "application/json")
);
var responseBody = await response.Content.ReadAsStringAsync();
Console.WriteLine(responseBody);
}
}
```


The output is a vector array of 1,536 dimensions.
