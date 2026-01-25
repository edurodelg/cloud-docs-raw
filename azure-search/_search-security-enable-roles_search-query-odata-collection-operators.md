---
merged_at: 2026-01-25T03:18:13.753120
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-security-enable-roles.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-security-enable-roles -->

# Enable or disable role-based access control in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to enable role-based access control (RBAC) for data plane operations on Azure AI Search. With RBAC enabled, you can use Microsoft Entra ID authentication instead of API keys.

Important

When you create a search service, key-based authentication is the default, but it's not the most secure option. We recommend that you replace it with role-based access as described in this article.

Only [data plane](/en-us/azure/azure-resource-manager/management/control-plane-and-data-plane) roles can be disabled. Roles for service administration (control plane) are built in and can't be enabled or disabled.

If you observe key-related activity, such as Get Admin Keys, in the **Activity Log** on a roles-only search service, those actions are initiated on the control plane and don't affect your content or content-related operations.

## Prerequisites

- A search service in any region, on any tier, including free.
**Owner**,**User Access Administrator**, or a custom role with[Microsoft.Authorization/roleAssignments/write](/en-us/azure/templates/microsoft.authorization/roleassignments)permissions to enable RBAC.- After enabling RBAC, you need data plane roles to access content:
**Search Service Contributor**,**Search Index Data Contributor**, and**Search Index Data Reader**. See[Assign roles](search-security-rbac)for details.

## Enable role-based access for data plane operations

Configure your search service to recognize an **authorization** header on data requests that provide an OAuth2 access token.

When you enable roles for the data plane, the change is effective immediately, but wait a few seconds before assigning roles.

The default failure mode for unauthorized requests is `http401WithBearerChallenge`

. Alternatively, you can set the failure mode to `http403`

.

Sign in to the

