---
merged_at: 2026-01-25T03:18:14.049952
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-filters.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-filters -->

# Add a filter to a vector query in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

`strictPostFilter`

is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

`prefilter`

and `postfilter`

are generally available in the [latest stable REST API version](/en-us/rest/api/searchservice/search-service-api-versions).

In Azure AI Search, you can use a [filter expression](search-filters) to add inclusion or exclusion criteria to a [vector query](vector-search-how-to-query). You can also specify a filtering mode that applies the filter:

- Before query execution, known as
*prefiltering*. - After query execution, known as
*postfiltering*. - After the global top-
`k`

results are identified, known as*strict postfiltering*(preview).

This article uses REST for illustration. For code samples in other languages and end-to-end solutions that include vector queries, see the [azure-search-vector-samples](https://github.com/Azure/azure-search-vector-samples) GitHub repository.

You can also use [Search Explorer](search-get-started-portal-import-vectors#check-results) in the Azure portal to query vector content. In the JSON view, you can add filters and specify the filter mode.

## How filtering works in vector queries

Azure AI Search uses the Hierarchical Navigable Small World (HNSW) algorithm for Approximate Nearest Neighbor (ANN) search, storing HNSW graphs across multiple shards. Each shard contains a portion of the entire index.

Filters apply to `filterable`

*nonvector* fields, either string or numeric, to include or exclude search documents based on filter criteria. Vector fields themselves aren't filterable, but you can use filters on other fields in the same index to narrow the documents considered for vector search. If your index lacks suitable text or numeric fields, check for document metadata that might help with filtering, such as `LastModified`

or `CreatedBy`

properties.

The `vectorFilterMode`

parameter controls where filter operations are applied during the stages of search, which affects how the results are filtered to a subset of items (such as by category, tag, or other attributes) and impacts latency, recall, and throughput. There are three modes:

`preFilter`

applies the filter*during*HNSW traversal on each shard. This mode maximizes recall but can traverse more of the graph, increasing CPU and latency for highly selective filters.`postFilter`

runs HNSW traversal and filtering on each shard independently, intersects results at the shard level, and then aggregates the top`k`

from each shard into a global top`k`

. This mode can create false negatives for highly selective filters or small`k`

values.`strictPostFilter`

(preview) finds the unfiltered global top`k`

*before*applying the filter. This mode has the highest risk of returning false negatives for highly selective filters and small`k`

values.

For more information about these modes, see [Set the filter mode](#set-the-filter-mode).

## Define a filter

Filters determine the scope of vector queries and are defined using [Documents - Search Post (REST API)](/en-us/rest/api/searchservice/documents/search-post). Unless you want to use a preview feature, use the latest stable version of the [Search Service REST APIs](/en-us/rest/api/searchservice/search-service-api-versions) to formulate the request.

This REST API provides:

`filter`

for the criteria.`vectorFilterMode`

to specify when the filter is applied during the vector query. For supported modes, see[Set the filter mode](#set-the-filter-mode).

```
POST https://{search-endpoint}/indexes/{index-name}/docs/search?api-version={api-version}
Content-Type: application/json
api-key: {admin-api-key}
{
"count": true,
"select": "title, content, category",
"filter": "category eq 'Databases'",
"vectorFilterMode": "preFilter",
"vectorQueries": [
{
"kind": "vector",
"vector": [
-0.009154141,
0.018708462,
. . . // Trimmed for readability
-0.02178128,
-0.00086512347
],
"fields": "contentVector",
"k": 50
}
]
}
```


In this example, the vector embedding targets the `contentVector`

field, and the filter criteria apply to `category`

, a filterable text field. Because the `preFilter`

mode is used, the filter is applied before the search engine runs the query, so only documents in the `Databases`

category are considered during the vector search.

## Set the filter mode

The `vectorFilterMode`

parameter determines when and how the filter is applied relative to vector query execution. You can use the following modes:

`preFilter`

(recommended)`postFilter`

`strictPostFilter`

(preview)

Note

`preFilter`

is the default for indexes created after approximately October 15, 2023. For indexes created before this date, `postFilter`

is the default. To use `preFilter`

and other advanced vector features, such as vector compression, you must recreate your index.

You can test compatibility by sending a vector query with `"vectorFilterMode": "preFilter"`

on the `2023-10-01-preview`

REST API version or later. If the query fails, your index doesn't support `preFilter`

.

Prefiltering applies filters before query execution, which reduces the candidate set for the vector search algorithm. The top-`k`

results are then selected from this filtered set.

In a vector query, `preFilter`

is the default mode because it favors recall and quality over latency.

#### How this mode works

On each shard, apply the filter predicate

*during*HNSW traversal, expanding the graph until`k`

candidates are found.Produce the prefiltered local top-

`k`

results per shard.Aggregate the filtered results into a global top-

`k`

result set.

#### Effect of this mode

Traversal expands the search surface to find more filtered candidates, especially if the filter is selective. This produces the most similar top-`k`

results across all shards. Each shard identifies the `k`

results that satisfy the filter predicate.

Prefiltering guarantees that `k`

results are returned if they exist in the index. For highly selective filters, this can cause a significant portion of the graph to be traversed, increasing computation cost and latency while reducing throughput. If your filter is highly selective (has very few matches), consider using `exhaustive: true`

to perform exhaustive search.

### Comparison table

| Mode | Recall (filtered results) | Computational cost | Risk of false negatives | When to use |
|---|---|---|---|---|
`preFilter` |
Very high | Higher (increases with filter selectivity and complexity) | No risk | Recommended default for all scenarios, especially when recall is critical (sensitive search domains), when using selective filters, or when using small `k` . |
`postFilter` |
Medium to high (decreases with filter selectivity) | Similar to unfiltered but increases with filter complexity | Moderate (can miss matches per shard) | An option for filters that aren't too selective and for higher-`k` queries. |
`strictPostFilter` |
Lowest (decreases most quickly with filter selectivity) | Similar to unfiltered | Highest (can return zero results for selective filters or small `k` ) |
An option for faceted search applications where surfacing more results after filter application impacts the user experience more than the risk of false negatives. Don't use with small `k` . |

### Benchmark testing of prefiltering and postfiltering

Important

This section applies to prefiltering and postfiltering, not strict postfiltering.

To understand the conditions under which one filter mode performs better than the other, we ran a series of tests to evaluate query outcomes over small, medium, and large indexes.

- Small (100,000 documents, 2.5-GB index, 1,536 dimensions)
- Medium (1 million documents, 25-GB index, 1,536 dimensions)
- Large (1 billion documents, 1.9-TB index, 96 dimensions)

For the small and medium workloads, we used a Standard 2 (S2) service with one partition and one replica. For the large workload, we used a Standard 3 (S3) service with 12 partitions and one replica.

Indexes had an identical construction: one key field, one vector field, one text field, and one numeric filterable field. The following index is defined using the `2023-11-03`

syntax.

```
def get_index_schema(self, index_name, dimensions):
return {
"name": index_name,
"fields": [
{"name": "id", "type": "Edm.String", "key": True, "searchable": True},
{"name": "content_vector", "type": "Collection(Edm.Single)", "dimensions": dimensions,
"searchable": True, "retrievable": True, "filterable": False, "facetable": False, "sortable": False,
"vectorSearchProfile": "defaulthnsw"},
{"name": "text", "type": "Edm.String", "searchable": True, "filterable": False, "retrievable": True,
"sortable": False, "facetable": False},
{"name": "score", "type": "Edm.Double", "searchable": False, "filterable": True,
"retrievable": True, "sortable": True, "facetable": True}
],
"vectorSearch": {
"algorithms": [
{
"name": "defaulthnsw",
"kind": "hnsw",
"hnswParameters": { "metric": "euclidean" }
}
],
"profiles": [
{
"name": "defaulthnsw",
"algorithm": "defaulthnsw"
}
]
}
}
```


In queries, we used an identical filter for both prefilter and postfilter operations. We used a simple filter to ensure that variations in performance were due to filtering mode, not filter complexity.

Outcomes were measured in queries per second (QPS).

### Takeaways

Prefiltering is almost always slower than postfiltering, except on small indexes where performance is approximately equal.

On larger datasets, prefiltering is orders of magnitude slower.

Why is prefilter the default if it's almost always slower? Prefiltering guarantees that

`k`

results are returned if they exist in the index, where the bias favors recall and precision over speed.Use postfiltering if you:

Value speed over selection (postfiltering can return fewer than

`k`

results).Use filters that aren't overly selective.

Have indexes of sufficient size such that prefiltering performance is unacceptable.


### Details

Given a dataset with 100,000 vectors at 1,536 dimensions:

When filtering more than 30% of the dataset, prefiltering and postfiltering were comparable.

When filtering less than 0.1% of the dataset, prefiltering was about 50% slower than postfiltering.


Given a dataset with 1 million vectors at 1,536 dimensions:

When filtering more than 30% of the dataset, prefiltering was about 30% slower.

When filtering less than 2% of the dataset, prefiltering was about seven times slower.


Given a dataset with 1 billion vectors at 96 dimensions:

When filtering more than 5% of the dataset, prefiltering was about 50% slower.

When filtering less than 10% of the dataset, prefiltering was about seven times slower.


The following graph shows prefilter relative QPS, computed as prefilter QPS divided by postfilter QPS.

The vertical axis represents the relative performance of prefiltering compared to postfiltering, expressed as a ratio of QPS (queries per second). For example:

- A value of
`0.0`

means prefiltering is 100% slower than postfiltering. - A value of
`0.5`

means prefiltering is 50% slower. - A value of
`1.0`

means prefiltering and post filtering are equivalent.

The horizontal axis represents the filtering rate, or the percentage of candidate documents after applying the filter. For example, a rate of `1.00%`

means the filter criteria selected one percent of the search corpus.


---

<!-- DOCUMENTO FUSIONADO: cognitive-search-skill-annotation-language.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-skill-annotation-language -->

# Skill context and input annotation language

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article is the reference documentation for skill context and input syntax. It's a full description of the expression language used to construct paths to nodes in an enriched document.

Azure AI Search skills can use and [enrich the data coming from the data source and from the output of other skills](cognitive-search-defining-skillset).
The data working set that represents the current state of the indexer work for the current document starts from the raw data coming from the data source and is
progressively enriched with each skill iteration's output data.
That data is internally organized in a tree-like structure that can be queried to be used as skill inputs or to be added to the index.
The nodes in the tree can be simple values such as strings and numbers, arrays, or complex objects and even binary files.
Even simple values can be enriched with more structured information.
For example, a string can be annotated with additional information that is stored beneath it in the enrichment tree.
The expressions used to query that internal structure use a rich syntax that is detailed in this article.
The enriched data structure can be [inspected from debug sessions](cognitive-search-debug-session).
Expressions querying the structure can also be tested from debug sessions.

Throughout the article, we use the following enriched data as an example.
This data is typical of the kind of structure you would get when enriching a document using a skillset with [OCR](cognitive-search-skill-ocr), [key phrase extraction](cognitive-search-skill-keyphrases), [text translation](cognitive-search-skill-text-translation), [language detection](cognitive-search-skill-language-detection), and [entity recognition](cognitive-search-skill-entity-recognition-v3) skills, plus a custom tokenizer skill.

| Path | Value |
|---|---|
`document` |
|
`merged_content` |
"Study of BMN 110 in Pediatric Patients"... |
`keyphrases` |
|
`[0]` |
"Study of BMN" |
`[1]` |
"Syndrome" |
`[2]` |
"Pediatric Patients" |
| ... | |
`locations` |
|
`[0]` |
"IVA" |
`translated_text` |
"Étude de BMN 110 chez les patients pédiatriques"... |
`entities` |
|
`[0]` |
|
`category` |
"Organization" |
`subcategory` |
`null` |
`confidenceScore` |
0.72 |
`length` |
3 |
`offset` |
9 |
`text` |
"BMN" |
| ... | |
`organizations` |
|
`[0]` |
"BMN" |
`language` |
"en" |
`normalized_images` |
|
`[0]` |
|
`layoutText` |
... |
`text` |
|
`words` |
|
`[0]` |
"Study" |
`[1]` |
"of" |
`[2]` |
"BMN" |
`[3]` |
"110" |
| ... | |
`[1]` |
|
`layoutText` |
... |
`text` |
|
`words` |
|
`[0]` |
"it" |
`[1]` |
"is" |
`[2]` |
"certainly" |
| ... | |
| ... | |
| ... |

## Document root

Data is under one root element and the path is `"/document"`

. The root element is the default context for skills.

## Simple paths

Simple paths through the internal enriched document can be expressed with simple tokens separated by slashes.
This syntax is similar to [the JSON Pointer specification](https://datatracker.ietf.org/doc/html/rfc6901.html).

### Object properties

The properties of nodes that represent objects add their values to the tree under the property's name. Those values can be obtained by appending the property name as a token separated by a slash:

| Expression | Value |
|---|---|
`/document/merged_content/language` |
`"en"` |

Property name tokens are case-sensitive.

### Array item index

Specific elements of an array can be referenced by using their numeric index like a property name:

| Expression | Value |
|---|---|
`/document/merged_content/keyphrases/1` |
`"Syndrome"` |
`/document/merged_content/entities/0/text` |
`"BMN"` |

### Escape sequences

There are several characters that have a special meaning and need to be escaped if they're to be interpreted as-is instead of a syntax element. These characters include `#`

, `/`

, and `~`

among others.

| Escape sequence | Special meaning (usage in path syntax) | Example |
|---|---|---|
`~0` |
Used for escaping `~` |
"~0" for `~` , where "~/documents" becomes "~0~1documents" |
`~1` |
Used for escaping `/` |
"~1" for `/` , where "~/documents" becomes "~0~1documents" |
`~2` |
Used for generically to escape arbitrary sequences (including but not limited to `#` and `*` ) |
"~2#~2" where "readme#requirements" becomes "readme~2#~2requirements" |

## Array enumeration

An array of values can be obtained using the `'*'`

token:

| Expression | Value |
|---|---|
`/document/normalized_images/0/text/words/*` |
`["Study", "of", "BMN", "110" ...]` |

The `'*'`

token doesn't have to be at the end of the path. It's possible to enumerate all nodes matching a path with a star in the middle or with multiple stars:

| Expression | Value |
|---|---|
`/document/normalized_images/*/text/words/*` |
`["Study", "of", "BMN", "110" ... "it", "is", "certainly" ...]` |

This example returns a flat list of all matching nodes.

It's possible to maintain more structure and get a separate array for the words of each page by using a `'#'`

token instead of the second `'*'`

token:

| Expression | Value |
|---|---|
`/document/normalized_images/*/text/words/#` |
`[["Study", "of", "BMN", "110" ...], ["it", "is", "certainly" ...] ...]` |

The `'#'`

token expresses that the array should be treated as a single value instead of being enumerated.

### Enumerating arrays in context

It's often useful to process each element of an array in isolation and have a different set of skill inputs and outputs for each.
This best practice can be done by setting the context of the skill to an enumeration instead of the default `"/document"`

.

In the following example, we use one of the input expressions we used before, but with a different context that changes the resulting value.

| Context | Expression | Values |
|---|---|---|
`/document/normalized_images/*` |
`/document/normalized_images/*/text/words/*` |
`["Study", "of", "BMN", "110" ...]` `["it", "is", "certainly" ...]` ... |

For this combination of context and input, the skill gets executed once for each normalized image: once for `"/document/normalized_images/0"`

and once for `"/document/normalized_images/1"`

. The two input values corresponding to each skill execution are detailed in the values column.

When you enumerate an array in context, any outputs the skill produces are added to the document as enrichments of the context.
In the previous example, an output named `"out"`

has its values for each execution added to the document respectively under `"/document/normalized_images/0/out"`

and `"/document/normalized_images/1/out"`

.

## Literal values

Skill inputs can take literal values as their inputs instead of dynamic values queried from the existing document. This best practice can be achieved by prefixing the value with an equal sign. Values can be numbers, strings or Boolean.
String values can be enclosed in single `'`

or double `"`

quotes.

| Expression | Value |
|---|---|
`=42` |
`42` |
`=2.45E-4` |
`0.000245` |
`="some string"` |
`"some string"` |
`='some other string'` |
`"some other string"` |
`="unicod\u0065"` |
`"unicode"` |
`=false` |
`false` |

### In line arrays

If a certain skill input requires an array of data, but the data is represented as a single value currently or you need to combine multiple different single values into an array field, then you can create an array value inline as part of a skill input expression by wrapping a comma separated list of expressions in brackets (`[`

and `]`

). The array value can be a combination of expression paths or literal values as needed. You can also create nested arrays within arrays this way.

| Expression | Value |
|---|---|
`=['item']` |
["item"] |
`=[$(/document/merged_content/entities/0/text), 'item']` |
["BMN", "item"] |
`=[1, 3, 5]` |
[1, 3, 5] |
`=[true, true, false]` |
[true, true, false] |
`=[[$(/document/merged_content/entities/0/text), 'item'],['item2', $(/document/merged_content/keyphrases/1)]]` |
[["BMN", "item"], ["item2", "Syndrome"]] |

If the skill has a context that explains to run the skill per an array input (that is, how `"context": "/document/pages/*"`

means the skill runs once per "page" in `pages`

) then passing that value as the expression as input to an in line array uses one of those values at a time.

For an example with our sample enriched data, if your skill's `context`

is `/document/merged_content/keyphrases/*`

and then you create an inline array of the following `=['key phrase', $(/document/merged_content/keyphrases/*)]`

on an input of that skill, then the skill is executed three times, once with a value of ["key phrase", "Study of BMN"], another with a value of ["key phrase", "Syndrome"], and finally with a value of ["key phrase", "Pediatric Patients"]. The literal "key phrase" value stays the same each time, but the value of the expression path changes with each skill execution.

## Composite expressions

It's possible to combine values together using unary, binary, and ternary operators.
Operators can combine literal values and values resulting from path evaluation.
When used inside an expression, paths should be enclosed between `"$("`

and `")"`

.

### Boolean not `'!'`


| Expression | Value |
|---|---|
`=!false` |
`true` |

### Negative `'-'`


| Expression | Value |
|---|---|
`=-42` |
`-42` |
`=-$(/document/merged_content/entities/0/offset)` |
`-9` |

### Addition `'+'`


| Expression | Value |
|---|---|
`=2+2` |
`4` |
`=2+$(/document/merged_content/entities/0/offset)` |
`11` |

### Subtraction `'-'`


| Expression | Value |
|---|---|
`=2-1` |
`1` |
`=$(/document/merged_content/entities/0/offset)-2` |
`7` |

### Multiplication `'*'`


| Expression | Value |
|---|---|
`=2*3` |
`6` |
`=$(/document/merged_content/entities/0/offset)*2` |
`18` |

### Division `'/'`


| Expression | Value |
|---|---|
`=3/2` |
`1.5` |
`=$(/document/merged_content/entities/0/offset)/3` |
`3` |

### Modulo `'%'`


| Expression | Value |
|---|---|
`=15%4` |
`3` |
`=$(/document/merged_content/entities/0/offset)%2` |
`1` |

### String concatenation `'+'`


| Expression | Value |
|---|---|
`="Hello," + "world!"` |
`"Hello, world!"` |
`=$(/document/merged_content/entities/0/text) + $(/document/merged_content/entities/0/category)` |
`"BMN Organization"` |

### Less than, less than or equal, greater than and greater than or equal `'<'`

`'<='`

`'>'`

`'>='`


| Expression | Value |
|---|---|
`=15<4` |
`false` |
`=4<=4` |
`true` |
`=15>4` |
`true` |
`=1>=2` |
`false` |

### Equality and nonequality `'=='`

`'!='`


| Expression | Value |
|---|---|
`=15==4` |
`false` |
`=4==4` |
`true` |
`=15!=4` |
`true` |
`=1!=1` |
`false` |

### Logical operations and, or and exclusive or `'&&'`

`'||'`

`'^'`


| Expression | Value |
|---|---|
`=true&&true` |
`true` |
`=true&&false` |
`false` |
`=true||true` |
`true` |
`=true||false` |
`true` |
`=false||false` |
`false` |
`=true^false` |
`true` |
`=true^true` |
`false` |

### Ternary operator `'?:'`


It's possible to give an input different values based on the evaluation of a Boolean expression using the ternary operator.

| Expression | Value |
|---|---|
`=true?"true":"false"` |
`"true"` |
`=$(/document/merged_content/entities/0/offset)==9?"nine":"not nine"` |
`"nine"` |

### Parentheses and operator priority

Operators are evaluated with priorities that match usual conventions: unary operators, then multiplication, division and modulo, then addition and subtraction, then comparison, then equality, and then logical operators. Usual associativity rules also apply.

Parentheses can be used to change or disambiguate evaluation order.

| Expression | Value |
|---|---|
`=3*2+5` |
`11` |
`=3*(2+5)` |
`21` |
