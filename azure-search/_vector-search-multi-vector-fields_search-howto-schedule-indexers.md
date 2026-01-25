---
merged_at: 2026-01-25T03:18:13.780390
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vector-search-multi-vector-fields.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-multi-vector-fields -->

# Multi-vector field support in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This feature is currently in public preview. This preview is provided without a service-level agreement and isn't recommended for production workloads. Certain features might not be supported or might have constrained capabilities. For more information, see [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

The multi-vector field support feature in Azure AI Search enables you to index multiple child vectors within a single document field. This feature is valuable for use cases like multimodal data or long-form documents, where representing the content with a single vector would lead to loss of important detail.

## Limitations

- Semantic ranker isn't supported for nested chunks within a complex field. Therefore, the semantic ranker doesn't support nested vectors in multi-vector fields.

## Understand multi-vector field support

Traditionally, vector types, for example `Collection(Edm.Single)`

could only be used in top-level fields. With the introduction of multi-vector field support, you can now use vector types in nested fields of complex collections, effectively allowing multiple vectors to be associated with a single document.

A single document can include up to 100 vectors in total, across all complex collection fields. Vector fields can only be nested one level deep.

### Index definition with multi-vector field

No new index properties are needed for this feature. Here's a sample index definition:

```
{
"name": "multivector-index",
"fields": [
{
"name": "id",
"type": "Edm.String",
"key": true,
"searchable": true
},
{
"name": "title",
"type": "Edm.String",
"searchable": true
},
{
"name": "description",
"type": "Edm.String",
"searchable": true
},
{
"name": "descriptionEmbedding",
"type": "Collection(Edm.Single)",
"dimensions": 3,
"searchable": true,
"retrievable": true,
"vectorSearchProfile": "hnsw"
},
{
"name": "scenes",
"type": "Collection(Edm.ComplexType)",
"fields": [
{
"name": "embedding",
"type": "Collection(Edm.Single)",
"dimensions": 3,
"searchable": true,
"retrievable": true,
"vectorSearchProfile": "hnsw"
},
{
"name": "timestamp",
"type": "Edm.Int32",
"retrievable": true
},
{
"name": "description",
"type": "Edm.String",
"searchable": true,
"retrievable": true
},
{
"name": "framePath",
"type": "Edm.String",
"retrievable": true
}
]
}
]
}
```


### Sample ingest document

Here's a sample document that illustrates how you might use multi-vector fields in practice:

```
{
"id": "123",
"title": "Non-Existent Movie",
"description": "A fictional movie for demonstration purposes.",
"descriptionEmbedding": [1, 2, 3],
"releaseDate": "2025-08-01",
"scenes": [
{
"embedding": [4, 5, 6],
"timestamp": 120,
"description": "A character is introduced.",
"framePath": "nonexistentmovie\\scenes\\scene120.png"
},
{
"embedding": [7, 8, 9],
"timestamp": 2400,
"description": "The climax of the movie.",
"framePath": "nonexistentmovie\\scenes\\scene2400.png"
}
]
}
```


In this example, the scenes field is a complex collection containing multiple vectors (the embedding fields), along with other associated data. Each vector represents a scene from the movie and could be used to find similar scenes in other movies, among other potential use cases.

## Query with multi-vector field support

The multi-vector field support feature introduces some changes to the query mechanism in Azure AI Search. However, the main querying process remains largely the same.
Previously, `vectorQueries`

could only target vector fields defined as top-level index fields. With this feature, we're relaxing this restriction and allowing vectorQueries to target fields that are nested within a collection of complex types (up to one level deep).
Additionally, a new query time parameter is available: `perDocumentVectorLimit`

.

- Setting
`perDocumentVectorLimit`

to`1`

ensures that at most one vector per document is matched, guaranteeing that results come from distinct documents. - Setting
`perDocumentVectorLimit`

to`0`

(unlimited) allows multiple relevant vectors from the same document to be matched.

```
{
"vectorQueries": [
{
"kind": "text",
"text": "whales swimming",
"K": 50,
"fields": "scenes/embedding",
"perDocumentVectorLimit": 0
}
],
"select": "title, scenes/timestamp, scenes/framePath"
}
```


