---
merged_at: 2026-01-25T03:18:14.065766
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-features-list.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-features-list -->

# Features of Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search provides information retrieval and uses optional AI integration to extract more value from text and vector content.

The following table summarizes features by category. There's feature parity in all Azure public, private, and sovereign clouds, but some features aren't supported in [specific regions](search-region-support) or [specific tiers](search-sku-tier#feature-availability-by-tier).

Note

Looking for preview features? See the [preview features list](search-api-preview).

## Indexing and data extraction

| Category | Features |
|---|---|
| Data sources | Search indexes can accept text from any source, provided it's submitted as a JSON document.
Indexers |
| Hierarchical and nested data structures |
Complex types |

[from Lucene or Microsoft are used to intelligently handle language-specific linguistics including verb tenses, gender, irregular plural nouns (for example, 'mouse' vs. 'mice'), word decompounding, word-breaking (for languages with no spaces), and more.](index-add-language-analyzers)**Language analyzers**[are used for complex query forms such as phonetic matching and regular expressions.](index-add-custom-analyzers)**Custom lexical analyzers**## Chat model and agent integration

| Category | Features |
|---|---|
| Chat completion models used during indexing |
GenAI prompt skill (preview) |

[uses a large language model for query planning, decomposing and paraphrasing complex queries for better query coverage over your index. Responses from agentic retrieval are designed for agent-to-agent workflows. You can pass search results as single large string, which simplifies agent consumption of your proprietary content. The response also includes citations and query execution information.](agentic-retrieval-overview)**Agentic retrieval (preview)**[can be implemented using existing capabilities. The ability to](retrieval-augmented-generation-overview)**RAG patterns**[tune for relevance](search-relevance-overview)and construct hybrid queries improve the quality of the content sent to chat bots for answer generation.## Applied AI and AI enriched content

| Category | Features |
|---|---|
| AI processing during indexing |
AI enrichment |

[built-in skills](cognitive-search-predefined-skills)from Microsoft, such as text translation or Optical Character Recognition (OCR), or

[custom skills](cognitive-search-create-custom-skill-example)that you provide.

[splits up larger passages into smaller chunks that can be vectorized, with vectors routed to dedicated fields in an index for vector and hybrid search.](vector-search-integrated-vectorization)

**Integrated data chunking and vectorization**[are used to encode user query strings into vectors for vector search. You can use the same embedding models for queries that you used for indexing.](vector-search-how-to-configure-vectorizer)**Vectorizers**[is persistent storage of AI enriched or AI generated content, intended for non-search scenarios like knowledge mining and data science workloads. A knowledge store is defined in a skillset, but created in Azure Storage as objects or tabular rowsets.](knowledge-store-concept-intro)**Knowledge store**[refers to cached enrichments that can be reused during skillset execution. Caching is valuable in skillsets that include OCR and image analysis, which are expensive to process.](enrichment-cache-how-to-configure)**Enrichment caching (preview)**## Vector and hybrid retrieval

| Category | Features |
|---|---|
| Vector indexing | Within a search index, add
vector search |

[Formulate single and multiple vector queries](vector-search-how-to-query).[Hierarchical Navigable Small World (HNSW)](vector-search-ranking#about-hnsw)or[exhaustive K-Nearest Neighbors (KNN)](vector-search-ranking#about-exhaustive-knn)to find similar vectors in a search index.[Apply filters before or after query execution](vector-search-filters)for greater precision during information retrieval.[hybrid query request](hybrid-search-how-to-query).[consolidates vector and text search, with optional semantic ranking and relevance tuning for best results.](hybrid-search-overview)**Hybrid search**[Text Split skill](cognitive-search-skill-textsplit). Native vectorization through[vectorizers](vector-search-how-to-configure-vectorizer)and embedding skills such as[Azure OpenAI Embedding](cognitive-search-skill-azure-openai-embedding),[Azure Vision multimodal](cognitive-search-skill-vision-vectorize), and[AML](cognitive-search-aml-skill)that you can use to connect to endpoints in the Microsoft Foundry model catalog.[provides an end-to-end indexing pipeline from source files to queries.](vector-search-integrated-vectorization)**Integrated vectorization**[built-in scalar and binary quantization](vector-search-how-to-quantization)to reduce vector index size in memory and on disk. You can also forego storage of vectors you don't need, or assign narrow data types to vector fields for reduced storage requirements.## Full text and other query forms

| Category | Features |
|---|---|
| Free-form text search |
Full-text search |

[provides logical operators, phrase search operators, suffix operators, precedence operators.](query-simple-syntax)

**Simple query syntax**[includes all operations in simple syntax, with extensions for fuzzy search, proximity search, term boosting, and regular expressions.](query-lucene-syntax)

**Full Lucene query syntax**[is a key benefit of Azure AI Search. Scoring profiles are used to model relevance as a function of values in the documents themselves. For example, you might want newer products or discounted products to appear higher in the search results. You can also build scoring profiles using tags for personalized scoring based on customer search preferences you've tracked and stored separately.](index-add-scoring-profiles)**Simple scoring**[is premium feature that reranks results based on semantic relevance to the query. Depending on your content and scenario, it can significantly improve search relevance with almost minimal configuration or effort.](semantic-search-overview)**Semantic ranker**[filter over and match on geographic coordinates. You can](search-query-odata-geo-spatial-functions)**Geospatial functions**[match on distance](search-query-simple-examples#example-6-geospatial-search)or by inclusion in a polygon shape.[is enabled through a single query parameter. Azure AI Search returns a faceted navigation structure you can use as the code behind a categories list, for self-directed filtering (for example, to filter catalog items by price-range or brand).](search-faceted-navigation)**Faceted navigation**[can be used to incorporate faceted navigation into your application's UI, enhance query formulation, and filter based on user- or developer-specified criteria. Create filters using the OData syntax.](query-odata-filter-orderby-syntax)**Filters**[can be enabled for type-ahead queries in a search bar.](search-add-autocomplete-suggestions)**Autocomplete**[also works off of partial text inputs in a search bar, but the results are actual documents in your index rather than query terms.](/en-us/rest/api/searchservice/suggesters)**Search suggestions**[associates equivalent terms that implicitly expand the scope of a query, without the user having to provide the alternate terms.](search-synonyms)**Synonyms**[applies text formatting to a matching keyword in search results. You can choose which fields return highlighted snippets.](/en-us/rest/api/searchservice/documents/search-post)**Hit highlighting**[is offered for multiple fields via the index schema and then toggled at query-time with a single search parameter.](/en-us/rest/api/searchservice/documents/search-post)**Sorting**[and throttling your search results is straightforward with the finely tuned control that Azure AI Search offers over your search results.](search-pagination-page-layout)**Paging**## Security features

| Category | Features |
|---|---|
| Network security |
IP rules for inbound firewall support |

[using Azure Private Link to force all requests through a virtual network.](service-create-private-endpoint)

**Create a private endpoint**[support allows you to join Azure AI Search to a network security perimeter that includes other Azure resources so that you can manage network access holistically.](search-security-network-security-perimeter)

**Network security perimeter**[is built into the internal storage layer and is irrevocable.](search-security-overview#encryption)**Microsoft-managed encryption-at-rest**[that you create and manage in Azure Key Vault can be used for supplemental encryption of indexes and synonym maps. For services created after August 1 2020, CMK encryption extends to data on temporary disks, for full double encryption of indexed content.](search-security-manage-encryption-keys)**Customer-managed encryption keys (CMK)**[assigns roles to users and groups in Microsoft Entra ID for controlled access to search content and operations. You can also use](search-security-rbac)**Role-based access control**[if you don't want to use role assignments.](search-security-api-keys)**key-based authentication**[filters out search results that a user isn't authorized to see. For several data sources, if the data source provides an access control model, you can configure an index to inherit the user permission metadata.](search-document-level-access-overview)**Document-level access control (preview)**[allows an indexer to connect to Azure resources that are protected through Azure Private Link.](search-indexer-howto-access-private)**Data connections through private endpoints**[authenticates connections to Azure resources using a Microsoft Entra security principal, which eliminates storage and passing of hardcoded API keys.](search-how-to-managed-identities)**Data connections through managed identities**[means that connection strings to external data sources can omit user names and passwords. When an indexer connects to the data source, the resource allows the connection if the search service was previously registered as a trusted service (applies to Azure Storage only).](search-how-to-managed-identities)**Data access using a trusted identity**## Portal features

| Category | Features |
|---|---|
| Tools for prototyping and inspection |
Add index |

[creates indexes, indexers, skillsets, and data source definitions. If your data exists in Azure, this wizard can save you significant time and effort, especially for proof-of-concept investigation and exploration.](search-import-data-portal)

**Import data**wizard[creates a full indexing pipeline that includes data chunking and vectorization. The wizard creates all of the objects and configuration settings.](search-get-started-portal-import-vectors)

**Import data (new)**wizard[is used to test queries and refine scoring profiles.](search-explorer)

**Search explorer**[is used to generate an HTML page that can be used to test the search experience.](search-create-app-portal)

**Create demo app**[is a visual editor that lets you debug a skillset interactively. It shows you dependencies, output, and transformations.](cognitive-search-debug-session)

**Debug Sessions**[to go beyond the metrics-at-a-glance that are always visible in the Azure portal. Metrics on queries per second, latency, and throttling are captured and reported in portal pages with no extra configuration required.](monitor-azure-cognitive-search)**Enable monitoring features**## Programmability

| Category | Features |
|---|---|
| REST |
Service REST API |

[is for service creation and provisioning through Azure Resource Manager. You can also use this API to manage keys and capacity.](/en-us/rest/api/searchmanagement/)

**Management REST API**[is for data plane operations, including all operations related to indexing, queries, and AI enrichment. You can also use this client library to retrieve system information and statistics.](/en-us/dotnet/api/overview/azure/search.documents-readme)**Azure.Search.Documents**[is for service creation and provisioning through Azure Resource Manager. You can also use this API to manage keys and capacity.](/en-us/dotnet/api/microsoft.azure.management.search)**Microsoft.Azure.Management.Search**[is for data plane operations, including all operations related to indexing, queries, and AI enrichment. You can also use this client library to retrieve system information and statistics.](/en-us/java/api/com.azure.search.documents)**com.azure.search.documents**[is for service creation and provisioning through Azure Resource Manager. You can also use this API to manage keys and capacity.](/en-us/java/api/overview/azure/search/management)**com.microsoft.azure.management.search**[is for data plane operations, including all operations related to indexing, queries, and AI enrichment. You can also use this client library to retrieve system information and statistics.](/en-us/python/api/overview/azure/search-documents-readme)**azure-search-documents**[is for service creation and provisioning through Azure Resource Manager. You can also use this API to manage keys and capacity.](/en-us/python/api/azure-mgmt-search/)**azure-mgmt-search**[is for data plane operations, including all operations related to indexing, queries, and AI enrichment. You can also use this client library to retrieve system information and statistics.](/en-us/javascript/api/@azure/search-documents/)**azure/search-documents**[is for service creation and provisioning through Azure Resource Manager. You can also use this API to manage keys and capacity.](/en-us/javascript/api/@azure/arm-search/)**azure/arm-search**


---

<!-- DOCUMENTO FUSIONADO: search-indexer-securing-resources.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-indexer-securing-resources -->

# Indexer access to content protected by Azure network security

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If your Azure resources are deployed in an Azure virtual network, this concept article explains how a search indexer can access content that's protected by network security. It describes the outbound traffic patterns and indexer execution environments. It also covers the network protections supported by Azure AI Search and factors that might influence your security strategy. Finally, because Azure Storage is used for both data access and persistent storage, this article also covers network considerations that are specific to [search and storage connectivity](#access-to-a-network-protected-storage-account).

Looking for step-by-step instructions instead? See [How to configure firewall rules to allow indexer access](search-indexer-howto-access-ip-restricted) or [How to make outbound connections through a private endpoint](search-indexer-howto-access-private).

## Resources accessed by indexers

Azure AI Search indexers can make outbound calls to various Azure resources in three situations:

- Connections to external data sources during indexing
- Connections to external, encapsulated code through a skillset that includes custom skills
- Connections to Azure Storage during skillset execution to cache enrichments, save debug session state, or write to a knowledge store

A list of all possible Azure resource types that an indexer might access in a typical run are listed in the table below.

| Resource | Purpose within indexer run |
|---|---|
| Azure Storage (blobs, ADLS Gen 2, files, tables) | Data source |
| Azure Storage (blobs, tables) | Skillsets (caching enrichments, debug sessions, knowledge store projections) |
| Azure Cosmos DB (various APIs) | Data source |
| Azure SQL Database | Data source |
| Microsoft OneLake | Data source |
| SQL Server on Azure virtual machines | Data source |
| SQL Managed Instance | Data source |
| Azure Functions | Attached to a skillset and used to host for custom web API skills |

Note

An indexer also connects to Foundry Tools for built-in skills. However, that connection is made over the internal network and isn't subject to any network provisions under your control.

Indexers connect to resources using the following approaches:

- A public endpoint with credentials
- A private endpoint, using Azure Private Link
- Connect as a trusted service
- Connect through IP addressing

If your Azure resource is on a virtual network, you should use either a private endpoint or IP addressing to admit indexer connections to the data.

## Supported network protections

Your Azure resources could be protected using any number of the network isolation mechanisms offered by Azure. Depending on the resource and region, Azure AI Search indexers can make outbound connections through IP firewalls and private endpoints, subject to the limitations indicated in the following table.

| Resource | IP restriction | Private endpoint |
|---|---|---|
| Azure Storage for text-based indexing (blobs, ADLS Gen 2, files, tables) | Supported only if the storage account and search service are in different regions. | Supported |
| Azure Storage for AI enrichment (caching, debug sessions, knowledge store) | Supported only if the storage account and search service are in different regions. | Supported |
| Azure Cosmos DB for NoSQL | Supported | Supported |
| Azure Cosmos DB for MongoDB | Supported | Unsupported |
| Azure Cosmos DB for Apache Gremlin | Supported | Unsupported |
| Azure SQL Database | Supported | Supported |
| SQL Server on Azure virtual machines | Supported | N/A |
| SQL Managed Instance | Supported | N/A |
| Azure Functions | Supported | Supported, only for certain tiers of Azure functions |

## Network access and indexer execution environments

Azure AI Search has the concept of an [ indexer execution environment](search-howto-run-reset-indexers#indexer-execution-environment) that optimizes processing based on the characteristics of the job. There are two environments. If you're using an IP firewall to control access to Azure resources, knowing about execution environments will help you set up an IP range that is inclusive of both environments.

For any given indexer run, Azure AI Search determines the best environment in which to run the indexer. Depending on the number and types of tasks assigned, the indexer will run in one of two environments/

| Execution environment | Description |
|---|---|
Private 1 |
Internal to a search service. Indexers running in the private environment share computing resources with other indexing and query workloads on the same search service. If you set up a private connection between an indexer and your data, such as a shared private link, this is the only execution environment you can use and it's used automatically. |
| multitenant | Managed and secured by Microsoft at no extra cost. It isn't subject to any network provisions under your control. This environment is used to offload computationally intensive processing, leaving service-specific resources available for routine operations. Examples of resource-intensive indexer jobs include skillsets, processing large documents, or processing a high volume of documents. |

1 To prevent heavy load on the private execution environment, indexers with more than 2 Azure OpenAI Embedding or Azure Vision multimodal embeddings skills will be restricted from running in this environment.

### Setting up IP ranges for indexer execution

This section explains IP firewall configuration for admitting requests from either execution environment.

If your Azure resource is behind a firewall, set up [inbound rules that admit indexer connections](search-indexer-howto-access-ip-restricted) for all of the IPs from which an indexer request can originate. This includes the IP address used by the search service, and the IP addresses used by the multitenant environment.

To obtain the IP address of the search service (and the private execution environment), use

`nslookup`

(or`ping`

) to find the fully qualified domain name (FQDN) of your search service. The FQDN of a search service in the public cloud would be`<service-name>.search.windows.net`

.To obtain the IP addresses of the multitenant environments within which an indexer might run, use the

`AzureCognitiveSearch`

service tag.[Azure service tags](/en-us/azure/virtual-network/service-tags-overview)have a published range of IP addresses of the multitenant environments for each region. You can find these IPs using the[discovery API](/en-us/azure/virtual-network/service-tags-overview#use-the-service-tag-discovery-api)or a[downloadable JSON file](/en-us/azure/virtual-network/service-tags-overview#discover-service-tags-by-using-downloadable-json-files). IP ranges are allocated by region, so check your search service region before you start.

#### Setting up IP rules for Azure SQL

When setting the IP rule for the multitenant environment, certain SQL data sources support a simple approach for IP address specification. Instead of enumerating all of the IP addresses in the rule, you can create a [Network Security Group rule](/en-us/azure/virtual-network/network-security-groups-overview) that specifies the `AzureCognitiveSearch`

service tag.

You can specify the service tag if your data source is either:

Notice that if you specified the service tag for the multitenant environment IP rule, you'll still need an explicit inbound rule for the private execution environment (meaning the search service itself), as obtained through `nslookup`

.

## Choose a connectivity approach

A search service can't be provisioned into a specific virtual network, running natively on a virtual machine. Although some Azure resources offer [virtual network service endpoints](/en-us/azure/virtual-network/virtual-network-service-endpoints-overview), this functionality won't be offered by Azure AI Search. You should plan on implementing one of the following approaches.

| Approach | Details |
|---|---|
| Secure the inbound connection to your Azure resource | Configure an inbound firewall rule on your Azure resource that admits indexer requests for your data. Your firewall configuration should include the service tag for multitenant execution and the IP address of your search service. See
|

[Make outbound connections through a private endpoint](search-indexer-howto-access-private).Connections through a private endpoint must originate from the search service's private execution environment.

Configuring an IP firewall is free. A private endpoint, which is based on Azure Private Link, has a billing impact. See [Azure Private Link pricing](https://azure.microsoft.com/pricing/details/private-link/) for details.

After you configure network security, follow up with role assignments that specify which users and groups have read and write access to your data and operations.

### Considerations for using a private endpoint

This section narrows in on the private connection option.

- A shared private link requires a billable search service, where the minimum tier is either Basic for text-based indexing or Standard 2 (S2) for skills-based indexing. See
[tier limits on the number of private endpoints](search-limits-quotas-capacity#shared-private-link-resource-limits)for details.

Once a shared private link is created, the search service always uses it for every indexer connection to that specific Azure resource. The private connection is locked and enforced internally. You can't bypass the private connection for a public connection.

Requires a billable Azure Private Link resource.

Requires that a subscription owner approve the private endpoint connection.

Requires that you turn off the multitenant execution environment for the indexer.

You do this by setting the

`executionEnvironment`

of the indexer to`"Private"`

. This step ensures that all indexer execution is confined to the private environment provisioned within the search service. This setting is scoped to an indexer and not the search service. If you want all indexers to connect over private endpoints, each one must have the following configuration:`{ "name" : "myindexer", ... other indexer properties "parameters" : { ... other parameters "configuration" : { ... other configuration properties "executionEnvironment": "Private" } } }`


Once you have an approved private endpoint to a resource, indexers that are set to be *private* attempt to obtain access via the private link that was created and approved for the Azure resource.

Azure AI Search will validate that callers of the private endpoint have appropriate role assignments. For example, if you request a private endpoint connection to a storage account with read-only permissions, this call will be rejected.

If the private endpoint isn't approved, or if the indexer didn't use the private endpoint connection, you'll find a `transientFailure`

error message in indexer execution history.

## Supplement network security with token authentication

Firewalls and network security are a first step in preventing unauthorized access to data and operations. Authorization should be your next step.

We recommend role-based access, where Microsoft Entra ID users and groups are assigned to roles that determine read and write access to your service. See [Connect to Azure AI Search using role-based access controls](search-security-rbac) for a description of built-in roles and instructions for creating custom roles.

If you don't need key-based authentication, we recommend that you disable API keys and use role assignments exclusively.

## Access to a network-protected storage account

A search service stores indexes and synonym lists. For other features that require storage, Azure AI Search takes a dependency on Azure Storage. Enrichment caching, debug sessions, and knowledge stores fall into this category. The location of each service, and any network protections in place for storage, will determine your data access strategy.

### Same-region services

In Azure Storage, access through a firewall requires that the request originates from a different region. If Azure Storage and Azure AI Search are in the same region, you can bypass the IP restrictions on the storage account by accessing data under the system identity of the search service.

There are two options for supporting data access using the system identity:

Configure search to run as a

[trusted service](search-indexer-howto-access-trusted-service-exception)and use the[trusted service exception](/en-us/azure/storage/common/storage-network-security#trusted-access-based-on-a-managed-identity)in Azure Storage.Configure a

[resource instance rule](/en-us/azure/storage/common/storage-network-security#grant-access-from-azure-resource-instances)in Azure Storage that admits inbound requests from an Azure resource.

The above options depend on Microsoft Entra ID for authentication, which means that the connection must be made with a Microsoft Entra login. Currently, only an Azure AI Search [system-assigned managed identity](search-how-to-managed-identities#create-a-system-managed-identity) is supported for same-region connections through a firewall.

### Services in different regions

When search and storage are in different regions, you can use the previously mentioned options or set up IP rules that admit requests from your service. Depending on the workload, you might need to set up rules for multiple execution environments as described in the next section.

## Next steps

Now that you're familiar with indexer data access options for solutions deployed in an Azure virtual network, review either of the following how-to articles as your next step:
