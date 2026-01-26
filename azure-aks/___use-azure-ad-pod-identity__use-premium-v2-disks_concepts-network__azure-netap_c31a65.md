---
merged_at: 2026-01-26T23:04:06.014892
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-ad-pod-identity -->

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
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-premium-v2-disks -->

# Use Azure Premium SSD v2 disks on Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure Premium SSD v2 disks](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2) offer IO-intense enterprise workloads, a consistent submillisecond disk latency, and high IOPS and throughput. The performance (capacity, throughput, and IOPS) of Premium SSD v2 disks can be independently configured at any time, making it easier for more scenarios to be cost efficient while meeting performance needs.

This article describes how to configure a new or existing AKS cluster to use Azure Premium SSD v2 disks.

## Before you begin

Before creating or upgrading an AKS cluster that is able to use Azure Premium SSD v2 disks, you need to create an AKS cluster in the same region and availability zone that supports Premium Storage and attach the disks following the steps below.

For an existing AKS cluster, you can enable Premium SSD v2 disks by adding a new node pool to your cluster, and then attach the disks following the steps below.

Important

Azure Premium SSD v2 disks require node pools deployed in regions that support these disks. For a list of supported regions, see [Premium SSD v2 disk supported regions](/en-us/azure/virtual-machines/disks-types#regional-availability).

### Limitations

- Azure Premium SSD v2 disks have certain limitations that you need to be aware of. For a complete list, see
[Premium SSD v2 limitations](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2-limitations).

## Use Premium SSD v2 disks dynamically with a storage class

To use Premium SSD v2 disks in a deployment or stateful set, you can use a [storage class for dynamic provisioning](azure-disk-csi).

### Create the storage class

A storage class is used to define how a unit of storage is dynamically created with a persistent volume. For more information on Kubernetes storage classes, see [Kubernetes Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

In this example, you create a storage class that references Premium SSD v2 disks. Create a file named `azure-pv2-disk-sc.yaml`

, and copy in the following manifest.

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: premium2-disk-sc
parameters:
cachingMode: None
skuName: PremiumV2_LRS
DiskIOPSReadWrite: "4000"
DiskMBpsReadWrite: "1000"
provisioner: disk.csi.azure.com
reclaimPolicy: Delete
volumeBindingMode: Immediate
allowVolumeExpansion: true
```


Create the storage class with the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command and specify your *azure-pv2-disk-sc.yaml* file:

```
kubectl apply -f azure-pv2-disk-sc.yaml
```


The output from the command resembles the following example:

```
storageclass.storage.k8s.io/premium2-disk-sc created
```


## Create a persistent volume claim

A persistent volume claim (PVC) is used to automatically provision storage based on a storage class. In this case, a PVC can use the previously created storage class to create an ultra disk.

Create a file named `azure-pv2-disk-pvc.yaml`

, and copy in the following manifest. The claim requests a disk named `premium2-disk`

that is *1000 GB* in size with *ReadWriteOnce* access. The *premium2-disk-sc* storage class is specified as the storage class.

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: premium2-disk
spec:
accessModes:
- ReadWriteOnce
storageClassName: premium2-disk-sc
resources:
requests:
storage: 1000Gi
```


Create the persistent volume claim with the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command and specify your *azure-pv2-disk-pvc.yaml* file:

```
kubectl apply -f azure-pv2-disk-pvc.yaml
```


The output from the command resembles the following example:

```
persistentvolumeclaim/premium2-disk created
```


## Use the persistent volume

Once the persistent volume claim has been created and the disk successfully provisioned, a pod can be created with access to the disk. The following manifest creates a basic NGINX pod that uses the persistent volume claim named *premium2-disk* to mount the Azure disk at the path `/mnt/azure`

.

Create a file named `nginx-premium2.yaml`

, and copy in the following manifest.

```
kind: Pod
apiVersion: v1
metadata:
name: nginx-premium2
spec:
containers:
- name: nginx-premium2
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
resources:
requests:
cpu: 100m
memory: 128Mi
limits:
cpu: 250m
memory: 256Mi
volumeMounts:
- mountPath: "/mnt/azure"
name: volume
volumes:
- name: volume
persistentVolumeClaim:
claimName: premium2-disk
```


Create the pod with the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command, as shown in the following example:

```
kubectl apply -f nginx-premium2.yaml
```


The output from the command resembles the following example:

```
pod/nginx-premium2 created
```


You now have a running pod with your Azure disk mounted in the `/mnt/azure`

directory. This configuration can be seen when inspecting your pod via `kubectl describe pod nginx-premium2`

, as shown in the following condensed example:

```
kubectl describe pod nginx-premium2
[...]
Volumes:
volume:
Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace)
ClaimName: premium2-disk
ReadOnly: false
kube-api-access-sh59b:
Type: Projected (a volume that contains injected data from multiple sources)
TokenExpirationSeconds: 3607
ConfigMapName: kube-root-ca.crt
ConfigMapOptional: <nil>
DownwardAPI: true
QoS Class: Burstable
Node-Selectors: <none>
Tolerations: node.kubernetes.io/memory-pressure:NoSchedule op=Exists
node.kubernetes.io/not-ready:NoExecute op=Exists for 300s
node.kubernetes.io/unreachable:NoExecute op=Exists for 300s
Events:
Type Reason Age From Message
---- ------ ---- ---- -------
Normal Scheduled 7m58s default-scheduler Successfully assigned default/nginx-premium2 to aks-agentpool-12254644-vmss000006
Normal SuccessfulAttachVolume 7m46s attachdetach-controller AttachVolume.Attach succeeded for volume "pvc-ff39fb64-1189-4c52-9a24-e065b855b886"
Normal Pulling 7m39s kubelet Pulling image "mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine"
Normal Pulled 7m38s kubelet Successfully pulled image "mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine" in 1.192915667s
Normal Created 7m38s kubelet Created container nginx-premium2
Normal Started 7m38s kubelet Started container nginx-premium2
[...]
```


## Set IOPS and throughput limits

Input/Output Operations Per Second (IOPS) and throughput limits for Azure Premium v2 SSD disk is currently not supported through AKS. To adjust performance, you can use the Azure CLI command [az disk update](/en-us/cli/azure/disk#az-disk-update) and including the `--disk-iops-read-write`

and `--disk-mbps-read-write`

parameters.

The following example updates the disk IOPS read/write to **5000** and Mbps to **200**. For `--resource-group`

, the value must be the second resource group automatically created to store the AKS worker nodes with the naming convention *MC_resourcegroupname_clustername_location*. For more information, see [Why are two resource groups created with AKS?](faq).

The value for the `--name`

parameter is the name of the volume created using the StorageClass, and it starts with `pvc-`

. To identify the disk name, you can run `kubectl get pvc`

or navigate to the secondary resource group in the portal to find it. See [manage resources from the Azure portal](/en-us/azure/azure-resource-manager/management/manage-resources-portal#open-resources) to learn more.

```
az disk update --subscription subscriptionName --resource-group myResourceGroup --name diskName --disk-iops-read-write=5000 --disk-mbps-read-write=200
```


## Next steps

- For more about Premium SSD v2 disks, see
[Using Azure Premium SSD v2 disks](/en-us/azure/virtual-machines/disks-deploy-premium-v2). - For more about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service (AKS)](operator-best-practices-storage).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network -->

# Networking concepts for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In a container-based, microservices approach to application development, application components work together to process their tasks. Kubernetes provides various resources enabling this cooperation:

- You can connect to and expose applications internally or externally.
- You can build highly available applications by load balancing your applications.
- You can restrict the flow of network traffic into or between pods and nodes to improve security.
- You can configure Ingress traffic for SSL/TLS termination or routing of multiple components for your more complex applications.

This article introduces the core concepts that provide networking to your applications in AKS:

## Kubernetes networking basics

Kubernetes employs a virtual networking layer to manage access within and between your applications or their components:

**Kubernetes nodes and virtual network**: Kubernetes nodes are connected to a virtual network. This setup enables pods (basic units of deployment in Kubernetes) to have both inbound and outbound connectivity.**Kube-proxy component**: kube-proxy runs on each node and is responsible for providing the necessary network features.

Regarding specific Kubernetes functionalities:

**Load balancer**: You can use a load balancer to distribute network traffic evenly across various resources.**Ingress controllers**: These facilitate Layer 7 routing, which is essential for directing application traffic.**Egress traffic control**: Kubernetes allows you to manage and control outbound traffic from cluster nodes.**Network policies**: These policies enable security measures and filtering for network traffic in pods.

In the context of the Azure platform:

- Azure streamlines virtual networking for AKS (Azure Kubernetes Service) clusters.
- Creating a Kubernetes load balancer on Azure simultaneously sets up the corresponding Azure load balancer resource.
- As you open network ports to pods, Azure automatically configures the necessary network security group rules.
- Azure can also manage external DNS configurations for HTTP application routing as new Ingress routes are established.

## Azure virtual networks

In AKS, you can deploy a cluster that uses one of the following network models:

**Overlay network model**: Overlay networking is the most common networking model used in Kubernetes. Pods are given an IP address from a private, logically separate CIDR from the Azure virtual network subnet where AKS nodes are deployed. This model enables simpler, improved scalability when compared to the flat network model.**Flat network model**: A flat network model in AKS assigns IP addresses to pods from a subnet from the same Azure virtual network as the AKS nodes. Any traffic leaving your clusters isn't SNAT'd, and the pod IP address is directly exposed to the destination. This model can be useful for scenarios like exposing pod IP addresses to external services.

For more information on networking models in AKS, see [CNI Networking in AKS](concepts-network-cni-overview).

## Control outbound (egress) traffic

AKS clusters are deployed on a virtual network and have outbound dependencies on services outside of that virtual network, which are almost entirely defined with fully qualified domain names (FQDNs). AKS provides several outbound configuration options which allow you to customize the way in which these external resources are accessed.

Note

After [31 March 2026](https://azure.microsoft.com/updates?id=default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access), new AKS clusters that use the **AKS-managed virtual network** option will place cluster subnets into [private subnets](/en-us/azure/virtual-network/ip-services/default-outbound-access#why-is-disabling-default-outbound-access-recommended) by default (`defaultOutboundAccess = false`

).

This setting **does not impact AKS-managed cluster traffic**, which uses explicitly configured outbound paths. It may affect **unsupported scenarios**, such as deploying other resources (e.g., VMs) into the same subnet.

**Clusters using BYO VNets are unaffected** by this change. In supported configurations, no action is required.

### Outbound configuration options

For more information on the supported AKS cluster outbound configuration types, see [Customize cluster egress with outbound types in Azure Kubernetes Service (AKS)](egress-outboundtype).

By default, AKS clusters have unrestricted outbound (egress) Internet access, which allows the nodes and services you run to access external resources as needed. If desired, you can restrict outbound traffic.

For more information on how to restrict outbound traffic from your cluster see [Control egress traffic for cluster nodes in AKS](limit-egress-traffic).

## Network security groups

A network security group filters traffic for VMs like the AKS nodes. As you create Services, such as a *LoadBalancer*, the Azure platform automatically configures any necessary network security group rules.

You don't need to manually configure network security group rules to filter traffic for pods in an AKS cluster. You can define any required ports and forwarding as part of your Kubernetes Service manifests and let the Azure platform create or update the appropriate rules.

You can also use network policies to automatically apply traffic filter rules to pods.

For more information, see [How network security groups filter network traffic](/en-us/azure/virtual-network/network-security-group-how-it-works).

### Custom virtual network requirements

When using a custom virtual network with AKS clusters, if you have added Network Security Group (NSG) rules to restrict traffic between different subnets, ensure that the NSG security rules permit the following types of communication:

| Destination | Source | Protocol | Port | Use |
|---|---|---|---|---|
| APIServer Subnet CIDR | Cluster Subnet | TCP | 443 and 4443 | Required to enable communication between Nodes and the API server. |
| APIServer Subnet CIDR | Azure Load Balancer | TCP | 9988 | Required to enable communication between Azure Load Balancer and the API server. You can also enable all communication between the Azure Load Balancer and the API Server Subnet CIDR. |
| Node CIDR | Node CIDR | All Protocols | All Ports | Required to enable communication between Nodes. |
| Node CIDR | Pod CIDR | All Protocols | All Ports | Required for Service traffic routing. |
| Pod CIDR | Pod CIDR | All Protocols | All Ports | Required for Pod to Pod and Pod to Service traffic, including DNS. |

These requirements apply to both AKS Standard and AKS Automatic clusters when using custom virtual networks.

## Network policies

By default, all pods in an AKS cluster can send and receive traffic without limitations. For improved security, define rules that control the flow of traffic, like:

- Back-end applications are only exposed to required frontend services.
- Database components are only accessible to the application tiers that connect to them.

Network policy is a Kubernetes feature available in AKS that lets you control the traffic flow between pods. You can allow or deny traffic to the pod based on settings such as assigned labels, namespace, or traffic port. While network security groups are better for AKS nodes, network policies are a more suited, cloud-native way to control the flow of traffic for pods. As pods are dynamically created in an AKS cluster, required network policies can be automatically applied.

For more information, see [Secure traffic between pods using network policies in Azure Kubernetes Service (AKS)](use-network-policies).

## Next steps

To get started with AKS networking, create and configure an AKS cluster with your own IP address ranges using [Azure CNI Overlay](azure-cni-overlay) or [Azure CNI](configure-azure-cni).

For associated best practices, see [Best practices for network connectivity and security in AKS](operator-best-practices-network).

For more information on core Kubernetes and AKS concepts, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-nfs -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-vertical-pod-autoscaler -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/best-practices-cost -->

# Best practices for cost optimization in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Cost optimization is about maximizing the value of resources while minimizing unnecessary expenses within your cloud environment. This process involves identifying cost effective configuration options and implementing best practices to improve operational efficiency. An AKS environment can be optimized to minimize cost while taking into account performance and reliability requirements.

In this article, you learn about:

- Holistic monitoring and FinOps practices.
- Strategic infrastructure selection.
- Dynamic rightsizing and autoscaling.
- Leveraging Azure discounts for substantial savings.

## Embrace FinOps to build a cost saving culture

[Financial operations (FinOps)](https://www.finops.org/introduction/what-is-finops/) is a discipline that combines financial accountability with cloud management and optimization. It focuses on driving alignment between finance, operations, and engineering teams to understand and control cloud costs. The FinOps foundation has several notable projects, such as the [ FinOps Framework](https://finops.org/framework) and the

[.](https://focus.finops.org/)

**FOCUS Specification**For more information, see [What is FinOps?](/en-us/azure/cost-management-billing/finops/)

## Prepare the application environment

### Evaluate SKU family

It's important to evaluate the resource requirements of your application before deployment. Small development workloads have different infrastructure needs than large production ready workloads. While a combination of CPU, memory, and networking capacity configurations heavily influences the cost effectiveness of a SKU, consider the following virtual machine (VM) types:

| SKU family | Description | Use case |
|---|---|---|
Azure Spot Virtual Machines |

[Spot node pools](spot-node-pool)and deployed to a single fault domain with no high availability or service-level agreement (SLA) guarantees. Spot VMs allow you to take advantage of unutilized Azure capacity with significant discounts (up to 90%, as compared to pay-as-you-go prices). If Azure needs capacity back, the Azure infrastructure evicts the Spot nodes.**Arm-based processors (Arm64)**[Arm64 node pool support in AKS](use-arm64-vms), you can create Arm64 Ubuntu agent nodes and even mix Intel and ARM architecture nodes within a cluster. These ARM VMs are engineered to efficiently run dynamic, scalable workloads and can deliver up to 50% better price-performance than comparable x86-based VMs for scale-out workloads.**GPU optimized SKUs**[GPU-enabled Linux node pools on AKS](gpu-cluster)are best for compute-intensive workloads like graphics rendering, large model training, and inferencing.Note

The cost of compute varies across regions. When picking a less expensive region to run workloads, be conscious of the potential impact of latency as well as data transfer costs. To learn more about VM SKUs and their characteristics, see [Sizes for virtual machines in Azure](/en-us/azure/virtual-machines/sizes).

### Review storage options

For more information on storage options and related cost considerations, see the following articles:

[Best practices for storage and backups in Azure Kubernetes Service (AKS)](operator-best-practices-storage)[Storage options for applications in Azure Kubernetes Service (AKS)](concepts-storage)

### Use cluster preset configurations

It can be difficult to pick the right VM SKU, regions, number of nodes, and other configuration options. [Cluster preset configurations](quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal) in the Azure portal offloads this initial challenge by providing recommended configurations for different application environments that are cost-conscious and performant. The **Dev/Test** preset is best for developing new workloads or testing existing workloads. The **Production Economy** preset is best for serving production traffic in a cost-conscious way if your workloads can tolerate interruptions. Noncritical features are off by default, and the preset values can be modified at any time.

### Consider multitenancy

AKS offer flexibility in how you run multitenant clusters and isolate resources. For friendly multitenancy, you can share clusters and infrastructure across teams and business units through [ logical isolation](operator-best-practices-cluster-isolation#logically-isolated-clusters). Kubernetes

[Namespaces](concepts-clusters-workloads#namespaces)form the logical isolation boundary for workloads and resources. Sharing infrastructure reduces cluster management overhead while also improving resource utilization and pod density within the cluster. To learn more about multitenancy on AKS and to determine if it's right for your organizational needs, see

[AKS considerations for multitenancy](/en-us/azure/architecture/guide/multitenant/service/aks)and

[Design clusters for multitenancy](operator-best-practices-cluster-isolation#design-clusters-for-multi-tenancy).

Warning

Kubernetes environments aren't entirely safe for hostile multitenancy. If any tenant on the shared infrastructure can't be trusted, more planning is needed to prevent tenants from impacting the security of other services.

Consider [ physical isolation](operator-best-practices-cluster-isolation#physically-isolated-clusters) boundaries. In this model, teams or workloads are assigned to their own cluster. Added management and financial overhead will be a tradeoff.

## Build cloud native applications

### Make your container as lean as possible

A lean container refers to optimizing the size and resource footprint of the containerized application. Check that your base image is minimal and only contains the necessary dependencies. Remove any unnecessary libraries and packages. A smaller container image accelerates deployment times and increases the efficiency of scaling operations. [Artifact Streaming on AKS](artifact-streaming) allows you to stream container images from Azure Container Registry (ACR). It pulls only the necessary layer for initial pod startup, reducing the pull time for larger images from minutes to seconds.

### Enforce resource quotas

[Resource quotas](operator-best-practices-scheduler#enforce-resource-quotas) provide a way to reserve and limit resources across a development team or project. Quotas are defined on a namespace and can set on compute resources, storage resources, and object counts. When you define resource quotas, it prevents individual namespaces from consuming more resources than allocated. Resource quotas are useful for multitenant clusters where teams are sharing infrastructure.

### Use cluster start/stop

When left unattended, small development/test clusters can accrue unnecessary costs. You can turn off clusters that don't need to run at all times using the [cluster start and stop](start-stop-cluster?tabs=azure-cli) feature. This feature shuts down all system and user node pools so you don't pay for extra compute. The state of your cluster and objects is maintained when you start the cluster again.

### Use capacity reservations

Capacity reservations allow you to reserve compute capacity in an Azure region or availability zone for any duration of time. Reserved capacity is available for immediate use until the reservation is deleted. [Associating an existing capacity reservation group to a node pool](manage-node-pools#associate-capacity-reservation-groups-to-node-pools) guarantees allocated capacity for your node pool and helps you avoid potential on-demand pricing spikes during periods of high compute demand.

## Monitor your environment and spend

### Increase visibility with Microsoft Cost Management

[Microsoft Cost Management](/en-us/azure/cost-management-billing/cost-management-billing-overview) offers a broad set of capabilities to help with cloud budgeting, forecasting, and visibility for costs both inside and outside of the cluster. Proper visibility is essential for deciphering spending trends, identifying optimization opportunities, and increasing accountability among application developers and platform teams. Enable the [AKS Cost Analysis add-on](cost-analysis) for granular cluster cost breakdown by Kubernetes constructs along with Azure Compute, Network, and Storage categories.

### Azure Monitor

If you're ingesting metric data via Container insights, we recommend migrating to managed Prometheus, which offers a significant cost reduction. You can [disable Container insights metrics using the data collection rule (DCR)](/en-us/azure/azure-monitor/containers/container-insights-data-collection-dcr?tabs=portal) and deploy the [managed Prometheus add-on](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana), which supports configuration via Azure Resource Manager, Azure CLI, Azure portal, and Terraform.

For more information, see [Azure Monitor best practices](/en-us/azure/azure-monitor/best-practices-containers#cost-optimization) and [managing costs for Container insights](/en-us/azure/azure-monitor/containers/container-insights-cost).

### Log Analytics

For control plane logs, consider disabling the categories you don't need and/or using the Basic Logs API when applicable to reduce Log Analytics costs. For more information, see [Azure Kubernetes Service (AKS) control plane/resource logs](monitor-aks#aks-control-plane-resource-logs). For data plane logs, or *application logs*, consider adjusting the [cost optimization settings](monitor-aks#aks-data-plane-container-insights-logs).

You can also use [Transformations in Azure Monitor](/en-us/azure/azure-monitor/data-collection/data-collection-transformations) to filter or modify control plane and data plane logs before they are sent to a Log Analytics workspace. For more information on how to create a transformation see [Create a transformation in Azure Monitor](/en-us/azure/azure-monitor/data-collection/data-collection-transformations-create?tabs=portal).

### Azure Advisor cost recommendations

AKS cost recommendations in Azure Advisor provide recommendations to help you achieve cost-efficiency without sacrificing reliability. Advisor analyzes your resource configurations and recommends optimization solutions. For more information, see [Get Azure Kubernetes Service (AKS) cost recommendations in Azure Advisor](cost-advisors).

## Optimize workloads through autoscaling

### Establish a baseline

Before configuring your autoscaling settings, you can use [Azure Load Testing](/en-us/azure/load-testing/overview-what-is-azure-load-testing) to establish a baseline for your application. Load testing helps you understand how your application behaves under different traffic conditions and identify performance bottlenecks. Once you have a baseline, you can configure autoscaling settings to ensure your application can handle the expected load.

### Enable application autoscaling

#### Vertical pod autoscaling

Requests and limits that are higher than actual usage can result in overprovisioned workloads and wasted resources. In contrast, requests and limits that are too low can result in throttling and workload issues due to lack of memory. The [Vertical Pod Autoscaler (VPA)](vertical-pod-autoscaler) allows you to fine-tune CPU and memory resources required by your pods. VPA provides recommended values for CPU and memory requests and limits based on historical container usage, which you can set manually or update automatically. * Best for applications with fluctuating resource demands*. VPA’s recommendation-only

*off mode*allows teams to review resource suggestions without enforcing them automatically. This mode can be enabled during testing, and VPA recommendations can be used to set the CPU and memory request and limits for production environments.

#### Horizontal pod autoscaling

The [Horizontal Pod Autoscaler (HPA)](concepts-scale#horizontal-pod-autoscaler) dynamically scales the number of pod replicas based on observed metrics, such as CPU or memory utilization. During periods of high demand, HPA scales out, adding more pod replicas to distribute the workload. During periods of low demand, HPA scales in, reducing the number of replicas to conserve resources. * Best for applications with predictable resource demands*.

Warning

You shouldn't use the VPA with the HPA on the same CPU or memory metrics. This combination can lead to conflicts, as both autoscalers attempt to respond to changes in demand using the same metrics. However, you can use the VPA for CPU or memory with the HPA for custom metrics to prevent overlap and ensure that each autoscaler focuses on distinct aspects of workload scaling.

#### Kubernetes event-driven autoscaling

The [Kubernetes Event-driven Autoscaler (KEDA) add-on](keda-about) provides extra flexibility to scale based on various event-driven metrics that align with your application behavior. For example, for a web application, KEDA can monitor incoming HTTP request traffic and adjust the number of pod replicas to ensure the application remains responsive. For processing jobs, KEDA can scale the application based on message queue length. Managed support is provided for all [Azure Scalers](https://keda.sh/docs/2.13/scalers/). KEDA also allows you to scale down to 0 replicas, especially helpful for sporadic event-driven workloads, periodic machine learning (ML) or GPU workloads, and dev/test or low traffic environments.

### Enable infrastructure autoscaling

#### Cluster autoscaling

To keep up with application demand, the [Cluster Autoscaler](cluster-autoscaler-overview) watches for pods that can't be scheduled due to resource constraints and scales the number of nodes in the node pool accordingly. When nodes don't have running pods, the Cluster Autoscaler scales down the number of nodes. The Cluster Autoscaler profile settings apply to all autoscaler-enabled node pools in a cluster. For more information, see [Cluster Autoscaler best practices and considerations](cluster-autoscaler-overview#best-practices-and-considerations).

#### Node autoprovisioning

Complicated workloads might require several node pools with different VM size configurations to accommodate CPU and memory requirements. Accurately selecting and managing several node pool configurations adds complexity and operational overhead. [Node Autoprovision (NAP)](node-autoprovision?tabs=azure-cli) simplifies the SKU selection process and decides the optimal VM configuration based on pending pod resource requirements to run workloads in the most efficient and cost effective manner.

Note

For more information on scaling best practices, see [Performance and scaling for small to medium workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale) and [Performance and scaling best practices for large workloads in Azure Kubernetes Service (AKS)](best-practices-performance-scale-large).

## Save with Azure discounts

### Azure Reservations

If your workload is predictable and exists for an extended period of time, consider purchasing an [Azure Reservation](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations) to further reduce your resource costs. Azure Reservations operate on a one-year or three-year term, offering up to 72% discount as compared to pay-as-you-go prices for compute. Reservations automatically apply to matching resources. * Best for workloads that are committed to running in the same SKUs and regions over an extended period of time*.

### Azure Savings Plan

If you have consistent spend, but your use of disparate resources across SKUs and regions makes Azure Reservations infeasible, consider purchasing an [Azure Savings Plan](/en-us/azure/cost-management-billing/savings-plan/savings-plan-compute-overview). Like Azure Reservations, Azure Savings Plans operate on a one-year or three-year term and automatically apply to any resources within benefit scope. You commit to spend a fixed hourly amount on compute resources irrespective of SKU or region. * Best for workloads that utilize different resources and/or different data center regions*.

### Azure Hybrid Benefit

[Azure Hybrid Benefit for Azure Kubernetes Service (AKS)](azure-hybrid-benefit) allows you to maximize your on-premises licenses at no extra cost. Use any qualifying on-premises licenses that also have an active Software Assurance (SA) or a qualifying subscription to get Windows VMs on Azure at a reduced cost.

## Next steps

Cost optimization is an ongoing and iterative effort. Learn more by reviewing the following recommendations and architecture guidance:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/postgresql-ha-overview -->

# Overview of deploying a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this guide, you deploy a highly available PostgreSQL cluster that spans multiple Azure availability zones on AKS with Azure CLI.

This article walks through the prerequisites for setting up a PostgreSQL cluster on [Azure Kubernetes Service (AKS)](what-is-aks) and provides an overview of the full deployment process and architecture.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Prerequisites

- This guide assumes a basic understanding of
[core Kubernetes concepts](concepts-clusters-workloads)and[PostgreSQL](https://www.postgresql.org/). - You need the
**Owner**or**User Access Administrator**and the**Contributor**[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles)on a subscription in your Azure account.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


You also need the following resources installed:

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.56 or later.[jq](https://jqlang.github.io/jq/), version 1.5 or later.[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)version 1.21.0 or later.[Helm](https://helm.sh/docs/intro/install/)version 3.0.0 or later.[openssl](https://www.openssl.org/)version 3.3.0 or later.[Visual Studio Code](https://code.visualstudio.com/Download)or equivalent.[Krew](https://krew.sigs.k8s.io/)version 0.4.4 or later.[kubectl CloudNativePG (CNPG) Plugin](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew).


## Deployment process

In this guide, you learn how to:

- Use Azure CLI to create a multi-zone AKS cluster.
- Deploy a highly available PostgreSQL cluster and database using the
[CNPG operator](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew). - Set up monitoring for PostgreSQL using Prometheus and Grafana.
- Deploy a sample dataset to a PostgreSQL database.
- Perform PostgreSQL and AKS cluster upgrades.
- Simulate a cluster interruption and PostgreSQL replica failover.
- Perform backup and restore of a PostgreSQL database.

## Deployment architecture

This diagram illustrates a PostgreSQL cluster setup with one primary replica and two read replicas managed by the [CloudNativePG (CNPG)](https://cloudnative-pg.io/) operator. The architecture provides a highly available PostgreSQL running on an AKS cluster that can withstand a zone outage by failing over across replicas.

Backups are stored on [Azure Blob Storage](/en-us/azure/storage/blobs/), providing another way to restore the database in the event of an issue with streaming replication from the primary replica.

You might choose to host PostgreSQL on AKS when you need full control over database configuration, extensions, and deployment architecture. It’s ideal for integrating tightly with Kubernetes-native tooling, optimizing costs at scale, and fine-tuning performance through custom resource allocation, caching strategies, and storage configurations tailored to your workload.

Note

For applications that require data separation at the database level, you can add more databases with postInitSQL commands and similar. It's currently not possible to add more databases in a declarative way with the CNPG operator. [Learn more](https://github.com/cloudnative-pg/cloudnative-pg) about the CNPG operator.

### Storage considerations

The type of storage you use can have large effects on PostgreSQL performance. Later in this guide, you select the option best suited for your goals and performance needs.

| Storage type | Compatible driver | Description |
|---|---|---|
|

**Maximum data resiliency**. Azure Premium SSD delivers high-performance storage and seamlessly works with Azure Premium zone-redundant storage (ZRS). Premium SSD is provisioned based on specific sizes, which each offer certain IOPS and throughput levels.[Premium SSD v2](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2)**Best price-performance**. Azure Premium SSD v2 offers higher performance than Azure Premium SSDs while also generally being less costly. Unlike Premium SSDs, Premium SSD v2 doesn't have dedicated sizes. You can set a Premium SSD v2 to any supported size you prefer, and make granular adjustments to the performance without downtime. Azure Premium SSD v2 disks have certain limitations that you should be aware of. For a complete list, see[Premium SSD v2 limitations](/en-us/azure/virtual-machines/disks-types#premium-ssd-v2-limitations).[Local NVMe or temp SSD (Ephemeral Disks)](/en-us/azure/storage/container-storage/use-container-storage-with-local-disk#what-is-ephemeral-disk)**Maximum performance**. Ephemeral Disks are local NVMe and temporary SSD storage available on select VM families. They offer the highest possible IOPS, throughput, and submillisecond latency for your AKS cluster. You can also take advantage of Ephemeral Disks' high performance using[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction), a managed Kubernetes storage solution that dynamically provisions persistent volumes for stateful workloads like PostgreSQL. However, because these disks reside on the local VMs hosting the cluster, data isn't persisted to an Azure storage service. As a result, any data stored on these disks will be lost if the cluster is stopped or deallocated. To address this limitation, later sections in this guide show you how to set up periodic backups of your PostgreSQL data to[Azure Blob Storage](/en-us/azure/storage/blobs/).## Next steps

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2
- Adam Sharif | Customer Engineer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-configuration-options -->

# Azure Key Vault provider for Secrets Store CSI Driver for AKS configuration and troubleshooting options

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Key Vault provider for Secrets Store Container Storage Interface (CSI) Driver enables secure and automated management of secrets in Azure Kubernetes Service (AKS). This article provides guidance on configuring the provider, troubleshooting common issues, and optimizing secret handling in your AKS environment.

## Prerequisites

Follow the steps in the following articles before proceeding with this guide. Once you complete these steps, you can apply extra configurations or perform troubleshooting on your AKS cluster.

[Use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster](csi-secrets-store-driver)[Provide an identity to access the Azure Key Vault provider for Secrets Store CSI Driver in AKS](csi-secrets-store-identity-access)

## Configuration options

### Manage auto rotation

Once you enable auto rotation for Azure Key Vault Secrets Provider, it updates the pod mount and the Kubernetes secret defined in the `secretObjects`

field of `SecretProviderClass`

. It does so by polling for changes periodically, based on the rotation poll interval you defined. The default rotation poll interval is *two minutes*. When a secret is updated in the external secrets store after the initial pod deployment, both the Kubernetes Secret and the pod mount are periodically refreshed. The update frequency and method depend on how your application accesses the secret data.

**Mount the Kubernetes Secret as a volume**: Use the auto rotation and sync K8s secrets features of Secrets Store CSI Driver. The application needs to watch for changes from the mounted Kubernetes Secret volume. When the CSI Driver updates the Kubernetes Secret, the corresponding volume contents automatically update as well.**Application reads the data from the container filesystem**: Use the rotation feature of Secrets Store CSI Driver. The application needs to watch for the file change from the volume mounted by the CSI driver.**Use the Kubernetes Secret for an environment variable**: Restart the pod to get the latest secret as an environment variable. Use a tool such as[Reloader](https://github.com/stakater/Reloader)to watch for changes on the synced Kubernetes Secret and perform rolling upgrades on pods.

To enable auto rotation of secrets on a new AKS cluster using the

command and enable the`az aks create`

`enable-secret-rotation`

add-on, run the following command:`az aks create \ --name myAKSCluster2 \ --resource-group myResourceGroup \ --enable-addons azure-keyvault-secrets-provider \ --enable-secret-rotation \ --generate-ssh-keys`

To update an existing AKS cluster to enable auto rotation of secrets using the

command and the`az aks addon update`

`enable-secret-rotation`

parameter, run the following command:`az aks addon update --resource-group myResourceGroup --name myAKSCluster2 --addon azure-keyvault-secrets-provider --enable-secret-rotation`


### Sync mounted content with a Kubernetes secret

Note

The YAML examples in this section are incomplete. You need to modify them to support your chosen method of access to your key vault identity. For details, see [Provide an identity to access the Azure Key Vault provider for Secrets Store CSI Driver](csi-secrets-store-identity-access).

You might want to create a Kubernetes secret to mirror your mounted secrets content. Your secrets sync after you start a pod to mount them. When you delete the pods that consume the secrets, your Kubernetes secret is also deleted.

Sync mounted content with a Kubernetes secret using the `secretObjects`

field when creating a `SecretProviderClass`

to define the desired state of the Kubernetes secret, as shown in the
following example YAML. Make sure the `objectName`

in the `secretObjects`

field matches the file name of the mounted content. If you use `objectAlias`

instead, it should match the object alias.

```
apiVersion: secrets-store.csi.x-k8s.io/v1
kind: SecretProviderClass
metadata:
name: azure-sync
spec:
provider: azure
secretObjects: # [OPTIONAL] SecretObjects defines the desired state of synced Kubernetes secret objects
- data:
- key: username # data field to populate
objectName: foo1 # name of the mounted content to sync; this could be the object name or the object alias
secretName: foosecret # name of the Kubernetes secret object
type: Opaque # type of Kubernetes secret object (for example, Opaque, kubernetes.io/tls)
```


### Set an environment variable to reference Kubernetes secrets

Note

The example YAML demonstrates how to access a secret using either environment variables or `volume/volumeMount`

. Typically, an application uses one method or the other. However, to make a secret available through environment variables, at least one pod must mount the secret.

Reference your newly created Kubernetes secret by setting an environment variable in your pod, as shown in the following example YAML.

```
kind: Pod
apiVersion: v1
metadata:
name: busybox-secrets-store-inline
spec:
containers:
- name: busybox
image: registry.k8s.io/e2e-test-images/busybox:1.29-1
command:
- "/bin/sleep"
- "10000"
volumeMounts:
- name: secrets-store01-inline
mountPath: "/mnt/secrets-store"
readOnly: true
env:
- name: SECRET_USERNAME
valueFrom:
secretKeyRef:
name: foosecret
key: username
volumes:
- name: secrets-store01-inline
csi:
driver: secrets-store.csi.k8s.io
readOnly: true
volumeAttributes:
secretProviderClass: "azure-sync"
```


### Migrate from open-source to AKS-managed Secrets Store CSI Driver

Uninstall the open-source Secrets Store CSI Driver using the following

`helm delete`

command:`helm delete <release name>`

Tip

If you installed the driver and provider using deployment YAMLs, you can delete the components using the following

`kubectl delete`

command:`# Delete AKV provider pods from Linux nodes kubectl delete -f https://raw.githubusercontent.com/Azure/secrets-store-csi-driver-provider-azure/master/deployment/provider-azure-installer.yaml # Delete AKV provider pods from Windows nodes kubectl delete -f https://raw.githubusercontent.com/Azure/secrets-store-csi-driver-provider-azure/master/deployment/provider-azure-installer-windows.yaml`

Upgrade your existing AKS cluster with the feature using the

command:`az aks enable-addons`

`az aks enable-addons --addons azure-keyvault-secrets-provider --name myAKSCluster --resource-group myResourceGroup`


## Access metrics

You can monitor the health and performance of the Azure Key Vault provider for Secrets Store CSI Driver by collecting metrics it exposes. These metrics provide insights into request durations, error rates, and the overall operation of the provider and driver components, helping you troubleshoot issues and optimize your AKS cluster's secret management.

Metrics are served via Prometheus from port 8898, but this port isn't exposed outside the pod by default. Access the metrics over localhost using the `kubectl port-forward`

command:

```
kubectl port-forward -n kube-system ds/aks-secrets-store-provider-azure 8898:8898 & curl localhost:8898/metrics
```


These metrics help you monitor the performance and reliability of the Azure Key Vault provider including request latency and error tracking for both Key Vault and gRPC operations.

| Metric | Description | Tags |
|---|---|---|
| keyvault_request | The distribution of how long it took to get from the key vault. | `os_type=<runtime os>` , `provider=azure` , `object_name=<keyvault object name>` , `object_type=<keyvault object type>` , `error=<error if failed>` |
| grpc_request | The distribution of how long it took for the gRPC requests. | `os_type=<runtime os>` , `provider=azure` , `grpc_method=<rpc full method>` , `grpc_code=<grpc status code>` , `grpc_message=<grpc status message>` |

## Troubleshooting

For troubleshooting steps, see [Troubleshoot Azure Key Vault Provider for Secrets Store CSI Driver](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-key-vault-csi-secrets-store-csi-driver).

## Next steps

To learn more about the Azure Key Vault provider for Secrets Store CSI Driver, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-acr -->

# Tutorial - Create an Azure Container Registry (ACR) and build images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Container Registry (ACR) is a private registry for container images. A private container registry allows you to securely build and deploy your applications and custom code.

In this tutorial, you deploy an ACR instance and push a container image to it. You learn how to:

- Create an ACR instance.
- Use
[ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-overview)to build and push container images to ACR. - View images in your registry.

## Before you begin

In the [previous tutorial](tutorial-kubernetes-prepare-app), you used Docker to create a container image for a simple Azure Store Front application. If you haven't created the Azure Store Front app image, return to [Tutorial 1 - Prepare an application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an Azure Container Registry

Before creating an ACR instance, you need a resource group. An Azure resource group is a logical container into which you deploy and manage Azure resources.

Important

This tutorial uses *myResourceGroup* as a placeholder for the resource group name. If you want to use a different name, replace *myResourceGroup* with your own resource group name.

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location westus2`

Create an ACR instance using the

command and provide your own unique registry name. The registry name must be unique within Azure and contain 5-50 lowercase alphanumeric characters. This tutorial series uses an environment variable,`az acr create`

`$ACRNAME`

, as a placeholder for the container registry name. You can set this environment variable to your unique ACR name to use in future commands. The*Basic*SKU is a cost-optimized entry point for development purposes that provides a balance of storage and throughput.`az acr create --resource-group myResourceGroup --name $ACRNAME --sku Basic`


## Build and push container images to registry

Build and push the images to your ACR using the Azure CLI

command.`az acr build`

Note

For this step, there isn't an equivalent Azure PowerShell cmdlet that performs this task.

In the following example, we don't build the

`product-service`

image. This image can take a long time to build, and there's a container image already available in the GitHub Container Registry (GHCR). You can use thecommand to import the image from the GHCR to your ACR instance. We also don't build the`az acr import`

`rabbitmq`

image. This image is available from the Docker Hub public repository and doesn't need to be built or pushed to your ACR instance.`az acr import --name $ACRNAME --source ghcr.io/azure-samples/aks-store-demo/product-service:latest --image aks-store-demo/product-service:latest az acr build --registry $ACRNAME --image aks-store-demo/order-service:latest ./src/order-service/ az acr build --registry $ACRNAME --image aks-store-demo/store-front:latest ./src/store-front/`


## List images in registry

View the images in your ACR instance using the

command.`az acr repository list`

`az acr repository list --name $ACRNAME --output table`

The following example output lists the available images in your registry:

`Result ---------------- aks-store-demo/product-service aks-store-demo/order-service aks-store-demo/store-front`


## Next steps

In this tutorial, you created an ACR and pushed images to it to use in an AKS cluster. You learned how to:

- Create an ACR instance.
- Use
[ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-overview)to build and push container images to ACR. - View images in your registry.

In the next tutorial, you learn how to deploy a Kubernetes cluster in Azure.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-metrics-managed-prometheus -->

# Collect metrics for Istio service mesh add-on workloads for Azure Kubernetes Service in Azure Managed Prometheus

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This guide explains how to set up and use Azure Managed Prometheus to collect metrics from Istio service mesh add-on workloads on your Azure Kubernetes cluster.

## Prerequisites

Complete steps to enable the Istio add-on on the cluster as per

[documentation](istio-deploy-addon)

## Enable Azure Monitor managed service for Prometheus

Azure Monitor managed service for Prometheus collects data from Azure Kubernetes cluster.
To enable Azure Monitor managed service for Prometheus, you must create an [Azure Monitor workspace](/en-us/azure/azure-monitor/essentials/azure-monitor-workspace-manage?tabs=cli#create-an-azure-monitor-workspace) to store the metrics:

```
export AZURE_MONITOR_WORKSPACE=<azure-monitor-workspace-name>
export AZURE_MONITOR_WORKSPACE_ID=$(az monitor account create \
--name $AZURE_MONITOR_WORKSPACE \
--resource-group $RESOURCE_GROUP \
--location $LOCATION \
--query id -o tsv)
```


### Enable Prometheus addon

To collect Prometheus metrics from your Kubernetes cluster, [enable Prometheus addon](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable?tabs=cli#enable-with-cli):

```
az aks update --enable-azure-monitor-metrics --name $CLUSTER --resource-group $RESOURCE_GROUP --azure-monitor-workspace-resource-id $AZURE_MONITOR_WORKSPACE_ID
```


### Customize scraping of Prometheus metrics in Azure Monitor managed service

Create a scrape config in a file named `prometheus-config`

, similar to the sample provided below. This configuration enables pod annotation-based scraping, which allows Prometheus to automatically discover and scrape metrics from pods with specific annotations.

Important

The scrape config below is just an example. We **highly** recommend customizing it based on your needs. If not adjusted, it could lead to unexpected costs from frequent metric collection and increased data storage.

```
global:
scrape_interval: 30s
scrape_configs:
- job_name: workload
scheme: http
kubernetes_sd_configs:
- role: endpoints
relabel_configs:
- source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_scrape]
action: keep
regex: true
- source_labels: [__meta_kubernetes_pod_annotation_prometheus_io_path]
action: replace
target_label: __metrics_path__
regex: (.+)
- source_labels: [__address__, __meta_kubernetes_pod_annotation_prometheus_io_port]
action: replace
regex: ([^:]+)(?::\d+)?;(\d+)
replacement: $1:$2
target_label: __address__
```


To [enable pod annotation-based scraping](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration), create configmap `ama-metrics-prometheus-config`

that references `prometheus-config`

file in `kube-system`

namespace.

```
kubectl create configmap ama-metrics-prometheus-config --from-file=prometheus-config -n kube-system
```


### Verify Metric Collection

Configure access permissions: navigate to your Azure Monitor workspace in Azure portal and create role assignment for yourself to grant 'Monitoring Data Reader' role on the workspace resource.

Generate sample traffic: send a few requests to the product page created earlier, for example:

`curl -s "http://${GATEWAY_URL_EXTERNAL}/productpage" | grep -o "<title>.*</title>"`

View/Query metrics in Azure portal: navigate to Prometheus explorer under your Azure Monitor workspace and

[query metrics](/en-us/azure/azure-monitor/essentials/prometheus-workbooks). The example below shows results for query`istio_requests_total`

.

## Delete resources

If you want to clean up the Istio service mesh and the ingresses (leaving behind the cluster), run the following command:

```
az aks mesh disable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


If you want to clean up all the resources created from the Istio how-to guidance documents, run the following command:

```
az group delete --name ${RESOURCE_GROUP} --yes --no-wait
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-wireguard-encryption-concepts -->

# In transit encryption with WireGuard (public preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As organizations increasingly rely on Azure Kubernetes Service (AKS) to run containerized workloads, ensuring the security of network traffic between applications and services becomes essential especially in regulated or security-sensitive environments. In-transit encryption with WireGuard protects data as it moves between pods and nodes, mitigating risks of interception or tampering. WireGuard is known for its simplicity, and robust cryptography, offers a powerful solution for securing communication within AKS clusters.

WireGuard encryption for AKS is part of the [Advanced Container Networking Services (ACNS)](advanced-container-networking-services-overview) feature set, and its implementation is based on [Cilium](https://docs.cilium.io/en/stable/security/network/encryption-wireguard/).

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## WireGuard encryption scope

WireGuard in-transit encryption in AKS is designed to secure specific traffic flows within your Kubernetes cluster. This section outlines which traffic types are encrypted and which aren't currently supported via Advanced Container Networking Services(ACNS).

Supported/Encrypted traffic flows:

- Inter-node pod traffic: Traffic leaving a pod from one node destined to a pod on another node.

Unsupported/Unencrypted traffic flows

- Same-node pod traffic: Traffic between pods on the same node
- Node-network traffic: traffic generated by the node itself destined to another node

## Architecture overview

WireGuard encryption relies on [Azure CNI powered by cilium](azure-cni-powered-by-cilium) to secure inter-node communications within a distributed system. The architecture uses a dedicated WireGuard agent that orchestrates key management, interface configuration, and dynamic peer updates. This section attempts to provide a detailed explanation

### WireGuard agent

Upon startup, the Cilium agent evaluates its configuration to determine if encryption is enabled. When WireGuard is selected as the encryption mode, the agent initializes a dedicated WireGuard subsystem. The wireguard agent is responsible for configuring and initializing components required for enforcing WireGuard encryption.

### Key generation

A fundamental requirement to secure communication is the generation of cryptographic key pairs. Each node in the Kubernetes cluster will automatically generate a unique WireGuard key pair during the initialization phase and distributes its public key via the “network.cilium.io/wg-pub-key” annotation in the Kubernetes CiliumNode custom resource object. The key pairs are stored in memory and rotated every 120 seconds. The private key serves as the node’s confidential identity. The public key is shared with the peer nodes in the cluster to decrypt and encrypt traffic from and to Cilium-managed endpoints running on that node. These keys are managed entirely by Azure, not by the customer, ensuring secure and automated handling without requiring manual intervention. This mechanism ensures that only nodes with validated credentials can participate in the encrypted network.

### Interface creation

Once the key generation process concludes, the WireGuard agent configures a dedicated network interface (cilium_wg0). This process involves interface creation and configuration with the previously generated private key.

## Comparison with virtual network encryption

Azure offers multiple options for securing in-transit traffic in AKS, including [virtual network level encryption](/en-us/azure/virtual-network/virtual-network-encryption-overview) and WireGuard-based encryption. While both approaches enhance the confidentiality and integrity of network traffic, they differ in scope, flexibility, and deployment requirements. This section helps you understand when to use each solution.

**Use virtual network encryption when**

**You require full network-layer encryption for all traffic within the virtual network:**Virtual network encryption ensures that all traffic regardless of workload or orchestration layer is automatically encrypted as it traverses the Azure Virtual Network.**You need minimal performance overhead:**Virtual network encryption uses hardware acceleration in supported VM SKUs, offloading encryption from the OS to the underlying hardware. This design delivers high throughput with low CPU usage.**All your virtual machines support virtual network encryption:**Virtual network encryption depends on VM SKUs that support the necessary hardware acceleration. If your infrastructure consists entirely of supported SKUs, virtual network encryption can be seamlessly enabled.**Your AKS Network configurations supports virtual network encryption:**Virtual network encryption has some limitations when it comes to aks pod networking. For more information, see[Virtual network encryption supported scenarios](/en-us/azure/virtual-network/virtual-network-encryption-overview#supported-scenarios)

**Use WireGuard encryption When**

**You want to make sure that your application traffic is encrypted across all node**virtual network encryption does not encrypt traffic between nodes on the same physical host.**You want to unify encryption across multi-cloud or hybrid environments:**WireGuard offers a cloud-agnostic solution, enabling consistent encryption across clusters running in different cloud providers or on-premises.**You don’t need or want to encrypt all traffic within the virtual network:**WireGuard enables a more targeted encryption strategy ideal for securing sensitive workloads without incurring the overhead of encrypting all traffic.**Some of your VM SKUs don’t support virtual network encryption:**WireGuard is implemented in software and works regardless of VM hardware support, making it a practical option for heterogeneous environments.

## Considerations & limitations

• WireGuard isn't [FIPS](https://csrc.nist.gov/pubs/fips/140-2/upd2/final) compliant.
• WireGuard encryption doesn't apply to pods uses host networking (spec.hostNetwork: true) because these pods use the host identity instead of having individual identities.

Important

WireGuard encryption operates at the software level, which can introduce latency and impact throughput performance. The extent of this impact depends on various factors, including VM size (node SKU), network configuration, and application traffic patterns. Our benchmarking indicates that throughput is limited to 1.5 Gbps with an MTU of 1500; however, results may vary depending on workload characteristics and cluster configuration. Using a SKU that supports MTU 3900 resulted in approximately 2.5x higher throughput. While WireGuard encryption can be used alongside network policies, doing so may lead to further performance degradation, with reduced throughput and increased latency. For applications sensitive to latency or throughput, we strongly recommend evaluating WireGuard in a non-production environment first. As always, results may vary based on workload characteristics and cluster configuration.

## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[WireGuard encryption](how-to-apply-wireguard)on AKS.For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](container-network-observability-metrics).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/intro-aks-automatic -->

# What is Azure Kubernetes Service (AKS) Automatic?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

Azure Kubernetes Service (AKS) Automatic offers an experience that makes the most common tasks on Kubernetes fast and frictionless, while preserving the flexibility, extensibility, and consistency of Kubernetes. Azure takes care of your cluster setup, including node management, scaling, security, and preconfigured settings that follow AKS well-architected recommendations. Automatic clusters dynamically allocate compute resources based on your specific workload requirements and are tuned for running production applications.

**Production ready by default**: Clusters are preconfigured for optimal production use, suitable for most applications. They offer fully managed node pools that automatically allocate and scale resources based on your workload needs. Pods are bin packed efficiently, to maximize resource utilization.**Built-in best practices and safeguards**: AKS Automatic clusters have a hardened default configuration, with many cluster, application, and networking security settings enabled by default. AKS automatically patches your nodes and cluster components while adhering to any planned maintenance schedules.**Code to Kubernetes in minutes**: Go from a container image to a deployed application that adheres to best practices patterns within minutes, with access to the comprehensive capabilities of the Kubernetes API and its rich ecosystem.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## AKS Automatic and Standard feature comparison

The following table provides a comparison of options that are available, preconfigured, and default in both AKS Automatic and AKS Standard. For more information on whether specific features are available in Automatic, you can check the documentation for that feature.

**Preconfigured** features are always enabled and you can't disable or change their settings. **Default** features are configured for you but can be changed. **Optional** features are available for you to configure and aren't enabled by default.

When enabling optional features, you can follow the linked feature documentation. When you reach a step for cluster creation, follow steps to create an [AKS Automatic cluster](learn/quick-kubernetes-automatic-deploy) instead of creating an AKS Standard cluster.

### Application deployment, monitoring, and observability

Application deployment can be streamlined using [automated deployments](automated-deployments) from source control, which creates Kubernetes manifest and generates CI/CD workflows. Additionally, the cluster is configured with monitoring tools such as Managed Prometheus for metrics, Managed Grafana for visualization, and Container Insights for log collection.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Application deployment | Optional: * Use
* Create deployment pipelines using
* Bring your own CI/CD pipeline. |
Optional: * Use
* Create deployment pipelines using
* Bring your own CI/CD pipeline. |
| Monitoring, logging, and visualization | Default: *
*
*
*
Optional: *
|
Default:
Optional: *
*
*
*
|

### Node management, scaling, and cluster operations

Node management is automatically handled without the need for manual node pool creation. Scaling is seamless, with nodes created based on workload requests. Additionally, features for workload scaling like Horizontal Pod Autoscaler (HPA), [Kubernetes Event Driven Autoscaling (KEDA)](keda-about), and [Vertical Pod Autoscaler (VPA)](vertical-pod-autoscaler) are enabled. Clusters are configured for automatic node repair, automatic cluster upgrades, and detection of deprecated Kubernetes standard API usage. You can also set a planned maintenance schedule for upgrades if needed.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Node management | Preconfigured: AKS Automatic manages the node pools using
|
Default: You create and manage system and user node pools Optional: AKS Standard manages user node pools using
|
| Scaling | Preconfigured: AKS Automatic creates nodes based on workload requests using
|
Default: Manual scaling of node pools. Optional: *
*
*
*
|
| Cluster tier and Service Level Agreement (SLA) | Preconfigured: Standard tier cluster with up to 5,000 nodes, a
|
Default: Free tier cluster with 10 nodes but can support up to 1,000 nodes. Optional: * Standard tier cluster with up to 5,000 nodes and a
* Premium tier cluster with up to 5,000 nodes,
|
| Node operating system | Preconfigured:
|
Default: Ubuntu Optional: *
*
|
| Node resource group | Preconfigured: Fully managed node resource group to prevent accidental or intentional changes to cluster resources. |
Default: Unrestricted Optional:
|
| Node auto-repair | Preconfigured: Continuously monitors the health state of worker nodes and performs
|
Preconfigured: Continuously monitors the health state of worker nodes and performs
|
| Cluster upgrades | Preconfigured: Clusters are
|
Default: Manual upgrade. Optional: Automatic upgrade using a selectable
|
| Kubernetes API breaking change detection | Preconfigured: Cluster upgrades are stopped on detection of
|
Preconfigured: Cluster upgrades are stopped on detection of
|
| Planned maintenance windows | Default: Set
|
Optional: Set
|

### Security and policies

Cluster authentication and authorization use [Azure Role-based Access Control (RBAC) for Kubernetes authorization](manage-azure-rbac) and applications can use features like [workload identity with Microsoft Entra Workload ID](workload-identity-overview) and [OpenID Connect (OIDC) cluster issuer](use-oidc-issuer) to have secure communication with Azure services. [Deployment safeguards](deployment-safeguards) enforce Kubernetes best practices through Azure Policy controls and the built-in [image cleaner](image-cleaner) removes unused images with vulnerabilities, enhancing image security.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Cluster authentication and authorization | Preconfigured:
|
Default: Local accounts. Optional: *
*
|
| Cluster security | Preconfigured:
|
Optional:
|
| Application security | Preconfigured: *
*
Optional:*
|
Optional: *
*
Optional:*
|
| Image security | Preconfigured:
|
Optional:
|
| Policy enforcement | Preconfigured:
Optional:*
|
Optional:
Optional:*
|
| Managed namespaces | Optional: Use
|
Optional: Use
|

### Networking

AKS Automatic clusters use [managed Virtual Network powered by Azure CNI Overlay with Cilium](azure-cni-powered-by-cilium) for high-performance networking and robust security. Ingress is handled by [managed NGINX using the application routing add-on](app-routing), integrating seamlessly with Azure DNS and Azure Key Vault. Egress uses a [managed NAT gateway](nat-gateway#create-an-aks-cluster-with-a-managed-nat-gateway) for scalable outbound connections. Additionally, you have the flexibility to enable [Istio-based service mesh add-on for AKS](istio-about) or bring your own service mesh.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Virtual network | Default:
Optional: *
*
|
Default:
Optional: *
*
*
*
|
| Ingress | Preconfigured:
Optional: *
* Bring your own ingress or gateway. |
Optional: *
*
* Bring your own ingress or gateway. |
| Egress | Preconfigured:
Optional (with custom virtual network): *
*
*
|
Default:
Optional: *
*
*
|
| Service mesh | Optional: *
* Bring your own service mesh. |
Optional: *
* Bring your own service mesh. |

## Next steps

To learn more about AKS Automatic, follow the quickstart to create a cluster.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-resource-reservations -->

# Node resource reservations in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about node resource reservations in Azure Kubernetes Service (AKS).

## Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS.

AKS reserves two types of resources, **CPU** and **memory**, on each node to maintain node performance and functionality. As a node grows larger in resources, the resource reservations also grow due to a higher need for management of user-deployed pods. Keep in mind that you can't change resource reservations on a node.

### CPU reservations

Reserved CPU is dependent on node type and cluster configuration, which might result in less allocatable CPU due to running extra features. The following table shows CPU reservations in millicores:

| CPU cores on host | 1 core | 2 cores | 4 cores | 8 cores | 16 cores | 32 cores | 64 cores |
|---|---|---|---|---|---|---|---|
| Kube-reserved CPU (millicores) | 60 | 100 | 140 | 180 | 260 | 420 | 740 |

### Memory reservations

In AKS, reserved memory consists of the sum of two values:

**AKS 1.29 and later**

has the`kubelet`

daemon*memory.available < 100 Mi*eviction rule by default. This rule ensures that a node has at least 100 Mi allocatable at all times. When a host is below that available memory threshold, the`kubelet`

triggers the termination of one of the running pods and frees up memory on the host machine.**A rate of memory reservations**set according to the lesser value of:*20 MB * Max Pods supported on the Node + 50 MB*or*25% of the total system memory resources*.**Examples**:- If the virtual machine (VM) provides 8 GB of memory and the node supports up to 30 pods, AKS reserves
*20 MB * 30 Max Pods + 50 MB = 650 MB*for kube-reserved.`Allocatable space = 8 GB - 0.65 GB (kube-reserved) - 0.1 GB (eviction threshold) = 7.25 GB or 90.625% allocatable.`

- If the VM provides 4 GB of memory and the node supports up to 70 pods, AKS reserves
*25% * 4 GB = 1000 MB*for kube-reserved, as this is less than*20 MB * 70 Max Pods + 50 MB = 1450 MB*.

For more information, see

[Configure maximum pods per node in an AKS cluster](concepts-network-ip-address-planning#maximum-pods-per-node).- If the virtual machine (VM) provides 8 GB of memory and the node supports up to 30 pods, AKS reserves

**AKS versions prior to 1.29**

has the`kubelet`

daemon*memory.available < 750 Mi*eviction rule by default. This rule ensures that a node has at least 750 Mi allocatable at all times. When a host is below that available memory threshold, the`kubelet`

triggers the termination of one of the running pods and free up memory on the host machine.**A regressive rate of memory reservations**for the kubelet daemon to properly function (*kube-reserved*).- 25% of the first 4 GB of memory
- 20% of the next 4 GB of memory (up to 8 GB)
- 10% of the next 8 GB of memory (up to 16 GB)
- 6% of the next 112 GB of memory (up to 128 GB)
- 2% of any memory more than 128 GB


Note

AKS reserves an extra 2 GB for system processes in Windows nodes that isn't part of the calculated memory.

Memory and CPU allocation rules are designed to:

- Keep agent nodes healthy, including some hosting system pods critical to cluster health.
- Cause the node to report less allocatable memory and CPU than it would report if it weren't part of a Kubernetes cluster.

For example, if a node offers 7 GB, it reports 34% of memory not allocatable including the 750 Mi hard eviction threshold.

`0.75 + (0.25*4) + (0.20*3) = 0.75 GB + 1 GB + 0.6 GB = 2.35 GB / 7 GB = 33.57% reserved`


In addition to reservations for Kubernetes itself, the underlying node OS also reserves an amount of CPU and memory resources to maintain OS functions.

For associated best practices, see [Best practices for basic scheduler features in AKS](operator-best-practices-scheduler).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-diagnostics -->

# Azure Kubernetes Service Diagnose and Solve Problems overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Troubleshooting Azure Kubernetes Service (AKS) cluster issues plays an important role in maintaining your cluster, especially if your cluster is running mission-critical workloads. AKS Diagnose and Solve Problems is an intelligent, self-diagnostic experience that:

- Helps you identify and resolve problems in your cluster.
- Requires no extra configuration or billing cost.

## Open AKS Diagnose and Solve Problems

You can access AKS Diagnose and Solve Problems using the following steps:

In the

[Azure portal](https://portal.azure.com), navigate to your AKS cluster resource.From the service menu, select

**Diagnose and solve problems**.Select a troubleshooting category tile that best describes the issue of your cluster by referring the keywords in each tile description on the homepage or typing a keyword that best describes your issue in the search bar.


## View a diagnostic report

After selecting a category, you can view various diagnostic reports that provide detailed information about the issue. The *Overview* option from the navigation menu runs all the diagnostics in that particular category and displays any issues that are found with the cluster. Select **View details** under each tile to view a detailed description of the issue, including:

- An issue summary
- Error details
- Recommended actions
- Links to helpful docs
- Related-metrics
- Logging data

### Example scenario: Diagnose connectivity issues

I observed that my application is getting disconnected or experiencing intermittent connection issues. In response, I navigate to the AKS Diagnose and Solve Problems home page and select the **Connectivity Issues** tile to investigate the potential causes.

I received a diagnostic alert indicating that the disconnection might be related to my *Cluster DNS*. To gather more information, I select **View details**.

Based on the diagnostic result, it appears that the issue might be related to known DNS issues or the VNet configuration. I can use the documentation links provided to address the issue and resolve the problem.

If the recommended documentation based on the diagnostic results doesn't resolve the issue, I can return to the previous step in Diagnostics and refer to additional documentation.

## Use AKS Diagnose and Solve Problems for best practices

Deploying applications on AKS requires adherence to best practices to guarantee optimal performance, availability, and security. The AKS Diagnose and Solve Problems **Best Practices** tile provides an array of best practices that can assist in managing various aspects, such as VM resource provisioning, cluster upgrades, scaling operations, subnet configuration, and other essential aspects of a cluster's configuration.

Leveraging the AKS Diagnose and Solve Problems can be vital in ensuring that your cluster adheres to best practices and that any potential issues are identified and resolved in a timely and effective manner. By incorporating AKS Diagnose and Solve Problems into your operational practices, you can be confident in the reliability and security of your application in production.

### Example scenario: View best practices

I'm curious about the best practices I can follow to prevent potential problems. In response, I navigate to the AKS Diagnose and Solve Problems home page and select the **Best Practices** tile.

From here, I can view the best practices that are recommended for my cluster and select **View details** to see the results.

## Next steps

- Collect logs to help you further troubleshoot your cluster issues using
[AKS Periscope](https://aka.ms/aksperiscope). - Read the
[triage practices section](/en-us/azure/architecture/operator-guides/aks/aks-triage-practices)of the AKS day-2 operations guide. - Post your questions or feedback at
[UserVoice](https://feedback.azure.com/d365community/forum/aabe212a-f724-ec11-b6e6-000d3a4f0da0). Make sure to add "[Diag]" in the title.
