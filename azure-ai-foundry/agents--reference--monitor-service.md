---
source_url: https://learn.microsoft.com/en-us/azure/ai-foundry/agents/reference/monitor-service
fetched_at: 2026-01-26T23:15:11.630831
---

# Foundry Agent Service monitoring data reference

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This document refers to the [Microsoft Foundry (classic)](../../what-is-foundry?view=foundry-classic#microsoft-foundry-portals) portal.

🔍 [View the Microsoft Foundry (new) documentation](../../what-is-foundry?view=foundry&preserve-view=true) to learn about the new portal.

This article contains all the monitoring reference information for this service.

See [Monitor Foundry Agent Service](../how-to/metrics?view=foundry-classic) for details on the data you can collect on your agents.

## Metrics

Here are the most important metrics we think you should monitor for Agent Service. Later in this article is a longer list of all available metrics which contains more details on metrics in this shorter list. *See the below list for most up to date information. We're working on refreshing the tables in the following sections.*

## Supported metrics

This section lists all the automatically collected platform metrics for this service. These metrics are also part of the global list of [all platform metrics supported in Azure Monitor](/en-us/azure/azure-monitor/reference/supported-metrics/metrics-index#supported-metrics-per-resource-type).

- All columns might not be present in every table.
- Some columns might be beyond the viewing area of the page. Select
**Expand table**to view all available columns.

**Table headings**

**Category**- The metrics group or classification.**Metric**- The metric display name as it appears in the Azure portal.**Name in REST API**- The metric name as referred to in the[REST API](/en-us/azure/azure-monitor/essentials/rest-api-walkthrough).**Unit**- Unit of measure.**Aggregation**- The default[aggregation](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained)type. Valid values: Average (Avg), Minimum (Min), Maximum (Max), Total (Sum), Count.**Dimensions**-[Dimensions](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#dimensions-splitting-and-filtering)available for the metric.**Time Grains**-[Intervals](/en-us/azure/azure-monitor/essentials/metrics-aggregation-explained#granularity)at which the metric is sampled. For example,`PT1M`

indicates that the metric is sampled every minute,`PT30M`

every 30 minutes,`PT1H`

every hour, and so on.**DS Export**- Whether the metric is exportable to Azure Monitor Logs via diagnostic settings. For information on exporting metrics, see[Create diagnostic settings in Azure Monitor](/en-us/azure/azure-monitor/essentials/create-diagnostic-settings?tabs=portal).

### Category: Agents

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
AgentsNumber of events for AI Agents in this workspace |
`Agents` |
Count | Average, Maximum, Minimum, Total (Sum) | `EventType` |
PT1M | No |
IndexedFilesNumber of files indexed for file search in this workspace |
`IndexedFiles` |
Count | Average, Maximum, Minimum, Total (Sum) | `ErrorCode` , `Status` , `VectorStoreId` |
PT1M | No |
MessagesNumber of events for AI Agent messages in this workspace |
`Messages` |
Count | Average, Maximum, Minimum, Total (Sum) | `EventType` , `ThreadId` |
PT1M | No |
RunsNumber of runs by AI Agents in this workspace |
`Runs` |
Count | Average, Maximum, Minimum, Total (Sum) | `AgentId` , `RunStatus` , `StatusCode` , `StreamType` |
PT1M | No |
ThreadsNumber of events for AI Agent threads in this workspace |
`Threads` |
Count | Average, Maximum, Minimum, Total (Sum) | `EventType` |
PT1M | No |
TokensCount of tokens by AI Agents in this workspace |
`Tokens` |
Count | Average, Maximum, Minimum, Total (Sum) | `AgentId` , `TokenType` |
PT1M | No |
ToolCallsTool calls made by AI Agents in this workspace |
`ToolCalls` |
Count | Average, Maximum, Minimum, Total (Sum) | `AgentId` , `ToolName` |
PT1M | No |

### Category: Model

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Model Deploy FailedNumber of model deployments that failed in this workspace |
`Model Deploy Failed` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `StatusCode` |
PT1M | Yes |
Model Deploy StartedNumber of model deployments started in this workspace |
`Model Deploy Started` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` |
PT1M | Yes |
Model Deploy SucceededNumber of model deployments that succeeded in this workspace |
`Model Deploy Succeeded` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` |
PT1M | Yes |
Model Register FailedNumber of model registrations that failed in this workspace |
`Model Register Failed` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `StatusCode` |
PT1M | Yes |
Model Register SucceededNumber of model registrations that succeeded in this workspace |
`Model Register Succeeded` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` |
PT1M | Yes |

### Category: Quota

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Active CoresNumber of active cores |
`Active Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Active NodesNumber of Acitve nodes. These are the nodes which are actively running a job. |
`Active Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Idle CoresNumber of idle cores |
`Idle Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Idle NodesNumber of idle nodes. Idle nodes are the nodes which are not running any jobs but can accept new job if available. |
`Idle Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Leaving CoresNumber of leaving cores |
`Leaving Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Leaving NodesNumber of leaving nodes. Leaving nodes are the nodes which just finished processing a job and will go to Idle state. |
`Leaving Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Preempted CoresNumber of preempted cores |
`Preempted Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Preempted NodesNumber of preempted nodes. These nodes are the low priority nodes which are taken away from the available node pool. |
`Preempted Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Quota Utilization PercentagePercent of quota utilized |
`Quota Utilization Percentage` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` , `VmFamilyName` , `VmPriority` |
PT1M | Yes |
Total CoresNumber of total cores |
`Total Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Total NodesNumber of total nodes. This total includes some of Active Nodes, Idle Nodes, Unusable Nodes, Premepted Nodes, Leaving Nodes |
`Total Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Unusable CoresNumber of unusable cores |
`Unusable Cores` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |
Unusable NodesNumber of unusable nodes. Unusable nodes are not functional due to some unresolvable issue. Azure will recycle these nodes. |
`Unusable Nodes` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `ClusterName` |
PT1M | Yes |

### Category: Resource

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
CpuCapacityMillicoresMaximum capacity of a CPU node in millicores. Capacity is aggregated in one minute intervals. |
`CpuCapacityMillicores` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
CpuMemoryCapacityMegabytesMaximum memory utilization of a CPU node in megabytes. Utilization is aggregated in one minute intervals. |
`CpuMemoryCapacityMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
CpuMemoryUtilizationMegabytesMemory utilization of a CPU node in megabytes. Utilization is aggregated in one minute intervals. |
`CpuMemoryUtilizationMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
CpuMemoryUtilizationPercentageMemory utilization percentage of a CPU node. Utilization is aggregated in one minute intervals. |
`CpuMemoryUtilizationPercentage` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
CpuUtilizationPercentage of utilization on a CPU node. Utilization is reported at one minute intervals. |
`CpuUtilization` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `runId` , `NodeId` , `ClusterName` |
PT1M | Yes |
CpuUtilizationMillicoresUtilization of a CPU node in millicores. Utilization is aggregated in one minute intervals. |
`CpuUtilizationMillicores` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
CpuUtilizationPercentageUtilization percentage of a CPU node. Utilization is aggregated in one minute intervals. |
`CpuUtilizationPercentage` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
DiskAvailMegabytesAvailable disk space in megabytes. Metrics are aggregated in one minute intervals. |
`DiskAvailMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
DiskReadMegabytesData read from disk in megabytes. Metrics are aggregated in one minute intervals. |
`DiskReadMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
DiskUsedMegabytesUsed disk space in megabytes. Metrics are aggregated in one minute intervals. |
`DiskUsedMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
DiskWriteMegabytesData written into disk in megabytes. Metrics are aggregated in one minute intervals. |
`DiskWriteMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
GpuCapacityMilliGPUsMaximum capacity of a GPU device in milli-GPUs. Capacity is aggregated in one minute intervals. |
`GpuCapacityMilliGPUs` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuEnergyJoulesInterval energy in Joules on a GPU node. Energy is reported at one minute intervals. |
`GpuEnergyJoules` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `runId` , `rootRunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuMemoryCapacityMegabytesMaximum memory capacity of a GPU device in megabytes. Capacity aggregated in at one minute intervals. |
`GpuMemoryCapacityMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuMemoryUtilizationPercentage of memory utilization on a GPU node. Utilization is reported at one minute intervals. |
`GpuMemoryUtilization` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `runId` , `NodeId` , `DeviceId` , `ClusterName` |
PT1M | Yes |
GpuMemoryUtilizationMegabytesMemory utilization of a GPU device in megabytes. Utilization aggregated in at one minute intervals. |
`GpuMemoryUtilizationMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuMemoryUtilizationPercentageMemory utilization percentage of a GPU device. Utilization aggregated in at one minute intervals. |
`GpuMemoryUtilizationPercentage` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuUtilizationPercentage of utilization on a GPU node. Utilization is reported at one minute intervals. |
`GpuUtilization` |
Count | Average, Maximum, Minimum, Total (Sum) | `Scenario` , `runId` , `NodeId` , `DeviceId` , `ClusterName` |
PT1M | Yes |
GpuUtilizationMilliGPUsUtilization of a GPU device in milli-GPUs. Utilization is aggregated in one minute intervals. |
`GpuUtilizationMilliGPUs` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
GpuUtilizationPercentageUtilization percentage of a GPU device. Utilization is aggregated in one minute intervals. |
`GpuUtilizationPercentage` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `DeviceId` , `ComputeName` |
PT1M | Yes |
IBReceiveMegabytesNetwork data received over InfiniBand in megabytes. Metrics are aggregated in one minute intervals. |
`IBReceiveMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` , `DeviceId` |
PT1M | Yes |
IBTransmitMegabytesNetwork data sent over InfiniBand in megabytes. Metrics are aggregated in one minute intervals. |
`IBTransmitMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` , `DeviceId` |
PT1M | Yes |
NetworkInputMegabytesNetwork data received in megabytes. Metrics are aggregated in one minute intervals. |
`NetworkInputMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` , `DeviceId` |
PT1M | Yes |
NetworkOutputMegabytesNetwork data sent in megabytes. Metrics are aggregated in one minute intervals. |
`NetworkOutputMegabytes` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` , `DeviceId` |
PT1M | Yes |
StorageAPIFailureCountAzure Blob Storage API calls failure count. |
`StorageAPIFailureCount` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |
StorageAPISuccessCountAzure Blob Storage API calls success count. |
`StorageAPISuccessCount` |
Count | Average, Maximum, Minimum, Total (Sum) | `RunId` , `InstanceId` , `ComputeName` |
PT1M | Yes |

### Category: Run

| Metric | Name in REST API | Unit | Aggregation | Dimensions | Time Grains | DS Export |
|---|---|---|---|---|---|---|
Cancel Requested RunsNumber of runs where cancel was requested for this workspace. Count is updated when cancellation request has been received for a run. |
`Cancel Requested Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Cancelled RunsNumber of runs cancelled for this workspace. Count is updated when a run is successfully cancelled. |
`Cancelled Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Completed RunsNumber of runs completed successfully for this workspace. Count is updated when a run has completed and output has been collected. |
`Completed Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
ErrorsNumber of run errors in this workspace. Count is updated whenever run encounters an error. |
`Errors` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` |
PT1M | Yes |
Failed RunsNumber of runs failed for this workspace. Count is updated when a run fails. |
`Failed Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Finalizing RunsNumber of runs entered finalizing state for this workspace. Count is updated when a run has completed but output collection still in progress. |
`Finalizing Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Not Responding RunsNumber of runs not responding for this workspace. Count is updated when a run enters Not Responding state. |
`Not Responding Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Not Started RunsNumber of runs in Not Started state for this workspace. Count is updated when a request is received to create a run but run information has not yet been populated. |
`Not Started Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Preparing RunsNumber of runs that are preparing for this workspace. Count is updated when a run enters Preparing state while the run environment is being prepared. |
`Preparing Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Provisioning RunsNumber of runs that are provisioning for this workspace. Count is updated when a run is waiting on compute target creation or provisioning. |
`Provisioning Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Queued RunsNumber of runs that are queued for this workspace. Count is updated when a run is queued in compute target. Can occure when waiting for required compute nodes to be ready. |
`Queued Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Started RunsNumber of runs running for this workspace. Count is updated when run starts running on required resources. |
`Started Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
Starting RunsNumber of runs started for this workspace. Count is updated after request to create run and run info, such as the Run Id, has been populated |
`Starting Runs` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` , `RunType` , `PublishedPipelineId` , `ComputeType` , `PipelineStepType` , `ExperimentName` |
PT1M | Yes |
WarningsNumber of run warnings in this workspace. Count is updated whenever a run encounters a warning. |
`Warnings` |
Count | Total (Sum), Average, Minimum, Maximum, Count | `Scenario` |
PT1M | Yes |

## Related content

- See
[Monitor Agent Service](../how-to/metrics?view=foundry-classic)for a description of monitoring Agent Service. - See
[Monitor Azure resources with Azure Monitor](/en-us/azure/azure-monitor/essentials/monitor-azure-resource)for details on monitoring Azure resources.