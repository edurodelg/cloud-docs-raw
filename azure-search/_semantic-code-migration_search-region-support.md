---
merged_at: 2026-01-25T02:11:58.410923
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: semantic-code-migration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/semantic-code-migration -->

# Migrate semantic ranking code from previous versions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If your semantic ranking code was written against early preview APIs, this article identifies the code changes necessary for migrating to newer API versions. Breaking changes for semantic ranker are limited to query logic in recent APIs, but if your code was written against the initial preview version, you might need to change your semantic configuration as well.

## Breaking changes

There are two breaking changes for semantic ranker across REST API versions:

`searchFields`

was replaced by`semanticConfiguration`

in 2021-04-30-preview`queryLanguage`

was ignored starting in 2023-07-01-preview, but reinstated for query rewrite in 2024-11-01-preview

Other version-specific updates pertain to new capabilities, but don't break existing code and are therefore not breaking changes.

If you're using Azure SDKs, multiple APIs have been renamed over time. The SDK change logs provide the details.

## API versions providing semantic ranking

Check your code for the REST API version or SDK package version to confirm which one provides semantic ranking. The following API versions have some level of support for semantic ranking.

| Release type | REST API version | Semantic ranker updates |
|---|---|---|
| initial |
|

`queryType=semantic`

to Search Documents[2021-04-30-preview](/en-us/rest/api/searchservice/preview-api/search-documents)`semanticConfiguration`

to Create or Update Index[2023-07-01-preview](/en-us/rest/api/searchservice/preview-api/search-documents)`semanticConfiguration`

. Starting on July 14, 2023 updates to the Microsoft-hosted semantic models made semantic ranker language-agnostic, effectively decommissioning the `queryLanguage`

property for semantic ranking. There's no breaking change in code, but the property is ignored. Customers were advised to remove this property from code.[2023-10-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2023-10-01-preview&preserve-view=true)`semanticQuery`

to send a query used only for reranking purposes.[2023-11-01](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2023-11-01&preserve-view=true)`semanticConfiguration`

that progressed to the stable version. If your code targets this version or later, it's compatible with newer API versions unless you adopt new preview features.[2024-05-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2024-05-01-preview&preserve-view=true)[2024-07-01](/en-us/rest/api/searchservice/indexes/create-or-update?view=rest-searchservice-2024-07-01&preserve-view=true)[2024-09-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2024-09-01-preview&preserve-view=true)[2024-11-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2024-11-01-preview&preserve-view=true)`queryLanguage`

property is now required if you use [query rewrite (preview)](semantic-how-to-query-rewrite).[2025-03-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-03-01-preview&preserve-view=true)[2025-05-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-05-01-preview&preserve-view=true)[better integration with scoring profiles](semantic-how-to-enable-scoring-profiles).[2025-08-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-08-01-preview&preserve-view=true)[2025-11-01-preview](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-11-01-preview&preserve-view=true)## Change logs for Azure SDKs

To determine which semantic features are available in a specific Azure SDK package and whether any APIs have been renamed, see the SDK's change log:

[Azure SDK for .NET change log](https://github.com/Azure/azure-sdk-for-net/blob/Azure.Search.Documents_11.5.1/sdk/search/Azure.Search.Documents/CHANGELOG.md#1150-2023-11-10&preserve-view=true)[Azure SDK for Python change log](https://github.com/Azure/azure-sdk-for-python/blob/main/sdk/search/azure-search-documents/CHANGELOG.md#1140-2023-10-13&preserve-view=true)[Azure SDK for Java change log](https://github.com/Azure/azure-sdk-for-java/blob/azure-search-documents_11.6.1/sdk/search/azure-search-documents/CHANGELOG.md#1160-2023-11-13&preserve-view=true)[Azure SDK for JavaScript change log](https://github.com/Azure/azure-sdk-for-js/blob/%40azure/search-documents_12.0.0/sdk/search/search-documents/CHANGELOG.md#1200-2023-11-13&preserve-view=true)

## 2024-11-01-preview

- Adds
[query rewrite](semantic-how-to-query-rewrite)to Search Documents. - Requires
`queryLanguage`

for query rewrite workloads. For a list of valid values, see the[REST API](/en-us/rest/api/searchservice/documents/search-post?view=rest-searchservice-2024-11-01-preview#querylanguage&preserve-view=true).

## 2024-09-01-preview

No changes to semantic ranking syntax from the 2024-07-01 stable version.

## 2024-07-01

No changes to semantic ranking syntax from the 2024-05-01-preview version.

Don't use this API version. It implements a vector query syntax that's incompatible with any newer API version.

## 2024-05-01-preview

No changes to semantic ranking syntax from the 2024-03-01-preview version.

## 2024-03-01-preview

No changes to semantic ranking syntax from the 2023-10-01-preview version, but vector queries are introduced. Semantic ranking now applies to responses from hybrid and vector queries. You can apply reranking on any human-readable text fields in the response, assuming the fields are listed in `prioritizedFields`

.

## 2023-11-01

- Excludes
`SemanticDebug`

and`semanticQuery`

, otherwise the same as the 2023-10-01-preview version.

## 2023-10-01-preview

- Adds
`semanticQuery`


## 2023-07-01-preview

- Adds
`semanticErrorHandling`

,`semanticMaxWaitInMilliseconds`

. - Adds numerous semantic-related fields to the response, such as
`SemanticDebug`

and`SemanticErrorMode`

. - Ignores
`queryLanguage`

, it's no longer used in semantic ranking.

Starting on July 14, 2023, semantic ranker is language agnostic. In preview versions, semantic ranking would deprioritize results differing from the `querylanguage`

specified by the field analyzer. However, the `queryLanguage`

property is still applicable to [spell correction](speller-how-to-add) and the short list of languages supported by that feature.

## 2021-04-30-preview

- Semantic support is through
[Search Documents](/en-us/rest/api/searchservice/preview-api/search-documents)and[Create or Update Index](/en-us/rest/api/searchservice/preview-api/create-or-update-index)preview API calls. - Adds
`semanticConfiguration`

to a search index. A semantic configuration has a name and a prioritized field list. - Adds ``prioritizedFields`.

The `searchFields`

property is no longer used to prioritize fields. In all versions moving forward, `semanticConfiguration.prioritizedFields`

replaces `searchFields`

as the mechanism for specifying which fields to use for L2 ranking.

## 2020-06-30-preview

- Semantic support is through a
[Search Documents](/en-us/rest/api/searchservice/preview-api/search-documents)preview API call. - Adds
`queryType=semantic`

to the query request. - Adapts
`searchFields`

so that if the query type is semantic, the`searchFields`

property determines the priority order of field inputs to the semantic ranker. - Adds
`captions`

,`answers`

, and`highlights`

to the query response.

## Next steps

Test your semantic configuration migration by running a semantic query.


---

<!-- DOCUMENTO FUSIONADO: search-region-support.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-region-support -->

# Azure AI Search regions list

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article identifies the cloud regions in which Azure AI Search is available. It also lists which premium features are available in each region.

## Features subject to regional availability

When you create an Azure AI Search service, your region selection might depend on features that are only available in certain regions. The following table lists those region-specific features.

| Feature | Description | Availability |
|---|---|---|
|

[built-in skills](cognitive-search-predefined-skills)that make internal calls to Foundry Tools for enrichment and transformation during indexing. Integration requires that Azure AI Search coexists with a[Microsoft Foundry resource](/en-us/azure/ai-services/multi-service-resource)in the same physical region. You can bypass region requirements by using[identity-based connections](cognitive-search-attach-cognitive-services#bill-through-a-keyless-connection), currently in public preview.[Availability zones](/en-us/azure/reliability/reliability-ai-search#availability-zone-support)[Agentic retrieval](agentic-retrieval-overview)[Confidential computing](search-security-overview#data-in-use)Confidential computing disables or restricts certain features, including agentic retrieval, semantic ranker, query rewrite, and skillset execution.

[Semantic ranker](semantic-search-overview)[Query rewrite](semantic-how-to-query-rewrite)[Extra capacity](search-limits-quotas-capacity#service-limits)*don't*offer higher-capacity partitions.If you have an older search service in a supported region, check if you can [upgrade your service](search-how-to-upgrade). Otherwise, create a new search service to benefit from more capacity at the same billing rate.

[Azure Vision in Foundry Tools 4.0 multimodal APIs](search-get-started-portal-image-search)[Azure Vision region list](/en-us/azure/ai-services/computer-vision/overview-image-analysis#region-availability)first, and then verify Azure AI Search is available in the same region.## Azure Public regions

You can create an Azure AI Search service in any of the following Azure public regions. Almost all of these regions support [higher-capacity tiers](search-limits-quotas-capacity#service-limits). Exceptions are noted where applicable.

### Americas

| Region | AI enrichment | Availability zones | Agentic retrieval | Confidential computing | Semantic ranker | Query rewrite |
|---|---|---|---|---|---|---|
Brazil South 1 |
✅ | ✅ | ✅ | ✅ | ✅ | |
Canada Central 1 |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
Canada East 1 |
✅ | ✅ | ||||
| Central US | ✅ | ✅ | ✅ | ✅ | ✅ | |
East US 1, 2 |
✅ | ✅ | ✅ | ✅ | ||
East US 2 1 |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Mexico Central | ✅ | |||||
North Central US 1 |
✅ | ✅ | ✅ | ✅ | ||
South Central US 1 |
✅ | ✅ | ✅ | ✅ | ✅ | |
West US 1 |
✅ | ✅ | ✅ | ✅ | ||
West US 2 3 |
✅ | ✅ | ✅ | ✅ | ✅ | |
| West US 3 | ✅ | ✅ | ✅ | ✅ | ✅ | |
West Central US 1 |
✅ | ✅ | ✅ |

1 This region supports [agentic retrieval](agentic-retrieval-overview) and [semantic ranker](semantic-search-overview) on the free tier.

2 This region is experiencing capacity constraints that prevent the creation of new search services for Basic and S1 tiers. Please choose a different region.

3 This region doesn't have indexer support for [Microsoft Purview sensitivity labels](search-indexer-sensitivity-labels).

### Europe

| Region | AI enrichment | Availability zones | Agentic retrieval | Confidential computing | Semantic ranker | Query rewrite |
|---|---|---|---|---|---|---|
France Central 1 |
✅ | ✅ | ✅ | ✅ | ✅ | |
Germany West Central 1 |
✅ | ✅ | ✅ | ✅ | ||
| Italy North | ✅ | ✅ | ✅ | ✅ | ||
| Norway East | ✅ | ✅ | ✅ | |||
| North Europe | ✅ | ✅ | ✅ | ✅ | ✅ | |
Poland Central 1 |
✅ | ✅ | ||||
Spain Central 2 |
✅ | ✅ | ✅ | ✅ | ||
Sweden Central 1 |
✅ | ✅ | ✅ | ✅ | ✅ | |
Switzerland North 1 |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Switzerland West | ✅ | ✅ | ✅ | ✅ | ||
UK South 1 |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| UK West | ✅ | ✅ | ||||
West Europe 1 |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ |

1 This region supports [agentic retrieval](agentic-retrieval-overview) and [semantic ranker](semantic-search-overview) on the free tier.

2 [Higher storage limits](search-limits-quotas-capacity#service-limits) aren't available in this region. If you want higher limits, choose a different region.

### Middle East

| Region | AI enrichment | Availability zones | Agentic retrieval | Confidential computing | Semantic ranker | Query rewrite |
|---|---|---|---|---|---|---|
Israel Central 1 |
✅ | |||||
Qatar Central 1 |
✅ | ✅ | ✅ | |||
UAE North 2, 3 |
✅ | ✅ | ✅ | ✅ | ✅ |

1 [Higher storage limits](search-limits-quotas-capacity#service-limits) aren't available in this region. If you want higher limits, choose a different region.

2 This region supports [agentic retrieval](agentic-retrieval-overview) and [semantic ranker](semantic-search-overview) on the free tier.

3 This region is experiencing capacity constraints that prevent the creation of new search services. Please choose a different region.

### Africa

| Region | AI enrichment | Availability zones | Agentic retrieval | Confidential computing | Semantic ranker | Query rewrite |
|---|---|---|---|---|---|---|
South Africa North 1 |
✅ | ✅ | ✅ | ✅ | ✅ |

1 This region supports [agentic retrieval](agentic-retrieval-overview) and [semantic ranker](semantic-search-overview) on the free tier.

### Asia Pacific

| Region | AI enrichment | Availability zones | Agentic retrieval | Confidential computing | Semantic ranker | Query rewrite |
|---|---|---|---|---|---|---|
Australia East 1 |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Australia Southeast | ✅ | ✅ | ||||
| Central India | ✅ | ✅ | ✅ | ✅ | ✅ | |
| East Asia | ✅ | ✅ | ✅ | ✅ | ✅ | |
| Indonesia Central | ✅ | |||||
| Jio India West | ✅ | ✅ | ✅ | ✅ | ||
| Jio India Central | ||||||
Japan East 1 |
✅ | ✅ | ✅ | ✅ | ✅ | |
| Japan West | ✅ | ✅ | ✅ | |||
Korea Central 1 |
✅ | ✅ | ✅ | ✅ | ✅ | ✅ |
| Korea South | ✅ | ✅ | ||||
| Malaysia West | ✅ | |||||
| New Zealand North | ✅ | |||||
| South India | ✅ | |||||
| Southeast Asia | ✅ | ✅ | ✅ | ✅ | ✅ |

1 This region supports [agentic retrieval](agentic-retrieval-overview) and [semantic ranker](semantic-search-overview) on the free tier.

## Azure Government regions

| Region | AI enrichment | Availability zones | Agentic retrieval | Confidential computing | Semantic ranker | Query rewrite |
|---|---|---|---|---|---|---|
| Arizona | ✅ | ✅ | ✅ | ✅ | ||
| Texas | ||||||
| Virginia | ✅ | ✅ | ✅ | ✅ | ✅ |

## Azure operated by 21Vianet

| Region | AI enrichment 1 |
Availability zones | Agentic retrieval | Confidential computing | Semantic ranker | Query rewrite |
|---|---|---|---|---|---|---|
| China East | ||||||
China East 2 2 |
✅ | |||||
| China East 3 | ||||||
| China North | ||||||
China North 2 2 |
||||||
| China North 3 | ✅ | ✅ | ✅ | ✅ |

1 Only China East 2 fully supports AI enrichment. In other 21Vianet regions, you can use skillsets with the [Azure OpenAI Embedding skill](cognitive-search-skill-azure-openai-embedding) for integrated vectorization, which depends on the availability of Azure OpenAI and Azure AI Search in your region. Otherwise, AI enrichment isn't supported.

2 [Higher storage limits](search-limits-quotas-capacity#service-limits) aren't available in this region. If you want higher limits, choose a different region.
