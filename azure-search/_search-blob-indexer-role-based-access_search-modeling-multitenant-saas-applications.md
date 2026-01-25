---
merged_at: 2026-01-25T02:11:58.464565
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-blob-indexer-role-based-access.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-blob-indexer-role-based-access -->

# Use a blob indexer or knowledge source to ingest RBAC scopes metadata

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Azure Storage allows for role-based access on containers in blob storage, where roles like **Storage Blob Data Reader** or **Storage Blob Data Contributor** determine whether someone has access to content. Preview APIs in Azure AI Search now support ingestion of user permissions alongside document ingestion so that you can use those permissions to control access to search results. If a user lacks permissions on a specific directory or file in Azure Storage, that user doesn't have access to the corresponding documents in Azure AI Search results, even if you personally have a **Search Index Data Reader** assignment *on the index*.

- 2025-05-01-preview and later, RBAC scopes metadata can be ingested using the
[Blob indexer](search-how-to-index-azure-data-lake-storage). - 2025-11-01-preview provides equivalent support for
[Blob knowledge sources](agentic-knowledge-source-how-to-blob)in Azure Storage.

RBAC scope is set at the container level and flows to all blobs (documents) through permission inheritance. RBAC scope is captured during indexing as permission metadata. You can use the push APIs to upload and index content and permission metadata manually (see [Indexing Permissions using the push REST API](search-index-access-control-lists-and-rbac-push-api)), or you can use an indexer or knowledge source to automate data ingestion. This article focuses on indexing automation.

At query time, the identity of the caller is included in the request header via the `x-ms-query-source-authorization`

parameter. The identity must match the permission metadata on documents if the user is to see the search results.

This article focuses on the indexing automation approaches, built on this foundation:

