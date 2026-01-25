---
merged_at: 2026-01-25T12:25:33.838995
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: istio-latency.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-latency -->

# Latency comparison across versions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This document elaborates on the [data plane latency performance](istio-scale#data-plane-performance) across Istio add-on versions and Kubernetes version. The results evaluate the impact of adding sidecar proxies to the data path, showcasing the P90 and P99 latency difference. The comparison measures the difference between traffic routed through the sidecar and traffic sent directly to the pod.

- Traffic going through the sidecar: client --> client-sidecar --> server-sidecar --> server
- Traffic directly going to the pod: client --> server

## Test specifications

- Node SKU: Standard D16 v5 (16 vCPU, 64-GB memory)
- Two proxy workers
- 1-KB payload
- 1,000 Queries per second (QPS) at varying client connections
`http/1.1`

protocol and mutual Transport Layer Security (TLS) enabled

| P99 Latency Difference | P90 Latency Difference |
|---|---|
|


---

<!-- DOCUMENTO FUSIONADO: configure-azure-cni.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/configure-azure-cni -->

# Configure Azure CNI networking in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Container Networking Interface (CNI) networking in Azure to create and use a virtual network subnet for an Azure Kubernetes Service (AKS) cluster. For more information on network options and considerations, see [Networking concepts for applications in Azure Kubernetes Service](/en-us/azure/aks/concepts-network).

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Configure networking

For information on planning IP addresses, see [IP address planning for your Azure Kubernetes Service clusters](concepts-network-ip-address-planning).

Sign in to the

[Azure portal](https://portal.azure.com/).On the Azure portal home page, select

**Create a resource**.Under

**Categories**, select**Containers**>**Azure Kubernetes Service (AKS)**.On the

**Basics**tab, configure the following settings:- Under
**Project details**:**Subscription**: Select your Azure subscription.**Resource group**: Select**Create new**, enter a resource group name (such as**test-rg**), and then select**Ok**.

- Under
**Cluster details**:**Kubernetes cluster name**: Enter a cluster name, such as**aks-cluster**.**Region**: Select**East US 2**.


- Under
Select

**Next**>**Next**to get to the**Networking**tab.For

**Container networking**, select**Azure CNI Node Subnet**.Select

**Review + create**>**Create**.
