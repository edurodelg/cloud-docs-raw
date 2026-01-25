---
merged_at: 2026-01-25T12:06:27.827454
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: image-cleaner.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/image-cleaner -->

# Use Image Cleaner to clean up vulnerable stale images on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

It's common to use pipelines to build and deploy images on Azure Kubernetes Service (AKS) clusters. While great for image creation, this process often doesn't account for the stale images left behind and can lead to image bloat on cluster nodes. These images might contain vulnerabilities, which might create security issues. To remove security risks in your clusters, you can clean these unreferenced images. Manually cleaning images can be time intensive. Image Cleaner performs automatic image identification and removal, which mitigates the risk of stale images and reduces the time required to clean them up.

Note

Image Cleaner is a feature based on [Eraser](https://eraser-dev.github.io/eraser).
On an AKS cluster, the feature name and property name is `Image Cleaner`

, while the relevant Image Cleaner pods' names contain `Eraser`

.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.49.0 or later. Run
`az --version`

to find your version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

Image Cleaner doesn't yet support Windows node pools or AKS virtual nodes.

## How Image Cleaner works

After you enable Image Cleaner, there will be a controller manager pod named `eraser-controller-manager`

deployed to your cluster.


With Image Cleaner, you can choose between manual and automatic mode and the following configuration options:

## Configuration options

| Name | Description | Required |
|---|---|---|
`--enable-image-cleaner` |
Enable the Image Cleaner feature for an AKS cluster | Yes, unless disable is specified |
`--disable-image-cleaner` |
Disable the Image Cleaner feature for an AKS cluster | Yes, unless enable is specified |
`--image-cleaner-interval-hours` |
This parameter determines the interval time (in hours) Image Cleaner uses to run. The default value for Azure CLI is one week, the minimum value is 24 hours and the maximum is three months. | Not required for Azure CLI, required for ARM template or other clients |

### Automatic mode

Once `eraser-controller-manager`

is deployed, the following steps will be taken automatically:

- It immediately starts the cleanup process and creates
`eraser-aks-xxxxx`

worker pods for each node. - There are three containers in each worker pod:
- A
**collector**, which collects unused images. - A
**trivy-scanner**, which leverages[trivy](https://github.com/aquasecurity/trivy)to scan image vulnerabilities. - A
**remover**, which removes unused images with vulnerabilities.

- A
- After the cleanup process completes, the worker pod is deleted and the next scheduled cleanup happens according to the
`--image-cleaner-interval-hours`

you define.

### Manual mode

You can manually trigger the cleanup by defining a CRD object,`ImageList`

. This triggers the `eraser-contoller-manager`

to create `eraser-aks-xxxxx`

worker pods for each node and complete the manual removal process.

Note

After disabling Image Cleaner, the old configuration still exists. This means if you enable the feature again without explicitly passing configuration, the existing value is used instead of the default.

## Enable Image Cleaner on your AKS cluster

### Enable Image Cleaner on a new cluster

Enable Image Cleaner on a new AKS cluster using the

command with the`az aks create`

`--enable-image-cleaner`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner \ --generate-ssh-keys`


### Enable Image Cleaner on an existing cluster

Enable Image Cleaner on an existing AKS cluster using the

command.`az aks update`

`az aks update \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner`


### Update the Image Cleaner interval on a new or existing cluster

Update the Image Cleaner interval on a new or existing AKS cluster using the

`--image-cleaner-interval-hours`

parameter.`# Create a new cluster with specifying the interval az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner \ --image-cleaner-interval-hours 48 \ --generate-ssh-keys # Update the interval on an existing cluster az aks update \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner \ --image-cleaner-interval-hours 48`


## Manually remove images using Image Cleaner

Important

The `name`

must be set to `imagelist`

.

Manually remove an image using the following

`kubectl apply`

command. This example removes the`docker.io/library/alpine:3.7.3`

image if it's unused.`cat <<EOF | kubectl apply -f - apiVersion: eraser.sh/v1 kind: ImageList metadata: name: imagelist spec: images: - docker.io/library/alpine:3.7.3 EOF`


The manual cleanup is a one-time operation and is only triggered when a new `imagelist`

is created or changes are made to the existing `imagelist`

. After the image is deleted, the `imagelist`

won't be deleted automatically.

If you need to trigger another manual cleanup, you have to create a new `imagelist`

or make changes to an existing one. If you want to remove the same image again, you need to create a new `imagelist`

.

### Delete an existing ImageList and create a new one

Delete the old

`imagelist`

using the`kubectl delete`

command.`kubectl delete ImageList imagelist`

Create a new

`imagelist`

with the same image name. The following example uses the same image as the[previous example](#manually-remove-images-using-image-cleaner).`cat <<EOF | kubectl apply -f - apiVersion: eraser.sh/v1 kind: ImageList metadata: name: imagelist spec: images: - docker.io/library/alpine:3.7.3 EOF`


### Modify an existing ImageList

Modify the existing

`imagelist`

using the`kubectl edit`

command.`kubectl edit ImageList imagelist # Add a new image to the list apiVersion: eraser.sh/v1 kind: ImageList metadata: name: imagelist spec: images: docker.io/library/python:alpine3.18`


When using manual mode, the `eraser-aks-xxxxx`

pod deletes within 10 minutes after work completion.

## Image exclusion list

Images specified in the exclusion list aren't removed from the cluster. Image Cleaner supports system and user-defined exclusion lists. It's not supported to edit the system exclusion list.

### Check the system exclusion list

Check the system exclusion list using the following

`kubectl get`

command.`kubectl get -n kube-system configmap eraser-system-exclusion -o yaml`


### Create a user-defined exclusion list

Create a sample JSON file to contain excluded images.

`cat > sample.json <<EOF {"excluded": ["excluded-image-name"]} EOF`

Create a

`configmap`

using the sample JSON file using the following`kubectl create`

and`kubectl label`

command.`kubectl create configmap excluded --from-file=sample.json --namespace=kube-system kubectl label configmap excluded eraser.sh/exclude.list=true -n kube-system`


## Disable Image Cleaner

Disable Image Cleaner on your cluster using the

command with the`az aks update`

`--disable-image-cleaner`

parameter.`az aks update \ --resource-group myResourceGroup \ --name myManagedCluster \ --disable-image-cleaner`


## FAQ

### How can I check which version Image Cleaner is using?

```
kubectl describe configmap -n kube-system eraser-manager-config | grep tag -C 3
```


### Does Image Cleaner support other vulnerability scanners besides trivy-scanner?

No.

### Can I specify vulnerability levels for images to clean?

No. The default settings for vulnerability levels include:

`LOW`

,`MEDIUM`

,`HIGH`

, and`CRITICAL`


You can't customize the default settings.

### How to review images were cleaned up by Image Cleaner?

Image logs are stored in the `eraser-aks-xxxxx`

worker pod. When `eraser-aks-xxxxx`

is alive, you can run the following commands to view deletion logs:

```
kubectl logs -n kube-system <worker-pod-name> -c collector
kubectl logs -n kube-system <worker-pod-name> -c trivy-scanner
kubectl logs -n kube-system <worker-pod-name> -c remover
```


The `eraser-aks-xxxxx`

pod deletes within 10 minutes after work completion. You can follow these steps to enable the [Azure Monitor add-on](monitor-aks) and use the Container Insights pod log table. After that, historical logs will be stored and you can review them even `eraser-aks-xxxxx`

is deleted.

Ensure Azure Monitoring is enabled on your cluster. For detailed steps, see

[Enable Container Insights on AKS clusters](/en-us/azure/azure-monitor/containers/container-insights-enable-aks#existing-aks-cluster).Logs for the containers running in

`kube-system`

namespace are not collected by default. Remove the`kube-system`

namespace from`exclude_namespaces`

in the configmap and apply the config map to enable collection of these logs. See[Configure Container insights data collection](/en-us/azure/azure-monitor/containers/container-insights-data-collection-configure#configure-data-collection-using-configmap)for details.Get the Log Analytics resource ID using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myManagedCluster`

After a few minutes, the command returns JSON-formatted information about the solution, including the workspace resource ID:

`"addonProfiles": { "omsagent": { "config": { "logAnalyticsWorkspaceResourceID": "/subscriptions/<WorkspaceSubscription>/resourceGroups/<DefaultWorkspaceRG>/providers/Microsoft.OperationalInsights/workspaces/<defaultWorkspaceName>" }, "enabled": true } }`

In the Azure portal, search for the workspace resource ID, then select

**Logs**.Copy one of the following queries and paste into the query window.

Use the following query if your cluster is using the

[ContainerLogV2 schema](/en-us/azure/azure-monitor/containers/container-insights-logs-schema). If you're still using`ContainerLog`

, you should upgrade to ContainerlogV2.`ContainerLogV2 | where PodName startswith "eraser-aks-" and PodNamespace == "kube-system" | project TimeGenerated, PodName, LogMessage, LogSource`

If you want continue to use

`ContainerLog`

, use the following query instead:`let startTimestamp = ago(1h); KubePodInventory | where TimeGenerated > startTimestamp | project ContainerID, PodName=Name, Namespace | where PodName startswith "eraser-aks-" and Namespace == "kube-system" | distinct ContainerID, PodName | join ( ContainerLog | where TimeGenerated > startTimestamp ) on ContainerID // at this point before the next pipe, columns from both tables are available to be "projected". Due to both // tables having a "Name" column, we assign an alias as PodName to one column which we actually want | project TimeGenerated, PodName, LogEntry, LogEntrySource | summarize by TimeGenerated, LogEntry | order by TimeGenerated desc`


Select

**Run**. Any deleted image logs appear in the**Results**area.


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
