---
merged_at: 2026-01-25T12:25:33.930735
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: managed-identity-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/managed-identity-overview -->

# Overview of managed identities in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of system-assigned and user-assigned managed identities in AKS, including how they work, role assignments, and AKS-specific managed identity features.

To enable a managed identity on a new or existing AKS cluster, see [Use a managed identity in Azure Kubernetes Service (AKS)](use-managed-identity). For more information about managed identities in Azure, see the [Managed identities for Azure resources documentation](/en-us/entra/identity/managed-identities-azure-resources/).

Note

The system-assigned and user-assigned identity types differ from a [workload identity](workload-identity-overview), which is intended for use by an application running on a pod.

## AKS managed identity authorization flow

AKS clusters use system-assigned or user-assigned [managed identities](/en-us/entra/identity/managed-identities-azure-resources/overview) to request tokens from Microsoft Entra. These tokens help authorize access to other resources running in Azure. You assign an [Azure role-based access control (Azure RBAC)](/en-us/azure/role-based-access-control/overview) role to the managed identity to grant it permissions to a particular Azure resource. For example, you can grant permissions to a managed identity to access secrets in an Azure key vault for use by the cluster.

### Managed identity behavior in AKS

When you deploy an AKS cluster, a system-assigned managed identity is created for you by default. You can also create the cluster with a user-assigned managed identity, or update an existing cluster to a different type of managed identity.

If your cluster already uses a managed identity and you change the identity type (for example, from system-assigned to user-assigned), there's a delay while control plane components switch to the new identity. Control plane components continue to use the old identity until its token expires. After the token refreshes, they switch to the new identity. This process can take several hours.

Note

It's also possible to create a cluster with an application [service principal](kubernetes-service-principal) rather that a managed identity. However, we recommend using a managed identity over an application service principal for security and ease of use. If you have an existing cluster that uses an application service principal, you can update it to use a managed identity.

### AKS identity and credential management

The Azure platform manages both system-assigned and user-assigned managed identities and their credentials, so you can authorize access from your applications without needing to provision or rotate any secrets.

## System-assigned managed identity

The following table summarizes the key characteristics of a system-assigned managed identity in AKS:

| Creation | Lifecycle | Sharing across resources | Common use cases |
|---|---|---|---|
| Created as part of an Azure resource, such as an AKS cluster | Tied to the lifecycle of the parent resource, so it gets deleted when the parent resource is deleted | Can only be associated with a single resource | • Workloads contained within a single Azure resource • Workloads that require independent identities |

### User-assigned managed identity

The following table summarizes the key characteristics of a user-assigned managed identity in AKS:

| Creation | Lifecycle | Sharing across resources | Common use cases |
|---|---|---|---|
| Created as a standalone Azure resource, and must exist prior to cluster creation | Independent of the lifecycle of any specific resource, so it requires manual deletion if no longer needed | Can be shared across multiple resources | • Workloads that run on multiple resources and can share a single identity • Workloads that require preauthorization to a secure resource as part of a provisioning process • Workloads where resources are recycled frequently but need consistent permissions |

### Pre-created kubelet managed identity

A pre-created kubelet managed identity is an optional user-assigned identity that kubelet can use to access other resources in Azure. This feature enables scenarios such as connection to Azure Container Registry (ACR) during cluster creation. If you don't specify a user-assigned managed identity for kubelet, AKS creates a user-assigned kubelet identity in the node resource group. For a user-assigned kubelet identity outside the default worker node resource group, you need to assign the [Managed Identity Operator](/en-us/azure/role-based-access-control/built-in-roles#managed-identity-operator) role on the kubelet identity for control plane managed identity.

## Role assignments for managed identities in AKS

You can assign an Azure RBAC role to a managed identity to grant the cluster permissions on another Azure resource. Azure RBAC supports both built-in and custom role definitions that specify levels of permissions. To assign a role, see [Steps to assign an Azure role](/en-us/azure/role-based-access-control/role-assignments-steps).

When you assign an Azure RBAC role to a managed identity, you must define the scope for the role. In general, it's a best practice to limit the scope of a role to the minimum privileges required by the managed identity. For more information on scoping Azure RBAC roles, see [Understand scope for Azure RBAC](/en-us/azure/role-based-access-control/scope-overview).

### Control plane managed identity role assignments

When you create and use your own VNet, attached Azure disks, static IP address, route table, or user-assigned kubelet identity where the resources are outside of the worker node resource group, the Azure CLI adds the role assignment automatically. If you're using an ARM template or another method, use the principal ID of the managed identity to perform a role assignment.

If you're not using the Azure CLI, but you're using your own VNet, attached Azure disks, static IP address, route table, or user-assigned kubelet identity that's outside of the worker node resource group, we recommend using a [user-assigned managed identity for the control plane](use-managed-identity#create-a-user-assigned-managed-identity).

When the control plane uses a system-assigned managed identity, the identity is created at the same time as the cluster, so the role assignment can't be performed until after cluster creation.

## Summary of managed identities used by AKS

AKS uses several managed identities for built-in services and add-ons. The following table summarizes the managed identities used by AKS, their use cases, default permissions, and whether you can bring your own identity:

| Identity | Name | Use case | Default permissions | Bring your own identity |
|---|---|---|---|---|
| Control plane | AKS cluster name | Used by AKS control plane components to manage cluster resources including ingress load balancers and AKS-managed public IPs, Cluster Autoscaler, Azure Disk, File, Blob CSI drivers | Contributor role for Node resource group | Supported |
| Kubelet | AKS cluster name-agentpool | Authentication with Azure Container Registry (ACR) | N/A for Kubernetes version 1.15 and later | Supported |
| Add-on | AzureNPM | No identity required | N/A | Unsupported |
| Add-on | AzureCNI network monitoring | No identity required | N/A | Unsupported |
| Add-on | azure-policy (gatekeeper) | No identity required | N/A | Unsupported |
| Add-on | Calico | No identity required | N/A | Unsupported |
| Add-on | application-routing | Manages Azure DNS and Azure Key Vault certificates | Key Vault Secrets User role for Key Vault, DNS Zone Contributor role for DNS zones, Private DNS Zone Contributor role for private DNS zones | Unsupported |
| Add-on | HTTPApplicationRouting | Manages required network resources | Reader role for node resource group, contributor role for DNS zone | Unsupported |
| Add-on | Ingress application gateway | Manages required network resources | Contributor role for node resource group | Unsupported |
| Add-on | omsagent | Used to send AKS metrics to Azure Monitor | Monitoring Metrics Publisher role | Unsupported |
| Add-on | Virtual-Node (ACIConnector) | Manages required network resources for Azure Container Instances (ACI) | Contributor role for node resource group | Unsupported |
| Add-on | Cost analysis | Used to gather cost allocation data | N/A | Supported |
| Workload identity | Microsoft Entra Workload ID | Enables applications to access cloud resources securely with Microsoft Entra Workload ID | N/A | Unsupported |

## Next step: Enable managed identities in AKS

To learn how to enable managed identities on a new or existing AKS cluster, see [Use a managed identity in Azure Kubernetes Service (AKS)](use-managed-identity).


---

<!-- DOCUMENTO FUSIONADO: optimize-aks-costs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/optimize-aks-costs -->

# Optimize Azure Kubernetes Service (AKS) usage and costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides guidance on how to optimize your Azure Kubernetes Service (AKS) usage and costs. It covers guidance on the following topics:

## Automatic scaling

### Horizontal pod autoscaling

The * Horizontal Pod Autoscaler (HPA)* monitors resource demand and automatically updates a workload resource to automatically scale the number of pods to match demand. The response to increased load is to deploy more pods. If the load decreases and the number of pods is above the configured minimum, the autoscaler tells the workload resource to scale down.

The Metrics API gets data from the kubelet every 60 seconds, and the HPA checks the Metrics API every 15 seconds for any needed changes by default. This means that the HPA updates every 60 seconds. When you configure the HPA for a deployment, you define the minimum and maximum number of replicas that can run and the metrics that the HPA uses to determine when to scale.

