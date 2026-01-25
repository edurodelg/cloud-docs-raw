---
merged_at: 2026-01-25T03:18:13.754702
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: semantic-how-to-enable-scoring-profiles.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/semantic-how-to-enable-scoring-profiles -->

# Use scoring profiles with semantic ranker in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can apply a [scoring profile](index-add-scoring-profiles) over [semantically ranked search results](semantic-search-overview), where the scoring profile is processed last.

To ensure the scoring profile provides the determining score, the semantic ranker adds a response field, `@search.rerankerBoostedScore`

, that applies scoring profile logic on semantically ranked results. In search results that include `@search.score`

from level 1 ranking, `@search.rerankerScore`

from semantic ranker, and `@search.reRankerBoostedScore`

, results are sorted by `@search.reRankerBoostedScore`

.

## Prerequisites

[Azure AI Search](search-create-service-portal)in any[region that provides semantic ranking](search-region-support), with[semantic ranker enabled](semantic-how-to-enable-disable).A search index with a semantic configuration that specifies

`"rankingOrder": "boostedRerankerScore"`

and a scoring profile that specifies[functions](index-add-scoring-profiles#use-functions).

## Limitations

Boosting of semantically ranked results applies to scoring profile functions only. There's no boosting if the scoring profile consists only of weighted text fields.

## How does semantic configuration with scoring profiles work?

When you execute a semantic query associated with a scoring profile, a third search score, `@search.rerankerBoostedScore`

value, is generated for every document in your search results. This boosted score, calculated by applying the scoring profile to the existing reranker score, doesn't have a guaranteed range (0–4) like a normal reranker score, and scores can be significantly higher than 4.

Semantic results are sorted by `@search.rerankerBoostedScore`

by default if a scoring profile exists. If the `rankingOrder`

property isn't specified, then `BoostedRerankerScore`

is the default value in the semantic configuration.

In this scenario, a scoring profile is used twice.

First, the scoring profile defined in your index is used during the initial L1 ranking phase, boosting results from:

- Text-based queries (BM25 or RRF)
- The text portion of vector queries
- Hybrid queries that combine both types

Next, the semantic ranker rescores the top 50 results, promoting more semantically relevant matches to the top. This step can erase the benefit of the scoring profile. For example, if you boosted based on freshness, then semantic reordering replaces that boost with its own logic of what is most relevant.

Finally, the scoring profile is applied again, after reranking, restoring the boosts influence over the final order of results. If you boost by freshness, the semantically ranked results are rescored based on freshness.


## Enable scoring profiles in semantic configuration

To enable scoring profiles for semantically ranked results, [update an index](/en-us/rest/api/searchservice/indexes/create-or-update#rankingorder) by setting the `rankingOrder`

property of its semantic configuration. Use the PUT method to update the index with your revisions. No index rebuild is required.

```
PUT https://{service-name}.search.windows.com/indexes/{index-name}?api-version=2025-09-01
{
"semantic": {
"configurations": [
{
"name": "mySemanticConfig",
"rankingOrder": "boostedRerankerScore"
}
]
}
}
```


## Disable scoring profiles in semantic configuration

To opt out of sorting by semantic reranker boosted score, set the `rankingOrder`

field to `reRankerScore`

value in the semantic configuration.

```
PUT /indexes/{index-name}?api-version=2025-09-01
{
"semantic": {
"configurations": [
{
"name": "mySemanticConfig",
"rankingOrder": "reRankerScore"
}
]
}
}
```


Even if you opt out of sorting by `@search.rerankerBoostedScore`

, the `boostedRerankerScore`

field is still produced in the response, but it's no longer used to sort results.

## Example query and response

Start with a [semantic query](semantic-how-to-query-request) that specifies a scoring profile. This query targets a search index that has `rankingOrder`

set to `boostedRerankerScore`

.

```
POST /indexes/{index-name}/docs/search?api-version=2025-09-01
{
"search": "my query to be boosted",
"scoringProfile": "myScoringProfile",
"queryType": "semantic"
}
```


The response includes the new `rerankerBoostedScore`

, alongside the L1 `@search.score`

and the L2 `@search.rerankerScore`

. Results are ordered by `@search.rerankerBoostedScore`

.

```
{
"value": [
{
"@search.score": 0.63,
"@search.rerankerScore": 2.98,
"@search.rerankerBoostedScore": 7.68,
"content": "boosted content 2"
},
{
"@search.score": 1.12,
"@search.rerankerScore": 3.12,
"@search.rerankerBoostedScore": 5.61,
"content": "boosted content 1"
}
]
}
```


---

<!-- DOCUMENTO FUSIONADO: search-query-odata-logical-operators.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-odata-logical-operators -->

# OData logical operators in Azure AI Search - and, or, not

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

# OData logical operators in Azure AI Search -

[OData filter expressions](query-odata-filter-orderby-syntax) in Azure AI Search are Boolean expressions that evaluate to `true`

or `false`

. You can write a complex filter by writing a series of [simpler filters](search-query-odata-comparison-operators) and composing them using the logical operators from [Boolean algebra](https://en.wikipedia.org/wiki/Boolean_algebra):

`and`

: A binary operator that evaluates to`true`

if both its left and right sub-expressions evaluate to`true`

.`or`

: A binary operator that evaluates to`true`

if either one of its left or right sub-expressions evaluates to`true`

.`not`

: A unary operator that evaluates to`true`

if its sub-expression evaluates to`false`

, and vice-versa.

These, together with the [collection operators any and all](search-query-odata-collection-operators), allow you to construct filters that can express very complex search criteria.


## Syntax

The following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) defines the grammar of an OData expression that uses the logical operators.

```
logical_expression ::=
boolean_expression ('and' | 'or') boolean_expression
| 'not' boolean_expression
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

There are two forms of logical expressions: binary (`and`

/`or`

), where there are two sub-expressions, and unary (`not`

), where there is only one. The sub-expressions can be Boolean expressions of any kind:

- Fields or range variables of type
`Edm.Boolean`

- Functions that return values of type
`Edm.Boolean`

, such as`geo.intersects`

or`search.ismatch`

[Comparison expressions](search-query-odata-comparison-operators), such as`rating gt 4`

[Collection expressions](search-query-odata-collection-operators), such as`Rooms/any(room: room/Type eq 'Deluxe Room')`

- The Boolean literals
`true`

or`false`

. - Other logical expressions constructed using
`and`

,`or`

, and`not`

.

Important

There are some situations where not all kinds of sub-expression can be used with `and`

/`or`

, particularly inside lambda expressions. See [OData collection operators in Azure AI Search](search-query-odata-collection-operators#limitations) for details.

### Logical operators and `null`


Most Boolean expressions such as functions and comparisons cannot produce `null`

values, and the logical operators cannot be applied to the `null`

literal directly (for example, `x and null`

is not allowed). However, Boolean fields can be `null`

, so you need to be aware of how the `and`

, `or`

, and `not`

operators behave in the presence of null. This is summarized in the following table, where `b`

is a field of type `Edm.Boolean`

:

| Expression | Result when `b` is `null` |
|---|---|
`b` |
`false` |
`not b` |
`true` |
`b eq true` |
`false` |
`b eq false` |
`false` |
`b eq null` |
`true` |
`b ne true` |
`true` |
`b ne false` |
`true` |
`b ne null` |
`false` |
`b and true` |
`false` |
`b and false` |
`false` |
`b or true` |
`true` |
`b or false` |
`false` |

When a Boolean field `b`

appears by itself in a filter expression, it behaves as if it had been written `b eq true`

, so if `b`

is `null`

, the expression evaluates to `false`

. Similarly, `not b`

behaves like `not (b eq true)`

, so it evaluates to `true`

. In this way, `null`

fields behave the same as `false`

. This is consistent with how they behave when combined with other expressions using `and`

and `or`

, as shown in the table above. Despite this, a direct comparison to `false`

(`b eq false`

) will still evaluate to `false`

. In other words, `null`

is not equal to `false`

, even though it behaves like it in Boolean expressions.

## Examples

Match documents where the `rating`

field is between 3 and 5, inclusive:

```
rating ge 3 and rating le 5
```


Match documents where all elements of the `ratings`

field are less than 3 or greater than 5:

```
ratings/all(r: r lt 3 or r gt 5)
```


Match documents where the `location`

field is within the given polygon, and the document does not contain the term "public".

```
geo.intersects(location, geography'POLYGON((-122.031577 47.578581, -122.031577 47.678581, -122.131577 47.678581, -122.031577 47.578581))') and not search.ismatch('public')
```


Match documents for hotels in Vancouver, Canada where there is a deluxe room with a base rate less than 160:

```
Address/City eq 'Vancouver' and Address/Country eq 'Canada' and Rooms/any(room: room/Type eq 'Deluxe Room' and room/BaseRate lt 160)
```
