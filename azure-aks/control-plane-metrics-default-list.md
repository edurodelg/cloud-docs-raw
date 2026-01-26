---
source_url: https://learn.microsoft.com/en-us/azure/aks/control-plane-metrics-default-list
fetched_at: 2026-01-26T22:55:50.245679
---

# Azure Kubernetes Service monitoring data reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article contains all the monitoring reference information for this service.

See [Monitor Azure Kubernetes Service (AKS)](monitor-aks) for details on the data you can collect for AKS and how to use it.

## Metrics

This section lists all the automatically collected platform metrics for this service. These metrics are also part of the global list of [all platform metrics supported in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index#supported-metrics-per-resource-type).

For information on metric retention, see [Azure Monitor Metrics overview](/en-us/azure/azure-monitor/essentials/data-platform-metrics#retention-of-metrics).

### Supported metrics for Microsoft.ContainerService/managedClusters

The following table lists the metrics available for the Microsoft.ContainerService/managedClusters resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

### Category: API Server

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
API Server CPU Usage PercentageMaximum CPU percentage (based off current limit) used by API server pod across instances |
`apiserver_cpu_usage_percentage` |
Percent | Maximum, Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
API Server Memory Usage PercentageMaximum memory percentage (based off current limit) used by API server pod across instances |
`apiserver_memory_usage_percentage` |
Percent | Maximum, Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |

### Category: API Server (PREVIEW)

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Inflight RequestsMaximum number of currently used inflight requests on the apiserver per request kind in the last second |
`apiserver_current_inflight_requests` |
Count | Total (Sum), Average | `requestKind` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |

### Category: Cluster Autoscaler (PREVIEW)

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Cluster HealthDetermines whether or not cluster autoscaler will take action on the cluster |
`cluster_autoscaler_cluster_safe_to_autoscale` |
Count | Total (Sum), Average | <none> | PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Scale Down CooldownDetermines if the scale down is in cooldown - No nodes will be removed during this timeframe |
`cluster_autoscaler_scale_down_in_cooldown` |
Count | Total (Sum), Average | <none> | PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Unneeded NodesCluster auotscaler marks those nodes as candidates for deletion and are eventually deleted |
`cluster_autoscaler_unneeded_nodes_count` |
Count | Total (Sum), Average | <none> | PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Unschedulable PodsNumber of pods that are currently unschedulable in the cluster |
`cluster_autoscaler_unschedulable_pods_count` |
Count | Total (Sum), Average | <none> | PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |

### Category: ETCD

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
ETCD CPU Usage PercentageMaximum CPU percentage (based off current limit) used by ETCD pod across instances |
`etcd_cpu_usage_percentage` |
Percent | Maximum, Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
ETCD Database Usage PercentageMaximum utilization of the ETCD database across instances |
`etcd_database_usage_percentage` |
Percent | Maximum, Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
ETCD Memory Usage PercentageMaximum memory percentage (based off current limit) used by ETCD pod across instances |
`etcd_memory_usage_percentage` |
Percent | Maximum, Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |

### Category: Nodes

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Total number of available cpu cores in a managed clusterTotal number of available cpu cores in a managed cluster |
`kube_node_status_allocatable_cpu_cores` |
Count | Total (Sum), Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Total amount of available memory in a managed clusterTotal amount of available memory in a managed cluster |
`kube_node_status_allocatable_memory_bytes` |
Bytes | Total (Sum), Average | <none> | PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Statuses for various node conditionsStatuses for various node conditions |
`kube_node_status_condition` |
Count | Total (Sum), Average | `condition` , `status` , `status2` , `node` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |

### Category: Nodes (PREVIEW)

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
CPU Usage MillicoresAggregated measurement of CPU utilization in millicores across the cluster |
`node_cpu_usage_millicores` |
MilliCores | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
CPU Usage PercentageAggregated average CPU utilization measured in percentage across the cluster |
`node_cpu_usage_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Disk Used BytesDisk space used in bytes by device |
`node_disk_usage_bytes` |
Bytes | Maximum, Average | `node` , `nodepool` , `device` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Disk Used PercentageDisk space used in percent by device |
`node_disk_usage_percentage` |
Percent | Maximum, Average | `node` , `nodepool` , `device` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory RSS BytesContainer RSS memory used in bytes |
`node_memory_rss_bytes` |
Bytes | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory RSS PercentageContainer RSS memory used in percent |
`node_memory_rss_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory Working Set BytesContainer working set memory used in bytes |
`node_memory_working_set_bytes` |
Bytes | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory Working Set PercentageContainer working set memory used in percent |
`node_memory_working_set_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Network In BytesNetwork received bytes |
`node_network_in_bytes` |
Bytes | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Network Out BytesNetwork transmitted bytes |
`node_network_out_bytes` |
Bytes | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |

### Category: Pods

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Number of pods by phaseNumber of pods by phase |
`kube_pod_status_phase` |
Count | Total (Sum), Average | `phase` , `namespace` , `pod` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Number of pods in Ready stateNumber of pods in Ready state |
`kube_pod_status_ready` |
Count | Total (Sum), Average | `namespace` , `pod` , `condition` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |

### Supported metrics for microsoft.kubernetes/connectedClusters

The following table lists the metrics available for the microsoft.kubernetes/connectedClusters resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

### Category: Availability

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Total number of cpu cores in a connected clusterTotal number of cpu cores in a connected cluster |
`capacity_cpu_cores` |
Count | Total (Sum), Average | <none> | PT1M | Yes |

### Category: Nodes (PREVIEW)

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
CPU Usage PercentageAggregated average CPU utilization measured in percentage across the cluster |
`node_cpu_usage_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Disk Used PercentageDisk space used in percent by device |
`node_disk_usage_percentage` |
Percent | Maximum, Average | `node` , `nodepool` , `device` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory RSS PercentageContainer RSS memory used in percent |
`node_memory_rss_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |
Memory Working Set PercentageContainer working set memory used in percent |
`node_memory_working_set_percentage` |
Percent | Maximum, Average | `node` , `nodepool` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | Yes |

### Supported metrics for microsoft.kubernetesconfiguration/extensions

The following table lists the metrics available for the microsoft.kubernetesconfiguration/extensions resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

### Category: Latency

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Api Request Duration in SecondsHistogram of request durations |
`ApiRequestDurationSeconds` |
Seconds | Average | `AppName` , `GpuEnabled` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Ingestion TimeTotal ingestion time in minutes |
`IngestionTimeMinutes` |
Seconds | Average | `AppName` , `GpuEnabled` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Input Preprocessing Time (Milliseconds)Input preprocessing time in milliseconds |
`InputPreprocessingTimeMilliseconds` |
Milliseconds | Average | `GpuEnabled` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Call LLM Total Time in SecondsTotal call_llm time in seconds |
`TotalCallLLMTimeSeconds` |
Seconds | Average | `AppName` , `GpuEnabled` , `LLMProvider` , `OutputLength` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Embedding Generation Total Time in SecondsTotal time taken to generate embeddings from local model |
`TotalGenerateEmbeddingsTimeSeconds` |
Seconds | Average | `AppName` , `GpuEnabled` , `InputLength` , `OutputLength` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Hybrid Search Embedding Generation Total Time in SecondsTotal time taken to generate Hybrid Search embeddings from local model |
`TotalGenerateHybridSearchEmbeddingsTimeSeconds` |
Seconds | Average | `AppName` , `GpuEnabled` , `InputLength` , `OutputLength` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Reranking Generation Total Time in SecondsTotal time taken to generate Reranking |
`TotalGenerateRerankingTimeSeconds` |
Seconds | Average | `AppName` , `GpuEnabled` , `InputLength` , `OutputLength` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Get Chat History Summary Total Time in MillisecondsTotal get_chat_history_summary time in milliseconds |
`TotalGetChatHistorySummaryTimeMilliseconds` |
Milliseconds | Average | `AppName` , `GpuEnabled` , `InputHistoryPairs` , `LLMProvider` , `MaxTokens` , `OutputLength` , `Temperature` , `TopP` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Get LLM Payload Total Time in MillisecondsTotal get_llm_payload time in milliseconds |
`TotalGetLLMPayloadTimeMilliseconds` |
Milliseconds | Average | `AppName` , `DiversityPenalty` , `GpuEnabled` , `LengthPenalty` , `LLMProvider` , `MaxTokens` , `RepetitionPenalty` , `Temperature` , `TopP` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Get Hybrid Search Total Time in MillisecondsTotal hybrid search time in milliseconds |
`TotalHybridSearchTimeMilliseconds` |
Milliseconds | Average | `AppName` , `ChunkMinScore` , `GpuEnabled` , `IndexType` , `InputLength` , `MetricType` , `TopK` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Inference Total Time in SecondsTotal inference time in seconds |
`TotalInferenceTimeSeconds` |
Seconds | Average | `AppName` , `DiversityPenalty` , `GpuEnabled` , `InputLength` , `LLMProvider` , `MaxTokens` , `OutputLength` , `RepetitionPenalty` , `Temperature` , `TopK` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Chunks Search Total Time in MillisecondsTotal search chunks time in milliseconds |
`TotalSearchChunksTimeMilliseconds` |
Milliseconds | Average | `AppName` , `EmbeddingIndexName` , `GpuEnabled` , `InputLength` , `OutputChunks` , `TopK` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Search Total Time in MillisecondsTotal time taken to search |
`TotalSearchTimeMilliseconds` |
Milliseconds | Average | `AppName` , `ChunkMinScore` , `GpuEnabled` , `InputLength` , `QueryType` , `TopK` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Similarity Search Total Time in MillisecondsTotal time taken to search for similar documents |
`TotalSimilaritySearchTimeMilliseconds` |
Milliseconds | Average | `AppName` , `GpuEnabled` , `InputLength` , `ChunkMinScore` , `IndexType` , `MetricType` , `TopK` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |

### Category: Traffic

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Active PDU SessionsNumber of Active PDU Sessions |
`ActiveSessionCount` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | No |
API Failure CountCount of failed API requests |
`ApiFailureCount` |
Count | Count | `EndpointName` , `GpuEnabled` , `StatusCode` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
API Request CountTotal number of API requests |
`ApiRequestCount` |
Count | Count | `AppName` , `GpuEnabled` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
API Success CountCount of successful API requests |
`ApiSuccessCount` |
Count | Count | `EndpointName` , `GpuEnabled` , `StatusCode` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Authentication AttemptsAuthentication attempts rate (per minute) |
`AuthAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Authentication FailuresAuthentication failure rate (per minute) |
`AuthFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Result` |
PT1M | Yes |
Authentication SuccessesAuthentication success rate (per minute) |
`AuthSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Connected NodeBsNumber of connected gNodeBs or eNodeBs |
`ConnectedNodebs` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
DeRegistration AttemptsUE deregistration attempts rate (per minute) |
`DeRegistrationAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
DeRegistration SuccessesUE deregistration success rate (per minute) |
`DeRegistrationSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Evaluation API Request CountTotal number of Evaluation API requests |
`EvaluationApiRequestCount` |
Count | Count | `AppName` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Failed Skipped CountCount of failed or skipped files |
`FailedSkippedCount` |
Count | Count | `Category` , `GpuEnabled` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
File Ingestion RateTotal files ingested per Job |
`FileIngestionRate` |
Count | Total (Sum) | `AppName` , `GpuEnabled` , `FileType` , `JobID` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Hybrid Search Model API Request CountTotal number of Hybrid Search Model API requests |
`HybridSearchModelApiRequestCount` |
Count | Count | `AppName` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Inference Answer FeedbackInference Answer Feedback |
`InferenceAnswerFeedback` |
Count | Count | `AppName` , `ChunkMinScore` , `ChunkScores` , `GpuEnabled` , `LLMProvider` , `RunId` , `Thumb` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Inference API Request CountNumber of Inference API requests |
`InferenceApiRequestCount` |
Count | Count | `AppName` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Ingestion API Request CountNumber of Ingestion API requests |
`IngestionApiRequestCount` |
Count | Count | `AppName` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Number of EvaluationsNumber of Evaluations |
`NumberOfEvaluations` |
Count | Count | `AppName` , `GpuEnabled` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Number of JobsNumber of jobs |
`NumberOfJobs` |
Count | Count | `AppName` , `GpuEnabled` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Paging AttemptsPaging attempts rate (per minute) |
`PagingAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Paging FailuresPaging failure rate (per minute) |
`PagingFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Provisioned SubscribersNumber of provisioned subscribers |
`ProvisionedSubscribers` |
Count | Total (Sum) | `PccpId` , `SiteId` |
PT1M | No |
RAN Setup FailuresRAN setup failure rate (per minute) |
`RanSetupFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Cause` |
PT1M | Yes |
RAN Setup RequestsRAN setup reuests rate (per minute) |
`RanSetupRequest` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
RAN Setup ResponsesRAN setup response rate (per minute) |
`RanSetupResponse` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Registered SubscribersNumber of registered subscribers |
`RegisteredSubscribers` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Registered Subscribers ConnectedNumber of registered and connected subscribers |
`RegisteredSubscribersConnected` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Registered Subscribers IdleNumber of registered and idle subscribers |
`RegisteredSubscribersIdle` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Registration AttemptsRegistration attempts rate (per minute) |
`RegistrationAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Registration FailuresRegistration failure rate (per minute) |
`RegistrationFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Result` |
PT1M | Yes |
Registration SuccessesRegistration success rate (per minute) |
`RegistrationSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Service Request AttemptsService request attempts rate (per minute) |
`ServiceRequestAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Service Request FailuresService request failure rate (per minute) |
`ServiceRequestFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Result` , `Tai` |
PT1M | Yes |
Service Request SuccessesService request success rate (per minute) |
`ServiceRequestSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Session Establishment AttemptsPDU session establishment attempts rate (per minute) |
`SessionEstablishmentAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Dnn` |
PT1M | Yes |
Session Establishment FailuresPDU session establishment failure rate (per minute) |
`SessionEstablishmentFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Dnn` |
PT1M | Yes |
Session Establishment SuccessesPDU session establishment success rate (per minute) |
`SessionEstablishmentSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` , `Dnn` |
PT1M | Yes |
Session ReleasesSession release rate (per minute) |
`SessionRelease` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
UE Context Release CommandsUE context release command message rate (per minute) |
`UeContextReleaseCommand` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
UE Context Release CompletesUE context release complete message rate (per minute) |
`UeContextReleaseComplete` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
UE Context Release RequestsUE context release request message rate (per minute) |
`UeContextReleaseRequest` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
User Plane BandwidthUser plane bandwidth in bits/second. |
`UserPlaneBandwidth` |
BitsPerSecond | Total (Sum) | `PcdpId` , `SiteId` , `Direction` , `Interface` |
PT1M | No |
User Plane Packet Drop RateUser plane packet drop rate (packets/sec) |
`UserPlanePacketDropRate` |
CountPerSecond | Total (Sum) | `PcdpId` , `SiteId` , `Cause` , `Direction` , `Interface` |
PT1M | No |
User Plane Packet RateUser plane packet rate (packets/sec) |
`UserPlanePacketRate` |
CountPerSecond | Total (Sum) | `PcdpId` , `SiteId` , `Direction` , `Interface` |
PT1M | No |
VectorDB API Request CountTotal number of API requests to VectorDB |
`VectorDbApiRequestCount` |
Count | Count | `AppName` , `Method` , `Route` |
PT1M, PT5M, PT15M, PT30M, PT1H, PT6H, PT12H | No |
Xn Handover AttemptsHandover attempts rate (per minute) |
`XnHandoverAttempt` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Xn Handover FailuresHandover failure rate (per minute) |
`XnHandoverFailure` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |
Xn Handover SuccessesHandover success rate (per minute) |
`XnHandoverSuccess` |
Count | Total (Sum) | `3gppGen` , `PccpId` , `SiteId` |
PT1M | Yes |

### Supported metrics for Microsoft.Compute/virtualMachines

The following table lists the metrics available for the Microsoft.Compute/virtualMachines resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

### Category: Other

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Available Memory BytesAmount of physical memory, in bytes, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Bytes` |
Bytes | Average | <none> | PT1M | Yes |
Available Memory PercentageAmount of physical memory, in percentage, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Percentage` |
Percent | Average | <none> | PT1M | Yes |
CPU Credits ConsumedTotal number of credits consumed by the Virtual Machine. Only available on B-series burstable VMs |
`CPU Credits Consumed` |
Count | Average | <none> | PT1M | Yes |
CPU Credits RemainingTotal number of credits available to burst. Only available on B-series burstable VMs |
`CPU Credits Remaining` |
Count | Average | <none> | PT1M | Yes |
Data Disk Bandwidth Consumed PercentagePercentage of data disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`Data Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk IOPS Consumed PercentagePercentage of data disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`Data Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk LatencyAverage time to complete each IO during monitoring period for Data Disk. Values are in milliseconds. |
`Data Disk Latency` |
Milliseconds | Average | `LUN` |
PT1M | Yes |
Data Disk Max Burst BandwidthMaximum bytes per second throughput Data Disk can achieve with bursting |
`Data Disk Max Burst Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Max Burst IOPSMaximum IOPS Data Disk can achieve with bursting |
`Data Disk Max Burst IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Queue DepthData Disk Queue Depth(or Queue Length) |
`Data Disk Queue Depth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period |
`Data Disk Read Bytes/sec` |
BytesPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Read Operations/SecRead IOPS from a single disk during monitoring period |
`Data Disk Read Operations/Sec` |
CountPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Target BandwidthBaseline bytes per second throughput Data Disk can achieve without bursting |
`Data Disk Target Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Target IOPSBaseline IOPS Data Disk can achieve without bursting |
`Data Disk Target IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Used Burst BPS Credits PercentagePercentage of Data Disk burst bandwidth credits used so far |
`Data Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk Used Burst IO Credits PercentagePercentage of Data Disk burst I/O credits used so far |
`Data Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period |
`Data Disk Write Bytes/sec` |
BytesPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Write Operations/SecWrite IOPS from a single disk during monitoring period |
`Data Disk Write Operations/Sec` |
CountPerSecond | Average | `LUN` |
PT1M | Yes |
Disk Read BytesBytes read from disk during monitoring period |
`Disk Read Bytes` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Disk Read Operations/SecDisk Read IOPS |
`Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Disk Write BytesBytes written to disk during monitoring period |
`Disk Write Bytes` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Disk Write Operations/SecDisk Write IOPS |
`Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Inbound FlowsInbound Flows are number of current flows in the inbound direction (traffic going into the VM) |
`Inbound Flows` |
Count | Average | <none> | PT1M | Yes |
Inbound Flows Maximum Creation RateThe maximum creation rate of inbound flows (traffic going into the VM) |
`Inbound Flows Maximum Creation Rate` |
CountPerSecond | Average | <none> | PT1M | Yes |
Network In Billable (Deprecated)The number of billable bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) (Deprecated) |
`Network In` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network In TotalThe number of bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) |
`Network In Total` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network Out Billable (Deprecated)The number of billable bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) (Deprecated) |
`Network Out` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network Out TotalThe number of bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) |
`Network Out Total` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
OS Disk Bandwidth Consumed PercentagePercentage of operating system disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`OS Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk IOPS Consumed PercentagePercentage of operating system disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`OS Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk LatencyAverage time to complete each IO during monitoring period for OS Disk. Values are in milliseconds. |
`OS Disk Latency` |
Milliseconds | Average | <none> | PT1M | Yes |
OS Disk Max Burst BandwidthMaximum bytes per second throughput OS Disk can achieve with bursting |
`OS Disk Max Burst Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Max Burst IOPSMaximum IOPS OS Disk can achieve with bursting |
`OS Disk Max Burst IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Queue DepthOS Disk Queue Depth(or Queue Length) |
`OS Disk Queue Depth` |
Count | Average | <none> | PT1M | Yes |
OS Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for OS disk |
`OS Disk Read Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
OS Disk Read Operations/SecRead IOPS from a single disk during monitoring period for OS disk |
`OS Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
OS Disk Target BandwidthBaseline bytes per second throughput OS Disk can achieve without bursting |
`OS Disk Target Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Target IOPSBaseline IOPS OS Disk can achieve without bursting |
`OS Disk Target IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Used Burst BPS Credits PercentagePercentage of OS Disk burst bandwidth credits used so far |
`OS Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk Used Burst IO Credits PercentagePercentage of OS Disk burst I/O credits used so far |
`OS Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for OS disk |
`OS Disk Write Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
OS Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for OS disk |
`OS Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Outbound FlowsOutbound Flows are number of current flows in the outbound direction (traffic going out of the VM) |
`Outbound Flows` |
Count | Average | <none> | PT1M | Yes |
Outbound Flows Maximum Creation RateThe maximum creation rate of outbound flows (traffic going out of the VM) |
`Outbound Flows Maximum Creation Rate` |
CountPerSecond | Average | <none> | PT1M | Yes |
Percentage CPUThe percentage of allocated compute units that are currently in use by the Virtual Machine(s) |
`Percentage CPU` |
Percent | Average | <none> | PT1M | Yes |
Premium Data Disk Cache Read HitPremium Data Disk Cache Read Hit |
`Premium Data Disk Cache Read Hit` |
Percent | Average | `LUN` |
PT1M | Yes |
Premium Data Disk Cache Read MissPremium Data Disk Cache Read Miss |
`Premium Data Disk Cache Read Miss` |
Percent | Average | `LUN` |
PT1M | Yes |
Premium OS Disk Cache Read HitPremium OS Disk Cache Read Hit |
`Premium OS Disk Cache Read Hit` |
Percent | Average | <none> | PT1M | Yes |
Premium OS Disk Cache Read MissPremium OS Disk Cache Read Miss |
`Premium OS Disk Cache Read Miss` |
Percent | Average | <none> | PT1M | Yes |
Temp Disk Latency (Preview)Average time to complete each IO during monitoring period for Temp Disk. Values are in milliseconds. |
`Temp Disk Latency` |
Milliseconds | Average | <none> | PT1M | Yes |
Temp Disk Queue DepthTemp Disk Queue Depth(or Queue Length). |
`Temp Disk Queue Depth` |
Count | Average | <none> | PT1M | Yes |
Temp Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Read Operations/SecRead IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
VM Cached Bandwidth Consumed PercentagePercentage of cached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached Bandwidth Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Cached IOPS Consumed PercentagePercentage of cached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached IOPS Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Cached Used Burst BPS Credits PercentagePercentage of Cached Burst BPS Credits used by the VM. |
`VM Local Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Cached Used Burst IO Credits PercentagePercentage of Cached Burst IO Credits used by the VM. |
`VM Local Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Used Burst BPS Credits PercentagePercentage of Uncached Burst BPS Credits used by the VM. |
`VM Remote Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Used Burst IO Credits PercentagePercentage of Uncached Burst IO Credits used by the VM. |
`VM Remote Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Bandwidth Consumed PercentagePercentage of uncached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached Bandwidth Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Uncached IOPS Consumed PercentagePercentage of uncached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached IOPS Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Availability Metric (Preview)Measure of Availability of Virtual machines over time. |
`VmAvailabilityMetric` |
Count | Average, Minimum, Maximum | `Context` |
PT1M | Yes |

