---
source_url: https://learn.microsoft.com/en-us/azure/search/whats-new
fetched_at: 2026-01-25T02:09:12.721092
---

# What's new in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn about the latest updates to Azure AI Search functionality, docs, and samples.

Note

Preview features are announced here, but we also maintain a [preview features list](search-api-preview) so you can find them in one place.

## December 2025

| Item | Description |
|---|---|
|

[Knowledge bases](agentic-retrieval-how-to-create-knowledge-base)and[knowledge sources](agentic-knowledge-source-overview)in the Azure portal have been updated to use the 2025-11-01-preview REST APIs instead of the 2025-08-01-preview. Portal-created knowledge bases now support the[retrieval reasoning effort](agentic-retrieval-how-to-set-retrieval-reasoning-effort), and query-time properties (maximum runtime and maximum output size) have been removed from the UI. The portal continues to support search index and blob knowledge sources only; other knowledge source types must be created programmatically.If you previously created knowledge bases or knowledge sources in the portal, those objects still use the 2025-08-01-preview schema. For help with breaking changes, see [Migrate your agentic retrieval code](agentic-retrieval-how-to-migrate).

## November 2025

| Item | Description |
|---|---|
|

[Semantic ranker and agentic retrieval on free tiers](semantic-search-overview)[select regions](search-region-support), subject to limits on query volume.[Knowledge agents renamed to knowledge bases](agentic-retrieval-overview)[Migrate your agentic retrieval code](agentic-retrieval-how-to-migrate).[Knowledge bases (preview)](agentic-retrieval-how-to-create-knowledge-base)`retrievalInstructions`

and `outputConfiguration`

properties for improved query planning and execution control. It also provides a new [reasoning effort](agentic-retrieval-how-to-set-retrieval-reasoning-effort)for control over LLM processing.[Knowledge sources (preview)](agentic-knowledge-source-overview)[indexed OneLake](agentic-knowledge-source-how-to-onelake),[indexed SharePoint](agentic-knowledge-source-how-to-sharepoint-indexed),[remote SharePoint](agentic-knowledge-source-how-to-sharepoint-remote), and[web](agentic-knowledge-source-how-to-web). For indexed knowledge sources, the new`ingestionParameters`

object provides properties to control content ingestion and processing, including `contentExtractionMode`

for use of the [Azure Content Understanding skill](cognitive-search-skill-content-understanding)and`ingestionPermissionOptions`

for use of ACLs in the generated indexer.[Knowledge retrieval (preview)](agentic-retrieval-how-to-retrieve)[reasoning effort](agentic-retrieval-how-to-set-retrieval-reasoning-effort), zero-model-call mode for efficiency, and partial responses.[Portal support for knowledge sources and knowledge bases (preview)](get-started-portal-agentic-retrieval)[Migrate your agentic retrieval code](agentic-retrieval-how-to-migrate).[Foundry IQ (preview)](/en-us/azure/ai-foundry/agents/how-to/tools/knowledge-retrieval)[Azure Content Understanding skill (preview)](cognitive-search-skill-content-understanding)`contentExtractionMode`

property within `ingestionParameters`

