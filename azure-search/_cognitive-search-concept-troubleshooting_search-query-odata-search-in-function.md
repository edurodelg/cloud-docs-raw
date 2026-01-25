---
merged_at: 2026-01-25T03:18:13.757785
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cognitive-search-concept-troubleshooting.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/cognitive-search-concept-troubleshooting -->

# Tips for AI enrichment in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article contains tips to help you get started with AI enrichment and skillsets used during indexing.

## Tip 1: Start simple and start small

Both the [ Import data wizard](search-get-started-skillset) and the

[in the Azure portal support AI enrichment. Without writing any code, you can create and examine all of the objects used in an enrichment pipeline: an index, indexer, data source, and skillset.](search-get-started-portal-import-vectors)

**Import data (new)**wizardAnother way to start simply is by creating a data source with just a handful of documents or rows in a table that are representative of the documents that will be indexed. A small data set is the best way to increase the speed of finding and fixing issues.Run your sample through the end-to-end pipeline and check that the results meet your needs. Once you're satisfied with the results, you're ready to add more files to your data source.

## Tip 2: See what works even if there are some failures

Sometimes a small failure stops an indexer in its tracks. That is fine if you plan to fix issues one by one. However, you might want to ignore a particular type of error, allowing the indexer to continue so that you can see what flows are actually working.

To ignore errors during development, set `maxFailedItems`

and `maxFailedItemsPerBatch`

as -1 as part of the indexer definition.

```
{
// rest of your indexer definition
"parameters":
{
"maxFailedItems":-1,
"maxFailedItemsPerBatch":-1
}
}
```


Note

As a best practice, set the `maxFailedItems`

and `maxFailedItemsPerBatch`

to 0 for production workloads

## Tip 3: Use Debug session to troubleshoot issues

[ Debug session](cognitive-search-debug-session) is a visual editor that shows a skillset's dependency graph, inputs and outputs, and definitions. It works by loading a single document from your search index, with the current indexer and skillset configuration. You can then run the entire skillset, scoped to a single document. Within a debug session, you can identify and resolve errors, validate changes, and commit changes to a parent skillset. For a walkthrough, see

[Tutorial: debug sessions](cognitive-search-tutorial-debug-sessions).

## Tip 4: Expected content fails to appear

If you're missing content, check for dropped documents in the Azure portal. In the search service page, open **Indexers** and look at the **Docs succeeded** column. Click through to indexer execution history to review specific errors.

If the problem is related to file size, you might see an error like this: "The blob <file-name>" has the size of <file-size> bytes, which exceed the maximum size for document extraction for your current service tier." For more information on indexer limits, see [Service limits](search-limits-quotas-capacity).

A second reason for content failing to appear might be related input/output mapping errors. For example, an output target name is "People" but the index field name is lower-case "people". The system could return 201 success messages for the entire pipeline so you think indexing succeeded, when in fact a field is empty.

## Tip 5: Extend processing beyond maximum run time

Image analysis is computationally intensive for even simple cases, so when images are especially large or complex, processing times can exceed the maximum time allowed.

