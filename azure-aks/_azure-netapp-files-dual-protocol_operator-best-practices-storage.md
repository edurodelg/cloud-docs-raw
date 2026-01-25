---
merged_at: 2026-01-25T12:25:33.948884
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-netapp-files-dual-protocol.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-dual-protocol -->

# Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service

After you [configure Azure NetApp Files for Azure Kubernetes Service](azure-netapp-files), you can provision Azure NetApp Files volumes for Azure Kubernetes Service.

Azure NetApp Files supports volumes using [NFS](azure-netapp-files-nfs) (NFSv3 or NFSv4.1), [SMB](azure-netapp-files-smb), and dual-protocol (NFSv3 and SMB, or NFSv4.1 and SMB).

This article shows you how to statically provisioning volumes for dual-protocol access using NFS or SMB.

## Before you begin

## Provision a dual-protocol volume in Azure Kubernetes Service

This section describes how to expose an Azure NetApp Files dual-protocol volume statically to Kubernetes. Instructions are provided for both SMB and NFS protocols. You can expose the same volume via SMB to Windows worker nodes and via NFS to Linux worker nodes.

### Create the persistent volume for NFS

Define variables for later usage. Replace *myresourcegroup*, *myaccountname*, *mypool1*, *myvolname* with an appropriate value from your dual-protocol volume.

```
RESOURCE_GROUP="myresourcegroup"
ANF_ACCOUNT_NAME="myaccountname"
POOL_NAME="mypool1"
VOLUME_NAME="myvolname"
```


List the details of your volume using the `az netappfiles volume show`

command.

```
az netappfiles volume show \
--resource-group $RESOURCE_GROUP \
--account-name $ANF_ACCOUNT_NAME \
--pool-name $POOL_NAME \
--volume-name $VOLUME_NAME -o JSON
```


The following output is an example of the above command executed with real values.

```
{
...
"creationToken": "myfilepath2",
...
"mountTargets": [
{
...
"ipAddress": "10.0.0.4",
...
}
],
...
}
```


Create a file named `pv-nfs.yaml`

and copy in the following YAML. Make sure the server matches the output IP address from the previous step, and the path matches the output from `creationToken`

above. The capacity must also match the volume size from Step 2.

```
apiVersion: v1
kind: PersistentVolume
metadata:
name: pv-nfs
spec:
capacity:
storage: 100Gi
accessModes:
- ReadWriteMany
mountOptions:
- vers=3
nfs:
server: 10.0.0.4
path: /myfilepath2
```


Create the persistent volume using the `kubectl apply`

command:

```
kubectl apply -f pv-nfs.yaml
```


Verify the status of the persistent volume is *Available* by using the `kubectl describe`

command:

```
kubectl describe pv pv-nfs
```


### Create a persistent volume claim for NFS

Create a file named `pvc-nfs.yaml`

and copy in the following YAML. This manifest creates a PVC named `pvc-nfs`

for 100Gi storage and `ReadWriteMany`

