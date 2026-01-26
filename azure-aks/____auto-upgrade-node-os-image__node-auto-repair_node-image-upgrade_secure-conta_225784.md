---
merged_at: 2026-01-26T20:54:26.171565
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-os-image -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-repair -->

# Azure Kubernetes Service (AKS) node auto-repair

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) continuously monitors the health state of worker nodes and performs automatic node repair if they become unhealthy. The Azure virtual machine (VM) platform [performs maintenance on VMs](/en-us/azure/virtual-machines/maintenance-and-updates) experiencing issues. AKS and Azure VMs work together to minimize service disruptions for clusters.

In this article, you learn how the automatic node repair functionality behaves for Windows and Linux nodes.

## How AKS checks for NotReady nodes

AKS uses the following rules to determine if a node is unhealthy and needs repair:

- The node reports the
status on consecutive checks within a 10-minute time frame.**NotReady** - The node doesn't report any status within 10 minutes.

You can manually check the health state of your nodes with the `kubectl get nodes`

command.

## How automatic repair works

Note

AKS initiates repair operations with the user account **aks-remediator**.

If AKS identifies an unhealthy node that remains unhealthy for at least *five* minutes, AKS performs the following actions:

- AKS reboots the node.
- If the node remains unhealthy after reboot, AKS reimages the node.
- If the node remains unhealthy after reimage and it's a Linux node, AKS redeploys the node.

AKS retries the restart, reimage, and redeploy sequence up to three times if the node remains unhealthy. The overall auto repair process can take up to an hour to complete.

## Limitations

AKS node auto-repair is a best effort service and we don't guarantee that the node is restored back to healthy status. If your node persists in an unhealthy state, we highly encourage that you perform manual investigation of the node. Learn more about [troubleshooting node NotReady status](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/node-not-ready-basic-troubleshooting).

There are cases where AKS doesn't perform automatic repair. Failure to automatically repair the node can occur either by design or if Azure can't detect that an issue exists. Examples of when auto-repair isn't performed include:

- A node status isn't being reported due to error in network configuration.
- A node failed to initially register as a healthy node.
- If either of the following taints are present on the node:
`node.cloudprovider.kubernetes.io/shutdown`

,`ToBeDeletedByClusterAutoscaler`

. - A node is in the process of being upgraded, resulting in the following annotation on the node
`"cluster-autoscaler.kubernetes.io/scale-down-disabled": "true"`

and`"kubernetes.azure.com/azure-cluster-autoscaler-scale-down-disabled-reason": "upgrade"`


## Monitor node auto-repair using Kubernetes events

When AKS performs node auto-repair on your cluster, AKS emits Kubernetes events from the aks-auto-repair source for visibility. The following events appear on a node object when auto-repair happens.

To learn more about accessing, storing, and configuring alerts on Kubernetes events, see [Use Kubernetes events for troubleshooting in Azure Kubernetes Service](events).

| Reason | Event Message | Description |
|---|---|---|
| NodeRebootStart | Node auto-repair is initiating a reboot action due to NotReady status persisting for more than 5 minutes. | This event is emitted to notify you when reboot is about to be performed on your node. This action is the first in the overall node auto-repair sequence. |
| NodeRebootEnd | Reboot action from node auto-repair is completed. | Emitted once reboot is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after the reboot is performed. |
| NodeReimageStart | Node auto-repair is initiating a reimage action due to NotReady status persisting for more than 5 minutes. | This event is emitted to notify you when reimage is about to be performed on your node. |
| NodeReimageEnd | Reimage action from node auto-repair is completed. | Emitted once reimage is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after the reimage is performed. |
| NodeRedeployStart | Node auto-repair is initiating a redeploy action due to NotReady status persisting more than 5 minutes. | This event is emitted to notify you when redeploy is about to be performed on your node. Redeploy is the last action in the node auto-repair sequence. |
| NodeRedeployEnd | Redeploy action from node auto-repair is completed. | Emitted once redeploy is complete on the node. This event doesn't indicate the health status (healthy or unhealthy) of the node after redeploy is performed. |

If any errors occur during the node auto-repair process, the following events are emitted with the verbatim error message. Learn more about [troubleshooting common node auto-repair errors](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/node-auto-repair-errors).

Note

*Error code* in the following event messages varies depending on the error reported.

| Reason | Event Message | Description |
|---|---|---|
| NodeRebootError | Node auto-repair reboot action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the reboot action. |
| NodeReimageError | Node auto-repair reimage action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the reimage action. |
| NodeRedeployError | Node auto-repair redeploy action failed due to an operation failure. See error details here: Error code |
Emitted when there's an error with the redeploy action. |

## Next steps

