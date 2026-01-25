---
merged_at: 2026-01-25T12:25:33.921069
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-netapp-files.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files -->

# Configure Azure NetApp Files for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A persistent volume represents a piece of storage that has been provisioned for use with Kubernetes pods. A persistent volume can be used by one or many pods, and it can be statically or dynamically provisioned. This article shows you how to configure [Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-introduction) to be used by pods on an Azure Kubernetes Service (AKS) cluster.

[Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-introduction) is an enterprise-class, high-performance, metered file storage service running on Azure and supports volumes using [NFS](azure-netapp-files-nfs) (NFSv3 or NFSv4.1), [SMB](azure-netapp-files-smb), and [dual-protocol](azure-netapp-files-dual-protocol) (NFSv3 and SMB, or NFSv4.1 and SMB). Kubernetes users have two options for using Azure NetApp Files volumes for Kubernetes workloads:

- Create Azure NetApp Files volumes
**statically**. In this scenario, the creation of volumes is external to AKS. Volumes are created using the Azure CLI or from the Azure portal, and are then exposed to Kubernetes by the creation of a`PersistentVolume`

. Statically created Azure NetApp Files volumes have many limitations (for example, inability to be expanded, needing to be over-provisioned, and so on). Statically created volumes aren't recommended for most use cases. - Create Azure NetApp Files volumes
**dynamically**, orchestrating through Kubernetes. This method is the**preferred**way to create multiple volumes directly through Kubernetes, and is achieved using[Trident](https://docs.netapp.com/us-en/trident/index.html). Trident is a CSI-compliant dynamic storage orchestrator that helps provision volumes natively through Kubernetes.

Note

Dual-protocol volumes can only be created **statically**. For more information on using dual-protocol volumes with Azure Kubernetes Service, see [Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol).

Using a CSI driver to directly consume Azure NetApp Files volumes from AKS workloads is the recommended configuration for most use cases. This requirement is accomplished using Trident, an open-source dynamic storage orchestrator for Kubernetes. Trident is an enterprise-grade storage orchestrator purpose-built for Kubernetes, and fully supported by NetApp. It simplifies access to storage from Kubernetes clusters by automating storage provisioning.

You can take advantage of Trident's Container Storage Interface (CSI) driver for Azure NetApp Files to abstract underlying details and create, expand, and snapshot volumes on-demand.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

The following considerations apply when you use Azure NetApp Files:

- Your AKS cluster must be
[in a region that supports Azure NetApp Files](https://azure.microsoft.com/global-infrastructure/services/?products=netapp®ions=all). - The Azure CLI version 2.0.59 or higher installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - After the initial deployment of an AKS cluster, you can choose to provision Azure NetApp Files volumes statically or dynamically.
- To use dynamic provisioning with Azure NetApp Files with Network File System (NFS), install and configure
[Trident](https://docs.netapp.com/us-en/trident/index.html)version 19.07 or higher. To use dynamic provisioning with Azure NetApp Files with Secure Message Block (SMB), install and configure Trident version 22.10 or higher. Dynamic provisioning for SMB shares is only supported on windows worker nodes. - Before you deploy Azure NetApp Files SMB volumes, you must identify the AD DS integration requirements for Azure NetApp Files to ensure that Azure NetApp Files is well connected to AD DS. For more information, see
[Understand guidelines for Active Directory Domain Services site design and planning](/en-us/azure/azure-netapp-files/understand-guidelines-active-directory-domain-service-site). Both the AKS cluster and Azure NetApp Files must have connectivity to the same AD.

## Configure Azure NetApp Files for AKS workloads

This section describes how to set up Azure NetApp Files for AKS workloads. It's applicable for all scenarios within this article.

Define variables for later usage. Replace

*myresourcegroup*,*mylocation*,*myaccountname*,*mypool1*,*poolsize*,*premium*,*myvnet*,*myANFSubnet*, and*myprefix*with appropriate values for your environment.`RESOURCE_GROUP="myresourcegroup" LOCATION="mylocation" ANF_ACCOUNT_NAME="myaccountname" POOL_NAME="mypool1" SIZE="poolsize" # size in TiB SERVICE_LEVEL="Premium" # valid values are Standard, Premium and Ultra VNET_NAME="myvnet" SUBNET_NAME="myANFSubnet" ADDRESS_PREFIX="myprefix"`

Register the

*Microsoft.NetApp*resource provider by running the following command:`az provider register --namespace Microsoft.NetApp --wait`

Note

This operation can take several minutes to complete.

Create a new account by using the command

. When you create an Azure NetApp account for use with AKS, you can create the account in an existing resource group or create a new one in the same region as the AKS cluster.`az netappfiles account create`

`az netappfiles account create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME`

Create a new capacity pool by using the command

. Replace the variables shown in the command with your Azure NetApp Files information. The`az netappfiles pool create`

`account_name`

should be the same as created in Step 3.`az netappfiles pool create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --size $SIZE \ --service-level $SERVICE_LEVEL`

Create a subnet to

[delegate to Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-delegate-subnet)using the command. Specify the resource group hosting the existing virtual network for your AKS cluster. Replace the variables shown in the command with your Azure NetApp Files information.`az network vnet subnet create`

Note

This subnet must be in the same virtual network as your AKS cluster.

`az network vnet subnet create \ --resource-group $RESOURCE_GROUP \ --vnet-name $VNET_NAME \ --name $SUBNET_NAME \ --delegations "Microsoft.Netapp/volumes" \ --address-prefixes $ADDRESS_PREFIX`


## Statically or dynamically provision Azure NetApp Files volumes for NFS or SMB

After you [configure Azure NetApp Files for AKS workloads](#configure-azure-netapp-files-for-aks-workloads), you can statically or dynamically provision Azure NetApp Files using NFS, SMB, or dual-protocol volumes within the capacity pool. Follow instructions in:

[Provision Azure NetApp Files NFS volumes for Azure Kubernetes Service](azure-netapp-files-nfs)[Provision Azure NetApp Files SMB volumes for Azure Kubernetes Service](azure-netapp-files-smb)[Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol)

## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:


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
