---
merged_at: 2026-02-05T08:27:02.804595
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-windows-2019-2022 -->

# Upgrade the operating system (OS) version for your Azure Kubernetes Service (AKS) Windows workloads

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When upgrading the OS version of a running Windows workload on Azure Kubernetes Service (AKS), you need to deploy a new node pool to ensure the Windows versions match on each node pool. This article describes the steps to upgrade the OS version for Windows workloads on AKS.

## Windows Server OS version support

When a new Windows Server OS version is released, AKS is committed to supporting it. We recommend that you upgrade to the latest version to take advantage of the fixes, improvements, and new functionality. AKS provides a five-year support lifecycle for every Windows Server version, starting with Windows Server 2022. During this period, AKS releases a new version that supports a newer version of Windows Server OS for you to upgrade to. After the five-year lifecycle ends, you must migrate workloads to newer supported versions to ensure compatibility, security updates, and continued support from AKS.

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Limitations

- Node pool update to migrate from one Windows Server version to another isn't supported.
- Different Windows Server versions can't coexist on the same node pool on AKS. You need to create a new node pool to host the new OS version. It's important that you match the permissions and access of the previous node pool to the new one.
- Windows Server 2025 (preview) is supported starting in Kubernetes version 1.32.

## Before you begin

- Update the
`FROM`

statement in your Dockerfile to the new OS version. - Check your application and verify the container app works on the new OS version.
- Deploy the verified container app on AKS to a development or testing environment.
- Take note of the new image name or tag for use in this article.

Note

To learn how to build a Dockerfile for Windows workloads, see [Dockerfile on Windows](/en-us/virtualization/windowscontainers/manage-docker/manage-windows-dockerfile) and [Optimize Windows Dockerfiles](/en-us/virtualization/windowscontainers/manage-docker/optimize-windows-dockerfile).

### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b5**.`az extension update --name aks-preview`


### Register `AksWindows2025Preview`

feature flag

Register the

`AksWindows2025Preview`

feature flag using the [`az feature register`

][az-feature-register] command.`az feature register --namespace "Microsoft.ContainerService" --name "AksWindows2025Preview"`

Verify the registration status using the [

`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.`az feature show --namespace Microsoft.ContainerService --name AksWindows2025Preview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Add a new node pool to an existing cluster

Add a node pool with your desired OS version to your existing cluster:

[Use CLI to add a Windows node pool](learn/quick-windows-container-deploy-cli)to an existing cluster.[Use Portal to add a Windows node pool](learn/quick-windows-container-deploy-portal)to an existing cluster.[Use PowerShell to add a Windows node pool](learn/quick-windows-container-deploy-powershell)to an existing cluster.[Use Terraform to add a Windows node pool](learn/quick-windows-container-deploy-terraform)to an existing cluster.

## Update the YAML file

Node Selector is the most common and recommended option for placement of Windows pods on Windows nodes.

Add Node Selector to your YAML file by adding the following annotation:

`nodeSelector: "kubernetes.io/os": windows`

The annotation finds any available Windows node and places the pod on that node (following all other scheduling rules). When upgrading your OS version, you need to enforce the placement on a Windows node and a node running the latest OS version. To accomplish this, one option is to use a different annotation. Update

`<OSSKU>`

to match the ossku your desired Windows OS version, for example`Windows2025`

.`nodeSelector: "kubernetes.azure.com/os-sku": <OSSKU>`

Once you update the

`nodeSelector`

in the YAML file, you also need to update the container image you want to use. You can get this information from the previous step in which you created a new version of the containerized application by changing the`FROM`

statement on your Dockerfile.Note

You should use the same YAML file you used to initially deploy the application. This ensures that no other configuration changes besides the

`nodeSelector`

and container image.

## Apply the updated YAML file to the existing workload

View the nodes on your cluster using the

`kubectl get nodes`

command.`kubectl get nodes -o wide`

The following example output shows all nodes on the cluster, including the new node pool you created and the existing node pools:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME aks-agentpool-18877473-vmss000000 Ready agent 5h40m v1.23.8 10.240.0.4 <none> Ubuntu 18.04.6 LTS 5.4.0-1085-azure containerd://1.5.11+azure-2 akspoolws000000 Ready agent 3h15m v1.23.8 10.240.0.208 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akspoolws000001 Ready agent 3h17m v1.23.8 10.240.0.239 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akspoolws000002 Ready agent 3h17m v1.23.8 10.240.1.14 <none> Windows Server 2022 Datacenter 10.0.20348.825 containerd://1.6.6+azure akswspool000000 Ready agent 5h37m v1.23.8 10.240.0.115 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure akswspool000001 Ready agent 5h37m v1.23.8 10.240.0.146 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure akswspool000002 Ready agent 5h37m v1.23.8 10.240.0.177 <none> Windows Server 2019 Datacenter 10.0.17763.3165 containerd://1.6.6+azure`

Apply the updated YAML file to the existing workload using the

`kubectl apply`

command and specify the name of the YAML file.`kubectl apply -f <filename>`

The following example output shows a

*configured*status for the deployment:`deployment.apps/sample configured service/sample unchanged`

At this point, AKS starts the process of terminating the existing pods and deploying new pods to the nodes with the

`nodeSelector`

annotation.Check the status of the deployment using the

`kubectl get pods`

command.`kubectl get pods -o wide`

The following example output shows the pods in the

`default`

namespace:`NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES sample-7794bfcc4c-k62cq 1/1 Running 0 2m49s 10.240.0.238 akspoolws000000 <none> <none> sample-7794bfcc4c-rswq9 1/1 Running 0 2m49s 10.240.1.10 akspoolws000001 <none> <none> sample-7794bfcc4c-sh78c 1/1 Running 0 2m49s 10.240.0.228 akspoolws000000 <none> <none>`


## Security and authentication considerations

If you're using Group Managed Service Accounts (gMSA), you need to update the Managed Identity configuration for the new node pool. gMSA uses a secret (user account and password) so the node that runs the Windows pod can authenticate the container against Microsoft Entra ID. To access that secret on Azure Key Vault, the node uses a Managed Identity that allows the node to access the resource. Since Managed Identities are configured per node pool, and the pod now resides on a new node pool, you need to update that configuration. For more information, see [Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster](use-group-managed-service-accounts).

The same principle applies to Managed Identities for any other pod or node pool when accessing other Azure resources. You need to update any access that Managed Identity provides to reflect the new node pool. To view update and sign-in activities, see [How to view Managed Identity activity](/en-us/azure/active-directory/managed-identities-azure-resources/how-to-view-managed-identity-activity).

## Next steps

In this article, you learned how to upgrade the OS version for Windows workloads on AKS. To learn more about Windows workloads on AKS, see [Deploy a Windows container application on Azure Kubernetes Service (AKS)](learn/quick-windows-container-deploy-cli).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing-dns-ssl -->

# Set up a custom domain name and SSL certificate with the application routing add-on for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure custom domain names and SSL/TLS certificates for AKS ingress using [Azure Key Vault](/en-us/azure/key-vault/general/overview) and [Azure DNS](/en-us/azure/dns/dns-overview) with the [application routing add-on for AKS](app-routing).

## Prerequisites

An AKS cluster with the

[application routing add-on](app-routing).Azure Key Vault if you want to configure SSL termination and store certificates in the vault hosted in Azure. If you don't have one, see

[Create a key vault using the Azure CLI](/en-us/azure/key-vault/general/quick-create-cli).To enable support for HTTPS traffic, you need an SSL certificate. If you don't have one, see

[create a certificate](#create-and-export-a-self-signed-ssl-certificate).Azure DNS if you want to configure global and private zone management and host them in Azure. If you don't have an Azure DNS zone, you can

[create one](#create-a-global-azure-dns-zone). To enable support for DNS zones:- All global Azure DNS zones need to be in the same resource group, which could be different from the cluster resource group.
- All private Azure DNS zones need to be in the same resource group, which could be different from the cluster resource group.
- The resource group doesn't need to be in the same subscription as the cluster.


### Required Azure permissions

**Your user account needs**: [Owner](/en-us/azure/role-based-access-control/built-in-roles#owner), [Azure account administrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles), or [Azure co-administrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles) role on your Azure subscription.

**What the commands do**: When you run `az aks approuting update --attach-kv`

or `az aks approuting zone add --attach-zones`

, these commands use your role assignment permissions to automatically grant the application routing add-on's managed identity the following roles:

**Key Vault Certificate User**role on your Azure Key Vault (for certificate access).**DNS Zone Contributor**role on your Azure DNS zones (for DNS record management).

For more information on AKS managed identities, see [Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use `kubectl`

, the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure kubectl to connect to your Kubernetes cluster using the

command.`az aks get-credentials`

`# Set environment variables for your resource group and cluster name export RESOURCE_GROUP=<resource-group-name> export CLUSTER_NAME=<cluster-name> # Get the AKS cluster credentials az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Create and export a self-signed SSL certificate

For testing, you can use a self-signed public certificate instead of a Certificate Authority (CA)-signed certificate. If you already have a certificate, you can skip this step.

Caution

Self-signed certificates are digital certificates that aren't signed by a trusted third-party CA. The company or developer responsible for the website or software creates, issues, and signs these certificates. This is why self-signed certificates are considered unsafe for public-facing websites and applications. Azure Key Vault has a [trusted partnership with the some Certificate Authorities](/en-us/azure/key-vault/certificates/how-to-integrate-certificate-authority).

Create a self-signed SSL certificate to use with the ingress using the

`openssl req`

command. Make sure you replacewith the DNS name you're using.`<host-name>`

`openssl req -new -x509 -nodes -out aks-ingress-tls.crt -keyout aks-ingress-tls.key -subj "/CN=<host-name>" -addext "subjectAltName=DNS:<host-name>"`

Export the SSL certificate and skip the password prompt using the

`openssl pkcs12 -export`

command.`openssl pkcs12 -export -in aks-ingress-tls.crt -inkey aks-ingress-tls.key -out aks-ingress-tls.pfx`


## Import a self-signed SSL certificate into Azure Key Vault

Import the SSL certificate into Azure Key Vault using the

command. If your certificate is password protected, you can pass the password through the`az keyvault certificate import`

`--password`

flag.`# Set environment variables for your key vault name and certificate name export KEY_VAULT_NAME=<key-vault-name> export KEY_VAULT_CERT_NAME=<key-vault-certificate-name> # Import the SSL certificate into Azure Key Vault az keyvault certificate import --vault-name $KEY_VAULT_NAME --name $KEY_VAULT_CERT_NAME --file aks-ingress-tls.pfx [--password <certificate password if specified>]`


Note

To enable the application routing add-on to reload certificates from Azure Key Vault when they change, you should enable the [secret autorotation feature](csi-secrets-store-configuration-options) of the Secrets Store CSI driver. When autorotation is enabled, the driver updates the pod mount and the Kubernetes secret by polling for changes periodically, based on the rotation poll interval you define. The default rotation poll interval is two minutes.

## Enable Azure Key Vault integration

Azure Key Vault offers [two authorization systems](/en-us/azure/key-vault/general/rbac-access-policy): **Azure role-based access control (Azure RBAC)**, which operates on the management plane, and the **access policy model**, which operates on both the management plane and the data plane. The `--attach-kv`

operation selects the appropriate access model to use.

Get the resource ID for the key vault using the

command and set the output to an environment variable.`az keyvault show`

`KEY_VAULT_ID=$(az keyvault show --name <KeyVaultName> --query "id" --output tsv)`

Update the application routing add-on to enable the Azure Key Vault provider for Secrets Store CSI Driver and apply the required role assignments using the

command with the`az aks approuting update`

`--enable-kv`

and`--attach-kv`

arguments.`az aks approuting update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-kv --attach-kv ${KEY_VAULT_ID}`


## Create a global Azure DNS zone

If you already have an Azure DNS zone, you can skip this step.

Create an Azure DNS zone using the

command.`az network dns zone create`

`# Set environment variables for your resource group and DNS zone name export RESOURCE_GROUP=<resource-group-name> export ZONE_NAME=<zone-name> # Create the Azure DNS zone az network dns zone create --resource-group $RESOURCE_GROUP --name $ZONE_NAME`


## Enable Azure DNS integration

Get the resource ID for the DNS zone using the

command and set the output to an environment variable.`az network dns zone show`

`ZONE_ID=$(az network dns zone show --resource-group $RESOURCE_GROUP --name $ZONE_NAME --query "id" --output tsv)`

Update the application routing add-on to enable Azure DNS integration using the

command. You can pass a comma-separated list of DNS zone resource IDs.`az aks approuting zone`

`az aks approuting zone add --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --ids=${ZONE_ID} --attach-zones`


## Create an Ingress class that uses a host name and a certificate from Azure Key Vault

The application routing add-on creates an Ingress class on the cluster named *webapprouting.kubernetes.azure.com*. When you create an Ingress object with this class, it activates the add-on.

Get the certificate URI to use in the ingress from Azure Key Vault using the

command.`az keyvault certificate show`

`az keyvault certificate show --vault-name $KEY_VAULT_NAME --name $KEY_VAULT_CERT_NAME --query "id" --output tsv`

The following example output shows the certificate URI returned from the command:

`https://KeyVaultName.vault.azure.net/certificates/KeyVaultCertificateName/ab12c34567d89e01f2345g6h78ijkl90`

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.Update

with the name of your DNS host and`<host-name>`

with the URI returned from the previous command. The string value for`<key-vault-certificate-uri>`

should only include`<key-vault-certificate-uri>`

`https://yourkeyvault.vault.azure.net/certificates/certname`

. Remove the*Certificate Version*at the end of the URI string to get the current version.The

key in the`secretName`

`tls`

section defines the name of the secret that contains the certificate for this Ingress resource. This certificate is presented in the browser when a client browses to the URL specified in the`<host-name>`

key. Make sure that the value of`secretName`

is equal to`keyvault-`

followed by the value of the Ingress resource name (from`metadata.name`

). In the example YAML,`secretName`

needs to be equal to`keyvault-<your-ingress-name>`

.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: annotations: kubernetes.azure.com/tls-cert-keyvault-uri: <key-vault-certificate-uri> name: aks-helloworld namespace: hello-web-app-routing spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - host: <host-name> http: paths: - backend: service: name: aks-helloworld port: number: 80 path: / pathType: Prefix tls: - hosts: - <host-name> secretName: keyvault-<your-ingress-name>`

Create the cluster resources using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n hello-web-app-routing`

The following example output shows the created resource:

`Ingress.networking.k8s.io/aks-helloworld created`


## Verify the managed ingress was created

Verify the managed ingress was created using the

command.`kubectl get ingress`

`kubectl get ingress -n hello-web-app-routing`

The following example output shows the created managed ingress:

`NAME CLASS HOSTS ADDRESS PORTS AGE aks-helloworld webapprouting.kubernetes.azure.com myapp.contoso.com 20.51.92.19 80, 443 4m`


## Related content

Learn about monitoring the Ingress NGINX controller metrics included with the application routing add-on with [with Prometheus in Grafana](app-routing-nginx-prometheus) as part of analyzing the performance and usage of your application.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/image-integrity -->

# Use Image Integrity to validate signed images before deploying them to your Azure Kubernetes Service (AKS) clusters (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) and its underlying container model provide increased scalability and manageability for cloud native applications. With AKS, you can launch flexible software applications according to the runtime needs of your system. However, this flexibility can introduce new challenges.

In these application environments, using signed container images helps verify that your deployments are built from a trusted entity and that images haven't been tampered with since their creation. Image Integrity is a service that allows you to add an Azure Policy built-in definition to verify that only signed images are deployed to your AKS clusters.

Note

Image Integrity is a feature based on [Ratify](https://github.com/deislabs/ratify). On an AKS cluster, the feature name and property name is `ImageIntegrity`

, while the relevant Image Integrity pods' names contain `Ratify`

.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

An Azure subscription. If you don't have an Azure subscription, you can create a

[free account](https://azure.microsoft.com/free).`aks-preview`

CLI extension version 0.5.96 or later.Ensure that the Azure Policy add-on for AKS is enabled on your cluster. If you don't have this add-on installed, see

[Install Azure Policy add-on for AKS](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks).An AKS cluster enabled with OIDC Issuer. To create a new cluster or update an existing cluster, see

[Configure an AKS cluster with OIDC Issuer](use-oidc-issuer).The

`EnableImageIntegrityPreview`

feature flags registered on your Azure subscription. Register the feature flags using the following commands:Register the

`EnableImageIntegrityPreview`

feature flags using thecommand.`az feature register`

`# Register the EnableImageIntegrityPreview feature flag az feature register --namespace "Microsoft.ContainerService" --name "EnableImageIntegrityPreview" It may take a few minutes for the status to show as *Registered*.`

Verify the registration status using the

command.`az feature show`

`# Verify the EnableImageIntegrityPreview feature flag registration status az feature show --namespace "Microsoft.ContainerService" --name "EnableImageIntegrityPreview"`

Once the status shows

*Registered*, refresh the registration of the`Microsoft.ContainerService`

resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Considerations and limitations

- Your AKS clusters must run Kubernetes version 1.26 or above.
- You shouldn't use this feature for production Azure Container Registry (ACR) registries or workloads.
- Image Integrity supports a maximum of 200 unique signatures concurrently cluster-wide.
- Notation is the only supported verifier.
- Audit is the only supported verification policy effect.

## How Image Integrity works

Image Integrity uses Ratify, Azure Policy, and Gatekeeper to validate signed images before deploying them to your AKS clusters. Enabling Image Integrity on your cluster deploys a `Ratify`

pod. This `Ratify`

pod performs the following tasks:

- Reconciles certificates from Azure Key Vault per the configuration you set up through
`Ratify`

CRDs. - Accesses images stored in ACR when validation requests come from
[Azure Policy](/en-us/azure/governance/policy/concepts/policy-for-kubernetes). To enable this experience, Azure Policy extends Gatekeeper, an admission controller webhook for[Open Policy Agent (OPA)](https://www.openpolicyagent.org/). - Determines whether the target image is signed with a trusted cert and therefore considered as
*trusted*. `AzurePolicy`

and`Gatekeeper`

consume the validation results as the compliance state to decide whether to allow the deployment request.

## Enable Image Integrity on your AKS cluster

Note

Image signature verification is a governance-oriented scenario and leverages [Azure Policy](/en-us/azure/governance/policy/concepts/policy-for-kubernetes) to verify image signatures on AKS clusters at-scale. We recommend using AKS's Image Integrity built-in Azure Policy initiative, which is available in [Azure Policy's built-in definition library](/en-us/azure/governance/policy/samples/built-in-policies#kubernetes).

Create a policy assignment with the AKS policy initiative

using the`[Preview]: Use Image Integrity to ensure only trusted images are deployed`

command.`az policy assignment create`

`export SCOPE="/subscriptions/${SUBSCRIPTION}/resourceGroups/${RESOURCE_GROUP}" export LOCATION=$(az group show --name ${RESOURCE_GROUP} --query location -o tsv) az policy assignment create --name 'deploy-trustedimages' --policy-set-definition 'af28bf8b-c669-4dd3-9137-1e68fdc61bd6' --display-name 'Audit deployment with unsigned container images' --scope ${SCOPE} --mi-system-assigned --role Contributor --identity-scope ${SCOPE} --location ${LOCATION}`

The

`Ratify`

pod deploys after you enable the feature.

Note

The policy deploys the Image Integrity feature on your cluster when it detects any update operation on the cluster. If you want to enable the feature immediately, you need to create a policy remediation using the [ az policy remediation create](/en-us/cli/azure/policy/remediation#az-policy-remediation-create) command.

```
assignment_id=$(az policy assignment show --name 'deploy-trustedimages' --scope ${SCOPE} --query id -o tsv)
az policy remediation create --policy-assignment "$assignment_id" --definition-reference-id deployAKSImageIntegrity --name remediation --resource-group ${RESOURCE_GROUP}
```


## Set up verification configurations

For Image Integrity to properly verify the target signed image, you need to set up `Ratify`

configurations through K8s [CRDs](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/#customresourcedefinitions) using `kubectl`

.

In this article, we use a self-signed CA cert from the official Ratify documentation to set up verification configurations. For more examples, see [Ratify CRDs](https://ratify.dev/docs/1.0/ratify-configuration).

Create a

`VerifyConfig`

file named`verify-config.yaml`

and copy in the following YAML:`apiVersion: config.ratify.deislabs.io/v1beta1 kind: KeyManagementProvider metadata: name: certstore-inline spec: provider: inline parameters: value: | -----BEGIN CERTIFICATE----- MIIDQzCCAiugAwIBAgIUDxHQ9JxxmnrLWTA5rAtIZCzY8mMwDQYJKoZIhvcNAQEL BQAwKTEPMA0GA1UECgwGUmF0aWZ5MRYwFAYDVQQDDA1SYXRpZnkgU2FtcGxlMB4X DTIzMDYyOTA1MjgzMloXDTMzMDYyNjA1MjgzMlowKTEPMA0GA1UECgwGUmF0aWZ5 MRYwFAYDVQQDDA1SYXRpZnkgU2FtcGxlMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A MIIBCgKCAQEAshmsL2VM9ojhgTVUUuEsZro9jfI27VKZJ4naWSHJihmOki7IoZS8 3/3ATpkE1lGbduJ77M9UxQbEW1PnESB0bWtMQtjIbser3mFCn15yz4nBXiTIu/K4 FYv6HVdc6/cds3jgfEFNw/8RVMBUGNUiSEWa1lV1zDM2v/8GekUr6SNvMyqtY8oo ItwxfUvlhgMNlLgd96mVnnPVLmPkCmXFN9iBMhSce6sn6P9oDIB+pr1ZpE4F5bwa gRBg2tWN3Tz9H/z2a51Xbn7hCT5OLBRlkorHJl2HKKRoXz1hBgR8xOL+zRySH9Qo 3yx6WvluYDNfVbCREzKJf9fFiQeVe0EJOwIDAQABo2MwYTAdBgNVHQ4EFgQUKzci EKCDwPBn4I1YZ+sDdnxEir4wHwYDVR0jBBgwFoAUKzciEKCDwPBn4I1YZ+sDdnxE ir4wDwYDVR0TAQH/BAUwAwEB/zAOBgNVHQ8BAf8EBAMCAgQwDQYJKoZIhvcNAQEL BQADggEBAGh6duwc1MvV+PUYvIkDfgj158KtYX+bv4PmcV/aemQUoArqM1ECYFjt BlBVmTRJA0lijU5I0oZje80zW7P8M8pra0BM6x3cPnh/oZGrsuMizd4h5b5TnwuJ hRvKFFUVeHn9kORbyQwRQ5SpL8cRGyYp+T6ncEmo0jdIOM5dgfdhwHgb+i3TejcF 90sUs65zovUjv1wa11SqOdu12cCj/MYp+H8j2lpaLL2t0cbFJlBY6DNJgxr5qync cz8gbXrZmNbzC7W5QK5J7fcx6tlffOpt5cm427f9NiK2tira50HU7gC3HJkbiSTp Xw10iXXMZzSbQ0/Hj2BF4B40WfAkgRg= -----END CERTIFICATE----- --- apiVersion: config.ratify.deislabs.io/v1beta1 kind: Store metadata: name: store-oras spec: name: oras # If you want to you use Workload Identity for Ratify to access Azure Container Registry, # uncomment the following lines, and fill the proper ClientID: # See more: https://ratify.dev/docs/reference/oras-auth-provider # parameters: # authProvider: # name: azureWorkloadIdentity # clientID: XXX --- apiVersion: config.ratify.deislabs.io/v1beta1 kind: Verifier metadata: name: verifier-notary-inline spec: name: notation artifactTypes: application/vnd.cncf.notary.signature parameters: verificationCertStores: # certificates for validating signatures certs: # name of the trustStore - certstore-inline # name of the certificate store CRD to include in this trustStore trustPolicyDoc: # policy language that indicates which identities are trusted to produce artifacts version: "1.0" trustPolicies: - name: default registryScopes: - "*" signatureVerification: level: strict trustStores: - ca:certs trustedIdentities: - "*"`

Apply the

`VerifyConfig`

to your cluster using the`kubectl apply`

command.`kubectl apply -f verify-config.yaml`


## Deploy sample images to your AKS cluster

Deploy a signed image using the

`kubectl run demo`

command.`kubectl run demo-signed --image=ghcr.io/deislabs/ratify/notary-image:signed`

The following example output shows that Image Integrity allows the deployment:

`ghcr.io/deislabs/ratify/notary-image:signed pod/demo-signed created`


If you want to use your own images, see the [guidance for image signing](/en-us/azure/container-registry/container-registry-tutorial-sign-build-push).

## Disable Image Integrity

### Remove policy initiative

First you should remove the policy initiative using the

command.`az policy assignment delete`

`az policy assignment delete --name 'deploy-trustedimages'`


### Diable add-on

Then disable Image Integrity add-on on your cluster using the

command with the`az aks update`

`--disable-image-integrity`

flag.`az aks update --resource-group myResourceGroup --name MyManagedCluster --disable-image-integrity`


## Next steps

In this article, you learned how to use Image Integrity to validate signed images before deploying them to your Azure Kubernetes Service (AKS) clusters. If you want to learn how to sign your own containers, see [Build, sign, and verify container images using Notary and Azure Key Vault (Preview)](/en-us/azure/container-registry/container-registry-tutorial-sign-build-push).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kueue-overview -->

# Install and Configure Kueue on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to install and configure Kueue to schedule batch workloads on an Azure Kubernetes Service (AKS) cluster. You also explore different Kueue concepts, installation methods to enable advanced Kueue features, and learn how to verify your deployments.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## What are batch workloads?

Batch deployments are typically non-interactive workloads that are retriable, have a finite duration, and might experience spiky or bursty resource usage. These workloads include, but aren't limited to:

- Data processing jobs.
- Security vulnerability scans.
- Media encoding or video transcoding.
- Report generation or financial analysis.
- GPU workloads that require all resources to be available and might tolerate a delayed start but can't tolerate partial GPU allocation.

These workloads are often modeled using a Kubernetes Job, CronJob, or custom resource definition (CRD) like [RayJob](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started/rayjob-quick-start.html) or [Kubeflow MPIJob](https://www.kubeflow.org/docs/components/trainer/legacy-v1/user-guides/mpi/). Batch deployments present the following set of distinct requirements from general purpose deployments:

- Scheduling logic beyond selecting the first available node.
- Fairness, queueing, and resource awareness.
- Lifecycle awareness of jobs and pods.

The default AKS scheduler satisfies the requirements of Kubernetes services but provides limited configuration for batch workloads that require a job queueing system.

## What is Kueue?

[Kueue](https://kueue.sigs.k8s.io/docs/overview/) is an open-source Kubernetes-native job queueing project designed to manage batch workloads and ensure efficient, fair, and policy-driven scheduling in Kubernetes clusters. Kueue integrates with the [Kubernetes scheduling](https://github.com/kubernetes/community/blob/master/sig-scheduling/README.md) ecosystem to coordinate resource allocation, prioritization, and capacity control for batch jobs.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

Kueue introduces a two-level queuing model:

- A
`ClusterQueue`

represents shared resource pools (such as CPU, memory, GPU quotas). - A
`LocalQueue`

represents a tenant-facing queue in a namespace (where users submit their batch jobs).

Workloads submitted to a `LocalQueue`

are matched to a `ClusterQueue`

to determine if they can be admitted.

Note

A `LocalQueue`

is always needed for users to submit batch workloads, and the `LocalQueue`

tells Kueue about which ClusterQueue to assign the job to. The `ClusterQueue`

determines if sufficient resources are available for the job to be admitted and run.

## Who can use Kueue?

Batch workload administrators (including platform or cluster administrators and DevOps engineers) and batch users (data scientists, developers, and ML engineers) can benefit from deploying workloads with Kueue on AKS.

A batch admin focuses on configuring, managing, and securing the platform-level infrastructure to support batch workloads, and have the following responsibilities:

- Provision and manage AKS node pools.
- Define resource quotas, ClusterQueues, and policies for workload isolation.
- Tune autoscaling and cost-efficiency (such as the Cluster Autoscaler or Kueue quotas).
- Monitor cluster and queue health.
- Create and maintain templates and reusable workflows.

A batch user runs compute-intensive or parallel jobs using the platform-level infrastructure configured by a batch admin, and typically:

- Submit batch jobs (such as Job, Workload, or custom controller CRDs) and monitor job status and outputs
- Select appropriate queue or resource flavor for jobs (based on guidance from batch admins)
- Optimize job specs for resource and performance needs

| Queue Type | Scope | Created By | Used For |
|---|---|---|---|
ClusterQueue |
Cluster-wide | Platform admin | Define shared compute capacity and quota management |
LocalQueue |
Namespace | Namespace owner | Enable workload submission, mapped to ClusterQueue |

## Prerequisites

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Azure CLI installed on your local machine. To install or upgrade, see
[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). [Helm version 3 or above](https://helm.sh/docs/intro/install/)installed.

## Install Kueue with Helm

While most features and scheduling policies that you might require are enabled by default, some aren't like `TopologyAwareScheduling`

. If needed, reconfigure your Kueue installation by changing the default [Feature Gates](https://kueue.sigs.k8s.io/docs/installation/#feature-gates-for-alpha-and-beta-features) or by configuring [Kueue paramater values](https://github.com/kubernetes-sigs/kueue/blob/main/charts/kueue/README.md#configuration) in the `values.yaml`

file of the Helm chart.

Kueue supports multiple workload [Frameworks](https://kueue.sigs.k8s.io/docs/tasks/run/) that you need to explicitly enable to use Kueue’s scheduling and resource management capabilities when running [MPI Operator](https://www.kubeflow.org/docs/components/training/mpi/) MPIJobs, [KubeRay's](https://github.com/ray-project/kuberay) [RayJob](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started/rayjob-quick-start.html) and more.

In this guide, Kueue is configured to include `LocalQueueMetrics`

and `Topology Aware Scheduling`

and frameworks from Kubeflow, Ray, and [JobSet](https://jobset.sigs.k8s.io/docs/concepts/).

`LocalQueueMetrics`

provides detailed Prometheus metrics specific to the state and activity of LocalQueues, enabling fine-grained monitoring of workload admission, quota reservation, and resource utilization.`TopologyAwareScheduling`

allows scheduling of pods based on the topology of nodes in a pool or cluster to improve available bandwidth between the pods.

Note

Update version as needed: [kueue/releases](https://github.com/kubernetes-sigs/kueue/releases)

Create and save a

`values.yaml`

file to optionally customize your Kueue configuration.`cat <<EOF > values.yaml controllerManager: featureGates: - name: TopologyAwareScheduling enabled: true - name: LocalQueueMetrics enabled: true managerConfig: controllerManagerConfigYaml: | apiVersion: config.kueue.x-k8s.io/v1beta1 kind: Configuration integrations: frameworks: - batch/job - kubeflow.org/mpijob - ray.io/rayjob - ray.io/raycluster - jobset.x-k8s.io/jobset - kubeflow.org/paddlejob - kubeflow.org/pytorchjob - kubeflow.org/tfjob - kubeflow.org/xgboostjob - kubeflow.org/jaxjob EOF`

Install the latest version of the Kueue controller and CRDs in a dedicated namespace using the

`helm install`

command.`LATEST_VERSION=$(curl -s https://api.github.com/repos/kubernetes-sigs/kueue/releases/latest | grep tag_name | cut -d '"' -f 4 | sed 's/^v//') helm install kueue oci://registry.k8s.io/kueue/charts/kueue \ --version=${LATEST_VERSION} \ --create-namespace --namespace=kueue-system \ --values values.yaml`

Confirm the deployment status using the

`helm list`

command.`helm list --namespace kueue-system`

Your output should include a

`Status`

of`deployed`

and look like:`Pulled: registry.k8s.io/kueue/charts/kueue:0.13.4 Digest: - NAME: kueue LAST DEPLOYED: - NAMESPACE: kueue-system STATUS: deployed REVISION: 1 TEST SUITE: None`


## Confirm deployment status

Verify that controller pods are running properly.

`kubectl get deploy -n kueue-system`

Your output should look similar to the following example output:

`NAME READY UP-TO-DATE AVAILABLE AGE kueue-controller-manager 1/1 1 1 7s`

Confirm the installation of Kueue resources on your AKS cluster:

`kubectl get crds | grep kueue`

Your output should include the following Kueue CRDs:

`admissionchecks.kueue.x-k8s.io 2025-09-11T18:20:48Z clusterqueues.kueue.x-k8s.io 2025-09-11T18:20:48Z cohorts.kueue.x-k8s.io 2025-09-11T18:20:48Z localqueues.kueue.x-k8s.io 2025-09-11T18:20:48Z multikueueclusters.kueue.x-k8s.io 2025-09-11T18:20:48Z multikueueconfigs.kueue.x-k8s.io 2025-09-11T18:20:48Z provisioningrequestconfigs.kueue.x-k8s.io 2025-09-11T18:20:48Z resourceflavors.kueue.x-k8s.io 2025-09-11T18:20:48Z topologies.kueue.x-k8s.io 2025-09-11T18:20:48Z workloadpriorityclasses.kueue.x-k8s.io 2025-09-11T18:20:48Z workloads.kueue.x-k8s.io 2025-09-11T18:20:48Z`


## Uninstall Kueue

If you no longer need to use the Kueue controller manager or Kueue custom resources in your AKS cluster, you can uninstall the Helm repository and remove the dedicated namespace and resources.

Uninstall the Kueue Helm repository using the

`helm uninstall`

command.`helm uninstall kueue --namespace kueue-system`

Remove the dedicated namespace and resources using the

`kubectl delete`

command.`kubectl delete namespace kueue-system`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/core-aks-concepts -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-configuration -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-clusters-workloads -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/create-nginx-ingress-private-controller -->

# Configure NGINX ingress controller to support Azure private DNS zone with application routing add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure an NGINX ingress controller to work with an Azure internal load balancer. It also explains how to configure a private Azure DNS zone to enable DNS resolution for the private endpoints to resolve specific domains.

## Before you begin

An AKS cluster with the

[application routing add-on](app-routing).To attach an Azure private DNS Zone, you need the

[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner),[Azure account administrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles), or[Azure coadministrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles)role on your Azure subscription.

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use `kubectl`

, the Kubernetes command-line client. You can install it locally using the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell, `kubectl`

is already installed.

The following example configures connecting to your cluster named *aks-cluster* in the *test-rg* using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials \
--resource-group test-rg \
--name aks-cluster
```


## Create a virtual network

To publish a private DNS zone to your virtual network, specify a list of virtual networks that are allowed to resolve records within the zone with [virtual network links](/en-us/azure/dns/private-dns-virtual-network-links).

The following example creates a virtual network named *vnet-1* in the *test-rg* resource group, and one subnet named *subnet-1* to create within the virtual network with a specific address prefix.

```
az network vnet create \
--name vnet-1 \
--resource-group test-rg \
--location eastus \
--address-prefix 10.2.0.0/16 \
--subnet-name subnet-1 \
--subnet-prefixes 10.2.0.0/24
```


## Create an Azure private DNS zone

Note

You can configure the application routing add-on to automatically create records on one or more Azure global and private DNS zones for hosts defined on ingress resources. All global Azure DNS zones and all private Azure DNS zones must be in the same resource group.

Create a DNS zone using the [az network private-dns zone create](/en-us/cli/azure/network/private-dns/zone?#az-network-private-dns-zone-create) command, specifying the name of the zone and the resource group to create it in. The following example creates a DNS zone named *private.contoso.com* in the *test-rg* resource group.

```
az network private-dns zone create \
--resource-group test-rg \
--name private.contoso.com
```


You create a virtual network link to the DNS zone created earlier using the [az network private-dns link vnet create](/en-us/cli/azure/network/private-dns/link/vnet#az-network-private-dns-link-vnet-create) command. The following example creates a link named *dns-link* to the zone *private.contoso.com* for the virtual network *vnet-1*. Include the `--registration-enabled`

parameter to specify the link isn't registration enabled.

```
az network private-dns link vnet create \
--resource-group test-rg \
--name dns-link \
--zone-name private.contoso.com \
--virtual-network vnet-1 \
--registration-enabled false
```


The Azure DNS private zone auto registration feature manages DNS records for virtual machines deployed in a virtual network. When you link a virtual network with a private DNS zone with this setting enabled, a DNS record gets created for each Azure virtual machine for your AKS node deployed in the virtual network.

## Attach an Azure private DNS zone to the application routing add-on

Note

The `az aks approuting zone add`

command uses the permissions of the user running the command to create the [Azure DNS Zone](/en-us/azure/dns/dns-protect-private-zones-recordsets) role assignment. The **Private DNS Zone Contributor** role is a built-in role for managing private DNS resources and is assigned to the add-on's managed identity. For more information on AKS managed identities, see [Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

Retrieve the resource ID for the DNS zone using the

command and set the output to a variable named`az network dns zone show`

`ZONEID`

. The following example queries the zone*private.contoso.com*in the resource group*test-rg*.`ZONEID=$(az network private-dns zone show \ --resource-group test-rg \ --name private.contoso.com \ --query "id" \ --output tsv)`

Update the add-on to enable integration with Azure DNS using the

command. You can pass a comma-separated list of DNS zone resource IDs. The following example updates the AKS cluster`az aks approuting zone`

*aks-cluster*in the resource group*test-rg*.`az aks approuting zone add \ --resource-group test-rg \ --name aks-cluster \ --ids=${ZONEID} \ --attach-zones`


## Create an NGINX ingress controller with a private IP address and an internal load balancer

The application routing add-on uses a Kubernetes [custom resource definition (CRD)](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) called [ NginxIngressController](https://aka.ms/aks/approuting/nginxingresscontrollercrd) to configure NGINX ingress controllers. You can create more ingress controllers or modify an existing configuration.

`NginxIngressController`

CRD has a `loadBalancerAnnotations`

field to control the behavior of the NGINX ingress controller's service by setting load balancer annotations. For more information about load balancer annotations, see [Customizations via Kubernetes annotations](configure-load-balancer-standard#customizations-via-kubernetes-annotations).

Perform the following steps to create an NGINX ingress controller with an internal facing Azure Load Balancer with a private IP address.

Copy the following YAML manifest into a new file named

**nginx-internal-controller.yaml**and save the file to your local computer.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-internal spec: ingressClassName: nginx-internal controllerNamePrefix: nginx-internal loadBalancerAnnotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true"`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-internal-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-internal created`

Verify the ingress controller was created

You can verify the status of the NGINX ingress controller using the

command.`kubectl get nginxingresscontroller`

`kubectl get nginxingresscontroller`

The following example output shows the created resource. It might take a few minutes for the controller to be available:

`NAME INGRESSCLASS CONTROLLERNAMEPREFIX AVAILABLE default webapprouting.kubernetes.azure.com nginx True nginx-internal nginx-internal nginx-internal True`


## Deploy an application

The application routing add-on uses annotations on Kubernetes Ingress objects to create the appropriate resources.

Create the application namespace called

`aks-store`

to run the example pods using the`kubectl create namespace`

command.`kubectl create namespace aks-store`

Deploy the AKS store application using the following YAML manifest file:

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/sample-manifests/docs/app-routing/aks-store-deployments-and-services.yaml -n aks-store`


This manifest creates the necessary deployments and services for the AKS store application.

## Create the Ingress resource that uses a host name on the Azure private DNS zone and a private IP address

Update ** host** with the name of your DNS host, for example,

**store-front.private.contoso.com**. Verify you're specifying nginx-internal for the ingressClassName.

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: store-front namespace: aks-store spec: ingressClassName: nginx-internal rules: - host: store-front.private.contoso.com http: paths: - backend: service: name: store-front port: number: 80 path: / pathType: Prefix`

Create the ingress resource using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n aks-store`

The following example output shows the created resource:

`ingress.networking.k8s.io/store-front created`


## Verify the managed Ingress was created

You can verify the managed Ingress was created using the [ kubectl get ingress](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.

```
kubectl get ingress -n aks-store
```


The following example output shows the created managed Ingress:

```
NAME CLASS HOSTS ADDRESS PORTS AGE
store-front nginx-internal store-front.private.contoso.com 80 10s
```


## Verify the Azure private DNS zone was updated

In a few minutes, run the [az network private-dns record-set a list](/en-us/cli/azure/network/private-dns/record-set/a#az-network-private-dns-record-set-a-list) command to view the A records for your Azure private DNS zone. Specify the name of the resource group and the name of the DNS zone. In this example, the resource group is *test-rg* and DNS zone is *private.contoso.com*.

```
az network private-dns record-set a list \
--resource-group test-rg \
--zone-name private.contoso.com
```


The following example output shows the created record:

```
[
{
"aRecords": [
{
"ipv4Address": "10.224.0.7"
}
],
"etag": "ecc303c5-4577-4ca2-b545-d34e160d1c2d",
"fqdn": "store-front.private.contoso.com.",
"id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/test-rg/providers/Microsoft.Network/privateDnsZones/private.contoso.com/A/store-front",
"isAutoRegistered": false,
"name": "store-front",
"resourceGroup": "test-rg",
"ttl": 300,
"type": "Microsoft.Network/privateDnsZones/A"
}
]
```


## Next steps

For other configuration information related to SSL encryption other advanced NGINX ingress controller and ingress resource configuration, review [DNS and SSL configuration](app-routing-dns-ssl) and [application routing add-on configuration](app-routing-nginx-configuration).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-terraform -->

# Quickstart: Create a Windows-based Azure Kubernetes Service (AKS) cluster using Terraform

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you create an Azure Kubernetes cluster with a Windows node pool using Terraform. Azure Kubernetes Service (AKS) is a managed container orchestration service provided by Azure. It simplifies the deployment, scaling, and operations of containerized applications. The service uses Kubernetes, an open-source system for automating the deployment, scaling, and management of containerized applications. The Windows node pool allows you to run Windows containers in your Kubernetes cluster.

[Terraform](https://www.terraform.io) enables the definition, preview, and deployment of cloud infrastructure. Using Terraform, you create configuration files using [HCL syntax](https://developer.hashicorp.com/terraform/language/syntax/configuration). The HCL syntax allows you to specify the cloud provider - such as Azure - and the elements that make up your cloud infrastructure. After you create your configuration files, you create an *execution plan* that allows you to preview your infrastructure changes before they're deployed. Once you verify the changes, you apply the execution plan to deploy the infrastructure.

- Generate a random resource group name.
- Create an Azure resource group.
- Create an Azure virtual network.
- Create an Azure Kubernetes cluster.
- Create an Azure Kubernetes cluster node pool.

## Prerequisites

Create an Azure account with an active subscription. You can

[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Implement the Terraform code

Note

The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/101-aks-cluster-windows). You can view the log file containing the [test results from current and previous versions of Terraform](https://github.com/Azure/terraform/tree/master/quickstart/101-aks-cluster-windows/TestRecord.md).

See more [articles and sample code showing how to use Terraform to manage Azure resources](/en-us/azure/terraform)

Create a directory in which to test and run the sample Terraform code and make it the current directory.

Create a file named

`providers.tf`

and insert the following code.`terraform { required_version = ">= 1.0" required_providers { azurerm = { source = "hashicorp/azurerm" version = "~>3.0" } random = { source = "hashicorp/random" version = "~>3.0" } } } provider "azurerm" { features { } }`

Create a file named

`main.tf`

and insert the following code.`# Generate random resource group name resource "random_pet" "rg_name" { prefix = var.resource_group_name_prefix } resource "azurerm_resource_group" "rg" { location = var.resource_group_location name = random_pet.rg_name.id } resource "random_pet" "azurerm_kubernetes_cluster_name" { prefix = "cluster" } resource "random_pet" "azurerm_kubernetes_cluster_dns_prefix" { prefix = "dns" } resource "random_string" "azurerm_kubernetes_cluster_node_pool" { length = 6 special = false numeric = false lower = true upper = false } resource "azurerm_virtual_network" "vnet" { name = "myvnet" location = azurerm_resource_group.rg.location resource_group_name = azurerm_resource_group.rg.name address_space = ["10.1.0.0/16"] subnet { name = "subnet1" address_prefix = "10.1.1.0/24" } } resource "azurerm_kubernetes_cluster" "aks" { name = random_pet.azurerm_kubernetes_cluster_name.id location = azurerm_resource_group.rg.location resource_group_name = azurerm_resource_group.rg.name dns_prefix = random_pet.azurerm_kubernetes_cluster_dns_prefix.id identity { type = "SystemAssigned" } default_node_pool { name = "agentpool" vm_size = "Standard_D2_v2" node_count = var.node_count_linux vnet_subnet_id = element(tolist(azurerm_virtual_network.vnet.subnet), 0).id } windows_profile { admin_username = var.admin_username admin_password = var.admin_password } network_profile { network_plugin = "azure" load_balancer_sku = "standard" } } resource "azurerm_kubernetes_cluster_node_pool" "win" { name = random_string.azurerm_kubernetes_cluster_node_pool.result kubernetes_cluster_id = azurerm_kubernetes_cluster.aks.id vm_size = "Standard_D4s_v3" node_count = var.node_count_windows os_type = "Windows" }`

Create a file named

`variables.tf`

and insert the following code.`variable "resource_group_location" { type = string default = "eastus" description = "Location of the resource group." } variable "resource_group_name_prefix" { type = string default = "rg" description = "Prefix of the resource group name that's combined with a random ID so name is unique in your Azure subscription." } variable "node_count_linux" { type = number description = "The initial quantity of Linux nodes for the node pool." default = 1 } variable "node_count_windows" { type = number description = "The initial quantity of Windows nodes for the node pool." default = 1 } variable "admin_username" { type = string description = "The admin username for the Windows node pool." default = "azureuser" } variable "admin_password" { type = string description = "The admin password for the Windows node pool." default = "Passw0rd1234Us!" }`

Create a file named

`outputs.tf`

and insert the following code.`output "resource_group_name" { value = azurerm_resource_group.rg.name } output "kubernetes_cluster_name" { value = azurerm_kubernetes_cluster.aks.name } output "kubernetes_cluster_dns_prefix" { value = azurerm_kubernetes_cluster.aks.dns_prefix } output "kubernetes_cluster_node_pool_name" { value = azurerm_kubernetes_cluster_node_pool.win.name } output "kubernetes_cluster_kube_config_raw" { value = azurerm_kubernetes_cluster.aks.kube_config_raw sensitive = true }`


## Initialize Terraform

Run [terraform init](https://www.terraform.io/docs/commands/init.html) to initialize the Terraform deployment. This command downloads the Azure provider required to manage your Azure resources.

```
terraform init -upgrade
```


**Key points:**

- The
`-upgrade`

parameter upgrades the necessary provider plugins to the newest version that complies with the configuration's version constraints.

## Create a Terraform execution plan

Run [terraform plan](https://www.terraform.io/docs/commands/plan.html) to create an execution plan.

```
terraform plan -out main.tfplan
```


**Key points:**

- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

## Apply a Terraform execution plan

Run [terraform apply](https://www.terraform.io/docs/commands/apply.html) to apply the execution plan to your cloud infrastructure.

```
terraform apply main.tfplan
```


**Key points:**

- The example
`terraform apply`

command assumes you previously ran`terraform plan -out main.tfplan`

. - If you specified a different filename for the
`-out`

parameter, use that same filename in the call to`terraform apply`

. - If you didn't use the
`-out`

parameter, call`terraform apply`

without any parameters.

## Verify the results

Run [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) to print the cluster's nodes.

```
kubectl get node -o wide
```


## Clean up resources

When you no longer need the resources created via Terraform, do the following steps:

Run

[terraform plan](https://www.terraform.io/docs/commands/plan.html)and specify the`destroy`

flag.`terraform plan -destroy -out main.destroy.tfplan`

**Key points:**- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

- The
Run

[terraform apply](https://www.terraform.io/docs/commands/apply.html)to apply the execution plan.`terraform apply main.destroy.tfplan`


## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure](/en-us/azure/developer/terraform/troubleshoot).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-portal -->

# Deploy a Windows Server container on an Azure Kubernetes Service (AKS) cluster using the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this article, you deploy an AKS cluster that runs Windows Server containers using the Azure portal. You also deploy an ASP.NET sample application in a Windows Server container to the cluster.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - If you're unfamiliar with the Azure Cloud Shell, review
[Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview). - Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Create an AKS cluster

Sign in to the

[Azure portal](https://portal.azure.com).On the Azure portal home page, select

**Create a resource**.In the

**Categories**section, select**Containers**>**Azure Kubernetes Service (AKS)**.On the

**Basics**tab, configure the following settings:- Under
**Project details**:**Subscription**: Select the Azure subscription you want to use for this AKS cluster.**Resource group**: Select**Create new**, enter a resource group name, such as*myResourceGroup*, and then select**Ok**. While you can select an existing resource group, for testing or evaluation purposes, we recommend creating a resource group to temporarily host these resources and avoid impacting your production or development workloads.

- Under
**Cluster details**:**Cluster preset configuration**: Select**Dev/Test**. For more details on preset configurations, see[Cluster configuration presets in the Azure portal](../quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal).**Kubernetes cluster name**: Enter a cluster name, such as*myAKSCluster*.**Region**: Select a region, such as*East US 2*.**Availability zones**: Select**None**.**AKS pricing tier**: Select**Free**.Leave the default values for the remaining settings, and select

**Next**.


- Under
On the

**Node pools**tab, configure the following settings:Select

**Add node pool**and enter a**Node pool name**, such as*npwin*. For a Windows node pool, the name must be*six characters or fewer*.**Mode**: Select**User**.**OS SKU**: Select**Windows 2022**.**Availability zones**: Select**None**.Leave the

**Enable Azure Spot instances**checkbox unchecked.**Node size**: Select**Choose a size**. On the**Select a VM size**page, select**D2s_v3**, and then select**Select**.Leave the default values for the remaining settings, and select

**Add**.

Select

**Review + create**to run validation on the cluster configuration. After validation completes, select**Create**.It takes a few minutes to create the AKS cluster. When your deployment is complete, navigate to your resource by selecting

**Go to resource**, or by browsing to the AKS cluster resource group and selecting the AKS resource.

## Connect to the cluster

You use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client, to manage your Kubernetes clusters. `kubectl`

is already installed if you use Azure Cloud Shell. If you're unfamiliar with the Cloud Shell, review [Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview).

Open Cloud Shell by selecting the

`>_`

button at the top of the Azure portal page.Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. The following command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

`kubectl get nodes`

command, which returns a list of the cluster nodes.`kubectl get nodes`

The following sample output shows all the nodes in the cluster. Make sure the status of all nodes is

*Ready*:`NAME STATUS ROLES AGE VERSION aks-agentpool-11741175-vmss000000 Ready agent 8m17s v1.29.9 aks-agentpool-11741175-vmss000001 Ready agent 8m17s v1.29.9 aksnpwin000000 Ready agent 8m17s v1.29.9 aks-userpool-11741175-vmss000000 Ready agent 8m17s v1.29.9 aks-userpool-11741175-vmss000001 Ready agent 8m17s v1.29.9`


## Deploy the application

A Kubernetes manifest file defines a desired state for the cluster, such as which container images to run. In this quickstart, you use a manifest file to create all objects needed to run the ASP.NET sample application in a Windows Server container. This manifest file includes a [Kubernetes deployment](../concepts-clusters-workloads#deployments-and-yaml-manifests) for the ASP.NET sample application and an external [Kubernetes service](../concepts-network-services) to access the application from the internet.

The ASP.NET sample application is provided as part of the [.NET Framework Samples](https://hub.docker.com/_/microsoft-dotnet-framework-samples/) and runs in a Windows Server container. The Kubernetes manifest file must define a [node selector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) to tell your AKS cluster to run your ASP.NET sample application's pod on a node that can run Windows Server containers.

Create a file named

`sample.yaml`

and paste in the following YAML definition.`apiVersion: apps/v1 kind: Deployment metadata: name: sample labels: app: sample spec: replicas: 1 template: metadata: name: sample labels: app: sample spec: nodeSelector: "kubernetes.io/os": windows containers: - name: sample image: mcr.microsoft.com/dotnet/framework/samples:aspnetapp resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 selector: matchLabels: app: sample --- apiVersion: v1 kind: Service metadata: name: sample spec: type: LoadBalancer ports: - protocol: TCP port: 80 selector: app: sample`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f sample.yaml`

The following sample output shows the deployment and service created successfully:

`deployment.apps/sample created service/sample created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete. Occasionally, the service can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

Check the status of the deployed pods using the

command. Make all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service sample --watch`

Initially, the output shows the

*EXTERNAL-IP*for the sample service as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE sample LoadBalancer 10.0.37.27 <pending> 80:30572/TCP 6s`

When the

*EXTERNAL-IP*address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.See the sample app in action by opening a web browser to the external IP address of your service.


## Delete resources

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), you should delete your cluster to avoid incurring Azure charges.

In the Azure portal, navigate to your resource group.

Select

**Delete resource group**.Enter the name of your resource group to confirm deletion and select

**Delete**.In the

**Delete confirmation**dialog box, select**Delete**.Note

The AKS cluster was created with system-assigned managed identity (default identity option used in this quickstart), the identity is managed by the platform and does not require removal.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed an ASP.NET sample application in a Windows Server container to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS, and to walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-powershell -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using Azure PowerShell

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Deploy an AKS cluster using Azure PowerShell.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This article assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. For ease of use, try the PowerShell environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Quickstart for Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you want to use PowerShell locally, then install the

[Az PowerShell](/en-us/powershell/azure/new-azureps-module-az)module and connect to your Azure account using the[Connect-AzAccount](/en-us/powershell/module/az.accounts/Connect-AzAccount)cmdlet. Make sure that you run the commands with administrative privileges. For more information, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps).Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).If you have more than one Azure subscription, set the subscription that you wish to use for the quickstart by calling the

[Set-AzContext](/en-us/powershell/module/az.accounts/set-azcontext)cmdlet. For more information, see[Manage Azure subscriptions with Azure PowerShell](/en-us/powershell/azure/manage-subscriptions-azureps#change-the-active-subscription).

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the

cmdlet.`New-AzResourceGroup`

`New-AzResourceGroup -Name myResourceGroup -Location eastus`

The following example output resembles successful creation of the resource group:

`ResourceGroupName : myResourceGroup Location : eastus ProvisioningState : Succeeded Tags : ResourceId : /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup`


## Create AKS cluster

To create an AKS cluster, use the [ New-AzAksCluster](/en-us/powershell/module/az.aks/new-azakscluster) cmdlet. The following example creates a cluster named

*myAKSCluster*with one node and enables a system-assigned managed identity.

```
New-AzAksCluster -ResourceGroupName myResourceGroup `
-Name myAKSCluster `
-NodeCount 1 `
-EnableManagedIdentity `
-GenerateSshKey
```


After a few minutes, the command completes and returns information about the cluster.

Note

When you create an AKS cluster, a second resource group called the *node resource group* is automatically created to store the AKS resources. For more information, see [Node resource group](../core-aks-concepts#node-resource-group). When you [delete the resource group](#delete-resources) for the AKS cluster, the node resource group is also deleted. You also see a *NetworkWatcherRG* resource group created by default. This resource group is used by Azure Network Watcher to store monitoring data. You can safely ignore this resource group. For more information, see [Enable or disable Azure Network Watcher](/en-us/azure/network-watcher/network-watcher-create).

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, call the `Install-AzAksCliTool`

cmdlet.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecmdlet. This command downloads credentials and configures the Kubernetes CLI to use them.`Import-AzAksCredential`

`Import-AzAksCredential -ResourceGroupName myResourceGroup -Name myAKSCluster`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the single node created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-nodepool1-11853318-vmss000000 Ready agent 2m26s v1.27.7`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Create a file named

`aks-store-quickstart.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: rabbitmq spec: replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 resources: requests: cpu: 1m memory: 1Mi limits: cpu: 1m memory: 7Mi --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make all pods are`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete resources

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges. Remove the resource group, container service, and all related resources by calling the [ Remove-AzResourceGroup](/en-us/powershell/module/az.resources/remove-azresourcegroup) cmdlet.

```
Remove-AzResourceGroup -Name myResourceGroup
```


Note

The AKS cluster was created with system-assigned managed identity (default identity option used in this quickstart), the identity is managed by the platform and doesn't require removal.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-portal -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Deploy an AKS cluster using the Azure portal.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - If you're unfamiliar with the Azure Cloud Shell, review
[Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview). - Make sure that the identity you use to create your cluster has the appropriate minimum permissions. For more information about access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Create an AKS cluster

Sign in to the

[Azure portal](https://portal.azure.com).On the Azure portal home page, select

**Create a resource**.In the

**Categories**section, select**Infrastructure Services**>**Azure Kubernetes Service (AKS)**.On the

**Basics**tab, configure the following settings:Under

**Project details**:**Subscription**: Select the Azure subscription you want to use for this AKS cluster.**Resource group**: Select**Create new**, enter a resource group name, like*myResourceGroup*, and then select**Ok**. While you can select an existing resource group, for testing or evaluation purposes, we recommend creating a resource group to temporarily host these resources and avoid impacting your production or development workloads.

Under

**Cluster details**:**Cluster preset configuration**: Select**Dev/Test**. For more details about preset configurations, see[Cluster configuration presets in the Azure portal](../quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal). You can change the preset configuration when creating your cluster by selecting**Compare presets**and choosing a different option.


On the

**Node pools**tab, configure the following settings:Select

**Add node pool**and select**Add a Virtual Machine Scale Set node pool****Name**: Enter a name like*nplinux*.**Mode**: Select**User**.**OS SKU**: Select**Ubuntu Linux**.**Availability zones**: Select**None**.Leave the

**Enable Azure Spot instances**checkbox unchecked.**Node size**: Select**Choose a size**. On the**Select a VM size**page, search for**D2s_v5**, select that VM size, and**Select**.Use the default values for the remaining settings, and select

**Add**.

Select

**Review + create**to run validation on the cluster configuration. After validation completes, select**Create**.It takes a few minutes to create the AKS cluster. When your deployment is complete, navigate to your resource by selecting

**Go to resource**, or by browsing to the AKS cluster resource group and selecting the AKS resource.

## Connect to the cluster

You use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/), to manage Kubernetes clusters. `kubectl`

is already installed if you use Azure Cloud Shell. If you're unfamiliar with the Cloud Shell, review [Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview).

If you're using Cloud Shell, open it with the `>_`

button on the top of the Azure portal. If you're using PowerShell locally, connect to Azure via the `Connect-AzAccount`

command. If you're using Azure CLI locally, connect to Azure via the `az login`

command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using

`kubectl get`

to return a list of the cluster nodes.`kubectl get nodes`

The following example output shows the single node created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-nodepool1-31718369-0 Ready agent 6m44s v1.15.10`


## Deploy the application

You use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A Kubernetes manifest file defines a cluster's desired state, like which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, like Rabbit MQ, without persistent storage for production. These containers are used here for simplicity, but we recommend using managed services, like Azure Cosmos DB or Azure Service Bus.

In the Cloud Shell, open an editor and create a file named

`aks-store-quickstart.yaml`

.Paste the following manifest into the editor:

`apiVersion: apps/v1 kind: StatefulSet metadata: name: rabbitmq spec: serviceName: rabbitmq replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 env: - name: AI_SERVICE_URL value: "http://ai-service:5001/" resources: requests: cpu: 1m memory: 1Mi limits: cpu: 2m memory: 20Mi readinessProbe: httpGet: path: /health port: 3002 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3002 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi startupProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 5 periodSeconds: 5 readinessProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 3 livenessProbe: httpGet: path: /health port: 8080 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest:`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

command. Make sure all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the

`store-front`

application. Monitor progress using thecommand with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial series](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges.

In the Azure portal, navigate to your AKS cluster resource group.

Select

**Delete resource group**.Enter the name of the resource group to delete, and then select

**Delete**>**Delete**.Note

The AKS cluster was created with a system-assigned managed identity. This identity is managed by the platform and doesn't require removal.


## Next steps

In this quickstart, you deployed a Kubernetes cluster, and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial series.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you learn how to:

- Deploy an AKS cluster using the Azure CLI.
- Run a sample multi-container application with a group of microservices and web front ends that simulate a retail scenario.

Note

This article includes steps to deploy a cluster with default settings for evaluation purposes only. Before you deploy a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more information on access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
[az account set](/en-us/cli/azure/account#az-account-set)command. For more information, see[How to manage Azure subscriptions – Azure CLI](/en-us/cli/azure/manage-azure-subscriptions-azure-cli?tabs=bash#change-the-active-subscription). - Dependent upon your Azure subscription, you might need to request a vCPU quota increase. For more information, see
[Increase VM-family vCPU quotas](/en-us/azure/quotas/per-vm-quota-requests).

## Register resource providers

You might need to register resource providers in your Azure subscription. For example, `Microsoft.ContainerService`

is required.

Run the following command to check the registration status.

```
az provider show --namespace Microsoft.ContainerService --query registrationState
```


If necessary, register the resource provider.

```
az provider register --namespace Microsoft.ContainerService
```


## Define environment variables

Define the following environment variables for use throughout this quickstart.

```
export RANDOM_ID="$(openssl rand -hex 3)"
export MY_RESOURCE_GROUP_NAME="myAKSResourceGroup$RANDOM_ID"
export REGION="westus"
export MY_AKS_CLUSTER_NAME="myAKSCluster$RANDOM_ID"
export MY_DNS_LABEL="mydnslabel$RANDOM_ID"
```


The `RANDOM_ID`

variable's value is a six character alphanumeric value appended to the resource group and cluster name so that the names are unique. Use the `echo`

command to view variable values like `echo $RANDOM_ID`

.

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

Create a resource group using the [az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name $MY_RESOURCE_GROUP_NAME --location $REGION
```


The result looks like the following example.

```
{
"id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myAKSResourceGroup<randomIDValue>",
"location": "westus",
"managedBy": null,
"name": "myAKSResourceGroup<randomIDValue>",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


## Create an AKS cluster

Create an AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a cluster with one node and enables a system-assigned managed identity.

```
az aks create \
--resource-group $MY_RESOURCE_GROUP_NAME \
--name $MY_AKS_CLUSTER_NAME \
--node-count 1 \
--generate-ssh-keys
```


Note

When you create a new cluster, AKS automatically creates a second resource group to store the AKS resources. For more information, see [Why are two resource groups created with AKS?](../faq)

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, use the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials --resource-group $MY_RESOURCE_GROUP_NAME --name $MY_AKS_CLUSTER_NAME`

Verify the connection to your cluster using the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. This command returns a list of the cluster nodes.`kubectl get nodes`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A Kubernetes manifest file defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

- Store front: Web application for customers to view products and place orders.
- Product service: Shows product information.
- Order service: Places orders.
`RabbitMQ`

: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as `RabbitMQ`

, without persistent storage for production. We use it here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Create a file named

*aks-store-quickstart.yaml*and copy in the following manifest.`apiVersion: apps/v1 kind: StatefulSet metadata: name: rabbitmq spec: serviceName: rabbitmq replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 env: - name: AI_SERVICE_URL value: "http://ai-service:5001/" resources: requests: cpu: 1m memory: 1Mi limits: cpu: 2m memory: 20Mi readinessProbe: httpGet: path: /health port: 3002 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3002 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi startupProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 5 periodSeconds: 5 readinessProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 3 livenessProbe: httpGet: path: /health port: 8080 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in Cloud Shell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest.`kubectl apply -f aks-store-quickstart.yaml`


## Test the application

You can validate that the application is running by visiting the public IP address or the application URL.

Get the application URL using the following commands:

```
runtime="5 minutes"
endtime=$(date -ud "$runtime" +%s)
while [[ $(date -u +%s) -le $endtime ]]
do
STATUS=$(kubectl get pods -l app=store-front -o 'jsonpath={..status.conditions[?(@.type=="Ready")].status}')
echo $STATUS
if [ "$STATUS" == 'True' ]
then
export IP_ADDRESS=$(kubectl get service store-front --output 'jsonpath={..status.loadBalancer.ingress[0].ip}')
echo "Service IP Address: $IP_ADDRESS"
break
else
sleep 10
fi
done
```


```
curl $IP_ADDRESS
```


Results:

```
<!doctype html>
<html lang="">
<head>
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width,initial-scale=1">
<link rel="icon" href="/favicon.ico">
<title>store-front</title>
<script defer="defer" src="/js/chunk-vendors.df69ae47.js"></script>
<script defer="defer" src="/js/app.7e8cfbb2.js"></script>
<link href="/css/app.a5dc49f6.css" rel="stylesheet">
</head>
<body>
<div id="app"></div>
</body>
</html>
```


```
echo "You can now visit your web server at $IP_ADDRESS"
```


To view the application website, open a browser and enter the IP address. The page looks like the following example.

## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure billing charges. You can remove the resource group, container service, and all related resources using the [az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name $MY_RESOURCE_GROUP_NAME
```


The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance about how to create full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and do a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-flatcar-deploy-cli -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you learn how to:

- Create an AKS cluster using Flatcar Container Linux for AKS (preview).
- Deploy an AKS cluster using the Azure CLI.
- Run a sample multi-container application with a group of microservices and web front ends that simulate a retail scenario.

Note

This article includes steps to deploy a cluster with default settings for evaluation purposes only. Before you deploy a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more information on access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command. For more information, see`az account set`

[How to manage Azure subscriptions – Azure CLI](/en-us/cli/azure/manage-azure-subscriptions-azure-cli?tabs=bash#change-the-active-subscription). - Dependent upon your Azure subscription, you might need to request a vCPU quota increase. For more information, see
[Increase VM-family vCPU quotas](/en-us/azure/quotas/per-vm-quota-requests).

## Register resource providers

You might need to register resource providers in your Azure subscription. For example, `Microsoft.ContainerService`

is required.

Check the registration status using the [ az provider show](/en-us/cli/azure/provider#az-provider-show) command.

```
az provider show --namespace Microsoft.ContainerService --query registrationState
```


If necessary, register the resource provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command.

```
az provider register --namespace Microsoft.ContainerService
```


## Install `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Flatcar Container Linux requires a minimum of 18.0.0b42**.`az extension update --name aks-preview`


## Register `AKSFlatcarPreview`

feature flag

Register the

`AKSFlatcarPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AKSFlatcarPreview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AKSFlatcarPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Define environment variables

- Define the following environment variables for use throughout this quickstart:

```
export RANDOM_ID="$(openssl rand -hex 3)"
export MY_RESOURCE_GROUP_NAME="myAKSResourceGroup$RANDOM_ID"
export REGION="westus"
export MY_AKS_CLUSTER_NAME="myAKSCluster$RANDOM_ID"
```


The `RANDOM_ID`

variable's value is a six-character alphanumeric value appended to the resource group and cluster name so that the names are unique. Use the `echo`

command to view variable values like `echo $RANDOM_ID`

.

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

- Create a resource group using the
command.`az group create`


```
az group create \
--name $MY_RESOURCE_GROUP_NAME \
--location $REGION
```


Example output:

```
{
"id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myAKSResourceGroup<randomIDValue>",
"location": "westus",
"managedBy": null,
"name": "myAKSResourceGroup<randomIDValue>",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


## Create an AKS cluster

- Create an AKS cluster using the
command. The following example creates a cluster with one node and enables a system-assigned managed identity:`az aks create`


```
az aks create \
--resource-group $MY_RESOURCE_GROUP_NAME \
--name $MY_AKS_CLUSTER_NAME \
--os-sku flatcar \
--node-count 1 \
--generate-ssh-keys
```


Note

When you create a new cluster, AKS automatically creates a second resource group to store the AKS resources. For more information, see [Why are two resource groups created with AKS?](../faq)

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials \ --resource-group $MY_RESOURCE_GROUP_NAME \ --name $MY_AKS_CLUSTER_NAME`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A Kubernetes manifest file defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

- Store front: Web application for customers to view products and place orders.
- Product service: Shows product information.
- Order service: Places orders.
`RabbitMQ`

: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as `RabbitMQ`

, without persistent storage for production. We use it here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a file named

*aks-store-quickstart.yaml*and copy in the following manifest.`apiVersion: apps/v1 kind: StatefulSet metadata: name: rabbitmq spec: serviceName: rabbitmq replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 env: - name: AI_SERVICE_URL value: "http://ai-service:5001/" resources: requests: cpu: 1m memory: 1Mi limits: cpu: 2m memory: 20Mi readinessProbe: httpGet: path: /health port: 3002 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3002 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi startupProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 5 periodSeconds: 5 readinessProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 3 livenessProbe: httpGet: path: /health port: 8080 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in Cloud Shell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

command. Make sure all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the

`store-front`

application. Monitor progress using thecommand with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure billing charges.

Remove the resource group, container service, and all related resources using the

command.`az group delete`

`az group delete --name $MY_RESOURCE_GROUP_NAME`

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity so you don't need to manually remove it.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance about how to create full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and do a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-powershell -->

# Deploy a Windows Server container on an Azure Kubernetes Service (AKS) cluster using PowerShell

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this article, you use Azure PowerShell to deploy an AKS cluster that runs Windows Server containers. You also deploy an ASP.NET sample application in a Windows Server container to the cluster.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. For ease of use, try the PowerShell environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Quickstart for Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you want to use PowerShell locally, then install the

[Az PowerShell](/en-us/powershell/azure/new-azureps-module-az)module and connect to your Azure account using the[Connect-AzAccount](/en-us/powershell/module/az.accounts/Connect-AzAccount)cmdlet. Make sure that you run the commands with administrative privileges. For more information, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps).Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).If you have more than one Azure subscription, set the subscription that you wish to use for the quickstart by calling the

[Set-AzContext](/en-us/powershell/module/az.accounts/set-azcontext)cmdlet. For more information, see[Manage Azure subscriptions with Azure PowerShell](/en-us/powershell/azure/manage-subscriptions-azureps#change-the-active-subscription).If you're using osSku

`Windows2025`

, you need to install the`aks-preview`

extension and register the preview flag.Specifying the

`OsSKU`

parameter requires PowerShell Az module version 9.2.0 or higher.

### Install the `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

- Install the
`aks-preview`

Azure CLI extension using thecommand.`az extension add`


```
az extension add --name aks-preview
```


- Update to the latest version of the extension using the
command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b40**.

```
az extension update --name aks-preview
```


### Register the `AksWindows2025Preview`

feature flag

- Register the
`AksWindows2025Preview`

feature flag using the [`az feature register`

][az-feature-register] command.

```
az feature register --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


- Verify the registration status using the [
`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.

```
az feature show --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're asked to specify a location. This location is where resource group metadata is stored and where your resources run in Azure if you don't specify another region during resource creation.

Create a resource group using the

cmdlet. The following example creates a resource group named`New-AzResourceGroup`

*myResourceGroup*in the*eastus*region.`New-AzResourceGroup -Name myResourceGroup -Location eastus`

The following example output shows that the resource group was created successfully:

`ResourceGroupName : myResourceGroup Location : eastus ProvisioningState : Succeeded Tags : ResourceId : /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup`


## Create an AKS cluster

In this section, we create an AKS cluster with the following configuration:

- The cluster is configured with two nodes to ensure it operates reliably. A
[node](../concepts-clusters-workloads#nodes)is an Azure virtual machine (VM) that runs the Kubernetes node components and container runtime. - The
`-WindowsProfileAdminUserName`

and`-WindowsProfileAdminUserPassword`

parameters set the administrator credentials for any Windows Server nodes on the cluster and must meet the[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference). - The node pool uses
`VirtualMachineScaleSets`

.

Use the following steps to create the AKS cluster with Azure PowerShell:

Create the administrator credentials for your Windows Server containers using the following command. This command prompts you to enter a

`WindowsProfileAdminUserName`

and`WindowsProfileAdminUserPassword`

. The password must be a minimum of 14 characters and meet the[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).`$AdminCreds = Get-Credential ` -Message 'Please create the administrator credentials for your Windows Server containers'`

Create your cluster using the

cmdlet and specify the`New-AzAksCluster`

`WindowsProfileAdminUserName`

and`WindowsProfileAdminUserPassword`

parameters.`New-AzAksCluster -ResourceGroupName myResourceGroup ` -Name myAKSCluster ` -NodeCount 2 ` -NetworkPlugin azure ` -NodeVmSetType VirtualMachineScaleSets ` -WindowsProfileAdminUserName $AdminCreds.UserName ` -WindowsProfileAdminUserPassword $secureString ` -GenerateSshKey`

After a few minutes, the command completes and returns JSON-formatted information about the cluster. Occasionally, the cluster can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

If you get a password validation error, and the password that you set meets the length and complexity requirements, try creating your resource group in another region. Then try creating the cluster with the new resource group.

If you don't specify an administrator username and password when creating the node pool, the username is set to

*azureuser*and the password is set to a random value. For more information, see the[Windows Server FAQ](../windows-faq).The administrator username can't be changed, but you can change the administrator password that your AKS cluster uses for Windows Server nodes using

`az aks update`

. For more information, see the[Windows Server FAQ](../windows-faq).To run an AKS cluster that supports node pools for Windows Server containers, your cluster needs to use a network policy that uses

[Azure CNI (advanced)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md)network plugin. The`-NetworkPlugin azure`

parameter specifies Azure CNI.

## Add a node pool

By default, an AKS cluster is created with a node pool that can run Linux containers. You must add another node pool that can run Windows Server containers alongside the Linux node pool.

To create a Windows node pool, you need to specify a supported `OsType`

and `OsSku`

. Use the information in the following table to determine which is appropriate for your cluster:

`OsType` |
`OsSku` |
Default | Supported K8s versions | Details |
|---|---|---|---|---|
`windows` |
`Windows2025` |
Currently in preview. Not default. | 1.32+ | Updated defaults: containerd 2.0, Generation 2 image is used by default. |
`windows` |
`Windows2022` |
Default in K8s 1.25-1.35 | Not available in K8s 1.36+ | Retires in March 2027. Updated defaults: FIPS is enabled by default. |
`windows` |
`Windows2019` |
Default in K8s 1.24 and below | Not available in K8s 1.33+ | Retires in March 2026. |

Windows Server 2022 is the default operating system for Kubernetes versions 1.25-1.35. Windows Server 2019 is the default OS for earlier versions. If you don't specify a particular OS SKU, Azure creates the new node pool with the default SKU for the version of Kubernetes used by the cluster.

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Add a Windows Server node pool using the

cmdlet. The following command creates a new node pool named`New-AzAksNodePool`

*npwin*and adds it to*myAKSCluster*. The command also uses the default subnet in the default virtual network created when running`New-AzAksCluster`

:`New-AzAksNodePool -ResourceGroupName myResourceGroup ` -ClusterName myAKSCluster ` -VmSetType VirtualMachineScaleSets ` -OsType Windows ` -OsSKU Windows2022 ` -Name npwin`


## Connect to the cluster

You use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client, to manage your Kubernetes clusters. If you use Azure Cloud Shell, `kubectl`

is already installed. If you want to install `kubectl`

locally, you can use the `Install-AzAzAksCliTool`

cmdlet.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecmdlet. This command downloads credentials and configures the Kubernetes CLI to use them.`Import-AzAksCredential`

`Import-AzAksCredential -ResourceGroupName myResourceGroup -Name myAKSCluster`

Verify the connection to your cluster using the

command, which returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows all the nodes in the cluster. Make sure the status of all nodes is

**Ready**:`NAME STATUS ROLES AGE VERSION aks-nodepool1-20786768-vmss000000 Ready agent 22h v1.27.7 aks-nodepool1-20786768-vmss000001 Ready agent 22h v1.27.7 aksnpwin000000 Ready agent 21h v1.27.7`


## Deploy the application

A Kubernetes manifest file defines a desired state for the cluster, such as what container images to run. In this article, you use a manifest to create all objects needed to run the ASP.NET sample application in a Windows Server container. This manifest includes a [Kubernetes deployment](../concepts-clusters-workloads#deployments-and-yaml-manifests) for the ASP.NET sample application and an external [Kubernetes service](../concepts-network-services) to access the application from the internet.

The ASP.NET sample application is provided as part of the [.NET Framework Samples](https://hub.docker.com/_/microsoft-dotnet-framework-samples/) and runs in a Windows Server container. AKS requires Windows Server containers to be based on images of *Windows Server 2019* or greater. The Kubernetes manifest file must also define a [node selector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) to tell your AKS cluster to run your ASP.NET sample application's pod on a node that can run Windows Server containers.

Create a file named

`sample.yaml`

and copy in the following YAML definition:`apiVersion: apps/v1 kind: Deployment metadata: name: sample labels: app: sample spec: replicas: 1 template: metadata: name: sample labels: app: sample spec: nodeSelector: "kubernetes.io/os": windows containers: - name: sample image: mcr.microsoft.com/dotnet/framework/samples:aspnetapp resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 selector: matchLabels: app: sample --- apiVersion: v1 kind: Service metadata: name: sample spec: type: LoadBalancer ports: - protocol: TCP port: 80 selector: app: sample`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f sample.yaml`

The following example output shows the deployment and service created successfully:

`deployment.apps/sample created service/sample created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete. Occasionally, the service can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

Check the status of the deployed pods using the

command. Make all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service sample --watch`

Initially, the output shows the

*EXTERNAL-IP*for the sample service as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE sample LoadBalancer 10.0.37.27 <pending> 80:30572/TCP 6s`

When the

*EXTERNAL-IP*address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`sample LoadBalancer 10.0.37.27 52.179.23.131 80:30572/TCP 2m`

See the sample app in action by opening a web browser to the external IP address of your service.


## Delete resources

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), then delete your cluster to avoid incurring Azure charges.

Remove the resource group, container service, and all related resources using the

cmdlet.`Remove-AzResourceGroup`

`Remove-AzResourceGroup -Name myResourceGroup`

Note

The AKS cluster was created with system-assigned managed identity (default identity option used in this quickstart). The Azure platform manages this identity, so it doesn't require removal.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed an ASP.NET sample application in a Windows Server container to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS, and to walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Deploy an AKS cluster using an Azure Resource Manager template.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

An [Azure Resource Manager template](/en-us/azure/azure-resource-manager/templates/overview) is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This article assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. Make sure that the identity you use to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine, you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

After you deploy the cluster from the template, you can use either Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


This article requires Azure CLI version 2.0.64 or later. If you're using Azure Cloud Shell, the latest version is already installed there.

### Create an SSH key pair

To create an AKS cluster using an ARM template, you provide an SSH public key. If you need this resource, follow the steps in this section. Otherwise, skip to the [Review the template](#review-the-template) section.

To access AKS nodes, you connect using an SSH key pair (public and private). To create an SSH key pair:

Go to

[https://shell.azure.com](https://shell.azure.com)to open Cloud Shell in your browser.Create an SSH key pair using the

[az sshkey create](/en-us/cli/azure/sshkey#az-sshkey-create)command or the`ssh-keygen`

command.`# Create an SSH key pair using Azure CLI az sshkey create --name "mySSHKey" --resource-group "myResourceGroup" # or # Create an SSH key pair using ssh-keygen ssh-keygen -t rsa -b 4096`

To deploy the template, you must provide the public key from the SSH pair. To retrieve the public key, call

[az sshkey show](/en-us/cli/azure/sshkey#az-sshkey-show):`az sshkey show --name "mySSHKey" --resource-group "myResourceGroup" --query "publicKey"`


By default, the SSH key files are created in the *~/.ssh* directory. Running the `az sshkey create`

or `ssh-keygen`

command will overwrite any existing SSH key pair with the same name.

For more information about creating SSH keys, see [Create and manage SSH keys for authentication in Azure](/en-us/azure/virtual-machines/linux/create-ssh-keys-detailed).

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/aks/).

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"metadata": {
"_generator": {
"name": "bicep",
"version": "0.26.170.59819",
"templateHash": "14823542069333410776"
}
},
"parameters": {
"clusterName": {
"type": "string",
"defaultValue": "aks101cluster",
"metadata": {
"description": "The name of the Managed Cluster resource."
}
},
"location": {
"type": "string",
"defaultValue": "[resourceGroup().location]",
"metadata": {
"description": "The location of the Managed Cluster resource."
}
},
"dnsPrefix": {
"type": "string",
"metadata": {
"description": "Optional DNS prefix to use with hosted Kubernetes API server FQDN."
}
},
"osDiskSizeGB": {
"type": "int",
"defaultValue": 0,
"minValue": 0,
"maxValue": 1023,
"metadata": {
"description": "Disk size (in GB) to provision for each of the agent pool nodes. This value ranges from 0 to 1023. Specifying 0 will apply the default disk size for that agentVMSize."
}
},
"agentCount": {
"type": "int",
"defaultValue": 3,
"minValue": 1,
"maxValue": 50,
"metadata": {
"description": "The number of nodes for the cluster."
}
},
"agentVMSize": {
"type": "string",
"defaultValue": "standard_d2s_v3",
"metadata": {
"description": "The size of the Virtual Machine."
}
},
"linuxAdminUsername": {
"type": "string",
"metadata": {
"description": "User name for the Linux Virtual Machines."
}
},
"sshRSAPublicKey": {
"type": "string",
"metadata": {
"description": "Configure all linux machines with the SSH RSA public key string. Your key should include three parts, for example 'ssh-rsa AAAAB...snip...UcyupgH azureuser@linuxvm'"
}
}
},
"resources": [
{
"type": "Microsoft.ContainerService/managedClusters",
"apiVersion": "2024-02-01",
"name": "[parameters('clusterName')]",
"location": "[parameters('location')]",
"identity": {
"type": "SystemAssigned"
},
"properties": {
"dnsPrefix": "[parameters('dnsPrefix')]",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": "[parameters('osDiskSizeGB')]",
"count": "[parameters('agentCount')]",
"vmSize": "[parameters('agentVMSize')]",
"osType": "Linux",
"mode": "System"
}
],
"linuxProfile": {
"adminUsername": "[parameters('linuxAdminUsername')]",
"ssh": {
"publicKeys": [
{
"keyData": "[parameters('sshRSAPublicKey')]"
}
]
}
}
}
}
],
"outputs": {
"controlPlaneFQDN": {
"type": "string",
"value": "[reference(resourceId('Microsoft.ContainerService/managedClusters', parameters('clusterName')), '2024-02-01').fqdn]"
}
}
}
```


The resource type defined in the ARM template is [ Microsoft.ContainerService/managedClusters](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template).

For more AKS samples, see the [AKS quickstart templates](https://azure.microsoft.com/resources/templates/?term=Azure+Kubernetes+Service) site.

## Deploy the template

Select

**Deploy to Azure**to sign in and open a template.On the

**Basics**page, leave the default values for the*OS Disk Size GB*,*Agent Count*,*Agent VM Size*, and*OS Type*, and configure the following template parameters:**Subscription**: Select an Azure subscription.**Resource group**: Select**Create new**. Enter a unique name for the resource group, such as*myResourceGroup*, then select**OK**.**Location**: Select a location, such as**East US**.**Cluster name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**DNS prefix**: Enter a unique DNS prefix for your cluster, such as*myakscluster*.**Linux Admin Username**: Enter a username to connect using SSH, such as*azureuser*.**SSH public key source**: Select**Use existing public key**.**Key pair name**: Copy and paste the*public*part of your SSH key pair (by default, the contents of*~/.ssh/id_rsa.pub*).

Select

**Review + Create**>**Create**.

It takes a few minutes to create the AKS cluster. Wait for the cluster to be successfully deployed before you move on to the next step.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/).

If you use Azure Cloud Shell, `kubectl`

is already installed. To install and run `kubectl`

locally, call the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. This command returns a list of the cluster nodes.`kubectl get nodes`

The following example output shows the three nodes created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-agentpool-27442051-vmss000000 Ready agent 10m v1.27.7 aks-agentpool-27442051-vmss000001 Ready agent 10m v1.27.7 aks-agentpool-27442051-vmss000002 Ready agent 11m v1.27.7`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Create a file named

`aks-store-quickstart.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: rabbitmq spec: replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 resources: requests: cpu: 1m memory: 1Mi limits: cpu: 1m memory: 7Mi --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make all pods are`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges.

Remove the resource group, container service, and all related resources by calling the [az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name myResourceGroup --yes --no-wait
```


Note

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-cli -->

# Deploy a Windows Server container on an Azure Kubernetes Service (AKS) cluster using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this article, you use Azure CLI to deploy an AKS cluster that runs Windows Server containers. You also deploy an ASP.NET sample application in a Windows Server container to the cluster.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.0.64 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more information about access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command. For more information, see`az account set`

[How to manage Azure subscriptions – Azure CLI](/en-us/cli/azure/manage-azure-subscriptions-azure-cli?tabs=bash#change-the-active-subscription). - If you're using
`--os-sku Windows2025`

, you need to install the`aks-preview`

extension and register the preview flag. The minimum version is 18.0.0b40.

### Install the `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

- Install the
`aks-preview`

Azure CLI extension using thecommand.`az extension add`


```
az extension add --name aks-preview
```


- Update to the latest version of the extension using the
command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b40**.

```
az extension update --name aks-preview
```


### Register the `AksWindows2025Preview`

feature flag

- Register the
`AksWindows2025Preview`

feature flag using the [`az feature register`

][az-feature-register] command.

```
az feature register --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


- Verify the registration status using the [
`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.

```
az feature show --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're asked to specify a location. This location is where resource group metadata is stored and where your resources run in Azure if you don't specify another region during resource creation.

Create a resource group using the

command. The following example creates a resource group named`az group create`

*myResourceGroup*in the*WestUS2*location.`export RANDOM_SUFFIX=$(openssl rand -hex 3) export REGION="canadacentral" export MY_RESOURCE_GROUP_NAME="myAKSResourceGroup$RANDOM_SUFFIX" az group create --name $MY_RESOURCE_GROUP_NAME --location $REGION`

Results:

`{ "id": "/subscriptions/xxxxx-xxxxx-xxxxx-xxxxx/resourceGroups/myResourceGroupxxxxx", "location": "WestUS2", "managedBy": null, "name": "myResourceGroupxxxxx", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`


## Create an AKS cluster

In this section, we create an AKS cluster with the following configuration:

- The cluster is configured with two nodes to ensure it operates reliably. A
[node](../concepts-clusters-workloads#nodes)is an Azure virtual machine (VM) that runs the Kubernetes node components and container runtime. - The
`--windows-admin-password`

and`--windows-admin-username`

parameters set the administrator credentials for any Windows Server nodes on the cluster and must meet[Windows Server password requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference). - The node pool uses
`VirtualMachineScaleSets`

.

Use the following steps to create the AKS cluster with Azure CLI:

Create a username to use as administrator credentials for the Windows Server nodes on your cluster.

`export WINDOWS_USERNAME="winadmin"`

Create a password for the administrator username you created in the previous step. The password must be a minimum of 14 characters and meet the

[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).`export WINDOWS_PASSWORD=$(echo "P@ssw0rd$(openssl rand -base64 10 | tr -dc 'A-Za-z0-9!@#$%^&*()' | cut -c1-6)")`

Create your cluster using the

command and specify the`az aks create`

`--windows-admin-username`

and`--windows-admin-password`

parameters. The following example command creates a cluster using the values from`WINDOWS_USERNAME`

and`WINDOWS_PASSWORD`

you set in the previous commands. A random suffix is appended to the cluster name for uniqueness.`export MY_AKS_CLUSTER="myAKSCluster$RANDOM_SUFFIX" az aks create \ --resource-group $MY_RESOURCE_GROUP_NAME \ --name $MY_AKS_CLUSTER \ --node-count 2 \ --enable-addons monitoring \ --generate-ssh-keys \ --windows-admin-username $WINDOWS_USERNAME \ --windows-admin-password $WINDOWS_PASSWORD \ --vm-set-type VirtualMachineScaleSets \ --network-plugin azure`

After a few minutes, the command completes and returns JSON-formatted information about the cluster. Occasionally, the cluster can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

If you get a password validation error, and the password that you set meets the length and complexity requirements, try creating your resource group in another region. Then try creating the cluster with the new resource group.

If you don't specify an administrator username and password when creating the node pool, the username is set to

*azureuser*and the password is set to a random value. For more information, see the[Windows Server FAQ](../windows-faq)You can't change the administrator username, but you can change the administrator password that your AKS cluster uses for Windows Server nodes using

`az aks update`

. For more information, see[Windows Server FAQ](../windows-faq).To run an AKS cluster that supports node pools for Windows Server containers, your cluster needs to use a network policy that uses

[Azure CNI (advanced)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md)network plugin. The`--network-plugin azure`

parameter specifies Azure CNI.

## Add a node pool

By default, all AKS clusters are created with a node pool that can run Linux containers. You must add a Windows node pool that can run Windows Server containers alongside the Linux node pool. To check if you have a Windows node pool in your cluster, you can view the nodes on your cluster using the `kubectl get nodes -o wide`

command.

To create a Windows node pool, you need to specify a supported `OsType`

and `OsSku`

. Use the information in the following table to determine which is appropriate for your cluster:

`OsType` |
`OsSku` |
Default | Supported K8s versions | Details |
|---|---|---|---|---|
`windows` |
`Windows2025` |
Currently in preview. Not default. | 1.32+ | Updated defaults: `containerd` 2.0, Generation 2 image is used by default. |
`windows` |
`Windows2022` |
Default in K8s 1.25-1.35 | Not available in K8s 1.36+ | Retires in March 2027. Updated defaults: FIPS is enabled by default. |
`windows` |
`Windows2019` |
Default in K8s 1.24 and below | Not available in K8s 1.33+ | Retires in March 2026. |

Windows Server 2022 is the default operating system for Kubernetes versions 1.25-1.35. Windows Server 2019 is the default OS for earlier versions. If you don't specify a particular OS SKU, Azure creates the new node pool with the default SKU for the version of Kubernetes used by the cluster.

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Add a Windows node pool using the

command with a specified`az aks nodepool add`

`OsType`

and`OsSku`

. If you don't specify a particular OS SKU, Azure creates the new node pool with the default SKU for the version of Kubernetes used by the cluster.`az aks nodepool add \ --resource-group $MY_RESOURCE_GROUP_NAME \ --cluster-name $MY_AKS_CLUSTER \ --os-type Windows \ --os-sku Windows2022 \ --name npwin \ --node-count 1`

This command creates a new node pool named

*npwin*and adds it to*myAKSCluster*. The command also uses the default subnet in the default virtual network created when running`az aks create`

.

## Connect to the cluster

You use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client, to manage your Kubernetes clusters. If you use Azure Cloud Shell, `kubectl`

is already installed. If you want to install and run `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group $MY_RESOURCE_GROUP_NAME --name $MY_AKS_CLUSTER`

Verify the connection to your cluster using the

command, which returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes -o wide`

The following example output shows all nodes in the cluster. Make sure the status of all nodes is

*Ready*:`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME aks-nodepool1-20786768-vmss000000 Ready agent 22h v1.27.7 10.224.0.4 <none> Ubuntu 22.04.3 LTS 5.15.0-1052-azure containerd://1.7.5-1 aks-nodepool1-20786768-vmss000001 Ready agent 22h v1.27.7 10.224.0.33 <none> Ubuntu 22.04.3 LTS 5.15.0-1052-azure containerd://1.7.5-1 aksnpwin000000 Ready agent 20h v1.27.7 10.224.0.62 <none> Windows Server 2022 Datacenter 10.0.20348.2159 containerd://1.6.21+azure`

Note

The container runtime for each node pool is shown under

*CONTAINER-RUNTIME*. The container runtime values begin with`containerd://`

, which means that they each use`containerd`

for the container runtime.

## Deploy the application

A Kubernetes manifest file defines a desired state for the cluster, such as what container images to run. In this article, you use a manifest to create all objects needed to run the ASP.NET sample application in a Windows Server container. This manifest includes a [Kubernetes deployment](../concepts-clusters-workloads#deployments-and-yaml-manifests) for the ASP.NET sample application and an external [Kubernetes service](../concepts-network-services) to access the application from the internet.

The ASP.NET sample application is provided as part of the [.NET Framework Samples](https://hub.docker.com/_/microsoft-dotnet-framework-samples/) and runs in a Windows Server container. AKS requires Windows Server containers to be based on images of *Windows Server 2022* or greater. The Kubernetes manifest file must also define a [node selector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) to tell your AKS cluster to run your ASP.NET sample application's pod on a node that can run Windows Server containers.

Create a file named

`sample.yaml`

and copy in the following YAML definition:`apiVersion: apps/v1 kind: Deployment metadata: name: sample labels: app: sample spec: replicas: 1 template: metadata: name: sample labels: app: sample spec: nodeSelector: "kubernetes.io/os": windows containers: - name: sample image: mcr.microsoft.com/dotnet/framework/samples:aspnetapp resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 selector: matchLabels: app: sample --- apiVersion: v1 kind: Service metadata: name: sample spec: type: LoadBalancer ports: - protocol: TCP port: 80 selector: app: sample`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f sample.yaml`

The following example output shows the deployment and service created successfully:

`{ "deployment.apps/sample": "created", "service/sample": "created" }`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete. Occasionally, the service can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

Check the status of the deployed pods using the

command. Make sure all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`while true; do export EXTERNAL_IP=$(kubectl get service sample -o jsonpath="{.status.loadBalancer.ingress[0].ip}" 2>/dev/null) if [[ -n "$EXTERNAL_IP" && "$EXTERNAL_IP" != "<pending>" ]]; then kubectl get service sample break fi echo "Still waiting for external IP assignment..." sleep 5 done`

Initially, the output shows the

*EXTERNAL-IP*for the sample service as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE sample LoadBalancer xx.xx.xx.xx pending xx:xxxx/TCP 2m`

When the

*EXTERNAL-IP*address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output replaces

`<public-ip-address>`

with a valid public IP address assigned to the service:`{ "NAME": "sample", "TYPE": "LoadBalancer", "CLUSTER-IP": "10.0.37.27", "EXTERNAL-IP": "<public-ip-address>", "PORT(S)": "80:30572/TCP", "AGE": "2m" }`

See the sample app in action by opening a web browser to the external IP address of your service after a few minutes.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed an ASP.NET sample application in a Windows Server container to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS, and to walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-flatcar-deploy-arm-template -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Create an AKS cluster using Flatcar Container Linux for AKS (preview).
- Deploy an AKS cluster using an Azure Resource Manager template.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

An [Azure Resource Manager template](/en-us/azure/azure-resource-manager/templates/overview) is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This article assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. Make sure that the identity you use to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine, you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

After you deploy the cluster from the template, you can use either Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.

## Register resource providers

You might need to register resource providers in your Azure subscription. For example, `Microsoft.ContainerService`

is required.

Check the registration status using the [ az provider show](/en-us/cli/azure/provider#az-provider-show) command.

```
az provider show --namespace Microsoft.ContainerService --query registrationState
```


If necessary, register the resource provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command.

```
az provider register --namespace Microsoft.ContainerService
```


## Install `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Flatcar Container Linux requires a minimum of 18.0.0b42**.`az extension update --name aks-preview`


## Register `AKSFlatcarPreview`

feature flag

Register the

`AKSFlatcarPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AKSFlatcarPreview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AKSFlatcarPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create an SSH key pair

To create an AKS cluster using an ARM template, you provide an SSH public key. If you need this resource, follow the steps in this section. Otherwise, skip to the [Review the template](#review-the-template) section.

To access AKS nodes, you connect using an SSH key pair (public and private). To create an SSH key pair:

Go to

[https://shell.azure.com](https://shell.azure.com)to open Cloud Shell in your browser.Create a resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command.`az group create \ --name myResourceGroup \ --location eastus`

Create an SSH key pair using the

[az sshkey create](/en-us/cli/azure/sshkey#az-sshkey-create)command or the`ssh-keygen`

command.`az sshkey create --name mySSHKey --resource-group myResourceGroup`

Or create an SSH key pair using ssh-keygen

`ssh-keygen -t rsa -b 4096`

To deploy the template, you must provide the public key from the SSH pair. Retrieve the public key using the

command.`az sshkey show`

`az sshkey show --name mySSHKey --resource-group myResourceGroup --query publicKey`

By default, the SSH key files are created in the

*~/.ssh*directory. Running the`az sshkey create`

or`ssh-keygen`

command overwrites any existing SSH key pair with the same name.For more information about creating SSH keys, see

[Create and manage SSH keys for authentication in Azure](/en-us/azure/virtual-machines/linux/create-ssh-keys-detailed).

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/aks/).

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"metadata": {
"_generator": {
"name": "bicep",
"version": "0.26.170.59819",
"templateHash": "14823542069333410776"
}
},
"parameters": {
"clusterName": {
"type": "string",
"defaultValue": "aks101cluster",
"metadata": {
"description": "The name of the Managed Cluster resource."
}
},
"location": {
"type": "string",
"defaultValue": "[resourceGroup().location]",
"metadata": {
"description": "The location of the Managed Cluster resource."
}
},
"dnsPrefix": {
"type": "string",
"metadata": {
"description": "Optional DNS prefix to use with hosted Kubernetes API server FQDN."
}
},
"osDiskSizeGB": {
"type": "int",
"defaultValue": 0,
"minValue": 0,
"maxValue": 1023,
"metadata": {
"description": "Disk size (in GB) to provision for each of the agent pool nodes. This value ranges from 0 to 1023. Specifying 0 will apply the default disk size for that agentVMSize."
}
},
"agentCount": {
"type": "int",
"defaultValue": 3,
"minValue": 1,
"maxValue": 50,
"metadata": {
"description": "The number of nodes for the cluster."
}
},
"agentVMSize": {
"type": "string",
"defaultValue": "standard_d2s_v3",
"metadata": {
"description": "The size of the Virtual Machine."
}
},
"linuxAdminUsername": {
"type": "string",
"metadata": {
"description": "User name for the Linux Virtual Machines."
}
},
"sshRSAPublicKey": {
"type": "string",
"metadata": {
"description": "Configure all linux machines with the SSH RSA public key string. Your key should include three parts, for example 'ssh-rsa AAAAB...snip...UcyupgH azureuser@linuxvm'"
}
}
},
"resources": [
{
"type": "Microsoft.ContainerService/managedClusters",
"apiVersion": "2024-02-01",
"name": "[parameters('clusterName')]",
"location": "[parameters('location')]",
"identity": {
"type": "SystemAssigned"
},
"properties": {
"dnsPrefix": "[parameters('dnsPrefix')]",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": "[parameters('osDiskSizeGB')]",
"count": "[parameters('agentCount')]",
"vmSize": "[parameters('agentVMSize')]",
"osType": "Linux",
"mode": "System"
}
],
"linuxProfile": {
"adminUsername": "[parameters('linuxAdminUsername')]",
"ssh": {
"publicKeys": [
{
"keyData": "[parameters('sshRSAPublicKey')]"
}
]
}
}
}
}
],
"outputs": {
"controlPlaneFQDN": {
"type": "string",
"value": "[reference(resourceId('Microsoft.ContainerService/managedClusters', parameters('clusterName')), '2024-02-01').fqdn]"
}
}
}
```


The resource type defined in the ARM template is [ Microsoft.ContainerService/managedClusters](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template).

For more AKS samples, see the [AKS quickstart templates](https://azure.microsoft.com/resources/templates/?term=Azure+Kubernetes+Service) site.

## Deploy the template

Select

**Deploy to Azure**to sign in and open a template.On the

**Basics**page, leave the default values for the*OS Disk Size GB*,*Agent Count*,*Agent VM Size*, and*OS Type*, and configure the following template parameters:**Subscription**: Select an Azure subscription.**Resource group**: Select**Create new**. Enter a unique name for the resource group, such as*myResourceGroup*, then select**OK**.**OS SKU**: Specify**flatcar**, if you do not update OS SKU, the default will be`Ubuntu`

.**Location**: Select a location, such as**East US**.**Cluster name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**DNS prefix**: Enter a unique DNS prefix for your cluster, such as*myakscluster*.**Linux Admin Username**: Enter a username to connect using SSH, such as*azureuser*.**SSH public key source**: Select**Use existing public key**.**Key pair name**: Copy and paste the*public*part of your SSH key pair (by default, the contents of*~/.ssh/id_rsa.pub*).

Select

**Review + Create**>**Create**.

It takes a few minutes to create the AKS cluster. Wait for the cluster to be successfully deployed before you move on to the next step.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/).

If you use Azure Cloud Shell, `kubectl`

is already installed. To install and run `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az_aks_install_cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials \ --resource-group myResourceGroup \ --name myAKSCluster`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the three nodes created in the previous steps. Make sure the node status is

*Ready*:`NAME STATUS ROLES AGE VERSION aks-agentpool-38955149-vmss000000 Ready <none> 5m53s v1.32.7 aks-agentpool-38955149-vmss000001 Ready <none> 6m31s v1.32.7 aks-agentpool-238955149-vmss000002 Ready <none> 6m35s v1.32.7`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a file named

`aks-store-quickstart.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: rabbitmq spec: replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 resources: requests: cpu: 1m memory: 1Mi limits: cpu: 1m memory: 7Mi --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

Check the status of the deployed pods using the

command. Make all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the store-front application. Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action:


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges.

- Remove the resource group, container service, and all related resources using the
command.`az group delete`


```
az group delete --name myResourceGroup
```


Note

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity, so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-automatic-deploy -->

# Quickstart: Create an Azure Kubernetes Service (AKS) Automatic cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

[Azure Kubernetes Service (AKS) Automatic](../intro-aks-automatic) provides the easiest managed Kubernetes experience for developers, DevOps engineers, and platform engineers. Ideal for modern and AI applications, AKS Automatic automates AKS cluster setup and operations and embeds best practice configurations. Users of any skill level can benefit from the security, performance, and dependability of AKS Automatic for their applications. AKS Automatic also includes a [pod readiness SLA](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services) that guarantees 99.9% of pod readiness operations complete within 5 minutes, guaranteeing reliable, self-healing infrastructure for your applications.

In this quickstart, you learn to:

- Deploy an AKS Automatic cluster.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

## Before you begin

- This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads). - AKS Automatic will
[enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks), but you should pre-register the`Microsoft.PolicyInsights`

resource provider in your subscription for a smoother experience. See[Azure resource providers and types](/en-us/cli/azure/provider#az-provider-register)for more information.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.77.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command.`az account set`


- To deploy a Bicep file, you need to write access on the resources you create and access to all operations on the
`Microsoft.Resources/deployments`

resource type. For example, to create a virtual machine, you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

## Limitations

- AKS Automatic clusters' system nodepool require deployment in Azure regions that support at least three
[availability zones](/en-us/azure/reliability/regions-list), ephemeral OS disk, and Azure Linux OS. - You can only create AKS Automatic clusters in regions where
[API Server VNet Integration](../api-server-vnet-integration)is generally available (GA).

Important

AKS Automatic tries to dynamically select a virtual machine size for the `system`

node pool based on the capacity available in the subscription. Make sure your subscription has quota for 16 vCPUs of any of the following sizes in the region you're deploying the cluster to: [Standard_D4lds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series), [Standard_D4ads_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dadsv5-series), [Standard_D4ds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v4](/en-us/azure/virtual-machines/sizes/general-purpose/dv4-series), [Standard_DS3_v2](/en-us/azure/virtual-machines/sizes/general-purpose/dsv3-series), [Standard_DS12_v2](/en-us/azure/virtual-machines/sizes/memory-optimized/dv2-dsv2-series-memory), [Standard_D4alds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/daldsv6-series), [Standard_D4lds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv6-series), or [Standard_D4alds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series). You can [view quotas for specific VM-families and submit quota increase requests](/en-us/azure/quotas/per-vm-quota-requests) through the Azure portal.
If you have additional questions, learn more through the [troubleshooting docs](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/aks-automatic-troubleshoot/).

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name myResourceGroup --location eastus
```


The following sample output resembles successful creation of the resource group:

```
{
"id": "/subscriptions/<guid>/resourceGroups/myResourceGroup",
"location": "eastus",
"managedBy": null,
"name": "myResourceGroup",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null
}
```


## Create an AKS Automatic cluster

To create an AKS Automatic cluster, use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a cluster named

*myAKSAutomaticCluster*with Managed Prometheus and Container Insights integration enabled.

```
az aks create \
--resource-group myResourceGroup \
--name myAKSAutomaticCluster \
--sku automatic
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with

[Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

Note

When you create a cluster using the Azure CLI, your user is [assigned built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) for `Azure Kubernetes Service RBAC Cluster Admin`

.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSAutomaticCluster
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Create Automatic Kubernetes cluster

To create an AKS Automatic cluster, search for

**Kubernetes Services**, and select**Automatic Kubernetes cluster**from the drop-down options.On the

**Basics**tab, fill in all the mandatory fields (Subscription, Resource group, Kubernetes cluster name, and Region) required to get started:On the

**Monitoring**tab, choose your monitoring configurations from Azure Monitor, Managed Prometheus, Grafana Dashboards, Container Network Observability (ACNS) and/or configure alerts. Enable Managed Grafana (optional), add tags (optional), and proceed to create the cluster.On the

**Advanced**tab, update your networking (optional), managed identity (optional), security and managed namespaces (optional) settings and proceed to create the cluster.Get started with configuring your first application from GitHub and set up an automated deployment pipeline.


## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac). When you create a cluster using the Azure portal, your user is [assigned built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) for `Azure Kubernetes Service RBAC Cluster Admin`

.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSAutomaticCluster
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name myResourceGroup --location eastus
```


The following sample output resembles successful creation of the resource group:

```
{
"id": "/subscriptions/<guid>/resourceGroups/myResourceGroup",
"location": "eastus",
"managedBy": null,
"name": "myResourceGroup",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null
}
```


## Review the Bicep file

This Bicep file defines an AKS Automatic cluster. While in preview, you need to specify the *system nodepool* agent pool profile.

```
@description('The name of the managed cluster resource.')
param clusterName string = 'myAKSAutomaticCluster'
@description('The location of the managed cluster resource.')
param location string = resourceGroup().location
resource aks 'Microsoft.ContainerService/managedClusters@2024-03-02-preview' = {
name: clusterName
location: location
sku: {
name: 'Automatic'
}
properties: {
agentPoolProfiles: [
{
name: 'systempool'
mode: 'System'
count: 3
}
]
}
identity: {
type: 'SystemAssigned'
}
}
```


For more information about the resource defined in the Bicep file, see the [ Microsoft.ContainerService/managedClusters](/en-us/azure/templates/microsoft.containerservice/managedclusters?tabs=bicep&pivots=deployment-language-bicep) reference.

## Deploy the Bicep file

Save the Bicep file as

**main.bicep**to your local computer.Important

The Bicep file sets the

`clusterName`

param to the string*myAKSAutomaticCluster*. If you want to use a different cluster name, make sure to update the string to your preferred cluster name before saving the file to your computer.Deploy the Bicep file using the Azure CLI.

`az deployment group create --resource-group myResourceGroup --template-file main.bicep`

It takes a few minutes to create the AKS cluster. Wait for the cluster to be successfully deployed before you move on to the next step.


## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

Important

When you create a cluster using Bicep, you need to [assign one of the built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) such as `Azure Kubernetes Service RBAC Reader`

, `Azure Kubernetes Service RBAC Writer`

, `Azure Kubernetes Service RBAC Admin`

, or `Azure Kubernetes Service RBAC Cluster Admin`

to your users, scoped to the cluster or a specific namespace, example using `az role assignment create --role "Azure Kubernetes Service RBAC Cluster Admin" --scope <AKS cluster resource id> --assignee user@contoso.com`

. Also make sure your users have the `Azure Kubernetes Service Cluster User`

built-in role to be able to do run `az aks get-credentials`

, and then get the kubeconfig of your AKS cluster using the `az aks get-credentials`

command.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a namespace

`aks-store-demo`

to deploy the Kubernetes resources into.`kubectl create ns aks-store-demo`

Deploy the application using the

command into the`kubectl apply`

`aks-store-demo`

namespace. The YAML file defining the deployment is on[GitHub](https://github.com/Azure-Samples/aks-store-demo).`kubectl apply -n aks-store-demo -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-ingress-quickstart.yaml`

The following sample output shows the deployments and services:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created ingress/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make sure all pods are`Running`

before proceeding. If this is the first workload you deploy, it may take a few minutes for[node auto provisioning](../node-autoprovision)to create a node pool to run the pods.`kubectl get pods -n aks-store-demo`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get ingress store-front -n aks-store-demo --watch`

The

**ADDRESS**output for the`store-front`

service initially shows empty:`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 80 12m`

Once the

**ADDRESS**changes from blank to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following sample output shows a valid public IP address assigned to the service:

`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 4.255.22.196 80 12m`

Open a web browser to the external IP address of your ingress to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges. Run the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.

```
az group delete --name myResourceGroup --yes --no-wait
```


Note

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity, so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster using [AKS Automatic](../intro-aks-automatic) and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS Automatic, continue to the introduction.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kueue-overview -->

# Install and Configure Kueue on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to install and configure Kueue to schedule batch workloads on an Azure Kubernetes Service (AKS) cluster. You also explore different Kueue concepts, installation methods to enable advanced Kueue features, and learn how to verify your deployments.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## What are batch workloads?

Batch deployments are typically non-interactive workloads that are retriable, have a finite duration, and might experience spiky or bursty resource usage. These workloads include, but aren't limited to:

- Data processing jobs.
- Security vulnerability scans.
- Media encoding or video transcoding.
- Report generation or financial analysis.
- GPU workloads that require all resources to be available and might tolerate a delayed start but can't tolerate partial GPU allocation.

These workloads are often modeled using a Kubernetes Job, CronJob, or custom resource definition (CRD) like [RayJob](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started/rayjob-quick-start.html) or [Kubeflow MPIJob](https://www.kubeflow.org/docs/components/trainer/legacy-v1/user-guides/mpi/). Batch deployments present the following set of distinct requirements from general purpose deployments:

- Scheduling logic beyond selecting the first available node.
- Fairness, queueing, and resource awareness.
- Lifecycle awareness of jobs and pods.

The default AKS scheduler satisfies the requirements of Kubernetes services but provides limited configuration for batch workloads that require a job queueing system.

## What is Kueue?

[Kueue](https://kueue.sigs.k8s.io/docs/overview/) is an open-source Kubernetes-native job queueing project designed to manage batch workloads and ensure efficient, fair, and policy-driven scheduling in Kubernetes clusters. Kueue integrates with the [Kubernetes scheduling](https://github.com/kubernetes/community/blob/master/sig-scheduling/README.md) ecosystem to coordinate resource allocation, prioritization, and capacity control for batch jobs.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

Kueue introduces a two-level queuing model:

- A
`ClusterQueue`

represents shared resource pools (such as CPU, memory, GPU quotas). - A
`LocalQueue`

represents a tenant-facing queue in a namespace (where users submit their batch jobs).

Workloads submitted to a `LocalQueue`

are matched to a `ClusterQueue`

to determine if they can be admitted.

Note

A `LocalQueue`

is always needed for users to submit batch workloads, and the `LocalQueue`

tells Kueue about which ClusterQueue to assign the job to. The `ClusterQueue`

determines if sufficient resources are available for the job to be admitted and run.

## Who can use Kueue?

Batch workload administrators (including platform or cluster administrators and DevOps engineers) and batch users (data scientists, developers, and ML engineers) can benefit from deploying workloads with Kueue on AKS.

A batch admin focuses on configuring, managing, and securing the platform-level infrastructure to support batch workloads, and have the following responsibilities:

- Provision and manage AKS node pools.
- Define resource quotas, ClusterQueues, and policies for workload isolation.
- Tune autoscaling and cost-efficiency (such as the Cluster Autoscaler or Kueue quotas).
- Monitor cluster and queue health.
- Create and maintain templates and reusable workflows.

A batch user runs compute-intensive or parallel jobs using the platform-level infrastructure configured by a batch admin, and typically:

- Submit batch jobs (such as Job, Workload, or custom controller CRDs) and monitor job status and outputs
- Select appropriate queue or resource flavor for jobs (based on guidance from batch admins)
- Optimize job specs for resource and performance needs

| Queue Type | Scope | Created By | Used For |
|---|---|---|---|
ClusterQueue |
Cluster-wide | Platform admin | Define shared compute capacity and quota management |
LocalQueue |
Namespace | Namespace owner | Enable workload submission, mapped to ClusterQueue |

## Prerequisites

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Azure CLI installed on your local machine. To install or upgrade, see
[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). [Helm version 3 or above](https://helm.sh/docs/intro/install/)installed.

## Install Kueue with Helm

While most features and scheduling policies that you might require are enabled by default, some aren't like `TopologyAwareScheduling`

. If needed, reconfigure your Kueue installation by changing the default [Feature Gates](https://kueue.sigs.k8s.io/docs/installation/#feature-gates-for-alpha-and-beta-features) or by configuring [Kueue paramater values](https://github.com/kubernetes-sigs/kueue/blob/main/charts/kueue/README.md#configuration) in the `values.yaml`

file of the Helm chart.

Kueue supports multiple workload [Frameworks](https://kueue.sigs.k8s.io/docs/tasks/run/) that you need to explicitly enable to use Kueue’s scheduling and resource management capabilities when running [MPI Operator](https://www.kubeflow.org/docs/components/training/mpi/) MPIJobs, [KubeRay's](https://github.com/ray-project/kuberay) [RayJob](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started/rayjob-quick-start.html) and more.

In this guide, Kueue is configured to include `LocalQueueMetrics`

and `Topology Aware Scheduling`

and frameworks from Kubeflow, Ray, and [JobSet](https://jobset.sigs.k8s.io/docs/concepts/).

`LocalQueueMetrics`

provides detailed Prometheus metrics specific to the state and activity of LocalQueues, enabling fine-grained monitoring of workload admission, quota reservation, and resource utilization.`TopologyAwareScheduling`

allows scheduling of pods based on the topology of nodes in a pool or cluster to improve available bandwidth between the pods.

Note

Update version as needed: [kueue/releases](https://github.com/kubernetes-sigs/kueue/releases)

Create and save a

`values.yaml`

file to optionally customize your Kueue configuration.`cat <<EOF > values.yaml controllerManager: featureGates: - name: TopologyAwareScheduling enabled: true - name: LocalQueueMetrics enabled: true managerConfig: controllerManagerConfigYaml: | apiVersion: config.kueue.x-k8s.io/v1beta1 kind: Configuration integrations: frameworks: - batch/job - kubeflow.org/mpijob - ray.io/rayjob - ray.io/raycluster - jobset.x-k8s.io/jobset - kubeflow.org/paddlejob - kubeflow.org/pytorchjob - kubeflow.org/tfjob - kubeflow.org/xgboostjob - kubeflow.org/jaxjob EOF`

Install the latest version of the Kueue controller and CRDs in a dedicated namespace using the

`helm install`

command.`LATEST_VERSION=$(curl -s https://api.github.com/repos/kubernetes-sigs/kueue/releases/latest | grep tag_name | cut -d '"' -f 4 | sed 's/^v//') helm install kueue oci://registry.k8s.io/kueue/charts/kueue \ --version=${LATEST_VERSION} \ --create-namespace --namespace=kueue-system \ --values values.yaml`

Confirm the deployment status using the

`helm list`

command.`helm list --namespace kueue-system`

Your output should include a

`Status`

of`deployed`

and look like:`Pulled: registry.k8s.io/kueue/charts/kueue:0.13.4 Digest: - NAME: kueue LAST DEPLOYED: - NAMESPACE: kueue-system STATUS: deployed REVISION: 1 TEST SUITE: None`


## Confirm deployment status

Verify that controller pods are running properly.

`kubectl get deploy -n kueue-system`

Your output should look similar to the following example output:

`NAME READY UP-TO-DATE AVAILABLE AGE kueue-controller-manager 1/1 1 1 7s`

Confirm the installation of Kueue resources on your AKS cluster:

`kubectl get crds | grep kueue`

Your output should include the following Kueue CRDs:

`admissionchecks.kueue.x-k8s.io 2025-09-11T18:20:48Z clusterqueues.kueue.x-k8s.io 2025-09-11T18:20:48Z cohorts.kueue.x-k8s.io 2025-09-11T18:20:48Z localqueues.kueue.x-k8s.io 2025-09-11T18:20:48Z multikueueclusters.kueue.x-k8s.io 2025-09-11T18:20:48Z multikueueconfigs.kueue.x-k8s.io 2025-09-11T18:20:48Z provisioningrequestconfigs.kueue.x-k8s.io 2025-09-11T18:20:48Z resourceflavors.kueue.x-k8s.io 2025-09-11T18:20:48Z topologies.kueue.x-k8s.io 2025-09-11T18:20:48Z workloadpriorityclasses.kueue.x-k8s.io 2025-09-11T18:20:48Z workloads.kueue.x-k8s.io 2025-09-11T18:20:48Z`


## Uninstall Kueue

If you no longer need to use the Kueue controller manager or Kueue custom resources in your AKS cluster, you can uninstall the Helm repository and remove the dedicated namespace and resources.

Uninstall the Kueue Helm repository using the

`helm uninstall`

command.`helm uninstall kueue --namespace kueue-system`

Remove the dedicated namespace and resources using the

`kubectl delete`

command.`kubectl delete namespace kueue-system`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/core-aks-concepts -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-configuration -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-clusters-workloads -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-mcp -->

# Integrate an MCP server with an LLM Inference Service on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you connect an MCP-compliant tool server with an AI toolchain operator (KAITO) inference workspace on Azure Kubernetes Service (AKS), enabling secure and modular tool calling for LLM applications. You also learn how to validate end-to-end tool invocation by integrating the model with the MCP server and monitoring real-time function execution through structured responses.

## Model Context Protocol (MCP)

As an extension of [KAITO inference with tool calling](ai-toolchain-operator-tool-calling), the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) provides a standardized way to define and expose tools for language models to call.

Tool calling with MCP makes it easier to connect language models to real services and actions without tightly coupling logic into the model itself. Instead of embedding every function or API call into your application code, MCP lets you run a standalone tool server that exposes standardized tools or APIs that any compatible LLM can use. This clean separation means you can update tools independently, share them across models, and manage them like any other microservice.

You can bring-your-own (BYO) internal or connect external MCP servers seamlessly with your KAITO inference workspace on AKS.

## MCP with AI toolchain operator (KAITO) on AKS

You can register an external MCP server in a uniform, schema-driven format and serve it to any compatible inference endpoint, including those [deployed with a KAITO workspace](https://kaito-project.github.io/kaito/docs/tool-calling/#model-context-protocol-mcp). This approach allows for externalizing business logic, decoupling model behavior from tool execution, and reusing tools across agents, models, and environments.

In this guide, you register a pre-defined MCP server, test real calls issued by an LLM running in a KAITO inference workspace, and confirm the entire tool execution path (from model prompt to MCP function invocation) works as intended. You have flexibility to scale or swap tools independent of your model.

## Prerequisites

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Your AKS cluster is running on Kubernetes version
`1.33`

or higher. To upgrade your cluster, see[Upgrade your AKS cluster](upgrade-aks-cluster). - Install and configure Azure CLI version
`2.77.0`

or later. To find your version, run`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - You have the
[AI toolchain operator add-on enabled](ai-toolchain-operator)on your cluster and a[KAITO workspace with tool calling support](ai-toolchain-operator-tool-calling)deployed on your cluster. - An external MCP server available at an accessible URL (e.g.,
`https://mcp.example.com/mcp`

) that returns valid`/list_tools`

and has`stream`

transport.

## Connect to a reference MCP server

In this example, we'll use a reference [Time MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/time#time-mcp-server), which provides time zone conversion capabilities and enables LLMs to get current time information and perform conversions using standardized names.

## Port-forward the KAITO inference service

Confirm that your KAITO workspace is ready and retrieve the inference service endpoint using the

`kubectl get`

command.`kubectl get svc workspace‑phi‑4-mini-toolcall`

Note

The output might be a

`ClusterIP`

or internal address. Check which port(s) the service listens on. The default KAITO inference API is on port`80`

for HTTP. If it's only internal, you can port‑forward locally.Port-forward the inference service for testing using the

`kubectl port-forward`

command.`kubectl port-forward svc/workspace‑phi‑4‑mini-toolcall 8000:80`

Check

`/v1/models`

endpoint to confirm that`Phi-4-mini-instruct`

LLM is available using`curl`

.`curl http://localhost:8000/v1/models`

Your

`Phi-4-mini-instruct`

OpenAI-compatible inference API will be available at:`http://localhost:8000/v1/chat/completions`


## Confirm the reference MCP server is valid

This example assumes that the Time MCP server is hosted at `https://mcp.example.com`

.

Confirm the server returns tools using

`curl`

.`curl https://mcp.example.com/mcp/list_tools`

Expected output:

`{ "tools": [ { "name": "get_current_time", "description": "Get the current time in a specific timezone", "arguments": { "timezone": "string" } }, { "name": "convert_time", "description": "Convert time between two timezones", "arguments": { "source_timezone": "string", "time": "string", "target_timezone": "string" } } ] }`


## Connect MCP server to the KAITO workspace using API request

KAITO automatically fetches tool definitions from **tools declared in API requests** or registered dynamically inside the inference runtime (vLLM + MCP tool loader).

In this guide, we create a Python virtual environment to send a tool-calling request to the `Phi-4-mini-instruct`

inference endpoint using the MCP definition and pointing to the server.

Define a new working directory for this test project.

`mkdir kaito-mcp cd kaito-mcp`

Create a Python virtual environment and activate it so that all packages are local to your test project.

`uv venv source .venv/bin/activate`

Use the open-source

[Autogen](https://microsoft.github.io/autogen/stable//index.html)framework to test the tool calling functionality and install its dependencies:`uv pip install "autogen-ext[openai]" "autogen-agentchat" "autogen-ext[mcp]"`

Create a test file named

`test.py`

that:- Connects to the Time MCP server and loads
`get_current_time`

tool. - Connects to your KAITO inference service running at
`localhost:8000`

. - Sends an example query like “What time is it in Europe/Paris?”
- Enables automatic selection and calling of the
`get_current_time`

tool.

`import asyncio from autogen_agentchat.agents import AssistantAgent from autogen_agentchat.ui import Console from autogen_core import CancellationToken from autogen_core.models import ModelFamily, ModelInfo from autogen_ext.models.openai import OpenAIChatCompletionClient from autogen_ext.tools.mcp import (StreamableHttpMcpToolAdapter, StreamableHttpServerParams) from openai import OpenAI async def main() -> None: # Create server params for the Time MCP service server_params = StreamableHttpServerParams( url="https://mcp.example.com/mcp", timeout=30.0, terminate_on_close=True, ) # Load the get_current_time tool from the server adapter = await StreamableHttpMcpToolAdapter.from_server_params(server_params, "get_current_time") # Fetch model name from KAITO's local OpenAI-compatible API model = OpenAI(base_url="http://localhost:8000/v1", api_key="dummy").models.list().data[0].id model_info: ModelInfo = { "vision": False, "function_calling": True, "json_output": True, "family": ModelFamily.UNKNOWN, "structured_output": True, "multiple_system_messages": True, } # Connect to the KAITO inference workspace model_client = OpenAIChatCompletionClient( base_url="http://localhost:8000/v1", api_key="dummy", model=model, model_info=model_info ) # Define the assistant agent agent = AssistantAgent( name="time-assistant", model_client=model_client, tools=[adapter], system_message="You are a helpful assistant that can provide time information." ) # Run a test task that invokes the tool await Console( agent.run_stream( task="What time is it in Europe/Paris?", cancellation_token=CancellationToken() ) ) if __name__ == "__main__": asyncio.run(main())`

- Connects to the Time MCP server and loads
Run the test script in your virtual environment.

`uv run test.py`

In the output of this test, you should expect the following:

- The model correctly generates a tool call using the MCP name and expected arguments.
- Autogen sends the tool call to the MCP server, the MCP server runs the logic and returns a result.
- The
`Phi-4-mini-instruct`

LLM interprets the raw tool output and provides a natural language response.

`---------- TextMessage (user) ---------- What time is it in Europe/Paris? ---------- ToolCallRequestEvent (time-assistant) ---------- [FunctionCall(id='chatcmpl-tool-xxxx', arguments='{"timezone": "Europe/Paris"}', name='get_current_time')] ---------- ToolCallExecutionEvent (time-assistant) ---------- [FunctionExecutionResult(content='{"timezone":"Europe/Paris","datetime":"2025-09-17T17:43:05+02:00","is_dst":true}', name='get_current_time', call_id='chatcmpl-tool-xxxx', is_error=False)] ---------- ToolCallSummaryMessage (time-assistant) ---------- The current time in Europe/Paris is 5:43 PM (CEST).`


## Experiment with more MCP tools

You can test the various tools available to this MCP server, such as `convert_time`

.

In your

`test.py`

file from the previous step, update your`adapter`

definition to the following:`adapter = await StreamableHttpMcpToolAdapter.from_server_params(server_params, "convert_time")`

Update your

`task`

definition to invoke the new tool. For example:`task="Convert 9:30 AM New York time to Tokyo time."`

Save and run the Python script.

`uv run test.py`

Expected output:

`9:30 AM in New York is 10:30 PM in Tokyo.`


## Troubleshooting

The following table outlines common errors when testing KAITO inference with an external MCP server and how to resolve them:

| Error | How to resolve |
|---|---|
`Tool not found` |
Ensure that your tool name matches the one declared in `/mcp/list_tools` . |
`401 Unauthorized` |
If your MCP server requires an Auth token, make sure to update `server_params` to include headers with the Auth token. |
`connection refused` |
Ensure the KAITO inference service is port-forwarded properly (e.g. to `localhost:8000` ). |
`tool call ignored` |
Review the
|

## Next steps

In this article, you learned how to connect a KAITO workspace to an external reference MCP server using Autogen to enable tool calling through the OpenAI-compatible API. You also validated that the LLM could discover, invoke, and integrate results from MCP-compliant tools on AKS. To learn more, see the following resources:

[Deploy and test tool calls](ai-toolchain-operator-tool-calling)with the AI toolchain operator add-on on AKS.- KAITO tool calling and
[MCP official documentation](https://kaito-project.github.io/kaito/docs/tool-calling).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/virtual-nodes-cli -->

# Create and configure an Azure Kubernetes Services (AKS) cluster to use virtual nodes using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Virtual nodes enable network communication between pods that run in Azure Container Instances (ACI) and AKS clusters. To provide this communication, you create a virtual network subnet and assign delegated permissions. Virtual nodes only work with AKS clusters created using *advanced* networking (Azure CNI). By default, AKS clusters are created with *basic* networking (kubenet). This article shows you how to create a virtual network and subnets, then deploy an AKS cluster that uses advanced networking.

This article shows you how to use the Azure CLI to create and configure virtual network resources and an AKS cluster enabled with virtual nodes.

## Before you begin

Important

Before using virtual nodes with AKS, review both the [limitations of AKS virtual nodes](virtual-nodes) and the [virtual networking limitations of ACI](/en-us/azure/container-instances/container-instances-virtual-network-concepts). These limitations affect the location, networking configuration, and other configuration details of both your AKS cluster and the virtual nodes.

You need the ACI service provider registered with your subscription. You can check the status of the ACI provider registration using the

command.`az provider list`

`az provider list --query "[?contains(namespace,'Microsoft.ContainerInstance')]" -o table`

The

*Microsoft.ContainerInstance*provider should report as*Registered*, as shown in the following example output:`Namespace RegistrationState RegistrationPolicy --------------------------- ------------------- -------------------- Microsoft.ContainerInstance Registered RegistrationRequired`

If the provider shows as

*NotRegistered*, register the provider using the.`az provider register`

`az provider register --namespace Microsoft.ContainerInstance`

If using Azure CLI, this article requires Azure CLI version 2.0.49 or later. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). You can also use[Azure Cloud Shell](#launch-azure-cloud-shell).

### Launch Azure Cloud Shell

The Azure Cloud Shell is a free interactive shell you can use to run the steps in this article. It has common Azure tools preinstalled and configured.

To open the Cloud Shell, select **Try it** from the upper right corner of a code block. You can also launch Cloud Shell in a separate browser tab by going to [https://shell.azure.com/bash](https://shell.azure.com/bash). Select **Copy** to copy the blocks of code, paste it into the Cloud Shell, and press enter to run it.

## Create a resource group

An Azure resource group is a logical group in which Azure resources are deployed and managed.

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`


## Create a virtual network

Important

Virtual node requires a custom virtual network and associated subnet. It can't be associated with the same virtual network as the AKS cluster.

Create a virtual network using the

command. The following example creates a virtual network named`az network vnet create`

*myVnet*with an address prefix of*10.0.0.0/8*and a subnet named*myAKSSubnet*. The address prefix of this subnet defaults to*10.240.0.0/16*.`az network vnet create \ --resource-group myResourceGroup \ --name myVnet \ --address-prefixes 10.0.0.0/8 \ --subnet-name myAKSSubnet \ --subnet-prefix 10.240.0.0/16`

Create an extra subnet for the virtual nodes using the

command. The following example creates a subnet named`az network vnet subnet create`

*myVirtualNodeSubnet*with an address prefix of*10.241.0.0/16*.`az network vnet subnet create \ --resource-group myResourceGroup \ --vnet-name myVnet \ --name myVirtualNodeSubnet \ --address-prefixes 10.241.0.0/16`


## Create an AKS cluster with managed identity

Get the subnet ID using the

command.`az network vnet subnet show`

`az network vnet subnet show --resource-group myResourceGroup --vnet-name myVnet --name myAKSSubnet --query id -o tsv`

Create an AKS cluster using the

command and replace`az aks create`

`<subnetId>`

with the ID obtained in the previous step. The following example creates a cluster named*myAKSCluster*with five nodes.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 5 \ --network-plugin azure \ --vnet-subnet-id <subnetId> \ --generate-ssh-keys`

After several minutes, the command completes and returns JSON-formatted information about the cluster.


For more information on managed identities, see [Use managed identities](use-managed-identity).

## Enable the virtual nodes addon

Note

If you have an existing Azure Kubernetes Service Cluster created that uses Azure CNI for the Advanced Networking you should be able to enable virtual nodes as an add-on using the CLI.

Enable virtual nodes using the

command. The following example uses the subnet named`az aks enable-addons`

*myVirtualNodeSubnet*created in a previous step.`az aks enable-addons \ --resource-group myResourceGroup \ --name myAKSCluster \ --addons virtual-node \ --subnet-name myVirtualNodeSubnet`


## Connect to the cluster

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This step downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

command, which returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the single VM node created and the virtual node for Linux,

*virtual-node-aci-linux*:`NAME STATUS ROLES AGE VERSION virtual-node-aci-linux Ready agent 28m v1.11.2 aks-agentpool-14693408-0 Ready agent 32m v1.11.2`


## Deploy a sample app

Create a file named

`virtual-node.yaml`

and copy in the following YAML. The YAML schedules the container on the node by defining a[nodeSelector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/)and[toleration](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/).`apiVersion: apps/v1 kind: Deployment metadata: name: aci-helloworld spec: replicas: 1 selector: matchLabels: app: aci-helloworld template: metadata: labels: app: aci-helloworld spec: containers: - name: aci-helloworld image: mcr.microsoft.com/azuredocs/aci-helloworld ports: - containerPort: 80 nodeSelector: kubernetes.io/role: agent kubernetes.io/os: linux type: virtual-kubelet tolerations: - key: virtual-kubelet.io/provider operator: Exists - key: azure.com/aci effect: NoSchedule`

Run the application using the

command.`kubectl apply`

`kubectl apply -f virtual-node.yaml`

Get a list of pods and the scheduled node using the

command with the`kubectl get pods`

`-o wide`

argument.`kubectl get pods -o wide`

The pod is scheduled on the virtual node

*virtual-node-aci-linux*, as shown in the following example output:`NAME READY STATUS RESTARTS AGE IP NODE aci-helloworld-9b55975f-bnmfl 1/1 Running 0 4m 10.241.0.4 virtual-node-aci-linux`

The pod is assigned an internal IP address from the Azure virtual network subnet delegated for use with virtual nodes.


Note

If you use images stored in Azure Container Registry, [configure and use a Kubernetes secret](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/). A current limitation of virtual nodes is you can't use integrated Microsoft Entra service principal authentication. If you don't use a secret, pods scheduled on virtual nodes fail to start and report the error `HTTP response status code 400 error code "InaccessibleImage"`

.

## Test the virtual node pod

Test the pod running on the virtual node by browsing to the demo application with a web client. As the pod is assigned an internal IP address, you can quickly test this connectivity from another pod on the AKS cluster.

Create a test pod and attach a terminal session to it using the following

`kubectl run -it`

command.`kubectl run -it --rm testvk --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

Install

`curl`

in the pod using`apt-get`

.`apt-get update && apt-get install -y curl`

Access the address of your pod using

`curl`

, such as. Provide your own internal IP address shown in the previous[http://10.241.0.4](http://10.241.0.4)`kubectl get pods`

command.`curl -L http://10.241.0.4`

The demo application is displayed, as shown in the following condensed example output:

`<html> <head> <title>Welcome to Azure Container Instances!</title> </head> [...]`

Close the terminal session to your test pod with

`exit`

. When your session is ends, the pod is deleted.

## Remove virtual nodes

Delete the

`aci-helloworld`

pod running on the virtual node using the`kubectl delete`

command.`kubectl delete -f virtual-node.yaml`

Disable the virtual nodes using the

command.`az aks disable-addons`

`az aks disable-addons --resource-group myResourceGroup --name myAKSCluster --addons virtual-node`

Remove the virtual network resources and resource group using the following commands.

`# Change the name of your resource group, cluster and network resources as needed RES_GROUP=myResourceGroup AKS_CLUSTER=myAKScluster AKS_VNET=myVnet AKS_SUBNET=myVirtualNodeSubnet # Get AKS node resource group NODE_RES_GROUP=$(az aks show --resource-group $RES_GROUP --name $AKS_CLUSTER --query nodeResourceGroup --output tsv) # Get network profile ID NETWORK_PROFILE_ID=$(az network profile list --resource-group $NODE_RES_GROUP --query "[0].id" --output tsv) # Delete the network profile az network profile delete --id $NETWORK_PROFILE_ID -y # Grab the service association link ID SAL_ID=$(az network vnet subnet show --resource-group $RES_GROUP --vnet-name $AKS_VNET --name $AKS_SUBNET --query id --output tsv)/providers/Microsoft.ContainerInstance/serviceAssociationLinks/default # Delete the service association link for the subnet az resource delete --ids $SAL_ID --api-version 2021-10-01 # Delete the subnet delegation to Azure Container Instances az network vnet subnet update --resource-group $RES_GROUP --vnet-name $AKS_VNET --name $AKS_SUBNET --remove delegations`


## Next steps

In this article, you scheduled a pod on the virtual node and assigned a private internal IP address. You could instead create a service deployment and route traffic to your pod through a load balancer or ingress controller. For more information, see [Create a basic ingress controller in AKS](ingress-basic).

Virtual nodes are often one component of a scaling solution in AKS. For more information on scaling solutions, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-application-template -->

# Deploy an Azure Kubernetes application by using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To deploy a Kubernetes application programmatically through Azure CLI, you select the Kubernetes application and settings, generate an ARM template, accept legal terms and conditions, and finally deploy the ARM template.

## Select Kubernetes application

First, you need to select the Kubernetes application that you want to deploy in the Azure portal.

In the Azure portal, go to the

[Marketplace page](https://portal.azure.com/#view/Microsoft_Azure_Marketplace/MarketplaceOffersBlade/selectedMenuItemId/home/fromContext/AKS).Select your Kubernetes application.

Select the required plan.

Select the

**Usage Information + Support**tab. Copy the values for`publisherID`

,`productID`

, and`planID`

. You'll need these values later.

## Generate ARM template

Continue on to generate the ARM template for your deployment.

Select the

**Create**button.Fill out all the application (extension) details.

At the bottom of the

**Review + Create**tab, select**Download a template for automation**.If all the validations are passed, you'll see the ARM template in the editor.

Download the ARM template and save it to a file on your computer.


## Accept terms and agreements

Before you can deploy a Kubernetes application, you need to accept its terms and agreements. To do so, use [Azure CLI](/en-us/cli/azure/vm/image/terms) or [Azure PowerShell](/en-us/powershell/module/az.marketplaceordering/). Be sure to use the values you copied for `plan-publisher`

, `plan-offerID`

, and `plan-name`

in your command.

```
az vm image terms accept --offer <Product ID> --plan <Plan ID> --publisher <Publisher ID>
```


Note

Although this Azure CLI command is for VMs, it also works for containers. For more information, see the [ az cm image terms reference](/en-us/cli/azure/vm/image/terms).

```
## Get-AzMarketplaceTerms -Publisher <Publisher ID> -Product <Product ID> -Name <Plan ID>
```


## Deploy ARM template

Once you've accepted the terms, you can deploy your ARM template. For instructions, see [Tutorial: Create and deploy your first ARM template](/en-us/azure/azure-resource-manager/templates/template-tutorial-create-first-template).

## Next steps

- Learn about
[Kubernetes applications available through Marketplace](deploy-marketplace). - Learn about
[cluster extensions](cluster-extensions).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/understand-aks-costs -->

# Understand Azure Kubernetes Service (AKS) usage and costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides resources you can use to better understand your Azure Kubernetes Service (AKS) usage and costs and identify cost optimization opportunities.

## About cost analysis

[Microsoft Cost Management](/en-us/azure/cost-management-billing/costs/reporting-get-started) is a suite of FinOps tools that help you analyze, monitor, and optimize your cloud costs. It's available for Azure customers with access to a billing account, subscription, resource group, or management group. For more information, see [What is Microsoft Cost Management?](/en-us/azure/cost-management-billing/costs/overview-cost-management)

[Cost analysis](/en-us/azure/cost-management-billing/costs/reporting-get-started#cost-analysis) is a feature of Cost Management that helps you understand your costs and usage. It provides insights into how your resources are being used and helps you identify opportunities to reduce costs. For more information, see [Start analyzing costs in Azure](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis).

## Cost analysis resources

### Cost analysis add-on for AKS

The cost analysis add-on for AKS allows you to view comprehensive cost data scoped to Kubernetes constructs, such as clusters and namespaces, and Azure Compute, Network, and Storage resources. Enable it on your AKS cluster by following the steps in [Enable the Azure Kubernetes Service (AKS) cost analysis add-on](cost-analysis). To learn more about viewing the cost data, see [View Kubernetes costs](/en-us/azure/cost-management-billing/costs/view-kubernetes-costs).

### Azure Cost Optimization workbook

The [Azure Cost Optimization workbook](/en-us/azure/advisor/advisor-workbook-cost-optimization) provides a comprehensive view of your Azure costs and recommendations for optimizing them. For more information, see [Cost Optimization workbook](/en-us/azure/advisor/advisor-workbook-cost-optimization).

### Azure Orphaned Resources workbook

The [Azure Orphaned Resources workbook](https://github.com/dolevshor/azure-orphan-resources) helps you identify and manage unused resources in your Azure environment. For more information, see [Orphaned Resources workbook](https://techcommunity.microsoft.com/blog/fasttrackforazureblog/azure-orphan-resources/3492198).

## Next steps

For more information about managing your AKS costs, see [Best practices for cost optimization in Azure Kubernetes Service (AKS)](best-practices-cost).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubelet-logs -->

# Get kubelet logs from Azure Kubernetes Service cluster nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might need to review logs to troubleshoot a problem in your Azure Kubernetes Service (AKS) cluster. You can use tools in the Azure portal to view logs for AKS [main components](monitor-aks-reference#resource-logs) and [cluster containers](/en-us/azure/azure-monitor/containers/container-insights-overview). Occasionally, you might need to get *kubelet* logs from AKS nodes to help you troubleshoot an issue.

This article shows you how to use `journalctl`

to view kubelet logs on an AKS node.

Alternatively, you can collect kubelet logs by using the [syslog collection feature in Container insights in Azure Monitor](https://aka.ms/CISyslog).

## Before you begin

This article assumes that you have an existing AKS cluster. If you need an AKS cluster, create one by using the [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

## Connect to your AKS cluster

To interact with your AKS cluster, first get the cluster credentials by using the Azure CLI:

```
export RESOURCE_GROUP_NAME="<ResourceGroupName>"
export AKS_CLUSTER_NAME="<AKSClusterName>"
az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $AKS_CLUSTER_NAME
```


This command configures kubectl to use the credentials for your AKS cluster.

## Use the kubectl raw command

You can quickly view any node's kubelet logs by using the following command:

```
export NODE_NAME="aks-agentpool-xxxxxxx-0"
kubectl get --raw "/api/v1/nodes/$NODE_NAME/proxy/logs/messages" | grep kubelet
```


Results:

```
I0508 12:26:17.905042 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:27.943494 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:28.920125 8672 server.go:796] GET /stats/summary: (10.370874ms) 200 [[Ruby] 10.244.0.x:52492]
I0508 12:26:37.964650 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
...
```


## Create an SSH connection

You must create a Secure Shell Protocol (SSH) connection with the node you need to view kubelet logs for. To create this connection, complete the steps that are described in [SSH into AKS cluster nodes](ssh).

## Get kubelet logs

After you connect to the node by using `kubectl debug`

, run the following command to pull the kubelet logs:

```
chroot /host
journalctl -u kubelet -o cat
```


Note

For Windows nodes, the log data is in `C:\k`

and can be viewed by using the `more`

command:

```
more C:\k\kubelet.log
```


The following example output shows kubelet log data:

```
I0508 12:26:17.905042 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:27.943494 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:28.920125 8672 server.go:796] GET /stats/summary: (10.370874ms) 200 [[Ruby] 10.244.0.x:52292]
I0508 12:26:37.964650 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:47.996449 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:58.019746 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:05.107680 8672 server.go:796] GET /stats/summary/: (24.853838ms) 200 [[Go-http-client/1.1] 10.244.0.x:44660]
I0508 12:27:08.041736 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:18.068505 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:28.094889 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:38.121346 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:44.015205 8672 server.go:796] GET /stats/summary: (30.236824ms) 200 [[Ruby] 10.244.0.x:52588]
I0508 12:27:48.145640 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:58.178534 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:05.040375 8672 server.go:796] GET /stats/summary/: (27.78503ms) 200 [[Go-http-client/1.1] 10.244.0.x:44660]
I0508 12:28:08.214158 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:18.242160 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:28.274408 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:38.296074 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:48.321952 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:58.344656 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-advanced-scheduler -->

# Best practices for advanced scheduler features in Azure Kubernetes Service (AKS) using the kube-scheduler

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. Advanced features provided by the Kubernetes scheduler let you control:

- Which pods can be scheduled on certain nodes.
- How multi-pod applications can be appropriately distributed across the cluster.

This best practices article focuses on advanced Kubernetes scheduling features for cluster operators. In this article, you learn how to:

- Use taints and tolerations to limit what pods can be scheduled on nodes.
- Give preference to pods to run on certain nodes with node selectors or node affinity.
- Split apart or group together pods with inter-pod affinity or anti-affinity.
- Restrict scheduling of workloads that require GPUs only on nodes with schedulable GPUs.

If additional capabilities or ML frameworks are needed to schedule and queue batch workloads, you can [install and configure Kueue on AKS](kueue-overview) to ensure efficient, policy-driven scheduling in AKS clusters.

If fine-grained scheduler configuration is needed to optimize how pods and jobs prioritize specific nodes, storage resources, topology, and more, you can [configure a scheduler on AKS](concepts-scheduler-configuration).

## Provide dedicated nodes using taints and tolerations


Best practice guidance:Limit access for resource-intensive applications, such as ingress controllers, to specific nodes. Keep node resources available for workloads that require them, and don't allow scheduling of other workloads on the nodes.


When you create your AKS cluster, you can deploy nodes with GPU support or a large number of powerful CPUs. For more information, see [Use GPUs on AKS](gpu-cluster). You can use these nodes for large data processing workloads such as machine learning (ML) or artificial intelligence (AI).

Because this node resource hardware is typically expensive to deploy, limit the workloads that can be scheduled on these nodes. Instead, dedicate some nodes in the cluster to run ingress services and prevent other workloads.

This support for different nodes is provided by using multiple node pools. An AKS cluster supports one or more node pools.

The Kubernetes scheduler uses taints and tolerations to restrict what workloads can run on nodes.

- Apply a
**taint**to a node to indicate only specific pods can be scheduled on them. - Then apply a
**toleration**to a pod, allowing them to*tolerate*a node's taint.

When you deploy a pod to an AKS cluster, Kubernetes only schedules pods on nodes whose taint aligns with the toleration. Taints and tolerations work together to ensure that pods aren't scheduled onto inappropriate nodes. One or more taints are applied to a node, marking the node so that it doesn't accept any pods that don't tolerate the taints.

For example, assume you added a node pool in your AKS cluster for nodes with GPU support. You define name, such as *gpu*, then a value for scheduling. Setting this value to *NoSchedule* restricts the Kubernetes scheduler from scheduling pods with undefined toleration on the node.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name taintnp \
--node-taints sku=gpu:NoSchedule \
--no-wait
```


With a taint applied to nodes in the node pool, you define a toleration in the pod specification that allows scheduling on the nodes. The following example defines the `sku: gpu`

and `effect: NoSchedule`

to tolerate the taint applied to the node pool in the previous step:

```
kind: Pod
apiVersion: v1
metadata:
name: app
spec:
containers:
- name: app
image: <your-workload>:gpu
resources:
requests:
cpu: 0.5
memory: 2Gi
limits:
cpu: 4.0
memory: 16Gi
tolerations:
- key: "sku"
operator: "Equal"
value: "gpu"
effect: "NoSchedule"
```


When this pod is deployed using `kubectl apply -f gpu-toleration.yaml`

, Kubernetes can successfully schedule the pod on the nodes with the taint applied. This logical isolation lets you control access to resources within a cluster.

When you apply taints, work with your application developers and owners to allow them to define the required tolerations in their deployments.

For more information about how to use multiple node pools in AKS, see [Create multiple node pools for a cluster in AKS](create-node-pools).

### Behavior of taints and tolerations in AKS

When you upgrade a node pool in AKS, taints and tolerations follow a set pattern as they're applied to new nodes:

#### Default clusters that use Azure Virtual Machine Scale Sets

You can [taint a node pool](manage-node-pools#specify-a-taint-label-or-tag-for-a-node-pool) from the AKS API to have newly scaled out nodes receive API specified node taints.

Let's assume:

- You begin with a two-node cluster:
*node1*and*node2*. - You upgrade the node pool.
- Two other nodes are created:
*node3*and*node4*. - The taints are passed on respectively.
- The original
*node1*and*node2*are deleted.

#### Clusters without Virtual Machine Scale Sets support

Again, let's assume:

- You have a two-node cluster:
*node1*and*node2*. - You upgrade the node pool.
- An extra node is created:
*node3*. - The taints from
*node1*are applied to*node3*. *node1*is deleted.- A new
*node1*is created to replace to original*node1*. - The
*node2*taints are applied to the new*node1*. *node2*is deleted.

In essence, *node1* becomes *node3*, and *node2* becomes the new *node1*.

When you scale a node pool in AKS, taints and tolerations don't carry over by design.

## Control pod scheduling using node selectors and affinity


Best practice guidanceControl the scheduling of pods on nodes using node selectors, node affinity, or inter-pod affinity. These settings allow the Kubernetes scheduler to logically isolate workloads, such as by hardware in the node.


Taints and tolerations logically isolate resources with a hard cut-off. If the pod doesn't tolerate a node's taint, it isn't scheduled on the node.

Alternatively, you can use node selectors. For example, you label nodes to indicate locally attached SSD storage or a large amount of memory, and then define in the pod specification a node selector. Kubernetes schedules those pods on a matching node.

Unlike tolerations, pods without a matching node selector can still be scheduled on labeled nodes. This behavior allows unused resources on the nodes to consume, but prioritizes pods that define the matching node selector.

Let's look at an example of nodes with a high amount of memory. These nodes prioritize pods that request a high amount of memory. To ensure the resources don't sit idle, they also allow other pods to run. The following example command adds a node pool with the label *hardware=highmem* to the *myAKSCluster* in the *myResourceGroup*. All nodes in that node pool have this label.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name labelnp \
--node-count 1 \
--labels hardware=highmem \
--no-wait
```


A pod specification then adds the `nodeSelector`

property to define a node selector that matches the label set on a node:

```
kind: Pod
apiVersion: v1
metadata:
name: app
spec:
containers:
- name: app
image: <your-workload>:gpu
resources:
requests:
cpu: 0.5
memory: 2Gi
limits:
cpu: 4.0
memory: 16Gi
nodeSelector:
hardware: highmem
```


When you use these scheduler options, work with your application developers and owners to allow them to correctly define their pod specifications.

For more information about using node selectors, see [Assigning Pods to Nodes](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/).

### Node affinity

A node selector is a basic solution for assigning pods to a given node. *Node affinity* provides more flexibility, allowing you to define what happens if the pod can't be matched with a node. You can:

*Require*that Kubernetes scheduler matches a pod with a labeled host. Or,*Prefer*a match but allow the pod to be scheduled on a different host if no match is available.

The following example sets the node affinity to *requiredDuringSchedulingIgnoredDuringExecution*. This affinity requires the Kubernetes schedule to use a node with a matching label. If no node is available, the pod has to wait for scheduling to continue. To allow the pod to be scheduled on a different node, you can instead set the value to * preferredDuringSchedulingIgnoreDuringExecution*:

```
kind: Pod
apiVersion: v1
metadata:
name: app
spec:
containers:
- name: app
image: <your-workload>:gpu
resources:
requests:
cpu: 0.5
memory: 2Gi
limits:
cpu: 4.0
memory: 16Gi
affinity:
nodeAffinity:
requiredDuringSchedulingIgnoredDuringExecution:
nodeSelectorTerms:
- matchExpressions:
- key: hardware
operator: In
values:
- highmem
```


The *IgnoredDuringExecution* part of the setting indicates that the pod shouldn't be evicted from the node if the node labels change. The Kubernetes scheduler only uses the updated node labels for new pods being scheduled, not pods already scheduled on the nodes.

For more information, see [Affinity and anti-affinity](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity).

### Inter-pod affinity and anti-affinity

One final approach for the Kubernetes scheduler to logically isolate workloads is using inter-pod affinity or anti-affinity. These settings define that pods either *shouldn't* or *should* be scheduled on a node that has an existing matching pod. By default, the Kubernetes scheduler tries to schedule multiple pods in a replica set across nodes. You can define more specific rules around this behavior.

For example, you have a web application that also uses an Azure Cache for Redis.

- You use pod anti-affinity rules to request that the Kubernetes scheduler distributes replicas across nodes.
- You use affinity rules to ensure each web app component is scheduled on the same host as a corresponding cache.

The distribution of pods across nodes looks like the following example:

Node 1 |
Node 2 |
Node 3 |
|---|---|---|
| webapp-1 | webapp-2 | webapp-3 |
| cache-1 | cache-2 | cache-3 |

Inter-pod affinity and anti-affinity provide a more complex deployment than node selectors or node affinity. With the deployment, you logically isolate resources and control how Kubernetes schedules pods on nodes.

For a complete example of this web application with Azure Cache for Redis example, see [Co-locate pods on the same node](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#always-co-located-in-the-same-node).

## Next steps

This article focused on advanced Kubernetes scheduler features. For more information about cluster operations in AKS, see the following best practices:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-terraform -->

# Quickstart: Create a Windows-based Azure Kubernetes Service (AKS) cluster using Terraform

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you create an Azure Kubernetes cluster with a Windows node pool using Terraform. Azure Kubernetes Service (AKS) is a managed container orchestration service provided by Azure. It simplifies the deployment, scaling, and operations of containerized applications. The service uses Kubernetes, an open-source system for automating the deployment, scaling, and management of containerized applications. The Windows node pool allows you to run Windows containers in your Kubernetes cluster.

[Terraform](https://www.terraform.io) enables the definition, preview, and deployment of cloud infrastructure. Using Terraform, you create configuration files using [HCL syntax](https://developer.hashicorp.com/terraform/language/syntax/configuration). The HCL syntax allows you to specify the cloud provider - such as Azure - and the elements that make up your cloud infrastructure. After you create your configuration files, you create an *execution plan* that allows you to preview your infrastructure changes before they're deployed. Once you verify the changes, you apply the execution plan to deploy the infrastructure.

- Generate a random resource group name.
- Create an Azure resource group.
- Create an Azure virtual network.
- Create an Azure Kubernetes cluster.
- Create an Azure Kubernetes cluster node pool.

## Prerequisites

Create an Azure account with an active subscription. You can

[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Implement the Terraform code

Note

The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/101-aks-cluster-windows). You can view the log file containing the [test results from current and previous versions of Terraform](https://github.com/Azure/terraform/tree/master/quickstart/101-aks-cluster-windows/TestRecord.md).

See more [articles and sample code showing how to use Terraform to manage Azure resources](/en-us/azure/terraform)

Create a directory in which to test and run the sample Terraform code and make it the current directory.

Create a file named

`providers.tf`

and insert the following code.`terraform { required_version = ">= 1.0" required_providers { azurerm = { source = "hashicorp/azurerm" version = "~>3.0" } random = { source = "hashicorp/random" version = "~>3.0" } } } provider "azurerm" { features { } }`

Create a file named

`main.tf`

and insert the following code.`# Generate random resource group name resource "random_pet" "rg_name" { prefix = var.resource_group_name_prefix } resource "azurerm_resource_group" "rg" { location = var.resource_group_location name = random_pet.rg_name.id } resource "random_pet" "azurerm_kubernetes_cluster_name" { prefix = "cluster" } resource "random_pet" "azurerm_kubernetes_cluster_dns_prefix" { prefix = "dns" } resource "random_string" "azurerm_kubernetes_cluster_node_pool" { length = 6 special = false numeric = false lower = true upper = false } resource "azurerm_virtual_network" "vnet" { name = "myvnet" location = azurerm_resource_group.rg.location resource_group_name = azurerm_resource_group.rg.name address_space = ["10.1.0.0/16"] subnet { name = "subnet1" address_prefix = "10.1.1.0/24" } } resource "azurerm_kubernetes_cluster" "aks" { name = random_pet.azurerm_kubernetes_cluster_name.id location = azurerm_resource_group.rg.location resource_group_name = azurerm_resource_group.rg.name dns_prefix = random_pet.azurerm_kubernetes_cluster_dns_prefix.id identity { type = "SystemAssigned" } default_node_pool { name = "agentpool" vm_size = "Standard_D2_v2" node_count = var.node_count_linux vnet_subnet_id = element(tolist(azurerm_virtual_network.vnet.subnet), 0).id } windows_profile { admin_username = var.admin_username admin_password = var.admin_password } network_profile { network_plugin = "azure" load_balancer_sku = "standard" } } resource "azurerm_kubernetes_cluster_node_pool" "win" { name = random_string.azurerm_kubernetes_cluster_node_pool.result kubernetes_cluster_id = azurerm_kubernetes_cluster.aks.id vm_size = "Standard_D4s_v3" node_count = var.node_count_windows os_type = "Windows" }`

Create a file named

`variables.tf`

and insert the following code.`variable "resource_group_location" { type = string default = "eastus" description = "Location of the resource group." } variable "resource_group_name_prefix" { type = string default = "rg" description = "Prefix of the resource group name that's combined with a random ID so name is unique in your Azure subscription." } variable "node_count_linux" { type = number description = "The initial quantity of Linux nodes for the node pool." default = 1 } variable "node_count_windows" { type = number description = "The initial quantity of Windows nodes for the node pool." default = 1 } variable "admin_username" { type = string description = "The admin username for the Windows node pool." default = "azureuser" } variable "admin_password" { type = string description = "The admin password for the Windows node pool." default = "Passw0rd1234Us!" }`

Create a file named

`outputs.tf`

and insert the following code.`output "resource_group_name" { value = azurerm_resource_group.rg.name } output "kubernetes_cluster_name" { value = azurerm_kubernetes_cluster.aks.name } output "kubernetes_cluster_dns_prefix" { value = azurerm_kubernetes_cluster.aks.dns_prefix } output "kubernetes_cluster_node_pool_name" { value = azurerm_kubernetes_cluster_node_pool.win.name } output "kubernetes_cluster_kube_config_raw" { value = azurerm_kubernetes_cluster.aks.kube_config_raw sensitive = true }`


## Initialize Terraform

Run [terraform init](https://www.terraform.io/docs/commands/init.html) to initialize the Terraform deployment. This command downloads the Azure provider required to manage your Azure resources.

```
terraform init -upgrade
```


**Key points:**

- The
`-upgrade`

parameter upgrades the necessary provider plugins to the newest version that complies with the configuration's version constraints.

## Create a Terraform execution plan

Run [terraform plan](https://www.terraform.io/docs/commands/plan.html) to create an execution plan.

```
terraform plan -out main.tfplan
```


**Key points:**

- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

## Apply a Terraform execution plan

Run [terraform apply](https://www.terraform.io/docs/commands/apply.html) to apply the execution plan to your cloud infrastructure.

```
terraform apply main.tfplan
```


**Key points:**

- The example
`terraform apply`

command assumes you previously ran`terraform plan -out main.tfplan`

. - If you specified a different filename for the
`-out`

parameter, use that same filename in the call to`terraform apply`

. - If you didn't use the
`-out`

parameter, call`terraform apply`

without any parameters.

## Verify the results

Run [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) to print the cluster's nodes.

```
kubectl get node -o wide
```


## Clean up resources

When you no longer need the resources created via Terraform, do the following steps:

Run

[terraform plan](https://www.terraform.io/docs/commands/plan.html)and specify the`destroy`

flag.`terraform plan -destroy -out main.destroy.tfplan`

**Key points:**- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

- The
Run

[terraform apply](https://www.terraform.io/docs/commands/apply.html)to apply the execution plan.`terraform apply main.destroy.tfplan`


## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure](/en-us/azure/developer/terraform/troubleshoot).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-portal -->

# Deploy a Windows Server container on an Azure Kubernetes Service (AKS) cluster using the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this article, you deploy an AKS cluster that runs Windows Server containers using the Azure portal. You also deploy an ASP.NET sample application in a Windows Server container to the cluster.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - If you're unfamiliar with the Azure Cloud Shell, review
[Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview). - Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Create an AKS cluster

Sign in to the

[Azure portal](https://portal.azure.com).On the Azure portal home page, select

**Create a resource**.In the

**Categories**section, select**Containers**>**Azure Kubernetes Service (AKS)**.On the

**Basics**tab, configure the following settings:- Under
**Project details**:**Subscription**: Select the Azure subscription you want to use for this AKS cluster.**Resource group**: Select**Create new**, enter a resource group name, such as*myResourceGroup*, and then select**Ok**. While you can select an existing resource group, for testing or evaluation purposes, we recommend creating a resource group to temporarily host these resources and avoid impacting your production or development workloads.

- Under
**Cluster details**:**Cluster preset configuration**: Select**Dev/Test**. For more details on preset configurations, see[Cluster configuration presets in the Azure portal](../quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal).**Kubernetes cluster name**: Enter a cluster name, such as*myAKSCluster*.**Region**: Select a region, such as*East US 2*.**Availability zones**: Select**None**.**AKS pricing tier**: Select**Free**.Leave the default values for the remaining settings, and select

**Next**.


- Under
On the

**Node pools**tab, configure the following settings:Select

**Add node pool**and enter a**Node pool name**, such as*npwin*. For a Windows node pool, the name must be*six characters or fewer*.**Mode**: Select**User**.**OS SKU**: Select**Windows 2022**.**Availability zones**: Select**None**.Leave the

**Enable Azure Spot instances**checkbox unchecked.**Node size**: Select**Choose a size**. On the**Select a VM size**page, select**D2s_v3**, and then select**Select**.Leave the default values for the remaining settings, and select

**Add**.

Select

**Review + create**to run validation on the cluster configuration. After validation completes, select**Create**.It takes a few minutes to create the AKS cluster. When your deployment is complete, navigate to your resource by selecting

**Go to resource**, or by browsing to the AKS cluster resource group and selecting the AKS resource.

## Connect to the cluster

You use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client, to manage your Kubernetes clusters. `kubectl`

is already installed if you use Azure Cloud Shell. If you're unfamiliar with the Cloud Shell, review [Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview).

Open Cloud Shell by selecting the

`>_`

button at the top of the Azure portal page.Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. The following command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

`kubectl get nodes`

command, which returns a list of the cluster nodes.`kubectl get nodes`

The following sample output shows all the nodes in the cluster. Make sure the status of all nodes is

*Ready*:`NAME STATUS ROLES AGE VERSION aks-agentpool-11741175-vmss000000 Ready agent 8m17s v1.29.9 aks-agentpool-11741175-vmss000001 Ready agent 8m17s v1.29.9 aksnpwin000000 Ready agent 8m17s v1.29.9 aks-userpool-11741175-vmss000000 Ready agent 8m17s v1.29.9 aks-userpool-11741175-vmss000001 Ready agent 8m17s v1.29.9`


## Deploy the application

A Kubernetes manifest file defines a desired state for the cluster, such as which container images to run. In this quickstart, you use a manifest file to create all objects needed to run the ASP.NET sample application in a Windows Server container. This manifest file includes a [Kubernetes deployment](../concepts-clusters-workloads#deployments-and-yaml-manifests) for the ASP.NET sample application and an external [Kubernetes service](../concepts-network-services) to access the application from the internet.

The ASP.NET sample application is provided as part of the [.NET Framework Samples](https://hub.docker.com/_/microsoft-dotnet-framework-samples/) and runs in a Windows Server container. The Kubernetes manifest file must define a [node selector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) to tell your AKS cluster to run your ASP.NET sample application's pod on a node that can run Windows Server containers.

Create a file named

`sample.yaml`

and paste in the following YAML definition.`apiVersion: apps/v1 kind: Deployment metadata: name: sample labels: app: sample spec: replicas: 1 template: metadata: name: sample labels: app: sample spec: nodeSelector: "kubernetes.io/os": windows containers: - name: sample image: mcr.microsoft.com/dotnet/framework/samples:aspnetapp resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 selector: matchLabels: app: sample --- apiVersion: v1 kind: Service metadata: name: sample spec: type: LoadBalancer ports: - protocol: TCP port: 80 selector: app: sample`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f sample.yaml`

The following sample output shows the deployment and service created successfully:

`deployment.apps/sample created service/sample created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete. Occasionally, the service can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

Check the status of the deployed pods using the

command. Make all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service sample --watch`

Initially, the output shows the

*EXTERNAL-IP*for the sample service as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE sample LoadBalancer 10.0.37.27 <pending> 80:30572/TCP 6s`

When the

*EXTERNAL-IP*address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.See the sample app in action by opening a web browser to the external IP address of your service.


## Delete resources

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), you should delete your cluster to avoid incurring Azure charges.

In the Azure portal, navigate to your resource group.

Select

**Delete resource group**.Enter the name of your resource group to confirm deletion and select

**Delete**.In the

**Delete confirmation**dialog box, select**Delete**.Note

The AKS cluster was created with system-assigned managed identity (default identity option used in this quickstart), the identity is managed by the platform and does not require removal.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed an ASP.NET sample application in a Windows Server container to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS, and to walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-powershell -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using Azure PowerShell

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Deploy an AKS cluster using Azure PowerShell.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This article assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. For ease of use, try the PowerShell environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Quickstart for Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you want to use PowerShell locally, then install the

[Az PowerShell](/en-us/powershell/azure/new-azureps-module-az)module and connect to your Azure account using the[Connect-AzAccount](/en-us/powershell/module/az.accounts/Connect-AzAccount)cmdlet. Make sure that you run the commands with administrative privileges. For more information, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps).Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).If you have more than one Azure subscription, set the subscription that you wish to use for the quickstart by calling the

[Set-AzContext](/en-us/powershell/module/az.accounts/set-azcontext)cmdlet. For more information, see[Manage Azure subscriptions with Azure PowerShell](/en-us/powershell/azure/manage-subscriptions-azureps#change-the-active-subscription).

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the

cmdlet.`New-AzResourceGroup`

`New-AzResourceGroup -Name myResourceGroup -Location eastus`

The following example output resembles successful creation of the resource group:

`ResourceGroupName : myResourceGroup Location : eastus ProvisioningState : Succeeded Tags : ResourceId : /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup`


## Create AKS cluster

To create an AKS cluster, use the [ New-AzAksCluster](/en-us/powershell/module/az.aks/new-azakscluster) cmdlet. The following example creates a cluster named

*myAKSCluster*with one node and enables a system-assigned managed identity.

```
New-AzAksCluster -ResourceGroupName myResourceGroup `
-Name myAKSCluster `
-NodeCount 1 `
-EnableManagedIdentity `
-GenerateSshKey
```


After a few minutes, the command completes and returns information about the cluster.

Note

When you create an AKS cluster, a second resource group called the *node resource group* is automatically created to store the AKS resources. For more information, see [Node resource group](../core-aks-concepts#node-resource-group). When you [delete the resource group](#delete-resources) for the AKS cluster, the node resource group is also deleted. You also see a *NetworkWatcherRG* resource group created by default. This resource group is used by Azure Network Watcher to store monitoring data. You can safely ignore this resource group. For more information, see [Enable or disable Azure Network Watcher](/en-us/azure/network-watcher/network-watcher-create).

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, call the `Install-AzAksCliTool`

cmdlet.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecmdlet. This command downloads credentials and configures the Kubernetes CLI to use them.`Import-AzAksCredential`

`Import-AzAksCredential -ResourceGroupName myResourceGroup -Name myAKSCluster`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the single node created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-nodepool1-11853318-vmss000000 Ready agent 2m26s v1.27.7`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Create a file named

`aks-store-quickstart.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: rabbitmq spec: replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 resources: requests: cpu: 1m memory: 1Mi limits: cpu: 1m memory: 7Mi --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make all pods are`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete resources

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges. Remove the resource group, container service, and all related resources by calling the [ Remove-AzResourceGroup](/en-us/powershell/module/az.resources/remove-azresourcegroup) cmdlet.

```
Remove-AzResourceGroup -Name myResourceGroup
```


Note

The AKS cluster was created with system-assigned managed identity (default identity option used in this quickstart), the identity is managed by the platform and doesn't require removal.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-portal -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Deploy an AKS cluster using the Azure portal.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - If you're unfamiliar with the Azure Cloud Shell, review
[Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview). - Make sure that the identity you use to create your cluster has the appropriate minimum permissions. For more information about access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Create an AKS cluster

Sign in to the

[Azure portal](https://portal.azure.com).On the Azure portal home page, select

**Create a resource**.In the

**Categories**section, select**Infrastructure Services**>**Azure Kubernetes Service (AKS)**.On the

**Basics**tab, configure the following settings:Under

**Project details**:**Subscription**: Select the Azure subscription you want to use for this AKS cluster.**Resource group**: Select**Create new**, enter a resource group name, like*myResourceGroup*, and then select**Ok**. While you can select an existing resource group, for testing or evaluation purposes, we recommend creating a resource group to temporarily host these resources and avoid impacting your production or development workloads.

Under

**Cluster details**:**Cluster preset configuration**: Select**Dev/Test**. For more details about preset configurations, see[Cluster configuration presets in the Azure portal](../quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal). You can change the preset configuration when creating your cluster by selecting**Compare presets**and choosing a different option.


On the

**Node pools**tab, configure the following settings:Select

**Add node pool**and select**Add a Virtual Machine Scale Set node pool****Name**: Enter a name like*nplinux*.**Mode**: Select**User**.**OS SKU**: Select**Ubuntu Linux**.**Availability zones**: Select**None**.Leave the

**Enable Azure Spot instances**checkbox unchecked.**Node size**: Select**Choose a size**. On the**Select a VM size**page, search for**D2s_v5**, select that VM size, and**Select**.Use the default values for the remaining settings, and select

**Add**.

Select

**Review + create**to run validation on the cluster configuration. After validation completes, select**Create**.It takes a few minutes to create the AKS cluster. When your deployment is complete, navigate to your resource by selecting

**Go to resource**, or by browsing to the AKS cluster resource group and selecting the AKS resource.

## Connect to the cluster

You use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/), to manage Kubernetes clusters. `kubectl`

is already installed if you use Azure Cloud Shell. If you're unfamiliar with the Cloud Shell, review [Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview).

If you're using Cloud Shell, open it with the `>_`

button on the top of the Azure portal. If you're using PowerShell locally, connect to Azure via the `Connect-AzAccount`

command. If you're using Azure CLI locally, connect to Azure via the `az login`

command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using

`kubectl get`

to return a list of the cluster nodes.`kubectl get nodes`

The following example output shows the single node created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-nodepool1-31718369-0 Ready agent 6m44s v1.15.10`


## Deploy the application

You use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A Kubernetes manifest file defines a cluster's desired state, like which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, like Rabbit MQ, without persistent storage for production. These containers are used here for simplicity, but we recommend using managed services, like Azure Cosmos DB or Azure Service Bus.

In the Cloud Shell, open an editor and create a file named

`aks-store-quickstart.yaml`

.Paste the following manifest into the editor:

`apiVersion: apps/v1 kind: StatefulSet metadata: name: rabbitmq spec: serviceName: rabbitmq replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 env: - name: AI_SERVICE_URL value: "http://ai-service:5001/" resources: requests: cpu: 1m memory: 1Mi limits: cpu: 2m memory: 20Mi readinessProbe: httpGet: path: /health port: 3002 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3002 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi startupProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 5 periodSeconds: 5 readinessProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 3 livenessProbe: httpGet: path: /health port: 8080 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest:`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

command. Make sure all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the

`store-front`

application. Monitor progress using thecommand with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial series](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges.

In the Azure portal, navigate to your AKS cluster resource group.

Select

**Delete resource group**.Enter the name of the resource group to delete, and then select

**Delete**>**Delete**.Note

The AKS cluster was created with a system-assigned managed identity. This identity is managed by the platform and doesn't require removal.


## Next steps

In this quickstart, you deployed a Kubernetes cluster, and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial series.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you learn how to:

- Deploy an AKS cluster using the Azure CLI.
- Run a sample multi-container application with a group of microservices and web front ends that simulate a retail scenario.

Note

This article includes steps to deploy a cluster with default settings for evaluation purposes only. Before you deploy a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more information on access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
[az account set](/en-us/cli/azure/account#az-account-set)command. For more information, see[How to manage Azure subscriptions – Azure CLI](/en-us/cli/azure/manage-azure-subscriptions-azure-cli?tabs=bash#change-the-active-subscription). - Dependent upon your Azure subscription, you might need to request a vCPU quota increase. For more information, see
[Increase VM-family vCPU quotas](/en-us/azure/quotas/per-vm-quota-requests).

## Register resource providers

You might need to register resource providers in your Azure subscription. For example, `Microsoft.ContainerService`

is required.

Run the following command to check the registration status.

```
az provider show --namespace Microsoft.ContainerService --query registrationState
```


If necessary, register the resource provider.

```
az provider register --namespace Microsoft.ContainerService
```


## Define environment variables

Define the following environment variables for use throughout this quickstart.

```
export RANDOM_ID="$(openssl rand -hex 3)"
export MY_RESOURCE_GROUP_NAME="myAKSResourceGroup$RANDOM_ID"
export REGION="westus"
export MY_AKS_CLUSTER_NAME="myAKSCluster$RANDOM_ID"
export MY_DNS_LABEL="mydnslabel$RANDOM_ID"
```


The `RANDOM_ID`

variable's value is a six character alphanumeric value appended to the resource group and cluster name so that the names are unique. Use the `echo`

command to view variable values like `echo $RANDOM_ID`

.

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

Create a resource group using the [az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name $MY_RESOURCE_GROUP_NAME --location $REGION
```


The result looks like the following example.

```
{
"id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myAKSResourceGroup<randomIDValue>",
"location": "westus",
"managedBy": null,
"name": "myAKSResourceGroup<randomIDValue>",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


## Create an AKS cluster

Create an AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a cluster with one node and enables a system-assigned managed identity.

```
az aks create \
--resource-group $MY_RESOURCE_GROUP_NAME \
--name $MY_AKS_CLUSTER_NAME \
--node-count 1 \
--generate-ssh-keys
```


Note

When you create a new cluster, AKS automatically creates a second resource group to store the AKS resources. For more information, see [Why are two resource groups created with AKS?](../faq)

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, use the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials --resource-group $MY_RESOURCE_GROUP_NAME --name $MY_AKS_CLUSTER_NAME`

Verify the connection to your cluster using the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. This command returns a list of the cluster nodes.`kubectl get nodes`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A Kubernetes manifest file defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

- Store front: Web application for customers to view products and place orders.
- Product service: Shows product information.
- Order service: Places orders.
`RabbitMQ`

: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as `RabbitMQ`

, without persistent storage for production. We use it here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Create a file named

*aks-store-quickstart.yaml*and copy in the following manifest.`apiVersion: apps/v1 kind: StatefulSet metadata: name: rabbitmq spec: serviceName: rabbitmq replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 env: - name: AI_SERVICE_URL value: "http://ai-service:5001/" resources: requests: cpu: 1m memory: 1Mi limits: cpu: 2m memory: 20Mi readinessProbe: httpGet: path: /health port: 3002 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3002 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi startupProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 5 periodSeconds: 5 readinessProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 3 livenessProbe: httpGet: path: /health port: 8080 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in Cloud Shell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest.`kubectl apply -f aks-store-quickstart.yaml`


## Test the application

You can validate that the application is running by visiting the public IP address or the application URL.

Get the application URL using the following commands:

```
runtime="5 minutes"
endtime=$(date -ud "$runtime" +%s)
while [[ $(date -u +%s) -le $endtime ]]
do
STATUS=$(kubectl get pods -l app=store-front -o 'jsonpath={..status.conditions[?(@.type=="Ready")].status}')
echo $STATUS
if [ "$STATUS" == 'True' ]
then
export IP_ADDRESS=$(kubectl get service store-front --output 'jsonpath={..status.loadBalancer.ingress[0].ip}')
echo "Service IP Address: $IP_ADDRESS"
break
else
sleep 10
fi
done
```


```
curl $IP_ADDRESS
```


Results:

```
<!doctype html>
<html lang="">
<head>
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width,initial-scale=1">
<link rel="icon" href="/favicon.ico">
<title>store-front</title>
<script defer="defer" src="/js/chunk-vendors.df69ae47.js"></script>
<script defer="defer" src="/js/app.7e8cfbb2.js"></script>
<link href="/css/app.a5dc49f6.css" rel="stylesheet">
</head>
<body>
<div id="app"></div>
</body>
</html>
```


```
echo "You can now visit your web server at $IP_ADDRESS"
```


To view the application website, open a browser and enter the IP address. The page looks like the following example.

## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure billing charges. You can remove the resource group, container service, and all related resources using the [az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name $MY_RESOURCE_GROUP_NAME
```


The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance about how to create full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and do a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-flatcar-deploy-cli -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you learn how to:

- Create an AKS cluster using Flatcar Container Linux for AKS (preview).
- Deploy an AKS cluster using the Azure CLI.
- Run a sample multi-container application with a group of microservices and web front ends that simulate a retail scenario.

Note

This article includes steps to deploy a cluster with default settings for evaluation purposes only. Before you deploy a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more information on access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command. For more information, see`az account set`

[How to manage Azure subscriptions – Azure CLI](/en-us/cli/azure/manage-azure-subscriptions-azure-cli?tabs=bash#change-the-active-subscription). - Dependent upon your Azure subscription, you might need to request a vCPU quota increase. For more information, see
[Increase VM-family vCPU quotas](/en-us/azure/quotas/per-vm-quota-requests).

## Register resource providers

You might need to register resource providers in your Azure subscription. For example, `Microsoft.ContainerService`

is required.

Check the registration status using the [ az provider show](/en-us/cli/azure/provider#az-provider-show) command.

```
az provider show --namespace Microsoft.ContainerService --query registrationState
```


If necessary, register the resource provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command.

```
az provider register --namespace Microsoft.ContainerService
```


## Install `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Flatcar Container Linux requires a minimum of 18.0.0b42**.`az extension update --name aks-preview`


## Register `AKSFlatcarPreview`

feature flag

Register the

`AKSFlatcarPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AKSFlatcarPreview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AKSFlatcarPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Define environment variables

- Define the following environment variables for use throughout this quickstart:

```
export RANDOM_ID="$(openssl rand -hex 3)"
export MY_RESOURCE_GROUP_NAME="myAKSResourceGroup$RANDOM_ID"
export REGION="westus"
export MY_AKS_CLUSTER_NAME="myAKSCluster$RANDOM_ID"
```


The `RANDOM_ID`

variable's value is a six-character alphanumeric value appended to the resource group and cluster name so that the names are unique. Use the `echo`

command to view variable values like `echo $RANDOM_ID`

.

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

- Create a resource group using the
command.`az group create`


```
az group create \
--name $MY_RESOURCE_GROUP_NAME \
--location $REGION
```


Example output:

```
{
"id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myAKSResourceGroup<randomIDValue>",
"location": "westus",
"managedBy": null,
"name": "myAKSResourceGroup<randomIDValue>",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


## Create an AKS cluster

- Create an AKS cluster using the
command. The following example creates a cluster with one node and enables a system-assigned managed identity:`az aks create`


```
az aks create \
--resource-group $MY_RESOURCE_GROUP_NAME \
--name $MY_AKS_CLUSTER_NAME \
--os-sku flatcar \
--node-count 1 \
--generate-ssh-keys
```


Note

When you create a new cluster, AKS automatically creates a second resource group to store the AKS resources. For more information, see [Why are two resource groups created with AKS?](../faq)

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials \ --resource-group $MY_RESOURCE_GROUP_NAME \ --name $MY_AKS_CLUSTER_NAME`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A Kubernetes manifest file defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

- Store front: Web application for customers to view products and place orders.
- Product service: Shows product information.
- Order service: Places orders.
`RabbitMQ`

: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as `RabbitMQ`

, without persistent storage for production. We use it here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a file named

*aks-store-quickstart.yaml*and copy in the following manifest.`apiVersion: apps/v1 kind: StatefulSet metadata: name: rabbitmq spec: serviceName: rabbitmq replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 env: - name: AI_SERVICE_URL value: "http://ai-service:5001/" resources: requests: cpu: 1m memory: 1Mi limits: cpu: 2m memory: 20Mi readinessProbe: httpGet: path: /health port: 3002 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3002 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi startupProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 5 periodSeconds: 5 readinessProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 3 livenessProbe: httpGet: path: /health port: 8080 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in Cloud Shell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

command. Make sure all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the

`store-front`

application. Monitor progress using thecommand with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure billing charges.

Remove the resource group, container service, and all related resources using the

command.`az group delete`

`az group delete --name $MY_RESOURCE_GROUP_NAME`

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity so you don't need to manually remove it.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance about how to create full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and do a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-powershell -->

# Deploy a Windows Server container on an Azure Kubernetes Service (AKS) cluster using PowerShell

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this article, you use Azure PowerShell to deploy an AKS cluster that runs Windows Server containers. You also deploy an ASP.NET sample application in a Windows Server container to the cluster.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. For ease of use, try the PowerShell environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Quickstart for Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you want to use PowerShell locally, then install the

[Az PowerShell](/en-us/powershell/azure/new-azureps-module-az)module and connect to your Azure account using the[Connect-AzAccount](/en-us/powershell/module/az.accounts/Connect-AzAccount)cmdlet. Make sure that you run the commands with administrative privileges. For more information, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps).Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).If you have more than one Azure subscription, set the subscription that you wish to use for the quickstart by calling the

[Set-AzContext](/en-us/powershell/module/az.accounts/set-azcontext)cmdlet. For more information, see[Manage Azure subscriptions with Azure PowerShell](/en-us/powershell/azure/manage-subscriptions-azureps#change-the-active-subscription).If you're using osSku

`Windows2025`

, you need to install the`aks-preview`

extension and register the preview flag.Specifying the

`OsSKU`

parameter requires PowerShell Az module version 9.2.0 or higher.

### Install the `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

- Install the
`aks-preview`

Azure CLI extension using thecommand.`az extension add`


```
az extension add --name aks-preview
```


- Update to the latest version of the extension using the
command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b40**.

```
az extension update --name aks-preview
```


### Register the `AksWindows2025Preview`

feature flag

- Register the
`AksWindows2025Preview`

feature flag using the [`az feature register`

][az-feature-register] command.

```
az feature register --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


- Verify the registration status using the [
`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.

```
az feature show --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're asked to specify a location. This location is where resource group metadata is stored and where your resources run in Azure if you don't specify another region during resource creation.

Create a resource group using the

cmdlet. The following example creates a resource group named`New-AzResourceGroup`

*myResourceGroup*in the*eastus*region.`New-AzResourceGroup -Name myResourceGroup -Location eastus`

The following example output shows that the resource group was created successfully:

`ResourceGroupName : myResourceGroup Location : eastus ProvisioningState : Succeeded Tags : ResourceId : /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup`


## Create an AKS cluster

In this section, we create an AKS cluster with the following configuration:

- The cluster is configured with two nodes to ensure it operates reliably. A
[node](../concepts-clusters-workloads#nodes)is an Azure virtual machine (VM) that runs the Kubernetes node components and container runtime. - The
`-WindowsProfileAdminUserName`

and`-WindowsProfileAdminUserPassword`

parameters set the administrator credentials for any Windows Server nodes on the cluster and must meet the[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference). - The node pool uses
`VirtualMachineScaleSets`

.

Use the following steps to create the AKS cluster with Azure PowerShell:

Create the administrator credentials for your Windows Server containers using the following command. This command prompts you to enter a

`WindowsProfileAdminUserName`

and`WindowsProfileAdminUserPassword`

. The password must be a minimum of 14 characters and meet the[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).`$AdminCreds = Get-Credential ` -Message 'Please create the administrator credentials for your Windows Server containers'`

Create your cluster using the

cmdlet and specify the`New-AzAksCluster`

`WindowsProfileAdminUserName`

and`WindowsProfileAdminUserPassword`

parameters.`New-AzAksCluster -ResourceGroupName myResourceGroup ` -Name myAKSCluster ` -NodeCount 2 ` -NetworkPlugin azure ` -NodeVmSetType VirtualMachineScaleSets ` -WindowsProfileAdminUserName $AdminCreds.UserName ` -WindowsProfileAdminUserPassword $secureString ` -GenerateSshKey`

After a few minutes, the command completes and returns JSON-formatted information about the cluster. Occasionally, the cluster can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

If you get a password validation error, and the password that you set meets the length and complexity requirements, try creating your resource group in another region. Then try creating the cluster with the new resource group.

If you don't specify an administrator username and password when creating the node pool, the username is set to

*azureuser*and the password is set to a random value. For more information, see the[Windows Server FAQ](../windows-faq).The administrator username can't be changed, but you can change the administrator password that your AKS cluster uses for Windows Server nodes using

`az aks update`

. For more information, see the[Windows Server FAQ](../windows-faq).To run an AKS cluster that supports node pools for Windows Server containers, your cluster needs to use a network policy that uses

[Azure CNI (advanced)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md)network plugin. The`-NetworkPlugin azure`

parameter specifies Azure CNI.

## Add a node pool

By default, an AKS cluster is created with a node pool that can run Linux containers. You must add another node pool that can run Windows Server containers alongside the Linux node pool.

To create a Windows node pool, you need to specify a supported `OsType`

and `OsSku`

. Use the information in the following table to determine which is appropriate for your cluster:

`OsType` |
`OsSku` |
Default | Supported K8s versions | Details |
|---|---|---|---|---|
`windows` |
`Windows2025` |
Currently in preview. Not default. | 1.32+ | Updated defaults: containerd 2.0, Generation 2 image is used by default. |
`windows` |
`Windows2022` |
Default in K8s 1.25-1.35 | Not available in K8s 1.36+ | Retires in March 2027. Updated defaults: FIPS is enabled by default. |
`windows` |
`Windows2019` |
Default in K8s 1.24 and below | Not available in K8s 1.33+ | Retires in March 2026. |

Windows Server 2022 is the default operating system for Kubernetes versions 1.25-1.35. Windows Server 2019 is the default OS for earlier versions. If you don't specify a particular OS SKU, Azure creates the new node pool with the default SKU for the version of Kubernetes used by the cluster.

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Add a Windows Server node pool using the

cmdlet. The following command creates a new node pool named`New-AzAksNodePool`

*npwin*and adds it to*myAKSCluster*. The command also uses the default subnet in the default virtual network created when running`New-AzAksCluster`

:`New-AzAksNodePool -ResourceGroupName myResourceGroup ` -ClusterName myAKSCluster ` -VmSetType VirtualMachineScaleSets ` -OsType Windows ` -OsSKU Windows2022 ` -Name npwin`


## Connect to the cluster

You use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client, to manage your Kubernetes clusters. If you use Azure Cloud Shell, `kubectl`

is already installed. If you want to install `kubectl`

locally, you can use the `Install-AzAzAksCliTool`

cmdlet.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecmdlet. This command downloads credentials and configures the Kubernetes CLI to use them.`Import-AzAksCredential`

`Import-AzAksCredential -ResourceGroupName myResourceGroup -Name myAKSCluster`

Verify the connection to your cluster using the

command, which returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows all the nodes in the cluster. Make sure the status of all nodes is

**Ready**:`NAME STATUS ROLES AGE VERSION aks-nodepool1-20786768-vmss000000 Ready agent 22h v1.27.7 aks-nodepool1-20786768-vmss000001 Ready agent 22h v1.27.7 aksnpwin000000 Ready agent 21h v1.27.7`


## Deploy the application

A Kubernetes manifest file defines a desired state for the cluster, such as what container images to run. In this article, you use a manifest to create all objects needed to run the ASP.NET sample application in a Windows Server container. This manifest includes a [Kubernetes deployment](../concepts-clusters-workloads#deployments-and-yaml-manifests) for the ASP.NET sample application and an external [Kubernetes service](../concepts-network-services) to access the application from the internet.

The ASP.NET sample application is provided as part of the [.NET Framework Samples](https://hub.docker.com/_/microsoft-dotnet-framework-samples/) and runs in a Windows Server container. AKS requires Windows Server containers to be based on images of *Windows Server 2019* or greater. The Kubernetes manifest file must also define a [node selector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) to tell your AKS cluster to run your ASP.NET sample application's pod on a node that can run Windows Server containers.

Create a file named

`sample.yaml`

and copy in the following YAML definition:`apiVersion: apps/v1 kind: Deployment metadata: name: sample labels: app: sample spec: replicas: 1 template: metadata: name: sample labels: app: sample spec: nodeSelector: "kubernetes.io/os": windows containers: - name: sample image: mcr.microsoft.com/dotnet/framework/samples:aspnetapp resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 selector: matchLabels: app: sample --- apiVersion: v1 kind: Service metadata: name: sample spec: type: LoadBalancer ports: - protocol: TCP port: 80 selector: app: sample`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f sample.yaml`

The following example output shows the deployment and service created successfully:

`deployment.apps/sample created service/sample created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete. Occasionally, the service can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

Check the status of the deployed pods using the

command. Make all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service sample --watch`

Initially, the output shows the

*EXTERNAL-IP*for the sample service as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE sample LoadBalancer 10.0.37.27 <pending> 80:30572/TCP 6s`

When the

*EXTERNAL-IP*address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`sample LoadBalancer 10.0.37.27 52.179.23.131 80:30572/TCP 2m`

See the sample app in action by opening a web browser to the external IP address of your service.


## Delete resources

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), then delete your cluster to avoid incurring Azure charges.

Remove the resource group, container service, and all related resources using the

cmdlet.`Remove-AzResourceGroup`

`Remove-AzResourceGroup -Name myResourceGroup`

Note

The AKS cluster was created with system-assigned managed identity (default identity option used in this quickstart). The Azure platform manages this identity, so it doesn't require removal.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed an ASP.NET sample application in a Windows Server container to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS, and to walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Deploy an AKS cluster using an Azure Resource Manager template.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

An [Azure Resource Manager template](/en-us/azure/azure-resource-manager/templates/overview) is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This article assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. Make sure that the identity you use to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine, you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

After you deploy the cluster from the template, you can use either Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


This article requires Azure CLI version 2.0.64 or later. If you're using Azure Cloud Shell, the latest version is already installed there.

### Create an SSH key pair

To create an AKS cluster using an ARM template, you provide an SSH public key. If you need this resource, follow the steps in this section. Otherwise, skip to the [Review the template](#review-the-template) section.

To access AKS nodes, you connect using an SSH key pair (public and private). To create an SSH key pair:

Go to

[https://shell.azure.com](https://shell.azure.com)to open Cloud Shell in your browser.Create an SSH key pair using the

[az sshkey create](/en-us/cli/azure/sshkey#az-sshkey-create)command or the`ssh-keygen`

command.`# Create an SSH key pair using Azure CLI az sshkey create --name "mySSHKey" --resource-group "myResourceGroup" # or # Create an SSH key pair using ssh-keygen ssh-keygen -t rsa -b 4096`

To deploy the template, you must provide the public key from the SSH pair. To retrieve the public key, call

[az sshkey show](/en-us/cli/azure/sshkey#az-sshkey-show):`az sshkey show --name "mySSHKey" --resource-group "myResourceGroup" --query "publicKey"`


By default, the SSH key files are created in the *~/.ssh* directory. Running the `az sshkey create`

or `ssh-keygen`

command will overwrite any existing SSH key pair with the same name.

For more information about creating SSH keys, see [Create and manage SSH keys for authentication in Azure](/en-us/azure/virtual-machines/linux/create-ssh-keys-detailed).

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/aks/).

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"metadata": {
"_generator": {
"name": "bicep",
"version": "0.26.170.59819",
"templateHash": "14823542069333410776"
}
},
"parameters": {
"clusterName": {
"type": "string",
"defaultValue": "aks101cluster",
"metadata": {
"description": "The name of the Managed Cluster resource."
}
},
"location": {
"type": "string",
"defaultValue": "[resourceGroup().location]",
"metadata": {
"description": "The location of the Managed Cluster resource."
}
},
"dnsPrefix": {
"type": "string",
"metadata": {
"description": "Optional DNS prefix to use with hosted Kubernetes API server FQDN."
}
},
"osDiskSizeGB": {
"type": "int",
"defaultValue": 0,
"minValue": 0,
"maxValue": 1023,
"metadata": {
"description": "Disk size (in GB) to provision for each of the agent pool nodes. This value ranges from 0 to 1023. Specifying 0 will apply the default disk size for that agentVMSize."
}
},
"agentCount": {
"type": "int",
"defaultValue": 3,
"minValue": 1,
"maxValue": 50,
"metadata": {
"description": "The number of nodes for the cluster."
}
},
"agentVMSize": {
"type": "string",
"defaultValue": "standard_d2s_v3",
"metadata": {
"description": "The size of the Virtual Machine."
}
},
"linuxAdminUsername": {
"type": "string",
"metadata": {
"description": "User name for the Linux Virtual Machines."
}
},
"sshRSAPublicKey": {
"type": "string",
"metadata": {
"description": "Configure all linux machines with the SSH RSA public key string. Your key should include three parts, for example 'ssh-rsa AAAAB...snip...UcyupgH azureuser@linuxvm'"
}
}
},
"resources": [
{
"type": "Microsoft.ContainerService/managedClusters",
"apiVersion": "2024-02-01",
"name": "[parameters('clusterName')]",
"location": "[parameters('location')]",
"identity": {
"type": "SystemAssigned"
},
"properties": {
"dnsPrefix": "[parameters('dnsPrefix')]",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": "[parameters('osDiskSizeGB')]",
"count": "[parameters('agentCount')]",
"vmSize": "[parameters('agentVMSize')]",
"osType": "Linux",
"mode": "System"
}
],
"linuxProfile": {
"adminUsername": "[parameters('linuxAdminUsername')]",
"ssh": {
"publicKeys": [
{
"keyData": "[parameters('sshRSAPublicKey')]"
}
]
}
}
}
}
],
"outputs": {
"controlPlaneFQDN": {
"type": "string",
"value": "[reference(resourceId('Microsoft.ContainerService/managedClusters', parameters('clusterName')), '2024-02-01').fqdn]"
}
}
}
```


The resource type defined in the ARM template is [ Microsoft.ContainerService/managedClusters](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template).

For more AKS samples, see the [AKS quickstart templates](https://azure.microsoft.com/resources/templates/?term=Azure+Kubernetes+Service) site.

## Deploy the template

Select

**Deploy to Azure**to sign in and open a template.On the

**Basics**page, leave the default values for the*OS Disk Size GB*,*Agent Count*,*Agent VM Size*, and*OS Type*, and configure the following template parameters:**Subscription**: Select an Azure subscription.**Resource group**: Select**Create new**. Enter a unique name for the resource group, such as*myResourceGroup*, then select**OK**.**Location**: Select a location, such as**East US**.**Cluster name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**DNS prefix**: Enter a unique DNS prefix for your cluster, such as*myakscluster*.**Linux Admin Username**: Enter a username to connect using SSH, such as*azureuser*.**SSH public key source**: Select**Use existing public key**.**Key pair name**: Copy and paste the*public*part of your SSH key pair (by default, the contents of*~/.ssh/id_rsa.pub*).

Select

**Review + Create**>**Create**.

It takes a few minutes to create the AKS cluster. Wait for the cluster to be successfully deployed before you move on to the next step.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/).

If you use Azure Cloud Shell, `kubectl`

is already installed. To install and run `kubectl`

locally, call the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. This command returns a list of the cluster nodes.`kubectl get nodes`

The following example output shows the three nodes created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-agentpool-27442051-vmss000000 Ready agent 10m v1.27.7 aks-agentpool-27442051-vmss000001 Ready agent 10m v1.27.7 aks-agentpool-27442051-vmss000002 Ready agent 11m v1.27.7`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Create a file named

`aks-store-quickstart.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: rabbitmq spec: replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 resources: requests: cpu: 1m memory: 1Mi limits: cpu: 1m memory: 7Mi --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make all pods are`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges.

Remove the resource group, container service, and all related resources by calling the [az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name myResourceGroup --yes --no-wait
```


Note

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-cli -->

# Deploy a Windows Server container on an Azure Kubernetes Service (AKS) cluster using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this article, you use Azure CLI to deploy an AKS cluster that runs Windows Server containers. You also deploy an ASP.NET sample application in a Windows Server container to the cluster.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.0.64 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more information about access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command. For more information, see`az account set`

[How to manage Azure subscriptions – Azure CLI](/en-us/cli/azure/manage-azure-subscriptions-azure-cli?tabs=bash#change-the-active-subscription). - If you're using
`--os-sku Windows2025`

, you need to install the`aks-preview`

extension and register the preview flag. The minimum version is 18.0.0b40.

### Install the `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

- Install the
`aks-preview`

Azure CLI extension using thecommand.`az extension add`


```
az extension add --name aks-preview
```


- Update to the latest version of the extension using the
command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b40**.

```
az extension update --name aks-preview
```


### Register the `AksWindows2025Preview`

feature flag

- Register the
`AksWindows2025Preview`

feature flag using the [`az feature register`

][az-feature-register] command.

```
az feature register --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


- Verify the registration status using the [
`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.

```
az feature show --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're asked to specify a location. This location is where resource group metadata is stored and where your resources run in Azure if you don't specify another region during resource creation.

Create a resource group using the

command. The following example creates a resource group named`az group create`

*myResourceGroup*in the*WestUS2*location.`export RANDOM_SUFFIX=$(openssl rand -hex 3) export REGION="canadacentral" export MY_RESOURCE_GROUP_NAME="myAKSResourceGroup$RANDOM_SUFFIX" az group create --name $MY_RESOURCE_GROUP_NAME --location $REGION`

Results:

`{ "id": "/subscriptions/xxxxx-xxxxx-xxxxx-xxxxx/resourceGroups/myResourceGroupxxxxx", "location": "WestUS2", "managedBy": null, "name": "myResourceGroupxxxxx", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`


## Create an AKS cluster

In this section, we create an AKS cluster with the following configuration:

- The cluster is configured with two nodes to ensure it operates reliably. A
[node](../concepts-clusters-workloads#nodes)is an Azure virtual machine (VM) that runs the Kubernetes node components and container runtime. - The
`--windows-admin-password`

and`--windows-admin-username`

parameters set the administrator credentials for any Windows Server nodes on the cluster and must meet[Windows Server password requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference). - The node pool uses
`VirtualMachineScaleSets`

.

Use the following steps to create the AKS cluster with Azure CLI:

Create a username to use as administrator credentials for the Windows Server nodes on your cluster.

`export WINDOWS_USERNAME="winadmin"`

Create a password for the administrator username you created in the previous step. The password must be a minimum of 14 characters and meet the

[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).`export WINDOWS_PASSWORD=$(echo "P@ssw0rd$(openssl rand -base64 10 | tr -dc 'A-Za-z0-9!@#$%^&*()' | cut -c1-6)")`

Create your cluster using the

command and specify the`az aks create`

`--windows-admin-username`

and`--windows-admin-password`

parameters. The following example command creates a cluster using the values from`WINDOWS_USERNAME`

and`WINDOWS_PASSWORD`

you set in the previous commands. A random suffix is appended to the cluster name for uniqueness.`export MY_AKS_CLUSTER="myAKSCluster$RANDOM_SUFFIX" az aks create \ --resource-group $MY_RESOURCE_GROUP_NAME \ --name $MY_AKS_CLUSTER \ --node-count 2 \ --enable-addons monitoring \ --generate-ssh-keys \ --windows-admin-username $WINDOWS_USERNAME \ --windows-admin-password $WINDOWS_PASSWORD \ --vm-set-type VirtualMachineScaleSets \ --network-plugin azure`

After a few minutes, the command completes and returns JSON-formatted information about the cluster. Occasionally, the cluster can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

If you get a password validation error, and the password that you set meets the length and complexity requirements, try creating your resource group in another region. Then try creating the cluster with the new resource group.

If you don't specify an administrator username and password when creating the node pool, the username is set to

*azureuser*and the password is set to a random value. For more information, see the[Windows Server FAQ](../windows-faq)You can't change the administrator username, but you can change the administrator password that your AKS cluster uses for Windows Server nodes using

`az aks update`

. For more information, see[Windows Server FAQ](../windows-faq).To run an AKS cluster that supports node pools for Windows Server containers, your cluster needs to use a network policy that uses

[Azure CNI (advanced)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md)network plugin. The`--network-plugin azure`

parameter specifies Azure CNI.

## Add a node pool

By default, all AKS clusters are created with a node pool that can run Linux containers. You must add a Windows node pool that can run Windows Server containers alongside the Linux node pool. To check if you have a Windows node pool in your cluster, you can view the nodes on your cluster using the `kubectl get nodes -o wide`

command.

To create a Windows node pool, you need to specify a supported `OsType`

and `OsSku`

. Use the information in the following table to determine which is appropriate for your cluster:

`OsType` |
`OsSku` |
Default | Supported K8s versions | Details |
|---|---|---|---|---|
`windows` |
`Windows2025` |
Currently in preview. Not default. | 1.32+ | Updated defaults: `containerd` 2.0, Generation 2 image is used by default. |
`windows` |
`Windows2022` |
Default in K8s 1.25-1.35 | Not available in K8s 1.36+ | Retires in March 2027. Updated defaults: FIPS is enabled by default. |
`windows` |
`Windows2019` |
Default in K8s 1.24 and below | Not available in K8s 1.33+ | Retires in March 2026. |

Windows Server 2022 is the default operating system for Kubernetes versions 1.25-1.35. Windows Server 2019 is the default OS for earlier versions. If you don't specify a particular OS SKU, Azure creates the new node pool with the default SKU for the version of Kubernetes used by the cluster.

Important

Starting on March 01, 2026, Azure Kubernetes Service (AKS) no longer supports Windows Server 2019 node pools. Node pools running Kubernetes version 1.33+ can't use Windows Server 2019. Starting on April 01, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4091) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=aks-will-stop-support-for-windows-server-2019-on-march-1-2026). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on March 15, 2027, Azure Kubernetes Service (AKS) no longer supports Windows Server 2022 node pools. Node pools running Kubernetes version 1.36+ can't use Windows Server 2022. Starting on April 01, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4168) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=ws2022-retirement-aks). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Add a Windows node pool using the

command with a specified`az aks nodepool add`

`OsType`

and`OsSku`

. If you don't specify a particular OS SKU, Azure creates the new node pool with the default SKU for the version of Kubernetes used by the cluster.`az aks nodepool add \ --resource-group $MY_RESOURCE_GROUP_NAME \ --cluster-name $MY_AKS_CLUSTER \ --os-type Windows \ --os-sku Windows2022 \ --name npwin \ --node-count 1`

This command creates a new node pool named

*npwin*and adds it to*myAKSCluster*. The command also uses the default subnet in the default virtual network created when running`az aks create`

.

## Connect to the cluster

You use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client, to manage your Kubernetes clusters. If you use Azure Cloud Shell, `kubectl`

is already installed. If you want to install and run `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group $MY_RESOURCE_GROUP_NAME --name $MY_AKS_CLUSTER`

Verify the connection to your cluster using the

command, which returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes -o wide`

The following example output shows all nodes in the cluster. Make sure the status of all nodes is

*Ready*:`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME aks-nodepool1-20786768-vmss000000 Ready agent 22h v1.27.7 10.224.0.4 <none> Ubuntu 22.04.3 LTS 5.15.0-1052-azure containerd://1.7.5-1 aks-nodepool1-20786768-vmss000001 Ready agent 22h v1.27.7 10.224.0.33 <none> Ubuntu 22.04.3 LTS 5.15.0-1052-azure containerd://1.7.5-1 aksnpwin000000 Ready agent 20h v1.27.7 10.224.0.62 <none> Windows Server 2022 Datacenter 10.0.20348.2159 containerd://1.6.21+azure`

Note

The container runtime for each node pool is shown under

*CONTAINER-RUNTIME*. The container runtime values begin with`containerd://`

, which means that they each use`containerd`

for the container runtime.

## Deploy the application

A Kubernetes manifest file defines a desired state for the cluster, such as what container images to run. In this article, you use a manifest to create all objects needed to run the ASP.NET sample application in a Windows Server container. This manifest includes a [Kubernetes deployment](../concepts-clusters-workloads#deployments-and-yaml-manifests) for the ASP.NET sample application and an external [Kubernetes service](../concepts-network-services) to access the application from the internet.

The ASP.NET sample application is provided as part of the [.NET Framework Samples](https://hub.docker.com/_/microsoft-dotnet-framework-samples/) and runs in a Windows Server container. AKS requires Windows Server containers to be based on images of *Windows Server 2022* or greater. The Kubernetes manifest file must also define a [node selector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) to tell your AKS cluster to run your ASP.NET sample application's pod on a node that can run Windows Server containers.

Create a file named

`sample.yaml`

and copy in the following YAML definition:`apiVersion: apps/v1 kind: Deployment metadata: name: sample labels: app: sample spec: replicas: 1 template: metadata: name: sample labels: app: sample spec: nodeSelector: "kubernetes.io/os": windows containers: - name: sample image: mcr.microsoft.com/dotnet/framework/samples:aspnetapp resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 selector: matchLabels: app: sample --- apiVersion: v1 kind: Service metadata: name: sample spec: type: LoadBalancer ports: - protocol: TCP port: 80 selector: app: sample`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f sample.yaml`

The following example output shows the deployment and service created successfully:

`{ "deployment.apps/sample": "created", "service/sample": "created" }`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete. Occasionally, the service can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

Check the status of the deployed pods using the

command. Make sure all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`while true; do export EXTERNAL_IP=$(kubectl get service sample -o jsonpath="{.status.loadBalancer.ingress[0].ip}" 2>/dev/null) if [[ -n "$EXTERNAL_IP" && "$EXTERNAL_IP" != "<pending>" ]]; then kubectl get service sample break fi echo "Still waiting for external IP assignment..." sleep 5 done`

Initially, the output shows the

*EXTERNAL-IP*for the sample service as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE sample LoadBalancer xx.xx.xx.xx pending xx:xxxx/TCP 2m`

When the

*EXTERNAL-IP*address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output replaces

`<public-ip-address>`

with a valid public IP address assigned to the service:`{ "NAME": "sample", "TYPE": "LoadBalancer", "CLUSTER-IP": "10.0.37.27", "EXTERNAL-IP": "<public-ip-address>", "PORT(S)": "80:30572/TCP", "AGE": "2m" }`

See the sample app in action by opening a web browser to the external IP address of your service after a few minutes.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed an ASP.NET sample application in a Windows Server container to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS, and to walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-flatcar-deploy-arm-template -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Create an AKS cluster using Flatcar Container Linux for AKS (preview).
- Deploy an AKS cluster using an Azure Resource Manager template.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

An [Azure Resource Manager template](/en-us/azure/azure-resource-manager/templates/overview) is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This article assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. Make sure that the identity you use to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine, you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

After you deploy the cluster from the template, you can use either Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.

## Register resource providers

You might need to register resource providers in your Azure subscription. For example, `Microsoft.ContainerService`

is required.

Check the registration status using the [ az provider show](/en-us/cli/azure/provider#az-provider-show) command.

```
az provider show --namespace Microsoft.ContainerService --query registrationState
```


If necessary, register the resource provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command.

```
az provider register --namespace Microsoft.ContainerService
```


## Install `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Flatcar Container Linux requires a minimum of 18.0.0b42**.`az extension update --name aks-preview`


## Register `AKSFlatcarPreview`

feature flag

Register the

`AKSFlatcarPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AKSFlatcarPreview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AKSFlatcarPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create an SSH key pair

To create an AKS cluster using an ARM template, you provide an SSH public key. If you need this resource, follow the steps in this section. Otherwise, skip to the [Review the template](#review-the-template) section.

To access AKS nodes, you connect using an SSH key pair (public and private). To create an SSH key pair:

Go to

[https://shell.azure.com](https://shell.azure.com)to open Cloud Shell in your browser.Create a resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command.`az group create \ --name myResourceGroup \ --location eastus`

Create an SSH key pair using the

[az sshkey create](/en-us/cli/azure/sshkey#az-sshkey-create)command or the`ssh-keygen`

command.`az sshkey create --name mySSHKey --resource-group myResourceGroup`

Or create an SSH key pair using ssh-keygen

`ssh-keygen -t rsa -b 4096`

To deploy the template, you must provide the public key from the SSH pair. Retrieve the public key using the

command.`az sshkey show`

`az sshkey show --name mySSHKey --resource-group myResourceGroup --query publicKey`

By default, the SSH key files are created in the

*~/.ssh*directory. Running the`az sshkey create`

or`ssh-keygen`

command overwrites any existing SSH key pair with the same name.For more information about creating SSH keys, see

[Create and manage SSH keys for authentication in Azure](/en-us/azure/virtual-machines/linux/create-ssh-keys-detailed).

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/aks/).

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"metadata": {
"_generator": {
"name": "bicep",
"version": "0.26.170.59819",
"templateHash": "14823542069333410776"
}
},
"parameters": {
"clusterName": {
"type": "string",
"defaultValue": "aks101cluster",
"metadata": {
"description": "The name of the Managed Cluster resource."
}
},
"location": {
"type": "string",
"defaultValue": "[resourceGroup().location]",
"metadata": {
"description": "The location of the Managed Cluster resource."
}
},
"dnsPrefix": {
"type": "string",
"metadata": {
"description": "Optional DNS prefix to use with hosted Kubernetes API server FQDN."
}
},
"osDiskSizeGB": {
"type": "int",
"defaultValue": 0,
"minValue": 0,
"maxValue": 1023,
"metadata": {
"description": "Disk size (in GB) to provision for each of the agent pool nodes. This value ranges from 0 to 1023. Specifying 0 will apply the default disk size for that agentVMSize."
}
},
"agentCount": {
"type": "int",
"defaultValue": 3,
"minValue": 1,
"maxValue": 50,
"metadata": {
"description": "The number of nodes for the cluster."
}
},
"agentVMSize": {
"type": "string",
"defaultValue": "standard_d2s_v3",
"metadata": {
"description": "The size of the Virtual Machine."
}
},
"linuxAdminUsername": {
"type": "string",
"metadata": {
"description": "User name for the Linux Virtual Machines."
}
},
"sshRSAPublicKey": {
"type": "string",
"metadata": {
"description": "Configure all linux machines with the SSH RSA public key string. Your key should include three parts, for example 'ssh-rsa AAAAB...snip...UcyupgH azureuser@linuxvm'"
}
}
},
"resources": [
{
"type": "Microsoft.ContainerService/managedClusters",
"apiVersion": "2024-02-01",
"name": "[parameters('clusterName')]",
"location": "[parameters('location')]",
"identity": {
"type": "SystemAssigned"
},
"properties": {
"dnsPrefix": "[parameters('dnsPrefix')]",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": "[parameters('osDiskSizeGB')]",
"count": "[parameters('agentCount')]",
"vmSize": "[parameters('agentVMSize')]",
"osType": "Linux",
"mode": "System"
}
],
"linuxProfile": {
"adminUsername": "[parameters('linuxAdminUsername')]",
"ssh": {
"publicKeys": [
{
"keyData": "[parameters('sshRSAPublicKey')]"
}
]
}
}
}
}
],
"outputs": {
"controlPlaneFQDN": {
"type": "string",
"value": "[reference(resourceId('Microsoft.ContainerService/managedClusters', parameters('clusterName')), '2024-02-01').fqdn]"
}
}
}
```


The resource type defined in the ARM template is [ Microsoft.ContainerService/managedClusters](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template).

For more AKS samples, see the [AKS quickstart templates](https://azure.microsoft.com/resources/templates/?term=Azure+Kubernetes+Service) site.

## Deploy the template

Select

**Deploy to Azure**to sign in and open a template.On the

**Basics**page, leave the default values for the*OS Disk Size GB*,*Agent Count*,*Agent VM Size*, and*OS Type*, and configure the following template parameters:**Subscription**: Select an Azure subscription.**Resource group**: Select**Create new**. Enter a unique name for the resource group, such as*myResourceGroup*, then select**OK**.**OS SKU**: Specify**flatcar**, if you do not update OS SKU, the default will be`Ubuntu`

.**Location**: Select a location, such as**East US**.**Cluster name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**DNS prefix**: Enter a unique DNS prefix for your cluster, such as*myakscluster*.**Linux Admin Username**: Enter a username to connect using SSH, such as*azureuser*.**SSH public key source**: Select**Use existing public key**.**Key pair name**: Copy and paste the*public*part of your SSH key pair (by default, the contents of*~/.ssh/id_rsa.pub*).

Select

**Review + Create**>**Create**.

It takes a few minutes to create the AKS cluster. Wait for the cluster to be successfully deployed before you move on to the next step.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/).

If you use Azure Cloud Shell, `kubectl`

is already installed. To install and run `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az_aks_install_cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials \ --resource-group myResourceGroup \ --name myAKSCluster`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the three nodes created in the previous steps. Make sure the node status is

*Ready*:`NAME STATUS ROLES AGE VERSION aks-agentpool-38955149-vmss000000 Ready <none> 5m53s v1.32.7 aks-agentpool-38955149-vmss000001 Ready <none> 6m31s v1.32.7 aks-agentpool-238955149-vmss000002 Ready <none> 6m35s v1.32.7`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a file named

`aks-store-quickstart.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: rabbitmq spec: replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 resources: requests: cpu: 1m memory: 1Mi limits: cpu: 1m memory: 7Mi --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

Check the status of the deployed pods using the

command. Make all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the store-front application. Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action:


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges.

- Remove the resource group, container service, and all related resources using the
command.`az group delete`


```
az group delete --name myResourceGroup
```


Note

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity, so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-automatic-deploy -->

# Quickstart: Create an Azure Kubernetes Service (AKS) Automatic cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

[Azure Kubernetes Service (AKS) Automatic](../intro-aks-automatic) provides the easiest managed Kubernetes experience for developers, DevOps engineers, and platform engineers. Ideal for modern and AI applications, AKS Automatic automates AKS cluster setup and operations and embeds best practice configurations. Users of any skill level can benefit from the security, performance, and dependability of AKS Automatic for their applications. AKS Automatic also includes a [pod readiness SLA](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services) that guarantees 99.9% of pod readiness operations complete within 5 minutes, guaranteeing reliable, self-healing infrastructure for your applications.

In this quickstart, you learn to:

- Deploy an AKS Automatic cluster.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

## Before you begin

- This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads). - AKS Automatic will
[enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks), but you should pre-register the`Microsoft.PolicyInsights`

resource provider in your subscription for a smoother experience. See[Azure resource providers and types](/en-us/cli/azure/provider#az-provider-register)for more information.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.77.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command.`az account set`


- To deploy a Bicep file, you need to write access on the resources you create and access to all operations on the
`Microsoft.Resources/deployments`

resource type. For example, to create a virtual machine, you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

## Limitations

- AKS Automatic clusters' system nodepool require deployment in Azure regions that support at least three
[availability zones](/en-us/azure/reliability/regions-list), ephemeral OS disk, and Azure Linux OS. - You can only create AKS Automatic clusters in regions where
[API Server VNet Integration](../api-server-vnet-integration)is generally available (GA).

Important

AKS Automatic tries to dynamically select a virtual machine size for the `system`

node pool based on the capacity available in the subscription. Make sure your subscription has quota for 16 vCPUs of any of the following sizes in the region you're deploying the cluster to: [Standard_D4lds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series), [Standard_D4ads_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dadsv5-series), [Standard_D4ds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v4](/en-us/azure/virtual-machines/sizes/general-purpose/dv4-series), [Standard_DS3_v2](/en-us/azure/virtual-machines/sizes/general-purpose/dsv3-series), [Standard_DS12_v2](/en-us/azure/virtual-machines/sizes/memory-optimized/dv2-dsv2-series-memory), [Standard_D4alds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/daldsv6-series), [Standard_D4lds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv6-series), or [Standard_D4alds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series). You can [view quotas for specific VM-families and submit quota increase requests](/en-us/azure/quotas/per-vm-quota-requests) through the Azure portal.
If you have additional questions, learn more through the [troubleshooting docs](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/aks-automatic-troubleshoot/).

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name myResourceGroup --location eastus
```


The following sample output resembles successful creation of the resource group:

```
{
"id": "/subscriptions/<guid>/resourceGroups/myResourceGroup",
"location": "eastus",
"managedBy": null,
"name": "myResourceGroup",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null
}
```


## Create an AKS Automatic cluster

To create an AKS Automatic cluster, use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a cluster named

*myAKSAutomaticCluster*with Managed Prometheus and Container Insights integration enabled.

```
az aks create \
--resource-group myResourceGroup \
--name myAKSAutomaticCluster \
--sku automatic
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with

[Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

Note

When you create a cluster using the Azure CLI, your user is [assigned built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) for `Azure Kubernetes Service RBAC Cluster Admin`

.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSAutomaticCluster
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Create Automatic Kubernetes cluster

To create an AKS Automatic cluster, search for

**Kubernetes Services**, and select**Automatic Kubernetes cluster**from the drop-down options.On the

**Basics**tab, fill in all the mandatory fields (Subscription, Resource group, Kubernetes cluster name, and Region) required to get started:On the

**Monitoring**tab, choose your monitoring configurations from Azure Monitor, Managed Prometheus, Grafana Dashboards, Container Network Observability (ACNS) and/or configure alerts. Enable Managed Grafana (optional), add tags (optional), and proceed to create the cluster.On the

**Advanced**tab, update your networking (optional), managed identity (optional), security and managed namespaces (optional) settings and proceed to create the cluster.Get started with configuring your first application from GitHub and set up an automated deployment pipeline.


## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac). When you create a cluster using the Azure portal, your user is [assigned built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) for `Azure Kubernetes Service RBAC Cluster Admin`

.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSAutomaticCluster
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name myResourceGroup --location eastus
```


The following sample output resembles successful creation of the resource group:

```
{
"id": "/subscriptions/<guid>/resourceGroups/myResourceGroup",
"location": "eastus",
"managedBy": null,
"name": "myResourceGroup",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null
}
```


## Review the Bicep file

This Bicep file defines an AKS Automatic cluster. While in preview, you need to specify the *system nodepool* agent pool profile.

```
@description('The name of the managed cluster resource.')
param clusterName string = 'myAKSAutomaticCluster'
@description('The location of the managed cluster resource.')
param location string = resourceGroup().location
resource aks 'Microsoft.ContainerService/managedClusters@2024-03-02-preview' = {
name: clusterName
location: location
sku: {
name: 'Automatic'
}
properties: {
agentPoolProfiles: [
{
name: 'systempool'
mode: 'System'
count: 3
}
]
}
identity: {
type: 'SystemAssigned'
}
}
```


For more information about the resource defined in the Bicep file, see the [ Microsoft.ContainerService/managedClusters](/en-us/azure/templates/microsoft.containerservice/managedclusters?tabs=bicep&pivots=deployment-language-bicep) reference.

## Deploy the Bicep file

Save the Bicep file as

**main.bicep**to your local computer.Important

The Bicep file sets the

`clusterName`

param to the string*myAKSAutomaticCluster*. If you want to use a different cluster name, make sure to update the string to your preferred cluster name before saving the file to your computer.Deploy the Bicep file using the Azure CLI.

`az deployment group create --resource-group myResourceGroup --template-file main.bicep`

It takes a few minutes to create the AKS cluster. Wait for the cluster to be successfully deployed before you move on to the next step.


## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

Important

When you create a cluster using Bicep, you need to [assign one of the built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) such as `Azure Kubernetes Service RBAC Reader`

, `Azure Kubernetes Service RBAC Writer`

, `Azure Kubernetes Service RBAC Admin`

, or `Azure Kubernetes Service RBAC Cluster Admin`

to your users, scoped to the cluster or a specific namespace, example using `az role assignment create --role "Azure Kubernetes Service RBAC Cluster Admin" --scope <AKS cluster resource id> --assignee user@contoso.com`

. Also make sure your users have the `Azure Kubernetes Service Cluster User`

built-in role to be able to do run `az aks get-credentials`

, and then get the kubeconfig of your AKS cluster using the `az aks get-credentials`

command.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a namespace

`aks-store-demo`

to deploy the Kubernetes resources into.`kubectl create ns aks-store-demo`

Deploy the application using the

command into the`kubectl apply`

`aks-store-demo`

namespace. The YAML file defining the deployment is on[GitHub](https://github.com/Azure-Samples/aks-store-demo).`kubectl apply -n aks-store-demo -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-ingress-quickstart.yaml`

The following sample output shows the deployments and services:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created ingress/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make sure all pods are`Running`

before proceeding. If this is the first workload you deploy, it may take a few minutes for[node auto provisioning](../node-autoprovision)to create a node pool to run the pods.`kubectl get pods -n aks-store-demo`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get ingress store-front -n aks-store-demo --watch`

The

**ADDRESS**output for the`store-front`

service initially shows empty:`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 80 12m`

Once the

**ADDRESS**changes from blank to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following sample output shows a valid public IP address assigned to the service:

`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 4.255.22.196 80 12m`

Open a web browser to the external IP address of your ingress to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges. Run the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.

```
az group delete --name myResourceGroup --yes --no-wait
```


Note

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity, so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster using [AKS Automatic](../intro-aks-automatic) and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS Automatic, continue to the introduction.
