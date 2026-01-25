---
merged_at: 2026-01-25T03:18:13.767069
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-query-odata-syntax-reference.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-odata-syntax-reference -->

# OData expression syntax reference for Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search uses [OData expressions](https://docs.oasis-open.org/odata/odata/v4.01/odata-v4.01-part2-url-conventions.html) as parameters throughout the API. Most commonly, OData expressions are used for the `$orderby`

and `$filter`

parameters. These expressions can be complex, containing multiple clauses, functions, and operators. However, even simple OData expressions like property paths are used in many parts of the Azure AI Search REST API. For example, path expressions are used to refer to subfields of complex fields everywhere in the API, such as when listing subfields in a [suggester](index-add-suggesters), a [scoring function](index-add-scoring-profiles), the `$select`

parameter, or even [fielded search in Lucene queries](query-lucene-syntax).

This article describes all these forms of OData expressions using a formal grammar. There is also an [interactive diagram](#syntax-diagram) to help visually explore the grammar.

## Formal grammar

We can describe the subset of the OData language supported by Azure AI Search using an EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) grammar. Rules are listed "top-down", starting with the most complex expressions, and breaking them down into more primitive expressions. At the top are the grammar rules that correspond to specific parameters of the Azure AI Search REST API:

, defined by the`$filter`

`filter_expression`

rule., defined by the`$orderby`

`order_by_expression`

rule., defined by the`$select`

`select_expression`

rule.- Field paths, defined by the
`field_path`

rule. Field paths are used throughout the API. They can refer to either top-level fields of an index, or subfields with one or more[complex field](search-howto-complex-data-types)ancestors.

After the EBNF is a browsable [syntax diagram](https://en.wikipedia.org/wiki/Syntax_diagram) that allows you to interactively explore the grammar and the relationships between its rules.

```
/* Top-level rules */
filter_expression ::= boolean_expression
order_by_expression ::= order_by_clause(',' order_by_clause)*
select_expression ::= '*' | field_path(',' field_path)*
field_path ::= identifier('/'identifier)*
/* Shared base rules */
identifier ::= [a-zA-Z_][a-zA-Z_0-9]*
/* Rules for $orderby */
order_by_clause ::= (field_path | sortable_function) ('asc' | 'desc')?
sortable_function ::= geo_distance_call | 'search.score()'
/* Rules for $filter */
boolean_expression ::=
collection_filter_expression
| logical_expression
| comparison_expression
| boolean_literal
| boolean_function_call
| '(' boolean_expression ')'
| variable
/* This can be a range variable in the case of a lambda, or a field path. */
variable ::= identifier | field_path
collection_filter_expression ::=
field_path'/all(' lambda_expression ')'
| field_path'/any(' lambda_expression ')'
| field_path'/any()'
lambda_expression ::= identifier ':' boolean_expression
logical_expression ::=
boolean_expression ('and' | 'or') boolean_expression
| 'not' boolean_expression
comparison_expression ::=
variable_or_function comparison_operator constant |
constant comparison_operator variable_or_function
variable_or_function ::= variable | function_call
comparison_operator ::= 'gt' | 'lt' | 'ge' | 'le' | 'eq' | 'ne'
/* Rules for constants and literals */
constant ::=
string_literal
| date_time_offset_literal
| integer_literal
| float_literal
| boolean_literal
| 'null'
string_literal ::= "'"([^'] | "''")*"'"
date_time_offset_literal ::= date_part'T'time_part time_zone
date_part ::= year'-'month'-'day
time_part ::= hour':'minute(':'second('.'fractional_seconds)?)?
zero_to_fifty_nine ::= [0-5]digit
digit ::= [0-9]
year ::= digit digit digit digit
month ::= '0'[1-9] | '1'[0-2]
day ::= '0'[1-9] | [1-2]digit | '3'[0-1]
hour ::= [0-1]digit | '2'[0-3]
minute ::= zero_to_fifty_nine
second ::= zero_to_fifty_nine
fractional_seconds ::= integer_literal
time_zone ::= 'Z' | sign hour':'minute
sign ::= '+' | '-'
/* In practice integer literals are limited in length to the precision of
the corresponding EDM data type. */
integer_literal ::= sign? digit+
float_literal ::=
sign? whole_part fractional_part? exponent?
| 'NaN'
| '-INF'
| 'INF'
whole_part ::= integer_literal
fractional_part ::= '.'integer_literal
exponent ::= 'e' sign? integer_literal
boolean_literal ::= 'true' | 'false'
/* Rules for functions */
function_call ::=
geo_distance_call |
boolean_function_call
geo_distance_call ::=
'geo.distance(' variable ',' geo_point ')'
| 'geo.distance(' geo_point ',' variable ')'
geo_point ::= "geography'POINT(" lon_lat ")'"
lon_lat ::= float_literal ' ' float_literal
boolean_function_call ::=
geo_intersects_call |
search_in_call |
search_is_match_call
geo_intersects_call ::=
'geo.intersects(' variable ',' geo_polygon ')'
/* You need at least four points to form a polygon, where the first and
last points are the same. */
geo_polygon ::=
"geography'POLYGON((" lon_lat ',' lon_lat ',' lon_lat ',' lon_lat_list "))'"
lon_lat_list ::= lon_lat(',' lon_lat)*
search_in_call ::=
'search.in(' variable ',' string_literal(',' string_literal)? ')'
/* Note that it is illegal to call search.ismatch or search.ismatchscoring
from inside a lambda expression. */
search_is_match_call ::=
'search.ismatch'('scoring')?'(' search_is_match_parameters ')'
search_is_match_parameters ::=
string_literal(',' string_literal(',' query_type ',' search_mode)?)?
query_type ::= "'full'" | "'simple'"
search_mode ::= "'any'" | "'all'"
```


## Syntax diagram

To visually explore the OData language grammar supported by Azure AI Search, try the interactive syntax diagram:


---

<!-- DOCUMENTO FUSIONADO: search-how-to-upgrade.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-upgrade -->

# Upgrade your Azure AI Search service in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An upgrade brings older search services to the capabilities of new services created in the same region. Specifically, it upgrades the computing power of the underlying service. This one-time operation doesn't introduce breaking changes to your application, and you shouldn't need to change any code.

For [eligible services](#upgrade-eligibility), an upgrade increases the [partition storage](#higher-storage-limits) and [vector index size](#higher-vector-limits) on the same pricing tier at no extra cost.

This article describes how to upgrade your service in the [Azure portal](https://portal.azure.com/). Alternatively, you can use the [Search Management REST APIs](/en-us/rest/api/searchmanagement/) to upgrade your service programmatically. For more information, see [Manage your search service using REST](search-manage-rest#upgrade-a-service).

Tip

Looking to [change your pricing tier](search-capacity-planning#change-your-pricing-tier)? You can switch between Basic and Standard (S1, S2, and S3) tiers.

## About service upgrades

In April 2024, Azure AI Search increased the [storage capacity](search-limits-quotas-capacity#service-limits) of newly created search services. Services created before April 2024 saw no capacity changes, so if you wanted larger and faster partitions, you had to create a new service. However, some older services can now be upgraded to benefit from the higher-capacity partitions.

Currently, an upgrade only increases the [storage limit](#higher-storage-limits) and [vector index size](#higher-vector-limits) of [eligible services](#upgrade-eligibility).

### Upgrade eligibility

To qualify for an upgrade, your service must:

- Have been
[created before April 3, 2024](#check-your-service-creation-or-upgrade-date). Services created after this date should already have higher capacity. - Be in a
[region where higher capacity is enabled](search-limits-quotas-capacity#partition-storage-gb). Most regions provide higher-capacity partitions, as noted in the table's footnotes. - Be in a
[region that doesn't have capacity constraints on your pricing tier](search-region-support). Constrained regions and tiers are noted in the footnotes of each table.

Important

Some search services created before January 1, 2019 don't support upgrades. In this situation, you must create a new service in a [high-capacity region](search-limits-quotas-capacity#partition-storage-gb) to get increased storage and vector limits.

### Higher storage limits

For [eligible services](#upgrade-eligibility), the following table compares the storage limit (per partition) before and after an upgrade.

Basic 1 |
S1 | S2 | S3/HD | L1 | L2 | |
|---|---|---|---|---|---|---|
Limit before upgrade |
2 GB | 25 GB | 100 GB | 200 GB | 1 TB | 2 TB |
Limit after upgrade |
15 GB | 160 GB | 512 GB | 1 TB | 2 TB | 4 TB |

1 Basic services created before April 3, 2024 were originally limited to one partition, which increases to three partitions after an upgrade. [Partition counts for all other pricing tiers](search-limits-quotas-capacity#service-limits) stay the same.

### Higher vector limits

For [eligible services](#upgrade-eligibility), the following table compares the vector index size (per partition) before and after an upgrade.

| Basic | S1 | S2 | S3/HD | L1 | L2 | |
|---|---|---|---|---|---|---|
Limit before upgrade |
0.5 GB 1 or 1 GB 2 |
1 GB 1 or 3 GB 2 |
6 GB 1 or 12 GB 2 |
12 GB 1 or 36 GB 2 |
12 GB | 36 GB |
Limit after upgrade |
5 GB | 35 GB | 150 GB | 300 GB | 150 GB | 300 GB |

1 Applies to services created before July 1, 2023.

2 Applies to services created between July 1, 2023 and April 3, 2024 in all regions except Germany West Central, Qatar Central, and West India, to which the 1 limits apply.

## Check your service creation or upgrade date

On the **Overview** page, you can view various metadata about your search service, including **Date created** and **Date upgraded**.

The date you created your service partially determines its [upgrade eligibility](#upgrade-eligibility). If your service has never been upgraded, **Date upgraded** doesn't appear.

## Upgrade your service

You can't undo a service upgrade. Before you proceed, make sure that you want to permanently increase the [storage limit](#higher-storage-limits) and [vector index size](#higher-vector-limits) of your search service. We recommend that you test this operation in a nonproduction environment.

The availability of your search service during an upgrade depends on how many replicas you've provisioned. With two or more replicas, your service remains available while one replica is updated. For more information, see [Reliability in Azure AI Search](/en-us/azure/reliability/reliability-ai-search).

To upgrade your service:

Sign in to the

[Azure portal](https://portal.azure.com/)and select your search service.On the

**Overview**page, select**Upgrade**from the command bar.If this button appears dimmed, an upgrade isn’t available for your service. Your service either

[has the latest upgrade](#check-your-service-creation-or-upgrade-date)or[doesn't qualify for an upgrade](#upgrade-eligibility).Review the upgrade details for your service, and then select

**Upgrade**.A confirmation appears reminding you that the upgrade can't be undone.

To permanently upgrade your service, select

**Upgrade**.Check your notifications to confirm that the operation started.

Depending on the size of your service, this operation can take several hours to complete. If the upgrade fails, your service returns to its original state.


## Next step

After you upgrade your search service, you might want to reconsider your scale configuration:
