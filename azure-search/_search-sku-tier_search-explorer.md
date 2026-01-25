---
merged_at: 2026-01-25T02:11:58.440671
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-sku-tier.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-sku-tier -->

# Choose a service tier for Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Part of [creating a search service](search-create-service-portal) is choosing a pricing tier (or SKU). In the Azure portal, tier is specified in the **Select Pricing Tier** page when you create the service. In PowerShell or Azure CLI, the tier is specified through the `-Sku`

parameter.

The tier determines the:

- Maximum number of indexes and other objects allowed on the service.
- Size and speed of partitions (physical storage).
- Billable rate as a fixed monthly cost, but also an incremental cost if you add capacity.
- Workload characteristics. Some tiers are optimized for specific workloads.

In a few instances, the tier you choose determines the availability of [premium features](#feature-availability-by-tier).

Billing rates are shown in the Azure portal's **Select Pricing Tier** page. You can check the [pricing page](https://azure.microsoft.com/pricing/details/search/) for regional rates and review [Plan and manage costs](search-sku-manage-costs) to learn more about the billing model.

Note

Search services created after April 3, 2024 have larger partitions and higher vector quotas at almost every tier. For more information, see [Service limits](search-limits-quotas-capacity#service-limits).

## Tier descriptions

Tiers include **Free**, **Basic**, **Standard**, and **Storage Optimized**. Standard and Storage Optimized are available with several configurations and capacities. The following screenshot from Azure portal shows the available tiers, minus pricing (which you can find in the Azure portal and on the [pricing page](https://azure.microsoft.com/pricing/details/search/)).

**Free** creates a [limited search service](search-limits-quotas-capacity#subscription-limits) for smaller projects, like running tutorials and code samples. Internally, system resources are shared among multiple subscribers. You can't scale a free service, run significant workloads, and some premium features aren't available. You can only have one free search service per Azure subscription. If the service is inactive for an extended period of time, it might be deleted to free up capacity, especially if the region is under capacity constraints.

The most commonly used billable tiers include:

**Basic**has the ability to meet SLA with its support for three replicas.**Standard (S1, S2, S3)**is the default. It gives you more flexibility in scaling for workloads. You can scale both partitions and replicas. With dedicated resources under your control, you can deploy larger projects, optimize performance, and increase capacity.

Some tiers are designed for certain types of work:

**Standard 3 High Density (S3 HD)**is a*hosting mode*for S3, where the underlying hardware is optimized for a large number of smaller indexes and is intended for multitenancy scenarios. S3 HD has the same per-unit charge as S3, but the hardware is optimized for fast file reads on a large number of smaller indexes.**Storage Optimized (L1, L2)**tiers offer larger storage capacity at a lower price per TB than the Standard tiers. These tiers are designed for large indexes that don't change very often. The primary tradeoff is higher query latency, which you should validate for your specific application requirements.

You can find out more about the various tiers on the [pricing page](https://azure.microsoft.com/pricing/details/search/), in the [Service limits in Azure AI Search](search-limits-quotas-capacity) article, and on the Azure portal page when you're provisioning a service.

## Region availability by tier

The [regions list](search-region-support) provides the locations where Azure AI Search is offered. Some regions might have capacity constraints for certain tiers, which prevents the creation of new search services on those tiers. The list uses footnotes to indicate constrained regions and tiers.

When you create a search service in the Azure portal, unavailable region–tier combinations are automatically excluded.

## Feature availability by tier

Most features are available on all tiers, including the Free tier. In a few cases, the tier determines the availability of a feature. The following table describes the constraints.

| Feature | Tier considerations |
|---|---|
|

[more limitations](search-limits-quotas-capacity#indexer-limits)on the free tier.[indexer](search-how-to-create-indexers?tabs=indexer-rest#create-an-indexer)`executionEnvironment`

configuration parameter[AI enrichment](cognitive-search-concept-intro)[Managed or trusted identities for outbound (indexer) access](search-how-to-managed-identities)[Customer-managed encryption keys](search-security-manage-encryption-keys)[IP firewall access](service-configure-firewall)[Private endpoint (integration with Azure Private Link)](service-create-private-endpoint)For outbound connections by indexers to other Azure resources, not available on Free or S3 HD.

For indexers that use skillsets, not available on Free, Basic, S1, or S3 HD.

[Availability zones](/en-us/azure/reliability/reliability-ai-search#availability-zone-support)[Semantic ranker](semantic-search-overview)Resource-intensive features might not work well unless you give it sufficient capacity. For example, [AI enrichment](cognitive-search-concept-intro) has long-running skills that time out on a Free service unless the dataset is small.

## Upper limits

Tiers determine the maximum storage of the service itself, plus the maximum number of indexes, indexers, data sources, skillsets, and synonym maps that you can create. For a full break out of all limits, see [Service limits in Azure AI Search](search-limits-quotas-capacity).

## Partition size and speed

Tier pricing includes details about per-partition storage that ranges from 15 GB for Basic, up to 2 TB for Storage Optimized (L2) tiers. Other hardware characteristics, such as speed of operations, latency, and transfer rates, aren't published, but tiers that are designed for specific solution architectures are built on hardware that has the features to support those scenarios. For more information about partitions, see [Estimate and manage capacity](search-capacity-planning) and [Reliability in Azure AI Search](/en-us/azure/reliability/reliability-ai-search).

Note

Higher-capacity partitions became available in select regions in April 2024. A second wave of higher-capacity partitions was released in May 2024. If you have an older search service, you might be able to [upgrade your service](search-how-to-upgrade) to benefit from more capacity at the same billing rate.

## Billing rates

Tiers have different billing rates, with higher rates for tiers that run on more expensive hardware or provide more expensive features. The tier billing rate can be found in the [Azure pricing pages](https://azure.microsoft.com/pricing/details/search/) for Azure AI Search.

Once you create a service, the billing rate becomes both a *fixed cost* of running the service around the clock, and an *incremental cost* if you choose to add more capacity.

Search services are allocated computing resources in the form of *partitions* (for storage), and *replicas* (instances of the query engine). Initially, a service is created with one of each, and the billing rate is inclusive of both resources. However, if you scale capacity, the costs go up or down in increments of the billable rate.

The following example provides an illustration. Assume a hypothetical billing rate of $100 per month. If you keep the search service at its initial capacity of one partition and one replica, then $100 is what you can expect to pay at the end of the month. However, if you add two more replicas to achieve high availability, the monthly bill increases to $300 ($100 for the first replica-partition pair, followed by $200 for the two replicas).

This billing model is based on the concept of applying the billing rate to the number *search units* (SU) used by a search service. All services are initially provisioned at one SU, but you can increase the SUs by adding either partitions or replicas to handle larger workloads. For more information, see [How to estimate costs of a search service](search-sku-manage-costs).

## Tier changes

Note

Existing search services can switch between Basic and Standard (S1, S2, and S3) tiers. Your current service configuration can't exceed the limits of the target tier, and your region can't have capacity constraints on the target tier. For more information, see [Change your pricing tier](search-capacity-planning#change-your-pricing-tier).

To switch to a different tier than those previously listed:

[Create a search service](search-create-service-portal)on the new tier.- Deploy your search content onto the new service.
[Follow this checklist](search-howto-move-across-regions#prepare-and-move)to ensure you have all the content. - Delete the old service when you're sure it's no longer needed.

For large indexes that you don't want to rebuild from scratch, use one of the following backup and restore samples:

[Backup and restore sample (C#)](https://github.com/Azure-Samples/azure-search-dotnet-utilities/blob/main/index-backup-restore/README.md)[Backup and restore sample (Python)](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/utilities/index-backup-restore/azure-search-backup-and-restore.ipynb)[Backup and restore sample for very large indexes (Python)](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/utilities/resumable-index-backup-restore/backup-and-restore.ipynb)

## Next steps

The best way to choose a pricing tier is to start with a least-cost tier, and then allow experience and testing to inform your decision to keep the service or switch to a higher tier.

For next steps, we recommend that you create a search service at a tier that can accommodate the level of testing you propose to do, and then review the following guidance on estimating cost and capacity:


---

<!-- DOCUMENTO FUSIONADO: search-explorer.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-explorer -->

# Quickstart: Use Search explorer to run queries in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you learn how to use **Search explorer**, a built-in query tool in the Azure portal for running queries against an Azure AI Search index. Use this tool to test a query or filter expression or to confirm whether content exists in the index.

This quickstart uses an existing index to demonstrate Search explorer.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An Azure AI Search service.

[Create a service](search-create-service-portal)or[find an existing service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices)in your current subscription. For this quickstart, you can use a free service.This quickstart uses the hotels-sample index. Follow the instructions in

[this quickstart](search-import-data-portal)to create the index.

## Start Search explorer

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Overview**.On the command bar, select

**Search explorer**.Alternatively, select the

**Search explorer**tab on the index page.

## Query three ways

There are three approaches to querying in Search explorer:

Query view provides a default search bar. It accepts an empty query or free-text query with Booleans, such as

`ocean view + parking`

.Image view provides a window to browse or drag and drop PNG, JPG, or JPEG files. Unless your index has an

[image vectorizer and an equivalent skill](vector-search-how-to-configure-vectorizer#supported-embedding-models), this view is unavailable.JSON view supports parameterized queries. Filters, orderby, select, count, searchFields, and all other parameters must be set in JSON view.


## Example: Image query

Search explorer accepts images as query inputs through **Image view**, which requires that you use a supported vectorizer–skill pair. For more information, see [Configure a vectorizer in a search index](vector-search-how-to-configure-vectorizer).

The hotels-sample index isn't configured for image vectorization. If you want to run image queries, create an index as described in [Quickstart: Vector search in the Azure portal](search-get-started-portal-import-vectors). The quickstart relies on text-based sample data, so you must use documents that contain images.

To run an image query, select or drag an image to the search area, and then select **Search**. Search explorer vectorizes the image and sends the vector to the search engine for query execution. The search engine returns documents that are sufficiently similar to the input image, up to the specified `k`

number of results.

## Examples: JSON queries

The following are examples of JSON queries you can run using Search explorer. To follow these examples, switch to **JSON view**. You can paste each JSON example into the text area.

Tip

The JSON view supports intellisense for parameter name completion. Place your cursor inside the JSON view and enter a space character to see a list of all query parameters. You can also enter a letter, like `s`

, to see only the query parameters that begin with that letter.

Intellisense doesn't exclude invalid parameters, so use your best judgment.

### Run an unspecified query

In Search explorer, POST requests are formulated internally using [Documents - Search Post (REST API)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2024-05-01-preview&preserve-view=true), with responses returned as verbose JSON documents.

For a first look at content, execute an empty search by selecting **Search** with no terms provided. An empty search is useful as a first query because it returns entire documents so that you can review document composition. On an empty search, there's no search score, and documents are returned in arbitrary order (`"@search.score": 1`

for all documents). By default, 50 documents are returned per search request.

Add `"count": true`

to get the number of matches found in an index. On an empty search, the count is the total number of documents in the index. On a qualified search, it's the number of documents matching the query input. Recall that the service returns the top-50 matches by default, so the count might indicate more matches in the index than what's returned in the results.

Equivalent syntax for an empty search is `*`

or `"search": "*"`

.

```
{
"search": "*",
"count": true
}
```


**Results**

### Run a free-text query

Free-form search, with or without operators, is useful for simulating user-defined queries sent from a custom app to Azure AI Search. Only fields attributed as searchable in the index are scanned for matches.

You don't need the JSON view for a free-text query, but we provide it in JSON for consistency with other examples in this article.

Notice that when you provide search criteria, such as query terms or expressions, search rank comes into play. The following example illustrates a free text search. The `@search.score`

is a relevance score computed for the match using the [default scoring algorithm](index-ranking-similarity#default-scoring-algorithm).

```
{
"search": "activities `outdoor pool` restaurant OR continental breakfast"
}
```


**Results**

You can use Ctrl-F to search within results for specific terms of interest.

### Limit fields in search results

Add [ "select"](search-query-odata-select) to limit results to the explicitly named fields for more readable output in

**Search explorer**. Only fields attributed as retrievable in the index can show up in results.

```
{
"search": "activities `outdoor pool` restaurant OR continental breakfast",
"count": true,
"select": "HotelId, HotelName, Tags, Description"
}
```


**Results**

### Return next batch of results

Azure AI Search returns the top-50 matches based on the search rank. The hotels-sample index only has 50 hotels, so we use a smaller number to illustrate paging. To get the next set of matching documents, append `"top": 20`

and `"skip": 10`

to increase the result set to 20 documents (default is 50, maximum is 1000), skipping the first 10 documents. You can check the document key (`HotelId`

) to identify a document.

Recall that you need to provide search criteria, such as a query term or expression, to get ranked results. Search scores decrease the deeper you reach into search results.

```
{
"search": "activities `outdoor pool` restaurant OR continental breakfast",
"count": true,
"select": "HotelId, HotelName, Tags, Description",
"top": 20,
"skip": 10
}
```


**Results**

### Filter expressions (greater than, less than, equal to)

Use the [ filter](search-query-odata-filter) parameter to specify inclusion or exclusion criteria. The field must be attributed as filterable in the index. This example searches for ratings greater than four:

```
{
"search": "activities `outdoor pool` restaurant OR continental breakfast",
"count": true,
"select": "HotelId, HotelName, Tags, Description, Rating",
"filter": "Rating gt 4"
}
```


**Results**

### Sort results

Add [ orderby](search-query-odata-orderby) to sort results by another field besides search score. The field must be attributed as sortable in the index. In situations where the filtered value is identical (for example, same price), the order is arbitrary, but you can add more criteria for deeper sorting. Here's an example expression you can use to test this out:

```
{
"search": "activities `outdoor pool` restaurant OR continental breakfast",
"count": true,
"select": "HotelId, HotelName, Tags, Description, Rating, LastRenovationDate",
"filter": "Rating gt 4",
"orderby": "LastRenovationDate desc"
}
```


**Results**

## Takeaways

In this quickstart, you used **Search explorer** to query an index using the REST API.

Results are returned as verbose JSON documents so that you can view the construction and content of each document in its entirety. The

`select`

parameter in a query expression limits which fields are returned.Search results are composed of all fields attributed as retrievable in the index. Select the

**Fields**tab to review attributes.Keyword search, similar to what you might enter in a commercial web browser, is useful for testing an end-user experience. For example, assuming the hotels-sample index, you can enter

`"activities 'outdoor pool' restaurant OR continental breakfast"`

, and then you can use Ctrl-F to find terms within the search results.Query and filter expressions are articulated in a syntax implemented by Azure AI Search. The default is a

[simple syntax](/en-us/rest/api/searchservice/simple-query-syntax-in-azure-search), but you can optionally use[full Lucene](/en-us/rest/api/searchservice/lucene-query-syntax-in-azure-search)for more powerful queries.[Filter expressions](/en-us/rest/api/searchservice/odata-expression-syntax-for-azure-search)are articulated in an OData syntax.

## Clean up resources

When you work in your own subscription, it's a good idea at the end of a project to identify whether you still need the resources you created. Resources left running can cost you money. You can delete resources individually or delete the resource group to delete the entire set of resources.

In the Azure portal, you can find and manage resources by selecting **All resources** or **Resource groups** from the left pane.

Remember that a free search service is limited to three indexes, three indexers, and three data sources. To stay under the limit, you can delete these items individually in the Azure portal.

## Next step

To learn more about query structures and syntax, use a REST client to create query expressions that use more parts of the REST API. [Documents - Search Post (REST API)](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2024-05-01-preview&preserve-view=true) is especially helpful for learning and exploration.
