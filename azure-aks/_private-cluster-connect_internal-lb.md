---
merged_at: 2026-01-25T12:06:27.862178
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: private-cluster-connect.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/private-cluster-connect -->

# Establish network connectivity to a private Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In private AKS clusters, the API server endpoint has no public IP address. To manage the API server, you need to use a virtual machine (VM) or container that has access to the virtual network (VNet) of the AKS cluster. There are several options for establishing network connectivity to the private cluster:

- Use an
[Azure Cloud Shell](/en-us/azure/cloud-shell/vnet/overview)instance deployed into a subnet that's connected to the API server for the cluster. - Use
[Azure Bastion](/en-us/azure/bastion/bastion-connect-to-aks-private-cluster)'s native client tunneling feature (preview). - Use a VM in a separate network and set up
[virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview). - Use a
[private endpoint](/en-us/azure/private-link/private-endpoint-overview)connection. - Create a VM in the same VNet as the AKS cluster using the
command with the`az vm create`

`--vnet-name`

flag. - Use an
[Express Route or VPN](/en-us/azure/expressroute/expressroute-about-virtual-network-gateways)connection. - Use the
[AKS](access-private-cluster).`command invoke`

feature

## Choose a connectivity option

Azure Cloud Shell and Azure Bastion (preview) are the easiest options. Express Route and VPNs add costs and require extra networking complexity. Virtual network peering requires you to plan your network CIDR ranges to ensure there are no overlapping ranges.

The following table outlines the key differences and limitations of using Azure Cloud Shell and Azure Bastion:

| Option | Azure Cloud Shell | Azure Bastion (preview) |
|---|---|---|
| Key differences | • Ephemeral, browser-based access. • Cost-effective. • Comes with preinstalled tools like `az cli` and `kubectl` . |
• Persistent, long-running access. • Suited for managing multiple clusters. • Use your own native client tooling. |
| Limitations | • Not supported with AKS Automatic clusters or clusters with network resource group (NRG) lockdown. • You can't have multiple Cloud Shell sessions in different VNets at the same time. |
• Not supported with AKS Automatic clusters or clusters with NRG lockdown. |

## Connect using Azure Cloud Shell

Connecting to a private AKS cluster through Azure Cloud Shell requires completing the following steps:

**Deploy required resources:**You need to deploy Cloud Shell in a VNet that can reach your private cluster. This step provisions the necessary infrastructure. While Cloud Shell is a free service, using Cloud Shell in a VNet requires some resources that incur cost. For more information, see[Deploy Cloud Shell in a virtual network](/en-us/azure/cloud-shell/vnet/deployment).**Configure the connection:**After you deploy the resources, any user in the subscription that has appropriate permissions on the cluster can configure Cloud Shell to deploy in the VNet to allow a secure connection to the private cluster.

## Deploy required resources

To deploy and configure the required resources, you must have the **Owner** role assignment on the subscription. To view and assign roles, see [List Owners of a Subscription](/en-us/azure/role-based-access-control/role-assignments-list-portal#list-owners-of-a-subscription).

You can deploy the required resources using the Azure portal or the provided ARM template if you manage infrastructure as code or have organizational policies that require specific resource naming conventions.

You can optionally leave the deployed resources in place for future connections or delete and recreate them as needed.

### Use the Azure portal (preview)

This option creates a separate VNet with the necessary resources for Cloud Shell and configures VNet peering for you.

- In the
[Azure portal](https://portal.azure.com), navigate to your private cluster resource. - On the Overview page, select
**Connect**. - On the
**Cloud Shell**tab, under**Prerequisites for private cluster connection**, select**Configure**to deploy the necessary resources.- The deployment creates a new resource group named
`RG-CloudShell-PrivateClusterConnection-{RANDOM_ID}`

.

- The deployment creates a new resource group named
- Once the deployment succeeds, under
**Set cluster context**, select**Open Cloud Shell**.


Note

If you already configured Cloud Shell in a VNet for a particular cluster, repeating these steps ensures your Cloud Shell user settings are correctly aligned with that VNet.

### Use an ARM template

To have more control over the deployment configuration, use the [provided ARM template](/en-us/azure/cloud-shell/vnet/deployment).

You can deploy Cloud Shell in the same VNet as your AKS private cluster with a dedicated subnet, or you can deploy in a new VNet and connect via [VNet peering](/en-us/azure/virtual-network/virtual-network-peering-overview).

## Configure connection to the private cluster

After you [deploy the required resources](#deploy-required-resources), any user in the subscription can configure their Cloud Shell to deploy in the given VNet using the steps in [Configure Cloud Shell to use a virtual network](/en-us/azure/cloud-shell/vnet/deployment#5-configure-cloud-shell-to-use-a-virtual-network).

Ensure the user has appropriate Kubernetes-level access to successfully connect to the private cluster. For more information, see [Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).

## Connect using Azure Bastion (preview)

Azure Bastion is a fully managed PaaS service that you provision to securely connect to private resources via private IP addresses. To use Bastion's native client tunneling feature, see [Connect to AKS private cluster using Azure Bastion](/en-us/azure/bastion/bastion-connect-to-aks-private-cluster).

## Connect using virtual network (VNet) peering

To use VNet peering, you need to set up a link between the VNet and the private DNS zone. You can set up VNet peering using either the Azure portal or the Azure CLI.

### Use the Azure portal

In the

[Azure portal](https://portal.azure.com), navigate to your node resource group and select your**private DNS zone resource**.In the service menu, under

**DNS Management**, select**Virtual Network Links**>**Add**.On the

**Add Virtual Network Link**page, configure the following settings:**Link name**: Enter a name for the virtual network link.**Virtual Network**: Select the virtual network that contains the VM.

Select

**Create**to create the virtual network link.Navigate to the resource group that contains the virtual network of your AKS cluster and select your

**virtual network resource**.In the service menu, under

**Settings**, select**Peerings**>**Add**.On the

**Add peering**page, configure the following settings:**Peering link name**: Enter a name for the peering link.**Virtual network**: Select the virtual network of the VM.

Select

**Add**to create the peering link.

For more information, see [Virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview).

### Use the Azure CLI

Create a new link to add the virtual network of the VM to the private DNS zone using the

command.`az network private-dns link vnet create`

`az network private-dns link vnet create \ --name <new-link-name> \ --resource-group <node-resource-group-name> \ --zone-name <private-dns-zone-name> \ --virtual-network <vm-virtual-network-resource-id> \ --registration-enabled false`

Create a peering between the virtual network of the VM and the virtual network of the node resource group using the

command.`az network vnet peering create`

`az network vnet peering create \ --name <new-peering-name-1> \ --resource-group <vm-virtual-network-resource-group-name> \ --vnet-name <vm-virtual-network-name> \ --remote-vnet <node-resource-group-virtual-network-resource-id> \ --allow-vnet-access`

Create a second peering between the virtual network of the node resource group and the virtual network of the VM using the

command.`az network vnet peering create`

`az network vnet peering create \ --name <new-peering-name-2> \ --resource-group <node-resource-group-name> \ --vnet-name <node-resource-group-virtual-network-name> \ --remote-vnet <vm-virtual-network-resource-id> \ --allow-vnet-access`

List the virtual network peerings you created using the

command.`az network vnet peering list`

`az network vnet peering list \ --resource-group <node-resource-group-name> \ --vnet-name <private-dns-zone-name>`


## Use a private endpoint connection

You can set up a private endpoint so that a VNet doesn't need to be peered to communicate with the private cluster. To set up a private endpoint connection, you first create a new private endpoint in the virtual network containing the consuming resources, and then create a link between your virtual network and a new private DNS zone in the same network.

Important

If the virtual network is configured with custom DNS servers, you need to set up private DNS appropriately for the environment. For more information, see the [Virtual network name resolution documentation](/en-us/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances#name-resolution-that-uses-your-own-dns-server).

### Create a private endpoint resource

From the

[Azure portal home page](https://portal.azure.com), select**Create a resource**.Search for

**Private Endpoint**and select**Create**>**Private Endpoint**.Select

**Create**.On the

**Basics**tab, configure the following settings:**Project details****Subscription**: Select the subscription where your private cluster is located.**Resource group**: Select the resource group that contains your virtual network.

**Instance details****Name**: Enter a name for your private endpoint, such as*myPrivateEndpoint*.**Region**: Select the same region as your virtual network.


Select

**Next: Resource**and configure the following settings:**Connection method**: Select**Connect to an Azure resource in my directory**.**Subscription**: Select the subscription where your private cluster is located.**Resource type**: Select**Microsoft.ContainerService/managedClusters**.**Resource**: Select your private cluster.**Target sub-resource**: Select**management**.

Select

**Next: Virtual Network**and configure the following settings:**Networking****Virtual network**: Select your virtual network.**Subnet**: Select your subnet.


Select

**Next: DNS**>**Next: Tags**and (optionally) set up key-values as needed.Select

**Next: Review + create**>**Create**.

Once the resource is created, record the private IP address of the private endpoint for future use.

### Create a private DNS zone

Once you create the private endpoint, create a new private DNS zone with the same name as the private DNS zone created by the private cluster. Remember to create this DNS zone in the VNet containing the consuming resources.

In the Azure portal, navigate to your node resource group and select your

**private DNS zone resource**.In the service menu, under

**DNS Management**, select**Recordsets**and note the following:- The name of the private DNS zone, which follows the pattern
`*.privatelink.<region>.azmk8s.io`

. - The name of the
`A`

record (excluding the private DNS name). - The time-to-live (TTL).

- The name of the private DNS zone, which follows the pattern
From the

[Azure portal home page](https://portal.azure.com), select**Create a resource**.Search for

**Private DNS zone**and select**Create**>**Private DNS zone**.On the

**Basics**tab, configure the following settings:**Project details**- Select your
**Subscription**. - Select the
**Resource group**where you created the private endpoint.

- Select your
**Instance details****Name**: Enter the name of the DNS zone retrieved from previous steps.**Region**: Defaults to the location of your resource group.


Select

**Review + create**>**Create**.

### Create an `A`

record

Once the private DNS zone is created, create an `A`

record, which associates the private endpoint to the private cluster.

Navigate to your private DNS zone resource.

In the service menu, under

**DNS Management**, select**Recordsets**>**Add**.On the

**Add record set**page, configure the following settings:**Name**: Enter the name retrieved from the`A`

record in the private cluster's DNS zone.**Type**: Select**A - Address record**.**TTL**: Enter the number from the`A`

record in the private cluster's DNS zone.**TTL unit**: Change the dropdown value to match the one in the`A`

record from the private cluster's DNS zone.**IP address**: Enter the**IP address of the private endpoint you created**.

Select

**Add**to create the`A`

record.

Important

When creating the `A`

record, only use the name and not the fully qualified domain name (FQDN).

### Link the private DNS zone to the virtual network

Once the `A`

record is created, link the private DNS zone to the virtual network that will access the private cluster.

Navigate to your private DNS zone resource.

In the service menu, under

**DNS Management**, select**Virtual Network Links**>**Add**.On the

**Add Virtual Network Link**page, configure the following settings:**Link name**: Enter a name for your virtual network link.**Subscription**: Select the subscription where your private cluster is located.**Virtual Network**: Select the virtual network of your private cluster.

Select

**Create**to create the link.It might take a few minutes for the operation to complete. Once the virtual network link is created, you can access it from the

**Virtual Network Links**tab you used in step 2.

Warning

- If the private cluster is stopped and restarted, the private cluster's original private link service is removed and recreated, which breaks the connection between your private endpoint and the private cluster. To resolve this issue, delete and recreate any user-created private endpoints linked to the private cluster. If the recreated private endpoints have new IP addresses, you also need to update DNS records.
- If you update the DNS records in the private DNS zone, ensure the host that you're trying to connect from is using the updated DNS records. You can verify this using the
`nslookup`

command. If you notice the updates aren't reflected in the output, you might need to flush the DNS cache on your machine and try again.

## Create a VM in the same virtual network

To create a VM in the same VNet as your private AKS cluster, use the [ az vm create](/en-us/cli/azure/vm#az-vm-create) command with the

`--vnet-name`

flag to specify the VNet.```
az vm create \
--resource-group <resource-group-name> \
--name <vm-name> \
--image <image-name> \
--vnet-name <vm-virtual-network-name> \
--subnet <subnet-name> \
--admin-username <admin-username> \
--admin-password <admin-password>
```


## Use an Express Route or VPN connection

To use an Express Route or VPN connection, see [About ExpressRoute virtual network gateways](/en-us/azure/expressroute/expressroute-about-virtual-network-gateways).

## Use the AKS `command invoke`

feature

To use the AKS `command invoke`

feature to connect to a private cluster, see [Access a private cluster using command invoke](access-private-cluster).

## Related content

For more information about private clusters in AKS, see [Create a private Azure Kubernetes Service (AKS) cluster](private-clusters).


---

<!-- DOCUMENTO FUSIONADO: internal-lb.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/internal-lb -->

# Use an internal load balancer with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can create and use an internal load balancer to restrict access to your applications in Azure Kubernetes Service (AKS). An internal load balancer doesn't have a public IP and makes a Kubernetes service accessible only to applications that can reach the private IP. These applications can be within the same virtual network or in another virtual network through virtual network peering. This article shows you how to create and use an internal load balancer with AKS.

Important

On September 30, 2025, Basic Load Balancer will be retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). There's no integrated option to use the Azure AKS API operation to migrate the Load Balancer SKU. The Load Balancer SKU decision must be done at cluster creation time. Therefore, if you're currently using Basic Load Balancer, take the necessary steps to migrate your workloads to a new created cluster with the new default Standard Load Balancer SKU prior to the retirement date.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the Azure CLI version 2.0.59 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you want to use an existing subnet or resource group, the AKS cluster identity needs permission to manage network resources. For information, see
[Configure Azure CNI networking in AKS](configure-azure-cni). If you're configuring your load balancer to use an[IP address in a different subnet](#specify-a-different-subnet), ensure the AKS cluster identity also has`Read`

access to that subnet.- For more information on permissions, see
[Delegate AKS access to other Azure resources](kubernetes-service-principal#delegate-access-to-other-azure-resources).

- For more information on permissions, see

## Create an internal load balancer

Create a service manifest named

`internal-lb.yaml`

with the service type`LoadBalancer`

and the`azure-load-balancer-internal`

annotation.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`

Deploy the internal load balancer using the

command. This command creates an Azure load balancer in the node resource group connected to the same virtual network as your AKS cluster.`kubectl apply`

`kubectl apply -f internal-lb.yaml`

View the service details using the

`kubectl get service`

command.`kubectl get service internal-app`

The IP address of the internal load balancer is shown in the

`EXTERNAL-IP`

column, as shown in the following example output. In this context,*External*refers to the external interface of the load balancer. It doesn't mean that it receives a public, external IP address. This IP address is dynamically assigned from the same subnet as the AKS cluster.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE internal-app LoadBalancer 10.0.248.59 10.240.0.7 80:30555/TCP 2m`


## Specify an IP address

When you specify an IP address for the load balancer, the specified IP address must reside in the same virtual network as the AKS cluster, but it can't already be assigned to another resource in the virtual network. For example, you shouldn't use an IP address in the range designated for the Kubernetes subnet within the AKS cluster. Using an IP address that's already assigned to another resource in the same virtual network can cause issues with the load balancer.

You can use the [ az network vnet subnet list](/en-us/cli/azure/network/vnet/subnet#az-network-vnet-subnet-list) Azure CLI command or the

[PowerShell cmdlet to get the subnets in your virtual network.](/en-us/powershell/module/az.network/get-azvirtualnetworksubnetconfig)

`Get-AzVirtualNetworkSubnetConfig`

For more information on subnets, see [Add a node pool with a unique subnet](node-pool-unique-subnet).

If you want to use a specific IP address with the load balancer, you have two options: **set service annotations** or **add the LoadBalancerIP property to the load balancer YAML manifest**.

Important

Adding the *LoadBalancerIP* property to the load balancer YAML manifest is deprecating following [upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235). While current usage remains the same and existing services are expected to work without modification, we **highly recommend setting service annotations** instead. For more information about service annotations, see [Azure LoadBalancer supported annotations](https://cloud-provider-azure.sigs.k8s.io/topics/loadbalancer/#loadbalancer-annotations).

Set service annotations using

`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-ipv4: 10.240.0.25 service.beta.kubernetes.io/azure-load-balancer-internal: "true" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`


View the service details using the

`kubectl get service`

command.`kubectl get service internal-app`

The IP address in the

`EXTERNAL-IP`

column should reflect your specified IP address, as shown in the following example output:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE internal-app LoadBalancer 10.0.184.168 10.240.0.25 80:30225/TCP 4m`


For more information on configuring your load balancer in a different subnet, see [Specify a different subnet](#specify-a-different-subnet).

## Connect Azure Private Link service to internal load balancer

### Before you begin

- You need Kubernetes version 1.22.x or later.
- You need an existing resource group with a virtual network and subnet. This resource group is where you
[create the private endpoint](#create-a-private-endpoint-to-the-private-link-service). If you don't have these resources, see[Create a virtual network and subnet](configure-kubenet#create-a-virtual-network-and-subnet).

### Create a Private Link service connection

Create a service manifest named

`internal-lb-pls.yaml`

with the service type`LoadBalancer`

and the`azure-load-balancer-internal`

and`azure-pls-create`

annotations. For more options, refer to the[Azure Private Link Service Integration](https://kubernetes-sigs.github.io/cloud-provider-azure/topics/pls-integration/)design document.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true" service.beta.kubernetes.io/azure-pls-create: "true" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`

Deploy the internal load balancer using the

command. This command creates an Azure load balancer in the node resource group connected to the same virtual network as your AKS cluster. It also creates a Private Link Service object that connects to the frontend IP configuration of the load balancer associated with the Kubernetes service.`kubectl apply`

`kubectl apply -f internal-lb-pls.yaml`

View the service details using the

`kubectl get service`

command.`kubectl get service internal-app`

The IP address of the internal load balancer is shown in the

`EXTERNAL-IP`

column, as shown in the following example output. In this context,*External*refers to the external interface of the load balancer. It doesn't mean that it receives a public, external IP address.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE internal-app LoadBalancer 10.125.17.53 10.125.0.66 80:30430/TCP 64m`

View the details of the Private Link Service object using the

command.`az network private-link-service list`

`# Create a variable for the node resource group AKS_MC_RG=$(az aks show -g myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv) # View the details of the Private Link Service object az network private-link-service list -g $AKS_MC_RG --query "[].{Name:name,Alias:alias}" -o table`

Your output should look similar to the following example output:

`Name Alias -------- ------------------------------------------------------------------------- pls-xyz pls-xyz.abc123-defg-4hij-56kl-789mnop.eastus2.azure.privatelinkservice`


### Create a Private Endpoint to the Private Link service

A Private Endpoint allows you to privately connect to your Kubernetes service object via the Private Link Service you created.

Create the private endpoint using the

command.`az network private-endpoint create`

`# Create a variable for the private link service AKS_PLS_ID=$(az network private-link-service list -g $AKS_MC_RG --query "[].id" -o tsv) # Create the private endpoint $ az network private-endpoint create \ -g myOtherResourceGroup \ --name myAKSServicePE \ --vnet-name myOtherVNET \ --subnet pe-subnet \ --private-connection-resource-id $AKS_PLS_ID \ --connection-name connectToMyK8sService`


### PLS Customizations via Annotations

You can use the following annotations to customize the PLS resource:

| Annotation | Value | Description | Required | Default |
|---|---|---|---|---|
`service.beta.kubernetes.io/azure-pls-create` |
`"true"` |
Boolean indicating whether a PLS needs to be created. | Required | |
`service.beta.kubernetes.io/azure-pls-name` |
`<PLS name>` |
String specifying the name of the PLS resource to be created. | Optional | `"pls-<LB frontend config name>"` |
`service.beta.kubernetes.io/azure-pls-resource-group` |
`Resource Group name` |
String specifying the name of the Resource Group where the PLS resource is created | Optional | `MC_ resource` |
`service.beta.kubernetes.io/azure-pls-ip-configuration-subnet` |
`<Subnet name>` |
String indicating the subnet to which the PLS is deployed. This subnet must exist in the same virtual network as the backend pool. PLS NAT IPs are allocated within this subnet. | Optional | If `service.beta.kubernetes.io/azure-load-balancer-internal-subnet` , this ILB subnet is used. Otherwise, the default subnet from config file is used. |
`service.beta.kubernetes.io/azure-pls-ip-configuration-ip-address-count` |
`[1-8]` |
Total number of private NAT IPs to allocate. | Optional | 1 |
`service.beta.kubernetes.io/azure-pls-ip-configuration-ip-address` |
`"10.0.0.7 ... 10.0.0.10"` |
A space separated list of static IPv4 IPs to be allocated. (IPv6 isn't supported right now.) Total number of IPs shouldn't be greater than the ip count specified in `service.beta.kubernetes.io/azure-pls-ip-configuration-ip-address-count` . If there are fewer IPs specified, the rest are dynamically allocated. The first IP in the list is set as `Primary` . |
Optional | All IPs are dynamically allocated. |
`service.beta.kubernetes.io/azure-pls-proxy-protocol` |
`"true"` or `"false"` |
Boolean indicating whether the TCP PROXY protocol should be enabled on the PLS to pass through connection information, including the link ID and source IP address. The backend service MUST support the PROXY protocol or the connections fails. | Optional | `false` |
`service.beta.kubernetes.io/azure-pls-visibility` |
`"sub1 sub2 sub3 … subN"` or `"*"` |
A space separated list of Azure subscription IDs for which the private link service is visible. Use `"*"` to expose the PLS to all subs (Least restrictive). |
Optional | Empty list `[]` indicating role-based access control only: This private link service is only available to individuals with role-based access control permissions within your directory. (Most restrictive) |
`service.beta.kubernetes.io/azure-pls-auto-approval` |
`"sub1 sub2 sub3 … subN"` |
A space separated list of Azure subscription IDs. This allows PE connection requests from the subscriptions listed to the PLS to be automatically approved. This only works when visibility is set to `"*"` . |
Optional | `[]` |

## Use private networks

When you create your AKS cluster, you can specify advanced networking settings. These settings allow you to deploy the cluster into an existing Azure virtual network and subnets. For example, you can deploy your AKS cluster into a private network connected to your on-premises environment and run services that are only accessible internally.

For more information, see [configure your own virtual network subnets with Kubenet](configure-kubenet) or [with Azure CNI](configure-azure-cni).

You don't need to make any changes to the previous steps to deploy an internal load balancer that uses a private network in an AKS cluster. The load balancer is created in the same resource group as your AKS cluster, but it's instead connected to your private virtual network and subnet, as shown in the following example:

```
$ kubectl get service internal-app
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
internal-app LoadBalancer 10.1.15.188 10.0.0.35 80:31669/TCP 1m
```


Note

The cluster identity used by the AKS cluster must at least have the [Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor) role on the virtual network resource. You can view the cluster identity using the [ az aks show](/en-us/cli/azure/aks#az-aks-show) command, such as

`az aks show --resource-group <resource-group-name> --name <cluster-name> --query "identity"`

. You can assign the Network Contributor role using the [command, such as](/en-us/cli/azure/role/assignment#az-role-assignment-create)

`az role assignment create`

`az role assignment create --assignee <identity-resource-id> --scope <virtual-network-resource-id> --role "Network Contributor"`

.If you want to define a [custom role](/en-us/azure/role-based-access-control/custom-roles-cli) instead, you need the following permissions:

`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


For more information, see [Add, change, or delete a virtual network subnet](/en-us/azure/virtual-network/virtual-network-manage-subnet).

### Specify a different subnet

Add the

`azure-load-balancer-internal-subnet`

annotation to your service to specify a subnet for your load balancer. The subnet specified must be in the same virtual network as your AKS cluster. When deployed, the load balancer`EXTERNAL-IP`

address is part of the specified subnet.`apiVersion: v1 kind: Service metadata: name: internal-app annotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true" service.beta.kubernetes.io/azure-load-balancer-internal-subnet: "apps-subnet" spec: type: LoadBalancer ports: - port: 80 selector: app: internal-app`


## Delete the load balancer

The load balancer is deleted when all of its services are deleted.

As with any Kubernetes resource, you can directly delete a service, such as `kubectl delete service internal-app`

, which also deletes the underlying Azure load balancer.

## Next steps

To learn more about Kubernetes services, see the [Kubernetes services documentation](https://kubernetes.io/docs/concepts/services-networking/service/).
