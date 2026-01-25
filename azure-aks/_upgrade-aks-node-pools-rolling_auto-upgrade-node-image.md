---
merged_at: 2026-01-25T12:25:33.954546
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: upgrade-aks-node-pools-rolling.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-node-pools-rolling -->

# Configure rolling upgrades for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A rolling upgrade strategy upgrades nodes one at a time (or a few at a time), minimizing workload disruption while ensuring the node pool remains available throughout the upgrade process. This article explains how to configure rolling upgrades for AKS node pools, including surge settings, drain timeout, and soak time.

## Before you begin

- Ensure your control plane is already upgraded to the target Kubernetes version. You can't upgrade node pools to a version higher than the control plane. For more information, see
[Upgrade the AKS cluster control plane](upgrade-aks-control-plane). - If you're using the Azure CLI, this article requires Azure CLI version 2.34.1 or later. Use the
`az --version`

command to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install]. - You need the
`Microsoft.ContainerService/managedClusters/agentPools/write`

RBAC role permission to configure rolling upgrades for AKS node pools.

## Overview of rolling upgrade behavior

During a rolling upgrade, AKS performs the following operations for each node in the node pool:

**Add surge nodes**: Add new buffer nodes based on max surge (`--max-surge`

) settings to maintain capacity during the upgrade.**Cordon and drain nodes**:[Cordon and drain](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)the old nodes one at a time to minimize disruption to running applications. If you're using max surge, it cordons and drains as many nodes at the same time as the number of buffer nodes specified.**Wait for soak time**(optional): Wait for a configured[soak duration](#set-node-soak-time-value)before proceeding to allow workloads to stabilize on the new nodes before continuing the upgrade.**Reimage old nodes**: When the old nodes are drained, they're reimaged to receive the new version. The reimaged nodes become the buffer nodes for the next set of nodes to be upgraded.**Repeat**: The process repeats until all nodes in the node pool are upgraded.**Remove surge nodes**: After all nodes are upgraded, any remaining buffer nodes are removed, maintaining the original node pool size and balance.

## Configure rolling upgrade settings

### Customize node surge

Important

- Node surges require subscription quota for the requested max surge count for each upgrade operation. For example, a cluster that has five node pools, each with a count of four nodes, has a total of 20 nodes. If each node pool has a max surge value of 50%, extra compute and IP quota of 10 nodes (
*two*nodes ×*five*pools) is required to complete the upgrade. - The max surge setting on a node pool is persistent. Subsequent Kubernetes upgrades or node version upgrades use this setting. You can change the max surge value for your node pools at any time. For production node pools, we recommend a max surge setting of 33%.
- If you're using Azure CNI, validate there are available IPs in the subnet to
[satisfy IP requirements of Azure CNI](configure-azure-cni).

AKS configures upgrades to surge with one extra node by default. A default value of *one* for the max surge setting enables AKS to minimize workload disruption by creating an extra node before the cordon/drain of existing applications to replace an older versioned node. You can customize the max surge value per node pool. When you increase the max surge value, the upgrade process completes faster, but you might experience more disruptions during the upgrade process.

For example, a max surge value of `100%`

provides the fastest possible upgrade process but also causes all nodes in the node pool to be drained simultaneously. You might want to use a higher value like this for testing environments. For production node pools, we recommend a max surge setting of `33%`

.

AKS accepts both integer values and a percentage value for max surge. For example:

| Value type | Example | Description |
|---|---|---|
| Integer | `5` |
Five extra nodes to surge |
| Percentage | `50%` |
Surge value of half the current node count in the pool |

Max surge percent values can be a minimum of `1%`

and a maximum of `100%`

. A percent value is rounded up to the nearest node count. If the max surge value is higher than the required number of nodes to be upgraded, the number of nodes to be upgraded is used for the max surge value.

#### Set max surge value

Set max surge values for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) or

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

`--max-surge`

parameter. For example:```
# Set max surge for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33%
# Update max surge for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 5
```


### Customize unavailable nodes

Important

- You must set max surge to
`0`

in order to set a max unavailable value. The two values can't both be active at the same time. - Max unavailable doesn't create surge nodes during the upgrade process. Instead, AKS cordons
*n*nodes (the max unavailable value) at a time and evicts the pods to other nodes in the agent pool. This might cause workload disruptions if the pods can't be scheduled. - Max unavailable might cause more failures due to unsatisfied Pod Disruption Budgets (PDBs) since there are fewer resources for pods to be scheduled on. For more information, see
[Troubleshooting for Pod Disruption Budgets](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/error-code-poddrainfailure). - You can't set max unavailable on system node pools.