access mode, matching the PV you created.

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: pvc-nfs
spec:
accessModes:
- ReadWriteMany
storageClassName: ""
resources:
requests:
storage: 100Gi
```


Create the persistent volume claim using the `kubectl apply`

command:

```
kubectl apply -f pvc-nfs.yaml
```


Verify the *Status* of the persistent volume claim is *Bound* by using the `kubectl describe`

command:

```
kubectl describe pvc pvc-nfs
```


### Mount within a pod using NFS

Create a file named `nginx-nfs.yaml`

and copy in the following YAML. This manifest defines a `nginx`

pod that uses the persistent volume claim.

```
kind: Pod
apiVersion: v1
metadata:
name: nginx-nfs
spec:
containers:
- image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
name: nginx-nfs
command:
- "/bin/sh"
- "-c"
- while true; do echo $(date) >> /mnt/azure/outfile; sleep 1; done
volumeMounts:
- name: disk01
mountPath: /mnt/azure
volumes:
- name: disk01
persistentVolumeClaim:
claimName: pvc-nfs
```


Create the pod using the `kubectl apply`

[kubectl-apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command:

```
kubectl apply -f nginx-nfs.yaml
```


Verify the pod is *Running* by using the `kubectl apply`

command:

```
kubectl describe pod nginx-nfs
```


Verify your volume has been mounted on the pod by using `kubectl exec`

to connect to the pod, and then use `df -h`

to check if the volume is mounted.

```
kubectl exec -it nginx-nfs -- sh
```


```
/ # df -h
Filesystem Size Used Avail Use% Mounted on
...
10.0.0.4:/myfilepath2 100T 384K 100T 1% /mnt/azure
...
```


### Create a secret with the domain credentials

- Create a secret on your AKS cluster to access the AD server using the
`kubectl create secret`

command. This secret will be used by the Kubernetes persistent volume to access the Azure NetApp Files SMB volume. Use the following command to create the secret, replacing `USERNAME`

with your username, `PASSWORD`

with your password, and `DOMAIN_NAME`

with your Active Directory domain name.

```
kubectl create secret generic smbcreds --from-literal=username=USERNAME --from-literal=password="PASSWORD" --from-literal=domain='DOMAIN_NAME'
```


- To verify the secret has been created, run the
`kubectl get`

command.

```
kubectl get secret
```


```
NAME TYPE DATA AGE
smbcreds Opaque 2 20h
```


### Install an SMB CSI driver

You must install a Container Storage Interface (CSI) driver to create a Kubernetes SMB `PersistentVolume`

.

Install the SMB CSI driver on your cluster using helm. Be sure to set the `windows.enabled`

option to `true`

:

```
helm repo add csi-driver-smb https://raw.githubusercontent.com/kubernetes-csi/csi-driver-smb/master/charts
helm install csi-driver-smb csi-driver-smb/csi-driver-smb --namespace kube-system --version v1.10.0 –-set windows.enabled=true
```


For other methods of installing the SMB CSI Driver, see [Install SMB CSI driver master version on a Kubernetes cluster](https://github.com/kubernetes-csi/csi-driver-smb/blob/master/docs/install-csi-driver-master.md).

Verify the `csi-smb`

controller pod is running and each worker node has a pod running using the `kubectl get pods`

command:

```
kubectl get pods -n kube-system | grep csi-smb
```


```
csi-smb-controller-68df7b4758-xf2m9 3/3 Running 0 3m46s
csi-smb-node-s6clj 3/3 Running 0 3m47s
csi-smb-node-win-tfxvk 3/3 Running 0 3m47s
```


### Create the persistent volume for SMB

Define variables for later usage. Replace *myresourcegroup*, *myaccountname*, *mypool1*, *myvolname* with an appropriate value from your dual-protocol volume.

```
RESOURCE_GROUP="myresourcegroup"
ANF_ACCOUNT_NAME="myaccountname"
POOL_NAME="mypool1"
VOLUME_NAME="myvolname"
```


List the details of your volume using `az netappfiles volume show`

command.

```
az netappfiles volume show \
--resource-group $RESOURCE_GROUP \
--account-name $ANF_ACCOUNT_NAME \
--pool-name $POOL_NAME \
--volume-name "$VOLUME_NAME -o JSON
```


The following output is an example of the above command executed with real values.

```
{
...
"creationToken": "myvolname",
...
"mountTargets": [
{
...
"
"smbServerFqdn": "ANF-1be3.contoso.com",
...
}
],
...
}
```


Create a file named `pv-smb.yaml`

and copy in the following YAML. If necessary, replace `myvolname`

with the `creationToken`

and replace `ANF-1be3.contoso.com\myvolname`

with the value of `smbServerFqdn`

from the previous step. Be sure to include your AD credentials secret along with the namespace where it's located that you created in a prior step.

```
apiVersion: v1
kind: PersistentVolume
metadata:
name: anf-pv-smb
spec:
storageClassName: ""
capacity:
storage: 100Gi
accessModes:
- ReadWriteMany
persistentVolumeReclaimPolicy: Retain
mountOptions:
- dir_mode=0777
- file_mode=0777
- vers=3.0
csi:
driver: smb.csi.k8s.io
readOnly: false
volumeHandle: myvolname # make sure it's a unique name in the cluster
volumeAttributes:
source: \\ANF-1be3.contoso.com\myvolname
nodeStageSecretRef:
name: smbcreds
namespace: default
```


Create the persistent volume using the `kubectl apply`

command:

```
kubectl apply -f pv-smb.yaml
```


Verify the status of the persistent volume is *Available* using the `kubectl describe`

command:

```
kubectl describe pv anf-pv-smb
```


### Create a persistent volume claim for SMB

Create a file name `pvc-smb.yaml`

and copy in the following YAML.

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: anf-pvc-smb
spec:
accessModes:
- ReadWriteMany
volumeName: anf-pv-smb
storageClassName: ""
resources:
requests:
storage: 100Gi
```


Create the persistent volume claim using the `kubectl apply`

command:

```
kubectl apply -f pvc-smb.yaml
```


Verify the status of the persistent volume claim is *Bound* by using the `kubectl describe`

command:

```
kubectl describe pvc anf-pvc-smb
```


### Mount within a pod using SMB

Create a file named `iis-smb.yaml`

and copy in the following YAML. This file will be used to create an Internet Information Services pod to mount the volume to path `/inetpub/wwwroot`

.

```
apiVersion: v1
kind: Pod
metadata:
name: iis-pod
labels:
app: web
spec:
nodeSelector:
"kubernetes.io/os": windows
volumes:
- name: smb
persistentVolumeClaim:
claimName: anf-pvc-smb
containers:
- name: web
image: mcr.microsoft.com/windows/servercore/iis:windowsservercore
resources:
limits:
cpu: 1
memory: 800M
ports:
- containerPort: 80
volumeMounts:
- name: smb
mountPath: "/inetpub/wwwroot"
readOnly: false
```


Create the pod using the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command:

```
kubectl apply -f iis-smb.yaml
```


Verify the pod is *Running* and `/inetpub/wwwroot`

is mounted from SMB by using the `kubectl describe`

command:

```
kubectl describe pod iis-pod
```


The output of the command resembles the following example:

```
Name: iis-pod
Namespace: default
Priority: 0
Node: akswin000001/10.225.5.246
Start Time: Fri, 05 May 2023 09:34:41 -0400
Labels: app=web
Annotations: <none>
Status: Running
IP: 10.225.5.248
IPs:
IP: 10.225.5.248
Containers:
web:
Container ID: containerd://39a1659b6a2b6db298df630237b2b7d959d1b1722edc81ce9b1bc7f06237850c
Image: mcr.microsoft.com/windows/servercore/iis:windowsservercore
Image ID: mcr.microsoft.com/windows/servercore/iis@sha256:0f0114d0f6c6ee569e1494953efdecb76465998df5eba951dc760ac5812c7409
Port: 80/TCP
Host Port: 0/TCP
State: Running
Started: Fri, 05 May 2023 09:34:55 -0400
Ready: True
Restart Count: 0
Limits:
cpu: 1
memory: 800M
Requests:
cpu: 1
memory: 800M
Environment: <none>
Mounts:
/inetpub/wwwroot from smb (rw)
/var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-mbnv8 (ro)
...
```


Verify your volume has been mounted on the pod by using the [kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec) command to connect to the pod. Then use the `dir`

command in the correct directory to check if the volume is mounted and the size matches the size of the volume you provisioned.

```
kubectl exec -it iis-pod –- cmd.exe
```


The output of the command resembles the following example:

```
Microsoft Windows [Version 10.0.20348.1668]
(c) Microsoft Corporation. All rights reserved.
C:\>cd /inetpub/wwwroot
C:\inetpub\wwwroot>dir
Volume in drive C has no label.
Volume Serial Number is 86BB-AA55
Directory of C:\inetpub\wwwroot
05/04/2023 08:15 PM <DIR> .
05/04/2023 08:15 PM <DIR> ..
0 File(s) 0 bytes
2 Dir(s) 107,373,838,336 bytes free
```


## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:


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
