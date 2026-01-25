---
merged_at: 2026-01-25T12:06:27.895243
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-csi-files-storage-provision.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-csi-files-storage-provision -->

# Azure storage CSI driver and volume provisioning

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Blob storage Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant driver used by Azure Kubernetes Service (AKS) to
manage the lifecycle of Azure Blob storage. The CSI is a standard for exposing arbitrary block and
file storage systems to containerized workloads on Kubernetes.

By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids having to touch the core Kubernetes code and wait for its release cycles.

When you mount Azure Blob storage as a file system into a container or pod, it enables you to use blob storage with many applications that work massive amounts of unstructured data. For example:

- Log file data
- Images, documents, and streaming video or audio
- Disaster recovery data

Applications access data stored in Azure Blob storage using either BlobFuse or the Network File System (NFS) 3.0 protocol. Before the introduction of the Azure Blob storage CSI driver, the only option was to manually install an unsupported driver to access Blob storage from your application running on AKS. When the Azure Blob storage CSI driver is enabled on AKS, there are two built-in storage classes:

- azureblob-fuse-premium
- azureblob-nfs-premium

To create an AKS cluster with CSI drivers support, see [CSI drivers on AKS](csi-storage-drivers). To
learn more about the differences in access between each of the Azure storage types using the NFS
protocol, see
[Compare access to Azure Files, Blob Storage, and Azure NetApp Files with NFS](/en-us/azure/storage/common/nfs-comparison).

The Azure Disks Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant
driver used by Azure Kubernetes Service (AKS) to manage the lifecycle of Azure Disk.

The CSI is a standard for exposing arbitrary block and file storage systems to containerized
workloads on Kubernetes. By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins
to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids
having to touch the core Kubernetes code and wait for its release cycles. To create an AKS cluster
with CSI driver support, see [Enable CSI driver on AKS](csi-storage-drivers).

For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

Note

*In-tree drivers* refer to the current storage drivers that are part of the core Kubernetes code versus the new CSI drivers, which are plug-ins.

The Azure Files Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant driver used by Azure Kubernetes Service (AKS) to
manage the lifecycle of Azure file shares. The CSI is a standard for exposing arbitrary block and
file storage systems to containerized workloads on Kubernetes.

By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids having to touch the core Kubernetes code and wait for its release cycles.

To create an AKS cluster with CSI drivers support, see [Enable CSI drivers on AKS](csi-storage-drivers).

Note

*In-tree drivers* refer to the current storage drivers that are part of the core Kubernetes code versus the new CSI drivers, which are plug-ins.

## Azure CSI driver features

Azure Blob storage CSI driver supports the following features:

- BlobFuse
- NFS 3.0 protocol

In addition to in-tree driver features, Azure Disk CSI driver supports the following features:

Performance improvements during concurrent disk attach and detach

- In-tree drivers attach or detach disks in serial, while CSI drivers attach or detach disks in batch. There's significant improvement when there are multiple disks attaching to one node.

Premium SSD v1 and v2 are supported.

`PremiumV2_LRS`

only supports`None`

caching mode

Zone-redundant storage (ZRS) disk support

`Premium_ZRS`

,`StandardSSD_ZRS`

disk types are supported. ZRS disk could be scheduled on the zone or non-zone node, without the restriction that disk volume should be colocated in the same zone as a given node. For more information, including which regions are supported, see[Zone-redundant storage for managed disks](/en-us/azure/virtual-machines/disks-redundancy).


Note

Depending on the VM SKU that's being used, the Azure Disk CSI driver might have a per-node volume limit. For some powerful VMs (for example, 16 cores), the limit is 64 volumes per node. To identify the limit per VM SKU, review the **Max data disks** column for each VM SKU offered. For a list of VM SKUs offered and their corresponding detailed capacity limits, see [General purpose virtual machine sizes](/en-us/azure/virtual-machines/sizes-general).

## Prerequisites

You must have the Azure CLI version 2.42 or later installed and configured. To find the version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you installed the Azure CLI`aks-preview`

extension, make sure that you update the extension to the latest version by calling`az extension update --name aks-preview`

.Perform the following steps to

[clean up the open source driver](https://github.com/kubernetes-sigs/blob-csi-driver/blob/master/docs/install-csi-driver-master.md#clean-up-blob-csi-driver)if you previously installed the[CSI Blob Storage open-source driver](https://github.com/kubernetes-sigs/blob-csi-driver)to access Azure Blob storage from your cluster.Your AKS cluster

*Control plane*identity (your AKS cluster name) is added to the[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)role on the VNet and network security group.To support an [Azure Data Lake Storage Gen2 account][azure-datalake-storage-account] (ADLS) when using BlobFuse mount, perform the following actions:

- To create an ADLS account using the driver in dynamic provisioning, specify
`isHnsEnabled: "true"`

in the storage class parameters. - To enable BlobFuse access to an ADLS account in static provisioning, specify the mount option
`--use-adls=true`

in the persistent volume. - If you're going to enable a storage account with Hierarchical Namespace, existing persistent volumes (PVs) should be remounted with
`--use-adls=true`

mount option.

- To create an ADLS account using the driver in dynamic provisioning, specify
By default, the BlobFuse cache is located in the

`/mnt`

directory. If the virtual machine (VM) SKU provides a temporary disk, the`/mnt`

directory is mounted on the temporary disk. However, if the VM SKU doesn't provide a temporary disk, the`/mnt`

directory is mounted on the OS disk, you could set`--tmp-path=`

mount option to specify a different cache directory.

Note

If the **blobfuse-proxy** isn't enabled during the installation of the open source driver, the uninstallation of the open source driver disrupts existing blobfuse mounts. However, NFS mounts remain unaffected.

You must have an AKS cluster with the Azure Disk CSI driver enabled. The CSI driver is enabled by default on AKS clusters running Kubernetes version 1.21 or later.

Azure CLI version 2.37.0 or later is installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`kubectl`

command-line tool is installed and configured to connect to your AKS cluster.A storage class configured to use the Azure Disk CSI driver (

`disk.csi.azure.com`

).The Azure Disk CSI driver has a per-node volume limit. The volume count changes based on the size of the node/node pool. Run the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command to determine the number of volumes that can be allocated per node:`kubectl get CSINode <nodename> -o yaml`

If the per-node volume limit is an issue for your workload, consider using

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for persistent volumes instead of CSI drivers.

**General requirements:**

You must have an AKS cluster with the Azure Files CSI driver enabled. The Azure Files CSI driver is enabled by default on AKS clusters running Kubernetes version 1.21 or later.

Azure CLI version 2.37.0 or later is installed and configured. To check your version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`kubectl`

command-line tool is installed and configured to connect to your AKS cluster.A storage class configured to use the Azure Files CSI driver (

`file.csi.azure.com`

).When choosing between standard and premium file shares, it's important you understand the provisioning model and requirements of the expected usage pattern you plan to run on Azure Files. For more information, see

[Choosing an Azure Files performance tier based on usage patterns](/en-us/azure/storage/files/understand-performance#choosing-a-performance-tier-based-on-usage-patterns).

**Network File Share (NFS) requirements:**

Your AKS cluster

*Control plane*identity (your AKS cluster name) is added to the[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)role on the VNet and**NetworkSecurityGroup**.Your AKS cluster's service principal or managed service identity (MSI) must be added to the

**Contributor**role to the storage account.

**Managed Identity requirements:**

Ensure the

[user-assigned Kubelet identity](use-managed-identity#create-a-kubelet-managed-identity)is granted the`Storage File Data SMB MI Admin`

role on the storage account. If you use your own storage account, you need to assign`Storage File Data SMB MI Admin`

role to the user-assigned Kubelet identity on that storage account.If the CSI driver creates the storage account, grant the

`Storage File Data SMB MI Admin`

role to the resource group where the storage account resides.If you use the default built-in user-assigned Kubelet identity, it already has the required

`Storage File Data SMB MI Admin`

role on the managed node resource group.

Note

The Azure File CSI driver only permits the mounting of SMB file shares using key-based (NTLM v2) authentication, and therefore doesn't support the maximum security profile of Azure File share settings. On the other hand, mounting NFS file shares doesn't require key-based authentication.

## Enable CSI driver on a new or existing AKS cluster

Using the Azure CLI, you can enable the Blob storage CSI driver on a new or existing AKS cluster before you configure a persistent volume for use by pods in the cluster.

To enable the driver on a new cluster, include the

`--enable-blob-driver`

parameter with the`az aks create`

command as shown in the following example:`az aks create \ --enable-blob-driver \ --name myAKSCluster \ --resource-group myResourceGroup \ --generate-ssh-keys`

To enable the driver on an existing cluster, include the

`--enable-blob-driver`

parameter with the`az aks update`

command as shown in the following example:`az aks update --enable-blob-driver --name myAKSCluster --resource-group myResourceGroup`


You're prompted to confirm there isn't an open-source Blob CSI driver installed. After you confirm, it might take several minutes to complete this action. Once it's complete, you should see in the output the status of enabling the driver on your cluster. The following example resembles the section indicating the results of the previous command:

```
"storageProfile": {
"blobCsiDriver": {
"enabled": true
},
...
}
```


## Disable CSI driver on an existing AKS cluster

Using the Azure CLI, you can disable the Blob storage CSI driver on an existing AKS cluster after you remove the persistent volume from the cluster.

To disable the driver on an existing cluster, include the

`--disable-blob-driver`

parameter with the`az aks update`

command as shown in the following example:`az aks update --disable-blob-driver --name myAKSCluster --resource-group myResourceGroup`


## Use a persistent volume for storage

Kubernetes assigns a [persistent volume](concepts-storage#persistent-volumes) (PV) as a storage resource to one or more pods. You can provision PVs dynamically through Kubernetes or statically as an administrator.

If multiple pods need concurrent access to the same storage volume, you can use Azure Blob storage to connect by using NFS or BlobFuse. This article shows you how to dynamically create an Azure Blob storage container for use by multiple pods in an AKS cluster.

For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

This article shows you how to dynamically create a PV with Azure disk for use by a single pod in an AKS cluster.

If multiple pods need concurrent access to the same storage volume, you can use Azure Files to
connect by using the [Server Message Block (SMB)](/en-us/windows/desktop/FileIO/microsoft-smb-protocol-and-cifs-protocol-overview) or
[Network File System (NFS)](/en-us/windows-server/storage/nfs/nfs-overview). This article shows you how to dynamically create an Azure
Files share for use by multiple pods in an AKS cluster.

**Dynamically provisioned volume:** Use this approach when you want Kubernetes to automatically
create and manage storage resources. It's ideal for scenarios where you need on-demand scaling,
prefer infrastructure-as-code, and want to minimize manual configuration steps.

**Statically provisioned volume:** Choose this method if you already have an Azure Blob storage
account or container that you want to use. It provides more control over storage setup, access, and
lifecycle, and is suitable when you need to connect to existing resources or reuse storage across
multiple clusters or workloads.

This section provides guidance for cluster administrators who want to provision one or more persistent volumes that include details of Blob storage for use by a workload. A persistent volume claim (PVC) uses the storage class object to dynamically provision an Azure Blob storage container.

To provision a persistent volume using Azure Blob storage with the provided storage class, follow these steps:

Create the

`StorageClass`

manifest by saving the following YAML to a file named`blob-fuse-sc.yaml`

:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: blob-fuse provisioner: blob.csi.azure.com parameters: skuName: Premium_LRS # available values: Standard_LRS, Premium_LRS, Standard_GRS, Standard_RAGRS, Standard_ZRS, Premium_ZRS protocol: fuse2 networkEndpointType: privateEndpoint reclaimPolicy: Delete volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - -o allow_other - --file-cache-timeout-in-seconds=120 - --use-attr-cache=true - --cancel-list-on-mount-seconds=10 # prevent billing charges on mounting - -o attr_timeout=120 - -o entry_timeout=120 - -o negative_timeout=120 - --log-level=LOG_WARNING # LOG_WARNING, LOG_INFO, LOG_DEBUG - --cache-size-mb=1000 # Default will be 80% of available memory, eviction will happen beyond specified value.`

To create the storage class in your cluster, apply the

`StorageClass`

by running the following command:`kubectl apply -f blob-fuse-sc.yaml`


## Create a PVC using built-in storage class

A storage class is used to define how an Azure Blob storage container is created. A storage account is automatically created in the node resource group for use with the storage class to hold the Azure Blob storage container. Choose one of the following Azure storage redundancy SKUs for skuName:

**Standard_LRS**: Standard locally redundant storage**Premium_LRS**: Premium locally redundant storage**Standard_ZRS**: Standard zone redundant storage**Premium_ZRS**: Premium zone redundant storage**Standard_GRS**: Standard geo-redundant storage**Standard_RAGRS**: Standard read-access geo-redundant storage

When you use storage CSI drivers on AKS, there are two other built-in `StorageClasses`

that use the Azure Blob CSI storage driver.

The reclaim policy on both storage classes ensures that the underlying Azure Blob storage is deleted
when the respective PV is deleted. The storage classes also configure the container to be expandable
by default, as the `set allowVolumeExpansion`

parameter is set to **true**.

Note

Shrinking persistent volumes isn't supported.

Use the [kubectl get sc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command to see the storage classes. The following example
shows the `azureblob-fuse-premium`

and `azureblob-nfs-premium`

storage classes available within an
AKS cluster:

```
NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE
azureblob-fuse-premium blob.csi.azure.com Delete Immediate true 23h
azureblob-nfs-premium blob.csi.azure.com Delete Immediate true 23h
```


To use these storage classes, create a PVC and respective pod that references and uses them. A PVC is used to automatically allocate storage based on a storage class. You can create a PVC using one of the built-in storage classes or a custom storage class. This PVC creates an Azure Blob storage container with your specified SKU, size, and protocol. When you create a pod definition, the PVC is specified to request the desired storage.

A PVC uses the storage class object to dynamically provision an Azure Blob storage container. The following YAML can be used to create a 5 GB PVC with *ReadWriteMany* access, using the built-in storage class. For more information on access modes, see the [Kubernetes persistent volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) documentation.

Create a file named

`blob-nfs-pvc.yaml`

and copy the following YAML:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azure-blob-storage spec: accessModes: - ReadWriteMany storageClassName: azureblob-nfs-premium resources: requests: storage: 5Gi`

Create the PVC with the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command:`kubectl create -f blob-nfs-pvc.yaml`


Once complete, the Blob storage container is created. You can use the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)
command to view the status of the PVC:

```
kubectl get pvc azure-blob-storage
```


The output of the command resembles the following example:

```
NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE
azure-blob-storage Bound pvc-b88e36c5-c518-4d38-a5ee-337a7dda0a68 5Gi RWX azureblob-nfs-premium 92m
```


## Mount the PVC

The following YAML creates a pod that uses the PVC **azure-blob-storage** to mount the Azure Blob storage at the `/mnt/blob`

path.

Create a file named

`blob-nfs-pv`

, and copy the following YAML. Make sure that the**claimName**matches the PVC created in the previous step.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/blob" name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: azure-blob-storage`

Create the pod with the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f blob-nfs-pv.yaml`

After the pod is in the running state, run the following command to create a new file called

`test.txt`

.`kubectl exec mypod -- touch /mnt/blob/test.txt`

To validate the disk is correctly mounted, run the following command, and verify you see the

`test.txt`

file in the output:`kubectl exec mypod -- ls /mnt/blob`

The output of the command resembles the following example:

`test.txt`


## Create an Azure Blob custom storage class

The default storage classes suit the most common scenarios, but not all. In some cases, you might want to have your own storage class customized with your own parameters. In this section, we provide two examples with the first one using the NFS protocol, and the second one using BlobFuse.

In this example, the following manifest configures mounting a Blob storage container using the NFS
protocol. Use it to add the `tags`

parameter.

Create a file named

`blob-nfs-sc.yaml`

, and paste the following example manifest:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azureblob-nfs-premium provisioner: blob.csi.azure.com parameters: protocol: nfs tags: environment=Development volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - nconnect=4`

Create the storage class with the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f blob-nfs-sc.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/blob-nfs-premium created`


## Mount an NFS or BlobFuse PV

In this section, you mount the PV using the NFS protocol or BlobFuse.

Mounting Blob storage using the NFS v3 protocol doesn't authenticate using an account key. Your AKS
cluster needs to reside in the same or peered virtual network as the agent node. The only way to
secure the data in your storage account is by using a virtual network and other network security
settings. For more information on how to set up NFS access to your storage account, see
[Mount Blob Storage by using the Network File System (NFS) 3.0 protocol](/en-us/azure/storage/blobs/network-file-system-protocol-support-how-to).

The following example demonstrates how to mount a Blob storage container as a persistent volume using the NFS protocol.

Create a file named

`pv-blob-nfs.yaml`

and copy in the following YAML. Under`storageClass`

, update`resourceGroup`

,`storageAccount`

, and`containerName`

.Note

The

`volumeHandle`

value within your YAML should be a unique volumeID for every identical storage blob container in the cluster.The characters

`#`

and`/`

are reserved for internal use and can't be used.`apiVersion: v1 kind: PersistentVolume metadata: annotations: pv.kubernetes.io/provisioned-by: blob.csi.azure.com name: pv-blob spec: capacity: storage: 1Pi accessModes: - ReadWriteMany persistentVolumeReclaimPolicy: Retain # If set as "Delete" container would be removed after pvc deletion storageClassName: azureblob-nfs-premium mountOptions: - nconnect=4 csi: driver: blob.csi.azure.com # make sure volumeid is unique for every identical storage blob container in the cluster # character `#` and `/` are reserved for internal use and cannot be used in volumehandle volumeHandle: account-name_container-name volumeAttributes: resourceGroup: resourceGroupName storageAccount: storageAccountName containerName: containerName protocol: nfs`

Note

While the

[Kubernetes API](https://github.com/kubernetes/kubernetes/blob/release-1.26/pkg/apis/core/types.go#L303-L306)**capacity**attribute is mandatory, this value isn't used by the Azure Blob storage CSI driver because you can flexibly write data until you reach your storage account's capacity limit. The value of the`capacity`

attribute is used only for size matching between*PVs*and*PVCs*. We recommend using a fictitious high value. The pod sees a mounted volume with a fictitious size of 5 Petabytes.Run the following command to create the persistent volume using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command referencing the YAML file created earlier:`kubectl create -f pv-blob-nfs.yaml`

Create a

`pvc-blob-nfs.yaml`

file with a*PersistentVolumeClaim*. For example:`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: pvc-blob spec: accessModes: - ReadWriteMany resources: requests: storage: 10Gi volumeName: pv-blob storageClassName: azureblob-nfs-premium`

Run the following command to create the persistent volume claim using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command referencing the YAML file created earlier:`kubectl create -f pvc-blob-nfs.yaml`


## Create a pod

The following YAML creates a pod that uses the PV or PVC named **pvc-blob** created earlier, to mount the Azure Blob storage at the `/mnt/blob`

path.

Create a file named

`nginx-pod-blob.yaml`

, and copy in the following YAML. Make sure that the**claimName**matches the PVC created in the previous step when creating a PV for NFS or BlobFuse.`kind: Pod apiVersion: v1 metadata: name: nginx-blob spec: nodeSelector: "kubernetes.io/os": linux containers: - image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine name: nginx-blob volumeMounts: - name: blob01 mountPath: "/mnt/blob" readOnly: false volumes: - name: blob01 persistentVolumeClaim: claimName: pvc-blob`

Run the following command to create the pod and mount the PVC using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command:`kubectl create -f nginx-pod-blob.yaml`

Run the following command to create an interactive shell session with the pod to verify if the Blob storage is mounted:

`kubectl exec -it nginx-blob -- df -h`

The output from the command resembles the following example:

`Filesystem Size Used Avail Use% Mounted on ... blobfuse 14G 41M 13G 1% /mnt/blob ...`


## Create a StatefulSet

To ensure your workload retains its storage volume across pod restarts or replacements, use a StatefulSet. StatefulSets simplify the process of associating persistent storage with pods, so that new pods created to replace failed ones can automatically access the same storage volumes. The following examples demonstrate how to set up a StatefulSet for Blob storage using either BlobFuse or the NFS protocol.

Create a file named

`azure-blob-nfs-ss.yaml`

and copy in the following YAML.`apiVersion: apps/v1 kind: StatefulSet metadata: name: statefulset-blob-nfs labels: app: nginx spec: serviceName: statefulset-blob-nfs replicas: 1 template: metadata: labels: app: nginx spec: nodeSelector: "kubernetes.io/os": linux containers: - name: statefulset-blob-nfs image: mcr.microsoft.com/azurelinux/base/nginx:1.25 volumeMounts: - name: persistent-storage mountPath: /mnt/blob updateStrategy: type: RollingUpdate selector: matchLabels: app: nginx volumeClaimTemplates: - metadata: name: persistent-storage spec: storageClassName: azureblob-nfs-premium accessModes: ["ReadWriteMany"] resources: requests: storage: 100Gi`

Create the StatefulSet with the

`kubectl create`

command:`kubectl create -f azure-blob-nfs-ss.yaml`


### Dynamic PVC storage class parameters

The following table includes parameters you can use to define a custom storage class for your dynamic PVC.

| Name | Description | Example | Mandatory | Default value |
|---|---|---|---|---|
| skuName | Specify an Azure storage account type (alias: `storageAccountType` ). |
`Standard_LRS` , `Premium_LRS` , `Standard_GRS` , `Standard_RAGRS` |
No | `Standard_LRS` |
| location | Specify an Azure location. | `eastus` |
No | If empty, the driver uses the same location name as current cluster. |
| resourceGroup | Specify an Azure resource group name. | myResourceGroup | No | If empty, the driver uses the same resource group name as current cluster. |
| storageAccount | Specify an Azure storage account name. | storageAccountName | No | When a specific storage account name isn't provided, the driver looks for a suitable storage account that matches the account settings within the same resource group. If it fails to find a matching storage account, it creates a new one. However, if a storage account name is specified, the storage account must already exist. |
networkEndpointType 1 |
Specify network endpoint type for the storage account created by driver. If privateEndpoint is specified, a
|

`privateEndpoint`

`fuse`

, `nfs`

`fuse`

`pvc-fuse`

for BlobFuse or `pvc-nfs`

for NFS v3.`<storage-account>.blob.core.windows.net`

.`<storage-account>.blob.core.windows.net`

or other sovereign cloud storage account DNS domain name.`true`

,`false`

`false`

`core.windows.net`

`true`

,`false`

`false`

1 If the storage account is created by the driver, then you only need to specify `networkEndpointType: privateEndpoint`

parameter in storage class. The CSI driver creates the private endpoint and private DNS zone (named `privatelink.blob.core.windows.net`

) together with the account. If you bring your own storage account, then you need to [create the private endpoint](/en-us/azure/storage/common/storage-private-endpoints) for the storage account. If you're using Azure Blob storage in a network isolated cluster, you must create a custom storage class with `networkEndpointType: privateEndpoint`

.

### Static PV provisioning parameters

The following table includes parameters you can use to define your static PV.

| Name | Description | Example | Mandatory | Default value |
|---|---|---|---|---|
| volumeHandle | Specify a value the driver can use to uniquely identify the storage blob container in the cluster. | A recommended way to produce a unique value is to combine the globally unique storage account name and container name: `{account-name}_{container-name}` . The `#` and `/` characters are reserved for internal use and can't be used in a volume handle. |
Yes | |
| volumeAttributes.resourceGroup | Specify Azure resource group name. | myResourceGroup | No | If empty, driver uses the same resource group name as current cluster. |
| volumeAttributes.storageAccount | Specify an existing Azure storage account name. | storageAccountName | Yes | |
| volumeAttributes.containerName | Specify existing container name. | container | Yes | |
| volumeAttributes.protocol | Specify BlobFuse mount or NFS v3 mount. | `fuse` , `nfs` |
No | `fuse` |

## Create Azure Disk PVs using built-in storage classes

A storage class is used to define how a unit of storage is dynamically created with a PV. For more information on Kubernetes storage classes, see [Kubernetes storage classes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

When you use the Azure Disk CSI driver on AKS, there are two more built-in `StorageClasses`

that use the Azure Disk CSI storage driver. The other CSI storage classes are created with the cluster alongside the in-tree default storage classes.

`managed-csi`

: Creates managed disks using Azure Standard SSD with locally redundant storage (LRS). With Kubernetes version 1.29 for AKS clusters deployed across multiple availability zones, this storage class uses Azure Standard SSD zone-redundant storage (ZRS) to provision managed disks.`managed-csi-premium`

: Provisions managed disks using Azure Premium LRS. Beginning with Kubernetes version 1.29, for AKS clusters spanning multiple availability zones, this storage class automatically uses Azure Premium ZRS to create managed disks.

Effective starting with Kubernetes version 1.29, when you deploy Azure Kubernetes Service (AKS) clusters across multiple availability zones, AKS now utilizes zone-redundant storage (ZRS) to create managed disks within built-in storage classes.

ZRS ensures synchronous replication of your Azure managed disks across multiple Azure availability zones in your chosen region. This redundancy strategy enhances the resilience of your applications and safeguards your data against datacenter failures.

However, it's important to note that zone-redundant storage (ZRS) comes at a higher cost compared to locally redundant storage (LRS). If cost optimization is a priority, you can create a new storage class with the LRS SKU name parameter and use it in your persistent volume claim.


Reducing the size of a PVC isn't supported due to the risk of data loss. You can edit an existing storage class using the `kubectl edit sc`

command, or you can create your own custom storage class. For example, if you want to use a disk of size 4 TiB, you must create a storage class that defines `cachingmode: None`

because [disk caching isn't supported for disks 4 TiB and larger][disk-host-cache-setting]. For more information about storage classes and creating your own storage class, see [Storage options for applications in AKS](concepts-storage#storage-classes).

The reclaim policy in both storage classes ensures that the underlying Azure Disks are deleted when the respective PV is deleted. The storage classes also configure the PVs to be expandable. You just need to edit the PVC with the new size.

To use these storage classes, create a [PVC](concepts-storage#persistent-volume-claims) and respective pod that references and uses them. A PVC is used to automatically provision storage based on a storage class. A PVC can use one of the precreated storage classes or a user-defined storage class to create an Azure-managed disk for the desired SKU and size. When you create a pod definition, the PVC is specified to request the desired storage.

Note

Persistent volume claims are specified in GiB but Azure managed disks are billed based on the SKU for a specific size. These SKUs range from 32GiB for S4 or P4 disks to 32TiB for S80 or P80 disks (in preview). The throughput and IOPS performance of a Premium managed disk depends on both the SKU and the instance size of the nodes in the AKS cluster. For more information, see [Pricing and performance of managed disks](https://azure.microsoft.com/pricing/details/managed-disks/).

You can see the precreated storage classes using the [ kubectl get sc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. The following example shows the precreated storage classes available within an AKS cluster:

```
kubectl get sc
```


The output of the command resembles the following example:

```
NAME PROVISIONER AGE
default (default) disk.csi.azure.com 1h
managed-csi disk.csi.azure.com 1h
```


A PVC automatically provisions storage based on a storage class. In this case, a PVC can use one of the precreated storage classes to create a standard or premium Azure managed disk.

Create a file named

`azure-pvc.yaml`

and copy in the following manifest. The claim requests a disk named`azure-managed-disk`

that's`5 GB`

in size with`ReadWriteOnce`

access. The*managed-csi*storage class is specified as the storage class.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azure-managed-disk spec: accessModes: - ReadWriteOnce storageClassName: managed-csi resources: requests: storage: 5Gi`

Tip

To create a disk that uses premium storage, use

`storageClassName: managed-csi-premium`

rather than*managed-csi*.Create the persistent volume claim using the

command and specify your`kubectl apply`

*azure-pvc.yaml*file.`kubectl apply -f azure-pvc.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/azure-managed-disk created`


## Apply a PVC to a pod

After you create the persistent volume claim, you must verify it has a status of `Pending`

. The `Pending`

status indicates it's ready to be used by a pod.

Verify the status of the PVC using the

`kubectl describe pvc`

command.`kubectl describe pvc azure-managed-disk`

The output of the command resembles the following condensed example:

`Name: azure-managed-disk Namespace: default StorageClass: managed-csi Status: Pending [...]`

Create a file named

`azure-pvc-disk.yaml`

and copy in the following manifest. This manifest creates a basic NGINX pod that uses the persistent volume claim named`azure-managed-disk`

to mount the Azure Disk at the path`/mnt/azure`

. For Windows Server containers, specify a`mountPath`

using the Windows path convention, such as*'D:'*.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/azure" name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: azure-managed-disk`

Create the pod using the

command.`kubectl apply`

`kubectl apply -f azure-pvc-disk.yaml`

The output of the command resembles the following example:

`pod/mypod created`

You now have a running pod with your Azure Disk mounted in the

`/mnt/azure`

directory. Check the pod configuration using thecommand.`kubectl describe`

`kubectl describe pod mypod`

The output of the command resembles the following example:

`[...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: azure-managed-disk ReadOnly: false default-token-smm2n: Type: Secret (a volume populated by a Secret) SecretName: default-token-smm2n Optional: false [...] Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Scheduled 2m default-scheduler Successfully assigned mypod to aks-nodepool1-79590246-0 Normal SuccessfulMountVolume 2m kubelet, aks-nodepool1-79590246-0 MountVolume.SetUp succeeded for volume "default-token-smm2n" Normal SuccessfulMountVolume 1m kubelet, aks-nodepool1-79590246-0 MountVolume.SetUp succeeded for volume "pvc-faf0f176-8b8d-11e8-923b-deb28c58d242" [...]`


## Dynamic storage class parameters for PVCs

The following table includes parameters you can use to define a custom storage class for your PVCs.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| skuName | Azure Disks storage account type (alias: `storageAccountType` ) |
`Standard_LRS` , `Premium_LRS` , `StandardSSD_LRS` , `PremiumV2_LRS` , `UltraSSD_LRS` , `Premium_ZRS` , `StandardSSD_ZRS` |
No | `StandardSSD_LRS` |
| fsType | File System Type | `ext4` , `ext3` , `ext2` , `xfs` , `btrfs` for Linux, `ntfs` for Windows |
No | `ext4` for Linux, `ntfs` for Windows |
| cachingMode | [Azure Data Disk Host Cache Setting][disk-host-cache-setting](PremiumV2_LRS and UltraSSD_LRS only support `None` caching mode) |
`None` , `ReadOnly` , `ReadWrite` |
No | `ReadOnly` |
| resourceGroup | Specify the resource group for the Azure Disks | Existing resource group name | No | If empty, driver uses the same resource group name as current AKS cluster |
| DiskIOPSReadWrite | [UltraSSD disk][ultra-ssd-disks] or [Premium SSD v2][premiumv2_lrs_disks] IOPS Capability (minimum: 2 IOPS/GiB) | 100~160000 | No | `500` |
| DiskMBpsReadWrite | [UltraSSD disk][ultra-ssd-disks] or [Premium SSD v2][premiumv2_lrs_disks] Throughput Capability(minimum: 0.032/GiB) | 1~2000 | No | `100` |
| LogicalSectorSize | Logical sector size in bytes for ultra disk. Supported values are 512 ad 4096. 4096 is the default. | `512` , `4096` |
No | `4096` |
| tags | Azure Disk [tags][azure-tags] | Tag format: `key1=val1,key2=val2` |
No | "" |
| diskEncryptionSetID | ResourceId of the disk encryption set to use for [enabling encryption at rest][disk-encryption] | format: `/subscriptions/{subs-id}/resourceGroups/{rg-name}/providers/Microsoft.Compute/diskEncryptionSets/{diskEncryptionSet-name}` |
No | "" |
| diskEncryptionType | Encryption type of the disk encryption set. | `EncryptionAtRestWithCustomerKey` (by default), `EncryptionAtRestWithPlatformAndCustomerKeys` |
No | "" |
| writeAcceleratorEnabled | [Write Accelerator on Azure Disks][azure-disk-write-accelerator] | `true` , `false` |
No | "" |
| networkAccessPolicy | NetworkAccessPolicy property to prevent generation of the SAS URI for a disk or a snapshot | `AllowAll` , `DenyAll` , `AllowPrivate` |
No | `AllowAll` |
| diskAccessID | Azure Resource ID of the DiskAccess resource to use private endpoints on disks | No | `` | |
| enableBursting | [Enable on-demand bursting][on-demand-bursting] beyond the provisioned performance target of the disk. On-demand bursting should only be applied to Premium disk and when the disk size > 512 GB. Ultra and shared disk isn't supported. Bursting is disabled by default. | `true` , `false` |
No | `false` |
| userAgent | The user agent is used for [customer usage attribution][customer-usage-attribution] | No | The generated user agent is formatted as `driverName/driverVersion compiler/version (OS-ARCH)` |
|
| subscriptionID | Specify Azure subscription ID where the Azure Disks is created. | Azure subscription ID | No | If not empty, `resourceGroup` must be provided. |

## Static provisioning parameters for a PV

The following table includes parameters you can use to define a PV.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| volumeHandle | Azure disk URI | `/subscriptions/{sub-id}/resourcegroups/{group-name}/providers/microsoft.compute/disks/{disk-id}` |
Yes | N/A |
| volumeAttributes.fsType | File system type | `ext4` , `ext3` , `ext2` , `xfs` , `btrfs` for Linux, `ntfs` for Windows |
No | `ext4` for Linux, `ntfs` for Windows |
| volumeAttributes.partition | Partition number of the existing disk (only supported on Linux) | `1` , `2` , `3` |
No | Empty (no partition) - Make sure partition format is like `-part1` |
| volumeAttributes.cachingMode | [Disk host cache setting][disk-host-cache-setting] | `None` , `ReadOnly` , `ReadWrite` |
No | `ReadOnly` |

## Create an Azure Disk custom storage class

The default storage classes are suitable for most common scenarios. For some cases, you might want
to have your own storage class customized with your own parameters. For example, you might want to
change the `volumeBindingMode`

class.

You can use a `volumeBindingMode: Immediate`

class that guarantees it occurs immediately once the
persistent volume claim (PVC) is created. When your node pools are topology constrained, for example
when using availability zones, PVs would be bound or provisioned without knowledge of the pod's
scheduling requirements.

To address this scenario, you can use `volumeBindingMode: WaitForFirstConsumer`

, which delays the binding and provisioning of a PV until a pod that uses the PVC is created. This approach ensures that the persistent volume (PV) is provisioned in the same availability zone or topology as required per the pod's scheduling constraints. The default storage classes use `volumeBindingMode: WaitForFirstConsumer`

class.

Create a file named

`sc-azuredisk-csi-waitforfirstconsumer.yaml`

, and then paste the following manifest. The storage class is the same as our`managed-csi`

storage class, but with a different`volumeBindingMode`

class. For example:`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: azuredisk-csi-waitforfirstconsumer provisioner: disk.csi.azure.com parameters: skuname: StandardSSD_LRS allowVolumeExpansion: true reclaimPolicy: Delete volumeBindingMode: WaitForFirstConsumer`

Create the storage class by running the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify your`sc-azuredisk-csi-waitforfirstconsumer.yaml`

file:`kubectl apply -f sc-azuredisk-csi-waitforfirstconsumer.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/azuredisk-csi-waitforfirstconsumer created`


## Learn about volume snapshots

The Azure Disk CSI driver supports [volume snapshots](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html), enabling you to capture the state of persistent volumes at specific points in time for backup and restore operations. Volume snapshots let you create point-in-time copies of your persistent data without interrupting running applications. You can use these snapshots to create new volumes or restore existing ones to a previous state.

You can create two types of snapshots:

**Full snapshots**: Capture the complete state of the disk.**Incremental snapshots**: Capture only the changes since the last snapshot, offering better storage efficiency and cost savings.[Incremental snapshots](/en-us/azure/virtual-machines/disks-incremental-snapshots)are the default behavior when the`incremental`

parameter is set to`true`

in your VolumeSnapshotClass.

The following table provides details for these parameters.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| resourceGroup | Resource group for storing snapshot shots | EXISTING RESOURCE GROUP | No | If not specified, snapshots are stored in the same resource group as source Azure Disks |
| incremental | Take
|

`true`

, `false`

`true`

[tags](/en-us/azure/azure-resource-manager/management/tag-resources)[customer usage attribution](/en-us/azure/marketplace/azure-partner-customer-usage-attribution)`driverName/driverVersion compiler/version (OS-ARCH)`

`resourceGroup`

must be provided, `incremental`

must set as `false`

Volume snapshots support the following scenarios:

**Backup and restore**: Create point-in-time backups of stateful application data and restore when needed.**Data cloning**: Clone existing volumes to create new persistent volumes with the same data.**Disaster recovery**: Quickly recover from data loss or corruption.

### Create a volume snapshot

Note

Before proceeding, ensure that the application isn't writing data to the source disk.

For an example of this capability, create a

[volume snapshot class](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/storageclass-azuredisk-snapshot.yaml)with the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/storageclass-azuredisk-snapshot.yaml`

The output of the command resembles the following example:

`volumesnapshotclass.snapshot.storage.k8s.io/csi-azuredisk-vsc created`

Create a

[volume snapshot](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/azuredisk-volume-snapshot.yaml)from the PVC that was created earlier in this article.`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/azuredisk-volume-snapshot.yaml`

The output of the command resembles the following example:

`volumesnapshot.snapshot.storage.k8s.io/azuredisk-volume-snapshot created`

To verify that the snapshot was created correctly, run the following command:

`kubectl describe volumesnapshot azuredisk-volume-snapshot`

The output of the command resembles the following example:

`Name: azuredisk-volume-snapshot Namespace: default Labels: <none> Annotations: API Version: snapshot.storage.k8s.io/v1 Kind: VolumeSnapshot Metadata: Creation Timestamp: 2020-08-27T05:27:58Z Finalizers: snapshot.storage.kubernetes.io/volumesnapshot-as-source-protection snapshot.storage.kubernetes.io/volumesnapshot-bound-protection Generation: 1 Resource Version: 714582 Self Link: /apis/snapshot.storage.k8s.io/v1/namespaces/default/volumesnapshots/azuredisk-volume-snapshot UID: dd953ab5-6c24-42d4-ad4a-f33180e0ef87 Spec: Source: Persistent Volume Claim Name: pvc-azuredisk Volume Snapshot Class Name: csi-azuredisk-vsc Status: Bound Volume Snapshot Content Name: snapcontent-dd953ab5-6c24-42d4-ad4a-f33180e0ef87 Creation Time: 2020-08-31T05:27:59Z Ready To Use: true Restore Size: 10Gi Events: <none>`


### Create a new PVC based on a volume snapshot

You can create a new PVC based on a volume snapshot.

Use the snapshot created in the previous step, and create a

[new PVC](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/pvc-azuredisk-snapshot-restored.yaml)and a[new pod](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/nginx-pod-restored-snapshot.yaml)to consume it:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/pvc-azuredisk-snapshot-restored.yaml kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/nginx-pod-restored-snapshot.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk-snapshot-restored created pod/nginx-restored created`

To make sure it's the same PVC created before, check the contents by running the following command:

`kubectl exec nginx-restored -- ls /mnt/azuredisk`

The output of the command resembles the following example:

`lost+found outfile test.txt`


We can still see our previously created `test.txt`

file as expected.

## Clone volumes

A cloned volume is defined as a duplicate of an existing Kubernetes volume. For more information on cloning volumes in Kubernetes, see [volume cloning](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#volume-cloning).

Create a

[cloned volume](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml)of the[previously created](#create-azure-disk-pvs-using-built-in-storage-classes)`azuredisk-pvc`

and a[new pod](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml)to consume it.`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/cloning/pvc-azuredisk-cloning.yaml kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk-cloning created pod/nginx-restored-cloning created`

You can verify the content of the cloned volume by running the following command and confirming the file

`test.txt`

is created:`kubectl exec nginx-restored-cloning -- ls /mnt/azuredisk`

The output of the command resembles the following example:

`lost+found outfile test.txt`


## Resize an Azure Disk PV without downtime

You can request a larger volume for a PVC. Edit the PVC object, and specify a larger size. This change triggers the expansion of the underlying volume that backs the PV.

Note

A new PV is never created to satisfy the claim. Instead, an existing volume is resized.

In AKS, the built-in `managed-csi`

storage class already supports expansion, so use the [previously created](#create-azure-disk-pvs-using-built-in-storage-classes) one. The PVC requested a 10-Gi persistent volume. You can confirm by running the following command:

```
kubectl exec -it nginx-azuredisk -- df -h /mnt/azuredisk
```


The output of the command resembles the following example:

```
Filesystem Size Used Avail Use% Mounted on
/dev/sdc 9.8G 42M 9.8G 1% /mnt/azuredisk
```


Expand the PVC by increasing the

`spec.resources.requests.storage`

field running the following command:`kubectl patch pvc pvc-azuredisk --type merge --patch '{"spec": {"resources": {"requests": {"storage": "15Gi"}}}}'`

Note

Shrinking PVs is currently not supported. Trying to patch an existing PVC with a smaller size than the current one leads to the following error message:

`The persistentVolumeClaim "pvc-azuredisk" is invalid: spec.resources.requests.storage: Forbidden: field can not be less than previous value.`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk patched`

Run the following command to confirm the volume size increased:

`kubectl get pv`

The output of the command resembles the following example:

`NAME CAPACITY ACCESS MODES RECLAIM POLICY STATUS CLAIM STORAGECLASS REASON AGE pvc-391ea1a6-0191-4022-b915-c8dc4216174a 15Gi RWO Delete Bound default/pvc-azuredisk managed-csi 2d2h (...)`

And after a few minutes, run the following commands to confirm the size of the PVC:

`kubectl get pvc pvc-azuredisk`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE pvc-azuredisk Bound pvc-391ea1a6-0191-4022-b915-c8dc4216174a 15Gi RWO managed-csi 2d2h`

Run the following command to confirm the size of the disk inside the pod:

`kubectl exec -it nginx-azuredisk -- df -h /mnt/azuredisk`

The output of the command resembles the following example:

`Filesystem Size Used Avail Use% Mounted on /dev/sdc 15G 46M 15G 1% /mnt/azuredisk`


If your pod has *multiple containers*, you can specify which container by running the following command:

```
kubectl exec -it nginx-azuredisk -c <ContainerName> -- df -h /mnt/azuredisk
```


## Windows containers

The Azure Disk CSI driver supports Windows nodes and containers. If you want to use Windows containers, follow the [Windows containers quickstart](learn/quick-kubernetes-deploy-cli) to add a Windows node pool.

After you have a Windows node pool, you can now use the built-in storage classes like

`managed-csi`

. You can deploy an example[Windows-based stateful set](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/windows/statefulset.yaml)that saves timestamps into the file`data.txt`

by running the following[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/windows/statefulset.yaml`

The output of the command resembles the following example:

`statefulset.apps/busybox-azuredisk created`

To validate the content of the volume, run the following command:

`kubectl exec -it statefulset-azuredisk-win-0 -- powershell -c "type c:/mnt/azuredisk/data.txt"`

The output of the command resembles the following example:

`2020-08-27 08:13:41Z 2020-08-27 08:13:42Z 2020-08-27 08:13:44Z (...)`


## On-demand bursting

On-demand disk bursting model allows disk bursts whenever its needs exceed its current capacity. This model generates extra charges anytime the disk bursts. On-demand bursting is only available for premium SSDs larger than 512 GiB. For more information on premium SSDs provisioned IOPS and throughput per disk, see [Premium SSD size](/en-us/azure/virtual-machines/disks-types#premium-ssds). Alternatively, credit-based bursting is where the disk will burst only if it has burst credits accumulated in its credit bucket. Credit-based bursting doesn't generate extra charges when the disk bursts. Credit-based bursting is only available for premium SSDs 512 GiB and smaller, and standard SSDs 1,024 GiB and smaller. For more information on on-demand bursting, see [On-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting).

Important

The default `managed-csi-premium`

storage class has on-demand bursting disabled and uses credit-based bursting. Any premium SSD dynamically created by a persistent volume claim based on the default `managed-csi-premium`

storage class also has on-demand bursting disabled.

To create a premium SSD persistent volume with [on-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting) enabled, you can create a new storage class with the [enableBursting](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/docs/driver-parameters.md) parameter set to `true`

as shown in the following YAML template. For more information on enabling on-demand bursting, see [On-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting). For more information on building your own storage class with on-demand bursting enabled, see [Create a Burstable Managed CSI Premium Storage Class](https://github.com/Azure-Samples/burstable-managed-csi-premium).

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: burstable-managed-csi-premium
provisioner: disk.csi.azure.com
parameters:
skuname: Premium_LRS
enableBursting: "true"
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```


## Clean up resources

When you're done with the resources created in this article, you can remove them using the
`kubectl delete`

command.

```
# Remove the pod
kubectl delete -f azure-pvc-disk.yaml
# Remove the persistent volume claim
kubectl delete -f azure-pvc.yaml
```


## Provision Azure Files PVs

Azure Files supports Azure Premium file shares. The minimum file share capacity is 100 GiB. We recommend using Azure Premium file shares instead of Standard file shares because Premium file shares offer higher performance, low-latency disk support for I/O-intensive workloads. With Azure Files shares, there's no limit as to how many can be mounted on a node. For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

When you use storage CSI drivers on AKS, there are two more built-in `StorageClasses`

that uses the Azure Files CSI storage drivers. The other CSI storage classes are created with the cluster alongside the in-tree default storage classes.

`azurefile-csi`

: Uses Azure Standard Storage to create an Azure file share.`azurefile-csi-premium`

: Uses Azure Premium Storage to create an Azure file share.

The reclaim policy on both storage classes ensures that the underlying Azure files share is deleted when the respective PV is deleted. Since the storage classes also configure the file shares to be expandable, you just need to edit the [PVC](concepts-storage#persistent-volume-claims) with the new size.

Note

To have the best experience with Azure Files, follow these best practices. The location to configure mount options (`mountOptions`

) depends on whether you're provisioning dynamic or static persistent volumes.

- If you're dynamically provisioning a volume with a storage class, specify the mount options on the storage class object (kind:
`StorageClass`

). - If you're statically provisioning a volume, specify the mount options on the PersistentVolume object (kind:
`PersistentVolume`

). - If you're mounting the file share as an inline volume, specify the mount options on the Pod object (kind:
`Pod`

).

We recommend FIO when running benchmarking tests. For more information, see [benchmarking tools and tests](/en-us/azure/storage/files/nfs-performance#benchmarking-tools-and-tests).

A storage class is used to define how an Azure file share is created. A storage account is automatically created in the [node resource group](faq) for use with the storage class to hold the Azure files share. Choose one of the following [Azure storage redundancy SKUs](/en-us/azure/storage/common/storage-redundancy) for *skuName*:

**Standard_LRS**: Standard locally redundant storage**Standard_GRS**: Standard geo-redundant storage**Standard_ZRS**: Standard zone-redundant storage**Standard_RAGRS**: Standard read-access geo-redundant storage**Standard_RAGZRS**: Standard read-access geo-zone-redundant storage**Premium_LRS**: Premium locally redundant storage**Premium_ZRS**: Premium zone-redundant storage

For more information on Kubernetes storage classes for Azure Files, see [Kubernetes Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/#azure-file).

Create a file named

`azure-file-sc.yaml`

and copy in the following example manifest. For more information on`mountOptions`

, see the[Mount options](#mount-options)section.`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: my-azurefile provisioner: file.csi.azure.com # replace with "kubernetes.io/azure-file" if aks version is less than 1.21 allowVolumeExpansion: true mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict - actimeo=30 - nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks parameters: skuName: Premium_LRS`

Create the storage class using the

command.`kubectl apply`

`kubectl apply -f azure-file-sc.yaml`


### Create a PVC

A PVC uses the storage class object to dynamically provision an Azure file share. You can use the following YAML to create a PVC that's *100 GB* in size with *ReadWriteMany* access. For more information on access modes, see [Kubernetes persistent volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes).

Create a file named

`azure-file-pvc.yaml`

and copy in the following YAML. Make sure the`storageClassName`

matches the storage class you created in the previous step.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: my-azurefile spec: accessModes: - ReadWriteMany storageClassName: my-azurefile resources: requests: storage: 100Gi`

Note

If using the

`Premium_LRS`

SKU for your storage class, the minimum value for`storage`

must be`100Gi`

.Create the PVC using the

command.`kubectl apply`

`kubectl apply -f azure-file-pvc.yaml`

Once completed, the file share is created. A Kubernetes secret is also created that includes connection information and credentials. You can use the

command to view the status of the PVC:`kubectl get`

`kubectl get pvc my-azurefile`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE my-azurefile Bound pvc-8436e62e-a0d9-11e5-8521-5a8664dc0477 100Gi RWX my-azurefile 5m`


### Mount the PVC

The following YAML creates a pod that uses the PVC *my-azurefile* to mount the Azure Files file share at the */mnt/azure* path. For Windows Server containers, specify a `mountPath`

using the Windows path convention, such as *"D:"*.

Create a file named

`azure-pvc-files.yaml`

, and copy in the following YAML. Make sure the`claimName`

matches the PVC you created in the previous step.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: /mnt/azure name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: my-azurefile`

Create the pod using the

command.`kubectl apply`

`kubectl apply -f azure-pvc-files.yaml`

You now have a running pod with your Azure Files file share mounted in the

*/mnt/azure*directory. This configuration can be seen when inspecting your pod using thecommand. The following condensed example output shows the volume mounted in the container.`kubectl describe`

`Containers: mypod: Container ID: docker://053bc9c0df72232d755aa040bfba8b533fa696b123876108dec400e364d2523e Image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine Image ID: docker-pullable://nginx@sha256:d85914d547a6c92faa39ce7058bd7529baacab7e0cd4255442b04577c4d1f424 State: Running Started: Fri, 01 Mar 2019 23:56:16 +0000 Ready: True Mounts: /mnt/azure from volume (rw) /var/run/secrets/kubernetes.io/serviceaccount from default-token-8rv4z (ro) [...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: my-azurefile ReadOnly: false [...]`


### Mount options

For Kubernetes versions 1.13.0 and later, the default values for `fileMode`

and `dirMode`

are `0777`

. When dynamically provisioning PVs using a storage class, you can define mount options directly in the storage class manifest. For details, see [Mount options](https://kubernetes.io/docs/concepts/storage/storage-classes/#mount-options). The following example demonstrates setting these permissions to `0777`

:

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: my-azurefile
provisioner: file.csi.azure.com # replace with "kubernetes.io/azure-file" if aks version is less than 1.21
allowVolumeExpansion: true
mountOptions:
- dir_mode=0777
- file_mode=0777
- uid=0
- gid=0
- mfsymlinks
- cache=strict
- actimeo=30
- nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks
parameters:
skuName: Premium_LRS
```


## Storage class parameters for dynamic volumes

The following table includes parameters you can use to define a custom storage class for your PVC.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| accountAccessTier |
|

`Hot`

or `Cool`

, and Premium account can only choose `Premium`

.`102400`

`true`

or `false`

`false`

`true`

or `false`

`false`

`true`

or `false`

`false`

`eastus`

.`true`

or `false`

`false`

1`privateEndpoint`

is specified, a private endpoint is created for the storage account. For other cases, a service endpoint is created by default.`privateEndpoint`

`smb`

, `nfs`

`smb`

`true`

or `false`

`false`

`true`

or `false`

`false`

`accountname.privatelink.file.core.windows.net`

.`accountname.file.core.windows.net`

or other sovereign cloud account address.[Access tier for file share](/en-us/azure/storage/files/storage-files-planning#storage-tiers)`TransactionOptimized`

(default), `Hot`

, and `Cool`

. Premium storage account type for file shares only.`storageAccountType`

)`Standard_LRS`

, `Standard_ZRS`

, `Standard_GRS`

, `Standard_RAGRS`

, `Standard_RAGZRS`

,`Premium_LRS`

, `Premium_ZRS`

, `StandardV2_LRS`

, `StandardV2_ZRS`

, `StandardV2_GRS`

, `StandardV2_GZRS`

, `PremiumV2_LRS`

, `PremiumV2_ZRS`

`Standard_LRS`

Minimum file share size for Premium account type is 100 GB.

ZRS account type is supported in limited regions.

NFS file share only supports Premium account type.

Standard V2 SKU names are for

[Azure Files provisioned v2 model](/en-us/azure/storage/files/understanding-billing#provisioned-v2-model).`core.windows.net`

, `core.chinacloudapi.cn`

, etc.`core.windows.net`

.[Tags](/en-us/azure/azure-resource-manager/management/tag-resources)are created in new storage account.1 If the storage account is created by the driver, then you only need to specify
`networkEndpointType: privateEndpoint`

parameter in storage class. The CSI driver creates the
private endpoint and private DNS zone (named `privatelink.file.core.windows.net`

) together with the
account. If you bring your own storage account, then you need to
[create the private endpoint](/en-us/azure/storage/common/storage-private-endpoints) for the storage account. If you're
using Azure Files storage in a network isolated cluster, you must create a custom storage class with
"networkEndpointType: privateEndpoint". You can follow this sample for reference:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: azurefile-csi
provisioner: file.csi.azure.com
allowVolumeExpansion: true
parameters:
skuName: Premium_LRS # available values: Premium_LRS, Premium_ZRS, Standard_LRS, Standard_GRS, Standard_ZRS, Standard_RAGRS, Standard_RAGZRS
networkEndpointType: privateEndpoint
reclaimPolicy: Delete
volumeBindingMode: Immediate
mountOptions:
- dir_mode=0777 # modify this permission if you want to enhance the security
- file_mode=0777
- mfsymlinks
- cache=strict # https://linux.die.net/man/8/mount.cifs
- nosharesock # reduce probability of reconnect race
- actimeo=30 # reduce latency for metadata-heavy workload
- nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks
```


## Static provisioning parameters for PVs

The following table includes parameters you can use to define a PV.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| volumeAttributes.resourceGroup | Specify an Azure resource group name. | myResourceGroup | No | If empty, driver uses the same resource group name as current cluster. |
| volumeAttributes.storageAccount | Specify an existing Azure storage account name. | storageAccountName | Yes | |
| volumeAttributes.shareName | Specify an Azure file share name. | fileShareName | Yes | |
| volumeAttributes.folderName | Specify a folder name in Azure file share. | folderName | No | If folder name doesn't exist in file share, mount would fail. |
| volumeAttributes.protocol | Specify file share protocol. | `smb` , `nfs` |
No | `smb` |
| volumeAttributes.server | Specify Azure storage account server address | Existing server address, for example `accountname.privatelink.file.core.windows.net` . |
No | If empty, driver uses default `accountname.file.core.windows.net` or other sovereign cloud account address. |

## Create a PV snapshot class

The Azure Files CSI driver supports creating [snapshots of persistent volumes](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html) and the underlying file shares.

Create a

[volume snapshot class](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/snapshot/volumesnapshotclass-azurefile.yaml)with the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/snapshot/volumesnapshotclass-azurefile.yaml`

The output of the command resembles the following example:

`volumesnapshotclass.snapshot.storage.k8s.io/csi-azurefile-vsc created`

Create a

[volume snapshot](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/snapshot/volumesnapshot-azurefile.yaml)from the PVC created earlier (`pvc-azurefile`

).`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/snapshot/volumesnapshot-azurefile.yaml`

The output of the command resembles the following example:

`volumesnapshot.snapshot.storage.k8s.io/azurefile-volume-snapshot created`

Verify the snapshot was created correctly by running the following command:

`kubectl describe volumesnapshot azurefile-volume-snapshot`

The output of the command resembles the following example:

`Name: azurefile-volume-snapshot Namespace: default Labels: <none> Annotations: API Version: snapshot.storage.k8s.io/v1beta1 Kind: VolumeSnapshot Metadata: Creation Timestamp: 2020-08-27T22:37:41Z Finalizers: snapshot.storage.kubernetes.io/volumesnapshot-as-source-protection snapshot.storage.kubernetes.io/volumesnapshot-bound-protection Generation: 1 Resource Version: 955091 Self Link: /apis/snapshot.storage.k8s.io/v1beta1/namespaces/default/volumesnapshots/azurefile-volume-snapshot UID: c359a38f-35c1-4fb1-9da9-2c06d35ca0f4 Spec: Source: Persistent Volume Claim Name: pvc-azurefile Volume Snapshot Class Name: csi-azurefile-vsc Status: Bound Volume Snapshot Content Name: snapcontent-c359a38f-35c1-4fb1-9da9-2c06d35ca0f4 Ready To Use: false Events: <none>`


## Resize an Azure Files PV

You can request a larger volume for a PVC. Edit the PVC object, and specify a larger size. This change triggers the expansion of the underlying volume that backs the PV.

Note

A new PV is never created to satisfy the claim. Instead, an existing volume is resized. Shrinking persistent volumes is currently not supported.

In AKS, the built-in `azurefile-csi`

storage class already supports expansion, so use the PVC we created earlier with this storage class. The PVC requested a 100 GiB file share. We can confirm that by running:

```
kubectl exec -it nginx-azurefile -- df -h /mnt/azurefile
```


The output of the command resembles the following example:

```
Filesystem Size Used Avail Use% Mounted on
//f149b5a219bd34caeb07de9.file.core.windows.net/pvc-5e5d9980-da38-492b-8581-17e3cad01770 100G 128K 100G 1% /mnt/azurefile
```


Expand the PVC by increasing the

`spec.resources.requests.storage`

field:`kubectl patch pvc pvc-azurefile --type merge --patch '{"spec": {"resources": {"requests": {"storage": "200Gi"}}}}'`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azurefile patched`

Verify that both the PVC and the file system inside the pod show the new size:

`kubectl get pvc pvc-azurefile NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE pvc-azurefile Bound pvc-5e5d9980-da38-492b-8581-17e3cad01770 200Gi RWX azurefile-csi 64m kubectl exec -it nginx-azurefile -- df -h /mnt/azurefile Filesystem Size Used Avail Use% Mounted on //f149b5a219bd34caeb07de9.file.core.windows.net/pvc-5e5d9980-da38-492b-8581-17e3cad01770 200G 128K 200G 1% /mnt/azurefile`


## Use a PV with private Azure Files storage (private endpoint)

If your Azure Files resources are protected with a private endpoint, you must create your own storage class. Make sure to configure your [DNS settings to resolve the private endpoint IP address to the FQDN of the connection string](/en-us/azure/private-link/private-endpoint-dns#azure-services-dns-zone-configuration).

Customize the following parameters:

`resourceGroup`

: The resource group where the storage account is deployed.`storageAccount`

: The storage account name.`server`

: The FQDN of the storage account's private endpoint.

Create a file named

`private-azure-file-sc.yaml`

, and then paste the following example manifest in the file. Replace the values for`<resourceGroup>`

and`<storageAccountName>`

. For example:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: private-azurefile-csi provisioner: file.csi.azure.com allowVolumeExpansion: true parameters: resourceGroup: <resourceGroup> storageAccount: <storageAccountName> server: <storageAccountName>.file.core.windows.net reclaimPolicy: Delete volumeBindingMode: Immediate mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict # https://linux.die.net/man/8/mount.cifs - nosharesock # reduce probability of reconnect race - actimeo=30 # reduce latency for metadata-heavy workload`

Create the storage class by using the

`kubectl apply`

command:`kubectl apply -f private-azure-file-sc.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/private-azurefile-csi created`

Create a file named

`private-pvc.yaml`

, and then paste the following example manifest in the file:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: private-azurefile-pvc spec: accessModes: - ReadWriteMany storageClassName: private-azurefile-csi resources: requests: storage: 100Gi`

Create the PVC by using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f private-pvc.yaml`


## Use Managed Identity to access Azure Files storage (Preview)

Azure Files now supports managed identity-based authentication for SMB access. With this capability, your applications running in AKS can securely access Azure Files shares without the need to store or manage storage account keys or credentials. Managed identities provide a streamlined and secure authentication mechanism, simplifying access management and reducing the risk associated with credential exposure. You can create a dynamic volume or a static volume.

Note

Managed identity support for Azure Files in AKS is available in preview starting with AKS version 1.34 on Linux nodes.

To enable managed identity for dynamically provisioned volumes, follow these steps:

Create a storage class with managed identity enabled using a YAML file, for example,

`azurefile-csi-managed-identity.yaml`

with the following sample content. Set`mountWithManagedIdentity: "true"`

under`parameters`

:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azurefile-csi provisioner: file.csi.azure.com parameters: resourceGroup: EXISTING_RESOURCE_GROUP_NAME # optional, node resource group by default if it's not provided storageAccount: EXISTING_STORAGE_ACCOUNT_NAME # optional, a new account will be created if it's not provided mountWithManagedIdentity: "true" # optional, clientID of the managed identity, kubelet identity would be used by default if it's not provided clientID: "xxxxx-xxxx-xxx-xxx-xxxxxxx" reclaimPolicy: Delete volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - dir_mode=0777 # modify this permission if you want to enhance the security - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict # https://linux.die.net/man/8/mount.cifs - nosharesock # reduce probability of reconnect race - actimeo=30 # reduce latency for metadata-heavy workload - nobrl # disable sending byte range lock requests to the server`

Apply this storage class by running the following command:

`kubectl apply -f azurefile-csi-managed-identity.yaml`

Deploy your

**StatefulSet**or workload using the new storage class that references this PVC to ensure that the volume is provisioned using managed identity authentication. In your PVC manifest, set`storageClassName: azurefile-csi-managed-identity`

. For example:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azurefile-managed-identity-pvc spec: accessModes: - ReadWriteMany storageClassName: azurefile-csi-managed-identity resources: requests: storage: 100Gi`


## Learn about Azure Files NFS

Azure Files supports the
[NFS v4.1 protocol](/en-us/azure/storage/files/storage-files-how-to-create-nfs-shares). NFS version 4.1
support for Azure Files provides you with a fully managed NFS system as a service built on highly
available, highly durable distributed resilient storage platform.

This option is optimized for random access workloads with in-place data updates and provides full POSIX file system support. This section shows you how to use NFS shares with the Azure File CSI driver on an AKS cluster.

Note

You can use a private endpoint instead of allowing access to the selected VNet.

This section explains how to maximize performance and security when using Azure Files NFS 4.1 with AKS. Learn how to:

Optimize NFS read and write size settings

Create and configure an NFS storage class

Deploy workloads that use NFS-backed volumes

Enable Encryption in Transit (EiT) to protect data as it moves between your AKS cluster and Azure Files.


This section provides information about how to approach performance tuning NFS with the Azure Files
CSI driver with the `rsize`

(read size) and `wsize`

(write size) options. The `rsize`

and `wsize`

options set the maximum transfer size of an NFS operation. If `rsize`

or `wsize`

aren't specified on
mount, the client and server negotiate the largest size supported by the two. Currently, both Azure
Files and modern Linux distributions support read and write sizes as large as 1,048,576 bytes (1
MiB).

Optimal performance is based on efficient client-server communication. Increasing or decreasing the
**mount** read and write option size values can improve NFS performance. The default size of the
read/write packets transferred between client and server are 8 KB for NFS version 2, and 32 KB for
NFS version 3 and 4. These defaults might be too large or too small. Reducing the `rsize`

and
`wsize`

might improve NFS performance in a congested network by sending smaller packets for each
NFS-read reply and write request. However, this reduction can increase the number of packets needed
to send data across the network, increasing total network traffic and CPU utilization on the client
and server.

It's important that you perform testing to find an `rsize`

and `wsize`

that sustains efficient
packet transfer, where it doesn't decrease throughput and increase latency.

For example, to configure a maximum `rsize`

and `wsize`

of 256-KiB, configure the `mountOptions`

in
the storage class as follows:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: azurefile-csi-nfs
provisioner: file.csi.azure.com
allowVolumeExpansion: true
parameters:
protocol: nfs
mountOptions:
- nconnect=4
- noresvport
- actimeo=30
- rsize=262144
- wsize=262144
```


## Other storage class examples

## Windows containers

The Azure Files CSI driver also supports Windows nodes and containers. To use Windows containers, follow the [Windows containers quickstart](learn/quick-windows-container-deploy-cli) to add a Windows node pool.

After you have a Windows node pool, use the built-in storage classes like

`azurefile-csi`

or create a custom one. You can deploy an example[Windows-based stateful set](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/windows/statefulset.yaml)that saves timestamps into a file`data.txt`

by running the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/windows/statefulset.yaml`

The output of the command resembles the following example:

`statefulset.apps/busybox-azurefile created`

Validate the contents of the volume by running the following

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command:`kubectl exec -it busybox-azurefile-0 -- cat c:\\mnt\\azurefile\\data.txt # on Linux or MacOS Bash kubectl exec -it busybox-azurefile-0 -- cat c:\mnt\azurefile\data.txt # on Windows Powershell or CMD`

The output of the commands resembles the following example:

`2020-08-27 22:11:01Z 2020-08-27 22:11:02Z 2020-08-27 22:11:04Z (...)`


## Next steps

- For Azure Files CSI driver parameters, see
[CSI driver parameters](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/docs/driver-parameters.md#static-provisionbring-your-own-file-share). - For more information about disk-based storage solutions, see
[Disk-based solutions in AKS](/en-us/azure/cloud-adoption-framework/scenarios/app-platform/aks/storage#disk-based-solutions). - For more information about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service](operator-best-practices-storage). - For more information about Azure ultra disk, see [Use ultra disks on Azure Kubernetes Service (AKS)][use-ultra-disks].
- For more information about Azure tags, see
[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags).


---

<!-- DOCUMENTO FUSIONADO: policy-reference.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/policy-reference -->

# Azure Policy built-in definitions for Azure Kubernetes Service

[[Preview]: [Image Integrity] Kubernetes clusters should only use images signed by notation](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fcf426bb8-b320-4321-8545-1b784a5df3a4) |
Use images signed by notation to ensure that images come from trusted sources and will not be maliciously modified. For more info, visit [https://aka.ms/aks/image-integrity](https://aka.ms/aks/image-integrity) |
Audit, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ImageIntegrityNotationVerification.json) |
[[Preview]: Azure Backup Extension should be installed in AKS clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffda9cd0b-094c-4cd5-ac2a-5e06e5277c45) |
Ensure protection installation of backup extension in your AKS Clusters to leverage Azure Backup. Azure Backup for AKS is a secure and cloud native data protection solution for AKS clusters |
AuditIfNotExists, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/Kubernetes_InstallAzureBackupExtension_Audit.json) |
[[Preview]: Azure Backup should be enabled for AKS clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0b0434ec-2bad-4229-965f-bb7ae5a71257) |
Ensure protection of your AKS Clusters by enabling Azure Backup. Azure Backup for AKS is a secure and cloud native data protection solution for AKS clusters. |
AuditIfNotExists, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/Kubernetes_EnableAzureBackup_Audit.json) |
[[Preview]: Azure Kubernetes Service Managed Clusters should be Zone Redundant](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2dec5f47-bc40-40d1-8c7d-a39d9d6808d1) |
Azure Kubernetes Service Managed Clusters can be configured to be Zone Redundant or not. The policy checks the node pools in the cluster and ensures that avaialbilty zones are set for all the node pools. |
Audit, Deny, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Resilience/ContainerService_managedclusters_ZoneRedundant_Audit.json) |
[[Preview]: Deploy Image Integrity on Azure Kubernetes Service](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5dc99dae-cfb2-42cc-8762-9aae02b74e27) |
Deploy both Image Integrity and Policy Add-Ons Azure Kubernetes clusters. For more info, visit [https://aka.ms/aks/image-integrity](https://aka.ms/aks/image-integrity) |
DeployIfNotExists, Disabled |
[1.2.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_ImageIntegrity_DINE.json) |
[[Preview]: Install Azure Backup Extension in AKS clusters (Managed Cluster) with a given tag.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fbdff5235-9f40-4a32-893f-38a03d5d607c) |
Installing the Azure Backup Extension is a pre-requisite for protecting your AKS Clusters. Enforce installation of backup extension on all AKS clusters containing a given tag. Doing this can help you manage Backup of AKS Clusters at scale. |
AuditIfNotExists, DeployIfNotExists, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/Kubernetes_InstallAzureBackupExtensionWithTag_DINE.json) |
[[Preview]: Install Azure Backup Extension in AKS clusters (Managed Cluster) without a given tag.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9a021087-bba6-42fd-b535-bba75297566b) |
Installing the Azure Backup Extension is a pre-requisite for protecting your AKS Clusters. Enforce installation of backup extension on all AKS clusters without a particular tag value. Doing this can help you manage Backup of AKS Clusters at scale. |
AuditIfNotExists, DeployIfNotExists, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Backup/Kubernetes_InstallAzureBackupExtensionWithoutTag_DINE.json) |
[[Preview]: Kubernetes cluster containers should use only allowed sysctl interfaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5e5a0673-649e-4d50-bf9d-5a387a4e2081) |
Containers should use only allowed sysctl interfaces in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedSysctlInterfaces.json) |
[[Preview]: Kubernetes cluster should implement accurate Pod Disruption Budgets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd9e8f2c1-4c5a-4f5c-8b5a-2abf1e9f7b4d) |
Prevents faulty Pod Disruption Budgets, ensuring a minimum number of operational pods. Refer to the official Kubernetes documentation for details. Relies on Gatekeeper data replication and syncs all Deployment, StatefulSet, and PodDisruptionBudget resources scoped to it into OPA. Before applying this policy, ensure that the synced resources won't strain your memory capacity. All resources of these kinds across namespaces will sync. Note: currently in preview for Kubernetes Service (AKS). |
Audit, Deny, Disabled |
[1.3.1-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/DisallowedBadPodDisruptionBudgets.json) |
[[Preview]: Kubernetes clusters should restrict creation of given resource type](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb81f454c-eebb-4e4f-9dfe-dca060e8a8fd) |
Given Kubernetes resource type should not be deployed in certain namespace. |
Audit, Deny, Disabled |
[2.3.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockResource.json) |
[[Preview]: Prevents containers from being ran as root by setting runAsNotRoot to true.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2fe7ba7d-f670-41f5-8b70-b61dc7dfbe18) |
Setting runAsNotRoot to true increases security by preventing containers from being ran as root. |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateRunAsNonRoot.json) |
[[Preview]: Prevents init containers from being ran as root by setting runAsNotRoot to true.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffed6510d-00b9-40db-a347-933125a6a327) |
Setting runAsNotRoot to true increases security by preventing containers from being ran as root. |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateRunAsNonRootInitContainers.json) |
[[Preview]: Sets Kubernetes cluster container securityContext.runAsUser fields to 1000, a non-root user id](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa8e3ce3c-cac3-4402-a28a-03ee3ede9790) |
Reduces attack surface introduced by escalating privileges as root user in the presence of security vulnerabilities. |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateRunAsNonRootUserContainers.json) |
[[Preview]: Sets Kubernetes cluster containers' secure computing mode profile type to RuntimeDefault if not present.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F6f87d474-38a9-46c9-bdfe-d7fa3b9836bf) |
Setting secure computing mode profile type for containers to prevent unauthorized and potentially harmful system calls to the kernel from user space. |
Mutate, Disabled |
[1.2.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateSeccompProfileContainers.json) |
[[Preview]: Sets Kubernetes cluster init containers securityContext.runAsUser fields to 1000, a non-root user id](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F97de439f-fd35-4d43-a693-3644f51a51fd) |
Reduces attack surface introduced by escalating privileges as root user in the presence of security vulnerabilities. |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateRunAsNonRootUserInitContainers.json) |
[[Preview]: Sets Kubernetes cluster init containers' secure computing mode profile type to RuntimeDefault if not present.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F6bcd4321-fb89-4e3e-bf6c-999c13d47f43) |
Setting secure computing mode profile type for init containers to prevent unauthorized and potentially harmful system calls to the kernel from user space. |
Mutate, Disabled |
[1.2.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateSeccompProfileInitContainers.json) |
[[Preview]: Sets Kubernetes cluster Pod securityContext.runAsUser fields to 1000, a non-root user id](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffe74a23d-79e4-401c-bd0d-fd7a5b35af32) |
Reduces attack surface introduced by escalating privileges as root user in the presence of security vulnerabilities. |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateRunAsNonRootUserPod.json) |
[[Preview]: Sets Privilege escalation in the Pod spec in init containers to false.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F4ee3ee6a-96ea-4d25-9c00-17f11d2e02c8) |
Setting Privilege escalation to false in init containers increases security by preventing containers from allowing privilege escalation such as via set-user-ID or set-group-ID file mode. |
Mutate, Disabled |
[1.2.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutatePrivilegeEscalationInitContainers.json) |
[[Preview]: Sets Privilege escalation in the Pod spec to false.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd77df159-718b-4aca-b94b-8e8890a98231) |
Setting Privilege escalation to false increases security by preventing containers from allowing privilege escalation such as via set-user-ID or set-group-ID file mode. |
Mutate, Disabled |
[1.2.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutatePrivilegeEscalationContainers.json) |
[[Preview]: Sets UnhealthyPodEvictionPolicy to 'AlwaysAllow'](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5c58d54b-87f0-4dcd-83ea-e855fc988997) |
Sets Pod Disruption Budget's UnhealthyPodEvictionPolicy to 'AlwaysAllow' to allow for evicting even unhealthy pods when performing cluster administration |
Mutate, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateUnhealthyPodEvictionPolicy.json) |
[Authorized IP ranges should be defined on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0e246bcf-5f6f-4f87-bc6f-775d4712c7ea) |
Restrict access to the Kubernetes Service Management API by granting API access only to IP addresses in specific ranges. It is recommended to limit access to authorized IP ranges to ensure that only applications from allowed networks can access the cluster. |
Audit, Disabled |
[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableIpRanges_KubernetesService_Audit.json) |
[Azure Kubernetes Clusters should disable SSH](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F28257686-e9db-403e-b9e2-a5eecbe03da9) |
Disable SSH gives you the ability to secure your cluster and reduce the attack surface. To learn more, visit: aka.ms/aks/disablessh |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_DisableSSH_Audit.json) |
[Azure Kubernetes Clusters should enable Container Storage Interface(CSI)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc5110b6e-5272-4989-9935-59ad06fdf341) |
The Container Storage Interface (CSI) is a standard for exposing arbitrary block and file storage systems to containerized workloads on Azure Kubernetes Service. To learn more, [https://aka.ms/aks-csi-driver](https://aka.ms/aks-csi-driver) |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CSI.json) |
[Azure Kubernetes Clusters should enable Key Management Service (KMS)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fdbbdc317-9734-4dd8-9074-993b29c69008) |
Use Key Management Service (KMS) to encrypt secret data at rest in etcd for Kubernetes cluster security. Learn more at: [https://aka.ms/aks/kmsetcdencryption](https://aka.ms/aks/kmsetcdencryption). |
Audit, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_EnableKMS.json) |
[Azure Kubernetes Clusters should use Azure CNI](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F46238e2f-3f6f-4589-9f3f-77bed4116e67) |
Azure CNI is a prerequisite for some Azure Kubernetes Service features, including Azure network policies, Windows node pools and virtual nodes add-on. Learn more at: [https://aka.ms/aks-azure-cni](https://aka.ms/aks-azure-cni) |
Audit, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_EnableCNI.json) |
[Azure Kubernetes Service clusters should be a member of an Azure Kubernetes Fleet Manager.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc7f49635-e3f0-4986-b072-90d0c7c3d4cd) |
Detect and report any AKS clusters that are not members of an Azure Kubernetes Fleet Manager. To learn more, visit [https://aka.ms/kubernetes-fleet/policy](https://aka.ms/kubernetes-fleet/policy) |
AuditIfNotExists, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Detect_Non_Fleet_Manager_Member_Audit.json) |
[Azure Kubernetes Service Clusters should disable Command Invoke](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F89f2d532-c53c-4f8f-9afa-4927b1114a0d) |
Disabling command invoke can enhance the security by avoiding bypass of restricted network access or Kubernetes role-based access control |
Audit, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_DisableRunCommand_Audit.json) |
[Azure Kubernetes Service Clusters should enable cluster auto-upgrade](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5c345cdf-2049-47e0-b8fe-b0e96bc2df35) |
AKS cluster auto-upgrade can ensure your clusters are up to date and don't miss the latest features or patches from AKS and upstream Kubernetes. Learn more at: [https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-cluster](/en-us/azure/aks/auto-upgrade-cluster). |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Autoupgrade_Cluster_Audit.json) |
[Azure Kubernetes Service Clusters should enable Image Cleaner](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Faf3c26b2-6fad-493e-9236-9c68928516ab) |
Image Cleaner performs automatic vulnerable, unused image identification and removal, which mitigates the risk of stale images and reduces the time required to clean them up. Learn more at: [https://aka.ms/aks/image-cleaner](https://aka.ms/aks/image-cleaner). |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_ImageCleaner_Audit.json) |
[Azure Kubernetes Service Clusters should enable Microsoft Entra ID integration](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F450d2877-ebea-41e8-b00c-e286317d21bf) |
AKS-managed Microsoft Entra ID integration can manage the access to the clusters by configuring Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership. Learn more at: [https://aka.ms/aks-managed-aad](https://aka.ms/aks-managed-aad). |
Audit, Disabled |
[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AAD_Integration_Audit.json) |
[Azure Kubernetes Service Clusters should enable node os auto-upgrade](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F04408ca5-aa10-42ce-8536-98955cdddd4c) |
AKS node OS auto-upgrade controls node-level OS security updates. Learn more at: [https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-image](/en-us/azure/aks/auto-upgrade-node-image). |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Autoupgrade_NodeOS_Audit.json) |
[Azure Kubernetes Service Clusters should enable workload identity](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2cc2e023-0dac-4046-875b-178f683929d5) |
Workload identity allows to assign a unique identity to each Kubernetes Pod and associate it with Azure AD protected resources such as Azure Key Vault, enabling secure access to these resources from within the Pod. Learn more at: [https://aka.ms/aks/wi](https://aka.ms/aks/wi). |
Audit, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_WorkloadIdentity_Audit.json) |
[Azure Kubernetes Service clusters should have Defender profile enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa1840de2-8088-4ea8-b153-b4c723e9cb01) |
Microsoft Defender for Containers provides cloud-native Kubernetes security capabilities including environment hardening, workload protection, and run-time protection. When you enable the SecurityProfile.AzureDefender on your Azure Kubernetes Service cluster, an agent is deployed to your cluster to collect security event data. Learn more about Microsoft Defender for Containers in [https://docs.microsoft.com/azure/defender-for-cloud/defender-for-containers-introduction?tabs=defender-for-container-arch-aks](/en-us/azure/defender-for-cloud/defender-for-containers-introduction) |
Audit, Disabled |
[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ASC_Azure_Defender_AKS_SecurityProfile_Audit.json) |
[Azure Kubernetes Service Clusters should have local authentication methods disabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F993c2fcd-2b29-49d2-9eb0-df2c3a730c32) |
Disabling local authentication methods improves security by ensuring that Azure Kubernetes Service Clusters should exclusively require Azure Active Directory identities for authentication. Learn more at: [https://aka.ms/aks-disable-local-accounts](https://aka.ms/aks-disable-local-accounts). |
Audit, Deny, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_DisableLocalAccounts_Deny.json) |
[Azure Kubernetes Service Clusters should use managed identities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fda6e2401-19da-4532-9141-fb8fbde08431) |
Use managed identities to wrap around service principals, simplify cluster management and avoid the complexity required to managed service principals. Learn more at: [https://aka.ms/aks-update-managed-identities](https://aka.ms/aks-update-managed-identities) |
Audit, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_MSI_Audit.json) |
[Azure Kubernetes Service Private Clusters should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F040732e8-d947-40b8-95d6-854c95024bf8) |
Enable the private cluster feature for your Azure Kubernetes Service cluster to ensure network traffic between your API server and your node pools remains on the private network only. This is a common requirement in many regulatory and industry compliance standards. |
Audit, Deny, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_PrivateCluster_Deny.json) |
[Azure Policy Add-on for Kubernetes service (AKS) should be installed and enabled on your clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F0a15ec92-a229-4763-bb14-0ea34a568f8d) |
Azure Policy Add-on for Kubernetes service (AKS) extends Gatekeeper v3, an admission controller webhook for Open Policy Agent (OPA), to apply at-scale enforcements and safeguards on your clusters in a centralized, consistent manner. |
Audit, Disabled |
[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AzurePolicyAddOn_Audit.json) |
[Azure running container images should have vulnerabilities resolved (powered by Microsoft Defender Vulnerability Management)](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F17f4b1cc-c55c-4d94-b1f9-2978f6ac2957) |
Container image vulnerability assessment scans your registry for commonly known vulnerabilities (CVEs) and provides a detailed vulnerability report for each image. This recommendation provides visibility to vulnerable images currently running in your Kubernetes clusters. Remediating vulnerabilities in container images that are currently running is key to improving your security posture, significantly reducing the attack surface for your containerized workloads. |
AuditIfNotExists, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/MDC_K8sRuningImagesVulnerabilityAssessmentBasedOnMDVM_Audit.json) |
[Both operating systems and data disks in Azure Kubernetes Service clusters should be encrypted by customer-managed keys](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7d7be79c-23ba-4033-84dd-45e2a5ccdd67) |
Encrypting OS and data disks using customer-managed keys provides more control and greater flexibility in key management. This is a common requirement in many regulatory and industry compliance standards. |
Audit, Deny, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_CMK_Deny.json) |
[Cannot Edit Individual Nodes](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F53a4a537-990c-495a-92e0-7c21a465442c) |
Cannot Edit Individual Nodes. Users should not edit individual nodes. Please edit node pools. Modifying individual nodes can lead to inconsistent settings, operational challenges, and potential security risks. |
Audit, Deny, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/CannotEditIndividualNodes.json) |
[Configure AKS clusters to automatically join the specified Azure Kubernetes Fleet Manager](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fcadd9445-aeb8-4ee4-b505-c279db2f737f) |
Detect and ensure that AKS clusters join a given Azure Kubernetes Fleet Manager. Optionally, select a look-up tag to specify what fleet update group to join. To learn more, visit [https://aka.ms/kubernetes-fleet/policy](https://aka.ms/kubernetes-fleet/policy) |
DeployIfNotExists, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Autojoin_Fleet_Manager_DINE.json) |
[Configure Azure Kubernetes Service clusters to enable Defender profile](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F64def556-fbad-4622-930e-72d1d5589bf5) |
Microsoft Defender for Containers provides cloud-native Kubernetes security capabilities including environment hardening, workload protection, and run-time protection. When you enable the SecurityProfile.Defender on your Azure Kubernetes Service cluster, an agent is deployed to your cluster to collect security event data. Learn more about Microsoft Defender for Containers: [https://docs.microsoft.com/azure/defender-for-cloud/defender-for-containers-introduction?tabs=defender-for-container-arch-aks](/en-us/azure/defender-for-cloud/defender-for-containers-introduction). |
DeployIfNotExists, Disabled |
[4.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ASC_Azure_Defender_AKS_SecurityProfile_DINE.json) |
[Configure installation of Flux extension on Kubernetes cluster](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff9175d5f-abc8-1dc3-bd3c-5d7476ada3d1) |
Install Flux extension on Kubernetes cluster to enable deployment of 'fluxconfigurations' in the cluster |
DeployIfNotExists, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-Extension-to-Kubernetes-cluster_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using Bucket source and secrets in KeyVault](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5174c1db-ca42-e0d4-b320-4f1cf6a1fa93) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Bucket. This definition requires a Bucket SecretKey stored in Key Vault. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/GitOps-Flux2-to-Kubernetes-cluster-Bucket-KVSecret_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using Git repository and HTTPS CA Certificate](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2630c91f-8a20-8f43-14a2-2485b648e2a9) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Git repository. This definition requires a HTTPS CA Certificate. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-to-Kubernetes-cluster-HTTPs-CA-Cert_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using Git repository and HTTPS secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fbf1a31be-3b79-5ba8-c9e0-9a8c9ad9f749) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Git repository. This definition requires a HTTPS key secret stored in Key Vault. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-to-Kubernetes-cluster-HTTPS-secrets_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using Git repository and local secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb6c7fd52-4723-5f4d-a157-3d39bd16a1d7) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Git repository. This definition requires local authentication secrets stored in the Kubernetes cluster. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-to-Kubernetes-cluster-LocalAuthRef_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using Git repository and SSH secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9e980dca-f3e1-8da3-6717-ad37b1ca6b27) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Git repository. This definition requires a SSH private key secret stored in Key Vault. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-to-Kubernetes-cluster-SSH_DINE.json) |
[Configure Kubernetes clusters with Flux v2 configuration using public Git repository](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F83ea2fd1-9eaf-2f6d-f672-cd7b2ac798f6) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Git repository. This definition requires no secrets. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-Flux2-to-Kubernetes-cluster-no-secrets_DINE.json) |
[Configure Kubernetes clusters with specified Flux v2 Bucket source using local secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb8c1d6c1-6137-97c6-9c34-d4627e54ca26) |
Deploy a 'fluxConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined Bucket. This definition requires local authentication secrets stored in the Kubernetes cluster. For instructions, visit [https://aka.ms/GitOpsFlux2Policy](https://aka.ms/GitOpsFlux2Policy). |
DeployIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/GitOps-Flux2-to-Kubernetes-cluster-Bucket-K8sSecret_DINE.json) |
[Configure Kubernetes clusters with specified GitOps configuration using HTTPS secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa6f560f4-f582-4b67-b123-a37dcd1bf7ea) |
Deploy a 'sourceControlConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined git repo. This definition requires HTTPS user and key secrets stored in Key Vault. For instructions, visit [https://aka.ms/K8sGitOpsPolicy](https://aka.ms/K8sGitOpsPolicy). |
auditIfNotExists, AuditIfNotExists, deployIfNotExists, DeployIfNotExists, disabled, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-to-Kubernetes-cluster-HTTPS-secrets_DINE.json) |
[Configure Kubernetes clusters with specified GitOps configuration using no secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1d61c4d2-aef2-432b-87fc-7f96b019b7e1) |
Deploy a 'sourceControlConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined git repo. This definition requires no secrets. For instructions, visit [https://aka.ms/K8sGitOpsPolicy](https://aka.ms/K8sGitOpsPolicy). |
auditIfNotExists, AuditIfNotExists, deployIfNotExists, DeployIfNotExists, disabled, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-to-Kubernetes-cluster-no-secrets_DINE.json) |
[Configure Kubernetes clusters with specified GitOps configuration using SSH secrets](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc050047b-b21b-4822-8a2d-c1e37c3c0c6a) |
Deploy a 'sourceControlConfiguration' to Kubernetes clusters to assure that the clusters get their source of truth for workloads and configurations from the defined git repo. This definition requires a SSH private key secret in Key Vault. For instructions, visit [https://aka.ms/K8sGitOpsPolicy](https://aka.ms/K8sGitOpsPolicy). |
auditIfNotExists, AuditIfNotExists, deployIfNotExists, DeployIfNotExists, disabled, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/Deploy-GitOps-to-Kubernetes-cluster-SSH-secrets_DINE.json) |
[Configure Microsoft Entra ID integrated Azure Kubernetes Service Clusters with required Admin Group Access](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F36a27de4-199b-40fb-b336-945a8475d6c5) |
Ensure to improve cluster security by centrally govern Administrator access to Microsoft Entra ID integrated AKS clusters. |
DeployIfNotExists, Disabled |
[2.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AAD_AdminGroup_DINE.json) |
[Configure Node OS Auto upgrade on Azure Kubernetes Cluster](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F40f1aee2-4db4-4b74-acb1-c6972e24cca8) |
Use Node OS auto-upgrade to control node-level OS security updates of Azure Kubernetes Service (AKS) clusters. For more info, visit [https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-node-image](/en-us/azure/aks/auto-upgrade-node-image). |
DeployIfNotExists, Disabled |
[1.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Autoupgrade_NodeOS_DINE.json) |
[Deploy - Configure diagnostic settings for Azure Kubernetes Service to Log Analytics workspace](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F6c66c325-74c8-42fd-a286-a74b0e2939d8) |
Deploys the diagnostic settings for Azure Kubernetes Service to stream resource logs to a Log Analytics workspace. |
DeployIfNotExists, Disabled |
[3.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/DataConnectorsAzureKubernetes_DINE.json) |
[Deploy Azure Policy Add-on to Azure Kubernetes Service clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa8eff44f-8c92-45c3-a3fb-9880802d67a7) |
Use Azure Policy Add-on to manage and report on the compliance state of your Azure Kubernetes Service (AKS) clusters. For more information, see [https://aka.ms/akspolicydoc](https://aka.ms/akspolicydoc). |
DeployIfNotExists, Disabled |
[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_AzurePolicyAddOn_DINE.json) |
[Deploy Image Cleaner on Azure Kubernetes Service](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F7e49285c-4bed-4564-b26a-5225ccc311f3) |
Deploy Image Cleaner on Azure Kubernetes clusters. For more info, visit [https://aka.ms/aks/image-cleaner](https://aka.ms/aks/image-cleaner) |
DeployIfNotExists, Disabled |
[1.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_ImageCleaner_DINE.json) |
[Deploy Planned Maintenance to schedule and control upgrades for your Azure Kubernetes Service (AKS) cluster](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe1352e44-d34d-4e4d-a22e-451a15f759a1) |
Planned Maintenance allows you to schedule weekly maintenance windows to perform updates and minimize workload impact. Once scheduled, upgrades occur only during the window you selected. Learn more at: [https://aka.ms/aks/planned-maintenance](https://aka.ms/aks/planned-maintenance) |
DeployIfNotExists, AuditIfNotExists, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_Maintenance_DINE.json) |
[Disable Command Invoke on Azure Kubernetes Service clusters](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1b708b0a-3380-40e9-8b79-821f9fa224cc) |
Disabling command invoke can enhance the security by rejecting invoke-command access to the cluster |
DeployIfNotExists, Disabled |
[1.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_DisableRunCommand_DINE.json) |
[Ensure cluster containers have readiness or liveness probes configured](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb1a9997f-2883-4f12-bdff-2280f99b5915) |
This policy enforces that all pods have a readiness and/or liveness probes configured. Probe Types can be any of tcpSocket, httpGet and exec. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For instructions on using this policy, visit [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[3.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerEnforceProbes.json) |
[Kubernetes cluster container images must include the preStop hook](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a3b9003-eac6-4d39-a184-4a567ace7645) |
Requires that container images include a preStop hook to gracefully terminate processes during pod shutdowns. |
Audit, Deny, Disabled |
[1.1.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerEnforcePreStopHook.json) |
[Kubernetes cluster container images should not include latest image tag](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F021f8078-41a0-40e6-81b6-c6597da9f3ee) |
Requires that container images do not use the latest tag in Kubernetes, it is a best practice to ensure reproducibility, prevent unintended updates, and facilitate easier debugging and rollbacks by using explicit and versioned container images. |
Audit, Deny, Disabled |
[2.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ImagesDoNotUseLatest.json) |
[Kubernetes cluster containers CPU and memory resource limits should not exceed the specified limits](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe345eecc-fa47-480f-9e88-67dcc122b164) |
Enforce container CPU and memory resource limits to prevent resource exhaustion attacks in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerResourceLimits.json) |
[Kubernetes cluster containers CPU and memory resource requests must be defined](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F03a4ecdb-0684-4039-be91-2762979e1bc8) |
Enforce container CPU and memory resource requests to ensure scheduled node has required resources. |
Audit, Deny, Disabled |
[1.0.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerResourceRequests.json) |
[Kubernetes cluster containers should not share host namespaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F47a1ee2f-2a2a-4576-bf2a-e0e36709c2b8) |
Block pod containers from sharing the host process ID namespace, host IPC namespace, and host network namespace in a Kubernetes cluster. This recommendation aligns with the Kubernetes Pod Security Standards for host namespaces and is part of CIS 5.2.1, 5.2.2 and 5.2.3 which are intended to improve the security of your Kubernetes environments. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[6.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockHostNamespace.json) |
[Kubernetes cluster containers should not use forbidden sysctl interfaces](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F56d0a13f-712f-466b-8416-56fb354fb823) |
Containers should not use forbidden sysctl interfaces in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[7.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ForbiddenSysctlInterfaces.json) |
[Kubernetes cluster containers should only pull images when image pull secrets are present](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F12db3749-7e03-4b9f-b443-d37d3fb9f8d9) |
Restrict containers' image pulls to enforce the presence of ImagePullSecrets, ensuring secure and authorized access to images within a Kubernetes cluster |
Audit, Deny, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerRestrictedImagePulls.json) |
[Kubernetes cluster containers should only use allowed AppArmor profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F511f5417-5d12-434d-ab2e-816901e72a5e) |
Containers should only use allowed AppArmor profiles in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[6.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceAppArmorProfile.json) |
[Kubernetes cluster containers should only use allowed capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc26596ff-4d70-4e6a-9a30-c2506bd2f80c) |
Restrict the capabilities to reduce the attack surface of containers in a Kubernetes cluster. This recommendation is part of CIS 5.2.8 and CIS 5.2.9 which are intended to improve the security of your Kubernetes environments. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedCapabilities.json) |
[Kubernetes cluster containers should only use allowed images](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffebd0533-8e55-448f-b837-bd0e06f16469) |
Use images from trusted registries to reduce the Kubernetes cluster's exposure risk to unknown vulnerabilities, security issues and malicious images. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[9.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedImages.json) |
[Kubernetes cluster containers should only use allowed ProcMountType](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff85eb0dd-92ee-40e9-8a76-db25a507d6d3) |
Pod containers can only use allowed ProcMountTypes in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedProcMountType.json) |
[Kubernetes cluster containers should only use allowed pull policy](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F50c83470-d2f0-4dda-a716-1938a4825f62) |
Restrict containers' pull policy to enforce containers to use only allowed images on deployments |
Audit, Deny, Disabled |
[3.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerAllowedPullPolicy.json) |
[Kubernetes cluster containers should only use allowed seccomp profiles](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F975ce327-682c-4f2e-aa46-b9598289b86c) |
Pod containers can only use allowed seccomp profiles in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[7.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedSeccompProfile.json) |
[Kubernetes cluster containers should run with a read only root file system](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fdf49d893-a74c-421d-bc95-c663042e5b80) |
Run containers with a read only root file system to protect from changes at run-time with malicious binaries being added to PATH in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ReadOnlyRootFileSystem.json) |
[Kubernetes cluster pod FlexVolume volumes should only use allowed drivers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff4a8fce0-2dd5-4c21-9a36-8f0ec809d663) |
Pod FlexVolume volumes should only use allowed drivers in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[5.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/FlexVolumeDrivers.json) |
[Kubernetes cluster pod hostPath volumes should only use allowed host paths](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F098fc59e-46c7-4d99-9b16-64990e543d75) |
Limit pod HostPath volume mounts to the allowed host paths in a Kubernetes Cluster. This policy is generally available for Kubernetes Service (AKS), and Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[6.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedHostPaths.json) |
[Kubernetes cluster pods and containers should follow SELinux security standards](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe1e6c427-07d9-46ab-9689-bfa85431e636) |
This policy enforces Kubernetes Pod Security Standards for SELinux options. Under PSS mode, 'user' and 'role' fields must be empty, and 'type' field must be one of the allowed values. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[8.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/SELinux.json) |
[Kubernetes cluster pods and containers should only run with approved user and group IDs](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ff06ddb64-5fa3-4b77-b166-acb36f7f6042) |
Control the user, primary group, supplemental group and file system group IDs that pods and containers can use to run in a Kubernetes Cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[6.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedUsersGroups.json) |
[Kubernetes cluster pods should only use allowed volume types](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F16697877-1118-4fb1-9b65-9898ec2509ec) |
Pods can only use allowed volume types in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[5.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedVolumeTypes.json) |
[Kubernetes cluster pods should only use approved host network and port list](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F82985f06-dc18-4a48-bc1c-b9f4f0098cfe) |
Restrict pod access to the host network and the allowable host ports in a Kubernetes cluster. This recommendation is part of CIS 5.2.4 which is intended to improve the security of your Kubernetes environments and aligns with Pod Security Standards (PSS) for hostPorts. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[7.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/HostNetworkPorts.json) |
[Kubernetes cluster pods should use specified labels](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F46592696-4c7b-4bf3-9e45-6c2763bdc0a6) |
Use specified labels to identify the pods in a Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[7.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/PodEnforceLabels.json) |
[Kubernetes cluster services should listen only on allowed ports](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F233a2a17-77ca-4fb1-9b6b-69223d272a44) |
Restrict services to listen only on allowed ports to secure access to the Kubernetes cluster. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ServiceAllowedPorts.json) |
[Kubernetes cluster services should only use allowed external IPs](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd46c275d-1680-448d-b2ec-e495a3b6cc89) |
Use allowed external IPs to avoid the potential attack (CVE-2020-8554) in a Kubernetes cluster. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[5.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AllowedExternalIPs.json) |
[Kubernetes cluster services should use unique selectors](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fb0fdedee-7b9e-4a17-9f5d-5e8e912d2f01) |
Ensure Services in a Namespace Have Unique Selectors. A unique service selector ensures that each service within a namespace is uniquely identifiable based on specific criteria. This policy syncs service resources into OPA via Gatekeeper. Before applying, verify Gatekeeper pods memory capacity won't be exceeded. Parameters apply to specific namespaces, but it syncs all resources of that type across all namespaces. Currently in preview for Kubernetes Service (AKS). |
Audit, Deny, Disabled |
[1.2.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/UniqueServiceSelectors.json) |
[Kubernetes cluster should not allow privileged containers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F95edb821-ddaf-4404-9732-666045e056b4) |
Do not allow privileged containers creation in a Kubernetes cluster. This recommendation is part of CIS 5.2.1 which is intended to improve the security of your Kubernetes environments. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[9.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilege.json) |
[Kubernetes cluster should not use naked pods](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F65280eef-c8b4-425e-9aec-af55e55bf581) |
Block usage of naked Pods. Naked Pods will not be rescheduled in the event of a node failure. Pods should be managed by Deployment, Replicset, Daemonset or Jobs |
Audit, Deny, Disabled |
[2.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockNakedPods.json) |
[Kubernetes cluster Windows containers should not overcommit cpu and memory](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa2abc456-f0ae-464b-bd3a-07a3cdbd7fb1) |
Windows container resource requests should be less or equal to the resource limit or unspecified to avoid overcommit. If Windows memory is over-provisioned it will process pages in disk - which can slow down performance - instead of terminating the container with out-of-memory |
Audit, Deny, Disabled |
[2.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/WindowsContainerResourceLimits.json) |
[Kubernetes cluster Windows containers should not run as ContainerAdministrator](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5485eac0-7e8f-4964-998b-a44f4f0c1e75) |
Prevent usage of ContainerAdministrator as the user to execute the container processes for Windows pods or containers. This recommendation is intended to improve the security of Windows nodes. For more information, see [https://kubernetes.io/docs/concepts/windows/intro/](https://kubernetes.io/docs/concepts/windows/intro/) . |
Audit, Deny, Disabled |
[1.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/WindowsBlockContainerAdmin.json) |
[Kubernetes cluster Windows containers should only run with approved user and domain user group](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F57dde185-5c62-4063-b965-afbb201e9c1c) |
Control the user that Windows pods and containers can use to run in a Kubernetes Cluster. This recommendation is part of Pod Security Policies on Windows nodes which are intended to improve the security of your Kubernetes environments. |
Audit, Deny, Disabled |
[2.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/WindowsContainerAllowedUsername.json) |
[Kubernetes cluster Windows pods should not run HostProcess containers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F077f0ce1-86d6-4058-bc60-de05067e8622) |
Prevent prviledged access to the windows node. This recommendation is intended to improve the security of Windows nodes. For more information, see [https://kubernetes.io/docs/concepts/windows/intro/](https://kubernetes.io/docs/concepts/windows/intro/) . |
Audit, Deny, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/WindowsBlockHostProcess.json) |
[Kubernetes clusters should be accessible only over HTTPS](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1a5b4dca-0b6f-4cf5-907c-56316bc1bf3d) |
Use of HTTPS ensures authentication and protects data in transit from network layer eavesdropping attacks. This capability is currently generally available for Kubernetes Service (AKS), and in preview for Azure Arc enabled Kubernetes. For more info, visit [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc) |
audit, Audit, deny, Deny, disabled, Disabled |
[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/IngressHttpsOnly.json) |
[Kubernetes clusters should disable automounting API credentials](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F423dd1ba-798e-40e4-9c4d-b6902674b423) |
Disable automounting API credentials to prevent a potentially compromised Pod resource to run API commands against Kubernetes clusters. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockAutomountToken.json) |
[Kubernetes clusters should ensure that the cluster-admin role is only used where required](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa3dc4946-dba6-43e6-950d-f96532848c9f) |
The role 'cluster-admin' provides wide-ranging powers over the environment and should be used only where and when needed. |
Audit, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockAdminRolebindings.json) |
[Kubernetes clusters should minimize wildcard use in role and cluster role](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fca8d5704-aa2b-40cf-b110-dc19052825ad) |
Using wildcards '*' can be a security risk because it grants broad permissions that may not be necessary for a specific role. If a role has too many permissions, it could potentially be abused by an attacker or compromised user to gain unauthorized access to resources in the cluster. |
Audit, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockWildcardRoles.json) |
[Kubernetes clusters should not allow container privilege escalation](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1c6e92c9-99f0-4e55-9cf2-0c234dc48f99) |
Do not allow containers to run with privilege escalation to root in a Kubernetes cluster. This recommendation is part of CIS 5.2.5 which is intended to improve the security of your Kubernetes environments. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[8.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerNoPrivilegeEscalation.json) |
[Kubernetes clusters should not allow endpoint edit permissions of ClusterRole/system:aggregate-to-edit](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F1ddac26b-ed48-4c30-8cc5-3a68c79b8001) |
ClusterRole/system:aggregate-to-edit should not allow endpoint edit permissions due to CVE-2021-25740, Endpoint & EndpointSlice permissions allow cross-Namespace forwarding, [https://github.com/kubernetes/kubernetes/issues/103675](https://github.com/kubernetes/kubernetes/issues/103675). This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Disabled |
[3.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockEndpointEditDefaultRole.json) |
[Kubernetes clusters should not grant CAP_SYS_ADMIN security capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd2e7ea85-6b44-4317-a0be-1b951587f626) |
To reduce the attack surface of your containers, restrict CAP_SYS_ADMIN Linux capabilities. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[5.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerDisallowedSysAdminCapability.json) |
[Kubernetes clusters should not use specific security capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa27c700f-8a22-44ec-961c-41625264370b) |
Prevent specific security capabilities in Kubernetes clusters to prevent ungranted privileges on the Pod resource. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[5.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ContainerDisallowedCapabilities.json) |
[Kubernetes clusters should not use the default namespace](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9f061a12-e40d-4183-a00e-171812443373) |
Prevent usage of the default namespace in Kubernetes clusters to protect against unauthorized access for ConfigMap, Pod, Secret, Service, and ServiceAccount resource types. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[4.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/BlockDefaultNamespace.json) |
[Kubernetes clusters should specify host in ingress resource rules](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd8c942c6-16a3-400b-8f2e-785f44030036) |
Ensure specifying host in ingress resource rules to prevent unintentional exposure of backend services to unauthorized access. This policy evaluates Kubernetes Ingress resources to ensure that each rule has a specified host field. |
Audit, Deny, Disabled |
[1.1.0-preview](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/RequireIngressHost.json) |
[Kubernetes clusters should use Container Storage Interface(CSI) driver StorageClass](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F4f3823b6-6dac-4b5a-9c61-ce1afb829f17) |
The Container Storage Interface (CSI) is a standard for exposing arbitrary block and file storage systems to containerized workloads on Kubernetes. In-tree provisioner StorageClass should be deprecated since AKS version 1.21. To learn more, [https://aka.ms/aks-csi-driver](https://aka.ms/aks-csi-driver) |
Audit, Deny, Disabled |
[2.3.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceCSIDriver.json) |
[Kubernetes clusters should use internal load balancers](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F3fc4dc25-5baf-40d8-9b05-7fe74c1bc64e) |
Use internal load balancers to make a Kubernetes service accessible only to applications running in the same virtual network as the Kubernetes cluster. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
audit, Audit, deny, Deny, disabled, Disabled |
[8.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/LoadbalancerNoPublicIPs.json) |
[Kubernetes resources should have required annotations](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F9a5f4e39-e427-4d5d-ae73-93db00328bec) |
Ensure that required annotations are attached on a given Kubernetes resource kind for improved resource management of your Kubernetes resources. This policy is generally available for Kubernetes Service (AKS), and preview for Azure Arc enabled Kubernetes. For more information, see [https://aka.ms/kubepolicydoc](https://aka.ms/kubepolicydoc). |
Audit, Deny, Disabled |
[3.2.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/EnforceResourceAnnotation.json) |
[Kubernetes Services should be upgraded to a non-vulnerable Kubernetes version](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Ffb893a29-21bb-418c-a157-e99480ec364c) |
Upgrade your Kubernetes service cluster to a later Kubernetes version to protect against known vulnerabilities in your current Kubernetes version. Vulnerability CVE-2019-9946 has been patched in Kubernetes versions 1.11.9+, 1.12.7+, 1.13.5+, and 1.14.0+ |
Audit, Disabled |
[1.0.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_UpgradeVersion_KubernetesService_Audit.json) |
[Must Have Anti Affinity Rules or Topology Spread Constraints Set](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F34c88cd4-5d72-4dbb-bf77-12c3cafe8791) |
This policy ensures that pods are scheduled on different nodes within the cluster. By enforcing anti-affinity rules or pod topology spread constraints, availability is maintained even if one of the nodes becomes unavailable. Pods will continue to run on other nodes, enhancing resilience. |
Audit, Deny, Disabled |
[1.2.2](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MustHaveAntiAffinityRulesSet.json) |
[Mutate K8s Container to drop all capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc873b3ba-c605-42e4-a64b-a142a93826fc) |
Mutates securityContext.capabilities.drop to add in "ALL". This drops all capabilities for k8s linux containers |
Mutate, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateContainerAllowedCapabilitiesContainers.json) |
[Mutate K8s Init Container to drop all capabilities](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fc812272d-7488-495f-a505-047d34b83f58) |
Mutates securityContext.capabilities.drop to add in "ALL". This drops all capabilities for k8s linux init containers |
Mutate, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateContainerAllowedCapabilitiesInitContainers.json) |
[No AKS Specific Labels](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fa22123bd-b9da-4c86-9424-24903e91fd55) |
Prevents customers from applying AKS specific labels. AKS uses labels prefixed with `kubernetes.azure.com` to denote AKS owned components. The customer should not use these labels. |
Audit, Deny, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/NoAKSSpecificLabels.json) |
[Prints a message if a mutation is applied](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe24df237-32cb-4a6c-a2f6-85b499cda9f2) |
Looks up the mutation annotations applied and prints a message if annotation exists. |
Audit, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/PrintMutationsAnnotations.json) |
[Reserved System Pool Taints](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F48940d92-ff05-449e-9111-e742d9280451) |
Restricts the CriticalAddonsOnly taint to just the system pool. AKS uses the CriticalAddonsOnly taint to keep customer pods away from the system pool. It ensures a clear separation between AKS components and customer pods, as well as prevents customer pods from being evicted if they do not tolerate the CriticalAddonsOnly taint. |
Audit, Deny, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/ReservedSystemPoolTaints.json) |
[Resource logs in Azure Kubernetes Service should be enabled](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F245fc9df-fa96-4414-9a0b-3738c2f7341c) |
Azure Kubernetes Service's resource logs can help recreate activity trails when investigating security incidents. Enable it to make sure the logs will exist when needed |
AuditIfNotExists, Disabled |
[1.0.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AuditDiagnosticLog_Audit.json) |
[Restricts the CriticalAddonsOnly taint to just the system pool.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fe16d171b-bfe5-4d79-a525-19736b396e92) |
To avoid eviction of user apps from user pools and maintain separation of concerns between the user and system pools, the 'CriticalAddonsOnly' taint should not be applied to user pools. |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateReservedSystemPoolTaints.json) |
[Role-Based Access Control (RBAC) should be used on Kubernetes Services](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fac4a19c2-fa67-49b4-8ae5-0b2e78c49457) |
To provide granular filtering on the actions that users can perform, use Role-Based Access Control (RBAC) to manage permissions in Kubernetes Service Clusters and configure relevant authorization policies. |
Audit, Disabled |
[1.1.0](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Security%20Center/ASC_EnableRBAC_KubernetesService_Audit.json) |
[Sets automountServiceAccountToken in the Pod spec in containers to false.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F57f274ef-580a-4ed2-bcf8-5c6fa3775253) |
Setting automountServiceAccountToken to false increases security by avoiding the default auto-mounting of service account tokens |
Mutate, Disabled |
[1.2.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateMountServiceAccountToken.json) |
[Sets Kubernetes cluster containers CPU limits to default values in case not present.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F42ba1d72-e90f-42f8-bf99-5a1351eed2b1) |
Setting container CPU limits to prevent resource exhaustion attacks in a Kubernetes cluster. |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateResourceCPULimits.json) |
[Sets Kubernetes cluster containers memory limits to default values in case not present.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F5f86d473-38a8-46c9-bdfe-d7fa3b9836bf) |
Setting container memory limits to prevent resource exhaustion attacks in a Kubernetes cluster. |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateResourceMemoryLimits.json) |
[Sets maxUnavailable pods to 1 for PodDisruptionBudget resources](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2Fd77f191e-2338-45d0-b6d4-4ee1c586a192) |
Setting your max unavailable pod value to 1 ensures that your application or service is available during a disruption |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateMaxUnavailablePods.json) |
[Sets readOnlyRootFileSystem in the Pod spec in init containers to true if it is not set.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F2ae2f266-ecc3-4d26-82c5-8c3cb7774f45) |
Setting readOnlyRootFileSystem to true increases security by preventing containers from writing into the root filesystem. This works only for linux containers. |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateReadOnlyRootFilesystemInitContainers.json) |
[Sets readOnlyRootFileSystem in the Pod spec to true if it is not set.](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F8e875f96-2c56-40ca-86db-b9f6a0be7347) |
Setting readOnlyRootFileSystem to true increases security by preventing containers from writing into the root filesystem |
Mutate, Disabled |
[1.3.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/MutateReadOnlyRootFilesystem.json) |
[Temp disks and cache for agent node pools in Azure Kubernetes Service clusters should be encrypted at host](https://portal.azure.com/#blade/Microsoft_Azure_Policy/PolicyDetailBlade/definitionId/%2Fproviders%2FMicrosoft.Authorization%2FpolicyDefinitions%2F41425d9f-d1a5-499a-9932-f8ed8453932c) |
To enhance data security, the data stored on the virtual machine (VM) host of your Azure Kubernetes Service nodes VMs should be encrypted at rest. This is a common requirement in many regulatory and industry compliance standards. |
Audit, Deny, Disabled |
[1.0.1](https://github.com/Azure/azure-policy/blob/master/built-in-policies/policyDefinitions/Kubernetes/AKS_EncryptionAtHost_Deny.json) |
