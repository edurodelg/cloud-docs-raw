---
merged_at: 2026-01-25T02:11:58.415188
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-security-trimming-for-azure-search.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-security-trimming-for-azure-search -->

# Security filters for trimming results in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For search solutions that can't use the [built-in access control list (ACL) support](search-document-level-access-overview) for document-level authorization, Azure AI Search supports creating a filter that trims search results based on a string containing a group or user identity.

This article describes a pattern for security filtering having the following steps:

- Assemble source documents with the required content, including a string for storing an identity
- Create a field in the search index for the principal identifiers
- Push the documents to the search index for indexing
- Query the index with the
`search.in`

filter function

It concludes with links to demos and examples that provide hands-on learning. We recommend reviewing this article first to understand the pattern.

## About the security filter pattern

The security filter pattern simulates document-level authorization by using a regular OData filter that includes or excludes a search result based on a string consisting of a security principal. There's no authentication or authorization through the security principal. The principal is just a string, used in a filter expression, to include or exclude a document from the search results.

There are several ways to achieve security filtering. One way is through a complicated disjunction of equality expressions: for example, `Id eq 'id1' or Id eq 'id2'`

, and so forth. This approach is error-prone, difficult to maintain, and in cases where the list contains hundreds or thousands of values, slows down query response time by many seconds.

A better solution is using the `search.in`

function for security filters, as described in this article. If you use `search.in(Id, 'id1, id2, ...')`

instead of an equality expression, you can expect subsecond response times.

## Prerequisites

A string field containing a group or user identity, such as a Microsoft Entra object identifier.

Other fields in the same document should provide the content that's accessible to that group or user. In the following JSON documents, the "security_id" fields contain identities used in a security filter, and the name, salary, and marital status are included if the identity of the caller matches the "security_id" of the document.

`{ "Employee-1": { "employee_id": "100-1000-10-1-10000-1", "name": "Abram", "salary": 75000, "married": true, "security_id": "alphanumeric-object-id-for-employee-1" }, "Employee-2": { "employee_id": "200-2000-20-2-20000-2", "name": "Adams", "salary": 75000, "married": true, "security_id": "alphanumeric-object-id-for-employee-2" } }`


## Create security field

In the search index, within the fields collection, you need one field that contains the group or user identity, similar to the fictitious "security_id" field in the previous example.

Add a security field as a

`Collection(Edm.String)`

.Set the field's

`filterable`

attribute set to`true`

.Set the field's

`retrievable`

attribute to`false`

so that it isn't returned as part of the search request.Indexes require a document key. The "file_id" field satisfies that requirement.

Indexes should also contain searchable and retrievable content. The "file_name" and "file_description" fields represent that in this example.

The following index schema satisfies the field requirements. Documents that you index on Azure AI Search should have values for all of these fields, including the "group_ids". For the document with

`file_name`

"secured_file_b", only users that belong to group IDs "group_id1" or "group_id2" have read access to the file.`POST https://[search service].search.windows.net/indexes/securedfiles/docs/index?api-version=2025-09-01 { "name": "securedfiles", "fields": [ {"name": "file_id", "type": "Edm.String", "key": true, "searchable": false }, {"name": "file_name", "type": "Edm.String", "searchable": true }, {"name": "file_description", "type": "Edm.String", "searchable": true }, {"name": "group_ids", "type": "Collection(Edm.String)", "filterable": true, "retrievable": false } ] }`


## Push data into your index using the REST API

Populate your search index with documents that provide values for each field in the fields collection, including values for the security field. Azure AI Search doesn't provide APIs or features for populating the security field specifically. However, several of the examples listed at the end of this article explain techniques for populating this field.

In Azure AI Search, the approaches for loading data are:

- A single push or pull (indexer) operation that imports documents populated with all fields
- Multiple push or pull operations. As long as secondary import operations target the right document identifier, you can load fields individually through multiple imports.

The following example shows a single HTTP POST request to the docs collection of your index's URL endpoint (see [Documents - Index](/en-us/rest/api/searchservice/documents/)). The body of the HTTP request is a JSON rendering of the documents to be indexed:

```
POST https://[search service].search.windows.net/indexes/securedfiles/docs/index?api-version=2025-09-01
{
"value": [
{
"@search.action": "upload",
"file_id": "1",
"file_name": "secured_file_a",
"file_description": "File access is restricted to Human Resources.",
"group_ids": ["group_id1"]
},
{
"@search.action": "upload",
"file_id": "2",
"file_name": "secured_file_b",
"file_description": "File access is restricted to Human Resources and Recruiting.",
"group_ids": ["group_id1", "group_id2"]
},
{
"@search.action": "upload",
"file_id": "3",
"file_name": "secured_file_c",
"file_description": "File access is restricted to Operations and Logistics.",
"group_ids": ["group_id5", "group_id6"]
}
]
}
```


