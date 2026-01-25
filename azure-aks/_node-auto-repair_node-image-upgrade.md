---
merged_at: 2026-01-25T12:06:27.737291
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-auto-repair.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-repair -->

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

<!-- DOCUMENTO FUSIONADO: node-image-upgrade.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-image-upgrade -->

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
