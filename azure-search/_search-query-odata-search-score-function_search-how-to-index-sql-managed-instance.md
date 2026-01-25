---
merged_at: 2026-01-25T03:18:13.732336
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-query-odata-search-score-function.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-odata-search-score-function -->

# OData search.score function in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

# OData

When you send a query to Azure AI Search without the [ $orderby parameter](search-query-odata-orderby), the results that come back will be sorted in descending order by relevance score. Even when you do use

**$orderby**, the relevance score is used to break ties by default. However, sometimes it's useful to use the relevance score as an initial sort criteria, and some other criteria as the tie-breaker. The example in this article demonstrates using the

`search.score`

function for sorting.Note

The relevance score is computed by the relevance ranking algorithm, and the range varies depending on which algorithm you use. For more information, see [Relevance and scoring in Azure AI Search](index-similarity-and-scoring).

## Syntax

The syntax for `search.score`

in **$orderby** is `search.score()`

. The function `search.score`

doesn't take any parameters. It can be used with the `asc`

or `desc`

sort-order specifier, just like any other clause in the **$orderby** parameter. It can appear anywhere in the list of sort criteria.

## Example

Sort hotels in descending order by `search.score`

and `rating`

, and then in ascending order by distance from the given coordinates so that between two hotels with identical ratings, the closest one is listed first:

```
search.score() desc,rating desc,geo.distance(location, geography'POINT(-122.131577 47.678581)') asc
```


---

<!-- DOCUMENTO FUSIONADO: search-how-to-index-sql-managed-instance.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-index-sql-managed-instance -->

# Indexer connections to Azure SQL Managed Instance through a public endpoint

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Indexers in Azure AI Search connect to external data sources over a public endpoint. If you're setting up an [Azure SQL indexer](search-how-to-index-sql-database) for a connection to a SQL managed instance, follow the steps in this article to ensure the public endpoint is set up correctly.

Alternatively, for private connections, [create a shared private link](search-indexer-how-to-access-private-sql) instead.

Note

[Always Encrypted](/en-us/sql/relational-databases/security/encryption/always-encrypted-database-engine) columns are not currently supported by Azure AI Search indexers.

## Enable a public endpoint

This article highlights just the steps for an indexer connection in Azure AI Search. If you want more background, see [Configure public endpoint in Azure SQL Managed Instance](/en-us/azure/azure-sql/managed-instance/public-endpoint-configure) instead.

For a new SQL Managed Instance, create the resource with the

**Enable public endpoint**option selected.Alternatively, if the instance already exists, you can enable public endpoint on an existing SQL Managed Instance under

**Security**>**Networking**>**Public endpoint**>**Enable**.

## Get public endpoint connection string

To get a connection string, go to

**Settings**>**Connection strings**.Copy the connection string to use in the search indexer's data source connection. Be sure to copy the connection string for the

**public endpoint**(port 3342, not port 1433).

## Next steps

With configuration out of the way, you can now specify a SQL managed instance as an indexer data source using the basic instructions for [setting up an Azure SQL indexer](search-how-to-index-sql-database).