## Rank across multiple vectors in a single field

When multiple vectors are associated with a single document, Azure AI Search uses the maximum score among them for ranking. The system uses the most relevant vector to score each document, which prevents dilution by less relevant ones.

## Retrieve relevant elements in a collection

When a collection of complex types is included in the `$select`

parameter, only the elements that matched the vector query are returned. This is useful for retrieving associated metadata such as timestamps, text descriptions, or image paths.

Note

To reduce payload size, avoid including the vector values themselves in the `$select`

parameter. Consider omitting vector storage entirely if unnecessary.

## Debug multi-vector queries (preview)

When a document includes multiple embedded vectors, such as text and image embeddings in different subfields, the system uses the highest vector score across all elements to rank the document.

To debug how each vector contributed, use the `innerHits`

debug mode (available in the latest preview REST API).

```
POST /indexes/my-index/docs/search?api-version=2025-11-01-preview
{
"vectorQueries": [
{
"kind": "vector",
"field": "keyframes.imageEmbedding",
"kNearestNeighborsCount": 5,
"vector": [ /* query vector */ ]
}
],
"debug": "innerHits"
}
```


### Example response shape

```
"@search.documentDebugInfo": {
"innerHits": {
"keyframes": [
{
"ordinal": 0,
"vectors": [
{
"imageEmbedding": {
"searchScore": 0.958,
"vectorSimilarity": 0.956
},
"textEmbedding": {
"searchScore": 0.958,
"vectorSimilarity": 0.956
}
}
]
},
{
"ordinal": 1,
"vectors": [
{
"imageEmbedding": null,
"textEmbedding": {
"searchScore": 0.872,
"vectorSimilarity": 0.869
}
}
]
}
]
}
}
```


### Field descriptions

| Field | Description |
|---|---|
`ordinal` |
Zero-based index of the element inside the collection. |
`vectors` |
One entry per searchable vector field contained in the element. |
`searchScore` |
Final score for that field, after any rescoring and boosts. |
`vectorSimilarity` |
Raw similarity returned by the distance function. |

Note

`innerHits`

currently reports only vector fields.

### Relationship to debug=vector

Here are some facts about this property:

The existing

`debug=vector`

switch remains unchanged.When used with multi-vector fields,

`@search.document`

`DebugInfo.vector.subscore`

shows the maximum score used to rank the parent document, but not per-element detail.Use

`innerHits`

to gain insight into how individual elements contributed to the score.


---

<!-- DOCUMENTO FUSIONADO: search-howto-schedule-indexers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-howto-schedule-indexers -->

# Schedule an indexer in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Indexers can be configured to run on a schedule when you set the `schedule`

property. Some situations where indexer scheduling is useful include:

- Source data is changing over time, and you want the indexer to automatically process the difference.
- Source data is very large, and you need a recurring schedule to index all of the content.
- An index is populated from multiple sources, using multiple indexers, and you want to stagger the jobs to reduce conflicts.

When indexing can't complete within the [typical 2-hour processing window](search-howto-run-reset-indexers#indexer-execution), you can schedule the indexer to run on a 2-hour cadence to work through a large volume of data. As long as your data source supports [change detection logic](search-howto-create-indexers#change-detection-and-internal-state), indexers can automatically pick up where they left off on each run.

Once an indexer is on a schedule, it remains on the schedule until you clear the interval or start time, or set `disabled`

to true. Leaving the indexer on a schedule when there's nothing to process won't impact system performance. Checking for changed content is a relatively fast operation.

## Prerequisites

A valid indexer configured with a data source and index.

