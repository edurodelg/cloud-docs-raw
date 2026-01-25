---
merged_at: 2026-01-25T03:18:14.039114
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-how-to-index-azure-blob-json.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-index-azure-blob-json -->

# Index JSON blobs and files in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to**: [Blob indexers](search-how-to-index-azure-blob-storage), [File indexers](search-file-storage-integration)

For blob indexing in Azure AI Search, this article shows you how to set properties for blobs or files consisting of JSON documents. JSON files in Azure Blob Storage or Azure Files commonly assume any of these forms:

- A single JSON document
- A JSON document containing an array of well-formed JSON elements
- A JSON document containing multiple entities, separated by a newline

The blob indexer provides a `parsingMode`

parameter to optimize the output of the search document based on JSON structure. Parsing modes consist of the following options:

| parsingMode | JSON document | Description |
|---|---|---|
`json` |
One per blob | (default) Parses JSON blobs as a single chunk of text. Each JSON blob becomes a single search document. |
`jsonArray` |
Multiple per blob | Parses a JSON array in the blob, where each element of the array becomes a separate search document. |
`jsonLines` |
Multiple per blob | Parses a blob that contains multiple JSON entities (also an array), with individual elements separated by a newline. The indexer starts a new search document after each new line. |

For both ** jsonArray** and

**, you should review**

`jsonLines`

[Indexing one blob to produce many search documents](search-how-to-index-azure-blob-one-to-many)to understand how the blob indexer handles disambiguation of the document key for multiple search documents produced from the same blob.

Within the indexer definition, you can optionally set [field mappings](search-indexer-field-mappings) to choose which properties of the source JSON document are used to populate your target search index. For example, when using the ** jsonArray** parsing mode, if the array exists as a lower-level property, you can set a "documentRoot" property indicating where the array is placed within the blob.

Note

When a JSON parsing mode is used, Azure AI Search assumes that all blobs use the same parser (either for ** json**,

**or**

`jsonArray`

**). If you have a mix of different file types in the same data source, consider using**

`jsonLines`

