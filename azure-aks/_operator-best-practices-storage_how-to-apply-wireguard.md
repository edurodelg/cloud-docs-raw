---
merged_at: 2026-01-25T12:06:27.829095
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: operator-best-practices-storage.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-storage -->

# Best practices for storage and backups in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you create and manage clusters in Azure Kubernetes Service (AKS), your applications often need storage. Make sure you understand pod performance needs and access methods so that you can select the best storage for your application. The AKS node size may impact your storage choices. Plan for ways to back up and test the restore process for attached storage.

This best practices article focuses on storage considerations for cluster operators. In this article, you learn:

- What types of storage are available.
- How to correctly size AKS nodes for storage performance.
- Differences between dynamic and static provisioning of volumes.
- Ways to back up and secure your data volumes.

## Choose the appropriate storage type


Best practice guidanceUnderstand the needs of your application to pick the right storage. Use high performance, SSD-backed storage for production workloads. Plan for network-based storage when you need multiple concurrent connections.


Applications often require different types and speeds of storage. Determine the most appropriate storage type by asking the following questions.

- Do your applications need storage that connects to individual pods?
- Do your applications need storage shared across multiple pods?
- Is the storage for read-only access to data?
- Will the storage be used to write large amounts of structured data?

The following table outlines the available storage types and their capabilities:

| Use case | Volume plugin | Read/write once | Read-only many | Read/write many | Windows Server container support |
|---|---|---|---|---|---|
| Shared configuration | Azure Files | Yes | Yes | Yes | Yes |
| Structured app data | Azure Disks | Yes | No | No | Yes |
| Unstructured data, file system operations |
|

AKS provides two primary types of secure storage for volumes backed by Azure Disks or Azure Files. Both use the default Azure Storage Service Encryption (SSE) that encrypts data at rest. Disks cannot be encrypted using Azure Disk Encryption at the AKS node level. With Azure Files shares, there is no limit as to how many can be mounted on a node.

Both Azure Files and Azure Disks are available in Standard and Premium performance tiers:

*Premium*disks- Backed by high-performance solid-state disks (SSDs).
- Recommended for all production workloads.

*Standard*disks- Backed by regular spinning disks (HDDs).
- Good for archival or infrequently accessed data.


While the default storage tier for the Azure Disk CSI driver is Premium SSD, your custom StorageClass can use Premium SSD, Standard SSD, or Standard HDD.

Understand the application performance needs and access patterns to choose the appropriate storage tier. For more information about Managed Disks sizes and performance tiers, see [Azure Managed Disks overview](/en-us/azure/virtual-machines/managed-disks-overview).

### Create and use storage classes to define application needs

Define the type of storage you want using Kubernetes *storage classes*. The storage class is then referenced in the pod or deployment specification. Storage class definitions work together to create the appropriate storage and connect it to pods.

