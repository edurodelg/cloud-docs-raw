---
source_url: https://learn.microsoft.com/en-us/azure/search/search-get-started-portal-image-search
fetched_at: 2026-01-25T03:13:34.802236
---

# Quickstart: Multimodal search in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use the **Import data (new)** wizard in the Azure portal to get started with [multimodal search](multimodal-search-overview). The wizard simplifies the process of extracting, chunking, vectorizing, and loading both text and images into a searchable index.

This quickstart uses a multimodal PDF from the [azure-search-sample-data](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/sustainable-ai-pdf) repo. However, you can use different files and still complete this quickstart.

Tip

Have text-heavy documents? See [Quickstart: Vector search in the Azure portal](search-get-started-portal-import-vectors) to chunk and vectorize content with optional image support.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An

[Azure AI Search service](search-create-service-portal). We recommend the Basic tier or higher.An

[Azure Storage account](/en-us/azure/storage/common/storage-account-create). Use Azure Blob Storage or Azure Data Lake Storage Gen2 (storage account with a hierarchical namespace) on a standard performance (general-purpose v2) account. Access tiers can be hot, cool, or cold.Familiarity with the wizard. See

[Import data wizards in the Azure portal](search-import-data-portal).

### Supported extraction methods

For content extraction, choose either default extraction via Azure AI Search or enhanced extraction via [Azure Document Intelligence in Foundry Tools](/en-us/azure/ai-services/document-intelligence/overview).

| Method | Description |
|---|---|
| Default extraction | Extracts location metadata from PDF images only. Doesn't require another Azure resource. |
| Enhanced extraction | Extracts location metadata from text and images for multiple document types. Requires an
1 for integration. |

