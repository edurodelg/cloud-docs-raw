---
merged_at: 2026-01-25T12:25:33.976736
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: configure-kubenet.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/configure-kubenet -->

# Use kubenet networking with your own IP address ranges in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

AKS clusters use kubenet and create an Azure virtual network and subnet for you by default. With kubenet, nodes get an IP address from the Azure virtual network subnet. Pods receive an IP address from a logically different address space to the Azure virtual network subnet of the nodes. Network address translation (NAT) is then configured so the pods can reach resources on the Azure virtual network. The source IP address of the traffic is NAT'd to the node's primary IP address. This approach greatly reduces the number of IP addresses you need to reserve in your network space for pods to use.

With [Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. These IP addresses must be planned in advance and unique across your network space. Each node has a configuration parameter for the maximum number of pods it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow. You can configure the maximum pods deployable to a node at cluster creation time or when creating new node pools. If you don't specify `maxPods`

when creating new node pools, you receive a default value of *110* for kubenet.

This article shows you how to use kubenet networking to create and use a virtual network subnet for an AKS cluster. For more information on network options and considerations, see [Network concepts for Kubernetes and AKS](concepts-network).

## Prerequisites

- The virtual network for the AKS cluster must allow outbound internet connectivity.
- Don't create more than one AKS cluster in the same subnet.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the Kubernetes service address range, pod address range, or cluster virtual network address range. The range can't be updated after you create your cluster. - The cluster identity used by the AKS cluster must at least have the
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)role on the subnet within your virtual network. CLI helps set the role assignment automatically. If you're using an ARM template or other clients, you need to manually set the role assignment. You must also have the appropriate permissions, such as the subscription owner, to create a cluster identity and assign it permissions. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, you need the following permissions:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


Warning

To use Windows Server node pools, you must use Azure CNI. The kubenet network model isn't available for Windows Server containers.

## Before you begin

You need the Azure CLI version 2.0.65 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Overview of kubenet networking with your own subnet

In many environments, you have defined virtual networks and subnets with allocated IP address ranges, and you use these resources to support multiple services and applications. To provide network connectivity, AKS clusters can use *kubenet* (basic networking) or Azure CNI (*advanced networking*).

With *kubenet*, only the nodes receive an IP address in the virtual network subnet. Pods can't communicate directly with each other. Instead, User Defined Routing (UDR) and IP forwarding handle connectivity between pods across nodes. UDRs and IP forwarding configuration is created and maintained by the AKS service by default, but you can [bring your own route table for custom route management](#bring-your-own-subnet-and-route-table-with-kubenet) if you want. You can also deploy pods behind a service that receives an assigned IP address and load balances traffic for the application. The following diagram shows how the AKS nodes receive an IP address in the virtual network subnet, but not the pods:

Azure supports a maximum of *400* routes in a UDR, so you can't have an AKS cluster larger than 400 nodes. AKS [virtual nodes](virtual-nodes-cli) and Azure Network Policies aren't supported with *kubenet*. [Calico Network Policies](https://docs.projectcalico.org/v3.9/security/calico-network-policy) are supported.

With *Azure CNI*, each pod receives an IP address in the IP subnet and can communicate directly with other pods and services. Your clusters can be as large as the IP address range you specify. However, you must plan the IP address range in advance, and all the IP addresses are consumed by the AKS nodes based on the maximum number of pods they can support. Advanced network features and scenarios such as [virtual nodes](virtual-nodes-cli) or Network Policies (either Azure or Calico) are supported with *Azure CNI*.

### Limitations & considerations for kubenet

- An additional hop is required in the design of kubenet, which adds minor latency to pod communication.
- Route tables and user-defined routes are required for using kubenet, which adds complexity to operations.
- For more information, see
[Customize cluster egress with a user-defined routing table in AKS](egress-udr)and[Customize cluster egress with outbound types in AKS](egress-outboundtype).

- For more information, see
- Direct pod addressing isn't supported for kubenet due to kubenet design.
- Unlike Azure CNI clusters, multiple kubenet clusters can't share a subnet.
- AKS doesn't apply Network Security Groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure the security rules in the NSGs allow traffic between the node and pod CIDR. For more details, see
[Network security groups](concepts-network#network-security-groups). - Features
**not supported on kubenet**include:

Note

Some of the system pods such as **konnectivity** within the cluster use the host node IP address rather than an IP from the overlay address space. The system pods will only use the node IP and not an IP address from the virtual network.

### IP address availability and exhaustion

A common issue with *Azure CNI* is that the assigned IP address range is too small to then add more nodes when you scale or upgrade a cluster. The network team also might not be able to issue a large enough IP address range to support your expected application demands.

As a compromise, you can create an AKS cluster that uses *kubenet* and connect to an existing virtual network subnet. This approach lets the nodes receive defined IP addresses without the need to reserve a large number of IP addresses up front for any potential pods that could run in the cluster. With *kubenet*, you can use a much smaller IP address range and support large clusters and application demands. For example, with a */27* IP address range on your subnet, you can run a 20-25 node cluster with enough room to scale or upgrade. This cluster size can support up to *2,200-2,750* pods (with a default maximum of 110 pods per node). The maximum number of pods per node that you can configure with *kubenet* in AKS is 250.

The following basic calculations compare the difference in network models:

**kubenet**: A simple*/24*IP address range can support up to*251*nodes in the cluster. Each Azure virtual network subnet reserves the first three IP addresses for management operations. This node count can support up to*27,610*pods, with a default maximum of 110 pods per node.**Azure CNI**: That same basic*/24*subnet range can only support a maximum of*eight*nodes in the cluster. This node count can only support up to*240*pods, with a default maximum of 30 pods per node.

Note

These maximums don't take into account upgrade or scale operations. In practice, you can't run the maximum number of nodes the subnet IP address range supports. You must leave some IP addresses available for scaling or upgrading operations.

### Virtual network peering and ExpressRoute connections

To provide on-premises connectivity, both *kubenet* and *Azure-CNI* network approaches can use [Azure virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview) or [ExpressRoute connections](/en-us/azure/expressroute/expressroute-introduction). Plan your IP address ranges carefully to prevent overlap and incorrect traffic routing. For example, many on-premises networks use a *10.0.0.0/8* address range that's advertised over the ExpressRoute connection. We recommend creating your AKS clusters in Azure virtual network subnets outside this address range, such as *172.16.0.0/16*.

### Choose a network model to use

The following considerations help outline when each network model may be the most appropriate:

**Use kubenet when**:

- You have limited IP address space.
- Most of the pod communication is within the cluster.
- You don't need advanced AKS features, such as virtual nodes or Azure Network Policy.

**Use Azure CNI when**:

- You have available IP address space.
- Most of the pod communication is to resources outside of the cluster.
- You don't want to manage user defined routes for pod connectivity.
- You need AKS advanced features, such as virtual nodes or Azure Network Policy.

For more information to help you decide which network model to use, see [Compare network models and their support scope](concepts-network-cni-overview).

## Create a virtual network and subnet

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

If you don't have an existing virtual network and subnet to use, create these network resources using the

command. The following example command creates a virtual network named`az network vnet create`

*myAKSVnet*with the address prefix of*192.168.0.0/16*and a subnet named*myAKSSubnet*with the address prefix*192.168.1.0/24*:`az network vnet create \ --resource-group myResourceGroup \ --name myAKSVnet \ --address-prefixes 192.168.0.0/16 \ --subnet-name myAKSSubnet \ --subnet-prefix 192.168.1.0/24 \ --location eastus`

Get the subnet resource ID using the

command and store it as a variable named`az network vnet subnet show`

`SUBNET_ID`

for later use.`SUBNET_ID=$(az network vnet subnet show --resource-group myResourceGroup --vnet-name myAKSVnet --name myAKSSubnet --query id -o tsv)`


## Create an AKS cluster in the virtual network

### Create an AKS cluster with system-assigned managed identities

Note

When using system-assigned identity, the Azure CLI grants the Network Contributor role to the system-assigned identity after the cluster is created. If you're using an ARM template or other clients, you need to use the [user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity) instead.

Create an AKS cluster with system-assigned managed identities using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin kubenet \ --service-cidr 10.0.0.0/16 \ --dns-service-ip 10.0.0.10 \ --pod-cidr 10.244.0.0/16 \ --vnet-subnet-id $SUBNET_ID \ --generate-ssh-keys`

Deployment parameters:

*--service-cidr*is optional. This address is used to assign internal services in the AKS cluster an IP address. This IP address range should be an address space that isn't in use elsewhere in your network environment, including any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.0.0.0/16.*--dns-service-ip*is optional. The address should be the*.10*address of your service IP address range. The default value is 10.0.0.10.*--pod-cidr*is optional. This address should be a large address space that isn't in use elsewhere in your network environment. This range includes any on-premises network ranges if you connect, or plan to connect, your Azure virtual networks using Express Route or a Site-to-Site VPN connection. The default value is 10.244.0.0/16.- This address range must be large enough to accommodate the number of nodes that you expect to scale up to. You can't change this address range once the cluster is deployed.
- The pod IP address range is used to assign a
*/24*address space to each node in the cluster. In the following example, the*--pod-cidr*of*10.244.0.0/16*assigns the first node*10.244.0.0/24*, the second node*10.244.1.0/24*, and the third node*10.244.2.0/24*. - As the cluster scales or upgrades, the Azure platform continues to assign a pod IP address range to each new node.


### Create an AKS cluster with user-assigned managed identity

#### Create a managed identity

Create a managed identity using the

command. If you have an existing managed identity, find the principal ID using the`az identity`

`az identity show --ids <identity-resource-id>`

command instead.`az identity create --name myIdentity --resource-group myResourceGroup`

Your output should resemble the following example output:

`{ "clientId": "<client-id>", "clientSecretUrl": "<clientSecretUrl>", "id": "/subscriptions/<subscriptionid>/resourcegroups/myResourceGroup/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "westus2", "name": "myIdentity", "principalId": "<principal-id>", "resourceGroup": "myResourceGroup", "tags": {}, "tenantId": "<tenant-id>", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


#### Add role assignment for managed identity

If you're using the Azure CLI, the role is automatically added and you can skip this step. If you're using an ARM template or other clients, you need to use the Principal ID of the cluster managed identity to perform a role assignment.

Get the virtual network resource ID using the

command and store it as a variable named`az network vnet show`

`VNET_ID`

.`VNET_ID=$(az network vnet show --resource-group myResourceGroup --name myAKSVnet --query id -o tsv)`

Assign the managed identity for your AKS cluster

*Network Contributor*permissions on the virtual network using thecommand and provide the`az role assignment create`

*<principalId>*.`az role assignment create --assignee <control-plane-identity-principal-id> --scope $VNET_ID --role "Network Contributor" # Example command az role assignment create --assignee 22222222-2222-2222-2222-222222222222 --scope "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup/providers/Microsoft.Network/virtualNetworks/myAKSVnet" --role "Network Contributor"`


Note

Permission granted to your cluster's managed identity used by Azure may take up 60 minutes to populate.

#### Create an AKS cluster

Create an AKS cluster using the

command and provide the control plane's managed identity resource ID for the`az aks create`

`assign-identity`

argument to assign the user-assigned managed identity.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 3 \ --network-plugin kubenet \ --vnet-subnet-id $SUBNET_ID \ --assign-identity <identity-resource-id> \ --generate-ssh-keys`


When you create an AKS cluster, a network security group and route table are automatically created. These network resources are managed by the AKS control plane. The network security group is automatically associated with the virtual NICs on your nodes. The route table is automatically associated with the virtual network subnet. Network security group rules and route tables are automatically updated as you create and expose services.

## Bring your own subnet and route table with kubenet

With kubenet, a route table must exist on your cluster subnet(s). AKS supports bringing your own existing subnet and route table. If your custom subnet doesn't contain a route table, AKS creates one for you and adds rules throughout the cluster lifecycle. If your custom subnet contains a route table when you create your cluster, AKS acknowledges the existing route table during cluster operations and adds/updates rules accordingly for cloud provider operations.

Warning

You can add/update custom rules on the custom route table. However, rules are added by the Kubernetes cloud provider which can't be updated or removed. Rules such as *0.0.0.0/0* generally exist on a given route table (unless the egress outbound type is `none`

) and map to the target of your internet gateway, such as an NVA or other egress gateway. Take caution when updating rules.

Learn more about setting up a [custom route table](/en-us/azure/virtual-network/manage-route-table).

Kubenet networking requires organized route table rules to successfully route requests. Due to this design, route tables must be carefully maintained for each cluster that relies on it. Multiple clusters can't share a route table because pod CIDRs from different clusters might overlap which causes unexpected and broken routing scenarios. When configuring multiple clusters on the same virtual network or dedicating a virtual network to each cluster, consider the following limitations:

- A custom route table must be associated to the subnet before you create the AKS cluster.
- The associated route table resource can't be updated after cluster creation. However, custom rules can be modified on the route table.
- Each AKS cluster must use a single, unique route table for all subnets associated with the cluster. You can't reuse a route table with multiple clusters due to the potential for overlapping pod CIDRs and conflicting routing rules.
- For system-assigned managed identity, it's only supported to provide your own subnet and route table via Azure CLI because Azure CLI automatically adds the role assignment. If you're using an ARM template or other clients, you must use a
[user-assigned managed identity](configure-kubenet#create-an-aks-cluster-with-user-assigned-managed-identity), assign permissions before cluster creation, and ensure the user-assigned identity has write permissions to your custom subnet and custom route table. - Using the same route table with multiple AKS clusters isn't supported.

Note

When you create and use your own VNet and route table with the kubenet network plugin, you must configure a [user-assigned managed identity](use-managed-identity#create-a-user-assigned-managed-identity) for the cluster. With a system-assigned managed identity, you can't retrieve the identity ID before creating a cluster, which causes a delay during role assignment.

Both system-assigned and user-assigned managed identities are supported when you create and use your own VNet and route table with the Azure network plugin. We highly recommend using a user-assigned managed identity for BYO scenarios.

### Add a route table with a user-assigned managed identity to your AKS cluster

After creating a custom route table and associating it with a subnet in your virtual network, you can create a new AKS cluster specifying your route table with a user-assigned managed identity. You need to use the subnet ID for where you plan to deploy your AKS cluster. This subnet also must be associated with your custom route table.

Get the subnet ID using the

command.`az network vnet subnet list`

`az network vnet subnet list --resource-group myResourceGroup --vnet-name myAKSVnet [--subscription]`

Create an AKS cluster with a custom subnet pre-configured with a route table using the

command and providing your values for the`az aks create`

`--vnet-subnet-id`

and`--assign-identity`

parameters.`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --vnet-subnet-id mySubnetIDResourceID \ --assign-identity controlPlaneIdentityResourceID \ --generate-ssh-keys`


## Next steps

This article showed you how to deploy your AKS cluster into your existing virtual network subnet. Now, you can start [creating new apps using Helm](quickstart-helm) or [deploying existing apps using Helm](kubernetes-helm).


---

<!-- DOCUMENTO FUSIONADO: azure-netapp-files-smb.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-smb -->

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