By default, you can access Kubernetes events and logs on your AKS cluster from the past 1 hour. To store and query events and logs from the past 90 days, enable [Container Insights](/en-us/azure/azure-monitor/containers/container-insights-overview#access-container-insights) for deeper troubleshooting on your AKS cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-image-upgrade -->

# Upgrade Azure Kubernetes Service (AKS) node images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) regularly provides new node images, so it's beneficial to upgrade your node images frequently to use the latest AKS features. Linux node images are updated weekly, and Windows node images are updated monthly. Image upgrade announcements are included in the [AKS release notes](https://github.com/Azure/AKS/releases), and it can take up to a week for these updates to be rolled out across all regions. You can also perform node image upgrades automatically and schedule them using planned maintenance. For more information, see [Automatically upgrade node images](auto-upgrade-node-image).

This article shows you how to upgrade AKS cluster node images and how to update node pool images without upgrading the Kubernetes version. For information on upgrading the Kubernetes version for your cluster, see [Upgrade an AKS cluster](upgrade-aks-cluster).

Note

The AKS cluster must use virtual machine scale sets for the nodes.

It's not possible to downgrade a node image version (for example *AKSUbuntu-2204 to AKSUbuntu-1804*, or *AKSUbuntu-2204-202308.01.0 to AKSUbuntu-2204-202307.27.0*).

## Connect to your AKS cluster

Connect to your AKS cluster using the [

`az aks get-credentials`

][az-aks-get-credentials] command.`az aks get-credentials \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER`


## Check for available node image upgrades

Check for available node image upgrades using the

command.`az aks nodepool get-upgrades`

`az aks nodepool get-upgrades \ --nodepool-name $AKS_NODEPOOL \ --cluster-name $AKS_CLUSTER \ --resource-group $AKS_RESOURCE_GROUP`

In the output, find and make note of the

`latestNodeImageVersion`

value. This value is the latest node image version available for your node pool.Check your current node image version to compare with the latest version using the

command.`az aks nodepool show`

`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --query nodeImageVersion`

If the

`nodeImageVersion`

value is different from the`latestNodeImageVersion`

, you can upgrade your node image.

## Upgrade all node images in all node pools

Upgrade all node images in all node pools in your cluster using the

command with the`az aks upgrade`

`--node-image-only`

flag.`az aks upgrade \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER \ --node-image-only \ --yes`

You can check the status of the node images using the

`kubectl get nodes`

command.Note

This command might differ slightly depending on the shell you use. For more information on Windows and PowerShell environments, see the

[Kubernetes JSONPath documentation](https://kubernetes.io/docs/reference/kubectl/jsonpath/).`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

When the upgrade completes, use the

command to get the updated node pool details. The current node image is shown in the`az aks show`

`nodeImageVersion`

property.`az aks show \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER`


## Upgrade a specific node pool

Update the OS image of a node pool without doing a Kubernetes cluster upgrade using the

command with the`az aks nodepool upgrade`

`--node-image-only`

flag.`az aks nodepool upgrade \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --node-image-only`

You can check the status of the node images with the

`kubectl get nodes`

command.Note

This command may differ slightly depending on the shell you use. For more information on Windows and PowerShell environments, see the

[Kubernetes JSONPath documentation](https://kubernetes.io/docs/reference/kubectl/jsonpath/).`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

When the upgrade completes, use the

command to get the updated node pool details. The current node image is shown in the`az aks nodepool show`

`nodeImageVersion`

property.`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL`


## Upgrade node images with node surge

To speed up the node image upgrade process, you can upgrade your node images using a customizable node surge value. By default, AKS uses one extra node to configure upgrades.

Upgrade node images with node surge using the

command with the`az aks nodepool update`

`--max-surge`

flag to configure the number of nodes used for upgrades.Note

To learn more about the trade-offs of various

`--max-surge`

settings, see[Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade).`az aks nodepool update \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL \ --max-surge 33% \ --no-wait`

You can check the status of the node images with the

`kubectl get nodes`

command.`kubectl get nodes -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.metadata.labels.kubernetes\.azure\.com\/node-image-version}{"\n"}{end}'`

Get the updated node pool details using the

command. The current node image is shown in the`az aks nodepool show`

`nodeImageVersion`

property.`az aks nodepool show \ --resource-group $AKS_RESOURCE_GROUP \ --cluster-name $AKS_CLUSTER \ --name $AKS_NODEPOOL`


## Next steps

- For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). - Learn how to upgrade the Kubernetes version with
[Upgrade an AKS cluster](upgrade-aks-cluster). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn more about multiple node pools with
[Create multiple node pools](create-node-pools). - Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/secure-container-access -->

# Security container access to resources using built-in Linux security features

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to secure container access to resources for your Azure Kubernetes Service (AKS) workloads.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview

In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access.

You can use built-in Kubernetes *pod security contexts* to define more permissions, such as the user or group to run as, the Linux capabilities to expose, or setting `allowPrivilegeEscalation: false`

in the pod manifest. For more best practices, see [Secure pod access to resources](https://kubernetes.io/docs/concepts/security/pod-security-standards/).

To improve the host isolation and decrease lateral movement on Linux, you can use *user-namespaces*.

For even more granular control of container actions, you can use built-in Linux security features such as *AppArmor* and *seccomp*.

- Define Linux security features at the node level.
- Implement features through a pod manifest.

Built-in Linux security features are only available on Linux nodes and pods.

Note

Currently, Kubernetes environments aren't completely safe for hostile multitenant usage. Additional security features, like *Microsoft Defender for Containers*, *AppArmor*, *seccomp*, *user-namespaces*, *Pod Security Admission*, or *Kubernetes RBAC for nodes*, efficiently block exploits.

For true security when running hostile multitenant workloads, only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster, not an individual node.

For these types of hostile multitenant workloads, you should use physically isolated clusters.

## User-namespaces

Linux pods run using several namespaces by default: a network namespaces to isolate the network identity and a PID namespace to isolate the processes. A [user-namespace](https://man7.org/linux/man-pages/man7/user_namespaces.7.html) isolates the users inside the container from the users on the host. It also limits the scope of capabilities and the pod's interactions with the rest of the system.

The UIDs and GIDs inside the container are mapped to unprivileged users on the host, so all interaction with the rest of the host happen as those unprivileged UID and GID. For example, root inside the container (UID 0) can be mapped to user 65536 on the host. Kubernetes creates the mapping to guarantee it doesn't overlap with other pods using user-namespaces on the system.

The Kubernetes implementation has some key benefits:

**Increased host isolation**: If a container escapes the pod boundaries, even if it runs as root inside the container, it has no privileges on the host. The reason is because the UIDs and GIDs of the container are mapped to unprivileged users on the host. If there's a container escape, user-namespaces greatly protects what files on the host a container can read/write, which process it can send signals to. Capabilities granted are only valid inside the user namespace and not on the host.**Prevention of lateral movement**: As the UIDs and GIDs for different containers are mapped to different, nonoverlapping UIDs and GIDs on the host, containers have a harder time attacking each other. For example, suppose container A runs with different UIDs and GIDs on the host than container B. In case of a container breakout, the operations it can do on container B's files and processes are limited: only read/write what a file allows to others. But not even that ends up being possible, as there's an extra prevention on the parent directory of the pod root volume to make sure only the pod GID can access it.**Honor Least-privilege principle**: As the UIDs and GIDs are mapped to unprivileged users on the host, only users that need the privilege on the host (and disable user namespaces) get it. Without user namespaces, there's no separation between container's users and host's users. We can't avoid giving privileges on the host to processes that don't need it, when they need privilege just inside the container.**Enablement of new use cases**: User namespaces allow containers to gain certain capabilities inside their own user namespace without affecting the host. The capabilities granted restricted to the pod unlocks new possibilities, such as running applications that require privileged operations without granting full root access on the host. Common new use-cases that can be implemented securely are: running nested containers and unprivileged container builds.**Unprivileged container setup**: Most of the container creation and setup doesn't run as root on the host, which significantly limits the impact of many CVEs.

None of these things are true when user-namespaces aren't used. If the container runs as root, when user-namespaces aren't used, the process is running as root on the host, the capabilities are valid on the host and the container setup is done as root on the host.

### Before you begin

Before you begin, make sure you have the following:

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Minimum kubernetes version 1.33 for the control plane and worker nodes. If you're not using kubernetes version 1.33 or higher, you'll need to
[upgrade your kubernetes version](upgrade-aks-cluster). - Worker nodes running Azure Linux 3.0 or Ubuntu 24.04. If you're not using these OS versions, you will not have the minimum
[stack requirements](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/#before-you-begin)to enable user-namespaces. You'll need to[upgrade your OS version](upgrade-os-version).

### Limitations

- User-namespaces is a linux kernel feature and is not supported for Windows node pools.
- Don't hesitate to check the
[Kubernetes documentation for user namespaces](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/), in particular the limitations section.

### Enable user-namespaces

There are no configurations needed to use this feature. If using the required AKS version, everything works out of the box.

Create a file named

`mypod.yaml`

and copy in the following manifest:To use user-namespaces, the yaml needs to have the field

`hostUsers: false`

.`apiVersion: v1 kind: Pod metadata: name: userns spec: hostUsers: false containers: - name: shell command: ["sleep", "infinity"] image: debian`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f mypod.yaml`

Check the status of the deployed pods using the

`kubectl get pods`

command.`kubectl get pods`

Exec into the pod to check

`/proc/self/uid_map`

by using the`kubectl exec`

command:`kubectl exec -ti userns -- bash # Now inside the pod run cat /proc/self/uid_map`


The output should have 65536 in the last column. For example:

```
0 833617920 65536
```


### CVEs mitigated

Here are some CVEs that are completely/partially mitigated with user-namespaces.

Bear in mind the list isn't exhaustive, it's just a selection of CVEs with high score that are mitigated:

[CVE-2019-5736](https://nvd.nist.gov/vuln/detail/CVE-2019-5736)- Score 8.6 (HIGH)[CVE 2024-21262](https://github.com/opencontainers/runc/security/advisories/GHSA-xr7r-f8xq-vfvv): Score 8.6 (HIGH)[CVE 2022-0492](https://unit42.paloaltonetworks.com/cve-2022-0492-cgroups/): Score 7.8 (HIGH)[CVE-2021-25741](https://nvd.nist.gov/vuln/detail/CVE-2021-25741): Score: 8.1 (HIGH) / 8.8 (HIGH)[CVE-2017-1002101](https://nvd.nist.gov/vuln/detail/CVE-2017-1002101): Score: 9.6 (CRITICAL) / 8.8(HIGH)

To learn more, read this [blog post](https://kubernetes.io/blog/2025/04/25/userns-enabled-by-default/) with additional information around user-namespaces.

## App Armor

To limit container actions, you can use the [AppArmor](https://kubernetes.io/docs/tutorials/clusters/apparmor/) Linux kernel security module. AppArmor is available as part of the underlying AKS node OS and is enabled by default. You create AppArmor profiles that restrict read, write, or execute actions, or system functions like mounting filesystems. Default AppArmor profiles restrict access to various `/proc`

and `/sys`

locations and provide a means to logically isolate containers from the underlying node. AppArmor works for any application that runs on Linux, not just Kubernetes pods.

Note

Azure Linux 3.0 does not offer AppArmor support. For Azure Linux 3.0 nodes, the recommendation is to leverage SELinux instead of AppArmor for mandatory access control.

To see AppArmor in action, the following example creates a profile that prevents writing to files.

[SSH](manage-ssh-node-access)to an AKS node.Create a file named

*deny-write.profile*.Copy and paste the following content:

`#include <tunables/global> profile k8s-apparmor-example-deny-write flags=(attach_disconnected) { #include <abstractions/base> file, # Deny all file writes. deny /** w, }`


AppArmor profiles are added using the `apparmor_parser`

command.

Add the profile to AppArmor.

Specify the name of the profile created in the previous step:

`sudo apparmor_parser deny-write.profile`

If the profile is correctly parsed and applied to AppArmor, you won't see any output and you'll return to the command prompt.

From your local machine, create a pod manifest named

*aks-apparmor.yaml*. This manifest:- Defines an annotation for
`container.apparmor.security.beta.kubernetes`

. - References the
*deny-write*profile created in the previous steps.

`apiVersion: v1 kind: Pod metadata: name: hello-apparmor annotations: container.apparmor.security.beta.kubernetes.io/hello: localhost/k8s-apparmor-example-deny-write spec: containers: - name: hello image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: [ "sh", "-c", "echo 'Hello AppArmor!' && sleep 1h" ]`

- Defines an annotation for
With the pod deployed, run the following command and verify the

*hello-apparmor*pod shows a*Running*status:`kubectl get pods NAME READY STATUS RESTARTS AGE aks-ssh 1/1 Running 0 4m2s hello-apparmor 0/1 Running 0 50s`


For more information about AppArmor, see [AppArmor profiles in Kubernetes](https://kubernetes.io/docs/tutorials/clusters/apparmor/).

## Secure computing (seccomp)

While AppArmor works for any Linux application, [seccomp ( secure computing)](https://kubernetes.io/docs/reference/node/seccomp/) works at the process level. Seccomp is also a Linux kernel security module and is natively supported by the

`containerd`

runtime used by AKS nodes. With seccomp, you can limit a container's system calls. Seccomp establishes an extra layer of protection against common system call vulnerabilities exploited by malicious actors and allows you to specify a default profile for all workloads in the node.### Configure a default seccomp profile (preview)

You can apply default seccomp profiles using [custom node configurations](/en-us/azure/aks/custom-node-configuration) when creating a new Linux node pool. There are two values supported on AKS: `RuntimeDefault`

and `Unconfined`

. Some workloads might require a lower number of syscall restrictions than others. This means that they can fail during runtime with the 'RuntimeDefault' profile. To mitigate such a failure, you can specify the `Unconfined`

profile. If your workload requires a custom profile, see [Configure a custom seccomp profile](#configure-a-custom-seccomp-profile).

#### Limitations

- SeccompDefault is not a supported parameter for windows node pools.
- SeccompDefault is available starting in 2024-09-02-preview API.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

#### Register the `KubeletDefaultSeccompProfilePreview`

feature flag

Register the

`KubeletDefaultSeccompProfilePreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "KubeletDefaultSeccompProfilePreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "KubeletDefaultSeccompProfilePreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


#### Restrict your container's system calls with seccomp

**1. Follow steps to apply a seccomp profile in your kubelet configuration by specifying "seccompDefault": "RuntimeDefault"**.


`RuntimeDefault`

uses containerd's default seccomp profile, restricting certain system calls to enhance security. Restricted syscalls will fail. For more information, see the [containerD default seccomp profile](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51).

**2. Check that the configuration was applied**.

You can confirm the settings are applied to the nodes by [connecting to the host](node-access) and verifying configuration changes have been made on the filesystem.

**3. Troubleshoot workload failures**.

When SeccompDefault is enabled, the container runtime default seccomp profile is used by default for all workloads scheduled on the node. This might cause workloads to fail due to blocked syscalls. If a workload failure has occurred, you might see errors such as:

- Workload is existing unexpectedly after the feature is enabled, with "permission denied" error.
- Seccomp error messages can also be seen in auditd or syslog by replacing SCMP_ACT_ERRNO with SCMP_ACT_LOG in the default profile.

If you experience the above errors, we recommend that you change your seccomp profile to `Unconfined`

. `Unconfined`

places no restrictions on syscalls, allowing all system calls, which reduces security.

### Configure a custom seccomp profile

With a custom seccomp profile, you can have more granular control over restricted syscalls. Align to the best practice of granting the container minimal permission only to run by:

- Defining with filters what actions to allow or deny.
- Annotating within a pod YAML manifest to associate with the seccomp filter.

To see seccomp in action, create a filter that prevents changing permissions on a file.

[SSH](manage-ssh-node-access)to an AKS node.Create a seccomp filter named

*/var/lib/kubelet/seccomp/prevent-chmod*.Copy and paste the following content:

`{ "defaultAction": "SCMP_ACT_ALLOW", "syscalls": [ { "name": "chmod", "action": "SCMP_ACT_ERRNO" }, { "name": "fchmodat", "action": "SCMP_ACT_ERRNO" }, { "name": "chmodat", "action": "SCMP_ACT_ERRNO" } ] }`

In version 1.19 and later, you need to configure:

`{ "defaultAction": "SCMP_ACT_ALLOW", "syscalls": [ { "names": ["chmod","fchmodat","chmodat"], "action": "SCMP_ACT_ERRNO" } ] }`

From your local machine, create a pod manifest named

*aks-seccomp.yaml*and paste the following content. This manifest:- Defines an annotation for
`seccomp.security.alpha.kubernetes.io`

. - References the
*prevent-chmod*filter created in the previous step.

`apiVersion: v1 kind: Pod metadata: name: chmod-prevented annotations: seccomp.security.alpha.kubernetes.io/pod: localhost/prevent-chmod spec: containers: - name: chmod image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: - "chmod" args: - "777" - /etc/hostname restartPolicy: Never`

In version 1.19 and later, you need to configure:

`apiVersion: v1 kind: Pod metadata: name: chmod-prevented spec: securityContext: seccompProfile: type: Localhost localhostProfile: prevent-chmod containers: - name: chmod image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: - "chmod" args: - "777" - /etc/hostname restartPolicy: Never`

- Defines an annotation for
Deploy the sample pod using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f ./aks-seccomp.yaml`

View pod status using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.- The pod reports an error.
- The
`chmod`

command is prevented from running by the seccomp filter, as shown in the example output:

`kubectl get pods NAME READY STATUS RESTARTS AGE chmod-prevented 0/1 Error 0 7s`


For help troubleshooting your seccomp profile see the article [Troubleshoot seccomp profile configuration in Azure Kubernetes Service](/en-us/troubleshoot/azure/azure-kubernetes/security/troubleshoot-seccomp-profiles).

## Seccomp security profile options

Seccomp security profiles are a set of defined syscalls that are allowed or restricted. Most container runtimes have a default seccomp profile that is similar if not the same as the one Docker uses. For more information about available profiles, see [Docker](https://kubernetes.io/docs/reference/node/seccomp/) or [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) default seccomp profiles.

AKS uses the [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) default seccomp profile for our RuntimeDefault when you configure seccomp using [custom node configuration](/en-us/azure/aks/custom-node-configuration).

### Significant syscalls blocked by default profile

Both [Docker](https://kubernetes.io/docs/reference/node/seccomp/) and [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) maintain allowlists of safe syscalls. This table lists the significant (but not all) syscalls that are effectively blocked because they aren't on the allowlist. If any of the blocked syscalls are required by your workload, don't use the `RuntimeDefault`

seccomp profile.

When changes are made to [Docker](https://kubernetes.io/docs/reference/node/seccomp/) and [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51), AKS updates their default configuration to match. Updates to this list may cause workload failure. For release updates, see [AKS release notes](https://github.com/Azure/AKS/releases).

| Blocked syscall | Description |
|---|---|
`acct` |
Accounting syscall which could let containers disable their own resource limits or process accounting. Also gated by `CAP_SYS_PACCT` . |
`add_key` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`bpf` |
Deny loading potentially persistent bpf programs into kernel, already gated by `CAP_SYS_ADMIN` . |
`clock_adjtime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`clock_settime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`clone` |
Deny cloning new namespaces. Also gated by `CAP_SYS_ADMIN for CLONE_*` flags, except `CLONE_NEWUSER` . |
`create_module` |
Deny manipulation and functions on kernel modules. Obsolete. Also gated by `CAP_SYS_MODULE` . |
`delete_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`finit_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`get_kernel_syms` |
Deny retrieval of exported kernel and module symbols. Obsolete. |
`get_mempolicy` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`init_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`ioperm` |
Prevent containers from modifying kernel I/O privilege levels. Already gated by `CAP_SYS_RAWIO` . |
`iopl` |
Prevent containers from modifying kernel I/O privilege levels. Already gated by `CAP_SYS_RAWIO` . |
`kcmp` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`kexec_file_load` |
Sister syscall of kexec_load that does the same thing, slightly different arguments. Also gated by `CAP_SYS_BOOT` . |
`kexec_load` |
Deny loading a new kernel for later execution. Also gated by `CAP_SYS_BOOT` . |
`keyctl` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`lookup_dcookie` |
Tracing/profiling syscall, which could leak information on the host. Also gated by `CAP_SYS_ADMIN` . |
`mbind` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`mount` |
Deny mounting, already gated by `CAP_SYS_ADMIN` . |
`move_pages` |
Syscall that modifies kernel memory and NUMA settings. |
`nfsservctl` |
Deny interaction with the kernel nfs daemon. Obsolete since Linux 3.1. |
`open_by_handle_at` |
Cause of an old container breakout. Also gated by `CAP_DAC_READ_SEARCH` . |
`perf_event_open` |
Tracing/profiling syscall, which could leak information on the host. |
`personality` |
Prevent container from enabling BSD emulation. Not inherently dangerous, but poorly tested, potential for kernel vulns. |
`pivot_root` |
Deny pivot_root, should be privileged operation. |
`process_vm_readv` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`process_vm_writev` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`ptrace` |
Tracing/profiling syscall. Blocked in Linux kernel versions before 4.8 to avoid seccomp bypass. Tracing/profiling arbitrary processes is already blocked by dropping CAP_SYS_PTRACE, because it could leak information on the host. |
`query_module` |
Deny manipulation and functions on kernel modules. Obsolete. |
`quotactl` |
Quota syscall which could let containers disable their own resource limits or process accounting. Also gated by `CAP_SYS_ADMIN` . |
`reboot` |
Don't let containers reboot the host. Also gated by `CAP_SYS_BOOT` . |
`request_key` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`set_mempolicy` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`setns` |
Deny associating a thread with a namespace. Also gated by `CAP_SYS_ADMIN` . |
`settimeofday` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`stime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`swapon` |
Deny start/stop swapping to file/device. Also gated by `CAP_SYS_ADMIN` . |
`swapoff` |
Deny start/stop swapping to file/device. Also gated by `CAP_SYS_ADMIN` . |
`sysfs` |
Obsolete syscall. |
`_sysctl` |
Obsolete, replaced by /proc/sys. |
`umount` |
Should be a privileged operation. Also gated by `CAP_SYS_ADMIN` . |
`umount2` |
Should be a privileged operation. Also gated by `CAP_SYS_ADMIN` . |
`unshare` |
Deny cloning new namespaces for processes. Also gated by `CAP_SYS_ADMIN` , with the exception of unshare --user. |
`uselib` |
Older syscall related to shared libraries, unused for a long time. |
`userfaultfd` |
Userspace page fault handling, largely needed for process migration. |
`ustat` |
Obsolete syscall. |
`vm86` |
In kernel x86 real mode virtual machine. Also gated by `CAP_SYS_ADMIN` . |
`vm86old` |
In kernel x86 real mode virtual machine. Also gated by `CAP_SYS_ADMIN` . |

## Next steps

For associated best practices, see [Best practices for cluster security and upgrades in AKS](operator-best-practices-cluster-security) and [Best practices for pod security in AKS](developer-best-practices-pod-security).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/faq -->

# AKS frequently asked questions

This article provides answers to some of the most common questions about Azure Kubernetes Service (AKS).

## Support

### Does AKS offer a service-level agreement?

AKS provides service-level agreement (SLA) guarantees in the [Standard pricing tier with the Uptime SLA feature](free-standard-pricing-tiers).

### What is platform support, and what does it include?

Platform support is a reduced support plan for unsupported n-3 version clusters. Platform support includes only Azure infrastructure support.

For more information, see the [platform support policy](supported-kubernetes-versions).

### Does AKS automatically upgrade my unsupported clusters?

Yes, AKS initiates auto-upgrades for unsupported clusters. When a cluster in an n-3 version (where *n* is the latest supported AKS minor version that's generally available) is about to drop to n-4, AKS automatically upgrades the cluster to n-2 to remain in an AKS support policy.

For more information, see [Supported Kubernetes versions](supported-kubernetes-versions), [Planned maintenance windows](planned-maintenance), and [Automatic upgrades](auto-upgrade-cluster).

### Can I apply Azure reservation discounts to my AKS agent nodes?

AKS agent nodes are billed as standard Azure virtual machines (VMs). If you purchased [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations) for the VM size that you're using in AKS, those discounts are automatically applied.

## Operations

### Can I run Windows Server containers on AKS?

Yes, AKS supports Windows Server containers. For more information, see the [Windows Server on AKS FAQ](windows-faq).

### What Linux operating systems (OS) are supported on AKS?

AKS supports four main Linux operating systems, including Ubuntu Linux, [Azure Linux](use-azure-linux), [Azure Linux OS Guard](use-azure-linux-os-guard), and [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks). When specifying `--os-type Linux`

during node pool creation or cluster creation, the default OS is Ubuntu Linux.

### What operating systems (OS) versions are supported on AKS?

When using `--os-sku Ubuntu`

, AKS defaults to Ubuntu 22.04 in Kubernetes versions 1.25-1.34. AKS defaults to Ubuntu 24.04 in Kubernetes versions 1.35+.
When using `--os-sku AzureLinux`

, AKS defaults to Azure Linux 3.0 in Kubernetes versions 1.32+.
In some scenarios, like FIPS-enabled node pools, the default OS version might differ. See [node images](node-images) for more information.

### Can I move or migrate my cluster between Azure tenants?

No. Moving your AKS cluster between tenants is currently unsupported.

### Can I move or migrate my cluster between subscriptions?

No. Moving your AKS cluster between subscriptions is currently unsupported.

### Can I move my AKS cluster or AKS infrastructure resources to other resource groups or rename them?

No. Moving or renaming your AKS cluster and its associated resources isn't supported.

### Can I restore my cluster after I delete it?

No. You can't restore your cluster after you delete it. When you delete your cluster, the node resource group and all its resources are also deleted.

If you want to keep any of your resources, move them to another resource group before you delete your cluster. If you want to protect against accidental deletes, you can lock the AKS managed resource group that's hosting your cluster resources by using [Node resource group lockdown](node-resource-group-lockdown).

### Can I scale my AKS cluster to zero?

You can completely [stop a running AKS cluster](start-stop-cluster) or [scale or autoscale all or specific User node pools](scale-cluster#scale-user-node-pools-to-0) to zero.

You can't directly scale [system node pools](use-system-pools) to zero.

### Can I use the virtual machine scale set APIs to scale manually?

No. Scale operations that use the virtual machine scale set APIs aren't supported. You can use the AKS APIs (`az aks scale`

).

### Can I use virtual machine scale sets to manually scale to zero nodes?

No. Scale operations that use the virtual machine scale set APIs aren't supported. You can use the AKS API to scale nonsystem node pools to zero or [stop your cluster](start-stop-cluster) instead.

### Can I stop or deallocate all my VMs?

No. This configuration isn't supported. [Stop your cluster](start-stop-cluster) instead.

### Why are two resource groups created with AKS?

AKS builds upon many Azure infrastructure resources, including virtual machine scale sets, virtual networks, and managed disks. These integrations enable you to apply many of the core capabilities of the Azure platform within the managed Kubernetes environment provided by AKS. For example, you can use most Azure VM types directly with AKS, and you can use Azure Reservations to receive discounts on those resources automatically.

To enable this architecture, each AKS deployment spans two resource groups:

- You create the first resource group. This group contains only the Kubernetes service resource. The AKS resource provider automatically creates the second resource group during deployment. An example of the second resource group is
*MC_myResourceGroup_myAKSCluster_eastus*. For information on how to specify the name of this second resource group, see the next section. - The second resource group, known as the
*node resource group*, contains all of the infrastructure resources associated with the cluster. These resources include the Kubernetes node VMs, virtual networking, and storage. By default, the node resource group has a name like*MC_myResourceGroup_myAKSCluster_eastus*. AKS automatically deletes the node resource group whenever you delete the cluster. Use this resource group only for resources that share the cluster's lifecycle.

Note

Modifying any resource under the node resource group in the AKS cluster is an unsupported action and will cause cluster operation failures. You can prevent changes from being made to the node resource group. [Block users from modifying resources](node-resource-group-lockdown) that the AKS cluster manages.

### Can I provide my own name for the AKS node resource group?

By default, AKS names the node resource group *MC_resourcegroupname_clustername_location*, but you can provide your own name.

To specify your own resource group name, install the [aks-preview](/en-us/cli/azure/aks) Azure CLI extension version *0.3.2* or later. When you create an AKS cluster by using the `az aks create`

command, use the `--node-resource-group`

parameter and specify a name for the resource group. If you use an [Azure Resource Manager template](/en-us/azure/templates/microsoft.containerservice/2022-09-01/managedclusters) to deploy an AKS cluster, you can define the resource group name by using the `nodeResourceGroup`

property.

- The Azure resource provider automatically creates the secondary resource group.
- You can specify a custom resource group name only when you create the cluster.

As you work with the node resource group, you can't:

- Specify an existing resource group for the node resource group.
- Specify a different subscription for the node resource group.
- Change the node resource group name after you create the cluster.
- Specify names for the managed resources within the node resource group.
- Modify or delete Azure-created tags of managed resources within the node resource group.

### Can I modify tags and other properties of the AKS resources in the node resource group?

You might get unexpected scaling and upgrading errors if you modify or delete Azure-created tags and other resource properties in the node resource group. AKS allows you to create and modify custom tags created by end users, and you can add those tags when you [create a node pool](manage-node-pools#specify-a-taint-label-or-tag-for-a-node-pool). You might want to create or modify custom tags, for example, to assign a business unit or cost center. Another option is to apply policies and modify tags through the AKS resource itself—specifically via the cluster and node pools..

Azure-created tags are created for their respective Azure services, and you should always allow them. For AKS, there are the `aks-managed`

and `k8s-azure`

tags. Modifying any *Azure-created tags* on resources under the node resource group in the AKS cluster is an unsupported action, which breaks the service-level objective (SLO).

Note

In the past, the tag name `Owner`

was reserved for AKS to manage the public IP that's assigned on the front-end IP of the load balancer. Now, services use the `aks-managed`

prefix. For legacy resources, don't use Azure policies to apply the `Owner`

tag name. Otherwise, all resources on your AKS cluster deployment and update operations will break. This restriction doesn't apply to newly created resources.

### Why do I see aks-managed prefixed Helm releases on my cluster, and why does their revision count keep increasing?

AKS uses Helm to deliver components to your cluster. You can safely ignore `aks-managed`

prefixed Helm releases. Continuously increasing revisions on these Helm releases are expected and safe.

## Quotas, limits, and region availability

### Which Azure regions currently provide AKS?

For a complete list of available regions, see [AKS regions and availability](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

### Can I spread an AKS cluster across regions?

No. AKS clusters are regional resources and can't span regions. For guidance on how to create an architecture that includes multiple regions, see [best practices for business continuity and disaster recovery](operator-best-practices-multi-region#plan-for-multiregion-deployment).

### Can I spread an AKS cluster across availability zones?

Yes, you can deploy an AKS cluster across one or more [availability zones](availability-zones) in [regions that support them](/en-us/azure/reliability/availability-zones-region-support).

### Can I have different VM sizes in a single cluster?

Yes, you can use different VM sizes in your AKS cluster by creating [multiple node pools](create-node-pools).

### What's the size limit on a container image in AKS?

AKS doesn't set a limit on the container image size. But the larger the image, the higher the memory demand. A larger size could potentially exceed resource limits or the overall available memory of worker nodes. By default, memory for VM size Standard_DS2_v2 for an AKS cluster is set to 7 GiB.

When a container image is excessively large, as in the terabyte (TB) range, the kubelet might not be able to pull it from your container registry to a node because of the lack of disk space.

For Windows Server nodes, Windows Update doesn't automatically run and apply the latest updates. You should perform an upgrade on the cluster and the Windows Server node pools in your AKS cluster. Follow a regular schedule based on the Windows Update release cycle and your own validation process. This upgrade process creates nodes that run the latest Windows Server image and patches, and then removes the older nodes. For more information on this process, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

### Are AKS images required to run as root?

The following images have functional requirements to run as root, and exceptions must be filed for any policies:

*mcr.microsoft.com/oss/kubernetes/coredns**mcr.microsoft.com/azuremonitor/containerinsights/ciprod**mcr.microsoft.com/oss/calico/node**mcr.microsoft.com/oss/kubernetes-csi/azuredisk-csi*

## Security, access, and identity

### Can I limit who has access to the Kubernetes API server?

Yes, there are two options for limiting access to the API server:

- Use
[API server authorized IP ranges](api-server-authorized-ip-ranges)if you want to maintain a public endpoint for the API server but restrict access to a set of trusted IP ranges. - Use a
[private cluster](private-clusters)if you want to limit the API server to be accessible*only*from within your virtual network.

### Are security updates applied to AKS agent nodes?

AKS patches CVEs that have a *vendor fix* every week. CVEs without a fix are waiting on a vendor fix before they can be remediated. The AKS images are automatically updated within 30 days. We recommend that you apply an updated node image on a regular cadence to ensure that the latest patched images and OS patches are all applied and current. You can do this task:

- Manually, through the Azure portal or the Azure CLI.
- By upgrading your AKS cluster. The cluster upgrades
[cordon and drain nodes](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)automatically. Then it brings a new node online with the latest Ubuntu image and a new patch version or a minor Kubernetes version. For more information, see[Upgrade an AKS cluster](upgrade-cluster). - By using a
[node image upgrade](node-image-upgrade).

### Are there security threats that target AKS that I should be aware of?

Microsoft provides guidance for other actions that you can take to secure your workloads through services like [Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction?tabs=defender-for-container-arch-aks). For information on a security threat related to AKS and Kubernetes, see [New large-scale campaign targets Kubeflow](https://techcommunity.microsoft.com/t5/azure-security-center/new-large-scale-campaign-targets-kubeflow/ba-p/2425750) (June 8, 2021).

### Does AKS store any customer data outside the cluster's region?

No. All data is stored in the cluster's region.

### How can I avoid permission ownership setting slow issues when the volume has numerous files?

Traditionally, if your pod is running as a nonroot user (which it should), you must specify an `fsGroup`

parameter inside the pod's security context so that the volume is readable and writable by the pod. For more information on this requirement, see [Configure a security context for a pod or container](https://kubernetes.io/docs/tasks/configure-pod-container/security-context/).

A side effect of setting `fsGroup`

is that each time a volume is mounted, Kubernetes must use the `chown()`

and `chmod()`

commands recursively for all the files and directories inside the volume (with a few exceptions). This scenario happens even if group ownership of the volume already matches the requested `fsGroup`

parameter. This configuration might be expensive for larger volumes with lots of small files, which can cause pod startup to take a long time. This scenario was a known problem before v1.20. The workaround is to set the pod to run as root:

```
apiVersion: v1
kind: Pod
metadata:
name: security-context-demo
spec:
securityContext:
runAsUser: 0
fsGroup: 0
```


The issue was resolved with Kubernetes version 1.20. For more information, see [Kubernetes 1.20: Granular control of volume permission changes](https://kubernetes.io/blog/2020/12/14/kubernetes-release-1.20-fsgroupchangepolicy-fsgrouppolicy/).

## Networking

### How does the managed control plane communicate with my nodes?

AKS uses a secure tunnel communication to allow the `api-server`

and individual node kubelets to communicate, even on separate virtual networks. The tunnel is secured through mutual Transport Layer Security encryption. The current main tunnel that AKS uses is [Konnectivity, previously known as apiserver-network-proxy](https://kubernetes.io/docs/tasks/extend-kubernetes/setup-konnectivity/). Verify that all network rules follow the [Azure required network rules and fully qualified domain names (FQDNs)](limit-egress-traffic).

### Can my pods use the API server FQDN instead of the cluster IP?

Yes, you can add the annotation `kubernetes.azure.com/set-kube-service-host-fqdn`

to pods to set the `KUBERNETES_SERVICE_HOST`

variable to the domain name of the API server instead of the in-cluster service IP. This modification is useful in cases where your cluster egress is done via a layer 7 firewall. An example is when you use Azure Firewall with application rules.

### Can I configure NSGs with AKS?

AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. AKS modifies only the network interface NSG settings. If you're using Container Network Interface (CNI), you also must ensure that the security rules in the NSGs allow traffic between the node and pod classless interdomain routing (CIDR) ranges. If you're using kubenet, you must also ensure that the security rules in the NSGs allow traffic between the node and pod CIDR. For more information, see [Network security groups](concepts-network#network-security-groups).

### How does time synchronization work in AKS?

AKS nodes run the chrony service, which pulls time from the local host. Containers that run on pods get the time from the AKS nodes. Applications that open inside a container use time from the container of the pod.

## Add-ons, extensions, and integrations

### Can I use custom VM extensions?

No. AKS is a managed service. Manipulation of the infrastructure as a service (IaaS) resources isn't supported. To install custom components, use the Kubernetes APIs and mechanisms. For example, use DaemonSets to install any required components.

### What Kubernetes admission controllers does AKS support? Can admission controllers be added or removed?

AKS supports the following [admission controllers](https://kubernetes.io/docs/reference/access-authn-authz/admission-controllers/):

`NamespaceLifecycle`

`LimitRanger`

`ServiceAccount`

`DefaultIngressClass`

`DefaultStorageClass`

`DefaultTolerationSeconds`

`MutatingAdmissionWebhook`

`ValidatingAdmissionWebhook`

`ResourceQuota`

`PodNodeSelector`

`PodTolerationRestriction`

`ExtendedResourceToleration`


Currently, you can't modify the list of admission controllers in AKS.

### Can I use admission controller webhooks on AKS?

Yes, you can use admission controller webhooks on AKS. We recommend that you exclude internal AKS namespaces, which are marked with the `control-plane`

label. For example:

```
namespaceSelector:
matchExpressions:
- key: control-plane
operator: DoesNotExist
```


AKS firewalls the API server egress so that your admission controller webhooks need to be accessible from within the cluster.

### Can admission controller webhooks affect kube-system and internal AKS namespaces?

To protect the stability of the system and prevent custom admission controllers from affecting internal services in the `kube-system`

namespace, AKS has an admissions enforcer, which automatically excludes `kube-system`

and AKS internal namespaces. This service ensures that the custom admission controllers don't affect the services that run in `kube-system`

.

If you have a critical use case for deploying something on `kube-system`

(not recommended) in support of your custom admission webhook, you can add the following label or annotation so that the admissions enforcer ignores it:

- Label:
`"admissions.enforcer/disabled": "true"`

- Annotation:
`"admissions.enforcer/disabled": true`


### Is Azure Key Vault integrated with AKS?

[Azure Key Vault provider for Secrets Store CSI Driver](csi-secrets-store-driver) provides native integration of Azure Key Vault into AKS.

### Can I use FIPS cryptographic libraries with deployments on AKS?

Nodes that are enabled with Federal Information Processing Standards (FIPS) are now supported on Linux-based node pools. For more information, see [Add a FIPS-enabled node pool](enable-fips-nodes).

### How are AKS add-ons updated?

Any patch, including a security patch, is automatically applied to the AKS cluster. Anything bigger than a patch, like major or minor version changes (which can have breaking changes to your deployed objects), are updated when you update your cluster if a new release is available. For information on when a new release is available, see [AKS release notes](https://github.com/Azure/AKS/releases).

### What is the purpose of the AKS Linux extension that I see installed on my Linux virtual machine scale sets instances?

The AKS Linux extension is an Azure VM extension that installs and configures monitoring tools on Kubernetes worker nodes. The extension is installed on all new and existing Linux nodes. It configures the following monitoring tools:

[Node-exporter](https://github.com/prometheus/node_exporter): Collects hardware telemetry from the VM and makes it available by using a metrics endpoint. Then, a monitoring tool, such as Prometheus, can scrap these metrics.[Node-problem-detector](https://github.com/kubernetes/node-problem-detector): Aims to make various node problems visible to upstream layers in the cluster management stack. It's a systemd unit that runs on each node, detects node problems, and reports them to the cluster's API server by using`Events`

and`NodeConditions`

.[ig](https://go.microsoft.com/fwlink/p/?linkid=2260320): Is an eBPF-powered open-source framework for debugging and observing Linux and Kubernetes systems. It provides a set of tools (or gadgets) that gather relevant information that users can use to identify the cause of performance issues, crashes, or other anomalies. Notably, its independence from Kubernetes enables users to employ it also for debugging control plane issues.

These tools help provide observability around many node health-related problems, such as:

**Infrastructure daemon issues:**NTP service down**Hardware issues:**Bad CPU, memory, or disk**Kernel issues:**Kernel deadlock, corrupted file system**Container runtime issues:**Unresponsive runtime daemon

The extension *doesn't require extra outbound access* to any URLs, IP addresses, or ports beyond the [documented AKS egress requirements](limit-egress-traffic). It doesn't require any special permissions granted in Azure. It uses `kubeconfig`

to connect to the API server to send the monitoring data that's collected.

## Troubleshoot cluster issues

### Why is it taking so long to delete my cluster?

Most clusters are deleted upon user request. In some cases, especially cases where you bring your own resource group or perform cross-resource group tasks, deletion can take more time or even fail. If you have an issue with deletions, double-check that you don't have locks on the resource group. Also make sure that any resources outside the resource group are disassociated from the resource group.

### Why is it taking so long to create or update my cluster?

If you have issues with creating and updating clusters, make sure that you don't have any assigned policies or service constraints that might block your AKS cluster from managing resources like VMs, load balancers, or tags.

### If I have pods or deployments in NodeLost or Unknown states, can I still upgrade my cluster?

You can, but we don't recommend it. Perform updates when the state of the cluster is known and healthy.

### If I have a cluster with one or more nodes in an Unhealthy state, or if it's shut down, can I perform an upgrade?

No. Delete or remove any nodes that are in a failed state or otherwise from the cluster before you upgrade.

### I tried to delete my cluster, but I see the error "[Errno 11001] getaddrinfo failed."

Most commonly, this error arises if you have one or more NSGs in use that are still associated with the cluster. Remove them and attempt to delete the cluster again.

### I ran an upgrade, but now my pods are in crash loops and readiness probes fail.

Confirm that your service principal isn't expired. For more information, see [AKS service principal](kubernetes-service-principal) and [AKS update credentials](update-credentials).

### My cluster was working, but suddenly I can't provision load balancers or mount persistent volume claims.

Confirm that your service principal isn't expired. For more information, see [AKS service principal](kubernetes-service-principal) and [AKS update credentials](update-credentials).

## Retirements and deprecations

### Which Linux OS versions are deprecated on AKS?

Ubuntu 16.04 and Ubuntu 18.04 are no longer supported on AKS.
Starting on 17 March 2027, AKS will no longer support Ubuntu 20.04. For more information on this retirement, see [Retirement: Ubuntu 20.04 node pools on AKS](https://github.com/Azure/AKS/issues/4874).

### Which Windows OS versions are deprecated on AKS?

Starting on 1 March 2026, AKS will no longer support Windows Server 2019 node pools. Kubernetes versions 1.33+ can't use Windows Server 2019. For more information on this retirement, see [Retirement: Windows Server 2019 node pools on AKS](https://github.com/Azure/AKS/issues/4091).
Starting on 15 March 2027, AKS will no longer support Windows Server 2022 node pools. Kubernetes versions 1.36+ can't use Windows Server 2022. For more information on this retirement, see [Retirement: Windows Server 2022 node pools on AKS](https://github.com/Azure/AKS/issues/4168).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quotas-skus-regions -->

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

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-scale -->

# Scaling options for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When running applications in Azure Kubernetes Service (AKS), you might need to actively increase or decrease the amount of compute resources in your cluster. As you change the number of application instances you have, you might need to change the number of underlying Kubernetes nodes. You might also need to provision a large number of other application instances.

This article introduces core AKS application scaling concepts, including [manually scaling pods or nodes](#manually-scale-pods-or-nodes), using the [Horizontal pod autoscaler](#horizontal-pod-autoscaler), using the [Cluster autoscaler](#cluster-autoscaler), and integrating with [Azure Container Instances (ACI)](#burst-to-azure-container-instances-aci).

## Manually scale pods or nodes

You can manually scale replicas, or pods, and nodes to test how your application responds to a change in available resources and state. Manually scaling resources lets you define a set amount of resources to use, such as the number of nodes, to maintain a fixed cost. To manually scale, you define a replica or node count. The Kubernetes API then schedules the creation of more pods or the draining of nodes based on that replica or node count.

When you scale down nodes, the Kubernetes API calls the relevant Azure Compute API tied to the compute type used by your cluster. For example, for clusters built on Virtual Machine Scale Sets, the Virtual Machine Scale Sets API determines which nodes to remove. To learn more about how nodes are selected for removal on scale down, see the [Virtual Machine Scale Sets FAQ](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-faq#if-i-reduce-my-scale-set-capacity-from-20-to-15--which-vms-are-removed-).

To get started with manually scaling nodes, see [manually scale nodes in an AKS cluster](scale-cluster). To manually scale the number of pods, see [kubectl scale command](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/).

## Horizontal pod autoscaler

Kubernetes uses the horizontal pod autoscaler (HPA) to monitor the resource demand and automatically scale the number of pods. By default, the HPA checks the Metrics API every 15 seconds for any required changes in replica count, while the Metrics API retrieves data from the Kubelet every 60 seconds. As a result, HPA is updated every 60 seconds. When changes are required, the number of replicas is scaled accordingly. HPA works with AKS clusters that have deployed Metrics Server for Kubernetes version 1.8 and higher.

When you configure the HPA for a given deployment, you define the minimum and maximum number of replicas that can run. You also define the metric to monitor and base scaling decisions on, such as CPU usage.

To get started with the horizontal pod autoscaler in AKS, see [Autoscale pods in AKS](tutorial-kubernetes-scale#autoscale-pods).

### Cooldown of scaling events

As the HPA is effectively updated every 60 seconds, previous scale events might not have successfully completed before another check is made. This behavior could cause the HPA to change the number of replicas before the previous scale event could receive application workload and the resource demands to adjust accordingly.

To minimize race events, a delay value is set. This value defines how long the HPA must wait after a scale event before another scale event can be triggered. This behavior allows the new replica count to take effect and the Metrics API to reflect the distributed workload. There's [no delay for scale-up events as of Kubernetes 1.12](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/#support-for-cooldown-delay). However, the default delay on scale down events is *5 minutes*.

## Cluster autoscaler

To respond to changing pod demands, the Kubernetes cluster autoscaler adjusts the number of nodes based on the requested compute resources in the node pool. By default, the cluster autoscaler checks the Metrics API server every 10 seconds for any required changes in node count. If the cluster autoscaler determines that a change is required, the number of nodes in your AKS cluster is increased or decreased accordingly. The cluster autoscaler works with Kubernetes RBAC-enabled AKS clusters that run Kubernetes 1.10.x or higher.

The cluster autoscaler is typically used alongside the [horizontal pod autoscaler](#horizontal-pod-autoscaler). When combined, the horizontal pod autoscaler increases or decreases the number of pods based on application demand, and the cluster autoscaler adjusts the number of nodes to run more pods.

To get started with the cluster autoscaler in AKS, see [Cluster autoscaler on AKS](cluster-autoscaler).

### Scale out events

If a node doesn't have sufficient compute resources to run a requested pod, that pod can't progress through the scheduling process. The pod can't start unless more compute resources are made available within the node pool.

When the cluster autoscaler notices pods that can't be scheduled because of node pool resource constraints, the number of nodes within the node pool is increased to provide extra compute resources. When the nodes are successfully deployed and available for use within the node pool, the pods are then scheduled to run on them.

If your application needs to scale rapidly, some pods might remain in a state of waiting to be scheduled until more nodes deployed by the cluster autoscaler can accept the scheduled pods. For applications that have high burst demands, you can scale with virtual nodes and [Azure Container Instances](#burst-to-azure-container-instances-aci).

### Scale in events

The cluster autoscaler also monitors the pod scheduling status for nodes that haven't recently received new scheduling requests. This scenario indicates the node pool has more compute resources than required, and the number of nodes can be decreased. By default, nodes that pass a threshold of no longer being needed for 10 minutes are scheduled for deletion. When this situation occurs, pods are scheduled to run on other nodes within the node pool, and the cluster autoscaler decreases the number of nodes.

Your applications might experience some disruption as pods are scheduled on different nodes when the cluster autoscaler decreases the number of nodes. To minimize disruption, avoid applications that use a single pod instance.

## Kubernetes Event-driven Autoscaling (KEDA)

[Kubernetes Event-driven Autoscaling](https://keda.sh/docs/2.13/concepts/) (KEDA) is an open source component for event-driven autoscaling of workloads. It scales workloads dynamically based on the number of events received. KEDA extends Kubernetes with a custom resource definition (CRD), referred to as a *ScaledObject*, to describe how applications should be scaled in response to specific traffic.

KEDA scaling is useful in scenarios where workloads receive bursts of traffic or handle high volumes of data. KEDA differs from the Horizontal Pod Autoscaler as KEDA is event-driven and scales based on the number of events, while HPA is metrics-driven based on the resource utilization (for example, CPU and memory).

To get started with the KEDA add-on in AKS, see [KEDA overview](keda-about).

## Node Autoprovisioning

[Node autoprovisioning (preview)](node-autoprovision) (NAP), uses the open source Karpenter project that automatically deploys, configures, and manages [Karpenter](https://karpenter.sh/) on your AKS cluster. NAP dynamically provisions nodes based on pending pod resource requirements; it'll automatically select the optimal virtual machine (VM) SKU and quantity to meet real-time demand.

NAP takes a predefined list of VM SKUs as the starting point to decide which SKU is best suited for pending workloads. For more precise control, users can define the upper limits of resources used by a node pool and preferences of where workloads should be scheduled if there are multiple node pools.

## Control Plane Scaling and Safeguards

Kubernetes has a multi-dimensional scale envelope with each resource type representing a dimension. Not all resources are alike. For example, watches are commonly set on secrets, which result in list calls to the kube-apiserver that add cost and a disproportionately higher load on the control plane compared to resources without watches.

The control plane manages all the resource scaling in the cluster, so the more you scale the cluster within a given dimension, the less you can scale within other dimensions. For example, running hundreds of thousands of pods in an AKS cluster impacts how much pod churn rate (pod mutations per second) the control plane can support. Refer to ** best practices**.

AKS automatically scales control plane components based on key signals such as the total number of cores in the cluster and CPU or memory pressure on the control plane components.

To verify whether the control plane has scaled up, check the ConfigMap named 'large-cluster-control-plane-scaling-status'

```
kubectl describe configmap large-cluster-control-plane-scaling-status -n kube-system
```


### Control Plane Safeguards

If scaling the API server automatically does not stabilize it under high load scenarios, AKS deploys a managed API server guard. This guard acts as a last-resort mechanism to protect the API server by throttling non-system client requests and preventing the control plane from becoming completely unresponsive. System-critical calls to API server from components such as kubelet will continue to function normally.

To verify whether the managed API server guard has been applied, check for the presence of **"aks-managed-apiserver-guard"** FlowSchema and PriorityLevelConfiguration.

```
kubectl get flowschemas
kubectl get prioritylevelconfigurations
```


Refer to [API server and Etcd Troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd#cause-4-aks-managed-api-server-guard-was-applied) if the **"aks-managed-apiserver-guard"** FlowSchema and PriorityLevelConfiguration have been applied on the cluster for quick mitigation.

## Burst to Azure Container Instances (ACI)

To rapidly scale your AKS cluster, you can integrate with Azure Container Instances (ACI). Kubernetes has built-in components to scale the replica and node count. However, if your application needs to rapidly scale, the [horizontal pod autoscaler](#horizontal-pod-autoscaler) might schedule more pods than what the existing compute resources in the node pool can support. If configured, this scenario would then trigger the [cluster autoscaler](#cluster-autoscaler) to deploy more nodes in the node pool, but it might take a few minutes for those nodes to successfully provision and allow the Kubernetes scheduler to run pods on them.

ACI lets you quickly deploy container instances without extra infrastructure overhead. When you connect with AKS, ACI becomes a secured, logical extension of your AKS cluster. The [virtual nodes](virtual-nodes-cli) component, which is based on [virtual Kubelet](https://virtual-kubelet.io/), is installed in your AKS cluster that presents ACI as a virtual Kubernetes node. Kubernetes can then schedule pods that run as ACI instances through virtual nodes, not as pods on VM nodes directly in your AKS cluster.

Your application requires no modifications to use virtual nodes. Your deployments can scale across AKS and ACI and with no delay as the cluster autoscaler deploys new nodes in your AKS cluster.

Virtual nodes are deployed to another subnet in the same virtual network as your AKS cluster. This virtual network configuration secures the traffic between ACI and AKS. Like an AKS cluster, an ACI instance is a secure, logical compute resource isolated from other users.

## Next steps

To get started with scaling applications, see the following resources:

- Manually scale
[pods](https://kubernetes.io/docs/reference/kubectl/generated/kubectl_scale/)or[nodes](scale-cluster) - Use the
[horizontal pod autoscaler](tutorial-kubernetes-scale#autoscale-pods) - Use the
[cluster autoscaler](cluster-autoscaler) - Use the
[Kubernetes Event-driven Autoscaling (KEDA) add-on](keda-about)

For more information on core Kubernetes and AKS concepts, see the following articles:

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___dapr-workflow_use-capacity-reservation-groups_concepts-vulnerability-manageme_af223d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __dapr-workflow_use-capacity-reservation-groups_concepts-vulnerability-managemen_9df1f2.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _dapr-workflow_use-capacity-reservation-groups.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: dapr-workflow.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/dapr-workflow -->

# Deploy and run workflows with the Dapr extension for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Dapr Workflow, you can easily orchestrate messaging, state management, and failure-handling logic across various microservices. Dapr Workflow can help you create long-running, fault-tolerant, and stateful applications.

In this guide, you use the [provided order processing workflow example](https://github.com/Azure-Samples/dapr-workflows-aks-sample) to:

- Create an Azure Container Registry and an AKS cluster for this sample.
- Install the Dapr extension on your AKS cluster.
- Deploy the sample application to AKS.
- Start and query workflow instances using HTTP API calls.

The workflow example is an ASP.NET Core project with:

- A
that contains the setup of the app, including the registration of the workflow and workflow activities.`Program.cs`

file - Workflow definitions found in the
.`Workflows`

directory - Workflow activity definitions found in the
.`Activities`

directory

## Prerequisites

- An
[Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)with Owner or Admin role. [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)- The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli) - The latest version of
[Dapr](https://docs.dapr.io/getting-started/install-dapr-cli/) - Latest
[Docker](https://docs.docker.com/get-docker/) - Latest
[Helm](https://helm.sh/docs/intro/install/)

## Set up the environment

### Clone the sample project

Clone the example workflow application.

```
git clone https://github.com/Azure-Samples/dapr-workflows-aks-sample.git
```


Navigate to the sample's root directory.

```
cd dapr-workflows-aks-sample
```


### Create a Kubernetes cluster

Create a resource group to hold the AKS cluster.

```
az group create --name myResourceGroup --location eastus
```


Create an AKS cluster.

```
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --generate-ssh-keys
```


[Make sure kubectl is installed and pointed to your AKS cluster.](tutorial-kubernetes-deploy-cluster#connect-to-cluster-using-kubectl) If you use the Azure Cloud Shell,

`kubectl`

is already installed.For more information, see the [Deploy an AKS cluster](tutorial-kubernetes-deploy-cluster) tutorial.

## Deploy the application to AKS

### Install Dapr on your AKS cluster

Install the Dapr extension on your AKS cluster. Before you start, make sure you have:

[Installed or updated the](dapr#add-the-azure-cli-extension-for-cluster-extensions).`k8s-extension`

[Registered the](dapr#register-the-kubernetesconfiguration-resource-provider)`Microsoft.KubernetesConfiguration`

service provider

```
az k8s-extension create --cluster-type managedClusters --cluster-name myAKSCluster --resource-group myResourceGroup --name dapr --extension-type Microsoft.Dapr
```


After a few minutes, you'll see output showing the Dapr connection to your AKS cluster. Next, initialize Dapr on your cluster.

```
dapr init -k
```


Verify Dapr is installed:

```
kubectl get pods -A
```


### Deploy the Redis Actor state store component

Navigate to the `Deploy`

directory in your forked version of the sample:

```
cd Deploy
```


Deploy the Redis component:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install redis bitnami/redis
kubectl apply -f redis.yaml
```


### Run the application

Once Redis is deployed, deploy the application to AKS:

```
kubectl apply -f deployment.yaml
```


Expose the Dapr sidecar and the sample app:

```
kubectl apply -f service.yaml
export APP_URL=$(kubectl get svc/workflows-sample -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export DAPR_URL=$(kubectl get svc/workflows-sample-dapr -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
```


Verify that the above commands were exported:

```
echo $APP_URL
echo $DAPR_URL
```


## Start the workflow

Now that the application and Dapr are deployed to the AKS cluster, you can now start and query workflow instances. Restock items in the inventory using the following API call to the sample app:

```
curl -X GET $APP_URL/stock/restock
```


Start the workflow:

```
curl -i -X POST $DAPR_URL/v1.0/workflows/dapr/OrderProcessingWorkflow/start \
-H "Content-Type: application/json" \
-H "dapr-app-id: dwf-app" \
-d '{"Name": "Paperclips", "TotalCost": 99.95, "Quantity": 1}'
```


Expected output includes an auto-generated instance ID:

```
HTTP/1.1 202 Accepted
Content-Type: application/json
Traceparent: 00-00000000000000000000000000000000-0000000000000000-00
Date: Tue, 23 Apr 2024 15:35:00 GMT
Content-Length: 21
{"instanceID":"<generated-id>"}
```


Check the workflow status:

```
curl -i -X GET $DAPR_URL/v1.0/workflows/dapr/OrderProcessingWorkflow/<instance-id> \
-H "dapr-app-id: dwf-app"
```


Expected output:

```
HTTP/1.1 200 OK
Content-Type: application/json
Traceparent: 00-00000000000000000000000000000000-0000000000000000-00
Date: Tue, 23 Apr 2024 15:51:02 GMT
Content-Length: 580
```


Monitor the application logs:

```
kubectl logs -l run=workflows-sample -c workflows-sample --tail=20
```


Expected output:

```
{
"instanceID":"1234",
"workflowName":"OrderProcessingWorkflow",
"createdAt":"2024-04-23T15:35:00.156714334Z",
"lastUpdatedAt":"2024-04-23T15:35:00.176459055Z",
"runtimeStatus":"COMPLETED",
"dapr.workflow.input":"{ \"input\" : {\"Name\": \"Paperclips\", \"TotalCost\": 99.95, \"Quantity\": 1}}",
"dapr.workflow.output":"{\"Processed\":true}"
}
```


Notice that the workflow status is marked as completed.


---

<!-- DOCUMENTO FUSIONADO: use-capacity-reservation-groups.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-capacity-reservation-groups -->

# Assign capacity reservation groups to Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your workload demands change, you can associate existing [capacity reservation groups (CRGs)](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set) to your Azure Kubernetes Service (AKS) node pools to guarantee allocated capacity for them. Capacity reservation groups allow you to reserve compute capacity in an Azure region or availability zone for any duration of time. This feature is useful for workloads that require guaranteed capacity, such as those with predictable traffic patterns or those that need to meet specific performance requirements.

In this article, you learn how to use capacity reservation groups with node pools in AKS.

Note

Deleting a node pool implicitly dissociates that node pool from any associated capacity reservation group before the node pool is deleted. Deleting a cluster implicitly dissociates all node pools in that cluster from their associated capacity reservation groups.

## Prerequisites for using capacity reservation groups with AKS node pools

- You need the Azure CLI version 2.56 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need an existing
[capacity reservation group](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set)with at least one capacity reservation. If not, the node pool is added to the cluster with a warning and no capacity reservation group gets associated. - You need to
[create a user-assigned managed identity with the](#create-a-user-assigned-managed-identity-and-assign-it-to-an-aks-cluster)for the resource group that contains the capacity reservation group and assign the identity to your AKS cluster. System-assigned managed identities don't work for this feature.`Contributor`

role

### Create a user-assigned managed identity and assign it to an AKS cluster

Create a user-assigned managed identity using the

command.`az identity create`

`az identity create --name <identity-name> --resource-group <resource-group-name> --location <location>`

Get the ID of the user-assigned managed identity using the

command and set it to an environment variable.`az identity show`

`IDENTITY_ID=$(az identity show --name <identity-name> --resource-group <resource-group-name> --query identity.id -o tsv)`

Assign the

`Contributor`

role to the user-assigned identity using thecommand.`az role assignment create`

`az role assignment create --assignee $IDENTITY_ID --role "Contributor" --scope /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>`

It can take up to

*60 minutes*for the role assignment to propagate.Assign the user-assigned managed identity to a new or existing AKS cluster using the

`--assign-identity`

flag with theor`az aks create`

command.`az aks update`

`# Create a new AKS cluster with the user-assigned managed identity az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --generate-ssh-keys # Update an existing AKS cluster to use the user-assigned managed identity az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> \ --node-count <node-count> \ --enable-managed-identity \ --assign-identity $IDENTITY_ID`


## Limitations for using capacity reservation groups with AKS node pools

You can't update an existing node pool with a capacity reservation group. Instead, you need to create a new node pool with the `--crg-id`

flag to associate it with the capacity reservation group. You can also associate an existing capacity reservation group with a system node pool during cluster creation.

## Get the ID of an existing capacity reservation group

Get the ID of an existing capacity reservation group using the

command and set it to an environment variable.`az capacity reservation group show`

`CRG_ID=$(az capacity reservation group show --capacity-reservation-group <crg-name> --resource-group <resource-group-name> --query id -o tsv)`


## Associate an existing capacity reservation group with a node pool

Associate an existing capacity reservation group with a node pool using the

command with the`az aks nodepool add`

`--crg-id`

flag. The following example assumes you have a CRG named "myCRG".`az aks nodepool add --resource-group <resource-group-name> --cluster-name <cluster-name> --name <node-pool-name> --crg-id $CRG_ID`


## Associate an existing capacity reservation group with a system node pool

To associate an existing capacity reservation group with a system node pool, you need to assign the user-assigned managed identity with the `Contributor`

role to the cluster during cluster creation. You can then use the `--crg-id`

flag to associate the capacity reservation group with the system node pool.

Create a new AKS cluster with the user-assigned managed identity and associate it with the capacity reservation group using the

`--assign-identity`

and`--crg-id`

flags with thecommand.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --crg-id $CRG_ID \ --generate-ssh-keys`


## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).


---

<!-- DOCUMENTO FUSIONADO: concepts-vulnerability-management.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-vulnerability-management -->

# Vulnerability management for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Vulnerability management involves detecting, assessing, mitigating, and reporting on any security vulnerabilities that exist in an organization's systems and software. Vulnerability management is a shared responsibility between you and Microsoft.

This article describes how Microsoft manages security vulnerabilities and security updates (also referred to as patches), for Azure Kubernetes Service (AKS) clusters.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## How vulnerabilities are discovered

Microsoft identifies and patches vulnerabilities and missing security updates for the following components:

AKS Container Images

Ubuntu operating system 18.04 and 22.04 worker nodes: Canonical provides Microsoft with OS builds that have all available security updates applied.

Windows Server 2022 OS worker nodes: The Windows Server operating system is patched on the second Tuesday of every month. SLAs should be the same as per their support contract and severity.

Azure Linux OS Nodes: Azure Linux provides AKS with OS builds that have all available security updates applied.


## AKS Container Images

While the [Cloud Native Computing Foundation](https://www.cncf.io/) (CNCF) owns and maintains most of the code AKS runs, Microsoft takes responsibility for building the open-source packages we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, as well as control over the binaries in container images. Having responsibility for building the open-source packages deployed on AKS enables us to establish a software supply chain over the binary, and to patch the software as needed.

Microsoft is active in the broader Kubernetes ecosystem to help build the future of cloud-native compute in the wider CNCF community. This work not only ensures the quality of every Kubernetes release for the world, but also enables AKS quickly get new Kubernetes releases out into production for several years. In some cases, ahead of other cloud providers by several months. Microsoft collaborates with other industry partners in the Kubernetes security organization. For example, the Security Response Committee (SRC) receives, prioritizes, and patches embargoed security vulnerabilities before they're announced to the public. This commitment ensures Kubernetes is secure for everyone, and enables AKS to patch and respond to vulnerabilities faster to keep our customers safe. In addition to Kubernetes, Microsoft has signed up to receive pre-release notifications for software vulnerabilities for products such as Envoy, container runtimes, and many other open-source projects.

Microsoft scans container images using static analysis to discover vulnerabilities and missing updates in Kubernetes and Microsoft-managed containers. If fixes are available, the scanner automatically begins the update and release process.

In addition to automated scanning, Microsoft discovers and updates vulnerabilities unknown to scanners in the following ways:

Microsoft performs its own audits, penetration testing, and vulnerability discovery across all AKS platforms. Specialized teams inside Microsoft and trusted third-party security vendors conduct their own attack research.

Microsoft actively engages with the security research community through multiple vulnerability reward programs. A dedicated

[Microsoft Azure Bounty program](https://www.microsoft.com/msrc/bounty-microsoft-azure)provides significant bounties for the best cloud vulnerability found each year.Microsoft collaborates with other industry and open source software partners who share vulnerabilities, security research, and updates before the public release of the vulnerability. The goal of this collaboration is to update large pieces of Internet infrastructure before the vulnerability is announced to the public. In some cases, Microsoft contributes vulnerabilities found to this community.

Microsoft's security collaboration happens on many levels. Sometimes it occurs formally through programs where organizations sign up to receive pre-release notifications about software vulnerabilities for products such as Kubernetes and Docker. Collaboration also happens informally due to our engagement with many open source projects such as the Linux kernel, container runtimes, virtualization technology, and others.


## Worker Nodes

### Linux nodes

The nightly canonical OS security updates are turned off by default in AKS. In order to enable them explicitly, use the `unmanaged`

[channel](node-image-upgrade).

If you are using the `unmanaged`

[channel](node-image-upgrade), then nightly canonical security updates are applied to the OS on the node. The node image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node receives all the security and kernel updates available during the automatic assessment performed every night, but remains unpatched until all checks and restarts are complete. You can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

For AKS clusters using a [channel](node-image-upgrade) other than `unmanaged`

, the unattended upgrade process is disabled.

### Windows Server nodes

For Windows Server nodes, Windows Update doesn't automatically run and apply the latest updates. Schedule Windows Server node pool upgrades in your AKS cluster around the regular Windows Update release cycle and your own update management process. This upgrade process creates nodes that run the latest Windows Server image and patches, then removes the older nodes. For more information on this process, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

## How vulnerabilities are classified

Microsoft makes large investments in security hardening the entire stack, including the OS, container, Kubernetes, and network layers, in addition to setting good defaults and providing security-hardened configurations and managed components. Combined, these efforts help to reduce the impact and likelihood of vulnerabilities.

The AKS team classifies vulnerabilities according to the Kubernetes vulnerability scoring system. Classifications consider many factors including AKS configuration and security hardening. As a result of this approach, and the investments AKS make in security, AKS vulnerability classifications might differ from other classification sources.

The following table describes vulnerability severity categories:

| Severity | Description |
|---|---|
| Critical | A vulnerability easily exploitable in all clusters by an unauthenticated remote attacker that leads to full system compromise. |
| High | A vulnerability easily exploitable for many clusters that leads to loss of confidentiality, integrity, or availability. |
| Medium | A vulnerability exploitable for some clusters where loss of confidentiality, integrity, or availability is limited by common configurations, difficulty of the exploit itself, required access, or user interaction. |
| Low | All other vulnerabilities. Exploitation is unlikely or consequences of exploitation are limited. |

## How vulnerabilities are updated

AKS patches Common Vulnerabilities and Exposures (CVEs) that have a *vendor fix* every week. Any CVEs without a fix are waiting on a vendor fix before they can be remediated. The fixed container images are cached in the next corresponding virtual hard disk (VHD) build, which also contains the updated Ubuntu/Azure Linux/Windows patched CVEs. As long as you're running the updated VHD, you shouldn't be running any container image CVEs with a vendor fix that is over 30 days old.

For the OS-based vulnerabilities in the VHD, AKS also relies on node image vhd updates by default, so any security updates will come with weekly node image releases. Unattended upgrades is disabled unless you switch to unmanaged which is not recommended as its release is global.

## Update release timelines

Microsoft's goal is to mitigate detected vulnerabilities within a time period appropriate for the risks they represent. The [Microsoft Azure FedRAMP High](/en-us/azure/azure-government/compliance/azure-services-in-fedramp-auditscope#azure-government-services-by-audit-scope) Provisional Authorization to Operate (P-ATO) includes AKS in audit scope and has been authorized. FedRAMP Continuous Monitoring Strategy Guide and the FedRAMP Low, Moderate, and High Security Control baselines requires remediation of known vulnerabilities within a specific time period according to their severity level. As specified in FedRAMP RA-5d.

## How vulnerabilities and updates are communicated

In general, Microsoft doesn't broadly communicate the release of new patch versions for AKS. However, Microsoft constantly monitors and validates available CVE patches to support them in AKS in a timely manner. If a critical patch is found or user action is required, Microsoft [posts and updates CVE issue details on GitHub](https://github.com/Azure/AKS/issues?q=is%3Aissue+is%3Aopen+cve).

## Security Reporting

You can report a security issue to the Microsoft Security Response Center (MSRC), by [creating a vulnerability report](https://aka.ms/opensource/security/create-report).

If you prefer to submit a report without logging in to the tool, send email to [secure@microsoft.com](mailto:secure@microsoft.com). If possible, encrypt your message with our PGP key by downloading it from the [Microsoft Security Response Center PGP Key page](https://aka.ms/opensource/security/pgpkey).

You should receive a response within 24 hours. If for some reason you don't, follow up with an email to ensure we received your original message. For more information, go to the [Microsoft Security Response Center](https://aka.ms/opensource/security/msrc).

Include the following requested information (as much as you can provide) to help us better understand the nature and scope of the possible issue:

- Type of issue (for example, buffer overflow, SQL injection, cross-site scripting, etc.)
- Full paths of source file(s) related to the manifestation of the issue
- The location of the affected source code (tag/branch/commit or direct URL)
- Any special configuration required to reproduce the issue
- Step-by-step instructions to reproduce the issue
- Proof-of-concept or exploit code (if possible)
- Impact of the issue, including how an attacker might exploit the issue

This information helps us triage your reported security issue quicker.

If you're reporting for a bug bounty, more complete reports can contribute to a higher bounty award. For more information about our active programs, see [Microsoft Bug Bounty Program](https://aka.ms/opensource/security/bounty).

### Policy

Microsoft follows the principle of [Coordinated Vulnerability Disclosure](https://aka.ms/opensource/security/cvd).

## Next steps

See the overview about [Upgrading Azure Kubernetes Service clusters and node pools](upgrade).


---

<!-- DOCUMENTO FUSIONADO: _use-windows-gpu__deploy-marketplace_quickstart-event-grid.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-windows-gpu.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-windows-gpu -->

# Use Windows GPUs for compute-intensive workloads on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Graphical processing units (GPUs) are often used for compute-intensive workloads, such as graphics and visualization workloads. AKS supports GPU-enabled Windows and [Linux](gpu-cluster) node pools to run compute-intensive Kubernetes workloads.

This article helps you provision Windows nodes with schedulable GPUs on new and existing AKS clusters (preview).

## Supported GPU-enabled virtual machines (VMs)

To view supported GPU-enabled VMs, see [GPU-optimized VM sizes in Azure](/en-us/azure/virtual-machines/sizes-gpu). For AKS node pools, we recommend a minimum size of *Standard_NC6s_v3*. The NVv4 series (based on AMD GPUs) aren't supported on AKS.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

## Limitations

- Updating an existing Windows node pool to add GPU isn't supported.
- Not supported on Kubernetes version 1.28 and below.

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-windows-container-deploy-cli),[Azure PowerShell](learn/quick-windows-container-deploy-powershell), or the[Azure portal](learn/quick-windows-container-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed and configured to use the
`--gpu-driver`

field with the`az aks nodepool add`

command. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you have the
`aks-preview`

Azure CLI extension installed, please update the version to 18.0.0b2 or later.

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command. The following example command gets the credentials for the`az aks get-credentials`

*myAKSCluster*in the*myResourceGroup*resource group:`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Using Windows GPU with automatic driver installation

Using NVIDIA GPUs involves the installation of various NVIDIA software components such as the [DirectX device plugin for Kubernetes](https://github.com/aarnaud/k8s-directx-device-plugin), GPU driver installation, and more. When you create a Windows node pool with a supported GPU-enabled VM, these components and the appropriate NVIDIA CUDA or GRID drivers are installed. For NC and ND series VM sizes, the CUDA driver is installed. For NV series VM sizes, the GRID driver is installed.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `WindowsGPUPreview`

feature flag

Register the

`WindowsGPUPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "WindowsGPUPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "WindowsGPUPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a Windows GPU-enabled node pool (preview)

To create a Windows GPU-enabled node pool, you need to use a supported GPU-enabled VM size and specify the `os-type`

as `Windows`

. The default Windows `os-sku`

is `Windows2022`

, but all Windows `os-sku`

options are supported.

Create a Windows GPU-enabled node pool using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type Windows \ --kubernetes-version 1.29.0 \ --node-vm-size Standard_NC6s_v3`

Check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable).Once you confirm that your GPUs are schedulable, you can run your GPU workload.


#### Specify GPU Driver Type (preview)

By default, AKS specifies a default GPU driver type for each supported GPU-enabled VM. Because workload and driver compatibility are important for functioning GPU workloads, you can specify the driver type for your Windows GPU node. This feature is not supported for Linux GPU node pools.

When creating a Windows agent pool with GPU support, you have the option to specify the type of GPU driver using the `--driver-type`

flag.

The available options are:

- GRID: For applications requiring virtualization support.
- CUDA: Optimized for computational tasks in scientific computing and data-intensive applications.

Note

When you set the `--driver-type`

flag, you assume responsibility for ensuring that the selected driver type is compatible with the specific VM size and configuration of your node pool. While AKS attempts to validate compatibility, there are scenarios where the node pool creation might fail due to incompatibilities between the specified driver type and the underlying VM or hardware.

To create a Windows GPU-enabled node pool with a specific GPU Driver type, use the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name gpunp \
--node-count 1 \
--os-type Windows \
--kubernetes-version 1.29.0 \
--node-vm-size Standard_NC6s_v3 \
--driver-type GRID
```


For example, the above command creates a GPU-enabled node pool using the `GRID`

GPU driver type. Selecting this driver type overrides the default of `CUDA`

driver type for NC series VM skus.

## Using Windows GPU with manual driver installation

When creating a Windows node pool with N-series (NVIDIA GPU) VM sizes in AKS, the GPU driver and Kubernetes DirectX device plugin are installed automatically. To bypass this automatic installation, use the following steps:

[Skip GPU driver installation](#skip-gpu-driver-installation)by setting the configuration`--gpu-driver none`

at node pool create time.[Manual installation of the Kubernetes DirectX device plugin](#manually-install-the-kubernetes-directx-device-plugin).

### Skip GPU driver installation

AKS has automatic GPU driver installation enabled by default. In some cases, such as installing your own drivers, you may want to skip GPU driver installation.

Note

The `gpu-driver`

API field is a suggested alternative for customers previously using the `--skip-gpu-driver-install`

node pool tag.

- The
`--skip-gpu-driver-install`

node pool tag on AKS will be retired on 14 August 2025. To retain the existing behavior of skipping automatic GPU driver installation, upgrade your node pools to the latest node image version and set the`--gpu-driver`

field to`none`

. After 14 August 2025, you won't be able to provision AKS GPU-enabled node pools with the`--skip-gpu-driver-install`

node pool tag to bypass this default behavior. For more information, see.`skip-gpu-driver`

tag retirement

Create a node pool using the

command and setting the API field`az aks nodepool add`

`--gpu-driver`

to`none`

to skip automatic GPU driver installation.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type windows \ --os-sku windows2022 \ --gpu-driver none`


Note

If the `--node-vm-size`

that you're using isn't yet onboarded on AKS, you can't use GPUs and the `--gpu-driver`

field doesn't work.

### Manually install the Kubernetes DirectX device plugin

You can deploy a DaemonSet for the Kubernetes DirectX device plugin, which runs a pod on each node to provide the required drivers for the GPUs.

Add a node pool to your cluster using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \ --node-count 1 \ --os-type windows \ --os-sku windows2022`


## Create a namespace and deploy the Kubernetes DirectX device plugin

Create a namespace using the

command.`kubectl create namespace`

`kubectl create namespace gpu-resources`

Create a file named

*k8s-directx-device-plugin.yaml*and paste the following YAML manifest provided as part of the[NVIDIA device plugin for Kubernetes project](https://github.com/NVIDIA/k8s-device-plugin):`apiVersion: apps/v1 kind: DaemonSet metadata: name: nvidia-device-plugin-daemonset namespace: gpu-resources spec: selector: matchLabels: name: nvidia-device-plugin-ds updateStrategy: type: RollingUpdate template: metadata: # Mark this pod as a critical add-on; when enabled, the critical add-on scheduler # reserves resources for critical add-on pods so that they can be rescheduled after # a failure. This annotation works in tandem with the toleration below. annotations: scheduler.alpha.kubernetes.io/critical-pod: "" labels: name: nvidia-device-plugin-ds spec: tolerations: # Allow this pod to be rescheduled while the node is in "critical add-ons only" mode. # This, along with the annotation above marks this pod as a critical add-on. - key: CriticalAddonsOnly operator: Exists - key: nvidia.com/gpu operator: Exists effect: NoSchedule - key: "sku" operator: "Equal" value: "gpu" effect: "NoSchedule" containers: - image: mcr.microsoft.com/aks/aks-windows-gpu-device-plugin:0.0.17 name: nvidia-device-plugin-ctr securityContext: allowPrivilegeEscalation: false capabilities: drop: ["ALL"] volumeMounts: - name: device-plugin mountPath: /var/lib/kubelet/device-plugins volumes: - name: device-plugin hostPath: path: /var/lib/kubelet/device-plugins`

Create the DaemonSet and confirm the NVIDIA device plugin is created successfully using the

command.`kubectl apply`

`kubectl apply -f nvidia-device-plugin-ds.yaml`

Now that you successfully installed the NVIDIA device plugin, you can check that your

[GPUs are schedulable](#confirm-that-gpus-are-schedulable).

## Confirm that GPUs are schedulable

After creating your cluster, confirm that GPUs are schedulable in Kubernetes.

List the nodes in your cluster using the

command.`kubectl get nodes`

`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-gpunp-28993262-0 Ready agent 13m v1.20.7`

Confirm the GPUs are schedulable using the

command.`kubectl describe node`

`kubectl describe node aks-gpunp-28993262-0`

Under the

*Capacity*section, the GPU should list as`microsoft.com/directx: 1`

. Your output should look similar to the following condensed example output:`Capacity: [...] microsoft.com.directx/gpu: 1 [...]`


## Clean up resources

Remove the associated Kubernetes objects you created in this article using the

command.`kubectl delete job`

`kubectl delete jobs windows-gpu-workload`


## Next steps

- To run Apache Spark jobs, see
[Run Apache Spark jobs on AKS](spark-job). - For more information on features of the Kubernetes scheduler, see
[Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler). - For more information on Azure Kubernetes Service and Azure Machine Learning, see:


---

<!-- DOCUMENTO FUSIONADO: _deploy-marketplace_quickstart-event-grid.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: deploy-marketplace.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/deploy-marketplace -->

# Deploy and manage a Kubernetes application from Azure Marketplace

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy and manage a Kubernetes application from Azure Marketplace.

[Azure Marketplace](/en-us/marketplace/azure-marketplace-overview) is an online store that contains thousands of IT software applications and services built by industry-leading technology companies. In Azure Marketplace, you can find, try, buy, and deploy the software and services that you need to build new solutions and manage your cloud infrastructure. The catalog includes solutions for different industries and technical areas, free trials, and consulting services from Microsoft partners.

## Limitations

- This feature is currently supported only in the following regions:
- Australia East, Australia Southeast, Brazil South, Canada Central, Canada East, Central India, Central US, East Asia, East US, East US 2, East US 2 EAUP, France Central, France South, Germany North, Germany West Central, Japan East, Japan West, Jio India West, Korea Central, Korea South, North Central Us, North Europe, Norway East, Norway West, South Africa North, South Central US, South India, Southeast Asia, Sweden Central, Switzerland North, UAE North, UK South, UK West, West Central US, West Europe, West US, West US 2, West US 3

- You can't deploy Kubernetes application-based container offers on AKS for Azure Stack HCI or AKS Edge Essentials.

## Select and deploy a Kubernetes application

### From an AKS cluster

In the Azure portal, navigate to your AKS cluster resource.

From the service menu, under

**Settings**, select**Extensions + applications**>**Add**.You can search for an offer or publisher directly by name, or you can browse all offers. To view Kubernetes application offers, select

**Containers**under**Categories**.After you decide on an application, select the offer. The following example uses the

**TrilioVault for Kubernetes - BYOL**offer.Select

**Plans + Pricing**to ensure the terms are acceptable, and then select**Create**.Follow each page in the application creation process, filling in information for your resource group, your cluster, and any configuration options that the application requires. You can decide to deploy on a new AKS cluster or use an existing cluster.

Once you've filled in all the required information, select

**Review + create**>**Create**.It might take a few minutes for the application to deploy. You can monitor the deployment status from the

**Extensions + applications**page.

### Search in the Azure portal

From the Azure portal home page, search for and select

**Marketplace**.You can search for an offer or publisher directly by name, or you can browse all offers. To find Kubernetes application offers, on the left side under

**Categories**select**Containers**.After you decide on an application, select the offer. The following example uses the

**TrilioVault for Kubernetes - BYOL**offer.Select

**Plans + Pricing**to ensure the terms are acceptable, and then select**Create**.Follow each page in the application creation process, filling in information for your resource group, your cluster, and any configuration options that the application requires. You can decide to deploy on a new AKS cluster or use an existing cluster.

Once you've filled in all the required information, select

**Review + create**>**Create**.It might take a few minutes for the application to deploy. You can monitor the deployment status from the

**Extensions + applications**page.

## Verify the deployment

- Navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Verify that the extension is listed and the
*Provisioning State*shows**Succeeded**.

## Manage the offer lifecycle

For lifecycle management, a Kubernetes offer is represented as a cluster extension for AKS. For more information, see [Cluster extensions for AKS](cluster-extensions). Purchasing an offer from Azure Marketplace creates a new instance of the extension on your AKS cluster.

- In the Azure portal, navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Select an extension name to navigate to a properties view where you're able to disable autoupgrades, check the provisioning state, delete the extension instance, or modify configuration settings as needed.

## Monitor billing and usage information

- In the Azure portal, navigate to your cluster's resource group.
- From the service menu, under
**Cost Management**, select**Cost analysis**. Under**Product**, you can see a cost breakdown for the plan that you selected.

## Remove an offer

You can delete a purchased plan for an Azure container offer by deleting the extension instance on the cluster.

- Navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Select an application, then select
**Uninstall**.

## Troubleshooting

If you experience issues, see the [troubleshooting checklist for failed deployments of a Kubernetes offer](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-failed-kubernetes-deployment-offer).

## Next steps

- Learn more about
[exploring and analyzing costs](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis). - Learn more about
[deploying a Kubernetes application programmatically using Azure CLI](/en-us/azure/aks/deploy-application-az-cli). - Learn more about
[deploying a Kubernetes application using an ARM template](/en-us/azure/aks/deploy-application-template).


---

<!-- DOCUMENTO FUSIONADO: quickstart-event-grid.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/quickstart-event-grid -->

# Quickstart: Subscribe to Azure Kubernetes Service (AKS) events with Azure Event Grid

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Event Grid is a fully managed event routing service that provides uniform event consumption using a publish-subscribe model.

In this quickstart, you create an AKS cluster and subscribe to AKS events.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.

Note

AKS operations are independent of Azure Event Grid availability and aren't impacted during Event Grid [Service Outages](https://azure.status.microsoft/status).

## Create an AKS cluster

Create an AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a resource group *MyResourceGroup* and a cluster named *MyAKS* with one node in the *MyResourceGroup* resource group:

```
az group create --name MyResourceGroup --location eastus
az aks create --resource-group yResourceGroup --name MyAKS --location eastus --node-count 1 --generate-ssh-keys
```


## Subscribe to AKS events

Create a namespace and event hub using [az eventhubs namespace create](/en-us/cli/azure/eventhubs/namespace#az-eventhubs-namespace-create) and [az eventhubs eventhub create](/en-us/cli/azure/eventhubs/eventhub#az-eventhubs-eventhub-create). The following example creates a namespace *MyNamespace* and an event hub *MyEventGridHub* in *MyNamespace*, both in the *MyResourceGroup* resource group.

```
az eventhubs namespace create --location eastus --name MyNamespace --resource-group MyResourceGroup
az eventhubs eventhub create --name MyEventGridHub --namespace-name MyNamespace --resource-group MyResourceGroup
```


Note

The *name* of your namespace must be unique.

Subscribe to the AKS events using [az eventgrid event-subscription create](/en-us/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create):

```
SOURCE_RESOURCE_ID=$(az aks show --resource-group MyResourceGroup --name MyAKS --query id --output tsv)
ENDPOINT=$(az eventhubs eventhub show --resource-group MyResourceGroup --name MyEventGridHub --namespace-name MyNamespace --query id --output tsv)
az eventgrid event-subscription create --name MyEventGridSubscription \
--source-resource-id $SOURCE_RESOURCE_ID \
--endpoint-type eventhub \
--endpoint $ENDPOINT
```


Verify your subscription to AKS events using `az eventgrid event-subscription list`

:

```
az eventgrid event-subscription list --source-resource-id $SOURCE_RESOURCE_ID
```


The following example output shows you're subscribed to events from the *MyAKS* cluster and those events are delivered to the *MyEventGridHub* event hub:

```
[
{
"deadLetterDestination": null,
"deadLetterWithResourceIdentity": null,
"deliveryWithResourceIdentity": null,
"destination": {
"deliveryAttributeMappings": null,
"endpointType": "EventHub",
"resourceId": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/Microsoft.EventHub/namespaces/MyNamespace/eventhubs/MyEventGridHub"
},
"eventDeliverySchema": "EventGridSchema",
"expirationTimeUtc": null,
"filter": {
"advancedFilters": null,
"enableAdvancedFilteringOnArrays": null,
"includedEventTypes": [
"Microsoft.ContainerService.NewKubernetesVersionAvailable","Microsoft.ContainerService.ClusterSupportEnded","Microsoft.ContainerService.ClusterSupportEnding","Microsoft.ContainerService.NodePoolRollingFailed","Microsoft.ContainerService.NodePoolRollingStarted","Microsoft.ContainerService.NodePoolRollingSucceeded"
],
"isSubjectCaseSensitive": null,
"subjectBeginsWith": "",
"subjectEndsWith": ""
},
"id": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/Microsoft.ContainerService/managedClusters/MyAKS/providers/Microsoft.EventGrid/eventSubscriptions/MyEventGridSubscription",
"labels": null,
"name": "MyEventGridSubscription",
"provisioningState": "Succeeded",
"resourceGroup": "MyResourceGroup",
"retryPolicy": {
"eventTimeToLiveInMinutes": 1440,
"maxDeliveryAttempts": 30
},
"systemData": null,
"topic": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/microsoft.containerservice/managedclusters/MyAKS",
"type": "Microsoft.EventGrid/eventSubscriptions"
}
]
```


When AKS events occur, you see those events appear in your event hub. For example, when the list of available Kubernetes versions for your clusters changes, you see a `Microsoft.ContainerService.NewKubernetesVersionAvailable`

event. There are also new events available now for upgrades and cluster within support. For more information on the events AKS emits, see [Azure Kubernetes Service (AKS) as an Event Grid source](/en-us/azure/event-grid/event-schema-aks).

## Delete the cluster and subscriptions

Use the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, the AKS cluster, namespace, and event hub, and all related resources.

```
az group delete --name MyResourceGroup --yes --no-wait
```


Note

When you delete the cluster, the Microsoft Entra service principal used by the AKS cluster isn't removed. For steps on how to remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal).

If you used a managed identity, the identity is managed by the platform and doesn't require removal.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then subscribed to AKS events in Azure Event Hubs.

To learn more about AKS, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.


---

<!-- DOCUMENTO FUSIONADO: _secure-container-access__upgrade-aks-node-pools-rolling_auto-upgrade-node-image.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: secure-container-access.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/secure-container-access -->

# Security container access to resources using built-in Linux security features

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to secure container access to resources for your Azure Kubernetes Service (AKS) workloads.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview

In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access.

You can use built-in Kubernetes *pod security contexts* to define more permissions, such as the user or group to run as, the Linux capabilities to expose, or setting `allowPrivilegeEscalation: false`

in the pod manifest. For more best practices, see [Secure pod access to resources](https://kubernetes.io/docs/concepts/security/pod-security-standards/).

To improve the host isolation and decrease lateral movement on Linux, you can use *user-namespaces*.

For even more granular control of container actions, you can use built-in Linux security features such as *AppArmor* and *seccomp*.

- Define Linux security features at the node level.
- Implement features through a pod manifest.

Built-in Linux security features are only available on Linux nodes and pods.

Note

Currently, Kubernetes environments aren't completely safe for hostile multitenant usage. Additional security features, like *Microsoft Defender for Containers*, *AppArmor*, *seccomp*, *user-namespaces*, *Pod Security Admission*, or *Kubernetes RBAC for nodes*, efficiently block exploits.

For true security when running hostile multitenant workloads, only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster, not an individual node.

For these types of hostile multitenant workloads, you should use physically isolated clusters.

## User-namespaces

Linux pods run using several namespaces by default: a network namespaces to isolate the network identity and a PID namespace to isolate the processes. A [user-namespace](https://man7.org/linux/man-pages/man7/user_namespaces.7.html) isolates the users inside the container from the users on the host. It also limits the scope of capabilities and the pod's interactions with the rest of the system.

The UIDs and GIDs inside the container are mapped to unprivileged users on the host, so all interaction with the rest of the host happen as those unprivileged UID and GID. For example, root inside the container (UID 0) can be mapped to user 65536 on the host. Kubernetes creates the mapping to guarantee it doesn't overlap with other pods using user-namespaces on the system.

The Kubernetes implementation has some key benefits:

**Increased host isolation**: If a container escapes the pod boundaries, even if it runs as root inside the container, it has no privileges on the host. The reason is because the UIDs and GIDs of the container are mapped to unprivileged users on the host. If there's a container escape, user-namespaces greatly protects what files on the host a container can read/write, which process it can send signals to. Capabilities granted are only valid inside the user namespace and not on the host.**Prevention of lateral movement**: As the UIDs and GIDs for different containers are mapped to different, nonoverlapping UIDs and GIDs on the host, containers have a harder time attacking each other. For example, suppose container A runs with different UIDs and GIDs on the host than container B. In case of a container breakout, the operations it can do on container B's files and processes are limited: only read/write what a file allows to others. But not even that ends up being possible, as there's an extra prevention on the parent directory of the pod root volume to make sure only the pod GID can access it.**Honor Least-privilege principle**: As the UIDs and GIDs are mapped to unprivileged users on the host, only users that need the privilege on the host (and disable user namespaces) get it. Without user namespaces, there's no separation between container's users and host's users. We can't avoid giving privileges on the host to processes that don't need it, when they need privilege just inside the container.**Enablement of new use cases**: User namespaces allow containers to gain certain capabilities inside their own user namespace without affecting the host. The capabilities granted restricted to the pod unlocks new possibilities, such as running applications that require privileged operations without granting full root access on the host. Common new use-cases that can be implemented securely are: running nested containers and unprivileged container builds.**Unprivileged container setup**: Most of the container creation and setup doesn't run as root on the host, which significantly limits the impact of many CVEs.

None of these things are true when user-namespaces aren't used. If the container runs as root, when user-namespaces aren't used, the process is running as root on the host, the capabilities are valid on the host and the container setup is done as root on the host.

### Before you begin

Before you begin, make sure you have the following:

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Minimum kubernetes version 1.33 for the control plane and worker nodes. If you're not using kubernetes version 1.33 or higher, you'll need to
[upgrade your kubernetes version](upgrade-aks-cluster). - Worker nodes running Azure Linux 3.0 or Ubuntu 24.04. If you're not using these OS versions, you will not have the minimum
[stack requirements](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/#before-you-begin)to enable user-namespaces. You'll need to[upgrade your OS version](upgrade-os-version).

### Limitations

- User-namespaces is a linux kernel feature and is not supported for Windows node pools.
- Don't hesitate to check the
[Kubernetes documentation for user namespaces](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/), in particular the limitations section.

### Enable user-namespaces

There are no configurations needed to use this feature. If using the required AKS version, everything works out of the box.

Create a file named

`mypod.yaml`

and copy in the following manifest:To use user-namespaces, the yaml needs to have the field

`hostUsers: false`

.`apiVersion: v1 kind: Pod metadata: name: userns spec: hostUsers: false containers: - name: shell command: ["sleep", "infinity"] image: debian`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f mypod.yaml`

Check the status of the deployed pods using the

`kubectl get pods`

command.`kubectl get pods`

Exec into the pod to check

`/proc/self/uid_map`

by using the`kubectl exec`

command:`kubectl exec -ti userns -- bash # Now inside the pod run cat /proc/self/uid_map`


The output should have 65536 in the last column. For example:

```
0 833617920 65536
```


### CVEs mitigated

Here are some CVEs that are completely/partially mitigated with user-namespaces.

Bear in mind the list isn't exhaustive, it's just a selection of CVEs with high score that are mitigated:

[CVE-2019-5736](https://nvd.nist.gov/vuln/detail/CVE-2019-5736)- Score 8.6 (HIGH)[CVE 2024-21262](https://github.com/opencontainers/runc/security/advisories/GHSA-xr7r-f8xq-vfvv): Score 8.6 (HIGH)[CVE 2022-0492](https://unit42.paloaltonetworks.com/cve-2022-0492-cgroups/): Score 7.8 (HIGH)[CVE-2021-25741](https://nvd.nist.gov/vuln/detail/CVE-2021-25741): Score: 8.1 (HIGH) / 8.8 (HIGH)[CVE-2017-1002101](https://nvd.nist.gov/vuln/detail/CVE-2017-1002101): Score: 9.6 (CRITICAL) / 8.8(HIGH)

To learn more, read this [blog post](https://kubernetes.io/blog/2025/04/25/userns-enabled-by-default/) with additional information around user-namespaces.

## App Armor

To limit container actions, you can use the [AppArmor](https://kubernetes.io/docs/tutorials/clusters/apparmor/) Linux kernel security module. AppArmor is available as part of the underlying AKS node OS and is enabled by default. You create AppArmor profiles that restrict read, write, or execute actions, or system functions like mounting filesystems. Default AppArmor profiles restrict access to various `/proc`

and `/sys`

locations and provide a means to logically isolate containers from the underlying node. AppArmor works for any application that runs on Linux, not just Kubernetes pods.

Note

Azure Linux 3.0 does not offer AppArmor support. For Azure Linux 3.0 nodes, the recommendation is to leverage SELinux instead of AppArmor for mandatory access control.

To see AppArmor in action, the following example creates a profile that prevents writing to files.

[SSH](manage-ssh-node-access)to an AKS node.Create a file named

*deny-write.profile*.Copy and paste the following content:

`#include <tunables/global> profile k8s-apparmor-example-deny-write flags=(attach_disconnected) { #include <abstractions/base> file, # Deny all file writes. deny /** w, }`


AppArmor profiles are added using the `apparmor_parser`

command.

Add the profile to AppArmor.

Specify the name of the profile created in the previous step:

`sudo apparmor_parser deny-write.profile`

If the profile is correctly parsed and applied to AppArmor, you won't see any output and you'll return to the command prompt.

From your local machine, create a pod manifest named

*aks-apparmor.yaml*. This manifest:- Defines an annotation for
`container.apparmor.security.beta.kubernetes`

. - References the
*deny-write*profile created in the previous steps.

`apiVersion: v1 kind: Pod metadata: name: hello-apparmor annotations: container.apparmor.security.beta.kubernetes.io/hello: localhost/k8s-apparmor-example-deny-write spec: containers: - name: hello image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: [ "sh", "-c", "echo 'Hello AppArmor!' && sleep 1h" ]`

- Defines an annotation for
With the pod deployed, run the following command and verify the

*hello-apparmor*pod shows a*Running*status:`kubectl get pods NAME READY STATUS RESTARTS AGE aks-ssh 1/1 Running 0 4m2s hello-apparmor 0/1 Running 0 50s`


For more information about AppArmor, see [AppArmor profiles in Kubernetes](https://kubernetes.io/docs/tutorials/clusters/apparmor/).

## Secure computing (seccomp)

While AppArmor works for any Linux application, [seccomp ( secure computing)](https://kubernetes.io/docs/reference/node/seccomp/) works at the process level. Seccomp is also a Linux kernel security module and is natively supported by the

`containerd`

runtime used by AKS nodes. With seccomp, you can limit a container's system calls. Seccomp establishes an extra layer of protection against common system call vulnerabilities exploited by malicious actors and allows you to specify a default profile for all workloads in the node.### Configure a default seccomp profile (preview)

You can apply default seccomp profiles using [custom node configurations](/en-us/azure/aks/custom-node-configuration) when creating a new Linux node pool. There are two values supported on AKS: `RuntimeDefault`

and `Unconfined`

. Some workloads might require a lower number of syscall restrictions than others. This means that they can fail during runtime with the 'RuntimeDefault' profile. To mitigate such a failure, you can specify the `Unconfined`

profile. If your workload requires a custom profile, see [Configure a custom seccomp profile](#configure-a-custom-seccomp-profile).

#### Limitations

- SeccompDefault is not a supported parameter for windows node pools.
- SeccompDefault is available starting in 2024-09-02-preview API.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

#### Register the `KubeletDefaultSeccompProfilePreview`

feature flag

Register the

`KubeletDefaultSeccompProfilePreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "KubeletDefaultSeccompProfilePreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "KubeletDefaultSeccompProfilePreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


#### Restrict your container's system calls with seccomp

**1. Follow steps to apply a seccomp profile in your kubelet configuration by specifying "seccompDefault": "RuntimeDefault"**.


`RuntimeDefault`

uses containerd's default seccomp profile, restricting certain system calls to enhance security. Restricted syscalls will fail. For more information, see the [containerD default seccomp profile](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51).

**2. Check that the configuration was applied**.

You can confirm the settings are applied to the nodes by [connecting to the host](node-access) and verifying configuration changes have been made on the filesystem.

**3. Troubleshoot workload failures**.

When SeccompDefault is enabled, the container runtime default seccomp profile is used by default for all workloads scheduled on the node. This might cause workloads to fail due to blocked syscalls. If a workload failure has occurred, you might see errors such as:

- Workload is existing unexpectedly after the feature is enabled, with "permission denied" error.
- Seccomp error messages can also be seen in auditd or syslog by replacing SCMP_ACT_ERRNO with SCMP_ACT_LOG in the default profile.

If you experience the above errors, we recommend that you change your seccomp profile to `Unconfined`

. `Unconfined`

places no restrictions on syscalls, allowing all system calls, which reduces security.

### Configure a custom seccomp profile

With a custom seccomp profile, you can have more granular control over restricted syscalls. Align to the best practice of granting the container minimal permission only to run by:

- Defining with filters what actions to allow or deny.
- Annotating within a pod YAML manifest to associate with the seccomp filter.

To see seccomp in action, create a filter that prevents changing permissions on a file.

[SSH](manage-ssh-node-access)to an AKS node.Create a seccomp filter named

*/var/lib/kubelet/seccomp/prevent-chmod*.Copy and paste the following content:

`{ "defaultAction": "SCMP_ACT_ALLOW", "syscalls": [ { "name": "chmod", "action": "SCMP_ACT_ERRNO" }, { "name": "fchmodat", "action": "SCMP_ACT_ERRNO" }, { "name": "chmodat", "action": "SCMP_ACT_ERRNO" } ] }`

In version 1.19 and later, you need to configure:

`{ "defaultAction": "SCMP_ACT_ALLOW", "syscalls": [ { "names": ["chmod","fchmodat","chmodat"], "action": "SCMP_ACT_ERRNO" } ] }`

From your local machine, create a pod manifest named

*aks-seccomp.yaml*and paste the following content. This manifest:- Defines an annotation for
`seccomp.security.alpha.kubernetes.io`

. - References the
*prevent-chmod*filter created in the previous step.

`apiVersion: v1 kind: Pod metadata: name: chmod-prevented annotations: seccomp.security.alpha.kubernetes.io/pod: localhost/prevent-chmod spec: containers: - name: chmod image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: - "chmod" args: - "777" - /etc/hostname restartPolicy: Never`

In version 1.19 and later, you need to configure:

`apiVersion: v1 kind: Pod metadata: name: chmod-prevented spec: securityContext: seccompProfile: type: Localhost localhostProfile: prevent-chmod containers: - name: chmod image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: - "chmod" args: - "777" - /etc/hostname restartPolicy: Never`

- Defines an annotation for
Deploy the sample pod using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f ./aks-seccomp.yaml`

View pod status using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.- The pod reports an error.
- The
`chmod`

command is prevented from running by the seccomp filter, as shown in the example output:

`kubectl get pods NAME READY STATUS RESTARTS AGE chmod-prevented 0/1 Error 0 7s`


For help troubleshooting your seccomp profile see the article [Troubleshoot seccomp profile configuration in Azure Kubernetes Service](/en-us/troubleshoot/azure/azure-kubernetes/security/troubleshoot-seccomp-profiles).

## Seccomp security profile options

Seccomp security profiles are a set of defined syscalls that are allowed or restricted. Most container runtimes have a default seccomp profile that is similar if not the same as the one Docker uses. For more information about available profiles, see [Docker](https://kubernetes.io/docs/reference/node/seccomp/) or [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) default seccomp profiles.

AKS uses the [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) default seccomp profile for our RuntimeDefault when you configure seccomp using [custom node configuration](/en-us/azure/aks/custom-node-configuration).

### Significant syscalls blocked by default profile

Both [Docker](https://kubernetes.io/docs/reference/node/seccomp/) and [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) maintain allowlists of safe syscalls. This table lists the significant (but not all) syscalls that are effectively blocked because they aren't on the allowlist. If any of the blocked syscalls are required by your workload, don't use the `RuntimeDefault`

seccomp profile.

When changes are made to [Docker](https://kubernetes.io/docs/reference/node/seccomp/) and [containerD](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51), AKS updates their default configuration to match. Updates to this list may cause workload failure. For release updates, see [AKS release notes](https://github.com/Azure/AKS/releases).

| Blocked syscall | Description |
|---|---|
`acct` |
Accounting syscall which could let containers disable their own resource limits or process accounting. Also gated by `CAP_SYS_PACCT` . |
`add_key` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`bpf` |
Deny loading potentially persistent bpf programs into kernel, already gated by `CAP_SYS_ADMIN` . |
`clock_adjtime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`clock_settime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`clone` |
Deny cloning new namespaces. Also gated by `CAP_SYS_ADMIN for CLONE_*` flags, except `CLONE_NEWUSER` . |
`create_module` |
Deny manipulation and functions on kernel modules. Obsolete. Also gated by `CAP_SYS_MODULE` . |
`delete_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`finit_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`get_kernel_syms` |
Deny retrieval of exported kernel and module symbols. Obsolete. |
`get_mempolicy` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`init_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`ioperm` |
Prevent containers from modifying kernel I/O privilege levels. Already gated by `CAP_SYS_RAWIO` . |
`iopl` |
Prevent containers from modifying kernel I/O privilege levels. Already gated by `CAP_SYS_RAWIO` . |
`kcmp` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`kexec_file_load` |
Sister syscall of kexec_load that does the same thing, slightly different arguments. Also gated by `CAP_SYS_BOOT` . |
`kexec_load` |
Deny loading a new kernel for later execution. Also gated by `CAP_SYS_BOOT` . |
`keyctl` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`lookup_dcookie` |
Tracing/profiling syscall, which could leak information on the host. Also gated by `CAP_SYS_ADMIN` . |
`mbind` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`mount` |
Deny mounting, already gated by `CAP_SYS_ADMIN` . |
`move_pages` |
Syscall that modifies kernel memory and NUMA settings. |
`nfsservctl` |
Deny interaction with the kernel nfs daemon. Obsolete since Linux 3.1. |
`open_by_handle_at` |
Cause of an old container breakout. Also gated by `CAP_DAC_READ_SEARCH` . |
`perf_event_open` |
Tracing/profiling syscall, which could leak information on the host. |
`personality` |
Prevent container from enabling BSD emulation. Not inherently dangerous, but poorly tested, potential for kernel vulns. |
`pivot_root` |
Deny pivot_root, should be privileged operation. |
`process_vm_readv` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`process_vm_writev` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`ptrace` |
Tracing/profiling syscall. Blocked in Linux kernel versions before 4.8 to avoid seccomp bypass. Tracing/profiling arbitrary processes is already blocked by dropping CAP_SYS_PTRACE, because it could leak information on the host. |
`query_module` |
Deny manipulation and functions on kernel modules. Obsolete. |
`quotactl` |
Quota syscall which could let containers disable their own resource limits or process accounting. Also gated by `CAP_SYS_ADMIN` . |
`reboot` |
Don't let containers reboot the host. Also gated by `CAP_SYS_BOOT` . |
`request_key` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`set_mempolicy` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`setns` |
Deny associating a thread with a namespace. Also gated by `CAP_SYS_ADMIN` . |
`settimeofday` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`stime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`swapon` |
Deny start/stop swapping to file/device. Also gated by `CAP_SYS_ADMIN` . |
`swapoff` |
Deny start/stop swapping to file/device. Also gated by `CAP_SYS_ADMIN` . |
`sysfs` |
Obsolete syscall. |
`_sysctl` |
Obsolete, replaced by /proc/sys. |
`umount` |
Should be a privileged operation. Also gated by `CAP_SYS_ADMIN` . |
`umount2` |
Should be a privileged operation. Also gated by `CAP_SYS_ADMIN` . |
`unshare` |
Deny cloning new namespaces for processes. Also gated by `CAP_SYS_ADMIN` , with the exception of unshare --user. |
`uselib` |
Older syscall related to shared libraries, unused for a long time. |
`userfaultfd` |
Userspace page fault handling, largely needed for process migration. |
`ustat` |
Obsolete syscall. |
`vm86` |
In kernel x86 real mode virtual machine. Also gated by `CAP_SYS_ADMIN` . |
`vm86old` |
In kernel x86 real mode virtual machine. Also gated by `CAP_SYS_ADMIN` . |

## Next steps

For associated best practices, see [Best practices for cluster security and upgrades in AKS](operator-best-practices-cluster-security) and [Best practices for pod security in AKS](developer-best-practices-pod-security).


---

<!-- DOCUMENTO FUSIONADO: _upgrade-aks-node-pools-rolling_auto-upgrade-node-image.md -->
<!-- URL ORIGINAL: N/A -->

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
