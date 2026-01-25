---
merged_at: 2026-01-25T03:18:13.750462
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: search-monitor-enable-logging.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/search-monitor-enable-logging -->

# Configure diagnostic logging for Azure AI Search

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Diagnostic logs provide insight into operations that occur in your Azure AI Search resource. In contrast to Activity Logs that track operations performed on Azure resources at the subscription level, known as the [control plane](/en-us/azure/azure-resource-manager/management/control-plane-and-data-plane), diagnostic logging monitors operations on the search service itself. Diagnostic logging is essential for effective oversight of service operations like indexing and queries.

This article explains how to enable diagnostic logging and find information about system and user operations on an Azure AI Search resource.

Note

Azure AI Search doesn't log the identity of the person or app accessing content or operations on the search service. If you require this level of monitoring, you need to implement it in your client application.

## Prerequisites

- An
[Azure Log Analytics workspace](/en-us/azure/azure-monitor/logs/quick-create-workspace)in the same subscription.

## Enable diagnostic logging

Sign in to the

[Azure portal](https://portal.azure.com)and[find your search service](https://portal.azure.com/#blade/HubsExtension/BrowseResourceBlade/resourceType/Microsoft.Search%2FsearchServices).Under

**Monitoring**>**Diagnostic settings**, select**Add diagnostic setting**.Provide a descriptive name that identifies the service and level of logging, such as "my-search-service-all-logs" or "my-search-service-audit-logs".

Under

**Logs**, choose a category:**Audit logs**capture user or app interactions with data or the settings of the service, but don't include user or groups identities.**Operation logs**capture information about operations on a search service.**allLogs**collect everything.

Verbose logging can be expensive to store and complex to manage and store. You might want to start with

**allLogs**and then switch to more scoped logging if it meets your information requirements. For more information about these categories, see[Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings).For a destination, we recommend

**Send to Log Analytics workspace**so that you can run Kusto queries against the data. Provide an existing Log Analytics workspace to store your logs.Save the settings.


Repeat these steps if you require a more [comprehensive data collection strategy](/en-us/azure/azure-monitor/logs/workspace-design).

Each diagnostic setting you create requires separate storage. If you use the Azure portal to review logs, the first diagnostic setting is used by default. You can navigate to specific workspaces for visualization support.

Note

If you're using [key-based authentication](search-security-api-keys), Azure AI Search can't monitor individual user access to content on the search service. If you require this level of monitoring, you need to implement it in your client application.

## View logs in Log Analytics

Follow these instructions to explore log analytics data for your search service.

Under

**Monitoring**, select**Logs**. Query hub opens by default. You can try the available queries, or close the hub and open a query window in KQL mode to run queries written in the[Kusto Query Language (KQL)](/en-us/kusto/query).In a query window, you can run Kusto queries against your logs.


## Sample Kusto queries

Here are a few basic Kusto queries you can use to explore your log data.

Run this query for all diagnostic logs from Azure AI Search services over the specified time period:

```
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.SEARCH"
```


Run this query to see the 10 most recent logs:

```
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.SEARCH"
| take 10
```


Run this query to group operations by **Resource**:

```
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.SEARCH" |
summarize count() by Resource
```


Run this query to find the average time it takes to perform an operation:

```
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.SEARCH"
| summarize avg(DurationMs)
by OperationName
```


Run this query to view the volume of operations over time split by OperationName with counts binned for every 10 seconds.

```
AzureDiagnostics
| where ResourceProvider == "MICROSOFT.SEARCH"
| summarize count()
by bin(TimeGenerated, 10s), OperationName
| render areachart kind=unstacked
```


---

<!-- DOCUMENTO FUSIONADO: knowledge-store-connect-power-bi.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/search/knowledge-store-connect-power-bi -->

# Connect a knowledge store with Power BI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

*Knowledge stores* are secondary storage that exists in Azure Storage and contain the outputs of Azure AI Search skillsets. They're separate from knowledge sources and knowledge bases, which are used in [agentic retrieval](agentic-retrieval-overview) workflows.

In this article, learn how to connect to and query a knowledge store using Power Query in the Power BI Desktop app. You can get started faster with templates, or build a custom dashboard from scratch.

A knowledge store that's composed of tables in Azure Storage work best in Power BI. If the tables contain projections from the same skillset and projection group, you can easily "join" them to build table visualizations that include fields from related tables.

Follow the steps in this article using sample data and a knowledge store as [created in this portal quickstart](knowledge-store-create-portal) or through [REST APIs](knowledge-store-create-rest).

## Connect to Azure Storage

Start

[Power BI Desktop](https://powerbi.microsoft.com/downloads/)and select**Get data**.In

**Get Data**, select**Azure**, and then select**Azure Table Storage**.Select

**Connect**.For

**Account Name or URL**, enter in your Azure Storage account name (the full URL is created for you).If prompted, enter the storage account key.


## Set up tables

Select the checkbox next to all of the tables that were created from the same skillset, and then select

**Load**.On the top ribbon, select

**Transform Data**to open the**Power Query Editor**.Open

*hotelReviewsDocument*and remove its*PartitionKey*,*RowKey*, and*Timestamp*columns. Those columns are used for table relationships in Azure Table Storage. Power BI doesn't need them. You should be left with one column named "Content" showing*Record*in each one.Select the icon with opposing arrows at the upper right side of the table to expand

*Content*. When the list of columns appears, select all columns. Clear columns starting with 'metadata'. Select**OK**to include the selected columns.Change the data type for the following columns by clicking the ABC-123 icon at the top left of the column.

- For
*content.latitude*and*Content.longitude*, select**Decimal Number**. - For
*Content.reviews_date*and*Content.reviews_dateAdded*, select**Date/Time**.

- For
Open

*hotelReviewsSsPages*and repeat column deletion steps, expanding*Content*to select columns from the records. There are no data type modifications for this table.Open

*hotelReviewsSsKeyPhrases*and repeat column deletion steps, expanding*Content*to select columns from the records. There are no data type modifications for this table.On the command bar, select

**Close and Apply**.

## Check table relationships

Select on the Model tile on the left pane and validate that Power BI shows relationships between all three tables.

Double-click each relationship and make sure that the

**Cross-filter direction**is set to**Both**. This enables your visuals to refresh when a filter is applied.

## Build a report

Select on the Report tile on the left pane to explore data through visualizations. For text fields, tables and cards are useful visualizations.

Choose fields from each of the three tables to fill in the table or card.


## Sample Power BI template - Azure portal only

When creating a [knowledge store using the Azure portal](knowledge-store-create-portal), you have the option of downloading a [Power BI template](https://github.com/Azure-Samples/cognitive-search-templates) on the second page of the **Import data** wizard. This template gives you several visualizations, such as WordCloud and Network Navigator, for text-based content.

Select **Get Power BI Template** on the **Add cognitive skills** page to retrieve and download the template from its public GitHub location. The wizard modifies the template to accommodate the shape of your data, as captured in the knowledge store projections specified in the wizard. For this reason, the template you download varies each time you run the wizard, assuming different data inputs and skill selections.

Note

The template is downloaded while the wizard is in mid-flight. You'll have to wait until the knowledge store is actually created in Azure Table Storage before you can use it.

## Video introduction

For a demonstration of using Power BI with a knowledge store, watch the following video.