For indexers that have skillsets, skillset execution is [capped at 2 hours for most tiers](search-limits-quotas-capacity#indexer-limits). If skillset processing fails to complete within that period, you can put your indexer on a 2-hour recurring schedule to have the indexer pick up processing where it left off.

Scheduled indexing resumes at the last known good document. On a recurring schedule, the indexer can work its way through the image backlog over a series of hours or days, until all unprocessed images are processed. For more information on schedule syntax, see [Schedule an indexer](search-howto-schedule-indexers).

Note

If an indexer is set to a certain schedule but repeatedly fails on the same document over and over again each time it runs, the indexer will begin running on a less frequent interval (up to the maximum of at least once every 24 hours) until it successfully makes progress again. = If you believe you have fixed whatever the issue that was causing the indexer to be stuck at a certain point, you can perform an on-demand run of the indexer, and if that successfully makes progress, the indexer will return to its set schedule interval again.

## Tip 6: Increase indexing throughput

For [parallel indexing](search-howto-large-index), distribute your data into multiple containers or multiple virtual folders inside the same container. Then create multiple data source and indexer pairs. All indexers can use the same skillset and write into the same target search index, so your search app doesn’t need to be aware of this partitioning.


---

<!-- DOCUMENTO FUSIONADO: search-query-odata-search-in-function.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-query-odata-search-in-function -->

# OData search.in function in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

# OData

A common scenario in [OData filter expressions](query-odata-filter-orderby-syntax) is to check whether a single field in each document is equal to one of many possible values. For example, this is how some applications implement [security trimming](search-security-trimming-for-azure-search) -- by checking a field containing one or more principal IDs against a list of principal IDs representing the user issuing the query. One way to write a query like this is to use the [ eq](search-query-odata-comparison-operators) and

[operators:](search-query-odata-logical-operators)

`or`

```
group_ids/any(g: g eq '123' or g eq '456' or g eq '789')
```


However, there is a shorter way to write this, using the `search.in`

function:

```
group_ids/any(g: search.in(g, '123, 456, 789'))
```


Important

Besides being shorter and easier to read, using `search.in`

also provides [performance benefits](#bkmk_performance) and avoids certain [size limitations of filters](search-query-odata-filter#bkmk_limits) when there are hundreds or even thousands of values to include in the filter. For this reason, we strongly recommend using `search.in`

instead of a more complex disjunction of equality expressions.

Note

Version 4.01 of the OData standard has recently introduced the [ in operator](https://docs.oasis-open.org/odata/odata/v4.01/cs01/part2-url-conventions/odata-v4.01-cs01-part2-url-conventions.html#_Toc505773230), which has similar behavior as the

`search.in`

function in Azure AI Search. However, Azure AI Search does not support this operator, so you must use the `search.in`

function instead.## Syntax

The following EBNF ([Extended Backus-Naur Form](https://en.wikipedia.org/wiki/Extended_Backus%E2%80%93Naur_form)) defines the grammar of the `search.in`

function:

```
search_in_call ::=
'search.in(' variable ',' string_literal(',' string_literal)? ')'
```


An interactive syntax diagram is also available:

Note

See [OData expression syntax reference for Azure AI Search](search-query-odata-syntax-reference) for the complete EBNF.

The `search.in`

function tests whether a given string field or range variable is equal to one of a given list of values. Equality between the variable and each value in the list is determined in a case-sensitive fashion, the same way as for the `eq`

operator. Therefore an expression like `search.in(myfield, 'a, b, c')`

is equivalent to `myfield eq 'a' or myfield eq 'b' or myfield eq 'c'`

, except that `search.in`

will yield much better performance.

There are two overloads of the `search.in`

function:

`search.in(variable, valueList)`

`search.in(variable, valueList, delimiters)`


The parameters are defined in the following table:

| Parameter name | Type | Description |
|---|---|---|
`variable` |
`Edm.String` |
A string field reference (or a range variable over a string collection field in the case where `search.in` is used inside an `any` or `all` expression). |
`valueList` |
`Edm.String` |
A string containing a delimited list of values to match against the `variable` parameter. If the `delimiters` parameter is not specified, the default delimiters are space and comma. |
`delimiters` |
`Edm.String` |
A string where each character is treated as a separator when parsing the `valueList` parameter. The default value of this parameter is `' ,'` which means that any values with spaces and/or commas between them will be separated. If you need to use separators other than spaces and commas because your values include those characters, you can specify alternate delimiters such as `'|'` in this parameter. |

### Performance of `search.in`


If you use `search.in`

, you can expect sub-second response time when the second parameter contains a list of hundreds or thousands of values. There is no explicit limit on the number of items you can pass to `search.in`

, although you are still limited by the maximum request size. However, the latency will grow as the number of values grows.

## Examples

Find all hotels with name equal to either 'Sea View motel' or 'Budget hotel'. Phrases contain spaces, which is a default delimiter. You can specify an alternative delimiter in single quotes as the third string parameter:

```
search.in(HotelName, 'Sea View motel,Budget hotel', ',')
```


Find all hotels with name equal to either 'Sea View motel' or 'Budget hotel' separated by '|'):

```
search.in(HotelName, 'Sea View motel|Budget hotel', '|')
```


Find all hotels with rooms that have the tag 'wifi' or 'tub':

```
Rooms/any(room: room/Tags/any(tag: search.in(tag, 'wifi, tub')))
```


Find a match on phrases within a collection, such as 'heated towel racks' or 'hairdryer included' in tags.

```
Rooms/any(room: room/Tags/any(tag: search.in(tag, 'heated towel racks,hairdryer included', ','))
```


Find all hotels without the tag 'motel' or 'cabin':

```
Tags/all(tag: not search.in(tag, 'motel, cabin'))
```
