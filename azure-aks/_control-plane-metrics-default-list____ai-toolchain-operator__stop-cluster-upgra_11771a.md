---
merged_at: 2026-01-26T20:54:26.160376
merged_files: 2
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/control-plane-metrics-default-list -->

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

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __ai-toolchain-operator__stop-cluster-upgrade-api-breaking-changes_upgrade-aks-i_e82720.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _ai-toolchain-operator__stop-cluster-upgrade-api-breaking-changes_upgrade-aks-ip_d83ddb.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ai-toolchain-operator.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator -->

# Deploy an AI model on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use the AI toolchain operator add-on to efficiently self-host large language models on Kubernetes, reducing costs and resource complexity, enhancing customization, and maintaining full control over your data.

## About KAITO

Self-hosting large language models (LLMs) on Kubernetes is gaining momentum among organizations with inference workloads at scale, such as batch processing, chatbots, agents, and AI-driven applications. These organizations often have access to commercial-grade GPUs and are seeking alternatives to costly per-token API pricing models, which can quickly scale out of control. Many also require the ability to fine-tune or customize their models, a capability typically restricted by closed-source API providers. Additionally, companies handling sensitive or proprietary data - especially in regulated sectors such as finance, healthcare, or defense - prioritize self-hosting to maintain strict control over data and prevent exposure through third-party systems.

To address these needs and more, the [Kubernetes AI Toolchain Operator (KAITO)](https://github.com/kaito-project/kaito), a Cloud Native Computing Foundation (CNCF) Sandbox project, simplifies the process of deploying and managing open-source LLM workloads on Kubernetes. KAITO integrates with vLLM, a high-throughput inference engine designed to serve large language models efficiently. vLLM as an inference engine helps reduce memory and GPU requirements without significantly compromising accuracy.

Built on top of the open-source KAITO project, the AI toolchain operator managed add-on offers a modular, plug-and-play setup that allows teams to quickly deploy models and expose them via production-ready APIs. It includes built-in features like OpenAI-compatible APIs, prompt formatting, and streaming response support. When deployed on an AKS cluster, KAITO ensures data stays within your organization’s controlled environment, providing a secure, compliant alternative to cloud-hosted LLM APIs.

## Before you begin

- This article assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for AKS](concepts-clusters-workloads). - For
and default resource configuration, see the**all hosted model preset images**[KAITO GitHub repository](https://github.com/kaito-project/kaito/tree/main/presets). - The AI toolchain operator add-on currently supports KAITO
**version 0.6.0**, please make a note of this in considering your choice of model from the KAITO model repository.

## Limitations

`AzureLinux`

and`Windows`

OS SKU are not currently supported.- AMD GPU VM sizes are not supported
`instanceType`

in a KAITO workspace. - AI toolchain operator add-on is supported in
**public**Azure regions.

## Prerequisites

If you don't have an Azure subscription, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.If you have multiple Azure subscriptions, make sure you select the correct subscription in which the resources will be created and charged using the

[az account set](/en-us/cli/azure/account#az-account-set)command.Note

Your Azure subscription must have GPU VM quota recommended for your model deployment in the same Azure region as your AKS resources.


Azure CLI version 2.76.0 or later installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The Kubernetes command-line client, kubectl, installed and configured. For more information, see

[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/).

### Export environment variables

To simplify the configuration steps in this article, you can define environment variables using the following commands. Make sure to replace the placeholder values with your own.

`export AZURE_SUBSCRIPTION_ID="mySubscriptionID" export AZURE_RESOURCE_GROUP="myResourceGroup" export AZURE_LOCATION="myLocation" export CLUSTER_NAME="myClusterName"`


## Enable the AI toolchain operator add-on on an AKS cluster

The following sections describe how to create an AKS cluster with the AI toolchain operator add-on enabled and deploy a default hosted AI model.

### Create an AKS cluster with the AI toolchain operator add-on enabled

Create an Azure resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command.`az group create --name $AZURE_RESOURCE_GROUP --location $AZURE_LOCATION`

Create an AKS cluster with the AI toolchain operator add-on enabled using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command with the`--enable-ai-toolchain-operator`

and`--enable-oidc-issuer`

flags.`az aks create --location $AZURE_LOCATION \ --resource-group $AZURE_RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-ai-toolchain-operator \ --enable-oidc-issuer \ --generate-ssh-keys`

On an existing AKS cluster, you can enable the AI toolchain operator add-on using the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command.`az aks update --name $CLUSTER_NAME \ --resource-group $AZURE_RESOURCE_GROUP \ --enable-ai-toolchain-operator \ --enable-oidc-issuer`


## Connect to your cluster

Configure

`kubectl`

to connect to your cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command.`az aks get-credentials --resource-group $AZURE_RESOURCE_GROUP --name $CLUSTER_NAME`

Verify the connection to your cluster using the

`kubectl get`

command.`kubectl get nodes`


## Deploy a default hosted AI model

KAITO offers a range of small to large language models hosted as public container images, which can be deployed in one step using a KAITO workspace. You can browse the preset LLM images available in the [KAITO model registry](https://github.com/kaito-project/kaito/tree/main/presets). In this section, we'll use the high-performant multimodal [Microsoft Phi-4-mini](https://techcommunity.microsoft.com/blog/educatordeveloperblog/welcome-to-the-new-phi-4-models---microsoft-phi-4-mini--phi-4-multimodal/4386037) language model as an example:

Deploy the

[Phi-4-mini instruct](https://huggingface.co/microsoft/Phi-4-mini-instruct)model preset for inference from the KAITO model repository using the`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/kaito-project/kaito/refs/heads/main/examples/inference/kaito_workspace_phi_4_mini.yaml`

Track the live resource changes in your workspace using the

`kubectl get`

command.`kubectl get workspace workspace-phi-4-mini -w`

Note

As you track the KAITO workspace deployment, note that machine readiness can take up to 10 minutes, and workspace readiness up to 20 minutes depending on the size of your model.

Check your inference service and get the service IP address using the

`kubectl get svc`

command.`export SERVICE_IP=$(kubectl get svc workspace-phi-4-mini -o jsonpath='{.spec.clusterIP}')`

Test the Phi-4-mini instruct inference service with a sample input of your choice using the

[OpenAI chat completions API format](https://platform.openai.com/docs/api-reference/chat):`kubectl run -it --rm --restart=Never curl --image=curlimages/curl -- curl -X POST http://$SERVICE_IP/v1/completions -H "Content-Type: application/json" \ -d '{ "model": "phi-4-mini-instruct", "prompt": "How should I dress for the weather today?", "max_tokens": 10 }'`


## Deploy a custom or domain-specific LLM

Open-source LLMs are often trained in different contexts and domains, and the hosted model presets may not always fit the requirements of your application or data. In this case, KAITO also supports inference deployment of newer or domain-specific language models from [HuggingFace](https://huggingface.co/). Try out a custom model inference deployment with KAITO by following [this article](kaito-custom-inference-model).

## Clean up resources

If you no longer need these resources, you can delete them to avoid incurring extra Azure compute charges.

Delete the KAITO workspace using the

`kubectl delete workspace`

command.`kubectl delete workspace workspace-phi-4-mini`

You need to manually delete the GPU node pools provisioned by the KAITO deployment. Use the node label created by

[Phi-4-mini instruct workspace](https://raw.githubusercontent.com/kaito-project/kaito/refs/heads/main/examples/inference/kaito_workspace_phi_4_mini.yaml)to get the node pool name using thecommand. In this example, the node label is "kaito.sh/workspace": "workspace-phi-4-mini".`az aks nodepool list`

`az aks nodepool list --resource-group $AZURE_RESOURCE_GROUP --cluster-name $CLUSTER_NAME`

[Delete the node pool](delete-node-pool)with this name from your AKS cluster and repeat the steps in this section for each KAITO workspace that will be removed.

## Common troubleshooting scenarios

After applying the KAITO model inference workspace, your resource readiness and workspace conditions might not update to `True`

for the following reasons:

- Your Azure subscription doesn't have quota for the minimum GPU instance type specified in your KAITO workspace. You'll need to
[request a quota increase](/en-us/azure/quotas/quickstart-increase-quota-portal)for the GPU VM family in your Azure subscription. - The GPU instance type isn't available in your AKS region. Confirm the
[GPU instance availability in your specific region](https://azure.microsoft.com/explore/global-infrastructure/products-by-region/?regions=&products=virtual-machines)and switch the Azure region if your GPU VM family isn't available.

## Next steps

Learn more about KAITO model deployment options below:

- Deploy LLMs with your application on AKS using
[KAITO in Visual Studio Code](aks-extension-kaito). [Monitor your KAITO inference workload](ai-toolchain-operator-monitoring).[Fine tune a model](ai-toolchain-operator-fine-tune)with the AI toolchain operator add-on on AKS.- Configure and test
[tool calling with KAITO inference](ai-toolchain-operator-tool-calling). - Integrate an
[MCP server with the AI toolchain operator](ai-toolchain-operator-mcp)add-on on AKS.


---

<!-- DOCUMENTO FUSIONADO: _stop-cluster-upgrade-api-breaking-changes_upgrade-aks-ipam-and-dataplane.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: stop-cluster-upgrade-api-breaking-changes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/stop-cluster-upgrade-api-breaking-changes -->

# Stop Azure Kubernetes Service (AKS) cluster upgrades automatically on API breaking changes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to stop Azure Kubernetes Service (AKS) cluster upgrades automatically on API breaking changes.

## Overview

To stay within a supported Kubernetes version, you have to upgrade your cluster at least once per year and prepare for all possible disruptions. These disruptions include ones caused by API breaking changes, deprecations, and dependencies such as Helm and Container Storage Interface (CSI). It can be difficult to anticipate these disruptions and migrate critical workloads without experiencing any downtime.

You can configure your AKS cluster to automatically stop upgrade operations consisting of a minor version change with deprecated APIs and alert you to the issue. This feature helps you avoid unexpected disruptions and gives you time to address the deprecated APIs before proceeding with the upgrade.

## Before you begin

Before you begin, make sure you meet the following prerequisites:

- The upgrade operation is a Kubernetes minor version change for the cluster control plane.
- The Kubernetes version you're upgrading to is 1.26 or later.
- The last seen usage of deprecated APIs for the targeted version you're upgrading to must occur within 12 hours before the upgrade operation. AKS records usage hourly, so any usage of deprecated APIs within one hour isn't guaranteed to appear in the detection.

## Mitigate stopped upgrade operations

If you meet the [prerequisites](#before-you-begin), attempt an upgrade, and receive an error message similar to the following example error message:

```
Bad Request({
"code": "ValidationError",
"message": "Control Plane upgrade is blocked due to recent usage of a Kubernetes API deprecated in the specified version. Please refer to https://kubernetes.io/docs/reference/using-api/deprecation-guide to migrate the usage. To bypass this error, set enable-force-upgrade in upgradeSettings.overrideSettings. Bypassing this error without migrating usage will result in the deprecated Kubernetes API calls failing. Usage details: 1 error occurred:\n\t* usage has been detected on API flowcontrol.apiserver.k8s.io.prioritylevelconfigurations.v1beta1, and was recently seen at: 2023-03-23 20:57:18 +0000 UTC, which will be removed in 1.26\n\n",
"subcode": "UpgradeBlockedOnDeprecatedAPIUsage"
})
```


You have two options to mitigate the issue: you can [remove usage of deprecated APIs (recommended)](#remove-usage-of-deprecated-apis-recommended) or [bypass validation to ignore API changes](#bypass-validation-to-ignore-api-changes).

### Remove usage of deprecated APIs (recommended)

In the Azure portal, navigate to your cluster resource and select

**Diagnose and solve problems**Select

**Create, Upgrade, Delete, and Scale**>**Kubernetes API deprecations**.Wait 12 hours from the time the last deprecated API usage was seen. Read-Only verbs are excluded from the deprecated api usage namely

[Get/List/Watch](https://kubernetes.io/docs/reference/using-api/api-concepts/).(You can also check past API usage by enabling[Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-query#resource-logs)and exploring kube audit logs.)Retry your cluster upgrade.


### Bypass validation to ignore API changes

Note

This method requires you to use the Azure CLI version 2.57 or later. If you have the preview CLI extension installed, you need to update to version `3.0.0b10`

or later. This method isn't recommended, as deprecated APIs in the targeted Kubernetes version might not work long term. We recommend removing them as soon as possible after the upgrade completes.

Bypass validation to ignore API breaking changes and invoke an upgrade. Specify the

`enable-force-upgrade`

flag and set the`upgrade-override-until`

property to define the end of the window during which validation is bypassed. If no value is set, it defaults the window to three days from the current time. The date and time you specify must be in the future.`az aks upgrade --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --kubernetes-version $KUBERNETES_VERSION --enable-force-upgrade --upgrade-override-until 2023-10-01T13:00:00Z`

Note

`Z`

is the zone designator for the zero UTC/GMT offset, also known as 'Zulu' time. This example sets the end of the window to`13:00:00`

GMT. For more information, see[Combined date and time representations](https://wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).

## Next steps

This article showed you how to stop AKS cluster upgrades automatically on API breaking changes. To learn more about more upgrade options for AKS clusters, see [Upgrade options for Azure Kubernetes Service (AKS) clusters](upgrade-cluster).


---

<!-- DOCUMENTO FUSIONADO: upgrade-aks-ipam-and-dataplane.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-ipam-and-dataplane -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```


---

<!-- DOCUMENTO FUSIONADO: _migrate-from-npm-to-cilium-network-policy__use-byo-cni_gpu-health-monitoring.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: migrate-from-npm-to-cilium-network-policy.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/migrate-from-npm-to-cilium-network-policy -->

# Migrate from Network Policy Manager (NPM) to Cilium Network Policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, we provide a comprehensive guide to plan, execute, and validate the migration from Network Policy Manager (NPM) to Cilium Network Policy. The goal is to ensure policy parity, minimize service disruption, and align with Azure CNI's strategic direction toward eBPF-based networking and enhanced observability.

Important

This guide applies exclusively to AKS clusters running Linux nodes. Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Key considerations before you begin

- Policy Compatibility: NPM and Cilium differ in enforcement models. Before migration you need to validate that existing policies are compatible or identify required changes. Refer to the Pre-Migration Validation section for guidance.
- Downtime Expectations: Policy enforcement might be temporarily inconsistent during node reimaging.
- Windows Node Pools: Cilium Network Policy isn't currently supported for Windows nodes in AKS.

## Pre-migration validation

Before migrating from Network Policy Manager (NPM) to Cilium Network Policy, it's important to assess the compatibility of your existing network policies. While most policies continue to function as expected post-migration, there are specific scenarios where behavior might differ between NPM and Cilium. These differences could require updates to your policies either before or after the migration to ensure consistent enforcement and avoid unintended traffic drops. In this section, we outline known scenarios where policy adjustments might be necessary. We explain why it matters, and provide guidance on what actions—if any—are required to make your policies Cilium-compatible.

### NetworkPolicy with endPort

Note

Cilium started supporting the `endPort`

field in Kubernetes NetworkPolicy in version 1.17.

The endPort field allows you to define a range of ports in a single rule, rather than specifying individual ports.

Here's an example of a Kubernetes NetworkPolicy that uses the endPort field:

```
egress:
- to:
- ipBlock:
cidr: 10.0.0.0/24
ports:
- protocol: TCP
port: 32000
endPort: 32768
```


**Action Required:**

- If your AKS cluster is running Cilium version 1.17 or later, no changes are needed as endPort is fully supported.
- If your cluster is running a Cilium version earlier than 1.17, remove the endPort field from any policies before migrating. Use explicit single-port entries instead.

### NetworkPolicy with ipBlock

The ipBlock field in Kubernetes NetworkPolicy allows you to define CIDR ranges for ingress sources or egress destinations. These ranges can include external IPs, Pod IPs, or Node IPs. However, Cilium doesn't allow egress to Pod or Node IPs using ipBlock, even if those IPs fall within the specified CIDR range.

For example, the following NetworkPolicy uses an ipBlock to allow all egress traffic to 0.0.0.0/0:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
```


- Under NPM, this policy would allow egress to all destinations, including Pods and Nodes.
- After migrating to Cilium, egress to Pod and Node IPs will be blocked, even though they fall within the 0.0.0.0/0 range.

**Action Required:**

- To allow traffic to Pod IPs, before migration replace the ipBlock with a combination of namespaceSelector and podSelector.

Here's an example of using namespaceSelector and podSelector:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: example-ipblock
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 0.0.0.0/0
- namespaceSelector: {}
- podSelector: {}
```


- For Node IPs, there's no pre-migration workaround. After migration, you must create a CiliumNetworkPolicy that explicitly allows egress to the host and/or remote-node entities. Until this policy is in place, egress traffic to Node IPs is blocked.

Here's an example of CiliumNetworkPolicy to allow traffic from/to local and remote nodes:

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: allow-node-egress
namespace: ipblock-test
spec:
endpointSelector: {} # Applies to all pods in the namespace
egress:
- toEntities:
- host # host allows traffic from/to the local node's host network namespace
- remote-node # remote-node allows traffic from/to the remote node's host network namespace
```


### NetworkPolicy with named Ports

Kubernetes NetworkPolicy allows you to reference ports by name instead of number. If you're using named ports in your NetworkPolicies, Cilium might fail to enforce rules correctly and lead to unexpected traffic being blocked. This issue happens when the same port name is used for different ports.
For more information, see [Cilium GitHub issue #30003](https://github.com/cilium/cilium/issues/30003).

Here's an example of NetworkPolicy uses Named port to allow egress traffic:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
annotations:
name: allow-egress
namespace: default
spec:
podSelector:
matchLabels:
network-rules-egress: cilium-np-test
egress:
- ports:
- port: http-test # Named port
protocol: TCP
policyTypes:
- Egress
```


**Action Required:**

- Before migration, replace all named ports in your policies with their corresponding numeric values.

### NetworkPolicy with Egress Policies

Kubernetes NetworkPolicy on NPM doesn't block egress traffic from a pod to its own node's IP, this traffic is implicitly allowed. After you migrate to Cilium, this behavior will change, and traffic to local nodes that was previously allowed will be blocked unless explicitly allowed.

For example, the following policy allows egress only to an internal API subnet:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: allow-egress
namespace: default
spec:
podSelector: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.20.30.0/24
```


- With NPM: Egress traffic to 10.20.30.0/24 is allowed explicitly, and egress traffic to the local node is allowed implicitly.
- With Cilium: Only traffic to 10.20.30.0/24 is allowed; egress to the node IP is blocked unless you permit it explicitly.

**Action Required:**

- Review all existing egress policies for your workloads.
- If your applications rely on NPM's implicit allow behavior for egress to the local node, you must add explicit egress rules to maintain connectivity after migration.
- You can add a CiliumNetworkPolicy after migration to explicitly allow egress traffic to the local host.

### Ingress policy behavior changes

Under Network Policy Manager (NPM), ingress traffic arriving via a LoadBalancer or NodePort service with "externalTrafficPolicy=Cluster" - which is the default setting - isn't subject to ingress policy enforcement. This behavior means that even if a pod has a restrictive ingress policy, traffic from external sources might still reach it via loadbalancer or nodeport services.

In contrast, Cilium enforces ingress policies on all traffic, including traffic routed internally due to externalTrafficPolicy=Cluster. As a result, after migration, traffic that was previously allowed might be dropped if the appropriate ingress rules aren't explicitly defined.

For example, Customer creates a network policy to deny all in ingress traffic

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: default-deny-ingress
spec:
podSelector: {}
policyTypes:
- Ingress
```


- With NPM: Direct connection to the pod or via ClusterIP service is blocked. However, access through NodePort or LoadBalancer is still allowed despite the deny-all policy.
- With Cilium: All ingress traffic is blocked, including traffic via NodePort or LoadBalancer, unless explicitly allowed.

**Action Required:**

- Review all ingress policies for workloads behind LoadBalancer or NodePort services using externalTrafficPolicy=Cluster.
- Ensure that ingress rules explicitly allow traffic from the expected external sources (for example, IP ranges, namespaces, or labels).
- If your policy currently relies on the implicit allow behavior under NPM, you must add explicit ingress rules to maintain connectivity after migration.

## Upgrade to Azure CNI Powered by Cilium

To use Cilium Network Policy, your AKS cluster must be running Azure CNI powered by Cilium. When you enable Cilium in a cluster currently using NPM, the existing NPM engine is automatically uninstalled and replaced with Cilium.

Warning

The upgrade process triggers each node pool to be reimaged simultaneously. Upgrading each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image upgrade or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium will begin enforcing network policies only after all nodes are reimaged.

Important

These instructions apply to clusters upgrading from Azure CNI to Azure CNI with the Cilium dataplane. Upgrades from bring-your-own CNIs or changes the IPAM mode aren't covered here. For more information, see [Upgrade Azure CNI documentation](update-azure-cni).

To perform the upgrade, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Use the following command to upgrade an existing cluster to Azure CNI Powered by Cilium. Replace the values for `clusterName`

and `resourceGroupName`

:

```
az aks update --name <clusterName> --resource-group <resourceGroupName> --network-dataplane cilium
```


## Next steps

For more information about using Cilium FQDN network policy on AKS, see

[Set up FQDN filtering feature for Container Network Security in Advanced Container Networking Services](how-to-apply-fqdn-filtering-policies).For more information about using Cilium L7 network policy on AKS, see

[Set up Layer 7(L7) policies with Advanced Container Networking Services](how-to-apply-l7-policies).For more information about network policy best practices on aks, see

[Best practices for network policies in Azure Kubernetes Service (AKS)](network-policy-best-practices)


---

<!-- DOCUMENTO FUSIONADO: _use-byo-cni_gpu-health-monitoring.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-byo-cni.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-byo-cni -->

# Bring your own CNI plugin with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes doesn't provide a network interface system by default. Instead, [network plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/) provide this functionality. Azure Kubernetes Service (AKS) provides several supported Container Network Interface (CNI) plugins. For information on supported plugins, see [Networking concepts for applications in Azure Kubernetes Service](concepts-network).

The supported plugins meet most networking needs in Kubernetes. However, advanced AKS users might want the same CNI plugin that they used in on-premises Kubernetes environments. Or these users might want to use advanced functionalities available in other CNI plugins.

This article shows how to deploy an AKS cluster with no CNI plugin preinstalled. From there, you can install any CNI plugin that works in Azure.

## Support

Microsoft support can't assist with CNI-related issues in clusters that you deploy by bringing your own CNI plugin. For example, CNI-related issues would cover most east/west (pod to pod) traffic, along with `kubectl proxy`

and similar commands. If you want CNI-related support, use a supported AKS network plugin or seek support from the CNI plugin vendor.

Microsoft still provides support for issues that aren't related to CNI.

## Prerequisites

- For Azure Resource Manager or Bicep, use at least template version 2022-01-02-preview or 2022-06-01.
- For the Azure CLI, use at least version 2.39.0.
- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the address range for the Kubernetes service, pods, or cluster virtual network. - The cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet or modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node's Classless Inter-Domain Routing (CIDR) range. For more information, see
[Network security groups](concepts-network#network-security-groups). - AKS doesn't create a route table in the managed virtual network.
- You must specify a Pod CIDR (IP address range for pods). The AKS control plane uses this range for internal traffic routing to pods, even though pod IP assignment will be managed by your custom CNI. If no pod CIDR is provided, control plane to pod communication may fail or be misrouted. You must select a pod CIDR that does not conflict with any other network in your environment and avoids Azure reserved ranges, such as,
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

. For example, you might use a range such as`10.XX.0.0/16`

that is unique to your cluster. This ensures that the control plane can route directly to pod IPs on your nodes, and no IP overlap will occur if you integrate with other networks or clusters.

## Create an AKS cluster with no CNI plugin preinstalled

Create an Azure resource group for your AKS cluster by using the

command.`az group create`

`az group create --location eastus --name myResourceGroup`

Create an AKS cluster by using the

command. Pass the`az aks create`

`--network-plugin`

parameter with the parameter value of`none`

.`az aks create \ --location eastus \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin none \ --pod-cidr "10.10.0.0/16" \ --generate-ssh-keys`


## Deploy a CNI plugin

After AKS provisioning finishes, the cluster is online. But all the nodes are in a `NotReady`

state, as shown in the following example:

```
$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
aks-nodepool1-23902496-vmss000000 NotReady agent 6m9s v1.21.9
$ kubectl get node -o custom-columns='NAME:.metadata.name,STATUS:.status.conditions[?(@.type=="Ready")].message'
NAME STATUS
aks-nodepool1-23902496-vmss000000 container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:Network plugin returns error: cni plugin not initialized
```


At this point, the cluster is ready for installation of a CNI plugin.


---

<!-- DOCUMENTO FUSIONADO: gpu-health-monitoring.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/gpu-health-monitoring -->

# GPU health monitoring in Node Problem Detector (NPD) in Azure Kubernetes Service (AKS) nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how Azure Kubernetes Service (AKS) uses Node Problem Detector (NPD) to monitor the health of GPU-enabled node pools. NPD is a Kubernetes component that detects and reports node-level issues, including hardware faults, driver errors, and connectivity problems that can affect the performance and availability of GPU workloads.

## About GPU health monitoring in NPD

AKS supports GPU health monitoring through [Node Problem Detector (NPD)](node-problem-detector), enabling automatic detection and reporting of issues that affect GPU-enabled node pools on an AKS cluster. GPU health monitoring helps Kubernetes operators keep GPU nodes healthy and performant by surfacing hardware faults, communication failures, and system-level errors. NPD sets GPU-related node conditions and enable platform engineering teams to take action before issues impact application performance or availability.

These health signals are vital for ensuring optimal performance and reliability across a range of GPU workloads, including:

- Machine learning (ML) training and inference.
- AI model development.
- High-performance computing (HPC).
- Graphics rendering and data-intensive simulations.

## Limitations

AKS Node Problem Detector * does not* run GPU health checks on node pools with

`--gpu-driver none`

, where **self-managed**or custom GPU driver was installed on the nodes.

## Supported GPU health checks

NPD regularly monitors GPU-enabled node pools and sets conditions when anomalies are detected. The following GPU health checks are currently supported:

**GPUMissing**: NPD verifies that the number of GPUs detected by the`nvidia-smi`

utility matches the expected GPU count for the VM SKU assigned to the node.- A mismatch might indicate a hardware fault, driver issue, or misconfiguration. Accurate GPU enumeration is critical for ensuring scheduling accuracy and workload availability on GPU nodes.

**GPUXIDErrors**: Checks for XID (eXecution ID) errors emitted by the GPU driver in the kernel logs. XID errors are low-level GPU faults that typically occur when:- The driver misprograms the GPU.
- There's a corruption in the command stream sent to the GPU.
- A hardware failure or instability affects GPU operation.

For more information, see

[XID errors on NVIDIA GPUs](https://docs.nvidia.com/deploy/xid-errors/index.html).**NVLink Status**: For NVIDIA VM SKUs that support NVLink, this condition confirms that NVLink is active and functioning.- NVLink is a high-speed interconnect used to facilitate data transfer between multiple GPUs.
- If NVLink is inactive or degraded, multi-GPU workloads might experience reduced performance or communication bottlenecks.

For more information, see

[NVIDIA NVLink](https://www.nvidia.com/en-us/data-center/nvlink/).**InfiniBand Link Flapping**: NPD monitors for InfiniBand (IB) link flapping, or intermittent connectivity of the IB network device.- Link flapping shouldn't occur under normal operating conditions and might result in degraded inter-node communication for distributed workloads.
- It can also signal physical layer issues, misconfigured firmware, or driver instability.

**NVIDIA GRID Driver License Check**: For NVIDIA VM SKUs that support GRID driver, this condition verifies license status of the installed GRID driver on[supported NVIDIA VM SKUs](/en-us/azure/virtual-machines/sizes/gpu-accelerated/nvadsa10v5-series).- Invalid might indicate the installed GRID driver is not licensed.


## Frequently asked questions

### Does Node Problem Detector (NPD) automatically remediate GPU node issues?

NPD doesn't take direct action to remediate GPU-enabled node issues. NPD detects and reports problems by publishing Kubernetes node conditions and events. Any remediation (for example: draining a node, restarting workloads, or replacing faulty hardware) must be handled manually, through external automation, or alerting systems configured by the Kubernetes operator.

### On which Azure VM sizes does AKS conduct GPU health monitoring through NPD?

Currently, NPD conducts health checks on GPU nodes provisioned with the `Standard_ND96asr_v4`

or `Standard_ND96isr_H100_v5`

VM size on AKS. Also on [A10 SKU](/en-us/azure/virtual-machines/sizes/gpu-accelerated/nvadsa10v5-series) for GRID Driver License checks.

### Does NPD monitor the health of multi-instance GPU (MIG) node pools?

Yes, NPD health monitoring is supported on [MIG-enabled AKS node pools](gpu-multi-instance).

## Next steps

- Provision GPUs on
[Linux](use-nvidia-gpu)or[Windows](use-windows-gpu)node pools in your AKS cluster. - Learn more about the
[types of node conditions and events](node-problem-detector)set by NPD on AKS. [Monitor general GPU metrics](monitor-gpu-metrics)using a self-managed metrics exporter.


---

<!-- DOCUMENTO FUSIONADO: __core-aks-concepts_use-system-pools__cluster-configuration_concepts-clusters-wo_72e13d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _core-aks-concepts_use-system-pools.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: core-aks-concepts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/core-aks-concepts -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## What is Kubernetes?

Kubernetes is an open-source container orchestration platform for automating the deployment, scaling, and management of containerized applications. For more information, see the official [Kubernetes documentation](https://kubernetes.io/docs/home/).

## What is AKS?

AKS is a managed Kubernetes service that simplifies deploying, managing, and scaling containerized applications that use Kubernetes. For more information, see [What is Azure Kubernetes Service (AKS)?](what-is-aks).

## Cluster components

An AKS cluster is divided into two main components:

**Control plane**: The control plane provides the core Kubernetes services and orchestration of application workloads.**Nodes**: Nodes are the underlying virtual machines (VMs) that run your applications.

Note

AKS managed components have the label `kubernetes.azure.com/managedby`

: `aks`

.

AKS manages the Helm releases with the prefix `aks-managed`

. Continuously increasing revisions on these releases are expected and safe.

### Control plane

The Azure managed control plane is composed of several components that help manage the cluster:

| Component | Description |
|---|---|
`kube-apiserver` |
The API server (
|

`etcd`

[etcd](https://kubernetes.io/docs/concepts/overview/components/#etcd)helps to maintain the state of your Kubernetes cluster and configuration.`kube-scheduler`

[kube-scheduler](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler)) helps to make scheduling decisions. It watches for new pods with no assigned node and selects a node for them to run on.`kube-controller-manager`

[kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager)) runs controller processes, such as noticing and responding when nodes go down.`cloud-controller-manager`

[cloud-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager)) embeds cloud-specific control logic to run controllers specific to the cloud provider.### Nodes

Each AKS cluster has at least one node, which is an Azure VM that runs Kubernetes node components. The following components run on each node:

| Component | Description |
|---|---|
`kubelet` |
The
|

`kube-proxy`

[kube-proxy](https://kubernetes.io/docs/concepts/overview/components/#kube-proxy)is a network proxy that maintains network rules on nodes.`container runtime`

[container runtime](https://kubernetes.io/docs/concepts/overview/components/#container-runtime)manages the execution and lifecycle of containers.## Node configuration

Configure the following settings for nodes.

### VM size and image

The *Azure VM size* for your nodes defines CPUs, memory, size, and the storage type available, such as a high-performance solid-state drive or a regular hard-disk drive. The VM size you choose depends on the workload requirements and the number of pods that you plan to run on each node. As of May 2025, the default VM SKU and size will be dynamically selected by AKS based on available capacity and quota if the parameter is left blank during deployment. For more information, see [Supported VM sizes in Azure Kubernetes Service (AKS)](quotas-skus-regions#supported-vm-sizes).

In AKS, the *VM image* for your cluster's nodes is based on Ubuntu Linux, [Azure Linux](use-azure-linux), or Windows Server 2022. When you create an AKS cluster or scale out the number of nodes, the Azure platform automatically creates and configures the requested number of VMs. Agent nodes are billed as standard VMs. Any VM size discounts, including [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations), are automatically applied.

### OS disks

Default OS disk sizing is used on new clusters or node pools only when a default OS disk size isn't specified. This behavior applies to both managed and ephemeral OS disks. For more information, see [Default OS disk sizing](concepts-storage#default-os-disk-sizing).

### Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS. To maintain node performance and functionality, AKS reserves two types of resources, CPU and memory, on each node. For more information, see [Resource reservations in AKS](node-resource-reservations).

### OS

AKS supports two linux distros: Ubuntu and Azure Linux. Ubuntu is the default Linux distro on AKS. Windows node pools are also supported on AKS with the [Long Term Servicing Channel (LTSC)](/en-us/windows-server/get-started/servicing-channels-comparison) as the default channel on AKS. For more information on default OS versions, see documentation on [node images](node-images).

### Container runtime

A container runtime is software that executes containers and manages container images on a node. The runtime helps abstract away system calls or OS-specific functionality to run containers on Linux or Windows. For Linux node pools, [containerd](https://containerd.io/) is used on Kubernetes version 1.19 and higher. For Windows Server 2019 and 2022 node pools, [containerd](https://containerd.io/) is generally available and is the only runtime option on Kubernetes version 1.23 and higher.

## Pods

A *pod* is a group of one or more containers that share the same network and storage resources and a specification for how to run the containers. Pods typically have a 1:1 mapping with a container, but you can run multiple containers in a pod.

## Node pools

In AKS, nodes of the same configuration are grouped together into *node pools*. These node pools contain the underlying virtual machine scale sets and virtual machines (VMs) that run your applications.

When you create an AKS cluster, you define the initial number of nodes and their size (version), which creates a [system node pool](use-system-pools). System node pools serve the primary purpose of hosting critical system pods, such as CoreDNS and `konnectivity`

.

To support applications that have different compute or storage demands, you can create *user node pools*. User node pools serve the primary purpose of hosting your application pods.

For more information, see [Create node pools in AKS](create-node-pools) and [Manage node pools in AKS](manage-node-pools).

## Node resource group

When you create an AKS cluster in an Azure resource group, the AKS resource provider automatically creates a second resource group called the *node resource group*. This resource group contains all the infrastructure resources associated with the cluster, including VMs, virtual machine scale sets, and storage.

For more information, see the following resources:

[Why are two resource groups created with AKS?](faq)[Can I provide my own name for the AKS node resource group?](faq)[Can I modify tags and other properties of the resources in the AKS node resource group?](faq)

## Namespaces

Kubernetes resources, such as pods and deployments, are logically grouped into *namespaces* to divide an AKS cluster and create, view, or manage access to resources.

The following namespaces are created by default in an AKS cluster:

| Namespace | Description |
|---|---|
`default` |
The
|

`kube-node-lease`

[kube-node-lease](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace enables nodes to communicate their availability to the control plane.`kube-public`

[kube-public](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace isn't typically used, but you can use it so that resources are visible across the whole cluster by any user.`kube-system`

[kube-system](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace is used by Kubernetes to manage cluster resources, such as`coredns`

, `konnectivity-agent`

, and `metrics-server`

. It is not recommended to deploy your own applications to this namespace. For rare cases where deploying your own applications to this namespace is necessary, see the [FAQ](faq#can-admission-controller-webhooks-affect-kube-system-and-internal-aks-namespaces-)to learn how.## Cluster modes

In AKS, you can create a cluster with the Automatic or Standard mode. AKS Automatic provides a more fully managed experience. You can manage cluster configuration, including nodes, scaling, security, and other preconfigured settings. AKS Standard provides more control over the cluster configuration, including the ability to manage node pools, scaling, and other settings.

For more information, see [AKS Automatic and Standard feature comparison](intro-aks-automatic#aks-automatic-and-standard-feature-comparison).

## Pricing tiers

AKS offers three pricing tiers for cluster management: Free, Standard, and Premium. The pricing tier you choose determines the features that are available for managing your cluster.

For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

## Supported Kubernetes versions

For more information, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

## Related content

For information on more core concepts for AKS, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: use-system-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-system-pools -->

# Manage system node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In Azure Kubernetes Service (AKS), nodes of the same configuration are grouped together into *node pools*. Node pools contain the underlying VMs that run your applications. System node pools and user node pools are two different node pool modes for your AKS clusters. System node pools serve the primary purpose of hosting critical system pods such as `CoreDNS`

and `metrics-server`

. User node pools serve the primary purpose of hosting your application pods. However, application pods can be scheduled on system node pools if you wish to only have one pool in your AKS cluster. Every AKS cluster must contain at least one system node pool with at least two nodes.

Important

If you run a single system node pool for your AKS cluster in a production environment, we recommend you use at least three nodes for the node pool.

This article explains how to manage system node pools in AKS. For information about how to use multiple node pools, see [use multiple node pools](use-multiple-node-pools).

## Before you begin

You need the Azure CLI version 2.3.1 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

The following limitations apply when you create and manage AKS clusters that support system node pools.

- See
[Quotas, VM size restrictions, and region availability in AKS](quotas-skus-regions). - An API version of 2020-03-01 or greater must be used to set a node pool mode. Clusters created on API versions older than 2020-03-01 contain only user node pools, but can be migrated to contain system node pools by following
[update pool mode steps](#update-existing-cluster-system-and-user-node-pools). - The name of a node pool may only contain lowercase alphanumeric characters and must begin with a lowercase letter. For Linux node pools, the length must be between 1 and 12 characters. For Windows node pools, the length must be between one and six characters.
- The mode of a node pool is a required property and must be explicitly set when using ARM templates or direct API calls.

## System and user node pools

For a system node pool, AKS automatically assigns the label **kubernetes.azure.com/mode: system** to its nodes. This causes AKS to prefer scheduling system pods on node pools that contain this label. This label doesn't prevent you from scheduling application pods on system node pools. However, we recommend you isolate critical system pods from your application pods to prevent misconfigured or rogue application pods from accidentally deleting system pods.

You can enforce this behavior by creating a dedicated system node pool. Use the `CriticalAddonsOnly=true:NoSchedule`

taint to prevent application pods from being scheduled on system node pools.

System node pools have the following restrictions:

- System node pools must support at least 30 pods as described by the
[minimum and maximum value formula for pods](concepts-network-ip-address-planning#maximum-pods-per-node). - System pools osType must be Linux.
- User node pools osType may be Linux or Windows.
- System pools must contain at least two nodes, and user node pools may contain zero or more nodes.
- System node pools require a VM SKU of at least 4 vCPUs and 4GB memory.
[B series VMs](/en-us/azure/virtual-machines/sizes-b-series-burstable)are not supported for system node pools.- A minimum of three nodes of 8 vCPUs or two nodes of at least 16 vCPUs is recommended (for example, Standard_DS4_v2), especially for large clusters (Multiple CoreDNS Pod replicas, 3-4+ add-ons, etc.).
- Spot node pools require user node pools.
- Adding another system node pool or changing which node pool is a system node pool
*does not*automatically move system pods. System pods can continue to run on the same node pool, even if you change it to a user node pool. If you delete or scale down a node pool running system pods that were previously a system node pool, those system pods are redeployed with preferred scheduling to the new system node pool.

You can do the following operations with node pools:

- Create a dedicated system node pool (prefer scheduling of system pods to node pools of
`mode:system`

) - Change a system node pool to be a user node pool, provided you have another system node pool to take its place in the AKS cluster.
- Change a user node pool to be a system node pool.
- Delete user node pools.
- You can delete system node pools, provided you have another system node pool to take its place in the AKS cluster.
- An AKS cluster may have multiple system node pools and requires at least one system node pool.
- If you want to change various immutable settings on existing node pools, you can create new node pools to replace them. One example is to add a new node pool with a new maxPods setting and delete the old node pool.
- Use
[node affinity](operator-best-practices-advanced-scheduler#node-affinity)to*require*or*prefer*which nodes can be scheduled based on node labels. You can set`key`

to`kubernetes.azure.com`

,`operator`

to`In`

, and`values`

of either`user`

or`system`

to your YAML, applying this definition using`kubectl apply -f yourYAML.yaml`

.

## Create a new AKS cluster with a system node pool

When you create a new AKS cluster, the initial node pool defaults to a mode of type `system`

. When you create new node pools with `az aks nodepool add`

, those node pools are user node pools unless you explicitly specify the mode parameter.

The following example creates a resource group named *myResourceGroup* in the *eastus* region.

```
az group create --name myResourceGroup --location eastus
```


Use the [az aks create](/en-us/cli/azure/aks#az-aks-create) command to create an AKS cluster. The following example creates a cluster named *myAKSCluster* with one dedicated system pool containing two nodes. For your production workloads, ensure you're using system node pools with at least three nodes. This operation may take several minutes to complete.

```
# Create a new AKS cluster with a single system pool
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --generate-ssh-keys
```


## Add a dedicated system node pool to an existing AKS cluster

You can add one or more system node pools to existing AKS clusters. It's recommended to schedule your application pods on user node pools, and dedicate system node pools to only critical system pods. This prevents rogue application pods from accidentally deleting system pods. Enforce this behavior with the `CriticalAddonsOnly=true:NoSchedule`

[taint](manage-node-pools#set-node-pool-taints) for your system node pools.

The following command adds a dedicated node pool of mode type system with a default count of three nodes.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name systempool \
--node-count 3 \
--node-taints CriticalAddonsOnly=true:NoSchedule \
--mode System
```


## Show details for your node pool

You can check the details of your node pool with the following command.

```
az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --name systempool
```


A mode of type **System** is defined for system node pools, and a mode of type **User** is defined for user node pools. For a system pool, verify the taint is set to `CriticalAddonsOnly=true:NoSchedule`

, which will prevent application pods from beings scheduled on this node pool.

```
{
"agentPoolType": "VirtualMachineScaleSets",
"availabilityZones": null,
"count": 3,
"enableAutoScaling": null,
"enableNodePublicIp": false,
"id": "/subscriptions/yourSubscriptionId/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster/agentPools/systempool",
"maxCount": null,
"maxPods": 110,
"minCount": null,
"mode": "System",
"name": "systempool",
"nodeImageVersion": "AKSUbuntu-1604-2020.06.30",
"nodeLabels": {},
"nodeTaints": [
"CriticalAddonsOnly=true:NoSchedule"
],
"orchestratorVersion": "1.16.10",
"osDiskSizeGb": 128,
"osType": "Linux",
"provisioningState": "Succeeded",
"proximityPlacementGroupId": null,
"resourceGroup": "myResourceGroup",
"scaleSetEvictionPolicy": null,
"scaleSetPriority": null,
"spotMaxPrice": null,
"tags": null,
"type": "Microsoft.ContainerService/managedClusters/agentPools",
"upgradeSettings": {
"maxSurge": null
},
"vmSize": "Standard_DS2_v2",
"vnetSubnetId": null
}
```


## Update existing cluster system and user node pools

Note

An API version of 2020-03-01 or greater must be used to set a system node pool mode. Clusters created on API versions older than 2020-03-01 contain only user node pools as a result. To receive system node pool functionality and benefits on older clusters, update the mode of existing node pools with the following commands on the latest Azure CLI version.

You can change modes for both system and user node pools. You can change a system node pool to a user pool only if another system node pool already exists on the AKS cluster.

This command changes a system node pool to a user node pool.

```
az aks nodepool update --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --mode user
```


This command changes a user node pool to a system node pool.

```
az aks nodepool update --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --mode system
```


## Delete a system node pool

Note

To use system node pools on AKS clusters before API version 2020-03-02, add a new system node pool, then delete the original default node pool.

You must have at least two system node pools on your AKS cluster before you can delete one of them.

```
az aks nodepool delete --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool
```


## Clean up resources

To delete the cluster, use the [az group delete](/en-us/cli/azure/group#az-group-delete) command to delete the AKS resource group:

```
az group delete --name myResourceGroup --yes --no-wait
```


## Next steps

In this article, you learned how to create and manage system node pools in an AKS cluster. For information about how to start and stop AKS node pools, see [start and stop AKS node pools](start-stop-nodepools).


---

<!-- DOCUMENTO FUSIONADO: _cluster-configuration_concepts-clusters-workloads.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cluster-configuration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/cluster-configuration -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## What is Kubernetes?

Kubernetes is an open-source container orchestration platform for automating the deployment, scaling, and management of containerized applications. For more information, see the official [Kubernetes documentation](https://kubernetes.io/docs/home/).

## What is AKS?

AKS is a managed Kubernetes service that simplifies deploying, managing, and scaling containerized applications that use Kubernetes. For more information, see [What is Azure Kubernetes Service (AKS)?](what-is-aks).

## Cluster components

An AKS cluster is divided into two main components:

**Control plane**: The control plane provides the core Kubernetes services and orchestration of application workloads.**Nodes**: Nodes are the underlying virtual machines (VMs) that run your applications.

Note

AKS managed components have the label `kubernetes.azure.com/managedby`

: `aks`

.

AKS manages the Helm releases with the prefix `aks-managed`

. Continuously increasing revisions on these releases are expected and safe.

### Control plane

The Azure managed control plane is composed of several components that help manage the cluster:

| Component | Description |
|---|---|
`kube-apiserver` |
The API server (
|

`etcd`

[etcd](https://kubernetes.io/docs/concepts/overview/components/#etcd)helps to maintain the state of your Kubernetes cluster and configuration.`kube-scheduler`

[kube-scheduler](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler)) helps to make scheduling decisions. It watches for new pods with no assigned node and selects a node for them to run on.`kube-controller-manager`

[kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager)) runs controller processes, such as noticing and responding when nodes go down.`cloud-controller-manager`

[cloud-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager)) embeds cloud-specific control logic to run controllers specific to the cloud provider.### Nodes

Each AKS cluster has at least one node, which is an Azure VM that runs Kubernetes node components. The following components run on each node:

| Component | Description |
|---|---|
`kubelet` |
The
|

`kube-proxy`

[kube-proxy](https://kubernetes.io/docs/concepts/overview/components/#kube-proxy)is a network proxy that maintains network rules on nodes.`container runtime`

[container runtime](https://kubernetes.io/docs/concepts/overview/components/#container-runtime)manages the execution and lifecycle of containers.## Node configuration

Configure the following settings for nodes.

### VM size and image

The *Azure VM size* for your nodes defines CPUs, memory, size, and the storage type available, such as a high-performance solid-state drive or a regular hard-disk drive. The VM size you choose depends on the workload requirements and the number of pods that you plan to run on each node. As of May 2025, the default VM SKU and size will be dynamically selected by AKS based on available capacity and quota if the parameter is left blank during deployment. For more information, see [Supported VM sizes in Azure Kubernetes Service (AKS)](quotas-skus-regions#supported-vm-sizes).

In AKS, the *VM image* for your cluster's nodes is based on Ubuntu Linux, [Azure Linux](use-azure-linux), or Windows Server 2022. When you create an AKS cluster or scale out the number of nodes, the Azure platform automatically creates and configures the requested number of VMs. Agent nodes are billed as standard VMs. Any VM size discounts, including [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations), are automatically applied.

### OS disks

Default OS disk sizing is used on new clusters or node pools only when a default OS disk size isn't specified. This behavior applies to both managed and ephemeral OS disks. For more information, see [Default OS disk sizing](concepts-storage#default-os-disk-sizing).

### Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS. To maintain node performance and functionality, AKS reserves two types of resources, CPU and memory, on each node. For more information, see [Resource reservations in AKS](node-resource-reservations).

### OS

AKS supports two linux distros: Ubuntu and Azure Linux. Ubuntu is the default Linux distro on AKS. Windows node pools are also supported on AKS with the [Long Term Servicing Channel (LTSC)](/en-us/windows-server/get-started/servicing-channels-comparison) as the default channel on AKS. For more information on default OS versions, see documentation on [node images](node-images).

### Container runtime

A container runtime is software that executes containers and manages container images on a node. The runtime helps abstract away system calls or OS-specific functionality to run containers on Linux or Windows. For Linux node pools, [containerd](https://containerd.io/) is used on Kubernetes version 1.19 and higher. For Windows Server 2019 and 2022 node pools, [containerd](https://containerd.io/) is generally available and is the only runtime option on Kubernetes version 1.23 and higher.

## Pods

A *pod* is a group of one or more containers that share the same network and storage resources and a specification for how to run the containers. Pods typically have a 1:1 mapping with a container, but you can run multiple containers in a pod.

## Node pools

In AKS, nodes of the same configuration are grouped together into *node pools*. These node pools contain the underlying virtual machine scale sets and virtual machines (VMs) that run your applications.

When you create an AKS cluster, you define the initial number of nodes and their size (version), which creates a [system node pool](use-system-pools). System node pools serve the primary purpose of hosting critical system pods, such as CoreDNS and `konnectivity`

.

To support applications that have different compute or storage demands, you can create *user node pools*. User node pools serve the primary purpose of hosting your application pods.

For more information, see [Create node pools in AKS](create-node-pools) and [Manage node pools in AKS](manage-node-pools).

## Node resource group

When you create an AKS cluster in an Azure resource group, the AKS resource provider automatically creates a second resource group called the *node resource group*. This resource group contains all the infrastructure resources associated with the cluster, including VMs, virtual machine scale sets, and storage.

For more information, see the following resources:

[Why are two resource groups created with AKS?](faq)[Can I provide my own name for the AKS node resource group?](faq)[Can I modify tags and other properties of the resources in the AKS node resource group?](faq)

## Namespaces

Kubernetes resources, such as pods and deployments, are logically grouped into *namespaces* to divide an AKS cluster and create, view, or manage access to resources.

The following namespaces are created by default in an AKS cluster:

| Namespace | Description |
|---|---|
`default` |
The
|

`kube-node-lease`

[kube-node-lease](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace enables nodes to communicate their availability to the control plane.`kube-public`

[kube-public](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace isn't typically used, but you can use it so that resources are visible across the whole cluster by any user.`kube-system`

[kube-system](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace is used by Kubernetes to manage cluster resources, such as`coredns`

, `konnectivity-agent`

, and `metrics-server`

. It is not recommended to deploy your own applications to this namespace. For rare cases where deploying your own applications to this namespace is necessary, see the [FAQ](faq#can-admission-controller-webhooks-affect-kube-system-and-internal-aks-namespaces-)to learn how.## Cluster modes

In AKS, you can create a cluster with the Automatic or Standard mode. AKS Automatic provides a more fully managed experience. You can manage cluster configuration, including nodes, scaling, security, and other preconfigured settings. AKS Standard provides more control over the cluster configuration, including the ability to manage node pools, scaling, and other settings.

For more information, see [AKS Automatic and Standard feature comparison](intro-aks-automatic#aks-automatic-and-standard-feature-comparison).

## Pricing tiers

AKS offers three pricing tiers for cluster management: Free, Standard, and Premium. The pricing tier you choose determines the features that are available for managing your cluster.

For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

## Supported Kubernetes versions

For more information, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

## Related content

For information on more core concepts for AKS, see the following resources:


---

<!-- DOCUMENTO FUSIONADO: concepts-clusters-workloads.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-clusters-workloads -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## What is Kubernetes?

Kubernetes is an open-source container orchestration platform for automating the deployment, scaling, and management of containerized applications. For more information, see the official [Kubernetes documentation](https://kubernetes.io/docs/home/).

## What is AKS?

AKS is a managed Kubernetes service that simplifies deploying, managing, and scaling containerized applications that use Kubernetes. For more information, see [What is Azure Kubernetes Service (AKS)?](what-is-aks).

## Cluster components

An AKS cluster is divided into two main components:

**Control plane**: The control plane provides the core Kubernetes services and orchestration of application workloads.**Nodes**: Nodes are the underlying virtual machines (VMs) that run your applications.

Note

AKS managed components have the label `kubernetes.azure.com/managedby`

: `aks`

.

AKS manages the Helm releases with the prefix `aks-managed`

. Continuously increasing revisions on these releases are expected and safe.

### Control plane

The Azure managed control plane is composed of several components that help manage the cluster:

| Component | Description |
|---|---|
`kube-apiserver` |
The API server (
|

`etcd`

[etcd](https://kubernetes.io/docs/concepts/overview/components/#etcd)helps to maintain the state of your Kubernetes cluster and configuration.`kube-scheduler`

[kube-scheduler](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler)) helps to make scheduling decisions. It watches for new pods with no assigned node and selects a node for them to run on.`kube-controller-manager`

[kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager)) runs controller processes, such as noticing and responding when nodes go down.`cloud-controller-manager`

[cloud-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager)) embeds cloud-specific control logic to run controllers specific to the cloud provider.### Nodes

Each AKS cluster has at least one node, which is an Azure VM that runs Kubernetes node components. The following components run on each node:

| Component | Description |
|---|---|
`kubelet` |
The
|

`kube-proxy`

[kube-proxy](https://kubernetes.io/docs/concepts/overview/components/#kube-proxy)is a network proxy that maintains network rules on nodes.`container runtime`

[container runtime](https://kubernetes.io/docs/concepts/overview/components/#container-runtime)manages the execution and lifecycle of containers.## Node configuration

Configure the following settings for nodes.

### VM size and image

The *Azure VM size* for your nodes defines CPUs, memory, size, and the storage type available, such as a high-performance solid-state drive or a regular hard-disk drive. The VM size you choose depends on the workload requirements and the number of pods that you plan to run on each node. As of May 2025, the default VM SKU and size will be dynamically selected by AKS based on available capacity and quota if the parameter is left blank during deployment. For more information, see [Supported VM sizes in Azure Kubernetes Service (AKS)](quotas-skus-regions#supported-vm-sizes).

In AKS, the *VM image* for your cluster's nodes is based on Ubuntu Linux, [Azure Linux](use-azure-linux), or Windows Server 2022. When you create an AKS cluster or scale out the number of nodes, the Azure platform automatically creates and configures the requested number of VMs. Agent nodes are billed as standard VMs. Any VM size discounts, including [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations), are automatically applied.

### OS disks

Default OS disk sizing is used on new clusters or node pools only when a default OS disk size isn't specified. This behavior applies to both managed and ephemeral OS disks. For more information, see [Default OS disk sizing](concepts-storage#default-os-disk-sizing).

### Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS. To maintain node performance and functionality, AKS reserves two types of resources, CPU and memory, on each node. For more information, see [Resource reservations in AKS](node-resource-reservations).

### OS

AKS supports two linux distros: Ubuntu and Azure Linux. Ubuntu is the default Linux distro on AKS. Windows node pools are also supported on AKS with the [Long Term Servicing Channel (LTSC)](/en-us/windows-server/get-started/servicing-channels-comparison) as the default channel on AKS. For more information on default OS versions, see documentation on [node images](node-images).

### Container runtime

A container runtime is software that executes containers and manages container images on a node. The runtime helps abstract away system calls or OS-specific functionality to run containers on Linux or Windows. For Linux node pools, [containerd](https://containerd.io/) is used on Kubernetes version 1.19 and higher. For Windows Server 2019 and 2022 node pools, [containerd](https://containerd.io/) is generally available and is the only runtime option on Kubernetes version 1.23 and higher.

## Pods

A *pod* is a group of one or more containers that share the same network and storage resources and a specification for how to run the containers. Pods typically have a 1:1 mapping with a container, but you can run multiple containers in a pod.

## Node pools

In AKS, nodes of the same configuration are grouped together into *node pools*. These node pools contain the underlying virtual machine scale sets and virtual machines (VMs) that run your applications.

When you create an AKS cluster, you define the initial number of nodes and their size (version), which creates a [system node pool](use-system-pools). System node pools serve the primary purpose of hosting critical system pods, such as CoreDNS and `konnectivity`

.

To support applications that have different compute or storage demands, you can create *user node pools*. User node pools serve the primary purpose of hosting your application pods.

For more information, see [Create node pools in AKS](create-node-pools) and [Manage node pools in AKS](manage-node-pools).

## Node resource group

When you create an AKS cluster in an Azure resource group, the AKS resource provider automatically creates a second resource group called the *node resource group*. This resource group contains all the infrastructure resources associated with the cluster, including VMs, virtual machine scale sets, and storage.

For more information, see the following resources:

[Why are two resource groups created with AKS?](faq)[Can I provide my own name for the AKS node resource group?](faq)[Can I modify tags and other properties of the resources in the AKS node resource group?](faq)

## Namespaces

Kubernetes resources, such as pods and deployments, are logically grouped into *namespaces* to divide an AKS cluster and create, view, or manage access to resources.

The following namespaces are created by default in an AKS cluster:

| Namespace | Description |
|---|---|
`default` |
The
|

`kube-node-lease`

[kube-node-lease](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace enables nodes to communicate their availability to the control plane.`kube-public`

[kube-public](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace isn't typically used, but you can use it so that resources are visible across the whole cluster by any user.`kube-system`

[kube-system](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace is used by Kubernetes to manage cluster resources, such as`coredns`

, `konnectivity-agent`

, and `metrics-server`

. It is not recommended to deploy your own applications to this namespace. For rare cases where deploying your own applications to this namespace is necessary, see the [FAQ](faq#can-admission-controller-webhooks-affect-kube-system-and-internal-aks-namespaces-)to learn how.## Cluster modes

In AKS, you can create a cluster with the Automatic or Standard mode. AKS Automatic provides a more fully managed experience. You can manage cluster configuration, including nodes, scaling, security, and other preconfigured settings. AKS Standard provides more control over the cluster configuration, including the ability to manage node pools, scaling, and other settings.

For more information, see [AKS Automatic and Standard feature comparison](intro-aks-automatic#aks-automatic-and-standard-feature-comparison).

## Pricing tiers

AKS offers three pricing tiers for cluster management: Free, Standard, and Premium. The pricing tier you choose determines the features that are available for managing your cluster.

For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

## Supported Kubernetes versions

For more information, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

## Related content

For information on more core concepts for AKS, see the following resources:
