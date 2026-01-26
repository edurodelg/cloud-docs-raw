---
merged_at: 2026-01-26T20:54:26.184505
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __node-auto-provisioning-aksnodeclass___scale-node-pools_start-stop-nodepools_co_ffd35f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _node-auto-provisioning-aksnodeclass___scale-node-pools_start-stop-nodepools_con_fc05ae.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-auto-provisioning-aksnodeclass.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-aksnodeclass -->

# Configure AKSNodeClass resources for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure `AKSNodeClass`

resources to define Azure-specific settings for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS) using Karpenter. `AKSNodeClass`

allows you to customize various aspects of the nodes that Karpenter provisions, such as the virtual machine (VM) image, operating system (OS) disk size, maximum pods per node, and kubelet configurations.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview of AKSNodeClass resources

`AKSNodeClass`

resources enable you to configure Azure-specific settings for NAP. Each [ NodePool resource](node-auto-provisioning-node-pools) must reference an

`AKSNodeClass`

using `spec.template.spec.nodeClassRef`

. You can have multiple `NodePools`

that point to the same `AKSNodeClass`

, allowing you to share common Azure configurations across different node pools.## Image family configuration

The `imageFamily`

field dictates the default VM image and bootstrapping logic for nodes provisioned through the `AKSNodeClass`

. If you don't specify an image family, the default is `Ubuntu2204`

. GPUs are supported with both image families on compatible VM sizes.

### Supported image families

: Ubuntu 22.04 Long Term Support (LTS) is the default Linux distribution for AKS nodes.`Ubuntu`

: Azure Linux is Microsoft's alternative Linux distribution for AKS workloads. For more information, see the`AzureLinux`

[Azure Linux documentation](/en-us/azure/aks/use-azure-linux)

#### Example image family configuration

The following example configures the `AKSNodeClass`

to use the `AzureLinux`

image family:

```
spec:
imageFamily: AzureLinux
```


#### FIPS compliant node image configuration

You can enable Federal Information Process Standard (FIPS) compliant node images also. For more in FIPS in AKS, visit our [FIPS documentation](enable-fips-nodes)

The `fipsMode`

field is set by default to Disabled, and can be set to the following options:

- FIPS - select FIPS-compliant node images
- Disabled - do not use FIPS-compliant node images

The following example configures the 'AKSNodeClass' to select FIPS-compliant node images by setting `fipsMode`

to `FIPS`

:

```
spec:
fipsMode: FIPS
```


## Virtual network (VNet) subnet configuration

The `vnetSubnetID`

field specifies which Azure VNet subnet should be used for provisioning node network interfaces. This field is optional. If you don't specify a subnet, NAP uses the default subnet configured during Karpenter installation. For more information, see [Subnet configurations for NAP](node-auto-provisioning-networking#subnet-configurations-for-nap).

### Example subnet configuration

The subnet ID must be in the full Azure Resource Manager (ARM) format, as shown in the following example:

```
spec:
vnetSubnetID: "/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Network/virtualNetworks/{vnet-name}/subnets/{subnet-name}"
```


## OS disk size configuration

The `osDiskSizeGB`

field specifies the size of the OS disk in gigabytes. The default value is 128 GB, and the minimum value is 30 GB.

Consider larger OS disk sizes for workloads that:

- Store significant data locally.
- Require extra space for container images.
- Have high disk I/O requirements.

### Example OS disk size configuration

```
spec:
osDiskSizeGB: 256 # 256 GB OS disk
```


## Ephemeral OS disk configuration

NAP automatically uses [Ephemeral OS disks](/en-us/azure/virtual-machines/ephemeral-os-disks) when available and suitable for the requested disk size. Ephemeral OS disks provide better performance and lower cost compared to managed disks.

### Ephemeral disk selection criteria

The system automatically chooses Ephemeral disks in the following scenarios:

- The VM instance type supports Ephemeral OS disks.
- The Ephemeral disk capacity is greater than or equal to the requested
`osDiskSizeGB`

. - The VM has sufficient ephemeral storage capacity.

If these conditions aren't met, the system falls back to using managed disks.

### Ephemeral disk types and prioritization

Azure VMs can have different types of ephemeral storage. The system uses the following priority order:

**NVMe disks**(highest performance)**Cache disks**(balanced performance)**Resource disks**(basic performance)

### Example ephemeral disk configuration

You can use node pool requirements to ensure nodes have sufficient ephemeral disk capacity, as shown in the following example:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: ephemeral-disk-pool
spec:
template:
spec:
requirements:
- key: karpenter.azure.com/sku-storage-ephemeralos-maxsize
operator: Gt
values: ["128"] # Require ephemeral disk larger than 128 GB
nodeClassRef:
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
name: my-node-class
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: my-node-class
spec:
osDiskSizeGB: 128 # This will use ephemeral disk if available and large enough
```


This configuration ensures that only VM instance types with ephemeral disks larger than 128 GB are selected, guaranteeing ephemeral disk usage for the specified OS disk size.

## Maximum pods configuration

The `maxPods`

field specifies the maximum number of pods that can be scheduled on a node. This setting affects both cluster density and network configuration.

The minimum value for `maxPods`

is 10, and the maximum value is 250.

### Default behavior for `maxPods`


The default behavior for `maxPods`

depends on the network plugin configuration. The following table summarizes the defaults:

| Network plugin configuration | Default `maxPods` per node |
|---|---|
| Azure CNI with standard networking (v1 or NodeSubnet) | 30 |
| Azure CNI with overlay networking | 250 |
| None (no network plugin) | 250 |
| Other configurations | 110 (standard Kubernetes default) |

### Example maximum pods configuration

```
spec:
maxPods: 50 # Allow up to 50 pods per node
```


## LocalDNS configuration

LocalDNS deploys a node level DNS proxy that resolves DNS queries closer to workloads, reducing query latency and improving resiliency during transient DNS disruptions. For more information, see the [LocalDNS documentation](localdns-custom). By default, LocalDNS is set to Disabled and can be configured to the following options:

`Disabled`

(default) - Disables the LocalDNS feature. DNS queries aren't resolved locally on the node.`Preferred`

- AKS manages LocalDNS enablement based on the Kubernetes version of the node pool. The configuration is always validated and included, but LocalDNS isn't enabled unless the correct Kubernetes version is used.`Required`

- LocalDNS is enforced on the node pool if all prerequisites are satisfied. If the requirements aren't met, the deployment fails.

### Example LocalDNS configuration

You can customize LocalDNS configurations such as `vnetDNSOverrides`

and `kubeDNSOverrides`

. For more details on the supported plugins, see [Customize LocalDNS](localdns-custom).

```
spec:
LocalDNS:
mode: Required
vnetDNSOverrides:
- zone: "."
cacheDuration: "30s"
forwardDestination: VnetDNS
forwardPolicy: Random
maxConcurrent: 80
protocol: ForceTCP
queryLogging: Log
serveStale: Immediate
serveStaleDuration: "100s"
- zone: "cluster.local"
cacheDuration: "40s"
forwardDestination: VnetDNS
forwardPolicy: Sequential
maxConcurrent: 70
protocol: PreferUDP
queryLogging: Error
serveStale: Disable
serveStaleDuration: "30s"
kubeDNSOverrides:
- zone: "."
cacheDuration: "30s"
forwardDestination: ClusterCoreDNS
forwardPolicy: RoundRobin
maxConcurrent: 100
protocol: PreferUDP
queryLogging: Log
serveStale: Immediate
serveStaleDuration: "60s"
- zone: "cluster.local"
cacheDuration: "10s"
forwardDestination: ClusterCoreDNS
forwardPolicy: Sequential
maxConcurrent: 50
protocol: PreferUDP
queryLogging: Error
serveStale: Disable
serveStaleDuration: "30s"
```


## Kubelet configuration

The `kubelet`

section allows you to configure various kubelet parameters that affect node behavior. These parameters are typical kubelet arguments, so the Azure provider simply passes them through to the kubelet on the node.

Important

**Configure kubelet settings carefully**, and test any changes in nonproduction environments first.

### CPU management

The following settings control CPU management behavior for the kubelet:

```
spec:
kubelet:
cpuManagerPolicy: "static" # or "none"
cpuCFSQuota: true
cpuCFSQuotaPeriod: "100ms"
```


`cpuManagerPolicy`

: Controls how the kubelet allocates CPU resources. Set to`"static"`

for CPU pinning in latency-sensitive workloads.`cpuCFSQuota`

: Enables CPU Completely Fair Scheduler (CFS) quota enforcement for containers that specify CPU limits.`cpuCFSQuotaPeriod`

: Sets the CPU CFS quota period.

### Image garbage collection

The following settings control image garbage collection behavior for the kubelet:

```
spec:
kubelet:
imageGCHighThresholdPercent: 85
imageGCLowThresholdPercent: 80
```


These settings control when the kubelet performs garbage collection of container images:

`imageGCHighThresholdPercent`

: Disk usage percentage that triggers image garbage collection.`imageGCLowThresholdPercent`

: Target disk usage percentage after garbage collection.

### Topology management

The following setting controls the topology manager policy for the kubelet:

```
spec:
kubelet:
topologyManagerPolicy: "best-effort" # none, restricted, best-effort, single-numa-node
```


The topology manager helps coordinate resource allocation for latency-sensitive workloads across CPU and device (like GPU) resources.

### System configuration

The following settings allow you to configure extra system parameters for the kubelet:

```
spec:
kubelet:
allowedUnsafeSysctls:
- "kernel.msg*"
- "net.ipv4.route.min_pmtu"
containerLogMaxSize: "50Mi"
containerLogMaxFiles: 5
podPidsLimit: 4096
```


`allowedUnsafeSysctls`

: List of permitted unsafe sysctls that pods can use.`containerLogMaxSize`

: Maximum size of container log files before rotation.`containerLogMaxFiles`

: Maximum number of container log files to retain.`podPidsLimit`

: Maximum number of processes allowed in any pod.

## Azure resource tags configuration

You can specify Azure resource tags that apply to all VM instances created using a particular `AKSNodeClass`

resource. Tags are useful for cost tracking, resource organization, and compliance requirements.

### Tag limitations

- Azure resource tags have a limit of 50 tags per resource.
- Tag names are case-insensitive but tag values are case-sensitive.
- Azure reserves some tag names that can't be used. For more information, see
[Tag guidance and limits](/en-us/azure/azure-resource-manager/management/tag-resources#tag-restrictions).

### Example tags configuration

```
spec:
tags:
Environment: "production"
Team: "platform"
Application: "web-service"
CostCenter: "engineering"
```


## Comprehensive `AKSNodeClass`

configuration example

The following example demonstrates a comprehensive `AKSNodeClass`

configuration that includes all the settings discussed in this article:

```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
template:
spec:
nodeClassRef:
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
name: comprehensive-example
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: comprehensive-example
spec:
# Image family configuration
# Default: Ubuntu
# Valid values: Ubuntu, AzureLinux
imageFamily: Ubuntu
# FIPS compliant mode - allows support for FIPS-compliant node images
# Default: Disabled
# Valid values: FIPS, Disabled
fipsMode: Disabled
# LocalDNS mode - allows use of LocalDNS feature
# Default: Disabled
# Valid values: Preferred, Required, Disabled
LocalDNS:
mode: Disabled
# additional details on vnetDNSOverrides and kubeDNSOverrides can be added here
# Virtual network subnet configuration (optional)
# If not specified, uses the default --vnet-subnet-id from Karpenter installation
vnetSubnetID: "/subscriptions/12345678-1234-1234-1234-123456789012/resourceGroups/my-rg/providers/Microsoft.Network/virtualNetworks/my-vnet/subnets/my-subnet"
# OS disk size configuration
# Default: 128 GB
# Minimum: 30 GB
osDiskSizeGB: 128
# Maximum pods per node configuration
# Default behavior depends on network plugin:
# - Azure CNI with standard networking: 30 pods
# - Azure CNI with overlay networking: 250 pods
# - Other configurations: 110 pods
# Range: 10-250
maxPods: 30
# Azure resource tags (optional)
# Applied to all VM instances created with this AKSNodeClass
tags:
Environment: "production"
Team: "platform-team"
Application: "web-service"
CostCenter: "engineering"
# Kubelet configuration (optional)
# All fields are optional with sensible defaults
kubelet:
# CPU management policy
# Default: "none"
# Valid values: none, static
cpuManagerPolicy: "static"
# CPU CFS quota enforcement
# Default: true
cpuCFSQuota: true
# CPU CFS quota period
# Default: "100ms"
cpuCFSQuotaPeriod: "100ms"
# Image garbage collection thresholds
# imageGCHighThresholdPercent must be greater than imageGCLowThresholdPercent
# Range: 0-100
imageGCHighThresholdPercent: 85
imageGCLowThresholdPercent: 80
# Topology manager policy
# Default: "none"
# Valid values: none, restricted, best-effort, single-numa-node
topologyManagerPolicy: "best-effort"
# Allowed unsafe sysctls (optional)
# Comma-separated list of unsafe sysctls or patterns
allowedUnsafeSysctls:
- "kernel.msg*"
- "net.ipv4.route.min_pmtu"
# Container log configuration
# containerLogMaxSize default: "50Mi"
containerLogMaxSize: "50Mi"
# containerLogMaxFiles default: 5, minimum: 2
containerLogMaxFiles: 5
# Pod process limits
# Default: -1 (unlimited)
podPidsLimit: 4096
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: __scale-node-pools_start-stop-nodepools_concepts-network-ip-address-planning.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _scale-node-pools_start-stop-nodepools.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: scale-node-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/scale-node-pools -->

# Scale node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your application workload demands change, you might need to scale the number of nodes in a node pool in Azure Kubernetes Service (AKS). In this article, you learn how to manually and automatically scale node pools in AKS.

## Prerequisites for AKS node pool scaling

- An existing AKS cluster with at least one node pool. If you need to create one, see
[Create an AKS cluster with node pools](create-node-pools). - You need the Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Scale a node pool manually

Scale the number of nodes in a node pool using the [

`az aks nodepool scale`

][az-aks-nodepool-scale] command. The`--node-count`

flag specifies the desired number of nodes in the node pool. In this example, the node pool is scaled to five nodes.`az aks nodepool scale \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --node-count 5 \ --no-wait`