If you need to update an existing document with the list of groups, you can use the `merge`

or `mergeOrUpload`

action:

```
{
"value": [
{
"@search.action": "mergeOrUpload",
"file_id": "3",
"group_ids": ["group_id7", "group_id8", "group_id9"]
}
]
}
```


## Apply the security filter in the query

In order to trim documents based on `group_ids`

access, you should issue a search query with a `group_ids/any(g:search.in(g, 'group_id1, group_id2,...'))`

filter, where 'group_id1, group_id2,...' are the groups to which the search request issuer belongs.

This filter matches all documents for which the `group_ids`

field contains one of the given identifiers.
For full details on searching documents using Azure AI Search, you can read [Search Documents](/en-us/rest/api/searchservice/documents/search-post?).

This sample shows how to set up query using a POST request.

Issue the HTTP POST request, specifying the filter in the request body:

```
POST https://[service name].search.windows.net/indexes/securedfiles/docs/search?api-version=2025-09-01
{
"filter":"group_ids/any(g:search.in(g, 'group_id1, group_id2'))"
}
```


You should get the documents back where `group_ids`

contains either "group_id1" or "group_id2". In other words, you get the documents to which the request issuer has read access.

```
{
[
{
"@search.score":1.0,
"file_id":"1",
"file_name":"secured_file_a",
},
{
"@search.score":1.0,
"file_id":"2",
"file_name":"secured_file_b"
}
]
}
```


## Next steps

This article describes a pattern for filtering results based on user identity and the `search.in()`

function. You can use this function to pass in principal identifiers for the requesting user to match against principal identifiers associated with each target document. When a search request is handled, the `search.in`

function filters out search results for which none of the user's principals have read access. The principal identifiers can represent things like security groups, roles, or even the user's own identity.

For more examples, demos, and videos:


---

<!-- DOCUMENTO FUSIONADO: search-index-access-control-lists-and-rbac-push-api.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-index-access-control-lists-and-rbac-push-api -->

# Indexing document Access Control Lists (ACLs) using the push REST APIs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

Indexing documents, along with their associated [Access Control Lists (ACLs)](/en-us/azure/storage/blobs/data-lake-storage-access-control) and container [Role-Based Access Control (RBAC) roles](/en-us/azure/role-based-access-control/overview), into an Azure AI Search index via the [push REST APIs](/en-us/rest/api/searchservice/documents/?view=rest-searchservice-2025-11-01-preview&preserve-view=true) preserves document-level permission on indexed content at query time.

Key features include:

- Flexible control over ingestion pipelines.
- Standardized schema for permissions metadata.
- Support for hierarchical permissions, such as folder-level ACLs.

This article explains how to use the push REST API to index document-level permissions' metadata in Azure AI Search. This process prepares your index to query and enforce end-user permissions on search results.

## Prerequisites

Content with ACL metadata from

[Microsoft Entra ID](/en-us/entra/fundamentals/whatis)or another POSIX-style ACL system.The

[latest preview REST API](/en-us/rest/api/searchservice/documents/?view=rest-searchservice-2025-11-01-preview&preserve-view=true)or a preview Azure SDK package providing equivalent features.An index schema with a

`permissionFilterOption`

enabled, plus`permissionFilter`

field attributes that store the permissions associated with the document.

## Limitations

An ACL field with permission filter type

`userIds`

or`groupIds`

can hold at most 32 values.An index can hold at most five unique values among fields of type

`rbacScope`

on all documents. There's no limit on the number of documents that share the same value of`rbacScope`

.A preexisting field can be converted into a

`permissionFilter`

field type for use with built-in ACLs or RBAC metadata filtering. To enable filtering on an existing index, create new fields or modify an existing field to include a`permissionFilter`

.Only one field of each

`permissionFilter`

type (one each of`groupIds`

,`usersIds`

, and`rbacScope`

) can exist in an index.Each permissionFilter field should have

`filterable`

set to true.This functionality is currently not supported in the Azure portal.


## Create an index with permission filter fields

Indexing document ACLs and RBAC metadata with the REST API requires setting up an index schema that enables permission filters and has fields with permission filter assignments.

First, add a `permissionFilterOption`

option. Valid values are `enabled`

or `disabled`

, and you should set it to `enabled`

. You can switch it to `disabled`

if you want to turn off the permission filter functionality at the index level.

Second, create string fields for your permission metadata and include `permissionFilter`

. Recall that you can have one of each permission filter type.

Here's a basic example schema that includes all `permissionFilter`

types:

```
{
"fields": [
{ "name": "UserIds", "type": "Collection(Edm.String)", "permissionFilter": "userIds", "filterable": true },
{ "name": "GroupIds", "type": "Collection(Edm.String)", "permissionFilter": "groupIds", "filterable": true },
{ "name": "RbacScope", "type": "Edm.String", "permissionFilter": "rbacScope", "filterable": true },
{ "name": "DocumentId", "type": "Edm.String", "key": true }
],
"permissionFilterOption": "enabled"
}
```


## REST API indexing example

Once you have an index with permission filter fields, you can populate those values using the indexing push API as with any other document fields. Here's an example using the specified index schema, where each document specifies the upload action, the key field (DocumentId), and permission fields. It should also have content, but that field is omitted in this example for brevity.

```
POST https://exampleservice.search.windows.net/indexes('indexdocumentsexample')/docs/search.index?api-version=2025-11-01-preview
{
"value": [
{
"@search.action": "upload",
"DocumentId": "1",
"UserIds": ["00aa00aa-bb11-cc22-dd33-44ee44ee44ee", "11bb11bb-cc22-dd33-ee44-55ff55ff55ff", "22cc22cc-dd33-ee44-ff55-66aa66aa66aa"],
"GroupIds": ["none"]
"RbacScope": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Example-Storage-rg/providers/Microsoft.Storage/storageAccounts/azurestorage12345/blobServices/default/containers/blob-container-01"
},
{
"@search.action": "merge",
"DocumentId": "2",
"UserIds": ["all"],
"GroupIds": ["33dd33dd-ee44-ff55-aa66-77bb77bb77bb", "44ee44ee-ff55-aa66-bb77-88cc88cc88cc"]
},
{
"@search.action": "mergeOrUpload",
"DocumentId": "3",
"UserIds": ["1cdd8521-38cf-49ab-b483-17ddaa48f68f"],
"RbacScope": "/subscriptions/00000000-0000-0000-0000-000000000000/resourceGroups/Example-Storage-rg/providers/Microsoft.Storage/storageAccounts/azurestorage12345/blobServices/default/containers/blob-container-03"
}
]
}
```


## ACL access resolution rules

This section explains how document access is determined for a user based on the ACL values assigned to each document. The key rule is that *a user only needs to match one ACL type to gain access to the document*. For example, if a document has fields for `userIds`

, `groupIds`

, and `rbacScope`

, the user can access the document by matching any one of these ACL fields.

### Special ACL values "all" and "none"

ACL fields, such as `userIds`

and `groupIds`

, typically contain lists of GUIDs (Globally Unique Identifiers) that identify the users and groups with access to the document. Two special string values, "all" and "none", are supported for these ACL field types. These values act as broad filters to control access at the global level as showcased in the following table.

| userIds / groupIds value | Meaning |
|---|---|
| ["all"] | Any user can access the document |
| ["none"] | No user can access the document by matching this ACL type |
| [] (empty array) | No user can access the document by matching this ACL type |

Because a user needs to match only one field type, the special value "all" grants public access regardless of the contents of any other ACL field, as all users are matched and granted permission. In contrast, setting `userIds`

to "none" or "empty" means no users are granted access to the document *based on their user ID*. It might be possible that they're still granted access by matching their group ID or by RBAC metadata.

### Access control example

This example illustrates how the document access rules are resolved based on the specific document ACL field values. For readability, this scenario uses ACL aliases such as "user1," "group1," instead of GUIDs.

| Document # | userIds | groupIds | RBAC Scope | Permitted users list | Note |
|---|---|---|---|---|---|
| 1 | ["none"] | [] | Empty | No users have access | The values ["none"] and [] behave exactly the same |
| 2 | ["none"] | [] | scope/to/container1 | Users with RBAC permissions to container1 | The value of "none" doesn't block access by matching other ACL fields |
| 3 | ["none"] | ["group1", "group2"] | Empty | Members of group1 or group2 | |
| 4 | ["all"] | ["none"] | Empty | Any user | Any querying user matches the ACL filter "all", so all users have access |
| 5 | ["all"] | ["group1", "group2"] | scope/to/container1 | Any user | Since all users match the "all" filter for userID, the groupID and RBAC filters don't have any impact |
| 6 | ["user1", "user2"] | ["group1"] | Empty | User1, user2, or any member of group1 | |
| 7 | ["user1", "user2"] | [] | Empty | User1, user2, or any user with RBAC permissions to container1 |
