---
merged_at: 2026-01-25T12:25:33.941057
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: long-term-support.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/long-term-support -->

# Long-term support for Azure Kubernetes Service (AKS) versions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Kubernetes community releases a new minor version approximately every four months, with a support window for each version for one year. In Azure Kubernetes Service (AKS), this support window is called *community support*.

AKS supports versions of Kubernetes that are within this *community support* window to push bug fixes and security updates from community releases. While the community support release cadence provides benefits, it requires that you keep up to date with Kubernetes releases, which can be difficult depending on your application's dependencies and the pace of change in the Kubernetes ecosystem.

To help you manage your Kubernetes version upgrades, AKS provides a *long-term support* (LTS) option, which extends the support window for a Kubernetes version to give you more time to plan and test upgrades to newer Kubernetes versions.

## AKS support types

After approximately one year, a given Kubernetes minor version exits *community support*, making bug fixes and security updates unavailable for your AKS clusters.

AKS offers one year of *community support* and one year of *long-term support* to backport security fixes from the upstream community. The upstream LTS working group contributes to the community, extending the support window. LTS provides more time to plan and test upgrades over two years from the Kubernetes version's general availability (GA).

| Community support | Long-term support | |
|---|---|---|
When to use |
When you can keep up with upstream Kubernetes releases | When you need control over when to migrate from one version to another |
Supported versions |
Three most recent GA minor versions | All supported Kubernetes versions from 1.27 onward are eligible for Long-Term Support (LTS). |

## LTS Patch process

