---
merged_at: 2026-01-25T12:25:33.869284
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: container-network-performance-ebpf-host-routing.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-performance-ebpf-host-routing -->

# Overview of eBPF Host Routing (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

As containerized workloads scale across distributed environments, the need for high-performance, low-latency networking becomes critical. eBPF Host Routing is a performance-focused feature within [Advanced Container Networking Services (ACNS)](advanced-container-networking-services-overview) that uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in Kubernetes clusters. Legacy routing on Kubernetes hosts introduces overhead in the form of iptables and netfilter rule processing in the host network namespace. eBPF Host Routing has benefits over legacy host routing by:

- Implementing the routing logic in eBPF programs.
- Allowing Cilium eBPF to bypass iptables in the host namespace.

This direct path reduces the number of hops and processing layers, resulting in faster packet delivery.

## Key benefits

Reduced latency - Bypassing iptables in host results in lower pod-to-pod latency

Increased throughput - Compared to legacy routing, significant improvements can be observed for pod-to-pod traffic between nodes

Reduced CPU usage - Due to removing iptables-based SNAT and routing logic, a modest reduction of CPU usage

Use cases for eBPF Host Routing are performance-critical workloads such as high-throughput microservices, real-time services, or AI/ML workloads. Ensure deployment environment meets the requirements before enabling.

## Components of eBPF Host Routing

** iptables blocker** - An init container that prevents any future installation of iptables rules in the host network namespace (such rules will be bypassed when eBPF host routing is enabled).

** IP Masquerade Agent** - When eBPF Host Routing is active, Cilium takes over SNAT responsibilities using BPF-based masquerading.

`ip-masq-agent`

remains running to maintain consistent behavior if eBPF Host Routing is later disabled; however, its iptables rules are ignored while eBPF Host Routing is active.## Considerations

Enabling eBPF Host Routing causes iptables rules in the host network namespace to be bypassed. Hence, AKS attempts to detect and block enablement of eBPF Host Routing on clusters where iptables rules are in use in the host network namespace.

On clusters with eBPF host routing enabled, AKS blocks attempts to install iptables rules in the host network namespace. Trying to bypass this block may cause the cluster to be inoperational.


## Limitations

eBPF host routing is currently incompatible with nodes running OSes other than Ubuntu 24.04, or Azure Linux 3.0. eBPF host routing is currently also not supported with Confidential VMs and Pod Sandboxing.

eBPF Host Routing can only be enabled for all nodes in a cluster. Hybrid node scenarios aren't supported.

Windows nodes aren't supported by Azure CNI Powered by Cilium, and by extension, eBPF Host Routing.

Istio add-on can't be used along with eBPF Host Routing enabled clusters.

Dual stack networking isn't supported.


## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to enable

[eBPF Host Routing](how-to-enable-ebpf-host-routing)on AKS.For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](container-network-observability-metrics).


---

<!-- DOCUMENTO FUSIONADO: upgrade.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade -->

# Upgrading Azure Kubernetes Service clusters and node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An Azure Kubernetes Service (AKS) cluster needs to be periodically updated to ensure security and compatibility with the latest features. There are two components of an AKS cluster that are necessary to maintain:

*Cluster Kubernetes version*: Part of the AKS cluster lifecycle involves performing upgrades to the latest Kubernetes version. It’s important that you upgrade to apply the latest security releases and to get access to the latest Kubernetes features, as well as to stay within the[AKS support window](supported-kubernetes-versions#kubernetes-version-support-policy).*Node image version*: AKS regularly provides new node images with the latest OS and runtime updates. It's beneficial to upgrade your nodes' images regularly to ensure support for the latest AKS features and to apply essential security patches and hot fixes.

For Linux nodes, node image security patches and hotfixes may be performed without your initiation as *unattended updates*. These updates are automatically applied, but AKS doesn't automatically reboot your Linux nodes to complete the update process. You're required to use a tool like [kured](node-updates-kured) or [node image upgrade](node-image-upgrade) to reboot the nodes and complete the cycle.

The following table summarizes the details of updating each component:

| Component name | Frequency of upgrade | Planned Maintenance supported | Supported operation methods | Supported operation methods (Multi-Cluster) | Documentation link |
|---|---|---|---|---|---|
| Cluster Kubernetes version upgrade (minor) | Roughly every three months | Yes | Automatic, Manual | Automatic, Manual |
|

[AKS release tracker](release-tracker)[Upgrade an AKS cluster](upgrade-cluster),[Multi-cluster upgrade](/en-us/azure/kubernetes-fleet/concepts-update-orchestration)**Linux**: weekly**Windows**: monthly[AKS node image upgrade](node-image-upgrade),[Multi-cluster upgrade](/en-us/azure/kubernetes-fleet/concepts-update-orchestration)[AKS node security patches](concepts-vulnerability-management#worker-nodes)## Multi-cluster upgrade

When you have multiple clusters, an important practice that you should include as part of your upgrade process is remembering to follow commonly used deployment and testing patterns. Testing an upgrade in a development or test environment before deployment in production is an important step to ensure application functionality and compatibility with the target environment. It can help you identify and fix any errors, bugs, or issues that might affect the performance, security, or usability of the application or underlying infrastructure.

[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview) has built-in support for [multi-cluster upgrades](/en-us/azure/kubernetes-fleet/concepts-update-orchestration) which implements the best practice above to minimize application disruptions caused by cluster upgrades. Besides allowing you to customize the order of upgrades of multiple clusters, it also allows you to use consistent node OS image versions across clusters in different regions.

## Automatic upgrades

Automatic upgrades can be performed through [auto upgrade channels](auto-upgrade-cluster) or via [GitHub Actions](node-upgrade-github-actions).

[Automatic multi-cluster upgrades](/en-us/azure/kubernetes-fleet/update-automation) can be performed through [Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview) to adopt the best practice of testing and verifying an upgrade in a development or test environment before production.

## Planned maintenance

[Planned maintenance](planned-maintenance) allows you to schedule weekly maintenance windows that will update your control plane and your kube-system pods, helping to minimize workload impact.

## Troubleshooting

To find details and solutions to specific issues, view the following troubleshooting guides:

## Next steps

For more information what cluster operations may trigger specific upgrade events, upgrade best practices, and other considerations, see the [AKS operator's guide on patching](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).