### Supported metrics for Microsoft.Compute/virtualmachineScaleSets

The following table lists the metrics available for the Microsoft.Compute/virtualmachineScaleSets resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Available Memory BytesAmount of physical memory, in bytes, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Bytes` |
Bytes | Average | `VMName` |
PT1M | Yes |
Available Memory PercentageAmount of physical memory, in percentage, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Percentage` |
Percent | Average | `VMName` |
PT1M | Yes |
CPU Credits ConsumedTotal number of credits consumed by the Virtual Machine. Only available on B-series burstable VMs |
`CPU Credits Consumed` |
Count | Average | `VMName` |
PT1M | Yes |
CPU Credits RemainingTotal number of credits available to burst. Only available on B-series burstable VMs |
`CPU Credits Remaining` |
Count | Average | `VMName` |
PT1M | Yes |
Data Disk Bandwidth Consumed PercentagePercentage of data disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`Data Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk IOPS Consumed PercentagePercentage of data disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`Data Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk LatencyAverage time to complete each IO during monitoring period for Data Disk. Values are in milliseconds. |
`Data Disk Latency` |
Milliseconds | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Max Burst BandwidthMaximum bytes per second throughput Data Disk can achieve with bursting |
`Data Disk Max Burst Bandwidth` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Max Burst IOPSMaximum IOPS Data Disk can achieve with bursting |
`Data Disk Max Burst IOPS` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Queue DepthData Disk Queue Depth(or Queue Length) |
`Data Disk Queue Depth` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period |
`Data Disk Read Bytes/sec` |
BytesPerSecond | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Read Operations/SecRead IOPS from a single disk during monitoring period |
`Data Disk Read Operations/Sec` |
CountPerSecond | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Target BandwidthBaseline bytes per second throughput Data Disk can achieve without bursting |
`Data Disk Target Bandwidth` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Target IOPSBaseline IOPS Data Disk can achieve without bursting |
`Data Disk Target IOPS` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Used Burst BPS Credits PercentagePercentage of Data Disk burst bandwidth credits used so far |
`Data Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Used Burst IO Credits PercentagePercentage of Data Disk burst I/O credits used so far |
`Data Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period |
`Data Disk Write Bytes/sec` |
BytesPerSecond | Average | `LUN` , `VMName` |
PT1M | Yes |
Data Disk Write Operations/SecWrite IOPS from a single disk during monitoring period |
`Data Disk Write Operations/Sec` |
CountPerSecond | Average | `LUN` , `VMName` |
PT1M | Yes |
Disk Read BytesBytes read from disk during monitoring period |
`Disk Read Bytes` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
Disk Read Operations/SecDisk Read IOPS |
`Disk Read Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Disk Write BytesBytes written to disk during monitoring period |
`Disk Write Bytes` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
Disk Write Operations/SecDisk Write IOPS |
`Disk Write Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Inbound FlowsInbound Flows are number of current flows in the inbound direction (traffic going into the VM) |
`Inbound Flows` |
Count | Average | `VMName` |
PT1M | Yes |
Inbound Flows Maximum Creation RateThe maximum creation rate of inbound flows (traffic going into the VM) |
`Inbound Flows Maximum Creation Rate` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Network In Billable (Deprecated)The number of billable bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) (Deprecated) |
`Network In` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
Network In TotalThe number of bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) |
`Network In Total` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
Network Out Billable (Deprecated)The number of billable bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) (Deprecated) |
`Network Out` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
Network Out TotalThe number of bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) |
`Network Out Total` |
Bytes | Total (Sum) | `VMName` |
PT1M | Yes |
OS Disk Bandwidth Consumed PercentagePercentage of operating system disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`OS Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk IOPS Consumed PercentagePercentage of operating system disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`OS Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk LatencyAverage time to complete each IO during monitoring period for OS Disk. Values are in milliseconds. |
`OS Disk Latency` |
Milliseconds | Average | `VMName` |
PT1M | Yes |
OS Disk Max Burst BandwidthMaximum bytes per second throughput OS Disk can achieve with bursting |
`OS Disk Max Burst Bandwidth` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Max Burst IOPSMaximum IOPS OS Disk can achieve with bursting |
`OS Disk Max Burst IOPS` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Queue DepthOS Disk Queue Depth(or Queue Length) |
`OS Disk Queue Depth` |
Count | Average | `VMName` |
PT1M | Yes |
OS Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for OS disk |
`OS Disk Read Bytes/sec` |
BytesPerSecond | Average | `VMName` |
PT1M | Yes |
OS Disk Read Operations/SecRead IOPS from a single disk during monitoring period for OS disk |
`OS Disk Read Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
OS Disk Target BandwidthBaseline bytes per second throughput OS Disk can achieve without bursting |
`OS Disk Target Bandwidth` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Target IOPSBaseline IOPS OS Disk can achieve without bursting |
`OS Disk Target IOPS` |
Count | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Used Burst BPS Credits PercentagePercentage of OS Disk burst bandwidth credits used so far |
`OS Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Used Burst IO Credits PercentagePercentage of OS Disk burst I/O credits used so far |
`OS Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
OS Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for OS disk |
`OS Disk Write Bytes/sec` |
BytesPerSecond | Average | `VMName` |
PT1M | Yes |
OS Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for OS disk |
`OS Disk Write Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Outbound FlowsOutbound Flows are number of current flows in the outbound direction (traffic going out of the VM) |
`Outbound Flows` |
Count | Average | `VMName` |
PT1M | Yes |
Outbound Flows Maximum Creation RateThe maximum creation rate of outbound flows (traffic going out of the VM) |
`Outbound Flows Maximum Creation Rate` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Percentage CPUThe percentage of allocated compute units that are currently in use by the Virtual Machine(s) |
`Percentage CPU` |
Percent | Average | `VMName` |
PT1M | Yes |
Premium Data Disk Cache Read HitPremium Data Disk Cache Read Hit |
`Premium Data Disk Cache Read Hit` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Premium Data Disk Cache Read MissPremium Data Disk Cache Read Miss |
`Premium Data Disk Cache Read Miss` |
Percent | Average | `LUN` , `VMName` |
PT1M | Yes |
Premium OS Disk Cache Read HitPremium OS Disk Cache Read Hit |
`Premium OS Disk Cache Read Hit` |
Percent | Average | `VMName` |
PT1M | Yes |
Premium OS Disk Cache Read MissPremium OS Disk Cache Read Miss |
`Premium OS Disk Cache Read Miss` |
Percent | Average | `VMName` |
PT1M | Yes |
Temp Disk Latency (Preview)Average time to complete each IO during monitoring period for Temp Disk. Values are in milliseconds. |
`Temp Disk Latency` |
Milliseconds | Average | `VMName` |
PT1M | Yes |
Temp Disk Queue DepthTemp Disk Queue Depth(or Queue Length). |
`Temp Disk Queue Depth` |
Count | Average | `VMName` |
PT1M | Yes |
Temp Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Bytes/sec` |
BytesPerSecond | Average | `VMName` |
PT1M | Yes |
Temp Disk Read Operations/SecRead IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
Temp Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Bytes/sec` |
BytesPerSecond | Average | `VMName` |
PT1M | Yes |
Temp Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Operations/Sec` |
CountPerSecond | Average | `VMName` |
PT1M | Yes |
VM Cached Bandwidth Consumed PercentagePercentage of cached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached Bandwidth Consumed Percentage` |
Percent | Average | `VMName` |
PT1M | Yes |
VM Cached IOPS Consumed PercentagePercentage of cached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached IOPS Consumed Percentage` |
Percent | Average | `VMName` |
PT1M | Yes |
VM Cached Used Burst BPS Credits PercentagePercentage of Cached Burst BPS Credits used by the VM. |
`VM Local Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | `VMName` |
PT1M | Yes |
VM Cached Used Burst IO Credits PercentagePercentage of Cached Burst IO Credits used by the VM. |
`VM Local Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | `VMName` |
PT1M | Yes |
VM Uncached Used Burst BPS Credits PercentagePercentage of Uncached Burst BPS Credits used by the VM. |
`VM Remote Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | `VMName` |
PT1M | Yes |
VM Uncached Used Burst IO Credits PercentagePercentage of Uncached Burst IO Credits used by the VM. |
`VM Remote Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | `VMName` |
PT1M | Yes |
VM Uncached Bandwidth Consumed PercentagePercentage of uncached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached Bandwidth Consumed Percentage` |
Percent | Average | `VMName` |
PT1M | Yes |
VM Uncached IOPS Consumed PercentagePercentage of uncached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached IOPS Consumed Percentage` |
Percent | Average | `VMName` |
PT1M | Yes |
VM Availability Metric (Preview)Measure of Availability of Virtual machines over time. |
`VmAvailabilityMetric` |
Count | Average, Minimum, Maximum | `VMName` , `Context` |
PT1M | Yes |

### Supported metrics for Microsoft.Compute/virtualMachineScaleSets/virtualMachines

The following table lists the metrics available for the Microsoft.Compute/virtualMachineScaleSets/virtualMachines resource type.

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Available Memory BytesAmount of physical memory, in bytes, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Bytes` |
Bytes | Average | <none> | PT1M | Yes |
Available Memory PercentageAmount of physical memory, in percentage, immediately available for allocation to a process or for system use in the Virtual Machine |
`Available Memory Percentage` |
Percent | Average | <none> | PT1M | Yes |
CPU Credits ConsumedTotal number of credits consumed by the Virtual Machine. Only available on B-series burstable VMs |
`CPU Credits Consumed` |
Count | Average | <none> | PT1M | Yes |
CPU Credits RemainingTotal number of credits available to burst. Only available on B-series burstable VMs |
`CPU Credits Remaining` |
Count | Average | <none> | PT1M | Yes |
Data Disk Bandwidth Consumed PercentagePercentage of data disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`Data Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk IOPS Consumed PercentagePercentage of data disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`Data Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk LatencyAverage time to complete each IO during monitoring period for Data Disk. Values are in milliseconds. |
`Data Disk Latency` |
Milliseconds | Average | `LUN` |
PT1M | Yes |
Data Disk Max Burst BandwidthMaximum bytes per second throughput Data Disk can achieve with bursting |
`Data Disk Max Burst Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Max Burst IOPSMaximum IOPS Data Disk can achieve with bursting |
`Data Disk Max Burst IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Queue DepthData Disk Queue Depth(or Queue Length) |
`Data Disk Queue Depth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period |
`Data Disk Read Bytes/sec` |
BytesPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Read Operations/SecRead IOPS from a single disk during monitoring period |
`Data Disk Read Operations/Sec` |
CountPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Target BandwidthBaseline bytes per second throughput Data Disk can achieve without bursting |
`Data Disk Target Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Target IOPSBaseline IOPS Data Disk can achieve without bursting |
`Data Disk Target IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
Data Disk Used Burst BPS Credits PercentagePercentage of Data Disk burst bandwidth credits used so far |
`Data Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk Used Burst IO Credits PercentagePercentage of Data Disk burst I/O credits used so far |
`Data Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
Data Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period |
`Data Disk Write Bytes/sec` |
BytesPerSecond | Average | `LUN` |
PT1M | Yes |
Data Disk Write Operations/SecWrite IOPS from a single disk during monitoring period |
`Data Disk Write Operations/Sec` |
CountPerSecond | Average | `LUN` |
PT1M | Yes |
Disk Read BytesBytes read from disk during monitoring period |
`Disk Read Bytes` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Disk Read Operations/SecDisk Read IOPS |
`Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Disk Write BytesBytes written to disk during monitoring period |
`Disk Write Bytes` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Disk Write Operations/SecDisk Write IOPS |
`Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Inbound FlowsInbound Flows are number of current flows in the inbound direction (traffic going into the VM) |
`Inbound Flows` |
Count | Average | <none> | PT1M | Yes |
Inbound Flows Maximum Creation RateThe maximum creation rate of inbound flows (traffic going into the VM) |
`Inbound Flows Maximum Creation Rate` |
CountPerSecond | Average | <none> | PT1M | Yes |
Network In Billable (Deprecated)The number of billable bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) (Deprecated) |
`Network In` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network In TotalThe number of bytes received on all network interfaces by the Virtual Machine(s) (Incoming Traffic) |
`Network In Total` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network Out Billable (Deprecated)The number of billable bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) (Deprecated) |
`Network Out` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
Network Out TotalThe number of bytes out on all network interfaces by the Virtual Machine(s) (Outgoing Traffic) |
`Network Out Total` |
Bytes | Total (Sum) | <none> | PT1M | Yes |
OS Disk Bandwidth Consumed PercentagePercentage of operating system disk bandwidth consumed per minute. Only available on VM series that support premium storage. |
`OS Disk Bandwidth Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk IOPS Consumed PercentagePercentage of operating system disk I/Os consumed per minute. Only available on VM series that support premium storage. |
`OS Disk IOPS Consumed Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk LatencyAverage time to complete each IO during monitoring period for OS Disk. Values are in milliseconds. |
`OS Disk Latency` |
Milliseconds | Average | <none> | PT1M | Yes |
OS Disk Max Burst BandwidthMaximum bytes per second throughput OS Disk can achieve with bursting |
`OS Disk Max Burst Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Max Burst IOPSMaximum IOPS OS Disk can achieve with bursting |
`OS Disk Max Burst IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Queue DepthOS Disk Queue Depth(or Queue Length) |
`OS Disk Queue Depth` |
Count | Average | <none> | PT1M | Yes |
OS Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for OS disk |
`OS Disk Read Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
OS Disk Read Operations/SecRead IOPS from a single disk during monitoring period for OS disk |
`OS Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
OS Disk Target BandwidthBaseline bytes per second throughput OS Disk can achieve without bursting |
`OS Disk Target Bandwidth` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Target IOPSBaseline IOPS OS Disk can achieve without bursting |
`OS Disk Target IOPS` |
Count | Average | `LUN` |
PT1M | Yes |
OS Disk Used Burst BPS Credits PercentagePercentage of OS Disk burst bandwidth credits used so far |
`OS Disk Used Burst BPS Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk Used Burst IO Credits PercentagePercentage of OS Disk burst I/O credits used so far |
`OS Disk Used Burst IO Credits Percentage` |
Percent | Average | `LUN` |
PT1M | Yes |
OS Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for OS disk |
`OS Disk Write Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
OS Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for OS disk |
`OS Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Outbound FlowsOutbound Flows are number of current flows in the outbound direction (traffic going out of the VM) |
`Outbound Flows` |
Count | Average | <none> | PT1M | Yes |
Outbound Flows Maximum Creation RateThe maximum creation rate of outbound flows (traffic going out of the VM) |
`Outbound Flows Maximum Creation Rate` |
CountPerSecond | Average | <none> | PT1M | Yes |
Percentage CPUThe percentage of allocated compute units that are currently in use by the Virtual Machine(s) |
`Percentage CPU` |
Percent | Average | <none> | PT1M | Yes |
Premium Data Disk Cache Read HitPremium Data Disk Cache Read Hit |
`Premium Data Disk Cache Read Hit` |
Percent | Average | `LUN` |
PT1M | Yes |
Premium Data Disk Cache Read MissPremium Data Disk Cache Read Miss |
`Premium Data Disk Cache Read Miss` |
Percent | Average | `LUN` |
PT1M | Yes |
Premium OS Disk Cache Read HitPremium OS Disk Cache Read Hit |
`Premium OS Disk Cache Read Hit` |
Percent | Average | <none> | PT1M | Yes |
Premium OS Disk Cache Read MissPremium OS Disk Cache Read Miss |
`Premium OS Disk Cache Read Miss` |
Percent | Average | <none> | PT1M | Yes |
Temp Disk Latency (Preview)Average time to complete each IO during monitoring period for Temp Disk. Values are in milliseconds. |
`Temp Disk Latency` |
Milliseconds | Average | <none> | PT1M | Yes |
Temp Disk Queue DepthTemp Disk Queue Depth(or Queue Length). |
`Temp Disk Queue Depth` |
Count | Average | <none> | PT1M | Yes |
Temp Disk Read Bytes/SecBytes/Sec read from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Read Operations/SecRead IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Read Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Write Bytes/SecBytes/Sec written to a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Bytes/sec` |
BytesPerSecond | Average | <none> | PT1M | Yes |
Temp Disk Write Operations/SecWrite IOPS from a single disk during monitoring period for Temp Disk. |
`Temp Disk Write Operations/Sec` |
CountPerSecond | Average | <none> | PT1M | Yes |
VM Cached Bandwidth Consumed PercentagePercentage of cached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached Bandwidth Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Cached IOPS Consumed PercentagePercentage of cached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Cached IOPS Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Cached Used Burst BPS Credits PercentagePercentage of Cached Burst BPS Credits used by the VM. |
`VM Local Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Cached Used Burst IO Credits PercentagePercentage of Cached Burst IO Credits used by the VM. |
`VM Local Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Used Burst BPS Credits PercentagePercentage of Uncached Burst BPS Credits used by the VM. |
`VM Remote Used Burst BPS Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Used Burst IO Credits PercentagePercentage of Uncached Burst IO Credits used by the VM. |
`VM Remote Used Burst IO Credits Percentage` |
Percent | Average, Minimum, Maximum | <none> | PT1M | Yes |
VM Uncached Bandwidth Consumed PercentagePercentage of uncached disk bandwidth consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached Bandwidth Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Uncached IOPS Consumed PercentagePercentage of uncached disk IOPS consumed by the VM. Only available on VM series that support premium storage. |
`VM Uncached IOPS Consumed Percentage` |
Percent | Average | <none> | PT1M | Yes |
VM Availability Metric (Preview)Measure of Availability of Virtual machines over time. |
`VmAvailabilityMetric` |
Count | Average, Minimum, Maximum | <none> | PT1M | Yes |