AKS can also configure upgrades to not use a surge node and upgrade the nodes in place. The max unavailable value determines how many nodes can be simultaneously cordoned and drained from the existing node pool nodes.

AKS accepts both integer values and a percentage value for max unavailable. For example:

| Value type | Example | Description |
|---|---|---|
| Integer | `5` |
Five nodes are cordoned from the existing nodes |
| Percentage | `50%` |
Half the current node count in the pool will be unavailable |

Max unavailable percent values can be a minimum of `1%`

and a maximum of `100%`

. A percent value is rounded up to the nearest node count.

#### Set max unavailable value

Set max unavailable values for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add),

[, or the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade)

`az aks nodepool upgrade`

`--max-unavailable`

parameter. For example:```
# Set max unavailable for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
# Update max unavailable for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
# Set max unavailable at upgrade time
az aks nodepool upgrade \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 0 \
--max-unavailable 5
```


### Customize node drain timeout

You might have long-running workloads on certain pods that you can't reschedule to another node during runtime. For example, a memory-intensive stateful workload that must finish running. In these cases, you can configure a node drain timeout that AKS respects in the upgrade workflow.

The default node drain timeout value is 30 minutes. Node drain timeout values can be a minimum of 5 minutes and a maximum of 24 hours.

If the drain timeout value elapses and pods are still running, the upgrade operation stops. Any subsequent `PUT`

operation resumes the stopped upgrade.

Tip

For long-running pods, you should also configure the [ terminationGracePeriodSeconds](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/) in your pod spec.

#### Set node drain timeout value

Set node drain timeout (in minutes) for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) or

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

`--drain-time-out`

parameter.```
# Set drain timeout for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--drain-time-out 100
# Update drain timeout for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--drain-time-out 45
```


### Customize node soak time

To enable a waiting period for a specified duration of time between draining a node and proceeding to reimage it and move on to the next node, you can set the soak time. This soak time gives you the opportunity to perform other tasks during the upgrade process, such as checking application health from a monitoring dashboard.

The default node soak time is 0 minutes. Node soak time values can be a minimum of 0 minutes and a maximum of 30 minutes. We recommend keeping soak time as short as reasonably possible. A higher node soak time increases the total upgrade duration and delays discovery of issues.

#### Set node soak time value

Set node soak time (in minutes) for new or existing node pools using the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add),

[, or](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)

`az aks nodepool update`

[command with the](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-upgrade)

`az aks nodepool upgrade`

`--node-soak-duration`

flag.```
# Set node soak time for a new node pool
az aks nodepool add \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--node-soak-duration 10
# Update node soak time for an existing node pool
az aks nodepool update \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33% \
--node-soak-duration 5
# Set node soak time when upgrading an existing node pool
az aks nodepool upgrade \
--name <node-pool-name> \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--max-surge 33% \
--node-soak-duration 20
```


## View AKS node upgrade events

View upgrade events using the `kubectl get events`

command to monitor the rolling upgrade progress.

```
kubectl get events --field-selector reason=Drain,reason=Surge,reason=Upgrade
```


Example output during an upgrade event:

```
default 2m1s Normal Drain node/aks-nodepool1-12345678-vmss000001 Draining node: [aks-nodepool1-12345678-vmss000001]
default 9m22s Normal Surge node/aks-nodepool1-12345678-vmss000002 Created a surge node [aks-nodepool1-12345678-vmss000002 nodepool1] for agentpool nodepool1
default 1m45s Normal Upgrade node/aks-nodepool1-12345678-vmss000001 Soak duration 5m0s after draining node: aks-nodepool1-12345678-vmss000001
```


## Recommended AKS node pool upgrade settings for production workloads

The following table outlines recommended node pool upgrade settings for production workloads:

| Setting | Recommendation |
|---|---|
Max surge |
Set to 33% for production node pools |
Drain timeout |
Configure based on your longest-running pod's requirements |
Soak time |
Use a short duration (0-5 minutes) unless you need manual verification |
Pod Disruption Budgets |
Configure PDBs for critical workloads to control pod eviction |
Upgrade order |
Upgrade non-production node pools first to validate the new version |


---

<!-- DOCUMENTO FUSIONADO: auto-upgrade-node-image.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-image -->

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
