---
merged_at: 2026-02-01T08:17:25.361487
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/monitor-functions -->

# Monitor Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes:

- The types of monitoring data you can collect for this service.
- Ways to analyze that data.

Note

If you're already familiar with this service and/or Azure Monitor and just want to know how to analyze monitoring data, see the [Analyze](#analyze-monitoring-data) section near the end of this article.

When you have critical applications and business processes that rely on Azure resources, you need to monitor and get alerts for your system. The Azure Monitor service collects and aggregates metrics and logs from every component of your system. Azure Monitor provides you with a view of availability, performance, and resilience, and notifies you of issues. You can use the Azure portal, PowerShell, Azure CLI, REST API, or client libraries to set up and view monitoring data.

- For more information on Azure Monitor, see the
[Azure Monitor overview](/en-us/azure/azure-monitor/overview). - For more information on how to monitor Azure resources in general, see
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource).

## Insights

Some services in Azure have a built-in monitoring dashboard in the Azure portal that provides a starting point for monitoring your service. These dashboards are called *insights*, and you can find them in the **Insights Hub** of Azure Monitor in the Azure portal.

### Application Insights

Azure Functions has built-in integration with Application Insights to monitor function executions. For detailed information about how to integrate, configure, and use Application Insights to monitor Azure Functions, see the following articles:

[Monitor executions in Azure Functions](functions-monitoring)[Configure monitoring for Azure Functions](configure-monitoring)[Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data)[Monitor Azure Functions with Application Insights](/en-us/azure/azure-monitor/app/monitor-functions)

## Resource types

Azure uses the concept of resource types and IDs to identify everything in a subscription. Resource types are also part of the resource IDs for every resource running in Azure. For example, one resource type for a virtual machine is `Microsoft.Compute/virtualMachines`

. For a list of services and their associated resource types, see [Resource providers](/en-us/azure/azure-resource-manager/management/azure-services-resource-providers).

Azure Monitor similarly organizes core monitoring data into metrics and logs based on resource types, also called *namespaces*. Different metrics and logs are available for different resource types. Your service might be associated with more than one resource type.

For more information about the resource types for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference).

## Data storage

For Azure Monitor:

- Metrics data is stored in the Azure Monitor metrics database.
- Log data is stored in the Azure Monitor logs store. Log Analytics is a tool in the Azure portal that can query this store.
- The Azure activity log is a separate store with its own interface in the Azure portal.

You can optionally route metric and activity log data to the Azure Monitor logs store. You can then use Log Analytics to query the data and correlate it with other log data.

Many services can use diagnostic settings to send metric and log data to other storage locations outside Azure Monitor. Examples include Azure Storage, [hosted partner systems](/en-us/azure/partner-solutions/overview), and [non-Azure partner systems, by using Event Hubs](/en-us/azure/azure-monitor/essentials/stream-monitoring-data-event-hubs).

For detailed information on how Azure Monitor stores data, see [Azure Monitor data platform](/en-us/azure/azure-monitor/platform/data-platform).

## Azure Monitor platform metrics

Azure Monitor provides platform metrics for most services. These metrics are:

- Individually defined for each namespace.
- Stored in the Azure Monitor time-series metrics database.
- Lightweight and capable of supporting near real-time alerting.
- Used to track the performance of a resource over time.

**Collection:** Azure Monitor collects platform metrics automatically. No configuration is required.

**Routing:** You can also route some platform metrics to Azure Monitor Logs / Log Analytics so you can query them with other log data. Check the **DS export** setting for each metric to see if you can use a diagnostic setting to route the metric to Azure Monitor Logs / Log Analytics.

- For more information, see the
[Metrics diagnostic setting](/en-us/azure/azure-monitor/essentials/diagnostic-settings#metrics). - To configure diagnostic settings for a service, see
[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings).

For a list of all metrics it's possible to gather for all resources in Azure Monitor, see [Supported metrics in Azure Monitor](/en-us/azure/azure-monitor/platform/metrics-supported).

For a list of available metrics for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference#metrics).

Note

App Service metrics (Microsoft.Web/sites) aren't available when your function app runs on Linux in a [Consumption plan](consumption-plan).

## Azure Monitor resource logs

Resource logs provide insight into operations that were done by an Azure resource. Logs are generated automatically, but you must route them to Azure Monitor logs to save or query them. Logs are organized in categories. A given namespace might have multiple resource log categories.

**Collection:** Resource logs aren't collected and stored until you create a *diagnostic setting* and route the logs to one or more locations. When you create a diagnostic setting, you specify which categories of logs to collect. There are multiple ways to create and maintain diagnostic settings, including the Azure portal, programmatically, and though Azure Policy.

**Routing:** The suggested default is to route resource logs to Azure Monitor Logs so you can query them with other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information, see [Azure resource logs](/en-us/azure/azure-monitor/essentials/resource-logs) and [Resource log destinations](/en-us/azure/azure-monitor/essentials/diagnostic-settings#destinations).

For detailed information about collecting, storing, and routing resource logs, see [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

For a list of all available resource log categories in Azure Monitor, see [Supported resource logs in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-logs/logs-index).

All resource logs in Azure Monitor have the same header fields, followed by service-specific fields. The common schema is outlined in [Azure Monitor resource log schema](/en-us/azure/azure-monitor/essentials/resource-logs-schema).

Azure Functions integrates with Azure Monitor Logs to monitor functions. For detailed instructions on how to set up diagnostic settings to configure and route resource logs, see [Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/platform/diagnostic-settings).


For the available resource log categories, their associated Log Analytics tables, and the logs schemas for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference#resource-logs).

Important

Application Insights processes telemetry in batches. When a batch payload is too large or contains unescaped special characters, log entries might be dropped. To help prevent data loss:

- Limit individual log messages to 10,000 characters, especially when you log large XML or JSON payloads.
- Escape special characters in log data.
- Summarize or truncate large payloads before you log them.

## Azure activity log

The activity log contains subscription-level events that track operations for each Azure resource as seen from outside that resource; for example, creating a new resource or starting a virtual machine.

**Collection:** Activity log events are automatically generated and collected in a separate store for viewing in the Azure portal.

**Routing:** You can send activity log data to Azure Monitor Logs so you can analyze it alongside other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information on how to route the activity log, see [Overview of the Azure activity log](/en-us/azure/azure-monitor/essentials/activity-log).

## Other logs

Azure Functions also offers the ability to collect more than Azure Monitor resource logs. To view a near real time stream of application log files generated by your function running in Azure, you can connect to Application Insights and use Live Metrics Stream. Or, you can use the App Service platform built-in log streaming to view a stream of application log files. For more information, see [Enable streaming execution logs in Azure Functions](streaming-logs).

## Analyze monitoring data

There are many tools for analyzing monitoring data.

### Azure Monitor tools

Azure Monitor supports the following basic tools:

[Metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started), a tool in the Azure portal that allows you to view and analyze metrics for Azure resources. For more information, see[Analyze metrics with Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started).[Log Analytics](/en-us/azure/azure-monitor/learn/quick-create-workspace), a tool in the Azure portal that allows you to query and analyze log data by using the[Kusto query language (KQL)](/en-us/azure/data-explorer/kusto/query). For more information, see[Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/get-started-queries).The

[activity log](/en-us/azure/azure-monitor/essentials/activity-log), which has a user interface in the Azure portal for viewing and basic searches. To do more in-depth analysis, you have to route the data to Azure Monitor logs and run more complex queries in Log Analytics.

Tools that allow more complex visualization include:

[Dashboards](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards)that let you combine different kinds of data into a single pane in the Azure portal.[Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview), customizable reports that you can create in the Azure portal. Workbooks can include text, metrics, and log queries.[Grafana](/en-us/azure/azure-monitor/visualize/grafana-plugin), an open platform tool that excels in operational dashboards. You can use Grafana to create dashboards that include data from multiple sources other than Azure Monitor.[Power BI](/en-us/azure/azure-monitor/logs/log-powerbi), a business analytics service that provides interactive visualizations across various data sources. You can configure Power BI to automatically import log data from Azure Monitor to take advantage of these visualizations.

### Azure Monitor export tools

You can get data out of Azure Monitor into other tools by using the following methods:

**Metrics:**Use the[REST API for metrics](/en-us/rest/api/monitor/operation-groups)to extract metric data from the Azure Monitor metrics database. The API supports filter expressions to refine the data retrieved. For more information, see[Azure Monitor REST API reference](/en-us/rest/api/monitor/filter-syntax).**Logs:**Use the REST API or the[associated client libraries](/en-us/azure/azure-monitor/logs/api/overview).Another option is the

[workspace data export](/en-us/azure/azure-monitor/logs/logs-data-export?tabs=portal).

To get started with the REST API for Azure Monitor, see [Azure monitoring REST API walkthrough](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough?tabs=portal).

### Analyze metrics for Azure Functions

Functions provides these two dynamic scale plans that support serverless hosting:

Provides fast horizontal scaling, with flexible compute options, virtual network integration, and full support for connections using Microsoft Entra ID authentication. In this plan, instances dynamically scale out based on configured per-instance concurrency, incoming events, and per-function workloads for optimal efficiency. Flex Consumption is the recommended plan for serverless hosting. For more information, see [Azure Functions Flex Consumption plan hosting](flex-consumption-plan).

The app-level metrics available to your app depend on the type of consumption plan you use.

These Azure Monitor metrics are related to Flex Consumption plan billing:

| Metric | Description | Meter calculation |
|---|---|---|
On Demand Function Execution Count |
Total number of function executions in on demand instances. | `OnDemandFunctionExecutionCount` relates to the On Demand Total Executions meter. |
Always Ready Function Execution Count |
Total number of function executions in always ready instances. | `AlwaysReadyFunctionExecutionCount` relates to the Always Ready Total Executions meter. |
On Demand Function Execution Units |
Total MB-milliseconds from on demand instances while actively executing functions. | `OnDemandFunctionExecutionUnits / 1,024,000` is the On Demand Execution Time meter, in GB-seconds. |
Always Ready Function Execution Units |
Total MB-milliseconds from always ready instances while actively executing functions. | `AlwaysReadyFunctionExecutionUnits / 1,024,000` is the Always Ready Execution Time meter, in GB-seconds. |
Always Ready Units |
The total MB-milliseconds of always ready instances assigned to the app, whether or not functions are actively executing. | `AlwaysReadyUnits / 1,024,000` is the Always Ready Baseline meter, in GB-seconds. |

For more information, see [Azure Functions monitoring data reference](monitor-functions-reference).

To better understand the costs of your functions, use Azure Monitor to view cost-related metrics that your function apps generate. You can view Monitor metrics by using one of these tools:

Use [Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started) to view cost-related data for your Flex Consumption plan function apps in a graphical format.

In the

[Azure portal](https://portal.azure.com), go to your function app.In the left panel, scroll down to

**Monitoring**and select**Metrics**.From

**Metric**, select**On Demand Function Execution Count**and**Sum**for**Aggregation**. This selection adds the sum of the execution counts during the chosen period to the chart.Select

**Add metric**and add**On Demand Function Execution Units**,**Always Ready Function Execution Count**,**Always Ready Function Execution Units**, and**Always Ready Units**to the chart.

The resulting chart contains the totals for all the Flex Consumption execution metrics in the chosen time range, which in this example is a custom time range.

Because the number of On Demand Function Execution Units is greater than On Demand Function Execution Count, and there were no [always ready instances](flex-consumption-plan#always-ready-instances) on the app, the chart just shows On Demand Function Execution Units.

This chart shows a total of 3.54 billion `On Demand Function Execution Units`

consumed in a 16-minute period, measured in MB-milliseconds. To convert to GB-seconds, divide by 1,024,000. In this example, the function app consumed `3,540,000,000 / 1,024,000 = 3,457.03`

GB-seconds. You can take this value and multiply it by the current price of On Demand Execution Time on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/), which gives you the cost of these 16 minutes, assuming you already used any free grants of execution time. You can use this same calculation with the The Always Ready Function Execution Units metric and the Always Ready Execution Time billing meter cost, as well as with the Always Ready Units metric and the Always Ready Baseline billing meter cost, to find out the GB-seconds costs for always ready instances.

To calculate the On Demand Total Executions cost, take the On Demand Function Execution Count sum for the same time period, convert to millions, and then multiply by the On Demand Total Executions price on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/). For example, 2,100 executions in the example above converts to `0.0021`

million executions. You can use this same calculation with the Always Ready Function Execution Count metric and the Always Ready Total Executions billing meter to find out the cost for executions handled by always ready instance.

To learn more about estimating costs for these plans, see [Estimating consumption plan costs](functions-consumption-costs).

### Analyze logs for Azure Functions

Azure Functions writes all logs to the **FunctionAppLogs** table under **LogManagement** in the Log Analytics workspace where you send the data. You can use Kusto queries to query the data.


## Kusto queries

You can analyze monitoring data in the Azure Monitor Logs / Log Analytics store by using the Kusto query language (KQL).

Important

When you select **Logs** from the service's menu in the portal, Log Analytics opens with the query scope set to the current service. This scope means that log queries will only include data from that type of resource. If you want to run a query that includes data from other Azure services, select **Logs** from the **Azure Monitor** menu. See [Log query scope and time range in Azure Monitor Log Analytics](/en-us/azure/azure-monitor/logs/scope) for details.

For a list of common queries for any service, see the [Log Analytics queries interface](/en-us/azure/azure-monitor/logs/queries).

The following sample queries can help you monitor all your functions app logs:

```
FunctionAppLogs
| order by TimeGenerated desc
```


```
FunctionAppLogs
| project TimeGenerated, HostInstanceId, Message, _ResourceId
| order by TimeGenerated desc
```


The following sample query can help you monitor a specific functions app's logs:

```
FunctionAppLogs
| where FunctionName == "<Function name>"
| order by TimeGenerated desc
```


The following sample query can help you monitor exceptions on all your functions app logs:

```
FunctionAppLogs
| where ExceptionDetails != ""
| order by TimeGenerated asc
```


The following sample query can help you monitor exceptions on a specific functions app's logs:

```
FunctionAppLogs
| where ExceptionDetails != ""
| where FunctionName == "<Function name>"
| order by TimeGenerated desc
```


## Alerts

Azure Monitor alerts proactively notify you when specific conditions are found in your monitoring data. Alerts allow you to identify and address issues in your system before your customers notice them. For more information, see [Azure Monitor alerts](/en-us/azure/azure-monitor/alerts/alerts-overview).

There are many sources of common alerts for Azure resources. For examples of common alerts for Azure resources, see [Sample log alert queries](/en-us/azure/azure-monitor/alerts/alerts-log-alert-query-samples). The [Azure Monitor Baseline Alerts (AMBA)](https://aka.ms/amba) site provides a semi-automated method of implementing important platform metric alerts, dashboards, and guidelines. The site applies to a continually expanding subset of Azure services, including all services that are part of the Azure Landing Zone (ALZ).

The common alert schema standardizes the consumption of Azure Monitor alert notifications. For more information, see [Common alert schema](/en-us/azure/azure-monitor/alerts/alerts-common-schema).

### Types of alerts

You can alert on any metric or log data source in the Azure Monitor data platform. There are many different types of alerts depending on the services you're monitoring and the monitoring data you're collecting. Different types of alerts have various benefits and drawbacks. For more information, see [Choose the right monitoring alert type](/en-us/azure/azure-monitor/alerts/alerts-types).

The following list describes the types of Azure Monitor alerts you can create:

[Metric alerts](/en-us/azure/azure-monitor/alerts/alerts-types#metric-alerts)evaluate resource metrics at regular intervals. Metrics can be platform metrics, custom metrics, logs from Azure Monitor converted to metrics, or Application Insights metrics. Metric alerts can also apply multiple conditions and dynamic thresholds.[Log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#log-alerts)allow users to use a Log Analytics query to evaluate resource logs at a predefined frequency.[Activity log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#activity-log-alerts)trigger when a new activity log event occurs that matches defined conditions. Resource Health alerts and Service Health alerts are activity log alerts that report on your service and resource health.

Some Azure services also support [smart detection alerts](/en-us/azure/azure-monitor/alerts/alerts-types#smart-detection-alerts), [Prometheus alerts](/en-us/azure/azure-monitor/alerts/alerts-types#prometheus-alerts), or [recommended alert rules](/en-us/azure/azure-monitor/alerts/alerts-manage-alert-rules#enable-recommended-alert-rules-in-the-azure-portal).

For some services, you can monitor at scale by applying the same metric alert rule to multiple resources of the same type that exist in the same Azure region. Individual notifications are sent for each monitored resource. For supported Azure services and clouds, see [Monitor multiple resources with one alert rule](/en-us/azure/azure-monitor/alerts/alerts-types#monitor-multiple-resources-with-one-alert-rule).

Note

If you're creating or running an application that runs on your service, [Azure Monitor application insights](/en-us/azure/azure-monitor/overview#application-insights) might offer more types of alerts.

### Azure Functions alert rules

The following table lists common and recommended alert rules for Azure Functions. These alerts are just recommendations. You can set alerts for any metric, log entry, or activity log entry listed in the [Monitoring data reference for Azure Functions](monitor-functions-reference).

| Alert type | Condition | Description |
|---|---|---|
| Metric | Average connections | When number of connections exceed a set value |
| Metric | HTTP 404 | When HTTP 404 responses exceed a set value |
| Metric | HTTP Server Errors | When HTTP 5xx errors exceed a set value |
| Activity Log | Create or update function app | When app is created or updated |
| Activity Log | Delete function app | When app is deleted |
| Activity Log | Restart function app | When app is restarted |
| Activity Log | Stop function app | When app is stopped |

### Advisor recommendations

For some services, if critical conditions or imminent changes occur during resource operations, an alert displays on the service **Overview** page in the portal. You can find more information and recommended fixes for the alert in **Advisor recommendations** under **Monitoring** in the left menu. During normal operations, no advisor recommendations display.

For more information on Azure Advisor, see [Azure Advisor overview](/en-us/azure/advisor/advisor-overview).

## Related content

For more information about monitoring Azure Functions, see the following articles:

[Azure Functions monitoring data reference](monitor-functions-reference)provides a reference of the metrics, logs, and other important values available for your function app.[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)gives general details about monitoring Azure resources.[Monitor executions in Azure Functions](functions-monitoring)details how to monitor a function app.[How to configure monitoring for Azure Functions](configure-monitoring)describes how to configure monitoring.[Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data)describes how to view and query the data being collected from a function app.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-monitor-log-analytics -->

# Monitor Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes:

- The types of monitoring data you can collect for this service.
- Ways to analyze that data.

Note

If you're already familiar with this service and/or Azure Monitor and just want to know how to analyze monitoring data, see the [Analyze](#analyze-monitoring-data) section near the end of this article.

When you have critical applications and business processes that rely on Azure resources, you need to monitor and get alerts for your system. The Azure Monitor service collects and aggregates metrics and logs from every component of your system. Azure Monitor provides you with a view of availability, performance, and resilience, and notifies you of issues. You can use the Azure portal, PowerShell, Azure CLI, REST API, or client libraries to set up and view monitoring data.

- For more information on Azure Monitor, see the
[Azure Monitor overview](/en-us/azure/azure-monitor/overview). - For more information on how to monitor Azure resources in general, see
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource).

## Insights

Some services in Azure have a built-in monitoring dashboard in the Azure portal that provides a starting point for monitoring your service. These dashboards are called *insights*, and you can find them in the **Insights Hub** of Azure Monitor in the Azure portal.

### Application Insights

Azure Functions has built-in integration with Application Insights to monitor function executions. For detailed information about how to integrate, configure, and use Application Insights to monitor Azure Functions, see the following articles:

[Monitor executions in Azure Functions](functions-monitoring)[Configure monitoring for Azure Functions](configure-monitoring)[Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data)[Monitor Azure Functions with Application Insights](/en-us/azure/azure-monitor/app/monitor-functions)

## Resource types

Azure uses the concept of resource types and IDs to identify everything in a subscription. Resource types are also part of the resource IDs for every resource running in Azure. For example, one resource type for a virtual machine is `Microsoft.Compute/virtualMachines`

. For a list of services and their associated resource types, see [Resource providers](/en-us/azure/azure-resource-manager/management/azure-services-resource-providers).

Azure Monitor similarly organizes core monitoring data into metrics and logs based on resource types, also called *namespaces*. Different metrics and logs are available for different resource types. Your service might be associated with more than one resource type.

For more information about the resource types for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference).

## Data storage

For Azure Monitor:

- Metrics data is stored in the Azure Monitor metrics database.
- Log data is stored in the Azure Monitor logs store. Log Analytics is a tool in the Azure portal that can query this store.
- The Azure activity log is a separate store with its own interface in the Azure portal.

You can optionally route metric and activity log data to the Azure Monitor logs store. You can then use Log Analytics to query the data and correlate it with other log data.

Many services can use diagnostic settings to send metric and log data to other storage locations outside Azure Monitor. Examples include Azure Storage, [hosted partner systems](/en-us/azure/partner-solutions/overview), and [non-Azure partner systems, by using Event Hubs](/en-us/azure/azure-monitor/essentials/stream-monitoring-data-event-hubs).

For detailed information on how Azure Monitor stores data, see [Azure Monitor data platform](/en-us/azure/azure-monitor/platform/data-platform).

## Azure Monitor platform metrics

Azure Monitor provides platform metrics for most services. These metrics are:

- Individually defined for each namespace.
- Stored in the Azure Monitor time-series metrics database.
- Lightweight and capable of supporting near real-time alerting.
- Used to track the performance of a resource over time.

**Collection:** Azure Monitor collects platform metrics automatically. No configuration is required.

**Routing:** You can also route some platform metrics to Azure Monitor Logs / Log Analytics so you can query them with other log data. Check the **DS export** setting for each metric to see if you can use a diagnostic setting to route the metric to Azure Monitor Logs / Log Analytics.

- For more information, see the
[Metrics diagnostic setting](/en-us/azure/azure-monitor/essentials/diagnostic-settings#metrics). - To configure diagnostic settings for a service, see
[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings).

For a list of all metrics it's possible to gather for all resources in Azure Monitor, see [Supported metrics in Azure Monitor](/en-us/azure/azure-monitor/platform/metrics-supported).

For a list of available metrics for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference#metrics).

Note

App Service metrics (Microsoft.Web/sites) aren't available when your function app runs on Linux in a [Consumption plan](consumption-plan).

## Azure Monitor resource logs

Resource logs provide insight into operations that were done by an Azure resource. Logs are generated automatically, but you must route them to Azure Monitor logs to save or query them. Logs are organized in categories. A given namespace might have multiple resource log categories.

**Collection:** Resource logs aren't collected and stored until you create a *diagnostic setting* and route the logs to one or more locations. When you create a diagnostic setting, you specify which categories of logs to collect. There are multiple ways to create and maintain diagnostic settings, including the Azure portal, programmatically, and though Azure Policy.

**Routing:** The suggested default is to route resource logs to Azure Monitor Logs so you can query them with other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information, see [Azure resource logs](/en-us/azure/azure-monitor/essentials/resource-logs) and [Resource log destinations](/en-us/azure/azure-monitor/essentials/diagnostic-settings#destinations).

For detailed information about collecting, storing, and routing resource logs, see [Diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

For a list of all available resource log categories in Azure Monitor, see [Supported resource logs in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-logs/logs-index).

All resource logs in Azure Monitor have the same header fields, followed by service-specific fields. The common schema is outlined in [Azure Monitor resource log schema](/en-us/azure/azure-monitor/essentials/resource-logs-schema).

Azure Functions integrates with Azure Monitor Logs to monitor functions. For detailed instructions on how to set up diagnostic settings to configure and route resource logs, see [Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/platform/diagnostic-settings).


For the available resource log categories, their associated Log Analytics tables, and the logs schemas for Azure Functions, see [Azure Functions monitoring data reference](monitor-functions-reference#resource-logs).

Important

Application Insights processes telemetry in batches. When a batch payload is too large or contains unescaped special characters, log entries might be dropped. To help prevent data loss:

- Limit individual log messages to 10,000 characters, especially when you log large XML or JSON payloads.
- Escape special characters in log data.
- Summarize or truncate large payloads before you log them.

## Azure activity log

The activity log contains subscription-level events that track operations for each Azure resource as seen from outside that resource; for example, creating a new resource or starting a virtual machine.

**Collection:** Activity log events are automatically generated and collected in a separate store for viewing in the Azure portal.

**Routing:** You can send activity log data to Azure Monitor Logs so you can analyze it alongside other log data. Other locations such as Azure Storage, Azure Event Hubs, and certain Microsoft monitoring partners are also available. For more information on how to route the activity log, see [Overview of the Azure activity log](/en-us/azure/azure-monitor/essentials/activity-log).

## Other logs

Azure Functions also offers the ability to collect more than Azure Monitor resource logs. To view a near real time stream of application log files generated by your function running in Azure, you can connect to Application Insights and use Live Metrics Stream. Or, you can use the App Service platform built-in log streaming to view a stream of application log files. For more information, see [Enable streaming execution logs in Azure Functions](streaming-logs).

## Analyze monitoring data

There are many tools for analyzing monitoring data.

### Azure Monitor tools

Azure Monitor supports the following basic tools:

[Metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started), a tool in the Azure portal that allows you to view and analyze metrics for Azure resources. For more information, see[Analyze metrics with Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started).[Log Analytics](/en-us/azure/azure-monitor/learn/quick-create-workspace), a tool in the Azure portal that allows you to query and analyze log data by using the[Kusto query language (KQL)](/en-us/azure/data-explorer/kusto/query). For more information, see[Get started with log queries in Azure Monitor](/en-us/azure/azure-monitor/logs/get-started-queries).The

[activity log](/en-us/azure/azure-monitor/essentials/activity-log), which has a user interface in the Azure portal for viewing and basic searches. To do more in-depth analysis, you have to route the data to Azure Monitor logs and run more complex queries in Log Analytics.

Tools that allow more complex visualization include:

[Dashboards](/en-us/azure/azure-monitor/visualize/tutorial-logs-dashboards)that let you combine different kinds of data into a single pane in the Azure portal.[Workbooks](/en-us/azure/azure-monitor/visualize/workbooks-overview), customizable reports that you can create in the Azure portal. Workbooks can include text, metrics, and log queries.[Grafana](/en-us/azure/azure-monitor/visualize/grafana-plugin), an open platform tool that excels in operational dashboards. You can use Grafana to create dashboards that include data from multiple sources other than Azure Monitor.[Power BI](/en-us/azure/azure-monitor/logs/log-powerbi), a business analytics service that provides interactive visualizations across various data sources. You can configure Power BI to automatically import log data from Azure Monitor to take advantage of these visualizations.

### Azure Monitor export tools

You can get data out of Azure Monitor into other tools by using the following methods:

**Metrics:**Use the[REST API for metrics](/en-us/rest/api/monitor/operation-groups)to extract metric data from the Azure Monitor metrics database. The API supports filter expressions to refine the data retrieved. For more information, see[Azure Monitor REST API reference](/en-us/rest/api/monitor/filter-syntax).**Logs:**Use the REST API or the[associated client libraries](/en-us/azure/azure-monitor/logs/api/overview).Another option is the

[workspace data export](/en-us/azure/azure-monitor/logs/logs-data-export?tabs=portal).

To get started with the REST API for Azure Monitor, see [Azure monitoring REST API walkthrough](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough?tabs=portal).

### Analyze metrics for Azure Functions

Functions provides these two dynamic scale plans that support serverless hosting:

Provides fast horizontal scaling, with flexible compute options, virtual network integration, and full support for connections using Microsoft Entra ID authentication. In this plan, instances dynamically scale out based on configured per-instance concurrency, incoming events, and per-function workloads for optimal efficiency. Flex Consumption is the recommended plan for serverless hosting. For more information, see [Azure Functions Flex Consumption plan hosting](flex-consumption-plan).

The app-level metrics available to your app depend on the type of consumption plan you use.

These Azure Monitor metrics are related to Flex Consumption plan billing:

| Metric | Description | Meter calculation |
|---|---|---|
On Demand Function Execution Count |
Total number of function executions in on demand instances. | `OnDemandFunctionExecutionCount` relates to the On Demand Total Executions meter. |
Always Ready Function Execution Count |
Total number of function executions in always ready instances. | `AlwaysReadyFunctionExecutionCount` relates to the Always Ready Total Executions meter. |
On Demand Function Execution Units |
Total MB-milliseconds from on demand instances while actively executing functions. | `OnDemandFunctionExecutionUnits / 1,024,000` is the On Demand Execution Time meter, in GB-seconds. |
Always Ready Function Execution Units |
Total MB-milliseconds from always ready instances while actively executing functions. | `AlwaysReadyFunctionExecutionUnits / 1,024,000` is the Always Ready Execution Time meter, in GB-seconds. |
Always Ready Units |
The total MB-milliseconds of always ready instances assigned to the app, whether or not functions are actively executing. | `AlwaysReadyUnits / 1,024,000` is the Always Ready Baseline meter, in GB-seconds. |

For more information, see [Azure Functions monitoring data reference](monitor-functions-reference).

To better understand the costs of your functions, use Azure Monitor to view cost-related metrics that your function apps generate. You can view Monitor metrics by using one of these tools:

Use [Azure Monitor metrics explorer](/en-us/azure/azure-monitor/essentials/metrics-getting-started) to view cost-related data for your Flex Consumption plan function apps in a graphical format.

In the

[Azure portal](https://portal.azure.com), go to your function app.In the left panel, scroll down to

**Monitoring**and select**Metrics**.From

**Metric**, select**On Demand Function Execution Count**and**Sum**for**Aggregation**. This selection adds the sum of the execution counts during the chosen period to the chart.Select

**Add metric**and add**On Demand Function Execution Units**,**Always Ready Function Execution Count**,**Always Ready Function Execution Units**, and**Always Ready Units**to the chart.

The resulting chart contains the totals for all the Flex Consumption execution metrics in the chosen time range, which in this example is a custom time range.

Because the number of On Demand Function Execution Units is greater than On Demand Function Execution Count, and there were no [always ready instances](flex-consumption-plan#always-ready-instances) on the app, the chart just shows On Demand Function Execution Units.

This chart shows a total of 3.54 billion `On Demand Function Execution Units`

consumed in a 16-minute period, measured in MB-milliseconds. To convert to GB-seconds, divide by 1,024,000. In this example, the function app consumed `3,540,000,000 / 1,024,000 = 3,457.03`

GB-seconds. You can take this value and multiply it by the current price of On Demand Execution Time on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/), which gives you the cost of these 16 minutes, assuming you already used any free grants of execution time. You can use this same calculation with the The Always Ready Function Execution Units metric and the Always Ready Execution Time billing meter cost, as well as with the Always Ready Units metric and the Always Ready Baseline billing meter cost, to find out the GB-seconds costs for always ready instances.

To calculate the On Demand Total Executions cost, take the On Demand Function Execution Count sum for the same time period, convert to millions, and then multiply by the On Demand Total Executions price on the [Functions pricing page](https://azure.microsoft.com/pricing/details/functions/). For example, 2,100 executions in the example above converts to `0.0021`

million executions. You can use this same calculation with the Always Ready Function Execution Count metric and the Always Ready Total Executions billing meter to find out the cost for executions handled by always ready instance.

To learn more about estimating costs for these plans, see [Estimating consumption plan costs](functions-consumption-costs).

### Analyze logs for Azure Functions

Azure Functions writes all logs to the **FunctionAppLogs** table under **LogManagement** in the Log Analytics workspace where you send the data. You can use Kusto queries to query the data.


## Kusto queries

You can analyze monitoring data in the Azure Monitor Logs / Log Analytics store by using the Kusto query language (KQL).

Important

When you select **Logs** from the service's menu in the portal, Log Analytics opens with the query scope set to the current service. This scope means that log queries will only include data from that type of resource. If you want to run a query that includes data from other Azure services, select **Logs** from the **Azure Monitor** menu. See [Log query scope and time range in Azure Monitor Log Analytics](/en-us/azure/azure-monitor/logs/scope) for details.

For a list of common queries for any service, see the [Log Analytics queries interface](/en-us/azure/azure-monitor/logs/queries).

The following sample queries can help you monitor all your functions app logs:

```
FunctionAppLogs
| order by TimeGenerated desc
```


```
FunctionAppLogs
| project TimeGenerated, HostInstanceId, Message, _ResourceId
| order by TimeGenerated desc
```


The following sample query can help you monitor a specific functions app's logs:

```
FunctionAppLogs
| where FunctionName == "<Function name>"
| order by TimeGenerated desc
```


The following sample query can help you monitor exceptions on all your functions app logs:

```
FunctionAppLogs
| where ExceptionDetails != ""
| order by TimeGenerated asc
```


The following sample query can help you monitor exceptions on a specific functions app's logs:

```
FunctionAppLogs
| where ExceptionDetails != ""
| where FunctionName == "<Function name>"
| order by TimeGenerated desc
```


## Alerts

Azure Monitor alerts proactively notify you when specific conditions are found in your monitoring data. Alerts allow you to identify and address issues in your system before your customers notice them. For more information, see [Azure Monitor alerts](/en-us/azure/azure-monitor/alerts/alerts-overview).

There are many sources of common alerts for Azure resources. For examples of common alerts for Azure resources, see [Sample log alert queries](/en-us/azure/azure-monitor/alerts/alerts-log-alert-query-samples). The [Azure Monitor Baseline Alerts (AMBA)](https://aka.ms/amba) site provides a semi-automated method of implementing important platform metric alerts, dashboards, and guidelines. The site applies to a continually expanding subset of Azure services, including all services that are part of the Azure Landing Zone (ALZ).

The common alert schema standardizes the consumption of Azure Monitor alert notifications. For more information, see [Common alert schema](/en-us/azure/azure-monitor/alerts/alerts-common-schema).

### Types of alerts

You can alert on any metric or log data source in the Azure Monitor data platform. There are many different types of alerts depending on the services you're monitoring and the monitoring data you're collecting. Different types of alerts have various benefits and drawbacks. For more information, see [Choose the right monitoring alert type](/en-us/azure/azure-monitor/alerts/alerts-types).

The following list describes the types of Azure Monitor alerts you can create:

[Metric alerts](/en-us/azure/azure-monitor/alerts/alerts-types#metric-alerts)evaluate resource metrics at regular intervals. Metrics can be platform metrics, custom metrics, logs from Azure Monitor converted to metrics, or Application Insights metrics. Metric alerts can also apply multiple conditions and dynamic thresholds.[Log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#log-alerts)allow users to use a Log Analytics query to evaluate resource logs at a predefined frequency.[Activity log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#activity-log-alerts)trigger when a new activity log event occurs that matches defined conditions. Resource Health alerts and Service Health alerts are activity log alerts that report on your service and resource health.

Some Azure services also support [smart detection alerts](/en-us/azure/azure-monitor/alerts/alerts-types#smart-detection-alerts), [Prometheus alerts](/en-us/azure/azure-monitor/alerts/alerts-types#prometheus-alerts), or [recommended alert rules](/en-us/azure/azure-monitor/alerts/alerts-manage-alert-rules#enable-recommended-alert-rules-in-the-azure-portal).

For some services, you can monitor at scale by applying the same metric alert rule to multiple resources of the same type that exist in the same Azure region. Individual notifications are sent for each monitored resource. For supported Azure services and clouds, see [Monitor multiple resources with one alert rule](/en-us/azure/azure-monitor/alerts/alerts-types#monitor-multiple-resources-with-one-alert-rule).

Note

If you're creating or running an application that runs on your service, [Azure Monitor application insights](/en-us/azure/azure-monitor/overview#application-insights) might offer more types of alerts.

### Azure Functions alert rules

The following table lists common and recommended alert rules for Azure Functions. These alerts are just recommendations. You can set alerts for any metric, log entry, or activity log entry listed in the [Monitoring data reference for Azure Functions](monitor-functions-reference).

| Alert type | Condition | Description |
|---|---|---|
| Metric | Average connections | When number of connections exceed a set value |
| Metric | HTTP 404 | When HTTP 404 responses exceed a set value |
| Metric | HTTP Server Errors | When HTTP 5xx errors exceed a set value |
| Activity Log | Create or update function app | When app is created or updated |
| Activity Log | Delete function app | When app is deleted |
| Activity Log | Restart function app | When app is restarted |
| Activity Log | Stop function app | When app is stopped |

### Advisor recommendations

For some services, if critical conditions or imminent changes occur during resource operations, an alert displays on the service **Overview** page in the portal. You can find more information and recommended fixes for the alert in **Advisor recommendations** under **Monitoring** in the left menu. During normal operations, no advisor recommendations display.

For more information on Azure Advisor, see [Azure Advisor overview](/en-us/azure/advisor/advisor-overview).

## Related content

For more information about monitoring Azure Functions, see the following articles:

[Azure Functions monitoring data reference](monitor-functions-reference)provides a reference of the metrics, logs, and other important values available for your function app.[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)gives general details about monitoring Azure resources.[Monitor executions in Azure Functions](functions-monitoring)details how to monitor a function app.[How to configure monitoring for Azure Functions](configure-monitoring)describes how to configure monitoring.[Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data)describes how to view and query the data being collected from a function app.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/develop-python-worker-extensions -->

# Develop Python worker extensions for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

Starting with Python 3.13, python worker extensions will no longer be supported.

Azure Functions lets you integrate custom behaviors as part of Python function execution. This feature enables you to create business logic that customers can easily use in their own function apps. Worker extensions are supported in both the v1 and v2 Python programming models.

In this tutorial, you'll learn how to:

- Create an application-level Python worker extension for Azure Functions.
- Consume your extension in an app the way your customers do.
- Package and publish an extension for consumption.

## Prerequisites

Before you start, you must meet these requirements:

[Python 3.7 or above](https://www.python.org/downloads). To check the full list of supported Python versions in Azure Functions, see the[Python developer guide](functions-reference-python#supported-python-versions).The

[Azure Functions Core Tools](functions-run-local#v2), version 4.0.5095 or later, which supports using the extension with the[v2 Python programming model](functions-reference-python). Check your version with`func --version`

.[Visual Studio Code](https://code.visualstudio.com/)installed on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).

## Create the Python Worker extension

The extension you create reports the elapsed time of an HTTP trigger invocation in the console logs and in the HTTP response body.

### Folder structure

The folder for your extension project should be like the following structure:

```
<python_worker_extension_root>/
| - .venv/
| - python_worker_extension_timer/
| | - __init__.py
| - setup.py
| - readme.md
```


| Folder/file | Description |
|---|---|
.venv/ |
(Optional) Contains a Python virtual environment used for local development. |
python_worker_extension/ |
Contains the source code of the Python worker extension. This folder contains the main Python module to be published into PyPI. |
setup.py |
Contains the metadata of the Python worker extension package. |
readme.md |
Contains the instruction and usage of your extension. This content is displayed as the description in the home page in your PyPI project. |

### Configure project metadata

First you create `setup.py`

, which provides essential information about your package. To make sure that your extension is distributed and integrated into your customer's function apps properly, confirm that `'azure-functions >= 1.7.0, < 2.0.0'`

is in the `install_requires`

section.

In the following template, you should change `author`

, `author_email`

, `install_requires`

, `license`

, `packages`

, and `url`

fields as needed.

```
from setuptools import find_packages, setup
setup(
name='python-worker-extension-timer',
version='1.0.0',
author='Your Name Here',
author_email='your@email.here',
classifiers=[
'Intended Audience :: End Users/Desktop',
'Development Status :: 5 - Production/Stable',
'Intended Audience :: End Users/Desktop',
'License :: OSI Approved :: Apache Software License',
'Programming Language :: Python',
'Programming Language :: Python :: 3.7',
'Programming Language :: Python :: 3.8',
'Programming Language :: Python :: 3.9',
'Programming Language :: Python :: 3.10',
],
description='Python Worker Extension Demo',
include_package_data=True,
long_description=open('readme.md').read(),
install_requires=[
'azure-functions >= 1.7.0, < 2.0.0',
# Any additional packages that will be used in your extension
],
extras_require={},
license='MIT',
packages=find_packages(where='.'),
url='https://your-github-or-pypi-link',
zip_safe=False,
)
```


Next, you'll implement your extension code in the application-level scope.

### Implement the timer extension

Add the following code in `python_worker_extension_timer/__init__.py`

to implement the application-level extension:

```
import typing
from logging import Logger
from time import time
from azure.functions import AppExtensionBase, Context, HttpResponse
class TimerExtension(AppExtensionBase):
"""A Python worker extension to record elapsed time in a function invocation
"""
@classmethod
def init(cls):
# This records the starttime of each function
cls.start_timestamps: typing.Dict[str, float] = {}
@classmethod
def configure(cls, *args, append_to_http_response:bool=False, **kwargs):
# Customer can use TimerExtension.configure(append_to_http_response=)
# to decide whether the elapsed time should be shown in HTTP response
cls.append_to_http_response = append_to_http_response
@classmethod
def pre_invocation_app_level(
cls, logger: Logger, context: Context,
func_args: typing.Dict[str, object],
*args, **kwargs
) -> None:
logger.info(f'Recording start time of {context.function_name}')
cls.start_timestamps[context.invocation_id] = time()
@classmethod
def post_invocation_app_level(
cls, logger: Logger, context: Context,
func_args: typing.Dict[str, object],
func_ret: typing.Optional[object],
*args, **kwargs
) -> None:
if context.invocation_id in cls.start_timestamps:
# Get the start_time of the invocation
start_time: float = cls.start_timestamps.pop(context.invocation_id)
end_time: float = time()
# Calculate the elapsed time
elapsed_time = end_time - start_time
logger.info(f'Time taken to execute {context.function_name} is {elapsed_time} sec')
# Append the elapsed time to the end of HTTP response
# if the append_to_http_response is set to True
if cls.append_to_http_response and isinstance(func_ret, HttpResponse):
func_ret._HttpResponse__body += f' (TimeElapsed: {elapsed_time} sec)'.encode()
```


This code inherits from [AppExtensionBase](https://github.com/Azure/azure-functions-python-library/blob/dev/azure/functions/extension/app_extension_base.py) so that the extension applies to every function in the app. You could have also implemented the extension on a function-level scope by inheriting from [FuncExtensionBase](https://github.com/Azure/azure-functions-python-library/blob/dev/azure/functions/extension/func_extension_base.py).

The `init`

method is a class method that's called by the worker when the extension class is imported. You can do initialization actions here for the extension. In this case, a hash map is initialized for recording the invocation start time for each function.

The `configure`

method is customer-facing. In your readme file, you can tell your customers when they need to call `Extension.configure()`

. The readme should also document the extension capabilities, possible configuration, and usage of your extension. In this example, customers can choose whether the elapsed time is reported in the `HttpResponse`

.

The `pre_invocation_app_level`

method is called by the Python worker before the function runs. It provides the information from the function, such as function context and arguments. In this example, the extension logs a message and records the start time of an invocation based on its invocation_id.

Similarly, the `post_invocation_app_level`

is called after function execution. This example calculates the elapsed time based on the start time and current time. It also overwrites the return value of the HTTP response.

### Create a readme.md

Create a readme.md file in the root of your extension project. This file contains the instructions and usage of your extension. The readme.md content is displayed as the description in the home page in your PyPI project.

```
# Python Worker Extension Timer
In this file, tell your customers when they need to call `Extension.configure()`.
The readme should also document the extension capabilities, possible configuration,
and usage of your extension.
```


## Consume your extension locally

Now that you've created an extension, you can use it in an app project to verify it works as intended.

### Create an HTTP trigger function

Create a new folder for your app project and navigate to it.

From the appropriate shell, such as Bash, run the following command to initialize the project:

`func init --python`

Use the following command to create a new HTTP trigger function that allows anonymous access:

`func new -t HttpTrigger -n HttpTrigger -a anonymous`


### Activate a virtual environment

Create a Python virtual environment, based on OS as follows:

Activate the Python virtual environment, based on OS as follows:


### Configure the extension

Install remote packages for your function app project using the following command:

`pip install -r requirements.txt`

Install the extension from your local file path, in editable mode as follows:

`pip install -e <PYTHON_WORKER_EXTENSION_ROOT>`

In this example, replace

`<PYTHON_WORKER_EXTENSION_ROOT>`

with the root file location of your extension project.When a customer uses your extension, they'll instead add your extension package location to the requirements.txt file, as in the following examples:

Open the local.settings.json project file and add the following field to

`Values`

:`"PYTHON_ENABLE_WORKER_EXTENSIONS": "1"`

When running in Azure, you instead add

`PYTHON_ENABLE_WORKER_EXTENSIONS=1`

to the[app settings in the function app](functions-how-to-use-azure-function-app-settings#settings).Add following two lines before the

`main`

function in*__init.py__*file for the v1 programming model, or in the*function_app.py*file for the v2 programming model:`from python_worker_extension_timer import TimerExtension TimerExtension.configure(append_to_http_response=True)`

This code imports the

`TimerExtension`

module and sets the`append_to_http_response`

configuration value.

### Verify the extension

From your app project root folder, start the function host using

`func host start --verbose`

. You should see the local endpoint of your function in the output as`https://localhost:7071/api/HttpTrigger`

.In the browser, send a GET request to

`https://localhost:7071/api/HttpTrigger`

. You should see a response like the following, with the**TimeElapsed**data for the request appended.`This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response. (TimeElapsed: 0.0009996891021728516 sec)`


## Publish your extension

After you've created and verified your extension, you still need to complete these remaining publishing tasks:

- Choose a license.
- Create a readme.md and other documentation.
- Publish the extension library to a Python package registry or a version control system (VCS).

To publish your extension to PyPI:

Run the following command to install

`twine`

and`wheel`

in your default Python environment or a virtual environment:`pip install twine wheel`

Remove the old

`dist/`

folder from your extension repository.Run the following command to generate a new package inside

`dist/`

:`python setup.py sdist bdist_wheel`

Run the following command to upload the package to PyPI:

`twine upload dist/*`

You may need to provide your PyPI account credentials during upload. You can also test your package upload with

`twine upload -r testpypi dist/*`

. For more information, see the[Twine documentation](https://twine.readthedocs.io/en/stable/).

After these steps, customers can use your extension by including your package name in their requirements.txt.

For more information, see the [official Python packaging tutorial](https://packaging.python.org/tutorials/packaging-projects/).

## Examples

You can view completed sample extension project from this article in the

[python_worker_extension_timer](https://github.com/Azure-Samples/python-worker-extension-timer)sample repository.OpenCensus integration is an open-source project that uses the extension interface to integrate telemetry tracing in Azure Functions Python apps. See the

[opencensus-python-extensions-azure](https://github.com/census-ecosystem/opencensus-python-extensions-azure/tree/main/extensions/functions)repository to review the implementation of this Python worker extension.

## Next steps

For more information about Azure Functions Python development, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-openai-assistantcreate-output -->

# Azure OpenAI assistant create output binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The Azure OpenAI extension for Azure Functions is currently in preview.

The Azure OpenAI assistant create output binding allows you to create a new assistant chat bot from your function code execution.

For information on setup and configuration details of the Azure OpenAI extension, see [Azure OpenAI extensions for Azure Functions](functions-bindings-openai). To learn more about Azure OpenAI assistants, see [Azure OpenAI Assistants API](/en-us/azure/ai-services/openai/concepts/assistants).

Note

References and examples are only provided for the [Node.js v4 model](functions-reference-node?pivots=nodejs-model-v4).

Note

References and examples are only provided for the [Python v2 model](functions-reference-python?pivots=python-mode-decorators#programming-model).

Note

While both C# process models are supported, only [isolated worker model](dotnet-isolated-process-guide) examples are provided.

## Example

This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
/// <summary>
/// HTTP PUT function that creates a new assistant chat bot with the specified ID.
/// </summary>
[Function(nameof(CreateAssistant))]
public static async Task<CreateChatBotOutput> CreateAssistant(
[HttpTrigger(AuthorizationLevel.Anonymous, "put", Route = "assistants/{assistantId}")] HttpRequestData req,
string assistantId)
{
string instructions =
"""
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
""";
using StreamReader reader = new(req.Body);
string request = await reader.ReadToEndAsync();
return new CreateChatBotOutput
{
HttpResponse = new ObjectResult(new { assistantId }) { StatusCode = 201 },
ChatBotCreateRequest = new AssistantCreateRequest(assistantId, instructions)
{
ChatStorageConnectionSetting = DefaultChatStorageConnectionSetting,
CollectionName = DefaultCollectionName,
},
};
}
public class CreateChatBotOutput
{
[AssistantCreateOutput()]
public AssistantCreateRequest? ChatBotCreateRequest { get; set; }
[HttpResult]
public IActionResult? HttpResponse { get; set; }
}
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
/**
* The default storage account setting for the table storage account.
* This constant is used to specify the connection string for the table storage
* account
* where chat data will be stored.
*/
final String DEFAULT_CHATSTORAGE = "AzureWebJobsStorage";
/**
* The default collection name for the table storage account.
* This constant is used to specify the collection name for the table storage
* account
* where chat data will be stored.
*/
final String DEFAULT_COLLECTION = "ChatState";
/*
* HTTP PUT function that creates a new assistant chat bot with the specified ID.
*/
@FunctionName("CreateAssistant")
public HttpResponseMessage createAssistant(
@HttpTrigger(
name = "req",
methods = {HttpMethod.PUT},
authLevel = AuthorizationLevel.ANONYMOUS,
route = "assistants/{assistantId}")
HttpRequestMessage<Optional<String>> request,
@BindingName("assistantId") String assistantId,
@AssistantCreate(name = "AssistantCreate") OutputBinding<AssistantCreateRequest> message,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
String instructions = "Don't make assumptions about what values to plug into functions.\n" +
"Ask for clarification if a user request is ambiguous.";
AssistantCreateRequest assistantCreateRequest = new AssistantCreateRequest(assistantId, instructions);
assistantCreateRequest.setChatStorageConnectionSetting(DEFAULT_CHATSTORAGE);
assistantCreateRequest.setCollectionName(DEFAULT_COLLECTION);
message.setValue(assistantCreateRequest);
JSONObject response = new JSONObject();
response.put("assistantId", assistantId);
return request.createResponseBuilder(HttpStatus.CREATED)
.header("Content-Type", "application/json")
.body(response.toString())
.build();
}
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
const { app, input, output } = require("@azure/functions");
const CHAT_STORAGE_CONNECTION_SETTING = "AzureWebJobsStorage";
const COLLECTION_NAME = "ChatState";
const chatBotCreateOutput = output.generic({
type: 'assistantCreate'
})
app.http('CreateAssistant', {
methods: ['PUT'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraOutputs: [chatBotCreateOutput],
handler: async (request, context) => {
const assistantId = request.params.assistantId
const instructions =
`
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
`
const createRequest = {
id: assistantId,
instructions: instructions,
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
}
context.extraOutputs.set(chatBotCreateOutput, createRequest)
return { status: 202, jsonBody: { assistantId: assistantId } }
}
})
```


```
import { HttpRequest, InvocationContext, app, input, output } from "@azure/functions"
const CHAT_STORAGE_CONNECTION_SETTING = "AzureWebJobsStorage";
const COLLECTION_NAME = "ChatState";
const chatBotCreateOutput = output.generic({
type: 'assistantCreate'
})
app.http('CreateAssistant', {
methods: ['PUT'],
route: 'assistants/{assistantId}',
authLevel: 'anonymous',
extraOutputs: [chatBotCreateOutput],
handler: async (request: HttpRequest, context: InvocationContext) => {
const assistantId = request.params.assistantId
const instructions =
`
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
`
const createRequest = {
id: assistantId,
instructions: instructions,
chatStorageConnectionSetting: CHAT_STORAGE_CONNECTION_SETTING,
collectionName: COLLECTION_NAME
}
context.extraOutputs.set(chatBotCreateOutput, createRequest)
return { status: 202, jsonBody: { assistantId: assistantId } }
}
})
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

Here's the *function.json* file for Create Assistant:

```
{
"bindings": [
{
"authLevel": "function",
"type": "httpTrigger",
"direction": "in",
"name": "Request",
"route": "assistants/{assistantId}",
"methods": [
"put"
]
},
{
"type": "http",
"direction": "out",
"name": "Response"
},
{
"type": "assistantCreate",
"direction": "out",
"dataType": "string",
"name": "Requests"
}
]
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

{{This comes from the example code comment}}

```
using namespace System.Net
param($Request, $TriggerMetadata)
$assistantId = $Request.params.assistantId
$instructions = "Don't make assumptions about what values to plug into functions."
$instructions += "\nAsk for clarification if a user request is ambiguous."
$create_request = @{
"id" = $assistantId
"instructions" = $instructions
"chatStorageConnectionSetting" = "AzureWebJobsStorage"
"collectionName" = "ChatState"
}
Push-OutputBinding -Name Requests -Value (ConvertTo-Json $create_request)
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = [HttpStatusCode]::Accepted
Body = (ConvertTo-Json @{ "assistantId" = $assistantId})
Headers = @{
"Content-Type" = "application/json"
}
})
```


This example demonstrates the creation process, where the HTTP PUT function that creates a new assistant chat bot with the specified ID. The response to the prompt is returned in the HTTP response.

```
DEFAULT_CHAT_STORAGE_SETTING = "AzureWebJobsStorage"
DEFAULT_CHAT_COLLECTION_NAME = "ChatState"
@apis.function_name("CreateAssistant")
@apis.route(route="assistants/{assistantId}", methods=["PUT"])
@apis.assistant_create_output(arg_name="requests")
def create_assistant(
req: func.HttpRequest, requests: func.Out[str]
) -> func.HttpResponse:
assistantId = req.route_params.get("assistantId")
instructions = """
Don't make assumptions about what values to plug into functions.
Ask for clarification if a user request is ambiguous.
"""
create_request = {
"id": assistantId,
"instructions": instructions,
"chatStorageConnectionSetting": DEFAULT_CHAT_STORAGE_SETTING,
"collectionName": DEFAULT_CHAT_COLLECTION_NAME,
}
requests.set(json.dumps(create_request))
response_json = {"assistantId": assistantId}
return func.HttpResponse(
json.dumps(response_json), status_code=202, mimetype="application/json"
)
```


## Attributes

Apply the `CreateAssistant`

attribute to define an assistant create output binding, which supports these parameters:

| Parameter | Description |
|---|---|
Id |
The identifier of the assistant to create. |
Instructions |
Optional. The instructions that are provided to assistant to follow. |
ChatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
CollectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Annotations

The `CreateAssistant`

annotation enables you to define an assistant create output binding, which supports these parameters:

| Element | Description |
|---|---|
name |
Gets or sets the name of the output binding. |
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Decorators

During the preview, define the output binding as a `generic_output_binding`

binding of type `createAssistant`

, which supports these parameters:

| Parameter | Description |
|---|---|
arg_name |
The name of the variable that represents the binding parameter. |
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chat_storage_connection_setting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collection_name |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Configuration

The binding supports these configuration properties that you set in the function.json file.

| Property | Description |
|---|---|
type |
Must be `CreateAssistant` . |
direction |
Must be `out` . |
name |
The name of the output binding. |
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Configuration

The binding supports these properties, which are defined in your code:

| Property | Description |
|---|---|
id |
The identifier of the assistant to create. |
instructions |
Optional. The instructions that are provided to assistant to follow. |
chatStorageConnectionSetting |
Optional. The configuration section name for the table settings for chat storage. The default value is `AzureWebJobsStorage` . |
collectionName |
Optional. The table collection name for chat storage. The default value is `ChatState` . |

## Usage

See the [Example section](#example) for complete examples.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-queue-trigger -->

# Azure Queue storage trigger for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The queue storage trigger runs a function as messages are added to Azure Queue storage.

Azure Queue storage scaling decisions for the Consumption and Premium plans are done via target-based scaling. For more information, see [Target-based scaling](functions-target-based-scaling).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

## Example

Use the queue trigger to start a function when a new item is received on a queue. The queue message is provided as input to the function.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a [C# function](dotnet-isolated-process-guide) that polls the `input-queue`

queue and writes several messages to an output queue each time a queue item is processed.

```
[Function(nameof(QueueInputOutputFunction))]
[QueueOutput("output-queue")]
public string[] QueueInputOutputFunction([QueueTrigger("input-queue")] Album myQueueItem, FunctionContext context)
{
// Use a string array to return more than one message.
string[] messages = {
$"Album name = {myQueueItem.Name}",
$"Album songs = {myQueueItem.Songs}"};
_logger.LogInformation("{msg1},{msg2}", messages[0], messages[1]);
// Queue Output messages
return messages;
}
```


The following Java example shows a storage queue trigger function, which logs the triggered message placed into queue `myqueuename`

.

```
@FunctionName("queueprocessor")
public void run(
@QueueTrigger(name = "msg",
queueName = "myqueuename",
connection = "myconnvarname") String message,
final ExecutionContext context
) {
context.getLogger().info(message);
}
```


The following example shows a queue trigger [TypeScript function](functions-reference-node?tabs=typescript). The function polls the `myqueue-items`

queue and writes a log each time a queue item is processed.

```
import { app, InvocationContext } from '@azure/functions';
export async function storageQueueTrigger1(queueItem: unknown, context: InvocationContext): Promise<void> {
context.log('Storage queue function processed work item:', queueItem);
context.log('expirationTime =', context.triggerMetadata.expirationTime);
context.log('insertionTime =', context.triggerMetadata.insertionTime);
context.log('nextVisibleTime =', context.triggerMetadata.nextVisibleTime);
context.log('id =', context.triggerMetadata.id);
context.log('popReceipt =', context.triggerMetadata.popReceipt);
context.log('dequeueCount =', context.triggerMetadata.dequeueCount);
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
handler: storageQueueTrigger1,
});
```


The [usage](#usage) section explains `queueItem`

. The [message metadata section](#message-metadata) explains all of the other variables shown.

The following example shows a queue trigger [JavaScript function](functions-reference-node). The function polls the `myqueue-items`

queue and writes a log each time a queue item is processed.

```
const { app } = require('@azure/functions');
app.storageQueue('storageQueueTrigger1', {
queueName: 'myqueue-items',
connection: 'MyStorageConnectionAppSetting',
handler: (queueItem, context) => {
context.log('Storage queue function processed work item:', queueItem);
context.log('expirationTime =', context.triggerMetadata.expirationTime);
context.log('insertionTime =', context.triggerMetadata.insertionTime);
context.log('nextVisibleTime =', context.triggerMetadata.nextVisibleTime);
context.log('id =', context.triggerMetadata.id);
context.log('popReceipt =', context.triggerMetadata.popReceipt);
context.log('dequeueCount =', context.triggerMetadata.dequeueCount);
},
});
```


The [usage](#usage) section explains `queueItem`

. The [message metadata section](#message-metadata) explains all of the other variables shown.

The following example demonstrates how to read a queue message passed to a function via a trigger.

A Storage queue trigger is defined in *function.json* file where `type`

is set to `queueTrigger`

.

```
{
"bindings": [
{
"name": "QueueItem",
"type": "queueTrigger",
"direction": "in",
"queueName": "messages",
"connection": "MyStorageConnectionAppSetting"
}
]
}
```


The code in the *Run.ps1* file declares a parameter as `$QueueItem`

, which allows you to read the queue message in your function.

```
# Input bindings are passed in via param block.
param([string] $QueueItem, $TriggerMetadata)
# Write out the queue message and metadata to the information log.
Write-Host "PowerShell queue trigger function processed work item: $QueueItem"
Write-Host "Queue item expiration time: $($TriggerMetadata.ExpirationTime)"
Write-Host "Queue item insertion time: $($TriggerMetadata.InsertionTime)"
Write-Host "Queue item next visible time: $($TriggerMetadata.NextVisibleTime)"
Write-Host "ID: $($TriggerMetadata.Id)"
Write-Host "Pop receipt: $($TriggerMetadata.PopReceipt)"
Write-Host "Dequeue count: $($TriggerMetadata.DequeueCount)"
```


The following example demonstrates how to read a queue message passed to a function via a trigger. The example depends on whether you use the v1 or v2 Python programming model.

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="QueueFunc")
@app.queue_trigger(arg_name="msg", queue_name="inputqueue",
connection="storageAccountConnectionString") # Queue trigger
@app.queue_output(arg_name="outputQueueItem", queue_name="outqueue",
connection="storageAccountConnectionString") # Queue output binding
def test_function(msg: func.QueueMessage,
outputQueueItem: func.Out[str]) -> None:
logging.info('Python queue trigger function processed a queue item: %s',
msg.get_body().decode('utf-8'))
outputQueueItem.set('hello')
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use the [QueueTriggerAttribute](https://github.com/Azure/azure-webjobs-sdk/blob/master/src/Microsoft.Azure.WebJobs.Extensions.Storage/Queues/QueueTriggerAttribute.cs) to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#queue-trigger).

In [C# class libraries](dotnet-isolated-process-guide), the attribute's constructor takes the name of the queue to monitor, as shown in the following example:

```
[Function(nameof(QueueInputOutputFunction))]
[QueueOutput("output-queue")]
public string[] QueueInputOutputFunction([QueueTrigger("input-queue")] Album myQueueItem, FunctionContext context)
```


This example also demonstrates setting the [connection string setting](#connections) in the attribute itself.

## Annotations

The `QueueTrigger`

annotation gives you access to the queue that triggers the function. The following example makes the queue message available to the function via the `message`

parameter.

```
package com.function;
import com.microsoft.azure.functions.annotation.*;
import java.util.Queue;
import com.microsoft.azure.functions.*;
public class QueueTriggerDemo {
@FunctionName("QueueTriggerDemo")
public void run(
@QueueTrigger(name = "message", queueName = "messages", connection = "MyStorageConnectionAppSetting") String message,
final ExecutionContext context
) {
context.getLogger().info("Queue message: " + message);
}
}
```


| Property | Description |
|---|---|
`name` |
Declares the parameter name in the function signature. When the function is triggered, this parameter's value has the contents of the queue message. |
`queueName` |
Declares the queue name in the storage account. |
`connection` |
Points to the storage account connection string. |

## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using decorators, the following properties on the `queue_trigger`

decorator define the Queue Storage trigger:

| Property | Description |
|---|---|
`arg_name` |
Declares the parameter name in the function signature. When the function is triggered, this parameter's value has the contents of the queue message. |
`queue_name` |
Declares the queue name in the storage account. |
`connection` |
Points to the storage account connection string. |

For Python functions defined by using function.json, see the Configuration section.

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the properties that you can set on the `options`

object passed to the `app.storageQueue()`

method.

| Property | Description |
|---|---|
queueName |
The name of the queue to poll. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Queues. See
|

The following table explains the binding configuration properties that you set in the *function.json* file and the `QueueTrigger`

attribute.

| function.json property | Description |
|---|---|
type |
Must be set to `queueTrigger` . This property is set automatically when you create the trigger in the Azure portal. |
direction |
In the function.json file only. Must be set to `in` . This property is set automatically when you create the trigger in the Azure portal. |
name |
The name of the variable that contains the queue item payload in the function code. |
queueName |
The name of the queue to poll. |
connection |
The name of an app setting or setting collection that specifies how to connect to Azure Queues. See
|

See the [Example section](#example) for complete examples.

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Usage

Note

Functions expect a *base64* encoded string. Any adjustments to the encoding type (in order to prepare data as a *base64* encoded string) need to be implemented in the calling service.

The usage of the Queue trigger depends on the extension package version, and the C# modality used in your function app, which can be one of these modes:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see usage details for the mode and version.

The queue trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The message content as a string. Use when the message is simple text.. |
`byte[]` |
The bytes of the message. |
| JSON serializable types | When a queue message contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BinaryData](/en-us/dotnet/api/system.binarydata)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues 5.2.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues/5.2.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

The [QueueTrigger](/en-us/java/api/com.microsoft.azure.functions.annotation.queuetrigger) annotation gives you access to the queue message that triggered the function.

Access the queue message via string parameter that matches the name designated by binding's `name`

parameter in the *function.json* file.

Access the queue message via the parameter typed as [QueueMessage](/en-us/python/api/azure-functions/azure.functions.queuemessage).

## Metadata

The queue trigger provides several [metadata properties](functions-bindings-expressions-patterns#trigger-metadata). These properties can be used as part of binding expressions in other bindings or as parameters in your code, for language workers that provide this access to message metadata.

The message metadata properties are members of the [CloudQueueMessage](/en-us/dotnet/api/microsoft.azure.storage.queue.cloudqueuemessage) class.

The message metadata properties can be accessed from `context.triggerMetadata`

.

The message metadata properties can be accessed from the passed `$TriggerMetadata`

parameter.

| Property | Type | Description |
|---|---|---|
`QueueTrigger` |
`string` |
Queue payload (if a valid string). If the queue message payload is a string, `QueueTrigger` has the same value as the variable named by the `name` property in function.json. |
`DequeueCount` |
`long` |
The number of times this message has been dequeued. |
`ExpirationTime` |
`DateTimeOffset` |
The time that the message expires. |
`Id` |
`string` |
Queue message ID. |
`InsertionTime` |
`DateTimeOffset` |
The time that the message was added to the queue. |
`NextVisibleTime` |
`DateTimeOffset` |
The time that the message will next be visible. |
`PopReceipt` |
`string` |
The message's pop receipt. |

The following message metadata properties can be accessed from the passed binding parameter (`msg`

in previous [examples](#example)).

| Property | Description |
|---|---|
`body` |
Queue payload as a string. |
`dequeue_count` |
The number of times this message has been dequeued. |
`expiration_time` |
The time that the message expires. |
`id` |
Queue message ID. |
`insertion_time` |
The time that the message was added to the queue. |
`time_next_visible` |
The time that the message will next be visible. |
`pop_receipt` |
The message's pop receipt. |

## Connections

The `connection`

property is a reference to environment configuration that specifies how the app should connect to Azure Queues. It may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

To obtain a connection string, follow the steps shown at [Manage storage account access keys](../storage/common/storage-account-keys-manage).

This connection string should be stored in an application setting with a name matching the value specified by the `connection`

property of the binding configuration.

If the app setting name begins with "AzureWebJobs", you can specify only the remainder of the name here. For example, if you set `connection`

to "MyStorage", the Functions runtime looks for an app setting that is named "AzureWebJobsMyStorage." If you leave `connection`

empty, the Functions runtime uses the default Storage connection string in the app setting that is named `AzureWebJobsStorage`

.

### Identity-based connections

If you're using [version 5.x or higher of the extension](functions-bindings-storage-queue#storage-extension-5x-and-higher) ([bundle 3.x or higher](functions-bindings-storage-queue?tabs=extensionv3#install-bundle) for non-.NET language stacks), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To use an identity, you define settings under a common prefix that maps to the `connection`

property in the trigger and binding configuration.

If you're setting `connection`

to "AzureWebJobsStorage", see [Connecting to host storage with an identity](functions-reference#connecting-to-host-storage-with-an-identity). For all other connections, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Queue Service URI | `<CONNECTION_NAME_PREFIX>__queueServiceUri` 1 |
The data plane URI of the queue service to which you're connecting, using the HTTPS scheme. | https://<storage_account_name>.queue.core.windows.net |

1 `<CONNECTION_NAME_PREFIX>__serviceUri`

can be used as an alias. If both forms are provided, the `queueServiceUri`

form is used. The `serviceUri`

form can't be used when the overall connection configuration is to be used across blobs, queues, and/or tables.

Other properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

You will need to create a role assignment that provides access to your queue at runtime. Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Queue Storage extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles |
|---|---|
| Trigger |
|

[Storage Queue Data Contributor](../role-based-access-control/built-in-roles#storage-queue-data-contributor),[Storage Queue Data Message Sender](../role-based-access-control/built-in-roles#storage-queue-data-message-sender)## Poison messages

When a queue trigger function fails, Azure Functions retries the function up to five times for a given queue message, including the first try. If all five attempts fail, the functions runtime adds a message to a queue named *<originalqueuename>-poison*. You can write a function to process messages from the poison queue by logging them or sending a notification that manual attention is needed.

To handle poison messages manually, check the [dequeueCount](#message-metadata) of the queue message.

## Peek lock

The peek-lock pattern happens automatically for queue triggers, using the visibility mechanics provided by the storage service. As messages are dequeued by the triggered function, they're marked as invisible. Execution of a queue triggered function can have one of these results on message in the queue:

- Function execution completes successfully and the message is deleted from the queue.
- Function execution fails and the Functions host updates the visibility of the message based on the
`visibilityTimeout`

[setting in the host.json file](functions-bindings-storage-queue#host-json). The default visibility timeout is zero, which means that the message immediately reappears in the queue for reprocessing. Use the`visibilityTimeout`

setting to delay the reprocessing of messages that fail to process. This timeout setting applies to all queue triggered functions in the function app. - The Functions host crashes during function execution. When this uncommon event occurs, the host can't apply the
`visibilityTimeout`

to the message being processed. Instead, the message is left with the default 10 minute timeout set by the storage service. After 10 minutes, the message reappears in the queue for reprocessing. This service-defined default timeout can't be changed.

## Polling algorithm

The queue trigger implements a random exponential back-off algorithm to reduce the effect of idle-queue polling on storage transaction costs.

The algorithm uses the following logic:

- When a message is found, the runtime waits 100 milliseconds and then checks for another message.
- When no message is found, it waits about 200 milliseconds before trying again.
- After subsequent failed attempts to get a queue message, the wait time continues to increase until it reaches the maximum wait time, which defaults to one minute.
- The maximum wait time is configurable via the
`maxPollingInterval`

property in the[host.json file](functions-host-json-v1#queues).

During local development, the maximum polling interval defaults to two seconds.

Note

In regards to billing when hosting function apps in the Consumption plan, you are not charged for time spent polling by the runtime.

## Concurrency

When there are multiple queue messages waiting, the queue trigger retrieves a batch of messages and invokes function instances concurrently to process them. By default, the batch size is 16. When the number being processed gets down to 8, the runtime gets another batch and starts processing those messages. So the maximum number of concurrent messages being processed per function on one virtual machine (VM) is 24. This limit applies separately to each queue-triggered function on each VM. If your function app scales out to multiple VMs, each VM waits for triggers and attempt to run functions. For example, if a function app scales out to 3 VMs, the default maximum number of concurrent instances of one queue-triggered function is 72.

The batch size and the threshold for getting a new batch are configurable in the [host.json file](functions-host-json#queues). If you want to minimize parallel execution for queue-triggered functions in a function app, you can set the batch size to 1. This setting eliminates concurrency only so long as your function app runs on a single virtual machine (VM).

The queue trigger automatically prevents a function from processing a queue message multiple times simultaneously.

## host.json properties

The host.json file contains settings that control queue trigger behavior. See the [host.json settings](functions-bindings-storage-queue#host-json) section for details regarding available settings.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/flex-consumption-site-updates -->

# Site update strategies in Flex Consumption

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you host your app with Azure Functions in the [Flex Consumption plan](flex-consumption-plan), you can control how updates are deployed to running instances. A site update occurs whenever you deploy code, modify application settings, or change other configuration properties. The Flex Consumption plan provides a site configuration setting (`SiteUpdateStrategy`

) that you can use to control whether your function app experiences downtime during these updates and how in-progress executions are handled.

The Flex Consumption plan currently supports these update strategies:

**Recreate**: Functions restarts all running instances after replacing your code with the latest version. This approach might cause brief downtime while instances are recycled and preserves the default behavior from other Azure Functions hosting plans.**Rolling update**(preview): Provides zero-downtime deployments by draining and replacing instances in batches. In-progress executions complete naturally without forced termination.

Important

The rolling update strategy is currently in preview and isn't recommended for production apps. Review the current [limitations and considerations](flex-consumption-site-updates#rolling-update-strategy-considerations) before enabling this strategy in any production app.

## Strategy comparison

This table compares the two site update strategies:

| Consideration | Recreate | Rolling update |
|---|---|---|
| Downtime | Brief downtime as your app scales out from zero after the restart | No period of downtime |
| In-progress executions | Forcefully terminated | Allowed to complete within the
|

✔ Brief downtime is acceptable.

✔ You're deploying breaking changes and need a clean restart.

✔ Your functions are stateless and can handle interruptions.

✔ You have long-running or critical functions that can't be interrupted.

✔ Your changes are backward-compatible.

✔ You must preserve in-progress executions.

## Update strategy behaviors

This table compares the update process of the two strategies:

**Recreate strategy**:

**Rolling update strategy**:

- A site update (code or configuration changes) is applied to your function app.
- The recreate strategy is triggered to update running instances with the new changes.
- The platform forcefully restarts all live and draining instances.
- The scaling system immediately begins provisioning new instances with the updated version (original instances might still be deprovisioning in the background).

- A site update (code or configuration changes) is applied to your function app.
- The rolling update strategy is triggered to update running instances with the new changes.
- The platform assigns all live instances to batches.
- At regular intervals, the platform drains one batch of instances. Draining prevents instances from accepting new events while allowing in-progress executions to complete (up to the one hour maximum execution time).
- Simultaneously, the scaling platform provisions new instances running the updated version to replace the draining capacity.
- This process continues until all live instances are running the updated version.

This table compares the key characteristics of the two strategies:

**Recreate strategy**:

**Rolling update strategy**:

**Brief downtime**: Your app is unavailable while instances restart and scale out**Execution interruption**: In-progress executions are terminated immediately**No completion signal**: Monitor instance logs to track when original instances stop emitting logs

**Zero downtime**: deployments are done in batches so that executions complete without forced termination.**Asynchronous operations**: Draining and scale-out happen simultaneously without waiting for each other to complete. The scale-out isn't guaranteed to occur before the next drain interval.**Overlapping updates**: You can initiate additional rolling updates while one is in progress. All non-latest instances are drained, and only the newest version is scaled out.**Dynamic scaling**: The platform adjusts instance count based on current demand during the update.**Platform managed capacity**: When demand increases, the platform provisions more instances than it drains. When demand decreases, it creates only the necessary instances to meet current needs. This approach ensures continuous availability while optimizing resource usage.

## Rolling update strategy considerations

Keep these current behaviors and limitations in mind when using the rolling update strategy. This list is maintained during the preview period and could change as the feature approaches general availability (GA).

**Platform-managed parameters**: The platform controls the parameters (such as batch count, instances per batch, number of batches, and drain intervals) that determine rolling update behaviors. These parameters might change before GA to optimize performance and reliability.**No real-time monitoring**: There's currently no visibility into how many instances are draining, how many batches remain, or current progress percentages.**No completion signal**: However, you can monitor instance logs to estimate when an update completes.**Single-instance scenarios**: Apps running on one instance experience brief downtime similar to recreate, though in-progress executions still complete.**Durable Functions**: Because mixing versions during updates can cause unexpected behavior in a Durable orchestration, use an explicit[orchestration version match strategy](durable/durable-functions-orchestration-versioning).**Infrastructure as Code**: Deploying code and configuration changes together triggers multiple rolling updates that might overlap.**Backward compatibility**: Make sure that your changes work with the previous version during the rolling update transition period.

## Configure your update strategy

You can set the update strategy for your app using the `SiteUpdateStrategy`

site setting, which is a child of `functionAppConfig`

. By default, `SiteUpdateStrategy.type`

is set to `Recreate`

. Currently, only Bicep and ARM templates with API version `2023-12-01`

or later support changing this property.

```
functionAppConfig: {
...
siteUpdateStrategy: {
type: 'RollingUpdate'
}
...
}
```


Changes to the site update strategy take effect at the next site update. For example, changing `type`

from `Recreate`

to `RollingUpdate`

uses the recreate strategy for that update. All subsequent site updates then use rolling updates.

## Monitoring site updates

During the public preview, there's no built-in completion signal for site updates. You can use KQL queries in Application Insights as a best-effort approach to estimate rolling update progress.

### Monitoring rolling update progress

These KQL queries provide a best-effort estimate of rolling update progress by tracking instance turnover in Application Insights logs. This approach has significant limitations and shouldn't be relied upon for production automation:

```
// Rolling update completion check
let deploymentStart = datetime('2025-10-30T19:00:00Z'); // Set to your deployment start time
let checkInterval = 10s; // How often you run this query
let buffer = 30s; // Safety buffer for instance detection
//
// Get original instances (active before deployment)
let originalInstances =
traces
| where timestamp between ((deploymentStart - buffer) .. deploymentStart)
| where cloud_RoleInstance != ""
| summarize by InstanceId = cloud_RoleInstance;
//
// Get currently active instances
let currentInstances =
traces
| where timestamp >= now() - checkInterval
| where cloud_RoleInstance != ""
| summarize by InstanceId = cloud_RoleInstance;
//
// Check completion status
currentInstances
| join kind=leftouter (originalInstances | extend IsOriginal = true) on InstanceId
| extend IsOriginal = isnotnull(IsOriginal)
| summarize
OriginalStillActiveInstances = make_set_if(InstanceId, IsOriginal),
NewInstances = make_set_if(InstanceId, not(IsOriginal)),
OriginalStillActiveCount = countif(IsOriginal),
NewCount = countif(not(IsOriginal)),
TotalOriginal = toscalar(originalInstances | count)
| extend
RollingUpdateComplete = iff(OriginalStillActiveCount == 0, "YES", "NO"),
PercentComplete = round(100.0 * (1.0 - todouble(OriginalStillActiveCount) / todouble(TotalOriginal)), 1)
| project RollingUpdateComplete, PercentComplete, OriginalStillActiveCount, NewCount
```


How to use this query for estimation:

- Paste this query in the Logs blade of the Application Insights resource associated with your function app.
- Set
`deploymentStart`

to the timestamp when your site update returns success. - Run the query periodically to estimate progress. Set the polling interval to be at least as long as your average function execution time, and ensure the
`checkInterval`

variable in the query matches this polling frequency. - The query returns approximate values:
`RollingUpdateComplete`

: Best estimate of whether all original instances are replaced`PercentComplete`

: Estimated percentage of original instances that are replaced`OriginalStillActiveCount`

: Estimated number of original instances still running`NewCount`

: Number of new instances currently active


Keep these limitations in mind when using these queries:

**Timing gap**: The`deploymentStart`

time represents when your site update returns success, but the actual rolling update might not start immediately. During this gap, any scale-out events provision instances running the original version. Since the query only tracks instances active at`deploymentStart`

, it doesn't monitor these new original-version instances, potentially causing false completion signals.**Log-based detection**: This approach relies on application logs to infer instance state rather than directly querying instance status. Instances might be running but not actively logging, leading to false completion signals when original instances are still active but didn't emit logs within the`checkInterval`

window.

**Recommendation for production**: Use rolling updates when zero-downtime deployments are critical. Ensure your deployment pipelines don't require waiting for update completion before proceeding to subsequent steps. Use recreate when you need faster, more predictable update timing and can tolerate brief downtime.

## FAQ

**I'm used to deployment slots for zero downtime deployments. How do rolling updates differ?**

- Unlike deployment slots, rolling updates require no additional infrastructure. Set
`siteUpdateStrategy.type`

to`"RollingUpdate"`

for zero-downtime deployments. - Rolling updates preserve in-progress executions, while deployment slots terminate them during swaps.
[Certain site properties](functions-deployment-slots#manage-settings)and sticky settings can't be swapped and require modifying the production slot directly. - Unlike deployment slots, rolling updates don't provide a separate environment for you to canary test changes or route a percentage of live traffic to. If you need these features, use a plan that supports deployment slots, like Elastic Premium, or manage separate Flex Consumption apps behind a traffic manager.

**How do I roll back a site update?**

- There's currently no feature to roll back a site update. If a rollback is necessary, initiate another site update with the previous state of code or configuration.

**How are timer triggers handled?**

- Timer triggers maintain their singleton nature. Once a timer-triggered function app is marked for drain, new timer functions run on the latest version.

**I'm seeing runtime errors during the rolling update...what went wrong?**

- If new instances fail to start or encounter runtime errors, the issue is likely in the application code, dependencies, configuration settings, or environment variables that you modified.
- To resolve the issue, redeploy your last known healthy version to restore the runtime. Then test your proposed changes in a development or staging environment before reattempting. Review error logs to identify what specific change caused the issue.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-integrate-storage-queue-output-binding -->

# Add messages to an Azure Storage queue using Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Functions, input and output bindings provide a declarative way to make data from external services available to your code. In this article, you use an output binding to create a message in a queue when an HTTP request triggers a function. You use Azure storage container to view the queue messages that your function creates.

## Prerequisites

An Azure subscription. If you don't have one, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.Follow the directions in

[Create your first function in the Azure portal](functions-create-function-app-portal), omitting the**Clean up resources**step, to create the function app and function to use in this article.

## Add an output binding

In this section, you use the portal UI to add an Azure Queue Storage output binding to the function you created in the prerequisites. This binding makes it possible to write minimal code to create a message in a queue. You don't need to write code for such tasks as opening a storage connection, creating a queue, or getting a reference to a queue. The Azure Functions runtime and queue output binding take care of those tasks for you.

In the Azure portal, search for and select the function app that you created in

[Create your first function from the Azure portal](functions-get-started).In your function app, select the function that you created.

Select

**Integration**, and then select**+ Add output**.Select the

**Azure Queue Storage**binding type and add the settings as specified in the table that follows this screenshot:Setting Suggested value description **Message parameter name**outputQueueItem The name of the output binding parameter. **Queue name**outqueue The name of the queue to connect to in your storage account. **Storage account connection**AzureWebJobsStorage You can use the existing storage account connection used by your function app or create a new one. Select

**OK**to add the binding.

Now that you have an output binding defined, you need to update the code to use the binding to add messages to a queue.

## Add code that uses the output binding

In this section, you add code that writes a message to the output queue. The message includes the value passed to the HTTP trigger in the query string. For example, if the query string includes `name=Azure`

, the queue message is *Name passed to the function: Azure*.

In your function, select

**Code + Test**to display the function code in the editor.Update the function code, according to your function language:

Add an

**outputQueueItem**parameter to the method signature as shown in the following example:`public static async Task<IActionResult> Run(HttpRequest req, ICollector<string> outputQueueItem, ILogger log) { ... }`

In the body of the function, just before the

`return`

statement, add code that uses the parameter to create a queue message:`outputQueueItem.Add("Name passed to the function: " + name);`

Select

**Save**to save your changes.

## Test the function

After the code changes are saved, select

**Test**.Confirm that your test matches this screenshot, and then select

**Run**.Notice that the

**Request body**contains the`name`

value*Azure*. This value appears in the queue message created when the function is invoked.As an alternative to selecting

**Run**, you can call the function by entering a URL in a browser and specifying the`name`

value in the query string. This browser method is shown in[Create your first function from the Azure portal](functions-get-started).Check the logs to make sure that the function succeeded.

A new queue named

**outqueue**is created in your storage account by the Functions runtime when the output binding is first used. You use storage account to verify that the queue and a message in it were created.

### Find the storage account connected to AzureWebJobsStorage

In your function app, expand

**Settings**, and then select**Environment variables**.In the

**App settings**tab, select**AzureWebJobsStorage**.Locate and make note of the account name.


### Examine the output queue

In the resource group for your function app, select the storage account that you're using.

Under

**Queue service**, select**Queues**, and select the queue named**outqueue**.The queue contains the message that the queue output binding created when you ran the HTTP-triggered function. If you invoked the function with the default

`name`

value of*Azure*, the queue message is*Name passed to the function: Azure*.Run the function again.

A new message appears in the queue.


## Clean up resources

In the preceding steps, you created Azure resources in a resource group. If you don't expect to need these resources in the future, you can delete them by deleting the resource group:

From the Azure portal menu or home page, select

**Resource groups**>**myResourceGroup**.On the

**myResourceGroup**pane, make sure that the listed resources are the ones you want to delete.Select

**Delete resource group**. Type**myResourceGroup**in the text box to confirm, and then select**Delete**.

## Related content

In this article, you added an output binding to an existing function. For more information about binding to Queue Storage, see [Queue Storage trigger and bindings](functions-bindings-storage-queue).

[Azure Functions triggers and bindings concepts](functions-triggers-bindings)

Learn how Functions integrates with other services.[Azure Functions developer reference](functions-reference)

Provides more technical information about the Functions runtime and a reference for coding functions and defining triggers and bindings.[Code and test Azure Functions locally](functions-develop-local)

Describes the options for developing your functions locally.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-java-gradle -->

# Use Java and Gradle to create and publish a function to Azure

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to build and publish a Java function project to Azure Functions with the Gradle command-line tool. When you're done, your function code runs in Azure in a [serverless hosting plan](consumption-plan) and is triggered by an HTTP request.

Note

If Gradle is not your preferred development tool, check out our similar tutorials for Java developers using [Maven](how-to-create-function-azure-cli?pivots=programming-language-java), [IntelliJ IDEA](/en-us/azure/developer/java/toolkit-for-intellij/quickstart-functions) and [VS Code](how-to-create-function-vs-code?pivot=programming-language-java).

## Prerequisites

To develop functions using Java, you must have the following installed:

[Java Developer Kit](/en-us/azure/developer/java/fundamentals/java-support-on-azure), version 8, 11, 17 or 21. (Java 21 is currently supported on Linux only)[Azure CLI](/en-us/cli/azure)[Azure Functions Core Tools](functions-run-local#v2)version 2.6.666 or above[Gradle](https://gradle.org/), version 6.8 and above

You also need an active Azure subscription. If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) before you begin.

Important

The JAVA_HOME environment variable must be set to the install location of the JDK to complete this quickstart.

## Prepare a Functions project

Use the following command to clone the sample project:

```
git clone https://github.com/Azure-Samples/azure-functions-samples-java.git
cd azure-functions-samples-java/triggers-bindings
```


Open `build.gradle`

and change the `appName`

in the following section to a unique name to avoid domain name conflict when deploying to Azure.

```
azurefunctions {
resourceGroup = 'java-functions-group'
appName = 'azure-functions-sample-demo'
pricingTier = 'Consumption'
region = 'westus'
runtime {
os = 'windows'
}
localDebug = "transport=dt_socket,server=y,suspend=n,address=5005"
}
```


Open the new Function.java file from the *src/main/java* path in a text editor and review the generated code. This code is an [HTTP triggered](functions-bindings-http-webhook) function that echoes the body of the request.

## Run the function locally

Run the following command to build then run the function project:

```
gradle jar --info
gradle azureFunctionsRun
```


You see output like the following from Azure Functions Core Tools when you run the project locally:

... Now listening on: http://0.0.0.0:7071 Application started. Press Ctrl+C to shut down. Http Functions: HttpExample: [GET,POST] http://localhost:7071/api/HttpExample ...

Trigger the function from the command line using the following cURL command in a new terminal window:

```
curl -w "\n" http://localhost:7071/api/HttpExample --data AzureFunctions
```


The expected output is the following:

Hello, AzureFunctions

Note

If you set authLevel to `FUNCTION`

or `ADMIN`

, the [access key](function-keys-how-to) isn't required when running locally.

Use `Ctrl+C`

in the terminal to stop the function code.

## Deploy the function to Azure

A function app and related resources are created in Azure when you first deploy your function app. Before you can deploy, use the [az login](/en-us/cli/azure/authenticate-azure-cli) Azure CLI command to sign in to your Azure subscription.

```
az login
```


Tip

If your account can access multiple subscriptions, use [az account set](/en-us/cli/azure/account#az-account-set) to set the default subscription for this session.

Use the following command to deploy your project to a new function app.

```
gradle azureFunctionsDeploy
```


This creates the following resources in Azure, based on the values in the build.gradle file:

- Resource group. Named with the
*resourceGroup*you supplied. - Storage account. Required by Functions. The name is generated randomly based on Storage account name requirements.
- App Service plan. Serverless Consumption plan hosting for your function app in the specified
*region*. The name is generated randomly. - Function app. A function app is the deployment and execution unit for your functions. The name is your
*appName*, appended with a randomly generated number.

The deployment also packages the project files and deploys them to the new function app using [zip deployment](functions-deployment-technologies#zip-deploy), with run-from-package mode enabled.

The authLevel for HTTP Trigger in sample project is `ANONYMOUS`

, which will skip the authentication. However, if you use other authLevel like `FUNCTION`

or `ADMIN`

, you need to get the function key to call the function endpoint over HTTP. The easiest way to get the function key is from the [Azure portal](https://portal.azure.com).

## Get the HTTP trigger URL

You can get the URL required to trigger your function, with the function key, from the Azure portal.

Browse to the

[Azure portal](https://portal.azure.com), sign in, type the*appName*of your function app into**Search**at the top of the page, and press enter.In your function app, select

**Functions**, choose your function, then click**Get Function Url**at the top right.Choose

**default (Function key)**and select**Copy**.

You can now use the copied URL to access your function.

## Verify the function in Azure

To verify the function app running on Azure using `cURL`

, replace the URL from the sample below with the URL that you copied from the portal.

```
curl -w "\n" http://azure-functions-sample-demo.azurewebsites.net/api/HttpExample --data AzureFunctions
```


This sends a POST request to the function endpoint with `AzureFunctions`

in the body of the request. You see the following response.

Hello, AzureFunctions

## Next steps

You've created a Java functions project with an HTTP triggered function, run it on your local machine, and deployed it to Azure. Now, extend your function by...

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-azure-sql-trigger -->

# Azure SQL trigger for Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure SQL trigger uses [SQL change tracking](/en-us/sql/relational-databases/track-changes/about-change-tracking-sql-server) functionality to monitor a SQL table for changes and trigger a function when a row is created, updated, or deleted. For configuration details for change tracking for use with the Azure SQL trigger, see [Set up change tracking](#set-up-change-tracking-required). For information on setup details of the Azure SQL extension for Azure Functions, see the [SQL binding overview](functions-bindings-azure-sql).

The Azure SQL trigger scaling decisions for the [Consumption and Premium plans](functions-scale) are done via target-based scaling. For more information, see [Target-based scaling](functions-target-based-scaling) and review the [Azure Functions hosting options](functions-scale).

Note

Support for Consumption plans requires [release v3.1.284 or later](https://github.com/Azure/azure-functions-sql-extension/releases) of the [Azure SQL bindings for Azure Functions](functions-bindings-azure-sql).

## Functionality Overview

The Azure SQL trigger binding uses a polling loop to check for changes, triggering the user function when changes are detected. At a high level, the loop looks like this:

```
while (true) {
1. Get list of changes on table - up to a maximum number controlled by the Sql_Trigger_MaxBatchSize setting
2. Trigger function with list of changes
3. Wait for delay controlled by Sql_Trigger_PollingIntervalMs setting
}
```


Changes are processed in the order that their changes were made, with the oldest changes being processed first. A couple notes about change processing:

- If changes to multiple rows are made at once the exact order that they’re sent to the function is based on the order returned by the CHANGETABLE function
- Changes are "batched" together for a row. If multiple changes are made to a row between each iteration of the loop then only a single change entry exists for that row which will show the difference between the last processed state and the current state
- If changes are made to a set of rows, and then another set of changes are made to half of those same rows, then the half of the rows that weren't changed a second time are processed first. This processing logic is due to the above note with the changes being batched - the trigger will only see the "last" change made and use that for the order it processes them in

Note

Azure SQL change tracking can detect row-level changes in tables that use encryption technologies such as Always Encrypted or Transparent Data Encryption (TDE). However, the Azure SQL trigger doesn’t decrypt or expose encrypted column values in the change payload. The trigger can detect that a change occurred but can’t access the decrypted data for those columns.

For more information on change tracking and how it's used by applications such as Azure SQL triggers, see [work with change tracking](/en-us/sql/relational-databases/track-changes/work-with-change-tracking-sql-server) .

Important

For optimal security, you should use Microsoft Entra ID with managed identities for connections between Functions and Azure SQL Database. Managed identities make your app more secure by eliminating secrets from your application deployments, such as credentials in the connection strings, server names, and ports being used. You can learn how to use managed identities in this tutorial, [Connect a function app to Azure SQL with managed identity and SQL bindings](functions-identity-access-azure-sql-with-managed-identity).

## Example usage

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-outofproc).

The example refers to a `ToDoItem`

class and a corresponding database table:

```
namespace AzureSQL.ToDo
{
public class ToDoItem
{
public Guid Id { get; set; }
public int? order { get; set; }
public string title { get; set; }
public string url { get; set; }
public bool? completed { get; set; }
}
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


[Change tracking](#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds to a `IReadOnlyList<SqlChange<T>>`

, a list of `SqlChange`

objects each with two properties:

**Item:**the item that was changed. The type of the item should follow the table schema as seen in the`ToDoItem`

class.**Operation:**a value from`SqlChangeOperation`

enum. The possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a [C# function](functions-dotnet-class-library) that is invoked when there are changes to the `ToDo`

table:

```
using System;
using System.Collections.Generic;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Azure.Functions.Worker.Extensions.Sql;
using Microsoft.Extensions.Logging;
using Newtonsoft.Json;
namespace AzureSQL.ToDo
{
public static class ToDoTrigger
{
[Function("ToDoTrigger")]
public static void Run(
[SqlTrigger("[dbo].[ToDo]", "SqlConnectionString")]
IReadOnlyList<SqlChange<ToDoItem>> changes,
FunctionContext context)
{
var logger = context.GetLogger("ToDoTrigger");
foreach (SqlChange<ToDoItem> change in changes)
{
ToDoItem toDoItem = change.Item;
logger.LogInformation($"Change operation: {change.Operation}");
logger.LogInformation($"Id: {toDoItem.Id}, Title: {toDoItem.title}, Url: {toDoItem.url}, Completed: {toDoItem.completed}");
}
}
}
}
```


## Example usage

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-java).

The example refers to a `ToDoItem`

class, a `SqlChangeToDoItem`

class, a `SqlChangeOperation`

enum, and a corresponding database table:

In a separate file `ToDoItem.java`

:

```
package com.function;
import java.util.UUID;
public class ToDoItem {
public UUID Id;
public int order;
public String title;
public String url;
public boolean completed;
public ToDoItem() {
}
public ToDoItem(UUID Id, int order, String title, String url, boolean completed) {
this.Id = Id;
this.order = order;
this.title = title;
this.url = url;
this.completed = completed;
}
}
```


In a separate file `SqlChangeToDoItem.java`

:

```
package com.function;
public class SqlChangeToDoItem {
public ToDoItem item;
public SqlChangeOperation operation;
public SqlChangeToDoItem() {
}
public SqlChangeToDoItem(ToDoItem Item, SqlChangeOperation Operation) {
this.Item = Item;
this.Operation = Operation;
}
}
```


In a separate file `SqlChangeOperation.java`

:

```
package com.function;
import com.google.gson.annotations.SerializedName;
public enum SqlChangeOperation {
@SerializedName("0")
Insert,
@SerializedName("1")
Update,
@SerializedName("2")
Delete;
}
```


```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


[Change tracking](#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds to a `SqlChangeToDoItem[]`

, an array of `SqlChangeToDoItem`

objects each with two properties:

**item:**the item that was changed. The type of the item should follow the table schema as seen in the`ToDoItem`

class.**operation:**a value from`SqlChangeOperation`

enum. The possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a Java function that is invoked when there are changes to the `ToDo`

table:

```
package com.function;
import com.microsoft.azure.functions.ExecutionContext;
import com.microsoft.azure.functions.annotation.FunctionName;
import com.microsoft.azure.functions.sql.annotation.SQLTrigger;
import com.function.Common.SqlChangeToDoItem;
import com.google.gson.Gson;
import java.util.logging.Level;
public class ProductsTrigger {
@FunctionName("ToDoTrigger")
public void run(
@SQLTrigger(
name = "todoItems",
tableName = "[dbo].[ToDo]",
connectionStringSetting = "SqlConnectionString")
SqlChangeToDoItem[] todoItems,
ExecutionContext context) {
context.getLogger().log(Level.INFO, "SQL Changes: " + new Gson().toJson(changes));
}
}
```


## Example usage

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-powershell).

The example refers to a `ToDoItem`

database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


[Change tracking](#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds to `todoChanges`

, a list of objects each with two properties:

**item:**the item that was changed. The structure of the item will follow the table schema.**operation:**the possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a PowerShell function that is invoked when there are changes to the `ToDo`

table.

The following is binding data in the function.json file:

```
{
"name": "todoChanges",
"type": "sqlTrigger",
"direction": "in",
"tableName": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample PowerShell code for the function in the `run.ps1`

file:

```
using namespace System.Net
param($todoChanges)
# The output is used to inspect the trigger binding parameter in test methods.
# Use -Compress to remove new lines and spaces for testing purposes.
$changesJson = $todoChanges | ConvertTo-Json -Compress
Write-Host "SQL Changes: $changesJson"
```


## Example usage

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-js).

The example refers to a `ToDoItem`

database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


[Change tracking](#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds `todoChanges`

, an array of objects each with two properties:

**item:**the item that was changed. The structure of the item will follow the table schema.**operation:**the possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a JavaScript function that is invoked when there are changes to the `ToDo`

table.

The following is binding data in the function.json file:

```
{
"name": "todoChanges",
"type": "sqlTrigger",
"direction": "in",
"tableName": "dbo.ToDo",
"connectionStringSetting": "SqlConnectionString"
}
```


The [configuration](#configuration) section explains these properties.

The following is sample JavaScript code for the function in the `index.js`

file:

```
module.exports = async function (context, todoChanges) {
context.log(`SQL Changes: ${JSON.stringify(todoChanges)}`)
}
```


## Example usage

More samples for the Azure SQL trigger are available in the [GitHub repository](https://github.com/Azure/azure-functions-sql-extension/tree/main/samples/samples-python).

The example refers to a `ToDoItem`

database table:

```
CREATE TABLE dbo.ToDo (
[Id] UNIQUEIDENTIFIER PRIMARY KEY,
[order] INT NULL,
[title] NVARCHAR(200) NOT NULL,
[url] NVARCHAR(200) NOT NULL,
[completed] BIT NOT NULL
);
```


[Change tracking](#set-up-change-tracking-required) is enabled on the database and on the table:

```
ALTER DATABASE [SampleDatabase]
SET CHANGE_TRACKING = ON
(CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);
ALTER TABLE [dbo].[ToDo]
ENABLE CHANGE_TRACKING;
```


The SQL trigger binds to a variable `todoChanges`

, a list of objects each with two properties:

**item:**the item that was changed. The structure of the item will follow the table schema.**operation:**the possible values are`Insert`

,`Update`

, and`Delete`

.

The following example shows a Python function that is invoked when there are changes to the `ToDo`

table.

The following is sample python code for the function_app.py file:

```
import json
import logging
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="ToDoTrigger")
@app.sql_trigger(arg_name="todo",
table_name="ToDo",
connection_string_setting="SqlConnectionString")
def todo_trigger(todo: str) -> None:
logging.info("SQL Changes: %s", json.loads(todo))
```


## Attributes

The [C# library](functions-dotnet-class-library) uses the [SqlTrigger](https://github.com/Azure/azure-functions-sql-extension/blob/main/src/TriggerBinding/SqlTriggerAttribute.cs) attribute to declare the SQL trigger on the function, which has the following properties:

| Attribute property | Description |
|---|---|
TableName |
Required. The name of the table monitored by the trigger. |
ConnectionStringSetting |
Required. The name of an app setting that contains the connection string for the database containing the table monitored for changes. The connection string setting name corresponds to the application setting (in `local.settings.json` for local development) that contains the
|
LeasesTableName |
Optional. Name of the table used to store leases. If not specified, the leases table name will be Leases_{FunctionId}_{TableId}. More information on how this is generated can be found
|

## Annotations

In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@SQLTrigger`

annotation (`com.microsoft.azure.functions.sql.annotation.SQLTrigger`

) on parameters whose value would come from Azure SQL. This annotation supports the following elements:

| Element | Description |
|---|---|
name |
Required. The name of the parameter that the trigger binds to. |
tableName |
Required. The name of the table monitored by the trigger. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database containing the table monitored for changes. The connection string setting name corresponds to the application setting (in `local.settings.json` for local development) that contains the
|
LeasesTableName |
Optional. Name of the table used to store leases. If not specified, the leases table name will be Leases_{FunctionId}_{TableId}. More information on how this is generated can be found
|

## Configuration

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
name |
Required. The name of the parameter that the trigger binds to. |
type |
Required. Must be set to `sqlTrigger` . |
direction |
Required. Must be set to `in` . |
tableName |
Required. The name of the table monitored by the trigger. |
connectionStringSetting |
Required. The name of an app setting that contains the connection string for the database containing the table monitored for changes. The connection string setting name corresponds to the application setting (in `local.settings.json` for local development) that contains the
|
LeasesTableName |
Optional. Name of the table used to store leases. If not specified, the leases table name will be Leases_{FunctionId}_{TableId}. More information on how this is generated can be found
|

## Optional Configuration

The following optional settings can be configured for the SQL trigger for local development or for cloud deployments.

### host.json

This section describes the configuration settings available for this binding in version 2.x and later. Settings in the host.json file apply to all functions in a function app instance. For more information about function app configuration settings, see [host.json reference for Azure Functions](functions-host-json).

| Setting | Default | Description |
|---|---|---|
MaxBatchSize |
100 | The maximum number of changes processed with each iteration of the trigger loop before being sent to the triggered function. |
PollingIntervalMs |
1000 | The delay in milliseconds between processing each batch of changes. (1000 ms is 1 second) |
MaxChangesPerWorker |
1000 | The upper limit on the number of pending changes in the user table that are allowed per application-worker. If the count of changes exceeds this limit, it might result in a scale-out. The setting only applies for Azure Function Apps with
|

#### Example host.json file

Here is an example host.json file with the optional settings:

```
{
"version": "2.0",
"extensions": {
"Sql": {
"MaxBatchSize": 300,
"PollingIntervalMs": 1000,
"MaxChangesPerWorker": 100
}
},
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
},
"logLevel": {
"default": "Trace"
}
}
}
```


### local.setting.json

The local.settings.json file stores app settings and settings used by local development tools. Settings in the local.settings.json file are used only when you're running your project locally. When you publish your project to Azure, be sure to also add any required settings to the app settings for the function app.

Important

Because the local.settings.json may contain secrets, such as connection strings, you should never store it in a remote repository. Tools that support Functions provide ways to synchronize settings in the local.settings.json file with the [app settings](functions-how-to-use-azure-function-app-settings#settings) in the function app to which your project is deployed.

| Setting | Default | Description |
|---|---|---|
Sql_Trigger_BatchSize |
100 | The maximum number of changes processed with each iteration of the trigger loop before being sent to the triggered function. |
Sql_Trigger_PollingIntervalMs |
1000 | The delay in milliseconds between processing each batch of changes. (1000 ms is 1 second) |
Sql_Trigger_MaxChangesPerWorker |
1000 | The upper limit on the number of pending changes in the user table that are allowed per application-worker. If the count of changes exceeds this limit, it might result in a scale-out. The setting only applies for Azure Function Apps with
|

#### Example local.settings.json file

Here is an example local.settings.json file with the optional settings:

```
{
"IsEncrypted": false,
"Values": {
"AzureWebJobsStorage": "UseDevelopmentStorage=true",
"FUNCTIONS_WORKER_RUNTIME": "dotnet",
"SqlConnectionString": "",
"Sql_Trigger_MaxBatchSize": 300,
"Sql_Trigger_PollingIntervalMs": 1000,
"Sql_Trigger_MaxChangesPerWorker": 100
}
}
```


## Set up change tracking (required)

Setting up change tracking for use with the Azure SQL trigger requires two steps. These steps can be completed from any SQL tool that supports running queries, including [Visual Studio Code](/en-us/sql/tools/visual-studio-code/mssql-extensions), [Azure Data Studio](/en-us/azure-data-studio/download-azure-data-studio) or [SQL Server Management Studio](/en-us/sql/ssms/download-sql-server-management-studio-ssms).

Enable change tracking on the SQL database, substituting

`your database name`

with the name of the database where the table to be monitored is located:`ALTER DATABASE [your database name] SET CHANGE_TRACKING = ON (CHANGE_RETENTION = 2 DAYS, AUTO_CLEANUP = ON);`

The

`CHANGE_RETENTION`

option specifies the time period for which change tracking information (change history) is kept. The retention of change history by the SQL database might affect trigger functionality. For example, if the Azure Function is turned off for several days and then resumed, the database will contain the changes that occurred in past two days in the above setup example.The

`AUTO_CLEANUP`

option is used to enable or disable the clean-up task that removes old change tracking information. If a temporary problem that prevents the trigger from running, turning off auto cleanup can be useful to pause the removal of information older than the retention period until the problem is resolved.More information on change tracking options is available in the

[SQL documentation](/en-us/sql/relational-databases/track-changes/enable-and-disable-change-tracking-sql-server).Enable change tracking on the table, substituting

`your table name`

with the name of the table to be monitored (changing the schema if appropriate):`ALTER TABLE [dbo].[your table name] ENABLE CHANGE_TRACKING;`

The trigger needs to have read access on the table being monitored for changes and to the change tracking system tables. Each function trigger has an associated change tracking table and leases table in a schema

`az_func`

. These tables are created by the trigger if they don't yet exist. More information on these data structures is available in the Azure SQL binding library[documentation](https://github.com/Azure/azure-functions-sql-extension/blob/main/docs/BindingsOverview.md#internal-state-tables).

## Enable runtime-driven scaling

Optionally, your functions can scale automatically based on the number of changes that are pending to be processed in the user table. To allow your functions to scale properly on the Premium plan when using SQL triggers, you need to enable runtime scale monitoring.

In the Azure portal, in your function app, select

**Configuration**.On the

**Function runtime settings**tab, for**Runtime Scale Monitoring**, select**On**.

## Retry support

Further information on the SQL trigger [retry support](https://github.com/Azure/azure-functions-sql-extension/blob/main/docs/BindingsOverview.md#retry-support-for-trigger-bindings) and [leases tables](https://github.com/Azure/azure-functions-sql-extension/blob/main/docs/TriggerBinding.md#internal-state-tables) is available in the GitHub repository.

### Startup retries

If an exception occurs during startup then the host runtime automatically attempts to restart the trigger listener with an exponential backoff strategy. These retries continue until either the listener is successfully started or the startup is canceled.

### Broken connection retries

If the function successfully starts but then an error causes the connection to break (such as the server going offline) then the function continues to try and reopen the connection until the function is either stopped or the connection succeeds. If the connection is successfully re-established then it picks up processing changes where it left off.

Note that these retries are outside the built-in idle connection retry logic that SqlClient has which can be configured with the `ConnectRetryCount`

and `ConnectRetryInterval`

[connection string options](/en-us/dotnet/api/microsoft.data.sqlclient.sqlconnection.connectionstring?view=sqlclient-dotnet-core-5.0&preserve-view=true#Microsoft_Data_SqlClient_SqlConnection_ConnectionString). The built-in idle connection retries are attempted first and if those fail to reconnect then the trigger binding attempts to re-establish the connection itself.

### Function exception retries

If an exception occurs in the user function when processing changes then the batch of rows currently being processed are retried again in 60 seconds. Other changes are processed as normal during this time, but the rows in the batch that caused the exception are ignored until the timeout period has elapsed.

If the function execution fails five times in a row for a given row then that row is completely ignored for all future changes. Because the rows in a batch aren't deterministic, rows in a failed batch might end up in different batches in subsequent invocations. This means that not all rows in the failed batch will necessarily be ignored. If other rows in the batch were the ones causing the exception, the "good" rows might end up in a different batch that doesn't fail in future invocations.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-add-output-binding-storage-queue-vs-code -->

# Connect Azure Functions to Azure Storage using Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you connect Azure services and other resources to functions without having to write your own integration code. These *bindings*, which represent both input and output, are declared within the function definition. Data from bindings is provided to the function as parameters. A *trigger* is a special type of input binding. Although a function has only one trigger, it can have multiple input and output bindings. To learn more, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

In this article, you learn how to use Visual Studio Code to connect Azure Storage to the function you created in the previous quickstart article. The output binding that you add to this function writes data from the HTTP request to a message in an Azure Queue storage queue.

Most bindings require a stored connection string that Functions uses to access the bound service. To make it easier, you use the storage account that you created with your function app. The connection to this account is already stored in an app setting named `AzureWebJobsStorage`

.

Note

This article currently supports [Node.js v4 for Functions](functions-reference-node?pivots=nodejs-model-v4).

## Configure your local environment

Before you begin, you must meet the following requirements:

Install the

[Azure Storage extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurestorage).Install

[Azure Storage Explorer](https://storageexplorer.com/). Storage Explorer is a tool that you'll use to examine queue messages generated by your output binding. Storage Explorer is supported on macOS, Windows, and Linux-based operating systems.

- Install
[.NET Core CLI tools](/en-us/dotnet/core/tools/?tabs=netcore2x).

- Complete the steps in
[part 1 of Create a function in Azure using Visual Studio Code](how-to-create-function-vs-code).

This article assumes that you're already signed in to your Azure subscription from Visual Studio Code. You can sign in by running `Azure: Sign In`

from the command palette.

## Download the function app settings

In the [previous quickstart article](how-to-create-function-vs-code?pivot=programming-language-csharp), you created a function app in Azure along with the required storage account. The connection string for this account is stored securely in the app settings in Azure. In this article, you write messages to a Storage queue in the same account. To connect to your storage account when running the function locally, you must download app settings to the *local.settings.json* file.

Press

`F1`to open the command palette, then search for and run the command`Azure Functions: Download Remote Settings...`

.Choose the function app you created in the previous article. Select

**Yes to all**to overwrite the existing local settings.Important

Because the

*local.settings.json*file contains secrets, it never gets published, and is excluded from the source control.Copy the value

`AzureWebJobsStorage`

, which is the key for the storage account connection string value. You use this connection to verify that the output binding works as expected.

## Register binding extensions

Because you're using a Queue storage output binding, you must have the Storage bindings extension installed before you run the project.

Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles is already enabled in the *host.json* file at the root of the project, which should look like the following example:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[3.*, 4.0.0)"
}
}
```


Now, you can add the storage output binding to your project.

Your project has been configured to use [extension bundles](extension-bundles), which automatically installs a predefined set of extension packages.

Extension bundles is already enabled in the *host.json* file at the root of the project, which should look like the following example:

```
{
"version": "2.0",
"logging": {
"applicationInsights": {
"samplingSettings": {
"isEnabled": true,
"excludedTypes": "Request"
}
}
},
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.*, 5.0.0)"
}
}
```


Now, you can add the storage output binding to your project.

Except for HTTP and timer triggers, bindings are implemented as extension packages. Run the following [dotnet add package](/en-us/dotnet/core/tools/dotnet-add-package) command in the Terminal window to add the Storage extension package to your project.

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues --prerelease
```


Now, you can add the storage output binding to your project.

## Add an output binding

To write to an Azure Storage queue:

Add an

`extraOutputs`

property to the binding configuration`{ methods: ['GET', 'POST'], extraOutputs: [sendToQueue], // add output binding to HTTP trigger authLevel: 'function', handler: () => {} }`

Add a

`output.storageQueue`

function above the`app.http`

call`const sendToQueue = output.storageQueue({ queueName: 'outqueue', connection: 'AzureWebJobsStorage', });`


To write to an Azure Storage queue:

Add an

`extraOutputs`

property to the binding configuration`{ methods: ['GET', 'POST'], extraOutputs: [sendToQueue], // add output binding to HTTP trigger authLevel: 'function', handler: () => {} }`

Add a

`output.storageQueue`

function above the`app.http`

call`const sendToQueue: StorageQueueOutput = output.storageQueue({ queueName: 'outqueue', connection: 'AzureWebJobsStorage', });`


In Functions, each type of binding requires a `direction`

, `type`

, and unique `name`

. The way you define these attributes depends on the language of your function app.

Binding attributes are defined in the *function.json* file for a given function. Depending on the binding type, additional properties may be required. The [queue output configuration](functions-bindings-storage-queue-output#configuration) describes the fields required for an Azure Storage queue binding. The extension makes it easy to add bindings to the *function.json* file.

To create a binding, right-click (Ctrl+click on macOS) the `function.json`

file in your HttpTrigger folder and choose **Add binding...**. Follow the prompts to define the following binding properties for the new binding:

| Prompt | Value | Description |
|---|---|---|
Select binding direction |
`out` |
The binding is an output binding. |
Select binding with direction... |
`Azure Queue Storage` |
The binding is an Azure Storage queue binding. |
The name used to identify this binding in your code |
`msg` |
Name that identifies the binding parameter referenced in your code. |
The queue to which the message will be sent |
`outqueue` |
The name of the queue that the binding writes to. When the queueName doesn't exist, the binding creates it on first use. |
Select setting from "local.setting.json" |
`AzureWebJobsStorage` |
The name of an application setting that contains the connection string for the Storage account. The `AzureWebJobsStorage` setting contains the connection string for the Storage account you created with the function app. |

A binding is added to the `bindings`

array in your *function.json*, which should look like the following:

```
"name": "msg",
"queueName": "outqueue",
"connection": "AzureWebJobsStorage"
}
]
}
```


Binding attributes are defined by decorating specific function code in the *function_app.py* file. You use the `queue_output`

decorator to add an [Azure Queue storage output binding](/en-us/azure/azure-functions/functions-bindings-triggers-python#azure-queue-storage-output-binding).

By using the `queue_output`

decorator, the binding direction is implicitly 'out' and type is Azure Storage Queue. Add the following decorator to your function code in *HttpExample\function_app.py*:

```
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
```


In this code, `arg_name`

identifies the binding parameter referenced in your code, `queue_name`

is name of the queue that the binding writes to, and `connection`

is the name of an application setting that contains the connection string for the Storage account. In quickstarts you use the same storage account as the function app, which is in the `AzureWebJobsStorage`

setting. When the `queue_name`

doesn't exist, the binding creates it on first use.

In a C# project, the bindings are defined as binding attributes on the function method. Specific definitions depend on whether your app runs in-process (C# class library) or in an isolated worker process.

Open the *HttpExample.cs* project file and add the following `MultiResponse`

class:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public HttpResponseData HttpResponse { get; set; }
}
```


The `MultiResponse`

class allows you to write to a storage queue named `outqueue`

and an HTTP success message. Multiple messages could be sent to the queue because the `QueueOutput`

attribute is applied to a string array.

The `Connection`

property sets the connection string for the storage account. In this case, you could omit `Connection`

because you're already using the default storage account.

In a Java project, the bindings are defined as binding annotations on the function method. The *function.json* file is then autogenerated based on these annotations.

Browse to the location of your function code under *src/main/java*, open the *Function.java* project file, and add the following parameter to the `run`

method definition:

```
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
```


The `msg`

parameter is an [ OutputBinding<T>](/en-us/java/api/com.microsoft.azure.functions.outputbinding) type, which represents a collection of strings that are written as messages to an output binding when the function completes. In this case, the output is a storage queue named

`outqueue`

. The connection string for the Storage account is set by the `connection`

method. Rather than the connection string itself, you pass the application setting that contains the Storage account connection string.The `run`

method definition should now look like the following example:

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
```


## Add code that uses the output binding

After the binding is defined, you can use the `name`

of the binding to access it as an attribute in the function signature. By using an output binding, you don't have to use the Azure Storage SDK code for authentication, getting a queue reference, or writing data. The Functions runtime and queue output binding do those tasks for you.

Add code that uses the output binding object on `context.extraOutputs`

to create a queue message. Add this code before the return statement.

```
context.extraOutputs.set(sendToQueue, [msg]);
```


At this point, your function could look as follows:

```
const { app, output } = require('@azure/functions');
const sendToQueue = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [sendToQueue],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


Add code that uses the output binding object on `context.extraOutputs`

to create a queue message. Add this code before the return statement.

```
context.extraOutputs.set(sendToQueue, [msg]);
```


At this point, your function could look as follows:

```
import {
app,
output,
HttpRequest,
HttpResponseInit,
InvocationContext,
StorageQueueOutput,
} from '@azure/functions';
const sendToQueue: StorageQueueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
export async function HttpExample(
request: HttpRequest,
context: InvocationContext,
): Promise<HttpResponseInit> {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
}
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: HttpExample,
});
```


Add code that uses the `Push-OutputBinding`

cmdlet to write text to the queue using the `msg`

output binding. Add this code before you set the OK status in the `if`

statement.

```
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
```


At this point, your function must look as follows:

```
using namespace System.Net
# Input bindings are passed in via param block.
param($Request, $TriggerMetadata)
# Write to the Azure Functions log stream.
Write-Host "PowerShell HTTP trigger function processed a request."
# Interact with query parameters or the body of the request.
$name = $Request.Query.Name
if (-not $name) {
$name = $Request.Body.Name
}
if ($name) {
# Write the $name value to the queue,
# which is the name passed to the function.
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
$status = [HttpStatusCode]::OK
$body = "Hello $name"
}
else {
$status = [HttpStatusCode]::BadRequest
$body = "Please pass a name on the query string or in the request body."
}
# Associate values to output bindings by calling 'Push-OutputBinding'.
Push-OutputBinding -Name Response -Value ([HttpResponseContext]@{
StatusCode = $status
Body = $body
})
```


Update *HttpExample\function_app.py* to match the following code, add the `msg`

parameter to the function definition and `msg.set(name)`

under the `if name:`

statement:

```
import azure.functions as func
import logging
app = func.FunctionApp(http_auth_level=func.AuthLevel.ANONYMOUS)
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
name = req.params.get('name')
if not name:
try:
req_body = req.get_json()
except ValueError:
pass
else:
name = req_body.get('name')
if name:
msg.set(name)
return func.HttpResponse(f"Hello, {name}. This HTTP triggered function executed successfully.")
else:
return func.HttpResponse(
"This HTTP triggered function executed successfully. Pass a name in the query string or in the request body for a personalized response.",
status_code=200
)
```


The `msg`

parameter is an instance of the [ azure.functions.Out class](/en-us/python/api/azure-functions/azure.functions.out). The

`set`

method writes a string message to the queue. In this case, it's the `name`

passed to the function in the URL query string.Replace the existing `HttpExample`

class with the following code:

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequestData req,
FunctionContext executionContext)
{
var logger = executionContext.GetLogger("HttpExample");
logger.LogInformation("C# HTTP trigger function processed a request.");
var message = "Welcome to Azure Functions!";
var response = req.CreateResponse(HttpStatusCode.OK);
response.Headers.Add("Content-Type", "text/plain; charset=utf-8");
response.WriteString(message);
// Return a response to both HTTP trigger and storage output binding.
return new MultiResponse()
{
// Write a single message.
Messages = new string[] { message },
HttpResponse = response
};
}
}
```


Now, you can use the new `msg`

parameter to write to the output binding from your function code. Add the following line of code before the success response to add the value of `name`

to the `msg`

output binding.

```
msg.setValue(name);
```


When you use an output binding, you don't have to use the Azure Storage SDK code for authentication, getting a queue reference, or writing data. The Functions runtime and queue output binding do those tasks for you.

Your `run`

method should now look like the following example:

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
context.getLogger().info("Java HTTP trigger processed a request.");
// Parse query parameter
String query = request.getQueryParameters().get("name");
String name = request.getBody().orElse(query);
if (name == null) {
return request.createResponseBuilder(HttpStatus.BAD_REQUEST)
.body("Please pass a name on the query string or in the request body").build();
} else {
// Write the name to the message queue.
msg.setValue(name);
return request.createResponseBuilder(HttpStatus.OK).body("Hello, " + name).build();
}
}
```


## Update the tests

Because the archetype also creates a set of tests, you need to update these tests to handle the new `msg`

parameter in the `run`

method signature.

Browse to the location of your test code under *src/test/java*, open the *Function.java* project file, and replace the line of code under `//Invoke`

with the following code.

```
@SuppressWarnings("unchecked")
final OutputBinding<String> msg = (OutputBinding<String>)mock(OutputBinding.class);
final HttpResponseMessage ret = new Function().run(req, msg, context);
```


## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to Azure. If you don't already have Core Tools installed locally, you are prompted to install it the first time you run your project.

To call your function, press

`F5`to start the function app project. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel. You can see the URL endpoint of your HTTP-triggered function running locally.If you don't already have Core Tools installed, select

**Install**to install Core Tools when prompted to do so.

If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to**WSL Bash**.With the Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Windows) or`Ctrl -`click (macOS) the`HttpExample`

function and choose**Execute Function Now...**.In the

**Enter request body**, press`Enter`to send a request message to your function.When the function executes locally and returns a response, a notification is raised in Visual Studio Code. Information about the function execution is shown in the

**Terminal**panel.Press

`Ctrl + C`to stop Core Tools and disconnect the debugger.

## Run the function locally

As in the previous article, press

`F5`to start the function app project and Core Tools.With the Core Tools running, go to the

**Azure: Functions**area. Under**Functions**, expand**Local Project**>**Functions**. Right-click (Ctrl-click on Mac) the`HttpExample`

function and select**Execute Function Now...**.In the

**Enter request body**, you see the request message body value of`{ "name": "Azure" }`

. Press`Enter`to send this request message to your function.After a response is returned, press

`Ctrl + C`to stop Core Tools.

Because you're using the storage connection string, your function connects to the Azure storage account when running locally. A new queue named **outqueue** is created in your storage account by the Functions runtime when the output binding is first used. You'll use Storage Explorer to verify that the queue was created along with the new message.

### Connect Storage Explorer to your account

Skip this section if you've already installed Azure Storage Explorer and connected it to your Azure account.

Run the

[Azure Storage Explorer](https://storageexplorer.com/)tool, select the connect icon on the left, and select**Add an account**.In the

**Connect**dialog, choose**Add an Azure account**, choose your**Azure environment**, and then select**Sign in...**.

After you successfully sign in to your account, you see all of the Azure subscriptions associated with your account. Choose your subscription and select **Open Explorer**.

### Examine the output queue

In Visual Studio Code, press

`F1`to open the command palette, then search for and run the command`Azure Storage: Open in Storage Explorer`

and choose your storage account name. Your storage account opens in the Azure Storage Explorer.Expand the

**Queues**node, and then select the queue named**outqueue**.The queue contains the message that the queue output binding created when you ran the HTTP-triggered function. If you invoked the function with the default

`name`

value of*Azure*, the queue message is*Name passed to the function: Azure*.Run the function again, send another request, and you see a new message in the queue.


Now, it's time to republish the updated function app to Azure.

## Redeploy and verify the updated app

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure Functions: Deploy to function app...`

.Choose the function app that you created in the first article. Because you're redeploying your project to the same app, select

**Deploy**to dismiss the warning about overwriting files.After the deployment completes, you can again use the

**Execute Function Now...**feature to trigger the function in Azure. This command automatically retrieves the function access key and uses it when calling the HTTP trigger endpoint.Again

[view the message in the storage queue](#examine-the-output-queue)to verify that the output binding generates a new message in the queue.

## Clean up resources

In Azure, *resources* refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You've created resources to complete these quickstarts. You may be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). If you don't need the resources anymore, here's how to delete them:

In Visual Studio Code, press

`F1`to open the command palette. In the command palette, search for and select`Azure: Open in portal`

.Choose your function app and press

`Enter`. The function app page opens in the Azure portal.In the

**Overview**tab, select the named link next to**Resource group**.On the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

You've updated your HTTP triggered function to write data to a Storage queue. Now you can learn more about developing Functions using Visual Studio Code:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-machine-learning-tensorflow -->

# Tutorial: Apply machine learning models in Azure Functions with Python and TensorFlow

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Python, TensorFlow, and Azure Functions with a machine learning model to classify an image based on its contents. Because you do all work locally and create no Azure resources in the cloud, there is no cost to complete this tutorial.

- Initialize a local environment for developing Azure Functions in Python.
- Import a custom TensorFlow machine learning model into a function app.
- Build a serverless HTTP API for classifying an image as containing a dog or a cat.
- Consume the API from a web app.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). [Python 3.7.4](https://www.python.org/downloads/release/python-374/). (Python 3.7.4 and Python 3.6.x are verified with Azure Functions; Python 3.8 and later versions are not yet supported.)- The
[Azure Functions Core Tools](functions-run-local#install-the-azure-functions-core-tools) - A code editor such as
[Visual Studio Code](https://code.visualstudio.com/)

### Prerequisite check

- In a terminal or command window, run
`func --version`

to check that the Azure Functions Core Tools are version 2.7.1846 or later. - Run
`python --version`

(Linux/macOS) or`py --version`

(Windows) to check your Python version reports 3.7.x.

## Clone the tutorial repository

In a terminal or command window, clone the following repository using Git:

`git clone https://github.com/Azure-Samples/functions-python-tensorflow-tutorial.git`

Navigate into the folder and examine its contents.

`cd functions-python-tensorflow-tutorial`

*start*is your working folder for the tutorial.*end*is the final result and full implementation for your reference.*resources*contains the machine learning model and helper libraries.*frontend*is a website that calls the function app.


## Create and activate a Python virtual environment

Navigate to the *start* folder and run the following commands to create and activate a virtual environment named `.venv`

. Be sure to use Python 3.7, which is supported by Azure Functions.

```
cd start
python -m venv .venv
source .venv/bin/activate
```


If Python didn't install the venv package on your Linux distribution, run the following command:

```
sudo apt-get install python3-venv
```


You run all subsequent commands in this activated virtual environment. (To exit the virtual environment, run `deactivate`

.)

## Create a local functions project

In Azure Functions, a function project is a container for one or more individual functions that each responds to a specific trigger. All functions in a project share the same local and hosting configurations. In this section, you create a function project that contains a single boilerplate function named `classify`

that provides an HTTP endpoint. You add more specific code in a later section.

In the

*start*folder, use the Azure Functions Core Tools to initialize a Python function app:`func init --worker-runtime python`

After initialization, the

*start*folder contains various files for the project, including configurations files named[local.settings.json](functions-develop-local#local-settings-file)and[host.json](functions-host-json). Because*local.settings.json*can contain secrets downloaded from Azure, the file is excluded from source control by default in the*.gitignore*file.Tip

Because a function project is tied to a specific runtime, all the functions in the project must be written with the same language.

Add a function to your project by using the following command, where the

`--name`

argument is the unique name of your function and the`--template`

argument specifies the function's trigger.`func new`

create a subfolder matching the function name that contains a code file appropriate to the project's chosen language and a configuration file named*function.json*.`func new --name classify --template "HTTP trigger"`

This command creates a folder matching the name of the function,

*classify*. In that folder are two files:*__init__.py*, which contains the function code, and*function.json*, which describes the function's trigger and its input and output bindings. For details on the contents of these files, see[Programming model](functions-reference-python?pivots=python-mode-configuration#programming-model)in the Python developer guide.

## Run the function locally

Start the function by starting the local Azure Functions runtime host in the

*start*folder:`func start`

Once you see the

`classify`

endpoint appear in the output, navigate to the URL,`http://localhost:7071/api/classify?name=Azure`

. The message "Hello Azure!" should appear in the output.Use

**Ctrl**-**C**to stop the host.

## Import the TensorFlow model and add helper code

To modify the `classify`

function to classify an image based on its contents, you use a pre-built TensorFlow model that was trained with and exported from Azure Custom Vision Service. The model, which is contained in the *resources* folder of the sample you cloned earlier, classifies an image based on whether it contains a dog or a cat. You then add some helper code and dependencies to your project.

To build your own model using the free tier of the Custom Vision Service, follow the instructions in the [sample project repository](https://github.com/Azure-Samples/functions-python-tensorflow-tutorial/blob/master/train-custom-vision-model.md).

Tip

If you want to host your TensorFlow model independent of the function app, you can instead mount a file share containing your model to your Linux function app. To learn more, see [Mount a file share to a Python function app using Azure CLI](scripts/functions-cli-mount-files-storage-linux).

In the

*start*folder, run following command to copy the model files into the*classify*folder. Be sure to include`\*`

in the command.`cp ../resources/model/* classify`

Verify that the

*classify*folder contains files named*model.pb*and*labels.txt*. If not, check that you ran the command in the*start*folder.In the

*start*folder, run the following command to copy a file with helper code into the*classify*folder:`cp ../resources/predict.py classify`

Verify that the

*classify*folder now contains a file named*predict.py*.Open

*start/requirements.txt*in a text editor and add the following dependencies required by the helper code:`tensorflow==1.14 Pillow requests`

Save

*requirements.txt*.Install the dependencies by running the following command in the

*start*folder. Installation may take a few minutes, during which time you can proceed with modifying the function in the next section.`pip install --no-cache-dir -r requirements.txt`

On Windows, you may encounter the error, "Could not install packages due to an EnvironmentError: [Errno 2] No such file or directory:" followed by a long pathname to a file like

*sharded_mutable_dense_hashtable.cpython-37.pyc*. Typically, this error happens because the depth of the folder path becomes too long. In this case, set the registry key`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\FileSystem@LongPathsEnabled`

to`1`

to enable long paths. Alternately, check where your Python interpreter is installed. If that location has a long path, try reinstalling in a folder with a shorter path.

Tip

When calling upon *predict.py* to make its first prediction, a function named `_initialize`

loads the TensorFlow model from disk and caches it in global variables. This caching speeds up subsequent predictions.

## Update the function to run predictions

Open

*classify/__init__.py*in a text editor and add the following lines after the existing`import`

statements to import the standard JSON library and the*predict*helpers:`import logging import azure.functions as func import json # Import helper script from .predict import predict_image_from_url`

Replace the entire contents of the

`main`

function with the following code:`def main(req: func.HttpRequest) -> func.HttpResponse: image_url = req.params.get('img') logging.info('Image URL received: ' + image_url) results = predict_image_from_url(image_url) headers = { "Content-type": "application/json", "Access-Control-Allow-Origin": "*" } return func.HttpResponse(json.dumps(results), headers = headers)`

This function receives an image URL in a query string parameter named

`img`

. It then calls`predict_image_from_url`

from the helper library to download and classify the image using the TensorFlow model. The function then returns an HTTP response with the results.Important

Because this HTTP endpoint is called by a web page hosted on another domain, the response includes an

`Access-Control-Allow-Origin`

header to satisfy the browser's Cross-Origin Resource Sharing (CORS) requirements.In a production application, change

`*`

to the web page's specific origin for added security.Save your changes, then assuming that dependencies have finished installing, start the local function host again with

`func start`

. Be sure to run the host in the*start*folder with the virtual environment activated. Otherwise the host will start, but you will see errors when invoking the function.`func start`

In a browser, open the following URL to invoke the function with the URL of a cat image and confirm that the returned JSON classifies the image as a cat.

`http://localhost:7071/api/classify?img=https://raw.githubusercontent.com/Azure-Samples/functions-python-tensorflow-tutorial/master/resources/assets/samples/cat1.png`

Keep the host running because you use it in the next step.


### Run the local web app front end to test the function

To test invoking the function endpoint from another web app, there's a simple app in the repository's *frontend* folder.

Open a new terminal or command prompt and activate the virtual environment (as described earlier under

[Create and activate a Python virtual environment](#create-and-activate-a-python-virtual-environment)).Navigate to the repository's

*frontend*folder.Start an HTTP server with Python:

`python -m http.server`

In a browser, navigate to

`localhost:8000`

, then enter one of the following photo URLs into the textbox, or use the URL of any publicly accessible image.`https://raw.githubusercontent.com/Azure-Samples/functions-python-tensorflow-tutorial/master/resources/assets/samples/cat1.png`

`https://raw.githubusercontent.com/Azure-Samples/functions-python-tensorflow-tutorial/master/resources/assets/samples/cat2.png`

`https://raw.githubusercontent.com/Azure-Samples/functions-python-tensorflow-tutorial/master/resources/assets/samples/dog1.png`

`https://raw.githubusercontent.com/Azure-Samples/functions-python-tensorflow-tutorial/master/resources/assets/samples/dog2.png`


Select

**Submit**to invoke the function endpoint to classify the image.If the browser reports an error when you submit the image URL, check the terminal in which you're running the function app. If you see an error like "No module found 'PIL'", you may have started the function app in the

*start*folder without first activating the virtual environment you created earlier. If you still see errors, run`pip install -r requirements.txt`

again with the virtual environment activated and look for errors.

Note

The model always classifies the content of the image as a cat or a dog, regardless of whether the image contains either, defaulting to dog. Images of tigers and panthers, for example, typically classify as cat, but images of elephants, carrots, or airplanes classify as dog.

## Clean up resources

Because the entirety of this tutorial runs locally on your machine, there are no Azure resources or services to clean up.

## Next steps

In this tutorial, you learned how to build and customize an HTTP API endpoint with Azure Functions to classify images using a TensorFlow model. You also learned how to call the API from a web app. You can use the techniques in this tutorial to build out APIs of any complexity, all while running on the serverless compute model provided by Azure Functions.

See also:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-first-quarkus -->

# Deploy serverless Java apps with Quarkus on Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you'll develop, build, and deploy a serverless Java app to Azure Functions by using [Quarkus](https://quarkus.io). This article uses Quarkus Funqy and its built-in support for the Azure Functions HTTP trigger for Java. Using Quarkus with Azure Functions gives you the power of the Quarkus programming model with the scale and flexibility of Azure Functions. When you finish, you'll run serverless Quarkus applications on Azure Functions and continue to monitor your app on Azure.

## Prerequisites

- The
[Azure CLI](/en-us/cli/azure/overview)installed on your own computer. - An
[Azure account](https://azure.microsoft.com/). If you don't have an Azure account, create a[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. [Java JDK 17](/en-us/azure/developer/java/fundamentals/java-support-on-azure)with`JAVA_HOME`

configured appropriately. This article was written with Java 17 in mind, but Azure Functions and Quarkus also support older versions of Java.[Apache Maven 3.8.1+](https://maven.apache.org).

## Create the app project

Use the following command to clone the sample Java project for this article. The sample is on [GitHub](https://github.com/Azure-Samples/quarkus-azure).

```
git clone https://github.com/Azure-Samples/quarkus-azure
cd quarkus-azure
git checkout 2023-01-10
cd functions-quarkus
```


If you see a message about being in **detached HEAD** state, this message is safe to ignore. Because this article does not require any commits, detached HEAD state is appropriate.

Explore the sample function. Open the *functions-quarkus/src/main/java/io/quarkus/GreetingFunction.java* file.

Run the following command. The `@Funq`

annotation makes your method (in this case, `funqyHello`

) a serverless function.

```
@Funq
public String funqyHello() {
return "hello funqy";
}
```


Azure Functions Java has its own set of Azure-specific annotations, but these annotations aren't necessary when you're using Quarkus on Azure Functions in a simple capacity as we're doing here. For more information about Azure Functions Java annotations, see the [Azure Functions Java developer guide](functions-reference-java).

Unless you specify otherwise, the function's name is the same as the method name. You can also use the following command to define the function name with a parameter to the annotation:

```
@Funq("alternateName")
public String funqyHello() {
return "hello funqy";
}
```


The name is important. It becomes a part of the REST URI to invoke the function, as shown later in the article.

## Test the function locally

Use `mvn`

to run Quarkus dev mode on your local terminal. Running Quarkus in this way enables live reload with background compilation. When you modify your Java files and/or your resource files and refresh your browser, these changes will automatically take effect.

A browser refresh triggers a scan of the workspace. If the scan detects any changes, the Java files are recompiled and the application is redeployed. Your redeployed application services the request. If there are any problems with compilation or deployment, an error page will let you know.

In the following procedure, replace `yourResourceGroupName`

with a resource group name. Function app names must be globally unique across all of Azure. Resource group names must be globally unique within a subscription. This article achieves the necessary uniqueness by prepending the resource group name to the function name. Consider prepending a unique identifier to any names you create that must be unique. A useful technique is to use your initials followed by today's date in `mmdd`

format.

The resource group is not necessary for this part of the instructions, but it's required later. For simplicity, the Maven project requires you to define the property.

Invoke Quarkus dev mode:

`mvn -DskipTests -DresourceGroup=<yourResourceGroupName> quarkus:dev`

The output should look like this:

`... --/ __ \/ / / / _ | / _ \/ //_/ / / / __/ -/ /_/ / /_/ / __ |/ , _/ ,< / /_/ /\ \ --\___\_\____/_/ |_/_/|_/_/|_|\____/___/ INFO [io.quarkus] (Quarkus Main Thread) quarkus-azure-function 1.0-SNAPSHOT on JVM (powered by Quarkus xx.xx.xx.) started in 1.290s. Listening on: http://localhost:8080 INFO [io.quarkus] (Quarkus Main Thread) Profile dev activated. Live Coding activated. INFO [io.quarkus] (Quarkus Main Thread) Installed features: [cdi, funqy-http, smallrye-context-propagation, vertx] -- Tests paused Press [r] to resume testing, [o] Toggle test output, [:] for the terminal, [h] for more options>`

Access the function by using the

`CURL`

command on your local terminal:`curl localhost:8080/api/funqyHello`

The output should look like this:

`"hello funqy"`


## Add dependency injection to the function

The open-standard technology Jakarta EE Contexts and Dependency Injection (CDI) provides dependency injection in Quarkus.

Add a new function that uses dependency injection.

Create a

*GreetingService.java*file in the*functions-quarkus/src/main/java/io/quarkus*directory. Use the following code as the source code of the file:`package io.quarkus; import javax.enterprise.context.ApplicationScoped; @ApplicationScoped public class GreetingService { public String greeting(String name) { return "Welcome to build Serverless Java with Quarkus on Azure Functions, " + name; } }`

Save the file.

`GreetingService`

is an injectable bean that implements a`greeting()`

method. The method returns a`Welcome...`

string message with a`name`

parameter.Open the existing

*functions-quarkus/src/main/java/io/quarkus/GreetingFunction.java*file. Replace the class with the following code to add a new`gService`

field and the`greeting`

method:`package io.quarkus; import javax.inject.Inject; import io.quarkus.funqy.Funq; public class GreetingFunction { @Inject GreetingService gService; @Funq public String greeting(String name) { return gService.greeting(name); } @Funq public String funqyHello() { return "hello funqy"; } }`

Save the file.

Access the new

`greeting`

function by using the`curl`

command on your local terminal:`curl -d '"Dan"' -X POST localhost:8080/api/greeting`

The output should look like this:

`"Welcome to build Serverless Java with Quarkus on Azure Functions, Dan"`

Important

Live Coding (also called dev mode) allows you to run the app and make changes on the fly. Quarkus will automatically recompile and reload the app when changes are made. This is a powerful and efficient style of developing that you'll use throughout this article.

Before you move forward to the next step, stop Quarkus dev mode by selecting Ctrl+C.


## Deploy the app to Azure

If you haven't already, sign in to your Azure subscription by using the following

[az login](/en-us/cli/azure/reference-index)command and follow the on-screen directions:`az login`

Note

If multiple Azure tenants are associated with your Azure credentials, you must specify which tenant you want to sign in to. You can do this by using the

`--tenant`

option. For example:`az login --tenant contoso.onmicrosoft.com`

.Continue the process in the web browser. If no web browser is available or if the web browser fails to open, use device code flow with

`az login --use-device-code`

.After you sign in successfully, the output on your local terminal should look similar to the following:

`xxxxxxx-xxxxx-xxxx-xxxxx-xxxxxxxxx 'Microsoft' [ { "cloudName": "AzureCloud", "homeTenantId": "xxxxxx-xxxx-xxxx-xxxx-xxxxxxx", "id": "xxxxxx-xxxx-xxxx-xxxx-xxxxxxxx", "isDefault": true, "managedByTenants": [], "name": "Contoso account services", "state": "Enabled", "tenantId": "xxxxxxx-xxxx-xxxx-xxxxx-xxxxxxxxxx", "user": { "name": "user@contoso.com", "type": "user" } } ]`

Build and deploy the functions to Azure.

The

*pom.xml*file that you generated in the previous step uses`azure-functions-maven-plugin`

. Running`mvn install`

generates configuration files and a staging directory that`azure-functions-maven-plugin`

requires. For`yourResourceGroupName`

, use the value that you used previously.`mvn clean install -DskipTests -DtenantId=<your tenantId from shown previously> -DresourceGroup=<yourResourceGroupName> azure-functions:deploy`

During deployment, sign in to Azure. The

`azure-functions-maven-plugin`

plug-in is configured to prompt for Azure sign-in each time the project is deployed. During the build, output similar to the following appears:`[INFO] Auth type: DEVICE_CODE To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AXCWTLGMP to authenticate.`

Do as the output says and authenticate to Azure by using the browser and the provided device code. Many other authentication and configuration options are available. The complete reference documentation for

`azure-functions-maven-plugin`

is available at[Azure Functions: Configuration Details](https://github.com/microsoft/azure-maven-plugins/wiki/Azure-Functions:-Configuration-Details).After authentication, the build should continue and finish. Make sure that output includes

`BUILD SUCCESS`

near the end.`Successfully deployed the artifact to https://quarkus-demo-123451234.azurewebsites.net`

You can also find the URL to trigger your function on Azure in the output log:

`[INFO] HTTP Trigger Urls: [INFO] quarkus : https://quarkus-azure-functions-http-archetype-20220629204040017.azurewebsites.net/api/{*path}`

It will take a while for the deployment to finish. In the meantime, let's explore Azure Functions in the Azure portal.


## Access and monitor the serverless function on Azure

Sign in to [the portal](https://aka.ms/publicportal) and ensure that you've selected the same tenant and subscription that you used in the Azure CLI.

Type

**function app**on the search bar at the top of the Azure portal and select the Enter key. Your function app should be deployed and show up with the name`<yourResourceGroupName>-function-quarkus`

.Select the function app to show detailed information, such as

**Location**,**Subscription**,**URL**,**Metrics**, and**App Service Plan**. Then, select the**URL**value.Confirm that the welcome page says your function app is "up and running."

Invoke the

`greeting`

function by using the following`curl`

command on your local terminal.Important

Replace

`YOUR_HTTP_TRIGGER_URL`

with your own function URL that you find in the Azure portal or output.`curl -d '"Dan on Azure"' -X POST https://YOUR_HTTP_TRIGGER_URL/api/greeting`

The output should look similar to the following:

`"Welcome to build Serverless Java with Quarkus on Azure Functions, Dan on Azure"`

You can also access the other function (

`funqyHello`

) by using the following`curl`

command:`curl https://YOUR_HTTP_TRIGGER_URL/api/funqyHello`

The output should be the same as what you observed earlier:

`"hello funqy"`

If you want to exercise the basic metrics capability in the Azure portal, try invoking the function within a shell

`for`

loop:`for i in {1..100}; do curl -d '"Dan on Azure"' -X POST https://YOUR_HTTP_TRIGGER_URL/api/greeting; done`

After a while, you'll see some metrics data in the portal.


Now that you've opened your Azure function in the portal, here are more features that you can access from the portal:

- Monitor the performance of your Azure function. For more information, see
[Monitoring Azure Functions](monitor-functions). - Explore telemetry. For more information, see
[Analyze Azure Functions telemetry in Application Insights](analyze-telemetry-data). - Set up logging. For more information, see
[Enable streaming execution logs in Azure Functions](streaming-logs).

## Clean up resources

If you don't need these resources, you can delete them by running the following command:

```
az group delete --name <yourResourceGroupName> --yes
```


## Next steps

In this article, you learned how to:

- Run Quarkus dev mode.
- Deploy a Funqy app to Azure functions by using
`azure-functions-maven-plugin`

. - Examine the performance of the function in the portal.

To learn more about Azure Functions and Quarkus, see the following articles and references:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/security-baseline -->

# Azure security baseline for Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This security baseline applies guidance from the [Microsoft cloud security benchmark version 1.0](/en-us/security/benchmark/azure/overview) to Functions. The Microsoft cloud security benchmark provides recommendations on how you can secure your cloud solutions on Azure. The content is grouped by the security controls defined by the Microsoft cloud security benchmark and the related guidance applicable to Functions.

You can monitor this security baseline and its recommendations using Microsoft Defender for Cloud. Azure Policy definitions will be listed in the Regulatory Compliance section of the Microsoft Defender for Cloud portal page.

When a feature has relevant Azure Policy Definitions, they are listed in this baseline to help you measure compliance with the Microsoft cloud security benchmark controls and recommendations. Some recommendations may require a paid Microsoft Defender plan to enable certain security scenarios.

Note

**Features** not applicable to Functions have been excluded. To see how Functions completely maps to the Microsoft cloud security benchmark, see the ** full Functions security baseline mapping file**.

## Security profile

The security profile summarizes high-impact behaviors of Functions, which may result in increased security considerations.

| Service Behavior Attribute | Value |
|---|---|
| Product Category | Compute, Web |
| Customer can access HOST / OS | No Access |
| Service can be deployed into customer's virtual network | True |
| Stores customer content at rest | True |

## Network security

*For more information, see the Microsoft cloud security benchmark: Network security.*

### NS-1: Establish network segmentation boundaries

#### Features

##### Virtual Network Integration

**Description**: Service supports deployment into customer's private Virtual Network (VNet). [Learn more](/en-us/azure/virtual-network/virtual-network-for-azure-services#services-that-can-be-deployed-into-a-virtual-network).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Deploy the service into a virtual network. Assign private IPs to the resource (where applicable) unless there is a strong reason to assign public IPs directly to the resource.

**Note**: Networking features are exposed by the service but need to be configured for the application. By default, public network access is allowed.

**Reference**: [Azure Functions networking options](/en-us/azure/azure-functions/functions-networking-options)

##### Network Security Group Support

**Description**: Service network traffic respects Network Security Groups rule assignment on its subnets. [Learn more](/en-us/azure/virtual-network/network-security-groups-overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Use network security groups (NSG) to restrict or monitor traffic by port, protocol, source IP address, or destination IP address. Create NSG rules to restrict your service's open ports (such as preventing management ports from being accessed from untrusted networks). Be aware that by default, NSGs deny all inbound traffic but allow traffic from virtual network and Azure Load Balancers.

**Reference**: [Azure Functions networking options](/en-us/azure/azure-functions/functions-networking-options)

### NS-2: Secure cloud services with network controls

#### Features

##### Azure Private Link

**Description**: Service native IP filtering capability for filtering network traffic (not to be confused with NSG or Azure Firewall). [Learn more](/en-us/azure/private-link/private-link-overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Deploy private endpoints for all Azure resources that support the Private Link feature, to establish a private access point for the resources.

**Reference**: [Azure Functions networking options](/en-us/azure/azure-functions/functions-networking-options)

##### Disable Public Network Access

**Description**: Service supports disabling public network access either through using service-level IP ACL filtering rule (not NSG or Azure Firewall) or using a 'Disable Public Network Access' toggle switch. [Learn more](/en-us/security/benchmark/azure/security-controls-v3-network-security#ns-2-secure-cloud-services-with-network-controls).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: Azure Functions can be configured with private endpoints, but there is not presently a single toggle for disabling public network access absent configuring private endpoints.

**Configuration Guidance**: Disable public network access either using the service-level IP ACL filtering rule or a toggling switch for public network access.

## Identity management

*For more information, see the Microsoft cloud security benchmark: Identity management.*

### IM-1: Use centralized identity and authentication system

#### Features

##### Azure AD Authentication Required for Data Plane Access

**Description**: Service supports using Azure AD authentication for data plane access. [Learn more](/en-us/azure/active-directory/authentication/overview-authentication).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: Customer-owned endpoints may be configured to require Azure AD authentication requirements. System-provided endpoints for deployment operations and advanced developer tools support Azure AD but by default have the ability to alternatively use publishing credentials. These publishing credentials can be disabled. Some data plane endpoints on the app may be accessed by administrative keys configured in the Functions host, and these are not configurable with Azure AD requirements at this time.

**Configuration Guidance**: Use Azure Active Directory (Azure AD) as the default authentication method to control your data plane access.

**Reference**: [Configure deployment credentials - disable basic authentication](/en-us/azure/app-service/deploy-configure-credentials#disable-basic-authentication)

##### Local Authentication Methods for Data Plane Access

**Description**: Local authentications methods supported for data plane access, such as a local username and password. [Learn more](/en-us/azure/app-service/overview-authentication-authorization).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | True | Microsoft |

**Feature notes**: Deployment credentials are created by default, but they can be disabled. Some operations exposed by the application runtime may be performed using an administrative key, which cannot presently be disabled. This key can be stored in Azure Key Vault, and it can be regenerated at any time. Avoid the usage of local authentication methods or accounts, these should be disabled wherever possible. Instead use Azure AD to authenticate where possible.

**Configuration Guidance**: No additional configurations are required as this is enabled on a default deployment.

**Reference**: [Disable basic authentication](/en-us/azure/app-service/deploy-configure-credentials?tabs=cli#disable-basic-authentication)

### IM-3: Manage application identities securely and automatically

#### Features

##### Managed Identities

**Description**: Data plane actions support authentication using managed identities. [Learn more](/en-us/azure/active-directory/managed-identities-azure-resources/overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Use Azure managed identities instead of service principals when possible, which can authenticate to Azure services and resources that support Azure Active Directory (Azure AD) authentication. Managed identity credentials are fully managed, rotated, and protected by the platform, avoiding hard-coded credentials in source code or configuration files.

**Reference**: [How to use managed identities for App Service and Azure Functions](/en-us/azure/app-service/overview-managed-identity?toc=%2Fazure%2Fazure-functions%2Ftoc.json)

##### Service Principals

**Description**: Data plane supports authentication using service principals. [Learn more](/en-us/powershell/azure/create-azure-service-principal-azureps).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: There is no current Microsoft guidance for this feature configuration. Please review and determine if your organization wants to configure this security feature.

#### Microsoft Defender for Cloud monitoring

**Azure Policy built-in definitions - Microsoft.Web**:

Name(Azure portal) |
Description | Effect(s) | Version(GitHub) |
|---|---|---|---|
|

[3.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Service/UseManagedIdentity_WebApp_Audit.json)### IM-7: Restrict resource access based on conditions

#### Features

##### Conditional Access for Data Plane

**Description**: Data plane access can be controlled using Azure AD Conditional Access Policies. [Learn more](/en-us/azure/active-directory/conditional-access/overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: For data plane endpoints which are not defined by the application, conditional access would need to be configured against Azure Service Management.

**Configuration Guidance**: Define the applicable conditions and criteria for Azure Active Directory (Azure AD) conditional access in the workload. Consider common use cases such as blocking or granting access from specific locations, blocking risky sign-in behavior, or requiring organization-managed devices for specific applications.

### IM-8: Restrict the exposure of credential and secrets

#### Features

##### Service Credential and Secrets Support Integration and Storage in Azure Key Vault

**Description**: Data plane supports native use of Azure Key Vault for credential and secrets store. [Learn more](/en-us/azure/key-vault/secrets/about-secrets).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Ensure that secrets and credentials are stored in secure locations such as Azure Key Vault, instead of embedding them into code or configuration files.

**Reference**: [Use Key Vault references for App Service and Azure Functions](/en-us/azure/app-service/app-service-key-vault-references?toc=%2Fazure%2Fazure-functions%2Ftoc.json)

## Privileged access

*For more information, see the Microsoft cloud security benchmark: Privileged access.*

### PA-1: Separate and limit highly privileged/administrative users

#### Features

##### Local Admin Accounts

**Description**: Service has the concept of a local administrative account. [Learn more](/en-us/security/benchmark/azure/security-controls-v3-privileged-access#pa-1-separate-and-limit-highly-privilegedadministrative-users).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| False | Not Applicable | Not Applicable |

**Configuration Guidance**: This feature is not supported to secure this service.

### PA-7: Follow just enough administration (least privilege) principle

#### Features

##### Azure RBAC for Data Plane

**Description**: Azure Role-Based Access Control (Azure RBAC) can be used to managed access to service's data plane actions. [Learn more](/en-us/azure/role-based-access-control/overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: The only data-plane actions which can leverage Azure RBAC are the Kudu/SCM/deployment endpoints. These require permission over the `Microsoft.Web/sites/publish/Action`

operation. Endpoints exposed by the customer application itself are not covered by Azure RBAC.

**Configuration Guidance**: Use Azure role-based access control (Azure RBAC) to manage Azure resource access through built-in role assignments. Azure RBAC roles can be assigned to users, groups, service principals, and managed identities.

**Reference**: [RBAC permissions required to access Kudu](/en-us/azure/app-service/resources-kudu#rbac-permissions-required-to-access-kudu)

### PA-8: Determine access process for cloud provider support

#### Features

##### Customer Lockbox

**Description**: Customer Lockbox can be used for Microsoft support access. [Learn more](/en-us/azure/security/fundamentals/customer-lockbox-overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: In support scenarios where Microsoft needs to access your data, use Customer Lockbox to review, then approve or reject each of Microsoft's data access requests.

## Data protection

*For more information, see the Microsoft cloud security benchmark: Data protection.*

### DP-2: Monitor anomalies and threats targeting sensitive data

#### Features

##### Data Leakage/Loss Prevention

**Description**: Service supports DLP solution to monitor sensitive data movement (in customer's content). [Learn more](/en-us/security/benchmark/azure/security-controls-v3-data-protection#dp-2-monitor-anomalies-and-threats-targeting-sensitive-data).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| False | Not Applicable | Not Applicable |

**Configuration Guidance**: This feature is not supported to secure this service.

### DP-3: Encrypt sensitive data in transit

#### Features

##### Data in Transit Encryption

**Description**: Service supports data in-transit encryption for data plane. [Learn more](/en-us/azure/security/fundamentals/double-encryption#data-in-transit).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: Function apps are created by default to support TLS 1.2 as a minimum version, but an app can be configured with a lower version through a configuration setting. HTTPS is not required of incoming requests by default, but this can also be set via a configuration setting, at which point any HTTP request will be automatically redirected to use HTTPS.

**Configuration Guidance**: Enable secure transfer in services where there is a native data in transit encryption feature built in. Enforce HTTPS on any web applications and services and ensure TLS v1.2 or later is used. Legacy versions such as SSL 3.0, TLS v1.0 should be disabled. For remote management of Virtual Machines, use SSH (for Linux) or RDP/TLS (for Windows) instead of an unencrypted protocol.

**Reference**: [Add and manage TLS/SSL certificates in Azure App Service](/en-us/azure/app-service/configure-ssl-certificate?toc=%2Fazure%2Fazure-functions%2Ftoc.json&tabs=apex%2Cportal)

#### Microsoft Defender for Cloud monitoring

**Azure Policy built-in definitions - Microsoft.Web**:

Name(Azure portal) |
Description | Effect(s) | Version(GitHub) |
|---|---|---|---|
|

[4.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/App%20Service/Webapp_AuditHTTP_Audit.json)### DP-4: Enable data at rest encryption by default

#### Features

##### Data at Rest Encryption Using Platform Keys

**Description**: Data at-rest encryption using platform keys is supported, any customer content at rest is encrypted with these Microsoft managed keys. [Learn more](/en-us/azure/security/fundamentals/encryption-atrest#encryption-at-rest-in-microsoft-cloud-services).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | True | Microsoft |

**Configuration Guidance**: No additional configurations are required as this is enabled on a default deployment.

### DP-5: Use customer-managed key option in data at rest encryption when required

#### Features

##### Data at Rest Encryption Using CMK

**Description**: Data at-rest encryption using customer-managed keys is supported for customer content stored by the service. [Learn more](/en-us/azure/security/fundamentals/encryption-models).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: Azure Functions does not directly support this feature, but an application can be configured to leverage services which do, in place of any possible data storage in Functions. Azure Files may be mounted as the file system, all App Settings, including secrets, may be stored in Azure Key Vault, and deployment options such as run-from-package may pull content from Azure Blob storage.

**Configuration Guidance**: If required for regulatory compliance, define the use case and service scope where encryption using customer-managed keys are needed. Enable and implement data at rest encryption using customer-managed key for those services.

**Reference**: [Encrypt your application data at rest using customer-managed keys](/en-us/azure/azure-functions/configure-encrypt-at-rest-using-cmk)

### DP-6: Use a secure key management process

#### Features

##### Key Management in Azure Key Vault

**Description**: The service supports Azure Key Vault integration for any customer keys, secrets, or certificates. [Learn more](/en-us/azure/key-vault/general/overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Use Azure Key Vault to create and control the life cycle of your encryption keys, including key generation, distribution, and storage. Rotate and revoke your keys in Azure Key Vault and your service based on a defined schedule or when there is a key retirement or compromise. When there is a need to use customer-managed key (CMK) in the workload, service, or application level, ensure you follow the best practices for key management: Use a key hierarchy to generate a separate data encryption key (DEK) with your key encryption key (KEK) in your key vault. Ensure keys are registered with Azure Key Vault and referenced via key IDs from the service or application. If you need to bring your own key (BYOK) to the service (such as importing HSM-protected keys from your on-premises HSMs into Azure Key Vault), follow recommended guidelines to perform initial key generation and key transfer.

**Reference**: [Use Key Vault references for App Service and Azure Functions](/en-us/azure/app-service/app-service-key-vault-references?toc=%2Fazure%2Fazure-functions%2Ftoc.json)

### DP-7: Use a secure certificate management process

#### Features

##### Certificate Management in Azure Key Vault

**Description**: The service supports Azure Key Vault integration for any customer certificates. [Learn more](/en-us/azure/key-vault/certificates/certificate-scenarios).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Use Azure Key Vault to create and control the certificate lifecycle, including creation, importing, rotation, revocation, storage, and purging of the certificate. Ensure the certificate generation follows defined standards without using any insecure properties, such as: insufficient key size, overly long validity period, insecure cryptography. Setup automatic rotation of the certificate in Azure Key Vault and the Azure service (if supported) based on a defined schedule or when there is a certificate expiration. If automatic rotation is not supported in the application, ensure they are still rotated using manual methods in Azure Key Vault and the application.

**Reference**: [Add a TLS/SSL certificate in Azure App Service](/en-us/azure/app-service/configure-ssl-certificate)

## Asset management

*For more information, see the Microsoft cloud security benchmark: Asset management.*

### AM-2: Use only approved services

#### Features

##### Azure Policy Support

**Description**: Service configurations can be monitored and enforced via Azure Policy. [Learn more](/en-us/azure/governance/policy/tutorials/create-and-manage).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Use Microsoft Defender for Cloud to configure Azure Policy to audit and enforce configurations of your Azure resources. Use Azure Monitor to create alerts when there is a configuration deviation detected on the resources. Use Azure Policy [deny] and [deploy if not exists] effects to enforce secure configuration across Azure resources.

## Logging and threat detection

*For more information, see the Microsoft cloud security benchmark: Logging and threat detection.*

### LT-1: Enable threat detection capabilities

#### Features

##### Microsoft Defender for Service / Product Offering

**Description**: Service has an offering-specific Microsoft Defender solution to monitor and alert on security issues. [Learn more](/en-us/azure/security-center/azure-defender).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: Defender for App Service includes Azure Functions. If this solution is enabled, function apps under the enablement scope will be included.

**Configuration Guidance**: Use Azure Active Directory (Azure AD) as the default authentication method to control your management plane access. When you get an alert from Microsoft Defender for Key Vault, investigate and respond to the alert.

**Reference**: [Defender for App Service](/en-us/azure/defender-for-cloud/defender-for-app-service-introduction)

### LT-4: Enable logging for security investigation

#### Features

##### Azure Resource Logs

**Description**: Service produces resource logs that can provide enhanced service-specific metrics and logging. The customer can configure these resource logs and send them to their own data sink like a storage account or log analytics workspace. [Learn more](/en-us/azure/azure-monitor/platform/platform-logs-overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Configuration Guidance**: Enable resource logs for the service. For example, Key Vault supports additional resource logs for actions that get a secret from a key vault or and Azure SQL has resource logs that track requests to a database. The content of resource logs varies by the Azure service and resource type.

**Reference**: [Monitoring Azure Functions with Azure Monitor Logs](/en-us/azure/azure-functions/functions-monitor-log-analytics)

## Backup and recovery

*For more information, see the Microsoft cloud security benchmark: Backup and recovery.*

### BR-1: Ensure regular automated backups

#### Features

##### Azure Backup

**Description**: The service can be backed up by the Azure Backup service. [Learn more](/en-us/azure/backup/backup-overview).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| False | Not Applicable | Not Applicable |

**Feature notes**: A feature for backing up an application is available if hosted on a Standard, Premium, or Isolated App Service plan. This feature does not leverage Azure Backup and does not include event sources or externally linked storage. See /azure/app-service/manage-backup for more details.

**Configuration Guidance**: This feature is not supported to secure this service.

##### Service Native Backup Capability

**Description**: Service supports its own native backup capability (if not using Azure Backup). [Learn more](/en-us/security/benchmark/azure/security-controls-v3-backup-recovery#br-1-ensure-regular-automated-backups).

| Supported | Enabled By Default | Configuration Responsibility |
|---|---|---|
| True | False | Customer |

**Feature notes**: A backup feature is available to apps running on Standard, Premium, and Isolated App Service plans. This does not include backing up event sources or externally provided storage.

**Configuration Guidance**: There is no current Microsoft guidance for this feature configuration. Please review and determine if your organization wants to configure this security feature.

**Reference**: [Back up and restore your app in Azure App Service](/en-us/azure/app-service/manage-backup)

## Next steps

- See the
[Microsoft cloud security benchmark overview](../overview) - Learn more about
[Azure security baselines](../security-baselines-overview)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/scenario-database-changes-azure-cosmosdb -->

# Quickstart: Respond to database changes in Azure Cosmos DB using Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this Quickstart, you use Visual Studio Code to build an app that responds to database changes in a No SQL database in Azure Cosmos DB. After testing the code locally, you deploy it to a new serverless function app you create running in a Flex Consumption plan in Azure Functions.

The project source uses the Azure Developer CLI (azd) extension with Visual Studio Code to simplify initializing and verifying your project code locally, as well as and deploying your code to Azure. This deployment follows current best practices for secure and scalable Azure Functions deployments.

Important

While responding to [changes in an Azure Cosmos DB No SQL database](functions-bindings-cosmosdb-v2-trigger) is supported for all languages, this quickstart scenario currently only has examples for C#, Python, and TypeScript. To complete this quickstart, select one of these supported languages at the top of the article.

## Prerequisites

An Azure account with an active subscription.

[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).[Visual Studio Code](https://code.visualstudio.com/)on one of the[supported platforms](https://code.visualstudio.com/docs/supporting/requirements#_platforms).The

[Azure Functions extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.vscode-azurefunctions)for Visual Studio Code. This extension requires[Azure Functions Core Tools](functions-run-local). When this tool isn't available locally, the extension tries to install it by using a package-based installer. You can also install or update the Core Tools package by running`Azure Functions: Install or Update Azure Functions Core Tools`

from the command palette. If you don't have npm or Homebrew installed on your local computer, you must instead[manually install or update Core Tools](functions-run-local#install-the-azure-functions-core-tools).

[C# extension](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csharp)for Visual Studio Code.

[Node.js 18.x](https://nodejs.org/en/about/previous-releases)or above. Use the`node --version`

command to check your version.

Python versions that are

[supported by Azure Functions](supported-languages#languages-by-runtime-version). For more information, see[How to install Python](https://wiki.python.org/moin/BeginnersGuide/Download).The

[Python extension](https://marketplace.visualstudio.com/items?itemName=ms-python.python)for Visual Studio Code.

- The
[Azure Developer CLI extension](https://marketplace.visualstudio.com/items?itemName=ms-azuretools.azure-dev)for Visual Studio Code.

## Initialize the project

You can use the `azd init`

command from the command palette to create a local Azure Functions code project from a template.

In Visual Studio Code, open a folder or workspace in which you want to create your project.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Initialize App (init)`

, and then choose**Select a template**.There might be a slight delay while

`azd`

initializes the current folder or workspace.

When prompted, choose

**Select a template**, then search for and select`Azure Functions with Cosmos DB Bindings (.NET)`

.When prompted, enter a unique environment name, such as

`cosmosdbchanges-dotnet`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-cosmosdb)and initializes the project in the current folder or workspace. In`azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

When prompted, choose

**Select a template**, then search for and select`Azure Functions TypeScript CosmosDB trigger`

.When prompted, enter a unique environment name, such as

`cosmosdbchanges-ts`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-cosmosdb)and initializes the project in the current folder or workspace. In`azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

When prompted, choose

**Select a template**, then search for and select`Azure Functions Python with CosmosDB triggers and bindings...`

.When prompted, enter a unique environment name, such as

`cosmosdbchanges-py`

.This command pulls the project files from the

[template repository](https://github.com/Azure-Samples/functions-quickstart-python-azd-cosmosdb)and initializes the project in the current folder or workspace. In`azd`

, the environment is used to maintain a unique deployment context for your app, and you can define more than one. It's also part of the name of the resource group you create in Azure.

Run this command, depending on your local operating system, to grant configuration scripts the required permissions:

Run this command with sufficient privileges:

`chmod +x ./infra/scripts/*.sh`


Before you can run your app locally, you must create the resources in Azure. This project doesn't use local emulation for Azure Cosmos DB.

## Create Azure resources

This project is configured to use the `azd provision`

command to create a function app in a Flex Consumption plan, along with other required Azure resources that follows current best practices.

In Visual Studio Code, press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Sign In with Azure Developer CLI`

, and then sign in using your Azure account.Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Provision Azure resources (provision)`

to create the required Azure resources:When prompted in the Terminal window, provide these required deployment parameters:

Prompt Description Select an Azure Subscription to use Choose the subscription in which you want your resources to be created. *location*deployment parameterAzure region in which to create the resource group that contains the new Azure resources. Only regions that currently support the Flex Consumption plan are shown. *vnetEnabled*deployment parameterWhile the template supports creating resources inside a virtual network, to simplify deployment and testing, choose `False`

.The

`azd provision`

command uses your response to these prompts with the Bicep configuration files to create and configure these required Azure resources, following the latest best practices:- Flex Consumption plan and function app
- Azure Cosmos DB account
- Azure Storage (required) and Application Insights (recommended)
- Access policies and roles for your account
- Service-to-service connections using managed identities (instead of stored connection strings)

Post-provision hooks also generate the

*local.settings.json*file required when running locally. This file also contains the settings required to connect to your Azure Cosmos DB database in Azure.Tip

Should any steps fail during provisioning, you can rerun the

`azd provision`

command again after resolving any issues.After the command completes successfully, you can run your project code locally and trigger on the Azure Cosmos DB database in Azure.


## Run the function locally

Visual Studio Code integrates with [Azure Functions Core tools](functions-run-local) to let you run this project on your local development computer before you publish to your new function app in Azure.

Press

`F1`and in the command palette search for and run the command`Azurite: Start`

.To start the function locally, press

`F5`or the**Run and Debug**icon in the left-hand side Activity bar. The**Terminal**panel displays the output from Core Tools. Your app starts in the**Terminal**panel, and you can see the name of the function that's running locally.If you have trouble running on Windows, make sure that the default terminal for Visual Studio Code isn't set to

**WSL Bash**.With Core Tools still running in

**Terminal**, press`F1`and in the command palette search for and run the command`NoSQL: Create Item...`

and select both the`document-db`

database and the`documents`

container.Replace the contents of the

*New Item.json*file with this JSON data and select**Save**:`{ "id": "doc1", "title": "Sample document", "content": "This is a sample document for testing my Azure Cosmos DB trigger in Azure Functions." }`

After you select

**Save**, you see the execution of the function in the terminal and the local document is updated to include metadata added by the service.When you're done, press Ctrl+C in the terminal window to stop the

`func.exe`

host process.

## Review the code (optional)

The function is triggered based on the change feed in an Azure Cosmos DB NoSQL database. These environment variables configure how the trigger monitors the change feed:

`COSMOS_CONNECTION__accountEndpoint`

: The Cosmos DB account endpoint`COSMOS_DATABASE_NAME`

: The name of the database to monitor`COSMOS_CONTAINER_NAME`

: The name of the container to monitor

These environment variables are created for you both in Azure (function app settings) and locally (local.settings.json) during the `azd provision`

operation.

You can review the code that defines the Azure Cosmos DB trigger in the [CosmosTrigger.cs project file](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd-cosmosdb/blob/main/CosmosTrigger.cs).

You can review the code that defines the Azure Cosmos DB trigger in the [cosmos_trigger.ts project file](https://github.com/Azure-Samples/functions-quickstart-typescript-azd-cosmosdb/blob/main/src/functions/cosmos_trigger.ts).

You can review the code that defines the Azure Cosmos DB trigger in the [function_app.py project file](https://github.com/Azure-Samples/functions-quickstart-python-azd-cosmosdb/blob/main/function_app.py).

After you review and verify your function code locally, it's time to publish the project to Azure.

## Deploy to Azure

You can run the `azd deploy`

command from Visual Studio Code to deploy the project code to your already provisioned resources in Azure.

Press

`F1`to open the command palette, search for and run the command`Azure Developer CLI (azd): Deploy to Azure (deploy)`

.The

`azd deploy`

command packages and deploys your code to the deployment container. The app is then started and runs in the deployed package.After the command completes successfully, your app is running in Azure.


## Invoke the function on Azure

In Visual Studio Code, press

`F1`and in the command palette search for and run the command`Azure: Open in portal`

, select`Function app`

, and choose your new app. Sign in with your Azure account, if necessary.This command opens your new function app in the Azure portal.

In the

**Overview**tab on the main page, select your function app name and then the**Logs**tab.Use the

`NoSQL: Create Item`

command in Visual Studio Code to again add a document to the container as before.Verify again that the function gets triggered by an update in the monitored container.


## Redeploy your code

You can run the `azd deploy`

command as many times as you need to deploy code updates to your function app.

Note

Deployed code files are always overwritten by the latest deployment package.

Your initial responses to `azd`

prompts and any environment variables generated by `azd`

are stored locally in your named environment. Use the `azd env get-values`

command to review all of the variables in your environment that were used when creating Azure resources.

## Clean up resources

When you're done working with your function app and related resources, you can use this command to delete the function app and its related resources from Azure and avoid incurring any further costs:

```
azd down --no-prompt
```


Note

The `--no-prompt`

option instructs `azd`

to delete your resource group without a confirmation from you.

This command doesn't affect your local code project.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-signalr-service-input -->

# SignalR Service input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Before a client can connect to Azure SignalR Service, it must retrieve the service endpoint URL and a valid access token. The *SignalRConnectionInfo* input binding produces the SignalR Service endpoint URL and a valid token that are used to connect to the service. The token is time-limited and can be used to authenticate a specific user to a connection. Therefore, you shouldn't cache the token or share it between clients. Usually you use *SignalRConnectionInfo* with HTTP trigger for clients to retrieve the connection information.

For more information on how to use this binding to create a "negotiate" function that is compatible with a SignalR client SDK, see [Azure Functions development and configuration with Azure SignalR Service](../azure-signalr/signalr-concept-serverless-development-config).

When not explicitly declared, assume that examples are using the default connection setting value of `AzureSignalRConnectionString`

. For information on setup and configuration details, see the [overview](functions-bindings-signalr-service).

## Example

You can create a C# function by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. An isolated worker process is required to support C# functions running on long-term support (LTS) and non-LTS versions for .NET and the .NET Framework.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Azure Functions runtime.[C# script](functions-reference-csharp): Used primarily when you create C# functions in the Azure portal.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

The following example shows a [C# function](dotnet-isolated-process-guide) that acquires SignalR connection information using the input binding and returns it over HTTP.

```
[Function(nameof(Negotiate))]
public static string Negotiate([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[SignalRConnectionInfoInput(HubName = "serverless")] string connectionInfo)
{
// The serialization of the connection info object is done by the framework. It should be camel case. The SignalR client respects the camel case response only.
return connectionInfo;
}
```


The following example shows a SignalR connection info input binding in a *function.json* file and a function that uses the binding to return the connection information.

Here's binding data for the example in the *function.json* file:

```
{
"type": "signalRConnectionInfo",
"name": "connectionInfo",
"hubName": "hubName1",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "in"
}
```


Here's the JavaScript code:

```
const { app, input } = require('@azure/functions');
const inputSignalR = input.generic({
type: 'signalRConnectionInfo',
name: 'connectionInfo',
hubName: 'hubName1',
connectionStringSetting: 'AzureSignalRConnectionString',
});
app.post('negotiate', {
authLevel: 'function',
handler: (request, context) => {
return { body: JSON.stringify(context.extraInputs.get(inputSignalR)) }
},
route: 'negotiate',
extraInputs: [inputSignalR],
});
```


Complete PowerShell examples are pending.

The following example shows a SignalR connection info input binding in a *function.json* file and a [Python function](functions-reference-python) that uses the binding to return the connection information.

Here's the Python code:

```
def main(req: func.HttpRequest, connectionInfoJson: str) -> func.HttpResponse:
return func.HttpResponse(
connectionInfoJson,
status_code=200,
headers={
'Content-type': 'application/json'
}
)
```


The following example shows a [Java function](functions-reference-java) that acquires SignalR connection information using the input binding and returns it over HTTP.

```
@FunctionName("negotiate")
public SignalRConnectionInfo negotiate(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> req,
@SignalRConnectionInfoInput(
name = "connectionInfo",
HubName = "hubName1") SignalRConnectionInfo connectionInfo) {
return connectionInfo;
}
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attribute to define the function. C# script instead uses a function.json configuration file.

The following table explains the properties of the `SignalRConnectionInfoInput`

attribute:

| Attribute property | Description |
|---|---|
HubName |
Required. The hub name. |
ConnectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
UserId |
Optional. The user identifier of a SignalR connection. You can use a
|

**IdToken****ClaimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**ClaimTypeList****IdToken**.## Annotations

The following table explains the supported settings for the `SignalRConnectionInfoInput`

annotation.

| Setting | Description |
|---|---|
name |
Variable name used in function code for connection info object. |
hubName |
Required. The hub name. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
userId |
Optional. The user identifier of a SignalR connection. You can use a
|

**idToken****claimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**claimTypeList****idToken**.## Annotations

The following table explains the supported settings for the `SignalRConnectionInfoInput`

annotation.

| Setting | Description |
|---|---|
name |
Variable name used in function code for connection info object. |
hubName |
Required. The hub name. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
userId |
Optional. The user identifier of a SignalR connection. You can use a
|

**idToken****claimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**claimTypeList****idToken**.## Configuration

The following table explains the binding configuration properties that you set in the *function.json* file.

| function.json property | Description |
|---|---|
type |
Must be set to `signalRConnectionInfo` . |
direction |
Must be set to `in` . |
hubName |
Required. The hub name. |
connectionStringSetting |
The name of the app setting or settings collection that contains the SignalR Service connection string, which defaults to `AzureSignalRConnectionString` . |
userId |
Optional. The user identifier of a SignalR connection. You can use a
|

**idToken****claimTypeList**. You can use a[binding expression](#binding-expressions-for-http-trigger)to bind the value to an HTTP request header or query.**claimTypeList****idToken**.Warning

For the simplicity, we omit the authentication and authorization parts in this sample. As a result, this endpoint is publicly accessible without any restrictions. To ensure the security of your negotiation endpoint, you should implement appropriate authentication and authorization mechanisms based on your specific requirements. For guidance on protecting your HTTP endpoints, see the following articles:

## Usage

### Managed identity-based connections

For optimal security, your function app should use managed identities when connecting to the Azure SignalR service instead of using a connection string, which contains a shared secret key. For more information, see [Authorize requests to Azure SignalR Service resources with Microsoft Entra managed identities](../azure-signalr/signalr-howto-authorize-managed-identity#azure-signalr-service-bindings-in-azure-functions).

### Authenticated tokens

When an authenticated client triggers the function, you can add a user ID claim to the generated token. You can easily add authentication to a function app using [App Service Authentication](../app-service/overview-authentication-authorization).

App Service authentication sets HTTP headers named `x-ms-client-principal-id`

and `x-ms-client-principal-name`

that contain the authenticated user's client principal ID and name, respectively.

You can set the `UserId`

property of the binding to the value from either header using a [binding expression](#binding-expressions-for-http-trigger): `{headers.x-ms-client-principal-id}`

or `{headers.x-ms-client-principal-name}`

.

```
[Function("Negotiate")]
public static string Negotiate([HttpTrigger(AuthorizationLevel.Anonymous)] HttpRequestData req,
[SignalRConnectionInfoInput(HubName = "hubName1", UserId = "{headers.x-ms-client-principal-id}")] string connectionInfo)
{
// The serialization of the connection info object is done by the framework. It should be camel case. The SignalR client respects the camel case response only.
return connectionInfo;
}
```


```
@FunctionName("negotiate")
public SignalRConnectionInfo negotiate(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST, HttpMethod.GET },
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> req,
@SignalRConnectionInfoInput(name = "connectionInfo", hubName = "hubName1", userId = "{headers.x-ms-signalr-userid}") SignalRConnectionInfo connectionInfo) {
return connectionInfo;
}
```


Here's binding data in the *function.json* file:

```
{
"type": "signalRConnectionInfo",
"name": "connectionInfo",
"hubName": "hubName1",
"userId": "{headers.x-ms-client-principal-id}",
"connectionStringSetting": "<name of setting containing SignalR Service connection string>",
"direction": "in"
}
```


Here's the JavaScript code:

```
const { app, input } = require('@azure/functions');
const inputSignalR = input.generic({
type: 'signalRConnectionInfo',
name: 'connectionInfo',
hubName: 'hubName1',
connectionStringSetting: 'AzureSignalRConnectionString',
userId: '{headers.x-ms-client-principal-id}',
});
app.post('negotiate', {
authLevel: 'function',
handler: (request, context) => {
return { body: JSON.stringify(context.extraInputs.get(inputSignalR)) }
},
route: 'negotiate',
extraInputs: [inputSignalR],
});
```


Complete PowerShell examples are pending.

Here's the Python code:

```
def main(req: func.HttpRequest, connectionInfo: str) -> func.HttpResponse:
# connectionInfo contains an access key token with a name identifier
# claim set to the authenticated user
return func.HttpResponse(
connectionInfo,
status_code=200,
headers={
'Content-type': 'application/json'
}
)
```


```
@FunctionName("negotiate")
public SignalRConnectionInfo negotiate(
@HttpTrigger(
name = "req",
methods = { HttpMethod.POST },
authLevel = AuthorizationLevel.ANONYMOUS) HttpRequestMessage<Optional<String>> req,
@SignalRConnectionInfoInput(
name = "connectionInfo",
HubName = "hubName1",
userId = "{headers.x-ms-client-principal-id}") SignalRConnectionInfo connectionInfo) {
return connectionInfo;
}
```


### Binding expressions for HTTP trigger

[
It's a common scenario that the values of some attributes of SignalR input binding come from HTTP requests. Therefore, we show how to bind values from HTTP requests to SignalR input binding attributes via ][binding expression](functions-bindings-expressions-patterns#trigger-metadata).

| HTTP metadata type | Binding expression format | Description | Example |
|---|---|---|---|
| HTTP request query | `{query.QUERY_PARAMETER_NAME}` |
Binds the value of corresponding query parameter to an attribute | `{query.userName}` |
| HTTP request header | `{headers.HEADER_NAME}` |
Binds the value of a header to an attribute | `{headers.token}` |

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/storage-considerations -->

# Storage considerations for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a function app instance in Azure, you must provide access to a default Azure Storage account. The following diagram and table detail how Azure Functions uses services in the default storage account:


| Storage service | Functions usage |
|---|---|
|

1.Deployment source for apps that run in a

[Flex Consumption plan](flex-consumption-plan).Used by default for

[task hubs in Durable Functions](durable/durable-functions-task-hubs).Can be used to store function app code for

[Linux Consumption remote build](functions-deployment-technologies#remote-build)or as part of[external package URL deployments](functions-deployment-technologies#external-package-url).[Azure Files](../storage/files/storage-files-introduction)2[Consumption Plan](consumption-plan)and[Premium Plan](functions-premium-plan).Maintain

[extension bundles](extension-bundles).Store deployment logs.

Supports

[Managed dependencies in PowerShell](functions-reference-powershell#managed-dependencies-feature).[Azure Queue storage](../storage/queues/storage-queues-introduction)[task hubs in Durable Functions](durable/durable-functions-task-hubs). Used for failure and retry handling in[specific Azure Functions triggers](functions-bindings-storage-blob-trigger). Used for object tracking by the[Blob storage trigger](functions-bindings-storage-blob-trigger).[Azure Table storage](../storage/tables/table-storage-overview)[task hubs in Durable Functions](durable/durable-functions-task-hubs).Used for tracking

[diagnostic events](functions-diagnostics).- Blob storage is the default store for function keys, but you can
[configure an alternate store](function-keys-how-to#manage-key-storage). - Azure Files is set up by default, but you can
[create an app without Azure Files](#create-an-app-without-azure-files)under certain conditions.

## Important considerations

You must strongly consider the following facts regarding the storage accounts used by your function apps:

When your function app is hosted on the Consumption plan or Premium plan, your function code and configuration files are stored in Azure Files in the linked storage account. When you delete this storage account, the content is deleted and can't be recovered. For more information, see

[Storage account was deleted](functions-recover-storage-account#storage-account-was-deleted).Important data, such as function code,

[access keys](function-keys-how-to), and other important service-related data, persist in the storage account. You must carefully manage access to the storage accounts used by function apps in the following ways:Audit and limit the access of apps and users to the storage account based on a least-privilege model. Permissions to the storage account can come from

[data actions in the assigned role](../role-based-access-control/role-definitions#control-and-data-actions)or through permission to perform the[listKeys operation](/en-us/rest/api/storagerp/storage-accounts/list-keys).Monitor both control plane activity (such as retrieving keys) and data plane operations (such as writing to a blob) in your storage account. Consider maintaining storage logs in a location other than Azure Storage. For more information, see

[Storage logs](#storage-logs).


## Storage account requirements

Storage accounts that you create during the function app creation process in the Azure portal work with the new function app. When you choose to use an existing storage account, the list provided doesn't include certain unsupported storage accounts. The following restrictions apply to storage accounts used by your function app. Make sure an existing storage account meets these requirements:

The account type must support Blob, Queue, and Table storage. Some storage accounts don't support queues and tables. These accounts include blob-only storage accounts and Azure Premium Storage. To learn more about storage account types, see

[Storage account overview](../storage/common/storage-account-overview).You can't use a network-secured storage account when your function app is hosted in the

[Consumption plan](consumption-plan).When you create your function app in the Azure portal, you can only choose an existing storage account in the same region as the function app that you create. This requirement is a performance optimization and not a strict limitation. To learn more, see

[Storage account location](#storage-account-location).When you create your function app on a plan with

[availability zone support](/en-us/azure/reliability/reliability-functions#availability-zone-support)enabled, only[zone-redundant storage accounts](../storage/common/storage-redundancy#zone-redundant-storage)are supported.

When you use deployment automation to create your function app with a network-secured storage account, you must include specific networking configurations in your ARM template or Bicep file. If you don't include these settings and resources, your automated deployment might fail in validation. For ARM template and Bicep guidance, see [Secured deployments](functions-infrastructure-as-code#secured-deployments). For an overview on configuring storage accounts with networking, see [How to use a secured storage account with Azure Functions](configure-networking-how-to).

## Storage account guidance

Every function app requires a storage account to operate. When you delete that account, your function app stops running. To troubleshoot storage-related issues, see [How to troubleshoot storage-related issues](functions-recover-storage-account). The following considerations apply to the storage account used by function apps.

### Storage account location

For best performance, your function app should use a storage account in the same region, which reduces latency. The Azure portal enforces this best practice. If you need to use a storage account in a region different from your function app, you must create your function app outside of the Azure portal.

The storage account must be accessible to the function app. If you need to use a secured storage account, consider [restricting your storage account to a virtual network](functions-networking-options#restrict-your-storage-account-to-a-virtual-network).

### Storage account connection setting

By default, function apps configure the `AzureWebJobsStorage`

connection as a connection string stored in the [AzureWebJobsStorage application setting](functions-app-settings#azurewebjobsstorage). You can also [configure AzureWebJobsStorage to use an identity-based connection](functions-reference#connecting-to-host-storage-with-an-identity) without a secret.

Function apps running in a Consumption plan (Windows only) or an Elastic Premium plan (Windows or Linux) can use Azure Files to store the images required to enable dynamic scaling. For these plans, set the connection string for the storage account in the [WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](functions-app-settings#website_contentazurefileconnectionstring) setting and the name of the file share in the [WEBSITE_CONTENTSHARE](functions-app-settings#website_contentshare) setting. This value is usually the same account used for `AzureWebJobsStorage`

. You can also [create a function app that doesn't use Azure Files](#create-an-app-without-azure-files), but scaling might be limited.

Note

You must update a storage account connection string when you regenerate storage keys. For more information, see [Create an Azure storage account](../storage/common/storage-account-create).

### Shared storage accounts

Multiple function apps can share the same storage account without any problems. For example, in Visual Studio, you can develop multiple apps by using the [Azurite storage emulator](functions-develop-local#local-storage-emulator). In this case, the emulator acts like a single storage account. The same storage account that your function app uses can also store your application data. However, this approach isn't always a good idea in a production environment.

You might need to use separate storage accounts to [avoid host ID collisions](#avoiding-host-id-collisions).

### Lifecycle management policy considerations

Don't apply [lifecycle management policies](../storage/blobs/lifecycle-management-overview) to your Blob Storage account used by your function app. Functions uses Blob storage to persist important information, such as [function access keys](function-keys-how-to). Policies could remove blobs, such as keys, needed by the Functions host. If you must use policies, exclude containers used by Functions, which are prefixed with `azure-webjobs`

or `scm`

.

### Storage logs

Because function code and keys might be persisted in the storage account, logging of activity against the storage account is a good way to monitor for unauthorized access. Azure Monitor resource logs can be used to track events against the storage data plane. See [Monitoring Azure Storage](../storage/blobs/monitor-blob-storage) for details on how to configure and examine these logs.

The [Azure Monitor activity log](/en-us/azure/azure-monitor/essentials/activity-log) shows control plane events, including the [listKeys operation](/en-us/rest/api/storagerp/storage-accounts/list-keys). However, you should also configure resource logs for the storage account to track subsequent use of keys or other identity-based data plane operations. You should have at least the [StorageWrite log category](../storage/blobs/monitor-blob-storage#collection-and-routing) enabled to be able to identify modifications to the data outside of normal Functions operations.

To limit the potential impact of any broadly scoped storage permissions, consider using a nonstorage destination for these logs, such as Log Analytics. For more information, see [Monitoring Azure Blob Storage](../storage/blobs/monitor-blob-storage).

### Optimize storage performance

To maximize performance, use a separate storage account for each function app. This approach is particularly important when you have Durable Functions or Event Hubs triggered functions, which both generate a high volume of storage transactions. When your application logic interacts with Azure Storage, either directly (using the Storage SDK) or through one of the storage bindings, you should use a dedicated storage account. For example, if you have an event hub-triggered function writing some data to blob storage, use two storage accounts: one for the function app and another for the blobs that the function stores.

### Consistent routing through virtual networks

Multiple function apps hosted in the same plan can also use the same storage account for the Azure Files content share, defined by `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

. When you secure this storage account by using a virtual network, all of these apps (including slots) should use the same value for `vnetContentShareEnabled`

(formerly `WEBSITE_CONTENTOVERVNET`

) and the same virtual network integration configuration to ensure that traffic routes consistently through the intended virtual network. A mismatch in this setting between apps that use the same Azure Files storage account might result in traffic routing through public networks. In this configuration, storage account network rules block access.

## Working with blobs

A key scenario for Functions is file processing of files in a blob container, such as for image processing or sentiment analysis. To learn more, see [Process file uploads](functions-scenarios#process-file-uploads).

### Trigger on a blob container

There are several ways to run your function code based on changes to blobs in a storage container, as indicated by this diagram:


Use the following table to determine which function trigger best fits your needs for processing added or updated blobs in a container:

| Strategy | Blob trigger (polling) | Blob trigger (event-driven) | Queue trigger | Event Grid trigger |
|---|---|---|---|---|
| Latency | High (up to 10 min) | Low | Medium | Low |
|

[Blob storage](functions-bindings-storage-blob-trigger)[Blob storage](functions-bindings-storage-blob-trigger)[Queue storage](functions-bindings-storage-queue-trigger)[Event Grid](functions-bindings-event-grid-trigger)[Blob name pattern](functions-bindings-storage-blob-trigger#blob-name-patterns)[Event filters](../storage/blobs/storage-blob-event-overview#filtering-events)[Event filters](../storage/blobs/storage-blob-event-overview#filtering-events)[event subscription](../event-grid/concepts#event-subscriptions)[Flex Consumption plan](flex-consumption-plan)[inbound access restrictions](functions-networking-options#inbound-access-restrictions)3[Blob storage trigger reference](functions-bindings-storage-blob-trigger#example).`Source`

parameter value of `EventGrid`

. For more information, see [Tutorial: Trigger Azure Functions on blob containers using an event subscription](functions-event-grid-blob-trigger).[How to work with Event Grid triggers and bindings in Azure Functions](event-grid-how-tos).- Blob storage input and output bindings support blob-only accounts.
- High scale can be loosely defined as containers that have more than 100,000 blobs in them or storage accounts that have more than 100 blob updates per second.
- You can work around inbound access restrictions by having the event subscription deliver events over an encrypted channel in public IP space using a known user identity. For more information, see
[Deliver events securely using managed identities](../event-grid/deliver-events-using-managed-identity).

## Storage data encryption

Azure Storage encrypts all data in a storage account at rest. For more information, see [Azure Storage encryption for data at rest](../storage/common/storage-service-encryption).

By default, data is encrypted with Microsoft-managed keys. For more control over encryption keys, you can supply customer-managed keys to use for encryption of blob and file data. These keys must be present in Azure Key Vault for Functions to be able to access the storage account. To learn more, see [Encrypt your application data at rest using customer-managed keys](configure-encrypt-at-rest-using-cmk).

### In-region data residency

When all customer data must remain within a single region, the storage account associated with the function app must be one with [in-region redundancy](../storage/common/storage-redundancy). An in-region redundant storage account also must be used with [Azure Durable Functions](durable/durable-functions-azure-storage-provider#storage-account-selection).

Other platform-managed customer data is only stored within the region when hosting in an internally load-balanced App Service Environment (ASE). To learn more, see [ASE zone redundancy](../app-service/environment/zone-redundancy#in-region-data-residency).

## Host ID considerations

Note

The Host ID considerations in this section don't apply when your app runs in a [Flex Consumption plan](flex-consumption-plan). In this hosting plan, the Host ID value is created in a way that avoids these potential issues.

Functions uses a host ID value as a way to uniquely identify a particular function app in stored artifacts. By default, this ID is autogenerated from the name of the function app, truncated to the first 32 characters. This ID is then used when storing per-app correlation and tracking information in the linked storage account. When you have function apps with names longer than 32 characters and when the first 32 characters are identical, this truncation can result in duplicate host ID values. When two function apps with identical host IDs use the same storage account, you get a host ID collision because stored data can't be uniquely linked to the correct function app.

Note

This same kind of host ID collision can occur between a function app in a production slot and the same function app in a staging slot, when both slots use the same storage account.

In version 4.x of the Functions runtime, an error is logged and the host is stopped, resulting in a hard failure. For more information, see [HostID Truncation can cause collisions](https://github.com/Azure/azure-functions-host/issues/2015).

### Avoiding host ID collisions

You can use the following strategies to avoid host ID collisions:

- Use a separate storage account for each function app or slot involved in the collision.
- Rename one of your function apps to a value fewer than 32 characters in length, which changes the computed host ID for the app and removes the collision.
- Set an explicit host ID for one or more of the colliding apps. To learn more, see
[Override the host ID](#override-the-host-id).

Important

Changing the storage account associated with an existing function app or changing the app's host ID can affect the behavior of existing functions. For example, a Blob storage trigger tracks whether it's processed individual blobs by writing receipts under a specific host ID path in storage. When the host ID changes or you point to a new storage account, previously processed blobs could be reprocessed.

### Override the host ID

You can explicitly set a specific host ID for your function app in the application settings by using the `AzureFunctionsWebHost__hostid`

setting. For more information, see [AzureFunctionsWebHost__hostid](functions-app-settings#azurefunctionswebhost__hostid).

When the collision occurs between slots, you must set a specific host ID for each slot, including the production slot. You must also mark these settings as [deployment settings](functions-deployment-slots#create-a-deployment-setting) so they don't get swapped. To learn how to create app settings, see [Work with application settings](functions-how-to-use-azure-function-app-settings#settings).

## Azure Arc-enabled clusters

When your function app is deployed to an Azure Arc-enabled Kubernetes cluster, your function app might not require a storage account. In this case, functions only require a storage account when your function app uses a trigger that requires storage. The following table indicates which triggers might require a storage account and which don't.

| Not required | might require storage |
|---|---|
| •
•
•
•
•
|

[Azure SQL](functions-bindings-azure-sql)•

[Blob storage](functions-bindings-storage-blob)•

[Event Grid](functions-bindings-event-grid)•

[Event Hubs](functions-bindings-event-hubs)•

[IoT Hub](functions-bindings-event-iot)•

[Queue storage](functions-bindings-storage-queue)•

[SendGrid](functions-bindings-sendgrid)•

[SignalR](functions-bindings-signalr-service)•

[Table storage](functions-bindings-storage-table)•

[Timer](functions-bindings-timer)•

[Twilio](functions-bindings-twilio)To create a function app on an Azure Arc-enabled Kubernetes cluster without storage, you must use the Azure CLI command [az functionapp create](/en-us/cli/azure/functionapp#az-functionapp-create). The version of the Azure CLI must include version 0.1.7 or a later version of the [appservice-kube extension](/en-us/cli/azure/appservice/kube). Use the `az --version`

command to verify that the extension is installed and is the correct version.

Creating your function app resources using methods other than the Azure CLI requires an existing storage account. If you plan to use any triggers that require a storage account, you should create the account before you create the function app.

## Create an app without Azure Files

The Azure Files service provides a shared file system that supports high-scale scenarios. When your function app runs in an Elastic Premium plan or on Windows in a Consumption plan, an Azure Files share is created by default in your storage account. This share is used by Functions to enable certain features, like log streaming. It's also used as a shared package deployment location, which guarantees the consistency of your deployed function code across all instances.

By default, function apps hosted in Premium and Consumption plans use [zip deployment](deployment-zip-push), with deployment packages stored in this Azure file share. This section is only relevant to these hosting plans.

Using Azure Files requires the use of a connection string, which is stored in your app settings as [ WEBSITE_CONTENTAZUREFILECONNECTIONSTRING](functions-app-settings#website_contentazurefileconnectionstring). Azure Files doesn't currently support identity-based connections. If your scenario requires you to not store any secrets in app settings, you must remove your app's dependency on Azure Files. You can avoid this dependency by creating your app without the default Azure Files dependency.

Note

You should also consider running your function app in the Flex Consumption plan, which provides greater control over the deployment package, including the ability use managed identity connections. For more information, see [Configure deployment settings](flex-consumption-how-to#configure-deployment-settings).

To run your app without the Azure file share, you must meet the following requirements:

- You must
[deploy your package to a remote Azure Blob storage container](run-functions-from-deployment-package)and then set the URL that provides access to that package as theapp setting. This approach lets you store your app content in Blob storage instead of Azure Files, which does support`WEBSITE_RUN_FROM_PACKAGE`

[managed identities](run-functions-from-deployment-package#fetch-a-package-from-azure-blob-storage-using-a-managed-identity).

You must manually update the deployment package and maintain the deployment package URL, which likely contains a shared access signature (SAS).

You should also note the following considerations:

- The app can't use version 1.x of the Functions runtime.
- Your app can't rely on a shared writeable file system.
- Portal editing isn't supported.
- Log streaming experiences in clients such as the Azure portal default to file system logs. You should instead rely on Application Insights logs.

If the preceding requirements suit your scenario, you can proceed to create a function app without Azure Files. Create an app without the `WEBSITE_CONTENTAZUREFILECONNECTIONSTRING`

and `WEBSITE_CONTENTSHARE`

app settings in one of these ways:

- Bicep/ARM templates: remove the two app settings from the ARM template or Bicep file and then deploy the app using the modified template.
- The Azure portal: unselect
**Add an Azure Files connection**in the**Storage**tab when you create the app in the Azure portal.

Azure Files is used to enable dynamic scale-out for Functions. Scaling could be limited when you run your app without Azure Files in the Elastic Premium plan and Consumption plans running on Windows.

## Mount file shares

*This functionality is current only available when running on Linux.*

You can mount existing Azure Files shares to your Linux function apps. By mounting a share to your Linux function app, you can use existing machine learning models or other data in your functions.

Important

After 30 September 2028, the option to host your function app on Linux in a Consumption plan is retired. To avoid disruptions, migrate your existing Consumption plan apps that run on Linux to the [Flex Consumption plan](flex-consumption-plan) before that date. Apps running on Windows in a Consumption plan aren't affected by this change.
For more information, see the [Linux Consumption plan retirement notice](https://go.microsoft.com/fwlink/?linkid=2335809).

You can use the following command to mount an existing share to your Linux function app.

[az webapp config storage-account add](/en-us/cli/azure/webapp/config/storage-account#az-webapp-config-storage-account-add)

In this command, `share-name`

is the name of the existing Azure Files share. `custom-id`

can be any string that uniquely defines the share when mounted to the function app. Also, `mount-path`

is the path from which the share is accessed in your function app. `mount-path`

must be in the format `/dir-name`

, and it can't start with `/home`

.

For a complete example, see [Create a Python function app and mount an Azure Files share](scripts/functions-cli-mount-files-storage-linux).

Currently, only a `storage-type`

of `AzureFiles`

is supported. You can only mount five shares to a given function app. Mounting a file share can increase the cold start time by at least 200-300 ms, or even more when the storage account is in a different region.

The mounted share is available to your function code at the `mount-path`

specified. For example, when `mount-path`

is `/path/to/mount`

, you can access the target directory by file system APIs, as in the following Python example:

```
import os
...
files_in_share = os.listdir("/path/to/mount")
```


## Related article

Learn more about Azure Functions hosting options.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb-v2-output -->

# Azure Cosmos DB output binding for Azure Functions 2.x and higher

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.

For information on setup and configuration details, see the [overview](functions-bindings-cosmosdb-v2).

Important

This article uses tabs to support multiple versions of the Node.js programming model. The v4 model is generally available and is designed to have a more flexible and intuitive experience for JavaScript and TypeScript developers. For more details about how the v4 model works, refer to the [Azure Functions Node.js developer guide](functions-reference-node). To learn more about the differences between v3 and v4, refer to the [migration guide](functions-node-upgrade-v4).

Azure Functions supports two programming models for Python. The way that you define your bindings depends on your chosen programming model.

The Python v2 programming model lets you define bindings using decorators directly in your Python function code. For more information, see the [Python developer guide](functions-reference-python?pivots=python-mode-decorators#programming-model).

This article supports both programming models.

A C# function can be created by using one of the following C# modes:

[Isolated worker model](dotnet-isolated-process-guide): Compiled C# function that runs in a worker process that's isolated from the runtime. Isolated worker process is required to support C# functions running on LTS and non-LTS versions .NET and the .NET Framework. Extensions for isolated worker process functions use`Microsoft.Azure.Functions.Worker.Extensions.*`

namespaces.[In-process model](functions-dotnet-class-library): Compiled C# function that runs in the same process as the Functions runtime. In a variation of this model, Functions can be run using[C# scripting](functions-reference-csharp), which is supported primarily for C# portal editing. Extensions for in-process functions use`Microsoft.Azure.WebJobs.Extensions.*`

namespaces.

Important

[Support will end for the in-process model on November 10, 2026](https://aka.ms/azure-functions-retirements/in-process-model). We highly recommend that you [migrate your apps to the isolated worker model](/en-us/azure/azure-functions/migrate-dotnet-to-isolated-model) for full support.

## Example

Unless otherwise noted, examples in this article target version 3.x of the [Azure Cosmos DB extension](functions-bindings-cosmosdb-v2). For use with extension version 4.x, you need to replace the string `collection`

in property and attribute names with `container`

and `connection_string_setting`

with `connection`

.

The following code defines a `MyDocument`

type:

```
public class MyDocument
{
public string? Id { get; set; }
public string? Text { get; set; }
public int Number { get; set; }
public bool Boolean { get; set; }
}
```


In the following example, the return type is an [ IReadOnlyList<T>](/en-us/dotnet/api/system.collections.generic.ireadonlylist-1), which is a modified list of documents from trigger binding parameter:

```
using System.Collections.Generic;
using System.Linq;
using Microsoft.Azure.Functions.Worker;
using Microsoft.Extensions.Logging;
namespace SampleApp
{
public class CosmosDBFunction
{
private readonly ILogger<CosmosDBFunction> _logger;
public CosmosDBFunction(ILogger<CosmosDBFunction> logger)
{
_logger = logger;
}
//<docsnippet_exponential_backoff_retry_example>
[Function(nameof(CosmosDBFunction))]
[ExponentialBackoffRetry(5, "00:00:04", "00:15:00")]
[CosmosDBOutput("%CosmosDb%", "%CosmosContainerOut%", Connection = "CosmosDBConnection", CreateIfNotExists = true)]
public object? Run(
[CosmosDBTrigger(
"%CosmosDb%",
"%CosmosContainerIn%",
Connection = "CosmosDBConnection",
LeaseContainerName = "leases",
CreateLeaseContainerIfNotExists = true)] IReadOnlyList<MyDocument> input,
FunctionContext context)
{
if (input != null && input.Any())
{
foreach (var doc in input)
{
_logger.LogInformation("Doc Id: {id}", doc.Id);
}
// Cosmos Output
return input.Select(p => new { id = p.Id });
}
return null;
}
//</docsnippet_exponential_backoff_retry_example>
}
```


[Queue trigger, save message to database via return value](#queue-trigger-save-message-to-database-via-return-value-java)[HTTP trigger, save one document to database via return value](#http-trigger-save-one-document-to-database-via-return-value-java)[HTTP trigger, save one document to database via OutputBinding](#http-trigger-save-one-document-to-database-via-outputbinding-java)[HTTP trigger, save multiple documents to database via OutputBinding](#http-trigger-save-multiple-documents-to-database-via-outputbinding-java)

### Queue trigger, save message to database via return value

The following example shows a Java function that adds a document to a database with data from a message in Queue storage.

```
@FunctionName("getItem")
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "AzureCosmosDBConnection")
public String cosmosDbQueryById(
@QueueTrigger(name = "msg",
queueName = "myqueue-items",
connection = "AzureWebJobsStorage")
String message,
final ExecutionContext context) {
return "{ id: \"" + System.currentTimeMillis() + "\", Description: " + message + " }";
}
```


#### HTTP trigger, save one document to database via return value

The following example shows a Java function whose signature is annotated with `@CosmosDBOutput`

and has return value of type `String`

. The JSON document returned by the function is automatically written to the corresponding Azure Cosmos DB collection.

```
@FunctionName("WriteOneDoc")
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
public String run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
final ExecutionContext context) {
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Generate document
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
context.getLogger().info("Document to be saved: " + jsonDocument);
return jsonDocument;
}
```


### HTTP trigger, save one document to database via OutputBinding

The following example shows a Java function that writes a document to Azure Cosmos DB via an `OutputBinding<T>`

output parameter. In this example, the `outputItem`

parameter needs to be annotated with `@CosmosDBOutput`

, not the function signature. Using `OutputBinding<T>`

lets your function take advantage of the binding to write the document to Azure Cosmos DB while also allowing returning a different value to the function caller, such as a JSON or XML document.

```
@FunctionName("WriteOneDocOutputBinding")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
OutputBinding<String> outputItem,
final ExecutionContext context) {
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Generate document
final String jsonDocument = "{\"id\":\"" + id + "\", " +
"\"description\": \"" + name + "\"}";
context.getLogger().info("Document to be saved: " + jsonDocument);
// Set outputItem's value to the JSON document to be saved
outputItem.setValue(jsonDocument);
// return a different document to the browser or calling client.
return request.createResponseBuilder(HttpStatus.OK)
.body("Document created successfully.")
.build();
}
```


### HTTP trigger, save multiple documents to database via OutputBinding

The following example shows a Java function that writes multiple documents to Azure Cosmos DB via an `OutputBinding<T>`

output parameter. In this example, the `outputItem`

parameter is annotated with `@CosmosDBOutput`

, not the function signature. The output parameter, `outputItem`

has a list of `ToDoItem`

objects as its template parameter type. Using `OutputBinding<T>`

lets your function take advantage of the binding to write the documents to Azure Cosmos DB while also allowing returning a different value to the function caller, such as a JSON or XML document.

```
@FunctionName("WriteMultipleDocsOutputBinding")
public HttpResponseMessage run(
@HttpTrigger(name = "req",
methods = {HttpMethod.GET, HttpMethod.POST},
authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@CosmosDBOutput(name = "database",
databaseName = "ToDoList",
collectionName = "Items",
connectionStringSetting = "Cosmos_DB_Connection_String")
OutputBinding<List<ToDoItem>> outputItem,
final ExecutionContext context) {
// Parse query parameter
String query = request.getQueryParameters().get("desc");
String name = request.getBody().orElse(query);
// Item list
context.getLogger().info("Parameters are: " + request.getQueryParameters());
// Generate documents
List<ToDoItem> items = new ArrayList<>();
for (int i = 0; i < 5; i ++) {
// Generate random ID
final int id = Math.abs(new Random().nextInt());
// Create ToDoItem
ToDoItem item = new ToDoItem(String.valueOf(id), name);
items.add(item);
}
// Set outputItem's value to the list of POJOs to be saved
outputItem.setValue(items);
context.getLogger().info("Document to be saved: " + items);
// return a different document to the browser or calling client.
return request.createResponseBuilder(HttpStatus.OK)
.body("Documents created successfully.")
.build();
}
```


In the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBOutput`

annotation on parameters that is written to Azure Cosmos DB. The annotation parameter type should be `OutputBinding<T>`

, where `T`

is either a native Java type or a POJO.

The following example shows a storage queue triggered [TypeScript function](functions-reference-node?tabs=typescript) for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the TypeScript code:

```
import { app, InvocationContext, output } from '@azure/functions';
interface MyQueueItem {
name: string;
employeeId: string;
address: string;
}
interface MyCosmosItem {
id: string;
name: string;
employeeId: string;
address: string;
}
export async function storageQueueTrigger1(queueItem: MyQueueItem, context: InvocationContext): Promise<MyCosmosItem> {
return {
id: `${queueItem.name}-${queueItem.employeeId}`,
name: queueItem.name,
employeeId: queueItem.employeeId,
address: queueItem.address,
};
}
app.storageQueue('storageQueueTrigger1', {
queueName: 'inputqueue',
connection: 'MyStorageConnectionAppSetting',
return: output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: true,
connectionStringSetting: 'MyAccount_COSMOSDB',
}),
handler: storageQueueTrigger1,
});
```


To output multiple documents, return an array instead of a single object. For example:

```
return [
{
id: 'John Henry-123456',
name: 'John Henry',
employeeId: '123456',
address: 'A town nearby',
},
{
id: 'John Doe-123457',
name: 'John Doe',
employeeId: '123457',
address: 'A town far away',
},
];
```


The following example shows a storage queue triggered [JavaScript function](functions-reference-node) for a queue that receives JSON in the following format:

```
{
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


The function creates Azure Cosmos DB documents in the following format for each record:

```
{
"id": "John Henry-123456",
"name": "John Henry",
"employeeId": "123456",
"address": "A town nearby"
}
```


Here's the JavaScript code:

```
const { app, output } = require('@azure/functions');
const cosmosOutput = output.cosmosDB({
databaseName: 'MyDatabase',
collectionName: 'MyCollection',
createIfNotExists: true,
connectionStringSetting: 'MyAccount_COSMOSDB',
});
app.storageQueue('storageQueueTrigger1', {
queueName: 'inputqueue',
connection: 'MyStorageConnectionAppSetting',
return: cosmosOutput,
handler: (queueItem, context) => {
return {
id: `${queueItem.name}-${queueItem.employeeId}`,
name: queueItem.name,
employeeId: queueItem.employeeId,
address: queueItem.address,
};
},
});
```


To output multiple documents, return an array instead of a single object. For example:

```
return [
{
id: 'John Henry-123456',
name: 'John Henry',
employeeId: '123456',
address: 'A town nearby',
},
{
id: 'John Doe-123457',
name: 'John Doe',
employeeId: '123457',
address: 'A town far away',
},
];
```


The following example shows how to write data to Azure Cosmos DB using an output binding. The binding is declared in the function's configuration file (*functions.json*), and takes data from a queue message and writes out to an Azure Cosmos DB document.

```
{
"name": "EmployeeDocument",
"type": "cosmosDB",
"databaseName": "MyDatabase",
"collectionName": "MyCollection",
"createIfNotExists": true,
"connectionStringSetting": "MyStorageConnectionAppSetting",
"direction": "out"
}
```


In the *run.ps1* file, the object returned from the function is mapped to an `EmployeeDocument`

object, which is persisted in the database.

```
param($QueueItem, $TriggerMetadata)
Push-OutputBinding -Name EmployeeDocument -Value @{
id = $QueueItem.name + '-' + $QueueItem.employeeId
name = $QueueItem.name
employeeId = $QueueItem.employeeId
address = $QueueItem.address
}
```


The following example demonstrates how to write a document to an Azure Cosmos DB database as the output of a function. The example depends on whether you use the [v1 or v2 Python programming model](functions-reference-python).

```
import logging
import azure.functions as func
app = func.FunctionApp()
@app.route()
@app.cosmos_db_output(arg_name="documents",
database_name="DB_NAME",
collection_name="COLLECTION_NAME",
create_if_not_exists=True,
connection_string_setting="CONNECTION_SETTING")
def main(req: func.HttpRequest, documents: func.Out[func.Document]) -> func.HttpResponse:
request_body = req.get_body()
documents.set(func.Document.from_json(request_body))
return 'OK'
```


## Attributes

Both [in-process](functions-dotnet-class-library) and [isolated worker process](dotnet-isolated-process-guide) C# libraries use attributes to define the function. C# script instead uses a function.json configuration file as described in the [C# scripting guide](functions-reference-csharp#azure-cosmos-db-v2-output).

| Attribute property | Description |
|---|---|
Connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**DatabaseName****ContainerName****CreateIfNotExists***false*because new containers are created with reserved throughput, which has cost implications. For more information, see the[pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).**PartitionKey**`CreateIfNotExists`

is true, it defines the partition key path for the created container. May include binding parameters.**ContainerThroughput**`CreateIfNotExists`

is true, it defines the [throughput](/en-us/azure/cosmos-db/set-throughput)of the created container.**PreferredLocations**`East US,South Central US,North Europe`

.## Decorators

*Applies only to the Python v2 programming model.*

For Python v2 functions defined using a decorator, the following properties on the `cosmos_db_output`

:

| Property | Description |
|---|---|
`arg_name` |
The variable name used in function code that represents the list of documents with changes. |
`database_name` |
The name of the Azure Cosmos DB database with the container being monitored. |
`container_name` |
The name of the Azure Cosmos DB container being monitored. |
`create_if_not_exists` |
A Boolean value that indicates whether the database and collection should be created if they do not exist. |
`connection_string_setting` |
The connection string of the Azure Cosmos DB being monitored. |

For Python functions defined by using *function.json*, see the [Configuration](#configuration) section.

## Annotations

From the [Java functions runtime library](/en-us/java/api/overview/azure/functions/runtime), use the `@CosmosDBOutput`

annotation on parameters that write to Azure Cosmos DB. The annotation supports the following properties:

## Configuration

*Applies only to the Python v1 programming model.*

The following table explains the binding configuration properties that you set in the *function.json* file, where properties differ by extension version:

| function.json property | Description |
|---|---|
connection |
The name of an app setting or setting collection that specifies how to connect to the Azure Cosmos DB account being monitored. For more information, see
|

**databaseName****containerName****createIfNotExists***false*because new containers are created with reserved throughput, which has cost implications. For more information, see the[pricing page](https://azure.microsoft.com/pricing/details/cosmos-db/).**partitionKey**`createIfNotExists`

is true, it defines the partition key path for the created container. May include binding parameters.**containerThroughput**`createIfNotExists`

is true, it defines the [throughput](/en-us/azure/cosmos-db/set-throughput)of the created container.**preferredLocations**`East US,South Central US,North Europe`

.See the [Example section](#example) for complete examples.

## Usage

By default, when you write to the output parameter in your function, a document is created in your database. You should specify the document ID of the output document by specifying the `id`

property in the JSON object passed to the output parameter.

Note

When you specify the ID of an existing document, it gets overwritten by the new output document.

The output function parameter must be defined as `func.Out[func.Document]`

. Refer to the [output example](#example) for details.

The parameter type supported by the Cosmos DB output binding depends on the Functions runtime version, the extension package version, and the C# modality used.

When you want the function to write to a single document, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
| JSON serializable types | An object representing the JSON content of a document. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple documents, the Cosmos DB output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is JSON serializable type |
An array containing multiple documents. Each entry represents one document. |

For other output scenarios, create and use a [CosmosClient](/en-us/dotnet/api/microsoft.azure.cosmos.cosmosclient) with other types from [Microsoft.Azure.Cosmos](/en-us/dotnet/api/microsoft.azure.cosmos) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## Connections

The `connectionStringSetting`

/`connection`

and `leaseConnectionStringSetting`

/`leaseConnection`

properties are references to environment configuration which specifies how the app should connect to Azure Cosmos DB. They may specify:

- The name of an application setting containing a
[connection string](#connection-string) - The name of a shared prefix for multiple application settings, together defining an
[identity-based connection](#identity-based-connections). This option is only available for the`connection`

and`leaseConnection`

versions from[version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4).

If the configured value is both an exact match for a single setting and a prefix match for other settings, the exact match is used.

### Connection string

The connection string for your database account should be stored in an application setting with a name matching the value specified by the connection property of the binding configuration.

### Identity-based connections

If you are using [version 4.x or higher of the extension](functions-bindings-cosmosdb-v2?tabs=extensionv4), instead of using a connection string with a secret, you can have the app use an [Microsoft Entra identity](../active-directory/fundamentals/active-directory-whatis). To do this, you would define settings under a common prefix which maps to the connection property in the trigger and binding configuration.

In this mode, the extension requires the following properties:

| Property | Environment variable template | Description | Example value |
|---|---|---|---|
| Account Endpoint | `<CONNECTION_NAME_PREFIX>__accountEndpoint` |
The Azure Cosmos DB account endpoint URI. | https://<database_account_name>.documents.azure.com:443/ |

Additional properties may be set to customize the connection. See [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified with the `credential`

and `clientID`

properties. Note that configuring a user-assigned identity with a resource ID is **not** supported. When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Grant permission to the identity

Whatever identity is being used must have permissions to perform the intended actions. For most Azure services, this means you need to [assign a role in Azure RBAC](../role-based-access-control/role-assignments-steps), using either built-in or custom roles which provide those permissions.

Important

Some permissions might be exposed by the target service that are not necessary for all contexts. Where possible, adhere to the **principle of least privilege**, granting the identity only required privileges. For example, if the app only needs to be able to read from a data source, use a role that only has permission to read. It would be inappropriate to assign a role that also allows writing to that service, as this would be excessive permission for a read operation. Similarly, you would want to ensure the role assignment is scoped only over the resources that need to be read.

Cosmos DB does not use Azure RBAC for data operations. Instead, it uses a [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) which is built on similar concepts. You will need to create a role assignment that provides access to your database account at runtime. Azure RBAC Management roles like [Owner](../role-based-access-control/built-in-roles#owner) are not sufficient. The following table shows built-in roles that are recommended when using the Azure Cosmos DB extension in normal operation. Your application may require additional permissions based on the code you write.

| Binding type | Example built-in roles1 |
|---|---|
Trigger2 |
|

[Cosmos DB Built-in Data Reader](/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions)[Cosmos DB Built-in Data Contributor](/en-us/azure/cosmos-db/how-to-setup-rbac#built-in-role-definitions)1 These roles cannot be used in an Azure RBAC role assignment. See the [Cosmos DB built-in RBAC system](/en-us/azure/cosmos-db/how-to-setup-rbac) documentation for details on how to assign these roles.

2 When using identity, Cosmos DB treats container creation as a management operation. It is not available as a data-plane operation for the trigger. You will need to ensure that you create the containers needed by the trigger (including the lease container) before setting up your function.

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Azure Cosmos DB |
|

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/add-bindings-existing-function -->

# Connect functions to Azure services using bindings

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a function, language-specific trigger code is added in your project from a set of trigger templates. If you want to connect your function to other services by using input or output bindings, you have to add specific binding definitions in your function. To learn more about bindings, see [Azure Functions triggers and bindings concepts](functions-triggers-bindings).

## Local development

When you develop functions locally, you need to update the function code to add bindings. For languages that use function.json, [Visual Studio Code](#visual-studio-code) provides tooling to add bindings to a function.

### Manually add bindings based on examples

When adding a binding to an existing function, you need to add binding-specific attributes to the function definition in code.

When adding a binding to an existing function, you need to add binding-specific annotations to the function definition in code.

When adding a binding to an existing function, you need to update the function code and add a definition to the function.json configuration file.

When adding a binding to an existing function, you need update the function definition, depending on your model:

The following example shows the function definition after adding a [Queue Storage output binding](functions-bindings-storage-queue-output) to an [HTTP triggered function](functions-bindings-http-webhook-trigger):

Because an HTTP triggered function also returns an HTTP response, the function returns a `MultiResponse`

object, which represents both the HTTP and queue output.

```
[Function("HttpExample")]
public static MultiResponse Run([HttpTrigger(AuthorizationLevel.Function, "get", "post")] HttpRequest req,
FunctionContext executionContext)
{
```


This example is the definition of the `MultiResponse`

object that includes the output binding:

```
public class MultiResponse
{
[QueueOutput("outqueue",Connection = "AzureWebJobsStorage")]
public string[] Messages { get; set; }
public IActionResult HttpResponse { get; set; }
}
```


When applying that example to your own project, you might need to change `HttpRequest`

to `HttpRequestData`

and `IActionResult`

to `HttpResponseData`

, depending on if you are using [ASP.NET Core integration](dotnet-isolated-process-guide#aspnet-core-integration) or not.

Messages are sent to the queue when the function completes. The way you define the output binding depends on your process model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=csharp#manually-add-bindings-based-on-examples).

```
@FunctionName("HttpExample")
public HttpResponseMessage run(
@HttpTrigger(name = "req", methods = {HttpMethod.GET, HttpMethod.POST}, authLevel = AuthorizationLevel.ANONYMOUS)
HttpRequestMessage<Optional<String>> request,
@QueueOutput(name = "msg", queueName = "outqueue",
connection = "AzureWebJobsStorage") OutputBinding<String> msg,
final ExecutionContext context) {
```


For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=java#manually-add-bindings-based-on-examples).

```
const { app, output } = require('@azure/functions');
const sendToQueue = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
extraOutputs: [sendToQueue],
handler: async (request, context) => {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
},
});
```


The way you define the output binding depends on the version of your Node.js model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=javascript#manually-add-bindings-based-on-examples).

```
$outputMsg = $name
Push-OutputBinding -name msg -Value $outputMsg
```


For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=powershell#manually-add-bindings-based-on-examples).

```
@app.route(route="HttpExample")
@app.queue_output(arg_name="msg", queue_name="outqueue", connection="AzureWebJobsStorage")
def HttpExample(req: func.HttpRequest, msg: func.Out [func.QueueMessage]) -> func.HttpResponse:
logging.info('Python HTTP trigger function processed a request.')
```


The way you define the output binding depends on the version of your Python model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=python#manually-add-bindings-based-on-examples).

```
import {
app,
output,
HttpRequest,
HttpResponseInit,
InvocationContext,
StorageQueueOutput,
} from '@azure/functions';
const sendToQueue: StorageQueueOutput = output.storageQueue({
queueName: 'outqueue',
connection: 'AzureWebJobsStorage',
});
export async function HttpExample(
request: HttpRequest,
context: InvocationContext,
): Promise<HttpResponseInit> {
try {
context.log(`Http function processed request for url "${request.url}"`);
const name = request.query.get('name') || (await request.text());
context.log(`Name: ${name}`);
if (name) {
const msg = `Name passed to the function ${name}`;
context.extraOutputs.set(sendToQueue, [msg]);
return { body: msg };
} else {
context.log('Missing required data');
return { status: 404, body: 'Missing required data' };
}
} catch (error) {
context.log(`Error: ${error}`);
return { status: 500, body: 'Internal Server Error' };
}
}
app.http('HttpExample', {
methods: ['GET', 'POST'],
authLevel: 'anonymous',
handler: HttpExample,
});
```


The way you define the output binding depends on the version of your Node.js model. For more information, including links to example binding code that you can refer to, see [Add bindings to a function](add-bindings-existing-function?tabs=typescript#manually-add-bindings-based-on-examples).

Use the following table to find examples of specific binding types that you can use to guide you in updating an existing function. First, choose the language tab that corresponds to your project.

Binding code for C# depends on the [specific process model](dotnet-isolated-process-guide#benefits-of-the-isolated-worker-model).

| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/storage/Microsoft.Azure.WebJobs.Extensions.Storage.Blobs)[Trigger](functions-bindings-cosmosdb-v2-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-cosmosdb-v2-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-cosmosdb-v2-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-csharp#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-csharp#examples)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-csharp)[Trigger](functions-bindings-azure-sql-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-azure-sql-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-azure-sql-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](/en-us/samples/azure-samples/azure-sql-binding-func-dotnet-todo/todo-backend-dotnet-azure-sql-bindings-azure-functions/)[Trigger](functions-bindings-event-grid-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-grid-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Trigger](functions-bindings-event-hubs-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-hubs-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-event-iot-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-event-iot-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-http-webhook-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure-Samples/functions-quickstart-dotnet-azd)[Trigger](functions-bindings-storage-queue-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-storage-queue-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/storage/Microsoft.Azure.WebJobs.Extensions.Storage.Queues/samples/functionapp)[Trigger](functions-bindings-rabbitmq-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-rabbitmq-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-sendgrid?tabs=isolated-process&pivots=programming-language-csharp#example)[Trigger](functions-bindings-service-bus-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-service-bus-output?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-sdk-for-net/tree/main/sdk/servicebus/Microsoft.Azure.WebJobs.Extensions.ServiceBus)[Trigger](functions-bindings-signalr-service-trigger?tabs=isolated-process&pivots=programming-language-csharp#example)[Input](functions-bindings-signalr-service-input?tabs=isolated-process&pivots=programming-language-csharp#example)[Output](functions-bindings-signalr-service-output?tabs=isolated-process&pivots=programming-language-csharp)[Input](functions-bindings-storage-table-input?tabs=isolated-process&pivots=programming-language-csharp)[Output](functions-bindings-storage-table-output?tabs=isolated-process&pivots=programming-language-csharp)[Trigger](functions-bindings-timer?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)[Output](functions-bindings-twilio?tabs=isolated-process&pivots=programming-language-csharp#example)[Link](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/dev/sample/ExtensionsSample/Samples)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-java#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-java#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/java-functions-eventhub-cosmosdb)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-java#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-java#examples)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-java)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-java#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-java#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-java#example)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-java#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-java#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-java#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-java#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-java#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-java#example)[Output](functions-bindings-sendgrid?pivots=programming-language-java#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-java#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-java#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-java#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-java)[Input](functions-bindings-storage-table-input?pivots=programming-language-java)[Output](functions-bindings-storage-table-output?pivots=programming-language-java)[Trigger](functions-bindings-timer?pivots=programming-language-java#example)[Link](https://github.com/Azure-Samples/azure-functions-samples-java/tree/master/triggers-bindings/src/main/java/com/functions)[Output](functions-bindings-twilio?pivots=programming-language-java#example)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-nodejs)[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-javascript#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-add-output-binding-cosmosdb-cli-v4-programming-model)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-javascript#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-javascript#examples)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-javascript#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-node)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-javascript#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-typescript)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/functions-docs-javascript/tree/master/functions-add-output-binding-storage-queue-cli-v4-programming-model)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-javascript#example)[Output](functions-bindings-sendgrid?pivots=programming-language-javascript#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-javascript#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-javascript#example)[Link](https://github.com/Azure-Samples/azure-functions-servicebus-sdk-bindings-nodejs/tree/main/serviceBusSampleWithComplete)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-javascript#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-javascript#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-javascript)[Input](functions-bindings-storage-table-input?pivots=programming-language-javascript)[Output](functions-bindings-storage-table-output?pivots=programming-language-javascript)[Trigger](functions-bindings-timer?pivots=programming-language-javascript#example)[Output](functions-bindings-twilio?pivots=programming-language-javascript#example)| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Trigger](functions-bindings-cosmosdb-v2-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-cosmosdb-v2-input?pivots=programming-language-powershell#example)[Output](functions-bindings-cosmosdb-v2-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-azure-sql-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-azure-sql-input?pivots=programming-language-powershell#example)[Output](functions-bindings-azure-sql-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-grid-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-grid-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-hubs-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-hubs-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-event-iot-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-event-iot-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-http-webhook-trigger?pivots=programming-language-powershell#example)[Link](https://github.com/Azure-Samples/functions-quickstart-powershell-azd)[Trigger](functions-bindings-storage-queue-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-storage-queue-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-rabbitmq-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-rabbitmq-output?pivots=programming-language-powershell#example)[Output](functions-bindings-sendgrid?pivots=programming-language-powershell#example)[Trigger](functions-bindings-service-bus-trigger?pivots=programming-language-powershell#example)[Output](functions-bindings-service-bus-output?pivots=programming-language-powershell#example)[Trigger](functions-bindings-signalr-service-trigger?pivots=programming-language-powershell#example)[Input](functions-bindings-signalr-service-input?pivots=programming-language-powershell#example)[Output](functions-bindings-signalr-service-output?pivots=programming-language-powershell)[Input](functions-bindings-storage-table-input?pivots=programming-language-powershell)[Output](functions-bindings-storage-table-output?pivots=programming-language-powershell)[Trigger](functions-bindings-timer?pivots=programming-language-powershell#example)[Output](functions-bindings-twilio?pivots=programming-language-powershell#example)Binding code for Python depends on the Python model version.

| Service | Examples | Samples |
|---|---|---|
| Blob Storage |
|

[Link](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python)[Trigger](functions-bindings-cosmosdb-v2-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-cosmosdb-v2-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-cosmosdb-v2-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-cosmosdb)[Input](functions-bindings-azure-data-explorer-input?pivots=programming-language-python#examples)[Output](functions-bindings-azure-data-explorer-output?pivots=programming-language-python#examples)[Trigger](functions-bindings-azure-sql-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-azure-sql-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-azure-sql-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure/Webjobs.Extensions.Kusto/tree/main/samples/samples-python)[Trigger](functions-bindings-event-grid-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-grid-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-hubs-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-hubs-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-event-iot-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-event-iot-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-http-webhook-trigger?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-http-azd)[Trigger](functions-bindings-storage-queue-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-storage-queue-output?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-rabbitmq-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-rabbitmq-output?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-sendgrid?tabs=python-v2&pivots=programming-language-python#example)[Trigger](functions-bindings-service-bus-trigger?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-service-bus-output?tabs=python-v2&pivots=programming-language-python#example)[Link](https://github.com/Azure-Samples/functions-quickstart-python-azd-service-bus)[Trigger](functions-bindings-signalr-service-trigger?tabs=python-v2&pivots=programming-language-python#example)[Input](functions-bindings-signalr-service-input?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-signalr-service-output?tabs=python-v2&pivots=programming-language-python)[Input](functions-bindings-storage-table-input?tabs=python-v2&pivots=programming-language-python)[Output](functions-bindings-storage-table-output?tabs=python-v2&pivots=programming-language-python)[Trigger](functions-bindings-timer?tabs=python-v2&pivots=programming-language-python#example)[Output](functions-bindings-twilio?tabs=python-v2&pivots=programming-language-python#example)### Visual Studio Code

When you use Visual Studio Code to develop your function and your function uses a function.json file, the Azure Functions extension can automatically add a binding to an existing function.json file. To learn more, see [Add input and output bindings](functions-develop-vs-code#add-input-and-output-bindings).

## Azure portal

When you develop your functions in the [Azure portal](https://portal.azure.com), you add input and output bindings in the **Integrate** tab for a given function. The new bindings are added to either the function.json file or to the method attributes, depending on your language. The following articles show examples of how to add bindings to an existing function in the portal:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-create-your-first-function-visual-studio -->

# Quickstart: Create your first C# function in Azure using Visual Studio

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions lets you use Visual Studio to create local C# function projects and then easily publish this project to run in a scalable serverless environment in Azure. If you prefer to develop your C# apps locally using Visual Studio Code, you should instead consider the [Visual Studio Code-based version](how-to-create-function-vs-code?pivot=programming-language-csharp) of this article.

By default, this article shows you how to create C# functions that run on .NET 8 in an [isolated worker process](dotnet-isolated-process-guide). Function apps that run in an isolated worker process are supported on all versions of .NET that are supported by Functions. For more information, see [Supported versions](dotnet-isolated-process-guide#supported-versions).

In this article, you learn how to:

- Use Visual Studio to create a C# class library project.
- Create a function that responds to HTTP requests.
- Run your code locally to verify function behavior.
- Deploy your code project to Azure Functions.

Completing this quickstart incurs a small cost of a few USD cents or less in your Azure account.

This video shows you how to create a C# function in Azure.

The steps in the video are also described in the following sections.

## Prerequisites

[Visual Studio 2022](https://visualstudio.microsoft.com/vs/). Make sure to select the**Azure development**workload during installation.[Azure subscription](../guides/developer/azure-developer-guide#understanding-accounts-subscriptions-and-billing). If you don't already have an account,[create a free one](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

## Create a function app project

The Azure Functions project template in Visual Studio creates a C# class library project that you can publish to a function app in Azure. You can use a function app to group functions as a logical unit for easier management, deployment, scaling, and sharing of resources.

From the Visual Studio menu, select

**File**>**New**>**Project**.In

**Create a new project**, enter*functions*in the search box, choose the**Azure Functions**template, and then select**Next**.In

**Configure your new project**, enter a**Project name**for your project, and then select**Next**. The function app name must be valid as a C# namespace, so don't use underscores, hyphens, or any other nonalphanumeric characters.For the remaining

**Additional information**settings,Setting Value Description **Functions worker****.NET 8.0 Isolated (Long Term Support)**Your functions run on .NET 8 in an isolated worker process. **Function****HTTP trigger**This value creates a function triggered by an HTTP request. **Use Azurite for runtime storage account (AzureWebJobsStorage)**Enable Because a function app in Azure requires a storage account, one is assigned or created when you publish your project to Azure. An HTTP trigger doesn't use an Azure Storage account connection string; all other trigger types require a valid Azure Storage account connection string. When you select this option, the [Azurite emulator](../storage/common/storage-use-azurite?tabs=visual-studio)is used.**Authorization level****Anonymous**The created function can be triggered by any client without providing a key. This authorization setting makes it easy to test your new function. For more information, see [Authorization level](functions-bindings-http-webhook-trigger#http-auth).Make sure you set the

**Authorization level**to**Anonymous**. If you choose the default level of**Function**, you're required to present the[function key](function-keys-how-to)in requests to access your function endpoint in Azure.Select

**Create**to create the function project and HTTP trigger function.

Visual Studio creates a project and class that contains boilerplate code for the HTTP trigger function type. The boilerplate code sends an HTTP response that includes a value from the request body or query string. The `HttpTrigger`

attribute specifies that the function is triggered by an HTTP request.

## Rename the function

The `Function`

method attribute sets the name of the function, which by default is generated as `Function1`

. Since the tooling doesn't let you override the default function name when you create your project, take a minute to create a better name for the function class, file, and metadata.

In

**File Explorer**, right-click the Function1.cs file and rename it to`HttpExample.cs`

.In the code, rename the Function1 class to

`HttpExample`

.In the method named

`Run`

, rename the`Function`

method attribute to`HttpExample`

.

Your function definition should now look like the following code:

```
[Function("HttpExample")]
public IActionResult Run([HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")] HttpRequest req)
{
_logger. LogInformation("C# HTTP trigger function processed a request.");
return new OkObjectResult("Hello, functions");
}
```


Now that you've renamed the function, you can test it on your local computer.

## Run the function locally

Visual Studio integrates with Azure Functions Core Tools so that you can test your functions locally using the full Azure Functions runtime.

To run your function, press

`F5`in Visual Studio. You might need to enable a firewall exception so that the tools can handle HTTP requests. Authorization levels are never enforced when you run a function locally.Copy the URL of your function from the Azure Functions runtime output.

Paste the URL for the HTTP request into your browser's address bar and run the request. The following image shows the response in the browser to the local GET request returned by the function:

To stop debugging, press

`Shift`+`F5`in Visual Studio.

After you've verified that the function runs correctly on your local computer, it's time to publish the project to Azure.

## Publish the project to Azure

Visual Studio can publish your local project to Azure. Before you can publish your project, you must have a function app in your Azure subscription. If you don't already have a function app in Azure, Visual Studio can help you create one before you publish your project. In this article, you create a function app that runs on Linux in a Flex Consumption plan, which is the recommended plan for event-driven and secure serverless functions.

In

**Solution Explorer**, right-click the project and then select**Publish**.On the

**Publish**page, make the following selections:- On
**Target**, select**Azure**, and then select**Next**. - On
**Specific target**, select**Azure Function App**, and then select**Next**. - On
**Functions instance**, select**Create new**.

- On
Create a new instance by using the values specified in the following table:

Setting Value Description **Name**A globally unique name The name must uniquely identify your new function app. Accept the suggested name or enter a new name. The following characters are valid: `a-z`

,`0-9`

, and`-`

.**Subscription name**The name of your subscription The function app is created in an Azure subscription. Accept the default subscription or select a different one from the list. [Resource group](../azure-resource-manager/management/overview)The name of your resource group The function app is created in a resource group. Select **New**to create a new resource group. You can also select an existing resource group from the list.[Plan Type](functions-scale)**Flex Consumption**When you publish your project to a function app that runs in a [Flex Consumption plan](flex-consumption-plan), you might pay only for executions of your functions app. Other hosting plans can incur higher costs.**IMPORTANT:**

When creating a Flex Consumption plan, you must first select**App service plan**and then reselect**Flex Consumption**to clear an issue with the dialog.**Operating system****Linux**The Flex Consumption plan currently requires Linux. **Location**The location of the app service Select a location in an [Azure region supported by the Flex Consumption plan](flex-consumption-how-to#view-currently-supported-regions). When an unsupported region is selected, the**Create**button is grayed-out.**Instance memory size****2048**The [memory size of the virtual machine instances](flex-consumption-plan#instance-sizes)in which the app runs is unique to the Flex Consumption plan.[Azure Storage](storage-considerations)A general-purpose storage account The Functions runtime requires a Storage account. Select **New**to configure a general-purpose storage account. You can also use an existing account that meets the[storage account requirements](storage-considerations#storage-account-requirements).[Application Insights](functions-monitoring)An Application Insights instance You should turn on Application Insights integration for your function app. Select **New**to create a new instance, either in a new or in an existing Log Analytics workspace. You can also use an existing instance.Select

**Create**to create a function app and its related resources in Azure. The status of resource creation is shown in the lower-left corner of the window.Select

**Finish**. The**Publish profile creation progress**window appears. When the profile is created, select**Close**.On the publish profile page, select

**Publish**to deploy the package that contains your project files to your new function app in Azure.When deployment is complete, the root URL of the function app in Azure is shown on the publish profile page.

On the publish profile page, go to the

**Hosting**section. Select the ellipsis (**...**), and then select**Open in Azure portal**. The new function app Azure resource opens in the Azure portal.

## Verify your function in Azure

In the Azure portal, you should be in the

**Overview**page for your new functions app.Under

**Functions**, select your new function named**HttpExample**, then in the function page select**Get function URL**and then the**Copy to clipboard icon**.In the address bar in your browser, paste the URL you copied and run the request.

The URL that calls your HTTP trigger function is in the following format:

`https://<APP_NAME>.azurewebsites.net/api/HttpExample?name=Functions`

Go to this URL and you see a response in the browser to the remote GET request returned by the function, which looks like the following example:


## Clean up resources

*Resources* in Azure refer to function apps, functions, storage accounts, and so forth. They're grouped into *resource groups*, and you can delete everything in a group by deleting the group.

You created Azure resources to complete this quickstart. You could be billed for these resources, depending on your [account status](https://azure.microsoft.com/account/) and [service pricing](https://azure.microsoft.com/pricing/). Other quickstarts in this collection build upon this quickstart. If you plan to work with subsequent quickstarts, tutorials, or with any of the services you've created in this quickstart, don't clean up the resources.

Use the following steps to delete the function app and its related resources to avoid incurring any further costs.

In the Visual Studio Publish dialogue, in the Hosting section, select

**Open in Azure portal**.In the function app page, select the

**Overview**tab and then select the link under**Resource group**.In the

**Resource group**page, review the list of included resources, and verify that they're the ones you want to delete.Select

**Delete resource group**, and follow the instructions.Deletion may take a couple of minutes. When it's done, a notification appears for a few seconds. You can also select the bell icon at the top of the page to view the notification.


## Next steps

In this quickstart, you used Visual Studio to create and publish a C# function app in Azure with a simple HTTP trigger function.

To learn more about working with C# functions that run in an isolated worker process, see the [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide). Check out [.NET supported versions](functions-dotnet-class-library#supported-versions) to see other versions of supported .NET versions in an isolated worker process.

Advance to the next article to learn how to add an Azure Storage queue binding to your function:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-storage-blob -->

# Azure Blob storage bindings for Azure Functions overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Functions integrates with [Azure Storage](../storage/) via [triggers and bindings](functions-triggers-bindings). Integrating with Blob storage allows you to build functions that react to changes in blob data as well as read and write values.

| Action | Type |
|---|---|
| Run a function as blob storage data changes |
|

[Input binding](functions-bindings-storage-blob-input)[Output binding](functions-bindings-storage-blob-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

The functionality of the extension varies depending on the extension version:

This version introduces the ability to [connect using an identity instead of a secret](functions-reference#configure-an-identity-based-connection). For a tutorial on configuring your function apps with managed identities, see the [creating a function app with identity-based connections tutorial](functions-identity-based-connections-tutorial).

This version allows you to bind to types from [Azure.Storage.Blobs](/en-us/dotnet/api/azure.storage.blobs). Learn more about how these new types are different from `WindowsAzure.Storage`

and `Microsoft.Azure.Storage`

and how to migrate to them from the [Azure.Storage.Blobs Migration Guide](https://github.com/Azure/azure-sdk-for-net/blob/main/sdk/storage/Azure.Storage.Blobs/AzureStorageNetMigrationV12.md).

This version supports configuration of triggers and bindings through [.NET Aspire integration](dotnet-aspire-integration#connection-configuration-with-aspire).

Add the extension to your project by installing the [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs), version 5.x or later.

Using the .NET CLI:

```
dotnet add package Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs
```


Note

Azure Blobs, Azure Queues, and Azure Tables now use separate extensions and are referenced individually. For example, to use the triggers and bindings for all three services in your .NET isolated-process app, you should add the following packages to your project:

[Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs)[Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Queues)[Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables)

Previously, the extensions shipped together as [Microsoft.Azure.Functions.Worker.Extensions.Storage, version 4.x](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/4.0.4). This same package also has a [5.x version](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage/5.0.0), which references the split packages for blobs and queues only. When upgrading your package references from older versions, you may therefore need to additionally reference the new [Microsoft.Azure.Functions.Worker.Extensions.Tables](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Tables) NuGet package. Also, when referencing these newer split packages, make sure you are not referencing an older version of the combined storage package, as this will result in conflicts from two definitions of the same bindings.

If you're writing your application using F#, you must also configure this extension as part of the app's [startup configuration](dotnet-isolated-process-guide#start-up-and-configuration). In the call to `ConfigureFunctionsWorkerDefaults()`

or `ConfigureFunctionsWebApplication()`

, add a delegate that takes an `IFunctionsWorkerApplication`

parameter. Then within the body of that delegate, call `ConfigureBlobStorageExtension()`

on the object:

```
let hostBuilder = new HostBuilder()
hostBuilder.ConfigureFunctionsWorkerDefaults(fun (context: HostBuilderContext) (appBuilder: IFunctionsWorkerApplicationBuilder) ->
appBuilder.ConfigureBlobStorageExtension() |> ignore
) |> ignore
```


## Install bundle

To be able to use this binding extension in your app, make sure that the *host.json* file in the root of your project contains this `extensionBundle`

reference:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


In this example, the `version`

value of `[4.0.0, 5.0.0)`

instructs the Functions host to use a bundle version that is at least `4.0.0`

but less than `5.0.0`

, which includes all potential versions of 4.x. This notation effectively maintains your app on the latest available minor version of the v4.x extension bundle.

When possible, you should use the latest extension bundle major version and allow the runtime to automatically maintain the latest minor version. You can view the contents of the latest bundle on the [extension bundles release page](https://github.com/Azure/azure-functions-extension-bundles/releases/latest). For more information, see [Azure Functions extension bundles](extension-bundles).

## Binding types

The binding types supported for .NET depend on both the extension version and C# execution mode, which can be one of the following:

An isolated worker process class library compiled C# function runs in a process isolated from the runtime.

Choose a version to see binding type details for the mode and version.

The isolated worker process supports parameter types according to the tables below.

**Blob trigger**

The blob trigger can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)11 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Blob input binding**

When you want the function to process a single blob, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | When a blob contains JSON data, Functions tries to deserialize the JSON data into a plain-old CLR object (POCO) type. |
1 |

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient)1,[BlockBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blockblobclient)1,[PageBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.pageblobclient)1,[AppendBlobClient](/en-us/dotnet/api/azure.storage.blobs.specialized.appendblobclient)1,[BlobBaseClient](/en-us/dotnet/api/azure.storage.blobs.specialized.blobbaseclient)1When you want the function to process multiple blobs from a container, the blob input binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` or `List<T>` where `T` is one of the single blob input binding types |
An array or list of multiple blobs. Each entry represents one blob from the container. You can also bind to any interfaces implemented by these types, such as `IEnumerable<T>` . |
1 |

1 To use these types, you need to reference [Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs 6.0.0 or later](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.Storage.Blobs/6.0.0) and the [common dependencies for SDK type bindings](dotnet-isolated-process-guide#sdk-types).

**Blob output binding**

When you want the function to write to a single blob, the blob output binding can bind to the following types:

| Type | Description |
|---|---|
`string` |
The blob content as a string. Use when the blob content is simple text. |
`byte[]` |
The bytes of the blob content. |
| JSON serializable types | An object representing the content of a JSON blob. Functions attempts to serialize a plain-old CLR object (POCO) type into JSON data. |

When you want the function to write to multiple blobs, the blob output binding can bind to the following types:

| Type | Description |
|---|---|
`T[]` where `T` is one of the single blob output binding types |
An array containing content for multiple blobs. Each entry represents the content of one blob. |

For other output scenarios, create and use a [BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient) or [BlobContainerClient](/en-us/dotnet/api/azure.storage.blobs.blobcontainerclient) with other types from [Azure.Storage.Blobs](/en-us/dotnet/api/azure.storage.blobs) directly. See [Register Azure clients](dotnet-isolated-process-guide#register-azure-clients) for an example of using dependency injection to create a client type from the Azure SDK.

## SDK Binding Types

SDK Types for Azure Storage Blob are generally available! Follow the [Python SDK Bindings for Blob Sample](https://github.com/Azure-Samples/azure-functions-blob-sdk-bindings-python) to get started with SDK Types for Blob in Python.

Important

Using SDK type bindings requires the [Python v2 programming model](functions-reference-python?pivots=python-mode-decorators#sdk-type-bindings).

| Binding | Parameter types | Samples |
|---|---|---|
| Blob trigger |
|

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_blobclient/function_app.py)`BlobClient`

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py)`ContainerClient`

`StorageStreamDownloader`

[BlobClient](/en-us/dotnet/api/azure.storage.blobs.blobclient),[ContainerClient](/en-us/python/api/azure-storage-blob/azure.storage.blob.containerclient),[StorageStreamDownloader](/en-us/python/api/azure-storage-blob/azure.storage.blob.storagestreamdownloader)[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_blobclient/function_app.py)`BlobClient`

[,](https://github.com/Azure/azure-functions-python-extensions/blob/dev/azurefunctions-extensions-bindings-blob/samples/blob_samples_containerclient/function_app.py)`ContainerClient`

`StorageStreamDownloader`

## host.json settings

This section describes the function app configuration settings available for functions that use this binding. These settings only apply when using extension version 5.0.0 and higher. The example host.json file below contains only the version 2.x+ settings for this binding. For more information about function app configuration settings in versions 2.x and later versions, see [host.json reference for Azure Functions](functions-host-json).

Note

This section doesn't apply to extension versions before 5.0.0. For those earlier versions, there aren't any function app-wide configuration settings for blobs.

```
{
"version": "2.0",
"extensions": {
"blobs": {
"maxDegreeOfParallelism": 4,
"poisonBlobThreshold": 1
}
}
}
```


| Property | Default | Description |
|---|---|---|
| maxDegreeOfParallelism | 8 * (the number of available cores) | The integer number of concurrent invocations allowed for all blob-triggered functions in a given function app. The minimum allowed value is 1. |
| poisonBlobThreshold | 5 | The integer number of times to try processing a message before moving it to the poison queue. The minimum allowed value is 1. |

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/container-concepts -->

# Linux container support in Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you plan and develop your individual functions to run in Azure Functions, you're typically focused on the code itself. Azure Functions makes it easy to deploy just your code project to a function app in Azure. When you deploy your project to a Linux function app, your code runs in a container that is created for you automatically and seamlessly integrates with Functions management tools.

Functions also supports containerized function app deployments. In a containerized deployment, you create your own function app instance in a local Docker container from a supported based image. You can then deploy this *containerized* function app to a hosting environment in Azure. Creating your own function app container lets you customize or otherwise control the immediate runtime environment of your function code.

Important

When you create your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific. See the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container. For more information, see [Maintaining custom containers](container-concepts#maintaining-custom-containers).

## Container hosting options

There are several options for hosting your containerized function apps in Azure:

| Hosting option | Benefits |
|---|---|
|
Azure Functions provides integrated support for developing, deploying, and managing containerized function apps on
Recommended hosting option for containerized function apps n Azure. |

**Azure Arc-enabled Kubernetes clusters (preview)***Hosting Azure Functions containers on Azure Arc-enabled Kubernetes clusters is currently in preview.*For more information, see[Working with containers and Azure Functions](functions-how-to-custom-container?pivots=azure-arc).[Azure Functions](functions-how-to-custom-container?pivots=azure-functions#azure-portal-create-using-containers)[Elastic Premium](functions-premium-plan)or an[App Service (Dedicated)](dedicated-plan)plan. Use Container Apps hosting for rich container support from Container Apps. Premium plan hosting provides you with the benefits of dynamic scaling. You might want to use Dedicated plan hosting to take advantage of existing unused App Service plan resources.[Kubernetes](functions-kubernetes-keda)[KEDA](https://keda.sh)(Kubernetes-based Event Driven Autoscaling) pairs seamlessly with the Azure Functions runtime and tooling to provide event driven scale in Kubernetes.**Important:**Kubernetes hosting of your containerized function apps, either by using KEDA or by direct deployment, is an open-source effort that you can use free of cost.*Best-effort*support for this hosting scenario is provided only by contributors and by the community. You're responsible for maintaining your own function app containers in a cluster, even when deploying them to Azure Kubernetes Service (AKS).## Feature support comparison

The degree to which various features and behaviors of Azure Functions are supported when running your function app in a container depends on the container hosting option you choose.

| Feature/behavior |
|
|---|

[Container Apps (direct)](../container-apps/overview)

[Premium plan](functions-premium-plan)

[Dedicated plan](dedicated-plan)

[Kubernetes](functions-kubernetes-keda)

[Event-driven scaling](event-driven-scaling)5[scale rules](../container-apps/scale-app#scale-rules))1123[Scale-to-zero instances](event-driven-scaling#scale-in-behaviors)6678[Core Tools deployment](functions-run-local#deploy-containers)`func kubernetes`

[Revisions](../container-apps/revisions)[Yes](../container-apps/revisions)[Deployment slots](functions-deployment-slots)[Streaming logs](streaming-logs)[Yes](../container-apps/log-streaming)[Yes](../container-apps/log-streaming)[Console access](../container-apps/container-console)[Yes](../container-apps/container-console)[Kudu](functions-how-to-custom-container#enable-ssh-connections))[Kudu](functions-how-to-custom-container#enable-ssh-connections))[using](https://kubernetes.io/docs/reference/kubectl/))`kubectl`

[Scale rules](../container-apps/scale-app#scale-rules)[Always-ready/pre-warmed instances](functions-premium-plan#eliminate-cold-starts)[App Service authentication](../app-service/overview-authentication-authorization)[Yes](../container-apps/authentication)[Custom domain names](../app-service/app-service-web-tutorial-custom-domain)[Yes](../container-apps/custom-domains-certificates)[Private key certificates](../app-service/overview-tls)[Yes](../container-apps/custom-domains-certificates)[Yes](../container-apps/networking)[Yes](/en-us/azure/reliability/reliability-azure-container-apps)[Yes](../container-apps/troubleshooting#use-the-diagnose-and-solve-problems-tool)[Yes](../container-apps/troubleshooting#use-the-diagnose-and-solve-problems-tool)[Yes](functions-diagnostics)[Yes](functions-diagnostics)[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[workload profiles](../container-apps/workload-profiles-overview))[Configurable memory/CPU count](../container-apps/workload-profiles-overview)[Yes](../container-apps/billing#consumption-plan)[Yes](../container-apps/billing#consumption-plan)[Container Apps billing](../container-apps/billing)[Container Apps billing](../container-apps/billing)[Premium plan billing](functions-premium-plan#billing)[Dedicated plan billing](dedicated-plan#billing)[AKS pricing](/en-us/azure/aks/free-standard-pricing-tiers)- On Container Apps, the default is 10 instances, but you can set the
[maximum number of replicas](../container-apps/scale-app#scale-definition), which has an overall maximum of 1000. This setting is honored as long as there's enough cores quota available. When you create your function app from the Azure portal, you're limited to 300 instances. - In some regions, Linux apps on a Premium plan can scale to 100 instances. For more information, see the
[Premium plan article](functions-premium-plan#region-max-scale-out). - For specific limits for the various App Service plan options, see the
[App Service plan limits](../azure-resource-manager/management/azure-subscription-service-limits#azure-app-service-limits). - Requires
[KEDA](functions-kubernetes-keda); supported by most triggers. To learn which triggers support event-driven scaling, see[Considerations for Container Apps hosting](functions-container-apps-hosting#considerations-for-container-apps-hosting). - When the
[minimum number of replicas](../container-apps/scale-app#scale-definition)is set to zero, the default timeout depends on the specific triggers used in the app. - There's no maximum execution timeout duration enforced. However, the grace period given to a function execution is 60 minutes
[during scale in](event-driven-scaling#scale-in-behaviors), and a grace period of 10 minutes is given during platform updates. - Requires the App Service plan be set to
[Always On](dedicated-plan#always-on). A grace period of 10 minutes is given during platform updates.

## Maintaining custom containers

When creating your own containers, you're required to keep the base image of your container updated to the latest supported base image. Supported base images for Azure Functions are language-specific and are found in the [Azure Functions base image repos](https://mcr.microsoft.com/catalog?search=functions).

The Functions team is committed to publishing monthly updates for these base images. Regular updates include the latest minor version updates and security fixes for both the Functions runtime and languages. You should regularly update your container from the latest base image and redeploy the updated version of your container.

Choose your base image based on the language stack you're using in your function app. The following table provides examples for each stack. In general, the tag should start with `4-`

to indicate the V4 Functions runtime. When new minor versions are released, this tag will be updated to point to the new version. As you periodically rebuild your custom image, you will pull the new versions through that same tag, allowing your app to have the same updates. You shouldn't use tags that specify minor runtime versions, as these will not receive updates, and your app will potentially remain on an unpatched version, no matter how often you rebuild your custom image.

| Language Stack | Example recommended base image tags |
|---|---|
| .NET (isolated worker model) | `mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0` or`mcr.microsoft.com/azure-functions/dotnet-isolated:4-dotnet-isolated8.0-appservice` (These examples target .NET 8. Select the appropriate image for the .NET version you need.) |
| .NET (legacy in-process model) | `mcr.microsoft.com/azure-functions/dotnet:4-dotnet8.0` or`mcr.microsoft.com/azure-functions/dotnet:4-dotnet8.0-appservice` (Support will end for the in-process model on November 10, 2026. You should
|
| Java | `mcr.microsoft.com/azure-functions/java:4-java21` or`mcr.microsoft.com/azure-functions/java:4-java21-appservice` (These examples target Java 21. Select the appropriate image for the Java version you need.) |
| Node.js (JavaScript or TypeScript) | `mcr.microsoft.com/azure-functions/node:4-node22` or`mcr.microsoft.com/azure-functions/node:4-node22-appservice` (These examples target Node.js 22. Select the appropriate image for the Node.js version you need.) |
| PowerShell | `mcr.microsoft.com/azure-functions/powershell:4-powershell7.4` or`mcr.microsoft.com/azure-functions/powershell:4-powershell7.4-appservice` (These examples target PowerShell 7.4. Select the appropriate image for the PowerShell version you need.) |
| Python | `mcr.microsoft.com/azure-functions/python:4-python3.12` or`mcr.microsoft.com/azure-functions/python:4-python3.12-appservice` (These examples target Python 3.12. Select the appropriate image for the Python version you need.) |
| Custom handlers / other | `mcr.microsoft.com/azure-functions/base:4` or`mcr.microsoft.com/azure-functions/base:4-appservice` |

Base images ending in `-appservice`

enable SSH and remote debugging from the platform. Unless you need these capabilities, you can use the base images without the `-appservice`

suffix.

Important

It isn't sufficient to just have one of the above tags in your Dockerfile. You need to regularly pull the latest image from that tag so that your custom image can be rebuilt to include the latest updates. If you don't pull the latest image and rebuild, your app will continue to run on the old base image.

When you create or deploy your own containerized app using a custom image, you're responsible for making sure that your custom image staying up-to-date with our released base images. In addition to new features and improvements, these base image updates can also include security updates that are critical for your app. To ensure your app is protected, make sure you're staying up to date. You should regularly pull the latest version of the base image, rebuild your custom container image, and redeploy your app to use it.

In some cases, we're required to make platform-level changes that could mean that an app in a custom container using an old base image might stop working properly. For such major changes, we roll out updated images well in advance so that apps that take regular updates aren't negatively impacted. To avoid potential problems with your apps running in custom containers, make sure you don't fall too far behind the latest minor version released. During a support case, should we determine that your app is experiencing problems because it's on an older or unsupported version, we do request that you update your container to the latest base image version before continuing with support.

## Getting started

Use these links to get started working with Azure Functions in Linux containers:

| I want to... | See article: |
|---|---|
| Create my first containerized functions |
|

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-web-pubsub -->

# Web PubSub bindings for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This set of articles explains how to authenticate, send real-time messages to clients connected to [Azure Web PubSub](https://azure.microsoft.com/products/web-pubsub/) by using Azure Web PubSub bindings in Azure Functions.

| Action | Type |
|---|---|
| Handle client events from Web PubSub |
|

[Input binding](functions-bindings-web-pubsub-input)[Output binding](functions-bindings-web-pubsub-output)## Install extension

The extension NuGet package you install depends on the C# mode you're using in your function app:

Functions execute in an isolated C# worker process. To learn more, see [Guide for running C# Azure Functions in an isolated worker process](dotnet-isolated-process-guide).

Add the extension to your project by installing this [NuGet package](https://www.nuget.org/packages/Microsoft.Azure.Functions.Worker.Extensions.WebPubSub/).

## Install bundle

To be able to use this binding extension in your app, make sure that the *host.json* file in the root of your project contains this `extensionBundle`

reference:

```
{
"version": "2.0",
"extensionBundle": {
"id": "Microsoft.Azure.Functions.ExtensionBundle",
"version": "[4.0.0, 5.0.0)"
}
}
```


In this example, the `version`

value of `[4.0.0, 5.0.0)`

instructs the Functions host to use a bundle version that is at least `4.0.0`

but less than `5.0.0`

, which includes all potential versions of 4.x. This notation effectively maintains your app on the latest available minor version of the v4.x extension bundle.

When possible, you should use the latest extension bundle major version and allow the runtime to automatically maintain the latest minor version. You can view the contents of the latest bundle on the [extension bundles release page](https://github.com/Azure/azure-functions-extension-bundles/releases/latest). For more information, see [Azure Functions extension bundles](extension-bundles).

Note

The Web PubSub extensions for Java is not supported yet.

## Key concepts

(1)-(2) `WebPubSubConnection`

input binding with HttpTrigger to generate client connection.

(3)-(4) `WebPubSubTrigger`

trigger binding or `WebPubSubContext`

input binding with HttpTrigger to handle service request.

(5)-(6) `WebPubSub`

output binding to request service do something.

## Connection

You can use [connection string](#connection-string) or [Microsoft Entra identity](#identity-based-connections) to connect to Azure Web PubSub service.

### Connection String

By default, an application setting named `WebPubSubConnectionString`

is used to store your Web PubSub connection string. When you choose to use a different setting name for your connection, you must explicitly set that as the key name in your binding definitions. During local development, you must also add this setting to the `Values`

collection in the [ local.settings.json file](functions-develop-local#local-settings-file).

Important

A connection string includes the authorization information required for your application to access Azure Web PubSub service. The access key inside the connection string is similar to a root password for your service. For optimal security, your function app should use [managed identities](#identity-based-connections) when connecting to the Web PubSub service instead of using a connection string.

For details on how to configure and use Web PubSub and Azure Functions together, refer to [Tutorial: Create a serverless notification app with Azure Functions and Azure Web PubSub service](../azure-web-pubsub/tutorial-serverless-notification).

### Identity-based connections

If you're using Azure Web PubSub Functions Extensions v1.10.0 or higher, instead of using a connection string with an access key, you can configure your function app to authenticate to Azure Web PubSub using a Microsoft Entra identity.

This approach removes the need to manage secrets and is recommended for production workloads.

#### Prerequisites

Make sure the Microsoft Entra identity used by your function app has been granted an appropriate Azure RBAC role on the target Web PubSub resource:

#### Configuration

Identity-based connections in Azure Functions use a set of settings that share a common prefix. By default, Azure Web PubSub Functions extensions look for settings with the prefix `WebPubSubConnectionString`

. You can customize this prefix by setting the `connection`

property in your trigger or binding.

For Azure Web PubSub, the service-specific setting you must provide is the service endpoint URI:

| Property | Environment variable template | Description | Required |
|---|---|---|---|
| Service URI | `WebPubSubConnectionString__serviceUri` |
The URI of your Web PubSub service endpoint. | Yes |

When hosted in the Azure Functions service, identity-based connections use a [managed identity](../app-service/overview-managed-identity?toc=/azure/azure-functions/toc.json). The system-assigned identity is used by default, although a user-assigned identity can be specified. For more information on how to customize the identity, [Common properties for identity-based connections](functions-reference#common-properties-for-identity-based-connections).

When run in other contexts, such as local development, your developer identity is used instead, although this can be customized. See [Local development with identity-based connections](functions-reference#local-development-with-identity-based-connections).

#### Example configuration

The following example shows how to configure identity-based with default settings:

```
{
"WebPubSubConnectionString__serviceUri": "https://your-webpubsub.webpubsub.azure.com"
}
```


Note

When using `local.settings.json`

file at local, [Azure App Configuration](../azure-app-configuration/quickstart-azure-functions-csharp), or [Key Vault](/en-us/azure/key-vault/general/overview) to provide settings for identity-based connections, replace `__`

with `:`

in the setting name to ensure names are resolved correctly.

For example, `WebPubSubConnectionString:serviceUri`

.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-dapr-input-secret -->

# Dapr Secret input binding for Azure Functions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Dapr secret input binding allows you to read secrets data as input during function execution.

For information on setup and configuration details of the Dapr extension, see the [Dapr extension overview](functions-bindings-dapr).

## Example

A C# function can be created using one of the following C# modes:

| Execution model | Description |
|---|---|
Isolated worker model |
Your function code runs in a separate .NET worker process. Use with
|

**In-process model**[Long Term Support (LTS) versions of .NET](functions-dotnet-class-library#supported-versions). To learn more, see[Develop C# class library functions using Azure Functions](functions-dotnet-class-library).```
[FunctionName("RetrieveSecret")]
public static void Run(
[DaprServiceInvocationTrigger] object args,
[DaprSecret("kubernetes", "my-secret", Metadata = "metadata.namespace=default")] IDictionary<string, string> secret,
ILogger log)
{
log.LogInformation("C# function processed a RetrieveSecret request from the Dapr Runtime.");
}
```


The following example creates a `"RetrieveSecret"`

function using the `DaprSecretInput`

binding with the [ DaprServiceInvocationTrigger](functions-bindings-dapr-trigger-svc-invoke):

```
@FunctionName("RetrieveSecret")
public void run(
@DaprServiceInvocationTrigger(
methodName = "RetrieveSecret") Object args,
@DaprSecretInput(
secretStoreName = "kubernetes",
key = "my-secret",
metadata = "metadata.namespace=default")
Map<String, String> secret,
final ExecutionContext context)
```


In the following example, the Dapr secret input binding is paired with a Dapr invoke trigger, which is registered by the `app`

object:

```
const { app, trigger } = require('@azure/functions');
app.generic('RetrieveSecret', {
trigger: trigger.generic({
type: 'daprServiceInvocationTrigger',
name: "payload"
}),
extraInputs: [daprSecretInput],
handler: async (request, context) => {
context.log("Node function processed a RetrieveSecret request from the Dapr Runtime.");
const daprSecretInputValue = context.extraInputs.get(daprSecretInput);
// print the fetched secret value
for (var key in daprSecretInputValue) {
context.log(`Stored secret: Key=${key}, Value=${daprSecretInputValue[key]}`);
}
}
});
```


The following examples show Dapr triggers in a *function.json* file and PowerShell code that uses those bindings.

Here's the *function.json* file for `daprServiceInvocationTrigger`

:

```
{
"bindings":
{
"type": "daprSecret",
"direction": "in",
"name": "secret",
"key": "my-secret",
"secretStoreName": "localsecretstore",
"metadata": "metadata.namespace=default"
}
}
```


For more information about *function.json* file properties, see the [Configuration](#configuration) section.

In code:

```
using namespace System
using namespace Microsoft.Azure.WebJobs
using namespace Microsoft.Extensions.Logging
using namespace Microsoft.Azure.WebJobs.Extensions.Dapr
using namespace Newtonsoft.Json.Linq
param (
$payload, $secret
)
# PowerShell function processed a CreateNewOrder request from the Dapr Runtime.
Write-Host "PowerShell function processed a RetrieveSecretLocal request from the Dapr Runtime."
# Convert the object to a JSON-formatted string with ConvertTo-Json
$jsonString = $secret | ConvertTo-Json
Write-Host "$jsonString"
```


The following example shows a Dapr Secret input binding, which uses the [v2 Python programming model](functions-reference-python). To use the `daprSecret`

binding alongside the `daprServiceInvocationTrigger`

in your Python function app code:

```
import logging
import json
import azure.functions as func
app = func.FunctionApp()
@app.function_name(name="RetrieveSecret")
@app.dapr_service_invocation_trigger(arg_name="payload", method_name="RetrieveSecret")
@app.dapr_secret_input(arg_name="secret", secret_store_name="localsecretstore", key="my-secret", metadata="metadata.namespace=default")
def main(payload, secret: str) :
# Function should be invoked with this command: dapr invoke --app-id functionapp --method RetrieveSecret --data '{}'
logging.info('Python function processed a RetrieveSecret request from the Dapr Runtime.')
secret_dict = json.loads(secret)
for key in secret_dict:
logging.info("Stored secret: Key = " + key +
', Value = ' + secret_dict[key])
```


## Attributes

In the [in-process model](functions-dotnet-class-library), use the `DaprSecret`

to define a Dapr secret input binding, which supports these parameters:

| Parameter | Description |
|---|---|
SecretStoreName |
The name of the secret store to get the secret. |
Key |
The key identifying the name of the secret to get. |
Metadata |
Optional. An array of metadata properties in the form `"key1=value1&key2=value2"` . |

## Annotations

The `DaprSecretInput`

annotation allows you to have your function access a secret.

| Element | Description |
|---|---|
secretStoreName |
The name of the Dapr secret store. |
key |
The secret key value. |
metadata |
Optional. The metadata values. |

## Configuration

The following table explains the binding configuration properties that you set in the code.

| Property | Description |
|---|---|
key |
The secret key value. |
secretStoreName |
Name of the secret store as defined in the local-secret-store.yaml component file. |
metadata |
The metadata namespace. |

The following table explains the binding configuration properties that you set in the function.json file.

| function.json property | Description |
|---|---|
key |
The secret key value. |
secretStoreName |
Name of the secret store as defined in the local-secret-store.yaml component file. |
metadata |
The metadata namespace. |

See the [Example section](#example) for complete examples.

## Usage

To use the Dapr secret input binding, start by setting up a Dapr secret store component. You can learn more about which component to use and how to set it up in the official Dapr documentation.

To use the `daprSecret`

in **Python v2**, set up your project with the correct dependencies.

In your

`requirements.text`

file, add the following line:`azure-functions==1.18.0b3`

In the terminal, install the Python library.

`pip install -r .\requirements.txt`

Modify your

`local.setting.json`

file with the following configuration:`"PYTHON_ISOLATE_WORKER_DEPENDENCIES":1`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/azure-functions/functions-bindings-cosmosdb -->

# Azure Cosmos DB bindings for Azure Functions 1.x

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

[Support will end for version 1.x of the Azure Functions runtime on September 14, 2026](https://aka.ms/azure-functions-retirements/hostv1). We highly recommend that you [migrate your apps to version 4.x](migrate-version-1-version-4) for full support.

This article explains how to work with [Azure Cosmos DB](/en-us/azure/cosmos-db/serverless-computing-database) bindings in Azure Functions. Azure Functions supports trigger, input, and output bindings for Azure Cosmos DB.

Keep these important considerations in mind when using the Azure Cosmos DB binding for the Functions v1.x runtime:

This article is for Azure Functions 1.x. We recommend that you run your functions on the most recent version of the Functions runtime. For information about how to use these bindings in the latest Functions runtime, see

[Azure Cosmos DB bindings for Azure Functions 2.x](functions-bindings-cosmosdb-v2).This binding was originally named DocumentDB. In Azure Functions version 1.x, only the trigger was renamed Azure Cosmos DB; the input binding, output binding, and NuGet package retain the DocumentDB name.

Azure Cosmos DB bindings are only supported for use with the SQL API. For all other Azure Cosmos DB APIs, you should access the database from your function by using the static client for your API, including

[Azure Cosmos DB for MongoDB](/en-us/azure/cosmos-db/mongodb-introduction),[Azure Cosmos DB for Apache Cassandra](/en-us/azure/cosmos-db/cassandra-introduction),[Azure Cosmos DB for Apache Gremlin](/en-us/azure/cosmos-db/graph-introduction), and[Azure Cosmos DB for Table](/en-us/azure/cosmos-db/table-introduction).The Azure Cosmos DB bindings for the Functions v1.x runtime don't support Microsoft Entra authentication and managed identities. To improve security, you should upgrade to run on the latest version of the Functions runtime.


## Packages - Functions 1.x

The Azure Cosmos DB bindings for Functions version 1.x are provided in the [Microsoft.Azure.WebJobs.Extensions.DocumentDB](https://www.nuget.org/packages/Microsoft.Azure.WebJobs.Extensions.DocumentDB) NuGet package, version 1.x. Source code for the bindings is in the [azure-webjobs-sdk-extensions](https://github.com/Azure/azure-webjobs-sdk-extensions/tree/v2.x/src/WebJobs.Extensions.DocumentDB) GitHub repository.

The following table lists how to add support for output binding in each development environment.

| Development environment | To add support in Functions 1.x |
|---|---|
| Local development: C# class library |
|

## Trigger

The Azure Cosmos DB Trigger uses the [Azure Cosmos DB Change Feed](/en-us/azure/cosmos-db/change-feed) to listen for inserts and updates across partitions. The change feed publishes inserts and updates, not deletions.

## Trigger - example

The following example shows an [in-process C# function](functions-dotnet-class-library) that is invoked when there are inserts or updates in the specified database and collection.

```
using Microsoft.Azure.Documents;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
namespace CosmosDBSamplesV1
{
public static class CosmosTrigger
{
[FunctionName("CosmosTrigger")]
public static void Run([CosmosDBTrigger(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
LeaseCollectionName = "leases",
CreateLeaseCollectionIfNotExists = true)]IReadOnlyList<Document> documents,
TraceWriter log)
{
if (documents != null && documents.Count > 0)
{
log.Info($"Documents modified: {documents.Count}");
log.Info($"First document Id: {documents[0].Id}");
}
}
}
}
```


## Trigger - attributes

For [in-process C# class libraries](functions-dotnet-class-library), use the [CosmosDBTrigger](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/master/src/WebJobs.Extensions.CosmosDB/Trigger/CosmosDBTriggerAttribute.cs) attribute.

The attribute's constructor takes the database name and collection name. For information about those settings and other properties that you can configure, see [Trigger - configuration](#trigger---configuration). Here's a `CosmosDBTrigger`

attribute example in a method signature:

```
[FunctionName("DocumentUpdates")]
public static void Run(
[CosmosDBTrigger("database", "collection", ConnectionStringSetting = "myCosmosDB")]
IReadOnlyList<Document> documents,
TraceWriter log)
{
...
}
```


For a complete example, see [Trigger - C# example](#trigger).

## Trigger - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `CosmosDBTrigger`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `cosmosDBTrigger` . |
direction |
n/a | Must be set to `in` . This parameter is set automatically when you create the trigger in the Azure portal. |
name |
n/a | The variable name used in function code that represents the list of documents with changes. |
connectionStringSetting |
ConnectionStringSetting |
The name of an app setting that contains the connection string used to connect to the Azure Cosmos DB account being monitored. |
databaseName |
DatabaseName |
The name of the Azure Cosmos DB database with the collection being monitored. |
collectionName |
CollectionName |
The name of the collection being monitored. |
leaseConnectionStringSetting |
LeaseConnectionStringSetting |
(Optional) The name of an app setting that contains the connection string to the service which holds the lease collection. When not set, the `connectionStringSetting` value is used. This parameter is automatically set when the binding is created in the portal. The connection string for the leases collection must have write permissions. |
leaseDatabaseName |
LeaseDatabaseName |
(Optional) The name of the database that holds the collection used to store leases. When not set, the value of the `databaseName` setting is used. This parameter is automatically set when the binding is created in the portal. |
leaseCollectionName |
LeaseCollectionName |
(Optional) The name of the collection used to store leases. When not set, the value `leases` is used. |
createLeaseCollectionIfNotExists |
CreateLeaseCollectionIfNotExists |
(Optional) When set to `true` , the leases collection is automatically created when it doesn't already exist. The default value is `false` . |
leasesCollectionThroughput |
LeasesCollectionThroughput |
(Optional) Defines the amount of Request Units to assign when the leases collection is created. This setting is only used When `createLeaseCollectionIfNotExists` is set to `true` . This parameter is automatically set when the binding is created using the portal. |
leaseCollectionPrefix |
LeaseCollectionPrefix |
(Optional) When set, it adds a prefix to the leases created in the Lease collection for this Function, effectively allowing two separate Azure Functions to share the same Lease collection by using different prefixes. |
feedPollDelay |
FeedPollDelay |
(Optional) When set, it defines, in milliseconds, the delay in between polling a partition for new changes on the feed, after all current changes are drained. Default is 5000 (5 seconds). |
leaseAcquireInterval |
LeaseAcquireInterval |
(Optional) When set, it defines, in milliseconds, the interval to kick off a task to compute if partitions are distributed evenly among known host instances. Default is 13000 (13 seconds). |
leaseExpirationInterval |
LeaseExpirationInterval |
(Optional) When set, it defines, in milliseconds, the interval for which the lease is taken on a lease representing a partition. If the lease is not renewed within this interval, it will cause it to expire and ownership of the partition will move to another instance. Default is 60000 (60 seconds). |
leaseRenewInterval |
LeaseRenewInterval |
(Optional) When set, it defines, in milliseconds, the renew interval for all leases for partitions currently held by an instance. Default is 17000 (17 seconds). |
checkpointFrequency |
CheckpointFrequency |
(Optional) When set, it defines, in milliseconds, the interval between lease checkpoints. Default is always after each Function call. |
maxItemsPerInvocation |
MaxItemsPerInvocation |
(Optional) When set, it customizes the maximum amount of items received per Function call. |
startFromBeginning |
StartFromBeginning |
(Optional) When set, it tells the Trigger to start reading changes from the beginning of the history of the collection instead of the current time. This only works the first time the Trigger starts, as in subsequent runs, the checkpoints are already stored. Setting this to `true` when there are leases already created has no effect. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Trigger - usage

The trigger requires a second collection that it uses to store *leases* over the partitions. Both the collection being monitored and the collection that contains the leases must be available for the trigger to work.

Important

If multiple functions are configured to use an Azure Cosmos DB trigger for the same collection, each of the functions should use a dedicated lease collection or specify a different `LeaseCollectionPrefix`

for each function. Otherwise, only one of the functions will be triggered. For information about the prefix, see the [Configuration section](#trigger---configuration).

The trigger doesn't indicate whether a document was updated or inserted, it just provides the document itself. If you need to handle updates and inserts differently, you could do that by implementing timestamp fields for insertion or update.

## Input

The Azure Cosmos DB input binding uses the SQL API to retrieve one or more Azure Cosmos DB documents and passes them to the input parameter of the function. The document ID or query parameters can be determined based on the trigger that invokes the function.

## Input - example

This section contains the following examples:

[Queue trigger, look up ID from JSON](#queue-trigger-look-up-id-from-json-c)[HTTP trigger, look up ID from query string](#http-trigger-look-up-id-from-query-string-c)[HTTP trigger, look up ID from route data](#http-trigger-look-up-id-from-route-data-c)[HTTP trigger, look up ID from route data, using SqlQuery](#http-trigger-look-up-id-from-route-data-using-sqlquery-c)[HTTP trigger, get multiple docs, using SqlQuery](#http-trigger-get-multiple-docs-using-sqlquery-c)[HTTP trigger, get multiple docs, using DocumentClient](#http-trigger-get-multiple-docs-using-documentclient-c)

The examples refer to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV1
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


### Queue trigger, look up ID from JSON

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by a queue message that contains a JSON object. The queue trigger parses the JSON into an object named `ToDoItemLookup`

, which contains the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
namespace CosmosDBSamplesV1
{
public class ToDoItemLookup
{
public string ToDoItemId { get; set; }
}
}
```


```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromJSON
{
[FunctionName("DocByIdFromJSON")]
public static void Run(
[QueueTrigger("todoqueueforlookup")] ToDoItemLookup toDoItemLookup,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
Id = "{ToDoItemId}")]ToDoItem toDoItem,
TraceWriter log)
{
log.Info($"C# Queue trigger function processed Id={toDoItemLookup?.ToDoItemId}");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
}
}
}
```


### HTTP trigger, look up ID from query string

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by an HTTP request that uses a query string to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromQueryString
{
[FunctionName("DocByIdFromQueryString")]
public static HttpResponseMessage Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
Id = "{Query.id}")] ToDoItem toDoItem,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, look up ID from route data

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromRouteData
{
[FunctionName("DocByIdFromRouteData")]
public static HttpResponseMessage Run(
[HttpTrigger(
AuthorizationLevel.Anonymous, "get", "post",
Route = "todoitems/{id}")]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
Id = "{id}")] ToDoItem toDoItem,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
if (toDoItem == null)
{
log.Info($"ToDo item not found");
}
else
{
log.Info($"Found ToDo item, Description={toDoItem.Description}");
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, look up ID from route data, using SqlQuery

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a single document. The function is triggered by an HTTP request that uses route data to specify the ID to look up. That ID is used to retrieve a `ToDoItem`

document from the specified database and collection.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocByIdFromRouteDataUsingSqlQuery
{
[FunctionName("DocByIdFromRouteDataUsingSqlQuery")]
public static HttpResponseMessage Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post",
Route = "todoitems2/{id}")]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
SqlQuery = "select * from ToDoItems r where r.id = {id}")] IEnumerable<ToDoItem> toDoItems,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
foreach (ToDoItem toDoItem in toDoItems)
{
log.Info(toDoItem.Description);
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, get multiple docs, using SqlQuery

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a list of documents. The function is triggered by an HTTP request. The query is specified in the `SqlQuery`

attribute property.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System.Collections.Generic;
using System.Net;
using System.Net.Http;
namespace CosmosDBSamplesV1
{
public static class DocsBySqlQuery
{
[FunctionName("DocsBySqlQuery")]
public static HttpResponseMessage Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]
HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection",
SqlQuery = "SELECT top 2 * FROM c order by c._ts desc")]
IEnumerable<ToDoItem> toDoItems,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
foreach (ToDoItem toDoItem in toDoItems)
{
log.Info(toDoItem.Description);
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


### HTTP trigger, get multiple docs, using DocumentClient (C#)

The following example shows a [C# function](functions-dotnet-class-library) that retrieves a list of documents. The function is triggered by an HTTP request. The code uses a `DocumentClient`

instance provided by the Azure Cosmos DB binding to read a list of documents. The `DocumentClient`

instance could also be used for write operations.

```
using Microsoft.Azure.Documents.Client;
using Microsoft.Azure.Documents.Linq;
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Extensions.Http;
using Microsoft.Azure.WebJobs.Host;
using System;
using System.Linq;
using System.Net;
using System.Net.Http;
using System.Threading.Tasks;
namespace CosmosDBSamplesV1
{
public static class DocsByUsingDocumentClient
{
[FunctionName("DocsByUsingDocumentClient")]
public static async Task<HttpResponseMessage> Run(
[HttpTrigger(AuthorizationLevel.Anonymous, "get", "post", Route = null)]HttpRequestMessage req,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection")] DocumentClient client,
TraceWriter log)
{
log.Info("C# HTTP trigger function processed a request.");
Uri collectionUri = UriFactory.CreateDocumentCollectionUri("ToDoItems", "Items");
string searchterm = req.GetQueryNameValuePairs()
.FirstOrDefault(q => string.Compare(q.Key, "searchterm", true) == 0)
.Value;
if (searchterm == null)
{
return req.CreateResponse(HttpStatusCode.NotFound);
}
log.Info($"Searching for word: {searchterm} using Uri: {collectionUri.ToString()}");
IDocumentQuery<ToDoItem> query = client.CreateDocumentQuery<ToDoItem>(collectionUri)
.Where(p => p.Description.Contains(searchterm))
.AsDocumentQuery();
while (query.HasMoreResults)
{
foreach (ToDoItem result in await query.ExecuteNextAsync())
{
log.Info(result.Description);
}
}
return req.CreateResponse(HttpStatusCode.OK);
}
}
}
```


## Input - attributes

In [in-process C# class libraries](functions-dotnet-class-library), use the [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) attribute.

The attribute's constructor takes the database name and collection name. For information about those settings and other properties that you can configure, see [the following configuration section](#input---configuration).

## Input - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `DocumentDB`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `documentdb` . |
direction |
n/a | Must be set to `in` . |
name |
n/a | Name of the binding parameter that represents the document in the function. |
databaseName |
DatabaseName |
The database containing the document. |
collectionName |
CollectionName |
The name of the collection that contains the document. |
id |
Id |
The ID of the document to retrieve. This property supports
id and sqlQuery properties. If you don't set either one, the entire collection is retrieved. |

**sqlQuery****SqlQuery**`SELECT * FROM c where c.departmentId = {departmentId}`

. Don't set both the **id**and**sqlQuery**properties. If you don't set either one, the entire collection is retrieved.**connection****ConnectionStringSetting****partitionKey****PartitionKey**When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Input - usage

When the function exits successfully, any changes made to the input document via named input parameters are automatically persisted.

## Output

The Azure Cosmos DB output binding lets you write a new document to an Azure Cosmos DB database using the SQL API.

## Output - example

This section contains the following examples:

- Queue trigger, write one doc
- Queue trigger, write docs using
`IAsyncCollector`


The examples refer to a simple `ToDoItem`

type:

```
namespace CosmosDBSamplesV1
{
public class ToDoItem
{
public string Id { get; set; }
public string Description { get; set; }
}
}
```


### Queue trigger, write one doc

The following example shows a [C# function](functions-dotnet-class-library) that adds a document to a database, using data provided in message from Queue storage.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System;
namespace CosmosDBSamplesV1
{
public static class WriteOneDoc
{
[FunctionName("WriteOneDoc")]
public static void Run(
[QueueTrigger("todoqueueforwrite")] string queueMessage,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection")]out dynamic document,
TraceWriter log)
{
document = new { Description = queueMessage, id = Guid.NewGuid() };
log.Info($"C# Queue trigger function inserted one row");
log.Info($"Description={queueMessage}");
}
}
}
```


### Queue trigger, write docs using IAsyncCollector

The following example shows a [C# function](functions-dotnet-class-library) that adds a collection of documents to a database, using data provided in a queue message JSON.

```
using Microsoft.Azure.WebJobs;
using Microsoft.Azure.WebJobs.Host;
using System.Threading.Tasks;
namespace CosmosDBSamplesV1
{
public static class WriteDocsIAsyncCollector
{
[FunctionName("WriteDocsIAsyncCollector")]
public static async Task Run(
[QueueTrigger("todoqueueforwritemulti")] ToDoItem[] toDoItemsIn,
[DocumentDB(
databaseName: "ToDoItems",
collectionName: "Items",
ConnectionStringSetting = "CosmosDBConnection")]
IAsyncCollector<ToDoItem> toDoItemsOut,
TraceWriter log)
{
log.Info($"C# Queue trigger function processed {toDoItemsIn?.Length} items");
foreach (ToDoItem toDoItem in toDoItemsIn)
{
log.Info($"Description={toDoItem.Description}");
await toDoItemsOut.AddAsync(toDoItem);
}
}
}
}
```


## Output - attributes

In [in-process C# class libraries](functions-dotnet-class-library), use the [DocumentDB](https://github.com/Azure/azure-webjobs-sdk-extensions/blob/v2.x/src/WebJobs.Extensions.DocumentDB/DocumentDBAttribute.cs) attribute.

The attribute's constructor takes the database name and collection name. For information about those settings and other properties that you can configure, see [Output - configuration](#output---configuration). Here's a `DocumentDB`

attribute example in a method signature:

```
[FunctionName("QueueToDocDB")]
public static void Run(
[QueueTrigger("myqueue-items", Connection = "AzureWebJobsStorage")] string myQueueItem,
[DocumentDB("ToDoList", "Items", Id = "id", ConnectionStringSetting = "myCosmosDB")] out dynamic document)
{
...
}
```


For a complete example, see [Output](#output).

## Output - configuration

The following table explains the binding configuration properties that you set in the *function.json* file and the `DocumentDB`

attribute.

| function.json property | Attribute property | Description |
|---|---|---|
type |
n/a | Must be set to `documentdb` . |
direction |
n/a | Must be set to `out` . |
name |
n/a | Name of the binding parameter that represents the document in the function. |
databaseName |
DatabaseName |
The database containing the collection where the document is created. |
collectionName |
CollectionName |
The name of the collection where the document is created. |
createIfNotExists |
CreateIfNotExists |
A boolean value to indicate whether the collection is created when it doesn't exist. The default is false because new collections are created with reserved throughput, which has cost implications. For more information, see the
|
partitionKey |
PartitionKey |
When `CreateIfNotExists` is true, defines the partition key path for the created collection. |
collectionThroughput |
CollectionThroughput |
When `CreateIfNotExists` is true, defines the
|
connection |
ConnectionStringSetting |
The name of the app setting containing your Azure Cosmos DB connection string. |

When you're developing locally, add your application settings in the [local.settings.json file](functions-develop-local#local-settings-file) in the `Values`

collection.

## Output - usage

By default, when you write to the output parameter in your function, a document is created in your database. This document has an automatically generated GUID as the document ID. You can specify the document ID of the output document by specifying the `id`

property in the JSON object passed to the output parameter.

Note

When you specify the ID of an existing document, it gets overwritten by the new output document.

## Exceptions and return codes

| Binding | Reference |
|---|---|
| Azure Cosmos DB |
|