[Change detection](search-howto-create-indexers#change-detection-and-internal-state)in the data source. Azure Storage and SharePoint have built-in change detection. Other data sources, such as[Azure SQL](search-how-to-index-sql-database)and[Azure Cosmos DB](search-how-to-index-cosmosdb-sql)must be enabled manually.

## Schedule definition

A schedule is part of the indexer definition. If the `schedule`

property is omitted, the indexer will only run on demand. The property has two parts.

| Property | Description |
|---|---|
| "interval" | (required) The amount of time between the start of two consecutive indexer executions. The smallest interval allowed is 5 minutes, and the longest is 1440 minutes (24 hours). It must be formatted as an XSD "dayTimeDuration" value (a restricted subset of an
The pattern for this is: `P(nD)(T(nH)(nM))` . Examples: `PT15M` for every 15 minutes, `PT2H` for every two hours. |

The following example is a schedule that starts on January 1 at midnight and runs every two hours.

```
{
"dataSourceName" : "hotels-ds",
"targetIndexName" : "hotels-idx",
"schedule" : { "interval" : "PT2H", "startTime" : "2024-01-01T00:00:00Z" }
}
```


## Configure a schedule

Schedules are specified in an indexer definition. To set up a schedule, you can use Azure portal, REST APIs, or an Azure SDK.

- Sign in to the
[Azure portal](https://portal.azure.com)and open the search service page. - On the left pane, select
**Indexers**. - Open an indexer.
- Select
**Settings**. - Scroll down to
**Schedule**, and then choose Hourly, Daily, or Custom to set a specific date, time, or custom interval.

Switch to the **Indexer Definition (JSON)** tab at the top of the index to view the schedule definition in XSD format.

## Scheduling behavior FAQ

**Can I run multiple indexer jobs in parallel?**

You can run multiple indexers simultaneously, but each indexer is single instance. You can't run two copies of the same indexer concurrently.

For text-based indexing, the scheduler can kick off as many indexer jobs as the search service supports, which is determined by the number of [search units](search-capacity-planning#concepts-search-units-replicas-partitions). For example, if the service has three replicas and four partitions, you can have 12 indexer jobs in active execution, whether initiated on demand or on a schedule.

For skills-based indexing, indexers run in a specific [execution environment](search-howto-run-reset-indexers#indexer-execution-environment). For this reason, the number of service units has no bearing on the number of skills-based indexer jobs you can run. Multiple skills-based indexers can run in parallel, but doing so depends on content processor availability within the execution environment.

**Do scheduled jobs always start at the designated time?**

Indexer processes can be queued up and might not start exactly at the time posted, depending on the processing workload and other factors. For example, if an indexer happens to still be running when its next scheduled execution is set to start, the pending execution is postponed until the next scheduled occurrence, allowing the current job to finish.

Let’s consider an example to make this more concrete. Suppose we configure an indexer schedule with an interval of hourly and a start time of January 1, 2024 at 8:00:00 AM UTC. Here's what could happen when an indexer run takes longer than an hour:

The first indexer execution starts at or around January 1, 2024 at 8:00 AM UTC. Assume this execution takes 20 minutes (or any amount of time that's less than 1 hour).

The second execution starts at or around January 1, 2024 9:00 AM UTC. Suppose that this execution takes 70 minutes - more than an hour – and it will not complete until 10:10 AM UTC.

The third execution is scheduled to start at 10:00 AM UTC, but at that time the previous execution is still running. This scheduled execution is then skipped. The next execution of the indexer won't start until 11:00 AM UTC.


In rare cases, such as during maintenance or when recovering from transient conditions, multiple indexer runs are queued up. When this occurs, the indexer executes pending workloads sequentially within the scheduled window. For example, if an indexer is scheduled to run hourly and several runs were delayed or triggered on-demand, those queued up jobs will execute back-to-back until the queue is drained. These are not additional runs, but represent previously scheduled or requested executions. While this behavior is uncommon in most scenarios, the indexer is designed to eventually process all queued tasks to maintain consistency and data freshness.

Note

If you have strict indexer execution requirements that are time-sensitive, you should consider using the [push API model](search-what-is-data-import#pushing-data-to-an-index) so you can control the indexing pipeline directly.

**What happens if indexing fails repeatedly on the same document?**

If an indexer is set to a certain schedule but repeatedly fails on the same document each time, the indexer will begin running on a less frequent interval (up to the maximum interval of at least once every 2 hours or 24 hours, depending on different implementation factors) until it successfully makes progress again. If you believe you have fixed the underlying issue, you can [run the indexer manually](search-howto-run-reset-indexers), and if indexing succeeds, the indexer will return to its regular schedule.

## Next steps

For indexers that run on a schedule, you can monitor operations by retrieving status from the search service, or obtain detailed information by enabling resource logging.