[file extension filters](search-blob-storage-integration#controlling-which-blobs-are-indexed)to control which files are imported.

The following sections describe each mode in more detail. If you're unfamiliar with indexer clients and concepts, see [Create a search indexer](search-howto-create-indexers). You should also be familiar with the details of [basic blob indexer configuration](search-how-to-index-azure-blob-storage), which isn't repeated here.

## Index single JSON documents (one per blob)

By default, blob indexers parse JSON blobs as a single chunk of text, one search document for each blob in a container. If the JSON is structured, the search document can reflect that structure, with individual elements represented as individual fields. For example, assume you have the following JSON document in Azure Blob Storage:

```
{
"article" : {
"text" : "A hopefully useful article explaining how to parse JSON blobs",
"datePublished" : "2020-04-13",
"tags" : [ "search", "storage", "howto" ]
}
}
```


The blob indexer parses the JSON document into a single search document, loading an index by matching "text", "datePublished", and "tags" from the source against identically named and typed target index fields. Given an index with "text", "datePublished, and "tags" fields, the blob indexer can infer the correct mapping without a field mapping present in the request.

Although the default behavior is one search document per JSON blob, setting the ** json** parsing mode changes the internal field mappings for content, promoting fields inside

`content`

to actual fields in the search index. An example indexer definition for the **parsing mode might look like this:**

`json`

```
POST https://[service name].search.windows.net/indexers?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
{
"name" : "my-json-indexer",
"dataSourceName" : "my-blob-datasource",
"targetIndexName" : "my-target-index",
"parameters" : { "configuration" : { "parsingMode" : "json" } }
}
```


Note

As with all indexers, if fields don't clearly match, you should expect to explicitly specify individual [field mappings](search-indexer-field-mappings) unless you're using the implicit fields mappings available for blob content and metadata, as described in [basic blob indexer configuration](search-how-to-index-azure-blob-storage).
To override an existing index value, the source JSON must provide a non-null value. If the field in the source document is null, the indexer will retain the existing value. To explicitly clear a field, pass an empty string ("") instead. This prevents unintended deletions from the index.

### json example (single hotel JSON files)

The [hotel JSON document data set](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/hotels/hotel-json-documents) on GitHub is helpful for testing JSON parsing, where each blob represents a structured JSON file. You can upload the data files to Blob Storage and use an [import wizard](search-get-started-portal) to quickly evaluate how this content is parsed into individual search documents.

The data set consists of five blobs, each containing a hotel document with an address collection and a rooms collection. The blob indexer detects both collections and reflects the structure of the input documents in the index schema.

## Parse JSON arrays

Alternatively, you can use the JSON array option. This option is useful when blobs contain an array of well-formed JSON objects, and you want each element to become a separate search document. Using ** jsonArrays**, the following JSON blob produces three separate documents, each with

`"id"`

and `"text"`

fields.```
[
{ "id" : "1", "text" : "example 1" },
{ "id" : "2", "text" : "example 2" },
{ "id" : "3", "text" : "example 3" }
]
```


The `parameters`

property on the indexer contains parsing mode values. For a JSON array, the indexer definition should look similar to the following example.

```
POST https://[service name].search.windows.net/indexers?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
{
"name" : "my-json-indexer",
"dataSourceName" : "my-blob-datasource",
"targetIndexName" : "my-target-index",
"parameters" : { "configuration" : { "parsingMode" : "jsonArray" } }
}
```


### jsonArrays example

The [New York Philharmonic JSON data set](https://github.com/Azure-Samples/azure-search-sample-data/tree/main/ny-philharmonic) on GitHub is helpful for testing JSON array parsing. You can upload the data files to Blob storage and use an [import wizard](search-get-started-portal) to quickly evaluate how this content is parsed into individual search documents.

The data set consists of eight blobs, each containing a JSON array of entities, for a total of 100 entities. The entities vary as to which fields are populated, but the end result is one search document per entity, from all arrays, in all blobs.

### Parsing nested JSON arrays

For JSON arrays having nested elements, you can specify a `documentRoot`

to indicate a multi-level structure. For example, if your blobs look like this:

```
{
"level1" : {
"level2" : [
{ "id" : "1", "text" : "Use the documentRoot property" },
{ "id" : "2", "text" : "to pluck the array you want to index" },
{ "id" : "3", "text" : "even if it's nested inside the document" }
]
}
}
```


Use this configuration to index the array contained in the `level2`

property:

```
{
"name" : "my-json-array-indexer",
... other indexer properties
"parameters" : { "configuration" : { "parsingMode" : "jsonArray", "documentRoot" : "/level1/level2" } }
}
```


## Parse JSON entities separated by newlines

If your blob contains multiple JSON entities separated by a newline, and you want each element to become a separate search document, use ** jsonLines**.

```
{ "id" : "1", "text" : "example 1" }
{ "id" : "2", "text" : "example 2" }
{ "id" : "3", "text" : "example 3" }
```


For JSON lines, the indexer definition should look similar to the following example.

```
POST https://[service name].search.windows.net/indexers?api-version=2025-09-01
Content-Type: application/json
api-key: [admin key]
{
"name" : "my-json-indexer",
"dataSourceName" : "my-blob-datasource",
"targetIndexName" : "my-target-index",
"parameters" : { "configuration" : { "parsingMode" : "jsonLines" } }
}
```


## Map JSON fields to search fields

Field mappings associate a source field with a destination field in situations where the field names and types aren't identical. But field mappings can also be used to match parts of a JSON document and "lift" them into top-level fields of the search document.

The following example illustrates this scenario. For more information about field mappings in general, see [field mappings](search-indexer-field-mappings).

```
{
"article" : {
"text" : "A hopefully useful article explaining how to parse JSON blobs",
"datePublished" : "2016-04-13"
"tags" : [ "search", "storage", "howto" ]
}
}
```


Assume a search index with the following fields: `text`

of type `Edm.String`

, `date`

of type `Edm.DateTimeOffset`

, and `tags`

of type `Collection(Edm.String)`

. Notice the discrepancy between "datePublished" in the source and `date`

field in the index. To map your JSON into the desired shape, use the following field mappings:

```
"fieldMappings" : [
{ "sourceFieldName" : "/article/text", "targetFieldName" : "text" },
{ "sourceFieldName" : "/article/datePublished", "targetFieldName" : "date" },
{ "sourceFieldName" : "/article/tags", "targetFieldName" : "tags" }
]
```


Source fields are specified using the [JSON Pointer](https://tools.ietf.org/html/rfc6901) notation. You start with a forward slash to refer to the root of your JSON document, then pick the desired property (at arbitrary level of nesting) by using forward slash-separated path.

You can also refer to individual array elements by using a zero-based index. For example, to pick the first element of the "tags" array from the above example, use a field mapping like this:

```
{ "sourceFieldName" : "/article/tags/0", "targetFieldName" : "firstTag" }
```


Note

If "sourceFieldName" refers to a property that doesn't exist in the JSON blob, that mapping is skipped without an error. This behavior allows indexing to continue for JSON blobs that have a different schema (which is a common use case). Because there's no validation check, check the mappings carefully for typos so that you aren't losing documents for the wrong reason.


---

<!-- DOCUMENTO FUSIONADO: search-howto-managed-identities-cosmos-db.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-howto-managed-identities-cosmos-db -->

# Connect to Azure Cosmos DB using a managed identity (Azure AI Search)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to set up an indexer connection to an Azure Cosmos DB database using a managed identity instead of providing credentials in the connection string.'

You can use a system-assigned managed identity or a user-assigned managed identity. Managed identities are Microsoft Entra logins and require Azure role assignments to access data in Azure Cosmos DB. You can optionally [enforce role-based access as the only authentication method](/en-us/azure/cosmos-db/how-to-setup-rbac#disable-local-auth) for data connections by setting `disableLocalAuth`

to `true`

for your Azure Cosmos DB for NoSQL account.

## Prerequisites

[Create a managed identity](search-how-to-managed-identities)for your search service.

## Limitations

- Indexers that connect to Azure Cosmos DB for Gremlin and MongoDB (currently in preview) only support the
*legacy*approach.

## Supported approaches for managed identity authentication

Azure AI Search supports two mechanisms to connect to Azure Cosmos DB using managed identity.

The

*legacy*approach requires configuring the managed identity to have reader permissions on the control plane of the target Azure Cosmos DB account. Azure AI Search utilizes that identity to fetch the account keys of Cosmos DB account in the background to access the data. This approach won't work if the Cosmos DB account has`"disableLocalAuth": true`

.The

*modern*approach requires configuring the managed identity appropriate roles on the control and data plane of the target Azure Cosmos DB account. Azure AI Search will then request an access token to access the data in the Cosmos DB account. This approach works even if the Cosmos DB account has`"disableLocalAuth": true`

.

Indexers that connect to Azure Cosmos DB for NoSQL support both the *legacy* and the *modern* approach - the *modern* approach is recommended.

## Connect to Azure Cosmos DB for NoSQL

This section outlines the steps to configure connecting to Azure Cosmos DB for NoSQL via the *modern* approach.

### Configure control plane role assignments

Sign in to Azure portal and find your Cosmos DB for NoSQL account.

Select

**Access control (IAM)**.Select

**Add**and then select**Role assignment**.From the list of job function roles, select

**Cosmos DB Account Reader**.Select

**Next**.Select

**Managed identity**and then select**Members**.Filter by system-assigned managed identities or user-assigned managed identities. You should see the managed identity that you previously created for your search service. If you don't have one, see

[Configure search to use a managed identity](search-how-to-managed-identities). If you already set one up but it's not available, give it a few minutes.Select the identity and save the role assignment.


For more information, see [Use control plane role-based access control with Azure Cosmos DB for NoSQL](/en-us/azure/cosmos-db/nosql/security/how-to-grant-control-plane-role-based-access).

### Configure data plane role assignments

The managed identity needs to assigned a role to read from the Cosmos DB account's data plane. The Object (principal) ID for the search service's system/user assigned identity can be found from the search service's "Identity" tab. This step can only be performed via Azure CLI at the moment.

Set variables:

```
$cosmosdb_acc_name = <cosmos db account name>
$resource_group = <resource group name>
$subsciption = <subscription ID>
$system_assigned_principal = <Object (principal) ID for the search service's system/user assigned identity>
$readOnlyRoleDefinitionId = "00000000-0000-0000-0000-000000000001"
$scope=$(az cosmosdb show --name $cosmosdb_acc_name --resource-group $resource_group --query id --output tsv)
```


Define a role assignment for the system-assigned identity:

```
az cosmosdb sql role assignment create --account-name $cosmosdb_acc_name --resource-group $resource_group --role-definition-id $readOnlyRoleDefinitionId --principal-id $system_assigned_principal --scope $scope
```


For more information, see [Use data plane role-based access control with Azure Cosmos DB for NoSQL](/en-us/azure/cosmos-db/nosql/security/how-to-grant-data-plane-role-based-access)

### Configure the data source definition

Once you have configured **both** control plane and data plane role assignments on the Azure Cosmos DB for NoSQL account, you can set up a connection to it that operates under that role.

Indexers use a data source object for connections to an external data source. This section explains how to specify a system-assigned managed identity or a user-assigned managed identity on a data source connection string. You can find more [connection string examples](search-how-to-managed-identities#connection-string-examples) in the managed identity article.

Tip

You can create a data source connection to Cosmos DB in the Azure portal, specifying either a system or user-assigned managed identity, and then view the JSON definition to see how the connection string is formulated.

The [REST API](/en-us/rest/api/searchservice/data-sources/create), Azure portal, and the [.NET SDK](/en-us/dotnet/api/azure.search.documents.indexes.models.searchindexerdatasourceconnection) support using a system-assigned or user-assigned managed identity.

#### Connect through system-assigned identity

When you're connecting with a system-assigned managed identity, the only change to the data source definition is the format of the "credentials" property. Provide a database name and a ResourceId that has no account key or password. The ResourceId must include the subscription ID of Azure Cosmos DB, the resource group, and the Azure Cosmos DB account name.

Here's an example using the [Create Data Source](/en-us/rest/api/searchservice/data-sources/create) REST API that exercises the *modern* approach.

```
POST https://[service name].search.windows.net/datasources?api-version=2025-09-01
{
"name": "my-cosmosdb-ds",
"type": "cosmosdb",
"credentials": {
"connectionString": "ResourceId=/subscriptions/[subscription-id]/resourceGroups/[rg-name]/providers/Microsoft.DocumentDB/databaseAccounts/[cosmos-account-name];Database=[cosmos-database];IdentityAuthType=AccessToken"
},
"container": { "name": "[my-cosmos-collection]" }
}
```


Note

If the `IdentityAuthType`

property isn't part of the connection string, then Azure AI Search defaults to the *legacy* approach to ensure backward compatibility.

#### Connect through user-assigned identity (preview)

You need to add an "identity" property to the data source definition, where you specify the specific identity (out of several that can be assigned to the search service), that will be used to connect to the Azure Cosmos DB account.

Here's an example using user-assigned identity via the *modern* approach.

```
POST https://[service name].search.windows.net/datasources?api-version=2025-11-01-preview
{
"name": "[my-cosmosdb-ds]",
"type": "cosmosdb",
"credentials": {
"connectionString": "ResourceId=/subscriptions/[subscription-id]/resourceGroups/[rg-name]/providers/Microsoft.DocumentDB/databaseAccounts/[cosmos-account-name];Database=[cosmos-database];IdentityAuthType=AccessToken"
},
"container": { "name": "[my-cosmos-collection]"},
"identity" : {
"@odata.type": "#Microsoft.Azure.Search.DataUserAssignedIdentity",
"userAssignedIdentity": "/subscriptions/[subscription-id]/resourcegroups/[rg-name]/providers/Microsoft.ManagedIdentity/userAssignedIdentities/[my-user-managed-identity-name]"
}
}
```


## Connect to Azure Cosmos DB for Gremlin/MongoDB (preview)

This section outlines the steps to configure connecting to Azure Cosmos DB for Gremlin/Mongo via the *legacy* approach.

### Configure control plane role assignments

Follow the same steps as before to assign the appropriate roles on the control plane of the Azure Cosmos DB for Gremlin/MongoDB.

### Set the connection string

- For MongoDB collections, add "ApiKind=MongoDb" to the connection string and use a preview REST API.
- For Gremlin graphs, add "ApiKind=Gremlin" to the connection string and use a preview REST API.
- For either kinds, only the
**legacy**approach is supported - that is,`IdentityAuthType=AccountKey`

or omitting it entirely is the only valid connection string.

Here's an example to connect to MongoDB collections using system-assigned identity via the REST API

```
POST https://[service name].search.windows.net/datasources?api-version=2025-11-01-preview
{
"name": "my-cosmosdb-ds",
"type": "cosmosdb",
"credentials": {
"connectionString": "ResourceId=/subscriptions/[subscription-id]/resourceGroups/[rg-name]/providers/Microsoft.DocumentDB/databaseAccounts/[cosmos-account-name];Database=[cosmos-database];ApiKind=MongoDb"
},
"container": { "name": "[my-cosmos-collection]", "query": null },
"dataChangeDetectionPolicy": null
}
```


Here's an example to connect to Gremlin graphs using user-assigned identity.

```
POST https://[service name].search.windows.net/datasources?api-version=2025-11-01-preview
{
"name": "[my-cosmosdb-ds]",
"type": "cosmosdb",
"credentials": {
"connectionString": "ResourceId=/subscriptions/[subscription-id]/resourceGroups/[rg-name]/providers/Microsoft.DocumentDB/databaseAccounts/[cosmos-account-name];Database=[cosmos-database];ApiKind=Gremlin"
},
"container": { "name": "[my-cosmos-collection]"},
"identity" : {
"@odata.type": "#Microsoft.Azure.Search.DataUserAssignedIdentity",
"userAssignedIdentity": "/subscriptions/[subscription-id]/resourcegroups/[rg-name]/providers/Microsoft.ManagedIdentity/userAssignedIdentities/[my-user-managed-identity-name]"
}
}
```


## Run the indexer to verify permissions

Connection information and permissions on the remote service are validated at run time during indexer execution. If the indexer is successful, the connection syntax and role assignments are valid. For more information, see [Run or reset indexers, skills, or documents](search-howto-run-reset-indexers).

## Troubleshoot connections

For Azure Cosmos DB for NoSQL, check whether the account has its access restricted to select networks. You can rule out any firewall issues by trying the connection without restrictions in place. Refer to

[Indexer access to content protected by Azure network security](search-indexer-securing-resources)for more informationFor Azure Cosmos DB for NoSQL, if the indexer fails due to authentication issues, ensure that the role assignments have been done

**both**on the control plane and data plane of the Cosmos DB account.For Gremlin or MongoDB, if you recently rotated your Azure Cosmos DB account keys, you need to wait up to 15 minutes for the managed identity connection string to work.
