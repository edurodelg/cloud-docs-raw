---
source_url: https://learn.microsoft.com/en-us/azure/search/search-security-rbac
fetched_at: 2026-01-25T03:12:19.919153
---

# Connect to Azure AI Search using roles

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure provides global authentication and [role-based access control](/en-us/azure/role-based-access-control/role-assignments-portal) through Microsoft Entra ID for all services running on the platform. In this article, learn which roles provide access to search content and administration on Azure AI Search.

In Azure AI Search, you can assign Azure roles for:

[Service administration](#assign-roles-for-service-administration)[Development or write-access to a search service](#assign-roles-for-development)[Read-only access for queries](#assign-roles-for-read-only-queries)[Scoped access to a single index](#grant-access-to-a-single-index)

Per-user access over search results (sometimes referred to as *row-level security* or *document-level access*) is supported through permission inheritance for Azure Data Lake Storage (ADLS) Gen2 and Azure blob indexes and through security filters for all other platforms (see [Document-level access control](search-document-level-access-overview)).

Role assignments are cumulative and pervasive across all tools and client libraries. You can assign roles by using any of the [supported approaches](/en-us/azure/role-based-access-control/role-assignments-steps) described in Azure role-based access control documentation.

Role-based access is optional, but recommended. The alternative is [key-based authentication](search-security-api-keys), which is the default.

### Quick reference: Roles by task

| Task | Required role(s) |
|---|---|
| Create or manage indexes, indexers, skillsets | Search Service Contributor |
| Load documents into an index | Search Index Data Contributor |
| Query an index | Search Index Data Reader |
| Full development access | Search Service Contributor + Search Index Data Contributor + Search Index Data Reader |
| Service administration | Owner or Contributor |

## Prerequisites

A search service in any region, on any tier,

[enabled for role-based access](search-security-enable-roles).Owner, User Access Administrator, Role-based Access Control Administrator, or a custom role with

[Microsoft.Authorization/roleAssignments/write](/en-us/azure/templates/microsoft.authorization/roleassignments)permissions.

## Built-in roles used in search

Roles are a collection of permissions on specific operations that affect either data plane or control plane layers.

*Data plane* refers to operations against the search service endpoint, such as indexing or queries, or any other operation specified in the [Search Service REST APIs](/en-us/rest/api/searchservice/) or equivalent Azure SDK client libraries.

*Control plane* refers to Azure resource management, such as creating or configuring a search service.

The following roles are built in. If these roles don't meet your needs, [create a custom role](#create-a-custom-role).

| Role | Plane | Description |
|---|---|---|
|

On the data plane, this role has the same access as the Search Service Contributor role. It includes access to all data plane actions except the ability to query documents.

[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)On the data plane, this role has the same access as the Search Service Contributor role. It includes access to all data plane actions except the ability to query or index documents.

[Reader](/en-us/azure/role-based-access-control/built-in-roles#reader)[Search Service Contributor](/en-us/azure/role-based-access-control/built-in-roles#search-service-contributor)[for the permissions list.](/en-us/azure/role-based-access-control/resource-provider-operations#microsoftsearch)`Microsoft.Search/searchServices/*`

[Search Index Data Contributor](/en-us/azure/role-based-access-control/built-in-roles#search-index-data-contributor)[Grant access to a single index](#grant-access-to-a-single-index)to narrow the scope.[Search Index Data Reader](/en-us/azure/role-based-access-control/built-in-roles#search-index-data-reader)[Grant access to a single index](#grant-access-to-a-single-index)to narrow the scope.Combine these roles to get sufficient permissions for your use case.

Note

If you disable Azure role-based access, built-in roles for the control plane (Owner, Contributor, Reader) continue to be available. Disabling role-based access removes just the data-related permissions associated with those roles. If you disable data plane roles, Search Service Contributor is equivalent to control-plane Contributor.

## Summary of permissions

| Permissions | Search Index Data Reader | Search Index Data Contributor | Search Service Contributor | Owner/Contributor | Reader |
|---|---|---|---|---|---|
| View the resource in Azure portal | ❌ | ❌ | ✅ | ✅ | ✅ |
| View resource properties, metrics, and endpoint | ❌ | ❌ | ✅ | ✅ | ✅ |
| List all objects on the resource | ❌ | ❌ | ✅ | ✅ | ✅ |
| Access quotas and service statistics | ❌ | ❌ | ✅ | ✅ | ❌ |
| Read and query an index | ✅ | ✅ | ❌ | ❌ | ❌ |
Upload data for indexing 1 |
❌ | ✅ | ❌ | ❌ | ❌ |
Elevated read regardless of permission filters 2 |
❌ | ✅ | ❌ | ❌ | ❌ |
| Create or edit indexes and aliases | ❌ | ❌ | ✅ | ✅ | ❌ |
| Create, edit, and run indexers, data sources, and skillsets | ❌ | ❌ | ✅ | ✅ | ❌ |
| Create or edit synonym maps | ❌ | ❌ | ✅ | ✅ | ❌ |
| Create or edit debug sessions | ❌ | ❌ | ✅ | ✅ | ❌ |
| Create or manage deployments | ❌ | ❌ | ✅ | ✅ | ❌ |
| Create or configure Azure AI Search resources | ❌ | ❌ | ✅ | ✅ | ❌ |
| View, copy, and regenerate keys under Keys | ❌ | ❌ | ✅ | ✅ | ❌ |
| View roles, policies, and definitions | ❌ | ❌ | ✅ | ✅ | ❌ |
| Set authentication options | ❌ | ❌ | ✅ | ✅ | ❌ |
| Configure private connections | ❌ | ❌ | ✅ | ✅ | ❌ |
| Configure network security | ❌ | ❌ | ✅ | ✅ | ❌ |

1 In the Azure portal, an Owner or Contributor can run the Import data wizards that create and load indexes, even though they can't upload documents in other clients. The search service itself, not individual users, makes data connections in the wizard. The wizards have the `Microsoft.Search/searchServices/indexes/documents/*`

permission necessary for completing this task.

2 Use elevated read for debugging queries that obtain results by using the identity of the called. For more information, see [Investigate incorrect query results](search-query-access-control-rbac-enforcement#elevated-permissions-for-investigating-incorrect-results).

Owners and Contributors grant the same permissions, except that only Owners can assign roles.

## Assign roles

In this section, assign roles for:

- Service administration
- Development or write access to a search service
- Read-only access for queries

### Assign roles for service administration

As a service administrator, you can create and configure a search service, and perform all control plane operations described in the [Management REST API](/en-us/rest/api/searchmanagement/) or equivalent client libraries. If you're an Owner or Contributor, you can also perform most data plane [Search REST API](/en-us/rest/api/searchservice/) tasks in the Azure portal.

| Role | ID |
|---|---|
`Owner` |

`Contributor`

`Reader`

Sign in to the

[Azure portal](https://portal.azure.com).Select

**Access Control (IAM)**in the left pane.Select

**+ Add**>**Add role assignment**to start the**Add role assignment**wizard.Select a role.

- Owner (full access to all data plane and control plane operations, except for query permissions)
- Contributor (same as Owner, except for permissions to assign roles)
- Reader (acceptable for monitoring and viewing metrics)

On the

**Members**tab, select the Microsoft Entra user or group identity. If you're setting up permissions for another Azure service, select a system or user-managed identity.On the

**Review + assign**tab, select**Review + assign**to assign the role.

### Assign roles for development

Role assignments apply globally across the search service. To [scope permissions to a single index](#rbac-single-index), use PowerShell or the Azure CLI to create a custom role.

| Task | Role | ID |
|---|---|---|
| Create or manage objects |
`Search Service Contributor` |

`Search Index Data Contributor`

`Search Index Data Reader`

Another combination of roles that provides full access is Contributor or Owner, plus Search Index Data Reader.

Important

If you configure role-based access for a service or index and you also provide an API key on the request, the search service uses the API key to authenticate.

Sign in to the

[Azure portal](https://portal.azure.com).Select

**Access Control (IAM)**in the left pane.Select

**+ Add**>**Add role assignment**to start the**Add role assignment**wizard.Select a role.

- Search Service Contributor (create, read, update, and delete operations on indexes, indexers, skillsets, and other top-level objects)
- Search Index Data Contributor (load documents and run indexing jobs)
- Search Index Data Reader (query an index)

On the

**Members**tab, select the Microsoft Entra user or group identity. If you're setting up permissions for another Azure service, select a system or user-managed identity.On the

**Review + assign**tab, select**Review + assign**to assign the role.

### Assign roles for read-only queries

Use the Search Index Data Reader role for apps and processes that only need read access to an index.

| Role | ID |
|---|---|
`Search Index Data Reader` |

[with PowerShell](search-security-rbac#grant-access-to-a-single-index)

This role is very specific. It grants [GET or POST access](/en-us/rest/api/searchservice/documents) to the *documents collection of a search index* for search, autocomplete, and suggestions. It doesn't support GET or LIST operations on an index or other top-level objects, or GET service statistics.

This section provides basic steps for setting up the role assignment and is here for completeness, but for comprehensive instructions on configuring your app for role-based access, see [Use Azure AI Search without keys](search-security-rbac-client-code).

Note

As a developer, if you need to debug queries that are predicated on a Microsoft identity, use Search Index Data Contributor or create a custom role that gives you [elevated permissions for debug purposes](search-query-access-control-rbac-enforcement#elevated-permissions-for-investigating-incorrect-results).

Sign in to the

[Azure portal](https://portal.azure.com).Select

**Access Control (IAM)**in the left pane.Select

**+ Add**>**Add role assignment**to start the**Add role assignment**wizard.Select the

**Search Index Data Reader**role.On the

**Members**tab, select the Microsoft Entra user or group identity. If you're setting up permissions for another Azure service, select a system or user-managed identity.On the

**Review + assign**tab, select**Review + assign**to assign the role.

## Test role assignments

Use a client to test role assignments. Remember that roles are cumulative. You can't delete or deny inherited roles that are scoped to the subscription or resource group level at the resource (search service) level.

[Configure your application for keyless connections](search-security-rbac-client-code) and have role assignments in place before testing.

Sign in to the

[Azure portal](https://portal.azure.com).Navigate to your search service.

On the Overview page, select the

**Indexes**tab:Search Service Contributors can view and create any object, but can't load documents or query an index. To verify permissions,

[create a search index](search-how-to-create-search-index#create-an-index).Search Index Data Contributors can load documents. There's no load documents option in the Azure portal outside of Import data wizard, but you can

[reset and run an indexer](search-howto-run-reset-indexers)to confirm document load permissions.Search Index Data Readers can query the index. To verify permissions, use

[Search explorer](search-explorer). You should be able to send queries and view results, but you shouldn't be able to view the index definition or create one.


## Test as current user

If you're already a Contributor or Owner of your search service, you can use a bearer token for your user identity to authenticate to Azure AI Search.

Get a bearer token for the current user by using the Azure CLI:

`az account get-access-token --scope https://search.azure.com/.default`

Or use PowerShell:

`Get-AzAccessToken -ResourceUrl https://search.azure.com`

Paste these variables into a new text file in Visual Studio Code.

`@baseUrl = PASTE-YOUR-SEARCH-SERVICE-URL-HERE @index-name = PASTE-YOUR-INDEX-NAME-HERE @token = PASTE-YOUR-TOKEN-HERE`

Paste in and then send a request to confirm access. Here's one that queries the hotels-quickstart index.

`POST https://{{baseUrl}}/indexes/{{index-name}}/docs/search?api-version=2025-09-01 HTTP/1.1 Content-type: application/json Authorization: Bearer {{token}} { "queryType": "simple", "search": "motel", "filter": "", "select": "HotelName,Description,Category,Tags", "count": true }`


## Grant access to a single index

In some scenarios, you might want to limit an application's access to a single resource, such as an index.

The Azure portal doesn't currently support role assignments at this level of granularity, but you can assign roles using [PowerShell](/en-us/azure/role-based-access-control/role-assignments-powershell) or the [Azure CLI](/en-us/azure/role-based-access-control/role-assignments-cli).

In PowerShell, use [New-AzRoleAssignment](/en-us/powershell/module/az.resources/new-azroleassignment), providing the Azure user or group name, and the scope of the assignment.

Load the

`Azure`

and`AzureAD`

modules and connect to your Azure account:`Import-Module -Name Az Import-Module -Name AzureAD Connect-AzAccount`

Add a role assignment scoped to an individual index:

`New-AzRoleAssignment -ObjectId <objectId> ` -RoleDefinitionName "Search Index Data Contributor" ` -Scope "/subscriptions/<subscription>/resourceGroups/<resource-group>/providers/Microsoft.Search/searchServices/<search-service>/indexes/<index-name>"`


## Create a custom role

If [built-in roles](#built-in-roles-used-in-search) don't provide the right combination of permissions, you can create a [custom role](/en-us/azure/role-based-access-control/custom-roles) to support the operations you require.

This example clones **Search Index Data Reader** and then adds the ability to list indexes by name. Normally, listing the indexes on a search service is considered an administrative right.

These steps are derived from [Create or update Azure custom roles using the Azure portal](/en-us/azure/role-based-access-control/custom-roles-portal). A search service page supports cloning from an existing role.

These steps create a custom role that augments search query rights to include listing indexes by name. Typically, listing indexes is considered an admin function.

In the Azure portal, go to your search service.

In the left-navigation pane, select

**Access Control (IAM)**.In the action bar, select

**Roles**.Right-click

**Search Index Data Reader**(or another role) and select**Clone**to open the**Create a custom role**wizard.On the Basics tab, provide a name for the custom role, such as "Search Index Data Explorer", and then select

**Next**.On the Permissions tab, select

**Add permission**.On the Add permissions tab, search for and then select the

**Microsoft Search**tile.Set the permissions for your custom role. At the top of the page, use the default

**Actions**selection:- Under Microsoft.Search/operations, select
**Read : List all available operations**. - Under Microsoft.Search/searchServices/indexes, select
**Read : Read Index**.

- Under Microsoft.Search/operations, select
On the same page, switch to

**Data actions**and under Microsoft.Search/searchServices/indexes/documents, select**Read : Read Documents**.The JSON definition looks like the following example:

`{ "properties": { "roleName": "search index data explorer", "description": "", "assignableScopes": [ "/subscriptions/0000000000000000000000000000000/resourceGroups/free-search-svc/providers/Microsoft.Search/searchServices/demo-search-svc" ], "permissions": [ { "actions": [ "Microsoft.Search/operations/read", "Microsoft.Search/searchServices/indexes/read" ], "notActions": [], "dataActions": [ "Microsoft.Search/searchServices/indexes/documents/read" ], "notDataActions": [] } ] } }`

Select

**Review + create**to create the role. You can now assign users and groups to the role.

## Conditional Access

If you need to enforce organizational policies, such as multifactor authentication, use [Microsoft Entra Conditional Access](/en-us/entra/identity/conditional-access/overview).

To enable a Conditional Access policy for Azure AI Search, follow these steps:

[Sign in](https://portal.azure.com)to the Azure portal.Search for

**Microsoft Entra Conditional Access**.Select

**Policies**.Select

**New policy**.In the

**Cloud apps or actions**section of the policy, add**Azure AI Search**as a cloud app depending on how you want to set up your policy.Update the remaining parameters of the policy. For example, specify which users and groups this policy applies to.

Save the policy.


Important

If your search service has a managed identity assigned to it, the specific search service shows up as a cloud app that you can include or exclude as part of the Conditional Access policy. You can't enforce Conditional Access policies on a specific search service. Instead, make sure you select the general **Azure AI Search** cloud app.

## Troubleshooting role-based access control issues

When you develop applications that use role-based access control for authentication, you might encounter some common problems:

If the authorization token comes from a

[managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview)and you recently assigned the appropriate permissions, it[might take several hours](/en-us/entra/identity/managed-identities-azure-resources/managed-identity-best-practice-recommendations#limitation-of-using-managed-identities-for-authorization)for these permissions assignments to take effect.The default configuration for a search service is

[key-based authentication](search-security-api-keys). If you don't change the default key setting to**Both**or**Role-based access control**, then all requests by using role-based authentication are automatically denied regardless of the underlying permissions.