---
merged_at: 2026-01-26T20:54:26.148731
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___upgrade_nvidia-gpu-operator_node-auto-provisioning-node-pools__aks-virtual-ma_1854cd.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __upgrade_nvidia-gpu-operator_node-auto-provisioning-node-pools.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _upgrade_nvidia-gpu-operator.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: node-auto-provisioning-node-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-node-pools -->

# Configure node pools for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure node pools for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS), including SKU selectors, resource limits, and priority weights. It also provides examples to help you get started.

## Overview of node pools in NAP

NAP uses virtual machine (VM) SKU requirements to decide the best VMs for pending workloads. You can configure:

- SKU families and specific instance types.
- Resource limits and priorities.
- Spot or On-demand instances.
- Architecture and capabilities requirements.

The `NodePool`

resource sets constraints on the nodes that NAP creates and the pods that run on those nodes. When you first install NAP, it creates a [default NodePool](#review-default-node-pool-configuration). You can modify this node pool or create extra node pools to suit your workload requirements.

## Key behaviors of `NodePools`

in NAP

When configuring `NodePools`

for NAP, keep the following behaviors in mind:

- NAP requires at least one
`NodePool`

to function. - NAP evaluates each configured
`NodePool`

. - NAP skips
`NodePools`

with taints not tolerated by a pod. - NAP applies startup taints to provisioned nodes but doesn't require pod toleration.
- NAP works best with mutually exclusive
`NodePools`

. When multiple`NodePools`

match, it uses the one with highest weight.

## Review default node pool configuration

The configuration of the default [Karpenter NodePool](https://karpenter.sh/docs/concepts/nodepools/) named

`default`

created by NAP is as follows:```
apiVersion: karpenter.sh/v1
kind: NodePool
metadata:
name: default
spec:
disruption:
consolidationPolicy: WhenEmptyOrUnderutilized
template:
spec:
nodeClassRef:
name: default
expireAfter: Never
# Requirements that constrain the parameters of provisioned nodes.
# These requirements are combined with pod.spec.affinity.nodeAffinity rules.
# Operators { In, NotIn, Exists, DoesNotExist, Gt, and Lt } are supported.
# https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#operators
requirements:
- key: kubernetes.io/arch
operator: In
values:
- amd64
- key: kubernetes.io/os
operator: In
values:
- linux
- key: karpenter.sh/capacity-type
operator: In
values:
- on-demand
- key: karpenter.azure.com/sku-family
operator: In
values:
- D
```


It also creates a `system-surge`

node pool, which helps to autoscale system pool nodes.

## Control configuration of default node pool during cluster creation

When you [create a new AKS cluster enabled with NAP using the Azure CLI](use-node-auto-provisioning#enable-nap-on-a-new-cluster), you can include the `--node-provisioning-default-pools`

flag to control the configuration of the default NAP `NodePool`

.

The `--node-provisioning-default-pools`

flag controls the default NAP `NodePool`

configuration and accepts the following values:

(default): Creates two standard`Auto`

`NodePools`

for immediate use.: Doesn't create any`None`

`NodePools`

. You must define your own.

Warning

**Changing from Auto to None**: If you change the setting from


`Auto`

to `None`

on an existing cluster, the default `NodePools`

aren't deleted automatically. You must delete them manually if you no longer need them.## Node pool configuration options

The following sections outline various configuration options for `NodePools`

in NAP, including [well-known labels and SKU selectors](#well-known-labels-and-sku-selectors), [node pool limits](#node-pool-limits), and [node pool weights](#node-pool-weights).

### Well-known labels and SKU selectors

Kubernetes defines [well-known labels](https://kubernetes.io/docs/reference/labels-annotations-taints/) that Azure implements. You can define these labels in the `spec.requirements`

section of the `NodePool`

API. NAP also supports Azure-specific labels for more advanced scheduling.

`karpenter.azure.com`

SKU selectors

The following table lists the `karpenter.azure.com`

SKU selectors you can use in the `spec.requirements`

section of your `NodePool`

API to define VM characteristics for your nodes:

| Selector | Description | Example |
|---|---|---|
`karpenter.azure.com/sku-family` |
VM SKU family | D, F, L, etc. |
`karpenter.azure.com/sku-name` |
Explicit SKU name | Standard_A1_v2 |
`karpenter.azure.com/sku-version` |
SKU version (without "v", can use 1) | 1, 2 |
`karpenter.sh/capacity-type` |
VM allocation type (Spot / On-demand) | Spot |
`karpenter.azure.com/sku-cpu` |
Number of CPUs in VM | 16 |
`karpenter.azure.com/sku-memory` |
Memory in VM in MiB | 131072 |
`kubernetes.azure.com/sku-cpu` |
Number of CPUs in VM | 16 |
`kubernetes.azure.com/sku-memory` |
Memory in VM in MiB | 131072 |
`karpenter.azure.com/sku-gpu-name` |
GPU name | A100 |
`karpenter.azure.com/sku-gpu-manufacturer` |
GPU manufacturer | nvidia |
`karpenter.azure.com/sku-gpu-count` |
GPU count per VM | 2 |
`karpenter.azure.com/sku-networking-accelerated` |
Whether the VM has accelerated networking | [true, false] |
`karpenter.azure.com/sku-storage-premium-capable` |
Whether the VM supports Premium IO storage | [true, false] |
`karpenter.azure.com/sku-storage-ephemeralos-maxsize` |
Size limit for the Ephemeral operating system (OS) disk in Gb | 92 |

`kubernetes.io`

well-known labels

The following table lists the `kubernetes.io`

well-known labels you can use in the `spec.requirements`

section of your `NodePool`

API to define node characteristics for your nodes:

| Label | Description | Example |
|---|---|---|
`topology.kubernetes.io/zone` |
Availability zone(s) | [uksouth-1,uksouth-2,uksouth-3] |
`kubernetes.io/os` |
Operating system | linux |
`kubernetes.io/arch` |
CPU architecture (AMD64 or ARM64) | [amd64, arm64] |

#### SKU family examples

The `karpenter.azure.com/sku-family`

selector allows you to target specific VM families.

| Family | Description |
|---|---|
| D-series | General-purpose VMs with balanced CPU-to-memory ratio |
| F-series | Compute-optimized VMs with high CPU-to-memory ratio |
| E-series | Memory-optimized VMs for memory-intensive applications |
| L-series | Storage-optimized VMs with high disk throughput |
| N-series | GPU-enabled VMs for compute-intensive workloads |

Example configuration using SKU family:

```
requirements:
- key: karpenter.azure.com/sku-family
operator: In
values:
- D
- F
```


#### SKU name examples

The `karpenter.azure.com/sku-name`

selector allows you to specify the exact VM instance type.

```
requirements:
- key: karpenter.azure.com/sku-name
operator: In
values:
- Standard_D4s_v3
- Standard_F8s_v2
```


#### SKU version examples

The `karpenter.azure.com/sku-version`

selector targets specific generations of VM SKUs.

```
requirements:
- key: karpenter.azure.com/sku-version
operator: In
values:
- "3" # v3 generation
- "5" # v5 generation
```


#### Availability zone example

The `topology.kubernetes.io/zone`

selector allows you to specify the availability zones for your nodes.

```
requirements:
- key: topology.kubernetes.io/zone
operator: In
values:
- eastus-1
- eastus-2
```


Note

You can find available zones for your region using the `az account list-locations --output table`

Azure CLI command.

#### Architecture example

The `kubernetes.io/arch`

selector allows you to specify the CPU architecture for your nodes. NAP supports both `amd64`

and `arm64`

nodes.

```
requirements:
- key: kubernetes.io/arch
operator: In
values:
- amd64
- arm64
```


#### OS example

The `kubernetes.io/os`

selector allows you to specify the operating system for your nodes.

```
requirements:
- key: kubernetes.io/os
operator: In
values:
- linux
```


#### Capacity type example

The `karpenter.sh/capacity-type`

selector allows you to specify whether to use Spot or On-demand instances.

Note

NAP prioritizes Spot instances when both Spot and On-demand are specified.

```
requirements:
- key: karpenter.sh/capacity-type
operator: In
values:
- spot
- on-demand
```


### Node pool limits

By default, NAP attempts to schedule your workloads within the Azure quota you have available. You can also specify the upper limit of resources that a node pool uses by specifying limits within the node pool spec. For example:

```
spec:
# Resource limits constrain the total size of the cluster.
# Limits prevent Node Auto Provisioning from creating new instances once the limit is exceeded.
limits:
cpu: "1000"
memory: 1000Gi
```


### Node pool weights

When you have multiple node pools defined, you can set a preference of where a workload should be scheduled by defining the relative weight in your node pool definitions. For example:

```
spec:
# Priority given to the node pool when the scheduler considers which to select.
# Higher weights indicate higher priority when comparing node pools.
# Specifying no weight is equivalent to specifying a weight of 0.
weight: 10
```


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: _aks-virtual-machine-sizes_devops-pipeline.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: aks-virtual-machine-sizes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-virtual-machine-sizes -->

# Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) supports various virtual machine (VM) sizes, generations, and features to accommodate different workloads and performance requirements. This article provides an overview of available VM sizes and generations for AKS, how to check for available VM sizes in your region, reasons why certain VM sizes might not be available, and what happens when a VM size retires.

## VM support on AKS

Azure supports both Generation 1 (Gen 1) and [Generation 2 (Gen 2) virtual machines (VMs)](/en-us/azure/virtual-machines/generation-2). With some [exceptions](/en-us/windows-server/virtualization/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v), we generally recommend [migrating to Generation 2 VMs](#gen-2-vms-on-aks) to take advantage of the newest features and functionalities in Azure VMs.

The VM size and operating system (OS) you select when creating an AKS node pool determines the VM generation and [node image](node-images) used. Check the [list of supported sizes](/en-us/azure/virtual-machines/generation-2#generation-2-vm-sizes) to see if your SKU supports or requires Gen 2.

### Limitations

There are some limitations to take into account when choosing a VM generation and/or OS:

- Trusted Launch can only be enabled on VM sizes that support Gen 2.
- Confidential VM sizes always use Gen 2 on AKS.
- Arm64 VM sizes always use Gen 2 on AKS.
- Windows Server 2019 node pools don't support Gen 2 VM sizes.
- Windows Server 2022 node pools require use of a custom header to use Gen 2.

To use Gen 2 VMs on AKS, see [Use Gen 2 VMs](#gen-2-vms-on-aks).

## Available VM features

AKS supports various VM features that enhance security, performance, and functionality. Some key features include:

uses pending pod resource requirements to decide the optimal VM configuration to run your workloads efficiently and cost-effectively.**Node autoprovisioning (NAP)**provide a better experience for dynamic workloads and high availability requirements. Virtual Machines node pools enable you to set up multiple similar-family VMs in a single node pool. Your workloads are automatically scheduled on the available resources you configure.**Virtual Machines node pools**

## Supported VM sizes

For in-depth information about VM sizes available in Azure, see [Azure VM sizes](/en-us/azure/virtual-machines/sizes/overview?tabs=breakdownseries%2Cgeneralsizelist%2Ccomputesizelist%2Cmemorysizelist%2Cstoragesizelist%2Cgpusizelist%2Cfpgasizelist%2Chpcsizelist). To view supported Gen 2 VM sizes, see [Generation 2 VM sizes](/en-us/azure/virtual-machines/generation-2).

AKS also supports the following VM types and features:

[Confidential VMs (CVMs)](use-cvm)[Arm-based processor (Arm64) VMs](use-arm64-vms)[GPU-optimized VMs](/en-us/azure/virtual-machines/sizes/overview?tabs=breakdownseries%2Cgeneralsizelist%2Ccomputesizelist%2Cmemorysizelist%2Cstoragesizelist%2Cgpusizelist%2Cfpgasizelist%2Chpcsizelist#gpu-accelerated)[Trusted Launch](use-trusted-launch)[Federal Information Process Standard (FIPS)](enable-fips-nodes)

### Default behavior for supported VM sizes

There are three scenarios when creating a node pool with a supported VM size:

- If the VM size supports only Gen 1, the default behavior for both Linux and Windows node pools is to use the Gen 1 node image.
- If the VM size supports only Gen 2, the default behavior for both Linux and Windows node pools is to use the Gen 2 node image. Windows Server 2022 node pools require a custom header to use a VM size that only supports Gen 2. For more information, see
[Create a Windows node pool with a Gen 2 VM](generation-2-vms#create-a-node-pool-with-a-gen-2-vm). - If the VM size supports both Gen 1 and Gen 2, the default behavior for both Linux and Windows (in Windows Server 2025+) nodes pools is to use the Gen 2 node image. To use the Gen 2 node image for Windows Server 2022, see
[Create a Windows node pool with a Gen 2 VM](generation-2-vms#create-a-node-pool-with-a-gen-2-vm).

## Check available VM sizes

Check available VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
az vm list-skus --location <your-location> --output table
```


## Why certain VM sizes might not be available

There are several reasons why certain VM sizes might not be available, including:

**Quota limits**: All Azure services set default limits and quotas for resources and features. For more information, see the following resources:[Quotas and regional limits for Azure Kubernetes Service (AKS)](quotas-skus-regions)[Check your quota usage](/en-us/azure/virtual-machines/quotas)[Request a quota increase through an Azure support request](https://portal.azure.com/#blade/Microsoft_Azure_Support/HelpAndSupportBlade/newsupportrequest)(for**Issue type**, select**Quota**)

Note

- For
, VM sizes with**user node pools***fewer than two vCPUs and two GBs of memory (RAM)*might not be used by default. - For
, VM sizes with**system node pools***fewer than two vCPUs and four GBs of memory (RAM)*might not be used by default. To ensure that you can reliably schedule the required`kube-system`

pods and your applications, we recommend that you**do not use any**.[B series VMs](/en-us/azure/virtual-machines/sizes/general-purpose/bv1-series)or[Av1 series VMs](/en-us/azure/virtual-machines/sizes/retirement/av1-series-retirement)

**VM sizes in preview**: VM sizes in preview might not be available to you if you haven't registered the preview flag for the VM size.**Blocked by AKS**: Some VM sizes might not be available by default in AKS. These sizes might require extra testing or validation to ensure compatibility with AKS. If you need a specific VM size that isn't available to you, you can[submit a GitHub issue request](https://github.com/Azure/AKS/issues).

Make sure you understand which features your workloads need and choose a VM size that meets those requirements. Later VM versions typically have better performance and improved features. For example, [Gen 2 VMs](#gen-2-vms-on-aks) have increased security and performance benefits over Gen 1 VMs.

## What happens when a VM size retires?

When a VM size or series reaches its retirement date, the VM is deallocated. VM deallocation causes your AKS node pools to break. To check the retirement status of a VM size, see [Retired Azure VM size series](/en-us/azure/virtual-machines/sizes/retirement/retired-sizes-list) or perform a search in [Azure Updates](https://azure.microsoft.com/updates). To check the VM size of your node pools, use the [`az aks nodepool list`

][az-aks-nodepool-list] command and query for the `vmSize`

property:

```
az aks nodepool list --resource-group <your-resource-group> --cluster-name <your-cluster-name> --query "[].{Name:name, VMSize:vmSize}" --output table
```


If you're using a VM size that's retiring/retired, we recommend [migrating your node pools to a supported VM size](#migrate-node-pools-to-a-supported-vm-size) to prevent any potential disruption to your service. Currently, AKS *doesn't support* transitioning to a new VM size within the same node pool.

## Migrate node pools to a supported VM size

Once you determine the appropriate node pools to take action on, you can [resize your node pools](resize-node-pool). During the resizing process, a new node pool is created and workloads are migrated to the new node pool.

For more information on migrating to a new VM size, see the following resources:

[Migrate from Gen 1 to Gen 2 VMs](#gen-2-vms-on-aks)[General-purpose sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/d-ds-dv2-dsv2-ls-series-migration-guide)[Storage-optimized sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/d-ds-dv2-dsv2-ls-series-migration-guide)[GPU-accelerated sizes migration guide](/en-us/azure/virtual-machines/migration/sizes/n-series-migration)[Azure Dedicated Host SKU migration guide](/en-us/azure/virtual-machines/migration/dedicated-host-migration-guide)

## Gen 2 VMs on AKS

Gen 2 VMs are generally Azure's newer offerings and have exclusive features over Gen 1 VMs like increased memory, improved CPU performance, support for NVMe disks, and support for [Trusted Launch](use-trusted-launch).

While we generally recommend running Gen 2 VMs, you should make sure that the generation you choose supports your requirements. To learn more about the differences between generations, and when one might make more sense than the other, see [Should I create a Gen 1 or 2 VM in Hyper-V?](/en-us/windows-server/virtualization/hyper-v/plan/should-i-create-a-generation-1-or-2-virtual-machine-in-hyper-v)

To use Gen 2 VMs on AKS, see [Use generation 2 VMs on AKS](generation-2-vms).

## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)


---

<!-- DOCUMENTO FUSIONADO: devops-pipeline.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/devops-pipeline -->

# Build and deploy to Azure Kubernetes Service with Azure Pipelines

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Azure DevOps Services**

Use [Azure Pipelines](/en-us/azure/devops/pipelines/) to automatically deploy to Azure Kubernetes Service (AKS). Azure Pipelines lets you build, test, and deploy with continuous integration (CI) and continuous delivery (CD) using [Azure DevOps](/en-us/azure/devops/).

In this article, you'll learn how to create a pipeline that continuously builds and deploys your app. Every time you change your code in a repository that contains a Dockerfile, the images are pushed to your Azure Container Registry, and the manifests are then deployed to your AKS cluster.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - An Azure Resource Manager service connection.
[Create an Azure Resource Manager service connection](/en-us/azure/devops/pipelines/library/connect-to-azure#create-an-azure-resource-manager-service-connection-using-automated-security). - A GitHub account. Create a free
[GitHub account](https://github.com/join)if you don't have one already.

## Get the code

Fork the following repository containing a sample application and a Dockerfile:

```
https://github.com/MicrosoftDocs/pipelines-javascript-docker
```


## Create the Azure resources

Sign in to the [Azure portal](https://portal.azure.com/), and then select the [Cloud Shell](/en-us/azure/cloud-shell/overview) button in the upper-right corner. Use Azure CLI or PowerShell to create an AKS cluster.

### Create a container registry

```
# Create a resource group
az group create --name myapp-rg --location eastus
# Create a container registry
az acr create --resource-group myapp-rg --name mycontainerregistry --sku Basic
# Create a Kubernetes cluster
az aks create \
--resource-group myapp-rg \
--name myapp \
--node-count 1 \
--enable-addons monitoring \
--generate-ssh-keys
```


## Sign in to Azure Pipelines

Sign in to [Azure Pipelines](https://azure.microsoft.com/services/devops/pipelines). After you sign in, your browser goes to `https://dev.azure.com/my-organization-name`

and displays your Azure DevOps dashboard.

Within your selected organization, create a *project*. If you don't have any projects in your organization, you see a **Create a project to get started** screen. Otherwise, select the **Create Project** button in the upper-right corner of the dashboard.

## Create the pipeline

### Connect and select your repository

Sign in to your Azure DevOps organization and go to your project.

Go to

**Pipelines**, and then select**New pipeline**.Do the steps of the wizard by first selecting

**GitHub**as the location of your source code.You might be redirected to GitHub to sign in. If so, enter your GitHub credentials.

When you see the list of repositories, select your repository.

You might be redirected to GitHub to install the Azure Pipelines app. If so, select

**Approve & install**.Select

**Deploy to Azure Kubernetes Service**.If you're prompted, select the subscription in which you created your registry and cluster.

Select the

`myapp`

cluster.For

**Namespace**, select**Existing**, and then select**default**.Select the name of your container registry.

You can leave the image name set to the default.

Set the service port to 8080.

Set the

**Enable Review App for Pull Requests**checkbox for[review app](/en-us/azure/devops/pipelines/process/environments-kubernetes)related configuration to be included in the pipeline YAML autogenerated in subsequent steps.Select

**Validate and configure**.As Azure Pipelines creates your pipeline, the process will:

Create a

*Docker registry service connection*to enable your pipeline to push images into your container registry.Create an

*environment*and a Kubernetes resource within the environment. For an RBAC-enabled cluster, the created Kubernetes resource implicitly creates ServiceAccount and RoleBinding objects in the cluster so that the created ServiceAccount can't perform operations outside the chosen namespace.Generate an

*azure-pipelines.yml*file, which defines your pipeline.Generate Kubernetes manifest files. These files are generated by hydrating the

[deployment.yml](https://github.com/Microsoft/azure-pipelines-yaml/blob/master/templates/resources/k8s/deployment.yml)and[service.yml](https://github.com/Microsoft/azure-pipelines-yaml/blob/master/templates/resources/k8s/service.yml)templates based on selections you made. When you're ready, select**Save and run**.

Select

**Save and run**.You can change the

**Commit message**to something like*Add pipeline to our repository*. When you're ready, select**Save and run**to commit the new pipeline into your repo, and then begin the first run of your new pipeline!

## See your app deploy

As your pipeline runs, watch as your build stage, and then your deployment stage, go from blue (running) to green (completed). You can select the stages and jobs to watch your pipeline in action.

Note

If you're using a Microsoft-hosted agent, you must add the IP range of the Microsoft-hosted agent to your firewall. Get the weekly list of IP ranges from the [weekly JSON file](https://www.microsoft.com/download/details.aspx?id=56519), which is published every Wednesday. The new IP ranges become effective the following Monday. For more information, see [Microsoft-hosted agents](/en-us/azure/devops/pipelines/agents/hosted?tabs=yaml&view=azure-devops&preserve-view=true#networking).
To find the IP ranges that are required for your Azure DevOps organization, learn how to [identify the possible IP ranges for Microsoft-hosted agents](/en-us/azure/devops/pipelines/agents/hosted?tabs=yaml&view=azure-devops&preserve-view=true#to-identify-the-possible-ip-ranges-for-microsoft-hosted-agents).

After the pipeline run is finished, explore what happened and then go see your app deployed. From the pipeline summary:

Select the

**Environments**tab.Select

**View environment**.Select the instance of your app for the namespace you deployed to. If you used the defaults, then it is the

**myapp**app in the**default**namespace.Select the

**Services**tab.Select and copy the external IP address to your clipboard.

Open a new browser tab or window and enter <IP address>:8080.


If you're building our sample app, then *Hello world* appears in your browser.

## How the pipeline builds

When you finished selecting options and then proceeded to validate and configure the pipeline Azure Pipelines created a pipeline for you, using the *Deploy to Azure Kubernetes Service* template.

The build stage uses the [Docker task](/en-us/azure/devops/pipelines/tasks/build/docker) to build and push the image to the Azure Container Registry.

```
- stage: Build
displayName: Build stage
jobs:
- job: Build
displayName: Build job
pool:
vmImage: $(vmImageName)
steps:
- task: Docker@2
displayName: Build and push an image to container registry
inputs:
command: buildAndPush
repository: $(imageRepository)
dockerfile: $(dockerfilePath)
containerRegistry: $(dockerRegistryServiceConnection)
tags: |
$(tag)
- task: PublishPipelineArtifact@1
inputs:
artifactName: 'manifests'
path: 'manifests'
```


The deployment job uses the *Kubernetes manifest task* to create the `imagePullSecret`

required by Kubernetes cluster nodes to pull from the Azure Container Registry resource. Manifest files are then used by the Kubernetes manifest task to deploy to the Kubernetes cluster. The manifest files, `service.yml`

and `deployment.yml`

, were generated when you used the **Deploy to Azure Kubernetes Service** template.

```
- stage: Deploy
displayName: Deploy stage
dependsOn: Build
jobs:
- deployment: Deploy
displayName: Deploy job
pool:
vmImage: $(vmImageName)
environment: 'myenv.aksnamespace' #customize with your environment
strategy:
runOnce:
deploy:
steps:
- task: DownloadPipelineArtifact@2
inputs:
artifactName: 'manifests'
downloadPath: '$(System.ArtifactsDirectory)/manifests'
- task: KubernetesManifest@1
displayName: Create imagePullSecret
inputs:
action: 'createSecret'
connectionType: 'kubernetesServiceConnection'
kubernetesServiceConnection: 'myapp-default' #customize for your Kubernetes service connection
secretType: 'dockerRegistry'
secretName: '$(imagePullSecret)'
dockerRegistryEndpoint: '$(dockerRegistryServiceConnection)'
- task: KubernetesManifest@1
displayName: Deploy to Kubernetes cluster
inputs:
action: 'deploy'
connectionType: 'kubernetesServiceConnection'
kubernetesServiceConnection: 'myapp-default' #customize for your Kubernetes service connection
manifests: |
$(Pipeline.Workspace)/manifests/deployment.yml
$(Pipeline.Workspace)/manifests/service.yml
containers: '$(containerRegistry)/$(imageRepository):$(tag)'
imagePullSecrets: '$(imagePullSecret)'
```


## Clean up resources

Whenever you're done with the resources you created, you can use the following command to delete them:

```
az group delete --name myapp-rg
```


Enter `y`

when you're prompted.


---

<!-- DOCUMENTO FUSIONADO: _private-clusters__operator-best-practices-cluster-security_node-updates-kured.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: private-clusters.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/private-clusters -->

# Create a private Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article helps you deploy a private link-based AKS cluster. If you're interested in creating an AKS cluster without required private link or tunnel, see [Create an Azure Kubernetes Service (AKS) cluster with API Server VNet integration](api-server-vnet-integration).

## Overview of private clusters in AKS

In a private cluster, the control plane or API server has internal IP addresses that are defined in the [RFC1918 - Address Allocation for Private Internet](https://tools.ietf.org/html/rfc1918) document. By using a private cluster, you can ensure network traffic between your API server and your node pools remains only on the private network.

The control plane or API server is in an AKS-managed Azure resource group, and your cluster or node pool is in your resource group. The server and the cluster or node pool can communicate with each other through the [Azure Private Link service](/en-us/azure/private-link/private-link-service-overview#limitations) in the API server virtual network and a private endpoint exposed on the subnet of your AKS cluster.

When you create a private AKS cluster, AKS creates both private and public fully qualified domain names (FQDNs) with corresponding DNS zones by default. For detailed DNS configuration options, see [Configure a private DNS zone, private DNS subzone, or custom subdomain](#configure-a-private-dns-zone-private-dns-subzone-or-custom-subdomain-for-a-private-aks-cluster).

## Region availability

Private clusters are available in public regions, Azure Government, and Microsoft Azure operated by 21Vianet regions where [AKS is supported](https://azure.microsoft.com/global-infrastructure/services/?products=kubernetes-service).

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on August 18, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see [Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).

Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.

## Prerequisites for private AKS clusters

- The Azure CLI version 2.28.0 or higher. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If using Azure Resource Manager (ARM) or the Azure REST API, the AKS API version must be
*2021-05-01 or higher*. - To use a custom DNS server, add the Azure public IP address
*168.63.129.16*as the upstream DNS server in the custom DNS server, and make sure to add this public IP address as the*first*DNS server. For more information about the Azure IP address, see[What is IP address 168.63.129.16?](/en-us/azure/virtual-network/what-is-ip-address-168-63-129-16)- The cluster's DNS zone should be what you forward to
*168.63.129.16*. You can find more information on zone names in[Azure services DNS zone configuration](/en-us/azure/private-link/private-endpoint-dns#azure-services-dns-zone-configuration).

- The cluster's DNS zone should be what you forward to
- Existing AKS clusters enabled with API Server VNet integration can have private cluster mode enabled. For more information, see
[Enable or disable private cluster mode on an existing cluster with API Server VNet integration](api-server-vnet-integration#enable-or-disable-private-cluster-mode-on-an-existing-cluster-with-api-server-vnet-integration).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Limitations and considerations for private AKS clusters

- You can't apply IP authorized ranges to the private API server endpoint - they only apply to the public API server.
[Azure Private Link service limitations](/en-us/azure/private-link/private-link-service-overview#limitations)apply to private clusters.- There's no support for Azure DevOps Microsoft-hosted Agents with private clusters. Consider using
[self-hosted agents](/en-us/azure/devops/pipelines/agents/agents). - If you need to enable Azure Container Registry on a private AKS cluster,
[set up a private link for the container registry in the cluster virtual network (VNet)](/en-us/azure/container-registry/container-registry-private-link)or set up peering between the container registry's virtual network and the private cluster's virtual network. - Deleting or modifying the private endpoint in the customer subnet causes the cluster to stop functioning.
- Azure Private Link service is supported on Standard Azure Load Balancer only. Basic Azure Load Balancer isn't supported.

## Hub and spoke with custom DNS for private AKS clusters

[Hub and spoke architectures](/en-us/azure/architecture/reference-architectures/hybrid-networking/hub-spoke) are commonly used to deploy networks in Azure. In many of these deployments, DNS settings in the spoke VNets are configured to reference a central DNS forwarder to allow for on-premises and Azure-based DNS resolution.

Keep the following considerations in mind when deploying private AKS clusters in hub and spoke architectures with custom DNS:

When a private cluster is created, a private endpoint (1) and a private DNS zone (2) are created in the cluster-managed resource group by default. The cluster uses an

`A`

record in the private zone to resolve the IP of the private endpoint for communication to the API server.The private DNS zone is linked only to the VNet that the cluster nodes are attached to (3), which means that the private endpoint can only be resolved by hosts in that linked VNet. In scenarios where no custom DNS is configured on the VNet (default), it works without issue as hosts point at

*168.63.129.16*for DNS that can resolve records in the private DNS zone because of the link.If you keep the default private DNS zone behavior, AKS tries to link the zone directly to the spoke VNet that hosts the cluster even when the zone is already linked to a hub VNet.

In spoke VNets that use custom DNS servers, this action can fail if the cluster's managed identity lacks

**Network Contributor**on the spoke VNet.To prevent the failure, choose

**one**of the following supported configurations:**Custom private DNS zone**: Provide a precreated private zone and set`privateDNSZone`

/`--private-dns-zone`

to its resource ID. Link that zone to the appropriate VNet (for example, the hub VNet) and set`publicDNS`

to`false`

/ use`--disable-public-fqdn`

.**Public DNS only**: Disable private zone creation by setting`privateDNSZone`

/`--private-dns-zone`

to`none`

**and**leave`publicDNS`

at its default value (`true`

) / don't use`--disable-public-fqdn`

.

If you're using

[bring your own (BYO) route table with kubenet](configure-kubenet#bring-your-own-subnet-and-route-table-with-kubenet)and BYO DNS with private clusters, cluster creation fails. You need to associate thein the node resource group to the subnet after the cluster creation failed to make the creation successful.`RouteTable`


Keep the following limitations in mind when using custom DNS with private AKS clusters:

- Setting
`privateDNSZone`

/`--private-dns-zone`

to`none`

**and**`publicDNS: false`

/`--disable-public-fqdn`

at the same time**isn't supported**. - Conditional forwarding doesn't support subdomains.

## Create a private AKS cluster with default basic networking

Create a resource group using the

command. You can also use an existing resource group for your AKS cluster.`az group create`

`az group create \ --name <private-cluster-resource-group> \ --location <location>`

Create a private cluster with default basic networking using the

command with the`az aks create`

`--enable-private-cluster`

flag.**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.

`az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --generate-ssh-keys`


## Create a private AKS cluster with advanced networking

Create a resource group using the

command. You can also use an existing resource group for your AKS cluster.`az group create`

`az group create \ --name <private-cluster-resource-group> \ --location <location>`

Create a private cluster with advanced networking using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--network-plugin azure`

: Specifies the Azure CNI networking plugin.`--vnet-subnet-id`

: The resource ID of an existing subnet in a virtual network.`--dns-service-ip`

: An available IP address within the Kubernetes service address range to use for the cluster DNS service.`--service-cidr`

: A CIDR notation IP range from which to assign service cluster IPs.

`az aks create \ --resource-group <private-cluster-resource-group> \ --name <private-cluster-name> \ --load-balancer-sku standard \ --enable-private-cluster \ --network-plugin azure \ --vnet-subnet-id <subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 --generate-ssh-keys`


## Use custom domains with private AKS clusters

If you want to configure custom domains that can only be resolved internally, see [Use custom domains](coredns-custom#use-custom-domains).

## Disable a public FQDN on a private AKS cluster

### Disable a public FQDN on a new cluster

Disable a public FQDN when creating a private AKS cluster using the

command with the`az aks create`

`--disable-public-fqdn`

flag.`az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone <private-dns-zone-mode> \ --disable-public-fqdn \ --generate-ssh-keys`


### Disable a public FQDN on an existing cluster

Disable a public FQDN on an existing AKS cluster using the

command with the`az aks update`

`--disable-public-fqdn`

flag.`az aks update \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --disable-public-fqdn`


## Configure a private DNS zone, private DNS subzone, or custom subdomain for a private AKS cluster

You can configure private DNS settings for a private AKS cluster using the Azure CLI (with the `--private-dns-zone`

parameter) or an Azure Resource Manager (ARM) template (with the `privateDNSZone`

property). The following table outlines the options available for the `--private-dns-zone`

parameter / `privateDNSZone`

property:

| Setting | Description |
|---|---|
`system` |
The default value when configuring a private DNS zone. If you omit `--private-dns-zone` / `privateDNSZone` , AKS creates a private DNS zone in the node resource group. |
`none` |
If you set `--private-dns-zone` / `privateDNSZone` to `none` , AKS doesn't create a private DNS zone. |
`<custom-private-dns-zone-resource-id>` |
To use this parameter, you need to create a private DNS zone in the following format for Azure global cloud: `privatelink.<region>.azmk8s.io` or `<subzone>.privatelink.<region>.azmk8s.io` . You need the resource ID of the private DNS zone for future use. You also need a user-assigned identity or service principal with the
`private.<region>.azmk8s.io` or `<subzone>.private.<region>.azmk8s.io` . You can't change or delete this resource after creating the cluster, as it can cause performance issues and cluster upgrade failures. You can use `--fqdn-subdomain <subdomain>` with `<custom-private-dns-zone-resource-id>` only to provide subdomain capabilities to `privatelink.<region>.azmk8s.io` . If you're specifying a subzone, there's a 32 character limit for the `<subzone>` name. |

Keep the following considerations in mind when configuring private DNS for a private AKS cluster:

- If the private DNS zone is in a different subscription than the AKS cluster, you need to register the
`Microsoft.ContainerServices`

Azure provider in both subscriptions. - If your AKS cluster is configured with an Active Directory service principal, AKS doesn't support using a system-assigned managed identity with custom private DNS zone. The cluster must use
[user-assigned managed identity authentication](use-managed-identity).

## Create a private AKS cluster with a private DNS zone

Create a private AKS cluster with a private DNS zone using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--private-dns-zone [system|none]`

: Configures the private DNS zone for the cluster. The default value is`system`

.`--assign-identity <resource-id>`

: The resource ID of a user-assigned managed identity with the[Private DNS Zone Contributor](/en-us/azure/role-based-access-control/built-in-roles#dns-zone-contributor)and[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)roles.

`az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone [system|none] \ --generate-ssh-keys`


## Create a private AKS cluster with a custom private DNS zone or private DNS subzone

Create a private AKS cluster with a custom private DNS zone or subzone using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--private-dns-zone <custom-private-dns-zone-resource-id>|<custom-private-dns-subzone-resource-id>`

: The resource ID of a precreated private DNS zone or subzone in the following format for Azure global cloud:`privatelink.<region>.azmk8s.io`

or`<subzone>.privatelink.<region>.azmk8s.io`

.`--assign-identity <resource-id>`

: The resource ID of a user-assigned managed identity with the[Private DNS Zone Contributor](/en-us/azure/role-based-access-control/built-in-roles#dns-zone-contributor)and[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)roles.

`# The custom private DNS zone name should be in the following format: "<subzone>.privatelink.<region>.azmk8s.io" az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone [<custom-private-dns-zone-resource-id>|<custom-private-dns-subzone-resource-id>] \ --generate-ssh-keys`


## Create a private AKS cluster with a custom private DNS zone and custom subdomain

Create a private AKS cluster with a custom private DNS zone and subdomain using the

command.`az aks create`

**Key parameters in this command**:`--enable-private-cluster`

: Enables private cluster mode.`--private-dns-zone <custom-private-dns-zone-resource-id>`

: The resource ID of a precreated private DNS zone in the following format for Azure global cloud:`privatelink.<region>.azmk8s.io`

.`--fqdn-subdomain <subdomain>`

: The subdomain to use for the cluster FQDN within the custom private DNS zone.`--assign-identity <resource-id>`

: The resource ID of a user-assigned managed identity with the[Private DNS Zone Contributor](/en-us/azure/role-based-access-control/built-in-roles#dns-zone-contributor)and[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)roles.

`# The custom private DNS zone name should be in one of the following formats: "privatelink.<region>.azmk8s.io" or "<subzone>.privatelink.<region>.azmk8s.io" az aks create \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --load-balancer-sku standard \ --enable-private-cluster \ --assign-identity <resource-id> \ --private-dns-zone <custom-private-dns-zone-resource-id> \ --fqdn-subdomain <subdomain> \ --generate-ssh-keys`


## Update an existing private AKS cluster from a private DNS zone to public

You can only update from `byo`

(bring your own) or `system`

to `none`

. No other combination of update values is supported.

Warning

When you update a private cluster from `byo`

or `system`

to `none`

, the agent nodes change to use a public FQDN. In an AKS cluster that uses Azure Virtual Machine Scale Sets, a [node image upgrade](node-image-upgrade) is performed to update your nodes with the public FQDN.

Update a private cluster from

`byo`

or`system`

to`none`

using thecommand with the`az aks update`

`--private-dns-zone`

parameter set to`none`

.`az aks update \ --name <private-cluster-name> \ --resource-group <private-cluster-resource-group> \ --private-dns-zone none`


## Configure kubectl to connect to a private AKS cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group <private-cluster-resource-group> --name <private-cluster-name>`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The command returns output similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-12345678-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-12345678-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-12345678-vmss000002 Ready agent 3h6m v1.15.11`


---

<!-- DOCUMENTO FUSIONADO: _operator-best-practices-cluster-security_node-updates-kured.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: operator-best-practices-cluster-security.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-cluster-security -->

# Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), workload and data security is a key consideration. When you run multi-tenant clusters using logical isolation, you especially need to secure resource and workload access. Minimize the risk of attack by applying the latest Kubernetes and node OS security updates.

This article focuses on how to secure your AKS cluster. You learn how to:

- Use Microsoft Entra ID and Kubernetes role-based access control (Kubernetes RBAC) to secure API server access.
- Secure container access to node resources.
- Upgrade an AKS cluster to the latest Kubernetes version.
- Keep nodes up to date and automatically apply security patches.

You can also read the best practices for [container image management](operator-best-practices-container-image-management) and for [pod security](developer-best-practices-pod-security).

## Enable threat protection


Best practice guidanceYou can enable

[Defender for Containers]to help secure your containers. Defender for Containers can assess cluster configurations and provide security recommendations, run vulnerability scans, and provide real-time protection and alerting for Kubernetes nodes and clusters.

## Secure access to the API server and cluster nodes


Best practice guidanceOne of the most important ways to secure your cluster is to secure access to the Kubernetes API server. To control access to the API server, integrate Kubernetes RBAC with Microsoft Entra ID. With these controls,you secure AKS the same way that you secure access to your Azure subscriptions.


The Kubernetes API server provides a single connection point for requests to perform actions within a cluster. To secure and audit access to the API server, limit access and provide the lowest possible permission levels. while this approach isn't unique to Kubernetes, it's especially important when you've logically isolated your AKS cluster for multi-tenant use.

Microsoft Entra ID provides an enterprise-ready identity management solution that integrates with AKS clusters. Since Kubernetes doesn't provide an identity management solution, you may be hard-pressed to granularly restrict access to the API server. With Microsoft Entra integrated clusters in AKS, you use your existing user and group accounts to authenticate users to the API server.

Using Kubernetes RBAC and Microsoft Entra ID-integration, you can secure the API server and provide the minimum permissions required to a scoped resource set, like a single namespace. You can grant different Microsoft Entra users or groups different Kubernetes roles. With granular permissions, you can restrict access to the API server and provide a clear audit trail of actions performed.

The recommended best practice is to use *groups* to provide access to files and folders instead of individual identities. For example, use a Microsoft Entra ID *group* membership to bind users to Kubernetes roles rather than individual *users*. As a user's group membership changes, their access permissions on the AKS cluster change accordingly.

Meanwhile, let's say you bind the individual user directly to a role and their job function changes. While the Microsoft Entra group memberships update, their permissions on the AKS cluster would not. In this scenario, the user ends up with more permissions than they require.

For more information about Microsoft Entra integration, Kubernetes RBAC, and Azure RBAC, see [Best practices for authentication and authorization in AKS](concepts-identity).

## Restrict access to Instance Metadata API


Best practice guidanceAdd a network policy in all user namespaces to block pod egress to the metadata endpoint.


Note

To implement Network Policy, include the attribute `--network-policy azure`

when creating the AKS cluster. Use the following command to create the cluster:
`az aks create -g myResourceGroup -n myManagedCluster --network-plugin azure --network-policy azure --generate-ssh-keys`


```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: restrict-instance-metadata
spec:
podSelector:
matchLabels: {}
policyTypes:
- Egress
egress:
- to:
- ipBlock:
cidr: 10.10.0.0/0#example
except:
- 169.254.169.254/32
```


## Secure container access to resources


Best practice guidanceLimit access to actions that containers can perform. Provide the least number of permissions, and avoid the use of root access or privileged escalation.


In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access.

Using user-namespaces, you improve the host isolation and limit the lateral movement in case of container breakouts. These improvements are significant whether the pod is running as root or not.

For even more granular control of container actions, you can also use built-in Linux security features such as *AppArmor* and *seccomp*.

For more information, see [Secure container access to resources](secure-container-access).

## Regularly update to the latest version of Kubernetes


Best practice guidanceTo stay current on new features and bug fixes, regularly upgrade the Kubernetes version in your AKS cluster.


Kubernetes releases new features at a quicker pace than more traditional infrastructure platforms. Kubernetes updates include:

- New features
- Bug or security fixes

New features typically move through *alpha* and *beta* status before they become *stable*. Once stable, are generally available and recommended for production use. Kubernetes new feature release cycle allows you to update Kubernetes without regularly encountering breaking changes or adjusting your deployments and templates.

AKS supports three minor versions of Kubernetes. Once a new minor patch version is introduced, the oldest minor version and patch releases supported are retired. Minor Kubernetes updates happen on a periodic basis. To stay within support, ensure you have a governance process to check for necessary upgrades. For more information, see [Supported Kubernetes versions AKS](supported-kubernetes-versions).

To check the versions that are available for your cluster, use the [az aks get-upgrades](/en-us/cli/azure/aks#az-aks-get-upgrades) command as shown in the following example:

```
az aks get-upgrades --resource-group myResourceGroup --name myAKSCluster --output table
```


You can then upgrade your AKS cluster using the [az aks upgrade](/en-us/cli/azure/aks#az-aks-upgrade) command. The upgrade process safely:

- Cordons and drains one node at a time.
- Schedules pods on remaining nodes.
- Deploys a new node running the latest OS and Kubernetes versions.

Important

Test new minor versions in a dev test environment and validate that your workload remains healthy with the new Kubernetes version.

Kubernetes may deprecate APIs (like in version 1.16) that your workloads rely on. When bringing new versions into production, consider using [multiple node pools on separate versions](create-node-pools) and upgrade individual pools one at a time to progressively roll the update across a cluster. If running multiple clusters, upgrade one cluster at a time to progressively monitor for impact or changes.

```
az aks upgrade --resource-group myResourceGroup --name myAKSCluster --kubernetes-version KUBERNETES_VERSION
```


For more information about upgrades in AKS, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions) and [Upgrade an AKS cluster](upgrade-cluster).

## Process Linux node updates

Each evening, Linux nodes in AKS get security patches through their distro update channel. This behavior is automatically configured as the nodes are deployed in an AKS cluster. To minimize disruption and potential impact to running workloads, nodes are not automatically rebooted if a security patch or kernel update requires it. For more information about how to handle node reboots, see [Apply security and kernel updates to nodes in AKS](node-updates-kured).

### Node image upgrades

Unattended upgrades apply updates to the Linux node OS, but the image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node will receive all the security and kernel updates available during the automatic check every night but will remain unpatched until all checks and restarts are complete. You can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

## Process Windows Server node updates

For Windows Server nodes, regularly perform a node image upgrade operation to safely cordon and drain pods and deploy updated nodes.


---

<!-- DOCUMENTO FUSIONADO: node-updates-kured.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-updates-kured -->

# Apply security and kernel updates to Linux nodes in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To protect your clusters, security updates are automatically applied to Linux nodes in AKS. These updates include OS security fixes or kernel updates. Some of these updates require a node reboot to complete the process. AKS doesn't automatically reboot these Linux nodes to complete the update process.

The process to keep Windows Server nodes up to date is a little different. Windows Server nodes don't receive daily updates. Instead, you perform an AKS upgrade that deploys new nodes with the latest base Window Server image and patches. For AKS clusters that use Windows Server nodes, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

This article shows you how to use the open-source [kured (KUbernetes REboot Daemon)](https://github.com/kubereboot/kured) to watch for Linux nodes that require a reboot, then automatically handle the rescheduling of running pods and node reboot process.

Note

`Kured`

is an open-source project in the Cloud Native Computing Foundation. Please direct issues to the [kured GitHub](https://github.com/kubereboot/kured). Additional support can be found in the #kured channel on [CNCF Slack](https://slack.cncf.io).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Before you begin

You need the Azure CLI version 2.0.59 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Understand the AKS node update experience

In an AKS cluster, your Kubernetes nodes run as Azure virtual machines (VMs). These Linux-based VMs use an Ubuntu or Azure Linux image, with the OS configured to automatically check for updates every day. If security or kernel updates are available, they're automatically downloaded and installed.

Some security updates, such as kernel updates, require a node reboot to finalize the process. A Linux node that requires a reboot creates a file named */var/run/reboot-required*. This reboot process doesn't happen automatically.

You can use your own workflows and processes to handle node reboots, or use `kured`

to orchestrate the process. With `kured`

, a [DaemonSet](concepts-clusters-workloads#statefulsets-and-daemonsets) is deployed that runs a pod on each Linux node in the cluster. These pods in the DaemonSet watch for existence of the */var/run/reboot-required* file, and then initiate a process to reboot the nodes.

### Node image upgrades

Unattended upgrades apply updates to the Linux node OS, but the image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node receives all the security and kernel updates available during the automatic check every day but remains unpatched until all checks and restarts are complete.

Alternatively, you can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

### Node upgrades

There's another process in AKS that lets you *upgrade* a cluster. An upgrade is typically to move to a newer version of Kubernetes, not just apply node security updates. An AKS upgrade performs the following actions:

- A new node is deployed with the latest security updates and Kubernetes version applied.
- An old node is cordoned and drained.
- Pods are scheduled on the new node.
- The old node is deleted.

You can't remain on the same Kubernetes version during an upgrade event. You must specify a newer version of Kubernetes. To upgrade to the latest version of Kubernetes, you can [upgrade your AKS cluster](upgrade-cluster).

## Deploy kured in an AKS cluster

To deploy the `kured`

DaemonSet, install the following official Kured Helm chart. This creates a role and cluster role, bindings, and a service account, then deploys the DaemonSet using `kured`

.

```
# Add the Kured Helm repository
helm repo add kubereboot https://kubereboot.github.io/charts/
# Update your local Helm chart repository cache
helm repo update
# Create a dedicated namespace where you would like to deploy kured into
kubectl create namespace kured
# Install kured in that namespace with Helm 3 (only on Linux nodes, kured is not working on Windows nodes)
helm install my-release kubereboot/kured --namespace kured --set controller.nodeSelector."kubernetes\.io/os"=linux
```


You can also configure extra parameters for `kured`

, such as integration with Prometheus or Slack. For more information about configuration parameters, see the [kured Helm chart](https://github.com/kubereboot/charts/tree/main/charts/kured).

## Update cluster nodes

By default, Linux nodes in AKS check for updates every evening. If you don't want to wait, you can manually perform an update to check that `kured`

runs correctly. First, follow the steps to [SSH to one of your AKS nodes](ssh). Once you have an SSH connection to the Linux node, check for updates and apply them as follows:

```
sudo apt-get update && sudo apt-get upgrade -y
```


If updates were applied that require a node reboot, a file is written to */var/run/reboot-required*. `Kured`

checks for nodes that require a reboot every 60 minutes by default.

## Monitor and review reboot process

When one of the replicas in the DaemonSet detects that a node reboot is required, a lock is placed on the node through the Kubernetes API. This lock prevents more pods from being scheduled on the node. The lock also indicates that only one node should be rebooted at a time. With the node cordoned off, running pods are drained from the node, and the node is rebooted.

You can monitor the status of the nodes using the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. The following example output shows a node with a status of *SchedulingDisabled* as the node prepares for the reboot process:

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-28993262-0 Ready,SchedulingDisabled agent 1h v1.11.7
```


Once the update process is complete, you can view the status of the nodes using the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command with the `--output wide`

parameter. This output lets you see a difference in *KERNEL-VERSION* of the underlying nodes, as shown in the following example output. The *aks-nodepool1-28993262-0* was updated in a previous step and shows kernel version *4.15.0-1039-azure*. The node *aks-nodepool1-28993262-1* that hasn't been updated shows kernel version *4.15.0-1037-azure*.

```
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodepool1-28993262-0 Ready agent 1h v1.11.7 10.240.0.4 <none> Ubuntu 16.04.6 LTS 4.15.0-1039-azure docker://3.0.4
aks-nodepool1-28993262-1 Ready agent 1h v1.11.7 10.240.0.5 <none> Ubuntu 16.04.6 LTS 4.15.0-1037-azure docker://3.0.4
```


## Next steps

This article detailed how to use `kured`

to reboot Linux nodes automatically as part of the security update process. To upgrade to the latest version of Kubernetes, you can [upgrade your AKS cluster](upgrade-cluster).

For AKS clusters that use Windows Server nodes, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-addon -->

# Deploy Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to install the Istio-based service mesh add-on for Azure Kubernetes Service (AKS) cluster.

For more information on Istio and the service mesh add-on, see [Istio-based service mesh add-on for Azure Kubernetes Service](istio-about).

Tip

You can use Azure Copilot to help deploy Istio to your AKS clusters in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#install-and-work-with-istio).

## Before you begin

The add-on requires Azure CLI version 2.57.0 or later installed. You can run

`az --version`

to verify version. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).To find information about which Istio add-on revisions are available in a region and their compatibility with AKS standard and LTS cluster versions, use the command

:`az aks mesh get-revisions`

`az aks mesh get-revisions --location <location> -o table`

For more information on the Istio add-on's compatibility with AKS, refer to the

[compatibility support policy](istio-support-policy#aks-compatibility).In some cases, Istio CRDs from previous installations may not be automatically cleaned up on uninstall. Ensure existing Istio CRDs are deleted:

`kubectl delete crd $(kubectl get crd -A | grep "istio.io" | awk '{print $1}')`

It is recommended to also clean up other resources from self-managed installations of Istio such as ClusterRoles, MutatingWebhookConfigurations and ValidatingWebhookConfigurations.

Note that if you choose to use any

`istioctl`

CLI commands, you will need to include a flag to point to the add-on installation of Istio:`--istioNamespace aks-istio-system`


### Set environment variables

```
export CLUSTER=<cluster-name>
export RESOURCE_GROUP=<resource-group-name>
export LOCATION=<location>
```


## Install Istio add-on

This section includes steps to install the Istio add-on during cluster creation or enable for an existing cluster using the Azure CLI. If you want to install the add-on using Bicep, see the guide for [installing an AKS cluster with the Istio service mesh add-on using Bicep](https://github.com/Azure-Samples/aks-istio-addon-bicep). To learn more about the Bicep resource definition for an AKS cluster, see [Bicep managedCluster reference](/en-us/azure/templates/microsoft.containerservice/managedclusters).

Note

If you need the `istiod`

and ingress/egress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

### Revision selection

If you enable the add-on without specifying a revision, a default supported revision is installed for you.

To specify a revision, perform the following steps.

- Use the
command to check which revisions are available for different AKS cluster versions in a region.`az aks mesh get-revisions`

- Based on the available revisions, you can include the
`--revision asm-X-Y`

(ex:`--revision asm-1-24`

) flag in the enable command you use for mesh installation.

### Install mesh during cluster creation

To install the Istio add-on when creating the cluster, use the `--enable-azure-service-mesh`

or`--enable-asm`

parameter.

```
az group create --name ${RESOURCE_GROUP} --location ${LOCATION}
az aks create \
--resource-group ${RESOURCE_GROUP} \
--name ${CLUSTER} \
--enable-asm \
--generate-ssh-keys
```


### Install mesh for existing cluster

The following example enables Istio add-on for an existing AKS cluster:

Important

You can't enable the Istio add-on on an existing cluster if an Open Service Mesh (OSM) add-on is already on your cluster. Uninstall the OSM add-on before installing the Istio add-on.
For more information, see [uninstall the OSM add-on from your AKS cluster](open-service-mesh-uninstall-add-on).
Istio add-on can only be enabled on AKS clusters of version >= 1.23.

```
az aks mesh enable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


## Verify successful installation

To verify the Istio add-on is installed on your cluster, run the following command:

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.mode'
```


Confirm the output shows `Istio`

.

Use `az aks get-credentials`

to get the credentials for your AKS cluster:

```
az aks get-credentials --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


Use `kubectl`

to verify that `istiod`

(Istio control plane) pods are running successfully:

```
kubectl get pods -n aks-istio-system
```


Confirm the `istiod`

pod has a status of `Running`

. For example:

```
NAME READY STATUS RESTARTS AGE
istiod-asm-1-24-74f7f7c46c-xfdtl 1/1 Running 0 2m
istiod-asm-1-24-74f7f7c46c-4nt2v 1/1 Running 0 2m
```


## Enable sidecar injection

To automatically install sidecar to any new pods, you need to annotate your namespaces with the revision label corresponding to the control plane revision currently installed.

If you're unsure which revision is installed, use:

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.istio.revisions'
```


Apply the revision label:

```
kubectl label namespace default istio.io/rev=asm-X-Y
```


Important

Explicit versioning matching the control plane revision (ex: `istio.io/rev=asm-1-24`

) is required.

The default `istio-injection=enabled`

label will not work and will **cause the sidecar injection to skip the namespace** for the add-on.

For manual injection of sidecar using `istioctl kube-inject`

, you need to specify extra parameters for `istioNamespace`

(`-i`

) and `revision`

(`-r`

). For example:

```
kubectl apply -f <(istioctl kube-inject -f sample.yaml -i aks-istio-system -r asm-X-Y) -n foo
```


## Trigger sidecar injection

You can either deploy the sample application provided for testing, or trigger sidecar injection for existing workloads.

### Existing applications

If you have existing applications to be added to the mesh, ensure their namespaces are labeled as in the previous step, and then restart their deployments to trigger sidecar injection:

```
kubectl rollout restart -n <namespace> <deployment name>
```


Verify that sidecar injection succeeded by ensuring all containers are ready and looking for the `istio-proxy`

container in the `kubectl describe`

output, for example:

```
kubectl describe pod -n namespace <pod name>
```


The `istio-proxy`

container is the Envoy sidecar. Your application is now part of the data plane.

### Deploy sample application

Use `kubectl apply`

to deploy the sample application on the cluster:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/platform/kube/bookinfo.yaml
```


Note

Clusters using an HTTP proxy for outbound internet access will need to set up a Service Entry. For setup instructions see [HTTP proxy support in Azure Kubernetes Service](http-proxy)

Confirm several deployments and services are created on your cluster. For example:

```
service/details created
serviceaccount/bookinfo-details created
deployment.apps/details-v1 created
service/ratings created
serviceaccount/bookinfo-ratings created
deployment.apps/ratings-v1 created
service/reviews created
serviceaccount/bookinfo-reviews created
deployment.apps/reviews-v1 created
deployment.apps/reviews-v2 created
deployment.apps/reviews-v3 created
service/productpage created
serviceaccount/bookinfo-productpage created
deployment.apps/productpage-v1 created
```


Use `kubectl get services`

to verify that the services were created successfully:

```
kubectl get services
```


Confirm the following services were deployed:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
details ClusterIP 10.0.180.193 <none> 9080/TCP 87s
kubernetes ClusterIP 10.0.0.1 <none> 443/TCP 15m
productpage ClusterIP 10.0.112.238 <none> 9080/TCP 86s
ratings ClusterIP 10.0.15.201 <none> 9080/TCP 86s
reviews ClusterIP 10.0.73.95 <none> 9080/TCP 86s
```


```
kubectl get pods
```


```
NAME READY STATUS RESTARTS AGE
details-v1-558b8b4b76-2llld 2/2 Running 0 2m41s
productpage-v1-6987489c74-lpkgl 2/2 Running 0 2m40s
ratings-v1-7dc98c7588-vzftc 2/2 Running 0 2m41s
reviews-v1-7f99cc4496-gdxfn 2/2 Running 0 2m41s
reviews-v2-7d79d5bd5d-8zzqd 2/2 Running 0 2m41s
reviews-v3-7dbcdcbc56-m8dph 2/2 Running 0 2m41s
```


Confirm that all the pods have status of `Running`

with two containers in the `READY`

column. The second container (`istio-proxy`

) added to each pod is the Envoy sidecar injected by Istio, and the other is the application container.

To test this sample application against ingress, check out [next-steps](#next-steps).

## Next steps

[Deploy external or internal ingresses for Istio service mesh add-on](istio-deploy-ingress)[Scale istiod and ingress gateway HPA](istio-scale#scaling)[Collect metrics for Istio service mesh add-on workloads in Azure Managed Prometheus](istio-metrics-managed-prometheus)[Deploy egress gateways for the Istio service mesh add-on](istio-deploy-egress)[Enable Istio CNI for Istio service mesh add-on (Preview)](istio-cni)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-azure-cni-dynamic-ip-allocation -->

# Configure Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A drawback with the traditional CNI is the exhaustion of pod IP addresses as the AKS cluster grows, which results in the need to rebuild your entire cluster in a bigger subnet. The new dynamic IP allocation capability in Azure CNI solves this problem by allocating pod IPs from a subnet separate from the subnet hosting the AKS cluster.

It offers the following benefits:

**Better IP utilization**: IPs are dynamically allocated to cluster Pods from the Pod subnet. This leads to better utilization of IPs in the cluster compared to the traditional CNI solution, which does static allocation of IPs for every node.**Scalable and flexible**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pods are assigned virtual network IPs, they have direct connectivity to other cluster pod and resources in the VNet. The solution supports very large clusters without any degradation in performance.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using NSGs to filter traffic between node pools.**Kubernetes network policies**: Both the Azure Network Policies and Calico work with this new solution.

This article shows you how to use Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support in AKS.

## Prerequisites

Review the

[prerequisites](configure-azure-cni#prerequisites)for configuring basic Azure CNI networking in AKS, as the same prerequisites apply to this article.Review the

[deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS, as the same parameters apply.AKS Engine and DIY clusters aren't supported.

Azure CLI version

`2.37.0`

or later.If you have an existing cluster, you need to enable Container Insights for monitoring IP subnet usage. You can enable Container Insights using the

command, as shown in the following example:`az aks enable-addons`

`az aks enable-addons --addons monitoring --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME`


## Plan IP addressing

Planning your IP addressing is much simpler with this feature. Since the nodes and pods scale independently, their address spaces can also be planned separately. Since pod subnets can be configured to the granularity of a node pool, you can always add a new subnet when you add a node pool. The system pods in a cluster/node pool also receive IPs from the pod subnet, so this behavior needs to be accounted for.

IPs are allocated to nodes in batches of 16. Pod subnet IP allocation should be planned with a minimum of 16 IPs per node in the cluster; nodes will request 16 IPs on startup and will request another batch of 16 any time there are <8 IPs unallocated in their allotment.

The planning of IPs for Kubernetes services and Docker bridge remain unchanged.

To view and verify the NodeNetworkConfiguration (NNC) resources responsible for these IP allocations, you can run the following command:

```
kubectl get nodenetworkconfigs -n kube-system -o wide
```


## Maximum pods per node in a cluster with Pod Subnet - Dynamic IP Allocation and enhanced subnet support

The pods per node value when using Azure CNI Pod Subnet - Dynamic IP Allocation is slightly different from the traditional CNI behavior:

| CNI | Default | Configurable at deployment |
|---|---|---|
| Traditional Azure CNI | 30 | Yes (up to 250) |
| Azure CNI Pod Subnet - Dynamic IP Allocation | 250 | Yes (up to 250) |

All other guidance related to configuring the maximum pods per node remains the same.

## Deployment parameters

The [deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS are all valid, with two exceptions:

- The
**subnet**parameter now refers to the subnet related to the cluster's nodes. - An additional parameter
**pod subnet**is used to specify the subnet whose IP addresses will be dynamically allocated to pods.

## Configure Pod Subnet - Dynamic IP Allocation and enhanced subnet support - Azure CLI

Using Pod Subnet - Dynamic IP Allocation and enhanced subnet support in your cluster is similar to the default method for configuring a cluster Azure CNI. The following example walks through creating a new virtual network with a subnet for nodes and a subnet for pods, and creating a cluster that uses Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support. Be sure to replace variables such as `$subscription`

with your own values.

Create the virtual network with two subnets.

```
RESOURCE_GROUP_NAME="myResourceGroup"
VNET_NAME="myVirtualNetwork"
LOCATION="westcentralus"
SUBNET_NAME_1="nodesubnet"
SUBNET_NAME_2="podsubnet"
# Create the resource group
az group create --name $RESOURCE_GROUP_NAME --location $LOCATION
# Create our two subnet network
az network vnet create --resource-group $RESOURCE_GROUP_NAME --location $LOCATION --name $VNET_NAME --address-prefixes 10.0.0.0/8 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_1 --address-prefixes 10.240.0.0/16 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_2 --address-prefixes 10.241.0.0/16 -o none
```


Create the cluster, referencing the node subnet using `--vnet-subnet-id`

and the pod subnet using `--pod-subnet-id`

and enabling the monitoring add-on.

```
CLUSTER_NAME="myAKSCluster"
SUBSCRIPTION="aaaaaaa-aaaaa-aaaaaa-aaaa"
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--location $LOCATION \
--max-pods 250 \
--node-count 2 \
--network-plugin azure \
--vnet-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_1 \
--pod-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_2 \
--enable-addons monitoring \
--generate-ssh-keys
```


### Adding node pool

When adding node pool, reference the node subnet using `--vnet-subnet-id`

and the pod subnet using `--pod-subnet-id`

. The following example creates two new subnets that are then referenced in the creation of a new node pool:

```
SUBNET_NAME_3="node2subnet"
SUBNET_NAME_4="pod2subnet"
NODE_POOL_NAME="mynodepool"
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_3 --address-prefixes 10.242.0.0/16 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_4 --address-prefixes 10.243.0.0/16 -o none
az aks nodepool add --cluster-name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --name $NODE_POOL_NAME \
--max-pods 250 \
--node-count 2 \
--vnet-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_3 \
--pod-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_4 \
--no-wait
```


## Monitor IP subnet usage

Azure CNI provides the capability to monitor IP subnet usage. To enable IP subnet usage monitoring, follow the steps below:

### Get the YAML file

Download or grep the file named container-azm-ms-agentconfig.yaml from

[GitHub](https://raw.githubusercontent.com/microsoft/Docker-Provider/ci_prod/kubernetes/container-azm-ms-agentconfig.yaml).Find

in integrations. Set`azure_subnet_ip_usage`

`enabled`

to`true`

.Save the file.


### Get the AKS credentials

Set the variables for subscription, resource group and cluster. Consider the following as examples:

```
az account set --subscription $SUBSCRIPTION
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME
```


### Apply the config

- Open the terminal in the folder in which the downloaded
**container-azm-ms-agentconfig.yaml**file is saved. - Apply the config using the
`kubectl apply -f container-azm-ms-agentconfig.yaml`

command. This will restart the pod and after 5-10 minutes, the metrics will be visible. - View the metrics on the cluster by navigating to Workbooks on the cluster page in the Azure portal, and find the workbook named
*Subnet IP Usage*.

## Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support FAQs

**Can I assign multiple pod subnets to a cluster/node pool?**Only one subnet can be assigned to a cluster or node pool. However, multiple clusters or node pools can share a single subnet.

**Can I assign Pod subnets from a different VNet altogether?**No, the pod subnet should be from the same VNet as the cluster.

**Can some node pools in a cluster use the traditional CNI while others use the new CNI?**The entire cluster should use only one type of CNI.


## Next steps

Learn more about networking in AKS in the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-deploy-addon-bicep -->

# Deploy the Open Service Mesh add-on using Bicep in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy the Open Service Mesh (OSM) add-on to Azure Kubernetes Service (AKS) using a [Bicep](/en-us/azure/azure-resource-manager/bicep/) template.

Note

With the retirement of [Open Service Mesh (OSM)](https://docs.openservicemesh.io/) by the Cloud Native Computing Foundation (CNCF), we recommend identifying your OSM configurations and migrating them to an equivalent Istio configuration. For information about migrating from OSM to Istio, see [Migration guidance for Open Service Mesh (OSM) configurations to Istio](open-service-mesh-istio-migration-guidance).

Important

Based on the version of Kubernetes your cluster is running, the OSM add-on installs a different version of OSM.

| Kubernetes version | OSM version installed |
|---|---|
| 1.24.0 or greater | 1.2.5 |
| Between 1.23.5 and 1.24.0 | 1.1.3 |
| Below 1.23.5 | 1.0.0 |

Older versions of OSM may not be available for install or be actively supported if the corresponding AKS version has reached end of life. You can check the [AKS Kubernetes release calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar) for information on AKS version support windows.

[Bicep](/en-us/azure/azure-resource-manager/bicep/overview) is a domain-specific language that uses declarative syntax to deploy Azure resources. You can use Bicep in place of creating [Azure Resource Manager templates](/en-us/azure/azure-resource-manager/templates/overview) to deploy your infrastructure-as-code Azure resources.

## Before you begin

Before you begin, make sure you have the following prerequisites in place:

- The Azure CLI version 2.20.0 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - An SSH public key used for deploying AKS. For more information, see
[Create SSH keys using the Azure CLI](/en-us/azure/virtual-machines/ssh-keys-azure-cli). [Visual Studio Code](https://code.visualstudio.com/)with a Bash terminal.- The Visual Studio Code
[Bicep extension](/en-us/azure/azure-resource-manager/bicep/install).

## Install the OSM add-on for a new AKS cluster by using Bicep

For deployment of a new AKS cluster, you enable the OSM add-on at cluster creation. The following instructions use a generic Bicep template that deploys an AKS cluster by using ephemeral disks and the [ kubenet](configure-kubenet) container network interface, and then enables the OSM add-on. For more advanced deployment scenarios, see

[What is Bicep?](/en-us/azure/azure-resource-manager/bicep/overview)

### Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name <my-osm-bicep-aks-cluster-rg> --location <azure-region>`


### Create the main and parameters Bicep files

Create a directory to store the necessary Bicep deployment files. The following example creates a directory named

*bicep-osm-aks-addon*and changes to the directory:`mkdir bicep-osm-aks-addon cd bicep-osm-aks-addon`

Create the main file and the parameters file.

`touch osm.aks.bicep && touch osm.aks.parameters.json`

Open the

*osm.aks.bicep*file and copy in the following content:`// https://learn.microsoft.com/azure/aks/troubleshooting#what-naming-restrictions-are-enforced-for-aks-resources-and-parameters @minLength(3) @maxLength(63) @description('Provide a name for the AKS cluster. The only allowed characters are letters, numbers, dashes, and underscore. The first and last character must be a letter or a number.') param clusterName string @minLength(3) @maxLength(54) @description('Provide a name for the AKS dnsPrefix. Valid characters include alphanumeric values and hyphens (-). The dnsPrefix can\'t include special characters such as a period (.)') param clusterDNSPrefix string param k8Version string param sshPubKey string param location string param adminUsername string resource aksCluster 'Microsoft.ContainerService/managedClusters@2021-03-01' = { name: clusterName location: location identity: { type: 'SystemAssigned' } properties: { kubernetesVersion: k8Version dnsPrefix: clusterDNSPrefix enableRBAC: true agentPoolProfiles: [ { name: 'agentpool' count: 3 vmSize: 'Standard_DS2_v2' osDiskSizeGB: 30 osDiskType: 'Ephemeral' osType: 'Linux' mode: 'System' } ] linuxProfile: { adminUsername: adminUserName ssh: { publicKeys: [ { keyData: sshPubKey } ] } } addonProfiles: { openServiceMesh: { enabled: true config: {} } } } }`

Open the

*osm.aks.parameters.json*file and copy in the following content. Make sure you replace the deployment parameter values with your own values.Note

The

*osm.aks.parameters.json*file is an example template parameters file needed for the Bicep deployment. Update the parameters specifically for your deployment environment. The parameters you need to add values for include:`clusterName`

,`clusterDNSPrefix`

,`k8Version`

,`sshPubKey`

,`location`

, and`adminUsername`

. To find a list of supported Kubernetes versions in your region, use the`az aks get-versions --location <region>`

command.`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#", "contentVersion": "1.0.0.0", "parameters": { "clusterName": { "value": "<YOUR CLUSTER NAME HERE>" }, "clusterDNSPrefix": { "value": "<YOUR CLUSTER DNS PREFIX HERE>" }, "k8Version": { "value": "<YOUR SUPPORTED KUBERNETES VERSION HERE>" }, "sshPubKey": { "value": "<YOUR SSH KEY HERE>" }, "location": { "value": "<YOUR AZURE REGION HERE>" }, "adminUsername": { "value": "<YOUR ADMIN USERNAME HERE>" } } }`


### Deploy the Bicep files

Open a terminal and authenticate to your Azure account for the Azure CLI using the

`az login`

command.Deploy the Bicep files using the

command.`az deployment group create`

`az deployment group create \ --name OSMBicepDeployment \ --resource-group osm-bicep-test \ --template-file osm.aks.bicep \ --parameters @osm.aks.parameters.json`


## Validate installation of the OSM add-on

Query the add-on profiles of the cluster to check the enabled state of the installed add-ons. The following command should return

`true`

:`az aks list -g <my-osm-aks-cluster-rg> -o json | jq -r '.[].addonProfiles.openServiceMesh.enabled'`

Get the status of the

*osm-controller*using the following`kubectl`

commands.`kubectl get deployments -n kube-system --selector app=osm-controller kubectl get pods -n kube-system --selector app=osm-controller kubectl get services -n kube-system --selector app=osm-controller`


## Access the OSM add-on configuration

You can configure the OSM controller using the OSM MeshConfig resource, and you can view the OSM controller's configuration settings using the Azure CLI.

View the OSM controller's configuration settings using the

`kubectl get`

command.`kubectl get meshconfig osm-mesh-config -n kube-system -o yaml`

Here's an example output of MeshConfig:

`apiVersion: config.openservicemesh.io/v1alpha1 kind: MeshConfig metadata: creationTimestamp: "0000-00-00A00:00:00A" generation: 1 name: osm-mesh-config namespace: kube-system resourceVersion: "2494" uid: 6c4d67f3-c241-4aeb-bf4f-b029b08faa31 spec: certificate: serviceCertValidityDuration: 24h featureFlags: enableEgressPolicy: true enableMulticlusterMode: false enableWASMStats: true observability: enableDebugServer: true osmLogLevel: info tracing: address: jaeger.osm-system.svc.cluster.local enable: false endpoint: /api/v2/spans port: 9411 sidecar: configResyncInterval: 0s enablePrivilegedInitContainer: false envoyImage: mcr.microsoft.com/oss/envoyproxy/envoy:v1.18.3 initContainerImage: mcr.microsoft.com/oss/openservicemesh/init:v0.9.1 logLevel: error maxDataPlaneConnections: 0 resources: {} traffic: enableEgress: true enablePermissiveTrafficPolicyMode: true inboundExternalAuthorization: enable: false failureModeAllow: false statPrefix: inboundExtAuthz timeout: 1s useHTTPSIngress: false`

Notice that

`enablePermissiveTrafficPolicyMode`

is configured to`true`

. In OSM, permissive traffic policy mode bypasses[SMI](https://smi-spec.io/)traffic policy enforcement. In this mode, OSM automatically discovers services that are a part of the service mesh. The discovered services will have traffic policy rules programmed on each Envoy proxy sidecar to allow communications between these services.Warning

Before you proceed, verify that your permissive traffic policy mode is set to

`true`

. If it isn't, change it to`true`

using the following command:`kubectl patch meshconfig osm-mesh-config -n kube-system -p '{"spec":{"traffic":{"enablePermissiveTrafficPolicyMode":true}}}' --type=merge`


## Clean up resources

When you no longer need the Azure resources, delete the deployment's test resource group using the

command.`az group delete`

`az group delete --name osm-bicep-test`

Alternatively, you can uninstall the OSM add-on and the related resources from your cluster. For more information, see

[Uninstall the Open Service Mesh add-on from your AKS cluster](open-service-mesh-uninstall-add-on).

## Next steps

This article showed you how to install the OSM add-on on an AKS cluster and verify that it's installed and running. With the OSM add-on installed on your cluster, you can [deploy a sample application](https://release-v1-0.docs.openservicemesh.io/docs/getting_started/install_apps/) or [onboard an existing application](https://release-v1-0.docs.openservicemesh.io/docs/guides/app_onboarding/) to work with your OSM mesh.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/flatcar-container-linux-for-aks -->

# Use Flatcar Container Linux for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of Flatcar Container Linux for AKS, a Cloud Native Compute Foundation (CNCF) project that provides security, reliability, and cross-cloud capabilities. Flatcar Container Linux is available in preview as an OS option on AKS. You can deploy Flatcar Container Linux node pools in a new AKS cluster or add Flatcar Container Linux node pools to your existing clusters. To learn more about Flatcar Container Linux, see the [Flatcar documentation](https://www.flatcar.org/).

## Flatcar Container Linux for AKS benefits

Flatcar uses an immutable OS filesystem, and it eliminates configuration drift and prevents unauthorized changes, ensuring robust protection for your workloads across multiple cloud platforms. Designed for versatility, Flatcar enables cross-cloud deployment, empowering businesses to scale effortlessly and securely.

## Limitations

Flatcar Container Linux for AKS has the following limitations:

[FIPS](enable-fips-nodes)isn't supported with Flatcar Container Linux.[Trusted Launch](use-trusted-launch)isn't supported with Flatcar Container Linux.[Confidential VM sizes](use-cvm)aren't supported with Flatcar Container Linux.- The
`SecurityPatch`

[node OS upgrade channel](auto-upgrade-node-os-image)isn't supported with Flatcar Container Linux. - During preview, AKS doesn't support in-place updates with Flatcar Container Linux.
[Artifact Streaming](artifact-streaming)(preview) isn't supported with Flatcar Container Linux.[Generation 1 VMs](aks-virtual-machine-sizes)aren't supported with Flatcar Container Linux, which means you can't use VM sizes that only support Generation 1.[Pod Sandboxing (preview)](use-pod-sandboxing)isn't supported with Flatcar Container Linux.[Node auto-provisioning](node-autoprovision)isn't supported with Flatcar Container Linux.[Azure Monitor VM(SS) extension](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-portal#:%7E:text=Virtual%20machine%20(VM)%20extension)isn't supported.

Note

If you have an existing cluster with any of the above features enabled, you might not be able to add a node pool using Flatcar Container Linux.

## Get started with Flatcar Container Linux for AKS

To get started using the Flatcar Container Linux for AKS, see the following resources:

- Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using
[Azure CLI](learn/quick-flatcar-deploy-cli) - Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using an
[ARM template](learn/quick-flatcar-deploy-arm-template) - Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool using
[Azure CLI or an ARM template](create-node-pools) - Add a Flatcar Container Linux for AKS (preview) node pool to an existing cluster using
[Azure CLI or an ARM template](create-node-pools)

## OS migrations and upgrades with Flatcar Container Linux

AKS doesn't support in-place migrations from existing Linux clusters or node pools to Flatcar Container Linux clusters or node pools. To migrate existing workloads to Flatcar Container Linux for AKS, you need to recreate your node pools using `--os-sku flatcar`

.

Flatcar Container Linux for AKS releases weekly AKS node images. Versioning follows the AKS date-based format (for example: 202506.13.0). You can check the node images in the release notes and by using the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. For example:```
az aks nodepool list --resource-group <resource-group-name> --cluster-name <aks-cluster-name> --query '[].{name: name, nodeImageVersion: nodeImageVersion}'
```


Example output:

```
[
{
"name": "nodes",
"nodeImageVersion": "AKSFlatcar-flatcargen2-202508.06.0"
}
]
```


You can check the Flatcar version number (for example: Flatcar 4372.0.1) in the release notes and by using `kubectl get nodes`

command. For example:

```
kubectl get nodes -o wide
```


Example output:

```
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodes-16363508-vmss000000 Ready <none> 2m33s v1.32.6 10.224.0.4 <none> Flatcar Container Linux by Kinvolk 4372.0.1 (Oklo) 6.12.35-flatcar containerd://2.0.4
```


Flatcar's inbuilt automatic A/B update for the OS partition is disabled and only full node image updates are supported.

## Next steps

To learn more about Flatcar Container Linux, see the [Flatcar documentation](https://www.flatcar.org/).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kms-observability -->

# Observability for Azure Kubernetes Service (AKS) clusters with Key Management Service (KMS) etcd encryption (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to view observability metrics and improve observability for AKS clusters with KMS etcd encryption.

## Prerequisites

- An AKS cluster with KMS etcd encryption enabled. For more information, see
[Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster](use-kms-etcd-encryption). - You must enable
[diagnostic settings for the key vault to check the encryption logs](/en-us/azure/key-vault/general/howto-logging).

## Check the KMS config

Get the KMS config using the

command.`az aks show`

`az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query "securityProfile.azureKeyVaultKms"`

The output looks similar to the following example output:

`... "securityProfile": { "azureKeyVaultKms": { "enabled": true, "keyId": "https://<key-vault-name>.vault.azure.net/keys/<key-name>/<key-id>", "keyVaultNetworkAccess": "Public", "keyVaultResourceId": <key-vault-resource-id> ...`


## Diagnose and solve problems

Because the KMS plugin is a sidecar of `kube-apiserver`

pod, you can't access it directly. To improve the observability of KMS, you can check the KMS status using the Azure portal.

- In the Azure portal, navigate to your AKS cluster.
- From the service menu, select
**Diagnose and solve problems**. - In the search bar, search for
**KMS**and select**Azure KeyVault KMS Integration Issues**.

### Example problem

Let's say you see the following issue: `KeyExpired: Operation encrypt isn't allowed on an expired key`

.

Because the AKS KMS plugin currently only allows bring your own (BYO) key vault and key, it's your responsibility to manage the key lifecycle. If the key is expired, the KMS plugin fails to decrypt the existing secrets. To resolve this issue, you need to *extend the key expiration date* to make KMS work and *rotate the key version*.

## Next steps

For more information on using KMS with AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-extension-attach-azure-container-registry -->

# Attach to Azure Container Registry (ACR) using the Azure Kubernetes Service (AKS) extension for Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to attach to Azure Container Registry (ACR) using the Azure Kubernetes Service (AKS) extension for Visual Studio Code.

## Prerequisites

Before you begin, make sure you have the following resources:

- An Azure container registry. If you don't have one, create one using the steps in
[Quickstart: Create a private container registry](/en-us/azure/container-registry/container-registry-get-started-azure-cli). - An AKS cluster. If you don't have one, create one using the steps in
[Quickstart: Deploy an AKS cluster](learn/quick-kubernetes-deploy-cli). - The Azure Kubernetes Service (AKS) extension for Visual Studio Code downloaded. For more information, see
[Install the Azure Kubernetes Service (AKS) extension for Visual Studio Code](aks-extension-vs-code#installation).

## Attach your Azure container registry to your AKS cluster

You can access the screen for attaching your container registry to your AKS cluster using the command palette or the Kubernetes view.

On your keyboard, press

`Ctrl+Shift+P`

to open the command palette.Enter the following information:

**Subscription**: Select the Azure subscription that holds your resources.**ACR Resource Group**: Select the resource group for your container registry.**Container Registry**: Select the container registry you want to attach to your cluster.**Cluster Resource Group**: Select the resource group for your cluster.**Cluster**: Select the cluster you want to attach to your container registry.

Select

**Attach**.You should see a green checkmark, which means your container registry is attached to your AKS cluster.


For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Product support and feedback

If you have a question or want to offer product feedback, please open an issue on the [AKS extension GitHub repository](https://github.com/Azure/vscode-aks-tools/issues/new/choose).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations for AKS](integrations).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-upgrade-cluster -->

# Tutorial - Upgrade an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As part of the application and cluster lifecycle, you might want to upgrade to the latest available version of Kubernetes. You can upgrade your Azure Kubernetes Service (AKS) cluster using the Azure CLI, Azure PowerShell, or the Azure portal.

In this tutorial, you upgrade an AKS cluster. You learn how to:

- Identify current and available Kubernetes versions.
- Upgrade your Kubernetes nodes.
- Validate a successful upgrade.

## Before you begin

In previous tutorials, you packaged an application into a container image and uploaded the container image to Azure Container Registry (ACR). You also created an AKS cluster and deployed an application to it. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

If using Azure CLI, this tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

If using Azure PowerShell, this tutorial requires Azure PowerShell version 5.9.0 or later. Run `Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see [Install Azure PowerShell](/en-us/powershell/azure/install-az-ps).

## Get available cluster versions

Before you upgrade, check which Kubernetes releases are available for your cluster using the

command.`az aks get-upgrades`

`az aks get-upgrades --resource-group myResourceGroup --name myAKSCluster`

The following example output shows the current version as

*1.28.9*and lists the available versions under`upgrades`

:`{ "agentPoolProfiles": null, "controlPlaneProfile": { "kubernetesVersion": "1.28.9", ... "upgrades": [ { "isPreview": null, "kubernetesVersion": "1.29.4" }, { "isPreview": null, "kubernetesVersion": "1.29.2" } ] }, ... }`


## Upgrade an AKS cluster

AKS nodes are carefully cordoned and drained to minimize any potential disruptions to running applications. During this process, AKS performs the following steps:

- Adds a new buffer node (or as many nodes as configured in
[max surge](upgrade-aks-cluster#customize-node-surge-upgrade)) to the cluster that runs the specified Kubernetes version. [Cordons and drains](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)one of the old nodes to minimize disruption to running applications. If you're using max surge, it[cordons and drains](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)as many nodes at the same time as the number of buffer nodes specified.- When the old node is fully drained, it's reimaged to receive the new version and becomes the buffer node for the following node to be upgraded.
- This process repeats until all nodes in the cluster have been upgraded.
- At the end of the process, the last buffer node is deleted, maintaining the existing agent node count and zone balance.

Note

If no patch is specified, the cluster automatically upgrades to the specified minor version's latest GA patch. For example, setting `--kubernetes-version`

to `1.28`

results in the cluster upgrading to `1.28.9`

.

For more information, see [Supported Kubernetes minor version upgrades in AKS](supported-kubernetes-versions#alias-minor-version).

You can either [manually upgrade your cluster](#manually-upgrade-cluster) or [configure automatic cluster upgrades](#configure-automatic-cluster-upgrades). **We recommend you configure automatic cluster upgrades to ensure your cluster is always running the latest version of Kubernetes**.

### Manually upgrade cluster

Upgrade your cluster using the

command.`az aks upgrade`

`az aks upgrade \ --resource-group myResourceGroup \ --name myAKSCluster \ --kubernetes-version KUBERNETES_VERSION`

You will be prompted to confirm the upgrade operation, and to confirm that you want to upgrade the control plane

*and*all the node pools to the selected version of Kubernetes:`Are you sure you want to perform this operation? (y/N): y Since control-plane-only argument is not specified, this will upgrade the control plane AND all nodepools to version 1.29.2. Continue? (y/N): y`

Note

You can only upgrade one minor version at a time. For example, you can upgrade from

*1.14.x*to*1.15.x*, but you can't upgrade from*1.14.x*to*1.16.x*directly. To upgrade from*1.14.x*to*1.16.x*, you must first upgrade from*1.14.x*to*1.15.x*, then perform another upgrade from*1.15.x*to*1.16.x*.The following example output shows the result of upgrading to

*1.29.2*. Notice the`kubernetesVersion`

now shows*1.29.2*:`{ ... "agentPoolProfiles": [ { ... "count": 3, "currentOrchestratorVersion": "1.29.2", "maxPods": 110, "name": "nodepool1", "nodeImageVersion": "AKSUbuntu-2204gen2containerd-202405.27.0", "orchestratorVersion": "1.29.2", "osType": "Linux", "upgradeSettings": { "drainTimeoutInMinutes": null, "maxSurge": "10%", "nodeSoakDurationInMinutes": null, "undrainableNodeBehavior": null }, "vmSize": "Standard_DS2_v2", ... } ], ... "currentKubernetesVersion": "1.29.2", "dnsPrefix": "myAKSClust-myResourceGroup-19da35", "enableRbac": false, "fqdn": "myaksclust-myresourcegroup-19da35-bd54a4be.hcp.westus2.azmk8s.io", "id": "/subscriptions/<Subscription ID>/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster", "kubernetesVersion": "1.29.2", "location": "westus2", "name": "myAKSCluster", "type": "Microsoft.ContainerService/ManagedClusters" ... }`


### Configure automatic cluster upgrades

Set an auto-upgrade channel on your cluster using the

command with the`az aks update`

`--auto-upgrade-channel`

parameter set to`patch`

.`az aks update --resource-group myResourceGroup --name myAKSCluster --auto-upgrade-channel patch`


For more information, see [Automatically upgrade an Azure Kubernetes Service (AKS) cluster](auto-upgrade-cluster).

#### Upgrade AKS node images

AKS regularly provides new node images. Linux node images are updated weekly, and Windows node images are updated monthly. We recommend upgrading your node images frequently to use the latest AKS features and security updates. For more information, see [Upgrade node images in Azure Kubernetes Service (AKS)](node-image-upgrade). To configure automatic node image upgrades, see [Automatically upgrade Azure Kubernetes Service (AKS) cluster node operating system images](auto-upgrade-node-image).

## View the upgrade events

Note

When you upgrade your cluster, the following Kubernetes events might occur on the nodes:

**Surge**: Create a surge node.**Drain**: Evict pods from the node. Each pod has a*five minute timeout*to complete the eviction.**Update**: Update of a node has succeeded or failed.**Delete**: Delete a surge node.

View the upgrade events in the default namespaces using the

`kubectl get events`

command.`kubectl get events --field-selector source=upgrader`

The following example output shows some of the above events listed during an upgrade:

`LAST SEEN TYPE REASON OBJECT MESSAGE ... 5m Normal Drain node/aks-nodepool1-96663640-vmss000000 Draining node: aks-nodepool1-96663640-vmss000000 5m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Deleting node aks-nodepool1-96663640-vmss000000 from API server 4m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Successfully reimaged node: aks-nodepool1-96663640-vmss000000 4m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Successfully upgraded node: aks-nodepool1-96663640-vmss000000 4m Normal Drain node/aks-nodepool1-96663640-vmss000000 Draining node: aks-nodepool1-96663640-vmss000000 ...`


## Validate an upgrade

Confirm the upgrade was successful using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --output table`

The following example output shows the AKS cluster runs

*KubernetesVersion 1.27.3*:`Name Location ResourceGroup KubernetesVersion CurrentKubernetesVersion ProvisioningState Fqdn ------------ ---------- --------------- ------------------- ------------------------ ------------------- ---------------------------------------------------------------- myAKSCluster westus2 myResourceGroup 1.29.2 1.29.2 Succeeded myaksclust-myresourcegroup-19da35-bd54a4be.hcp.westus2.azmk8s.io`


## Delete the cluster

As this tutorial is the last part of the series, you might want to delete your AKS cluster to avoid incurring Azure charges.

Remove the resource group, container service, and all related resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


Note

When you delete the cluster, the Microsoft Entra service principal used by the AKS cluster isn't removed. For steps on how to remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal). If you used a managed identity, the identity is managed by the platform and doesn't require that you provision or rotate any secrets.

## Next steps

In this tutorial, you upgraded Kubernetes in an AKS cluster. You learned how to:

- Identify current and available Kubernetes versions.
- Upgrade your Kubernetes nodes.
- Validate a successful upgrade.

For more information on AKS, see the [AKS overview](intro-kubernetes). For guidance on how to create full solutions with AKS, see the [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?WT.mc_id=AKSDOCSPAGE).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/availability-zones -->

# Configure availability zones in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Availability zones](/en-us/azure/reliability/availability-zones-overview) help protect your applications and data from datacenter failures. Zones are unique physical locations within an Azure region. Each zone includes one or more datacenters equipped with independent power, cooling, and networking.

Using Azure Kubernetes Service (AKS) with availability zones physically distributes resources across different availability zones within a single region, improving reliability. Deploying nodes in multiple zones doesn't incur additional costs. For more information on AKS reliability features including availability zones, multi-region configurations, reliability during service maintenance, and backup, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks).

This article shows you how to configure AKS resources to use availability zones.

## AKS resources

This diagram shows the Azure resources that are created when you create an AKS cluster:

### AKS control plane

Microsoft hosts the [AKS control plane](/en-us/azure/aks/core-aks-concepts#control-plane), the Kubernetes API server, and services such as `scheduler`

and `etcd`

as a managed service. Microsoft replicates the control plane in multiple zones.

Other resources of your cluster deploy in a managed resource group in your Azure subscription. By default, this resource group is prefixed with *MC_* for *managed cluster* and contains the resources mentioned in the following sections.

### Node pools

Node pools are created as virtual machine scale sets in your Azure subscription.

When you create an AKS cluster, one [system node pool](/en-us/azure/aks/use-system-pools) is required and is created automatically. It hosts critical system pods such as `CoreDNS`

and `metrics-server`

. You can add more [user node pools](/en-us/azure/aks/create-node-pools) to your AKS cluster to host your applications.

There are three ways node pools can be deployed:

- Zone-spanning
- Zone-aligned
- Regional

The system node pool zones are configured when the cluster or node pool is created.

#### Zone-spanning

In this configuration, nodes are spread across all selected zones. These zones are specified by using the `--zones`

parameter.

```
# Create an AKS cluster, and create a zone-spanning system node pool in all three AZs, one node in each AZ
az aks create --resource-group example-rg --name example-cluster --node-count 3 --zones 1 2 3
# Add one new zone-spanning user node pool, two nodes in each
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-a --node-count 6 --zones 1 2 3
```


AKS automatically balances the number of nodes between zones.

If a zonal outage occurs, nodes within the affected zone might be affected, but nodes in other availability zones remain unaffected.

To validate node locations, run the following command:

```
kubectl get nodes -o custom-columns='NAME:metadata.name, REGION:metadata.labels.topology\.kubernetes\.io/region, ZONE:metadata.labels.topology\.kubernetes\.io/zone'
```


```
NAME REGION ZONE
aks-nodepool1-34917322-vmss000000 eastus eastus-1
aks-nodepool1-34917322-vmss000001 eastus eastus-2
aks-nodepool1-34917322-vmss000002 eastus eastus-3
```


#### Zone-aligned

In this configuration, each node is aligned (pinned) to a specific zone. To create three node pools for a region with three availability zones:

```
# # Add three new zone-aligned user node pools, two nodes in each
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-x --node-count 2 --zones 1
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-y --node-count 2 --zones 2
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-z --node-count 2 --zones 3
```


This configuration can be used when you need [lower latency between nodes](/en-us/azure/aks/reduce-latency-ppg). It also provides more granular control over scaling operations, or when you're using the [cluster autoscaler](cluster-autoscaler-overview).

Note

If a single workload is deployed across node pools, we recommend setting `--balance-similar-node-groups`

to `true`

to maintain a balanced distribution of nodes across zones for your workloads during scale-up operations.

#### Regional (not using availability zones)

Regional mode is used when the zone assignment isn't set in the deployment template (for example, `"zones"=[]`

or `"zones"=null`

).

In this configuration, the node pool creates regional (not zone-pinned) instances and implicitly places instances throughout the region. There's no guarantee that instances are balanced or spread across zones, or that instances are in the same availability zone.

In the rare case of a full zonal outage, any or all instances within the node pool might be affected.

To validate node locations, run the following command:

```
kubectl get nodes -o custom-columns='NAME:metadata.name, REGION:metadata.labels.topology\.kubernetes\.io/region, ZONE:metadata.labels.topology\.kubernetes\.io/zone'
```


```
NAME REGION ZONE
aks-nodepool1-34917322-vmss000000 eastus 0
aks-nodepool1-34917322-vmss000001 eastus 0
aks-nodepool1-34917322-vmss000002 eastus 0
```


## Deployments

### Pods

Kubernetes is aware of Azure availability zones, and can balance pods across nodes in different zones. In the event a zone becomes unavailable, Kubernetes moves pods away from affected nodes automatically.

As documented in the Kubernetes reference [Well-Known Labels, Annotations and Taints](https://kubernetes.io/docs/reference/labels-annotations-taints/), Kubernetes uses the `topology.kubernetes.io/zone`

label to automatically distribute pods in a replication controller or service across the various available zones available.

To see which pods and nodes are running, run the following command:

```
kubectl describe pod | grep -e "^Name:" -e "^Node:"
```


The `maxSkew`

parameter describes the degree to which pods might be unevenly distributed. Assuming three zones and three replicas, setting this value to `1`

ensures that each zone has at least one pod running:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: my-deployment
spec:
selector:
matchLabels:
app: my-app
template:
metadata:
labels:
app: my-app
spec:
topologySpreadConstraints:
- maxSkew: 1
topologyKey: topology.kubernetes.io/zone
whenUnsatisfiable: DoNotSchedule
labelSelector:
matchLabels:
app: my-app
containers:
- name: my-container
image: my-image
```


### Storage and volumes

By default, Kubernetes versions 1.29 and later use Azure Managed Disks by using zone-redundant storage for Persistent Volume Claims.

These disks are replicated between zones, to enhance the resilience of your applications. This action helps to safeguard your data against datacenter failures.

The following example shows a Persistent Volume Claim that uses Azure Standard SSD in zone-redundant storage:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: azure-managed-disk
spec:
accessModes:
- ReadWriteOnce
storageClassName: managed-csi
#storageClassName: managed-csi-premium
resources:
requests:
storage: 5Gi
```


For zone-aligned deployments, you can create a new storage class with the `skuname`

parameter set to `LRS`

(locally redundant storage). You can then use the new storage class in your Persistent Volume Claim.

Although locally redundant storage disks are less expensive, they aren't zone-redundant, and attaching a disk to a node in a different zone isn't supported.

The following example shows a locally redundant storage Standard SSD storage class:

```
kind: StorageClass
metadata:
name: azuredisk-csi-standard-lrs
provisioner: disk.csi.azure.com
parameters:
skuname: StandardSSD_LRS
#skuname: PremiumV2_LRS
```


### Load balancers

Kubernetes deploys Azure Standard Load Balancer by default, which balances inbound traffic across all zones in a region. If a node becomes unavailable, the load balancer reroutes traffic to healthy nodes.

An example service that uses Azure Load Balancer:

```
apiVersion: v1
kind: Service
metadata:
name: example
spec:
type: LoadBalancer
selector:
app: myapp
ports:
- port: 80
targetPort: 8080
```


Important

On September 30, 2025, Basic Load Balancer will be retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). If you use Basic Load Balancer, make sure to [upgrade](/en-us/azure/load-balancer/load-balancer-basic-upgrade-guidance) to Standard Load Balancer before the retirement date.

## Limitations

The following limitations apply when you're using availability zones:

- See
[Quotas, virtual machine size restrictions, and region availability in AKS](quotas-skus-regions#supported-vm-sizes). - The number of availability zones used
*can't be changed*after the node pool is created. - Most regions support availability zones.
[See a list of regions](/en-us/azure/reliability/regions-list).

## Related content

- Learn about
[Reliability in AKS](/en-us/azure/reliability/reliability-aks). - Learn about
[system node pools](/en-us/azure/aks/use-system-pools). - Learn about
[user node pools](/en-us/azure/aks/create-node-pools). - Learn about
[load balancers](/en-us/azure/aks/load-balancer-standard). - Get
[best practices for business continuity and disaster recovery in AKS](operator-best-practices-storage).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-azure-ad -->

# Enable AKS-managed Microsoft Entra integration for Kubernetes clusters with kubelogin

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The AKS-managed Microsoft Entra integration simplifies the Microsoft Entra integration process. Previously, you were required to create a client and server app, and the Microsoft Entra tenant had to assign [Directory Readers](/en-us/entra/identity/role-based-access-control/permissions-reference#directory-readers) role permissions. Now, the Azure Kubernetes Service (AKS) resource provider manages the client and server apps for you.

Cluster administrators can configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership. Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/entra/identity-platform/v2-protocols-oidc).

Learn more about the Microsoft Entra integration flow in the [Microsoft Entra documentation](concepts-identity#azure-ad-integration).

## Limitations

The following are constraints to integrate authentication on AKS:

- Integration can't be disabled after being added.
- Downgrades from an integrated cluster to the legacy Microsoft Entra ID clusters aren't supported.
- Clusters without Kubernetes RBAC support are unable to add the integration.

## Before you begin

To install the AKS addon, verify you have the following items:

- You have Azure CLI version 2.29.0 or later installed and configured. To find the version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

with a minimum version of[1.18.1](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1181)or. With the Azure CLI and the Azure PowerShell module, these two commands are included and automatically managed. Meaning, they're upgraded by default and running`kubelogin`

`az aks install-cli`

isn't required or recommended. If you're using an automated pipeline, you need to manage upgrades for the correct or latest version. The difference between the minor versions of Kubernetes and`kubectl`

shouldn't be more than*one*version. Otherwise, authentication issues occur on the wrong version. - If you're using
[helm](https://github.com/helm/helm), you need a minimum version of helm 3.3. - This configuration requires you have a Microsoft Entra group for your cluster. This group is registered as an admin group on the cluster to grant admin permissions. If you don't have an existing Microsoft Entra group, you can create one using the
command.`az ad group create`


Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution

`PATH`

. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded `kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.## Enable the integration on your AKS cluster

### Create a new cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create an AKS cluster and enable administration access for your Microsoft Entra group using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-aad \ --aad-admin-group-object-ids <id> \ --aad-tenant-id <id> \ --generate-ssh-keys`

A successful creation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body.

`"AADProfile": { "adminGroupObjectIds": [ "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb" ], "clientAppId": null, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee" }`


### Use an existing cluster

Enable AKS-managed Microsoft Entra integration on your existing Kubernetes RBAC enabled cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. Make sure to set your admin group to keep access on your cluster.

```
az aks update \
--resource-group MyResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id-1>,<id-2> \
--aad-tenant-id <id>
```


A successful activation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


### Migrate legacy cluster to integration

If your cluster uses legacy Microsoft Entra integration, you can upgrade to AKS-managed Microsoft Entra integration through the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

Warning

Free tier clusters might experience API server downtime during the upgrade. We recommend upgrading during your nonbusiness hours.
After the upgrade, the `kubeconfig`

content changes. You need to run `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

to merge the new credentials into the `kubeconfig`

file.

```
az aks update \
--resource-group myResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id> \
--aad-tenant-id <id>
```


A successful migration of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


## Access your enabled cluster

Get the user credentials to access your cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myManagedCluster`

Follow your sign in instructions.

Set

`kubelogin`

to use the Azure CLI.`kubelogin convert-kubeconfig -l azurecli`

View the nodes in the cluster with the

`kubectl get nodes`

command.`kubectl get nodes`


## Non-interactive sign-in with kubelogin

There are some non-interactive scenarios that don't support `kubectl`

. In these cases, use [ kubelogin](https://github.com/Azure/kubelogin) to connect to the cluster with a non-interactive service principal credential to perform continuous integration pipelines.

Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution PATH. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded

`kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.When getting the `clusterUser`

credential, you can use the `format`

query parameter to overwrite the default behavior. You can set the value to `azure`

to use the original `kubeconfig`

format:

```
az aks get-credentials --format azure
```


If your Microsoft Entra integrated cluster uses Kubernetes version 1.24 or lower, you need to manually convert the `kubeconfig`

format.

```
export KUBECONFIG=/path/to/kubeconfig
kubelogin convert-kubeconfig
```


If you receive the message **error: The Azure auth plugin has been removed.**, you need to run the command `kubelogin convert-kubeconfig`

to convert the `kubeconfig`

format manually. For more information, see [Azure Kubelogin Known Issues](https://azure.github.io/kubelogin/known-issues.html).

## Troubleshoot access issues

Important

The step described in this section suggests an alternative authentication method compared to the normal Microsoft Entra group authentication. Use this option only in an emergency.

If you lack administrative access to a valid Microsoft Entra group, you can follow this workaround. Sign in with an account that is a member of the [Azure Kubernetes Service Cluster Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) role and grant your group or tenant admin credentials to access your cluster.

## Next steps

- Learn about
[Microsoft Entra integration with Kubernetes RBAC](azure-ad-rbac). - Learn more about
[AKS and Kubernetes identity concepts](concepts-identity). - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS. - Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create AKS-managed Microsoft Entra ID enabled clusters.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/enable-authentication-microsoft-entra-id -->

# Enable AKS-managed Microsoft Entra integration for Kubernetes clusters with kubelogin

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The AKS-managed Microsoft Entra integration simplifies the Microsoft Entra integration process. Previously, you were required to create a client and server app, and the Microsoft Entra tenant had to assign [Directory Readers](/en-us/entra/identity/role-based-access-control/permissions-reference#directory-readers) role permissions. Now, the Azure Kubernetes Service (AKS) resource provider manages the client and server apps for you.

Cluster administrators can configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership. Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/entra/identity-platform/v2-protocols-oidc).

Learn more about the Microsoft Entra integration flow in the [Microsoft Entra documentation](concepts-identity#azure-ad-integration).

## Limitations

The following are constraints to integrate authentication on AKS:

- Integration can't be disabled after being added.
- Downgrades from an integrated cluster to the legacy Microsoft Entra ID clusters aren't supported.
- Clusters without Kubernetes RBAC support are unable to add the integration.

## Before you begin

To install the AKS addon, verify you have the following items:

- You have Azure CLI version 2.29.0 or later installed and configured. To find the version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

with a minimum version of[1.18.1](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1181)or. With the Azure CLI and the Azure PowerShell module, these two commands are included and automatically managed. Meaning, they're upgraded by default and running`kubelogin`

`az aks install-cli`

isn't required or recommended. If you're using an automated pipeline, you need to manage upgrades for the correct or latest version. The difference between the minor versions of Kubernetes and`kubectl`

shouldn't be more than*one*version. Otherwise, authentication issues occur on the wrong version. - If you're using
[helm](https://github.com/helm/helm), you need a minimum version of helm 3.3. - This configuration requires you have a Microsoft Entra group for your cluster. This group is registered as an admin group on the cluster to grant admin permissions. If you don't have an existing Microsoft Entra group, you can create one using the
command.`az ad group create`


Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution

`PATH`

. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded `kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.## Enable the integration on your AKS cluster

### Create a new cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create an AKS cluster and enable administration access for your Microsoft Entra group using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-aad \ --aad-admin-group-object-ids <id> \ --aad-tenant-id <id> \ --generate-ssh-keys`

A successful creation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body.

`"AADProfile": { "adminGroupObjectIds": [ "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb" ], "clientAppId": null, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee" }`


### Use an existing cluster

Enable AKS-managed Microsoft Entra integration on your existing Kubernetes RBAC enabled cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. Make sure to set your admin group to keep access on your cluster.

```
az aks update \
--resource-group MyResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id-1>,<id-2> \
--aad-tenant-id <id>
```


A successful activation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


### Migrate legacy cluster to integration

If your cluster uses legacy Microsoft Entra integration, you can upgrade to AKS-managed Microsoft Entra integration through the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

Warning

Free tier clusters might experience API server downtime during the upgrade. We recommend upgrading during your nonbusiness hours.
After the upgrade, the `kubeconfig`

content changes. You need to run `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

to merge the new credentials into the `kubeconfig`

file.

```
az aks update \
--resource-group myResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id> \
--aad-tenant-id <id>
```


A successful migration of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


## Access your enabled cluster

Get the user credentials to access your cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myManagedCluster`

Follow your sign in instructions.

Set

`kubelogin`

to use the Azure CLI.`kubelogin convert-kubeconfig -l azurecli`

View the nodes in the cluster with the

`kubectl get nodes`

command.`kubectl get nodes`


## Non-interactive sign-in with kubelogin

There are some non-interactive scenarios that don't support `kubectl`

. In these cases, use [ kubelogin](https://github.com/Azure/kubelogin) to connect to the cluster with a non-interactive service principal credential to perform continuous integration pipelines.

Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution PATH. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded

`kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.When getting the `clusterUser`

credential, you can use the `format`

query parameter to overwrite the default behavior. You can set the value to `azure`

to use the original `kubeconfig`

format:

```
az aks get-credentials --format azure
```


If your Microsoft Entra integrated cluster uses Kubernetes version 1.24 or lower, you need to manually convert the `kubeconfig`

format.

```
export KUBECONFIG=/path/to/kubeconfig
kubelogin convert-kubeconfig
```


If you receive the message **error: The Azure auth plugin has been removed.**, you need to run the command `kubelogin convert-kubeconfig`

to convert the `kubeconfig`

format manually. For more information, see [Azure Kubelogin Known Issues](https://azure.github.io/kubelogin/known-issues.html).

## Troubleshoot access issues

Important

The step described in this section suggests an alternative authentication method compared to the normal Microsoft Entra group authentication. Use this option only in an emergency.

If you lack administrative access to a valid Microsoft Entra group, you can follow this workaround. Sign in with an account that is a member of the [Azure Kubernetes Service Cluster Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) role and grant your group or tenant admin credentials to access your cluster.

## Next steps

- Learn about
[Microsoft Entra integration with Kubernetes RBAC](azure-ad-rbac). - Learn more about
[AKS and Kubernetes identity concepts](concepts-identity). - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS. - Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create AKS-managed Microsoft Entra ID enabled clusters.