For more information, see [Storage classes in AKS](concepts-storage#storage-classes).

## Size the nodes for storage needs


Best practice guidanceEach node size supports a maximum number of disks. Different node sizes also provide different amounts of local storage and network bandwidth. Plan appropriately for your application demands to deploy the right size of nodes.


AKS nodes run as various Azure VM types and sizes. Each VM size provides:

- A different amount of core resources such as CPU and memory.
- A maximum number of disks that can be attached.

Storage performance also varies between VM sizes for the maximum local and attached disk IOPS (input/output operations per second).

If your applications require Azure Disks as their storage solution, strategize an appropriate node VM size. Storage capabilities and CPU and memory amounts play a major role when deciding on a VM size.

For example, while both the *Standard_B2ms* and *Standard_DS2_v2* VM sizes include a similar amount of CPU and memory resources, their potential storage performance is different:

| Node type and size | vCPU | Memory (GiB) | Max data disks | Max uncached disk IOPS | Max uncached throughput (MBps) |
|---|---|---|---|---|---|
| Standard_B2ms | 2 | 8 | 4 | 1,920 | 22.5 |
| Standard_DS2_v2 | 2 | 7 | 8 | 6,400 | 96 |

In this example, the *Standard_DS2_v2* offers twice as many attached disks, and three to four times the amount of IOPS and disk throughput. If you only compared core compute resources and compared costs, you might have chosen the *Standard_B2ms* VM size with poor storage performance and limitations.

Work with your application development team to understand their storage capacity and performance needs. Choose the appropriate VM size for the AKS nodes to meet or exceed their performance needs. Regularly baseline applications to adjust VM size as needed.

Note

By default, disk size and performance for managed disks is assigned according to the selected VM SKU and vCPU count. Default OS disk sizing is only used on new clusters or node pools when Ephemeral OS disks are not supported and a default OS disk size is not specified. For more information, see [Default OS disk sizing](cluster-configuration#default-os-disk-sizing).

For more information about available VM sizes, see [Sizes for Linux virtual machines in Azure](/en-us/azure/virtual-machines/sizes).

### Consider ephemeral NVMe data disks for maximum performance


Best practice guidanceConsider ephemeral NVMe data disks when you need the highest storage throughput and IOPS, and your workload can tolerate the temporary nature of local node storage. Ephemeral NVMe data disks provide low-latency, host-attached storage that delivers the highest IOPS and throughput available in Azure. NVMe disks are available on L-series, E-series, and GPU VMs, with expanding support for the newer Azure VM v6 and v7 families such as the D-series, F-series, H-series.


NVMe-backed storage enhances workloads that demand high-speed caching, temporary storage, or transient data processing. It eliminates the reliance on high-performance remote disks, which typically require the largest and most costly VM configurations to achieve optimal performance.

Common scenarios that benefit from ephemeral NVMe data disks include:

- AI training or inference pipelines that stage large datasets or checkpoints between iterations
- High-performance databases or streaming engines that maintain replicas or logs across pods
- Batch analytics jobs that require temporary scratch space or shuffle storage

Because NVMe data is tied to the node instance, plan for pod disruption budgets and ensure your application can quickly rebuild from durable storage or replication. Data placed on these disks is lost whenever a node is deallocated, reimaged, or fails.

For further recommendations on ephemeral NVMe data disks, see [Best practices for ephemeral NVMe data disks in Azure Kubernetes Service (AKS)](best-practices-storage-nvme). To expose NVMe capacity to pods, use [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction), which will can orchestrate and create ephemeral **or** persistent volumes backed by local NVMe disks. For implementation guidance, see [Use Azure Container Storage with AKS](/en-us/azure/storage/container-storage/container-storage-aks-quickstart).

Important

Use NVMe data disks only for workloads that can tolerate data loss and recover quickly. Keep business-critical data on durable storage such as Azure Disk or Azure Files.

## Dynamically provision volumes


Best practice guidanceTo reduce management overhead and enable scaling, avoid statically create and assign persistent volumes. Use dynamic provisioning. In your storage classes, define the appropriate reclaim policy to minimize unneeded storage costs once pods are deleted.


To attach storage to pods, use persistent volumes. Persistent volumes can be created manually or dynamically. Creating persistent volumes manually adds management overhead and limits your ability to scale. Instead, provision persistent volume dynamically to simplify storage management and allow your applications to grow and scale as needed.

A persistent volume claim (PVC) lets you dynamically create storage as needed. Underlying Azure disks are created as pods request them. In the pod definition, request a volume to be created and attached to a designated mount path.

For the concepts on how to dynamically create and use volumes, see [Persistent Volumes Claims](concepts-storage#persistent-volume-claims).

To see these volumes in action, see how to dynamically create and use a persistent volume with [Azure Disks](azure-disk-csi) or [Azure Files](azure-files-csi).

As part of your storage class definitions, set the appropriate *reclaimPolicy*. This reclaimPolicy controls the behavior of the underlying Azure storage resource when the pod is deleted. The underlying storage resource can either be deleted or retained for future pod use. Set the reclaimPolicy to *retain* or *delete*.

Understand your application needs, and implement regular checks for retained storage to minimize the amount of unused and billed storage.

For more information about storage class options, see [storage reclaim policies](concepts-storage#storage-classes).

## Secure and back up your data


Best practice guidanceBack up your data using an appropriate tool for your storage type, such as Velero or Azure Backup. Verify the integrity and security of those backups.


When your applications store and consume data persisted on disks or in files, you need to take regular backups or snapshots of that data. Azure Disks can use built-in snapshot technologies. Your applications may need to flush writes-to-disk before you perform the snapshot operation. [Velero](https://github.com/heptio/velero) can back up persistent volumes along with additional cluster resources and configurations. If you can't [remove state from your applications](operator-best-practices-multi-region#remove-service-state-from-inside-containers), back up the data from persistent volumes and regularly test the restore operations to verify data integrity and the processes required.

Understand the limitations of the different approaches to data backups and if you need to quiesce your data prior to snapshot. Data backups don't necessarily let you restore your application environment of cluster deployment. For more information about those scenarios, see [Best practices for business continuity and disaster recovery in AKS](operator-best-practices-multi-region).

## Next steps

This article focused on storage best practices in AKS. For more information about storage basics in Kubernetes, see [Storage concepts for applications in AKS](concepts-storage).


---

<!-- DOCUMENTO FUSIONADO: how-to-apply-wireguard.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-wireguard -->

# Deploy WireGuard encryption with Advanced Container Networking Services (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

WireGuard encryption with Advanced Cluster Networking Services is currently in PREVIEW.

See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

This article shows you how to deploy WireGuard encryption with Advanced Container Networking Services in Azure Kubernetes Service (AKS) clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.71.0. To find the version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).WireGuard encryption is only supported with the Azure CNI powered by Cilium. If you're using any other network plugin, WireGuard encryption isn't supported. See

[Configure Azure CNI Powered by Cilium](/en-us/azure/aks/azure-cni-powered-by-cilium).WireGuard establishes encrypted tunnels over UDP port 51871, which is exposed on each AKS node. Ensure UDP port 51871 is allowed between all node IPs, especially if your environment uses firewalls.


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


### Register the `AdvancedNetworkingWireGuardPreview`

feature flag

Register the `AdvancedNetworkingWireGuardPreview`

feature flag using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command.

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingWireGuardPreview"
```


Verify successful registration using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for the registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingWireGuardPreview"
```


Once the feature shows `Registered`

, refresh the registration of the `Microsoft.ContainerService`

resource provider using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

### Enable Advanced Container Networking Services and WireGuard

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability).**Container Network Security:**Offers security features like Fully Qualified Domain Name (FQDN) filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.
WireGuard is disabled by default even after enabling ACNS. To enable WireGuard set the encryption type by using the flag `--acns-transit-encryption-type wireguard`

.

```
# Set environment variables for the AKS cluster name and resource group. Make sure to replace the placeholders with your own values.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<resourcegroup-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--location eastus \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--enable-acns \
--acns-transit-encryption-type wireguard \
--generate-ssh-keys
```


## Enable Advanced Container Networking Services and WireGuard on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features, which includes [Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security)feature.

Important

Enabling WireGuard on an existing cluster will trigger a rollout restart of the Cilium agent across all nodes. For large clusters, this process can take some time and may temporarily impact workloads. It's recommended to plan the update during a maintenance window or low-traffic period to minimise disruption

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

WireGuard is disabled by default even after enabling ACNS. To enable WireGuard set the encryption type by using the flag `--acns-transit-encryption-type wireguard`

.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-transit-encryption-type wireguard
```


## Get cluster credentials

Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Validate the setup

Validate that WireGuard is enabled successfully using cilium-dbg cli

Note

It might take a few minutes for WireGuard to be fully enabled and configured across all nodes after activation.

- Run a bash shell in one of the Cilium pods

```
kubectl -n kube-system exec -ti ds/cilium -- bash
```


- Check that WireGuard is enabled

```
cilium-dbg encrypt status
```


Expected output:

```
Encryption: Wireguard
Interface: cilium_wg0
Public key: jikeOvVATORm/1GD0kZLxKhw1lofdsfdgiXWVyVIR3T0=
Number of peers: 2
```


The number of peers should equal the number of nodes minus one.

## Troubleshooting

When WireGuard encryption is enabled in an AKS cluster using Cilium CNI, you can use the cilium-dbg CLI tool to inspect tunnel status, verify peer connectivity, and debug encryption-related issues.

### Inspect WireGuard peers

You can inspect peer status and configuration on each node using:

```
kubectl exec -n kube-system ds/cilium -- cilium-dbg debuginfo --output json | jq .encryption
```


Expected output:

```
{
"wireguard": {
"interfaces": [
{
"listen-port": 51871,
"name": "cilium_wg0",
"peer-count": 1,
"peers": [
{
"allowed-ips": [
"10.244.1.31/32",
"10.244.1.206/32",
"10.224.0.6/32"
],
"endpoint": "10.224.0.6:51871",
"last-handshake-time": "2025-04-24T11:13:49.102Z",
"public-key": "3qwZEQLdK5IcFcdXxtr1m8RkDqznPVWEEirJ88+zDyk=",
"transfer-rx": 2457024,
"transfer-tx": 15746568
}
],
"public-key": "jikeOvVATORm/1GD0kZLxKhw1lofdsfdgiXWVyVIR3T0="
}
],
"node-encryption": "Disabled"
}
}
```


This output shows the current state of WireGuard encryption on the node.

- listen-port: The UDP port (51871) where this node is listening for encrypted traffic from peers.
- peer-count: The number of remote WireGuard peers configured for this node.
- peers:
- allowed-ips: list of pod IP addresses routed through the encrypted tunnel to this peer.
- endpoint: The IP and port of the remote peer's WireGuard interface.
- last-handshake-time: Timestamp of the most recent successful key exchange with this peer.
- public-key: The public key of the remote peer.
- transfer-rx / transfer-tx: The total number of bytes received/transmitted over the tunnel.

- public-key: The local WireGuard interface’s public key.
- node-encryption: Encrypts traffic originating from the node itself or from host-network pods. At present, only pod traffic is encrypted. Node encryption is not yet supported and remains disabled by default.

## Disabling WireGuard on an existing cluster

WireGuard can be disabled independently without affecting other ACNS features. To disable it, set the flag `--acns-transit-encryption-type=none`

.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-transit-encryption-type none
```


## Known issues

- Packets might be dropped when configuring the WireGuard device leading to connectivity issues. This issue happens when endpoints are added or removed or when node updates occur. In some cases, this issue might lead to failed calls to
[sendmsg](https://man7.org/linux/man-pages/man2/sendmsg.2.html)and[sendto](https://man7.org/linux/man-pages/man2/sendto.2.html). For more information, see[GitHub issue 33159](https://github.com/cilium/cilium/issues/33159).