LTS supports only the two most recent patch versions. This differs from Community support, where all patch versions are supported. However, AKS reserves the right to deprecate any patch version in response to critical security vulnerabilities (CVEs). For more details on community support policy, see [Kubernetes version support policy](supported-kubernetes-versions#kubernetes-version-support-policy).

To identify the latest supported patch versions, refer to the [AKS release tracker](https://releases.aks.azure.com/webpage/index.html).

We recommend enabling the [auto-upgrade patch channel](auto-upgrade-cluster) to ensure your clusters remain up-to-date with the latest patches.

## Enable long-term support

**Enabling LTS requires moving your cluster to the Premium tier and explicitly selecting the LTS support plan**. While it's possible to enable LTS when the cluster is in *community support*, you're charged once you enable the Premium tier.

Note

We strongly recommend enabling the patch auto-upgrade channel to ensure your cluster always receives the latest supported patches. LTS only supports the last two patch versions for each minor version. Clusters not on the latest patches may lose support.

### Enable LTS on a new cluster

Create a new cluster with LTS enabled using the

command.`az aks create`

The following command creates a new AKS cluster with LTS enabled using Kubernetes version 1.27 as an example. To review available Kubernetes releases, see the

[AKS release tracker](release-tracker).`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --tier premium \ --k8s-support-plan AKSLongTermSupport \ --kubernetes-version 1.27 \ --auto-upgrade-channel patch \ --generate-ssh-keys`


### Enable LTS on an existing cluster

Enable LTS on an existing cluster using the

command.`az aks update`

`az aks update --resource-group <resource-group-name> --name <cluster-name> --tier premium --k8s-support-plan AKSLongTermSupport --auto-upgrade-channel patch`


Tip

To see which Kubernetes versions you can upgrade to, use the [AKS release tracker](https://releases.aks.azure.com/webpage/index.html) or run `az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name>`

.

## Migrate to the latest LTS version

The upstream Kubernetes community supports a two-minor-version upgrade path. The process migrates the objects in your Kubernetes cluster as part of the upgrade process, and provides a tested and accredited migration path.

If you want to carry out an in-place migration, the AKS service migrates your control plane from the previous LTS version to the latest, and then migrate your data plane. To carry out an in-place upgrade to the latest LTS version, you need to specify an LTS enabled Kubernetes version as the upgrade target.

Migrate to the latest LTS version using the

command.`az aks upgrade`

The following command uses Kubernetes version 1.32.2 as an example version. To review available Kubernetes releases, see the

[AKS release tracker](release-tracker).`az aks upgrade --resource-group <resource-group-name> --name <cluster-name> --kubernetes-version 1.32.2`

Note

Moving forward, all AKS Kubernetes versions will be LTS-compatible. For the latest LTS calendar, visit the

[AKS Kubernetes Release Calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar). To view available LTS releases and their patches by region, see the[AKS release tracker](release-tracker).

## Disable long-term support on an existing cluster

**Disabling LTS on an existing cluster requires moving your cluster to the free or standard tier and explicitly selecting the KubernetesOfficial support plan**.

There are approximately two years between one LTS version and the next. In lieu of upstream support for migrating more than two minor versions, there's a high likelihood your application depends on Kubernetes APIs that are deprecated. We recommend you thoroughly test your application on the target LTS Kubernetes version and carry out a blue/green deployment from one version to another.

Disable LTS on an existing cluster using the

command.`az aks update`

`az aks update --resource-group <resource-group-name> --name <cluster-name> --tier [free|standard] --k8s-support-plan KubernetesOfficial`

Upgrade the cluster to a later supported version using the

command.`az aks upgrade`

The following command uses Kubernetes version 1.28.3 as an example version. To review available Kubernetes releases, see the

[AKS release tracker](release-tracker).`az aks upgrade --resource-group <resource-group-name> --name <cluster-name> --kubernetes-version 1.28.3`


## Unsupported add-ons and features

The AKS team currently tracks add-on versions where Kubernetes community support exists. Once a version leaves community support, we rely on open-source projects for managed add-ons to continue that support. Due to various external factors, some add-ons and features might not support Kubernetes versions outside these upstream community support windows.

The following table provides a list of add-ons and features that aren't supported and the reasons they're unsupported:

| Add-on / Feature | Reason it's unsupported |
|---|---|
| Calico | Requires Calico Enterprise agreement past community support. |
| Key Management Service (KMS) | KMSv2 replaces KMS during this LTS cycle. |
| Dapr | AKS extensions aren't supported. |
| Application Gateway Ingress Controller | Migration to App Gateway for Containers happens during LTS period. |
| Open Service Mesh | OSM is deprecated. |
| AAD Pod Identity | Deprecated in place of Workload Identity. |

Note

You can't move your cluster to long-term support if any of these add-ons or features are enabled.

While these AKS managed add-ons aren't supported by Microsoft, you can install their open-source versions on your cluster if you want to use them past community support.

## How we decide the next LTS version

Versions of Kubernetes LTS are available for two years from GA, and we mark a higher version of Kubernetes as LTS based on the following criteria:

- That sufficient time elapsed for customers to migrate from the prior LTS version to the current LTS version.
- The previous version completed a two year support window.

Read the [AKS release notes](https://github.com/Azure/AKS/releases) to stay informed of when you're able to plan your migration.

## Frequently asked questions

### Can I create a new AKS cluster with an LTS version after community support ends?

Yes, you can create a new AKS cluster using an LTS version even after its community support period has ended, provided you have opted into LTS. However, this is only valid until the end of the LTS version's lifecycle. After that, you must upgrade to the next supported LTS version. For more details, see the [AKS Kubernetes Release Calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar).

### Can I enable and disable LTS on an AKS-supported version after community support ends?

Yes, you can enable the LTS support plan on any AKS-supported version even after its community support period has ended. However, once the community support period has ended, you can't disable LTS for that version.

### Does a community-supported AKS cluster automatically become LTS eligible after End of Life?

No, you must explicitly enable LTS on the cluster to receive support. This also requires upgrading to the Premium tier. Refer to the [Premium tier pricing](https://azure.microsoft.com/pricing/details/kubernetes-service/) for more information.

### Will every AKS version support Long-Term Support (LTS)?

Yes, AKS ensures that all supported Kubernetes versions are eligible for Long-Term Support (LTS). You can opt into LTS for any supported version available today.

### What is the pricing model for LTS?

LTS is available on the Premium tier refer to the [Premium tier pricing](https://azure.microsoft.com/pricing/details/kubernetes-service/) for more information.

### Will enabling LTS disrupt workloads?

No. It’s a configuration-only change; it doesn’t reimage nodes or disrupt workloads, so no downtime is expected.


---

<!-- DOCUMENTO FUSIONADO: concepts-network-azure-cni-overlay.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-network-azure-cni-overlay -->

# Overview of Azure CNI Overlay networking in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure CNI Overlay is a networking model for Azure Kubernetes Service (AKS) that provides efficient IP address management and high-performance pod communication. This article provides an overview of Azure CNI Overlay, including its architecture, IP address planning, and differences from the traditional kubenet networking model.

## Overview of overlay networking

The traditional [Azure Container Networking Interface (CNI)](configure-azure-cni) assigns a virtual network IP address to every pod. It assigns this IP address from a reserved set of IPs on every node *or* a separate subnet reserved for pods. This approach requires IP address planning and might lead to address exhaustion, which introduces difficulties scaling your clusters as your application demands grow.

In overlay networking, only the Kubernetes cluster nodes are assigned IPs from subnets. Pods receive IPs from a private Classless Inter-Domain Routing (CIDR) range provided at the time of cluster creation. Each node is assigned a `/24`

address space carved out from the same CIDR. Extra nodes created when you scale out a cluster automatically receive `/24`

address spaces from the same CIDR. Azure CNI assigns IPs to pods from this `/24`

space.

A separate routing domain is created in the Azure networking stack for the pod's private CIDR space. This domain creates an overlay network for direct communication between pods. There's no need to provision custom routes on the cluster subnet or use an encapsulation method to tunnel traffic between pods, which provides connectivity performance between pods on par with virtual machines (VMs) in a virtual network. Workloads running within the pods aren't even aware that network address manipulation is happening.


Communication with endpoints outside the cluster, such as on-premises and peered virtual networks, uses the node IP through network address translation (NAT). Azure CNI translates the source IP (overlay IP of the pod) of the traffic to the primary IP address of the VM. This translation enables the Azure networking stack to route the traffic to the destination.

Endpoints outside the cluster can't connect to a pod directly. You have to publish the pod's application as a Kubernetes Load Balancer service to make it reachable on the virtual network.

You can provide outbound (egress) connectivity to the internet for overlay pods by using a [standard load balancer](egress-outboundtype#outbound-type-of-loadbalancer) or [managed NAT gateway](nat-gateway). You can also control egress traffic by directing it to a firewall via [user-defined routes on the cluster subnet](egress-outboundtype#outbound-type-of-userdefinedrouting).

You can configure ingress connectivity to the cluster by using an ingress controller, such as Application Gateway for Containers, NGINX, or the application routing add-on.

## Differences between kubenet and Azure CNI Overlay

Like Azure CNI Overlay, kubenet assigns IP addresses to pods from an address space that's logically different from the virtual network, but it has scaling and other limitations. The following table provides a detailed comparison between kubenet and Azure CNI Overlay:

| Area | Azure CNI Overlay | kubenet |
|---|---|---|
| Cluster scale | 5,000 nodes and 250 pods per node | 400 nodes and 250 pods per node |
| Network configuration | Simple - no extra configurations required for pod networking | Complex - requires route tables and user-defined routes on the cluster subnet for pod networking |
| Pod connectivity performance | Performance on par with VMs in a virtual network | Extra hop adds latency |
| Kubernetes network policies | Azure network policies, Calico, Cilium | Calico |
| OS platforms supported | Linux, Windows Server 2022, Windows Server 2019 | Linux only |

Note

If you don't want to assign virtual network IP addresses to pods due to IP shortage, we recommend using Azure CNI Overlay.

## IP address planning

The following sections provide guidance on how to plan your IP address space for Azure CNI Overlay.

### Cluster nodes

When you set up your AKS cluster, make sure that your virtual network subnets have enough room to grow for future scaling. You can assign each node pool to a dedicated subnet. A `/24`

subnet can fit up to 251 nodes because the first three IP addresses are reserved for management tasks.

### Pods

The `/24`

size that Azure CNI Overlay assigns is fixed and can't be increased or decreased. You can run up to 250 pods on a node. When you plan the pod address space, ensure that the private CIDR is large enough to provide `/24`

address spaces for new nodes to support future cluster expansion.

When you plan IP address space for pods, consider the following factors:

- You can use the same pod CIDR space on multiple independent AKS clusters in the same virtual network.
- Pod CIDR space must not overlap with the cluster subnet range.
- Pod CIDR space must not overlap with directly connected networks, like virtual network peering, Azure ExpressRoute, or VPN. If external traffic has source IPs in the pod CIDR range, it needs translation to a non-overlapping IP via Source Network Address Translation (SNAT) to communicate with the cluster.
- Pod CIDR space
*can only be expanded*.

### Kubernetes service address range

The size of the service address CIDR depends on the number of cluster services that you plan to create. It must be smaller than `/12`

. This range shouldn't overlap with the pod CIDR range, cluster subnet range, and IP range used in peered virtual networks and on-premises networks.

### Kubernetes service IP address for DNS

The IP address for DNS is within the Kubernetes service address range that cluster service discovery uses. Don't use the first IP address in your address range, because this address is used for the `kubernetes.default.svc.cluster.local`

address.

Important

The private CIDR ranges available for the pod CIDR are defined in [RFC 1918](https://tools.ietf.org/html/rfc1918) and [RFC 6598](https://tools.ietf.org/html/rfc6598). Although we don't block the use of public IP ranges, they're considered out of Microsoft's support scope. We recommend using private IP ranges for the pod CIDR.

When you use Azure CNI in overlay mode, ensure that the pod CIDR doesn't overlap with any external IP addresses or networks (such as on-premises networks, peered virtual networks, or ExpressRoute). If an external host uses an IP within the pod CIDR, packets destined for that host from the pod might be redirected into the overlay network and SNAT'd by the node. This situation causes the external endpoint to become unreachable.

## Network security groups

Pod-to-pod traffic with Azure CNI Overlay isn't encapsulated, and subnet [network security group (NSG)](/en-us/azure/virtual-network/network-security-groups-overview) rules are applied. If the subnet NSG contains deny rules that would affect the pod CIDR traffic, make sure that the following rules are in place to ensure proper cluster functionality (in addition to all [AKS egress requirements](limit-egress-traffic)):

- Traffic from the node CIDR to the node CIDR on all ports and protocols
- Traffic from the node CIDR to the pod CIDR on all ports and protocols (required for service traffic routing)
- Traffic from the pod CIDR to the pod CIDR on all ports and protocols (required for pod-to-pod and pod-to-service traffic, including DNS)

Traffic from a pod to any destination outside the pod CIDR block uses SNAT to set the source IP to the IP of the node where the pod runs.

If you want to restrict traffic between workloads in the cluster, we recommend using [network policies](use-network-policies).

## Maximum pods per node

You can configure the maximum number of pods per node at the time of cluster creation or when you add a new node pool. The default for Azure CNI Overlay is 250. The maximum value that you can specify in Azure CNI Overlay is 250, and the minimum value is 10. The value for maximum pods per node that you configure during creation of a node pool applies to the nodes in that node pool only.

Choosing a network model

Azure CNI offers two IP addressing options for pods: *overlay networking* and the *traditional configuration that assigns virtual network IPs to pods*. The choice of which option to use for your AKS cluster is a balance between flexibility and advanced configuration needs. The following considerations help outline when each network model might be the most appropriate.

Use overlay networking when:

- You want to scale to a large number of pods but are limited by IP address space in your virtual network.
- Most of the pod communication is within the cluster.
- You don't need advanced AKS features, such as virtual nodes.

Use the traditional virtual network option when:

- You have available IP address space.
- Most of the pod communication is to resources outside the cluster.
- Resources outside the cluster need to reach pods directly.
- You need AKS advanced features, such as virtual nodes.

## Limitations with Azure CNI Overlay

Azure CNI Overlay has the following limitations:

- VM availability sets aren't supported.
- You can't use
[DCsv2-series](/en-us/azure/virtual-machines/dcv2-series)virtual machines in node pools. To meet requirements for confidential computing, consider using[DCasv5 or DCadsv5-series confidential VMs](/en-us/azure/virtual-machines/dcasv5-dcadsv5-series)instead. - If you're using your own subnet to deploy the cluster, the names of the subnet, the virtual network, and the resource group that contains the virtual network must be 63 characters or fewer. These names are used as labels in AKS worker nodes, so they're subject to
[Kubernetes syntax rules for labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#syntax-and-character-set).

## Related content

To get started with Azure CNI Overlay in AKS, see the following articles:
