---
merged_at: 2026-01-25T03:18:14.001849
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-indexer-sharepoint-access-control-lists.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-indexer-sharepoint-access-control-lists -->

# Use a SharePoint indexer to ingest permission metadata and filter search results based on user access rights

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

This article explains how to ingest an Access Control List (ACL) alongside other content from SharePoint in Microsoft 365 using an Azure AI Search indexer. Permissions from SharePoint are preserved as permission metadata for each indexed document. When users query an index containing content from SharePoint, their search results consist of only those documents for which they have permission to access.

Important

For scenarios that require the full SharePoint permissions model, sensitivity labels, and out-of-the-box security trimming, use a [remote SharePoint knowledge source](agentic-knowledge-source-how-to-sharepoint-remote). This approach calls SharePoint directly via the [Copilot retrieval API](/en-us/microsoft-365-copilot/extensibility/api/ai-services/retrieval/overview) so governance remains fully in SharePoint and query results automatically respect all applicable permissions and labels.

## Prerequisites

[Azure AI Search](search-create-service-portal)(Basic or higher).SharePoint in Microsoft 365 sites, libraries, folders, and files with configured permissions.

Follow all configuration steps mentioned in the

[SharePoint indexer documentation](search-how-to-index-sharepoint-online). Make sure that you apply the specific requirements in this document for ACL ingestion configuration.Configure

[Application permissions](search-how-to-index-sharepoint-online#step-2-decide-which-permissions-the-indexer-requires)with`Files.Read.All`

and`Sites.FullControl.All`

(or`Sites.Selected`

instead of`Sites.FullControl.All`

), to index only the content and permissions of specific sites. Then, grant the application full control permissions for just those selected sites.

## Limitations

During public preview, this functionality applies to initial ingestion only: ACLs are captured on the first ingestion of each file. If permissions change in the source, you must

[explicitly reindex those documents or their respective ACLs](#synchronize-permissions-between-indexed-and-source-content).Not supported in this preview:

[SharePoint Information Management policies](/en-us/sharepoint/intro-to-info-mgmt-policies)applicable to user access.- Document
[shareable](/en-us/sharepoint/shareable-links-anyone-specific-people-organization)"Anyone links" or "People in your organization links". Only "specific people links" sync are supported. [SharePoint groups](/en-us/sharepoint/modern-experience-sharing-permissions)that can't be resolved to Microsoft Entra groups (such as Owners, Members, Visitors groups).- Azure portal is out of support during preview; use REST API version 2025-11-01-preview or SDK preview packages.
- This feature must not be tested in combination with
[sensitivity labels preservation and honoring](search-indexer-sensitivity-labels)feature at this time. Both features must be tested on different indexers and indexes accordingly, since their coexistence is not supported currently.


## Support for the SharePoint permission model

This preview supports only basic ACLs for documents, as shown in the following table. The SharePoint indexer doesn't support lists ingestion, so it excludes lists permissions.

| SharePoint Feature | Description | Supported | Notes |
|---|---|---|---|
| Site & library inheritance | Site → library → folder → file. | ✔️ | Evaluated at ingestion; effective ACLs computed per file. |
| Folder & file unique ACLs | Item-level access. | ✔️ | Included when present at first ingestion. |
| Microsoft Entra (M365/Security) Groups | Group-based access. | ✔️ | Group IDs included when resolvable to Entra identifier (ID). |
| SharePoint site groups | Owners/Members/Visitors. | ⚠️ Partial | Included only when resolvable to Entra group ID. |
| Shareable "Anyone links" or "People in your organization links" | Org-wide or public access. | ❌ | Not supported in preview. |
| External/guest users | Access for guests. | ❌ | Not supported. |
| Information Management policies | Policies to define specific permissions requirements. | ❌ | Not supported in preview. |
| Purview sensitivity labels | Document-level security for privacy, categorization, permissions, and encryption | ❌ | Supported via a separate feature:
|

## How hierarchical permissions are evaluated

SharePoint permissions inherit the hierarchy of Site → Library → Folder → File, unless inheritance is broken.

During ingestion, the indexer gathers user and group identifiers (ID) at each level and computes the effective ACL for each file.

## Configure your search service for ACL ingestion and honoring at query time

These steps configure your search service for ACL ingestion and enable ACL honoring at query time.

### 1. Data source configuration

Set `indexerPermissionOptions`

in the [data source definition](search-how-to-index-sharepoint-online#step-4-create-data-source) to allow indexing of `userIds`

and `groupIds`

from SharePoint documents.

```
{
"name": "my-sharepoint-acl-datasource",
"type": "sharepoint",
"indexerPermissionOptions": ["userIds", "groupIds"],
"credentials": {
"connectionString": "<connection-string>;"
},
"container": {
"name": "<library-name>",
"query": "<optional-folder-path>"
}
}
```


### 2. Add permission fields to the index definition

Add fields to your [index schema definition](search-how-to-index-sharepoint-online#step-5-create-an-index) to store ACLs and support query-time filtering.

```
{
"fields": [
{ "name": "UserIds", "type": "Collection(Edm.String)", "permissionFilter": "userIds", "filterable": true, "retrievable": false },
{ "name": "GroupIds", "type": "Collection(Edm.String)", "permissionFilter": "groupIds", "filterable": true, "retrievable": false }
],
"permissionFilterOption": "enabled"
}
```


Set `retrievable`

attribute to `true`

only during development to verify values. You can change retrievable from true to false with no index rebuild requirement.

### 3. Configure index projections in your skillset (if applicable)

If your indexer uses a [skillset](cognitive-search-working-with-skillsets) with data chunking, such as a [split skill](cognitive-search-skill-textsplit) when enabling [integrated vectorization](vector-search-integrated-vectorization), make sure to map ACL properties to each chunk using [index projections](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2025-11-01-preview&preserve-view=true).

```
PUT https://{service}.search.windows.net/skillsets/{skillset}?api-version=2025-11-01-preview
{
"name": "my-skillset",
"skills": [
{
"@odata.type": "#Microsoft.Skills.Text.SplitSkill",
"name": "#split",
"context": "/document",
"inputs": [{ "name": "text", "source": "/document/content" }],
"outputs": [{ "name": "textItems", "targetName": "chunks" }]
}
// ... (other skills such as embeddings, entity recognition, etc.)
],
"indexProjections": {
"selectors": [
{
"targetIndexName": "chunks-index",
"parentKeyFieldName": "parentId", // must exist in target index
"sourceContext": "/document/chunks/*", // match your split output path
"mappings": [
{ "name": "chunkId", "source": "/document/chunks/*/id" }, // if you create an id per chunk
{ "name": "content", "source": "/document/chunks/*/text" }, // chunk text
{ "name": "parentId", "source": "/document/id" }, // parent doc id
{ "name": "UserIds", "source": "/document/metadata_user_ids" } // <-- parent → child
{ "name": "GroupIds", "source": "/document/metadata_group_ids" } // <-- parent → child
]
}
],
"parameters": {
"projectionMode": "skipIndexingParentDocuments"
}
}
}
```


### 4. Configure the indexer field mappings for ACLs

Besides your required [indexer configuration](search-how-to-index-sharepoint-online#step-6-create-an-indexer), map raw metadata ACL fields from SharePoint to your index fields.

```
{
"fieldMappings": [
{ "sourceFieldName": "metadata_user_ids", "targetFieldName": "UserIds" },
{ "sourceFieldName": "metadata_group_ids", "targetFieldName": "GroupIds" }
]
}
```


## Synchronize permissions between indexed and source content

During public preview when the configuration is completed, and ACLs are captured during the first indexer run and for new files only. To pick up later changes:

| Change Scope | Recommended | Trigger | What refreshes |
|---|---|---|---|
| Single/few files | Update | LastModified | Content and ACLs |
| Many items | Update |
|

### Reset specific documents

You can [reset specific documents](/en-us/rest/api/searchservice/indexers/reset-docs?view=rest-searchservice-2025-11-01-preview&preserve-view=true) to fully ingest again content and ACLs.

```
POST https://{service}.search.windows.net/indexers/{indexer}/resetdocs?api-version=2025-11-01-preview
{
"documentKeys": ["doc123", "doc456"]
}
```


### Resync ACLs across the full data source

You can [resync the full data set ACL content](/en-us/rest/api/searchservice/indexers/resync?view=rest-searchservice-2025-11-01-preview&preserve-view=true) after initial ingestion.

```
POST https://{service}.search.windows.net/indexers/{indexer}/resync?api-version=2025-11-01-preview
{
"options": ["permissions"]
}
```


Important

If you change SharePoint permissions without triggering an update mechanism, the index serves stale ACL data for previously ingested files.

After indexing your data and ACLs, you can [query the index](search-query-access-control-rbac-enforcement). .


---

<!-- DOCUMENTO FUSIONADO: multimodal-search-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/multimodal-search-overview -->

# Multimodal search in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Multimodal search refers to the ability to ingest, understand, and retrieve information across multiple content types, including text, images, video, and audio. In Azure AI Search, multimodal search natively supports the ingestion of documents containing text and images and the retrieval of their content, enabling you to perform searches that combine both modalities.

Building a robust multimodal pipeline typically involves:

Extracting inline images and page text from documents.

Describing images in natural language.

Embedding both text and images into a shared vector space.

Storing the images for later use as annotations.


Multimodal search also requires preserving the order of information as it appears in the documents and executing [hybrid queries](hybrid-search-overview) that combine [full-text search](search-lucene-query-architecture) with [vector search](vector-search-overview) and [semantic ranking](semantic-search-overview).

In practice, an application that uses multimodal search can answer questions like "What is the process to have an HR form approved?" even when the only authoritative description of the process lives inside an embedded diagram in a PDF file.

## Why use multimodal search?

Traditionally, multimodal search requires separate systems for text and image processing, often requiring custom code and low-level configurations from developers. Maintaining these systems incurs higher costs, complexity, and effort.

Azure AI Search addresses these challenges by integrating images into the same retrieval pipeline as text. With a single multimodal pipeline, you can simplify setup and unlock information that resides in charts, screenshots, infographics, scanned forms, and other complex visuals.

Multimodal search is ideal for [retrieval-augmented generation (RAG)](retrieval-augmented-generation-overview) scenarios. By interpreting the structural logic of images, multimodal search makes your RAG application or AI agent less likely overlook important visual details. It also provides your users with detailed answers that can be traced back to their original sources, regardless of the source's modality.

## How does multimodal search work?

To simplify the creation of a multimodal pipeline, Azure AI Search offers the **Import data (new)** wizard in the Azure portal. The wizard helps you configure a data source, define extraction and enrichment settings, and generate a multimodal index that contains text, embedded image references, and vector embeddings. For more information, see [Quickstart: Multimodal search in the Azure portal](search-get-started-portal-image-search).

The wizard follows these steps to create a multimodal pipeline:

**Extract content:**Choose from the[Document Extraction skill](cognitive-search-skill-document-extraction),[Document Layout skill](cognitive-search-skill-document-intelligence-layout), or[Azure Content Understanding skill](cognitive-search-skill-content-understanding)to obtain page text, inline images, and structural metadata. Each skill offers different capabilities for metadata extraction, table handling, and file format support. For detailed comparisons, see[Options for multimodal content extraction](#options-for-multimodal-content-extraction).**Chunk text:**The[Text Split skill](cognitive-search-skill-textsplit)breaks the extracted text into manageable chunks for use in the remaining pipeline, such as the embedding skill.**Generate image descriptions:**The[GenAI Prompt skill](cognitive-search-skill-genai-prompt)verbalizes images, producing concise natural-language descriptions for text search and embedding using a large language model (LLM).**Generate embeddings:**The embedding skill creates vector representations of text and images, enabling similarity and hybrid retrieval. You can call[Azure OpenAI](cognitive-search-skill-azure-openai-embedding),[Microsoft Foundry](cognitive-search-aml-skill), or[Azure Vision](cognitive-search-skill-vision-vectorize)embedding models natively.Alternatively, you can skip image verbalization and pass the extracted text and images directly to a multimodal embedding model through the

[AML skill](cognitive-search-aml-skill)or[Azure Vision multimodal embeddings skill](cognitive-search-skill-vision-vectorize). For more information, see[Options for multimodal content embedding](#options-for-multimodal-content-embedding).**Store extracted images:**The[knowledge store](knowledge-store-concept-intro)contains extracted images that can be returned directly to client applications. When you use the wizard, an image's location is stored directly in the multimodal index, enabling convenient retrieval at query time.

Tip

To see multimodal search in action, plug your wizard-created index into the [multimodal RAG sample application](https://aka.ms/azs-multimodal-sample-app-repo). The sample demonstrates how a RAG application consumes a multimodal index and renders both textual citations and associated image snippets in the response. The sample also showcases the code-based process of data ingestion and indexing.

## Options for multimodal content extraction

A multimodal pipeline begins by cracking each source document into chunks of text, inline images, and associated metadata. For this step, Azure AI Search provides three built-in skills:

| Characteristic | Document Extraction skill | Document Layout skill | Azure Content Understanding skill |
|---|---|---|---|
| Text location metadata extraction (pages and bounding polygons) | No | Yes | Yes |
| Image location metadata extraction (pages and bounding polygons) | Yes | Yes | Yes |
| Table extraction and preservation | No | No | Yes (including cross-page tables) |
| Cross-page semantic units | Not applicable | Single page only | Yes (spans page boundaries) |
| Location metadata extraction based on file type | PDFs only. | Multiple supported file types according to the
|

[Multiple supported file types](/en-us/azure/ai-services/content-understanding/language-region-support), including PDF, DOCX, XLSX, and PPTX.[Azure AI Search pricing](https://azure.microsoft.com/pricing/details/search/).[Document Layout pricing](https://azure.microsoft.com/pricing/details/ai-document-intelligence/).[Azure Content Understanding pricing](https://azure.microsoft.com/pricing/details/content-understanding/).## Options for multimodal content embedding

In Azure AI Search, retrieving knowledge from images can follow two complementary paths: image verbalization or direct embeddings. Understanding the distinctions helps you align cost, latency, and answer quality with the needs of your application.

### Image verbalization followed by text embeddings

With this method, the [GenAI Prompt skill](cognitive-search-skill-genai-prompt) invokes an LLM during ingestion to create a concise natural-language description of each extracted image, such as "Five-step HR access workflow that begins with manager approval." The description is stored as text and embedded alongside the surrounding document text, which you can then vectorize by calling the [Azure OpenAI](cognitive-search-skill-azure-openai-embedding), [Microsoft Foundry](cognitive-search-aml-skill), or [Azure Vision](cognitive-search-skill-vision-vectorize) embedding models.

Because the image is now expressed in language, Azure AI Search can:

Interpret the relationships and entities shown in a diagram.

Supply ready-made captions that an LLM can cite verbatim in a response.

Return relevant snippets for RAG applications or AI agent scenarios with grounded data.


The added semantic depth entails an LLM call for every image and a marginal increase in indexing time.

### Direct multimodal embeddings

A second option is to pass the document-extracted images and text to a multimodal embedding model that produces vector representations in the same vector space. Configuration is straightforward, and no LLM is required at indexing time. Direct embeddings are well suited to visual similarity and “find-me-something-that-looks-like-this” scenarios.

Because the representation is purely mathematical, it doesn't convey why two images are related, and it doesn't offer the LLM ready context for citations or detailed explanations.

### Combining both approaches

Many solutions need both encoding paths. Diagrams, flow charts, and other explanation-rich visuals are verbalized so that semantic information is available for RAG and AI agent grounding. Screenshots, product photos, or artwork are embedded directly for efficient similarity search. You can customize your Azure AI Search index and indexer skillset pipeline so it can store the two sets of vectors and retrieve them side by side.

## Options for querying multimodal content

If your multimodal pipeline is powered by the GenAI Prompt skill, you can run [hybrid queries](hybrid-search-overview) over both plain text and verbalized images in your search index. You can also use filters to narrow the search results to specific content types, such as only text or only images.

Although the GenAI Prompt skill supports text-to-vector queries via hybrid search, it doesn't support [image-to-vector queries](search-explorer#example-image-query). Only the multimodal embedding models provide the vectorizers that convert images into vectors at query time.

To use images as query inputs for your multimodal index, you must use the [AML skill](cognitive-search-aml-skill) or [Azure Vision multimodal embeddings skill](cognitive-search-skill-vision-vectorize) with an equivalent vectorizer. For more information, see [Configure a vectorizer in a search index](vector-search-how-to-configure-vectorizer).

## Tutorials and samples

To help you get started with multimodal search in Azure AI Search, here's a collection of content that demonstrates how to create and optimize multimodal indexes using Azure functionality.

| Content | Description |
|---|---|
|
