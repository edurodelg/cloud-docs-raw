---
merged_at: 2026-01-25T12:06:27.709278
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: virtual-nodes.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/virtual-nodes -->

# Create and configure an Azure Kubernetes Services (AKS) cluster to use virtual nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To rapidly scale application workloads in an AKS cluster, you can use virtual nodes. With virtual nodes, you have quick provisioning of pods, and only pay per second for their execution time. You don't need to wait for Kubernetes cluster autoscaler to deploy VM compute nodes to run more pods. Virtual nodes are only supported with Linux pods and nodes.

The virtual nodes add on for AKS is based on the open source project [Virtual Kubelet](https://github.com/virtual-kubelet/virtual-kubelet).

This article gives you an overview of the region availability and networking requirements for using virtual nodes, and the known limitations.

## Regional availability

All regions, where ACI supports VNET SKUs, are supported for virtual nodes deployments. For more information, see [Resource availability for Azure Container Instances in Azure regions](/en-us/azure/container-instances/container-instances-region-availability).

For available CPU and memory SKUs in each region, review [Azure Container Instances Resource availability for Azure Container Instances in Azure regions - Linux container groups](/en-us/azure/container-instances/container-instances-region-availability#linux-container-groups)

## Network requirements

Virtual nodes enable network communication between pods that run in Azure Container Instances (ACI) and the AKS cluster. To support this communication, a virtual network subnet is created and delegated permissions are assigned. Virtual nodes only work with AKS clusters created using *advanced* networking (Azure CNI). By default, AKS clusters are created with *basic* networking (kubenet).

Pods running in Azure Container Instances (ACI) need access to the AKS API server endpoint, in order to configure networking.

## Limitations

Virtual nodes functionality is heavily dependent on ACI's feature set. In addition to the [quotas and limits for Azure Container Instances](/en-us/azure/container-instances/container-instances-quotas), the following are scenarios not supported with virtual nodes or are deployment considerations:

Using service principal to pull ACR images.

[Workaround](https://github.com/virtual-kubelet/azure-aci/blob/master/README.md#private-registry)is to use[Kubernetes secrets](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/#create-a-secret-by-providing-credentials-on-the-command-line).Important

Secrets built according to the Kubernetes documentation (for standard nodes) will not work with virtual nodes. A specific server format is required, as detailed in

.`ImageRegistryCredential`

- Azure Container Instances[Virtual Network Limitations](/en-us/azure/container-instances/container-instances-vnet)including VNet peering, Kubernetes network policies, and outbound traffic to the internet with network security groups.Init containers.

[Arguments](/en-us/azure/container-instances/container-instances-exec#restrictions)for exec in ACI.[DaemonSets](concepts-clusters-workloads#statefulsets-and-daemonsets)won't deploy pods to the virtual nodes.To schedule Windows Server containers to ACI, you need to manually install the open source

[Virtual Kubelet ACI](https://github.com/virtual-kubelet/azure-aci)provider.Virtual nodes require AKS clusters with Azure CNI networking.

Using API server authorized ip ranges for AKS.

Volume mounting Azure Files share support

[General-purpose V2](/en-us/azure/storage/common/storage-account-overview#types-of-storage-accounts)and[General-purpose V1](/en-us/azure/storage/common/storage-account-overview#types-of-storage-accounts). However, virtual nodes currently don't support[Persistent Volumes](concepts-storage#persistent-volumes)and[Persistent Volume Claims](concepts-storage#persistent-volume-claims). Follow the instructions for mounting[a volume with Azure Files share as an inline volume](azure-csi-files-storage-provision#mount-file-share-as-an-inline-volume).Using IPv6 isn't supported.

Attaching managed identities to virtual node is not supported.

Virtual nodes don't support the

[Container hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/)feature.

## Next steps

Configure virtual nodes for your clusters:

[Create virtual nodes using Azure CLI](virtual-nodes-cli)[Create virtual nodes using the portal in Azure Kubernetes Services (AKS)](virtual-nodes-portal)

Virtual nodes are often one component of a scaling solution in AKS. For more information on scaling solutions, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: flatcar-container-linux-for-aks.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/flatcar-container-linux-for-aks -->

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
