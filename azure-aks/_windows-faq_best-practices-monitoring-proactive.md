---
merged_at: 2026-01-25T12:25:33.912657
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: windows-faq.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/windows-faq -->

# Frequently asked questions about Windows Server on AKS

This article provides answers to some of the most common questions about using Windows Server containers on Azure Kubernetes Service (AKS).

## Why can't I create new Windows Server 2019 node pools?

Windows Server 2019 isn't supported in Kubernetes version 1.33 and above. Use a supported Windows Server version such as Windows Server 2025 (preview) or Windows Server 2022.

## Why can't I upgrade my Windows Server 2019 node pools to Kubernetes version 1.33?

Windows Server 2019 isn't supported in Kubernetes version 1.33 and above. Use a supported Windows Server version such as Windows Server 2025 (preview) or Windows Server 2022.

## What kind of disks are supported for Windows?

Azure Disks and Azure Files are the supported volume types, and are accessed as New Technology File System (NTFS) volumes in the Windows Server container.

## Does Windows support generation 2 virtual machines (VMs)?

Generation 2 VMs are supported on Windows starting with Windows Server 2022. Generation 2 VMs are default in Windows Server 2025.

For more information, see [Support for generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## How do I patch my Windows nodes?

To get the latest patches for Windows nodes, you can either [upgrade the node pool](manage-node-pools#upgrade-a-single-node-pool) or [upgrade the node image](node-image-upgrade).

## Is preserving the client source IP supported?

At this time, [client source IP preservation](concepts-network-ingress#ingress-controllers) isn't supported with Windows nodes.

## Can I change the maximum number of pods per node?

Yes. For more information, see [Maximum number of pods](concepts-network-ip-address-planning#maximum-pods-per-node).

## What is the default transmission control protocol (TCP) time-out in Windows OS?

The default TCP time-out in Windows OS is four minutes. This value isn't configurable. When an application uses a longer time-out, the TCP connections between different containers in the same node close after four minutes.

## Why am I seeing an error when I try to create a new Windows agent pool?

If you created your cluster before February 2020 and didn't perform any upgrade operations, the cluster still uses an old Windows image. You might see an error that resembles the following example:

"The following list of images referenced from the deployment template isn't found: Publisher: MicrosoftWindowsServer, Offer: WindowsServer, Sku: 2019-datacenter-core-smalldisk-2004, Version: latest. Refer to [Find and use Azure Marketplace Virtual Machine images with Azure PowerShell](/en-us/azure/virtual-machines/windows/cli-ps-findimage) for instructions on finding available images."

To fix this issue, you need to perform the following steps:

- Upgrade the
[cluster control plane](manage-node-pools#upgrade-a-cluster-control-plane-with-multiple-node-pools), which updates the image offer and publisher. - Create new Windows agent pools.
- Move Windows pods from existing Windows agent pools to new Windows agent pools.
- Delete old Windows agent pools.

## Why am I seeing an error when I try to deploy Windows pods?

If you specify a value in `--max-pods`

less than the number of pods you want to create, you might see the `No available addresses`

error.

To fix this error, use the `az aks nodepool add`

command with a high enough `--max-pods`

value. For example:

```
az aks nodepool add \
--cluster-name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--name $NODEPOOL_NAME \
--max-pods 3
```


For more details, see the [ --max-pods documentation](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add).

## Why is there an unexpected user named "sshd" on my virtual machine node?

AKS adds a user named "sshd" when installing the OpenSSH service. This user isn't malicious. We recommend that customers update their alerts to ignore this unexpected user account.

## How do I rotate the service principal for my Windows node pool?

Windows node pools don't support service principal rotation. To update the service principal, create a new Windows node pool and migrate your pods from the older pool to the new one. After your pods are migrated to the new pool, delete the older node pool.

Instead of service principals, you can use managed identities. For more information, see [Use managed identities in AKS](use-managed-identity).

## How do I change the administrator password for Windows Server nodes on my cluster?

To change the administrator password using the Azure CLI, use the `az aks update`

command with the `--admin-password`

parameter. For example:

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--admin-password <new-password>
```


To change the password using Azure PowerShell, use the `Set-AzAksCluster`

cmdlet with the `-AdminPassword`

parameter. For example:

```
Set-AzAksCluster `
-ResourceGroupName $RESOURCE_GROUP `
-Name $CLUSTER_NAME `
-AdminPassword <new-password>
```


Keep in mind that performing a cluster update causes a restart and only updates the Windows Server node pools. For information about Windows Server password requirements, see [Windows Server password requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).

## How many node pools can I create?

AKS clusters with Windows node pools have the same resource limits as the default limits specified for the AKS service. For more information, see [Quotas, virtual machine size restrictions, and region availability in Azure Kubernetes Service (AKS)](quotas-skus-regions).

## Can I run ingress controllers on Windows nodes?

Yes, you can run ingress controllers that support Windows Server containers.

## Can my Windows Server containers use gMSA?

Yes. Group-managed service account (gMSA) support is generally available (GA) for Windows on AKS. For more information, see [Enable Group Managed Service Accounts (GMSA) for your Windows Server nodes on your Azure Kubernetes Service (AKS) cluster](use-group-managed-service-accounts)

## Are there any limitations on the number of services on a cluster with Windows nodes?

A cluster with Windows nodes can have approximately 500 services (sometimes less) before it encounters port exhaustion. This limitation applies to a Kubernetes Service with External Traffic Policy set to "Cluster".

When the external traffic policy on a Service is configured as a Cluster, the traffic undergoes an extra Source NAT on the node. This process also results in reservation of a port from the TCPIP dynamic port pool. This port pool is a limited resource (~16K ports by default) and many active connections to a Service can lead to dynamic port pool exhaustion resulting in connection drops.

If the Kubernetes Service is configured with External Traffic Policy set to "Local", port exhaustion problems aren't likely to occur at 500 services.

## How do I change the time zone of a running container?

To change the time zone of a running Windows Server container, connect to the running container with a PowerShell session. For example:

```
kubectl exec -it CONTAINER-NAME -- PowerShell
```


In the running container, use [Set-TimeZone](/en-us/powershell/module/microsoft.powershell.management/set-timezone) to set the time zone of the running container. For example:

```
Set-TimeZone -Id "Russian Standard Time"
```


To see the current time zone of the running container or an available list of time zones, use [Get-TimeZone](/en-us/powershell/module/microsoft.powershell.management/get-timezone).


---

<!-- DOCUMENTO FUSIONADO: best-practices-monitoring-proactive.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/best-practices-monitoring-proactive -->

# Proactive monitoring best practices for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers the best practices for proactive monitoring on Azure Kubernetes Service (AKS) and provides a comprehensive list of the key signals AKS recommends for you to monitor.

Proactively monitoring your AKS clusters is crucial for reducing downtime and saving business interruptions for your applications. This process involves identifying and monitoring key indicators of abnormal behavior in your cluster that might lead to major issues or downtime.

## Monitoring and alerting overview

Monitoring on AKS involves using metrics, logs, and events to ensure the health and performance of your cluster. Common scenarios to monitor include node performance, pod status, and overall resource utilization in your cluster. Logs provide insights into system events and cluster operations and activity. For more information about the methods and signals AKS provides for monitoring, see [Monitor Azure Kubernetes Service (AKS)](monitor-aks).

The best way to proactively monitor your cluster is to configure [Azure Monitor alerts](/en-us/azure/azure-monitor/alerts/alerts-overview). Alerts act as proactive measures to notify you of potential issues or anomalies before they escalate into critical problems. By defining thresholds for key metrics and logs, you receive immediate alerts when these signals exceed predefined limits, indicating potential issues like resource exhaustion or application failures. We highly recommend defining [service-level objectives (SLOs)](/en-us/azure/well-architected/reliability/metrics) for your application to measure the performance and reliability of your service. Configuring alerts on the key signals for your SLOs allows you to quickly detect any degradation of your application's quality of service that your customers receive. Overall, setting timely alerts enables you to quickly investigate and remediate problems, minimizing downtime and ensuring high availability of applications running on your AKS cluster.

## How to configure alerts on specific metric types

| Metric type | Where to find these metrics | How to configure alerts |
|---|---|---|
| AKS Platform Metric | View
|

[Create a metric alert for an Azure resource](/en-us/azure/azure-monitor/alerts/tutorial-metric-alert).[Azure Monitor and Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).[Azure Monitor managed service for Prometheus rule groups](/en-us/azure/azure-monitor/essentials/prometheus-rule-groups).[Azure activity logs for AKS](monitor-aks#azure-activity-log).[Activity log alerts](/en-us/azure/azure-monitor/alerts/alerts-types#activity-log-alerts).**Settings > Properties**blade for your AKS cluster in the Azure portal.2. Select your

**infrastructure resource group**to view the infrastructure resources associated with your cluster.3. Select the

**Virtual Machine Scale Set instance**that matches the name of your node pool you're creating alerts for.4. Navigate to the

**Alerts**blade to create your metric alert.**Settings > Properties**blade for your AKS cluster in the Azure portal.2. Select your

**infrastructure resource group**to view the infrastructure resources associated with your cluster.3. Select the

**load balancer instance**to bring up the Azure portal page for load balancer.4. Navigate to the

**Alerts**page to create your load balancer metric alert.[Azure Monitor resource logs](monitor-aks#azure-monitor-resource-logs).[Create log search alerts from Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-alerts).## Critical signals for configuring alerts

To get holistic coverage of your AKS environment, you need to configure alerts on the three main components of your cluster:

**Cluster infrastructure**: Alerts targeting the underlying infrastructure of your cluster such as nodes, disks, and networking.**Application health**: Alerts for monitoring the health of your pods and applications. Some common indicators of unhealthy applications include out-of-memory kills (OOMKills) of your pods, pods in not ready state, etc.**Kubernetes control plane**: Alerts on AKS control plane to monitor the health and performance of the API server, etcd, and other components.

The following sections contain the key signals which we recommend all AKS customers monitor closely. The AKS team is working to add all critical signals to the existing [Recommended Alerts](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts) feature, which allows you to easily enable alerts for all signals with a one-click experience. The Prometheus metrics alerts are available in Public Preview today, and the remaining alerts are estimated to be available in early 2025. For now, you can manually configure alerts on the critical signals.

### Cluster infrastructure alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| Cluster is in a failed state | Azure Activity Logs | Create or update managed cluster | Status of the log is Failed, indicating that the cluster upgrade or creation action failed. |
| Node pool is in a failed state | Azure Activity Logs | Create or update agent pool | Status of the log is Failed, indicating that the node pool is in a Failed state due to a failed Create, Read, Upgrade, or Delete (CRUD) operation. |
| High Node OS Disk Bandwidth Usage | Virtual Machine Scale Set Metric | OS Disk Bandwidth Consumed Percentage | Node OS disk bandwidth utilization is above 95%. |
| High Node OS Disk IOPS Usage | Virtual Machine Scale Set Metric | OS Disk IOPS Consumed Percentage | Node OS disk IOPS utilization is above 95%. |
| High Node OS Disk Space Usage | AKS Platform Metric | Disk Used Percentage | Node OS disk space percentage utilization is above 90%. |
| High Node CPU Usage | AKS Platform Metric | CPU Usage Percentage | Node CPU Usage is greater than 90%. |
| High Node Memory Usage | AKS Platform Metric | Memory Working Set Percentage | Node Memory Usage is greater than 90%. |
| Node is in NotReady state | AKS Platform Metric | Status for various node conditions | Node is in NotReady state for >20 minutes. |
| SNAT port exhaustion | Load Balancer (LB) Metric | SNAT Connection Count | Filter for Connection State = "Failed" |

### Application health alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| High number of unhealthy pods | Azure Managed Prometheus Metric | Alert name: KubePodReadyStateLow | Available as an AKS recommended alert. To enable this alert, see
|

[Recommended alert rules for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts?tabs=portal).[Recommended alert rules for Kubernetes clusters](/en-us/azure/azure-monitor/containers/kubernetes-metric-alerts?tabs=portal).### Kubernetes control plane alerts

| Alert scenario | Source | Signal | Recommended threshold |
|---|---|---|---|
| ETCD is Filled Up | Azure Managed Prometheus Metric | etcd_mvcc_db_total_size_in_use_in_bytes | ETCD utilization is greater than 2 GB |
| API Server Too Many Requests Errors | Azure Managed Prometheus Metric | apiserver_request_total | Filter for error code 429 |
| API Server Webhook and Tunnel Errors | Azure Managed Prometheus Metric | apiserver_request_total | Filter for error codes 500 and 503 |

## Next steps

For more information about monitoring on AKS, see the following articles:
