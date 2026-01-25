---
merged_at: 2026-01-25T12:06:27.866081
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-azure-ad-pod-identity.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-azure-ad-pod-identity -->

# Use Microsoft Entra pod-managed identities in AKS (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Microsoft Entra pod-managed identities use Azure Kubernetes Service (AKS) primitives to associate [managed identities for Azure resources](/en-us/azure/active-directory/managed-identities-azure-resources/overview) and identities in Microsoft Entra ID with pods. Administrators create identities and bindings as Kubernetes primitives that allow pods to access Azure resources that rely on Microsoft Entra ID as an identity provider.

Microsoft Entra pod-managed identities in AKS have the following limitations:

- Each cluster supports up to 200 pod-managed identities.
- Each cluster supports up to 200 pod-managed identity exceptions.
- Pod-managed identities are supported only on Linux node pools.
- This feature is supported only on clusters backed by Virtual Machine Scale Sets.

Important

We recommend you review [Microsoft Entra Workload ID](workload-identity-overview). This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities to federate with any external identity providers on behalf of the application.

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated on October 24, 2022, and the project archived in September 2023. For more information, see the [deprecation notice](https://github.com/Azure/aad-pod-identity#-announcement). The AKS Pod Identity Managed add-on is patched and supported through September 2025 to allow time for customers to move over to [Microsoft Entra Workload ID](workload-identity-overview).

## Operation mode options

Microsoft Entra pod-managed identity supports two modes of operation:

**Standard Mode**: In this mode, the following two components are deployed to the AKS cluster:[Managed Identity Controller (MIC)](https://azure.github.io/aad-pod-identity/docs/concepts/mic/): An MIC is a Kubernetes controller that watches for changes to pods,[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/), and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)through the Kubernetes API Server. When it detects a relevant change, the MIC adds or deletes[AzureAssignedIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureassignedidentity/)as needed. Specifically, when a pod is scheduled, the MIC assigns the managed identity on Azure to the underlying Virtual Machine Scale Set used by the node pool during the creation phase. When all pods using the identity are deleted, it removes the identity from the Virtual Machine Scale Set of the node pool, unless the same managed identity is used by other pods. The MIC takes similar actions when AzureIdentity or AzureIdentityBinding are created or deleted.[Node Managed Identity (NMI)](https://azure.github.io/aad-pod-identity/docs/concepts/nmi/): NMI is a pod that runs as a DaemonSet on each node in the AKS cluster. NMI intercepts security token requests to the[Azure Instance Metadata Service](/en-us/azure/virtual-machines/linux/instance-metadata-service?tabs=linux)on each node. NMI intercepts token requests and redirects them to itself. It then checks if the pod is authorized to access the requested identity and, if so, retrieves the token from the Microsoft Entra tenant on behalf of the application.

**Managed Mode**: This mode offers only NMI. When installed via the AKS cluster add-on, Azure manages creation of Kubernetes primitives (AzureIdentity and AzureIdentityBinding) and identity assignment in response to CLI commands by the user. Otherwise, if installed via Helm chart, the identity needs to be manually assigned and managed per the user. For more information, see[Pod identity in managed mode](https://azure.github.io/aad-pod-identity/docs/configure/pod_identity_in_managed_mode/).

When you install the Microsoft Entra pod-managed identity via Helm chart or YAML manifest as shown in the [Installation Guide](https://azure.github.io/aad-pod-identity/docs/getting-started/installation/), you can choose between the `standard`

and `managed`

mode. If you instead decide to install the
Microsoft Entra pod-managed identity using the AKS cluster add-on as shown in this article, the setup uses the `managed`

mode.

## Prerequisites

Your Microsoft Entra pod-managed identities in AKS must meet the following requirements:

The Azure CLI version 2.20.0 or later is installed.

Your AKS cluster is at version 1.26 or later.

You must have the appropriate permissions such as the

**Owner**or**Contributor**role.

## Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

To install the aks-preview extension, run the following command:

```
az extension add --name aks-preview
```


Run the following command to update to the latest version of the extension released:

```
az extension update --name aks-preview
```


## Register the EnablePodIdentityPreview feature flag

Register the `EnablePodIdentityPreview`

feature flag by using the [az feature register](/en-us/cli/azure/feature#az-feature-register) command as shown in the following example:

```
az feature register --namespace "Microsoft.ContainerService" --name "EnablePodIdentityPreview"
```


Tip

To disable the AKS Managed add-on, run the following command:

```
az feature unregister --namespace "Microsoft.ContainerService" --name "EnablePodIdentityPreview"
```


It takes a few minutes for the status to show as *Registered*. Verify the registration status by using the [az feature show](/en-us/cli/azure/feature#az-feature-show) command:

```
az feature show --namespace "Microsoft.ContainerService" --name "EnablePodIdentityPreview"
```


When the status reflects *Registered*, refresh the registration of the *Microsoft.ContainerService* resource provider by using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command:

```
az provider register --namespace Microsoft.ContainerService
```


## Manage an AKS cluster with pod-managed identities

You can manage your AKS cluster with either the Azure Container Networking Interface (CNI) or Kubenet network plugin when enabling Microsoft Entra pod-managed identities.

Create an AKS cluster with Azure CNI and pod-managed identity enabled with the default recommended configuration. The following commands use

[az group create](/en-us/cli/azure/group#az-group-create)to create a resource group named*myResourceGroup*and thecommand to create an AKS cluster named`az aks create`

*myAKSCluster*in the*myResourceGroup*resource group.`az group create --name myResourceGroup --location eastus az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-pod-identity \ --network-plugin azure \ --generate-ssh-keys`

Use

to sign in to your AKS cluster. This command also downloads and configures the`az aks get-credentials`

`kubectl`

client certificate on your development computer.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


When you enable pod-managed identity on your AKS cluster, the system adds an `AzurePodIdentityException`

named *aks-addon-exception* to the *kube-system* namespace. An `AzurePodIdentityException`

lets pods with certain labels access the Azure Instance Metadata Service (IMDS) endpoint without interception by the NMI server. The *aks-addon-exception* allows AKS first-party addons, such as Microsoft Entra pod-managed identity, to operate without requiring you to manually configure an `AzurePodIdentityException`

. Optionally, you can add, remove, and update an `AzurePodIdentityException`

using:

`az aks pod-identity exception add`

`az aks pod-identity exception delete`

`az aks pod-identity exception update`

Or

`kubectl`


## Update an existing AKS cluster with Azure CNI

To update an existing AKS cluster with Azure CNI to include pod-managed identity, run the following command:

```
az aks update --resource-group $MY_RESOURCE_GROUP --name $MY_CLUSTER --enable-pod-identity
```


## Create a managed identity

You must have the relevant permissions (for example, **Owner**) on your subscription to create the identity.

To create an identity to be used by the demo pod with [az identity create](/en-us/cli/azure/identity#az-identity-create), set the *IDENTITY_CLIENT_ID* and *IDENTITY_RESOURCE_ID* variables, run the following command:

```
az group create --name myIdentityResourceGroup --location eastus
export IDENTITY_RESOURCE_GROUP="myIdentityResourceGroup"
export IDENTITY_NAME="application-identity"
az identity create --resource-group ${IDENTITY_RESOURCE_GROUP} --name ${IDENTITY_NAME}
export IDENTITY_CLIENT_ID="$(az identity show --resource-group ${IDENTITY_RESOURCE_GROUP} --name ${IDENTITY_NAME} --query clientId -o tsv)"
export IDENTITY_RESOURCE_ID="$(az identity show --resource-group ${IDENTITY_RESOURCE_GROUP} --name ${IDENTITY_NAME} --query id -o tsv)"
```


## Assign permissions for the managed identity

The managed identity assigned to the pod must be granted appropriate permissions based on the operations the pod performs. Ensure that you assign only the minimum required roles to follow security best practices.

To run the demo, the *IDENTITY_CLIENT_ID* managed identity must have **Virtual Machine Contributor** permissions in the resource group that contains the Virtual Machine Scale Set of your AKS cluster.

```
# Obtain the name of the resource group containing the Virtual Machine Scale set of your AKS cluster, commonly called the node resource group
NODE_GROUP=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
# Obtain the id of the node resource group
NODES_RESOURCE_ID=$(az group show --name $NODE_GROUP -o tsv --query "id")
# Create a role assignment granting your managed identity permissions on the node resource group
az role assignment create --role "Virtual Machine Contributor" --assignee "$IDENTITY_CLIENT_ID" --scope $NODES_RESOURCE_ID
```


## Create a pod-managed identity

To create a pod-managed identity for the cluster using `az aks pod-identity add`

, run the following command:

```
export POD_IDENTITY_NAME="my-pod-identity"
export POD_IDENTITY_NAMESPACE="my-app"
az aks pod-identity add --resource-group myResourceGroup --cluster-name myAKSCluster --namespace ${POD_IDENTITY_NAMESPACE} --name ${POD_IDENTITY_NAME} --identity-resource-id ${IDENTITY_RESOURCE_ID}
```


Note

The "POD_IDENTITY_NAME" has to be a valid Domain Name System [(DNS) subdomain name](https://kubernetes.io/docs/concepts/overview/working-with-objects/names/#dns-subdomain-names) as defined in [RFC 1123](https://tools.ietf.org/html/rfc1123).

When you assign the pod-managed identity by using `pod-identity add`

, the Azure CLI attempts to grant the Managed Identity Operator role over the pod-managed identity (*IDENTITY_RESOURCE_ID*) to the cluster identity.

Azure creates an AzureIdentity resource in your cluster representing the identity in Azure, and an AzureIdentityBinding resource that connects the AzureIdentity to a selector. You can view these resources by running the following command:

```
kubectl get azureidentity -n $POD_IDENTITY_NAMESPACE
kubectl get azureidentitybinding -n $POD_IDENTITY_NAMESPACE
```


## Run a sample application

For a pod to use Microsoft Entra pod-managed identity, the pod needs an *aadpodidbinding* label with a value that matches a selector from a *AzureIdentityBinding*. By default, the selector matches the name of the pod-managed identity, but it can also be set using the `--binding-selector`

option when calling `az aks pod-identity add`

.

To run a sample application using Microsoft Entra pod-managed identity, create a `demo.yaml`

file with the following contents. Replace *POD_IDENTITY_NAME*, *IDENTITY_CLIENT_ID*, and *IDENTITY_RESOURCE_GROUP* with the values from the previous steps. Replace *SUBSCRIPTION_ID* with your subscription ID.

Note

In the previous steps, you created the *POD_IDENTITY_NAME*, *IDENTITY_CLIENT_ID*, and *IDENTITY_RESOURCE_GROUP* variables. You can use a command such as `echo`

to display the value you set for variables, for example `echo $POD_IDENTITY_NAME`

.

```
apiVersion: v1
kind: Pod
metadata:
name: demo
labels:
aadpodidbinding: $POD_IDENTITY_NAME
spec:
containers:
- name: demo
image: mcr.microsoft.com/oss/azure/aad-pod-identity/demo:v1.6.3
args:
- --subscriptionid=$SUBSCRIPTION_ID
- --clientid=$IDENTITY_CLIENT_ID
- --resourcegroup=$IDENTITY_RESOURCE_GROUP
env:
- name: MY_POD_NAME
valueFrom:
fieldRef:
fieldPath: metadata.name
- name: MY_POD_NAMESPACE
valueFrom:
fieldRef:
fieldPath: metadata.namespace
- name: MY_POD_IP
valueFrom:
fieldRef:
fieldPath: status.podIP
nodeSelector:
kubernetes.io/os: linux
```


Notice the pod definition has an `aadpodidbinding`

label with a value that matches the name of the pod-managed identity you ran `az aks pod-identity add`

in the previous step.

Deploy the

`demo.yaml`

to the same namespace as your pod-managed identity using`kubectl apply`

:`kubectl apply -f demo.yaml --namespace $POD_IDENTITY_NAMESPACE`

Verify the sample application successfully runs using

`kubectl logs`

:`kubectl logs demo --follow --namespace $POD_IDENTITY_NAMESPACE`

Verify that the logs show a token is successfully acquired and that the HTTP

*GET*request operation is successful.`... successfully doARMOperations vm count 0 successfully acquired a token using the MSI, msiEndpoint(http://169.254.169.254/metadata/identity/oauth2/token) successfully acquired a token, userAssignedID MSI, msiEndpoint(http://169.254.169.254/metadata/identity/oauth2/token) clientID(xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx) successfully made GET on instance metadata ...`


## Run an application with multiple identities

To enable an application to use multiple identities, set the `--binding-selector`

to the same selector when creating pod identities:

```
az aks pod-identity add --resource-group myResourceGroup --cluster-name myAKSCluster --namespace ${POD_IDENTITY_NAMESPACE} --name ${POD_IDENTITY_NAME_1} --identity-resource-id ${IDENTITY_RESOURCE_ID_1} --binding-selector myMultiIdentitySelector
az aks pod-identity add --resource-group myResourceGroup --cluster-name myAKSCluster --namespace ${POD_IDENTITY_NAMESPACE} --name ${POD_IDENTITY_NAME_2} --identity-resource-id ${IDENTITY_RESOURCE_ID_2} --binding-selector myMultiIdentitySelector
```


Then set the `aadpodidbinding`

field in your pod YAML to the binding selector you specified.

```
apiVersion: v1
kind: Pod
metadata:
name: demo
labels:
aadpodidbinding: myMultiIdentitySelector
...
```


## Disable pod-managed identity on an existing cluster

To disable pod-managed identity on an existing cluster, remove the pod-managed identities from the cluster by running the following command:

`az aks pod-identity delete --name ${POD_IDENTITY_NAME} --namespace ${POD_IDENTITY_NAMESPACE} --resource-group myResourceGroup --cluster-name myAKSCluster`

Then disable the feature on the cluster by running the following command:

`az aks update --resource-group myResourceGroup --name myAKSCluster --disable-pod-identity`


## Clean up resources

To remove a Microsoft Entra pod-managed identity from your cluster, remove the sample application and the pod-managed identity from the cluster.

```
kubectl delete pod demo --namespace $POD_IDENTITY_NAMESPACE
```


Then remove the identity and the role assignment of cluster identity.

```
az aks pod-identity delete \
--name ${POD_IDENTITY_NAME} \
--namespace ${POD_IDENTITY_NAMESPACE} \
--resource-group myResourceGroup \
--cluster-name myAKSCluster
az identity delete \
--resource-group ${IDENTITY_RESOURCE_GROUP} \
--name ${IDENTITY_NAME}
az role assignment delete \
--role "Managed Identity Operator" \
--assignee "$IDENTITY_CLIENT_ID" \
--scope "$IDENTITY_RESOURCE_ID"
```


## Next steps

For more information on managed identities, see [Managed identities for Azure resources](/en-us/azure/active-directory/managed-identities-azure-resources/overview).


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
