---
source_url: https://learn.microsoft.com/en-us/azure/search/search-howto-run-reset-indexers
fetched_at: 2026-01-25T02:08:52.338863
---

# Run or reset indexers, skills, or documents

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure AI Search, there are several ways to run an indexer:

[Run immediately upon indexer creation](search-howto-create-indexers). This is the default unless you create the indexer in a "disabled" state.[Run on a schedule](search-howto-schedule-indexers)to invoke execution at regular intervals.- Run on demand, with or without a "reset".

This article explains how to run indexers on demand, with and without a reset. It also describes indexer execution, duration, and concurrency.

## How indexers connect to Azure resources

Indexers are one of the few subsystems that make overt outbound calls to other Azure resources. Depending on the external data source, you can use keys or roles to authenticate the connection.

In terms of Azure roles, indexers don't have separate identities: a connection from the search engine to another Azure resource is made using the [system or user-assigned managed identity](search-how-to-managed-identities) of a search service, plus a role assignment on the target Azure resource. If the indexer connects to an Azure resource on a virtual network, you should create a [shared private link](search-indexer-howto-access-private) for that connection.

## Indexer execution

A search service runs one indexer job per [search unit](search-capacity-planning#concepts-search-units-replicas-partitions). Every search service starts with one search unit, but each new partition or replica increases the search units of your service. You can check the search unit count in the Azure portal's Essential section of the **Overview** page. If you need concurrent processing, make sure your search units include sufficient replicas. Indexers don't run in the background, so you might experience more query throttling than usual if the service is under pressure.

The following screenshot shows the number of search units, which determines how many indexers can run at once.


Once indexer execution starts, you can't pause or stop it. Indexer execution stops when there are no more documents to load or refresh, or when the [maximum running time limit](search-limits-quotas-capacity#indexer-limits) is reached.

You can run multiple indexers at one time assuming sufficient capacity, but each indexer itself is single-instance. Starting a new instance while the indexer is already in execution produces this error: `"Failed to run indexer "<indexer name>" error: "Another indexer invocation is currently in progress; concurrent invocations are not allowed."`


## Indexer execution environment

An indexer job runs in a managed execution environment. Currently, there are two environments:

A private execution environment runs on search clusters that are specific to your search service.

A multitenant environment has content processors that are managed and secured by Microsoft at no extra cost. This environment is used to offload computationally intensive processing, leaving service-specific resources available for routine operations. Whenever possible, most skillsets execute in the multitenant environment. This is the default.

*Computationally intensive processing*refers to skillsets running on content processors and indexer jobs that process a high volume of documents, or documents of a large size. Non-skillset processing on the multitenant content processors is determined by heuristics and system information and isn't under customer control.

You can prevent usage of the multitenant environment on Standard2 or higher services by pinning an indexer and skillset processing exclusively to your search clusters. [Set the executionEnvironment parameter](search-how-to-create-indexers?tabs=indexer-rest#create-an-indexer) in the indexer definition to always run an indexer in the private execution environment.

[IP firewalls](search-indexer-securing-resources#setting-up-ip-ranges-for-indexer-execution) block the multitenant environment, so if you have a firewall, [create a rule](search-indexer-howto-access-ip-restricted#configure-ip-firewall-rules-to-allow-indexer-connections-from-azure-ai-search) that allows multitenant processor connections.

Indexer limits vary for each environment:

| Workload | Maximum duration | Maximum jobs | Execution environment |
|---|---|---|---|
| Private execution | 24 hours | One indexer job per
1. |

[some query latency](search-performance-analysis#impact-of-indexing-on-queries)if indexing volumes are large.231 Search units can be [flexible combinations](search-capacity-planning#partition-and-replica-combinations) of partitions and replicas, but indexer jobs aren't tied to one or the other. In other words, if you have 12 units, you can have 12 indexer jobs running concurrently in private execution, no matter how the search units are deployed.

2 If more than two hours are needed to process all of the data, [enable change detection](search-howto-create-indexers#change-detection-and-internal-state) and [schedule the indexer](search-howto-schedule-indexers) to run at 5-minute intervals to resume indexing quickly if it stops due to a time out. See [Indexing a large data set](search-howto-large-index) for more strategies.

3 "Indeterminate" means that the limit isn't quantified by the number of jobs. Some workloads, such as skillset processing, can run in parallel, which could result in many jobs even though only one indexer is involved. Although the environment doesn't impose constraints, [indexer limits](search-limits-quotas-capacity#indexer-limits) for your search service still apply.

## Run without reset

A [Run Indexer](/en-us/rest/api/searchservice/indexers/run) operation detects and processes only what it necessary to synchronize the search index with changes in the underlying data source. Incremental indexing starts by locating an internal high-water mark to find the last updated search document, which becomes the starting point for indexer execution over new and updated documents in the data source.

[Change detection](search-howto-create-indexers#change-detection-and-internal-state) is essential for determining what's new or updated in the data source. Indexers use the change detection capabilities of the underlying data source to determine what's new or updated in the data source.

Azure Storage has built-in change detection through its LastModified property.

Other data sources, such as Azure SQL or Azure Cosmos DB, have to be configured for change detection before the indexer can read new and updated rows.


If the underlying content is unchanged, a run operation has no effect. In this case, indexer execution history indicates `0\0`

documents processed.

You need to reset the indexer, as explained in the next section, to reprocess in full.

## Resetting indexers

After the initial run, an indexer keeps track of which search documents are indexed through an internal *high-water mark*. The marker is never exposed, but internally the indexer knows where it last stopped.

If you need to rebuild all or part of an index, use Reset APIs available at decreasing levels in the object hierarchy:

[Reset Indexers](#reset-indexers)clears the high-water mark and performs a full reindex of all documents[Resync Indexers (preview)](#resync-indexers)performs an efficient partial reindex of all documents[Reset Documents (preview)](#reset-docs)reindexes a specific document or list of documents[Reset Skills (preview)](#reset-skills)invokes skill processing for a specific skill

After reset, follow with a Run command to reprocess new and existing documents. Orphaned search documents having no counterpart in the data source can't be removed through reset/run. If you need to delete specific documents, see [Delete documents in a search index](search-how-to-delete-documents) or [Documents - Index](/en-us/rest/api/searchservice/documents) instead.

Note

Tables can't be empty. If you use TRUNCATE TABLE to clear rows, a reset and rerun of the indexer won't remove the corresponding search documents. To remove orphaned search documents, you must [index them with a delete action](search-how-to-delete-documents#delete-a-single-document).

## How to reset and run indexers

Reset clears the high-water mark. All documents in the search index are flagged for full overwrite, without inline updates or merging into existing content. For indexers with a skillset and [enrichment caching](enrichment-cache-how-to-configure), resetting the index also implicitly resets the skillset.

The actual work occurs when you follow a reset with a Run command:

- All new documents found the underlying source are added to the search index.
- All documents that exist in both the data source and search index are overwritten in the search index.
- Any enriched content created from skillsets are rebuilt. The enrichment cache, if one is enabled, is refreshed.

As previously noted, reset is a passive operation: you must follow with a Run request to rebuild the index.

Reset/run operations apply to a search index or a knowledge store, to specific documents or projections, and to cached enrichments if a reset explicitly or implicitly includes skills.

Reset also applies to create and update operations. It won't trigger deletion or clean up of orphaned documents in the search index. For more information about deleting documents, see [Documents - Index](/en-us/rest/api/searchservice/documents/).

Once you reset an indexer, you can't undo the action.

Sign in to the

[Azure portal](https://portal.azure.com)and open the search service page.On the

**Overview**page, select the**Indexers**tab.Select an indexer.

Select the

**Reset**command, and then select**Yes**to confirm the action.Refresh the page to show the status. You can select the item to view its details.

Select

**Run**to start indexer processing, or wait for the next scheduled execution.

## How to reset skills (preview)

The Reset Skills request selectively processes one or more skills on the next indexer run. For indexers that have skillsets, you can reset individual skills to force reprocessing of just that skill and any downstream skills that depend on its output. The [enrichment cache](enrichment-cache-how-to-configure), if you enabled it, is also refreshed.

For indexers that have caching enabled, you can explicitly request processing for skill updates that the indexer cannot detect. For example, if you make external changes, such as revisions to a custom skill, you can use this API to rerun the skill. Outputs, such as a knowledge store or search index, are refreshed using reusable data from the cache and new content per the updated skill.

We recommend the [latest preview API](/en-us/rest/api/searchservice/skillsets/reset-skills?view=rest-searchservice-2025-11-01-preview&preserve-view=true).

```
POST /skillsets/[skillset name]/resetskills?api-version=2025-11-01-preview
{
"skillNames" : [
"#1",
"#5",
"#6"
]
}
```


You can specify individual skills, as indicated in the example above, but if any of those skills require output from unlisted skills (#2 through #4), unlisted skills will run unless the cache can provide the necessary information. In order for this to be true, cached enrichments for skills #2 through #4 must not have dependency on #1 (listed for reset).

If no skills are specified, the entire skillset is executed and if caching is enabled, the cache is also refreshed.

Remember to follow up with [Run Indexer](/en-us/rest/api/searchservice/indexers/run) to invoke actual processing.

## How to reset docs (preview)

The [Indexers - Reset Docs (preview)](/en-us/rest/api/searchservice/indexers/reset-docs?view=rest-searchservice-2025-11-01-preview&preserve-view=true) accepts a list of document keys so that you can refresh specific documents. If specified, the reset parameters become the sole determinant of what gets processed, regardless of other changes in the underlying data. For example, if 20 blobs were added or updated since the last indexer run, but you only reset one document, only that document is processed.

On a per-document basis, all fields in the search document are refreshed with values and metadata from the data source. You can't pick and choose which fields to refresh.

If the data source is Azure Data Lake Storage (ADLS) Gen2, and the blobs are associated with permission metadata, those permissions are also re-ingested in the search index if permissions change in the underlying data. For more information, see [Re-indexing ACL and RBAC scope with ADLS Gen2 indexers](search-indexer-access-control-lists-and-role-based-access#synchronize-permissions-between-indexed-and-source-content).

If the document is enriched through a skillset and has cached data, the skillset is invoked for just the specified documents, and the cache is updated for the reprocessed documents.

When you're testing this API for the first time, the following APIs can help you validate and test the behaviors. We recommend the latest preview API.

Call

[Indexers - Get Status](/en-us/rest/api/searchservice/indexers/get-status?view=rest-searchservice-2025-11-01-preview&preserve-view=true)with a preview API version to check reset status and execution status. You can find information about the reset request at the end of the status response.Call

[Indexers - Reset Docs](/en-us/rest/api/searchservice/indexers/reset-docs?view=rest-searchservice-2025-11-01-preview&preserve-view=true)with a preview API version to specify which documents to process.`POST https://[service name].search.windows.net/indexers/[indexer name]/resetdocs?api-version=2025-11-01-preview { "documentKeys" : [ "1001", "4452" ] }`

The API accepts two types of document identifiers as input: Document keys that uniquely identify documents in a search index, and datasource document identifiers that uniquely identify documents in a data source. The body should contain either a list of document keys

*or*a list of data source document identifiers that the indexer looks for in the data source. Invoking the API adds the document keys or data source document identifiers to be reset to the indexer metadata. On the next scheduled or on-demand run of the indexer, the indexer processes only the reset documents.If you use document keys to reset documents and your document keys are referenced in an indexer field mapping, the indexer uses field mapping to locate the appropriate field in the underlying data source.

The document keys provided in the request are values from the search index, which can be different from the corresponding fields in the data source. If you're unsure of the key value,

[send a query](search-query-create)to return the value. You can use`select`

to return just the document key field.For blobs that are parsed into multiple search documents (where parsingMode is set to

[jsonLines or jsonArrays](search-how-to-index-azure-blob-json), or[delimitedText](search-how-to-index-azure-blob-csv)), the document key is generated by the indexer and might be unknown to you. In this scenario, a query for the document key to return the correct value.If you want the indexer to stop trying to process reset documents, you can set "documentKeys" or "datasourceDocumentIds" to an empty list "[]". This results in the indexer resuming regular indexing based on the high water mark. Invalid document keys or document keys that don't exist are ignored.


Call

[Run Indexer](/en-us/rest/api/searchservice/indexers/run)(any API version) to process the documents you specified. Only those specific documents are indexed.Call

[Run Indexer](/en-us/rest/api/searchservice/indexers/run)a second time to process from the last high-water mark.Call

[Search Documents](/en-us/rest/api/searchservice/documents/search-post)to check for updated values, and also to return document keys if you're unsure of the value. Use`"select": "<field names>"`

if you want to limit which fields appear in the response.

### Overwriting the document key list

Calling Reset Documents API multiple times with different keys appends the new keys to the list of document keys reset. Calling the API with the ** overwrite** parameter set to true will overwrite the current list with the new one:

```
POST https://[service name].search.windows.net/indexers/[indexer name]/resetdocs?api-version=2025-11-01-preview
{
"documentKeys" : [
"200",
"630"
],
"overwrite": true
}
```


## How to resync indexers (preview)

[Resync Indexers](/en-us/rest/api/searchservice/indexers/resync?view=rest-searchservice-2025-11-01-preview&preserve-view=true) is a preview REST API that performs a partial reindex of all documents.
An indexer is considered synchronized with its data source when specific fields of all documents in the target index are consistent with the data in the data source. Typically, an indexer achieves synchronization after a successful initial run. If a document is deleted from the data source, the indexer remains synchronized according to this definition. However, during the next indexer run, the corresponding document in the target index will be removed if delete tracking is enabled.

If a document is modified in the data source, the indexer becomes unsynchronized. Generally, change tracking mechanisms will resynchronize the indexer during the next run. For example, in Azure Storage, modifying a blob updates its last modified time, allowing it to be re-indexed in the subsequent indexer run because the updated time surpasses the high-water mark set by the previous run.

In contrast, for certain data sources like ADLS Gen2, altering the Access Control Lists (ACLs) of a blob does not change its last modified time, rendering change tracking ineffective if ACLs are to be ingested. Consequently, the modified blob will not be re-indexed in the subsequent run, as only documents modified after the last high-water mark are processed.

While using either "reset" or "reset docs" can address this issue, "reset" can be time-consuming and inefficient for large datasets, and "reset docs" requires identifying the document key of the blob intended for update.

Resync Indexers offers an efficient and convenient alternative. Users simply place the indexer in resync mode and specify the content to resynchronize by calling the resync indexers API. In the next run, the indexer will inspect only relevant portion of data in the source and avoid any unnecessary processing that is unrelated to the specified data. It will also query the existing documents in the target index and only update the documents that show discrepancies between the data source and the target index. After the resync run, the indexer will be synchronized and revert to regular indexer run mode for subsequent runs.

### How to resync and run indexers

Call

[Indexers - Resync](/en-us/rest/api/searchservice/indexers/resync?view=rest-searchservice-2025-11-01-preview&preserve-view=true)with a preview API version to specify what content to re-synchronize.`POST https://[service name].search.windows.net/indexers/[indexer name]/resync?api-version=2025-11-01-preview { "options" : [ "permissions" ] }`

- The
`options`

field is required. Currently the only supported option is`permissions`

. That is, only permission filter fields in the target index will be updated.

- The
Call

[Run Indexer](/en-us/rest/api/searchservice/indexers/run)(any API version) to re-synchronize the indexer.Call

[Run Indexer](/en-us/rest/api/searchservice/indexers/run)a second time to process from the last high-water mark.

## Check reset status "currentState"

To check reset status and to see which document keys are queued up for processing, following these steps.

Call

[Get Indexer Status](/en-us/rest/api/searchservice/indexers/get-status?view=rest-searchservice-2025-11-01-preview&preserve-view=true)with a preview API.The preview API will return the

section, found at the end of the response.`currentState`

`"currentState": { "mode": "indexingResetDocs", "allDocsInitialTrackingState": "{\"LastFullEnumerationStartTime\":\"2021-02-06T19:02:07.0323764+00:00\",\"LastAttemptedEnumerationStartTime\":\"2021-02-06T19:02:07.0323764+00:00\",\"NameHighWaterMark\":null}", "allDocsFinalTrackingState": "{\"LastFullEnumerationStartTime\":\"2021-02-06T19:02:07.0323764+00:00\",\"LastAttemptedEnumerationStartTime\":\"2021-02-06T19:02:07.0323764+00:00\",\"NameHighWaterMark\":null}", "resetDocsInitialTrackingState": null, "resetDocsFinalTrackingState": null, "resyncInitialTrackingState": null, "resyncFinalTrackingState": null, "resetDocumentKeys": [ "200", "630" ] }`

Check the "mode":

For Reset Skills, "mode" should be set to

(because potentially all documents are affected, in terms of the fields that are populated through AI enrichment).`indexingAllDocs`

For Resync Indexers, "mode" should be set to

. The indexer checks all documents and focuses on interested data in data source and interested fields in the target index.`indexingResync`

For Reset Documents, "mode" should be set to

. The indexer retains this status until all the document keys provided in the reset documents call are processed, during which time no other indexer jobs will execute while the operation is progressing. Finding all of the documents in the document keys list requires cracking each document to locate and match on the key, and this can take a while if the data set is large. If a blob container contains hundreds of blobs, and the docs you want to reset are at the end, the indexer won't find the matching blobs until all of the others have been checked first.`indexingResetDocs`

After the documents are reprocessed, run Get Indexer Status again. The indexer returns to the

mode and will process any new or updated documents on the next run.`indexingAllDocs`


## Check indexer runtime quota for S3 HD search services

Applies to search services at the Standard 3 High Density (S3 HD) pricing tier.

To help you monitor indexer running times relative to the 24-hour window, [Get Service Statistics](/en-us/rest/api/searchservice/get-service-statistics/get-service-statistics#servicestatistics?view=rest-searchservice-2025-11-01-preview&preserve-view=true) and [Get Indexer Status](/en-us/rest/api/searchservice/indexers/get-status?view=rest-searchservice-2025-11-01-preview&preserve-view=true) now return more information in the response.

### Track cumulative runtime quota

Track a search service's cumulative indexer runtime usage and determine how much runtime quota is left within the current 24-hour window period.

Send a GET request to the search service resource provider. For help with setting up a REST client and getting an access token, see [Connect to a search service](/en-us/azure/search/search-get-started-rbac?pivots=rest).

```
GET {{search-endpoint}}/servicestats?api-version=2025-11-01-preview
Content-Type: application/json
Authorization: Bearer {{accessToken}}
```


Responses include `indexersRuntime`

properties, showing start and end times, seconds used, seconds remaining, and cumulative runtime within the last 24 hours.

### Track indexer runtime quota

Return the same information for a single indexer.

```
GET {{search-endpoint}}/indexers/hotels-sample-indexer/search.status?api-version=2025-11-01-preview
Content-Type: application/json
Authorization: Bearer {{accessToken}}
```


Responses include a `runtime`

properties, showing start and end times, seconds used, and seconds remaining.

## Next steps

Reset APIs are used to inform the scope of the next indexer run. For actual processing, you'll need to invoke an on-demand indexer run or allow a scheduled job to complete the work. After the run is finished, the indexer returns to normal processing, whether that is on a schedule or on-demand processing.

After you reset and rerun indexer jobs, you can monitor status from the search service, or obtain detailed information through resource logging.