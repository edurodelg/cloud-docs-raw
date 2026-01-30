---
merged_at: 2026-01-30T23:42:48.935935
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-csi-disk-storage-provision -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-csi-blob-storage-provision -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-csi-files-storage-provision -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ingress-basic -->

# Create an unmanaged ingress controller

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services. Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services. When you use an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.

This article shows you how to deploy the [NGINX ingress controller](https://github.com/kubernetes/ingress-nginx) in an Azure Kubernetes Service (AKS) cluster. Two applications are then run in the AKS cluster, each of which is accessible over the single IP address.

Important

The Application routing add-on is recommended for ingress in AKS. For more information, see [Managed nginx Ingress with the application routing add-on](/en-us/azure/aks/app-routing).

Note

There are two open source ingress controllers for Kubernetes based on Nginx: one is maintained by the Kubernetes community ([kubernetes/ingress-nginx](https://github.com/kubernetes/ingress-nginx)), and one is maintained by NGINX, Inc. ([nginxinc/kubernetes-ingress](https://github.com/nginxinc/kubernetes-ingress)). This article will be using the Kubernetes community ingress controller.

## Before you begin

- This article uses Helm 3 to install the NGINX ingress controller on a
[supported version of Kubernetes](/en-us/azure/aks/supported-kubernetes-versions). Make sure that you're using the latest release of Helm and have access to the*ingress-nginx*Helm repository. The steps outlined in this article may not be compatible with previous versions of the Helm chart, NGINX ingress controller, or Kubernetes. - This article assumes you have an existing AKS cluster with an integrated Azure Container Registry (ACR). For more information on creating an AKS cluster with an integrated ACR, see
[Authenticate with Azure Container Registry from Azure Kubernetes Service](/en-us/azure/aks/cluster-container-registry-integration#create-a-new-acr). - The Kubernetes API health endpoint,
`healthz`

was deprecated in Kubernetes v1.16. You can replace this endpoint with the`livez`

and`readyz`

endpoints instead. See[Kubernetes API endpoints for health](https://kubernetes.io/docs/reference/using-api/health-checks/#api-endpoints-for-health)to determine which endpoint to use for your scenario. - If you're using Azure CLI, this article requires that you're running the Azure CLI version 2.0.64 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install]. - If you're using Azure PowerShell, this article requires that you're running Azure PowerShell version 5.9.0 or later. Run
`Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell).

## Basic configuration

To create a basic NGINX ingress controller without customizing the defaults, you'll use Helm. The following configuration uses the default configuration for simplicity. You can add parameters for customizing the deployment, like `--set controller.replicaCount=3`

.

Note

If you would like to enable [client source IP preservation](/en-us/azure/aks/concepts-network-ingress#ingress-controllers) for requests to containers in your cluster, add `--set controller.service.externalTrafficPolicy=Local`

to the Helm install command. The client source IP is stored in the request header under *X-Forwarded-For*. When you're using an ingress controller with client source IP preservation enabled, TLS pass-through won't work.

```
NAMESPACE=ingress-basic
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx \
--create-namespace \
--namespace $NAMESPACE \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.service.externalTrafficPolicy=Local
```


Note

In this tutorial, `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

is being set to `/healthz`

. This means if the response code of the requests to `/healthz`

is not `200`

, the entire ingress controller will be down. You can modify the value to other URI in your own scenario. You cannot delete this part or unset the value, or the ingress controller will still be down.
The package `ingress-nginx`

used in this tutorial, which is provided by [Kubernetes official](https://github.com/kubernetes/ingress-nginx), will always return `200`

response code if requesting `/healthz`

, as it is designed as [default backend](https://kubernetes.github.io/ingress-nginx/user-guide/default-backend/) for users to have a quick start, unless it is being overwritten by ingress rules.

## Customized configuration

As an alternative to the basic configuration presented in the above section, the next set of steps will show how to deploy a customized ingress controller. You'll have the option of using an internal static IP address, or using a dynamic public IP address.

### Import the images used by the Helm chart into your ACR

To control image versions, you'll want to import them into your own Azure Container Registry. The [NGINX ingress controller Helm chart](https://github.com/kubernetes/ingress-nginx/tree/main/charts/ingress-nginx) relies on three container images. Use `az acr import`

to import those images into your ACR.

```
REGISTRY_NAME=<REGISTRY_NAME>
SOURCE_REGISTRY=registry.k8s.io
CONTROLLER_IMAGE=ingress-nginx/controller
CONTROLLER_TAG=v1.8.1
PATCH_IMAGE=ingress-nginx/kube-webhook-certgen
PATCH_TAG=v20230407
DEFAULTBACKEND_IMAGE=defaultbackend-amd64
DEFAULTBACKEND_TAG=1.5
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$CONTROLLER_IMAGE:$CONTROLLER_TAG --image $CONTROLLER_IMAGE:$CONTROLLER_TAG
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$PATCH_IMAGE:$PATCH_TAG --image $PATCH_IMAGE:$PATCH_TAG
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG --image $DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG
```


Note

In addition to importing container images into your ACR, you can also import Helm charts into your ACR. For more information, see [Push and pull Helm charts to an Azure Container Registry](/en-us/azure/container-registry/container-registry-helm-repos).

### Create an ingress controller

To create the ingress controller, use Helm to install *ingress-nginx*. The ingress controller needs to be scheduled on a Linux node. Windows Server nodes shouldn't run the ingress controller. A node selector is specified using the `--set nodeSelector`

parameter to tell the Kubernetes scheduler to run the NGINX ingress controller on a Linux-based node.

For added redundancy, two replicas of the NGINX ingress controllers are deployed with the `--set controller.replicaCount`

parameter. To fully benefit from running replicas of the ingress controller, make sure there's more than one node in your AKS cluster.

The following example creates a Kubernetes namespace for the ingress resources named *ingress-basic* and is intended to work within that namespace. Specify a namespace for your own environment as needed. If your AKS cluster isn't Kubernetes role-based access control enabled, add `--set rbac.create=false`

to the Helm commands.

Note

If you would like to enable [client source IP preservation](/en-us/azure/aks/concepts-network-ingress#ingress-controllers) for requests to containers in your cluster, add `--set controller.service.externalTrafficPolicy=Local`

to the Helm install command. The client source IP is stored in the request header under *X-Forwarded-For*. When you're using an ingress controller with client source IP preservation enabled, TLS pass-through won't work.

```
# Add the ingress-nginx repository
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
# Set variable for ACR location to use for pulling images
ACR_LOGIN_SERVER=<REGISTRY_LOGIN_SERVER>
# Use Helm to deploy an NGINX ingress controller
helm install ingress-nginx ingress-nginx/ingress-nginx \
--version 4.7.1 \
--namespace ingress-basic \
--create-namespace \
--set controller.replicaCount=2 \
--set controller.nodeSelector."kubernetes\.io/os"=linux \
--set controller.image.registry=$ACR_LOGIN_SERVER \
--set controller.image.image=$CONTROLLER_IMAGE \
--set controller.image.tag=$CONTROLLER_TAG \
--set controller.image.digest="" \
--set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.service.externalTrafficPolicy=Local \
--set controller.admissionWebhooks.patch.image.registry=$ACR_LOGIN_SERVER \
--set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \
--set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \
--set controller.admissionWebhooks.patch.image.digest="" \
--set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
--set defaultBackend.image.registry=$ACR_LOGIN_SERVER \
--set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \
--set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \
--set defaultBackend.image.digest=""
```


### Create an ingress controller using an internal IP address

By default, an NGINX ingress controller is created with a dynamic public IP address assignment. A common configuration requirement is to use an internal, private network and IP address. This approach allows you to restrict access to your services to internal users, with no external access.

Use the `--set controller.service.loadBalancerIP`

and `--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-internal"=true`

parameters to assign an internal IP address to your ingress controller. Provide your own internal IP address for use with the ingress controller. Make sure that this IP address isn't already in use within your virtual network. If you're using an existing virtual network and subnet, you must configure your AKS cluster with the correct permissions to manage the virtual network and subnet. For more information, see [Use kubenet networking with your own IP address ranges in Azure Kubernetes Service (AKS)](/en-us/azure/aks/configure-kubenet) or [Configure Azure CNI networking in Azure Kubernetes Service (AKS)](/en-us/azure/aks/configure-azure-cni?tabs=configure-networking-portal).

```
# Add the ingress-nginx repository
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
# Set variable for ACR location to use for pulling images
ACR_LOGIN_SERVER=<REGISTRY_LOGIN_SERVER>
# Use Helm to deploy an NGINX ingress controller
helm install ingress-nginx ingress-nginx/ingress-nginx \
--version 4.7.1 \
--namespace ingress-basic \
--create-namespace \
--set controller.replicaCount=2 \
--set controller.nodeSelector."kubernetes\.io/os"=linux \
--set controller.image.registry=$ACR_LOGIN_SERVER \
--set controller.image.image=$CONTROLLER_IMAGE \
--set controller.image.tag=$CONTROLLER_TAG \
--set controller.image.digest="" \
--set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
--set controller.service.loadBalancerIP=10.224.0.42 \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-internal"=true \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.admissionWebhooks.patch.image.registry=$ACR_LOGIN_SERVER \
--set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \
--set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \
--set controller.admissionWebhooks.patch.image.digest="" \
--set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
--set defaultBackend.image.registry=$ACR_LOGIN_SERVER \
--set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \
--set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \
--set defaultBackend.image.digest=""
```


## Check the load balancer service

Check the load balancer service by using `kubectl get services`

.

```
kubectl get services --namespace ingress-basic -o wide -w ingress-nginx-controller
```


When the Kubernetes load balancer service is created for the NGINX ingress controller, an IP address is assigned under *EXTERNAL-IP*, as shown in the following example output:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE SELECTOR
ingress-nginx-controller LoadBalancer 10.0.65.205 EXTERNAL-IP 80:30957/TCP,443:32414/TCP 1m app.kubernetes.io/component=controller,app.kubernetes.io/instance=ingress-nginx,app.kubernetes.io/name=ingress-nginx
```


If you browse to the external IP address at this stage, you see a 404 page displayed. This is because you still need to set up the connection to the external IP, which is done in the next sections.

## Run demo applications

To see the ingress controller in action, run two demo applications in your AKS cluster. In this example, you use `kubectl apply`

to deploy two instances of a simple *Hello world* application.

Create an

`aks-helloworld-one.yaml`

file and copy in the following example YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aks-helloworld-one spec: replicas: 1 selector: matchLabels: app: aks-helloworld-one template: metadata: labels: app: aks-helloworld-one spec: containers: - name: aks-helloworld-one image: mcr.microsoft.com/azuredocs/aks-helloworld:v1 ports: - containerPort: 80 env: - name: TITLE value: "Welcome to Azure Kubernetes Service (AKS)" --- apiVersion: v1 kind: Service metadata: name: aks-helloworld-one spec: type: ClusterIP ports: - port: 80 selector: app: aks-helloworld-one`

Create an

`aks-helloworld-two.yaml`

file and copy in the following example YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aks-helloworld-two spec: replicas: 1 selector: matchLabels: app: aks-helloworld-two template: metadata: labels: app: aks-helloworld-two spec: containers: - name: aks-helloworld-two image: mcr.microsoft.com/azuredocs/aks-helloworld:v1 ports: - containerPort: 80 env: - name: TITLE value: "AKS Ingress Demo" --- apiVersion: v1 kind: Service metadata: name: aks-helloworld-two spec: type: ClusterIP ports: - port: 80 selector: app: aks-helloworld-two`

Run the two demo applications using

`kubectl apply`

:`kubectl apply -f aks-helloworld-one.yaml --namespace ingress-basic kubectl apply -f aks-helloworld-two.yaml --namespace ingress-basic`


## Create an ingress route

Both applications are now running on your Kubernetes cluster. To route traffic to each application, create a Kubernetes ingress resource. The ingress resource configures the rules that route traffic to one of the two applications.

In the following example, traffic to *EXTERNAL_IP/hello-world-one* is routed to the service named `aks-helloworld-one`

. Traffic to *EXTERNAL_IP/hello-world-two* is routed to the `aks-helloworld-two`

service. Traffic to *EXTERNAL_IP/static* is routed to the service named `aks-helloworld-one`

for static assets.

Create a file named

`hello-world-ingress.yaml`

and copy in the following example YAML:`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: hello-world-ingress annotations: nginx.ingress.kubernetes.io/ssl-redirect: "false" nginx.ingress.kubernetes.io/use-regex: "true" nginx.ingress.kubernetes.io/rewrite-target: /$2 spec: ingressClassName: nginx rules: - http: paths: - path: /hello-world-one(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80 - path: /hello-world-two(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-two port: number: 80 - path: /(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80 --- apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: hello-world-ingress-static annotations: nginx.ingress.kubernetes.io/ssl-redirect: "false" nginx.ingress.kubernetes.io/rewrite-target: /static/$2 spec: ingressClassName: nginx rules: - http: paths: - path: /static(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80`

Create the ingress resource using the

`kubectl apply`

command.`kubectl apply -f hello-world-ingress.yaml --namespace ingress-basic`


## Test the ingress controller

To test the routes for the ingress controller, browse to the two applications. Open a web browser to the IP address of your NGINX ingress controller, such as *EXTERNAL_IP*. The first demo application is displayed in the web browser, as shown in the following example:

Now add the */hello-world-two* path to the IP address, such as *EXTERNAL_IP/hello-world-two*. The second demo application with the custom title is displayed:

### Test an internal IP address

Create a test pod and attach a terminal session to it.

`kubectl run -it --rm aks-ingress-test --image=mcr.microsoft.com/dotnet/runtime-deps:6.0 --namespace ingress-basic`

Install

`curl`

in the pod using`apt-get`

.`apt-get update && apt-get install -y curl`

Access the address of your Kubernetes ingress controller using

`curl`

, such as. Provide your own internal IP address specified when you deployed the ingress controller.[http://10.224.0.42](http://10.224.0.42)`curl -L http://10.224.0.42`

No path was provided with the address, so the ingress controller defaults to the

*/*route. The first demo application is returned, as shown in the following condensed example output:`<!DOCTYPE html> <html xmlns="http://www.w3.org/1999/xhtml"> <head> <link rel="stylesheet" type="text/css" href="/static/default.css"> <title>Welcome to Azure Kubernetes Service (AKS)</title> [...]`

Add the

*/hello-world-two*path to the address, such as.[http://10.224.0.42/hello-world-two](http://10.224.0.42/hello-world-two)`curl -L -k http://10.224.0.42/hello-world-two`

The second demo application with the custom title is returned, as shown in the following condensed example output:

`<!DOCTYPE html> <html xmlns="http://www.w3.org/1999/xhtml"> <head> <link rel="stylesheet" type="text/css" href="/static/default.css"> <title>AKS Ingress Demo</title> [...]`


## Clean up resources

This article used Helm to install the ingress components and sample apps. When you deploy a Helm chart, many Kubernetes resources are created. These resources include pods, deployments, and services. To clean up these resources, you can either delete the entire sample namespace, or the individual resources.

### Delete the sample namespace and all resources

To delete the entire sample namespace, use the `kubectl delete`

command and specify your namespace name. All the resources in the namespace are deleted.

```
kubectl delete namespace ingress-basic
```


### Delete resources individually

Alternatively, a more granular approach is to delete the individual resources created.

List the Helm releases with the

`helm list`

command.`helm list --namespace ingress-basic`

Look for charts named

*ingress-nginx*and*aks-helloworld*, as shown in the following example output:`NAME NAMESPACE REVISION UPDATED STATUS CHART APP VERSION ingress-nginx ingress-basic 1 2020-01-06 19:55:46.358275 -0600 CST deployed nginx-ingress-1.27.1 0.26.1`

Uninstall the releases with the

`helm uninstall`

command.`helm uninstall ingress-nginx --namespace ingress-basic`

Remove the two sample applications.

`kubectl delete -f aks-helloworld-one.yaml --namespace ingress-basic kubectl delete -f aks-helloworld-two.yaml --namespace ingress-basic`

Remove the ingress route that directed traffic to the sample apps.

`kubectl delete -f hello-world-ingress.yaml`

Delete the namespace using the

`kubectl delete`

command and specifying your namespace name.`kubectl delete namespace ingress-basic`


## Next steps

To configure TLS with your existing ingress components, see [Use TLS with an ingress controller](/en-us/previous-versions/azure/aks/ingress-tls).

To configure your AKS cluster to use application routing, see [Application routing add-on](/en-us/azure/aks/app-routing).

This article included some external components to AKS. To learn more about these components, see the following project pages:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/long-term-support -->

# Long-term support for Azure Kubernetes Service (AKS) versions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Kubernetes community releases a new minor version approximately every four months, with a support window for each version for one year. In Azure Kubernetes Service (AKS), this support window is called *community support*.

AKS supports versions of Kubernetes that are within this *community support* window to push bug fixes and security updates from community releases. While the community support release cadence provides benefits, it requires that you keep up to date with Kubernetes releases, which can be difficult depending on your application's dependencies and the pace of change in the Kubernetes ecosystem.

To help you manage your Kubernetes version upgrades, AKS provides a *long-term support* (LTS) option, which extends the support window for a Kubernetes version to give you more time to plan and test upgrades to newer Kubernetes versions.

## AKS support types

After approximately one year, a given Kubernetes minor version exits *community support*, making bug fixes and security updates unavailable for your AKS clusters.

AKS offers one year of *community support* and one year of *long-term support* to backport security fixes from the upstream community. The upstream LTS working group contributes to the community, extending the support window. LTS provides more time to plan and test upgrades over two years from the Kubernetes version's general availability (GA).

| Community support | Long-term support | |
|---|---|---|
When to use |
When you can keep up with upstream Kubernetes releases | When you need control over when to migrate from one version to another |
Supported versions |
Three most recent GA minor versions | All supported Kubernetes versions from 1.27 onward are eligible for Long-Term Support (LTS). |

## LTS Patch process

LTS supports only the two most recent patch versions. This differs from Community support, where all patch versions are supported. However, AKS reserves the right to deprecate any patch version in response to critical security vulnerabilities (CVEs). For more details on community support policy, see [Kubernetes version support policy](supported-kubernetes-versions#kubernetes-version-support-policy).

To identify the latest supported patch versions, refer to the [AKS release tracker](https://releases.aks.azure.com/webpage/index.html).

We recommend enabling the [auto-upgrade patch channel](auto-upgrade-cluster) to ensure your clusters remain up-to-date with the latest patches.

## Enable long-term support

**Enabling LTS requires moving your cluster to the Premium tier and explicitly selecting the LTS support plan**. While it's possible to enable LTS when the cluster is in *community support*, you're charged once you enable the Premium tier.

Note

We strongly recommend enabling the patch auto-upgrade channel to ensure your cluster always receives the latest supported patches. LTS only supports the last two patch versions for each minor version. Clusters not on the latest patches may lose support.

### Enable LTS on a new cluster

Create a new cluster with LTS enabled using the

command.`az aks create`

The following command creates a new AKS cluster with LTS enabled using Kubernetes version 1.27 as an example. To review available Kubernetes releases, see the

[AKS release tracker](release-tracker).`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --tier premium \ --k8s-support-plan AKSLongTermSupport \ --kubernetes-version 1.27 \ --auto-upgrade-channel patch \ --generate-ssh-keys`


### Enable LTS on an existing cluster

Enable LTS on an existing cluster using the

command.`az aks update`

`az aks update --resource-group <resource-group-name> --name <cluster-name> --tier premium --k8s-support-plan AKSLongTermSupport --auto-upgrade-channel patch`


Tip

To see which Kubernetes versions you can upgrade to, use the [AKS release tracker](https://releases.aks.azure.com/webpage/index.html) or run `az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name>`

.

## Migrate to the latest LTS version

The upstream Kubernetes community supports a two-minor-version upgrade path. The process migrates the objects in your Kubernetes cluster as part of the upgrade process, and provides a tested and accredited migration path.

If you want to carry out an in-place migration, the AKS service migrates your control plane from the previous LTS version to the latest, and then migrate your data plane. To carry out an in-place upgrade to the latest LTS version, you need to specify an LTS enabled Kubernetes version as the upgrade target.

Migrate to the latest LTS version using the

command.`az aks upgrade`

The following command uses Kubernetes version 1.32.2 as an example version. To review available Kubernetes releases, see the

[AKS release tracker](release-tracker).`az aks upgrade --resource-group <resource-group-name> --name <cluster-name> --kubernetes-version 1.32.2`

Note

Moving forward, all AKS Kubernetes versions will be LTS-compatible. For the latest LTS calendar, visit the

[AKS Kubernetes Release Calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar). To view available LTS releases and their patches by region, see the[AKS release tracker](release-tracker).

## Disable long-term support on an existing cluster

**Disabling LTS on an existing cluster requires moving your cluster to the free or standard tier and explicitly selecting the KubernetesOfficial support plan**.

There are approximately two years between one LTS version and the next. In lieu of upstream support for migrating more than two minor versions, there's a high likelihood your application depends on Kubernetes APIs that are deprecated. We recommend you thoroughly test your application on the target LTS Kubernetes version and carry out a blue/green deployment from one version to another.

Disable LTS on an existing cluster using the

command.`az aks update`

`az aks update --resource-group <resource-group-name> --name <cluster-name> --tier [free|standard] --k8s-support-plan KubernetesOfficial`

Upgrade the cluster to a later supported version using the

command.`az aks upgrade`

The following command uses Kubernetes version 1.28.3 as an example version. To review available Kubernetes releases, see the

[AKS release tracker](release-tracker).`az aks upgrade --resource-group <resource-group-name> --name <cluster-name> --kubernetes-version 1.28.3`


## Unsupported add-ons and features

The AKS team currently tracks add-on versions where Kubernetes community support exists. Once a version leaves community support, we rely on open-source projects for managed add-ons to continue that support. Due to various external factors, some add-ons and features might not support Kubernetes versions outside these upstream community support windows.

The following table provides a list of add-ons and features that aren't supported and the reasons they're unsupported:

| Add-on / Feature | Reason it's unsupported |
|---|---|
| Calico | Requires Calico Enterprise agreement past community support. |
| Key Management Service (KMS) | KMSv2 replaces KMS during this LTS cycle. |
| Dapr | AKS extensions aren't supported. |
| Application Gateway Ingress Controller | Migration to App Gateway for Containers happens during LTS period. |
| Open Service Mesh | OSM is deprecated. |
| AAD Pod Identity | Deprecated in place of Workload Identity. |

Note

You can't move your cluster to long-term support if any of these add-ons or features are enabled.

While these AKS managed add-ons aren't supported by Microsoft, you can install their open-source versions on your cluster if you want to use them past community support.

## How we decide the next LTS version

Versions of Kubernetes LTS are available for two years from GA, and we mark a higher version of Kubernetes as LTS based on the following criteria:

- That sufficient time elapsed for customers to migrate from the prior LTS version to the current LTS version.
- The previous version completed a two year support window.

Read the [AKS release notes](https://github.com/Azure/AKS/releases) to stay informed of when you're able to plan your migration.

## Frequently asked questions

### Can I create a new AKS cluster with an LTS version after community support ends?

Yes, you can create a new AKS cluster using an LTS version even after its community support period has ended, provided you have opted into LTS. However, this is only valid until the end of the LTS version's lifecycle. After that, you must upgrade to the next supported LTS version. For more details, see the [AKS Kubernetes Release Calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar).

### Can I enable and disable LTS on an AKS-supported version after community support ends?

Yes, you can enable the LTS support plan on any AKS-supported version even after its community support period has ended. However, once the community support period has ended, you can't disable LTS for that version.

### Does a community-supported AKS cluster automatically become LTS eligible after End of Life?

No, you must explicitly enable LTS on the cluster to receive support. This also requires upgrading to the Premium tier. Refer to the [Premium tier pricing](https://azure.microsoft.com/pricing/details/kubernetes-service/) for more information.

### Will every AKS version support Long-Term Support (LTS)?

Yes, AKS ensures that all supported Kubernetes versions are eligible for Long-Term Support (LTS). You can opt into LTS for any supported version available today.

### What is the pricing model for LTS?

LTS is available on the Premium tier refer to the [Premium tier pricing](https://azure.microsoft.com/pricing/details/kubernetes-service/) for more information.

### Will enabling LTS disrupt workloads?

No. It’s a configuration-only change; it doesn’t reimage nodes or disrupt workloads, so no downtime is expected.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-azure-cni-overlay -->

# Overview of Azure CNI Overlay networking in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure CNI Overlay is a networking model for Azure Kubernetes Service (AKS) that provides efficient IP address management and high-performance pod communication. This article provides an overview of Azure CNI Overlay, including its architecture, IP address planning, and differences from the traditional kubenet networking model.

## Overview of overlay networking

The traditional [Azure Container Networking Interface (CNI)](configure-azure-cni) assigns a virtual network IP address to every pod. It assigns this IP address from a reserved set of IPs on every node *or* a separate subnet reserved for pods. This approach requires IP address planning and might lead to address exhaustion, which introduces difficulties scaling your clusters as your application demands grow.

In overlay networking, only the Kubernetes cluster nodes are assigned IPs from subnets. Pods receive IPs from a private Classless Inter-Domain Routing (CIDR) range provided at the time of cluster creation. Each node is assigned a `/24`

address space carved out from the same CIDR. Extra nodes created when you scale out a cluster automatically receive `/24`

address spaces from the same CIDR. Azure CNI assigns IPs to pods from this `/24`

space.

A separate routing domain is created in the Azure networking stack for the pod's private CIDR space. This domain creates an overlay network for direct communication between pods. There's no need to provision custom routes on the cluster subnet or use an encapsulation method to tunnel traffic between pods, which provides connectivity performance between pods on par with virtual machines (VMs) in a virtual network. Workloads running within the pods aren't even aware that network address manipulation is happening.


Communication with endpoints outside the cluster, such as on-premises and peered virtual networks, uses the node IP through network address translation (NAT). Azure CNI translates the source IP (overlay IP of the pod) of the traffic to the primary IP address of the VM. This translation enables the Azure networking stack to route the traffic to the destination.

Endpoints outside the cluster can't connect to a pod directly. You have to publish the pod's application as a Kubernetes Load Balancer service to make it reachable on the virtual network.

You can provide outbound (egress) connectivity to the internet for overlay pods by using a [standard load balancer](egress-outboundtype#outbound-type-of-loadbalancer) or [managed NAT gateway](nat-gateway). You can also control egress traffic by directing it to a firewall via [user-defined routes on the cluster subnet](egress-outboundtype#outbound-type-of-userdefinedrouting).

You can configure ingress connectivity to the cluster by using an ingress controller, such as Application Gateway for Containers, NGINX, or the application routing add-on.

## Differences between kubenet and Azure CNI Overlay

Like Azure CNI Overlay, kubenet assigns IP addresses to pods from an address space that's logically different from the virtual network, but it has scaling and other limitations. The following table provides a detailed comparison between kubenet and Azure CNI Overlay:

| Area | Azure CNI Overlay | kubenet |
|---|---|---|
| Cluster scale | 5,000 nodes and 250 pods per node | 400 nodes and 250 pods per node |
| Network configuration | Simple - no extra configurations required for pod networking | Complex - requires route tables and user-defined routes on the cluster subnet for pod networking |
| Pod connectivity performance | Performance on par with VMs in a virtual network | Extra hop adds latency |
| Kubernetes network policies | Azure network policies, Calico, Cilium | Calico |
| OS platforms supported | Linux, Windows Server 2022, Windows Server 2019 | Linux only |

Note

If you don't want to assign virtual network IP addresses to pods due to IP shortage, we recommend using Azure CNI Overlay.

## IP address planning

The following sections provide guidance on how to plan your IP address space for Azure CNI Overlay.

### Cluster nodes

When you set up your AKS cluster, make sure that your virtual network subnets have enough room to grow for future scaling. You can assign each node pool to a dedicated subnet. A `/24`

subnet can fit up to 251 nodes because the first three IP addresses are reserved for management tasks.

### Pods

The `/24`

size that Azure CNI Overlay assigns is fixed and can't be increased or decreased. You can run up to 250 pods on a node. When you plan the pod address space, ensure that the private CIDR is large enough to provide `/24`

address spaces for new nodes to support future cluster expansion.

When you plan IP address space for pods, consider the following factors:

- You can use the same pod CIDR space on multiple independent AKS clusters in the same virtual network.
- Pod CIDR space must not overlap with the cluster subnet range.
- Pod CIDR space must not overlap with directly connected networks, like virtual network peering, Azure ExpressRoute, or VPN. If external traffic has source IPs in the pod CIDR range, it needs translation to a non-overlapping IP via Source Network Address Translation (SNAT) to communicate with the cluster.
- Pod CIDR space
*can only be expanded*.

### Kubernetes service address range

The size of the service address CIDR depends on the number of cluster services that you plan to create. It must be smaller than `/12`

. This range shouldn't overlap with the pod CIDR range, cluster subnet range, and IP range used in peered virtual networks and on-premises networks.

### Kubernetes service IP address for DNS

The IP address for DNS is within the Kubernetes service address range that cluster service discovery uses. Don't use the first IP address in your address range, because this address is used for the `kubernetes.default.svc.cluster.local`

address.

Important

The private CIDR ranges available for the pod CIDR are defined in [RFC 1918](https://tools.ietf.org/html/rfc1918) and [RFC 6598](https://tools.ietf.org/html/rfc6598). Although we don't block the use of public IP ranges, they're considered out of Microsoft's support scope. We recommend using private IP ranges for the pod CIDR.

When you use Azure CNI in overlay mode, ensure that the pod CIDR doesn't overlap with any external IP addresses or networks (such as on-premises networks, peered virtual networks, or ExpressRoute). If an external host uses an IP within the pod CIDR, packets destined for that host from the pod might be redirected into the overlay network and SNAT'd by the node. This situation causes the external endpoint to become unreachable.

## Network security groups

Pod-to-pod traffic with Azure CNI Overlay isn't encapsulated, and subnet [network security group (NSG)](/en-us/azure/virtual-network/network-security-groups-overview) rules are applied. If the subnet NSG contains deny rules that would affect the pod CIDR traffic, make sure that the following rules are in place to ensure proper cluster functionality (in addition to all [AKS egress requirements](limit-egress-traffic)):

- Traffic from the node CIDR to the node CIDR on all ports and protocols
- Traffic from the node CIDR to the pod CIDR on all ports and protocols (required for service traffic routing)
- Traffic from the pod CIDR to the pod CIDR on all ports and protocols (required for pod-to-pod and pod-to-service traffic, including DNS)

Traffic from a pod to any destination outside the pod CIDR block uses SNAT to set the source IP to the IP of the node where the pod runs.

If you want to restrict traffic between workloads in the cluster, we recommend using [network policies](use-network-policies).

## Maximum pods per node

You can configure the maximum number of pods per node at the time of cluster creation or when you add a new node pool. The default for Azure CNI Overlay is 250. The maximum value that you can specify in Azure CNI Overlay is 250, and the minimum value is 10. The value for maximum pods per node that you configure during creation of a node pool applies to the nodes in that node pool only.

Choosing a network model

Azure CNI offers two IP addressing options for pods: *overlay networking* and the *traditional configuration that assigns virtual network IPs to pods*. The choice of which option to use for your AKS cluster is a balance between flexibility and advanced configuration needs. The following considerations help outline when each network model might be the most appropriate.

Use overlay networking when:

- You want to scale to a large number of pods but are limited by IP address space in your virtual network.
- Most of the pod communication is within the cluster.
- You don't need advanced AKS features, such as virtual nodes.

Use the traditional virtual network option when:

- You have available IP address space.
- Most of the pod communication is to resources outside the cluster.
- Resources outside the cluster need to reach pods directly.
- You need AKS advanced features, such as virtual nodes.

## Limitations with Azure CNI Overlay

Azure CNI Overlay has the following limitations:

- VM availability sets aren't supported.
- You can't use
[DCsv2-series](/en-us/azure/virtual-machines/dcv2-series)virtual machines in node pools. To meet requirements for confidential computing, consider using[DCasv5 or DCadsv5-series confidential VMs](/en-us/azure/virtual-machines/dcasv5-dcadsv5-series)instead. - If you're using your own subnet to deploy the cluster, the names of the subnet, the virtual network, and the resource group that contains the virtual network must be 63 characters or fewer. These names are used as labels in AKS worker nodes, so they're subject to
[Kubernetes syntax rules for labels](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/#syntax-and-character-set).

## Related content

To get started with Azure CNI Overlay in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-migrate-in-tree-volumes -->

# Migrate from in-tree storage class to CSI drivers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The implementation of the [Container Storage Interface (CSI) driver](csi-storage-drivers) was introduced in Azure Kubernetes Service (AKS) starting with version 1.21. By adopting and using CSI as the standard, your existing stateful workloads using in-tree Persistent Volumes (PVs) should be migrated or upgraded to use the CSI driver.

To make this process as simple as possible, and to ensure no data loss, this article provides different migration options. These options include scripts to help ensure a smooth migration from in-tree to Azure Disks and Azure Files CSI drivers.

## Before you begin

- The Azure CLI version 2.37.0 or later. Run
`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - Kubectl and cluster administrators have access to create, get, list, delete access to a PVC or PV, volume snapshot, or volume snapshot content. For a Microsoft Entra RBAC enabled cluster, you're a member of the
[Azure Kubernetes Service RBAC Cluster Admin](manage-azure-rbac#create-role-assignments-for-cluster-access)role.

## Migrate Disk volumes

Note

The labels `failure-domain.beta.kubernetes.io/zone`

and `failure-domain.beta.kubernetes.io/region`

have been deprecated in AKS 1.24 and removed in 1.28. If your existing persistent volumes are still using nodeAffinity matching these two labels, you need to change them to `topology.kubernetes.io/zone`

and `topology.kubernetes.io/region`

labels in the new persistent volume setting.

Migration from in-tree to CSI is supported using two migration options:

- Create a static volume
- Create a dynamic volume

### Create a static volume

Using this option, you create a PV by statically assigning `claimRef`

to a new PVC that you'll create later, and specify the `volumeName`

for the *PersistentVolumeClaim*.


The benefits of this approach are:

- It's simple and can be automated.
- No need to clean up original configuration using in-tree storage class.
- Low risk as you're only performing a logical deletion of Kubernetes PV/PVC, the actual physical data isn't deleted.
- No extra cost incurred as the result of not having to create additional Azure objects, such as disk, snapshots, etc.

The following are important considerations to evaluate:

- Transition to static volumes from original dynamic-style volumes requires constructing and managing PV objects manually for all options.
- Potential application downtime when redeploying the new application with reference to the new PVC object.

#### Migration

Update the existing PV

`ReclaimPolicy`

from**Delete**to**Retain**by running the following command:`kubectl patch pv pvName -p '{"spec":{"persistentVolumeReclaimPolicy":"Retain"}}'`

Replace

**pvName**with the name of your selected PersistentVolume. Alternatively, if you want to update the reclaimPolicy for multiple PVs, create a file named**patchReclaimPVs.sh**and copy in the following code.`#!/bin/bash # Patch the Persistent Volume in case ReclaimPolicy is Delete NAMESPACE=$1 i=1 for PVC in $(kubectl get pvc -n $NAMESPACE | awk '{ print $1}'); do # Ignore first record as it contains header if [ $i -eq 1 ]; then i=$((i + 1)) else PV="$(kubectl get pvc $PVC -n $NAMESPACE -o jsonpath='{.spec.volumeName}')" RECLAIMPOLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" echo "Reclaim Policy for Persistent Volume $PV is $RECLAIMPOLICY" if [[ $RECLAIMPOLICY == "Delete" ]]; then echo "Updating ReclaimPolicy for $pv to Retain" kubectl patch pv $PV -p '{"spec":{"persistentVolumeReclaimPolicy":"Retain"}}' fi fi done`

Execute the script with the

`namespace`

parameter to specify the cluster namespace`./PatchReclaimPolicy.sh <namespace>`

.Get a list of all of the PVCs in namespace sorted by

**creationTimestamp**by running the following command. Set the namespace using the`--namespace`

argument along with the actual cluster namespace.`kubectl get pvc -n <namespace> --sort-by=.metadata.creationTimestamp -o custom-columns=NAME:.metadata.name,CreationTime:.metadata.creationTimestamp,StorageClass:.spec.storageClassName,Size:.spec.resources.requests.storage`

This step is helpful if you have a large number of PVs that need to be migrated, and you want to migrate a few at a time. Running this command enables you to identify which PVCs were created in a given time frame. When you run the

*CreatePV.sh*script, two of the parameters are start time and end time that enable you to only migrate the PVCs during that period of time.Create a file named

**CreatePV.sh**and copy in the following code. The script does the following:- Creates a new PersistentVolume with name
`existing-pv-csi`

for all PersistentVolumes in namespaces for storage class`storageClassName`

. - Configure new PVC name as
`existing-pvc-csi`

. - Creates a new PVC with the PV name you specify.

`#!/bin/bash #kubectl get pvc -n <namespace> --sort-by=.metadata.creationTimestamp -o custom-columns=NAME:.metadata.name,CreationTime:.metadata.creationTimestamp,StorageClass:.spec.storageClassName,Size:.spec.resources.requests.storage # TimeFormat 2022-04-20T13:19:56Z NAMESPACE=$1 FILENAME=$(date +%Y%m%d%H%M)-$NAMESPACE EXISTING_STORAGE_CLASS=$2 STORAGE_CLASS_NEW=$3 STARTTIMESTAMP=$4 ENDTIMESTAMP=$5 i=1 for PVC in $(kubectl get pvc -n $NAMESPACE | awk '{ print $1}'); do # Ignore first record as it contains header if [ $i -eq 1 ]; then i=$((i + 1)) else PVC_CREATION_TIME=$(kubectl get pvc $PVC -n $NAMESPACE -o jsonpath='{.metadata.creationTimestamp}') if [[ $PVC_CREATION_TIME >= $STARTTIMESTAMP ]]; then if [[ $ENDTIMESTAMP > $PVC_CREATION_TIME ]]; then PV="$(kubectl get pvc $PVC -n $NAMESPACE -o jsonpath='{.spec.volumeName}')" RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" STORAGECLASS="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.storageClassName}')" echo $PVC RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" if [[ $RECLAIM_POLICY == "Retain" ]]; then if [[ $STORAGECLASS == $EXISTING_STORAGE_CLASS ]]; then STORAGE_SIZE="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.capacity.storage}')" SKU_NAME="$(kubectl get storageClass $STORAGE_CLASS_NEW -o jsonpath='{.parameters.skuname}')" DISK_URI="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.azureDisk.diskURI}')" PERSISTENT_VOLUME_RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" cat >$PVC-csi.yaml <<EOF apiVersion: v1 kind: PersistentVolume metadata: annotations: pv.kubernetes.io/provisioned-by: disk.csi.azure.com name: $PV-csi spec: accessModes: - ReadWriteOnce capacity: storage: $STORAGE_SIZE claimRef: apiVersion: v1 kind: PersistentVolumeClaim name: $PVC-csi namespace: $NAMESPACE csi: driver: disk.csi.azure.com volumeAttributes: csi.storage.k8s.io/pv/name: $PV-csi csi.storage.k8s.io/pvc/name: $PVC-csi csi.storage.k8s.io/pvc/namespace: $NAMESPACE requestedsizegib: "$STORAGE_SIZE" skuname: $SKU_NAME volumeHandle: $DISK_URI persistentVolumeReclaimPolicy: $PERSISTENT_VOLUME_RECLAIM_POLICY storageClassName: $STORAGE_CLASS_NEW --- apiVersion: v1 kind: PersistentVolumeClaim metadata: name: $PVC-csi namespace: $NAMESPACE spec: accessModes: - ReadWriteOnce storageClassName: $STORAGE_CLASS_NEW resources: requests: storage: $STORAGE_SIZE volumeName: $PV-csi EOF kubectl apply -f $PVC-csi.yaml LINE="PVC:$PVC,PV:$PV,StorageClassTarget:$STORAGE_CLASS_NEW" printf '%s\n' "$LINE" >>$FILENAME fi fi fi fi fi done`

- Creates a new PersistentVolume with name
To create a new PersistentVolume for all PersistentVolumes in the namespace, execute the script

**CreatePV.sh**with the following parameters:`namespace`

- The cluster namespace`sourceStorageClass`

- The in-tree storage driver-based StorageClass`targetCSIStorageClass`

- The CSI storage driver-based StorageClass, which can be either one of the default storage classes that have the provisioner set to**disk.csi.azure.com**or**file.csi.azure.com**. Or you can create a custom storage class as long as it is set to either one of those two provisioners.`startTimeStamp`

- Provide a start time**before**PVC creation time in the format**yyyy-mm-ddthh:mm:ssz**`endTimeStamp`

- Provide an end time in the format**yyyy-mm-ddthh:mm:ssz**.

`./CreatePV.sh <namespace> <sourceIntreeStorageClass> <targetCSIStorageClass> <startTimestamp> <endTimestamp>`

Update your application to use the new PVC.


### Create a dynamic volume

Using this option, you dynamically create a Persistent Volume from a Persistent Volume Claim.


The benefits of this approach are:

It's less risky because all new objects are created while retaining other copies with snapshots.

No need to construct PVs separately and add volume name in PVC manifest.


The following are important considerations to evaluate:

While this approach is less risky, it does create multiple objects that will increase your storage costs.

During creation of the new volume(s), your application is unavailable.

Deletion steps should be performed with caution. Temporary

[resource locks](/en-us/azure/azure-resource-manager/management/lock-resources)can be applied to your resource group until migration is completed and your application is successfully verified.Perform data validation/verification as new disks are created from snapshots.


#### Migration

Before proceeding, verify the following:

For specific workloads where data is written to memory before being written to disk, the application should be stopped and to allow in-memory data to be flushed to disk.

`VolumeSnapshot`

class should exist as shown in the following example YAML:`apiVersion: snapshot.storage.k8s.io/v1 kind: VolumeSnapshotClass metadata: name: custom-disk-snapshot-sc driver: disk.csi.azure.com deletionPolicy: Delete parameters: incremental: "false"`


Get list of all the PVCs in a specified namespace sorted by

*creationTimestamp*by running the following command. Set the namespace using the`--namespace`

argument along with the actual cluster namespace.`kubectl get pvc --namespace <namespace> --sort-by=.metadata.creationTimestamp -o custom-columns=NAME:.metadata.name,CreationTime:.metadata.creationTimestamp,StorageClass:.spec.storageClassName,Size:.spec.resources.requests.storage`

This step is helpful if you have a large number of PVs that need to be migrated, and you want to migrate a few at a time. Running this command enables you to identify which PVCs were created in a given time frame. When you run the

*MigrateCSI.sh*script, two of the parameters are start time and end time that enable you to only migrate the PVCs during that period of time.Create a file named

**MigrateToCSI.sh**and copy in the following code. The script does the following:- Creates a full disk snapshot using the Azure CLI
- Creates
`VolumesnapshotContent`

- Creates
`VolumeSnapshot`

- Creates a new PVC from
`VolumeSnapshot`

- Creates a new file with the filename
`<namespace>-timestamp`

, which contains a list of all old resources that needs to be cleaned up.

`#!/bin/bash #kubectl get pvc -n <namespace> --sort-by=.metadata.creationTimestamp -o custom-columns=NAME:.metadata.name,CreationTime:.metadata.creationTimestamp,StorageClass:.spec.storageClassName,Size:.spec.resources.requests.storage # TimeFormat 2022-04-20T13:19:56Z NAMESPACE=$1 FILENAME=$NAMESPACE-$(date +%Y%m%d%H%M) EXISTING_STORAGE_CLASS=$2 STORAGE_CLASS_NEW=$3 VOLUME_STORAGE_CLASS=$4 START_TIME_STAMP=$5 END_TIME_STAMP=$6 i=1 for PVC in $(kubectl get pvc -n $NAMESPACE | awk '{ print $1}'); do # Ignore first record as it contains header if [ $i -eq 1 ]; then i=$((i + 1)) else PVC_CREATION_TIME=$(kubectl get pvc $PVC -n $NAMESPACE -o jsonpath='{.metadata.creationTimestamp}') if [[ $PVC_CREATION_TIME > $START_TIME_STAMP ]]; then if [[ $END_TIME_STAMP > $PVC_CREATION_TIME ]]; then PV="$(kubectl get pvc $PVC -n $NAMESPACE -o jsonpath='{.spec.volumeName}')" RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" STORAGE_CLASS="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.storageClassName}')" echo $PVC RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" if [[ $STORAGE_CLASS == $EXISTING_STORAGE_CLASS ]]; then STORAGE_SIZE="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.capacity.storage}')" SKU_NAME="$(kubectl get storageClass $STORAGE_CLASS_NEW -o jsonpath='{.parameters.skuname}')" DISK_URI="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.azureDisk.diskURI}')" TARGET_RESOURCE_GROUP="$(cut -d'/' -f5 <<<"$DISK_URI")" echo $DISK_URI SUBSCRIPTION_ID="$(echo $DISK_URI | grep -o 'subscriptions/[^/]*' | sed 's#subscriptions/##g')" echo $TARGET_RESOURCE_GROUP PERSISTENT_VOLUME_RECLAIM_POLICY="$(kubectl get pv $PV -n $NAMESPACE -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" az snapshot create --resource-group $TARGET_RESOURCE_GROUP --name $PVC-$FILENAME --source "$DISK_URI" --subscription ${SUBSCRIPTION_ID} SNAPSHOT_PATH=$(az snapshot list --resource-group $TARGET_RESOURCE_GROUP --query "[?name == '$PVC-$FILENAME'].id | [0]" --subscription ${SUBSCRIPTION_ID}) SNAPSHOT_HANDLE=$(echo "$SNAPSHOT_PATH" | tr -d '"') echo $SNAPSHOT_HANDLE sleep 10 # Create Restore File cat <<EOF >$PVC-csi.yml apiVersion: snapshot.storage.k8s.io/v1 kind: VolumeSnapshotContent metadata: name: $PVC-$FILENAME spec: deletionPolicy: 'Delete' driver: 'disk.csi.azure.com' volumeSnapshotClassName: $VOLUME_STORAGE_CLASS source: snapshotHandle: $SNAPSHOT_HANDLE volumeSnapshotRef: apiVersion: snapshot.storage.k8s.io/v1 kind: VolumeSnapshot name: $PVC-$FILENAME namespace: $1 --- apiVersion: snapshot.storage.k8s.io/v1 kind: VolumeSnapshot metadata: name: $PVC-$FILENAME namespace: $1 spec: volumeSnapshotClassName: $VOLUME_STORAGE_CLASS source: volumeSnapshotContentName: $PVC-$FILENAME --- apiVersion: v1 kind: PersistentVolumeClaim metadata: name: csi-$PVC namespace: $1 spec: accessModes: - ReadWriteOnce storageClassName: $STORAGE_CLASS_NEW resources: requests: storage: $STORAGE_SIZE dataSource: name: $PVC-$FILENAME kind: VolumeSnapshot apiGroup: snapshot.storage.k8s.io EOF kubectl create -f $PVC-csi.yml LINE="OLDPVC:$PVC,OLDPV:$PV,VolumeSnapshotContent:volumeSnapshotContent-$FILENAME,VolumeSnapshot:volumesnapshot$FILENAME,OLDdisk:$DISK_URI" printf '%s\n' "$LINE" >>$FILENAME fi fi fi fi done`

To migrate the disk volumes, execute the script

**MigrateToCSI.sh**with the following parameters:`namespace`

- The cluster namespace`sourceStorageClass`

- The in-tree storage driver-based StorageClass`targetCSIStorageClass`

- The CSI storage driver-based StorageClass`volumeSnapshotClass`

- Name of the volume snapshot class. For example,`custom-disk-snapshot-sc`

.`startTimeStamp`

- Provide a start time in the format**yyyy-mm-ddthh:mm:ssz**.`endTimeStamp`

- Provide an end time in the format**yyyy-mm-ddthh:mm:ssz**.

`./MigrateToCSI.sh <namespace> <sourceStorageClass> <TargetCSIstorageClass> <VolumeSnapshotClass> <startTimestamp> <endTimestamp>`

Update your application to use the new PVC.

Manually delete the older resources including in-tree PVC/PV, VolumeSnapshot, and VolumeSnapshotContent. Otherwise, maintaining the in-tree PVC/PC and snapshot objects will generate more cost.


## Migrate File share volumes

Migration from in-tree to CSI is supported by creating a static volume:

- No need to clean up original configuration using in-tree storage class.
- Low risk as you're only performing a logical deletion of Kubernetes PV/PVC, the actual physical data isn't deleted.
- No extra cost incurred as the result of not having to create additional Azure objects, such as file shares, etc.

### Migration

Update the existing PV

`ReclaimPolicy`

from**Delete**to**Retain**by running the following command:`kubectl patch pv pvName -p '{"spec":{"persistentVolumeReclaimPolicy":"Retain"}}'`

Replace

**pvName**with the name of your selected PersistentVolume. Alternatively, if you want to update the reclaimPolicy for multiple PVs, create a file named**patchReclaimPVs.sh**and copy in the following code.`#!/bin/bash # Patch the Persistent Volume in case ReclaimPolicy is Delete namespace=$1 i=1 for pvc in $(kubectl get pvc -n $namespace | awk '{ print $1}'); do # Ignore first record as it contains header if [ $i -eq 1 ]; then i=$((i + 1)) else pv="$(kubectl get pvc $pvc -n $namespace -o jsonpath='{.spec.volumeName}')" reclaimPolicy="$(kubectl get pv $pv -n $namespace -o jsonpath='{.spec.persistentVolumeReclaimPolicy}')" echo "Reclaim Policy for Persistent Volume $pv is $reclaimPolicy" if [[ $reclaimPolicy == "Delete" ]]; then echo "Updating ReclaimPolicy for $pv to Retain" kubectl patch pv $pv -p '{"spec":{"persistentVolumeReclaimPolicy":"Retain"}}' fi fi done`

Execute the script with the

`namespace`

parameter to specify the cluster namespace`./PatchReclaimPolicy.sh <namespace>`

.Create a new Storage Class with the provisioner set to

`file.csi.azure.com`

, or you can use one of the default StorageClasses with the CSI file provisioner.Get the

`secretName`

and`shareName`

from the existing*PersistentVolumes*by running the following command:`kubectl describe pv pvName`

Create a new PV using the new StorageClass, and the

`shareName`

and`secretName`

from the in-tree PV. Create a file named*azurefile-mount-pv.yaml*and copy in the following code. Under`csi`

, update`resourceGroup`

,`volumeHandle`

, and`shareName`

. For mount options, the default value for*fileMode*and*dirMode*is*0777*.The default value for

`fileMode`

and`dirMode`

is**0777**.`apiVersion: v1 kind: PersistentVolume metadata: annotations: pv.kubernetes.io/provisioned-by: file.csi.azure.com name: azurefile spec: capacity: storage: 5Gi accessModes: - ReadWriteMany persistentVolumeReclaimPolicy: Retain storageClassName: azurefile-csi csi: driver: file.csi.azure.com readOnly: false volumeHandle: "{resource-group-name}#{account-name}#{file-share-name}" # make sure this volumeid is unique for every identical share in the cluster volumeAttributes: resourceGroup: EXISTING_RESOURCE_GROUP_NAME # optional, only set this when storage account is not in the same resource group as the cluster nodes shareName: aksshare nodeStageSecretRef: name: azure-secret namespace: default mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict - nosharesock - nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks`

Create a file named

*azurefile-mount-pvc.yaml*file with a*PersistentVolumeClaim*that uses the*PersistentVolume*using the following code.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azurefile spec: accessModes: - ReadWriteMany storageClassName: azurefile-csi volumeName: azurefile resources: requests: storage: 5Gi`

Use the

`kubectl`

command to create the*PersistentVolume*.`kubectl apply -f azurefile-mount-pv.yaml`

Use the

`kubectl`

command to create the*PersistentVolumeClaim*.`kubectl apply -f azurefile-mount-pvc.yaml`

Verify your

*PersistentVolumeClaim*is created and bound to the*PersistentVolume*by running the following command.`kubectl get pvc azurefile`

The output resembles the following:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE azurefile Bound azurefile 5Gi RWX azurefile 5s`

Update your container spec to reference your

*PersistentVolumeClaim*and update your pod. For example, copy the following code and create a file named*azure-files-pod.yaml*.`... volumes: - name: azure persistentVolumeClaim: claimName: azurefile`

The pod spec can't be updated in place. Use the following

`kubectl`

commands to delete and then re-create the pod.`kubectl delete pod mypod`

`kubectl apply -f azure-files-pod.yaml`


## Next steps

- For more information about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service](operator-best-practices-storage). - Protect your newly migrated CSI Driver based PVs by
[backing them up using Azure Backup for AKS](/en-us/azure/backup/azure-kubernetes-service-cluster-backup).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/free-standard-pricing-tiers -->

# Free, Standard, and Premium pricing tiers for Azure Kubernetes Service (AKS) cluster management

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Manage your Azure Kubernetes Service (AKS) clusters using AKS pricing tiers. This article explains the differences between these tiers, when to use each tier, and how to create or update AKS clusters using Azure CLI.

## About AKS pricing tiers

AKS offers three pricing tiers for cluster management: the **Free tier**, the **Standard tier**, and the **Premium tier**.

**SKU and tier relationship**:

**Base SKU clusters**: Can use any of the three pricing tiers (Free, Standard, or Premium).**Automatic SKU clusters**: Must use the Standard tier (automatically selected during cluster creation).

## AKS pricing tiers comparison

The following table compares the Free, Standard, and Premium pricing tiers for AKS cluster management:

| Tier | When to use | Supported cluster types | Pricing | Feature comparison |
|---|---|---|---|---|
| Free | • Development/testing environments. • Learning and evaluation scenarios. • Non-production workloads. |
• Development clusters or small scale testing environments. • Clusters with fewer than 10 nodes. |
• Free cluster management. • Pay-as-you-go for resources you consume. |
• Recommended for clusters with fewer than 10 nodes, but can support up to 1,000 nodes. • Includes all current AKS features. |
| Standard | • Production workloads requiring 99.9-99.95% API server uptime. • Workloads needing financial service level agreement (SLA) coverage. |
• Default tier for Automatic SKU clusters. • Enterprise-grade or production workloads. • Clusters with up to 5,000 nodes. |
• Pay-as-you-go for resources you consume. •
|
• Uptime SLA is enabled by default. • Greater cluster reliability. • Supports up to 5,000 nodes in a cluster. • Includes all current AKS features. |
| Premium | • Production workloads requiring 99.9-99.95% API server uptime. • Workloads requiring 24-month
• Regulated environments requiring extended maintenance. |
• Enterprise-grade or production workloads. • Clusters with up to 5,000 nodes. |
• Pay-as-you-go for resources you consume. •
|
• Includes all current AKS features. •
|

## Uptime SLA terms and conditions

Standard and Premium tiers include Uptime SLA by default:

**With availability zones**: 99.95% availability of the Kubernetes API server**Without availability zones**: 99.9% availability of the Kubernetes API server**Free tier**: Best-effort uptime (no SLA guarantee)

For more information, see the [SLA](https://azure.microsoft.com/support/legal/sla/kubernetes-service/v1_1/).

## Region availability

The following tables outline the availability of AKS pricing tiers by region:

| Region type | Available pricing tiers |
|---|---|
| Public regions and Azure Government regions where
|

- Standard tier

- Premium tier

[Private AKS clusters](private-clusters)in all public regions where AKS is supported- Standard tier

- Premium tier

## Prerequisites

- You need
[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.47.0 or later. Find the current version using the`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You can create your cluster in an existing resource group or create a new one. To learn more about resource groups and working with them, see
[managing resource groups using the Azure CLI](/en-us/azure/azure-resource-manager/management/manage-resource-groups-cli).

## Create a resource group

Create a resource group using the

command.`az group create`

`# Set environment variables export REGION=<your-region> export RESOURCE_GROUP=<your-resource-group-name> # Create the resource group az group create --name $RESOURCE_GROUP --location $REGION`

Results:

`{ "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/"<your-resource-group-name>", "location": "<your-region>", "managedBy": null, "name": "<your-resource-group-name>", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`


## Create an AKS cluster in the Free tier

Create an AKS cluster in the Free tier using the

command with the`az aks create`

`--tier`

parameter set to`free`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --tier free \ --generate-ssh-keys`

Results:

`{ ... "sku": { "name": "Base", "tier": "Free" }, ... }`


## Create an AKS cluster in the Standard tier

Create an AKS cluster in the Standard tier using the

command with the`az aks create`

`--tier`

parameter set to`standard`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --tier standard \ --generate-ssh-keys`

Results:

`{ ... "sku": { "name": "Base", "tier": "Standard" }, ... }`


## Create an AKS cluster in the Premium tier

Important

When creating a cluster in the Premium tier, you must also enable the [LTS plan](long-term-support) by setting the `--k8s-support-plan`

parameter to `AKSLongTermSupport`

. You should enable/disable LTS and the Premium tier together.

Create an AKS cluster in the Premium tier using the

command with the`az aks create`

`--tier`

parameter set to`premium`

and the`--k8s-support-plan`

parameter set to`AKSLongTermSupport`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --tier premium \ --k8s-support-plan AKSLongTermSupport \ --generate-ssh-keys`

Results:

`{ ... "sku": { "name": "Base", "tier": "Premium" }, "supportPlan": "AKSLongTermSupport", ... }`


## Update an existing cluster from the Standard tier to the Free tier

Update an existing cluster from the Standard tier to the Free tier using the

command with the`az aks update`

`--tier`

parameter set to`free`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --tier free`

Results:

`{ ... "sku": { "name": "Base", "tier": "Free" }, ... }`


## Update an existing cluster from the Free tier to the Standard tier

Update an existing cluster from the Free tier to the Standard tier using the

command with the`az aks update`

`--tier`

parameter set to`standard`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --tier standard`

Results:

`{ ... "sku": { "name": "Base", "tier": "Standard" }, ... }`


## Update an existing cluster to or from the Premium tier

Important

[Updating existing clusters to or from the Premium tier](long-term-support#enable-lts-on-an-existing-cluster) requires changing the support plan.

### Update an existing cluster to the Premium tier

Update an existing cluster to the Premium tier using the

command with the`az aks update`

`--tier`

parameter set to`premium`

and the`--k8s-support-plan`

parameter set to`AKSLongTermSupport`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --tier premium --k8s-support-plan AKSLongTermSupport`

Results:

`{ ... "sku": { "name": "Base", "tier": "Premium" }, "supportPlan": "AKSLongTermSupport", ... }`


### Update an existing cluster from the Premium tier to the Free or Standard tier

Update an existing cluster from the Premium tier to the Free or Standard tier using the

command with the`az aks update`

`--tier`

parameter set to`free`

or`standard`

and the`--k8s-support-plan`

parameter set to`KubernetesOfficial`

. The following example shows updating to the Free tier.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --tier free --k8s-support-plan KubernetesOfficial`

Results:

`{ ... "sku": { "name": "Base", "tier": "Free" }, "supportPlan": "KubernetesOfficial", ... }`


## Update an existing cluster from the Base SKU to the Automatic SKU

Important

Make sure all the [AKS Automatic features](intro-aks-automatic) are enabled on your cluster before updating.

Update an existing cluster from the Base SKU to the Automatic SKU using the

command with the`az aks update`

`--sku`

parameter set to`Automatic`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --sku Automatic`

Results:

`{ ... "sku": { "name": "Automatic", "tier": "Standard" }, ... }`


## Update an existing cluster from the Automatic SKU to the Base SKU

Update an existing cluster from the Automatic SKU to the Base SKU using the

command with the`az aks update`

`--sku`

parameter set to`Base`

.`# Set environment variables export RESOURCE_GROUP=<your-resource-group-name> export CLUSTER_NAME=<your-aks-cluster-name> # Update the AKS cluster az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --sku Base`

Results:

`{ ... "sku": { "name": "Base", "tier": "Standard" }, ... }`


## Related content

- Use
[availability zones](availability-zones)to increase high availability with your AKS cluster workloads. [Limit egress traffic](limit-egress-traffic)on AKS clusters to meet security and compliance requirements.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/gpu-health-monitoring -->

# GPU health monitoring in Node Problem Detector (NPD) in Azure Kubernetes Service (AKS) nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how Azure Kubernetes Service (AKS) uses Node Problem Detector (NPD) to monitor the health of GPU-enabled node pools. NPD is a Kubernetes component that detects and reports node-level issues, including hardware faults, driver errors, and connectivity problems that can affect the performance and availability of GPU workloads.

## About GPU health monitoring in NPD

AKS supports GPU health monitoring through [Node Problem Detector (NPD)](node-problem-detector), enabling automatic detection and reporting of issues that affect GPU-enabled node pools on an AKS cluster. GPU health monitoring helps Kubernetes operators keep GPU nodes healthy and performant by surfacing hardware faults, communication failures, and system-level errors. NPD sets GPU-related node conditions and enable platform engineering teams to take action before issues impact application performance or availability.

These health signals are vital for ensuring optimal performance and reliability across a range of GPU workloads, including:

- Machine learning (ML) training and inference.
- AI model development.
- High-performance computing (HPC).
- Graphics rendering and data-intensive simulations.

## Limitations

AKS Node Problem Detector * does not* run GPU health checks on node pools with

`--gpu-driver none`

, where **self-managed**or custom GPU driver was installed on the nodes.

## Supported GPU health checks

NPD regularly monitors GPU-enabled node pools and sets conditions when anomalies are detected. The following GPU health checks are currently supported:

**GPUMissing**: NPD verifies that the number of GPUs detected by the`nvidia-smi`

utility matches the expected GPU count for the VM SKU assigned to the node.- A mismatch might indicate a hardware fault, driver issue, or misconfiguration. Accurate GPU enumeration is critical for ensuring scheduling accuracy and workload availability on GPU nodes.

**GPUXIDErrors**: Checks for XID (eXecution ID) errors emitted by the GPU driver in the kernel logs. XID errors are low-level GPU faults that typically occur when:- The driver misprograms the GPU.
- There's a corruption in the command stream sent to the GPU.
- A hardware failure or instability affects GPU operation.

For more information, see

[XID errors on NVIDIA GPUs](https://docs.nvidia.com/deploy/xid-errors/index.html).**NVLink Status**: For NVIDIA VM SKUs that support NVLink, this condition confirms that NVLink is active and functioning.- NVLink is a high-speed interconnect used to facilitate data transfer between multiple GPUs.
- If NVLink is inactive or degraded, multi-GPU workloads might experience reduced performance or communication bottlenecks.

For more information, see

[NVIDIA NVLink](https://www.nvidia.com/en-us/data-center/nvlink/).**InfiniBand Link Flapping**: NPD monitors for InfiniBand (IB) link flapping, or intermittent connectivity of the IB network device.- Link flapping shouldn't occur under normal operating conditions and might result in degraded inter-node communication for distributed workloads.
- It can also signal physical layer issues, misconfigured firmware, or driver instability.

**NVIDIA GRID Driver License Check**: For NVIDIA VM SKUs that support GRID driver, this condition verifies license status of the installed GRID driver on[supported NVIDIA VM SKUs](/en-us/azure/virtual-machines/sizes/gpu-accelerated/nvadsa10v5-series).- Invalid might indicate the installed GRID driver is not licensed.


## Frequently asked questions

### Does Node Problem Detector (NPD) automatically remediate GPU node issues?

NPD doesn't take direct action to remediate GPU-enabled node issues. NPD detects and reports problems by publishing Kubernetes node conditions and events. Any remediation (for example: draining a node, restarting workloads, or replacing faulty hardware) must be handled manually, through external automation, or alerting systems configured by the Kubernetes operator.

### On which Azure VM sizes does AKS conduct GPU health monitoring through NPD?

Currently, NPD conducts health checks on GPU nodes provisioned with the `Standard_ND96asr_v4`

or `Standard_ND96isr_H100_v5`

VM size on AKS. Also on [A10 SKU](/en-us/azure/virtual-machines/sizes/gpu-accelerated/nvadsa10v5-series) for GRID Driver License checks.

### Does NPD monitor the health of multi-instance GPU (MIG) node pools?

Yes, NPD health monitoring is supported on [MIG-enabled AKS node pools](gpu-multi-instance).

## Next steps

- Provision GPUs on
[Linux](use-nvidia-gpu)or[Windows](use-windows-gpu)node pools in your AKS cluster. - Learn more about the
[types of node conditions and events](node-problem-detector)set by NPD on AKS. [Monitor general GPU metrics](monitor-gpu-metrics)using a self-managed metrics exporter.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-extensions -->

# Deploy and manage cluster extensions for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Cluster extensions provide an Azure Resource Manager driven experience for installation and lifecycle management of services like Azure Machine Learning or Kubernetes applications on an AKS cluster. This feature enables:

- Azure Resource Manager-based deployment of extensions, including at-scale deployments across AKS clusters.
- Lifecycle management of the extension (Update, Delete) from Azure Resource Manager.

## Categories of cluster extensions

There are two categories of cluster extensions, *Core* and *Standard* that can be deployed onto AKS clusters.

### Core extensions

Core Kubernetes extensions have broader region availability, a more integrated AKS experience, and release alignment to AKS version releases. Azure Backup is a core extension.

#### AKS native experience

Core extensions can be managed using `az aks`

CLI command.

```
az aks extension create \
--name <core extension name> \
--extension-type <type> \
--cluster-name <name> \
--resource-group <group>
```


For more information about the commands, see [ az aks](/en-us/cli/azure/aks).

#### Release policy

Minor and major upgrades of core extensions occur alongside AKS minor and major version updates to avoid introducing breaking changes and provide better reliability.

### Standard extensions

For information about the other cluster extensions, see the table in [Currently available extensions](cluster-extensions#currently-available-extensions) and the [Kubernetes apps](deploy-marketplace) deployed via Azure Marketplace are of the Standard Extension type.

Standard extensions can be managed using the `az k8s-extension`

CLI command. For more information, see [Deploy and manage cluster extensions by using Azure CLI](deploy-extensions-az-cli).

```
az k8s-extension create \
--name <standard extension name> \
--extension-type <extension-type> \
--scope cluster \
--cluster-name <clusterName> \
--resource-group <resourceGroupName> \
--cluster-type managedClusters
```


## Cluster extension requirements

The cluster extensions platform is supported in all regions where AKS is deployed, except Qatar Central and US air gapped clouds. Although the platform is available in all regions, check the region availability for individual extensions.

Important

Ensure that your AKS cluster is created with a managed identity, as cluster extensions don't work with service principal-based clusters.

For new clusters created with `az aks create`

, managed identity is configured by default. For existing service principal-based clusters that need to be switched over to managed identity, it can be enabled by running `az aks update`

with the `--enable-managed-identity`

flag. For more information, see [Use managed identity](use-managed-identity).

Note

If you enabled [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) on your AKS cluster or are considering implementing it,
we recommend you first review [Workload identity overview](workload-identity-overview) to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.
The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated as of October 24, 2022.

## Currently available extensions

| Extension | Description |
|---|---|
|

`Dapr`

is a portable, event-driven runtime that makes it easy for any developer to build resilient, stateless, and stateful applications that run on cloud and edge.[Azure App Configuration](azure-app-configuration-quickstart)[Azure Machine Learning](/en-us/azure/machine-learning/how-to-attach-kubernetes-anywhere)[Flux (GitOps)](/en-us/azure/azure-arc/kubernetes/conceptual-gitops-flux2)[supported versions of Flux (GitOps)](/en-us/azure/azure-arc/kubernetes/extensions-release#flux-gitops)and[Tutorial: Deploy applications using GitOps with Flux v2](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2).[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)[Azure Backup for AKS](/en-us/azure/backup/azure-kubernetes-service-backup-overview)You can also [select and deploy Kubernetes applications available through Marketplace](deploy-marketplace).

Note

Cluster extensions provide a platform for different extensions to be installed and managed on an AKS cluster. If you're facing issues while using any of these extensions, open a support ticket with the respective service.

## Next steps

- Learn how to
[deploy cluster extensions by using Azure CLI](deploy-extensions-az-cli). - Read about
[cluster extensions](/en-us/azure/azure-arc/kubernetes/conceptual-extensions).
