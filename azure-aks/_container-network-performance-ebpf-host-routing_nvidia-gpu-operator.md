---
merged_at: 2026-01-25T12:06:27.699524
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

<!-- DOCUMENTO FUSIONADO: nvidia-gpu-operator.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/nvidia-gpu-operator -->

# Use NVIDIA GPU Operator on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The NVIDIA GPU Operator automates the management and deployment of all NVIDIA software components needed to provision GPU including driver installation, the [NVIDIA device plugin for Kubernetes](https://github.com/NVIDIA/k8s-device-plugin?tab=readme-ov-file), the NVIDIA container runtime, and more. Since the NVIDIA GPU Operator handles these components, it's not necessary to separately install the NVIDIA device plugin on your AKS cluster. This also means that the automatic GPU driver installation should be skipped in order to use the NVIDIA GPU Operator on AKS.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.72.2 or later installed to set the
`--gpu-driver`

field. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Note

GPU-enabled VMs contain specialized hardware subject to higher pricing and region availability. For more information, see the [pricing](free-standard-pricing-tiers) tool and [region availability](quotas-skus-regions).

## Limitations

- NVIDIA GPU Operator isn't supported for the following OS options: Windows Server versions,
[Flatcar Container Linux for AKS (preview)](flatcar-container-linux-for-aks), and[Azure Linux with OS Guard for AKS (preview)](use-azure-linux-os-guard).

## Get the credentials for your cluster

Get the credentials for your AKS cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. The following example command gets the credentials for the cluster

`myAKSCluster`

in the `myResourceGroup`

resource group:```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


Note

The NVIDIA GPU Operator is not compatible with multiple OS versions on the same AKS cluster.

Skip automatic GPU driver installation by creating an NVIDIA GPU-enabled node pool using the [

`az aks nodepool add`

][az-aks-nodepool-add] command and setting the API field`--gpu-driver`

to the value`none`

. Setting this API field to`none`

during node pool creation skips the default GPU driver installation, see[this example](gpu-cluster#skip-gpu-driver-installation). Any existing nodes aren't changed. You can scale the node pool to zero and then back up to make the change take effect.Follow the NVIDIA documentation to

[Install the GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/getting-started.html).Now that you successfully installed the GPU Operator, you can check that your

[GPUs are schedulable](gpu-cluster#confirm-that-gpus-are-schedulable)and[run a GPU workload](gpu-cluster#run-a-gpu-enabled-workload).

Note

There might be additional considerations to take when using the NVIDIA GPU Operator and deploying on SPOT instances. Please refer to [https://github.com/NVIDIA/gpu-operator/issues/577](https://github.com/NVIDIA/gpu-operator/issues/577)

## Next steps

[Monitor NVIDIA GPU metrics](monitor-gpu-metrics)using Azure Managed Prometheus and Azure Managed Grafana.- Learn more about
[Ray clusters on AKS](ray-overview).