Check the status of your node pools using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name>`

The following example output shows the node pool is in the

*Scaling*state with a new count of five nodes:`[ { ... "count": 5, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Scaling", ... "vmSize": "Standard_DS2_v2", ... }, { ... "count": 2, ... "name": "<node-pool-name-2>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Succeeded", ... "vmSize": "Standard_DS2_v2", ... } ]`

It takes a few minutes for the scale operation to complete. After the scale operation is complete, the node pool's

`provisioningState`

changes to*Succeeded*.

## Scale a node pool automatically with the cluster autoscaler

You can use the [cluster autoscaler](cluster-autoscaler-overview) with multiple node pools, and you can enable it on individual node pools and pass unique autoscaling rules to them.

Enable the cluster autoscaler on an existing node pool using the [

`az aks nodepool update`

][az-aks-nodepool-update] command with the`--update-cluster-autoscaler`

flag. The`--min-count`

and`--max-count`

flags specify the minimum and maximum number of nodes in the node pool. In this example, the cluster autoscaler is enabled with a minimum count of one node and a maximum count of five nodes:`az aks nodepool update \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --update-cluster-autoscaler \ --min-count 1 \ --max-count 5`


Note

If you want to disable the cluster autoscaler on a node pool, use the [`az aks nodepool update`

][az-aks-nodepool-update] command with the `--disable-cluster-autoscaler`

flag instead of `--update-cluster-autoscaler`

.

## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).


---

<!-- DOCUMENTO FUSIONADO: start-stop-nodepools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/start-stop-nodepools -->

# Start and stop an Azure Kubernetes Service (AKS) node pool

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might not need to continuously run your AKS workloads. For example, you might have a development cluster that has node pools running specific workloads. To optimize your compute costs, you can completely stop your node pools in your AKS cluster.

## Features and limitations

- You can't stop system pools.
- Spot node pools are supported.
- Stopped node pools can be upgraded.
- The cluster and node pool must be running.
- You can't stop node pools from clusters which use the
[Node Autoprovisioning (NAP)](node-autoprovision)feature.

Tip

You can use Azure Copilot to stop and start your node pools in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#start-and-stop-node-pools).

## Before you begin

This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using the [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

## Stop an AKS node pool

Stop a running AKS node pool using the

command.`az aks nodepool stop`

`az aks nodepool stop --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

Verify your node pool stopped using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

The following condensed example output shows the

`powerState`

as`Stopped`

:`{ [...] "osType": "Linux", "podSubnetId": null, "powerState": { "code": "Stopped" }, "provisioningState": "Succeeded", "proximityPlacementGroupId": null, [...] }`

Note

If the

`provisioningState`

shows`Stopping`

, your node pool is still in the process of stopping.Note

Stopping the node pool will stop its Cluster Autoscaler, and starts it back when starting the node pool. So if you manually modify the number of VMSS instances in the pool while it's stopped, Cluster Autoscaler might show inconsistencies.


## Start a stopped AKS node pool

Restart a stopped node pool using the

command.`az aks nodepool start`

`az aks nodepool start --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

Verify your node pool started using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

The following condensed example output shows the

`powerState`

as`Running`

:`{ [...] "osType": "Linux", "podSubnetId": null, "powerState": { "code": "Running" }, "provisioningState": "Succeeded", "proximityPlacementGroupId": null, [...] }`

Note

If the

`provisioningState`

shows`Starting`

, your node pool is still in the process of starting.

## Next steps

- To learn how to scale
`User`

pools to 0, see[scale](scale-cluster#scale-user-node-pools-to-0).`User`

pools to 0 - To learn how to stop your cluster, see
[cluster start/stop](start-stop-cluster). - To learn how to save costs using Spot instances, see
[add a spot node pool to AKS](spot-node-pool). - To learn more about the AKS support policies, see
[AKS support policies](support-policies).


---

<!-- DOCUMENTO FUSIONADO: concepts-network-ip-address-planning.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-network-ip-address-planning -->

# IP address planning for your Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance on IP address planning for Azure Kubernetes Service (AKS) clusters.

For specific guidance on IP address planning for individual CNI options, see the [next steps](#next-steps) section for links to plugin documentation.

## Subnet sizing

Your Azure VNet subnet must be large enough to accommodate your cluster, which depends on whether you're using an [overlay network](#overlay-networks) or a [flat network](#flat-networks).

### Overlay networks

With overlay networks, like [Azure CNI Overlay](concepts-network-azure-cni-overlay), your subnet needs to be large enough to assign IPs to your nodes. Pods are assigned IPs from a separate, private CIDR range and won't require VNet IPs. The VNet subnet you use for your cluster can be smaller than with flat networks.

It's important to ensure you allocate enough space in your private CIDR range for your pods to account for scaling. When planning your IP address range sizes, you should calculate your maximum pod count. Each node in your cluster is assigned a /24 (256 IP addresses) subnet for pods. You should plan your overlay network subnet to accommodate the maximum number of nodes you expect to run.

### Flat networks

Flat networks, like [Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet), require a large enough subnet to accommodate both nodes *and* pods. Since nodes and pods receive IPs from your VNet, you need to plan for the maximum number of nodes and pods you expect to run. Azure CNI Pod Subnet uses a subnet for your nodes and a separate subnet for your pods, so you need to plan for both.

## IP address sizing

### Upgrading and scaling considerations

When IP address planning for your AKS cluster, you should **consider the number of IP addresses required for upgrade and scaling operations**. If you set the IP address range to only support a fixed number of nodes, you won't be able to upgrade or scale your cluster.

When you **upgrade** your AKS cluster, a new node is deployed in the cluster. Services and workloads begin to run on the new node, and an older node is removed from the cluster. This rolling upgrade process requires a minimum of one additional block of IP addresses to be available. Your node count is then `n + 1`

where `n`

is the number of nodes in your cluster.

When you **scale** an AKS cluster, a new node is deployed in the cluster. Services and workloads begin to run on the new node. Your IP address range needs to take into considerations how you want to scale up the number of nodes and pods your cluster can support. A minimum of one additional node for upgrade operations or the number of nodes set by the [Customize node surge upgrade](upgrade-aks-cluster#customize-node-surge-upgrade) option should also be included. Your node count is then `n + number-of-additional-scaled-nodes-you-anticipate + max surge`

.

If you're using [Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet) and you expect your nodes to run the maximum number of pods and you regularly destroy and deploy pods, you should also factor in extra IP addresses per node. There can be few seconds latency required to delete a service and release its IP address for a new service to be deployed and acquire the address. The extra IP addresses account for this possibility.

The IP address plan for an AKS cluster consists of a virtual network, at least one subnet for nodes and pods, and a Kubernetes service address range.

| Azure Resource | Address Range | Limits and Sizing |
|---|---|---|
| Azure Virtual Network | Max size /8. 65,536 configured IP address limit. See
|

Use the following equation to calculate the minimum subnet size, including an extra node for upgrade operations: `(number of nodes + max surge nodes) + ((number of nodes + max surge nodes) * maximum pods per node that you configure)`


Example for a 50-node cluster: `(51) + (51 * 30 (default)) = 1,581`

(/21 or larger)

Example for a 50-node cluster, preparing to scale up an extra 10 nodes with the default max surge of 1 node: `(61) + (61 * 30 (default)) = 1,891`

(/21 or larger)

If you don't specify a maximum number of pods per node when you create your cluster, the maximum number of pods per node is set to 30. The minimum number of IP addresses required is based on that value. If you calculate your minimum IP address requirements on a different maximum value, see [Maximum pods per node](#maximum-pods-per-node) to set this value when you deploy your cluster.

*kubernetes.default.svc.cluster.local*address.## Maximum pods per node

The maximum number of pods per node in an AKS cluster is 250. The *default* maximum number of pods per node varies between *kubenet* and *Azure CNI* networking, and the method of cluster deployment.

| CNI | Default max pods | Configurable at deployment |
|---|---|---|
| Azure CNI Overlay | 250 | Yes (up to 250) |
| Azure CNI Pod subnet | 110 | Yes (up to 250) |
| Azure CNI (Legacy) | 30 | Yes (up to 250) |
| Kubenet | 110 | Yes (up to 250) |

## Configuring maximum pods per node for your clusters

You can configure the maximum number of pods per node either at cluster deployment time or as you add new node pools. You can set the maximum pods per node value as high as 250.

A minimum value for maximum pods per node is enforced to guarantee space for system pods critical to cluster health. The minimum value that can be set for maximum pods per node is 10 if and only if the configuration of each node pool has space for a minimum of 30 pods. For example, setting the maximum pods per node to the minimum of 10 requires each individual node pool to have a minimum of three nodes. This requirement applies for each new node pool created as well, so if 10 is defined as maximum pods per node each subsequent node pool added must have at least three nodes.

| Networking | Minimum | Maximum |
|---|---|---|
| Azure CNI | 10 | 250 |
| Kubenet | 10 | 250 |

Note

The minimum value in the previous table is strictly enforced by the AKS service. You cannot set a value for *maxPods* that is lower than the minimum shown, as doing so can prevent the cluster from starting.

### New clusters

You can define maximum pods per node when you create a new cluster using one of the following methods:

**Azure CLI**: Specify the`--max-pods`

argument when you deploy a cluster with thecommand.`az aks create`

**Azure Resource Manager template**: Specify the`maxPods`

property in the [ManagedClusterAgentPoolProfile] object when you deploy a cluster with an Azure Resource Manager template.**Azure portal**: Change the`Max pods per node`

field in the node pool settings when creating a cluster or adding a new node pool.

### Existing clusters

You can define maximum pods per node when you create a new node pool. If you need to increase the *maxPods* setting on an existing cluster, add a new node pool with the new desired *maxPods* count. After migrating your pods to the new pool, delete the node older pool.


---

<!-- DOCUMENTO FUSIONADO: __concepts-machine-learning-ops_aks-managed-gpu-nodes_deployment-safeguards.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _concepts-machine-learning-ops_aks-managed-gpu-nodes.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: concepts-machine-learning-ops.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-machine-learning-ops -->

# Concepts - Machine learning operations (MLOps) for AI and machine learning workflows

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about machine learning operations (MLOps), including what types of practices and tools are involved, and how it can simplify and speed up your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## What is MLOps?

Machine learning operations (MLOps) encompasses practices that facilitate collaboration between data scientists, IT operations, and business stakeholders, ensuring that machine learning models are developed, deployed, and maintained efficiently. MLOps applies DevOps principles to machine learning projects, aiming to automate and streamline the end-to-end machine learning lifecycle. This lifecycle includes training, packaging, validating, deploying, monitoring, and retraining models.

MLOps requires multiple roles and tools to work together effectively. Data scientists focus on tasks related to training the model, which is referred to as the * inner loop*. Machine learning engineers and IT operations teams handle the

*, where they apply DevOps practices to package, validate, deploy, and monitor models. When the model needs fine-tuning or retraining, the process loops back to the inner loop.*

**outer loop**### MLOps pipeline

Your MLOps pipeline may leverage various tools and microservices that are deployed sequentially or in parallel. Below are examples of key components in your pipeline that benefit from implementing the following best practices to reduce overhead and allow for faster iteration:

- Unstructured data store for new data flowing into your application
- Vector database to store and query structured, pre-processed data
- Data ingestion and indexing framework
- Vector ingestion and/or model retraining workflows
- Metrics collection and alerting tools (tracking model performance, volume of ingested data, etc.)
- Lifecycle management tools

## DevOps and MLOps

DevOps is a combination of tools and practices that enable you to create robust and reproducible applications. The goal of using DevOps is to quickly deliver value to your end users. Creating, deploying, and monitoring robust and reproducible models to deliver value to end users is the primary goal of MLOps.

There are *three* processes that are essential to MLOps:

**Machine learning workloads**for which a data scientist is responsible, including exploratory data analysis (EDA), feature engineering, and model training and tuning.**Software development practices**including planning, developing, testing, and packaging the model for deployment.**Operational aspects of deploying and maintaining the model in production**, including releasing, configuring resources, and monitoring the model.

### DevOps principles that apply to MLOps

MLOps leverages several principles from DevOps to enhance the machine learning lifecycle, such as *automation*, *continuous integration and delivery (CI/CD)*, *source control*, *Agile planning*, and *infrastructure as code (IaC)*.

#### Automation

By automating tasks, you can reduce manual errors, increase efficiency, and ensure consistency across the ML lifecycle. Automation can be applied to various stages, including data collection, model training, deployment, and monitoring. Through automation, you can also apply proactive measures in the AI pipeline to ensure data compliance with your organization's policies.

For example, your pipeline can automate:

- Model tuning/retraining at regular time intervals or when a certain amount of new data is collected in your application.
- Detection of performance degradation to kickstart fine-tuning or retraining on a different subset of data.
- Common vulnerability and exposure (CVE) scanning on base container images pulled from external container registries to ensure safe security practices.

#### Continuous integration (CI)

Continuous integration covers the *creating* and *verifying* aspects of the model development process. The goal of CI is to create the code and to verify the quality of the code and the model before deployment. This includes testing on a range of sample data sets to ensure that the model performs as expected and meets quality standards.

In MLOps, CI might involve:

- Refactoring exploratory code in Jupyter notebooks into Python or R scripts.
- Validating new input data for missing or error values.
- Unit testing and integration testing in the end-to-end pipeline.

To perform linting and unit testing, you can use automation tools like Azure Pipelines in Azure DevOps or GitHub Actions.

#### Continuous delivery (CD)

Continuous delivery involves the steps needed to safely deploy a model in production. The first step is to package and deploy the model in *pre-production environments*, such as dev and test environments. Portability of the parameters, hyperparameters, and other model artifacts is an important aspect to maintain as you promote the code through these environments. This portability is especially important when it comes to large language models (LLMs) and stable diffusion models. Once the model passes the unit tests and quality assurance (QA) tests, you can approve it for deployment in the *production environment*.

#### Source control

Source control, or *version control*, is essential for managing changes to code and models. In an ML system, this refers to data versioning, code versioning, and model versioning, which allow cross-functional teams to collaborate effectively and track changes over time. Using a Git-based source control system, like [ Azure Repos](https://azure.microsoft.com/products/devops/repos/#:%7E:text=Overview.%20Free%20private%20Git%20repositories,%20pull%20requests,%20and?msockid=182ea2d5e1ff6eb61ccbb1b8e5ff608a) in Azure DevOps or a

**GitHub repository**, enables you to programmatically maintain a history of changes, revert to previous versions, and manage branches for different experiments.

#### Agile planning

Agile planning involves isolating work into *sprints*, which are short time frames for completing specific tasks. This approach allows teams to adapt to changes quickly and deliver incremental improvements to the model. Model training can be an ongoing process, and Agile planning can help scope the project and enable better team alignment.

You can use tools like [ Azure Boards](/en-us/azure/devops/boards/get-started/what-is-azure-boards) in Azure DevOps or

**GitHub issues**to manage your Agile planning.

#### Infrastructure as code (IaC)

You use infrastructure as code to repeat and automate the infrastructure needed to train, deploy, and serve your models. In an ML system, IaC helps simplify and define the appropriate Azure resources needed for the specific job type in code, and the code is maintained in a repository. This allows you to version control your infrastructure and make changes for resource optimization, cost-effectiveness, etc. as needed.

## Next steps

Check out the following articles to learn about best practices for MLOps in your intelligent applications on AKS:


---

<!-- DOCUMENTO FUSIONADO: aks-managed-gpu-nodes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-managed-gpu-nodes -->

# Create a fully managed GPU node pool on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you run GPU workloads in Azure Kubernetes Service (AKS), you need to install and maintain several software components, including the GPU driver, Kubernetes device plugin, and GPU metrics exporter for telemetry. These components are essential for enabling GPU scheduling, container-level GPU access, observability of resource usage, and proper functioning of AKS GPU-enabled nodes. Previously, cluster operators had to either install these components manually or use open-source alternatives like the [NVIDIA GPU Operator](nvidia-gpu-operator), which can introduce complexity and operational overhead.

AKS now supports fully managed GPU nodes (preview) and installs the NVIDIA GPU driver, device plugin, and Data Center GPU Manager [(DCGM) metrics exporter](https://github.com/NVIDIA/dcgm-exporter/tree/main) by default. This feature enables one-step GPU node pool creation and makes the availability of GPU resources in AKS as simple as general purpose CPU nodes.

In this article, you learn how to provision a fully managed GPU node pool (preview) in your AKS cluster, including default installation of the NVIDIA GPU driver, device plugin, and metrics exporter.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed. To find the version, run
`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need to
[install and upgrade to latest version of the](#install-the-aks-preview-cli-extension).`aks-preview`

extension - You need to
[register the](#register-the-managedgpuexperiencepreview-feature-flag-in-your-subscription).`ManagedGPUExperiencePreview`

feature flag in your subscription

## Limitations

- This feature currently supports
[NVIDIA GPU-enabled virtual machine (VM) sizes](/en-us/azure/virtual-machines/sizes-gpu)only. - Updating a general-purpose node pool to add a GPU VM size isn't supported on AKS.
- Windows node pools are not supported with this feature, because GPU metrics are not supported. When creating Windows GPU node pools, AKS automatically installs and manages the drivers and Directx device plugin. See
[AKS Windows GPU documentation](use-windows-gpu)for more information. - Migrating your existing
[multi-instance GPU](gpu-multi-instance)node pools to use this feature isn't supported. - In-place upgrades to use this feature on existing GPU-enabled nodes isn't supported.

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](https://azure.microsoft.com/pricing/) tool and [region availability](https://azure.microsoft.com/global-infrastructure/services/).

### Install the `aks-preview`

CLI extension

Install the

`aks-preview`

CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update the extension to ensure you have the latest version installed using the

command.`az extension update`

`az extension update --name aks-preview`


### Register the `ManagedGPUExperiencePreview`

feature flag in your subscription

Register the

`ManagedGPUExperiencePreview`

feature flag in your subscription using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name ManagedGPUExperiencePreview`


## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Create an AKS-managed GPU node pool (preview)

You can add a fully managed GPU node pool (preview) to an existing AKS cluster by specifying OS SKU and `--tags EnableManagedGPUExperience=true`

command. When you do this, AKS will install the GPU driver, GPU device plugin, and metrics exporter automatically.

To use the default Ubuntu operating system (OS) SKU, you create the node pool without specifying an OS SKU. The node pool is configured for the default operating system based on the Kubernetes version of the cluster.

Add a node pool to your cluster using the

command with the`az aks nodepool add`

`--tags EnableManagedGPUExperience=true`

command.`az aks nodepool add \ --resource‐group MyResourceGroup \ --cluster‐name MyAKSCluster \ --name gpunp \ --node‐count 1 \ --node‐vm‐size Standard_NC6s_v3 \ --node‐taints sku=gpu:NoSchedule \ --enable‐cluster‐autoscaler \ --min‐count 1 \ --max‐count 3 \ --tags EnableManagedGPUExperience=true`

Confirm that the managed NVIDIA GPU software components are installed successfully:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name gpunp \`

Your output should include the following values:

`... ... "gpuInstanceProfile": … "gpuProfile": { "driver": "Install" }, ... ...`


## Migrate existing GPU workloads to an AKS-managed GPU node pool

In-place upgrades from a standard NVIDIA GPU node pool to a fully managed NVIDIA GPU node pool (preview) on your AKS cluster isn't supported. We recommend cordoning and draining your existing GPU nodes, then redeploying your workloads to a new GPU-enabled node pool with this feature enabled. See [Resize node pools on AKS](resize-node-pool) to learn more.

## Bring your own (BYO) GPU driver

If you want to control the installation of the NVIDIA drivers or use the [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html), you can bypass the GPU driver installation during node pool creation. In this case, Microsoft **doesn't support or manage** the maintenance and compatibility of the NVIDIA drivers as part of the node image deployment. See [Skip GPU driver installation](use-nvidia-gpu#skip-gpu-driver-installation) for NVIDIA GPU-enabled nodes on AKS to learn more.

## Next steps

- Deploy a
[sample GPU workload](use-nvidia-gpu#run-a-gpu-enabled-workload)on your AKS-managed GPU-enabled nodes. - Learn about
[GPU utilization and performance metrics](monitor-gpu-metrics)from managed NVIDIA DCGM exporter on your GPU node pool.

## Related articles

- Learn about
[GPU health monitoring](gpu-health-monitoring)with Node Problem Detector (NPD) on AKS. - Run
[distributed inference on multiple AKS GPU nodes](https://blog.aks.azure.com/2025/07/08/kaito-inference-with-acstor).


---

<!-- DOCUMENTO FUSIONADO: deployment-safeguards.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/deployment-safeguards -->

# Use Deployment Safeguards to enforce best practices in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Deployment Safeguards to enforce best practices on an Azure Kubernetes Service (AKS) cluster.

## Overview

Note

Deployment Safeguards is turned on by default in AKS Automatic.

Throughout the development lifecycle, it is common for bugs, issues, and other problems to arise if the initial deployment of your Kubernetes resources includes misconfigurations. To ease the burden of Kubernetes development, Azure Kubernetes Service (AKS) offers Deployment Safeguards. Deployment Safeguards enforce Kubernetes best practices in your AKS cluster through Azure Policy controls.

Deployment Safeguards offer two levels of configuration:

`Warn`

: Displays warning messages in the code terminal to alert you of any noncompliant cluster configurations but still allows the request to go through.`Enforce`

: Enforces compliant configurations by denying and mutating deployments if they don't follow best practices.

After you configure Deployment Safeguards for 'Warn' or 'Enforce', Deployment Safeguards programmatically assess your Kubernetes resources at creation or update time for compliance. Deployment Safeguards also display aggregated compliance information across your workloads at a per resource level via Azure Policy's compliance dashboard in the [Azure portal](https://portal.azure.com/#view/Microsoft_Azure_Policy/PolicyMenuBlade/%7E/Compliance) or in your CLI or terminal. Running a noncompliant workload indicates that your cluster is not following best practices and that workloads on your cluster are at risk of experiencing issues caused by your cluster configuration.

## Prerequisites

Note

Cluster admins don't need Azure Policy permissions to enable or disable Deployment Safeguards. However, it's required to have the Azure Policy add-on installed.

- You need to enable the Azure Policy add-on for AKS. For more information, see
[Enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks). This includes registering the`Microsoft.PolicyInsights`

resource provider in your subscription.

## Deployment Safeguards policies

The following table lists the policies that become active and the Kubernetes resources they target when you enable Deployment Safeguards. You can view the [currently available Deployment Safeguards](https://portal.azure.com/#view/Microsoft_Azure_Policy/InitiativeDetail.ReactView/id/%2Fproviders%2FMicrosoft.Authorization%2FpolicySetDefinitions%2Fc047ea8e-9c78-49b2-958b-37e56d291a44/scopes/) in the Azure portal as an Azure Policy definition or at [Azure Policy built-in definitions for Azure Kubernetes Service](/en-us/azure/aks/policy-reference#policy-definitions). The intention behind this collection is to create a common and generic list of best practices applicable to most users and use cases.

| Deployment safeguard policy | Mutation outcome if available |
|---|---|
| Cannot Edit Individual Nodes | N/A |
| Kubernetes cluster containers CPU and memory resource limits shouldn't exceed the specified limits | Sets CPU resource limits to 500m if not set and sets memory limits to 500Mi if no path is present |
| Must Have Anti Affinity Rules or topologySpreadConstraintsSet | N/A |
| No AKS Specific Labels | N/A |
| Kubernetes cluster containers should only use allowed images | N/A |
| Reserved System Pool Taints | Removes the `CriticalAddonsOnly` taint from a user node pool if not set. AKS uses the `CriticalAddonsOnly` taint to keep customer pods away from the system pool. This configuration ensures a clear separation between AKS components and customer pods and prevents eviction of customer pods that don't tolerate the `CriticalAddonsOnly` taint. |
| Ensure cluster containers have readiness or liveness probes configured | N/A |
| Kubernetes clusters should use Container Storage Interface (CSI) driver StorageClass | N/A |
| Kubernetes cluster services should use unique selectors | N/A |
| Kubernetes cluster container images should not include latest image tag | N/A |

If you want to submit an idea or request for Deployment Safeguards, open an issue in the [AKS GitHub repository](https://github.com/Azure/AKS) and add `[Deployment Safeguards request]`

to the beginning of the title.

## Pod Security Standards in Deployment Safeguards

Note

Baseline Pod Security Standards are now turned on by default in AKS Automatic. The baseline Pod Security Standards in AKS Automatic can't be turned off.

Deployment Safeguards also supports the ability to turn on [Baseline, Restricted and Privileged Pod Security Standards](https://kubernetes.io/docs/concepts/security/pod-security-standards/). To ensure your workloads deploy successfully, make sure each manifest complies with the Baseline or Restricted Pod Security requirements. By default, Azure Kubernetes Service uses Privileged Pod Security Standards.

| Policy | Error Message | Fix |
|---|---|---|
| AppArmor | `AppArmor annotation values must be undefined/nil, runtime/default, or localhost/*` or `AppArmor profile type must be one of: undefined/nil, RuntimeDefault, or Localhost` |
Remove any specification of AppArmor. Kubernetes by default applies apparmor settings. "On supported hosts, the RuntimeDefault AppArmor profile is applied by default". |
| Host Namespaces | `Host network namespaces are disallowed: spec.hostNetwork is set to true'` or `'Host PID namespaces are disallowed: spec.hostPID is set to true'` or `'Host IPC namespaces are disallowed: spec.hostIPC is set to true'` |
Set those values to false, or remove specifying the fields. |
| Privileged Containers | `'Privileged [ephemeral\|init\|N/A] containers are disallowed: spec.containers[*].securityContext.privileged is set to true'` |
Set the appropriate securityContext.privileged field to false, or remove the field. |
| Capabilities | Message will start with `'Disallowed capabilities detected` |
Remove the capability shown from the container's manifest. |
| HostPath volumes | `HostPath volumes are forbidden under restricted security policy unless containers mounting them are from allowed images` |
Remove the HostPath volume and volume mount. |
| Host Ports | HostPorts are forbidden under baseline security policy | Remove the host port specification from the offending container. |
| SELinux | `SELinux type must be one of: undefined/empty, container_t, container_init_t, container_kvm_t, or container_engine_t` |
Set the container's securityContext.seLinuxOptions.type field to one of the allowed values. |
| /proc Mount Type | ProcMount must be undefined/nil or 'Default' in spec.containers[*].securityContext.procMount | Set "* `spec.containers[*].securityContext.procMount` " to 'Default' or have it be undefined. |
| Seccomp | `Seccomp profile must not be explicitly set to Unconfined. Allowed values are: undefined/nil, RuntimeDefault, or Localhost` |
Set `securityContext.seccompProfile.type` on the pod or containers to one of the allowed values. |
| Sysctls | `Disallowed sysctl detected. Only baseline Kubernetes pod security standard sysctls are permitted` |
Remove the disallowed systctls( see the
|

`Only the following volume types are allowed under restricted policy: configMap, csi, downwardAPI, emptyDir, ephemeral, persistentVolumeClaim, projected, secret`

`Privilege escalation must be set to false under restricted policy`

`* `

spec.containers[*].securityContext.allowPrivilegeEscalation`` must explicitly be set to false for each container, initContainer, and ephemeralContainer.`Containers must not run as root user in spec.containers[*].securityContext.runAsNonRoot`

`'Containers must not run as root user: spec.securityContext.runAsUser is set to 0'`

`Seccomp profile must be "RuntimeDefault" or "Localhost" under restricted policy`

`securityContext.seccompProfile.type`

on the pod or containers to one of the allowed values. This differs from the baseline in the fact that the restricted policy doesn't allow an undefined value.`All containers must drop ALL capabilities under restricted policy`

or `Only NET_BIND_SERVICE may be added to capabilities under restricted policy`

## Enable Deployment Safeguards

Note

Using the Deployment Safeguards `Enforce`

level means you're opting in to deployments being blocked and mutated. Consider how these policies might work with your AKS cluster before enabling `Enforce`

.

### Enable Deployment Safeguards on an existing cluster

Enable Deployment Safeguards on an existing cluster that has the Azure Policy add-on enabled using the `az aks safeguard create`

command with the `--level`

flag. If you want to receive noncompliance warnings, set the `--level`

to `Warn`

. If you want to deny or mutate all noncompliant deployments, set it to `Enforce`

.

```
az aks safeguards create --resource-group <resource-group-name> --name <cluster-name> --level Enforce
```


You can also enable Deployment Safeguards by using the `--cluster`

flag and specifying the cluster resource ID.

```
az aks safeguards create --cluster <ID> --level Enforce
```


If you want to update the Deployment Safeguards level of an existing cluster, run the following command with the new value for `--level`

.

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn
```


### Excluding namespaces

You can also exclude certain namespaces from Deployment Safeguards. When you exclude a namespace, activity in that namespace is unaffected by Deployment Safeguards warnings or enforcement.

For example, to exclude the namespaces `ns1`

and `ns2`

, use a space separated list of namespaces with the `--excluded-ns`

flag, as shown in the following example:

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn --excluded-ns ns1 ns2
```


### Turn on Pod Security Standards

Note

Azure Kubernetes Service (AKS) uses `Privileged`

Pod Security Standards by default. If you want to revert to the default configuration, set the `--pss-level`

flag to `Privileged`

.

To enable Pod Security Standards in Deployment Safeguards, use the `--pss-level`

flag to select one of the following levels: `Baseline`

, `Restricted`

, or `Privileged`

.

```
az aks safeguards update --resource-group <resource-group-name> --name <cluster-name> --level Warn --pss-level <Baseline|Restricted|Privileged>
```


### Update your Deployment Safeguard version

Deployment Safeguards adhere to the [AKS addon versioning scheme](supported-kubernetes-versions). Each new version of a Deployment Safeguard will be released as a new minor version in AKS. These updates will be communicated through the [AKS GitHub release notes](https://github.com/Azure/AKS/releases) and reflected in the "Deployment Safeguards Policies" table in our documentation.

To learn more about AKS versioning and addons, refer to the following documentation: [aks-component-versions](supported-kubernetes-versions) and [aks-versioning-for-addons](integrations#add-ons).

## Verify compliance across clusters

After deploying your Kubernetes manifest, you see warnings or a potential denial message in your CLI or terminal if the cluster isn't compliant with Deployment Safeguards, as shown in the following examples:

**Warn**

```
$ kubectl apply -f deployment.yaml
Warning: [azurepolicy-k8sazurev1antiaffinityrules-ceffa082711831ebffd1] Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing
deployment.apps/simple-web created
```


**Enforce**

With Deployment Safeguard mutations, the `Enforce`

level mutates your Kubernetes resources when applicable. However, your Kubernetes resources still need to pass all safeguards to deploy successfully. If any safeguard policies fail, your resource is denied and won't be deployed.

```
$ kubectl apply -f deployment.yaml
Error from server (Forbidden): error when creating "deployment.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [azurepolicy-k8sazurev1antiaffinityrules-ceffa082711831ebffd1] Deployment with 2 replicas should have either podAntiAffinity or topologySpreadConstraints set to avoid disruptions due to nodes crashing
```


If your Kubernetes resources comply with the applicable mutation safeguards and meet all other safeguard requirements, they'll be successfully deployed, as shown in the following example:

```
$ kubectl apply -f deployment.yaml
deployment.apps/simple-web created
```


## Verify compliance across clusters using the Azure Policy dashboard

To verify Deployment Safeguards have been applied and to check on your cluster's compliance, navigate to the Azure portal page for your cluster and select **Policies**, then select **go to Azure Policy**.

From the list of policies and initiatives, select the initiative associated with Deployment Safeguards. You see a dashboard showing compliance state across your AKS cluster.

Note

To properly assess compliance across your AKS cluster, the Azure Policy initiative must be scoped to your cluster's resource group.

## Disable Deployment Safeguards

To disable Deployment Safeguards on your cluster, use the `delete`

command.

```
az aks safeguards delete --resource-group <resource-group-name> --name <cluster-name>
```


## FAQ

#### Can I create my own mutations?

No. If you have an idea for a safeguard, open an issue in the [AKS GitHub repository](https://github.com/Azure/AKS) and add `[Deployment Safeguards request]`

to the beginning of the title.

#### Can I pick and choose which mutations I want in Enforcement?

No. Deployment Safeguards is all or nothing. Once you turn on Warn or Enforce, all safeguards are active.

#### Why did my deployment resource get admitted even though it wasn't following best practices?

Deployment Safeguards enforce best practice standards through Azure Policy controls and has policies that validate against Kubernetes resources. To evaluate and enforce cluster components, Azure Policy extends [Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/). Gatekeeper enforcement also currently operates in a [ fail-open model](https://open-policy-agent.github.io/gatekeeper/website/docs/failing-closed/#considerations). As there's no guarantee that Gatekeeper responds to our networking call, we make sure that in that case, the validation is skipped so that the deny doesn't block your deployments.

To learn more, see [workload validation in Gatekeeper](https://open-policy-agent.github.io/gatekeeper/website/docs/workload-resources/).

## Next steps

- Learn more about
[best practices](best-practices)for operating an AKS cluster.


---

<!-- DOCUMENTO FUSIONADO: ___passive-cold-solution_virtual-nodes-portal__what-is-aks_intro-kubernetes_conf_2f8ca5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __passive-cold-solution_virtual-nodes-portal__what-is-aks_intro-kubernetes.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _passive-cold-solution_virtual-nodes-portal.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: passive-cold-solution.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/passive-cold-solution -->

# Passive-cold solution overview for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create an application in Azure Kubernetes Service (AKS) and choose an Azure region during resource creation, it's a single-region app. When the region becomes unavailable during a disaster, your application also becomes unavailable. If you create an identical deployment in a secondary Azure region, your application becomes less susceptible to a single-region disaster, which guarantees business continuity, and any data replication across the regions lets you recover your last application state.

This guide outlines a passive-cold solution for AKS. Within this solution, we deploy two independent and identical AKS clusters into two paired Azure regions with only one cluster actively serving traffic when the application is needed.

Note

The following practice has been reviewed internally and vetted in conjunction with our Microsoft partners.

## Passive-cold solution overview

In this approach, we have two independent AKS clusters being deployed in two Azure regions. When the application is needed, we activate the passive cluster to receive traffic. If the passive cluster goes down, we must manually activate the cold cluster to take over the flow of traffic. We can set this condition through a manual input every time or to specify a certain event.

## Scenarios and configurations

This solution is best implemented as a “use as needed” workload, which is useful for scenarios that require workloads to run at specific times of day or run on demand. Example use cases for a passive-cold approach include:

- A manufacturing company that needs to run a complex and resource-intensive simulation on a large dataset. In this case, the passive cluster is located in a cloud region that offers high-performance computing and storage services. The passive cluster is only used when the simulation is triggered by the user or by a schedule. If the cluster doesn’t work upon triggering, the cold cluster can be used as a backup and the workload can run on it instead.
- A government agency that needs to maintain a backup of its critical systems and data in case of a cyber attack or natural disaster. In this case, the passive cluster is located in a secure and isolated location that’s not accessible to the public.

## Components

The passive-cold disaster recovery solution uses many Azure services. This example architecture involves the following components:

**Multiple clusters and regions**: You deploy multiple AKS clusters, each in a separate Azure region. When the app is needed, the passive cluster is activated to receive network traffic.

**Key Vault**: You provision an [Azure Key Vault](/en-us/azure/key-vault/general/overview) in each region to store secrets and keys.

**Log Analytics**: Regional [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview) instances store regional networking metrics and diagnostic logs. A shared instance stores metrics and diagnostic logs for all AKS instances.

**Hub-spoke pair**: A hub-spoke pair is deployed for each regional AKS instance. [Azure Firewall Manager](/en-us/azure/firewall-manager/overview) policies manage the firewall rules across each region.

**Container Registry**: The container images for the workload are stored in a managed container registry. With this solution, a single [Azure Container Registry](/en-us/azure/container-registry/container-registry-intro) instance is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables you to replicate images to the selected Azure regions and provides continued access to images even if a region experiences an outage.

## Failover process

If the passive cluster isn't functioning properly because of an issue in its specific Azure region, you can activate the cold cluster and redirect all traffic to that cluster's region. You can use this process while the passive cluster is deactivated until it starts working again. The cold cluster can take a couple minutes to come online, as it has been turned off and needs to complete the setup process. This approach isn't ideal for time-sensitive applications. In that case, we recommend considering an [active-active failover](active-active-solution#failover-process).

### Application Pods (Regional)

A Kubernetes deployment object creates multiple replicas of a pod (*ReplicaSet*). If one is unavailable, traffic is routed between the remaining replicas. The Kubernetes *ReplicaSet* attempts to keep the specified number of replicas up and running. If one instance goes down, a new instance should be recreated. [Liveness probes](/en-us/azure/container-instances/container-instances-liveness-probe) can check the state of the application or process running in the pod. If the pod is unresponsive, the liveness probe removes the pod, which forces the *ReplicaSet* to create a new instance.

For more information, see [Kubernetes ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

### Application Pods (Global)

When an entire region becomes unavailable, the pods in the cluster are no longer available to serve requests. In this case, the Azure Front Door instance routes all traffic to the remaining health regions. The Kubernetes clusters and pods in these regions continue to serve requests. To compensate for increased traffic and requests to the remaining cluster, keep in mind the following guidance:

- Make sure network and compute resources are right sized to absorb any sudden increase in traffic due to region failover. For example, when using Azure Container Network Interface (CNI), make sure you have a subnet that can support all pod IPs with a spiked traffic load.
- Use the
[Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler)to increase the pod replica count to compensate for the increased regional demand. - Use the AKS
[Cluster Autoscaler](cluster-autoscaler)to increase the Kubernetes instance node counts to compensate for the increased regional demand.

### Kubernetes node pools (Regional)

Occasionally, localized failure can occur to compute resources, such as power becoming unavailable in a single rack of Azure servers. To protect your AKS nodes from becoming a single point regional failure, use [Azure Availability Zones](availability-zones). Availability zones ensure that AKS nodes in each availability zone are physically separated from those defined in another availability zones.

### Kubernetes node pools (Global)

In a complete regional failure, Azure Front Door routes traffic to the remaining healthy regions. Again, make sure to compensate for increased traffic and requests to the remaining cluster.

## Failover testing strategy

While there are no mechanisms currently available within AKS to take down an entire region of deployment for testing purposes, [Azure Chaos Studio](/en-us/azure/chaos-studio/chaos-studio-overview) offers the ability to create a chaos experiment on your cluster.

## Next steps

If you're considering a different solution, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: virtual-nodes-portal.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/virtual-nodes-portal -->

# Create and configure an Azure Kubernetes Services (AKS) cluster to use virtual nodes in the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Virtual nodes enable network communication between pods that run in Azure Container Instances (ACI) and Azure Kubernetes Service (AKS) clusters. To provide this communication, a virtual network subnet is created and delegated permissions are assigned. Virtual nodes only work with AKS clusters created using *advanced* networking (Azure CNI). AKS clusters are created with *basic* networking (kubenet) by default.

This article shows you how to create a virtual network and subnets, and then deploy an AKS cluster that uses advanced networking using the Azure portal.

Note

For an overview of virtual node region availability and limitations, see [Use virtual nodes in AKS](virtual-nodes).

## Before you begin

You need the ACI service provider registered on your subscription.

Check the status of the ACI provider registration using the

command.`az provider list`

`az provider list --query "[?contains(namespace,'Microsoft.ContainerInstance')]" -o table`

The following example output shows the

*Microsoft.ContainerInstance*provider is*Registered*:`Namespace RegistrationState RegistrationPolicy --------------------------- ------------------- -------------------- Microsoft.ContainerInstance Registered RegistrationRequired`

If the provider is

*NotRegistered*, register it using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerInstance`


## Create an AKS cluster

- Navigate to the Azure portal home page.
- Select
**Create a resource**>**Containers**. - On the
**Azure Kubernetes Service (AKS)**resource, select**Create**. - On the
**Basics**page, configure the following options:*Project details*: Select an Azure subscription, then select or create an Azure resource group, such as*myResourceGroup*.*Cluster details*: Enter a**Kubernetes cluster name**, such as*myAKSCluster*. Select a region and Kubernetes version for the AKS cluster.

- Select
**Next: Node pools**and check **Enable virtual nodes*. - Select
**Review + create**. - After the validation completes, select
**Create**.

By default, this process creates a managed cluster identity, which is used for cluster communication and integration with other Azure services. For more information, see [Use managed identities](use-managed-identity). You can also use a service principal as your cluster identity.

This process configures the cluster for advanced networking and the virtual nodes to use their own Azure virtual network subnet. The subnet has delegated permissions to connect Azure resources between the AKS cluster. If you don't already have a delegated subnet, the Azure portal creates and configures an Azure virtual network and subnet with the virtual nodes.

## Connect to the cluster

The Azure Cloud Shell is a free interactive shell you can use to run the steps in this article. It has common Azure tools preinstalled and configured to use with your account. To manage a Kubernetes cluster, use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. The `kubectl`

client is pre-installed in the Azure Cloud Shell.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. The following example gets credentials for the cluster name`az aks get-credentials`

*myAKSCluster*in the resource group named*myResourceGroup*:`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

.`kubectl get nodes`

`kubectl get nodes`

The following example output shows the single VM node created and the virtual Linux node named

*virtual-node-aci-linux*:`NAME STATUS ROLES AGE VERSION virtual-node-aci-linux Ready agent 28m v1.11.2 aks-agentpool-14693408-0 Ready agent 32m v1.11.2`


## Deploy a sample app

In the Azure Cloud Shell, create a file named

`virtual-node.yaml`

and copy in the following YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aci-helloworld spec: replicas: 1 selector: matchLabels: app: aci-helloworld template: metadata: labels: app: aci-helloworld spec: containers: - name: aci-helloworld image: mcr.microsoft.com/azuredocs/aci-helloworld ports: - containerPort: 80 nodeSelector: kubernetes.io/role: agent beta.kubernetes.io/os: linux type: virtual-kubelet tolerations: - key: virtual-kubelet.io/provider operator: Exists`

The YAML defines a

[nodeSelector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/)and[toleration](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/), which allows the pod to be scheduled on the virtual node. The pod is assigned an internal IP address from the Azure virtual network subnet delegated for use with virtual nodes.Run the application using the

command.`kubectl apply`

`kubectl apply -f virtual-node.yaml`

View the pods scheduled on the node using the

command with the`kubectl get pods`

`-o wide`

argument.`kubectl get pods -o wide`

The following example output shows the

`virtual-node-helloworld`

pod scheduled on the`virtual-node-linux`

node.`NAME READY STATUS RESTARTS AGE IP NODE virtual-node-helloworld-9b55975f-bnmfl 1/1 Running 0 4m 10.241.0.4 virtual-node-aci-linux`


Note

If you use images stored in Azure Container Registry, [configure and use a Kubernetes secret](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/). A limitation of virtual nodes is you can't use integrated Microsoft Entra service principal authentication. If you don't use a secret, pods scheduled on virtual nodes fail to start and report the error `HTTP response status code 400 error code "InaccessibleImage"`

.

## Test the virtual node pod

To test the pod running on the virtual node, browse to the demo application with a web client. The pod is assigned an internal IP address, so you can easily test the connectivity from another pod on the AKS cluster.

Create a test pod and attach a terminal session to it using the following

`kubectl run`

command.`kubectl run -it --rm virtual-node-test --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

Install

`curl`

in the pod using the following`apt-get`

command.`apt-get update && apt-get install -y curl`

Access the address of your pod using the following

`curl`

command and provide your internal IP address.`curl -L http://10.241.0.4`

The following condensed example output shows the demo application.

`<html> <head> <title>Welcome to Azure Container Instances!</title> </head> [...]`

Close the terminal session to your test pod with

`exit`

, which also deletes the pod.`exit`


## Next steps

In this article, you scheduled a pod on the virtual node and assigned a private, internal IP address. If you want, you can instead create a service deployment and route traffic to your pod through a load balancer or ingress controller. For more information, see [Create a basic ingress controller in AKS](ingress-basic).

Virtual nodes are one component of a scaling solution in AKS. For more information on scaling solutions, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: _what-is-aks_intro-kubernetes.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: what-is-aks.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/what-is-aks -->

# What is Azure Kubernetes Service (AKS)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that you can use to deploy and manage containerized applications. You need minimal container orchestration expertise to use AKS. AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure. AKS is an ideal platform for deploying and managing containerized applications that require high availability, scalability, and portability, and for deploying applications to multiple regions, using open-source tools, and integrating with existing DevOps tools.

This article is intended for platform administrators or developers who are looking for a scalable, automated, managed Kubernetes solution.

## Overview of AKS

AKS reduces the complexity and operational overhead of managing Kubernetes by shifting that responsibility to Azure. When you create an AKS cluster, Azure automatically creates and configures a control plane for you at no cost. The Azure platform manages the AKS control plane, which is responsible for the Kubernetes objects and worker nodes that you deploy to run your applications. Azure takes care of critical operations like health monitoring and maintenance, and you only pay for the AKS nodes that run your applications.

Note

AKS is [CNCF-certified](https://www.cncf.io/training/certification/software-conformance/) and is compliant with SOC, ISO, PCI DSS, and HIPAA. For more information, see the [Microsoft Azure compliance overview](https://azure.microsoft.com/explore/trusted-cloud/compliance/).

## Container solutions in Azure

Azure offers a range of container solutions designed to accommodate various workloads, architectures, and business needs.

| Container solution | Resource type |
|---|---|
|

[Azure Red Hat OpenShift](/en-us/azure/openshift/intro-openshift)[Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview)[Azure Container Instances](/en-us/azure/container-instances/container-instances-overview)[Azure Container Apps](/en-us/azure/container-apps/overview)For more information comparing the various solutions, see the following resources:

### When to use AKS

The following list describes some common use cases for AKS:

: Migrate existing applications to containers and run them in a fully managed Kubernetes environment.[Lift and shift to containers with AKS](/en-us/azure/cloud-adoption-framework/migrate/): Simplify the deployment and management of microservices-based applications with streamlined horizontal scaling, self-healing, load balancing, and secret management.[Microservices with AKS](/en-us/azure/architecture/guide/aks/aks-cicd-azure-pipelines): Efficiently balance speed and security by implementing secure DevOps with Kubernetes.[Secure DevOps for AKS](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Use virtual nodes to provision pods inside ACI that start in seconds and scale to meet demand.[Bursting from AKS with ACI](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Train models using large datasets with familiar tools, such as TensorFlow and Kubeflow.[Machine learning model training with AKS](/en-us/azure/architecture/ai-ml/idea/machine-learning-model-deployment-aks): Ingest and process real-time data streams with millions of data points collected via sensors, and perform fast analyses and computations to develop insights into complex scenarios.[Data streaming with AKS](/en-us/azure/architecture/solution-ideas/articles/data-streaming-scenario): Run Windows Server containers on AKS to modernize your Windows applications and infrastructure.[Using Windows containers on AKS](windows-aks-customer-stories)

## Features of AKS

The following table lists some of the key features of AKS:

| Feature | Description |
|---|---|
Identity and security management |
• Enforce
• Integrate with
• Use
|

**Logging and monitoring**[Container Insights](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable), a feature in Azure Monitor, to monitor the health and performance of your clusters and containerized applications.• Set up

[Advanced Container Networking Services](advanced-container-networking-services-overview)to collect and visualize network traffic data from your clusters.**Streamlined deployments**[smart defaults](quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal).• Autoscale your applications using the

[Kubernetes Event Driven Autoscaler (KEDA)](keda-about).• Use

[Draft for AKS](draft)to ready source code and prepare your applications for production.**Clusters and nodes**• Create clusters that run multiple node pools to support mixed operating systems and Windows Server containers.

• Configure automatic scaling using the

[cluster autoscaler](cluster-autoscaler)and[horizontal pod autoscaler](tutorial-kubernetes-scale#autoscale-pods).• Deploy clusters with

[confidential computing nodes](/en-us/azure/confidential-computing/confidential-nodes-aks-overview)to allow containers to run in a hardware-based trusted execution environment.**Storage volume support**• Use

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for fully managed, cloud-based volume management and orchestration of block storage. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes.• Use

[Azure Disks](azure-disk-csi)CSI driver for single pod access and[Azure Files](azure-files-csi)CSI driver for multiple, concurrent pod access.• Use

[Azure NetApp Files](azure-netapp-files)for high-performance, high-throughput, and low-latency file shares.**Networking**[networking options](concepts-network-cni-overview)for your needs.•

[Bring your own Container Network Interface (CNI)](use-byo-cni)to use a third-party CNI plugin.• Easily access applications deployed to your clusters using the

[application routing add-on with nginx](app-routing).**Development tooling integration**[Helm](quickstart-helm).• Install the

[Kubernetes extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools)to manage your workloads.• Leverage the features of Istio with the

[Istio-based service mesh add-on](istio-about).## Get started with AKS

Get started with AKS using the following resources:

- Learn the
[core Kubernetes concepts for AKS](concepts-clusters-workloads). - Evaluate application deployment on AKS with our
[AKS tutorial series](tutorial-kubernetes-prepare-app). - Review the
[Azure Well-Architected Framework for AKS](/en-us/azure/well-architected/service-guides/azure-kubernetes-service)to learn how to design and operate reliable, secure, efficient, and cost-effective applications on AKS. [Plan your design and operations](/en-us/azure/architecture/reference-architectures/containers/aks-start-here)for AKS using our reference architectures.- Explore
[configuration options and recommended best practices for cost optimization](best-practices-cost)on AKS.


---

<!-- DOCUMENTO FUSIONADO: intro-kubernetes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/intro-kubernetes -->

# What is Azure Kubernetes Service (AKS)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that you can use to deploy and manage containerized applications. You need minimal container orchestration expertise to use AKS. AKS reduces the complexity and operational overhead of managing Kubernetes by offloading much of that responsibility to Azure. AKS is an ideal platform for deploying and managing containerized applications that require high availability, scalability, and portability, and for deploying applications to multiple regions, using open-source tools, and integrating with existing DevOps tools.

This article is intended for platform administrators or developers who are looking for a scalable, automated, managed Kubernetes solution.

## Overview of AKS

AKS reduces the complexity and operational overhead of managing Kubernetes by shifting that responsibility to Azure. When you create an AKS cluster, Azure automatically creates and configures a control plane for you at no cost. The Azure platform manages the AKS control plane, which is responsible for the Kubernetes objects and worker nodes that you deploy to run your applications. Azure takes care of critical operations like health monitoring and maintenance, and you only pay for the AKS nodes that run your applications.

Note

AKS is [CNCF-certified](https://www.cncf.io/training/certification/software-conformance/) and is compliant with SOC, ISO, PCI DSS, and HIPAA. For more information, see the [Microsoft Azure compliance overview](https://azure.microsoft.com/explore/trusted-cloud/compliance/).

## Container solutions in Azure

Azure offers a range of container solutions designed to accommodate various workloads, architectures, and business needs.

| Container solution | Resource type |
|---|---|
|

[Azure Red Hat OpenShift](/en-us/azure/openshift/intro-openshift)[Azure Arc-enabled Kubernetes](/en-us/azure/azure-arc/kubernetes/overview)[Azure Container Instances](/en-us/azure/container-instances/container-instances-overview)[Azure Container Apps](/en-us/azure/container-apps/overview)For more information comparing the various solutions, see the following resources:

### When to use AKS

The following list describes some common use cases for AKS:

: Migrate existing applications to containers and run them in a fully managed Kubernetes environment.[Lift and shift to containers with AKS](/en-us/azure/cloud-adoption-framework/migrate/): Simplify the deployment and management of microservices-based applications with streamlined horizontal scaling, self-healing, load balancing, and secret management.[Microservices with AKS](/en-us/azure/architecture/guide/aks/aks-cicd-azure-pipelines): Efficiently balance speed and security by implementing secure DevOps with Kubernetes.[Secure DevOps for AKS](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Use virtual nodes to provision pods inside ACI that start in seconds and scale to meet demand.[Bursting from AKS with ACI](/en-us/azure/architecture/reference-architectures/containers/aks-start-here): Train models using large datasets with familiar tools, such as TensorFlow and Kubeflow.[Machine learning model training with AKS](/en-us/azure/architecture/ai-ml/idea/machine-learning-model-deployment-aks): Ingest and process real-time data streams with millions of data points collected via sensors, and perform fast analyses and computations to develop insights into complex scenarios.[Data streaming with AKS](/en-us/azure/architecture/solution-ideas/articles/data-streaming-scenario): Run Windows Server containers on AKS to modernize your Windows applications and infrastructure.[Using Windows containers on AKS](windows-aks-customer-stories)

## Features of AKS

The following table lists some of the key features of AKS:

| Feature | Description |
|---|---|
Identity and security management |
• Enforce
• Integrate with
• Use
|

**Logging and monitoring**[Container Insights](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable), a feature in Azure Monitor, to monitor the health and performance of your clusters and containerized applications.• Set up

[Advanced Container Networking Services](advanced-container-networking-services-overview)to collect and visualize network traffic data from your clusters.**Streamlined deployments**[smart defaults](quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal).• Autoscale your applications using the

[Kubernetes Event Driven Autoscaler (KEDA)](keda-about).• Use

[Draft for AKS](draft)to ready source code and prepare your applications for production.**Clusters and nodes**• Create clusters that run multiple node pools to support mixed operating systems and Windows Server containers.

• Configure automatic scaling using the

[cluster autoscaler](cluster-autoscaler)and[horizontal pod autoscaler](tutorial-kubernetes-scale#autoscale-pods).• Deploy clusters with

[confidential computing nodes](/en-us/azure/confidential-computing/confidential-nodes-aks-overview)to allow containers to run in a hardware-based trusted execution environment.**Storage volume support**• Use

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for fully managed, cloud-based volume management and orchestration of block storage. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes.• Use

[Azure Disks](azure-disk-csi)CSI driver for single pod access and[Azure Files](azure-files-csi)CSI driver for multiple, concurrent pod access.• Use

[Azure NetApp Files](azure-netapp-files)for high-performance, high-throughput, and low-latency file shares.**Networking**[networking options](concepts-network-cni-overview)for your needs.•

[Bring your own Container Network Interface (CNI)](use-byo-cni)to use a third-party CNI plugin.• Easily access applications deployed to your clusters using the

[application routing add-on with nginx](app-routing).**Development tooling integration**[Helm](quickstart-helm).• Install the

[Kubernetes extension for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-kubernetes-tools.vscode-kubernetes-tools)to manage your workloads.• Leverage the features of Istio with the

[Istio-based service mesh add-on](istio-about).## Get started with AKS

Get started with AKS using the following resources:

- Learn the
[core Kubernetes concepts for AKS](concepts-clusters-workloads). - Evaluate application deployment on AKS with our
[AKS tutorial series](tutorial-kubernetes-prepare-app). - Review the
[Azure Well-Architected Framework for AKS](/en-us/azure/well-architected/service-guides/azure-kubernetes-service)to learn how to design and operate reliable, secure, efficient, and cost-effective applications on AKS. [Plan your design and operations](/en-us/azure/architecture/reference-architectures/containers/aks-start-here)for AKS using our reference architectures.- Explore
[configuration options and recommended best practices for cost optimization](best-practices-cost)on AKS.


---

<!-- DOCUMENTO FUSIONADO: configure-load-balancer-standard.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/configure-load-balancer-standard -->

# Configure a public standard load balancer in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can customize different settings for your standard public load balancer at cluster creation time or by updating the cluster. These customization options allow you to create a load balancer that meets your workload needs. With the standard load balancer, you can:

[Change the inbound pool type](#change-the-inbound-pool-type).[Set or scale the number of managed outbound IPs](#scale-the-number-of-managed-outbound-public-ips).[Provide your own custom outbound IPs or outbound IP prefix](#provide-your-own-outbound-public-ips-or-prefixes).[Customize the number of allocated outbound ports to each node on the cluster](#configure-the-allocated-outbound-ports).[Configure the timeout setting for idle connections](#configure-the-load-balancer-idle-timeout).

Important

You can only use one outbound IP option (managed IPs, bring your own IP, or IP prefix) at a given time.

## Before you begin

- Follow the steps in
[Use a public standard load balancer in Azure Kubernetes Service (AKS)](load-balancer-standard)to create and deploy a load balancer service in AKS.

## Change the inbound pool type

You can reference AKS nodes in the load balancer backend pools by their IP configuration (Azure Virtual Machine Scale Sets based membership) or their IP address only. The IP address based backend pool membership provides higher efficiencies when updating services and provisioning load balancers, especially at high node counts. When combined with [NAT Gateway](nat-gateway) or [user-defined routing egress](egress-udr) types, provisioning of new nodes and services are more performant.

Two different pool membership types are available:

`nodeIPConfiguration`

: Legacy Virtual Machine Scale Sets IP configuration based pool membership type.`nodeIP`

: IP-based membership type.

### Requirements for changing the inbound pool type

Make sure you meet the following requirements before changing the inbound pool type:

- The AKS cluster must be version 1.23 or newer.
- The AKS cluster must be using standard load balancers and Virtual Machine Scale Sets.

-
[Create a new AKS cluster with IP-based inbound pool membership](#tabpanel_1_create-cluster-ip-based) -
[Update an existing AKS cluster to use IP-based inbound pool membership](#tabpanel_1_update-cluster-ip-based)

Create an AKS cluster with IP-based inbound pool membership using the

command with the`az aks create`

`--load-balancer-backend-pool-type=nodeIP`

parameter.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-backend-pool-type=nodeIP \ --generate-ssh-keys`


## Scale the number of managed outbound public IPs

Azure Load Balancer provides outbound and inbound connectivity from a VNet. Outbound rules make it simple to configure network address translation for the public standard load balancer.

Outbound rules follow the same syntax as load balancing and inbound NAT rules: *frontend IPs + parameters + backend pool*

An outbound rule configures outbound NAT for all virtual machines (VMs) identified by the backend pool to be translated to the frontend. Parameters provide more control over the outbound NAT algorithm.

While you can use an outbound rule with a single public IP address, outbound rules are great for scaling outbound NAT because they ease the configuration burden. You can use multiple IP addresses to plan for large-scale scenarios and outbound rules to mitigate SNAT exhaustion prone patterns. Each IP address provided by a frontend provides 64k ephemeral ports for the load balancer to use as SNAT ports.

When using a *Standard* SKU load balancer with managed outbound public IPs (which are created by default), you can scale the number of managed outbound public IPs using the `--load-balancer-managed-outbound-ip-count`

parameter.

Important

We don't recommend using the Azure portal to make any outbound rule changes. When making these changes, you should go through the AKS cluster and not directly on the Load Balancer resource.

Outbound rule changes made directly on the Load Balancer resource are removed whenever the cluster is reconciled, such as when it's stopped, started, upgraded, or scaled.

Use the Azure CLI, as shown in the examples. Outbound rule changes made using `az aks`

CLI commands are permanent across cluster downtime.

For more information, see [Azure Load Balancer outbound rules](/en-us/azure/load-balancer/outbound-rules).

### Set the number of managed outbound public IPs

-
[Create a new cluster with a specific number of managed outbound public IPs](#tabpanel_2_create-cluster-managed-outbound-ips) -
[Update an existing cluster to scale the number of managed outbound public IPs](#tabpanel_2_update-cluster-managed-outbound-ips)

Create a new AKS cluster with a specific number of managed outbound public IPs using the

command with the`az aks create`

`--load-balancer-managed-outbound-ip-count`

parameter. The following example sets the number of managed outbound public IPs to*two*.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-managed-outbound-ip-count 2 \ --generate-ssh-keys`


## Provide your own outbound public IPs or prefixes

When you use a *Standard* SKU load balancer, the AKS cluster automatically creates a public IP in the AKS-managed infrastructure resource group and assigns it to the load balancer outbound pool by default.

A public IP created by AKS is an AKS-managed resource, meaning AKS manages the lifecycle of that public IP and doesn't require user action directly on the public IP resource. Alternatively, you can assign your own custom public IP or public IP prefix at cluster creation time. Your custom IPs can also be updated on an existing cluster's load balancer properties.

### Requirements for using your own outbound public IPs or prefixes

Make sure you meet the following requirements before providing your own outbound public IPs or prefixes:

- You must create and own custom public IP addresses. You can't reuse managed public IP addresses created by AKS as a "bring your own custom IP" because it can cause management conflicts.
- You must ensure the AKS cluster identity has permissions to access the outbound IP, as per the
[required public IP permissions list](kubernetes-service-principal#grant-access-to-networking-resources). - Make sure you meet the
[prerequisites and constraints](/en-us/azure/virtual-network/ip-services/public-ip-address-prefix#limitations)necessary to configure outbound IPs or outbound IP prefixes.

### Provide your own outbound public IPs

-
[Provide your own outbound public IPs when creating a new cluster](#tabpanel_3_create-cluster-custom-ips) -
[Update an existing cluster to use your own outbound public IPs](#tabpanel_3_update-cluster-custom-ips)

Create a new AKS cluster with your own outbound public IPs using the

command with the`az aks create`

`--load-balancer-outbound-ips`

parameter. Make sure you replace the placeholder values with your own.`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-outbound-ips $PUBLIC_IP_ID1,$PUBLIC_IP_ID2 \ --generate-ssh-keys`


### Provide your own outbound public IP prefixes

-
[Provide your own outbound public IP prefixes when creating a new cluster](#tabpanel_4_create-cluster-custom-ip-prefixes) -
[Update an existing cluster to use your own outbound public IP prefixes](#tabpanel_4_update-cluster-custom-ip-prefixes)

Create a new AKS cluster with your own outbound public IP prefixes using the

command with the`az aks create`

`--load-balancer-outbound-ip-prefixes`

parameter. Make sure you replace the placeholder values with your own.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --load-balancer-outbound-ip-prefixes $PUBLIC_IP_PREFIX_ID1,$PUBLIC_IP_PREFIX_ID2 \ --generate-ssh-keys`


## Configure the allocated outbound ports

Important

If you have applications on your cluster that can establish a large number of connections to small set of destinations on public IP addresses, like many instances of a frontend application connecting to a database, you might have a scenario susceptible to encounter SNAT port exhaustion. SNAT port exhaustion happens when an application runs out of outbound ports to use to establish a connection to another application or host. If you have a scenario susceptible to encounter SNAT port exhaustion, we highly recommend you increase the allocated outbound ports and outbound frontend IPs on the load balancer.

For more information on SNAT, see [Use SNAT for outbound connections](/en-us/azure/load-balancer/load-balancer-outbound-connections).

By default, AKS sets *AllocatedOutboundPorts* on its load balancer to `0`

, which enables [automatic outbound port assignment based on backend pool size](/en-us/azure/load-balancer/load-balancer-outbound-connections#preallocatedports) when creating a cluster. For example, if a cluster has 50 or fewer nodes, 1024 ports are allocated to each node. This value allows for scaling to cluster maximum node counts without requiring networking reconfiguration, but can make SNAT port exhaustion more common as more nodes are added. As the number of nodes in the cluster increases, fewer ports are available per node. Increasing the node counts across the boundaries in the chart (for example, going from 50 to 51 nodes or 100 to 101) might be disruptive to connectivity as the SNAT ports allocated to existing nodes are reduced to allow for more nodes. We recommend using an explicit value for *AllocatedOutboundPorts*.

### View the current allocated outbound ports

Get the

*AllocatedOutboundPorts*value for the AKS cluster load balancer using thecommand.`az network lb outbound-rule list`

`NODE_RG=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query nodeResourceGroup -o tsv) az network lb outbound-rule list --resource-group $NODE_RG --lb-name kubernetes -o table`

The following example output shows that automatic outbound port assignment based on backend pool size is enabled for the cluster:

`AllocatedOutboundPorts EnableTcpReset IdleTimeoutInMinutes Name Protocol ProvisioningState ResourceGroup ------------------------ ---------------- ---------------------- --------------- ---------- ------------------- ------------- 0 True 30 aksOutboundRule All Succeeded MC_myResourceGroup_myAKSCluster_eastus`


### Calculate and verify outbound ports and IPs needed

Before setting a specific value or increasing an existing value for either outbound ports or outbound IP addresses, you must calculate the appropriate number of outbound ports and IP addresses. Use the following equation for this calculation rounded to the nearest integer: `64,000 ports per IP / <outbound ports per node> * <number of outbound IPs> = <maximum number of nodes in the cluster>`

.

#### Considerations for calculating outbound ports and IPs

When calculating the number of outbound ports and IPs and setting the values, keep the following information in mind:

- The number of outbound ports per node is fixed based on the value you set.
- The value for outbound ports must be a multiple of 8.
- Adding more IPs doesn't add more ports to any node, but it provides capacity for more nodes in the cluster.
- You must account for nodes that might be added as part of upgrades, including the count of nodes specified via
and`maxCount`

values.`maxSurge`


#### Examples of calculating outbound ports and IPs

The following examples show how the values you set affect the number of outbound ports and IP addresses:

- If the default values are used and the cluster has 48 nodes, each node has 1024 ports available.
- If the default values are used and the cluster scales from 48 to 52 nodes, each node is updated from 1024 ports available to 512 ports available.
- If the number of outbound ports is set to 1,000 and the outbound IP count is set to 2, then the cluster can support a maximum of 128 nodes:
`64,000 ports per IP / 1,000 ports per node * 2 IPs = 128 nodes`

. - If the number of outbound ports is set to 1,000 and the outbound IP count is set to 7, then the cluster can support a maximum of 448 nodes:
`64,000 ports per IP / 1,000 ports per node * 7 IPs = 448 nodes`

. - If the number of outbound ports is set to 4,000 and the outbound IP count is set to 2, then the cluster can support a maximum of 32 nodes:
`64,000 ports per IP / 4,000 ports per node * 2 IPs = 32 nodes`

. - If the number of outbound ports is set to 4,000 and the outbound IP count is set to 7, then the cluster can support a maximum of 112 nodes:
`64,000 ports per IP / 4,000 ports per node * 7 IPs = 112 nodes`

.

Important

After calculating the number of outbound ports and IPs, verify you have extra outbound port capacity to handle node surge during upgrades. It's critical to allocate sufficient excess ports for extra nodes needed for upgrade and other operations. AKS defaults to *one* buffer node for upgrade operations. If you're using [ maxSurge values](upgrade-aks-cluster#customize-node-surge-upgrade), multiply the outbound ports per node by your

`maxSurge`

value to determine the number of ports required. For example, if you calculate that you need 4000 ports per node with 7 IP addresses on a cluster with a maximum of 100 nodes and a max surge of 2:- 2 surge nodes * 4000 ports per node = 8000 ports needed for node surge during upgrades.
- 100 nodes * 4000 ports per node = 400,000 ports required for your cluster.
- 7 IPs * 64000 ports per IP = 448,000 ports available for your cluster.

This example shows the cluster has an excess capacity of 48,000 ports, which is sufficient to handle the 8000 ports needed for node surge during upgrades.

### Set the allocated outbound ports and outbound IPs

Once the values have been calculated and verified, you can apply those values using `load-balancer-outbound-ports`

and either `load-balancer-managed-outbound-ip-count`

, `load-balancer-outbound-ips`

, or `load-balancer-outbound-ip-prefixes`

when creating or updating a cluster.

-
[Create a new cluster with specific outbound ports and IPs](#tabpanel_5_create-cluster-outbound-ports-ips) -
[Update an existing cluster with specific outbound ports and IPs](#tabpanel_5_update-cluster-outbound-ports-ips)

Create a new AKS cluster with specific outbound ports and IPs using the

command. The following example sets the`az aks create`

`--load-balancer-managed-outbound-ip-count`

parameter to*7*and the`--load-balancer-outbound-ports`

parameter to*4000*:`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-managed-outbound-ip-count 7 \ --load-balancer-outbound-ports 4000 \ --generate-ssh-keys`


## Configure the load balancer idle timeout

When SNAT port resources are exhausted, outbound flows fail until existing flows release SNAT ports. Load balancer reclaims SNAT ports when the flow closes, and the AKS-configured load balancer uses a 30-minute idle timeout for reclaiming SNAT ports from idle flows. You can also use transport (for example, ** TCP keepalives** or

**) to refresh an idle flow and reset this idle timeout if necessary.**

`application-layer keepalives`

If you expect to have numerous short-lived connections and no long-lived connections that might have long times of idle, like using `kubectl proxy`

or `kubectl port-forward`

, consider using a low timeout value such as *4 minutes*. When using TCP keepalives, it's sufficient to enable them on one side of the connection. For example, it's sufficient to enable them on the server side only to reset the idle timer of the flow. It's not necessary for both sides to start TCP keepalives. Similar concepts exist for application layer, including database client-server configurations. Check the server side for what options exist for application-specific keepalives.

Important

AKS enables *TCP Reset* on idle by default. We recommend you keep this configuration and leverage it for more predictable application behavior on your scenarios. For more information, see [Azure load balancer TCP reset](/en-us/azure/load-balancer/load-balancer-tcp-reset).

When setting *IdleTimeoutInMinutes* to a different value than the default of 30 minutes, consider how long your workloads need an outbound connection. Also consider that the default timeout value for a *Standard* SKU load balancer used outside of AKS is *4 minutes*. An *IdleTimeoutInMinutes* value that more accurately reflects your specific AKS workload can help decrease SNAT exhaustion caused by tying up connections no longer being used.

Warning

Altering the values for *AllocatedOutboundPorts* and *IdleTimeoutInMinutes* might significantly change the behavior of the outbound rule for your load balancer and shouldn't be done lightly. See [Troubleshoot SNAT](troubleshoot-source-network-address-translation) and review the [Load balancer outbound rules](/en-us/azure/load-balancer/load-balancer-outbound-connections#outboundrules) and [outbound connections in Azure](/en-us/azure/load-balancer/load-balancer-outbound-connections) before updating these values to fully understand the impact of your changes.

-
[Create a new cluster with a specific idle timeout](#tabpanel_6_create-cluster-idle-timeout) -
[Update an existing cluster with a specific idle timeout](#tabpanel_6_update-cluster-idle-timeout)

Create a new AKS cluster with a specific idle timeout using the

command with the`az aks create`

`--load-balancer-idle-timeout`

parameter. The following example sets the idle timeout to*4 minutes*:`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --load-balancer-idle-timeout 4 \ --generate-ssh-keys`


## Restrict inbound traffic to specific IP ranges

The following manifest uses `loadBalancerSourceRanges`

to specify a new IP range for inbound external traffic:

```
apiVersion: v1
kind: Service
metadata:
name: azure-vote-front
spec:
type: LoadBalancer
ports:
- port: 80
selector:
app: azure-vote-front
loadBalancerSourceRanges:
- MY_EXTERNAL_IP_RANGE
```


This example updates the rule to allow inbound external traffic only from the `MY_EXTERNAL_IP_RANGE`

range. If you replace `MY_EXTERNAL_IP_RANGE`

with the internal subnet IP address, traffic is restricted to only cluster internal IPs. If traffic is restricted to cluster internal IPs, clients outside your Kubernetes cluster are unable to access the load balancer.

Note

Keep the following information in mind when restricting inbound traffic:

- When you need to allow both CIDR blocks and Azure service tags, remove the
`loadBalancerSourceRanges`

property and add the`service.beta.kubernetes.io/azure-allowed-ip-ranges`

and/or`service.beta.kubernetes.io/azure-allowed-service-tags`

Load Balancer annotations. This configuration applies filtering only at the NSG layer and skips host-level kube-proxy rules. If you set the`loadBalancerSourceRanges`

property together with the`azure-allowed-service-tags`

annotation, AKS will report an error when you attempt to apply the specification. - Inbound, external traffic flows from the load balancer to the VNet for your AKS cluster. The VNet has a network security group (NSG) which allows all inbound traffic from the load balancer. This NSG uses a
[service tag](/en-us/azure/virtual-network/network-security-groups-overview#service-tags)of type*LoadBalancer*to allow traffic from the load balancer. - Pod CIDR should be added to
`loadBalancerSourceRanges`

if there are Pods needing to access the service's Load Balancer IP for clusters with Kubernetes version 1.25 or higher.

## Maintain the client's IP on inbound connections

By default, a service of type `LoadBalancer`

[in Kubernetes](https://kubernetes.io/docs/tutorials/services/source-ip/#source-ip-for-services-with-type-loadbalancer) and in AKS doesn't persist the client's IP address on the connection to the pod. The source IP on the packet that's delivered to the pod becomes the private IP of the node. To maintain the client's IP address, you must set `service.spec.externalTrafficPolicy`

to `local`

in the service definition. The following manifest shows an example:

```
apiVersion: v1
kind: Service
metadata:
name: azure-vote-front
spec:
type: LoadBalancer
externalTrafficPolicy: Local
ports:
- port: 80
selector:
app: azure-vote-front
```


## Customizations via Kubernetes Annotations

The following annotations are supported for Kubernetes services with type `LoadBalancer`

, and they only apply to **INBOUND** flows.

| Annotation | Value | Description |
|---|---|---|
`service.beta.kubernetes.io/azure-load-balancer-internal` |
`true` or `false` |
Specify whether the load balancer should be internal. If not set, it defaults to public. |
`service.beta.kubernetes.io/azure-load-balancer-internal-subnet` |
Name of the subnet | Specify which subnet the internal load balancer should be bound to. If not set, it defaults to the subnet configured in cloud config file. |
`service.beta.kubernetes.io/azure-dns-label-name` |
Name of the DNS label on Public IPs | Specify the DNS label name for the public service. If it's set to an empty string, the DNS entry in the Public IP isn't used. |
`service.beta.kubernetes.io/azure-shared-securityrule` |
`true` or `false` |
Specify exposing the service through a potentially shared Azure security rule to increase service exposure, utilizing Azure
|

`service.beta.kubernetes.io/azure-load-balancer-resource-group`

`service.beta.kubernetes.io/azure-allowed-service-tags`

[service tags](/en-us/azure/virtual-network/network-security-groups-overview#service-tags)separated by commas.`service.beta.kubernetes.io/azure-allowed-ip-ranges`

`service.beta.kubernetes.io/azure-load-balancer-tcp-idle-timeout`

`service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset`

`true`

or `false`

`service.beta.kubernetes.io/azure-load-balancer-ipv4`

`service.beta.kubernetes.io/azure-load-balancer-ipv6`

### Customize allowed IP ranges (preview)

You can use the `azure-allowed-service-tags`

and `azure-allowed-ip-ranges`

annotations to combine CIDR blocks and Azure service tags on the load balancer. Add `service.beta.kubernetes.io/azure-allowed-ip-ranges`

with a comma-separated list of IP prefixes, and add `service.beta.kubernetes.io/azure-allowed-service-tags`

with one or more Azure service tags. The AKS cloud provider merges both values into a single NSG rule, so traffic is filtered centrally at the NSG giving you a single, NSG-centric control plane for both IP addresses and service tags.

You can continue to use the `loadBalancerSourceRanges`

property for cases where you want CIDR-based restrictions enforced both in the NSG and the host. You can't use this property with the `azure-allowed-service-tags`

annotation. If both are specified, AKS reports an error when you try to apply the load balancer service specification.

### Customize the load balancer health probe

The following annotations are supported to customize the load balancer health probe behavior:

| Annotation | Value | Description |
|---|---|---|
`service.beta.kubernetes.io/azure-load-balancer-health-probe-interval` |
Health probe interval | |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-num-of-probe` |
The minimum number of unhealthy responses of health probe | |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
Request path of the health probe | |
`service.beta.kubernetes.io/port_{port}_no_lb_rule` |
true/false | {port} is service port number. When set to `true` , no load balancer or health probe rules for this port are generated. Health check service shouldn't be exposed to the public internet. |
`service.beta.kubernetes.io/port_{port}_no_probe_rule` |
true/false | {port} is service port number. When set to `true` , no health probe rules for this port are generated. |
`service.beta.kubernetes.io/port_{port}_health-probe_protocol` |
Health probe protocol | {port} is service port number. Explicit protocol for the health probe for the service port {port}, overriding port.appProtocol if set. |
`service.beta.kubernetes.io/port_{port}_health-probe_port` |
port number or port name in service manifest | {port} is service port number. Explicit port for the health probe for the service port {port}, overriding the default value. |
`service.beta.kubernetes.io/port_{port}_health-probe_interval` |
Health probe interval | {port} is service port number. |
`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe` |
The minimum number of unhealthy responses of health probe | {port} is service port number. |
`service.beta.kubernetes.io/port_{port}_health-probe_request-path` |
Request path of the health probe | {port} is service port number. |

Note

AKS now supports shared health probes for `externalTrafficPolicy: Cluster`

Services. To learn more, see [Use shared health probes for externalTrafficPolicy: Cluster Services (preview) in Azure Kubernetes Service (AKS)](shared-health-probes).

#### Default health probe behavior

Currently, the default protocol of the health probe varies among services with different transport protocols, app protocols, annotation, and external traffic policies.

- For local services, HTTP and /healthz would be used. The health probe will query
`NodeHealthPort`

rather than actual backend service. - For cluster TCP services, TCP would be used.
- For cluster UDP services, no health probes.

Note

For local services with PLS integration and PLS proxy protocol enabled, the default HTTP and /healthz health probe doesn't work. Thus health probe can be customized the same way as cluster services to support this scenario.

##### Health probe request path annotation

Starting in Kubernetes version 1.20, the service annotation `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

was introduced to determine the health probe behavior.

- For clusters <=1.23,
`spec.ports.appProtocol`

would only be used as probe protocol when`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

is also set. - For clusters >1.24,
`spec.ports.appProtocol`

would be used as probe protocol and`/`

would be used as default probe request path (`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

could be used to change to a different request path).

Note that the request path would be ignored when using TCP or the `spec.ports.appProtocol`

is empty. The following table summarizes the default health probe behavior:

| loadbalancer sku | `externalTrafficPolicy` |
spec.ports.Protocol | spec.ports.AppProtocol | `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
LB probe protocol | LB probe request path |
|---|---|---|---|---|---|---|
| standard | local | any | any | any | http | `/healthz` |
| standard | cluster | udp | any | any | null | null |
| standard | cluster | tcp | (ignored) | tcp | null | |
| standard | cluster | tcp | tcp | (ignored) | tcp | null |
| standard | cluster | tcp | http/https | TCP(<=1.23) or http/https(>=1.24) | null(<=1.23) or `/` (>=1.24) |
|
| standard | cluster | tcp | http/https | `/custom-path` |
http/https | `/custom-path` |
| standard | cluster | tcp | unsupported protocol | `/custom-path` |
tcp | null |
| basic | local | any | any | any | http | `/healthz` |
| basic | cluster | tcp | (ignored) | tcp | null | |
| basic | cluster | tcp | tcp | (ignored) | tcp | null |
| basic | cluster | tcp | http | TCP(<=1.23) or http/https(>=1.24) | null(<=1.23) or `/` (>=1.24) |
|
| basic | cluster | tcp | http | `/custom-path` |
http | `/custom-path` |
| basic | cluster | tcp | unsupported protocol | `/custom-path` |
tcp | null |

##### Health probe interval and number of probes annotations

Starting in Kubernetes version 1.21, two service annotations `service.beta.kubernetes.io/azure-load-balancer-health-probe-interval`

and `load-balancer-health-probe-num-of-probe`

were introduced, which customize the configuration of health probe. If `service.beta.kubernetes.io/azure-load-balancer-health-probe-interval`

isn't set, a default value of *5* is applied. If `load-balancer-health-probe-num-of-probe`

isn't set, a default value of *2* is applied.

### Custom Load Balancer health probe for port

Different ports in a service can require different health probe configurations. This could be because of service design (such as a single health endpoint controlling multiple ports), or Kubernetes features like the [MixedProtocolLBService](https://kubernetes.io/docs/concepts/services-networking/service/#load-balancers-with-mixed-protocol-types).

The following table summarizes the port-specific annotations that can be used to override the global health probe annotations for a specific port in the service:

| Port-specific annotation | Global probe annotation | Behavior |
|---|---|---|
`service.beta.kubernetes.io/port_{port}_no_lb_rule` |
N/A (no equivalent globally) | If set to `true` , no load balancer or probe rules are generated. |
`service.beta.kubernetes.io/port_{port}_no_probe_rule` |
N/A (no equivalent globally) | If set to `true` , no probe rules are generated. |
`service.beta.kubernetes.io/port_{port}_health-probe_protocol` |
N/A (no equivalent globally) | Sets the health probe protocol for this service port (for example: Http, Https, Tcp). |
`service.beta.kubernetes.io/port_{port}_health-probe_port` |
N/A (no equivalent globally) | Sets the health probe port for this service port (for example: 15021). |
`service.beta.kubernetes.io/port_{port}_health-probe_request-path` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path` |
For Http or Https, sets the health probe request path (defaults to /). |
`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-num-of-probe` |
Number of consecutive probe failures before the port is considered unhealthy. |
`service.beta.kubernetes.io/port_{port}_health-probe_interval` |
`service.beta.kubernetes.io/azure-load-balancer-health-probe-interval` |
The amount of time between probe attempts. |

## Next steps

To learn more about Kubernetes services, see the [Kubernetes services documentation](https://kubernetes.io/docs/concepts/services-networking/service/).

To learn more about using internal load balancer for inbound traffic, see the [AKS internal load balancer documentation](internal-lb).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/private-cluster-connect -->

# Establish network connectivity to a private Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In private AKS clusters, the API server endpoint has no public IP address. To manage the API server, you need to use a virtual machine (VM) or container that has access to the virtual network (VNet) of the AKS cluster. There are several options for establishing network connectivity to the private cluster:

- Use an
[Azure Cloud Shell](/en-us/azure/cloud-shell/vnet/overview)instance deployed into a subnet that's connected to the API server for the cluster. - Use
[Azure Bastion](/en-us/azure/bastion/bastion-connect-to-aks-private-cluster)'s native client tunneling feature (preview). - Use a VM in a separate network and set up
[virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview). - Use a
[private endpoint](/en-us/azure/private-link/private-endpoint-overview)connection. - Create a VM in the same VNet as the AKS cluster using the
command with the`az vm create`

`--vnet-name`

flag. - Use an
[Express Route or VPN](/en-us/azure/expressroute/expressroute-about-virtual-network-gateways)connection. - Use the
[AKS](access-private-cluster).`command invoke`

feature

## Choose a connectivity option

Azure Cloud Shell and Azure Bastion (preview) are the easiest options. Express Route and VPNs add costs and require extra networking complexity. Virtual network peering requires you to plan your network CIDR ranges to ensure there are no overlapping ranges.

The following table outlines the key differences and limitations of using Azure Cloud Shell and Azure Bastion:

| Option | Azure Cloud Shell | Azure Bastion (preview) |
|---|---|---|
| Key differences | • Ephemeral, browser-based access. • Cost-effective. • Comes with preinstalled tools like `az cli` and `kubectl` . |
• Persistent, long-running access. • Suited for managing multiple clusters. • Use your own native client tooling. |
| Limitations | • Not supported with AKS Automatic clusters or clusters with network resource group (NRG) lockdown. • You can't have multiple Cloud Shell sessions in different VNets at the same time. |
• Not supported with AKS Automatic clusters or clusters with NRG lockdown. |

## Connect using Azure Cloud Shell

Connecting to a private AKS cluster through Azure Cloud Shell requires completing the following steps:

**Deploy required resources:**You need to deploy Cloud Shell in a VNet that can reach your private cluster. This step provisions the necessary infrastructure. While Cloud Shell is a free service, using Cloud Shell in a VNet requires some resources that incur cost. For more information, see[Deploy Cloud Shell in a virtual network](/en-us/azure/cloud-shell/vnet/deployment).**Configure the connection:**After you deploy the resources, any user in the subscription that has appropriate permissions on the cluster can configure Cloud Shell to deploy in the VNet to allow a secure connection to the private cluster.

## Deploy required resources

To deploy and configure the required resources, you must have the **Owner** role assignment on the subscription. To view and assign roles, see [List Owners of a Subscription](/en-us/azure/role-based-access-control/role-assignments-list-portal#list-owners-of-a-subscription).

You can deploy the required resources using the Azure portal or the provided ARM template if you manage infrastructure as code or have organizational policies that require specific resource naming conventions.

You can optionally leave the deployed resources in place for future connections or delete and recreate them as needed.

### Use the Azure portal (preview)

This option creates a separate VNet with the necessary resources for Cloud Shell and configures VNet peering for you.

- In the
[Azure portal](https://portal.azure.com), navigate to your private cluster resource. - On the Overview page, select
**Connect**. - On the
**Cloud Shell**tab, under**Prerequisites for private cluster connection**, select**Configure**to deploy the necessary resources.- The deployment creates a new resource group named
`RG-CloudShell-PrivateClusterConnection-{RANDOM_ID}`

.

- The deployment creates a new resource group named
- Once the deployment succeeds, under
**Set cluster context**, select**Open Cloud Shell**.


Note

If you already configured Cloud Shell in a VNet for a particular cluster, repeating these steps ensures your Cloud Shell user settings are correctly aligned with that VNet.

### Use an ARM template

To have more control over the deployment configuration, use the [provided ARM template](/en-us/azure/cloud-shell/vnet/deployment).

You can deploy Cloud Shell in the same VNet as your AKS private cluster with a dedicated subnet, or you can deploy in a new VNet and connect via [VNet peering](/en-us/azure/virtual-network/virtual-network-peering-overview).

## Configure connection to the private cluster

After you [deploy the required resources](#deploy-required-resources), any user in the subscription can configure their Cloud Shell to deploy in the given VNet using the steps in [Configure Cloud Shell to use a virtual network](/en-us/azure/cloud-shell/vnet/deployment#5-configure-cloud-shell-to-use-a-virtual-network).

Ensure the user has appropriate Kubernetes-level access to successfully connect to the private cluster. For more information, see [Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).

## Connect using Azure Bastion (preview)

Azure Bastion is a fully managed PaaS service that you provision to securely connect to private resources via private IP addresses. To use Bastion's native client tunneling feature, see [Connect to AKS private cluster using Azure Bastion](/en-us/azure/bastion/bastion-connect-to-aks-private-cluster).

## Connect using virtual network (VNet) peering

To use VNet peering, you need to set up a link between the VNet and the private DNS zone. You can set up VNet peering using either the Azure portal or the Azure CLI.

### Use the Azure portal

In the

[Azure portal](https://portal.azure.com), navigate to your node resource group and select your**private DNS zone resource**.In the service menu, under

**DNS Management**, select**Virtual Network Links**>**Add**.On the

**Add Virtual Network Link**page, configure the following settings:**Link name**: Enter a name for the virtual network link.**Virtual Network**: Select the virtual network that contains the VM.

Select

**Create**to create the virtual network link.Navigate to the resource group that contains the virtual network of your AKS cluster and select your

**virtual network resource**.In the service menu, under

**Settings**, select**Peerings**>**Add**.On the

**Add peering**page, configure the following settings:**Peering link name**: Enter a name for the peering link.**Virtual network**: Select the virtual network of the VM.

Select

**Add**to create the peering link.

For more information, see [Virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview).

### Use the Azure CLI

Create a new link to add the virtual network of the VM to the private DNS zone using the

command.`az network private-dns link vnet create`

`az network private-dns link vnet create \ --name <new-link-name> \ --resource-group <node-resource-group-name> \ --zone-name <private-dns-zone-name> \ --virtual-network <vm-virtual-network-resource-id> \ --registration-enabled false`

Create a peering between the virtual network of the VM and the virtual network of the node resource group using the

command.`az network vnet peering create`

`az network vnet peering create \ --name <new-peering-name-1> \ --resource-group <vm-virtual-network-resource-group-name> \ --vnet-name <vm-virtual-network-name> \ --remote-vnet <node-resource-group-virtual-network-resource-id> \ --allow-vnet-access`

Create a second peering between the virtual network of the node resource group and the virtual network of the VM using the

command.`az network vnet peering create`

`az network vnet peering create \ --name <new-peering-name-2> \ --resource-group <node-resource-group-name> \ --vnet-name <node-resource-group-virtual-network-name> \ --remote-vnet <vm-virtual-network-resource-id> \ --allow-vnet-access`

List the virtual network peerings you created using the

command.`az network vnet peering list`

`az network vnet peering list \ --resource-group <node-resource-group-name> \ --vnet-name <private-dns-zone-name>`


## Use a private endpoint connection

You can set up a private endpoint so that a VNet doesn't need to be peered to communicate with the private cluster. To set up a private endpoint connection, you first create a new private endpoint in the virtual network containing the consuming resources, and then create a link between your virtual network and a new private DNS zone in the same network.

Important

If the virtual network is configured with custom DNS servers, you need to set up private DNS appropriately for the environment. For more information, see the [Virtual network name resolution documentation](/en-us/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#name-resolution-that-uses-your-own-dns-server).

### Create a private endpoint resource

From the

[Azure portal home page](https://portal.azure.com), select**Create a resource**.Search for

**Private Endpoint**and select**Create**>**Private Endpoint**.Select

**Create**.On the

**Basics**tab, configure the following settings:**Project details****Subscription**: Select the subscription where your private cluster is located.**Resource group**: Select the resource group that contains your virtual network.

**Instance details****Name**: Enter a name for your private endpoint, such as*myPrivateEndpoint*.**Region**: Select the same region as your virtual network.


Select

**Next: Resource**and configure the following settings:**Connection method**: Select**Connect to an Azure resource in my directory**.**Subscription**: Select the subscription where your private cluster is located.**Resource type**: Select**Microsoft.ContainerService/managedClusters**.**Resource**: Select your private cluster.**Target sub-resource**: Select**management**.

Select

**Next: Virtual Network**and configure the following settings:**Networking****Virtual network**: Select your virtual network.**Subnet**: Select your subnet.


Select

**Next: DNS**>**Next: Tags**and (optionally) set up key-values as needed.Select

**Next: Review + create**>**Create**.

Once the resource is created, record the private IP address of the private endpoint for future use.

### Create a private DNS zone

Once you create the private endpoint, create a new private DNS zone with the same name as the private DNS zone created by the private cluster. Remember to create this DNS zone in the VNet containing the consuming resources.

In the Azure portal, navigate to your node resource group and select your

**private DNS zone resource**.In the service menu, under

**DNS Management**, select**Recordsets**and note the following:- The name of the private DNS zone, which follows the pattern
`*.privatelink.<region>.azmk8s.io`

. - The name of the
`A`

record (excluding the private DNS name). - The time-to-live (TTL).

- The name of the private DNS zone, which follows the pattern
From the

[Azure portal home page](https://portal.azure.com), select**Create a resource**.Search for

**Private DNS zone**and select**Create**>**Private DNS zone**.On the

**Basics**tab, configure the following settings:**Project details**- Select your
**Subscription**. - Select the
**Resource group**where you created the private endpoint.

- Select your
**Instance details****Name**: Enter the name of the DNS zone retrieved from previous steps.**Region**: Defaults to the location of your resource group.


Select

**Review + create**>**Create**.

### Create an `A`

record

Once the private DNS zone is created, create an `A`

record, which associates the private endpoint to the private cluster.

Navigate to your private DNS zone resource.

In the service menu, under

**DNS Management**, select**Recordsets**>**Add**.On the

**Add record set**page, configure the following settings:**Name**: Enter the name retrieved from the`A`

record in the private cluster's DNS zone.**Type**: Select**A - Address record**.**TTL**: Enter the number from the`A`

record in the private cluster's DNS zone.**TTL unit**: Change the dropdown value to match the one in the`A`

record from the private cluster's DNS zone.**IP address**: Enter the**IP address of the private endpoint you created**.

Select

**Add**to create the`A`

record.

Important

When creating the `A`

record, only use the name and not the fully qualified domain name (FQDN).

### Link the private DNS zone to the virtual network

Once the `A`

record is created, link the private DNS zone to the virtual network that will access the private cluster.

Navigate to your private DNS zone resource.

In the service menu, under

**DNS Management**, select**Virtual Network Links**>**Add**.On the

**Add Virtual Network Link**page, configure the following settings:**Link name**: Enter a name for your virtual network link.**Subscription**: Select the subscription where your private cluster is located.**Virtual Network**: Select the virtual network of your private cluster.

Select

**Create**to create the link.It might take a few minutes for the operation to complete. Once the virtual network link is created, you can access it from the

**Virtual Network Links**tab you used in step 2.

Warning

- If the private cluster is stopped and restarted, the private cluster's original private link service is removed and recreated, which breaks the connection between your private endpoint and the private cluster. To resolve this issue, delete and recreate any user-created private endpoints linked to the private cluster. If the recreated private endpoints have new IP addresses, you also need to update DNS records.
- If you update the DNS records in the private DNS zone, ensure the host that you're trying to connect from is using the updated DNS records. You can verify this using the
`nslookup`

command. If you notice the updates aren't reflected in the output, you might need to flush the DNS cache on your machine and try again.

## Create a VM in the same virtual network

To create a VM in the same VNet as your private AKS cluster, use the [ az vm create](/en-us/cli/azure/vm#az-vm-create) command with the

`--vnet-name`

flag to specify the VNet.```
az vm create \
--resource-group <resource-group-name> \
--name <vm-name> \
--image <image-name> \
--vnet-name <vm-virtual-network-name> \
--subnet <subnet-name> \
--admin-username <admin-username> \
--admin-password <admin-password>
```


## Use an Express Route or VPN connection

To use an Express Route or VPN connection, see [About ExpressRoute virtual network gateways](/en-us/azure/expressroute/expressroute-about-virtual-network-gateways).

## Use the AKS `command invoke`

feature

To use the AKS `command invoke`

feature to connect to a private cluster, see [Access a private cluster using command invoke](access-private-cluster).

## Related content

For more information about private clusters in AKS, see [Create a private Azure Kubernetes Service (AKS) cluster](private-clusters).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/internal-lb -->

# Use an internal load balancer with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can create and use an internal load balancer to restrict access to your applications in Azure Kubernetes Service (AKS). An internal load balancer doesn't have a public IP and makes a Kubernetes service accessible only to applications that can reach the private IP. These applications can be within the same virtual network or in another virtual network through virtual network peering. This article shows you how to create and use an internal load balancer with AKS.

Important

On September 30, 2025, Basic Load Balancer will be retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). There's no integrated option to use the Azure AKS API operation to migrate the Load Balancer SKU. The Load Balancer SKU decision must be done at cluster creation time. Therefore, if you're currently using Basic Load Balancer, take the necessary steps to migrate your workloads to a new created cluster with the new default Standard Load Balancer SKU prior to the retirement date.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.0.59 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you want to use an existing subnet or resource group, the AKS cluster identity needs permission to manage network resources. For information, see
[Configure Azure CNI networking in AKS](configure-azure-cni). If you're configuring your load balancer to use an[IP address in a different subnet](#specify-a-different-subnet), ensure the AKS cluster identity also has`Read`

access to that subnet.- For more information on permissions, see
[Delegate AKS access to other Azure resources](kubernetes-service-principal#delegate-access-to-other-azure-resources).

- For more information on permissions, see

## Create an internal load balancer

Create a service manifest named

`internal-lb.yaml`

with the service type`LoadBalancer`

and the`azure-load-balancer-internal`

annotation.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`

Deploy the internal load balancer using the

command. This command creates an Azure load balancer in the node resource group connected to the same virtual network as your AKS cluster.`kubectl apply`

`kubectl apply -f internal-lb.yaml`

View the service details using the

`kubectl get service`

command.`kubectl get service internal-app`

The IP address of the internal load balancer is shown in the

`EXTERNAL-IP`

column, as shown in the following example output. In this context,*External*refers to the external interface of the load balancer. It doesn't mean that it receives a public, external IP address. This IP address is dynamically assigned from the same subnet as the AKS cluster.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE internal-app LoadBalancer 10.0.248.59 10.240.0.7 80:30555/TCP 2m`


## Specify an IP address

When you specify an IP address for the load balancer, the specified IP address must reside in the same virtual network as the AKS cluster, but it can't already be assigned to another resource in the virtual network. For example, you shouldn't use an IP address in the range designated for the Kubernetes subnet within the AKS cluster. Using an IP address that's already assigned to another resource in the same virtual network can cause issues with the load balancer.

You can use the [ az network vnet subnet list](/en-us/cli/azure/network/vnet/subnet#az-network-vnet-subnet-list) Azure CLI command or the

[PowerShell cmdlet to get the subnets in your virtual network.](/en-us/powershell/module/az.network/get-azvirtualnetworksubnetconfig)

`Get-AzVirtualNetworkSubnetConfig`

For more information on subnets, see [Add a node pool with a unique subnet](node-pool-unique-subnet).

If you want to use a specific IP address with the load balancer, you have two options: **set service annotations** or **add the LoadBalancerIP property to the load balancer YAML manifest**.

Important

Adding the *LoadBalancerIP* property to the load balancer YAML manifest is deprecating following [upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235). While current usage remains the same and existing services are expected to work without modification, we **highly recommend setting service annotations** instead. For more information about service annotations, see [Azure LoadBalancer supported annotations](https://cloud-provider-azure.sigs.k8s.io/topics/loadbalancer/#loadbalancer-annotations).

Set service annotations using

`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-ipv4: 10.240.0.25 service.beta.kubernetes.io/azure-load-balancer-internal: "true" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`


View the service details using the

`kubectl get service`

command.`kubectl get service internal-app`

The IP address in the

`EXTERNAL-IP`

column should reflect your specified IP address, as shown in the following example output:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE internal-app LoadBalancer 10.0.184.168 10.240.0.25 80:30225/TCP 4m`


For more information on configuring your load balancer in a different subnet, see [Specify a different subnet](#specify-a-different-subnet).

## Connect Azure Private Link service to internal load balancer

### Before you begin

- You need Kubernetes version 1.22.x or later.
- You need an existing resource group with a virtual network and subnet. This resource group is where you
[create the private endpoint](#create-a-private-endpoint-to-the-private-link-service). If you don't have these resources, see[Create a virtual network and subnet](configure-kubenet#create-a-virtual-network-and-subnet).

### Create a Private Link service connection

Create a service manifest named

`internal-lb-pls.yaml`

with the service type`LoadBalancer`

and the`azure-load-balancer-internal`

and`azure-pls-create`

annotations. For more options, refer to the[Azure Private Link Service Integration](https://kubernetes-sigs.github.io/cloud-provider-azure/topics/pls-integration/)design document.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true" service.beta.kubernetes.io/azure-pls-create: "true" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`

Deploy the internal load balancer using the

command. This command creates an Azure load balancer in the node resource group connected to the same virtual network as your AKS cluster. It also creates a Private Link Service object that connects to the frontend IP configuration of the load balancer associated with the Kubernetes service.`kubectl apply`

`kubectl apply -f internal-lb-pls.yaml`

View the service details using the

`kubectl get service`

command.`kubectl get service internal-app`

The IP address of the internal load balancer is shown in the

`EXTERNAL-IP`

column, as shown in the following example output. In this context,*External*refers to the external interface of the load balancer. It doesn't mean that it receives a public, external IP address.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE internal-app LoadBalancer 10.125.17.53 10.125.0.66 80:30430/TCP 64m`

View the details of the Private Link Service object using the

command.`az network private-link-service list`

`# Create a variable for the node resource group AKS_MC_RG=$(az aks show -g myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv) # View the details of the Private Link Service object az network private-link-service list -g $AKS_MC_RG --query "[].{Name:name,Alias:alias}" -o table`

Your output should look similar to the following example output:

`Name Alias -------- ------------------------------------------------------------------------- pls-xyz pls-xyz.abc123-defg-4hij-56kl-789mnop.eastus2.azure.privatelinkservice`


### Create a Private Endpoint to the Private Link service

A Private Endpoint allows you to privately connect to your Kubernetes service object via the Private Link Service you created.

Create the private endpoint using the

command.`az network private-endpoint create`

`# Create a variable for the private link service AKS_PLS_ID=$(az network private-link-service list -g $AKS_MC_RG --query "[].id" -o tsv) # Create the private endpoint $ az network private-endpoint create \ -g myOtherResourceGroup \ --name myAKSServicePE \ --vnet-name myOtherVNET \ --subnet pe-subnet \ --private-connection-resource-id $AKS_PLS_ID \ --connection-name connectToMyK8sService`


### PLS Customizations via Annotations

You can use the following annotations to customize the PLS resource:

| Annotation | Value | Description | Required | Default |
|---|---|---|---|---|
`service.beta.kubernetes.io/azure-pls-create` |
`"true"` |
Boolean indicating whether a PLS needs to be created. | Required | |
`service.beta.kubernetes.io/azure-pls-name` |
`<PLS name>` |
String specifying the name of the PLS resource to be created. | Optional | `"pls-<LB frontend config name>"` |
`service.beta.kubernetes.io/azure-pls-resource-group` |
`Resource Group name` |
String specifying the name of the Resource Group where the PLS resource is created | Optional | `MC_ resource` |
`service.beta.kubernetes.io/azure-pls-ip-configuration-subnet` |
`<Subnet name>` |
String indicating the subnet to which the PLS is deployed. This subnet must exist in the same virtual network as the backend pool. PLS NAT IPs are allocated within this subnet. | Optional | If `service.beta.kubernetes.io/azure-load-balancer-internal-subnet` , this ILB subnet is used. Otherwise, the default subnet from config file is used. |
`service.beta.kubernetes.io/azure-pls-ip-configuration-ip-address-count` |
`[1-8]` |
Total number of private NAT IPs to allocate. | Optional | 1 |
`service.beta.kubernetes.io/azure-pls-ip-configuration-ip-address` |
`"10.0.0.7 ... 10.0.0.10"` |
A space separated list of static IPv4 IPs to be allocated. (IPv6 isn't supported right now.) Total number of IPs shouldn't be greater than the ip count specified in `service.beta.kubernetes.io/azure-pls-ip-configuration-ip-address-count` . If there are fewer IPs specified, the rest are dynamically allocated. The first IP in the list is set as `Primary` . |
Optional | All IPs are dynamically allocated. |
`service.beta.kubernetes.io/azure-pls-proxy-protocol` |
`"true"` or `"false"` |
Boolean indicating whether the TCP PROXY protocol should be enabled on the PLS to pass through connection information, including the link ID and source IP address. The backend service MUST support the PROXY protocol or the connections fails. | Optional | `false` |
`service.beta.kubernetes.io/azure-pls-visibility` |
`"sub1 sub2 sub3 … subN"` or `"*"` |
A space separated list of Azure subscription IDs for which the private link service is visible. Use `"*"` to expose the PLS to all subs (Least restrictive). |
Optional | Empty list `[]` indicating role-based access control only: This private link service is only available to individuals with role-based access control permissions within your directory. (Most restrictive) |
`service.beta.kubernetes.io/azure-pls-auto-approval` |
`"sub1 sub2 sub3 … subN"` |
A space separated list of Azure subscription IDs. This allows PE connection requests from the subscriptions listed to the PLS to be automatically approved. This only works when visibility is set to `"*"` . |
Optional | `[]` |

## Use private networks

When you create your AKS cluster, you can specify advanced networking settings. These settings allow you to deploy the cluster into an existing Azure virtual network and subnets. For example, you can deploy your AKS cluster into a private network connected to your on-premises environment and run services that are only accessible internally.

For more information, see [configure your own virtual network subnets with Kubenet](configure-kubenet) or [with Azure CNI](configure-azure-cni).

You don't need to make any changes to the previous steps to deploy an internal load balancer that uses a private network in an AKS cluster. The load balancer is created in the same resource group as your AKS cluster, but it's instead connected to your private virtual network and subnet, as shown in the following example:

```
$ kubectl get service internal-app
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
internal-app LoadBalancer 10.1.15.188 10.0.0.35 80:31669/TCP 1m
```


Note

The cluster identity used by the AKS cluster must at least have the [Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor) role on the virtual network resource. You can view the cluster identity using the [ az aks show](/en-us/cli/azure/aks#az-aks-show) command, such as

`az aks show --resource-group <resource-group-name> --name <cluster-name> --query "identity"`

. You can assign the Network Contributor role using the [command, such as](/en-us/cli/azure/role/assignment#az-role-assignment-create)

`az role assignment create`

`az role assignment create --assignee <identity-resource-id> --scope <virtual-network-resource-id> --role "Network Contributor"`

.If you want to define a [custom role](/en-us/azure/role-based-access-control/custom-roles-cli) instead, you need the following permissions:

`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


For more information, see [Add, change, or delete a virtual network subnet](/en-us/azure/virtual-network/virtual-network-manage-subnet).

### Specify a different subnet

Add the

`azure-load-balancer-internal-subnet`

annotation to your service to specify a subnet for your load balancer. The subnet specified must be in the same virtual network as your AKS cluster. When deployed, the load balancer`EXTERNAL-IP`

address is part of the specified subnet.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true" service.beta.kubernetes.io/azure-load-balancer-internal-subnet: "apps-subnet" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`


## Delete the load balancer

The load balancer is deleted when all of its services are deleted.

As with any Kubernetes resource, you can directly delete a service, such as `kubectl delete service internal-app`

, which also deletes the underlying Azure load balancer.

## Next steps

To learn more about Kubernetes services, see the [Kubernetes services documentation](https://kubernetes.io/docs/concepts/services-networking/service/).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-monitoring -->

# Monitor and visualize AI inference metrics on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Monitoring and observability play a key role in maintaining high performance and low cost of your AI workload deployments in Azure Kubernetes Service (AKS). Visibility into system and performance metrics can indicate the limits of your underlying infrastructure and motivate real-time adjustments and optimizations to reduce workload interruptions. Monitoring also provides valuable insights into resource utilization for cost-effective management of computational resources and accurate provisioning.

The Kubernetes AI Toolchain Operator (KAITO) is a managed add-on for AKS that simplifies deployment and operations for AI models in your AKS cluster.

In [KAITO version 0.4.4](https://github.com/kaito-project/kaito/releases/tag/v0.4.4) and later versions, the vLLM inference runtime is enabled by default in the AKS managed add-on. [vLLM](https://docs.vllm.ai/en/latest/) is a library for language model inference and serving. It surfaces key system performance, resource usage, and request processing for [Prometheus metrics](https://docs.vllm.ai/en/latest/design/v1/metrics.html) that you can use to evaluate your KAITO inference deployments.

In this article, you'll learn how to monitor and visualize vLLM inference metrics using the AI toolchain operator add-on with Azure Managed Prometheus and Azure Managed Grafana on your AKS cluster.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Install and configure Azure CLI version 2.47.0 or later. To find your version, run
`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

## Prerequisites

- Install and configure kubectl, the Kubernetes command-line client. For more information, see
[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - Enable the
[AI toolchain operator add-on](ai-toolchain-operator)in your AKS cluster. - If you already have the AI toolchain operator add-on enabled, update your AKS cluster to the latest version to run KAITO v0.4.4 or later.
- Enable
[the managed service for Prometheus and Azure Managed Grafana](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable)in your AKS cluster. - Have permissions to
[create or update Azure Managed Grafana instances](/en-us/azure/managed-grafana/how-to-manage-access-permissions-users-identities)in your Azure subscription.

## Deploy a KAITO inference service

In this example, you collect metrics for the [Qwen-2.5-coder-7B-instruct language model](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml).

Start by applying the following KAITO workspace custom resource to your cluster:

`kubectl apply -f https://raw.githubusercontent.com/Azure/kaito/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml`

Track the live resource changes in your KAITO workspace:

`kubectl get workspace workspace-qwen-2-5-coder-7b-instruct -w`

Note

Machine readiness can take up to 10 minutes, and workspace readiness can take up to 20 minutes depending on the size of your language model.

Confirm that your inference service is running and get the service IP address:

`export SERVICE_IP=$(kubectl get svc workspace-qwen-2-5-coder-7b-instruct -o jsonpath='{.spec.clusterIP}') echo $SERVICE_IP`


## Surface KAITO inference metrics to the managed service for Prometheus

Prometheus metrics are collected by default at the KAITO [ /metrics endpoint](https://github.com/kaito-project/kaito/tree/main).

Add the following label to your KAITO inference service so that a Kubernetes

`ServiceMonitor`

deployment can detect it:`kubectl label svc workspace-qwen-2-5-coder-7b-instruct App=qwen-2-5-coder`

Create a

`ServiceMonitor`

resource to define the inference service endpoints and the required configurations to scrape the vLLM Prometheus metrics. Export these metrics to the managed service for Prometheus by deploying the following`ServiceMonitor`

YAML manifest in the`kube-system`

namespace:`cat <<EOF | kubectl apply -n kube-system -f - apiVersion: azmonitoring.coreos.com/v1 kind: ServiceMonitor metadata: name: prometheus-kaito-monitor spec: selector: matchLabels: App: qwen-2-5-coder endpoints: - port: http interval: 30s path: /metrics scheme: http EOF`

Check for the following output to verify that

`ServiceMonitor`

is created:`servicemonitor.azmonitoring.coreos.com/prometheus-kaito-monitor created`

Verify that your

`ServiceMonitor`

deployment is running successfully:`kubectl get servicemonitor prometheus-kaito-monitor -n kube-system`

In the Azure portal, verify that vLLM metrics are successfully collected in the managed service for Prometheus.

In your Azure Monitor workspace, go to

**Managed Prometheus**>**Prometheus explorer**.Select the

**Grid**tab and confirm that a metrics item is associated with the job named`workspace-qwen-2-5-coder-7b-instruct`

.Note

The

`up`

value of this item should be`1`

. A value of`1`

indicates that Prometheus metrics are successfully being scraped from your AI inference service endpoint.


## Visualize KAITO inference metrics in Azure Managed Grafana

The vLLM project provides a Grafana dashboard configuration named

[grafana.json](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)for inference workload monitoring. Navigate to the bottom of this[page](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)and copy the entire contents of the`grafana.json`

file.Go to the bottom of the

[examples page](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)and copy the entire contents of the`grafana.json`

file:Complete the steps to

[import the Grafana configurations into a new dashboard](/en-us/azure/managed-grafana/how-to-create-dashboard#import-a-json-dashboard)in Azure Managed Grafana.Go to your Managed Grafana endpoint, view the available dashboards, and select the

**vLLM**dashboard.To begin collecting data for your selected model deployment, confirm that the

**datasource**value shown at the top left of the Grafana dashboard is your instance of the managed service for Prometheus you created for this example.Copy the inference preset name defined in your KAITO workspace to the

**model_name**field in the Grafana dashboard. In this example, the model name is[qwen2.5-coder-7b-instruct](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml).In a few moments, verify that the metrics for your KAITO inference service appear in the vLLM Grafana dashboard.

Note

The value of these inference metrics remains

**0**until the requests are submitted to the model inference server.

## Related content

[Monitor and visualize](monitor-aks)your AKS deployments at scale.- Test and monitor
[tool calling with KAITO inference](ai-toolchain-operator-tool-calling)on your cluster. [Fine-tune an AI model](ai-toolchain-operator-fine-tune)by using the AI toolchain operator add-on in AKS.- Learn about AKS GPU workload deployment options on
[Linux](gpu-cluster)and[Windows](use-windows-gpu)nodes.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-containerd -->

# Create Windows Server node pools with containerd in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For Kubernetes version 1.20 and higher, you can specify [ containerd](https://containerd.io/) as the container runtime for Windows Server 2019 node pools. Starting with Kubernetes 1.23,

`containerd`

is the default and only container runtime for Windows.In this article, you learn how to create Windows Server node pools with `containerd`

in Azure Kubernetes Service (AKS).

## Prerequisites

[Azure CLI](/en-us/cli/azure/install-azure-cli)installed and configured. Find the version using the`az version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).- An existing AKS cluster with a system node pool. If you need to create one, see
[Create an AKS cluster with a single node pool](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli).

## Limitations and considerations

When using Windows Server node pools with `containerd`

, keep the following limitations and considerations in mind:

- Both the control plane and Windows Server 2019 node pools must use Kubernetes version 1.20 or greater.
- When you create or update a node pool to run Windows Server containers, the default value for
`--node-vm-size`

is`Standard_D2s_v3`

, which was the minimum recommended size for Windows Server 2019 node pools up to Kubernetes version 1.20. The minimum recommended size for Windows Server 2019 node pools using`containerd`

is`Standard_D4s_v3`

. When setting the`--node-vm-size`

parameter, check the[list of restricted virtual machine (VM) sizes](/en-us/azure/virtual-machines/sizes/overview). - We recommend using
[taints or labels](manage-node-pools#set-node-pool-taints)with your Windows Server 2019 node pools running`containerd`

and tolerations or node selectors with your deployments to guarantee your workloads are scheduled correctly.

## Add a Windows Server node pool with `containerd`


Add a Windows Server node pool with

`containerd`

into your existing cluster using the [`az aks nodepool add`

][az-aks-nodepool-add].Note

If you don't specify the

`WindowsContainerRuntime=containerd`

custom header, the node pool still uses`containerd`

as the container runtime by default.`az aks nodepool add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --os-type Windows \ --name $CONTAINER_D_NODE_POOL_NAME \ --node-vm-size Standard_D4s_v3 \ --kubernetes-version 1.20.5 \ --aks-custom-headers WindowsContainerRuntime=containerd \ --node-count 1`


## Upgrade an existing Windows Server node pool to `containerd`


Upgrade a specific node pool from Docker to

`containerd`

using the [`az aks nodepool upgrade`

][az-aks-nodepool-upgrade] command.`export CONTAINER_D_NODE_POOL_NAME="mywindowsnodepool" az aks nodepool upgrade \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name $CONTAINER_D_NODE_POOL_NAME \ --kubernetes-version 1.20.7 \ --aks-custom-headers WindowsContainerRuntime=containerd`


## Upgrade all existing Windows Server node pools to `containerd`


Upgrade all node pools from Docker to

`containerd`

using the [`az aks nodepool upgrade`

][az-aks-nodepool-upgrade] command.`az aks nodepool upgrade \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --kubernetes-version 1.20.7 \ --aks-custom-headers WindowsContainerRuntime=containerd`


## Next steps

For more information about node pools in AKS, see [Manage node pools for a cluster in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/delete-node-pool -->

# Delete an Azure Kubernetes Service (AKS) node pool

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article outlines node pool deletion in Azure Kubernetes Service (AKS), including what happens when you delete a node pool and how to delete a node pool.

## What happens when you delete a node pool?

When you delete a node pool, the following resources are deleted:

- The virtual machine scale set (VMSS) and virtual machines (VMs) for each node in the node pool
- Any node instances in the node pool along with any pods running on those nodes

## Delete a node pool

Important

Keep the following information in mind when deleting a node pool:

**You can't recover a node pool after it's deleted**. You need to create a new node pool and redeploy your applications.

Delete a node pool using the [ az aks nodepool delete](/en-us/cli/azure/aks#az-aks-nodepool-delete) command.

```
az aks nodepool delete \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--name <node-pool-name>
```


To verify that the node pool was deleted successfully, use the `kubectl get nodes`

command to confirm that the nodes in the node pool no longer exist.

## Ignore PodDisruptionBudgets (PDBs) when removing an existing node pool

If your cluster has PodDisruptionBudgets that are preventing the deletion of the node pool, you can ignore the PodDisruptionBudget requirements by setting `--ignore-pod-disruption-budget`

to `true`

. To learn more about PodDisruptionBudgets, see:

[Plan for availability using a pod disruption budget](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets)[Specifying a Disruption Budget for your Application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)[Disruptions](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/)

Delete an existing node pool without following any PodDisruptionBudgets set on the cluster using the

command with the`az aks nodepool delete`

`--ignore-pod-disruption-budget`

flag set to`true`

:`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1 \ --ignore-pod-disruption-budget true`

To verify that the node pool was deleted successfully, use the

`kubectl get nodes`

command to confirm that the nodes in the node pool no longer exist.

## Remove specific VMs in an existing node pool

Note

When you delete a VM with this command, AKS doesn't perform cordon and drain. To minimize the disruption of rescheduling pods currently running on the VM you plan to delete, perform a cordon and drain on the VM before deleting. You can learn more about how to cordon and drain using the example scenario provided in the resizing node pools tutorial.

List the existing nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-mynodepool-20823458-vmss000000 Ready agent 63m v1.21.9 aks-mynodepool-20823458-vmss000001 Ready agent 63m v1.21.9 aks-mynodepool-20823458-vmss000002 Ready agent 63m v1.21.9`

Delete the specified VMs using the

command. Make sure to replace the placeholders with your own values.`az aks nodepool delete-machines`

`az aks nodepool delete-machines \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --machine-names <vm-name-1> <vm-name-2>`

Verify the VMs were successfully deleted using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should no longer include the VMs that you specified in the

`az aks nodepool delete-machines`

command.

## Next steps

For more information about adjusting node pool sizes in AKS, see [Resize node pools](resize-node-pool).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/artifact-streaming -->

# Reduce image pull time with Artifact Streaming on Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

High performance compute workloads often involve large images, which can cause long image pull times and slow down your workload deployments. Artifact Streaming on AKS allows you to stream container images from Azure Container Registry (ACR) to AKS. AKS only pulls the necessary layers for initial pod startup, reducing the time it takes to pull images and deploy your workloads.

Artifact Streaming can reduce time to pod readiness by over 15%, depending on the size of the image, and it works best for images <30GB. Based on our testing, we saw reductions in pod start-up times for images <10GB from minutes to seconds. If you have a pod that needs access to a large file (>30GB), then you should mount it as a volume instead of building it as a layer. This is because if your pod requires that file to start, it congests the node. Artifact Streaming isn't ideal for read heavy images from your filesystem if you need that on startup. With Artifact Streaming, pod start-up becomes concurrent, whereas without it, pods start in serial.

This article describes how to enable the Artifact Streaming feature on your AKS node pools to stream artifacts from ACR.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

Important

Artifact Streaming (preview) is a suggested alternative for customers previously using Teleport (preview).
[Teleport (preview)](https://github.com/Azure/acr/blob/main/docs/teleport/aks-getting-started.md) on AKS will be retired on 15 July 2025. Please migrate to Artifact Streaming (preview) on AKS or update your node pools to set `--aks-custom-headers EnableACRTeleport=false`

.
Azure Container Registry removed the Teleport API, meaning that any nodes with Teleport enabled will pull images from Azure Container Registry like any other AKS node without Teleport.
After 15 July 2025, AKS node pools with Teleport enabled might experience breakage and node provisioning failures. For more information, see [aka.ms/aks/teleport-retirement](https://aka.ms/aks/teleport-retirement).

## Limitations

- Artifact Steaming isn't supported for the following OS options:
[Windows Server versions](windows-best-practices),[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks), and[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard).

## Prerequisites

- You need an existing AKS cluster with ACR integration. If you don't have one, you can create one using
[Authenticate with ACR from AKS](cluster-container-registry-integration). [Enable Artifact Streaming on ACR](#enable-artifact-streaming-on-acr).- This feature requires Kubernetes version 1.25 or later. To check your AKS cluster version, see
[Check for available AKS cluster upgrades](upgrade-cluster).

Note

Artifact Streaming is only supported on Ubuntu 22.04, Ubuntu 20.04, and Azure Linux node pools. Windows node pools aren't supported.

## Install the `aks-preview`

CLI extension

Install the

`aks-preview`

CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update the extension to ensure you have the latest version installed using the

command.`az extension update`

`az extension update --name aks-preview`


## Register the `ArtifactStreamingPreview`

feature flag in your subscription

Register the

`ArtifactStreamingPreview`

feature flag in your subscription using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name ArtifactStreamingPreview`


## Enable Artifact Streaming on ACR

Enablement on ACR is a prerequisite for Artifact Streaming on AKS. For more information, see [Artifact Streaming on ACR](https://aka.ms/acr/artifact-streaming).

Create an Azure resource group to hold your ACR instance using the

command.`az group create`

`az group create --name myStreamingTest --location westus`

Create a new premium SKU Azure Container Registry using the

command with the`az acr create`

`--sku Premium`

flag.`az acr create --resource-group myStreamingTest --name mystreamingtest --sku Premium`

Configure the default ACR instance for your subscription using the

command.`az configure`

`az configure --defaults acr="mystreamingtest"`

Push or import an image to the registry using the

command.`az acr import`

`az acr import --source docker.io/jupyter/all-spark-notebook:latest --repository jupyter/all-spark-notebook:latest`

Create a streaming artifact from the image using the

command.`az acr artifact-streaming create`

`az acr artifact-streaming create --image jupyter/all-spark-notebook:latest`

Verify the generated Artifact Streaming using the

command.`az acr manifest list-referrers`

`az acr manifest list-referrers --name jupyter/all-spark-notebook:latest`


## Enable Artifact Streaming on AKS

### Enable Artifact Streaming on a new node pool

Create a new node pool with Artifact Streaming enabled using the

command with the`az aks nodepool add`

`--enable-artifact-streaming`

.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myNodePool \ --enable-artifact-streaming`


### Enable Artifact Streaming on an existing node pool

Update an existing node pool to enable Artifact Streaming using the

command with the`az aks nodepool update`

`--enable-artifact-streaming`

.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myNodePool \ --enable-artifact-streaming`


## Check if Artifact Streaming is enabled

Now that you enabled Artifact Streaming on a premium ACR and connected that to an AKS node pool with Artifact Streaming enabled, any new pod deployments on this cluster with an image pull from the ACR with Artifact Streaming enabled will see reductions in image pull times.

Check if your node pool has Artifact Streaming enabled using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --name myNodePool --query artifactStreamingProfile`

In the output, check that the

`Enabled`

field is set to`true`

.

## Next steps

This article described how to enable Artifact Streaming on your AKS node pools to stream artifacts from ACR and reduce image pull time. To learn more about working with container images in AKS, see [Best practices for container image management and security in AKS](operator-best-practices-container-image-management).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quickstart-dapr -->

# Quickstart: Deploy an application using the Dapr cluster extension for Azure Kubernetes Service (AKS) or Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use the [Dapr cluster extension](dapr-overview) in an AKS or Arc-enabled Kubernetes cluster. You deploy [a hello world example](https://github.com/Azure-Samples/dapr-aks-extension-quickstart), which consists of a Python application that generates messages and a Node.js application that consumes and persists the messages.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.- An AKS Cluster with:
[Workload identity](workload-identity-deploy-cluster#deploy-and-configure-microsoft-entra-workload-id-on-an-azure-kubernetes-service-aks-cluster)enabled[Managed identity](workload-identity-deploy-cluster#create-a-managed-identity)created in the same subscription[A Kubernetes service account](workload-identity-deploy-cluster#create-a-kubernetes-service-account)[Federated identity credential](workload-identity-deploy-cluster#create-the-federated-identity-credential)[Dapr cluster extension](dapr-overview)installed on the AKS cluster

[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)installed locally.

## Clone the repository

Clone the

[Dapr quickstarts repository](https://github.com/Azure-Samples/dapr-aks-extension-quickstart)using the`git clone`

command.`git clone https://github.com/Azure-Samples/dapr-aks-extension-quickstart.git`

Change to the

`dapr-aks-extension-quickstart`

directory.

## Create and configure a Redis store

Open the [Azure portal](https://portal.azure.com/#create/Microsoft.Cache) to start the Azure Cache for Redis creation flow.

- Fill out the recommended information according to
[the "Create an open-source Redis cache" quickstart instructions](/en-us/azure/azure-cache-for-redis/quickstart-create-redis). - Select
**Create**to start the Redis instance deployment.

### Verify resource information

- Once the Redis resource is deployed, navigate to its overview page.
- Take note of:
- The hostname, found in the
**Essentials**section of the cache overview page. The hostname format looks similar to:`xxxxxx.redis.cache.windows.net`

. - The SSL port, found in the cache's
**Advanced Settings**blade. The default value is`6380`

.

- The hostname, found in the
- Navigate to the
**Authentication**blade and verify Microsoft Entra Authentication is enabled on your resource.

### Add managed identity

In the

**Authentication**blade, type the name of the[Managed Identity you created as a prerequisite](#prerequisites)in the field under**Enable Microsoft Entra Authentication**checkbox.Verify your managed identity is added as a Redis User assigned Data Owner Access Policy permissions.


### Enable public network access

For this scenario, your Redis cache uses public network access. Be sure to [clean up resources](#clean-up-resources) when you're finished with this quickstart.

- Navigate to the
**Private Endpoint**blade. - Click
**Enable public network access**from the top menu.

## Configure the Dapr components

In `redis.yaml`

, the component is configured to use Entra ID Authentication using workload identity enabled for AKS cluster. No access keys are required.

```
- name: useEntraID
value: "true"
- name: enableTLS
value: true
```


In your preferred code editor, navigate to the

`deploy`

directory in the sample and open`redis.yaml`

.For

`redisHost`

, replace the placeholder`<REDIS_HOST>:<REDIS_PORT>`

value with the Redis cache hostname and SSL port[you saved earlier from Azure portal](#verify-resource-information).`- name: redisHost value: <your-cache-name>.redis.cache.windows.net:6380`


### Apply the configuration

Apply the

`redis.yaml`

file using the`kubectl apply`

command.`kubectl apply -f ./deploy/redis.yaml`

Verify your state store was successfully configured using the

`kubectl get components.redis`

command.`kubectl get components.redis -o yaml`

**Expected output**`component.dapr.io/statestore created`


## Deploy the Node.js app with the Dapr sidecar

### Configure the Node.js app

In `node.yaml`

, the pod spec has the label added to use workload identity:

```
labels:
app: node
azure.workload.identity/use: "true"
```


Navigate to the

`deploy`

directory and open`node.yaml`

.Replace the placeholder

`<SERVICE_ACCOUNT_NAME>`

value for`serviceAccountName`

with[the service account name you created](workload-identity-deploy-cluster#create-a-kubernetes-service-account).- This value should be the same service account you used to create the federated identity credential.


### Apply the configuration

Apply the Node.js app deployment to your cluster using the

`kubectl apply`

command.`kubectl apply -f ./deploy/node.yaml`

Kubernetes deployments are asynchronous, so before moving on to the next steps, verify the deployment is complete with the following command:

`kubectl rollout status deploy/nodeapp`

Access your service using the

`kubectl get svc`

command.`kubectl get svc nodeapp`

Make note of the

`EXTERNAL-IP`

in the output.

### Verify the Node.js service

Using

`curl`

, call the service with your`EXTERNAL-IP`

.`curl $EXTERNAL_IP/ports`

**Example output**`{"DAPR_HTTP_PORT":"3500","DAPR_GRPC_PORT":"50001"}`

Submit an order to the application.

`curl --request POST --data "@sample.json" --header Content-Type:application/json $EXTERNAL_IP/neworder`

Confirm the order.

`curl $EXTERNAL_IP/order`

**Expected output**`{ "orderId": "42" }`


## Deploy the Python app with the Dapr sidecar

### Configure the Python app

In `python.yaml`

, the pod spec has the label added to use workload identity:

```
labels:
app: node
azure.workload.identity/use: "true"
```


Navigate to the

`deploy`

directory and open`python.yaml`

.Replace the placeholder

`<SERVICE_ACCOUNT_NAME>`

value for`serviceAccountName`

with[the service account name you created](workload-identity-deploy-cluster#create-a-kubernetes-service-account).- This value should be the same service account you used to create the federated identity credential.


### Apply the configuration

Deploy the Python app to your Kubernetes cluster using the

`kubectl apply`

command.`kubectl apply -f ./deploy/python.yaml`

Kubernetes deployments are asynchronous, so before moving on to the next steps, verify the deployment is complete with the following command:

`kubectl rollout status deploy/pythonapp`


## Observe messages and confirm persistence

Now that both the Node.js and Python applications are deployed, you can watch messages come through.

Get the logs of the Node.js app using the

`kubectl logs`

command.`kubectl logs --selector=app=node -c node --tail=-1`

**Expected output**`Got a new order! Order ID: 1 Successfully persisted state Got a new order! Order ID: 2 Successfully persisted state Got a new order! Order ID: 3 Successfully persisted state`

Using

`curl`

, call the Node.js app's order endpoint to get the latest order.`curl $EXTERNAL_IP/order`

You should see the latest JSON output in the response.


## Clean up resources

If you no longer plan to use the resources from this quickstart, you can delete all associated resources by removing the resource group.

Remove the resource group, cluster, namespace, and all related resources using the [az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name MyResourceGroup
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-secure-gateway -->

# Secure ingress gateway for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Deploy external or internal Istio Ingress](istio-deploy-ingress) article describes how to configure an ingress gateway to expose an HTTP service to external/internal traffic. This article shows how to expose a secure HTTPS service using either simple or mutual TLS.

## Prerequisites

Enable the Istio add-on on the cluster as per

[documentation](istio-deploy-addon)Deploy an external Istio ingress gateway as per

[documentation](istio-deploy-ingress)

Note

This article refers to the external ingress gateway for demonstration, same steps would apply for configuring mutual TLS for internal ingress gateway.

## Required client/server certificates and keys

This article requires several certificates and keys. You can use your favorite tool to create them or you can use the following [openssl](https://man.openbsd.org/openssl.1) commands.

Create a root certificate and private key for signing the certificates for sample services:

`mkdir bookinfo_certs openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -subj '/O=bookinfo Inc./CN=bookinfo.com' -keyout bookinfo_certs/bookinfo.com.key -out bookinfo_certs/bookinfo.com.crt`

Generate a certificate and private key for

`productpage.bookinfo.com`

:`openssl req -out bookinfo_certs/productpage.bookinfo.com.csr -newkey rsa:2048 -nodes -keyout bookinfo_certs/productpage.bookinfo.com.key -subj "/CN=productpage.bookinfo.com/O=product organization" openssl x509 -req -sha256 -days 365 -CA bookinfo_certs/bookinfo.com.crt -CAkey bookinfo_certs/bookinfo.com.key -set_serial 0 -in bookinfo_certs/productpage.bookinfo.com.csr -out bookinfo_certs/productpage.bookinfo.com.crt`

Generate a client certificate and private key:

`openssl req -out bookinfo_certs/client.bookinfo.com.csr -newkey rsa:2048 -nodes -keyout bookinfo_certs/client.bookinfo.com.key -subj "/CN=client.bookinfo.com/O=client organization" openssl x509 -req -sha256 -days 365 -CA bookinfo_certs/bookinfo.com.crt -CAkey bookinfo_certs/bookinfo.com.key -set_serial 1 -in bookinfo_certs/client.bookinfo.com.csr -out bookinfo_certs/client.bookinfo.com.crt`


## Configure a TLS ingress gateway

Create a Kubernetes TLS secret for the ingress gateway; use [Azure Key Vault](/en-us/azure/key-vault/general/basic-concepts) to host certificates/keys and [Azure Key Vault Secrets Provider add-on](csi-secrets-store-driver) to sync secrets to the cluster.

### Set up Azure Key Vault and sync secrets to the cluster

Create Azure Key Vault

You need an

[Azure Key Vault resource](/en-us/azure/key-vault/general/quick-create-cli)to supply the certificate and key inputs to the Istio add-on.`export AKV_NAME=<azure-key-vault-resource-name> az keyvault create --name $AKV_NAME --resource-group $RESOURCE_GROUP --location $LOCATION`

Enable

[Azure Key Vault provider for Secret Store CSI Driver](csi-secrets-store-driver)add-on on your cluster.`az aks enable-addons --addons azure-keyvault-secrets-provider --resource-group $RESOURCE_GROUP --name $CLUSTER`

If your Key Vault is using Azure RBAC for the permissions model, follow the instructions

[here](/en-us/azure/key-vault/general/rbac-guide#using-azure-rbac-secret-key-and-certificate-permissions-with-key-vault)to assign an Azure role of Key Vault Secrets User for the add-on's user-assigned managed identity. Alternatively, if your key vault is using the vault access policy permissions model, authorize the user-assigned managed identity of the add-on to access Azure Key Vault resource using access policy:`OBJECT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.objectId' -o tsv | tr -d '\r') CLIENT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.clientId') TENANT_ID=$(az keyvault show --resource-group $RESOURCE_GROUP --name $AKV_NAME --query 'properties.tenantId') az keyvault set-policy --name $AKV_NAME --object-id $OBJECT_ID --secret-permissions get list`

Create secrets in Azure Key Vault using the certificates and keys.

`az keyvault secret set --vault-name $AKV_NAME --name test-productpage-bookinfo-key --file bookinfo_certs/productpage.bookinfo.com.key az keyvault secret set --vault-name $AKV_NAME --name test-productpage-bookinfo-crt --file bookinfo_certs/productpage.bookinfo.com.crt az keyvault secret set --vault-name $AKV_NAME --name test-bookinfo-crt --file bookinfo_certs/bookinfo.com.crt`

Use the following manifest to deploy SecretProviderClass to provide Azure Key Vault specific parameters to the CSI driver.

`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: productpage-credential-spc namespace: aks-istio-ingress spec: provider: azure secretObjects: - secretName: productpage-credential type: kubernetes.io/tls data: - objectName: test-productpage-bookinfo-key key: tls.key - objectName: test-productpage-bookinfo-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $AKV_NAME cloudName: "" objects: | array: - | objectName: test-productpage-bookinfo-key objectType: secret objectAlias: "test-productpage-bookinfo-key" - | objectName: test-productpage-bookinfo-crt objectType: secret objectAlias: "test-productpage-bookinfo-crt" tenantId: $TENANT_ID EOF`

Alternatively, to reference a certificate object type directly from Azure Key Vault, use the following manifest to deploy SecretProviderClass. In this example,

`test-productpage-bookinfo-cert-pxf`

is the name of the certificate object in Azure Key Vault. Refer to[obtain certificates and keys](csi-secrets-store-identity-access?pivots=access-with-a-user-assigned-managed-identity#obtain-certificates-and-keys)section for more information.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: productpage-credential-spc namespace: aks-istio-ingress spec: provider: azure secretObjects: - secretName: productpage-credential type: kubernetes.io/tls data: - objectName: test-productpage-bookinfo-key key: tls.key - objectName: test-productpage-bookinfo-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $AKV_NAME cloudName: "" objects: | array: - | objectName: test-productpage-bookinfo-cert-pfx #certificate object name from keyvault objectType: secret objectAlias: "test-productpage-bookinfo-key" - | objectName: test-productpage-bookinfo-cert-pfx #certificate object name from keyvault objectType: cert objectAlias: "test-productpage-bookinfo-crt" tenantId: $TENANT_ID EOF`

Use the following manifest to deploy a sample pod. The secret store CSI driver requires a pod to reference the SecretProviderClass resource to ensure secrets sync from Azure Key Vault to the cluster.

`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: secrets-store-sync-productpage namespace: aks-istio-ingress spec: containers: - name: busybox image: mcr.microsoft.com/oss/busybox/busybox:1.33.1 command: - "/bin/sleep" - "10" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "productpage-credential-spc" EOF`

Verify

`productpage-credential`

secret created on the cluster namespace`aks-istio-ingress`

as defined in the SecretProviderClass resource.`kubectl describe secret/productpage-credential -n aks-istio-ingress`

Example output:

`Name: productpage-credential Namespace: aks-istio-ingress Labels: secrets-store.csi.k8s.io/managed=true Annotations: <none> Type: tls Data ==== cert: 1066 bytes key: 1704 bytes`


### Configure ingress gateway and virtual service

Route HTTPS traffic via the Istio ingress gateway to the sample applications. Use the following manifest to deploy gateway and virtual service resources.

```
cat <<EOF | kubectl apply -f -
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-gateway
spec:
selector:
istio: aks-istio-ingressgateway-external
servers:
- port:
number: 443
name: https
protocol: HTTPS
tls:
mode: SIMPLE
credentialName: productpage-credential
hosts:
- productpage.bookinfo.com
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: productpage-vs
spec:
hosts:
- productpage.bookinfo.com
gateways:
- bookinfo-gateway
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
port:
number: 9080
host: productpage
EOF
```


Note

In the gateway definition, `credentialName`

must match the `secretName`

in SecretProviderClass resource and `selector`

must refer to the external ingress gateway by its label, in which the key of the label is `istio`

and the value is `aks-istio-ingressgateway-external`

. For internal ingress gateway label is `istio`

and the value is `aks-istio-ingressgateway-internal`

.

Set environment variables for external ingress host and ports:

```
export INGRESS_HOST_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export SECURE_INGRESS_PORT_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.spec.ports[?(@.name=="https")].port}')
export SECURE_GATEWAY_URL_EXTERNAL=$INGRESS_HOST_EXTERNAL:$SECURE_INGRESS_PORT_EXTERNAL
echo "https://$SECURE_GATEWAY_URL_EXTERNAL/productpage"
```


### Verification

Send an HTTPS request to access the productpage service through HTTPS:

```
curl -s -HHost:productpage.bookinfo.com --resolve "productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL:$INGRESS_HOST_EXTERNAL" --cacert bookinfo_certs/bookinfo.com.crt "https://productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


Note

To configure HTTPS ingress access to an HTTPS service, i.e., configure an ingress gateway to perform SNI passthrough instead of TLS termination on incoming requests, update the tls mode in the gateway definition to `PASSTHROUGH`

. This instructs the gateway to pass the ingress traffic “as is”, without terminating TLS.

## Configure a mutual TLS ingress gateway

Extend your gateway definition to support mutual TLS.

Update the ingress gateway credential by deleting the current secret and creating a new one. The server uses the CA certificate to verify its clients, and we must use the key ca.crt to hold the CA certificate.

`kubectl delete secretproviderclass productpage-credential-spc -n aks-istio-ingress kubectl delete secret/productpage-credential -n aks-istio-ingress kubectl delete pod/secrets-store-sync-productpage -n aks-istio-ingress`

Use the following manifest to recreate SecretProviderClass with CA certificate.

`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: productpage-credential-spc namespace: aks-istio-ingress spec: provider: azure secretObjects: - secretName: productpage-credential type: opaque data: - objectName: test-productpage-bookinfo-key key: tls.key - objectName: test-productpage-bookinfo-crt key: tls.crt - objectName: test-bookinfo-crt key: ca.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $AKV_NAME cloudName: "" objects: | array: - | objectName: test-productpage-bookinfo-key objectType: secret objectAlias: "test-productpage-bookinfo-key" - | objectName: test-productpage-bookinfo-crt objectType: secret objectAlias: "test-productpage-bookinfo-crt" - | objectName: test-bookinfo-crt objectType: secret objectAlias: "test-bookinfo-crt" tenantId: $TENANT_ID EOF`

Use the following manifest to redeploy sample pod to sync secrets from Azure Key Vault to the cluster.

`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: secrets-store-sync-productpage namespace: aks-istio-ingress spec: containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "productpage-credential-spc" EOF`

Verify

`productpage-credential`

secret created on the cluster namespace`aks-istio-ingress`

.`kubectl describe secret/productpage-credential -n aks-istio-ingress`

Example output:

`Name: productpage-credential Namespace: aks-istio-ingress Labels: secrets-store.csi.k8s.io/managed=true Annotations: <none> Type: opaque Data ==== ca.crt: 1188 bytes tls.crt: 1066 bytes tls.key: 1704 bytes`


Use the following manifest to update the gateway definition to set the TLS mode to MUTUAL.

`cat <<EOF | kubectl apply -f - apiVersion: networking.istio.io/v1beta1 kind: Gateway metadata: name: bookinfo-gateway spec: selector: istio: aks-istio-ingressgateway-external # use istio default ingress gateway servers: - port: number: 443 name: https protocol: HTTPS tls: mode: MUTUAL credentialName: productpage-credential # must be the same as secret hosts: - productpage.bookinfo.com EOF`


### Verification

Attempt to send HTTPS request using the prior approach - without passing the client certificate - and see it fail.

```
curl -v -HHost:productpage.bookinfo.com --resolve "productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL:$INGRESS_HOST_EXTERNAL" --cacert bookinfo_certs/bookinfo.com.crt "https://productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL/productpage"
```


Example output:

```
...
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS alert, unknown (628):
* OpenSSL SSL_read: error:0A00045C:SSL routines::tlsv13 alert certificate required, errno 0
* Failed receiving HTTP2 data
* OpenSSL SSL_write: SSL_ERROR_ZERO_RETURN, errno 0
* Failed sending HTTP2 data
* Connection #0 to host productpage.bookinfo.com left intact
curl: (56) OpenSSL SSL_read: error:0A00045C:SSL routines::tlsv13 alert certificate required, errno 0
```


Pass your client’s certificate with the `--cert`

flag and private key with the `--key`

flag to curl.

```
curl -s -HHost:productpage.bookinfo.com --resolve "productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL:$INGRESS_HOST_EXTERNAL" --cacert bookinfo_certs/bookinfo.com.crt --cert bookinfo_certs/client.bookinfo.com.crt --key bookinfo_certs/client.bookinfo.com.key "https://productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Delete resources

If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/api-server-authorized-ip-ranges -->

# Secure access to the API server using authorized IP address ranges in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use API server authorized IP address ranges to limit which IP addresses and CIDRs can access control plane endpoints for your Azure Kubernetes Service (AKS) workloads.

## Prerequisites

- The Azure CLI version 2.0.76 or later installed and configured. Check your version using the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - To learn what IP addresses to include when integrating your AKS cluster with Azure DevOps, see
[Allowed IP addresses and domain URLs](/en-us/azure/devops/organizations/security/allow-list-ip-url).

Tip

From the Azure portal, you can use Azure Copilot to make changes to the IP addresses that can access your cluster. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#enable-ip-address-authorization).

## Limitations and considerations

- This feature is only supported on the Standard SKU load balancer for clusters created after October 2019. Any existing clusters on the Basic SKU load balancer with the feature enabled should continue to work properly if the Kubernetes version and control plane are upgraded. However, you can't migrate these clusters to the Standard SKU load balancer.
- You can't use this feature with
[private clusters](private-clusters). - When using this feature with clusters that use
[Node public IPs](use-node-public-ips), the node pools using the Node public IPs must use public IP prefixes. You must add the public IP prefixes as authorized ranges. - You can specify up to 200 authorized IP ranges. To go beyond this limit, consider using
[API Server VNet Integration](api-server-vnet-integration), which supports up to 2,000 authorized IP ranges.

## Overview of API server authorized IP ranges

The Kubernetes API server exposes underlying Kubernetes APIs and provides the interaction for management tools like `kubectl`

and the Kubernetes dashboard. AKS provides a single-tenant cluster control plane with a dedicated API server. The API server is assigned a public IP address by default. You can control access using Kubernetes role-based access control (Kubernetes RBAC) or Azure RBAC.

To secure access to the otherwise publicly accessible AKS control plane / API server, you can enable and use authorized IP ranges. These authorized IP ranges only allow defined IP address ranges to communicate with the API server. Any requests made to the API server from an IP address that isn't part of these authorized IP ranges is blocked. The rules can take up to two minutes to propagate. Allow up to that time when testing the connection.

## Recommended IP ranges to allow

We recommend including the following IP address ranges in your API server authorized IP ranges configuration:

- The cluster egress IP address (firewall, NAT gateway, or other address, depending on your
[outbound type](egress-outboundtype)). - Any range that represents networks that you'll administer the cluster from.

## Create an AKS cluster with API server authorized IP ranges enabled

Note

When you enable API server authorized IP ranges during cluster creation, both the API server public IP and the outbound public IP of the [Standard SKU load balancer](load-balancer-standard) are automatically allowed by default, in addition to any ranges you specify.

**Special case - 0.0.0.0/32**: This is a special value that tells AKS to allow only the outbound public IP of the Standard SKU load balancer to access the API server. The

`0.0.0.0/32`

value acts as a placeholder that:- Disables the default behavior of allowing extra client IP ranges.
- Restricts API server access to only the cluster's own outbound IP.
- Is useful for scenarios where you want the cluster to self-manage but block external access.

When creating a cluster with API server authorized IP ranges enabled, you provide a list of authorized public IP address ranges. When you specify a CIDR range, you must use the network address (first IP address in the range). For example, if you want to allow the range `137.117.106.88`

to `137.117.106.95`

, you must specify `137.117.106.88/29`

.

Create an AKS cluster with API server authorized IP ranges enabled using the

command with the`az aks create`

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows the IP address range`73.140.245.0/24`

to access the API server:`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 73.140.245.0/24 --generate-ssh-keys`


Create an AKS cluster with API server authorized IP ranges enabled using the

cmdlet with the`New-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows the IP address range`73.140.245.0/24`

to access the API server:`New-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -NodeVmSetType VirtualMachineScaleSets -LoadBalancerSku Standard -ApiServerAccessAuthorizedIpRange '73.140.245.0/24' -GenerateSshKey`


- From the
[Azure portal home page](https://portal.azure.com/#home), select**Create a resource**>**Containers**>**Azure Kubernetes Service (AKS)**. - Configure the cluster settings as needed.
- In the
**Networking**section under**Public access**, select**Set authorized IP ranges**. - For
**Specify IP ranges**, enter the IP address ranges you want to authorize to access the API server. - Configure the rest of the cluster settings as needed.
- When you're ready, select
**Review + create**>**Create**to create the cluster.

## Specify outbound IPs for a Standard SKU load balancer

When creating a cluster with API server authorized IP ranges enabled, you can also specify the outbound IP addresses or prefixes for the cluster using the `--load-balancer-outbound-ips`

or `--load-balancer-outbound-ip-prefixes`

parameters. All IPs provided in the parameters are allowed along with the IPs in the `--api-server-authorized-ip-ranges`

parameter.

Create an AKS cluster with API server authorized IP ranges enabled and specify the outbound IP addresses for the Standard SKU load balancer using the

`--load-balancer-outbound-ips`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*, allows the IP address range`73.140.245.0/24`

to access the API server, and specifies two outbound IP addresses for the Standard SKU load balancer. Make sure to replace the placeholders`<public-ip-id-1>`

and`<public-ip-id-2>`

with the actual resource IDs of your public IP addresses.`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 73.140.245.0/24 --load-balancer-outbound-ips <public-ip-id-1>,<public-ip-id-2> --generate-ssh-keys`


## Allow only the outbound public IP of the Standard SKU load balancer

Create an AKS cluster with API server authorized IP ranges enabled and allow only the outbound public IP of the Standard SKU load balancer using the

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*with API server authorized IP ranges enabled and allows only the outbound public IP of the Standard SKU load balancer:`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 0.0.0.0/32 --generate-ssh-keys`


Create an AKS cluster with API server authorized IP ranges enabled and allow only the outbound public IP of the Standard SKU load balancer using the

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*with API server authorized IP ranges enabled and allows only the outbound public IP of the Standard SKU load balancer:`New-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -NodeVmSetType VirtualMachineScaleSets -LoadBalancerSku Standard -ApiServerAccessAuthorizedIpRange '0.0.0.0/32' -GenerateSshKey`


- From the
[Azure portal home page](https://portal.azure.com/#home), select**Create a resource**>**Containers**>**Azure Kubernetes Service (AKS)**. - Configure the cluster settings as needed.
- In the
**Networking**section under**Public access**, select**Set authorized IP ranges**. - For
**Specify IP ranges**, enter`0.0.0.0/32`

. This setting allows only the outbound public IP of the Standard SKU load balancer. - Configure the rest of the cluster settings as needed.
- When you're ready, select
**Review + create**>**Create**to create the cluster.

## Update the API server authorized IP ranges on an existing cluster

Update an existing cluster's API server authorized IP ranges using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and updates the IP address range to`73.140.245.0/24`

:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges 73.140.245.0/24`


## Allow multiple IP address ranges

To allow multiple IP address ranges, you can list several IP addresses, separated by commas.

Update an existing cluster's API server authorized IP ranges to allow multiple IP address ranges using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows multiple IP address ranges:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges 73.140.245.0/24,193.168.1.0/24,194.168.1.0/24`


Update an existing cluster's API server authorized IP ranges using the

cmdlet with the`Set-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and updates the IP address range to`73.140.245.0/24`

:`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange '73.140.245.0/24'`


- Navigate to the Azure portal and select the AKS cluster you want to update.
- From the service menu, under
**Settings**, select**Networking**. - Under
**Resource settings**, select**Manage**. - On the
**Authorized IP ranges**page, update the**Authorized IP ranges**as needed. - When you're done, select
**Save**.

## Disable API server authorized IP ranges on an existing cluster

Disable API server authorized IP ranges using the

command and specify an empty range`az aks update`

`""`

for the`--api-server-authorized-ip-ranges`

parameter.`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges ""`


Disable API server authorized IP ranges using the

cmdlet and specify an empty range`Set-AzAksCluster`

`''`

for the`-ApiServerAccessAuthorizedIpRange`

parameter.`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange ''`


- Navigate to the Azure portal and select the AKS cluster you want to update.
- From the service menu, under
**Settings**, select**Networking**. - Under
**Resource settings**, select**Manage**. - On the
**Authorized IP ranges**page, deselect the**Set authorized IP ranges**checkbox. - Select
**Save**.

## Find existing API server authorized IP ranges

Find existing API server authorized IP ranges using the

command with the`az aks show`

`--query`

parameter set to`apiServerAccessProfile.authorizedIpRanges`

.`az aks show --resource-group myResourceGroup --name myAKSCluster --query apiServerAccessProfile.authorizedIpRanges`

Example output:

`[ "73.140.245.0/24" ]`


Find existing API server authorized IP ranges using the

cmdlet.`Get-AzAksCluster`

`Get-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster | Select-Object -ExpandProperty ApiServerAccessProfile`

Example output:

`AuthorizedIPRanges: {73.140.245.0/24} ...`


Navigate to the Azure portal and select your AKS cluster.

From the service menu, under

**Settings**, select**Networking**. The existing API server authorized IP ranges are listed under**Resource settings**.

## Access the API server from your development machine, tooling, or automation

You must add your development machines, tooling, or automation IP addresses to the AKS cluster list of approved IP ranges to access the API server from there.

Another option is to configure a jumpbox with the necessary tooling inside a separate subnet in the firewall's virtual network. This option assumes your environment has a firewall with the respective network and that you added the firewall IPs to authorized ranges. Similarly, if you forced tunneling from the AKS subnet to the firewall subnet, having the jumpbox in the cluster subnet also works.

Note

The following example adds another IP address to the approved ranges. It still includes the existing IP address. If you don't include your existing IP address, this command replaces it with the new one instead of adding it to the authorized ranges.

Retrieve your IP address and set it to an environment variable using the following command:

`# Retrieve your IP address CURRENT_IP=$(dig +short "myip.opendns.com" "@resolver1.opendns.com")`

Add your IP address to the approved list using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example adds your current IP address to the existing API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges $CURRENT_IP/24,73.140.245.0/24`


Retrieve your IP address and set it to an environment variable using the following command:

`# Retrieve your IP address CURRENT_IP=$(dig +short "myip.opendns.com" "@resolver1.opendns.com")`

Add your IP address to the approved list using the

cmdlet with the`Set-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example adds your current IP address to the existing API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*:`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange '$CURRENT_IP/24,73.140.245.0/24'`


Another option is to use the following command on Windows systems to get the public IPv4 address:

```
Invoke-RestMethod http://ipinfo.io/json | Select -exp ip
```


You can also follow the steps in [Find your IP address](https://support.microsoft.com/help/4026518/windows-10-find-your-ip-address) or search on *what is my IP address?* in an internet browser.

## Related content

To learn more about security in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-deploy-add-on-arm -->

# Install the Kubernetes Event-driven Autoscaling (KEDA) add-on using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

This article shows you how to deploy the Kubernetes Event-driven Autoscaling (KEDA) add-on to Azure Kubernetes Service (AKS) using an [ARM template](/en-us/azure/azure-resource-manager/templates/).

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.31.

For more information on how to securely scale your applications with workload identity, please read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, please read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - This article assumes you have an existing Azure resource group. If you don't have an existing resource group, you can create one using the
command.`az group create`

- Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules). [Create an SSH key pair](#create-an-ssh-key-pair).

Note

If you're using [Microsoft Entra Workload ID](/en-us/azure/aks/workload-identity-overview) and you enable KEDA before Workload ID, you need to restart the KEDA operator pods so the proper environment variables can be injected:

Restart the pods by running

`kubectl rollout restart deployment keda-operator -n kube-system`

.Obtain KEDA operator pods using

`kubectl get pod -n kube-system`

and finding pods that begin with`keda-operator`

.Verify successful injection of the environment variables by running

`kubectl describe pod <keda-operator-pod> -n kube-system`

. Under`Environment`

, you should see values for`AZURE_TENANT_ID`

,`AZURE_FEDERATED_TOKEN_FILE`

, and`AZURE_AUTHORITY_HOST`

.

## Create an SSH key pair

Navigate to the

[Azure Cloud Shell](https://shell.azure.com/).Create an SSH key pair using the

command.`az sshkey create`

`az sshkey create --name <sshkey-name> --resource-group <resource-group-name>`


## Enable the KEDA add-on with an ARM template

Deploy the

[ARM template for an AKS cluster](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.kubernetes%2Faks%2Fazuredeploy.json).Select

**Edit template**.Enable the KEDA add-on by specifying the

`workloadAutoScalerProfile`

field in the ARM template, as shown in the following example:`"workloadAutoScalerProfile": { "keda": { "enabled": true } }`

Select

**Save**.Update the required values for the ARM template:

**Subscription**: Select the Azure subscription to use for the deployment.**Resource group**: Select the resource group to use for the deployment.**Region**: Select the region to use for the deployment.**Dns Prefix**: Enter a unique DNS name to use for the cluster.**Linux Admin Username**: Enter a username for the cluster.**SSH public key source**: Select**Use existing key stored in Azure**.**Store Keys**: Select the key pair you created earlier in the article.

Select

**Review + create**>**Create**.

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local device, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client.

If you use the Azure Cloud Shell, `kubectl`

is already installed. You can also install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

- Configure
`kubectl`

to connect to your Kubernetes cluster, use the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. The following example gets credentials for the AKS cluster named*MyAKSCluster*in the*MyResourceGroup*:

```
az aks get-credentials --resource-group MyResourceGroup --name MyAKSCluster
```


## Example deployment

The following snippet is a sample deployment that creates a cluster with KEDA enabled with a single node pool comprised of three `DS2_v5`

nodes.

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"resources": [
{
"apiVersion": "2023-03-01",
"dependsOn": [],
"type": "Microsoft.ContainerService/managedClusters",
"location": "westcentralus",
"name": "myAKSCluster",
"properties": {
"kubernetesVersion": "1.27",
"enableRBAC": true,
"dnsPrefix": "myAKSCluster",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": 200,
"count": 3,
"enableAutoScaling": false,
"vmSize": "Standard_D2S_v5",
"osType": "Linux",
"type": "VirtualMachineScaleSets",
"mode": "System",
"maxPods": 110,
"availabilityZones": [],
"nodeTaints": [],
"enableNodePublicIP": false
}
],
"networkProfile": {
"loadBalancerSku": "standard",
"networkPlugin": "kubenet"
},
"workloadAutoScalerProfile": {
"keda": {
"enabled": true
}
}
},
"identity": {
"type": "SystemAssigned"
}
}
]
}
```


## Start scaling apps with KEDA

You can autoscale your apps with KEDA using custom resource definitions (CRDs). For more information, see the [KEDA documentation](https://keda.sh/docs/scalers/).

## Remove resources

Remove the resource group and all related resources using the

command.`az group delete`

`az group delete --name <resource-group-name>`


## Next steps

This article showed you how to install the KEDA add-on on an AKS cluster, and then verify that it's installed and running. With the KEDA add-on installed on your cluster, you can [deploy a sample application](https://github.com/kedacore/sample-dotnet-worker-servicebus-queue) to start scaling apps.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more, view the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing -->

# Managed NGINX ingress with the application routing add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

One way to route Hypertext Transfer Protocol (HTTP) and secure (HTTPS) traffic to applications running on an Azure Kubernetes Service (AKS) cluster is to use the [Kubernetes Ingress object](https://kubernetes.io/docs/concepts/services-networking/ingress/). When you create an Ingress object that uses the application routing add-on NGINX Ingress classes, the add-on creates, configures, and manages one or more Ingress controllers in your AKS cluster.

This article shows you how to deploy and configure a basic Ingress controller in your AKS cluster.

## Application routing add-on with NGINX features

The application routing add-on with NGINX delivers the following:

- Easy configuration of managed NGINX Ingress controllers based on
[Kubernetes NGINX Ingress controller](https://kubernetes.github.io/ingress-nginx/). - Integration with
[Azure DNS](/en-us/azure/dns/dns-overview)for public and private zone management - SSL termination with certificates stored in Azure Key Vault.

For other configurations, see:

[DNS and SSL configuration](app-routing-dns-ssl)[Application routing add-on configuration](app-routing-nginx-configuration)[Configure internal NGIX ingress controller for Azure private DNS zone](create-nginx-ingress-private-controller).

With the retirement of [Open Service Mesh](https://release-v1-2.docs.openservicemesh.io/) (OSM) by the Cloud Native Computing Foundation (CNCF), using the application routing add-on with OSM is not recommended.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.54.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

- The application routing add-on supports up to five Azure DNS zones.
- The application routing add-on can only be enabled on AKS clusters with
[managed identity](use-managed-identity). - All global Azure DNS zones integrated with the add-on have to be in the same resource group.
- All private Azure DNS zones integrated with the add-on have to be in the same resource group.
- Editing the ingress-nginx
`ConfigMap`

in the`app-routing-system`

namespace isn't supported. - The following snippet annotations are blocked and will prevent an Ingress from being configured:
`load_module`

,`lua_package`

,`_by_lua`

,`location`

,`root`

,`proxy_pass`

,`serviceaccount`

,`{`

,`}`

,`'`

.

## Enable application routing using Azure CLI

### Enable on a new cluster

To enable application routing on a new cluster, use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command, specifying the

`--enable-app-routing`

flag.```
az aks create \
--resource-group <ResourceGroupName> \
--name <ClusterName> \
--location <Location> \
--enable-app-routing \
--generate-ssh-keys
```


### Enable on an existing cluster

To enable application routing on an existing cluster, use the [ az aks approuting enable](/en-us/cli/azure/aks/approuting#az-aks-approuting-enable) command.

```
az aks approuting enable --resource-group <ResourceGroupName> --name <ClusterName>
```


## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure `kubectl`

to connect to your Kubernetes cluster using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --resource-group <ResourceGroupName> --name <ClusterName>
```


## Deploy an application

The application routing add-on uses annotations on Kubernetes Ingress objects to create the appropriate resources.

Create the application namespace called

`aks-store`

to run the example pods using the`kubectl create namespace`

command.`kubectl create namespace aks-store`

Deploy the AKS store application using the following YAML manifest file:

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/sample-manifests/docs/app-routing/aks-store-deployments-and-services.yaml -n aks-store`


This manifest will create the necessary deployments and services for the AKS store application.

### Create the Ingress object

The application routing add-on creates an Ingress class on the cluster named *webapprouting.kubernetes.azure.com*. When you create an Ingress object with this class, it activates the add-on.

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: store-front namespace: aks-store spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - http: paths: - backend: service: name: store-front port: number: 80 path: / pathType: Prefix`

Create the ingress resource using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n aks-store`

The following example output shows the created resource:

`ingress.networking.k8s.io/store-front created`


## Verify the managed Ingress was created

You can verify the managed Ingress was created using the `kubectl get ingress`

command.

```
kubectl get ingress -n aks-store
```


The following example output shows the created managed Ingress:

```
NAME CLASS HOSTS ADDRESS PORTS AGE
store-front webapprouting.kubernetes.azure.com * 51.8.10.109 80 110s
```


You can verify that the AKS store works pointing your browser to the public IP address of the Ingress controller. Find the IP address with kubectl:

```
kubectl get service -n app-routing-system nginx -o jsonpath="{.status.loadBalancer.ingress[0].ip}"
```


## Remove the application routing add-on

To remove the associated namespace, use the `kubectl delete namespace`

command.

```
kubectl delete namespace aks-store
```


To remove the application routing add-on from your cluster, use the [ az aks approuting disable](/en-us/cli/azure/aks/approuting#az-aks-approuting-disable) command.

```
az aks approuting disable --name <ClusterName> --resource-group <ResourceGroupName>
```


Note

To avoid potential disruption of traffic into the cluster when the application routing add-on is disabled, some Kubernetes resources, including *configMaps*, *secrets*, and the *deployment* that runs the controller, will remain on the cluster. These resources are in the *app-routing-system* namespace. You can remove these resources if they're no longer needed by deleting the namespace with `kubectl delete ns app-routing-system`

.

## Next steps

[Configure custom ingress configurations](app-routing-nginx-configuration)shows how to create an advanced Ingress configuration and[configure a custom domain using Azure DNS to manage DNS zones and setup a secure ingress](app-routing-dns-ssl).To integrate with an Azure internal load balancer and configure a private Azure DNS zone to enable DNS resolution for the private endpoints to resolve specific domains, see

[Configure internal NGINX ingress controller for Azure private DNS zone](create-nginx-ingress-private-controller).Learn about monitoring the ingress-nginx controller metrics included with the application routing add-on with

[with Prometheus in Grafana](app-routing-nginx-prometheus)(preview) as part of analyzing the performance and usage of your application.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/custom-node-configuration -->

# Customize the node configuration for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Customizing your node configuration allows you to adjust operating system (OS) settings or kubelet parameters to match the needs of your workloads. When you create an AKS cluster or add a node pool to your cluster, you can customize a subset of commonly used OS and kubelet settings. To configure settings beyond this subset, you can [use a daemon set to customize your needed configurations without losing AKS support for your nodes](support-policies#shared-responsibility).

## Create custom node configuration files for AKS node pools

OS and kubelet configuration changes require you to create a new configuration file with the parameters and your desired settings. If a value for a parameter isn't specified, then the value is set to the default.

Note

The following examples show common configuration settings. You can modify the settings to meet your workload requirements. For a full list of supported custom configuration parameters, see the [Supported custom configuration parameters](#supported-custom-configuration-parameters) section.

### Kubelet configuration

Create a `linuxkubeletconfig.json`

file with the following contents:

```
{
"cpuManagerPolicy": "static",
"cpuCfsQuota": true,
"cpuCfsQuotaPeriod": "200ms",
"imageGcHighThreshold": 90,
"imageGcLowThreshold": 70,
"topologyManagerPolicy": "best-effort",
"allowedUnsafeSysctls": [
"kernel.msg*",
"net.*"
],
"failSwapOn": false
}
```


### OS configuration

Create a `linuxosconfig.json`

file with the following contents:

```
{
"transparentHugePageEnabled": "madvise",
"transparentHugePageDefrag": "defer+madvise",
"swapFileSizeMB": 1500,
"sysctls": {
"netCoreSomaxconn": 163849,
"netIpv4TcpTwReuse": true,
"netIpv4IpLocalPortRange": "32000 60000"
}
}
```


## Create an AKS cluster using custom configuration files

Note

Keep the following information in mind when using custom configuration files when creating a new AKS cluster:

- If you specify a configuration when creating a cluster, the configuration applies only to the nodes in the initial node pool. Any settings not configured in the JSON file retain their default values.
`CustomLinuxOsConfig`

isn't supported for the Windows OS type.

Create a new cluster using custom configuration files using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and specifying your configuration files for the

`--kubelet-config`

and `--linux-os-config`

parameters. The following example command creates a new cluster with the custom `./linuxkubeletconfig.json`

and `./linuxosconfig.json`

files:```
az aks create --name <cluster-name> --resource-group <resource-group-name> --kubelet-config ./linuxkubeletconfig.json --linux-os-config ./linuxosconfig.json
```


## Add a node pool using custom configuration files

Note

Keep the following information in mind when using custom configuration files when adding a new node pool to an existing AKS cluster:

- When you add a Linux node pool to an existing cluster, you can specify the kubelet configuration, OS configuration, or both. When you add a Windows node pool to an existing cluster, you can only specify the kubelet configuration. If you specify a configuration when adding a node pool, the configuration applies only to the nodes in the new node pool. Any settings not configured in the JSON file retain their default values.
`CustomKubeletConfig`

is supported for Linux and Windows node pools.

Create a new Linux node pool using the [ az aks nodepool add](/en-us/cli/azure/aks#az-aks-create) command and specifying your configuration files for the

`--kubelet-config`

and `--linux-os-config`

parameters. The following example command creates a new Linux node pool with the custom `./linuxkubeletconfig.json`

file:```
az aks nodepool add --name <node-pool-name> --cluster-name <cluster-name> --resource-group <resource-group-name> --kubelet-config ./linuxkubeletconfig.json
```


## Confirm settings were applied

After you apply custom node configuration, you can confirm the settings were applied to the nodes by [connecting to the host](node-access) and verifying `sysctl`

or configuration changes were made on the filesystem.

## Supported custom configuration parameters

### Linux kubelet custom configuration

| Parameter | Allowed values/interval | Default | Description |
|---|---|---|---|
`cpuManagerPolicy` |
none, static | none | The static policy allows containers in
|

`cpuCfsQuota`

`cpuCfsQuotaPeriod`

`100ms`

`imageGcHighThreshold`

`imageGcLowThreshold`

`imageGcHighThreshold`

*can*trigger garbage collection.`topologyManagerPolicy`

[Control Topology Management Policies on a node](https://kubernetes.io/docs/tasks/administer-cluster/topology-manager/).`allowedUnsafeSysctls`

`kernel.shm*`

, `kernel.msg*`

, `kernel.sem`

, `fs.mqueue.*`

, `net.*`

`containerLogMaxSizeMB`

`containerLogMaxFiles`

`podMaxPids`

`seccompDefault`

`Unconfined`

, `RuntimeDefault`

`Unconfined`

`RuntimeDefault`

uses containerd's default seccomp profile, restricting certain system calls to enhance security. Restricted syscalls fail. `Unconfined`

places no restrictions on syscalls, allowing all system calls and reducing security. For more information, see the [containerd default seccomp profile](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51). This parameter is in preview.[Register](/en-us/azure/azure-resource-manager/management/preview-features?tabs=azure-cli#register-preview-feature)the "KubeletDefaultSeccompProfilePreview" feature flag using the[command with](/en-us/cli/azure/feature#az-feature-register)`az feature register`

`--namespace "Microsoft.ContainerService"`

.### Windows kubelet custom configuration

| Parameter | Allowed values/interval | Default | Description |
|---|---|---|---|
`imageGcHighThreshold` |
0-100 | 85 | The percent of disk usage after which image garbage collection is always run. Minimum disk usage that triggers garbage collection. To disable image garbage collection, set to 100. |
`imageGcLowThreshold` |
0-100, no higher than `imageGcHighThreshold` |
80 | The percent of disk usage before which image garbage collection is never run. Minimum disk usage that can trigger garbage collection. |
`containerLogMaxSizeMB` |
Size in megabytes (MB) | 10 | The maximum size (for example, 10 MB) of a container log file before it gets rotated. |
`containerLogMaxFiles` |
≥ 2 | 5 | The maximum number of container log files that can be present for a container. |

## Linux custom OS configuration settings

Important

To simplify search and readability, the OS settings are displayed in this article by their name, but they should be added to the configuration JSON file or AKS API using the [camelCase capitalization convention](/en-us/dotnet/standard/design-guidelines/capitalization-conventions).

For example, if you modify the `vm.max_map_count setting`

, you should reformat to `vmMaxMapCount`

in the configuration JSON file.

### Linux file handle limits

When serving high amounts of traffic, that traffic commonly comes from a large number of local files. You can adjust the following kernel settings and built-in limits to allow you to handle more, at the cost of some system memory.

The following table lists the file handle limits that you can customize per node pool:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`fs.file-max` |
8192 - 9223372036854775807 | 9223372036854775807 | 9223372036854775807 | 9223372036854775807 | Maximum number of file-handles that the Linux kernel allocates. This value is set to the maximum possible value (2^63-1) to prevent file descriptor exhaustion and ensure unlimited system-wide file handles for containerized workloads. |
`fs.inotify.max_user_watches` |
781250 - 2097152 | 1048576 | 1048576 | 1048576 | Maximum number of file watches allowed by the system. Each watch is roughly 90 bytes on a 32-bit kernel, and roughly 160 bytes on a 64-bit kernel. |
`fs.aio-max-nr` |
65536 - 6553500 | 65536 | 65536 | 65536 | The aio-nr shows the current system-wide number of asynchronous io requests. aio-max-nr allows you to change the maximum value aio-nr can grow to. |
`fs.nr_open` |
8192 - 20000500 | 1048576 | 1048576 | 1073741816 | The maximum number of file-handles a process can allocate. |

Note

The `fs.file-max`

parameter is set to 9223372036854775807 (the maximum value for a signed 64-bit integer) across Ubuntu and Azure Linux based on upstream defaults. This configuration:

**Prevents denial-of-service attacks**based on system-wide file descriptor exhaustion.**Ensures container workloads**are never bottlenecked by system-wide file handle limits.**Maintains security**through per-process limits (`fs.nr_open`

and`ulimit`

) which still apply to individual processes.**Optimizes for container platforms**where many containers might run simultaneously, each potentially opening many files and network connection.

### Linux socket and network tuning

For agent nodes, which are expected to handle large numbers of concurrent sessions, you can use following TCP and network options and adjust them per node pool:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`net.core.somaxconn` |
4096 - 3240000 | 16384 | 16384 | 16384 | Maximum number of connection requests that can be queued for any given listening socket. An upper limit for the value of the backlog parameter passed to the
`somaxconn` , then it's silently truncated to this limit. |

`net.core.netdev_max_backlog`

`net.core.rmem_max`

`net.core.wmem_max`

`net.core.optmem_max`

`net.ipv4.tcp_max_syn_backlog`

`net.ipv4.tcp_max_tw_buckets`

`timewait`

sockets held by system simultaneously. If this number is exceeded, time-wait socket is immediately destroyed and warning is printed.`net.ipv4.tcp_fin_timeout`

`net.ipv4.tcp_keepalive_time`

`keepalive`

messages when `keepalive`

is enabled.`net.ipv4.tcp_keepalive_probes`

`keepalive`

probes TCP sends out, until it decides that the connection is broken.`net.ipv4.tcp_keepalive_intvl`

`tcp_keepalive_probes`

it makes up the time to kill a connection that isn't responding, after probes started.`net.ipv4.tcp_tw_reuse`

`TIME-WAIT`

sockets for new connections when it's safe from protocol viewpoint.`net.ipv4.ip_local_port_range`

`net.ipv4.neigh.default.gc_thresh1`

`net.ipv4.neigh.default.gc_thresh2`

`net.ipv4.neigh.default.gc_thresh3`

`net.netfilter.nf_conntrack_max`

`nf_conntrack`

is a module that tracks connection entries for NAT within Linux. The `nf_conntrack`

module uses a hash table to record the *established connection*record of the TCP protocol.`nf_conntrack_max`

is the maximum number of nodes in the hash table, that is, the maximum number of connections supported by the `nf_conntrack`

module or the size of connection tracking table. **Default value**is dynamically calculated based on system memory using the formula:`RAM_in_bytes / 16384`

(or `RAM_in_MB * 64`

). For example, a VM with 8 GB RAM has a default of approximately 524,288 connections. Actual values vary based on the VM size and available memory.`net.netfilter.nf_conntrack_buckets`

`nf_conntrack`

is a module that tracks connection entries for NAT within Linux. The `nf_conntrack`

module uses a hash table to record the *established connection*record of the TCP protocol.`nf_conntrack_buckets`

is the size of hash table. **Default value**is dynamically calculated based on system memory using the formula:`RAM_in_bytes / 16384`

, with a minimum of 1,024 buckets and a maximum of 262,144 buckets. The default `nf_conntrack_max`

is typically set to `nf_conntrack_buckets * 4`

. Actual values vary based on the VM size and available memory.### Linux worker limits

Like file descriptor limits, the number of workers or threads that a process can create are limited by both a kernel setting and user limits. The user limit on AKS is unlimited. The following table lists the kernel setting that you can customize per node pool:

| Setting | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|
`kernel.threads-max` |
Dynamically calculated | Dynamically calculated | Dynamically calculated | Processes can spin up worker threads. The maximum number of all threads that can be created is set with the kernel setting `kernel.threads-max` . Default value is dynamically calculated based on system memory using the formula: `total_ram_pages / 4` (where each page is typically 4 KB). Actual values vary based on the VM size and available memory. |

### Linux virtual memory

The following table lists the kernel settings that you can customize per node pool to tune the operation of the virtual memory (VM) subsystem of the Linux kernel and the `writeout`

of dirty data to disk:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`vm.max_map_count` |
65530 | 1048576 | 1048576 | This file contains the maximum number of memory map areas a process can have. Memory map areas are used as a side-effect of calling `malloc` , directly by `mmap` , `mprotect` , and `madvise` , and also when loading shared libraries. |
|
`vm.vfs_cache_pressure` |
1 - 100 | 100 | 100 | 100 | This percentage value controls the tendency of the kernel to reclaim the memory, which is used for caching of directory and inode objects. |
`vm.swappiness` |
0 - 100 | 60 | 60 | 60 | This control is used to define how aggressively the kernel swaps memory pages. Higher values increase aggressiveness, lower values decrease the amount of swap. A value of 0 instructs the kernel not to initiate swap until the amount of free and file-backed pages is less than the high water mark in a zone. |
`swapFileSizeMB` |
1 MB - Size of the
|

`transparentHugePageEnabled`

`always`

, `madvise`

, `never`

`always`

`always`

`madvise`

[Transparent Hugepages](https://www.kernel.org/doc/html/latest/admin-guide/mm/transhuge.html#admin-guide-transhuge)is a Linux kernel feature intended to improve performance by making more efficient use of your processor's memory-mapping hardware. When enabled the kernel attempts to allocate`hugepages`

whenever possible and any Linux process receives 2-MB pages if the `mmap`

region is 2 MB naturally aligned. In certain cases when `hugepages`

are enabled system wide, applications might end up allocating more memory resources. An application might `mmap`

a large region but only touch 1 byte of it, in that case a 2-MB page might be allocated instead of a 4k page for no good reason. This scenario is why it's possible to disable `hugepages`

system-wide or to only have them inside `MADV_HUGEPAGE madvise`

regions.`transparentHugePageDefrag`

`always`

, `defer`

, `defer+madvise`

, `madvise`

, `never`

`madvise`

`madvise`

`madvise`

`hugepages`

available.## Related content

- Learn
[how to configure your AKS cluster](concepts-clusters-workloads). - Learn how
[upgrade the node images](node-image-upgrade)in your cluster. - See
[Upgrade an Azure Kubernetes Service (AKS) cluster](upgrade-cluster)to learn how to upgrade your cluster to the latest version of Kubernetes. - See the list of
[Frequently asked questions about AKS](faq)to find answers to some common AKS questions.
