---
merged_at: 2026-02-02T15:56:31.840124
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/image-cleaner -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-dual-protocol -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-custom-vnet -->

# Create a node auto-provisioning (NAP) cluster in a custom virtual network in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create a virtual network (VNet) and subnet, create a managed identity with permissions to access the VNet, and create an Azure Kubernetes Service (AKS) cluster in your custom VNet with node auto-provisioning (NAP) enabled.

## Prerequisites

- An Azure subscription. If you don't have one, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version
`2.76.0`

or later. To find the version, run`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/get-started-with-azure-cli). - Read the
[Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning)article, which details[how NAP works](node-auto-provisioning#how-does-node-auto-provisioning-work). - Read the
[Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning-networking).

## Limitations

- When creating a NAP cluster in a custom virtual network (VNet), you must use a
[Standard Load Balancer](load-balancer-standard). The Basic Load Balancer isn't supported. - To review other limitations and unsupported features for NAP, see the
[Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning#limitations-and-unsupported-features)article.

## Create a virtual network and subnet

Important

When using a custom VNet with NAP keep the following information in mind:

- You must create and delegate an API server subnet to
`Microsoft.ContainerService/managedClusters`

, which grants the AKS service permissions to inject the API server pods and internal load balancer into that subnet. You can't use the subnet for any other workloads, but you can use it for multiple AKS clusters located in the same VNet. The minimum supported API server subnet size is*/28*. - All traffic within the VNet is allowed by default. However, if you added network security group (NSG) rules to restrict traffic between different subnets, you need to ensure you configure the proper permissions. For more information, see the
[Network security group documentation](/en-us/azure/virtual-network/network-security-groups-overview).

Create a VNet using the

command.`az network vnet create`

`az network vnet create \ --name $VNET_NAME \ --resource-group $RG_NAME \ --location $LOCATION \ --address-prefixes 172.19.0.0/16`

Create a subnet using the

command and delegate it to`az network vnet subnet create`

`Microsoft.ContainerService/managedClusters`

.`az network vnet subnet create \ --resource-group $RG_NAME \ --vnet-name $VNET_NAME \ --name $SUBNET_NAME \ --delegations Microsoft.ContainerService/managedClusters \ --address-prefixes 172.19.0.0/28`


## Create a managed identity and give it permissions to access the VNet

Create a managed identity using the

command.`az identity create`

`az identity create \ --resource-group $RG_NAME \ --name $IDENTITY_NAME \ --location $LOCATION`

Get the principal ID of the managed identity and set it to an environment variable using the [

`az identity show`

][az-identity-show] command.`IDENTITY_PRINCIPAL_ID=$(az identity show --resource-group $RG_NAME --name $IDENTITY_NAME --query principalId -o tsv)`

Assign the

*Network Contributor*role to the managed identity using thecommand.`az role assignment create`

`az role assignment create \ --scope "/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$RG_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME" \ --role "Network Contributor" \ --assignee $IDENTITY_PRINCIPAL_ID`


## Create an AKS cluster with node auto-provisioning (NAP) in a custom VNet

Create an AKS cluster with NAP enabled in your custom VNet using the

command. Make sure to set the`az aks create`

`--node-provisioning-mode`

flag to`Auto`

to enable NAP.The following command also sets the

`--network-plugin`

to`azure`

,`--network-plugin-mode`

to`overlay`

, and`--network-dataplane`

to`cilium`

. For more information on networking configurations supported with NAP, see[Configure networking for node auto-provisioning on AKS](node-autoprovision-networking).`az aks create \ --name $CLUSTER_NAME \ --resource-group $RG_NAME \ --location $LOCATION \ --assign-identity "/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$RG_NAME/providers/Microsoft.ManagedIdentity/userAssignedIdentities/$IDENTITY_NAME" \ --network-dataplane cilium \ --network-plugin azure \ --network-plugin-mode overlay \ --vnet-subnet-id "/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$RG_NAME/providers/Microsoft.Network/virtualNetworks/$CUSTOM_VNET_NAME/subnets/$SUBNET_NAME" \ --node-provisioning-mode Auto`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials \ --resource-group $RG_NAME \ --name $CLUSTER_NAME`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-resource-group-lockdown -->

# Deploy a fully managed resource group using node resource group lockdown in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS deploys infrastructure into your subscription for connecting to and running your applications. Changes made directly to resources in the [node resource group](concepts-clusters-workloads#node-resource-group) can affect cluster operations or cause future issues. For example, scaling, storage, or network configurations should be made through the Kubernetes API and not directly on these resources.

To prevent changes from being made to the node resource group, you can apply a deny assignment and block users from modifying resources created as part of the AKS cluster.

## Before you begin

Before you begin, you need the following resources installed and configured:

- The Azure CLI version 2.44.0 or later. Run
`az --version`

to find the current version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an AKS cluster with node resource group lockdown

Create a cluster with node resource group lockdown using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with the

`--nrg-lockdown-restriction-level`

flag set to `ReadOnly`

. This configuration allows you to view the resources but not modify them.```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--nrg-lockdown-restriction-level ReadOnly \
--generate-ssh-keys
```


## Update an existing cluster with node resource group lockdown

Update an existing cluster with node resource group lockdown using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--nrg-lockdown-restriction-level`

flag set to `ReadOnly`

. This configuration allows you to view the resources but not modify them.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --nrg-lockdown-restriction-level ReadOnly
```


## Remove node resource group lockdown from a cluster

Remove node resource group lockdown from an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--nrg-restriction-level`

flag set to `Unrestricted`

. This configuration allows you to view and modify the resources.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --nrg-lockdown-restriction-level Unrestricted
```


## Next steps

To learn more about the node resource group in AKS, see [Node resource group](concepts-clusters-workloads#node-resource-group).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-pool-unique-subnet -->

# Create node pools with unique subnets in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Certain workloads might require splitting cluster nodes into separate pools for logical isolation. Separate subnets dedicated to each node pool in the cluster can help support this isolation, which can address requirements such as having noncontiguous virtual network address space to split across node pools.

In this article, you learn how to create node pools with unique subnets in Azure Kubernetes Service (AKS).

## Prerequisites

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.35.0 or later. Run`az version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).- An existing AKS cluster with a system node pool. If you need to create one, see
[Create an AKS cluster with a single node pool](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli).

## Limitations

- All subnets assigned to node pools must belong to the same virtual network (VNet).
- System pods must have access to all nodes and pods in the cluster to provide critical functionality, such as DNS resolution and tunneling kubectl logs/exec/port-forward proxy.
- If you expand your VNet after creating the cluster, you must update your cluster before adding a subnet outside the original CIDR block. While AKS errors out on the agent pool add, the
`aks-preview`

Azure CLI extension (version 0.5.66 and higher) now supports running`az aks update`

command with only the required`--resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

arguments. This command performs an update operation without making any changes, which can recover a cluster stuck in a failed state. - In clusters with Kubernetes version less than 1.23.3, kube-proxy SNATs traffic from new subnets, which can cause Azure Network Policy to drop the packets.
- Windows nodes SNAT traffic to the new subnets until the node pool is reimaged.
- Internal load balancers default to one of the node pool subnets.

## Add a node pool with a unique subnet

Add a node pool with a unique subnet into your existing AKS cluster using the

command and the`az aks nodepool add`

`--vnet-subnet-id`

parameter specified.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 3 \ --vnet-subnet-id $SUBNET_RESOURCE_ID`


## Next steps

For more information about node pools in AKS, see [Manage node pools for a cluster in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-storage -->

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/draft -->

# Draft for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Draft](https://github.com/Azure/draft) is an open-source project that streamlines Kubernetes development by taking a non-containerized application and generating the Dockerfiles, Kubernetes manifests, Helm charts, Kustomize configurations, and other artifacts associated with a containerized application. Draft can also create a GitHub Action workflow file to quickly build and deploy applications onto any Kubernetes cluster.

## How it works

Draft has the following commands to help ease your development on Kubernetes:

`draft create`

: Creates the Dockerfile and the proper manifest files.`draft setup-gh`

: Sets up your GitHub OIDC.`draft generate-workflow`

: Generates the GitHub Action workflow file for deployment onto your cluster.`draft up`

: Sets up your GitHub OIDC and generates a GitHub Action workflow file, combining the previous two commands.

## Prerequisites

- If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Install the latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli-windows)and the*aks-preview*extension. - If you don't have one already, you need to create an
[AKS cluster](tutorial-kubernetes-deploy-cluster)and an Azure Container Registry instance.

### Install the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update the extension to make sure you have the latest version using the

command.`az extension update`

`az extension update --name aks-preview`


## Create artifacts using `draft create`


You can use `draft create`

to create Dockerfiles, Helm charts, Kubernetes manifests, or Kustomize files needed to deploy your application onto an AKS cluster.

Create an artifact using the

command.`az aks draft create`

`az aks draft create`

You can also run the command on a specific directory using the

`--destination`

flag, as shown in the following example:`az aks draft create --destination /Workspaces/ContosoAir`


## Set up GitHub OIDC using `draft setup-gh`


To use Draft, you have to register your application with GitHub using `draft setup-gh`

. This step only needs to be done once per repository.

Register your application with GitHub using the

command.`az aks draft setup-gh`

`az aks draft setup-gh`


## Generate a GitHub Action workflow file for deployment using `draft generate-workflow`


After you create your artifacts and set up GitHub OIDC, you can use `draft generate-workflow`

to generate a GitHub Action workflow file, creating an action that deploys your application onto your AKS cluster. Once your workflow file is generated, you must commit it into your repository in order to initiate the GitHub Action.

Generate a GitHub Action workflow file using the

command.`az aks draft generate-workflow`

`az aks draft generate-workflow`

You can also run the command on a specific directory using the

`--destination`

flag, as shown in the following example:`az aks draft generate-workflow --destination /Workspaces/ContosoAir`


## Set up GitHub OpenID Connect (OIDC) and generate a GitHub Action workflow file using `draft up`


`draft up`

is a single command to accomplish GitHub OIDC setup and generate a GitHub Action workflow file for deployment. It effectively combines the `draft setup-gh`

and `draft generate-workflow`

commands, meaning it's most commonly used when getting started in a new repository for the first time, and only needs to be run once. Subsequent updates to the GitHub Action workflow file can be made using `draft generate-workflow`

.

Set up GitHub OIDC and generate a GitHub Action workflow file using the

command.`az aks draft up`

`az aks draft up`

You can also run the command on a specific directory using the

`--destination`

flag, as shown in the following example:`az aks draft up --destination /Workspaces/ContosoAir`


## Use Application Routing with Draft to make your application accessible over the internet

Application Routing][app-routing](app-routing) is the easiest way to get your web application up and running in Kubernetes securely. Application Routing removes the complexity of ingress controllers and certificate and DNS management, and it offers configuration for enterprises looking to bring their own. Application Routing offers a managed ingress controller based on nginx that you can use without restrictions and integrates out of the box with Open Service Mesh to secure intra-cluster communications.

Set up Draft with Application Routing using the

and pass in the DNS name and Azure Key Vault-stored certificate when prompted.`az aks draft update`

`az aks draft update`

You can also run the command on a specific directory using the

`--destination`

flag, as shown in the following example:`az aks draft update --destination /Workspaces/ContosoAir`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-extension-kaito -->

# Deploy and test inference models with the AI toolchain operator (KAITO) in Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use the AI toolchain operator (KAITO) add-on in the Azure Kubernetes Service (AKS) extension for Visual Studio Code. KAITO automatically provisions the right-sized GPU nodes and sets up the inference server as an endpoint server to your AI model(s), allowing you to test and experiment with AI on AKS with ease.

## Prerequisites

- The Azure Kubernetes Service (AKS) extension for Visual Studio Code needs to be installed to use the KAITO experience. For more information, see
[Install the Azure Kubernetes Service (AKS) extension for Visual Studio Code](aks-extension-vs-code#installation). - The cluster that you are deploying to is a Standard Cluster
*(Kaito cannot currently be installed on Automatic clusters)*. - Verify that your Azure subscription has GPU quota for your chosen model by checking the
[KAITO model workspaces](https://github.com/kaito-project/kaito/tree/main/presets).

## Install KAITO on your cluster

- In the Kubernetes tab, under
**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Install KAITO**. - Once on the page, select
**Install KAITO**to start the KAITO installation process. - When the installation completes, you will see a
**Generate Workspace**button that redirects you to the model deployment page.

## Create a KAITO workspace

When creating a KAITO workspace, you can either deploy the default workspace CRD directly into your AKS cluster or save the CRD and customize it for your needs.

- In the Kubernetes tab, under
**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Create KAITO workspace**. - Find and select the model you want to deploy.
- Select
**Deploy default workspace CRD**or**Customize workspace CRD**. - Select
**Deploy default workspace CRD**to deploy the model. It tracks the progress of the model and notifies you once the model successfully deploys. It also notifies you if the model was already deployed unsuccessfully onto your cluster. - When the deployment completes, you see a
**View Deployed Models**button that redirects you to the deployment management page.

## Manage KAITO models

The **Manage KAITO models** page allows you to see all models deployed in your AKS cluster along with their status (*ongoing*, *successful*, or *failed*).

In the Kubernetes tab, under

**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Manage KAITO models**.From this page, you can choose to perform one of the following actions:

**Get logs**: Select**Get Logs**to access the latest logs from the KAITO workspace pods for your deployment. This action generates a new text file containing the most recent 500 lines of logs.**Delete a model**: Select**Delete Workspace**(or**Cancel**for ongoing deployments). For failed deployments, select**Redeploy Default CRD**to remove the current deployment and restart the model deployment process from scratch.**Test a model**: Select**Test**. This action brings you to a new page where you can interact with the deployed model through a chat interface.


## Test your model

In the Kubernetes tab, under

**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Manage KAITO models**.Select

**Test**. This action brings you to a new page where you can interact with the deployed model through the**Prompt**box chat interface.You can optionally adjust the parameters:

**Temperature**: Controls the randomness of the model's output. A low temperature is good for tasks needing precision, like math problems, while a high temperature is better for tasks like creative writing.**Top P**: Limits the next-word choices to a dynamic subset of the vocabulary, determined by a cumulative probability threshold.**Top K**: Limits the next-word selection to the top`K`

most probable words. Smaller`K`

values lead to more predictable outputs, while larger values increase variability.**Repetition Penalty**: Penalizes the model for repeating the same phrases, words, or sequences. This is useful for avoiding repetitive or looping outputs, especially in longer generations.**Max Length**: Defines the maximum number of tokens (words or subwords) in the generated output.


For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Delete your model inference deployment

- Once you've finished testing the model(s) and you want to free up the allocated GPU resources on your cluster, go to the Kubernetes tab, and under
**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Manage KAITO models**. - For each deployed model, select
**Delete Workspace**to clear all allocated resources created by the inference deployment.

## Product support and feedback

If you have a question or want to offer product feedback, please open an issue on the [AKS extension GitHub repository](https://github.com/Azure/vscode-aks-tools/issues/new/choose).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations for AKS](integrations).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-node-public-ips -->

# Use instance-level public IPs in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS nodes don't require their own public IP addresses for communication. However, scenarios may require nodes in a node pool to receive their own dedicated public IP addresses. A common scenario is for gaming workloads, where a console needs to make a direct connection to a cloud virtual machine to minimize hops. This scenario can be achieved on AKS by using Node Public IP.

First, create a new resource group.

```
az group create --name <resourceGroup> --location <region>
```


Create a new AKS cluster and attach a public IP for your nodes. Each of the nodes in the node pool receives a unique public IP. You can verify this by looking at the Virtual Machine Scale Set instances.

```
az aks create \
--resource-group <resourceGroup> \
--name <aksClusterName> \
--location <region> \
--enable-node-public-ip \
--generate-ssh-keys
```


For existing AKS clusters, you can also add a new node pool, and attach a public IP for your nodes.

```
az aks nodepool add --resource-group <resourceGroup> --cluster-name <aksClusterName> --name <newNodePool> --enable-node-public-ip
```


## Use a public IP prefix

There are a number of [benefits to using a public IP prefix](/en-us/azure/virtual-network/ip-services/public-ip-address-prefix). AKS supports using addresses from an existing public IP prefix for your nodes by passing the resource ID with the flag `--node-public-ip-prefix-id`

when creating a new cluster or adding a node pool.

First, create a public IP prefix using [az network public-ip prefix create](/en-us/cli/azure/network/public-ip/prefix#az-network-public-ip-prefix-create):

```
az network public-ip prefix create --length 28 --location <region> --name <publicIPPrefixName> --resource-group <resourceGroup>
```


View the output, and take note of the `id`

for the prefix:

```
{
...
"id": "/subscriptions/<subscription-id>/resourceGroups/<resourceGroup>/providers/Microsoft.Network/publicIPPrefixes/<publicIPPrefixName>",
...
}
```


Finally, when creating a new cluster or adding a new node pool, use the flag `--node-public-ip-prefix-id`

and pass in the prefix's resource ID:

```
az aks create \
--resource-group <resourceGroup> \
--name <aksClusterName> \
--location <region> \
--enable-node-public-ip \
--node-public-ip-prefix-id /subscriptions/<subscription-id>/resourceGroups/<resourceGroup>/providers/Microsoft.Network/publicIPPrefixes/<publicIPPrefixName> \
--generate-ssh-keys
```


## Locate public IPs for nodes

You can locate the public IPs for your nodes in various ways:

- Use the Azure CLI command
.`az vmss list-instance-public-ips`

- Use
[PowerShell or Bash commands](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine). - You can also view the public IPs in the Azure portal by viewing the instances in the Virtual Machine Scale Set.

Important

The [node resource group](faq) contains the nodes and their public IPs. Use the node resource group when executing commands to find the public IPs for your nodes.

```
az vmss list-instance-public-ips --resource-group <MC_region_aksClusterName_region> --name <virtualMachineScaleSetName>
```


## Use public IP tags on node public IPs

Public IP tags can be utilized on node public IPs to utilize the [Azure Routing Preference](/en-us/azure/virtual-network/ip-services/routing-preference-overview) feature.

### Requirements

- AKS version 1.29 or greater is required.

### Create a new cluster using routing preference internet

```
az aks create \
--name <aksClusterName> \
--location <region> \
--resource-group <resourceGroup> \
--enable-node-public-ip \
--node-public-ip-tags RoutingPreference=Internet \
--generate-ssh-keys
```


### Add a node pool with routing preference internet

```
az aks nodepool add --cluster-name <aksClusterName> \
--name <nodePoolName> \
--location <region> \
--resource-group <resourceGroup> \
--enable-node-public-ip \
--node-public-ip-tags RoutingPreference=Internet
```


## Allow host port connections and add node pools to application security groups

AKS nodes utilizing node public IPs that host services on their host address need to have an NSG rule added to allow the traffic. Adding the desired ports in the node pool configuration will create the appropriate allow rules in the cluster network security group.

If a network security group is in place on the subnet with a cluster using bring-your-own virtual network, an allow rule must be added to that network security group. This can be limited to the nodes in a given node pool by adding the node pool to an [application security group (ASG)](/en-us/azure/virtual-network/network-security-groups-overview#application-security-groups). A managed ASG will be created by default in the managed resource group if allowed host ports are specified. Nodes can also be added to one or more custom ASGs by specifying the resource ID of the NSG(s) in the node pool parameters.

### Host port specification format

When specifying the list of ports to allow, use a comma-separate list with entries in the format of `port/protocol`

or `startPort-endPort/protocol`

.

Examples:

- 80/tcp
- 80/tcp,443/tcp
- 53/udp,80/tcp
- 50000-60000/tcp

### Requirements

- AKS version 1.29 or greater is required.

### Create a new cluster with allowed ports and application security groups

```
az aks create \
--resource-group <resourceGroup> \
--name <aksClusterName> \
--nodepool-name <nodePoolName> \
--nodepool-allowed-host-ports 80/tcp,443/tcp,53/udp,40000-60000/tcp,40000-50000/udp\
--nodepool-asg-ids "<asgId>,<asgId>" \
--generate-ssh-keys
```


### Add a new node pool with allowed ports and application security groups

```
az aks nodepool add \
--resource-group <resourceGroup> \
--cluster-name <aksClusterName> \
--name <nodePoolName> \
--allowed-host-ports 80/tcp,443/tcp,53/udp,40000-60000/tcp,40000-50000/udp \
--asg-ids "<asgId>,<asgId>"
```


### Update the allowed ports and application security groups for a node pool

```
az aks nodepool update \
--resource-group <resourceGroup> \
--cluster-name <aksClusterName> \
--name <nodePoolName> \
--allowed-host-ports 80/tcp,443/tcp,53/udp,40000-60000/tcp,40000-50000/udp \
--asg-ids "<asgId>,<asgId>"
```


## Automatically assign host ports for pod workloads (PREVIEW)

When public IPs are configured on nodes, host ports can be utilized to allow pods to directly receive traffic without having to configure a load balancer service. This is especially useful in scenarios like gaming, where the ephemeral nature of the node IP and port is not a problem because a matchmaker service at a well-known hostname can provide the correct host and port to use at connection time. However, because only one process on a host can be listening on the same port, using applications with host ports can lead to problems with scheduling. To avoid this issue, AKS provides the ability to have the system dynamically assign an available port at scheduling time, preventing conflicts.

Warning

Pod host port traffic will be blocked by the default NSG rules in place on the cluster. This feature should be combined with allowing host ports on the node pool to allow traffic to flow.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Requirements

- AKS version 1.29 or greater is required.

### Register the 'PodHostPortAutoAssignPreview' feature flag

Register the `PodHostPortAutoAssignPreview`

feature flag by using the [az feature register](/en-us/cli/azure/feature#az-feature-register) command, as shown in the following example:

```
az feature register --namespace "Microsoft.ContainerService" --name "PodHostPortAutoAssignPreview"
```


It takes a few minutes for the status to show *Registered*. Verify the registration status by using the [az feature show](/en-us/cli/azure/feature#az-feature-show) command:

```
az feature show --namespace "Microsoft.ContainerService" --name "PodHostPortAutoAssignPreview"
```


When the status reflects *Registered*, refresh the registration of the *Microsoft.ContainerService* resource provider by using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command:

```
az provider register --namespace Microsoft.ContainerService
```


### Automatically assign a host port to a pod

Triggering host port auto assignment is done by deploying a workload without any host ports and applying the `kubernetes.azure.com/assign-hostports-for-containerports`

annotation with the list of ports that need host port assignments. The value of the annotation should be specified as a comma-separated list of entries like `port/protocol`

, where the port is an individual port number that is defined in the Pod spec and the protocol is `tcp`

or `udp`

.

Ports will be assigned from the range `40000-59999`

and will be unique across the cluster. The assigned ports will also be added to environment variables inside the pod so that the application can determine what ports were assigned. The environment variable name will be in the following format (example below): `<deployment name>_PORT_<port number>_<protocol>_HOSTPORT`

, so an example would be `mydeployment_PORT_8080_TCP_HOSTPORT: 41932`

.

Here is an example `echoserver`

deployment, showing the mapping of host ports for ports 8080 and 8443:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: echoserver-hostport
labels:
app: echoserver-hostport
spec:
replicas: 3
selector:
matchLabels:
app: echoserver-hostport
template:
metadata:
annotations:
kubernetes.azure.com/assign-hostports-for-containerports: 8080/tcp,8443/tcp
labels:
app: echoserver-hostport
spec:
nodeSelector:
kubernetes.io/os: linux
containers:
- name: echoserver-hostport
image: k8s.gcr.io/echoserver:1.10
ports:
- name: http
containerPort: 8080
protocol: TCP
- name: https
containerPort: 8443
protocol: TCP
```


When the deployment is applied, the `hostPort`

entries will be in the YAML of the individual pods:

```
$ kubectl describe pod echoserver-hostport-75dc8d8855-4gjfc
<cut for brevity>
Containers:
echoserver-hostport:
Container ID: containerd://d0b75198afe0612091f412ee7cf7473f26c80660143a96b459b3e699ebaee54c
Image: k8s.gcr.io/echoserver:1.10
Image ID: k8s.gcr.io/echoserver@sha256:cb5c1bddd1b5665e1867a7fa1b5fa843a47ee433bbb75d4293888b71def53229 Ports: 8080/TCP, 8443/TCP
Host Ports: 46645/TCP, 49482/TCP
State: Running
Started: Thu, 12 Jan 2023 18:02:50 +0000
Ready: True
Restart Count: 0
Environment:
echoserver-hostport_PORT_8443_TCP_HOSTPORT: 49482
echoserver-hostport_PORT_8080_TCP_HOSTPORT: 46645
```


## Next steps

Learn about

[using multiple node pools in AKS](create-node-pools).Learn about

[using standard load balancers in AKS](load-balancer-standard)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-wireguard -->

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

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dns-concepts -->

# DNS Resolution in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Domain Name System (DNS) resolution is a critical component in Azure Kubernetes Service (AKS), enabling pods and services to communicate using human-readable names instead of IP addresses. AKS provides built-in DNS services to ensure seamless name resolution for both internal cluster resources and external endpoints. Understanding how DNS works in AKS helps cluster operators and developers ensure reliable connectivity, optimize performance, and troubleshoot networking issues effectively.

## CoreDNS in Azure Kubernetes Service

[CoreDNS](https://coredns.io/) is the default DNS service in Azure Kubernetes Service (AKS), providing internal name resolution and service discovery for workloads running in the cluster. It operates as a set of pods in the kube-system namespace and is tightly integrated with Kubernetes networking.

When a pod in AKS issues a DNS query—such as resolving the name of another service—the request is routed to the CoreDNS pods. These pods process the query and return the appropriate IP address or forward the request to an upstream DNS server for external domains.

This architecture ensures a balance between flexibility and operational safety in a managed environment. For details on how to customize CoreDNS in AKS, refer to the [CoreDNS customization guide](coredns-custom).

For information on the CoreDNS project, see [the CoreDNS upstream project page](https://coredns.io/).

## LocalDNS in Azure Kubernetes Service

Note

This document provides an overview of what LocalDNS is and its benefits in AKS. It doesn't include setup instructions. For guidance on enabling and configuring LocalDNS, see the [LocalDNS how-to guide](localdns-custom).

### Overview

LocalDNS is an advanced feature in Azure Kubernetes Service (AKS) that deploys a Domain Name System (DNS) proxy on each node to provide highly resilient, low-latency DNS resolution. By handling DNS queries locally, this proxy reduces traffic to the CoreDNS addon pods, improving overall DNS reliability and performance in the cluster. LocalDNS is especially beneficial in large clusters or environments with high DNS query volumes, where centralized DNS resolution can become a bottleneck.

When LocalDNS is enabled, AKS deploys a local DNS cache as a `systemd`

service on each node. Pods on the node send their DNS queries to this local cache, enabling faster resolution by reducing network hops. This approach also minimizes `conntrack`

table usage, lowering the risk of table exhaustion. Additionally, if upstream DNS becomes unavailable, LocalDNS can continue serving cached responses for a configurable duration, helping maintain pod connectivity and service reliability.

### Key capabilities

**Reduced DNS resolution latency:**Each AKS node runs a LocalDNS`systemd`

service. Workloads running on the node send DNS queries to this service, which resolves them locally, reducing network hops and speeding up DNS lookups.**Customizable DNS behavior:**You can use`kubeDNSOverrides`

and`vnetDNSOverrides`

to control DNS behavior in the cluster.**Avoid conntrack races and conntrack table exhaustion:**Pods send DNS queries to the LocalDNS service on the same node without creating new`conntrack`

table entries. Skipping the connection tracking helps reduce[conntrack races](https://github.com/kubernetes/kubernetes/issues/56903)and avoids User Datagram Protocol (UDP) DNS entries from filling up`conntrack`

tables. This optimization prevents dropped and rejected connections caused by`conntrack`

table exhaustion and race conditions.**Connection upgraded to TCP:**The connection from the`localdns`

cache to the cluster’s CoreDNS service uses Transmission Control Protocol (TCP). TCP allows for connection rebalancing and removes`conntrack`

table entries when the server closes the connection (in contrast to UDP connections, which have a default 30-second timeout). Applications don't need changes, because the`localdns`

service still listens for UDP traffic.**Caching:**The LocalDNS cache plugin can be configured with serveStale and Time to Live (TTL) settings.`serveStale`

,`serveStaleDurationInSeconds`

, and`cacheDurationInSeconds`

parameters can be configured to achieve DNS resiliency, even during an upstream DNS outage.**Protocol control:**You can set the DNS query protocol (such as PreferUDP or ForceTCP) for each domain. This flexibility lets you optimize DNS traffic for specific domains or meet network requirements.

### Other benefits and considerations

| Benefits | Considerations |
|---|---|
Better scalability: Reduces load on centralized CoreDNS pods |
Minimal resource overhead: Uses a small amount of CPU and memory on each node |
Seamless integration: Does not require changes to existing application connections |
Configuration changes: Updates require node image upgrades, which can cause temporary disruptions |
Block invalid search domains: Prevents invalid DNS queries at the node level |

By using LocalDNS, you get faster and more reliable DNS resolution for your workloads, reduce the risk of DNS-related outages, and gain more control over DNS traffic in your AKS environment.

## Next steps

To learn how to enable LocalDNS and configure its settings in your AKS cluster, see the [LocalDNS how-to guide](localdns-custom).

To learn more about core network concepts, see [Network concepts for applications in AKS](concepts-network).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-concepts -->

# Advanced Container Networking Services for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services is a suite of services designed to enhance the networking capabilities of Azure Kubernetes Service (AKS) clusters. Advanced Container Networking Services offers the following key feature sets: [ Container Network Observability](#container-network-observability),

[, and](#container-network-security)

**Container Network Security**[. These features provide deep insights into network traffic, strengthen security measures, and optimize network performance for containerized applications running in AKS.](#container-network-performance)

**Container Network Performance**## Container Network Observability

Container Network Observability provides deep insights into network traffic and performance across containerized environments. This feature set **works across both Cilium and non-Cilium data planes**, offering flexibility for diverse networking needs. The feature uses eBPF to enhance scalability and performance by identifying potential bottlenecks and network congestion before applications are affected.

Key benefits of Container Network Observability include:

- Compatibility with all Container Networking Interface (CNI) variants in Azure.
, including node-level metrics and Hubble metrics for detailed network insights.*Container network metrics*- Hubble metrics for Domain Name System (DNS) resolution, pod-to-pod communication, and service interactions.
that capture essential metadata such as IPs, ports, and traffic flow for troubleshooting, monitoring, and security enforcement.*Container network logs*- Integration with the managed service for Prometheus in Azure Monitor and Azure Managed Grafana for simplified metrics storage and visualization.

### Container network metrics

This feature collects node-level metrics, including CPU, memory, and network performance, to monitor the health of cluster nodes. For deeper insights, Hubble metrics provide data on DNS resolution times, service-to-service communication, and pod-level network behavior. These metrics help you analyze application performance, detect anomalies, and optimize workloads.

For more information, see the [metrics overview](container-network-observability-metrics).

### Container network logs

Container network logs give you detailed insight into traffic within and across clusters by capturing metadata like source and destination IP addresses, ports, protocols, and flow direction. These logs enable monitoring network behavior, troubleshooting connectivity issues, and enforcing security policies. Persistent and real-time logging options ensure comprehensive, actionable network observability.

For more information, see the [container network logs overview](container-network-observability-logs).

## Container Network Security

Container Network Security enhances the security posture of AKS clusters by providing advanced network security features. It leverages eBPF technology to enforce network policies at the kernel level, ensuring efficient and effective security controls for containerized applications. **Container Network Security is available only on clusters with Azure CNI Powered by Cilium**.

### FQDN-based filtering

FQDN-based filtering allows you to create network policies based on fully qualified domain names (FQDNs) rather than IP addresses. This capability simplifies policy management, especially in dynamic environments where IP addresses frequently change. By using FQDNs, you can ensure that your applications communicate only with trusted external services, enhancing security and compliance.

For more information, see the [FQDN-based filtering overview](container-network-security-fqdn-filtering-concepts).

### Layer 7 policy

Layer 7 policy enables application-layer traffic control, allowing you to define policies based on specific application protocols. This feature provides granular control over network traffic, enabling you to enforce security policies that align with application behavior. With Layer 7 policy, you can monitor and restrict traffic based on HTTP methods, URLs, headers, and other application-level attributes.

For more information, see the [Layer 7 policy overview](container-network-security-l7-policy-concepts).

### WireGuard Encryption (preview)

WireGuard Encryption leverages the WireGuard protocol to provide secure, encrypted communication between Cilium-managed endpoints within your AKS cluster. This feature ensures that data transmitted over the network is protected from eavesdropping and tampering, enhancing the overall security of your containerized applications.

For more information, see the [WireGuard encryption overview](container-network-security-wireguard-encryption-concepts).

## Container Network Performance

Container Network Performance optimizes network performance for containerized applications running in AKS clusters. It leverages eBPF technology to enhance network routing and reduce latency, ensuring that applications can communicate efficiently and effectively. **Container Network Performance is available only on clusters with Azure CNI Powered by Cilium**.

### eBPF Host Routing

eBPF Host Routing uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in AKS clusters.

For more information, see the [eBPF Host Routing overview](container-network-performance-ebpf-host-routing).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/limit-egress-traffic -->

# Limit network traffic with Azure Firewall in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use the [outbound network and fully qualified domain name (FQDN) rules for AKS clusters](outbound-rules-control-egress) to control egress traffic using Azure Firewall. To simplify this configuration, Azure Firewall provides an Azure Kubernetes Service (`AzureKubernetesService`

) FQDN tag that restricts outbound traffic from the AKS cluster.

## Firewall frontend IP requirements

**Production minimum**: Use at least 20 frontend IPs on Azure Firewall to avoid source network address translation (SNAT) port exhaustion.**High-traffic clusters**: If your cluster creates many outbound connections to the same destinations, you might need more frontend IPs to avoid maxing out ports per IP**API server protection**: Add the firewall's public frontend IP to[API server authorized IP ranges](api-server-authorized-ip-ranges)for enhanced security**Developer access**: When using authorized IP ranges, either use a jumpbox in the firewall's virtual network (VNet) or add developer endpoint IPs to the authorized range

This guidance applies throughout the configuration process described in this article.

Note

The FQDN tag contains all the FQDNs listed in [outbound network and FQDN rules for AKS clusters](outbound-rules-control-egress) and is automatically updated.

## Architecture overview

The following diagram illustrates the architecture of an AKS cluster with restricted egress traffic using Azure Firewall:

Key components of this architecture include:

**Public ingress is forced to flow through firewall filters**:- AKS agent nodes are isolated in a dedicated subnet.
[Azure Firewall](/en-us/azure/firewall/overview)is deployed in its own subnet.- A DNAT rule translates the firewall public IP into the load balancer frontend IP.

**Outbound requests start from agent nodes to the Azure Firewall internal IP using a**:[user-defined route (UDR)](egress-outboundtype)- Requests from AKS agent nodes follow a UDR that has been placed on the subnet the AKS cluster was deployed into.
- Azure Firewall egresses out of the VNet from a public IP frontend.
- Access to the public internet or other Azure services flows to and from the firewall frontend IP address.
- You can protect access to the AKS control plane using
[API server authorized IP ranges](api-server-authorized-ip-ranges), including the firewall public frontend IP address.

**Internal traffic**:- You can use an
[internal load balancer](internal-lb)for internal traffic, which you could isolate on its own subnet, instead of or alongside a[public load balancer](load-balancer-standard).

- You can use an

## Configure environment variables

The following table lists the environment variables used in this article. Set these variables in your shell before proceeding, or modify the commands to use your own values.

| Variable | Description | Example value |
|---|---|---|
`PREFIX` |
Prefix for resource names | `aks-egress` |
`RESOURCE_GROUP` |
Name of the resource group | `aks-egress-rg` |
`LOCATION` |
Azure region for resources | `eastus` |
`PLUGIN` |
Network plugin for AKS | `azure` |
`CLUSTER_NAME` |
Name of the AKS cluster | `aks-egress` |
`VNET_NAME` |
Name of the virtual network | `aks-egress-vnet` |
`AKS_SUBNET_NAME` |
Name of the subnet for AKS | `aks-subnet` |
`FW_SUBNET_NAME` |
Name of the subnet for Azure Firewall | `AzureFirewallSubnet` |
`FW_NAME` |
Name of the Azure Firewall | `aks-egress-fw` |
`FW_PUBLICIP_NAME` |
Name of the public IP for Azure Firewall | `aks-egress-fwpublicip` |
`FW_IPCONFIG_NAME` |
Name of the IP configuration for Azure Firewall | `aks-egress-fwconfig` |
`FW_ROUTE_TABLE_NAME` |
Name of the route table for Azure Firewall | `aks-egress-fwrt` |
`FW_ROUTE_NAME_1` |
Name of the route for Azure Firewall | `aks-egress-fwrn` |
`FW_ROUTE_NAME_2` |
Name of the internet route for Azure Firewall | `aks-egress-fwrn-internet` |

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a virtual network with multiple subnets

Provision a VNet with two separate subnets: one for the cluster and one for the firewall. Optionally, you can create one for internal service ingress. The following diagram illustrates the empty network topology before deploying any resources:

Create a VNet using the

command.`az network vnet create`

`az network vnet create \ --resource-group $RESOURCE_GROUP \ --name $VNET_NAME \ --location $LOCATION \ --address-prefixes 10.42.0.0/16 \ --subnet-name $AKS_SUBNET_NAME \ --subnet-prefix 10.42.1.0/24`

Create a subnet for Azure Firewall using the

command.`az network vnet subnet create`

`# Dedicated subnet for Azure Firewall (subnet must be named "AzureFirewallSubnet") az network vnet subnet create \ --resource-group $RESOURCE_GROUP \ --vnet-name $VNET_NAME \ --name $FW_SUBNET_NAME \ --address-prefix 10.42.2.0/24`


## Create a public IP for Azure Firewall

Create a standard SKU public IP resource using the

command. This resource is used as the frontend IP address for the Azure Firewall.`az network public-ip create`

`az network public-ip create --resource-group $RESOURCE_GROUP --name $FW_PUBLICIP_NAME --location $LOCATION --sku "Standard"`


## Install the Azure Firewall CLI extension

Register the

[Azure Firewall CLI extension](https://github.com/Azure/azure-cli-extensions/tree/main/src/azure-firewall)to create an Azure Firewall using thecommand.`az extension add`

`az extension add --name azure-firewall`


## Create an Azure Firewall and enable DNS proxy

Note

For high-traffic scenarios, see the [firewall frontend IP requirements](#firewall-frontend-ip-requirements) section.

For more information on how to create an Azure Firewall with multiple IPs, see [Create an Azure Firewall with multiple public IP addresses using Bicep](/en-us/azure/firewall/quick-create-multiple-ip-bicep).

Create an Azure Firewall and enable DNS proxy using the

command with`az network firewall create`

`--enable-dns-proxy`

set to`true`

.`az network firewall create --resource-group $RESOURCE_GROUP --name $FW_NAME --location $LOCATION --enable-dns-proxy true`

Setting up the public IP address to the Azure Firewall might take a few minutes. Once it's ready, you can assign the IP address to the firewall front end.

Note

To use FQDN on network rules, you need DNS proxy enabled. When DNS proxy is enabled, the firewall listens on port 53 and forwards DNS requests to the DNS server you specify. This setting allows the firewall to automatically translate the FQDN.


## Create an IP configuration for Azure Firewall

Create an Azure Firewall IP configuration using the

command.`az network firewall ip-config create`

`az network firewall ip-config create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --name $FW_IPCONFIG_NAME --public-ip-address $FW_PUBLICIP_NAME --vnet-name $VNET_NAME`


## Get the Azure Firewall IP addresses

Save the public and private firewall frontend IP addresses for configuration later using the following commands:

`export FW_PUBLIC_IP=$(az network public-ip show --resource-group $RESOURCE_GROUP --name $FW_PUBLICIP_NAME --query "ipAddress" -o tsv) export FW_PRIVATE_IP=$(az network firewall show --resource-group $RESOURCE_GROUP --name $FW_NAME --query "ipConfigurations[0].privateIPAddress" -o tsv)`

Note

For API server security, see the

[firewall frontend IP requirements](#firewall-frontend-ip-requirements)section.

## UDR configuration for AKS egress through Azure Firewall

Azure automatically routes traffic between Azure subnets, VNets, and on-premises networks. To modify default routing, create a route table with the following requirements:

**Required route parameters**:

**Route destination**:`0.0.0.0/0`

(all traffic)**Next hop type**: Network virtual appliance (NVA)**Next hop IP**: Azure Firewall private IP address**Association**: One route table per subnet (*zero*or*one*allowed)

**UDR constraints**:

- Default internet route (
`0.0.0.0/0`

) already exists but requires public IP for SNAT. - Route must point to gateway/NVA, not directly to internet.
- AKS validates route configuration and prevents direct internet routes.
- Each subnet supports maximum of
*one*associated route table.

**Outbound type impact**:

**UDR (**: No load balancer public IP created for outbound requests.`userDefinedRouting`

)**Load Balancer public IP**: Only created for inbound requests with`LoadBalancer`

service type.**SNAT configuration**: Requires proper public IP configuration for outbound connectivity.

For more information, see [Outbound rules for Azure Load Balancer](/en-us/azure/load-balancer/outbound-rules#scenario6out).

## Create a route with a hop to Azure Firewall

Create an empty route table using the

command. The route table defines the Azure Firewall as the next hop. Each subnet can have`az network route-table create`

*zero*or*one*route table associated to it.`az network route-table create --resource-group $RESOURCE_GROUP --location $LOCATION --name $FW_ROUTE_TABLE_NAME`

Create routes in the route table for the subnets using the

command.`az network route-table route create`

`az network route-table route create --resource-group $RESOURCE_GROUP --name $FW_ROUTE_NAME_1 --route-table-name $FW_ROUTE_TABLE_NAME --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address $FW_PRIVATE_IP az network route-table route create --resource-group $RESOURCE_GROUP --name $FW_ROUTE_NAME_2 --route-table-name $FW_ROUTE_TABLE_NAME --address-prefix $FW_PUBLIC_IP/32 --next-hop-type Internet`


For information on how to override Azure's default system routes or add more routes to a subnet's route table, see the [Virtual network route table documentation](/en-us/azure/virtual-network/virtual-networks-udr-overview#user-defined).

## Azure Firewall outbound rules for AKS

Note

For applications outside of the `kube-system`

or `gatekeeper-system`

namespaces that need to talk to the API server, an extra network rule to allow TCP communication to port 443 for the API server IP in addition to adding application rule for `fqdn-tag`

of `AzureKubernetesService`

is required.

The following network rules are required for AKS egress traffic control through Azure Firewall:

- The first network rule allows access to port 9000 via TCP.
- The second network rule allows access to port 1194 via UDP. If you're deploying to Microsoft Azure operated by 21Vianet, see the
[Azure operated by 21Vianet required network rules](outbound-rules-control-egress#microsoft-azure-operated-by-21vianet-required-network-rules). In this article, the commands use the`AzureCloud.$LOCATION`

service tag as the destination address. Service tags represent groups of IP address prefixes for Azure services in specific regions. This automatically includes the appropriate CIDR ranges for Azure services without requiring manual IP range specification. - The third network rule opens port 123 to
`ntp.ubuntu.com`

FQDN via UDP. Adding an FQDN as a network rule is one of the specific features of Azure Firewall, so you need to adapt it when using your own options. - The fourth and fifth network rules allow access to pull containers from GitHub Container Registry (
`ghcr.io`

) and Docker Hub (`docker.io`

).

## Create network rules on Azure Firewall

Create the network rules using the following

commands.`az network firewall network-rule create`

`az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'apitcp' --protocols 'TCP' --source-addresses '*' --destination-addresses "AzureCloud.$LOCATION" --destination-ports 9000 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'apiudp' --protocols 'UDP' --source-addresses '*' --destination-addresses "AzureCloud.$LOCATION" --destination-ports 1194 --action allow --priority 100 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'time' --protocols 'UDP' --source-addresses '*' --destination-fqdns 'ntp.ubuntu.com' --destination-ports 123 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'ghcr' --protocols 'TCP' --source-addresses '*' --destination-fqdns ghcr.io pkg-containers.githubusercontent.com --destination-ports '443' az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'docker' --protocols 'TCP' --source-addresses '*' --destination-fqdns docker.io registry-1.docker.io production.cloudflare.docker.com --destination-ports '443'`


## Create application rules on Azure Firewall

Create the application rule using the

command.`az network firewall application-rule create`

`az network firewall application-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwar' --name 'fqdn' --source-addresses '*' --protocols 'http=80' 'https=443' --fqdn-tags "AzureKubernetesService" --action allow --priority 100`


To learn more about Azure Firewall, see the [Azure Firewall documentation](/en-us/azure/firewall/overview).

## Associate the route table to AKS

To associate the cluster with the firewall, the dedicated subnet for the cluster's subnet must reference the route table.

Associate the route table to AKS using the

command.`az network vnet subnet update`

`az network vnet subnet update --resource-group $RESOURCE_GROUP --vnet-name $VNET_NAME --name $AKS_SUBNET_NAME --route-table $FW_ROUTE_TABLE_NAME`


## Deploy an AKS cluster that follows your outbound rules

You can now deploy an AKS cluster into the existing VNet. You use the [ userDefinedRouting outbound type](egress-outboundtype), which ensures that any outbound traffic is forced through the firewall and no other egress paths exist. You can also use the

[.](egress-outboundtype#outbound-type-of-loadbalancer)

`loadBalancer`

outbound typeSet an environment variable for the subnet ID of the target subnet using the following command:

`SUBNET_ID=$(az network vnet subnet show --resource-group $RESOURCE_GROUP --vnet-name $VNET_NAME --name $AKS_SUBNET_NAME --query id -o tsv)`


You define the outbound type to use the UDR that already exists on the subnet. This configuration enables AKS to skip the setup and IP provisioning for the load balancer.

Tip

You can add extra features to the cluster deployment, such as [ private clusters](private-clusters).

For API server authorized IP ranges setup and developer access considerations, see the [firewall frontend IP requirements](#firewall-frontend-ip-requirements) section.

## Create an AKS cluster with system-assigned identities

Note

AKS creates a system-assigned kubelet identity in the node resource group if you don't [specify your own kubelet managed identity](use-managed-identity#create-a-kubelet-managed-identity).

For user-defined routing, system-assigned identity only supports the CNI network plugin.

Create an AKS cluster using a system-assigned managed identity with the CNI network plugin using the

command.`az aks create`

`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --location $LOCATION \ --node-count 3 \ --network-plugin azure \ --outbound-type userDefinedRouting \ --vnet-subnet-id $SUBNET_ID \ --api-server-authorized-ip-ranges $FW_PUBLIC_IP \ --generate-ssh-keys`


## Create user-assigned identities

If you don't have user-assigned identities, follow the steps in this section. If you already have user-assigned identities, skip to [Create an AKS cluster with user-assigned identities](#create-an-aks-cluster-with-user-assigned-identities).

Create a managed identity using the

command.`az identity create`

`az identity create --name myIdentity --resource-group $RESOURCE_GROUP`

The output should resemble the following example output:

`{ ... "id": "/subscriptions/<subscriptionid>/resourcegroups/aks-egress-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "eastus", "name": "myIdentity", ... "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`

Create a kubelet managed identity using the

command.`az identity create`

`az identity create --name myKubeletIdentity --resource-group $RESOURCE_GROUP`

The output should resemble the following example output:

`{ ... "id": "/subscriptions/<subscriptionid>/resourcegroups/aks-egress-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myKubeletIdentity", "location": "eastus", "name": "myKubeletIdentity", ... "resourceGroup": "aks-egress-rg", ... "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


Note

If you create your own VNet and route table where the resources are outside of the worker node resource group, the CLI automatically adds the role assignment. If you're using an ARM template or other method, you need to use the principal ID of the cluster managed identity to perform a [role assignment](use-managed-identity#add-a-role-assignment-for-a-system-assigned-managed-identity).

## Create an AKS cluster with user-assigned identities

Create an AKS cluster with your existing user-assigned managed identities in the subnet using the

command. Provide the resource ID of the managed identity for the control plane and the resource ID of the kubelet identity.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --location $LOCATION \ --node-count 3 \ --network-plugin kubenet \ --outbound-type userDefinedRouting \ --vnet-subnet-id $SUBNET_ID \ --api-server-authorized-ip-ranges $FW_PUBLIC_IP \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id> \ --generate-ssh-keys`


## Enable developer access to the API server

If you used authorized IP ranges for your cluster in the previous step, you need to add your developer tooling IP addresses to the AKS cluster list of approved IP ranges so you access the API server from there. You can also configure a jumpbox with the needed tooling inside a separate subnet in the firewall's VNet.

Retrieve your IP address using the following command:

`CURRENT_IP=$(dig @resolver1.opendns.com ANY myip.opendns.com +short)`

Add the IP address to the approved ranges using the

command.`az aks update`

`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --api-server-authorized-ip-ranges $CURRENT_IP/32`


## Connect to the AKS cluster

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Deploy a public service on AKS

You can now start exposing services and deploying applications to this cluster. This example exposes a public service, but you also might want to expose an internal service using an [internal load balancer](internal-lb).

Review the

[AKS Store Demo quickstart](https://github.com/Azure-Samples/aks-store-demo/blob/main/aks-store-quickstart.yaml)manifest to understand the deployed components.Deploy the service using the

`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-quickstart.yaml`


## Get the load balancer internal IP and service IP

Get the internal IP address assigned to the load balancer using the

`kubectl get services`

command.`kubectl get services`

The IP address should be listed in the

`EXTERNAL-IP`

column, as shown in the following example output:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE kubernetes ClusterIP 10.0.0.1 <none> 443/TCP 9m10s order-service ClusterIP 10.0.104.144 <none> 3000/TCP 11s product-service ClusterIP 10.0.237.60 <none> 3002/TCP 10s rabbitmq ClusterIP 10.0.161.128 <none> 5672/TCP,15672/TCP 11s store-front LoadBalancer 10.0.89.139 20.39.18.6 80:32271/TCP 10s`

Get the service IP using the

`kubectl get svc store-front`

command.`SERVICE_IP=$(kubectl get svc store-front -o jsonpath='{.status.loadBalancer.ingress[*].ip}')`


## Create a DNAT rule on Azure Firewall

Important

When you use Azure Firewall to restrict egress traffic and create a UDR to force all egress traffic, make sure you create an appropriate DNAT rule in Azure Firewall to correctly allow ingress traffic. Using Azure Firewall with a UDR breaks the ingress setup due to asymmetric routing. The issue occurs if the AKS subnet has a default route that goes to the firewall's private IP address, but you're using a public load balancer - ingress or Kubernetes service of type `loadBalancer`

. In this case, the incoming load balancer traffic is received via its public IP address, but the return path goes through the firewall's private IP address. Because the firewall is stateful, it drops the returning packet because the firewall isn't aware of an established session. To learn how to integrate Azure Firewall with your ingress or service load balancer, see [Integrate Azure Firewall with Azure Standard Load Balancer](/en-us/azure/firewall/integrate-lb).

To configure inbound connectivity, you need to write a DNAT rule to the Azure Firewall. To test connectivity to your cluster, a rule is defined for the firewall frontend public IP address to route to the internal IP exposed by the internal service. You can customize the destination address. The translated address must be the IP address of the internal load balancer. The translated port must be the exposed port for your Kubernetes service. You also need to specify the internal IP address assigned to the load balancer created by the Kubernetes service.

Add the NAT rule using the

command.`az network firewall nat-rule create`

`az network firewall nat-rule create --collection-name exampleset --destination-addresses $FW_PUBLIC_IP --destination-ports 80 --firewall-name $FW_NAME --name inboundrule --protocols Any --resource-group $RESOURCE_GROUP --source-addresses '*' --translated-port 80 --action Dnat --priority 100 --translated-address $SERVICE_IP`


## Validate connectivity

Navigate to the Azure Firewall frontend IP address in a browser to validate connectivity. You should see the AKS store app. In this example, the firewall public IP was

`52.253.228.132`

:, you can view products, add them to your cart, and then place an order.


## Clean up resources

If you no longer need the resources created in this article, you can delete them to avoid incurring future costs.

Delete the AKS resource group using the

command.`az group delete`

`az group delete --name $RESOURCE_GROUP`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/advanced-container-networking-services-overview -->

# Advanced Container Networking Services for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services is a suite of services designed to enhance the networking capabilities of Azure Kubernetes Service (AKS) clusters. Advanced Container Networking Services offers the following key feature sets: [ Container Network Observability](#container-network-observability),

[, and](#container-network-security)

**Container Network Security**[. These features provide deep insights into network traffic, strengthen security measures, and optimize network performance for containerized applications running in AKS.](#container-network-performance)

**Container Network Performance**## Container Network Observability

Container Network Observability provides deep insights into network traffic and performance across containerized environments. This feature set **works across both Cilium and non-Cilium data planes**, offering flexibility for diverse networking needs. The feature uses eBPF to enhance scalability and performance by identifying potential bottlenecks and network congestion before applications are affected.

Key benefits of Container Network Observability include:

- Compatibility with all Container Networking Interface (CNI) variants in Azure.
, including node-level metrics and Hubble metrics for detailed network insights.*Container network metrics*- Hubble metrics for Domain Name System (DNS) resolution, pod-to-pod communication, and service interactions.
that capture essential metadata such as IPs, ports, and traffic flow for troubleshooting, monitoring, and security enforcement.*Container network logs*- Integration with the managed service for Prometheus in Azure Monitor and Azure Managed Grafana for simplified metrics storage and visualization.

### Container network metrics

This feature collects node-level metrics, including CPU, memory, and network performance, to monitor the health of cluster nodes. For deeper insights, Hubble metrics provide data on DNS resolution times, service-to-service communication, and pod-level network behavior. These metrics help you analyze application performance, detect anomalies, and optimize workloads.

For more information, see the [metrics overview](container-network-observability-metrics).

### Container network logs

Container network logs give you detailed insight into traffic within and across clusters by capturing metadata like source and destination IP addresses, ports, protocols, and flow direction. These logs enable monitoring network behavior, troubleshooting connectivity issues, and enforcing security policies. Persistent and real-time logging options ensure comprehensive, actionable network observability.

For more information, see the [container network logs overview](container-network-observability-logs).

## Container Network Security

Container Network Security enhances the security posture of AKS clusters by providing advanced network security features. It leverages eBPF technology to enforce network policies at the kernel level, ensuring efficient and effective security controls for containerized applications. **Container Network Security is available only on clusters with Azure CNI Powered by Cilium**.

### FQDN-based filtering

FQDN-based filtering allows you to create network policies based on fully qualified domain names (FQDNs) rather than IP addresses. This capability simplifies policy management, especially in dynamic environments where IP addresses frequently change. By using FQDNs, you can ensure that your applications communicate only with trusted external services, enhancing security and compliance.

For more information, see the [FQDN-based filtering overview](container-network-security-fqdn-filtering-concepts).

### Layer 7 policy

Layer 7 policy enables application-layer traffic control, allowing you to define policies based on specific application protocols. This feature provides granular control over network traffic, enabling you to enforce security policies that align with application behavior. With Layer 7 policy, you can monitor and restrict traffic based on HTTP methods, URLs, headers, and other application-level attributes.

For more information, see the [Layer 7 policy overview](container-network-security-l7-policy-concepts).

### WireGuard Encryption (preview)

WireGuard Encryption leverages the WireGuard protocol to provide secure, encrypted communication between Cilium-managed endpoints within your AKS cluster. This feature ensures that data transmitted over the network is protected from eavesdropping and tampering, enhancing the overall security of your containerized applications.

For more information, see the [WireGuard encryption overview](container-network-security-wireguard-encryption-concepts).

## Container Network Performance

Container Network Performance optimizes network performance for containerized applications running in AKS clusters. It leverages eBPF technology to enhance network routing and reduce latency, ensuring that applications can communicate efficiently and effectively. **Container Network Performance is available only on clusters with Azure CNI Powered by Cilium**.

### eBPF Host Routing

eBPF Host Routing uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in AKS clusters.

For more information, see the [eBPF Host Routing overview](container-network-performance-ebpf-host-routing).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-oidc-issuer -->

# Create an OpenID Connect provider on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to create and manage an OpenID Connect (OIDC) provider for your Azure Kubernetes Service (AKS) cluster. The OIDC issuer allows your AKS cluster to integrate with identity providers like Microsoft Entra ID, enabling secure authentication and single sign-on (SSO) capabilities for applications running within the cluster.

## About OpenID Connect (OIDC) on AKS

[OpenID Connect](/en-us/azure/active-directory/fundamentals/auth-oidc) (OIDC) extends the OAuth 2.0 authorization protocol for use as another authentication protocol issued by Microsoft Entra ID. You can use OIDC to enable single sign-on (SSO) between OAuth-enabled applications on your Azure Kubernetes Service (AKS) cluster using a security token called an ID token. You can enable the OIDC issuer on your AKS clusters, which allows Microsoft Entra ID (or another cloud provider's identity and access management platform) to discover the API server's public signing keys.

## Prerequisites

**Platform requirements**:

- Azure CLI version 2.42.0+ (
`az --version`

to check version,[install or upgrade Azure CLI](/en-us/cli/azure/install-azure-cli)if needed) - Minimum Kubernetes version is 1.22+

**Version-specific behavior**:

- OIDC issuer enabled by default (no
`--enable-oidc-issuer`

flag needed) for Kubernetes version 1.34+ - Token auto-extension disabled (
`--service-account-extend-token-expiration=false`

) for Kubernetes version 1.30.0+ - Manual enablement required if not previously configured for Kubernetes version earlier than 1.34

**Important considerations**:

- You can't disable OIDC issuer once enabled
- Enabling OIDC issuer on existing clusters requires API server restart (brief downtime)
- Maximum token lifetime is 24 hours (one day)
- Projected service account tokens required for Kubernetes 1.30+ clusters

## Create an AKS cluster with the OIDC issuer

Create an AKS cluster using the

command with the`az aks create`

`--enable-oidc-issuer`

parameter.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster with OIDC issuer enabled (OIDC issuer enabled by default for Kubernetes 1.34+) az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --enable-oidc-issuer \ --generate-ssh-keys`


## Enable the OIDC issuer on an existing AKS cluster

Enable the OIDC issuer on an existing AKS cluster using the

command with the`az aks update`

`--enable-oidc-issuer`

parameter.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Enable the OIDC issuer on the existing AKS cluster az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-oidc-issuer`


## Get the OIDC issuer URL

Get the OIDC issuer URL using the

command.`az aks show`

`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Get the OIDC issuer URL az aks show \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --query "oidcIssuerProfile.issuerUrl" \ -o tsv`

By default, the issuer is set to use the base URL

`https://{region}.oic.prod-aks.azure.com`

, where the value for`{region}`

matches the location the AKS cluster is deployed in.

## Rotate the OIDC key

Important

Keep the following considerations in mind when rotating the OIDC key:

- If you want to invalidate the old key immediately after key rotation, you must rotate the OIDC key twice and restart the pods using projected service account tokens.
- Both old and new keys remain valid for 24 hours after rotation.
- Manual token refresh required every 24 hours (unless using
[Azure Identity SDK](workload-identity-overview#azure-identity-client-libraries), which rotates automatically).

Rotate the OIDC key using the

command.`az aks oidc-issuer`

`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Rotate the OIDC signing keys az aks oidc-issuer rotate-signing-keys \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP`


## Get the discovery document

Navigate to your

[OIDC issuer URL](#get-the-oidc-issuer-url)in your browser and append`/.well-known/openid-configuration`

to the URL. For example:`https://eastus.oic.prod-aks.azure.com/.well-known/openid-configuration`

.Your output should resemble the following example output:

`{ "issuer": "https://eastus.oic.prod-aks.azure.com/ffffffff-eeee-dddd-cccc-bbbbbbbbbbb0/00000000-0000-0000-0000-000000000000/", "jwks_uri": "https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/openid/v1/jwks", "response_types_supported": [ "id_token" ], "subject_types_supported": [ "public" ], "id_token_signing_alg_values_supported": [ "RS256" ] }`


## Get the JWK Set document

Navigate to the

in your browser. For example:**jwks_uri**from the discovery document`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/openid/v1/jwks`

.Your output should resemble the following example output:

`{ "keys": [ { "use": "sig", "kty": "RSA", "kid": "xxx", "alg": "RS256", "n": "xxxx", "e": "AQAB" }, { "use": "sig", "kty": "RSA", "kid": "xxx", "alg": "RS256", "n": "xxxx", "e": "AQAB" } ] }`

Note

During key rotation, there's one other key present in the discovery document.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-scale -->

# Tutorial - Scale applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you followed the previous tutorials, you have a working Kubernetes cluster and Azure Store Front app.

In this tutorial, you scale out the pods in the app, try pod autoscaling, and scale the number of Azure VM nodes to change the cluster's capacity for hosting workloads. You learn how to:

- Scale the Kubernetes nodes.
- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created an AKS cluster, deployed an application, and used Azure Service Bus to redeploy an updated application. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Manually scale pods

View the pods in your cluster using the

command.`kubectl get`

`kubectl get pods`

The following example output shows the pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE order-service-848767080-tf34m 1/1 Running 0 31m product-service-4019737227-2q2qz 1/1 Running 0 31m store-front-2606967446-2q2qz 1/1 Running 0 31m`

Manually change the number of pods in the

*store-front*deployment using thecommand.`kubectl scale`

`kubectl scale --replicas=5 deployment.apps/store-front`

Verify the additional pods were created using the

command.`kubectl get pods`

`kubectl get pods --selector app=store-front`

The following example output shows the additional pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE store-front-3309479140-2hfh0 1/1 Running 0 3m store-front-3309479140-bzt05 1/1 Running 0 3m store-front-3309479140-fvcvm 1/1 Running 0 3m store-front-3309479140-hrbf2 1/1 Running 0 15m store-front-3309479140-qphz8 1/1 Running 0 3m`


## Autoscale pods

To use the horizontal pod autoscaler, all containers must have defined CPU requests and limits, and pods must have specified requests. In the `aks-store-quickstart`

deployment, the *front-end* container requests 1m CPU with a limit of 1000m CPU.

These resource requests and limits are defined for each container, as shown in the following condensed example YAML:

```
...
containers:
- name: store-front
image: ghcr.io/azure-samples/aks-store-demo/store-front:latest
ports:
- containerPort: 8080
name: store-front
...
resources:
requests:
cpu: 1m
...
limits:
cpu: 1000m
...
```


### Autoscale pods using a manifest file

Create a manifest file to define the autoscaler behavior and resource limits, as shown in the following condensed example manifest file

`aks-store-quickstart-hpa.yaml`

:`apiVersion: autoscaling/v2 kind: HorizontalPodAutoscaler metadata: name: store-front-hpa spec: maxReplicas: 10 # define max replica count minReplicas: 3 # define min replica count scaleTargetRef: apiVersion: apps/v1 kind: Deployment name: store-front metrics: - type: Resource resource: name: cpu target: type: Utilization averageUtilization: 50`

Apply the autoscaler manifest file using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart-hpa.yaml`

Check the status of the autoscaler using the

`kubectl get hpa`

command.`kubectl get hpa`

After a few minutes, with minimal load on the Azure Store Front app, the number of pod replicas decreases to three. You can use

`kubectl get pods`

command again to see the unneeded pods being removed.

Note

You can enable the Kubernetes-based Event-Driven Autoscaler (KEDA) AKS add-on to your cluster to drive scaling based on the number of events needing to be processed. For more information, see [Enable simplified application autoscaling with the Kubernetes Event-Driven Autoscaling (KEDA) add-on (Preview)](keda-about).

## Manually scale AKS nodes

If you created your Kubernetes cluster using the commands in the previous tutorials, your cluster has two nodes. If you want to increase or decrease this amount, you can manually adjust the number of nodes.

The following example increases the number of nodes to three in the Kubernetes cluster named *myAKSCluster*. The command takes a couple of minutes to complete.

Scale your cluster nodes using the

command.`az aks scale`

`az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 3`

Once the cluster successfully scales, your output will be similar to following example output:

`"aadProfile": null, "addonProfiles": null, "agentPoolProfiles": [ { ... "count": 3, "mode": "System", "name": "nodepool1", "osDiskSizeGb": 128, "osDiskType": "Managed", "osType": "Linux", "ports": null, "vmSize": "Standard_DS2_v2", "vnetSubnetId": null ... } ... ]`


You can also autoscale the nodes in your cluster. For more information, see [Use the cluster autoscaler with node pools](cluster-autoscaler#use-the-cluster-autoscaler-on-node-pools).

## Next steps

In this tutorial, you used different scaling features in your Kubernetes cluster. You learned how to:

- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.
- Manually scale the Kubernetes nodes.

In the next tutorial, you learn how to upgrade Kubernetes in your AKS cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-pool-snapshot -->

# Azure Kubernetes Service (AKS) node pool snapshot

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS releases a new node image weekly. Every new cluster, new node pool, or upgrade cluster always receives the latest image, which can make it hard to maintain consistency and have repeatable environments.

Node pool snapshots allow you to take a configuration snapshot of your node pool and then create new node pools or new clusters based of that snapshot for as long as that configuration and kubernetes version is supported. For more information on the supportability windows, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

The snapshot is an Azure resource that contains the configuration information from the source node pool, such as the node image version, kubernetes version, OS type, and OS SKU. You can then reference this snapshot resource and the respective values of its configuration to create any new node pool or cluster based off of it.

## Before you begin

This article assumes that you have an existing AKS cluster. If you don't have an AKS cluster, for guidance on a designing an enterprise-scale implementation of AKS, see [Plan your AKS design](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

### Limitations

- Any node pool or cluster created from a snapshot must use a VM from the same virtual machine family as the snapshot, for example, you can't create a new N-Series node pool based of a snapshot captured from a D-Series node pool because the node images in those cases are structurally different.
- Snapshots must be created same region as the source node pool, those snapshots can be used to create or update clusters and node pools in other regions.

## Take a node pool snapshot

In order to take a snapshot from a node pool, you need the node pool resource ID, which you can get from the following command:

```
NODEPOOL_ID=$(az aks nodepool show --name nodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --query id -o tsv)
```


Important

Your AKS node pool must be created or upgraded after Nov 10th, 2021 in order for a snapshot to be taken from it.
If you are using the `aks-preview`

Azure CLI extension version `0.5.59`

or newer, the commands for node pool snapshot have changed. For updated commands, see the [Node Pool Snapshot CLI reference](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add).

Now, to take a snapshot from the previous node pool, you use the `az aks snapshot`

CLI command.

```
az aks nodepool snapshot create --name MySnapshot --resource-group MyResourceGroup --nodepool-id $NODEPOOL_ID --location eastus
```


## Create a node pool from a snapshot

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use the following command to add a new node pool based off of this snapshot.

```
az aks nodepool add --name np2 --cluster-name myAKSCluster --resource-group myResourceGroup --snapshot-id $SNAPSHOT_ID
```


## Upgrading a node pool to a snapshot

You can upgrade a node pool to a snapshot configuration if the snapshot Kubernetes version and node image version are more recent than the current node pool versions. And the snapshot node image version is within 90 days of the node image publish date.

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use this command to upgrade this node pool to this snapshot configuration.

```
az aks nodepool upgrade --name nodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --snapshot-id $SNAPSHOT_ID
```


Note

Your node pool image version is the same contained in the snapshot and remains the same throughout every scale operation. However, if this node pool is upgraded or a node image upgrade is performed without providing a snapshot-id the node image is upgraded to the latest version.

Note

To upgrade only the node version for your node pool, use the `--node-image-only`

flag. This is required when upgrading the node image version for a node pool based on a snapshot with an identical Kubernetes version.

## Create a cluster from a snapshot

When you create a cluster from a snapshot, the snapshot configuration creates the cluster original system pool.

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use this command to create this cluster off of the snapshot configuration.

```
az aks create \
--name myAKSCluster2 \
--resource-group myResourceGroup \
--snapshot-id $SNAPSHOT_ID \
--generate-ssh-keys
```


## Next steps

- See the
[AKS release notes](https://github.com/Azure/AKS/releases)for information about the latest node images. - Learn how to upgrade the Kubernetes version with
[Upgrade an AKS cluster](upgrade-cluster). - Learn how to upgrade your node image version with
[Node Image Upgrade](node-image-upgrade) - Learn more about multiple node pools with
[Create multiple node pools](create-node-pools).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/network-isolated -->

# Create a network isolated Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Organizations typically have strict security and compliance requirements to regulate egress (outbound) network traffic from a cluster to eliminate risks of data exfiltration. By default, standard SKU Azure Kubernetes Service (AKS) clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. The conceptual document on [outbound network and FQDN rules for AKS clusters](outbound-rules-control-egress) provides a list of required endpoints for the AKS cluster and its optional add-ons and features.

One common solution to restricting outbound traffic from the cluster is to use a [firewall device](limit-egress-traffic) to restrict traffic based on firewall rules. Firewall is applicable when your application requires outbound access, but when outbound requests have to be inspected and secured. Configuring a firewall manually with required egress rules and *FQDNs* is a cumbersome process especially if your only requirement is to create an isolated AKS cluster with no outbound dependencies for the cluster bootstrapping.

To reduce risk of data exfiltration, network isolated cluster allows for bootstrapping the AKS cluster without any outbound network dependencies, even for fetching cluster components/images from Microsoft Artifact Registry (MAR). The cluster operator could incrementally set up allowed outbound traffic for each scenario they want to enable. This article walks you through the steps of creating a network isolated cluster.

## Before you begin

- Read the
[conceptual overview of this feature](concepts-network-isolated), which provides an explanation of how network isolated clusters work. The overview article also:- Explains two options for private Azure Container Registry (ACR) resource used for cluster bootstrapping - AKS-managed ACR or bring-your-own ACR.
- Explains two private cluster modes for creating private access to API server -
[private link-based](private-clusters)or[API Server Vnet Integration](api-server-vnet-integration). - Explains the two outbound types for cluster egress control -
`none`

or`block`

(preview). - Describes the
[current limitations of network isolated clusters](concepts-network-isolated#limitations).


Note

Outbound type `none`

is generally available.
Outbound type`block`

is in preview.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.71.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- You should install the
`aks-preview`

Azure CLI extension version*9.0.0b2*or later if you are using outbound type`block`

(preview).- If you don't already have the
`aks-preview`

extension, install it using thecommand.`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand.`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
- Network isolated clusters are supported on AKS clusters using Kubernetes version 1.30 or higher.
- If you're choosing to use the Bring your own (BYO) Azure Container Registry (ACR) option, you need to ensure the ACR is
[Premium SKU service tier](/en-us/azure/container-registry/container-registry-skus). - If you are using a network isolated cluster configured with API Server VNet Integration, you should follow the prerequisites and guidance in this
[document](api-server-vnet-integration).

## Deploy a network isolated cluster with AKS-managed ACR

AKS creates, manages, and reconciles an ACR resource in this option. You don't need to assign any permissions or manage the ACR. AKS manages the cache rules, private link, and private endpoint used in the network isolated cluster.

### Create a network isolated cluster

When creating a network isolated AKS cluster, you can choose one of the following private cluster modes - private link-based or API Server Vnet Integration.

Regardless of the mode you select, you should set `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

The `--bootstrap-artifact-source`

can be set to either `Direct`

or `Cache`

corresponding to using direct MAR (NOT network isolated) and private ACR (network isolated) for image pulls respectively.

The `--outbound-type parameter`

can be set to either `none`

or `block`

(preview). If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

#### Private link-based

Create a private link-based network isolated cluster by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with `--bootstrap-artifact-source`

, `--enable-private-cluster`

, and `--outbound-type`

parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --bootstrap-artifact-source Cache --outbound-type none --network-plugin azure --enable-private-cluster
```


#### API Server VNet integration

Create a network isolated cluster configured with API Server VNet Integration by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with `--bootstrap-artifact-source`

, `--enable-private-cluster`

, `--enable-apiserver-vnet-integration`

and `--outbound-type`

parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --bootstrap-artifact-source Cache --outbound-type none --network-plugin azure --enable-private-cluster --enable-apiserver-vnet-integration
```


### Update an existing AKS cluster to network isolated type

If you'd rather enable network isolation on an existing AKS cluster instead of creating a new cluster, use the [az aks update](/en-us/cli/azure/aks#az-aks-update) command.

To enable the network isolated feature on an existing AKS cluster, first run the following command to update `bootstrap-artifact-source`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache
```


Then you need to manually reimage all the exisiting nodepools:

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Note

You need to ensure the outbound exists until the first reimage completes. To check if the reimage completes, run:

```
NODEPOOLS=$(az aks nodepool list \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--query "[].name" -o tsv)
for NODEPOOL in $NODEPOOLS; do
echo "Waiting for node pool $NODEPOOL to finish upgrading..."
az aks nodepool wait \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--name "$NODEPOOL" \
--updated
echo "Node pool $NODEPOOL upgrade succeeded."
done
```


Wait and ensure the reimage completes, then run the following command to update `outbound-type`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --outbound-type none
```


Important

Remember to reimage the cluster's node pools instantly after you update the artifact source to Cache. Otherwise, the feature won't take effect for the cluster.

## Deploy a network isolated cluster with bring your own ACR

AKS supports bringing your own (BYO) ACR. To support the BYO ACR scenario, you have to configure an ACR private endpoint and a private DNS zone before you create the AKS cluster.

The following steps show how to prepare these resources:

- Custom virtual network and subnets for AKS and ACR.
- ACR, ACR cache rule, private endpoint, and private DNS zone.
- Custom control plane identity and kubelet identity.

### Step 1: Create the virtual network and subnets

```
az group create --name ${RESOURCE_GROUP} --location ${LOCATION}
az network vnet create --resource-group ${RESOURCE_GROUP} --name ${VNET_NAME} --address-prefixes 192.168.0.0/16
az network vnet subnet create --name ${AKS_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.1.0/24
SUBNET_ID=$(az network vnet subnet show --name ${AKS_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' --output tsv)
az network vnet subnet create --name ${ACR_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.2.0/24 --private-endpoint-network-policies Disabled
```


### Step 2: Disable virtual network outbound connectivity (Optional)

There are multiple ways to [disable the virtual network outbound connectivity](/en-us/azure/virtual-network/ip-services/default-outbound-access#how-can-i-transition-to-an-explicit-method-of-public-connectivity-and-disable-default-outbound-access).

### Step 3: Create the ACR and enable artifact cache

Create the ACR with the private link.

`az acr create --resource-group ${RESOURCE_GROUP} --name ${REGISTRY_NAME} --sku Premium --public-network-enabled false REGISTRY_ID=$(az acr show --name ${REGISTRY_NAME} -g ${RESOURCE_GROUP} --query 'id' --output tsv)`

Create an ACR cache rule following the below command to allow users to cache MAR container images and binaries in the new ACR, note the cache rule name and repo names must be strictly aligned with the guidance below.

`az acr cache create -n aks-managed-mcr -r ${REGISTRY_NAME} -g ${RESOURCE_GROUP} --source-repo "mcr.microsoft.com/*" --target-repo "aks-managed-repository/*"`


Note

With BYO ACR, it is your responsibility to ensure the ACR cache rule is created and maintained correctly as above. This step is critical to cluster creation, functioning and upgrading. This cache rule should NOT be modified.

### Step 4: Create a private endpoint for the ACR

```
az network private-endpoint create --name myPrivateEndpoint --resource-group ${RESOURCE_GROUP} --vnet-name ${VNET_NAME} --subnet ${ACR_SUBNET_NAME} --private-connection-resource-id ${REGISTRY_ID} --group-id registry --connection-name myConnection
NETWORK_INTERFACE_ID=$(az network private-endpoint show --name myPrivateEndpoint --resource-group ${RESOURCE_GROUP} --query 'networkInterfaces[0].id' --output tsv)
REGISTRY_PRIVATE_IP=$(az network nic show --ids ${NETWORK_INTERFACE_ID} --query "ipConfigurations[?privateLinkConnectionProperties.requiredMemberName=='registry'].privateIPAddress" --output tsv)
DATA_ENDPOINT_PRIVATE_IP=$(az network nic show --ids ${NETWORK_INTERFACE_ID} --query "ipConfigurations[?privateLinkConnectionProperties.requiredMemberName=='registry_data_$LOCATION'].privateIPAddress" --output tsv)
```


### Step 5: Create a private DNS zone and add records

Create a private DNS zone named `privatelink.azurecr.io`

. Add the records for the registry REST endpoint `{REGISTRY_NAME}.azurecr.io`

, and the registry data endpoint `{REGISTRY_NAME}.{REGISTRY_LOCATION}.data.azurecr.io`

.

```
az network private-dns zone create --resource-group ${RESOURCE_GROUP} --name "privatelink.azurecr.io"
az network private-dns link vnet create --resource-group ${RESOURCE_GROUP} --zone-name "privatelink.azurecr.io" --name MyDNSLink --virtual-network ${VNET_NAME} --registration-enabled false
az network private-dns record-set a create --name ${REGISTRY_NAME} --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP}
az network private-dns record-set a add-record --record-set-name ${REGISTRY_NAME} --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP} --ipv4-address ${REGISTRY_PRIVATE_IP}
az network private-dns record-set a create --name ${REGISTRY_NAME}.${LOCATION}.data --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP}
az network private-dns record-set a add-record --record-set-name ${REGISTRY_NAME}.${LOCATION}.data --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP} --ipv4-address ${DATA_ENDPOINT_PRIVATE_IP}
```


### Step 6: Create control plane and kubelet identities

#### Control plane identity

```
az identity create --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP}
CLUSTER_IDENTITY_RESOURCE_ID=$(az identity show --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' -o tsv)
CLUSTER_IDENTITY_PRINCIPAL_ID=$(az identity show --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'principalId' -o tsv)
```


#### Kubelet identity

```
az identity create --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP}
KUBELET_IDENTITY_RESOURCE_ID=$(az identity show --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' -o tsv)
KUBELET_IDENTITY_PRINCIPAL_ID=$(az identity show --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'principalId' -o tsv)
```


#### Grant AcrPull permissions for the Kubelet identity

```
az role assignment create --role AcrPull --scope ${REGISTRY_ID} --assignee-object-id ${KUBELET_IDENTITY_PRINCIPAL_ID} --assignee-principal-type ServicePrincipal
```


After you configure these resources, you can proceed to create the network isolated AKS cluster with BYO ACR.

### Step 7: Create network isolated cluster using BYO ACR

When creating a network isolated cluster, you can choose one of the following private cluster modes - private link-based or API Server Vnet Integration.

Regardless of the mode you select, you should set `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

The `--bootstrap-artifact-source`

can be set to either `Direct`

or `Cache`

corresponding to using direct Microsoft Artifact Registry (MAR) (NOT network isolated) and private ACR (network isolated) for image pulls respectively.

The `--outbound-type parameter`

can be set to either `none`

or `block`

(preview). If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

#### Private link-based

Create a private link-based network isolated cluster that accesses your ACR by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with the required parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --vnet-subnet-id ${SUBNET_ID} --assign-identity ${CLUSTER_IDENTITY_RESOURCE_ID} --assign-kubelet-identity ${KUBELET_IDENTITY_RESOURCE_ID} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID} --outbound-type none --network-plugin azure --enable-private-cluster
```


#### API Server VNet integration

For a network isolated cluster configured with API server VNet integration, first create a subnet and assign the correct role with the following commands:

```
az network vnet subnet create --name ${APISERVER_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.3.0/24
export APISERVER_SUBNET_ID=$(az network vnet subnet show --resource-group ${RESOURCE_GROUP} --vnet-name ${VNET_NAME} --name ${APISERVER_SUBNET_NAME} --query id -o tsv)
```


```
az role assignment create --scope ${APISERVER_SUBNET_ID} --role "Network Contributor" --assignee-object-id ${CLUSTER_IDENTITY_PRINCIPAL_ID} --assignee-principal-type ServicePrincipal
```


Create a network isolated cluster configured with API Server VNet Integration and access your ACR by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with the required parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --vnet-subnet-id ${SUBNET_ID} --assign-identity ${CLUSTER_IDENTITY_RESOURCE_ID} --assign-kubelet-identity ${KUBELET_IDENTITY_RESOURCE_ID} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID} --outbound-type none --network-plugin azure --enable-apiserver-vnet-integration --apiserver-subnet-id ${APISERVER_SUBNET_ID}
```


### Update an existing AKS cluster

If you'd rather enable network isolation on an existing AKS cluster instead of creating a new cluster, use the [az aks update](/en-us/cli/azure/aks#az-aks-update) command.

When creating the private endpoint and private DNS zone for the BYO ACR, use the existing virtual network and subnets of the existing AKS cluster. When you assign the **AcrPull** permission to the kubelet identity, use the existing kubelet identity of the existing AKS cluster.

To enable the network isolated feature on an existing AKS cluster, first run the following command to update `bootstrap-artifact-source`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID}
```


Then you need to manually reimage all the exisiting nodepools:

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Note

You need to ensure the outbound exists until the first reimage completes. To check if the reimage completes, run:

```
NODEPOOLS=$(az aks nodepool list \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--query "[].name" -o tsv)
for NODEPOOL in $NODEPOOLS; do
echo "Waiting for node pool $NODEPOOL to finish upgrading..."
az aks nodepool wait \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--name "$NODEPOOL" \
--updated
echo "Node pool $NODEPOOL upgrade succeeded."
done
```


Wait and ensure the reimage completes, then run the following command to update `outbound-type`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --outbound-type none
```


Important

Remember to reimage the cluster's node pools instantly after you update the artifact source to Cache. Otherwise, the feature won't take effect for the cluster.

### Update your ACR ID

It's possible to update the private ACR used with a network isolated cluster. To identify the ACR resource ID, use the `az aks show`

command.

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME}
```


Updating the ACR ID is performed by running the `az aks update`

command with the `--bootstrap-artifact-source`

and `--bootstrap-container-registry-resource-id`

parameters.

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id <New BYO ACR resource ID>
```


When you update the ACR ID on an existing cluster, you need to manually reimage all existing nodes.

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Important

Remember to reimage the cluster's node pools after you enable the network isolated cluster feature. Otherwise, the feature won't take effect for the cluster.

## Validate that network isolated cluster is enabled

To validate the network isolated cluster feature is enabled, use the `[az aks show](/en-us/cli/azure/aks#az-aks-show) command

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME}
```


The following output shows that the feature is enabled, based on the values of the `outboundType`

property (none or blocked) and `artifactSource`

property (Cached).

```
"kubernetesVersion": "1.30.3",
"name": "myAKSCluster"
"type": "Microsoft.ContainerService/ManagedClusters"
"properties": {
...
"networkProfile": {
...
"outboundType": "none",
...
},
...
"bootstrapProfile": {
"artifactSource": "Cache",
"containerRegistryId": "/subscriptions/my-subscription-id/my-node-resource-group-name/providers/Microsoft.ContainerRegistry/registries/my-registry-name"
},
...
}
```


## Disable network isolated cluster

Disable the network isolated cluster feature by running the `az aks update`

command with the `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Direct --outbound-type LoadBalancer
```


When you disable the feature on an existing cluster, you need to manually reimage all existing nodes.

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Important

Remember to reimage the cluster's node pools after you disable the network isolated cluster feature. Otherwise, the feature won't take effect for the cluster.

## Troubleshooting

If you're experiencing issues, such as image pull fails, see [Troubleshoot network isolated Azure Kubernetes Service (AKS) clusters issues](/en-us/troubleshoot/azure/azure-kubernetes/extensions/troubleshoot-network-isolated-cluster).

## Next steps

If you want to set up outbound restriction configuration using Azure Firewall, visit [Control egress traffic using Azure Firewall in AKS](limit-egress-traffic).

If you want to restrict how pods communicate between themselves and East-West traffic restrictions within cluster, see [Secure traffic between pods using network policies in AKS](use-network-policies).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-scheduler-configuration -->

# Scheduler configuration concepts for workload placement in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers scheduler configuration and advanced scheduling concepts for workload placement in Azure Kubernetes Service (AKS), including configurable scheduler profiles, scheduling plugins, and scheduling constraints.

## About the AKS scheduler

In AKS, the default mechanism of workload placement across nodes within a cluster is through the scheduler. The default scheduler is a control plane component responsible for assigning AKS deployment pods to nodes. Once the AKS scheduler selects a node, the deployment pod is bound to it, and the rest of the lifecycle continues.

When a pod is created without a specified node, the scheduler selects an optimal node based on several criteria, including (but not limited to):

- Available resources (CPU, memory)
[Node affinity/anti-affinity](operator-best-practices-advanced-scheduler#node-affinity)[Pod affinity/anti-affinity](operator-best-practices-advanced-scheduler#inter-pod-affinity-and-anti-affinity)[Taints and tolerations](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

### AKS scheduler configuration and scheduling strategies

By default, the AKS scheduler comes with a set of built-in rules that work well for general-purpose workloads. However, advanced use cases might require custom scheduling strategies. For example:

- Batch jobs might prefer collocating in a few nodes (for better performance) over topology-aware spreading (for reliability).
- Cost-sensitive workloads might benefit from node binpacking to consolidate jobs and minimize idle compute node costs.

To support these use cases, AKS allows you to set one or more in-tree scheduling plugins through a Kubernetes custom resource (CRD) to configure the scheduling behavior on your AKS cluster.

## Configurable scheduler profiles

A scheduler profile is a set of one or more in-tree scheduling plugins and configurations that dictate how to schedule a pod. Previously, AKS managed the scheduler configuration, and it wasn't accessible to users. Starting from Kubernetes version `1.33`

, you can now configure and set a scheduler profile (preview) for the Kubernetes scheduler on your cluster.

Each scheduler profile has the following components:

- A unique name.
- A set of
[scheduling plugins](#supported-in-tree-scheduling-plugins). - Custom arguments for fine-grained behavior (applicable to certain plugins).

## Supported in-tree scheduling plugins

AKS supports configuration of 18 in-tree Kubernetes scheduling plugins that allow pods to be placed on specific nodes, ensure pods are matched with specific storage resources, optimize for nodes with container images, and more.

The following sections walk you through these plugins, which are grouped into the following categories:

[Scheduling constraints and order-based plugins](#scheduling-constraints-and-order-based-plugins)[Node selection constraints scheduling plugins](#node-selection-constraints-scheduling-plugins)[Resource and topology optimization scheduling plugins](#resource-and-topology-optimization-scheduling-plugins)

To learn more about these plugins and configuration options, see the [Kubernetes Scheduling Plugin documentation](https://kubernetes.io/docs/reference/scheduling/config/#scheduling-plugins).

### Scheduling constraints and order-based plugins

`DefaultBinder`

: Responsible for binding the pod to a node after the scheduler selects a suitable node. Once the node is selected, the`DefaultBinder`

creates a binding object to ensure the pod is scheduled onto that node.`DefaultPreemption`

: Handles preemption, which is the process of evicting lower-priority pods to make room for higher-priority pods. If a pod can't be scheduled because there aren’t enough resources on the node, this plugin preempts other pods to make space. This plugin can receive the following arguments:`PodPriority`

: Defines the priority of the pod being scheduled.`PreemptionPolicy`

: The policy for handling pod preemption (for example:`"PreemptLowerPriority"`

or`"DoNotPreempt"`

).`PodPriorityClass`

: The priority class associated with the pod.`PodInfo`

: Information about the pods that are candidates for preemption.`Node`

: Information about the node on which preemption is considered.

`SchedulingGates`

: Introduces the concept of scheduling gates, which are conditions that must be satisfied before a pod is scheduled. For example, it can enforce the completion of certain tasks or operations before the scheduler attempts to schedule a pod.`PrioritySort`

: Sorts the list of pods according to their priority class. Pods with higher priority are scheduled first. It helps with the preemption decision-making and determines which pods to consider for priority scheduling.

### Node selection constraints scheduling plugins

`InterPodAffinity`

: Takes into account*affinity*rules specified by the user that influences scheduling based on the proximity of other pods. If a pod has affinity rules, it tries to schedule the pod on the same node or in the same topology as other pods that it has an affinity for (for example: for performance reasons or tight coupling). This plugin can receive the following arguments:`Affinity`

: Defines required or preferred affinity rules for the pod, which specifies other pods that the pod should or shouldn't be scheduled nearby.`TopologyKey`

: The key representing the failure domain to which the affinity rule applies (for example:`"kubernetes.io/hostname"`

for node-level affinity or`"topology.kubernetes.io/zone"`

for zone-level).`Weight`

: Defines how strongly the scheduler should consider a specific affinity rule.`Pod`

: The pod being scheduled.`OtherPods`

: List of other pods to consider in relation to the affinity rules.

`NodeAffinity`

: Enables scheduling based on node labels. It allows users to specify rules for which nodes a pod can be scheduled on based on the node's labels and provides fine-grained control over pod placement on nodes. This plugin can receive the following arguments:`NodeAffinity`

: Defines the required or preferred node affinity rules, such as`requiredDuringSchedulingIgnoredDuringExecution`

or`preferredDuringSchedulingIgnoredDuringExecution`

.`NodeSelectorTerms`

: Defines the set of node labels and values that must match.`Pod`

: The pod being scheduled.`Node`

: A potential node for scheduling.`LabelSelector`

: A selector for choosing nodes based on labels.

`NodeName`

: Forces pods to be scheduled on a specific node. When you specify the exact node name, the scheduler places the pod on that node if possible.`NodePorts`

: Ensures that a pod with a service of type`NodePort`

can be scheduled on a node that has the required ports available for binding. It checks whether the node has enough resources to support the node port allocations for the service.`NodeUnschedulable`

: Ensures that pods aren't scheduled on nodes marked as*unschedulable*. If a node is tainted with`node.kubernetes.io/unschedulable`

, the scheduler doesn't place any new pods on that node.`TaintToleration`

: Checks if a pod has the required tolerations to be scheduled on a node that has taints. Taints on nodes prevent pods from being scheduled unless the pod has a matching toleration.`NodeVolumeLimits`

: Checks whether a node has exceeded its volume limit. Each node has a maximum number of volumes it can attach, and this plugin ensures that the pod isn't scheduled on a node that has already reached that supported limit.`VolumeBinding`

: Ensures that persistent volumes (PVs) are properly bound to pods. It checks whether the volume that a pod requires can be bound to a node and ensures the volume is available on the selected node. This plugin can receive the following arguments:`VolumeClaims`

: The persistent volume claims (PVCs) made by the pod being scheduled.`Node`

: The candidate node being considered for scheduling.`VolumeAvailable`

: Checks if the persistent volume is available on the node or within the appropriate zone.`Pod`

: The pod that is requesting volume binding.`StorageClass`

: The storage class associated with the persistent volume.`VolumeBindingMode`

: Defines whether the volume binding mode is`Immediate`

or`WaitForFirstConsumer`

(for delayed binding until a pod is scheduled).

`VolumeRestrictions`

: Ensures that volume restrictions (such as limitations on the number of volumes a node can have attached) are respected when scheduling a pod. It prevents scheduling a pod on a node where the volume restrictions would be violated.`VolumeZone`

: Ensures that volumes are scheduled in the same availability zone as the pod. For example, if a pod requests a volume that must be in a specific zone, the plugin ensures that both the pod and the volume are in the same zone.

### Resource and topology optimization scheduling plugins

`NodeResourcesBalancedAllocation`

: Aims to balance the resource allocation on nodes. When scheduling a pod, it considers how resources like CPU and memory are allocated across nodes to avoid overprovisioning or underutilizing resources. This plugin can receive the following arguments:`ResourceRequests`

: The resource requests (CPU, memory, etc.) of the pod being scheduled.`Node`

: A candidate node for scheduling.`NodeResources`

: The available resources (CPU, memory, etc.) of the node.`ClusterResourceUsage`

: Cluster-wide resource usage metrics to help decide the best node to balance resources.

`NodeResourcesFit`

: Checks whether a node has enough available resources (CPU, memory, etc.) to run the pod. It ensures that a pod is only scheduled on a node that has sufficient resources available. This plugin can receive the following arguments:`ResourceRequests`

: The resource requests of the pod.`Node`

: The candidate node being considered for scheduling.`NodeCapacity`

: The available capacity of resources on the node.`Pod`

: The pod being scheduled, with its resource requests.

`ImageLocality`

: Helps the scheduler decide whether to schedule a pod onto a node based on the presence of a required container image. It tries to schedule pods on nodes where the required image is already present, reducing the time needed to pull the image.`PodTopologySpread`

: Ensures that pods are spread evenly across the topology (like zones or regions) to achieve high availability and fault tolerance. It tries to avoid placing multiple replicas of a pod in the same failure domain. This plugin can receive the following arguments:`TopologySpreadConstraints`

: Defines the constraints for how pods should be spread across failure domains, including the key (for example:`topology.kubernetes.io/zone`

) and the number of pods to be placed in each domain.`Pod`

: The pod being scheduled.`FailureDomain`

: The failure domain key (for example: zone or region).`PodAffinity`

: Information about pod affinity, which could also impact how the pods are distributed.`Node`

: Potential nodes for placement.`PodSpreadScore`

: Used to determine how much "spread" the pod should have across domains (higher scores indicate better spreading).


## Next step


[Configure and deploy a scheduler profile (preview) on your AKS cluster].

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-workload-identity -->

# Securely scale your applications using the KEDA add-on and workload identity on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to securely scale your applications with the Kubernetes Event-driven Autoscaling (KEDA) add-on and workload identity on Azure Kubernetes Service (AKS).

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules).

## Create a resource group

Create a resource group using the

command. Make sure you replace the placeholder values with your own values.`az group create`

`LOCATION=<azure-region> RG_NAME=<resource-group-name> az group create --name $RG_NAME --location $LOCATION`


## Create an AKS cluster

Create an AKS cluster with the KEDA add-on, workload identity, and OIDC issuer enabled using the

command with the`az aks create`

`--enable-workload-identity`

,`--enable-keda`

, and`--enable-oidc-issuer`

flags. Make sure you replace the placeholder value with your own value.`AKS_NAME=<cluster-name> az aks create \ --name $AKS_NAME \ --resource-group $RG_NAME \ --enable-workload-identity \ --enable-oidc-issuer \ --enable-keda \ --generate-ssh-keys`

Validate the deployment was successful and make sure the cluster has KEDA, workload identity, and OIDC issuer enabled using the

command with the`az aks show`

`--query`

flag set to`"[workloadAutoScalerProfile, securityProfile, oidcIssuerProfile]"`

.`az aks show \ --name $AKS_NAME \ --resource-group $RG_NAME \ --query "[workloadAutoScalerProfile, securityProfile, oidcIssuerProfile]"`

Connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --name $AKS_NAME \ --resource-group $RG_NAME \ --overwrite-existing`


## Create an Azure Service Bus

Create an Azure Service Bus namespace using the

command. Make sure to replace the placeholder value with your own value.`az servicebus namespace create`

`SB_NAME=<service-bus-name> SB_HOSTNAME="${SB_NAME}.servicebus.windows.net" az servicebus namespace create \ --name $SB_NAME \ --resource-group $RG_NAME \ --disable-local-auth`

Create an Azure Service Bus queue using the

command. Make sure to replace the placeholder value with your own value.`az servicebus queue create`

`SB_QUEUE_NAME=<service-bus-queue-name> az servicebus queue create \ --name $SB_QUEUE_NAME \ --namespace $SB_NAME \ --resource-group $RG_NAME`


## Create a managed identity

Create a managed identity using the

command. Make sure to replace the placeholder value with your own value.`az identity create`

`MI_NAME=<managed-identity-name> MI_CLIENT_ID=$(az identity create \ --name $MI_NAME \ --resource-group $RG_NAME \ --query "clientId" \ --output tsv)`

Get the OIDC issuer URL using the

command with the`az aks show`

`--query`

flag set to`oidcIssuerProfile.issuerUrl`

.`AKS_OIDC_ISSUER=$(az aks show \ --name $AKS_NAME \ --resource-group $RG_NAME \ --query oidcIssuerProfile.issuerUrl \ --output tsv)`

Create a federated credential between the managed identity and the namespace and service account used by the workload using the

command. Make sure to replace the placeholder value with your own value.`az identity federated-credential create`

`FED_WORKLOAD=<federated-credential-workload-name> az identity federated-credential create \ --name $FED_WORKLOAD \ --identity-name $MI_NAME \ --resource-group $RG_NAME \ --issuer $AKS_OIDC_ISSUER \ --subject system:serviceaccount:default:$MI_NAME \ --audience api://AzureADTokenExchange`

Create a second federated credential between the managed identity and the namespace and service account used by the keda-operator using the

command. Make sure to replace the placeholder value with your own value.`az identity federated-credential create`

`FED_KEDA=<federated-credential-keda-name> az identity federated-credential create \ --name $FED_KEDA \ --identity-name $MI_NAME \ --resource-group $RG_NAME \ --issuer $AKS_OIDC_ISSUER \ --subject system:serviceaccount:kube-system:keda-operator \ --audience api://AzureADTokenExchange`


## Create role assignments

Get the object ID for the managed identity using the

command with the`az identity show`

`--query`

flag set to`"principalId"`

.`MI_OBJECT_ID=$(az identity show \ --name $MI_NAME \ --resource-group $RG_NAME \ --query "principalId" \ --output tsv)`

Get the Service Bus namespace resource ID using the

command with the`az servicebus namespace show`

`--query`

flag set to`"id"`

.`SB_ID=$(az servicebus namespace show \ --name $SB_NAME \ --resource-group $RG_NAME \ --query "id" \ --output tsv)`

Assign the Azure Service Bus Data Owner role to the managed identity using the

command.`az role assignment create`

`az role assignment create \ --role "Azure Service Bus Data Owner" \ --assignee-object-id $MI_OBJECT_ID \ --assignee-principal-type ServicePrincipal \ --scope $SB_ID`


## Enable Workload Identity on KEDA operator

After creating the federated credential for the

`keda-operator`

ServiceAccount, you will need to manually restart the`keda-operator`

pods to ensure Workload Identity environment variables are injected into the pod.`kubectl rollout restart deploy keda-operator -n kube-system`

Confirm the keda-operator pods restart

`kubectl get pod -n kube-system -lapp=keda-operator -w`

Once you've confirmed the keda-operator pods have finished rolling hit

`Ctrl+c`

to break the previous watch command then confirm the Workload Identity environment variables have been injected.`KEDA_POD_ID=$(kubectl get po -n kube-system -l app.kubernetes.io/name=keda-operator -ojsonpath='{.items[0].metadata.name}') kubectl describe po $KEDA_POD_ID -n kube-system`

You should see output similar to the following under

**Environment**.`--- AZURE_CLIENT_ID: AZURE_TENANT_ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx AZURE_FEDERATED_TOKEN_FILE: /var/run/secrets/azure/tokens/azure-identity-token AZURE_AUTHORITY_HOST: https://login.microsoftonline.com/ ---`

Deploy a KEDA TriggerAuthentication resource that includes the User-Assigned Managed Identity's Client ID.

`kubectl apply -f - <<EOF apiVersion: keda.sh/v1alpha1 kind: TriggerAuthentication metadata: name: azure-servicebus-auth namespace: default # this must be same namespace as the ScaledObject/ScaledJob that will use it spec: podIdentity: provider: azure-workload identityId: $MI_CLIENT_ID EOF`

Note

With the TriggerAuthentication in place, KEDA will be able to authenticate via workload identity. The

`keda-operator`

Pods use the`identityId`

to authenticate against Azure resources when evaluating scaling triggers.

## Publish messages to Azure Service Bus

At this point everything is configured for scaling with KEDA and Microsoft Entra Workload Identity. We will test this by deploying producer and consumer workloads.

Create a new ServiceAccount for the workloads.

`kubectl apply -f - <<EOF apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: $MI_CLIENT_ID name: $MI_NAME EOF`

Deploy a Job to publish 100 messages.

`kubectl apply -f - <<EOF apiVersion: batch/v1 kind: Job metadata: name: myproducer spec: template: metadata: labels: azure.workload.identity/use: "true" spec: serviceAccountName: $MI_NAME containers: - image: ghcr.io/azure-samples/aks-app-samples/servicebusdemo:latest name: myproducer resources: {} env: - name: OPERATION_MODE value: "producer" - name: MESSAGE_COUNT value: "100" - name: AZURE_SERVICEBUS_QUEUE_NAME value: $SB_QUEUE_NAME - name: AZURE_SERVICEBUS_HOSTNAME value: $SB_HOSTNAME restartPolicy: Never EOF`


## Consume messages from Azure Service Bus

Now that we have published messages to the Azure Service Bus queue, we will deploy a ScaledJob to consume the messages. This ScaledJob will use the KEDA TriggerAuthentication resource to authenticate against the Azure Service Bus queue using the workload identity and scale out every 10 messages.

Deploy a ScaledJob resource to consume the messages. The scale trigger will be configured to scale out every 10 messages. The KEDA scaler will create 10 jobs to consume the 100 messages.

`kubectl apply -f - <<EOF apiVersion: keda.sh/v1alpha1 kind: ScaledJob metadata: name: myconsumer-scaledjob spec: jobTargetRef: template: metadata: labels: azure.workload.identity/use: "true" spec: serviceAccountName: $MI_NAME containers: - image: ghcr.io/azure-samples/aks-app-samples/servicebusdemo:latest name: myconsumer env: - name: OPERATION_MODE value: "consumer" - name: MESSAGE_COUNT value: "10" - name: AZURE_SERVICEBUS_QUEUE_NAME value: $SB_QUEUE_NAME - name: AZURE_SERVICEBUS_HOSTNAME value: $SB_HOSTNAME restartPolicy: Never triggers: - type: azure-servicebus metadata: queueName: $SB_QUEUE_NAME namespace: $SB_NAME messageCount: "10" authenticationRef: name: azure-servicebus-auth EOF`

Note

ScaledJob creates a Kubernetes Job resource whenever a scaling event occurs and thus a Job template needs to be passed in when creating the resource. As new Jobs are created, Pods will be deployed with workload identity bits to consume messages.

Verify the KEDA scaler worked as intended.

`kubectl describe scaledjob myconsumer-scaledjob`

You should see events similar to the following.

`Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal KEDAScalersStarted 10m scale-handler Started scalers watch Normal ScaledJobReady 10m keda-operator ScaledJob is ready for scaling Warning KEDAScalerFailed 10m scale-handler context canceled Normal KEDAJobsCreated 10m scale-handler Created 10 jobs`


## Clean up resources

After you verify that the deployment is successful, you can clean up the resources to avoid incurring Azure costs.

Delete the Azure resource group and all resources in it using the [

`az group delete`

][az-group-delete] command.`az group delete --name $RG_NAME --yes --no-wait`


## Next steps

This article showed you how to securely scale your applications using the KEDA add-on and workload identity in AKS.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more about KEDA, see the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dns-concepts -->

# DNS Resolution in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Domain Name System (DNS) resolution is a critical component in Azure Kubernetes Service (AKS), enabling pods and services to communicate using human-readable names instead of IP addresses. AKS provides built-in DNS services to ensure seamless name resolution for both internal cluster resources and external endpoints. Understanding how DNS works in AKS helps cluster operators and developers ensure reliable connectivity, optimize performance, and troubleshoot networking issues effectively.

## CoreDNS in Azure Kubernetes Service

[CoreDNS](https://coredns.io/) is the default DNS service in Azure Kubernetes Service (AKS), providing internal name resolution and service discovery for workloads running in the cluster. It operates as a set of pods in the kube-system namespace and is tightly integrated with Kubernetes networking.

When a pod in AKS issues a DNS query—such as resolving the name of another service—the request is routed to the CoreDNS pods. These pods process the query and return the appropriate IP address or forward the request to an upstream DNS server for external domains.

This architecture ensures a balance between flexibility and operational safety in a managed environment. For details on how to customize CoreDNS in AKS, refer to the [CoreDNS customization guide](coredns-custom).

For information on the CoreDNS project, see [the CoreDNS upstream project page](https://coredns.io/).

## LocalDNS in Azure Kubernetes Service

Note

This document provides an overview of what LocalDNS is and its benefits in AKS. It doesn't include setup instructions. For guidance on enabling and configuring LocalDNS, see the [LocalDNS how-to guide](localdns-custom).

### Overview

LocalDNS is an advanced feature in Azure Kubernetes Service (AKS) that deploys a Domain Name System (DNS) proxy on each node to provide highly resilient, low-latency DNS resolution. By handling DNS queries locally, this proxy reduces traffic to the CoreDNS addon pods, improving overall DNS reliability and performance in the cluster. LocalDNS is especially beneficial in large clusters or environments with high DNS query volumes, where centralized DNS resolution can become a bottleneck.

When LocalDNS is enabled, AKS deploys a local DNS cache as a `systemd`

service on each node. Pods on the node send their DNS queries to this local cache, enabling faster resolution by reducing network hops. This approach also minimizes `conntrack`

table usage, lowering the risk of table exhaustion. Additionally, if upstream DNS becomes unavailable, LocalDNS can continue serving cached responses for a configurable duration, helping maintain pod connectivity and service reliability.

### Key capabilities

**Reduced DNS resolution latency:**Each AKS node runs a LocalDNS`systemd`

service. Workloads running on the node send DNS queries to this service, which resolves them locally, reducing network hops and speeding up DNS lookups.**Customizable DNS behavior:**You can use`kubeDNSOverrides`

and`vnetDNSOverrides`

to control DNS behavior in the cluster.**Avoid conntrack races and conntrack table exhaustion:**Pods send DNS queries to the LocalDNS service on the same node without creating new`conntrack`

table entries. Skipping the connection tracking helps reduce[conntrack races](https://github.com/kubernetes/kubernetes/issues/56903)and avoids User Datagram Protocol (UDP) DNS entries from filling up`conntrack`

tables. This optimization prevents dropped and rejected connections caused by`conntrack`

table exhaustion and race conditions.**Connection upgraded to TCP:**The connection from the`localdns`

cache to the cluster’s CoreDNS service uses Transmission Control Protocol (TCP). TCP allows for connection rebalancing and removes`conntrack`

table entries when the server closes the connection (in contrast to UDP connections, which have a default 30-second timeout). Applications don't need changes, because the`localdns`

service still listens for UDP traffic.**Caching:**The LocalDNS cache plugin can be configured with serveStale and Time to Live (TTL) settings.`serveStale`

,`serveStaleDurationInSeconds`

, and`cacheDurationInSeconds`

parameters can be configured to achieve DNS resiliency, even during an upstream DNS outage.**Protocol control:**You can set the DNS query protocol (such as PreferUDP or ForceTCP) for each domain. This flexibility lets you optimize DNS traffic for specific domains or meet network requirements.

### Other benefits and considerations

| Benefits | Considerations |
|---|---|
Better scalability: Reduces load on centralized CoreDNS pods |
Minimal resource overhead: Uses a small amount of CPU and memory on each node |
Seamless integration: Does not require changes to existing application connections |
Configuration changes: Updates require node image upgrades, which can cause temporary disruptions |
Block invalid search domains: Prevents invalid DNS queries at the node level |

By using LocalDNS, you get faster and more reliable DNS resolution for your workloads, reduce the risk of DNS-related outages, and gain more control over DNS traffic in your AKS environment.

## Next steps

To learn how to enable LocalDNS and configure its settings in your AKS cluster, see the [LocalDNS how-to guide](localdns-custom).

To learn more about core network concepts, see [Network concepts for applications in AKS](concepts-network).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-concepts -->

# Advanced Container Networking Services for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services is a suite of services designed to enhance the networking capabilities of Azure Kubernetes Service (AKS) clusters. Advanced Container Networking Services offers the following key feature sets: [ Container Network Observability](#container-network-observability),

[, and](#container-network-security)

**Container Network Security**[. These features provide deep insights into network traffic, strengthen security measures, and optimize network performance for containerized applications running in AKS.](#container-network-performance)

**Container Network Performance**## Container Network Observability

Container Network Observability provides deep insights into network traffic and performance across containerized environments. This feature set **works across both Cilium and non-Cilium data planes**, offering flexibility for diverse networking needs. The feature uses eBPF to enhance scalability and performance by identifying potential bottlenecks and network congestion before applications are affected.

Key benefits of Container Network Observability include:

- Compatibility with all Container Networking Interface (CNI) variants in Azure.
, including node-level metrics and Hubble metrics for detailed network insights.*Container network metrics*- Hubble metrics for Domain Name System (DNS) resolution, pod-to-pod communication, and service interactions.
that capture essential metadata such as IPs, ports, and traffic flow for troubleshooting, monitoring, and security enforcement.*Container network logs*- Integration with the managed service for Prometheus in Azure Monitor and Azure Managed Grafana for simplified metrics storage and visualization.

### Container network metrics

This feature collects node-level metrics, including CPU, memory, and network performance, to monitor the health of cluster nodes. For deeper insights, Hubble metrics provide data on DNS resolution times, service-to-service communication, and pod-level network behavior. These metrics help you analyze application performance, detect anomalies, and optimize workloads.

For more information, see the [metrics overview](container-network-observability-metrics).

### Container network logs

Container network logs give you detailed insight into traffic within and across clusters by capturing metadata like source and destination IP addresses, ports, protocols, and flow direction. These logs enable monitoring network behavior, troubleshooting connectivity issues, and enforcing security policies. Persistent and real-time logging options ensure comprehensive, actionable network observability.

For more information, see the [container network logs overview](container-network-observability-logs).

## Container Network Security

Container Network Security enhances the security posture of AKS clusters by providing advanced network security features. It leverages eBPF technology to enforce network policies at the kernel level, ensuring efficient and effective security controls for containerized applications. **Container Network Security is available only on clusters with Azure CNI Powered by Cilium**.

### FQDN-based filtering

FQDN-based filtering allows you to create network policies based on fully qualified domain names (FQDNs) rather than IP addresses. This capability simplifies policy management, especially in dynamic environments where IP addresses frequently change. By using FQDNs, you can ensure that your applications communicate only with trusted external services, enhancing security and compliance.

For more information, see the [FQDN-based filtering overview](container-network-security-fqdn-filtering-concepts).

### Layer 7 policy

Layer 7 policy enables application-layer traffic control, allowing you to define policies based on specific application protocols. This feature provides granular control over network traffic, enabling you to enforce security policies that align with application behavior. With Layer 7 policy, you can monitor and restrict traffic based on HTTP methods, URLs, headers, and other application-level attributes.

For more information, see the [Layer 7 policy overview](container-network-security-l7-policy-concepts).

### WireGuard Encryption (preview)

WireGuard Encryption leverages the WireGuard protocol to provide secure, encrypted communication between Cilium-managed endpoints within your AKS cluster. This feature ensures that data transmitted over the network is protected from eavesdropping and tampering, enhancing the overall security of your containerized applications.

For more information, see the [WireGuard encryption overview](container-network-security-wireguard-encryption-concepts).

## Container Network Performance

Container Network Performance optimizes network performance for containerized applications running in AKS clusters. It leverages eBPF technology to enhance network routing and reduce latency, ensuring that applications can communicate efficiently and effectively. **Container Network Performance is available only on clusters with Azure CNI Powered by Cilium**.

### eBPF Host Routing

eBPF Host Routing uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in AKS clusters.

For more information, see the [eBPF Host Routing overview](container-network-performance-ebpf-host-routing).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-ingress -->

# Deploy ingress gateways for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy external or internal ingresses for the Istio service mesh add-on for Azure Kubernetes Service (AKS) cluster.

Note

When you perform a [minor revision upgrade](istio-upgrade#minor-revision-upgrades-with-ingress-and-egress-gateways) of the Istio add-on, another deployment for the external / internal gateways will be created for the new control plane revision.

## Prerequisites

This guide assumes you followed the [documentation](istio-deploy-addon) to enable the Istio add-on on an AKS cluster, deploy a sample application, and set environment variables.

## Enable external ingress gateway

Note

If you need the ingress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

Use `az aks mesh enable-ingress-gateway`

to enable an externally accessible Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type external
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-external -n aks-istio-ingress
```


Observe from the output that the external IP address of the service is a publicly accessible one:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-external LoadBalancer 10.0.10.249 <EXTERNAL_IP> 15021:30705/TCP,80:32444/TCP,443:31728/TCP 4m21s
```


Applications aren't accessible from outside the cluster by default after enabling the ingress gateway. To make an application accessible, map the sample deployment's ingress to the Istio ingress gateway using the following manifest:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-gateway-external
spec:
selector:
istio: aks-istio-ingressgateway-external
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-external
spec:
hosts:
- "*"
gateways:
- bookinfo-gateway-external
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-external`

, which can be found as label on the service mapped to the external ingress that was enabled earlier.

Set environment variables for external ingress host and ports:

```
export INGRESS_HOST_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_EXTERNAL=$INGRESS_HOST_EXTERNAL:$INGRESS_PORT_EXTERNAL
```


Retrieve the external address of the sample application:

```
echo "http://$GATEWAY_URL_EXTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is displayed. Alternatively, you can also use `curl`

to confirm the sample application is accessible. For example:

```
curl -s "http://${GATEWAY_URL_EXTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Enable internal ingress gateway

Use `az aks mesh enable-ingress-gateway`

to enable an internal Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type internal
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-internal -n aks-istio-ingress
```


Observe from the output that the external IP address of the service isn't a publicly accessible one and is instead only locally accessible:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-internal LoadBalancer 10.0.182.240 <IP> 15021:30764/TCP,80:32186/TCP,443:31713/TCP 87s
```


After enabling the ingress gateway, applications need to be exposed through the gateway, and routing rules need to be configured accordingly. Use the following manifest to map the sample deployment's ingress to the Istio ingress gateway:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-internal-gateway
spec:
selector:
istio: aks-istio-ingressgateway-internal
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-internal
spec:
hosts:
- "*"
gateways:
- bookinfo-internal-gateway
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-internal`

, which can be found as label on the service mapped to the internal ingress that was enabled earlier.

Set environment variables for internal ingress host and ports:

```
export INGRESS_HOST_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_INTERNAL=$INGRESS_HOST_INTERNAL:$INGRESS_PORT_INTERNAL
```


Retrieve the address of the sample application:

```
echo "http://$GATEWAY_URL_INTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is **NOT** displayed. Alternatively, you can also use `curl`

to confirm the sample application is **NOT** accessible. For example:

```
curl -s "http://${GATEWAY_URL_INTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Use `kubectl exec`

to confirm application is accessible from inside the cluster's virtual network:

```
kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS "http://$GATEWAY_URL_INTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Ingress gateway service customizations

### Annotations

The following annotations can be added to the Kubernetes service for the external and internal ingress gateways:

`external-dns.alpha.kubernetes.io/hostname`

: for specifying the domain for resource's DNS records. For more information, see[external-dns](https://kubernetes-sigs.github.io/external-dns/latest/docs/annotations/annotations/#external-dnsalphakubernetesiohostname).`service.beta.kubernetes.io/azure-allowed-ip-ranges`

: for specifying a list of allowed IP ranges separated by commas.`service.beta.kubernetes.io/azure-allowed-service-tags`

: for specifying which[service tags](/en-us/azure/virtual-network/service-tags-overview)the ingress gateway can receive requests from.`service.beta.kubernetes.io/azure-disable-load-balancer-floating-ip`

: set to`true`

to disable floating IP address in load balancer rule.`service.beta.kubernetes.io/azure-load-balancer-internal-subnet`

: name of subnet to bind internal ingress gateway to. This subnet must exist in the same virtual network as the mesh.`service.beta.kubernetes.io/azure-load-balancer-ipv4`

: for configuring a static IPv4 address.`service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset`

: for controlling whether Azure Load Balancer enables TCP Reset.`service.beta.kubernetes.io/azure-load-balancer-resource-group`

: for specifying the resource group of a public IP in a different resource group from the cluster.`service.beta.kubernetes.io/azure-load-balancer-tcp-idle-timeout`

: for configuring the TCP idle timeout in minutes for connections through the Azure Load Balancer.`service.beta.kubernetes.io/azure-pip-ip-tags`

: for specifying a list of IpTags separated by commas.`service.beta.kubernetes.io/azure-pip-name`

: for specifying the name of a public IP address.`service.beta.kubernetes.io/azure-shared-securityrule`

: for exposing the ingress gateway through an[augmented security rule](/en-us/azure/virtual-network/network-security-groups-overview#augmented-security-rules).

The add-on supports health probe annotations for ports 80 and 443. Learn more about the usage of ports [here](/en-us/azure/aks/load-balancer-standard#customize-the-load-balancer-health-probe).

### External traffic policy

The add-on supports customization of `.spec.externalTrafficPolicy`

in the Kubernetes service for the ingress gateway. Setting `.spec.externalTrafficPolicy`

to `Local`

preserves the client source IP at the Istio ingress gateway and avoids a second hop in the traffic path to the backend ingress gateway pods.

```
kubectl patch service aks-istio-ingressgateway-external -n aks-istio-ingress --type merge --patch '{"spec": {"externalTrafficPolicy": "Local"}}'
```


Note

Modifying the `.spec.externalTrafficPolicy`

to `Local`

risks potentially imbalanced traffic spreading. Before applying this change, it is recommended to read the [Kubernetes docs](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip) to understand the tradeoffs between the different `externalTrafficPolicy`

settings.

## Delete resources

If you want to clean up the Istio external or internal ingress gateways, but leave the mesh enabled on the cluster, run the following command:

```
az aks mesh disable-ingress-gateway --ingress-gateway-type <external/internal> --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```


## Next steps

Note

If there are any issues encountered with deploying the Istio ingress gateway or configuring ingress traffic routing, refer to [article on troubleshooting Istio add-on ingress gateways](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-ingress-gateway)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/limit-egress-traffic -->

# Limit network traffic with Azure Firewall in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use the [outbound network and fully qualified domain name (FQDN) rules for AKS clusters](outbound-rules-control-egress) to control egress traffic using Azure Firewall. To simplify this configuration, Azure Firewall provides an Azure Kubernetes Service (`AzureKubernetesService`

) FQDN tag that restricts outbound traffic from the AKS cluster.

## Firewall frontend IP requirements

**Production minimum**: Use at least 20 frontend IPs on Azure Firewall to avoid source network address translation (SNAT) port exhaustion.**High-traffic clusters**: If your cluster creates many outbound connections to the same destinations, you might need more frontend IPs to avoid maxing out ports per IP**API server protection**: Add the firewall's public frontend IP to[API server authorized IP ranges](api-server-authorized-ip-ranges)for enhanced security**Developer access**: When using authorized IP ranges, either use a jumpbox in the firewall's virtual network (VNet) or add developer endpoint IPs to the authorized range

This guidance applies throughout the configuration process described in this article.

Note

The FQDN tag contains all the FQDNs listed in [outbound network and FQDN rules for AKS clusters](outbound-rules-control-egress) and is automatically updated.

## Architecture overview

The following diagram illustrates the architecture of an AKS cluster with restricted egress traffic using Azure Firewall:

Key components of this architecture include:

**Public ingress is forced to flow through firewall filters**:- AKS agent nodes are isolated in a dedicated subnet.
[Azure Firewall](/en-us/azure/firewall/overview)is deployed in its own subnet.- A DNAT rule translates the firewall public IP into the load balancer frontend IP.

**Outbound requests start from agent nodes to the Azure Firewall internal IP using a**:[user-defined route (UDR)](egress-outboundtype)- Requests from AKS agent nodes follow a UDR that has been placed on the subnet the AKS cluster was deployed into.
- Azure Firewall egresses out of the VNet from a public IP frontend.
- Access to the public internet or other Azure services flows to and from the firewall frontend IP address.
- You can protect access to the AKS control plane using
[API server authorized IP ranges](api-server-authorized-ip-ranges), including the firewall public frontend IP address.

**Internal traffic**:- You can use an
[internal load balancer](internal-lb)for internal traffic, which you could isolate on its own subnet, instead of or alongside a[public load balancer](load-balancer-standard).

- You can use an

## Configure environment variables

The following table lists the environment variables used in this article. Set these variables in your shell before proceeding, or modify the commands to use your own values.

| Variable | Description | Example value |
|---|---|---|
`PREFIX` |
Prefix for resource names | `aks-egress` |
`RESOURCE_GROUP` |
Name of the resource group | `aks-egress-rg` |
`LOCATION` |
Azure region for resources | `eastus` |
`PLUGIN` |
Network plugin for AKS | `azure` |
`CLUSTER_NAME` |
Name of the AKS cluster | `aks-egress` |
`VNET_NAME` |
Name of the virtual network | `aks-egress-vnet` |
`AKS_SUBNET_NAME` |
Name of the subnet for AKS | `aks-subnet` |
`FW_SUBNET_NAME` |
Name of the subnet for Azure Firewall | `AzureFirewallSubnet` |
`FW_NAME` |
Name of the Azure Firewall | `aks-egress-fw` |
`FW_PUBLICIP_NAME` |
Name of the public IP for Azure Firewall | `aks-egress-fwpublicip` |
`FW_IPCONFIG_NAME` |
Name of the IP configuration for Azure Firewall | `aks-egress-fwconfig` |
`FW_ROUTE_TABLE_NAME` |
Name of the route table for Azure Firewall | `aks-egress-fwrt` |
`FW_ROUTE_NAME_1` |
Name of the route for Azure Firewall | `aks-egress-fwrn` |
`FW_ROUTE_NAME_2` |
Name of the internet route for Azure Firewall | `aks-egress-fwrn-internet` |

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a virtual network with multiple subnets

Provision a VNet with two separate subnets: one for the cluster and one for the firewall. Optionally, you can create one for internal service ingress. The following diagram illustrates the empty network topology before deploying any resources:

Create a VNet using the

command.`az network vnet create`

`az network vnet create \ --resource-group $RESOURCE_GROUP \ --name $VNET_NAME \ --location $LOCATION \ --address-prefixes 10.42.0.0/16 \ --subnet-name $AKS_SUBNET_NAME \ --subnet-prefix 10.42.1.0/24`

Create a subnet for Azure Firewall using the

command.`az network vnet subnet create`

`# Dedicated subnet for Azure Firewall (subnet must be named "AzureFirewallSubnet") az network vnet subnet create \ --resource-group $RESOURCE_GROUP \ --vnet-name $VNET_NAME \ --name $FW_SUBNET_NAME \ --address-prefix 10.42.2.0/24`


## Create a public IP for Azure Firewall

Create a standard SKU public IP resource using the

command. This resource is used as the frontend IP address for the Azure Firewall.`az network public-ip create`

`az network public-ip create --resource-group $RESOURCE_GROUP --name $FW_PUBLICIP_NAME --location $LOCATION --sku "Standard"`


## Install the Azure Firewall CLI extension

Register the

[Azure Firewall CLI extension](https://github.com/Azure/azure-cli-extensions/tree/main/src/azure-firewall)to create an Azure Firewall using thecommand.`az extension add`

`az extension add --name azure-firewall`


## Create an Azure Firewall and enable DNS proxy

Note

For high-traffic scenarios, see the [firewall frontend IP requirements](#firewall-frontend-ip-requirements) section.

For more information on how to create an Azure Firewall with multiple IPs, see [Create an Azure Firewall with multiple public IP addresses using Bicep](/en-us/azure/firewall/quick-create-multiple-ip-bicep).

Create an Azure Firewall and enable DNS proxy using the

command with`az network firewall create`

`--enable-dns-proxy`

set to`true`

.`az network firewall create --resource-group $RESOURCE_GROUP --name $FW_NAME --location $LOCATION --enable-dns-proxy true`

Setting up the public IP address to the Azure Firewall might take a few minutes. Once it's ready, you can assign the IP address to the firewall front end.

Note

To use FQDN on network rules, you need DNS proxy enabled. When DNS proxy is enabled, the firewall listens on port 53 and forwards DNS requests to the DNS server you specify. This setting allows the firewall to automatically translate the FQDN.


## Create an IP configuration for Azure Firewall

Create an Azure Firewall IP configuration using the

command.`az network firewall ip-config create`

`az network firewall ip-config create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --name $FW_IPCONFIG_NAME --public-ip-address $FW_PUBLICIP_NAME --vnet-name $VNET_NAME`


## Get the Azure Firewall IP addresses

Save the public and private firewall frontend IP addresses for configuration later using the following commands:

`export FW_PUBLIC_IP=$(az network public-ip show --resource-group $RESOURCE_GROUP --name $FW_PUBLICIP_NAME --query "ipAddress" -o tsv) export FW_PRIVATE_IP=$(az network firewall show --resource-group $RESOURCE_GROUP --name $FW_NAME --query "ipConfigurations[0].privateIPAddress" -o tsv)`

Note

For API server security, see the

[firewall frontend IP requirements](#firewall-frontend-ip-requirements)section.

## UDR configuration for AKS egress through Azure Firewall

Azure automatically routes traffic between Azure subnets, VNets, and on-premises networks. To modify default routing, create a route table with the following requirements:

**Required route parameters**:

**Route destination**:`0.0.0.0/0`

(all traffic)**Next hop type**: Network virtual appliance (NVA)**Next hop IP**: Azure Firewall private IP address**Association**: One route table per subnet (*zero*or*one*allowed)

**UDR constraints**:

- Default internet route (
`0.0.0.0/0`

) already exists but requires public IP for SNAT. - Route must point to gateway/NVA, not directly to internet.
- AKS validates route configuration and prevents direct internet routes.
- Each subnet supports maximum of
*one*associated route table.

**Outbound type impact**:

**UDR (**: No load balancer public IP created for outbound requests.`userDefinedRouting`

)**Load Balancer public IP**: Only created for inbound requests with`LoadBalancer`

service type.**SNAT configuration**: Requires proper public IP configuration for outbound connectivity.

For more information, see [Outbound rules for Azure Load Balancer](/en-us/azure/load-balancer/outbound-rules#scenario6out).

## Create a route with a hop to Azure Firewall

Create an empty route table using the

command. The route table defines the Azure Firewall as the next hop. Each subnet can have`az network route-table create`

*zero*or*one*route table associated to it.`az network route-table create --resource-group $RESOURCE_GROUP --location $LOCATION --name $FW_ROUTE_TABLE_NAME`

Create routes in the route table for the subnets using the

command.`az network route-table route create`

`az network route-table route create --resource-group $RESOURCE_GROUP --name $FW_ROUTE_NAME_1 --route-table-name $FW_ROUTE_TABLE_NAME --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address $FW_PRIVATE_IP az network route-table route create --resource-group $RESOURCE_GROUP --name $FW_ROUTE_NAME_2 --route-table-name $FW_ROUTE_TABLE_NAME --address-prefix $FW_PUBLIC_IP/32 --next-hop-type Internet`


For information on how to override Azure's default system routes or add more routes to a subnet's route table, see the [Virtual network route table documentation](/en-us/azure/virtual-network/virtual-networks-udr-overview#user-defined).

## Azure Firewall outbound rules for AKS

Note

For applications outside of the `kube-system`

or `gatekeeper-system`

namespaces that need to talk to the API server, an extra network rule to allow TCP communication to port 443 for the API server IP in addition to adding application rule for `fqdn-tag`

of `AzureKubernetesService`

is required.

The following network rules are required for AKS egress traffic control through Azure Firewall:

- The first network rule allows access to port 9000 via TCP.
- The second network rule allows access to port 1194 via UDP. If you're deploying to Microsoft Azure operated by 21Vianet, see the
[Azure operated by 21Vianet required network rules](outbound-rules-control-egress#microsoft-azure-operated-by-21vianet-required-network-rules). In this article, the commands use the`AzureCloud.$LOCATION`

service tag as the destination address. Service tags represent groups of IP address prefixes for Azure services in specific regions. This automatically includes the appropriate CIDR ranges for Azure services without requiring manual IP range specification. - The third network rule opens port 123 to
`ntp.ubuntu.com`

FQDN via UDP. Adding an FQDN as a network rule is one of the specific features of Azure Firewall, so you need to adapt it when using your own options. - The fourth and fifth network rules allow access to pull containers from GitHub Container Registry (
`ghcr.io`

) and Docker Hub (`docker.io`

).

## Create network rules on Azure Firewall

Create the network rules using the following

commands.`az network firewall network-rule create`

`az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'apitcp' --protocols 'TCP' --source-addresses '*' --destination-addresses "AzureCloud.$LOCATION" --destination-ports 9000 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'apiudp' --protocols 'UDP' --source-addresses '*' --destination-addresses "AzureCloud.$LOCATION" --destination-ports 1194 --action allow --priority 100 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'time' --protocols 'UDP' --source-addresses '*' --destination-fqdns 'ntp.ubuntu.com' --destination-ports 123 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'ghcr' --protocols 'TCP' --source-addresses '*' --destination-fqdns ghcr.io pkg-containers.githubusercontent.com --destination-ports '443' az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'docker' --protocols 'TCP' --source-addresses '*' --destination-fqdns docker.io registry-1.docker.io production.cloudflare.docker.com --destination-ports '443'`


## Create application rules on Azure Firewall

Create the application rule using the

command.`az network firewall application-rule create`

`az network firewall application-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwar' --name 'fqdn' --source-addresses '*' --protocols 'http=80' 'https=443' --fqdn-tags "AzureKubernetesService" --action allow --priority 100`


To learn more about Azure Firewall, see the [Azure Firewall documentation](/en-us/azure/firewall/overview).

## Associate the route table to AKS

To associate the cluster with the firewall, the dedicated subnet for the cluster's subnet must reference the route table.

Associate the route table to AKS using the

command.`az network vnet subnet update`

`az network vnet subnet update --resource-group $RESOURCE_GROUP --vnet-name $VNET_NAME --name $AKS_SUBNET_NAME --route-table $FW_ROUTE_TABLE_NAME`


## Deploy an AKS cluster that follows your outbound rules

You can now deploy an AKS cluster into the existing VNet. You use the [ userDefinedRouting outbound type](egress-outboundtype), which ensures that any outbound traffic is forced through the firewall and no other egress paths exist. You can also use the

[.](egress-outboundtype#outbound-type-of-loadbalancer)

`loadBalancer`

outbound typeSet an environment variable for the subnet ID of the target subnet using the following command:

`SUBNET_ID=$(az network vnet subnet show --resource-group $RESOURCE_GROUP --vnet-name $VNET_NAME --name $AKS_SUBNET_NAME --query id -o tsv)`


You define the outbound type to use the UDR that already exists on the subnet. This configuration enables AKS to skip the setup and IP provisioning for the load balancer.

Tip

You can add extra features to the cluster deployment, such as [ private clusters](private-clusters).

For API server authorized IP ranges setup and developer access considerations, see the [firewall frontend IP requirements](#firewall-frontend-ip-requirements) section.

## Create an AKS cluster with system-assigned identities

Note

AKS creates a system-assigned kubelet identity in the node resource group if you don't [specify your own kubelet managed identity](use-managed-identity#create-a-kubelet-managed-identity).

For user-defined routing, system-assigned identity only supports the CNI network plugin.

Create an AKS cluster using a system-assigned managed identity with the CNI network plugin using the

command.`az aks create`

`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --location $LOCATION \ --node-count 3 \ --network-plugin azure \ --outbound-type userDefinedRouting \ --vnet-subnet-id $SUBNET_ID \ --api-server-authorized-ip-ranges $FW_PUBLIC_IP \ --generate-ssh-keys`


## Create user-assigned identities

If you don't have user-assigned identities, follow the steps in this section. If you already have user-assigned identities, skip to [Create an AKS cluster with user-assigned identities](#create-an-aks-cluster-with-user-assigned-identities).

Create a managed identity using the

command.`az identity create`

`az identity create --name myIdentity --resource-group $RESOURCE_GROUP`

The output should resemble the following example output:

`{ ... "id": "/subscriptions/<subscriptionid>/resourcegroups/aks-egress-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "eastus", "name": "myIdentity", ... "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`

Create a kubelet managed identity using the

command.`az identity create`

`az identity create --name myKubeletIdentity --resource-group $RESOURCE_GROUP`

The output should resemble the following example output:

`{ ... "id": "/subscriptions/<subscriptionid>/resourcegroups/aks-egress-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myKubeletIdentity", "location": "eastus", "name": "myKubeletIdentity", ... "resourceGroup": "aks-egress-rg", ... "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


Note

If you create your own VNet and route table where the resources are outside of the worker node resource group, the CLI automatically adds the role assignment. If you're using an ARM template or other method, you need to use the principal ID of the cluster managed identity to perform a [role assignment](use-managed-identity#add-a-role-assignment-for-a-system-assigned-managed-identity).

## Create an AKS cluster with user-assigned identities

Create an AKS cluster with your existing user-assigned managed identities in the subnet using the

command. Provide the resource ID of the managed identity for the control plane and the resource ID of the kubelet identity.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --location $LOCATION \ --node-count 3 \ --network-plugin kubenet \ --outbound-type userDefinedRouting \ --vnet-subnet-id $SUBNET_ID \ --api-server-authorized-ip-ranges $FW_PUBLIC_IP \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id> \ --generate-ssh-keys`


## Enable developer access to the API server

If you used authorized IP ranges for your cluster in the previous step, you need to add your developer tooling IP addresses to the AKS cluster list of approved IP ranges so you access the API server from there. You can also configure a jumpbox with the needed tooling inside a separate subnet in the firewall's VNet.

Retrieve your IP address using the following command:

`CURRENT_IP=$(dig @resolver1.opendns.com ANY myip.opendns.com +short)`

Add the IP address to the approved ranges using the

command.`az aks update`

`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --api-server-authorized-ip-ranges $CURRENT_IP/32`


## Connect to the AKS cluster

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Deploy a public service on AKS

You can now start exposing services and deploying applications to this cluster. This example exposes a public service, but you also might want to expose an internal service using an [internal load balancer](internal-lb).

Review the

[AKS Store Demo quickstart](https://github.com/Azure-Samples/aks-store-demo/blob/main/aks-store-quickstart.yaml)manifest to understand the deployed components.Deploy the service using the

`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-quickstart.yaml`


## Get the load balancer internal IP and service IP

Get the internal IP address assigned to the load balancer using the

`kubectl get services`

command.`kubectl get services`

The IP address should be listed in the

`EXTERNAL-IP`

column, as shown in the following example output:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE kubernetes ClusterIP 10.0.0.1 <none> 443/TCP 9m10s order-service ClusterIP 10.0.104.144 <none> 3000/TCP 11s product-service ClusterIP 10.0.237.60 <none> 3002/TCP 10s rabbitmq ClusterIP 10.0.161.128 <none> 5672/TCP,15672/TCP 11s store-front LoadBalancer 10.0.89.139 20.39.18.6 80:32271/TCP 10s`

Get the service IP using the

`kubectl get svc store-front`

command.`SERVICE_IP=$(kubectl get svc store-front -o jsonpath='{.status.loadBalancer.ingress[*].ip}')`


## Create a DNAT rule on Azure Firewall

Important

When you use Azure Firewall to restrict egress traffic and create a UDR to force all egress traffic, make sure you create an appropriate DNAT rule in Azure Firewall to correctly allow ingress traffic. Using Azure Firewall with a UDR breaks the ingress setup due to asymmetric routing. The issue occurs if the AKS subnet has a default route that goes to the firewall's private IP address, but you're using a public load balancer - ingress or Kubernetes service of type `loadBalancer`

. In this case, the incoming load balancer traffic is received via its public IP address, but the return path goes through the firewall's private IP address. Because the firewall is stateful, it drops the returning packet because the firewall isn't aware of an established session. To learn how to integrate Azure Firewall with your ingress or service load balancer, see [Integrate Azure Firewall with Azure Standard Load Balancer](/en-us/azure/firewall/integrate-lb).

To configure inbound connectivity, you need to write a DNAT rule to the Azure Firewall. To test connectivity to your cluster, a rule is defined for the firewall frontend public IP address to route to the internal IP exposed by the internal service. You can customize the destination address. The translated address must be the IP address of the internal load balancer. The translated port must be the exposed port for your Kubernetes service. You also need to specify the internal IP address assigned to the load balancer created by the Kubernetes service.

Add the NAT rule using the

command.`az network firewall nat-rule create`

`az network firewall nat-rule create --collection-name exampleset --destination-addresses $FW_PUBLIC_IP --destination-ports 80 --firewall-name $FW_NAME --name inboundrule --protocols Any --resource-group $RESOURCE_GROUP --source-addresses '*' --translated-port 80 --action Dnat --priority 100 --translated-address $SERVICE_IP`


## Validate connectivity

Navigate to the Azure Firewall frontend IP address in a browser to validate connectivity. You should see the AKS store app. In this example, the firewall public IP was

`52.253.228.132`

:, you can view products, add them to your cart, and then place an order.


## Clean up resources

If you no longer need the resources created in this article, you can delete them to avoid incurring future costs.

Delete the AKS resource group using the

command.`az group delete`

`az group delete --name $RESOURCE_GROUP`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/advanced-container-networking-services-overview -->

# Advanced Container Networking Services for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services is a suite of services designed to enhance the networking capabilities of Azure Kubernetes Service (AKS) clusters. Advanced Container Networking Services offers the following key feature sets: [ Container Network Observability](#container-network-observability),

[, and](#container-network-security)

**Container Network Security**[. These features provide deep insights into network traffic, strengthen security measures, and optimize network performance for containerized applications running in AKS.](#container-network-performance)

**Container Network Performance**## Container Network Observability

Container Network Observability provides deep insights into network traffic and performance across containerized environments. This feature set **works across both Cilium and non-Cilium data planes**, offering flexibility for diverse networking needs. The feature uses eBPF to enhance scalability and performance by identifying potential bottlenecks and network congestion before applications are affected.

Key benefits of Container Network Observability include:

- Compatibility with all Container Networking Interface (CNI) variants in Azure.
, including node-level metrics and Hubble metrics for detailed network insights.*Container network metrics*- Hubble metrics for Domain Name System (DNS) resolution, pod-to-pod communication, and service interactions.
that capture essential metadata such as IPs, ports, and traffic flow for troubleshooting, monitoring, and security enforcement.*Container network logs*- Integration with the managed service for Prometheus in Azure Monitor and Azure Managed Grafana for simplified metrics storage and visualization.

### Container network metrics

This feature collects node-level metrics, including CPU, memory, and network performance, to monitor the health of cluster nodes. For deeper insights, Hubble metrics provide data on DNS resolution times, service-to-service communication, and pod-level network behavior. These metrics help you analyze application performance, detect anomalies, and optimize workloads.

For more information, see the [metrics overview](container-network-observability-metrics).

### Container network logs

Container network logs give you detailed insight into traffic within and across clusters by capturing metadata like source and destination IP addresses, ports, protocols, and flow direction. These logs enable monitoring network behavior, troubleshooting connectivity issues, and enforcing security policies. Persistent and real-time logging options ensure comprehensive, actionable network observability.

For more information, see the [container network logs overview](container-network-observability-logs).

## Container Network Security

Container Network Security enhances the security posture of AKS clusters by providing advanced network security features. It leverages eBPF technology to enforce network policies at the kernel level, ensuring efficient and effective security controls for containerized applications. **Container Network Security is available only on clusters with Azure CNI Powered by Cilium**.

### FQDN-based filtering

FQDN-based filtering allows you to create network policies based on fully qualified domain names (FQDNs) rather than IP addresses. This capability simplifies policy management, especially in dynamic environments where IP addresses frequently change. By using FQDNs, you can ensure that your applications communicate only with trusted external services, enhancing security and compliance.

For more information, see the [FQDN-based filtering overview](container-network-security-fqdn-filtering-concepts).

### Layer 7 policy

Layer 7 policy enables application-layer traffic control, allowing you to define policies based on specific application protocols. This feature provides granular control over network traffic, enabling you to enforce security policies that align with application behavior. With Layer 7 policy, you can monitor and restrict traffic based on HTTP methods, URLs, headers, and other application-level attributes.

For more information, see the [Layer 7 policy overview](container-network-security-l7-policy-concepts).

### WireGuard Encryption (preview)

WireGuard Encryption leverages the WireGuard protocol to provide secure, encrypted communication between Cilium-managed endpoints within your AKS cluster. This feature ensures that data transmitted over the network is protected from eavesdropping and tampering, enhancing the overall security of your containerized applications.

For more information, see the [WireGuard encryption overview](container-network-security-wireguard-encryption-concepts).

## Container Network Performance

Container Network Performance optimizes network performance for containerized applications running in AKS clusters. It leverages eBPF technology to enhance network routing and reduce latency, ensuring that applications can communicate efficiently and effectively. **Container Network Performance is available only on clusters with Azure CNI Powered by Cilium**.

### eBPF Host Routing

eBPF Host Routing uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in AKS clusters.

For more information, see the [eBPF Host Routing overview](container-network-performance-ebpf-host-routing).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-pool-unique-subnet -->

# Create node pools with unique subnets in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Certain workloads might require splitting cluster nodes into separate pools for logical isolation. Separate subnets dedicated to each node pool in the cluster can help support this isolation, which can address requirements such as having noncontiguous virtual network address space to split across node pools.

In this article, you learn how to create node pools with unique subnets in Azure Kubernetes Service (AKS).

## Prerequisites

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.35.0 or later. Run`az version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).- An existing AKS cluster with a system node pool. If you need to create one, see
[Create an AKS cluster with a single node pool](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli).

## Limitations

- All subnets assigned to node pools must belong to the same virtual network (VNet).
- System pods must have access to all nodes and pods in the cluster to provide critical functionality, such as DNS resolution and tunneling kubectl logs/exec/port-forward proxy.
- If you expand your VNet after creating the cluster, you must update your cluster before adding a subnet outside the original CIDR block. While AKS errors out on the agent pool add, the
`aks-preview`

Azure CLI extension (version 0.5.66 and higher) now supports running`az aks update`

command with only the required`--resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

arguments. This command performs an update operation without making any changes, which can recover a cluster stuck in a failed state. - In clusters with Kubernetes version less than 1.23.3, kube-proxy SNATs traffic from new subnets, which can cause Azure Network Policy to drop the packets.
- Windows nodes SNAT traffic to the new subnets until the node pool is reimaged.
- Internal load balancers default to one of the node pool subnets.

## Add a node pool with a unique subnet

Add a node pool with a unique subnet into your existing AKS cluster using the

command and the`az aks nodepool add`

`--vnet-subnet-id`

parameter specified.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 3 \ --vnet-subnet-id $SUBNET_RESOURCE_ID`


## Next steps

For more information about node pools in AKS, see [Manage node pools for a cluster in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-services -->

# Kubernetes Services in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use Kubernetes Services to logically group pods and provide network connectivity by allowing direct access to them through a specific IP address or DNS name on a designated port. This allows you to expose your application workloads to other services within the cluster or to external clients without having to manually manage the network configuration for each pod hosting a workload.

You can specify what kind of service you want using Kubernetes *Service type values*. For more information, see the

[Kubernetes Service documentation](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types).

The following Service types are available in AKS: [ ClusterIP](#clusterip),

[,](#nodeport)

`NodePort`

[, and](#loadbalancer)

`LoadBalancer`

[.](#externalname)

`ExternalName`

## ClusterIP

`ClusterIP`

creates an internal IP address for use within the AKS cluster. The `ClusterIP`

Service is good for *internal-only applications* that support other workloads within the cluster. ClusterIP is used by default if you don't explicitly specify a type for a Service.


## NodePort

`NodePort`

creates a port mapping on the underlying node that allows the application to be accessed directly with the node IP address and port.


## LoadBalancer

`LoadBalancer`

creates an Azure load balancer resource, configures an external IP address, and connects the requested pods to the load balancer backend pool. To allow customer traffic to reach the application, load balancing rules are created on the desired ports.


For HTTP load balancing of inbound traffic, you can also use an [Ingress controller](concepts-network-ingress#ingress-controllers).

You can also use the `LoadBalancer`

type to create multiple public load balancers in a single AKS cluster. This is useful for large clusters or port-heavy workloads that can quickly exhaust the limits of a single load balancer. For more information, see [Use multiple public load balancers in Azure Kubernetes Service (preview)](use-multiple-standard-load-balancer).

## ExternalName

`ExternalName`

creates a specific DNS entry for easier application access. You can dynamically assign the load balancers and service IP address, or you can specify an existing static IP address. You can assign both internal and external static IP addresses. Existing static IP addresses are often tied to a DNS entry.

You can create both *internal* and *external* load balancers. Internal load balancers are only assigned a private IP address, so they can't be accessed from the Internet.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-oidc-issuer -->

# Create an OpenID Connect provider on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to create and manage an OpenID Connect (OIDC) provider for your Azure Kubernetes Service (AKS) cluster. The OIDC issuer allows your AKS cluster to integrate with identity providers like Microsoft Entra ID, enabling secure authentication and single sign-on (SSO) capabilities for applications running within the cluster.

## About OpenID Connect (OIDC) on AKS

[OpenID Connect](/en-us/azure/active-directory/fundamentals/auth-oidc) (OIDC) extends the OAuth 2.0 authorization protocol for use as another authentication protocol issued by Microsoft Entra ID. You can use OIDC to enable single sign-on (SSO) between OAuth-enabled applications on your Azure Kubernetes Service (AKS) cluster using a security token called an ID token. You can enable the OIDC issuer on your AKS clusters, which allows Microsoft Entra ID (or another cloud provider's identity and access management platform) to discover the API server's public signing keys.

## Prerequisites

**Platform requirements**:

- Azure CLI version 2.42.0+ (
`az --version`

to check version,[install or upgrade Azure CLI](/en-us/cli/azure/install-azure-cli)if needed) - Minimum Kubernetes version is 1.22+

**Version-specific behavior**:

- OIDC issuer enabled by default (no
`--enable-oidc-issuer`

flag needed) for Kubernetes version 1.34+ - Token auto-extension disabled (
`--service-account-extend-token-expiration=false`

) for Kubernetes version 1.30.0+ - Manual enablement required if not previously configured for Kubernetes version earlier than 1.34

**Important considerations**:

- You can't disable OIDC issuer once enabled
- Enabling OIDC issuer on existing clusters requires API server restart (brief downtime)
- Maximum token lifetime is 24 hours (one day)
- Projected service account tokens required for Kubernetes 1.30+ clusters

## Create an AKS cluster with the OIDC issuer

Create an AKS cluster using the

command with the`az aks create`

`--enable-oidc-issuer`

parameter.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster with OIDC issuer enabled (OIDC issuer enabled by default for Kubernetes 1.34+) az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --enable-oidc-issuer \ --generate-ssh-keys`


## Enable the OIDC issuer on an existing AKS cluster

Enable the OIDC issuer on an existing AKS cluster using the

command with the`az aks update`

`--enable-oidc-issuer`

parameter.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Enable the OIDC issuer on the existing AKS cluster az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-oidc-issuer`


## Get the OIDC issuer URL

Get the OIDC issuer URL using the

command.`az aks show`

`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Get the OIDC issuer URL az aks show \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --query "oidcIssuerProfile.issuerUrl" \ -o tsv`

By default, the issuer is set to use the base URL

`https://{region}.oic.prod-aks.azure.com`

, where the value for`{region}`

matches the location the AKS cluster is deployed in.

## Rotate the OIDC key

Important

Keep the following considerations in mind when rotating the OIDC key:

- If you want to invalidate the old key immediately after key rotation, you must rotate the OIDC key twice and restart the pods using projected service account tokens.
- Both old and new keys remain valid for 24 hours after rotation.
- Manual token refresh required every 24 hours (unless using
[Azure Identity SDK](workload-identity-overview#azure-identity-client-libraries), which rotates automatically).

Rotate the OIDC key using the

command.`az aks oidc-issuer`

`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Rotate the OIDC signing keys az aks oidc-issuer rotate-signing-keys \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP`


## Get the discovery document

Navigate to your

[OIDC issuer URL](#get-the-oidc-issuer-url)in your browser and append`/.well-known/openid-configuration`

to the URL. For example:`https://eastus.oic.prod-aks.azure.com/.well-known/openid-configuration`

.Your output should resemble the following example output:

`{ "issuer": "https://eastus.oic.prod-aks.azure.com/ffffffff-eeee-dddd-cccc-bbbbbbbbbbb0/00000000-0000-0000-0000-000000000000/", "jwks_uri": "https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/openid/v1/jwks", "response_types_supported": [ "id_token" ], "subject_types_supported": [ "public" ], "id_token_signing_alg_values_supported": [ "RS256" ] }`


## Get the JWK Set document

Navigate to the

in your browser. For example:**jwks_uri**from the discovery document`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/openid/v1/jwks`

.Your output should resemble the following example output:

`{ "keys": [ { "use": "sig", "kty": "RSA", "kid": "xxx", "alg": "RS256", "n": "xxxx", "e": "AQAB" }, { "use": "sig", "kty": "RSA", "kid": "xxx", "alg": "RS256", "n": "xxxx", "e": "AQAB" } ] }`

Note

During key rotation, there's one other key present in the discovery document.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-scale -->

# Tutorial - Scale applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you followed the previous tutorials, you have a working Kubernetes cluster and Azure Store Front app.

In this tutorial, you scale out the pods in the app, try pod autoscaling, and scale the number of Azure VM nodes to change the cluster's capacity for hosting workloads. You learn how to:

- Scale the Kubernetes nodes.
- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created an AKS cluster, deployed an application, and used Azure Service Bus to redeploy an updated application. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Manually scale pods

View the pods in your cluster using the

command.`kubectl get`

`kubectl get pods`

The following example output shows the pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE order-service-848767080-tf34m 1/1 Running 0 31m product-service-4019737227-2q2qz 1/1 Running 0 31m store-front-2606967446-2q2qz 1/1 Running 0 31m`

Manually change the number of pods in the

*store-front*deployment using thecommand.`kubectl scale`

`kubectl scale --replicas=5 deployment.apps/store-front`

Verify the additional pods were created using the

command.`kubectl get pods`

`kubectl get pods --selector app=store-front`

The following example output shows the additional pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE store-front-3309479140-2hfh0 1/1 Running 0 3m store-front-3309479140-bzt05 1/1 Running 0 3m store-front-3309479140-fvcvm 1/1 Running 0 3m store-front-3309479140-hrbf2 1/1 Running 0 15m store-front-3309479140-qphz8 1/1 Running 0 3m`


## Autoscale pods

To use the horizontal pod autoscaler, all containers must have defined CPU requests and limits, and pods must have specified requests. In the `aks-store-quickstart`

deployment, the *front-end* container requests 1m CPU with a limit of 1000m CPU.

These resource requests and limits are defined for each container, as shown in the following condensed example YAML:

```
...
containers:
- name: store-front
image: ghcr.io/azure-samples/aks-store-demo/store-front:latest
ports:
- containerPort: 8080
name: store-front
...
resources:
requests:
cpu: 1m
...
limits:
cpu: 1000m
...
```


### Autoscale pods using a manifest file

Create a manifest file to define the autoscaler behavior and resource limits, as shown in the following condensed example manifest file

`aks-store-quickstart-hpa.yaml`

:`apiVersion: autoscaling/v2 kind: HorizontalPodAutoscaler metadata: name: store-front-hpa spec: maxReplicas: 10 # define max replica count minReplicas: 3 # define min replica count scaleTargetRef: apiVersion: apps/v1 kind: Deployment name: store-front metrics: - type: Resource resource: name: cpu target: type: Utilization averageUtilization: 50`

Apply the autoscaler manifest file using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart-hpa.yaml`

Check the status of the autoscaler using the

`kubectl get hpa`

command.`kubectl get hpa`

After a few minutes, with minimal load on the Azure Store Front app, the number of pod replicas decreases to three. You can use

`kubectl get pods`

command again to see the unneeded pods being removed.

Note

You can enable the Kubernetes-based Event-Driven Autoscaler (KEDA) AKS add-on to your cluster to drive scaling based on the number of events needing to be processed. For more information, see [Enable simplified application autoscaling with the Kubernetes Event-Driven Autoscaling (KEDA) add-on (Preview)](keda-about).

## Manually scale AKS nodes

If you created your Kubernetes cluster using the commands in the previous tutorials, your cluster has two nodes. If you want to increase or decrease this amount, you can manually adjust the number of nodes.

The following example increases the number of nodes to three in the Kubernetes cluster named *myAKSCluster*. The command takes a couple of minutes to complete.

Scale your cluster nodes using the

command.`az aks scale`

`az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 3`

Once the cluster successfully scales, your output will be similar to following example output:

`"aadProfile": null, "addonProfiles": null, "agentPoolProfiles": [ { ... "count": 3, "mode": "System", "name": "nodepool1", "osDiskSizeGb": 128, "osDiskType": "Managed", "osType": "Linux", "ports": null, "vmSize": "Standard_DS2_v2", "vnetSubnetId": null ... } ... ]`


You can also autoscale the nodes in your cluster. For more information, see [Use the cluster autoscaler with node pools](cluster-autoscaler#use-the-cluster-autoscaler-on-node-pools).

## Next steps

In this tutorial, you used different scaling features in your Kubernetes cluster. You learned how to:

- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.
- Manually scale the Kubernetes nodes.

In the next tutorial, you learn how to upgrade Kubernetes in your AKS cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/network-isolated -->

# Create a network isolated Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Organizations typically have strict security and compliance requirements to regulate egress (outbound) network traffic from a cluster to eliminate risks of data exfiltration. By default, standard SKU Azure Kubernetes Service (AKS) clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. The conceptual document on [outbound network and FQDN rules for AKS clusters](outbound-rules-control-egress) provides a list of required endpoints for the AKS cluster and its optional add-ons and features.

One common solution to restricting outbound traffic from the cluster is to use a [firewall device](limit-egress-traffic) to restrict traffic based on firewall rules. Firewall is applicable when your application requires outbound access, but when outbound requests have to be inspected and secured. Configuring a firewall manually with required egress rules and *FQDNs* is a cumbersome process especially if your only requirement is to create an isolated AKS cluster with no outbound dependencies for the cluster bootstrapping.

To reduce risk of data exfiltration, network isolated cluster allows for bootstrapping the AKS cluster without any outbound network dependencies, even for fetching cluster components/images from Microsoft Artifact Registry (MAR). The cluster operator could incrementally set up allowed outbound traffic for each scenario they want to enable. This article walks you through the steps of creating a network isolated cluster.

## Before you begin

- Read the
[conceptual overview of this feature](concepts-network-isolated), which provides an explanation of how network isolated clusters work. The overview article also:- Explains two options for private Azure Container Registry (ACR) resource used for cluster bootstrapping - AKS-managed ACR or bring-your-own ACR.
- Explains two private cluster modes for creating private access to API server -
[private link-based](private-clusters)or[API Server Vnet Integration](api-server-vnet-integration). - Explains the two outbound types for cluster egress control -
`none`

or`block`

(preview). - Describes the
[current limitations of network isolated clusters](concepts-network-isolated#limitations).


Note

Outbound type `none`

is generally available.
Outbound type`block`

is in preview.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.71.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- You should install the
`aks-preview`

Azure CLI extension version*9.0.0b2*or later if you are using outbound type`block`

(preview).- If you don't already have the
`aks-preview`

extension, install it using thecommand.`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand.`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
- Network isolated clusters are supported on AKS clusters using Kubernetes version 1.30 or higher.
- If you're choosing to use the Bring your own (BYO) Azure Container Registry (ACR) option, you need to ensure the ACR is
[Premium SKU service tier](/en-us/azure/container-registry/container-registry-skus). - If you are using a network isolated cluster configured with API Server VNet Integration, you should follow the prerequisites and guidance in this
[document](api-server-vnet-integration).

## Deploy a network isolated cluster with AKS-managed ACR

AKS creates, manages, and reconciles an ACR resource in this option. You don't need to assign any permissions or manage the ACR. AKS manages the cache rules, private link, and private endpoint used in the network isolated cluster.

### Create a network isolated cluster

When creating a network isolated AKS cluster, you can choose one of the following private cluster modes - private link-based or API Server Vnet Integration.

Regardless of the mode you select, you should set `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

The `--bootstrap-artifact-source`

can be set to either `Direct`

or `Cache`

corresponding to using direct MAR (NOT network isolated) and private ACR (network isolated) for image pulls respectively.

The `--outbound-type parameter`

can be set to either `none`

or `block`

(preview). If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

#### Private link-based

Create a private link-based network isolated cluster by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with `--bootstrap-artifact-source`

, `--enable-private-cluster`

, and `--outbound-type`

parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --bootstrap-artifact-source Cache --outbound-type none --network-plugin azure --enable-private-cluster
```


#### API Server VNet integration

Create a network isolated cluster configured with API Server VNet Integration by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with `--bootstrap-artifact-source`

, `--enable-private-cluster`

, `--enable-apiserver-vnet-integration`

and `--outbound-type`

parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --bootstrap-artifact-source Cache --outbound-type none --network-plugin azure --enable-private-cluster --enable-apiserver-vnet-integration
```


### Update an existing AKS cluster to network isolated type

If you'd rather enable network isolation on an existing AKS cluster instead of creating a new cluster, use the [az aks update](/en-us/cli/azure/aks#az-aks-update) command.

To enable the network isolated feature on an existing AKS cluster, first run the following command to update `bootstrap-artifact-source`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache
```


Then you need to manually reimage all the exisiting nodepools:

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Note

You need to ensure the outbound exists until the first reimage completes. To check if the reimage completes, run:

```
NODEPOOLS=$(az aks nodepool list \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--query "[].name" -o tsv)
for NODEPOOL in $NODEPOOLS; do
echo "Waiting for node pool $NODEPOOL to finish upgrading..."
az aks nodepool wait \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--name "$NODEPOOL" \
--updated
echo "Node pool $NODEPOOL upgrade succeeded."
done
```


Wait and ensure the reimage completes, then run the following command to update `outbound-type`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --outbound-type none
```


Important

Remember to reimage the cluster's node pools instantly after you update the artifact source to Cache. Otherwise, the feature won't take effect for the cluster.

## Deploy a network isolated cluster with bring your own ACR

AKS supports bringing your own (BYO) ACR. To support the BYO ACR scenario, you have to configure an ACR private endpoint and a private DNS zone before you create the AKS cluster.

The following steps show how to prepare these resources:

- Custom virtual network and subnets for AKS and ACR.
- ACR, ACR cache rule, private endpoint, and private DNS zone.
- Custom control plane identity and kubelet identity.

### Step 1: Create the virtual network and subnets

```
az group create --name ${RESOURCE_GROUP} --location ${LOCATION}
az network vnet create --resource-group ${RESOURCE_GROUP} --name ${VNET_NAME} --address-prefixes 192.168.0.0/16
az network vnet subnet create --name ${AKS_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.1.0/24
SUBNET_ID=$(az network vnet subnet show --name ${AKS_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' --output tsv)
az network vnet subnet create --name ${ACR_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.2.0/24 --private-endpoint-network-policies Disabled
```


### Step 2: Disable virtual network outbound connectivity (Optional)

There are multiple ways to [disable the virtual network outbound connectivity](/en-us/azure/virtual-network/ip-services/default-outbound-access#how-can-i-transition-to-an-explicit-method-of-public-connectivity-and-disable-default-outbound-access).

### Step 3: Create the ACR and enable artifact cache

Create the ACR with the private link.

`az acr create --resource-group ${RESOURCE_GROUP} --name ${REGISTRY_NAME} --sku Premium --public-network-enabled false REGISTRY_ID=$(az acr show --name ${REGISTRY_NAME} -g ${RESOURCE_GROUP} --query 'id' --output tsv)`

Create an ACR cache rule following the below command to allow users to cache MAR container images and binaries in the new ACR, note the cache rule name and repo names must be strictly aligned with the guidance below.

`az acr cache create -n aks-managed-mcr -r ${REGISTRY_NAME} -g ${RESOURCE_GROUP} --source-repo "mcr.microsoft.com/*" --target-repo "aks-managed-repository/*"`


Note

With BYO ACR, it is your responsibility to ensure the ACR cache rule is created and maintained correctly as above. This step is critical to cluster creation, functioning and upgrading. This cache rule should NOT be modified.

### Step 4: Create a private endpoint for the ACR

```
az network private-endpoint create --name myPrivateEndpoint --resource-group ${RESOURCE_GROUP} --vnet-name ${VNET_NAME} --subnet ${ACR_SUBNET_NAME} --private-connection-resource-id ${REGISTRY_ID} --group-id registry --connection-name myConnection
NETWORK_INTERFACE_ID=$(az network private-endpoint show --name myPrivateEndpoint --resource-group ${RESOURCE_GROUP} --query 'networkInterfaces[0].id' --output tsv)
REGISTRY_PRIVATE_IP=$(az network nic show --ids ${NETWORK_INTERFACE_ID} --query "ipConfigurations[?privateLinkConnectionProperties.requiredMemberName=='registry'].privateIPAddress" --output tsv)
DATA_ENDPOINT_PRIVATE_IP=$(az network nic show --ids ${NETWORK_INTERFACE_ID} --query "ipConfigurations[?privateLinkConnectionProperties.requiredMemberName=='registry_data_$LOCATION'].privateIPAddress" --output tsv)
```


### Step 5: Create a private DNS zone and add records

Create a private DNS zone named `privatelink.azurecr.io`

. Add the records for the registry REST endpoint `{REGISTRY_NAME}.azurecr.io`

, and the registry data endpoint `{REGISTRY_NAME}.{REGISTRY_LOCATION}.data.azurecr.io`

.

```
az network private-dns zone create --resource-group ${RESOURCE_GROUP} --name "privatelink.azurecr.io"
az network private-dns link vnet create --resource-group ${RESOURCE_GROUP} --zone-name "privatelink.azurecr.io" --name MyDNSLink --virtual-network ${VNET_NAME} --registration-enabled false
az network private-dns record-set a create --name ${REGISTRY_NAME} --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP}
az network private-dns record-set a add-record --record-set-name ${REGISTRY_NAME} --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP} --ipv4-address ${REGISTRY_PRIVATE_IP}
az network private-dns record-set a create --name ${REGISTRY_NAME}.${LOCATION}.data --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP}
az network private-dns record-set a add-record --record-set-name ${REGISTRY_NAME}.${LOCATION}.data --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP} --ipv4-address ${DATA_ENDPOINT_PRIVATE_IP}
```


### Step 6: Create control plane and kubelet identities

#### Control plane identity

```
az identity create --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP}
CLUSTER_IDENTITY_RESOURCE_ID=$(az identity show --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' -o tsv)
CLUSTER_IDENTITY_PRINCIPAL_ID=$(az identity show --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'principalId' -o tsv)
```


#### Kubelet identity

```
az identity create --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP}
KUBELET_IDENTITY_RESOURCE_ID=$(az identity show --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' -o tsv)
KUBELET_IDENTITY_PRINCIPAL_ID=$(az identity show --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'principalId' -o tsv)
```


#### Grant AcrPull permissions for the Kubelet identity

```
az role assignment create --role AcrPull --scope ${REGISTRY_ID} --assignee-object-id ${KUBELET_IDENTITY_PRINCIPAL_ID} --assignee-principal-type ServicePrincipal
```


After you configure these resources, you can proceed to create the network isolated AKS cluster with BYO ACR.

### Step 7: Create network isolated cluster using BYO ACR

When creating a network isolated cluster, you can choose one of the following private cluster modes - private link-based or API Server Vnet Integration.

Regardless of the mode you select, you should set `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

The `--bootstrap-artifact-source`

can be set to either `Direct`

or `Cache`

corresponding to using direct Microsoft Artifact Registry (MAR) (NOT network isolated) and private ACR (network isolated) for image pulls respectively.

The `--outbound-type parameter`

can be set to either `none`

or `block`

(preview). If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

#### Private link-based

Create a private link-based network isolated cluster that accesses your ACR by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with the required parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --vnet-subnet-id ${SUBNET_ID} --assign-identity ${CLUSTER_IDENTITY_RESOURCE_ID} --assign-kubelet-identity ${KUBELET_IDENTITY_RESOURCE_ID} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID} --outbound-type none --network-plugin azure --enable-private-cluster
```


#### API Server VNet integration

For a network isolated cluster configured with API server VNet integration, first create a subnet and assign the correct role with the following commands:

```
az network vnet subnet create --name ${APISERVER_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.3.0/24
export APISERVER_SUBNET_ID=$(az network vnet subnet show --resource-group ${RESOURCE_GROUP} --vnet-name ${VNET_NAME} --name ${APISERVER_SUBNET_NAME} --query id -o tsv)
```


```
az role assignment create --scope ${APISERVER_SUBNET_ID} --role "Network Contributor" --assignee-object-id ${CLUSTER_IDENTITY_PRINCIPAL_ID} --assignee-principal-type ServicePrincipal
```


Create a network isolated cluster configured with API Server VNet Integration and access your ACR by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with the required parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --vnet-subnet-id ${SUBNET_ID} --assign-identity ${CLUSTER_IDENTITY_RESOURCE_ID} --assign-kubelet-identity ${KUBELET_IDENTITY_RESOURCE_ID} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID} --outbound-type none --network-plugin azure --enable-apiserver-vnet-integration --apiserver-subnet-id ${APISERVER_SUBNET_ID}
```


### Update an existing AKS cluster

If you'd rather enable network isolation on an existing AKS cluster instead of creating a new cluster, use the [az aks update](/en-us/cli/azure/aks#az-aks-update) command.

When creating the private endpoint and private DNS zone for the BYO ACR, use the existing virtual network and subnets of the existing AKS cluster. When you assign the **AcrPull** permission to the kubelet identity, use the existing kubelet identity of the existing AKS cluster.

To enable the network isolated feature on an existing AKS cluster, first run the following command to update `bootstrap-artifact-source`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID}
```


Then you need to manually reimage all the exisiting nodepools:

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Note

You need to ensure the outbound exists until the first reimage completes. To check if the reimage completes, run:

```
NODEPOOLS=$(az aks nodepool list \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--query "[].name" -o tsv)
for NODEPOOL in $NODEPOOLS; do
echo "Waiting for node pool $NODEPOOL to finish upgrading..."
az aks nodepool wait \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--name "$NODEPOOL" \
--updated
echo "Node pool $NODEPOOL upgrade succeeded."
done
```


Wait and ensure the reimage completes, then run the following command to update `outbound-type`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --outbound-type none
```


Important

Remember to reimage the cluster's node pools instantly after you update the artifact source to Cache. Otherwise, the feature won't take effect for the cluster.

### Update your ACR ID

It's possible to update the private ACR used with a network isolated cluster. To identify the ACR resource ID, use the `az aks show`

command.

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME}
```


Updating the ACR ID is performed by running the `az aks update`

command with the `--bootstrap-artifact-source`

and `--bootstrap-container-registry-resource-id`

parameters.

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id <New BYO ACR resource ID>
```


When you update the ACR ID on an existing cluster, you need to manually reimage all existing nodes.

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Important

Remember to reimage the cluster's node pools after you enable the network isolated cluster feature. Otherwise, the feature won't take effect for the cluster.

## Validate that network isolated cluster is enabled

To validate the network isolated cluster feature is enabled, use the `[az aks show](/en-us/cli/azure/aks#az-aks-show) command

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME}
```


The following output shows that the feature is enabled, based on the values of the `outboundType`

property (none or blocked) and `artifactSource`

property (Cached).

```
"kubernetesVersion": "1.30.3",
"name": "myAKSCluster"
"type": "Microsoft.ContainerService/ManagedClusters"
"properties": {
...
"networkProfile": {
...
"outboundType": "none",
...
},
...
"bootstrapProfile": {
"artifactSource": "Cache",
"containerRegistryId": "/subscriptions/my-subscription-id/my-node-resource-group-name/providers/Microsoft.ContainerRegistry/registries/my-registry-name"
},
...
}
```


## Disable network isolated cluster

Disable the network isolated cluster feature by running the `az aks update`

command with the `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Direct --outbound-type LoadBalancer
```


When you disable the feature on an existing cluster, you need to manually reimage all existing nodes.

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Important

Remember to reimage the cluster's node pools after you disable the network isolated cluster feature. Otherwise, the feature won't take effect for the cluster.

## Troubleshooting

If you're experiencing issues, such as image pull fails, see [Troubleshoot network isolated Azure Kubernetes Service (AKS) clusters issues](/en-us/troubleshoot/azure/azure-kubernetes/extensions/troubleshoot-network-isolated-cluster).

## Next steps

If you want to set up outbound restriction configuration using Azure Firewall, visit [Control egress traffic using Azure Firewall in AKS](limit-egress-traffic).

If you want to restrict how pods communicate between themselves and East-West traffic restrictions within cluster, see [Secure traffic between pods using network policies in AKS](use-network-policies).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-pool-snapshot -->

# Azure Kubernetes Service (AKS) node pool snapshot

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS releases a new node image weekly. Every new cluster, new node pool, or upgrade cluster always receives the latest image, which can make it hard to maintain consistency and have repeatable environments.

Node pool snapshots allow you to take a configuration snapshot of your node pool and then create new node pools or new clusters based of that snapshot for as long as that configuration and kubernetes version is supported. For more information on the supportability windows, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

The snapshot is an Azure resource that contains the configuration information from the source node pool, such as the node image version, kubernetes version, OS type, and OS SKU. You can then reference this snapshot resource and the respective values of its configuration to create any new node pool or cluster based off of it.

## Before you begin

This article assumes that you have an existing AKS cluster. If you don't have an AKS cluster, for guidance on a designing an enterprise-scale implementation of AKS, see [Plan your AKS design](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

### Limitations

- Any node pool or cluster created from a snapshot must use a VM from the same virtual machine family as the snapshot, for example, you can't create a new N-Series node pool based of a snapshot captured from a D-Series node pool because the node images in those cases are structurally different.
- Snapshots must be created same region as the source node pool, those snapshots can be used to create or update clusters and node pools in other regions.

## Take a node pool snapshot

In order to take a snapshot from a node pool, you need the node pool resource ID, which you can get from the following command:

```
NODEPOOL_ID=$(az aks nodepool show --name nodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --query id -o tsv)
```


Important

Your AKS node pool must be created or upgraded after Nov 10th, 2021 in order for a snapshot to be taken from it.
If you are using the `aks-preview`

Azure CLI extension version `0.5.59`

or newer, the commands for node pool snapshot have changed. For updated commands, see the [Node Pool Snapshot CLI reference](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add).

Now, to take a snapshot from the previous node pool, you use the `az aks snapshot`

CLI command.

```
az aks nodepool snapshot create --name MySnapshot --resource-group MyResourceGroup --nodepool-id $NODEPOOL_ID --location eastus
```


## Create a node pool from a snapshot

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use the following command to add a new node pool based off of this snapshot.

```
az aks nodepool add --name np2 --cluster-name myAKSCluster --resource-group myResourceGroup --snapshot-id $SNAPSHOT_ID
```


## Upgrading a node pool to a snapshot

You can upgrade a node pool to a snapshot configuration if the snapshot Kubernetes version and node image version are more recent than the current node pool versions. And the snapshot node image version is within 90 days of the node image publish date.

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use this command to upgrade this node pool to this snapshot configuration.

```
az aks nodepool upgrade --name nodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --snapshot-id $SNAPSHOT_ID
```


Note

Your node pool image version is the same contained in the snapshot and remains the same throughout every scale operation. However, if this node pool is upgraded or a node image upgrade is performed without providing a snapshot-id the node image is upgraded to the latest version.

Note

To upgrade only the node version for your node pool, use the `--node-image-only`

flag. This is required when upgrading the node image version for a node pool based on a snapshot with an identical Kubernetes version.

## Create a cluster from a snapshot

When you create a cluster from a snapshot, the snapshot configuration creates the cluster original system pool.

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use this command to create this cluster off of the snapshot configuration.

```
az aks create \
--name myAKSCluster2 \
--resource-group myResourceGroup \
--snapshot-id $SNAPSHOT_ID \
--generate-ssh-keys
```


## Next steps

- See the
[AKS release notes](https://github.com/Azure/AKS/releases)for information about the latest node images. - Learn how to upgrade the Kubernetes version with
[Upgrade an AKS cluster](upgrade-cluster). - Learn how to upgrade your node image version with
[Node Image Upgrade](node-image-upgrade) - Learn more about multiple node pools with
[Create multiple node pools](create-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-fine-tune-language-models -->

# Concepts - Fine-tuning language models for AI and machine learning workflows

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about fine-tuning [language models](concepts-ai-ml-language-models), including some common methods and how applying the tuning results can improve the performance of your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## Pre-trained language models

*Pre-trained language models (PLMs)* offer an accessible way to get started with AI inferencing and are widely used in natural language processing (NLP). PLMs are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks. These models typically consist of billions of parameters, or *weights*, that are learned during the pre-training process.

PLMs can learn universal language representations that capture the statistical properties of natural language, such as the probability of words or sequences of words occurring in a given context. These representations can be transferred to downstream tasks, such as text classification, named entity recognition, and question answering, by fine-tuning the model on task-specific datasets.

### Pros and cons

The following table lists some pros and cons of using PLMs in your AI and machine learning workflows:

| Pros | Cons |
|---|---|
| • Get started quickly with deployment in your machine learning lifecycle. • Avoid heavy compute costs associated with model training. • Reduces the need to store large, labeled datasets. |
• Might provide generalized or outdated responses based on pre-training data sources. • Might not be suitable for all tasks or domains. • Performance can vary depending on inferencing context. |

## Fine-tuning methods

### Parameter efficient fine-tuning

*Parameter efficient fine-tuning (PEFT)* is a method for fine-tuning PLMs on relatively small datasets with limited compute resources. PEFT uses a combination of techniques, like additive and selective methods to update weights, to improve the performance of the model on specific tasks. PEFT requires minimal compute resources and flexible quantities of data, making it suitable for low-resource settings. This method retains most of the weights of the original pre-trained model and updates the remaining weights to fit context-specific, labeled data.

### Low rank adaptation

*Low rank adaptation (LoRA)* is a PEFT method commonly used to customize large language models for new tasks. This method tracks changes to model weights and efficiently stores smaller weight matrices that represent only the model's trainable parameters, reducing memory usage and the compute power needed for fine-tuning. LoRA creates fine-tuning results, known as *adapter layers*, that can be temporarily stored and pulled into the model's architecture for new inferencing jobs.

*Quantized low rank adaptation (QLoRA)* is an extension of LoRA that further reduces memory usage by introducing quantization to the adapter layers. For more information, see [Making LLMs even more accessible with bitsandbites, 4-bit quantization, and QLoRA](https://huggingface.co/blog/4bit-transformers-bitsandbytes#:%7E:text=We%20present%20QLoRA%2C%20an%20efficient%20finetuning%20approach%20that,pretrained%20language%20model%20into%20Low%20Rank%20Adapters%7E%20%28LoRA%29.).

## Experiment with fine-tuning language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The AI toolchain operator add-on leverages KAITO to simplify onboarding, save on infrastructure costs, and reduce the time-to-inference for open-source models on an AKS cluster. The add-on automatically provisions right-sized GPU nodes and sets up the associated inference server as an endpoint server to your chosen model.

With KAITO version 0.3.0 or later, you can efficiently fine-tune supported MIT and Apache 2.0 licensed models with the following features:

- Store your retraining data as a container image in a private container registry.
- Host the new adapter layer image in a private container registry.
- Efficiently pull the image for inferencing with adapter layers in new scenarios.

For guidance on getting started with fine-tuning on KAITO, see the [Kaito Tuning Workspace API documentation][kaito-fine-tuning]. To learn more about deploying language models with KAITO in your AKS clusters, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-scheduler-configuration -->

# Scheduler configuration concepts for workload placement in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers scheduler configuration and advanced scheduling concepts for workload placement in Azure Kubernetes Service (AKS), including configurable scheduler profiles, scheduling plugins, and scheduling constraints.

## About the AKS scheduler

In AKS, the default mechanism of workload placement across nodes within a cluster is through the scheduler. The default scheduler is a control plane component responsible for assigning AKS deployment pods to nodes. Once the AKS scheduler selects a node, the deployment pod is bound to it, and the rest of the lifecycle continues.

When a pod is created without a specified node, the scheduler selects an optimal node based on several criteria, including (but not limited to):

- Available resources (CPU, memory)
[Node affinity/anti-affinity](operator-best-practices-advanced-scheduler#node-affinity)[Pod affinity/anti-affinity](operator-best-practices-advanced-scheduler#inter-pod-affinity-and-anti-affinity)[Taints and tolerations](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

### AKS scheduler configuration and scheduling strategies

By default, the AKS scheduler comes with a set of built-in rules that work well for general-purpose workloads. However, advanced use cases might require custom scheduling strategies. For example:

- Batch jobs might prefer collocating in a few nodes (for better performance) over topology-aware spreading (for reliability).
- Cost-sensitive workloads might benefit from node binpacking to consolidate jobs and minimize idle compute node costs.

To support these use cases, AKS allows you to set one or more in-tree scheduling plugins through a Kubernetes custom resource (CRD) to configure the scheduling behavior on your AKS cluster.

## Configurable scheduler profiles

A scheduler profile is a set of one or more in-tree scheduling plugins and configurations that dictate how to schedule a pod. Previously, AKS managed the scheduler configuration, and it wasn't accessible to users. Starting from Kubernetes version `1.33`

, you can now configure and set a scheduler profile (preview) for the Kubernetes scheduler on your cluster.

Each scheduler profile has the following components:

- A unique name.
- A set of
[scheduling plugins](#supported-in-tree-scheduling-plugins). - Custom arguments for fine-grained behavior (applicable to certain plugins).

## Supported in-tree scheduling plugins

AKS supports configuration of 18 in-tree Kubernetes scheduling plugins that allow pods to be placed on specific nodes, ensure pods are matched with specific storage resources, optimize for nodes with container images, and more.

The following sections walk you through these plugins, which are grouped into the following categories:

[Scheduling constraints and order-based plugins](#scheduling-constraints-and-order-based-plugins)[Node selection constraints scheduling plugins](#node-selection-constraints-scheduling-plugins)[Resource and topology optimization scheduling plugins](#resource-and-topology-optimization-scheduling-plugins)

To learn more about these plugins and configuration options, see the [Kubernetes Scheduling Plugin documentation](https://kubernetes.io/docs/reference/scheduling/config/#scheduling-plugins).

### Scheduling constraints and order-based plugins

`DefaultBinder`

: Responsible for binding the pod to a node after the scheduler selects a suitable node. Once the node is selected, the`DefaultBinder`

creates a binding object to ensure the pod is scheduled onto that node.`DefaultPreemption`

: Handles preemption, which is the process of evicting lower-priority pods to make room for higher-priority pods. If a pod can't be scheduled because there aren’t enough resources on the node, this plugin preempts other pods to make space. This plugin can receive the following arguments:`PodPriority`

: Defines the priority of the pod being scheduled.`PreemptionPolicy`

: The policy for handling pod preemption (for example:`"PreemptLowerPriority"`

or`"DoNotPreempt"`

).`PodPriorityClass`

: The priority class associated with the pod.`PodInfo`

: Information about the pods that are candidates for preemption.`Node`

: Information about the node on which preemption is considered.

`SchedulingGates`

: Introduces the concept of scheduling gates, which are conditions that must be satisfied before a pod is scheduled. For example, it can enforce the completion of certain tasks or operations before the scheduler attempts to schedule a pod.`PrioritySort`

: Sorts the list of pods according to their priority class. Pods with higher priority are scheduled first. It helps with the preemption decision-making and determines which pods to consider for priority scheduling.

### Node selection constraints scheduling plugins

`InterPodAffinity`

: Takes into account*affinity*rules specified by the user that influences scheduling based on the proximity of other pods. If a pod has affinity rules, it tries to schedule the pod on the same node or in the same topology as other pods that it has an affinity for (for example: for performance reasons or tight coupling). This plugin can receive the following arguments:`Affinity`

: Defines required or preferred affinity rules for the pod, which specifies other pods that the pod should or shouldn't be scheduled nearby.`TopologyKey`

: The key representing the failure domain to which the affinity rule applies (for example:`"kubernetes.io/hostname"`

for node-level affinity or`"topology.kubernetes.io/zone"`

for zone-level).`Weight`

: Defines how strongly the scheduler should consider a specific affinity rule.`Pod`

: The pod being scheduled.`OtherPods`

: List of other pods to consider in relation to the affinity rules.

`NodeAffinity`

: Enables scheduling based on node labels. It allows users to specify rules for which nodes a pod can be scheduled on based on the node's labels and provides fine-grained control over pod placement on nodes. This plugin can receive the following arguments:`NodeAffinity`

: Defines the required or preferred node affinity rules, such as`requiredDuringSchedulingIgnoredDuringExecution`

or`preferredDuringSchedulingIgnoredDuringExecution`

.`NodeSelectorTerms`

: Defines the set of node labels and values that must match.`Pod`

: The pod being scheduled.`Node`

: A potential node for scheduling.`LabelSelector`

: A selector for choosing nodes based on labels.

`NodeName`

: Forces pods to be scheduled on a specific node. When you specify the exact node name, the scheduler places the pod on that node if possible.`NodePorts`

: Ensures that a pod with a service of type`NodePort`

can be scheduled on a node that has the required ports available for binding. It checks whether the node has enough resources to support the node port allocations for the service.`NodeUnschedulable`

: Ensures that pods aren't scheduled on nodes marked as*unschedulable*. If a node is tainted with`node.kubernetes.io/unschedulable`

, the scheduler doesn't place any new pods on that node.`TaintToleration`

: Checks if a pod has the required tolerations to be scheduled on a node that has taints. Taints on nodes prevent pods from being scheduled unless the pod has a matching toleration.`NodeVolumeLimits`

: Checks whether a node has exceeded its volume limit. Each node has a maximum number of volumes it can attach, and this plugin ensures that the pod isn't scheduled on a node that has already reached that supported limit.`VolumeBinding`

: Ensures that persistent volumes (PVs) are properly bound to pods. It checks whether the volume that a pod requires can be bound to a node and ensures the volume is available on the selected node. This plugin can receive the following arguments:`VolumeClaims`

: The persistent volume claims (PVCs) made by the pod being scheduled.`Node`

: The candidate node being considered for scheduling.`VolumeAvailable`

: Checks if the persistent volume is available on the node or within the appropriate zone.`Pod`

: The pod that is requesting volume binding.`StorageClass`

: The storage class associated with the persistent volume.`VolumeBindingMode`

: Defines whether the volume binding mode is`Immediate`

or`WaitForFirstConsumer`

(for delayed binding until a pod is scheduled).

`VolumeRestrictions`

: Ensures that volume restrictions (such as limitations on the number of volumes a node can have attached) are respected when scheduling a pod. It prevents scheduling a pod on a node where the volume restrictions would be violated.`VolumeZone`

: Ensures that volumes are scheduled in the same availability zone as the pod. For example, if a pod requests a volume that must be in a specific zone, the plugin ensures that both the pod and the volume are in the same zone.

### Resource and topology optimization scheduling plugins

`NodeResourcesBalancedAllocation`

: Aims to balance the resource allocation on nodes. When scheduling a pod, it considers how resources like CPU and memory are allocated across nodes to avoid overprovisioning or underutilizing resources. This plugin can receive the following arguments:`ResourceRequests`

: The resource requests (CPU, memory, etc.) of the pod being scheduled.`Node`

: A candidate node for scheduling.`NodeResources`

: The available resources (CPU, memory, etc.) of the node.`ClusterResourceUsage`

: Cluster-wide resource usage metrics to help decide the best node to balance resources.

`NodeResourcesFit`

: Checks whether a node has enough available resources (CPU, memory, etc.) to run the pod. It ensures that a pod is only scheduled on a node that has sufficient resources available. This plugin can receive the following arguments:`ResourceRequests`

: The resource requests of the pod.`Node`

: The candidate node being considered for scheduling.`NodeCapacity`

: The available capacity of resources on the node.`Pod`

: The pod being scheduled, with its resource requests.

`ImageLocality`

: Helps the scheduler decide whether to schedule a pod onto a node based on the presence of a required container image. It tries to schedule pods on nodes where the required image is already present, reducing the time needed to pull the image.`PodTopologySpread`

: Ensures that pods are spread evenly across the topology (like zones or regions) to achieve high availability and fault tolerance. It tries to avoid placing multiple replicas of a pod in the same failure domain. This plugin can receive the following arguments:`TopologySpreadConstraints`

: Defines the constraints for how pods should be spread across failure domains, including the key (for example:`topology.kubernetes.io/zone`

) and the number of pods to be placed in each domain.`Pod`

: The pod being scheduled.`FailureDomain`

: The failure domain key (for example: zone or region).`PodAffinity`

: Information about pod affinity, which could also impact how the pods are distributed.`Node`

: Potential nodes for placement.`PodSpreadScore`

: Used to determine how much "spread" the pod should have across domains (higher scores indicate better spreading).


## Next step


[Configure and deploy a scheduler profile (preview) on your AKS cluster].

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-workload-identity -->

# Securely scale your applications using the KEDA add-on and workload identity on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to securely scale your applications with the Kubernetes Event-driven Autoscaling (KEDA) add-on and workload identity on Azure Kubernetes Service (AKS).

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules).

## Create a resource group

Create a resource group using the

command. Make sure you replace the placeholder values with your own values.`az group create`

`LOCATION=<azure-region> RG_NAME=<resource-group-name> az group create --name $RG_NAME --location $LOCATION`


## Create an AKS cluster

Create an AKS cluster with the KEDA add-on, workload identity, and OIDC issuer enabled using the

command with the`az aks create`

`--enable-workload-identity`

,`--enable-keda`

, and`--enable-oidc-issuer`

flags. Make sure you replace the placeholder value with your own value.`AKS_NAME=<cluster-name> az aks create \ --name $AKS_NAME \ --resource-group $RG_NAME \ --enable-workload-identity \ --enable-oidc-issuer \ --enable-keda \ --generate-ssh-keys`

Validate the deployment was successful and make sure the cluster has KEDA, workload identity, and OIDC issuer enabled using the

command with the`az aks show`

`--query`

flag set to`"[workloadAutoScalerProfile, securityProfile, oidcIssuerProfile]"`

.`az aks show \ --name $AKS_NAME \ --resource-group $RG_NAME \ --query "[workloadAutoScalerProfile, securityProfile, oidcIssuerProfile]"`

Connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --name $AKS_NAME \ --resource-group $RG_NAME \ --overwrite-existing`


## Create an Azure Service Bus

Create an Azure Service Bus namespace using the

command. Make sure to replace the placeholder value with your own value.`az servicebus namespace create`

`SB_NAME=<service-bus-name> SB_HOSTNAME="${SB_NAME}.servicebus.windows.net" az servicebus namespace create \ --name $SB_NAME \ --resource-group $RG_NAME \ --disable-local-auth`

Create an Azure Service Bus queue using the

command. Make sure to replace the placeholder value with your own value.`az servicebus queue create`

`SB_QUEUE_NAME=<service-bus-queue-name> az servicebus queue create \ --name $SB_QUEUE_NAME \ --namespace $SB_NAME \ --resource-group $RG_NAME`


## Create a managed identity

Create a managed identity using the

command. Make sure to replace the placeholder value with your own value.`az identity create`

`MI_NAME=<managed-identity-name> MI_CLIENT_ID=$(az identity create \ --name $MI_NAME \ --resource-group $RG_NAME \ --query "clientId" \ --output tsv)`

Get the OIDC issuer URL using the

command with the`az aks show`

`--query`

flag set to`oidcIssuerProfile.issuerUrl`

.`AKS_OIDC_ISSUER=$(az aks show \ --name $AKS_NAME \ --resource-group $RG_NAME \ --query oidcIssuerProfile.issuerUrl \ --output tsv)`

Create a federated credential between the managed identity and the namespace and service account used by the workload using the

command. Make sure to replace the placeholder value with your own value.`az identity federated-credential create`

`FED_WORKLOAD=<federated-credential-workload-name> az identity federated-credential create \ --name $FED_WORKLOAD \ --identity-name $MI_NAME \ --resource-group $RG_NAME \ --issuer $AKS_OIDC_ISSUER \ --subject system:serviceaccount:default:$MI_NAME \ --audience api://AzureADTokenExchange`

Create a second federated credential between the managed identity and the namespace and service account used by the keda-operator using the

command. Make sure to replace the placeholder value with your own value.`az identity federated-credential create`

`FED_KEDA=<federated-credential-keda-name> az identity federated-credential create \ --name $FED_KEDA \ --identity-name $MI_NAME \ --resource-group $RG_NAME \ --issuer $AKS_OIDC_ISSUER \ --subject system:serviceaccount:kube-system:keda-operator \ --audience api://AzureADTokenExchange`


## Create role assignments

Get the object ID for the managed identity using the

command with the`az identity show`

`--query`

flag set to`"principalId"`

.`MI_OBJECT_ID=$(az identity show \ --name $MI_NAME \ --resource-group $RG_NAME \ --query "principalId" \ --output tsv)`

Get the Service Bus namespace resource ID using the

command with the`az servicebus namespace show`

`--query`

flag set to`"id"`

.`SB_ID=$(az servicebus namespace show \ --name $SB_NAME \ --resource-group $RG_NAME \ --query "id" \ --output tsv)`

Assign the Azure Service Bus Data Owner role to the managed identity using the

command.`az role assignment create`

`az role assignment create \ --role "Azure Service Bus Data Owner" \ --assignee-object-id $MI_OBJECT_ID \ --assignee-principal-type ServicePrincipal \ --scope $SB_ID`


## Enable Workload Identity on KEDA operator

After creating the federated credential for the

`keda-operator`

ServiceAccount, you will need to manually restart the`keda-operator`

pods to ensure Workload Identity environment variables are injected into the pod.`kubectl rollout restart deploy keda-operator -n kube-system`

Confirm the keda-operator pods restart

`kubectl get pod -n kube-system -lapp=keda-operator -w`

Once you've confirmed the keda-operator pods have finished rolling hit

`Ctrl+c`

to break the previous watch command then confirm the Workload Identity environment variables have been injected.`KEDA_POD_ID=$(kubectl get po -n kube-system -l app.kubernetes.io/name=keda-operator -ojsonpath='{.items[0].metadata.name}') kubectl describe po $KEDA_POD_ID -n kube-system`

You should see output similar to the following under

**Environment**.`--- AZURE_CLIENT_ID: AZURE_TENANT_ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx AZURE_FEDERATED_TOKEN_FILE: /var/run/secrets/azure/tokens/azure-identity-token AZURE_AUTHORITY_HOST: https://login.microsoftonline.com/ ---`

Deploy a KEDA TriggerAuthentication resource that includes the User-Assigned Managed Identity's Client ID.

`kubectl apply -f - <<EOF apiVersion: keda.sh/v1alpha1 kind: TriggerAuthentication metadata: name: azure-servicebus-auth namespace: default # this must be same namespace as the ScaledObject/ScaledJob that will use it spec: podIdentity: provider: azure-workload identityId: $MI_CLIENT_ID EOF`

Note

With the TriggerAuthentication in place, KEDA will be able to authenticate via workload identity. The

`keda-operator`

Pods use the`identityId`

to authenticate against Azure resources when evaluating scaling triggers.

## Publish messages to Azure Service Bus

At this point everything is configured for scaling with KEDA and Microsoft Entra Workload Identity. We will test this by deploying producer and consumer workloads.

Create a new ServiceAccount for the workloads.

`kubectl apply -f - <<EOF apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: $MI_CLIENT_ID name: $MI_NAME EOF`

Deploy a Job to publish 100 messages.

`kubectl apply -f - <<EOF apiVersion: batch/v1 kind: Job metadata: name: myproducer spec: template: metadata: labels: azure.workload.identity/use: "true" spec: serviceAccountName: $MI_NAME containers: - image: ghcr.io/azure-samples/aks-app-samples/servicebusdemo:latest name: myproducer resources: {} env: - name: OPERATION_MODE value: "producer" - name: MESSAGE_COUNT value: "100" - name: AZURE_SERVICEBUS_QUEUE_NAME value: $SB_QUEUE_NAME - name: AZURE_SERVICEBUS_HOSTNAME value: $SB_HOSTNAME restartPolicy: Never EOF`


## Consume messages from Azure Service Bus

Now that we have published messages to the Azure Service Bus queue, we will deploy a ScaledJob to consume the messages. This ScaledJob will use the KEDA TriggerAuthentication resource to authenticate against the Azure Service Bus queue using the workload identity and scale out every 10 messages.

Deploy a ScaledJob resource to consume the messages. The scale trigger will be configured to scale out every 10 messages. The KEDA scaler will create 10 jobs to consume the 100 messages.

`kubectl apply -f - <<EOF apiVersion: keda.sh/v1alpha1 kind: ScaledJob metadata: name: myconsumer-scaledjob spec: jobTargetRef: template: metadata: labels: azure.workload.identity/use: "true" spec: serviceAccountName: $MI_NAME containers: - image: ghcr.io/azure-samples/aks-app-samples/servicebusdemo:latest name: myconsumer env: - name: OPERATION_MODE value: "consumer" - name: MESSAGE_COUNT value: "10" - name: AZURE_SERVICEBUS_QUEUE_NAME value: $SB_QUEUE_NAME - name: AZURE_SERVICEBUS_HOSTNAME value: $SB_HOSTNAME restartPolicy: Never triggers: - type: azure-servicebus metadata: queueName: $SB_QUEUE_NAME namespace: $SB_NAME messageCount: "10" authenticationRef: name: azure-servicebus-auth EOF`

Note

ScaledJob creates a Kubernetes Job resource whenever a scaling event occurs and thus a Job template needs to be passed in when creating the resource. As new Jobs are created, Pods will be deployed with workload identity bits to consume messages.

Verify the KEDA scaler worked as intended.

`kubectl describe scaledjob myconsumer-scaledjob`

You should see events similar to the following.

`Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal KEDAScalersStarted 10m scale-handler Started scalers watch Normal ScaledJobReady 10m keda-operator ScaledJob is ready for scaling Warning KEDAScalerFailed 10m scale-handler context canceled Normal KEDAJobsCreated 10m scale-handler Created 10 jobs`


## Clean up resources

After you verify that the deployment is successful, you can clean up the resources to avoid incurring Azure costs.

Delete the Azure resource group and all resources in it using the [

`az group delete`

][az-group-delete] command.`az group delete --name $RG_NAME --yes --no-wait`


## Next steps

This article showed you how to securely scale your applications using the KEDA add-on and workload identity in AKS.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more about KEDA, see the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ha-dr-overview -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-identity-access -->

# Connect your Azure identity provider to the Azure Key Vault Secrets Store CSI Driver in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Secrets Store Container Storage Interface (CSI) Driver on Azure Kubernetes Service (AKS) provides various methods of identity-based access to your Azure Key Vault. This article outlines these methods and best practices for when to use Azure role-based access control (Azure RBAC) or OpenID Connect (OIDC) security models to access your key vault and AKS cluster.

You can use one of the following access methods:

- Service Connector with managed identity
- Workload ID
- User-assigned managed identity

Learn how to connect to Azure Key Vault with the Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster using Service Connector. In this article, you complete the following tasks:

- Create an AKS cluster and an Azure Key Vault.
- Create a connection between the AKS cluster and the Azure Key Vault with Service Connector.
- Create a
`SecretProviderClass`

CRD and a`Pod`

that consumes the CSI provider to test the connection. - Clean up resources.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The
[Azure CLI](/en-us/cli/azure/install-azure-cli). Sign in using thecommand.`az login`

[Docker](https://docs.docker.com/get-docker/)and[kubectl](https://kubernetes.io/docs/tasks/tools/). To install kubectl locally, use thecommand.`az aks install-cli`

- A basic understanding of containers and AKS. Get started by
[preparing an application for AKS](/en-us/azure/aks/tutorial-kubernetes-prepare-app). - Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster.

## Initial set-up

If you're using Service Connector for the first time, start by running the command

[az provider register](/en-us/cli/azure/provider#az-provider-register)to register the Service Connector and Kubernetes Configuration resource providers.`az provider register -n Microsoft.ServiceLinker`

`az provider register -n Microsoft.KubernetesConfiguration`

Tip

You can check if these resource providers have already been registered by running the commands

`az provider show -n "Microsoft.ServiceLinker" --query registrationState`

and`az provider show -n "Microsoft.KubernetesConfiguration" --query registrationState`

.Optionally, use the Azure CLI command to get a list of supported target services for AKS cluster.

`az aks connection list-support-types --output table`


## Create Azure resources

Create a resource group using the

command.`az group create`

`az group create \ --name <resource-group-name> \ --location <location>`

Create an AKS cluster using the

command. The following example creates a single-node AKS cluster with managed identity enabled.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --enable-managed-identity \ --node-count 1`

Connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group <resource-group-name> \ --name <cluster-name>`

Create an Azure key vault using the

command.`az keyvault create`

`az keyvault create \ --resource-group <resource-group-name> \ --name <key-vault-name> \ --location <location>`

Create a secret in the key vault using the

command.`az keyvault secret set`

`az keyvault secret set \ --vault-name <key-vault-name> \ --name <secret-name> \ --value <secret-value>`


## Create a service connection in AKS with Service Connector

You can create a service connection to Azure Key Vault using the Azure portal or Azure CLI.

In the Azure portal, navigate to your AKS cluster resource.

From the service menu, under

**Settings**, select**Service Connector**>**Create**.On the

**Create connection**page, configure the following settings in the**Basics**tab:**Kubernetes namespace**: Select**default**.**Service type**: Select**Key Vault**and select the checkbox to enable the Azure Key Vault CSI Provider.**Connection name**: Enter a name for the connection.**Subscription**: Select the subscription that contains the key vault.**Key vault**: Select the key vault you created.**Client type**: Select**None**.

Select

**Review + create**, and then select**Create**to create the connection.

## Test the connection

### Clone the sample repo and deploy manifest files

Clone the sample repository using the

`git clone`

command.`git clone https://github.com/Azure-Samples/serviceconnector-aks-samples.git`

Change directories to the Azure Key Vault CSI provider sample.

`cd serviceconnector-aks-samples/azure-keyvault-csi-provider`

In the

`secret_provider_class.yaml`

file, replace the following placeholders with your Azure Key Vault information:- Replace
`<AZURE_KEYVAULT_NAME>`

with the name of the key vault you created and connected. - Replace
`<AZURE_KEYVAULT_TENANTID>`

with the tenant ID of the key vault. - Replace
`<AZURE_KEYVAULT_CLIENTID>`

with identity client ID of the`azureKeyvaultSecretsProvider`

addon. - Replace
`<KEYVAULT_SECRET_NAME>`

with the key vault secret you created. For example,`ExampleSecret`

.

- Replace
Deploy the

`SecretProviderClass`

CRD using the`kubectl apply`

command.`kubectl apply -f secret_provider_class.yaml`

Deploy the

`Pod`

manifest file using the`kubectl apply`

command.The command creates a pod named

`sc-demo-keyvault-csi`

in the default namespace of your AKS cluster.`kubectl apply -f pod.yaml`


### Verify the connection

Verify the pod was created successfully using the

`kubectl get`

command.`kubectl get pod/sc-demo-keyvault-csi`

After the pod starts, the mounted content at the volume path specified in your deployment YAML is available.

Show the secrets held in the secrets store using the

`kubectl exec`

command.`kubectl exec sc-demo-keyvault-csi -- ls /mnt/secrets-store/`

Display a secret using the

`kubectl exec`

command.This example command shows a test secret named

`ExampleSecret`

.`kubectl exec sc-demo-keyvault-csi -- cat /mnt/secrets-store/ExampleSecret`


## Prerequisites for CSI Driver

- Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster. - Microsoft Entra Workload ID supports both Windows and Linux clusters.

## Access with a Microsoft Entra Workload ID

A [Microsoft Entra Workload ID](workload-identity-overview) is an identity that an application running on a pod uses to authenticate itself against other Azure services, such as workloads in software. The Secret Store CSI Driver integrates with native Kubernetes capabilities to federate with external identity providers.

In this security model, the AKS cluster acts as token issuer. Microsoft Entra ID then uses OIDC to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. For your workload to exchange a service account token projected to its volume for a Microsoft Entra token, you need the Azure Identity client library in the Azure SDK or the Microsoft Authentication Library (MSAL)

Note

- This authentication method replaces Microsoft Entra pod-managed identity (preview). The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated as of October 24, 2022.
- Microsoft Entra Workload ID supports both Windows and Linux clusters.

### Configure workload identity

Set your subscription using the

command.`az account set`

`export SUBSCRIPTION_ID=<subscription id> export RESOURCE_GROUP=<resource group name> export UAMI=<name for user assigned identity> export KEYVAULT_NAME=<existing keyvault name> export CLUSTER_NAME=<aks cluster name> az account set --subscription $SUBSCRIPTION_ID`

Create a managed identity using the

command.`az identity create`

Note

This step assumes you have an existing AKS cluster with workload identity enabled. If workload identity isn't enabled, see

[Enable workload identity on an existing AKS cluster](workload-identity-deploy-cluster#enable-oidc-issuer-and-microsoft-entra-workload-id-on-an-aks-cluster)to enable it.`az identity create --name $UAMI --resource-group $RESOURCE_GROUP export USER_ASSIGNED_CLIENT_ID="$(az identity show --resource-group $RESOURCE_GROUP --name $UAMI --query 'clientId' -o tsv)" export IDENTITY_TENANT=$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query identity.tenantId -o tsv)`

Create a role assignment that grants the workload identity permission to access the key vault secrets, access keys, and certificates using the

command.`az role assignment create`

Important

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`key`

or`certificate`

type, assign therole to give permissions.`Key Vault Certificate User`

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`secret`

type, assign therole.`Key Vault Secrets User`

- If your key vault isn't set with
`--enable-rbac-authorization`

, you can use thecommand with the`az keyvault set-policy`

`--key-permissions get`

,`--certificate-permissions get`

, or`--secret-permissions get`

parameter to create a key vault policy to grant access for keys, certificates, or secrets. For example:

`az keyvault set-policy --name $KEYVAULT_NAME --key-permissions get --object-id $IDENTITY_OBJECT_ID`

`export KEYVAULT_SCOPE=$(az keyvault show --name $KEYVAULT_NAME --query id -o tsv) # Example command for key vault with Azure RBAC enabled using `key` type az role assignment create --role "Key Vault Certificate User" --assignee $USER_ASSIGNED_CLIENT_ID --scope $KEYVAULT_SCOPE`

- If your key vault is set with
Get the AKS cluster OIDC Issuer URL using the

command.`az aks show`

Note

This step assumes you have an existing AKS cluster with the OIDC Issuer URL enabled. If the OIDC Issuer URL isn't enabled, see

[Update an AKS cluster with OIDC Issuer](use-oidc-issuer#enable-the-oidc-issuer-on-an-existing-aks-cluster)to enable it.`export AKS_OIDC_ISSUER="$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query "oidcIssuerProfile.issuerUrl" -o tsv)" echo $AKS_OIDC_ISSUER`

Establish a federated identity credential between the Microsoft Entra application, service account issuer, and subject. Get the object ID of the Microsoft Entra application using the following commands. Make sure to update the values for

`serviceAccountName`

and`serviceAccountNamespace`

with the Kubernetes service account name and its namespace.`export SERVICE_ACCOUNT_NAME="workload-identity-sa" # sample name; can be changed export SERVICE_ACCOUNT_NAMESPACE="default" # can be changed to namespace of your workload cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${USER_ASSIGNED_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`

Create the federated identity credential between the managed identity, service account issuer, and subject using the

command.`az identity federated-credential create`

`export FEDERATED_IDENTITY_NAME="aksfederatedidentity" # can be changed as needed az identity federated-credential create --name $FEDERATED_IDENTITY_NAME --identity-name $UAMI --resource-group $RESOURCE_GROUP --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME}`

Deploy a

`SecretProviderClass`

using the`kubectl apply`

command and the following YAML script.`cat <<EOF | kubectl apply -f - # This is a SecretProviderClass example using workload identity to access your key vault apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-kvname-wi # needs to be unique per namespace spec: provider: azure parameters: usePodIdentity: "false" clientID: "${USER_ASSIGNED_CLIENT_ID}" # Setting this to use workload identity keyvaultName: ${KEYVAULT_NAME} # Set to the name of your key vault cloudName: "" # [OPTIONAL for Azure] if not provided, the Azure environment defaults to AzurePublicCloud objects: | array: - | objectName: secret1 # Set to the name of your secret objectType: secret # object types: secret, key, or cert objectVersion: "" # [OPTIONAL] object versions, default to latest if empty - | objectName: key1 # Set to the name of your key objectType: key objectVersion: "" tenantId: "${IDENTITY_TENANT}" # The tenant ID of the key vault EOF`

Note

If you use

`objectAlias`

instead of`objectName`

, update the YAML script to account for it.Note

In order for the

`SecretProviderClass`

to function properly, make sure to populate your Azure Key Vault with secrets, keys, or certificates before referencing them in the`objects`

section.Deploy a sample pod using the

`kubectl apply`

command and the following YAML script.`cat <<EOF | kubectl apply -f - # This is a sample pod definition for using SecretProviderClass and workload identity to access your key vault kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline-wi labels: azure.workload.identity/use: "true" spec: serviceAccountName: "workload-identity-sa" containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-kvname-wi" EOF`


## Prerequisites for CSI Driver

- Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster.

## Access with managed identity

A [Microsoft Entra Managed ID](/en-us/entra/identity/managed-identities-azure-resources/overview) is an identity that an administrator uses to authenticate themselves against other Azure services. The managed identity uses Azure RBAC to federate with external identity providers.

In this security model, you can grant access to your cluster's resources to team members or tenants sharing a managed role. The role is checked for scope to access the keyvault and other credentials. When you [enabled the Azure Key Vault provider for Secrets Store CSI Driver on your AKS Cluster](csi-secrets-store-driver#create-an-aks-cluster-with-azure-key-vault-provider-for-secrets-store-csi-driver-support), it created a user identity.

### Configure managed identity

Access your key vault using the

command and the user-assigned managed identity created by the add-on. You should also retrieve the identity's`az aks show`

`clientId`

, which you use in later steps when creating a`SecretProviderClass`

.`az aks show --resource-group <resource-group> --name <cluster-name> --query addonProfiles.azureKeyvaultSecretsProvider.identity.objectId -o tsv az aks show --resource-group <resource-group> --name <cluster-name> --query addonProfiles.azureKeyvaultSecretsProvider.identity.clientId -o tsv`

Alternatively, you can create a new managed identity and assign it to your virtual machine (VM) scale set or to each VM instance in your availability set using the following commands.

`az identity create --resource-group <resource-group> --name <identity-name> az vmss identity assign --resource-group <resource-group> --name <agent-pool-vmss> --identities <identity-resource-id> az vm identity assign --resource-group <resource-group> --name <agent-pool-vm> --identities <identity-resource-id> az identity show --resource-group <resource-group> --name <identity-name> --query 'clientId' -o tsv`

Create a role assignment that grants the identity permission to access the key vault secrets, access keys, and certificates using the

command.`az role assignment create`

Important

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`key`

or`certificate`

type, assign therole.`Key Vault Certificate User`

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`secret`

type, assign therole.`Key Vault Secrets User`

- If your key vault isn't set with
`--enable-rbac-authorization`

, you can use thecommand with the`az keyvault set-policy`

`--key-permissions get`

,`--certificate-permissions get`

, or`--secret-permissions get`

parameter to create a key vault policy to grant access for keys, certificates, or secrets. For example:

`az keyvault set-policy --name $KEYVAULT_NAME --key-permissions get --object-id $IDENTITY_OBJECT_ID`

`export IDENTITY_OBJECT_ID="$(az identity show --resource-group <resource-group> --name <identity-name> --query 'principalId' -o tsv)" export KEYVAULT_SCOPE=$(az keyvault show --name <key-vault-name> --query id -o tsv) # Example command for key vault with Azure RBAC enabled using `key` type az role assignment create --role "Key Vault Certificate User" --assignee $USER_ASSIGNED_CLIENT_ID --scope $KEYVAULT_SCOPE`

- If your key vault is set with
Create a

`SecretProviderClass`

using the following YAML. Make sure to use your own values for`userAssignedIdentityID`

,`keyvaultName`

,`tenantId`

, and the objects to retrieve from your key vault.`# This is a SecretProviderClass example using user-assigned identity to access your key vault apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-kvname-user-msi spec: provider: azure parameters: usePodIdentity: "false" useVMManagedIdentity: "true" # Set to true for using managed identity userAssignedIdentityID: <client-id> # Set the clientID of the user-assigned managed identity to use keyvaultName: <key-vault-name> # Set to the name of your key vault cloudName: "" # [OPTIONAL for Azure] if not provided, the Azure environment defaults to AzurePublicCloud objects: | array: - | objectName: secret1 objectType: secret # object types: secret, key, or cert objectVersion: "" # [OPTIONAL] object versions, default to latest if empty - | objectName: key1 objectType: key objectVersion: "" tenantId: <tenant-id> # The tenant ID of the key vault`

Note

If you use

`objectAlias`

instead of`objectName`

, make sure to update the YAML script.Note

In order for the

`SecretProviderClass`

to function properly, make sure to populate your Azure Key Vault with secrets, keys, or certificates before referencing them in the`objects`

section.Apply the

`SecretProviderClass`

to your cluster using the`kubectl apply`

command.`kubectl apply -f secretproviderclass.yaml`

Create a pod using the following YAML.

`# This is a sample pod definition for using SecretProviderClass and the user-assigned identity to access your key vault kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline-user-msi spec: containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-kvname-user-msi"`

Apply the pod to your cluster using the

`kubectl apply`

command.`kubectl apply -f pod.yaml`


## Validate Key Vault secrets

After the pod starts, the mounted content at the volume path specified in your deployment YAML is available. Use the following commands to validate your secrets and print a test secret.

Show secrets held in the secrets store using the following command.

`kubectl exec busybox-secrets-store-inline-user-msi -- ls /mnt/secrets-store/`

Display a secret in the store using the following command. This example command shows the test secret

`ExampleSecret`

.`kubectl exec busybox-secrets-store-inline-user-msi -- cat /mnt/secrets-store/ExampleSecret`


## Obtain certificates and keys

The Azure Key Vault design makes sharp distinctions between keys, secrets, and certificates. The certificate features of the Key Vault service are designed to make use of key and secret capabilities. When you create a key vault certificate, it creates an addressable key and secret with the same name. This key allows authentication operations, and the secret allows the retrieval of the certificate value as a secret.

A key vault certificate also contains public x509 certificate metadata. The key vault stores both the public and private components of your certificate in a secret. You can obtain each individual component by specifying the `objectType`

in `SecretProviderClass`

. The following table shows which objects map to the various resources associated with your certificate:

| Object | Return value | Returns entire certificate chain |
|---|---|---|
`key` |
The public key, in Privacy Enhanced Mail (PEM) format. | N/A |
`cert` |
The certificate, in PEM format. | No |
`secret` |
The private key and certificate, in PEM format. | Yes |

## Disable the addon on existing clusters

Note

Before you disable the add-on, ensure that *no* `SecretProviderClass`

is in use. Trying to disable the add-on while a `SecretProviderClass`

exists results in an error.

Disable the Azure Key Vault provider for Secrets Store CSI Driver capability in an existing cluster using the [ az aks disable-addons](/en-us/cli/azure/aks#az-aks-disable-addons) command with the

`azure-keyvault-secrets-provider`

add-on.```
az aks disable-addons --addons azure-keyvault-secrets-provider --resource-group myResourceGroup --name myAKSCluster
```


Note

When you disable the add-on, existing workloads should have no issues or see any updates in the mounted secrets. If the pod restarts or a new pod is created as part of scale-up event, the pod fails to start because the driver is no longer running.

## Next steps

In this article, you learned how to create and provide an identity to access your Azure Key Vault. The [Service Connector](/en-us/azure/service-connector/overview) integration helps simplify the connection configuration for AKS workloads and Azure backing services. It securely handles authentication and network configurations and follows best practices for connecting to Azure services. For more information, see [Use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster](/en-us/azure/service-connector/tutorial-python-aks-keyvault-csi-driver) and the [Service Connector introduction](https://blog.aks.azure.com/2024/05/23/service-connector-intro).

If you want to configure extra configuration options or perform troubleshooting, see [Configuration options and troubleshooting resources for Azure Key Vault provider with Secrets Store CSI Driver in AKS](csi-secrets-store-configuration-options).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-multi-region -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr -->

# Install the Dapr extension for Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Dapr](dapr-overview) simplifies building resilient, stateless, and stateful applications that run on the cloud and edge and embrace the diversity of languages and developer frameworks. With Dapr's sidecar architecture, you can keep your code platform agnostic while tackling challenges around building microservices, like:

- Calling other services reliably and securely
- Building event-driven apps with pub/sub
- Building applications that are portable across multiple cloud services and hosts (for example, Kubernetes vs. a virtual machine)

Note

If you plan on installing Dapr in a Kubernetes production environment, see the [Dapr guidelines for production usage](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-production) documentation page.

## How it works

The Dapr extension uses the Azure CLI or a Bicep template to provision the Dapr control plane on your AKS or Arc-enabled Kubernetes cluster, creating the following Dapr services:

| Dapr service | Description |
|---|---|
`dapr-operator` |
Manages component updates and Kubernetes services endpoints for Dapr (state stores, pub/subs, etc.) |
`dapr-sidecar-injector` |
Injects Dapr into annotated deployment pods and adds the environment variables `DAPR_HTTP_PORT` and `DAPR_GRPC_PORT` to enable user-defined applications to easily communicate with Dapr without hard-coding Dapr port values. |
`dapr-placement` |
Used for actors only. Creates mapping tables that map actor instances to pods. |
`dapr-sentry` |
Manages mTLS between services and acts as a certificate authority. For more information, read the
|

Once Dapr is installed on your cluster, you can begin to develop using the Dapr building block APIs by [adding a few annotations](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-overview/#adding-dapr-to-a-kubernetes-deployment) to your deployments. For a more in-depth overview of the building block APIs and how to best use them, see the [Dapr building blocks overview](https://docs.dapr.io/developing-applications/building-blocks/).

Warning

If you install Dapr through the AKS or Arc-enabled Kubernetes extension, our recommendation is to continue using the extension for future management of Dapr instead of the Dapr CLI. Combining the two tools can cause conflicts and result in undesired behavior.

## Prerequisites

- An Azure subscription.
[Don't have one? Create a free account.](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) - The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli). - An existing
[AKS cluster](tutorial-kubernetes-deploy-cluster)or connected[Arc-enabled Kubernetes cluster](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster). [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)

Select how you'd like to install, deploy, and configure the Dapr extension.

## Before you begin

### Add the Azure CLI extension for cluster extensions

Install the `k8s-extension`

Azure CLI extension by running the following commands:

```
az extension add --name k8s-extension
```


If the `k8s-extension`

extension is already installed, you can update it to the latest version using the following command:

```
az extension update --name k8s-extension
```


### Register the `KubernetesConfiguration`

resource provider

If you aren't already using cluster extensions, you may need to register the resource provider with your subscription. You can check the status of the provider registration using the [az provider list](/en-us/cli/azure/provider#az-provider-list) command, as shown in the following example:

```
az provider list --query "[?contains(namespace,'Microsoft.KubernetesConfiguration')]" -o table
```


The *Microsoft.KubernetesConfiguration* provider should report as *Registered*, as shown in the following example output:

```
Namespace RegistrationState RegistrationPolicy
--------------------------------- ------------------- --------------------
Microsoft.KubernetesConfiguration Registered RegistrationRequired
```


If the provider shows as *NotRegistered*, register the provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) as shown in the following example:

```
az provider register --namespace Microsoft.KubernetesConfiguration
```


### Register the `ExtensionTypes`

feature to your Azure subscription

The `ExtensionTypes`

feature needs to be registered to your Azure subscription. In the terminal, verify you're in the correct subscription:

```
az account set --subscription <YOUR-AZURE-SUBSCRIPTION-ID>
```


Register the `ExtensionTypes`

feature.

```
az feature registration create --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


Feature registration may take some time. After a few minutes, check the registration status using the following command:

```
az feature show --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


## Create the extension and install Dapr on your AKS or Arc-enabled Kubernetes cluster

When installing the Dapr extension, use the flag value that corresponds to your cluster type:

**AKS cluster**:`--cluster-type managedClusters`

.**Arc-enabled Kubernetes cluster**:`--cluster-type connectedClusters`

.

Note

If you're using Dapr OSS on your AKS cluster and would like to install the Dapr extension for AKS, read more about [how to successfully migrate to the Dapr extension](dapr-migration).

Create the Dapr extension, which installs Dapr on your AKS or Arc-enabled Kubernetes cluster.

For example, install the latest version of Dapr via the Dapr extension on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false
```


### Keep your managed AKS cluster updated to the latest version

Based on your environment (dev, test, or production), you can keep up-to-date with the latest stable Dapr versions.

#### Choosing a release train

When configuring the extension, you can choose to install Dapr from a particular release train. Specify one of the two release train values:

| Value | Description |
|---|---|
`stable` |
Default. |
`dev` |
Early releases that can contain experimental features. Not suitable for production. |

For example:

```
--release-train stable
```


#### Configuring automatic updates to Dapr control plane

Warning

Auto-upgrade is not suitable for production environments. Only enable automatic updates to the Dapr control plane in dev or test environments. [Learn how to manually upgrade to the latest Dapr version for production environments.](#viewing-the-latest-stable-dapr-versions-available)

If you install Dapr without specifying a version, `--auto-upgrade-minor-version`

*is automatically enabled*, configuring the Dapr control plane to automatically update its minor version on new releases.

You can disable auto-update by specifying the `--auto-upgrade-minor-version`

parameter and setting the value to `false`

.

[Dapr versioning is in MAJOR.MINOR.PATCH format](https://docs.dapr.io/operations/support/support-versioning/#versioning), which means

`1.11.0`

to `1.12.0`

is a *minor*version upgrade.

```
--auto-upgrade-minor-version true
```


#### Viewing the latest stable Dapr versions available

To upgrade to the latest Dapr version in a production environment, you need to manually upgrade. Start by viewing a list of the stable Dapr versions available to your managed AKS cluster. Run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable
```


To see the latest stable Dapr version available to your managed AKS cluster, run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable --show-latest
```


To view a list of the stable Dapr versions available *by location*:

[Make sure you've registered the](dapr#register-the-extensiontypes-feature-to-your-azure-subscription)`ExtensionTypes`

feature to your Azure subscription.- Run the following command.

```
az k8s-extension extension-types list-versions-by-location --location westus --extension-type microsoft.dapr
```


[Next, manually update Dapr to the latest stable version.](#targeting-a-specific-dapr-version)

#### Targeting a specific Dapr version

Note

Dapr is supported with a rolling window, including only the current and previous versions. It is your operational responsibility to remain up to date with these supported versions. If you have an older version of Dapr, you may have to do intermediate upgrades to get to a supported version.

The same command-line argument is used for installing a specific version of Dapr or rolling back to a previous version. Set `--auto-upgrade-minor-version`

to `false`

and `--version`

to the version of Dapr you wish to install. If the `version`

parameter is omitted, the extension installs the latest version of Dapr. The following example command installs Dapr version `1.14.4-msft.10`

on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false \
--version 1.14.4-msft.10
```


## Troubleshooting

### Troubleshooting extension management errors

If the extension fails to create or update, try suggestions and solutions in the [Dapr extension troubleshooting guide](dapr-troubleshooting).

### Troubleshooting Dapr functional errors

Troubleshoot Dapr open source errors unrelated to the extension via the [common Dapr issues and solutions guide](https://docs.dapr.io/operations/troubleshooting/common_issues/).

## Support

Note

Learn more about [how Microsoft handles issues raised for the Dapr extension](dapr-overview#issue-handling).

If you're experiencing Dapr runtime security risks and regressions while using the extension, open an issue with the [Dapr open source project](https://github.com/dapr/dapr/issues/new/choose).

You could also start a discussion in the Dapr project Discord:

## Delete the Dapr extension from your cluster

The process of uninstalling the Dapr extension from AKS does not delete the CRDs created during installation. These CRDs remain in the cluster as residual components, essential for the reconciler during the installation and uninstallation of the extension.

To clean the cluster of these CRDs, you can manually delete them **after** the Dapr extension has been completely uninstalled from AKS.

### Uninstalling the extension

Delete the extension from your AKS cluster using the following command:

```
az k8s-extension delete --resource-group <myResourceGroup> --cluster-name <myAKSCluster> --cluster-type managedClusters --name dapr
```


Or, if using a Bicep template, you can delete the template.

### Listing the CRDs in your cluster

To find the CRDs you'd like to remove, run the following command:

```
kubectl get crds | findstr dapr.io
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-scheduler-configuration -->

# Scheduler configuration concepts for workload placement in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers scheduler configuration and advanced scheduling concepts for workload placement in Azure Kubernetes Service (AKS), including configurable scheduler profiles, scheduling plugins, and scheduling constraints.

## About the AKS scheduler

In AKS, the default mechanism of workload placement across nodes within a cluster is through the scheduler. The default scheduler is a control plane component responsible for assigning AKS deployment pods to nodes. Once the AKS scheduler selects a node, the deployment pod is bound to it, and the rest of the lifecycle continues.

When a pod is created without a specified node, the scheduler selects an optimal node based on several criteria, including (but not limited to):

- Available resources (CPU, memory)
[Node affinity/anti-affinity](operator-best-practices-advanced-scheduler#node-affinity)[Pod affinity/anti-affinity](operator-best-practices-advanced-scheduler#inter-pod-affinity-and-anti-affinity)[Taints and tolerations](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

### AKS scheduler configuration and scheduling strategies

By default, the AKS scheduler comes with a set of built-in rules that work well for general-purpose workloads. However, advanced use cases might require custom scheduling strategies. For example:

- Batch jobs might prefer collocating in a few nodes (for better performance) over topology-aware spreading (for reliability).
- Cost-sensitive workloads might benefit from node binpacking to consolidate jobs and minimize idle compute node costs.

To support these use cases, AKS allows you to set one or more in-tree scheduling plugins through a Kubernetes custom resource (CRD) to configure the scheduling behavior on your AKS cluster.

## Configurable scheduler profiles

A scheduler profile is a set of one or more in-tree scheduling plugins and configurations that dictate how to schedule a pod. Previously, AKS managed the scheduler configuration, and it wasn't accessible to users. Starting from Kubernetes version `1.33`

, you can now configure and set a scheduler profile (preview) for the Kubernetes scheduler on your cluster.

Each scheduler profile has the following components:

- A unique name.
- A set of
[scheduling plugins](#supported-in-tree-scheduling-plugins). - Custom arguments for fine-grained behavior (applicable to certain plugins).

## Supported in-tree scheduling plugins

AKS supports configuration of 18 in-tree Kubernetes scheduling plugins that allow pods to be placed on specific nodes, ensure pods are matched with specific storage resources, optimize for nodes with container images, and more.

The following sections walk you through these plugins, which are grouped into the following categories:

[Scheduling constraints and order-based plugins](#scheduling-constraints-and-order-based-plugins)[Node selection constraints scheduling plugins](#node-selection-constraints-scheduling-plugins)[Resource and topology optimization scheduling plugins](#resource-and-topology-optimization-scheduling-plugins)

To learn more about these plugins and configuration options, see the [Kubernetes Scheduling Plugin documentation](https://kubernetes.io/docs/reference/scheduling/config/#scheduling-plugins).

### Scheduling constraints and order-based plugins

`DefaultBinder`

: Responsible for binding the pod to a node after the scheduler selects a suitable node. Once the node is selected, the`DefaultBinder`

creates a binding object to ensure the pod is scheduled onto that node.`DefaultPreemption`

: Handles preemption, which is the process of evicting lower-priority pods to make room for higher-priority pods. If a pod can't be scheduled because there aren’t enough resources on the node, this plugin preempts other pods to make space. This plugin can receive the following arguments:`PodPriority`

: Defines the priority of the pod being scheduled.`PreemptionPolicy`

: The policy for handling pod preemption (for example:`"PreemptLowerPriority"`

or`"DoNotPreempt"`

).`PodPriorityClass`

: The priority class associated with the pod.`PodInfo`

: Information about the pods that are candidates for preemption.`Node`

: Information about the node on which preemption is considered.

`SchedulingGates`

: Introduces the concept of scheduling gates, which are conditions that must be satisfied before a pod is scheduled. For example, it can enforce the completion of certain tasks or operations before the scheduler attempts to schedule a pod.`PrioritySort`

: Sorts the list of pods according to their priority class. Pods with higher priority are scheduled first. It helps with the preemption decision-making and determines which pods to consider for priority scheduling.

### Node selection constraints scheduling plugins

`InterPodAffinity`

: Takes into account*affinity*rules specified by the user that influences scheduling based on the proximity of other pods. If a pod has affinity rules, it tries to schedule the pod on the same node or in the same topology as other pods that it has an affinity for (for example: for performance reasons or tight coupling). This plugin can receive the following arguments:`Affinity`

: Defines required or preferred affinity rules for the pod, which specifies other pods that the pod should or shouldn't be scheduled nearby.`TopologyKey`

: The key representing the failure domain to which the affinity rule applies (for example:`"kubernetes.io/hostname"`

for node-level affinity or`"topology.kubernetes.io/zone"`

for zone-level).`Weight`

: Defines how strongly the scheduler should consider a specific affinity rule.`Pod`

: The pod being scheduled.`OtherPods`

: List of other pods to consider in relation to the affinity rules.

`NodeAffinity`

: Enables scheduling based on node labels. It allows users to specify rules for which nodes a pod can be scheduled on based on the node's labels and provides fine-grained control over pod placement on nodes. This plugin can receive the following arguments:`NodeAffinity`

: Defines the required or preferred node affinity rules, such as`requiredDuringSchedulingIgnoredDuringExecution`

or`preferredDuringSchedulingIgnoredDuringExecution`

.`NodeSelectorTerms`

: Defines the set of node labels and values that must match.`Pod`

: The pod being scheduled.`Node`

: A potential node for scheduling.`LabelSelector`

: A selector for choosing nodes based on labels.

`NodeName`

: Forces pods to be scheduled on a specific node. When you specify the exact node name, the scheduler places the pod on that node if possible.`NodePorts`

: Ensures that a pod with a service of type`NodePort`

can be scheduled on a node that has the required ports available for binding. It checks whether the node has enough resources to support the node port allocations for the service.`NodeUnschedulable`

: Ensures that pods aren't scheduled on nodes marked as*unschedulable*. If a node is tainted with`node.kubernetes.io/unschedulable`

, the scheduler doesn't place any new pods on that node.`TaintToleration`

: Checks if a pod has the required tolerations to be scheduled on a node that has taints. Taints on nodes prevent pods from being scheduled unless the pod has a matching toleration.`NodeVolumeLimits`

: Checks whether a node has exceeded its volume limit. Each node has a maximum number of volumes it can attach, and this plugin ensures that the pod isn't scheduled on a node that has already reached that supported limit.`VolumeBinding`

: Ensures that persistent volumes (PVs) are properly bound to pods. It checks whether the volume that a pod requires can be bound to a node and ensures the volume is available on the selected node. This plugin can receive the following arguments:`VolumeClaims`

: The persistent volume claims (PVCs) made by the pod being scheduled.`Node`

: The candidate node being considered for scheduling.`VolumeAvailable`

: Checks if the persistent volume is available on the node or within the appropriate zone.`Pod`

: The pod that is requesting volume binding.`StorageClass`

: The storage class associated with the persistent volume.`VolumeBindingMode`

: Defines whether the volume binding mode is`Immediate`

or`WaitForFirstConsumer`

(for delayed binding until a pod is scheduled).

`VolumeRestrictions`

: Ensures that volume restrictions (such as limitations on the number of volumes a node can have attached) are respected when scheduling a pod. It prevents scheduling a pod on a node where the volume restrictions would be violated.`VolumeZone`

: Ensures that volumes are scheduled in the same availability zone as the pod. For example, if a pod requests a volume that must be in a specific zone, the plugin ensures that both the pod and the volume are in the same zone.

### Resource and topology optimization scheduling plugins

`NodeResourcesBalancedAllocation`

: Aims to balance the resource allocation on nodes. When scheduling a pod, it considers how resources like CPU and memory are allocated across nodes to avoid overprovisioning or underutilizing resources. This plugin can receive the following arguments:`ResourceRequests`

: The resource requests (CPU, memory, etc.) of the pod being scheduled.`Node`

: A candidate node for scheduling.`NodeResources`

: The available resources (CPU, memory, etc.) of the node.`ClusterResourceUsage`

: Cluster-wide resource usage metrics to help decide the best node to balance resources.

`NodeResourcesFit`

: Checks whether a node has enough available resources (CPU, memory, etc.) to run the pod. It ensures that a pod is only scheduled on a node that has sufficient resources available. This plugin can receive the following arguments:`ResourceRequests`

: The resource requests of the pod.`Node`

: The candidate node being considered for scheduling.`NodeCapacity`

: The available capacity of resources on the node.`Pod`

: The pod being scheduled, with its resource requests.

`ImageLocality`

: Helps the scheduler decide whether to schedule a pod onto a node based on the presence of a required container image. It tries to schedule pods on nodes where the required image is already present, reducing the time needed to pull the image.`PodTopologySpread`

: Ensures that pods are spread evenly across the topology (like zones or regions) to achieve high availability and fault tolerance. It tries to avoid placing multiple replicas of a pod in the same failure domain. This plugin can receive the following arguments:`TopologySpreadConstraints`

: Defines the constraints for how pods should be spread across failure domains, including the key (for example:`topology.kubernetes.io/zone`

) and the number of pods to be placed in each domain.`Pod`

: The pod being scheduled.`FailureDomain`

: The failure domain key (for example: zone or region).`PodAffinity`

: Information about pod affinity, which could also impact how the pods are distributed.`Node`

: Potential nodes for placement.`PodSpreadScore`

: Used to determine how much "spread" the pod should have across domains (higher scores indicate better spreading).


## Next step


[Configure and deploy a scheduler profile (preview) on your AKS cluster].

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-workload-identity -->

# Securely scale your applications using the KEDA add-on and workload identity on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to securely scale your applications with the Kubernetes Event-driven Autoscaling (KEDA) add-on and workload identity on Azure Kubernetes Service (AKS).

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules).

## Create a resource group

Create a resource group using the

command. Make sure you replace the placeholder values with your own values.`az group create`

`LOCATION=<azure-region> RG_NAME=<resource-group-name> az group create --name $RG_NAME --location $LOCATION`


## Create an AKS cluster

Create an AKS cluster with the KEDA add-on, workload identity, and OIDC issuer enabled using the

command with the`az aks create`

`--enable-workload-identity`

,`--enable-keda`

, and`--enable-oidc-issuer`

flags. Make sure you replace the placeholder value with your own value.`AKS_NAME=<cluster-name> az aks create \ --name $AKS_NAME \ --resource-group $RG_NAME \ --enable-workload-identity \ --enable-oidc-issuer \ --enable-keda \ --generate-ssh-keys`

Validate the deployment was successful and make sure the cluster has KEDA, workload identity, and OIDC issuer enabled using the

command with the`az aks show`

`--query`

flag set to`"[workloadAutoScalerProfile, securityProfile, oidcIssuerProfile]"`

.`az aks show \ --name $AKS_NAME \ --resource-group $RG_NAME \ --query "[workloadAutoScalerProfile, securityProfile, oidcIssuerProfile]"`

Connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --name $AKS_NAME \ --resource-group $RG_NAME \ --overwrite-existing`


## Create an Azure Service Bus

Create an Azure Service Bus namespace using the

command. Make sure to replace the placeholder value with your own value.`az servicebus namespace create`

`SB_NAME=<service-bus-name> SB_HOSTNAME="${SB_NAME}.servicebus.windows.net" az servicebus namespace create \ --name $SB_NAME \ --resource-group $RG_NAME \ --disable-local-auth`

Create an Azure Service Bus queue using the

command. Make sure to replace the placeholder value with your own value.`az servicebus queue create`

`SB_QUEUE_NAME=<service-bus-queue-name> az servicebus queue create \ --name $SB_QUEUE_NAME \ --namespace $SB_NAME \ --resource-group $RG_NAME`


## Create a managed identity

Create a managed identity using the

command. Make sure to replace the placeholder value with your own value.`az identity create`

`MI_NAME=<managed-identity-name> MI_CLIENT_ID=$(az identity create \ --name $MI_NAME \ --resource-group $RG_NAME \ --query "clientId" \ --output tsv)`

Get the OIDC issuer URL using the

command with the`az aks show`

`--query`

flag set to`oidcIssuerProfile.issuerUrl`

.`AKS_OIDC_ISSUER=$(az aks show \ --name $AKS_NAME \ --resource-group $RG_NAME \ --query oidcIssuerProfile.issuerUrl \ --output tsv)`

Create a federated credential between the managed identity and the namespace and service account used by the workload using the

command. Make sure to replace the placeholder value with your own value.`az identity federated-credential create`

`FED_WORKLOAD=<federated-credential-workload-name> az identity federated-credential create \ --name $FED_WORKLOAD \ --identity-name $MI_NAME \ --resource-group $RG_NAME \ --issuer $AKS_OIDC_ISSUER \ --subject system:serviceaccount:default:$MI_NAME \ --audience api://AzureADTokenExchange`

Create a second federated credential between the managed identity and the namespace and service account used by the keda-operator using the

command. Make sure to replace the placeholder value with your own value.`az identity federated-credential create`

`FED_KEDA=<federated-credential-keda-name> az identity federated-credential create \ --name $FED_KEDA \ --identity-name $MI_NAME \ --resource-group $RG_NAME \ --issuer $AKS_OIDC_ISSUER \ --subject system:serviceaccount:kube-system:keda-operator \ --audience api://AzureADTokenExchange`


## Create role assignments

Get the object ID for the managed identity using the

command with the`az identity show`

`--query`

flag set to`"principalId"`

.`MI_OBJECT_ID=$(az identity show \ --name $MI_NAME \ --resource-group $RG_NAME \ --query "principalId" \ --output tsv)`

Get the Service Bus namespace resource ID using the

command with the`az servicebus namespace show`

`--query`

flag set to`"id"`

.`SB_ID=$(az servicebus namespace show \ --name $SB_NAME \ --resource-group $RG_NAME \ --query "id" \ --output tsv)`

Assign the Azure Service Bus Data Owner role to the managed identity using the

command.`az role assignment create`

`az role assignment create \ --role "Azure Service Bus Data Owner" \ --assignee-object-id $MI_OBJECT_ID \ --assignee-principal-type ServicePrincipal \ --scope $SB_ID`


## Enable Workload Identity on KEDA operator

After creating the federated credential for the

`keda-operator`

ServiceAccount, you will need to manually restart the`keda-operator`

pods to ensure Workload Identity environment variables are injected into the pod.`kubectl rollout restart deploy keda-operator -n kube-system`

Confirm the keda-operator pods restart

`kubectl get pod -n kube-system -lapp=keda-operator -w`

Once you've confirmed the keda-operator pods have finished rolling hit

`Ctrl+c`

to break the previous watch command then confirm the Workload Identity environment variables have been injected.`KEDA_POD_ID=$(kubectl get po -n kube-system -l app.kubernetes.io/name=keda-operator -ojsonpath='{.items[0].metadata.name}') kubectl describe po $KEDA_POD_ID -n kube-system`

You should see output similar to the following under

**Environment**.`--- AZURE_CLIENT_ID: AZURE_TENANT_ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx AZURE_FEDERATED_TOKEN_FILE: /var/run/secrets/azure/tokens/azure-identity-token AZURE_AUTHORITY_HOST: https://login.microsoftonline.com/ ---`

Deploy a KEDA TriggerAuthentication resource that includes the User-Assigned Managed Identity's Client ID.

`kubectl apply -f - <<EOF apiVersion: keda.sh/v1alpha1 kind: TriggerAuthentication metadata: name: azure-servicebus-auth namespace: default # this must be same namespace as the ScaledObject/ScaledJob that will use it spec: podIdentity: provider: azure-workload identityId: $MI_CLIENT_ID EOF`

Note

With the TriggerAuthentication in place, KEDA will be able to authenticate via workload identity. The

`keda-operator`

Pods use the`identityId`

to authenticate against Azure resources when evaluating scaling triggers.

## Publish messages to Azure Service Bus

At this point everything is configured for scaling with KEDA and Microsoft Entra Workload Identity. We will test this by deploying producer and consumer workloads.

Create a new ServiceAccount for the workloads.

`kubectl apply -f - <<EOF apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: $MI_CLIENT_ID name: $MI_NAME EOF`

Deploy a Job to publish 100 messages.

`kubectl apply -f - <<EOF apiVersion: batch/v1 kind: Job metadata: name: myproducer spec: template: metadata: labels: azure.workload.identity/use: "true" spec: serviceAccountName: $MI_NAME containers: - image: ghcr.io/azure-samples/aks-app-samples/servicebusdemo:latest name: myproducer resources: {} env: - name: OPERATION_MODE value: "producer" - name: MESSAGE_COUNT value: "100" - name: AZURE_SERVICEBUS_QUEUE_NAME value: $SB_QUEUE_NAME - name: AZURE_SERVICEBUS_HOSTNAME value: $SB_HOSTNAME restartPolicy: Never EOF`


## Consume messages from Azure Service Bus

Now that we have published messages to the Azure Service Bus queue, we will deploy a ScaledJob to consume the messages. This ScaledJob will use the KEDA TriggerAuthentication resource to authenticate against the Azure Service Bus queue using the workload identity and scale out every 10 messages.

Deploy a ScaledJob resource to consume the messages. The scale trigger will be configured to scale out every 10 messages. The KEDA scaler will create 10 jobs to consume the 100 messages.

`kubectl apply -f - <<EOF apiVersion: keda.sh/v1alpha1 kind: ScaledJob metadata: name: myconsumer-scaledjob spec: jobTargetRef: template: metadata: labels: azure.workload.identity/use: "true" spec: serviceAccountName: $MI_NAME containers: - image: ghcr.io/azure-samples/aks-app-samples/servicebusdemo:latest name: myconsumer env: - name: OPERATION_MODE value: "consumer" - name: MESSAGE_COUNT value: "10" - name: AZURE_SERVICEBUS_QUEUE_NAME value: $SB_QUEUE_NAME - name: AZURE_SERVICEBUS_HOSTNAME value: $SB_HOSTNAME restartPolicy: Never triggers: - type: azure-servicebus metadata: queueName: $SB_QUEUE_NAME namespace: $SB_NAME messageCount: "10" authenticationRef: name: azure-servicebus-auth EOF`

Note

ScaledJob creates a Kubernetes Job resource whenever a scaling event occurs and thus a Job template needs to be passed in when creating the resource. As new Jobs are created, Pods will be deployed with workload identity bits to consume messages.

Verify the KEDA scaler worked as intended.

`kubectl describe scaledjob myconsumer-scaledjob`

You should see events similar to the following.

`Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal KEDAScalersStarted 10m scale-handler Started scalers watch Normal ScaledJobReady 10m keda-operator ScaledJob is ready for scaling Warning KEDAScalerFailed 10m scale-handler context canceled Normal KEDAJobsCreated 10m scale-handler Created 10 jobs`


## Clean up resources

After you verify that the deployment is successful, you can clean up the resources to avoid incurring Azure costs.

Delete the Azure resource group and all resources in it using the [

`az group delete`

][az-group-delete] command.`az group delete --name $RG_NAME --yes --no-wait`


## Next steps

This article showed you how to securely scale your applications using the KEDA add-on and workload identity in AKS.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more about KEDA, see the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ha-dr-overview -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-fine-tune-language-models -->

# Concepts - Fine-tuning language models for AI and machine learning workflows

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about fine-tuning [language models](concepts-ai-ml-language-models), including some common methods and how applying the tuning results can improve the performance of your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## Pre-trained language models

*Pre-trained language models (PLMs)* offer an accessible way to get started with AI inferencing and are widely used in natural language processing (NLP). PLMs are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks. These models typically consist of billions of parameters, or *weights*, that are learned during the pre-training process.

PLMs can learn universal language representations that capture the statistical properties of natural language, such as the probability of words or sequences of words occurring in a given context. These representations can be transferred to downstream tasks, such as text classification, named entity recognition, and question answering, by fine-tuning the model on task-specific datasets.

### Pros and cons

The following table lists some pros and cons of using PLMs in your AI and machine learning workflows:

| Pros | Cons |
|---|---|
| • Get started quickly with deployment in your machine learning lifecycle. • Avoid heavy compute costs associated with model training. • Reduces the need to store large, labeled datasets. |
• Might provide generalized or outdated responses based on pre-training data sources. • Might not be suitable for all tasks or domains. • Performance can vary depending on inferencing context. |

## Fine-tuning methods

### Parameter efficient fine-tuning

*Parameter efficient fine-tuning (PEFT)* is a method for fine-tuning PLMs on relatively small datasets with limited compute resources. PEFT uses a combination of techniques, like additive and selective methods to update weights, to improve the performance of the model on specific tasks. PEFT requires minimal compute resources and flexible quantities of data, making it suitable for low-resource settings. This method retains most of the weights of the original pre-trained model and updates the remaining weights to fit context-specific, labeled data.

### Low rank adaptation

*Low rank adaptation (LoRA)* is a PEFT method commonly used to customize large language models for new tasks. This method tracks changes to model weights and efficiently stores smaller weight matrices that represent only the model's trainable parameters, reducing memory usage and the compute power needed for fine-tuning. LoRA creates fine-tuning results, known as *adapter layers*, that can be temporarily stored and pulled into the model's architecture for new inferencing jobs.

*Quantized low rank adaptation (QLoRA)* is an extension of LoRA that further reduces memory usage by introducing quantization to the adapter layers. For more information, see [Making LLMs even more accessible with bitsandbites, 4-bit quantization, and QLoRA](https://huggingface.co/blog/4bit-transformers-bitsandbytes#:%7E:text=We%20present%20QLoRA%2C%20an%20efficient%20finetuning%20approach%20that,pretrained%20language%20model%20into%20Low%20Rank%20Adapters%7E%20%28LoRA%29.).

## Experiment with fine-tuning language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The AI toolchain operator add-on leverages KAITO to simplify onboarding, save on infrastructure costs, and reduce the time-to-inference for open-source models on an AKS cluster. The add-on automatically provisions right-sized GPU nodes and sets up the associated inference server as an endpoint server to your chosen model.

With KAITO version 0.3.0 or later, you can efficiently fine-tune supported MIT and Apache 2.0 licensed models with the following features:

- Store your retraining data as a container image in a private container registry.
- Host the new adapter layer image in a private container registry.
- Efficiently pull the image for inferencing with adapter layers in new scenarios.

For guidance on getting started with fine-tuning on KAITO, see the [Kaito Tuning Workspace API documentation][kaito-fine-tuning]. To learn more about deploying language models with KAITO in your AKS clusters, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-services -->

# Kubernetes Services in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use Kubernetes Services to logically group pods and provide network connectivity by allowing direct access to them through a specific IP address or DNS name on a designated port. This allows you to expose your application workloads to other services within the cluster or to external clients without having to manually manage the network configuration for each pod hosting a workload.

You can specify what kind of service you want using Kubernetes *Service type values*. For more information, see the

[Kubernetes Service documentation](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types).

The following Service types are available in AKS: [ ClusterIP](#clusterip),

[,](#nodeport)

`NodePort`

[, and](#loadbalancer)

`LoadBalancer`

[.](#externalname)

`ExternalName`

## ClusterIP

`ClusterIP`

creates an internal IP address for use within the AKS cluster. The `ClusterIP`

Service is good for *internal-only applications* that support other workloads within the cluster. ClusterIP is used by default if you don't explicitly specify a type for a Service.


## NodePort

`NodePort`

creates a port mapping on the underlying node that allows the application to be accessed directly with the node IP address and port.


## LoadBalancer

`LoadBalancer`

creates an Azure load balancer resource, configures an external IP address, and connects the requested pods to the load balancer backend pool. To allow customer traffic to reach the application, load balancing rules are created on the desired ports.


For HTTP load balancing of inbound traffic, you can also use an [Ingress controller](concepts-network-ingress#ingress-controllers).

You can also use the `LoadBalancer`

type to create multiple public load balancers in a single AKS cluster. This is useful for large clusters or port-heavy workloads that can quickly exhaust the limits of a single load balancer. For more information, see [Use multiple public load balancers in Azure Kubernetes Service (preview)](use-multiple-standard-load-balancer).

## ExternalName

`ExternalName`

creates a specific DNS entry for easier application access. You can dynamically assign the load balancers and service IP address, or you can specify an existing static IP address. You can assign both internal and external static IP addresses. Existing static IP addresses are often tied to a DNS entry.

You can create both *internal* and *external* load balancers. Internal load balancers are only assigned a private IP address, so they can't be accessed from the Internet.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-hybrid-benefit -->

# What is Azure Hybrid Benefit for Azure Kubernetes Service?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Hybrid Benefit is a program that enables you to significantly reduce the costs of running workloads in the cloud. With Azure Hybrid Benefit for Azure Kubernetes Service (AKS), you can maximize the value of your on-premises licenses and modernize your applications at no extra cost. Azure Hybrid Benefit enables you to use your on-premises licenses that also have either active Software Assurance (SA) or a qualifying subscription to get Windows virtual machines (VMs) on Azure at a reduced cost.

For more information on qualifications for Azure Hybrid Benefit, what is included with it, how to stay compliant, and more, check out [Azure Hybrid Benefit for Windows Server](/en-us/azure/virtual-machines/windows/hybrid-use-benefit-licensing).

Note

Azure Hybrid Benefit for Azure Kubernetes Service follows the same licensing guidance as Azure Hybrid Benefit for Windows Server VMs on Azure.

## Enable Azure Hybrid Benefit for Azure Kubernetes Service

Azure Hybrid Benefit for Azure Kubernetes Service can be enabled at cluster creation or on an existing AKS cluster. You can enable and disable Azure Hybrid Benefit using either the Azure CLI or Azure PowerShell. In the following examples, be sure to replace the variable definitions with values matching your own cluster.

To create a new AKS cluster with Azure Hybrid Benefit enabled:

```
PASSWORD='' # replace with your own password value
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks create \
--resource-group $RG_NAME \
--name $CLUSTER \
--load-balancer-sku Standard \
--network-plugin azure \
--windows-admin-username azure \
--windows-admin-password $PASSWORD \
--enable-ahub \
--generate-ssh-keys
```


To enable Azure Hybrid Benefit on an existing AKS cluster:

```
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks update --resource-group $RG_NAME --name $CLUSTER--enable-ahub
```


## Disable Azure Hybrid Benefit for Azure Kubernetes Service

To disable Azure Hybrid Benefit for an AKS cluster:

```
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks update --resource-group $RG_NAME --name $CLUSTER --disable-ahub
```


## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-identity-access -->

# Connect your Azure identity provider to the Azure Key Vault Secrets Store CSI Driver in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Secrets Store Container Storage Interface (CSI) Driver on Azure Kubernetes Service (AKS) provides various methods of identity-based access to your Azure Key Vault. This article outlines these methods and best practices for when to use Azure role-based access control (Azure RBAC) or OpenID Connect (OIDC) security models to access your key vault and AKS cluster.

You can use one of the following access methods:

- Service Connector with managed identity
- Workload ID
- User-assigned managed identity

Learn how to connect to Azure Key Vault with the Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster using Service Connector. In this article, you complete the following tasks:

- Create an AKS cluster and an Azure Key Vault.
- Create a connection between the AKS cluster and the Azure Key Vault with Service Connector.
- Create a
`SecretProviderClass`

CRD and a`Pod`

that consumes the CSI provider to test the connection. - Clean up resources.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The
[Azure CLI](/en-us/cli/azure/install-azure-cli). Sign in using thecommand.`az login`

[Docker](https://docs.docker.com/get-docker/)and[kubectl](https://kubernetes.io/docs/tasks/tools/). To install kubectl locally, use thecommand.`az aks install-cli`

- A basic understanding of containers and AKS. Get started by
[preparing an application for AKS](/en-us/azure/aks/tutorial-kubernetes-prepare-app). - Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster.

## Initial set-up

If you're using Service Connector for the first time, start by running the command

[az provider register](/en-us/cli/azure/provider#az-provider-register)to register the Service Connector and Kubernetes Configuration resource providers.`az provider register -n Microsoft.ServiceLinker`

`az provider register -n Microsoft.KubernetesConfiguration`

Tip

You can check if these resource providers have already been registered by running the commands

`az provider show -n "Microsoft.ServiceLinker" --query registrationState`

and`az provider show -n "Microsoft.KubernetesConfiguration" --query registrationState`

.Optionally, use the Azure CLI command to get a list of supported target services for AKS cluster.

`az aks connection list-support-types --output table`


## Create Azure resources

Create a resource group using the

command.`az group create`

`az group create \ --name <resource-group-name> \ --location <location>`

Create an AKS cluster using the

command. The following example creates a single-node AKS cluster with managed identity enabled.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --enable-managed-identity \ --node-count 1`

Connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group <resource-group-name> \ --name <cluster-name>`

Create an Azure key vault using the

command.`az keyvault create`

`az keyvault create \ --resource-group <resource-group-name> \ --name <key-vault-name> \ --location <location>`

Create a secret in the key vault using the

command.`az keyvault secret set`

`az keyvault secret set \ --vault-name <key-vault-name> \ --name <secret-name> \ --value <secret-value>`


## Create a service connection in AKS with Service Connector

You can create a service connection to Azure Key Vault using the Azure portal or Azure CLI.

In the Azure portal, navigate to your AKS cluster resource.

From the service menu, under

**Settings**, select**Service Connector**>**Create**.On the

**Create connection**page, configure the following settings in the**Basics**tab:**Kubernetes namespace**: Select**default**.**Service type**: Select**Key Vault**and select the checkbox to enable the Azure Key Vault CSI Provider.**Connection name**: Enter a name for the connection.**Subscription**: Select the subscription that contains the key vault.**Key vault**: Select the key vault you created.**Client type**: Select**None**.

Select

**Review + create**, and then select**Create**to create the connection.

## Test the connection

### Clone the sample repo and deploy manifest files

Clone the sample repository using the

`git clone`

command.`git clone https://github.com/Azure-Samples/serviceconnector-aks-samples.git`

Change directories to the Azure Key Vault CSI provider sample.

`cd serviceconnector-aks-samples/azure-keyvault-csi-provider`

In the

`secret_provider_class.yaml`

file, replace the following placeholders with your Azure Key Vault information:- Replace
`<AZURE_KEYVAULT_NAME>`

with the name of the key vault you created and connected. - Replace
`<AZURE_KEYVAULT_TENANTID>`

with the tenant ID of the key vault. - Replace
`<AZURE_KEYVAULT_CLIENTID>`

with identity client ID of the`azureKeyvaultSecretsProvider`

addon. - Replace
`<KEYVAULT_SECRET_NAME>`

with the key vault secret you created. For example,`ExampleSecret`

.

- Replace
Deploy the

`SecretProviderClass`

CRD using the`kubectl apply`

command.`kubectl apply -f secret_provider_class.yaml`

Deploy the

`Pod`

manifest file using the`kubectl apply`

command.The command creates a pod named

`sc-demo-keyvault-csi`

in the default namespace of your AKS cluster.`kubectl apply -f pod.yaml`


### Verify the connection

Verify the pod was created successfully using the

`kubectl get`

command.`kubectl get pod/sc-demo-keyvault-csi`

After the pod starts, the mounted content at the volume path specified in your deployment YAML is available.

Show the secrets held in the secrets store using the

`kubectl exec`

command.`kubectl exec sc-demo-keyvault-csi -- ls /mnt/secrets-store/`

Display a secret using the

`kubectl exec`

command.This example command shows a test secret named

`ExampleSecret`

.`kubectl exec sc-demo-keyvault-csi -- cat /mnt/secrets-store/ExampleSecret`


## Prerequisites for CSI Driver

- Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster. - Microsoft Entra Workload ID supports both Windows and Linux clusters.

## Access with a Microsoft Entra Workload ID

A [Microsoft Entra Workload ID](workload-identity-overview) is an identity that an application running on a pod uses to authenticate itself against other Azure services, such as workloads in software. The Secret Store CSI Driver integrates with native Kubernetes capabilities to federate with external identity providers.

In this security model, the AKS cluster acts as token issuer. Microsoft Entra ID then uses OIDC to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. For your workload to exchange a service account token projected to its volume for a Microsoft Entra token, you need the Azure Identity client library in the Azure SDK or the Microsoft Authentication Library (MSAL)

Note

- This authentication method replaces Microsoft Entra pod-managed identity (preview). The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated as of October 24, 2022.
- Microsoft Entra Workload ID supports both Windows and Linux clusters.

### Configure workload identity

Set your subscription using the

command.`az account set`

`export SUBSCRIPTION_ID=<subscription id> export RESOURCE_GROUP=<resource group name> export UAMI=<name for user assigned identity> export KEYVAULT_NAME=<existing keyvault name> export CLUSTER_NAME=<aks cluster name> az account set --subscription $SUBSCRIPTION_ID`

Create a managed identity using the

command.`az identity create`

Note

This step assumes you have an existing AKS cluster with workload identity enabled. If workload identity isn't enabled, see

[Enable workload identity on an existing AKS cluster](workload-identity-deploy-cluster#enable-oidc-issuer-and-microsoft-entra-workload-id-on-an-aks-cluster)to enable it.`az identity create --name $UAMI --resource-group $RESOURCE_GROUP export USER_ASSIGNED_CLIENT_ID="$(az identity show --resource-group $RESOURCE_GROUP --name $UAMI --query 'clientId' -o tsv)" export IDENTITY_TENANT=$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query identity.tenantId -o tsv)`

Create a role assignment that grants the workload identity permission to access the key vault secrets, access keys, and certificates using the

command.`az role assignment create`

Important

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`key`

or`certificate`

type, assign therole to give permissions.`Key Vault Certificate User`

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`secret`

type, assign therole.`Key Vault Secrets User`

- If your key vault isn't set with
`--enable-rbac-authorization`

, you can use thecommand with the`az keyvault set-policy`

`--key-permissions get`

,`--certificate-permissions get`

, or`--secret-permissions get`

parameter to create a key vault policy to grant access for keys, certificates, or secrets. For example:

`az keyvault set-policy --name $KEYVAULT_NAME --key-permissions get --object-id $IDENTITY_OBJECT_ID`

`export KEYVAULT_SCOPE=$(az keyvault show --name $KEYVAULT_NAME --query id -o tsv) # Example command for key vault with Azure RBAC enabled using `key` type az role assignment create --role "Key Vault Certificate User" --assignee $USER_ASSIGNED_CLIENT_ID --scope $KEYVAULT_SCOPE`

- If your key vault is set with
Get the AKS cluster OIDC Issuer URL using the

command.`az aks show`

Note

This step assumes you have an existing AKS cluster with the OIDC Issuer URL enabled. If the OIDC Issuer URL isn't enabled, see

[Update an AKS cluster with OIDC Issuer](use-oidc-issuer#enable-the-oidc-issuer-on-an-existing-aks-cluster)to enable it.`export AKS_OIDC_ISSUER="$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query "oidcIssuerProfile.issuerUrl" -o tsv)" echo $AKS_OIDC_ISSUER`

Establish a federated identity credential between the Microsoft Entra application, service account issuer, and subject. Get the object ID of the Microsoft Entra application using the following commands. Make sure to update the values for

`serviceAccountName`

and`serviceAccountNamespace`

with the Kubernetes service account name and its namespace.`export SERVICE_ACCOUNT_NAME="workload-identity-sa" # sample name; can be changed export SERVICE_ACCOUNT_NAMESPACE="default" # can be changed to namespace of your workload cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${USER_ASSIGNED_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`

Create the federated identity credential between the managed identity, service account issuer, and subject using the

command.`az identity federated-credential create`

`export FEDERATED_IDENTITY_NAME="aksfederatedidentity" # can be changed as needed az identity federated-credential create --name $FEDERATED_IDENTITY_NAME --identity-name $UAMI --resource-group $RESOURCE_GROUP --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME}`

Deploy a

`SecretProviderClass`

using the`kubectl apply`

command and the following YAML script.`cat <<EOF | kubectl apply -f - # This is a SecretProviderClass example using workload identity to access your key vault apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-kvname-wi # needs to be unique per namespace spec: provider: azure parameters: usePodIdentity: "false" clientID: "${USER_ASSIGNED_CLIENT_ID}" # Setting this to use workload identity keyvaultName: ${KEYVAULT_NAME} # Set to the name of your key vault cloudName: "" # [OPTIONAL for Azure] if not provided, the Azure environment defaults to AzurePublicCloud objects: | array: - | objectName: secret1 # Set to the name of your secret objectType: secret # object types: secret, key, or cert objectVersion: "" # [OPTIONAL] object versions, default to latest if empty - | objectName: key1 # Set to the name of your key objectType: key objectVersion: "" tenantId: "${IDENTITY_TENANT}" # The tenant ID of the key vault EOF`

Note

If you use

`objectAlias`

instead of`objectName`

, update the YAML script to account for it.Note

In order for the

`SecretProviderClass`

to function properly, make sure to populate your Azure Key Vault with secrets, keys, or certificates before referencing them in the`objects`

section.Deploy a sample pod using the

`kubectl apply`

command and the following YAML script.`cat <<EOF | kubectl apply -f - # This is a sample pod definition for using SecretProviderClass and workload identity to access your key vault kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline-wi labels: azure.workload.identity/use: "true" spec: serviceAccountName: "workload-identity-sa" containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-kvname-wi" EOF`


## Prerequisites for CSI Driver

- Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster.

## Access with managed identity

A [Microsoft Entra Managed ID](/en-us/entra/identity/managed-identities-azure-resources/overview) is an identity that an administrator uses to authenticate themselves against other Azure services. The managed identity uses Azure RBAC to federate with external identity providers.

In this security model, you can grant access to your cluster's resources to team members or tenants sharing a managed role. The role is checked for scope to access the keyvault and other credentials. When you [enabled the Azure Key Vault provider for Secrets Store CSI Driver on your AKS Cluster](csi-secrets-store-driver#create-an-aks-cluster-with-azure-key-vault-provider-for-secrets-store-csi-driver-support), it created a user identity.

### Configure managed identity

Access your key vault using the

command and the user-assigned managed identity created by the add-on. You should also retrieve the identity's`az aks show`

`clientId`

, which you use in later steps when creating a`SecretProviderClass`

.`az aks show --resource-group <resource-group> --name <cluster-name> --query addonProfiles.azureKeyvaultSecretsProvider.identity.objectId -o tsv az aks show --resource-group <resource-group> --name <cluster-name> --query addonProfiles.azureKeyvaultSecretsProvider.identity.clientId -o tsv`

Alternatively, you can create a new managed identity and assign it to your virtual machine (VM) scale set or to each VM instance in your availability set using the following commands.

`az identity create --resource-group <resource-group> --name <identity-name> az vmss identity assign --resource-group <resource-group> --name <agent-pool-vmss> --identities <identity-resource-id> az vm identity assign --resource-group <resource-group> --name <agent-pool-vm> --identities <identity-resource-id> az identity show --resource-group <resource-group> --name <identity-name> --query 'clientId' -o tsv`

Create a role assignment that grants the identity permission to access the key vault secrets, access keys, and certificates using the

command.`az role assignment create`

Important

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`key`

or`certificate`

type, assign therole.`Key Vault Certificate User`

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`secret`

type, assign therole.`Key Vault Secrets User`

- If your key vault isn't set with
`--enable-rbac-authorization`

, you can use thecommand with the`az keyvault set-policy`

`--key-permissions get`

,`--certificate-permissions get`

, or`--secret-permissions get`

parameter to create a key vault policy to grant access for keys, certificates, or secrets. For example:

`az keyvault set-policy --name $KEYVAULT_NAME --key-permissions get --object-id $IDENTITY_OBJECT_ID`

`export IDENTITY_OBJECT_ID="$(az identity show --resource-group <resource-group> --name <identity-name> --query 'principalId' -o tsv)" export KEYVAULT_SCOPE=$(az keyvault show --name <key-vault-name> --query id -o tsv) # Example command for key vault with Azure RBAC enabled using `key` type az role assignment create --role "Key Vault Certificate User" --assignee $USER_ASSIGNED_CLIENT_ID --scope $KEYVAULT_SCOPE`

- If your key vault is set with
Create a

`SecretProviderClass`

using the following YAML. Make sure to use your own values for`userAssignedIdentityID`

,`keyvaultName`

,`tenantId`

, and the objects to retrieve from your key vault.`# This is a SecretProviderClass example using user-assigned identity to access your key vault apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-kvname-user-msi spec: provider: azure parameters: usePodIdentity: "false" useVMManagedIdentity: "true" # Set to true for using managed identity userAssignedIdentityID: <client-id> # Set the clientID of the user-assigned managed identity to use keyvaultName: <key-vault-name> # Set to the name of your key vault cloudName: "" # [OPTIONAL for Azure] if not provided, the Azure environment defaults to AzurePublicCloud objects: | array: - | objectName: secret1 objectType: secret # object types: secret, key, or cert objectVersion: "" # [OPTIONAL] object versions, default to latest if empty - | objectName: key1 objectType: key objectVersion: "" tenantId: <tenant-id> # The tenant ID of the key vault`

Note

If you use

`objectAlias`

instead of`objectName`

, make sure to update the YAML script.Note

In order for the

`SecretProviderClass`

to function properly, make sure to populate your Azure Key Vault with secrets, keys, or certificates before referencing them in the`objects`

section.Apply the

`SecretProviderClass`

to your cluster using the`kubectl apply`

command.`kubectl apply -f secretproviderclass.yaml`

Create a pod using the following YAML.

`# This is a sample pod definition for using SecretProviderClass and the user-assigned identity to access your key vault kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline-user-msi spec: containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-kvname-user-msi"`

Apply the pod to your cluster using the

`kubectl apply`

command.`kubectl apply -f pod.yaml`


## Validate Key Vault secrets

After the pod starts, the mounted content at the volume path specified in your deployment YAML is available. Use the following commands to validate your secrets and print a test secret.

Show secrets held in the secrets store using the following command.

`kubectl exec busybox-secrets-store-inline-user-msi -- ls /mnt/secrets-store/`

Display a secret in the store using the following command. This example command shows the test secret

`ExampleSecret`

.`kubectl exec busybox-secrets-store-inline-user-msi -- cat /mnt/secrets-store/ExampleSecret`


## Obtain certificates and keys

The Azure Key Vault design makes sharp distinctions between keys, secrets, and certificates. The certificate features of the Key Vault service are designed to make use of key and secret capabilities. When you create a key vault certificate, it creates an addressable key and secret with the same name. This key allows authentication operations, and the secret allows the retrieval of the certificate value as a secret.

A key vault certificate also contains public x509 certificate metadata. The key vault stores both the public and private components of your certificate in a secret. You can obtain each individual component by specifying the `objectType`

in `SecretProviderClass`

. The following table shows which objects map to the various resources associated with your certificate:

| Object | Return value | Returns entire certificate chain |
|---|---|---|
`key` |
The public key, in Privacy Enhanced Mail (PEM) format. | N/A |
`cert` |
The certificate, in PEM format. | No |
`secret` |
The private key and certificate, in PEM format. | Yes |

## Disable the addon on existing clusters

Note

Before you disable the add-on, ensure that *no* `SecretProviderClass`

is in use. Trying to disable the add-on while a `SecretProviderClass`

exists results in an error.

Disable the Azure Key Vault provider for Secrets Store CSI Driver capability in an existing cluster using the [ az aks disable-addons](/en-us/cli/azure/aks#az-aks-disable-addons) command with the

`azure-keyvault-secrets-provider`

add-on.```
az aks disable-addons --addons azure-keyvault-secrets-provider --resource-group myResourceGroup --name myAKSCluster
```


Note

When you disable the add-on, existing workloads should have no issues or see any updates in the mounted secrets. If the pod restarts or a new pod is created as part of scale-up event, the pod fails to start because the driver is no longer running.

## Next steps

In this article, you learned how to create and provide an identity to access your Azure Key Vault. The [Service Connector](/en-us/azure/service-connector/overview) integration helps simplify the connection configuration for AKS workloads and Azure backing services. It securely handles authentication and network configurations and follows best practices for connecting to Azure services. For more information, see [Use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster](/en-us/azure/service-connector/tutorial-python-aks-keyvault-csi-driver) and the [Service Connector introduction](https://blog.aks.azure.com/2024/05/23/service-connector-intro).

If you want to configure extra configuration options or perform troubleshooting, see [Configuration options and troubleshooting resources for Azure Key Vault provider with Secrets Store CSI Driver in AKS](csi-secrets-store-configuration-options).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-multi-region -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr -->

# Install the Dapr extension for Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Dapr](dapr-overview) simplifies building resilient, stateless, and stateful applications that run on the cloud and edge and embrace the diversity of languages and developer frameworks. With Dapr's sidecar architecture, you can keep your code platform agnostic while tackling challenges around building microservices, like:

- Calling other services reliably and securely
- Building event-driven apps with pub/sub
- Building applications that are portable across multiple cloud services and hosts (for example, Kubernetes vs. a virtual machine)

Note

If you plan on installing Dapr in a Kubernetes production environment, see the [Dapr guidelines for production usage](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-production) documentation page.

## How it works

The Dapr extension uses the Azure CLI or a Bicep template to provision the Dapr control plane on your AKS or Arc-enabled Kubernetes cluster, creating the following Dapr services:

| Dapr service | Description |
|---|---|
`dapr-operator` |
Manages component updates and Kubernetes services endpoints for Dapr (state stores, pub/subs, etc.) |
`dapr-sidecar-injector` |
Injects Dapr into annotated deployment pods and adds the environment variables `DAPR_HTTP_PORT` and `DAPR_GRPC_PORT` to enable user-defined applications to easily communicate with Dapr without hard-coding Dapr port values. |
`dapr-placement` |
Used for actors only. Creates mapping tables that map actor instances to pods. |
`dapr-sentry` |
Manages mTLS between services and acts as a certificate authority. For more information, read the
|

Once Dapr is installed on your cluster, you can begin to develop using the Dapr building block APIs by [adding a few annotations](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-overview/#adding-dapr-to-a-kubernetes-deployment) to your deployments. For a more in-depth overview of the building block APIs and how to best use them, see the [Dapr building blocks overview](https://docs.dapr.io/developing-applications/building-blocks/).

Warning

If you install Dapr through the AKS or Arc-enabled Kubernetes extension, our recommendation is to continue using the extension for future management of Dapr instead of the Dapr CLI. Combining the two tools can cause conflicts and result in undesired behavior.

## Prerequisites

- An Azure subscription.
[Don't have one? Create a free account.](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) - The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli). - An existing
[AKS cluster](tutorial-kubernetes-deploy-cluster)or connected[Arc-enabled Kubernetes cluster](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster). [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)

Select how you'd like to install, deploy, and configure the Dapr extension.

## Before you begin

### Add the Azure CLI extension for cluster extensions

Install the `k8s-extension`

Azure CLI extension by running the following commands:

```
az extension add --name k8s-extension
```


If the `k8s-extension`

extension is already installed, you can update it to the latest version using the following command:

```
az extension update --name k8s-extension
```


### Register the `KubernetesConfiguration`

resource provider

If you aren't already using cluster extensions, you may need to register the resource provider with your subscription. You can check the status of the provider registration using the [az provider list](/en-us/cli/azure/provider#az-provider-list) command, as shown in the following example:

```
az provider list --query "[?contains(namespace,'Microsoft.KubernetesConfiguration')]" -o table
```


The *Microsoft.KubernetesConfiguration* provider should report as *Registered*, as shown in the following example output:

```
Namespace RegistrationState RegistrationPolicy
--------------------------------- ------------------- --------------------
Microsoft.KubernetesConfiguration Registered RegistrationRequired
```


If the provider shows as *NotRegistered*, register the provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) as shown in the following example:

```
az provider register --namespace Microsoft.KubernetesConfiguration
```


### Register the `ExtensionTypes`

feature to your Azure subscription

The `ExtensionTypes`

feature needs to be registered to your Azure subscription. In the terminal, verify you're in the correct subscription:

```
az account set --subscription <YOUR-AZURE-SUBSCRIPTION-ID>
```


Register the `ExtensionTypes`

feature.

```
az feature registration create --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


Feature registration may take some time. After a few minutes, check the registration status using the following command:

```
az feature show --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


## Create the extension and install Dapr on your AKS or Arc-enabled Kubernetes cluster

When installing the Dapr extension, use the flag value that corresponds to your cluster type:

**AKS cluster**:`--cluster-type managedClusters`

.**Arc-enabled Kubernetes cluster**:`--cluster-type connectedClusters`

.

Note

If you're using Dapr OSS on your AKS cluster and would like to install the Dapr extension for AKS, read more about [how to successfully migrate to the Dapr extension](dapr-migration).

Create the Dapr extension, which installs Dapr on your AKS or Arc-enabled Kubernetes cluster.

For example, install the latest version of Dapr via the Dapr extension on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false
```


### Keep your managed AKS cluster updated to the latest version

Based on your environment (dev, test, or production), you can keep up-to-date with the latest stable Dapr versions.

#### Choosing a release train

When configuring the extension, you can choose to install Dapr from a particular release train. Specify one of the two release train values:

| Value | Description |
|---|---|
`stable` |
Default. |
`dev` |
Early releases that can contain experimental features. Not suitable for production. |

For example:

```
--release-train stable
```


#### Configuring automatic updates to Dapr control plane

Warning

Auto-upgrade is not suitable for production environments. Only enable automatic updates to the Dapr control plane in dev or test environments. [Learn how to manually upgrade to the latest Dapr version for production environments.](#viewing-the-latest-stable-dapr-versions-available)

If you install Dapr without specifying a version, `--auto-upgrade-minor-version`

*is automatically enabled*, configuring the Dapr control plane to automatically update its minor version on new releases.

You can disable auto-update by specifying the `--auto-upgrade-minor-version`

parameter and setting the value to `false`

.

[Dapr versioning is in MAJOR.MINOR.PATCH format](https://docs.dapr.io/operations/support/support-versioning/#versioning), which means

`1.11.0`

to `1.12.0`

is a *minor*version upgrade.

```
--auto-upgrade-minor-version true
```


#### Viewing the latest stable Dapr versions available

To upgrade to the latest Dapr version in a production environment, you need to manually upgrade. Start by viewing a list of the stable Dapr versions available to your managed AKS cluster. Run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable
```


To see the latest stable Dapr version available to your managed AKS cluster, run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable --show-latest
```


To view a list of the stable Dapr versions available *by location*:

[Make sure you've registered the](dapr#register-the-extensiontypes-feature-to-your-azure-subscription)`ExtensionTypes`

feature to your Azure subscription.- Run the following command.

```
az k8s-extension extension-types list-versions-by-location --location westus --extension-type microsoft.dapr
```


[Next, manually update Dapr to the latest stable version.](#targeting-a-specific-dapr-version)

#### Targeting a specific Dapr version

Note

Dapr is supported with a rolling window, including only the current and previous versions. It is your operational responsibility to remain up to date with these supported versions. If you have an older version of Dapr, you may have to do intermediate upgrades to get to a supported version.

The same command-line argument is used for installing a specific version of Dapr or rolling back to a previous version. Set `--auto-upgrade-minor-version`

to `false`

and `--version`

to the version of Dapr you wish to install. If the `version`

parameter is omitted, the extension installs the latest version of Dapr. The following example command installs Dapr version `1.14.4-msft.10`

on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false \
--version 1.14.4-msft.10
```


## Troubleshooting

### Troubleshooting extension management errors

If the extension fails to create or update, try suggestions and solutions in the [Dapr extension troubleshooting guide](dapr-troubleshooting).

### Troubleshooting Dapr functional errors

Troubleshoot Dapr open source errors unrelated to the extension via the [common Dapr issues and solutions guide](https://docs.dapr.io/operations/troubleshooting/common_issues/).

## Support

Note

Learn more about [how Microsoft handles issues raised for the Dapr extension](dapr-overview#issue-handling).

If you're experiencing Dapr runtime security risks and regressions while using the extension, open an issue with the [Dapr open source project](https://github.com/dapr/dapr/issues/new/choose).

You could also start a discussion in the Dapr project Discord:

## Delete the Dapr extension from your cluster

The process of uninstalling the Dapr extension from AKS does not delete the CRDs created during installation. These CRDs remain in the cluster as residual components, essential for the reconciler during the installation and uninstallation of the extension.

To clean the cluster of these CRDs, you can manually delete them **after** the Dapr extension has been completely uninstalled from AKS.

### Uninstalling the extension

Delete the extension from your AKS cluster using the following command:

```
az k8s-extension delete --resource-group <myResourceGroup> --cluster-name <myAKSCluster> --cluster-type managedClusters --name dapr
```


Or, if using a Bicep template, you can delete the template.

### Listing the CRDs in your cluster

To find the CRDs you'd like to remove, run the following command:

```
kubectl get crds | findstr dapr.io
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-isolated -->

# Network isolated Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Organizations typically have strict security and compliance requirements to regulate egress (outbound) network traffic from a cluster to eliminate risks of data exfiltration. By default, standard SKU Azure Kubernetes Service (AKS) clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. The conceptual document on [outbound network and fully qualified domain name (FQDN) rules for AKS clusters](outbound-rules-control-egress) provides a list of required endpoints for the AKS cluster and its optional add-ons and features.

One common solution to restricting outbound traffic from the cluster is to use a [firewall device](limit-egress-traffic) to restrict traffic based on firewall rules. Firewall is applicable when your application requires outbound access, but when outbound requests have to be inspected and secured. Configuring a firewall manually with required egress rules and *FQDNs* is a cumbersome process especially if your only requirement is to create an isolated AKS cluster with no outbound dependencies for the cluster bootstrapping.

To reduce risk of data exfiltration, network isolated cluster allows for bootstrapping the AKS cluster without any outbound network dependencies, even for fetching cluster components/images from Microsoft Artifact Registry (MAR). The cluster operator could incrementally set up allowed outbound traffic for each scenario they want to enable.

## How a network isolated cluster works

The following diagram shows the network communication between dependencies for a network isolated cluster.


AKS clusters fetch artifacts required for the cluster and its features or add-ons from the Microsoft Artifact Registry (MAR). This image pull allows AKS to provide newer versions of the cluster components and to also address critical security vulnerabilities. A network isolated cluster attempts to pull those images and binaries from a private Azure Container Registry (ACR) instance connected to the cluster instead of pulling from MAR. If the images aren't present, the private ACR pulls them from MAR and serves them via its private endpoint, eliminating the need to enable egress from the cluster to the public MAR endpoint.

The following two options are supported for a private ACR associated with network isolated clusters:

**AKS-managed ACR**- AKS creates, manages, and reconciles an ACR resource in this option. There's nothing you need to do.Note

The AKS-managed ACR resource is created in your subscription. If you delete the cluster with AKS-managed ACR for bootstrap artifact source. Related resources such as the AKS-managed ACR, private link, and private endpoint are also automatically deleted. If you change outbound type on a cluster to any type other than

`none`

or`block`

with`--bootstrap-artifact-source`

retained as`Cache`

. Then the related resources are not deleted.**Bring your own (BYO) ACR**- The BYO ACR option requires creating an ACR with a private link between the ACR resource and the AKS cluster. See[Connect privately to an Azure container registry using Azure Private Link](/en-us/azure/container-registry/container-registry-private-link)to understand how to configure a private endpoint for your registry. You also need to assign permissions and manage the cache rules, private link, and private endpoint used in the cluster.Note

When you delete the AKS cluster or after you disable the feature. The BYO ACR, private link, and private endpoint aren't deleted automatically. If you add customized images and cache rules to the BYO ACR, they persist after cluster reconciliation.


To create a network isolated cluster, you need to first ensure network traffic between your API server and your node pools remains only on the private network, you can choose one of the following private cluster modes:

[Private link-based cluster](private-clusters)- The control plane or API server is in an AKS-managed Azure resource group, and your node pool is in your resource group. The server and the node pool can communicate with each other through the Azure Private Link service in the API server virtual network and a private endpoint which is exposed on the subnet of your AKS cluster.[API Server VNet Integration configured cluster](api-server-vnet-integration)- A cluster configured with API Server VNet Integration projects the API server endpoint directly into a delegated subnet in the virtual network where AKS is deployed. API Server VNet Integration enables network communication between the API server and the cluster nodes without requiring a private link or tunnel.

You also need to ensure the egress path for your AKS cluster are controlled and limited, you can choose one of the following network outbound types:

[Outbound type of](/en-us/azure/aks/egress-outboundtype#outbound-type-of-none)- If`none`

`none`

is set. AKS doesn't automatically configure egress paths and a default route is not required. It is supported in both bring-your-own (BYO) virtual network scenarios and managed virtual network scenarios. For bring your own virtual network scenario, you must establish explicit egress paths if needed.[Outbound type of](/en-us/azure/aks/egress-outboundtype#outbound-type-of-block-preview)-If`block`

(preview)`block`

is set. AKS configures network rules to actively block all egress traffic from the cluster. This option is useful for highly secure environments where outbound connectivity must be restricted. It is supported in managed virtual network scenario. You can also achieve similar effect by blocking all egress traffic by adding[network security group (NSG)](/en-us/azure/virtual-network/network-security-groups-overview)rules with`none`

in bring-your-own virtual network scenario.

Note

Outbound type of `none`

is generally available.
Outbound type `block`

is in preview.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Limitations

`Unmanaged`

channel is not supported.- Windows node pools are not yet supported.
- kubenet networking is not supported.

Caution

If you are using [Node Public IP](use-node-public-ips) in network isolated AKS clusters, it will allow outbound traffic with outbound type `none`

.

## Using features, add-ons, and extensions requiring egress

For network isolated clusters with BYO ACR:

- If you want to use any AKS feature or add-on that requires outbound network access in network isolated clusters with outbound type
`none`

,[this document](outbound-rules-control-egress)contains the outbound network requirements for each feature. Also, this doc enumerates the features or add-ons that support private link integration for secure connection from within the cluster's virtual network. It is recommended to set up private endpoints to access these features. For example, you can set up[private endpoint based ingestion](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-private-link)to use Managed Prometheus (Azure Monitor workspace) and Container insights (Log Analytics workspace) in network isolated clusters. If a private link integration is not available for any of these features. Then you can set up the cluster with a[user-defined routing table and an Azure Firewall](limit-egress-traffic)based on the network rules and application rules that required for that feature. - If you are using
[Azure Container Storage Interface (CSI) driver](azure-files-csi)for Azure Files and Blob storage, you must create a custom storage class with "networkEndpointType: privateEndpoint", see examples in[Azure Files storage classes](/en-us/azure/aks/azure-csi-files-storage-provision#dynamically-provision-a-volume)and[Azure Blob storage classes](/en-us/azure/aks/azure-csi-blob-storage-provision?tabs=mount-nfs%2Csecret#storage-class-parameters-for-dynamic-persistent-volumes). - The following AKS cluster extensions aren't supported yet on network isolated clusters:

## Frequently asked questions

### What's the difference between network isolated cluster and Azure Firewall?

A network isolated cluster doesn't require any egress traffic beyond the VNet throughout the cluster bootstrapping process. A network isolated cluster has outbound type as either `none`

or `block`

. If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

A firewall typically establishes a barrier between a trusted network and an untrusted network, such as the Internet. Azure Firewall, for example, can restrict outbound HTTP and HTTPS traffic that's based on the destination. It gives you fine-grained control of egress traffic, but at the same time allows you to provide access to the FQDNs encompassing an AKS cluster’s outbound dependencies. This is something that NSGs can't do. For example, you can set outbound type of the cluster to `userDefinedRouting`

to force outbound traffic through the firewall and then configure FQDN restrictions on outbound traffic. There are many cases where you still want a firewall. Such as you have outbound traffic anyway from your application or you want to control, inspect, and secure the cluster traffic both egress and ingress.

In summary, while Azure Firewall can be used to define egress restrictions on clusters with outbound requests, network isolated clusters go further on secure-by-default posture by eliminating or blocking the outbound requests altogether.

### Do I need to set up any allowlist endpoints for the network isolated cluster to work?

The cluster creation and bootstrapping stages don't require any outbound traffic from the network isolated cluster. Images required for AKS components and addons are pulled from the private ACR connected to the cluster instead of pulling from Microsoft Artifact Registry (MAR) over public endpoints.

After setting up a network isolated cluster. If you want to enable features or add-ons that need to make outbound requests to their service endpoints, you can set up private endpoints to the services powered by Azure Private Link.

### Can I manually upgrade packages to upgrade node pool image?

Manually upgrading packages based on egress to package repositories is not recommended. Instead, you can [manually upgrade](node-image-upgrade) or [autoupgrade your node OS images](auto-upgrade-node-os-image). Only `NodeImage`

and `None`

upgrade channels are currently supported for network isolated clusters.

### What if I change the outbound type other than `none`

or `block`

, does that still make a network isolated cluster?

The only supported outbound types for a network isolated cluster are outbound type `none`

and `block`

. If you use any other outbound type, the cluster may still pull artifacts from the private ACR associated, however that may generate egress traffic.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kms-data-encryption-concepts -->

# Data encryption at rest concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) stores sensitive data such as Kubernetes secrets in etcd, the distributed key-value store used by Kubernetes. For enhanced security and compliance requirements, AKS supports encryption of Kubernetes secrets at rest using the Kubernetes Key Management Service (KMS) provider integrated with Azure Key Vault.

This article explains the key concepts, encryption models, and key management options available for protecting Kubernetes secrets at rest in AKS.

## Understanding data encryption at rest

Data encryption at rest protects your data when it's stored on disk. Without encryption at rest, an attacker who gains access to the underlying storage could potentially read sensitive data like Kubernetes secrets.

AKS provides encryption for Kubernetes secrets stored in etcd:

| Layer | Description |
|---|---|
Azure platform encryption |
Azure Storage automatically encrypts all data at rest using 256-bit AES encryption. This encryption is always enabled and transparent to users. |
KMS provider encryption |
An optional layer that encrypts Kubernetes secrets before they're written to etcd using keys stored in Azure Key Vault. |

For more information about Azure's encryption at rest capabilities, see [Azure data encryption at rest](/en-us/azure/security/fundamentals/encryption-atrest) and [Azure encryption models](/en-us/azure/security/fundamentals/encryption-models).

## KMS provider for data encryption

The [Kubernetes KMS provider](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/) is a mechanism that enables encryption of Kubernetes secrets at rest using an external key management system. AKS integrates with Azure Key Vault to provide this capability, giving you control over encryption keys while maintaining the security benefits of a managed Kubernetes service.

### How KMS encryption works

When you enable KMS for an AKS cluster:

**Secret creation**: When a secret is created, the Kubernetes API server sends the secret data to the KMS provider plugin.**Encryption**: The KMS plugin encrypts the secret data using a Data Encryption Key (DEK), which is itself encrypted using a Key Encryption Key (KEK) stored in Azure Key Vault.**Storage**: The encrypted secret is stored in etcd.**Secret retrieval**: When a secret is read, the KMS plugin decrypts the DEK using the KEK from Azure Key Vault, then uses the DEK to decrypt the secret data.

This envelope encryption approach provides both security and performance benefits. The DEK handles frequent encryption operations locally while the KEK in Azure Key Vault provides the security of a hardware-backed key management system.

## Key management options

AKS offers two key management options for KMS encryption:

### Platform-managed keys (PMK)

With platform-managed keys, AKS automatically manages the encryption keys for you:

- AKS creates and manages the encryption keys.
- Key rotation is handled automatically by the platform.
- No additional configuration or key vault setup is required.

**When to use platform-managed keys:**

- You want the simplest setup with minimal configuration.
- You don't have specific regulatory requirements that mandate customer-managed keys.
- You want automatic key rotation without manual intervention.

### Customer-managed keys (CMK)

With customer-managed keys, you have full control over the encryption keys:

- You create and manage your own Azure Key Vault and encryption keys.
- You control key rotation schedules and policies.

**When to use customer-managed keys:**

- You have regulatory or compliance requirements that mandate customer-managed keys.
- You need to control the key lifecycle, including rotation schedules and key versions.
- You require audit logs for all key operations.

### Key vault network access options

When using customer-managed keys, you can configure the network access for your Azure Key Vault:

| Network access | Description | Use case |
|---|---|---|
Public |
Key vault is accessible over the public internet with authentication. | Development environments, simpler setup |
Private |
Key vault has public network access disabled. AKS accesses the key vault through the
|

## Comparing encryption key options

| Feature | Platform-managed keys | Customer-managed keys (Public) | Customer-managed keys (Private) |
|---|---|---|---|
Key ownership |
Microsoft manages | Customer manages | Customer manages |
Key rotation |
Automatic |
|

[User configurable](/en-us/azure/key-vault/keys/how-to-configure-key-rotation)**Key vault creation****Network isolation**## Requirements

- The new
[KMS encryption with platform-managed keys or customer-managed keys with automatic key rotation](kms-data-encryption)experience requires**Kubernetes version 1.33 or later**. - The new
[KMS encryption with platform-managed keys or customer-managed keys with automatic key rotation](kms-data-encryption)experience is only supported on AKS clusters where[managed identity is used for the cluster's identity](use-managed-identity).

## Limitations

**No downgrade**: After enabling the new KMS encryption experience, you can't disable the feature.**Key deletion**: Deleting the encryption key or key vault makes your secrets unrecoverable.**Private endpoint access**: Key vault access using[private link/endpoint](/en-us/azure/key-vault/general/private-link-service)isn't yet supported. For private key vaults, use the[trusted services firewall exception](/en-us/azure/key-vault/general/network-security#key-vault-firewall-enabled-trusted-services-only).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-workflow -->

# Deploy and run workflows with the Dapr extension for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Dapr Workflow, you can easily orchestrate messaging, state management, and failure-handling logic across various microservices. Dapr Workflow can help you create long-running, fault-tolerant, and stateful applications.

In this guide, you use the [provided order processing workflow example](https://github.com/Azure-Samples/dapr-workflows-aks-sample) to:

- Create an Azure Container Registry and an AKS cluster for this sample.
- Install the Dapr extension on your AKS cluster.
- Deploy the sample application to AKS.
- Start and query workflow instances using HTTP API calls.

The workflow example is an ASP.NET Core project with:

- A
that contains the setup of the app, including the registration of the workflow and workflow activities.`Program.cs`

file - Workflow definitions found in the
.`Workflows`

directory - Workflow activity definitions found in the
.`Activities`

directory

## Prerequisites

- An
[Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)with Owner or Admin role. [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)- The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli) - The latest version of
[Dapr](https://docs.dapr.io/getting-started/install-dapr-cli/) - Latest
[Docker](https://docs.docker.com/get-docker/) - Latest
[Helm](https://helm.sh/docs/intro/install/)

## Set up the environment

### Clone the sample project

Clone the example workflow application.

```
git clone https://github.com/Azure-Samples/dapr-workflows-aks-sample.git
```


Navigate to the sample's root directory.

```
cd dapr-workflows-aks-sample
```


### Create a Kubernetes cluster

Create a resource group to hold the AKS cluster.

```
az group create --name myResourceGroup --location eastus
```


Create an AKS cluster.

```
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --generate-ssh-keys
```


[Make sure kubectl is installed and pointed to your AKS cluster.](tutorial-kubernetes-deploy-cluster#connect-to-cluster-using-kubectl) If you use the Azure Cloud Shell,

`kubectl`

is already installed.For more information, see the [Deploy an AKS cluster](tutorial-kubernetes-deploy-cluster) tutorial.

## Deploy the application to AKS

### Install Dapr on your AKS cluster

Install the Dapr extension on your AKS cluster. Before you start, make sure you have:

[Installed or updated the](dapr#add-the-azure-cli-extension-for-cluster-extensions).`k8s-extension`

[Registered the](dapr#register-the-kubernetesconfiguration-resource-provider)`Microsoft.KubernetesConfiguration`

service provider

```
az k8s-extension create --cluster-type managedClusters --cluster-name myAKSCluster --resource-group myResourceGroup --name dapr --extension-type Microsoft.Dapr
```


After a few minutes, you'll see output showing the Dapr connection to your AKS cluster. Next, initialize Dapr on your cluster.

```
dapr init -k
```


Verify Dapr is installed:

```
kubectl get pods -A
```


### Deploy the Redis Actor state store component

Navigate to the `Deploy`

directory in your forked version of the sample:

```
cd Deploy
```


Deploy the Redis component:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install redis bitnami/redis
kubectl apply -f redis.yaml
```


### Run the application

Once Redis is deployed, deploy the application to AKS:

```
kubectl apply -f deployment.yaml
```


Expose the Dapr sidecar and the sample app:

```
kubectl apply -f service.yaml
export APP_URL=$(kubectl get svc/workflows-sample -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export DAPR_URL=$(kubectl get svc/workflows-sample-dapr -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
```


Verify that the above commands were exported:

```
echo $APP_URL
echo $DAPR_URL
```


## Start the workflow

Now that the application and Dapr are deployed to the AKS cluster, you can now start and query workflow instances. Restock items in the inventory using the following API call to the sample app:

```
curl -X GET $APP_URL/stock/restock
```


Start the workflow:

```
curl -i -X POST $DAPR_URL/v1.0/workflows/dapr/OrderProcessingWorkflow/start \
-H "Content-Type: application/json" \
-H "dapr-app-id: dwf-app" \
-d '{"Name": "Paperclips", "TotalCost": 99.95, "Quantity": 1}'
```


Expected output includes an auto-generated instance ID:

```
HTTP/1.1 202 Accepted
Content-Type: application/json
Traceparent: 00-00000000000000000000000000000000-0000000000000000-00
Date: Tue, 23 Apr 2024 15:35:00 GMT
Content-Length: 21
{"instanceID":"<generated-id>"}
```


Check the workflow status:

```
curl -i -X GET $DAPR_URL/v1.0/workflows/dapr/OrderProcessingWorkflow/<instance-id> \
-H "dapr-app-id: dwf-app"
```


Expected output:

```
HTTP/1.1 200 OK
Content-Type: application/json
Traceparent: 00-00000000000000000000000000000000-0000000000000000-00
Date: Tue, 23 Apr 2024 15:51:02 GMT
Content-Length: 580
```


Monitor the application logs:

```
kubectl logs -l run=workflows-sample -c workflows-sample --tail=20
```


Expected output:

```
{
"instanceID":"1234",
"workflowName":"OrderProcessingWorkflow",
"createdAt":"2024-04-23T15:35:00.156714334Z",
"lastUpdatedAt":"2024-04-23T15:35:00.176459055Z",
"runtimeStatus":"COMPLETED",
"dapr.workflow.input":"{ \"input\" : {\"Name\": \"Paperclips\", \"TotalCost\": 99.95, \"Quantity\": 1}}",
"dapr.workflow.output":"{\"Processed\":true}"
}
```


Notice that the workflow status is marked as completed.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-metrics-server-vertical-pod-autoscaler -->

# Configure Metrics Server VPA in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Metrics Server](https://kubernetes-sigs.github.io/metrics-server/) is a scalable, efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines. With Azure Kubernetes Service (AKS), vertical pod autoscaling is enabled for the Metrics Server. The Metrics Server is commonly used by other Kubernetes add-ons, like the [Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler).

Vertical Pod Autoscaler (VPA) enables you to adjust the resource limit when the Metrics Server is experiencing consistent CPU and memory resource constraints.

## Prerequisites

- An AKS cluster with Kubernetes version 1.24 or higher.
- The Kubernetes command-line tool
`kubectl`

installed on your computer or use Azure Cloud Shell to run`kubectl`

commands.

## Get credentials

To run the `kubectl`

commands, you need your AKS credentials merged into your profile's `.kube/config`

file. Replace `<resourceGroupName>`

and `<clusterName>`

with your cluster's values.

```
az aks get-credentials --resource-group <resourceGroupName> --name <clusterName>
```


## Metrics server throttling

If the Metrics Server throttling rate is high, and the memory usage of its two pods is unbalanced, it's an indication that the Metrics Server needs more resources than the default values.

To update the coefficient values, create a `ConfigMap`

in the overlay `kube-system`

namespace to override the values in the Metrics Server specification. Perform the following steps to update the metrics server.

Create a

`ConfigMap`

file named*metrics-server-config.yaml*and copy the manifest code into the file.`apiVersion: v1 kind: ConfigMap metadata: name: metrics-server-config namespace: kube-system labels: kubernetes.io/cluster-service: "true" addonmanager.kubernetes.io/mode: EnsureExists data: NannyConfiguration: |- apiVersion: nannyconfig/v1alpha1 kind: NannyConfiguration baseCPU: 100m cpuPerNode: 1m baseMemory: 100Mi memoryPerNode: 8Mi`

In the

`ConfigMap`

example, the resource limit and request are changed to the following values where`n`

is the number of nodes:- cpu: (100+1n) millicores
- memory: (100+8n) mebibytes

If you're using Cloud Shell, use

**Manage files**and select**Upload**so the file is available in your Bash session.Create the

`ConfigMap`

using the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest:`kubectl apply -f metrics-server-config.yaml`

Restart the two Metrics Server pods using

[kubectl rollout restart](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout). The following command deletes both pods and new pods are created.`kubectl rollout restart -n kube-system deployment metrics-server`

The new Metrics Server pods are created before the old pods are terminated so there isn't downtime.

List the pods using

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)to get the new Metrics Server pod names that are used in the next command.`kubectl get pods --namespace kube-system`

`NAME READY STATUS RESTARTS AGE metrics-server-1a2b333c44-wxyz5 2/2 Running 0 15s metrics-server-1a2b333c44-abcd6 2/2 Running 0 15s`

If you notice a third Metrics Server pod with a longer age value, it's because the termination occurs after the new pods are available.

To verify the updated resources took effect for each pod, run the following command to review the Metrics Server VPA log. Replace

`<metrics-server-pod-name>`

with the name of each of your metrics server pods.`kubectl -n kube-system logs <metrics-server-pod-name> -c metrics-server-vpa`

The following example output resembles the results showing the updated throttling settings were applied.

`I0811 19:08:34.930865 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server] I0811 19:08:34.931128 1 pod_nanny.go:87] Version: 1.8.23 I0811 19:08:34.931200 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server. I0811 19:08:34.931249 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi I0811 19:08:34.932085 1 pod_nanny.go:144] cpu: 100m, extra_cpu: 1m, memory: 100Mi, extra_memory: 8Mi I0811 19:08:34.932177 1 pod_nanny.go:278] Resources: [{Base:{i:{value:100 scale:-3} d:{Dec:<nil>} s:100m Format:DecimalSI} ExtraPerResource:{i:{value:1 scale:-3} d:{Dec:<nil>} s:1m Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:8388608 scale:0} d:{Dec:<nil>} s: Format:BinarySI} Name:memory}]`


Be cautious of the `baseCPU`

, `cpuPerNode`

, `baseMemory`

, and the `memoryPerNode`

, because AKS doesn't validate the `ConfigMap`

. As a recommended practice, increase the value gradually to avoid unnecessary resource consumption. Proactively monitor resource usage when updating or creating the `ConfigMap`

. A large number of resource requests could negatively affect the node.

## Manually configure Metrics Server resource usage

The Metrics Server VPA adjusts resource usage by the number of nodes. If the cluster scales up or down often, the Metrics Server might restart frequently. In this case, you can bypass VPA and manually control its resource usage. This method to configure VPA isn't to be performed in addition to the steps described in the previous section.

If you would like to bypass VPA for Metrics Server and manually control its resource usage, perform the following steps.

Create a

`ConfigMap`

file named*metrics-server-config.yaml*and copy in the following manifest.`apiVersion: v1 kind: ConfigMap metadata: name: metrics-server-config namespace: kube-system labels: kubernetes.io/cluster-service: "true" addonmanager.kubernetes.io/mode: EnsureExists data: NannyConfiguration: |- apiVersion: nannyconfig/v1alpha1 kind: NannyConfiguration baseCPU: 100m cpuPerNode: 0m baseMemory: 100Mi memoryPerNode: 0Mi`

In this

`ConfigMap`

example, the resource limit and request are changed to the following values that don't trigger autoscaling:- cpu: 100 millicores
- memory: 100 mebibytes

If you're using Cloud Shell, use

**Manage files**and select**Upload**so the file is available in your Bash session.Create the

`ConfigMap`

using the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest:`kubectl apply -f metrics-server-config.yaml`

Restart the two Metrics Server pods using

[kubectl rollout restart](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout). The following command deletes both pods and new pods are created.`kubectl rollout restart -n kube-system deployment metrics-server`

The new Metrics Server pods are created before the old pods are terminated so there isn't downtime.

List the pods using

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)to get the new Metrics Server pod names that are used in the next command.`kubectl get pods --namespace kube-system`

`NAME READY STATUS RESTARTS AGE metrics-server-1a2b333c44-wxyz5 2/2 Running 0 15s metrics-server-1a2b333c44-abcd6 2/2 Running 0 15s`

If you notice a third Metrics Server pod with a longer age value, it's because the termination occurs after the new pods are available.

To verify the updated resources took effect for each pod, run the following command to review the Metrics Server VPA log. Replace

`<metrics-server-pod-name>`

with the name of each of your metrics server pods.`kubectl -n kube-system logs <metrics-server-pod-name> -c metrics-server-vpa`

The following example output resembles the results showing the updated throttling settings were applied.

`I0811 19:19:06.235018 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server] I0811 19:19:06.235105 1 pod_nanny.go:87] Version: 1.8.23 I0811 19:19:06.235136 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server. I0811 19:19:06.235171 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi I0811 19:19:06.235899 1 pod_nanny.go:144] cpu: 100m, extra_cpu: 0m, memory: 100Mi, extra_memory: 0Mi I0811 19:19:06.235917 1 pod_nanny.go:278] Resources: [{Base:{i:{value:100 scale:-3} d:{Dec:<nil>} s:100m Format:DecimalSI} ExtraPerResource:{i:{value:0 scale:-3} d:{Dec:<nil>} s: Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:0 scale:0} d:{Dec:<nil>} s: Format:BinarySI} Name:memory}]`


## Troubleshooting

### ConfigMap error

If you apply the following `ConfigMap`

, the Metrics Server VPA customizations aren't applied. You need add a unit for `baseCPU`

like `baseCPU: 100m`

that includes the `m`

unit.

```
apiVersion: v1
kind: ConfigMap
metadata:
name: metrics-server-config
namespace: kube-system
labels:
kubernetes.io/cluster-service: "true"
addonmanager.kubernetes.io/mode: EnsureExists
data:
NannyConfiguration: |-
apiVersion: nannyconfig/v1alpha1
kind: NannyConfiguration
baseCPU: 100
cpuPerNode: 1m
baseMemory: 100Mi
memoryPerNode: 8Mi
```


The following example output resembles the results showing the updated throttling settings aren't applied.

```
I0811 19:25:33.992691 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server]
I0811 19:25:33.992890 1 pod_nanny.go:87] Version: 1.8.23
I0811 19:25:33.992918 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server.
I0811 19:25:33.992937 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi
I0811 19:25:33.993586 1 pod_nanny.go:217] Unable to decode Nanny Configuration from config map, using default parameters
I0811 19:25:33.993602 1 pod_nanny.go:144] cpu: 150m, extra_cpu: 0.5m, memory: 100Mi, extra_memory: 4Mi
I0811 19:25:33.993610 1 pod_nanny.go:278] Resources: [{Base:{i:{value:150 scale:-3} d:{Dec:<nil>} s:150m Format:DecimalSI} ExtraPerResource:{i:{value:5 scale:-4} d:{Dec:<nil>} s: Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:4194304 scale:0} d:{Dec:<nil>} s:4Mi Format:BinarySI} Name:memory}]
```


### PodDisruptionBudget

For Kubernetes version 1.23 and higher clusters, Metrics Server has a `PodDisruptionBudget`

. It ensures the number of available Metrics Server pods is at least one. If you get something like this after running `kubectl get pods --namespace kube-system`

, it's possible that the customized resource usage is small. Increase the coefficient values to resolve it.

```
metrics-server-1a2b333c44-wxyz5 1/2 CrashLoopBackOff 6 (36s ago) 6m33s
metrics-server-1a2b333c44-abcd6 1/2 CrashLoopBackOff 6 (54s ago) 6m33s
metrics-server-5d69966543-hcrff 2/2 Running 0 37m
```


## Next steps

Metrics Server is a component in the core metrics pipeline. For more information, see [Metrics Server API design](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/release-tracker -->

# AKS release tracker

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS releases weekly rounds of fixes and feature and component updates that affect all clusters and customers. It's important for you to know when a particular AKS release is hitting your region, and the AKS release tracker provides these details in real time by versions and regions.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Overview

With AKS release tracker, you can follow specific component updates present in an AKS version release, such as fixes shipped to a core add-on, and node image updates for Azure Linux, Ubuntu, and Windows. The tracker provides links to the specific version of the AKS [release notes](https://github.com/Azure/AKS/releases) to help you identify relevant release instances. Real time data updates allow you to track the release order and status of each region.

## Use the release tracker

To view the release tracker, visit the [AKS release status webpage](https://releases.aks.azure.com/webpage/index.html).

### AKS releases

The top half of the tracker shows the current latest version and three previously available release versions for each region and links to the corresponding release notes entries. This view is helpful when you want to track the available versions by region.


The bottom half of the tracker shows the release order. The table has two views: *By Region* and *By Version*.


### AKS node image updates

The top half of the tracker shows the current latest node image version and three previously available node image versions for each region. This view is helpful when you want to track the available node image versions by region.


The bottom half of the tracker shows the node image update order. The table has two views: *By Region* and *By Version*.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/update-kms-key-vault -->

# Update the key vault mode for an Azure Kubernetes Service (AKS) cluster with Key Management Service (KMS) etcd encryption (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to update the key vault mode from public to private or private to public for an Azure Kubernetes Service (AKS) cluster with Key Management Service (KMS) etcd encryption.

## Prerequisites

- An AKS cluster with KMS etcd encryption enabled. For more information, see
[Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster](use-kms-etcd-encryption). - Azure CLI version 2.39.0 or later. Find your version using the
`az --version`

command. If you need to install or upgrade, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update a key vault mode

Note

To change a different key vault with a different mode (whether public or private), you can run [ az aks update](/en-us/cli/azure/aks#az-aks-update) directly. To change the mode of an attached key vault, you must first turn off KMS, then turn it on again using the new key vault IDs.

Turn off KMS on the existing cluster and release the key vault using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Warning

After you turn off KMS, the encryption key vault key is still needed. You can't delete or expire it.

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`

Update the key vault from public to private using the

command with the`az keyvault update`

`--public-network-access`

parameter set to`Disabled`

.`az keyvault update --name $KEY_VAULT --resource-group $RESOURCE_GROUP --public-network-access Disabled`

Turn on KMS with the updated private key vault using the

command with the`az aks update`

`--azure-keyvault-kms-key-vault-network-access`

parameter set to`Private`

.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-capacity-reservation-groups -->

# Assign capacity reservation groups to Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your workload demands change, you can associate existing [capacity reservation groups (CRGs)](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set) to your Azure Kubernetes Service (AKS) node pools to guarantee allocated capacity for them. Capacity reservation groups allow you to reserve compute capacity in an Azure region or availability zone for any duration of time. This feature is useful for workloads that require guaranteed capacity, such as those with predictable traffic patterns or those that need to meet specific performance requirements.

In this article, you learn how to use capacity reservation groups with node pools in AKS.

Note

Deleting a node pool implicitly dissociates that node pool from any associated capacity reservation group before the node pool is deleted. Deleting a cluster implicitly dissociates all node pools in that cluster from their associated capacity reservation groups.

## Prerequisites for using capacity reservation groups with AKS node pools

- You need the Azure CLI version 2.56 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need an existing
[capacity reservation group](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set)with at least one capacity reservation. If not, the node pool is added to the cluster with a warning and no capacity reservation group gets associated. - You need to
[create a user-assigned managed identity with the](#create-a-user-assigned-managed-identity-and-assign-it-to-an-aks-cluster)for the resource group that contains the capacity reservation group and assign the identity to your AKS cluster. System-assigned managed identities don't work for this feature.`Contributor`

role

### Create a user-assigned managed identity and assign it to an AKS cluster

Create a user-assigned managed identity using the

command.`az identity create`

`az identity create --name <identity-name> --resource-group <resource-group-name> --location <location>`

Get the ID of the user-assigned managed identity using the

command and set it to an environment variable.`az identity show`

`IDENTITY_ID=$(az identity show --name <identity-name> --resource-group <resource-group-name> --query identity.id -o tsv)`

Assign the

`Contributor`

role to the user-assigned identity using thecommand.`az role assignment create`

`az role assignment create --assignee $IDENTITY_ID --role "Contributor" --scope /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>`

It can take up to

*60 minutes*for the role assignment to propagate.Assign the user-assigned managed identity to a new or existing AKS cluster using the

`--assign-identity`

flag with theor`az aks create`

command.`az aks update`

`# Create a new AKS cluster with the user-assigned managed identity az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --generate-ssh-keys # Update an existing AKS cluster to use the user-assigned managed identity az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> \ --node-count <node-count> \ --enable-managed-identity \ --assign-identity $IDENTITY_ID`


## Limitations for using capacity reservation groups with AKS node pools

You can't update an existing node pool with a capacity reservation group. Instead, you need to create a new node pool with the `--crg-id`

flag to associate it with the capacity reservation group. You can also associate an existing capacity reservation group with a system node pool during cluster creation.

## Get the ID of an existing capacity reservation group

Get the ID of an existing capacity reservation group using the

command and set it to an environment variable.`az capacity reservation group show`

`CRG_ID=$(az capacity reservation group show --capacity-reservation-group <crg-name> --resource-group <resource-group-name> --query id -o tsv)`


## Associate an existing capacity reservation group with a node pool

Associate an existing capacity reservation group with a node pool using the

command with the`az aks nodepool add`

`--crg-id`

flag. The following example assumes you have a CRG named "myCRG".`az aks nodepool add --resource-group <resource-group-name> --cluster-name <cluster-name> --name <node-pool-name> --crg-id $CRG_ID`


## Associate an existing capacity reservation group with a system node pool

To associate an existing capacity reservation group with a system node pool, you need to assign the user-assigned managed identity with the `Contributor`

role to the cluster during cluster creation. You can then use the `--crg-id`

flag to associate the capacity reservation group with the system node pool.

Create a new AKS cluster with the user-assigned managed identity and associate it with the capacity reservation group using the

`--assign-identity`

and`--crg-id`

flags with thecommand.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --crg-id $CRG_ID \ --generate-ssh-keys`


## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-performance-scale -->

# Best practices for performance and scaling for small to medium workloads in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This article focuses on general best practices for **small to medium workloads**. For best practices specific to **large workloads**, see [Performance and scaling best practices for large workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale-large).

As you deploy and maintain clusters in AKS, you can use the following best practices to help you optimize performance and scaling.

In this article, you learn about:

- Tradeoffs and recommendations for autoscaling your workloads.
- Managing node scaling and efficiency based on your workload demands.
- Networking considerations for ingress and egress traffic.
- Monitoring and troubleshooting control plane and node performance.
- Capacity planning, surge scenarios, and cluster upgrades.
- Storage and networking considerations for data plane performance.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Application autoscaling vs. infrastructure autoscaling

### Application autoscaling

Application autoscaling is useful when dealing with cost optimization or infrastructure limitations. A well-configured autoscaler maintains high availability for your application while also minimizing costs. You only pay for the resources required to maintain availability, regardless of the demand.

For example, if an existing node has space but not enough IPs in the subnet, it might be able to skip the creation of a new node and instead immediately start running the application on a new pod.

#### Horizontal Pod autoscaling

Implementing [horizontal pod autoscaling](concepts-scale#horizontal-pod-autoscaler) is useful for applications with a steady and predictable resource demand. The Horizontal Pod Autoscaler (HPA) dynamically scales the number of pod replicas, which effectively distributes the load across multiple pods and nodes. This scaling mechanism is typically most beneficial for applications that can be decomposed into smaller, independent components capable of running in parallel.

The HPA provides resource utilization metrics by default. You can also integrate custom metrics or leverage tools like the [Kubernetes Event-Driven Autoscaler (KEDA) (Preview)](keda-about). These extensions allow the HPA to make scaling decisions based on multiple perspectives and criteria, providing a more holistic view of your application's performance. This is especially helpful for applications with varying complex scaling requirements.

Note

If maintaining high availability for your application is a top priority, we recommend leaving a slightly higher buffer for the minimum pod number for your HPA to account for scaling time.

#### Vertical Pod autoscaling

Implementing [vertical pod autoscaling](vertical-pod-autoscaler) is useful for applications with fluctuating and unpredictable resource demands. The Vertical Pod Autoscaler (VPA) allows you to fine-tune resource requests, including CPU and memory, for individual pods, enabling precise control over resource allocation. This granularity minimizes resource waste and enhances the overall efficiency of cluster utilization. The VPA also streamlines application management by automating resource allocation, freeing up resources for critical tasks.

Warning

You shouldn't use the VPA in conjunction with the HPA on the same CPU or memory metrics. This combination can lead to conflicts, as both autoscalers attempt to respond to changes in demand using the same metrics. However, you can use the VPA for CPU or memory in conjunction with the HPA for custom metrics to prevent overlap and ensure that each autoscaler focuses on distinct aspects of workload scaling.

Note

The VPA works based on historical data. We recommend waiting at least *24 hours* after deploying the VPA before applying any changes to give it time to collect recommendation data.

### Infrastructure autoscaling

#### Cluster autoscaling

Implementing cluster autoscaling is useful if your existing nodes lack sufficient capacity, as it helps with scaling up and provisioning new nodes.

When considering cluster autoscaling, the decision of when to remove a node involves a tradeoff between optimizing resource utilization and ensuring resource availability. Eliminating underutilized nodes enhances cluster utilization but might result in new workloads having to wait for resources to be provisioned before they can be deployed. It's important to find a balance between these two factors that aligns with your cluster and workload requirements and [configure the cluster autoscaler profile settings accordingly](cluster-autoscaler#update-the-cluster-autoscaler-settings).

The Cluster Autoscaler profile settings apply universally to all autoscaler-enabled node pools in your cluster. This means that any scaling actions occurring in one autoscaler-enabled node pool might impact the autoscaling behavior in another node pool. It's important to apply consistent and synchronized profile settings across all relevant node pools to ensure that the autoscaler behaves as expected.

##### Overprovisioning

Overprovisioning is a strategy that helps mitigate the risk of application pressure by ensuring there's an excess of readily available resources. This approach is especially useful for applications that experience highly variable loads and cluster scaling patterns that show frequent scale ups and scale downs.

To determine the optimal amount of overprovisioning, you can use the following formula:

```
1-buffer/1+traffic
```


For example, let's say you want to avoid hitting 100% CPU utilization in your cluster. You might opt for a 30% buffer to maintain a safety margin. If you anticipate an average traffic growth rate of 40%, you might consider overprovisioning by 50%, as calculated by the formula:

```
1-30%/1+40%=50%
```


An effective overprovisioning method involves the use of *pause pods*. Pause pods are low-priority deployments that can be easily replaced by high-priority deployments. You create low priority pods that serve the sole purpose of reserving buffer space. When a high-priority pod requires space, the pause pods are removed and rescheduled on another node or a new node to accommodate the high priority pod.

The following YAML shows an example pause pod manifest:

```
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
name: overprovisioning
value: -1
globalDefault: false
description: "Priority class used by overprovisioning."
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: overprovisioning
namespace: kube-system
spec:
replicas: 1
selector:
matchLabels:
run: overprovisioning
template:
metadata:
labels:
run: overprovisioning
spec:
priorityClassName: overprovisioning
containers:
- name: reserve-resources
image: your-custome-pause-image
resources:
requests:
cpu: 1
memory: 4Gi
```


## Node scaling and efficiency


Best practice guidance:Carefully monitor resource utilization and scheduling policies to ensure nodes are being used efficiently.


Node scaling allows you to dynamically adjust the number of nodes in your cluster based on workload demands. It's important to understand that adding more nodes to a cluster isn't always the best solution for improving performance. To ensure optimal performance, you should carefully monitor resource utilization and scheduling policies to ensure nodes are being used efficiently.

### Node images


Best practice guidance:Use the latest node image version to ensure that you have the latest security patches and bug fixes.


Using the latest node image version provides the best performance experience. AKS ships performance improvements within the weekly image releases. The latest daemonset images are cached on the latest VHD image, which provide lower latency benefits for node provisioning and bootstrapping. Falling behind on updates might have a negative impact on performance, so it's important to avoid large gaps between versions.

#### Azure Linux

The [Azure Linux Container Host on AKS](/en-us/azure/azure-linux/intro-azure-linux) uses a native AKS image and provides a single place for Linux development. Every package is built from source and validated, ensuring your services run on proven components.

Azure Linux is lightweight, only including the necessary set of packages to run container workloads. It provides a reduced attack surface and eliminates patching and maintenance of unnecessary packages. At its base layer, it has a Microsoft-hardened kernel tuned for Azure. This image is ideal for performance-sensitive workloads and platform engineers or operators that manage fleets of AKS clusters.

#### Ubuntu 2204

The [Ubuntu 2204 image](https://github.com/Azure/AKS/blob/master/CHANGELOG.md) is the default node image for AKS. It's a lightweight and efficient operating system optimized for running containerized workloads. This means that it can help reduce resource usage and improve overall performance. The image includes the latest security patches and updates, which help ensure that your workloads are protected from vulnerabilities.

The Ubuntu 2204 image is fully supported by Microsoft, Canonical, and the Ubuntu community and can help you achieve better performance and security for your containerized workloads.

### Virtual machines (VMs)


Best practice guidance:When selecting a VM, ensure the size and performance of the OS disk and VM SKU don't have a large discrepancy. A discrepancy in size or performance can cause performance issues and resource contention.


Application performance is closely tied to the VM SKUs you use in your workloads. Larger and more powerful VMs, generally provide better performance. For *mission critical or product workloads*, we recommend using VMs with at least an 8-core CPU. VMs with newer hardware generations, like v4 and v5, can also help improve performance. Keep in mind that create and scale latency might vary depending on the VM SKUs you use.

### Use dedicated system node pools

For scaling performance and reliability, we recommend using a dedicated system node pool. With this configuration, the dedicated system node pool reserves space for critical system resources such as system OS daemons. Your application workload can then run in a user node pool to increase the availability of allocatable resources for your application. This configuration also helps mitigate the risk of resource competition between the system and application.

### Create operations

Review the extensions and add-ons you have enabled during create provisioning. Extensions and add-ons can add latency to overall duration of create operations. If you don't need an extension or add-on, we recommend removing it to improve create latency.

You can also use availability zones to provide a higher level of availability to protect against potential hardware failures or planned maintenance events. AKS clusters distribute resources across logical sections of underlying Azure infrastructure. Availability zones physically separate nodes from other nodes to help ensure that a single failure doesn't impact the availability of your application. Availability zones are only available in certain regions. For more information, see [Availability zones in Azure](/en-us/azure/reliability/availability-zones-overview).

## Kubernetes API server

### LIST and WATCH operations

Kubernetes uses the LIST and WATCH operations to interact with the Kubernetes API server and monitor information about cluster resources. These operations are fundamental to how Kubernetes performs resource management.

**The LIST operation retrieves a list of resources that fit within certain criteria**, such as all pods in a specific namespace or all services in the cluster. This operation is useful when you want to get an overview of your cluster resources or you need to operator on multiple resources at once.

The LIST operation can retrieve large amounts of data, especially in large clusters with multiple resources. Be mindful of the fact that making unbounded or frequent LIST calls puts a significant load on the API server and can close down response times.

**The WATCH operation performs real-time resource monitoring**. When you set up a WATCH on a resource, the API server sends you updates whenever there are changes to that resource. This is important for controllers, like the ReplicaSet controller, which rely on WATCH to maintain the desired state of resources.

Be mindful of the fact that watching too many mutable resources or making too many concurrent WATCH requests can overwhelm the API server and cause excessive resource consumption.

To avoid potential issues and ensure the stability of the Kubernetes control plane, you can use the following strategies:

**Resource quotas**

Implement resource quotas to limit the number of resources that can be listed or watched by a particular user or namespace to prevent excessive calls.

**API Priority and Fairness**

Kubernetes introduced the concept of API Priority and Fairness (APF) to prioritize and manage API requests. You can use APF in Kubernetes to protect the cluster's API server and reduce the number of `HTTP 429 Too Many Requests`

responses seen by client applications.

| Custom resource | Key features |
|---|---|
| PriorityLevelConfigurations | * Define different priority levels for API requests. * Specifies a unique name and assigns an integer value representing the priority level. Higher priority levels have lower integer values, indicating they're more critical. * Can use multiple to categorize requests into different priority levels based on their importance. * Allow you to specify whether requests at a particular priority level should be subject to rate limits. |
| FlowSchemas | * Define how API requests should be routed to different priority levels based on request attributes. * Specify rules that match requests based on criteria like API groups, versions, and resources. * When a request matches a given rule, the request is directed to the priority level specified in the associated PriorityLevelConfiguration. * Can use to set the order of evaluation when multiple FlowSchemas match a request to ensure that certain rules take precedence. |

Configuring API with PriorityLevelConfigurations and FlowSchemas enables the prioritization of critical API requests over less important requests. This ensures that essential operations don't starve or experience delays because of lower priority requests.

**Optimize labeling and selectors**

When using LIST operations, optimize label selectors to narrow down the scope of the resources you want to query to reduce the amount of data returned and the load on the API server.

In Kubernetes CREATE and UPDATE operations refer to actions that manage and modify cluster resources.

### CREATE and UPDATE operations

**The CREATE operation creates new resources in the Kubernetes cluster**, such as pods, services, deployments, configmaps, and secrets. During a CREATE operation, a client, such as `kubectl`

or a controller, sends a request to the Kubernetes API server to create the new resource. The API server validates the request, ensures compliance with any admission controller policies, and then creates the resource in the cluster's desired state.

**The UPDATE operation modifies existing resources in the Kubernetes cluster**, including changes to resources specifications, like number of replicas, container images, environment variables, or labels. During an UPDATE operation, a client sends a request to the API server to update an existing resource. The API server validates the request, applies the changes to the resource definition, and updates the cluster resource.

CREATE and UPDATE operations can impact the performance of the Kubernetes API server under the following conditions:

**High concurrency**: When multiple users or applications make concurrent CREATE or UPDATE requests, it can lead to a surge in API requests arriving at the server at the same time. This can stress the API server's processing capacity and cause performance issues.**Complex resource definitions**: Resource definitions that are overly complex or involve multiple nested objects can increase the time it takes for the API server to validate and process CREATE and UPDATE requests, which can lead to performance degradation.**Resource validation and admission control**: Kubernetes enforces various admission control policies and validation checks on incoming CREATE and UPDATE requests. Large resource definitions, like ones with extensive annotations or configurations, might require more processing time.**Custom controllers**: Custom controllers that watch for changes in resources, like Deployments or StatefulSet controllers, can generate a significant number of updates when scaling or rolling out changes. These updates can strain the API server's resources.

For more information, see [Troubleshoot API server and etcd problems in AKS](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd).

## Data plane performance

The Kubernetes data plane is responsible for managing network traffic between containers and services. Issues with the data plane can lead to slow response times, degraded performance, and application downtime. It's important to carefully monitor and optimize data plane configurations, such as network latency, resource allocation, container density, and network policies, to ensure your containerized applications run smoothly and efficiently.

### Storage types

AKS recommends and defaults to using ephemeral OS disks. Ephemeral OS disks are created on local VM storage and aren't saved to remote Azure storage like managed OS disks. They have faster reimaging and boot times, enabling faster cluster operations, and they provide lower read/write latency on the OS disk of AKS agent nodes. Ephemeral OS disks work well for stateless workloads, where applications are tolerant of individual VM failures but not of VM deployment time or individual VM reimaging instances. Only certain VM SKUs support ephemeral OS disks, so you need to ensure that your desired SKU generation and size is compatible. For more information, see [Ephemeral OS disks in Azure Kubernetes Service (AKS)](cluster-configuration#use-ephemeral-os-on-new-clusters).

If your workload is unable to use ephemeral OS disks, AKS defaults to using Premium SSD OS disks. If Premium SSD OS disks aren't compatible with your workload, AKS defaults to Standard SSD disks. Currently, the only other available OS disk type is Standard HDD. For more information, see [Storage options in Azure Kubernetes Service (AKS)](concepts-storage).

The following table provides a breakdown of suggested use cases for OS disks supported in AKS:

| OS disk type | Key features | Suggested use cases |
|---|---|---|
| Ephemeral OS disks | * Faster reimaging and boot times. * Lower read/write latency on OS disk of AKS agent nodes. * High performance and availability. |
* Demanding enterprise workloads, such as SQL Server, Oracle, Dynamics, Exchange Server, MySQL, Cassandra, MongoDB, SAP Business Suite, etc. * Stateless production workloads that require high availability and low latency. |
| Premium SSD OS disks | * Consistent performance and low latency. * High availability. |
* Demanding enterprise workloads, such as SQL Server, Oracle, Dynamics, Exchange Server, MySQL, Cassandra, MongoDB, SAP Business Suite, etc. * Input/output (IO) intensive enterprise workloads. |
| Standard SSD OS disks | * Consistent performance. * Better availability and latency compared to Standard HDD disks. |
* Web servers. * Low input/output operations per second (IOPS) application servers. * Lightly used enterprise applications. * Dev/test workloads. |
| Standard HDD disks | * Low cost. * Exhibits variability in performance and latency. |
* Backup storage. * Mass storage with infrequent access. |

#### IOPS and throughput

Input/output operations per second (IOPS) refers to the number of read and write operations that a disk can perform in a second. Throughput refers to the amount of data that can be transferred in a given time period.

OS disks are responsible for storing the operating system and its associated files, and the VMs are responsible for running the applications. When selecting a VM, ensure the size and performance of the OS disk and VM SKU don't have a large discrepancy. A discrepancy in size or performance can cause performance issues and resource contention. For example, if the OS disk is significantly smaller than the VMs, it can limit the amount of space available for application data and cause the system to run out of disk space. If the OS disk has lower performance than the VMs, it can become a bottleneck and limit the overall performance of the system. Make sure the size and performance are balanced to ensure optimal performance in Kubernetes.

You can use the following steps to monitor IOPS and bandwidth meters on OS disks in the Azure portal:

- Navigate to the
[Azure portal](https://portal.azure.com/). - Search for
**Virtual machine scale sets**and select your virtual machine scale set. - Under
**Monitoring**, select**Metrics**.

Ephemeral OS disks can provide dynamic IOPS and throughput for your application, whereas managed disks have capped IOPS and throughput. For more information, see [Ephemeral OS disks for Azure VMs](/en-us/azure/virtual-machines/ephemeral-os-disks).

[Azure Premium SSD v2](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) is designed for IO-intense enterprise workloads that require sub-millisecond disk latencies and high IOPS and throughput at a low cost. It's suited for a broad range of workloads, such as SQL server, Oracle, MariaDB, SAP, Cassandra, MongoDB, big data/analytics, gaming, and more. This disk type is the highest performing option currently available for persistent volumes.

### Pod scheduling

The memory and CPU resources allocated to a VM have a direct impact on the performance of the pods running on the VM. When a pod is created, it's assigned a certain amount of memory and CPU resources, which are used to run the application. If the VM doesn't have enough memory or CPU resources available, it can cause the pods to slow down or even crash. If the VM has too much memory or CPU resources available, it can cause the pods to run inefficiently, wasting resources and increasing costs. We recommend monitoring the total pod requests across your workloads against the total allocatable resources for best scheduling predictability and performance. You can also set the maximum pods per node based on your capacity planning using `--max-pods`

.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-ingress -->

# Deploy ingress gateways for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy external or internal ingresses for the Istio service mesh add-on for Azure Kubernetes Service (AKS) cluster.

Note

When you perform a [minor revision upgrade](istio-upgrade#minor-revision-upgrades-with-ingress-and-egress-gateways) of the Istio add-on, another deployment for the external / internal gateways will be created for the new control plane revision.

## Prerequisites

This guide assumes you followed the [documentation](istio-deploy-addon) to enable the Istio add-on on an AKS cluster, deploy a sample application, and set environment variables.

## Enable external ingress gateway

Note

If you need the ingress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

Use `az aks mesh enable-ingress-gateway`

to enable an externally accessible Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type external
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-external -n aks-istio-ingress
```


Observe from the output that the external IP address of the service is a publicly accessible one:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-external LoadBalancer 10.0.10.249 <EXTERNAL_IP> 15021:30705/TCP,80:32444/TCP,443:31728/TCP 4m21s
```


Applications aren't accessible from outside the cluster by default after enabling the ingress gateway. To make an application accessible, map the sample deployment's ingress to the Istio ingress gateway using the following manifest:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-gateway-external
spec:
selector:
istio: aks-istio-ingressgateway-external
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-external
spec:
hosts:
- "*"
gateways:
- bookinfo-gateway-external
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-external`

, which can be found as label on the service mapped to the external ingress that was enabled earlier.

Set environment variables for external ingress host and ports:

```
export INGRESS_HOST_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_EXTERNAL=$INGRESS_HOST_EXTERNAL:$INGRESS_PORT_EXTERNAL
```


Retrieve the external address of the sample application:

```
echo "http://$GATEWAY_URL_EXTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is displayed. Alternatively, you can also use `curl`

to confirm the sample application is accessible. For example:

```
curl -s "http://${GATEWAY_URL_EXTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Enable internal ingress gateway

Use `az aks mesh enable-ingress-gateway`

to enable an internal Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type internal
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-internal -n aks-istio-ingress
```


Observe from the output that the external IP address of the service isn't a publicly accessible one and is instead only locally accessible:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-internal LoadBalancer 10.0.182.240 <IP> 15021:30764/TCP,80:32186/TCP,443:31713/TCP 87s
```


After enabling the ingress gateway, applications need to be exposed through the gateway, and routing rules need to be configured accordingly. Use the following manifest to map the sample deployment's ingress to the Istio ingress gateway:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-internal-gateway
spec:
selector:
istio: aks-istio-ingressgateway-internal
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-internal
spec:
hosts:
- "*"
gateways:
- bookinfo-internal-gateway
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-internal`

, which can be found as label on the service mapped to the internal ingress that was enabled earlier.

Set environment variables for internal ingress host and ports:

```
export INGRESS_HOST_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_INTERNAL=$INGRESS_HOST_INTERNAL:$INGRESS_PORT_INTERNAL
```


Retrieve the address of the sample application:

```
echo "http://$GATEWAY_URL_INTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is **NOT** displayed. Alternatively, you can also use `curl`

to confirm the sample application is **NOT** accessible. For example:

```
curl -s "http://${GATEWAY_URL_INTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Use `kubectl exec`

to confirm application is accessible from inside the cluster's virtual network:

```
kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS "http://$GATEWAY_URL_INTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Ingress gateway service customizations

### Annotations

The following annotations can be added to the Kubernetes service for the external and internal ingress gateways. See the [document on configuring public load balancers](configure-load-balancer-standard#customizations-via-kubernetes-annotations) for more information about these annotations.

`external-dns.alpha.kubernetes.io/hostname`

: for specifying the domain for resource's DNS records. For more information, see[external-dns](https://kubernetes-sigs.github.io/external-dns/latest/docs/annotations/annotations/#external-dnsalphakubernetesiohostname).`service.beta.kubernetes.io/azure-allowed-ip-ranges`

: for specifying a list of allowed IP ranges separated by commas.`service.beta.kubernetes.io/azure-allowed-service-tags`

: for specifying which[service tags](/en-us/azure/virtual-network/service-tags-overview)the ingress gateway can receive requests from.`service.beta.kubernetes.io/azure-disable-load-balancer-floating-ip`

: set to`true`

to disable floating IP address in load balancer rule.`service.beta.kubernetes.io/azure-load-balancer-internal-subnet`

: name of subnet to bind internal ingress gateway to. This subnet must exist in the same virtual network as the mesh.`service.beta.kubernetes.io/azure-load-balancer-ipv4`

: for configuring a static IPv4 address.`service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset`

: for controlling whether Azure Load Balancer enables TCP Reset.`service.beta.kubernetes.io/azure-load-balancer-resource-group`

: for specifying the resource group of a public IP in a different resource group from the cluster.`service.beta.kubernetes.io/azure-load-balancer-tcp-idle-timeout`

: for configuring the TCP idle timeout in minutes for connections through the Azure Load Balancer.`service.beta.kubernetes.io/azure-pip-ip-tags`

: for specifying a list of IpTags separated by commas.`service.beta.kubernetes.io/azure-pip-name`

: for specifying the name of a public IP address.`service.beta.kubernetes.io/azure-shared-securityrule`

: for exposing the ingress gateway through an[augmented security rule](/en-us/azure/virtual-network/network-security-groups-overview#augmented-security-rules).

The add-on supports the following health probe annotations for ports `80`

and `443`

:

`service.beta.kubernetes.io/port_{port}_no_lb_rule`

`service.beta.kubernetes.io/port_{port}_no_probe_rule`

`service.beta.kubernetes.io/port_{port}_health-probe_protocol`

`service.beta.kubernetes.io/port_{port}_health-probe_port`

`service.beta.kubernetes.io/port_{port}_health-probe_interval`

`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe`

`service.beta.kubernetes.io/port_{port}_health-probe_request-path`


### External traffic policy

The add-on supports customization of `.spec.externalTrafficPolicy`

in the Kubernetes service for the ingress gateway. Setting `.spec.externalTrafficPolicy`

to `Local`

preserves the client source IP at the Istio ingress gateway and avoids a second hop in the traffic path to the backend ingress gateway pods.

```
kubectl patch service aks-istio-ingressgateway-external -n aks-istio-ingress --type merge --patch '{"spec": {"externalTrafficPolicy": "Local"}}'
```


Note

Modifying the `.spec.externalTrafficPolicy`

to `Local`

risks potentially imbalanced traffic spreading. Before applying this change, it is recommended to read the [Kubernetes docs](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip) to understand the tradeoffs between the different `externalTrafficPolicy`

settings.

## Delete resources

If you want to clean up the Istio external or internal ingress gateways, but leave the mesh enabled on the cluster, run the following command:

```
az aks mesh disable-ingress-gateway --ingress-gateway-type <external/internal> --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```


## Next steps

Note

If there are any issues encountered with deploying the Istio ingress gateway or configuring ingress traffic routing, refer to [article on troubleshooting Istio add-on ingress gateways](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-ingress-gateway)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-marketplace -->

# Deploy and manage a Kubernetes application from Azure Marketplace

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy and manage a Kubernetes application from Azure Marketplace.

[Azure Marketplace](/en-us/marketplace/azure-marketplace-overview) is an online store that contains thousands of IT software applications and services built by industry-leading technology companies. In Azure Marketplace, you can find, try, buy, and deploy the software and services that you need to build new solutions and manage your cloud infrastructure. The catalog includes solutions for different industries and technical areas, free trials, and consulting services from Microsoft partners.

## Limitations

- This feature is currently supported only in the following regions:
- Australia East, Australia Southeast, Brazil South, Canada Central, Canada East, Central India, Central US, East Asia, East US, East US 2, East US 2 EAUP, France Central, France South, Germany North, Germany West Central, Japan East, Japan West, Jio India West, Korea Central, Korea South, North Central Us, North Europe, Norway East, Norway West, South Africa North, South Central US, South India, Southeast Asia, Sweden Central, Switzerland North, UAE North, UK South, UK West, West Central US, West Europe, West US, West US 2, West US 3

- You can't deploy Kubernetes application-based container offers on AKS for Azure Stack HCI or AKS Edge Essentials.

## Select and deploy a Kubernetes application

### From an AKS cluster

In the Azure portal, navigate to your AKS cluster resource.

From the service menu, under

**Settings**, select**Extensions + applications**>**Add**.You can search for an offer or publisher directly by name, or you can browse all offers. To view Kubernetes application offers, select

**Containers**under**Categories**.After you decide on an application, select the offer. The following example uses the

**TrilioVault for Kubernetes - BYOL**offer.Select

**Plans + Pricing**to ensure the terms are acceptable, and then select**Create**.Follow each page in the application creation process, filling in information for your resource group, your cluster, and any configuration options that the application requires. You can decide to deploy on a new AKS cluster or use an existing cluster.

Once you've filled in all the required information, select

**Review + create**>**Create**.It might take a few minutes for the application to deploy. You can monitor the deployment status from the

**Extensions + applications**page.

### Search in the Azure portal

From the Azure portal home page, search for and select

**Marketplace**.You can search for an offer or publisher directly by name, or you can browse all offers. To find Kubernetes application offers, on the left side under

**Categories**select**Containers**.After you decide on an application, select the offer. The following example uses the

**TrilioVault for Kubernetes - BYOL**offer.Select

**Plans + Pricing**to ensure the terms are acceptable, and then select**Create**.Follow each page in the application creation process, filling in information for your resource group, your cluster, and any configuration options that the application requires. You can decide to deploy on a new AKS cluster or use an existing cluster.

Once you've filled in all the required information, select

**Review + create**>**Create**.It might take a few minutes for the application to deploy. You can monitor the deployment status from the

**Extensions + applications**page.

## Verify the deployment

- Navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Verify that the extension is listed and the
*Provisioning State*shows**Succeeded**.

## Manage the offer lifecycle

For lifecycle management, a Kubernetes offer is represented as a cluster extension for AKS. For more information, see [Cluster extensions for AKS](cluster-extensions). Purchasing an offer from Azure Marketplace creates a new instance of the extension on your AKS cluster.

- In the Azure portal, navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Select an extension name to navigate to a properties view where you're able to disable autoupgrades, check the provisioning state, delete the extension instance, or modify configuration settings as needed.

## Monitor billing and usage information

- In the Azure portal, navigate to your cluster's resource group.
- From the service menu, under
**Cost Management**, select**Cost analysis**. Under**Product**, you can see a cost breakdown for the plan that you selected.

## Remove an offer

You can delete a purchased plan for an Azure container offer by deleting the extension instance on the cluster.

- Navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Select an application, then select
**Uninstall**.

## Troubleshooting

If you experience issues, see the [troubleshooting checklist for failed deployments of a Kubernetes offer](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-failed-kubernetes-deployment-offer).

## Next steps

- Learn more about
[exploring and analyzing costs](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis). - Learn more about
[deploying a Kubernetes application programmatically using Azure CLI](/en-us/azure/aks/deploy-application-az-cli). - Learn more about
[deploying a Kubernetes application using an ARM template](/en-us/azure/aks/deploy-application-template).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quickstart-event-grid -->

# Quickstart: Subscribe to Azure Kubernetes Service (AKS) events with Azure Event Grid

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Event Grid is a fully managed event routing service that provides uniform event consumption using a publish-subscribe model.

In this quickstart, you create an AKS cluster and subscribe to AKS events.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.

Note

AKS operations are independent of Azure Event Grid availability and aren't impacted during Event Grid [Service Outages](https://azure.status.microsoft/status).

## Create an AKS cluster

Create an AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a resource group *MyResourceGroup* and a cluster named *MyAKS* with one node in the *MyResourceGroup* resource group:

```
az group create --name MyResourceGroup --location eastus
az aks create --resource-group yResourceGroup --name MyAKS --location eastus --node-count 1 --generate-ssh-keys
```


## Subscribe to AKS events

Create a namespace and event hub using [az eventhubs namespace create](/en-us/cli/azure/eventhubs/namespace#az-eventhubs-namespace-create) and [az eventhubs eventhub create](/en-us/cli/azure/eventhubs/eventhub#az-eventhubs-eventhub-create). The following example creates a namespace *MyNamespace* and an event hub *MyEventGridHub* in *MyNamespace*, both in the *MyResourceGroup* resource group.

```
az eventhubs namespace create --location eastus --name MyNamespace --resource-group MyResourceGroup
az eventhubs eventhub create --name MyEventGridHub --namespace-name MyNamespace --resource-group MyResourceGroup
```


Note

The *name* of your namespace must be unique.

Subscribe to the AKS events using [az eventgrid event-subscription create](/en-us/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create):

```
SOURCE_RESOURCE_ID=$(az aks show --resource-group MyResourceGroup --name MyAKS --query id --output tsv)
ENDPOINT=$(az eventhubs eventhub show --resource-group MyResourceGroup --name MyEventGridHub --namespace-name MyNamespace --query id --output tsv)
az eventgrid event-subscription create --name MyEventGridSubscription \
--source-resource-id $SOURCE_RESOURCE_ID \
--endpoint-type eventhub \
--endpoint $ENDPOINT
```


Verify your subscription to AKS events using `az eventgrid event-subscription list`

:

```
az eventgrid event-subscription list --source-resource-id $SOURCE_RESOURCE_ID
```


The following example output shows you're subscribed to events from the *MyAKS* cluster and those events are delivered to the *MyEventGridHub* event hub:

```
[
{
"deadLetterDestination": null,
"deadLetterWithResourceIdentity": null,
"deliveryWithResourceIdentity": null,
"destination": {
"deliveryAttributeMappings": null,
"endpointType": "EventHub",
"resourceId": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/Microsoft.EventHub/namespaces/MyNamespace/eventhubs/MyEventGridHub"
},
"eventDeliverySchema": "EventGridSchema",
"expirationTimeUtc": null,
"filter": {
"advancedFilters": null,
"enableAdvancedFilteringOnArrays": null,
"includedEventTypes": [
"Microsoft.ContainerService.NewKubernetesVersionAvailable","Microsoft.ContainerService.ClusterSupportEnded","Microsoft.ContainerService.ClusterSupportEnding","Microsoft.ContainerService.NodePoolRollingFailed","Microsoft.ContainerService.NodePoolRollingStarted","Microsoft.ContainerService.NodePoolRollingSucceeded"
],
"isSubjectCaseSensitive": null,
"subjectBeginsWith": "",
"subjectEndsWith": ""
},
"id": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/Microsoft.ContainerService/managedClusters/MyAKS/providers/Microsoft.EventGrid/eventSubscriptions/MyEventGridSubscription",
"labels": null,
"name": "MyEventGridSubscription",
"provisioningState": "Succeeded",
"resourceGroup": "MyResourceGroup",
"retryPolicy": {
"eventTimeToLiveInMinutes": 1440,
"maxDeliveryAttempts": 30
},
"systemData": null,
"topic": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/microsoft.containerservice/managedclusters/MyAKS",
"type": "Microsoft.EventGrid/eventSubscriptions"
}
]
```


When AKS events occur, you see those events appear in your event hub. For example, when the list of available Kubernetes versions for your clusters changes, you see a `Microsoft.ContainerService.NewKubernetesVersionAvailable`

event. There are also new events available now for upgrades and cluster within support. For more information on the events AKS emits, see [Azure Kubernetes Service (AKS) as an Event Grid source](/en-us/azure/event-grid/event-schema-aks).

## Delete the cluster and subscriptions

Use the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, the AKS cluster, namespace, and event hub, and all related resources.

```
az group delete --name MyResourceGroup --yes --no-wait
```


Note

When you delete the cluster, the Microsoft Entra service principal used by the AKS cluster isn't removed. For steps on how to remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal).

If you used a managed identity, the identity is managed by the platform and doesn't require removal.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then subscribed to AKS events in Azure Event Hubs.

To learn more about AKS, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ha-dr-overview -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-fine-tune-language-models -->

# Concepts - Fine-tuning language models for AI and machine learning workflows

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about fine-tuning [language models](concepts-ai-ml-language-models), including some common methods and how applying the tuning results can improve the performance of your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## Pre-trained language models

*Pre-trained language models (PLMs)* offer an accessible way to get started with AI inferencing and are widely used in natural language processing (NLP). PLMs are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks. These models typically consist of billions of parameters, or *weights*, that are learned during the pre-training process.

PLMs can learn universal language representations that capture the statistical properties of natural language, such as the probability of words or sequences of words occurring in a given context. These representations can be transferred to downstream tasks, such as text classification, named entity recognition, and question answering, by fine-tuning the model on task-specific datasets.

### Pros and cons

The following table lists some pros and cons of using PLMs in your AI and machine learning workflows:

| Pros | Cons |
|---|---|
| • Get started quickly with deployment in your machine learning lifecycle. • Avoid heavy compute costs associated with model training. • Reduces the need to store large, labeled datasets. |
• Might provide generalized or outdated responses based on pre-training data sources. • Might not be suitable for all tasks or domains. • Performance can vary depending on inferencing context. |

## Fine-tuning methods

### Parameter efficient fine-tuning

*Parameter efficient fine-tuning (PEFT)* is a method for fine-tuning PLMs on relatively small datasets with limited compute resources. PEFT uses a combination of techniques, like additive and selective methods to update weights, to improve the performance of the model on specific tasks. PEFT requires minimal compute resources and flexible quantities of data, making it suitable for low-resource settings. This method retains most of the weights of the original pre-trained model and updates the remaining weights to fit context-specific, labeled data.

### Low rank adaptation

*Low rank adaptation (LoRA)* is a PEFT method commonly used to customize large language models for new tasks. This method tracks changes to model weights and efficiently stores smaller weight matrices that represent only the model's trainable parameters, reducing memory usage and the compute power needed for fine-tuning. LoRA creates fine-tuning results, known as *adapter layers*, that can be temporarily stored and pulled into the model's architecture for new inferencing jobs.

*Quantized low rank adaptation (QLoRA)* is an extension of LoRA that further reduces memory usage by introducing quantization to the adapter layers. For more information, see [Making LLMs even more accessible with bitsandbites, 4-bit quantization, and QLoRA](https://huggingface.co/blog/4bit-transformers-bitsandbytes#:%7E:text=We%20present%20QLoRA%2C%20an%20efficient%20finetuning%20approach%20that,pretrained%20language%20model%20into%20Low%20Rank%20Adapters%7E%20%28LoRA%29.).

## Experiment with fine-tuning language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The AI toolchain operator add-on leverages KAITO to simplify onboarding, save on infrastructure costs, and reduce the time-to-inference for open-source models on an AKS cluster. The add-on automatically provisions right-sized GPU nodes and sets up the associated inference server as an endpoint server to your chosen model.

With KAITO version 0.3.0 or later, you can efficiently fine-tune supported MIT and Apache 2.0 licensed models with the following features:

- Store your retraining data as a container image in a private container registry.
- Host the new adapter layer image in a private container registry.
- Efficiently pull the image for inferencing with adapter layers in new scenarios.

For guidance on getting started with fine-tuning on KAITO, see the [Kaito Tuning Workspace API documentation][kaito-fine-tuning]. To learn more about deploying language models with KAITO in your AKS clusters, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-services -->

# Kubernetes Services in AKS

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can use Kubernetes Services to logically group pods and provide network connectivity by allowing direct access to them through a specific IP address or DNS name on a designated port. This allows you to expose your application workloads to other services within the cluster or to external clients without having to manually manage the network configuration for each pod hosting a workload.

You can specify what kind of service you want using Kubernetes *Service type values*. For more information, see the

[Kubernetes Service documentation](https://kubernetes.io/docs/concepts/services-networking/service/#publishing-services-service-types).

The following Service types are available in AKS: [ ClusterIP](#clusterip),

[,](#nodeport)

`NodePort`

[, and](#loadbalancer)

`LoadBalancer`

[.](#externalname)

`ExternalName`

## ClusterIP

`ClusterIP`

creates an internal IP address for use within the AKS cluster. The `ClusterIP`

Service is good for *internal-only applications* that support other workloads within the cluster. ClusterIP is used by default if you don't explicitly specify a type for a Service.


## NodePort

`NodePort`

creates a port mapping on the underlying node that allows the application to be accessed directly with the node IP address and port.


## LoadBalancer

`LoadBalancer`

creates an Azure load balancer resource, configures an external IP address, and connects the requested pods to the load balancer backend pool. To allow customer traffic to reach the application, load balancing rules are created on the desired ports.


For HTTP load balancing of inbound traffic, you can also use an [Ingress controller](concepts-network-ingress#ingress-controllers).

You can also use the `LoadBalancer`

type to create multiple public load balancers in a single AKS cluster. This is useful for large clusters or port-heavy workloads that can quickly exhaust the limits of a single load balancer. For more information, see [Use multiple public load balancers in Azure Kubernetes Service (preview)](use-multiple-standard-load-balancer).

## ExternalName

`ExternalName`

creates a specific DNS entry for easier application access. You can dynamically assign the load balancers and service IP address, or you can specify an existing static IP address. You can assign both internal and external static IP addresses. Existing static IP addresses are often tied to a DNS entry.

You can create both *internal* and *external* load balancers. Internal load balancers are only assigned a private IP address, so they can't be accessed from the Internet.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-hybrid-benefit -->

# What is Azure Hybrid Benefit for Azure Kubernetes Service?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Hybrid Benefit is a program that enables you to significantly reduce the costs of running workloads in the cloud. With Azure Hybrid Benefit for Azure Kubernetes Service (AKS), you can maximize the value of your on-premises licenses and modernize your applications at no extra cost. Azure Hybrid Benefit enables you to use your on-premises licenses that also have either active Software Assurance (SA) or a qualifying subscription to get Windows virtual machines (VMs) on Azure at a reduced cost.

For more information on qualifications for Azure Hybrid Benefit, what is included with it, how to stay compliant, and more, check out [Azure Hybrid Benefit for Windows Server](/en-us/azure/virtual-machines/windows/hybrid-use-benefit-licensing).

Note

Azure Hybrid Benefit for Azure Kubernetes Service follows the same licensing guidance as Azure Hybrid Benefit for Windows Server VMs on Azure.

## Enable Azure Hybrid Benefit for Azure Kubernetes Service

Azure Hybrid Benefit for Azure Kubernetes Service can be enabled at cluster creation or on an existing AKS cluster. You can enable and disable Azure Hybrid Benefit using either the Azure CLI or Azure PowerShell. In the following examples, be sure to replace the variable definitions with values matching your own cluster.

To create a new AKS cluster with Azure Hybrid Benefit enabled:

```
PASSWORD='' # replace with your own password value
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks create \
--resource-group $RG_NAME \
--name $CLUSTER \
--load-balancer-sku Standard \
--network-plugin azure \
--windows-admin-username azure \
--windows-admin-password $PASSWORD \
--enable-ahub \
--generate-ssh-keys
```


To enable Azure Hybrid Benefit on an existing AKS cluster:

```
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks update --resource-group $RG_NAME --name $CLUSTER--enable-ahub
```


## Disable Azure Hybrid Benefit for Azure Kubernetes Service

To disable Azure Hybrid Benefit for an AKS cluster:

```
RG_NAME='myResourceGroup'
CLUSTER='myAKSCluster'
az aks update --resource-group $RG_NAME --name $CLUSTER --disable-ahub
```


## Next steps

To learn more about Windows containers on AKS, see the following resources:

[Learn how to deploy, manage, and monitor Windows containers on AKS](/en-us/training/paths/deploy-manage-monitor-wincontainers-aks).- Open an issue or provide feedback in the
[Windows containers GitHub repository](https://github.com/microsoft/Windows-Containers/issues). - Review the
[third-party partner solutions for Windows on AKS](windows-aks-partner-solutions).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-identity-access -->

# Connect your Azure identity provider to the Azure Key Vault Secrets Store CSI Driver in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Secrets Store Container Storage Interface (CSI) Driver on Azure Kubernetes Service (AKS) provides various methods of identity-based access to your Azure Key Vault. This article outlines these methods and best practices for when to use Azure role-based access control (Azure RBAC) or OpenID Connect (OIDC) security models to access your key vault and AKS cluster.

You can use one of the following access methods:

- Service Connector with managed identity
- Workload ID
- User-assigned managed identity

Learn how to connect to Azure Key Vault with the Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster using Service Connector. In this article, you complete the following tasks:

- Create an AKS cluster and an Azure Key Vault.
- Create a connection between the AKS cluster and the Azure Key Vault with Service Connector.
- Create a
`SecretProviderClass`

CRD and a`Pod`

that consumes the CSI provider to test the connection. - Clean up resources.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The
[Azure CLI](/en-us/cli/azure/install-azure-cli). Sign in using thecommand.`az login`

[Docker](https://docs.docker.com/get-docker/)and[kubectl](https://kubernetes.io/docs/tasks/tools/). To install kubectl locally, use thecommand.`az aks install-cli`

- A basic understanding of containers and AKS. Get started by
[preparing an application for AKS](/en-us/azure/aks/tutorial-kubernetes-prepare-app). - Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster.

## Initial set-up

If you're using Service Connector for the first time, start by running the command

[az provider register](/en-us/cli/azure/provider#az-provider-register)to register the Service Connector and Kubernetes Configuration resource providers.`az provider register -n Microsoft.ServiceLinker`

`az provider register -n Microsoft.KubernetesConfiguration`

Tip

You can check if these resource providers have already been registered by running the commands

`az provider show -n "Microsoft.ServiceLinker" --query registrationState`

and`az provider show -n "Microsoft.KubernetesConfiguration" --query registrationState`

.Optionally, use the Azure CLI command to get a list of supported target services for AKS cluster.

`az aks connection list-support-types --output table`


## Create Azure resources

Create a resource group using the

command.`az group create`

`az group create \ --name <resource-group-name> \ --location <location>`

Create an AKS cluster using the

command. The following example creates a single-node AKS cluster with managed identity enabled.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --enable-managed-identity \ --node-count 1`

Connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group <resource-group-name> \ --name <cluster-name>`

Create an Azure key vault using the

command.`az keyvault create`

`az keyvault create \ --resource-group <resource-group-name> \ --name <key-vault-name> \ --location <location>`

Create a secret in the key vault using the

command.`az keyvault secret set`

`az keyvault secret set \ --vault-name <key-vault-name> \ --name <secret-name> \ --value <secret-value>`


## Create a service connection in AKS with Service Connector

You can create a service connection to Azure Key Vault using the Azure portal or Azure CLI.

In the Azure portal, navigate to your AKS cluster resource.

From the service menu, under

**Settings**, select**Service Connector**>**Create**.On the

**Create connection**page, configure the following settings in the**Basics**tab:**Kubernetes namespace**: Select**default**.**Service type**: Select**Key Vault**and select the checkbox to enable the Azure Key Vault CSI Provider.**Connection name**: Enter a name for the connection.**Subscription**: Select the subscription that contains the key vault.**Key vault**: Select the key vault you created.**Client type**: Select**None**.

Select

**Review + create**, and then select**Create**to create the connection.

## Test the connection

### Clone the sample repo and deploy manifest files

Clone the sample repository using the

`git clone`

command.`git clone https://github.com/Azure-Samples/serviceconnector-aks-samples.git`

Change directories to the Azure Key Vault CSI provider sample.

`cd serviceconnector-aks-samples/azure-keyvault-csi-provider`

In the

`secret_provider_class.yaml`

file, replace the following placeholders with your Azure Key Vault information:- Replace
`<AZURE_KEYVAULT_NAME>`

with the name of the key vault you created and connected. - Replace
`<AZURE_KEYVAULT_TENANTID>`

with the tenant ID of the key vault. - Replace
`<AZURE_KEYVAULT_CLIENTID>`

with identity client ID of the`azureKeyvaultSecretsProvider`

addon. - Replace
`<KEYVAULT_SECRET_NAME>`

with the key vault secret you created. For example,`ExampleSecret`

.

- Replace
Deploy the

`SecretProviderClass`

CRD using the`kubectl apply`

command.`kubectl apply -f secret_provider_class.yaml`

Deploy the

`Pod`

manifest file using the`kubectl apply`

command.The command creates a pod named

`sc-demo-keyvault-csi`

in the default namespace of your AKS cluster.`kubectl apply -f pod.yaml`


### Verify the connection

Verify the pod was created successfully using the

`kubectl get`

command.`kubectl get pod/sc-demo-keyvault-csi`

After the pod starts, the mounted content at the volume path specified in your deployment YAML is available.

Show the secrets held in the secrets store using the

`kubectl exec`

command.`kubectl exec sc-demo-keyvault-csi -- ls /mnt/secrets-store/`

Display a secret using the

`kubectl exec`

command.This example command shows a test secret named

`ExampleSecret`

.`kubectl exec sc-demo-keyvault-csi -- cat /mnt/secrets-store/ExampleSecret`


## Prerequisites for CSI Driver

- Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster. - Microsoft Entra Workload ID supports both Windows and Linux clusters.

## Access with a Microsoft Entra Workload ID

A [Microsoft Entra Workload ID](workload-identity-overview) is an identity that an application running on a pod uses to authenticate itself against other Azure services, such as workloads in software. The Secret Store CSI Driver integrates with native Kubernetes capabilities to federate with external identity providers.

In this security model, the AKS cluster acts as token issuer. Microsoft Entra ID then uses OIDC to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. For your workload to exchange a service account token projected to its volume for a Microsoft Entra token, you need the Azure Identity client library in the Azure SDK or the Microsoft Authentication Library (MSAL)

Note

- This authentication method replaces Microsoft Entra pod-managed identity (preview). The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated as of October 24, 2022.
- Microsoft Entra Workload ID supports both Windows and Linux clusters.

### Configure workload identity

Set your subscription using the

command.`az account set`

`export SUBSCRIPTION_ID=<subscription id> export RESOURCE_GROUP=<resource group name> export UAMI=<name for user assigned identity> export KEYVAULT_NAME=<existing keyvault name> export CLUSTER_NAME=<aks cluster name> az account set --subscription $SUBSCRIPTION_ID`

Create a managed identity using the

command.`az identity create`

Note

This step assumes you have an existing AKS cluster with workload identity enabled. If workload identity isn't enabled, see

[Enable workload identity on an existing AKS cluster](workload-identity-deploy-cluster#enable-oidc-issuer-and-microsoft-entra-workload-id-on-an-aks-cluster)to enable it.`az identity create --name $UAMI --resource-group $RESOURCE_GROUP export USER_ASSIGNED_CLIENT_ID="$(az identity show --resource-group $RESOURCE_GROUP --name $UAMI --query 'clientId' -o tsv)" export IDENTITY_TENANT=$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query identity.tenantId -o tsv)`

Create a role assignment that grants the workload identity permission to access the key vault secrets, access keys, and certificates using the

command.`az role assignment create`

Important

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`key`

or`certificate`

type, assign therole to give permissions.`Key Vault Certificate User`

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`secret`

type, assign therole.`Key Vault Secrets User`

- If your key vault isn't set with
`--enable-rbac-authorization`

, you can use thecommand with the`az keyvault set-policy`

`--key-permissions get`

,`--certificate-permissions get`

, or`--secret-permissions get`

parameter to create a key vault policy to grant access for keys, certificates, or secrets. For example:

`az keyvault set-policy --name $KEYVAULT_NAME --key-permissions get --object-id $IDENTITY_OBJECT_ID`

`export KEYVAULT_SCOPE=$(az keyvault show --name $KEYVAULT_NAME --query id -o tsv) # Example command for key vault with Azure RBAC enabled using `key` type az role assignment create --role "Key Vault Certificate User" --assignee $USER_ASSIGNED_CLIENT_ID --scope $KEYVAULT_SCOPE`

- If your key vault is set with
Get the AKS cluster OIDC Issuer URL using the

command.`az aks show`

Note

This step assumes you have an existing AKS cluster with the OIDC Issuer URL enabled. If the OIDC Issuer URL isn't enabled, see

[Update an AKS cluster with OIDC Issuer](use-oidc-issuer#enable-the-oidc-issuer-on-an-existing-aks-cluster)to enable it.`export AKS_OIDC_ISSUER="$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query "oidcIssuerProfile.issuerUrl" -o tsv)" echo $AKS_OIDC_ISSUER`

Establish a federated identity credential between the Microsoft Entra application, service account issuer, and subject. Get the object ID of the Microsoft Entra application using the following commands. Make sure to update the values for

`serviceAccountName`

and`serviceAccountNamespace`

with the Kubernetes service account name and its namespace.`export SERVICE_ACCOUNT_NAME="workload-identity-sa" # sample name; can be changed export SERVICE_ACCOUNT_NAMESPACE="default" # can be changed to namespace of your workload cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${USER_ASSIGNED_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`

Create the federated identity credential between the managed identity, service account issuer, and subject using the

command.`az identity federated-credential create`

`export FEDERATED_IDENTITY_NAME="aksfederatedidentity" # can be changed as needed az identity federated-credential create --name $FEDERATED_IDENTITY_NAME --identity-name $UAMI --resource-group $RESOURCE_GROUP --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME}`

Deploy a

`SecretProviderClass`

using the`kubectl apply`

command and the following YAML script.`cat <<EOF | kubectl apply -f - # This is a SecretProviderClass example using workload identity to access your key vault apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-kvname-wi # needs to be unique per namespace spec: provider: azure parameters: usePodIdentity: "false" clientID: "${USER_ASSIGNED_CLIENT_ID}" # Setting this to use workload identity keyvaultName: ${KEYVAULT_NAME} # Set to the name of your key vault cloudName: "" # [OPTIONAL for Azure] if not provided, the Azure environment defaults to AzurePublicCloud objects: | array: - | objectName: secret1 # Set to the name of your secret objectType: secret # object types: secret, key, or cert objectVersion: "" # [OPTIONAL] object versions, default to latest if empty - | objectName: key1 # Set to the name of your key objectType: key objectVersion: "" tenantId: "${IDENTITY_TENANT}" # The tenant ID of the key vault EOF`

Note

If you use

`objectAlias`

instead of`objectName`

, update the YAML script to account for it.Note

In order for the

`SecretProviderClass`

to function properly, make sure to populate your Azure Key Vault with secrets, keys, or certificates before referencing them in the`objects`

section.Deploy a sample pod using the

`kubectl apply`

command and the following YAML script.`cat <<EOF | kubectl apply -f - # This is a sample pod definition for using SecretProviderClass and workload identity to access your key vault kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline-wi labels: azure.workload.identity/use: "true" spec: serviceAccountName: "workload-identity-sa" containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-kvname-wi" EOF`


## Prerequisites for CSI Driver

- Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster.

## Access with managed identity

A [Microsoft Entra Managed ID](/en-us/entra/identity/managed-identities-azure-resources/overview) is an identity that an administrator uses to authenticate themselves against other Azure services. The managed identity uses Azure RBAC to federate with external identity providers.

In this security model, you can grant access to your cluster's resources to team members or tenants sharing a managed role. The role is checked for scope to access the keyvault and other credentials. When you [enabled the Azure Key Vault provider for Secrets Store CSI Driver on your AKS Cluster](csi-secrets-store-driver#create-an-aks-cluster-with-azure-key-vault-provider-for-secrets-store-csi-driver-support), it created a user identity.

### Configure managed identity

Access your key vault using the

command and the user-assigned managed identity created by the add-on. You should also retrieve the identity's`az aks show`

`clientId`

, which you use in later steps when creating a`SecretProviderClass`

.`az aks show --resource-group <resource-group> --name <cluster-name> --query addonProfiles.azureKeyvaultSecretsProvider.identity.objectId -o tsv az aks show --resource-group <resource-group> --name <cluster-name> --query addonProfiles.azureKeyvaultSecretsProvider.identity.clientId -o tsv`

Alternatively, you can create a new managed identity and assign it to your virtual machine (VM) scale set or to each VM instance in your availability set using the following commands.

`az identity create --resource-group <resource-group> --name <identity-name> az vmss identity assign --resource-group <resource-group> --name <agent-pool-vmss> --identities <identity-resource-id> az vm identity assign --resource-group <resource-group> --name <agent-pool-vm> --identities <identity-resource-id> az identity show --resource-group <resource-group> --name <identity-name> --query 'clientId' -o tsv`

Create a role assignment that grants the identity permission to access the key vault secrets, access keys, and certificates using the

command.`az role assignment create`

Important

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`key`

or`certificate`

type, assign therole.`Key Vault Certificate User`

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`secret`

type, assign therole.`Key Vault Secrets User`

- If your key vault isn't set with
`--enable-rbac-authorization`

, you can use thecommand with the`az keyvault set-policy`

`--key-permissions get`

,`--certificate-permissions get`

, or`--secret-permissions get`

parameter to create a key vault policy to grant access for keys, certificates, or secrets. For example:

`az keyvault set-policy --name $KEYVAULT_NAME --key-permissions get --object-id $IDENTITY_OBJECT_ID`

`export IDENTITY_OBJECT_ID="$(az identity show --resource-group <resource-group> --name <identity-name> --query 'principalId' -o tsv)" export KEYVAULT_SCOPE=$(az keyvault show --name <key-vault-name> --query id -o tsv) # Example command for key vault with Azure RBAC enabled using `key` type az role assignment create --role "Key Vault Certificate User" --assignee $USER_ASSIGNED_CLIENT_ID --scope $KEYVAULT_SCOPE`

- If your key vault is set with
Create a

`SecretProviderClass`

using the following YAML. Make sure to use your own values for`userAssignedIdentityID`

,`keyvaultName`

,`tenantId`

, and the objects to retrieve from your key vault.`# This is a SecretProviderClass example using user-assigned identity to access your key vault apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-kvname-user-msi spec: provider: azure parameters: usePodIdentity: "false" useVMManagedIdentity: "true" # Set to true for using managed identity userAssignedIdentityID: <client-id> # Set the clientID of the user-assigned managed identity to use keyvaultName: <key-vault-name> # Set to the name of your key vault cloudName: "" # [OPTIONAL for Azure] if not provided, the Azure environment defaults to AzurePublicCloud objects: | array: - | objectName: secret1 objectType: secret # object types: secret, key, or cert objectVersion: "" # [OPTIONAL] object versions, default to latest if empty - | objectName: key1 objectType: key objectVersion: "" tenantId: <tenant-id> # The tenant ID of the key vault`

Note

If you use

`objectAlias`

instead of`objectName`

, make sure to update the YAML script.Note

In order for the

`SecretProviderClass`

to function properly, make sure to populate your Azure Key Vault with secrets, keys, or certificates before referencing them in the`objects`

section.Apply the

`SecretProviderClass`

to your cluster using the`kubectl apply`

command.`kubectl apply -f secretproviderclass.yaml`

Create a pod using the following YAML.

`# This is a sample pod definition for using SecretProviderClass and the user-assigned identity to access your key vault kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline-user-msi spec: containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-kvname-user-msi"`

Apply the pod to your cluster using the

`kubectl apply`

command.`kubectl apply -f pod.yaml`


## Validate Key Vault secrets

After the pod starts, the mounted content at the volume path specified in your deployment YAML is available. Use the following commands to validate your secrets and print a test secret.

Show secrets held in the secrets store using the following command.

`kubectl exec busybox-secrets-store-inline-user-msi -- ls /mnt/secrets-store/`

Display a secret in the store using the following command. This example command shows the test secret

`ExampleSecret`

.`kubectl exec busybox-secrets-store-inline-user-msi -- cat /mnt/secrets-store/ExampleSecret`


## Obtain certificates and keys

The Azure Key Vault design makes sharp distinctions between keys, secrets, and certificates. The certificate features of the Key Vault service are designed to make use of key and secret capabilities. When you create a key vault certificate, it creates an addressable key and secret with the same name. This key allows authentication operations, and the secret allows the retrieval of the certificate value as a secret.

A key vault certificate also contains public x509 certificate metadata. The key vault stores both the public and private components of your certificate in a secret. You can obtain each individual component by specifying the `objectType`

in `SecretProviderClass`

. The following table shows which objects map to the various resources associated with your certificate:

| Object | Return value | Returns entire certificate chain |
|---|---|---|
`key` |
The public key, in Privacy Enhanced Mail (PEM) format. | N/A |
`cert` |
The certificate, in PEM format. | No |
`secret` |
The private key and certificate, in PEM format. | Yes |

## Disable the addon on existing clusters

Note

Before you disable the add-on, ensure that *no* `SecretProviderClass`

is in use. Trying to disable the add-on while a `SecretProviderClass`

exists results in an error.

Disable the Azure Key Vault provider for Secrets Store CSI Driver capability in an existing cluster using the [ az aks disable-addons](/en-us/cli/azure/aks#az-aks-disable-addons) command with the

`azure-keyvault-secrets-provider`

add-on.```
az aks disable-addons --addons azure-keyvault-secrets-provider --resource-group myResourceGroup --name myAKSCluster
```


Note

When you disable the add-on, existing workloads should have no issues or see any updates in the mounted secrets. If the pod restarts or a new pod is created as part of scale-up event, the pod fails to start because the driver is no longer running.

## Next steps

In this article, you learned how to create and provide an identity to access your Azure Key Vault. The [Service Connector](/en-us/azure/service-connector/overview) integration helps simplify the connection configuration for AKS workloads and Azure backing services. It securely handles authentication and network configurations and follows best practices for connecting to Azure services. For more information, see [Use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster](/en-us/azure/service-connector/tutorial-python-aks-keyvault-csi-driver) and the [Service Connector introduction](https://blog.aks.azure.com/2024/05/23/service-connector-intro).

If you want to configure extra configuration options or perform troubleshooting, see [Configuration options and troubleshooting resources for Azure Key Vault provider with Secrets Store CSI Driver in AKS](csi-secrets-store-configuration-options).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-multi-region -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr -->

# Install the Dapr extension for Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Dapr](dapr-overview) simplifies building resilient, stateless, and stateful applications that run on the cloud and edge and embrace the diversity of languages and developer frameworks. With Dapr's sidecar architecture, you can keep your code platform agnostic while tackling challenges around building microservices, like:

- Calling other services reliably and securely
- Building event-driven apps with pub/sub
- Building applications that are portable across multiple cloud services and hosts (for example, Kubernetes vs. a virtual machine)

Note

If you plan on installing Dapr in a Kubernetes production environment, see the [Dapr guidelines for production usage](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-production) documentation page.

## How it works

The Dapr extension uses the Azure CLI or a Bicep template to provision the Dapr control plane on your AKS or Arc-enabled Kubernetes cluster, creating the following Dapr services:

| Dapr service | Description |
|---|---|
`dapr-operator` |
Manages component updates and Kubernetes services endpoints for Dapr (state stores, pub/subs, etc.) |
`dapr-sidecar-injector` |
Injects Dapr into annotated deployment pods and adds the environment variables `DAPR_HTTP_PORT` and `DAPR_GRPC_PORT` to enable user-defined applications to easily communicate with Dapr without hard-coding Dapr port values. |
`dapr-placement` |
Used for actors only. Creates mapping tables that map actor instances to pods. |
`dapr-sentry` |
Manages mTLS between services and acts as a certificate authority. For more information, read the
|

Once Dapr is installed on your cluster, you can begin to develop using the Dapr building block APIs by [adding a few annotations](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-overview/#adding-dapr-to-a-kubernetes-deployment) to your deployments. For a more in-depth overview of the building block APIs and how to best use them, see the [Dapr building blocks overview](https://docs.dapr.io/developing-applications/building-blocks/).

Warning

If you install Dapr through the AKS or Arc-enabled Kubernetes extension, our recommendation is to continue using the extension for future management of Dapr instead of the Dapr CLI. Combining the two tools can cause conflicts and result in undesired behavior.

## Prerequisites

- An Azure subscription.
[Don't have one? Create a free account.](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) - The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli). - An existing
[AKS cluster](tutorial-kubernetes-deploy-cluster)or connected[Arc-enabled Kubernetes cluster](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster). [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)

Select how you'd like to install, deploy, and configure the Dapr extension.

## Before you begin

### Add the Azure CLI extension for cluster extensions

Install the `k8s-extension`

Azure CLI extension by running the following commands:

```
az extension add --name k8s-extension
```


If the `k8s-extension`

extension is already installed, you can update it to the latest version using the following command:

```
az extension update --name k8s-extension
```


### Register the `KubernetesConfiguration`

resource provider

If you aren't already using cluster extensions, you may need to register the resource provider with your subscription. You can check the status of the provider registration using the [az provider list](/en-us/cli/azure/provider#az-provider-list) command, as shown in the following example:

```
az provider list --query "[?contains(namespace,'Microsoft.KubernetesConfiguration')]" -o table
```


The *Microsoft.KubernetesConfiguration* provider should report as *Registered*, as shown in the following example output:

```
Namespace RegistrationState RegistrationPolicy
--------------------------------- ------------------- --------------------
Microsoft.KubernetesConfiguration Registered RegistrationRequired
```


If the provider shows as *NotRegistered*, register the provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) as shown in the following example:

```
az provider register --namespace Microsoft.KubernetesConfiguration
```


### Register the `ExtensionTypes`

feature to your Azure subscription

The `ExtensionTypes`

feature needs to be registered to your Azure subscription. In the terminal, verify you're in the correct subscription:

```
az account set --subscription <YOUR-AZURE-SUBSCRIPTION-ID>
```


Register the `ExtensionTypes`

feature.

```
az feature registration create --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


Feature registration may take some time. After a few minutes, check the registration status using the following command:

```
az feature show --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


## Create the extension and install Dapr on your AKS or Arc-enabled Kubernetes cluster

When installing the Dapr extension, use the flag value that corresponds to your cluster type:

**AKS cluster**:`--cluster-type managedClusters`

.**Arc-enabled Kubernetes cluster**:`--cluster-type connectedClusters`

.

Note

If you're using Dapr OSS on your AKS cluster and would like to install the Dapr extension for AKS, read more about [how to successfully migrate to the Dapr extension](dapr-migration).

Create the Dapr extension, which installs Dapr on your AKS or Arc-enabled Kubernetes cluster.

For example, install the latest version of Dapr via the Dapr extension on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false
```


### Keep your managed AKS cluster updated to the latest version

Based on your environment (dev, test, or production), you can keep up-to-date with the latest stable Dapr versions.

#### Choosing a release train

When configuring the extension, you can choose to install Dapr from a particular release train. Specify one of the two release train values:

| Value | Description |
|---|---|
`stable` |
Default. |
`dev` |
Early releases that can contain experimental features. Not suitable for production. |

For example:

```
--release-train stable
```


#### Configuring automatic updates to Dapr control plane

Warning

Auto-upgrade is not suitable for production environments. Only enable automatic updates to the Dapr control plane in dev or test environments. [Learn how to manually upgrade to the latest Dapr version for production environments.](#viewing-the-latest-stable-dapr-versions-available)

If you install Dapr without specifying a version, `--auto-upgrade-minor-version`

*is automatically enabled*, configuring the Dapr control plane to automatically update its minor version on new releases.

You can disable auto-update by specifying the `--auto-upgrade-minor-version`

parameter and setting the value to `false`

.

[Dapr versioning is in MAJOR.MINOR.PATCH format](https://docs.dapr.io/operations/support/support-versioning/#versioning), which means

`1.11.0`

to `1.12.0`

is a *minor*version upgrade.

```
--auto-upgrade-minor-version true
```


#### Viewing the latest stable Dapr versions available

To upgrade to the latest Dapr version in a production environment, you need to manually upgrade. Start by viewing a list of the stable Dapr versions available to your managed AKS cluster. Run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable
```


To see the latest stable Dapr version available to your managed AKS cluster, run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable --show-latest
```


To view a list of the stable Dapr versions available *by location*:

[Make sure you've registered the](dapr#register-the-extensiontypes-feature-to-your-azure-subscription)`ExtensionTypes`

feature to your Azure subscription.- Run the following command.

```
az k8s-extension extension-types list-versions-by-location --location westus --extension-type microsoft.dapr
```


[Next, manually update Dapr to the latest stable version.](#targeting-a-specific-dapr-version)

#### Targeting a specific Dapr version

Note

Dapr is supported with a rolling window, including only the current and previous versions. It is your operational responsibility to remain up to date with these supported versions. If you have an older version of Dapr, you may have to do intermediate upgrades to get to a supported version.

The same command-line argument is used for installing a specific version of Dapr or rolling back to a previous version. Set `--auto-upgrade-minor-version`

to `false`

and `--version`

to the version of Dapr you wish to install. If the `version`

parameter is omitted, the extension installs the latest version of Dapr. The following example command installs Dapr version `1.14.4-msft.10`

on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false \
--version 1.14.4-msft.10
```


## Troubleshooting

### Troubleshooting extension management errors

If the extension fails to create or update, try suggestions and solutions in the [Dapr extension troubleshooting guide](dapr-troubleshooting).

### Troubleshooting Dapr functional errors

Troubleshoot Dapr open source errors unrelated to the extension via the [common Dapr issues and solutions guide](https://docs.dapr.io/operations/troubleshooting/common_issues/).

## Support

Note

Learn more about [how Microsoft handles issues raised for the Dapr extension](dapr-overview#issue-handling).

If you're experiencing Dapr runtime security risks and regressions while using the extension, open an issue with the [Dapr open source project](https://github.com/dapr/dapr/issues/new/choose).

You could also start a discussion in the Dapr project Discord:

## Delete the Dapr extension from your cluster

The process of uninstalling the Dapr extension from AKS does not delete the CRDs created during installation. These CRDs remain in the cluster as residual components, essential for the reconciler during the installation and uninstallation of the extension.

To clean the cluster of these CRDs, you can manually delete them **after** the Dapr extension has been completely uninstalled from AKS.

### Uninstalling the extension

Delete the extension from your AKS cluster using the following command:

```
az k8s-extension delete --resource-group <myResourceGroup> --cluster-name <myAKSCluster> --cluster-type managedClusters --name dapr
```


Or, if using a Bicep template, you can delete the template.

### Listing the CRDs in your cluster

To find the CRDs you'd like to remove, run the following command:

```
kubectl get crds | findstr dapr.io
```

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-isolated -->

# Network isolated Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Organizations typically have strict security and compliance requirements to regulate egress (outbound) network traffic from a cluster to eliminate risks of data exfiltration. By default, standard SKU Azure Kubernetes Service (AKS) clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. The conceptual document on [outbound network and fully qualified domain name (FQDN) rules for AKS clusters](outbound-rules-control-egress) provides a list of required endpoints for the AKS cluster and its optional add-ons and features.

One common solution to restricting outbound traffic from the cluster is to use a [firewall device](limit-egress-traffic) to restrict traffic based on firewall rules. Firewall is applicable when your application requires outbound access, but when outbound requests have to be inspected and secured. Configuring a firewall manually with required egress rules and *FQDNs* is a cumbersome process especially if your only requirement is to create an isolated AKS cluster with no outbound dependencies for the cluster bootstrapping.

To reduce risk of data exfiltration, network isolated cluster allows for bootstrapping the AKS cluster without any outbound network dependencies, even for fetching cluster components/images from Microsoft Artifact Registry (MAR). The cluster operator could incrementally set up allowed outbound traffic for each scenario they want to enable.

## How a network isolated cluster works

The following diagram shows the network communication between dependencies for a network isolated cluster.


AKS clusters fetch artifacts required for the cluster and its features or add-ons from the Microsoft Artifact Registry (MAR). This image pull allows AKS to provide newer versions of the cluster components and to also address critical security vulnerabilities. A network isolated cluster attempts to pull those images and binaries from a private Azure Container Registry (ACR) instance connected to the cluster instead of pulling from MAR. If the images aren't present, the private ACR pulls them from MAR and serves them via its private endpoint, eliminating the need to enable egress from the cluster to the public MAR endpoint.

The following two options are supported for a private ACR associated with network isolated clusters:

**AKS-managed ACR**- AKS creates, manages, and reconciles an ACR resource in this option. There's nothing you need to do.Note

The AKS-managed ACR resource is created in your subscription. If you delete the cluster with AKS-managed ACR for bootstrap artifact source. Related resources such as the AKS-managed ACR, private link, and private endpoint are also automatically deleted. If you change outbound type on a cluster to any type other than

`none`

or`block`

with`--bootstrap-artifact-source`

retained as`Cache`

. Then the related resources are not deleted.**Bring your own (BYO) ACR**- The BYO ACR option requires creating an ACR with a private link between the ACR resource and the AKS cluster. See[Connect privately to an Azure container registry using Azure Private Link](/en-us/azure/container-registry/container-registry-private-link)to understand how to configure a private endpoint for your registry. You also need to assign permissions and manage the cache rules, private link, and private endpoint used in the cluster.Note

When you delete the AKS cluster or after you disable the feature. The BYO ACR, private link, and private endpoint aren't deleted automatically. If you add customized images and cache rules to the BYO ACR, they persist after cluster reconciliation.


To create a network isolated cluster, you need to first ensure network traffic between your API server and your node pools remains only on the private network, you can choose one of the following private cluster modes:

[Private link-based cluster](private-clusters)- The control plane or API server is in an AKS-managed Azure resource group, and your node pool is in your resource group. The server and the node pool can communicate with each other through the Azure Private Link service in the API server virtual network and a private endpoint which is exposed on the subnet of your AKS cluster.[API Server VNet Integration configured cluster](api-server-vnet-integration)- A cluster configured with API Server VNet Integration projects the API server endpoint directly into a delegated subnet in the virtual network where AKS is deployed. API Server VNet Integration enables network communication between the API server and the cluster nodes without requiring a private link or tunnel.

You also need to ensure the egress path for your AKS cluster are controlled and limited, you can choose one of the following network outbound types:

[Outbound type of](/en-us/azure/aks/egress-outboundtype#outbound-type-of-none)- If`none`

`none`

is set. AKS doesn't automatically configure egress paths and a default route is not required. It is supported in both bring-your-own (BYO) virtual network scenarios and managed virtual network scenarios. For bring your own virtual network scenario, you must establish explicit egress paths if needed.[Outbound type of](/en-us/azure/aks/egress-outboundtype#outbound-type-of-block-preview)-If`block`

(preview)`block`

is set. AKS configures network rules to actively block all egress traffic from the cluster. This option is useful for highly secure environments where outbound connectivity must be restricted. It is supported in managed virtual network scenario. You can also achieve similar effect by blocking all egress traffic by adding[network security group (NSG)](/en-us/azure/virtual-network/network-security-groups-overview)rules with`none`

in bring-your-own virtual network scenario.

Note

Outbound type of `none`

is generally available.
Outbound type `block`

is in preview.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Limitations

`Unmanaged`

channel is not supported.- Windows node pools are not yet supported.
- kubenet networking is not supported.

Caution

If you are using [Node Public IP](use-node-public-ips) in network isolated AKS clusters, it will allow outbound traffic with outbound type `none`

.

## Using features, add-ons, and extensions requiring egress

For network isolated clusters with BYO ACR:

- If you want to use any AKS feature or add-on that requires outbound network access in network isolated clusters with outbound type
`none`

,[this document](outbound-rules-control-egress)contains the outbound network requirements for each feature. Also, this doc enumerates the features or add-ons that support private link integration for secure connection from within the cluster's virtual network. It is recommended to set up private endpoints to access these features. For example, you can set up[private endpoint based ingestion](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-private-link)to use Managed Prometheus (Azure Monitor workspace) and Container insights (Log Analytics workspace) in network isolated clusters. If a private link integration is not available for any of these features. Then you can set up the cluster with a[user-defined routing table and an Azure Firewall](limit-egress-traffic)based on the network rules and application rules that required for that feature. - If you are using
[Azure Container Storage Interface (CSI) driver](azure-files-csi)for Azure Files and Blob storage, you must create a custom storage class with "networkEndpointType: privateEndpoint", see examples in[Azure Files storage classes](/en-us/azure/aks/azure-csi-files-storage-provision#dynamically-provision-a-volume)and[Azure Blob storage classes](/en-us/azure/aks/azure-csi-blob-storage-provision?tabs=mount-nfs%2Csecret#storage-class-parameters-for-dynamic-persistent-volumes). - The following AKS cluster extensions aren't supported yet on network isolated clusters:

## Frequently asked questions

### What's the difference between network isolated cluster and Azure Firewall?

A network isolated cluster doesn't require any egress traffic beyond the VNet throughout the cluster bootstrapping process. A network isolated cluster has outbound type as either `none`

or `block`

. If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

A firewall typically establishes a barrier between a trusted network and an untrusted network, such as the Internet. Azure Firewall, for example, can restrict outbound HTTP and HTTPS traffic that's based on the destination. It gives you fine-grained control of egress traffic, but at the same time allows you to provide access to the FQDNs encompassing an AKS cluster’s outbound dependencies. This is something that NSGs can't do. For example, you can set outbound type of the cluster to `userDefinedRouting`

to force outbound traffic through the firewall and then configure FQDN restrictions on outbound traffic. There are many cases where you still want a firewall. Such as you have outbound traffic anyway from your application or you want to control, inspect, and secure the cluster traffic both egress and ingress.

In summary, while Azure Firewall can be used to define egress restrictions on clusters with outbound requests, network isolated clusters go further on secure-by-default posture by eliminating or blocking the outbound requests altogether.

### Do I need to set up any allowlist endpoints for the network isolated cluster to work?

The cluster creation and bootstrapping stages don't require any outbound traffic from the network isolated cluster. Images required for AKS components and addons are pulled from the private ACR connected to the cluster instead of pulling from Microsoft Artifact Registry (MAR) over public endpoints.

After setting up a network isolated cluster. If you want to enable features or add-ons that need to make outbound requests to their service endpoints, you can set up private endpoints to the services powered by Azure Private Link.

### Can I manually upgrade packages to upgrade node pool image?

Manually upgrading packages based on egress to package repositories is not recommended. Instead, you can [manually upgrade](node-image-upgrade) or [autoupgrade your node OS images](auto-upgrade-node-os-image). Only `NodeImage`

and `None`

upgrade channels are currently supported for network isolated clusters.

### What if I change the outbound type other than `none`

or `block`

, does that still make a network isolated cluster?

The only supported outbound types for a network isolated cluster are outbound type `none`

and `block`

. If you use any other outbound type, the cluster may still pull artifacts from the private ACR associated, however that may generate egress traffic.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kms-data-encryption-concepts -->

# Data encryption at rest concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) stores sensitive data such as Kubernetes secrets in etcd, the distributed key-value store used by Kubernetes. For enhanced security and compliance requirements, AKS supports encryption of Kubernetes secrets at rest using the Kubernetes Key Management Service (KMS) provider integrated with Azure Key Vault.

This article explains the key concepts, encryption models, and key management options available for protecting Kubernetes secrets at rest in AKS.

## Understanding data encryption at rest

Data encryption at rest protects your data when it's stored on disk. Without encryption at rest, an attacker who gains access to the underlying storage could potentially read sensitive data like Kubernetes secrets.

AKS provides encryption for Kubernetes secrets stored in etcd:

| Layer | Description |
|---|---|
Azure platform encryption |
Azure Storage automatically encrypts all data at rest using 256-bit AES encryption. This encryption is always enabled and transparent to users. |
KMS provider encryption |
An optional layer that encrypts Kubernetes secrets before they're written to etcd using keys stored in Azure Key Vault. |

For more information about Azure's encryption at rest capabilities, see [Azure data encryption at rest](/en-us/azure/security/fundamentals/encryption-atrest) and [Azure encryption models](/en-us/azure/security/fundamentals/encryption-models).

## KMS provider for data encryption

The [Kubernetes KMS provider](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/) is a mechanism that enables encryption of Kubernetes secrets at rest using an external key management system. AKS integrates with Azure Key Vault to provide this capability, giving you control over encryption keys while maintaining the security benefits of a managed Kubernetes service.

### How KMS encryption works

When you enable KMS for an AKS cluster:

**Secret creation**: When a secret is created, the Kubernetes API server sends the secret data to the KMS provider plugin.**Encryption**: The KMS plugin encrypts the secret data using a Data Encryption Key (DEK), which is itself encrypted using a Key Encryption Key (KEK) stored in Azure Key Vault.**Storage**: The encrypted secret is stored in etcd.**Secret retrieval**: When a secret is read, the KMS plugin decrypts the DEK using the KEK from Azure Key Vault, then uses the DEK to decrypt the secret data.

This envelope encryption approach provides both security and performance benefits. The DEK handles frequent encryption operations locally while the KEK in Azure Key Vault provides the security of a hardware-backed key management system.

## Key management options

AKS offers two key management options for KMS encryption:

### Platform-managed keys (PMK)

With platform-managed keys, AKS automatically manages the encryption keys for you:

- AKS creates and manages the encryption keys.
- Key rotation is handled automatically by the platform.
- No additional configuration or key vault setup is required.

**When to use platform-managed keys:**

- You want the simplest setup with minimal configuration.
- You don't have specific regulatory requirements that mandate customer-managed keys.
- You want automatic key rotation without manual intervention.

### Customer-managed keys (CMK)

With customer-managed keys, you have full control over the encryption keys:

- You create and manage your own Azure Key Vault and encryption keys.
- You control key rotation schedules and policies.

**When to use customer-managed keys:**

- You have regulatory or compliance requirements that mandate customer-managed keys.
- You need to control the key lifecycle, including rotation schedules and key versions.
- You require audit logs for all key operations.

### Key vault network access options

When using customer-managed keys, you can configure the network access for your Azure Key Vault:

| Network access | Description | Use case |
|---|---|---|
Public |
Key vault is accessible over the public internet with authentication. | Development environments, simpler setup |
Private |
Key vault has public network access disabled. AKS accesses the key vault through the
|

## Comparing encryption key options

| Feature | Platform-managed keys | Customer-managed keys (Public) | Customer-managed keys (Private) |
|---|---|---|---|
Key ownership |
Microsoft manages | Customer manages | Customer manages |
Key rotation |
Automatic |
|

[User configurable](/en-us/azure/key-vault/keys/how-to-configure-key-rotation)**Key vault creation****Network isolation**## Requirements

- The new
[KMS encryption with platform-managed keys or customer-managed keys with automatic key rotation](kms-data-encryption)experience requires**Kubernetes version 1.33 or later**. - The new
[KMS encryption with platform-managed keys or customer-managed keys with automatic key rotation](kms-data-encryption)experience is only supported on AKS clusters where[managed identity is used for the cluster's identity](use-managed-identity).

## Limitations

**No downgrade**: After enabling the new KMS encryption experience, you can't disable the feature.**Key deletion**: Deleting the encryption key or key vault makes your secrets unrecoverable.**Private endpoint access**: Key vault access using[private link/endpoint](/en-us/azure/key-vault/general/private-link-service)isn't yet supported. For private key vaults, use the[trusted services firewall exception](/en-us/azure/key-vault/general/network-security#key-vault-firewall-enabled-trusted-services-only).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-workflow -->

# Deploy and run workflows with the Dapr extension for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Dapr Workflow, you can easily orchestrate messaging, state management, and failure-handling logic across various microservices. Dapr Workflow can help you create long-running, fault-tolerant, and stateful applications.

In this guide, you use the [provided order processing workflow example](https://github.com/Azure-Samples/dapr-workflows-aks-sample) to:

- Create an Azure Container Registry and an AKS cluster for this sample.
- Install the Dapr extension on your AKS cluster.
- Deploy the sample application to AKS.
- Start and query workflow instances using HTTP API calls.

The workflow example is an ASP.NET Core project with:

- A
that contains the setup of the app, including the registration of the workflow and workflow activities.`Program.cs`

file - Workflow definitions found in the
.`Workflows`

directory - Workflow activity definitions found in the
.`Activities`

directory

## Prerequisites

- An
[Azure subscription](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)with Owner or Admin role. [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)- The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli) - The latest version of
[Dapr](https://docs.dapr.io/getting-started/install-dapr-cli/) - Latest
[Docker](https://docs.docker.com/get-docker/) - Latest
[Helm](https://helm.sh/docs/intro/install/)

## Set up the environment

### Clone the sample project

Clone the example workflow application.

```
git clone https://github.com/Azure-Samples/dapr-workflows-aks-sample.git
```


Navigate to the sample's root directory.

```
cd dapr-workflows-aks-sample
```


### Create a Kubernetes cluster

Create a resource group to hold the AKS cluster.

```
az group create --name myResourceGroup --location eastus
```


Create an AKS cluster.

```
az aks create --resource-group myResourceGroup --name myAKSCluster --node-count 2 --generate-ssh-keys
```


[Make sure kubectl is installed and pointed to your AKS cluster.](tutorial-kubernetes-deploy-cluster#connect-to-cluster-using-kubectl) If you use the Azure Cloud Shell,

`kubectl`

is already installed.For more information, see the [Deploy an AKS cluster](tutorial-kubernetes-deploy-cluster) tutorial.

## Deploy the application to AKS

### Install Dapr on your AKS cluster

Install the Dapr extension on your AKS cluster. Before you start, make sure you have:

[Installed or updated the](dapr#add-the-azure-cli-extension-for-cluster-extensions).`k8s-extension`

[Registered the](dapr#register-the-kubernetesconfiguration-resource-provider)`Microsoft.KubernetesConfiguration`

service provider

```
az k8s-extension create --cluster-type managedClusters --cluster-name myAKSCluster --resource-group myResourceGroup --name dapr --extension-type Microsoft.Dapr
```


After a few minutes, you'll see output showing the Dapr connection to your AKS cluster. Next, initialize Dapr on your cluster.

```
dapr init -k
```


Verify Dapr is installed:

```
kubectl get pods -A
```


### Deploy the Redis Actor state store component

Navigate to the `Deploy`

directory in your forked version of the sample:

```
cd Deploy
```


Deploy the Redis component:

```
helm repo add bitnami https://charts.bitnami.com/bitnami
helm install redis bitnami/redis
kubectl apply -f redis.yaml
```


### Run the application

Once Redis is deployed, deploy the application to AKS:

```
kubectl apply -f deployment.yaml
```


Expose the Dapr sidecar and the sample app:

```
kubectl apply -f service.yaml
export APP_URL=$(kubectl get svc/workflows-sample -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export DAPR_URL=$(kubectl get svc/workflows-sample-dapr -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
```


Verify that the above commands were exported:

```
echo $APP_URL
echo $DAPR_URL
```


## Start the workflow

Now that the application and Dapr are deployed to the AKS cluster, you can now start and query workflow instances. Restock items in the inventory using the following API call to the sample app:

```
curl -X GET $APP_URL/stock/restock
```


Start the workflow:

```
curl -i -X POST $DAPR_URL/v1.0/workflows/dapr/OrderProcessingWorkflow/start \
-H "Content-Type: application/json" \
-H "dapr-app-id: dwf-app" \
-d '{"Name": "Paperclips", "TotalCost": 99.95, "Quantity": 1}'
```


Expected output includes an auto-generated instance ID:

```
HTTP/1.1 202 Accepted
Content-Type: application/json
Traceparent: 00-00000000000000000000000000000000-0000000000000000-00
Date: Tue, 23 Apr 2024 15:35:00 GMT
Content-Length: 21
{"instanceID":"<generated-id>"}
```


Check the workflow status:

```
curl -i -X GET $DAPR_URL/v1.0/workflows/dapr/OrderProcessingWorkflow/<instance-id> \
-H "dapr-app-id: dwf-app"
```


Expected output:

```
HTTP/1.1 200 OK
Content-Type: application/json
Traceparent: 00-00000000000000000000000000000000-0000000000000000-00
Date: Tue, 23 Apr 2024 15:51:02 GMT
Content-Length: 580
```


Monitor the application logs:

```
kubectl logs -l run=workflows-sample -c workflows-sample --tail=20
```


Expected output:

```
{
"instanceID":"1234",
"workflowName":"OrderProcessingWorkflow",
"createdAt":"2024-04-23T15:35:00.156714334Z",
"lastUpdatedAt":"2024-04-23T15:35:00.176459055Z",
"runtimeStatus":"COMPLETED",
"dapr.workflow.input":"{ \"input\" : {\"Name\": \"Paperclips\", \"TotalCost\": 99.95, \"Quantity\": 1}}",
"dapr.workflow.output":"{\"Processed\":true}"
}
```


Notice that the workflow status is marked as completed.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-metrics-server-vertical-pod-autoscaler -->

# Configure Metrics Server VPA in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Metrics Server](https://kubernetes-sigs.github.io/metrics-server/) is a scalable, efficient source of container resource metrics for Kubernetes built-in autoscaling pipelines. With Azure Kubernetes Service (AKS), vertical pod autoscaling is enabled for the Metrics Server. The Metrics Server is commonly used by other Kubernetes add-ons, like the [Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler).

Vertical Pod Autoscaler (VPA) enables you to adjust the resource limit when the Metrics Server is experiencing consistent CPU and memory resource constraints.

## Prerequisites

- An AKS cluster with Kubernetes version 1.24 or higher.
- The Kubernetes command-line tool
`kubectl`

installed on your computer or use Azure Cloud Shell to run`kubectl`

commands.

## Get credentials

To run the `kubectl`

commands, you need your AKS credentials merged into your profile's `.kube/config`

file. Replace `<resourceGroupName>`

and `<clusterName>`

with your cluster's values.

```
az aks get-credentials --resource-group <resourceGroupName> --name <clusterName>
```


## Metrics server throttling

If the Metrics Server throttling rate is high, and the memory usage of its two pods is unbalanced, it's an indication that the Metrics Server needs more resources than the default values.

To update the coefficient values, create a `ConfigMap`

in the overlay `kube-system`

namespace to override the values in the Metrics Server specification. Perform the following steps to update the metrics server.

Create a

`ConfigMap`

file named*metrics-server-config.yaml*and copy the manifest code into the file.`apiVersion: v1 kind: ConfigMap metadata: name: metrics-server-config namespace: kube-system labels: kubernetes.io/cluster-service: "true" addonmanager.kubernetes.io/mode: EnsureExists data: NannyConfiguration: |- apiVersion: nannyconfig/v1alpha1 kind: NannyConfiguration baseCPU: 100m cpuPerNode: 1m baseMemory: 100Mi memoryPerNode: 8Mi`

In the

`ConfigMap`

example, the resource limit and request are changed to the following values where`n`

is the number of nodes:- cpu: (100+1n) millicores
- memory: (100+8n) mebibytes

If you're using Cloud Shell, use

**Manage files**and select**Upload**so the file is available in your Bash session.Create the

`ConfigMap`

using the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest:`kubectl apply -f metrics-server-config.yaml`

Restart the two Metrics Server pods using

[kubectl rollout restart](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout). The following command deletes both pods and new pods are created.`kubectl rollout restart -n kube-system deployment metrics-server`

The new Metrics Server pods are created before the old pods are terminated so there isn't downtime.

List the pods using

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)to get the new Metrics Server pod names that are used in the next command.`kubectl get pods --namespace kube-system`

`NAME READY STATUS RESTARTS AGE metrics-server-1a2b333c44-wxyz5 2/2 Running 0 15s metrics-server-1a2b333c44-abcd6 2/2 Running 0 15s`

If you notice a third Metrics Server pod with a longer age value, it's because the termination occurs after the new pods are available.

To verify the updated resources took effect for each pod, run the following command to review the Metrics Server VPA log. Replace

`<metrics-server-pod-name>`

with the name of each of your metrics server pods.`kubectl -n kube-system logs <metrics-server-pod-name> -c metrics-server-vpa`

The following example output resembles the results showing the updated throttling settings were applied.

`I0811 19:08:34.930865 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server] I0811 19:08:34.931128 1 pod_nanny.go:87] Version: 1.8.23 I0811 19:08:34.931200 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server. I0811 19:08:34.931249 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi I0811 19:08:34.932085 1 pod_nanny.go:144] cpu: 100m, extra_cpu: 1m, memory: 100Mi, extra_memory: 8Mi I0811 19:08:34.932177 1 pod_nanny.go:278] Resources: [{Base:{i:{value:100 scale:-3} d:{Dec:<nil>} s:100m Format:DecimalSI} ExtraPerResource:{i:{value:1 scale:-3} d:{Dec:<nil>} s:1m Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:8388608 scale:0} d:{Dec:<nil>} s: Format:BinarySI} Name:memory}]`


Be cautious of the `baseCPU`

, `cpuPerNode`

, `baseMemory`

, and the `memoryPerNode`

, because AKS doesn't validate the `ConfigMap`

. As a recommended practice, increase the value gradually to avoid unnecessary resource consumption. Proactively monitor resource usage when updating or creating the `ConfigMap`

. A large number of resource requests could negatively affect the node.

## Manually configure Metrics Server resource usage

The Metrics Server VPA adjusts resource usage by the number of nodes. If the cluster scales up or down often, the Metrics Server might restart frequently. In this case, you can bypass VPA and manually control its resource usage. This method to configure VPA isn't to be performed in addition to the steps described in the previous section.

If you would like to bypass VPA for Metrics Server and manually control its resource usage, perform the following steps.

Create a

`ConfigMap`

file named*metrics-server-config.yaml*and copy in the following manifest.`apiVersion: v1 kind: ConfigMap metadata: name: metrics-server-config namespace: kube-system labels: kubernetes.io/cluster-service: "true" addonmanager.kubernetes.io/mode: EnsureExists data: NannyConfiguration: |- apiVersion: nannyconfig/v1alpha1 kind: NannyConfiguration baseCPU: 100m cpuPerNode: 0m baseMemory: 100Mi memoryPerNode: 0Mi`

In this

`ConfigMap`

example, the resource limit and request are changed to the following values that don't trigger autoscaling:- cpu: 100 millicores
- memory: 100 mebibytes

If you're using Cloud Shell, use

**Manage files**and select**Upload**so the file is available in your Bash session.Create the

`ConfigMap`

using the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest:`kubectl apply -f metrics-server-config.yaml`

Restart the two Metrics Server pods using

[kubectl rollout restart](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#rollout). The following command deletes both pods and new pods are created.`kubectl rollout restart -n kube-system deployment metrics-server`

The new Metrics Server pods are created before the old pods are terminated so there isn't downtime.

List the pods using

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)to get the new Metrics Server pod names that are used in the next command.`kubectl get pods --namespace kube-system`

`NAME READY STATUS RESTARTS AGE metrics-server-1a2b333c44-wxyz5 2/2 Running 0 15s metrics-server-1a2b333c44-abcd6 2/2 Running 0 15s`

If you notice a third Metrics Server pod with a longer age value, it's because the termination occurs after the new pods are available.

To verify the updated resources took effect for each pod, run the following command to review the Metrics Server VPA log. Replace

`<metrics-server-pod-name>`

with the name of each of your metrics server pods.`kubectl -n kube-system logs <metrics-server-pod-name> -c metrics-server-vpa`

The following example output resembles the results showing the updated throttling settings were applied.

`I0811 19:19:06.235018 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server] I0811 19:19:06.235105 1 pod_nanny.go:87] Version: 1.8.23 I0811 19:19:06.235136 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server. I0811 19:19:06.235171 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi I0811 19:19:06.235899 1 pod_nanny.go:144] cpu: 100m, extra_cpu: 0m, memory: 100Mi, extra_memory: 0Mi I0811 19:19:06.235917 1 pod_nanny.go:278] Resources: [{Base:{i:{value:100 scale:-3} d:{Dec:<nil>} s:100m Format:DecimalSI} ExtraPerResource:{i:{value:0 scale:-3} d:{Dec:<nil>} s: Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:0 scale:0} d:{Dec:<nil>} s: Format:BinarySI} Name:memory}]`


## Troubleshooting

### ConfigMap error

If you apply the following `ConfigMap`

, the Metrics Server VPA customizations aren't applied. You need add a unit for `baseCPU`

like `baseCPU: 100m`

that includes the `m`

unit.

```
apiVersion: v1
kind: ConfigMap
metadata:
name: metrics-server-config
namespace: kube-system
labels:
kubernetes.io/cluster-service: "true"
addonmanager.kubernetes.io/mode: EnsureExists
data:
NannyConfiguration: |-
apiVersion: nannyconfig/v1alpha1
kind: NannyConfiguration
baseCPU: 100
cpuPerNode: 1m
baseMemory: 100Mi
memoryPerNode: 8Mi
```


The following example output resembles the results showing the updated throttling settings aren't applied.

```
I0811 19:25:33.992691 1 pod_nanny.go:86] Invoked by [/pod_nanny --config-dir=/etc/config --cpu=150m --extra-cpu=0.5m --memory=100Mi --extra-memory=4Mi --poll-period=180000 --threshold=5 --deployment=metrics-server --container=metrics-server]
I0811 19:25:33.992890 1 pod_nanny.go:87] Version: 1.8.23
I0811 19:25:33.992918 1 pod_nanny.go:109] Watching namespace: kube-system, pod: <metrics-server-pod-name>, container: metrics-server.
I0811 19:25:33.992937 1 pod_nanny.go:110] storage: MISSING, extra_storage: 0Gi
I0811 19:25:33.993586 1 pod_nanny.go:217] Unable to decode Nanny Configuration from config map, using default parameters
I0811 19:25:33.993602 1 pod_nanny.go:144] cpu: 150m, extra_cpu: 0.5m, memory: 100Mi, extra_memory: 4Mi
I0811 19:25:33.993610 1 pod_nanny.go:278] Resources: [{Base:{i:{value:150 scale:-3} d:{Dec:<nil>} s:150m Format:DecimalSI} ExtraPerResource:{i:{value:5 scale:-4} d:{Dec:<nil>} s: Format:DecimalSI} Name:cpu} {Base:{i:{value:104857600 scale:0} d:{Dec:<nil>} s:100Mi Format:BinarySI} ExtraPerResource:{i:{value:4194304 scale:0} d:{Dec:<nil>} s:4Mi Format:BinarySI} Name:memory}]
```


### PodDisruptionBudget

For Kubernetes version 1.23 and higher clusters, Metrics Server has a `PodDisruptionBudget`

. It ensures the number of available Metrics Server pods is at least one. If you get something like this after running `kubectl get pods --namespace kube-system`

, it's possible that the customized resource usage is small. Increase the coefficient values to resolve it.

```
metrics-server-1a2b333c44-wxyz5 1/2 CrashLoopBackOff 6 (36s ago) 6m33s
metrics-server-1a2b333c44-abcd6 1/2 CrashLoopBackOff 6 (54s ago) 6m33s
metrics-server-5d69966543-hcrff 2/2 Running 0 37m
```


## Next steps

Metrics Server is a component in the core metrics pipeline. For more information, see [Metrics Server API design](https://kubernetes.io/docs/tasks/debug/debug-cluster/resource-metrics-pipeline/).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/release-tracker -->

# AKS release tracker

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS releases weekly rounds of fixes and feature and component updates that affect all clusters and customers. It's important for you to know when a particular AKS release is hitting your region, and the AKS release tracker provides these details in real time by versions and regions.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Overview

With AKS release tracker, you can follow specific component updates present in an AKS version release, such as fixes shipped to a core add-on, and node image updates for Azure Linux, Ubuntu, and Windows. The tracker provides links to the specific version of the AKS [release notes](https://github.com/Azure/AKS/releases) to help you identify relevant release instances. Real time data updates allow you to track the release order and status of each region.

## Use the release tracker

To view the release tracker, visit the [AKS release status webpage](https://releases.aks.azure.com/webpage/index.html).

### AKS releases

The top half of the tracker shows the current latest version and three previously available release versions for each region and links to the corresponding release notes entries. This view is helpful when you want to track the available versions by region.


The bottom half of the tracker shows the release order. The table has two views: *By Region* and *By Version*.


### AKS node image updates

The top half of the tracker shows the current latest node image version and three previously available node image versions for each region. This view is helpful when you want to track the available node image versions by region.


The bottom half of the tracker shows the node image update order. The table has two views: *By Region* and *By Version*.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/update-kms-key-vault -->

# Update the key vault mode for an Azure Kubernetes Service (AKS) cluster with Key Management Service (KMS) etcd encryption (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to update the key vault mode from public to private or private to public for an Azure Kubernetes Service (AKS) cluster with Key Management Service (KMS) etcd encryption.

## Prerequisites

- An AKS cluster with KMS etcd encryption enabled. For more information, see
[Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster](use-kms-etcd-encryption). - Azure CLI version 2.39.0 or later. Find your version using the
`az --version`

command. If you need to install or upgrade, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update a key vault mode

Note

To change a different key vault with a different mode (whether public or private), you can run [ az aks update](/en-us/cli/azure/aks#az-aks-update) directly. To change the mode of an attached key vault, you must first turn off KMS, then turn it on again using the new key vault IDs.

Turn off KMS on the existing cluster and release the key vault using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Warning

After you turn off KMS, the encryption key vault key is still needed. You can't delete or expire it.

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`

Update the key vault from public to private using the

command with the`az keyvault update`

`--public-network-access`

parameter set to`Disabled`

.`az keyvault update --name $KEY_VAULT --resource-group $RESOURCE_GROUP --public-network-access Disabled`

Turn on KMS with the updated private key vault using the

command with the`az aks update`

`--azure-keyvault-kms-key-vault-network-access`

parameter set to`Private`

.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-capacity-reservation-groups -->

# Assign capacity reservation groups to Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your workload demands change, you can associate existing [capacity reservation groups (CRGs)](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set) to your Azure Kubernetes Service (AKS) node pools to guarantee allocated capacity for them. Capacity reservation groups allow you to reserve compute capacity in an Azure region or availability zone for any duration of time. This feature is useful for workloads that require guaranteed capacity, such as those with predictable traffic patterns or those that need to meet specific performance requirements.

In this article, you learn how to use capacity reservation groups with node pools in AKS.

Note

Deleting a node pool implicitly dissociates that node pool from any associated capacity reservation group before the node pool is deleted. Deleting a cluster implicitly dissociates all node pools in that cluster from their associated capacity reservation groups.

## Prerequisites for using capacity reservation groups with AKS node pools

- You need the Azure CLI version 2.56 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need an existing
[capacity reservation group](/en-us/azure/virtual-machines/capacity-reservation-associate-virtual-machine-scale-set)with at least one capacity reservation. If not, the node pool is added to the cluster with a warning and no capacity reservation group gets associated. - You need to
[create a user-assigned managed identity with the](#create-a-user-assigned-managed-identity-and-assign-it-to-an-aks-cluster)for the resource group that contains the capacity reservation group and assign the identity to your AKS cluster. System-assigned managed identities don't work for this feature.`Contributor`

role

### Create a user-assigned managed identity and assign it to an AKS cluster

Create a user-assigned managed identity using the

command.`az identity create`

`az identity create --name <identity-name> --resource-group <resource-group-name> --location <location>`

Get the ID of the user-assigned managed identity using the

command and set it to an environment variable.`az identity show`

`IDENTITY_ID=$(az identity show --name <identity-name> --resource-group <resource-group-name> --query identity.id -o tsv)`

Assign the

`Contributor`

role to the user-assigned identity using thecommand.`az role assignment create`

`az role assignment create --assignee $IDENTITY_ID --role "Contributor" --scope /subscriptions/<subscription-id>/resourceGroups/<resource-group-name>`

It can take up to

*60 minutes*for the role assignment to propagate.Assign the user-assigned managed identity to a new or existing AKS cluster using the

`--assign-identity`

flag with theor`az aks create`

command.`az aks update`

`# Create a new AKS cluster with the user-assigned managed identity az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --generate-ssh-keys # Update an existing AKS cluster to use the user-assigned managed identity az aks update \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> \ --node-count <node-count> \ --enable-managed-identity \ --assign-identity $IDENTITY_ID`


## Limitations for using capacity reservation groups with AKS node pools

You can't update an existing node pool with a capacity reservation group. Instead, you need to create a new node pool with the `--crg-id`

flag to associate it with the capacity reservation group. You can also associate an existing capacity reservation group with a system node pool during cluster creation.

## Get the ID of an existing capacity reservation group

Get the ID of an existing capacity reservation group using the

command and set it to an environment variable.`az capacity reservation group show`

`CRG_ID=$(az capacity reservation group show --capacity-reservation-group <crg-name> --resource-group <resource-group-name> --query id -o tsv)`


## Associate an existing capacity reservation group with a node pool

Associate an existing capacity reservation group with a node pool using the

command with the`az aks nodepool add`

`--crg-id`

flag. The following example assumes you have a CRG named "myCRG".`az aks nodepool add --resource-group <resource-group-name> --cluster-name <cluster-name> --name <node-pool-name> --crg-id $CRG_ID`


## Associate an existing capacity reservation group with a system node pool

To associate an existing capacity reservation group with a system node pool, you need to assign the user-assigned managed identity with the `Contributor`

role to the cluster during cluster creation. You can then use the `--crg-id`

flag to associate the capacity reservation group with the system node pool.

Create a new AKS cluster with the user-assigned managed identity and associate it with the capacity reservation group using the

`--assign-identity`

and`--crg-id`

flags with thecommand.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --location <location> \ --node-vm-size <vm-size> --node-count <node-count> \ --assign-identity $IDENTITY_ID \ --crg-id $CRG_ID \ --generate-ssh-keys`


## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-performance-scale -->

# Best practices for performance and scaling for small to medium workloads in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

This article focuses on general best practices for **small to medium workloads**. For best practices specific to **large workloads**, see [Performance and scaling best practices for large workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale-large).

As you deploy and maintain clusters in AKS, you can use the following best practices to help you optimize performance and scaling.

In this article, you learn about:

- Tradeoffs and recommendations for autoscaling your workloads.
- Managing node scaling and efficiency based on your workload demands.
- Networking considerations for ingress and egress traffic.
- Monitoring and troubleshooting control plane and node performance.
- Capacity planning, surge scenarios, and cluster upgrades.
- Storage and networking considerations for data plane performance.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Application autoscaling vs. infrastructure autoscaling

### Application autoscaling

Application autoscaling is useful when dealing with cost optimization or infrastructure limitations. A well-configured autoscaler maintains high availability for your application while also minimizing costs. You only pay for the resources required to maintain availability, regardless of the demand.

For example, if an existing node has space but not enough IPs in the subnet, it might be able to skip the creation of a new node and instead immediately start running the application on a new pod.

#### Horizontal Pod autoscaling

Implementing [horizontal pod autoscaling](concepts-scale#horizontal-pod-autoscaler) is useful for applications with a steady and predictable resource demand. The Horizontal Pod Autoscaler (HPA) dynamically scales the number of pod replicas, which effectively distributes the load across multiple pods and nodes. This scaling mechanism is typically most beneficial for applications that can be decomposed into smaller, independent components capable of running in parallel.

The HPA provides resource utilization metrics by default. You can also integrate custom metrics or leverage tools like the [Kubernetes Event-Driven Autoscaler (KEDA) (Preview)](keda-about). These extensions allow the HPA to make scaling decisions based on multiple perspectives and criteria, providing a more holistic view of your application's performance. This is especially helpful for applications with varying complex scaling requirements.

Note

If maintaining high availability for your application is a top priority, we recommend leaving a slightly higher buffer for the minimum pod number for your HPA to account for scaling time.

#### Vertical Pod autoscaling

Implementing [vertical pod autoscaling](vertical-pod-autoscaler) is useful for applications with fluctuating and unpredictable resource demands. The Vertical Pod Autoscaler (VPA) allows you to fine-tune resource requests, including CPU and memory, for individual pods, enabling precise control over resource allocation. This granularity minimizes resource waste and enhances the overall efficiency of cluster utilization. The VPA also streamlines application management by automating resource allocation, freeing up resources for critical tasks.

Warning

You shouldn't use the VPA in conjunction with the HPA on the same CPU or memory metrics. This combination can lead to conflicts, as both autoscalers attempt to respond to changes in demand using the same metrics. However, you can use the VPA for CPU or memory in conjunction with the HPA for custom metrics to prevent overlap and ensure that each autoscaler focuses on distinct aspects of workload scaling.

Note

The VPA works based on historical data. We recommend waiting at least *24 hours* after deploying the VPA before applying any changes to give it time to collect recommendation data.

### Infrastructure autoscaling

#### Cluster autoscaling

Implementing cluster autoscaling is useful if your existing nodes lack sufficient capacity, as it helps with scaling up and provisioning new nodes.

When considering cluster autoscaling, the decision of when to remove a node involves a tradeoff between optimizing resource utilization and ensuring resource availability. Eliminating underutilized nodes enhances cluster utilization but might result in new workloads having to wait for resources to be provisioned before they can be deployed. It's important to find a balance between these two factors that aligns with your cluster and workload requirements and [configure the cluster autoscaler profile settings accordingly](cluster-autoscaler#update-the-cluster-autoscaler-settings).

The Cluster Autoscaler profile settings apply universally to all autoscaler-enabled node pools in your cluster. This means that any scaling actions occurring in one autoscaler-enabled node pool might impact the autoscaling behavior in another node pool. It's important to apply consistent and synchronized profile settings across all relevant node pools to ensure that the autoscaler behaves as expected.

##### Overprovisioning

Overprovisioning is a strategy that helps mitigate the risk of application pressure by ensuring there's an excess of readily available resources. This approach is especially useful for applications that experience highly variable loads and cluster scaling patterns that show frequent scale ups and scale downs.

To determine the optimal amount of overprovisioning, you can use the following formula:

```
1-buffer/1+traffic
```


For example, let's say you want to avoid hitting 100% CPU utilization in your cluster. You might opt for a 30% buffer to maintain a safety margin. If you anticipate an average traffic growth rate of 40%, you might consider overprovisioning by 50%, as calculated by the formula:

```
1-30%/1+40%=50%
```


An effective overprovisioning method involves the use of *pause pods*. Pause pods are low-priority deployments that can be easily replaced by high-priority deployments. You create low priority pods that serve the sole purpose of reserving buffer space. When a high-priority pod requires space, the pause pods are removed and rescheduled on another node or a new node to accommodate the high priority pod.

The following YAML shows an example pause pod manifest:

```
apiVersion: scheduling.k8s.io/v1
kind: PriorityClass
metadata:
name: overprovisioning
value: -1
globalDefault: false
description: "Priority class used by overprovisioning."
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: overprovisioning
namespace: kube-system
spec:
replicas: 1
selector:
matchLabels:
run: overprovisioning
template:
metadata:
labels:
run: overprovisioning
spec:
priorityClassName: overprovisioning
containers:
- name: reserve-resources
image: your-custome-pause-image
resources:
requests:
cpu: 1
memory: 4Gi
```


## Node scaling and efficiency


Best practice guidance:Carefully monitor resource utilization and scheduling policies to ensure nodes are being used efficiently.


Node scaling allows you to dynamically adjust the number of nodes in your cluster based on workload demands. It's important to understand that adding more nodes to a cluster isn't always the best solution for improving performance. To ensure optimal performance, you should carefully monitor resource utilization and scheduling policies to ensure nodes are being used efficiently.

### Node images


Best practice guidance:Use the latest node image version to ensure that you have the latest security patches and bug fixes.


Using the latest node image version provides the best performance experience. AKS ships performance improvements within the weekly image releases. The latest daemonset images are cached on the latest VHD image, which provide lower latency benefits for node provisioning and bootstrapping. Falling behind on updates might have a negative impact on performance, so it's important to avoid large gaps between versions.

#### Azure Linux

The [Azure Linux Container Host on AKS](/en-us/azure/azure-linux/intro-azure-linux) uses a native AKS image and provides a single place for Linux development. Every package is built from source and validated, ensuring your services run on proven components.

Azure Linux is lightweight, only including the necessary set of packages to run container workloads. It provides a reduced attack surface and eliminates patching and maintenance of unnecessary packages. At its base layer, it has a Microsoft-hardened kernel tuned for Azure. This image is ideal for performance-sensitive workloads and platform engineers or operators that manage fleets of AKS clusters.

#### Ubuntu 2204

The [Ubuntu 2204 image](https://github.com/Azure/AKS/blob/master/CHANGELOG.md) is the default node image for AKS. It's a lightweight and efficient operating system optimized for running containerized workloads. This means that it can help reduce resource usage and improve overall performance. The image includes the latest security patches and updates, which help ensure that your workloads are protected from vulnerabilities.

The Ubuntu 2204 image is fully supported by Microsoft, Canonical, and the Ubuntu community and can help you achieve better performance and security for your containerized workloads.

### Virtual machines (VMs)


Best practice guidance:When selecting a VM, ensure the size and performance of the OS disk and VM SKU don't have a large discrepancy. A discrepancy in size or performance can cause performance issues and resource contention.


Application performance is closely tied to the VM SKUs you use in your workloads. Larger and more powerful VMs, generally provide better performance. For *mission critical or product workloads*, we recommend using VMs with at least an 8-core CPU. VMs with newer hardware generations, like v4 and v5, can also help improve performance. Keep in mind that create and scale latency might vary depending on the VM SKUs you use.

### Use dedicated system node pools

For scaling performance and reliability, we recommend using a dedicated system node pool. With this configuration, the dedicated system node pool reserves space for critical system resources such as system OS daemons. Your application workload can then run in a user node pool to increase the availability of allocatable resources for your application. This configuration also helps mitigate the risk of resource competition between the system and application.

### Create operations

Review the extensions and add-ons you have enabled during create provisioning. Extensions and add-ons can add latency to overall duration of create operations. If you don't need an extension or add-on, we recommend removing it to improve create latency.

You can also use availability zones to provide a higher level of availability to protect against potential hardware failures or planned maintenance events. AKS clusters distribute resources across logical sections of underlying Azure infrastructure. Availability zones physically separate nodes from other nodes to help ensure that a single failure doesn't impact the availability of your application. Availability zones are only available in certain regions. For more information, see [Availability zones in Azure](/en-us/azure/reliability/availability-zones-overview).

## Kubernetes API server

### LIST and WATCH operations

Kubernetes uses the LIST and WATCH operations to interact with the Kubernetes API server and monitor information about cluster resources. These operations are fundamental to how Kubernetes performs resource management.

**The LIST operation retrieves a list of resources that fit within certain criteria**, such as all pods in a specific namespace or all services in the cluster. This operation is useful when you want to get an overview of your cluster resources or you need to operator on multiple resources at once.

The LIST operation can retrieve large amounts of data, especially in large clusters with multiple resources. Be mindful of the fact that making unbounded or frequent LIST calls puts a significant load on the API server and can close down response times.

**The WATCH operation performs real-time resource monitoring**. When you set up a WATCH on a resource, the API server sends you updates whenever there are changes to that resource. This is important for controllers, like the ReplicaSet controller, which rely on WATCH to maintain the desired state of resources.

Be mindful of the fact that watching too many mutable resources or making too many concurrent WATCH requests can overwhelm the API server and cause excessive resource consumption.

To avoid potential issues and ensure the stability of the Kubernetes control plane, you can use the following strategies:

**Resource quotas**

Implement resource quotas to limit the number of resources that can be listed or watched by a particular user or namespace to prevent excessive calls.

**API Priority and Fairness**

Kubernetes introduced the concept of API Priority and Fairness (APF) to prioritize and manage API requests. You can use APF in Kubernetes to protect the cluster's API server and reduce the number of `HTTP 429 Too Many Requests`

responses seen by client applications.

| Custom resource | Key features |
|---|---|
| PriorityLevelConfigurations | * Define different priority levels for API requests. * Specifies a unique name and assigns an integer value representing the priority level. Higher priority levels have lower integer values, indicating they're more critical. * Can use multiple to categorize requests into different priority levels based on their importance. * Allow you to specify whether requests at a particular priority level should be subject to rate limits. |
| FlowSchemas | * Define how API requests should be routed to different priority levels based on request attributes. * Specify rules that match requests based on criteria like API groups, versions, and resources. * When a request matches a given rule, the request is directed to the priority level specified in the associated PriorityLevelConfiguration. * Can use to set the order of evaluation when multiple FlowSchemas match a request to ensure that certain rules take precedence. |

Configuring API with PriorityLevelConfigurations and FlowSchemas enables the prioritization of critical API requests over less important requests. This ensures that essential operations don't starve or experience delays because of lower priority requests.

**Optimize labeling and selectors**

When using LIST operations, optimize label selectors to narrow down the scope of the resources you want to query to reduce the amount of data returned and the load on the API server.

In Kubernetes CREATE and UPDATE operations refer to actions that manage and modify cluster resources.

### CREATE and UPDATE operations

**The CREATE operation creates new resources in the Kubernetes cluster**, such as pods, services, deployments, configmaps, and secrets. During a CREATE operation, a client, such as `kubectl`

or a controller, sends a request to the Kubernetes API server to create the new resource. The API server validates the request, ensures compliance with any admission controller policies, and then creates the resource in the cluster's desired state.

**The UPDATE operation modifies existing resources in the Kubernetes cluster**, including changes to resources specifications, like number of replicas, container images, environment variables, or labels. During an UPDATE operation, a client sends a request to the API server to update an existing resource. The API server validates the request, applies the changes to the resource definition, and updates the cluster resource.

CREATE and UPDATE operations can impact the performance of the Kubernetes API server under the following conditions:

**High concurrency**: When multiple users or applications make concurrent CREATE or UPDATE requests, it can lead to a surge in API requests arriving at the server at the same time. This can stress the API server's processing capacity and cause performance issues.**Complex resource definitions**: Resource definitions that are overly complex or involve multiple nested objects can increase the time it takes for the API server to validate and process CREATE and UPDATE requests, which can lead to performance degradation.**Resource validation and admission control**: Kubernetes enforces various admission control policies and validation checks on incoming CREATE and UPDATE requests. Large resource definitions, like ones with extensive annotations or configurations, might require more processing time.**Custom controllers**: Custom controllers that watch for changes in resources, like Deployments or StatefulSet controllers, can generate a significant number of updates when scaling or rolling out changes. These updates can strain the API server's resources.

For more information, see [Troubleshoot API server and etcd problems in AKS](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-apiserver-etcd).

## Data plane performance

The Kubernetes data plane is responsible for managing network traffic between containers and services. Issues with the data plane can lead to slow response times, degraded performance, and application downtime. It's important to carefully monitor and optimize data plane configurations, such as network latency, resource allocation, container density, and network policies, to ensure your containerized applications run smoothly and efficiently.

### Storage types

AKS recommends and defaults to using ephemeral OS disks. Ephemeral OS disks are created on local VM storage and aren't saved to remote Azure storage like managed OS disks. They have faster reimaging and boot times, enabling faster cluster operations, and they provide lower read/write latency on the OS disk of AKS agent nodes. Ephemeral OS disks work well for stateless workloads, where applications are tolerant of individual VM failures but not of VM deployment time or individual VM reimaging instances. Only certain VM SKUs support ephemeral OS disks, so you need to ensure that your desired SKU generation and size is compatible. For more information, see [Ephemeral OS disks in Azure Kubernetes Service (AKS)](cluster-configuration#use-ephemeral-os-on-new-clusters).

If your workload is unable to use ephemeral OS disks, AKS defaults to using Premium SSD OS disks. If Premium SSD OS disks aren't compatible with your workload, AKS defaults to Standard SSD disks. Currently, the only other available OS disk type is Standard HDD. For more information, see [Storage options in Azure Kubernetes Service (AKS)](concepts-storage).

The following table provides a breakdown of suggested use cases for OS disks supported in AKS:

| OS disk type | Key features | Suggested use cases |
|---|---|---|
| Ephemeral OS disks | * Faster reimaging and boot times. * Lower read/write latency on OS disk of AKS agent nodes. * High performance and availability. |
* Demanding enterprise workloads, such as SQL Server, Oracle, Dynamics, Exchange Server, MySQL, Cassandra, MongoDB, SAP Business Suite, etc. * Stateless production workloads that require high availability and low latency. |
| Premium SSD OS disks | * Consistent performance and low latency. * High availability. |
* Demanding enterprise workloads, such as SQL Server, Oracle, Dynamics, Exchange Server, MySQL, Cassandra, MongoDB, SAP Business Suite, etc. * Input/output (IO) intensive enterprise workloads. |
| Standard SSD OS disks | * Consistent performance. * Better availability and latency compared to Standard HDD disks. |
* Web servers. * Low input/output operations per second (IOPS) application servers. * Lightly used enterprise applications. * Dev/test workloads. |
| Standard HDD disks | * Low cost. * Exhibits variability in performance and latency. |
* Backup storage. * Mass storage with infrequent access. |

#### IOPS and throughput

Input/output operations per second (IOPS) refers to the number of read and write operations that a disk can perform in a second. Throughput refers to the amount of data that can be transferred in a given time period.

OS disks are responsible for storing the operating system and its associated files, and the VMs are responsible for running the applications. When selecting a VM, ensure the size and performance of the OS disk and VM SKU don't have a large discrepancy. A discrepancy in size or performance can cause performance issues and resource contention. For example, if the OS disk is significantly smaller than the VMs, it can limit the amount of space available for application data and cause the system to run out of disk space. If the OS disk has lower performance than the VMs, it can become a bottleneck and limit the overall performance of the system. Make sure the size and performance are balanced to ensure optimal performance in Kubernetes.

You can use the following steps to monitor IOPS and bandwidth meters on OS disks in the Azure portal:

- Navigate to the
[Azure portal](https://portal.azure.com/). - Search for
**Virtual machine scale sets**and select your virtual machine scale set. - Under
**Monitoring**, select**Metrics**.

Ephemeral OS disks can provide dynamic IOPS and throughput for your application, whereas managed disks have capped IOPS and throughput. For more information, see [Ephemeral OS disks for Azure VMs](/en-us/azure/virtual-machines/ephemeral-os-disks).

[Azure Premium SSD v2](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) is designed for IO-intense enterprise workloads that require sub-millisecond disk latencies and high IOPS and throughput at a low cost. It's suited for a broad range of workloads, such as SQL server, Oracle, MariaDB, SAP, Cassandra, MongoDB, big data/analytics, gaming, and more. This disk type is the highest performing option currently available for persistent volumes.

### Pod scheduling

The memory and CPU resources allocated to a VM have a direct impact on the performance of the pods running on the VM. When a pod is created, it's assigned a certain amount of memory and CPU resources, which are used to run the application. If the VM doesn't have enough memory or CPU resources available, it can cause the pods to slow down or even crash. If the VM has too much memory or CPU resources available, it can cause the pods to run inefficiently, wasting resources and increasing costs. We recommend monitoring the total pod requests across your workloads against the total allocatable resources for best scheduling predictability and performance. You can also set the maximum pods per node based on your capacity planning using `--max-pods`

.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-ingress -->

# Deploy ingress gateways for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy external or internal ingresses for the Istio service mesh add-on for Azure Kubernetes Service (AKS) cluster.

Note

When you perform a [minor revision upgrade](istio-upgrade#minor-revision-upgrades-with-ingress-and-egress-gateways) of the Istio add-on, another deployment for the external / internal gateways will be created for the new control plane revision.

## Prerequisites

This guide assumes you followed the [documentation](istio-deploy-addon) to enable the Istio add-on on an AKS cluster, deploy a sample application, and set environment variables.

## Enable external ingress gateway

Note

If you need the ingress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

Use `az aks mesh enable-ingress-gateway`

to enable an externally accessible Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type external
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-external -n aks-istio-ingress
```


Observe from the output that the external IP address of the service is a publicly accessible one:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-external LoadBalancer 10.0.10.249 <EXTERNAL_IP> 15021:30705/TCP,80:32444/TCP,443:31728/TCP 4m21s
```


Applications aren't accessible from outside the cluster by default after enabling the ingress gateway. To make an application accessible, map the sample deployment's ingress to the Istio ingress gateway using the following manifest:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-gateway-external
spec:
selector:
istio: aks-istio-ingressgateway-external
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-external
spec:
hosts:
- "*"
gateways:
- bookinfo-gateway-external
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-external`

, which can be found as label on the service mapped to the external ingress that was enabled earlier.

Set environment variables for external ingress host and ports:

```
export INGRESS_HOST_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_EXTERNAL=$INGRESS_HOST_EXTERNAL:$INGRESS_PORT_EXTERNAL
```


Retrieve the external address of the sample application:

```
echo "http://$GATEWAY_URL_EXTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is displayed. Alternatively, you can also use `curl`

to confirm the sample application is accessible. For example:

```
curl -s "http://${GATEWAY_URL_EXTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Enable internal ingress gateway

Use `az aks mesh enable-ingress-gateway`

to enable an internal Istio ingress on your AKS cluster:

```
az aks mesh enable-ingress-gateway --resource-group $RESOURCE_GROUP --name $CLUSTER --ingress-gateway-type internal
```


Use `kubectl get svc`

to check the service mapped to the ingress gateway:

```
kubectl get svc aks-istio-ingressgateway-internal -n aks-istio-ingress
```


Observe from the output that the external IP address of the service isn't a publicly accessible one and is instead only locally accessible:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
aks-istio-ingressgateway-internal LoadBalancer 10.0.182.240 <IP> 15021:30764/TCP,80:32186/TCP,443:31713/TCP 87s
```


After enabling the ingress gateway, applications need to be exposed through the gateway, and routing rules need to be configured accordingly. Use the following manifest to map the sample deployment's ingress to the Istio ingress gateway:

```
kubectl apply -f - <<EOF
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-internal-gateway
spec:
selector:
istio: aks-istio-ingressgateway-internal
servers:
- port:
number: 80
name: http
protocol: HTTP
hosts:
- "*"
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: bookinfo-vs-internal
spec:
hosts:
- "*"
gateways:
- bookinfo-internal-gateway
http:
- match:
- uri:
exact: /productpage
- uri:
prefix: /static
- uri:
exact: /login
- uri:
exact: /logout
- uri:
prefix: /api/v1/products
route:
- destination:
host: productpage
port:
number: 9080
EOF
```


Note

The selector used in the Gateway object points to `istio: aks-istio-ingressgateway-internal`

, which can be found as label on the service mapped to the internal ingress that was enabled earlier.

Set environment variables for internal ingress host and ports:

```
export INGRESS_HOST_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export INGRESS_PORT_INTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-internal -o jsonpath='{.spec.ports[?(@.name=="http2")].port}')
export GATEWAY_URL_INTERNAL=$INGRESS_HOST_INTERNAL:$INGRESS_PORT_INTERNAL
```


Retrieve the address of the sample application:

```
echo "http://$GATEWAY_URL_INTERNAL/productpage"
```


Navigate to the URL from the output of the previous command and confirm that the sample application's product page is **NOT** displayed. Alternatively, you can also use `curl`

to confirm the sample application is **NOT** accessible. For example:

```
curl -s "http://${GATEWAY_URL_INTERNAL}/productpage" | grep -o "<title>.*</title>"
```


Use `kubectl exec`

to confirm application is accessible from inside the cluster's virtual network:

```
kubectl exec "$(kubectl get pod -l app=ratings -o jsonpath='{.items[0].metadata.name}')" -c ratings -- curl -sS "http://$GATEWAY_URL_INTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


## Ingress gateway service customizations

### Annotations

The following annotations can be added to the Kubernetes service for the external and internal ingress gateways. See the [document on configuring public load balancers](configure-load-balancer-standard#customizations-via-kubernetes-annotations) for more information about these annotations.

`external-dns.alpha.kubernetes.io/hostname`

: for specifying the domain for resource's DNS records. For more information, see[external-dns](https://kubernetes-sigs.github.io/external-dns/latest/docs/annotations/annotations/#external-dnsalphakubernetesiohostname).`service.beta.kubernetes.io/azure-allowed-ip-ranges`

: for specifying a list of allowed IP ranges separated by commas.`service.beta.kubernetes.io/azure-allowed-service-tags`

: for specifying which[service tags](/en-us/azure/virtual-network/service-tags-overview)the ingress gateway can receive requests from.`service.beta.kubernetes.io/azure-disable-load-balancer-floating-ip`

: set to`true`

to disable floating IP address in load balancer rule.`service.beta.kubernetes.io/azure-load-balancer-internal-subnet`

: name of subnet to bind internal ingress gateway to. This subnet must exist in the same virtual network as the mesh.`service.beta.kubernetes.io/azure-load-balancer-ipv4`

: for configuring a static IPv4 address.`service.beta.kubernetes.io/azure-load-balancer-disable-tcp-reset`

: for controlling whether Azure Load Balancer enables TCP Reset.`service.beta.kubernetes.io/azure-load-balancer-resource-group`

: for specifying the resource group of a public IP in a different resource group from the cluster.`service.beta.kubernetes.io/azure-load-balancer-tcp-idle-timeout`

: for configuring the TCP idle timeout in minutes for connections through the Azure Load Balancer.`service.beta.kubernetes.io/azure-pip-ip-tags`

: for specifying a list of IpTags separated by commas.`service.beta.kubernetes.io/azure-pip-name`

: for specifying the name of a public IP address.`service.beta.kubernetes.io/azure-shared-securityrule`

: for exposing the ingress gateway through an[augmented security rule](/en-us/azure/virtual-network/network-security-groups-overview#augmented-security-rules).

The add-on supports the following health probe annotations for ports `80`

and `443`

:

`service.beta.kubernetes.io/port_{port}_no_lb_rule`

`service.beta.kubernetes.io/port_{port}_no_probe_rule`

`service.beta.kubernetes.io/port_{port}_health-probe_protocol`

`service.beta.kubernetes.io/port_{port}_health-probe_port`

`service.beta.kubernetes.io/port_{port}_health-probe_interval`

`service.beta.kubernetes.io/port_{port}_health-probe_num-of-probe`

`service.beta.kubernetes.io/port_{port}_health-probe_request-path`


### External traffic policy

The add-on supports customization of `.spec.externalTrafficPolicy`

in the Kubernetes service for the ingress gateway. Setting `.spec.externalTrafficPolicy`

to `Local`

preserves the client source IP at the Istio ingress gateway and avoids a second hop in the traffic path to the backend ingress gateway pods.

```
kubectl patch service aks-istio-ingressgateway-external -n aks-istio-ingress --type merge --patch '{"spec": {"externalTrafficPolicy": "Local"}}'
```


Note

Modifying the `.spec.externalTrafficPolicy`

to `Local`

risks potentially imbalanced traffic spreading. Before applying this change, it is recommended to read the [Kubernetes docs](https://kubernetes.io/docs/tasks/access-application-cluster/create-external-load-balancer/#preserving-the-client-source-ip) to understand the tradeoffs between the different `externalTrafficPolicy`

settings.

## Delete resources

If you want to clean up the Istio external or internal ingress gateways, but leave the mesh enabled on the cluster, run the following command:

```
az aks mesh disable-ingress-gateway --ingress-gateway-type <external/internal> --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```


## Next steps

Note

If there are any issues encountered with deploying the Istio ingress gateway or configuring ingress traffic routing, refer to [article on troubleshooting Istio add-on ingress gateways](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-ingress-gateway)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-marketplace -->

# Deploy and manage a Kubernetes application from Azure Marketplace

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy and manage a Kubernetes application from Azure Marketplace.

[Azure Marketplace](/en-us/marketplace/azure-marketplace-overview) is an online store that contains thousands of IT software applications and services built by industry-leading technology companies. In Azure Marketplace, you can find, try, buy, and deploy the software and services that you need to build new solutions and manage your cloud infrastructure. The catalog includes solutions for different industries and technical areas, free trials, and consulting services from Microsoft partners.

## Limitations

- This feature is currently supported only in the following regions:
- Australia East, Australia Southeast, Brazil South, Canada Central, Canada East, Central India, Central US, East Asia, East US, East US 2, East US 2 EAUP, France Central, France South, Germany North, Germany West Central, Japan East, Japan West, Jio India West, Korea Central, Korea South, North Central Us, North Europe, Norway East, Norway West, South Africa North, South Central US, South India, Southeast Asia, Sweden Central, Switzerland North, UAE North, UK South, UK West, West Central US, West Europe, West US, West US 2, West US 3

- You can't deploy Kubernetes application-based container offers on AKS for Azure Stack HCI or AKS Edge Essentials.

## Select and deploy a Kubernetes application

### From an AKS cluster

In the Azure portal, navigate to your AKS cluster resource.

From the service menu, under

**Settings**, select**Extensions + applications**>**Add**.You can search for an offer or publisher directly by name, or you can browse all offers. To view Kubernetes application offers, select

**Containers**under**Categories**.After you decide on an application, select the offer. The following example uses the

**TrilioVault for Kubernetes - BYOL**offer.Select

**Plans + Pricing**to ensure the terms are acceptable, and then select**Create**.Follow each page in the application creation process, filling in information for your resource group, your cluster, and any configuration options that the application requires. You can decide to deploy on a new AKS cluster or use an existing cluster.

Once you've filled in all the required information, select

**Review + create**>**Create**.It might take a few minutes for the application to deploy. You can monitor the deployment status from the

**Extensions + applications**page.

### Search in the Azure portal

From the Azure portal home page, search for and select

**Marketplace**.You can search for an offer or publisher directly by name, or you can browse all offers. To find Kubernetes application offers, on the left side under

**Categories**select**Containers**.After you decide on an application, select the offer. The following example uses the

**TrilioVault for Kubernetes - BYOL**offer.Select

**Plans + Pricing**to ensure the terms are acceptable, and then select**Create**.Follow each page in the application creation process, filling in information for your resource group, your cluster, and any configuration options that the application requires. You can decide to deploy on a new AKS cluster or use an existing cluster.

Once you've filled in all the required information, select

**Review + create**>**Create**.It might take a few minutes for the application to deploy. You can monitor the deployment status from the

**Extensions + applications**page.

## Verify the deployment

- Navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Verify that the extension is listed and the
*Provisioning State*shows**Succeeded**.

## Manage the offer lifecycle

For lifecycle management, a Kubernetes offer is represented as a cluster extension for AKS. For more information, see [Cluster extensions for AKS](cluster-extensions). Purchasing an offer from Azure Marketplace creates a new instance of the extension on your AKS cluster.

- In the Azure portal, navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Select an extension name to navigate to a properties view where you're able to disable autoupgrades, check the provisioning state, delete the extension instance, or modify configuration settings as needed.

## Monitor billing and usage information

- In the Azure portal, navigate to your cluster's resource group.
- From the service menu, under
**Cost Management**, select**Cost analysis**. Under**Product**, you can see a cost breakdown for the plan that you selected.

## Remove an offer

You can delete a purchased plan for an Azure container offer by deleting the extension instance on the cluster.

- Navigate to the cluster where you recently installed the application.
- From the service menu, under
**Settings**, select**Extensions + applications**. - Select an application, then select
**Uninstall**.

## Troubleshooting

If you experience issues, see the [troubleshooting checklist for failed deployments of a Kubernetes offer](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-failed-kubernetes-deployment-offer).

## Next steps

- Learn more about
[exploring and analyzing costs](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis). - Learn more about
[deploying a Kubernetes application programmatically using Azure CLI](/en-us/azure/aks/deploy-application-az-cli). - Learn more about
[deploying a Kubernetes application using an ARM template](/en-us/azure/aks/deploy-application-template).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quickstart-event-grid -->

# Quickstart: Subscribe to Azure Kubernetes Service (AKS) events with Azure Event Grid

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Event Grid is a fully managed event routing service that provides uniform event consumption using a publish-subscribe model.

In this quickstart, you create an AKS cluster and subscribe to AKS events.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.

Note

AKS operations are independent of Azure Event Grid availability and aren't impacted during Event Grid [Service Outages](https://azure.status.microsoft/status).

## Create an AKS cluster

Create an AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a resource group *MyResourceGroup* and a cluster named *MyAKS* with one node in the *MyResourceGroup* resource group:

```
az group create --name MyResourceGroup --location eastus
az aks create --resource-group yResourceGroup --name MyAKS --location eastus --node-count 1 --generate-ssh-keys
```


## Subscribe to AKS events

Create a namespace and event hub using [az eventhubs namespace create](/en-us/cli/azure/eventhubs/namespace#az-eventhubs-namespace-create) and [az eventhubs eventhub create](/en-us/cli/azure/eventhubs/eventhub#az-eventhubs-eventhub-create). The following example creates a namespace *MyNamespace* and an event hub *MyEventGridHub* in *MyNamespace*, both in the *MyResourceGroup* resource group.

```
az eventhubs namespace create --location eastus --name MyNamespace --resource-group MyResourceGroup
az eventhubs eventhub create --name MyEventGridHub --namespace-name MyNamespace --resource-group MyResourceGroup
```


Note

The *name* of your namespace must be unique.

Subscribe to the AKS events using [az eventgrid event-subscription create](/en-us/cli/azure/eventgrid/event-subscription#az-eventgrid-event-subscription-create):

```
SOURCE_RESOURCE_ID=$(az aks show --resource-group MyResourceGroup --name MyAKS --query id --output tsv)
ENDPOINT=$(az eventhubs eventhub show --resource-group MyResourceGroup --name MyEventGridHub --namespace-name MyNamespace --query id --output tsv)
az eventgrid event-subscription create --name MyEventGridSubscription \
--source-resource-id $SOURCE_RESOURCE_ID \
--endpoint-type eventhub \
--endpoint $ENDPOINT
```


Verify your subscription to AKS events using `az eventgrid event-subscription list`

:

```
az eventgrid event-subscription list --source-resource-id $SOURCE_RESOURCE_ID
```


The following example output shows you're subscribed to events from the *MyAKS* cluster and those events are delivered to the *MyEventGridHub* event hub:

```
[
{
"deadLetterDestination": null,
"deadLetterWithResourceIdentity": null,
"deliveryWithResourceIdentity": null,
"destination": {
"deliveryAttributeMappings": null,
"endpointType": "EventHub",
"resourceId": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/Microsoft.EventHub/namespaces/MyNamespace/eventhubs/MyEventGridHub"
},
"eventDeliverySchema": "EventGridSchema",
"expirationTimeUtc": null,
"filter": {
"advancedFilters": null,
"enableAdvancedFilteringOnArrays": null,
"includedEventTypes": [
"Microsoft.ContainerService.NewKubernetesVersionAvailable","Microsoft.ContainerService.ClusterSupportEnded","Microsoft.ContainerService.ClusterSupportEnding","Microsoft.ContainerService.NodePoolRollingFailed","Microsoft.ContainerService.NodePoolRollingStarted","Microsoft.ContainerService.NodePoolRollingSucceeded"
],
"isSubjectCaseSensitive": null,
"subjectBeginsWith": "",
"subjectEndsWith": ""
},
"id": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/Microsoft.ContainerService/managedClusters/MyAKS/providers/Microsoft.EventGrid/eventSubscriptions/MyEventGridSubscription",
"labels": null,
"name": "MyEventGridSubscription",
"provisioningState": "Succeeded",
"resourceGroup": "MyResourceGroup",
"retryPolicy": {
"eventTimeToLiveInMinutes": 1440,
"maxDeliveryAttempts": 30
},
"systemData": null,
"topic": "/subscriptions/SUBSCRIPTION_ID/resourceGroups/MyResourceGroup/providers/microsoft.containerservice/managedclusters/MyAKS",
"type": "Microsoft.EventGrid/eventSubscriptions"
}
]
```


When AKS events occur, you see those events appear in your event hub. For example, when the list of available Kubernetes versions for your clusters changes, you see a `Microsoft.ContainerService.NewKubernetesVersionAvailable`

event. There are also new events available now for upgrades and cluster within support. For more information on the events AKS emits, see [Azure Kubernetes Service (AKS) as an Event Grid source](/en-us/azure/event-grid/event-schema-aks).

## Delete the cluster and subscriptions

Use the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, the AKS cluster, namespace, and event hub, and all related resources.

```
az group delete --name MyResourceGroup --yes --no-wait
```


Note

When you delete the cluster, the Microsoft Entra service principal used by the AKS cluster isn't removed. For steps on how to remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal).

If you used a managed identity, the identity is managed by the platform and doesn't require removal.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then subscribed to AKS events in Azure Event Hubs.

To learn more about AKS, and walk through a complete code to deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/spot-node-pool -->

# Add an Azure Spot node pool to an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you add a secondary Spot node pool to an existing Azure Kubernetes Service (AKS) cluster.

A Spot node pool is a node pool backed by an [Azure Spot Virtual Machine scale set](/en-us/azure/virtual-machine-scale-sets/use-spot). With Spot VMs in your AKS cluster, you can take advantage of unutilized Azure capacity with significant cost savings. The amount of available unutilized capacity varies based on many factors, such as node size, region, and time of day.

When you deploy a Spot node pool, Azure allocates the Spot nodes if there's capacity available and deploys a Spot scale set that backs the Spot node pool in a single default domain. There's no SLA for the Spot nodes. There are no high availability guarantees. If Azure needs capacity back, the Azure infrastructure evicts the Spot nodes.

Spot nodes are great for workloads that can handle interruptions, early terminations, or evictions. For example, workloads such as batch processing jobs, development and testing environments, and large compute workloads might be good candidates to schedule on a Spot node pool.

## Before you begin

- This article assumes a basic understanding of Kubernetes and Azure Load Balancer concepts. For more information, see
[Kubernetes core concepts for Azure Kubernetes Service (AKS)](concepts-clusters-workloads). - If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - When you create a cluster to use a Spot node pool, the cluster must use Virtual Machine Scale Sets for node pools and the
*Standard*SKU load balancer. You must also add another node pool after you create your cluster, which is covered in this tutorial. - This article requires that you're running the Azure CLI version 2.14 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

The following limitations apply when you create and manage AKS clusters with a Spot node pool:

- A Spot node pool can't be a default node pool, it can only be used as a secondary pool.
- You can't upgrade the control plane and node pools at the same time. You must upgrade them separately or remove the Spot node pool to upgrade the control plane and remaining node pools at the same time.
- A Spot node pool must use Virtual Machine Scale Sets.
- You can't change
`ScaleSetPriority`

or`SpotMaxPrice`

after creation. - When setting
`SpotMaxPrice`

, the value must be*-1*or a*positive value with up to five decimal places*. - A Spot node pool has the
`kubernetes.azure.com/scalesetpriority:spot`

label, the`kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

taint, and the system pods have anti-affinity. - You must add a
[corresponding toleration](#verify-the-spot-node-pool)and affinity to schedule workloads on a Spot node pool.

## Add a Spot node pool to an AKS cluster

When adding a Spot node pool to an existing cluster, it must be a cluster with multiple node pools enabled. When you create an AKS cluster with multiple node pools enabled, you create a node pool with a `priority`

of `Regular`

by default. To add a Spot node pool, you must specify `Spot`

as the value for `priority`

. For more details on creating an AKS cluster with multiple node pools, see [use multiple node pools](create-node-pools).

- Create a node pool with a
`priority`

of`Spot`

using thecommand.`az aks nodepool add`


```
export SPOT_NODEPOOL="spotnodepool"
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $AKS_CLUSTER \
--name $SPOT_NODEPOOL \
--priority Spot \
--eviction-policy Delete \
--spot-max-price -1 \
--enable-cluster-autoscaler \
--min-count 1 \
--max-count 3 \
--no-wait
```


In the previous command, the `priority`

of `Spot`

makes the node pool a Spot node pool. The `eviction-policy`

parameter is set to `Delete`

, which is the default value. When you set the [eviction policy](/en-us/azure/virtual-machine-scale-sets/use-spot#eviction-policy) to `Delete`

, nodes in the underlying scale set of the node pool are deleted when they're evicted.

You can also set the eviction policy to `Deallocate`

, which means that the nodes in the underlying scale set are set to the *stopped-deallocated* state upon eviction. Nodes in the *stopped-deallocated* state count against your compute quota and can cause issues with cluster scaling or upgrading. The `priority`

and `eviction-policy`

values can only be set during node pool creation. Those values can't be updated later.

The previous command also enables the [cluster autoscaler](cluster-autoscaler), which we recommend using with Spot node pools. Based on the workloads running in your cluster, the cluster autoscaler scales the number of nodes up and down. For Spot node pools, the cluster autoscaler will scale up the number of nodes after an eviction if more nodes are still needed. If you change the maximum number of nodes a node pool can have, you also need to adjust the `maxCount`

value associated with the cluster autoscaler. If you don't use a cluster autoscaler, upon eviction, the Spot pool will eventually decrease to *0* and require manual operation to receive any additional Spot nodes.

Important

Only schedule workloads on Spot node pools that can handle interruptions, such as batch processing jobs and testing environments. We recommend you set up [taints and tolerations](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations) on your Spot node pool to ensure that only workloads that can handle node evictions are scheduled on a Spot node pool. For example, the above command adds a taint of `kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

, so only pods with a corresponding toleration are scheduled on this node.

## Verify the Spot node pool

- Verify your node pool was added using the
command and confirming the`az aks nodepool show`

`scaleSetPriority`

is`Spot`

.

```
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $AKS_CLUSTER --name $SPOT_NODEPOOL
```


Results:

```
{
"artifactStreamingProfile": null,
"availabilityZones": null,
"capacityReservationGroupId": null,
"count": 3,
"creationData": null,
"currentOrchestratorVersion": "1.30.10",
"eTag": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx",
"enableAutoScaling": true,
"enableCustomCaTrust": false,
"enableEncryptionAtHost": false,
"enableFips": false,
"enableNodePublicIp": false,
"enableUltraSsd": false,
"gatewayProfile": null,
"gpuInstanceProfile": null,
"gpuProfile": null,
"hostGroupId": null,
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/xxxxxxxxxxxxxxxx/providers/Microsoft.ContainerService/managedClusters/xxxxxxxxxxxxxxxx/agentPools/xxxxxxxxxxxx",
"kubeletConfig": null,
"kubeletDiskType": "OS",
"linuxOsConfig": null,
"maxCount": 3,
"maxPods": 30,
"messageOfTheDay": null,
"minCount": 1,
"mode": "User",
"name": "xxxxxxxxxxxx",
"networkProfile": {
"allowedHostPorts": null,
"applicationSecurityGroups": null,
"nodePublicIpTags": null
},
"nodeImageVersion": "AKSUbuntu-2204gen2containerd-xxxxxxxx.xx.x",
"nodeInitializationTaints": null,
"nodeLabels": {
"kubernetes.azure.com/scalesetpriority": "spot"
},
"nodePublicIpPrefixId": null,
"nodeTaints": [
"kubernetes.azure.com/scalesetpriority=spot:NoSchedule"
],
"orchestratorVersion": "x.xx.xx",
"osDiskSizeGb": 128,
"osDiskType": "Managed",
"osSku": "Ubuntu",
"osType": "Linux",
"podIpAllocationMode": null,
"podSubnetId": null,
"powerState": {
"code": "Running"
},
"provisioningState": "Creating",
"proximityPlacementGroupId": null,
"resourceGroup": "xxxxxxxxxxxxxxxx",
"scaleDownMode": "Delete",
"scaleSetEvictionPolicy": "Delete",
"scaleSetPriority": "Spot",
"securityProfile": {
"enableSecureBoot": false,
"enableVtpm": false,
"sshAccess": "LocalUser"
},
"spotMaxPrice": -1.0,
"status": null,
"tags": null,
"type": "Microsoft.ContainerService/managedClusters/agentPools",
"typePropertiesType": "VirtualMachineScaleSets",
"upgradeSettings": {
"drainTimeoutInMinutes": null,
"maxSurge": null,
"maxUnavailable": null,
"nodeSoakDurationInMinutes": null,
"undrainableNodeBehavior": null
},
"virtualMachineNodesStatus": null,
"virtualMachinesProfile": null,
"vmSize": "Standard_DS2_v2",
"vnetSubnetId": null,
"windowsProfile": null,
"workloadRuntime": "OCIContainer"
}
```


## Schedule a pod to run on the Spot node

To schedule a pod to run on a Spot node, you can add a toleration and node affinity that corresponds to the taint applied to your Spot node.

The following example shows a portion of a YAML file that defines a toleration corresponding to the `kubernetes.azure.com/scalesetpriority=spot:NoSchedule`

taint and a node affinity corresponding to the `kubernetes.azure.com/scalesetpriority=spot`

label used in the previous step with `requiredDuringSchedulingIgnoredDuringExecution`

and `preferredDuringSchedulingIgnoredDuringExecution`

node affinity rules:

```
spec:
containers:
- name: spot-example
tolerations:
- key: "kubernetes.azure.com/scalesetpriority"
operator: "Equal"
value: "spot"
effect: "NoSchedule"
affinity:
nodeAffinity:
requiredDuringSchedulingIgnoredDuringExecution:
nodeSelectorTerms:
- matchExpressions:
- key: "kubernetes.azure.com/scalesetpriority"
operator: In
values:
- "spot"
preferredDuringSchedulingIgnoredDuringExecution:
- weight: 1
preference:
matchExpressions:
- key: another-node-label-key
operator: In
values:
- another-node-label-value
```


When you deploy a pod with this toleration and node affinity, Kubernetes successfully schedules the pod on the nodes with the taint and label applied. In this example, the following rules apply:

- The node
*must*have a label with the key`kubernetes.azure.com/scalesetpriority`

, and the value of that label*must*be`spot`

. - The node
*preferably*has a label with the key`another-node-label-key`

, and the value of that label*must*be`another-node-label-value`

.

For more information, see [Assigning pods to nodes](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity).

## Upgrade a Spot node pool

When you upgrade a Spot node pool, AKS internally issues a cordon and an eviction notice, but no drain is applied. There are no surge nodes available for Spot node pool upgrades. Outside of these changes, the behavior when upgrading Spot node pools is consistent with that of other node pool types.

For more information on upgrading, see [Upgrade an AKS cluster](upgrade-cluster).

## Max price for a Spot pool

[Pricing for Spot instances is variable](/en-us/azure/virtual-machine-scale-sets/use-spot#pricing), based on region and SKU. For more information, see pricing information for [Linux](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/linux/) and [Windows](https://azure.microsoft.com/pricing/details/virtual-machine-scale-sets/windows/).

With variable pricing, you have the option to set a max price, in US dollars (USD) using up to five decimal places. For example, the value *0.98765* would be a max price of *$0.98765 USD per hour*. If you set the max price to *-1*, the instance won't be evicted based on price. As long as there's capacity and quota available, the price for the instance will be the lower price of either the current price for a Spot instance or for a standard instance.

## Next steps

In this article, you learned how to add a Spot node pool to an AKS cluster. For more information about how to control pods across node pools, see [Best practices for advanced scheduler features in AKS](operator-best-practices-advanced-scheduler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-cni-overlay -->

# Configure Azure CNI Overlay networking in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains the setup process, dual-stack networking configuration, and an example workload deployment for Azure CNI Overlay in Azure Kubernetes Service (AKS) clusters. For an overview of Azure CNI Overlay networking, see [Overview of Azure CNI Overlay networking in Azure Kubernetes Service (AKS)](concepts-network-azure-cni-overlay).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/free/)before you begin. - Azure CLI version 2.48.0 or later. To install or upgrade the Azure CLI, see
[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - An existing Azure resource group. If you need to create one, see
[Create resource groups](/en-us/azure/azure-resource-manager/management/manage-resource-groups-cli#create-resource-groups).

For dual-stack networking, you need Kubernetes version 1.26.3 or later.

## Key parameters for Azure CNI Overlay AKS clusters

The following table describes the key parameters for configuring Azure CNI Overlay networking in AKS clusters:

| Parameter | Description |
|---|---|
`--network-plugin` |
Set to `azure` to use Azure Container Networking Interface (CNI) networking. |
`--network-plugin-mode` |
Set to `overlay` to enable Azure CNI Overlay networking. This setting applies only when `--network-plugin=azure` . |
`--pod-cidr` |
Specify a custom pod Classless Inter-Domain Routing (CIDR) block for the cluster. The default is `10.244.0.0/16` . |

The default behavior for network plugins depends on whether you explicitly set `--network-plugin`

:

- If you don't specify
`--network-plugin`

, AKS defaults to Azure CNI Overlay. - If you specify
`--network-plugin=azure`

and omit`--network-plugin-mode`

, AKS intentionally uses virtual network (node subnet) mode for backward compatibility.

## Create an Azure CNI Overlay AKS cluster

Create an Azure CNI Overlay AKS cluster by using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with

`--network-plugin=azure`

and `--network-plugin-mode=overlay`

. If you don't specify a value for `--pod-cidr`

, AKS assigns the default value of `10.244.0.0/16`

.```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--location $REGION \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--generate-ssh-keys
```


## Add a new node pool to a dedicated subnet

Add a node pool to a different subnet within the same virtual network to control virtual machine (VM) node IP addresses for network traffic to virtual network or peered virtual network resources.

Add a new node pool to the cluster by using the [ az aks nodepool add](/en-us/cli/azure/aks#az_aks_nodepool_add) command and specify the subnet resource ID with the

`--vnet-subnet-id`

parameter. For example:```
az aks nodepool add \
--resource-group $RESOURCE_GROUP \
--cluster-name $CLUSTER_NAME \
--name $NODE_POOL_NAME \
--node-count 1 \
--mode system \
--vnet-subnet-id $SUBNET_RESOURCE_ID
```


## About Azure CNI Overlay AKS clusters with dual-stack networking

You can deploy your Azure CNI Overlay AKS clusters in a dual-stack mode with an Azure virtual network. In this configuration, nodes receive both an IPv4 and IPv6 address from the Azure virtual network subnet. Pods receive an IPv4 and IPv6 address from a different address space to the Azure virtual network subnet of the nodes. Network address translation (NAT) is then configured so that the pods can reach resources on the Azure virtual network. The source IP address of the traffic is NAT'd to the node's primary IP address of the same family (*IPv4 to IPv4* and *IPv6 to IPv6*).

Note

You can also deploy dual-stack networking clusters by using Azure CNI Powered by Cilium. For more information, see [Dual-stack networking with Azure CNI Powered by Cilium](azure-cni-powered-by-cilium#dual-stack-networking-with-azure-cni-powered-by-cilium).

## Dual-stack networking limitations

The following features aren't supported with dual-stack networking:

## Key parameters for dual-stack networking

The following table describes the key parameters for configuring dual-stack networking in Azure CNI Overlay AKS clusters:

| Parameter | Description |
|---|---|
`--ip-families` |
Takes a comma-separated list of IP families to enable on the cluster. Only `ipv4` and `ipv4,ipv6` are supported. |
`--pod-cidrs` |
Takes a comma-separated list of Classless Inter-Domain Routing (CIDR) notation IP ranges to assign pod IPs from. The count and order of ranges in this list must match the value provided to `--ip-families` . If you don't supply any values, the parameter uses the default value of `10.244.0.0/16,fd12:3456:789a::/64` . |
`--service-cidrs` |
Takes a comma-separated list of CIDR notation IP ranges to assign service IPs from. The count and order of ranges in this list must match the value provided to `--ip-families` . If you don't supply any values, the parameter uses the default value of `10.0.0.0/16,fd12:3456:789a:1::/108` . The IPv6 subnet assigned to `--service-cidrs` can be no larger than `/108` . |

## Create an Azure CNI Overlay AKS cluster with dual-stack networking (Linux)

Create an Azure resource group for the cluster by using the

command:`az group create`

`az group create --location $REGION --name $RESOURCE_GROUP`

Create a dual-stack AKS cluster by using the

command with the`az aks create`

`--ip-families`

parameter set to`ipv4,ipv6`

:`az aks create \ --location $REGION \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --network-plugin azure \ --network-plugin-mode overlay \ --ip-families ipv4,ipv6 \ --generate-ssh-keys`


## Create an Azure CNI Overlay AKS cluster with dual-stack networking (Windows)

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Before you create an Azure CNI Overlay AKS cluster with dual-stack networking with Windows node pools, you need to install the `aks-preview`

Azure CLI extension and register the `AzureOverlayDualStackPreview`

feature flag in your subscription.

### Install the `aks-preview`

Azure CLI extension

Install the

`aks-preview`

extension by using thecommand:`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension by using the

command:`az extension update`

`az extension update --name aks-preview`


### Register the `AzureOverlayDualStackPreview`

feature flag

Register the

`AzureOverlayDualStackPreview`

feature flag by using thecommand:`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AzureOverlayDualStackPreview"`

It takes a few minutes for the status to show

`Registered`

.Verify the registration status by using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AzureOverlayDualStackPreview"`

When the status reflects

`Registered`

, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand:`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a dual-stack Azure CNI Overlay AKS cluster and add a Windows node pool

Create a cluster with Azure CNI Overlay by using the

command:`az aks create`

`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --location $REGION \ --network-plugin azure \ --network-plugin-mode overlay \ --ip-families ipv4,ipv6 \ --generate-ssh-keys`

Add a Windows node pool to the cluster by using the

command:`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --os-type Windows \ --name $WINDOWS_NODE_POOL_NAME \ --node-count 2`


## Deploy an example workload to the Azure CNI Overlay AKS cluster

Deploy dual-stack AKS CNI Overlay clusters with IPv4/IPv6 addresses on virtual machine nodes. This example deploys an NGINX web server and exposes it by using a `LoadBalancer`

service with both IPv4 and IPv6 addresses.

Note

We recommend using the application routing add-on for ingress in AKS clusters. However, for demonstration purposes, this example deploys an NGINX web server without the application routing add-on. For more information about the add-on, see [Managed NGINX ingress with the application routing add-on](app-routing).

### Expose the workload by using a `LoadBalancer`

service

Expose the NGINX deployment by using either `kubectl`

commands or YAML manifests.

Important

There are currently *two limitations* that pertain to IPv6 services in AKS:

- Azure Load Balancer sends health probes to IPv6 destinations from a link-local address. In
*Azure Linux node pools*, you can't route this traffic to a pod, so traffic flowing to IPv6 services deployed with`externalTrafficPolicy: Cluster`

fails. - You must deploy IPv6 services with
`externalTrafficPolicy: Local`

, which causes`kube-proxy`

to respond to the probe on the node.

Expose the NGINX deployment by using the

`kubectl expose deployment nginx`

command:`kubectl expose deployment nginx --name=nginx-ipv4 --port=80 --type=LoadBalancer kubectl expose deployment nginx --name=nginx-ipv6 --port=80 --type=LoadBalancer --overrides='{"spec":{"ipFamilies": ["IPv6"]}}'`

Your output should show the exposed services. For example:

`service/nginx-ipv4 exposed service/nginx-ipv6 exposed`

After the deployment is exposed and the

`LoadBalancer`

services are fully provisioned, get the IP addresses of the services by using the`kubectl get services`

command:`kubectl get services`

Your output should show the services with their assigned IP addresses. For example:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE nginx-ipv4 LoadBalancer 10.0.88.78 20.46.24.24 80:30652/TCP 97s nginx-ipv6 LoadBalancer fd12:3456:789a:1::981a 2603:1030:8:5::2d 80:32002/TCP 63s`

Get the service IP by using the

`kubectl get services`

command and set it to an environment variable:`SERVICE_IP=$(kubectl get services nginx-ipv6 -o jsonpath='{.status.loadBalancer.ingress[0].ip}')`

Verify functionality by using a

`curl`

request from an IPv6-capable host. (*Azure Cloud Shell isn't IPv6 capable*.)`curl -s "http://[${SERVICE_IP}]" | head -n5`

Your output should show the HTML for the NGINX welcome page. For example:

`<!DOCTYPE html> <html> <head> <title>Welcome to nginx!</title> <style>`


## Related content

To learn more about Azure CNI Overlay networking on AKS, see the following articles:
