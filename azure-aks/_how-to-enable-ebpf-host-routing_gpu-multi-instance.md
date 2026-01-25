---
merged_at: 2026-01-25T12:25:33.925576
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: how-to-enable-ebpf-host-routing.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/how-to-enable-ebpf-host-routing -->

# Enable eBPF Host Routing with Advanced Container Networking Services (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

eBPF Host Routing with Advanced Container Networking Services is currently in PREVIEW.

See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

This article shows you how to enable eBPF Host Routing with Advanced Container Networking Services (ACNS) on Azure Kubernetes Service (AKS) clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/free/?WT.mc_id=A261C142F)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.71.0. To find the version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).eBPF Host Routing is only supported with Azure CNI powered by Cilium. See

[Configure Azure CNI Powered by Cilium](/en-us/azure/aks/azure-cni-powered-by-cilium)for more information on managed Cilium clusters.Review the

[Limitations](container-network-performance-ebpf-host-routing#limitations)section for node requirements and compatibility with existing iptable rules.

### Install the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install or update the Azure CLI preview extension using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

The minimum version of the aks-preview Azure CLI extension is `14.0.0b6`


```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the `AdvancedNetworkingPerformancePreview`

feature flag

Register the `AdvancedNetworkingPerformancePreview`

feature flag using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command.

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingPerformancePreview"
```


Verify successful registration using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for the registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingPerformancePreview"
```


Once the feature shows `Registered`

, refresh the registration of the `Microsoft.ContainerService`

resource provider using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

### Enable Advanced Container Networking Services and eBPF Host Routing

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).**Container Network Performance:**Improves latency and throughput for pod network traffic. To learn more visit[Container Network Performance](advanced-container-networking-services-overview#container-network-performance)

Note

Clusters with the Cilium data plane support Container Network Performance with eBPF Host Routing starting with Kubernetes version 1.33.

Warning

The only compatible OS versions are Ubuntu 24.04 or Azure Linux 3.0.

Create an Azure resource group for the cluster using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
export LOCATION="<location>"
az group create --location $LOCATION --name <resourcegroup-name>
```


Create a new AKS cluster with eBPF Host Routing by enabling ACNS through `--enable-acns`

and setting the acceleration mode with `--acns-datapath-acceleration-mode BpfVeth`

.

```
# Set environment variables for the AKS cluster name and resource group. Make sure to replace the placeholders with your own values.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<resourcegroup-name>"
export LOCATION="<location>"
export OS_SKU="<os-sku>" # Use AzureLinux or Ubuntu2404
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--location $LOCATION \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--kubernetes-version 1.33 \
--os-sku $OS_SKU \
--enable-acns \
--acns-datapath-acceleration-mode BpfVeth \
--generate-ssh-keys
```


### Enable eBPF Host Routing with Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with `--acns-datapath-acceleration-mode BpfVeth`

to enable Advanced Container Networking Services features that includes [Container Network Observability](advanced-container-networking-services-overview#container-network-observability),

[Container Network Security](advanced-container-networking-services-overview#container-network-security), and

[Container Network Performance](advanced-container-networking-services-overview#container-network-performance).

Note

Enabling eBPF Host Routing on an existing cluster may disrupt existing connections.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-datapath-acceleration-mode BpfVeth
```


## Disabling eBPF Host Routing on an existing cluster

eBPF Host Routing can be disabled independently without affecting other ACNS features. To disable it, set the flag `--acns-datapath-acceleration-mode=None`

.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-datapath-acceleration-mode None
```


## Related content

- Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services.


---

<!-- DOCUMENTO FUSIONADO: gpu-multi-instance.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/gpu-multi-instance -->

# Create a multi-instance GPU node pool in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Certain NVIDIA GPUs can be divided in up to seven independent instances. Each instance has its own Stream Multiprocessor (SM), which is responsible for executing instructions in parallel, and GPU memory. For more information on GPU partitioning, see [NVIDIA MIG](https://www.nvidia.com/en-us/technologies/multi-instance-gpu/).

This article walks you through how to create a multi-instance GPU node pool using a MIG-compatible VM size in an Azure Kubernetes Service (AKS) cluster.

## Prerequisites and limitations

- An Azure account with an active subscription. If you don't have one, you can
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - The Kubernetes command-line client,
[kubectl](https://kubernetes.io/docs/reference/kubectl/), installed and configured. If you use Azure Cloud Shell,`kubectl`

is already installed. If you want to install it locally, you can use thecommand.`az aks install-cli`

- Helm v3 installed and configured. For more information, see
[Installing Helm](https://helm.sh/docs/intro/install/). - Multi-instance GPU is currently supported on the
`Standard_NC40ads_H100_v5`

,`Standard_ND96isr_H100_v5`

, and A100 GPU VM sizes on AKS.

## GPU instance profiles

GPU instance profiles define how GPUs are partitioned. The following table shows the available GPU instance profile for the `Standard_ND96asr_v4`

:

| Profile name | Fraction of SM | Fraction of memory | Number of instances created |
|---|---|---|---|
| MIG 1g.5gb | 1/7 | 1/8 | 7 |
| MIG 2g.10gb | 2/7 | 2/8 | 3 |
| MIG 3g.20gb | 3/7 | 4/8 | 2 |
| MIG 4g.20gb | 4/7 | 4/8 | 1 |
| MIG 7g.40gb | 7/7 | 8/8 | 1 |

As an example, the GPU instance profile of `MIG 1g.5gb`

indicates that each GPU instance has 1g SM (streaming multiprocessors) and 5gb memory. In this case, the GPU is partitioned into seven instances.

The available GPU instance profiles available for this VM size include `MIG1g`

, `MIG2g`

, `MIG3g`

, `MIG4g`

, and `MIG7g`

.

Important

You can't change the applied GPU instance profile after node pool creation.

## Create an AKS cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location southcentralus`

Create an AKS cluster using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --generate-ssh-keys`

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Create a multi-instance GPU node pool

You can use either the Azure CLI or an HTTP request to the ARM API to create the node pool.

Create a multi-instance GPU node pool using the

command and specify the GPU instance profile. The example below creates a node pool with the`az aks nodepool add`

`Standard_ND96asr_v4`

MIG-compatible GPU VM size.`az aks nodepool add \ --name aksMigNode \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --node-vm-size Standard_ND96asr_v4 \ --node-count 1 \ --gpu-instance-profile MIG1g`


## Determine multi-instance GPU (MIG) strategy

Before you install the NVIDIA plugins, you need to specify which multi-instance GPU (MIG) strategy to use for GPU partitioning: *Single strategy* or *Mixed strategy*. The two strategies don't affect how you execute CPU workloads, but how GPU resources are displayed.

**Single strategy**: The single strategy treats every GPU instance as a GPU. If you use this strategy, the GPU resources are displayed as`nvidia.com/gpu: 1`

.**Mixed strategy**: The mixed strategy exposes the GPU instances and the GPU instance profile. If you use this strategy, the GPU resource are displayed as`nvidia.com/mig1g.5gb: 1`

.

## Install the NVIDIA device plugin and GPU feature discovery (GFD) components

Set your MIG strategy as an environment variable. You can use either single or mixed strategy.

`# Single strategy export MIG_STRATEGY=single # Mixed strategy export MIG_STRATEGY=mixed`

Add the NVIDIA device plugin helm repository using the

`helm repo add`

and`helm repo update`

commands.`helm repo add nvdp https://nvidia.github.io/k8s-device-plugin helm repo update`

Install the NVIDIA device plugin using the

`helm install`

command.`helm install nvdp nvdp/nvidia-device-plugin \ --version=0.17.0 \ --set migStrategy=${MIG_STRATEGY} \ --set gfd.enabled=true \ --namespace nvidia-device-plugin \ --create-namespace`


Note

Helm installation of the NVIDIA device plugin consolidates the Kubernetes device plugin and GFD repositories. Separate helm installation of the GFD software component is not recommended when using AKS-managed multi-instance GPU.

## Confirm multi-instance GPU capability

Verify the

`kubectl`

connection to your cluster using the`kubectl get`

command to return a list of cluster nodes.`kubectl get nodes -o wide`

Confirm the node has multi-instance GPU capability using the

`kubectl describe node`

command. The following example command describes the node named*aksMigNode*, which uses MIG1g as the GPU instance profile.`kubectl describe node aksMigNode`

Your output should resemble the following example output:

`# Single strategy output Allocatable: nvidia.com/gpu: 56 # Mixed strategy output Allocatable: nvidia.com/mig-1g.5gb: 56`


## Schedule work

The following examples are based on CUDA base image **version 12.1.1** for Ubuntu **22.04**, tagged as `12.1.1-base-ubuntu22.04`

.

### Single strategy

Create a file named

`single-strategy-example.yaml`

and copy in the following manifest.`apiVersion: v1 kind: Pod metadata: name: nvidia-single spec: containers: - name: nvidia-single image: nvidia/cuda:12.1.1-base-ubuntu22.04 command: ["/bin/sh"] args: ["-c","sleep 1000"] resources: limits: "nvidia.com/gpu": 1`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f single-strategy-example.yaml`

Verify the allocated GPU devices using the

`kubectl exec`

command. This command returns a list of the cluster nodes.`kubectl exec nvidia-single -- nvidia-smi -L`

The following example resembles output showing successfully created deployments and services:

`GPU 0: NVIDIA A100 40GB PCIe (UUID: GPU-48aeb943-9458-4282-da24-e5f49e0db44b) MIG 1g.5gb Device 0: (UUID: MIG-fb42055e-9e53-5764-9278-438605a3014c) MIG 1g.5gb Device 1: (UUID: MIG-3d4db13e-c42d-5555-98f4-8b50389791bc) MIG 1g.5gb Device 2: (UUID: MIG-de819d17-9382-56a2-b9ca-aec36c88014f) MIG 1g.5gb Device 3: (UUID: MIG-50ab4b32-92db-5567-bf6d-fac646fe29f2) MIG 1g.5gb Device 4: (UUID: MIG-7b6b1b6e-5101-58a4-b5f5-21563789e62e) MIG 1g.5gb Device 5: (UUID: MIG-14549027-dd49-5cc0-bca4-55e67011bd85) MIG 1g.5gb Device 6: (UUID: MIG-37e055e8-8890-567f-a646-ebf9fde3ce7a)`


### Mixed strategy

Create a file named

`mixed-strategy-example.yaml`

and copy in the following manifest.`apiVersion: v1 kind: Pod metadata: name: nvidia-mixed spec: containers: - name: nvidia-mixed image: nvidia/cuda:12.1.1-base-ubuntu22.04 command: ["/bin/sh"] args: ["-c","sleep 100"] resources: limits: "nvidia.com/mig-1g.5gb": 1`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f mixed-strategy-example.yaml`

Verify the allocated GPU devices using the

`kubectl exec`

command. This command returns a list of the cluster nodes.`kubectl exec nvidia-mixed -- nvidia-smi -L`

The following example resembles output showing successfully created deployments and services:

`GPU 0: NVIDIA A100 40GB PCIe (UUID: GPU-48aeb943-9458-4282-da24-e5f49e0db44b) MIG 1g.5gb Device 0: (UUID: MIG-fb42055e-9e53-5764-9278-438605a3014c)`


Important

The `latest`

tag for CUDA images has been deprecated on Docker Hub. Please refer to [NVIDIA's repository](https://hub.docker.com/r/nvidia/cuda/tags) for the latest images and corresponding tags.

## Troubleshooting

If you don't see multi-instance GPU capability after creating the node pool, confirm the API version isn't older than *2021-08-01*.

## Next steps

To learn more about GPUs on Azure Kubernetes Service, see:
