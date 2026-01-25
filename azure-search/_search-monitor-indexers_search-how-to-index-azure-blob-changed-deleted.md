---
merged_at: 2026-01-25T02:11:58.412348
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-monitor-indexers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-monitor-indexers -->

# Monitor indexer status and results in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can monitor indexer processing in the Azure portal, or programmatically through REST calls or an Azure SDK. In addition to status about the indexer itself, you can review start and end times, and detailed errors and warnings from a particular run.

## Monitor using Azure portal

You can see the current status of all of your indexers in your search service portal page. Azure portal pages refresh every few minutes, so you don't see evidence of a new indexer run right away. Select **Refresh** at the top of the page to immediately retrieve the most recent view.

| Status | Description |
|---|---|
In Progress |
Indicates active execution. the Azure portal reports on partial information. As indexing progresses, you can watch the Docs Succeeded value grow in response. Indexers that process large volumes of data can take a long time to run. For example, indexers that handle millions of source documents can run for 24 hours, and then restart almost immediately to pick up where it left off. As such, the status for high-volume indexers might always say In Progress in the Azure portal. Even when an indexer is running, details are available about ongoing progress and previous runs. |
Success |
Indicates the run was successful. An indexer run can be successful even if individual documents have errors, if the number of errors is less than the indexer's Max failed items setting. |
Failed |
The number of errors exceeded Max failed items and indexing stops. |
Reset |
The indexer's internal change tracking state was reset. The indexer runs in full, refreshing all documents, and not just those with newer timestamps. |

You can select on an indexer in the list to see more details about the indexer's current and recent runs.

The **Indexer summary** chart displays a graph of the number of documents processed in its most recent runs.

The **Execution details** list shows up to 50 of the most recent execution results. Select on an execution result in the list to see specifics about that run. This includes its start and end times, and any errors and warnings that occurred.

If there were document-specific problems during the run, they are listed in the Errors and Warnings fields.

Warnings are common with some types of indexers, and don't always indicate a problem. For example indexers that use Foundry Tools can report warnings when image or PDF files don't contain any text to process.

For more information about investigating indexer errors and warnings, see [Indexer troubleshooting guidance](search-indexer-troubleshooting).

## Monitor with Azure Monitoring Metrics

