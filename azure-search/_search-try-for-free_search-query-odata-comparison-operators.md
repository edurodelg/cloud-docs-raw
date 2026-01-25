---
merged_at: 2026-01-25T03:18:13.781663
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-try-for-free.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-try-for-free -->

# Try Azure AI Search for free

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you're new to Azure, you can create an Azure free account to explore Azure AI Search and other services at no charge. The free account provides credits that you can use to create and test services for 30 days.

This article explains how to maximize the value of your Azure free account to quickly and efficiently evaluate Azure AI Search.

## Prerequisites

- An internet connection and a supported web browser.
- A phone number, credit or debit card, and Microsoft or GitHub account to create an Azure free account.

## Create an Azure free account

To try Azure AI Search for free, [sign up for an Azure free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

The free account is active for 30 days and includes credits that allow you to create billable services at no charge. Currently, the credits are equivalent to USD200. This amount is subject to change, so verify the credit on the sign-up page.

## Choose a region

You can optionally integrate Azure AI Search with Foundry Tools for [AI enrichment](cognitive-search-concept-intro), [integrated vectorization](vector-search-integrated-vectorization), and [multimodal search](multimodal-search-overview). For billing purposes, you must [attach your Microsoft Foundry resource](cognitive-search-attach-cognitive-services) to your search service via a keyless connection (preview) or key-based connection. Key-based connections require both services to be in the same region.

Before you create resources for a key-based connection, confirm regional support:

: The**Azure AI Search regions****AI enrichment**column indicates whether Azure AI Search and Microsoft Foundry are in the same region.: The**Azure Vision regions****Multimodal embeddings**column indicates regional support for the multimodal APIs that enable text and image vectorization. Azure Vision provides these APIs, which you access through a Microsoft Foundry resource. Ensure that Azure AI Search and Microsoft Foundry are in the same region as the multimodal APIs.

Tip

If you don't need features powered by Foundry Tools, ignore the Azure Vision regions and choose an Azure AI Search region that provides the features and capacity you need.

## Choose a pricing tier

Azure AI Search offers several [pricing tiers](search-sku-tier), but only two tiers stay within the free account credit limits:

**Free**doesn't consume credits and provides 50 MB of storage. You can have one free search service per Azure subscription. This tier is always free and doesn't expire, even after your 30-day trial ends. However, it doesn't support semantic ranking or managed identities for Microsoft Entra ID authentication and authorization, which are commonly used in quickstarts.**Basic**(recommended) consumes about one-third of your USD200 credits over 30 days and provides 15 GB of storage in most regions. This tier supports all features, including semantic ranking and managed identities, and runs on dedicated infrastructure for consistent performance.

Note

Free search services that remain inactive for an extended period of time might be deleted to free up capacity, should the region be experiencing capacity constraints.

## Create resources

Most Azure AI Search scenarios require the following resources:

[Create an Azure AI Search service](search-create-service-portal). Choose the pricing tier that fits your needs and, if applicable, the same region as Microsoft Foundry. Most Azure AI Search regions provide higher-capacity storage limits. Only a few have older, lower limits. For the Basic tier, confirm that you have a 15-GB partition during service creation.[Create an Azure Storage account](/en-us/azure/storage/common/storage-account-create?tabs=azure-portal)to index your own files. Choose a general purpose account and use the default settings.[Create a Microsoft Foundry resource](/en-us/azure/ai-services/multi-service-resource)to use AI enrichment in your indexing workloads and the Azure Vision multimodal APIs as an embedding model provider.

## Run a quickstart

To get started with Azure AI Search, try one of the following quickstarts:

- Quickstart: Agentic retrieval (
[portal](get-started-portal-agentic-retrieval)or[programmatic](search-get-started-agentic-retrieval)) - Quickstart: Keyword search (
[portal](search-get-started-portal)or[programmatic](search-get-started-text)) - Quickstart: Vector search (
[portal](search-get-started-portal-import-vectors)or[programmatic](search-get-started-vector))

You can also explore the [azure-search-vector-samples](https://github.com/Azure/azure-search-vector-samples) GitHub repository or [solution accelerators](resource-tools). Many samples and accelerators include Bicep scripts that deploy all Azure resources and dependencies, allowing you to quickly explore operational solutions.

## Use a portal to explore features

You can access Azure AI Search through two portals, each optimized for different scenarios:

| Portal | Description | What you can do |
|---|---|---|
|

**This portal is most useful for classic search scenarios and overall resource management.**- Create and configure your search service.
- Build knowledge bases and knowledge sources for
[agentic retrieval](search-what-is-azure-search#what-is-agentic-retrieval). - Build indexes, indexers, data sources, and skillsets for
[classic search](search-what-is-azure-search#what-is-classic-search). - Query your knowledge bases and indexes.
- Track credits and monitor costs.

[Microsoft Foundry portal](https://ai.azure.com/?cid=learnDocs)**This portal is most useful for agentic retrieval (RAG) scenarios.**- Deploy embedding and chat models.
- Use
[Foundry IQ](/en-us/azure/ai-foundry/agents/how-to/tools/knowledge-retrieval)to connect your Azure AI Search knowledge base to an AI agent.

## Track your credit usage

During the trial period, you should stay under the USD200 credit allocation. Most services are on the Standard tier, so you aren't charged while they're not in use. However, an Azure AI Search service on the Basic tier is provisioned on dedicated clusters, so it's billable during its lifetime and can only be used by you. If you create a Basic search service, expect Azure AI Search to consume about one-third of your available credits during the trial period.

In the Azure portal, a notification in the upper-right corner shows how many credits have been used and how many remain. You can also monitor billing by searching for **Subscriptions** in the topmost search bar. The **Overview** page shows spending rates, forecasts, and cost management. For more information, see [Check usage of free services included with your Azure free account](/en-us/azure/cost-management-billing/manage/check-free-service-usage).

## Next step

Ready to move beyond exploration? After your free trial ends, learn how to [plan and manage capacity](search-capacity-planning) and [plan and manage costs](search-sku-manage-costs) for production workloads.


---

<!-- DOCUMENTO FUSIONADO: search-query-odata-comparison-operators.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-odata-comparison-operators -->

# OData comparison operators in Azure AI Search - eq, ne, gt, lt, ge, and le

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

# OData comparison operators in Azure AI Search -

The most basic operation in an [OData filter expression](query-odata-filter-orderby-syntax) in Azure AI Search is to compare a field to a given value. Two types of comparison are possible -- equality comparison, and range comparison. You can use the following operators to compare a field to a constant value:

Equality operators:

`eq`

: Test whether a field is**equal to**a constant value`ne`

: Test whether a field is**not equal to**a constant value

Range operators:

`gt`

: Test whether a field is**greater than**a constant value`lt`

: Test whether a field is**less than**a constant value`ge`

: Test whether a field is**greater than or equal to**a constant value`le`

: Test whether a field is**less than or equal to**a constant value

You can use the range operators in combination with the [logical operators](search-query-odata-logical-operators) to test whether a field is within a certain range of values. See the [examples](#examples) later in this article.

Note

If you prefer, you can put the constant value on the left side of the operator and the field name on the right side. For range operators, the meaning of the comparison is reversed. For example, if the constant value is on the left, `gt`

would test whether the constant value is greater than the field. You can also use the comparison operators to compare the result of a function, such as `geo.distance`

, with a value. For Boolean functions such as `search.ismatch`

, comparing the result to `true`

or `false`

is optional.

## Syntax

The following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) defines the grammar of an OData expression that uses the comparison operators.

```
comparison_expression ::=
variable_or_function comparison_operator constant |
constant comparison_operator variable_or_function
variable_or_function ::= variable | function_call
comparison_operator ::= 'gt' | 'lt' | 'ge' | 'le' | 'eq' | 'ne'
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

There are two forms of comparison expressions. The only difference between them is whether the constant appears on the left- or right-hand-side of the operator. The expression on the other side of the operator must be a **variable** or a function call. A variable can be either a field name, or a range variable in the case of a [lambda expression](search-query-odata-collection-operators).

## Data types for comparisons

The data types on both sides of a comparison operator must be compatible. For example, if the left side is a field of type `Edm.DateTimeOffset`

, then the right side must be a date-time constant. Numeric data types are more flexible. You can compare variables and functions of any numeric type with constants of any other numeric type, with a few limitations, as described in the following table.

| Variable or function type | Constant value type | Limitations |
|---|---|---|
`Edm.Double` |
`Edm.Double` |
Comparison is subject to
`NaN` |

`Edm.Double`

`Edm.Int64`

`Edm.Double`

, resulting in a loss of precision for values of large magnitude`Edm.Double`

`Edm.Int32`

`Edm.Int64`

`Edm.Double`

`NaN`

, `-INF`

, or `INF`

are not allowed`Edm.Int64`

`Edm.Int64`

`Edm.Int64`

`Edm.Int32`

`Edm.Int64`

before comparison`Edm.Int32`

`Edm.Double`

`NaN`

, `-INF`

, or `INF`

are not allowed`Edm.Int32`

`Edm.Int64`

`Edm.Int32`

`Edm.Int32`

For comparisons that are not allowed, such as comparing a field of type `Edm.Int64`

to `NaN`

, the Azure AI Search REST API will return an "HTTP 400: Bad Request" error.

Important

Even though numeric type comparisons are flexible, we highly recommend writing comparisons in filters so that the constant value is of the same data type as the variable or function to which it is being compared. This is especially important when mixing floating-point and integer values, where implicit conversions that lose precision are possible.

### Special cases for `null`

and `NaN`


When using comparison operators, it's important to remember that all non-collection fields in Azure AI Search can potentially be `null`

. The following table shows all the possible outcomes for a comparison expression where either side can be `null`

:

| Operator | Result when only the field or variable is `null` |
Result when only the constant is `null` |
Result when both the field or variable and the constant are `null` |
|---|---|---|---|
`gt` |
`false` |
HTTP 400: Bad Request error | HTTP 400: Bad Request error |
`lt` |
`false` |
HTTP 400: Bad Request error | HTTP 400: Bad Request error |
`ge` |
`false` |
HTTP 400: Bad Request error | HTTP 400: Bad Request error |
`le` |
`false` |
HTTP 400: Bad Request error | HTTP 400: Bad Request error |
`eq` |
`false` |
`false` |
`true` |
`ne` |
`true` |
`true` |
`false` |

In summary, `null`

is equal only to itself, and is not less or greater than any other value.

If your index has fields of type `Edm.Double`

and you upload `NaN`

values to those fields, you will need to account for that when writing filters. Azure AI Search implements the IEEE 754 standard for handling `NaN`

values, and comparisons with such values produce non-obvious results, as shown in the following table.

| Operator | Result when at least one operand is `NaN` |
|---|---|
`gt` |
`false` |
`lt` |
`false` |
`ge` |
`false` |
`le` |
`false` |
`eq` |
`false` |
`ne` |
`true` |

In summary, `NaN`

is not equal to any value, including itself.

### Comparing geo-spatial data

You can't directly compare a field of type `Edm.GeographyPoint`

with a constant value, but you can use the `geo.distance`

function. This function returns a value of type `Edm.Double`

, so you can compare it with a numeric constant to filter based on the distance from constant geo-spatial coordinates. See the [examples](#examples) below.

### Comparing string data

Strings can be compared in filters for exact matches using the `eq`

and `ne`

operators. These comparisons are case-sensitive.

## Examples

Match documents where the `Rating`

field is between 3 and 5, inclusive:

```
Rating ge 3 and Rating le 5
```


Match documents where the `Location`

field is less than 2 kilometers from the given latitude and longitude:

```
geo.distance(Location, geography'POINT(-122.031577 47.578581)') lt 2.0
```


Match documents where the `LastRenovationDate`

field is greater than or equal to January 1st, 2015, midnight UTC:

```
LastRenovationDate ge 2015-01-01T00:00:00.000Z
```


Match documents where the `Details/Sku`

field is not `null`

:

```
Details/Sku ne null
```


Match documents for hotels where at least one room has type "Deluxe Room", where the string of the `Rooms/Type`

field matches the filter exactly:

```
Rooms/any(room: room/Type eq 'Deluxe Room')
```
