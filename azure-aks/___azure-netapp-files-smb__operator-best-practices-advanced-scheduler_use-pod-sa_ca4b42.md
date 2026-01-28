---
merged_at: 2026-01-28T07:16:09.842590
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-smb -->

# Provision Azure NetApp Files SMB volumes for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After you [configure Azure NetApp Files for Azure Kubernetes Service](azure-netapp-files), you can provision Azure NetApp Files volumes for Azure Kubernetes Service.

Azure NetApp Files supports volumes using [NFS](azure-netapp-files-nfs) (NFSv3 or NFSv4.1), SMB, and [dual-protocol](azure-netapp-files-dual-protocol) (NFSv3 and SMB, or NFSv4.1 and SMB).

- This article describes details for provisioning SMB volumes statically or dynamically.
- For information about provisioning NFS volumes statically or dynamically, see
[Provision Azure NetApp Files NFS volumes for Azure Kubernetes Service](azure-netapp-files-nfs). - For information about provisioning dual-protocol volumes statically, see
[Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol)

## Statically configure for applications that use SMB volumes

This section describes how to create an SMB volume on Azure NetApp Files and expose the volume statically to Kubernetes for a containerized application to consume.

### Create an SMB Volume

Define variables for later usage. Replace

*myresourcegroup*,*mylocation*,*myaccountname*,*mypool1*,*premium*,*myfilepath*,*myvolsize*,*myvolname*, and*virtnetid*with an appropriate value for your environment. The filepath must be unique within all ANF accounts.`RESOURCE_GROUP="myresourcegroup" LOCATION="mylocation" ANF_ACCOUNT_NAME="myaccountname" POOL_NAME="mypool1" SERVICE_LEVEL="premium" # Valid values are standard, premium, and ultra UNIQUE_FILE_PATH="myfilepath" VOLUME_SIZE_GIB="myvolsize" VOLUME_NAME="myvolname" VNET_ID="vnetId" SUBNET_ID="anfSubnetId"`

Create a volume using the

command.`az netappfiles volume create`

`az netappfiles volume create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --name "$VOLUME_NAME" \ --service-level $SERVICE_LEVEL \ --vnet $VNET_ID \ --subnet $SUBNET_ID \ --usage-threshold $VOLUME_SIZE_GIB \ --file-path $UNIQUE_FILE_PATH \ --protocol-types CIFS`


### Create a secret with the domain credentials

Create a secret on your AKS cluster to access the Active Directory (AD) server using the

command. This secret will be used by the Kubernetes persistent volume to access the Azure NetApp Files SMB volume. Use the following command to create the secret, replacing`kubectl create secret`

`USERNAME`

with your username,`PASSWORD`

with your password, and`DOMAIN_NAME`

with your domain name for your AD.`kubectl create secret generic smbcreds --from-literal=username=USERNAME --from-literal=password="PASSWORD" --from-literal=domain='DOMAIN_NAME'`

Check the secret has been created.

`kubectl get secret NAME TYPE DATA AGE smbcreds Opaque 2 20h`


### Install an SMB CSI driver

You must install a Container Storage Interface (CSI) driver to create a Kubernetes SMB `PersistentVolume`

.

Install the SMB CSI driver on your cluster using helm. Be sure to set the

`windows.enabled`

option to`true`

:`helm repo add csi-driver-smb https://raw.githubusercontent.com/kubernetes-csi/csi-driver-smb/master/charts helm install csi-driver-smb csi-driver-smb/csi-driver-smb --namespace kube-system --version v1.13.0 --set windows.enabled=true`

For other methods of installing the SMB CSI Driver, see