## Minimal ingestion profile for control plane Metrics in Managed Prometheus

Azure Monitor metrics addon collects many Prometheus metrics by default. `Minimal ingestion profile`

is a setting that helps reduce ingestion volume of metrics, as only metrics used by default dashboards, default recording rules and default alerts are collected. This section describes how this setting is configured specifically for control plane metrics. This section also lists metrics collected by default when `minimal ingestion profile`

is enabled.

Note

For addon based collection, `Minimal ingestion profile`

setting is enabled by default. The discussion here is focused on control plane metrics. The current set of default targets and metrics is listed [here](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal).

Following targets are **enabled/ON** by default - meaning you don't have to provide any scrape job configuration for scraping these targets, as metrics addon scrapes these targets automatically by default:

`controlplane-apiserver`

(job=`controlplane-apiserver`

)`controlplane-etcd`

(job=`controlplane-etcd`

)

Following targets are available to scrape, but scraping isn't enabled (**disabled/OFF**) by default. Meaning you don't have to provide any scrape job configuration for scraping these targets, and you need to turn **ON/enable** scraping for these targets using the [ama-metrics-settings-configmap](https://github.com/Azure/prometheus-collector/blob/89e865a73601c0798410016e9beb323f1ecba335/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) under the `default-scrape-settings-enabled`

section.

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`


Note

The default scrape frequency for all default targets and scrapes is `30 seconds`

. You can override it for each target using the [ama-metrics-settings-configmap](https://github.com/Azure/prometheus-collector/blob/89e865a73601c0798410016e9beb323f1ecba335/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) under `default-targets-scrape-interval-settings`

section.

### Minimal ingestion for default ON targets

The following metrics are allow-listed with `minimalingestionprofile=true`

for default **ON** targets. The below metrics are collected by default, as these targets are scraped by default.

controlplane-apiserver:

`apiserver_request_total`

`apiserver_cache_list_fetched_objects_total`

`apiserver_cache_list_returned_objects_total`

`apiserver_flowcontrol_demand_seats_average`

`apiserver_flowcontrol_current_limit_seats`

`apiserver_request_sli_duration_seconds_bucket`

`apiserver_request_sli_duration_seconds_sum`

`apiserver_request_sli_duration_seconds_count`

`process_start_time_seconds`

`apiserver_request_duration_seconds_bucket`

`apiserver_request_duration_seconds_sum`

`apiserver_request_duration_seconds_count`

`apiserver_storage_list_fetched_objects_total`

`apiserver_storage_list_returned_objects_total`

`apiserver_current_inflight_requests`


Note

`apiserver_request_sli_duration_seconds_bucket`

and `apiserver_request_duration_seconds_bucket`

are not collected now with a recent release. These are high cardinality metrics which may increase the number of metrics stored based on the number of custom resources in the cluster. If you would like to collect these bucket metrics, you can add it to the keep list. We highly recommend not turning off the minimal ingestion profile for the control plane components

controlplane-etcd:

`etcd_server_has_leader`

`rest_client_requests_total`

`etcd_mvcc_db_total_size_in_bytes`

`etcd_mvcc_db_total_size_in_use_in_bytes`

`etcd_server_slow_read_indexes_total`

`etcd_server_slow_apply_total`

`etcd_network_client_grpc_sent_bytes_total`

`etcd_server_heartbeat_send_failures_total`


### Minimal ingestion for default OFF targets

The following are metrics that are allow-listed with `minimalingestionprofile=true`

for default **OFF** targets. These metrics aren't collected by default. You can turn **ON** scraping for these targets using `default-scrape-settings-enabled.<target-name>=true`

using the [ama-metrics-settings-configmap](https://github.com/Azure/prometheus-collector/blob/89e865a73601c0798410016e9beb323f1ecba335/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) under the `default-scrape-settings-enabled`

section.

controlplane-kube-controller-manager:

`workqueue_depth`

`rest_client_requests_total`

`rest_client_request_duration_seconds`


controlplane-kube-scheduler:

`scheduler_pending_pods`

`scheduler_unschedulable_pods`

`scheduler_queue_incoming_pods_total`

`scheduler_schedule_attempts_total`

`scheduler_preemption_attempts_total`


controlplane-cluster-autoscaler:

`rest_client_requests_total`

`cluster_autoscaler_last_activity`

`cluster_autoscaler_cluster_safe_to_autoscale`

`cluster_autoscaler_failed_scale_ups_total`

`cluster_autoscaler_scale_down_in_cooldown`

`cluster_autoscaler_scaled_up_nodes_total`

`cluster_autoscaler_unneeded_nodes_count`

`cluster_autoscaler_unschedulable_pods_count`

`cluster_autoscaler_nodes_count`

`cloudprovider_azure_api_request_errors`

`cloudprovider_azure_api_request_duration_seconds_bucket`

`cloudprovider_azure_api_request_duration_seconds_count`


controlplane-node-auto-provisioning:

`karpenter_pods_state`

`karpenter_nodes_created_total`

`karpenter_nodes_terminated_total`

`karpenter_nodeclaims_disrupted_total`

`karpenter_voluntary_disruption_eligible_nodes`

`karpenter_voluntary_disruption_decisions_total`


Note

The CPU and memory usage metrics for all control-plane targets are not exposed irrespective of the profile.

## Metric dimensions

For information about what metric dimensions are, see [Multi-dimensional metrics](/en-us/azure/azure-monitor/platform/data-platform-metrics#multi-dimensional-metrics).

This service has the following dimensions associated with its metrics.

| Dimension Name | Description |
|---|---|
| requestKind | Used by metrics such as Inflight Requests to split by type of request. |
| condition | Used by metrics such as Statuses for various node conditions, Number of pods in Ready state to split by condition type. |
| status | Used by metrics such as Statuses for various node conditions to split by status of the condition. |
| status2 | Used by metrics such as Statuses for various node conditions to split by status of the condition. |
| node | Used by metrics such as CPU Usage Millicores to split by the name of the node. |
| phase | Used by metrics such as Number of pods by phase to split by the phase of the pod. |
| namespace | Used by metrics such as Number of pods by phase to split by the namespace of the pod. |
| pod | Used by metrics such as Number of pods by phase to split by the name of the pod. |
| nodepool | Used by metrics such as Disk Used Bytes to split by the name of the nodepool. |
| device | Used by metrics such as Disk Used Bytes to split by the name of the device. |
| 3gppGen | Used by metrics such as Number of Active PDU Sessions. |
| Cause | Used by metrics such as User plane packet drop rate. |
| Direction | Used by metrics such as User plane bandwidth. |
| Dnn | Used by metrics such as PDU session establishment attempts rate. |
| Interface | Used by metrics such as User plane bandwidth. |
| LUN | Used by metrics such as Percentage of data disk bandwidth consumed. |
| PccpId | Used by metrics such as Number of Active PDU Sessions. |
| Result | Used by metrics such as Authentication failure rate. |
| SiteId | Used by metrics such as Number of Active PDU Sessions. |
| Tai | Used by metrics such as Service request failure rate. |
| VMName | Used by metrics such as Amount of physical memory. |

## Resource logs

This section lists the types of resource logs you can collect for this service. The section pulls from the list of [all resource logs category types supported in Azure Monitor](/en-us/azure/azure-monitor/platform/resource-logs-schema).

### Supported resource logs for Microsoft.ContainerService/fleets

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`cloud-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`fleet-hub-agent`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`fleet-hub-net-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`guard`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-apiserver`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-audit`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-audit-admin`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-scheduler`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)### Supported resource logs for Microsoft.ContainerService/managedClusters

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`cloud-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`cluster-autoscaler`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`csi-azuredisk-controller`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`csi-azurefile-controller`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`csi-snapshot-controller`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`fleet-mcs-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`fleet-member-agent`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`fleet-member-net-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`guard`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`karpenter-events`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-apiserver`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-audit`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-audit-admin`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-controller-manager`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)`kube-scheduler`

[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics)Logs from multiple Azure resources.

[Queries](/en-us/azure/azure-monitor/reference/queries/azurediagnostics#queries-for-microsoftcontainerservice)### Supported resource logs for microsoft.kubernetes/connectedClusters

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`cloud-controller-manager`

`cluster-autoscaler`

`csi-aksarcdisk-controller`

`csi-aksarcnfs-controller`

`csi-aksarcsmb-controller`

`guard`

`kube-apiserver`

[ArcK8sControlPlane](/en-us/azure/azure-monitor/reference/tables/arck8scontrolplane)Contains diagnostic logs for the Kubernetes API Server, Controller Manager, Scheduler, Cluster Autoscaler, Cloud Controller Manager, Guard, and the Azure CSI storage drivers. These diagnostic logs have distinct Category entries corresponding their diagnostic log setting (e.g. kube-apiserver, kube-audit-admin). Requires Diagnostic Settings to use the Resource Specific destination table.

`kube-audit`

[ArcK8sAudit](/en-us/azure/azure-monitor/reference/tables/arck8saudit)Contains all Kubernetes API Server audit logs including events with the get and list verbs. These events are useful for monitoring all of the interactions with the Kubernetes API. To limit the scope to modifying operations see the ArcK8sAuditAdmin table. Requires Diagnostic Settings to use the Resource Specific destination table.

`kube-audit-admin`

[ArcK8sAuditAdmin](/en-us/azure/azure-monitor/reference/tables/arck8sauditadmin)Contains Kubernetes API Server audit logs excluding events with the get and list verbs. These events are useful for monitoring resource modification requests made to the Kubernetes API. To see all modifying and non-modifying operations see the ArcK8sAudit table. Requires Diagnostic Settings to use the Resource Specific destination table.

`kube-controller-manager`

`kube-scheduler`

### Supported resource logs for Microsoft.Compute/virtualMachines

| Category | Category display name | Log table |
|
|---|

[Supports ingestion-time transformation](/en-us/azure/azure-monitor/essentials/data-collection-transformations)

`SoftwareUpdateProfile`

`SoftwareUpdates`

## Azure Monitor Logs tables

This section lists the Azure Monitor Logs tables relevant to this service, which are available for query by Log Analytics using Kusto queries. The tables contain resource log data and possibly more depending on what is collected and routed to them.

### AKS Microsoft.ContainerService/managedClusters

[AzureActivity](/en-us/azure/azure-monitor/reference/tables/azureactivity#columns)[AzureDiagnostics](/en-us/azure/azure-monitor/reference/tables/azurediagnostics#columns)[AzureMetrics](/en-us/azure/azure-monitor/reference/tables/azuremetrics#columns)[ContainerImageInventory](/en-us/azure/azure-monitor/reference/tables/containerimageinventory#columns)[ContainerInventory](/en-us/azure/azure-monitor/reference/tables/containerinventory#columns)[ContainerLog](/en-us/azure/azure-monitor/reference/tables/containerlog#columns)[ContainerLogV2](/en-us/azure/azure-monitor/reference/tables/containerlogv2#columns)[ContainerNodeInventory](/en-us/azure/azure-monitor/reference/tables/containernodeinventory#columns)[ContainerServiceLog](/en-us/azure/azure-monitor/reference/tables/containerservicelog#columns)[Heartbeat](/en-us/azure/azure-monitor/reference/tables/heartbeat#columns)[InsightsMetrics](/en-us/azure/azure-monitor/reference/tables/insightsmetrics#columns)[KubeEvents](/en-us/azure/azure-monitor/reference/tables/kubeevents#columns)[KubeMonAgentEvents](/en-us/azure/azure-monitor/reference/tables/kubemonagentevents#columns)[KubeNodeInventory](/en-us/azure/azure-monitor/reference/tables/kubenodeinventory#columns)[KubePodInventory](/en-us/azure/azure-monitor/reference/tables/kubepodinventory#columns)[KubePVInventory](/en-us/azure/azure-monitor/reference/tables/kubepvinventory#columns)[KubeServices](/en-us/azure/azure-monitor/reference/tables/kubeservices#columns)[Perf](/en-us/azure/azure-monitor/reference/tables/perf#columns)[Syslog](/en-us/azure/azure-monitor/reference/tables/syslog#columns)[AKSAudit](/en-us/azure/azure-monitor/reference/tables/aksaudit#columns)[AKSAuditAdmin](/en-us/azure/azure-monitor/reference/tables/aksauditAdmin#columns)[AKSControlPlane](/en-us/azure/azure-monitor/reference/tables/akscontrolplane#columns)

## Activity log

The linked table lists the operations that can be recorded in the activity log for this service. These operations are a subset of [all the possible resource provider operations in the activity log](/en-us/azure/role-based-access-control/resource-provider-operations).

For more information on the schema of activity log entries, see [Activity Log schema](/en-us/azure/azure-monitor/essentials/activity-log-schema).

The following table lists a few example operations related to AKS that might be created in the Activity log. Use the Activity log to track information such as when a cluster is created or had its configuration change. You can view this information in the portal or by using [other methods](/en-us/azure/azure-monitor/essentials/activity-log#other-methods-to-retrieve-activity-log-events). You can also use it to create an Activity log alert to be proactively notified when an event occurs.

| Operation | Description |
|---|---|
| Microsoft.ContainerService/managedClusters/write | Create or update managed cluster |
| Microsoft.ContainerService/managedClusters/delete | Delete Managed Cluster |
| Microsoft.ContainerService/managedClusters/listClusterMonitoringUserCredential/action | List clusterMonitoringUser credential |
| Microsoft.ContainerService/managedClusters/listClusterAdminCredential/action | List clusterAdmin credential |
| Microsoft.ContainerService/managedClusters/agentpools/write | Create or Update Agent Pool |

## Related content

- See
[Monitor Azure Kubernetes Service](monitor-aks)for a description of monitoring AKS. - See
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)for details on monitoring Azure resources.