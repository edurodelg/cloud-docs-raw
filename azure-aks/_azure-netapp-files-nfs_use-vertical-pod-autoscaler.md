---
merged_at: 2026-01-25T12:25:33.968322
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: azure-netapp-files-nfs.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-nfs -->

# Provision Azure NetApp Files NFS volumes for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After you [configure Azure NetApp Files for Azure Kubernetes Service](azure-netapp-files), you can provision Azure NetApp Files volumes for Azure Kubernetes Service.

Azure NetApp Files supports volumes using NFS (NFSv3 or NFSv4.1), [SMB](azure-netapp-files-smb), or [dual-protocol](azure-netapp-files-dual-protocol) (NFSv3 and SMB, or NFSv4.1 and SMB).

- This article describes details for provisioning NFS volumes statically or dynamically.
- For information about provisioning SMB volumes statically or dynamically, see
[Provision Azure NetApp Files SMB volumes for Azure Kubernetes Service](azure-netapp-files-smb). - For information about provisioning dual-protocol volumes statically, see
[Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol)

## Statically configure for applications that use NFS volumes

This section describes how to create an NFS volume on Azure NetApp Files and expose the volume statically to Kubernetes. It also describes how to use the volume with a containerized application.

### Create an NFS volume

Define variables for later usage. Replace

*myresourcegroup*,*mylocation*,*myaccountname*,*mypool1*,*premium*,*myfilepath*,*myvolsize*,*myvolname*,*vnetid*, and*anfSubnetID*with an appropriate value from your account and environment. The*filepath*must be unique within all ANF accounts.`RESOURCE_GROUP="myresourcegroup" LOCATION="mylocation" ANF_ACCOUNT_NAME="myaccountname" POOL_NAME="mypool1" SERVICE_LEVEL="premium" # Valid values are Standard, Premium, and Ultra UNIQUE_FILE_PATH="myfilepath" VOLUME_SIZE_GIB="myvolsize" VOLUME_NAME="myvolname" VNET_ID="vnetId" SUBNET_ID="anfSubnetId"`

Create a volume using the

command. For more information, see`az netappfiles volume create`

[Create an NFS volume for Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-create-volumes).`az netappfiles volume create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --name "$VOLUME_NAME" \ --service-level $SERVICE_LEVEL \ --vnet $VNET_ID \ --subnet $SUBNET_ID \ --usage-threshold $VOLUME_SIZE_GIB \ --file-path $UNIQUE_FILE_PATH \ --protocol-types NFSv3`


### Create the persistent volume

List the details of your volume using

command. Replace the variables with appropriate values from your Azure NetApp Files account and environment if not defined in a previous step.`az netappfiles volume show`

`az netappfiles volume show \ --resource-group $RESOURCE_GROUP \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --volume-name "$VOLUME_NAME -o JSON`

The following output is an example of the above command executed with real values.

`{ ... "creationToken": "myfilepath2", ... "mountTargets": [ { ... "ipAddress": "10.0.0.4", ... } ], ... }`

Create a file named

`pv-nfs.yaml`

and copy in the following YAML. Make sure the server matches the output IP address from Step 1, and the path matches the output from`creationToken`

above. The capacity must also match the volume size from the step above.`apiVersion: v1 kind: PersistentVolume metadata: name: pv-nfs spec: capacity: storage: 100Gi accessModes: - ReadWriteMany mountOptions: - vers=3 nfs: server: 10.0.0.4 path: /myfilepath2`

Create the persistent volume using the

command:`kubectl apply`

`kubectl apply -f pv-nfs.yaml`

Verify the status of the persistent volume is

*Available*by using thecommand:`kubectl describe`

`kubectl describe pv pv-nfs`


### Create a persistent volume claim

Create a file named

`pvc-nfs.yaml`

and copy in the following YAML. This manifest creates a PVC named`pvc-nfs`

for 100Gi storage and`ReadWriteMany`

