---
merged_at: 2026-01-25T15:16:21.157662
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ___gpu-multi-instance_active-active-solution_use-trusted-launch___access-private_8e395d.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __gpu-multi-instance_active-active-solution_use-trusted-launch.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _gpu-multi-instance_active-active-solution.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: active-active-solution.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/active-active-solution -->

# Recommended active-active high availability solution overview for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create an application in Azure Kubernetes Service (AKS) and choose an Azure region during resource creation, it's a single-region app. In the event of a disaster that causes the region to become unavailable, your application also becomes unavailable. If you create an identical deployment in a secondary Azure region, your application becomes less susceptible to a single-region disaster, which guarantees business continuity, and any data replication across the regions lets you recover your last application state.

While there are multiple patterns that can provide recoverability for an AKS solution, this guide outlines the recommended active-active high availability solution for AKS. Within this solution, we deploy two independent and identical AKS clusters into two paired Azure regions with both clusters actively serving traffic.

Note

The following use case can be considered standard practice within AKS. It has been reviewed internally and vetted in conjunction with our Microsoft partners.

## Active-active high availability solution overview

This solution relies on two identical AKS clusters configured to actively serve traffic. You place a global traffic manager, such as [Azure Front Door](/en-us/azure/frontdoor/front-door-overview), in front of the two clusters to distribute traffic across them. You must consistently configure the clusters to host an instance of all applications required for the solution to function.

Availability zones are another way to ensure high availability and fault tolerance for your AKS cluster within the same region. Availability zones allow you to distribute your cluster nodes across multiple isolated locations within an Azure region. This way, if one zone goes down due to a power outage, hardware failure, or network issue, your cluster can continue to run and serve your applications. Availability zones also improve the performance and scalability of your cluster by reducing the latency and contention among nodes. To set up availability zones for your AKS cluster, you need to specify the zone numbers when creating or updating your node pools. For more information, see [What are Azure availability zones?](/en-us/azure/reliability/availability-zones-overview)

Note

Many regions support availability zones. Consider using regions with availability zones to provide more resiliency and availability for your workloads. For more information, see [Recover from a region-wide service disruption](/en-us/azure/architecture/resiliency/recovery-loss-azure-region).

## Scenarios and configurations

This solution is best implemented when hosting stateless applications and/or with other technologies also deployed across both regions, such as horizontal scaling. In scenarios where the hosted application is reliant on resources, such as databases, that are actively in only one region, we recommend instead implementing an [active-passive solution](active-passive-solution) for potential cost savings, as active-passive has more downtime than active-active.

## Components

The active-active high availability solution uses many Azure services. This section covers only the components unique to this multi-cluster architecture. For more information on the remaining components, see the [AKS baseline architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=%2Fazure%2Faks%2Ftoc.json&bc=%2Fazure%2Faks%2Fbreadcrumb%2Ftoc.json).

**Multiple clusters and regions**: You deploy multiple AKS clusters, each in a separate Azure region. During normal operations, your Azure Front Door configuration routes network traffic between all regions. If one region becomes unavailable, traffic routes to a region with the fastest load time for the user.

**Hub-spoke network per region**: A regional hub-spoke network pair is deployed for each regional AKS instance. [Azure Firewall Manager](/en-us/azure/firewall-manager/overview) policies manage the firewall policies across all regions.

**Regional key store**: You provision [Azure Key Vault](/en-us/azure/key-vault/general/overview) in each region to store sensitive values and keys specific to the AKS instance and to support services found in that region.

**Azure Front Door**: [Azure Front Door](/en-us/azure/frontdoor/front-door-overview) load balances and routes traffic to a regional [Azure Application Gateway](/en-us/azure/application-gateway/overview) instance, which sits in front of each AKS cluster. Azure Front Door allows for *layer seven* global routing.

**Log Analytics**: Regional [Log Analytics](/en-us/azure/azure-monitor/logs/log-analytics-overview) instances store regional networking metrics and diagnostic logs. A shared instance stores metrics and diagnostic logs for all AKS instances.

**Container Registry**: The container images for the workload are stored in a managed container registry. With this solution, a single [Azure Container Registry](/en-us/azure/container-registry/container-registry-intro) instance is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables you to replicate images to the selected Azure regions and provides continued access to images even if a region experiences an outage.

## Failover process

If a service or service component becomes unavailable in one region, traffic should be routed to a region where that service is available. A multi-region architecture includes many different failure points. In this section, we cover the potential failure points.

### Application Pods (Regional)

A Kubernetes deployment object creates multiple replicas of a pod (*ReplicaSet*). If one is unavailable, traffic is routed between the remaining replicas. The Kubernetes *ReplicaSet* attempts to keep the specified number of replicas up and running. If one instance goes down, a new instance should be recreated. [Liveness probes](/en-us/azure/container-instances/container-instances-liveness-probe) can check the state of the application or process running in the pod. If the pod is unresponsive, the liveness probe removes the pod, which forces the *ReplicaSet* to create a new instance.