For more information, see [Horizontal Pod Autoscaling](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) and [Autoscale pods in AKS](tutorial-kubernetes-scale#autoscale-pods).

### Kubernetes event-driven autoscaling

The [Kubernetes Event-driven Autoscaler (KEDA)](https://keda.sh/) applies event-driven autoscaling to your workloads. KEDA works with the HPA and can extend functionality without overwriting or duplication.

You can use the KEDA add-on for AKS to scale your applications and leverage a [rich catalog of Azure KEDA scalers](https://keda.sh/docs/2.16/scalers/). For more information, see [Application autoscaling with the KEDA add-on](keda-about) and [Install the KEDA add-on for AKS](keda-deploy-add-on-cli).

### Vertical pod autoscaling

The * Vertical Pod Autoscaler (VPA)* automatically sets resource requests and limits on containers per workload based on past usage. The VPA frees up CPU and Memory for pods to ensure effective utilization of your AKS clusters. Over time, the VPA provides recommendations for resource usage.

For more information, see [Vertical pod autoscaling in Azure Kubernetes Service (AKS)](vertical-pod-autoscaler) and [Use the Vertical Pod Autoscaler (VPA) in Azure Kubernetes Service (AKS)](use-vertical-pod-autoscaler).

## Cluster right-sizing

### Right-size your cluster

It's important to * right-size your clusters* to optimize costs and performance. You can manually resize a cluster by adding or removing the nodes to meet the needs of your applications. You can also autoscale your cluster to automatically adjust the number of nodes in response to changing demands.

For more information, see [Resize Azure Kubernetes Service (AKS) clusters](resize-cluster).

### Cluster autoscaling

With the * cluster autoscaler*, you can automatically scale node pools based on resource usage and constraints, such as scaling up to schedule pending pods or scaling down to reduce costs for unused nodes. The

[cluster autoscaler profile](cluster-autoscaler-overview#cluster-autoscaler-profile)is a set of parameters that you can fine-tune to control the behavior of the cluster autoscaler.

For more information, see [Cluster autoscaling in Azure Kubernetes Service (AKS) overview](cluster-autoscaler-overview) and [Use the cluster autoscaler in Azure Kubernetes Service (AKS)](cluster-autoscaler).

### Node autoprovisioning (preview)

* Node autoprovisioning (NAP)* (preview), based on the open-source

[Karpenter](https://karpenter.sh/)project, helps you provision the right infrastructure based on the pending pod resource requirements of your workloads. With efficient bin-packing, you can consolidate your workloads onto the right-sized infrastructure to reduce operating costs.

For more information, see [Node autoprovisioning (preview) in Azure Kubernetes Service (AKS)](node-autoprovision).

## GPU optimizations

### GPU partitioning and sharing

GPU partitioning helps combat underutilization by splitting up or sharing GPUs across multiple workloads. The following sections cover different ways to partition and share GPUs in AKS.

#### Time-slicing

The [NVIDIA GPU Operator](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/overview.html) enables the * time-slicing* of GPUs in Kubernetes clusters. With time-slicing, a system administrator can define a set of

*replicas*for a GPU, each of which can be handed out independently to a pod to run workloads on. You can apply cluster-wide default time-slicing configurations and node-specific configurations.


For more information, see [Time-slicing GPUs in Kubernetes](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-sharing.html).

#### Multi-processing service (MPS)

A single process might not utilize all the memory and compute bandwidth capacity available on a GPU. The * Multi-Process Service (MPS)* enables logical partitioning of memory and compute resources between workloads and allows kernel and memcopy operations from different processes to overlap on the GPU. MPS helps you achieve higher GPU utilization and shorter running times.


For more information, see [Multi-Process Service (MPS)](https://docs.nvidia.com/deploy/mps/index.html#mps).

#### Multi-instance GPUs (MIGs)

* Multi-instance GPUs (MIGs)* enable you to partition GPUs based on the NVIDIA Ampere and later architectures into separate and secure GPU instances for CUDA applications.


For more information, see [GPU Operator with MIG](https://docs.nvidia.com/datacenter/cloud-native/gpu-operator/latest/gpu-operator-mig.html) and [Create a multi-instance GPU node pool in Azure Kubernetes Service (AKS)](gpu-multi-instance).

## Multitenancy

Multitenancy refers to the sharing of infrastructure across tenants, teams, and business units. The following table outlines different ways to implement multitenancy in AKS:

| Multitenancy type | Multitenancy level | Cluster pod density | Cost allocation | Ideal use case | Potential risks |
|---|---|---|---|---|---|
Dedicated cluster |

• Lower pod density and more overprovisioned resources

**Dedicated node pool**• Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc.

**Dedicated namespace**• Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc.

### Dedicated cluster

With * dedicated cluster multitenancy*, clusters are dedicated to a single workload or team.


The following table outlines pros and cons of using a dedicated cluster:

| Pros | Cons |
|---|---|
| • Easier isolation method • Straightforward cost allocation and chargeback • Great for cases where tenants don't trust each other (often from security and resource sharing perspectives) |
• High management and financial overhead • Generally low pod density and overprovisioned resources |

### Dedicated node pool

With * dedicated node pool multitenancy*, clusters are shared by many tenants.


The following table outlines pros and cons of using a dedicated node pool:

| Pros | Cons |
|---|---|
| • Medium pod density • Some shared infrastructure • Apply Azure tags to node pools dedicated to a single tenant (tags propagate to nodes and persist through upgrades) |
• Requires trust between the tenants • Requires extra cluster configurations, like network policies, quota management, role-based access control (RBAC), etc. |

### Dedicated namespace

With * dedicated namespace multitenancy*, clusters are shared by many tenants, with namespaces serving as the isolation boundary.


The following table outlines pros and cons of using a dedicated namespace:

| Pros | Cons |
|---|---|
| • Higher pod density • Best binpacking • Sharing infrastructure to maximize resource utilization |
• Unsafe for hostile environments by default • Requires extra security measures in place if all tenants can't be trusted |

## Azure discounts

To take savings one step further, take advantage of Azure discounts such as Azure Savings Plans, Reserved Instances, and Azure Hybrid Benefits.

| Azure discount type | Details |
|---|---|
Azure Savings Plans |

• Save up to 65% compared to pay-as-you-go

• Flexible, with no SKU family or region restrictions

• Best for workloads with consistent costs with resources in various SKUs and regions

**Reserved Instances**• Save up to 72% compared to pay-as-you-go

• Restricted to specific SKU families and regions

• Best for stable workloads running continuously (with no unexpected SKU or region changes)

**Azure Hybrid Benefits**• Use any qualifying on-premises licenses that have an active Software Assurance (SA) or qualifying subscription

## Next steps

To learn more about cost in AKS, see the following articles:
