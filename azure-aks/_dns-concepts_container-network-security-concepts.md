---
merged_at: 2026-01-25T12:25:33.887535
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: dns-concepts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/dns-concepts -->

# DNS Resolution in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Domain Name System (DNS) resolution is a critical component in Azure Kubernetes Service (AKS), enabling pods and services to communicate using human-readable names instead of IP addresses. AKS provides built-in DNS services to ensure seamless name resolution for both internal cluster resources and external endpoints. Understanding how DNS works in AKS helps cluster operators and developers ensure reliable connectivity, optimize performance, and troubleshoot networking issues effectively.

## CoreDNS in Azure Kubernetes Service

[CoreDNS](https://coredns.io/) is the default DNS service in Azure Kubernetes Service (AKS), providing internal name resolution and service discovery for workloads running in the cluster. It operates as a set of pods in the kube-system namespace and is tightly integrated with Kubernetes networking.

When a pod in AKS issues a DNS query—such as resolving the name of another service—the request is routed to the CoreDNS pods. These pods process the query and return the appropriate IP address or forward the request to an upstream DNS server for external domains.

This architecture ensures a balance between flexibility and operational safety in a managed environment. For details on how to customize CoreDNS in AKS, refer to the [CoreDNS customization guide](coredns-custom).

For information on the CoreDNS project, see [the CoreDNS upstream project page](https://coredns.io/).

## LocalDNS in Azure Kubernetes Service

Note

This document provides an overview of what LocalDNS is and its benefits in AKS. It doesn't include setup instructions. For guidance on enabling and configuring LocalDNS, see the [LocalDNS how-to guide](localdns-custom).

### Overview

LocalDNS is an advanced feature in Azure Kubernetes Service (AKS) that deploys a Domain Name System (DNS) proxy on each node to provide highly resilient, low-latency DNS resolution. By handling DNS queries locally, this proxy reduces traffic to the CoreDNS addon pods, improving overall DNS reliability and performance in the cluster. LocalDNS is especially beneficial in large clusters or environments with high DNS query volumes, where centralized DNS resolution can become a bottleneck.

When LocalDNS is enabled, AKS deploys a local DNS cache as a `systemd`

service on each node. Pods on the node send their DNS queries to this local cache, enabling faster resolution by reducing network hops. This approach also minimizes `conntrack`

table usage, lowering the risk of table exhaustion. Additionally, if upstream DNS becomes unavailable, LocalDNS can continue serving cached responses for a configurable duration, helping maintain pod connectivity and service reliability.

### Key capabilities

**Reduced DNS resolution latency:**Each AKS node runs a LocalDNS`systemd`

service. Workloads running on the node send DNS queries to this service, which resolves them locally, reducing network hops and speeding up DNS lookups.**Customizable DNS behavior:**You can use`kubeDNSOverrides`

and`vnetDNSOverrides`

to control DNS behavior in the cluster.**Avoid conntrack races and conntrack table exhaustion:**Pods send DNS queries to the LocalDNS service on the same node without creating new`conntrack`

table entries. Skipping the connection tracking helps reduce[conntrack races](https://github.com/kubernetes/kubernetes/issues/56903)and avoids User Datagram Protocol (UDP) DNS entries from filling up`conntrack`

tables. This optimization prevents dropped and rejected connections caused by`conntrack`

table exhaustion and race conditions.**Connection upgraded to TCP:**The connection from the`localdns`

cache to the cluster’s CoreDNS service uses Transmission Control Protocol (TCP). TCP allows for connection rebalancing and removes`conntrack`

table entries when the server closes the connection (in contrast to UDP connections, which have a default 30-second timeout). Applications don't need changes, because the`localdns`

service still listens for UDP traffic.**Caching:**The LocalDNS cache plugin can be configured with serveStale and Time to Live (TTL) settings.`serveStale`

,`serveStaleDurationInSeconds`

, and`cacheDurationInSeconds`

parameters can be configured to achieve DNS resiliency, even during an upstream DNS outage.**Protocol control:**You can set the DNS query protocol (such as PreferUDP or ForceTCP) for each domain. This flexibility lets you optimize DNS traffic for specific domains or meet network requirements.

### Other benefits and considerations

| Benefits | Considerations |
|---|---|
Better scalability: Reduces load on centralized CoreDNS pods |
Minimal resource overhead: Uses a small amount of CPU and memory on each node |
Seamless integration: Does not require changes to existing application connections |
Configuration changes: Updates require node image upgrades, which can cause temporary disruptions |
Block invalid search domains: Prevents invalid DNS queries at the node level |

By using LocalDNS, you get faster and more reliable DNS resolution for your workloads, reduce the risk of DNS-related outages, and gain more control over DNS traffic in your AKS environment.

## Next steps

To learn how to enable LocalDNS and configure its settings in your AKS cluster, see the [LocalDNS how-to guide](localdns-custom).

To learn more about core network concepts, see [Network concepts for applications in AKS](concepts-network).


---

<!-- DOCUMENTO FUSIONADO: container-network-security-concepts.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-security-concepts -->

# Advanced Container Networking Services for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services is a suite of services designed to enhance the networking capabilities of Azure Kubernetes Service (AKS) clusters. Advanced Container Networking Services offers the following key feature sets: [ Container Network Observability](#container-network-observability),

[, and](#container-network-security)

**Container Network Security**[. These features provide deep insights into network traffic, strengthen security measures, and optimize network performance for containerized applications running in AKS.](#container-network-performance)

**Container Network Performance**## Container Network Observability

Container Network Observability provides deep insights into network traffic and performance across containerized environments. This feature set **works across both Cilium and non-Cilium data planes**, offering flexibility for diverse networking needs. The feature uses eBPF to enhance scalability and performance by identifying potential bottlenecks and network congestion before applications are affected.

Key benefits of Container Network Observability include:

- Compatibility with all Container Networking Interface (CNI) variants in Azure.
, including node-level metrics and Hubble metrics for detailed network insights.*Container network metrics*- Hubble metrics for Domain Name System (DNS) resolution, pod-to-pod communication, and service interactions.
that capture essential metadata such as IPs, ports, and traffic flow for troubleshooting, monitoring, and security enforcement.*Container network logs*- Integration with the managed service for Prometheus in Azure Monitor and Azure Managed Grafana for simplified metrics storage and visualization.

### Container network metrics

This feature collects node-level metrics, including CPU, memory, and network performance, to monitor the health of cluster nodes. For deeper insights, Hubble metrics provide data on DNS resolution times, service-to-service communication, and pod-level network behavior. These metrics help you analyze application performance, detect anomalies, and optimize workloads.

For more information, see the [metrics overview](container-network-observability-metrics).

### Container network logs

Container network logs give you detailed insight into traffic within and across clusters by capturing metadata like source and destination IP addresses, ports, protocols, and flow direction. These logs enable monitoring network behavior, troubleshooting connectivity issues, and enforcing security policies. Persistent and real-time logging options ensure comprehensive, actionable network observability.

For more information, see the [container network logs overview](container-network-observability-logs).

## Container Network Security

Container Network Security enhances the security posture of AKS clusters by providing advanced network security features. It leverages eBPF technology to enforce network policies at the kernel level, ensuring efficient and effective security controls for containerized applications. **Container Network Security is available only on clusters with Azure CNI Powered by Cilium**.

### FQDN-based filtering

FQDN-based filtering allows you to create network policies based on fully qualified domain names (FQDNs) rather than IP addresses. This capability simplifies policy management, especially in dynamic environments where IP addresses frequently change. By using FQDNs, you can ensure that your applications communicate only with trusted external services, enhancing security and compliance.

For more information, see the [FQDN-based filtering overview](container-network-security-fqdn-filtering-concepts).

### Layer 7 policy

Layer 7 policy enables application-layer traffic control, allowing you to define policies based on specific application protocols. This feature provides granular control over network traffic, enabling you to enforce security policies that align with application behavior. With Layer 7 policy, you can monitor and restrict traffic based on HTTP methods, URLs, headers, and other application-level attributes.

For more information, see the [Layer 7 policy overview](container-network-security-l7-policy-concepts).

### WireGuard Encryption (preview)

WireGuard Encryption leverages the WireGuard protocol to provide secure, encrypted communication between Cilium-managed endpoints within your AKS cluster. This feature ensures that data transmitted over the network is protected from eavesdropping and tampering, enhancing the overall security of your containerized applications.

For more information, see the [WireGuard encryption overview](container-network-security-wireguard-encryption-concepts).

## Container Network Performance

Container Network Performance optimizes network performance for containerized applications running in AKS clusters. It leverages eBPF technology to enhance network routing and reduce latency, ensuring that applications can communicate efficiently and effectively. **Container Network Performance is available only on clusters with Azure CNI Powered by Cilium**.

### eBPF Host Routing

eBPF Host Routing uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in AKS clusters.

For more information, see the [eBPF Host Routing overview](container-network-performance-ebpf-host-routing).
