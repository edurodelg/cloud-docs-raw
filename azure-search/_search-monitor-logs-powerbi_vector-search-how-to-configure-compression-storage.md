---
merged_at: 2026-01-25T02:11:58.356387
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-monitor-logs-powerbi.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-monitor-logs-powerbi -->

# Visualize Azure AI Search Logs and Metrics with Power BI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure AI Search can send operation logs and service metrics to an Azure Storage account, which can then be visualized in Power BI. This article explains the steps and how to use a Power BI template app to visualize the data. The template covers information about queries, indexing, operations, and service metrics.

Note

The Power BI template currently uses a former product name, Azure Cognitive Search. The product name will be updated on the next template refresh.

## Set up logging and install the template

Enable metric and resource logging for your search service:

- Create or identify an existing
[Azure Storage account](/en-us/azure/storage/common/storage-account-create)where you can archive the logs. - Navigate to your search service in the Azure portal.
- Under Monitoring, select
**Diagnostic settings**. - Select
**Add diagnostic setting**. - Check
**Archive to a storage account**, provide your storage account information, and check**OperationLogs**and**AllMetrics**. - Select
**Save**.

- Create or identify an existing
Once logging is enabled, logs and metrics are generated as you use the search service. It can take up to an hour before logged events show up in Azure Storage. Look for a

**insights-logs-operationlogs**container for operations and a**insights-metrics-pt1m**container for metrics. Check your storage account for these containers to make sure you have data to visualize.Find the Power BI app template in the

[Power BI Apps marketplace](https://appsource.microsoft.com/en-us/product/power-bi/azurecognitivesearch.azurecognitivesearchlogsandmetrics?tab=Overview)and install it into a new workspace or an existing workspace. The template is called**Azure Cognitive Search: Analyze Logs and Metrics**.After installing the template, select it from your list of apps in Power BI.

Select

**Connect your data**.Provide the name of the storage account that contains your logs and metrics. By default, the app looks at the last 10 days of data, but this value can be changed with the

**Days**parameter.Select

**Key**as the authentication method and provide your storage account key. Select**None**or**Private**as the privacy level. Select**Sign In**to begin the loading process.Wait for the data to refresh. This might take some time depending on how much data you have. You can see if the data is still being refreshed based on the below indicator.

Select

**Azure Cognitive Search Report**to view the report.Refresh the page after opening the report so that it opens with your data.


## Modify app parameters

If you would like to visualize data from a different storage account or change the number of days of data to query, follow the below steps to change the **Days** and **StorageAccount** parameters.

Navigate to your Power BI apps, find your search app, and select the

**Edit**action to continue to the workspace.Select

**Settings**from the Dataset options.While in the Datasets tab, change the parameter values and select

**Apply**. If there's an issue with the connection, update the data source credentials on the same page.Navigate back to the workspace and select

**Refresh now**from the Dataset options.Open the report to view the updated data. You might also need to refresh the report to view the latest data.


## Troubleshooting report issues

If you can't see your data, try these troubleshooting steps:

Open the report and refresh the page to make sure you're viewing the latest data. There's an option in the report to refresh the data. Select this to get the latest data.

Ensure the storage account name and access key you provided are correct. The storage account name should correspond to the account configured with your search service logs.

Confirm that your storage account contains the containers

**insights-logs-operationlogs**and**insights-metrics-pt1m**and each container has data. The logs and metrics will be within a couple layers of folders.Check to see if the dataset is still refreshing. The refresh status indicator is shown in step 8 above. If it's still refreshing, wait until the refresh is complete to open and refresh the report.


---

<!-- DOCUMENTO FUSIONADO: vector-search-how-to-configure-compression-storage.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/vector-search-how-to-configure-compression-storage -->

# Choose an approach for optimizing vector storage and processing

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Embeddings, or the numerical representation of heterogeneous content, are the basis of vector search workloads. However, the sizes of embeddings make them hard to scale and expensive to process. Significant research and productization have produced multiple solutions for improving scale and reducing processing times. Azure AI Search taps into a number of these capabilities for faster and cheaper vector workloads.

This article covers all of the optimization techniques in Azure AI Search that can help you reduce vector size and query processing times.

You specify vector optimization settings in vector field definitions in a search index. Most of the features described in this article are generally available in the [latest stable REST API version](/en-us/rest/api/searchservice/operation-groups?view=rest-searchservice-2025-09-01&preserve-view=true) and Azure SDK packages targeting that version.

## Evaluate the options

Review the approaches in Azure AI Search for reducing the amount of storage used by vector fields. These approaches aren't mutually exclusive, so you can combine them for [maximum reduction in vector size](#example-vector-size-by-vector-compression-technique).

We recommend built-in quantization because it compresses vector size in memory *and* on disk with minimal effort. This approach tends to provide the most benefit in most scenarios. In contrast, narrow types (except for float16) require special effort to create them, and `stored`

saves on disk storage, which isn't as expensive as memory.

| Approach | Why use this approach |
|---|---|
|

[Truncate dimensions for MRL-capable text-embedding-3 models](vector-search-how-to-truncate-dimensions)[Matryoshka Representation Learning](https://arxiv.org/abs/2205.13147)(MRL) technique that produces multiple vector representations at different levels of compression. This approach produces faster searches and reduced storage costs with minimal loss of semantic information. In Azure AI Search, MRL support supplements scalar and binary quantization. When you use either quantization method, you can also specify a`truncateDimension`

property on your vector fields to reduce the dimensionality of text embeddings.[Assign smaller primitive data types to vector fields](vector-search-how-to-assign-narrow-data-types)[Index binary vectors](vector-search-how-to-index-binary-data).[Eliminate optional storage of retrievable vectors](vector-search-how-to-storage-options)Define all of these options on an empty index. To implement any of them, use the Azure portal, REST APIs, or an Azure SDK package targeting that API version.

After you define the index, you can load and index documents as a separate step.

## Example: Vector size by vector compression technique

[Vector quantization and storage options using Python](https://github.com/Azure/azure-search-vector-samples/blob/main/demo-python/code/vector-quantization-and-storage/README.md) is a Python code sample that creates multiple search indexes that vary by their use of vector storage quantization, [narrow data types](vector-search-how-to-assign-narrow-data-types), and [storage properties](vector-search-how-to-storage-options).

This code creates and compares storage and vector index size for each vector storage optimization option. From these results, you can see that [quantization](vector-search-how-to-quantization) reduces vector size the most, but the greatest storage savings are achieved if you use multiple options.

| Index name | Storage size | Vector size |
|---|---|---|
| compressiontest-baseline | 21.3613 MB | 4.8277 MB |
| compressiontest-scalar-compression | 17.7604 MB | 1.2242 MB |
| compressiontest-narrow | 16.5567 MB | 2.4254 MB |
| compressiontest-no-stored | 10.9224 MB | 4.8277 MB |
| compressiontest-all-options | 4.9192 MB | 1.2242 MB |

The Search Service REST APIs report storage and vector size at the index level, so you must compare indexes, not fields. Use [Indexes - Get Statistics](/en-us/rest/api/searchservice/indexes/get-statistics) (REST API) or an equivalent API in the Azure SDKs to get vector size.