1 For billing purposes, you must [attach your multi-service account](cognitive-search-attach-cognitive-services) to your Azure AI Search skillset. Currently, the wizard requires your search service and multi-service account to be in the [same supported region for the Document Layout skill](cognitive-search-skill-document-intelligence-layout#supported-regions), even when using keyless connections.

### Supported embedding methods

For content embedding, choose one of the following methods:

**Image verbalization:**Uses an LLM to generate natural-language descriptions of images, and then uses an embedding model to vectorize plain text and verbalized images.**Multimodal embeddings:**Uses an embedding model to directly vectorize both text and images.

The portal supports the following models for each method. Deployment instructions are provided in a [later section](#deploy-models).

| Provider | Models for image verbalization | Models for multimodal embeddings |
|---|---|---|
1 |

[Azure Vision multimodal](/en-us/azure/ai-services/computer-vision/how-to/image-retrieval)[Azure Vision multimodal](/en-us/azure/ai-services/computer-vision/how-to/image-retrieval)[Microsoft Foundry hub-based project](/en-us/azure/ai-foundry/how-to/hub-create-projects?view=foundry-classic&pivots=web-portal&preserve-view=true)- phi-4
- gpt-4o
- gpt-4o-mini
- gpt-5
- gpt-5-mini
- gpt-5-nano

- text-embedding-ada-002
- text-embedding-3-small
- text-embedding-3-large
- Cohere-embed-v3-english
2 - Cohere-embed-v3-multilingual
2

- Cohere-embed-v3-english
2 - Cohere-embed-v3-multilingual
2

[Microsoft Foundry project](/en-us/azure/ai-foundry/how-to/create-projects?view=foundry-classic&pivots=web-portal&preserve-view=true)- phi-4
- gpt-4o
- gpt-4o-mini
- gpt-5
- gpt-5-mini
- gpt-5-nano

- text-embedding-ada-002
- text-embedding-3-small
- text-embedding-3-large

[Azure OpenAI resource](/en-us/azure/ai-foundry/openai/how-to/create-resource?view=foundry-classic&pivots=web-portal&preserve-view=true)3, 4- gpt-4o
- gpt-4o-mini
- gpt-5
- gpt-5-mini
- gpt-5-nano

- text-embedding-ada-002
- text-embedding-3-small
- text-embedding-3-large

1 For billing purposes, you must [attach your multi-service account](cognitive-search-attach-cognitive-services) to your Azure AI Search skillset. Currently, the wizard requires your search service and multi-service account to be in the [same supported region for the Azure Vision multimodal embeddings skill](cognitive-search-skill-vision-vectorize#supported-regions), even when using keyless connections.

2 To use this model in the wizard, you must provision it as a serverless API deployment. You can use an [ARM/Bicep template](https://github.com/Azure-Samples/azure-ai-search-multimodal-sample/blob/42b4d07f2dd9f7720fdc0b0788bf107bdac5eecb/infra/ai/modules/project.bicep#L37C1-L38C1) for this task.

3 The endpoint of your Azure OpenAI resource must have a [custom subdomain](/en-us/azure/ai-services/cognitive-services-custom-subdomains), such as `https://my-unique-name.openai.azure.com`

. If you created your resource in the [Azure portal](https://portal.azure.com/), this subdomain was automatically generated during resource setup.

4 Azure OpenAI resources (with access to embedding models) that were created in the [Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs) aren't supported. You must create an Azure OpenAI resource in the Azure portal.

### Public endpoint requirements

All of the preceding resources must have public access enabled so that the Azure portal nodes can access them. Otherwise, the wizard fails. After the wizard runs, you can enable firewalls and private endpoints on the integration components for security. For more information, see [Secure connections in the import wizards](search-import-data-portal#secure-connections).

If private endpoints are already present and you can't disable them, the alternative is to run the respective end-to-end flow from a script or program on a virtual machine. The virtual machine must be on the same virtual network as the private endpoint. [Here's a Python code sample](https://github.com/Azure/azure-search-vector-samples/tree/main/demo-python/code/integrated-vectorization) for integrated vectorization. The same [GitHub repo](https://github.com/Azure/azure-search-vector-samples/tree/main) has samples in other programming languages.

### Check for space

If you're starting with the free service, you're limited to three indexes, three data sources, three skillsets, and three indexers. Make sure you have room for extra items before you begin. This quickstart creates one of each object.

## Configure access

Before you begin, make sure you have permissions to access content and operations. We recommend Microsoft Entra ID authentication and role-based access for authorization. You must be an **Owner** or **User Access Administrator** to assign roles. If roles aren't feasible, you can use [key-based authentication](search-security-api-keys) instead.

Configure the [required roles](#required-roles) and [conditional roles](#conditional-roles) identified in this section.

### Required roles

Azure AI Search and Azure Storage are required for all multimodal search scenarios.

Azure AI Search provides the multimodal pipeline. Configure access for yourself and your search service to read data, run the pipeline, and interact with other Azure resources.

On your Azure AI Search service:

[Assign the following roles](search-security-rbac)to yourself.**Search Service Contributor****Search Index Data Contributor****Search Index Data Reader**


### Conditional roles

The following tabs cover all wizard-compatible resources for multimodal search. Select only the tabs that apply to your chosen [extraction method](#supported-extraction-methods) and [embedding method](#supported-embedding-methods).

A multi-service account provides access to multiple Azure AI services, including [Azure Document Intelligence](/en-us/azure/ai-services/document-intelligence/overview) for content extraction and [Azure Vision](/en-us/azure/ai-services/computer-vision/overview) for content embedding. Your search service requires access to call the [Document Layout skill](cognitive-search-skill-document-intelligence-layout) and [Azure Vision multimodal embeddings skill](cognitive-search-skill-vision-vectorize).

On your multi-service account:

- Assign
**Cognitive Services User**to your[search service identity](search-how-to-managed-identities#create-a-system-managed-identity).

## Prepare sample data

This quickstart uses a sample multimodal PDF, but you can also use your own files. If you're on a free search service, use fewer than 20 files to stay within the free quota for enrichment processing.

To prepare the sample data for this quickstart:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your Azure Storage account.From the left pane, select

**Data storage**>**Containers**.Create a container, and then upload the

[sample PDF](https://github.com/Azure-Samples/azure-search-sample-data/blob/main/sustainable-ai-pdf/Accelerating-Sustainability-with-AI-2025.pdf)to the container.Create another container to store images extracted from the PDF.


## Deploy models

Note

If you're using Azure Vision, skip this step. The multimodal embeddings are built into your multi-service account and don't require model deployment.

The wizard offers several options for content embedding. Image verbalization requires an LLM to describe images and an embedding model to vectorize text and image content, while direct multimodal embeddings only require an embedding model. These models are available through Azure OpenAI and Foundry.

To deploy the models required for your chosen [embedding method](#supported-embedding-methods), see [Deploy Microsoft Foundry Models in the Foundry portal](/en-us/azure/ai-foundry/how-to/deploy-models-openai).

## Start the wizard

To start the wizard for multimodal search:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your Azure AI Search service.On the

**Overview**page, select**Import data (new)**.Select your data source:

**Azure Blob Storage**or**Azure Data Lake Storage Gen2**.Select

**Multimodal RAG**.

## Run the wizard

The wizard walks you through several configuration steps. This section covers each step in sequence.

### Connect to your data

Azure AI Search requires a connection to a data source for content ingestion and indexing. In this case, the data source is your Azure Storage account.

To connect to your data:

On the

**Connect to your data**page, select your Azure subscription.Select the storage account and container to which you uploaded the sample data.

Select the

**Authenticate using managed identity**checkbox. Leave the identity type as**System-assigned**.Select

**Next**.

### Extract your content

Depending on your chosen [extraction method](#supported-extraction-methods), the wizard provides configuration options for document cracking and chunking.

The default method calls the [Document Extraction skill](cognitive-search-skill-document-extraction) to extract text content and generate normalized images from your documents. The [Text Split skill](cognitive-search-skill-textsplit) is then called to split the extracted text content into pages.

To use the Document Extraction skill:

### Embed your content

During this step, the wizard uses your chosen [embedding method](#supported-embedding-methods) to generate vector representations of both text and images.

The wizard calls one skill to create descriptive text for images (image verbalization) and another skill to create vector embeddings for both text and images.

For image verbalization, the [GenAI Prompt skill](cognitive-search-skill-genai-prompt) uses your deployed LLM to analyze each extracted image and produce a natural-language description.

For embeddings, the [Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding), [AML skill](cognitive-search-aml-skill), or [Azure Vision multimodal embeddings skill](cognitive-search-skill-vision-vectorize) uses your deployed embedding model to convert text chunks and verbalized descriptions into high-dimensional vectors. These vectors enable similarity and hybrid retrieval.

To use the skills for image verbalization:

On the

**Content embedding**page, select**Image Verbalization**.On the

**Image Verbalization**tab:For the kind, select your LLM provider:

**Azure OpenAI**or**Azure AI Foundry**.Select your Azure subscription, resource, and LLM deployment.

For the authentication type, select

**System assigned identity**if you're not using a hub-based project. Otherwise, leave it as**API key**.Select the checkbox that acknowledges the billing effects of using these resources.


On the

**Text Vectorization**tab:For the kind, select your model provider:

**Azure OpenAI**,**Azure AI Foundry**, or**AI Vision vectorization**.Select your Azure subscription, resource, and embedding model deployment (if applicable).

For the authentication type, select

**System assigned identity**if you're not using a hub-based project. Otherwise, leave it as**API key**.Select the checkbox that acknowledges the billing effects of using these resources.


Select

**Next**.

### Store the extracted images

The next step is to send images extracted from your documents to Azure Storage. In Azure AI Search, this secondary storage is known as a [knowledge store](knowledge-store-concept-intro).

To store the extracted images:

On the

**Image output**page, select your Azure subscription.Select the storage account and blob container you created to store the images.

Select the

**Authenticate using managed identity**checkbox. Leave the identity type as**System-assigned**.Select

**Next**.

### Add semantic ranking

On the **Advanced settings** page, you can optionally add [semantic ranking](semantic-search-overview) to rerank results at the end of query execution. Reranking promotes the most semantically relevant matches to the top.

### Map new fields

On the **Advanced settings** page, you can optionally add fields to the index schema. By default, the wizard generates the fields described in the following table.

| Field | Applies to | Description | Attributes |
|---|---|---|---|
| content_id | Text and image vectors | String field. Document key for the index. | Retrievable, sortable, and searchable. |
| document_title | Text and image vectors | String field. Human-readable document title. | Retrievable and searchable. |
| text_document_id | Text vectors | String field. Identifies the parent document from which the text chunk originates. | Retrievable and filterable. |
| image_document_id | Image vectors | String field. Identifies the parent document from which the image originates. | Retrievable and filterable. |
| content_text | Text vectors | String field. Human-readable version of the text chunk. | Retrievable and searchable. |
| content_embedding | Text and image vectors | Collection(Edm.Single). Vector representation of text and images. | Retrievable and searchable. |
| content_path | Text and image vectors | String field. Path to the content in the storage container. | Retrievable and searchable. |
| locationMetadata | Image vectors | Edm.ComplexType. Contains metadata about the image's location in the documents. | Varies by field. |

You can't modify the generated fields or their attributes, but you can add fields if your data source provides them. For example, Azure Blob Storage provides a collection of metadata fields.

To add fields to the index schema:

Under

**Index fields**, select**Preview and edit**.Select

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

The final step is to review your configuration and create the necessary objects for multimodal search. If necessary, return to the previous pages in the wizard to adjust your configuration.

To finish the wizard:

On the

**Review and create**page, specify a prefix for the objects the wizard will create. A common prefix helps you stay organized.Select

**Create**.

When the wizard completes the configuration, it creates the following objects:

An indexer that drives the indexing pipeline.

A data source connection to Azure Blob Storage.

An index with text fields, vector fields, vectorizers, vector profiles, and vector algorithms. During the wizard workflow, you can't modify the default index. Indexes conform to the

[2024-05-01-preview REST API](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2024-05-01-preview&preserve-view=true)so that you can use preview features.A skillset with the following skills:

The

[Document Extraction skill](cognitive-search-skill-document-extraction)or[Document Layout skill](cognitive-search-skill-document-intelligence-layout)extracts text and images from source documents. The[Text Split skill](cognitive-search-skill-textsplit)accompanies the Document Extraction skill for data chunking, while the Document Layout skill has built-in chunking.The

[GenAI Prompt skill](cognitive-search-skill-genai-prompt)verbalizes images in natural language. If you're using direct multimodal embeddings, this skill is absent.The

[Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding),[AML skill](cognitive-search-aml-skill), or[Azure Vision multimodal embeddings skill](cognitive-search-skill-vision-vectorize)is called once for text vectorization and once for image vectorization.The

[Shaper skill](cognitive-search-skill-shaper)enriches the output with metadata and creates new images with contextual information.


Tip

Wizard-created objects have configurable JSON definitions. To view or modify these definitions, select **Search management** from the left pane, where you can view your indexes, indexers, data sources, and skillsets.

## Check results

This quickstart creates a multimodal index that supports [hybrid search](hybrid-search-overview) over both text and images. Unless you use direct multimodal embeddings, the index doesn't accept images as query inputs, which requires the [AML skill](cognitive-search-aml-skill) or [Azure Vision multimodal embeddings skill](cognitive-search-skill-vision-vectorize) with an equivalent vectorizer. For more information, see [Configure a vectorizer in a search index](vector-search-how-to-configure-vectorizer).

Hybrid search combines full-text queries and vector queries. When you issue a hybrid query, the search engine computes the semantic similarity between your query and the indexed vectors and ranks the results accordingly. For the index created in this quickstart, the results surface content from the `content_text`

field that closely aligns with your query.

To query your multimodal index:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your Azure AI Search service.From the left pane, select

**Search management**>**Indexes**.Select your index.

Select

**Query options**, and then select**Hide vector values in search results**. This step makes the results more readable.Enter text for which you want to search. Our example uses

`energy`

.To run the query, select

**Search**.The JSON results should include text and image content related to

`energy`

in your index. If you enabled semantic ranker, the`@search.answers`

array provides concise, high-confidence[semantic answers](semantic-answers)to help you quickly identify relevant matches.`"@search.answers": [ { "key": "a71518188062_aHR0cHM6Ly9oYWlsZXlzdG9yYWdlLmJsb2IuY29yZS53aW5kb3dzLm5ldC9tdWx0aW1vZGFsLXNlYXJjaC9BY2NlbGVyYXRpbmctU3VzdGFpbmFiaWxpdHktd2l0aC1BSS0yMDI1LnBkZg2_normalized_images_7", "text": "A vertical infographic consisting of three sections describing the roles of AI in sustainability: 1. **Measure, predict, and optimize complex systems**: AI facilitates analysis, modeling, and optimization in areas like energy distribution, resource allocation, and environmental monitoring. **Accelerate the development of sustainability solution...", "highlights": "A vertical infographic consisting of three sections describing the roles of AI in sustainability: 1. **Measure, predict, and optimize complex systems**: AI facilitates analysis, modeling, and optimization in areas like<em> energy distribution, </em>resource<em> allocation, </em>and environmental monitoring. **Accelerate the development of sustainability solution...", "score": 0.9950000047683716 }, { "key": "1cb0754930b6_aHR0cHM6Ly9oYWlsZXlzdG9yYWdlLmJsb2IuY29yZS53aW5kb3dzLm5ldC9tdWx0aW1vZGFsLXNlYXJjaC9BY2NlbGVyYXRpbmctU3VzdGFpbmFiaWxpdHktd2l0aC1BSS0yMDI1LnBkZg2_text_sections_5", "text": "...cross-laminated timber.8 Through an agreement with Brookfield, we aim 10.5 gigawatts (GW) of renewable energy to the grid.910.5 GWof new renewable energy capacity to be developed across the United States and Europe.Play 4 Advance AI policy principles and governance for sustainabilityWe advocated for policies that accelerate grid decarbonization", "highlights": "...cross-laminated timber.8 Through an agreement with Brookfield, we aim <em> 10.5 gigawatts (GW) of renewable energy </em>to the<em> grid.910.5 </em>GWof new<em> renewable energy </em>capacity to be developed across the United States and Europe.Play 4 Advance AI policy principles and governance for sustainabilityWe advocated for policies that accelerate grid decarbonization", "score": 0.9890000224113464 }, { "key": "1cb0754930b6_aHR0cHM6Ly9oYWlsZXlzdG9yYWdlLmJsb2IuY29yZS53aW5kb3dzLm5ldC9tdWx0aW1vZGFsLXNlYXJjaC9BY2NlbGVyYXRpbmctU3VzdGFpbmFiaWxpdHktd2l0aC1BSS0yMDI1LnBkZg2_text_sections_50", "text": "ForewordAct... Similarly, we have restored degraded stream ecosystems near our datacenters from Racine, Wisconsin120 to Jakarta, Indonesia.117INNOVATION SPOTLIGHTAI-powered Community Solar MicrogridsDeveloping energy transition programsWe are co-innovating with communities to develop energy transition programs that align their goals with broader s.", "highlights": "ForewordAct... Similarly, we have restored degraded stream ecosystems near our datacenters from Racine, Wisconsin120 to Jakarta, Indonesia.117INNOVATION SPOTLIGHTAI-powered Community<em> Solar MicrogridsDeveloping energy transition programsWe </em>are co-innovating with communities to develop<em> energy transition programs </em>that align their goals with broader s.", "score": 0.9869999885559082 } ]`


## Clean up resources

This quickstart uses billable Azure resources. If you no longer need the resources, delete them from your subscription to avoid charges.

## Next steps

This quickstart introduced you to the **Import data (new)** wizard, which creates all of the necessary objects for multimodal search. To explore each step in detail, see the following tutorials: