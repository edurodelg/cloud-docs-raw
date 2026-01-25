---
merged_at: 2026-01-25T12:06:27.875551
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: best-practices-performance-scale-large.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/best-practices-performance-scale-large -->

# Best practices for performance and scaling for large workloads in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This article focuses on general best practices for **large workloads**. For best practices specific to **small to medium workloads**, see [Performance and scaling best practices for small to medium workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale).

As you deploy and maintain clusters in AKS, you can use the following best practices to help you optimize performance and scaling.

Keep in mind that *large* is a relative term. Kubernetes has a multi-dimensional scale envelope, and the scale envelope for your workload depends on the resources you use. For example, a cluster with 100 nodes and thousands of pods or CRDs might be considered large. A 1,000 node cluster with 1,000 pods and various other resources might be considered small from the control plane perspective. The best signal for scale of a Kubernetes control plane is API server HTTP request success rate and latency, as that's a proxy for the amount of load on the control plane.

In this article, you learn about:

- AKS and Kubernetes control plane scalability.
- Kubernetes Client best practices, including backoff, watches, and pagination.
- Azure API and platform throttling limits.
- Feature limitations.
- Networking and node pool scaling best practices.

## AKS and Kubernetes control plane scalability

In AKS, a *cluster* consists of a set of nodes (physical or virtual machines (VMs)) that run Kubernetes agents and are managed by the Kubernetes control plane hosted by AKS. While AKS optimizes the Kubernetes control plane and its components for scalability and performance, it's still bound by the upstream project limits.

Kubernetes has a multi-dimensional scale envelope with each resource type representing a dimension. Not all resources are alike. For example, *watches* are commonly set on secrets, which result in list calls to the kube-apiserver that add cost and a disproportionately higher load on the control plane compared to resources without watches.

The control plane manages all the resource scaling in the cluster, so the more you scale the cluster within a given dimension, the less you can scale within other dimensions. For example, running hundreds of thousands of pods in an AKS cluster impacts how much pod churn rate (pod mutations per second) the control plane can support.

The size of the envelope is proportional to the size of the Kubernetes control plane. AKS supports three control plane tiers as part of the Base SKU: Free, Standard, and Premium tier. For more information, see [Free, Standard, and Premium pricing tiers for AKS cluster management](free-standard-pricing-tiers).

Important

We highly recommend using the Standard or Premium tier for production or at-scale workloads. AKS automatically scales up the Kubernetes control plane to support the following scale limits:

- Up to 5,000 nodes per AKS cluster
- 200,000 pods per AKS cluster (with Azure CNI Overlay)

In most cases, crossing the scale limit threshold results in degraded performance, but doesn't cause the cluster to immediately fail over. To manage load on the Kubernetes control plane, consider scaling in batches of up to 10-20% of the current scale. For example, for a 5,000 node cluster, scale in increments of 500-1,000 nodes. While AKS does autoscale your control plane, it doesn't happen instantaneously.

You can leverage API Priority and Fairness (APF) to throttle specific clients and request types to protect the control plane during high churn and load.

## Kubernetes clients

Kubernetes clients are the applications clients, such as operators or monitoring agents, deployed in the Kubernetes cluster that need to communicate with the kube-api server to perform read or mutate operations. It's important to optimize the behavior of these clients to minimize the load they add to the kube-api server and Kubernetes control plane.

You can analyze API server traffic and client behavior through Kube Audit logs. For more information, see [Troubleshoot the Kubernetes control plane](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd).

LIST requests can be expensive. When working with lists that might have more than a few thousand small objects or more than a few hundred large objects, you should consider the following guidelines:

**Consider the number of objects (CRs) you expect to eventually exist**when defining a new resource type (CRD).**The load on etcd and API server primarily relies on the size of the response**. Even if you use a field selector to filter the list and retrieve only a small number of results, these guidelines still apply. The only exception is retrieval of a single object by`metadata.name`

.**Avoid repeated LIST calls if possible**if your code needs to maintain an updated list of objects in memory. Instead, consider using the Informer classes provided in most Kubernetes libraries. Informers automatically combine LIST and WATCH functionalities to efficiently maintain an in-memory collection.**Consider whether you need strong consistency**if Informers don't meet your needs. Do you need to see the most recent data, up to the exact moment in time you issued the query? If not, set`ResourceVersion=0`

. This causes the API server cache to serve your request instead of etcd.**If you can't use Informers or the API server cache, read large lists in chunks**.**Avoid listing more often than needed**. If you can't use Informers, consider how often your application lists the resources. After you read the last object in a large list, don't immediately re-query the same list. You should wait a while instead.**Add approporiate exponential backoffs and retry policies**to prevent clients from overwhelming the API server.**Consider the number of running instances of your client application**. There's a big difference between having a single controller listing objects vs. having pods on each node doing the same thing. If you plan to have multiple instances of your client application periodically listing large numbers of objects, your solution won't scale to large clusters.**Keep the overall Etcd size small**and do not use Etcd as a regular database. Some object size reduction techniques are listed below- To reduce pod specification sizes, move environment variables from pod specifications to ConfigMaps
- Split large secrets or ConfigMaps into smaller, more manageable pieces
- Review and optimize resource specifications in your applications
- Reduce revision count


## Azure API and Platform throttling

The load on a cloud application can vary over time based on factors such as the number of active users or the types of actions that users perform. If the processing requirements of the system exceed the capacity of the available resources, the system can become overloaded and suffer from poor performance and failures.

To handle varying load sizes in a cloud application, you can allow the application to use resources up to a specified limit and then throttle them when the limit is reached. On Azure, throttling happens at two levels. Azure Resource Manager (ARM) throttles requests for the subscription and tenant. If the request is under the throttling limits for the subscription and tenant, ARM routes the request to the resource provider. The resource provider then applies throttling limits tailored to its operations. For more information, see [ARM throttling requests](/en-us/azure/azure-resource-manager/management/request-limits-and-throttling).

### Manage throttling in AKS

Azure API limits are usually defined at a subscription-region combination level. For example, all clients within a subscription in a given region share API limits for a given Azure API, such as Virtual Machine Scale Sets PUT APIs. Every AKS cluster has several AKS-owned clients, such as cloud provider or cluster autoscaler, or customer-owned clients, such as Datadog or self-hosted Prometheus, that call Azure APIs. When running multiple AKS clusters in a subscription within a given region, all the AKS-owned and customer-owned clients within the clusters share a common set of API limits. Therefore, the number of clusters you can deploy in a subscription region is a function of the number of clients deployed, their call patterns, and the overall scale and elasticity of the clusters.

Keeping the above considerations in mind, customers are typically able to deploy between 20-40 small to medium scale clusters per subscription-region. You can maximize your subscription scale using the following best practices:

Always upgrade your Kubernetes clusters to the latest version. Newer versions contain many improvements that address performance and throttling issues. If you're using an upgraded version of Kubernetes and still see throttling due to the actual load or the number of clients in the subscription, you can try the following options:

**Analyze errors using AKS Diagnose and Solve Problems**: You can use[AKS Diagnose and Solve Problems](aks-diagnostics)to analyze errors, identity the root cause, and get resolution recommendations.**Increase the Cluster Autoscaler scan interval**: If the diagnostic reports show that[Cluster Autoscaler throttling has been detected](/en-us/troubleshoot/azure/azure-kubernetes/429-too-many-requests-errors#analyze-and-identify-errors-by-using-aks-diagnose-and-solve-problems), you can[increase the scan interval](cluster-autoscaler#update-the-cluster-autoscaler-settings)to reduce the number of calls to Virtual Machine Scale Sets from the Cluster Autoscaler.**Reconfigure third-party applications to make fewer calls**: If you filter by*user agents*in thediagnostic and see that**View request rate and throttle details**[a third-party application, such as a monitoring application, makes a large number of GET requests](/en-us/troubleshoot/azure/azure-kubernetes/429-too-many-requests-errors#analyze-and-identify-errors-by-using-aks-diagnose-and-solve-problems), you can change the settings of these applications to reduce the frequency of the GET calls. Make sure the application clients use exponential backoff when calling Azure APIs.

**Split your clusters into different subscriptions or regions**: If you have a large number of clusters and node pools that use Virtual Machine Scale Sets, you can split them into different subscriptions or regions within the same subscription. Most Azure API limits are shared at the subscription-region level, so you can move or scale your clusters to different subscriptions or regions to get unblocked on Azure API throttling. This option is especially helpful if you expect your clusters to have high activity. There are no generic guidelines for these limits. If you want specific guidance, you can create a support ticket.

## Monitor AKS Control Plane metrics and logs

Monitoring control plane metrics in large AKS clusters is crucial for ensuring the stability and performance of Kubernetes workloads. These metrics provide visibility into the health and behavior of critical components like the API server, etcd, controller manager, and scheduler. In large-scale environments, where resource contention and high API call volumes are common, monitoring control plane metrics helps identify bottlenecks, detect anomalies, and optimize resource usage. By analyzing these metrics, operators can proactively address issues such as API server latency, high etcd objects, or excessive control plane resource consumption, ensuring efficient cluster operation and minimizing downtime.

Azure Monitor offers comprehensive metrics and logs on the health of the control plane through [Azure Managed Prometheus](monitor-control-plane-metrics#monitor-aks-control-plane-metrics-preview) and [Diagnostic settings](monitor-control-plane-metrics#azure-monitor-resource-logs)

- For list of alerts to configure for health of the control plane, please checkout
[Best practices for AKS control plane monitoring](best-practices-monitoring-proactive#kubernetes-control-plane-alerts) - To get the list of user agents having the highest latency, you can use the Control Plane logs/Diagnostic Settings

## Feature limitations

As you scale your AKS clusters to larger scale points, keep the following feature limitations in mind:

- AKS supports scaling up to 5,000 nodes by default for all Standard Tier / LTS clusters. AKS scales your cluster's control plane at runtime based on cluster size and API server resource utilization. If you can't scale up to the supported limit, enable
[control plane metrics (Preview)](monitor-control-plane-metrics)with the[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)to monitor the control plane. To help troubleshoot scaling performance or reliability issues, see the following resources:

Note

During the operation to scale the control plane, you might encounter elevated API server latency or timeouts for up to 15 minutes. If you continue to have problems scaling to the supported limit, open a [support ticket](https://portal.azure.com/#create/Microsoft.Support/Parameters/%7B%0D%0A%09%22subId%22%3A+%22%22%2C%0D%0A%09%22pesId%22%3A+%225a3a423f-8667-9095-1770-0a554a934512%22%2C%0D%0A%09%22supportTopicId%22%3A+%2280ea0df7-5108-8e37-2b0e-9737517f0b96%22%2C%0D%0A%09%22contextInfo%22%3A+%22AksLabelDeprecationMarch22%22%2C%0D%0A%09%22caller%22%3A+%22Microsoft_Azure_ContainerService+%2B+AksLabelDeprecationMarch22%22%2C%0D%0A%09%22severity%22%3A+%223%22%0D%0A%7D).

[Azure Network Policy Manager (Azure npm)](/en-us/azure/virtual-network/kubernetes-network-policies)only supports up to 250 nodes.- Some AKS node metrics, including node disk usage, node CPU/memory usage, and network in/out, won't be accessible in
[azure monitor platform metrics](/en-us/azure/azure-monitor/reference/supported-metrics/microsoft-containerservice-managedclusters-metrics)after the control plane is scaled up. To confirm if your control plane has been scaled up, look for the configmap 'large-cluster-control-plane-scaling-status'

```
kubectl describe configmap large-cluster-control-plane-scaling-status -n kube-system
```


- You can't use the Stop and Start feature with clusters that have more than 100 nodes. For more information, see
[Stop and start an AKS cluster](start-stop-cluster).

## Networking

As you scale your AKS clusters to larger scale points, keep the following networking best practices in mind:

- Use Managed NAT for cluster egress with at least two public IPs on the NAT gateway. For more information, see
[Create a managed NAT gateway for your AKS cluster](nat-gateway). - Use Azure CNI Overlay to scale up to 200,000 pods and 5,000 nodes per cluster. For more information, see
[Configure Azure CNI Overlay networking in AKS](azure-cni-overlay). - If your application needs direct pod-to-pod communication across clusters, use Azure CNI with dynamic IP allocation and scale up to 50,000 application pods per cluster with one routable IP per pod. For more information, see
[Configure Azure CNI networking for dynamic IP allocation in AKS](configure-azure-cni-dynamic-ip-allocation). - When using internal Kubernetes services behind an internal load balancer, we recommend creating an internal load balancer or service below a 750 node scale for optimal scaling performance and load balancer elasticity.
- Azure npm only supports up to 250 nodes. If you want to enforce network policies for larger clusters, consider using
[Azure CNI powered by Cilium](azure-cni-powered-by-cilium), which combines the robust control plane of Azure CNI with the Cilium data plane to provide high performance networking and security.

## Node pool scaling

As you scale your AKS clusters to larger scale points, keep the following node pool scaling best practices in mind:

- For system node pools, use the
*Standard_D16ds_v5*SKU or an equivalent core/memory VM SKU with ephemeral OS disks to provide sufficient compute resources for kube-system pods. - Since AKS has a limit of 1,000 nodes per node pool, we recommend creating at least five user node pools to scale up to 5,000 nodes.
- When running at-scale AKS clusters, use the cluster autoscaler whenever possible to ensure dynamic scaling of node pools based on the demand for compute resources. For more information, see
[Automatically scale an AKS cluster to meet application demands](cluster-autoscaler). - If you're scaling beyond 1,000 nodes and are
*not*using the cluster autoscaler, we recommend scaling in batches of 500-700 nodes at a time. The scaling operations should have a two-minute to five-minute wait time between scale up operations to prevent Azure API throttling. For more information, see[API management: Caching and throttling policies](https://azure.microsoft.com/blog/api-management-advanced-caching-and-throttling-policies/).

## Cluster upgrade considerations and best practices

- When a cluster reaches the 5,000 node limit, cluster upgrades are blocked. This limits prevents an upgrade because there isn't available node capacity to perform rolling updates within the max surge property limit. If you have a cluster at this limit, we recommend
[scaling down the cluster](concepts-scale)under 3,000 nodes before attempting a cluster upgrade. This will provide extra capacity for node churn and minimize load on the control plane. - When upgrading clusters with more than 500 nodes, it is recommended to use a
[max surge configuration](upgrade-aks-cluster#set-max-surge-value)of 10-20% of the node pool's capacity. AKS configures upgrades with a default value of 10% for max surge. You can customize the max surge settings per node pool to enable a trade-off between upgrade speed and workload disruption. When you increase the max surge settings, the upgrade process completes faster, but you might experience disruptions during the upgrade process. For more information, see[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade). - For more cluster upgrade information, see
[Upgrade an AKS cluster](upgrade-cluster).


---

<!-- DOCUMENTO FUSIONADO: best-practices-storage-nvme.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/best-practices-storage-nvme -->

# Best practices for ephemeral NVMe data disks in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Ephemeral NVMe data disks provide high-performance, low-latency storage that's ideal for demanding workloads running on Azure Kubernetes Service (AKS). Many modern applications, such as AI/ML training, data analytics, and high-throughput databases, require fast temporary storage to process large volumes of intermediate data efficiently. By using ephemeral NVMe disks, you can significantly improve application responsiveness and throughput, while optimizing for cost and scalability in your AKS clusters.

In contrast to remote disks, whose performance scales with the size of the virtual machine (VM), Ephemeral NVMe disks maintain full performance regardless of vCPU count. This is because they are physically attached to the VM and operate without relying on a remote disk controller. The difference is notable:

**Ultra Disk:**Achieving 400,000 IOPS requires a 112-vCPU VM (for example,[Standard_E112ibds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series-nvme)).**Local NVMe:**An 8-vCPU VM (for example,[Standard_L8s_v3](/en-us/azure/virtual-machines/sizes/storage-optimized/lsv3-series?tabs=sizestoragelocal#sizes-in-series)) can deliver 400,000 IOPS.

This results in approximately 14 times fewer vCPUs for equivalent IOPS performance, offering a substantial reduction in compute resource requirements.

This best practices article focuses on storage considerations for cluster operators. In this article, you learn:

- Common scenarios where ephemeral NVMe data disks provide performance benefits.
- How to identify which VM sizes support ephemeral NVMe data disks.
- How to use ephemeral NVMe data disks for your Kubernetes workloads.
- How ephemeral NVMe data disks work when your AKS nodes use ephemeral OS disks.
- How to measure the performance of your workloads using ephemeral NVMe data disks.

## Common scenarios of high-performance workloads

Ephemeral NVMe data disks are ideal for workloads that demand high throughput, low latency, and fast access to temporary or intermediate data. The following scenarios highlight where local NVMe disks provide the most significant benefits:

### High-performance databases (for example, PostgreSQL)

For databases such as PostgreSQL, especially in high-availability (HA) or read-intensive deployments, local NVMe disks can dramatically improve transaction throughput and reduce query latency. When used for temporary tablespaces, write-ahead logs (WAL), or as a cache layer, NVMe disks help offload I/O from persistent storage, accelerating analytics and transactional workloads.

Best practices:

- Use NVMe-backed volumes for PostgreSQL temp directories and WAL logs to maximize IOPS and minimize latency.
- For HA scenarios, ensure that persistent data directories remain on durable storage, while using NVMe for non-persistent, high-churn data.
- See
[PostgreSQL HA on AKS](/en-us/azure/aks/postgresql-ha-overview)for architecture guidance.

### AI model hosting and inference (for example, KAITO)

AI model serving platforms like [KAITO](https://github.com/kaito-project/kaito) benefit from NVMe disks for rapid model loading, artifact caching, and high-throughput inference. When models are stored as Open Container Initiative (OCI) artifacts and loaded on demand, local NVMe storage ensures minimal cold start times and efficient batch processing.

Best practices:

- Use NVMe-backed volumes for model cache directories to accelerate model pulls and reduce inference latency.
- For distributed inference, ensure each node has sufficient NVMe capacity to cache frequently used models.
- Integrate with Kubernetes-native storage solutions (for example, Azure Container Storage) for automated management and monitoring.
- See
[KAITO model as OCI artifacts](https://kaito-project.github.io/kaito/docs/next/model-as-oci-artifacts)for architecture guidance.

### Data analytics and ETL pipelines

Workloads that process large volumes of intermediate data, such as [Spark](https://spark.apache.org/), [Dask](https://www.dask.org/), or custom ETL jobs, can apply NVMe disks for shuffle storage, temporary files, and scratch space. This approach reduces bottlenecks during data transformation and aggregation.

Best practices:

- Configure shuffle and temp directories to use NVMe-backed storage.
- Clean up temporary data promptly to maximize available space.

### Caching layers and key-value stores

In-memory databases and caching solutions (for example, Redis, Memcached, RocksDB) can use NVMe disks as a fast persistence layer or for overflow storage, providing a balance between speed and durability.

Best practices:

- Use NVMe for write-heavy cache workloads where persistence isn't critical.
- Monitor disk usage to avoid eviction or data loss due to node restarts.

### High-performance computing (HPC) and simulation

HPC workloads, including genomics, financial modeling, and scientific simulations, often require rapid access to large datasets and scratch space for intermediate results. NVMe disks provide the necessary bandwidth and low latency for these scenarios.

## Check VM sizes with ephemeral NVMe data disks

Ephemeral NVMe data disks are available on select Azure VM sizes that offer local, high-performance storage directly attached to the physical host. These disks are ideal for temporary data, such as caches, scratch files, or intermediate processing, and aren't persisted after a VM is deallocated or stopped. The number and capacity of NVMe disks vary by VM size and family.

To determine which VM sizes support ephemeral NVMe data disks and their configurations, refer to the [Azure VM documentation](/en-us/azure/virtual-machines/sizes) and the [AKS supported VM sizes](/en-us/azure/aks/quotas-skus-regions). Look for VM series such as [Lsv4](/en-us/azure/virtual-machines/sizes/storage-optimized/lsv4-series) and [Ddsv6](/en-us/azure/virtual-machines/sizes/general-purpose/ddsv6-series), which are designed for high-throughput, low-latency workloads.

The following table lists example VM sizes and their NVMe disk configurations:

| VM Size | Number of NVMe Disks | Total NVMe Capacity (GiB) |
|---|---|---|
| Standard_L4s_v4 | 2 | 894 |
| Standard_L8s_v4 | 4 | 1,788 |
| Standard_L96s_v4 | 12 | 21,456 |
| Standard_D16ds_v6 | 2 | 880 |
| Standard_D32ds_v6 | 4 | 1,760 |
| Standard_D96ds_v6 | 6 | 5,280 |

For AI workloads that require GPU acceleration, consider VM sizes in the NC, ND, and NV series. Some GPU-enabled VM sizes, such as `Standard_NC48ads_A100_v4`

and `Standard_ND96isr_H100_v5`

, offer local NVMe storage in addition to powerful GPUs. These VMs are suitable for AI training, inference, and other compute-intensive scenarios where both GPU and fast local storage are needed.

Example GPU VM sizes with NVMe disks:

| VM Size | GPU Type | Number of NVMe Disks | Total NVMe Capacity (GiB) |
|---|---|---|---|
| Standard_NC48ads_A100_v4 | 2 x A100 | 2 | 1,788 |
| Standard_NC96ads_A100_v4 | 4 x A100 | 4 | 3,576 |
| Standard_ND96isr_H100_v5 | 8 x H100 | 8 | 28,610 |
| Standard_ND96isr_H200_v5 | 8 x H200 | 8 | 28,610 |

Note

Actual NVMe disk capacity and number might vary by region and VM generation. Not all GPU VM sizes include local NVMe storage. Always verify the latest VM specifications and NVMe disk availability in the Azure documentation, as configurations might change.

## Validate ephemeral NVMe data disks configuration

To ensure your AKS node is provisioned with ephemeral NVMe data disks, you can validate the configuration using the Azure CLI and by inspecting the node directly.

### Option 1: Use Azure CLI to check NVMe disk configuration

You can use the Azure CLI to inspect the VM size and attached NVMe disks with the following sample commands.

```
# Modify location and VM size if needed
locationName="eastus"
vmSize="Standard_L8s_v4"
az vm list-skus --resource-type virtualMachines --location $locationName \
--query "[?name=='$vmSize'].{
SkuName: name,
NvmeDiskSizeInMiB: capabilities[?name=='NvmeDiskSizeInMiB'] | [0].value,
NvmeSizePerDiskInMiB: capabilities[?name=='NvmeSizePerDiskInMiB'] | [0].value
}" -o table
SkuName NvmeDiskSizeInMiB NvmeSizePerDiskInMiB
--------------- ------------------- ----------------------
Standard_L8s_v4 1830912 457728
```


### Option 2: Use `lsblk`

to check disk and mount layout on the node

Login into an AKS node:

```
kubectl get nodes
# Modify the node name from above list as needed
nodeName="aks-myworkload-22647054-vmss000000"
# Use your approach to login into the node.
kubectl debug "node/$nodeName" \
--image=ubuntu \
--profile=sysadmin -it \
-- chroot /host /bin/bash
```


Once connected, use `lsblk`

to list block devices and identify NVMe disks:

```
lsblk -o NAME,HCTL,SIZE,MOUNTPOINT,MODEL
NAME HCTL SIZE MOUNTPOINT MODEL
sr0 0:0:0:2 750K Virtual DVD-ROM
nvme0n1 110G Microsoft NVMe Direct Disk v2
```


NVMe disks typically appear as `nvme*n1`

and are configured with `Microsoft NVMe Direct Disk*`

on model. This result confirms the presence and configuration of ephemeral NVMe data disks on your AKS node.

## Use ephemeral NVMe data disks in workloads

There are several ways to use ephemeral NVMe data disks in your AKS workloads. The most common approaches are:

### Azure Container Storage (recommended)

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction) is a Kubernetes-native storage solution that abstracts and manages local NVMe disks as persistent volumes, with advanced orchestration and data services.

You can deploy Azure Container Storage in your AKS cluster and provision volumes using standard Kubernetes PVCs.

Azure Container Storage offers the following advantages:

- Kubernetes-native experience with PersistentVolumeClaims.
- Automated discovery and management of NVMe disks for any VM sizes.
- Supports advanced features: dynamic provisioning, data security, and native integration with AKS.
- Improved reliability and operational simplicity.
- Enables high-performance workloads with default volume striping cross all available disks.

Azure Container Storage is the best option for Kubernetes workloads to orchestrate ephemeral NVMe data disks. It combines the raw performance of NVMe disks with Kubernetes-native management, security, and built-in integration with Azure’s monitoring features and Prometheus. This approach reduces operational complexity, improves reliability, and enables advanced scenarios (such as scaling and failover) that are difficult to achieve with `emptyDir`

or `hostPath`

.

For more information, see [Azure Container Storage documentation](/en-us/azure/storage/container-storage/container-storage-introduction).

`emptyDir`

Volumes

`emptyDir`

is a Kubernetes volume type that uses the node's local storage. When backed by NVMe disks, `emptyDir`

provides high throughput and low latency for temporary data.

To use this method, define an `emptyDir`

volume in your Pod spec. By default, it uses the fastest available storage (NVMe if present).

#### Advantages

- Simple to use and configure.
- No external dependencies.
- High performance when backed by NVMe.

#### Disadvantages

- Data is lost if the Pod is rescheduled to another node.
- No data persistence or replication.
- Limited to single NVMe disk.

`hostPath`

Volumes

`hostPath`

mounts a specific directory or disk from the node’s filesystem into the Pod. You can target NVMe mount points directly.

To use this method, specify the NVMe disk path (for example, `/mnt`

or `/mnt/nvme0n1`

) in the Pod spec.

#### Advantages

- Direct access to NVMe disk.
- Useful for advanced scenarios (for example, custom formatting, partitioning).

#### Disadvantages

- Tightly coupled to node layout; not portable.
- Security risks if not properly restricted.
- Limited to single NVMe disk.

## Ephemeral NVMe data disks with ephemeral OS disks

When deploying AKS nodes with local NVMe data disks, such as the `Standard_D2ads_v6`

VM size (single 100 GiB NVMe disk) with ephemeral OS disks setting opt-in, you might observe that the ephemeral OS disk (for example, 60 GiB) is provisioned from the NVMe capacity. However, the unused NVMe space (in this example, the extra 40 GiB) isn’t available to use, and there’s no supported way to access or recover it after the node is created.

This behavior is by design, as the ephemeral OS disk requirements dictate how the NVMe device is partitioned at provisioning time. It can be confusing since you don’t get access to all of its storage, especially with many VM sizes that come with only one NVMe disk.

Use the following example to validate this behavior:

```
# Create Standard_D2ads_v6 (Single 100 GiB NVMe disk) node pool using ephemeral OS disk with 60 GiB capacity
az aks nodepool add \
--resource-group $resourceGroup \
--cluster-name $clusterName \
--name $nodePoolName \
--node-count 1 \
--node-vm-size Standard_D2ads_v6 \
--node-osdisk-type Ephemeral \
--node-osdisk-size 60
kubectl debug "node/$nodeName" \
--image=ubuntu \
--profile=sysadmin -it \
-- chroot /host /bin/bash
lsblk -o NAME,FSTYPE,LABEL,MOUNTPOINT,SIZE,VENDOR,MODEL
NAME FSTYPE LABEL MOUNTPOINT SIZE VENDOR MODEL
sr0 750K Msft Virtual DVD-ROM
nvme0n1 60G MSFT NVMe Accelerator v1.0
|-nvme0n1p1 ext4 cloudimg-rootfs / 59.9G
|-nvme0n1p14 4M
`-nvme0n1p15 vfat UEFI /boot/efi 106M
```


When you use VM sizes with a single local NVMe data disk and enable ephemeral OS disk, the OS consumes the entire NVMe disk, leaving no space available for Kubernetes workloads to provision persistent volumes. For VM sizes with two or more local NVMe data disks, one disk is used for the ephemeral OS, and the others can be used to provision persistent volumes for your workloads.

### Current limitations

- The ephemeral OS disk consumes a portion of one local NVMe drive, with the remainder left inaccessible.
- There's no supported way to access or mount the unused NVMe space after node creation.
- You can't update or repartition the NVMe disk post-deployment.

### Customer impact

- Reduced usable NVMe capacity compared to what is advertised for the VM size.
- Inability to fully use high-performance local storage for workloads.
- Potential confusion and inconvenience during upgrades or node replacement.

### Recommendation

Decide the intended use of local NVMe disks, either for the OS disk or for Kubernetes workload storage—before provisioning AKS nodes. Ephemeral OS disk configuration is immutable after node creation, so planning ahead avoids the need to recreate nodes if requirements change.

Omit the OS disk size input when creating AKS nodes with ephemeral OS disks on NVMe-backed VMs. This prevents misconfiguration and aligns with product documentation, reducing the risk of inaccessible capacity and upgrade issues.


Note

These improvements are important for user experience and operational efficiency, especially as more VM SKUs with single NVMe disks become available. Follow the latest AKS documentation and monitor Azure updates for enhancements in ephemeral disk management.

## Measure workload performance with ephemeral NVMe data disks

Ephemeral NVMe data disks deliver high throughput and low latency for AKS workloads, but it's important to validate performance against your application's requirements. Benchmark your workloads on different VM sizes to identify the optimal configuration, and adjust VM sizes or disk configurations as needed.

Set up your application using local NVMe volumes, then use workload-specific benchmarking tools to measure IOPS, throughput, and latency. For example, with PostgreSQL, follow [Create infrastructure for PostgreSQL](/en-us/azure/aks/create-postgresql-ha) to deploy your environment, and use [pgbench](https://cloudnative-pg.io/documentation/1.26/benchmarking/#pgbench) to evaluate database performance.

The following steps introduce generic benchmarking with fio and local NVMe volumes managed by Azure Container Storage.

Enable Azure Container Storage on your AKS cluster. See

[Azure Container Storage Quickstart](/en-us/azure/storage/container-storage/container-storage-aks-quickstart)Deploy storage class, generic volume, fio pod with local NVMe volumes. See

[Use local NVMe with Azure Container Storage](/en-us/azure/storage/container-storage/use-container-storage-with-local-disk).Run the following fio command and modify as needed.

`# Run fio benchmark kubectl exec -it fiopod -- fio --directory=/mnt/cns --size=4000MB --filename_format='testfile.$jobnum' --wait_for_previous \ --thread --group_reporting --direct=1 --randrepeat=0 --norandommap=1 \ --ioengine=io_uring --numjobs=8 --disable_clat=1 --disable_slat=1 \ --name=precondition --bs=1M --iodepth=64 --rw=write \ --name=randwritebench --rw=randwrite --bs=4k --iodepth=16 --time_based --runtime=60 \ --name=randreadbench --rw=randread --bs=4k --iodepth=16 --time_based --runtime=60 \ --name=seqwritebench --rw=write --bs=128k --iodepth=16 --time_based --runtime=60 \ --name=seqreadbench --rw=read --bs=128k --iodepth=16 --time_based --runtime=60 > ./fio.log result=$(cat ./fio.log | \ awk ' BEGIN { print "Scenario,Type,IOPS,BW(MiB/s)" } /^[a-z]+bench:/ { split($1, a, ":") scenario = a[1] } /read: IOPS=/ && scenario ~ /(randreadbench|seqreadbench)/ { type = "read" match($0, /IOPS=([0-9.]+)([kM]?)/, iops_arr) match($0, /BW=([0-9.]+)MiB\/s/, bw_arr) iops = iops_arr[1] unit = iops_arr[2] if (unit == "k") iops *= 1000 else if (unit == "M") iops *= 1000000 bw = bw_arr[1] printf "%s,%s,%.0f,%.2f\n", scenario, type, iops, bw } /write: IOPS=/ && scenario ~ /(randwritebench|seqwritebench)/ { type = "write" match($0, /IOPS=([0-9.]+)([kM]?)/, iops_arr) match($0, /BW=([0-9.]+)MiB\/s/, bw_arr) iops = iops_arr[1] unit = iops_arr[2] if (unit == "k") iops *= 1000 else if (unit == "M") iops *= 1000000 bw = bw_arr[1] printf "%s,%s,%.0f,%.2f\n", scenario, type, iops, bw } ' | column -t -s,)`

Run fio on the VM with single NVMe disk (for example, standard_l8s_v3) and the VM with two NVMe disks (for example, Standard_L16s_v3). Evaluate the performance improvements from the NVMe volume striping cross multiple NVMe disks. See the following charts as examples:
