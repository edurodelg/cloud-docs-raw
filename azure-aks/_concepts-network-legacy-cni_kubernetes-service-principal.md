---
merged_at: 2026-01-25T12:06:27.849687
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: concepts-network-legacy-cni.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-network-legacy-cni -->

# AKS Legacy Container Networking Interfaces (CNI)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

In Azure Kubernetes Service (AKS), while [Azure CNI Overlay](concepts-network-azure-cni-overlay) and [Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet) are recommended for most scenarios, legacy networking models such as Azure CNI Node Subnet and kubenet are still available and supported. These legacy models offer different approaches to pod IP address management and networking, each with its own set of capabilities and considerations. This article provides an overview of these legacy networking options, detailing their prerequisites, deployment parameters, and key characteristics to help you understand their roles and how they can be used effectively within your AKS clusters.

## Prerequisites

The following prerequisites are required for Azure CNI Node Subnet:

The virtual network for the AKS cluster must allow outbound internet connectivity.

AKS clusters can't use

`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the Kubernetes service address range, pod address range, or cluster virtual network address range.The cluster identity used by the AKS cluster must have at least

[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within the virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`

`Microsoft.Authorization/roleAssignments/write`


The subnet assigned to the AKS node pool can't be a

[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview).

- AKS doesn't apply Network Security Groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, make sure the security rules in the NSGs allow traffic within the node CIDR range. For more information, see
[Network security groups](concepts-network#network-security-groups).

## Azure CNI Node Subnet

With [Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod. These IP addresses must be unique across your network space and must be planned in advance. Each node has a configuration parameter for the maximum number of pods that it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow.

With Azure CNI Node Subnet, each pod receives an IP address in the IP subnet and can communicate directly with other pods and services. Your clusters can be as large as the IP address range you specify. However, you must plan the IP address range in advance, and all the IP addresses are consumed by the AKS nodes based on the maximum number of pods they can support. Advanced network features and scenarios such as [virtual nodes](virtual-nodes-cli) or Network Policies (either Azure or Calico) are supported with Azure CNI.

### Deployment parameters

When you create an AKS cluster, the following parameters are configurable for Azure CNI networking:

**Virtual network**: The virtual network into which you want to deploy the Kubernetes cluster. You can create a new virtual network or use an existing one. If you want to use an existing virtual network, make sure it's in the same location and Azure subscription as your Kubernetes cluster. For information about the limits and quotas for an Azure virtual network, see [Azure subscription and service limits, quotas, and constraints](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-resource-manager-virtual-networking-limits).

**Subnet**: The subnet within the virtual network where you want to deploy the cluster. You can add new subnets into the virtual network during the cluster creation process. For hybrid connectivity, the address range shouldn't overlap with any other virtual networks in your environment.

**Azure Network Plugin**: When Azure network plugin is used, the internal LoadBalancer service with "externalTrafficPolicy=Local" can't be accessed from VMs with an IP in clusterCIDR that doesn't belong to AKS cluster.

**Kubernetes service address range**: This parameter is the set of virtual IPs that Kubernetes assigns to internal [services](concepts-network-services) in your cluster. This range can't be updated after you create your cluster. You can use any private address range that satisfies the following requirements:

- Must not be within the virtual network IP address range of your cluster.
- Must not overlap with any other virtual networks with which the cluster virtual network peers.
- Must not overlap with any on-premises IPs.
- Must not be within the ranges
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

.

While it's possible to specify a service address range within the same virtual network as your cluster, we don't recommend it. Overlapping IP ranges can result in unpredictable behavior. For more information, see the [FAQ](#azure-cni-pod-subnet-frequently-asked-questions). For more information on Kubernetes services, see [Services](concepts-network-services) in the Kubernetes documentation.

**Kubernetes DNS service IP address**: The IP address for the cluster's DNS service. This address must be within the *Kubernetes service address range*. Don't use the first IP address in your address range. The first address in your subnet range is used for the *kubernetes.default.svc.cluster.local* address.

**Azure CNI**: That same basic*/24*subnet range can only support a maximum of*8*nodes in the cluster. This node count can only support up to*240*pods, with a default maximum of 30 pods per node.

Note

These maximums don't take into account upgrade or scale operations. In practice, you can't run the maximum number of nodes the subnet IP address range supports. You must leave some IP addresses available for scaling or upgrading operations.

## Virtual network peering and ExpressRoute connections

You can use [Azure virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview) or [ExpressRoute connections](/en-us/azure/expressroute/expressroute-introduction) with *Azure CNI* to provide on-premises connectivity. Make sure you plan your IP addresses carefully to prevent overlap and incorrect traffic routing. For example, many on-premises networks use a *10.0.0.0/8* address range that's advertised over the ExpressRoute connection. We recommend creating your AKS clusters in Azure virtual network subnets outside of this address range, such as *172.16.0.0/16*.

For more information, see [Compare network models and their support scopes](concepts-network-cni-overview).

## Azure CNI Pod Subnet frequently asked questions

**Can I deploy VMs in my cluster subnet?**Yes for Azure CNI Node Subnet, the VMs can be deployed in the same subnet as the AKS cluster.

**What source IP do external systems see for traffic that originates in an Azure CNI-enabled pod?**Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod. But for

[Azure CNI dynamic IP allocation](concepts-network-azure-cni-pod-subnet#dynamic-ip-allocation-mode), no matter the connection is inside the same virtual network or cross virtual networks, the pod IP is always the source address for any traffic from the pod. This is because the[Azure CNI for dynamic IP allocation](concepts-network-azure-cni-pod-subnet#dynamic-ip-allocation-mode)implements[Microsoft Azure Container Networking](https://github.com/Azure/azure-container-networking)infrastructure, which gives end-to-end experience. Hence, it eliminates the use of, which is still used by traditional Azure CNI.`ip-masq-agent`

**Can I configure per-pod network policies?**Yes, Kubernetes network policy is available in AKS. To get started, see

[Secure traffic between pods by using network policies in AKS](use-network-policies).**Is the maximum number of pods deployable to a node configurable?**With

[Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod. These IP addresses must be unique across your network space and must be planned in advance. Each node has a configuration parameter for the maximum number of pods that it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow.**Can I deploy VMs in my cluster subnet?**Yes. But for

[Azure CNI for dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation), the VMs cannot be deployed in pod's subnet.**What source IP do external systems see for traffic that originates in an Azure CNI-enabled pod?**Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod.

But for

[Azure CNI for dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation), no matter the connection is inside the same virtual network or cross virtual networks, the pod IP is always the source address for any traffic from the pod. This is because the[Azure CNI for dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)implements[Microsoft Azure Container Networking](https://github.com/Azure/azure-container-networking)infrastructure, which gives end-to-end experience. Hence, it eliminates the use of, which is still used by traditional Azure CNI.`ip-masq-agent`

**Can I use a different subnet within my cluster virtual network for the***Kubernetes service address range*?It's not recommended, but this configuration is possible. The service address range is a set of virtual IPs (VIPs) that Kubernetes assigns to internal services in your cluster. Azure Networking has no visibility into the service IP range of the Kubernetes cluster. The lack of visibility into the cluster's service address range can lead to issues. It's possible to later create a new subnet in the cluster virtual network that overlaps with the service address range. If such an overlap occurs, Kubernetes could assign a service an IP that's already in use by another resource in the subnet, causing unpredictable behavior or failures. By ensuring you use an address range outside the cluster's virtual network, you can avoid this overlap risk. Yes, when you deploy a cluster with the Azure CLI or a Resource Manager template. See

[Maximum pods per node](concepts-network-ip-address-planning#maximum-pods-per-node).**Can I use a different subnet within my cluster virtual network for the***Kubernetes service address range*?It's not recommended, but this configuration is possible. The service address range is a set of virtual IPs (VIPs) that Kubernetes assigns to internal services in your cluster. Azure Networking has no visibility into the service IP range of the Kubernetes cluster. The lack of visibility into the cluster's service address range can lead to issues. It's possible to later create a new subnet in the cluster virtual network that overlaps with the service address range. If such an overlap occurs, Kubernetes could assign a service an IP that's already in use by another resource in the subnet, causing unpredictable behavior or failures. By ensuring you use an address range outside the cluster's virtual network, you can avoid this overlap risk.


---

<!-- DOCUMENTO FUSIONADO: kubernetes-service-principal.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kubernetes-service-principal -->

# Use a service principal with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) clusters require either a [Microsoft Entra service principal](/en-us/entra/identity-platform/app-objects-and-service-principals) or a [managed identity](/en-us/azure/active-directory/managed-identities-azure-resources/overview) to dynamically create and manage other Azure resources. This article describes how to create a Microsoft Entra service principal and use it with your AKS cluster.

Note

For optimal security and ease of use, we recommend using managed identities instead of service principals to authorize access from an AKS cluster to other resources in Azure. A managed identity is a special type of service principal that you can use to get Microsoft Entra credentials without the need to manage and secure credentials. For more information, see [Use a managed identity in AKS](use-managed-identity).

## Prerequisites

- You need Azure CLI version 2.0.59 or higher. Find your version using the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

- If using Azure PowerShell, you need Azure PowerShell version 5.0.0 or higher. Find your version using the
`Get-InstalledModule -Name Az`

cmdlet. If you need to install or upgrade, see[Install the Azure Az PowerShell module](/en-us/powershell/azure/install-az-ps).

- You need permissions to register an application with your Microsoft Entra tenant and to assign the application to a role in your subscription. If you don't have the necessary permissions, you need to ask your Microsoft Entra ID or subscription administrator to assign the necessary permissions or create the service principal for you.

## Considerations when using a service principal

Keep the following considerations in mind when using a Microsoft Entra service principal with AKS:

- The service principal for Kubernetes is a part of the cluster configuration, but don't use this identity to deploy the cluster. Instead,
[create a service principal](#create-a-service-principal)first, then use that service principal to create the AKS cluster. - Every service principal is associated with a Microsoft Entra application. You can associate the service principal for a Kubernetes cluster with any valid Microsoft Entra application name (for example:
`https://www.contoso.org/example`

). The URL for the application doesn't have to be a real endpoint. - When you specify the service principal
**client ID**, use the value of the application ID (`appId`

for Azure CLI or`ApplicationId`

for Azure PowerShell). - On the agent node virtual machines (VMs) in the AKS cluster, the service principal credentials are stored in the
`/etc/kubernetes/azure.json`

file. - When you delete an AKS cluster that you created using the
command or the`az aks create`

cmdlet, the service principal created isn't automatically deleted. See the`New-AzAksCluster`

[steps to delete a service principal](#delete-a-service-principal). - If you're using a service principal from a different Microsoft Entra tenant, there are other considerations around the permissions available when you deploy the cluster. You might not have the appropriate permissions to read and write directory information. For more information, see
[What are the default user permissions in Microsoft Entra ID?](/en-us/azure/active-directory/fundamentals/users-default-permissions)

## Create a service principal

Create a service principal using the

command.`az ad sp create-for-rbac`

`# Set environment variable SERVICE_PRINCIPAL_NAME=<your-service-principal-name> # Create the service principal az ad sp create-for-rbac --name $SERVICE_PRINCIPAL_NAME`

Your output should be similar to the following example output:

`{ "appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "displayName": "myAKSClusterServicePrincipal", "name": "http://myAKSClusterServicePrincipal", "password": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "tenant": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" }`

Copy the values for

`appId`

and`password`

from the output to use when creating the AKS cluster.

Create a service principal using the

command.`New-AzADServicePrincipal`

`# Set environment variable $SpName = <your-service-principal-name> # Create the service principal New-AzADServicePrincipal -DisplayName $SpName -OutVariable sp`

Your output should be similar to the following example output:

`Secret : System.Security.SecureString ServicePrincipalNames : {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx, http://myAKSClusterServicePrincipal} ApplicationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ObjectType : ServicePrincipal DisplayName : myAKSClusterServicePrincipal Id : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Type :`

The values are stored in a variable that you use when creating the AKS cluster.

Decrypt the value stored in the

**Secret**secure string using the following command.`$BSTR = [System.Runtime.InteropServices.Marshal]::SecureStringToBSTR($sp.Secret) [System.Runtime.InteropServices.Marshal]::PtrToStringAuto($BSTR)`


## Create an AKS cluster with an existing service principal

Create an AKS cluster with an existing service principal using the

command with the`az aks create`

`--service-principal`

and`--client-secret`

parameters set to specify the`appId`

and`password`

values.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> APP_ID=<app-id> CLIENT_SECRET=<password-value> # Create the AKS cluster az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --service-principal $APP_ID \ --client-secret $CLIENT_SECRET \ --generate-ssh-keys`


Convert the service principal

`ApplicationId`

and`Secret`

to a**PSCredential**object using the following command.`$Cred = New-Object -TypeName System.Management.Automation.PSCredential ($sp.ApplicationId, $sp.Secret)`

Create an AKS cluster with an existing service principal using the

cmdlet and specify the`New-AzAksCluster`

`ServicePrincipalIdAndSecret`

parameter with the**PSCredential**object as its value.`# Set environment variables $ResourceGroupName = <your-resource-group-name> $ClusterName = <your-aks-cluster-name> # Create the AKS cluster New-AzAksCluster -ResourceGroupName $ResourceGroupName -Name $ClusterName -ServicePrincipalIdAndSecret $Cred`


Note

If you're using an existing service principal with customized secret, make sure the secret isn't longer than 190 bytes.

## Delegate access to other Azure resources

You can use the service principal for the AKS cluster to access other resources. For example, if you want to deploy your AKS cluster into an existing Azure virtual network (VNet) subnet, connect to ACR, or access keys or secrets in a key vault from your cluster, then you need to delegate access to those resources to the service principal. To delegate access, assign an Azure role-based access control (Azure RBAC) role to the service principal.

When you assign roles, you specify the scope for the role assignment, such as a resource group or VNet resource. The role assignment determines what permissions the service principal has on the resource and at what scope.

Important

Permissions granted to a service principal associated with a cluster can take up 60 minutes to propagate.

## Create a role assignment

Note

The scope for a resource needs to be a full resource ID, such as `/subscriptions/\<guid\>/resourceGroups/myResourceGroup`

or `/subscriptions/\<guid\>/resourceGroups/myResourceGroupVnet/providers/Microsoft.Network/virtualNetworks/myVnet`

.

Create a role assignment using the

command. Specify the value of the service principal app ID for the`az role assignment create`

`--assignee`

parameter and the scope for the role assignment for the`--scope`

parameter. The following example assigns the service principal permissions to access secrets in a key vault:`az role assignment create \ --assignee <app-id> \ --scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.KeyVault/vaults/<vault-name>" \ --role "Key Vault Secrets User"`


Create a role assignment using the

cmdlet. Specify the value of the service principal app ID for the`New-AzRoleAssignment`

`-ApplicationId`

parameter and the scope for the role assignment for the`-Scope`

parameter. The following example assigns the service principal permissions to access secrets in a key vault:`New-AzRoleAssignment -ApplicationId <app-id> ` -Scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.KeyVault/vaults/<vault-name>" ` -RoleDefinitionName "Key Vault Secrets User"`


## Grant access to Azure Container Registry

If you use Azure Container Registry (ACR) as your container image store, you need to grant permissions to the service principal for your AKS cluster to read and pull images. We recommend following the steps in [Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration) to integrate with a registry and assign the appropriate role for the service principal.

## Grant access to networking resources

If you're using advanced networking with a VNet and subnet or public IP addresses in different resource group, you can assign the [Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor) built-in role on the subnet within the VNet. Alternatively, you can create a [custom role](/en-us/azure/role-based-access-control/custom-roles) with permissions to access the network resources in that resource group. For more information, see [AKS service permissions](concepts-identity#aks-service-permissions).

## Grant access to storage disks

If you need to access existing disk resources in another resource group, assign one of the following sets of role permissions:

- Create a
[custom role](/en-us/azure/role-based-access-control/custom-roles)and define the*Microsoft.Compute/disks/read*and*Microsoft.Compute/disks/write*role permissions. - Assign the
[Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor)built-in role on the resource group.

## Grant access to Azure Container Instances

If you use virtual kubelet to integrate with AKS and run Azure Container Instances (ACI) in resource group separate from the AKS cluster, you need to assign *Contributor* permissions to the AKS cluster service principal for the ACI resource group.

## Delete a service principal

Query for the service principal client ID (

`servicePrincipalProfile.clientId`

) and delete the service principal using thecommand with the`az ad sp delete`

`--id`

parameter. The [`az aks show`

][az-aks-show] command retrieves the client ID for the specified AKS cluster.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Delete the service principal az ad sp delete --id $(az aks show \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --query servicePrincipalProfile.clientId \ --output tsv)`


Query for the service principal client ID (

`ServicePrincipalProfile.ClientId`

) and delete the service principal using thecmdlet with the`Remove-AzADServicePrincipal`

`-ApplicationId`

parameter. The [`Get-AzAksCluster`

][get-azakscluster] cmdlet retrieves the client ID for the specified AKS cluster.`# Set environment variables $ResourceGroupName = <your-resource-group-name> $ClusterName = <your-aks-cluster-name> $ClientId = (Get-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster ).ServicePrincipalProfile.ClientId # Delete the service principal Remove-AzADServicePrincipal -ApplicationId $ClientId`


## Resolve service principal credential issues

Azure CLI caches the service principal credentials for AKS clusters.

Azure PowerShell caches the service principal credentials for AKS clusters.

If these credentials expire, you might encounter errors during AKS cluster deployment. If there's an issue with the cached credentials, you might receive an error message similar to the following error message:

```
Operation failed with status: 'Bad Request'.
Details: The credentials in ServicePrincipalProfile were invalid. Please see https://aka.ms/aks-sp-help for more details.
Details: adal: Refresh request failed. Status Code = '401'.
```


You can check the expiration date of your service principal credentials using the [ az ad app credential list](/en-us/cli/azure/ad/app/credential#az-ad-app-credential-list) command with the

`"[].endDateTime"`

query. The output shows you the `endDateTime`

of your credentials.```
az ad app credential list \
--id <app-id> \
--query "[].endDateTime" \
--output tsv
```


- Check the expiration date of your service principal credentials using the
cmdlet. The output shows you the`Get-AzADAppCredential`

`EndDate`

of your credentials.

```
Get-AzADAppCredential -ApplicationId <app-id>
```


**The default expiration time for the service principal credentials is one year**. If your credentials are older than one year, you can [reset the existing credentials](update-credentials#reset-the-existing-service-principal-credentials) or [create a new service principal](update-credentials#create-a-new-service-principal).
