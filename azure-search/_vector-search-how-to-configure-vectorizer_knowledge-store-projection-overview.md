---
merged_at: 2026-01-25T02:11:58.442660
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-how-to-configure-vectorizer.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-configure-vectorizer -->

# Configure a vectorizer in a search index

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, a *vectorizer* is a component that performs vectorization using a deployed embedding model on Azure OpenAI or Azure Vision in Foundry Tools. It converts text (or images) to vectors during query execution.

It's defined in a [search index](search-what-is-an-index), it applies to searchable vector fields, and it's used at query time to generate an embedding for a text or image query input. If instead you need to vectorize content as part of the indexing process, refer to [integrated vectorization](vector-search-integrated-vectorization). For built-in vectorization during indexing, you can configure an indexer and skillset that calls an embedding model for your raw text or image content.

To add a vectorizer to search index, you can use the index designer in Azure portal, or call the [Create or Update Index](/en-us/rest/api/searchservice/indexes/create-or-update) REST API, or use any Azure SDK package that's updated to provide this feature.

Vectorizers are now generally available as long as you use a generally available skill-vectorizer pair. [AzureOpenAIEmbedding vectorizer](vector-search-vectorizer-azure-open-ai) and [AzureOpenAIEmbedding skill](cognitive-search-skill-azure-openai-embedding) are generally available. The custom [Web API vectorizer](/en-us/rest/api/searchservice/indexes/create-or-update#webapivectorizer) is also generally available.

[Azure Vision vectorizer](vector-search-vectorizer-ai-services-vision), [Microsoft Foundry model catalog vectorizer](vector-search-vectorizer-azure-machine-learning-ai-studio-catalog), and their equivalent skills are still in preview. Your skillset must specify [2024-05-01-preview REST API](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2024-05-01-preview&preserve-view=true) to use preview skills and vectorizers.

## Prerequisites

[An index with searchable vector fields](vector-search-how-to-create-index)on Azure AI Search.A deployed embedding model (see the next section).

Permissions to use the embedding model. On Azure OpenAI, the caller must have

[Cognitive Services OpenAI User](/en-us/azure/ai-services/openai/how-to/role-based-access-control#azure-openai-roles)permissions. Or, you can provide an API key.[Visual Studio Code](https://code.visualstudio.com/download)with a[REST client](https://marketplace.visualstudio.com/items?itemName=humao.rest-client)to send the query and accept a response.

We recommend that you [enable diagnostic logging](search-monitor-enable-logging) on your search service to confirm vector query execution.

## Supported embedding models

The following table lists the embedding models that can be used with a vectorizer. Because you must use the [same embedding model for indexing and queries](vector-search-integrated-vectorization#using-integrated-vectorization-in-queries), vectorizers are paired with skills that generate embeddings during indexing. The table lists the skill associated with a particular vectorizer.

| Vectorizer kind | Model names | Model provider | Associated skill |
|---|---|---|---|
`azureOpenAI` |

text-embedding-3

[AzureOpenAIEmbedding skill](cognitive-search-skill-azure-openai-embedding)`aml`

Cohere-embed-v4

1[Microsoft Foundry model catalog](vector-search-integrated-vectorization-ai-studio)[AML skill](cognitive-search-aml-skill)`aiServicesVision`

[Multimodal embeddings 4.0 API](/en-us/azure/ai-services/computer-vision/concept-image-retrieval)[Azure Vision multimodal embeddings skill](cognitive-search-skill-vision-vectorize)`customWebApi`

[Custom Web API skill](cognitive-search-custom-skill-web-api)1 At this time, you can only specify `embed-v-4-0`

programmatically through the [AML skill](cognitive-search-aml-skill) or [Microsoft Foundry model catalog vectorizer](vector-search-vectorizer-azure-machine-learning-ai-studio-catalog), not through the Azure portal. However, you can use the portal to manage the skillset or vectorizer afterward.

## Try a vectorizer with sample data

The [ Import data (new) wizard](search-get-started-portal-import-vectors) reads files from Azure Blob storage, creates an index with chunked and vectorized fields, and adds a vectorizer. By design, the vectorizer that's created by the wizard is set to the same embedding model used to index the blob content.

[Upload sample data files](/en-us/azure/storage/blobs/storage-quickstart-blobs-portal)to a container on Azure Storage. We used some[small text files from NASA's earth book](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/nasa-e-book/earth-txt-10)to test these instructions on a free search service.Run the

, choosing the blob container for the data source.**Import data (new)**wizardChoose an existing deployment of

**text-embedding-ada-002**. This model generates embeddings during indexing and is also used to configure the vectorizer used during queries.After the wizard is finished and all indexer processing is complete, you should have an index with a searchable vector field. The field's JSON definition looks like this:

`{ "name": "vector", "type": "Collection(Edm.Single)", "searchable": true, "retrievable": true, "dimensions": 1536, "vectorSearchProfile": "vector-nasa-ebook-text-profile" }`

You should also have a vector profile and a vectorizer, similar to the following example:

`"profiles": [ { "name": "vector-nasa-ebook-text-profile", "algorithm": "vector-nasa-ebook-text-algorithm", "vectorizer": "vector-nasa-ebook-text-vectorizer" } ], "vectorizers": [ { "name": "vector-nasa-ebook-text-vectorizer", "kind": "azureOpenAI", "azureOpenAIParameters": { "resourceUri": "https://my-fake-azure-openai-resource.openai.azure.com", "deploymentId": "text-embedding-ada-002", "modelName": "text-embedding-ada-002", "apiKey": "0000000000000000000000000000000000000", "authIdentity": null }, "customWebApiParameters": null } ]`

Skip ahead to

[test your vectorizer](#test-a-vectorizer)for text-to-vector conversion during query execution.

## Define a vectorizer and vector profile

This section explains the modifications to an index schema for defining a vectorizer manually.

Use

[Create or Update Index](/en-us/rest/api/searchservice/indexes/create-or-update)to add`vectorizers`

to a search index.Add the following JSON to your index definition. The vectorizers section provides connection information to a deployed embedding model. This step shows two vectorizer examples so that you can compare an Azure OpenAI embedding model and a custom web API side by side.

`"vectorizers": [ { "name": "my_azure_open_ai_vectorizer", "kind": "azureOpenAI", "azureOpenAIParameters": { "resourceUri": "https://url.openai.azure.com", "deploymentId": "text-embedding-ada-002", "modelName": "text-embedding-ada-002", "apiKey": "mytopsecretkey" } }, { "name": "my_custom_vectorizer", "kind": "customWebApi", "customVectorizerParameters": { "uri": "https://my-endpoint", "authResourceId": " ", "authIdentity": " " } } ]`

In the same index, add a vector profiles section that specifies one of your vectorizers. Vector profiles also require a

[vector search algorithm](vector-search-ranking)used to create navigation structures.`"profiles": [ { "name": "my_vector_profile", "algorithm": "my_hnsw_algorithm", "vectorizer":"my_azure_open_ai_vectorizer" } ]`

Assign a vector profile to a vector field. The following example shows a fields collection with the required key field, a title string field, and two vector fields with a vector profile assignment.

`"fields": [ { "name": "ID", "type": "Edm.String", "key": true, "sortable": true, "analyzer": "keyword" }, { "name": "title", "type": "Edm.String" }, { "name": "vector", "type": "Collection(Edm.Single)", "dimensions": 1536, "vectorSearchProfile": "my_vector_profile", "searchable": true, "retrievable": true }, { "name": "my-second-vector", "type": "Collection(Edm.Single)", "dimensions": 1024, "vectorSearchProfile": "my_vector_profile", "searchable": true, "retrievable": true } ]`


## Test a vectorizer

Use a search client to send a query through a vectorizer. This example assumes Visual Studio Code with a REST client and a [sample index](#try-a-vectorizer-with-sample-data).

In Visual Studio Code, provide a search endpoint and

[search query API key](search-security-api-keys#find-existing-keys):`@baseUrl: @queryApiKey: 00000000000000000000000`

Paste in a

[vector query request](vector-search-how-to-query).`### Run a query POST {{baseUrl}}/indexes/vector-nasa-ebook-txt/docs/search?api-version=2025-09-01 HTTP/1.1 Content-Type: application/json api-key: {{queryApiKey}} { "count": true, "select": "title,chunk", "vectorQueries": [ { "kind": "text", "text": "what cloud formations exists in the troposphere", "fields": "vector", "k": 3, "exhaustive": true } ] }`

Key points about the query include:

`"kind": "text"`

tells the search engine that the input is a text string, and to use the vectorizer associated with the search field.`"text": "what cloud formations exists in the troposphere"`

is the text string to vectorize.`"fields": "vector"`

is the name of the field to query over. If you use the sample index produced by the wizard, the generated vector field is named`vector`

.

Send the request. You should get three

`k`

results, where the first result is the most relevant.

Notice that there are no vectorizer properties to set at query time. The query reads the vectorizer properties, as per the vector profile field assignment in the index.

## Check logs

If you enabled diagnostic logging for your search service, run a Kusto query to confirm query execution on your vector field:

```
OperationEvent
| where TIMESTAMP > ago(30m)
| where Name == "Query.Search" and AdditionalInfo["QueryMetadata"]["Vectors"] has "TextLength"
```


## Best practices

If you're setting up an Azure OpenAI vectorizer, consider the same [best practices](cognitive-search-skill-azure-openai-embedding#best-practices) that we recommend for the Azure OpenAI embedding skill.


---

<!-- DOCUMENTO FUSIONADO: knowledge-store-projection-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/knowledge-store-projection-overview -->

# Knowledge store "projections" in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

*Knowledge stores* are secondary storage that exists in Azure Storage and contain the outputs of Azure AI Search skillsets. They're separate from knowledge sources and knowledge bases, which are used in [agentic retrieval](agentic-retrieval-overview) workflows.

Projections define the physical tables, objects, and files in a [ knowledge store](knowledge-store-concept-intro) that accept content from an Azure AI Search enrichment pipeline. If you're creating a knowledge store, defining and shaping projections is most of the work.

This article introduces projection concepts and workflow so that you have some background before you start coding.

Projections are defined in Azure AI Search skillsets, but the end results are the table, object, and image file projections in Azure Storage.


## Types of projections and usage

A knowledge store is a logical construction that's physically expressed as a loose collection of tables, JSON objects, or binary image files in Azure Storage.

| Projection | Storage | Usage |
|---|---|---|
|

[Shaper skill or use inline shaping](knowledge-store-projection-shape)to specify columns and rows. You can organize content into multiple tables based on familiar normalization principles. Tables that are in the same group are automatically related.[Objects](knowledge-store-projections-examples#define-an-object-projection)[Files](knowledge-store-projections-examples#define-a-file-projection)## Projection definition

Projections are specified under the "knowledgeStore" property of a [skillset](/en-us/rest/api/searchservice/skillsets/create). Projection definitions are used during indexer invocation to create and load objects in Azure Storage with enriched content. If you're unfamiliar with these concepts, start with [AI enrichment](cognitive-search-concept-intro) for an introduction.

The following example illustrates the placement of projections under knowledgeStore, and the basic construction. The name, type, and content source make up a projection definition.

```
"knowledgeStore" : {
"storageConnectionString": "DefaultEndpointsProtocol=https;AccountName=<Acct Name>;AccountKey=<Acct Key>;",
"projections": [
{
"tables": [
{ "tableName": "ks-museums-main", "generatedKeyName": "ID", "source": "/document/tableprojection" },
{ "tableName": "ks-museumEntities", "generatedKeyName": "ID","source": "/document/tableprojection/Entities/*" }
],
"objects": [
{ "storageContainer": "ks-museums", "generatedKeyName": "ID", "source": "/document/objectprojection" }
],
"files": [ ]
}
]
```


## Projection groups

Projections are an array of complex collections, which means that you can specify multiple sets of each type. It's common to use just one projection group, but you might use multiple if storage requirements include supporting different tools and scenarios. For example, you might use one group for design and debug of a skillset, while a second set collects output used for an online app, with a third for data science workloads.

The same skillset output is used to populate all groups under projections. The following example shows two.

```
"knowledgeStore" : {
"storageConnectionString": "DefaultEndpointsProtocol=https;AccountName=<Acct Name>;AccountKey=<Acct Key>;",
"projections": [
{
"tables": [],
"objects": [],
"files": []
},
{
"tables": [],
"objects": [],
"files": []
}
]
}
```


Projection groups have the following key characteristics of mutual exclusivity and relatedness.

| Principle | Description |
|---|---|
| Mutual exclusivity | Each group is fully isolated from other groups to support different data shaping scenarios. For example, if you're testing different table structures and combinations, you would put each set in a different projection group for AB testing. Each group obtains data from the same source (enrichment tree) but is fully isolated from the table-object-file combination of any peer projection groups. |
| Relatedness | Within a projection group, content in tables, objects, and files are related. Knowledge store uses generated keys as reference points to a common parent node. For example, consider a scenario where you have a document containing images and text. You could project the text to tables and the images to binary files, and both tables and objects have a column/property containing the file URL. |

## Projection "source"

The source parameter is the third component of a projection definition. Because projections store data from an AI enrichment pipeline, the source of a projection is always the output of a skill. As such, output might be a single field (for example, a field of translated text), but often it's a reference to a data shape.

Data shapes come from your skillset. Among all of the built-in skills provided in Azure AI Search, there's a utility skill called the [ Shaper skill](cognitive-search-skill-shaper) that's used to create data shapes. You can include Shaper skills (as many as you need) to support the projections in the knowledge store.

Shapes are frequently used with table projections, where the shape not only specifies which rows go into the table, but also which columns are created (you can also pass a shape to an object projection).

Shapes can be complex and it's out of scope to discuss them in depth here, but the following example briefly illustrates a basic shape. The output of the Shaper skill is specified as the source of a table projection. Within the table projection itself will be columns for "metadata-storage_path", "reviews_text", "reviews_title", and so forth, as specified in the shape.

```
{
"@odata.type": "#Microsoft.Skills.Util.ShaperSkill",
"name": "ShaperForTables",
"description": null,
"context": "/document",
"inputs": [
{
"name": "metadata_storage_path",
"source": "/document/metadata_storage_path",
"sourceContext": null,
"inputs": []
},
{
"name": "reviews_text",
"source": "/document/reviews_text"
},
{
"name": "reviews_title",
"source": "/document/reviews_title"
},
{
"name": "reviews_username",
"source": "/document/reviews_username"
},
],
"outputs": [
{
"name": "output",
"targetName": "mytableprojection"
}
]
}
```


## Projection lifecycle

Projections have a lifecycle that is tied to the source data in your data source. As source data is updated and reindexed, projections are updated with the results of the enrichments, ensuring your projections are eventually consistent with the data in your data source. However, projections are also independently stored in Azure Storage. They won't be deleted when the indexer or the search service itself is deleted.

## Consume in apps

After the indexer is run, connect to projections and consume the data in other apps and workloads.

Use Azure portal to verify object creation and content in Azure Storage.

Use

[Power BI for data exploration](knowledge-store-connect-power-bi). This tool works best when the data is in Azure Table Storage. Within Power BI, you can manipulate data into new tables that are easier to query and analyze.Use enriched data in blob container in a data science pipeline. For example, you can

[load the data from blobs into a Pandas DataFrame](/en-us/azure/architecture/data-science-process/explore-data-blob).Finally, if you need to export your data from the knowledge store, Azure Data Factory has connectors to export the data and land it in the database of your choice.


## Checklist for getting started

Recall that projections are exclusive to knowledge stores, and aren't used to structure a search index.

In Azure Storage, get a connection string from

**Access Keys**and verify the account is StorageV2 (general purpose V2).While in Azure Storage, familiarize yourself with existing content in containers and tables so that you choose nonconflicting names for the projections. A knowledge store is a loose collection of tables and containers. Consider adopting a naming convention to keep track of related objects.

In Azure AI Search,

[enable enrichment caching (preview)](enrichment-cache-how-to-configure)in the indexer and then[run the indexer](search-howto-run-reset-indexers)to execute the skillset and populate the cache. This is a preview feature, so be sure to use the preview REST API on the indexer request. Once the cache is populated, you can modify projection definitions in a knowledge store free of charge (as long as the skills themselves aren't modified).In your code, all projections are defined solely in a skillset. There are no indexer properties (such as field mappings or output field mappings) that apply to projections. Within a skillset definition, you'll focus on two areas: knowledgeStore property and skills array.

Under knowledgeStore, specify table, object, file projections in the

`projections`

section. Object type, object name, and quantity (per the number of projections you define) are determined in this section.From the skills array, determine which skill outputs should be referenced in the

`source`

of each projection. All projections have a source. The source can be the output of an upstream skill, but is often the output of a Shaper skill. The composition of your projection is determined through shapes.

If you're adding projections to an existing skillset,

[update the skillset](/en-us/rest/api/searchservice/skillsets/create-or-update)and[run the indexer](/en-us/rest/api/searchservice/indexers/run).Check your results in Azure Storage. On subsequent runs, avoid naming collisions by deleting objects in Azure Storage or changing project names in the skillset.

If you're using

[Table projections](knowledge-store-projections-examples#define-a-table-projection)check[Understanding the Table Service data model](/en-us/rest/api/storageservices/Understanding-the-Table-Service-Data-Model)and[Scalability and performance targets for Table storage](/en-us/azure/storage/tables/scalability-targets)to make sure your data requirements are within Table storage documented limits.

## Next steps

Review syntax and examples for each projection type.
