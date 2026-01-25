---
source_url: https://learn.microsoft.com/en-us/azure/search/search-get-started-portal-import-vectors
fetched_at: 2026-01-25T02:04:28.198687
---

# Quickstart: Vector search in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use the **Import data (new)** wizard in the Azure portal to get started with [integrated vectorization](vector-search-integrated-vectorization). The wizard chunks your content and calls an embedding model to vectorize the chunks at indexing and query time.

This quickstart uses text-based PDFs and simple images from the [azure-search-sample-data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/sustainable-ai-pdf) repo. However, you can use different files and still complete this quickstart.

Tip

Have image-rich documents? See [Quickstart: Multimodal search in the Azure portal](search-get-started-portal-image-search) to extract, store, and search images alongside text.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An

[Azure AI Search service](search-create-service-portal). We recommend the Basic tier or higher.Familiarity with the wizard. See

[Import data wizards in the Azure portal](search-import-data-portal).

### Supported data sources

The wizard [supports several Azure data sources](search-import-data-portal#supported-data-sources-and-scenarios). However, this quickstart only covers the data sources that work with whole files, which are described in the following table.

| Supported data source | Description |
|---|---|
|

[Azure Data Lake Storage (ADLS) Gen2](/en-us/azure/storage/blobs/create-data-lake-storage-account)**Properties**tab on the**Overview**page.[Microsoft OneLake](search-how-to-index-onelake-files)### Supported embedding models

The portal supports the following embedding models for integrated vectorization. Deployment instructions are provided in a [later section](#prepare-embedding-model).

| Provider | Supported models |
|---|---|
1 |

[Azure Vision multimodal](/en-us/azure/ai-services/computer-vision/how-to/image-retrieval)[Microsoft Foundry hub-based project](/en-us/azure/ai-foundry/how-to/hub-create-projects)- text-embedding-ada-002
- text-embedding-3-small
- text-embedding-3-large

- Cohere-embed-v3-english
2 - Cohere-embed-v3-multilingual
2

[Microsoft Foundry project](/en-us/azure/ai-foundry/how-to/create-projects)- text-embedding-ada-002
- text-embedding-3-small
- text-embedding-3-large

[Azure OpenAI resource](/en-us/azure/ai-services/openai/how-to/create-resource)3, 4- text-embedding-ada-002
- text-embedding-3-small
- text-embedding-3-large

1 For billing purposes, you must [attach your multi-service account](cognitive-search-attach-cognitive-services) to your Azure AI Search skillset. Currently, the wizard requires your search service and multi-service account to be in the [same supported region for the Azure Vision multimodal embeddings skill](cognitive-search-skill-vision-vectorize#supported-regions), even when using keyless connections.

2 To use this model in the wizard, you must provision it as a serverless API deployment. You can use an [ARM/Bicep template](https://github.com/Azure-Samples/azure-ai-search-multimodal-sample/blob/42b4d07f2dd9f7720fdc0b0788bf107bdac5eecb/infra/ai/modules/project.bicep#L37C1-L38C1) for this task.

3 The endpoint of your Azure OpenAI resource must have a [custom subdomain](/en-us/azure/ai-services/cognitive-services-custom-subdomains), such as `https://my-unique-name.openai.azure.com`

. If you created your resource in the [Azure portal](https://portal.azure.com/), this subdomain was automatically generated during resource setup.

4 Azure OpenAI resources (with access to embedding models) that were created in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs) aren't supported. You must create an Azure OpenAI resource in the Azure portal.

### Public endpoint requirements

For this quickstart, all of the preceding resources must have public access enabled so that the Azure portal nodes can access them. Otherwise, the wizard fails. After the wizard runs, you can enable firewalls and private endpoints on the integration components for security. For more information, see [Secure connections in the import wizards](search-import-data-portal#secure-connections).

If private endpoints are already present and you can't disable them, the alternative option is to run the respective end-to-end flow from a script or program on a virtual machine. The virtual machine must be on the same virtual network as the private endpoint. Here's a [Python code sample](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-python/code/integrated-vectorization) for integrated vectorization. The same [GitHub repo](https://github.com/Azure/azure-search-vector-samples/tree/main) has samples in other programming languages.

### Role-based access

You can use Microsoft Entra ID with role assignments or key-based authentication with full-access connection strings. For Azure AI Search connections to other resources, we recommend role assignments. This quickstart assumes roles.

Free search services support role-based connections to Azure AI Search. However, they don't support managed identities on outbound connections to Azure Storage or Azure Vision. This lack of support requires key-based authentication on connections between free search services and other Azure resources. For more secure connections, use the Basic tier or higher, and then enable roles and configure a managed identity.

To configure the recommended role-based access:

On your search service,

[enable roles](search-security-enable-roles)and[configure a system-assigned managed identity](search-how-to-managed-identities#create-a-system-managed-identity).[Assign the following roles](search-security-rbac)to yourself.**Search Service Contributor****Search Index Data Contributor****Search Index Data Reader**

On your data source and embedding model provider, create role assignments that allow your search service to access data and models. See

[Prepare sample data](#prepare-sample-data)and[Prepare embedding models](#prepare-embedding-model).

Note

If you can't progress through the wizard because options aren't available (for example, you can't select a data source or an embedding model), revisit the role assignments. Error messages indicate that models or deployments don't exist, when the real cause is that the search service doesn't have permission to access them.

### Check for space

If you're starting with the free service, you're limited to three indexes, data sources, skillsets, and indexers. Basic limits you to 15. This quickstart creates one of each object, so make sure you have room for extra items before you begin.

## Prepare sample data

In this section, you use a [supported data source](#supported-data-sources) to prepare sample data. Before you proceed, make sure you completed the prerequisites for [role-based access](#role-based-access).

Sign in to the

[Azure portal](https://portal.azure.com/)and select your Azure Storage account.From the left pane, select

**Data storage**>**Containers**.Create a container, and then upload the

[health-plan PDF documents](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/health-plan)used for this quickstart.To assign roles:

From the left pane, select

**Access Control (IAM)**.Select

**Add**>**Add role assignment**.Under

**Job function roles**, select**Storage Blob Data Reader**, and then select**Next**.Under

**Members**, select**Managed identity**, and then select**Select members**.Select your subscription and the managed identity of your search service.


(Optional) Synchronize deletions in your container with deletions in the search index. To configure your indexer for deletion detection:

[Enable soft delete](/en-us/azure/storage/blobs/soft-delete-blob-enable?tabs=azure-portal#enable-blob-soft-delete-hierarchical-namespace)on your storage account. If you're using[native soft delete](search-how-to-index-azure-blob-changed-deleted#native-blob-soft-delete), the next step isn't required.[Add custom metadata](search-how-to-index-azure-blob-changed-deleted#soft-delete-strategy-using-custom-metadata)that an indexer can scan to determine which blobs are marked for deletion. Give your custom property a descriptive name. For example, you can name the property "IsDeleted" and set it to false. Repeat this step for every blob in the container. When you want to delete the blob, change the property to true. For more information, see[Change and delete detection when indexing from Azure Storage](search-how-to-index-azure-blob-changed-deleted).


## Prepare embedding model

In this section, you deploy a [supported embedding model](#supported-embedding-models) for later use in this quickstart. Before you proceed, make sure you completed the prerequisites for [role-based access](#role-based-access).

The wizard supports several embedding models. Internally, the wizard calls the [Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding) to connect to Azure OpenAI.

To assign roles:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your Azure OpenAI resource.From the left pane, select

**Access control (IAM)**.Select

**Add**>**Add role assignment**.Under

**Job function roles**, select**Cognitive Services OpenAI User**, and then select**Next**.Under

**Members**, select**Managed identity**, and then select**Select members**.Select your subscription and the managed identity of your search service.


To deploy an embedding model:

Sign in to the

[Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs)and select your Azure OpenAI resource.Deploy a

[supported embedding model](#supported-embedding-models).


## Start the wizard

To start the wizard for vector search:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your Azure AI Search service.On the

**Overview**page, select**Import data (new)**.Select your data source:

**Azure Blob Storage**,**ADLS Gen2**, or**OneLake**.Select

**RAG**.

## Run the wizard

The wizard walks you through several configuration steps. This section covers each step in sequence.

### Connect to your data

In this step, you connect Azure AI Search to your chosen [data source](#supported-data-sources) for content ingestion and indexing.

On the

**Connect to your data**page, select your Azure subscription.Select the storage account and container that provide the sample data.

If you enabled soft delete and added custom metadata in

[Prepare sample data](#prepare-sample-data), select the**Enable deletion tracking**checkbox.On subsequent indexing runs, the search index is updated to remove any search documents based on soft-deleted blobs on Azure Storage.

Blobs support either

**Native blob soft delete**or**Soft delete using custom metadata**.If you configured your blobs for soft delete, provide the metadata property name-value pair. We recommend

**IsDeleted**. If**IsDeleted**is set to**true**on a blob, the indexer drops the corresponding search document on the next indexer run.The wizard doesn't check Azure Storage for valid settings or throw an error if the requirements aren't met. Instead, deletion detection doesn't work, and your search index is likely to collect orphaned documents over time.


Select the

**Authenticate using managed identity**checkbox. Leave the identity type as**System-assigned**.Select

**Next**.

### Vectorize your text

During this step, the wizard uses your chosen [embedding model](#supported-embedding-models) to vectorize chunked data. Chunking is built in and nonconfigurable. The effective settings are:

```
"textSplitMode": "pages",
"maximumPageLength": 2000,
"pageOverlapLength": 500,
"maximumPagesToTake": 0, #unlimited
"unit": "characters"
```


On the

**Vectorize your text**page, select**Azure OpenAI**for the kind.Select your Azure subscription.

Select your Azure OpenAI resource, and then select the model you deployed in

[Prepare embedding model](#prepare-embedding-model).For the authentication type, select

**System assigned identity**.Select the checkbox that acknowledges the billing effects of using these resources.

Select

**Next**.

### Vectorize and enrich your images

The health-plan PDFs include a corporate logo, but otherwise, there are no images. You can skip this step if you're using the sample documents.

However, if your content includes useful images, you can apply AI in one or both of the following ways:

Use a supported image embedding model from the Microsoft Foundry model catalog or the Azure Vision multimodal embeddings API (via a multi-service account) to vectorize images.

Use optical character recognition (OCR) to extract text from images. This option invokes the

[OCR skill](cognitive-search-skill-ocr).

On the

**Vectorize and enrich your images**page, select the**Vectorize images**checkbox.For the kind, select your model provider:

**Azure AI Foundry**or**AI Vision vectorization**.Select your Azure subscription, resource, and embedding model deployment (if applicable).

For the authentication type, select

**System assigned identity**if you're not using a hub-based project. Otherwise, leave it as**API key**.Select the checkbox that acknowledges the billing effects of using these resources.

Select

**Next**.

### Add semantic ranking

On the **Advanced settings** page, you can optionally add [semantic ranking](semantic-search-overview) to rerank results at the end of query execution. Reranking promotes the most semantically relevant matches to the top.

### Map new fields

On the **Advanced settings** page, you can optionally add new fields, assuming the data source provides metadata or fields that aren't picked up on the first pass. By default, the wizard generates the fields described in the following table.

| Field | Applies to | Description |
|---|---|---|
| chunk_id | Text and image vectors | Generated string field. Searchable, retrievable, and sortable. This is the document key for the index. |
| parent_id | Text vectors | Generated string field. Retrievable and filterable. Identifies the parent document from which the chunk originates. |
| chunk | Text and image vectors | String field. Human readable version of the data chunk. Searchable and retrievable, but not filterable, facetable, or sortable. |
| title | Text and image vectors | String field. Human readable document title or page title or page number. Searchable and retrievable, but not filterable, facetable, or sortable. |
| text_vector | Text vectors | Collection(Edm.single). Vector representation of the chunk. Searchable and retrievable, but not filterable, facetable, or sortable. |

You can't modify the generated fields or their attributes, but you can add new fields if your data source provides them. For example, Azure Blob Storage provides a collection of metadata fields.

To add fields to the index schema:

On the

**Advanced settings**page, under**Index fields**, select**Preview and edit**.Select

**Add field**.Select a source field from the available fields, enter a field name for the index, and accept (or override) the default data type.

If you want to restore the schema to its original version, select

**Reset**.

Key points about this step:

The index schema provides vector and nonvector fields for chunked data.

Document parsing mode creates chunks (one search document per chunk).


### Schedule indexing

For data sources where the underlying data is volatile, you can [schedule indexing](search-howto-schedule-indexers) to capture changes at specific intervals or specific dates and times.

To schedule indexing:

On the

**Advanced settings**page, under**Schedule indexing**, specify a run schedule for the indexer. We recommend**Once**for this quickstart.Select

**Next**.

## Finish the wizard

The final step is to review your configuration and create the necessary objects for vector search. If necessary, return to the previous pages in the wizard to adjust your configuration.

To finish the wizard:

On the

**Review your configuration**page, specify a prefix for the objects that the wizard creates. A common prefix helps you stay organized.Select

**Create**.

When the wizard completes the configuration, it creates the following objects:

A data source connection.

An index with vector fields, vectorizers, vector profiles, and vector algorithms. You can't design or modify the default index during the wizard workflow. Indexes conform to the

[2024-05-01-preview REST API](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2024-05-01-preview&preserve-view=true).A skillset with the

[Text Split skill](cognitive-search-skill-textsplit)for chunking and an embedding skill for vectorization. The embedding skill is either the[Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding),[AML skill](cognitive-search-aml-skill), or[Azure Vision multimodal embeddings skill](cognitive-search-skill-vision-vectorize). The skillset also has the[index projections](index-projections-concept-intro)configuration, which maps data from one document in the data source to its corresponding chunks in a "child" index.An indexer with field mappings and output field mappings (if applicable).


Tip

Wizard-created objects have configurable JSON definitions. To view or modify these definitions, select **Search management** from the left pane, where you can view your indexes, indexers, data sources, and skillsets.

## Check results

Search Explorer accepts text strings as input and then vectorizes the text for vector query execution.

To query your vector index:

In the Azure portal, go to

**Search Management**>**Indexes**, and then select your index.Select

**Query options**, and then select**Hide vector values in search results**. This step makes the results more readable.From the

**View**menu, select**JSON view**so you can enter text for your vector query in the`text`

vector query parameter.The default query is an empty search (

`"*"`

) but includes parameters for returning the number matches. It's a hybrid query that runs text and vector queries in parallel. It also includes semantic ranking and specifies which fields to return in the results through the`select`

statement.`{ "search": "*", "count": true, "vectorQueries": [ { "kind": "text", "text": "*", "fields": "text_vector,image_vector" } ], "queryType": "semantic", "semanticConfiguration": "my-demo-semantic-configuration", "captions": "extractive", "answers": "extractive|count-3", "queryLanguage": "en-us", "select": "chunk_id,text_parent_id,chunk,title,image_parent_id" }`

Replace both asterisk (

`*`

) placeholders with a question related to health plans, such as`Which plan has the lowest deductible?`

.`{ "search": "Which plan has the lowest deductible?", "count": true, "vectorQueries": [ { "kind": "text", "text": "Which plan has the lowest deductible?", "fields": "text_vector,image_vector" } ], "queryType": "semantic", "semanticConfiguration": "my-demo-semantic-configuration", "captions": "extractive", "answers": "extractive|count-3", "queryLanguage": "en-us", "select": "chunk_id,text_parent_id,chunk,title" }`

To run the query, select

**Search**.Each document is a chunk of the original PDF. The

`title`

field shows which PDF the chunk comes from. Each`chunk`

is long. You can copy and paste one into a text editor to read the entire value.To see all of the chunks from a specific document, add a filter for the

`title_parent_id`

field for a specific PDF. You can check the**Fields**tab of your index to confirm the field is filterable.`{ "select": "chunk_id,text_parent_id,chunk,title", "filter": "text_parent_id eq 'aHR0cHM6Ly9oZWlkaXN0c3RvcmFnZWRlbW9lYXN0dXMuYmxvYi5jb3JlLndpbmRvd3MubmV0L2hlYWx0aC1wbGFuLXBkZnMvTm9ydGh3aW5kX1N0YW5kYXJkX0JlbmVmaXRzX0RldGFpbHMucGRm0'", "count": true, "vectorQueries": [ { "kind": "text", "text": "*", "k": 5, "fields": "text_vector" } ] }`


## Clean up resources

This quickstart uses billable Azure resources. If you no longer need the resources, delete them from your subscription to avoid charges.

## Next step

This quickstart introduced you to the **Import data (new)** wizard, which creates all of the necessary objects for integrated vectorization. To explore each step in detail, see [Set up integrated vectorization in Azure AI Search](search-how-to-integrated-vectorization).