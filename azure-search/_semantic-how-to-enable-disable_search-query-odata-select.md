---
merged_at: 2026-01-25T02:11:57.861485
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: semantic-how-to-enable-disable.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/semantic-how-to-enable-disable -->

# Enable or disable semantic ranker

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Semantic ranker is a premium feature billed by usage. By default, semantic ranker is enabled on a new billable search service and it's configured for the free plan, but anyone with *Contributor* permissions can disable it or change the billing plan. If you don't want anyone to use the feature, you can [disable it service-wide using the management REST API](#disable-semantic-ranker-using-the-rest-api). If you disable semantic ranking, you also disable [agentic retrieval](agentic-retrieval-overview).

## Check availability

To check if semantic ranker is available in your region, see the [Azure AI Search regions list](search-region-support).

## Enable semantic ranker

Semantic ranker might not be enabled on older services. Follow these steps to enable [semantic ranker](semantic-search-overview) at the service level. Once enabled, it's available to all indexes. You can't turn it on or off for specific indexes.

Open the

[Azure portal](https://portal.azure.com).Navigate to your search service. On the

**Overview**page, make sure the pricing tier is set to**Basic**or higher.On the left-navigation pane, select

**Settings**>**Premium features**.Select either the

**Free plan**(default) or the**Standard plan**. You can switch between the free plan and the standard plan at any time.

The free plan is capped at 1,000 queries per month. After the first 1,000 queries in the free plan, an error message indicates you exhausted your quota on the next semantic query. When quota is exhausted, you can upgrade to the standard plan to continue using semantic ranking.

## Disable semantic ranker using the REST API

To turn off feature enablement, or for full protection against accidental usage and charges, you can disable semantic ranker by using the [Create or Update Service API](/en-us/rest/api/searchmanagement/services/create-or-update#searchsemanticsearch) on your search service. After the feature is disabled, any requests that include the semantic query type are rejected.

Management REST API calls are authenticated through Microsoft Entra ID. For instructions on how to authenticate, see [Manage your Azure AI Search service with REST APIs](search-manage-rest).

```
PATCH https://management.azure.com/subscriptions/{{subscriptionId}}/resourcegroups/{{resource-group}}/providers/Microsoft.Search/searchServices/{{search-service-name}}?api-version=2025-05-01
{
"properties": {
"semanticSearch": "disabled"
}
}
```


To re-enable semantic ranker, run the previous request again and set `semanticSearch`

to either **Free** (default) or **Standard**.


---

<!-- DOCUMENTO FUSIONADO: search-query-odata-select.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-odata-select -->

# OData $select syntax in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, the **$select** parameter specifies which fields to include in search results. This article describes the OData syntax of **$select** and provides examples.

Field path construction and constants are described in the [OData language overview in Azure AI Search](query-odata-filter-orderby-syntax). For more information about search result composition, see [How to work with search results in Azure AI Search](search-pagination-page-layout).

## Syntax

The **$select** parameter determines which fields for each document are returned in the query result set. The following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) defines the grammar for the **$select** parameter:

```
select_expression ::= '*' | field_path(',' field_path)*
field_path ::= identifier('/'identifier)*
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

The **$select** parameter comes in two forms:

- A single star (
`*`

), indicating that all retrievable fields should be returned, or - A comma-separated list of field paths, identifying which fields should be returned.

When using the second form, you may only specify retrievable fields in the list.

If you list a complex field without specifying its subfields explicitly, all retrievable subfields will be included in the query result set. For example, assume your index has an `Address`

field with `Street`

, `City`

, and `Country`

subfields that are all retrievable. If you specify `Address`

in **$select**, the query results will include all three subfields.

## Examples

Include the `HotelId`

, `HotelName`

, and `Rating`

top-level fields in the results, and include the `City`

subfield of `Address`

:

```
$select=HotelId, HotelName, Rating, Address/City
```


An example result might look like this:

```
{
"HotelId": "1",
"HotelName": "Stay-Kay City Hotel",
"Rating": 4,
"Address": {
"City": "New York"
}
}
```


Include the `HotelName`

top-level field in the results. Include all subfields of `Address`

. Include the `Type`

and `BaseRate`

subfields of each object in the `Rooms`

collection:

```
$select=HotelName, Address, Rooms/Type, Rooms/BaseRate
```


An example result might look like this:

```
{
"HotelName": "Stay-Kay City Hotel",
"Rating": 4,
"Address": {
"StreetAddress": "677 5th Ave",
"City": "New York",
"StateProvince": "NY",
"Country": "USA",
"PostalCode": "10022"
},
"Rooms": [
{
"Type": "Budget Room",
"BaseRate": 9.69
},
{
"Type": "Budget Room",
"BaseRate": 8.09
}
]
}
```
