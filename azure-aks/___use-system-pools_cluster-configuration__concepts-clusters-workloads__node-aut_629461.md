---
merged_at: 2026-01-26T23:04:05.995685
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-system-pools -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-configuration -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-clusters-workloads -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning -->

# Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including how it works, upgrade behavior, prerequisites, limitations, and resources to get started.

## What is node auto-provisioning in AKS?

When you deploy workloads onto AKS, you need to select the appropriate virtual machine (VM) size as part of your node pool configuration. As your workloads become more complex, you might have different workloads with varying resource requirements, which makes it more difficult to design your VM configuration for numerous resource requests.

Node auto-provisioning (NAP) simplifies this process by automatically provisioning and managing the optimal VM configuration for your workloads. NAP uses pending pod resource requirements to decide the optimal VM configuration to run your workloads in the most efficient and cost-effective manner.

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects.

## How does node auto-provisioning work?

Node auto-provisioning provisions, scales, and manages VMs (nodes) in a cluster in response to pending pod pressure.

### Key components of node auto-provisioning

NAP uses the following key components to help manage your cluster's nodes:

| Component | Description |
|---|---|
`NodePool` and `AKSNodeClass` |
Custom Resource Definitions (CRDs) that you create and manage to define node provisioning policies, VM specifications, and constraints for your workloads. |
`NodeClaims` |
Managed by NAP to represent the current state of provisioned nodes that you can monitor. |
| Workload resource requirements | CPU, memory, and other specifications from your Pods, Deployments, Jobs, and other Kubernetes resources that drive provisioning decisions. |

## Kubernetes upgrade behavior for node auto-provisioning nodes

Kubernetes upgrades for node auto-provisioning nodes follow the control plane Kubernetes version. If you perform a cluster upgrade, your nodes are automatically updated to follow the same versioning as your control plane.

