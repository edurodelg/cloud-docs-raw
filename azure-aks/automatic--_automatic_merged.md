---
merged_at: 2026-02-06T16:45:38.405684
merged_files: 3
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/automatic/quick-automatic-managed-network -->

# Quickstart: Create an Azure Kubernetes Service (AKS) Automatic cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

[Azure Kubernetes Service (AKS) Automatic](../intro-aks-automatic) provides the easiest managed Kubernetes experience for developers, DevOps engineers, and platform engineers. Ideal for modern and AI applications, AKS Automatic automates AKS cluster setup and operations and embeds best practice configurations. Users of any skill level can benefit from the security, performance, and dependability of AKS Automatic for their applications. AKS Automatic also includes a [pod readiness SLA](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services) that guarantees 99.9% of pod readiness operations complete within 5 minutes, guaranteeing reliable, self-healing infrastructure for your applications.

In this quickstart, you learn to:

- Deploy an AKS Automatic cluster.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

## Before you begin

- This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads). - AKS Automatic will
[enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks), but you should pre-register the`Microsoft.PolicyInsights`

resource provider in your subscription for a smoother experience. See[Azure resource providers and types](/en-us/cli/azure/provider#az-provider-register)for more information.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.77.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command.`az account set`


- To deploy a Bicep file, you need to write access on the resources you create and access to all operations on the
`Microsoft.Resources/deployments`

resource type. For example, to create a virtual machine, you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

## Limitations

- AKS Automatic clusters' system nodepool require deployment in Azure regions that support at least three
[availability zones](/en-us/azure/reliability/regions-list), ephemeral OS disk, and Azure Linux OS. - You can only create AKS Automatic clusters in regions where
[API Server VNet Integration](../api-server-vnet-integration)is generally available (GA).

Important

AKS Automatic tries to dynamically select a virtual machine size for the `system`

node pool based on the capacity available in the subscription. Make sure your subscription has quota for 16 vCPUs of any of the following sizes in the region you're deploying the cluster to: [Standard_D4lds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series), [Standard_D4ads_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dadsv5-series), [Standard_D4ds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v4](/en-us/azure/virtual-machines/sizes/general-purpose/dv4-series), [Standard_DS3_v2](/en-us/azure/virtual-machines/sizes/general-purpose/dsv3-series), [Standard_DS12_v2](/en-us/azure/virtual-machines/sizes/memory-optimized/dv2-dsv2-series-memory), [Standard_D4alds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/daldsv6-series), [Standard_D4lds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv6-series), or [Standard_D4alds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series). You can [view quotas for specific VM-families and submit quota increase requests](/en-us/azure/quotas/per-vm-quota-requests) through the Azure portal.
If you have additional questions, learn more through the [troubleshooting docs](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/aks-automatic-troubleshoot/).

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name myResourceGroup --location eastus
```


The following sample output resembles successful creation of the resource group:

```
{
"id": "/subscriptions/<guid>/resourceGroups/myResourceGroup",
"location": "eastus",
"managedBy": null,
"name": "myResourceGroup",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null
}
```


## Create an AKS Automatic cluster

To create an AKS Automatic cluster, use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a cluster named

*myAKSAutomaticCluster*with Managed Prometheus and Container Insights integration enabled.

```
az aks create \
--resource-group myResourceGroup \
--name myAKSAutomaticCluster \
--sku automatic
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with

[Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

Note

When you create a cluster using the Azure CLI, your user is [assigned built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) for `Azure Kubernetes Service RBAC Cluster Admin`

.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSAutomaticCluster
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Create Automatic Kubernetes cluster

To create an AKS Automatic cluster, search for

**Kubernetes Services**, and select**Automatic Kubernetes cluster**from the drop-down options.On the

**Basics**tab, fill in all the mandatory fields (Subscription, Resource group, Kubernetes cluster name, and Region) required to get started:On the

**Monitoring**tab, choose your monitoring configurations from Azure Monitor, Managed Prometheus, Grafana Dashboards, Container Network Observability (ACNS) and/or configure alerts. Enable Managed Grafana (optional), add tags (optional), and proceed to create the cluster.On the

**Advanced**tab, update your networking (optional), managed identity (optional), security and managed namespaces (optional) settings and proceed to create the cluster.Get started with configuring your first application from GitHub and set up an automated deployment pipeline.


## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac). When you create a cluster using the Azure portal, your user is [assigned built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) for `Azure Kubernetes Service RBAC Cluster Admin`

.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSAutomaticCluster
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name myResourceGroup --location eastus
```


The following sample output resembles successful creation of the resource group:

```
{
"id": "/subscriptions/<guid>/resourceGroups/myResourceGroup",
"location": "eastus",
"managedBy": null,
"name": "myResourceGroup",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null
}
```


## Review the Bicep file

This Bicep file defines an AKS Automatic cluster. While in preview, you need to specify the *system nodepool* agent pool profile.

```
@description('The name of the managed cluster resource.')
param clusterName string = 'myAKSAutomaticCluster'
@description('The location of the managed cluster resource.')
param location string = resourceGroup().location
resource aks 'Microsoft.ContainerService/managedClusters@2024-03-02-preview' = {
name: clusterName
location: location
sku: {
name: 'Automatic'
}
properties: {
agentPoolProfiles: [
{
name: 'systempool'
mode: 'System'
count: 3
}
]
}
identity: {
type: 'SystemAssigned'
}
}
```


For more information about the resource defined in the Bicep file, see the [ Microsoft.ContainerService/managedClusters](/en-us/azure/templates/microsoft.containerservice/managedclusters?tabs=bicep&pivots=deployment-language-bicep) reference.

## Deploy the Bicep file

Save the Bicep file as

**main.bicep**to your local computer.Important

The Bicep file sets the

`clusterName`

param to the string*myAKSAutomaticCluster*. If you want to use a different cluster name, make sure to update the string to your preferred cluster name before saving the file to your computer.Deploy the Bicep file using the Azure CLI.

`az deployment group create --resource-group myResourceGroup --template-file main.bicep`

It takes a few minutes to create the AKS cluster. Wait for the cluster to be successfully deployed before you move on to the next step.


## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

Important

When you create a cluster using Bicep, you need to [assign one of the built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) such as `Azure Kubernetes Service RBAC Reader`

, `Azure Kubernetes Service RBAC Writer`

, `Azure Kubernetes Service RBAC Admin`

, or `Azure Kubernetes Service RBAC Cluster Admin`

to your users, scoped to the cluster or a specific namespace, example using `az role assignment create --role "Azure Kubernetes Service RBAC Cluster Admin" --scope <AKS cluster resource id> --assignee user@contoso.com`

. Also make sure your users have the `Azure Kubernetes Service Cluster User`

built-in role to be able to do run `az aks get-credentials`

, and then get the kubeconfig of your AKS cluster using the `az aks get-credentials`

command.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a namespace

`aks-store-demo`

to deploy the Kubernetes resources into.`kubectl create ns aks-store-demo`

Deploy the application using the

command into the`kubectl apply`

`aks-store-demo`

namespace. The YAML file defining the deployment is on[GitHub](https://github.com/Azure-Samples/aks-store-demo).`kubectl apply -n aks-store-demo -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-ingress-quickstart.yaml`

The following sample output shows the deployments and services:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created ingress/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make sure all pods are`Running`

before proceeding. If this is the first workload you deploy, it may take a few minutes for[node auto provisioning](../node-autoprovision)to create a node pool to run the pods.`kubectl get pods -n aks-store-demo`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get ingress store-front -n aks-store-demo --watch`

The

**ADDRESS**output for the`store-front`

service initially shows empty:`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 80 12m`

Once the

**ADDRESS**changes from blank to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following sample output shows a valid public IP address assigned to the service:

`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 4.255.22.196 80 12m`

Open a web browser to the external IP address of your ingress to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges. Run the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.

```
az group delete --name myResourceGroup --yes --no-wait
```


Note

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity, so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster using [AKS Automatic](../intro-aks-automatic) and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS Automatic, continue to the introduction.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/automatic/quick-automatic-custom-network -->

# Quickstart: Create an Azure Kubernetes Service (AKS) Automatic cluster in a custom virtual network

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

[Azure Kubernetes Service (AKS) Automatic](../intro-aks-automatic) provides the easiest managed Kubernetes experience for developers, DevOps engineers, and platform engineers. Ideal for modern and AI applications, AKS Automatic automates AKS cluster setup and operations and embeds best practice configurations. Users of any skill level can benefit from the security, performance, and dependability of AKS Automatic for their applications. AKS Automatic also includes a [pod readiness SLA](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services) that guarantees 99.9% of pod readiness operations complete within 5 minutes, guaranteeing reliable, self-healing infrastructure for your applications. This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

In this quickstart, you learn to:

- Create a virtual network.
- Create a managed identity with permissions over the virtual network.
- Deploy an AKS Automatic cluster in the virtual network.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

If you don't have an Azure account, create a [free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

### Prerequisites

- This article requires version 2.77.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there. If you need to install or upgrade, see
[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

- Cluster identity with a
`Network Contributor`

built-in role assignment on the API server subnet. - Cluster identity with a
`Network Contributor`

built-in role assignment on the virtual network to support[Node Autoprovisioning](../node-autoprovision). - User identity accessing the cluster with
and`Azure Kubernetes Service Cluster User Role`

.`Azure Kubernetes Service RBAC Writer`

- A virtual network with a dedicated API server subnet of at least
`*/28`

size that is delegated to`Microsoft.ContainerService/managedClusters`

.- If there's a Network Security Group (NSG) attached to subnets, ensure that the NSG security rules permit the required types of communication between cluster components. For detailed requirements, see
[Custom virtual network requirements](../concepts-network#custom-virtual-network-requirements). - If there's an Azure Firewall or other outbound restriction method or appliance, ensure the
[required outbound network rules and FQDNs](../outbound-rules-control-egress)are allowed.

- If there's a Network Security Group (NSG) attached to subnets, ensure that the NSG security rules permit the required types of communication between cluster components. For detailed requirements, see
- AKS Automatic will
[enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks), but you should pre-register the`Microsoft.PolicyInsights`

resource provider in your subscription for a smoother experience. See[Azure resource providers and types](/en-us/cli/azure/provider#az-provider-register)for more information.

## Limitations

- AKS Automatic clusters' system nodepool require deployment in Azure regions that support at least three
[availability zones](/en-us/azure/reliability/regions-list), ephemeral OS disk, and Azure Linux OS. - You can only create AKS Automatic clusters in regions where
[API Server VNet Integration](../api-server-vnet-integration)is generally available (GA).

Important

AKS Automatic tries to dynamically select a virtual machine size for the `system`

node pool based on the capacity available in the subscription. Make sure your subscription has quota for 16 vCPUs of any of the following sizes in the region you're deploying the cluster to: [Standard_D4lds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series), [Standard_D4ads_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dadsv5-series), [Standard_D4ds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v4](/en-us/azure/virtual-machines/sizes/general-purpose/dv4-series), [Standard_DS3_v2](/en-us/azure/virtual-machines/sizes/general-purpose/dsv3-series), [Standard_DS12_v2](/en-us/azure/virtual-machines/sizes/memory-optimized/dv2-dsv2-series-memory), [Standard_D4alds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/daldsv6-series), [Standard_D4lds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv6-series), or [Standard_D4alds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series). You can [view quotas for specific VM-families and submit quota increase requests](/en-us/azure/quotas/per-vm-quota-requests) through the Azure portal.
If you have additional questions, learn more through the [troubleshooting docs](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/aks-automatic-troubleshoot/).

## Define variables

Define the following variables that will be used in the subsequent steps.

```
RG_NAME=automatic-rg
VNET_NAME=automatic-vnet
CLUSTER_NAME=automatic
IDENTITY_NAME=automatic-uami
LOCATION=eastus
SUBSCRIPTION_ID=$(az account show --query id -o tsv)
```


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed.

Create a resource group using the [az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create -n ${RG_NAME} -l ${LOCATION}
```


The following sample output resembles successful creation of the resource group:

```
{
"id": "/subscriptions/<guid>/resourceGroups/automatic-rg",
"location": "eastus",
"managedBy": null,
"name": "automatic-rg",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null
}
```


## Create a virtual network

Create a virtual network using the [ az network vnet create](/en-us/cli/azure/network/vnet#az-network-vnet-create) command. Create an API server subnet and cluster subnet using the

[command.](/en-us/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create)

`az network vnet subnet create`

When using a custom virtual network with AKS Automatic, you must create and delegate an API server subnet to `Microsoft.ContainerService/managedClusters`

, which grants the AKS service permissions to inject the API server pods and internal load balancer into that subnet. You can't use the subnet for any other workloads, but you can use it for multiple AKS clusters located in the same virtual network. The minimum supported API server subnet size is a */28*.

Warning

An AKS cluster reserves at least 9 IPs in the subnet address space. Running out of IP addresses may prevent API server scaling and cause an API server outage.

```
az network vnet create --name ${VNET_NAME} \
--resource-group ${RG_NAME} \
--location ${LOCATION} \
--address-prefixes 172.19.0.0/16
az network vnet subnet create --resource-group ${RG_NAME} \
--vnet-name ${VNET_NAME} \
--name apiServerSubnet \
--delegations Microsoft.ContainerService/managedClusters \
--address-prefixes 172.19.0.0/28
az network vnet subnet create --resource-group ${RG_NAME} \
--vnet-name ${VNET_NAME} \
--name clusterSubnet \
--address-prefixes 172.19.1.0/24
```


### Network security group requirements

If you have added Network Security Group (NSG) rules to restrict traffic between different subnets in your custom virtual network, ensure that the NSG security rules permit the required types of communication between cluster components.

For detailed NSG requirements when using custom virtual networks with AKS clusters, see [Custom virtual network requirements](../concepts-network#custom-virtual-network-requirements).

## Create a managed identity and give it permissions on the virtual network

Create a managed identity using the [ az identity create](/en-us/cli/azure/identity#az-identity-create) command and retrieve the principal ID. Assign the

**Network Contributor**role on virtual network to the managed identity using the

[command.](/en-us/cli/azure/role/assignment#az-role-assignment-create)

`az role assignment create`

```
az identity create \
--resource-group ${RG_NAME} \
--name ${IDENTITY_NAME} \
--location ${LOCATION}
IDENTITY_PRINCIPAL_ID=$(az identity show --resource-group ${RG_NAME} --name ${IDENTITY_NAME} --query principalId -o tsv)
az role assignment create \
--scope "/subscriptions/${SUBSCRIPTION_ID}/resourceGroups/${RG_NAME}/providers/Microsoft.Network/virtualNetworks/${VNET_NAME}" \
--role "Network Contributor" \
--assignee ${IDENTITY_PRINCIPAL_ID}
```


## Create an AKS Automatic cluster in a custom virtual network

To create an AKS Automatic cluster, use the [az aks create](/en-us/cli/azure/aks#az-aks-create) command.

```
az aks create \
--resource-group ${RG_NAME} \
--name ${CLUSTER_NAME} \
--location ${LOCATION} \
--apiserver-subnet-id "/subscriptions/${SUBSCRIPTION_ID}/resourceGroups/${RG_NAME}/providers/Microsoft.Network/virtualNetworks/${VNET_NAME}/subnets/apiServerSubnet" \
--vnet-subnet-id "/subscriptions/${SUBSCRIPTION_ID}/resourceGroups/${RG_NAME}/providers/Microsoft.Network/virtualNetworks/${VNET_NAME}/subnets/clusterSubnet" \
--assign-identity "/subscriptions/${SUBSCRIPTION_ID}/resourcegroups/${RG_NAME}/providers/Microsoft.ManagedIdentity/userAssignedIdentities/${IDENTITY_NAME}" \
--sku automatic \
--no-ssh-key
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

When you create a cluster using the Azure CLI, your user is [assigned built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) for `Azure Kubernetes Service RBAC Cluster Admin`

.

Configure `kubectl`

to connect to your Kubernetes cluster using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group ${RG_NAME} --name ${CLUSTER_NAME}
```


Verify the connection to your cluster using the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Create a virtual network

This Bicep file defines a virtual network.

```
@description('The location of the managed cluster resource.')
param location string = resourceGroup().location
@description('The name of the virtual network.')
param vnetName string = 'aksAutomaticVnet'
@description('The address prefix of the virtual network.')
param addressPrefix string = '172.19.0.0/16'
@description('The name of the API server subnet.')
param apiServerSubnetName string = 'apiServerSubnet'
@description('The subnet prefix of the API server subnet.')
param apiServerSubnetPrefix string = '172.19.0.0/28'
@description('The name of the cluster subnet.')
param clusterSubnetName string = 'clusterSubnet'
@description('The subnet prefix of the cluster subnet.')
param clusterSubnetPrefix string = '172.19.1.0/24'
// Virtual network with an API server subnet and a cluster subnet
resource virtualNetwork 'Microsoft.Network/virtualNetworks@2023-09-01' = {
name: vnetName
location: location
properties: {
addressSpace: {
addressPrefixes: [ addressPrefix ]
}
subnets: [
{
name: apiServerSubnetName
properties: {
addressPrefix: apiServerSubnetPrefix
}
}
{
name: clusterSubnetName
properties: {
addressPrefix: clusterSubnetPrefix
}
}
]
}
}
output apiServerSubnetId string = resourceId('Microsoft.Network/virtualNetworks/subnets', vnetName, apiServerSubnetName)
output clusterSubnetId string = resourceId('Microsoft.Network/virtualNetworks/subnets', vnetName, clusterSubnetName)
```


Save the Bicep file **virtualNetwork.bicep** to your local computer.

Important

The Bicep file sets the `vnetName`

param to *aksAutomaticVnet*, the `addressPrefix`

param to *172.19.0.0/16*, the `apiServerSubnetPrefix`

param to *172.19.0.0/28*, and the `apiServerSubnetPrefix`

param to *172.19.1.0/24*. If you want to use different values, make sure to update the strings to your preferred values.

Deploy the Bicep file using the Azure CLI.

```
az deployment group create --resource-group <resource-group> --template-file virtualNetwork.bicep
```


All traffic within the virtual network is allowed by default. If you have added Network Security Group (NSG) rules to restrict traffic between different subnets in your custom virtual network, ensure that the NSG security rules permit the required types of communication between cluster components.

For detailed NSG requirements when using custom virtual networks with AKS clusters, see [Custom virtual network requirements](../concepts-network#custom-virtual-network-requirements).

## Create a managed identity

This Bicep file defines a user assigned managed identity.

```
param location string = resourceGroup().location
param uamiName string = 'aksAutomaticUAMI'
resource userAssignedManagedIdentity 'Microsoft.ManagedIdentity/userAssignedIdentities@2023-01-31' = {
name: uamiName
location: location
}
output uamiId string = userAssignedManagedIdentity.id
output uamiPrincipalId string = userAssignedManagedIdentity.properties.principalId
output uamiClientId string = userAssignedManagedIdentity.properties.clientId
```


Save the Bicep file **uami.bicep** to your local computer.

Important

The Bicep file sets the `uamiName`

param to the *aksAutomaticUAMI*. If you want to use a different identity name, make sure to update the string to your preferred name.

Deploy the Bicep file using the Azure CLI.

```
az deployment group create --resource-group <resource-group> --template-file uami.bicep
```


## Assign the Network Contributor role over the virtual network

This Bicep file defines role assignments over the virtual network.

```
@description('The name of the virtual network.')
param vnetName string = 'aksAutomaticVnet'
@description('The principal ID of the user assigned managed identity.')
param uamiPrincipalId string
// Get a reference to the virtual network
resource virtualNetwork 'Microsoft.Network/virtualNetworks@2023-09-01' existing ={
name: vnetName
}
// Assign the Network Contributor role to the user assigned managed identity on the virtual network
// '4d97b98b-1d4f-4787-a291-c67834d212e7' is the built-in Network Contributor role definition
// See: https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles/networking#network-contributor
resource networkContributorRoleAssignmentToVirtualNetwork 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(uamiPrincipalId, '4d97b98b-1d4f-4787-a291-c67834d212e7', resourceGroup().id, virtualNetwork.name)
scope: virtualNetwork
properties: {
roleDefinitionId: resourceId('Microsoft.Authorization/roleDefinitions', '4d97b98b-1d4f-4787-a291-c67834d212e7')
principalId: uamiPrincipalId
}
}
```


Save the Bicep file **roleAssignments.bicep** to your local computer.

Important

The Bicep file sets the `vnetName`

param to *aksAutomaticVnet*. If you used a different virtual network name, make sure to update the string to your preferred virtual network name.

Deploy the Bicep file using the Azure CLI. You need to provide the user assigned identity principal ID.

```
az deployment group create --resource-group <resource-group> --template-file roleAssignments.bicep \
--parameters uamiPrincipalId=<user assigned identity prinicipal id>
```


## Create an AKS Automatic cluster in a custom virtual network

This Bicep file defines the AKS Automatic cluster.

```
@description('The name of the managed cluster resource.')
param clusterName string = 'aksAutomaticCluster'
@description('The location of the managed cluster resource.')
param location string = resourceGroup().location
@description('The resource ID of the API server subnet.')
param apiServerSubnetId string
@description('The resource ID of the cluster subnet.')
param clusterSubnetId string
@description('The resource ID of the user assigned managed identity.')
param uamiId string
/// Create the AKS Automatic cluster using the custom virtual network and user assigned managed identity
resource aks 'Microsoft.ContainerService/managedClusters@2024-03-02-preview' = {
name: clusterName
location: location
sku: {
name: 'Automatic'
}
properties: {
agentPoolProfiles: [
{
name: 'systempool'
mode: 'System'
count: 3
vnetSubnetID: clusterSubnetId
}
]
apiServerAccessProfile: {
subnetId: apiServerSubnetId
}
networkProfile: {
outboundType: 'loadBalancer'
}
}
identity: {
type: 'UserAssigned'
userAssignedIdentities: {
'${uamiId}': {}
}
}
}
```


Save the Bicep file **aks.bicep** to your local computer.

Important

The Bicep file sets the `clusterName`

param to *aksAutomaticCluster*. If you want a different cluster name, make sure to update the string to your preferred cluster name.

Deploy the Bicep file using the Azure CLI. You need to provide the API server subnet resource ID, the cluster subnet resource ID, and user assigned managed identity resource ID.

```
az deployment group create --resource-group <resource-group> --template-file aks.bicep \
--parameters apiServerSubnetId=<API server subnet resource id> \
--parameters clusterSubnetId=<cluster subnet resource id> \
--parameters uamiId=<user assigned identity id>
```


## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

Important

When you create a cluster using Bicep, you need to [assign one of the built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) such as `Azure Kubernetes Service RBAC Reader`

, `Azure Kubernetes Service RBAC Writer`

, `Azure Kubernetes Service RBAC Admin`

, or `Azure Kubernetes Service RBAC Cluster Admin`

to your users, scoped to the cluster or a specific namespace, example using `az role assignment create --role "Azure Kubernetes Service RBAC Cluster Admin" --scope <AKS cluster resource id> --assignee user@contoso.com`

. Also make sure your users have the `Azure Kubernetes Service Cluster User`

built-in role to be able to do run `az aks get-credentials`

, and then get the kubeconfig of your AKS cluster using the `az aks get-credentials`

command.

Configure `kubectl`

to connect to your Kubernetes cluster using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group <resource-group> --name <cluster-name>
```


Verify the connection to your cluster using the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These containers are used here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a namespace

`aks-store-demo`

to deploy the Kubernetes resources into.`kubectl create ns aks-store-demo`

Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command into the`aks-store-demo`

namespace. The YAML file defining the deployment is on[GitHub](https://github.com/Azure-Samples/aks-store-demo).`kubectl apply -n aks-store-demo -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-ingress-quickstart.yaml`

The following sample output shows the deployments and services:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created ingress/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make sure all pods are`Running`

before proceeding. If this is the first workload you deploy, it may take a few minutes for[node auto provisioning](../node-autoprovision)to create a node pool to run the pods.`kubectl get pods -n aks-store-demo`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get ingress store-front -n aks-store-demo --watch`

The

**ADDRESS**output for the`store-front`

service initially shows empty:`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 80 12m`

Once the

**ADDRESS**changes from blank to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following sample output shows a valid public IP address assigned to the service:

`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 4.255.22.196 80 12m`

Open a web browser to the external IP address of your ingress to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges. Run the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.

```
az group delete --name <resource-group> --yes --no-wait
```


Note

The AKS cluster was created with a user-assigned managed identity. If you don't need that identity anymore, you can manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster using [AKS Automatic](../intro-aks-automatic) inside a custom virtual network and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS Automatic, continue to the introduction.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/automatic/quick-automatic-private-custom-network -->

# Quickstart: Create a private Azure Kubernetes Service (AKS) Automatic cluster in a custom virtual network

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

[Azure Kubernetes Service (AKS) Automatic](../intro-aks-automatic) provides the easiest managed Kubernetes experience for developers, DevOps engineers, and platform engineers. Ideal for modern and AI applications, AKS Automatic automates AKS cluster setup and operations and embeds best practice configurations. Users of any skill level can benefit from the security, performance, and dependability of AKS Automatic for their applications. AKS Automatic also includes a [pod readiness SLA](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services) that guarantees 99.9% of pod readiness operations complete within 5 minutes, guaranteeing reliable, self-healing infrastructure for your applications. This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

In this quickstart, you learn to:

- Create a virtual network.
- Create a managed identity with permissions over the virtual network.
- Deploy a private AKS Automatic cluster in the virtual network.
- Connect to the private cluster.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

### Prerequisites

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

- This article requires version 2.77.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there. If you need to install or upgrade, see
[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

- Cluster identity with a
`Network Contributor`

built-in role assignment on the API server subnet. - Cluster identity with a
`Network Contributor`

built-in role assignment on the virtual network to support[Node Autoprovisioning](../node-autoprovision). - User identity accessing the cluster with
and`Azure Kubernetes Service Cluster User Role`

.`Azure Kubernetes Service RBAC Writer`

- A virtual network with a dedicated API server subnet of at least
`*/28`

size that is delegated to`Microsoft.ContainerService/managedClusters`

.- If there's a Network Security Group (NSG) attached to subnets, ensure that the
[rules permit the following traffic](#network-security-group-rules)between the nodes and the API server, the Azure Load Balancer and the API server, and pod to pod communication. - If there's an Azure Firewall or other outbound restriction method or appliance, ensure the
[required outbound network rules and FQDNs](../outbound-rules-control-egress)are allowed.

- If there's a Network Security Group (NSG) attached to subnets, ensure that the
- AKS Automatic will
[enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks), but you should pre-register the`Microsoft.PolicyInsights`

resource provider in your subscription for a smoother experience. See[Azure resource providers and types](/en-us/cli/azure/provider#az-provider-register)for more information.

## Limitations

- AKS Automatic clusters' system nodepool require deployment in Azure regions that support at least three
[availability zones](/en-us/azure/reliability/regions-list), ephemeral OS disk, and Azure Linux OS. - You can only create AKS Automatic clusters in regions where
[API Server VNet Integration](../api-server-vnet-integration)is generally available (GA).

Important

AKS Automatic tries to dynamically select a virtual machine size for the `system`

node pool based on the capacity available in the subscription. Make sure your subscription has quota for 16 vCPUs of any of the following sizes in the region you're deploying the cluster to: [Standard_D4lds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series), [Standard_D4ads_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dadsv5-series), [Standard_D4ds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v4](/en-us/azure/virtual-machines/sizes/general-purpose/dv4-series), [Standard_DS3_v2](/en-us/azure/virtual-machines/sizes/general-purpose/dsv3-series), [Standard_DS12_v2](/en-us/azure/virtual-machines/sizes/memory-optimized/dv2-dsv2-series-memory), [Standard_D4alds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/daldsv6-series), [Standard_D4lds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv6-series), or [Standard_D4alds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series). You can [view quotas for specific VM-families and submit quota increase requests](/en-us/azure/quotas/per-vm-quota-requests) through the Azure portal.
If you have additional questions, learn more through the [troubleshooting docs](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/aks-automatic-troubleshoot/).

## Define variables

Define the following variables that will be used in the subsequent steps.

```
RG_NAME=automatic-rg
VNET_NAME=automatic-vnet
CLUSTER_NAME=automatic
IDENTITY_NAME=automatic-uami
LOCATION=eastus
SUBSCRIPTION_ID=$(az account show --query id -o tsv)
```


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed.

Create a resource group using the [az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create -n ${RG_NAME} -l ${LOCATION}
```


The following sample output resembles successful creation of the resource group:

```
{
"id": "/subscriptions/<guid>/resourceGroups/automatic-rg",
"location": "eastus",
"managedBy": null,
"name": "automatic-rg",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null
}
```


## Create a virtual network

Create a virtual network using the [ az network vnet create](/en-us/cli/azure/network/vnet#az-network-vnet-create) command. Create an API server subnet and cluster subnet using the

[command.](/en-us/cli/azure/network/vnet/subnet#az-network-vnet-subnet-create)

`az network vnet subnet create`

When using a custom virtual network with AKS Automatic, you must create and delegate an API server subnet to `Microsoft.ContainerService/managedClusters`

, which grants the AKS service permissions to inject the API server pods and internal load balancer into that subnet. You can't use the subnet for any other workloads, but you can use it for multiple AKS clusters located in the same virtual network. The minimum supported API server subnet size is a */28*.

Warning

An AKS cluster reserves at least 9 IPs in the subnet address space. Running out of IP addresses may prevent API server scaling and cause an API server outage.

```
az network vnet create --name ${VNET_NAME} \
--resource-group ${RG_NAME} \
--location ${LOCATION} \
--address-prefixes 172.19.0.0/16
az network vnet subnet create --resource-group ${RG_NAME} \
--vnet-name ${VNET_NAME} \
--name apiServerSubnet \
--delegations Microsoft.ContainerService/managedClusters \
--address-prefixes 172.19.0.0/28
az network vnet subnet create --resource-group ${RG_NAME} \
--vnet-name ${VNET_NAME} \
--name clusterSubnet \
--address-prefixes 172.19.1.0/24
```


### Network security group rules

All traffic within the virtual network is allowed by default. But if you added Network Security Group (NSG) rules to restrict traffic between different subnets, ensure that the NSG security rules permit the following types of communication:

| Destination | Source | Protocol | Port | Use |
|---|---|---|---|---|
| APIServer Subnet CIDR | Cluster Subnet | TCP | 443 and 4443 | Required to enable communication between Nodes and the API server. |
| APIServer Subnet CIDR | Azure Load Balancer | TCP | 9988 | Required to enable communication between Azure Load Balancer and the API server. You can also enable all communication between the Azure Load Balancer and the API Server Subnet CIDR. |
| Node CIDR | Node CIDR | All Protocols | All Ports | Required to enable communication between Nodes. |
| Node CIDR | Pod CIDR | All Protocols | All Ports | Required for Service traffic routing. |
| Pod CIDR | Pod CIDR | All Protocols | All Ports | Required for Pod to Pod and Pod to Service traffic, including DNS. |

## Create a managed identity and give it permissions on the virtual network

Create a managed identity using the [ az identity create](/en-us/cli/azure/identity#az-identity-create) command and retrieve the principal ID. Assign the

**Network Contributor**role on virtual network to the managed identity using the

[command.](/en-us/cli/azure/role/assignment#az-role-assignment-create)

`az role assignment create`

```
az identity create \
--resource-group ${RG_NAME} \
--name ${IDENTITY_NAME} \
--location ${LOCATION}
IDENTITY_PRINCIPAL_ID=$(az identity show --resource-group ${RG_NAME} --name ${IDENTITY_NAME} --query principalId -o tsv)
az role assignment create \
--scope "/subscriptions/${SUBSCRIPTION_ID}/resourceGroups/${RG_NAME}/providers/Microsoft.Network/virtualNetworks/${VNET_NAME}" \
--role "Network Contributor" \
--assignee ${IDENTITY_PRINCIPAL_ID}
```


## Create a private AKS Automatic cluster in a custom virtual network

To create a private AKS Automatic cluster, use the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. Note the use of the `--enable-private-cluster`

flag.

Note

You can refer to the [private cluster](../private-clusters) documentation for configuring additional options like disabling the cluster's public FQDN and configuring the private DNS zone.

```
az aks create \
--resource-group ${RG_NAME} \
--name ${CLUSTER_NAME} \
--location ${LOCATION} \
--apiserver-subnet-id "/subscriptions/${SUBSCRIPTION_ID}/resourceGroups/${RG_NAME}/providers/Microsoft.Network/virtualNetworks/${VNET_NAME}/subnets/apiServerSubnet" \
--vnet-subnet-id "/subscriptions/${SUBSCRIPTION_ID}/resourceGroups/${RG_NAME}/providers/Microsoft.Network/virtualNetworks/${VNET_NAME}/subnets/clusterSubnet" \
--assign-identity "/subscriptions/${SUBSCRIPTION_ID}/resourcegroups/${RG_NAME}/providers/Microsoft.ManagedIdentity/userAssignedIdentities/${IDENTITY_NAME}" \
--sku automatic \
--enable-private-cluster \
--no-ssh-key
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster.

## Connect to the cluster

When an AKS Automatic cluster is created as a private cluster, the API server endpoint has no public IP address. To manage the API server, for example via `kubectl`

, you need to connect through a machine that has access to the cluster's Azure virtual network. There are several options for establishing network connectivity to the private cluster:

- Create a virtual machine in the same virtual network as the AKS Automatic cluster using the
command with the`az vm create`

`--vnet-name`

flag. - Use a virtual machine in a separate virtual network and set up
[virtual network peering](../private-cluster-connect#connect-using-virtual-network-vnet-peering). - Use an
[Express Route or VPN](/en-us/azure/expressroute/expressroute-about-virtual-network-gateways)connection. - Use a
[private endpoint](../private-apiserver-vnet-integration-cluster)connection.

Creating a virtual machine in the same virtual network as the AKS cluster is the easiest option. ExpressRoute and VPNs add costs and require additional networking complexity. Virtual network peering requires you to plan your network CIDR ranges to ensure there are no overlapping ranges. Refer to [Options for connecting to the private cluster](../private-cluster-connect) for more information.

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

When you create a cluster using the Azure CLI, your user is [assigned built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) for `Azure Kubernetes Service RBAC Cluster Admin`

.

Configure `kubectl`

to connect to your Kubernetes cluster using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group ${RG_NAME} --name ${CLUSTER_NAME}
```


Verify the connection to your cluster using the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Create a virtual network

This Bicep file defines a virtual network.

```
@description('The location of the managed cluster resource.')
param location string = resourceGroup().location
@description('The name of the virtual network.')
param vnetName string = 'aksAutomaticVnet'
@description('The address prefix of the virtual network.')
param addressPrefix string = '172.19.0.0/16'
@description('The name of the API server subnet.')
param apiServerSubnetName string = 'apiServerSubnet'
@description('The subnet prefix of the API server subnet.')
param apiServerSubnetPrefix string = '172.19.0.0/28'
@description('The name of the cluster subnet.')
param clusterSubnetName string = 'clusterSubnet'
@description('The subnet prefix of the cluster subnet.')
param clusterSubnetPrefix string = '172.19.1.0/24'
// Virtual network with an API server subnet and a cluster subnet
resource virtualNetwork 'Microsoft.Network/virtualNetworks@2023-09-01' = {
name: vnetName
location: location
properties: {
addressSpace: {
addressPrefixes: [ addressPrefix ]
}
subnets: [
{
name: apiServerSubnetName
properties: {
addressPrefix: apiServerSubnetPrefix
}
}
{
name: clusterSubnetName
properties: {
addressPrefix: clusterSubnetPrefix
}
}
]
}
}
output apiServerSubnetId string = resourceId('Microsoft.Network/virtualNetworks/subnets', vnetName, apiServerSubnetName)
output clusterSubnetId string = resourceId('Microsoft.Network/virtualNetworks/subnets', vnetName, clusterSubnetName)
```


Save the Bicep file **virtualNetwork.bicep** to your local computer.

Important

The Bicep file sets the `vnetName`

param to *aksAutomaticVnet*, the `addressPrefix`

param to *172.19.0.0/16*, the `apiServerSubnetPrefix`

param to *172.19.0.0/28*, and the `apiServerSubnetPrefix`

param to *172.19.1.0/24*. If you want to use different values, make sure to update the strings to your preferred values.

Deploy the Bicep file using the Azure CLI.

```
az deployment group create --resource-group <resource-group> --template-file virtualNetwork.bicep
```


All traffic within the virtual network is allowed by default. But if you added Network Security Group (NSG) rules to restrict traffic between different subnets, ensure that the NSG security rules permit the following types of communication:

| Destination | Source | Protocol | Port | Use |
|---|---|---|---|---|
| APIServer Subnet CIDR | Cluster Subnet | TCP | 443 and 4443 | Required to enable communication between Nodes and the API server. |
| APIServer Subnet CIDR | Azure Load Balancer | TCP | 9988 | Required to enable communication between Azure Load Balancer and the API server. You can also enable all communication between the Azure Load Balancer and the API Server Subnet CIDR. |

## Create a managed identity

This Bicep file defines a user assigned managed identity.

```
param location string = resourceGroup().location
param uamiName string = 'aksAutomaticUAMI'
resource userAssignedManagedIdentity 'Microsoft.ManagedIdentity/userAssignedIdentities@2023-01-31' = {
name: uamiName
location: location
}
output uamiId string = userAssignedManagedIdentity.id
output uamiPrincipalId string = userAssignedManagedIdentity.properties.principalId
output uamiClientId string = userAssignedManagedIdentity.properties.clientId
```


Save the Bicep file **uami.bicep** to your local computer.

Important

The Bicep file sets the `uamiName`

param to the *aksAutomaticUAMI*. If you want to use a different identity name, make sure to update the string to your preferred name.

Deploy the Bicep file using the Azure CLI.

```
az deployment group create --resource-group <resource-group> --template-file uami.bicep
```


## Assign the Network Contributor role over the virtual network

This Bicep file defines role assignments over the virtual network.

```
@description('The name of the virtual network.')
param vnetName string = 'aksAutomaticVnet'
@description('The principal ID of the user assigned managed identity.')
param uamiPrincipalId string
// Get a reference to the virtual network
resource virtualNetwork 'Microsoft.Network/virtualNetworks@2023-09-01' existing ={
name: vnetName
}
// Assign the Network Contributor role to the user assigned managed identity on the virtual network
// '4d97b98b-1d4f-4787-a291-c67834d212e7' is the built-in Network Contributor role definition
// See: https://learn.microsoft.com/en-us/azure/role-based-access-control/built-in-roles/networking#network-contributor
resource networkContributorRoleAssignmentToVirtualNetwork 'Microsoft.Authorization/roleAssignments@2022-04-01' = {
name: guid(uamiPrincipalId, '4d97b98b-1d4f-4787-a291-c67834d212e7', resourceGroup().id, virtualNetwork.name)
scope: virtualNetwork
properties: {
roleDefinitionId: resourceId('Microsoft.Authorization/roleDefinitions', '4d97b98b-1d4f-4787-a291-c67834d212e7')
principalId: uamiPrincipalId
}
}
```


Save the Bicep file **roleAssignments.bicep** to your local computer.

Important

The Bicep file sets the `vnetName`

param to *aksAutomaticVnet*. If you used a different virtual network name, make sure to update the string to your preferred virtual network name.

Deploy the Bicep file using the Azure CLI. You need to provide the user assigned identity principal ID.

```
az deployment group create --resource-group <resource-group> --template-file roleAssignments.bicep \
--parameters uamiPrincipalId=<user assigned identity prinicipal id>
```


## Create a private AKS Automatic cluster in a custom virtual network

This Bicep file defines the AKS Automatic cluster.

Note

You can refer to the [private cluster](../private-clusters) documentation for configuring additional options like disabling the clusters public FQDN and configuring the private DNS zone.

```
@description('The name of the managed cluster resource.')
param clusterName string = 'aksAutomaticCluster'
@description('The location of the managed cluster resource.')
param location string = resourceGroup().location
@description('The resource ID of the API server subnet.')
param apiServerSubnetId string
@description('The resource ID of the cluster subnet.')
param clusterSubnetId string
@description('The resource ID of the user assigned managed identity.')
param uamiId string
/// Create the private AKS Automatic cluster using the custom virtual network and user assigned managed identity
resource aks 'Microsoft.ContainerService/managedClusters@2024-03-02-preview' = {
name: clusterName
location: location
sku: {
name: 'Automatic'
}
properties: {
agentPoolProfiles: [
{
name: 'systempool'
mode: 'System'
count: 3
vnetSubnetID: clusterSubnetId
}
]
apiServerAccessProfile: {
subnetId: apiServerSubnetId
enablePrivateCluster: true
}
networkProfile: {
outboundType: 'loadBalancer'
}
}
identity: {
type: 'UserAssigned'
userAssignedIdentities: {
'${uamiId}': {}
}
}
}
```


Save the Bicep file **aks.bicep** to your local computer.

Important

The Bicep file sets the `clusterName`

param to *aksAutomaticCluster*. If you want a different cluster name, make sure to update the string to your preferred cluster name.

Deploy the Bicep file using the Azure CLI. You need to provide the API server subnet resource ID, the cluster subnet resource ID, and user assigned identity principal ID.

```
az deployment group create --resource-group <resource-group> --template-file aks.bicep \
--parameters apiServerSubnetId=<API server subnet resource id> \
--parameters clusterSubnetId=<cluster subnet resource id> \
--parameters uamiPrincipalId=<user assigned identity prinicipal id>
```


## Connect to the cluster

When an AKS Automatic cluster is created as a private cluster, the API server endpoint has no public IP address. To manage the API server, for example via `kubectl`

, you need to connect through a machine that has access to the cluster's Azure virtual network. There are several options for establishing network connectivity to the private cluster:

- Create a virtual machine in the same virtual network as the AKS Automatic cluster using the
command with the`az vm create`

`--vnet-name`

flag. - Use a virtual machine in a separate virtual network and set up
[virtual network peering](../private-cluster-connect#connect-using-virtual-network-vnet-peering). - Use an
[Express Route or VPN](/en-us/azure/expressroute/expressroute-about-virtual-network-gateways)connection. - Use a
[private endpoint](../private-apiserver-vnet-integration-cluster)connection.

Creating a virtual machine in the same virtual network as the AKS cluster is the easiest option. Express Route and VPNs add costs and require additional networking complexity. Virtual network peering requires you to plan your network CIDR ranges to ensure there are no overlapping ranges. Refer to [Options for connecting to the private cluster](../private-cluster-connect) for more information.

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

Important

When you create a cluster using Bicep, you need to [assign one of the built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) such as `Azure Kubernetes Service RBAC Reader`

, `Azure Kubernetes Service RBAC Writer`

, `Azure Kubernetes Service RBAC Admin`

, or `Azure Kubernetes Service RBAC Cluster Admin`

to your users, scoped to the cluster or a specific namespace, example using `az role assignment create --role "Azure Kubernetes Service RBAC Cluster Admin" --scope <AKS cluster resource id> --assignee user@contoso.com`

. Also make sure your users have the `Azure Kubernetes Service Cluster User`

built-in role to be able to do run `az aks get-credentials`

, and then get the kubeconfig of your AKS cluster using the `az aks get-credentials`

command.

Configure `kubectl`

to connect to your Kubernetes cluster using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group <resource-group> --name <cluster-name>
```


Verify the connection to your cluster using the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These containers are used here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a namespace

`aks-store-demo`

to deploy the Kubernetes resources into.`kubectl create ns aks-store-demo`

Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command into the`aks-store-demo`

namespace. The YAML file defining the deployment is on[GitHub](https://github.com/Azure-Samples/aks-store-demo).`kubectl apply -n aks-store-demo -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-ingress-quickstart.yaml`

The following sample output shows the deployments and services:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created ingress/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make sure all pods are`Running`

before proceeding. If this is the first workload you deploy, it may take a few minutes for[node auto provisioning](../node-autoprovision)to create a node pool to run the pods.`kubectl get pods -n aks-store-demo`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get ingress store-front -n aks-store-demo --watch`

The

**ADDRESS**output for the`store-front`

service initially shows empty:`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 80 12m`

Once the

**ADDRESS**changes from blank to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following sample output shows a valid public IP address assigned to the service:

`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 4.255.22.196 80 12m`

Open a web browser to the external IP address of your ingress to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges. Run the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.

```
az group delete --name <resource-group> --yes --no-wait
```


Note

The AKS cluster was created with a user-assigned managed identity. If you don't need that identity anymore, you can manually remove it.

## Next steps

In this quickstart, you deployed a private Kubernetes cluster using [AKS Automatic](../intro-aks-automatic) inside a custom virtual network and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS Automatic, continue to the introduction.
