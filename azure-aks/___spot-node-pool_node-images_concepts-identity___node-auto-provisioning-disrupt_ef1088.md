---
merged_at: 2026-01-26T23:04:06.001337
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/spot-node-pool -->

# Add an Azure Spot node pool to an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you add a secondary Spot node pool to an existing Azure Kubernetes Service (AKS) cluster.

A Spot node pool is a node pool backed by an [Azure Spot Virtual Machine scale set](/en-us/azure/virtual-machine-scale-sets/use-spot). With Spot VMs in your AKS cluster, you can take advantage of unutilized Azure capacity with significant cost savings. The amount of available unutilized capacity varies based on many factors, such as node size, region, and time of day.

When you deploy a Spot node pool, Azure allocates the Spot nodes if there's capacity available and deploys a Spot scale set that backs the Spot node pool in a single default domain. There's no SLA for the Spot nodes. There are no high availability guarantees. If Azure needs capacity back, the Azure infrastructure evicts the Spot nodes.

Spot nodes are great for workloads that can handle interruptions, early terminations, or evictions. For example, workloads such as batch processing jobs, development and testing environments, and large compute workloads might be good candidates to schedule on a Spot node pool.

## Before you begin

- This article assumes a basic understanding of Kubernetes and Azure Load Balancer concepts. For more information, see
[Kubernetes core concepts for Azure Kubernetes Service (AKS)](concepts-clusters-workloads). - If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - When you create a cluster to use a Spot node pool, the cluster must use Virtual Machine Scale Sets for node pools and the
*Standard*SKU load balancer. You must also add another node pool after you create your cluster, which is covered in this tutorial. - This article requires that you're running the Azure CLI version 2.14 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

The following limitations apply when you create and manage AKS clusters with a Spot node pool:

- A Spot node pool can't be a default node pool, it can only be used as a secondary pool.
- You can't upgrade the control plane and node pools at the same time. You must upgrade them separately or remove the Spot node pool to upgrade the control plane and remaining node pools at the same time.
- A Spot node pool must use Virtual Machine Scale Sets.
- You can't change
`ScaleSetPriority`

or`SpotMaxPrice`

after creation. - When setting
`SpotMaxPrice`

, the value must be*-1*or a*positive value with up to five decimal places*. - A Spot node pool has the
`kubernetes.azure.com/scalesetpriority:spot`

label, the`kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

taint, and the system pods have anti-affinity. - You must add a
[corresponding toleration](#verify-the-spot-node-pool)and affinity to schedule workloads on a Spot node pool.

## Add a Spot node pool to an AKS cluster

When adding a Spot node pool to an existing cluster, it must be a cluster with multiple node pools enabled. When you create an AKS cluster with multiple node pools enabled, you create a node pool with a `priority`

of `Regular`

by default. To add a Spot node pool, you must specify `Spot`

as the value for `priority`

. For more details on creating an AKS cluster with multiple node pools, see [use multiple node pools](create-node-pools).

- Create a node pool with a
`priority`

of`Spot`

using thecommand.`az aks nodepool add`


```
export SPOT_NODEPOOL="spotnodepool"
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER \
--name $SPOT_NODEPOOL \
--priority Spot \
--eviction-policy Delete \
--spot-max-price -1 \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3 \
--no-wait
```


In the previous command, the `priority`

of `Spot`

makes the node pool a Spot node pool. The `eviction-policy`

parameter is set to `Delete`

, which is the default value. When you set the [eviction policy](/en-us/azure/virtual-machine-scale-sets/use-spot#eviction-policy) to `Delete`

, nodes in the underlying scale set of the node pool are deleted when they're evicted.

You can also set the eviction policy to `Deallocate`

, which means that the nodes in the underlying scale set are set to the *stopped-deallocated* state upon eviction. Nodes in the *stopped-deallocated* state count against your compute quota and can cause issues with cluster scaling or upgrading. The `priority`

and `eviction-policy`

values can only be set during node pool creation. Those values can't be updated later.

The previous command also enables the [cluster autoscaler](cluster-autoscaler), which we recommend using with Spot node pools. Based on the workloads running in your cluster, the cluster autoscaler scales the number of nodes up and down. For Spot node pools, the cluster autoscaler will scale up the number of nodes after an eviction if more nodes are still needed. If you change the maximum number of nodes a node pool can have, you also need to adjust the `maxCount`

value associated with the cluster autoscaler. If you don't use a cluster autoscaler, upon eviction, the Spot pool will eventually decrease to *0* and require manual operation to receive any additional Spot nodes.

Important

Only schedule workloads on Spot node pools that can handle interruptions, such as batch processing jobs and testing environments. We recommend you set up [taints and tolerations](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations) on your Spot node pool to ensure that only workloads that can handle node evictions are scheduled on a Spot node pool. For example, the above command adds a taint of `kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

, so only pods with a corresponding toleration are scheduled on this node.

## Verify the Spot node pool

- Verify your node pool was added using the
command and confirming the`az aks nodepool show`

`scaleSetPriority`

is`Spot`

.

```
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $AKS_CLUSTER --name $SPOT_NODEPOOL
```


Results:

```
{
"artifactStreamingProfile": null,
"availabilityZones": null,
"capacityReservationGroupId": null,
"count": 3,
"creationData": null,
"currentOrchestratorVersion": "1.30.10",
"eTag": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"enableAutoScaling": true,
"enableCustomCaTrust": false,
"enableEncryptionAtHost": false,
"enableFips": false,
"enableNodePublicIp": false,
"enableUltraSsd": false,
"gatewayProfile": null,
"gpuInstanceProfile": null,
"gpuProfile": null,
"hostGroupId": null,
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/xxxxxxxxxxxxxxxx/providers/Microsoft.ContainerService/managedClusters/xxxxxxxxxxxxxxxx/agentPools/xxxxxxxxxxxx",
"kubeletConfig": null,
"kubeletDiskType": "OS",
"linuxOsConfig": null,
"maxCount": 3,
"maxPods": 30,
"messageOfTheDay": null,
"minCount": 1,
"mode": "User",
"name": "xxxxxxxxxxxx",
"networkProfile": {
"allowedHostPorts": null,
"applicationSecurityGroups": null,
"nodePublicIpTags": null
},
"nodeImageVersion": "AKSUbuntu-2204gen2containerd-xxxxxxxx.xx.x",
"nodeInitializationTaints": null,
"nodeLabels": {
"kubernetes.azure.com/scalesetpriority": "spot"
},
"nodePublicIpPrefixId": null,
"nodeTaints": [
"kubernetes.azure.com/scalesetpriority=spot:NoSchedule"
],
"orchestratorVersion": "x.xx.xx",
"osDiskSizeGb": 128,
"osDiskType": "Managed",
"osSku": "Ubuntu",
"osType": "Linux",
"podIpAllocationMode": null,
"podSubnetId": null,
"powerState": {
"code": "Running"
},
"provisioningState": "Creating",
"proximityPlacementGroupId": null,
"resourceGroup": "xxxxxxxxxxxxxxxx",
"scaleDownMode": "Delete",
"scaleSetEvictionPolicy": "Delete",
"scaleSetPriority": "Spot",
"securityProfile": {
"enableSecureBoot": false,
"enableVtpm": false,
"sshAccess": "LocalUser"
},
"spotMaxPrice": -1.0,
"status": null,
"tags": null,
"type": "Microsoft.ContainerService/managedClusters/agentPools",
"typePropertiesType": "VirtualMachineScaleSets",
"upgradeSettings": {
"drainTimeoutInMinutes": null,
"maxSurge": null,
"maxUnavailable": null,
"nodeSoakDurationInMinutes": null,
"undrainableNodeBehavior": null
},
"virtualMachineNodesStatus": null,
"virtualMachinesProfile": null,
"vmSize": "Standard_DS2_v2",
"vnetSubnetId": null,
"windowsProfile": null,
"workloadRuntime": "OCIContainer"
}
```


## Schedule a pod to run on the Spot node

To schedule a pod to run on a Spot node, you can add a toleration and node affinity that corresponds to the taint applied to your Spot node.

The following example shows a portion of a YAML file that defines a toleration corresponding to the `kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

taint and a node affinity corresponding to the `kubernetes.azure.com/scalesetpriority=spot`

label used in the previous step with `requiredDuringSchedulingIgnoredDuringExecution`

and `preferredDuringSchedulingIgnoredDuringExecution`

node affinity rules:

```
spec:
containers:
- name: spot-example
tolerations:
- key: "kubernetes.azure.com/scalesetpriority"
operator: "Equal"
value: "spot"
effect: "NoSchedule"
affinity:
nodeAffinity:
requiredDuringSchedulingIgnoredDuringExecution:
nodeSelectorTerms:
- matchExpressions:
- key: "kubernetes.azure.com/scalesetpriority"
operator: In
values:
- "spot"
preferredDuringSchedulingIgnoredDuringExecution:
- weight: 1
preference:
matchExpressions:
- key: another-node-label-key
operator: In
values:
- another-node-label-value
```


When you deploy a pod with this toleration and node affinity, Kubernetes successfully schedules the pod on the nodes with the taint and label applied. In this example, the following rules apply:

- The node
*must*have a label with the key`kubernetes.azure.com/scalesetpriority`

, and the value of that label*must*be`spot`

. - The node
*preferably*has a label with the key`another-node-label-key`

, and the value of that label*must*be`another-node-label-value`

.

For more information, see [Assigning pods to nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity).

## Upgrade a Spot node pool

When you upgrade a Spot node pool, AKS internally issues a cordon and an eviction notice, but no drain is applied. There are no surge nodes available for Spot node pool upgrades. Outside of these changes, the behavior when upgrading Spot node pools is consistent with that of other node pool types.

For more information on upgrading, see [Upgrade an AKS cluster](upgrade-cluster).

## Max price for a Spot pool

[Pricing for Spot instances is variable](/en-us/azure/virtual-machine-scale-sets/use-spot#pricing), based on region and SKU. For more information, see pricing information for [Linux](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) and [Windows](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/windows/).

With variable pricing, you have the option to set a max price, in US dollars (USD) using up to five decimal places. For example, the value *0.98765* would be a max price of *$0.98765 USD per hour*. If you set the max price to *-1*, the instance won't be evicted based on price. As long as there's capacity and quota available, the price for the instance will be the lower price of either the current price for a Spot instance or for a standard instance.

## Next steps

In this article, you learned how to add a Spot node pool to an AKS cluster. For more information about how to control pods across node pools, see [Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-images -->

# Node images in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes the node images available for Azure Kubernetes Service (AKS) nodes.

Caution

In this article, there are references to Ubuntu OS versions that are being deprecated for AKS.

- Starting on March 17, 2027, AKS no longer supports Ubuntu 20.04. Existing node images will be deleted and AKS will no longer provide security updates. You'll no longer be able to scale your node pools. Migrate to a supported Ubuntu version by
[upgrading your node pools](upgrade-aks-cluster)to kubernetes version 1.34+. For more information on this retirement, see[AKS GitHub Issues](https://github.com/Azure/AKS/issues/4874). - As of
**November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the[202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning**March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by[upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster)to a supported Kubernetes version or migrating to[osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see[[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

Important

Older node images can contain unpatched security vulnerabilities and might not work properly with recently released features. Using older images might lead to issues with scaling, node readiness, and security. Depending on the age of the image version, it could also place the cluster outside of the support scope until you perform a node image upgrade. **We recommend that you keep node images current and enable automatic upgrades**.

## Node image releases

Azure Kubernetes Service (AKS) regularly provides new node images, so it's beneficial to upgrade your node images frequently to access the latest AKS features, component updates, and security fixes. You can find detailed summaries of each node image version in the [AKS VHD notes](https://github.com/Azure/AKS/tree/master/vhd-notes).

Linux node images are released weekly, and Windows node images are released monthly. New node images are included in the [AKS release notes](https://github.com/Azure/AKS/releases).


Best practice guidanceConfigure

[automatic node image upgrades]and schedule them using[planned maintenance]. This will ensure that your node images are always up to date without requiring manual upgrades.

When new node images are released, it can take up to two weeks for the updates to be rolled out across all regions. The [AKS Release Tracker](release-tracker) shows the current latest node image version, three previously available node image versions for each region, and the node image update order by region. Once the node image is available in your region, you can perform a [manual node image upgrade](node-image-upgrade) or configure [automatic node image upgrades](auto-upgrade-node-os-image) and schedule them using [planned maintenance](planned-maintenance).

## Default node images

AKS sets a default operating system (OS) and node image during cluster and node pool creation. OS Type can be used to filter between Linux or Windows.

| OS Type | Default OS | Default node image |
|---|---|---|
| Not Specified | Ubuntu Linux | Ubuntu with containerd and gen 2 |
| Linux | Ubuntu Linux | Ubuntu with containerd and gen 2 |
| Windows | Windows Server | Windows Server Long Term Servicing Channel (LTSC) with containerd and gen 1 |

Note

You can't specify the Windows OS Type during cluster creation since the system node pool in every cluster must be Linux.

### Factors that influence the default node image

The following factors influence the default image AKS chooses for your node pool:

**OS SKU**: If`--os-sku`

is specified, then your default OS changes. For example, if you specify Azure Linux as the OS SKU, then your node image is Azure Linux with containerd.**Virtual machine (VM) size**:**Hypervisor generation**: Each VM size supports Generation 1,[Generation 2](generation-2-vm), or both.- If Generation 2 is supported, AKS defaults to using the Generation 2 node image in all OS versions except for Windows Server 2019 and Windows Server 2022.
- If only Generation 1 is supported, AKS defaults to using the Generation 1 node image. Generation 1 isn't supported for Azure Linux OS Guard (preview) or Flatcar Container Linux for AKS (preview).

**Feature enablement**: There are some features embedded into the node image. If you choose to use any of these features, your default node image changes.[Federal Information Processing Standards (FIPS)](enable-fips-nodes)changes the default node image for all Linux node pools.[Pod Sandboxing](use-pod-sandboxing)changes the default node image for Azure Linux node pools.[Trusted Launch](use-trusted-launch)changes the default node image for all Linux node pools.


Note

Certain features can't be combined in a single node pool. Follow links to the feature documentation to review the limitations.

## Available Linux node images

### Ubuntu node images

The Ubuntu node images are fully validated by AKS and supported by Microsoft, Canonical, and the Ubuntu community. AKS won't retire an Ubuntu version before the end of Canonical's support lifecycle.

| Node image | Use case | Limitations |
|---|---|---|
Ubuntu with containerd and Gen 1 |
This is the standard node image for Ubuntu node pools using a VM size that only supports Generation 1. | N/A |
Ubuntu with containerd and Gen 2 |
This is the standard node image for Ubuntu node pools using a VM size that supports Generation 2. If a VM size supports both Generation 1 and Generation 2, this node image is selected. | N/A |
Ubuntu with containerd and FIPS |
This is a variant of the default node image for customers that enable
|

**Ubuntu with containerd and Arm64**[Arm64](use-arm64-vms). These images support Generation 2 only.**Ubuntu with containerd and CVM**[Confidential VM](use-cvm)size. These images support Generation 2 only.**Ubuntu with containerd and Trusted Launch**[Trusted Launch](use-trusted-launch). These images support Generation 2 only.### Azure Linux node images

The Azure Linux node images are fully validated by AKS and built from source, using a native AKS image.

| Node image | Use case | Limitations |
|---|---|---|
Azure Linux with containerd and Gen 1 |
This is the standard node image for Azure Linux node pools using a VM size that only supports Generation 1. | N/A |
Azure Linux with containerd and Gen 2 |
This is the standard node image for Azure Linux node pools using a VM size that supports Generation 2. If a VM size supports both Generation 1 and Generation 2, node image is selected. | N/A |
Azure Linux with containerd and FIPS |
This is a variant of the default node image for customers that enable
|

**Azure Linux with containerd and Arm64**[Arm64](use-arm64-vms). These images support Generation 2 only.**Azure Linux with containerd, FIPS, and Arm64**[Federal Information Processing Standards (FIPS)](enable-fips-nodes)and use a VM size that supports[Arm64](use-arm64-vms). These images support Generation 2 only.**Azure Linux with containerd and Trusted Launch**[Trusted Launch](use-trusted-launch). These images support Generation 2 only.**Azure Linux with containerd and Pod Sandboxing**[Pod Sandboxing](use-pod-sandboxing). These images support Generation 2 only.### Azure Linux with OS Guard for AKS (preview) node images

The Azure Linux with OS Guard for AKS node images are fully validated by AKS and built from source, using a native AKS image. Versioning for Azure Linux with OS Guard node images follow the AKS date-based format (for example: 202509.23.0). You can check the node images in the release notes and by running the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. For more information, see [Azure Linux with OS Guard for AKS](use-azure-linux-os-guard).

| Node image | Use case | Limitations |
|---|---|---|
Azure Linux with OS Guard with containerd, Gen 2, FIPS, and Trusted Launch |
This is the standard node image for Azure Linux with OS Guard for AKS node pools using a VM size. If you use a VM size that supports Gen 1 only, you won't be able to use Azure Linux with OS Guard. | N/A |

### Flatcar Container Linux for AKS (preview) node images

The Flatcar Container Linux for AKS node images are fully validated by AKS and supported by Microsoft and the Flatcar community. Versioning for Flatcar Container Linux node images follow the AKS date-based format (for example: 202506.13.0). You can check the node images in the release notes and by using the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. You can check the Flatcar version number (for example: Flatcar 4344.0.0) in the release notes and by running the `kubectl get nodes`

command. For more information, see [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks).

| Node image | Use case | Limitations |
|---|---|---|
Flatcar Container Linux with containerd and Gen 2 |
This is the standard node image for Flatcar Container Linux for AKS node pools using a VM size. If you use a VM size that supports Gen 1 only, you won't be able to use Flatcar OS. | N/A |
Flatcar Container Linux with containerd and Arm64 |
This is a variant of the default node image for customers that use a VM size that supports
|

## Available Windows Server node images

The Windows Server node images are fully validated by AKS and supported by Microsoft.

### Windows Server Long Term Servicing Channel (LTSC) node images

| Node image | Use case | Limitations |
|---|---|---|
Windows Server with containerd and Gen 1 |
This is the standard node image for Windows node pools using a VM size that supports Generation 1. If a VM size supports both Generation 1 and Generation 2, this node image is selected if using Windows Server 2019 or Windows Server 2022. | N/A |
Windows Server with containerd and Gen 2 |
This is the standard node image for Windows node pools using a VM size that supports Generation 2. If a VM size supports both Generation 1 and Generation 2, this node image is selected if using Windows Server 2025. | N/A |

### Windows Server Annual Channel for Containers (preview) node images

| Node image | Use case | Limitations |
|---|---|---|
Windows Server with containerd and Gen 1 |
This is the standard node image for Windows node pools using a VM size that only supports Generation 1. If a VM size supports both Generation 1 and Generation 2, this node image is selected. | N/A |
Windows Server with containerd and Gen 2 |
This is the standard node image for Windows node pools using a VM size that supports Generation 2. | N/A |

## Next steps

To learn more about node images, node pool upgrades, and node configurations on AKS, see the following resources:

- To learn about nodes and node configurations, see
[AKS core concepts](core-aks-concepts). - Configure
[automatic node image upgrades](auto-upgrade-node-os-image)and schedule them using[planned maintenance](planned-maintenance). - Apply
[custom node configurations](custom-node-configuration)to modify OS or kubelet settings. - For information about the latest node images, see the
[AKS release notes](https://github.com/Azure/AKS/releases). [Automatically apply cluster and node pool upgrades with GitHub Actions](node-upgrade-github-actions).- Learn about upgrading best practices with
[AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-identity -->

# Access and identity options for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can authenticate, authorize, secure, and control access to Kubernetes clusters in a variety of ways:

- Using Kubernetes role-based access control (Kubernetes RBAC), you can grant users, groups, and service accounts access to only the resources they need.
- With Azure Kubernetes Service (AKS), you can further enhance the security and permissions structure using Microsoft Entra ID and Azure RBAC.

Kubernetes RBAC and AKS help you secure your cluster access and provide only the minimum required permissions to developers and operators.

This article introduces the core concepts that help you authenticate and assign permissions in AKS.

## Kubernetes RBAC

Kubernetes RBAC provides granular filtering of user actions. With this control mechanism:

- You assign users or user groups permission to create and modify resources or view logs from running application workloads.
- You can scope permissions to a single namespace or across the entire AKS cluster.
- You create
*roles*to define permissions, and then assign those roles to users with*role bindings*.

For more information, see [Using Kubernetes RBAC authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/).

### Roles and ClusterRoles

#### Roles

Before assigning permissions to users with Kubernetes RBAC, you'll define user permissions as a *Role*. Grant permissions within a namespace using roles.

Note

Kubernetes roles *grant* permissions; they don't *deny* permissions.

To grant permissions across the entire cluster or to cluster resources outside a given namespace, you can instead use *ClusterRoles*.

#### ClusterRoles

A ClusterRole grants and applies permissions to resources across the entire cluster, not a specific namespace.

### RoleBindings and ClusterRoleBindings

Once you've defined roles to grant permissions to resources, you assign those Kubernetes RBAC permissions with a *RoleBinding*. If your AKS cluster [integrates with Microsoft Entra ID](#azure-ad-integration), RoleBindings grant permissions to Microsoft Entra users to perform actions within the cluster. See how in [Control access to cluster resources using Kubernetes role-based access control and Microsoft Entra identities](azure-ad-rbac).

#### RoleBindings

Assign roles to users for a given namespace using RoleBindings. With RoleBindings, you can logically segregate a single AKS cluster, only enabling users to access the application resources in their assigned namespace.

To bind roles across the entire cluster, or to cluster resources outside a given namespace, you instead use *ClusterRoleBindings*.

#### ClusterRoleBinding

With a ClusterRoleBinding, you bind roles to users and apply to resources across the entire cluster, not a specific namespace. This approach lets you grant administrators or support engineers access to all resources in the AKS cluster.

Note

Microsoft/AKS performs any cluster actions with user consent under a built-in Kubernetes role `aks-service`

and built-in role binding `aks-service-rolebinding`

.

This role enables AKS to troubleshoot and diagnose cluster issues, but can't modify permissions nor create roles or role bindings, or other high privilege actions. Role access is only enabled under active support tickets with just-in-time (JIT) access. Read more about [AKS support policies](support-policies).

### Kubernetes service accounts

*Service accounts* are one of the primary user types in Kubernetes. The Kubernetes API holds and manages service accounts. Service account credentials are stored as Kubernetes secrets, allowing them to be used by authorized pods to communicate with the API Server. Most API requests provide an authentication token for a service account or a normal user account.

Normal user accounts allow more traditional access for human administrators or developers, not just services and processes. While Kubernetes doesn't provide an identity management solution to store regular user accounts and passwords, you can integrate external identity solutions into Kubernetes. For AKS clusters, this integrated identity solution is Microsoft Entra ID.

For more information on the identity options in Kubernetes, see [Kubernetes authentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication).

## Azure role-based access control

Azure role-based access control (RBAC) is an authorization system built on [Azure Resource Manager](/en-us/azure/azure-resource-manager/management/overview) that provides fine-grained access management of Azure resources.

| RBAC system | Description |
|---|---|
| Kubernetes RBAC | Designed to work on Kubernetes resources within your AKS cluster. |
| Azure RBAC | Designed to work on resources within your Azure subscription. |

With Azure RBAC, you create a *role definition* that outlines the permissions to be applied. You then assign a user or group this role definition via a *role assignment* for a particular *scope*. The scope can be an individual resource, a resource group, or across the subscription.

For more information, see [What is Azure role-based access control (Azure RBAC)?](/en-us/azure/role-based-access-control/overview)

There are two levels of access needed to fully operate an AKS cluster:

[Access the AKS resource in your Azure subscription](#azure-rbac-to-authorize-access-to-the-aks-resource).- Control scaling or upgrading your cluster using the AKS APIs.
- Pull your
`kubeconfig`

.

- Access to the Kubernetes API. This access is controlled by either:
[Kubernetes RBAC](#kubernetes-rbac)(traditionally).[Integrating Azure RBAC with AKS for Kubernetes authorization](#azure-rbac-for-kubernetes-authorization).


### Azure RBAC to authorize access to the AKS resource

With Azure RBAC, you can provide your users (or identities) with granular access to AKS resources across one or more subscriptions. For example, you could use the [Azure Kubernetes Service Contributor role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-contributor-role) to scale and upgrade your cluster. Meanwhile, another user with the [Azure Kubernetes Service Cluster Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) only has permission to pull the Admin `kubeconfig`

.

[Use Azure RBAC to define access to the Kubernetes configuration file in AKS](control-kubeconfig-access).

### Azure RBAC for Kubernetes Authorization

With the Azure RBAC integration, AKS will use a Kubernetes Authorization webhook server so you can manage Microsoft Entra integrated Kubernetes cluster resource permissions and assignments using Azure role definition and role assignments.

As shown in the above diagram, when using the Azure RBAC integration, all requests to the Kubernetes API will follow the same authentication flow as explained on the [Microsoft Entra integration section](#azure-ad-integration).

If the identity making the request exists in Microsoft Entra ID, Azure will team with Kubernetes RBAC to authorize the request. If the identity exists outside of Microsoft Entra ID (i.e., a Kubernetes service account), authorization will defer to the normal Kubernetes RBAC.

In this scenario, you use Azure RBAC mechanisms and APIs to assign users built-in roles or create custom roles, just as you would with Kubernetes roles.

With this feature, you not only give users permissions to the AKS resource across subscriptions, but you also configure the role and permissions for inside each of those clusters controlling Kubernetes API access. For example, you can grant the `Azure Kubernetes Service RBAC Reader`

role on the subscription scope. The role recipient will be able to list and get all Kubernetes objects from all clusters without modifying them.

Important

You need to enable Azure RBAC for Kubernetes authorization before using this feature. For more details and step by step guidance, follow our [Use Azure RBAC for Kubernetes Authorization](manage-azure-rbac) how-to guide.

#### Built-in roles

AKS provides the following four built-in roles. They are similar to the [Kubernetes built-in roles](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#user-facing-roles) with a few differences, like supporting CRDs. See the full list of actions allowed by each [Azure built-in role](/en-us/azure/role-based-access-control/built-in-roles).

| Role | Description |
|---|---|
| Azure Kubernetes Service RBAC Reader | Allows read-only access to see most objects in a namespace. Doesn't allow viewing roles or role bindings. Doesn't allow viewing `Secrets` . Reading the `Secrets` contents enables access to `ServiceAccount` credentials in the namespace, which would allow API access as any `ServiceAccount` in the namespace (a form of privilege escalation). |
| Azure Kubernetes Service RBAC Writer | Allows read/write access to most objects in a namespace. Doesn't allow viewing or modifying roles, or role bindings. Allows accessing `Secrets` and running pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. |
| Azure Kubernetes Service RBAC Admin | Allows admin access, intended to be granted within a namespace. Allows read/write access to most resources in a namespace (or cluster scope), including the ability to create roles and role bindings within the namespace. Doesn't allow write access to resource quota or to the namespace itself. |
| Azure Kubernetes Service RBAC Cluster Admin | Allows super-user access to perform any action on any resource. Gives full control over every resource in the cluster and in all namespaces. |

## Microsoft Entra integration

Enhance your AKS cluster security with Microsoft Entra integration. Built on decades of enterprise identity management, Microsoft Entra ID is a multi-tenant, cloud-based directory and identity management service that combines core directory services, application access management, and identity protection. With Microsoft Entra ID, you can integrate on-premises identities into AKS clusters to provide a single source for account management and security.

With Microsoft Entra integrated AKS clusters, you can grant users or groups access to Kubernetes resources within a namespace or across the cluster.

- To obtain a
`kubectl`

configuration context, a user runs the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. - When a user interacts with the AKS cluster with
`kubectl`

, they're prompted to sign in with their Microsoft Entra credentials.

This approach provides a single source for user account management and password credentials. The user can only access the resources as defined by the cluster administrator.

Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/azure/active-directory/develop/v2-protocols-oidc). From inside of the Kubernetes cluster, [Webhook Token Authentication](https://kubernetes.io/docs/reference/access-authn-authz/authentication/#webhook-token-authentication) is used to verify authentication tokens. Webhook token authentication is configured and managed as part of the AKS cluster.

### Webhook and API server

As shown in the graphic above, the API server calls the AKS webhook server and performs the following steps:

`kubectl`

uses the Microsoft Entra client application to sign in users with[OAuth 2.0 device authorization grant flow](/en-us/azure/active-directory/develop/v2-oauth2-device-code).- Microsoft Entra ID provides an access_token, id_token, and a refresh_token.
- The user makes a request to
`kubectl`

with an access_token from`kubeconfig`

. `kubectl`

sends the access_token to API Server.- The API Server is configured with the Auth WebHook Server to perform validation.
- The authentication webhook server confirms the JSON Web Token signature is valid by checking the Microsoft Entra public signing key.
- If the user is a member of more than 200 groups, the server application uses user-provided credentials to query group memberships of the logged-in user from the MS Graph API. For users with group memberships of 200 or fewer the groups claim already exists in the client token. No query will be performed.
- A response is sent to the API Server with user information such as the user principal name (UPN) claim of the access token, and the group membership of the user based on the object ID.
- The API performs an authorization decision based on the Kubernetes Role/RoleBinding.
- Once authorized, the API server returns a response to
`kubectl`

. `kubectl`

provides feedback to the user.

Learn how to integrate AKS with Microsoft Entra ID with our [AKS-managed Microsoft Entra integration how-to guide](managed-azure-ad).

## AKS service permissions

When creating a cluster, AKS generates or modifies resources it needs (like VMs and NICs) to create and run the cluster on behalf of the user. This identity is distinct from the cluster's identity permission, which is created during cluster creation.

### Identity creating and operating the cluster permissions

The following permissions are needed by the identity creating and operating the cluster.

| Permission | Reason |
|---|---|
`Microsoft.Compute/diskEncryptionSets/read` |
Required to read disk encryption set ID. |
`Microsoft.Compute/proximityPlacementGroups/write` |
Required for updating proximity placement groups. |
`Microsoft.Network/applicationGateways/read` `Microsoft.Network/applicationGateways/write` `Microsoft.Network/virtualNetworks/subnets/join/action` |
Required to configure application gateways and join the subnet. |
`Microsoft.Network/virtualNetworks/subnets/join/action` |
Required to configure the Network Security Group for the subnet when using a custom VNET. |
`Microsoft.Network/publicIPAddresses/join/action` `Microsoft.Network/publicIPPrefixes/join/action` |
Required to configure the outbound public IPs on the Standard Load Balancer. |
`Microsoft.OperationalInsights/workspaces/sharedkeys/read` `Microsoft.OperationalInsights/workspaces/read` `Microsoft.OperationsManagement/solutions/write` `Microsoft.OperationsManagement/solutions/read` `Microsoft.ManagedIdentity/userAssignedIdentities/assign/action` |
Required to create and update Log Analytics workspaces and Azure monitoring for containers. |
`Microsoft.Network/virtualNetworks/joinLoadBalancer/action` |
Required to configure the IP-based Load Balancer Backend Pools. |

### AKS cluster identity permissions

The following permissions are used by the AKS cluster identity, which is created and associated with the AKS cluster. Each permission is used for the reasons below:

| Permission | Reason |
|---|---|
`Microsoft.ContainerService/managedClusters/*` |
Required for creating users and operating the cluster |
`Microsoft.Network/loadBalancers/delete` `Microsoft.Network/loadBalancers/read` `Microsoft.Network/loadBalancers/write` |
Required to configure the load balancer for a LoadBalancer service. |
`Microsoft.Network/publicIPAddresses/delete` `Microsoft.Network/publicIPAddresses/read` `Microsoft.Network/publicIPAddresses/write` |
Required to find and configure public IPs for a LoadBalancer service. |
`Microsoft.Network/publicIPAddresses/join/action` |
Required for configuring public IPs for a LoadBalancer service. |
`Microsoft.Network/networkSecurityGroups/read` `Microsoft.Network/networkSecurityGroups/write` |
Required to create or delete security rules for a LoadBalancer service. |
`Microsoft.Compute/disks/delete` `Microsoft.Compute/disks/read` `Microsoft.Compute/disks/write` `Microsoft.Compute/locations/DiskOperations/read` |
Required to configure AzureDisks. |
`Microsoft.Storage/storageAccounts/delete` `Microsoft.Storage/storageAccounts/listKeys/action` `Microsoft.Storage/storageAccounts/read` `Microsoft.Storage/storageAccounts/write` `Microsoft.Storage/operations/read` |
Required to configure storage accounts for AzureFile or AzureDisk. |
`Microsoft.Network/routeTables/read` `Microsoft.Network/routeTables/routes/delete` `Microsoft.Network/routeTables/routes/read` `Microsoft.Network/routeTables/routes/write` `Microsoft.Network/routeTables/write` |
Required to configure route tables and routes for nodes. |
`Microsoft.Compute/virtualMachines/read` |
Required to find information for virtual machines in a VMAS, such as zones, fault domain, size, and data disks. |
`Microsoft.Compute/virtualMachines/write` |
Required to attach AzureDisks to a virtual machine in a VMAS. |
`Microsoft.Compute/virtualMachineScaleSets/read` `Microsoft.Compute/virtualMachineScaleSets/virtualMachines/read` `Microsoft.Compute/virtualMachineScaleSets/virtualmachines/instanceView/read` |
Required to find information for virtual machines in a virtual machine scale set, such as zones, fault domain, size, and data disks. |
`Microsoft.Network/networkInterfaces/write` |
Required to add a virtual machine in a VMAS to a load balancer backend address pool. |
`Microsoft.Compute/virtualMachineScaleSets/write` |
Required to add a virtual machine scale set to a load balancer backend address pools and scale out nodes in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/delete` |
Required to delete a virtual machine scale set to a load balancer backend address pools and scale down nodes in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/virtualmachines/write` |
Required to attach AzureDisks and add a virtual machine from a virtual machine scale set to the load balancer. |
`Microsoft.Network/networkInterfaces/read` |
Required to search internal IPs and load balancer backend address pools for virtual machines in a VMAS. |
`Microsoft.Compute/virtualMachineScaleSets/virtualMachines/networkInterfaces/read` |
Required to search internal IPs and load balancer backend address pools for a virtual machine in a virtual machine scale set. |
`Microsoft.Compute/virtualMachineScaleSets/virtualMachines/networkInterfaces/ipconfigurations/publicipaddresses/read` |
Required to find public IPs for a virtual machine in a virtual machine scale set. |
`Microsoft.Network/virtualNetworks/read` `Microsoft.Network/virtualNetworks/subnets/read` |
Required to verify if a subnet exists for the internal load balancer in another resource group. |
`Microsoft.Compute/snapshots/delete` `Microsoft.Compute/snapshots/read` `Microsoft.Compute/snapshots/write` |
Required to configure snapshots for AzureDisk. |
`Microsoft.Compute/locations/vmSizes/read` `Microsoft.Compute/locations/operations/read` |
Required to find virtual machine sizes for finding AzureDisk volume limits. |

### Additional cluster identity permissions

When creating a cluster with specific attributes, you will need the following additional permissions for the cluster identity. Since these permissions are not automatically assigned, you must add them to the cluster identity after it's created.

| Permission | Reason |
|---|---|
`Microsoft.Network/networkSecurityGroups/write` `Microsoft.Network/networkSecurityGroups/read` |
Required if using a network security group in another resource group. Required to configure security rules for a LoadBalancer service. |
`Microsoft.Network/virtualNetworks/subnets/read` `Microsoft.Network/virtualNetworks/subnets/join/action` |
Required if using a subnet in another resource group such as a custom VNET. |
`Microsoft.Network/routeTables/routes/read` `Microsoft.Network/routeTables/routes/write` |
Required if using a subnet associated with a route table in another resource group such as a custom VNET with a custom route table. Required to verify if a subnet already exists for the subnet in the other resource group. |
`Microsoft.Network/virtualNetworks/subnets/read` |
Required if using an internal load balancer in another resource group. Required to verify if a subnet already exists for the internal load balancer in the resource group. |
`Microsoft.Network/privatednszones/*` |
Required if using a private DNS zone in another resource group such as a custom privateDNSZone. |

## AKS Node Access

By default Node Access is not required for AKS. The following access is needed for the node if a specific component is leveraged.

| Access | Reason |
|---|---|
`kubelet` |
Required to grant MSI access to ACR. |
`http app routing` |
Required for write permission to "random name".aksapp.io. |
`container insights` |
Required to grant permission to the Log Analytics workspace. |

## Summary

View the table for a quick summary of how users can authenticate to Kubernetes when Microsoft Entra integration is enabled. In all cases, the user's sequence of commands is:

Run

`az login`

to authenticate to Azure.Run

`az aks get-credentials`

to download credentials for the cluster into`.kube/config`

.Run

`kubectl`

commands.- The first command may trigger browser-based authentication to authenticate to the cluster, as described in the following table.


In the Azure portal, you can find:

- The
*Role Grant*(Azure RBAC role grant) referred to in the second column is shown on the**Access Control**tab. - The Cluster Admin Microsoft Entra group is shown on the
**Configuration**tab.- Also found with parameter name
`--aad-admin-group-object-ids`

in the Azure CLI.

- Also found with parameter name

| Description | Role grant required | Cluster admin Microsoft Entra group(s) | When to use |
|---|---|---|---|
| Legacy admin login using client certificate | Azure Kubernetes Service Cluster Admin Role. This role allows `az aks get-credentials` to be used with the `--admin` flag, which downloads a
`.kube/config` . This is the only purpose of "Azure Kubernetes Service Cluster Admin Role". |
n/a | If you're permanently blocked by not having access to a valid Microsoft Entra group with access to your cluster. |
| Microsoft Entra ID with manual (Cluster)RoleBindings | Azure Kubernetes Service Cluster User Role. The "User" role allows `az aks get-credentials` to be used without the `--admin` flag. (This is the only purpose of "Azure Kubernetes Service Cluster User Role".) The result, on a Microsoft Entra ID-enabled cluster, is the download of
`.kube/config` , which triggers browser-based authentication when it's first used by `kubectl` . |
User is not in any of these groups. Because the user is not in any Cluster Admin groups, their rights will be controlled entirely by any RoleBindings or ClusterRoleBindings that have been set up by cluster admins. The (Cluster)RoleBindings
`subjects` . If no such bindings have been set up, the user will not be able to excute any `kubectl` commands. |

`cluster-admin`

Kubernetes role. So users in these groups can run all `kubectl`

commands as `cluster-admin`

.*not*using Azure RBAC for Kubernetes authorization.First,

**Azure Kubernetes Service Cluster User Role**(as above).Second, one of the "Azure Kubernetes Service

**RBAC**..." roles listed above, or your own custom alternative.## Next steps

- To get started with Microsoft Entra ID and Kubernetes RBAC, see
[Integrate Microsoft Entra ID with AKS](managed-azure-ad). - For associated best practices, see
[Best practices for authentication and authorization in AKS](operator-best-practices-identity). - To get started with Azure RBAC for Kubernetes Authorization, see
[Use Azure RBAC to authorize access within the Azure Kubernetes Service (AKS) Cluster](manage-azure-rbac). - To get started securing your
`kubeconfig`

file, see[Limit access to cluster configuration file](control-kubeconfig-access). - To get started with managed identities in AKS, see
[Use a managed identity in AKS](use-managed-identity).

For more information on core Kubernetes and AKS concepts, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-disruption -->

# Configure node disruption policies for node auto-provisioning (NAP) nodes in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure node disruption policies for Azure Kubernetes Service (AKS) node auto-provisioning (NAP) nodes and details how disruption works to optimize resource utilization and cost efficiency.

NAP optimizes your cluster by:

- Removing or replacing underutilized nodes.
- Consolidating workloads to reduce costs.
- Respecting disruption budgets and maintenance windows.
- Providing manual control when needed.

## Before you begin

- Read the
[Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning)article, which details[how NAP works](node-auto-provisioning#how-does-node-auto-provisioning-work). - Read the
[Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning-networking).

## How does node disruption work for NAP nodes?

Karpenter sets a Kubernetes [finalizer](https://kubernetes.io/docs/concepts/overview/working-with-objects/finalizers/) on each node and node claim it provisions. The finalizer blocks the deletion of the node object, while the Termination Controller taints and drains the node before removing the underlying node claim.

When the workloads on your nodes scale down, NAP uses disruption rules on the node pool specification to decide when and how to remove those nodes and potentially reschedule your workloads for efficiency.

## Node disruption methods

NAP automatically discovers nodes eligible for disruption and spins up replacements when needed. You can trigger disruption through automated methods like *Expiration*, *Consolidation*, and *Drift*, manual methods, or external systems.

## Expiration

Expiration allows you to set a maximum age for your NAP nodes. Nodes are marked as expired and disrupted after reaching the age you specify for the node pool's `spec.disruption.expireAfter`

value.

### Example expiration configuration

The following example shows how to set the expiration time for NAP nodes to 24 hours:

```
spec:
disruption:
expireAfter: 24h # Expire nodes after 24 hours
```


## Consolidation

NAP works to actively reduce cluster cost by identifying when nodes can be removed because they're empty or underutilized, or when nodes can be replaced with lower priced variants. This process is called *Consolidation*. NAP primarily uses Consolidation to delete or replace nodes for optimal pod placement.

NAP performs the following types of consolidation in order to optimize resource utilization:

**Empty node consolidation**: Deletes any empty nodes in parallel.**Multi-node consolidation**: Deletes multiple nodes, possibly launching a single replacement.**Single-node consolidation**: Deletes any single node, possibly launching a replacement.

You can trigger consolidation through the `spec.disruption.consolidationPolicy`

field in the node pool specification using the `WhenEmpty`

, or `WhenEmptyOrUnderUtilized`

settings. You can also set the `consolidateAfter`

field, which is a time-based condition that determines how long NAP waits after discovering a consolidation opportunity before disrupting the node.

### Example consolidation configuration

The following example shows how to configure NAP to consolidate nodes when they're empty, and to wait 30 seconds after discovering a consolidation opportunity before disrupting the node:

```
disruption:
# Describes which types of nodes NAP should consider for consolidation
# `WhenEmptyOrUnderUtilized`: NAP considers all nodes for consolidation and attempts to remove or replace nodes when it discovers that the node is empty or underutilized and could be changed to reduce cost
# `WhenEmpty`: NAP only considers nodes for consolidation that don't contain any workload pods
consolidationPolicy: WhenEmpty
# The amount of time NAP should wait after discovering a consolidation decision
# Currently, you can only set this value when the consolidation policy is `WhenEmpty`
# You can choose to disable consolidation entirely by setting the string value `Never`
consolidateAfter: 30s
```


## Drift

Drift handles changes to the `NodePool`

/`AKSNodeClass`

resources. Values in the `NodeClaimTemplateSpec`

/`AKSNodeClassSpec`

are reflected in the same way that they're set. A `NodeClaim`

is detected as *drifted* if the values in the associated `NodePool`

/`AKSNodeClass`

don't match the values in the `NodeClaim`

. Similar to the upstream `deployment.spec.template`

relationship to pods, Karpenter annotates the associated `NodePool`

/`AKSNodeClass`

with a hash of the `NodeClaimTemplateSpec`

to check for drift. Karpenter removes the `Drifted`

status condition in the following scenarios:

- The
`Drift`

feature gate isn't enabled but the`NodeClaim`

is drifted. - The
`NodeClaim`

isn't drifted, but has the status condition.

Karpenter or the cloud provider interface might discover [special cases](#special-cases-on-drift) triggered by `NodeClaim`

/`Instance`

/`NodePool`

/`AKSNodeClass`

changes.

### Special cases on drift

In special cases, drift can correspond to multiple values and must be handled differently. Drift on resolved fields can create cases where drift occurs without changes to Custom Resource Definitions (CRDs), or where CRD changes don't result in drift.

For example, if a `NodeClaim`

has `node.kubernetes.io/instance-type: Standard_D2s_v3`

, and requirements change from `node.kubernetes.io/instance-type In [Standard_D2s_v3]`

to `node.kubernetes.io/instance-type In [Standard_D2s_v3, Standard_D4s_v3]`

, the `NodeClaim`

isn't drifted because its value is still compatible with the new requirements. Conversely, if a `NodeClaim`

uses a `NodeClaim`

`imageFamily`

, but the `spec.imageFamily`

field changes, Karpenter detects the `NodeClaim`

as *drifted* and rotates the node to meet that specification.

Important

Karpenter monitors subnet configuration changes and detects drift when the `vnetSubnetID`

in an `AKSNodeClass`

is modified. Understanding this behavior is critical when managing custom networking configurations. For more information, see [Subnet drift behavior](node-auto-provisioning-networking#subnet-drift-behavior).

For more information, see [Drift Design](https://github.com/aws/karpenter-core/blob/main/designs/drift.md).

## Termination grace period

You can set a termination grace period for NAP nodes using the `spec.template.spec.terminationGracePeriod`

field in the node pool specification. This setting allows you to configure how long Karpenter waits for pods to terminate gracefully. This setting takes precedence over a pod's `terminationGracePeriodSeconds`

and bypasses `PodDisruptionBudgets`

and the `karpenter.sh/do-not-disrupt`

annotation.

### Example termination grace period configuration

The following example shows how to set a termination grace period of 30 seconds for NAP nodes:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
spec:
terminationGracePeriod: 30s
```


## Disruption budgets

You can rate limit Karpenter's disruption by modifying the `spec.disruption.budgets`

field in the node pool specification. If you leave this setting undefined, Karpenter defaults to one budget with `nodes: 10%`

. Budgets consider nodes that are being deleted for any reason, and they only block Karpenter from voluntary disruptions through expiration, drift, emptiness, and consolidation.

When calculating if a budget blocks nodes from disruption, Karpenter counts the total nodes owned by a node pool and then subtracts nodes that are being deleted and nodes that are `NotReady`

. If the budget is configured with a percentage value, such as `20%`

, Karpenter calculates the number of allowed disruptions as `allowed_disruptions = roundup(total * percentage) - total_deleting - total_notready`

. For multiple budgets in a node pool, Karpenter takes the minimum (most restrictive) value of each of the budgets.

### Schedule and duration fields

When using budgets, you can optionally set the `schedule`

and `duration`

fields to create time-based budgets. These fields allow you to define maintenance windows or specific timeframes when disruption limits are stricter.

**Schedule**uses cron job syntax with special macros like`@yearly`

,`@monthly`

,`@weekly`

,`@daily`

,`@hourly`

.**Duration**allows compound durations like`10h5m`

,`30m`

, or`160h`

. Duration and Schedule must be defined together.

#### Schedule and duration examples

##### Maintenance window budget

Prevent disruptions during business hours:

```
budgets:
- nodes: "0"
schedule: "0 9 * * 1-5" # 9 AM Monday-Friday
duration: 8h # For 8 hours
```


##### Weekend-only disruptions

Only allow disruptions on weekends:

```
budgets:
- nodes: "50%"
schedule: "0 0 * * 6" # Saturday midnight
duration: 48h # All weekend
- nodes: "0" # Block all other times
```


##### Gradual rollout budget

Allow increasing disruption rates:

```
budgets:
- nodes: "1"
schedule: "0 2 * * *" # 2 AM daily
duration: 2h
- nodes: "3"
schedule: "0 4 * * *" # 4 AM daily
duration: 4h
```


### Budget configuration examples

The following `NodePool`

specification has three budgets configured:

- The first budget allows 20% of nodes owned by the node pool to be disrupted at once.
- The second budget acts as a ceiling, only allowing five disruptions when there are more than 25 nodes.
- The last budget blocks disruptions during the first 10 minutes of each day.

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
disruption:
consolidationPolicy: WhenEmptyOrUnderutilized
expireAfter: 720h # 30 * 24h = 720h
budgets:
- nodes: "20%" # Allow 20% of nodes to be disrupted
- nodes: "5" # Cap at maximum 5 nodes
- nodes: "0" # Block all disruptions during maintenance window
schedule: "@daily" # Scheduled daily
duration: 10m # Duration of 10 minutes
```


## Manual node disruption

You can manually disrupt NAP nodes using `kubectl`

or by deleting `NodePool`

resources.

### Remove nodes with kubectl

You can manually remove nodes using the `kubectl delete node`

command. You can delete specific nodes, all NAP-managed nodes, or nodes from a specific node pool by using labels, for example:

```
# Delete a specific node
kubectl delete node $NODE_NAME
# Delete all NAP-managed nodes
kubectl delete nodes -l karpenter.sh/nodepool
# Delete nodes from a specific nodepool
kubectl delete nodes -l karpenter.sh/nodepool=$NODEPOOL_NAME
```


### Delete `NodePool`

resources

The `NodePool`

owns `NodeClaims`

through an owner reference. NAP gracefully terminates nodes through cascading deletion when you delete the associated `NodePool`

.

## Control disruption using annotations

You can block or disable disruption for specific pods, nodes, or entire node pools using annotations.

### Pod controls

Block NAP from disrupting certain pods by setting the `karpenter.sh/do-not-disrupt: "true"`

annotation:

```
apiVersion: apps/v1
kind: Deployment
spec:
template:
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


This annotation prevents voluntary disruption for Expiration, Consolidation, and Drift. However, it doesn't prevent disruption from external systems or manual disruption through `kubectl`

or `NodePool`

deletion.

### Node controls

Block NAP from disrupting specific nodes:

```
apiVersion: v1
kind: Node
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


### Node pool controls

Disable disruption for all nodes in a `NodePool`

:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
metadata:
annotations:
karpenter.sh/do-not-disrupt: "true"
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ssh -->

# Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you eventually need to directly access an AKS node. This access could be for maintenance, log collection, or troubleshooting operations.

You access a node through authentication, which methods vary depending on your Node OS and method of connection. You securely authenticate against AKS Linux and Windows nodes through two options discussed in this article. One requires that you have Kubernetes API access, and the other is through the AKS ARM API, which provides direct private IP information. For security reasons, AKS nodes aren't exposed to the internet. Instead, to connect directly to any AKS nodes, you need to use either `kubectl debug`

or the host's private IP address.

## Access nodes using the Kubernetes API

This method requires usage of `kubectl debug`

command.

### Before you begin

This guide shows you how to create a connection to an AKS node and update the SSH key of your AKS cluster. To follow along the steps, you need to use Azure CLI that supports version 2.0.64 or later. Run `az --version`

to check the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Complete these steps if you don't have an SSH key. Create an SSH key depending on your Node OS Image, for [macOS and Linux](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys), or [Windows](/en-us/azure/virtual-machines/linux/ssh-from-windows). Make sure you save the key pair in the OpenSSH format, avoid unsupported formats such as `.ppk`

. Next, refer to [Manage SSH configuration](manage-ssh-node-access) to add the key to your cluster.

### Linux and macOS

Linux and macOS users can access their node using `kubectl debug`

or their private IP Address. Windows users should skip to the Windows Server Proxy section for a workaround to SSH via proxy.

#### Connect using kubectl debug

To create an interactive shell connection, use the `kubectl debug`

command to run a privileged container on your node.

To list your nodes, use the

`kubectl get nodes`

command:`kubectl get nodes -o wide`

Sample output:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE aks-nodepool1-37663765-vmss000000 Ready agent 166m v1.25.6 10.224.0.33 <none> Ubuntu 22.04.2 LTS aks-nodepool1-37663765-vmss000001 Ready agent 166m v1.25.6 10.224.0.4 <none> Ubuntu 22.04.2 LTS aksnpwin000000 Ready agent 160m v1.25.6 10.224.0.62 <none> Windows Server 2022 Datacenter`

Use the

`kubectl debug`

command to start a privileged container on your node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

You now have access to the node through a privileged container as a debugging pod.

Note

You can interact with the node session by running

`chroot /host`

from the privileged container.

#### Exit kubectl debug mode

When you're done with your node, enter the `exit`

command to end the interactive shell session. After the interactive container session closes, delete the debugging pod used with `kubectl delete pod`

.

```
kubectl delete pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx
```


### Windows Server proxy connection for SSH

Follow these steps as a workaround to connect with SSH on a Windows Server node.

#### Create a proxy server

At this time, you can't connect to a Windows Server node directly by using `kubectl debug`

. Instead, you need to first connect to another node in the cluster with `kubectl`

, then connect to the Windows Server node from that node using SSH.

To connect to another node in the cluster, use the `kubectl debug`

command. For more information, follow the above steps in the kubectl section. Create an SSH connection to the Windows Server node from another node using the SSH keys provided when you created the AKS cluster and the internal IP address of the Windows Server node.

Important

The following steps for creating the SSH connection to the Windows Server node from another node can only be used if you created your AKS cluster using the Azure CLI with the `--generate-ssh-keys`

parameter. If you want to use your own SSH keys instead, you can use the `az aks update`

to manage SSH keys on an existing AKS cluster. For more information, see [manage SSH node access](manage-ssh-node-access).

Note

If your Linux proxy node is down or unresponsive, use the [Azure Bastion](/en-us/azure/bastion/bastion-overview) method to connect instead.

Use the

`kubectl debug`

command to start a privileged container on your proxy (Linux) node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

Open a new terminal window and use the

`kubectl get pods`

command to get the name of the pod started by`kubectl debug`

.`kubectl get pods`

Sample output:

`NAME READY STATUS RESTARTS AGE node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 1/1 Running 0 21s`

In the sample output,

*node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx*is the name of the pod started by`kubectl debug`

.Use the

`kubectl port-forward`

command to open a connection to the deployed pod:`kubectl port-forward node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 2022:22`

Sample output:

`Forwarding from 127.0.0.1:2022 -> 22 Forwarding from [::1]:2022 -> 22`

The previous example begins forwarding network traffic from port

`2022`

on your development computer to port`22`

on the deployed pod. When using`kubectl port-forward`

to open a connection and forward network traffic, the connection remains open until you stop the`kubectl port-forward`

command.Open a new terminal and run the command

`kubectl get nodes`

to show the internal IP address of the Windows Server node:`kubectl get no -o custom-columns=NAME:metadata.name,'INTERNAL_IP:status.addresses[?(@.type == \"InternalIP\")].address'`

Sample output:

`NAME INTERNAL_IP aks-nodepool1-19409214-vmss000003 10.224.0.8`

In the previous example,

*10.224.0.62*is the internal IP address of the Windows Server node.Create an SSH connection to the Windows Server node using the internal IP address, and connect to port

`22`

through port`2022`

on your development computer. The default username for AKS nodes is*azureuser*. Accept the prompt to continue with the connection. You're then provided with the bash prompt of your Windows Server node:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' azureuser@10.224.0.62`

Sample output:

`The authenticity of host '10.224.0.62 (10.224.0.62)' can't be established. ECDSA key fingerprint is SHA256:1234567890abcdefghijklmnopqrstuvwxyzABCDEFG. Are you sure you want to continue connecting (yes/no)? yes`

Note

If you prefer to use password authentication, include the parameter

`-o PreferredAuthentications=password`

. For example:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' -o PreferredAuthentications=password azureuser@10.224.0.62`


## Use a host process container to access Windows node

Run the following script to create

`hostprocess.yaml`

. In the script, replace`AKSWINDOWSNODENAME`

with the AKS Windows node name.This specification uses the nanoserver base image. The base image doesn't have PowerShell, but because it runs as a host process container (HPC), PowerShell is available in the underlying VM.

`apiVersion: v1 kind: Pod metadata: labels: pod: hpc name: hpc spec: securityContext: windowsOptions: hostProcess: true runAsUserName: "NT AUTHORITY\\SYSTEM" hostNetwork: true containers: - name: hpc image: mcr.microsoft.com/windows/nanoserver:ltsc2022 # Use nanoserver:1809 for WS2019 command: - powershell.exe - -Command - "Start-Sleep 2147483" imagePullPolicy: IfNotPresent nodeSelector: kubernetes.io/os: windows kubernetes.io/hostname: AKSWINDOWSNODENAME tolerations: - effect: NoSchedule key: node.kubernetes.io/unschedulable operator: Exists - effect: NoSchedule key: node.kubernetes.io/network-unavailable operator: Exists - effect: NoExecute key: node.kubernetes.io/unreachable operator: Exists`

Run

`kubectl apply -f hostprocess.yaml`

to deploy the Windows HPC in the specified Windows node.Use

`kubectl exec -it [HPC-POD-NAME] -- powershell`

.You can run any PowerShell commands inside the HPC container to access the Windows node.


Note

You need to switch the root folder to `C:\`

inside the HPC container to access the files in the Windows node.

## SSH using Azure Bastion for Windows

If your Linux proxy node isn't reachable, using Azure Bastion as a proxy is an alternative. This method requires that you set up an Azure Bastion host for the virtual network in which the cluster resides. See [Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview) for more details.

## SSH using private IPs from the AKS API

If you don't have access to the Kubernetes API, you can get access to properties such as `Node IP`

and `Node Name`

through the [AKS agent pool API ](/en-us/rest/api/aks/agent-pools/get#agentpool), (available on stable versions `07-01-2024`

or above) to connect to AKS nodes.

### Create an interactive shell connection to a node using the IP address

For convenience, AKS nodes are exposed on the cluster's virtual network through private IP addresses. However, you need to be in the cluster's virtual network to SSH into the node. If you don't already have an environment configured, you can use [Azure Bastion](/en-us/azure/bastion/bastion-connect-vm-ssh-linux) to establish a proxy from which you can SSH to cluster nodes. Make sure the Azure Bastion is deployed in the same virtual network as the cluster.

Obtain private IPs using the

`az aks machine list`

command, targeting all the VMs in a specific node pool with the`--nodepool-name`

flag.`az aks machine list --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name nodepool1 -o table`

The following example output shows the internal IP addresses of all the nodes in the node pool:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4 aks-nodepool1-33555069-vmss000001 10.224.0.6 IPv4 aks-nodepool1-33555069-vmss000002 10.224.0.4 IPv4`

To target a specific node inside the node pool, use the

`--machine-name`

flag:`az aks machine show --cluster-name myAKScluster --nodepool-name nodepool1 -g myResourceGroup --machine-name aks-nodepool1-33555069-vmss000000 -o table`

The following example output shows the internal IP address of all the specified node:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4`

SSH to the node using the private IP address you obtained in the previous step. This step is applicable for Linux machines only. For Windows machines, see

[Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview).`ssh -i /path/to/private_key.pem azureuser@10.224.0.33`


## Next steps

If you need more troubleshooting data, you can [view the kubelet logs](kubelet-logs) or [view the Kubernetes control plane logs](monitor-aks-reference#resource-logs).

To learn about managing your SSH keys, see [Manage SSH configuration](manage-ssh-node-access).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-access -->

# Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you eventually need to directly access an AKS node. This access could be for maintenance, log collection, or troubleshooting operations.

You access a node through authentication, which methods vary depending on your Node OS and method of connection. You securely authenticate against AKS Linux and Windows nodes through two options discussed in this article. One requires that you have Kubernetes API access, and the other is through the AKS ARM API, which provides direct private IP information. For security reasons, AKS nodes aren't exposed to the internet. Instead, to connect directly to any AKS nodes, you need to use either `kubectl debug`

or the host's private IP address.

## Access nodes using the Kubernetes API

This method requires usage of `kubectl debug`

command.

### Before you begin

This guide shows you how to create a connection to an AKS node and update the SSH key of your AKS cluster. To follow along the steps, you need to use Azure CLI that supports version 2.0.64 or later. Run `az --version`

to check the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Complete these steps if you don't have an SSH key. Create an SSH key depending on your Node OS Image, for [macOS and Linux](/en-us/azure/virtual-machines/linux/mac-create-ssh-keys), or [Windows](/en-us/azure/virtual-machines/linux/ssh-from-windows). Make sure you save the key pair in the OpenSSH format, avoid unsupported formats such as `.ppk`

. Next, refer to [Manage SSH configuration](manage-ssh-node-access) to add the key to your cluster.

### Linux and macOS

Linux and macOS users can access their node using `kubectl debug`

or their private IP Address. Windows users should skip to the Windows Server Proxy section for a workaround to SSH via proxy.

#### Connect using kubectl debug

To create an interactive shell connection, use the `kubectl debug`

command to run a privileged container on your node.

To list your nodes, use the

`kubectl get nodes`

command:`kubectl get nodes -o wide`

Sample output:

`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE aks-nodepool1-37663765-vmss000000 Ready agent 166m v1.25.6 10.224.0.33 <none> Ubuntu 22.04.2 LTS aks-nodepool1-37663765-vmss000001 Ready agent 166m v1.25.6 10.224.0.4 <none> Ubuntu 22.04.2 LTS aksnpwin000000 Ready agent 160m v1.25.6 10.224.0.62 <none> Windows Server 2022 Datacenter`

Use the

`kubectl debug`

command to start a privileged container on your node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

You now have access to the node through a privileged container as a debugging pod.

Note

You can interact with the node session by running

`chroot /host`

from the privileged container.

#### Exit kubectl debug mode

When you're done with your node, enter the `exit`

command to end the interactive shell session. After the interactive container session closes, delete the debugging pod used with `kubectl delete pod`

.

```
kubectl delete pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx
```


### Windows Server proxy connection for SSH

Follow these steps as a workaround to connect with SSH on a Windows Server node.

#### Create a proxy server

At this time, you can't connect to a Windows Server node directly by using `kubectl debug`

. Instead, you need to first connect to another node in the cluster with `kubectl`

, then connect to the Windows Server node from that node using SSH.

To connect to another node in the cluster, use the `kubectl debug`

command. For more information, follow the above steps in the kubectl section. Create an SSH connection to the Windows Server node from another node using the SSH keys provided when you created the AKS cluster and the internal IP address of the Windows Server node.

Important

The following steps for creating the SSH connection to the Windows Server node from another node can only be used if you created your AKS cluster using the Azure CLI with the `--generate-ssh-keys`

parameter. If you want to use your own SSH keys instead, you can use the `az aks update`

to manage SSH keys on an existing AKS cluster. For more information, see [manage SSH node access](manage-ssh-node-access).

Note

If your Linux proxy node is down or unresponsive, use the [Azure Bastion](/en-us/azure/bastion/bastion-overview) method to connect instead.

Use the

`kubectl debug`

command to start a privileged container on your proxy (Linux) node and connect to it.`kubectl debug node/aks-nodepool1-37663765-vmss000000 -it --image=mcr.microsoft.com/cbl-mariner/busybox:2.0`

Sample output:

`Creating debugging pod node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx with container debugger on node aks-nodepool1-37663765-vmss000000. If you don't see a command prompt, try pressing enter. root@aks-nodepool1-37663765-vmss000000:/#`

Open a new terminal window and use the

`kubectl get pods`

command to get the name of the pod started by`kubectl debug`

.`kubectl get pods`

Sample output:

`NAME READY STATUS RESTARTS AGE node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 1/1 Running 0 21s`

In the sample output,

*node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx*is the name of the pod started by`kubectl debug`

.Use the

`kubectl port-forward`

command to open a connection to the deployed pod:`kubectl port-forward node-debugger-aks-nodepool1-37663765-vmss000000-bkmmx 2022:22`

Sample output:

`Forwarding from 127.0.0.1:2022 -> 22 Forwarding from [::1]:2022 -> 22`

The previous example begins forwarding network traffic from port

`2022`

on your development computer to port`22`

on the deployed pod. When using`kubectl port-forward`

to open a connection and forward network traffic, the connection remains open until you stop the`kubectl port-forward`

command.Open a new terminal and run the command

`kubectl get nodes`

to show the internal IP address of the Windows Server node:`kubectl get no -o custom-columns=NAME:metadata.name,'INTERNAL_IP:status.addresses[?(@.type == \"InternalIP\")].address'`

Sample output:

`NAME INTERNAL_IP aks-nodepool1-19409214-vmss000003 10.224.0.8`

In the previous example,

*10.224.0.62*is the internal IP address of the Windows Server node.Create an SSH connection to the Windows Server node using the internal IP address, and connect to port

`22`

through port`2022`

on your development computer. The default username for AKS nodes is*azureuser*. Accept the prompt to continue with the connection. You're then provided with the bash prompt of your Windows Server node:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' azureuser@10.224.0.62`

Sample output:

`The authenticity of host '10.224.0.62 (10.224.0.62)' can't be established. ECDSA key fingerprint is SHA256:1234567890abcdefghijklmnopqrstuvwxyzABCDEFG. Are you sure you want to continue connecting (yes/no)? yes`

Note

If you prefer to use password authentication, include the parameter

`-o PreferredAuthentications=password`

. For example:`ssh -o 'ProxyCommand ssh -p 2022 -W %h:%p azureuser@127.0.0.1' -o PreferredAuthentications=password azureuser@10.224.0.62`


## Use a host process container to access Windows node

Run the following script to create

`hostprocess.yaml`

. In the script, replace`AKSWINDOWSNODENAME`

with the AKS Windows node name.This specification uses the nanoserver base image. The base image doesn't have PowerShell, but because it runs as a host process container (HPC), PowerShell is available in the underlying VM.

`apiVersion: v1 kind: Pod metadata: labels: pod: hpc name: hpc spec: securityContext: windowsOptions: hostProcess: true runAsUserName: "NT AUTHORITY\\SYSTEM" hostNetwork: true containers: - name: hpc image: mcr.microsoft.com/windows/nanoserver:ltsc2022 # Use nanoserver:1809 for WS2019 command: - powershell.exe - -Command - "Start-Sleep 2147483" imagePullPolicy: IfNotPresent nodeSelector: kubernetes.io/os: windows kubernetes.io/hostname: AKSWINDOWSNODENAME tolerations: - effect: NoSchedule key: node.kubernetes.io/unschedulable operator: Exists - effect: NoSchedule key: node.kubernetes.io/network-unavailable operator: Exists - effect: NoExecute key: node.kubernetes.io/unreachable operator: Exists`

Run

`kubectl apply -f hostprocess.yaml`

to deploy the Windows HPC in the specified Windows node.Use

`kubectl exec -it [HPC-POD-NAME] -- powershell`

.You can run any PowerShell commands inside the HPC container to access the Windows node.


Note

You need to switch the root folder to `C:\`

inside the HPC container to access the files in the Windows node.

## SSH using Azure Bastion for Windows

If your Linux proxy node isn't reachable, using Azure Bastion as a proxy is an alternative. This method requires that you set up an Azure Bastion host for the virtual network in which the cluster resides. See [Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview) for more details.

## SSH using private IPs from the AKS API

If you don't have access to the Kubernetes API, you can get access to properties such as `Node IP`

and `Node Name`

through the [AKS agent pool API ](/en-us/rest/api/aks/agent-pools/get#agentpool), (available on stable versions `07-01-2024`

or above) to connect to AKS nodes.

### Create an interactive shell connection to a node using the IP address

For convenience, AKS nodes are exposed on the cluster's virtual network through private IP addresses. However, you need to be in the cluster's virtual network to SSH into the node. If you don't already have an environment configured, you can use [Azure Bastion](/en-us/azure/bastion/bastion-connect-vm-ssh-linux) to establish a proxy from which you can SSH to cluster nodes. Make sure the Azure Bastion is deployed in the same virtual network as the cluster.

Obtain private IPs using the

`az aks machine list`

command, targeting all the VMs in a specific node pool with the`--nodepool-name`

flag.`az aks machine list --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name nodepool1 -o table`

The following example output shows the internal IP addresses of all the nodes in the node pool:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4 aks-nodepool1-33555069-vmss000001 10.224.0.6 IPv4 aks-nodepool1-33555069-vmss000002 10.224.0.4 IPv4`

To target a specific node inside the node pool, use the

`--machine-name`

flag:`az aks machine show --cluster-name myAKScluster --nodepool-name nodepool1 -g myResourceGroup --machine-name aks-nodepool1-33555069-vmss000000 -o table`

The following example output shows the internal IP address of all the specified node:

`Name Ip Family --------------------------------- ----------- ----------- aks-nodepool1-33555069-vmss000000 10.224.0.5 IPv4`

SSH to the node using the private IP address you obtained in the previous step. This step is applicable for Linux machines only. For Windows machines, see

[Connect with Azure Bastion](/en-us/azure/bastion/bastion-overview).`ssh -i /path/to/private_key.pem azureuser@10.224.0.33`


## Next steps

If you need more troubleshooting data, you can [view the kubelet logs](kubelet-logs) or [view the Kubernetes control plane logs](monitor-aks-reference#resource-logs).

To learn about managing your SSH keys, see [Manage SSH configuration](manage-ssh-node-access).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-vulnerability-management -->

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