We recommend setting a Kubernetes [auto-upgrade](/en-us/azure/aks/auto-upgrade-cluster#cluster-auto-upgrade-channels) channel, which automatically handles Kubernetes upgrades for your cluster. We also recommend setting a [planned maintenance window](planned-maintenance#create-a-maintenance-window) for your cluster. The `aksManagedAutoUpgradeSchedule`

maintenance window allows you to control when to perform cluster upgrades scheduled by your designated auto-upgrade channel. For more information, see [Use planned maintenance to schedule and control upgrades for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Prerequisites

To use node auto-provisioning in AKS, you need the following prerequisites:

- An Azure subscription. If you don't have one, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version
`2.76.0`

or later. To find the version, run`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/get-started-with-azure-cli).

## Limitations and unsupported features

The following limitations and unsupported features apply to node auto-provisioning in AKS:

- You can't enable NAP on clusters enabled with the
[cluster autoscaler](cluster-autoscaler). - Windows node pools aren't supported.
- IPv6 clusters aren't supported.
[Service principals](kubernetes-service-principal)aren't supported. You can use either a system-assigned or user-assigned managed identity.[Custom certificate authority (CA) certificates](custom-certificate-authority)aren't supported.- You can't
[stop a cluster](start-stop-cluster)enabled with NAP. [HTTP proxy](http-proxy)isn't supported.- You can't change the
[cluster egress outbound type](egress-outboundtype)after you create a cluster enabled with NAP. - When creating a NAP cluster in a custom virtual network (VNet), you must use a
[Standard Load Balancer](load-balancer-standard). The Basic Load Balancer isn't supported.

## Get started with node auto-provisioning on AKS

The following resources help you get started with node auto-provisioning on AKS:

[Enable or disable node auto-provisioning on an AKS cluster](use-node-auto-provisioning)[Use node auto-provisioning in a custom virtual network](node-auto-provisioning-custom-vnet)[Configure networking for node auto-provisioning on AKS](node-auto-provisioning-networking)[Configure node pools for node auto-provisioning on AKS](node-auto-provisioning-node-pools)[Configure disruption policies for node auto-provisioning on AKS](node-auto-provisioning-disruption)[Upgrade node images for node auto-provisioning on AKS](node-auto-provisioning-upgrade-image)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-cluster-isolation -->

# Best practices for cluster isolation in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. AKS allows flexibility in how you run multi-tenant clusters and isolate resources. To maximize your investment in Kubernetes, it's important you understand AKS multi-tenancy and isolation features.

This best practices article focuses on isolation for cluster operators. In this article, you learn how to:

- Plan for multi-tenant clusters and separation of resources.
- Use logical or physical isolation in your AKS clusters.

## Design clusters for multi-tenancy

Kubernetes lets you logically isolate teams and workloads in the same cluster. The goal is to provide the least number of privileges scoped to the resources each team needs. A Kubernetes [Namespace](concepts-clusters-workloads#namespaces) creates a logical isolation boundary. Other Kubernetes features and considerations for isolation and multi-tenancy include the following areas:

### Scheduling

*Scheduling* uses basic features like resource quotas and pod disruption budgets. For more information about these features, see [Best practices for basic scheduler features in AKS](operator-best-practices-scheduler).

More advanced scheduler features include:

- Taints and tolerations.
- Node selectors.
- Node and pod affinity or anti-affinity.

For more information about these features, see [Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler).

### Networking

*Networking* uses network policies to control the flow of traffic in and out of pods.

For more information, see [Secure traffic between pods using network policies in AKS](use-network-policies).

### Authentication and authorization

*Authentication and authorization* uses:

- Role-based access control (RBAC).
- Microsoft Entra integration.
- Pod identities.
- Secrets in Azure Key Vault.

For more information about these features, see [Best practices for authentication and authorization in AKS](operator-best-practices-identity).

### Containers

*Containers* include:

- The Azure Policy add-on for AKS to enforce pod security.
- Pod security admission.
- Scanning images and runtime for vulnerabilities.
- Using App Armor or Seccomp (Secure Computing) to restrict container access to the underlying node.

## Logically isolated clusters


Best practice guidanceSeparate teams and projects using

logical isolation. Minimize the number of physical AKS clusters you deploy to isolate teams or applications.

With logical isolation, you can use a single AKS cluster for multiple workloads, teams, or environments. Kubernetes [Namespaces](concepts-clusters-workloads#namespaces) form the logical isolation boundary for workloads and resources.

Logical separation of clusters usually provides a higher pod density than physically isolated clusters, with less excess compute capacity sitting idle in the cluster. When combined with the Kubernetes cluster autoscaler, you can scale the number of nodes up or down to meet demands. This best practice approach minimizes costs by running only the required number of nodes.

Kubernetes environments aren't entirely safe for hostile multi-tenant usage. In a multi-tenant environment, multiple tenants work on a shared infrastructure. If all tenants can't be trusted, you need extra planning to prevent tenants from impacting the security and service of others.

Other security features, like Kubernetes RBAC for nodes, efficiently block exploits. For true security when running hostile multi-tenant workloads, you should only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster and not an individual node.

For these types of hostile multi-tenant workloads, you should use physically isolated clusters.

## Physically isolated clusters


Best practice guidanceMinimize the use of physical isolation for each separate team or application deployment and use

logicalisolation instead.

Physically separating AKS clusters is a common approach to cluster isolation. In this isolation model, teams or workloads are assigned their own AKS cluster. While physical isolation might look like the easiest way to isolate workloads or teams, it adds management and financial overhead. With physically isolated clusters, you must maintain multiple clusters and individually provide access and assign permissions. You're also billed for each individual node.

Physically isolated clusters usually have a low pod density. Since each team or workload has their own AKS cluster, the cluster is often over-provisioned with compute resources. Often, a few pods are scheduled on those nodes. Unclaimed node capacity can't be used for applications or services in development by other teams. These excess resources contribute to the extra costs in physically isolated clusters.

## Next steps

This article focused on cluster isolation. For more information about cluster operations in AKS, see the following best practice articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/virtual-machines-node-pools -->

# Use Virtual Machines node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you'll learn about the new Virtual Machines node pool type for AKS.

With Virtual Machines node pools, AKS directly manages the provisioning and bootstrapping of every single node. For Virtual Machine Scale Sets node pools, AKS manages the model of the Virtual Machine Scale Sets and uses it to achieve consistency across all nodes in the node pool. Virtual Machines node pools enable you to orchestrate your cluster with virtual machines that best fit your individual workloads.

## Overview

### How it works

A node pool consists of a set of virtual machines, where different virtual machine sizes are designated to support different types of workloads. These virtual machine sizes, referred to as SKUs, are categorized into different families that are optimized for specific purposes. For more information, see [VM SKUs](/en-us/azure/virtual-machines/sizes/overview).

To enable scaling of multiple virtual machine sizes, the Virtual Machines node pool type uses a `ScaleProfile`

that contains configurations indicating how the node pool can scale, specifically the desired list of virtual machine size and the count of each size. A `ManualScaleProfile`

is a scale profile that specifies one desired virtual machine size and the total count of that type in the nodepool. Only one virtual machine size is allowed in a `ManualScaleProfile`

. You need to create a separate `ManualScaleProfile`

for each virtual machine size in your node pool. When creating a new Virtual Machines node pool, you add an initial manual scale profile for a virtual machine size using the `vm-size`

field and including a `node-count`

, per the instructions below. You can also add additional manual scale profiles following the instructions for [adding manual scale profiles](/en-us/azure/aks/virtual-machines-node-pools#add-a-manual-scale-profile-to-a-node-pool).

Note

When creating a new Virtual Machines node pool, you can have multiple scale profiles, and you need at least one manual scale profile in your nodepool.

### Advantages

Advantages of the Virtual Machines node pool type include:

**Flexibility**: Node specifications can be updated to adapt to your current workload and needs.**Fine-tuned control**: Single node-level controls allow specifying and mixing nodes of different specs to lift restrictions from a single model and improve consistency.**Efficiency**: You can reduce the node footprint for your cluster, simplifying your operational requirements.

Virtual Machines node pools provide a better experience for dynamic workloads and high availability requirements. Virtual Machines node pools enable you to set up multiple similar-family virtual machines in one node pool. Your workload will be automatically scheduled on the available resources that you configure.

### Feature comparison

The following table highlights how Virtual Machines node pools compare with standard [Scale Set](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-orchestration-modes) node pools.

| Node pool type | Capabilities |
|---|---|
| Virtual Machines node pool | You can add, remove, or update nodes in a node pool. Virtual machine types can be any virtual machine of the same family type (for example, D-series, A-Series, etc.). |
| Virtual Machine Scale Set based node pool | You can add or remove nodes of the same size and type in a node pool. If you add a new virtual machine size to the cluster, you need to create a new node pool. |

### Limitations

[Cluster autoscaler](cluster-autoscaler-overview)is currently not supported.[InifiniBand](/en-us/azure/virtual-machines/extensions/enable-infiniband)isn't available.[Node pool snapshot](node-pool-snapshot)isn't supported.- All VM sizes selected in a node pool need to be from a similar virtual machine family. For example, you can't mix an N-Series virtual machine type with a D-Series virtual machine type in the same node pool.
- Virtual Machines node pools allow up to five different virtual machine sizes per node pool.

## Prerequisites

- An Azure subscription. If you don't have one, you can
[create a free account](https://azure.microsoft.com/free). - Azure CLI version 2.73.0 or later installed and configured. To find the version, run
`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli#install-azure-cli) - This feature requires kubernetes version 1.27 or greater. To upgrade your kubernetes version, see
[Upgrade AKS cluster](upgrade-aks-cluster)

## Create an AKS cluster with Virtual Machines node pools

Note

Only *one* VM size is allowed in a scale profile, and the maximum limit is *five* VM scale profiles overall for a Virtual Machines node pool.

Create an AKS cluster with Virtual Machines node pools using the

command with the`az aks create`

`--vm-set-type`

flag set to`"VirtualMachines"`

.The following example creates a cluster named

*myAKSCluster*with a Virtual Machines node pool containing two nodes, generates SSH keys, sets the load balancer SKU to*standard*, and sets the Kubernetes version to*1.31.0*:`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --vm-set-type "VirtualMachines" \ --vm-sizes "Standard_D4s_v3" --node-count 2 \ --kubernetes-version 1.31.0`


## Create a cluster with Windows enabled and a Windows Virtual Machine node pool

Virtual Machine node pools are available in Windows enabled clusters. The following example creates a cluster named *myAKSCluster* with a Virtual Machines node pool. These steps create a Linux system pool at first.

Create a username to use as administrator credentials for the Windows Server nodes on your cluster. The following commands prompt you for a username and sets it to

*WINDOWS_USERNAME*for use in a later command.`echo "Please enter the username to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_USERNAME`

Create a password for the administrator username you created in the previous step. The password must be a minimum of 14 characters and meet the

[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).`echo "Please enter the password to use as administrator credentials for Windows Server nodes on your cluster: " && read WINDOWS_PASSWORD`

Create an AKS cluster with Windows enabled and Virtual Machines type node pools using the

command with the`az aks create`

`--vm-set-type`

flag set to`"VirtualMachines"`

.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 2 \ --enable-addons monitoring \ --generate-ssh-keys \ --windows-admin-username $WINDOWS_USERNAME \ --windows-admin-password $WINDOWS_PASSWORD \ --vm-set-type "VirtualMachines" \ --network-plugin azure`

Add a Virtual Machines node pool to an existing Windows enabled cluster using the

command with the`az aks nodepool add`

`--vm-set-type`

flag set to`"VirtualMachines"`

. The following example adds a Virtual Machines node pool named*npwin*to the*myAKSCluster*cluster:`az aks nodepool add --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --os-type Windows \ --name npwin \ --vm-sizes "Standard_D2s_V3" \ --node-count 1 --vm-set-type "VirtualMachines"`


## Add a Virtual Machines node pool to an existing cluster

Add a Virtual Machines node pool to an existing cluster using the

command with the`az aks nodepool add`

`--vm-set-type`

flag set to`"VirtualMachines"`

.The following example adds a Virtual Machines node pool named

*myvmpool*to the*myAKSCluster*cluster. The node pool creates a ManualScaleProfile with`--vm-sizes`

set to*Standard_D4s_v3*and a`--node-count`

of 3:`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --vm-set-type "VirtualMachines" \ --vm-sizes "Standard_D4s_v3" \ --node-count 3`


## Add a manual scale profile to a node pool

Add a manual scale profile to a node pool using the

with the`az aks nodepool manual-scale add`

`--vm-sizes`

flag set to`"Standard_D2s_v3"`

and the`node-count`

set to 2.The following example adds a manual scale profile to node pool

*myvmpool*in cluster*myAKSCluster*. The node pool includes two nodes with a VM SKU of*Standard_D2s_v3*:`az aks nodepool manual-scale add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --vm-sizes "Standard_D2s_v3" \ --node-count 2`


## Update an existing manual scale profile

Update an existing manual scale profile in a node pool using the

command with the`az aks nodepool manual-scale update`

`--vm-sizes`

flag set to`"Standard_D2s_v3"`

.Note

Use the

`--current-vm-sizes`

parameter to specify the size of the existing node pool that you want to update. You can update`--vm-sizes`

and/or`--node-count`

. When using other tools or REST APIs, you need to pass in a full`agentPoolProfiles.virtualMachinesProfile.scale`

field when updating the node pool scale profile.The following example updates a manual scale profile to the

*myvmpool*node pool in the*myAKSCluster*cluster. The command updates the number of nodes to five and changes the VM SKU from*Standard_D4s_v3*to*Standard_D8s_v3*:`az aks nodepool manual-scale update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --current-vm-sizes "Standard_D4s_v3" \ --vm-sizes "Standard_D8s_v3" \ --node-count 5`


## Delete a manual scale profile

Delete an existing manual scale profile using the

command.`az aks nodepool manual-scale delete`

Note

The

`--current-vm-sizes`

parameter specifies the size of the existing node pool to be deleted. When using other tools or REST APIs to update the node pool scale profile, pass in a full`agentPoolProfiles.virtualMachinesProfile.scale`

field.The following example deletes the manual scale profile for the

*Standard_D8s_v3*VM SKU in the*myvmpool*node pool.`az aks nodepool manual-scale delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myvmpool \ --current-vm-sizes "Standard_D8s_v3"`


## Next steps

In this article, you learned how to use Virtual Machines node pools in AKS. To learn more about node pools in AKS, see [Create node pools](create-node-pools).

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

To enable the application routing add-on to reload certificates from Azure Key Vault when they change, you should enable the [secret autorotation feature](csi-secrets-store-configuration-options#manage-auto-rotation) of the Secrets Store CSI driver. When autorotation is enabled, the driver updates the pod mount and the Kubernetes secret by polling for changes periodically, based on the rotation poll interval you define. The default rotation poll interval is two minutes.

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-windows-os -->

# Upgrade the operating system (OS) version for your Azure Kubernetes Service (AKS) Windows workloads

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When upgrading the OS version of a running Windows workload on Azure Kubernetes Service (AKS), you need to deploy a new node pool to ensure the Windows versions match on each node pool. This article describes the steps to upgrade the OS version for Windows workloads on AKS.

## Windows Server OS version support

When a new Windows Server OS version is released, AKS is committed to supporting it. We recommend that you upgrade to the latest version to take advantage of the fixes, improvements, and new functionality. AKS provides a five-year support lifecycle for every Windows Server version, starting with Windows Server 2022. During this period, AKS releases a new version that supports a newer version of Windows Server OS for you to upgrade to. After the five-year lifecycle ends, you must migrate workloads to newer supported versions to ensure compatibility, security updates, and continued support from AKS.

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-windows-2019-2022 -->

# Upgrade the operating system (OS) version for your Azure Kubernetes Service (AKS) Windows workloads

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When upgrading the OS version of a running Windows workload on Azure Kubernetes Service (AKS), you need to deploy a new node pool to ensure the Windows versions match on each node pool. This article describes the steps to upgrade the OS version for Windows workloads on AKS.

## Windows Server OS version support

When a new Windows Server OS version is released, AKS is committed to supporting it. We recommend that you upgrade to the latest version to take advantage of the fixes, improvements, and new functionality. AKS provides a five-year support lifecycle for every Windows Server version, starting with Windows Server 2022. During this period, AKS releases a new version that supports a newer version of Windows Server OS for you to upgrade to. After the five-year lifecycle ends, you must migrate workloads to newer supported versions to ensure compatibility, security updates, and continued support from AKS.

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

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