Azure AI Search is a monitored resource in Azure Monitor, which means that you can use [Metrics Explorer](/en-us/azure/azure-monitor/essentials/data-platform-metrics#metrics-explorer) to see basic metrics about the number of indexer-processed documents and skill invocations. These metrics can be used to monitor indexer progress and [set up alerts](/en-us/azure/azure-monitor/alerts/alerts-metric-overview).

Metric views can be filtered or split up by a set of predefined dimensions. To learn about the dimensions associated with the metrics *Document processed count* and *Skill execution invocation count*, see [Metric dimensions](monitor-azure-cognitive-search-data-reference#metric-dimensions).

The following screenshot shows the number of documents processed by indexers within a service over an hour, split up by indexer name.

You can also configure the graph to see the number of skill invocations over the same hour interval.

## Monitor using Get Indexer Status (REST API)

You can retrieve the status and execution history of an indexer using the [Get Indexer Status command](/en-us/rest/api/searchservice/indexers/get-status):

```
GET https://[service name].search.windows.net/indexers/[indexer name]/status?api-version=2025-09-01
api-key: [Search service admin key]
```


The response contains overall indexer status, the last (or in-progress) indexer invocation, and the history of recent indexer invocations.

```
{
"status":"running",
"lastResult": {
"status":"success",
"errorMessage":null,
"startTime":"2018-11-26T03:37:18.853Z",
"endTime":"2018-11-26T03:37:19.012Z",
"errors":[],
"itemsProcessed":11,
"itemsFailed":0,
"initialTrackingState":null,
"finalTrackingState":null
},
"executionHistory":[ {
"status":"success",
"errorMessage":null,
"startTime":"2018-11-26T03:37:18.853Z",
"endTime":"2018-11-26T03:37:19.012Z",
"errors":[],
"itemsProcessed":11,
"itemsFailed":0,
"initialTrackingState":null,
"finalTrackingState":null
}]
}
```


Execution history contains up to the 50 most recent runs, which are sorted in reverse chronological order (most recent first).

Note there are two different status values. The top level status is for the indexer itself. An indexer status of **running** means the indexer is set up correctly and available to run, but not that it's currently running.

Each run of the indexer also has its own status that indicates whether that specific execution is ongoing (**running**), or already completed with a **success**, **transientFailure**, or **persistentFailure** status.

When an indexer is reset to refresh its change tracking state, a separate execution history entry is added with a **Reset** status.

For more information about status codes and indexer monitoring data, see [Get Indexer Status](/en-us/rest/api/searchservice/indexers/get-status).

## Monitor using .NET

The following C# example writes information about an indexer's status and the results of its most recent (or ongoing) run to the console.

```
static void CheckIndexerStatus(SearchIndexerClient indexerClient, SearchIndexer indexer)
{
try
{
string indexerName = "hotels-sql-idxr";
SearchIndexerStatus execInfo = indexerClient.GetIndexerStatus(indexerName);
Console.WriteLine("Indexer has run {0} times.", execInfo.ExecutionHistory.Count);
Console.WriteLine("Indexer Status: " + execInfo.Status.ToString());
IndexerExecutionResult result = execInfo.LastResult;
Console.WriteLine("Latest run");
Console.WriteLine("Run Status: {0}", result.Status.ToString());
Console.WriteLine("Total Documents: {0}, Failed: {1}", result.ItemCount, result.FailedItemCount);
TimeSpan elapsed = result.EndTime.Value - result.StartTime.Value;
Console.WriteLine("StartTime: {0:T}, EndTime: {1:T}, Elapsed: {2:t}", result.StartTime.Value, result.EndTime.Value, elapsed);
string errorMsg = (result.ErrorMessage == null) ? "none" : result.ErrorMessage;
Console.WriteLine("ErrorMessage: {0}", errorMsg);
Console.WriteLine(" Document Errors: {0}, Warnings: {1}\n", result.Errors.Count, result.Warnings.Count);
}
catch (Exception e)
{
// Handle exception
}
}
```


The output in the console looks something like this:

```
Indexer has run 18 times.
Indexer Status: Running
Latest run
Run Status: Success
Total Documents: 7, Failed: 0
StartTime: 11:29:31 PM, EndTime: 11:29:31 PM, Elapsed: 00:00:00.2560000
ErrorMessage: none
Document Errors: 0, Warnings: 0
```


Note there are two different status values. The top-level status is the status of the indexer itself. An indexer status of **Running** means that the indexer is set up correctly and available for execution, but not that it's currently executing.

Each run of the indexer also has its own status for whether that specific execution is ongoing (**Running**), or was already completed with a **Success** or **TransientError** status.

When an indexer is reset to refresh its change tracking state, a separate history entry is added with a **Reset** status.

## Next steps

For more information about status codes and indexer monitoring information, see the following API reference:


---

<!-- DOCUMENTO FUSIONADO: search-how-to-index-azure-blob-changed-deleted.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-how-to-index-azure-blob-changed-deleted -->

# Change and delete detection using indexers for Azure Storage in Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After an initial search index is created, you might want subsequent indexer jobs to only pick up new and changed documents. For indexed content that originates from Azure Storage, change detection occurs automatically because indexers keep track of the last update using the built-in timestamps on objects and files in Azure Storage.

Although change detection is a given, deletion detection isn't. An indexer doesn't track object deletion in data sources. To avoid having orphan search documents, you can implement a "soft delete" strategy that results in deleting search documents first, with physical deletion in Azure Storage following as a second step.

There are two ways to implement a soft delete strategy:

[Native blob soft delete](#native-blob-soft-delete), applies to Blob Storage only[Soft delete using custom metadata](#soft-delete-using-custom-metadata)

The deletion detection strategy must be applied from the very first indexer run. If you didn't establish the deletion policy prior to the initial run, any documents that were deleted before the policy was implemented will remain in your index, even if you add the policy to the indexer later and reset it. If this has occurred, it's suggested that you create a new index using a new indexer, ensuring the deletion policy is in place from the beginning.

## Prerequisites

Use an Azure Storage indexer for

[Blob Storage](search-how-to-index-azure-blob-storage),[Table Storage](search-how-to-index-azure-tables),[File Storage](search-how-to-index-azure-tables), or[Data Lake Storage Gen2](search-how-to-index-azure-data-lake-storage)Use consistent document keys and file structure. Changing document keys or directory names and paths (applies to ADLS Gen2) breaks the internal tracking information used by indexers to know which content was indexed, and when it was last indexed.


Note

ADLS Gen2 allows directories to be renamed. When a directory is renamed, the timestamps for the blobs in that directory don't get updated. As a result, the indexer won't reindex those blobs. If you need the blobs in a directory to be reindexed after a directory rename because they now have new URLs, you need to update the `LastModified`

timestamp for all the blobs in the directory so that the indexer knows to reindex them during a future run. The virtual directories in Azure Blob Storage can't be changed, so they don't have this issue.

## Native blob soft delete

For this deletion detection approach, Azure AI Search depends on the [native blob soft delete](/en-us/azure/storage/blobs/soft-delete-blob-overview) feature in Azure Blob Storage to determine whether blobs have transitioned to a soft deleted state. When blobs are detected in this state, a search indexer uses this information to remove the corresponding document from the index.

### Requirements for native soft delete

Blobs must be in an Azure Blob Storage container, including ADLS Gen2 Blob container. The Azure AI Search native blob soft delete policy isn't supported for Azure Files.

Document keys for the documents in your index must be mapped to either be a blob property or blob metadata, such as "metadata_storage_path".

You can use the

[REST API](/en-us/rest/api/searchservice/data-sources/create), or the indexer Data Source configuration in the Azure portal, to configure support for soft delete.[Blob versioning](/en-us/azure/storage/blobs/versioning-overview)must not be enabled in the storage account. Otherwise, native soft delete isn't supported by design.

### Configure native soft delete

In Blob storage, when enabling soft delete per the requirements, set the retention policy to a value that's much higher than your indexer interval schedule. If there's an issue running the indexer, or if you have a large number of documents to index, there's plenty of time for the indexer to eventually process the soft deleted blobs. Azure AI Search indexers will only delete a document from the index if it processes the blob while it's in a soft deleted state.

In Azure AI Search, set a native blob soft deletion detection policy on the data source. You can do this either from the Azure portal or by using the [REST API](/en-us/rest/api/searchservice/data-sources/create). The following instructions explain how to set the delete detection policy in Azure portal or through REST APIs.

Sign in to the

[Azure portal](https://portal.azure.com).On the Azure AI Search service Overview page, go to

**New Data Source**, a visual editor for specifying a data source definition.The following screenshot shows where you can find this feature in the Azure portal.

On the

**New Data Source**form, fill out the required fields, select the**Track deletions**checkbox and choose**Native blob soft delete**. Then hit**Save**to enable the feature on Data Source creation.

### Reindex undeleted blobs using native soft delete policies

If you restore a soft deleted blob in Blob storage, the indexer won't always reindex it. This is because the indexer uses the blob's `LastModified`

timestamp to determine whether indexing is needed. When a soft deleted blob is undeleted, its `LastModified`

timestamp doesn't get updated, so if the indexer has already processed blobs with more recent `LastModified`

timestamps, it won't reindex the undeleted blob.

To make sure that an undeleted blob is reindexed, you'll need to update the blob's `LastModified`

timestamp. One way to do this is by resaving the metadata of that blob. You don't need to change the metadata, but resaving the metadata will update the blob's `LastModified`

timestamp so that the indexer knows to pick it up.

## Soft delete strategy using custom metadata

This method uses custom metadata to indicate whether a search document should be removed from the index. It requires two separate actions: deleting the search document from the index, followed by file deletion in Azure Storage.

This feature is generally available.

There are steps to follow in both Azure Storage and Azure AI Search, but there are no other feature dependencies.

In Azure Storage, add a custom metadata key-value pair to the file to indicate the file is flagged for deletion. For example, you could name the property "IsDeleted", set to false. When you want to delete the file, change it to true.

In Azure AI Search, edit the data source definition to include a "dataDeletionDetectionPolicy" property. For example, the following policy considers a file to be deleted if it has a metadata property

`IsDeleted`

with the value`true`

:`PUT https://[service name].search.windows.net/datasources/file-datasource?api-version=2025-09-01 { "name" : "file-datasource", "type" : "azurefile", "credentials" : { "connectionString" : "<your storage connection string>" }, "container" : { "name" : "my-share", "query" : null }, "dataDeletionDetectionPolicy" : { "@odata.type" :"#Microsoft.Azure.Search.SoftDeleteColumnDeletionDetectionPolicy", "softDeleteColumnName" : "IsDeleted", "softDeleteMarkerValue" : "true" } }`

Run the indexer. Once the indexer has processed the file and deleted the document from the search index, you can then delete the physical file in Azure Storage.


## Reindex undeleted blobs and files

You can reverse a soft-delete if the original source file still physically exists in Azure Storage.

Change the

`"softDeleteMarkerValue" : "false"`

on the blob or file in Azure Storage.Check the blob or file's

`LastModified`

timestamp to make it's newer than the last indexer run. You can force an update to the current date and time by resaving the existing metadata.Run the indexer.