[Install SMB CSI driver master version on a Kubernetes cluster](https://github.com/kubernetes-csi/csi-driver-smb/blob/master/docs/install-csi-driver-master.md).Verify that the

`csi-smb`

controller pod is running and each worker node has a pod running using thecommand:`kubectl get pods`

`kubectl get pods -n kube-system | grep csi-smb csi-smb-controller-68df7b4758-xf2m9 3/3 Running 0 3m46s csi-smb-node-s6clj 3/3 Running 0 3m47s csi-smb-node-win-tfxvk 3/3 Running 0 3m47s`


### Create the persistent volume

List the details of your volume using

. Replace the variables with appropriate values from your Azure NetApp Files account and environment if not defined in a previous step.`az netappfiles volume show`

`az netappfiles volume show \ --resource-group $RESOURCE_GROUP \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --volume-name "$VOLUME_NAME -o JSON`

The following output is an example of the above command executed with real values.

`{ ... "creationToken": "myvolname", ... "mountTargets": [ { ... " "smbServerFqdn": "ANF-1be3.contoso.com", ... } ], ... }`

Create a file named

`pv-smb.yaml`

and copy in the following YAML. If necessary, replace`myvolname`

with the`creationToken`

and replace`ANF-1be3.contoso.com\myvolname`

with the value of`smbServerFqdn`

from the previous step. Be sure to include your AD credentials secret along with the namespace where the secret is located that you created in a prior step.`apiVersion: v1 kind: PersistentVolume metadata: name: anf-pv-smb spec: storageClassName: "" capacity: storage: 100Gi accessModes: - ReadWriteMany persistentVolumeReclaimPolicy: Retain mountOptions: - dir_mode=0777 - file_mode=0777 - vers=3.0 csi: driver: smb.csi.k8s.io readOnly: false volumeHandle: myvolname # make sure it's a unique name in the cluster volumeAttributes: source: \\ANF-1be3.contoso.com\myvolname nodeStageSecretRef: name: smbcreds namespace: default`

Create the persistent volume using the

command:`kubectl apply`

`kubectl apply -f pv-smb.yaml`

Verify the status of the persistent volume is

*Available*using thecommand:`kubectl describe`

`kubectl describe pv pv-smb`


### Create a persistent volume claim

Create a file name

`pvc-smb.yaml`

and copy in the following YAML.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: anf-pvc-smb spec: accessModes: - ReadWriteMany volumeName: anf-pv-smb storageClassName: "" resources: requests: storage: 100Gi`

Create the persistent volume claim using the

command:`kubectl apply`

`kubectl apply -f pvc-smb.yaml`

Verify the status of the persistent volume claim is

*Bound*by using the[kubectl describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe)command:`kubectl describe pvc pvc-smb`


### Mount with a pod

Create a file named

`iis-smb.yaml`

and copy in the following YAML. This file will be used to create an Internet Information Services pod to mount the volume to path`/inetpub/wwwroot`

.`apiVersion: v1 kind: Pod metadata: name: iis-pod labels: app: web spec: nodeSelector: "kubernetes.io/os": windows volumes: - name: smb persistentVolumeClaim: claimName: anf-pvc-smb containers: - name: web image: mcr.microsoft.com/windows/servercore/iis:windowsservercore resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 volumeMounts: - name: smb mountPath: "/inetpub/wwwroot" readOnly: false`

Create the pod using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f iis-smb.yaml`

Verify the pod is

*Running*and`/inetpub/wwwroot`

is mounted from SMB by using the[kubectl describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe)command:`kubectl describe pod iis-pod`

The output of the command resembles the following example:

`Name: iis-pod Namespace: default Priority: 0 Node: akswin000001/10.225.5.246 Start Time: Fri, 05 May 2023 09:34:41 -0400 Labels: app=web Annotations: <none> Status: Running IP: 10.225.5.248 IPs: IP: 10.225.5.248 Containers: web: Container ID: containerd://39a1659b6a2b6db298df630237b2b7d959d1b1722edc81ce9b1bc7f06237850c Image: mcr.microsoft.com/windows/servercore/iis:windowsservercore Image ID: mcr.microsoft.com/windows/servercore/iis@sha256:0f0114d0f6c6ee569e1494953efdecb76465998df5eba951dc760ac5812c7409 Port: 80/TCP Host Port: 0/TCP State: Running Started: Fri, 05 May 2023 09:34:55 -0400 Ready: True Restart Count: 0 Limits: cpu: 1 memory: 800M Requests: cpu: 1 memory: 800M Environment: <none> Mounts: /inetpub/wwwroot from smb (rw) /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-mbnv8 (ro) ...`

Verify your volume has been mounted on the pod by using the

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command to connect to the pod, and then use`dir`

command in the correct directory to check if the volume is mounted and the size matches the size of the volume you provisioned.`kubectl exec -it iis-pod –- cmd.exe`

The output of the command resembles the following example:

`Microsoft Windows [Version 10.0.20348.1668] (c) Microsoft Corporation. All rights reserved. C:\>cd /inetpub/wwwroot C:\inetpub\wwwroot>dir Volume in drive C has no label. Volume Serial Number is 86BB-AA55 Directory of C:\inetpub\wwwroot 05/04/2023 08:15 PM <DIR> . 05/04/2023 08:15 PM <DIR> .. 0 File(s) 0 bytes 2 Dir(s) 107,373,838,336 bytes free`


## Dynamically configure for applications that use SMB volumes

This section covers how to use Trident to dynamically create an SMB volume on Azure NetApp Files and automatically mount it to a containerized windows application.

### Install Trident

To dynamically provision SMB volumes, you need to install Trident version 22.10 or later. Dynamically provisioning SMB volumes requires windows worker nodes.

Trident is NetApp's dynamic storage provisioner that is purpose-built for Kubernetes. Simplify the consumption of storage for Kubernetes applications using Trident's industry-standard [Container Storage Interface (CSI)](https://kubernetes-csi.github.io/docs/) driver. Trident deploys on Kubernetes clusters as pods and provides dynamic storage orchestration services for your Kubernetes workloads.

Trident can be installed using the Trident operator (manually or using [Helm](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-operator.html)) or [ tridentctl](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-tridentctl.html). To learn more about these installation methods and how they work, see the

[Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html).

#### Install Trident using Helm

[Helm](https://helm.sh/) must be installed on your workstation to install Trident using this method. For other methods of installing Trident, see the [Trident Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html). If you have windows worker nodes in the cluster, ensure to enable windows with any installation method.

To install Trident using Helm for a cluster with windows worker nodes, run the following commands:

`helm repo add netapp-trident https://netapp.github.io/trident-helm-chart helm install trident netapp-trident/trident-operator --version 23.04.0 --create-namespace --namespace trident –-set windows=true`

The output of the command resembles the following example:

`NAME: trident LAST DEPLOYED: Fri May 5 14:23:05 2023 NAMESPACE: trident STATUS: deployed REVISION: 1 TEST SUITE: None NOTES: Thank you for installing trident-operator, which will deploy and manage NetApp's Trident CSI storage provisioner for Kubernetes. Your release is named 'trident' and is installed into the 'trident' namespace. Please note that there must be only one instance of Trident (and trident-operator) in a Kubernetes cluster. To configure Trident to manage storage resources, you will need a copy of tridentctl, which is available in pre-packaged Trident releases. You may find all Trident releases and source code online at https://github.com/NetApp/trident. To learn more about the release, try: $ helm status trident $ helm get all trident`

To confirm Trident was installed successfully, run the following

command:`kubectl describe`

`kubectl describe torc trident`

The output of the command resembles the following example:

`Name: trident Namespace: Labels: app.kubernetes.io/managed-by=Helm Annotations: meta.helm.sh/release-name: trident meta.helm.sh/release-namespace: trident API Version: trident.netapp.io/v1 Kind: TridentOrchestrator Metadata: ... Spec: IPv6: false Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: <nil> Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent k8sTimeout: 0 Kubelet Dir: <nil> Log Format: text Log Layers: <nil> Log Workflows: <nil> Namespace: trident Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Windows: true Status: Current Installation Params: IPv6: false Autosupport Hostname: Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: Autosupport Serial Number: Debug: false Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent Image Pull Secrets: Image Registry: k8sTimeout: 30 Kubelet Dir: /var/lib/kubelet Log Format: text Log Layers: Log Level: info Log Workflows: Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Message: Trident installed Namespace: trident Status: Installed Version: v23.04.0 Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Installing 74s trident-operator.netapp.io Installing Trident Normal Installed 46s trident-operator.netapp.io Trident installed`


### Create a backend

A backend must be created to instruct Trident about the Azure NetApp Files subscription and where it needs to create volumes. For more information about backends, see [Azure NetApp Files backend configuration options and examples](https://docs.netapp.com/us-en/trident/trident-use/anf-examples.html).

Create a file named

`backend-secret-smb.yaml`

and copy in the following YAML. Change the`Client ID`

and`clientSecret`

to the correct values for your environment.`apiVersion: v1 kind: Secret metadata: name: backend-tbc-anf-secret type: Opaque stringData: clientID: 00001111-aaaa-2222-bbbb-3333cccc4444 clientSecret: rR0rUmWXfNioN1KhtHisiSAnoTherboGuskey6pU`

Create a file named

`backend-anf-smb.yaml`

and copy in the following YAML. Change the`ClientID`

,`clientSecret`

,`subscriptionID`

,`tenantID`

,`location`

, and`serviceLevel`

to the correct values for your environment. The`tenantID`

,`clientID`

, and`clientSecret`

can be found from an application registration in Microsoft Entra ID with sufficient permissions for the Azure NetApp Files service. The application registration includes the Owner or Contributor role predefined by Azure. The Azure location must contain at least one delegated subnet. The`serviceLevel`

must match the`serviceLevel`

configured for the capacity pool in[Configure Azure NetApp Files for AKS workloads](azure-netapp-files#configure-azure-netapp-files-for-aks-workloads).`apiVersion: trident.netapp.io/v1 kind: TridentBackendConfig metadata: name: backend-tbc-anf-smb spec: version: 1 storageDriverName: azure-netapp-files subscriptionID: aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e tenantID: aaaabbbb-0000-cccc-1111-dddd2222eeee location: eastus serviceLevel: Premium credentials: name: backend-tbc-anf-secret nasType: smb`

Create the secret and backend using the

command.`kubectl apply`

Create the secret:

`kubectl apply -f backend-secret.yaml -n trident`

The output of the command resembles the following example:

`secret/backend-tbc-anf-secret created`

Create the backend:

`kubectl apply -f backend-anf.yaml -n trident`

The output of the command resembles the following example:

`tridentbackendconfig.trident.netapp.io/backend-tbc-anf created`

Verify the backend was created by running the following command:

`kubectl get tridentbackends -n trident`

The output of the command resembles the following example:

`NAME BACKEND BACKEND UUID tbe-9shfq backend-tbc-anf-smb 09cc2d43-8197-475f-8356-da7707bae203`


### Create a secret with the domain credentials for SMB

Create a secret on your AKS cluster to access the AD server using the

command. This information will be used by the Kubernetes persistent volume to access the Azure NetApp Files SMB volume. Use the following command, replacing`kubectl create secret`

`DOMAIN_NAME\USERNAME`

with your domain name and username and`PASSWORD`

with your password.`kubectl create secret generic smbcreds --from-literal=username=DOMAIN_NAME\USERNAME –from-literal=password="PASSWORD"`

Verify that the secret has been created.

`kubectl get secret`

The output resembles the following example:

`NAME TYPE DATA AGE smbcreds Opaque 2 2h`


### Create a storage class

A storage class is used to define how a unit of storage is dynamically created with a persistent volume. To consume Azure NetApp Files volumes, a storage class must be created.

Create a file named

`anf-storageclass-smb.yaml`

and copy in the following YAML.`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: anf-sc-smb provisioner: csi.trident.netapp.io allowVolumeExpansion: true parameters: backendType: "azure-netapp-files" trident.netapp.io/nasType: "smb" csi.storage.k8s.io/node-stage-secret-name: "smbcreds" csi.storage.k8s.io/node-stage-secret-namespace: "default"`

Create the storage class using the

command:`kubectl apply`

`kubectl apply -f anf-storageclass-smb.yaml`

The output of the command resembles the following example:

`storageclass/anf-sc-smb created`

Run the

command to view the status of the storage class:`kubectl get`

`kubectl get sc anf-sc-smb NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE anf-sc-smb csi.trident.netapp.io Delete Immediate true 13s`


### Create a PVC

A persistent volume claim (PVC) is a request for storage by a user. Upon the creation of a persistent volume claim, Trident automatically creates an Azure NetApp Files SMB share and makes it available for Kubernetes workloads to consume.

Create a file named

`anf-pvc-smb.yaml`

and copy the following YAML. In this example, a 100-GiB volume is created with`ReadWriteMany`

access and uses the storage class created in[Create a storage class](#create-a-storage-class).`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: anf-pvc-smb spec: accessModes: - ReadWriteMany resources: requests: storage: 100Gi storageClassName: anf-sc-smb`

Create the persistent volume claim with the

command:`kubectl apply`

`kubectl apply -f anf-pvc-smb.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/anf-pvc-smb created`

To view information about the persistent volume claim, run the

command:`kubectl get`

`kubectl get pvc`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE anf-pvc-smb Bound pvc-209268f5-c175-4a23-b61b-e34faf5b6239 100Gi RWX anf-sc-smb 5m38s`

To view the persistent volume created by Trident, run the following

command:`kubectl get`

`kubectl get pv NAME CAPACITY ACCESS MODES RECLAIM POLICY STATUS CLAIM STORAGECLASS REASON AGE pvc-209268f5-c175-4a23-b61b-e34faf5b6239 100Gi RWX Delete Bound default/anf-pvc-smb anf-sc-smb 5m52s`


### Use the persistent volume

After the PVC is created, a pod can be spun up to access the Azure NetApp Files volume. The following manifest can be used to define an Internet Information Services (IIS) pod that mounts the Azure NetApp Files SMB share created in the previous step. In this example, the volume is mounted at `/inetpub/wwwroot`

.

Create a file named

`anf-iis-pod.yaml`

and copy in the following YAML:`apiVersion: v1 kind: Pod metadata: name: iis-pod labels: app: web spec: nodeSelector: "kubernetes.io/os": windows volumes: - name: smb persistentVolumeClaim: claimName: anf-pvc-smb containers: - name: web image: mcr.microsoft.com/windows/servercore/iis:windowsservercore resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 volumeMounts: - name: smb mountPath: "/inetpub/wwwroot" readOnly: false`

Create the deployment using the

command:`kubectl apply`

`kubectl apply -f anf-iis-deploy-pod.yaml`

The output of the command resembles the following example:

`pod/iis-pod created`

Verify that the pod is running and is mounted via SMB to

`/inetpub/wwwroot`

by using thecommand:`kubectl describe`

`kubectl describe pod iis-pod`

The output of the command resembles the following example:

`Name: iis-pod Namespace: default Priority: 0 Node: akswin000001/10.225.5.246 Start Time: Fri, 05 May 2023 15:16:36 -0400 Labels: app=web Annotations: <none> Status: Running IP: 10.225.5.252 IPs: IP: 10.225.5.252 Containers: web: Container ID: containerd://1e4959f2b49e7ad842b0ec774488a6142ac9152ca380c7ba4d814ae739d5ed3e Image: mcr.microsoft.com/windows/servercore/iis:windowsservercore Image ID: mcr.microsoft.com/windows/servercore/iis@sha256:0f0114d0f6c6ee569e1494953efdecb76465998df5eba951dc760ac5812c7409 Port: 80/TCP Host Port: 0/TCP State: Running Started: Fri, 05 May 2023 15:16:44 -0400 Ready: True Restart Count: 0 Limits: cpu: 1 memory: 800M Requests: cpu: 1 memory: 800M Environment: <none> Mounts: /inetpub/wwwroot from smb (rw) /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-zznzs (ro)`

Verify that your volume has been mounted on the pod by using

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)to connect to the pod. And then use the`dir`

command in the correct directory to check if the volume is mounted and the size matches the size of the volume you provisioned.`kubectl exec -it iis-pod –- cmd.exe`

The output of the command resembles the following example:

`Microsoft Windows [Version 10.0.20348.1668] (c) Microsoft Corporation. All rights reserved. C:\>cd /inetpub/wwwroot C:\inetpub\wwwroot>dir Volume in drive C has no label. Volume Serial Number is 86BB-AA55 Directory of C:\inetpub\wwwroot 05/05/2023 01:38 AM <DIR> . 05/05/2023 01:38 AM <DIR> .. 0 File(s) 0 bytes 2 Dir(s) 107,373,862,912 bytes free C:\inetpub\wwwroot>exit`


## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-advanced-scheduler -->

# Best practices for advanced scheduler features in Azure Kubernetes Service (AKS) using the kube-scheduler

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. Advanced features provided by the Kubernetes scheduler let you control:

- Which pods can be scheduled on certain nodes.
- How multi-pod applications can be appropriately distributed across the cluster.

This best practices article focuses on advanced Kubernetes scheduling features for cluster operators. In this article, you learn how to:

- Use taints and tolerations to limit what pods can be scheduled on nodes.
- Give preference to pods to run on certain nodes with node selectors or node affinity.
- Split apart or group together pods with inter-pod affinity or anti-affinity.
- Restrict scheduling of workloads that require GPUs only on nodes with schedulable GPUs.

If additional capabilities or ML frameworks are needed to schedule and queue batch workloads, you can [install and configure Kueue on AKS](kueue-overview) to ensure efficient, policy-driven scheduling in AKS clusters.

If fine-grained scheduler configuration is needed to optimize how pods and jobs prioritize specific nodes, storage resources, topology, and more, you can [configure a scheduler on AKS](concepts-scheduler-configuration).

## Provide dedicated nodes using taints and tolerations


Best practice guidance:Limit access for resource-intensive applications, such as ingress controllers, to specific nodes. Keep node resources available for workloads that require them, and don't allow scheduling of other workloads on the nodes.


When you create your AKS cluster, you can deploy nodes with GPU support or a large number of powerful CPUs. For more information, see [Use GPUs on AKS](gpu-cluster). You can use these nodes for large data processing workloads such as machine learning (ML) or artificial intelligence (AI).

Because this node resource hardware is typically expensive to deploy, limit the workloads that can be scheduled on these nodes. Instead, dedicate some nodes in the cluster to run ingress services and prevent other workloads.

This support for different nodes is provided by using multiple node pools. An AKS cluster supports one or more node pools.

The Kubernetes scheduler uses taints and tolerations to restrict what workloads can run on nodes.

- Apply a
**taint**to a node to indicate only specific pods can be scheduled on them. - Then apply a
**toleration**to a pod, allowing them to*tolerate*a node's taint.

When you deploy a pod to an AKS cluster, Kubernetes only schedules pods on nodes whose taint aligns with the toleration. Taints and tolerations work together to ensure that pods aren't scheduled onto inappropriate nodes. One or more taints are applied to a node, marking the node so that it doesn't accept any pods that don't tolerate the taints.

For example, assume you added a node pool in your AKS cluster for nodes with GPU support. You define name, such as *gpu*, then a value for scheduling. Setting this value to *NoSchedule* restricts the Kubernetes scheduler from scheduling pods with undefined toleration on the node.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name taintnp \
--node-taints sku=gpu:NoSchedule \
--no-wait
```


With a taint applied to nodes in the node pool, you define a toleration in the pod specification that allows scheduling on the nodes. The following example defines the `sku: gpu`

and `effect: NoSchedule`

to tolerate the taint applied to the node pool in the previous step:

```
kind: Pod
apiVersion: v1
metadata:
name: app
spec:
containers:
- name: app
image: <your-workload>:gpu
resources:
requests:
cpu: 0.5
memory: 2Gi
limits:
cpu: 4.0
memory: 16Gi
tolerations:
- key: "sku"
operator: "Equal"
value: "gpu"
effect: "NoSchedule"
```


When this pod is deployed using `kubectl apply -f gpu-toleration.yaml`

, Kubernetes can successfully schedule the pod on the nodes with the taint applied. This logical isolation lets you control access to resources within a cluster.

When you apply taints, work with your application developers and owners to allow them to define the required tolerations in their deployments.

For more information about how to use multiple node pools in AKS, see [Create multiple node pools for a cluster in AKS](create-node-pools).

### Behavior of taints and tolerations in AKS

When you upgrade a node pool in AKS, taints and tolerations follow a set pattern as they're applied to new nodes:

#### Default clusters that use Azure Virtual Machine Scale Sets

You can [taint a node pool](manage-node-pools#specify-a-taint-label-or-tag-for-a-node-pool) from the AKS API to have newly scaled out nodes receive API specified node taints.

Let's assume:

- You begin with a two-node cluster:
*node1*and*node2*. - You upgrade the node pool.
- Two other nodes are created:
*node3*and*node4*. - The taints are passed on respectively.
- The original
*node1*and*node2*are deleted.

#### Clusters without Virtual Machine Scale Sets support

Again, let's assume:

- You have a two-node cluster:
*node1*and*node2*. - You upgrade the node pool.
- An extra node is created:
*node3*. - The taints from
*node1*are applied to*node3*. *node1*is deleted.- A new
*node1*is created to replace to original*node1*. - The
*node2*taints are applied to the new*node1*. *node2*is deleted.

In essence, *node1* becomes *node3*, and *node2* becomes the new *node1*.

When you scale a node pool in AKS, taints and tolerations don't carry over by design.

## Control pod scheduling using node selectors and affinity


Best practice guidanceControl the scheduling of pods on nodes using node selectors, node affinity, or inter-pod affinity. These settings allow the Kubernetes scheduler to logically isolate workloads, such as by hardware in the node.


Taints and tolerations logically isolate resources with a hard cut-off. If the pod doesn't tolerate a node's taint, it isn't scheduled on the node.

Alternatively, you can use node selectors. For example, you label nodes to indicate locally attached SSD storage or a large amount of memory, and then define in the pod specification a node selector. Kubernetes schedules those pods on a matching node.

Unlike tolerations, pods without a matching node selector can still be scheduled on labeled nodes. This behavior allows unused resources on the nodes to consume, but prioritizes pods that define the matching node selector.

Let's look at an example of nodes with a high amount of memory. These nodes prioritize pods that request a high amount of memory. To ensure the resources don't sit idle, they also allow other pods to run. The following example command adds a node pool with the label *hardware=highmem* to the *myAKSCluster* in the *myResourceGroup*. All nodes in that node pool have this label.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name labelnp \
--node-count 1 \
--labels hardware=highmem \
--no-wait
```


A pod specification then adds the `nodeSelector`

property to define a node selector that matches the label set on a node:

```
kind: Pod
apiVersion: v1
metadata:
name: app
spec:
containers:
- name: app
image: <your-workload>:gpu
resources:
requests:
cpu: 0.5
memory: 2Gi
limits:
cpu: 4.0
memory: 16Gi
nodeSelector:
hardware: highmem
```


When you use these scheduler options, work with your application developers and owners to allow them to correctly define their pod specifications.

For more information about using node selectors, see [Assigning Pods to Nodes](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/).

### Node affinity

A node selector is a basic solution for assigning pods to a given node. *Node affinity* provides more flexibility, allowing you to define what happens if the pod can't be matched with a node. You can:

*Require*that Kubernetes scheduler matches a pod with a labeled host. Or,*Prefer*a match but allow the pod to be scheduled on a different host if no match is available.

The following example sets the node affinity to *requiredDuringSchedulingIgnoredDuringExecution*. This affinity requires the Kubernetes schedule to use a node with a matching label. If no node is available, the pod has to wait for scheduling to continue. To allow the pod to be scheduled on a different node, you can instead set the value to * preferredDuringSchedulingIgnoreDuringExecution*:

```
kind: Pod
apiVersion: v1
metadata:
name: app
spec:
containers:
- name: app
image: <your-workload>:gpu
resources:
requests:
cpu: 0.5
memory: 2Gi
limits:
cpu: 4.0
memory: 16Gi
affinity:
nodeAffinity:
requiredDuringSchedulingIgnoredDuringExecution:
nodeSelectorTerms:
- matchExpressions:
- key: hardware
operator: In
values:
- highmem
```


The *IgnoredDuringExecution* part of the setting indicates that the pod shouldn't be evicted from the node if the node labels change. The Kubernetes scheduler only uses the updated node labels for new pods being scheduled, not pods already scheduled on the nodes.

For more information, see [Affinity and anti-affinity](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity).

### Inter-pod affinity and anti-affinity

One final approach for the Kubernetes scheduler to logically isolate workloads is using inter-pod affinity or anti-affinity. These settings define that pods either *shouldn't* or *should* be scheduled on a node that has an existing matching pod. By default, the Kubernetes scheduler tries to schedule multiple pods in a replica set across nodes. You can define more specific rules around this behavior.

For example, you have a web application that also uses an Azure Cache for Redis.

- You use pod anti-affinity rules to request that the Kubernetes scheduler distributes replicas across nodes.
- You use affinity rules to ensure each web app component is scheduled on the same host as a corresponding cache.

The distribution of pods across nodes looks like the following example:

Node 1 |
Node 2 |
Node 3 |
|---|---|---|
| webapp-1 | webapp-2 | webapp-3 |
| cache-1 | cache-2 | cache-3 |

Inter-pod affinity and anti-affinity provide a more complex deployment than node selectors or node affinity. With the deployment, you logically isolate resources and control how Kubernetes schedules pods on nodes.

For a complete example of this web application with Azure Cache for Redis example, see [Co-locate pods on the same node](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#always-co-located-in-the-same-node).

## Next steps

This article focused on advanced Kubernetes scheduler features. For more information about cluster operations in AKS, see the following best practices:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-pod-sandboxing -->

# Pod Sandboxing with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To help secure and protect your container workloads from untrusted or potentially malicious code, AKS now includes a mechanism called Pod Sandboxing. Pod Sandboxing provides an isolation boundary between the container application and the shared kernel and compute resources of the container host such as CPU, memory, and networking. Applications are spun up in isolated, lightweight pod virtual machines (VMs). Pod Sandboxing complements other security measures or data protection controls with your overall architecture to help you meet regulatory, industry, or governance compliance requirements for securing sensitive information.

This article helps you understand this new feature, and how to implement it.

## Prerequisites

The Azure CLI version 2.80.0 or later. Run

`az --version`

to find the version of your Azure CLI, and run`az upgrade`

to upgrade. For more details, see the steps at[Install Azure CLI](/en-us/cli/azure/install-azure-cli).AKS supports Pod Sandboxing on Kubernetes version 1.27.0 and higher.

To manage a Kubernetes cluster, use the Kubernetes command-line client

[kubectl](https://kubernetes.io/docs/reference/kubectl/). Azure Cloud Shell comes with`kubectl`

. You can install kubectl locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.

## Limitations

The following are constraints applicable to Pod Sandboxing:

Kata containers might not reach the IOPS performance limits that traditional containers can reach on Azure Files and high-performance local SSD.

[Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction)doesn't support assessing Kata runtime pods.[Kata](https://github.com/kata-containers/kata-containers/blob/main/docs/Limitations.md#host-network)host-network access isn't supported. It isn't possible to directly access the host networking configuration from within the VM.CPU and memory allocation with Pod Sandboxing has other considerations compared to

`runc`

. Reference the memory management sections in the[considerations page](considerations-pod-sandboxing).

## How it works

Pod Sandboxing on AKS builds on top of the open-source [Kata Containers](https://katacontainers.io/) project. Kata Containers running on the Azure Linux container host for AKS provides VM based isolation and a separate kernel for each pod. Pod Sandboxing allows users to allocate resources for each pod and doesn't share them with other Kata Containers or namespace containers running on the same host.

The solution architecture is based on the following main components:

- The
[Azure Linux container host for AKS](use-azure-linux) - Microsoft Hyper-V Hypervisor
- Open-source
[Cloud-Hypervisor](https://www.cloudhypervisor.org)Virtual Machine Monitor (VMM) - Integration with
[Kata Container](https://katacontainers.io)for the runtime

Deploying Pod Sandboxing using Kata Containers is similar to the standard `containerd`

workflow to deploy containers. Clusters with Pod Sandboxing enabled come with a specific runtime class that can be referenced in a pod manifest (`runtimeClassName: kata-vm-isolation`

).

To use this feature with a pod, the only difference is to add the **runtimeClassName**, `kata-vm-isolation`

to the pod spec. When a pod uses the `kata-vm-isolation`

runtimeClass, the hypervisor spins up a lightweight virtual machine with its own kernel, for the workload to operate in.

## Deploy new cluster

Perform the following steps to deploy an Azure Linux AKS cluster using the Azure CLI.

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command and specifying the following parameters:**--workload-runtime**: Specify*KataVmIsolation*to enable the Pod Sandboxing feature on the node pool. With this parameter, these other parameters should satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameters.**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature.**--node-vm-size**: Any Azure VM size that is a generation 2 VM and supports nested virtualization works. For example,[Dsv3](/en-us/azure/virtual-machines/dv3-dsv3-series#dsv3-series)VMs.

The following example creates a cluster named

*myAKSCluster*with one node in the*myResourceGroup*:`az aks create --name myAKSCluster \ --resource-group myResourceGroup \ --os-sku AzureLinux \ --workload-runtime KataVmIsolation \ --node-vm-size Standard_D4s_v3 \ --node-count 3 \ --generate-ssh-keys`

Run the following command to get access credentials for the Kubernetes cluster. Use the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command and replace the values for the cluster name and the resource group name.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

List all Pods in all namespaces using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.`kubectl get pods --all-namespaces`


## Deploy to an existing cluster

To use this feature with an existing AKS cluster, the following requirements must be met:

- Verify the cluster is running Kubernetes version 1.27.0 and higher.

Use the following command to enable Pod Sandboxing by creating a node pool to host it.

Add a node pool to your AKS cluster using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command. Specify the following parameters:**--resource-group**: Enter the name of an existing resource group to create the AKS cluster in.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter a unique name for your clusters node pool, such as*nodepool2*.**--workload-runtime**: Specify*KataVmIsolation*to enable the Pod Sandboxing feature on the node pool. Along with the`--workload-runtime`

parameter, these other parameters shall satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameter.**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature.**--node-vm-size**: Any Azure VM size that is a generation 2 VM and supports nested virtualization works. For example,[Dsv3](/en-us/azure/virtual-machines/dv3-dsv3-series#dsv3-series)VMs.


The following example adds a node pool to

*myAKSCluster*with one node in*nodepool2*in the*myResourceGroup*:`az aks nodepool add --cluster-name myAKSCluster --resource-group myResourceGroup --name nodepool2 --os-sku AzureLinux --workload-runtime KataVmIsolation --node-vm-size Standard_D4s_v3`

Run the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command to enable pod sandboxing on the cluster.`az aks update --name myAKSCluster --resource-group myResourceGroup`


## Deploying your applications

With Pod Sandboxing, you can deploy a mix of "normal" pods that don't utilize the Kata runtime alongside Kata pods that do utilize the runtime. The main difference between the two, when deploying, lies in the fact that a Kata pod has the line `runtimeClassName: kata-vm-isolation`

in its spec.

### Deploy an application with the Kata runtime

To deploy a pod with the Kata runtime on your AKS cluster, perform the following steps.

Create a file named

*kata-app.yaml*to describe your kata pod, and then paste the following manifest.`kind: Pod apiVersion: v1 metadata: name: isolated-pod spec: runtimeClassName: kata-vm-isolation containers: - name: kata image: mcr.microsoft.com/aks/fundamental/base-ubuntu:v0.0.11 command: ["/bin/sh", "-ec", "while :; do echo '.'; sleep 5 ; done"]`

The value for

**runtimeClassNameSpec**is`kata-vm-isolation`

.Deploy the Kubernetes pod by running the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify your*kata-app.yaml*file:`kubectl apply -f kata-app.yaml`

The output of the command resembles the following example:

`pod/isolated-pod created`


## (Optional) Verify Kernel Isolation configuration

If you would like to verify the difference between the kernel of a Kata and non-Kata pod, you can spin up another workload that doesn't have the Kata runtime.

```
kind: Pod
apiVersion: v1
metadata:
name: normal-pod
spec:
containers:
- name: non-kata
image: mcr.microsoft.com/aks/fundamental/base-ubuntu:v0.0.11
command: ["/bin/sh", "-ec", "while :; do echo '.'; sleep 5 ; done"]
```


To access a container inside the AKS cluster, start a shell session by running the

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command. In this example, you're accessing the container inside*kata-pod*.`kubectl exec -it isolated-pod -- /bin/sh`

Kubectl connects to your cluster, runs

`/bin/sh`

inside the first container within`isolated-pod`

, and forwards your terminal's input and output streams to the container's process. You can also start a shell session to the container hosting the non-Kata pod to see the differences.After starting a shell session to the container from

*kata-pod*, you can run commands to verify that the*kata*container is running in a pod sandbox. Notice that it has a different kernel version compared to the non-Kata container outside the sandbox.To see the kernel version run the following command:

`uname -r`

The following example resembles output from the pod sandbox kernel:

`[user]/# uname -r 6.6.96.mshv1`

Start a shell session to the container from

*normal-pod*to verify the kernel output:`kubectl exec -it normal-pod -- /bin/bash`

To see the kernel version run the following command:

`uname -r`

The following example resembles output from the VM that's running

*normal-pod*, which is a different kernel than the Kata pod running within the pod sandbox:`6.6.100.mshv1-1.azl3`


## Cleanup

When you're finished evaluating this feature, to avoid Azure charges, clean up your unnecessary resources. If you deployed a new cluster as part of your evaluation or testing, you can delete the cluster using the [az aks delete](/en-us/cli/azure/aks#az-aks-delete) command.

```
az aks delete --resource-group myResourceGroup --name myAKSCluster
```


If you deployed Pod Sandboxing on an existing cluster, you can remove the pods using the [kubectl delete pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl get pods
kubectl delete pod <kata-pod-name>
```


## Next steps

- Learn more about
[Azure Dedicated hosts](use-azure-dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events. - To further explore Pod Sandboxing isolation and explore workload scenarios, try out the
[Pod Sandboxing labs](https://azure-samples.github.io/aks-labs/docs/security/pod-sandboxing-on-aks).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-storage -->

# Storage options for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Applications running in Azure Kubernetes Service (AKS) might need to store and retrieve data. While some application workloads can use local, fast storage on unneeded, emptied nodes, others require storage that persists on more regular data volumes within the Azure platform.

Multiple pods might need to:

- Share the same data volumes.
- Reattach data volumes if the pod is rescheduled on a different node.

You also might need to collect and store sensitive data or application configuration information into pods.

This article introduces the core concepts that provide storage to your applications in AKS:

## Default OS disk sizing

### Ephemeral OS disks

If you select a VM SKU that supports Ephemeral OS disks but don't specify an OS disk size, AKS by default provisions an Ephemeral OS disk with a size that scales according to the total temp storage of the VM SKU so long as the temp is *at least 128GiB*. For example, the `Standard_D8ds_v5`

SKU with a temp disk size of 300GiB will receive a 300GiB Ephemeral OS disk by default if the disk parameters are unspecified.

If you want to use the temp storage of the VM SKU, you need to specify the OS disk size during deployment, otherwise it's consumed by default.

Important

Default Ephemeral OS disk sizing is only used on new clusters or node pools where Ephemeral OS disks are supported and a default OS disk size isn't specified. The default OS disk size might impact the performance or cost of your cluster. You can't change the OS disk size after cluster or node pool creation. This default Ephemeral sizing affects clusters or node pools created in March 2025 or later.

### Managed OS disks

When you create a new cluster or add a new node pool to an existing cluster, the number for vCPUs by default determines the OS disk size. The number of vCPUs is based on the VM SKU. The following table lists the default OS disk size for each VM SKU:

| VM SKU Cores (vCPUs) | Default OS Disk Tier | Provisioned IOPS | Provisioned Throughput (Mbps) |
|---|---|---|---|
| 1 - 7 | P10/128G | 500 | 100 |
| 8 - 15 | P15/256G | 1100 | 125 |
| 16 - 63 | P20/512G | 2300 | 150 |
| 64+ | P30/1024G | 5000 | 200 |

Important

Default Managed OS disk sizing is only used on new clusters or node pools when Ephemeral OS disks aren't supported and a default OS disk size isn't specified. The default OS disk size might impact the performance or cost of your cluster. You can't change the OS disk size after cluster or node pool creation. We recommend a minimum disk size of 512G if ephemeral OS disk cannot be used. This default Managed sizing affects clusters or node pools created in July 2022 or later.

## Ephemeral OS disk

By default, Azure automatically replicates the operating system disk for a virtual machine to Azure Storage to avoid data loss when the VM is relocated to another host. However, since containers aren't designed to have local state persisted, this behavior offers limited value while providing some drawbacks. These drawbacks include, but aren't limited to, slower node provisioning and higher read/write latency.

By contrast, Ephemeral OS disks are stored only on the host machine, just like a temporary disk. With this configuration, you get lower read/write latency with faster node scaling and cluster upgrades. Therefore, we strongly **recommend using Ephemeral OS disks whenever possible**.

Note

When you don't explicitly request [Azure managed disks](/en-us/azure/virtual-machines/managed-disks-overview) for the OS, AKS defaults to ephemeral OS if possible for a given node pool configuration.

Size requirements and recommendations for ephemeral OS disks are available in the [Azure VM documentation](/en-us/azure/virtual-machines/ephemeral-os-disks). The following are some general sizing considerations:

If you chose to use the AKS default VM size

[Standard_DS2_v2](/en-us/azure/virtual-machines/dv2-dsv2-series#dsv2-series)SKU with the default OS disk size of 100 GiB, the default VM size supports ephemeral OS, but only has 86 GiB of cache size. This configuration would default to managed disks if you don't explicitly specify it. If you do request an ephemeral OS, you receive a validation error.If you request the same

[Standard_DS2_v2](/en-us/azure/virtual-machines/dv2-dsv2-series#dsv2-series)SKU with a 60-GiB OS disk, this configuration would default to ephemeral OS. The requested size of 60 GiB is smaller than the maximum cache size of 86 GiB.If you select the

[Standard_D8s_v3](/en-us/azure/virtual-machines/dv3-dsv3-series#dsv3-series)SKU with 100-GB OS disk, this VM size supports ephemeral OS and has 200 GiB of cache space. If you don't specify the OS disk type, the node pool would receive ephemeral OS by default.

The latest generation of VM series doesn't have a dedicated cache, but only temporary storage. For example, if you selected the [Standard_E2bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series) VM size with the default OS disk size of 100 GiB, it supports ephemeral OS disks, but only has 75 GB of temporary storage. This configuration would default to managed OS disks if you don't explicitly specify it. If you do request an ephemeral OS disk, you receive a validation error.

If you request the same

[Standard_E2bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series)VM size with a 60-GiB OS disk, this configuration defaults to ephemeral OS disks. The requested size of 60 GiB is smaller than the maximum temporary storage of 75 GiB.If you select

[Standard_E4bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series)SKU with 100-GiB OS disk, this VM size supports ephemeral OS and has 150 GiB of temporary storage. If you don't specify the OS disk type, by default Azure provisions an ephemeral OS disk to the node pool.

### Customer-managed keys

You can manage encryption for your ephemeral OS disk with your own keys on an AKS cluster. For more information, see [Use Customer Managed key with Azure disk on AKS](azure-disk-customer-managed-keys).

## Ephemeral NVMe data disks

Ephemeral NVMe data disks provide high-performance, low-latency storage directly attached to the physical host of your Azure VM. These disks are ideal for workloads that require fast, temporary storage for intermediate data processing, such as caching, scratch space, or high-throughput analytics.

Ephemeral NVMe data disks were initially available only on Azure VM L-series, E-series, and GPU VMs. With the introduction of Azure VM v6 and v7 generations, support for ephemeral NVMe data disks has expanded to a much wider range of VM sizes, including D-series, F-series, H-series, and more. NVMe disks deliver significantly higher IOPS and throughput compared to traditional HDD or SSD options. However, data stored on these disks is temporary and will be lost if the VM is deallocated or redeployed.

To simplify management and provisioning of ephemeral NVMe data disks in AKS, use [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction). Azure Container Storage can automatically detect and orchestrate NVMe data disks, allowing you to create and manage persistent volumes for your Kubernetes workloads with minimal configuration. This approach is recommended for scenarios where high-performance, temporary storage is required, such as:

- High-speed caching layers, such as datasets and checkpoints for AI training, or model files used for AI inference
- High-performance, self-hosted databases that include built-in replication and backup features
- Data-intensive analytics and processing pipelines that require fast, temporary storage
- Temporary scratch space for batch jobs

Important

Ephemeral NVMe data disks are not suitable for storing critical or persistent data. Ensure your application can tolerate data loss and that important data is stored on persistent volumes backed by Azure Disk, Azure Files, or other durable storage options.

For more information on using Azure Container Storage with ephemeral NVMe data disks, see [Use Azure Container Storage with AKS](/en-us/azure/storage/container-storage/use-container-storage-with-local-disk).

## Volumes

Kubernetes typically treats individual pods as ephemeral, disposable resources. Applications have different approaches available to them for using and persisting data. A *volume* represents a way to store, retrieve, and persist data across pods and through the application lifecycle.

Traditional volumes are created as Kubernetes resources backed by Azure Storage. You can manually create data volumes to be assigned to pods directly or have Kubernetes automatically create them. Data volumes can use: [Azure Disk](/en-us/azure/virtual-machines/disks-types), [Azure Files](/en-us/azure/storage/files/storage-files-planning), [Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-service-levels), or [Azure Blobs](/en-us/azure/storage/common/storage-account-overview).

Note

Depending on the VM SKU you're using, the Azure Disk CSI driver might have a per-node volume limit. For some high performance VMs (for example, 16 cores), the limit is 64 volumes per node. To identify the limit per VM SKU, review the **Max data disks** column for each VM SKU offered. For a list of VM SKUs offered and their corresponding detailed capacity limits, see [General purpose virtual machine sizes](/en-us/azure/virtual-machines/sizes-general).

To help determine best fit for your workload between Azure Files and Azure NetApp Files, review the information provided in the article [Azure Files and Azure NetApp Files comparison](/en-us/azure/storage/files/storage-files-netapp-comparison).

### Azure Disk

Use [Azure Disk](azure-disk-csi) to create a Kubernetes *DataDisk* resource. Disks types include:

- Premium SSDs (recommended for most workloads)
- Ultra disks
- Standard SSDs
- Standard HDDs

Tip

For most production and development workloads, use Premium SSDs.

Because an Azure Disk is mounted as *ReadWriteOnce*, it's only available to a single node. For storage volumes accessible by pods on multiple nodes simultaneously, use Azure Files.

### Azure Files

Use [Azure Files](azure-files-csi) to mount a Server Message Block (SMB) version 3.1.1 share or Network File System (NFS) version 4.1 share. Azure Files let you share data across multiple nodes and pods and can use:

- Azure Premium storage backed by high-performance SSDs
- Azure Standard storage backed by regular HDDs

### Azure NetApp Files

- Ultra Storage
- Premium Storage
- Standard Storage

### Azure Blob Storage

Use [Azure Blob Storage](azure-blob-csi) to create a blob storage container and mount it using the NFS v3.0 protocol or BlobFuse.

- Block blobs

### Volume types

Kubernetes volumes represent more than just a traditional disk for storing and retrieving information. Kubernetes volumes can also be used as a way to inject data into a pod for use by its containers.

Common volume types in Kubernetes include:

#### emptyDir

Commonly used as temporary space for a pod. All containers within a pod can access the data on the volume. Data written to this volume type persists only for the lifespan of the pod. Once you delete the pod, the volume is deleted. This volume typically uses the underlying local node disk storage, though it can also exist only in the node's memory.

#### secret

You can use *secret* volumes to inject sensitive data into pods, such as passwords.

- Create a secret using the Kubernetes API.
- Define your pod or deployment and request a specific secret.
- Secrets are only provided to nodes with a scheduled pod that requires them.
- The secret is stored in
*tmpfs*, not written to disk.

- When you delete the last pod on a node requiring a secret, the secret is deleted from the node's tmpfs.
- Secrets are stored within a given namespace and are only accessed by pods within the same namespace.


#### configMap

You can use *configMap* to inject key-value pair properties into pods, such as application configuration information. Define application configuration information as a Kubernetes resource, easily updated and applied to new instances of pods as they're deployed.

Like using a secret:

- Create a ConfigMap using the Kubernetes API.
- Request the ConfigMap when you define a pod or deployment.
- ConfigMaps are stored within a given namespace and are only accessed by pods within the same namespace.


## Persistent volumes

Volumes defined and created as part of the pod lifecycle only exist until you delete the pod. Pods often expect their storage to remain if a pod is rescheduled on a different host during a maintenance event, especially in StatefulSets. A *persistent volume* (PV) is a storage resource created and managed by the Kubernetes API that can exist beyond the lifetime of an individual pod.

You can use the following Azure Storage services to provide the persistent volume:

As noted in the [Volumes](#volumes) section, the choice of Azure Disks or Azure Files is often determined by the need for concurrent access to the data or the performance tier.

A cluster administrator can *statically* create a persistent volume, or a volume can be created *dynamically* by the Kubernetes API server. If a pod is scheduled and requests storage that is currently unavailable, Kubernetes can create the underlying Azure Disk or File storage and attach it to the pod. Dynamic provisioning uses a *storage class* to identify what type of resource needs to be created.

Important

Persistent volumes can't be shared by Windows and Linux pods due to differences in file system support between the two operating systems.

If you want a fully managed solution for block-level access to data, consider using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction) instead of CSI drivers. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes. Azure Container Storage supports Azure Disks, Ephemeral Disks, and Azure Elastic SAN (preview) as backing storage, offering flexibility and scalability for stateful applications running on Kubernetes clusters.

## Storage classes

To specify different tiers of storage, such as premium or standard, you can create a *storage class*.

A storage class also defines a *reclaim policy*. When you delete the persistent volume, the reclaim policy controls the behavior of the underlying Azure Storage resource. The underlying resource can either be deleted or kept for use with a future pod.

For clusters using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction), you'll see an additional storage class called `acstor-<storage-pool-name>`

. An internal storage class is also created.

For clusters using [Container Storage Interface (CSI) drivers](csi-storage-drivers), the following extra storage classes are created:

| Storage class | Description |
|---|---|
`managed-csi` |
Uses Azure Standard SSD locally redundant storage (LRS) to create a managed disk. The reclaim policy ensures that the underlying Azure Disk is deleted when the persistent volume that used it is deleted. The storage class also configures the persistent volumes to be expandable. You can edit the persistent volume claim to specify the new size. Effective starting with Kubernetes version 1.29, in Azure Kubernetes Service (AKS) clusters deployed across multiple availability zones, this storage class utilizes Azure Standard SSD zone-redundant storage (ZRS) to create managed disks. |
`managed-csi-premium` |
Uses Azure Premium locally redundant storage (LRS) to create a managed disk. The reclaim policy again ensures that the underlying Azure Disk is deleted when the persistent volume that used it is deleted. Similarly, this storage class allows for persistent volumes to be expanded. Effective starting with Kubernetes version 1.29, in Azure Kubernetes Service (AKS) clusters deployed across multiple availability zones, this storage class utilizes Azure Premium zone-redundant storage (ZRS) to create managed disks. |
`azurefile-csi` |
Uses Azure Standard storage to create an Azure file share. The reclaim policy ensures that the underlying Azure file share is deleted when the persistent volume that used it is deleted. |
`azurefile-csi-premium` |
Uses Azure Premium storage to create an Azure file share. The reclaim policy ensures that the underlying Azure file share is deleted when the persistent volume that used it is deleted. |
`azureblob-nfs-premium` |
Uses Azure Premium storage to create an Azure Blob storage container and connect using the NFS v3 protocol. The reclaim policy ensures that the underlying Azure Blob storage container is deleted when the persistent volume that used it is deleted. |
`azureblob-fuse-premium` |
Uses Azure Premium storage to create an Azure Blob storage container and connect using BlobFuse. The reclaim policy ensures that the underlying Azure Blob storage container is deleted when the persistent volume that used it is deleted. |

Unless you specify a storage class for a persistent volume, the default storage class is used. Ensure volumes use the appropriate storage you need when requesting persistent volumes.

Important

Starting with Kubernetes version 1.21, AKS uses CSI drivers by default, and CSI migration is enabled. While existing in-tree persistent volumes continue to function, starting with version 1.26, AKS will no longer support volumes created using in-tree driver and storage provisioned for files and disk.

The `default`

class will be the same as `managed-csi`

.

Effective starting with Kubernetes version 1.29, when you deploy Azure Kubernetes Service (AKS) clusters across multiple availability zones, AKS now utilizes zone-redundant storage (ZRS) to create managed disks within built-in storage classes. ZRS ensures synchronous replication of your Azure managed disks across multiple Azure availability zones in your chosen region. This redundancy strategy enhances the resilience of your applications and safeguards your data against datacenter failures.

However, it's important to note that zone-redundant storage (ZRS) comes at a higher cost compared to locally redundant storage (LRS). If cost optimization is a priority, you can create a new storage class with the `skuname`

parameter set to LRS. You can then use the new storage class in your Persistent Volume Claim (PVC).

You can create a storage class for other needs using `kubectl`

. The following example uses premium managed disks and specifies that the underlying Azure Disk should be *retained* when you delete the pod:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: managed-premium-retain
provisioner: disk.csi.azure.com
parameters:
skuName: Premium_ZRS
reclaimPolicy: Retain
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```


Note

AKS reconciles the default storage classes and will overwrite any changes you make to those storage classes.

For more information about storage classes, see [StorageClass in Kubernetes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

## Persistent volume claims

A persistent volume claim (PVC) requests storage of a particular storage class, access mode, and size. The Kubernetes API server can dynamically provision the underlying Azure Storage resource if no existing resource can fulfill the claim based on the defined storage class.

The pod definition includes the volume mount once the volume has been connected to the pod.

Once an available storage resource has been assigned to the pod requesting storage, the persistent volume is *bound* to a persistent volume claim. Persistent volumes are mapped to claims in a 1:1 mapping.

The following example YAML manifest shows a persistent volume claim that uses the *managed-premium* storage class and requests an Azure Disk that is *5Gi* in size:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: azure-managed-disk
spec:
accessModes:
- ReadWriteOnce
storageClassName: managed-premium-retain
resources:
requests:
storage: 5Gi
```


When you create a pod definition, you also specify:

- The persistent volume claim to request the desired storage.
- The
*volume mount*for your applications to read and write data.

The following example YAML manifest shows how the previous persistent volume claim can be used to mount a volume at */mnt/azure*:

```
kind: Pod
apiVersion: v1
metadata:
name: nginx
spec:
containers:
- name: myfrontend
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
volumeMounts:
- mountPath: "/mnt/azure"
name: volume
volumes:
- name: volume
persistentVolumeClaim:
claimName: azure-managed-disk
```


For mounting a volume in a Windows container, specify the drive letter and path. For example:

```
...
volumeMounts:
- mountPath: "d:"
name: volume
- mountPath: "c:\k"
name: k-dir
...
```


## Next steps

For associated best practices, see [Best practices for storage and backups in AKS](operator-best-practices-storage) and [AKS storage considerations](/en-us/azure/cloud-adoption-framework/scenarios/app-platform/aks/storage).

For more information on Azure Container Storage, see the following articles:

For more information on using CSI drivers, see the following articles:

[Container Storage Interface (CSI) drivers for Azure Disk, Azure Files, and Azure Blob storage on Azure Kubernetes Service](csi-storage-drivers)[Use Azure Disk CSI driver in Azure Kubernetes Service](azure-disk-csi)[Use Azure Files CSI driver in Azure Kubernetes Service](azure-files-csi)[Use Azure Blob storage CSI driver in Azure Kubernetes Service](azure-blob-csi)[Configure Azure NetApp Files with Azure Kubernetes Service](azure-netapp-files)

For more information on core Kubernetes and AKS concepts, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubelet-logs -->

# Get kubelet logs from Azure Kubernetes Service cluster nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might need to review logs to troubleshoot a problem in your Azure Kubernetes Service (AKS) cluster. You can use tools in the Azure portal to view logs for AKS [main components](monitor-aks-reference#resource-logs) and [cluster containers](/en-us/azure/azure-monitor/containers/container-insights-overview). Occasionally, you might need to get *kubelet* logs from AKS nodes to help you troubleshoot an issue.

This article shows you how to use `journalctl`

to view kubelet logs on an AKS node.

Alternatively, you can collect kubelet logs by using the [syslog collection feature in Container insights in Azure Monitor](https://aka.ms/CISyslog).

## Before you begin

This article assumes that you have an existing AKS cluster. If you need an AKS cluster, create one by using the [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

## Connect to your AKS cluster

To interact with your AKS cluster, first get the cluster credentials by using the Azure CLI:

```
export RESOURCE_GROUP_NAME="<ResourceGroupName>"
export AKS_CLUSTER_NAME="<AKSClusterName>"
az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $AKS_CLUSTER_NAME
```


This command configures kubectl to use the credentials for your AKS cluster.

## Use the kubectl raw command

You can quickly view any node's kubelet logs by using the following command:

```
export NODE_NAME="aks-agentpool-xxxxxxx-0"
kubectl get --raw "/api/v1/nodes/$NODE_NAME/proxy/logs/messages" | grep kubelet
```


Results:

```
I0508 12:26:17.905042 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:27.943494 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:28.920125 8672 server.go:796] GET /stats/summary: (10.370874ms) 200 [[Ruby] 10.244.0.x:52492]
I0508 12:26:37.964650 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
...
```


## Create an SSH connection

You must create a Secure Shell Protocol (SSH) connection with the node you need to view kubelet logs for. To create this connection, complete the steps that are described in [SSH into AKS cluster nodes](ssh).

## Get kubelet logs

After you connect to the node by using `kubectl debug`

, run the following command to pull the kubelet logs:

```
chroot /host
journalctl -u kubelet -o cat
```


Note

For Windows nodes, the log data is in `C:\k`

and can be viewed by using the `more`

command:

```
more C:\k\kubelet.log
```


The following example output shows kubelet log data:

```
I0508 12:26:17.905042 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:27.943494 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:28.920125 8672 server.go:796] GET /stats/summary: (10.370874ms) 200 [[Ruby] 10.244.0.x:52292]
I0508 12:26:37.964650 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:47.996449 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:58.019746 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:05.107680 8672 server.go:796] GET /stats/summary/: (24.853838ms) 200 [[Go-http-client/1.1] 10.244.0.x:44660]
I0508 12:27:08.041736 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:18.068505 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:28.094889 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:38.121346 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:44.015205 8672 server.go:796] GET /stats/summary: (30.236824ms) 200 [[Ruby] 10.244.0.x:52588]
I0508 12:27:48.145640 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:58.178534 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:05.040375 8672 server.go:796] GET /stats/summary/: (27.78503ms) 200 [[Go-http-client/1.1] 10.244.0.x:44660]
I0508 12:28:08.214158 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:18.242160 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:28.274408 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:38.296074 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:48.321952 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:58.344656 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing-nginx-prometheus -->

# Monitor the ingress-nginx controller metrics in the application routing add-on with Prometheus and Grafana

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The ingress-nginx controller in the application routing add-on exposes many metrics for requests, the nginx process, and the controller that can be helpful in analyzing the performance and usage of your application.

The application routing add-on exposes the Prometheus metrics endpoint at `/metrics`

on port 10254 and a private Service `nginx-metrics`

.

## Prerequisites

- An Azure Kubernetes Service (AKS) cluster with the
[application routing add-on enabled](/en-us/azure/aks/app-routing). - A Prometheus instance, such as Azure Monitor managed service for Prometheus.

## Validating the metrics endpoint

To validate the metrics are being collected, you can set up a port forward from a local port to port 10254 on the `nginx-metrics`

service.

```
kubectl port-forward -n app-routing-system service/nginx-metrics :10254
```


```
Forwarding from 127.0.0.1:43307 -> 10254
Forwarding from [::1]:43307 -> 10254
```


Note the local port (`43307`

in this case) and open http://localhost:43307/metrics in your browser. You should see the ingress-nginx controller metrics loading.

You can now terminate the `port-forward`

process to close the forwarding.

## Configuring Azure Monitor managed service for Prometheus

Azure Monitor managed service for Prometheus is a fully managed Prometheus-compatible service that supports industry standard features such as PromQL, Grafana dashboards, and Prometheus alerts. This service requires configuring the metrics addon for the Azure Monitor agent, which sends data to Prometheus. If your cluster isn't configured with the add-on, you can follow this article to configure your Azure Kubernetes Service (AKS) cluster to send data to Azure Monitor managed service for Prometheus.

### Enable Service Monitor based scraping

Once your cluster is updated with the Azure Monitor agent, you need to configure the agent to enable scraping the metrics endpoint. You can [create a Pod or a Service Monitor](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-crd) to accomplish this.

The following creates a Service Monitor scrape metrics from the ingress-nginx controller deployed by the application routing add-on.

```
kubectl apply -f - <<EOF
apiVersion: azmonitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
name: nginx-monitor
namespace: app-routing-system
spec:
labelLimit: 63
labelNameLengthLimit: 511
labelValueLengthLimit: 1023
selector:
matchLabels:
app.kubernetes.io/component: ingress-controller
app.kubernetes.io/managed-by: aks-app-routing-operator
app.kubernetes.io/name: nginx
endpoints:
- port: prometheus
EOF
```


In a few minutes, the `ama-metrics`

pods in the `kube-system`

namespace should restart and pick up the new configuration.

## Review visualization of metrics in Azure Managed Grafana

Now that you have Azure Monitor managed service for Prometheus and Azure Managed Grafana configured, you should [access your Managed Grafana instance](/en-us/azure/managed-grafana/quickstart-managed-grafana-portal#access-your-managed-grafana-instance).

There are two [official ingress-nginx dashboards](https://github.com/kubernetes/ingress-nginx/tree/main/deploy/grafana/dashboards) dashboards that you can download and import into your Grafana instance:

- Ingress-nginx controller dashboard
- Request handling performance dashboard

### Ingress-nginx controller dashboard

This dashboard gives you visibility of request volume, connections, success rates, config reloads and configs out of sync. You can also use it to view the network IO pressure, memory and CPU use of the ingress controller. Finally, it also shows the P50, P95, and P99 percentile response times of your ingresses and their throughput.

You can download this dashboard from [GitHub](https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/grafana/dashboards/nginx.json).

### Request handling performance dashboard

This dashboard gives you visibility into the request handling performance of the different ingress upstream destinations, which are your applications' endpoints that the ingress controller is forwarding traffic to. It shows the P50, P95 and P99 percentile of total request and upstream response times. You can also view aggregates of request errors and latency. Use this dashboard to review and improve the performance and scalability of your applications.

You can download this dashboard from [GitHub](https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/grafana/dashboards/request-handling-performance.json).

### Importing a dashboard

To import a Grafana dashboard, expand the left menu and click on **Import** under Dashboards.

Then upload the desired dashboard file and click on **Load**.

## Next steps

- You can configure scaling your workloads using ingress metrics scraped with Prometheus using
[Kubernetes Event Driven Autoscaler (KEDA)](/en-us/azure/aks/keda-about). Learn more about[integrating KEDA with AKS](/en-us/azure/azure-monitor/essentials/integrate-keda#scalers). - Create and run a load test with
[Azure Load Testing](/en-us/azure/load-testing/quickstart-create-and-run-load-test)to test workload performance and optimize the scalability of your applications.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/certificate-rotation -->

# Certificate rotation in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) uses certificates for authentication with many of its components. You need to periodically rotate those certificates for security or policy reasons. This article shows you how certificate rotation works in your AKS cluster.

## Prerequisites

This article requires the Azure CLI version 2.0.77 or later. Check your version using the

`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Configure

`kubectl`

to connect to your AKS cluster using thecommand:`az aks get-credentials`

`az aks get-credentials --resource-group <resource-group> --name <cluster-name>`


## AKS certificates, Certificate Authorities, and Service Accounts

AKS generates and uses the following certificates, Certificate Authorities (CA), and Service Accounts (SA):

- The AKS API server creates a CA called the
*Cluster CA*, which signs certificates for one-way communication from the API server to kubelet. - Each kubelet creates a Certificate Signing Request (CSR), which the Cluster CA signs, for communication from the kubelet to the API server.
- The API aggregator uses the Cluster CA to issue certificates for communication with other APIs. The API aggregator can also have its own CA for issuing those certificates, but it currently uses the Cluster CA.
- Each agent node uses an SA token, which the Cluster CA signs.
- The
`kubectl`

client has a certificate for communicating with the AKS cluster.

Microsoft maintains all certificates mentioned in this section, except for the cluster certificate.

## Certificate expiration dates

Important

The expiration date for your certificates depends on when your AKS cluster was created:

**AKS clusters created**have certificates that expire after two years.*before*May 2019**AKS clusters created**have Cluster CA certificates that expire after 30 years.*after*May 2019

You can verify when your cluster was created using the `kubectl get nodes`

command, which shows you the `Age`

of your agent nodes.

## Check cluster certificate expiration date

Check the expiration date of the cluster certificate using the

`kubectl config view`

command.`kubectl config view --raw -o jsonpath="{.clusters[?(@.name == '')].cluster.certificate-authority-data}" | base64 -d | openssl x509 -text | grep -A2 Validity`


## Check API server certificate expiration date

Check the expiration date of the API server certificate using the following

`curl`

command:`curl https://{apiserver-fqdn} -k -v 2>&1 | grep expire`


## Check virtual machine (VM) agent node certificate expiration date

Check the expiration date of the VM agent node certificate using the

command.`az vm run-command invoke`

**Key parameters in this command**: -`--resource-group <node-resource-group>`

: The resource group that contains the VM agent node. -`--name <vm-name>`

: The name of the VM agent node. -`--scripts "openssl x509 -in /etc/kubernetes/certs/apiserver.crt -noout -enddate"`

: The script that retrieves the expiration date of the API server certificate located at`/etc/kubernetes/certs/apiserver.crt`

.`az vm run-command invoke --resource-group <node-resource-group> --name <vm-name> --command-id RunShellScript --query 'value[0].message' -otsv --scripts "openssl x509 -in /etc/kubernetes/certs/apiserver.crt -noout -enddate"`


## Check certificate expiration for the Azure Virtual Machine Scale Set agent node

Check the expiration date of the Azure Virtual Machine Scale Set agent node certificate using the

command.`az vmss run-command invoke`

**Key parameters in this command**: -`--resource-group <node-resource-group>`

: The resource group that contains the Azure Virtual Machine Scale Set agent node. -`--name <vmss-name>`

: The name of the Azure Virtual Machine Scale Set. -`--instance-id 1`

: The instance ID of the Azure Virtual Machine Scale Set agent node. -`--scripts "openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -noout -enddate"`

: The script that retrieves the expiration date of the kubelet client certificate located at`/var/lib/kubelet/pki/kubelet-client-current.pem`

.`az vmss run-command invoke --resource-group <node-resource-group> --name <vmss-name> --command-id RunShellScript --instance-id 1 --scripts "openssl x509 -in /var/lib/kubelet/pki/kubelet-client-current.pem -noout -enddate" --query "value[0].message"`


## Manually rotate your cluster certificates

Rotate all certificates, CAs, and SAs on your cluster using the

command.`az aks rotate-certs`

`az aks rotate-certs --resource-group <resource-group> --name <cluster-name>`

Important

The

command recreates all of your agent nodes, Azure Virtual Machine Scale Sets, and disks. This command can also cause up to`az aks rotate-certs`

*30 minutes of downtime*for your AKS cluster. If the command fails before completing, use the [`az aks show`

][az-aks-show] command to verify the status of the cluster is`Certificate Rotating`

. If the cluster is in a failed state, rerun thecommand to rotate your certificates again.`az aks rotate-certs`

Verify the old certificates are no longer valid using any

`kubectl`

command. The following example uses the`kubectl get nodes`

command:`kubectl get nodes`

If you didn't update the certificates used by

`kubectl`

, you see an error similar to the following example output:`Unable to connect to the server: x509: certificate signed by unknown authority (possibly because of "crypto/rsa: verification error" while trying to verify candidate authority certificate "ca")`

Update the certificate used by

`kubectl`

using thecommand with the`az aks get-credentials`

`--overwrite-existing`

flag.`az aks get-credentials --resource-group <resource-group> --name <cluster-name> --overwrite-existing`

Verify the certificates are updated using the

command.`kubectl get`

`kubectl get nodes`


If you have any services that run on top of AKS, you might need to update their certificates as well.

## Rotate the kubelet serving certificate

When you rotate the kubelet serving certificate, AKS allows kubelet server Transport Layer Security (TLS) Bootstrapping for both bootstrapping and rotating serving certificates signed by the Cluster CA.

### Limitations for kubelet serving certificate rotation

- Supported on Kubernetes version 1.27 and above.
- Not supported when the node pool is using a node pool snapshot based on any node image older than
`202501.12.0`

. - You can't manually enable this feature. Kubelet serving certificate rotation is enabled by default on existing node pools when they perform their first upgrade to any Kubernetes version 1.27 or higher. Kubelet serving certificate rotation is enabled by default on new node pools using Kubernetes version 1.27 or higher. To see if kubelet serving certificate rotation is enabled in your region, check the
[AKS releases](https://github.com/Azure/AKS/releases).

## Verify kubelet serving certificate rotation is enabled

Each node with the feature enabled is automatically given the label `kubernetes.azure.com/kubelet-serving-ca=cluster`

.

Verify the labels are set using the

`kubectl get nodes -L kubernetes.azure.com/kubelet-serving-ca`

command.`kubectl get nodes -L kubernetes.azure.com/kubelet-serving-ca`

The output should show the label

`kubernetes.azure.com/kubelet-serving-ca`

with the value`cluster`

for each agent node.

## Verify kubelet TLS Bootstrapping is working

Verify the bootstrapping process is taking place using the

command.`kubectl get`

`kubectl get csr --field-selector=spec.signerName=kubernetes.io/kubelet-serving`

In the output, all serving CSRs should be in the

`Approved,Issued`

state, which indicates the CSR was approved and issued a signed certificate. Serving CSRs have a signer name of`kubernetes.io/kubelet-serving`

. For example:`NAME AGE SIGNERNAME REQUESTOR REQUESTEDDURATION CONDITION csr-1ab2c 113s kubernetes.io/kube-apiserver-client-kubelet system:bootstrap:uoxr9r none Approved,Issued csr-defgh 111s kubernetes.io/kubelet-serving system:node:akswinp7000000 none Approved,Issued csr-ij3kl 46m kubernetes.io/kubelet-serving system:node:akswinp6000000 none Approved,Issued csr-mn4op 46m kubernetes.io/kube-apiserver-client-kubelet system:bootstrap:ho7zyu none Approved,Issued`


## Verify kubelet is using a certificate obtained from server TLS Bootstrapping

Confirm the kubelet is using a serving certificate signed by the Cluster CA using the

command.`kubectl debug`

`kubectl debug node/<node> -ti --image=mcr.microsoft.com/azurelinux/base/core:3.0 -- ls -l /host/var/lib/kubelet/kubelet-server-current.pem`

If a

`kubelet-server-current.pem`

symlink exists, then the kubelet bootstrapped/rotated its own serving certificate, and the Cluster CA signed it.

## Disable kubelet serving certificate rotation

Disable kubelet serving certificate rotation by updating the node pool using the

command with the`az aks nodepool update`

`aks-disable-kubelet-serving-certificate-rotation=true`

tag.`az aks nodepool update --cluster-name <cluster-name> --resource-group <resource-group> --name <node-pool-name> --tags aks-disable-kubelet-serving-certificate-rotation=true`


- Reimage your nodes using a
[node image upgrade](node-image-upgrade)or by scaling the pool to*zero*instances and then back up to the desired value.

## Certificate autorotation

Keep the following considerations in mind when using certificate autorotation:

- If you have an existing cluster, you have to upgrade that cluster to enable certificate autorotation.
- Don't disable TLS Bootstrap to keep certificate autorotation enabled.
- If the cluster is in a stopped state during certificate autorotation, only the control plane certificates are rotated. In this case, you should recreate the node pool after certificate rotation to initiate the node pool certificate rotation.
- For any AKS clusters created or upgraded after March 2022, AKS automatically rotates non-CA certificates on both the control plane and agent nodes within 80% of the client certificate valid time before they expire with no downtime for the cluster.

## Verify TLS Bootstrapping is enabled on current agent node pool

Verify your cluster has TLS Bootstrapping enabled by browsing to one to the following paths:

**On a Linux node**:`/var/lib/kubelet/bootstrap-kubeconfig`

or`/host/var/lib/kubelet/bootstrap-kubeconfig`

**On a Windows node**:`C:\k\bootstrap-config`


For more information, see

[Connect to Azure Kubernetes Service (AKS) cluster nodes for maintenance or troubleshooting](node-access).Note

The file path might change as Kubernetes versions evolve.

Once a region is configured, create a new cluster or upgrade an existing cluster to set certificate autorotation for the cluster certificate. You need to upgrade the control plane and node pool to enable this feature.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-fqdn-filtering-policies -->

# Set up FQDN filtering feature for Container Network Security in Advanced Container Networking Services

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to set up Advanced Container Networking Services with Container Network Security feature in AKS clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.71.0. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations:

- Wildcard FQDN policies are partially supported. This means you can create policies that match specific patterns with a leading wildcard (for example,
*.example.com), but you can't use a universal wildcard (*) to match all domains on the field`spec.egress.toPorts.rules.dns.matchPattern`


Supported Pattern:

`*.example.com`

- This allows traffic to all subdomains under example.com.`app*.example.com`

- This rule is more specific and only allows traffic to subdomains that start with "app" under example.comUnsupported Pattern

`*`

This attempt to match any domain name, which isn't supported.

- FQDN filtering is currently not supported with node-local DNS.
- Kubernetes service names aren't supported.
- Other L7 policies aren't supported.
- FQDN pods might exhibit performance degradation when handling more than 1,000 requests per second.
- If Advanced Container Networking Services(ACNS) security is disabled, FQDN and L7 policies (HTTP, HTTPS, Kafka, and gRPC) will be blocked.
- Alpine-based container images might encounter DNS resolution issues when used with Cilium Network Policies. This is due to musl libc's limited search domain iteration. To work around this, explicitly define all search domains in the Network Policy's DNS rules using wildcard patterns, like the below example

```
rules:
dns:
- matchPattern: "*.example.com"
- matchPattern: "*.example.com.*.*"
- matchPattern: "*.example.com.*.*.*"
- matchPattern: "*.example.com.*.*.*.*"
- matchPattern: "*.example.com.*.*.*.*.*"
- toFQDNs:
- matchPattern: "*.example.com"
```


### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability).**Container Network Security:**Offers security features like Fully Qualified Domain Name (FQDN) filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security).

```
# Set an environment variable for the AKS cluster name. Make sure to replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location eastus \
--network-plugin azure \
--network-dataplane cilium \
--node-count 2 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features which includes [Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security)feature

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


## Get cluster credentials

Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Test connectivity with a policy

This section demonstrates how to observe a policy being enforced through the Cilium Agent. A DNS request is made to an allowed FQDN and another case where it's blocked.

Create a file named `demo-policy.yaml`

and paste the following YAML manifest:

Note

The field `spec.egress.toPorts.rules.dns.matchPattern`

is **mandatory** when using to FQDNs in a policy. This section tells Cilium to inspect DNS queries and match them against specified patterns. Without this section, Cilium only allows the DNS traffic and not inspect its contents to learn which IPs are associated with the FQDNs. As a result, connections to those IPs (i.e., non-DNS traffic) are blocked because Cilium can't associate them with the allowed domain.

Make sure to check the [limitations](#limitations) section first.

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: "allow-bing-fqdn"
spec:
endpointSelector:
matchLabels:
app: demo-container
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: ANY
rules:
dns:
- matchPattern: "*.bing.com"
- toFQDNs:
- matchPattern: "*.bing.com"
```


Specify the name of your YAML manifest and apply it by using [kubectl apply][kubectl-apply]:

```
kubectl create ns demo
kubectl apply -f demo-policy.yaml -n demo
```


### Create a demo pod

Create a `client`

pod running Bash:

```
kubectl run -it client -n demo --image=k8s.gcr.io/e2e-test-images/agnhost:2.43 --labels="app=demo-container" --command -- bash
```


A shell with utilities for testing FQDN should open with the following output:

```
If you don't see a command prompt, try pressing enter.
bash-5.0#
```


In a separate window, run the following command to get the node of the running pod.

```
kubectl get po -n demo --sort-by="{spec.nodeName}" -o wide
```


The output should look similar to the following example:

```
NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES
client 1/1 Running 0 5m50s 192.168.0.139 aks-nodepool1-22058664-vmss000001 <none> <none>
```


The pod is running on a node named `aks-nodepool1-22058664-vmss000001`

. Obtain the Cilium Agent instance running on that node:

```
kubectl get po -n kube-system -o wide --field-selector spec.nodeName="aks-nodepool1-22058664-vmss000001" | grep "cilium"
```


The expected `cilium-s4x24`

should be in the output.

```
cilium-s4x24 1/1 Running 0 47m 10.224.0.4 aks-nodepool1-22058664-vmss000001 <none> <none>
```


### Inspect a Cilium Agent

Use the `cilium`

CLI to monitor traffic being blocked.

```
kubectl exec -it -n kube-system cilium-s4x24 -- sh
```


```
Defaulted container "cilium-agent" out of: cilium-agent, install-cni-binaries (init), mount-cgroup (init), apply-sysctl-overwrites (init), mount-bpf-fs (init), clean-cilium-state (init), block-wireserver (init)
#
```


Inside this shell, run `cilium monitor -t drop`

:

```
Listening for events on 2 CPUs with 64x4096 of shared memory
Press Ctrl-C to quit
time="2024-10-08T17:48:27Z" level=info msg="Initializing dissection cache..." subsys=monitor
```


### Verify policy

From the first shell, create a request to the allowed FQDN, `*.bing.com`

, as specified by the policy. This request should succeed and allowed by the agent.

```
./agnhost connect www.bing.com:80
```


Then create another request to an FQDN expected to be blocked:

```
./agnhost connect www.example.com:80
```


Cilium Agent blocked the request with the output:

```
xx drop (Policy denied) flow 0xfddd76f6 to endpoint 0, ifindex 29, file bpf_lxc.c:1274, , identity 48447->world: 192.168.0.149:45830 -> 93.184.215.14:80 tcp SYN
```


### Supported by CiliumClusterwideNetworkPolicy(CCNP)

`CiliumClusterwideNetworkPolicy`

supports FQDN filtering.

Note

[Namespace specific information](https://docs.cilium.io/en/latest/security/policy/kubernetes/#namespace-specific-information) such as `io.kubernetes.pod.namespace`

is only supported in cluster-wide policies.

```
apiVersion: cilium.io/v2
kind: CiliumClusterwideNetworkPolicy
metadata:
name: allow-bing-fqdn
spec:
endpointSelector: {} # Applies to all pods in the cluster
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: ANY
rules:
dns:
- matchPattern: "*.bing.com"
- toFQDNs:
- matchPattern: "*.bing.com"
```


## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to install and enable security features with Advanced Container Networking Services for your AKS cluster.

- For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see
[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/understand-aks-costs -->

# Understand Azure Kubernetes Service (AKS) usage and costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides resources you can use to better understand your Azure Kubernetes Service (AKS) usage and costs and identify cost optimization opportunities.

## About cost analysis

[Microsoft Cost Management](/en-us/azure/cost-management-billing/costs/reporting-get-started) is a suite of FinOps tools that help you analyze, monitor, and optimize your cloud costs. It's available for Azure customers with access to a billing account, subscription, resource group, or management group. For more information, see [What is Microsoft Cost Management?](/en-us/azure/cost-management-billing/costs/overview-cost-management)

[Cost analysis](/en-us/azure/cost-management-billing/costs/reporting-get-started#cost-analysis) is a feature of Cost Management that helps you understand your costs and usage. It provides insights into how your resources are being used and helps you identify opportunities to reduce costs. For more information, see [Start analyzing costs in Azure](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis).

## Cost analysis resources

### Cost analysis add-on for AKS

The cost analysis add-on for AKS allows you to view comprehensive cost data scoped to Kubernetes constructs, such as clusters and namespaces, and Azure Compute, Network, and Storage resources. Enable it on your AKS cluster by following the steps in [Enable the Azure Kubernetes Service (AKS) cost analysis add-on](cost-analysis). To learn more about viewing the cost data, see [View Kubernetes costs](/en-us/azure/cost-management-billing/costs/view-kubernetes-costs).

### Azure Cost Optimization workbook

The [Azure Cost Optimization workbook](/en-us/azure/advisor/advisor-workbook-cost-optimization) provides a comprehensive view of your Azure costs and recommendations for optimizing them. For more information, see [Cost Optimization workbook](/en-us/azure/advisor/advisor-workbook-cost-optimization).

### Azure Orphaned Resources workbook

The [Azure Orphaned Resources workbook](https://github.com/dolevshor/azure-orphan-resources) helps you identify and manage unused resources in your Azure environment. For more information, see [Orphaned Resources workbook](https://techcommunity.microsoft.com/blog/fasttrackforazureblog/azure-orphan-resources/3492198).

## Next steps

For more information about managing your AKS costs, see [Best practices for cost optimization in Azure Kubernetes Service (AKS)](best-practices-cost).

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
<!-- Source: N/A -->

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