[Azure Storage blobs secured using role-based access control (Azure RBAC)](/en-us/azure/storage/blobs/data-lake-storage-access-control-model#role-based-access-control-azure-rbac). There's no support for Attribute-based access control (Azure ABAC).[Azure Blob indexer](#configure-indexer-based-indexing)or a[Blob knowledge source](#configure-a-knowledge-source)that retrieves and ingests data and metadata, including permission filters. To get permission filter support, use the latest preview REST API or a preview package of an Azure SDK that supports the feature.[An index in Azure AI Search](search-how-to-create-search-index)containing the ingested documents and corresponding permissions. Permission metadata is stored as fields in the index.[A query that uses permission filters](search-query-access-control-rbac-enforcement). To set up queries that respect the permission filters, use the latest preview REST API or a preview package of an Azure SDK that supports the feature.

## Prerequisites

[Microsoft Entra ID authentication and authorization](/en-us/entra/identity/authentication/overview-authentication). Services and apps must be in the same tenant. Users can be in different tenants as long as all of the tenants are Microsoft Entra ID. Role assignments are used for each authenticated connection.Azure AI Search, any region, but you must have a billable tier (basic and higher) for managed identity support. The search service must be

[configured for role-based access](search-security-enable-roles)and it must[have a managed identity (either system or user)](search-how-to-managed-identities).Azure Storage, Standard performance (general-purpose v2), on hot, cool, and cold access tiers, with RBAC-secured containers or blobs.

You should understand how indexers and knowledge sources work and how to create an index. This article explains the configuration settings for the data source and indexer, but doesn't provide steps for creating the index. For more information about indexes designed for permission filters, see

[Create an index with permission filter fields](search-index-access-control-lists-and-rbac-push-api#create-an-index-with-permission-filter-fields).This functionality is currently not supported in the Azure portal, this includes Permission filters created through the

[Import wizards](search-import-data-portal). Use a programmatic approach to create or modify existing objects for document-level access.

## Configure Blob storage

Verify your blob container uses role-based access.

Sign in to the Azure portal and find your storage account.

Expand

**containers**and select the container that has the blobs you want to index.Select

**Access Control (IAM)**to check role assignments. Users and groups with**Storage Blob Data Reader**or**Storage Blob Data Contributor**will have access to search documents in the index after the container is indexed.

### Authorization

For indexer execution, your search service identity must have **Storage Blob Data Reader** permission. For more information, see [Connect to Azure Storage using a managed identity](search-howto-managed-identities-storage).

## Configure Azure AI Search

Recall that the search service must have:

### Authorization

For indexer execution, the client issuing the API call must have **Search Service Contributor** permission to create objects, **Search Index Data Contributor** permission to perform data import, and **Search Index Data Reader** to query an index see [Connect to Azure AI Search using roles](search-security-rbac).

## Configure a knowledge source

If you're using a knowledge source, definitions in the knowledge source are used to generate a full indexing pipeline (indexer, data source, and index). RBAC scope is detected and automatically included in the generated index. There's no need to modify any of the generated objects if you want permission inheritance in your indexed content.

Key points about the configuration that make it work for this scenario:

`isADLSGen2`

is set to false, which means the data source is Azure Blob storage.`ingestionPermissionOptions`

specifies`rbacScope`

.

```
# Create / Update Azure Blob Knowledge Source
###
PUT {{url}}/knowledgesources/azure-blob-ks?api-version=2025-11-01-preview
api-key: {{key}}
Content-Type: application/json
{
"name": "azure-blob-ks",
"kind": "azureBlob",
"description": "A sample azure blob knowledge source",
"azureBlobParameters": {
"connectionString": "{{blob-connection-string}}",
"containerName": "blobcontainer",
"folderPath": null,
"isADLSGen2": false,
"ingestionParameters": {
"identity": null,
"embeddingModel": {
"kind": "azureOpenAI",
"azureOpenAIParameters": {
"deploymentId": "text-embedding-3-large",
"modelName": "text-embedding-3-large",
"resourceUri": "{{aoai-endpoint}}",
"apiKey": "{{aoai-key}}"
}
},
"chatCompletionModel": null,
"disableImageVerbalization": true,
"ingestionSchedule": null,
"ingestionPermissionOptions": ["rbacScope"],
"contentExtractionMode": "minimal",
"aiServices": {
"uri": "{{ai-endpoint}}",
"apiKey": "{{ai-key}}"
}
}
}
}
```


## Configure indexer-based indexing

If you're using an indexer, configure it, the data source, and the index to pull permission metadata from blobs.

### Create the data source

Data Source type must be

`azureblob`

.Data source parsing mode must be the default.

Data source must have

`indexerPermissionOptions`

with`rbacScope`

.For

`rbacScope`

, configure the[connection string](search-how-to-index-azure-data-lake-storage#supported-credentials-and-connection-strings)with managed identity format.For connection strings using a

[user-assigned managed identity](search-howto-managed-identities-storage#user-assigned-managed-identity-preview), you must also specify the`identity`

property.


JSON example with system managed identity and `indexerPermissionOptions`

:

```
{
"name" : "my-blob-datasource",
"type": "azureblob",
"indexerPermissionOptions": ["rbacScope"],
"credentials": {
"connectionString": "ResourceId=/subscriptions/<your subscription ID>/resourceGroups/<your resource group name>/providers/Microsoft.Storage/storageAccounts/<your storage account name>/;"
},
"container": {
"name": "<your-container-name>",
"query": "<optional-query-used-for-selecting-specific-blobs>"
}
}
```


JSON schema example with a user-managed identity in the connection string:

```
{
"name" : "my-blob-datasource",
"type": "azureblob",
"indexerPermissionOptions": ["rbacScope"],
"credentials": {
"connectionString": "ResourceId=/subscriptions/<your subscription ID>/resourceGroups/<your resource group name>/providers/Microsoft.Storage/storageAccounts/<your storage account name>/;"
},
"container": {
"name": "<your-container-name>",
"query": "<optional-query-used-for-selecting-specific-blobs>"
},
"identity": {
"@odata.type": "#Microsoft.Azure.Search.DataUserAssignedIdentity",
"userAssignedIdentity": "/subscriptions/{subscription-ID}/resourceGroups/{resource-group-name}/providers/Microsoft.ManagedIdentity/userAssignedIdentities/{user-assigned-managed-identity-name}"
}
}
```


### Create permission fields in the index

In Azure AI Search, make sure your index contains field definitions for the permission metadata. Permission metadata can be indexed when `indexerPermissionOptions`

is specified in the data source definition.

Recommended schema attributes RBAC Scope:

- RBAC scope field with
`rbacScope`

permissionFilter value. - Property
`permissionFilterOption`

to enable filtering at querying time. - Use string fields for permission metadata
- Set
`filterable`

to true on all fields.

Notice that `retrievable`

is false. You can set it true during development to verify permissions are present, but remember to set to back to false before deploying to a production environment so that security principal identities aren't visible in results.

JSON schema example:

```
{
...
"fields": [
...
{
"name": "RbacScope",
"type": "Edm.String",
"permissionFilter": "rbacScope",
"filterable": true,
"retrievable": false
}
],
"permissionFilterOption": "enabled"
}
```


### Configure the indexer

Field mappings within an indexer set the data path to fields in an index. Target and destination fields that vary by name or data type require an explicit field mapping. The following metadata fields in Azure Blob Storage might need field mappings if you vary the field name:

**metadata_rbac_scope**(`Edm.String`

) - the container RBAC scope.

Specify `fieldMappings`

in the indexer to route the permission metadata to target fields during indexing.

JSON schema example:

```
{
...
"fieldMappings": [
{ "sourceFieldName": "metadata_rbac_scope", "targetFieldName": "RbacScope" }
]
}
```


### Run the indexer

Once your indexer, data source, and index are configured, run the indexer to set the process in motion. If there's a problem with configuration or permissions, those problems will surface in this step.

By default, an indexer runs as soon as you post it to a search service, but if the indexer configuration includes `disabled`

set to true, the indexer is posted in a disabled state so that you can run the indexer manually.

We recommend [running the indexer from the Azure portal](search-howto-run-reset-indexers#how-to-reset-and-run-indexers) so that you can monitor status and messages.

Assuming no errors, the index is now populated and you can move forward with [queries and testing](search-query-access-control-rbac-enforcement).

## Deletion tracking

To effectively manage blob deletion, ensure that you have enabled [deletion tracking](search-how-to-index-azure-blob-changed-deleted) before your indexer runs for the first time. This feature allows the system to detect deleted blobs from your source and delete the corresponding content from the index.


---

<!-- DOCUMENTO FUSIONADO: search-modeling-multitenant-saas-applications.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-modeling-multitenant-saas-applications -->

# Design patterns for multitenant SaaS applications and Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A multitenant application is one that provides the same services and capabilities to any number of tenants who can't see or share the data of any other tenant. This article discusses tenant isolation strategies for multitenant applications built with Azure AI Search.

## Azure AI Search concepts

As a search-as-a-service solution, [Azure AI Search](search-what-is-azure-search) allows developers to add rich search experiences to applications without managing any infrastructure or becoming an expert in information retrieval. Data is uploaded to the service and then stored in the cloud. Using simple requests to the Azure AI Search API, the data can then be modified and searched.

### Search services, indexes, fields, and documents

Before discussing design patterns, it's important to understand a few basic concepts.

When using Azure AI Search, one subscribes to a *search service*. As data is uploaded to Azure AI Search, it's stored in an *index* within the search service. There can be a number of indexes within a single service. To use the familiar concepts of databases, the search service can be likened to a database while the indexes within a service can be likened to tables within a database.

Each index within a search service has its own schema, which is defined by a number of customizable *fields*. Data is added to an Azure AI Search index in the form of individual *documents*. Each document must be uploaded to a particular index and must fit that index's schema. When searching data using Azure AI Search, the full-text search queries are issued against a particular index. To compare these concepts to those of a database, fields can be likened to columns in a table and documents can be likened to rows.

### Scalability

Any Azure AI Search service in the Standard [pricing tier](https://azure.microsoft.com/pricing/details/search/) can scale in two dimensions: storage and availability.

*Partitions*can be added to increase the storage of a search service.*Replicas*can be added to a service to increase the throughput of requests that a search service can handle.

Adding and removing partitions and replicas at will allow the capacity of the search service to grow with the amount of data and traffic the application demands. In order for a search service to achieve a read [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), it requires two replicas. In order for a service to achieve a read-write [SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/), it requires three replicas.

### Service and index limits in Azure AI Search

There are a few different [pricing tiers](https://azure.microsoft.com/pricing/details/search/) in Azure AI Search, each of the tiers has different [limits and quotas](search-limits-quotas-capacity). Some of these limits are at the service-level, some are at the index-level, and some are at the partition-level.

#### S3 High Density

In Azure AI Search’s S3 pricing tier, there's an option for the High Density (HD) mode designed specifically for multitenant scenarios. In many cases, it's necessary to support a large number of smaller tenants under a single service to achieve the benefits of simplicity and cost efficiency.

S3 HD allows for the many small indexes to be packed under the management of a single search service by trading the ability to scale out indexes using partitions for the ability to host more indexes in a single service.

An S3 service is designed to host a fixed number of indexes (maximum 200) and allow each index to scale in size horizontally as new partitions are added to the service. Adding partitions to S3 HD services increases the maximum number of indexes that the service can host. The ideal maximum size for an individual S3HD index is around 50 - 80 GB, although there's no hard size limit on each index imposed by the system.

## Considerations for multitenant applications

Multitenant applications must effectively distribute resources among the tenants while preserving some level of privacy between the various tenants. There are a few considerations when designing the architecture for such an application:

*Tenant isolation:*Application developers need to take appropriate measures to ensure that no tenants have unauthorized or unwanted access to the data of other tenants. Beyond the perspective of data privacy, tenant isolation strategies require effective management of shared resources and protection from noisy neighbors.*Cloud resource cost:*As with any other application, software solutions must remain cost competitive as a component of a multitenant application.*Ease of Operations:*When developing a multitenant architecture, the impact on the application's operations and complexity is an important consideration. Azure AI Search has a[99.9% SLA](https://azure.microsoft.com/support/legal/sla/search/v1_0/).*Global footprint:*Multitenant applications often need to serve tenants who are distributed across the globe.*Scalability:*Application developers need to consider how they reconcile between maintaining a sufficiently low level of application complexity and designing the application to scale with number of tenants and the size of tenants' data and workload.

Azure AI Search offers a few boundaries that can be used to isolate tenants’ data and workload.

## Modeling multitenancy with Azure AI Search

In the case of a multitenant scenario, the application developer consumes one or more search services and divides their tenants among services, indexes, or both. Azure AI Search has a few common patterns when modeling a multitenant scenario:

*One index per tenant:*Each tenant has its own index within a search service that is shared with other tenants.*One service per tenant:*Each tenant has its own dedicated Azure AI Search service, offering highest level of data and workload separation.*Mix of both:*Larger, more-active tenants are assigned dedicated services while smaller tenants are assigned individual indexes within shared services.

## Model 1: One index per tenant


In an index-per-tenant model, multiple tenants occupy a single Azure AI Search service where each tenant has their own index.

This approach works because all search requests and document operations are issued at an index level in Azure AI Search. In the application layer, there's the need awareness to direct the various tenants’ traffic to the proper indexes while also managing resources at the service level across all tenants.

A key attribute of the index-per-tenant model is the ability for the application developer to oversubscribe the capacity of a search service among the application’s tenants. If the tenants have an uneven distribution of workload, the optimal combination of tenants can be distributed across a search service’s indexes to accommodate a number of highly active, resource-intensive tenants while simultaneously serving a long tail of less active tenants. The trade-off is the inability of the model to handle situations where each tenant is concurrently highly active.

The index-per-tenant model provides the basis for a variable cost model, where an entire Azure AI Search service is bought up-front and then subsequently filled with tenants. This allows for unused capacity to be designated for trials and free accounts.

For applications with a global footprint, the index-per-tenant model might not be the most efficient. If an application's tenants are distributed across the globe, a separate service can be necessary for each region, duplicating costs across each of them.

Azure AI Search allows for the scale of both the individual indexes and the total number of indexes to grow. If an appropriate pricing tier is chosen, partitions and replicas can be added to the entire search service when an individual index within the service grows too large in terms of storage or traffic.

If the total number of indexes grows too large for a single service, another service has to be provisioned to accommodate the new tenants. If indexes have to be moved between search services as new services are added, the data from the index has to be manually copied from one index to the other as Azure AI Search doesn't allow for an index to be moved.

## Model 2: One service per tenant


In a service-per-tenant architecture, each tenant has its own search service.

In this model, the application achieves the maximum level of isolation for its tenants. Each service has dedicated storage and throughput for handling search requests. Each tenant has individual ownership of API keys.

For applications where each tenant has a large footprint or the workload has little variability from tenant to tenant, the service-per-tenant model is an effective choice as resources aren't shared across various tenants’ workloads.

A service per tenant model also offers the benefit of a predictable, fixed cost model. There's no up-front investment in an entire search service until there's a tenant to fill it, however the cost-per-tenant is higher than an index-per-tenant model.

The service-per-tenant model is an efficient choice for applications with a global footprint. With geographically distributed tenants, it's easy to have each tenant's service in the appropriate region.

The challenges in scaling this pattern arise when individual tenants outgrow their service. Azure AI Search doesn't currently support upgrading the pricing tier of a search service, so all data would have to be manually copied to a new service.

## Model 3: Hybrid

Another pattern for modeling multitenancy is mixing both index-per-tenant and service-per-tenant strategies.

By mixing the two patterns, an application's largest tenants can occupy dedicated services while the long tail of less active, smaller tenants can occupy indexes in a shared service. This model ensures that the largest tenants have consistently high performance from the service while helping to protect the smaller tenants from any noisy neighbors.

However, implementing this strategy relies on foresight in predicting which tenants will require a dedicated service versus an index in a shared service. Application complexity increases with the need to manage both of these multitenancy models.

## Achieving even finer granularity

The above design patterns to model multitenant scenarios in Azure AI Search assume a uniform scope where each tenant is a whole instance of an application. However, applications can sometimes handle many smaller scopes.

If service-per-tenant and index-per-tenant models aren't sufficiently small scopes, it's possible to model an index to achieve an even finer degree of granularity.

To have a single index behave differently for different client endpoints, a field can be added to an index, which designates a certain value for each possible client. Each time a client calls Azure AI Search to query or modify an index, the code from the client application specifies the appropriate value for that field using Azure AI Search's [filter](query-odata-filter-orderby-syntax) capability at query time.

This method can be used to achieve functionality of separate user accounts, separate permission levels, and even completely separate applications.

Note

Using the approach described above to configure a single index to serve multiple tenants affects the relevance of search results. Search relevance scores are computed at an index-level scope, not a tenant-level scope, so all tenants' data is incorporated in the relevance scores' underlying statistics such as term frequency.

## Next steps

Azure AI Search is a compelling choice for many applications. When evaluating the various design patterns for multitenant applications, consider the [various pricing tiers](https://azure.microsoft.com/pricing/details/search/) and the respective [service limits](search-limits-quotas-capacity) to best tailor Azure AI Search to fit application workloads and architectures of all sizes.
