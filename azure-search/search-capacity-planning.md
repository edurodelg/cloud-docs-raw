---
source_url: https://learn.microsoft.com/en-us/azure/search/search-capacity-planning
fetched_at: 2026-01-25T03:12:39.413594
---

# Estimate and manage capacity of a search service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, capacity is based on *replicas* and *partitions* that can be scaled to your workload. Replicas are copies of the search engine. Partitions are units of storage. Each new search service starts with one each, but you can add or remove replicas and partitions independently to accommodate fluctuating workloads. Adding capacity increases the [cost of running a search service](search-sku-manage-costs#billable-events).

The physical characteristics of replicas and partitions, such as processing speed and disk IO, vary by [pricing tier](search-sku-tier). On a standard search service, the replicas and partitions are faster and larger than those of a basic service.

Changing capacity isn't instantaneous. It can take up to an hour to commission or decommission partitions, especially on services with large amounts of data.

When scaling a search service, you can choose from the following tools and approaches:

Note

If your service was created before April or May 2024, a one-time upgrade to higher storage limits might be available at no extra cost. For more information, see [Upgrade your search service](search-how-to-upgrade).

## Concepts: search units, replicas, partitions

Capacity is expressed in *search units* that can be allocated in combinations of *partitions* and *replicas*.

| Concept | Definition |
|---|---|
Search unit |
A single increment of total available capacity. A minimum of one search unit is required to run the service. Depending on your pricing tier, the maximum ranges from one to 36 units. The number of search units equals the number of replicas multiplied by the number of partitions: R × P = SU. Each service starts with one replica and one partition, which consumes one unit: 1 × 1 = 1. Adding a second replica consumes two units: 2 × 1 = 2. A search unit is also the billing unit for a search service. |
Replica |
Instances of the search service, used primarily to load balance query operations. Each replica hosts one copy of an index. If you allocate three replicas, you have three copies of an index available for servicing query requests. |
Partition |
Physical storage and I/O for read/write operations (for example, when rebuilding or refreshing an index). Each partition has a slice of the total index. If you allocate three partitions, your index is divided into thirds. |

