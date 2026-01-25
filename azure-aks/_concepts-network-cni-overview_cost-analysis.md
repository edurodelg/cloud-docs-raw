---
merged_at: 2026-01-25T12:06:27.777454
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: concepts-network-cni-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-network-cni-overview -->

# Azure Kubernetes Service (AKS) CNI networking overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes uses Container Networking Interface (CNI) plugins to manage networking in Kubernetes clusters. CNI plug-ins are responsible for assigning IP addresses to pods, network routing between pods, Kubernetes service routing, and more.

Azure Kubernetes Service (AKS) provides multiple CNI plugins that you can use in your clusters, depending on your networking requirements.

## Networking models in AKS

Choosing a CNI plugin for your AKS cluster largely depends on which networking model fits your needs best. Each model has its own advantages and disadvantages that you should consider when planning your AKS cluster.

AKS uses two main networking models:

**Overlay network**:- Conserves IP address space for virtual networks by using logically separate Classless Inter-Domain Routing (CIDR) ranges for pods.
- Provides maximum cluster scale support.
- Provides simple management of IP addresses.

**Flat network**:- Provides full virtual network connectivity for pods. Pods can be directly reached via their private IP address from connected networks.
- Requires large, non-fragmented IP address space for virtual networks.


Both networking models have multiple supported options for CNI plugins. The main differences between the models are how pod IP addresses are assigned and how traffic leaves the cluster.

### Overlay networks

Overlay networking is the most common networking model used in Kubernetes. In overlay networks, pods receive an IP address from a private, logically separate CIDR from the Azure virtual network subnet where AKS nodes are deployed. This configuration allows for simpler and often better scalability than the flat network model.

In overlay networks, pods can communicate with each other directly. Traffic that leaves the cluster is Source Network Address Translated (SNAT'd) to the node's IP address. Inbound pod IP traffic is routed through a service, such as a load balancer. The pod IP address is then "hidden" behind the node's IP address. This approach reduces the number of IP addresses required for virtual networks in your clusters.


For overlay networking, AKS provides the [Azure CNI Overlay](concepts-network-azure-cni-overlay) plugin. We recommend this CNI plugin for most scenarios.

### Flat networks

Unlike an overlay network, a flat network model in AKS assigns IP addresses to pods from a subnet from the same Azure virtual network as the AKS nodes. Traffic that leaves your clusters is not SNAT'd, and the pod IP address is directly exposed to the destination. This approach can be useful for some scenarios, such as when you need to expose pod IP addresses to external services.


AKS provides two CNI plugins for flat networking:

[Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet), the recommended CNI plugin for flat networking scenarios.[Azure CNI Node Subnet](concepts-network-legacy-cni#azure-cni-node-subnet), a legacy CNI model for flat networks. In general, we recommend that you use it only if you*need*a managed virtual network for your cluster.

## Choosing a CNI plugin

When you're choosing a CNI plugin, there are several factors to consider. Each networking model has its own advantages and disadvantages. The best choice for your cluster depends on your specific requirements.

### Use case comparison

| CNI plugin | Networking model | Use case highlights |
|---|---|---|
| Azure CNI Overlay | Overlay | - Best for conserving IPs for virtual networks - Maximum node count supported by API server plus 250 pods per node - Simpler configuration - No direct external pod IP access |
| Azure CNI Pod Subnet | Flat | - Direct external pod access - Modes for efficient IP usage for virtual networks or large cluster scale support (preview) |
| Kubenet (legacy) | Overlay | - Prioritization of IP conservation - Limited scale - Manual route management |
| Azure CNI Node Subnet (legacy) | Flat | - Direct external pod access - Simpler configuration - Limited scale - Inefficient use of IPs for virtual networks |

### Feature comparison

| Feature | Azure CNI Overlay | Azure CNI Pod Subnet | Azure CNI Node Subnet (legacy) | Kubenet (legacy) |
|---|---|---|---|---|
| Deployment of a cluster in an existing or new virtual network | Supported | Supported | Supported | Supported with manual user-defined routes (UDRs) |
| Connectivity between pod and virtual machine (VM), with the VM in the same virtual network or a peered virtual network | Pod initiated | Both ways | Both ways | Pod initiated |
| On-premises access via virtual private network (VPN) and Azure ExpressRoute | Pod initiated | Both ways | Both ways | Pod initiated |
| Access to service endpoints | Supported | Supported | Supported | Supported |
| Exposure of services via load balancer | Supported | Supported | Supported | Supported |
| Exposure of services via Azure Application Gateway ingress controller | Supported | Supported | Supported | Supported |
| Exposure of services via Application Gateway for Containers | Supported | Supported | Supported | Not Supported |
| Windows node pools | Supported | Supported | Supported | Not supported |
| Default Azure DNS and private zones | Supported | Supported | Supported | Supported |
| Sharing of virtual network subnets across multiple clusters | Supported | Supported | Supported | Not supported |

### Support scope between network models

Depending on the CNI plugin that you use, you can deploy the virtual network resources for your cluster in one of the following ways:

- The Azure platform can automatically create and configure the virtual network resources when you create an AKS cluster, like in Azure CNI Overlay, Azure CNI Node Subnet, and Kubenet.
- You can manually create and configure the virtual network resources and attach to those resources when you create your AKS cluster.

Although capabilities like service endpoints or UDRs are supported, the [support policies for AKS](support-policies) define what changes you can make. For example:

- If you manually create the virtual network resources for an AKS cluster, you're supported when configuring your own UDRs or service endpoints.
- If the Azure platform automatically creates the virtual network resources for your AKS cluster, you can't manually change those AKS-managed resources to configure your own UDRs or service endpoints.

## Prerequisites

When you're planning your network configuration for AKS, keep these requirements and considerations in mind:

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for address ranges for the Kubernetes service, pods, or cluster virtual networks. - In scenarios where you bring your own virtual network, the cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Authorization/roleAssignments/write`

`Microsoft.Network/virtualNetworks/subnets/read`

(needed only if you're defining your own subnets and CIDRs)

- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node CIDR range. For more information, see
[Azure network security groups overview](/en-us/azure/virtual-network/network-security-groups-overview).


---

<!-- DOCUMENTO FUSIONADO: cost-analysis.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/cost-analysis -->

# Azure Kubernetes Service (AKS) cost analysis

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to enable cost analysis on Azure Kubernetes Service (AKS) to view detailed cost data for cluster resources.

## About cost analysis

AKS clusters rely on Azure resources, such as virtual machines (VMs), virtual disks, load balancers, and public IP addresses. Multiple applications can use these resources. The resource consumption patterns often differ for each application, so their contribution toward the total cluster resource cost might also vary. Some applications might have footprints across multiple clusters, which can pose a challenge when performing cost attribution and cost management.

When you enable cost analysis on your AKS cluster, you can view detailed cost allocation scoped to Kubernetes constructs, such as clusters and namespaces, and Azure Compute, Network, and Storage resources. The add-on is built on top of [OpenCost](https://www.opencost.io/), an open-source Cloud Native Computing Foundation Incubating project for usage data collection. Usage data is reconciled with your Azure invoice data to provide a comprehensive view of your AKS cluster costs directly in the Azure portal Cost Management views.

For more information on Microsoft Cost Management, see [Start analyzing costs in Azure](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis).

After enabling the cost analysis add-on and allowing time for data to be collected, you can use the information in [Understand AKS usage and costs](understand-aks-costs) to help you understand your data.

## Prerequisites

- Your cluster must use the
`Standard`

or`Premium`

tier, not the`Free`

tier. - To view cost analysis information, you must have one of the following roles on the subscription hosting the cluster:
`Owner`

,`Contributor`

,`Reader`

,`Cost Management Contributor`

, or`Cost Management Reader`

. [Managed identity](use-managed-identity)configured on your cluster.- If using the Azure CLI, you need version
`2.61.0`

or later installed. - Once you have enabled cost analysis, you can't downgrade your cluster to the
`Free`

tier without first disabling cost analysis. - Access to the Azure API including Azure Resource Manager (ARM) API. For a list of fully qualified domain names (FQDNs) required, see
[AKS Cost Analysis required FQDN](outbound-rules-control-egress#aks-cost-analysis-add-on).

## Limitations

- Kubernetes cost views are only available for the
*Enterprise Agreement*and*Microsoft Customer Agreement*Microsoft Azure offer types. For more information, see[Supported Microsoft Azure offers](/en-us/azure/cost-management-billing/costs/understand-cost-mgt-data#supported-microsoft-azure-offers). - Currently, virtual nodes aren't supported.

## Enable cost analysis on your AKS cluster

You can enable the cost analysis with the `--enable-cost-analysis`

flag during one of the following operations:

- Creating a
`Standard`

or`Premium`

tier AKS cluster. - Updating an existing
`Standard`

or`Premium`

tier AKS cluster. - Upgrading a
`Free`

cluster to`Standard`

or`Premium`

. - Upgrading a
`Standard`

cluster to`Premium`

. - Downgrading a
`Premium`

cluster to`Standard`

tier.

### Enable cost analysis on a new cluster

Enable cost analysis on a new cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with the

`--enable-cost-analysis`

flag. The following example creates a new AKS cluster in the `Standard`

tier with cost analysis enabled:```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="AKSCostRG$RANDOM_SUFFIX"
export CLUSTER_NAME="AKSCostCluster$RANDOM_SUFFIX"
export LOCATION="WestUS2"
az group create --resource-group $RESOURCE_GROUP --location $LOCATION
az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --location $LOCATION --enable-managed-identity --generate-ssh-keys --tier standard --enable-cost-analysis
```


Results:

```
{
"id": "/subscriptions/xxxxx/resourceGroups/AKSCostRGxxxx",
"location": "WestUS2",
"name": "AKSCostClusterxxxx",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.ContainerService/managedClusters"
}
```


### Enable cost analysis on an existing cluster

Enable cost analysis on an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-cost-analysis`

flag. The following example updates an existing AKS cluster in the `Standard`

tier to enable cost analysis:```
az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-cost-analysis
```


Results:

```
{
"id": "/subscriptions/xxxxx/resourceGroups/AKSCostRGxxxx",
"name": "AKSCostClusterxxxx",
"properties": {
"provisioningState": "Succeeded"
}
}
```


Note

An agent is deployed to the cluster when you enable the add-on. The agent consumes a small amount of CPU and Memory resources.

Warning

The AKS cost analysis add-on Memory usage is dependent on the number of containers deployed. You can roughly approximate Memory consumption using *200 MB + 0.5 MB per container*. The current Memory limit is set to *4 GB*, which supports approximately *7000 containers per cluster*. These estimates are subject to change.

Note

Enabling the cost analysis also creates a [managed identity](/en-us/entra/identity/managed-identities-azure-resources/overview) named `cost-analysis-identity`

with read access to the cluster's node resource group, and assigns it to the node pools in the cluster.
This is used to collect the ARM identifiers of cluster assets for reporting.

Since there is already a managed identity for the node pool itself, any commands on the node that use managed identities will need to [specify the identity to use](/en-us/entra/identity/managed-identities-azure-resources/managed-identities-faq#what-identity-will-imds-default-to-if-i-dont-specify-the-identity-in-the-request) rather than relying on the default.

For example, `az login --identity --resource-id <resource ID of identity>`

.

## Disable cost analysis on your AKS cluster

Disable cost analysis using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--disable-cost-analysis`

flag.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-cost-analysis
```


Results:

```
{
"id": "/subscriptions/xxxxx/resourceGroups/AKSCostRGxxxx",
"name": "AKSCostClusterxxxx",
"properties": {
"provisioningState": "Succeeded"
}
}
```


Note

If you want to downgrade your cluster from the `Standard`

or `Premium`

tier to the `Free`

tier while cost analysis is enabled, you must first disable cost analysis.

## View the cost data

You can view cost allocation data in the Azure portal. For more information, see [View AKS costs in Microsoft Cost Management](/en-us/azure/cost-management-billing/costs/view-kubernetes-costs).

### Cost definitions

In the Kubernetes namespaces and assets views, you might see any of the following charges:

**Idle charges**represent the cost of available resource capacity that isn't used by any workloads.**Service charges**represent the charges associated with the service, like Uptime SLA, Microsoft Defender for Containers, etc.**System charges**represent the cost of capacity reserved by AKS on each node to run system processes required by the cluster, including the kubelet and container runtime.[Learn more](concepts-clusters-workloads#resource-reservations).**Unallocated charges**represent the cost of resources that couldn't be allocated to namespaces.

Note

It might take *up to one day* for data to finalize. After 24 hours, any fluctuations in costs for the previous day will have stabilized.

## Troubleshooting

If you're experiencing issues, such as the `cost-agent`

pod getting `OOMKilled`

or stuck in a `Pending`

state, see [Troubleshoot AKS cost analysis add-on issues](/en-us/troubleshoot/azure/azure-kubernetes/aks-cost-analysis-add-on-issues).

## Next steps

For more information on cost in AKS, see [Understand Azure Kubernetes Service (AKS) usage and costs](understand-aks-costs).