.[SharePoint indexer ACL support (preview)](search-indexer-sharepoint-access-control-lists)[Elevated read permissions for ACLs (preview)](search-query-access-control-rbac-enforcement#elevated-permissions-for-investigating-incorrect-results)[Document-level sensitivity label indexing (preview)](search-indexer-sensitivity-labels)[SharePoint indexing updates (preview)](search-how-to-index-sharepoint-online)[Scoring function aggregation (preview)](index-add-scoring-profiles#example-function-aggregation)[Facet aggregations (preview)](search-faceted-navigation-examples#facet-aggregation-example)`azure-api.net`

endpoint support (preview)[Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding)and[Azure OpenAI vectorizer](vector-search-vectorizer-azure-open-ai)now accept`azure-api.net`

endpoints for Azure API Management (not custom endpoints).`services.ai.azure.com`

endpoint support[GenAI Prompt skill](cognitive-search-skill-genai-prompt),[Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding),[Azure OpenAI vectorizer](vector-search-vectorizer-azure-open-ai), and[AI enrichment](cognitive-search-concept-intro)now accept`services.ai.azure.com`

endpoints for Microsoft Foundry resources. When you [upgrade from Azure OpenAI to Foundry](/en-us/azure/ai-foundry/how-to/upgrade-azure-openai), a new project is automatically created and becomes available for RAG and multimodal RAG in the[.](search-import-data-portal)**Import data (new)**wizard## September 2025

| Item | Description |
|---|---|
|

[Logic app worklow integration](search-how-to-index-logic-apps)[OneLake indexer](search-how-to-index-onelake-files)[Document Layout skill](cognitive-search-skill-document-intelligence-layout)[Normalizers](search-normalizers)[Index description](agentic-retrieval-how-to-create-index#add-a-description)[Rescoring of binary quantized vectors](vector-search-how-to-quantization#supported-rescoring-techniques)[Rescoring options for scalar compressed vectors](vector-search-how-to-quantization#supported-rescoring-techniques)[Scoring profiles for semantically ranked results](semantic-how-to-enable-scoring-profiles)[Truncate dimensions](vector-search-how-to-truncate-dimensions)[Unpack](hybrid-search-ranking#unpack-a-search-score-into-subscores)`@search.score`

to view subscores in hybrid search results[Updates to import wizards (Phase 1)](search-import-data-portal)**Import and vectorize data**wizard has been renamed to**Import data (new)**and redeveloped to support keyword search, modernizing the legacy**Import data**workflow with an improved interface and user experience.**Import data (new)** isn't a direct replacement for the old wizard. For example, it supports fewer skills for keyword search.

Both wizards are currently available, but **Import data** will be deprecated in a future phase.

[Support for Azure confidential computing](search-security-overview#data-in-use)[confidential computing](/en-us/azure/confidential-computing/use-cases-scenarios)during service creation to process data in use on confidential VMs. This compute type isn't intended for general use, but rather for stringent regulatory, compliance, or security requirements.Confidential computing adds a 10% surcharge to the base cost of billable tiers. For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/search/).

Now generally available through the 2025-05-01 version of [Services - Create or Update (REST API)](/en-us/rest/api/searchmanagement/services/create-or-update?view=rest-searchservice-2025-05-01&preserve-view=true) and the [Azure portal](search-create-service-portal#choose-a-compute-type).

## August 2025

| Item | Description |
|---|---|
|

[Knowledge agents (preview)](agentic-retrieval-how-to-create-knowledge-base)`knowledgeSources`

instead of `targetIndexes`

and deprecates `defaultMaxDocsForReranker`

. New `retrievalInstructions`

and `outputConfiguration`

properties provide greater control over query planning and execution. For help with breaking changes, see [Migrate your agentic retrieval code](agentic-retrieval-how-to-migrate).[Knowledge sources (preview)](agentic-knowledge-source-overview)[search indexes](agentic-knowledge-source-how-to-search-index)and[Azure blobs](agentic-knowledge-source-how-to-blob).[Answer synthesis (preview)](agentic-retrieval-how-to-answer-synthesis)`answerSynthesis`

modality for knowledge agents. When specified, an LLM generates a natural-language answer as an embedded step in the retrieval pipeline. This differs from the default `extractiveData`

modality, which returns raw search results for downstream processing.`attemptFastPath`

boolean in knowledge agents enabled a shorter processing time if queries are concise and the initial response is sufficiently relevant. Replacement feature is the minimal retrieval reasoning effort.[Retrieval instructions (preview)](agentic-retrieval-how-to-create-knowledge-base)`retrievalInstructions`

property for knowledge agents guides query planning in an agentic retrieval workflow. For example, you can specify criteria for including or excluding specific knowledge sources.[Improved indexer runtime tracking information (preview)](search-howto-run-reset-indexers#check-indexer-runtime-quota-for-s3-hd-search-services)[Get Service Statistics](/en-us/rest/api/searchservice/get-service-statistics/get-service-statistics?view=rest-searchservice-2025-08-01-preview&preserve-view=true)response now provides cumulative indexer processing information for the entire service.[Get Status - Indexers](/en-us/rest/api/searchservice/indexers/get-status?view=rest-searchservice-2025-08-01-preview&preserve-view=true)provides the same information, but for a specific indexer.[Strict postfiltering for vector queries (preview)](vector-search-filters)`strictPostFilter`

mode for the `vectorFilterMode`

parameter. When specified, filters are applied after the global top-`k`

vector results are identified, ensuring that returned documents are a subset of the unfiltered results.[Increased maximum dimensions for vector fields](search-limits-quotas-capacity#index-limits)`4096`

. This update applies to all stable and preview REST API versions that support vectors and doesn't introduce breaking changes.## July 2025

| Item | Description |
|---|---|
|

[Upgrade to the latest REST API in Azure AI Search](search-api-migration).[Service upgrade](search-how-to-upgrade)[Upgrade Service (REST API)](/en-us/rest/api/searchmanagement/services/upgrade?view=rest-searchmanagement-2025-05-01&preserve-view=true)and the Azure portal.[Pricing tier change](search-capacity-planning#change-your-pricing-tier)`sku`

property in [Update Service (REST API)](/en-us/rest/api/searchmanagement/services/update?view=rest-searchmanagement-2025-05-01&preserve-view=true)and the Azure portal.[User-assigned managed identity assignment](search-how-to-managed-identities)`identity`

property that associates a user-assigned managed identity with a search service configuration. Only the assignment step, via the [Update Service (REST API)](/en-us/rest/api/searchmanagement/services/update?view=rest-searchmanagement-2025-05-01&preserve-view=true)or the Azure portal, is generally available. APIs used for data source or model connections that include a user-assigned managed identity are still in preview.[Network security perimeter](search-security-network-security-perimeter)[Azure Virtual Network Manager REST APIs](/en-us/rest/api/networkmanager/), which are used to join a search service, and the[Search Management REST APIs](/en-us/rest/api/searchmanagement/network-security-perimeter-configurations?view=rest-searchmanagement-2025-05-01&preserve-view=true), which are used to view and synchronize the configuration settings. Portal support for both steps is also generally available.## May 2025

| Item | Description |
|---|---|
|

[knowledge agent](agentic-retrieval-how-to-create-knowledge-base)object is introduced in this preview. Its[response payload](agentic-retrieval-how-to-retrieve)is designed for downstream agent and chat model consumption, with full transparency of the query plan and reference data. To get started in the portal, see[Quickstart: Agentic retrieval](search-get-started-agentic-retrieval).[Multivector support (preview)](vector-search-multi-vector-fields)[Scoring profiles with semantic ranking (preview)](semantic-how-to-enable-scoring-profiles)`@search.rerankerBoostedScore`

, to help you maintain consistent relevance and greater control over final ranking outcomes in your search pipeline.[Azure Logic Apps integration (preview)](search-how-to-index-logic-apps)[Import and vectorize data wizard](search-get-started-portal-import-vectors)in the Azure portal to build an indexing pipeline based on Azure Logic Apps integration.[Document-level access control (preview)](search-document-level-access-overview)[Multimodal search (preview)](multimodal-search-overview)[Quickstart: Search for multimodal content](search-get-started-portal-image-search)for portal wizard support and[Azure AI Search Multimodal RAG Demo](https://github.com/Azure-Samples/azure-ai-search-multimodal-sample)for a code-first approach.[GenAI prompt skill (preview)](cognitive-search-skill-genai-prompt)*image verbalization*, using an LLM to describe images and send the description to a searchable field in your index.[Document Layout skill (preview)](cognitive-search-skill-document-intelligence-layout)[Retrieval Augmented Generation (RAG)](search-get-started-portal-import-vectors)and[Multimodal RAG](search-get-started-portal-image-search). Logic apps integration is through the RAG path.[Index "description" support (preview)](agentic-retrieval-how-to-create-index#add-a-description)[2025-05-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-05-01-preview&preserve-view=true)## April 2025

| Item | Description |
|---|---|
|

[vector indexing at scale](https://github.com/microsoft/rag-time/tree/main/Journey%203%20-%20Optimize%20your%20Vector%20Index%20for%20Scale), and[agentic search](https://techcommunity.microsoft.com/blog/azure-ai-services-blog/bonus-rag-time-journey-agentic-rag/4404652)where you use an agent to evaluate a result and generate a better answer.## March 2025

| Item | Description |
|---|---|
|

[Upgrade Service (2025-02-01-preview)](/en-us/rest/api/searchmanagement/services/upgrade?view=rest-searchmanagement-2025-02-01-preview&preserve-view=true)and the Azure portal.[Pricing tier change (preview)](search-capacity-planning#change-your-pricing-tier)[pricing tier](search-sku-tier)of your search service. This provides flexibility to scale storage, increase request throughput, and decrease latency based on your needs. Initially, this preview only supported upgrades between Basic and Standard (S1, S2, and S3) tiers, but starting in July 2025, it supports upgrades*and*downgrades between these tiers. Available in[Update Service (2025-02-01-preview)](/en-us/rest/api/searchmanagement/services/update?view=rest-searchmanagement-2025-02-01-preview&preserve-view=true#searchupdateservicewithsku)and the Azure portal.[Facet hierarchies, aggregations, and facet filters (preview)](search-faceted-navigation-examples)[Search Documents (2025-03-01-preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2025-03-01-preview&preserve-view=true)and the Azure portal.[Rescore vector queries over binary quantization using full precision vectors (preview)](vector-search-how-to-quantization#supported-rescoring-techniques)`enableRescoring`

and `discardOriginals`

to use this feature, and call the latest preview API version on the request.[Semantic ranker prerelease models (preview)](semantic-how-to-configure#opt-in-for-prerelease-semantic-ranking-models)[Create or Update Index (2025-03-01-preview)](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2025-03-01-preview#semanticconfiguration&preserve-view=true).[Search Service REST 2025-03-01-preview](/en-us/rest/api/searchservice/search-service-api-versions?view=rest-searchservice-2025-03-01-preview&preserve-view=true)[Search Management 2025-02-01-preview](/en-us/rest/api/searchmanagement/management-api-versions?view=rest-searchmanagement-2025-02-01-preview&preserve-view=true)## February 2025

| Item | Description |
|---|---|
|

## 2024 announcements

| Month | Type | Announcement |
|---|---|---|
| December | Template |
|

[Network security perimeter](search-security-network-security-perimeter). Join a search service to a[network security perimeter](/en-us/azure/private-link/network-security-perimeter-concepts)to control network access to your search service. The Azure portal and the Management REST APIs in the[2024-06-01-preview](/en-us/rest/api/searchmanagement/network-security-perimeter-configurations?view=rest-searchmanagement-2024-06-01-preview&preserve-view=true)can be used to view and reconcile network security perimeter configurations.[Shared private link support for Azure AI service connections](search-indexer-howto-access-private). Connections to Azure AI for built-in skills processing can now be private using a shared private link on the connection.[Rescoring options for compressed vectors](vector-search-how-to-quantization#add-compressions-to-a-search-index). You can set options to rescore with original vectors instead of compressed vectors. Applies to HNSW and exhaustive KNN vector algorithms, using binary and scalar compression. Available in the[Create or Update Index (2024-11-01-preview)](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2024-09-01-preview&preserve-view=true), the Azure portal, and in the Azure SDK beta packages that provide this feature.[Store fewer vector instances](vector-search-how-to-storage-options). In vector compression scenarios, you can omit storage of full precision vectors if you don't need them for rescoring. Available in the[Create or Update Index (2024-11-01-preview)](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2024-09-01-preview&preserve-view=true), the Azure portal, and in the Azure SDK beta packages that provide this feature.[Query rewrite in the semantic reranker](semantic-how-to-query-rewrite). You can set options on a semantic query to rewrite the query input into a revised or expanded query that generates more relevant results from the L2 ranker. Available in the[Search Documents (2024-11-01-preview)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2024-11-01-preview&preserve-view=true), the Azure portal, and in the Azure SDK beta packages that provide this feature.[New semantic ranker models](semantic-search-overview). Semantic ranker runs with improved models in all supported regions. There's no change to APIs or the Azure portal experience.[Document Layout skill](cognitive-search-skill-document-intelligence-layout). A new skill used to analyze a document for structure and provide[structure-aware (paragraph) chunking](search-how-to-semantic-chunking). This skill calls Azure Document Intelligence in Foundry Tools and uses the Azure Document Intelligence layout model. Available in selected regions through the[Create or Update Skillset (2024-11-01-preview)](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2024-11-01-preview&preserve-view=true), the Azure portal, and in the Azure SDK beta packages that provide this feature.[Keyless billing for Azure AI skills processing](cognitive-search-attach-cognitive-services). You can now use a managed identity and roles for a keyless connection to Foundry Tools for built-in skills processing. This capability removes restrictions for having both search and Foundry Tools in the same region. Available in the[Create or Update Skillset (2024-11-01-preview)](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2024-11-01-preview&preserve-view=true), the Azure portal, and in the Azure SDK beta packages that provide this feature.[Markdown parsing mode](search-how-to-index-azure-blob-markdown). With this parsing mode, indexers can generate one-to-one or one-to-many search documents from Markdown files in Azure Storage and Microsoft OneLake. Available in the[Create or Update Indexer (2024-11-01-preview)](/en-us/rest/api/searchservice/indexers/create-or-update?view=rest-searchservice-2024-11-01-preview&preserve-view=true), the Azure portal, and in the Azure SDK beta packages that provide this feature.[2024-11-01-preview](/en-us/rest/api/searchservice/search-service-api-versions?view=rest-searchservice-2024-11-01-preview&preserve-view=true). Preview release of REST APIs for query rewrite, Document Layout skill, keyless billing for skills processing, Markdown parsing mode, and rescoring options for compressed vectors.[Portal support for structured data](search-get-started-portal-import-vectors). The**Import and vectorize data**wizard now supports Azure SQL, Azure Cosmos DB, and Azure Table Storage.[Lower the dimension requirements for MRL-trained text embedding models on Azure OpenAI](vector-search-how-to-truncate-dimensions). Text-embedding-3-small and Text-embedding-3-large are trained using Matryoshka Representation Learning (MRL). This allows you to truncate the embedding vectors to fewer dimensions, and adjust the balance between vector index size usage and retrieval quality. A new`truncationDimension`

in the [2024-09-01-preview](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2024-09-01-preview&preserve-view=true)enables access to MRL compression in text embedding models. This can only be configured for new vector fields.[Unpack](hybrid-search-ranking#unpack-a-search-score-into-subscores). You can investigate Reciprocal Rank Fusion (RRF) ranked results by viewing the individual query subscores of the final merged and scored result. A new`@search.score`

to view subscores in hybrid search results`debug`

property unpacks the search score. `QueryResultDocumentSubscores`

, `QueryResultDocumentRerankerInput`

, and `QueryResultDocumentSemanticField`

provide the extra detail. These definitions are available in the [2024-09-01-preview](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2024-09-01-preview&preserve-view=true).[Target filters in a hybrid search to just the vector queries](hybrid-search-how-to-query#example-hybrid-search-with-filters-targeting-vector-subqueries-preview). A filter on a hybrid query involves all subqueries on the request, regardless of type. You can override the global filter to scope the filter to a specific subquery. The new`filterOverride`

parameter is available on hybrid queries using the [2024-09-01-preview](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2024-09-01-preview&preserve-view=true).[Text Split skill (token chunking)](cognitive-search-skill-textsplit). This skill has new parameters that improve data chunking for embedding models. A new`unit`

parameter lets you specify token chunking. You can now chunk by token length, setting the length to a value that makes sense for your embedding model. You can also specify the tokenizer and any tokens that shouldn't be split during data chunking. The new `unit`

parameter and query subscore definitions are found in the [2024-09-01-preview](/en-us/rest/api/searchservice/skillsets/create-or-update?view=rest-searchservice-2024-09-01-preview&preserve-view=true).[2024-09-01-preview](/en-us/rest/api/searchservice/search-service-api-versions?view=rest-searchservice-2024-09-01-preview&preserve-view=true). Preview release of REST APIs for truncated dimensions in text-embedding-3 models, targeted vector filtering for hybrid queries, RRF subscore details for debugging, and token chunking for Text Split skill.[Portal support for customer-managed key encryption (CMK)](search-security-manage-encryption-keys#step-4-encrypt-content). When you create new objects in the Azure portal, you can now specify CMK-encryption and select an Azure Key Vault to provide the key.[Debug Session improvements](cognitive-search-debug-session). There are two important improvements. First, you can now debug integrated vectorization and data chunking workloads. Second, Debug Sessions is redesigned for a more streamlined presentation of skills and mappings. You can select an object in the flow, and view or edit its details in a side panel. The previous tabbed layout is fully replaced with more context-sensitive information on the page.[2024-07-01](/en-us/rest/api/searchservice/search-service-api-versions?view=rest-searchservice-2024-07-01&preserve-view=true). Stable release of REST APIs for generally available vector data types, vector compression, and integrated vectorization during indexing and queries.[Integrated vectorization](vector-search-integrated-vectorization), Announcing general availability. Skills-driven data chunking and embedding during indexing.[Vectorizers](vector-search-how-to-configure-vectorizer). Announcing general availability. Text-to-vector conversion during query execution. Both[Azure OpenAI vectorizer](vector-search-vectorizer-azure-open-ai)and[custom Web API vectorizer](vector-search-vectorizer-custom-web-api)are generally available.[AzureOpenAIEmbedding skill](cognitive-search-skill-azure-openai-embedding). Announcing general availability. A skill type that calls an Azure OpenAI embedding model to generate embeddings during indexing.[Index projections](index-projections-concept-intro). Announcing general availability. A component of a skillset definition that defines the shape of a secondary index, supporting a one-to-many index pattern, where content from an enrichment pipeline can target multiple indexes.[Binary and Scalar quantization](vector-search-how-to-quantization). Announcing general availability. Compress vector index size in memory and on disk using built-in quantization.[Narrow data types](vector-search-how-to-assign-narrow-data-types). Announcing general availability. Assign a smaller data type on vector fields, assuming incoming data is of that data type.[Import and vectorize data wizard](search-get-started-portal-import-vectors). Announcing general availability. A wizard that creates a full indexing pipeline that includes data chunking and vectorization. The wizard creates all necessary objects and configurations. This release adds wizard support for Azure Data Lake in Azure Storage.[stored property](vector-search-how-to-storage-options). Announcing general availability. Boolean that reduces storage of vector indexes by*not*storing retrievable vectors.[vectorQueries.Weight property](vector-search-how-to-query#vector-weighting). Announcing general availability. Specify the relative weight of each vector query in a search operation.[Chat with your data](https://github.com/Azure-Samples/chat-with-your-data-solution-accelerator). A solution accelerator for the RAG pattern running in Azure, using Azure AI Search for retrieval and Azure OpenAI large language models to create conversational search experiences. The code with sample data is available for use case scenarios such as financial advisor and contract review and summarization.[Conversational Knowledge Mining](https://github.com/microsoft/Customer-Service-Conversational-Insights-with-Azure-OpenAI-Services). A solution accelerator built on top of Azure AI Search, Azure Speech in Foundry Tools, and Azure OpenAI that allows customers to extract actionable insights from post-contact center conversations.[Build your own copilot](https://github.com/microsoft/Build-your-own-AI-Assistant-Solution-Accelerator). Create your own custom copilot solution that empowers[Client Advisor](https://github.com/microsoft/Build-your-own-copilot-Solution-Accelerator)to harness the power of generative AI across both structured and unstructured data. Help our customers to optimize daily tasks and foster better interactions with more clients.[Image search in the Azure portal](search-get-started-portal-image-search). Search explorer now supports image search. In a vector index that contains vectorized image content, you can drop images into Search Explorer to query for a match.[Higher capacity and more vector quota at every tier (same billing rate)](search-limits-quotas-capacity#service-limits). For most regions, partition sizes are now even larger for Standard 2 (S2), Standard 3 (S3), and Standard 3 High Density (S3 HD) for services created after April 3, 2024. To get the larger partitions, create a new service in a[region that provides newer infrastructure](search-region-support).Storage Optimized tiers (L1 and L2) also have more capacity. L1 and L2 customers must create a new service to benefit from the higher capacity. There's no in-place upgrade at this time.

Extra capacity is now available in

[more regions](search-limits-quotas-capacity#service-limits): Germany North, Germany West Central, South Africa North, Switzerland West, and Azure Government (Texas, Arizona, and Virginia).[OneLake integration (preview)](search-how-to-index-onelake-files). New indexer for OneLake files and OneLake shortcuts. If you use Microsoft OneLake for data access to Amazon Web Services (AWS) and Google data sources, use this indexer to import external data into a search index. This indexer is available through the Azure portal, the[2024-05-01-preview REST API](/en-us/rest/api/searchservice/data-sources/create-or-update?view=rest-searchservice-2024-05-01-preview&preserve-view=true), and Azure SDK beta packages.[Vector relevance](vector-search-how-to-query)[hybrid query relevance](hybrid-search-how-to-query). Four enhancements improve vector and hybrid search relevance.First, you can now set thresholds on vector search results to exclude low-scoring results.

Second, changes in the query architecture apply scoring profiles at the end of the query pipeline for every query type. Document boosting is a common scoring profile, and it now works as expected on vector and hybrid queries.

Third, you can set

[in hybrid queries to control the quantity of BM25-ranked search results that flow into the hybrid ranking model.](hybrid-search-how-to-query#set-maxtextrecallsize-and-countandfacetmode)`MaxTextRecallSize`

and `countAndFacetMode`

Fourth, for vector and hybrid search, you can weight a vector query to have boost or diminish its importance in a multiquery request.

[Binary vectors support](/en-us/rest/api/searchservice/supported-data-types).`Collection(Edm.Byte)`

is a new supported data type. This data type opens up integration with the [Cohere v3 binary embedding models](https://cohere.com/blog/int8-binary-embeddings)and custom binary quantization. Narrow data types lower the cost of large vector datasets. See[Index binary data for vector search](vector-search-how-to-index-binary-data)for more information.[Azure Vision multimodal embeddings skill (preview)](cognitive-search-skill-vision-vectorize). New skill that's bound to the[multimodal embeddings API of Azure Vision](/en-us/azure/ai-services/computer-vision/concept-image-retrieval). You can generate embeddings for text or images during indexing. This skill is available through the Azure portal and the[2024-05-01-preview REST API](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2024-05-01-preview&preserve-view=true).[Azure Vision vectorizer (preview)](vector-search-vectorizer-ai-services-vision). New vectorizer connects to an Azure Vision resource using the[multimodal embeddings API](/en-us/azure/ai-services/computer-vision/concept-image-retrieval)to generate embeddings at query time. This vectorizer is available through the Azure portal and the[2024-05-01-preview REST API](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2024-05-01-preview&preserve-view=true).[Microsoft Foundry model catalog vectorizer (preview)](vector-search-vectorizer-azure-machine-learning-ai-studio-catalog). New vectorizer connects to an embedding model deployed from the[Foundry model catalog](/en-us/azure/ai-foundry/how-to/model-catalog-overview). This vectorizer is available through the Azure portal and the[2024-05-01-preview REST API](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2024-05-01-preview&preserve-view=true).[.](vector-search-integrated-vectorization-ai-studio)**How to implement integrated vectorization using models from Foundry**[AzureOpenAIEmbedding skill (preview) supports more models on Azure OpenAI](cognitive-search-skill-azure-openai-embedding). Now supports text-embedding-3-large and text-embedding-3-small, along with text-embedding-ada-002 from the previous update. New`dimensions`

and `modelName`

properties make it possible to specify the various embedding models on Azure OpenAI. Previously, the dimensions limits were fixed at 1,536 dimensions, applicable to text-embedding-ada-002 only. The updated skill is available through the Azure portal and the [2024-05-01-preview REST API](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2024-05-01-preview&preserve-view=true).[Import and vectorize data wizard](search-get-started-portal-import-vectors)now supports OneLake indexers as a data source. For embeddings, it also supports connections to Azure Vision multimodal, Foundry model catalog, and more embedding models on Azure OpenAI.When adding a field to an index, you can choose a

[binary data type](vector-search-how-to-index-binary-data).[Search explorer](search-explorer)now defaults to 2024-05-01-preview and supports the new preview features for vector and hybrid queries.[2024-05-01-preview](/en-us/rest/api/searchservice/search-service-api-versions#2024-05-01-preview). New preview version of the Search REST APIs provides new skills and vectorizers, new binary data type, OneLake files indexer, and new query parameters for more relevant results. See[Upgrade REST APIs](search-api-migration)if you have existing code written against the 2023-07-01-preview and need to migrate to this version.[Azure SDK for Python](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/search/azure-search-documents/CHANGELOG.md),[Azure SDK for .NET](https://github.com/Azure/azure-sdk-for-net/blob/Azure.Search.Documents_11.6.0-beta.4/sdk/search/Azure.Search.Documents/CHANGELOG.md),[Azure SDK for Java](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/CHANGELOG.md)[Python code samples](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/readme.md). New end-to-end samples demonstrate[integration with Cohere Embed v3](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/community-integration/cohere/azure-search-cohere-embed-v3-sample.ipynb),[integration with OneLake and cloud data platforms on Google and AWS](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/conference-demos/ignite-2024/azure-ai-search-e2e-build-demo.ipynb), and[integration with Azure Vision multimodal APIs](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/embeddings/multimodal-embeddings/multimodal-embeddings.ipynb).[Security update addressing information disclosure](https://msrc.microsoft.com/update-guide/vulnerability/CVE-2024-29063). GET responses[no longer return connection strings or keys](search-api-migration#breaking-changes-for-client-code-that-reads-connection-information). Applies to GET Skillset, GET Index, and GET Indexer. This change helps protect your Azure assets integrated with AI Search from unauthorized access.[2024-03-01-preview Search REST API](/en-us/rest/api/searchservice/search-service-api-versions#2024-03-01-preview)[2024-03-01-preview Management REST API](/en-us/rest/api/searchmanagement/operation-groups?view=rest-searchmanagement-2024-03-01-preview&preserve-view=true)[2023-07-01-preview deprecation announcement](/en-us/rest/api/searchservice/search-service-api-versions#2023-07-01-preview). This version is no longer supported as of July 8, 2024. Newer API versions have a different vector configuration. You should[migrate to a newer version](search-api-migration)as soon as possible.[Basic and Standard tiers](search-limits-quotas-capacity#service-limits)offer more storage per partition, at the same per-partition billing rate. Extra capacity is subject to[regional availability](search-limits-quotas-capacity#service-limits)and applies to new search services created after April 3, 2024. Basic now supports up to three partitions and three replicas.[Vector quotas are higher](search-limits-quotas-capacity#vector-index-size-limits)on new services created after April 3, 2024 in selected regions.[Vector quantization, narrow vector data types, and a new](vector-search-how-to-configure-compression-storage). Collectively, these three features minimize storage and costs.`stored`

property (preview)`3072`

, up from `2048`

.## Previous year's announcements

## Service rebrand

This service has had multiple names over the years. Here they are in reverse chronological order:

**Azure AI Search**(November 2023) Renamed to align with Foundry Tools and customer expectations.**Azure Cognitive Search**(October 2019) Renamed to reflect the expanded (yet optional) use of cognitive skills and AI processing in service operations.**Azure Search**(March 2015) The original name.

## Service updates

You can find [service update announcements](https://azure.microsoft.com/updates/?product=search&status=all) for Azure AI Search on the Azure website.

## Feature rename

Semantic search was renamed to [semantic ranker](semantic-search-overview) in November 2023 to better describe the feature, which provides L2 ranking of an existing result set.