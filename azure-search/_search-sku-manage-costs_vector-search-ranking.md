---
merged_at: 2026-01-25T03:18:14.042624
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-sku-manage-costs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-sku-manage-costs -->

# Plan and manage costs of an Azure AI Search service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how Azure AI Search is billed, including fixed and variable costs, and provides guidance for cost management.

Before you create a search service, use the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/) to estimate costs based on your planned [capacity](search-capacity-planning) and features. Another resource is a capacity-planning worksheet that models your expected index size, indexing throughput, and indexing costs.

As your search workload evolves, follow our tips to minimize costs during both deployment and operation. You can also use built-in metrics to monitor query requests and [Cost Management](/en-us/azure/cost-management-billing/costs/overview-cost-management) to create budgets, alerts, and data exports.

Note

Higher-capacity partitions are available at the same billing rate on services created after April and May 2024. For more information about partition-size upgrades, see [Service limits](search-limits-quotas-capacity#service-limits).

## Understand the billing model

Azure AI Search has both fixed and pay-as-you-go billing. You pay a fixed rate for your search service as long as it exists, while premium features are billed according to your usage.

Costs for Azure AI Search are only a portion of the monthly costs in your Azure bill. Although this article focuses on planning and managing Azure AI Search costs, you're billed for all Azure services and resources used in your Azure subscription, including non-Microsoft services.

### How you're charged for the base service

When you create or use search resources, you're charged for the minimum required replica and partition combination (R × P) at the prorated hourly rate of your [pricing tier](search-sku-tier). As your search units increase or decrease, so do your costs. For more information and an example of the billing model, see [Billing rates](search-sku-tier#billing-rates).

### How you're charged for premium features

Premium features are charged in addition to the base cost of your search service. The following table lists premium features and their billing units. All of these features are optional, so if you don't use them, you don't incur any charges.

| Feature | Billing unit |
|---|---|
Image extraction (AI enrichment) 1 |
Per 1,000 images. See the
|

[Custom Entity Lookup skill](cognitive-search-skill-custom-entity-lookup)(AI enrichment)[pricing page](https://azure.microsoft.com/pricing/details/search/#pricing)[Built-in or custom skills](cognitive-search-predefined-skills)(AI enrichment)2[Vectorizers](vector-search-how-to-configure-vectorizer)2[Semantic ranker](semantic-search-overview)`queryType=semantic`

. Billed at a progressive rate. See the [pricing page](https://azure.microsoft.com/pricing/details/search/#pricing).[Agentic retrieval](agentic-retrieval-overview)[pricing page](https://azure.microsoft.com/pricing/details/search/#pricing).[Shared private link](search-indexer-howto-access-private)[Billed for bandwidth](https://azure.microsoft.com/pricing/details/private-link/)as long as the shared private link exists and is used.1 Refers to images extracted from a file within the indexer pipeline. Text extraction is free. Image extraction is billed when you [enable the indexAction parameter](cognitive-search-concept-image-scenarios#configure-indexers-for-image-processing) or when you call the

[Document Extraction skill](cognitive-search-skill-document-extraction).

2 Charges for Azure OpenAI models and Foundry models appear on your bill for those services.

### How you're otherwise charged

Depending on your configuration and usage, the following charges might apply:

Data traffic might incur networking costs. See the

[bandwidth pricing](https://azure.microsoft.com/pricing/details/bandwidth/).Several premium features, such as

[knowledge stores](knowledge-store-concept-intro),[debug sessions](cognitive-search-debug-session), and[enrichment caches](enrichment-cache-how-to-configure), depend on Azure Storage and incur storage costs. Charges for these features appear on your Azure Storage bill.[Customer-managed keys](search-security-manage-encryption-keys), which provide double encryption of sensitive content, require a billable[Azure Key Vault](https://azure.microsoft.com/pricing/details/key-vault/).A skillset can include

[billable built-in skills](cognitive-search-predefined-skills), nonbillable built-in utility skills, and custom skills. Nonbillable utility skills include[Conditional](cognitive-search-skill-conditional),[Shaper](cognitive-search-skill-shaper),[Text Merge](cognitive-search-skill-textmerger), and[Text Split](cognitive-search-skill-textsplit). They don't have an API key requirement or 20-document limit.A custom skill is functionality you provide. Custom skills are billable only if they call other billable services. They don't have an API key requirement or 20-document limit.


Note

You aren't billed for the number of full-text or vector queries, query responses, or documents ingested. However, [service limits](search-limits-quotas-capacity) apply to each pricing tier.

## Estimate and plan costs

Use the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/) to estimate your baseline costs for Azure AI Search. You can also find estimated costs and tier comparisons on the [Select Pricing Tier](search-create-service-portal#choose-a-tier) page during service creation.

For initial testing, we recommend that you create a capacity-planning worksheet. The worksheet helps you understand the index-to-source ratio and the effect of enrichment or vector features on both capacity and cost.

To create a capacity-planning worksheet:

Index a small sample (1–5%) of your data. Include any

[OCR](cognitive-search-skill-ocr), enrichment, or embedding skills you plan to use.Measure the index size, indexing throughput, and indexing costs.

Extrapolate the results to estimate the full-scale requirements for your data.


## Minimize costs

To minimize the costs of your Azure AI Search solution, use the following strategies:

### Deployment and configuration

Create a search service in a

[region with more storage per partition](search-limits-quotas-capacity#service-limits).Create all related Azure resources in the same region (or as few regions as possible) to minimize or eliminate bandwidth charges.

Choose the lightest

[pricing tier](search-sku-tier)that meets your needs. Basic and S1 offer full access to the modern API at the lowest hourly rate per SU.Use

[Azure Web Apps](/en-us/azure/app-service/overview)for your front-end application to keep requests and responses within the data center boundary.

### Scaling

[Add partitions](search-capacity-planning#add-or-remove-partitions-and-replicas)only when the index size or ingestion throughput requires it.[Add replicas](search-capacity-planning#add-or-remove-partitions-and-replicas)only when your queries per second increase, when complex queries are throttling your service, or when high availability is required.Scale up for resource-intensive operations, such as indexing, and then readjust downwards for regular query workloads.

Write code to automate scaling for predictable workload patterns.

Remember that capacity and pricing aren't linear. Doubling capacity more than doubles costs on the same tier. For better performance at a similar price, consider

[switching to a higher tier](search-performance-tips#tip-switch-to-a-standard-s2-tier).

### Indexing and enrichment

Use

[incremental indexing](search-howto-reindex)to process only new or changed data.Use

[enrichment caching](enrichment-cache-how-to-configure)and a[knowledge store](knowledge-store-concept-intro)to reuse previously enriched content. Although caching incurs a storage charge, it lowers the cumulative cost of[AI enrichment](cognitive-search-concept-intro).Keep vector payloads compact. For vector search, see the

[vector compression best practices](https://techcommunity.microsoft.com/blog/azure-ai-services-blog/azure-ai-search-cut-vector-costs-up-to-92-5-with-new-compression-techniques/4404866).

## Monitor costs

At the service level, you can [monitor built-in metrics](search-monitor-queries) for your queries per second (QPS), search latency, throttled queries, and index size. You can then [create an Azure Monitor dashboard](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards) that overlays QPS, latency, and cost data to determine when to add or remove replicas.

At the subscription or resource group level, [Cost Management](/en-us/azure/cost-management-billing/costs/overview-cost-management) provides tools to track, analyze, and control costs. You can use Cost Management to:

[Create budgets](/en-us/azure/cost-management-billing/costs/tutorial-acm-create-budgets?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn)that define and track progress against spending limits. For more granular monitoring, customize your budgets using[filters](/en-us/azure/cost-management-billing/costs/group-filter?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn)for specific Azure resources or services. Filters prevent you from accidentally creating resources that incur extra costs.[Create alerts](/en-us/azure/cost-management-billing/costs/cost-mgt-alerts-monitor-usage-spending?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn)that automatically notify stakeholders of spending anomalies or overspending risks. Alerts are based on spending compared to budget and cost thresholds. Both budgets and alerts are created for subscriptions and resource groups, making them useful for monitoring overall costs.[Export cost data](/en-us/azure/cost-management-billing/costs/tutorial-export-acm-data?WT.mc_id=costmanagementcontent_docsacmhorizontal_-inproduct-learn)to a storage account. This is helpful when you or others need to perform more cost analysis. For example, a finance team can analyze the data using Excel or Power BI. You can export your costs on a daily, weekly, or monthly schedule and set a custom date range. Exporting cost data is the recommended method for retrieving cost datasets.

## FAQ

**Can I temporarily shut down a search service to save on costs?**

Search runs as a continuous service. Dedicated resources are always operational and allocated for your exclusive use for the lifetime of your service. To stop billing entirely, you must delete the service. Deleting a service is permanent and also deletes its associated data.

**Can I change the billing rate (tier) of an existing search service?**

Existing services can switch between Basic and Standard (S1, S2, and S3) tiers. Your current service configuration can't exceed the limits of the target tier, and your region can't have capacity constraints on the target tier. For more information, see [Change your pricing tier](search-capacity-planning#change-your-pricing-tier).


---

<!-- DOCUMENTO FUSIONADO: vector-search-ranking.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-ranking -->

# Relevance in vector search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

During vector query execution, the search engine looks for similar vectors to find the best candidates to return in search results. Depending on how you indexed the vector content, the search for relevant matches is either exhaustive or constrained to nearest neighbors for faster processing. When candidates are found, similarity metrics are used to score each result based on the strength of the match.

This article explains the algorithms used to find relevant matches and the similarity metrics used for scoring. It also offers tips for improving relevance if search results don't meet expectations.

## Algorithms used in vector search

Vector search algorithms include:

[Exhaustive K-Nearest Neighbors (KNN)](#about-exhaustive-knn), which performs a brute-force scan of the entire vector space.[Hierarchical Navigable Small World (HNSW)](#about-hnsw), which performs an[Approximate Nearest Neighbor (ANN)](#about-ann)search.

Only vector fields marked as `searchable`

in the index or `searchFields`

in the query are used for searching and scoring.

### About exhaustive KNN

Exhaustive KNN calculates the distances between all pairs of data points and finds the exact `k`

nearest neighbors for a query point. Because the algorithm doesn't require fast random access of data points, KNN doesn't consume [vector index size](vector-search-index-size) quota. However, it provides the global set of nearest neighbors.

Exhaustive KNN is computationally intensive, so use it for small to medium datasets or when the need for precision outweighs the need for query performance. Another use case is building a dataset to evaluate the recall of an [ANN algorithm](#about-ann), as exhaustive KNN can be used to build the ground truth set of nearest neighbors.

### About HNSW

HNSW is an ANN algorithm optimized for high-recall, low-latency applications with unknown or volatile data distribution. During indexing, HNSW creates extra data structures that organize data points into a hierarchical graph. During query execution, HNSW navigates through this graph to find the most relevant matches, enabling efficient nearest neighbor searches.

HNSW requires all data points to reside in memory for fast random access, which consumes [vector index size](vector-search-index-size) quota. This design balances search accuracy with computational efficiency and makes HNSW suitable for most scenarios, especially when searching over larger datasets.

HNSW offers several tunable configuration parameters to optimize throughput, latency, and recall for your search application. For example, fields that specify HNSW also support exhaustive KNN using the [query request](vector-search-how-to-query) parameter `"exhaustive": true`

. However, fields indexed for `exhaustiveKnn`

don't support HNSW queries because the extra data structures that enable efficient search don't exist.

### About ANN

ANN is a class of algorithms for finding matches in vector space. This class of algorithms uses different data structures or data partitioning methods to significantly reduce the search space and accelerate query processing.

ANN algorithms sacrifice some accuracy but offer scalable and faster retrieval of approximate nearest neighbors, which makes them ideal for balancing accuracy and efficiency in modern information retrieval applications. You can adjust the parameters of your algorithm to fine-tune the recall, latency, memory, and disk footprint requirements of your search application.

Azure AI Search uses HNSW for its ANN algorithm.

## How nearest neighbor search works

Vector queries execute against an embedding space consisting of vectors generated from the same embedding model. Generally, the input value within a query request is fed into the same machine learning model that generated embeddings in the vector index. The output is a vector in the same embedding space. Since similar vectors are clustered close together, finding matches is equivalent to finding the vectors that are closest to the query vector, and returning the associated documents as the search result.

For example, if a query request is about hotels, the model maps the query into a vector that exists somewhere in the cluster of vectors representing documents about hotels. Identifying which vectors are the most similar to the query, based on a similarity metric, determines which documents are the most relevant.

When vector fields are indexed for exhaustive KNN, the query executes against "all neighbors". For fields indexed for HNSW, the search engine uses an HNSW graph to search over a subset of nodes within the vector index.

### Creating the HNSW graph

During indexing, the search service constructs the HNSW graph. The goal of indexing a new vector into an HNSW graph is to add it to the graph structure in a way that supports efficient nearest neighbor search. The following steps summarize the process:

Initialization: Start with an empty HNSW graph or, if it's not a new index, the existing HNSW graph.

Entry point: This is the top-level of the hierarchical graph and serves as the starting point for indexing.

Adding to the graph: Different hierarchical levels represent different granularities of the graph, with higher levels being more global, and lower levels being more granular. Each node in the graph represents a vector point.

Each node is connected to up to

`m`

neighbors that are nearby. This is the`m`

parameter.The

`efConstruction`

parameter governs the number of data points considered as candidate connections. This dynamic list forms the set of closest points in the existing graph for the algorithm to consider. Higher`efConstruction`

values result in more nodes being considered, which often leads to denser local neighborhoods for each vector.These connections use the configured similarity

`metric`

to determine distance. Some connections are "long-distance" connections that connect across different hierarchical levels, creating shortcuts in the graph that enhance search efficiency.

Graph pruning and optimization: This can happen after indexing all vectors, and it improves navigability and efficiency of the HNSW graph.


### Navigating the HNSW graph at query time

A vector query navigates the hierarchical graph structure to scan for matches. The following steps summarize the process:

Initialization: The algorithm initiates the search at the top-level of the hierarchical graph. This entry point contains the set of vectors that serve as starting points for search.

Traversal: Next, it traverses the graph level by level, navigating from the top-level to lower levels. It selects candidate nodes that are closer to the query vector based on the configured distance metric, such as cosine similarity.

Pruning: To improve efficiency, the algorithm prunes the search space by only considering nodes that are likely to contain nearest neighbors. It maintains a priority queue of potential candidates and updates it as the search progresses. The length of this queue is configured by the parameter

`efSearch`

.Refinement: As the algorithm moves to lower, more granular levels, HNSW considers more neighbors near the query. This consideration allows the candidate set of vectors to be refined, improving accuracy.

Completion: The search completes when the desired number of nearest neighbors are identified, or when other stopping criteria are met. The query-time parameter

`k`

governs this desired number of nearest neighbors.

## Similarity metrics used to measure nearness

The algorithm finds candidate vectors to evaluate similarity. To perform this task, a similarity metric calculation compares the candidate vector to the query vector and measures the similarity. The algorithm keeps track of the ordered set of most similar vectors that it found, which forms the ranked result set when the algorithm reaches completion.

| Metric | Description |
|---|---|
`cosine` |
This metric measures the angle between two vectors and isn't affected by differing vector lengths. Mathematically, it calculates the angle between two vectors. Cosine is the similarity metric used by
`cosine` in the vector configuration. |

`dotProduct`

`cosine`

similarity, but it's slightly more performant.`euclidean`

`l2 norm`

) This metric measures the length of the vector difference between two vectors. Mathematically, it calculates the Euclidean distance between two vectors, which is the l2-norm of the difference of the two vectors.Note

If you run two or more vector queries in parallel, or if you do a hybrid search that combines vector and text queries in the same request, [Reciprocal Rank Fusion (RRF)](hybrid-search-ranking) is used for scoring the final search results.

## Scores in a vector search results

The system calculates and assigns scores to each match. The highest matches return as `k`

results. The `@search.score`

property contains the score. The following table shows the range within which a score falls.

| Search method | Parameter | Scoring metric | Range |
|---|---|---|---|
| vector search | `@search.score` |
Cosine | 0.333 - 1.00 |

For the `cosine`

metric, the calculated `@search.score`

isn't the cosine value between the query vector and the document vectors. Instead, Azure AI Search applies transformations so that the score function is monotonically decreasing. Score values always decrease as the similarity gets worse. This transformation ensures that search scores are usable for ranking purposes.

There are some nuances with similarity scores:

- Cosine similarity is defined as the cosine of the angle between two vectors.
- Cosine distance is defined as
`1 - cosine_similarity`

.

To create a monotonically decreasing function, the `@search.score`

is defined as `1 / (1 + cosine_distance)`

.

If you need a cosine value instead of the synthetic value, use a formula to convert the search score back to cosine distance:

```
double ScoreToSimilarity(double score)
{
double cosineDistance = (1 - score) / score;
return -cosineDistance + 1;
}
```


Having the original cosine value can be useful in custom solutions that set up thresholds to trim results of low quality results.

## Tips for relevance tuning

If you aren't getting relevant results, try changing the [query configuration](vector-search-how-to-query). Vector queries don't have specific tuning features, such as a scoring profile or field or term boosting:

Try different

[chunk size and overlap](vector-search-how-to-chunk-documents)settings. Increase the chunk size and make sure there's enough overlap to keep context or continuity between chunks.For HNSW, try different levels of

`efConstruction`

to change the internal composition of the proximity graph. The default value is 400. The range is 100 to 1,000.Increase

`k`

results to send more search results to a chat model if you're using one.Try

[hybrid queries](hybrid-search-how-to-query)with semantic ranking. In benchmark testing, this combination consistently produced the most relevant results.