For more information, see [Kubernetes ReplicaSet](https://kubernetes.io/docs/concepts/workloads/controllers/replicaset/).

### Application Pods (Global)

When an entire region becomes unavailable, the pods in the cluster are no longer available to serve requests. In this case, the Azure Front Door instance routes all traffic to the remaining health regions. The Kubernetes clusters and pods in these regions continue to serve requests. To compensate for increased traffic and requests to the remaining cluster, keep in mind the following guidance:

- Make sure network and compute resources are right sized to absorb any sudden increase in traffic due to region failover. For example, when using Azure Container Network Interface (CNI), make sure you have a subnet that can support all pod IPs with a spiked traffic load.
- Use the
[Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler)to increase the pod replica count to compensate for the increased regional demand. - Use the AKS
[Cluster Autoscaler](cluster-autoscaler)to increase the Kubernetes instance node counts to compensate for the increased regional demand.

### Kubernetes node pools (Regional)

Occasionally, localized failure can occur to compute resources, such as power becoming unavailable in a single rack of Azure servers. To protect your AKS nodes from becoming a single point regional failure, use [Azure Availability Zones](availability-zones). Availability zones ensure that AKS nodes in each availability zone are physically separated from those defined in another availability zones.

### Kubernetes node pools (Global)

In a complete regional failure, Azure Front Door routes traffic to the remaining healthy regions. Again, make sure to compensate for increased traffic and requests to the remaining cluster.

## Failover testing strategy

While there are no mechanisms currently available within AKS to take down an entire region of deployment for testing purposes, [Azure Chaos Studio](/en-us/azure/chaos-studio/chaos-studio-overview) offers the ability to create a chaos experiment on your cluster.

## Next steps

If you're considering a different solution, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: use-trusted-launch.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-trusted-launch -->

# Trusted Launch for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Trusted Launch](/en-us/azure/virtual-machines/trusted-launch) improves the security of generation 2 virtual machines (VMs) by protecting against advanced and persistent attack techniques. It enables administrators to deploy AKS nodes, which contain the underlying virtual machines, with verified and signed bootloaders, OS kernels, and drivers. By using secure and measured boot, administrators gain insights and confidence of the entire boot chain's integrity.

This article helps you understand this new feature, and how to implement it.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview

Trusted Launch is composed of several, coordinated infrastructure technologies that can be enabled independently. Each technology provides another layer of defense against sophisticated threats.

**vTPM**- Trusted Launch introduces a virtualized version of a hardware[Trusted Platform Module](/en-us/windows/security/information-protection/tpm/trusted-platform-module-overview)(TPM), compliant with the TPM 2.0 specification. It serves as a dedicated secure vault for keys and measurements. Trusted Launch provides your VM with its own dedicated TPM instance, running in a secure environment outside the reach of any VM. The vTPM enables[attestation](/en-us/windows/security/information-protection/tpm/tpm-fundamentals#measured-boot-with-support-for-attestation)by measuring the entire boot chain of your VM (UEFI, OS, system, and drivers). Trusted Launch uses the vTPM to perform remote attestation by the cloud. It's used for platform health checks and for making trust-based decisions. As a health check, Trusted Launch can cryptographically certify that your VM booted correctly. If the process fails, possibly because your VM is running an unauthorized component,[Microsoft Defender for Cloud](/en-us/azure/defender-for-cloud/defender-for-cloud-introduction)issues integrity alerts. The alerts include details on which components failed to pass integrity checks.**Secure Boot**- At the root of Trusted Launch is Secure Boot for your VM. This mode, which is implemented in platform firmware, protects against the installation of malware-based rootkits and boot kits. Secure Boot works to ensure that only signed operating systems and drivers can boot. It establishes a "root of trust" for the software stack on your VM. With Secure Boot enabled, all OS boot components (boot loader, kernel, kernel drivers) must be signed by trusted publishers. Both Windows and select Linux distributions support Secure Boot. If Secure Boot fails to authenticate an image signed by a trusted publisher, the VM isn't allowed to boot. For more information, see[Secure Boot](/en-us/windows-hardware/design/device-experiences/oem-secure-boot).

## Before you begin

- The Azure CLI version 2.66.0 or later. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

- Secure Boot requires signed boot loaders, OS kernels, and drivers.

## Limitations

- AKS supports Trusted Launch on kubernetes version 1.25.2 and higher.
- Trusted Launch only supports
[Azure Generation 2 VMs](/en-us/azure/virtual-machines/generation-2). - Node pools with Windows Server operating system aren't supported.
- Trusted Launch can't be enabled in the same node pool as
[FIPS](enable-fips-nodes),[Arm64](use-arm64-vms),[Pod Sandboxing](use-pod-sandboxing), or[Confidential VM](use-cvm). For more information, see[node images documentation](node-images). - Trusted Launch doesn't support virtual node.
- Availability sets aren't supported, only Virtual Machine Scale Sets.
- To enable Secure Boot on GPU node pools, you need to skip installing the GPU driver. For more information, see
[Skip GPU driver installation](gpu-cluster#skip-gpu-driver-installation). - Ephemeral OS disks can be created with trusted Launch and all regions are supported. However, not all virtual machines sizes are supported. For more information, see
[Trusted Launch ephemeral OS sizes](/en-us/azure/virtual-machines/ephemeral-os-disks#trusted-launch-for-ephemeral-os-disks). [Flatcar Container Linux for AKS](flatcar-container-linux-for-aks)doesn't support Trusted Launch on AKS.

## Create an AKS cluster with Trusted Launch enabled

When creating a cluster, enabling vTPM or Secure Boot automatically sets up your node pools to use the customized Trusted Launch image. This image is specifically configured to support the security features enabled by Trusted Launch.

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command. Before running the command, review the following parameters:**--name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--resource-group**: Enter the name of an existing resource group to host the AKS cluster resource.**--enable-secure-boot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example creates a cluster named

*myAKSCluster*with one node in the*myResourceGroup*, and enables Secure Boot and vTPM:`az aks create \ --name myAKSCluster \ --resource-group myResourceGroup \ --node-count 1 \ --enable-secure-boot \ --enable-vtpm \ --generate-ssh-keys`

Run the following command to get access credentials for the Kubernetes cluster. Use the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command and replace the values for the cluster name and the resource group name.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Add a node pool with Trusted Launch enabled

When you create a node pool, enabling vTPM or Secure Boot automatically sets up your node pools to use the customized Trusted Launch image. This image is specifically configured to support the security features enabled by Trusted Launch.

Add a node pool with Trusted Launch enabled using the

command. Before running the command, review the following parameters:`az aks nodepool add`

**--cluster-name**: Enter the name of the AKS cluster.**--resource-group**: Enter the name of an existing resource group to host the AKS cluster resource.**--name**: Enter a unique name for the node pool. The name of a node pool can only contain lowercase alphanumeric characters and must begin with a lowercase letter. For Linux node pools, the length must be between 1-11 characters.**--node-count**: The number of nodes in the Kubernetes agent pool. Default is 3.**--enable-secure-boot**: Enables Secure Boot to authenticate image signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example deploys a node pool with vTPM and Secure Boot enabled on a cluster named

*myAKSCluster*with three nodes:`az aks nodepool add --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --node-count 3 --enable-vtpm --enable-secure-boot`

Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

- Node image version containing

Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Enable vTPM or secure boot on an existing Trusted Launch node pool

You can update an existing Trusted Launch node pool to enable vTPM or secure boot. The following scenarios are supported:

- When creating a node pool, you only specify
`--enable-secure-boot`

, you can run the update command to`--enable-vtpm`

- When creating a node pool, you only specify
`--enable-vtpm`

, you can run the update command to`--enable-secure-boot`


If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

- Node image version containing
Update a node pool with Trusted Launch enabled using the

command. Before running the command, review the following parameters:`az aks nodepool update`

**--resource-group**: Enter the name of an existing resource group hosting your existing AKS cluster.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter the name of your node pool, such as*mynodepool*.**--enable-secure-boot**: Enables Secure Boot to authenticate that the image was signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

Note

Secure Boot requires signed boot loaders, OS kernels, and drivers. If after enabling Secure Boot your nodes don't start, you can verify which boot components are responsible for Secure Boot failures within an Azure Linux Virtual Machine. See

[verify Secure Boot failures](/en-us/azure/virtual-machines/trusted-launch-faq#verify-secure-boot-failures).The following example updates the node pool

*mynodepool*on the*myAKSCluster*in the*myResourceGroup*, and enables vTPM. In this scenario, secure boot was enabled during node pool creation:`az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --enable-vtpm`

The following example updates the node pool

*mynodepool*on the*myAKSCluster*in the*myResourceGroup*, and enables secure boot. In this scenario, vTPM was enabled during node pool creation:`az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --enable-secure-boot`


Check that your node pool is using a Trusted Launch image.

Trusted Launch nodes have the following output:

- Node image version containing
`"TL"`

, such as`"AKSUbuntu-2204-gen2TLcontainerd"`

. `"Security-type"`

should be`"Trusted Launch"`

.

`kubectl get nodes kubectl describe node {node-name} | grep -e node-image-version -e security-type`

If your node pool doesn't currently have a Trusted Launch image, you won't be able to update the node pool to enable secure boot or vTPM.

- Node image version containing
Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "true", "enableSecureBoot": "true", } }`

Deploy your template with vTPM and secure boot enabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Assign pods to nodes with Trusted Launch enabled

You can constrain a pod and restrict it to run on a specific node or nodes, or preference to nodes with Trusted Launch enabled. You can control this using the following node pool selector in your pod manifest.

```
spec:
nodeSelector:
kubernetes.azure.com/security-type = "TrustedLaunch"
```


## Disable vTPM or secure boot on an existing Trusted Launch node pool

You can update an existing node pool to disable vTPM or secure boot. When this occurs, you'll still remain on the Trusted Launch image. You can re-enable vTPM or secure boot at any time by updating your node pool.

Update a node pool to disable secure boot or vTPM using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. Before running the command, review the following parameters:

**--resource-group**: Enter the name of an existing resource group hosting your existing AKS cluster.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter the name of your node pool, such as*mynodepool*.**--enable-secure-boot**: Enables Secure Boot to authenticate that the image was signed by a trusted publisher.**--enable-vtpm**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

To disable vTPM on an existing node pool:

```
az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --disable-vtpm
```


To disable secure boot on an existing node pool:

```
az aks nodepool update --cluster-name myCluster --resource-group myResourceGroup --name mynodepool --disable-secure-boot
```


Create a template with Trusted Launch parameters. Before creating the template, review the following parameters:

**enableSecureBoot**: Enables Secure Boot to authenticate an image signed by a trusted publisher.**enableVTPM**: Enables vTPM and performs attestation by measuring the entire boot chain of your VM.

In your template, provide values for

`enableVTPM`

and`enableSecureBoot`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters/agentPools`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "securityProfile": { "enableVTPM": "false", "enableSecureBoot": "false", } }`

Deploy your template with vTPM and secure boot disabled on your cluster. See

[Deploy an AKS cluster using an ARM template](/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template)for detailed instructions.

## Next steps

In this article, you learned how to enable Trusted Launch. Learn more about [Trusted Launch](/en-us/azure/virtual-machines/trusted-launch).


---

<!-- DOCUMENTO FUSIONADO: __access-private-cluster_istio-scale_use-managed-identity.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _access-private-cluster_istio-scale.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: access-private-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/access-private-cluster -->

# Access a private Azure Kubernetes Service (AKS) cluster using the command invoke or Run command feature

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you access a private Azure Kubernetes Service (AKS) cluster, you need to connect to the cluster from the cluster virtual network (VNet), a peered network, or a configured private endpoint. These approaches require extra configuration, such as setting up a VPN or Express Route.

With the Azure CLI, you can use `command invoke`

to access private clusters without the need to configure a VPN or Express Route. `command invoke`

allows you to remotely invoke commands, like `kubectl`

and `helm`

, on your private cluster through the Azure API without directly connecting to the cluster. The RBAC actions `Microsoft.ContainerService/managedClusters/runcommand/action`

and `Microsoft.ContainerService/managedClusters/commandResults/read`

control the permissions for using `command invoke`

.

With the Azure portal, you can use the `Run command`

feature to run commands on your private cluster. The `Run command`

feature uses the same `command invoke`

functionality to run commands on your cluster. The pod created by `Run command`

provides `kubectl`

and `helm`

for operating your cluster. `jq`

, `xargs`

, `grep`

, and `awk`

are available for Bash support.

Tip

You can use Azure Copilot to run `kubectl`

commands in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#run-cluster-commands).

## Prerequisites

**System and permission requirements**

| Requirement type | Specification | How to verify |
|---|---|---|
Azure CLI version |
2.24.0 or later | Use the
`az --version` |

**Private AKS cluster**[Create a private AKS cluster](private-clusters).**RBAC actions**`Microsoft.ContainerService/managedClusters/runcommand/action`

and `Microsoft.ContainerService/managedClusters/commandResults/read`

[Azure CLI command.](/en-us/cli/azure/role/assignment#az-role-assignment-list)`az role assignment list`

**Run command pod resource specifications**

| Resource type | Value | Impact |
|---|---|---|
CPU requests |
200m | Minimum CPU reserved for command pod |
Memory requests |
500Mi | Minimum memory reserved for command pod |
CPU limits |
500m | Maximum CPU available to command pod |
Memory limits |
1Gi | Maximum memory available to command pod |
Azure Resource Manager (ARM) API timeout |
60 seconds | Maximum time for pod scheduling |
Output size limit |
512kB | Maximum command output size |

## Limitations and considerations

**Design scope**

**Not for programmatic access**: Use Bastion, VPN, or ExpressRoute for automated API calls.**Pod scheduling dependency**: Requires sufficient cluster resources (see the[resource specifications](#prerequisites)).**Output limitations**:*exitCode*and*text*only, no API-level details.**Network constraints apply**: Subject to cluster networking and security restrictions.

**Potential failure points**

- Pod scheduling failure if nodes are resource-constrained.
- ARM API timeout (60 seconds) if pod can't be scheduled quickly.
- Output truncation if response exceeds 512kB limit.

## Use `command invoke`

on a private AKS cluster with the Azure CLI

Set environment variables for your resource group and cluster name to use in subsequent commands.

`export AKS_RESOURCE_GROUP="<resource-group-name>" export AKS_CLUSTER_NAME="<cluster-name>"`

These environment variables allow you to run AKS commands without having to rewrite their names.


### Use `command invoke`

to run a single command

Run a single command on your cluster using the

command and the`az aks command invoke`

`--command`

parameter to specify the command to run. The following example gets the pods in the`kube-system`

namespace.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "kubectl get pods -n kube-system"`


### Use `command invoke`

to run multiple commands

Run multiple commands on your cluster using the

command and the`az aks command invoke`

`--command`

parameter to specify the commands to run. The following example adds the Bitnami Helm chart repository, updates the repository, and installs the`nginx`

chart.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "helm repo add bitnami https://charts.bitnami.com/bitnami && helm repo update && helm install my-release bitnami/nginx"`


### Use `command invoke`

to run commands with an attached file

If you want to run a command with an attached file, the file must exist and be accessible in your current working directory. In the following example, we create a minimal deployment file for demonstration.

Create a Kubernetes manifest file named

`deployment.yaml`

. The following example deployment file deploys an`nginx`

pod.`cat <<EOF > deployment.yaml apiVersion: apps/v1 kind: Deployment metadata: name: nginx-demo spec: replicas: 1 selector: matchLabels: app: nginx-demo template: metadata: labels: app: nginx-demo spec: containers: - name: nginx image: nginx:1.21.6 ports: - containerPort: 80 EOF`

Apply the deployment file to your cluster using the

command with the`az aks command invoke`

`--file`

parameter to attach the file. The following example applies the`deployment.yaml`

file to the`default`

namespace.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "kubectl apply -f deployment.yaml -n default" \ --file deployment.yaml`


### Use `command invoke`

to run commands with all files in the current directory

Note

Use only small, necessary files to avoid exceeding system size limits.

In the following example, we create two minimal deployment files for demonstration.

Create two Kubernetes manifest files named

`deployment.yaml`

and`configmap.yaml`

. The following example deployment files deploy an`nginx`

pod and create a ConfigMap with a welcome message.`cat <<EOF > deployment.yaml apiVersion: apps/v1 kind: Deployment metadata: name: nginx-demo spec: replicas: 1 selector: matchLabels: app: nginx-demo template: metadata: labels: app: nginx-demo spec: containers: - name: nginx image: nginx:1.21.6 ports: - containerPort: 80 EOF cat <<EOF > configmap.yaml apiVersion: v1 kind: ConfigMap metadata: name: nginx-config data: welcome-message: "Hello from configmap" EOF`

Apply the deployment files to your cluster using the

command with the`az aks command invoke`

`--file`

parameter to attach the file. The following example applies the`deployment.yaml`

and`configmap.yaml`

files to the`default`

namespace.`az aks command invoke \ --resource-group $AKS_RESOURCE_GROUP \ --name $AKS_CLUSTER_NAME \ --command "kubectl apply -f deployment.yaml -f configmap.yaml -n default" \ --file deployment.yaml \ --file configmap.yaml`


## Use `Run command`

on a private AKS cluster in the Azure portal

You can use the following `kubectl`

commands with the `Run command`

feature:

`kubectl get nodes`

`kubectl get deployments`

`kubectl get pods`

`kubectl describe nodes`

`kubectl describe pod <pod-name>`

`kubectl describe deployment <deployment-name>`

`kubectl apply -f <file-name>`


### Use `Run command`

to run a single command

- In the Azure portal, navigate to your private cluster.
- From the service menu, under
**Kubernetes resources**, select**Run command**. - Enter the command you want to run and select
**Run**.

### Use `Run command`

to run commands with attached files

In the Azure portal, navigate to your private cluster.

From the service menu, under

**Kubernetes resources**, select**Run command**.Select

**Attach files**>**Browse for files**.Select the file or files you want to attach, and then select

**Attach**.Enter the command you want to run and select

**Run**.

## Disable `Run command`


You can disable the `Run command`

feature by setting [ .properties.apiServerAccessProfile.disableRunCommand to true](/en-us/rest/api/aks/managed-clusters/create-or-update).


## Troubleshoot `command invoke`

issues

For information on the most common issues with `az aks command invoke`

and how to fix them, see [Resolve az aks command invoke failures](/en-us/troubleshoot/azure/azure-kubernetes/resolve-az-aks-command-invoke-failures).

## Related content

In this article, you learned how to access a private cluster and run commands on that cluster. For more information on AKS clusters, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: istio-scale.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-scale -->

# Istio service mesh add-on performance and scaling

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Istio-based service mesh add-on is logically split into a control plane (`istiod`

) and a data plane. The data plane is composed of Envoy sidecar proxies inside workload pods. Istiod manages and configures these Envoy proxies. This article presents the performance of both the control and data plane for revision asm-1-19, including resource consumption, sidecar capacity, and latency overhead. Additionally, it provides suggestions for addressing potential strain on resources during periods of heavy load. This article also covers how to customize scaling for the control plane and gateways.

## Control plane performance

[Istiod’s CPU and memory requirements](https://istio.io/latest/docs/ops/deployment/performance-and-scalability/#control-plane-performance) correlate with the rate of deployment and configuration changes and the number of proxies connected. The scenarios tested were:

- Pod churn: examines the impact of pod churning on
`istiod`

. To reduce variables, only one service is used for all sidecars. - Multiple services: examines the impact of multiple services on the maximum sidecars Istiod can manage (sidecar capacity), where each service has
`N`

sidecars, totaling the overall maximum.

#### Test specifications

- One
`istiod`

instance with default settings - Horizontal pod autoscaling disabled
- Tested with two network plugins: Azure Container Networking Interface (CNI) Overlay and Azure CNI Overlay with Cilium
[(recommended network plugins for large scale clusters)](/en-us/azure/aks/azure-cni-overlay?tabs=kubectl#choosing-a-network-model-to-use) - Node SKU: Standard D16 v3 (16 vCPU, 64-GB memory)
- Kubernetes version: 1.28.5
- Istio revision: asm-1-19

### Pod churn

The [ClusterLoader2 framework](https://github.com/kubernetes/perf-tests/tree/master/clusterloader2#clusterloader) was used to determine the maximum number of sidecars Istiod can manage when there's sidecar churning. The churn percent is defined as the percent of sidecars churned down/up during the test. For example, 50% churn for 10,000 sidecars would mean that 5,000 sidecars were churned down, then 5,000 sidecars were churned up. The churn percents tested were determined from the typical churn percentage during deployment rollouts (`maxUnavailable`

). The churn rate was calculated by determining the total number of sidecars churned (up and down) over the actual time taken to complete the churning process.

#### Sidecar capacity and Istiod CPU and memory

**Azure CNI overlay**

| Churn (%) | Churn Rate (sidecars/sec) | Sidecar Capacity | Istiod Memory (GB) | Istiod CPU |
|---|---|---|---|---|
| 0 | -- | 25000 | 32.1 | 15 |
| 25 | 31.2 | 15000 | 22.2 | 15 |
| 50 | 31.2 | 15000 | 25.4 | 15 |

**Azure CNI overlay with Cilium**

| Churn (%) | Churn Rate (sidecars/sec) | Sidecar Capacity | Istiod Memory (GB) | Istiod CPU |
|---|---|---|---|---|
| 0 | -- | 30000 | 41.2 | 15 |
| 25 | 41.7 | 25000 | 36.1 | 16 |
| 50 | 37.9 | 25000 | 42.7 | 16 |

### Multiple services

The [ClusterLoader2 framework](https://github.com/kubernetes/perf-tests/tree/master/clusterloader2#clusterloader) was used to determine the maximum number of sidecars `istiod`

can manage with 1,000 services. The results can be compared to the 0% churn test (one service) in the pod churn scenario. Each service had `N`

sidecars contributing to the overall maximum sidecar count. The API Server resource usage was observed to determine if there was any significant stress from the add-on.

**Sidecar capacity**

| Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|
| 20000 | 20000 |

**CPU and memory**

| Resource | Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|---|
| API Server Memory (GB) | 38.9 | 9.7 |
| API Server CPU | 6.1 | 4.7 |
| Istiod Memory (GB) | 40.4 | 42.6 |
| Istiod CPU | 15 | 16 |

## Data plane performance

Various factors impact [sidecar performance](https://istio.io/latest/docs/ops/deployment/performance-and-scalability/#data-plane-performance) such as request size, number of proxy worker threads, and number of client connections. Additionally, any request flowing through the mesh traverses the client-side proxy and then the server-side proxy. Therefore, latency and resource consumption are measured to determine the data plane performance.

[ Fortio](https://fortio.org/) was used to create the load. The test was conducted with the

[Istio benchmark repository](https://github.com/istio/tools/tree/master/perf/benchmark#istio-performance-benchmarking)that was modified for use with the add-on.

#### Test specifications

- Tested with two network plugins: Azure CNI Overlay and Azure CNI Overlay with Cilium
[(recommended network plugins for large scale clusters)](/en-us/azure/aks/azure-cni-overlay?tabs=kubectl#choosing-a-network-model-to-use) - Node SKU: Standard D16 v5 (16 vCPU, 64-GB memory)
- Kubernetes version: 1.28.5
- Two proxy workers
- 1-KB payload
- 1,000 Queries per second (QPS) at varying client connections
`http/1.1`

protocol and mutual Transport Layer Security (TLS) enabled- 26 data points collected

#### CPU and memory

The memory and CPU usage for both the client and server proxy for 16 client connections and 1,000 QPS across all network plugin scenarios is roughly 0.4 vCPU and 72 MB.

#### Latency

The sidecar Envoy proxy collects raw telemetry data after responding to a client, which doesn't directly affect the request's total processing time. However, this process delays the start of handling the next request, contributing to queue wait times and influencing average and tail latencies. Depending on the traffic pattern, the actual tail latency varies.

The following results evaluate the impact of adding sidecar proxies to the data path, showcasing the P90 and P99 latency.

- Sidecar traffic path: client --> client-sidecar --> server-sidecar --> server
- Baseline traffic path: client --> server

A comparison of data plane latency performance across Istio add-on and AKS versions can be found [here](istio-latency).

| Azure CNI Overlay | Azure CNI Overlay with Cilium |
|---|---|
|

## Scaling

### Horizontal pod autoscaling customization

[Horizontal pod autoscaling (HPA)](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale/) is enabled for the `istiod`

and ingress/egress gateway deployments. The default configurations for `istiod`

and the gateways are:

- Min Replicas: 2
- Max Replicas: 5
- CPU Utilization: 80%

Note

To prevent conflicts with the `PodDisruptionBudget`

, the add-on does not allow setting the `minReplicas`

below the initial default of `2`

.

The following are the `istiod`

and ingress gateway HPA resources:

```
NAMESPACE NAME REFERENCE
aks-istio-ingress aks-istio-ingressgateway-external-asm-1-19 Deployment/aks-istio-ingressgateway-external-asm-1-19
aks-istio-ingress aks-istio-ingressgateway-internal-asm-1-19 Deployment/aks-istio-ingressgateway-internal-asm-1-19
aks-istio-system istiod-asm-1-19 Deployment/istiod-asm-1-19
```


The HPA configuration can be modified through patches and direct edits. Example:

```
kubectl patch hpa aks-istio-ingressgateway-external-asm-1-19 -n aks-istio-ingress --type merge --patch '{"spec": {"minReplicas": 3, "maxReplicas": 6}}'
```


Note

See the [Istio add-on upgrade documentation](istio-upgrade#minor-revision-upgrades-with-horizontal-pod-autoscaling-customizations) for details on how HPA settings are applied across both revisions during a canary upgrade.

## Service entry

Istio's ServiceEntry custom resource definition enables adding other services into the Istio’s internal service registry. A [ServiceEntry](https://istio.io/latest/docs/reference/config/networking/service-entry/) allows services already in the mesh to route or access the services specified. However, the configuration of multiple ServiceEntries with the `resolution`

field set to DNS can cause a [heavy load on Domain Name System (DNS) servers](https://preliminary.istio.io/latest/docs/ops/configuration/traffic-management/dns/#proxy-dns-resolution). The following suggestions can help reduce the load:

- Switch to
`resolution: NONE`

to avoid proxy DNS lookups entirely. Suitable for most use cases. However, when using an[Istio add-on egress gateway](istio-deploy-egress), the ServiceEntry resolution must be set to`DNS`

. - Increase TTL (Time To Live) if you control the domains being resolved.
- Limit the ServiceEntry scope with
`exportTo`

.


---

<!-- DOCUMENTO FUSIONADO: use-managed-identity.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-managed-identity -->

# Use a managed identity in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides step-by-step instructions on how to enable and use a system-assigned, user-assigned, or pre-created kubelet managed identity in Azure Kubernetes Service (AKS).

## AKS managed identity prerequisites

Read the

[Overview of managed identities in Azure Kubernetes Service (AKS)](managed-identity-overview)to understand the different types of managed identities available in AKS and how you can use them to securely access Azure resources.Before running the examples in this article, set your subscription as the current active subscription using the

command.`az account set`

`az account set --subscription <subscription-id>`

Create an Azure resource group if you don't already have one by calling the

command.`az group create`

`az group create \ --name <resource-group-name> \ --location <location>`


### Azure CLI version minimum requirements

- Make sure you have Azure CLI version 2.23.0 or later installed. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - To
[use a pre-created kubelet managed identity](use-managed-identity#create-a-kubelet-managed-identity), you need Azure CLI version 2.26.0 or later installed. - To update an existing cluster to use a
[system-assigned managed identity](use-managed-identity#update-an-existing-aks-cluster-to-use-a-system-assigned-managed-identity)or[a user-assigned managed identity](use-managed-identity#update-an-existing-cluster-to-use-a-user-assigned-managed-identity), you need Azure CLI version 2.49.0 or later installed.

### Limitations

Moving or migrating a managed identity-enabled cluster to a different tenant isn't supported.

If the cluster has Microsoft Entra pod-managed identity (

`aad-pod-identity`

) enabled, Node-Managed Identity (NMI) pods modify the iptables of the nodes to intercept calls to the Azure Instance Metadata (IMDS) endpoint. This configuration means any request made to the IMDS endpoint is intercepted by NMI, even if a particular pod doesn't use`aad-pod-identity`

.The AzurePodIdentityException custom resource definition (CRD) can be configured to specify that requests to the IMDS endpoint that originate from a pod matching labels defined in the CRD should be proxied without any processing in NMI. Exclude the system pods with the

`kubernetes.azure.com/managedby: aks`

label in*kube-system*namespace in`aad-pod-identity`

by configuring the AzurePodIdentityException CRD. For more information, see[Use Microsoft Entra pod-managed identities in Azure Kubernetes Service](use-azure-ad-pod-identity).To configure an exception, install the

[mic-exception YAML](https://github.com/Azure/aad-pod-identity/blob/master/deploy/infra/mic-exception.yaml).AKS doesn't support the use of a system-assigned managed identity when using a custom private DNS zone.

The USDOD Central, USDOD East, and USGov Iowa regions in Azure US Government cloud don't support creating a cluster with a user-assigned managed identity.


A pre-created kubelet managed identity must be a user-assigned managed identity.

The China East and China North regions in Microsoft Azure operated by 21Vianet aren't supported.

Important

All Microsoft Defender for Cloud features will be officially retired in the Azure in China region on August 18, 2026. Due to this upcoming retirement, Azure in China customers are no longer able to onboard new subscriptions to the service. A new subscription is any subscription that was not already onboarded to the Microsoft Defender for Cloud service prior to August 18, 2025, the date of the retirement announcement. For more information on the retirement, see

[Microsoft Defender for Cloud Deprecation in Microsoft Azure Operated by 21Vianet Announcement](https://aka.ms/mdcretirementinchina).Customers should work with their account representatives for Microsoft Azure operated by 21Vianet to assess the impact of this retirement on their own operations.


### Update cluster considerations

When you update a cluster, consider the following information:

- An update only works if there's a VHD update to consume. If you're running the latest VHD, you need to wait until the next VHD is available in order to perform the update.
- The Azure CLI ensures your addon's permission is correctly set after migrating. If you're not using the Azure CLI to perform the migrating operation, you need to handle the addon identity's permission by yourself. For an example using an Azure Resource Manager (ARM) template, see
[Assign Azure roles using ARM templates](/en-us/azure/role-based-access-control/role-assignments-template). - If your cluster was using
`--attach-acr`

to pull from images from Azure Container Registry (ACR), you need to run the`az aks update --resource-group <resource-group-name> --name <aks-cluster-name> --attach-acr <acr-resource-id>`

command after updating your cluster to let the newly created kubelet used for managed identity get the permission to pull from ACR. Otherwise, you won't be able to pull from ACR after the update.

## Enable a system-assigned managed identity on an AKS cluster

### Enable a system-assigned managed identity on a new AKS cluster

A system-assigned managed identity is enabled by default when you create a new AKS cluster.

Create an AKS cluster using the

command.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --generate-ssh-keys`


### Update an existing AKS cluster to use a system-assigned managed identity

Update an existing AKS cluster from a service principal to a system-assigned managed identity using the

command with the`az aks update`

`--enable-managed-identity`

parameter.`az aks update \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --enable-managed-identity`

After you update the cluster to use a system-assigned managed identity instead of a service principal, the control plane and pods use the system-assigned managed identity for authorization when accessing other services in Azure. Kubelet continues using a service principal until you also upgrade your agent pool. You can use the

`az aks nodepool upgrade --resource-group <resource-group-name> --cluster-name <aks-cluster-name> --name <node-pool-name> --node-image-only`

command on your nodes to update to a managed identity. A node pool upgrade causes downtime for your AKS cluster as the nodes in the node pools are cordoned, drained, and reimaged.

## Get the principal ID of a system-assigned managed identity

Get the principal ID for the cluster's system-assigned managed identity using the

command.`az aks show`

`CLIENT_ID=$(az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query identity.principalId \ --output tsv)`


## Add a role assignment for a system-assigned managed identity

Assign an Azure RBAC role to the system-assigned managed identity using the

command.`az role assignment create`

For a VNet, attached Azure disk, static IP address, or route table outside the default worker node resource group, you need to assign the

`Network Contributor`

role on the custom resource group.The following example assigns the

**Network Contributor**role to the system-assigned managed identity. The role assignment is scoped to the resource group that contains the VNet.`az role assignment create \ --assignee <client-id> \ --role "Network Contributor" \ --scope <custom-resource-group-id>`

Note

It can take up to 60 minutes for the permissions granted to your cluster's managed identity to propagate.


## Create a user-assigned managed identity

If you don't yet have a user-assigned managed identity resource, create one using the

command.`az identity create`

`az identity create \ --name <identity-name> \ --resource-group <resource-group-name>`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>", "location": "<location>", "name": "<identity-name>", "principalId": "<principal-id>", "resourceGroup": "<resource-group-name>", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


## Get the principal ID of the user-assigned managed identity

Get the principal ID of the user-assigned managed identity using the

command.`az identity show`

`CLIENT_ID=$(az identity show \ --name <identity-name> \ --resource-group <resource-group-name> \ --query principalId \ --output tsv)`


## Get the resource ID of the user-assigned managed identity

Get the resource ID of the user-assigned managed identity using the

command.`az identity show`

`RESOURCE_ID=$(az identity show \ --name <identity-name> \ --resource-group <resource-group-name> \ --query id \ --output tsv)`


## Assign an Azure RBAC role to the user-assigned managed identity

Add a role assignment for the user-assigned managed identity using the

command.`az role assignment create`

The following example assigns the

**Key Vault Secrets User**role to the user-assigned managed identity to grant it permissions to access secrets in a key vault. The role assignment is scoped to the key vault resource:`az role assignment create \ --assignee <client-id> \ --role "Key Vault Secrets User" \ --scope "<keyvault-resource-id>"`

Note

It can take up to 60 minutes for the permissions granted to your cluster's managed identity to propagate.


## Enable a user-assigned managed identity on an AKS cluster

### Enable a user-assigned managed identity on a new AKS cluster

Create an AKS cluster with the user-assigned managed identity using the

command. Include the`az aks create`

`--assign-identity`

parameter and pass in the resource ID for the user-assigned managed identity:`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --network-plugin azure \ --vnet-subnet-id <vnet-subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 \ --assign-identity $RESOURCE_ID \ --generate-ssh-keys`


### Update an existing cluster to use a user-assigned managed identity

Update an existing cluster to use a user-assigned managed identity using the

command. Include the`az aks update`

`--assign-identity`

parameter and pass in the resource ID for the user-assigned managed identity:`az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --enable-managed-identity \ --assign-identity $RESOURCE_ID`

The output for a successful cluster update to use a user-assigned managed identity should resemble the following example output:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } },`

Note

Migrating a managed identity for the control plane from system-assigned to user-assigned doesn't result in any downtime for control plane and agent pools. Control plane components continue to the old system-assigned identity for up to several hours, until the next token refresh.


## Determine which type of managed identity a cluster is using

Verify which type of managed identity your cluster is using with the

command.`az aks show`

`az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query identity.type \ --output tsv`

If the cluster is using a managed identity, the value of the

*type*property will be either**SystemAssigned**or**UserAssigned**.If the cluster is using a service principal, the value of the

*type*property will be null. Consider upgrading your cluster to use a managed identity.

## Create a kubelet managed identity

If you don't have a kubelet managed identity, create one using the

command.`az identity create`

`az identity create \ --name <kubelet-identity-name> \ --resource-group <resource-group-name>`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>", "location": "<location>", "name": "<kubelet-identity-name>", "principalId": "<principal-id>", "resourceGroup": "<resource-group-name>", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


## Assign an RBAC role to the kubelet managed identity

Assign the

`acrpull`

role on the kubelet managed identity using thecommand.`az role assignment create`

`az role assignment create \ --assignee <kubelet-client-id> \ --role "acrpull" \ --scope "<acr-registry-id>"`


## Enable a kubelet managed identity on an AKS cluster

### Enable a kubelet managed identity on a new AKS cluster

Create an AKS cluster with your existing identities using the

command.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --network-plugin azure \ --vnet-subnet-id <vnet-subnet-id> \ --dns-service-ip 10.2.0.10 \ --service-cidr 10.2.0.0/24 \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id> \ --generate-ssh-keys`

A successful AKS cluster creation using a kubelet managed identity should result in output similar to the following:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } }, "identityProfile": { "kubeletidentity": { "clientId": "<client-id>", "objectId": "<object-id>", "resourceId": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>" } },`


### Update an existing cluster to use a kubelet managed identity

To update an existing cluster to use the kubelet managed identity, first get the current control plane managed identity for your AKS cluster.

Warning

Updating the kubelet managed identity upgrades your AKS cluster's node pools, make sure you have the right availability configurations, such as Pod Disruption Budgets, configured before executing this to avoid workload disruption or execute this during a maintenance window.

Confirm your AKS cluster is using the user-assigned managed identity using the

command.`az aks show`

`az aks show \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --query "servicePrincipalProfile"`

If your cluster is using a managed identity, the output shows

`clientId`

with a value of**msi**. A cluster using a service principal shows an object ID. For example:`# The cluster is using a managed identity. { "clientId": "msi" }`

After confirming your cluster is using a managed identity, find the managed identity's resource ID using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --query "identity"`

For a user-assigned managed identity, your output should look similar to the following example output:

`{ "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": <identity-resource-id> "clientId": "<client-id>", "principalId": "<principal-id>" },`

Update your cluster with your existing identities using the

command. Provide the resource ID of the user-assigned managed identity for the control plane for the`az aks update`

`assign-identity`

argument. Provide the resource ID of the kubelet managed identity for the`assign-kubelet-identity`

argument.`az aks update \ --resource-group <resource-group-name> \ --name <aks-cluster-name> \ --enable-managed-identity \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id>`

Your output for a successful cluster update using your own kubelet managed identity should resemble the following example output:

`"identity": { "principalId": null, "tenantId": null, "type": "UserAssigned", "userAssignedIdentities": { "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<identity-name>": { "clientId": "<client-id>", "principalId": "<principal-id>" } } }, "identityProfile": { "kubeletidentity": { "clientId": "<client-id>", "objectId": "<object-id>", "resourceId": "/subscriptions/<subscription-id>/resourcegroups/<resource-group-name>/providers/Microsoft.ManagedIdentity/userAssignedIdentities/<kubelet-identity-name>" } },`


## Get the properties of the kubelet managed identity

Get the properties of the kubelet managed identity using the

command and query on the`az aks show`

`identityProfile.kubeletidentity`

property.`az aks show \ --name <aks-cluster-name> \ --resource-group <resource-group-name> \ --query "identityProfile.kubeletidentity"`


## Next steps

- Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create a managed identity-enabled cluster. - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS.


---

<!-- DOCUMENTO FUSIONADO: ___private-apiserver-vnet-integration-cluster_node-autoprovision-networking__nod_0f30c4.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __private-apiserver-vnet-integration-cluster_node-autoprovision-networking__node_efea80.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _private-apiserver-vnet-integration-cluster_node-autoprovision-networking.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: private-apiserver-vnet-integration-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/private-apiserver-vnet-integration-cluster -->

# Connect to an API Server VNet Integration cluster by using Azure Private Link

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

API Server VNet Integration lets you place the control‑plane IP inside your own VNet. The pattern described here extends that capability to more VNets by chaining Private Link. It's useful for hub‑and‑spoke topologies, dedicated build networks, or jump‑host VNets that must administer production clusters without opening the API server to the public internet.

This article applies **only to clusters that are created with API Server VNet Integration** and shows you how to:

- Deploy a
**private**AKS cluster with API Server VNet Integration. - Expose the API server through a
**Private Link Service (PLS)**inside the cluster virtual network. - Create a
**Private Endpoint (PE)**in a different virtual network. - Configure
**private DNS**so Kubernetes tools resolve the cluster’s private FQDN inside the remote network.

For private clusters that **do not** use API Server VNet Integration, see [Create a private AKS cluster](private-clusters).

## Region availability

API Server VNet Integration is currently available in a subset of Azure regions and is subject to regional capacity limits. Before you begin, confirm that your target region is supported. For more information, see [API Server VNet Integration](api-server-vnet-integration).

## Prerequisites

| Requirement | Minimum |
|---|---|
| Azure CLI | 2.73.0 |
| Permissions | Contributor + Network Contributor on both subscriptions |

If you use custom DNS servers, add Azure’s virtual IP **168.63.129.16** as an upstream forwarder.

## Set environment variables

Set the following environment variables for use throughout this article. Feel free to replace the placeholder values with your own.

```
LOCATION="westus3"
# Resource groups
AKS_RG="aks-demo-rg"
REMOTE_RG="client-demo-rg"
# AKS cluster
AKS_CLUSTER="aks-private"
AKS_SUBNET="aks-subnet"
# Private Link Service
PLS_NAME="apiserver-pls"
PLS_SUBNET="pls-subnet"
PLS_PREFIX="10.225.0.0/24"
# Remote VNet
REMOTE_VNET="client-vnet"
REMOTE_SUBNET="client-subnet"
REMOTE_VNET_PREFIX="192.168.0.0/16"
REMOTE_SUBNET_PREFIX="192.168.1.0/24"
PE_NAME="aks-pe"
PE_CONN_NAME="aks-pe-conn"
# DNS
DNS_ZONE="private.${LOCATION}.azmk8s.io"
DNS_LINK="dns-link"
```


## Create resource groups

```
# Create resource groups for the AKS cluster
az group create --name $AKS_RG --location $LOCATION
# Create a resource group for the remote VNet
az group create --name $REMOTE_RG --location $LOCATION
```


## Deploy a private cluster with API Server VNet Integration

Important

API Server VNet Integration requires its own subnet. If you don't supply one, AKS automatically creates it in the node resource group.

```
az aks create \
--name $AKS_CLUSTER \
--resource-group $AKS_RG \
--location $LOCATION \
--enable-private-cluster \
--enable-apiserver-vnet-integration
```


After the cluster finishes provisioning, capture the autogenerated node resource group, cluster VNet name, and private FQDN label:

```
AKS_NODE_RG=$(az aks show -g $AKS_RG -n $AKS_CLUSTER --query nodeResourceGroup -o tsv)
AKS_VNET=$(az network vnet list --resource-group $AKS_NODE_RG --query '[0].name' -o tsv)
DNS_RECORD=$(az aks show -g $AKS_RG -n $AKS_CLUSTER --query privateFqdn -o tsv | cut -d'.' -f1,2)
FRONTEND_IP_CONFIG_ID=$(az network lb show \
--name kube-apiserver \
--resource-group $AKS_NODE_RG \
--query "frontendIPConfigurations[0].id" \
-o tsv)
```


## Create a Private Link Service (PLS) in the AKS cluster VNet

Add a dedicated subnet for the PLS and disable network policies, which aren't supported on Private Link subnets.

Create the PLS and point it to the kube‑apiserver internal load balancer that AKS created for the control plane.

```
# Subnet for the PLS
az network vnet subnet create \
--name $PLS_SUBNET \
--vnet-name $AKS_VNET \
--resource-group $AKS_NODE_RG \
--address-prefixes $PLS_PREFIX \
--disable-private-link-service-network-policies
# PLS pointing to the API‑server ILB
az network private-link-service create \
--name $PLS_NAME \
--resource-group $AKS_NODE_RG \
--vnet-name $AKS_VNET \
--subnet $PLS_SUBNET \
--lb-frontend-ip-configs $FRONTEND_IP_CONFIG_ID \
--location $LOCATION
```


## Create a PrivateEndpoint (PE) in the remote VNet

```
# Remote VNet and subnet
az network vnet create \
--name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--location $LOCATION \
--address-prefixes $REMOTE_VNET_PREFIX
az network vnet subnet create \
--name $REMOTE_SUBNET \
--vnet-name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--address-prefixes $REMOTE_SUBNET_PREFIX
# Private Endpoint
PLS_ID=$(az network private-link-service show \
--name $PLS_NAME \
--resource-group $AKS_NODE_RG \
--query id -o tsv)
az network private-endpoint create \
--name $PE_NAME \
--resource-group $REMOTE_RG \
--vnet-name $REMOTE_VNET \
--subnet $REMOTE_SUBNET \
--private-connection-resource-id $PLS_ID \
--connection-name $PE_CONN_NAME \
--location $LOCATION
```


When the Private Endpoint finishes provisioning, note its network interface (NIC) ID so you can retrieve the allocated private IP address.

```
PE_NIC_ID=$(az network private-endpoint show \
--name $PE_NAME \
--resource-group $REMOTE_RG \
--query 'networkInterfaces[0].id' \
--output tsv)
# Capture the IP from the NIC
PE_IP=$(az network nic show \
--ids $PE_NIC_ID \
--query 'ipConfigurations[0].privateIPAddress' \
--output tsv)
```


## Configure private DNS

```
# Create or reuse the regional DNS zone
az network private-dns zone create \
--name $DNS_ZONE \
--resource-group $REMOTE_RG
az network private-dns record-set a create \
--name $DNS_RECORD \
--zone-name $DNS_ZONE \
--resource-group $REMOTE_RG
az network private-dns record-set a add-record \
--record-set-name $DNS_RECORD \
--zone-name $DNS_ZONE \
--resource-group $REMOTE_RG \
--ipv4-address $PE_IP
# Link zone to the remote VNet
REMOTE_VNET_ID=$(az network vnet show \
--name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--query id -o tsv)
az network private-dns link vnet create \
--name $DNS_LINK \
--zone-name $DNS_ZONE \
--resource-group $REMOTE_RG \
--virtual-network $REMOTE_VNET_ID \
--registration-enabled false
```


## Test the connection

If you try to test the connection locally, you might get an error because the DNS zone isn't linked to your local network.

```
az aks get-credentials --resource-group $AKS_RG --name $AKS_CLUSTER
kubectl get nodes
```


### Deploy a test VM in the remote VNet

To confirm the Private Endpoint path, deploy a test VM in the remote VNet and use it to connect to the AKS cluster.

```
# Create Network Security Group that allows inbound SSH (TCP 22)
az network nsg create \
--name "${REMOTE_VNET}-nsg" \
--resource-group $REMOTE_RG \
--location $LOCATION
az network nsg rule create \
--nsg-name "${REMOTE_VNET}-nsg" \
--resource-group $REMOTE_RG \
--name allow-ssh \
--priority 100 \
--access Allow \
--protocol Tcp \
--direction Inbound \
--source-address-prefixes '*' \
--destination-port-ranges 22
# Associate the NSG with the remote subnet
az network vnet subnet update \
--name $REMOTE_SUBNET \
--vnet-name $REMOTE_VNET \
--resource-group $REMOTE_RG \
--network-security-group "${REMOTE_VNET}-nsg"
# Create a small Ubuntu VM in that subnet (with a public IP for quick SSH)
az vm create \
--resource-group $REMOTE_RG \
--name test-vm \
--image Ubuntu2204 \
--size Standard_B2s \
--admin-username azureuser \
--generate-ssh-keys \
--vnet-name $REMOTE_VNET \
--subnet $REMOTE_SUBNET \
--public-ip-sku Standard
# Capture the public IP address
VM_PUBLIC_IP=$(az vm show -d -g $REMOTE_RG -n test-vm --query publicIps -o tsv)
```


### Connect to the VM and test the connection

```
ssh -i ~/.ssh/id_rsa azureuser@$VM_PUBLIC_IP
# Inside the VM
# Install Azure CLI
curl -sL https://aka.ms/InstallAzureCLIDeb | sudo bash
# Install kubectl
sudo az aks install-cli
# re-export the aks variables
export AKS_RG="aks-demo-rg"
export AKS_CLUSTER="aks-private"
# login to Azure. Follow the instructions to authenticate
az login
# Get the AKS credentials
az aks get-credentials --resource-group $AKS_RG --name $AKS_CLUSTER
# Test the connection
kubectl get nodes
# You should see the AKS nodes
# Exit the VM
exit
```


## Clean up resources

To avoid ongoing Azure charges, delete the resource groups using the [ az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name $AKS_RG --yes --no-wait
az group delete --name $REMOTE_RG --yes --no-wait
```


---

<!-- DOCUMENTO FUSIONADO: node-autoprovision-networking.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-autoprovision-networking -->

# Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of networking configuration requirements and recommendations for Azure Kubernetes Service (AKS) clusters using node auto-provisioning (NAP). It covers supported configurations, default subnet behavior, role-based access control (RBAC) setup, and classless inter-domain routing (CIDR) considerations.

For an overview of node auto-provisioning in AKS, see [Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning).

## Supported networking configurations for NAP

NAP supports the following networking configurations:

We recommend using Azure CNI with [Cilium](azure-cni-powered-by-cilium). Cilium provides advanced networking capabilities and is optimized for performance with NAP.

### Unsupported networking configurations for NAP

NAP doesn't support the following networking configurations:

- Calico network policy
- Dynamic IP allocation

## Subnet configurations for NAP

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects. You can use [ AKSNodeClass](node-auto-provisioning-aksnodeclass) resources to specify custom subnet configurations for NAP nodes in your node pools by setting the optional

`vnetSubnetID`

field, and Karpenter uses the subnet you specify for node provisioning. If you don't specify a subnet, Karpenter uses the default subnet configured during Karpenter installation. This default subnet is typically the same subnet specified during AKS cluster creation with the `--vnet-subnet-id`

parameter in the `az aks create`

command.This approach allows you to have a mix of node classes, with some using custom subnets for specific workloads, and others using the cluster's default subnet configuration.

## Subnet drift behavior

Karpenter monitors subnet configuration changes and detects drift when the `vnetSubnetID`

in an `AKSNodeClass`

is modified. Understanding this behavior is critical when managing custom networking configurations.

**Modifying vnetSubnetID from one valid subnet to another valid subnet isn't a supported operation**. If you change the

`vnetSubnetID`

to point to a different valid subnet, Karpenter detects this as subnet drift and prevents node provisioning until the issue is resolved by reverting the `vnetSubnetID`

to the original subnet. This behavior ensures that nodes are only provisioned in the intended subnets, maintaining network integrity and security. However, there are exceptions to this rule. You can only modify the `vnetSubnetID`

in the following scenarios:- Correcting a malformed subnet ID that prevents node provisioning.
- Fixing an invalid subnet reference that causes configuration errors.
- Updating a subnet identifier that points to a nonexistent or inaccessible subnet.

## Understand AKS cluster Classless Inter-Domain Routing (CIDR) ranges

When configuring custom networking with `vnetSubnetID`

, you're responsible for understanding and managing your cluster's CIDR ranges to avoid network conflicts. Unlike traditional AKS node pools created through ARM templates, Karpenter applies custom resource definitions (CRDs) that provision nodes instantly without the extended validation that ARM provides.

### CIDR considerations for custom subnet configurations

When configuring `vnetSubnetID`

, you must:

**Verify CIDR compatibility**: Ensure custom subnets don't conflict with existing CIDR ranges.**Plan IP capacity**: Calculate required IP addresses for expected scaling.**Validate connectivity**: Test network routes and security group rules.**Monitor usage**: Track subnet utilization and plan for growth.**Document configuration**: Maintain records of network design decisions.

### Common CIDR conflicts

Be aware of the following common CIDR conflict scenarios when using custom subnets with NAP:

```
# Example conflict scenarios:
# Cluster Pod CIDR: 10.244.0.0/16
# Custom Subnet: 10.244.1.0/24 ❌ CONFLICT
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.0.10.0/24 ❌ CONFLICT
# Safe configuration:
# Cluster Pod CIDR: 10.244.0.0/16
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.1.0.0/24 ✅ NO CONFLICT
```


## RBAC setup for custom subnet configurations

When using custom subnet configurations with NAP, you need to ensure that Karpenter has the necessary permissions to read subnet information and join nodes to the specified subnets. This requires setting up appropriate RBAC permissions for the cluster's managed identity.

There are two main approaches to setting up these permissions: **Assign broad virtual network (VNet) permissions** or **Assign scoped subnet permissions**.

This approach is the most permissive and grants the cluster identity permissions to read and join any subnet within the main VNet and provides network contributor access.

Important

Investigate the "Network Contributor" role before applying this approach to your production cluster.

#### Benefits and considerations

The following table outlines the benefits and considerations of assigning broad VNet permissions:

| Benefits | Considerations |
|---|---|
| • Simplifies permission management. • Eliminates the need to update permissions when adding new subnets. • Works well for single-tenant environments. • Functions when a subscription reaches the maximum number of custom roles. |
• Provides broader permissions than strictly necessary. • Might not meet strict security requirements. |

#### Required permissions

To assign broad VNet permissions, grant the cluster's managed identity the following permissions on the VNet:

```
# Get your cluster's managed identity
CLUSTER_IDENTITY=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query identity.principalId -o tsv)
# Get your VNet resource ID
VNET_ID="/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$VNET_RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME"
# Assign Network Contributor role for subnet read/join operations
az role assignment create \
--assignee $CLUSTER_IDENTITY \
--role "Network Contributor" \
--scope $VNET_ID
```


For a complete example of setting up custom networking and assigning broad VNet permissions, see the [Custom VNET setup - Most permissive RBAC sample script](https://gist.github.com/Bryce-Soghigian/a4259d6224db0c55081718caa7b37268).

## Example custom subnet configurations

The following example shows how to configure a custom subnet for NAP nodes using the `vnetSubnetID`

field in an `AKSNodeClass`

resource:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: custom-networking
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME"
```


The following example shows how to use multiple node classes with different subnet configurations:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: frontend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$FRONTEND_SUBNET_NAME"
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: backend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$BACKEND_SUBNET_NAME"
```


## Bring your own CNI (BYO CNI) support policy

Karpenter for Azure allows bring your own Container Network Interface (BYO CNI) configurations, following the same support policy as AKS. This means that when using a custom CNI, troubleshooting support related to networking is out of scope of any service-level agreements or warranties.

### Support scope details

The following outlines what is and isn't supported when using BYO CNI with Karpenter:

**Supported**: Karpenter-specific functionality and integration issues when using bring-your-own (BYO) CNI configurations.**Not supported**: CNI-specific networking issues, configuration problems, or troubleshooting when using third-party CNI plugins.

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: _node-auto-provisioning-networking_csi-secrets-store-driver.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-auto-provisioning-networking.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-networking -->

# Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of networking configuration requirements and recommendations for Azure Kubernetes Service (AKS) clusters using node auto-provisioning (NAP). It covers supported configurations, default subnet behavior, role-based access control (RBAC) setup, and classless inter-domain routing (CIDR) considerations.

For an overview of node auto-provisioning in AKS, see [Overview of node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning).

## Supported networking configurations for NAP

NAP supports the following networking configurations:

We recommend using Azure CNI with [Cilium](azure-cni-powered-by-cilium). Cilium provides advanced networking capabilities and is optimized for performance with NAP.

### Unsupported networking configurations for NAP

NAP doesn't support the following networking configurations:

- Calico network policy
- Dynamic IP allocation

## Subnet configurations for NAP

NAP automatically deploys, configures, and manages Karpenter on your AKS clusters and is based on the open-source [Karpenter](https://karpenter.sh) and [AKS Karpenter provider](https://github.com/Azure/karpenter-provider-azure) projects. You can use [ AKSNodeClass](node-auto-provisioning-aksnodeclass) resources to specify custom subnet configurations for NAP nodes in your node pools by setting the optional

`vnetSubnetID`

field, and Karpenter uses the subnet you specify for node provisioning. If you don't specify a subnet, Karpenter uses the default subnet configured during Karpenter installation. This default subnet is typically the same subnet specified during AKS cluster creation with the `--vnet-subnet-id`

parameter in the `az aks create`

command.This approach allows you to have a mix of node classes, with some using custom subnets for specific workloads, and others using the cluster's default subnet configuration.

## Subnet drift behavior

Karpenter monitors subnet configuration changes and detects drift when the `vnetSubnetID`

in an `AKSNodeClass`

is modified. Understanding this behavior is critical when managing custom networking configurations.

**Modifying vnetSubnetID from one valid subnet to another valid subnet isn't a supported operation**. If you change the

`vnetSubnetID`

to point to a different valid subnet, Karpenter detects this as subnet drift and prevents node provisioning until the issue is resolved by reverting the `vnetSubnetID`

to the original subnet. This behavior ensures that nodes are only provisioned in the intended subnets, maintaining network integrity and security. However, there are exceptions to this rule. You can only modify the `vnetSubnetID`

in the following scenarios:- Correcting a malformed subnet ID that prevents node provisioning.
- Fixing an invalid subnet reference that causes configuration errors.
- Updating a subnet identifier that points to a nonexistent or inaccessible subnet.

## Understand AKS cluster Classless Inter-Domain Routing (CIDR) ranges

When configuring custom networking with `vnetSubnetID`

, you're responsible for understanding and managing your cluster's CIDR ranges to avoid network conflicts. Unlike traditional AKS node pools created through ARM templates, Karpenter applies custom resource definitions (CRDs) that provision nodes instantly without the extended validation that ARM provides.

### CIDR considerations for custom subnet configurations

When configuring `vnetSubnetID`

, you must:

**Verify CIDR compatibility**: Ensure custom subnets don't conflict with existing CIDR ranges.**Plan IP capacity**: Calculate required IP addresses for expected scaling.**Validate connectivity**: Test network routes and security group rules.**Monitor usage**: Track subnet utilization and plan for growth.**Document configuration**: Maintain records of network design decisions.

### Common CIDR conflicts

Be aware of the following common CIDR conflict scenarios when using custom subnets with NAP:

```
# Example conflict scenarios:
# Cluster Pod CIDR: 10.244.0.0/16
# Custom Subnet: 10.244.1.0/24 ❌ CONFLICT
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.0.10.0/24 ❌ CONFLICT
# Safe configuration:
# Cluster Pod CIDR: 10.244.0.0/16
# Service CIDR: 10.0.0.0/16
# Custom Subnet: 10.1.0.0/24 ✅ NO CONFLICT
```


## RBAC setup for custom subnet configurations

When using custom subnet configurations with NAP, you need to ensure that Karpenter has the necessary permissions to read subnet information and join nodes to the specified subnets. This requires setting up appropriate RBAC permissions for the cluster's managed identity.

There are two main approaches to setting up these permissions: **Assign broad virtual network (VNet) permissions** or **Assign scoped subnet permissions**.

This approach is the most permissive and grants the cluster identity permissions to read and join any subnet within the main VNet and provides network contributor access.

Important

Investigate the "Network Contributor" role before applying this approach to your production cluster.

#### Benefits and considerations

The following table outlines the benefits and considerations of assigning broad VNet permissions:

| Benefits | Considerations |
|---|---|
| • Simplifies permission management. • Eliminates the need to update permissions when adding new subnets. • Works well for single-tenant environments. • Functions when a subscription reaches the maximum number of custom roles. |
• Provides broader permissions than strictly necessary. • Might not meet strict security requirements. |

#### Required permissions

To assign broad VNet permissions, grant the cluster's managed identity the following permissions on the VNet:

```
# Get your cluster's managed identity
CLUSTER_IDENTITY=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query identity.principalId -o tsv)
# Get your VNet resource ID
VNET_ID="/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$VNET_RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME"
# Assign Network Contributor role for subnet read/join operations
az role assignment create \
--assignee $CLUSTER_IDENTITY \
--role "Network Contributor" \
--scope $VNET_ID
```


For a complete example of setting up custom networking and assigning broad VNet permissions, see the [Custom VNET setup - Most permissive RBAC sample script](https://gist.github.com/Bryce-Soghigian/a4259d6224db0c55081718caa7b37268).

## Example custom subnet configurations

The following example shows how to configure a custom subnet for NAP nodes using the `vnetSubnetID`

field in an `AKSNodeClass`

resource:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: custom-networking
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME"
```


The following example shows how to use multiple node classes with different subnet configurations:

```
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: frontend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$FRONTEND_SUBNET_NAME"
---
apiVersion: karpenter.azure.com/v1beta1
kind: AKSNodeClass
metadata:
name: backend-nodes
spec:
vnetSubnetID: "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/$RESOURCE_GROUP/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$BACKEND_SUBNET_NAME"
```


## Bring your own CNI (BYO CNI) support policy

Karpenter for Azure allows bring your own Container Network Interface (BYO CNI) configurations, following the same support policy as AKS. This means that when using a custom CNI, troubleshooting support related to networking is out of scope of any service-level agreements or warranties.

### Support scope details

The following outlines what is and isn't supported when using BYO CNI with Karpenter:

**Supported**: Karpenter-specific functionality and integration issues when using bring-your-own (BYO) CNI configurations.**Not supported**: CNI-specific networking issues, configuration problems, or troubleshooting when using third-party CNI plugins.

## Next steps

For more information on node auto-provisioning in AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: csi-secrets-store-driver.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-driver -->

# Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Key Vault provider for Secrets Store CSI Driver allows for the integration of an Azure Key Vault as a secret store with an Azure Kubernetes Service (AKS) cluster via a [CSI volume](https://kubernetes-csi.github.io/docs/).

## Features

- Mounts secrets, keys, and certificates to a pod using a CSI volume.
- Supports CSI inline volumes.
- Supports mounting multiple secrets store objects as a single volume.
- Supports pod portability with the
`SecretProviderClass`

CRD. - Supports Windows containers.
- Syncs with Kubernetes secrets.
- Supports autorotation of mounted contents and synced Kubernetes secrets.

## Limitations

- A container using a
`ConfigMap`

or`Secret`

as a`subPath`

volume mount does not receive automated updates when the secret is rotated. This is a Kubernetes limitation. To have the changes take effect, the application needs to reload the changed file by either watching for changes in the file system or by restarting the pod. For more information, see[Secrets Store CSI Driver known limitations](https://secrets-store-csi-driver.sigs.k8s.io/known-limitations.html#secrets-not-rotated-when-using-subpath-volume-mount). - The add-on creates a managed identity named
`azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Prerequisites

- If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Check that your version of the Azure CLI is 2.30.0 or later. If it's an earlier version,
[install the latest version](/en-us/cli/azure/install-azure-cli).

### Network

- If using network isolated clusters, it's recommended to
[set up private endpoint to access Azure Key Vault](/en-us/azure/key-vault/general/private-link-service). - If the cluster has outbound type
`userDefinedRouting`

and uses a firewall device that can control outbound traffic based on domain names, such as Azure Firewall, ensure the[required outbound network rules and FQDNs are allowed](outbound-rules-control-egress#azure-key-vault-provider-for-secrets-store-csi-driver). - If you're restricting Ingress to the cluster, make sure ports
**9808**and**8095**are open.

### Roles

- The identity used to with the
`SecretProviderClass`

needs to have`Key Vault Certificate User`

to access`key`

or`certificate`

[object types](/en-us/azure/key-vault/general/about-keys-secrets-certificates#object-types). - The identity used to with the
`SecretProviderClass`

needs to have`Key Vault Secrets User`

to access`secret`

[object type](/en-us/azure/key-vault/general/about-keys-secrets-certificates#object-types).

## Create an AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver support

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus2`

Create an AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver capability using the

command with the`az aks create`

`--enable-addons azure-keyvault-secrets-provider`

parameter. The add-on creates a user-assigned managed identity you can use to authenticate to your key vault. The following example creates an AKS cluster with the Azure Key Vault provider for Secrets Store CSI Driver enabled.Note

If you want to use Microsoft Entra Workload ID, you must also use the

`--enable-oidc-issuer`

and`--enable-workload-identity`

parameters, such as in the following example:`az aks create --name myAKSCluster --resource-group myResourceGroup --enable-addons azure-keyvault-secrets-provider --enable-oidc-issuer --enable-workload-identity --generate-ssh-keys`

`az aks create \ --name myAKSCluster \ --resource-group myResourceGroup \ --enable-addons azure-keyvault-secrets-provider \ --generate-ssh-keys`

The previous command creates a user-assigned managed identity,

`azureKeyvaultSecretsProvider`

, to access Azure resources. The following example uses this identity to connect to the key vault that stores the secrets, but you can also use other[identity access methods](csi-secrets-store-identity-access). Take note of the identity's`clientId`

in the output.`..., "addonProfiles": { "azureKeyvaultSecretsProvider": { ..., "identity": { "clientId": "<client-id>", ... } }`


Note

After you enable this feature, AKS creates a managed identity named `azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Upgrade an existing AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver support

Upgrade an existing AKS cluster with Azure Key Vault provider for Secrets Store CSI Driver capability using the

command and enable the`az aks enable-addons`

`azure-keyvault-secrets-provider`

add-on. The add-on creates a user-assigned managed identity you can use to authenticate to your key vault.`az aks enable-addons --addons azure-keyvault-secrets-provider --name myAKSCluster --resource-group myResourceGroup`


Note

After you enable this feature, AKS creates a managed identity named `azurekeyvaultsecretsprovider-xxx`

in the node resource group and assigns it to the Virtual Machine Scale Sets (VMSS) automatically. You can use this managed identity or your own managed identity to access the key vault. It's not supported to prevent creation of the identity.

## Verify the Azure Key Vault provider for Secrets Store CSI Driver installation

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --name myAKSCluster --resource-group myResourceGroup`

Verify the installation is finished using the

`kubectl get pods`

command, which lists all pods with the`secrets-store-csi-driver`

and`secrets-store-provider-azure`

labels in the kube-system namespace.`kubectl get pods -n kube-system -l 'app in (secrets-store-csi-driver,secrets-store-provider-azure)'`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE aks-secrets-store-csi-driver-4vpkj 3/3 Running 2 4m25s aks-secrets-store-csi-driver-ctjq6 3/3 Running 2 4m21s aks-secrets-store-csi-driver-tlvlq 3/3 Running 2 4m24s aks-secrets-store-provider-azure-5p4nb 1/1 Running 0 4m21s aks-secrets-store-provider-azure-6pqmv 1/1 Running 0 4m24s aks-secrets-store-provider-azure-f5qlm 1/1 Running 0 4m25s`

Verify that each node in your cluster's node pool has a Secrets Store CSI Driver pod and a Secrets Store Provider Azure pod running.


## Create or use an existing Azure Key Vault

Create or update a key vault with Azure role-based access control (Azure RBAC) enabled using the

command or the`az keyvault create`

command with the`az keyvault update`

`--enable-rbac-authorization`

flag. The name of the key vault must be globally unique. For more details on key vault permission models and Azure RBAC, see[Provide access to Key Vault keys, certificates, and secrets with an Azure role-based access control](/en-us/azure/key-vault/general/rbac-guide)`## Create a new Azure key vault az keyvault create --name <keyvault-name> --resource-group myResourceGroup --location eastus2 --enable-rbac-authorization ## Update an existing Azure key vault az keyvault update --name <keyvault-name> --resource-group myResourceGroup --location eastus2 --enable-rbac-authorization`

Your key vault can store keys, secrets, and certificates. In this example, use the

command to set a plain-text secret called`az keyvault secret set`

`ExampleSecret`

.`az keyvault secret set --vault-name <keyvault-name> --name ExampleSecret --value MyAKSExampleSecret`

Take note of the following properties for future use:

- The name of the secret object in the key vault
- The object type (secret, key, or certificate)
- The name of your key vault resource
- The Azure tenant ID of the subscription


## Next steps

In this article, you learned how to use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster. You now need to provide an identity to access the Azure Key Vault. To learn how, continue to the next article.


---

<!-- DOCUMENTO FUSIONADO: __use-tags__node-resource-reservations_aks-diagnostics__windows-aks-partner-solu_ac9ee9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _use-tags__node-resource-reservations_aks-diagnostics.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-tags.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-tags -->

# Use Azure tags in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Azure Kubernetes Service (AKS), you can set Azure tags on an AKS cluster and its related resources using Azure Resource Manager and the Azure CLI. You can also use Kubernetes manifests to set Azure tags for certain resources. Azure tags are a useful tracking resource for certain business processes, such as *chargeback*.

This article explains how to set Azure tags for AKS clusters and related resources.

## Before you begin

Review the following information before you begin:

- Tags set on an AKS cluster apply to all resources related to the cluster, but not the node pools. This operation overwrites the values of existing keys.
- Tags set on a node pool apply only to resources related to that node pool. This operation overwrites the values of existing keys. Resources outside that node pool, including resources for the rest of the cluster and other node pools, are unaffected.
- Public IPs, files, and disks can have tags set by Kubernetes through a Kubernetes manifest. Tags set in this way maintain the Kubernetes values, even if you update them later using a different method. When you remove public IPs, files, or disks through Kubernetes, any tags set by Kubernetes are removed. The tags on those resources that Kubernetes doesn't track remain unaffected.

### Prerequisites

- The Azure CLI version 2.0.59 or later. To find your version, run
`az --version`

. If you need to install it or update your version, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - Kubernetes version 1.20 or later.

### Limitations

- Azure tags have keys that are case-insensitive for operations, such as when you're retrieving a tag by searching the key. In this case, a tag with the specified key is updated or retrieved regardless of casing. Tag values are case-sensitive.
- In AKS, if multiple tags are set with identical keys but different casing, the tags are used in alphabetical order. For example,
`{"Key1": "val1", "kEy1": "val2", "key1": "val3"}`

results in`Key1`

and`val1`

being set. - For shared resources, tags can't determine the split in resource usage on their own.

## Azure tags and AKS clusters

When you create or update an AKS cluster with the `--tags`

parameter, the following are assigned the Azure tags that you specified:

- The AKS cluster itself and its related resources:
- Route table
- Public IP
- Load balancer
- Network security group
- Virtual network
- AKS-managed kubelet msi
- AKS-managed add-on msi
- Private DNS zone associated with the
*private cluster* - Private endpoint associated with the
*private cluster*

- The node resource group

Note

Azure Private DNS only supports 15 tags. For more information, see the [tag resources](/en-us/azure/azure-resource-manager/management/tag-resources).

## Create or update tags on an AKS cluster

### Create a new AKS cluster

Important

If you're using existing resources when you create a new cluster, such as an IP address or route table, the `az aks create`

command overwrites the set of tags. If you delete the cluster later, any tags set by the cluster are removed.

Create a cluster and assign Azure tags using the

command with the`az aks create`

`--tags`

parameter.Note

To set tags on the initial node pool, the virtual machine scale set, and each virtual machine scale set instance associated with the initial node pool, you can also set the

`--nodepool-tags`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --tags dept=IT costcenter=9999 \ --generate-ssh-keys`

Verify the tags have been applied to the cluster and its related resources using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query '[tags]'`

The following example output shows the tags applied to the cluster:

`{ "clusterTags": { "dept": "IT", "costcenter": "9999" } }`


### Update an existing AKS cluster

Important

Setting tags on a cluster using the `az aks update`

command overwrites the set of tags. For example, if your cluster has the tags *dept=IT* and *costcenter=9999*, and you use `az aks update`

with the tags *team=alpha* and *costcenter=1234*, the new list of tags would be *team=alpha* and *costcenter=1234*.

Update the tags on an existing cluster using the

command with the`az aks update`

`--tags`

parameter.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --tags team=alpha costcenter=1234`

Verify the tags have been applied to the cluster and its related resources using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query '[tags]'`

The following example output shows the tags applied to the cluster:

`{ "clusterTags": { "team": "alpha", "costcenter": "1234" } }`


## Add tags to node pools

You can apply an Azure tag to a new or existing node pool in your AKS cluster. Tags applied to a node pool are applied to each node within the node pool and are persisted through upgrades. Tags are also applied to new nodes that are added to a node pool during scale-out operations. Adding a tag can help with tasks such as policy tracking or cost estimation.

When you create or update a node pool with the `--tags`

parameter, the tags you specify are assigned to the following resources:

- The node pool.
- The virtual machine scale set and each virtual machine scale set instance associated with the node pool.

### Create a new node pool

Create a node pool with an Azure tag using the

command with the`az aks nodepool add`

`--tags`

parameter.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name tagnodepool \ --node-count 1 \ --tags abtest=a costcenter=5555 \ --no-wait`

Verify that the tags have been applied to the node pool using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query 'agentPoolProfiles[].{nodepoolName:name,tags:tags}'`

The following example output shows the tags applied to the node pool:

`[ { "nodepoolName": "nodepool1", "tags": null }, { "nodepoolName": "tagnodepool", "tags": { "abtest": "a", "costcenter": "5555" } } ]`


### Update an existing node pool

Important

Setting tags on a node pool using the `az aks nodepool update`

command overwrites the set of tags. For example, if your node pool has the tags *abtest=a* and *costcenter=5555*, and you use `az aks nodepool update`

with the tags *appversion=0.0.2* and *costcenter=4444*, the new list of tags would be *appversion=0.0.2* and *costcenter=4444*.

Update a node pool with an Azure tag using the

command.`az aks nodepool update`

`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name tagnodepool \ --tags appversion=0.0.2 costcenter=4444 \ --no-wait`

Verify the tags have been applied to the node pool using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --query 'agentPoolProfiles[].{nodepoolName:name,tags:tags}'`

The following example output shows the tags applied to the node pool:

`[ { "nodepoolName": "nodepool1", "tags": null }, { "nodepoolName": "tagnodepool", "tags": { "appversion": "0.0.2", "costcenter": "4444" } } ]`


## Add tags using Kubernetes

Important

Setting tags on files, disks, and public IPs using Kubernetes updates the set of tags. For example, if your disk has the tags *dept=IT* and *costcenter=5555*, and you use Kubernetes to set the tags *team=beta* and *costcenter=3333*, the new list of tags would be *dept=IT*, *team=beta*, and *costcenter=3333*.

Any updates you make to tags through Kubernetes retain the value set through Kubernetes. For example, if your disk has tags *dept=IT* and *costcenter=5555* set by Kubernetes, and you use the portal to set the tags *team=beta* and *costcenter=3333*, the new list of tags would be *dept=IT*, *team=beta*, and *costcenter=5555*. If you then remove the disk through Kubernetes, the disk would have the tag *team=beta*.

You can apply Azure tags to public IPs, disks, and files using a Kubernetes manifest.

For public IPs, use

*service.beta.kubernetes.io/azure-pip-tags*under*annotations*. For example:`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-pip-tags: costcenter=3333,team=beta spec: ...`

For files and disks, use

*tags*under*parameters*. For example:`--- apiVersion: storage.k8s.io/v1 ... parameters: ... tags: costcenter=3333,team=beta ...`


## Next steps

Learn more about [using labels in an AKS cluster](use-labels).


---

<!-- DOCUMENTO FUSIONADO: _node-resource-reservations_aks-diagnostics.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-resource-reservations.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-resource-reservations -->

# Node resource reservations in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about node resource reservations in Azure Kubernetes Service (AKS).

## Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS.

AKS reserves two types of resources, **CPU** and **memory**, on each node to maintain node performance and functionality. As a node grows larger in resources, the resource reservations also grow due to a higher need for management of user-deployed pods. Keep in mind that you can't change resource reservations on a node.

### CPU reservations

Reserved CPU is dependent on node type and cluster configuration, which might result in less allocatable CPU due to running extra features. The following table shows CPU reservations in millicores:

| CPU cores on host | 1 core | 2 cores | 4 cores | 8 cores | 16 cores | 32 cores | 64 cores |
|---|---|---|---|---|---|---|---|
| Kube-reserved CPU (millicores) | 60 | 100 | 140 | 180 | 260 | 420 | 740 |

### Memory reservations

In AKS, reserved memory consists of the sum of two values:

**AKS 1.29 and later**

has the`kubelet`

daemon*memory.available < 100 Mi*eviction rule by default. This rule ensures that a node has at least 100 Mi allocatable at all times. When a host is below that available memory threshold, the`kubelet`

triggers the termination of one of the running pods and frees up memory on the host machine.**A rate of memory reservations**set according to the lesser value of:*20 MB * Max Pods supported on the Node + 50 MB*or*25% of the total system memory resources*.**Examples**:- If the virtual machine (VM) provides 8 GB of memory and the node supports up to 30 pods, AKS reserves
*20 MB * 30 Max Pods + 50 MB = 650 MB*for kube-reserved.`Allocatable space = 8 GB - 0.65 GB (kube-reserved) - 0.1 GB (eviction threshold) = 7.25 GB or 90.625% allocatable.`

- If the VM provides 4 GB of memory and the node supports up to 70 pods, AKS reserves
*25% * 4 GB = 1000 MB*for kube-reserved, as this is less than*20 MB * 70 Max Pods + 50 MB = 1450 MB*.

For more information, see

[Configure maximum pods per node in an AKS cluster](concepts-network-ip-address-planning#maximum-pods-per-node).- If the virtual machine (VM) provides 8 GB of memory and the node supports up to 30 pods, AKS reserves

**AKS versions prior to 1.29**

has the`kubelet`

daemon*memory.available < 750 Mi*eviction rule by default. This rule ensures that a node has at least 750 Mi allocatable at all times. When a host is below that available memory threshold, the`kubelet`

triggers the termination of one of the running pods and free up memory on the host machine.**A regressive rate of memory reservations**for the kubelet daemon to properly function (*kube-reserved*).- 25% of the first 4 GB of memory
- 20% of the next 4 GB of memory (up to 8 GB)
- 10% of the next 8 GB of memory (up to 16 GB)
- 6% of the next 112 GB of memory (up to 128 GB)
- 2% of any memory more than 128 GB


Note

AKS reserves an extra 2 GB for system processes in Windows nodes that isn't part of the calculated memory.

Memory and CPU allocation rules are designed to:

- Keep agent nodes healthy, including some hosting system pods critical to cluster health.
- Cause the node to report less allocatable memory and CPU than it would report if it weren't part of a Kubernetes cluster.

For example, if a node offers 7 GB, it reports 34% of memory not allocatable including the 750 Mi hard eviction threshold.

`0.75 + (0.25*4) + (0.20*3) = 0.75 GB + 1 GB + 0.6 GB = 2.35 GB / 7 GB = 33.57% reserved`


In addition to reservations for Kubernetes itself, the underlying node OS also reserves an amount of CPU and memory resources to maintain OS functions.

For associated best practices, see [Best practices for basic scheduler features in AKS](operator-best-practices-scheduler).


---

<!-- DOCUMENTO FUSIONADO: aks-diagnostics.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/aks-diagnostics -->

# Azure Kubernetes Service Diagnose and Solve Problems overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Troubleshooting Azure Kubernetes Service (AKS) cluster issues plays an important role in maintaining your cluster, especially if your cluster is running mission-critical workloads. AKS Diagnose and Solve Problems is an intelligent, self-diagnostic experience that:

- Helps you identify and resolve problems in your cluster.
- Requires no extra configuration or billing cost.

## Open AKS Diagnose and Solve Problems

You can access AKS Diagnose and Solve Problems using the following steps:

In the

[Azure portal](https://portal.azure.com), navigate to your AKS cluster resource.From the service menu, select

**Diagnose and solve problems**.Select a troubleshooting category tile that best describes the issue of your cluster by referring the keywords in each tile description on the homepage or typing a keyword that best describes your issue in the search bar.


## View a diagnostic report

After selecting a category, you can view various diagnostic reports that provide detailed information about the issue. The *Overview* option from the navigation menu runs all the diagnostics in that particular category and displays any issues that are found with the cluster. Select **View details** under each tile to view a detailed description of the issue, including:

- An issue summary
- Error details
- Recommended actions
- Links to helpful docs
- Related-metrics
- Logging data

### Example scenario: Diagnose connectivity issues

I observed that my application is getting disconnected or experiencing intermittent connection issues. In response, I navigate to the AKS Diagnose and Solve Problems home page and select the **Connectivity Issues** tile to investigate the potential causes.

I received a diagnostic alert indicating that the disconnection might be related to my *Cluster DNS*. To gather more information, I select **View details**.

Based on the diagnostic result, it appears that the issue might be related to known DNS issues or the VNet configuration. I can use the documentation links provided to address the issue and resolve the problem.

If the recommended documentation based on the diagnostic results doesn't resolve the issue, I can return to the previous step in Diagnostics and refer to additional documentation.

## Use AKS Diagnose and Solve Problems for best practices

Deploying applications on AKS requires adherence to best practices to guarantee optimal performance, availability, and security. The AKS Diagnose and Solve Problems **Best Practices** tile provides an array of best practices that can assist in managing various aspects, such as VM resource provisioning, cluster upgrades, scaling operations, subnet configuration, and other essential aspects of a cluster's configuration.

Leveraging the AKS Diagnose and Solve Problems can be vital in ensuring that your cluster adheres to best practices and that any potential issues are identified and resolved in a timely and effective manner. By incorporating AKS Diagnose and Solve Problems into your operational practices, you can be confident in the reliability and security of your application in production.

### Example scenario: View best practices

I'm curious about the best practices I can follow to prevent potential problems. In response, I navigate to the AKS Diagnose and Solve Problems home page and select the **Best Practices** tile.

From here, I can view the best practices that are recommended for my cluster and select **View details** to see the results.

## Next steps

- Collect logs to help you further troubleshoot your cluster issues using
[AKS Periscope](https://aka.ms/aksperiscope). - Read the
[triage practices section](/en-us/azure/architecture/operator-guides/aks/aks-triage-practices)of the AKS day-2 operations guide. - Post your questions or feedback at
[UserVoice](https://feedback.azure.com/d365community/forum/aabe212a-f724-ec11-b6e6-000d3a4f0da0). Make sure to add "[Diag]" in the title.


---

<!-- DOCUMENTO FUSIONADO: _windows-aks-partner-solutions__tutorial-kubernetes-prepare-acr_istio-metrics-ma_5fc028.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: windows-aks-partner-solutions.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/windows-aks-partner-solutions -->

# Windows AKS partner solutions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft collaborates with partners to ensure your build, test, deployment, configuration, and monitoring of your applications perform optimally with Windows containers on AKS.

Our third party partners featured in this article have introduction guides to help you start using their solutions with your applications running on Windows containers on AKS.

| Solutions | Partners |
|---|---|
| DevOps |
|

[NGINX](#f5-nginx)[Calico](#calico)[Datadog](#datadog)[New Relic](#new-relic)[Prisma Cloud](#prisma-cloud)[NetApp](#netapp)[Chef](#chef)## DevOps

DevOps streamlines the delivery process, improves collaboration across teams, and enhances software quality, ensuring swift, reliable, and continuous deployment of your Windows-based applications.

### GitLab

The GitLab DevSecOps Platform supports the Microsoft development ecosystem with performance, accessibility testing, SAST, DAST and Fuzzing security scanning, dependency scanning, SBOM, license management and more.

As an extensible platform, GitLab also allows you to plug in your own tooling for any stage. GitLab's integration with Azure Kubernetes Services (AKS) enables full DevSecOps workflows for Windows and Linux Container workloads using either Push CD or GitOps Pull CD with flux manifests. Using Cloud Native Buildpaks, GitLab Auto DevOps can build, test, and autodeploy OSS .NET projects.

To learn more, please our see our [joint blog](https://techcommunity.microsoft.com/t5/containers/using-gitlab-to-build-and-deploy-windows-containers-on-azure/ba-p/3889929).

### CircleCI

CircleCI’s integration with Azure Kubernetes Services (AKS) allows you to automate, build, validate, and ship containerized Windows applications, ensuring faster and more reliable software deployment. You can easily integrate your pipeline with AKS using CircleCI orbs, which are prepacked snippets of YAML configuration.

Follow this [tutorial](https://techcommunity.microsoft.com/t5/containers/continuous-deployment-of-windows-containers-with-circleci-and/ba-p/3841220) to learn how to set up a CI/CD pipeline to build a Dockerized ASP.NET application and deploy it to an AKS cluster.

## Networking

Ensure efficient traffic management, enhanced security, and optimal network performance with these solutions to achieve smooth application connectivity and communication.

### F5 NGINX

NGINX Ingress Controller deployed in AKS, on-premises, and in the cloud implements unified Kubernetes-native API gateways, load balancers, and Ingress controllers to reduce complexity, increase uptime, and provide in-depth insights into app health and performance for containerized Windows workloads.

Running at the edge of a Kubernetes cluster, NGINX Ingress Controller ensures holistic app security with user and service identities, authorization, access control, encrypted communications, and other NGINX App Protect modules for Layer 7 WAF and DoS app protection.

Learn how to manage connectivity to your Windows applications running on Windows nodes in a mixed-node AKS cluster with NGINX Ingress controller in this [blog](https://techcommunity.microsoft.com/t5/containers/improving-customer-experiences-with-f5-nginx-and-windows-on/ba-p/3820344).

### Calico

Tigera provides an active security platform with full-stack observability for containerized workloads and Microsoft AKS as a fully managed SaaS (Calico Cloud) or a self-managed service (Calico Enterprise). The platform prevents, detects, troubleshoots, and automatically mitigates exposure risks of security breaches for workloads in Microsoft AKS.

Its open-source offering, Calico Open Source, is the most widely adopted container networking and security solution. It specifies security and observability as code to ensure consistent enforcement of security policies, which enables DevOps, platform, and security teams to protect workloads, detect threats, achieve continuous compliance, and troubleshoot service issues in real-time.

For more information, see [Securing Windows workloads on Azure Kubernetes Service with Calico](https://techcommunity.microsoft.com/t5/containers/securing-windows-workloads-on-azure-kubernetes-service-with/ba-p/3815429).

## Observability

Observability provides deep insights into your systems, enabling rapid issue detection and resolution to enhance your application’s reliability and performance.

### Datadog

Datadog is the essential monitoring and security platform for cloud applications. We bring together end-to-end traces, metrics, and logs to make your applications, infrastructure, and third-party services entirely observable. Partner with Datadog for Windows on AKS environments to streamline monitoring, proactively resolve issues, and optimize application performance and availability.

Get started by following the recommendations in our [joint blog](https://techcommunity.microsoft.com/t5/containers/gain-full-observability-into-windows-containers-on-azure/ba-p/3853603).

### New Relic

New Relic's Azure Kubernetes integration is a powerful solution that seamlessly connects New Relic's monitoring and observability capabilities with Azure Kubernetes Service (AKS). By deploying the New Relic Kubernetes integration, users gain deep insights into their AKS clusters' performance, health, and resource utilization. This integration allows users to efficiently manage and troubleshoot containerized applications, optimize resource allocation, and proactively identify and resolve issues in their AKS environments. With New Relic's comprehensive monitoring and analysis tools, businesses can ensure the smooth operation and optimal performance of their Kubernetes workloads on Azure.

Check this [blog](https://techcommunity.microsoft.com/t5/containers/leveraging-new-relic-for-instrumentation-of-windows-container-on/ba-p/3870323) for detailed information.

## Security

Ensure the integrity and confidentiality of applications, thereby fostering trust and compliance across your infrastructure.

### Prisma Cloud

Prisma Cloud is a comprehensive Cloud-Native Application Protection Platform (CNAPP) tailor-made to help secure Windows containers on Azure Kubernetes Service (AKS). Gain continuous real-time visibility and control over Windows container environments, including vulnerability and compliance management, identities and permissions, and AI-assisted runtime defense. Integrated container scanning across the pipeline and in Azure Container Registry ensure security throughout the entire application lifecycle.

See [our guidance](https://techcommunity.microsoft.com/t5/containers/unlocking-new-possibilities-with-prisma-cloud-and-windows/ba-p/3866485) for more details.

## Storage

Storage enables standardized and seamless storage interactions, ensuring high application performance and data consistency.

### NetApp

[Astra](https://www.netapp.com/cloud-services/astra/) provides dynamic storage provisioning for stateful workloads on Azure Kubernetes Service (AKS). It also provides data protection using snapshots and clones. Provision SMB volumes through the Kubernetes control plane, making storage seamless and on-demand for all your Windows AKS workloads.

Follow the steps provided in [this blog](https://techcommunity.microsoft.com/t5/azure-architecture-blog/azure-netapp-files-smb-volumes-for-azure-kubernetes-services/ba-p/3052900) post to dynamically provision SMB volumes for Windows AKS workloads.

## Config management

Automate and standardize the system settings across your environments to enhance efficiency, reduce errors, and ensuring system stability and compliance.

### Chef

Chef provides visibility and threat detection from build to runtime that monitors, audits, and remediates the security of your Azure cloud services and Kubernetes and Windows container assets. Chef provides comprehensive visibility and continuous compliance into your cloud security posture and helps limit the risk of misconfigurations in cloud-native environments by providing best practices based on CIS, STIG, SOC2, PCI-DSS and other benchmarks. This is part of a broader compliance offering that supports on-premises or hybrid cloud environments including applications deployed on the edge.

To learn more about Chef’s capabilities, check out the comprehensive ‘how-to’ blog post here: [Securing Your Windows Environments Running on Azure Kubernetes Service with Chef](https://techcommunity.microsoft.com/t5/containers/securing-your-windows-environments-running-on-azure-kubernetes/ba-p/3821830).


---

<!-- DOCUMENTO FUSIONADO: _tutorial-kubernetes-prepare-acr_istio-metrics-managed-prometheus.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-prepare-acr.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-acr -->

# Tutorial - Create an Azure Container Registry (ACR) and build images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Container Registry (ACR) is a private registry for container images. A private container registry allows you to securely build and deploy your applications and custom code.

In this tutorial, you deploy an ACR instance and push a container image to it. You learn how to:

- Create an ACR instance.
- Use
[ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-overview)to build and push container images to ACR. - View images in your registry.

## Before you begin

In the [previous tutorial](tutorial-kubernetes-prepare-app), you used Docker to create a container image for a simple Azure Store Front application. If you haven't created the Azure Store Front app image, return to [Tutorial 1 - Prepare an application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an Azure Container Registry

Before creating an ACR instance, you need a resource group. An Azure resource group is a logical container into which you deploy and manage Azure resources.

Important

This tutorial uses *myResourceGroup* as a placeholder for the resource group name. If you want to use a different name, replace *myResourceGroup* with your own resource group name.

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location westus2`

Create an ACR instance using the

command and provide your own unique registry name. The registry name must be unique within Azure and contain 5-50 lowercase alphanumeric characters. This tutorial series uses an environment variable,`az acr create`

`$ACRNAME`

, as a placeholder for the container registry name. You can set this environment variable to your unique ACR name to use in future commands. The*Basic*SKU is a cost-optimized entry point for development purposes that provides a balance of storage and throughput.`az acr create --resource-group myResourceGroup --name $ACRNAME --sku Basic`


## Build and push container images to registry

Build and push the images to your ACR using the Azure CLI

command.`az acr build`

Note

For this step, there isn't an equivalent Azure PowerShell cmdlet that performs this task.

In the following example, we don't build the

`product-service`

image. This image can take a long time to build, and there's a container image already available in the GitHub Container Registry (GHCR). You can use thecommand to import the image from the GHCR to your ACR instance. We also don't build the`az acr import`

`rabbitmq`

image. This image is available from the Docker Hub public repository and doesn't need to be built or pushed to your ACR instance.`az acr import --name $ACRNAME --source ghcr.io/azure-samples/aks-store-demo/product-service:latest --image aks-store-demo/product-service:latest az acr build --registry $ACRNAME --image aks-store-demo/order-service:latest ./src/order-service/ az acr build --registry $ACRNAME --image aks-store-demo/store-front:latest ./src/store-front/`


## List images in registry

View the images in your ACR instance using the

command.`az acr repository list`

`az acr repository list --name $ACRNAME --output table`

The following example output lists the available images in your registry:

`Result ---------------- aks-store-demo/product-service aks-store-demo/order-service aks-store-demo/store-front`


## Next steps

In this tutorial, you created an ACR and pushed images to it to use in an AKS cluster. You learned how to:

- Create an ACR instance.
- Use
[ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-overview)to build and push container images to ACR. - View images in your registry.

In the next tutorial, you learn how to deploy a Kubernetes cluster in Azure.


---

<!-- DOCUMENTO FUSIONADO: istio-metrics-managed-prometheus.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-metrics-managed-prometheus -->

# Collect metrics for Istio service mesh add-on workloads for Azure Kubernetes Service in Azure Managed Prometheus

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This guide explains how to set up and use Azure Managed Prometheus to collect metrics from Istio service mesh add-on workloads on your Azure Kubernetes cluster.

## Prerequisites

Complete steps to enable the Istio add-on on the cluster as per

[documentation](istio-deploy-addon)

## Enable Azure Monitor managed service for Prometheus

Azure Monitor managed service for Prometheus collects data from Azure Kubernetes cluster.
To enable Azure Monitor managed service for Prometheus, you must create an [Azure Monitor workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-manage?tabs=cli#create-an-azure-monitor-workspace) to store the metrics:

```
export AZURE_MONITOR_WORKSPACE=<azure-monitor-workspace-name>
export AZURE_MONITOR_WORKSPACE_ID=$(az monitor account create \
--name $AZURE_MONITOR_WORKSPACE \
--resource-group $RESOURCE_GROUP \
--location $LOCATION \
--query id -o tsv)
```


### Enable Prometheus addon

To collect Prometheus metrics from your Kubernetes cluster, [enable Prometheus addon](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable?tabs=cli#enable-with-cli):

```
az aks update --enable-azure-monitor-metrics --name $CLUSTER --resource-group $RESOURCE_GROUP --azure-monitor-workspace-resource-id $AZURE_MONITOR_WORKSPACE_ID
```


### Customize scraping of Prometheus metrics in Azure Monitor managed service

Create a scrape config in a file named `prometheus-config`

, similar to the sample provided below. This configuration enables pod annotation-based scraping, which allows Prometheus to automatically discover and scrape metrics from pods with specific annotations.

Important

The scrape config below is just an example. We **highly** recommend customizing it based on your needs. If not adjusted, it could lead to unexpected costs from frequent metric collection and increased data storage.

```
global:
scrape_interval: 30s
scrape_configs:
- job_name: workload
scheme: http
kubernetes_sd_configs:
- role: endpoints
relabel_configs:
- source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
action: keep
regex: true
- source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
action: replace
target_label: __metrics_path__
regex: (.+)
- source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port]
action: replace
regex: ([^:]+)(?::\d+)?;(\d+)
replacement: $1:$2
target_label: __address__
```


To [enable pod annotation-based scraping](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration), create configmap `ama-metrics-prometheus-config`

that references `prometheus-config`

file in `kube-system`

namespace.

```
kubectl create configmap ama-metrics-prometheus-config --from-file=prometheus-config -n kube-system
```


### Verify Metric Collection

Configure access permissions: navigate to your Azure Monitor workspace in Azure portal and create role assignment for yourself to grant 'Monitoring Data Reader' role on the workspace resource.

Generate sample traffic: send a few requests to the product page created earlier, for example:

`curl -s "http://${GATEWAY_URL_EXTERNAL}/productpage" | grep -o "<title>.*</title>"`

View/Query metrics in Azure portal: navigate to Prometheus explorer under your Azure Monitor workspace and

[query metrics](/en-us/azure/azure-monitor/essentials/prometheus-workbooks). The example below shows results for query`istio_requests_total`

.

## Delete resources

If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```
