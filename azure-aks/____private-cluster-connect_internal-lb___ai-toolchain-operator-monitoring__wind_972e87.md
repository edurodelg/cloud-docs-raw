---
merged_at: 2026-01-28T07:16:09.862304
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/private-cluster-connect -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/internal-lb -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-monitoring -->

# Monitor and visualize AI inference metrics on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Monitoring and observability play a key role in maintaining high performance and low cost of your AI workload deployments in Azure Kubernetes Service (AKS). Visibility into system and performance metrics can indicate the limits of your underlying infrastructure and motivate real-time adjustments and optimizations to reduce workload interruptions. Monitoring also provides valuable insights into resource utilization for cost-effective management of computational resources and accurate provisioning.

The Kubernetes AI Toolchain Operator (KAITO) is a managed add-on for AKS that simplifies deployment and operations for AI models in your AKS cluster.

In [KAITO version 0.4.4](https://github.com/kaito-project/kaito/releases/tag/v0.4.4) and later versions, the vLLM inference runtime is enabled by default in the AKS managed add-on. [vLLM](https://docs.vllm.ai/en/latest/) is a library for language model inference and serving. It surfaces key system performance, resource usage, and request processing for [Prometheus metrics](https://docs.vllm.ai/en/latest/design/v1/metrics.html) that you can use to evaluate your KAITO inference deployments.

In this article, you'll learn how to monitor and visualize vLLM inference metrics using the AI toolchain operator add-on with Azure Managed Prometheus and Azure Managed Grafana on your AKS cluster.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Install and configure Azure CLI version 2.47.0 or later. To find your version, run
`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

## Prerequisites

- Install and configure kubectl, the Kubernetes command-line client. For more information, see
[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - Enable the
[AI toolchain operator add-on](ai-toolchain-operator)in your AKS cluster. - If you already have the AI toolchain operator add-on enabled, update your AKS cluster to the latest version to run KAITO v0.4.4 or later.
- Enable
[the managed service for Prometheus and Azure Managed Grafana](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable)in your AKS cluster. - Have permissions to
[create or update Azure Managed Grafana instances](/en-us/azure/managed-grafana/how-to-manage-access-permissions-users-identities)in your Azure subscription.

## Deploy a KAITO inference service

In this example, you collect metrics for the [Qwen-2.5-coder-7B-instruct language model](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml).

Start by applying the following KAITO workspace custom resource to your cluster:

`kubectl apply -f https://raw.githubusercontent.com/Azure/kaito/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml`

Track the live resource changes in your KAITO workspace:

`kubectl get workspace workspace-qwen-2-5-coder-7b-instruct -w`

Note

Machine readiness can take up to 10 minutes, and workspace readiness can take up to 20 minutes depending on the size of your language model.

Confirm that your inference service is running and get the service IP address:

`export SERVICE_IP=$(kubectl get svc workspace-qwen-2-5-coder-7b-instruct -o jsonpath='{.spec.clusterIP}') echo $SERVICE_IP`


## Surface KAITO inference metrics to the managed service for Prometheus

Prometheus metrics are collected by default at the KAITO [ /metrics endpoint](https://github.com/kaito-project/kaito/tree/main).

Add the following label to your KAITO inference service so that a Kubernetes

`ServiceMonitor`

deployment can detect it:`kubectl label svc workspace-qwen-2-5-coder-7b-instruct App=qwen-2-5-coder`

Create a

`ServiceMonitor`

resource to define the inference service endpoints and the required configurations to scrape the vLLM Prometheus metrics. Export these metrics to the managed service for Prometheus by deploying the following`ServiceMonitor`

YAML manifest in the`kube-system`

namespace:`cat <<EOF | kubectl apply -n kube-system -f - apiVersion: azmonitoring.coreos.com/v1 kind: ServiceMonitor metadata: name: prometheus-kaito-monitor spec: selector: matchLabels: App: qwen-2-5-coder endpoints: - port: http interval: 30s path: /metrics scheme: http EOF`

Check for the following output to verify that

`ServiceMonitor`

is created:`servicemonitor.azmonitoring.coreos.com/prometheus-kaito-monitor created`

Verify that your

`ServiceMonitor`

deployment is running successfully:`kubectl get servicemonitor prometheus-kaito-monitor -n kube-system`

In the Azure portal, verify that vLLM metrics are successfully collected in the managed service for Prometheus.

In your Azure Monitor workspace, go to

**Managed Prometheus**>**Prometheus explorer**.Select the

**Grid**tab and confirm that a metrics item is associated with the job named`workspace-qwen-2-5-coder-7b-instruct`

.Note

The

`up`

value of this item should be`1`

. A value of`1`

indicates that Prometheus metrics are successfully being scraped from your AI inference service endpoint.


## Visualize KAITO inference metrics in Azure Managed Grafana

The vLLM project provides a Grafana dashboard configuration named

[grafana.json](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)for inference workload monitoring. Navigate to the bottom of this[page](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)and copy the entire contents of the`grafana.json`

file.Go to the bottom of the

[examples page](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)and copy the entire contents of the`grafana.json`

file:Complete the steps to

[import the Grafana configurations into a new dashboard](/en-us/azure/managed-grafana/how-to-create-dashboard#import-a-json-dashboard)in Azure Managed Grafana.Go to your Managed Grafana endpoint, view the available dashboards, and select the

**vLLM**dashboard.To begin collecting data for your selected model deployment, confirm that the

**datasource**value shown at the top left of the Grafana dashboard is your instance of the managed service for Prometheus you created for this example.Copy the inference preset name defined in your KAITO workspace to the

**model_name**field in the Grafana dashboard. In this example, the model name is[qwen2.5-coder-7b-instruct](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml).In a few moments, verify that the metrics for your KAITO inference service appear in the vLLM Grafana dashboard.

Note

The value of these inference metrics remains

**0**until the requests are submitted to the model inference server.

## Related content

[Monitor and visualize](monitor-aks)your AKS deployments at scale.- Test and monitor
[tool calling with KAITO inference](ai-toolchain-operator-tool-calling)on your cluster. [Fine-tune an AI model](ai-toolchain-operator-fine-tune)by using the AI toolchain operator add-on in AKS.- Learn about AKS GPU workload deployment options on
[Linux](gpu-cluster)and[Windows](use-windows-gpu)nodes.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/windows-containerd -->

# Create Windows Server node pools with containerd in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For Kubernetes version 1.20 and higher, you can specify [ containerd](https://containerd.io/) as the container runtime for Windows Server 2019 node pools. Starting with Kubernetes 1.23,

`containerd`

is the default and only container runtime for Windows.In this article, you learn how to create Windows Server node pools with `containerd`

in Azure Kubernetes Service (AKS).

## Prerequisites

[Azure CLI](/en-us/cli/azure/install-azure-cli)installed and configured. Find the version using the`az version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).- An existing AKS cluster with a system node pool. If you need to create one, see
[Create an AKS cluster with a single node pool](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli).

## Limitations and considerations

When using Windows Server node pools with `containerd`

, keep the following limitations and considerations in mind:

- Both the control plane and Windows Server 2019 node pools must use Kubernetes version 1.20 or greater.
- When you create or update a node pool to run Windows Server containers, the default value for
`--node-vm-size`

is`Standard_D2s_v3`

, which was the minimum recommended size for Windows Server 2019 node pools up to Kubernetes version 1.20. The minimum recommended size for Windows Server 2019 node pools using`containerd`

is`Standard_D4s_v3`

. When setting the`--node-vm-size`

parameter, check the[list of restricted virtual machine (VM) sizes](/en-us/azure/virtual-machines/sizes/overview). - We recommend using
[taints or labels](manage-node-pools#set-node-pool-taints)with your Windows Server 2019 node pools running`containerd`

and tolerations or node selectors with your deployments to guarantee your workloads are scheduled correctly.

## Add a Windows Server node pool with `containerd`


Add a Windows Server node pool with

`containerd`

into your existing cluster using the [`az aks nodepool add`

][az-aks-nodepool-add].Note

If you don't specify the

`WindowsContainerRuntime=containerd`

custom header, the node pool still uses`containerd`

as the container runtime by default.`az aks nodepool add \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --os-type Windows \ --name $CONTAINER_D_NODE_POOL_NAME \ --node-vm-size Standard_D4s_v3 \ --kubernetes-version 1.20.5 \ --aks-custom-headers WindowsContainerRuntime=containerd \ --node-count 1`


## Upgrade an existing Windows Server node pool to `containerd`


Upgrade a specific node pool from Docker to

`containerd`

using the [`az aks nodepool upgrade`

][az-aks-nodepool-upgrade] command.`export CONTAINER_D_NODE_POOL_NAME="mywindowsnodepool" az aks nodepool upgrade \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --name $CONTAINER_D_NODE_POOL_NAME \ --kubernetes-version 1.20.7 \ --aks-custom-headers WindowsContainerRuntime=containerd`


## Upgrade all existing Windows Server node pools to `containerd`


Upgrade all node pools from Docker to

`containerd`

using the [`az aks nodepool upgrade`

][az-aks-nodepool-upgrade] command.`az aks nodepool upgrade \ --resource-group $RESOURCE_GROUP \ --cluster-name $CLUSTER_NAME \ --kubernetes-version 1.20.7 \ --aks-custom-headers WindowsContainerRuntime=containerd`


## Next steps

For more information about node pools in AKS, see [Manage node pools for a cluster in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/delete-node-pool -->

# Delete an Azure Kubernetes Service (AKS) node pool

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article outlines node pool deletion in Azure Kubernetes Service (AKS), including what happens when you delete a node pool and how to delete a node pool.

## What happens when you delete a node pool?

When you delete a node pool, the following resources are deleted:

- The virtual machine scale set (VMSS) and virtual machines (VMs) for each node in the node pool
- Any node instances in the node pool along with any pods running on those nodes

## Delete a node pool

Important

Keep the following information in mind when deleting a node pool:

**You can't recover a node pool after it's deleted**. You need to create a new node pool and redeploy your applications.

Delete a node pool using the [ az aks nodepool delete](/en-us/cli/azure/aks#az-aks-nodepool-delete) command.

```
az aks nodepool delete \
--resource-group <resource-group-name> \
--cluster-name <cluster-name> \
--name <node-pool-name>
```


To verify that the node pool was deleted successfully, use the `kubectl get nodes`

command to confirm that the nodes in the node pool no longer exist.

## Ignore PodDisruptionBudgets (PDBs) when removing an existing node pool

If your cluster has PodDisruptionBudgets that are preventing the deletion of the node pool, you can ignore the PodDisruptionBudget requirements by setting `--ignore-pod-disruption-budget`

to `true`

. To learn more about PodDisruptionBudgets, see:

[Plan for availability using a pod disruption budget](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets)[Specifying a Disruption Budget for your Application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)[Disruptions](https://kubernetes.io/docs/concepts/workloads/pods/disruptions/)

Delete an existing node pool without following any PodDisruptionBudgets set on the cluster using the

command with the`az aks nodepool delete`

`--ignore-pod-disruption-budget`

flag set to`true`

:`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1 \ --ignore-pod-disruption-budget true`

To verify that the node pool was deleted successfully, use the

`kubectl get nodes`

command to confirm that the nodes in the node pool no longer exist.

## Remove specific VMs in an existing node pool

Note

When you delete a VM with this command, AKS doesn't perform cordon and drain. To minimize the disruption of rescheduling pods currently running on the VM you plan to delete, perform a cordon and drain on the VM before deleting. You can learn more about how to cordon and drain using the example scenario provided in the resizing node pools tutorial.

List the existing nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should look similar to the following example output:

`NAME STATUS ROLES AGE VERSION aks-mynodepool-20823458-vmss000000 Ready agent 63m v1.21.9 aks-mynodepool-20823458-vmss000001 Ready agent 63m v1.21.9 aks-mynodepool-20823458-vmss000002 Ready agent 63m v1.21.9`

Delete the specified VMs using the

command. Make sure to replace the placeholders with your own values.`az aks nodepool delete-machines`

`az aks nodepool delete-machines \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --machine-names <vm-name-1> <vm-name-2>`

Verify the VMs were successfully deleted using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should no longer include the VMs that you specified in the

`az aks nodepool delete-machines`

command.

## Next steps

For more information about adjusting node pool sizes in AKS, see [Resize node pools](resize-node-pool).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/artifact-streaming -->

# Reduce image pull time with Artifact Streaming on Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

High performance compute workloads often involve large images, which can cause long image pull times and slow down your workload deployments. Artifact Streaming on AKS allows you to stream container images from Azure Container Registry (ACR) to AKS. AKS only pulls the necessary layers for initial pod startup, reducing the time it takes to pull images and deploy your workloads.

Artifact Streaming can reduce time to pod readiness by over 15%, depending on the size of the image, and it works best for images <30GB. Based on our testing, we saw reductions in pod start-up times for images <10GB from minutes to seconds. If you have a pod that needs access to a large file (>30GB), then you should mount it as a volume instead of building it as a layer. This is because if your pod requires that file to start, it congests the node. Artifact Streaming isn't ideal for read heavy images from your filesystem if you need that on startup. With Artifact Streaming, pod start-up becomes concurrent, whereas without it, pods start in serial.

This article describes how to enable the Artifact Streaming feature on your AKS node pools to stream artifacts from ACR.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

Important

Artifact Streaming (preview) is a suggested alternative for customers previously using Teleport (preview).
[Teleport (preview)](https://github.com/Azure/acr/blob/main/docs/teleport/aks-getting-started.md) on AKS will be retired on 15 July 2025. Please migrate to Artifact Streaming (preview) on AKS or update your node pools to set `--aks-custom-headers EnableACRTeleport=false`

.
Azure Container Registry removed the Teleport API, meaning that any nodes with Teleport enabled will pull images from Azure Container Registry like any other AKS node without Teleport.
After 15 July 2025, AKS node pools with Teleport enabled might experience breakage and node provisioning failures. For more information, see [aka.ms/aks/teleport-retirement](https://aka.ms/aks/teleport-retirement).

## Limitations

- Artifact Steaming isn't supported for the following OS options:
[Windows Server versions](windows-best-practices),[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks), and[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard).

## Prerequisites

- You need an existing AKS cluster with ACR integration. If you don't have one, you can create one using
[Authenticate with ACR from AKS](cluster-container-registry-integration). [Enable Artifact Streaming on ACR](#enable-artifact-streaming-on-acr).- This feature requires Kubernetes version 1.25 or later. To check your AKS cluster version, see
[Check for available AKS cluster upgrades](upgrade-cluster).

Note

Artifact Streaming is only supported on Ubuntu 22.04, Ubuntu 20.04, and Azure Linux node pools. Windows node pools aren't supported.

## Install the `aks-preview`

CLI extension

Install the

`aks-preview`

CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update the extension to ensure you have the latest version installed using the

command.`az extension update`

`az extension update --name aks-preview`


## Register the `ArtifactStreamingPreview`

feature flag in your subscription

Register the

`ArtifactStreamingPreview`

feature flag in your subscription using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name ArtifactStreamingPreview`


## Enable Artifact Streaming on ACR

Enablement on ACR is a prerequisite for Artifact Streaming on AKS. For more information, see [Artifact Streaming on ACR](https://aka.ms/acr/artifact-streaming).

Create an Azure resource group to hold your ACR instance using the

command.`az group create`

`az group create --name myStreamingTest --location westus`

Create a new premium SKU Azure Container Registry using the

command with the`az acr create`

`--sku Premium`

flag.`az acr create --resource-group myStreamingTest --name mystreamingtest --sku Premium`

Configure the default ACR instance for your subscription using the

command.`az configure`

`az configure --defaults acr="mystreamingtest"`

Push or import an image to the registry using the

command.`az acr import`

`az acr import --source docker.io/jupyter/all-spark-notebook:latest --repository jupyter/all-spark-notebook:latest`

Create a streaming artifact from the image using the

command.`az acr artifact-streaming create`

`az acr artifact-streaming create --image jupyter/all-spark-notebook:latest`

Verify the generated Artifact Streaming using the

command.`az acr manifest list-referrers`

`az acr manifest list-referrers --name jupyter/all-spark-notebook:latest`


## Enable Artifact Streaming on AKS

### Enable Artifact Streaming on a new node pool

Create a new node pool with Artifact Streaming enabled using the

command with the`az aks nodepool add`

`--enable-artifact-streaming`

.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myNodePool \ --enable-artifact-streaming`


### Enable Artifact Streaming on an existing node pool

Update an existing node pool to enable Artifact Streaming using the

command with the`az aks nodepool update`

`--enable-artifact-streaming`

.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myNodePool \ --enable-artifact-streaming`


## Check if Artifact Streaming is enabled

Now that you enabled Artifact Streaming on a premium ACR and connected that to an AKS node pool with Artifact Streaming enabled, any new pod deployments on this cluster with an image pull from the ACR with Artifact Streaming enabled will see reductions in image pull times.

Check if your node pool has Artifact Streaming enabled using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --name myNodePool --query artifactStreamingProfile`

In the output, check that the

`Enabled`

field is set to`true`

.

## Next steps

This article described how to enable Artifact Streaming on your AKS node pools to stream artifacts from ACR and reduce image pull time. To learn more about working with container images in AKS, see [Best practices for container image management and security in AKS](operator-best-practices-container-image-management).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/quickstart-dapr -->

# Quickstart: Deploy an application using the Dapr cluster extension for Azure Kubernetes Service (AKS) or Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you use the [Dapr cluster extension](dapr-overview) in an AKS or Arc-enabled Kubernetes cluster. You deploy [a hello world example](https://github.com/Azure-Samples/dapr-aks-extension-quickstart), which consists of a Python application that generates messages and a Node.js application that consumes and persists the messages.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.- An AKS Cluster with:
[Workload identity](workload-identity-deploy-cluster#deploy-and-configure-microsoft-entra-workload-id-on-an-azure-kubernetes-service-aks-cluster)enabled[Managed identity](workload-identity-deploy-cluster#create-a-managed-identity)created in the same subscription[A Kubernetes service account](workload-identity-deploy-cluster#create-a-kubernetes-service-account)[Federated identity credential](workload-identity-deploy-cluster#create-the-federated-identity-credential)[Dapr cluster extension](dapr-overview)installed on the AKS cluster

[kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/)installed locally.

## Clone the repository

Clone the

[Dapr quickstarts repository](https://github.com/Azure-Samples/dapr-aks-extension-quickstart)using the`git clone`

command.`git clone https://github.com/Azure-Samples/dapr-aks-extension-quickstart.git`

Change to the

`dapr-aks-extension-quickstart`

directory.

## Create and configure a Redis store

Open the [Azure portal](https://portal.azure.com/#create/Microsoft.Cache) to start the Azure Cache for Redis creation flow.

- Fill out the recommended information according to
[the "Create an open-source Redis cache" quickstart instructions](/en-us/azure/azure-cache-for-redis/quickstart-create-redis). - Select
**Create**to start the Redis instance deployment.

### Verify resource information

- Once the Redis resource is deployed, navigate to its overview page.
- Take note of:
- The hostname, found in the
**Essentials**section of the cache overview page. The hostname format looks similar to:`xxxxxx.redis.cache.windows.net`

. - The SSL port, found in the cache's
**Advanced Settings**blade. The default value is`6380`

.

- The hostname, found in the
- Navigate to the
**Authentication**blade and verify Microsoft Entra Authentication is enabled on your resource.

### Add managed identity

In the

**Authentication**blade, type the name of the[Managed Identity you created as a prerequisite](#prerequisites)in the field under**Enable Microsoft Entra Authentication**checkbox.Verify your managed identity is added as a Redis User assigned Data Owner Access Policy permissions.


### Enable public network access

For this scenario, your Redis cache uses public network access. Be sure to [clean up resources](#clean-up-resources) when you're finished with this quickstart.

- Navigate to the
**Private Endpoint**blade. - Click
**Enable public network access**from the top menu.

## Configure the Dapr components

In `redis.yaml`

, the component is configured to use Entra ID Authentication using workload identity enabled for AKS cluster. No access keys are required.

```
- name: useEntraID
value: "true"
- name: enableTLS
value: true
```


In your preferred code editor, navigate to the

`deploy`

directory in the sample and open`redis.yaml`

.For

`redisHost`

, replace the placeholder`<REDIS_HOST>:<REDIS_PORT>`

value with the Redis cache hostname and SSL port[you saved earlier from Azure portal](#verify-resource-information).`- name: redisHost value: <your-cache-name>.redis.cache.windows.net:6380`


### Apply the configuration

Apply the

`redis.yaml`

file using the`kubectl apply`

command.`kubectl apply -f ./deploy/redis.yaml`

Verify your state store was successfully configured using the

`kubectl get components.redis`

command.`kubectl get components.redis -o yaml`

**Expected output**`component.dapr.io/statestore created`


## Deploy the Node.js app with the Dapr sidecar

### Configure the Node.js app

In `node.yaml`

, the pod spec has the label added to use workload identity:

```
labels:
app: node
azure.workload.identity/use: "true"
```


Navigate to the

`deploy`

directory and open`node.yaml`

.Replace the placeholder

`<SERVICE_ACCOUNT_NAME>`

value for`serviceAccountName`

with[the service account name you created](workload-identity-deploy-cluster#create-a-kubernetes-service-account).- This value should be the same service account you used to create the federated identity credential.


### Apply the configuration

Apply the Node.js app deployment to your cluster using the

`kubectl apply`

command.`kubectl apply -f ./deploy/node.yaml`

Kubernetes deployments are asynchronous, so before moving on to the next steps, verify the deployment is complete with the following command:

`kubectl rollout status deploy/nodeapp`

Access your service using the

`kubectl get svc`

command.`kubectl get svc nodeapp`

Make note of the

`EXTERNAL-IP`

in the output.

### Verify the Node.js service

Using

`curl`

, call the service with your`EXTERNAL-IP`

.`curl $EXTERNAL_IP/ports`

**Example output**`{"DAPR_HTTP_PORT":"3500","DAPR_GRPC_PORT":"50001"}`

Submit an order to the application.

`curl --request POST --data "@sample.json" --header Content-Type:application/json $EXTERNAL_IP/neworder`

Confirm the order.

`curl $EXTERNAL_IP/order`

**Expected output**`{ "orderId": "42" }`


## Deploy the Python app with the Dapr sidecar

### Configure the Python app

In `python.yaml`

, the pod spec has the label added to use workload identity:

```
labels:
app: node
azure.workload.identity/use: "true"
```


Navigate to the

`deploy`

directory and open`python.yaml`

.Replace the placeholder

`<SERVICE_ACCOUNT_NAME>`

value for`serviceAccountName`

with[the service account name you created](workload-identity-deploy-cluster#create-a-kubernetes-service-account).- This value should be the same service account you used to create the federated identity credential.


### Apply the configuration

Deploy the Python app to your Kubernetes cluster using the

`kubectl apply`

command.`kubectl apply -f ./deploy/python.yaml`

Kubernetes deployments are asynchronous, so before moving on to the next steps, verify the deployment is complete with the following command:

`kubectl rollout status deploy/pythonapp`


## Observe messages and confirm persistence

Now that both the Node.js and Python applications are deployed, you can watch messages come through.

Get the logs of the Node.js app using the

`kubectl logs`

command.`kubectl logs --selector=app=node -c node --tail=-1`

**Expected output**`Got a new order! Order ID: 1 Successfully persisted state Got a new order! Order ID: 2 Successfully persisted state Got a new order! Order ID: 3 Successfully persisted state`

Using

`curl`

, call the Node.js app's order endpoint to get the latest order.`curl $EXTERNAL_IP/order`

You should see the latest JSON output in the response.


## Clean up resources

If you no longer plan to use the resources from this quickstart, you can delete all associated resources by removing the resource group.

Remove the resource group, cluster, namespace, and all related resources using the [az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name MyResourceGroup
```

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-secure-gateway -->

# Secure ingress gateway for Istio service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Deploy external or internal Istio Ingress](istio-deploy-ingress) article describes how to configure an ingress gateway to expose an HTTP service to external/internal traffic. This article shows how to expose a secure HTTPS service using either simple or mutual TLS.

## Prerequisites

Enable the Istio add-on on the cluster as per

[documentation](istio-deploy-addon)Deploy an external Istio ingress gateway as per

[documentation](istio-deploy-ingress)

Note

This article refers to the external ingress gateway for demonstration, same steps would apply for configuring mutual TLS for internal ingress gateway.

## Required client/server certificates and keys

This article requires several certificates and keys. You can use your favorite tool to create them or you can use the following [openssl](https://man.openbsd.org/openssl.1) commands.

Create a root certificate and private key for signing the certificates for sample services:

`mkdir bookinfo_certs openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -subj '/O=bookinfo Inc./CN=bookinfo.com' -keyout bookinfo_certs/bookinfo.com.key -out bookinfo_certs/bookinfo.com.crt`

Generate a certificate and private key for

`productpage.bookinfo.com`

:`openssl req -out bookinfo_certs/productpage.bookinfo.com.csr -newkey rsa:2048 -nodes -keyout bookinfo_certs/productpage.bookinfo.com.key -subj "/CN=productpage.bookinfo.com/O=product organization" openssl x509 -req -sha256 -days 365 -CA bookinfo_certs/bookinfo.com.crt -CAkey bookinfo_certs/bookinfo.com.key -set_serial 0 -in bookinfo_certs/productpage.bookinfo.com.csr -out bookinfo_certs/productpage.bookinfo.com.crt`

Generate a client certificate and private key:

`openssl req -out bookinfo_certs/client.bookinfo.com.csr -newkey rsa:2048 -nodes -keyout bookinfo_certs/client.bookinfo.com.key -subj "/CN=client.bookinfo.com/O=client organization" openssl x509 -req -sha256 -days 365 -CA bookinfo_certs/bookinfo.com.crt -CAkey bookinfo_certs/bookinfo.com.key -set_serial 1 -in bookinfo_certs/client.bookinfo.com.csr -out bookinfo_certs/client.bookinfo.com.crt`


## Configure a TLS ingress gateway

Create a Kubernetes TLS secret for the ingress gateway; use [Azure Key Vault](/en-us/azure/key-vault/general/basic-concepts) to host certificates/keys and [Azure Key Vault Secrets Provider add-on](csi-secrets-store-driver) to sync secrets to the cluster.

### Set up Azure Key Vault and sync secrets to the cluster

Create Azure Key Vault

You need an

[Azure Key Vault resource](/en-us/azure/key-vault/general/quick-create-cli)to supply the certificate and key inputs to the Istio add-on.`export AKV_NAME=<azure-key-vault-resource-name> az keyvault create --name $AKV_NAME --resource-group $RESOURCE_GROUP --location $LOCATION`

Enable

[Azure Key Vault provider for Secret Store CSI Driver](csi-secrets-store-driver)add-on on your cluster.`az aks enable-addons --addons azure-keyvault-secrets-provider --resource-group $RESOURCE_GROUP --name $CLUSTER`

If your Key Vault is using Azure RBAC for the permissions model, follow the instructions

[here](/en-us/azure/key-vault/general/rbac-guide#using-azure-rbac-secret-key-and-certificate-permissions-with-key-vault)to assign an Azure role of Key Vault Secrets User for the add-on's user-assigned managed identity. Alternatively, if your key vault is using the vault access policy permissions model, authorize the user-assigned managed identity of the add-on to access Azure Key Vault resource using access policy:`OBJECT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.objectId' -o tsv | tr -d '\r') CLIENT_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER --query 'addonProfiles.azureKeyvaultSecretsProvider.identity.clientId') TENANT_ID=$(az keyvault show --resource-group $RESOURCE_GROUP --name $AKV_NAME --query 'properties.tenantId') az keyvault set-policy --name $AKV_NAME --object-id $OBJECT_ID --secret-permissions get list`

Create secrets in Azure Key Vault using the certificates and keys.

`az keyvault secret set --vault-name $AKV_NAME --name test-productpage-bookinfo-key --file bookinfo_certs/productpage.bookinfo.com.key az keyvault secret set --vault-name $AKV_NAME --name test-productpage-bookinfo-crt --file bookinfo_certs/productpage.bookinfo.com.crt az keyvault secret set --vault-name $AKV_NAME --name test-bookinfo-crt --file bookinfo_certs/bookinfo.com.crt`

Use the following manifest to deploy SecretProviderClass to provide Azure Key Vault specific parameters to the CSI driver.

`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: productpage-credential-spc namespace: aks-istio-ingress spec: provider: azure secretObjects: - secretName: productpage-credential type: kubernetes.io/tls data: - objectName: test-productpage-bookinfo-key key: tls.key - objectName: test-productpage-bookinfo-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $AKV_NAME cloudName: "" objects: | array: - | objectName: test-productpage-bookinfo-key objectType: secret objectAlias: "test-productpage-bookinfo-key" - | objectName: test-productpage-bookinfo-crt objectType: secret objectAlias: "test-productpage-bookinfo-crt" tenantId: $TENANT_ID EOF`

Alternatively, to reference a certificate object type directly from Azure Key Vault, use the following manifest to deploy SecretProviderClass. In this example,

`test-productpage-bookinfo-cert-pxf`

is the name of the certificate object in Azure Key Vault. Refer to[obtain certificates and keys](csi-secrets-store-identity-access?pivots=access-with-a-user-assigned-managed-identity#obtain-certificates-and-keys)section for more information.`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: productpage-credential-spc namespace: aks-istio-ingress spec: provider: azure secretObjects: - secretName: productpage-credential type: kubernetes.io/tls data: - objectName: test-productpage-bookinfo-key key: tls.key - objectName: test-productpage-bookinfo-crt key: tls.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $AKV_NAME cloudName: "" objects: | array: - | objectName: test-productpage-bookinfo-cert-pfx #certificate object name from keyvault objectType: secret objectAlias: "test-productpage-bookinfo-key" - | objectName: test-productpage-bookinfo-cert-pfx #certificate object name from keyvault objectType: cert objectAlias: "test-productpage-bookinfo-crt" tenantId: $TENANT_ID EOF`

Use the following manifest to deploy a sample pod. The secret store CSI driver requires a pod to reference the SecretProviderClass resource to ensure secrets sync from Azure Key Vault to the cluster.

`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: secrets-store-sync-productpage namespace: aks-istio-ingress spec: containers: - name: busybox image: mcr.microsoft.com/oss/busybox/busybox:1.33.1 command: - "/bin/sleep" - "10" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "productpage-credential-spc" EOF`

Verify

`productpage-credential`

secret created on the cluster namespace`aks-istio-ingress`

as defined in the SecretProviderClass resource.`kubectl describe secret/productpage-credential -n aks-istio-ingress`

Example output:

`Name: productpage-credential Namespace: aks-istio-ingress Labels: secrets-store.csi.k8s.io/managed=true Annotations: <none> Type: tls Data ==== cert: 1066 bytes key: 1704 bytes`


### Configure ingress gateway and virtual service

Route HTTPS traffic via the Istio ingress gateway to the sample applications. Use the following manifest to deploy gateway and virtual service resources.

```
cat <<EOF | kubectl apply -f -
apiVersion: networking.istio.io/v1beta1
kind: Gateway
metadata:
name: bookinfo-gateway
spec:
selector:
istio: aks-istio-ingressgateway-external
servers:
- port:
number: 443
name: https
protocol: HTTPS
tls:
mode: SIMPLE
credentialName: productpage-credential
hosts:
- productpage.bookinfo.com
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
name: productpage-vs
spec:
hosts:
- productpage.bookinfo.com
gateways:
- bookinfo-gateway
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
port:
number: 9080
host: productpage
EOF
```


Note

In the gateway definition, `credentialName`

must match the `secretName`

in SecretProviderClass resource and `selector`

must refer to the external ingress gateway by its label, in which the key of the label is `istio`

and the value is `aks-istio-ingressgateway-external`

. For internal ingress gateway label is `istio`

and the value is `aks-istio-ingressgateway-internal`

.

Set environment variables for external ingress host and ports:

```
export INGRESS_HOST_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
export SECURE_INGRESS_PORT_EXTERNAL=$(kubectl -n aks-istio-ingress get service aks-istio-ingressgateway-external -o jsonpath='{.spec.ports[?(@.name=="https")].port}')
export SECURE_GATEWAY_URL_EXTERNAL=$INGRESS_HOST_EXTERNAL:$SECURE_INGRESS_PORT_EXTERNAL
echo "https://$SECURE_GATEWAY_URL_EXTERNAL/productpage"
```


### Verification

Send an HTTPS request to access the productpage service through HTTPS:

```
curl -s -HHost:productpage.bookinfo.com --resolve "productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL:$INGRESS_HOST_EXTERNAL" --cacert bookinfo_certs/bookinfo.com.crt "https://productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


Note

To configure HTTPS ingress access to an HTTPS service, i.e., configure an ingress gateway to perform SNI passthrough instead of TLS termination on incoming requests, update the tls mode in the gateway definition to `PASSTHROUGH`

. This instructs the gateway to pass the ingress traffic “as is”, without terminating TLS.

## Configure a mutual TLS ingress gateway

Extend your gateway definition to support mutual TLS.

Update the ingress gateway credential by deleting the current secret and creating a new one. The server uses the CA certificate to verify its clients, and we must use the key ca.crt to hold the CA certificate.

`kubectl delete secretproviderclass productpage-credential-spc -n aks-istio-ingress kubectl delete secret/productpage-credential -n aks-istio-ingress kubectl delete pod/secrets-store-sync-productpage -n aks-istio-ingress`

Use the following manifest to recreate SecretProviderClass with CA certificate.

`cat <<EOF | kubectl apply -f - apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: productpage-credential-spc namespace: aks-istio-ingress spec: provider: azure secretObjects: - secretName: productpage-credential type: opaque data: - objectName: test-productpage-bookinfo-key key: tls.key - objectName: test-productpage-bookinfo-crt key: tls.crt - objectName: test-bookinfo-crt key: ca.crt parameters: useVMManagedIdentity: "true" userAssignedIdentityID: $CLIENT_ID keyvaultName: $AKV_NAME cloudName: "" objects: | array: - | objectName: test-productpage-bookinfo-key objectType: secret objectAlias: "test-productpage-bookinfo-key" - | objectName: test-productpage-bookinfo-crt objectType: secret objectAlias: "test-productpage-bookinfo-crt" - | objectName: test-bookinfo-crt objectType: secret objectAlias: "test-bookinfo-crt" tenantId: $TENANT_ID EOF`

Use the following manifest to redeploy sample pod to sync secrets from Azure Key Vault to the cluster.

`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: Pod metadata: name: secrets-store-sync-productpage namespace: aks-istio-ingress spec: containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "productpage-credential-spc" EOF`

Verify

`productpage-credential`

secret created on the cluster namespace`aks-istio-ingress`

.`kubectl describe secret/productpage-credential -n aks-istio-ingress`

Example output:

`Name: productpage-credential Namespace: aks-istio-ingress Labels: secrets-store.csi.k8s.io/managed=true Annotations: <none> Type: opaque Data ==== ca.crt: 1188 bytes tls.crt: 1066 bytes tls.key: 1704 bytes`


Use the following manifest to update the gateway definition to set the TLS mode to MUTUAL.

`cat <<EOF | kubectl apply -f - apiVersion: networking.istio.io/v1beta1 kind: Gateway metadata: name: bookinfo-gateway spec: selector: istio: aks-istio-ingressgateway-external # use istio default ingress gateway servers: - port: number: 443 name: https protocol: HTTPS tls: mode: MUTUAL credentialName: productpage-credential # must be the same as secret hosts: - productpage.bookinfo.com EOF`


### Verification

Attempt to send HTTPS request using the prior approach - without passing the client certificate - and see it fail.

```
curl -v -HHost:productpage.bookinfo.com --resolve "productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL:$INGRESS_HOST_EXTERNAL" --cacert bookinfo_certs/bookinfo.com.crt "https://productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL/productpage"
```


Example output:

```
...
* TLSv1.2 (IN), TLS header, Supplemental data (23):
* TLSv1.3 (IN), TLS alert, unknown (628):
* OpenSSL SSL_read: error:0A00045C:SSL routines::tlsv13 alert certificate required, errno 0
* Failed receiving HTTP2 data
* OpenSSL SSL_write: SSL_ERROR_ZERO_RETURN, errno 0
* Failed sending HTTP2 data
* Connection #0 to host productpage.bookinfo.com left intact
curl: (56) OpenSSL SSL_read: error:0A00045C:SSL routines::tlsv13 alert certificate required, errno 0
```


Pass your client’s certificate with the `--cert`

flag and private key with the `--key`

flag to curl.

```
curl -s -HHost:productpage.bookinfo.com --resolve "productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL:$INGRESS_HOST_EXTERNAL" --cacert bookinfo_certs/bookinfo.com.crt --cert bookinfo_certs/client.bookinfo.com.crt --key bookinfo_certs/client.bookinfo.com.key "https://productpage.bookinfo.com:$SECURE_INGRESS_PORT_EXTERNAL/productpage" | grep -o "<title>.*</title>"
```


Confirm that the sample application's product page is accessible. The expected output is:

```
<title>Simple Bookstore App</title>
```


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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/api-server-authorized-ip-ranges -->

# Secure access to the API server using authorized IP address ranges in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use API server authorized IP address ranges to limit which IP addresses and CIDRs can access control plane endpoints for your Azure Kubernetes Service (AKS) workloads.

## Prerequisites

- The Azure CLI version 2.0.76 or later installed and configured. Check your version using the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - To learn what IP addresses to include when integrating your AKS cluster with Azure DevOps, see
[Allowed IP addresses and domain URLs](/en-us/azure/devops/organizations/security/allow-list-ip-url).

Tip

From the Azure portal, you can use Azure Copilot to make changes to the IP addresses that can access your cluster. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#enable-ip-address-authorization).

## Limitations and considerations

- This feature is only supported on the Standard SKU load balancer for clusters created after October 2019. Any existing clusters on the Basic SKU load balancer with the feature enabled should continue to work properly if the Kubernetes version and control plane are upgraded. However, you can't migrate these clusters to the Standard SKU load balancer.
- You can't use this feature with
[private clusters](private-clusters). - When using this feature with clusters that use
[Node public IPs](use-node-public-ips), the node pools using the Node public IPs must use public IP prefixes. You must add the public IP prefixes as authorized ranges. - You can specify up to 200 authorized IP ranges. To go beyond this limit, consider using
[API Server VNet Integration](api-server-vnet-integration), which supports up to 2,000 authorized IP ranges.

## Overview of API server authorized IP ranges

The Kubernetes API server exposes underlying Kubernetes APIs and provides the interaction for management tools like `kubectl`

and the Kubernetes dashboard. AKS provides a single-tenant cluster control plane with a dedicated API server. The API server is assigned a public IP address by default. You can control access using Kubernetes role-based access control (Kubernetes RBAC) or Azure RBAC.

To secure access to the otherwise publicly accessible AKS control plane / API server, you can enable and use authorized IP ranges. These authorized IP ranges only allow defined IP address ranges to communicate with the API server. Any requests made to the API server from an IP address that isn't part of these authorized IP ranges is blocked. The rules can take up to two minutes to propagate. Allow up to that time when testing the connection.

## Recommended IP ranges to allow

We recommend including the following IP address ranges in your API server authorized IP ranges configuration:

- The cluster egress IP address (firewall, NAT gateway, or other address, depending on your
[outbound type](egress-outboundtype)). - Any range that represents networks that you'll administer the cluster from.

## Create an AKS cluster with API server authorized IP ranges enabled

Note

When you enable API server authorized IP ranges during cluster creation, both the API server public IP and the outbound public IP of the [Standard SKU load balancer](load-balancer-standard) are automatically allowed by default, in addition to any ranges you specify.

**Special case - 0.0.0.0/32**: This is a special value that tells AKS to allow only the outbound public IP of the Standard SKU load balancer to access the API server. The

`0.0.0.0/32`

value acts as a placeholder that:- Disables the default behavior of allowing extra client IP ranges.
- Restricts API server access to only the cluster's own outbound IP.
- Is useful for scenarios where you want the cluster to self-manage but block external access.

When creating a cluster with API server authorized IP ranges enabled, you provide a list of authorized public IP address ranges. When you specify a CIDR range, you must use the network address (first IP address in the range). For example, if you want to allow the range `137.117.106.88`

to `137.117.106.95`

, you must specify `137.117.106.88/29`

.

Create an AKS cluster with API server authorized IP ranges enabled using the

command with the`az aks create`

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows the IP address range`73.140.245.0/24`

to access the API server:`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 73.140.245.0/24 --generate-ssh-keys`


Create an AKS cluster with API server authorized IP ranges enabled using the

cmdlet with the`New-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows the IP address range`73.140.245.0/24`

to access the API server:`New-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -NodeVmSetType VirtualMachineScaleSets -LoadBalancerSku Standard -ApiServerAccessAuthorizedIpRange '73.140.245.0/24' -GenerateSshKey`


- From the
[Azure portal home page](https://portal.azure.com/#home), select**Create a resource**>**Containers**>**Azure Kubernetes Service (AKS)**. - Configure the cluster settings as needed.
- In the
**Networking**section under**Public access**, select**Set authorized IP ranges**. - For
**Specify IP ranges**, enter the IP address ranges you want to authorize to access the API server. - Configure the rest of the cluster settings as needed.
- When you're ready, select
**Review + create**>**Create**to create the cluster.

## Specify outbound IPs for a Standard SKU load balancer

When creating a cluster with API server authorized IP ranges enabled, you can also specify the outbound IP addresses or prefixes for the cluster using the `--load-balancer-outbound-ips`

or `--load-balancer-outbound-ip-prefixes`

parameters. All IPs provided in the parameters are allowed along with the IPs in the `--api-server-authorized-ip-ranges`

parameter.

Create an AKS cluster with API server authorized IP ranges enabled and specify the outbound IP addresses for the Standard SKU load balancer using the

`--load-balancer-outbound-ips`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*, allows the IP address range`73.140.245.0/24`

to access the API server, and specifies two outbound IP addresses for the Standard SKU load balancer. Make sure to replace the placeholders`<public-ip-id-1>`

and`<public-ip-id-2>`

with the actual resource IDs of your public IP addresses.`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 73.140.245.0/24 --load-balancer-outbound-ips <public-ip-id-1>,<public-ip-id-2> --generate-ssh-keys`


## Allow only the outbound public IP of the Standard SKU load balancer

Create an AKS cluster with API server authorized IP ranges enabled and allow only the outbound public IP of the Standard SKU load balancer using the

`--api-server-authorized-ip-ranges`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*with API server authorized IP ranges enabled and allows only the outbound public IP of the Standard SKU load balancer:`az aks create --resource-group myResourceGroup --name myAKSCluster --vm-set-type VirtualMachineScaleSets --load-balancer-sku standard --api-server-authorized-ip-ranges 0.0.0.0/32 --generate-ssh-keys`


Create an AKS cluster with API server authorized IP ranges enabled and allow only the outbound public IP of the Standard SKU load balancer using the

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example creates a cluster named*myAKSCluster*in the resource group named*myResourceGroup*with API server authorized IP ranges enabled and allows only the outbound public IP of the Standard SKU load balancer:`New-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -NodeVmSetType VirtualMachineScaleSets -LoadBalancerSku Standard -ApiServerAccessAuthorizedIpRange '0.0.0.0/32' -GenerateSshKey`


- From the
[Azure portal home page](https://portal.azure.com/#home), select**Create a resource**>**Containers**>**Azure Kubernetes Service (AKS)**. - Configure the cluster settings as needed.
- In the
**Networking**section under**Public access**, select**Set authorized IP ranges**. - For
**Specify IP ranges**, enter`0.0.0.0/32`

. This setting allows only the outbound public IP of the Standard SKU load balancer. - Configure the rest of the cluster settings as needed.
- When you're ready, select
**Review + create**>**Create**to create the cluster.

## Update the API server authorized IP ranges on an existing cluster

Update an existing cluster's API server authorized IP ranges using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and updates the IP address range to`73.140.245.0/24`

:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges 73.140.245.0/24`


## Allow multiple IP address ranges

To allow multiple IP address ranges, you can list several IP addresses, separated by commas.

Update an existing cluster's API server authorized IP ranges to allow multiple IP address ranges using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and allows multiple IP address ranges:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges 73.140.245.0/24,193.168.1.0/24,194.168.1.0/24`


Update an existing cluster's API server authorized IP ranges using the

cmdlet with the`Set-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example updates API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*and updates the IP address range to`73.140.245.0/24`

:`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange '73.140.245.0/24'`


- Navigate to the Azure portal and select the AKS cluster you want to update.
- From the service menu, under
**Settings**, select**Networking**. - Under
**Resource settings**, select**Manage**. - On the
**Authorized IP ranges**page, update the**Authorized IP ranges**as needed. - When you're done, select
**Save**.

## Disable API server authorized IP ranges on an existing cluster

Disable API server authorized IP ranges using the

command and specify an empty range`az aks update`

`""`

for the`--api-server-authorized-ip-ranges`

parameter.`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges ""`


Disable API server authorized IP ranges using the

cmdlet and specify an empty range`Set-AzAksCluster`

`''`

for the`-ApiServerAccessAuthorizedIpRange`

parameter.`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange ''`


- Navigate to the Azure portal and select the AKS cluster you want to update.
- From the service menu, under
**Settings**, select**Networking**. - Under
**Resource settings**, select**Manage**. - On the
**Authorized IP ranges**page, deselect the**Set authorized IP ranges**checkbox. - Select
**Save**.

## Find existing API server authorized IP ranges

Find existing API server authorized IP ranges using the

command with the`az aks show`

`--query`

parameter set to`apiServerAccessProfile.authorizedIpRanges`

.`az aks show --resource-group myResourceGroup --name myAKSCluster --query apiServerAccessProfile.authorizedIpRanges`

Example output:

`[ "73.140.245.0/24" ]`


Find existing API server authorized IP ranges using the

cmdlet.`Get-AzAksCluster`

`Get-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster | Select-Object -ExpandProperty ApiServerAccessProfile`

Example output:

`AuthorizedIPRanges: {73.140.245.0/24} ...`


Navigate to the Azure portal and select your AKS cluster.

From the service menu, under

**Settings**, select**Networking**. The existing API server authorized IP ranges are listed under**Resource settings**.

## Access the API server from your development machine, tooling, or automation

You must add your development machines, tooling, or automation IP addresses to the AKS cluster list of approved IP ranges to access the API server from there.

Another option is to configure a jumpbox with the necessary tooling inside a separate subnet in the firewall's virtual network. This option assumes your environment has a firewall with the respective network and that you added the firewall IPs to authorized ranges. Similarly, if you forced tunneling from the AKS subnet to the firewall subnet, having the jumpbox in the cluster subnet also works.

Note

The following example adds another IP address to the approved ranges. It still includes the existing IP address. If you don't include your existing IP address, this command replaces it with the new one instead of adding it to the authorized ranges.

Retrieve your IP address and set it to an environment variable using the following command:

`# Retrieve your IP address CURRENT_IP=$(dig +short "myip.opendns.com" "@resolver1.opendns.com")`

Add your IP address to the approved list using the

command with the`az aks update`

`--api-server-authorized-ip-ranges`

parameter. The following example adds your current IP address to the existing API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*:`az aks update --resource-group myResourceGroup --name myAKSCluster --api-server-authorized-ip-ranges $CURRENT_IP/24,73.140.245.0/24`


Retrieve your IP address and set it to an environment variable using the following command:

`# Retrieve your IP address CURRENT_IP=$(dig +short "myip.opendns.com" "@resolver1.opendns.com")`

Add your IP address to the approved list using the

cmdlet with the`Set-AzAksCluster`

`-ApiServerAccessAuthorizedIpRange`

parameter. The following example adds your current IP address to the existing API server authorized IP ranges on the cluster named*myAKSCluster*in the resource group named*myResourceGroup*:`Set-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster -ApiServerAccessAuthorizedIpRange '$CURRENT_IP/24,73.140.245.0/24'`


Another option is to use the following command on Windows systems to get the public IPv4 address:

```
Invoke-RestMethod http://ipinfo.io/json | Select -exp ip
```


You can also follow the steps in [Find your IP address](https://support.microsoft.com/help/4026518/windows-10-find-your-ip-address) or search on *what is my IP address?* in an internet browser.

## Related content

To learn more about security in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-deploy-add-on-arm -->

# Install the Kubernetes Event-driven Autoscaling (KEDA) add-on using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

This article shows you how to deploy the Kubernetes Event-driven Autoscaling (KEDA) add-on to Azure Kubernetes Service (AKS) using an [ARM template](/en-us/azure/azure-resource-manager/templates/).

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.31.

For more information on how to securely scale your applications with workload identity, please read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, please read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - This article assumes you have an existing Azure resource group. If you don't have an existing resource group, you can create one using the
command.`az group create`

- Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules). [Create an SSH key pair](#create-an-ssh-key-pair).

Note

If you're using [Microsoft Entra Workload ID](/en-us/azure/aks/workload-identity-overview) and you enable KEDA before Workload ID, you need to restart the KEDA operator pods so the proper environment variables can be injected:

Restart the pods by running

`kubectl rollout restart deployment keda-operator -n kube-system`

.Obtain KEDA operator pods using

`kubectl get pod -n kube-system`

and finding pods that begin with`keda-operator`

.Verify successful injection of the environment variables by running

`kubectl describe pod <keda-operator-pod> -n kube-system`

. Under`Environment`

, you should see values for`AZURE_TENANT_ID`

,`AZURE_FEDERATED_TOKEN_FILE`

, and`AZURE_AUTHORITY_HOST`

.

## Create an SSH key pair

Navigate to the

[Azure Cloud Shell](https://shell.azure.com/).Create an SSH key pair using the

command.`az sshkey create`

`az sshkey create --name <sshkey-name> --resource-group <resource-group-name>`


## Enable the KEDA add-on with an ARM template

Deploy the

[ARM template for an AKS cluster](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.kubernetes%2Faks%2Fazuredeploy.json).Select

**Edit template**.Enable the KEDA add-on by specifying the

`workloadAutoScalerProfile`

field in the ARM template, as shown in the following example:`"workloadAutoScalerProfile": { "keda": { "enabled": true } }`

Select

**Save**.Update the required values for the ARM template:

**Subscription**: Select the Azure subscription to use for the deployment.**Resource group**: Select the resource group to use for the deployment.**Region**: Select the region to use for the deployment.**Dns Prefix**: Enter a unique DNS name to use for the cluster.**Linux Admin Username**: Enter a username for the cluster.**SSH public key source**: Select**Use existing key stored in Azure**.**Store Keys**: Select the key pair you created earlier in the article.

Select

**Review + create**>**Create**.

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local device, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client.

If you use the Azure Cloud Shell, `kubectl`

is already installed. You can also install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

- Configure
`kubectl`

to connect to your Kubernetes cluster, use the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. The following example gets credentials for the AKS cluster named*MyAKSCluster*in the*MyResourceGroup*:

```
az aks get-credentials --resource-group MyResourceGroup --name MyAKSCluster
```


## Example deployment

The following snippet is a sample deployment that creates a cluster with KEDA enabled with a single node pool comprised of three `DS2_v5`

nodes.

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"resources": [
{
"apiVersion": "2023-03-01",
"dependsOn": [],
"type": "Microsoft.ContainerService/managedClusters",
"location": "westcentralus",
"name": "myAKSCluster",
"properties": {
"kubernetesVersion": "1.27",
"enableRBAC": true,
"dnsPrefix": "myAKSCluster",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": 200,
"count": 3,
"enableAutoScaling": false,
"vmSize": "Standard_D2S_v5",
"osType": "Linux",
"type": "VirtualMachineScaleSets",
"mode": "System",
"maxPods": 110,
"availabilityZones": [],
"nodeTaints": [],
"enableNodePublicIP": false
}
],
"networkProfile": {
"loadBalancerSku": "standard",
"networkPlugin": "kubenet"
},
"workloadAutoScalerProfile": {
"keda": {
"enabled": true
}
}
},
"identity": {
"type": "SystemAssigned"
}
}
]
}
```


## Start scaling apps with KEDA

You can autoscale your apps with KEDA using custom resource definitions (CRDs). For more information, see the [KEDA documentation](https://keda.sh/docs/scalers/).

## Remove resources

Remove the resource group and all related resources using the

command.`az group delete`

`az group delete --name <resource-group-name>`


## Next steps

This article showed you how to install the KEDA add-on on an AKS cluster, and then verify that it's installed and running. With the KEDA add-on installed on your cluster, you can [deploy a sample application](https://github.com/kedacore/sample-dotnet-worker-servicebus-queue) to start scaling apps.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more, view the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing -->

# Managed NGINX ingress with the application routing add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

One way to route Hypertext Transfer Protocol (HTTP) and secure (HTTPS) traffic to applications running on an Azure Kubernetes Service (AKS) cluster is to use the [Kubernetes Ingress object](https://kubernetes.io/docs/concepts/services-networking/ingress/). When you create an Ingress object that uses the application routing add-on NGINX Ingress classes, the add-on creates, configures, and manages one or more Ingress controllers in your AKS cluster.

This article shows you how to deploy and configure a basic Ingress controller in your AKS cluster.

## Application routing add-on with NGINX features

The application routing add-on with NGINX delivers the following:

- Easy configuration of managed NGINX Ingress controllers based on
[Kubernetes NGINX Ingress controller](https://kubernetes.github.io/ingress-nginx/). - Integration with
[Azure DNS](/en-us/azure/dns/dns-overview)for public and private zone management - SSL termination with certificates stored in Azure Key Vault.

For other configurations, see:

[DNS and SSL configuration](app-routing-dns-ssl)[Application routing add-on configuration](app-routing-nginx-configuration)[Configure internal NGIX ingress controller for Azure private DNS zone](create-nginx-ingress-private-controller).

With the retirement of [Open Service Mesh](https://release-v1-2.docs.openservicemesh.io/) (OSM) by the Cloud Native Computing Foundation (CNCF), using the application routing add-on with OSM is not recommended.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.54.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

- The application routing add-on supports up to five Azure DNS zones.
- The application routing add-on can only be enabled on AKS clusters with
[managed identity](use-managed-identity). - All global Azure DNS zones integrated with the add-on have to be in the same resource group.
- All private Azure DNS zones integrated with the add-on have to be in the same resource group.
- Editing the ingress-nginx
`ConfigMap`

in the`app-routing-system`

namespace isn't supported. - The following snippet annotations are blocked and will prevent an Ingress from being configured:
`load_module`

,`lua_package`

,`_by_lua`

,`location`

,`root`

,`proxy_pass`

,`serviceaccount`

,`{`

,`}`

,`'`

.

## Enable application routing using Azure CLI

### Enable on a new cluster

To enable application routing on a new cluster, use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command, specifying the

`--enable-app-routing`

flag.```
az aks create \
--resource-group <ResourceGroupName> \
--name <ClusterName> \
--location <Location> \
--enable-app-routing \
--generate-ssh-keys
```


### Enable on an existing cluster

To enable application routing on an existing cluster, use the [ az aks approuting enable](/en-us/cli/azure/aks/approuting#az-aks-approuting-enable) command.

```
az aks approuting enable --resource-group <ResourceGroupName> --name <ClusterName>
```


## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure `kubectl`

to connect to your Kubernetes cluster using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --resource-group <ResourceGroupName> --name <ClusterName>
```


## Deploy an application

The application routing add-on uses annotations on Kubernetes Ingress objects to create the appropriate resources.

Create the application namespace called

`aks-store`

to run the example pods using the`kubectl create namespace`

command.`kubectl create namespace aks-store`

Deploy the AKS store application using the following YAML manifest file:

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/sample-manifests/docs/app-routing/aks-store-deployments-and-services.yaml -n aks-store`


This manifest will create the necessary deployments and services for the AKS store application.

### Create the Ingress object

The application routing add-on creates an Ingress class on the cluster named *webapprouting.kubernetes.azure.com*. When you create an Ingress object with this class, it activates the add-on.

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: store-front namespace: aks-store spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - http: paths: - backend: service: name: store-front port: number: 80 path: / pathType: Prefix`

Create the ingress resource using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n aks-store`

The following example output shows the created resource:

`ingress.networking.k8s.io/store-front created`


## Verify the managed Ingress was created

You can verify the managed Ingress was created using the `kubectl get ingress`

command.

```
kubectl get ingress -n aks-store
```


The following example output shows the created managed Ingress:

```
NAME CLASS HOSTS ADDRESS PORTS AGE
store-front webapprouting.kubernetes.azure.com * 51.8.10.109 80 110s
```


You can verify that the AKS store works pointing your browser to the public IP address of the Ingress controller. Find the IP address with kubectl:

```
kubectl get service -n app-routing-system nginx -o jsonpath="{.status.loadBalancer.ingress[0].ip}"
```


## Remove the application routing add-on

To remove the associated namespace, use the `kubectl delete namespace`

command.

```
kubectl delete namespace aks-store
```


To remove the application routing add-on from your cluster, use the [ az aks approuting disable](/en-us/cli/azure/aks/approuting#az-aks-approuting-disable) command.

```
az aks approuting disable --name <ClusterName> --resource-group <ResourceGroupName>
```


Note

To avoid potential disruption of traffic into the cluster when the application routing add-on is disabled, some Kubernetes resources, including *configMaps*, *secrets*, and the *deployment* that runs the controller, will remain on the cluster. These resources are in the *app-routing-system* namespace. You can remove these resources if they're no longer needed by deleting the namespace with `kubectl delete ns app-routing-system`

.

## Next steps

[Configure custom ingress configurations](app-routing-nginx-configuration)shows how to create an advanced Ingress configuration and[configure a custom domain using Azure DNS to manage DNS zones and setup a secure ingress](app-routing-dns-ssl).To integrate with an Azure internal load balancer and configure a private Azure DNS zone to enable DNS resolution for the private endpoints to resolve specific domains, see

[Configure internal NGINX ingress controller for Azure private DNS zone](create-nginx-ingress-private-controller).Learn about monitoring the ingress-nginx controller metrics included with the application routing add-on with

[with Prometheus in Grafana](app-routing-nginx-prometheus)(preview) as part of analyzing the performance and usage of your application.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/custom-node-configuration -->

# Customize the node configuration for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Customizing your node configuration allows you to adjust operating system (OS) settings or kubelet parameters to match the needs of your workloads. When you create an AKS cluster or add a node pool to your cluster, you can customize a subset of commonly used OS and kubelet settings. To configure settings beyond this subset, you can [use a daemon set to customize your needed configurations without losing AKS support for your nodes](support-policies#shared-responsibility).

## Create custom node configuration files for AKS node pools

OS and kubelet configuration changes require you to create a new configuration file with the parameters and your desired settings. If a value for a parameter isn't specified, then the value is set to the default.

Note

The following examples show common configuration settings. You can modify the settings to meet your workload requirements. For a full list of supported custom configuration parameters, see the [Supported custom configuration parameters](#supported-custom-configuration-parameters) section.

### Kubelet configuration

Create a `linuxkubeletconfig.json`

file with the following contents:

```
{
"cpuManagerPolicy": "static",
"cpuCfsQuota": true,
"cpuCfsQuotaPeriod": "200ms",
"imageGcHighThreshold": 90,
"imageGcLowThreshold": 70,
"topologyManagerPolicy": "best-effort",
"allowedUnsafeSysctls": [
"kernel.msg*",
"net.*"
],
"failSwapOn": false
}
```


### OS configuration

Create a `linuxosconfig.json`

file with the following contents:

```
{
"transparentHugePageEnabled": "madvise",
"transparentHugePageDefrag": "defer+madvise",
"swapFileSizeMB": 1500,
"sysctls": {
"netCoreSomaxconn": 163849,
"netIpv4TcpTwReuse": true,
"netIpv4IpLocalPortRange": "32000 60000"
}
}
```


## Create an AKS cluster using custom configuration files

Note

Keep the following information in mind when using custom configuration files when creating a new AKS cluster:

- If you specify a configuration when creating a cluster, the configuration applies only to the nodes in the initial node pool. Any settings not configured in the JSON file retain their default values.
`CustomLinuxOsConfig`

isn't supported for the Windows OS type.

Create a new cluster using custom configuration files using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and specifying your configuration files for the

`--kubelet-config`

and `--linux-os-config`

parameters. The following example command creates a new cluster with the custom `./linuxkubeletconfig.json`

and `./linuxosconfig.json`

files:```
az aks create --name <cluster-name> --resource-group <resource-group-name> --kubelet-config ./linuxkubeletconfig.json --linux-os-config ./linuxosconfig.json
```


## Add a node pool using custom configuration files

Note

Keep the following information in mind when using custom configuration files when adding a new node pool to an existing AKS cluster:

- When you add a Linux node pool to an existing cluster, you can specify the kubelet configuration, OS configuration, or both. When you add a Windows node pool to an existing cluster, you can only specify the kubelet configuration. If you specify a configuration when adding a node pool, the configuration applies only to the nodes in the new node pool. Any settings not configured in the JSON file retain their default values.
`CustomKubeletConfig`

is supported for Linux and Windows node pools.

Create a new Linux node pool using the [ az aks nodepool add](/en-us/cli/azure/aks#az-aks-create) command and specifying your configuration files for the

`--kubelet-config`

and `--linux-os-config`

parameters. The following example command creates a new Linux node pool with the custom `./linuxkubeletconfig.json`

file:```
az aks nodepool add --name <node-pool-name> --cluster-name <cluster-name> --resource-group <resource-group-name> --kubelet-config ./linuxkubeletconfig.json
```


## Confirm settings were applied

After you apply custom node configuration, you can confirm the settings were applied to the nodes by [connecting to the host](node-access) and verifying `sysctl`

or configuration changes were made on the filesystem.

## Supported custom configuration parameters

### Linux kubelet custom configuration

| Parameter | Allowed values/interval | Default | Description |
|---|---|---|---|
`cpuManagerPolicy` |
none, static | none | The static policy allows containers in
|

`cpuCfsQuota`

`cpuCfsQuotaPeriod`

`100ms`

`imageGcHighThreshold`

`imageGcLowThreshold`

`imageGcHighThreshold`

*can*trigger garbage collection.`topologyManagerPolicy`

[Control Topology Management Policies on a node](https://kubernetes.io/docs/tasks/administer-cluster/topology-manager/).`allowedUnsafeSysctls`

`kernel.shm*`

, `kernel.msg*`

, `kernel.sem`

, `fs.mqueue.*`

, `net.*`

`containerLogMaxSizeMB`

`containerLogMaxFiles`

`podMaxPids`

`seccompDefault`

`Unconfined`

, `RuntimeDefault`

`Unconfined`

`RuntimeDefault`

uses containerd's default seccomp profile, restricting certain system calls to enhance security. Restricted syscalls fail. `Unconfined`

places no restrictions on syscalls, allowing all system calls and reducing security. For more information, see the [containerd default seccomp profile](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51). This parameter is in preview.[Register](/en-us/azure/azure-resource-manager/management/preview-features?tabs=azure-cli#register-preview-feature)the "KubeletDefaultSeccompProfilePreview" feature flag using the[command with](/en-us/cli/azure/feature#az-feature-register)`az feature register`

`--namespace "Microsoft.ContainerService"`

.### Windows kubelet custom configuration

| Parameter | Allowed values/interval | Default | Description |
|---|---|---|---|
`imageGcHighThreshold` |
0-100 | 85 | The percent of disk usage after which image garbage collection is always run. Minimum disk usage that triggers garbage collection. To disable image garbage collection, set to 100. |
`imageGcLowThreshold` |
0-100, no higher than `imageGcHighThreshold` |
80 | The percent of disk usage before which image garbage collection is never run. Minimum disk usage that can trigger garbage collection. |
`containerLogMaxSizeMB` |
Size in megabytes (MB) | 10 | The maximum size (for example, 10 MB) of a container log file before it gets rotated. |
`containerLogMaxFiles` |
≥ 2 | 5 | The maximum number of container log files that can be present for a container. |

## Linux custom OS configuration settings

Important

To simplify search and readability, the OS settings are displayed in this article by their name, but they should be added to the configuration JSON file or AKS API using the [camelCase capitalization convention](/en-us/dotnet/standard/design-guidelines/capitalization-conventions).

For example, if you modify the `vm.max_map_count setting`

, you should reformat to `vmMaxMapCount`

in the configuration JSON file.

### Linux file handle limits

When serving high amounts of traffic, that traffic commonly comes from a large number of local files. You can adjust the following kernel settings and built-in limits to allow you to handle more, at the cost of some system memory.

The following table lists the file handle limits that you can customize per node pool:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`fs.file-max` |
8192 - 9223372036854775807 | 9223372036854775807 | 9223372036854775807 | 9223372036854775807 | Maximum number of file-handles that the Linux kernel allocates. This value is set to the maximum possible value (2^63-1) to prevent file descriptor exhaustion and ensure unlimited system-wide file handles for containerized workloads. |
`fs.inotify.max_user_watches` |
781250 - 2097152 | 1048576 | 1048576 | 1048576 | Maximum number of file watches allowed by the system. Each watch is roughly 90 bytes on a 32-bit kernel, and roughly 160 bytes on a 64-bit kernel. |
`fs.aio-max-nr` |
65536 - 6553500 | 65536 | 65536 | 65536 | The aio-nr shows the current system-wide number of asynchronous io requests. aio-max-nr allows you to change the maximum value aio-nr can grow to. |
`fs.nr_open` |
8192 - 20000500 | 1048576 | 1048576 | 1073741816 | The maximum number of file-handles a process can allocate. |

Note

The `fs.file-max`

parameter is set to 9223372036854775807 (the maximum value for a signed 64-bit integer) across Ubuntu and Azure Linux based on upstream defaults. This configuration:

**Prevents denial-of-service attacks**based on system-wide file descriptor exhaustion.**Ensures container workloads**are never bottlenecked by system-wide file handle limits.**Maintains security**through per-process limits (`fs.nr_open`

and`ulimit`

) which still apply to individual processes.**Optimizes for container platforms**where many containers might run simultaneously, each potentially opening many files and network connection.

### Linux socket and network tuning

For agent nodes, which are expected to handle large numbers of concurrent sessions, you can use following TCP and network options and adjust them per node pool:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`net.core.somaxconn` |
4096 - 3240000 | 16384 | 16384 | 16384 | Maximum number of connection requests that can be queued for any given listening socket. An upper limit for the value of the backlog parameter passed to the
`somaxconn` , then it's silently truncated to this limit. |

`net.core.netdev_max_backlog`

`net.core.rmem_max`

`net.core.wmem_max`

`net.core.optmem_max`

`net.ipv4.tcp_max_syn_backlog`

`net.ipv4.tcp_max_tw_buckets`

`timewait`

sockets held by system simultaneously. If this number is exceeded, time-wait socket is immediately destroyed and warning is printed.`net.ipv4.tcp_fin_timeout`

`net.ipv4.tcp_keepalive_time`

`keepalive`

messages when `keepalive`

is enabled.`net.ipv4.tcp_keepalive_probes`

`keepalive`

probes TCP sends out, until it decides that the connection is broken.`net.ipv4.tcp_keepalive_intvl`

`tcp_keepalive_probes`

it makes up the time to kill a connection that isn't responding, after probes started.`net.ipv4.tcp_tw_reuse`

`TIME-WAIT`

sockets for new connections when it's safe from protocol viewpoint.`net.ipv4.ip_local_port_range`

`net.ipv4.neigh.default.gc_thresh1`

`net.ipv4.neigh.default.gc_thresh2`

`net.ipv4.neigh.default.gc_thresh3`

`net.netfilter.nf_conntrack_max`

`nf_conntrack`

is a module that tracks connection entries for NAT within Linux. The `nf_conntrack`

module uses a hash table to record the *established connection*record of the TCP protocol.`nf_conntrack_max`

is the maximum number of nodes in the hash table, that is, the maximum number of connections supported by the `nf_conntrack`

module or the size of connection tracking table. **Default value**is dynamically calculated based on system memory using the formula:`RAM_in_bytes / 16384`

(or `RAM_in_MB * 64`

). For example, a VM with 8 GB RAM has a default of approximately 524,288 connections. Actual values vary based on the VM size and available memory.`net.netfilter.nf_conntrack_buckets`

`nf_conntrack`

is a module that tracks connection entries for NAT within Linux. The `nf_conntrack`

module uses a hash table to record the *established connection*record of the TCP protocol.`nf_conntrack_buckets`

is the size of hash table. **Default value**is dynamically calculated based on system memory using the formula:`RAM_in_bytes / 16384`

, with a minimum of 1,024 buckets and a maximum of 262,144 buckets. The default `nf_conntrack_max`

is typically set to `nf_conntrack_buckets * 4`

. Actual values vary based on the VM size and available memory.### Linux worker limits

Like file descriptor limits, the number of workers or threads that a process can create are limited by both a kernel setting and user limits. The user limit on AKS is unlimited. The following table lists the kernel setting that you can customize per node pool:

| Setting | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|
`kernel.threads-max` |
Dynamically calculated | Dynamically calculated | Dynamically calculated | Processes can spin up worker threads. The maximum number of all threads that can be created is set with the kernel setting `kernel.threads-max` . Default value is dynamically calculated based on system memory using the formula: `total_ram_pages / 4` (where each page is typically 4 KB). Actual values vary based on the VM size and available memory. |

### Linux virtual memory

The following table lists the kernel settings that you can customize per node pool to tune the operation of the virtual memory (VM) subsystem of the Linux kernel and the `writeout`

of dirty data to disk:

| Setting | Allowed values/interval | Ubuntu 22.04 default | Ubuntu 24.04 default | Azure Linux 3.0 default | Description |
|---|---|---|---|---|---|
`vm.max_map_count` |
65530 | 1048576 | 1048576 | This file contains the maximum number of memory map areas a process can have. Memory map areas are used as a side-effect of calling `malloc` , directly by `mmap` , `mprotect` , and `madvise` , and also when loading shared libraries. |
|
`vm.vfs_cache_pressure` |
1 - 100 | 100 | 100 | 100 | This percentage value controls the tendency of the kernel to reclaim the memory, which is used for caching of directory and inode objects. |
`vm.swappiness` |
0 - 100 | 60 | 60 | 60 | This control is used to define how aggressively the kernel swaps memory pages. Higher values increase aggressiveness, lower values decrease the amount of swap. A value of 0 instructs the kernel not to initiate swap until the amount of free and file-backed pages is less than the high water mark in a zone. |
`swapFileSizeMB` |
1 MB - Size of the
|

`transparentHugePageEnabled`

`always`

, `madvise`

, `never`

`always`

`always`

`madvise`

[Transparent Hugepages](https://www.kernel.org/doc/html/latest/admin-guide/mm/transhuge.html#admin-guide-transhuge)is a Linux kernel feature intended to improve performance by making more efficient use of your processor's memory-mapping hardware. When enabled the kernel attempts to allocate`hugepages`

whenever possible and any Linux process receives 2-MB pages if the `mmap`

region is 2 MB naturally aligned. In certain cases when `hugepages`

are enabled system wide, applications might end up allocating more memory resources. An application might `mmap`

a large region but only touch 1 byte of it, in that case a 2-MB page might be allocated instead of a 4k page for no good reason. This scenario is why it's possible to disable `hugepages`

system-wide or to only have them inside `MADV_HUGEPAGE madvise`

regions.`transparentHugePageDefrag`

`always`

, `defer`

, `defer+madvise`

, `madvise`

, `never`

`madvise`

`madvise`

`madvise`

`hugepages`

available.## Related content

- Learn
[how to configure your AKS cluster](concepts-clusters-workloads). - Learn how
[upgrade the node images](node-image-upgrade)in your cluster. - See
[Upgrade an Azure Kubernetes Service (AKS) cluster](upgrade-cluster)to learn how to upgrade your cluster to the latest version of Kubernetes. - See the list of
[Frequently asked questions about AKS](faq)to find answers to some common AKS questions.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing -->

# Managed NGINX ingress with the application routing add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

One way to route Hypertext Transfer Protocol (HTTP) and secure (HTTPS) traffic to applications running on an Azure Kubernetes Service (AKS) cluster is to use the [Kubernetes Ingress object](https://kubernetes.io/docs/concepts/services-networking/ingress/). When you create an Ingress object that uses the application routing add-on NGINX Ingress classes, the add-on creates, configures, and manages one or more Ingress controllers in your AKS cluster.

This article shows you how to deploy and configure a basic Ingress controller in your AKS cluster.

## Application routing add-on with NGINX features

The application routing add-on with NGINX delivers the following:

- Easy configuration of managed NGINX Ingress controllers based on
[Kubernetes NGINX Ingress controller](https://kubernetes.github.io/ingress-nginx/). - Integration with
[Azure DNS](/en-us/azure/dns/dns-overview)for public and private zone management - SSL termination with certificates stored in Azure Key Vault.

For other configurations, see:

[DNS and SSL configuration](app-routing-dns-ssl)[Application routing add-on configuration](app-routing-nginx-configuration)[Configure internal NGIX ingress controller for Azure private DNS zone](create-nginx-ingress-private-controller).

With the retirement of [Open Service Mesh](https://release-v1-2.docs.openservicemesh.io/) (OSM) by the Cloud Native Computing Foundation (CNCF), using the application routing add-on with OSM is not recommended.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.54.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

- The application routing add-on supports up to five Azure DNS zones.
- The application routing add-on can only be enabled on AKS clusters with
[managed identity](use-managed-identity). - All global Azure DNS zones integrated with the add-on have to be in the same resource group.
- All private Azure DNS zones integrated with the add-on have to be in the same resource group.
- Editing the ingress-nginx
`ConfigMap`

in the`app-routing-system`

namespace isn't supported. - The following snippet annotations are blocked and will prevent an Ingress from being configured:
`load_module`

,`lua_package`

,`_by_lua`

,`location`

,`root`

,`proxy_pass`

,`serviceaccount`

,`{`

,`}`

,`'`

.

## Enable application routing using Azure CLI

### Enable on a new cluster

To enable application routing on a new cluster, use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command, specifying the

`--enable-app-routing`

flag.```
az aks create \
--resource-group <ResourceGroupName> \
--name <ClusterName> \
--location <Location> \
--enable-app-routing \
--generate-ssh-keys
```


### Enable on an existing cluster

To enable application routing on an existing cluster, use the [ az aks approuting enable](/en-us/cli/azure/aks/approuting#az-aks-approuting-enable) command.

```
az aks approuting enable --resource-group <ResourceGroupName> --name <ClusterName>
```


## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure `kubectl`

to connect to your Kubernetes cluster using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --resource-group <ResourceGroupName> --name <ClusterName>
```


## Deploy an application

The application routing add-on uses annotations on Kubernetes Ingress objects to create the appropriate resources.

Create the application namespace called

`aks-store`

to run the example pods using the`kubectl create namespace`

command.`kubectl create namespace aks-store`

Deploy the AKS store application using the following YAML manifest file:

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/sample-manifests/docs/app-routing/aks-store-deployments-and-services.yaml -n aks-store`


This manifest will create the necessary deployments and services for the AKS store application.

### Create the Ingress object

The application routing add-on creates an Ingress class on the cluster named *webapprouting.kubernetes.azure.com*. When you create an Ingress object with this class, it activates the add-on.

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: store-front namespace: aks-store spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - http: paths: - backend: service: name: store-front port: number: 80 path: / pathType: Prefix`

Create the ingress resource using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n aks-store`

The following example output shows the created resource:

`ingress.networking.k8s.io/store-front created`


## Verify the managed Ingress was created

You can verify the managed Ingress was created using the `kubectl get ingress`

command.

```
kubectl get ingress -n aks-store
```


The following example output shows the created managed Ingress:

```
NAME CLASS HOSTS ADDRESS PORTS AGE
store-front webapprouting.kubernetes.azure.com * 51.8.10.109 80 110s
```


You can verify that the AKS store works pointing your browser to the public IP address of the Ingress controller. Find the IP address with kubectl:

```
kubectl get service -n app-routing-system nginx -o jsonpath="{.status.loadBalancer.ingress[0].ip}"
```


## Remove the application routing add-on

To remove the associated namespace, use the `kubectl delete namespace`

command.

```
kubectl delete namespace aks-store
```


To remove the application routing add-on from your cluster, use the [ az aks approuting disable](/en-us/cli/azure/aks/approuting#az-aks-approuting-disable) command.

```
az aks approuting disable --name <ClusterName> --resource-group <ResourceGroupName>
```


Note

To avoid potential disruption of traffic into the cluster when the application routing add-on is disabled, some Kubernetes resources, including *configMaps*, *secrets*, and the *deployment* that runs the controller, will remain on the cluster. These resources are in the *app-routing-system* namespace. You can remove these resources if they're no longer needed by deleting the namespace with `kubectl delete ns app-routing-system`

.

## Next steps

[Configure custom ingress configurations](app-routing-nginx-configuration)shows how to create an advanced Ingress configuration and[configure a custom domain using Azure DNS to manage DNS zones and setup a secure ingress](app-routing-dns-ssl).To integrate with an Azure internal load balancer and configure a private Azure DNS zone to enable DNS resolution for the private endpoints to resolve specific domains, see

[Configure internal NGINX ingress controller for Azure private DNS zone](create-nginx-ingress-private-controller).Learn about monitoring the ingress-nginx controller metrics included with the application routing add-on with

[with Prometheus in Grafana](app-routing-nginx-prometheus)(preview) as part of analyzing the performance and usage of your application.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-deploy-add-on-cli -->

# Install the Kubernetes Event-driven Autoscaling (KEDA) add-on using the Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

This article shows you how to install the Kubernetes Event-driven Autoscaling (KEDA) add-on to Azure Kubernetes Service (AKS) using the Azure CLI.

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.31.

For more information on how to securely scale your applications with workload identity, please read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, please read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules).

Note

If you're using [Microsoft Entra Workload ID](/en-us/azure/aks/workload-identity-overview) and you enable KEDA before Workload ID, you need to restart the KEDA operator pods so the proper environment variables can be injected:

Restart the pods by running

`kubectl rollout restart deployment keda-operator -n kube-system`

.Obtain KEDA operator pods using

`kubectl get pod -n kube-system`

and finding pods that begin with`keda-operator`

.Verify successful injection of the environment variables by running

`kubectl describe pod <keda-operator-pod> -n kube-system`

. Under`Environment`

, you should see values for`AZURE_TENANT_ID`

,`AZURE_FEDERATED_TOKEN_FILE`

, and`AZURE_AUTHORITY_HOST`

.

## Install the KEDA add-on with Azure CLI

To install the KEDA add-on, use `--enable-keda`

when creating or updating a cluster.

## Enable the KEDA add-on on your AKS cluster

Note

While KEDA provides various customization options, the KEDA add-on currently provides basic common configuration.

If you require custom configurations, you can manually edit the KEDA YAML files to customize the installation. **Azure doesn't offer support for custom configurations**.

### Create a new AKS cluster with KEDA add-on enabled

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

Create a new AKS cluster using the

command and enable the KEDA add-on using the`az aks create`

`--enable-keda`

flag.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-keda \ --generate-ssh-keys`


### Enable the KEDA add-on on an existing AKS cluster

Update an existing cluster using the

command and enable the KEDA add-on using the`az aks update`

`--enable-keda`

flag.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --enable-keda`


## Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Verify the KEDA add-on is installed on your cluster

Verify the KEDA add-on is installed on your cluster using the

command and set the`az aks show`

`--query`

parameter to`workloadAutoScalerProfile.keda.enabled`

.`az aks show --resource-group myResourceGroup --name myAKSCluster --query "workloadAutoScalerProfile.keda.enabled"`

The following example output shows the KEDA add-on is installed on the cluster:

`true`


## Verify KEDA is running on your cluster

Verify the KEDA add-on is running on your cluster using the

`kubectl get pods`

command.`kubectl get pods -n kube-system`

The following example output shows the KEDA operator, admissions hook, and metrics API server are installed on the cluster:

`keda-admission-webhooks-**********-2n9zl 1/1 Running 0 3d18h keda-admission-webhooks-**********-69dkg 1/1 Running 0 3d18h keda-operator-*********-4hb5n 1/1 Running 0 3d18h keda-operator-*********-pckpx 1/1 Running 0 3d18h keda-operator-metrics-apiserver-**********-gqg4s 1/1 Running 0 3d18h keda-operator-metrics-apiserver-**********-trfcb 1/1 Running 0 3d18h`


## Verify the KEDA version on your cluster

To verify the version of your KEDA, use `kubectl get crd/scaledobjects.keda.sh -o yaml `

. For example:

```
kubectl get crd/scaledobjects.keda.sh -o yaml
```


The following example output shows the configuration of KEDA in the `app.kubernetes.io/version`

label:

```
apiVersion: apiextensions.k8s.io/v1
kind: CustomResourceDefinition
metadata:
annotations:
controller-gen.kubebuilder.io/version: v0.9.0
meta.helm.sh/release-name: aks-managed-keda
meta.helm.sh/release-namespace: kube-system
creationTimestamp: "2023-08-09T15:58:56Z"
generation: 1
labels:
app.kubernetes.io/component: operator
app.kubernetes.io/managed-by: Helm
app.kubernetes.io/name: keda-operator
app.kubernetes.io/part-of: keda-operator
app.kubernetes.io/version: 2.10.1
helm.toolkit.fluxcd.io/name: keda-adapter-helmrelease
helm.toolkit.fluxcd.io/namespace: 64d3b6fd3365790001260647
name: scaledobjects.keda.sh
resourceVersion: "1421"
uid: 29109c8c-638a-4bf5-ac1b-c28ad9aa11fa
spec:
conversion:
strategy: None
group: keda.sh
names:
kind: ScaledObject
listKind: ScaledObjectList
plural: scaledobjects
shortNames:
- so
singular: scaledobject
scope: Namespaced
# Redacted due to length
```


## Disable the KEDA add-on on your AKS cluster

Disable the KEDA add-on on your cluster using the

command with the`az aks update`

`--disable-keda`

flag.`az aks update \ --resource-group myResourceGroup \ --name myAKSCluster \ --disable-keda`


## Next steps

This article showed you how to install the KEDA add-on on an AKS cluster using the Azure CLI.

With the KEDA add-on installed on your cluster, you can [deploy a sample application](https://github.com/kedacore/sample-dotnet-worker-servicebus-queue) to start scaling apps.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more, view the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/planned-maintenance -->

# Use planned maintenance to schedule and control upgrades for your Azure Kubernetes Service cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use planned maintenance to schedule and control cluster and node image upgrades in Azure Kubernetes Service (AKS).

Regular maintenance is performed on your AKS cluster automatically. There are two types of maintenance operations:

**AKS-initiated maintenance**involves the weekly releases that AKS performs to keep your cluster up to date with the latest features and fixes.**User-initiated maintenance**includes[cluster auto-upgrades](upgrade-cluster)and[node operating system (OS) automatic security updates](auto-upgrade-node-image).

When you use the feature of planned maintenance in AKS, you can run both types of maintenance in a cadence of your choice to minimize workload impact.

Note

You can use planned maintenance to schedule the timing of automatic upgrades, but enabling or disabling planned maintenance doesn't enable or disable automatic upgrades.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you don't have an AKS cluster, see
[Create an AKS cluster](learn/quick-kubernetes-deploy-cli). - If you're using the Azure CLI, upgrade to the latest version using the
command.`az upgrade`


## Considerations

When you use planned maintenance, the following considerations apply:

- AKS reserves the right to break planned maintenance windows for unplanned, reactive maintenance operations that are urgent or critical. These maintenance operations might even run during the
`notAllowedTime`

or`notAllowedDates`

periods defined in your configuration. - Maintenance operations are considered
*best effort only*and aren't guaranteed to occur within a specified window.

## Schedule configuration types for planned maintenance

Three schedule configuration types are available for planned maintenance:

`default`

is a basic configuration for controlling AKS releases, which covers control plane components and system add-ons upgrade. The releases can take up to two weeks to roll out to all regions from the initial time of shipping, because of Azure safe deployment practices.Choose

`default`

to schedule these updates in a manner that's least disruptive for you. You can monitor the status of an ongoing AKS release by region with the[weekly release tracker](release-tracker).`aksManagedAutoUpgradeSchedule`

controls when to perform cluster upgrades scheduled by your designated auto-upgrade channel. You can configure more finely controlled cadence and recurrence settings with this configuration compared to the`default`

configuration. For more information on cluster auto-upgrade, see[Automatically upgrade an Azure Kubernetes Service cluster](upgrade-cluster).`aksManagedNodeOSUpgradeSchedule`

controls when to perform the node OS security patching scheduled by your node OS auto-upgrade channel. You can configure more finely controlled cadence and recurrence settings with this configuration compared to the`default`

configuration. For more information on node OS auto-upgrade channels, see[Automatically patch and update AKS cluster node images](auto-upgrade-node-image).

We recommend using `aksManagedAutoUpgradeSchedule`

for all cluster Kubernetes version upgrade scenarios and `aksManagedNodeOSUpgradeSchedule`

for all node OS security patching scenarios.

The `default`

option is meant exclusively for AKS weekly releases. Use `default`

if you want to control the upgrade schedule for AKS control plane components (such as API Server, ETCD, etc.) and add-ons (such as CoreDNS, Metrics Server, etc.).

All three types of configurations can coexist.

## Create a maintenance window

Note

When you're using auto-upgrade, to ensure proper functionality, use a maintenance window with a duration of four hours or more.

Note

From the 2023-05-01 API version onwards, use the properties in the following table for `default`

configuration.

An `aksManagedAutoUpgradeSchedule`

or `aksManagedNodeOSUpgradeSchedule`

maintenance window and `default`

configuration from 2023-05-01 API version onwards has the following properties:

| Name | Description | Default value |
|---|---|---|
`utcOffset` |
The time zone for cluster maintenance. | `+00:00` |
`startDate` |
The date on which the maintenance window begins to take effect. | The current date at creation time |
`startTime` |
The time for maintenance to begin, based on the time zone determined by `utcOffset` . |
Not applicable |
`schedule` |
The upgrade frequency. Three types are available: `Weekly` , `AbsoluteMonthly` , and `RelativeMonthly` . |
Not applicable |
`intervalDays` |
The interval in days for maintenance runs. It's applicable only to `aksManagedNodeOSUpgradeSchedule` . |
Not applicable |
`intervalWeeks` |
The interval in weeks for maintenance runs. | Not applicable |
`intervalMonths` |
The interval in months for maintenance runs. | Not applicable |
`dayOfWeek` |
The specified day of the week for maintenance to begin. | Not applicable |
`durationHours` |
The duration of the window for maintenance to run. | Not applicable |
`notAllowedDates` |
A range of dates that maintenance can't run, determined by `start` and `end` child properties. It's applicable only when you're creating the maintenance window by using a configuration file. |
Not applicable |

### Deprecated properties

Note

If you create a `default`

configuration with the following deprecated properties, it migrates automatically to the new properties shown in the previous table.

**[Deprecated]** A `default`

maintenance window has the following legacy properties:

| Name | Description | Default value |
|---|---|---|
`timeInWeek` |
In a `default` configuration, this property contains the `day` and `hourSlots` values that define a maintenance window. |
Not applicable |
`timeInWeek.day` |
The day of the week to perform maintenance in a `default` configuration. |
Not applicable |
`timeInWeek.hourSlots` |
A list of hour-long time slots to perform maintenance on a particular day in a `default` configuration. |
Not applicable |
`notAllowedTime` |
A range of dates that maintenance can't run, determined by `start` and `end` child properties. This property is applicable only when you're creating the maintenance window by using a configuration file. |
Not applicable |

### Schedule types

Four schedule types are supported: `Daily`

, `Weekly`

, `AbsoluteMonthly`

, and `RelativeMonthly`

.

The following table shows which types are available for each maintenance-configuration option:

| Schedule type | `default` |
`aksManagedClusterAutoUpgradeSchedule` |
`aksManagedNodeOSUpgradeSchedule` |
|---|---|---|---|
| Daily | Unsupported ❌ | Supported ✅ (after Jun 2025) | Supported ✅ |
| Weekly | Supported ✅ | Supported ✅ | Supported ✅ |
| AbsoluteMonthly | Unsupported ❌ | Supported ✅ | Supported ✅ |
| RelativeMonthly | Unsupported ❌ | Supported ✅ | Supported ✅ |

All of the fields shown for each schedule type are required.

A `Daily`

schedule might look like "every three days":

```
"schedule": {
"daily": {
"intervalDays": 3
}
}
```


A `Weekly`

schedule might look like "every two weeks on Friday":

```
"schedule": {
"weekly": {
"intervalWeeks": 2,
"dayOfWeek": "Friday"
}
}
```


An `AbsoluteMonthly`

schedule might look like "every three months on the first day of the month":

```
"schedule": {
"absoluteMonthly": {
"intervalMonths": 3,
"dayOfMonth": 1
}
}
```


A `RelativeMonthly`

schedule might look like "every two months on the last Monday":

```
"schedule": {
"relativeMonthly": {
"intervalMonths": 2,
"dayOfWeek": "Monday",
"weekIndex": "Last"
}
}
```


Valid values for `weekIndex`

include `First`

, `Second`

, `Third`

, `Fourth`

, and `Last`

.

## Add a maintenance window configuration

Add a maintenance window configuration to an AKS cluster using the [ az aks maintenanceconfiguration add](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-add) command.

The first example adds a new `default`

configuration that schedules maintenance to run from 1:00 AM to 5:00 AM every Monday in the `UTC`

time zone. The second example adds a new `aksManagedAutoUpgradeSchedule`

configuration that schedules maintenance to run every third Friday between 12:00 AM and 8:00 AM in the `UTC+5:30`

time zone.

```
# Add a new default configuration
az aks maintenanceconfiguration add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name default --schedule-type Weekly --day-of-week Monday --interval-weeks 1 --duration 4 --utc-offset +00:00 --start-time 01:00
# Add a new aksManagedAutoUpgradeSchedule configuration
az aks maintenanceconfiguration add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name aksManagedAutoUpgradeSchedule --schedule-type Weekly --day-of-week Friday --interval-weeks 3 --duration 8 --utc-offset +05:30 --start-time 00:00
```


## Update an existing maintenance window

Update an existing maintenance configuration using the [ az aks maintenanceconfiguration update](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-update) command.

The following example updates the `default`

configuration to schedule maintenance to run from 2:00 AM to 6:00 AM every Friday:

```
az aks maintenanceconfiguration update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name default --schedule-type Weekly --day-of-week Friday --interval-weeks 1 --duration 4 --utc-offset +00:00 --start-time 02:00
```


## List all maintenance windows in an existing cluster

List the current maintenance configuration windows in your AKS cluster using the [ az aks maintenanceconfiguration list](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-list) command:

```
az aks maintenanceconfiguration list --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME
```


## Show a specific maintenance configuration window in an existing cluster

View a specific maintenance configuration window in your AKS cluster using the [ az aks maintenanceconfiguration show](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-show) command with the

`--name`

parameter:```
az aks maintenanceconfiguration show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name aksManagedAutoUpgradeSchedule
```


The following example output shows the maintenance window for `aksManagedAutoUpgradeSchedule`

:

```
{
"id": "/subscriptions/<subscription>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster/maintenanceConfigurations/aksManagedAutoUpgradeSchedule",
"maintenanceWindow": {
"durationHours": 4,
"notAllowedDates": [
{
"end": "2024-01-05",
"start": "2023-12-23"
}
],
"schedule": {
"absoluteMonthly": {
"dayOfMonth": 1,
"intervalMonths": 3
},
"daily": null,
"relativeMonthly": null,
"weekly": null
},
"startDate": "2023-01-20",
"startTime": "09:00",
"utcOffset": "-08:00"
},
"name": "aksManagedAutoUpgradeSchedule",
"notAllowedTime": null,
"resourceGroup": "myResourceGroup",
"systemData": null,
"timeInWeek": null,
"type": null
}
```


## Delete a maintenance configuration window in an existing cluster

Delete a maintenance configuration window in your AKS cluster using the [ az aks maintenanceconfiguration delete](/en-us/cli/azure/aks/maintenanceconfiguration#az-aks-maintenanceconfiguration-delete) command.

The following example deletes the `autoUpgradeSchedule`

maintenance configuration:

```
az aks maintenanceconfiguration delete --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name autoUpgradeSchedule
```


## Frequently asked questions (FAQ)

### How can I check the existing maintenance configurations in my cluster?

Use the `az aks maintenanceconfiguration show`

command.

### Can reactive, unplanned maintenance happen during the `notAllowedDates`

periods too?

Yes. AKS reserves the right to break these windows for unplanned, reactive maintenance operations that are urgent or critical.

### How can I tell if a maintenance event occurred?

For releases, check your cluster's region and look up information in [weekly releases](release-tracker) to see if it matches your maintenance schedule. To view the status of your automatic upgrades, look up [activity logs](monitor-aks-reference) on your cluster. You can also look up specific upgrade-related events, as mentioned in [Upgrade an AKS cluster](upgrade-cluster).

AKS also emits upgrade-related Azure Event Grid events. To learn more, see [AKS as an Event Grid source](quickstart-event-grid).

### Can I use more than one maintenance configuration at the same time?

Yes, you can run all three configurations simultaneously: `default`

, `aksManagedAutoUpgradeSchedule`

, and `aksManagedNodeOSUpgradeSchedule`

. If the windows overlap, AKS decides the running order.

### I configured a maintenance window, but the upgrade didn't happen. Why?

AKS auto-upgrade needs a certain amount of time, usually not more than 15 minutes, to take the maintenance window into consideration. We recommend at least 15 minutes between the creation or update of a maintenance configuration and the scheduled start time.

Also, ensure that your cluster is started when the planned maintenance window starts. If the cluster is stopped, its control plane is deallocated and no operations can be performed.

### Why was one of my agent pools upgraded outside the maintenance window?

If an agent pool isn't upgraded (for example, because pod disruption budgets prevented it), it might be upgraded later, outside the maintenance window. This scenario is referred to as a *catch-up upgrade*. It avoids letting agent pools be upgraded with a different version from the AKS control plane.

Another reason why an agent pool could be upgraded unexpectedly is when there's no defined maintenance configuration or if it was deleted. In that case, a cluster with auto-upgrade *but without a maintenance configuration* is upgraded at random times (*fallback schedule*), which might be an undesired timeframe.

### Are there any best practices for the maintenance configurations?

We recommend setting the [node OS security updates](auto-upgrade-node-image) schedule to a weekly cadence if you're using the `NodeImage`

channel, because a new node image is shipped every week. You can also opt in for the `SecurityPatch`

channel to receive daily security updates.

You can set the [auto-upgrade](auto-upgrade-cluster) schedule to a monthly cadence to stay current with the Kubernetes N-2 [support policy](support-policies).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

### Can I configure all my clusters in a single subscription to use the same maintenance configuration?

We don't recommend using the same maintenance configuration for multiple clusters in a single subscription, as doing so can lead to ARM throttling errors causing cluster upgrades to fail. Instead, we recommend staggering the maintenance windows for each cluster to avoid these errors.

### Why did my node pools get upgraded twice during the same maintenance window?

If a newer version of the node image becomes available during the maintenance window, AKS performs a second upgrade to ensure that your node pools are running the latest version. This behavior is normal and doesn't indicate an issue.

## Related content

To get started with upgrading your AKS cluster, see [Upgrade options for AKS clusters](upgrade-cluster).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/coredns-troubleshoot -->

# Troubleshoot issues with CoreDNS on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides troubleshooting guidance for various CoreDNS issues on Azure Kubernetes Service (AKS).

## Debug DNS resolution issues

For general CoreDNS troubleshooting steps, such as checking the endpoints or resolution, see [Debugging DNS resolution](https://kubernetes.io/docs/tasks/administer-cluster/dns-debugging-resolution/).

## Troubleshoot CoreDNS pod traffic imbalance

You might see one or two CoreDNS pods showing significantly higher CPU usage and handling more DNS queries than others, even with multiple CoreDNS pods running in your AKS cluster. This is a [known issue](https://github.com/kubernetes/kubernetes/issues/76517#issuecomment-490731578) in Kubernetes and can lead to one of the CoreDNS pods being overloaded and crashing.

This uneven distribution of DNS queries is primarily caused by User Datagram Protocol (UDP) load balancing limitations in Kubernetes. The platform uses a five-tuple hash (source IP, source port, destination IP, destination port, protocol) to distribute UDP traffic, so if an application reuses the same source port for DNS queries, all queries from that client are routed to the same CoreDNS pod. This distribution method can result in a single pod handling a disproportionate amount of traffic. Additionally, some applications use connection pooling and reuse DNS connections. This behavior can further concentrate DNS queries on a single CoreDNS pod, increasing the imbalance and the risk of overloading and potential crashes.

The following sections help you troubleshoot and mitigate this issue.

### Enable DNS query logging

Enable DNS query logging to capture required DNS query logs from CoreDNS pods.

Add the following configuration to your

`coredns-custom`

ConfigMap:`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom namespace: kube-system data: log.override: | # You can select any name here, but it must end with the .override file extension log`

Apply the ConfigMap changes using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`

View the CoreDNS debug logging using the

`kubectl logs`

command.`kubectl logs --namespace kube-system -l k8s-app=kube-dns`


### Check your CoreDNS pod traffic distribution

Get the names of all CoreDNS pods in your cluster using the

command.`kubectl get pods`

`kubectl get pods --namespace kube-system -l k8s-app=kube-dns`

Review the logs for each CoreDNS pod to analyze DNS query patterns using the

command. Repeat this command for all CoreDNS pods, replacing`kubectl logs`

`<coredns-pod-x>`

with the actual pod names.`kubectl logs --namespace kube-system <coredns-pod-x>`

In the outputs, look for repeated client IP addresses and ports that appear only in the logs of a single CoreDNS pod. This indicates that DNS queries from certain clients aren't being distributed evenly.

Example log output:

`[INFO] 10.244.0.247:5556 - 42621 "A IN myservice.default.svc.cluster.local. udp 28" NOERROR qr,aa,rd 106 0.000141s`

In this example log entry:

`10.244.0.247`

is the client IP address making the DNS query.`5556`

is the client source port.`42621`

is the query ID.

**If you see the same client IP and port repeatedly in only one pod's logs, this confirms a traffic imbalance**.

### Mitigate CoreDNS pod traffic imbalance

If you notice an imbalance, your application could be reusing UDP source ports or pooling their connections. Based on the root cause, you can take the following mitigation actions:

**Caused by UDP source port reuse**: UDP source port reuse occurs when a client application sends multiple DNS queries from the same UDP source port. If this is the issue, update your applications or DNS clients to randomize source ports for each DNS query, which helps distribute requests more evenly across pods.**Caused by connection pooling**: Connection pools are mechanisms applications use to reuse existing network connections instead of creating a new connection for each request. While this improves efficiency, it can result in all DNS queries from an application being sent over the same connection, and thus routed to the same CoreDNS pod. To mitigate this, adjust your application's DNS connection handling by reducing connection Time to Live (TTL) or randomizing connection creation, ensuring queries aren't concentrated on a single CoreDNS pod.

These changes can help achieve a more balanced DNS query distribution and reduce the risk of overloading individual pods.

## Troubleshoot invalid search domain completions for internal.cloudapp.net and reddog.microsoft.com

Azure DNS configures a default search domain of `<VNET_ID>.<REGION>.internal.cloudapp.net`

in virtual networks (VNets) using Azure DNS and a nonfunctional stub `reddog.microsoft.com`

in VNets using custom DNS servers. For more information, see the [Name resolution for resources documentation](/en-us/azure/virtual-network/virtual-networks-name-resolution-for-vms-and-role-instances).

Kubernetes configures pod DNS settings with `ndots: 5`

to properly support cluster service hostname resolution. These two configurations combine to result in invalid search domain completion queries that never succeed being sent to upstream name servers while the system processes through the domain search list. These invalid queries cause name resolution delays and can place extra load on upstream DNS servers.

As of the *v20241025* AKS release, AKS configures CoreDNS to respond with `NXDOMAIN`

in the following cases in order to prevent these invalid search domain completion queries from being forwarded to upstream DNS:

- Any query for the root domain or a subdomain of
`reddog.microsoft.com`

. - Any query for a subdomain of
`internal.cloudapp.net`

that has seven or more labels in the domain name.- This configuration allows virtual machine (VM) resolution by hostname to still succeed. For example, CoreDNS sends
`aks12345.myvnetid.myregion.internal.cloudapp.net`

(*six*labels) to Azure DNS, but rejects`mcr.microsoft.com.myvnetid.myregion.internal.cloudapp.net`

(*eight*labels).

- This configuration allows virtual machine (VM) resolution by hostname to still succeed. For example, CoreDNS sends

This block is implemented in the default server block in the CoreFile for the cluster. If needed, you can disable this rejection configuration by creating custom server blocks for the appropriate domain with a forward plugin enabled:

Create a file named

`corednsms.yaml`

and paste in the following example configuration. Make sure to update the IP addresses and hostnames with your own values.`apiVersion: v1 kind: ConfigMap metadata: name: coredns-custom # This is the name of the ConfigMap you can overwrite with your changes namespace: kube-system data: override-block.server: | internal.cloudapp.net:53 { errors cache 30 forward . /etc/resolv.conf } reddog.microsoft.com:53 { errors cache 30 forward . /etc/resolv.conf }`

Create the ConfigMap using the

command.`kubectl apply configmap`

`kubectl apply -f corednsms.yaml`

Perform a rolling restart to reload the ConfigMap and enable the Kubernetes Scheduler to restart CoreDNS without downtime using the

command.`kubectl rollout restart`

`kubectl --namespace kube-system rollout restart deployment coredns`


## Troubleshoot CoreDNS autoscaling issues

To troubleshoot CoreDNS autoscaling issues, see [Autoscaling CoreDNS in Azure Kubernetes Service (AKS)](coredns-autoscale).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-policy -->

# Secure your Azure Kubernetes Service (AKS) clusters with Azure Policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can apply and enforce built-in security policies on your Azure Kubernetes Service (AKS) clusters using [Azure Policy](/en-us/azure/governance/policy/overview). Azure Policy helps enforce organizational standards and assess compliance at-scale. After you install the [Azure Policy add-on for AKS](/en-us/azure/governance/policy/concepts/policy-for-kubernetes), you can apply individual policy definitions or groups of policy definitions called initiatives (sometimes called policysets) to your cluster. See [Azure Policy built-in definitions for AKS](policy-reference) for a complete list of AKS policy and initiative definitions.

This article shows you how to apply policy definitions to your cluster and verify those assignments are being enforced.

## Prerequisites

- This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[Azure portal](learn/quick-kubernetes-deploy-portal). - You need the
[Azure Policy add-on for AKS installed on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks).

## Assign a built-in policy definition or initiative

You can apply a policy definition or initiative in the Azure portal using the following steps:

- Navigate to the Azure Policy service in Azure portal called
**Policy**. - In the left pane of the Azure Policy page, select
**Definitions**. - Under
**Categories**, select`Kubernetes`

. - Choose the policy definition or initiative you want to apply. For this example, select the
**Kubernetes cluster pod security baseline standards for Linux-based workloads**initiative. - Select
**Assign**. - Set the
**Scope**to the resource group of the AKS cluster with the Azure Policy add-on enabled. - Select the
**Parameters**page and update the**Effect**from`audit`

to`deny`

to block new deployments violating the baseline initiative. You can also add extra namespaces to exclude from evaluation. For this example, keep the default values. - Select
**Review + create**>**Create**to submit the policy assignment.

## Create and assign a custom policy definition

Custom policies allow you to define rules for using Azure. For example, you can enforce the following types of rules:

- Security practices
- Cost management
- Organization-specific rules (like naming or locations)

Before creating a custom policy, check the [list of common patterns and samples](/en-us/azure/governance/policy/samples/) to see if your case is already covered.

Custom policy definitions are written in JSON. To learn more about creating a custom policy, see [Azure Policy definition structure](/en-us/azure/governance/policy/concepts/definition-structure) and [Create a custom policy definition](/en-us/azure/governance/policy/tutorials/create-custom-policy-definition).

Note

Azure Policy now utilizes a new property known as *templateInfo* that allows you to define the source type for the constraint template. When you define *templateInfo* in policy definitions, you don’t have to define *constraintTemplate* or *constraint* properties. You still need to define *apiGroups* and *kinds*. For more information on this, see [Understanding Azure Policy effects](/en-us/azure/governance/policy/concepts/effects#audit-properties).

Once you create your custom policy definition, see [Assign a policy definition](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#assign-a-policy-definition) for a step-by-step walkthrough of assigning the policy to your Kubernetes cluster.

## Validate an Azure Policy is running

Confirm the policy assignments are applied to your cluster using the following

`kubectl get`

command.`kubectl get constrainttemplates`

Note

Policy assignments can take

[up to 20 minutes to sync](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#assign-a-policy-definition)into each cluster.Your output should be similar to the following example output:

`NAME AGE k8sazureallowedcapabilities 23m k8sazureallowedusersgroups 23m k8sazureblockhostnamespace 23m k8sazurecontainerallowedimages 23m k8sazurecontainerallowedports 23m k8sazurecontainerlimits 23m k8sazurecontainernoprivilege 23m k8sazurecontainernoprivilegeescalation 23m k8sazureenforceapparmor 23m k8sazurehostfilesystem 23m k8sazurehostnetworkingports 23m k8sazurereadonlyrootfilesystem 23m k8sazureserviceallowedports 23m`


### Validate rejection of a privileged pod

Let's first test what happens when you schedule a pod with the security context of `privileged: true`

. This security context escalates the pod's privileges. The initiative disallows privileged pods, so the request is denied, which results in the deployment being rejected.

Create a file named

`nginx-privileged.yaml`

and paste in the following YAML manifest.`apiVersion: v1 kind: Pod metadata: name: nginx-privileged spec: containers: - name: nginx-privileged image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine securityContext: privileged: true`

Create the pod using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f nginx-privileged.yaml`

As expected, the pod fails to be scheduled, as shown in the following example output:

`Error from server ([denied by azurepolicy-container-no-privilege-00edd87bf80f443fa51d10910255adbc4013d590bec3d290b4f48725d4dfbdf9] Privileged container is not allowed: nginx-privileged, securityContext: {"privileged": true}): error when creating "privileged.yaml": admission webhook "validation.gatekeeper.sh" denied the request: [denied by azurepolicy-container-no-privilege-00edd87bf80f443fa51d10910255adbc4013d590bec3d290b4f48725d4dfbdf9] Privileged container is not allowed: nginx-privileged, securityContext: {"privileged": true}`

The pod doesn't reach the scheduling stage, so there are no resources to delete before you move on.


### Test creation of an unprivileged pod

In the previous example, the container image automatically tried to use root to bind NGINX to port 80. The policy initiative denies this request, so the pod fails to start. Now, let's try running that same NGINX pod without privileged access.

Create a file named

`nginx-unprivileged.yaml`

and paste in the following YAML manifest.`apiVersion: v1 kind: Pod metadata: name: nginx-unprivileged spec: containers: - name: nginx-unprivileged image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine`

Create the pod using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f nginx-unprivileged.yaml`

Check the status of the pod using the

command.`kubectl get pods`

`kubectl get pods`

Your output should be similar to the following example output, which shows the pod is successfully scheduled and has a status of

*Running*:`NAME READY STATUS RESTARTS AGE nginx-unprivileged 1/1 Running 0 18s`

This example shows the baseline initiative affecting only the deployments that violate policies in the collection. Allowed deployments continue to function.

Delete the NGINX unprivileged pod using the

command and specify the name of your YAML manifest.`kubectl delete`

`kubectl delete -f nginx-unprivileged.yaml`


## Disable a policy or initiative

You can remove the baseline initiative in the Azure portal using the following steps:

- Navigate to the
**Policy**pane on the Azure portal. - Select
**Assignments**. - Select the
**...**button next to the**Kubernetes cluster pod security baseline standards for Linux-based workload**initiative. - Select
**Delete assignment**.

## Next steps

For more information about how Azure Policy works, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-aks-scheduler -->

# Configure advanced scheduler profiles on Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy example scheduler profiles in Azure Kubernetes Service (AKS) to configure advanced scheduling behavior using in-tree scheduling plugins. This guide also explains how to verify the successful application of custom scheduler profiles targeting specific node pools or the entire AKS cluster.

## Limitations

- AKS currently doesn't manage the deployment of third-party schedulers or out-of-tree scheduling plugins.
- AKS doesn't support in-tree scheduling plugins targeting the
`aks-system`

scheduler. This restriction is in place to help prevent unexpected changes to AKS add-ons enabled on your cluster. Additionally, you can't define a`profile`

called`aks-system`

.

## Prerequisites

- The Azure CLI version
`2.76.0`

or later. Run`az --version`

to find the version, and run`az upgrade`

to upgrade the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - Kubernetes version
`1.33`

or later running on your AKS cluster. - The
version`aks-preview`

Azure CLI extension`18.0.0b27`

or later. [Register the](#register-the-user-defined-scheduler-configuration-preview-feature-flag)in your Azure subscription.`UserDefinedSchedulerConfigurationPreview`

feature flag- Review the
[supported advanced scheduling concepts](concepts-scheduler-configuration)and in-tree scheduling plugins on AKS.

### Install the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the

`aks-preview`

extension using thecommand.`az extension update`

`az extension update --name aks-preview`


### Register the User Defined Scheduler Configuration Preview feature flag

Register the

`UserDefinedSchedulerConfigurationPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "UserDefinedSchedulerConfigurationPreview"`

It takes a few minutes for the status to show

*Registered*.When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`


## Enable scheduler profile configuration on an AKS cluster

You can enable schedule profile configuration on a new or existing AKS cluster.

Create an AKS cluster with scheduler profile configuration enabled using the

command with the`az aks create`

`--enable-upstream-kubescheduler-user-configuration`

flag.`# Set environment variables export RESOURCE_GROUP=<resource-group-name> export CLUSTER_NAME=<aks-cluster-name> # Create an AKS cluster with schedule profile configuration enabled az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-upstream-kubescheduler-user-configuration \ --generate-ssh-keys`

Once the creation process completes, connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Verify installation of the scheduler controller

After enabling the feature on your AKS cluster, verify the custom resource definition (CRD) of the scheduler controller was successfully installed using the

`kubectl get`

command.`kubectl get crd schedulerconfigurations.aks.azure.com`

Note

This command won't succeed if the feature wasn't successfully enabled in the

[previous section](#enable-scheduler-profile-configuration-on-an-aks-cluster).

## Configure node bin-packing

Node bin-packing is a scheduling strategy that maximizes resource utilization by increasing pod density on nodes, within the set configuration. This strategy helps improve cluster efficiency by minimizing wasted resources and lowering the operational cost of maintaining idle or underutilized nodes.

In this example, the configured scheduler prioritizes scheduling pods on nodes with high CPU usage. Explicitly, this configuration avoids underutilizing nodes that still have free resources and helps to make better use of the resources already allocated to nodes. The CRD must be named `upstream`

.

Create a file named

`bin-pack-cpu-scheduler.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration profiles: - schedulerName: node-binpacking-cpu-scheduler pluginConfig: - name: NodeResourcesFit args: scoringStrategy: type: MostAllocated resources: - name: cpu weight: 1`

`NodeResourcesFit`

ensures that the scheduler checks if a node has enough resources to run the pod.`scoringStrategy: MostAllocated`

tells the scheduler to prefer nodes with high CPU resource usage. This helps achieve**better resource utilization**by placing new pods on nodes that are already "highly used".`Resources`

specifies that`CPU`

is the primary resource being considered for scoring, and with a weight of`1`

, CPU usage is prioritized with a relatively equal level of importance in the scheduling decision.

Apply the scheduling configuration manifest using the

`kubectl apply`

command.`kubectl apply -f bin-pack-cpu-scheduler.yaml`

To target this scheduling mechanism for specific workloads, update your pod deployments with the following

`schedulerName`

:`... ... spec: schedulerName: node-binpacking-cpu-scheduler ... ...`


## Configure pod topology spread

Pod topology spread is a scheduling strategy that seeks to distribute pods evenly across failure domains (such as availability zones or regions) to ensure high availability and fault tolerance in the event of zone or node failures. This strategy helps prevent the risk of all replicas of a pod being placed in the same failure domain. For more configuration guidance, see the [Kubernetes Pod Topology Spread Constraints documentation](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/). The CRD must be named `upstream`

.

Create a file named

`pod-topology-spreader-scheduler.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration profiles: - schedulerName: pod-distribution-scheduler pluginConfig: - name: PodTopologySpread args: apiVersion: kubescheduler.config.k8s.io/v1 kind: PodTopologySpreadArgs defaultingType: List defaultConstraints: - maxSkew: 1 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: ScheduleAnyway`

`PodTopologySpread`

plugin instructs the scheduler to try and distribute pods as evenly as possible across availability zones.`whenUnsatisfiable: ScheduleAnyway`

specifies schedule to schedule pods despite the inability to meet the topology constraints. This avoids pod scheduling failures when exact distribution isn't feasible.`List`

type applies the default constraints as a list of rules. The scheduler uses the rules in the order they're defined, and they apply to all pods that don’t specify custom topology spread constraints.`maxSkew: 1`

means the number of pods can differ by at most*1*between any two availability zones.`topologyKey: topology.kubernetes.io/zone`

indicates that the scheduler should spread pods across availability zones.

Apply the scheduling configuration manifest using the

`kubectl apply`

command.`kubectl apply -f pod-topology-spreader-scheduler.yaml`

To target this scheduling mechanism for specific workloads, update your pod deployments with the following

`schedulerName`

:`... ... spec: schedulerName: pod-distribution-scheduler ... ...`


## Assign a scheduler profile to an entire AKS cluster

In your scheduler profile configuration, update the

`schedulerName`

field as follows:`... ... - schedulerName: default_scheduler ... ...`

Reapply the manifest using the

`kubectl apply`

command.`kubectl apply -f aks-scheduler-customization.yaml`

Now, this configuration will become the

**default**scheduling operation for your entire AKS cluster.

## Configure multiple scheduler profiles

You can customize the upstream scheduler with multiple profiles and customize each profile with multiple plugins while using the same configuration file. As a reminder, the CRD must be named `upstream`

and user-configured fields include `percentageOfNodesToScore`

, `podInitialBackoffSeconds`

, `podMaxBackoffSeconds`

, and `profiles`

.

In the following example, we create two scheduling profiles called **scheduler-one** and **scheduler-two**. The fields `percentageOfNodesToScore`

, `podInitialBackoffSeconds`

, `podMaxBackoffSeconds`

, apply globally to all profiles defined.

**global parameters**

`percentageOfNodesToScore`

specifies the percentage of cluster nodes the scheduler evaluates during scoring to balance scheduling accuracy and speed. So**percentageOfNodesToScore: 40**means the scheduler will sample 40% of nodes instead of the entire cluster.`podInitialBackoffSeconds`

defines the initial delay before retrying a failed scheduling attempt to prevent rapid, repeated retries. So**podInitialBackoffSeconds: 1**means the scheduler waits 1 second before the first retry.`podMaxBackoffSeconds`

sets the maximum delay the scheduler will wait between exponential backoff retries for unschedulable pods. So**podMaxBackoffSeconds: 8**means the retry delay will never exceed 8 seconds even as backoff increases.

**scheduler-one** prioritizes placing pods across zones and nodes for balanced distribution with the following settings:

- Enforces strict zonal distribution and
*preferred*node distribution using`PodTopologySpread`

. - Honors hard pod affinity rules and considers the soft affinity rules with
`InterPodAffinity`

. *Prefers*nodes in specific zones to reduce cross-zone networking using`NodeAffinity`

.

**scheduler-two** prioritizes placing pods on nodes with available storage, CPU, and memory resources for timely resource-efficient resource usage with the following settings:

- Ensures pods are placed on nodes where PVCs can bind to PVs using
`VolumeBinding`

. - Validates that nodes and volumes satisfy zonal requirements using
`VolumeZone`

to avoid cross-zone storage access. - Prioritizes nodes based on CPU, memory, and ephemeral storage utilization, with
`NodeResourcesFit`

. - Favors nodes that already have the required container images using
`ImageLocality`

.

Note

You might need to adjust zones and other parameters based on your workload type.

Create a file named

`aks-scheduler-customization.yaml`

, with the CRD named`upstream`

, and paste in the following manifest:`apiVersion: aks.azure.com/v1alpha1 kind: SchedulerConfiguration metadata: name: upstream spec: rawConfig: | apiVersion: kubescheduler.config.k8s.io/v1 kind: KubeSchedulerConfiguration percentageOfNodesToScore: 40 podInitialBackoffSeconds: 1 podMaxBackoffSeconds: 8 profiles: - schedulerName: scheduler-one plugins: multiPoint: enabled: - name: PodTopologySpread - name: InterPodAffinity - name: NodeAffinity pluginConfig: # PodTopologySpread with strict zonal distribution - name: PodTopologySpread args: defaultingType: List defaultConstraints: - maxSkew: 2 topologyKey: topology.kubernetes.io/zone whenUnsatisfiable: DoNotSchedule - maxSkew: 1 topologyKey: kubernetes.io/hostname whenUnsatisfiable: ScheduleAnyway - name: InterPodAffinity args: hardPodAffinityWeight: 1 ignorePreferredTermsOfExistingPods: false - name: NodeAffinity args: addedAffinity: preferredDuringSchedulingIgnoredDuringExecution: - weight: 100 preference: matchExpressions: - key: topology.kubernetes.io/zone operator: In values: [westus3-1, westus3-2, westus3-3] - schedulerName: scheduler-two plugins: multiPoint: enabled: - name: VolumeBinding - name: VolumeZone - name: NodeAffinity - name: NodeResourcesFit - name: PodTopologySpread - name: ImageLocality pluginConfig: - name: PodTopologySpread args: defaultingType: List defaultConstraints: - maxSkew: 1 topologyKey: kubernetes.io/hostname whenUnsatisfiable: DoNotSchedule - name: VolumeBinding args: apiVersion: kubescheduler.config.k8s.io/v1 kind: VolumeBindingArgs bindTimeoutSeconds: 300 - name: NodeAffinity args: apiVersion: kubescheduler.config.k8s.io/v1 kind: NodeAffinityArgs addedAffinity: preferredDuringSchedulingIgnoredDuringExecution: - weight: 100 preference: matchExpressions: - key: topology.kubernetes.io/zone operator: In values: [westus3-1, westus3-2] - name: NodeResourcesFit args: apiVersion: kubescheduler.config.k8s.io/v1 kind: NodeResourcesFitArgs scoringStrategy: type: MostAllocated resources: - name: cpu weight: 3 - name: memory weight: 1 - name: ephemeral-storage weight: 2`

Apply the manifest using the

`kubectl apply`

command.`kubectl apply -f aks-scheduler-customization.yaml`


## Disable an AKS scheduler profile configuration

To disable the AKS scheduler profile configuration and revert to AKS scheduler default configuration on the cluster, first delete the

`schedulerconfiguration`

resource using the`kubectl delete`

command.`kubectl delete schedulerconfiguration upstream || true`

Note

Ensure that the previous step is complete and confirm that the

`schedulerconfiguration`

resource was deleted before proceeding to disable this feature.Disable the feature using the

command with the`az aks update`

`--disable-upstream-kubescheduler-user-configuration`

flag.`az aks update --subscription="${SUBSCRIPTION_ID}" \ --resource-group="${RESOURCE_GROUP}" \ --name="${CLUSTER_NAME}" \ --disable-upstream-kubescheduler-user-configuration`

Verify the feature is disabled using the

command.`az aks show`

`az aks show --resource-group="${RESOURCE_GROUP}" \ --name="${CLUSTER_NAME}" \ --query='properties.schedulerProfile'`

Your output should indicate that the feature is no longer enabled on your AKS cluster.


## Frequently asked questions (FAQ)

### What happens if I apply misconfigured scheduler profile to my AKS cluster?

Once you apply a scheduler profile, AKS checks if it contains a valid configuration of plugins and arguments. If the configuration targets a disallowed scheduler or sets the in-tree scheduling plugins improperly, AKS rejects the configuration and reverts to the last known "accepted" scheduler configuration. This check aims to limit impact on new and existing AKS clusters due to scheduler misconfiguration.

### How can I monitor and validate that the scheduler honored my configuration?

There are *three* recommended methods for observing the results of your applied scheduler profile:

- View the AKS
`kube-scheduler`

control plane logs to ensure that the scheduler received the configuration from the CRD. - Run the
`kubectl get schedulerconfiguration`

command. The output displays the status of the`configuration: pending`

during the rollout and`Succeeded`

or`Failed`

after the configuration is accepted or rejected by the scheduler. - Run the
`kubectl describe schedulerconfiguration`

command. The output displays a more detailed state of the scheduler, including any error during the reconciliation, and the current scheduler configuration in effect.

## Next steps

To learn more about the AKS scheduler and best practices, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-container-image-management -->

# Best practices for container image management and security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Container and container image security is a major priority when developing and running applications in Azure Kubernetes Service (AKS). Containers with outdated base images or unpatched application runtimes introduce security risks and possible attack vectors. You can minimize these risks by integrating and running scan and remediation tools in your containers at build and runtime. The earlier you catch the vulnerability or outdated base image, the more secure your application is.

In this article, *"containers"* refers to both the container images stored in a container registry and running containers.

This article focuses on how to secure your containers in AKS. You learn how to:

- Scan for and remediate image vulnerabilities.
- Automatically trigger and redeploy container images when a base image is updated.

- You can read the best practices for
[cluster security](operator-best-practices-cluster-security)and[pod security](developer-best-practices-pod-security). - You can use
[Container security in Defender for Cloud](/en-us/azure/security-center/container-security)to help scan your containers for vulnerabilities.[Azure Container Registry integration](/en-us/azure/security-center/defender-for-container-registries-introduction)with Defender for Cloud helps protect your images and registry from vulnerabilities.

## Secure the images and runtime


Best practice guidance

- Scan your container images for vulnerabilities.
- Only deploy validated images.
- Regularly update the base images and application runtime.
- Redeploy workloads in the AKS cluster.

When adopting container-based workloads, you want to verify the security of images and runtime used to build your own applications. To help avoid introducing security vulnerabilities into your deployments, you can use the following best practices:

- Include in your deployment workflow a process to scan container images using tools, such as
[Twistlock](https://www.twistlock.com/)or[Aqua](https://www.aquasec.com/). - Only allow verified images to be deployed.

For example, you can use a continuous integration and continuous deployment (CI/CD) pipeline to automate the image scans, verification, and deployments. Azure Container Registry includes these vulnerabilities scanning capabilities.

## Automatically build new images on base image update


Best practice guidanceAs you use base images for application images, use automation to build new images when the base image is updated. Since updated base images typically include security fixes, update any downstream application container images.


Each time a base image is updated, you should also update any downstream container images. Integrate this build process into validation and deployment pipelines such as [Azure Pipelines](/en-us/azure/devops/pipelines/) or Jenkins. These pipelines ensure your applications continue to run on the updated based images. Once your application container images are validated, you can then update AKS deployments to run the latest secure images.

Azure Container Registry Tasks can also automatically update container images when the base image is updated. With this feature, you build a few base images and keep them updated with bug and security fixes.

For more information about base image updates, see [Automate image builds on base image update with Azure Container Registry Tasks](/en-us/azure/container-registry/container-registry-tutorial-base-image-update).

## Next steps

This article focused on how to secure your containers. To implement some of these areas, see the following article:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/scale-cluster -->

# Manually scale the node count in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If the resource needs of your applications change, your cluster performance may be impacted due to low capacity on CPU, memory, PID space, or disk sizes. To address these changes, you can manually scale your AKS cluster to run a different number of nodes. When you scale in, nodes are carefully [cordoned and drained](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/) to minimize disruption to running applications. When you scale out, AKS waits until nodes are marked **Ready** by the Kubernetes cluster before pods are scheduled on them.

This article describes how to manually increase or decrease the number of nodes in an AKS cluster.

## Before you begin

Review the

[AKS service quotas and limits](quotas-skus-regions#service-quotas-and-limits)to verify your cluster can scale to your desired number of nodes.The name of a node pool may only contain lowercase alphanumeric characters and must begin with a lowercase letter.

- For Linux node pools, the length must be between 1-11 characters.
- For Windows node pools, the length must be between 1-6 characters.


## Scale the cluster nodes

Important

Removing nodes from a node pool using the kubectl command isn't supported. Doing so can create scaling issues with your AKS cluster.

Get the

*name*of your node pool using thecommand. The following example gets the node pool name for the cluster named`az aks show`

*myAKSCluster*in the*myResourceGroup*resource group:`az aks show --resource-group myResourceGroup --name myAKSCluster --query agentPoolProfiles`

The following example output shows that the

*name*is*nodepool1*:`[ { "count": 1, "maxPods": 110, "name": "nodepool1", "osDiskSizeGb": 30, "osType": "Linux", "vmSize": "Standard_DS2_v2" } ]`

Scale the cluster nodes using the

command. The following example scales a cluster named`az aks scale`

*myAKSCluster*to a single node. Provide your own`--nodepool-name`

from the previous command, such as*nodepool1*:`az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 1 --nodepool-name <your node pool name>`

The following example output shows the cluster successfully scaled to one node, as shown in the

*agentPoolProfiles*section:`{ "aadProfile": null, "addonProfiles": null, "agentPoolProfiles": [ { "count": 1, "maxPods": 110, "name": "nodepool1", "osDiskSizeGb": 30, "osType": "Linux", "vmSize": "Standard_DS2_v2", "vnetSubnetId": null } ], [...] }`


## Scale `User`

node pools to 0

Unlike `System`

node pools that always require running nodes, `User`

node pools allow you to scale to 0. To learn more on the differences between system and user node pools, see [System and user node pools](use-system-pools).

Important

You can't scale a user node pool with the cluster autoscaler enabled to 0 nodes. To scale a user node pool to 0 nodes, you must disable the cluster autoscaler first. For more information, see [Disable the cluster autoscaler on a node pool](cluster-autoscaler#disable-the-cluster-autoscaler-on-a-node-pool).

To scale a user pool to 0, you can use the

[az aks nodepool scale](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-scale)in alternative to the above`az aks scale`

command, and set`0`

as your node count.`az aks nodepool scale --name <your node pool name> --cluster-name myAKSCluster --resource-group myResourceGroup --node-count 0`

You can also autoscale

`User`

node pools to zero nodes, by setting the`--min-count`

parameter of the[Cluster Autoscaler](cluster-autoscaler)to`0`

.

## Next steps

In this article, you manually scaled an AKS cluster to increase or decrease the number of nodes. You can also use the [cluster autoscaler](cluster-autoscaler) to automatically scale your cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-storage-drivers -->

# Container Storage Interface (CSI) drivers on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Container Storage Interface (CSI) is a standard for exposing arbitrary block and file storage systems to containerized workloads on Kubernetes. By adopting and using CSI, Azure Kubernetes Service (AKS) can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes without having to touch the core Kubernetes code and wait for its release cycles.

The CSI storage driver support on AKS allows you to natively use:

can be used to create a Kubernetes**Azure Disks***DataDisk*resource. Disks can use Azure Premium Storage, backed by high-performance SSDs, or Azure Standard Storage, backed by regular HDDs or Standard SSDs. For most production and development workloads, use Premium Storage. Azure Disks are mounted as*ReadWriteOnce*and are only available to one node in AKS. For storage volumes that can be accessed by multiple nodes simultaneously, use Azure Files.can be used to mount an SMB 3.0/3.1 share backed by an Azure storage account to pods. With Azure Files, you can share data across multiple nodes and pods. Azure Files can use Azure Standard storage backed by regular HDDs or Azure Premium storage backed by high-performance SSDs.**Azure Files**can be used to mount Blob storage (or object storage) as a file system into a container or pod. Using Blob storage enables your cluster to support applications that work with large unstructured datasets like log file data, images or documents, HPC, and others. Additionally, if you ingest data into**Azure Blob storage**[Azure Data Lake storage](/en-us/azure/storage/blobs/data-lake-storage-introduction), you can directly mount and use it in AKS without configuring another interim filesystem.

Tip

If you want a fully managed solution for block-level access to data, consider using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction) instead of CSI drivers. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes. Azure Container Storage supports Azure Disks, Ephemeral Disks, and Azure Elastic SAN (preview) as backing storage, offering flexibility and scalability for stateful applications running on Kubernetes clusters.

## Prerequisites

- You need the Azure CLI version 2.42 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If the open-source CSI storage driver is installed on your cluster, uninstall it before enabling the Azure storage CSI driver.
- To enforce the Azure Policy for AKS
[policy definition](/en-us/azure/governance/policy/samples/built-in-policies#kubernetes)**Kubernetes clusters should use Container Storage Interface(CSI) driver StorageClass**, the Azure Policy add-on needs to be enabled on new and existing clusters. For an existing cluster, review the[Learn Azure Policy for Kubernetes](/en-us/azure/governance/policy/concepts/policy-for-kubernetes)to enable it.

## Disk encryption supported scenarios

CSI storage drivers support the following scenarios:

[Encrypted managed disks with customer-managed keys](/en-us/azure/virtual-machines/disks-cross-tenant-customer-managed-keys)using Azure Key Vaults stored in a different Microsoft Entra tenant.- Encrypt your Azure Storage disks hosting AKS OS and application data with
[customer-managed keys](azure-disk-customer-managed-keys).

## Enable CSI storage drivers on an existing cluster

To enable CSI storage drivers on a new cluster, include one of the following parameters depending on the storage system:

`--enable-disk-driver`

allows you to enable the[Azure Disks CSI driver](azure-disk-csi).`--enable-file-driver`

allows you to enable the[Azure Files CSI driver](azure-files-csi).`--enable-blob-driver`

allows you to enable the[Azure Blob storage CSI driver](azure-blob-csi).`--enable-snapshot-controller`

allows you to enable the[snapshot controller](https://kubernetes-csi.github.io/docs/snapshot-controller.html).

```
az aks update --name myAKSCluster --resource-group myResourceGroup --enable-disk-driver --enable-file-driver --enable-blob-driver --enable-snapshot-controller
```


It might take several minutes to complete this action. Once it's complete, you should see in the output the status of enabling the driver on your cluster. The following example resembles the section indicating the results when enabling the Blob storage CSI driver:

```
"storageProfile": {
"blobCsiDriver": {
"enabled": true
},
```


## Disable CSI storage drivers on a new or existing cluster

To disable CSI storage drivers on a new cluster, include one of the following parameters depending on the storage system:

`--disable-disk-driver`

allows you to disable the[Azure Disks CSI driver](azure-disk-csi).`--disable-file-driver`

allows you to disable the[Azure Files CSI driver](azure-files-csi).`--disable-blob-driver`

allows you to disable the[Azure Blob storage CSI driver](azure-blob-csi).`--disable-snapshot-controller`

allows you to disable the[snapshot controller](https://kubernetes-csi.github.io/docs/snapshot-controller.html).

```
az aks create \
--name myAKSCluster \
--resource-group myResourceGroup \
--disable-disk-driver \
--disable-file-driver \
--disable-blob-driver \
--disable-snapshot-controller \
--generate-ssh-keys
```


To disable CSI storage drivers on an existing cluster, use one of the parameters listed earlier depending on the storage system:

```
az aks update \
--name myAKSCluster \
--resource-group myResourceGroup \
--disable-disk-driver \
--disable-file-driver \
--disable-blob-driver \
--disable-snapshot-controller
```


Note

We recommend deleting the corresponding PersistentVolumeClaim object instead of the PersistentVolume object when deleting a CSI volume. The external provisioner in the CSI driver will react to the deletion of the PersistentVolumeClaim and based on its reclamation policy, it issues the DeleteVolume call against the CSI volume driver commands to delete the volume. The PersistentVolume object is then deleted.

## Migrate custom in-tree storage classes to CSI

Starting with Kubernetes version 1.26, in-tree persistent volume types *kubernetes.io/azure-disk* and *kubernetes.io/azure-file* are deprecated and will no longer be supported. *In-tree drivers* refers to the storage drivers that are part of the core Kubernetes code opposed to the CSI drivers, which are plug-ins.

Removing these drivers following their deprecation isn't planned, however you should migrate to the corresponding CSI drivers *disk.csi.azure.com* and *file.csi.azure.com*. To review the migration options for your storage classes and upgrade your cluster to use Azure Disks and Azure Files CSI drivers, see [Migrate from in-tree to CSI drivers](csi-migrate-in-tree-volumes).

If you've created in-tree driver storage classes, those storage classes continue to work since CSI migration is turned on after upgrading your cluster to 1.21.x. If you want to use CSI features you'll need to perform the migration.

## Next steps

- To use the CSI driver for Azure Disks, see
[Use Azure Disks with CSI drivers](azure-disk-csi). - To use the CSI driver for Azure Files, see
[Use Azure Files with CSI drivers](azure-files-csi). - To use the CSI driver for Azure Blob storage, see
[Use Azure Blob storage with CSI drivers](azure-blob-csi) - For more about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service](operator-best-practices-storage). - For more information on CSI migration, see
[Kubernetes in-tree to CSI Volume Migration](https://kubernetes.io/blog/2019/12/09/kubernetes-1-17-feature-csi-migration-beta).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/resize-node-pool -->

# Resize node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might want to change the size of your virtual machines (VMs) to accommodate an increasing number of deployments or to run a larger workload. Resizing AKS instances directly isn't supported when using [Virtual Machine Scale Sets](/en-us/azure/virtual-machine-scale-sets/overview) in AKS, as outlined in the [support policies for AKS](support-policies#user-customization-of-agent-nodes):

AKS agent nodes appear in the Azure portal as regular Azure IaaS resources. But these virtual machines are deployed into a custom Azure resource group (usually prefixed with MC_*). You can't make direct customizations to these nodes using the IaaS APIs or resources. Any custom changes that aren't done via the AKS API won't persist through an upgrade, scale, update, or reboot.


In this article, you learn the recommended method to resize a node pool by creating a new node pool with the desired SKU size, cordoning and draining the existing nodes, and then removing the existing node pool.

Important

This method is specific to [Virtual Machine Scale Sets](/en-us/azure/virtual-machine-scale-sets/overview)-based AKS clusters. When using Virtual Machines-based node pools, you can easily update the VM sizes in an existing node pool using a single Azure CLI command and have multiple VM sizes in the same node pool. For more information, see the [Virtual Machines node pools documentation](virtual-machines-node-pools).

## Create a new node pool with the desired SKU

Note

Every AKS cluster must contain at least one system node pool with at least one node. In this example, we use a `--mode`

of `System`

to add a system node pool to replace the system node pool we want to resize. You can [update the mode of a node pool](use-system-pools#update-existing-cluster-system-and-user-node-pools) at any time. You can also add a user node pool by setting `--mode`

to `User`

.

When resizing, make sure you consider all workload requirements, such as availability zones, and configure your VMSS node pool accordingly. You might need to modify the following command to best fit your needs. For a full list of the configuration options, see the [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) reference page.

Create a new node pool using the

command. In this example, we create a new node pool,`az aks nodepool add`

`mynodepool`

, with three nodes and the`Standard_DS3_v2`

VM SKU to replace an existing node pool,`nodepool1`

, that has the`Standard_DS2_v2`

VM SKU.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name mynodepool \ --node-count 3 \ --node-vm-size Standard_DS3_v2 \ --mode System \ --no-wait`

It takes a few minutes for the new node pool to be created.

Get the status of the new node pool using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should resemble the following example output, showing both the new node pool

`mynodepool`

and the existing node pool`nodepool1`

:`NAME STATUS ROLES AGE VERSION aks-mynodepool-98765432-vmss000000 Ready agent 23m v1.21.9 aks-mynodepool-98765432-vmss000001 Ready agent 23m v1.21.9 aks-mynodepool-98765432-vmss000002 Ready agent 23m v1.21.9 aks-nodepool1-12345678-vmss000000 Ready agent 10d v1.21.9 aks-nodepool1-12345678-vmss000001 Ready agent 10d v1.21.9 aks-nodepool1-12345678-vmss000002 Ready agent 10d v1.21.9`


## Cordon the existing nodes

Cordoning marks specified nodes as unschedulable and prevents any more pods from being added to the nodes.

Get the names of the nodes you want to cordon using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should resemble the following example output, showing the nodes in the existing node pool

`nodepool1`

that you want to cordon:`NAME STATUS ROLES AGE VERSION aks-nodepool1-12345678-vmss000000 Ready agent 7d21h v1.21.9 aks-nodepool1-12345678-vmss000001 Ready agent 7d21h v1.21.9 aks-nodepool1-12345678-vmss000002 Ready agent 7d21h v1.21.9`

Cordon the existing nodes using the

`kubectl cordon`

command, specifying the desired nodes in a space-separated list. For example:`kubectl cordon aks-nodepool1-12345678-vmss000000 aks-nodepool1-12345678-vmss000001 aks-nodepool1-12345678-vmss000002`

Your output should resemble the following example output, showing that the nodes are cordoned:

`node/aks-nodepool1-12345678-vmss000000 cordoned node/aks-nodepool1-12345678-vmss000001 cordoned node/aks-nodepool1-12345678-vmss000002 cordoned`


## Drain the existing nodes

Important

To successfully drain nodes and evict running pods, ensure that any PodDisruptionBudgets (PDBs) allow for at least one pod replica to be moved at a time. Otherwise, the drain/evict operation fails. To check this, you can run `kubectl get pdb -A`

and verify `ALLOWED DISRUPTIONS`

is at least `1`

or higher.

When you drain nodes, the pods running on them are evicted and recreated on the other schedulable nodes.

Drain the existing nodes using the

`kubectl drain`

command with the`--ignore-daemonsets`

and`--delete-emptydir-data`

flags, specifying the desired nodes in a space-separated list. For example:Important

Using

`--delete-emptydir-data`

is required to evict the AKS-created`coredns`

and`metrics-server`

pods. If you don't use this flag, you get an error. For more information, see the[documentation on emptydir](https://kubernetes.io/docs/concepts/storage/volumes/#emptydir).`kubectl drain aks-nodepool1-12345678-vmss000000 aks-nodepool1-12345678-vmss000001 aks-nodepool1-12345678-vmss000002 --ignore-daemonsets --delete-emptydir-data`

After the drain operation finishes, all pods (excluding the pods controlled by daemon sets) should be running on the new node pool. You can verify this using the

`kubectl get pods`

command.`kubectl get pods -o wide -A`


### Troubleshoot pod eviction issues

You might encounter the following error when draining nodes:


`Error when evicting pods/[podname] -n [namespace] (will retry after 5s): Cannot evict pod as it would violate the pod's disruption budget.`


By default, your cluster has AKS-managed pod disruption budgets (such as `coredns-pdb`

or `konnectivity-agent`

) with a `MinAvailable`

of `1`

. For example, if there are two `coredns`

pods running, only one can be disrupted at a time. While one of them is getting recreated and is unavailable, the other `coredns`

pod can't be evicted due to the pod disruption budget. This issue resolves itself after the initial `coredns`

pod is scheduled and running, allowing the second pod to be properly evicted and recreated.

Tip

Consider draining nodes one by one for a smoother eviction experience and to avoid throttling. For more information, see:

## Remove the existing node pool

Important

When you delete a node pool, AKS doesn't perform cordon and drain. To minimize the disruption of rescheduling pods currently running on the node pool you plan to delete, perform a cordon and drain on all nodes in the node pool before deleting.

Delete the original node pool using the

command.`az aks nodepool delete`

`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name nodepool1`

Verify that your AKS cluster has only the new node pool with the applications and pods properly running using the

`kubectl get nodes`

command.`kubectl get nodes`

Your output should resemble the following example output, showing only the new node pool

`mynodepool`

:`NAME STATUS ROLES AGE VERSION aks-mynodepool-98765432-vmss000000 Ready agent 63m v1.21.9 aks-mynodepool-98765432-vmss000001 Ready agent 63m v1.21.9 aks-mynodepool-98765432-vmss000002 Ready agent 63m v1.21.9`


## Next steps

After resizing a node pool by cordoning and draining, learn more about [using multiple node pools](create-node-pools).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ray-overview -->

# Deploy a Ray cluster on Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy a Ray cluster on Azure Kubernetes Service (AKS) using the KubeRay operator. You also learn how to use the Ray cluster to train a simple machine learning model and display the results on the Ray Dashboard.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## What is Ray?

[Ray](https://docs.ray.io/en/latest/index.html#) is an open-source project developed at UC Berkeley's RISE Lab that provides a unified framework for scaling AI and Python applications. It consists of a core distributed runtime and a set of AI libraries designed to accelerate machine learning workloads.

Ray simplifies the process of running compute-intensive Python tasks at scale, allowing you to seamlessly scale your applications. The framework supports various machine learning tasks, including distributed training, hyperparameter tuning, reinforcement learning, and production model serving.

For more information, see the [Ray GitHub repository](https://github.com/ray-project/ray).

## What is KubeRay?

[KubeRay](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started.html) is an open-source Kubernetes operator for deploying and managing Ray clusters on Kubernetes. KubeRay automates the deployment, scaling, and monitoring of Ray clusters. It provides a declarative way to define Ray clusters using Kubernetes custom resources, making it easy to manage Ray clusters alongside other Kubernetes resources.

For more information, see the [KubeRay GitHub repository](https://github.com/ray-project/kuberay).

## Ray deployment process

The deployment process consists of the following steps:

- Use Terraform to create a local plan file to define the desired state for infrastructure required AKS infrastructure that consists of an Azure resource group, a dedicated system node pool, and a workload node pool for Ray with three nodes.
- Deploy a local Terraform plan to Azure.
- Retrieve outputs from the Terraform deployment and obtain Kubernetes credentials to the newly deployed AKS cluster.
- Install the Helm Ray repository and deploy KubeRay to the AKS cluster using Helm.
- Download and execute a
[Ray Job](https://docs.ray.io/en/latest/cluster/running-applications/job-submission/index.html)YAML manifest from the Ray GitHub samples repo to perform an image classification with a[MNIST](https://github.com/cvdfoundation/mnist)dataset using[Convolutional Neural Networks (CNNs)](https://techcommunity.microsoft.com/discussions/machinelearning/what-is-convolutional-neural-network-%E2%80%94-cnn-deep-learning/4184725). - Output the logs from the Ray Job to gain insight into the machine learning process performed by Ray.

## Next step

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Russell de Pina | Principal TPM
- Ken Kilty | Principal TPM
- Erin Schaffer | Content Developer 2
- Adrian Joian | Principal Customer Engineer
- Ryan Graham | Principal Technical Specialist

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-migration -->

# Migrate from Dapr OSS to the Dapr extension for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to migrate from Dapr OSS to the Dapr extension for AKS.

You can configure the Dapr extension to use and manage the Kubernetes resources created by Dapr OSS by either:

[Checking for an existing Dapr installation using the Azure CLI](#check-for-an-existing-dapr-installation)(*default method*), or[Configuring the existing Dapr installation using](#configure-the-existing-dapr-installation-using---configuration-settings).`--configuration-settings`


For more information, see [an overview of the Dapr extension for AKS](dapr-overview).

## Check for an existing Dapr installation

When you [install the Dapr extension](dapr), the extension checks for an existing Dapr installation on your cluster. If Dapr exists, the extension uses and manages the Kubernetes resources created by Dapr OSS.

List the details of your current Dapr installation using the

`helm list -A`

command and save the Dapr release name and namespace from the output.`helm list -A`

Enter the Helm release name and namespace (from

`helm list -A`

) when prompted with the following questions:`Enter the Helm release name for Dapr, or press Enter to use the default name [dapr]: Enter the namespace where Dapr is installed, or press Enter to use the default namespace [dapr-system]:`


## Configure the existing Dapr installation using `--configuration-settings`


When you [create the Dapr extension](dapr), you can configure the extension to use and manage the Kubernetes resources created by Dapr OSS using the `--configuration-settings`

flag.

List the details of your current Dapr installation using the

`helm list -A`

command and save the Dapr release name and namespace from the output.`helm list -A`

Create the Dapr extension using the

and use the`az k8s-extension create`

`--configuration-settings`

flags to set the Dapr release name and namespace.`az k8s-extension create --cluster-type managedClusters \ --cluster-name myAKSCluster \ --resource-group myResourceGroup \ --name dapr \ --extension-type Microsoft.Dapr \ --configuration-settings "existingDaprReleaseName=dapr" \ --configuration-settings "existingDaprReleaseNamespace=dapr-system"`


## Update HA mode or placement service settings

When installing the Dapr extension on top of an existing Dapr installation, you receive the following message:

```
The extension will be installed on your existing Dapr installation. Note, if you have updated the default values for global.ha.* or dapr_placement.* in your existing Dapr installation, you must provide them in the configuration settings. Failing to do so will result in an error, since Helm upgrade will try to modify the StatefulSet. See <link> for more information.
```


Kubernetes only allows patching for limited fields in StatefulSets. If any of the HA mode or placement service settings are configured, the upgrade fails. To update the HA mode or placement service settings, you must delete the stateful set and then update the HA mode.

Delete the stateful set using the

`kubectl delete`

command.`kubectl delete statefulset.apps/dapr-placement-server -n dapr-system`

Update the HA mode using the

command.`az k8s-extension update`

`az k8s-extension update --cluster-type managedClusters \ --cluster-name myAKSCluster \ --resource-group myResourceGroup \ --name dapr \ --extension-type Microsoft.Dapr \ --auto-upgrade-minor-version true \ --configuration-settings "global.ha.enabled=true" \`


For more information, see the [Dapr production guidelines](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-production/#enabling-high-availability-in-an-existing-dapr-deployment).

## Next steps

Learn more about [Dapr](dapr-overview) and [how to use it](dapr).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/supported-kubernetes-versions -->

# Supported Kubernetes versions in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Kubernetes community [releases minor versions](https://kubernetes.io/releases/) roughly every four months.

Minor version releases include new features and improvements. Patch releases are more frequent (sometimes weekly) and are intended for critical bug fixes within a minor version. Patch releases include fixes for security vulnerabilities or major bugs.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Kubernetes versions

Kubernetes uses the standard [Semantic Versioning](https://semver.org/) versioning scheme for each version:

```
[major].[minor].[patch]
Examples:
1.29.2
1.29.1
```


Each number in the version reflects compatibility with previous versions:

**Major versions**: Introduce incompatible API changes or break backward compatibility.**Minor versions**: Add new features while maintaining backward compatibility.**Patch versions**: Include backward-compatible bug fixes.

Always use the latest patch release for your current minor version. For example, if your production cluster is on ** 1.29.1** and

**is the latest available patch version available for the**

`1.29.2`

*1.29*minor version, you should upgrade to

**as soon as possible to ensure your cluster is fully patched and supported.**

`1.29.2`

## AKS Kubernetes release calendar

Check the AKS Kubernetes release calendar for upcoming version releases. To see real-time updates of region release status and version release notes, visit the [AKS release status webpage](https://releases.aks.azure.com/). To learn more about the release status webpage, see [AKS release tracker](release-tracker).

Note

Note

AKS follows a 12-month support policy for generally available (GA) Kubernetes versions. To learn more about our Kubernetes version support policy, see the [FAQ](supported-kubernetes-versions#faq). Unless an explicit date is provided, the End of Life (EOL) date is the last day of the specified month. For example, "Mar 2026" indicates March 31, 2026.

For the past release history, see [Kubernetes history](https://github.com/kubernetes/kubernetes/releases).

| K8s version | Upstream release | AKS preview | AKS GA | End of life | Platform support |
|---|---|---|---|---|---|
| 1.29 | Dec 2023 | Feb 2024 | Mar 2024 | Mar 2025 | Until 1.33 GA |
| 1.30 | Apr 2024 | Jun 2024 | Jul 2024 | Aug 22, 2025 | Until 1.34 GA |
| 1.31 | Aug 2024 | Oct 2024 | Nov 2024 | Nov 1, 2025 | Until 1.35 GA |
| 1.32 | Dec 2024 | Feb 2025 | Apr 2025 | Mar 2026 | Until 1.36 GA |
| 1.33 | Apr 2025 | May 2025 | Jun 2025 | Jun 2026 | Until 1.37 GA |
| 1.34 | Aug 2025 | Oct 2025 | Nov 2025 | Nov 2026 | Until 1.38 GA |
| 1.35 | Dec 2025 | Feb 2026 | Mar 2026 | Mar 2027 | Until 1.39 GA |

### LTS Versions

Long-term support (LTS) needs to be enabled in order to get extended support. You can find more information on [Enable long-term support](/en-us/azure/aks/long-term-support#enable-long-term-support).

Note

Azure Linux 2.0 goes End of Life during the LTS period of AKS v1.28–v1.31. For more information on upgrading to Azure Linux 3.0 on AKS v1.28–v1.31, read the [Azure Linux AKS LTS Releases](/en-us/azure/azure-linux/support-cycle#aks-lts-releases) section.

| K8s version | Upstream release | AKS preview | AKS GA | End of life | LTS End of life |
|---|---|---|---|---|---|
| 1.27 | Apr 2023 | Jun 2023 | Jul 2023 | Jul 2024 | Jul 2025 |
| 1.28 | Aug 2023 | Sep 2023 | Nov 2023 | Jan 2025 | Feb 2026 |
| 1.29 | Dec 2023 | Feb 2024 | Mar 2024 | Mar 2025 | Apr 2026 |
| 1.30 | Apr 2024 | Jun 2024 | Jul 2024 | Aug 22, 2025 | Jul 2026 |
| 1.31 | Aug 2024 | Oct 2024 | Nov 2024 | Nov 1, 2025 | Nov 2026 |
| 1.32 | Dec 2024 | Feb 2025 | Apr 2025 | Mar 2026 | Mar 2027 |
| 1.33 | Apr 2025 | May 2025 | Jun 2025 | Jun 2026 | Jun 2027 |
| 1.34 | Aug 2025 | Oct 2025 | Nov 2025 | Nov 2026 | Nov 2027 |
| 1.35 | Dec 2025 | Feb 2026 | Mar 2026 | Mar 2027 | Mar 2028 |

### AKS Kubernetes release schedule Gantt chart

If you prefer to see this information visually, here's a Gantt chart with all the current releases displayed:

## AKS components breaking changes by version

Note the following important changes before you upgrade to any of the available minor versions:

### Kubernetes 1.34

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes From Kubernetes 1.33.0 |
Notes |
|---|---|---|---|---|
| aci-connector-linux 1.6.2 | addon-override-manager master.251002.2 | Linux - Ubuntu 22.04 |
kube-egress-gateway-daemon v0.0.21 → v0.1.3 | |
| addon-resizer v1.8.23-7 | apiserver-network-proxy-server v0.31.4-3 | azure-acr-credential-provider-pmc 1.34.1-ubuntu22.04u3 | kube-egress-gateway-daemon-init v0.0.21 → v0.1.3 | |
| ai-toolchain-operator 0.6.0 | app-routing-operator 0.2.12 | containerd 1.7.29-ubuntu22.04u1 | kube-egress-gateway-cnimanager v0.0.21 → v0.1.3 | |
| aks-windows-gpu-device-plugin 0.0.19 | automatic-authz-webhook master.251112.4 | datacenter-gpu-manager-4-core 1:4.4.1-1 | kube-egress-gateway-cni v0.0.21 → v0.1.3 | |
| ama-logs-linux 3.1.31 | ccp-webhook master.251105.4 | datacenter-gpu-manager-4-proprietary 1:4.4.1-1 | kube-egress-gateway-cni-ipam v0.0.21 → v0.1.3 | |
| ama-logs-win win-3.1.31 | cluster-autoscaler v1.33.1-aks-3 | kubectl 1.34.1-ubuntu22.04u4 | cloud-provider-node-manager-windows v1.33.3 → v1.34.0 | |
| app-routing-operator 0.0.3 | cost-analysis-scraper v0.0.25 | kubelet 1.34.1-ubuntu22.04u4 | cloud-provider-node-manager-linux v1.33.3 → v1.34.0 | |
| azure-monitor-metrics-cfg-reader 6.24.0-main | customer-net-probe master.250827.1 | kubernetes-cri-tools 1.32.0-ubuntu22.04u3 | metrics-server v0.7.2-10 → v0.8.0-4 | |
| azure-monitor-metrics-ksm v2.17.0 | envoy v1.35.6-master.251017.3 | nvidia-device-plugin 0.18.0-ubuntu22.04u2 | overlay-vpa v1.2.1-1 → v1.5.1-1 | |
| azure-monitor-metrics-linux 6.24.0-main | ingress-dispatcher v1.35.6-master.251017.3 | runc 1.3.3-ubuntu22.04u1 | coredns v1.12.1-7 → v1.13.1-2 | |
| azure-monitor-metrics-target-allocator | jwt-authenticator-egress master.250904.1 | Linux - AzureLinux 3.0 |
kube-egress-gateway-controller v0.0.21 → v0.1.3 | |
| azure-monitor-metrics-windows | kube-state-metrics v2.15.0-4 | azure-acr-credential-provider-pmc 1.34.1-1.azl3 | ||
| azure-npm-image v1.6.34 | kubeguard-guard v0.16.23 | containerd 2.0.0-14.azl3 | ||
| azure-npm-image-windows v1.5.5 | private-connect-balancer master.250731.2 | datacenter-gpu-manager-4-core 1:4.4.1-1 | ||
| azure-policy 1.15.1 | private-connect-router master.251105.2 | datacenter-gpu-manager-4-proprietary 1:4.4.1-1 | ||
| azure-policy-audit 1.15.1 | gpu-provisioner 0.3.7 (plugin) | dcgm-exporter 4.6.0-1.azl3 | ||
| azure-policy-webhook 1.15.1 | karpenter 1.6.5-aks (plugin) | kubectl 1.34.1-4.azl3 | ||
| certgen v0.1.9 | kms-controller master.250811.2 (plugin) | kubelet 1.34.1-4.azl3 | ||
| cilium-agent 1.14.10-1 | kms-operator master.250814.1 (plugin) | kubernetes-cri-tools 1.32.0-3.azl3 | ||
| cilium-envoy v1.31.5-250218 | kms-plugin-v2-plus master.251114.2 (plugin) | nvidia-container-toolkit 1.17.3 | ||
| cilium-operator-generic 1.14.10 | kube-egress-gateway-controller v0.1.3 | nvidia-device-plugin 0.18.0-2.azl3 | ||
| cloud-provider-node-manager-linux v1.34.0 | kubelet-serving-csr-approver v0.0.7 | Windows - Windows2022 |
||
| cloud-provider-node-manager-windows v1.34.0 | live-patching-controller v0.0.16 | containerd v2.0.4-azure.1 | ||
| ... | secure-tls-bootstrap-server v0.0.9 |

### Kubernetes 1.33

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes From Kubernetes 1.33.0 |
Notes |
|---|---|---|---|---|
| * aci-connector-linux 1.6.2 * addon-resizer v1.8.23-2 * ai-toolchain-operator 0.4.5 * aks-windows-gpu-device-plugin 0.0.19 * ama-logs-linux 3.1.26 * ama-logs-win win-3.1.26 * app-routing-operator 0.0.3 * azure-monitor-metrics-cfg-reader 6.16.0-main-04-15-2025-d78050c6-cfg * azure-monitor-metrics-ksm v2.15.0-4 * azure-monitor-metrics-linux 6.16.0-main-04-15-2025-d78050c6 * azure-monitor-metrics-target-allocator 6.16.0-main-04-15-2025-d78050c6-targetallocator * azure-monitor-metrics-windows 6.16.0-main-04-15-2025-d78050c6-win * azure-npm-image v1.5.45 * azure-npm-image-windows v1.5.5 * azure-policy 1.10.1 * azure-policy-webhook 1.10.0 * certgen v0.1.9 * cilium-agent 1.14.10-1 * cilium-envoy v1.31.5-250218 * cilium-operator-generic 1.14.10 * cloud-provider-node-manager-linux v1.33.0 * cloud-provider-node-manager-windows v1.33.0 * cluster-proportional-autoscaler v1.9.0-1 * container-networking-cilium-agent v1.16.6-250129 * container-networking-cilium-operator-generic v1.16.6-250129 * coredns v1.12.1-1 * cost-analysis-agent v0.0.23 * cost-analysis-opencost v1.111.0 * cost-analysis-prometheus v2.54.1 * cost-analysis-victoria-metrics v1.103.0 * extension-config-agent 1.23.3 * extension-manager 1.23.3 * fqdn-policy v1.16.6-250129 * gpu-provisioner 0.3.3 * health-probe-proxy v1.29.1 * hubble-relay v1.15.0 * image-cleaner v1.3.1 * ingress-appgw 1.8.1 * ip-masq-agent-v2 v0.1.15-2 * ipv6-hp-bpf v0.0.1 * keda v2.16.1 * keda-admission-webhooks v2.16.1 * keda-metrics-apiserver v2.16.1 * kube-egress-gateway-cni v0.0.20 * kube-egress-gateway-cni-ipam v0.0.20 * kube-egress-gateway-cnimanager v0.0.20 * kube-egress-gateway-daemon v0.0.20 * kube-egress-gateway-daemon-init v0.0.20 * metrics-server v0.7.2-6 * microsoft-defender-admission-controller 20250325.2 * microsoft-defender-low-level-collector 2.0.205 * microsoft-defender-low-level-init 1.3.81 * microsoft-defender-old-file-cleaner 1.0.214 * microsoft-defender-pod-collector 1.0.177 * microsoft-defender-security-publisher 1.0.211 * open-policy-agent-gatekeeper v3.18.2-1 * osm-bootstrap v1.2.9 * osm-controller v1.2.9 * osm-crds v1.2.9 * osm-healthcheck v1.2.9 * osm-init v1.2.9 * osm-injector v1.2.9 * osm-sidecar v1.32.2-hotfix.20241216 * overlay-vpa 1.2.1 * overlay-vpa-webhook-generation master.250430.1 * ratify-base v1.2.3 * retina-agent v0.0.31 * retina-agent-enterprise v0.1.9 * retina-agent-win v0.0.31 * retina-operator v0.1.9 * secrets-store-csi-driver v1.4.8 * secrets-store-csi-driver-windows v1.4.8 * secrets-store-driver-registrar-linux v2.11.1 * secrets-store-driver-registrar-windows v2.11.1 * secrets-store-livenessprobe-linux v2.13.1 * secrets-store-livenessprobe-windows v2.13.1 * secrets-store-provider-azure v1.6.2 * secrets-store-provider-azure-windows v1.6.2 * sgx-attestation 3.3.1 * sgx-plugin 1.0.0 * sgx-webhook 1.2.2 * tigera-operator v1.36.7 * windows-gmsa-webhook-image v0.12.1-2 * workload-identity-webhook v1.5.0 |
* addon-override-manager master.250116.1 * apiserver-network-proxy-server v0.30.3-hotfix.20240819 * app-routing-operator 0.2.5 * ccp-webhook master.250509.3 * cluster-autoscaler v1.32.1-aks * cost-analysis-scraper v0.0.23 * customer-net-probe master.250430.1 * envoy v1.31.5-master.241218.3 * ingress-dispatcher v1.31.5-master.250126.7 * kube-state-metrics v2.15.0-4 * gpu-provisioner 0.3.3 * karpenter 0.7.3-aks * kube-egress-gateway-controller v0.0.20 * kubelet-serving-csr-approver v0.0.7 * live-patching-controller v0.0.8 |
* Linux - Ubuntu 22.04 * containerd 1.7.27-ubuntu22.04u1 * kubernetes-cri-tools 1.32.0-ubuntu22.04u3 * runc 1.2.6-ubuntu22.04u1 * Linux - AzureLinux 3.0 * containerd 2.0.0-4.azl3 * nvidia-container-toolkit 1.17.3 * Windows - Windows2022 * containerd v1.7.20-azure.1 |
* coredns v1.11.3-7 → v1.12.1-1 * cloud-provider-node-manager-windows v1.32.5 → v1.33.0 * cloud-provider-node-manager-linux v1.32.5 → v1.33.0 |
N/A |

### Kubernetes 1.32

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.8.0 * Metrics-Server 0.6.3 * App routing operator v0.2.3 * KEDA 2.14.1 * Open Service Mesh v1.2.9 * Core DNS V1.9.4 * Overlay VPA 1.0.0 * Azure-Keyvault-SecretsProvider v1.4.5 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.3.1 * Azure Workload identity v1.3.0 * MDC Defender Low Level Collector 2.0.186 * open-policy-agent-gatekeeper v3.17.1 * Retina v0.0.17 |
* Cilium v1.17.0 * Cluster Autoscaler v1.30.6-aks * Tigera-Operator v1.34.7 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.23-ubuntu22.04u1 for Linux and v1.6.35+azure for Windows * Azure Linux 3.0 * Cgroups V2 * ContainerD 1.7.13-3.azl |
*
|

### Kubernetes 1.31

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.8.0 * Metrics-Server 0.6.3 * App routing operator v0.2.3 * KEDA 2.14.1 * Open Service Mesh v1.2.9 * Core DNS V1.9.4 * Overlay VPA 1.0.0 * Azure-Keyvault-SecretsProvider v1.4.5 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.3.1 * Azure Workload identity v1.3.0 * MDC Defender Low Level Collector 2.0.186 * open-policy-agent-gatekeeper v3.17.1 * Retina v0.0.17 |
* Cilium v1.16.6 * Cluster Autoscaler v1.30.6-aks * Tigera-Operator v1.30.11 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.23-ubuntu22.04u1 for Linux and v1.6.35+azure for Windows * Azure Linux 3.0 * Cgroups V2 * ContainerD 1.7.13-3.azl |
*
|

### Kubernetes 1.30

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.3.0 * App routing operator v0.2.3 * Metrics-Server 0.6.3 * KEDA 2.11.2 * Open Service Mesh 1.2.7 * Core DNS V1.9.4 * Overlay VPA 0.13.0 * Azure-Keyvault-SecretsProvider 1.4.1 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.2.3 * Azure Workload identity v1.2.0 * MDC Defender Security Publisher 1.0.68 * MDC Defender Old File Cleaner 1.3.68 * MDC Defender Pod Collector 1.0.78 * MDC Defender Low Level Collector 2.0.186 * Microsoft Entra Pod Identity 1.8.13.6 * GitOps 1.8.1 * CSI Secrets Store Driver 1.3.4-1 *
|
* Cilium v1.14.9 * CNI v1.4.43.1 (Default)/v1.5.11 (Azure CNI Overlay) * Cluster Autoscaler 1.27.3 * Tigera-Operator 1.30.7 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.5 for Linux and 1.7.1 for Windows * Azure Linux 2.0 * Cgroups V2 * ContainerD 1.6 |
* Tigera-Operator 1.30.7 | N/A |

### Kubernetes 1.29

AKS Managed Addons (addon) |
AKS Components (ccp) |
OS Components |
Breaking Changes |
Notes |
|---|---|---|---|---|
| * Azure Policy 1.3.0 * csi-provisioner v4.0.0 * App routing operator v0.2.1 * csi-attacher v4.5.0 * csi-snapshotter v6.3.3 * snapshot-controller v6.3.3 * Metrics-Server 0.6.3 * KEDA 2.11.2 * Open Service Mesh 1.2.7 * Core DNS V1.9.4 * Overlay VPA 0.13.0 * Azure-Keyvault-SecretsProvider 1.4.1 * Application Gateway Ingress Controller (AGIC) 1.7.2 * Image Cleaner v1.2.3 * Azure Workload identity v1.2.0 * MDC Defender Security Publisher 1.0.68 * MDC Defender Old File Cleaner 1.3.68 * MDC Defender Pod Collector 1.0.78 * MDC Defender Low Level Collector 2.0.186 * Microsoft Entra Pod Identity 1.8.13.6 * GitOps 1.8.1 * CSI Secrets Store Driver 1.3.4-1 * azurefile-csi-driver 1.29.3 |
* Cilium v1.14.9 * CNI v1.4.43.1 (Default)/v1.5.11 (Azure CNI Overlay) * Cluster Autoscaler 1.27.3 * Tigera-Operator 1.30.7 |
* OS Image Ubuntu 22.04 Cgroups V2 * ContainerD 1.7.5 for Linux and 1.7.1 for Windows * Azure Linux 2.0 * Cgroups V2 * ContainerD 1.6 |
* Tigera-Operator 1.30.7 * csi-provisioner v4.0.0 * csi-attacher v4.5.0 * csi-snapshotter v6.3.3 * snapshot-controller v6.3.3 |
N/A |

## Alias minor version

Note

Alias minor version requires Azure CLI version 2.37 or above and API version 20220401 or above. Use `az upgrade`

to install the latest version of the CLI.

You can create an AKS cluster without specifying a patch version. When you create a cluster without designating a patch, the cluster runs the minor version's latest GA patch. For example, if you create a cluster with ** 1.29** and

**is the latest GA would patch available, your cluster is created with**

`1.29.2`

**. If you want to upgrade your patch version in the same minor version, use**

`1.29.2`

[autoupgrade](auto-upgrade-cluster).

To see what patch you're on, run the `az aks show --resource-group myResourceGroup --name myAKSCluster`

command. The `currentKubernetesVersion`

property shows the whole Kubernetes version.

```
{
"apiServerAccessProfile": null,
"autoScalerProfile": null,
"autoUpgradeProfile": null,
"azurePortalFqdn": "myaksclust-myresourcegroup.portal.hcp.eastus.azmk8s.io",
"currentKubernetesVersion": "1.29.2",
}
```


## Kubernetes version support policy

AKS defines a generally available (GA) version as a version available in all regions and enabled in all SLO or SLA measurements. AKS supports three GA minor versions of Kubernetes:

AKS supports three GA minor versions:

- The latest GA version (N).
- The two previous minor versions (N-1 and N-2).
- Each supported minor version can support any number of patches at a given time. AKS reserves the right to deprecate patches if a critical CVE or security vulnerability is detected. For awareness on patch availability and any ad-hoc deprecation, refer to version release notes and visit the
[AKS release status webpage](release-tracker).

- Each supported minor version can support any number of patches at a given time. AKS reserves the right to deprecate patches if a critical CVE or security vulnerability is detected. For awareness on patch availability and any ad-hoc deprecation, refer to version release notes and visit the

AKS might also support preview versions, which are explicitly labeled and subject to [preview terms and conditions](https://azure.microsoft.com/support/legal/preview-supplemental-terms/).

AKS provides platform support only for one GA minor version of Kubernetes after the regular supported versions. The platform support window of Kubernetes versions on AKS is known as "N-3". For more information, see [platform support policy](#platform-support-policy).

Note

AKS uses safe deployment practices that involve gradual region deployment. This means it might take up to 10 business days for a new release or a new version to be available in all regions.

The supported window of Kubernetes minor versions on AKS is known as "N-2", where N refers to the latest release, meaning that two previous minor releases are also supported.

For example, on the day that AKS introduces version 1.29, support is provided for the following versions:

| New minor version | Supported Minor Version List |
|---|---|
| 1.29 | 1.29, 1.28, 1.27 |

When a new minor version is introduced, the oldest minor version is deprecated and removed. For example, let's say the current supported minor version list is:

```
1.29
1.28
1.27
```


When AKS releases 1.30, all the 1.27 versions go out of support 30 days later.

AKS might support any number of **patches** based on upstream community release availability for a given minor version. AKS reserves the right to deprecate any of these patches at any given time due to a CVE or potential bug concern. You're always encouraged to use the latest patch for a minor version.

## Platform support policy

Platform support policy is a reduced support plan for certain unsupported Kubernetes versions. During platform support, customers only receive support from Microsoft for AKS/Azure platform related issues. Any issues related to Kubernetes functionality and components aren't supported.

Platform support policy applies to clusters in an n-3 version (where n is the latest supported AKS GA minor version), before the cluster drops to n-4. For example, Kubernetes v1.26 is considered platform support when v1.29 is the latest GA version. If you're a running an n-2 version, the moment it becomes n-3 , the version also becomes end of official support, and you enter into the platform support policy.

AKS relies on the releases and patches from [Kubernetes](https://kubernetes.io/releases/), which is an Open Source project that only supports a sliding window of three minor versions. AKS can only guarantee [full support](#kubernetes-version-support-policy) while those versions are being serviced upstream. Since there's no more patches being produced upstream, AKS can either leave those versions unpatched or fork. Due to this limitation, platform support doesn't support anything from relying on Kubernetes upstream.

This table outlines support guidelines for Community Support compared to Platform support.

| Support category | Community Support (N-2) | Platform Support (N-3) |
|---|---|---|
| Upgrades from N-3 to a supported version | Supported | Supported |
| Platform (Azure) availability | Supported | Supported |
| Node pool scaling | Supported | Supported |
| VM availability | Supported | Supported |
| Storage, Networking related issues | Supported | Supported except for bug fixes and retired components |
| Start/stop | Supported | Supported |
| Rotate certificates | Supported | Supported |
| Infrastructure SLA | Supported | Supported |
| Control Plane SLA | Supported | Supported |
| Platform (AKS) SLA | Supported | Not supported |
| Kubernetes components (including Add-ons) | Supported | Not supported |
| Component updates | Supported | Not supported |
| Component hotfixes | Supported | Not supported |
| Applying bug fixes | Supported | Not supported |
| Applying security patches | Supported | Not supported |
| Kubernetes API support | Supported | Not supported |
| Node pool creation | Supported | Supported |
| Cluster creation | Supported | Not Supported |
| Node pool snapshot | Supported | Not supported |
| Node image upgrade | Supported | Supported |

Note

The table is subject to change and outlines common support scenarios. Any scenarios related to Kubernetes functionality and components aren't supported for N-3. For further support, see [Support and troubleshooting for AKS](aks-support-help).

### Supported `kubectl`

versions

You can use a `kubectl`

version that is one minor version older or newer than your kube-apiserver version, [Kubernetes support policy for kubectl](https://kubernetes.io/docs/setup/release/version-skew-policy/#kubectl).

For example, if your *kube-apiserver* is at *1.28*, then you can use versions *1.27* to *1.29* of `kubectl`

with that *kube-apiserver*.

To install or update `kubectl`

to the latest version, run:

```
az aks install-cli
```


## Long Term Support (LTS)

AKS offers one year of Community Support and one year of Long Term Support (LTS), including backported security fixes from the upstream community. Our upstream LTS working group contributes efforts back to the community to provide our customers with a longer support window.

For more information on LTS, see [Long term support for Azure Kubernetes Service (AKS)](long-term-support).

## Release and deprecation process

You can reference upcoming version releases and deprecations on the [AKS Kubernetes release calendar](#aks-kubernetes-release-calendar).

For new **minor** versions of Kubernetes:

- AKS announces new version release dates and old version deprecation in the
[AKS Release notes](https://aka.ms/aks/releasenotes)at least 30 days before removal. - AKS uses
[Azure Advisor](/en-us/azure/advisor/advisor-overview)to alert you if a new version could cause issues in your cluster because of deprecated APIs. Azure Advisor also alerts you if you're out of support - AKS publishes a
[service health notification](/en-us/azure/service-health/service-health-overview)available to all users with AKS and portal access and sends an email to the subscription administrators with the planned version removal dates.Note

To find out who is your subscription administrators or to change it, refer to

[manage Azure subscriptions](/en-us/azure/cost-management-billing/manage/add-change-subscription-administrator#assign-a-subscription-administrator). - You have
**30 days**from version removal to upgrade to a supported minor version release to continue receiving support.

For new **patch** versions of Kubernetes:

- Because of the urgent nature of patch versions, they can be introduced into the service as they become available. Once available, patches have a two month minimum lifecycle.
- In general, AKS doesn't broadly communicate the release of new patch versions. However, AKS constantly monitors and validates available CVE patches to support them in AKS in a timely manner. If a critical patch is found or user action is required, AKS notifies you to upgrade to the newly available patch.
- You have
**30 days**from a patch release's removal from AKS to upgrade into a supported patch and continue receiving support. However, you'll**no longer be able to create clusters or node pools once the version is deprecated/removed.**

### Supported versions policy exceptions

AKS reserves the right to add or remove new/existing versions with one or more critical production-impacting bugs or security issues without advance notice.

Specific patch releases might be skipped or rollout accelerated, depending on the severity of the bug or security issue.

## Azure portal and CLI versions

If you deploy an AKS cluster with Azure portal, Azure CLI, Azure PowerShell, the cluster defaults to the N-1 minor version and latest patch. For example, if AKS supports *1.29.2*, *1.29.1*, *1.28.7*, *1.28.6*, *1.27.11*, and *1.27.10*, the default version selected is *1.28.7*.

To find out what versions are currently available for your subscription and region, use the
[ az aks get-versions](/en-us/cli/azure/aks#az-aks-get-versions) command. The following example lists the available Kubernetes versions for the

*EastUS*region:

```
az aks get-versions --location eastus --output table
```


## FAQ

### How does Microsoft notify me of new Kubernetes versions?

The AKS team announces new Kubernetes version release dates in our documentation, on [GitHub](https://github.com/Azure/AKS/releases), and via email to subscription administrators with clusters nearing end of support. AKS also uses [Azure Advisor](/en-us/azure/advisor/advisor-overview) to alert you inside the Azure portal if you're out of support and inform you of deprecated APIs that can affect your application or development process.

### How often should I expect to upgrade Kubernetes versions to stay in support?

Starting with Kubernetes 1.19, the [open source community expanded support to one year](https://kubernetes.io/blog/2020/08/31/kubernetes-1-19-feature-one-year-support/). AKS commits to enabling patches and support matching the upstream commitments. For AKS clusters on 1.19 and greater, you can upgrade at a minimum of once a year to stay on a supported version.

**What happens when you upgrade a Kubernetes cluster with a minor version that isn't supported?**

If you're on the *n-3* version or older, it means you're outside of support and need to upgrade. If your upgrade from version n-3 to n-2 succeeds, you're back within our support policies. For example:

- If the oldest supported AKS minor version is
*1.27*and you're on*1.26*or older, you're outside of support. - If you successfully upgrade from
*1.26*to*1.27*or higher, you're back within our support policies.

Downgrades aren't supported.

### What does 'Outside of Support' mean?

'Outside of Support' means that:

- The version you're running is outside of the supported versions list.
- You'll be asked to upgrade the cluster to a supported version when requesting support, unless you're within the 30-day grace period after version deprecation.

Additionally, AKS doesn't make any runtime or other guarantees for clusters outside of the supported versions list.

### What happens when you scale a Kubernetes cluster with a minor version that isn't supported?

For minor versions not supported by AKS, scaling in or out should continue to work. Since there are no guarantees with quality of service, we recommend upgrading to bring your cluster back into support.

### Can you stay on a Kubernetes version forever?

If a cluster is out of support for more than three minor versions and carries security risks, Azure proactively contacts you. They advise you to upgrade your cluster. If you don't take further action, Azure reserves the right to automatically upgrade your cluster on your behalf.

### What happens if you scale a Kubernetes cluster with a minor version that isn't supported?

For minor versions not supported by AKS, scaling in or out should continue to work. Since there are no guarantees with quality of service, we recommend upgrading to bring your cluster back into support.

### What version does the control plane support if the node pool isn't in one of the supported AKS versions?

The control plane must be within a window of versions from all node pools. For details on upgrading the control plane or node pools, visit documentation on [upgrading node pools](manage-node-pools#upgrade-a-cluster-control-plane-with-multiple-node-pools).

### What is the allowed difference in versions between control plane and node pool?

The [version skew policy](https://kubernetes.io/releases/version-skew-policy/) now allows a difference of up to three versions between control plane and agent pools. AKS follows this skew version policy change starting from version 1.28 onwards.

### Can I skip multiple AKS versions during cluster upgrade?

If you upgrade a supported AKS cluster, Kubernetes minor versions can't be skipped. Kubernetes control planes [version skew policy](https://kubernetes.io/releases/version-skew-policy/) doesn't support minor version skipping. For example, upgrades between:

*1.28.x*->*1.29.x*: allowed.*1.27.x*->*1.28.x*: allowed.*1.27.x*->*1.29.x*: not allowed.

For control plane version upgrades, you can go up to three minor versions for community supported versions in sequential fashion.

To upgrade from *1.27.x* -> *1.29.x*:

- Upgrade from
*1.27.x*->*1.28.x*. - Upgrade from
*1.28.x*->*1.29.x*.

Note starting from 1.28 version onwards, agentpool versions can be up to three versions older to control plane versions per [version skew policy](https://kubernetes.io/releases/version-skew-policy/). If your version is much behind the minimum supported version, you might have to do more than one control plane upgrade operation to get to the minimum supported version. For example, if your current control plane version is *1.23.x* and you intend to upgrade to a minimum supported version of *1.27.x* as an example. You might have to upgrade sequentially four times from *1.23.x* in order to get to *1.27.x*. Also note that Agent pool versions can be upgraded to the control plane minor version. In the previous example you can upgrade agentpool version twice, once from *1.23.x* to *1.25.x*, when the control plane version is at *1.25.x*. And then from *1.25.x* to *1.27.x*, when control plane version is at *1.27.x*. When you upgrade in-place, like control plane and agent pool together the same rules applicable to control plane upgrade applies.

If performing an upgrade from an *unsupported version* the upgrade is done without any guarantee of functionality and is excluded from the service-level agreements and limited warranty. Clusters running *unsupported version* has the flexibility of decoupling control plane upgrades with node pool upgrades. However if your version is out of date, we recommend that you re-create the cluster.

### Can I create a new 1.xx.x cluster during the platform support window?

No, Creation of new clusters isn't possible during Platform Support period.

### I'm on a freshly deprecated version that is out of platform support, can I still add new node pools? Or should I upgrade?

Yes, you can add agent pools as long as they're compatible with the control plane version.

## Next steps

For information on how to upgrade your cluster, see:
