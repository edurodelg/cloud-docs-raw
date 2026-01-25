---
merged_at: 2026-01-25T12:25:33.955068
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: auto-upgrade-node-os-image.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-os-image -->

# Autoupgrade node OS images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS provides multiple autoupgrade channels dedicated to timely node-level OS security updates. This channel is different from cluster-level Kubernetes version upgrades and supersedes it.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Interactions between node OS autoupgrade and cluster autoupgrade

Node-level OS security updates are released at a faster rate than Kubernetes patch or minor version updates. The node OS autoupgrade channel grants you flexibility and enables a customized strategy for node-level OS security updates. Then, you can choose a separate plan for cluster-level Kubernetes version [autoupgrades](auto-upgrade-cluster).
It's best to use both cluster-level [autoupgrades](auto-upgrade-cluster) and the node OS autoupgrade channel together. Scheduling can be fine-tuned by applying two separate sets of [maintenance windows](planned-maintenance) - `aksManagedAutoUpgradeSchedule`

for the cluster [autoupgrade](auto-upgrade-cluster) channel and `aksManagedNodeOSUpgradeSchedule`

for the node OS autoupgrade channel.

## Channels for node OS image upgrades

The selected channel determines the timing of upgrades. When making changes to node OS auto-upgrade channels, allow up to 24 hours for the changes to take effect.

Note

- Node OS image auto-upgrade don't affect the cluster's Kubernetes version.
- Starting with API version 2023-06-01, the default for any new AKS cluster is
`NodeImage`

.

### Node OS channel changes that cause a reimage

The following node os channel transitions will trigger reimage on the nodes:

| From | To |
|---|---|
| Unmanaged | None |
| Unspecified | Unmanaged |
| SecurityPatch | Unmanaged |
| NodeImage | Unmanaged |
| None | Unmanaged |

### Available node OS upgrade channels

The following upgrade channels are available. You're allowed to choose one of these options:

| Channel | Description | OS-specific behavior |
|---|---|---|
`None` |
Your nodes don't have security updates applied automatically. This means you're solely responsible for your security updates. | N/A |
`Unmanaged` |
The OS built-in patching infrastructure automatically applies OS updates. Newly allocated machines are initially unpatched. The OS's infrastructure patches them at some point. | Ubuntu and Azure Linux (CPU node pools) apply security patches through unattended upgrade/dnf-automatic roughly once per day around 06:00 UTC. Windows doesn't automatically apply security patches, so this option behaves equivalently to `None` . You need to manage the reboot process using a tool like
`Unmanaged` . |
`SecurityPatch` |
OS security patches, which are AKS-tested, fully managed, and applied with safe deployment practices. AKS regularly updates the node's virtual hard disk (VHD) with patches from the image maintainer labeled "security only." There might be disruptions when the security patches are applied to the nodes. However AKS is limiting disruptions by only reimaging your nodes only when necessary, such as for certain kernel security packages. When the patches are applied, the VHD is updated and existing machines are upgraded to that VHD, honoring maintenance windows and surge settings. If AKS decides that reimaging nodes isn't necessary, it patches nodes live without draining pods and performs no VHD update. This option incurs the extra cost of hosting the VHDs in your node resource group. If you use this channel, Linux
|

`SecurityPatch`

works on kubernetes patch versions that are deprecated, so long as the minor Kubernetes version is still supported. [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)and[Azure Linux with OS Guard on AKS](use-azure-linux-os-guard)do not support`SecurityPatch`

.`NodeImage`

[unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates)are disabled by default. Node image upgrades are supported as long as cluster Kubernetes minor version is still in support. Node images are AKS-tested, fully managed, and applied with safe deployment practices.## What to choose - SecurityPatch Channel or NodeImage Channel?

There are two important considerations for you to choose between `SecurityPatch`

or `NodeImage`

channels.

| Property | NodeImage Channel | SecurityPatch Channel | Recommended Channel |
|---|---|---|---|
`Speed of shipping` |
The typical build, test, release, and rollout timelines for a new VHD can take approximately two weeks following safe deployment practices. Although in the event of CVEs, accelerated rollouts can occur on a case by case basis. The exact timing when a new VHD hits a region can be monitored via
|

