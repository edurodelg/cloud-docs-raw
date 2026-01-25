---
merged_at: 2026-01-25T02:11:57.910028
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: samples-rest.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/samples-rest -->

# REST samples for Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn about REST API samples that demonstrate the functionality and workflow of an Azure AI Search solution. These samples use the [Search Service REST APIs](/en-us/rest/api/searchservice).

REST is the definitive programming interface for Azure AI Search, offering a language-agnostic way to interact with the service. For this reason, most examples in our documentation use the REST APIs to demonstrate and explain important concepts.

You can use any client that supports HTTP calls. To learn how to formulate the HTTP request using Visual Studio Code with the REST Client extension, see the REST portion of [Quickstart: Full-text search](search-get-started-text).

## Doc samples

Code samples from the Azure AI Search team demonstrate features and workflows. The following samples are referenced in tutorials, quickstarts, and how-to articles. You can find these samples in [Azure-Samples/azure-search-rest-samples](https://github.com/Azure-Samples/azure-search-rest-samples) on GitHub.

| Sample | Article | Description |
|---|---|---|
|

[Quickstart: Agentic retrieval](search-get-started-agentic-retrieval)[quickstart-keyword-search](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/Quickstart-keyword-search)[Quickstart: Full-text search](search-get-started-text)[quickstart-semantic-ranking](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/Quickstart-semantic-ranking)[Quickstart: Semantic ranking](search-get-started-semantic)[quickstart-vectors](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/Quickstart-vectors)[Quickstart: Vector search](search-get-started-vector)[acl](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/acl)[Query-time ACL and RBAC enforcement](search-query-access-control-rbac-enforcement)[custom-analyzers](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/custom-analyzers)[Tutorial: Create a custom analyzer for phone numbers](tutorial-create-custom-analyzer)[debug-sessions](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/debug-sessions)[Tutorial: Fix a skillset using Debug Sessions](cognitive-search-tutorial-debug-sessions)[index-json-blobs](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/index-json-blobs)[Tutorial: Index JSON blobs from Azure Storage](search-semi-structured-data)[knowledge-store](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/knowledge-store)[Create a knowledge store using REST](knowledge-store-create-rest)[projections](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/projections)[Define projections in a knowledge store](knowledge-store-projections-examples)[skillset-tutorial](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/skillset-tutorial)[Tutorial: AI-generated searchable content from Azure blobs](tutorial-skillset)## Other samples

The following samples are also published by the Azure AI Search team but aren't referenced in documentation. Associated README files provide usage instructions.

| Sample | Description |
|---|---|
|

Tip

Use the [samples browser](/en-us/samples/browse/?expanded=azure&languages=http&products=azure-cognitive-search) to search for Microsoft code samples on GitHub. You can filter your search by product, service, and language.


---

<!-- DOCUMENTO FUSIONADO: samples-java.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/samples-java -->

# Java samples for Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Learn about Java code samples that demonstrate the functionality and workflow of an Azure AI Search solution. These samples use the [Azure AI Search client library](/en-us/java/api/overview/azure/search-documents-readme) for the [Azure SDK for Java](/en-us/azure/developer/java/sdk), which you can explore through the following links.

## SDK samples

Code samples from the Azure SDK development team demonstrate API usage. You can find these samples in [Azure/azure-sdk-for-java/tree/main/sdk/search/azure-search-documents/src/samples](https://github.com/Azure/azure-sdk-for-java/tree/main/sdk/search/azure-search-documents/src/samples) on GitHub.

| Sample | Description |
|---|---|
|

[index](search-what-is-an-index).[Indexer creation](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/src/samples/java/com/azure/search/documents/indexes/CreateIndexerExample.java)[indexer](search-indexer-overview).[Data source creation](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/src/samples/java/com/azure/search/documents/indexes/DataSourceExample.java)[supported data sources](search-indexer-overview#supported-data-sources).[Skillset creation](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/src/samples/java/com/azure/search/documents/indexes/CreateSkillsetExample.java)[skillset](cognitive-search-working-with-skillsets)that's attached to an indexer and perform AI-based enrichment during indexing.[Synonym creation](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/src/samples/java/com/azure/search/documents/SynonymMapsCreateExample.java)[synonym map](search-synonyms).[Load documents](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/src/samples/java/com/azure/search/documents/IndexContentManagementExample.java)[data import](search-what-is-data-import)operation.[Query syntax](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/src/samples/java/com/azure/search/documents/SearchAsyncWithFullyTypedDocumentsExample.java)[basic query](search-query-overview).[Vector search](https://github.com/Azure/azure-sdk-for-java/blob/main/sdk/search/azure-search-documents/src/samples/java/com/azure/search/documents/VectorSearchExample.java)[vector query](vector-search-how-to-query).## Doc samples

Code samples from the Azure AI Search team demonstrate features and workflows. The following samples are referenced in tutorials, quickstarts, and how-to articles that explain the code in detail. You can find these samples in [Azure-Samples/azure-search-java-samples](https://github.com/Azure-Samples/azure-search-java-samples) on GitHub.

| Sample | Article | Description |
|---|---|---|
|

[Quickstart: Full-text search](search-get-started-text)[quickstart-semantic-ranking](https://github.com/Azure-Samples/azure-search-java-samples/tree/main/quickstart-semantic-ranking)[Quickstart: Semantic ranking](search-get-started-semantic)[quickstart-vector-search](https://github.com/Azure-Samples/azure-search-java-samples/tree/main/quickstart-vector-search)[Quickstart: Vector search](search-get-started-vector)Tip

Use the [samples browser](/en-us/samples/browse/?languages=java&products=azure-cognitive-search) to search for Microsoft code samples on GitHub. You can filter your search by product, service, and language.
