---
merged_at: 2026-01-25T03:18:13.736674
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-howto-move-across-regions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-howto-move-across-regions -->

# Move your Azure AI Search service to another Azure region

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Occasionally, customers ask about moving a search service to another region. Currently, there's no built-in mechanism or tooling to help with that task, but this article can help you understand the manual steps for recreating indexes and other objects on a new search service in a different region.

Note

In the Azure portal, all services have an **Export template** command. In the case of Azure AI Search, this command produces a basic definition of a service (name, location, tier, replica, and partition count), but does not recognize the content of your service, nor does it carry over keys, roles, or logs. Although the command exists, we don't recommend using it for moving a search service.

## Prerequisites

Ensure that the services and features that your account uses are supported in the target region.

For preview features, ensure that your subscription is approved for the target region.


## Prepare and move

Identify dependencies and related services to understand the full impact of relocating a service, in case you need to move more than just Azure AI Search.

Azure Storage is used for logging, creating a knowledge store, and is a commonly used external data source for AI enrichment and indexing. Foundry Tools are used to power built-in skills during AI enrichment. Both Foundry Tools and your search service are required to be in the same region if you're using AI enrichment.

Create an inventory of all objects on the service so that you know what to move: indexes, synonym maps, indexers, data sources, skillsets. If you enabled logging, create and archive any reports you might need for a historical record.

Check pricing and availability in the new region to ensure availability of Azure AI Search plus any related services in the new region. Most features are available in all regions, but some preview features have restricted availability.

Create a service in the new region and republish from source code any existing indexes, synonym maps, indexers, data sources, and skillsets. Remember that service names must be unique so you can't reuse the existing name. Check each skillset to see if connections to Foundry Tools are still valid in terms of the same-region requirement. Also, if knowledge stores are created, check the connection strings for Azure Storage if you're using a different service.

Reload indexes and knowledge stores, if applicable. You'll either use application code to push JSON data into an index, or rerun indexers to pull documents in from external sources.

Enable logging, and if you're using them, re-create security roles.

Update client applications and test suites to use the new service name and API keys, and test all applications.


## Discard or clean up

Delete the old service once the new service is fully tested and operational. Deleting the service automatically deletes all content associated with the service.

## Next steps

The following links can help you locate more information when completing the steps outlined above.


---

<!-- DOCUMENTO FUSIONADO: search-more-like-this.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-more-like-this -->

# moreLikeThis (preview) in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This feature is in public preview under [Supplemental Terms of Use](https://azure.microsoft.com/support/legal/preview-supplemental-terms/). The [preview REST API](/en-us/rest/api/searchservice/index-preview) supports this feature.

`moreLikeThis=[key]`

is a query parameter in the [Search Documents API](/en-us/rest/api/searchservice/documents/search-post) that finds documents similar to the document specified by the document key. When a search request is made with `moreLikeThis`

, a query is generated with search terms extracted from the given document that describe that document best. The generated query is then used to make the search request. The `moreLikeThis`

parameter can't be used with the search parameter, `search=[string]`

.

By default, the contents of all top-level searchable fields are considered. If you want to specify particular fields instead, you can use the `searchFields`

parameter.

The `moreLikeThis`

parameter isn't supported for [complex types](search-howto-complex-data-types) and the presence of complex types will impact your query logic. If your index is a complex type, you must set `searchFields`

to the top-level searchable fields over which `moreLikeThis`

iterates. For example, if the index has a searchable `field1`

of type `Edm.String`

, and `field2`

that's a complex type with searchable subfields, the value of `searchFields`

must be set to `field1`

to exclude `field2`

.

## Examples

All following examples use the hotels sample from [Quickstart: Full-text search in the Azure portal](search-get-started-portal).

### Simple query

The following query finds documents whose description fields are most similar to the field of the source document as specified by the `moreLikeThis`

parameter:

```
GET /indexes/hotels-sample-index/docs?moreLikeThis=29&searchFields=Description&api-version=2024-05-01-preview
```


In this example, the request searches for hotels similar to the one with `HotelId`

29.
Rather than using HTTP GET, you can also invoke `MoreLikeThis`

using HTTP POST:

```
POST /indexes/hotels-sample-index/docs/search?api-version=2024-05-01-preview
{
"moreLikeThis": "29",
"searchFields": "Description"
}
```


### Apply filters

`MoreLikeThis`

can be combined with other common query parameters like `$filter`

. For instance, the query can be restricted to only hotels whose category is 'Budget' and where the rating is higher than 3.5:

```
GET /indexes/hotels-sample-index/docs?moreLikeThis=20&searchFields=Description&$filter=(Category eq 'Budget' and Rating gt 3.5)&api-version=2024-05-01-preview
```


### Select fields and limit results

The `$top`

selector can be used to limit how many results should be returned in a `MoreLikeThis`

query. Also, fields can be selected with `$select`

. Here the top three hotels are selected along with their ID, Name, and Rating:

```
GET /indexes/hotels-sample-index/docs?moreLikeThis=20&searchFields=Description&$filter=(Category eq 'Budget' and Rating gt 3.5)&$top=3&$select=HotelId,HotelName,Rating&api-version=2024-05-01-preview
```


## Next steps

You can use any REST client for this exercise.