access mode, matching the PV you created.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: pvc-nfs spec: accessModes: - ReadWriteMany storageClassName: "" resources: requests: storage: 100Gi`

Create the persistent volume claim using the

command:`kubectl apply`

`kubectl apply -f pvc-nfs.yaml`

Verify the

*Status*of the persistent volume claim is*Bound*by using thecommand:`kubectl describe`

`kubectl describe pvc pvc-nfs`


### Mount with a pod

Create a file named

`nginx-nfs.yaml`

and copy in the following YAML. This manifest defines a`nginx`

pod that uses the persistent volume claim.`kind: Pod apiVersion: v1 metadata: name: nginx-nfs spec: containers: - image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine name: nginx-nfs command: - "/bin/sh" - "-c" - while true; do echo $(date) >> /mnt/azure/outfile; sleep 1; done volumeMounts: - name: disk01 mountPath: /mnt/azure volumes: - name: disk01 persistentVolumeClaim: claimName: pvc-nfs`

Create the pod using the

command:`kubectl apply`

`kubectl apply -f nginx-nfs.yaml`

Verify the pod is

*Running*by using thecommand:`kubectl describe`

`kubectl describe pod nginx-nfs`

Verify your volume has been mounted on the pod by using

to connect to the pod, and then use`kubectl exec`

`df -h`

to check if the volume is mounted.`kubectl exec -it nginx-nfs -- sh`

`/ # df -h Filesystem Size Used Avail Use% Mounted on ... 10.0.0.4:/myfilepath2 100T 384K 100T 1% /mnt/azure ...`


## Dynamically configure for applications that use NFS volumes

Trident may be used to dynamically provision NFS or SMB files on Azure NetApp Files. Dynamically provisioned SMB volumes are only supported with windows worker nodes.

This section describes how to use Trident to dynamically create an NFS volume on Azure NetApp Files and automatically mount it to a containerized application.

### Install Trident