`NodeImage`

, even with safe deployment practices. SecurityPatch has the advantage of 'Live-patching' in Linux environments, where patching leads to selective 'reimaging' and doesn't reimage every time a patch gets applied. Re-image if it happens is controlled by maintenance windows.`SecurityPatch`

`Bugfixes`

`NodeImage`

## Set the node OS autoupgrade channel on a new cluster

- Set the node OS autoupgrade channel on a new cluster using the
command with the`az aks create`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER="myAKSCluster$RANDOM_SUFFIX"
az aks create \
--resource-group $RESOURCE_GROUP \
--name $AKS_CLUSTER \
--node-os-upgrade-channel SecurityPatch \
--generate-ssh-keys
```


## Set the node OS autoupgrade channel on an existing cluster

- Set the node os autoupgrade channel on an existing cluster using the
command with the`az aks update`

`--node-os-upgrade-channel`

parameter. The following example sets the node OS autoupgrade channel to`SecurityPatch`

.

```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --node-os-upgrade-channel SecurityPatch
```


Results:

```
{
"autoUpgradeProfile": {
"nodeOsUpgradeChannel": "SecurityPatch"
}
}
```


## Update ownership and schedule

The default cadence means there's no planned maintenance window applied.

| Channel | Updates Ownership | Default cadence |
|---|---|---|
`Unmanaged` |
OS driven security updates. AKS has no control over these updates. | Nightly around 6AM UTC for Ubuntu and Azure Linux. Monthly for Windows. |
`SecurityPatch` |
AKS-tested, fully managed, and applied with safe deployment practices. For more information, see
|

`NodeImage`

[AKS Node Images in Release tracker](release-tracker)Note

While Windows security updates are released on a monthly basis, using the `Unmanaged`

channel won't automatically apply these updates to Windows nodes. If you choose the `Unmanaged`

channel, you need to manage the reboot process for Windows nodes.

## Node channel known limitations

Currently, when you set the

[cluster autoupgrade channel](auto-upgrade-cluster)to`node-image`

, it also automatically sets the node OS autoupgrade channel to`NodeImage`

. You can't change node OS autoupgrade channel value if your cluster autoupgrade channel is`node-image`

. In order to set the node OS autoupgrade channel value, check the[cluster autoupgrade channel](auto-upgrade-cluster)value isn't`node-image`

.The

`SecurityPatch`

channel isn't supported on Windows OS node pools.

Note

Use CLI version 2.61.0 or above for the `SecurityPatch`

channel.

## Node OS planned maintenance windows

Planned maintenance for the node OS autoupgrade starts at your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of four hours or more.

For more information on Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Node OS autoupgrades FAQ

### How can I check the current nodeOsUpgradeChannel value on a cluster?

Run the `az aks show`

command and check the "autoUpgradeProfile" to determine what value the `nodeOsUpgradeChannel`

is set to:

```
az aks show --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER --query "autoUpgradeProfile"
```


Results:

```
{
"nodeOsUpgradeChannel": "SecurityPatch"
}
```


### How can I monitor the status of node OS autoupgrades?

To view the status of your node OS auto upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events as mentioned in [Upgrade an AKS cluster](upgrade-cluster). AKS also emits upgrade-related Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I change the node OS autoupgrade channel value if my cluster autoupgrade channel is set to `node-image`

?

No. Currently, when you set the [cluster autoupgrade channel](auto-upgrade-cluster) to `node-image`

, it also automatically sets the node OS autoupgrade channel to `NodeImage`

. You can't change the node OS autoupgrade channel value if your cluster autoupgrade channel is `node-image`

. In order to be able to change the node OS autoupgrade channel values, make sure the [cluster autoupgrade channel](auto-upgrade-cluster) isn't `node-image`

.

### Why is `SecurityPatch`

recommended over `Unmanaged`

channel?

On the `Unmanaged`

channel, AKS has no control over how and when the security updates are delivered. With `SecurityPatch`

, the security updates are fully tested and follow safe deployment practices. `SecurityPatch`

also honors maintenance windows. For more information, see [Increased security and resiliency of Canonical workloads on Azure](https://techcommunity.microsoft.com/t5/linux-and-open-source-blog/increased-security-and-resiliency-of-canonical-workloads-on/ba-p/3970623).

### Does `SecurityPatch`

always lead to a reimage of my nodes?

AKS limits reimages to only when necessary, such as certain kernel packages that may require a reimage to get fully applied. `SecurityPatch`

is designed to minimize disruptions as much as possible. If AKS decides reimaging nodes isn't necessary, it patches nodes live without draining pods and no VHD update is performed in such cases.

### Why does `SecurityPatch`

channel requires to reach `snapshot.ubuntu.com`

endpoint?

With the `SecurityPatch`

channel, the Linux cluster nodes have to download the required security patches and updates from ubuntu snapshot service described in [ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments](https://ubuntu.com/blog/ubuntu-snapshots-on-azure-ensuring-predictability-and-consistency-in-cloud-deployments).

### How do I know if a `SecurityPatch`

or `NodeImage`

upgrade is applied on my node?

Run the `kubectl get nodes --show-labels`

command to list the nodes in your cluster and their labels.

Among the returned labels, you should see a line similar to the following output:

```
kubernetes.azure.com/node-image-version=AKSUbuntu-2204gen2containerd-202410.27.0-2024.12.01
```


Here, the base node image version is `AKSUbuntu-2204gen2containerd-202410.27.0`

. If applicable, the security patch version typically follows. In the above example, it's `2024.12.01`

.

The same details also be looked up in the Azure portal under the node label view:

## Next steps

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).


---

<!-- DOCUMENTO FUSIONADO: quotas-skus-regions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/quotas-skus-regions -->

# Quotas, virtual machine size restrictions, and region availability in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure services set default limits and quotas for resources and features, including usage restrictions for certain virtual machine (VM) SKUs.

This article details the default resource limits for Azure Kubernetes Service (AKS) resources and the availability of AKS in Azure regions.

## Service quotas and limits

| Resource | Limit |
|---|---|
| Maximum number of clusters per subscription globally | 5,000 |
| Maximum nodes per cluster with Virtual Machine Scale Sets and
|

[node pools](/en-us/azure/aks/create-node-pools)Note: If you're unable to scale up to 5,000 nodes per cluster, see

[Best Practices for Large Clusters](/en-us/azure/aks/best-practices-performance-scale-large).[Kubenet](/en-us/azure/aks/concepts-network-legacy-cni#kubenet)networking plug-inAzure CLI default: 110

Azure Resource Manager template default: 110

Azure portal deployment default: 30

[Azure Container Networking Interface (Azure CNI)](/en-us/azure/aks/concepts-network-cni-overview)1Maximum recommended for Windows Server containers: 110

Default: 30

OSM controllers per cluster: 1

Pods per OSM controller: 1600

Kubernetes service accounts managed by OSM: 160

[Standard Load Balancer SKU](/en-us/azure/load-balancer/load-balancer-overview)1 Windows Server containers must use Azure CNI networking plug-in. Kubenet isn't supported for Windows Server containers.

| Kubernetes Control Plane tier | Limit |
|---|---|
| Standard tier | Automatically scales Kubernetes API server based on load. Larger control plane component limits and API server/etcd instances. |
| Free tier | Limited resources with
Not advised for production/critical workloads. |

### Quota limits on AKS Managed Clusters

Starting in September 2025, Azure Kubernetes Service will begin rolling out a change to enable quota for all current and new AKS customers. This rollout is expected to take place between September 1-30, 2025.

AKS quota will represent a limit of the maximum number of managed clusters (AKS clusters) that an Azure subscription can create per region. Once managed cluster quota is released, customers will need both quota for managed clusters and quota for their nodes (VM skus) in order to create an AKS cluster.

**Existing AKS customer subscriptions** will be given a default limit at or above their current usage depending on the available regional capacity. **Existing subscriptions using AKS for the first time and new subscriptions** will be given a default limit.

Customers can [view quota limits and usage](/en-us/azure/quotas/view-quotas) and [request additional quota](/en-us/azure/quotas/quickstart-increase-quota-portal) via the Azure portal Quotas page or via the [Quotas REST API](/en-us/rest/api/reserved-vm-instances/quotaapi). Prior to rollout completion, quota limits and usage *may* be visible in the Portal Quotas blade and customers will be able to request quota —however, the limits will not be enforced until rollout is complete.


lightbox="./media/quotas-skus-regions/portal-quotas-page-expanded.png"

When Managed Clusters Quota is rolled out, customers will receive the following error if they attempt to create a new cluster and are out of quota:

```
ManagedClusterCountExceedsQuotaLimit: Operation results in exceeding quota limits for managed clusters. Maximum allowed: %d, Current usage: %d, Additional requested: %d. Consider deleting unused clusters or requesting a quota increase. To request a quota increase, follow the instructions here: https://learn.microsoft.com/azure/quotas/quickstart-increase-quota-portal.
```


To remedy this, customers can [request additional quota in the Azure portal Quotas page](/en-us/azure/quotas/view-quotas) or via the [Quotas REST API](/en-us/rest/api/reserved-vm-instances/quotaapi).

#### AKS Managed Clusters Quota Limits

| Subscription Type | Default number of AKS clusters per subscription per region for new subscriptions1 |
Maximum number of AKS clusters per subscription per region via self service using
2 |
|---|

1 The default number of AKS clusters per subscription per region for new subscriptions may vary in regions with capacity constraints.

2 To request an increase of the quota limit, [use the Azure portal Quotas request process](/en-us/azure/quotas/quickstart-increase-quota-portal). Quota increase requests above the maximum self service amount will require a support ticket. Free Trial and Azure for Students subscriptions aren't eligible for limit or quota increases. If you have a Free Trial or Azure for Students subscription, you can upgrade to a pay-as-you-go subscription to get higher quota limits.

### Throttling limits on AKS resource provider APIs

AKS uses the [token bucket](https://en.wikipedia.org/wiki/Token_bucket) throttling algorithm to limit certain AKS [resource provider](/en-us/azure/azure-resource-manager/management/resource-providers-and-types) APIs. Throttling limits ensures the performance of the service and promotes fair usage of the service for all customers.

The buckets have a fixed size (also known as a burst rate) and refill over time at a fixed rate (also known as a sustained rate). Each throttling limit is in effect at the regional level for the specified resource in that region. For example, in the following table, a Subscription can call ListManagedClusters a maximum of 60 times (burst rate) at once for each ResourceGroup, but can continue to make 1 call every second thereafter (sustained rate).

| API request | Bucket size | Refill rate | Scope |
|---|---|---|---|
| LIST ManagedClusters | 500 requests | 1 requests / 1 second | Subscription |
| LIST ManagedClusters | 60 requests | 1 request / 1 second | ResourceGroup |
| PUT AgentPool | 20 requests | 1 request / 1 minute | AgentPool |
| PUT ManagedCluster | 20 requests | 1 request / 1 minute | ManagedCluster |
| GET ManagedCluster | 60 requests | 1 request / 1 second | Managed Cluster |
| GET Operation Status | 200 requests | 2 requests / 1 second | Subscription |
| All Other APIs | 60 requests | 1 request / 1 second | Subscription |

Note

The ManagedClusters and AgentPools buckets are counted separately for the same AKS cluster.

If a request is throttled, the request returns HTTP response code `429`

(Too Many Requests) and the error code shows as `Throttled`

in the response. Each throttled request includes a `Retry-After`

in the HTTP response header with the interval to wait before retrying, in seconds. Clients that use a bursty API call pattern should ensure that the Retry-After can be handled appropriately. To learn more about Retry-After, see the [following article](https://developer.mozilla.org/docs/Web/HTTP/Headers/Retry-After). Specifically, AKS uses `delay-seconds`

to specify the retry.

## Provisioned infrastructure

All other network, compute, and storage limitations apply to the provisioned infrastructure. For the relevant limits, see [Azure subscription and service limits](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits).

Important

When you upgrade an AKS cluster, extra resources are temporarily consumed. These resources include available IP addresses in a virtual network subnet or virtual machine vCPU quota.

For Windows Server containers, you can perform an upgrade operation to apply the latest node updates. If you don't have the available IP address space or vCPU quota to handle these temporary resources, the cluster upgrade process fails. For more information on the Windows Server node upgrade process, see [Upgrade a node pool in AKS](use-multiple-node-pools#upgrade-a-node-pool).

## Supported VM sizes

The list of supported VM sizes in AKS is evolving with the release of new VM SKUs in Azure. Follow the [AKS release notes](https://github.com/Azure/AKS/releases) to stay informed of new supported SKUs.

## Restricted VM sizes

Each node in an AKS cluster contains a fixed amount of compute resources such as vCPU and memory. Due to the required compute resources needed to run Kubernetes correctly, certain VM SKU sizes are restricted by default in AKS. These restrictions are to ensure that pods can be scheduled and function correctly on these nodes.

### User node pools

For user node pools, VM sizes with fewer than two vCPUs and two GBs of RAM (memory) might not be used.

### System node pools

For system node pools, VM sizes with fewer than two vCPUs and four GBs of RAM (memory) might not be used. To ensure that the required *kube-system* pods and your applications can reliably be scheduled, [B series VMs](/en-us/azure/virtual-machines/sizes-b-series-burstable) aren't supported for system node pools and [Av1 series VMs](/en-us/azure/virtual-machines/sizes/retirement/av1-series-retirement) aren't recommended.

For more information on VM types and their compute resources, see [Sizes for virtual machines in Azure](/en-us/azure/virtual-machines/sizes).

## Supported container image sizes

AKS doesn't set a limit on the container image size. However, it's important to understand that the larger the container image, the higher the memory demand. This demand could potentially exceed resource limits or the overall available memory of worker nodes. By default, memory for VM size Standard_DS2_v2 for an AKS cluster is set to 7 GiB.

When a container image is large (1 TiB or more), kubelet might not be able to pull it from your container registry to a node due to lack of disk space.

## Region availability

For the latest list of where you can deploy and run clusters, see [AKS region availability](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

## Smart VM Defaults

As of May 2025, AKS automatically selects the optimal default VM SKU based on available capacity and quota if the parameter is unspecified during deployment. This default ensures that deployments are matched with the best possible SKU, enhancing performance and reliability while optimizing resource utilization. Previously, the default AKS VM SKU was Standard_DS2_V2, but there are now dynamic outcomes in default provisioning based on SKU availability that affects all new VM create operations.

## Cluster configuration presets in the Azure portal

When you create a cluster using the Azure portal, you can choose a preset configuration to quickly customize based on your scenario. You can modify any of the preset values at any time.

| Preset | Description |
|---|---|
| Production Standard | Best for most applications serving production traffic with AKS recommended best practices. |
| Dev/Test | Best for developing new workloads or testing existing workloads. |
| Production Economy | Best for serving production traffic in a cost conscious way if your workloads can tolerate interruptions. |
| Production Enterprise | Best for serving production traffic with rigorous permissions and hardened security. |

| Production Standard | Dev/Test | Production Economy | Production Enterprise | |
|---|---|---|---|---|
System node pool node size |
Standard_D8ds_v5 | Standard_D4ds_v5 | Standard_D8ds_v5 | Standard_D16ds_v5 |
System node pool autoscaling range |
2-5 nodes | 2-5 nodes | 2-5 nodes | 2-5 nodes |
User node pool node size |
Standard_D8ds_v5 | - | Standard_D8as_v4 | Standard_D8ds_v5 |
User node pool autoscaling range |
2-100 nodes | - | 0-25 nodes | 2-100 nodes |
Private cluster |
- | - | - | |
Availability zones |
- | - | ||
Azure Policy |
- | - | ||
Azure Monitor |
- | - | ||
Secrets store CSI driver |
- | - | ||
Network configuration |
Azure CNI Overlay | Azure CNI Overlay | Azure CNI Overlay | Azure CNI Overlay |
Network policy |
None | None | None | None |
Authentication and Authorization |
Local accounts with Kubernetes role-based access control (RBAC) | Local accounts with Kubernetes RBAC | Microsoft Entra ID Authentication with Azure role-based access control (Azure RBAC) | Microsoft Entra ID authentication with Azure RBAC |

## Next steps

You can increase certain default limits and quotas. If your resource supports an increase, request the increase through an [Azure support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest) (for **Issue type**, select **Quota**).
