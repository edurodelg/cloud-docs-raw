---
merged_at: 2026-01-25T12:25:33.872588
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: windows-vs-linux-containers.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/windows-vs-linux-containers -->

# Windows container considerations with Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create deployments that use Windows Server containers on Azure Kubernetes Service (AKS), there are a few differences relative to Linux deployments you should keep in mind. For a detailed comparison of the differences between Windows and Linux in upstream Kubernetes, see [Windows containers in Kubernetes](https://kubernetes.io/docs/concepts/windows/intro/).

Some of the major differences include:

**Identity**: Windows Server uses a larger binary security identifier (SID) that's stored in the Windows Security Access Manager (SAM) database. This database isn't shared between the host and containers or between containers.**File permissions**: Windows Server uses an access control list based on SIDs rather than a bitmask of permissions and UID+GID.**File paths**: The convention on Windows Server is to use \ instead of /. In pod specs that mount volumes, specify the path correctly for Windows Server containers. For example, rather than a mount point of*/mnt/volume*in a Linux container, specify a drive letter and location such as*/K/Volume*to mount as the*K:*drive.

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

This article covers important considerations to keep in mind when using Windows containers instead of Linux containers in Kubernetes. For an in-depth comparison of Windows and Linux containers, see [Comparison with Linux](https://kubernetes.io/docs/concepts/windows/intro/#compatibility-linux-similarities).

## Considerations

| Feature | Windows considerations |
|---|---|
|

*must*be Linux.• The maximum number of nodes per cluster is 5000.

• The Windows Server node pool name has a limit of six characters.

[Privileged containers](use-windows-hpc#limitations)**HostProcess Containers (HPC) containers**.[HPC containers](use-windows-hpc#limitations)[Create a Windows HostProcess pod](https://kubernetes.io/docs/tasks/configure-pod-container/create-hostprocess-pod/).[Azure Network Policy Manager (Azure)](use-network-policies#overview-of-network-policy)• Named ports

• SCTP protocol

• Negative match labels or namespace selectors (all labels except "debug=true")

• "except" CIDR blocks (a CIDR with exceptions)

• Windows Server 2019

[Node upgrade](manage-node-pools#upgrade-a-single-node-pool)[node image upgrade](node-image-upgrade). These upgrades deploy new nodes with the latest Window Server 2019 and Windows Server 2022 base node image and security patches.[AKS Image Cleaner](image-cleaner#limitations)[BYOCNI](use-byo-cni)[Open Service Mesh](open-service-mesh-about)[GPU](use-windows-gpu)[Multi-instance GPU](gpu-multi-instance)[Generation 2 VMs](generation-2-vms)[Custom node config](custom-node-configuration)•

[kubelet](custom-node-configuration#kubelet-configuration): Supported.• OS config: Not supported.

## Next steps

For more information on Windows containers, see the [Windows Server containers FAQ](windows-faq).


---

<!-- DOCUMENTO FUSIONADO: azure-cni-overlay-pod-expand.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overlay-pod-expand -->

# Expand pod CIDR space in Azure CNI Overlay Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can expand your pod Classless Inter-Domain Routing (CIDR) space on Azure CNI Overlay clusters in Azure Kubernetes Service with Linux nodes only. The operation uses the [ az aks update](/en-us/cli/azure/aks#az_aks_update) command and allows expansions without the need to re-create your AKS cluster.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Requirements and parameters

| Requirement or parameter | Supported versions or values | Description |
|---|---|---|
| Feature flag | `EnableAzureCNIOverlayPodCIDRExpansion` |
This feature flag must be registered in your subscription to enable pod CIDR expansion in Azure CNI Overlay AKS clusters. |
| Azure CLI version | 2.48.0 or later | The Azure CLI version must be 2.48.0 or later to support the pod CIDR expansion feature. |
| Kubernetes version | 1.33 | Pod CIDR expansion is supported only on AKS clusters running Kubernetes version 1.33. |
| Node operating system | Linux | Pod CIDR expansion is supported only on Azure CNI Overlay AKS clusters with Linux nodes. |
| Networking mode | Azure CNI Overlay | Pod CIDR expansion is supported only on AKS clusters that use Azure CNI Overlay networking. |
| Example original pod CIDR | `10.244.0.0/18` |
This is an example of a starting pod CIDR block. |
| Example expanded pod CIDR | `10.244.0.0/16` |
This is an example of a target expanded pod CIDR block. |

## Limitations

- Windows nodes and hybrid node scenarios aren't supported.
- Shrinking or changing the pod CIDR isn't supported.
- Adding a discontinuous pod CIDR isn't supported. The new pod CIDR must be a larger superset that contains the complete original range.
- IPv6 pod CIDR expansion isn't supported.
- Changing multiple pod CIDR blocks via
`--pod-cidrs`

isn't supported. - If an
[Azure availability zone](availability-zones)is down during the expansion operation, new nodes might appear as`unready`

. You can expect these nodes to reconcile after the availability zone is up.

## Prerequisites

- You need an Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free/)before you begin. - Ensure that you meet the requirements listed in the
[Requirements and parameters](#requirements-and-parameters)section.

## Register the `EnableAzureCNIOverlayPodCIDRExpansion`

feature flag

Register the

`EnableAzureCNIOverlayPodCIDRExpansion`

feature flag by using thecommand:`az feature register`

`az feature register --namespace Microsoft.ContainerService --name EnableAzureCNIOverlayPodCIDRExpansion`

Verify successful registration by using the

command. It takes a few minutes for the registration to finish.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "EnableAzureCNIOverlayPodCIDRExpansion"`

After the feature shows

`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand:`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Update an Azure CNI Overlay AKS cluster to expand the pod CIDR space

Starting from a pod CIDR block of

`10.244.0.0/18`

, you can expand the pod CIDR space by using thecommand. For example:`az aks update`

`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --pod-cidr 10.244.0.0/16`

Note

Although the update operation might successfully finish and show the new pod CIDR in the network profile, be sure to validate the new cluster state through

`NodeNetworkConfig`

(`nnc`

).Verify the state of the upgrade operation by checking

`NodeNetworkConfig`

(`nnc`

) via the`kubectl get nnc`

command. In the output, all node pools should match your new pod CIDR block (for example,`10.244.0.0/16`

).`kubectl get nnc -A -o jsonpath='{range .items[*]}{.metadata.name}{" "}{.status.networkContainers[0].subnetAddressSpace}{"\n"}{end}'`


## Related content

To learn more about Azure CNI Overlay networking on AKS, see the following articles:
