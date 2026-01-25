---
merged_at: 2026-01-25T12:06:27.810828
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-cvm.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-cvm -->

# Use Confidential Virtual Machines (CVM) in Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Confidential Virtual Machines (CVM)](/en-us/azure/confidential-computing/confidential-vm-overview) offer strong security and confidentiality for tenants. CVMs offer VM based Hardware Trusted Execution Environment (TEE) that leverage SEV-SNP security features to deny the hypervisor and other host management code access to VM memory and state, providing defense in depth protections against operator access. These features enable node pools with CVM to target the migration of highly sensitive container workloads to AKS without any code refactoring while benefiting from the features of AKS. For example, you may require CVM if you have the following:

- Workloads that handle security critical data and/or sensitive customer data
- Services that are required to meet various compliance requirements, especially for government contracts. Without a scalable solution for securing data, this could potentially lead to the loss of accreditations and contracts.

In this article, you learn how to create AKS node pools using Confidential VM sizes.

## AKS supported confidential VM sizes

Azure offers a choice of [Trusted Execution Environment (TEE)](/en-us/azure/confidential-computing/trusted-execution-environment) options from both AMD and Intel. These TEEs allow you to create Confidential VM environments with excellent price-to-performance ratios, all without requiring any code changes.

- AMD-based Confidential VMs, use AMD SEV-SNP technology, which is introduced with third Gen AMD EPYC™ processors.
- Intel-based Confidential VMs use Intel TDX, with fourth Gen Intel® Xeon® processors.

Both technologies have different implementations. However both provide similar protections from the cloud infrastructure stack. For more information, see [CVM VM sizes](/en-us/azure/confidential-computing/virtual-machine-options).

## Security Features

CVMs offer the following security enhancements as compared to other virtual machine (VM) sizes:

- Robust hardware-based isolation between virtual machines, hypervisor, and host management code.
- Customizable attestation policies to ensure the host's compliance before deployment.
- Cloud-based Confidential OS disk encryption before the first boot.
- VM encryption keys that the platform or the customer (optionally) owns and manages.
- Secure key release with cryptographic binding between the platform's successful attestation and the VM's encryption keys.
- Dedicated virtual Trusted Platform Module (TPM) instance for attestation and protection of keys and secrets in the virtual machine.
- Secure boot capability similar to Trusted launch for Azure VMs

## How does it work?

If you're running a workload that requires enhanced confidentiality and integrity, you can benefit from memory encryption and enhanced security without code changes in your application. All pods on your CVM node are part of the same trust boundary. The nodes in a node pool created with CVM use a customized [node image](node-images) specially configured for CVM.

### Supported OS Versions

You can create CVM node pools on Linux OS types (Ubuntu and Azure Linux). However, not all OS versions support CVM node pools.

This table includes the supported OS versions:

| OS Type | OS SKU | CVM support | CVM default |
|---|---|---|---|
| Linux | `Ubuntu` |
Supported | Ubuntu 20.04 is default for K8s version 1.24-1.33. Ubuntu 24.04 is the default for K8s version 1.34-1.38. |
| Linux | `Ubuntu2204` |
Not Supported | AKS doesn't support CVM for Ubuntu 22.04. |
| Linux | `Ubuntu2404` |
Supported | CVM is supported on `Ubuntu2404` in K8s 1.32-1.38. |
| Linux | `AzureLinux` |
Supported on Azure Linux 3.0 | Azure Linux 3 is default when enabling CVM for K8s version 1.28-1.36. |
| Linux | `flatcar` |
Not supported |
|

`AzureLinuxOSGuard`

[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard)doesn't support CVM.When using `Ubuntu`

or `AzureLinux`

as the `osSKU`

, if the default OS version doesn't support CVM, AKS defaults to the most recent CVM-supported version of the OS. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support CVM, AKS defaults to Ubuntu 20.04 for Linux CVM-enabled node pools.

### Limitations

The following limitations apply when adding a node pool with CVM to AKS:

- You can't use FIPS, ARM64, Trusted Launch, or Pod Sandboxing.
- You can't update an existing node pool to migrate to a CVM size. To migrate, you'll need to
[resize your node pool](resize-node-pool). - You can't use CVM with Windows node pools.
- CVM with Azure Linux is currently in preview.

## Prerequisites

Before you begin, make sure you have the following:

- An existing AKS cluster.
- CVM sizes must be available for your subscription in the region where the cluster is created. You must have sufficient quota to create a node pool with a CVM size.
- If you're using Azure Linux os, you need to install the
`aks-preview`

extension, update the`aks-preview`

extension, and register the preview feature flag. If you're using Ubuntu, you can skip these steps.

### If you are using Azure Linux

CVMs for Ubuntu is GA, but CVMs with Azure Linux is currently still in preview. If you would like to use CVM node pools with Azure Linux as the OS of choice, ensure you enable the extension and register the flag.

#### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

`az extension update --name aks-preview`


#### Register `AzureLinuxCVMPreview`

feature flag

Register the

`AzureLinuxCVMPreview`

feature flag using the [`az feature register`

][az-feature-register] command.`az feature register --namespace "Microsoft.ContainerService" --name "AzureLinuxCVMPreview"`

Verify the registration status using the [

`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.`az feature show --namespace Microsoft.ContainerService --name AzureLinuxCVMPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Add a node pool with a CVM to your AKS cluster

Add a node pool with a CVM to your AKS cluster using the

command and set the`az aks nodepool add`

`node-vm-size`

to a supported[VM size](/en-us/azure/confidential-computing/virtual-machine-options).`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --node-count 3 \ --node-vm-size Standard_DC4as_v5`


If you don't specify the `osSKU`

or `osType`

, AKS defaults to `--os-type Linux`

and `--os-sku Ubuntu`

.

## Upgrade an existing node pool with a CVM to Ubuntu 24.04

Upgrade an existing node pool with a CVM to Ubuntu 24.04 from Ubuntu 20.04 using the

command. Set the`az aks nodepool update`

`os-sku`

as`Ubuntu2404`

.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --os-sku Ubuntu2404`


Note

A node pool which is Ubuntu 24.04 with a CVM is supported from AKS cluster 1.33 version. Additionally, before Ubuntu 24.04 becomes GA, you need to register the `Ubuntu2404Preview`

feature. For more information, see [ here](/en-us/azure/aks/upgrade-os-version#register-ubuntu2404preview-feature-flag) to register the feature.

## Verify the node pool uses CVM

Verify a node pool uses CVM using the

command and verify the`az aks nodepool show`

`vmSize`

is`Standard_DCa4_v5`

.`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize'`

The following example command and output shows the node pool uses CVM:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize' "Standard_DC4as_v5"`

Verify a node pool uses a CVM image using the

command.`az aks nodepool list`

`az aks nodepool list \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion'`

The following example command and output shows the node pool uses an Ubuntu 20.04 CVM image:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion' "AKSUbuntu-2004cvmcontainerd-202507.02.0"`


## Remove a node pool with CVM from an AKS cluster

Remove a node pool with CVM from an AKS cluster using the

command.`az aks nodepool delete`

`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool`


## Next steps

In this article, you learned how to add a node pool with CVM to an AKS cluster.

- For more information about CVM, see
[Confidential VM node pools support on AKS](/en-us/azure/confidential-computing/confidential-node-pool-aks). - To migrate an existing node pool to a CVM vm size, you can
[resize your node pool](resize-node-pool). - If you're only interested in enabling Trusted Launch on your node pools, see
[Trusted Launch on AKS](use-trusted-launch).


---

<!-- DOCUMENTO FUSIONADO: container-network-observability-metrics.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-metrics -->

# What is container network metrics?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services in Azure Kubernetes Service (AKS) facilitates the collection of comprehensive container network metrics to give you valuable insights into the performance of your containerized environment. The capability continuously captures essential metrics at the node level and pod level, including traffic volume, dropped packets, connection states, and Domain Name System (DNS) resolution times for effective monitoring and optimizing network performance.

Capturing these metrics is essential for understanding how containers communicate, how traffic flows between services, and where bottlenecks or disruptions might occur. Advanced Container Networking Services integrates seamlessly with monitoring tools like Prometheus and Grafana to give you a complete view of networking metrics. Use the metrics for in-depth troubleshooting, network optimization, and performance tuning.

In a cloud-native world, maintaining a healthy and efficient network in a dynamic containerized environment is vital to ensuring that applications perform as expected. Without proper visibility into network traffic and its patterns, identifying potential issues or inefficiencies becomes challenging.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Key benefits

Deep visibility into network performance

Enhanced troubleshooting and optimization

Proactive anomaly detection

Better resource management and scaling

Capacity planning and compliance

Source-level metrics filtering for cost optimization and noise reduction with

[container network metrics filtering](#container-network-metrics-filtering-preview)Simplified metrics storage and visualization options. Choose between:

**Azure managed service for Prometheus and Azure Managed Grafana**: Azure manages the infrastructure and maintenance, so you can focus on configuring metrics and visualizing metrics.**Bring your own (BYO) Prometheus and Grafana**: You deploy and configure your own instances of Prometheus and Grafana, and you manage the underlying infrastructure.


## Metrics captured

### Node-level metrics

Understanding the health of your container network at the node-level is crucial for maintaining optimal application performance. These metrics provide insights into traffic volume, dropped packets, number of connections, and other data by node. The metrics are stored in Prometheus format, so, you can view them in Grafana.

The following metrics are aggregated per node. All metrics include one of these labels:

`cluster`

`instance`

(node name)

For Cilium data plane scenarios, Container Network Observability provides metrics only for Linux. Windows is currently not supported. Cilium exposes several metrics including the following used by Container Network Observability.

| Metric name | Description | Extra labels | Linux | Windows |
|---|---|---|---|---|
cilium_forward_count_total |
Total forwarded packet count | `direction` |
✅ | ❌ |
cilium_forward_bytes_total |
Total forwarded byte count | `direction` |
✅ | ❌ |
cilium_drop_count_total |
Total dropped packet count | `direction` , `reason` |
✅ | ❌ |
cilium_drop_bytes_total |
Total dropped byte count | `direction` , `reason` |
✅ | ❌ |

### Pod-level metrics (Hubble metrics)

These Prometheus metrics include source and destination pod information so that you can pinpoint network-related issues at a granular level. Metrics cover information like traffic volume, dropped packets, TCP resets, and Layer 4/Layer 7 packet flows. DNS metrics like DNS errors and DNS requests missing responses are collected by default for non-Cilium data planes. For Cilium data planes, a Cilium FQDN network policy is required to collect DNS metrics, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.

The following table describes the metrics that are aggregated per pod (node information is preserved).

All metrics include labels:

`cluster`

`instance`

(node name)`source`

or`destination`

For

*outgoing traffic*, a`source`

label that indicates the source pod namespace and name is applied.For

*incoming traffic*, a`destination`

label that indicates the destination pod namespace and name is applied.


| Metric name | Description | Extra Labels | Linux | Windows |
|---|---|---|---|---|
hubble_dns_queries_total |
Total DNS requests by query | `source` or `destination` , `query` , `qtypes` (query type) |
✅ | ❌ |
hubble_dns_responses_total |
Total DNS responses by query/response | `source` or `destination` , `query` , `qtypes` (query type), `rcode` (return code), `ips_returned` (number of IPs) |
✅ | ❌ |
hubble_drop_total |
Total dropped packet count | `source` or `destination` , `protocol` , `reason` |
✅ | ❌ |
hubble_tcp_flags_total |
Total TCP packets count by flag | `source` or `destination` , `flag` |
✅ | ❌ |
hubble_flows_processed_total |
Total network flows processed (Layer 4/Layer 7 traffic) | `source` or `destination` , `protocol` , `verdict` , `type` , `subtype` |
✅ | ❌ |

## Container network metrics filtering (Preview)

Now that you have the ability to collect comprehensive metrics at both node and pod levels, you might find yourself dealing with a significant volume of data. To help reduce noise and optimize storage costs, Container Network Observability introduces **container network metrics filtering**. This feature enables you to filter metrics at the source before they are collected and stored, giving you control over which metrics are most relevant to your specific monitoring and troubleshooting needs. This feature is only available for Cilium clusters.

Container network metrics filtering is particularly valuable in large-scale production environments where the sheer volume of metrics can impact storage costs and query performance. By filtering out unnecessary metrics early in the collection process, you can focus on the data that matters most to your operations while maintaining the visibility you need for effective network monitoring.

The filtering capability supports multiple dimensions including namespace-based filtering to focus on specific applications, pod and label-based filtering for targeted monitoring, and metric-specific filtering to collect only the types of metrics that are essential for your use case. This flexibility allows you to strike the right balance between comprehensive observability and cost-effective operations.

To learn more on how to enable container network metrics filtering, see [How to Configure Container Network Metrics Filtering ](how-to-configure-container-network-metrics-filtering).

### Limitations

- Pod-level metrics are available only on Linux.
- Cilium data plane is supported starting with Kubernetes version 1.29.
- Metric labels have subtle differences between Cilium and non-Cilium clusters.
- For Cilium based clusters, DNS metrics are only available for pods that have Cilium Network policies (CNP) configured on their clusters, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.
- Flow logs are not currently available in the air gapped cloud.
- Hubble relay may crash if one of the Hubble node agents goes down and may cause interruptions to Hubble CLI.
- When using Advanced Container Networking Services (ACNS) on non-Cilium data planes, FIPS support isn't available on Ubuntu 20.04 nodes due to kernel restrictions. To enable FIPS in this scenario, you must use an Azure Linux node pool. This limitation is expected to be resolved with the release of Ubuntu 22 FIPS. For updates, see the
[AKS issue tracker](https://github.com/Azure/AKS/issues/4857). - Container network metrics filtering is only available for Cilium Clusters.

Refer to the FIPS support matrix below:

| Operating System | FIPS Support |
|---|---|
| Azure Linux 3.0 | Yes |
| Azure Linux 2.0 | Yes |
| Ubuntu 20.04 | No |

This limitation does not apply when ACNS is running on Cilium data planes.

### Scale

The managed service for Prometheus in Azure Monitor and Azure Managed Grafana impose service-specific scale limitations. For more information, see [Scrape Prometheus metrics at scale in Azure Monitor](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-scale).

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- To create an AKS cluster by using Container Network Observability to capture metrics, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.