Review the [partitions and replicas table](#partition-and-replica-combinations) for possible combinations that stay under the 36 unit limit.

## When to add capacity

Initially, a service is allocated a minimal level of resources consisting of one partition and one replica. The [tier you choose](search-sku-tier) determines partition size and speed, and each tier is optimized around a set of characteristics that fit various scenarios. If you choose a higher-end tier, you might [need fewer partitions](search-performance-tips#service-capacity) than if you go with S1. One of the questions you need to answer through self-directed testing is whether a larger and more expensive partition yields better performance than two cheaper partitions on a service provisioned at a lower tier.

A single service must have sufficient resources to handle all workloads (indexing and queries). Neither workload runs in the background. You can schedule indexing for times when query requests are naturally less frequent, but the service doesn't otherwise prioritize one task over another. Additionally, a certain amount of redundancy smooths out query performance when services or nodes are updated internally.

Guidelines for determining whether to add capacity include:

- Meeting the high availability criteria for service-level agreement.
- The frequency of HTTP 503 (Service unavailable) errors is increasing.
- The frequency of HTTP 429 (Too many requests) errors is increasing, an indication of low storage.
- Large query volumes are expected.
- A
[one-time upgrade](#how-to-upgrade-capacity)to newer infrastructure and larger partitions isn’t sufficient. - The current number of partitions isn’t adequate for indexing workloads.

As a general rule, search applications tend to need more replicas than partitions, particularly when the service operations are biased toward query workloads. Each replica is a copy of your index, allowing the service to load balance requests against multiple copies. Azure AI Search manages all load balancing and replication of an index, and you can alter the number of replicas allocated for your service at any time. You can allocate up to 12 replicas in a Standard search service and 3 replicas in a Basic search service. Replica allocation can be made either from the [Azure portal](search-create-service-portal) or one of the programmatic options.

Extra partitions are helpful for intensive indexing workloads. Extra partitions spread read/write operations across a larger number of compute resources.

Finally, larger indexes take longer to query. As such, you might find that every incremental increase in partitions requires a smaller but proportional increase in replicas. The complexity of your queries and query volume factors into how quickly query execution is turned around.

Note

Adding more replicas or partitions increases the cost of running the service, and can introduce slight variations in how results are ordered. Be sure to check the [pricing calculator](https://azure.microsoft.com/pricing/calculator/) to understand the billing implications of adding more nodes. The [chart below](#chart) can help you cross-reference the number of search units required for a specific configuration. For more information on how extra replicas affect query processing, see [Ordering results](search-pagination-page-layout#ordering-results).

## How to upgrade capacity

Some Azure AI Search capabilities are only available to new services. One such capability is higher storage capacity, which applies to [services created after April 2024](search-limits-quotas-capacity#service-limits). However, if you created your service before April 2024, you can get higher capacity without recreating your service by performing a one-time upgrade. For more information, see [Upgrade your search service](search-how-to-upgrade).

## How to change capacity

To increase or decrease the capacity of your service, you have two options:

### Add or remove partitions and replicas

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Settings**>**Scale**.The following screenshot shows a Standard service provisioned with one replica and partition. The formula at the bottom indicates how many search units are being used (1). If the unit price was $100 (not a real price), the monthly cost of running this service would be $100 on average.

Use the slider to increase or decrease the number of partitions, and then select

**Save**.This example adds a second replica and partition. Notice the search unit count; it's now four because the billing formula is replicas multiplied by partitions (2 x 2). Doubling capacity more than doubles the cost of running the service. If the search unit cost was $100, the new monthly bill would now be $400.

For the current per unit costs of each tier, visit the

[pricing page](https://azure.microsoft.com/pricing/details/search/).Check your notifications to confirm that the operation started.

This operation can take several hours to complete. It occurs in the background, so your search service remains fully operational and available for read and write operations.

You can't cancel the operation or monitor its progress. However, the following message displays while changes are underway:


### Change your pricing tier

Note

The Azure portal and [Services - Update (REST API)](/en-us/rest/api/searchmanagement/services/update) support changes between Basic and Standard (S1, S2, and S3) tiers. You can upgrade or downgrade tiers, provided your current service configuration doesn't exceed the [limits of the target tier](search-limits-quotas-capacity). Your region also can't have [capacity constraints on the target tier](search-region-support).

Your [pricing tier](search-sku-tier) determines the maximum storage of your search service. If you need more or less capacity, you can switch to a different pricing tier that accommodates your storage needs.

In addition to capacity, pricing tiers determine limits on indexes, indexers, and other search objects. Compare the [service limits](search-limits-quotas-capacity) of your current tier and your desired tier before you proceed. Generally, switching to a higher tier increases your [storage limit](search-limits-quotas-capacity#service-limits) and [vector limit](search-limits-quotas-capacity#vector-index-size-limits), increases request throughput, and decreases latency, while switching to a lower tier has the opposite effect.

Switching to a higher pricing tier also increases the cost of running your search service. For more information, see the [pricing page](https://azure.microsoft.com/pricing/details/search/).

To change your pricing tier:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.From the left pane, select

**Settings**>**Scale**.Under your current tier, select

**Change Pricing Tier**.On the

**Select Pricing Tier**page, choose a different tier from the list.You can switch between Basic, S1, S2, and S3, but you can't switch to or from Free, S3HD, L1, or L2. These tiers aren't selectable and appear dimmed.

To start the scale operation, select

**Save**.This operation can take several hours to complete. It occurs in the background, so your search service remains fully operational and available for read and write operations.

You can't cancel the operation or monitor its progress. However, the following message displays while changes are underway:


## How scale requests are handled

Upon receipt of a scale request, the search service:

- Checks whether the request is valid.
- Starts backing up data and system information.
- Checks whether the service is already in a provisioning state (currently adding or eliminating either replicas or partitions).
- Starts provisioning.

Scaling a service can take as little as 15 minutes or well over an hour, depending on the size of the service and the scope of the request. Backup can take several minutes, depending on the amount of data and number of partitions and replicas.

The above steps aren't entirely consecutive. For example, the system starts provisioning when it can safely do so, which could be while backup is winding down.

## Errors during scaling

The following table lists causes and solutions for errors that can occur during scaling operations.

| Error message | Cause | Solution |
|---|---|---|
| "Service update operations aren't allowed at this time because we're processing a previous request." | Another scaling operation is in progress. | Check the Overview page in the Azure portal or use the
1, 2 |
"Failed to scale search service servicename. Error: Object count ActualCount exceeds allowable limit: MaximumCount." |
Your current service configuration exceeds the limits of the target pricing tier. | Check that your storage usage, vector usage, indexes, indexers, and other objects fit within the lower tier's
|

1 There's no status for backups, which are internal operations that are unlikely to disrupt a scaling exercise.

2 If your search service appears to be stalled in a provisioning state, check for orphaned indexes that are unusable, with zero query volumes and no index updates. An unusable index can block changes to service capacity. In particular, look for [CMK-encrypted](search-security-manage-encryption-keys) indexes whose keys are no longer valid. Either delete the index or restore the keys to bring the index back online and unblock your scaling operation.

## Partition and replica combinations

The following chart applies to Standard tier and higher. It shows all possible combinations of partitions and replicas, subject to the 36 search unit maximum per service.

1 partition |
2 partitions |
3 partitions |
4 partitions |
6 partitions |
12 partitions |
|
|---|---|---|---|---|---|---|
1 replica |
1 SU | 2 SU | 3 SU | 4 SU | 6 SU | 12 SU |
2 replicas |
2 SU | 4 SU | 6 SU | 8 SU | 12 SU | 24 SU |
3 replicas |
3 SU | 6 SU | 9 SU | 12 SU | 18 SU | 36 SU |
4 replicas |
4 SU | 8 SU | 12 SU | 16 SU | 24 SU | N/A |
5 replicas |
5 SU | 10 SU | 15 SU | 20 SU | 30 SU | N/A |
6 replicas |
6 SU | 12 SU | 18 SU | 24 SU | 36 SU | N/A |
12 replicas |
12 SU | 24 SU | 36 SU | N/A | N/A | N/A |

Basic search services have lower search unit counts.

On search services created before April 3, 2024, Basic services can have exactly one partition and up to three replicas for a maximum limit of three SUs. The only adjustable resource is replicas. However, you might be able to increase your partition count by

[upgrading your service](search-how-to-upgrade).On search services created after April 3, 2024 in

[supported regions](search-limits-quotas-capacity#service-limits), Basic services can have up to three partitions and three replicas. The maximum SU limit is nine to support a full complement of partitions and replicas.

For search services on any billable tier, regardless of creation date, you need a minimum of two replicas for high availability on queries.

For billing rates per tier and currency, see the [Azure AI Search pricing page](https://azure.microsoft.com/pricing/details/search/).

## Estimate capacity using a billable tier

The size of the indexes you expect to build determines storage needs. There are no solid heuristics or generalities that help with estimates. The only way to determine the size of an index is [build one](search-what-is-an-index). Its size is based on tokenization and embeddings, and whether you enable suggesters, filtering, and sorting, or can take advantage of [vector compression](vector-search-how-to-quantization).

We recommend estimating on a billable tier, Basic or higher. The Free tier runs on physical resources shared by multiple customers and is subject to factors beyond your control. Only the dedicated resources of a billable search service can accommodate larger sampling and processing times for more realistic estimates of index quantity, size, and query volumes during development.

[Review service limits at each tier](search-limits-quotas-capacity#service-limits)to determine whether lower tiers can support the number of indexes you need. Consider whether you need multiple copies of an index for active development, testing, and production.A search service is subject to object limits (maximum number of indexes, indexers, skillsets, etc.) and storage limits. Whichever limit is reached first is the effective limit.

[Create a service at a billable tier](search-create-service-portal). Tiers are optimized for certain workloads. For example, the Storage Optimized tier has a limit of 10 indexes because it's designed to support a low number of large indexes.Start low, at Basic or S1, if you're not sure about the projected load.

Start high, at S2 or even S3, if testing includes large-scale indexing and query loads.

Start with Storage Optimized, at L1 or L2, if you're indexing a large amount of data and query load is relatively low, as with an internal business application.


[Build an initial index](search-what-is-an-index)to determine how source data translates to an index. This is the only way to estimate index size. Attributes on the field definitions affect physical storage requirements:For keyword search, marking fields as filterable and sortable

[increases index size](search-what-is-an-index#physical-structure-and-size).For vector search, you can

[set parameters to reduce vector size](vector-search-how-to-configure-compression-storage).

[Monitor storage, service limits, query volume, and latency](monitor-azure-cognitive-search)in the Azure portal. the Azure portal shows you queries per second, throttled queries, and search latency. All of these values can help you decide if you selected the right tier.Add replicas for high availability or to mitigate slow query performance.

There are no guidelines on how many replicas are needed to accommodate query loads. Query performance depends on the complexity of the query and competing workloads. Although adding replicas clearly results in better performance, the result isn't strictly linear: adding three replicas doesn't guarantee triple throughput. For guidance in estimating QPS for your solution, see

[Analyze performance](search-performance-analysis)and[Monitor queries](search-monitor-queries).

For an [inverted index](https://en.wikipedia.org/wiki/Inverted_index), size and complexity are determined by content, not necessarily by the amount of data that you feed into it. A large data source with high redundancy could result in a smaller index than a smaller dataset that contains highly variable content. So it's rarely possible to infer index size based on the size of the original dataset.

Storage requirements can be inflated if you include data that will never be searched. Ideally, documents contain only the data that you need for the search experience.

## Service-level agreement considerations

The Free tier and preview features aren't covered by [service-level agreements (SLAs)](https://azure.microsoft.com/support/legal/sla/search/v1_0/). For all billable tiers, SLAs take effect when you provision sufficient redundancy for your service.

Two or more replicas satisfy query (read) SLAs.

Three or more replicas satisfy query and indexing (read-write) SLAs.


The number of partitions doesn't affect SLAs.