[Azure portal](https://portal.azure.com)and navigate to your search service.Select

**Settings**and then select**Keys**in the left pane.Choose

**Role-based control**. Only choose**Both**if you're currently using keys and need time to transition clients to role-based access control.Option Description API Key (default) Requires [API keys](search-security-api-keys)on the request header for authorization.Role-based access control (recommended) Requires membership in a role assignment to complete the task. It also requires an authorization header on the request. Both Requests are valid using either an API key or role-based access control, but if you provide both in the same request, the API key is used. As an administrator, if you choose a roles-only approach,

[assign data plane roles](search-security-rbac)to your user account to restore full administrative access over data plane operations in the Azure portal. Roles include Search Service Contributor, Search Index Data Contributor, and Search Index Data Reader. You need the first two roles if you want equivalent access.Sometimes it can take five to ten minutes for role assignments to take effect. Until that happens, the following message appears in the Azure portal pages used for data plane operations.


## Disable role-based access control

It's possible to disable role-based access control for data plane operations and use key-based authentication instead. You might do this as part of a test workflow, for example to rule out permission issues.

To disable role-based access control in the Azure portal:

Sign in to the

[Azure portal](https://portal.azure.com)and open the search service page.Select

**Settings**and then select**Keys**in the left pane.Select

**API Keys**.

## Disable API key authentication

[Key access](search-security-api-keys), or local authentication, can be disabled on your service if you're exclusively using the built-in roles and Microsoft Entra authentication. Disabling API keys causes the search service to refuse all data-related requests that pass an API key in the header.

Admin API keys can be disabled, but not deleted. Query API keys can be deleted.

Owner or Contributor permissions are required to disable security features.

In the Azure portal, navigate to your search service.

In the left-navigation pane, select

**Keys**.Select

**Role-based access control**.

The change is effective immediately, but wait a few seconds before testing. Assuming you have permission to assign roles as a member of Owner, service administrator, or coadministrator, you can use portal features to test role-based access.


---

<!-- DOCUMENTO FUSIONADO: search-query-odata-collection-operators.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-odata-collection-operators -->

# OData collection operators in Azure AI Search - any and all

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

# OData collection operators in Azure AI Search -

When writing an [OData filter expression](query-odata-filter-orderby-syntax) to use with Azure AI Search, it's often useful to filter on collection fields. You can achieve this using the `any`

and `all`

operators.

## Syntax

The following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) defines the grammar of an OData expression that uses `any`

or `all`

.

```
collection_filter_expression ::=
field_path'/all(' lambda_expression ')'
| field_path'/any(' lambda_expression ')'
| field_path'/any()'
lambda_expression ::= identifier ':' boolean_expression
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

There are three forms of expression that filter collections.

- The first two iterate over a collection field, applying a predicate given in the form of a lambda expression to each element of the collection.
- An expression using
`all`

returns`true`

if the predicate is true for every element of the collection. - An expression using
`any`

returns`true`

if the predicate is true for at least one element of the collection.

- An expression using
- The third form of collection filter uses
`any`

without a lambda expression to test whether a collection field is empty. If the collection has any elements, it returns`true`

. If the collection is empty, it returns`false`

.

A **lambda expression** in a collection filter is like the body of a loop in a programming language. It defines a variable, called the **range variable**, that holds the current element of the collection during iteration. It also defines another boolean expression that is the filter criteria to apply to the range variable for each element of the collection.

## Examples

Match documents whose `tags`

field contains exactly the string "wifi":

```
tags/any(t: t eq 'wifi')
```


Match documents where every element of the `ratings`

field falls between 3 and 5, inclusive:

```
ratings/all(r: r ge 3 and r le 5)
```


Match documents where any of the geo coordinates in the `locations`

field is within the given polygon:

```
locations/any(loc: geo.intersects(loc, geography'POLYGON((-122.031577 47.578581, -122.031577 47.678581, -122.131577 47.678581, -122.031577 47.578581))'))
```


Match documents where the `rooms`

field is empty:

```
not rooms/any()
```


Match documents where (for all rooms) the `rooms/amenities`

field contains "tv", and `rooms/baseRate`

is less than 100:

```
rooms/all(room: room/amenities/any(a: a eq 'tv') and room/baseRate lt 100.0)
```


## Limitations

Not every feature of filter expressions is available inside the body of a lambda expression. The limitations differ depending on the data type of the collection field that you want to filter. The following table summarizes the limitations.

| Data type | Features allowed in lambda expressions with `any` |
Features allowed in lambda expressions with `all` |
|---|---|---|
`Collection(Edm.ComplexType)` |
Everything except `search.ismatch` and `search.ismatchscoring` |
Same |
`Collection(Edm.String)` |
Comparisons with `eq` or `search.in` Combining sub-expressions with `or` |
Comparisons with `ne` or `not search.in()` Combining sub-expressions with `and` |
`Collection(Edm.Boolean)` |
Comparisons with `eq` or `ne` |
Same |
`Collection(Edm.GeographyPoint)` |
Using `geo.distance` with `lt` or `le` `geo.intersects` Combining sub-expressions with `or` |
Using `geo.distance` with `gt` or `ge` `not geo.intersects(...)` Combining sub-expressions with `and` |
`Collection(Edm.DateTimeOffset)` , `Collection(Edm.Double)` , `Collection(Edm.Int32)` , `Collection(Edm.Int64)` |
Comparisons using `eq` , `ne` , `lt` , `gt` , `le` , or `ge` Combining comparisons with other sub-expressions using `or` Combining comparisons except `ne` with other sub-expressions using `and` Expressions using combinations of `and` and `or` in
|
Comparisons using `eq` , `ne` , `lt` , `gt` , `le` , or `ge` Combining comparisons with other sub-expressions using `and` Combining comparisons except `eq` with other sub-expressions using `or` Expressions using combinations of `and` and `or` in
|

For more details on these limitations as well as examples, see [Troubleshooting collection filters in Azure AI Search](search-query-troubleshoot-collection-filters). For more in-depth information on why these limitations exist, see [Understanding collection filters in Azure AI Search](search-query-understand-collection-filters).
