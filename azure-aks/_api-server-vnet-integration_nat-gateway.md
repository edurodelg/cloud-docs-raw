---
merged_at: 2026-01-25T12:06:27.848342
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: api-server-vnet-integration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/api-server-vnet-integration -->

# Create an Azure Kubernetes Service cluster with API Server VNet Integration

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An Azure Kubernetes Service (AKS) cluster configured with API Server VNet Integration projects the API server endpoint directly into a delegated subnet in the VNet where AKS is deployed. API Server VNet Integration enables network communication between the API server and the cluster nodes without requiring a private link or tunnel. The API server is available behind an internal load balancer VIP in the delegated subnet, which the nodes are configured to utilize. By using API Server VNet Integration, you can ensure network traffic between your API server and your node pools remains on the private network only.

## API server connectivity

The control plane or API server is in an AKS-managed Azure subscription. Your cluster or node pool is in your Azure subscription. The server and the virtual machines that make up the cluster nodes can communicate with each other through the API server VIP and pod IPs that are projected into the delegated subnet.

API Server VNet Integration is supported for public or private clusters. You can add or remove public access after cluster provisioning. Unlike non-VNet integrated clusters, the agent nodes always communicate directly with the private IP address of the API server internal load balancer (ILB) IP without using DNS. All node to API server traffic is kept on private networking, and no tunnel is required for API server to node connectivity. Out-of-cluster clients needing to communicate with the API server can do so normally if public network access is enabled. If public network access is disabled, you should follow the same private DNS setup methodology as standard [private clusters](private-clusters).

## Prerequisites

- You must have Azure CLI version 2.73.0 or later installed. You can check your version using the
`az --version`

command.

## Limitations

