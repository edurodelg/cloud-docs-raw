---
merged_at: 2026-01-25T02:11:58.446691
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-integrated-vectorization.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-integrated-vectorization -->

# Integrated vector embedding in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Integrated vectorization is an extension of the indexing and query pipelines in Azure AI Search. It adds the following capabilities:

- Vector encoding during indexing
- Vector encoding during queries

[Data chunking](vector-search-how-to-chunk-documents) isn't a hard requirement, but unless your raw documents are small, chunking is necessary for meeting the token input requirements of embedding models.

Vector conversions are one-way: nonvector-to-vector. For example, there's no vector-to-text conversion for queries or results, such as converting a vector result to a human-readable string, which is why indexes contain both vector and nonvector fields.

Integrated vectorization speeds up the development and minimizes maintenance tasks during data ingestion and query time because there are fewer operations that you have to implement manually. This capability is now generally available.

## Using integrated vectorization during indexing

For integrated data chunking and vector conversions, you're taking a dependency on the following components:

[An indexer](search-indexer-overview), which retrieves raw data from a[supported data source](search-indexer-overview#supported-data-sources)and drives the pipeline engine.[A search index](search-what-is-an-index)to receive the chunked and vectorized content.[A skillset](cognitive-search-working-with-skillsets)configured for:[Text Split skill](cognitive-search-skill-textsplit), used to chunk the data.An embedding skill, used to generate vector arrays, which can be any of the following:

[AzureOpenAIEmbedding skill](cognitive-search-skill-azure-openai-embedding), attached to text-embedding-ada-002,text-embedding-3-small, text-embedding-3-large on Azure OpenAI.[Custom skill](cognitive-search-custom-skill-web-api)that points to another embedding model on Azure or on another site.[Azure Vision multimodal embeddings skill (preview)](cognitive-search-skill-vision-vectorize)that points to the multimodal API for Azure Vision.[AML skill](cognitive-search-aml-skill)that points to select models in the Microsoft Foundry model catalog.


## Using integrated vectorization in queries

For text-to-vector conversion during queries, you take a dependency on these components:

A query that specifies one or more vector fields.

A text string that's converted to a vector at query time.

[A vectorizer](vector-search-how-to-configure-vectorizer), defined in the index schema, assigned to a vector field, and used automatically at query time to convert a text query to a vector. The vectorizer you set up must match the embedding model used to encode your content.

## Component diagram

The following diagram shows the components of integrated vectorization.

The workflow is an indexer pipeline. Indexers retrieve data from supported data sources and initiate data enrichment (or applied AI) by calling Azure OpenAI or Foundry Tools or custom code for text-to-vector conversions or other processing.

The diagram focuses on integrated vectorization, but your solution isn't limited to this list. You can add more skills for AI enrichment, create a knowledge store, add semantic ranking, add relevance tuning, and other query features.

## Availability and pricing

Integrated vectorization is available in all regions and tiers. However, if you're using skills and vectorizers for AI enrichment, regional requirements might apply. For more information, see [Attach a Foundry resource to a skillset](cognitive-search-attach-cognitive-services).

If you're using a custom skill and an Azure hosting mechanism (such as an Azure function app, Azure Web App, and Azure Kubernetes), check the [Azure product by region page](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/?products=search) for feature availability.

Data chunking (Text Split skill) is free and available on all Foundry Tools in all regions.

Note

Some older search services created before January 1, 2019 are deployed on infrastructure that doesn't support vector workloads. If you try to add a vector field to a schema and get an error, it's a result of outdated services. In this situation, you must create a new search service to try out the vector feature.

## What scenarios can integrated vectorization support?

Subdivide large documents into chunks, useful for vector and nonvector scenarios. For vectors, chunks help you meet the input constraints of embedding models. For nonvector scenarios, you might have a chat-style search app where GPT is assembling responses from indexed chunks. You can use vectorized or nonvectorized chunks for chat-style search.

Build a vector store where all of the fields are vector fields, and the document ID (required for a search index) is the only string field. Query the vector store to retrieve document IDs, and then send the document's vector fields to another model.

Combine vector and text fields for hybrid search, with or without semantic ranking. Integrated vectorization simplifies all of the

[scenarios supported by vector search](vector-search-overview#what-scenarios-can-vector-search-support).

## How to use integrated vectorization

For query-only vectorization:

[Add a vectorizer](vector-search-how-to-configure-vectorizer#define-a-vectorizer-and-vector-profile)to an index. It should be the same embedding model used to generate vectors in the index.[Assign the vectorizer](vector-search-how-to-configure-vectorizer#define-a-vectorizer-and-vector-profile)to a vector profile, and then assign a vector profile to the vector field.[Formulate a vector query](vector-search-how-to-configure-vectorizer#test-a-vectorizer)that specifies the text string to vectorize.

A more common scenario - data chunking and vectorization during indexing:

[Create a data source](search-howto-create-indexers#prepare-a-data-source)connection to a supported data source for indexer-based indexing.[Create a skillset](cognitive-search-defining-skillset)that calls[Text Split skill](cognitive-search-skill-textsplit)for chunking and[Azure OpenAI Embedding](cognitive-search-skill-azure-openai-embedding)or another embedding skill to vectorize the chunks.[Create an index](search-how-to-create-search-index)that specifies a[vectorizer](vector-search-how-to-configure-vectorizer)for query time, and assign it to vector fields.[Create an indexer](search-howto-create-indexers)to drive everything, from data retrieval, to skillset execution, through indexing. We recommend running the indexer[on a schedule](search-howto-schedule-indexers)to pick up changed documents or any documents that were missed due to throttling.

Optionally, [create secondary indexes](index-projections-concept-intro) for advanced scenarios where chunked content is in one index, and nonchunked in another index. Chunked indexes (or secondary indexes) are useful for RAG apps.

Tip

[Try the Import data (new) wizard](search-get-started-portal-import-vectors) in the Azure portal to explore integrated vectorization before writing any code.

### Secure connections to vectorizers and models

If your architecture requires private connections that bypass the internet, you can create a [shared private link connection](search-indexer-howto-access-private) to the embedding models used by skills during indexing and vectorizers at query time.

Shared private links only work for Azure-to-Azure connections. If you're connecting to OpenAI or another external model, the connection must be over the public internet.

For vectorization scenarios, you would use:

`openai_account`

for embedding models hosted on an Azure OpenAI resource.`sites`

for embedding models accessed as a[custom skill](cognitive-search-custom-skill-interface)or[custom vectorizer](vector-search-vectorizer-custom-web-api). The`sites`

group ID is for App services and Azure functions, which you could use to host an embedding model that isn't one of the Azure OpenAI embedding models.

## Benefits

Here are some of the key benefits of the integrated vectorization:

No separate data chunking and vectorization pipeline. Code is simpler to write and maintain.

Automate indexing end-to-end. When data changes in the source (such as in Azure Storage, Azure SQL, or Cosmos DB), the indexer can move those updates through the entire pipeline, from retrieval, to document cracking, through optional AI-enrichment, data chunking, vectorization, and indexing.

Batching and retry logic is built in (non-configurable). Azure AI Search has internal retry policies for throttling errors that surface due to the Azure OpenAI endpoint maxing out on token quotas for the embedding model. We recommend putting the indexer on a schedule (for example, every 5 minutes) so the indexer can process any calls that are throttled by the Azure OpenAI endpoint despite of the retry policies.

Projecting chunked content to secondary indexes. Secondary indexes are created as you would any search index (a schema with fields and other constructs), but they're populated in tandem with a primary index by an indexer. Content from each source document flows to fields in primary and secondary indexes during the same indexing run.

Secondary indexes are intended for question and answer or chat style apps. The secondary index contains granular information for more specific matches, but the parent index has more information and can often produce a more complete answer. When a match is found in the secondary index, the query returns the parent document from the primary index. For example, assuming a large PDF as a source document, the primary index might have basic information (title, date, author, description), while a secondary index has chunks of searchable content.


## Limitations

Make sure you know the [Azure OpenAI quotas and limits for embedding models](/en-us/azure/ai-services/openai/quotas-limits). Azure AI Search has retry policies, but if the quota is exhausted, retries fail.

Azure OpenAI token-per-minute limits are per model, per subscription. Keep this in mind if you're using an embedding model for both query and indexing workloads. If possible, [follow best practices](/en-us/azure/ai-services/openai/quotas-limits#general-best-practices-to-remain-within-rate-limits). Have an embedding model for each workload, and try to deploy them in different subscriptions.

On Azure AI Search, remember there are [service limits](search-limits-quotas-capacity) by tier and workloads.


---

<!-- DOCUMENTO FUSIONADO: search-query-access-control-rbac-enforcement.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-access-control-rbac-enforcement -->

# Query-time ACL and RBAC enforcement in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Query-time access control ensures that users only retrieve search results they're authorized to access, based on their identity, group memberships, roles, or attributes. This functionality is essential for secure enterprise search and compliance-driven workflows.

Authorized access depends on permission metadata that's ingested during indexing. For indexer data sources that have built-in access models, such as Azure Data Lake Storage (ADLS) Gen2 and SharePoint in Microsoft 365, an indexer can pull in the permission metadata for each document automatically. For other data sources, you must assemble the document payload yourself, and the payload must include both content and the associated permission metadata. You then use the [push APIs](search-index-access-control-lists-and-rbac-push-api) to load the index.

This article explains how to set up queries that use permission metadata to filter results.

## Prerequisites

Permission metadata must be in

`filterable`

string fields. You won't use the filter in your queries, but the search engine builds a filter internally to exclude unauthorized content.Permission metadata must consist of either POSIX-style permissions that identify the level of access and the group or user ID, or the resource ID of the container in ADLS Gen2 if you're using RBAC scope.

Depending on the data source:

- For ADLS Gen2 data sources, you must have configured Access Control Lists (ACLs) and/or Azure role-based access control (RBAC) roles at the container level.
- For Azure Blob data sources, you must have role assignments on the container. You can use a
[built-in indexer](search-indexer-access-control-lists-and-role-based-access), a[knowledge source](agentic-knowledge-source-how-to-blob), or[Push APIs](search-index-access-control-lists-and-rbac-push-api)to index permission metadata in your index. - For SharePoint data sources, you must have configured Access Control Lists (ACLs). You can use a
[built-in SharePoint indexer](search-how-to-index-sharepoint-online)and configure it with[ACL ingestion capabilities](search-indexer-sharepoint-access-control-lists).

Use the

[latest preview REST API](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true)or a preview package of an Azure SDK to query the index or knowledge source. This API version supports internal queries that filter out unauthorized results.

## Limitations

If ACL evaluation fails (for example, the Graph API is unavailable), the service returns

**5xx**and does**not**return a partially filtered result set.Document visibility requires both:

- the calling application’s RBAC role (Authorization header)
- the user identity carried by
**x-ms-query-source-authorization**

Initial ACL-based queries may experience higher latency compared to subsequent requests, due to caching and permission resolution overhead.


## ACL entry limits per data source

Access Control List (ACL) entry limits define how many distinct permission records can be associated with a file, folder, or item within a connected data source. Each entry represents a single user or group identity and the access rights granted to that identity (for example, Read, Write, or Execute).

The maximum number of ACL entries supported by Azure AI Search functionality varies depending on the data source type:

Azure Data Lake Storage Gen2 (ADLS Gen2):
Each file or directory can have up to [32 ACL entries permissions](/en-us/azure/storage/blobs/data-lake-storage-access-control). In this context, an entry means a single principal (user or group) with a specific permission set. Example: assigning "Everyone" read access and "Azure users" execute access would count as two ACL entries.

SharePoint in Microsoft 365:
SharePoint data source in search supports up to 1,000 permission entries per file. Each entry represents a unique user or group assignment in the item’s permission list. This is distinct from the overall [unique permission scopes limits](/en-us/office365/servicedescriptions/sharepoint-online-service-description/sharepoint-online-limits#unique-security-scopes-per-list-or-library) per list or library, which governs how many items can have unique permissions.

These limits determine how granularly Azure AI Search can honor item-level permissions when indexing or filtering search results. If an item exceeds these ACL entry limits, permissions beyond the limit may not be enforced at query time.

## How query-time enforcement works

This section lists the order of operations for ACL enforcement at query time. Operations vary depending on whether you use Azure RBAC scope or Microsoft Entra ID group or user IDs.

### 1. User permissions input

The end-user application includes a query access token as part of the search query request, and that access token is typically the identity of the user. The following table lists the source of the user permissions supported by Azure AI Search for ACL enforcement:

| Permission type | Source |
|---|---|
| userIds | `oid` from `x-ms-query-source-authorization` token |
| groupIds | Group membership fetched using the
|

`x-ms-query-source-authorization`

has on a storage container### 2. Security filter construction

Internally, Azure AI Search dynamically constructs security filters based on the user permissions provided. These security filters are automatically appended to any filters that might come in with the query if the index has the permission filter option enabled.

For Azure RBAC, permissions are lists of resource ID strings. There must be an Azure role assignment (Storage Blob Data Reader) on the data source that grants access to the security principal token in the authorization header. The filter excludes documents if there's no role assignment for the principal behind the access token on the request.

### 3. Results filtering

The security filter efficiently matches the userIds, groupIds, and rbacScope from the request against each list of ACLs in every document in the search index to limit the results returned to ones the user has access to. It's important to note that each filter is applied independently and a document is considered authorized if any filter succeeds. For example, if a user has access to a document through userIds but not through groupIds, the document is still considered valid and returned to the user.

## Query example

Here's an example of a query request from [sample code](https://github.com/Azure-Samples/azure-search-rest-samples/tree/main/acl). The query token is passed in the request header. The query token is the personal access token of a user or a group identity behind the request.

```
POST {{endpoint}}/indexes/stateparks/docs/search?api-version=2025-11-01-preview
Authorization: Bearer {{query-token}}
x-ms-query-source-authorization: {{query-token}}
Content-Type: application/json
{
"search": "*",
"select": "name,description,location,GroupIds",
"orderby": "name asc"
}
```


Note

If the query token is omitted, only public documents accessible to everyone are returned in the query request.

## Elevated permissions for investigating incorrect results

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Debugging queries that include permission metadata can be problematic because search results are specific to each user. As a developer or administrator, you might need elevated permissions to return results regardless of the permission metadata so that you can investigate problems with queries returning unauthorized content.

To investigate, you must be able to:

View the set of documents that the end user is able to view based on that user's permissions.

View all documents in the index to investigate why some might not be visible to the end user.


You can accomplish these tasks by adding a custom header, `x-ms-enable-elevated-read: true`

, to a query.

### Permissions for elevated-read requests

You must have [Search Index Data Contributor](search-security-rbac#built-in-roles-used-in-search) permissions or a [custom role](search-security-rbac#create-a-custom-role) that includes the Elevate Read permission.

Queries are a data plane operation, so the custom role can only consist of atomic data plane permissions. For a custom role, add the `Microsoft.Search/searchServices/indexes/contentSecurity/elevatedOperations/read`

permission.

### Add an elevated-read header to a query

After you set up permissions, you can run the query. The following example is a query request against a search index.

```
POST {endpoint}/indexes('{indexName}')/search.post.search?api-version=2025-11-01-preview
Authorization: Bearer {AUTH_TOKEN}
x-ms-query-source-authorization: Bearer {TOKEN}
x-ms-enable-elevated-read: true
{
"search": "prototype tests",
"select": "filename, author, date",
"count": true
}
```


Important

The `x-ms-enable-elevated-read`

header only works on Search POST actions. You can't perform an elevated read query on a [knowledge base retrieve](/en-us/rest/api/searchservice/knowledge-retrieval/retrieve?view=rest-searchservice-2025-11-01-preview&preserve-view=true) action.

### Important ACL functionality behavior change in specific preview API versions

Before REST API version `2025-11-01-preview`

, earlier preview versions `2025-05-01-preview`

and `2025-08-01-preview`

returned all documents when using a service API key or authorized Entra roles, even if no user token was provided. Applications that didn’t validate the presence of a user token could inadvertently expose results to end users if not implemented correctly or following best practices.

Starting in November 2025, this behavior changed:

- ACL permission filters now apply even when using only service API keys or Entra authentication across all versions that support ACL.
- If the user token is omitted, ACL-protected content isn't returned.
- To view all documents for troubleshooting, you must explicitly include the elevated-read header when using REST API version
`2025-11-01-preview`

.

This update helps keep content protected when applications don’t enforce best practices for token validation.