To dynamically provision NFS volumes, you need to install Trident. Trident is NetApp's dynamic storage provisioner that is purpose-built for Kubernetes. Simplify the consumption of storage for Kubernetes applications using Trident's industry-standard [Container Storage Interface (CSI)](https://kubernetes-csi.github.io/docs/) driver. Trident deploys on Kubernetes clusters as pods and provides dynamic storage orchestration services for your Kubernetes workloads.

Trident can be installed using the Trident operator (manually or using [Helm](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-operator.html)) or [ tridentctl](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-tridentctl.html). To learn more about these installation methods and how they work, see the

[Trident Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html).

#### Install Trident using Helm

[Helm](https://helm.sh/) must be installed on your workstation to install Trident using this method. For other methods of installing Trident, see the [Trident Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html).

To install Trident using Helm for a cluster with only Linux worker nodes, run the following commands:

`helm repo add netapp-trident https://netapp.github.io/trident-helm-chart helm install trident netapp-trident/trident-operator --version 23.04.0 --create-namespace --namespace trident`

The output of the command resembles the following example:

`NAME: trident LAST DEPLOYED: Fri May 5 13:55:36 2023 NAMESPACE: trident STATUS: deployed REVISION: 1 TEST SUITE: None NOTES: Thank you for installing trident-operator, which will deploy and manage NetApp's Trident CSI storage provisioner for Kubernetes. Your release is named 'trident' and is installed into the 'trident' namespace. Please note that there must be only one instance of Trident (and trident-operator) in a Kubernetes cluster. To configure Trident to manage storage resources, you will need a copy of tridentctl, which is available in pre-packaged Trident releases. You may find all Trident releases and source code online at https://github.com/NetApp/trident. To learn more about the release, try: $ helm status trident $ helm get all trident`

To confirm Trident was installed successfully, run the following

command:`kubectl describe`

`kubectl describe torc trident`

The output of the command resembles the following example:

`Name: trident Namespace: Labels: app.kubernetes.io/managed-by=Helm Annotations: meta.helm.sh/release-name: trident meta.helm.sh/release-namespace: trident API Version: trident.netapp.io/v1 Kind: TridentOrchestrator Metadata: ... Spec: IPv6: false Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: <nil> Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent k8sTimeout: 0 Kubelet Dir: <nil> Log Format: text Log Layers: <nil> Log Workflows: <nil> Namespace: trident Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Windows: false Status: Current Installation Params: IPv6: false Autosupport Hostname: Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: Autosupport Serial Number: Debug: false Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent Image Pull Secrets: Image Registry: k8sTimeout: 30 Kubelet Dir: /var/lib/kubelet Log Format: text Log Layers: Log Level: info Log Workflows: Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Message: Trident installed Namespace: trident Status: Installed Version: v23.04.0 Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Installing 2m59s trident-operator.netapp.io Installing Trident Normal Installed 2m31s trident-operator.netapp.io Trident installed`


### Create a backend

To instruct Trident about the Azure NetApp Files subscription and where it needs to create volumes, a backend is created. This step requires details about the account that was created in a previous step.

Create a file named

`backend-secret.yaml`

and copy in the following YAML. Change the`Client ID`

and`clientSecret`

to the correct values for your environment.`apiVersion: v1 kind: Secret metadata: name: backend-tbc-anf-secret type: Opaque stringData: clientID: 00001111-aaaa-2222-bbbb-3333cccc4444 clientSecret: rR0rUmWXfNioN1KhtHisiSAnoTherboGuskey6pU`

Create a file named

`backend-anf.yaml`

and copy in the following YAML. Change the`subscriptionID`

,`tenantID`

,`location`

, and`serviceLevel`

to the correct values for your environment. Use the`subscriptionID`

for the Azure subscription where Azure NetApp Files is enabled. Obtain the`tenantID`

,`clientID`

, and`clientSecret`

from an[application registration](/en-us/azure/active-directory/develop/howto-create-service-principal-portal)in Microsoft Entra ID with sufficient permissions for the Azure NetApp Files service. The application registration includes the Owner or Contributor role predefined by Azure. The location must be an Azure location that contains at least one delegated subnet created in a previous step. The`serviceLevel`

must match the`serviceLevel`

configured for the capacity pool in[Configure Azure NetApp Files for AKS workloads](azure-netapp-files#configure-azure-netapp-files-for-aks-workloads).`apiVersion: trident.netapp.io/v1 kind: TridentBackendConfig metadata: name: backend-tbc-anf spec: version: 1 storageDriverName: azure-netapp-files subscriptionID: aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e tenantID: aaaabbbb-0000-cccc-1111-dddd2222eeee location: eastus serviceLevel: Premium credentials: name: backend-tbc-anf-secret`

For more information about backends, see

[Azure NetApp Files backend configuration options and examples](https://docs.netapp.com/us-en/trident/trident-use/anf-examples.html).Apply the secret and backend using the

command. First apply the secret:`kubectl apply`

`kubectl apply -f backend-secret.yaml -n trident`

The output of the command resembles the following example:

`secret/backend-tbc-anf-secret created`

Apply the backend:

`kubectl apply -f backend-anf.yaml -n trident`

The output of the command resembles the following example:

`tridentbackendconfig.trident.netapp.io/backend-tbc-anf created`

Confirm the backend was created by using the

command:`kubectl get`

`kubectl get tridentbackends -n trident`

The output of the command resembles the following example:

`NAME BACKEND BACKEND UUID tbe-kfrdh backend-tbc-anf 8da4e926-9dd4-4a40-8d6a-375aab28c566`


### Create a storage class

A storage class is used to define how a unit of storage is dynamically created with a persistent volume. To consume Azure NetApp Files volumes, a storage class must be created.

Create a file named

`anf-storageclass.yaml`

and copy in the following YAML:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azure-netapp-files provisioner: csi.trident.netapp.io parameters: backendType: "azure-netapp-files" fsType: "nfs"`

Create the storage class using the

command:`kubectl apply`

`kubectl apply -f anf-storageclass.yaml`

The output of the command resembles the following example:

`storageclass/azure-netapp-files created`

Run the

command to view the status of the storage class:`kubectl get`

`kubectl get sc NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE azure-netapp-files csi.trident.netapp.io Delete Immediate false`


### Create a PVC

A persistent volume claim (PVC) is a request for storage by a user. Upon the creation of a persistent volume claim, Trident automatically creates an Azure NetApp Files volume and makes it available for Kubernetes workloads to consume.

Create a file named

`anf-pvc.yaml`

and copy in the following YAML. In this example, a 1-TiB volume is needed with ReadWriteMany access.`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: anf-pvc spec: accessModes: - ReadWriteMany resources: requests: storage: 1Ti storageClassName: azure-netapp-files`

Create the persistent volume claim with the

command:`kubectl apply`

`kubectl apply -f anf-pvc.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/anf-pvc created`

To view information about the persistent volume claim, run the

command:`kubectl get`

`kubectl get pvc`

The output of the command resembles the following example:

`kubectl get pvc -n trident NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE anf-pvc Bound pvc-bffa315d-3f44-4770-86eb-c922f567a075 1Ti RWO azure-netapp-files 62s`


### Use the persistent volume

After the PVC is created, Trident creates the persistent volume. A pod can be spun up to mount and access the Azure NetApp Files volume.

The following manifest can be used to define an NGINX pod that mounts the Azure NetApp Files volume created in the previous step. In this example, the volume is mounted at `/mnt/data`

.

Create a file named

`anf-nginx-pod.yaml`

and copy in the following YAML:`kind: Pod apiVersion: v1 metadata: name: nginx-pod spec: containers: - name: nginx image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/data" name: volume volumes: - name: volume persistentVolumeClaim: claimName: anf-pvc`

Create the pod using the

command:`kubectl apply`

`kubectl apply -f anf-nginx-pod.yaml`

The output of the command resembles the following example:

`pod/nginx-pod created`

Kubernetes has created a pod with the volume mounted and accessible within the

`nginx`

container at`/mnt/data`

. You can confirm by checking the event logs for the pod usingcommand:`kubectl describe`

`kubectl describe pod nginx-pod`

The output of the command resembles the following example:

`[...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: anf-pvc ReadOnly: false default-token-k7952: Type: Secret (a volume populated by a Secret) SecretName: default-token-k7952 Optional: false [...] Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Scheduled 15s default-scheduler Successfully assigned trident/nginx-pod to brameshb-non-root-test Normal SuccessfulAttachVolume 15s attachdetach-controller AttachVolume.Attach succeeded for volume "pvc-bffa315d-3f44-4770-86eb-c922f567a075" Normal Pulled 12s kubelet Container image "mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine" already present on machine Normal Created 11s kubelet Created container nginx Normal Started 10s kubelet Started container nginx`


## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:


---

<!-- DOCUMENTO FUSIONADO: use-vertical-pod-autoscaler.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-vertical-pod-autoscaler -->

# Use the Vertical Pod Autoscaler in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use the Vertical Pod Autoscaler (VPA) on your Azure Kubernetes Service (AKS) cluster. The VPA automatically adjusts the CPU and memory requests for your pods to match the usage patterns of your workloads. This feature helps to optimize the performance of your applications and reduce the cost of running your workloads in AKS.

For more information, see the [Vertical Pod Autoscaler overview](vertical-pod-autoscaler).

## Before you begin

If you have an existing AKS cluster, make sure it's running Kubernetes version 1.24 or higher.

You need the Azure CLI version 2.52.0 or later installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).If enabling VPA on an existing cluster, make sure

`kubectl`

is installed and configured to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --name <cluster-name> --resource-group <resource-group-name>`


## Deploy the Vertical Pod Autoscaler on a new cluster

Create a new AKS cluster with the VPA enabled using the

command with the`az aks create`

`--enable-vpa`

flag.`az aks create --name <cluster-name> --resource-group <resource-group-name> --enable-vpa --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Update an existing cluster to use the Vertical Pod Autoscaler

Update an existing cluster to use the VPA using the

command with the`az aks update`

`--enable-vpa`

flag.`az aks update --name <cluster-name> --resource-group <resource-group-name> --enable-vpa`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Disable the Vertical Pod Autoscaler on an existing cluster

Disable the VPA on an existing cluster using the

command with the`az aks update`

`--disable-vpa`

flag.`az aks update --name <cluster-name> --resource-group <resource-group-name> --disable-vpa`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Test Vertical Pod Autoscaler installation

In the following example, we create a deployment with two pods, each running a single container that requests 100 millicore and tries to utilize slightly above 500 millicores. We also create a VPA config pointing at the deployment. The VPA observes the behavior of the pods, and after about five minutes, updates the pods to request 500 millicores.

Create a file named

`hamster.yaml`

and copy in the following manifest of the Vertical Pod Autoscaler example from the[kubernetes/autoscaler](https://github.com/kubernetes/autoscaler/blob/master/vertical-pod-autoscaler/examples/hamster.yaml)GitHub repository:`apiVersion: "autoscaling.k8s.io/v1" kind: VerticalPodAutoscaler metadata: name: hamster-vpa spec: targetRef: apiVersion: "apps/v1" kind: Deployment name: hamster resourcePolicy: containerPolicies: - containerName: '*' minAllowed: cpu: 100m memory: 50Mi maxAllowed: cpu: 1 memory: 500Mi controlledResources: ["cpu", "memory"] --- apiVersion: apps/v1 kind: Deployment metadata: name: hamster spec: selector: matchLabels: app: hamster replicas: 2 template: metadata: labels: app: hamster spec: securityContext: runAsNonRoot: true runAsUser: 65534 containers: - name: hamster image: registry.k8s.io/ubuntu-slim:0.1 resources: requests: cpu: 100m memory: 50Mi command: ["/bin/sh"] args: - "-c" - "while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done"`

Deploy the

`hamster.yaml`

Vertical Pod Autoscaler example using thecommand.`kubectl apply`

`kubectl apply -f hamster.yaml`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

View the running pods using the

command.`kubectl get`

`kubectl get pods -l app=hamster`

Your output should look similar to the following example output:

`hamster-78f9dcdd4c-hf7gk 1/1 Running 0 24s hamster-78f9dcdd4c-j9mc7 1/1 Running 0 24s`

View the CPU and Memory reservations on one of the pods using the

command. Make sure you replace`kubectl describe`

`<example-pod>`

with one of the pod IDs returned in your output from the previous step.`kubectl describe pod hamster-<example-pod>`

Your output should look similar to the following example output:

`hamster: Container ID: containerd:// Image: k8s.gcr.io/ubuntu-slim:0.1 Image ID: sha256: Port: <none> Host Port: <none> Command: /bin/sh Args: -c while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done State: Running Started: Wed, 28 Sep 2022 15:06:14 -0400 Ready: True Restart Count: 0 Requests: cpu: 100m memory: 50Mi Environment: <none>`

The pod has 100 millicpu and 50 Mibibytes of Memory reserved in this example. For this sample application, the pod needs less than 100 millicpu to run, so there's no CPU capacity available. The pods also reserves less memory than needed. The Vertical Pod Autoscaler

*vpa-recommender*deployment analyzes the pods hosting the hamster application to see if the CPU and Memory requirements are appropriate. If adjustments are needed, the vpa-updater relaunches the pods with updated values.Monitor the pods using the

command.`kubectl get`

`kubectl get --watch pods -l app=hamster`

When the new hamster pod starts, you can view the updated CPU and Memory reservations using the

command. Make sure you replace`kubectl describe`

`<example-pod>`

with one of the pod IDs returned in your output from the previous step.`kubectl describe pod hamster-<example-pod>`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none>`

In the previous output, you can see that the CPU reservation increased to 587 millicpu, which is over five times the original value. The Memory increased to 262,144 Kilobytes, which is around 250 Mibibytes, or five times the original value. This pod was under-resourced, and the Vertical Pod Autoscaler corrected the estimate with a much more appropriate value.

View updated recommendations from VPA using the

command to describe the hamster-vpa resource information.`kubectl describe`

`kubectl describe vpa/hamster-vpa`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none>`


## Set Vertical Pod Autoscaler requests

The `VerticalPodAutoscaler`

object automatically sets resource requests on pods with an `updateMode`

of `Auto`

. You can set a different value depending on your requirements and testing. In this example, we create and test a deployment manifest with two pods, each running a container that requests 100 milliCPU and 50 MiB of Memory, and sets the `updateMode`

to `Recreate`

.

Create a file named

`azure-autodeploy.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: vpa-auto-deployment spec: replicas: 2 selector: matchLabels: app: vpa-auto-deployment template: metadata: labels: app: vpa-auto-deployment spec: containers: - name: mycontainer image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 50Mi command: ["/bin/sh"] args: ["-c", "while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done"]`

Create the pod using the

command.`kubectl create`

`kubectl create -f azure-autodeploy.yaml`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

View the running pods using the

command.`kubectl get`

`kubectl get pods`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE vpa-auto-deployment-54465fb978-kchc5 1/1 Running 0 52s vpa-auto-deployment-54465fb978-nhtmj 1/1 Running 0 52s`

Create a file named

`azure-vpa-auto.yaml`

and copy in the following manifest:`apiVersion: autoscaling.k8s.io/v1 kind: VerticalPodAutoscaler metadata: name: vpa-auto spec: targetRef: apiVersion: "apps/v1" kind: Deployment name: vpa-auto-deployment updatePolicy: updateMode: "Recreate"`

The

`targetRef.name`

value specifies that any pod controlled by a deployment named`vpa-auto-deployment`

belongs to`VerticalPodAutoscaler`

. The`updateMode`

value of`Recreate`

means that the Vertical Pod Autoscaler controller can delete a pod, adjust the CPU and Memory requests, and then create a new pod.Apply the manifest to the cluster using the

command.`kubectl apply`

`kubectl create -f azure-vpa-auto.yaml`

Wait a few minutes and then view the running pods using the

command.`kubectl get`

`kubectl get pods`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE vpa-auto-deployment-54465fb978-qbhc4 1/1 Running 0 2m49s vpa-auto-deployment-54465fb978-vbj68 1/1 Running 0 109s`

Get detailed information about one of your running pods using the

command. Make sure you replace`kubectl get`

`<pod-name>`

with the name of one of your pods from your previous output.`kubectl get pod <pod-name> --output yaml`

Your output should look similar to the following example output, which shows that VPA controller increased the Memory request to 262144k and the CPU request to 25 milliCPU:

`apiVersion: v1 kind: Pod metadata: annotations: vpaObservedContainers: mycontainer vpaUpdates: 'Pod resources updated by vpa-auto: container 0: cpu request, memory request' creationTimestamp: "2022-09-29T16:44:37Z" generateName: vpa-auto-deployment-54465fb978- labels: app: vpa-auto-deployment spec: containers: - args: - -c - while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done command: - /bin/sh image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine imagePullPolicy: IfNotPresent name: mycontainer resources: requests: cpu: 25m memory: 262144k`

Get detailed information about the Vertical Pod Autoscaler and its recommendations for CPU and Memory using the

command.`kubectl get`

`kubectl get vpa vpa-auto --output yaml`

Your output should look similar to the following example output:

`recommendation: containerRecommendations: - containerName: mycontainer lowerBound: cpu: 25m memory: 262144k target: cpu: 25m memory: 262144k uncappedTarget: cpu: 25m memory: 262144k upperBound: cpu: 230m memory: 262144k`

In this example, the results in the

`target`

attribute specify that it doesn't need to change the CPU or the Memory target for the container to run optimally. However, results can vary depending on the application and its resource utilization.The Vertical Pod Autoscaler uses the

`lowerBound`

and`upperBound`

attributes to decide whether to delete a pod and replace it with a new pod. If a pod has requests less than the lower bound or greater than the upper bound, the Vertical Pod Autoscaler deletes the pod and replaces it with a pod that meets the target attribute.

## Extra Recommender for Vertical Pod Autoscaler

The Recommender provides recommendations for resource usage based on real-time resource consumption. AKS deploys a Recommender when a cluster enables VPA. You can deploy a customized Recommender or an extra Recommender with the same image as the default one. The benefit of having a customized Recommender is that you can customize your recommendation logic. With an extra Recommender, you can partition VPAs to use different Recommenders.

In the following example, we create an extra Recommender, apply to an existing AKS cluster, and configure the VPA object to use the extra Recommender.

Create a file named

`extra_recommender.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: extra-recommender namespace: kube-system spec: replicas: 1 selector: matchLabels: app: extra-recommender template: metadata: labels: app: extra-recommender spec: serviceAccountName: vpa-recommender securityContext: runAsNonRoot: true runAsUser: 65534 containers: - name: recommender image: registry.k8s.io/autoscaling/vpa-recommender:0.13.0 imagePullPolicy: Always args: - --recommender-name=extra-recommender resources: limits: cpu: 200m memory: 1000Mi requests: cpu: 50m memory: 500Mi ports: - name: prometheus containerPort: 8942`

Deploy the

`extra-recomender.yaml`

Vertical Pod Autoscaler example using thecommand.`kubectl apply`

`kubectl apply -f extra-recommender.yaml`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

Create a file named

`hamster-extra-recommender.yaml`

and copy in the following manifest:`apiVersion: "autoscaling.k8s.io/v1" kind: VerticalPodAutoscaler metadata: name: hamster-vpa spec: recommenders: - name: 'extra-recommender' targetRef: apiVersion: "apps/v1" kind: Deployment name: hamster updatePolicy: updateMode: "Auto" resourcePolicy: containerPolicies: - containerName: '*' minAllowed: cpu: 100m memory: 50Mi maxAllowed: cpu: 1 memory: 500Mi controlledResources: ["cpu", "memory"] --- apiVersion: apps/v1 kind: Deployment metadata: name: hamster spec: selector: matchLabels: app: hamster replicas: 2 template: metadata: labels: app: hamster spec: securityContext: runAsNonRoot: true runAsUser: 65534 # nobody containers: - name: hamster image: k8s.gcr.io/ubuntu-slim:0.1 resources: requests: cpu: 100m memory: 50Mi command: ["/bin/sh"] args: - "-c" - "while true; do timeout 0.5s yes >/dev/null; sleep 0.5s; done"`

If

`memory`

isn't specified in`controlledResources`

, the Recommender doesn't respond to OOM events. In this example, we only set CPU in`controlledValues`

.`controlledValues`

allows you to choose whether to update the container's resource requests using the`RequestsOnly`

option, or by both resource requests and limits using the`RequestsAndLimits`

option. The default value is`RequestsAndLimits`

. If you use the`RequestsAndLimits`

option, requests are computed based on actual usage, and limits are calculated based on the current pod's request and limit ratio.For example, if you start with a pod that requests 2 CPUs and limits to 4 CPUs, VPA always sets the limit to be twice as much as requests. The same principle applies to Memory. When you use the

`RequestsAndLimits`

mode, it can serve as a blueprint for your initial application resource requests and limits.You can simplify the VPA object using

`Auto`

mode and computing recommendations for both CPU and Memory.Deploy the

`hamster-extra-recomender.yaml`

example using thecommand.`kubectl apply`

`kubectl apply -f hamster-extra-recommender.yaml`

Monitor your pods using the

`[kubectl get`

][kubectl-get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.`kubectl get --watch pods -l app=hamster`

When the new hamster pod starts, view the updated CPU and Memory reservations using the

command. Make sure you replace`kubectl describe`

`<example-pod>`

with one of your pod IDs.`kubectl describe pod hamster-<example-pod>`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none>`

View updated recommendations from VPA using the

command.`kubectl describe`

`kubectl describe vpa/hamster-vpa`

Your output should look similar to the following example output:

`State: Running Started: Wed, 28 Sep 2022 15:09:51 -0400 Ready: True Restart Count: 0 Requests: cpu: 587m memory: 262144k Environment: <none> Spec: recommenders: Name: customized-recommender`


## Troubleshoot the Vertical Pod Autoscaler

If you encounter issues with the Vertical Pod Autoscaler, you can troubleshoot the system components and custom resource definition to identify the problem.

Verify that all system components are running using the following command:

`kubectl get pods|grep vpa`

Your output should list

*three pods*: recommender, updater, and admission-controller, all with a status of`Running`

.For each of the pods returned in your previous output, verify that the system components are logging any errors using the following command:

`kubectl logs [pod name] | grep -e '^E[0-9]\{4\}'`

Verify that the custom resource definition was created using the following command:

`kubectl get customresourcedefinition | grep verticalpodautoscalers`


## Next steps

To learn more about the VPA object, see the [Vertical Pod Autoscaler API reference](vertical-pod-autoscaler-api-reference).