- API Server VNet Integration does not support
[Virtual Network Encryption](/en-us/azure/virtual-network/virtual-network-encryption-overview). Clusters deployed on**v3 or earlier AKS node SKUs**(which do not support VNet Encryption) are allowed but traffic will not be encrypted. Clusters deployed on**v4 or later AKS node SKUs**(which support VNet Encryption) are blocked because encrypted VNets are incompatible with API Server VNet Integration. See[AKS supported VM SKUs](quotas-skus-regions#supported-vm-sizes)for details.

## Availability

- API Server VNet Integration is available in all GA public cloud regions except eastus2 and qatarcentral. We are continually working on enabling this feature in these regions and will update this page when these regions become available.

## Create an AKS cluster with API Server VNet Integration using managed VNet

You can configure your AKS clusters with API Server VNet Integration in managed VNet or bring-your-own VNet mode. You can create them as public clusters (with API server access available via a public IP) or private clusters (where the API server is only accessible via private VNet connectivity). You can also toggle between a public and private state without redeploying your cluster.

### Create a resource group

Create a resource group using the

command.`az group create`

`az group create --location westus2 --name <resource-group>`


### Deploy a public cluster

Deploy a public AKS cluster with API Server VNet integration for managed VNet using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

flag.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-apiserver-vnet-integration \ --generate-ssh-keys`


### Deploy a private cluster

Deploy a private AKS cluster with API Server VNet integration for managed VNet using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

and`--enable-private-cluster`

flags.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-private-cluster \ --enable-apiserver-vnet-integration \ --generate-ssh-keys`


## Create a private AKS cluster with API Server VNet Integration using bring-your-own VNet

When using bring-your-own VNet, you must create and delegate an API server subnet to `Microsoft.ContainerService/managedClusters`

, which grants the AKS service permissions to inject the API server pods and internal load balancer into that subnet. You can't use the subnet for any other workloads, but you can use it for multiple AKS clusters located in the same virtual network. The minimum supported API server subnet size is a */28*.

The cluster identity needs permissions to both the API server subnet and the node subnet. Lack of permissions at the API server subnet can cause a provisioning failure.

Warning

An AKS cluster reserves at least 9 IPs in the subnet address space. Running out of IP addresses may prevent API server scaling and cause an API server outage.

### Create a resource group

- Create a resource group using the
command.`az group create`


```
az group create --location <location> --name <resource-group>
```


### Create a virtual network

Create a virtual network using the

command.`az network vnet create`

`az network vnet create --name <vnet-name> \ --resource-group <resource-group> \ --location <location> \ --address-prefixes 172.19.0.0/16`

Create an API server subnet using the

command.`az network vnet subnet create`

`az network vnet subnet create --resource-group <resource-group> \ --vnet-name <vnet-name> \ --name <apiserver-subnet-name> \ --delegations Microsoft.ContainerService/managedClusters \ --address-prefixes 172.19.0.0/28`

Create a cluster subnet using the

command.`az network vnet subnet create`

`az network vnet subnet create --resource-group <resource-group> \ --vnet-name <vnet-name> \ --name <cluster-subnet-name> \ --address-prefixes 172.19.1.0/24`


### Create a managed identity and give it permissions on the virtual network

Create a managed identity using the

command.`az identity create`

`az identity create --resource-group <resource-group> --name <managed-identity-name> --location <location>`

Assign the Network Contributor role to the API server subnet using the

command.`az role assignment create`

`az role assignment create --scope <apiserver-subnet-resource-id> \ --role "Network Contributor" \ --assignee <managed-identity-client-id>`

Assign the Network Contributor role to the cluster subnet using the

command.`az role assignment create`

`az role assignment create --scope <cluster-subnet-resource-id> \ --role "Network Contributor" \ --assignee <managed-identity-client-id>`


### Deploy a public cluster

Deploy a public AKS cluster with API Server VNet integration using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

flag.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-apiserver-vnet-integration \ --vnet-subnet-id <cluster-subnet-resource-id> \ --apiserver-subnet-id <apiserver-subnet-resource-id> \ --assign-identity <managed-identity-resource-id> \ --generate-ssh-keys`


### Deploy a private cluster

Deploy a private AKS cluster with API Server VNet integration using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

and`--enable-private-cluster`

flags.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-private-cluster \ --enable-apiserver-vnet-integration \ --vnet-subnet-id <cluster-subnet-resource-id> \ --apiserver-subnet-id <apiserver-subnet-resource-id> \ --assign-identity <managed-identity-resource-id> \ --generate-ssh-keys`


## Convert an existing AKS cluster to API Server VNet Integration

Warning

**API Server VNet Integration is a one-way, capacity-sensitive feature.**

**Manual restart required.**

After enabling API Server VNet Integration using`az aks update --enable-apiserver-vnet-integration`

, due to control plane resource transition, you must immediately restart the cluster for the change to take effect. This restart is not automated. Delaying the restart increases the risk of capacity becoming unavailable, which can prevent the API server from starting. The cluster restart also ensures that all nodes reliably reconnect to the new API server endpoint.**Capacity is validated, but not reserved.**

AKS validates regional capacity when you enable the feature on an existing cluster, but this validation does not reserve capacity. If the restart is delayed and capacity becomes unavailable in the meantime, the cluster may fail to start after a stop or restart. Clusters that enabled this feature before general availability (GA), or that have not yet restarted since enablement, will not undergo capacity validation.**Feature cannot be disabled.**

Once enabled, the feature is permanent. You cannot disable API Server VNet Integration.

This upgrade performs a node-image version upgrade on all node pools and restarts all workloads while they undergo a rolling image upgrade.

Warning

Converting a cluster to API Server VNet Integration results in a change of the API Server IP address, though the hostname remains the same. If the IP address of the API server has been configured in any firewalls or network security group rules, those rules may need to be updated.

Update your cluster to API Server VNet Integration using the

command with the`az aks update`

`--enable-apiserver-vnet-integration`

flag.`az aks update --name <cluster-name> \ --resource-group <resource-group> \ --enable-apiserver-vnet-integration \ --apiserver-subnet-id <apiserver-subnet-resource-id>`


## Enable or disable private cluster mode on an existing cluster with API Server VNet Integration

AKS clusters configured with API Server VNet Integration can have public network access/private cluster mode enabled or disabled without redeploying the cluster. The API server hostname doesn't change, but public DNS entries are modified or removed if necessary.

Note

`--disable-private-cluster`

is currently in preview. For more information, see [Reference and support levels](/en-us/cli/azure/reference-types-and-status).

### Enable private cluster mode

Enable private cluster mode using the

command with the`az aks update`

`--enable-private-cluster`

flag.`az aks update --name <cluster-name> \ --resource-group <resource-group> \ --enable-private-cluster`


### Disable private cluster mode

Disable private cluster mode using the

command with the`az aks update`

`--disable-private-cluster`

flag.`az aks update --name <cluster-name> \ --resource-group <resource-group> \ --disable-private-cluster`


## Connect to cluster using kubectl

Configure

`kubectl`

to connect to your cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group <resource-group> --name <cluster-name>`


## Expose the API server through Private Link

You can expose the API server endpoint of a private cluster with API Server VNet Integration using Azure Private Link. The following steps show how to create a Private Link Service (PLS) in the cluster VNet and connect to it from another VNet or subscription using a Private Endpoint.

### Create an API Server VNet Integration Private cluster

Create a private AKS cluster with API Server VNet Integration using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

and`--enable-private-cluster`

flags.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --enable-private-cluster \ --enable-apiserver-vnet-integration`


For more guidance on how to set up Private Link with API Server VNet Integration, see [Private Link with API Server VNet Integration](private-apiserver-vnet-integration-cluster).

## NSG security rules

All traffic within the VNet is allowed by default. But if you have added NSG rules to restrict traffic between different subnets, ensure that the NSG security rules permit the following types of communication:

| Destination | Source | Protocol | Port | Use |
|---|---|---|---|---|
| APIServer Subnet CIDR | Cluster Subnet | TCP | 443 and 4443 | Required to enable communication between Nodes and the API server. |
| APIServer Subnet CIDR | Azure Load Balancer | TCP | 9988 | Required to enable communication between Azure Load Balancer and the API server. You can also enable all communications between the Azure Load Balancer and the API Server Subnet CIDR. |

## Next steps

- For associated best practices, see
[Best practices for network connectivity and security in AKS](operator-best-practices-network). - For guidance on how to set up private link with API Server VNet Integration, see
[Private Link with API Server VNet Integration](private-apiserver-vnet-integration-cluster).


---

<!-- DOCUMENTO FUSIONADO: nat-gateway.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/nat-gateway -->

# Create a managed or user-assigned NAT gateway for your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

While you can route egress traffic through an Azure Load Balancer, there are limitations on the number of outbound flows of traffic you can have. Azure NAT Gateway allows up to 64,512 outbound UDP and TCP traffic flows per IP address with a maximum of 16 IP addresses.

This article shows you how to create an Azure Kubernetes Service (AKS) cluster with a managed NAT gateway and a user-assigned NAT gateway for egress traffic. It also shows you how to disable OutboundNAT on Windows.

## Before you begin

- Make sure you're using the latest version of
[Azure CLI](/en-us/cli/azure/install-azure-cli). - Make sure you're using Kubernetes version 1.20.x or above.
- Managed NAT gateway is incompatible with custom virtual networks.

Important

In non-private clusters, API server cluster traffic is routed and processed through the clusters outbound type. To prevent API server traffic from being processed as public traffic, consider using a [private cluster](private-clusters), or check out the [API Server VNet Integration](api-server-vnet-integration) feature.

## Create an AKS cluster with a managed NAT gateway

- Create an AKS cluster with a new managed NAT gateway using the
command with the`az aks create`

`--outbound-type managedNATGateway`

,`--nat-gateway-managed-outbound-ip-count`

, and`--nat-gateway-idle-timeout`

parameters. If you want the NAT gateway to operate out of a specific availability zone, specify the zone using`--zones`

. - If no zone is specified when creating a managed NAT gateway, then NAT gateway is deployed to "no zone" by default. When NAT gateway is placed in
**no zone**, Azure places the resource in a zone for you. For more information on non-zonal deployment model, see[non-zonal NAT gateway](/en-us/azure/nat-gateway/nat-availability-zones#non-zonal). - A managed NAT gateway resource can't be used across multiple availability zones.

The following commands first create the required resource group, then the AKS cluster with a managed NAT gateway.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export MY_RG="myResourceGroup$RANDOM_SUFFIX"
export MY_AKS="myNatCluster$RANDOM_SUFFIX"
az group create --name $MY_RG --location "eastus2"
```


Results:

```
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx",
"location": "eastus2",
"managedBy": null,
"name": "myResourceGroupxxx",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


```
az aks create \
--resource-group $MY_RG \
--name $MY_AKS \
--node-count 3 \
--outbound-type managedNATGateway \
--nat-gateway-managed-outbound-ip-count 2 \
--nat-gateway-idle-timeout 4 \
--generate-ssh-keys
```


Results:

```
{
"aadProfile": null,
"agentPoolProfiles": [
{
...
"name": "nodepool1",
...
"provisioningState": "Succeeded",
...
}
],
"dnsPrefix": "myNatClusterxxx-dns-xxx",
"fqdn": "myNatClusterxxx-dns-xxx.xxxxx.xxxxxx.cloudapp.azure.com",
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx",
"name": "myNatClusterxxx",
...
"resourceGroup": "myResourceGroupxxx",
...
"provisioningState": "Succeeded",
...
"type": "Microsoft.ContainerService/ManagedClusters"
}
```


- Update the outbound IP address or idle timeout using the
command with the`az aks update`

`--nat-gateway-managed-outbound-ip-count`

or`--nat-gateway-idle-timeout`

parameter.

The following example updates the NAT gateway managed outbound IP count for the AKS cluster to 5.

```
az aks update \
--resource-group $MY_RG \
--name $MY_AKS \
--nat-gateway-managed-outbound-ip-count 5
```


Results:

```
{
"aadProfile": null,
"agentPoolProfiles": [
{
...
"name": "nodepool1",
...
"provisioningState": "Succeeded",
...
}
],
"dnsPrefix": "myNatClusterxxx-dns-xxx",
"fqdn": "myNatClusterxxx-dns-xxx.xxxxx.xxxxxx.cloudapp.azure.com",
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx",
"name": "myNatClusterxxx",
...
"resourceGroup": "myResourceGroupxxx",
...
"provisioningState": "Succeeded",
...
"type": "Microsoft.ContainerService/ManagedClusters"
}
```


## Create an AKS cluster with a user-assigned NAT gateway

This configuration requires bring-your-own networking (via [Kubenet](configure-kubenet) or [Azure CNI](configure-azure-cni)) and that the NAT gateway is preconfigured on the subnet. The following commands create the required resources for this scenario.

Create a resource group using the

command.`az group create`

`export RANDOM_SUFFIX=$(openssl rand -hex 3) export MY_RG="myResourceGroup$RANDOM_SUFFIX" az group create --name $MY_RG --location southcentralus`

Results:

`{ "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx", "location": "southcentralus", "managedBy": null, "name": "myResourceGroupxxx", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`

Create a managed identity for network permissions and store the ID to

`$IDENTITY_ID`

for later use.`export IDENTITY_NAME="myNatClusterId$RANDOM_SUFFIX" export IDENTITY_ID=$(az identity create \ --resource-group $MY_RG \ --name $IDENTITY_NAME \ --location southcentralus \ --query id \ --output tsv)`

Results:

`/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myNatClusterIdxxx`

Create a public IP for the NAT gateway using the

command.`az network public-ip create`

`export PIP_NAME="myNatGatewayPip$RANDOM_SUFFIX" az network public-ip create \ --resource-group $MY_RG \ --name $PIP_NAME \ --location southcentralus \ --sku standard`

Results:

`{ "publicIp": { "ddosSettings": null, "dnsSettings": null, "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/publicIPAddresses/myNatGatewayPipxxx", "ipAddress": null, "ipTags": [], "location": "southcentralus", "name": "myNatGatewayPipxxx", ... "provisioningState": "Succeeded", ... "sku": { "name": "Standard", "tier": "Regional" }, "type": "Microsoft.Network/publicIPAddresses", ... } }`

Create the NAT gateway using the

command.`az network nat gateway create`

`export NATGATEWAY_NAME="myNatGateway$RANDOM_SUFFIX" az network nat gateway create \ --resource-group $MY_RG \ --name $NATGATEWAY_NAME \ --location southcentralus \ --public-ip-addresses $PIP_NAME`

Results:

`{ "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/natGateways/myNatGatewayxxx", "location": "southcentralus", "name": "myNatGatewayxxx", "provisioningState": "Succeeded", "publicIpAddresses": [ { "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/publicIPAddresses/myNatGatewayPipxxx" } ], ... "type": "Microsoft.Network/natGateways" }`

Important

A single NAT gateway resource can't be used across multiple availability zones. To ensure zone-resiliency, it is recommended to deploy a NAT gateway resource to each availability zone and assign to subnets containing AKS clusters in each zone. For more information on this deployment model, see

[NAT gateway for each zone](/en-us/azure/nat-gateway/nat-availability-zones#zonal-nat-gateway-resource-for-each-zone-in-a-region-to-create-zone-resiliency). If no zone is configured for NAT gateway, the default zone placement is "no zone", in which Azure places NAT gateway into a zone for you.Create a virtual network using the

command.`az network vnet create`

`export VNET_NAME="myVnet$RANDOM_SUFFIX" az network vnet create \ --resource-group $MY_RG \ --name $VNET_NAME \ --location southcentralus \ --address-prefixes 172.16.0.0/20`

Results:

`{ "newVNet": { "addressSpace": { "addressPrefixes": [ "172.16.0.0/20" ] }, ... "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/virtualNetworks/myVnetxxx", "location": "southcentralus", "name": "myVnetxxx", "provisioningState": "Succeeded", ... "type": "Microsoft.Network/virtualNetworks", ... } }`

Create a subnet in the virtual network using the NAT gateway and store the ID to

`$SUBNET_ID`

for later use.`export SUBNET_NAME="myNatCluster$RANDOM_SUFFIX" export SUBNET_ID=$(az network vnet subnet create \ --resource-group $MY_RG \ --vnet-name $VNET_NAME \ --name $SUBNET_NAME \ --address-prefixes 172.16.0.0/22 \ --nat-gateway $NATGATEWAY_NAME \ --query id \ --output tsv)`

Results:

`/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/virtualNetworks/myVnetxxx/subnets/myNatClusterxxx`

Create an AKS cluster using the subnet with the NAT gateway and the managed identity using the

command.`az aks create`

`export AKS_NAME="myNatCluster$RANDOM_SUFFIX" az aks create \ --resource-group $MY_RG \ --name $AKS_NAME \ --location southcentralus \ --network-plugin azure \ --vnet-subnet-id $SUBNET_ID \ --outbound-type userAssignedNATGateway \ --assign-identity $IDENTITY_ID \ --generate-ssh-keys`

Results:

`{ "aadProfile": null, "agentPoolProfiles": [ { ... "name": "nodepool1", ... "provisioningState": "Succeeded", ... } ], "dnsPrefix": "myNatClusterxxx-dns-xxx", "fqdn": "myNatClusterxxx-dns-xxx.xxxxx.xxxxxx.cloudapp.azure.com", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx", "name": "myNatClusterxxx", ... "resourceGroup": "myResourceGroupxxx", ... "provisioningState": "Succeeded", ... "type": "Microsoft.ContainerService/ManagedClusters" }`


## Disable OutboundNAT for Windows

Windows OutboundNAT can cause certain connection and communication issues with your AKS pods. An example issue is node port reuse. In this example, Windows OutboundNAT uses ports to translate your pod IP to your Windows node host IP, which can cause an unstable connection to the external service due to a port exhaustion issue.

Windows enables OutboundNAT by default. You can now manually disable OutboundNAT when creating new Windows agent pools.

### Prerequisites

- Existing AKS cluster with v1.26 or above. If you're using Kubernetes version 1.25 or older, you need to
[update your deployment configuration](tutorial-kubernetes-upgrade-cluster).

### Limitations

- You can't set cluster outbound type to LoadBalancer. You can set it to NAT Gateway or UDR:
[NAT Gateway](nat-gateway): NAT Gateway can automatically handle NAT connection and is more powerful than Standard Load Balancer. You might incur extra charges with this option.[UDR (UserDefinedRouting)](limit-egress-traffic): You must keep port limitations in mind when configuring routing rules.- If you need to switch from a load balancer to NAT Gateway, you can either add a NAT gateway into the VNet or run
to update the outbound type.`az aks upgrade`


Note

UserDefinedRouting has the following limitations:

- SNAT by Load Balancer (must use the default OutboundNAT) has "64 ports on the host IP".
- SNAT by Azure Firewall (disable OutboundNAT) has 2496 ports per public IP.
- SNAT by NAT Gateway (disable OutboundNAT) has 64512 ports per public IP.
- If the Azure Firewall port range isn't enough for your application, you need to use NAT Gateway.
- Azure Firewall doesn't SNAT with Network rules when the destination IP address is in a private IP address range per
[IANA RFC 1918 or shared address space per IANA RFC 6598](/en-us/azure/firewall/snat-private-range).

### Manually disable OutboundNAT for Windows

Manually disable OutboundNAT for Windows when creating new Windows agent pools using the

command with the`az aks nodepool add`

`--disable-windows-outbound-nat`

flag.Note

You can use an existing AKS cluster, but you might need to update the outbound type and add a node pool to enable

`--disable-windows-outbound-nat`

.The following command adds a Windows node pool to an existing AKS cluster, disabling OutboundNAT.

`export WIN_NODEPOOL_NAME="win$(head -c 1 /dev/urandom | xxd -p)" az aks nodepool add \ --resource-group $MY_RG \ --cluster-name $MY_AKS \ --name $WIN_NODEPOOL_NAME \ --node-count 3 \ --os-type Windows \ --disable-windows-outbound-nat`

Results:

`{ "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx/agentPools/mynpxxx", "name": "mynpxxx", "osType": "Windows", "provisioningState": "Succeeded", "resourceGroup": "myResourceGroupxxx", "type": "Microsoft.ContainerService/managedClusters/agentPools" }`


## Next steps

For more information on Azure NAT Gateway, see [Azure NAT Gateway](/en-us/azure/virtual-network/nat-gateway/nat-overview).
