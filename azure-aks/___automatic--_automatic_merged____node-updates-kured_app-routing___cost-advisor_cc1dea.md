---
merged_at: 2026-02-06T16:45:38.942639
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-updates-kured -->

# Apply security and kernel updates to Linux nodes in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To protect your clusters, security updates are automatically applied to Linux nodes in AKS. These updates include OS security fixes or kernel updates. Some of these updates require a node reboot to complete the process. AKS doesn't automatically reboot these Linux nodes to complete the update process.

The process to keep Windows Server nodes up to date is a little different. Windows Server nodes don't receive daily updates. Instead, you perform an AKS upgrade that deploys new nodes with the latest base Window Server image and patches. For AKS clusters that use Windows Server nodes, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

This article shows you how to use the open-source [kured (KUbernetes REboot Daemon)](https://github.com/kubereboot/kured) to watch for Linux nodes that require a reboot, then automatically handle the rescheduling of running pods and node reboot process.

Note

`Kured`

is an open-source project in the Cloud Native Computing Foundation. Please direct issues to the [kured GitHub](https://github.com/kubereboot/kured). Additional support can be found in the #kured channel on [CNCF Slack](https://slack.cncf.io).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Before you begin

You need the Azure CLI version 2.0.59 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Understand the AKS node update experience

In an AKS cluster, your Kubernetes nodes run as Azure virtual machines (VMs). These Linux-based VMs use an Ubuntu or Azure Linux image, with the OS configured to automatically check for updates every day. If security or kernel updates are available, they're automatically downloaded and installed.

Some security updates, such as kernel updates, require a node reboot to finalize the process. A Linux node that requires a reboot creates a file named */var/run/reboot-required*. This reboot process doesn't happen automatically.

You can use your own workflows and processes to handle node reboots, or use `kured`

to orchestrate the process. With `kured`

, a [DaemonSet](concepts-clusters-workloads#statefulsets-and-daemonsets) is deployed that runs a pod on each Linux node in the cluster. These pods in the DaemonSet watch for existence of the */var/run/reboot-required* file, and then initiate a process to reboot the nodes.

### Node image upgrades

Unattended upgrades apply updates to the Linux node OS, but the image used to create nodes for your cluster remains unchanged. If a new Linux node is added to your cluster, the original image is used to create the node. This new node receives all the security and kernel updates available during the automatic check every day but remains unpatched until all checks and restarts are complete.

Alternatively, you can use node image upgrade to check for and update node images used by your cluster. For more information on node image upgrade, see [Azure Kubernetes Service (AKS) node image upgrade](node-image-upgrade).

### Node upgrades

There's another process in AKS that lets you *upgrade* a cluster. An upgrade is typically to move to a newer version of Kubernetes, not just apply node security updates. An AKS upgrade performs the following actions:

- A new node is deployed with the latest security updates and Kubernetes version applied.
- An old node is cordoned and drained.
- Pods are scheduled on the new node.
- The old node is deleted.

You can't remain on the same Kubernetes version during an upgrade event. You must specify a newer version of Kubernetes. To upgrade to the latest version of Kubernetes, you can [upgrade your AKS cluster](upgrade-cluster).

## Deploy kured in an AKS cluster

To deploy the `kured`

DaemonSet, install the following official Kured Helm chart. This creates a role and cluster role, bindings, and a service account, then deploys the DaemonSet using `kured`

.

```
# Add the Kured Helm repository
helm repo add kubereboot https://kubereboot.github.io/charts/
# Update your local Helm chart repository cache
helm repo update
# Create a dedicated namespace where you would like to deploy kured into
kubectl create namespace kured
# Install kured in that namespace with Helm 3 (only on Linux nodes, kured is not working on Windows nodes)
helm install my-release kubereboot/kured --namespace kured --set controller.nodeSelector."kubernetes\.io/os"=linux
```


You can also configure extra parameters for `kured`

, such as integration with Prometheus or Slack. For more information about configuration parameters, see the [kured Helm chart](https://github.com/kubereboot/charts/tree/main/charts/kured).

## Update cluster nodes

By default, Linux nodes in AKS check for updates every evening. If you don't want to wait, you can manually perform an update to check that `kured`

runs correctly. First, follow the steps to [SSH to one of your AKS nodes](ssh). Once you have an SSH connection to the Linux node, check for updates and apply them as follows:

```
sudo apt-get update && sudo apt-get upgrade -y
```


If updates were applied that require a node reboot, a file is written to */var/run/reboot-required*. `Kured`

checks for nodes that require a reboot every 60 minutes by default.

## Monitor and review reboot process

When one of the replicas in the DaemonSet detects that a node reboot is required, a lock is placed on the node through the Kubernetes API. This lock prevents more pods from being scheduled on the node. The lock also indicates that only one node should be rebooted at a time. With the node cordoned off, running pods are drained from the node, and the node is rebooted.

You can monitor the status of the nodes using the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. The following example output shows a node with a status of *SchedulingDisabled* as the node prepares for the reboot process:

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-28993262-0 Ready,SchedulingDisabled agent 1h v1.11.7
```


Once the update process is complete, you can view the status of the nodes using the [kubectl get nodes](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command with the `--output wide`

parameter. This output lets you see a difference in *KERNEL-VERSION* of the underlying nodes, as shown in the following example output. The *aks-nodepool1-28993262-0* was updated in a previous step and shows kernel version *4.15.0-1039-azure*. The node *aks-nodepool1-28993262-1* that hasn't been updated shows kernel version *4.15.0-1037-azure*.

```
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodepool1-28993262-0 Ready agent 1h v1.11.7 10.240.0.4 <none> Ubuntu 16.04.6 LTS 4.15.0-1039-azure docker://3.0.4
aks-nodepool1-28993262-1 Ready agent 1h v1.11.7 10.240.0.5 <none> Ubuntu 16.04.6 LTS 4.15.0-1037-azure docker://3.0.4
```


## Next steps

This article detailed how to use `kured`

to reboot Linux nodes automatically as part of the security update process. To upgrade to the latest version of Kubernetes, you can [upgrade your AKS cluster](upgrade-cluster).

For AKS clusters that use Windows Server nodes, see [Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing -->

# Managed NGINX ingress with the application routing add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The [Kubernetes SIG Network](https://github.com/kubernetes/community/blob/master/sig-network/README.md) and the Security Response Committee [announced the upcoming retirement](https://www.kubernetes.dev/blog/2025/11/12/ingress-nginx-retirement/) of the [Ingress NGINX project](https://github.com/kubernetes/ingress-nginx/), with maintenance ending in **March 2026**. There's no immediate action required today for AKS clusters using the [Application Routing add-on with NGINX](/en-us/azure/aks/app-routing). Microsoft will provide official support for critical security patches for Application Routing add-on NGINX Ingress resources through **November 2026**.

AKS is aligning with upstream Kubernetes by moving to ** Gateway API as the long-term standard for ingress and L7 traffic management**. We recommend you start planning your migration path based on your current setup:

**Application Routing add-on users**: Production workloads remain fully supported through November 2026. AKS will continue evolving the Application Routing add-on with Gateway API alignment. You don't need to move to a different ingress product.**OSS NGINX users**have several options:- Migrate to the
[Application Routing add-on with NGINX](/en-us/azure/aks/app-routing)to benefit from official support through November 2026 while planning your long-term Gateway API migration. - Migrate to
[Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview), which supports both Ingress API and Gateway API.

- Migrate to the
**Service mesh users**: If you plan to adopt a service mesh, consider the[Istio-based service mesh add-on](/en-us/azure/aks/istio-about). Use Istio Ingress today, and plan to migrate to Istio Gateway API support when it becomes GA.

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cost-advisors -->

# Get Azure Kubernetes Service (AKS) cost recommendations in Azure Advisor

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS cost recommendations in Azure Advisor follow AKS cost best practices and help you optimize your deployments to achieve cost-efficiency without compromising on reliability. Advisor analyzes your resource configuration and recommends solutions to optimize your AKS cluster.

With Advisor, you can:

- Get proactive, actionable, and personalized best practices recommendations.
- Identify opportunities to reduce your overall Azure spend.
- Get recommendations with proposed actions inline.

Cost is one of five categories that Advisor recommendations can fall into. Other categories include reliability, security, performance, and operational excellence. For more information, see the
[Introduction to Azure Advisor](/en-us/azure/advisor/advisor-overview).

## Prerequisites

- To access Advisor recommendations you must have one of the following roles: Owner, Contributor, or Reader of a subscription, resource group, or resource.

## AKS cost recommendations

Recommendations are available for all clusters, but only the ones relevant to the cluster configuration and historical usage will be surfaced. There is no action required by the customer to enable Azure Advisor, as it is a provided by default for all Azure services out of box.

AKS cost recommendations include the following:

- Enable Vertical Pod Autoscaler recommendation mode to rightsize resource requests and limits.
- Use Azure Kubernetes Service Cost Analysis.
- Fine-tune the cluster autoscaler profile for rapid scale down and cost savings.

For more information, see [Cost recommendations](/en-us/azure/advisor/advisor-reference-cost-recommendations#azure-kubernetes-service).

### Enable Vertical Pod Autoscaler recommendation mode to rightsize resource requests and limits

Setting the correct request and limit values is difficult given the required amount of resources can vary greatly across workloads. Managing this at scale across hundreds or thousands of pods is an even greater challenge. Vertical Pod Autoscaler (VPA) automatically adjusts CPU and memory requests and limits for your pods based on historical workload usage patterns to improve resource utilization.

If you don't want VPA to automatically adjust the values and want additional control, VPA recommendation only mode provides suggested values without making automatic changes. This enables you to review and implement suggested values manually, which can prevent potential disruptions and ensure better control over resource allocation. VPA recommendation mode is a great option to help prevent over-provisioning, a major driver of unnecessary spend.

For more information, see [Vertical pod autoscaling in Azure Kubernetes Service (AKS)](vertical-pod-autoscaler#vpa-overview).

### Use Azure Kubernetes Service cost analysis

AKS cost analysis add-on provides detailed insights into the cost of resources used by your AKS cluster. View costs broken down by Kubernetes constructs like clusters and namespaces. This feature helps you identify cost drivers, track historical trends, identify anomalies and clusters or workloads with optimization opportunities. Having cost monitoring in place is an easy way to get visibility into cluster spend and take action to achieve significant cost savings.

Note

This recommendation is only available for public cloud clusters running in Enterprise or MCA type subscriptions.

For more information, see [Azure Kubernetes Service (AKS) cost analysis](cost-analysis).

### Fine-tune the cluster autoscaler profile for rapid scale down and cost savings

The cluster autoscaler profile is a set of parameters that control the behavior of the cluster autoscaler, which automatically adjusts the number of nodes in a cluster based on workload demand. Tuning these settings allows greater control over autoscaler behavior to optimize resource allocation for specific scenarios. A rapid scale down configuration means more aggressive node scale, which means less idle node costs.

For more information, see [Use the cluster autoscaler in Azure Kubernetes Service (AKS)](cluster-autoscaler#configure-cluster-autoscaler-profile-for-aggressive-scale-down).

## View the Advisor dashboard

You can view recommendations on the Advisor dashboard in Azure portal. For more information, see [Azure Advisor portal basics](/en-us/azure/advisor/advisor-get-started).

## Next steps

To learn more about cost optimization in Azure Kubernetes Service (AKS), see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/virtual-nodes -->

# Create and configure an Azure Kubernetes Services (AKS) cluster to use virtual nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To rapidly scale application workloads in an AKS cluster, you can use virtual nodes. With virtual nodes, you have quick provisioning of pods, and only pay per second for their execution time. You don't need to wait for Kubernetes cluster autoscaler to deploy VM compute nodes to run more pods. Virtual nodes are only supported with Linux pods and nodes.

The virtual nodes add on for AKS is based on the open source project [Virtual Kubelet](https://github.com/virtual-kubelet/virtual-kubelet).

This article gives you an overview of the region availability and networking requirements for using virtual nodes, and the known limitations.

## Regional availability

All regions, where ACI supports VNET SKUs, are supported for virtual nodes deployments. For more information, see [Resource availability for Azure Container Instances in Azure regions](/en-us/azure/container-instances/container-instances-region-availability).

For available CPU and memory SKUs in each region, review [Azure Container Instances Resource availability for Azure Container Instances in Azure regions - Linux container groups](/en-us/azure/container-instances/container-instances-region-availability#linux-container-groups)

## Network requirements

Virtual nodes enable network communication between pods that run in Azure Container Instances (ACI) and the AKS cluster. To support this communication, a virtual network subnet is created and delegated permissions are assigned. Virtual nodes only work with AKS clusters created using *advanced* networking (Azure CNI). By default, AKS clusters are created with *basic* networking (kubenet).

Pods running in Azure Container Instances (ACI) need access to the AKS API server endpoint, in order to configure networking.

## Limitations

Virtual nodes functionality is heavily dependent on ACI's feature set. In addition to the [quotas and limits for Azure Container Instances](/en-us/azure/container-instances/container-instances-quotas), the following are scenarios not supported with virtual nodes or are deployment considerations:

Using service principal to pull ACR images.

[Workaround](https://github.com/virtual-kubelet/azure-aci/blob/master/README.md#private-registry)is to use[Kubernetes secrets](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/#create-a-secret-by-providing-credentials-on-the-command-line).Important

Secrets built according to the Kubernetes documentation (for standard nodes) will not work with virtual nodes. A specific server format is required, as detailed in

.`ImageRegistryCredential`

- Azure Container Instances[Virtual Network Limitations](/en-us/azure/container-instances/container-instances-vnet)including VNet peering, Kubernetes network policies, and outbound traffic to the internet with network security groups.Init containers.

[Arguments](/en-us/azure/container-instances/container-instances-exec#restrictions)for exec in ACI.[DaemonSets](concepts-clusters-workloads#statefulsets-and-daemonsets)won't deploy pods to the virtual nodes.To schedule Windows Server containers to ACI, you need to manually install the open source

[Virtual Kubelet ACI](https://github.com/virtual-kubelet/azure-aci)provider.Virtual nodes require AKS clusters with Azure CNI networking.

Using API server authorized ip ranges for AKS.

Volume mounting Azure Files share support

[General-purpose V2](/en-us/azure/storage/common/storage-account-overview#types-of-storage-accounts)and[General-purpose V1](/en-us/azure/storage/common/storage-account-overview#types-of-storage-accounts). However, virtual nodes currently don't support[Persistent Volumes](concepts-storage#persistent-volumes)and[Persistent Volume Claims](concepts-storage#persistent-volume-claims). Follow the instructions for mounting[a volume with Azure Files share as an inline volume](azure-csi-files-storage-provision#mount-file-share-as-an-inline-volume).Using IPv6 isn't supported.

Attaching managed identities to virtual node is not supported.

Virtual nodes don't support the

[Container hooks](https://kubernetes.io/docs/concepts/containers/container-lifecycle-hooks/)feature.

## Next steps

Configure virtual nodes for your clusters:

[Create virtual nodes using Azure CLI](virtual-nodes-cli)[Create virtual nodes using the portal in Azure Kubernetes Services (AKS)](virtual-nodes-portal)

Virtual nodes are often one component of a scaling solution in AKS. For more information on scaling solutions, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/static-ip -->

# Use a static public IP address and DNS label with the Azure Kubernetes Service (AKS) load balancer

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a load balancer resource in an Azure Kubernetes Service (AKS) cluster, the public IP address assigned to it is only valid for the lifespan of that resource. If you delete the Kubernetes service, the associated load balancer and IP address are also deleted. If you want to assign a specific IP address or retain an IP address for redeployed Kubernetes services, you can create and use a static public IP address.

This article shows you how to create a static public IP address and assign it to your Kubernetes service.

## Before you begin

- You need the Azure CLI version 2.0.59 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - This article covers using a
*Standard*SKU IP with a*Standard*SKU load balancer. For more information, see[IP address types and allocation methods in Azure](/en-us/azure/virtual-network/ip-services/public-ip-addresses#sku).

## Create an AKS cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myNetworkResourceGroup --location eastus`

Create an AKS cluster using the

command.`az aks create`

`az aks create --name myAKSCluster --resource-group myNetworkResourceGroup --generate-ssh-keys`


## Create a static IP address

Get the name of the node resource group using the

command and query for the`az aks show`

`nodeResourceGroup`

property.`az aks show --name myAKSCluster --resource-group myNetworkResourceGroup --query nodeResourceGroup -o tsv`

Create a static public IP address in the node resource group using the

command.`az network public ip create`

`az network public-ip create \ --resource-group <node resource group name> \ --name myAKSPublicIP \ --sku Standard \ --allocation-method static`

Note

If you're using a

*Basic*SKU load balancer in your AKS cluster, use*Basic*for the`--sku`

parameter when defining a public IP. Only*Basic*SKU IPs work with the*Basic*SKU load balancer and only*Standard*SKU IPs work with*Standard*SKU load balancers.Get the static public IP address using the

command. Specify the name of the node resource group and public IP address you created, and query for the`az network public-ip list`

`ipAddress`

.`az network public-ip show --resource-group <node resource group name> --name myAKSPublicIP --query ipAddress --output tsv`


## Create a service using the static IP address

First, determine which type of managed identity your AKS cluster is using, system-assigned or user-assigned. If you're not certain, call the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the identity's*type*property.`az aks show \ --name myAKSCluster \ --resource-group myResourceGroup \ --query identity.type \ --output tsv`

If the cluster is using a managed identity, the value of the

*type*property will be either**SystemAssigned**or**UserAssigned**.If the cluster is using a service principal, the value of the

*type*property will be null. Consider upgrading your cluster to use a managed identity.If your AKS cluster uses a system-assigned managed identity, then query for the managed identity's principal ID as follows:

`# Get the principal ID for a system-assigned managed identity. CLIENT_ID=$(az aks show \ --name myAKSCluster \ --resource-group myNetworkResourceGroup \ --query identity.principalId \ --output tsv)`

If your AKS cluster uses a user-assigned managed identity, then the principal ID will be null. Query for the user-assigned managed identity's client ID instead:

`# Get the client ID for a user-assigned managed identity. CLIENT_ID=$(az aks show \ --name myAKSCluster \ --resource-group myNetworkResourceGroup \ --query identity.userAssignedIdentities.*.clientId \ --output tsv`

Assign delegated permissions for the managed identity used by the AKS cluster for the public IP's resource group by calling the

command.`az role assignment create`

`# Get the resource ID for the node resource group. RG_SCOPE=$(az group show \ --name <node resource group> \ --query id \ --output tsv) # Assign the Network Contributor role to the managed identity, # scoped to the node resource group. az role assignment create \ --assignee ${CLIENT_ID} \ --role "Network Contributor" \ --scope ${RG_SCOPE}`

Important

If you customized your outbound IP, make sure your cluster identity has permissions to both the outbound public IP and the inbound public IP.

Create a file named

`load-balancer-service.yaml`

and copy in the contents of the following YAML file, providing your own public IP address created in the previous step and the node resource group name.Important

Adding the

`loadBalancerIP`

property to the load balancer YAML manifest is deprecating following[upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235). While current usage remains the same and existing services are expected to work without modification, we**highly recommend setting service annotations**instead. To set service annotations, you can either use`service.beta.kubernetes.io/azure-pip-name`

for public IP name, or use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address, as shown in the example YAML.`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: <node resource group name> service.beta.kubernetes.io/azure-pip-name: myAKSPublicIP name: azure-load-balancer spec: type: LoadBalancer ports: - port: 80 selector: app: azure-load-balancer`

Note

Adding the

`service.beta.kubernetes.io/azure-pip-name`

annotation ensures the most efficient LoadBalancer creation and is highly recommended to avoid potential throttling.Set a public-facing DNS label to the service using the

`service.beta.kubernetes.io/azure-dns-label-name`

service annotation. This publishes a fully qualified domain name (FQDN) for your service using Azure's public DNS servers and top-level domain. The annotation value must be unique within the Azure location, so we recommend you use a sufficiently qualified label. Azure automatically appends a default suffix in the location you selected, such as`<location>.cloudapp.azure.com`

, to the name you provide, creating the FQDN.Note

If you want to publish the service on your own domain, see

[Azure DNS](https://azure.microsoft.com/services/dns/)and the[external-dns](https://github.com/kubernetes-sigs/external-dns)project.`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: <node resource group name> service.beta.kubernetes.io/azure-pip-name: myAKSPublicIP service.beta.kubernetes.io/azure-dns-label-name: <unique-service-label> name: azure-load-balancer spec: type: LoadBalancer ports: - port: 80 selector: app: azure-load-balancer`

Create the service and deployment using the

`kubectl apply`

command.`kubectl apply -f load-balancer-service.yaml`

To see the DNS label for your load balancer, use the

`kubectl describe service`

command.`kubectl describe service azure-load-balancer`

The DNS label will be listed under the

`Annotations`

, as shown in the following condensed example output:`Name: azure-load-balancer Namespace: default Labels: <none> Annotations: service.beta.kuberenetes.io/azure-dns-label-name: <unique-service-label>`


## Troubleshoot

If the static IP address defined in the `loadBalancerIP`

property of the Kubernetes service manifest doesn't exist or hasn't been created in the node resource group and there are no other delegations configured, the load balancer service creation fails. To troubleshoot, review the service creation events using the [ kubectl describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe) command. Provide the name of the service specified in the YAML manifest, as shown in the following example:

```
kubectl describe service azure-load-balancer
```


The output shows you information about the Kubernetes service resource. The following example output shows a `Warning`

in the `Events`

: "`user supplied IP address was not found`

." In this scenario, make sure you created the static public IP address in the node resource group and that the IP address specified in the Kubernetes service manifest is correct.

```
Name: azure-load-balancer
Namespace: default
Labels: <none>
Annotations: <none>
Selector: app=azure-load-balancer
Type: LoadBalancer
IP: 10.0.18.125
IP: 40.121.183.52
Port: <unset> 80/TCP
TargetPort: 80/TCP
NodePort: <unset> 32582/TCP
Endpoints: <none>
Session Affinity: None
External Traffic Policy: Cluster
Events:
Type Reason Age From Message
---- ------ ---- ---- -------
Normal CreatingLoadBalancer 7s (x2 over 22s) service-controller Creating load balancer
Warning CreatingLoadBalancerFailed 6s (x2 over 12s) service-controller Error creating load balancer (will retry): Failed to create load balancer for service default/azure-load-balancer: user supplied IP Address 40.121.183.52 was not found
```


## Next steps

For more control over the network traffic to your applications, use the application routing addon for AKS. For more information about the app routing addon, see [Managed NGINX ingress with the application routing add-on](app-routing).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-ray -->

# Configure and deploy a Ray cluster on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you configure and deploy a Ray cluster on Azure Kubernetes Service (AKS) using KubeRay. You also learn how to use the Ray cluster to train a simple machine learning model and display the results on the Ray Dashboard.

This article provides two methods to deploy the Ray cluster on AKS:

: Use the[Non-interactive deployment](#deploy-the-ray-sample-non-interactively)`deploy.sh`

script in the GitHub repository to deploy the complete Ray sample non-interactively.: Follow the manual deployment steps to deploy the Ray sample to AKS.[Manual deployment](#manually-deploy-the-ray-sample)

## Prerequisites

- Review the
[Ray cluster on AKS overview](ray-overview)to understand the components and deployment process. - An Azure subscription. If you don't have an Azure subscription, you can create a free account
[here](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The Azure CLI installed on your local machine. You can install it using the instructions in
[How to install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The
[Azure Kubernetes Service Preview extension](/en-us/azure/aks/draft#install-the-aks-preview-azure-cli-extension)installed. [Helm](https://helm.sh/docs/intro/install/)installed.[Terraform client tools](https://developer.hashicorp.com/terraform/install)or[OpenTofu](https://opentofu.org/)installed. This article uses Terraform, but the modules used should be compatible with OpenTofu.

## Deploy the Ray sample non-interactively

If you want to deploy the complete Ray sample non-interactively, you can use the `deploy.sh`

script in the GitHub repository ([https://github.com/Azure-Samples/aks-ray-sample](https://github.com/Azure-Samples/aks-ray-sample)). This script completes the steps outlined in the [Ray deployment process section](ray-overview#ray-deployment-process).

Clone the GitHub repo locally and change to the root of the repo using the following commands:

`git clone https://github.com/Azure-Samples/aks-ray-sample cd aks-ray-sample`

Deploy the complete sample using the following commands:

`chmod +x deploy.sh ./deploy.sh`

Once the deployment completes, review the output of the logs and the resource group in the Azure portal to see the infrastructure that was created.


## Manually deploy the Ray sample

Fashion MNIST is a dataset of Zalando's article images consisting of a training set of 60,000 examples and a test set of 10,000 examples. Each example is a 28x28 grayscale image associated with a label from ten classes. In this guide, you train a simple PyTorch model on this dataset using the Ray cluster.

### Deploy the RayJob specification

To train the model, you need to submit a Ray Job specification to the KubeRay operator running on a private AKS cluster. The Ray Job specification is a YAML file that describes the resources required to run the job, including the Docker image, the command to run, and the number of workers to use.

Looking at the Ray Job description, you might need to modify some fields to match your environment:

- The
`replicas`

field under the`workerGroupSpecs`

section in`rayClusterSpec`

specifies the number of worker pods that KubeRay schedules to the Kubernetes cluster. Each worker pod requires*3 CPUs*and*4 GB of memory*. The head pod requires*1 CPU*and*4 GB of memory*. Setting the`replicas`

field to*2*requires*8 vCPUs*in the node pool used to implement the RayCluster for the job. - The
`NUM_WORKERS`

field under`runtimeEnvYAML`

in`spec`

specifies the number of Ray actors to launch. Each Ray actor must be serviced by a worker pod in the Kubernetes cluster, so this field must be less than or equal to the`replicas`

field. In this example, we set`NUM_WORKERS`

to*2*, which matches the`replicas`

field. - The
`CPUS_PER_WORKER`

field must be set to*less than or equal the number of CPUs allocated to each worker pod minus 1*. In this example, the CPU resource request per worker pod is*3*, so`CPUS_PER_WORKER`

is set to*2*.

To summarize, you need a total of *8 vCPUs* in the node pool to run the PyTorch model training job. Since we added a taint on the system node pool so that no user pods can be scheduled on it, we must create a new node pool with at least *8 vCPUs* to host the Ray cluster.

Download the Ray Job specification file using the following command:

`curl -LO https://raw.githubusercontent.com/ray-project/kuberay/master/ray-operator/config/samples/pytorch-mnist/ray-job.pytorch-mnist.yaml`

Make any necessary modifications to the Ray Job specification file.

Launch the PyTorch model training job using the

`kubectl apply`

command.`kubectl apply -n kuberay -f ray-job.pytorch-mnist.yaml`


### Verify the RayJob deployment

Verify that you have two worker pods and one head pod running in the namespace using the

`kubectl get pods`

command.`kubectl get pods -n kuberay`

Your output should look similar to the following example output:

`NAME READY STATUS RESTARTS AGE kuberay-operator-7d7998bcdb-9h8hx 1/1 Running 0 3d2h pytorch-mnist-raycluster-s7xd9-worker-small-group-knpgl 1/1 Running 0 6m15s pytorch-mnist-raycluster-s7xd9-worker-small-group-p74cm 1/1 Running 0 6m15s rayjob-pytorch-mnist-fc959 1/1 Running 0 5m35s rayjob-pytorch-mnist-raycluster-s7xd9-head-l24hn 1/1 Running 0 6m15s`

Check the status of the RayJob using the

`kubectl get`

command.`kubectl get rayjob -n kuberay`

Your output should look similar to the following example output:

`NAME JOB STATUS DEPLOYMENT STATUS START TIME END TIME AGE rayjob-pytorch-mnist RUNNING Running 2024-11-22T03:08:22Z 9m36s`

Wait until the RayJob completes. This might take a few minutes. Once the

`JOB STATUS`

is`SUCCEEDED`

, you can check the training logs. You can do this by first getting the name of the pod running the RayJob using the`kubectl get pods`

command.`kubectl get pods -n kuberay`

In the output, you should see a pod with a name that starts with

`rayjob-pytorch-mnist`

, similar to the following example output:`NAME READY STATUS RESTARTS AGE kuberay-operator-7d7998bcdb-9h8hx 1/1 Running 0 3d2h pytorch-mnist-raycluster-s7xd9-worker-small-group-knpgl 1/1 Running 0 14m pytorch-mnist-raycluster-s7xd9-worker-small-group-p74cm 1/1 Running 0 14m rayjob-pytorch-mnist-fc959 0/1 Completed 0 13m rayjob-pytorch-mnist-raycluster-s7xd9-head-l24hn 1/1 Running 0 14m`

View the logs of the RayJob using the

`kubectl logs`

command. Make sure to replace`rayjob-pytorch-mnist-fc959`

with the name of the pod running your RayJob.`kubectl logs -n kuberay rayjob-pytorch-mnist-fc959`

In the output, you should see the training logs for the PyTorch model, similar to the following example output:

`2024-11-21 19:09:04,986 INFO cli.py:39 -- Job submission server address: http://rayjob-pytorch-mnist-raycluster-s7xd9-head-svc.kuberay.svc.cluster.local:8265 2024-11-21 19:09:05,712 SUCC cli.py:63 -- ------------------------------------------------------- 2024-11-21 19:09:05,713 SUCC cli.py:64 -- Job 'rayjob-pytorch-mnist-hndpx' submitted successfully 2024-11-21 19:09:05,713 SUCC cli.py:65 -- ------------------------------------------------------- 2024-11-21 19:09:05,713 INFO cli.py:289 -- Next steps 2024-11-21 19:09:05,713 INFO cli.py:290 -- Query the logs of the job: 2024-11-21 19:09:05,713 INFO cli.py:292 -- ray job logs rayjob-pytorch-mnist-hndpx 2024-11-21 19:09:05,713 INFO cli.py:294 -- Query the status of the job: ... View detailed results here: /home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23 To visualize your results with TensorBoard, run: `tensorboard --logdir /tmp/ray/session_2024-11-21_19-08-24_556164_1/artifacts/2024-11-21_19-11-24/TorchTrainer_2024-11-21_19-11-23/driver_artifacts` Training started with configuration: ╭─────────────────────────────────────────────────╮ │ Training config │ ├─────────────────────────────────────────────────┤ │ train_loop_config/batch_size_per_worker 16 │ │ train_loop_config/epochs 10 │ │ train_loop_config/lr 0.001 │ ╰─────────────────────────────────────────────────╯ (RayTrainWorker pid=1193, ip=10.244.4.193) Setting up process group for: env:// [rank=0, world_size=2] (TorchTrainer pid=1138, ip=10.244.4.193) Started distributed worker processes: (TorchTrainer pid=1138, ip=10.244.4.193) - (node_id=3ea81f12c0f73ebfbd5b46664e29ced00266e69355c699970e1d824b, ip=10.244.4.193, pid=1193) world_rank=0, local_rank=0, node_rank=0 (TorchTrainer pid=1138, ip=10.244.4.193) - (node_id=2b00ea2b369c9d27de9596ce329daad1d24626b149975cf23cd10ea3, ip=10.244.1.42, pid=1341) world_rank=1, local_rank=0, node_rank=1 (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/train-images-idx3-ubyte.gz (RayTrainWorker pid=1193, ip=10.244.4.193) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/train-images-idx3-ubyte.gz to /home/ray/data/FashionMNIST/raw/train-images-idx3-ubyte.gz (RayTrainWorker pid=1193, ip=10.244.4.193) 0%| | 0.00/26.4M [00:00<?, ?B/s] (RayTrainWorker pid=1193, ip=10.244.4.193) 0%| | 65.5k/26.4M [00:00<01:13, 356kB/s] (RayTrainWorker pid=1193, ip=10.244.4.193) 100%|██████████| 26.4M/26.4M [00:01<00:00, 18.9MB/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Extracting /home/ray/data/FashionMNIST/raw/train-images-idx3-ubyte.gz to /home/ray/data/FashionMNIST/raw (RayTrainWorker pid=1341, ip=10.244.1.42) 100%|██████████| 26.4M/26.4M [00:01<00:00, 18.7MB/s] ... Training finished iteration 1 at 2024-11-21 19:15:46. Total running time: 4min 22s ╭───────────────────────────────╮ │ Training result │ ├───────────────────────────────┤ │ checkpoint_dir_name │ │ time_this_iter_s 144.9 │ │ time_total_s 144.9 │ │ training_iteration 1 │ │ accuracy 0.805 │ │ loss 0.52336 │ ╰───────────────────────────────╯ (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 97%|█████████▋| 303/313 [00:01<00:00, 269.60it/s] Test Epoch 0: 100%|██████████| 313/313 [00:01<00:00, 267.14it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 0: 100%|██████████| 313/313 [00:01<00:00, 270.44it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 0: 100%|█████████▉| 1866/1875 [00:24<00:00, 82.49it/s] [repeated 35x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 0: 100%|██████████| 1875/1875 [00:24<00:00, 77.99it/s] Train Epoch 0: 100%|██████████| 1875/1875 [00:24<00:00, 76.19it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 0: 88%|████████▊ | 275/313 [00:01<00:00, 265.39it/s] [repeated 19x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 19%|█▉ | 354/1875 [00:04<00:18, 82.66it/s] [repeated 80x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 40%|████ | 757/1875 [00:09<00:13, 83.01it/s] [repeated 90x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 62%|██████▏ | 1164/1875 [00:14<00:08, 83.39it/s] [repeated 92x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 82%|████████▏ | 1533/1875 [00:19<00:05, 68.09it/s] [repeated 91x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 1: 91%|█████████▏| 1713/1875 [00:22<00:02, 70.20it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 91%|█████████ | 1707/1875 [00:22<00:02, 70.04it/s] [repeated 47x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 8%|▊ | 24/313 [00:00<00:01, 237.98it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 1: 96%|█████████▋| 302/313 [00:01<00:00, 250.76it/s] Test Epoch 1: 100%|██████████| 313/313 [00:01<00:00, 262.94it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 2: 0%| | 0/1875 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 92%|█████████▏| 289/313 [00:01<00:00, 222.57it/s] Training finished iteration 2 at 2024-11-21 19:16:12. Total running time: 4min 48s ╭───────────────────────────────╮ │ Training result │ ├───────────────────────────────┤ │ checkpoint_dir_name │ │ time_this_iter_s 25.975 │ │ time_total_s 170.875 │ │ training_iteration 2 │ │ accuracy 0.828 │ │ loss 0.45946 │ ╰───────────────────────────────╯ (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 100%|██████████| 313/313 [00:01<00:00, 226.04it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Train Epoch 1: 100%|██████████| 1875/1875 [00:24<00:00, 76.24it/s] [repeated 45x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 2: 13%|█▎ | 239/1875 [00:03<00:24, 67.30it/s] [repeated 64x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 1: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 1: 85%|████████▍ | 266/313 [00:01<00:00, 222.54it/s] [repeated 20x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) .. Training completed after 10 iterations at 2024-11-21 19:19:47. Total running time: 8min 23s 2024-11-21 19:19:47,596 INFO tune.py:1009 -- Wrote the latest version of all result files and experiment state to '/home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23' in 0.0029s. Training result: Result( metrics={'loss': 0.35892221605786073, 'accuracy': 0.872}, path='/home/ray/ray_results/TorchTrainer_2024-11-21_19-11-23/TorchTrainer_74867_00000_0_2024-11-21_19-11-24', filesystem='local', checkpoint=None ) (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/t10k-labels-idx1-ubyte.gz [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Downloading http://fashion-mnist.s3-website.eu-central-1.amazonaws.com/t10k-labels-idx1-ubyte.gz to /home/ray/data/FashionMNIST/raw/t10k-labels-idx1-ubyte.gz [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Extracting /home/ray/data/FashionMNIST/raw/t10k-labels-idx1-ubyte.gz to /home/ray/data/FashionMNIST/raw [repeated 7x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 9: 91%|█████████ | 1708/1875 [00:21<00:01, 83.84it/s] [repeated 23x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Train Epoch 9: 100%|██████████| 1875/1875 [00:23<00:00, 78.52it/s] [repeated 37x across cluster] (RayTrainWorker pid=1341, ip=10.244.1.42) Test Epoch 9: 0%| | 0/313 [00:00<?, ?it/s] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 9: 89%|████████▉ | 278/313 [00:01<00:00, 266.46it/s] [repeated 19x across cluster] (RayTrainWorker pid=1193, ip=10.244.4.193) Test Epoch 9: 97%|█████████▋| 305/313 [00:01<00:00, 256.69it/s] Test Epoch 9: 100%|██████████| 313/313 [00:01<00:00, 267.35it/s] 2024-11-21 19:19:51,728 SUCC cli.py:63 -- ------------------------------------------ 2024-11-21 19:19:51,728 SUCC cli.py:64 -- Job 'rayjob-pytorch-mnist-hndpx' succeeded 2024-11-21 19:19:51,728 SUCC cli.py:65 -- ------------------------------------------`


## View training results on the Ray Dashboard

When the RayJob successfully completes, you can view the training results on the Ray Dashboard. The Ray Dashboard provides real-time monitoring and visualizations of Ray clusters. You can use the Ray Dashboard to monitor the status of Ray clusters, view logs, and visualize the results of machine learning jobs.

To access the Ray Dashboard, you need to expose the Ray head service to the public internet by creating a *service shim* to expose the Ray head service on port 80 instead of port 8265.

Note

The `deploy.sh`

described in the previous section automatically exposes the Ray head service to the public internet. The following steps are included in the `deploy.sh`

script.

Get the name of the Ray head service and save it in a shell variable using the following command:

`rayclusterhead=$(kubectl get service -n $kuberay_namespace | grep 'rayjob-pytorch-mnist-raycluster' | grep 'ClusterIP' | awk '{print $1}')`

Create the service shim to expose the Ray head service on port 80 using the

`kubectl expose service`

command.`kubectl expose service $rayclusterhead \ -n $kuberay_namespace \ --port=80 \ --target-port=8265 \ --type=NodePort \ --name=ray-dash`

Create the ingress to expose the service shim using the ingress controller using the following command:

`cat <<EOF | kubectl apply -f - apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: ray-dash namespace: kuberay annotations: nginx.ingress.kubernetes.io/rewrite-target: / spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - http: paths: - backend: service: name: ray-dash port: number: 80 path: / pathType: Prefix EOF`

Get the public IP address of the ingress controller using the

`kubectl get service`

command.`kubectl get service -n app-routing-system`

In the output, you should see the public IP address of the load balancer attached to the ingress controller. Copy the public IP address and paste it into a web browser. You should see the Ray Dashboard.


## Clean up resources

To clean up the resources created in this guide, you can delete the Azure resource group that contains the AKS cluster.

## Next steps

To learn more about AI and machine learning workloads on AKS, see the following articles:

[Deploy an application that uses OpenAI on Azure Kubernetes Service (AKS)](open-ai-quickstart)[Build and deploy data and machine learning pipelines with Flyte on Azure Kubernetes Service (AKS)](use-flyte)[Deploy an AI model on Azure Kubernetes Service (AKS) with the AI toolchain operator](ai-toolchain-operator)

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Russell de Pina | Principal TPM
- Ken Kilty | Principal TPM
- Erin Schaffer | Content Developer 2
- Adrian Joian | Principal Customer Engineer
- Ryan Graham | Principal Technical Specialist

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-addon -->

# Deploy Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to install the Istio-based service mesh add-on for Azure Kubernetes Service (AKS) cluster.

For more information on Istio and the service mesh add-on, see [Istio-based service mesh add-on for Azure Kubernetes Service](istio-about).

Tip

You can use Azure Copilot to help deploy Istio to your AKS clusters in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#install-and-work-with-istio).

## Before you begin

The add-on requires Azure CLI version 2.57.0 or later installed. You can run

`az --version`

to verify version. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).To find information about which Istio add-on revisions are available in a region and their compatibility with AKS standard and LTS cluster versions, use the command

:`az aks mesh get-revisions`

`az aks mesh get-revisions --location <location> -o table`

For more information on the Istio add-on's compatibility with AKS, refer to the

[compatibility support policy](istio-support-policy#aks-compatibility).In some cases, Istio CRDs from previous installations may not be automatically cleaned up on uninstall. Ensure existing Istio CRDs are deleted:

`kubectl delete crd $(kubectl get crd -A | grep "istio.io" | awk '{print $1}')`

It is recommended to also clean up other resources from self-managed installations of Istio such as ClusterRoles, MutatingWebhookConfigurations and ValidatingWebhookConfigurations.

Note that if you choose to use any

`istioctl`

CLI commands, you will need to include a flag to point to the add-on installation of Istio:`--istioNamespace aks-istio-system`


### Set environment variables

```
export CLUSTER=<cluster-name>
export RESOURCE_GROUP=<resource-group-name>
export LOCATION=<location>
```


## Install Istio add-on

This section includes steps to install the Istio add-on during cluster creation or enable for an existing cluster using the Azure CLI. If you want to install the add-on using Bicep, see the guide for [installing an AKS cluster with the Istio service mesh add-on using Bicep](https://github.com/Azure-Samples/aks-istio-addon-bicep). To learn more about the Bicep resource definition for an AKS cluster, see [Bicep managedCluster reference](/en-us/azure/templates/microsoft.containerservice/managedclusters).

Note

If you need the `istiod`

and ingress/egress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

### Revision selection

If you enable the add-on without specifying a revision, a default supported revision is installed for you.

To specify a revision, perform the following steps.

- Use the
command to check which revisions are available for different AKS cluster versions in a region.`az aks mesh get-revisions`

- Based on the available revisions, you can include the
`--revision asm-X-Y`

(ex:`--revision asm-1-24`

) flag in the enable command you use for mesh installation.

### Install mesh during cluster creation

To install the Istio add-on when creating the cluster, use the `--enable-azure-service-mesh`

or`--enable-asm`

parameter.

```
az group create --name ${RESOURCE_GROUP} --location ${LOCATION}
az aks create \
--resource-group ${RESOURCE_GROUP} \
--name ${CLUSTER} \
--enable-asm \
--generate-ssh-keys
```


### Install mesh for existing cluster

The following example enables Istio add-on for an existing AKS cluster:

Important

You can't enable the Istio add-on on an existing cluster if an Open Service Mesh (OSM) add-on is already on your cluster. Uninstall the OSM add-on before installing the Istio add-on.
For more information, see [uninstall the OSM add-on from your AKS cluster](open-service-mesh-uninstall-add-on).
Istio add-on can only be enabled on AKS clusters of version >= 1.23.

```
az aks mesh enable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


## Verify successful installation

To verify the Istio add-on is installed on your cluster, run the following command:

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.mode'
```


Confirm the output shows `Istio`

.

Use `az aks get-credentials`

to get the credentials for your AKS cluster:

```
az aks get-credentials --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


Use `kubectl`

to verify that `istiod`

(Istio control plane) pods are running successfully:

```
kubectl get pods -n aks-istio-system
```


Confirm the `istiod`

pod has a status of `Running`

. For example:

```
NAME READY STATUS RESTARTS AGE
istiod-asm-1-24-74f7f7c46c-xfdtl 1/1 Running 0 2m
istiod-asm-1-24-74f7f7c46c-4nt2v 1/1 Running 0 2m
```


## Enable sidecar injection

To automatically install sidecar to any new pods, you need to annotate your namespaces with the revision label corresponding to the control plane revision currently installed.

If you're unsure which revision is installed, use:

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.istio.revisions'
```


Apply the revision label:

```
kubectl label namespace default istio.io/rev=asm-X-Y
```


Important

Explicit versioning matching the control plane revision (ex: `istio.io/rev=asm-1-24`

) is required.

The default `istio-injection=enabled`

label will not work and will **cause the sidecar injection to skip the namespace** for the add-on.

For manual injection of sidecar using `istioctl kube-inject`

, you need to specify extra parameters for `istioNamespace`

(`-i`

) and `revision`

(`-r`

). For example:

```
kubectl apply -f <(istioctl kube-inject -f sample.yaml -i aks-istio-system -r asm-X-Y) -n foo
```


## Trigger sidecar injection

You can either deploy the sample application provided for testing, or trigger sidecar injection for existing workloads.

### Existing applications

If you have existing applications to be added to the mesh, ensure their namespaces are labeled as in the previous step, and then restart their deployments to trigger sidecar injection:

```
kubectl rollout restart -n <namespace> <deployment name>
```


Verify that sidecar injection succeeded by ensuring all containers are ready and looking for the `istio-proxy`

container in the `kubectl describe`

output, for example:

```
kubectl describe pod -n namespace <pod name>
```


The `istio-proxy`

container is the Envoy sidecar. Your application is now part of the data plane.

### Deploy sample application

Use `kubectl apply`

to deploy the sample application on the cluster:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/platform/kube/bookinfo.yaml
```


Note

Clusters using an HTTP proxy for outbound internet access will need to set up a Service Entry. For setup instructions see [HTTP proxy support in Azure Kubernetes Service](http-proxy)

Confirm several deployments and services are created on your cluster. For example:

```
service/details created
serviceaccount/bookinfo-details created
deployment.apps/details-v1 created
service/ratings created
serviceaccount/bookinfo-ratings created
deployment.apps/ratings-v1 created
service/reviews created
serviceaccount/bookinfo-reviews created
deployment.apps/reviews-v1 created
deployment.apps/reviews-v2 created
deployment.apps/reviews-v3 created
service/productpage created
serviceaccount/bookinfo-productpage created
deployment.apps/productpage-v1 created
```


Use `kubectl get services`

to verify that the services were created successfully:

```
kubectl get services
```


Confirm the following services were deployed:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
details ClusterIP 10.0.180.193 <none> 9080/TCP 87s
kubernetes ClusterIP 10.0.0.1 <none> 443/TCP 15m
productpage ClusterIP 10.0.112.238 <none> 9080/TCP 86s
ratings ClusterIP 10.0.15.201 <none> 9080/TCP 86s
reviews ClusterIP 10.0.73.95 <none> 9080/TCP 86s
```


```
kubectl get pods
```


```
NAME READY STATUS RESTARTS AGE
details-v1-558b8b4b76-2llld 2/2 Running 0 2m41s
productpage-v1-6987489c74-lpkgl 2/2 Running 0 2m40s
ratings-v1-7dc98c7588-vzftc 2/2 Running 0 2m41s
reviews-v1-7f99cc4496-gdxfn 2/2 Running 0 2m41s
reviews-v2-7d79d5bd5d-8zzqd 2/2 Running 0 2m41s
reviews-v3-7dbcdcbc56-m8dph 2/2 Running 0 2m41s
```


Confirm that all the pods have status of `Running`

with two containers in the `READY`

column. The second container (`istio-proxy`

) added to each pod is the Envoy sidecar injected by Istio, and the other is the application container.

To test this sample application against ingress, check out [next-steps](#next-steps).

## Next steps

[Deploy external or internal ingresses for Istio service mesh add-on](istio-deploy-ingress)[Scale istiod and ingress gateway HPA](istio-scale#scaling)[Collect metrics for Istio service mesh add-on workloads in Azure Managed Prometheus](istio-metrics-managed-prometheus)[Deploy egress gateways for the Istio service mesh add-on](istio-deploy-egress)[Enable Istio CNI for Istio service mesh add-on (Preview)](istio-cni)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/configure-azure-cni-dynamic-ip-allocation -->

# Configure Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A drawback with the traditional CNI is the exhaustion of pod IP addresses as the AKS cluster grows, which results in the need to rebuild your entire cluster in a bigger subnet. The new dynamic IP allocation capability in Azure CNI solves this problem by allocating pod IPs from a subnet separate from the subnet hosting the AKS cluster.

It offers the following benefits:

**Better IP utilization**: IPs are dynamically allocated to cluster Pods from the Pod subnet. This leads to better utilization of IPs in the cluster compared to the traditional CNI solution, which does static allocation of IPs for every node.**Scalable and flexible**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pods are assigned virtual network IPs, they have direct connectivity to other cluster pod and resources in the VNet. The solution supports very large clusters without any degradation in performance.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using NSGs to filter traffic between node pools.**Kubernetes network policies**: Both the Azure Network Policies and Calico work with this new solution.

This article shows you how to use Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support in AKS.

## Prerequisites

Review the

[prerequisites](configure-azure-cni#prerequisites)for configuring basic Azure CNI networking in AKS, as the same prerequisites apply to this article.Review the

[deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS, as the same parameters apply.AKS Engine and DIY clusters aren't supported.

Azure CLI version

`2.37.0`

or later.If you have an existing cluster, you need to enable Container Insights for monitoring IP subnet usage. You can enable Container Insights using the

command, as shown in the following example:`az aks enable-addons`

`az aks enable-addons --addons monitoring --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME`


## Plan IP addressing

Planning your IP addressing is much simpler with this feature. Since the nodes and pods scale independently, their address spaces can also be planned separately. Since pod subnets can be configured to the granularity of a node pool, you can always add a new subnet when you add a node pool. The system pods in a cluster/node pool also receive IPs from the pod subnet, so this behavior needs to be accounted for.

IPs are allocated to nodes in batches of 16. Pod subnet IP allocation should be planned with a minimum of 16 IPs per node in the cluster; nodes will request 16 IPs on startup and will request another batch of 16 any time there are <8 IPs unallocated in their allotment.

The planning of IPs for Kubernetes services and Docker bridge remain unchanged.

To view and verify the NodeNetworkConfiguration (NNC) resources responsible for these IP allocations, you can run the following command:

```
kubectl get nodenetworkconfigs -n kube-system -o wide
```


## Maximum pods per node in a cluster with Pod Subnet - Dynamic IP Allocation and enhanced subnet support

The pods per node value when using Azure CNI Pod Subnet - Dynamic IP Allocation is slightly different from the traditional CNI behavior:

| CNI | Default | Configurable at deployment |
|---|---|---|
| Traditional Azure CNI | 30 | Yes (up to 250) |
| Azure CNI Pod Subnet - Dynamic IP Allocation | 250 | Yes (up to 250) |

All other guidance related to configuring the maximum pods per node remains the same.

## Deployment parameters

The [deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS are all valid, with two exceptions:

- The
**subnet**parameter now refers to the subnet related to the cluster's nodes. - An additional parameter
**pod subnet**is used to specify the subnet whose IP addresses will be dynamically allocated to pods.

## Configure Pod Subnet - Dynamic IP Allocation and enhanced subnet support - Azure CLI

Using Pod Subnet - Dynamic IP Allocation and enhanced subnet support in your cluster is similar to the default method for configuring a cluster Azure CNI. The following example walks through creating a new virtual network with a subnet for nodes and a subnet for pods, and creating a cluster that uses Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support. Be sure to replace variables such as `$subscription`

with your own values.

Create the virtual network with two subnets.

```
RESOURCE_GROUP_NAME="myResourceGroup"
VNET_NAME="myVirtualNetwork"
LOCATION="westcentralus"
SUBNET_NAME_1="nodesubnet"
SUBNET_NAME_2="podsubnet"
# Create the resource group
az group create --name $RESOURCE_GROUP_NAME --location $LOCATION
# Create our two subnet network
az network vnet create --resource-group $RESOURCE_GROUP_NAME --location $LOCATION --name $VNET_NAME --address-prefixes 10.0.0.0/8 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_1 --address-prefixes 10.240.0.0/16 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_2 --address-prefixes 10.241.0.0/16 -o none
```


Create the cluster, referencing the node subnet using `--vnet-subnet-id`

and the pod subnet using `--pod-subnet-id`

and enabling the monitoring add-on.

```
CLUSTER_NAME="myAKSCluster"
SUBSCRIPTION="aaaaaaa-aaaaa-aaaaaa-aaaa"
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--location $LOCATION \
--max-pods 250 \
--node-count 2 \
--network-plugin azure \
--vnet-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_1 \
--pod-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_2 \
--enable-addons monitoring \
--generate-ssh-keys
```


### Adding node pool

When adding node pool, reference the node subnet using `--vnet-subnet-id`

and the pod subnet using `--pod-subnet-id`

. The following example creates two new subnets that are then referenced in the creation of a new node pool:

```
SUBNET_NAME_3="node2subnet"
SUBNET_NAME_4="pod2subnet"
NODE_POOL_NAME="mynodepool"
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_3 --address-prefixes 10.242.0.0/16 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_4 --address-prefixes 10.243.0.0/16 -o none
az aks nodepool add --cluster-name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --name $NODE_POOL_NAME \
--max-pods 250 \
--node-count 2 \
--vnet-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_3 \
--pod-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_4 \
--no-wait
```


## Monitor IP subnet usage

Azure CNI provides the capability to monitor IP subnet usage. To enable IP subnet usage monitoring, follow the steps below:

### Get the YAML file

Download or grep the file named container-azm-ms-agentconfig.yaml from

[GitHub](https://raw.githubusercontent.com/microsoft/Docker-Provider/ci_prod/kubernetes/container-azm-ms-agentconfig.yaml).Find

in integrations. Set`azure_subnet_ip_usage`

`enabled`

to`true`

.Save the file.


### Get the AKS credentials

Set the variables for subscription, resource group and cluster. Consider the following as examples:

```
az account set --subscription $SUBSCRIPTION
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME
```


### Apply the config

- Open the terminal in the folder in which the downloaded
**container-azm-ms-agentconfig.yaml**file is saved. - Apply the config using the
`kubectl apply -f container-azm-ms-agentconfig.yaml`

command. This will restart the pod and after 5-10 minutes, the metrics will be visible. - View the metrics on the cluster by navigating to Workbooks on the cluster page in the Azure portal, and find the workbook named
*Subnet IP Usage*.

## Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support FAQs

**Can I assign multiple pod subnets to a cluster/node pool?**Only one subnet can be assigned to a cluster or node pool. However, multiple clusters or node pools can share a single subnet.

**Can I assign Pod subnets from a different VNet altogether?**No, the pod subnet should be from the same VNet as the cluster.

**Can some node pools in a cluster use the traditional CNI while others use the new CNI?**The entire cluster should use only one type of CNI.


## Next steps

Learn more about networking in AKS in the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/flatcar-container-linux-for-aks -->

# Use Flatcar Container Linux for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of Flatcar Container Linux for AKS, a Cloud Native Compute Foundation (CNCF) project that provides security, reliability, and cross-cloud capabilities. Flatcar Container Linux is available in preview as an OS option on AKS. You can deploy Flatcar Container Linux node pools in a new AKS cluster or add Flatcar Container Linux node pools to your existing clusters. To learn more about Flatcar Container Linux, see the [Flatcar documentation](https://www.flatcar.org/).

## Flatcar Container Linux for AKS benefits

Flatcar uses an immutable OS filesystem, and it eliminates configuration drift and prevents unauthorized changes, ensuring robust protection for your workloads across multiple cloud platforms. Designed for versatility, Flatcar enables cross-cloud deployment, empowering businesses to scale effortlessly and securely.

## Limitations

Flatcar Container Linux for AKS has the following limitations:

[FIPS](enable-fips-nodes)isn't supported with Flatcar Container Linux.[Trusted Launch](use-trusted-launch)isn't supported with Flatcar Container Linux.[Confidential VM sizes](use-cvm)aren't supported with Flatcar Container Linux.- The
`SecurityPatch`

[node OS upgrade channel](auto-upgrade-node-os-image)isn't supported with Flatcar Container Linux. - During preview, AKS doesn't support in-place updates with Flatcar Container Linux.
[Artifact Streaming](artifact-streaming)(preview) isn't supported with Flatcar Container Linux.[Generation 1 VMs](aks-virtual-machine-sizes)aren't supported with Flatcar Container Linux, which means you can't use VM sizes that only support Generation 1.[Pod Sandboxing (preview)](use-pod-sandboxing)isn't supported with Flatcar Container Linux.[Node auto-provisioning](node-autoprovision)isn't supported with Flatcar Container Linux.[Azure Monitor VM(SS) extension](/en-us/azure/azure-monitor/agents/azure-monitor-agent-manage?tabs=azure-portal#:%7E:text=Virtual%20machine%20(VM)%20extension)isn't supported.

Note

If you have an existing cluster with any of the above features enabled, you might not be able to add a node pool using Flatcar Container Linux.

## Get started with Flatcar Container Linux for AKS

To get started using the Flatcar Container Linux for AKS, see the following resources:

- Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using
[Azure CLI](learn/quick-flatcar-deploy-cli) - Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using an
[ARM template](learn/quick-flatcar-deploy-arm-template) - Create an AKS cluster with a single Flatcar Container Linux for AKS (preview) node pool using
[Azure CLI or an ARM template](create-node-pools) - Add a Flatcar Container Linux for AKS (preview) node pool to an existing cluster using
[Azure CLI or an ARM template](create-node-pools)

## OS migrations and upgrades with Flatcar Container Linux

AKS doesn't support in-place migrations from existing Linux clusters or node pools to Flatcar Container Linux clusters or node pools. To migrate existing workloads to Flatcar Container Linux for AKS, you need to recreate your node pools using `--os-sku flatcar`

.

Flatcar Container Linux for AKS releases weekly AKS node images. Versioning follows the AKS date-based format (for example: 202506.13.0). You can check the node images in the release notes and by using the [ az aks nodepool list](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-list) command to view the

`nodeImageVersion`

. For example:```
az aks nodepool list --resource-group <resource-group-name> --cluster-name <aks-cluster-name> --query '[].{name: name, nodeImageVersion: nodeImageVersion}'
```


Example output:

```
[
{
"name": "nodes",
"nodeImageVersion": "AKSFlatcar-flatcargen2-202508.06.0"
}
]
```


You can check the Flatcar version number (for example: Flatcar 4372.0.1) in the release notes and by using `kubectl get nodes`

command. For example:

```
kubectl get nodes -o wide
```


Example output:

```
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodes-16363508-vmss000000 Ready <none> 2m33s v1.32.6 10.224.0.4 <none> Flatcar Container Linux by Kinvolk 4372.0.1 (Oklo) 6.12.35-flatcar containerd://2.0.4
```


Flatcar's inbuilt automatic A/B update for the OS partition is disabled and only full node image updates are supported.

## Next steps

To learn more about Flatcar Container Linux, see the [Flatcar documentation](https://www.flatcar.org/).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kms-observability -->

# Observability for Azure Kubernetes Service (AKS) clusters with Key Management Service (KMS) etcd encryption (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to view observability metrics and improve observability for AKS clusters with KMS etcd encryption.

## Prerequisites

- An AKS cluster with KMS etcd encryption enabled. For more information, see
[Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster](use-kms-etcd-encryption). - You must enable
[diagnostic settings for the key vault to check the encryption logs](/en-us/azure/key-vault/general/howto-logging).

## Check the KMS config

Get the KMS config using the

command.`az aks show`

`az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query "securityProfile.azureKeyVaultKms"`

The output looks similar to the following example output:

`... "securityProfile": { "azureKeyVaultKms": { "enabled": true, "keyId": "https://<key-vault-name>.vault.azure.net/keys/<key-name>/<key-id>", "keyVaultNetworkAccess": "Public", "keyVaultResourceId": <key-vault-resource-id> ...`


## Diagnose and solve problems

Because the KMS plugin is a sidecar of `kube-apiserver`

pod, you can't access it directly. To improve the observability of KMS, you can check the KMS status using the Azure portal.

- In the Azure portal, navigate to your AKS cluster.
- From the service menu, select
**Diagnose and solve problems**. - In the search bar, search for
**KMS**and select**Azure KeyVault KMS Integration Issues**.

### Example problem

Let's say you see the following issue: `KeyExpired: Operation encrypt isn't allowed on an expired key`

.

Because the AKS KMS plugin currently only allows bring your own (BYO) key vault and key, it's your responsibility to manage the key lifecycle. If the key is expired, the KMS plugin fails to decrypt the existing secrets. To resolve this issue, you need to *extend the key expiration date* to make KMS work and *rotate the key version*.

## Next steps

For more information on using KMS with AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-extension-attach-azure-container-registry -->

# Attach to Azure Container Registry (ACR) using the Azure Kubernetes Service (AKS) extension for Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to attach to Azure Container Registry (ACR) using the Azure Kubernetes Service (AKS) extension for Visual Studio Code.

## Prerequisites

Before you begin, make sure you have the following resources:

- An Azure container registry. If you don't have one, create one using the steps in
[Quickstart: Create a private container registry](/en-us/azure/container-registry/container-registry-get-started-azure-cli). - An AKS cluster. If you don't have one, create one using the steps in
[Quickstart: Deploy an AKS cluster](learn/quick-kubernetes-deploy-cli). - The Azure Kubernetes Service (AKS) extension for Visual Studio Code downloaded. For more information, see
[Install the Azure Kubernetes Service (AKS) extension for Visual Studio Code](aks-extension-vs-code#installation).

## Attach your Azure container registry to your AKS cluster

You can access the screen for attaching your container registry to your AKS cluster using the command palette or the Kubernetes view.

On your keyboard, press

`Ctrl+Shift+P`

to open the command palette.Enter the following information:

**Subscription**: Select the Azure subscription that holds your resources.**ACR Resource Group**: Select the resource group for your container registry.**Container Registry**: Select the container registry you want to attach to your cluster.**Cluster Resource Group**: Select the resource group for your cluster.**Cluster**: Select the cluster you want to attach to your container registry.

Select

**Attach**.You should see a green checkmark, which means your container registry is attached to your AKS cluster.


For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Product support and feedback

If you have a question or want to offer product feedback, please open an issue on the [AKS extension GitHub repository](https://github.com/Azure/vscode-aks-tools/issues/new/choose).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations for AKS](integrations).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-upgrade-cluster -->

# Tutorial - Upgrade an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As part of the application and cluster lifecycle, you might want to upgrade to the latest available version of Kubernetes. You can upgrade your Azure Kubernetes Service (AKS) cluster using the Azure CLI, Azure PowerShell, or the Azure portal.

In this tutorial, you upgrade an AKS cluster. You learn how to:

- Identify current and available Kubernetes versions.
- Upgrade your Kubernetes nodes.
- Validate a successful upgrade.

## Before you begin

In previous tutorials, you packaged an application into a container image and uploaded the container image to Azure Container Registry (ACR). You also created an AKS cluster and deployed an application to it. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

If using Azure CLI, this tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

If using Azure PowerShell, this tutorial requires Azure PowerShell version 5.9.0 or later. Run `Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see [Install Azure PowerShell](/en-us/powershell/azure/install-az-ps).

## Get available cluster versions

Before you upgrade, check which Kubernetes releases are available for your cluster using the

command.`az aks get-upgrades`

`az aks get-upgrades --resource-group myResourceGroup --name myAKSCluster`

The following example output shows the current version as

*1.28.9*and lists the available versions under`upgrades`

:`{ "agentPoolProfiles": null, "controlPlaneProfile": { "kubernetesVersion": "1.28.9", ... "upgrades": [ { "isPreview": null, "kubernetesVersion": "1.29.4" }, { "isPreview": null, "kubernetesVersion": "1.29.2" } ] }, ... }`


## Upgrade an AKS cluster

AKS nodes are carefully cordoned and drained to minimize any potential disruptions to running applications. During this process, AKS performs the following steps:

- Adds a new buffer node (or as many nodes as configured in
[max surge](upgrade-aks-cluster#customize-node-surge-upgrade)) to the cluster that runs the specified Kubernetes version. [Cordons and drains](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)one of the old nodes to minimize disruption to running applications. If you're using max surge, it[cordons and drains](https://kubernetes.io/docs/tasks/administer-cluster/safely-drain-node/)as many nodes at the same time as the number of buffer nodes specified.- When the old node is fully drained, it's reimaged to receive the new version and becomes the buffer node for the following node to be upgraded.
- This process repeats until all nodes in the cluster have been upgraded.
- At the end of the process, the last buffer node is deleted, maintaining the existing agent node count and zone balance.

Note

If no patch is specified, the cluster automatically upgrades to the specified minor version's latest GA patch. For example, setting `--kubernetes-version`

to `1.28`

results in the cluster upgrading to `1.28.9`

.

For more information, see [Supported Kubernetes minor version upgrades in AKS](supported-kubernetes-versions#alias-minor-version).

You can either [manually upgrade your cluster](#manually-upgrade-cluster) or [configure automatic cluster upgrades](#configure-automatic-cluster-upgrades). **We recommend you configure automatic cluster upgrades to ensure your cluster is always running the latest version of Kubernetes**.

### Manually upgrade cluster

Upgrade your cluster using the

command.`az aks upgrade`

`az aks upgrade \ --resource-group myResourceGroup \ --name myAKSCluster \ --kubernetes-version KUBERNETES_VERSION`

You will be prompted to confirm the upgrade operation, and to confirm that you want to upgrade the control plane

*and*all the node pools to the selected version of Kubernetes:`Are you sure you want to perform this operation? (y/N): y Since control-plane-only argument is not specified, this will upgrade the control plane AND all nodepools to version 1.29.2. Continue? (y/N): y`

Note

You can only upgrade one minor version at a time. For example, you can upgrade from

*1.14.x*to*1.15.x*, but you can't upgrade from*1.14.x*to*1.16.x*directly. To upgrade from*1.14.x*to*1.16.x*, you must first upgrade from*1.14.x*to*1.15.x*, then perform another upgrade from*1.15.x*to*1.16.x*.The following example output shows the result of upgrading to

*1.29.2*. Notice the`kubernetesVersion`

now shows*1.29.2*:`{ ... "agentPoolProfiles": [ { ... "count": 3, "currentOrchestratorVersion": "1.29.2", "maxPods": 110, "name": "nodepool1", "nodeImageVersion": "AKSUbuntu-2204gen2containerd-202405.27.0", "orchestratorVersion": "1.29.2", "osType": "Linux", "upgradeSettings": { "drainTimeoutInMinutes": null, "maxSurge": "10%", "nodeSoakDurationInMinutes": null, "undrainableNodeBehavior": null }, "vmSize": "Standard_DS2_v2", ... } ], ... "currentKubernetesVersion": "1.29.2", "dnsPrefix": "myAKSClust-myResourceGroup-19da35", "enableRbac": false, "fqdn": "myaksclust-myresourcegroup-19da35-bd54a4be.hcp.westus2.azmk8s.io", "id": "/subscriptions/<Subscription ID>/resourcegroups/myResourceGroup/providers/Microsoft.ContainerService/managedClusters/myAKSCluster", "kubernetesVersion": "1.29.2", "location": "westus2", "name": "myAKSCluster", "type": "Microsoft.ContainerService/ManagedClusters" ... }`


### Configure automatic cluster upgrades

Set an auto-upgrade channel on your cluster using the

command with the`az aks update`

`--auto-upgrade-channel`

parameter set to`patch`

.`az aks update --resource-group myResourceGroup --name myAKSCluster --auto-upgrade-channel patch`


For more information, see [Automatically upgrade an Azure Kubernetes Service (AKS) cluster](auto-upgrade-cluster).

#### Upgrade AKS node images

AKS regularly provides new node images. Linux node images are updated weekly, and Windows node images are updated monthly. We recommend upgrading your node images frequently to use the latest AKS features and security updates. For more information, see [Upgrade node images in Azure Kubernetes Service (AKS)](node-image-upgrade). To configure automatic node image upgrades, see [Automatically upgrade Azure Kubernetes Service (AKS) cluster node operating system images](auto-upgrade-node-image).

## View the upgrade events

Note

When you upgrade your cluster, the following Kubernetes events might occur on the nodes:

**Surge**: Create a surge node.**Drain**: Evict pods from the node. Each pod has a*five minute timeout*to complete the eviction.**Update**: Update of a node has succeeded or failed.**Delete**: Delete a surge node.

View the upgrade events in the default namespaces using the

`kubectl get events`

command.`kubectl get events --field-selector source=upgrader`

The following example output shows some of the above events listed during an upgrade:

`LAST SEEN TYPE REASON OBJECT MESSAGE ... 5m Normal Drain node/aks-nodepool1-96663640-vmss000000 Draining node: aks-nodepool1-96663640-vmss000000 5m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Deleting node aks-nodepool1-96663640-vmss000000 from API server 4m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Successfully reimaged node: aks-nodepool1-96663640-vmss000000 4m Normal Upgrade node/aks-nodepool1-96663640-vmss000000 Successfully upgraded node: aks-nodepool1-96663640-vmss000000 4m Normal Drain node/aks-nodepool1-96663640-vmss000000 Draining node: aks-nodepool1-96663640-vmss000000 ...`


## Validate an upgrade

Confirm the upgrade was successful using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myAKSCluster --output table`

The following example output shows the AKS cluster runs

*KubernetesVersion 1.27.3*:`Name Location ResourceGroup KubernetesVersion CurrentKubernetesVersion ProvisioningState Fqdn ------------ ---------- --------------- ------------------- ------------------------ ------------------- ---------------------------------------------------------------- myAKSCluster westus2 myResourceGroup 1.29.2 1.29.2 Succeeded myaksclust-myresourcegroup-19da35-bd54a4be.hcp.westus2.azmk8s.io`


## Delete the cluster

As this tutorial is the last part of the series, you might want to delete your AKS cluster to avoid incurring Azure charges.

Remove the resource group, container service, and all related resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


Note

When you delete the cluster, the Microsoft Entra service principal used by the AKS cluster isn't removed. For steps on how to remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal). If you used a managed identity, the identity is managed by the platform and doesn't require that you provision or rotate any secrets.

## Next steps

In this tutorial, you upgraded Kubernetes in an AKS cluster. You learned how to:

- Identify current and available Kubernetes versions.
- Upgrade your Kubernetes nodes.
- Validate a successful upgrade.

For more information on AKS, see the [AKS overview](intro-kubernetes). For guidance on how to create full solutions with AKS, see the [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?WT.mc_id=AKSDOCSPAGE).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-azure-ad -->

# Enable AKS-managed Microsoft Entra integration for Kubernetes clusters with kubelogin

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The AKS-managed Microsoft Entra integration simplifies the Microsoft Entra integration process. Previously, you were required to create a client and server app, and the Microsoft Entra tenant had to assign [Directory Readers](/en-us/entra/identity/role-based-access-control/permissions-reference#directory-readers) role permissions. Now, the Azure Kubernetes Service (AKS) resource provider manages the client and server apps for you.

Cluster administrators can configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership. Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/entra/identity-platform/v2-protocols-oidc).

Learn more about the Microsoft Entra integration flow in the [Microsoft Entra documentation](concepts-identity#azure-ad-integration).

## Limitations

The following are constraints to integrate authentication on AKS:

- Integration can't be disabled after being added.
- Downgrades from an integrated cluster to the legacy Microsoft Entra ID clusters aren't supported.
- Clusters without Kubernetes RBAC support are unable to add the integration.

## Before you begin

To install the AKS addon, verify you have the following items:

- You have Azure CLI version 2.29.0 or later installed and configured. To find the version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

with a minimum version of[1.18.1](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1181)or. With the Azure CLI and the Azure PowerShell module, these two commands are included and automatically managed. Meaning, they're upgraded by default and running`kubelogin`

`az aks install-cli`

isn't required or recommended. If you're using an automated pipeline, you need to manage upgrades for the correct or latest version. The difference between the minor versions of Kubernetes and`kubectl`

shouldn't be more than*one*version. Otherwise, authentication issues occur on the wrong version. - If you're using
[helm](https://github.com/helm/helm), you need a minimum version of helm 3.3. - This configuration requires you have a Microsoft Entra group for your cluster. This group is registered as an admin group on the cluster to grant admin permissions. If you don't have an existing Microsoft Entra group, you can create one using the
command.`az ad group create`


Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution

`PATH`

. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded `kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.## Enable the integration on your AKS cluster

### Create a new cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create an AKS cluster and enable administration access for your Microsoft Entra group using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-aad \ --aad-admin-group-object-ids <id> \ --aad-tenant-id <id> \ --generate-ssh-keys`

A successful creation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body.

`"AADProfile": { "adminGroupObjectIds": [ "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb" ], "clientAppId": null, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee" }`


### Use an existing cluster

Enable AKS-managed Microsoft Entra integration on your existing Kubernetes RBAC enabled cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. Make sure to set your admin group to keep access on your cluster.

```
az aks update \
--resource-group MyResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id-1>,<id-2> \
--aad-tenant-id <id>
```


A successful activation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


### Migrate legacy cluster to integration

If your cluster uses legacy Microsoft Entra integration, you can upgrade to AKS-managed Microsoft Entra integration through the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

Warning

Free tier clusters might experience API server downtime during the upgrade. We recommend upgrading during your nonbusiness hours.
After the upgrade, the `kubeconfig`

content changes. You need to run `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

to merge the new credentials into the `kubeconfig`

file.

```
az aks update \
--resource-group myResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id> \
--aad-tenant-id <id>
```


A successful migration of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


## Access your enabled cluster

Get the user credentials to access your cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myManagedCluster`

Follow your sign in instructions.

Set

`kubelogin`

to use the Azure CLI.`kubelogin convert-kubeconfig -l azurecli`

View the nodes in the cluster with the

`kubectl get nodes`

command.`kubectl get nodes`


## Non-interactive sign-in with kubelogin

There are some non-interactive scenarios that don't support `kubectl`

. In these cases, use [ kubelogin](https://github.com/Azure/kubelogin) to connect to the cluster with a non-interactive service principal credential to perform continuous integration pipelines.

Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution PATH. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded

`kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.When getting the `clusterUser`

credential, you can use the `format`

query parameter to overwrite the default behavior. You can set the value to `azure`

to use the original `kubeconfig`

format:

```
az aks get-credentials --format azure
```


If your Microsoft Entra integrated cluster uses Kubernetes version 1.24 or lower, you need to manually convert the `kubeconfig`

format.

```
export KUBECONFIG=/path/to/kubeconfig
kubelogin convert-kubeconfig
```


If you receive the message **error: The Azure auth plugin has been removed.**, you need to run the command `kubelogin convert-kubeconfig`

to convert the `kubeconfig`

format manually. For more information, see [Azure Kubelogin Known Issues](https://azure.github.io/kubelogin/known-issues.html).

## Troubleshoot access issues

Important

The step described in this section suggests an alternative authentication method compared to the normal Microsoft Entra group authentication. Use this option only in an emergency.

If you lack administrative access to a valid Microsoft Entra group, you can follow this workaround. Sign in with an account that is a member of the [Azure Kubernetes Service Cluster Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) role and grant your group or tenant admin credentials to access your cluster.

## Next steps

- Learn about
[Microsoft Entra integration with Kubernetes RBAC](azure-ad-rbac). - Learn more about
[AKS and Kubernetes identity concepts](concepts-identity). - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS. - Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create AKS-managed Microsoft Entra ID enabled clusters.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/enable-authentication-microsoft-entra-id -->

# Enable AKS-managed Microsoft Entra integration for Kubernetes clusters with kubelogin

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The AKS-managed Microsoft Entra integration simplifies the Microsoft Entra integration process. Previously, you were required to create a client and server app, and the Microsoft Entra tenant had to assign [Directory Readers](/en-us/entra/identity/role-based-access-control/permissions-reference#directory-readers) role permissions. Now, the Azure Kubernetes Service (AKS) resource provider manages the client and server apps for you.

Cluster administrators can configure Kubernetes role-based access control (Kubernetes RBAC) based on a user's identity or directory group membership. Microsoft Entra authentication is provided to AKS clusters with OpenID Connect. OpenID Connect is an identity layer built on top of the OAuth 2.0 protocol. For more information on OpenID Connect, see the [OpenID Connect documentation](/en-us/entra/identity-platform/v2-protocols-oidc).

Learn more about the Microsoft Entra integration flow in the [Microsoft Entra documentation](concepts-identity#azure-ad-integration).

## Limitations

The following are constraints to integrate authentication on AKS:

- Integration can't be disabled after being added.
- Downgrades from an integrated cluster to the legacy Microsoft Entra ID clusters aren't supported.
- Clusters without Kubernetes RBAC support are unable to add the integration.

## Before you begin

To install the AKS addon, verify you have the following items:

- You have Azure CLI version 2.29.0 or later installed and configured. To find the version, run the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

with a minimum version of[1.18.1](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1181)or. With the Azure CLI and the Azure PowerShell module, these two commands are included and automatically managed. Meaning, they're upgraded by default and running`kubelogin`

`az aks install-cli`

isn't required or recommended. If you're using an automated pipeline, you need to manage upgrades for the correct or latest version. The difference between the minor versions of Kubernetes and`kubectl`

shouldn't be more than*one*version. Otherwise, authentication issues occur on the wrong version. - If you're using
[helm](https://github.com/helm/helm), you need a minimum version of helm 3.3. - This configuration requires you have a Microsoft Entra group for your cluster. This group is registered as an admin group on the cluster to grant admin permissions. If you don't have an existing Microsoft Entra group, you can create one using the
command.`az ad group create`


Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution

`PATH`

. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded `kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.## Enable the integration on your AKS cluster

### Create a new cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create an AKS cluster and enable administration access for your Microsoft Entra group using the

command.`az aks create`

`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-aad \ --aad-admin-group-object-ids <id> \ --aad-tenant-id <id> \ --generate-ssh-keys`

A successful creation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body.

`"AADProfile": { "adminGroupObjectIds": [ "aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb" ], "clientAppId": null, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee" }`


### Use an existing cluster

Enable AKS-managed Microsoft Entra integration on your existing Kubernetes RBAC enabled cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. Make sure to set your admin group to keep access on your cluster.

```
az aks update \
--resource-group MyResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id-1>,<id-2> \
--aad-tenant-id <id>
```


A successful activation of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


### Migrate legacy cluster to integration

If your cluster uses legacy Microsoft Entra integration, you can upgrade to AKS-managed Microsoft Entra integration through the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

Warning

Free tier clusters might experience API server downtime during the upgrade. We recommend upgrading during your nonbusiness hours.
After the upgrade, the `kubeconfig`

content changes. You need to run `az aks get-credentials --resource-group <AKS resource group name> --name <AKS cluster name>`

to merge the new credentials into the `kubeconfig`

file.

```
az aks update \
--resource-group myResourceGroup \
--name myManagedCluster \
--enable-aad \
--aad-admin-group-object-ids <id> \
--aad-tenant-id <id>
```


A successful migration of an AKS-managed Microsoft Entra ID cluster has the following section in the response body:

```
"AADProfile": {
"adminGroupObjectIds": [
"aaaaaaaa-0000-1111-2222-bbbbbbbbbbbb"
],
"clientAppId": null,
"managed": true,
"serverAppId": null,
"serverAppSecret": null,
"tenantId": "aaaabbbb-0000-cccc-1111-dddd2222eeee"
}
```


## Access your enabled cluster

Get the user credentials to access your cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myManagedCluster`

Follow your sign in instructions.

Set

`kubelogin`

to use the Azure CLI.`kubelogin convert-kubeconfig -l azurecli`

View the nodes in the cluster with the

`kubectl get nodes`

command.`kubectl get nodes`


## Non-interactive sign-in with kubelogin

There are some non-interactive scenarios that don't support `kubectl`

. In these cases, use [ kubelogin](https://github.com/Azure/kubelogin) to connect to the cluster with a non-interactive service principal credential to perform continuous integration pipelines.

Note

Microsoft Entra integrated clusters using a Kubernetes version newer than version 1.24 automatically use the `kubelogin`

format. Beginning with Kubernetes version 1.24, the default format of the `clusterUser`

credential for Microsoft Entra ID clusters is `exec`

, which requires [ kubelogin](https://github.com/Azure/kubelogin) binary in the execution PATH. There's no behavior change for non-Microsoft Entra clusters, or Microsoft Entra ID clusters running a version older than 1.24.
Existing downloaded

`kubeconfig`

continues to work. An optional query parameter `format`

is included when getting `clusterUser`

credential to overwrite the default behavior change. You can explicitly specify format to `azure`

if you need to maintain the old `kubeconfig`

format.When getting the `clusterUser`

credential, you can use the `format`

query parameter to overwrite the default behavior. You can set the value to `azure`

to use the original `kubeconfig`

format:

```
az aks get-credentials --format azure
```


If your Microsoft Entra integrated cluster uses Kubernetes version 1.24 or lower, you need to manually convert the `kubeconfig`

format.

```
export KUBECONFIG=/path/to/kubeconfig
kubelogin convert-kubeconfig
```


If you receive the message **error: The Azure auth plugin has been removed.**, you need to run the command `kubelogin convert-kubeconfig`

to convert the `kubeconfig`

format manually. For more information, see [Azure Kubelogin Known Issues](https://azure.github.io/kubelogin/known-issues.html).

## Troubleshoot access issues

Important

The step described in this section suggests an alternative authentication method compared to the normal Microsoft Entra group authentication. Use this option only in an emergency.

If you lack administrative access to a valid Microsoft Entra group, you can follow this workaround. Sign in with an account that is a member of the [Azure Kubernetes Service Cluster Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-admin-role) role and grant your group or tenant admin credentials to access your cluster.

## Next steps

- Learn about
[Microsoft Entra integration with Kubernetes RBAC](azure-ad-rbac). - Learn more about
[AKS and Kubernetes identity concepts](concepts-identity). - Learn how to
[use kubelogin](kubelogin-authentication)for all supported Microsoft Entra authentication methods in AKS. - Use
[Azure Resource Manager templates](/en-us/azure/templates/microsoft.containerservice/managedclusters)to create AKS-managed Microsoft Entra ID enabled clusters.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/auto-upgrade-cluster -->

# Automatically upgrade an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Part of the AKS cluster lifecycle involves performing periodic upgrades to the latest Kubernetes version. It's important you apply the latest security releases or upgrade to get the latest features. Before you learn about automatic upgrades, make sure you understand the [AKS cluster upgrade fundamentals](upgrade-cluster).

Note

Any upgrade operation, whether performed manually or automatically, upgrades the node image version if it's not already on the latest version. The latest version is contingent on a full AKS release and can be determined by visiting the [AKS release tracker](release-tracker).

Autoupgrade first upgrades the control plane, and then upgrades agent pools one by one.

## Why use cluster autoupgrade

Cluster autoupgrade provides a *set once and forget* mechanism that yields tangible time and operational cost benefits. You don't need to stop your workloads, redeploy your workloads, or create a new AKS cluster. By enabling autoupgrade, you can ensure your clusters are up to date and don't miss the latest features or patches from AKS and upstream Kubernetes.

AKS follows a strict supportability versioning window. With properly selected autoupgrade channels, you can avoid clusters falling into an unsupported version. For more on the AKS support window, see [Alias minor versions](supported-kubernetes-versions).

## Customer versus AKS-initiated autoupgrades

You can specify cluster autoupgrade specifics using the following guidance. The upgrades occur based on your specified cadence and are recommended to remain on supported Kubernetes versions.

AKS also initiates autoupgrades for unsupported clusters. When a cluster in an n-3 version (where n is the latest supported AKS GA minor version) is about to drop to n-4, AKS automatically upgrades the cluster to n-2 to remain in an AKS support [policy](supported-kubernetes-versions). Automatically upgrading a platform supported cluster to a supported version is enabled by default. Stopped node pools are upgraded during an autoupgrade operation. The upgrade applies to nodes when the node pool is started. To minimize disruptions, set up [maintenance windows](planned-maintenance).

## Cluster autoupgrade limitations

If you're using cluster autoupgrade, you can no longer upgrade the control plane first, and then upgrade the individual node pools. Cluster autoupgrade always upgrades the control plane and the node pools together. You can't upgrade the control plane only. Running the `az aks upgrade --control-plane-only`

command raises the following error:

```
NotAllAgentPoolOrchestratorVersionSpecifiedAndUnchanged: Using managed cluster api, all Agent pools' OrchestratorVersion must be all specified or all unspecified. If all specified, they must be stay unchanged or the same with control plane.
```


If using the `node-image`

(legacy and not to be used) cluster autoupgrade channel or the `NodeImage`

node image autoupgrade channel, Linux [unattended upgrades](https://help.ubuntu.com/community/AutomaticSecurityUpdates) are disabled by default.

## Cluster autoupgrade channels

Automatically completed upgrades are functionally the same as manual upgrades. The [selected autoupgrade channel](planned-maintenance) determines the timing of upgrades. When making changes to autoupgrade, allow 24 hours for the changes to take effect. Automatically upgrading a cluster follows the same process as manually upgrading a cluster. For more information, see [Upgrade an AKS cluster](upgrade-cluster).

The following upgrade channels are available:

| Channel | Action | Example |
|---|---|---|
`none` |
disables autoupgrades and keeps the cluster at its current version of Kubernetes. | Default setting if left unchanged. |
`patch` |
automatically upgrades the cluster to the latest supported patch version when it becomes available while keeping the minor version the same. | For example, if a cluster runs version 1.17.7, and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster upgrades to 1.17.9. |
`stable` |
automatically upgrades the cluster to the latest supported patch release on minor version N-1, where N is the latest supported minor version. |
For example, if a cluster runs version 1.17.7 and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster upgrades to 1.18.6. |
`rapid` |
automatically upgrades the cluster to the latest supported patch release on the latest supported minor version. | In cases where the cluster's Kubernetes version is an N-2 minor version, where N is the latest supported minor version, the cluster first upgrades to the latest supported patch version on N-1 minor version. For example, if a cluster runs version 1.17.7 and versions 1.17.9, 1.18.4, 1.18.6, and 1.19.1 are available, the cluster first upgrades to 1.18.6, then upgrades to 1.19.1. |
`node-image` (legacy) |
automatically upgrades the node image to the latest version available. | Microsoft provides patches and new images for image nodes frequently (weekly), but your running nodes don't get the new images unless you do a node image upgrade. Turning on the node-image channel automatically updates your node images whenever a new version is available. If you use this channel, Linux [unattended upgrades] are disabled by default. Node image upgrades work on patch versions that are deprecated, so long as the minor Kubernetes version is still supported. This channel is no longer recommended and is planned for deprecation in future. For an option that can automatically upgrade node images, see the `NodeImage` channel in
|

Note

Keep the following information in mind when using cluster autoupgrade:

Cluster autoupgrade only updates to GA versions of Kubernetes and doesn't update to preview versions.

With AKS, you can create a cluster without specifying the exact patch version. When you create a cluster without designating a patch, the cluster runs the minor version's latest GA patch. To learn more, see

[AKS support window](supported-kubernetes-versions).Autoupgrade requires the cluster's Kubernetes version to be within the

[AKS support window](supported-kubernetes-versions), even if using the`node-image`

channel.If you're using the preview API

`11-02-preview`

or later, and you select the`node-image`

cluster autoupgrade channel, the[node image autoupgrade channel](auto-upgrade-node-image)automatically sets to`NodeImage`

.Each cluster can only be associated with a single autoupgrade channel. The reason is because your specified channel determines the Kubernetes version that runs on the cluster.

If your cluster has no autoupgrade channel and you enable it for Long-Term Support (LTS), the cluster defaults to a

`patch`

autoupgrade channel.

## Use cluster autoupgrade with a new AKS cluster

Set the autoupgrade channel when creating a new cluster using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command and the

`auto-upgrade-channel`

parameter.```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export RESOURCE_GROUP="myResourceGroup$RANDOM_SUFFIX"
export AKS_CLUSTER_NAME="myAKSCluster"
az aks create --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --auto-upgrade-channel stable --generate-ssh-keys
```


## Use cluster autoupgrade with an existing AKS cluster

Set the autoupgrade channel on an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`auto-upgrade-channel`

parameter.```
az aks update --resource-group $RESOURCE_GROUP --name $AKS_CLUSTER_NAME --auto-upgrade-channel stable
```


Results:

```
{
"id": "/subscriptions/aaaa6a6a-bb7b-cc8c-dd9d-eeeeee0e0e0e/resourceGroups/myResourceGroupabc123/providers/Microsoft.ContainerService/managedClusters/myAKSCluster",
"properties": {
"autoUpgradeChannel": "stable",
"provisioningState": "Succeeded"
}
}
```


## Use autoupgrade with Planned Maintenance

If using Planned Maintenance and cluster autoupgrade, your upgrade starts during your specified maintenance window.

Note

To ensure proper functionality, use a maintenance window of *four hours or more*.

For more information on how to set a maintenance window with Planned Maintenance, see [Use Planned Maintenance to schedule maintenance windows for your Azure Kubernetes Service (AKS) cluster](planned-maintenance).

## Best practices for cluster autoupgrade

Use the following best practices to help maximize your success when using autoupgrade:

- To ensure your cluster is always in a supported version, for example within the N-2 rule, choose either
`stable`

or`rapid`

channels. - If you're interested in getting the latest patches as soon as possible, use the
`patch`

channel. The`node-image`

channel is a good fit if you want your agent pools to always run the most recent node images. - To automatically upgrade node images while using a different cluster upgrade channel, consider using the
[node image autoupgrade](auto-upgrade-node-image)`NodeImage`

channel. - Follow
[Operator best practices](operator-best-practices-scheduler#plan-for-availability-using-pod-disruption-budgets). - Follow
[PodDisruptionBudget (PDB) best practices](https://kubernetes.io/docs/tasks/run-application/configure-pdb/). - For upgrade troubleshooting information, see the
[AKS troubleshooting documentation](/en-us/support/azure/azure-kubernetes/welcome-azure-kubernetes).

For a detailed discussion of upgrade best practices and other considerations, see [AKS patch and upgrade guidance](/en-us/azure/architecture/operator-guides/aks/aks-upgrade-practices).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-tool-calling -->

# Integrate tool calling with LLM Inference with the AI toolchain operator add-on on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you configure and deploy an AI toolchain operator (KAITO) inference workspace on Azure Kubernetes Service (AKS) with support for OpenAI-style tool calling. You also learn how to validate tool calling functionality using vLLM metrics and local function mocks.

## What is tool calling?

Tool calling enables large language models (LLMs) to interface with external functions, APIs, or services. Instead of just generating text, an LLM can decide:

- "I need to call a weather API."
- "I need to use a calculator."
- "I should search a database."

It does this by invoking a defined “tool” with parameters it chooses based on the user’s request. Tool calling is useful for:

- Chatbots that book, summarize, or calculate.
- Enterprise LLM applications where hallucination must be minimized.
- Agent frameworks (AutoGen, LangGraph, LangChain, AgentOps, etc.).

In production environments, AI-enabled applications often demand more than natural language generation; they require the ability to take action based on user intent. Tool calling empowers LLMs to extend beyond text responses by invoking external tools, APIs, or custom logic in real time. This bridges the gap between language understanding and execution, enabling developers to build interactive AI assistants, agents, and automation workflows that are both accurate and useful. Instead of relying on static responses, LLMs can now access live data, trigger services, and complete tasks on behalf of users, both safely and reliably.

When deployed on AKS, tool calling becomes scalable, secure, and production ready. Kubernetes provides the flexibility to orchestrate inference workloads using high-performance runtimes like vLLM, while ensuring observability and governance of tool usage. With this pattern, AKS operators and app developers can more seamlessly update models or tools independently and deploy advanced AI features without compromising reliability.

As a result, tool calling on AKS is now a foundational pattern for building modern AI apps that are context-aware, action-capable, and enterprise-ready.

### Tool calling with KAITO

To streamline this deployment model, the AI toolchain operator (KAITO) add-on for AKS provides a managed solution for running inference services with [tool calling support](https://kaito-project.github.io/kaito/docs/tool-calling/). By leveraging KAITO inference workspaces, you can quickly spin up scalable, GPU-accelerated model endpoints with built-in support for tool calling and OpenAI-compatible APIs. This eliminates the operational overhead of configuring runtimes, managing dependencies, or scaling infrastructure manually.

## Prerequisites

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Your AKS cluster is running on Kubernetes version
`1.33`

or higher. To upgrade your cluster, see[Upgrade your AKS cluster](upgrade-aks-cluster). - Install and configure Azure CLI version
`2.77.0`

or later. To find your version, run`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The
[AI toolchain operator add-on enabled](ai-toolchain-operator)on your cluster. - A deployed KAITO inference workspace that supports tool calling. Refer to the official
[KAITO tool calling](https://kaito-project.github.io/kaito/docs/tool-calling/)documentation for the tool calling supported models with vLLM. - You deployed the
`workspace‑phi‑4-mini-toolcall`

[KAITO workspace](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_tool_calling.yaml)with the default configuration.

## Confirm the KAITO inference workspace is running

Monitor your workspace deployment with the

`kubectl get`

command.`kubectl get workspace workspace‑phi‑4‑mini-toolcall -w`

In the output, you want to verify the resource (

`ResourceReady`

) and inference (`InferenceReady`

) are ready and the workspace succeeded (`WorkspaceSucceeded`

being`true`

).

## Confirm the inference API is ready to serve

Once the

[workspace is ready](#confirm-the-kaito-inference-workspace-is-running), find the service endpoint using the`kubectl get`

command.`kubectl get svc workspace‑phi‑4-mini-toolcall`

Note

The output might be a

`ClusterIP`

or internal address. Check which port(s) the service listens on. The default KAITO inference API is on port`80`

for HTTP. If it's only internal, you can port‑forward locally.Port-forward the inference service for testing using the

`kubectl port-forward`

command.`kubectl port-forward svc/workspace‑phi‑4‑mini-toolcall 8000:80`

Check the

`/v1/models`

endpoint to confirm the LLM is available using`curl`

.`curl http://localhost:8000/v1/models`

To ensure the LLM is deployed, and the API is working, your output should be similar to the following:

`... { "object": "list", "data": [ { "id": "phi‑4‑mini‑instruct", ... ... } ] } ...`


## Test the named function tool‐calling

In this example, the `workspace‑phi‑4‑mini-toolcall`

workspace supports named function tool-calling by default, so we can confirm the LLM accepts a “tool” spec in OpenAI‑style requests and returns a “function call” structure.

The Python snippet we use in this section is from the [KAITO documentation](https://kaito-project.github.io/kaito/docs/tool-calling/#examples) and uses an OpenAI‑compatible client.

Confirm the LLM accepts a “tool” spec in OpenAI‑style requests and returns a “function call” structure. This example:

- Initializes the OpenAI-compatible client to talk to a local inference server. The server is assumed to be running at
`http://localhost:8000/v1`

and accepts OpenAI-style API calls. - Simulates the backend logic for a tool called
`get_weather`

. (In a real scenario, this would call a weather API.) - Describes the tool interface; the
`Phi-4-mini`

LLM will see this tool and decide whether to use it based on the user's input. - Sends a sample chat message to the model and provides the tool spec. The setting
`tool_choice="auto"`

allows the LLM to decide if it should call a tool based on the prompt. - In this case, the user's request was relevant to the
`get_weather`

tool, so we simulate the execution of the tool, calling the local function with the model's chosen arguments.

`from openai import OpenAI import json # local server client = OpenAI(base_url="http://localhost:8000/v1", api_key="dummy") def get_weather(location: str, unit: str) -> str: return f"Getting the weather for {location} in {unit}..." tool_functions = {"get_weather": get_weather} tools = [{ "type": "function", "function": { "name": "get_weather", "description": "Get the current weather in a given location", "parameters": { "type": "object", "properties": { "location": {"type": "string"}, "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]} }, "required": ["location", "unit"] } } }] response = client.chat.completions.create( model="phi‑4‑mini‑instruct", # or client.models.list().data[0].id messages=[{"role": "user", "content": "What's the weather like in San Francisco?"}], tools=tools, tool_choice="auto" ) # Inspect response tool_call = response.choices[0].message.tool_calls[0].function args = json.loads(tool_call.arguments) print("Function called:", tool_call.name) print("Arguments:", args) print("Result:", tool_functions[tool_call.name](**args))`

Your output should look similar to the following:

`Function called: get_weather Arguments: {"location": "San Francisco, CA", "unit": "fahrenheit"} Result: Getting the weather for San Francisco, CA in fahrenheit...`

The “tool_calls” field comes back, meaning the

`Phi-4-mini`

LLM decided to invoke the function. Now, a sample tool call has been successfully parsed and executed based on the model’s decision to confirm end-to-end tool calling behavior with the KAITO inference deployment.- Initializes the OpenAI-compatible client to talk to a local inference server. The server is assumed to be running at

## Troubleshooting

### Model preset doesn’t support tool calling

If you pick a model that isn't on the supported list, tool calling might not work. Make sure you [review the KAITO documentation](https://kaito-project.github.io/kaito/docs/tool-calling/), which explicitly lists which presets support tool calling.

### Misaligned runtime

The KAITO inference must use [vLLM runtime for tool calling](https://kaito-project.github.io/kaito/docs/tool-calling/#supported-inference-runtimes) (HuggingFace Transformers runtime generally doesn’t support tool calling in KAITO).

### Network / endpoint issues

If port-forwarding, ensure the service ports are correctly forwarded. If the external MCP server is unreachable, will error out.

### Timeouts

External MCP server calls might take time. Make sure the adapter or client timeout is sufficiently high.

### Authentication

If the external MCP server requires authentication (API key, header, etc.), ensure you supply correct credentials.

## Next steps

- Set up
[vLLM monitoring in the AI toolchain operator add-on](ai-toolchain-operator-monitoring)with Prometheus and Grafana on AKS. - Learn about
[MCP server support with KAITO](ai-toolchain-operator-mcp)and test standardized tool calling examples on your AKS cluster.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-telemetry -->

# Telemetry API for Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Istio can [generate metrics, distributed traces, and access logs](https://istio.io/latest/docs/concepts/observability/) for all workloads in the mesh. The Istio-based service mesh add-on for Azure Kubernetes Service (AKS) provides telemetry customization options through the [shared MeshConfig](istio-meshconfig) and the Istio Telemetry API `v1`

for Istio add-on minor revisions `asm-1-22`

and higher.

Note

While the [Istio MeshConfig](istio-meshconfig) also provides options for configuring telemetry globally across the mesh, the Telemetry API offers more granular control over telemetry settings on a per-service or per-workload basis. As the Istio community continues to invest in the Telemetry API, it is now the preferred method for telemetry configuration. We encourage migrating to the Telemetry API for configuring telemetry to be collected in the mesh.

## Prerequisites

- You must be on revision
`asm-1-22`

or higher. For information on how to perform minor version upgrades, see the[Istio add-on upgrade documentation](istio-upgrade).

## Configure Telemetry resources

The following example demonstrates how Envoy access logging can be enabled across the mesh for the Istio add-on via the Telemetry API using `asm-1-22`

(adjust the revision as needed). For guidance on other Telemetry API customizations for the add-on, see the [Telemetry API support scope](#telemetry-api-support-scope) section and the [Istio documentation](https://istio.io/latest/docs/reference/config/telemetry/).

### Deploy sample applications

Label the namespace for sidecar injection:

```
kubectl label ns default istio.io/rev=asm-1-22
```


Deploy the `sleep`

application and set the `SOURCE_POD`

environment variable:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/sleep/sleep.yaml
export SOURCE_POD=$(kubectl get pod -l app=sleep -o jsonpath={.items..metadata.name})
```


Then, deploy the `httpbin`

application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.22/samples/httpbin/httpbin.yaml
```


### Enable Envoy access logging with the Istio Telemetry API

Deploy the following Istio `v1`

Telemetry API resource to enable Envoy access logging for the entire mesh:

```
cat <<EOF | kubectl apply -n aks-istio-system -f -
apiVersion: telemetry.istio.io/v1
kind: Telemetry
metadata:
name: mesh-logging-default
spec:
accessLogging:
- providers:
- name: envoy
EOF
```


### Test access logs

Send a request from `sleep`

to `httpbin`

:

```
kubectl exec "$SOURCE_POD" -c sleep -- curl -sS -v httpbin:8000/status/418
```


Verify that access logs are visible for the `sleep`

pod:

```
kubectl logs -l app=sleep -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.690Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 12 11 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" outbound|8000||httpbin.default.svc.cluster.local 10.244.0.12:53336 10.0.112.220:8000 10.244.0.12:42360 - default
```


Now, verify that access logs are visible for the `httpbin`

pod:

```
kubectl logs -l app=httpbin -c istio-proxy
```


You should see the following output:

```
[2024-08-13T00:31:47.696Z] "GET /status/418 HTTP/1.1" 418 - via_upstream - "-" 0 135 2 1 "-" "curl/8.9.1" "cdecaca5-5964-48f3-b42d-f474dfa623d5" "httpbin:8000" "10.244.0.13:8080" inbound|8080|| 127.0.0.6:55401 10.244.0.13:8080 10.244.0.12:53336 outbound_.8000_._.httpbin.default.svc.cluster.local default
```


## Telemetry API support scope

For the Istio service mesh add-on for AKS, Telemetry API fields are classified as `allowed`

, `supported`

, and `blocked`

values. For more information about the Istio add-on's support policy for features and mesh configurations, see the Istio add-on [support policy document](istio-support-policy#allowed-supported-and-blocked-customizations).

The following Telemetry API configurations are either `allowed`

or `supported`

for the Istio add-on. Any field not included in this table is `blocked`

.

Telemetry API Field |
Supported/Allowed |
Notes |
|---|---|---|
`accessLogging.match` |
Supported | - |
`accessLogging.disabled` |
Supported | - |
`accessLogging.providers` |
Allowed | The default `envoy` access log provider is supported. For a managed experience for log collection and querying, see
`allowed` but unsupported. |
`metrics.overrides` |
Supported | - |
`metrics.providers` |
Allowed | Metrics collection with
`allowed` but unsupported. |

`tracing.*`

`allowed`

but unsupported.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-scenarios-hub -->

# AKS upgrade scenarios: Choose your path

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrading Azure Kubernetes Service (AKS) clusters safely requires the right strategy for your specific situation. Use this hub to quickly identify your scenario and get targeted guidance.

## What this article covers

This decision hub helps you choose the right AKS upgrade approach based on:

- A quick scenario finder with time constraints and priorities.
- Emergency upgrade paths for critical security responses.
- A strategy matrix that compares downtime tolerance and complexity.
- Role-based guidance for site reliability engineers, database administrators, developers, and security teams.
- Decision trees for complex multi-environment setups.

This hub is best for first-time upgraders, teams that need to evaluate options, and complex environments that require tailored approaches.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To get upgrade patterns for AKS clusters with stateful workloads, see
[Stateful workload upgrade patterns](stateful-workload-upgrades). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service (AKS) cluster](upgrade-aks-cluster).

## Quick scenario finder

What's your primary concern? Select your answer from the following table.

| My priority | Time constraint | Go to |
|---|---|---|
| Zero production downtime | Upgrade needed within hours |
|

[Staged fleet upgrades](aks-production-upgrade-strategies#scenario-2-stage-upgrades-across-environments)[Safe version intake](aks-production-upgrade-strategies#scenario-3-safe-kubernetes-version-intake)[Fast security patching](aks-production-upgrade-strategies#scenario-4-fastest-security-patch-deployment)[Stateful workload patterns](stateful-workload-upgrades)[Seamless architecture](aks-production-upgrade-strategies#scenario-5-application-architecture-for-seamless-upgrades)## Emergency upgrade (30-90 minutes)

If you need a critical security patch now, select a link for instructions:

**Immediate action:**[Automated security patching](aks-production-upgrade-strategies#scenario-4-fastest-security-patch-deployment)**With stateful workloads:**[Database safety patterns](stateful-workload-upgrades#emergency-upgrade-checklist)**Rollback ready:**[Quick recovery guide](aks-production-upgrade-strategies#emergency-rollback-procedures)

## Upgrade strategy matrix

Find your ideal approach based on business constraints.

| Downtime tolerance | Environment | Best strategy | Time investment |
|---|---|---|---|
| <2 minutes | Production | Blue-green deployment | 45-60 min |
| <30 seconds | Stateful apps | Ferris wheel pattern | 60-90 min |
| Planned window | Multi-environment | Staged fleet upgrade | 2-4 hours |
| Zero tolerance | Mission-critical | Application architecture | Ongoing |

## Key upgrade topics

### Core upgrade mechanics

### Production-ready strategies

[Scenario-based production upgrades](aks-production-upgrade-strategies)[Stateful workload upgrade patterns](stateful-workload-upgrades)[Cross-environment upgrade staging](aks-production-upgrade-strategies#scenario-2-stage-upgrades-across-environments)

### Advanced topics

## Quick wins (5-15 minutes)

Immediate actions that you can take:

**Pre-upgrade health check:**Run[cluster diagnostics](aks-diagnostics).**Backup validation:**Verify your[disaster recovery](ha-dr-overview)setup.**Monitoring setup:**Enable[upgrade notifications](aks-communication-manager).**Team preparation:**Review[support policies](support-policies).

## Learning path

If you're new to AKS upgrades, follow this learning sequence:

**Learn:**Learn about[Kubernetes concepts](core-aks-concepts)and read the[Upgrade overview](upgrade-cluster).**Practice:**Take the tutorial on how to[upgrade an AKS cluster](tutorial-kubernetes-upgrade-cluster).**Production:**Use the[production strategies](aks-production-upgrade-strategies).**Optimize:**Find out about[stateful patterns](stateful-workload-upgrades).

## Pro tips

**Always test in nonproduction first:**Perform tests even for emergency patches.**Monitor during upgrades:**Set up[real-time alerts](aks-communication-manager).**Plan for rollback:**Have a tested recovery procedure.**Communicate with teams:**Coordinate with app owners during upgrades.

## Related content

- For more help, choose your scenario from the preceding options or start with
[Production upgrade strategies](aks-production-upgrade-strategies). - For more information, see
[AKS support options](aks-support-help)or the[Troubleshooting guide](upgrade-cluster#common-upgrade-scenarios-and-recommendations).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/manage-azure-rbac -->

# Use Azure role-based access control for Kubernetes Authorization

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers how to use Azure RBAC for Kubernetes Authorization, which allows for the unified management and access control across Azure resources, AKS, and Kubernetes resources. For more information, see [Azure RBAC for Kubernetes Authorization](/en-us/azure/aks/concepts-identity#azure-rbac-for-kubernetes-authorization).

Note

When using [integrated authentication between Microsoft Entra ID and AKS](managed-azure-ad), you can use Microsoft Entra users, groups, or service principals as subjects in [Kubernetes role-based access control (Kubernetes RBAC)](/en-us/azure/aks/concepts-identity#azure-rbac-for-kubernetes-authorization). With this feature, you don't need to separately manage user identities and credentials for Kubernetes. However, you still need to set up and manage Azure RBAC and Kubernetes RBAC separately.

## Before you begin

- You need the Azure CLI version 2.24.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You need
`kubectl`

, with a minimum version of[1.18.3](https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG/CHANGELOG-1.18.md#v1183). - You need managed Microsoft Entra integration enabled on your cluster before you can add Azure RBAC for Kubernetes authorization. If you need to enable managed Microsoft Entra integration, see
[Use Microsoft Entra ID in AKS](managed-azure-ad). - If you have CRDs and are making custom role definitions, the only way to cover CRDs today is to use
`Microsoft.ContainerService/managedClusters/*/read`

. For the remaining objects, you can use the specific API groups, such as`Microsoft.ContainerService/apps/deployments/read`

. - New role assignments can take
*up to five minutes*to propagate and be updated by the authorization server. - Azure RBAC for Kubernetes Authorization requires that the Microsoft Entra tenant configured for authentication is same as the tenant for the subscription that holds your AKS cluster.

## Create a new AKS cluster with managed Microsoft Entra integration and Azure RBAC for Kubernetes Authorization

Create an Azure resource group using the

command.`az group create`

`export RESOURCE_GROUP=<resource-group-name> export LOCATION=<azure-region> az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster with managed Microsoft Entra integration and Azure RBAC for Kubernetes Authorization using the

command.`az aks create`

`export CLUSTER_NAME=<cluster-name> az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-aad \ --enable-azure-rbac \ --generate-ssh-keys`

Your output should look similar to the following example output:

`"AADProfile": { "adminGroupObjectIds": null, "clientAppId": null, "enableAzureRbac": true, "managed": true, "serverAppId": null, "serverAppSecret": null, "tenantId": "****-****-****-****-****" }`


## Enable Azure RBAC on an existing AKS cluster

Enable Azure RBAC for Kubernetes Authorization on an existing AKS cluster using the

command with the`az aks update`

`--enable-azure-rbac`

flag.`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-azure-rbac`


## Disable Azure RBAC for Kubernetes Authorization from an AKS cluster

Remove Azure RBAC for Kubernetes Authorization from an existing AKS cluster using the

command with the`az aks update`

`--disable-azure-rbac`

flag.`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --disable-azure-rbac`


## AKS built-in roles

AKS provides the following built-in roles:

| Role | Description |
|---|---|
| Azure Kubernetes Service RBAC Reader | Allows read-only access to see most objects in a namespace. It doesn't allow viewing roles or role bindings. This role doesn't allow viewing `Secrets` , since reading the contents of Secrets enables access to ServiceAccount credentials in the namespace, which would allow API access as any ServiceAccount in the namespace (a form of privilege escalation). |
| Azure Kubernetes Service RBAC Writer | Allows read/write access to most objects in a namespace. This role doesn't allow viewing or modifying roles or role bindings. However, this role allows accessing `Secrets` and running Pods as any ServiceAccount in the namespace, so it can be used to gain the API access levels of any ServiceAccount in the namespace. |
| Azure Kubernetes Service RBAC Admin | Allows admin access, intended to be granted within a namespace. Allows read/write access to most resources in a namespace (or cluster scope), including the ability to create roles and role bindings within the namespace. This role doesn't allow write access to resource quota or to the namespace itself. |
| Azure Kubernetes Service RBAC Cluster Admin | Allows super-user access to perform any action on any resource. It gives full control over every resource in the cluster and in all namespaces. |

## Create role assignments for cluster access

Get your AKS resource ID using the

command.`az aks show`

`AKS_ID=$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query id --output tsv)`

Create a role assignment using the

command.`az role assignment create`

`<AAD-ENTITY-ID>`

can be a username or the client ID of a service principal. The following example creates a role assignment for the*Azure Kubernetes Service RBAC Admin*role.`az role assignment create --role "Azure Kubernetes Service RBAC Admin" --assignee <AAD-ENTITY-ID> --scope $AKS_ID`

Note

You can create the

*Azure Kubernetes Service RBAC Reader*and*Azure Kubernetes Service RBAC Writer*role assignments scoped to a specific namespace within the cluster using thecommand and setting the scope to the desired namespace.`az role assignment create`

`az role assignment create --role "Azure Kubernetes Service RBAC Reader" --assignee <AAD-ENTITY-ID> --scope $AKS_ID/namespaces/<namespace-name>`


## Create custom roles definitions

The following example custom role definition allows a user to only read deployments and nothing else. For the full list of possible actions, see [Microsoft.ContainerService operations](/en-us/azure/role-based-access-control/resource-provider-operations#microsoftcontainerservice).

To create your own custom role definitions, copy the following file, replacing

`<YOUR SUBSCRIPTION ID>`

with your own subscription ID, and then save it as`deploy-view.json`

.`{ "Name": "AKS Deployment Reader", "Description": "Lets you view all deployments in cluster/namespace.", "Actions": [], "NotActions": [], "DataActions": [ "Microsoft.ContainerService/managedClusters/apps/deployments/read" ], "NotDataActions": [], "assignableScopes": [ "/subscriptions/<YOUR SUBSCRIPTION ID>" ] }`

Create the role definition using the

command, setting the`az role definition create`

`--role-definition`

to the`deploy-view.json`

file you created in the previous step.`az role definition create --role-definition @deploy-view.json`

Assign the role definition to a user or other identity using the

command.`az role assignment create`

`az role assignment create --role "AKS Deployment Reader" --assignee <AAD-ENTITY-ID> --scope $AKS_ID`


## Use Azure RBAC for Kubernetes Authorization with `kubectl`


Make sure you have the

[Azure Kubernetes Service Cluster User](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-cluster-user-role)built-in role, and then get the kubeconfig of your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

You can now use

`kubectl`

to manage your cluster. For example, you can list the nodes in your cluster using`kubectl get nodes`

.`kubectl get nodes`

Example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-93451573-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000002 Ready agent 3h6m v1.15.11`


## Use Azure RBAC for Kubernetes Authorization with `kubelogin`


AKS created the [ kubelogin](https://github.com/Azure/kubelogin) plugin to help unblock scenarios such as non-interactive logins, older

`kubectl`

versions, or leveraging SSO across multiple clusters without the need to sign in to a new cluster.Use the

`kubelogin`

plugin by running the following command:`export KUBECONFIG=/path/to/kubeconfig kubelogin convert-kubeconfig`

You can now use

`kubectl`

to manage your cluster. For example, you can list the nodes in your cluster using`kubectl get nodes`

.`kubectl get nodes`

Example output:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-93451573-vmss000000 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000001 Ready agent 3h6m v1.15.11 aks-nodepool1-93451573-vmss000002 Ready agent 3h6m v1.15.11`


## Clean up resources

### Delete role assignment

List role assignments using the

command.`az role assignment list`

`az role assignment list --scope $AKS_ID --query [].id --output tsv`

Delete role assignments using the

command.`az role assignment delete`

`az role assignment delete --ids <LIST OF ASSIGNMENT IDS>`


### Delete role definition

Delete the custom role definition using the

command.`az role definition delete`

`az role definition delete --name "AKS Deployment Reader"`


### Delete resource group and AKS cluster

Delete the resource group and AKS cluster using the

command.`az group delete`

`az group delete --name $RESOURCE_GROUP --yes --no-wait`


## Next steps

To learn more about AKS authentication, authorization, Kubernetes RBAC, and Azure RBAC, see:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/create-postgresql-ha -->

# Create infrastructure for deploying a highly available PostgreSQL database on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you create the infrastructure resources needed to deploy a highly available PostgreSQL database on AKS using the [CloudNativePG (CNPG)](https://cloudnative-pg.io/) operator.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Before you begin

- Review the deployment overview and make sure you meet all the prerequisites in
[How to deploy a highly available PostgreSQL database on AKS with Azure CLI](postgresql-ha-overview). [Set environment variables](#set-environment-variables)for use throughout this guide.[Install the required extensions](#install-required-extensions).

## Set environment variables

Set the following environment variables for use throughout this guide:

```
export SUFFIX=$(cat /dev/urandom | LC_ALL=C tr -dc 'a-z0-9' | fold -w 8 | head -n 1)
export LOCAL_NAME="cnpg"
export TAGS="owner=user"
export RESOURCE_GROUP_NAME="rg-${LOCAL_NAME}-${SUFFIX}"
export PRIMARY_CLUSTER_REGION="canadacentral"
export AKS_PRIMARY_CLUSTER_NAME="aks-primary-${LOCAL_NAME}-${SUFFIX}"
export AKS_PRIMARY_MANAGED_RG_NAME="rg-${LOCAL_NAME}-primary-aksmanaged-${SUFFIX}"
export AKS_PRIMARY_CLUSTER_FED_CREDENTIAL_NAME="pg-primary-fedcred1-${LOCAL_NAME}-${SUFFIX}"
export AKS_PRIMARY_CLUSTER_PG_DNSPREFIX=$(echo $(echo "a$(openssl rand -hex 5 | cut -c1-11)"))
export AKS_UAMI_CLUSTER_IDENTITY_NAME="mi-aks-${LOCAL_NAME}-${SUFFIX}"
export AKS_CLUSTER_VERSION="1.32"
export PG_NAMESPACE="cnpg-database"
export PG_SYSTEM_NAMESPACE="cnpg-system"
export PG_PRIMARY_CLUSTER_NAME="pg-primary-${LOCAL_NAME}-${SUFFIX}"
export PG_PRIMARY_STORAGE_ACCOUNT_NAME="hacnpgpsa${SUFFIX}"
export PG_STORAGE_BACKUP_CONTAINER_NAME="backups"
export MY_PUBLIC_CLIENT_IP=$(dig +short myip.opendns.com @resolver3.opendns.com)
```


## Install required extensions

Install the extensions needed for Kubernetes integration and monitoring:

```
az extension add --upgrade --name k8s-extension --yes
az extension add --upgrade --name amg --yes
```


As a prerequisite for using `kubectl`

, you need to first install [Krew](https://krew.sigs.k8s.io/), followed by the installation of the [CNPG plugin](https://cloudnative-pg.io/documentation/current/kubectl-plugin/#using-krew). These installations enable the management of the PostgreSQL operator using the subsequent commands.

```
(
set -x; cd "$(mktemp -d)" &&
OS="$(uname | tr '[:upper:]' '[:lower:]')" &&
ARCH="$(uname -m | sed -e 's/x86_64/amd64/' -e 's/\(arm\)\(64\)\?.*/\1\2/' -e 's/aarch64$/arm64/')" &&
KREW="krew-${OS}_${ARCH}" &&
curl -fsSLO "https://github.com/kubernetes-sigs/krew/releases/latest/download/${KREW}.tar.gz" &&
tar zxvf "${KREW}.tar.gz" &&
./"${KREW}" install krew
)
export PATH="${KREW_ROOT:-$HOME/.krew}/bin:$PATH"
kubectl krew install cnpg
```


## Create a resource group

Create a resource group to hold the resources you create in this guide using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create \
--name $RESOURCE_GROUP_NAME \
--location $PRIMARY_CLUSTER_REGION \
--tags $TAGS \
--query 'properties.provisioningState' \
--output tsv
```


## Create a user-assigned managed identity

In this section, you create a user-assigned managed identity (UAMI) to allow the CNPG PostgreSQL to use an AKS workload identity to access Azure Blob Storage. This configuration allows the PostgreSQL cluster on AKS to connect to Azure Blob Storage without a secret.

Create a user-assigned managed identity using the

command.`az identity create`

`AKS_UAMI_WI_IDENTITY=$(az identity create \ --name $AKS_UAMI_CLUSTER_IDENTITY_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --output json)`

Enable AKS workload identity and generate a service account to use later in this guide using the following commands:

`export AKS_UAMI_WORKLOAD_OBJECTID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.principalId') export AKS_UAMI_WORKLOAD_RESOURCEID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.id') export AKS_UAMI_WORKLOAD_CLIENTID=$( \ echo "${AKS_UAMI_WI_IDENTITY}" | jq -r '.clientId') echo "ObjectId: $AKS_UAMI_WORKLOAD_OBJECTID" echo "ResourceId: $AKS_UAMI_WORKLOAD_RESOURCEID" echo "ClientId: $AKS_UAMI_WORKLOAD_CLIENTID"`


The object ID is a unique identifier for the client ID (also known as the application ID) that uniquely identifies a security principal of type *Application* within the Microsoft Entra ID tenant. The resource ID is a unique identifier to manage and locate a resource in Azure. These values are required to enabled AKS workload identity.

The CNPG operator automatically generates a service account called *postgres* that you use later in the guide to create a federated credential that enables OAuth access from PostgreSQL to Azure Storage.

## Create a storage account in the primary region

Create an object storage account to store PostgreSQL backups in the primary region using the

command.`az storage account create`

`az storage account create \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --sku Standard_ZRS \ --kind StorageV2 \ --query 'provisioningState' \ --output tsv`

Create the storage container to store the Write Ahead Logs (WAL) and regular PostgreSQL on-demand and scheduled backups using the

command.`az storage container create`

`az storage container create \ --name $PG_STORAGE_BACKUP_CONTAINER_NAME \ --account-name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --auth-mode login`

Example output:

`{ "created": true }`

Note

If you encounter the error message:

`The request may be blocked by network rules of storage account. Please check network rule set using 'az storage account show -n accountname --query networkRuleSet'. If you want to change the default action to apply when no rule matches, please use 'az storage account update'`

. Make sure to verify user permissions for Azure Blob Storage and, if**necessary**, elevate your role to`Storage Blob Data Owner`

using the commands provided and after retry thecommand.`az storage container create`

`export USER_ID=$(az ad signed-in-user show --query id --output tsv) export STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID=$(az storage account show \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "id" \ --output tsv) az role assignment list --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID --output table az role assignment create \ --assignee-object-id $USER_ID \ --assignee-principal-type User \ --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID \ --role "Storage Blob Data Owner" \ --output tsv`


## Assign RBAC to storage accounts

To enable backups, the PostgreSQL cluster needs to read and write to an object store. The PostgreSQL cluster running on AKS uses a workload identity to access the storage account via the CNPG operator configuration parameter [ inheritFromAzureAD](https://cloudnative-pg.io/documentation/1.23/appendixes/object_stores/#azure-blob-storage).

Get the primary resource ID for the storage account using the

command.`az storage account show`

`export STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID=$(az storage account show \ --name $PG_PRIMARY_STORAGE_ACCOUNT_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query "id" \ --output tsv) echo $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID`

Assign the "Storage Blob Data Contributor" Azure built-in role to the object ID with the storage account resource ID scope for the UAMI associated with the managed identity for each AKS cluster using the

command.`az role assignment create`

`az role assignment create \ --role "Storage Blob Data Contributor" \ --assignee-object-id $AKS_UAMI_WORKLOAD_OBJECTID \ --assignee-principal-type ServicePrincipal \ --scope $STORAGE_ACCOUNT_PRIMARY_RESOURCE_ID \ --query "id" \ --output tsv`


## Set up monitoring infrastructure

In this section, you deploy an instance of Azure Managed Grafana, an Azure Monitor workspace, and an Azure Monitor Log Analytics workspace to enable monitoring of the PostgreSQL cluster. You also store references to the created monitoring infrastructure to use as input during the AKS cluster creation process later in the guide. This section might take some time to complete.

Note

Azure Managed Grafana instances and AKS clusters are billed independently. For more pricing information, see [Azure Managed Grafana pricing](https://azure.microsoft.com/pricing/details/managed-grafana/).

Create an Azure Managed Grafana instance using the

command.`az grafana create`

`export GRAFANA_PRIMARY="grafana-${LOCAL_NAME}-${SUFFIX}" export GRAFANA_RESOURCE_ID=$(az grafana create \ --resource-group $RESOURCE_GROUP_NAME \ --name $GRAFANA_PRIMARY \ --location $PRIMARY_CLUSTER_REGION \ --zone-redundancy Enabled \ --tags $TAGS \ --query "id" \ --output tsv) echo $GRAFANA_RESOURCE_ID`

Create an Azure Monitor workspace using the

command.`az monitor account create`

`export AMW_PRIMARY="amw-${LOCAL_NAME}-${SUFFIX}" export AMW_RESOURCE_ID=$(az monitor account create \ --name $AMW_PRIMARY \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --tags $TAGS \ --query "id" \ --output tsv) echo $AMW_RESOURCE_ID`

Create an Azure Monitor Log Analytics workspace using the

command.`az monitor log-analytics workspace create`

`export ALA_PRIMARY="ala-${LOCAL_NAME}-${SUFFIX}" export ALA_RESOURCE_ID=$(az monitor log-analytics workspace create \ --resource-group $RESOURCE_GROUP_NAME \ --workspace-name $ALA_PRIMARY \ --location $PRIMARY_CLUSTER_REGION \ --query "id" \ --output tsv) echo $ALA_RESOURCE_ID`


## Create the AKS cluster to host the PostgreSQL cluster

In this section, you create a multizone AKS cluster with a system node pool. The AKS cluster hosts the PostgreSQL cluster primary replica and two standby replicas, each aligned to a different availability zone to enable zonal redundancy.

You also add a user node pool to the AKS cluster to host the PostgreSQL cluster. Using a separate node pool allows for control over the Azure VM SKUs used for PostgreSQL and enables the AKS system pool to optimize performance and costs. You apply a label to the user node pool that you can reference for node selection when deploying the CNPG operator later in this guide. This section might take some time to complete.

Important

If you opt to use local NVMe as your PostgreSQL storage in the later parts of this guide, you need to choose a VM SKU that supports local NVMe drives, for example, [Storage optimized VM SKUs](/en-us/azure/virtual-machines/sizes/overview#storage-optimized) or [GPU accelerated VM SKUs](/en-us/azure/virtual-machines/sizes/overview#gpu-accelerated). Update `$USER_NODE_POOL_VMSKU`

accordingly.

Create an AKS cluster using the

command.`az aks create`

`export SYSTEM_NODE_POOL_VMSKU="standard_d2s_v3" export USER_NODE_POOL_NAME="postgres" export USER_NODE_POOL_VMSKU="standard_d4s_v3" az aks create \ --name $AKS_PRIMARY_CLUSTER_NAME \ --tags $TAGS \ --resource-group $RESOURCE_GROUP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --generate-ssh-keys \ --node-resource-group $AKS_PRIMARY_MANAGED_RG_NAME \ --enable-managed-identity \ --assign-identity $AKS_UAMI_WORKLOAD_RESOURCEID \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --nodepool-name systempool \ --enable-oidc-issuer \ --enable-workload-identity \ --enable-cluster-autoscaler \ --min-count 2 \ --max-count 3 \ --node-vm-size $SYSTEM_NODE_POOL_VMSKU \ --enable-azure-monitor-metrics \ --azure-monitor-workspace-resource-id $AMW_RESOURCE_ID \ --grafana-resource-id $GRAFANA_RESOURCE_ID \ --api-server-authorized-ip-ranges $MY_PUBLIC_CLIENT_IP \ --tier standard \ --kubernetes-version $AKS_CLUSTER_VERSION \ --zones 1 2 3 \ --output table`

Wait for the initial cluster operation to complete using the

command so additional updates, such as adding the user node pool, don’t collide with an in-progress managed-cluster update:`az aks wait`

`az aks wait \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --created`

Add a user node pool to the AKS cluster using the

command.`az aks nodepool add`

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $AKS_PRIMARY_CLUSTER_NAME \ --name $USER_NODE_POOL_NAME \ --enable-cluster-autoscaler \ --min-count 3 \ --max-count 6 \ --node-vm-size $USER_NODE_POOL_VMSKU \ --zones 1 2 3 \ --labels workload=postgres \ --output table`


## Connect to the AKS cluster and create namespaces

In this section, you get the AKS cluster credentials, which serve as the keys that allow you to authenticate and interact with the cluster. Once connected, you create two namespaces: one for the CNPG controller manager services and one for the PostgreSQL cluster and its related services.

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --output none`

Create the namespace for the CNPG controller manager services, the PostgreSQL cluster, and its related services by using the

command.`kubectl create namespace`

`kubectl create namespace $PG_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME kubectl create namespace $PG_SYSTEM_NAMESPACE --context $AKS_PRIMARY_CLUSTER_NAME`


You can now define another environment variable based on your desired storage option, which you reference later in the guide when deploying PostgreSQL.

You can reference the default preinstalled Premium SSD Azure Disks CSI driver storage class:

```
export POSTGRES_STORAGE_CLASS="managed-csi-premium"
```


## Update the monitoring infrastructure

The Azure Monitor workspace for Managed Prometheus and Azure Managed Grafana are automatically linked to the AKS cluster for metrics and visualization during the cluster creation process. In this section, you enable log collection with AKS Container insights and validate that Managed Prometheus is scraping metrics and Container insights is ingesting logs.

Enable Container insights monitoring on the AKS cluster using the

command.`az aks enable-addons`

`az aks enable-addons \ --addon monitoring \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --workspace-resource-id $ALA_RESOURCE_ID \ --output table`

Validate that Managed Prometheus is scraping metrics and Container insights is ingesting logs from the AKS cluster by inspecting the DaemonSet using the

command and the`kubectl get`

command.`az aks show`

`kubectl get ds ama-metrics-node \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace=kube-system kubectl get ds ama-logs \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace=kube-system az aks show \ --resource-group $RESOURCE_GROUP_NAME \ --name $AKS_PRIMARY_CLUSTER_NAME \ --query addonProfiles`

Your output should resemble the following example output, with

*six*nodes total (three for the system node pool and three for the PostgreSQL node pool) and the Container insights showing`"enabled": true`

:`NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR ama-metrics-node 6 6 6 6 6 <none> NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR ama-logs 6 6 6 6 6 <none> { "omsagent": { "config": { "logAnalyticsWorkspaceResourceID": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/rg-cnpg-9vbin3p8/providers/Microsoft.OperationalInsights/workspaces/ala-cnpg-9vbin3p8", "useAADAuth": "true" }, "enabled": true, "identity": null } }`


## Create a public static IP for PostgreSQL cluster ingress

To validate deployment of the PostgreSQL cluster and use client PostgreSQL tooling, such as *psql* and *PgAdmin*, you need to expose the primary and read-only replicas to ingress. In this section, you create an Azure public IP resource that you later supply to an Azure load balancer to expose PostgreSQL endpoints for query.

Get the name of the AKS cluster node resource group using the

command.`az aks show`

`export AKS_PRIMARY_CLUSTER_NODERG_NAME=$(az aks show \ --name $AKS_PRIMARY_CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --query nodeResourceGroup \ --output tsv) echo $AKS_PRIMARY_CLUSTER_NODERG_NAME`

Create the public IP address using the

command.`az network public-ip create`

`export AKS_PRIMARY_CLUSTER_PUBLICIP_NAME="$AKS_PRIMARY_CLUSTER_NAME-pip" az network public-ip create \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --location $PRIMARY_CLUSTER_REGION \ --sku Standard \ --zone 1 2 3 \ --allocation-method static \ --output table`

Get the newly created public IP address using the

command.`az network public-ip show`

`export AKS_PRIMARY_CLUSTER_PUBLICIP_ADDRESS=$(az network public-ip show \ --resource-group $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --name $AKS_PRIMARY_CLUSTER_PUBLICIP_NAME \ --query ipAddress \ --output tsv) echo $AKS_PRIMARY_CLUSTER_PUBLICIP_ADDRESS`

Get the resource ID of the node resource group using the

command.`az group show`

`export AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE=$(az group show --name \ $AKS_PRIMARY_CLUSTER_NODERG_NAME \ --query id \ --output tsv) echo $AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE`

Assign the "Network Contributor" role to the UAMI object ID using the node resource group scope using the

command.`az role assignment create`

`az role assignment create \ --assignee-object-id ${AKS_UAMI_WORKLOAD_OBJECTID} \ --assignee-principal-type ServicePrincipal \ --role "Network Contributor" \ --scope ${AKS_PRIMARY_CLUSTER_NODERG_NAME_SCOPE}`


## Install the CNPG operator in the AKS cluster

In this section, you install the CNPG operator in the AKS cluster using Helm or a YAML manifest.

Add the CNPG Helm repo using the

command.`helm repo add`

`helm repo add cnpg https://cloudnative-pg.github.io/charts`

Upgrade the CNPG Helm repo and install it on the AKS cluster using the

command with the`helm upgrade`

`--install`

flag.`helm upgrade --install cnpg \ --namespace $PG_SYSTEM_NAMESPACE \ --create-namespace \ --kube-context=$AKS_PRIMARY_CLUSTER_NAME \ cnpg/cloudnative-pg`

Verify the operator installation on the AKS cluster using the

command.`kubectl get`

`kubectl get deployment \ --context $AKS_PRIMARY_CLUSTER_NAME \ --namespace $PG_SYSTEM_NAMESPACE cnpg-cloudnative-pg`


## Next steps

## Contributors

*Microsoft maintains this article. The following contributors originally wrote it:*

- Ken Kilty | Principal TPM
- Russell de Pina | Principal TPM
- Adrian Joian | Senior Customer Engineer
- Jenny Hayes | Senior Content Developer
- Carol Smith | Senior Content Developer
- Erin Schaffer | Content Developer 2

## Acknowledgment

This documentation was jointly developed with EnterpriseDB, the maintainers of the CloudNativePG operator. We thank [Gabriele Bartolini](https://cloudnative-pg.io/authors/gbartolini/) for reviewing earlier drafts of this document and offering technical improvements.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-cvm -->

# Use Confidential Virtual Machines (CVM) in Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Confidential Virtual Machines (CVM)](/en-us/azure/confidential-computing/confidential-vm-overview) offer strong security and confidentiality for tenants. CVMs offer VM based Hardware Trusted Execution Environment (TEE) that leverage SEV-SNP security features to deny the hypervisor and other host management code access to VM memory and state, providing defense in depth protections against operator access. These features enable node pools with CVM to target the migration of highly sensitive container workloads to AKS without any code refactoring while benefiting from the features of AKS. For example, you may require CVM if you have the following:

- Workloads that handle security critical data and/or sensitive customer data
- Services that are required to meet various compliance requirements, especially for government contracts. Without a scalable solution for securing data, this could potentially lead to the loss of accreditations and contracts.

In this article, you learn how to create AKS node pools using Confidential VM sizes.

## AKS supported confidential VM sizes

Azure offers a choice of [Trusted Execution Environment (TEE)](/en-us/azure/confidential-computing/trusted-execution-environment) options from both AMD and Intel. These TEEs allow you to create Confidential VM environments with excellent price-to-performance ratios, all without requiring any code changes.

- AMD-based Confidential VMs, use AMD SEV-SNP technology, which is introduced with third Gen AMD EPYC™ processors.
- Intel-based Confidential VMs use Intel TDX, with fourth Gen Intel® Xeon® processors.

Both technologies have different implementations. However both provide similar protections from the cloud infrastructure stack. For more information, see [CVM VM sizes](/en-us/azure/confidential-computing/virtual-machine-options).

## Security Features

CVMs offer the following security enhancements as compared to other virtual machine (VM) sizes:

- Robust hardware-based isolation between virtual machines, hypervisor, and host management code.
- Customizable attestation policies to ensure the host's compliance before deployment.
- Cloud-based Confidential OS disk encryption before the first boot.
- VM encryption keys that the platform or the customer (optionally) owns and manages.
- Secure key release with cryptographic binding between the platform's successful attestation and the VM's encryption keys.
- Dedicated virtual Trusted Platform Module (TPM) instance for attestation and protection of keys and secrets in the virtual machine.
- Secure boot capability similar to Trusted launch for Azure VMs

## How does it work?

If you're running a workload that requires enhanced confidentiality and integrity, you can benefit from memory encryption and enhanced security without code changes in your application. All pods on your CVM node are part of the same trust boundary. The nodes in a node pool created with CVM use a customized [node image](node-images) specially configured for CVM.

### Supported OS Versions

You can create CVM node pools on Linux OS types (Ubuntu and Azure Linux). However, not all OS versions support CVM node pools.

This table includes the supported OS versions:

| OS Type | OS SKU | CVM support | CVM default |
|---|---|---|---|
| Linux | `Ubuntu` |
Supported | Ubuntu 20.04 is default for K8s version 1.24-1.33. Ubuntu 24.04 is the default for K8s version 1.34-1.38. |
| Linux | `Ubuntu2204` |
Not Supported | AKS doesn't support CVM for Ubuntu 22.04. |
| Linux | `Ubuntu2404` |
Supported | CVM is supported on `Ubuntu2404` in K8s 1.32-1.38. |
| Linux | `AzureLinux` |
Supported on Azure Linux 3.0 | Azure Linux 3 is default when enabling CVM for K8s version 1.28-1.36. |
| Linux | `flatcar` |
Not supported |
|

`AzureLinuxOSGuard`

[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard)doesn't support CVM.When using `Ubuntu`

or `AzureLinux`

as the `osSKU`

, if the default OS version doesn't support CVM, AKS defaults to the most recent CVM-supported version of the OS. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support CVM, AKS defaults to Ubuntu 20.04 for Linux CVM-enabled node pools.

### Limitations

The following limitations apply when adding a node pool with CVM to AKS:

- You can't use FIPS, ARM64, Trusted Launch, or Pod Sandboxing.
- You can't update an existing node pool to migrate to a CVM size. To migrate, you'll need to
[resize your node pool](resize-node-pool). - You can't use CVM with Windows node pools.
- CVM with Azure Linux is currently in preview.

## Prerequisites

Before you begin, make sure you have the following:

- An existing AKS cluster.
- CVM sizes must be available for your subscription in the region where the cluster is created. You must have sufficient quota to create a node pool with a CVM size.
- If you're using Azure Linux os, you need to install the
`aks-preview`

extension, update the`aks-preview`

extension, and register the preview feature flag. If you're using Ubuntu, you can skip these steps.

### If you are using Azure Linux

CVMs for Ubuntu is GA, but CVMs with Azure Linux is currently still in preview. If you would like to use CVM node pools with Azure Linux as the OS of choice, ensure you enable the extension and register the flag.

#### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

`az extension update --name aks-preview`


#### Register `AzureLinuxCVMPreview`

feature flag

Register the

`AzureLinuxCVMPreview`

feature flag using the [`az feature register`

][az-feature-register] command.`az feature register --namespace "Microsoft.ContainerService" --name "AzureLinuxCVMPreview"`

Verify the registration status using the [

`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.`az feature show --namespace Microsoft.ContainerService --name AzureLinuxCVMPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Add a node pool with a CVM to your AKS cluster

Add a node pool with a CVM to your AKS cluster using the

command and set the`az aks nodepool add`

`node-vm-size`

to a supported[VM size](/en-us/azure/confidential-computing/virtual-machine-options).`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --node-count 3 \ --node-vm-size Standard_DC4as_v5`


If you don't specify the `osSKU`

or `osType`

, AKS defaults to `--os-type Linux`

and `--os-sku Ubuntu`

.

## Upgrade an existing node pool with a CVM to Ubuntu 24.04

Upgrade an existing node pool with a CVM to Ubuntu 24.04 from Ubuntu 20.04 using the

command. Set the`az aks nodepool update`

`os-sku`

as`Ubuntu2404`

.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --os-sku Ubuntu2404`


Note

A node pool which is Ubuntu 24.04 with a CVM is supported from AKS cluster 1.33 version. Additionally, before Ubuntu 24.04 becomes GA, you need to register the `Ubuntu2404Preview`

feature. For more information, see [ here](/en-us/azure/aks/upgrade-os-version#register-ubuntu2404preview-feature-flag) to register the feature.

## Verify the node pool uses CVM

Verify a node pool uses CVM using the

command and verify the`az aks nodepool show`

`vmSize`

is`Standard_DCa4_v5`

.`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize'`

The following example command and output shows the node pool uses CVM:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'vmSize' "Standard_DC4as_v5"`

Verify a node pool uses a CVM image using the

command.`az aks nodepool list`

`az aks nodepool list \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion'`

The following example command and output shows the node pool uses an Ubuntu 20.04 CVM image:

`az aks nodepool show \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool \ --query 'nodeImageVersion' "AKSUbuntu-2004cvmcontainerd-202507.02.0"`


## Remove a node pool with CVM from an AKS cluster

Remove a node pool with CVM from an AKS cluster using the

command.`az aks nodepool delete`

`az aks nodepool delete \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name cvmnodepool`


## Next steps

In this article, you learned how to add a node pool with CVM to an AKS cluster.

- For more information about CVM, see
[Confidential VM node pools support on AKS](/en-us/azure/confidential-computing/confidential-node-pool-aks). - To migrate an existing node pool to a CVM vm size, you can
[resize your node pool](resize-node-pool). - If you're only interested in enabling Trusted Launch on your node pools, see
[Trusted Launch on AKS](use-trusted-launch).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-deploy-addon-bicep -->

# Deploy the Open Service Mesh add-on using Bicep in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy the Open Service Mesh (OSM) add-on to Azure Kubernetes Service (AKS) using a [Bicep](/en-us/azure/azure-resource-manager/bicep/) template.

Important

Starting on **September 30, 2027**, Azure Kubernetes Service (AKS) no longer supports the Open Service Mesh (OSM) add-on. The [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/) retired the upstream OSM project. [Migrate any existing OSM configurations to equivalent Istio configurations](/en-us/azure/aks/open-service-mesh-istio-migration-guidance). For more information on this retirement, see the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Based on the version of Kubernetes your cluster is running, the OSM add-on installs a different version of OSM.

| Kubernetes version | OSM version installed |
|---|---|
| 1.24.0 or greater | 1.2.5 |
| Between 1.23.5 and 1.24.0 | 1.1.3 |
| Below 1.23.5 | 1.0.0 |

Older versions of OSM may not be available for install or be actively supported if the corresponding AKS version has reached end of life. You can check the [AKS Kubernetes release calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar) for information on AKS version support windows.

[Bicep](/en-us/azure/azure-resource-manager/bicep/overview) is a domain-specific language that uses declarative syntax to deploy Azure resources. You can use Bicep in place of creating [Azure Resource Manager templates](/en-us/azure/azure-resource-manager/templates/overview) to deploy your infrastructure-as-code Azure resources.

## Before you begin

Before you begin, make sure you have the following prerequisites in place:

- The Azure CLI version 2.20.0 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - An SSH public key used for deploying AKS. For more information, see
[Create SSH keys using the Azure CLI](/en-us/azure/virtual-machines/ssh-keys-azure-cli). [Visual Studio Code](https://code.visualstudio.com/)with a Bash terminal.- The Visual Studio Code
[Bicep extension](/en-us/azure/azure-resource-manager/bicep/install).

## Install the OSM add-on for a new AKS cluster by using Bicep

For deployment of a new AKS cluster, you enable the OSM add-on at cluster creation. The following instructions use a generic Bicep template that deploys an AKS cluster by using ephemeral disks and the [ kubenet](configure-kubenet) container network interface, and then enables the OSM add-on. For more advanced deployment scenarios, see

[What is Bicep?](/en-us/azure/azure-resource-manager/bicep/overview)

### Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name <my-osm-bicep-aks-cluster-rg> --location <azure-region>`


### Create the main and parameters Bicep files

Create a directory to store the necessary Bicep deployment files. The following example creates a directory named

*bicep-osm-aks-addon*and changes to the directory:`mkdir bicep-osm-aks-addon cd bicep-osm-aks-addon`

Create the main file and the parameters file.

`touch osm.aks.bicep && touch osm.aks.parameters.json`

Open the

*osm.aks.bicep*file and copy in the following content:`// https://learn.microsoft.com/azure/aks/troubleshooting#what-naming-restrictions-are-enforced-for-aks-resources-and-parameters @minLength(3) @maxLength(63) @description('Provide a name for the AKS cluster. The only allowed characters are letters, numbers, dashes, and underscore. The first and last character must be a letter or a number.') param clusterName string @minLength(3) @maxLength(54) @description('Provide a name for the AKS dnsPrefix. Valid characters include alphanumeric values and hyphens (-). The dnsPrefix can\'t include special characters such as a period (.)') param clusterDNSPrefix string param k8Version string param sshPubKey string param location string param adminUsername string resource aksCluster 'Microsoft.ContainerService/managedClusters@2021-03-01' = { name: clusterName location: location identity: { type: 'SystemAssigned' } properties: { kubernetesVersion: k8Version dnsPrefix: clusterDNSPrefix enableRBAC: true agentPoolProfiles: [ { name: 'agentpool' count: 3 vmSize: 'Standard_DS2_v2' osDiskSizeGB: 30 osDiskType: 'Ephemeral' osType: 'Linux' mode: 'System' } ] linuxProfile: { adminUsername: adminUserName ssh: { publicKeys: [ { keyData: sshPubKey } ] } } addonProfiles: { openServiceMesh: { enabled: true config: {} } } } }`

Open the

*osm.aks.parameters.json*file and copy in the following content. Make sure you replace the deployment parameter values with your own values.Note

The

*osm.aks.parameters.json*file is an example template parameters file needed for the Bicep deployment. Update the parameters specifically for your deployment environment. The parameters you need to add values for include:`clusterName`

,`clusterDNSPrefix`

,`k8Version`

,`sshPubKey`

,`location`

, and`adminUsername`

. To find a list of supported Kubernetes versions in your region, use the`az aks get-versions --location <region>`

command.`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#", "contentVersion": "1.0.0.0", "parameters": { "clusterName": { "value": "<YOUR CLUSTER NAME HERE>" }, "clusterDNSPrefix": { "value": "<YOUR CLUSTER DNS PREFIX HERE>" }, "k8Version": { "value": "<YOUR SUPPORTED KUBERNETES VERSION HERE>" }, "sshPubKey": { "value": "<YOUR SSH KEY HERE>" }, "location": { "value": "<YOUR AZURE REGION HERE>" }, "adminUsername": { "value": "<YOUR ADMIN USERNAME HERE>" } } }`


### Deploy the Bicep files

Open a terminal and authenticate to your Azure account for the Azure CLI using the

`az login`

command.Deploy the Bicep files using the

command.`az deployment group create`

`az deployment group create \ --name OSMBicepDeployment \ --resource-group osm-bicep-test \ --template-file osm.aks.bicep \ --parameters @osm.aks.parameters.json`


## Validate installation of the OSM add-on

Query the add-on profiles of the cluster to check the enabled state of the installed add-ons. The following command should return

`true`

:`az aks list -g <my-osm-aks-cluster-rg> -o json | jq -r '.[].addonProfiles.openServiceMesh.enabled'`

Get the status of the

*osm-controller*using the following`kubectl`

commands.`kubectl get deployments -n kube-system --selector app=osm-controller kubectl get pods -n kube-system --selector app=osm-controller kubectl get services -n kube-system --selector app=osm-controller`


## Access the OSM add-on configuration

You can configure the OSM controller using the OSM MeshConfig resource, and you can view the OSM controller's configuration settings using the Azure CLI.

View the OSM controller's configuration settings using the

`kubectl get`

command.`kubectl get meshconfig osm-mesh-config -n kube-system -o yaml`

Here's an example output of MeshConfig:

`apiVersion: config.openservicemesh.io/v1alpha1 kind: MeshConfig metadata: creationTimestamp: "0000-00-00A00:00:00A" generation: 1 name: osm-mesh-config namespace: kube-system resourceVersion: "2494" uid: 6c4d67f3-c241-4aeb-bf4f-b029b08faa31 spec: certificate: serviceCertValidityDuration: 24h featureFlags: enableEgressPolicy: true enableMulticlusterMode: false enableWASMStats: true observability: enableDebugServer: true osmLogLevel: info tracing: address: jaeger.osm-system.svc.cluster.local enable: false endpoint: /api/v2/spans port: 9411 sidecar: configResyncInterval: 0s enablePrivilegedInitContainer: false envoyImage: mcr.microsoft.com/oss/envoyproxy/envoy:v1.18.3 initContainerImage: mcr.microsoft.com/oss/openservicemesh/init:v0.9.1 logLevel: error maxDataPlaneConnections: 0 resources: {} traffic: enableEgress: true enablePermissiveTrafficPolicyMode: true inboundExternalAuthorization: enable: false failureModeAllow: false statPrefix: inboundExtAuthz timeout: 1s useHTTPSIngress: false`

Notice that

`enablePermissiveTrafficPolicyMode`

is configured to`true`

. In OSM, permissive traffic policy mode bypasses[SMI](https://smi-spec.io/)traffic policy enforcement. In this mode, OSM automatically discovers services that are a part of the service mesh. The discovered services will have traffic policy rules programmed on each Envoy proxy sidecar to allow communications between these services.Warning

Before you proceed, verify that your permissive traffic policy mode is set to

`true`

. If it isn't, change it to`true`

using the following command:`kubectl patch meshconfig osm-mesh-config -n kube-system -p '{"spec":{"traffic":{"enablePermissiveTrafficPolicyMode":true}}}' --type=merge`


## Clean up resources

When you no longer need the Azure resources, delete the deployment's test resource group using the

command.`az group delete`

`az group delete --name osm-bicep-test`

Alternatively, you can uninstall the OSM add-on and the related resources from your cluster. For more information, see

[Uninstall the Open Service Mesh add-on from your AKS cluster](open-service-mesh-uninstall-add-on).

## Next steps

This article showed you how to install the OSM add-on on an AKS cluster and verify that it's installed and running. With the OSM add-on installed on your cluster, you can [deploy a sample application](https://release-v1-0.docs.openservicemesh.io/docs/getting_started/install_apps/) or [onboard an existing application](https://release-v1-0.docs.openservicemesh.io/docs/guides/app_onboarding/) to work with your OSM mesh.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/http-proxy -->

# HTTP proxy support in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to configure Azure Kubernetes Service (AKS) clusters to use an HTTP proxy for outbound internet access.

AKS clusters deployed into managed or custom virtual networks have certain outbound dependencies that are necessary to function properly, which created problems in environments requiring internet access to be routed through HTTP proxies. Nodes had no way of bootstrapping the configuration, environment variables, and certificates necessary to access internet services.

The HTTP proxy feature adds HTTP proxy support to AKS clusters, exposing a straightforward interface that you can use to secure AKS-required network traffic in proxy-dependent environments. With this feature, both AKS nodes and pods are configured to use the HTTP proxy. The feature also enables installation of a trusted certificate authority onto the nodes as part of bootstrapping a cluster. More complex solutions might require creating a chain of trust to establish secure communications across the network.

## Limitations and considerations

The following scenarios are **not** supported:

- Different proxy configurations per node pool
- User/Password authentication
- Custom certificate authorities (CAs) for API server communication
- AKS clusters with Windows node pools
- Node pools using Virtual Machine Availability Sets (VMAS)
- Using * as wildcard attached to a domain suffix for noProxy

`httpProxy`

, `httpsProxy`

, and `trustedCa`

have no value by default. Pods are injected with the following environment variables:

`HTTP_PROXY`

`http_proxy`

`HTTPS_PROXY`

`https_proxy`

`NO_PROXY`

`no_proxy`


To disable the injection of the proxy environment variables, you need to annotate the Pod with `"kubernetes.azure.com/no-http-proxy-vars":"true"`

.

## Before you begin

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Create a configuration file with HTTP proxy values

Create a file and provide values for `httpProxy`

, `httpsProxy`

, and `noProxy`

. If your environment requires it, provide a value for `trustedCa`

.

The schema for the config file looks like this:

```
{
"httpProxy": "string",
"httpsProxy": "string",
"noProxy": [
"string"
],
"trustedCa": "string"
}
```


Review requirements for each parameter:

`httpProxy`

: A proxy URL to use for creating HTTP connections outside the cluster. The URL scheme must be`http`

.`httpsProxy`

: A proxy URL to use for creating HTTPS connections outside the cluster. If not specified, then`httpProxy`

is used for both HTTP and HTTPS connections.`noProxy`

: A list of destination domain names, domains, IP addresses, or other network CIDRs to exclude proxying.`trustedCa`

: A string containing the`base64 encoded`

alternative CA certificate content. Currently only the`PEM`

format is supported.

Important

For compatibility with Go-based components that are part of the Kubernetes system, the certificate **must** support `Subject Alternative Names(SANs)`

instead of the deprecated Common Name certs.

There are differences in applications on how to comply with the environment variable `http_proxy`

, `https_proxy`

, and `no_proxy`

. Curl and Python don't support CIDR in `no_proxy`

, but Ruby does.

Example input:

```
{
"httpProxy": "http://myproxy.server.com:8080",
"httpsProxy": "https://myproxy.server.com:8080",
"noProxy": [
"localhost",
"127.0.0.1"
],
"trustedCA": "LS0tLS1CRUdJTiBDRVJUSUZJQ0FURS0tLS0tCk1JSUgvVENDQmVXZ0F3SUJB...S0tLS0="
}
```


## Create a cluster with an HTTP proxy configuration using the Azure CLI

You can configure an AKS cluster with an HTTP proxy configuration during cluster creation.

Use the

command and pass in your configuration as a JSON file.`az aks create`

`az aks create \ --name $clusterName \ --resource-group $resourceGroup \ --http-proxy-config aks-proxy-config.json \ --generate-ssh-keys`

Your cluster should initialize with the HTTP proxy configured on the nodes.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Update an HTTP proxy configuration

You can update HTTP proxy configurations on existing clusters, including:

- Updating an existing cluster to enable HTTP proxy and adding a new HTTP proxy configuration.
- Updating an existing cluster to change an HTTP proxy configuration.

### HTTP proxy update considerations

The `--http-proxy-config`

parameter should be set to a new JSON file with updated values for `httpProxy`

, `httpsProxy`

, `noProxy`

, and `trustedCa`

if necessary. The update injects new environment variables into pods with the new `httpProxy`

, `httpsProxy`

, or `noProxy`

values. Pods must be rotated for the apps to pick it up, because the environment variable values are injected by a mutating admission webhook.

Note

If switching to a new proxy, the new proxy must already exist for the update to be successful. After the upgrade is completed, you can delete the old proxy.

### Update a cluster to update or enable HTTP proxy

Enable or update HTTP proxy configurations on an existing cluster using the

command.`az aks update`

For example, let's say you created a new file with the base64 encoded string of the new CA cert called

*aks-proxy-config-2.json*. You can update the proxy configuration on your cluster with the following command:`az aks update --name $clusterName --resource-group $resourceGroup --http-proxy-config aks-proxy-config-2.json`


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Disable HTTP proxy on an existing cluster (Preview)

### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Disable HTTP Proxy requires a minimum of 18.0.0b13**.`az extension update --name aks-preview`


### Register `DisableHTTPProxyPreview`

feature flag

Register the

`DisableHTTPProxyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Update cluster to disable HTTP proxy (preview)

Update your cluster to disable HTTP proxy using the

command with`az aks update`

`--disable-http-proxy`

flag.`az aks update --name $clusterName --resource-group $resourceGroup --disable-http-proxy`


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify HTTP proxy is disabled by validating the HTTP proxy configuration isn't set on the pods and nodes using the

`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables aren't set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


### Re-enable HTTP proxy on an existing cluster

When you create a cluster, HTTP proxy is enabled by default. Once you disable HTTP proxy on a cluster, the proxy configuration is saved in the database but the proxy variables are removed from the pods and nodes.

To re-enable HTTP proxy on an existing cluster, use the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--enable-http-proxy`

flag.```
az aks update --name $clusterName --resource-group $resourceGroup --enable-http-proxy
```


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Important

If you had an HTTP proxy configuration on your cluster before disabling, the existing HTTP proxy configuration automatically applies when you re-enable HTTP proxy on that cluster. We recommend verifying the configuration to ensure it meets your current requirements before proceeding. If you want to change your HTTP proxy configuration after re-enabling HTTP proxy, follow the steps to [Update the HTTP proxy configuration on an existing cluster](#update-a-cluster-to-update-or-enable-http-proxy).

## Configure an HTTP proxy configuration using an Azure Resource Manager (ARM) template

You can deploy an AKS cluster with an HTTP proxy using an ARM template.

Review requirements for each parameter:

`httpProxy`

: A proxy URL to use for creating HTTP connections outside the cluster. The URL scheme must be`http`

.`httpsProxy`

: A proxy URL to use for creating HTTPS connections outside the cluster. If not specified, then`httpProxy`

is used for both HTTP and HTTPS connections.`noProxy`

: A list of destination domain names, domains, IP addresses, or other network CIDRs to exclude proxying.`trustedCa`

: A string containing the`base64 encoded`

alternative CA certificate content. Currently only the`PEM`

format is supported.

Important

For compatibility with Go-based components that are part of the Kubernetes system, the certificate

**must**support`Subject Alternative Names (SANs)`

instead of the deprecated Common Name certs.There are differences in applications on how to comply with the environment variable

`http_proxy`

,`https_proxy`

, and`no_proxy`

. Curl and Python don't support CIDR in`no_proxy`

, but Ruby does.Create a template with HTTP proxy parameters. In your template, provide values for

`httpProxy`

,`httpsProxy`

, and`noProxy`

. If necessary, provide a value for`trustedCa`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "true", "httpProxy": "string", "httpsProxy": "string", "noProxy": [ "string" ], "trustedCa": "string" } }`

Deploy your ARM template with the HTTP Proxy configuration. Your cluster should initialize with your HTTP proxy configured on the nodes.


## Update an HTTP proxy configuration

You can update HTTP proxy configurations on existing clusters, including:

- Updating an existing cluster to enable HTTP proxy and adding a new HTTP proxy configuration.
- Updating an existing cluster to change an HTTP proxy configuration.

### HTTP proxy update considerations

The `--http-proxy-config`

parameter should be set to a new JSON file with updated values for `httpProxy`

, `httpsProxy`

, `noProxy`

, and `trustedCa`

if necessary. The update injects new environment variables into pods with the new `httpProxy`

, `httpsProxy`

, or `noProxy`

values. Pods must be rotated for the apps to pick it up, because the environment variable values are injected by a mutating admission webhook.

Note

If switching to a new proxy, the new proxy must already exist for the update to be successful. After the upgrade is completed, you can delete the old proxy.

### Update an ARM template to configure HTTP proxy

In your template, provide new values for

`httpProxy`

,`httpsProxy`

, and`noProxy`

. If necessary, provide a value for`trustedCa`

.The same schema used for CLI deployment exists in the

`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "true", "httpProxy": "string", "httpsProxy": "string", "noProxy": [ "string" ], "trustedCa": "string" } }`

Deploy your ARM template with the updated HTTP Proxy configuration.


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify the HTTP proxy configuration is on the pods and nodes by checking that the environment variables contain the appropriate values for

`http_proxy`

,`https_proxy`

, and`no_proxy`

using the`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables are set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


## Disable HTTP proxy on an existing cluster using an ARM template (Preview)

### Install `aks-preview`

extension

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Disable HTTP Proxy requires a minimum of 18.0.0b13**.`az extension update --name aks-preview`


### Register `DisableHTTPProxyPreview`

feature flag

Register the

`DisableHTTPProxyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name DisableHTTPProxyPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Update cluster to disable HTTP proxy

Update your cluster ARM template to disable HTTP proxy by setting

`enabled`

to`false`

. The same schema used for CLI deployment exists in the`Microsoft.ContainerService/managedClusters`

definition under`"properties"`

, as shown in the following example:`"properties": { ..., "httpProxyConfig": { "enabled": "false", } }`

Deploy your ARM template with HTTP Proxy disabled.


Caution

AKS automatically reimages all node pools in the cluster when you update the proxy configuration on your cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command. You can use

[Pod Disruption Budgets (PDBs)](operator-best-practices-scheduler)to safeguard disruption to critical pods during reimage.

Verify HTTP proxy is disabled by validating that the HTTP Proxy configuration isn't set on the pods and nodes using the

`kubectl describe pod`

command.`kubectl describe {any pod} -n kube-system`

To validate proxy variables aren't set in pods, you can check the environment variables present on the nodes.

`kubectl get nodes kubectl node-shell {node name} cat /etc/environment`


### Re-enable HTTP proxy on an existing cluster

When you create a cluster, HTTP proxy is enabled by default. Once you disable HTTP proxy on a cluster, you can no longer add HTTP proxy configurations to that cluster.

If you want to re-enable HTTP proxy, follow the steps to [Update an HTTP proxy configuration using an ARM template](#update-an-arm-template-to-configure-http-proxy).

## Istio add-on HTTP proxy for External Services

If you're using the [Istio-based service mesh add-on for AKS](istio-about), you must create a Service Entry to enable your applications in the mesh to access noncluster or external resources via the HTTP proxy.

For example:

```
apiVersion: networking.istio.io/v1
kind: ServiceEntry
metadata:
name: proxy
spec:
hosts:
- my-company-proxy.com # ignored
addresses:
- $PROXY_IP/32
ports:
- number: $PROXY_PORT
name: tcp
protocol: TCP
location: MESH_EXTERNAL
```


Create a file and provide values for

`PROXY_IP`

and`PROXY_PORT`

.You can deploy the Service Entry using:

`kubectl apply -f service_proxy.yaml`


## Monitoring add-on configuration

HTTP proxy with the monitoring add-on supports the following configurations:

- Outbound proxy without authentication
- Outbound proxy with trusted cert for Log Analytics endpoint

The following configuration isn't supported:

- Custom Metrics and Recommended Alerts features when using a proxy with trusted certificates

## Next steps

For more information regarding the network requirements of AKS clusters, see [Control egress traffic for cluster nodes in AKS](limit-egress-traffic).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-kms-etcd-encryption -->

# Add Key Management Service (KMS) etcd encryption to an Azure Kubernetes Service (AKS) cluster (legacy)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

This article describes the legacy KMS experience for AKS. For new clusters running Kubernetes version 1.33 or later, we recommend using the new [KMS data encryption](kms-data-encryption) experience, which offers platform-managed keys, customer-managed keys with automatic key rotation, and a simplified configuration experience.

For conceptual information about data encryption options, see [Data encryption at rest concepts for AKS](kms-data-encryption-concepts).

This article shows you how to turn on encryption at rest for a public or private key vault using Azure Key Vault and the Key Management Service (KMS) plugin on AKS. You can use the KMS plugin to:

- Use a key in a key vault for etcd encryption.
- Bring your own keys.
- Provide encryption at rest for secrets stored in etcd.
- Rotate the keys in a key vault.

For more information on using KMS, see [Using a KMS provider for data encryption](https://kubernetes.io/docs/tasks/administer-cluster/kms-provider/).

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/free). - Azure CLI version 2.39.0 or later. Find your version using the
`az --version`

command. If you need to install or upgrade, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Warning

Starting on September 15, 2024, Konnectivity is no longer supported for private key vaults for new subscriptions or subscriptions that didn't previously use this configuration. For subscriptions currently using this configuration or used it in the past 60 days, support continues until AKS version 1.30 reaches end of life for community support.

KMS supports Konnectivity or [API Server VNet Integration](api-server-vnet-integration) for public key vaults.

KMS supports [API Server VNet Integration](api-server-vnet-integration) for both private and public key vaults.

You can use `kubectl get pods -n kube-system`

to verify the results and show that a `konnectivity-agent`

pod is running. If a pod is running, the AKS cluster is using Konnectivity. When you use API Server VNet Integration, you can run the `az aks show --resource-group <resource-group-name> --name <cluster-name>`

command to verify that the `enableVnetIntegration`

setting is set to `true`

.

## Limitations

The following limitations apply when you integrate KMS etcd encryption with AKS:

- Deleting the key, the key vault, or the associated identity isn't supported.
- KMS etcd encryption doesn't work with system-assigned managed identity. The key vault access policy must be set before the feature is turned on. System-assigned managed identity isn't available until after the cluster is created. Consider the cycle dependency.
- Because the firewall blocks traffic from the KMS plugin to Key Vault, two scenarios aren't supported. First, Azure Key Vault can't be configured with the firewall option
*Allow public access from specific virtual networks and IP addresses*. Second, Azure Key Vault can't be configured with*Disable public access*unless[API Server VNet Integration](api-server-vnet-integration)is enabled. - The maximum number of secrets supported by a cluster with KMS turned on is
*2,000*. However, it's important to note that[KMS v2](use-kms-v2)isn't limited by this restriction and can handle a higher number of secrets. - Bring your own (BYO) Azure key vault from another tenant isn't supported.
- With KMS turned on, you can't change the associated key vault mode (public versus private). To
[update a key vault mode](update-kms-key-vault), you must first turn off KMS, and then turn it on again. - If a cluster has KMS turned on and has a private key vault, it must use the
[API Server VNet Integration](api-server-vnet-integration)tunnel. Konnectivity isn't supported. - Using the Virtual Machine Scale Sets API to scale the nodes in the cluster down to zero deallocates the nodes. The cluster then goes down and becomes unrecoverable.
- After you turn off KMS, you can't delete or expire the keys. Such behaviors would cause the API server to stop working.
- For a private cluster with KMS enabled and virtual network integration that uses a private key vault, the network security group (NSG) must allow TCP port 443 from the API server to the private key vault's private endpoint IP address. This limitation needs to be considered when using other rules in the API subnet NSG or cluster subnet NSG.

## Create a key vault and key for a public key vault

The following sections describe how to turn on KMS for a public key vault. You can use a public key vault with or without Azure role-based access control (Azure RBAC).

Warning

Deleting the key or the key vault isn't supported and causes the secrets in the cluster to be unrecoverable.

If you need to recover your key vault or your key, see [Azure Key Vault recovery management with soft delete and purge protection](/en-us/azure/key-vault/general/key-vault-recovery?tabs=azure-cli).

Create a key vault with Azure RBAC using the

command. This example command also exports the key vault resource ID to an environment variable.`az keyvault create`

`export KEY_VAULT_RESOURCE_ID=$(az keyvault create --name $KEY_VAULT --resource-group $RESOURCE_GROUP --enable-rbac-authorization true --query id -o tsv)`

Assign yourself permissions to create a key using the

command. This example assigns the Key Vault Crypto Officer role to the signed-in user.`az role assignment create`

`az role assignment create --role "Key Vault Crypto Officer" --assignee-object-id $(az ad signed-in-user show --query id -o tsv) --assignee-principal-type "User" --scope $KEY_VAULT_RESOURCE_ID`

Create a key using the

command.`az keyvault key create`

`az keyvault key create --name $KEY_NAME --vault-name $KEY_VAULT`

Get the key ID and save it as an environment variable using the

command.`az keyvault key show`

`export KEY_ID=$(az keyvault key show --name $KEY_NAME --vault-name $KEY_VAULT --query 'key.kid' -o tsv) echo $KEY_ID`


## Create a user-assigned managed identity for a public key vault

Create a user-assigned managed identity using the

command.`az identity create`

`az identity create --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP`

Get the identity object ID and save it as an environment variable using the

command.`az identity show`

`export IDENTITY_OBJECT_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'principalId' -o tsv) echo $IDENTITY_OBJECT_ID`

Get the identity resource ID and save it as an environment variable using the

command.`az identity show`

`export IDENTITY_RESOURCE_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'id' -o tsv) echo $IDENTITY_RESOURCE_ID`


## Assign permissions to decrypt and encrypt a public key vault

The following sections describe how to assign decrypt and encrypt permissions for a public key vault with or without Azure RBAC.

-
[Assign permissions for a public key vault with Azure RBAC](#tabpanel_2_rbac-kv) -
[Assign permissions for a public key vault without Azure RBAC](#tabpanel_2_non-rbac-kv)

Assign the Key Vault Crypto User role to give decrypt and encrypt permissions using the

command.`az role assignment create`

`az role assignment create --role "Key Vault Crypto User" --assignee-object-id $IDENTITY_OBJECT_ID --assignee-principal-type "ServicePrincipal" --scope $KEY_VAULT_RESOURCE_ID`


## Enable KMS for a public key vault on an AKS cluster

The following sections describe how to turn on KMS for a public key vault on a new or existing AKS cluster.

### Create an AKS cluster with a public key vault and KMS

Create an AKS cluster with a public key vault and KMS using the

command with the`az aks create`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-id`

parameters.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --assign-identity $IDENTITY_RESOURCE_ID \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-vault-network-access "Public" \ --azure-keyvault-kms-key-id $KEY_ID \ --generate-ssh-keys`


### Enable a public key vault and KMS on an existing AKS cluster

Enable KMS on a public key vault on an existing cluster using the

command with the`az aks update`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-id`

parameters.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-vault-network-access "Public" \ --azure-keyvault-kms-key-id $KEY_ID`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Rotate existing keys in a public key vault

After you change the key ID (including changing either the key name or the key version), you can rotate the existing keys in the public key vault.

Warning

Remember to update all secrets after key rotation. If you don't update all secrets, the secrets are inaccessible if the keys that were created earlier don't exist or no longer work.

KMS uses two keys at the same time. After the first key rotation, you need to ensure both the old and new keys are valid (not expired) until the next key rotation. After the second key rotation, the oldest key can be safely removed/expired.

After rotating KMS key version with the new `keyId`

, check `securityProfile.azureKeyVaultKms.keyId`

in AKS resource json. Ensure the new key version is in use.

Rotate existing keys using the

command with the`az aks update`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-id`

parameters.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-vault-network-access "Public" \ --azure-keyvault-kms-key-id $NEW_KEY_ID`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Create a key vault and key for a private key vault

If you turn on KMS for a private key vault, AKS automatically creates a private endpoint and a private link in the node resource group. The key vault has a private endpoint connection with the AKS cluster.

Warning

Keep the following information in mind when using a private key vault:

- KMS only supports
[API Server VNet Integration](api-server-vnet-integration)for private key vault. - Creating or updating keys in a private key vault that doesn't have a private endpoint isn't supported. To learn how to manage private key vaults, see
[Integrate a key vault by using Azure Private Link](/en-us/azure/key-vault/general/private-link-service). - Deleting the key or the key vault isn't supported and causes the secrets in the cluster to be unrecoverable. If you need to recover your key vault or your key, see
[Azure Key Vault recovery management with soft delete and purge protection](/en-us/azure/key-vault/general/key-vault-recovery?tabs=azure-cli).

Create a private key vault using the

command with the`az keyvault create`

`--public-network-access Disabled`

parameter.`az keyvault create --name $KEY_VAULT --resource-group $RESOURCE_GROUP --public-network-access Disabled`

Create a key using the

command.`az keyvault key create`

`az keyvault key create --name $KEY_NAME --vault-name $KEY_VAULT`


## Create a user-assigned managed identity for a private key vault

Create a user-assigned managed identity using the

command.`az identity create`

`az identity create --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP`

Get the identity object ID and save it as an environment variable using the

command.`az identity show`

`export IDENTITY_OBJECT_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'principalId' -o tsv) echo $IDENTITY_OBJECT_ID`

Get the identity resource ID and save it as an environment variable using the

command.`az identity show`

`export IDENTITY_RESOURCE_ID=$(az identity show --name $IDENTITY_NAME --resource-group $RESOURCE_GROUP --query 'id' -o tsv) echo $IDENTITY_RESOURCE_ID`


## Assign permissions to decrypt and encrypt a private key vault

The following sections describe how to assign decrypt and encrypt permissions for a private key vault with or without Azure RBAC.

-
[Assign permissions for a private key vault with Azure RBAC](#tabpanel_3_rbac-kv) -
[Assign permissions for a private key vault without Azure RBAC](#tabpanel_3_non-rbac-kv)

Assign the Key Vault Crypto User role to give decrypt and encrypt permissions using the

command.`az role assignment create`

`az role assignment create --role "Key Vault Crypto User" --assignee-object-id $IDENTITY_OBJECT_ID --assignee-principal-type "ServicePrincipal" --scope $KEY_VAULT_RESOURCE_ID`


## Assign permissions to create a private link

For private key vaults, the Key Vault Contributor role is required to create a private link between the private key vault and the cluster.

Assign the Key Vault Contributor role using the

command.`az role assignment create`

`az role assignment create --role "Key Vault Contributor" --assignee-object-id $IDENTITY_OBJECT_ID --assignee-principal-type "ServicePrincipal" --scope $KEY_VAULT_RESOURCE_ID`


## Enable KMS for a private key vault on an AKS cluster

The following sections describe how to turn on KMS for a private key vault on a new or existing AKS cluster.

### Create an AKS cluster with a private key vault and KMS

Create an AKS cluster with a private key vault and KMS using the

command with the`az aks create`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-id`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-vault-resource-id`

parameters.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --assign-identity $IDENTITY_RESOURCE_ID \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID \ --generate-ssh-keys`


### Update an existing AKS cluster to turn on KMS etcd encryption for a private key vault

Enable KMS on a private key vault on an existing cluster using the

command with the`az aks update`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-id`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-vault-resource-id`

parameters.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


### Rotate existing keys in a private key vault

After you change the key ID (including changing either the key name or the key version), you can rotate the existing keys in the private key vault.

Warning

Remember to update all secrets after key rotation. If you don't update all secrets, the secrets are inaccessible if the keys that were created earlier don't exist or no longer work.

After you rotate the key, the previous key (key1) is still cached and shouldn't be deleted. If you want to delete the previous key (key1) immediately, you need to rotate the key twice. Then key2 and key3 are cached, and key1 can be deleted without affecting the existing cluster.

After rotating KMS key version with the new `keyId`

, check `securityProfile.azureKeyVaultKms.keyId`

in AKS resource json. Ensure the new key version is in use.

Rotate existing keys in a private key vault using the

command with the`az aks update`

`--enable-azure-keyvault-kms`

,`--azure-keyvault-kms-key-id`

,`--azure-keyvault-kms-key-vault-network-access`

, and`--azure-keyvault-kms-key-vault-resource-id`

parameters.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --enable-azure-keyvault-kms \ --azure-keyvault-kms-key-id $NEW_KEY_ID \ --azure-keyvault-kms-key-vault-network-access "Private" \ --azure-keyvault-kms-key-vault-resource-id $KEY_VAULT_RESOURCE_ID`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Disable KMS on an AKS cluster

Before you turn off KMS, verify that KMS is enabled on the cluster using the

command.`az aks list`

`az aks list --query "[].{Name:name, KmsEnabled:securityProfile.azureKeyVaultKms.enabled, KeyId:securityProfile.azureKeyVaultKms.keyId}" -o table`

Once confirmed, you can disable KMS using the

command with the`az aks update`

`--disable-azure-keyvault-kms`

parameter.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --disable-azure-keyvault-kms`

Update all secrets using the

`kubectl get secrets`

command to ensure the secrets created earlier are no longer encrypted. For larger clusters, you might want to subdivide the secrets by namespace or create an update script. If the previous command to update KMS fails, still run the following command to avoid unexpected state for KMS plugin.`kubectl get secrets --all-namespaces -o json | kubectl replace -f -`

When you run the command, the following error is safe to ignore:

`The object has been modified; please apply your changes to the latest version and try again.`


## Next steps

For more information on using KMS with AKS, see the following articles:

[Enable KMS data encryption in AKS](kms-data-encryption)- The new KMS experience with platform-managed keys and automatic key rotation[Data encryption at rest concepts for AKS](kms-data-encryption-concepts)[Update the key vault mode for an Azure Kubernetes Service (AKS) cluster with KMS etcd encryption](update-kms-key-vault)[Migrate to KMS v2 for etcd encryption in Azure Kubernetes Service (AKS)](use-kms-v2)[Observability for KMS etcd encryption in Azure Kubernetes Service (AKS)](kms-observability)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/update-azure-cni -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-azure-cni -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-node-pools -->

# Upgrade node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to upgrade a single node pool and how to upgrade the cluster control plane for multiple node pools in Azure Kubernetes Service (AKS).

Note

As a best practice, you should upgrade all node pools in an AKS cluster to the same Kubernetes version. The default behavior of [`az aks upgrade`

][az-aks-upgrade] is to upgrade all node pools together with the control plane to achieve this alignment. The ability to upgrade individual node pools lets you perform a rolling upgrade and schedule pods between node pools to maintain application uptime.

## Upgrade a single node pool

Note

The node pool operating system (OS) image version is tied to the Kubernetes version of the cluster. You only get OS image upgrades following a cluster upgrade.

Check for any available upgrades using the [

`az aks get-upgrades`

][az-aks-get-upgrades] command.`az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name>`

Upgrade a specific node pool using the [

`az aks nodepool upgrade`

][az-aks-nodepool-upgrade] command.`az aks nodepool upgrade \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --kubernetes-version <kubernetes-version> \ --no-wait`

Check the status of your node pool using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name>`

The following example output shows the node pool is in the

*Upgrading*state:`[ { ... "count": 3, ... "name": "<node-pool-name>", "orchestratorVersion": "<kubernetes-version>", ... "provisioningState": "Upgrading", ... "vmSize": "Standard_DS2_v2", ... }, { ... "count": 2, ... "name": "<node-pool-name-2>", "orchestratorVersion": "<kubernetes-version-2>", ... "provisioningState": "Succeeded", ... "vmSize": "Standard_DS2_v2", ... } ]`

It takes a few minutes to upgrade the nodes to the specified version. After the upgrade is complete, the node pool's

`provisioningState`

changes to*Succeeded*.

## Upgrade a cluster control plane with multiple node pools

An AKS cluster has two cluster resource objects with Kubernetes versions associated to them: the cluster control plane Kubernetes version and a node pool with a Kubernetes version.

### Upgrade behavior for the control plane and node pools

The control plane maps to one or many node pools. The behavior of an upgrade operation depends on which Azure CLI command you use and the flags you specify:

upgrades the control plane and all node pools in the cluster to the same Kubernetes version.`az aks upgrade`

with the`az aks upgrade`

`--control-plane-only`

flag upgrades only the cluster control plane and leaves all node pools unchanged.upgrades only the target node pool with the specified Kubernetes version.`az aks nodepool upgrade`


### Validation rules for upgrades

Note

Kubernetes uses the standard [Semantic Versioning](https://semver.org/) versioning scheme. The version number is expressed as *x.y.z*, where *x* is the major version, *y* is the minor version, and *z* is the patch version. For example, in version *1.12.6*, *1* is the major version, *12* is the minor version, and *6* is the patch version. The Kubernetes version of the control plane and the initial node pool are set during cluster creation. Other node pools have their Kubernetes version set when they are added to the cluster. The Kubernetes versions may differ between node pools and between a node pool and the control plane.

Kubernetes upgrades for a cluster control plane and node pools are validated using the following sets of rules:

**Rules for valid versions to upgrade node pools**:- The node pool version must have the same
*major*version as the control plane. - The node pool
*minor*version must be within two*minor*versions of the control plane version. - The node pool version can't be greater than the control
`major.minor.patch`

version.

- The node pool version must have the same
**Rules for submitting an upgrade operation**:- You can't downgrade the control plane or a node pool Kubernetes version.
- If a node pool Kubernetes version isn't specified, the behavior depends on the client. In Azure Resource Manager (ARM) templates, declaration falls back to the existing version defined for the node pool. If nothing is set, it falls back to the control plane version.
- You can't simultaneously submit multiple operations on a single control plane or node pool resource. You can either upgrade or scale a control plane or a node pool at a given time.


## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/stop-cluster-upgrade-api-breaking-changes -->

# Stop Azure Kubernetes Service (AKS) cluster upgrades automatically on API breaking changes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to stop Azure Kubernetes Service (AKS) cluster upgrades automatically on API breaking changes.

## Overview

To stay within a supported Kubernetes version, you have to upgrade your cluster at least once per year and prepare for all possible disruptions. These disruptions include ones caused by API breaking changes, deprecations, and dependencies such as Helm and Container Storage Interface (CSI). It can be difficult to anticipate these disruptions and migrate critical workloads without experiencing any downtime.

You can configure your AKS cluster to automatically stop upgrade operations consisting of a minor version change with deprecated APIs and alert you to the issue. This feature helps you avoid unexpected disruptions and gives you time to address the deprecated APIs before proceeding with the upgrade.

## Before you begin

Before you begin, make sure you meet the following prerequisites:

- The upgrade operation is a Kubernetes minor version change for the cluster control plane.
- The Kubernetes version you're upgrading to is 1.26 or later.
- The last seen usage of deprecated APIs for the targeted version you're upgrading to must occur within 12 hours before the upgrade operation. AKS records usage hourly, so any usage of deprecated APIs within one hour isn't guaranteed to appear in the detection.

## Mitigate stopped upgrade operations

If you meet the [prerequisites](#before-you-begin), attempt an upgrade, and receive an error message similar to the following example error message:

```
Bad Request({
"code": "ValidationError",
"message": "Control Plane upgrade is blocked due to recent usage of a Kubernetes API deprecated in the specified version. Please refer to https://kubernetes.io/docs/reference/using-api/deprecation-guide to migrate the usage. To bypass this error, set enable-force-upgrade in upgradeSettings.overrideSettings. Bypassing this error without migrating usage will result in the deprecated Kubernetes API calls failing. Usage details: 1 error occurred:\n\t* usage has been detected on API flowcontrol.apiserver.k8s.io.prioritylevelconfigurations.v1beta1, and was recently seen at: 2023-03-23 20:57:18 +0000 UTC, which will be removed in 1.26\n\n",
"subcode": "UpgradeBlockedOnDeprecatedAPIUsage"
})
```


You have two options to mitigate the issue: you can [remove usage of deprecated APIs (recommended)](#remove-usage-of-deprecated-apis-recommended) or [bypass validation to ignore API changes](#bypass-validation-to-ignore-api-changes).

### Remove usage of deprecated APIs (recommended)

In the Azure portal, navigate to your cluster resource and select

**Diagnose and solve problems**Select

**Create, Upgrade, Delete, and Scale**>**Kubernetes API deprecations**.Wait 12 hours from the time the last deprecated API usage was seen. Read-Only verbs are excluded from the deprecated api usage namely

[Get/List/Watch](https://kubernetes.io/docs/reference/using-api/api-concepts/).(You can also check past API usage by enabling[Container insights](/en-us/azure/azure-monitor/containers/container-insights-log-query#resource-logs)and exploring kube audit logs.)Retry your cluster upgrade.


### Bypass validation to ignore API changes

Note

This method requires you to use the Azure CLI version 2.57 or later. If you have the preview CLI extension installed, you need to update to version `3.0.0b10`

or later. This method isn't recommended, as deprecated APIs in the targeted Kubernetes version might not work long term. We recommend removing them as soon as possible after the upgrade completes.

Bypass validation to ignore API breaking changes and invoke an upgrade. Specify the

`enable-force-upgrade`

flag and set the`upgrade-override-until`

property to define the end of the window during which validation is bypassed. If no value is set, it defaults the window to three days from the current time. The date and time you specify must be in the future.`az aks upgrade --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --kubernetes-version $KUBERNETES_VERSION --enable-force-upgrade --upgrade-override-until 2023-10-01T13:00:00Z`

Note

`Z`

is the zone designator for the zero UTC/GMT offset, also known as 'Zulu' time. This example sets the end of the window to`13:00:00`

GMT. For more information, see[Combined date and time representations](https://wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).

## Next steps

This article showed you how to stop AKS cluster upgrades automatically on API breaking changes. To learn more about more upgrade options for AKS clusters, see [Upgrade options for Azure Kubernetes Service (AKS) clusters](upgrade-cluster).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/availability-zones -->

# Configure availability zones in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Availability zones](/en-us/azure/reliability/availability-zones-overview) help protect your applications and data from datacenter failures. Zones are unique physical locations within an Azure region. Each zone includes one or more datacenters equipped with independent power, cooling, and networking.

Using Azure Kubernetes Service (AKS) with availability zones physically distributes resources across different availability zones within a single region, improving reliability. Deploying nodes in multiple zones doesn't incur additional costs. For more information on AKS reliability features including availability zones, multi-region configurations, reliability during service maintenance, and backup, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks).

This article shows you how to configure AKS resources to use availability zones.

## AKS resources

This diagram shows the Azure resources that are created when you create an AKS cluster:

### AKS control plane

Microsoft hosts the [AKS control plane](/en-us/azure/aks/core-aks-concepts#control-plane), the Kubernetes API server, and services such as `scheduler`

and `etcd`

as a managed service. Microsoft replicates the control plane in multiple zones.

Other resources of your cluster deploy in a managed resource group in your Azure subscription. By default, this resource group is prefixed with *MC_* for *managed cluster* and contains the resources mentioned in the following sections.

### Node pools

Node pools are created as virtual machine scale sets in your Azure subscription.

When you create an AKS cluster, one [system node pool](/en-us/azure/aks/use-system-pools) is required and is created automatically. It hosts critical system pods such as `CoreDNS`

and `metrics-server`

. You can add more [user node pools](/en-us/azure/aks/create-node-pools) to your AKS cluster to host your applications.

There are three ways node pools can be deployed:

- Zone-spanning
- Zone-aligned
- Regional

The system node pool zones are configured when the cluster or node pool is created.

#### Zone-spanning

In this configuration, nodes are spread across all selected zones. These zones are specified by using the `--zones`

parameter.

```
# Create an AKS cluster, and create a zone-spanning system node pool in all three AZs, one node in each AZ
az aks create --resource-group example-rg --name example-cluster --node-count 3 --zones 1 2 3
# Add one new zone-spanning user node pool, two nodes in each
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-a --node-count 6 --zones 1 2 3
```


AKS automatically balances the number of nodes between zones.

If a zonal outage occurs, nodes within the affected zone might be affected, but nodes in other availability zones remain unaffected.

To validate node locations, run the following command:

```
kubectl get nodes -o custom-columns='NAME:metadata.name, REGION:metadata.labels.topology\.kubernetes\.io/region, ZONE:metadata.labels.topology\.kubernetes\.io/zone'
```


```
NAME REGION ZONE
aks-nodepool1-34917322-vmss000000 eastus eastus-1
aks-nodepool1-34917322-vmss000001 eastus eastus-2
aks-nodepool1-34917322-vmss000002 eastus eastus-3
```


#### Zone-aligned

In this configuration, each node is aligned (pinned) to a specific zone. To create three node pools for a region with three availability zones:

```
# # Add three new zone-aligned user node pools, two nodes in each
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-x --node-count 2 --zones 1
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-y --node-count 2 --zones 2
az aks nodepool add --resource-group example-rg --cluster-name example-cluster --name userpool-z --node-count 2 --zones 3
```


This configuration can be used when you need [lower latency between nodes](/en-us/azure/aks/reduce-latency-ppg). It also provides more granular control over scaling operations, or when you're using the [cluster autoscaler](cluster-autoscaler-overview).

Note

If a single workload is deployed across node pools, we recommend setting `--balance-similar-node-groups`

to `true`

to maintain a balanced distribution of nodes across zones for your workloads during scale-up operations.

#### Regional (not using availability zones)

Regional mode is used when the zone assignment isn't set in the deployment template (for example, `"zones"=[]`

or `"zones"=null`

).

In this configuration, the node pool creates regional (not zone-pinned) instances and implicitly places instances throughout the region. There's no guarantee that instances are balanced or spread across zones, or that instances are in the same availability zone.

In the rare case of a full zonal outage, any or all instances within the node pool might be affected.

To validate node locations, run the following command:

```
kubectl get nodes -o custom-columns='NAME:metadata.name, REGION:metadata.labels.topology\.kubernetes\.io/region, ZONE:metadata.labels.topology\.kubernetes\.io/zone'
```


```
NAME REGION ZONE
aks-nodepool1-34917322-vmss000000 eastus 0
aks-nodepool1-34917322-vmss000001 eastus 0
aks-nodepool1-34917322-vmss000002 eastus 0
```


## Deployments

### Pods

Kubernetes is aware of Azure availability zones, and can balance pods across nodes in different zones. In the event a zone becomes unavailable, Kubernetes moves pods away from affected nodes automatically.

As documented in the Kubernetes reference [Well-Known Labels, Annotations and Taints](https://kubernetes.io/docs/reference/labels-annotations-taints/), Kubernetes uses the `topology.kubernetes.io/zone`

label to automatically distribute pods in a replication controller or service across the various available zones available.

To see which pods and nodes are running, run the following command:

```
kubectl describe pod | grep -e "^Name:" -e "^Node:"
```


The `maxSkew`

parameter describes the degree to which pods might be unevenly distributed. Assuming three zones and three replicas, setting this value to `1`

ensures that each zone has at least one pod running:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: my-deployment
spec:
selector:
matchLabels:
app: my-app
template:
metadata:
labels:
app: my-app
spec:
topologySpreadConstraints:
- maxSkew: 1
topologyKey: topology.kubernetes.io/zone
whenUnsatisfiable: DoNotSchedule
labelSelector:
matchLabels:
app: my-app
containers:
- name: my-container
image: my-image
```


### Storage and volumes

By default, Kubernetes versions 1.29 and later use Azure Managed Disks by using zone-redundant storage for Persistent Volume Claims.

These disks are replicated between zones, to enhance the resilience of your applications. This action helps to safeguard your data against datacenter failures.

The following example shows a Persistent Volume Claim that uses Azure Standard SSD in zone-redundant storage:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: azure-managed-disk
spec:
accessModes:
- ReadWriteOnce
storageClassName: managed-csi
#storageClassName: managed-csi-premium
resources:
requests:
storage: 5Gi
```


For zone-aligned deployments, you can create a new storage class with the `skuname`

parameter set to `LRS`

(locally redundant storage). You can then use the new storage class in your Persistent Volume Claim.

Although locally redundant storage disks are less expensive, they aren't zone-redundant, and attaching a disk to a node in a different zone isn't supported.

The following example shows a locally redundant storage Standard SSD storage class:

```
kind: StorageClass
metadata:
name: azuredisk-csi-standard-lrs
provisioner: disk.csi.azure.com
parameters:
skuname: StandardSSD_LRS
#skuname: PremiumV2_LRS
```


### Load balancers

Kubernetes deploys Azure Standard Load Balancer by default, which balances inbound traffic across all zones in a region. If a node becomes unavailable, the load balancer reroutes traffic to healthy nodes.

An example service that uses Azure Load Balancer:

```
apiVersion: v1
kind: Service
metadata:
name: example
spec:
type: LoadBalancer
selector:
app: myapp
ports:
- port: 80
targetPort: 8080
```


Important

Starting on **September 30, 2025**, Azure Kubernetes Service (AKS) no longer supports Basic Load Balancer. To avoid any potential service disruptions, we recommend using Standard Load Balancer for new deployments and [upgrading any existing deployments to the Standard Load Balancer](/en-us/azure/load-balancer/load-balancer-basic-upgrade-guidance). For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/5020) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Limitations

The following limitations apply when you're using availability zones:

- See
[Quotas, virtual machine size restrictions, and region availability in AKS](quotas-skus-regions#supported-vm-sizes). - The number of availability zones used
*can't be changed*after the node pool is created. - Most regions support availability zones.
[See a list of regions](/en-us/azure/reliability/regions-list).

## Related content

- Learn about
[Reliability in AKS](/en-us/azure/reliability/reliability-aks). - Learn about
[system node pools](/en-us/azure/aks/use-system-pools). - Learn about
[user node pools](/en-us/azure/aks/create-node-pools). - Learn about
[load balancers](/en-us/azure/aks/load-balancer-standard). - Get
[best practices for business continuity and disaster recovery in AKS](operator-best-practices-storage).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/rdp -->

# Connect with RDP to Azure Kubernetes Service (AKS) cluster Windows Server nodes for maintenance or troubleshooting

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Throughout the lifecycle of your Azure Kubernetes Service (AKS) cluster, you may need to access an AKS Windows Server node. This access could be for maintenance, log collection, or other troubleshooting operations. You can access the AKS Windows Server nodes using RDP. For security purposes, the AKS nodes aren't exposed to the internet.

Alternatively, if you want to SSH to your AKS Windows Server nodes, you need access to the same key-pair that was used during cluster creation. Follow the steps in [SSH into Azure Kubernetes Service (AKS) cluster nodes](ssh).

This article shows you how to create an RDP connection with an AKS node using their private IP addresses.

## Before you begin

This article assumes that you have an existing AKS cluster with a Windows Server node. If you need an AKS cluster, see the article on [creating an AKS cluster with a Windows container using the Azure CLI](learn/quick-windows-container-deploy-cli). You need the Windows administrator username and password for the Windows Server node you want to troubleshoot. You also need an RDP client such as [Microsoft Remote Desktop](https://aka.ms/rdmac).

If you need to reset the password, use `az aks update`

to change the password.

```
az aks update --resource-group myResourceGroup --name myAKSCluster --windows-admin-password $WINDOWS_ADMIN_PASSWORD
```


If you need to reset the username and password, see [Reset Remote Desktop Services or its administrator password in a Windows VM](/en-us/troubleshoot/azure/virtual-machines/reset-rdp).

You also need the Azure CLI version 2.0.61 or later installed and configured. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Deploy a virtual machine to the same subnet as your cluster

The Windows Server nodes of your AKS cluster don't have externally accessible IP addresses. To make an RDP connection, you can deploy a virtual machine with a publicly accessible IP address to the same subnet as your Windows Server nodes.

The following example creates a virtual machine named *myVM* in the *myResourceGroup* resource group.

You need to get the subnet ID used by your Windows Server node pool and query for:

- The cluster's node resource group
- The virtual network
- The subnet's name
- The subnet ID

```
CLUSTER_RG=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
VNET_NAME=$(az network vnet list --resource-group $CLUSTER_RG --query [0].name -o tsv)
SUBNET_NAME=$(az network vnet subnet list --resource-group $CLUSTER_RG --vnet-name $VNET_NAME --query [0].name -o tsv)
SUBNET_ID=$(az network vnet subnet show --resource-group $CLUSTER_RG --vnet-name $VNET_NAME --name $SUBNET_NAME --query id -o tsv)
```


Now that you've the SUBNET_ID, run the following command in the same Azure Cloud Shell window to create the VM:

```
PUBLIC_IP_ADDRESS="myVMPublicIP"
az vm create \
--resource-group myResourceGroup \
--name myVM \
--image win2019datacenter \
--admin-username azureuser \
--admin-password {admin-password} \
--subnet $SUBNET_ID \
--nic-delete-option delete \
--os-disk-delete-option delete \
--nsg "" \
--public-ip-address $PUBLIC_IP_ADDRESS \
--query publicIpAddress -o tsv
```


The following example output shows the VM has been successfully created and displays the public IP address of the virtual machine.

```
13.62.204.18
```


Record the public IP address of the virtual machine. You'll use this address in a later step.

## Allow access to the virtual machine

AKS node pool subnets are protected with NSGs (Network Security Groups) by default. To get access to the virtual machine, you'll have to enabled access in the NSG.

Note

The NSGs are controlled by the AKS service. Any change you make to the NSG will be overwritten at any time by the control plane.

First, get the resource group and name of the NSG to add the rule to:

```
CLUSTER_RG=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
NSG_NAME=$(az network nsg list --resource-group $CLUSTER_RG --query [].name -o tsv)
```


Then, create the NSG rule:

```
az network nsg rule create \
--name tempRDPAccess \
--resource-group $CLUSTER_RG \
--nsg-name $NSG_NAME \
--priority 100 \
--destination-port-range 3389 \
--protocol Tcp \
--description "Temporary RDP access to Windows nodes"
```


## Get the node address

To manage a Kubernetes cluster, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. If you use Azure Cloud Shell, `kubectl`

is already installed. To install `kubectl`

locally, use the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command:

```
az aks install-cli
```


To configure `kubectl`

to connect to your Kubernetes cluster, use the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSCluster
```


List the internal IP address of the Windows Server nodes using the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command:

```
kubectl get nodes -o wide
```


The following example output shows the internal IP addresses of all the nodes in the cluster, including the Windows Server nodes.

```
$ kubectl get nodes -o wide
NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME
aks-nodepool1-42485177-vmss000000 Ready agent 18h v1.12.7 10.240.0.4 <none> Ubuntu 16.04.6 LTS 4.15.0-1040-azure docker://3.0.4
aksnpwin000000 Ready agent 13h v1.12.7 10.240.0.67 <none> Windows Server Datacenter 10.0.17763.437
```


Record the internal IP address of the Windows Server node you wish to troubleshoot. You'll use this address in a later step.

## Connect to the virtual machine and node

Connect to the public IP address of the virtual machine you created earlier using an RDP client such as [Microsoft Remote Desktop](https://aka.ms/rdmac).

After you have connected to your virtual machine, connect to the *internal IP address* of the Windows Server node you want to troubleshoot using an RDP client from within your virtual machine.

You're now connected to your Windows Server node.

You can now run any troubleshooting commands in the *cmd* window. Since Windows Server nodes use Windows Server Core, there's not a full GUI or other GUI tools when you connect to a Windows Server node over RDP.

## Remove RDP access

When done, exit the RDP connection to the Windows Server node then exit the RDP session to the virtual machine. After you exit both RDP sessions, delete the virtual machine with the [az vm delete](/en-us/cli/azure/vm#az-vm-delete) command:

```
# Delete the virtual machine
az vm delete \
--resource-group myResourceGroup \
--name myVM
```


Delete the public IP associated with the virtual machine:

```
az network public-ip delete \
--resource-group myResourceGroup \
--name $PUBLIC_IP_ADDRESS
```


Delete the NSG rule:

```
CLUSTER_RG=$(az aks show --resource-group myResourceGroup --name myAKSCluster --query nodeResourceGroup -o tsv)
NSG_NAME=$(az network nsg list --resource-group $CLUSTER_RG --query [].name -o tsv)
az network nsg rule delete \
--resource-group $CLUSTER_RG \
--nsg-name $NSG_NAME \
--name tempRDPAccess
```


## Connect with Azure Bastion

Alternatively, you can use [Azure Bastion](/en-us/azure/bastion/bastion-overview) to connect to your Windows Server node.

### Deploy Azure Bastion

To deploy Azure Bastion, you'll need to find the virtual network your AKS cluster is connected to.

- In the Azure portal, go to
**Virtual networks**. Select the virtual network your AKS cluster is connected to. - Under
**Settings**, select**Bastion**, then select**Deploy Bastion**. Wait until the process is finished before going to the next step.

### Connect to your Windows Server nodes using Azure Bastion

Go to the node resource group of the AKS cluster. Run the command below in the Azure Cloud Shell to get the name of your node resource group:

```
az aks show --name myAKSCluster --resource-group myResourceGroup --query 'nodeResourceGroup' -o tsv
```


- Select
**Overview**, and select your Windows node pool virtual machine scale set. - Under
**Settings**, select**Instances**. Select a Windows server node that you'd like to connect to. - Under
**Support + troubleshooting**, select**Bastion**. - Enter the credentials you set up when the AKS cluster was created. Select
**Connect**.

You can now run any troubleshooting commands in the *cmd* window. Since Windows Server nodes use Windows Server Core, there's not a full GUI or other GUI tools when you connect to a Windows Server node over RDP.

Note

If you close out of the terminal window, press **CTRL + ALT + End**, select **Task Manager**, select **More details**, select **File**, select **Run new task**, and enter **cmd.exe** to open another terminal. You can also logout and re-connect with Bastion.

### Remove Bastion access

When you're finished, exit the Bastion session and remove the Bastion resource.

- In the Azure portal, go to
**Bastion**and select the Bastion resource you created. - At the top of the page, select
**Delete**. Wait until the process is complete before proceeding to the next step. - In the Azure portal, go to
**Virtual networks**. Select the virtual network that your AKS cluster is connected to. - Under
**Settings**, select**Subnet**, and delete the**AzureBastionSubnet**subnet that was created for the Bastion resource.

## Next steps

If you need more troubleshooting data, you can [view the Kubernetes primary node logs](monitor-aks#aks-control-plane-resource-logs) or [Azure Monitor](/en-us/azure/azure-monitor/containers/container-insights-overview).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-ipam-and-dataplane -->

# Update Azure CNI IPAM mode and data plane technology for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Existing Azure Kubernetes Service (AKS) clusters inevitably need an update to newer IP assignment management (IPAM) modes and data plane technologies to access the latest features and supportability. This article provides guidance on updating an existing AKS cluster to use Azure CNI Overlay for the IPAM mode and Azure CNI Powered by Cilium as the data plane.

## Update the IPAM mode to Azure CNI Overlay

Updating an existing cluster to Azure CNI Overlay is an irreversible process.

You can update an existing AKS cluster to Azure CNI Overlay if the cluster:

- Is on Kubernetes version 1.27 or later.
- Doesn't use the
[dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)feature. - Doesn't have network policies enabled. If you need to uninstall the network policy engine before updating your cluster, follow the steps in
[Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico). - Doesn't use any Windows node pools with Docker as the container runtime.

Before Windows OS build 20348.1668, there was a limitation around Windows overlay pods incorrectly routing packets from host network pods via Source Network Address Translation (SNAT). This limitation had a detrimental effect for clusters that were updating to Azure CNI Overlay. To avoid this issue, use Windows OS build 20348.1668 or later.

Warning

If you're using a custom

`azure-ip-masq-agent`

configuration to include additional IP ranges that shouldn't send SNAT packets from pods, updating to Azure CNI Overlay can break connectivity to these ranges. Pod IPs from the overlay space are unreachable by anything outside the cluster nodes.For old clusters, a ConfigMap might be left over from a previous version of

`azure-ip-masq-agent`

. If this ConfigMap (named`azure-ip-masq-agent-config`

) exists and isn't intentionally in place, you should delete it before updating.If you're not using a custom

`ip-masq-agent`

configuration, only the`azure-ip-masq-agent-config-reconciled`

ConfigMap should exist with respect to Azure`ip-masq-agent`

ConfigMap. It's updated automatically during the update process.

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately to Azure CNI Overlay isn't supported. Any disruptions to cluster networking are similar to a node image update or Kubernetes version upgrade where each node in a node pool is reimaged.

Update an existing Azure Container Networking Interface (CNI) cluster to use Azure CNI Overlay by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16
```


The `--pod-cidr`

parameter is required when you update from legacy CNI plugins because the pods need to get IPs from a new overlay space. The new overlay space doesn't overlap with the existing Azure CNI Node Subnet plugin.

Classless Inter-Domain Routing (CIDR) for the pod also can't overlap with any virtual network address of the node pools. For example, if your virtual network address is 10.0.0.0/8, and your nodes are in the subnet 10.240.0.0/16, the `--pod-cidr`

parameter can't overlap with 10.0.0.0/8 or the existing service CIDR on the cluster.

## Update the data plane to Azure CNI Powered by Cilium

When you enable Cilium in a cluster that uses a different network policy engine (Azure Network Policy Manager or Calico), the network policy engine is uninstalled and replaced with Cilium. For more information, see [Uninstall Azure Network Policy Manager or Calico](use-network-policies#uninstall-azure-network-policy-manager-or-calico).

You can update an existing cluster to Azure CNI Powered by Cilium if the cluster doesn't have any Windows node pools.

Warning

The update process triggers node pools to be reimaged simultaneously. Updating each node pool separately isn't supported. Any disruptions to cluster networking are similar to a node image update or [Kubernetes version upgrade](upgrade-cluster) where each node in a node pool is reimaged. Cilium begins enforcing network policies only after all nodes are reimaged.

To perform the update, you need Azure CLI version 2.52.0 or later. Run `az --version`

to see the currently installed version. If you need to install or upgrade, see [Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

Update an existing cluster to Azure CNI Powered by Cilium by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--network-dataplane cilium
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/gpu-health-monitoring -->

# GPU health monitoring in Node Problem Detector (NPD) in Azure Kubernetes Service (AKS) nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how Azure Kubernetes Service (AKS) uses Node Problem Detector (NPD) to monitor the health of GPU-enabled node pools. NPD is a Kubernetes component that detects and reports node-level issues, including hardware faults, driver errors, and connectivity problems that can affect the performance and availability of GPU workloads.

## About GPU health monitoring in NPD

AKS supports GPU health monitoring through [Node Problem Detector (NPD)](node-problem-detector), enabling automatic detection and reporting of issues that affect GPU-enabled node pools on an AKS cluster. GPU health monitoring helps Kubernetes operators keep GPU nodes healthy and performant by surfacing hardware faults, communication failures, and system-level errors. NPD sets GPU-related node conditions and enable platform engineering teams to take action before issues impact application performance or availability.

These health signals are vital for ensuring optimal performance and reliability across a range of GPU workloads, including:

- Machine learning (ML) training and inference.
- AI model development.
- High-performance computing (HPC).
- Graphics rendering and data-intensive simulations.

## Limitations

AKS Node Problem Detector * does not* run GPU health checks on node pools with

`--gpu-driver none`

, where **self-managed**or custom GPU driver was installed on the nodes.

## Supported GPU health checks

NPD regularly monitors GPU-enabled node pools and sets conditions when anomalies are detected. The following GPU health checks are currently supported:

**GPUMissing**: NPD verifies that the number of GPUs detected by the`nvidia-smi`

utility matches the expected GPU count for the VM SKU assigned to the node.- A mismatch might indicate a hardware fault, driver issue, or misconfiguration. Accurate GPU enumeration is critical for ensuring scheduling accuracy and workload availability on GPU nodes.

**GPUXIDErrors**: Checks for XID (eXecution ID) errors emitted by the GPU driver in the kernel logs. XID errors are low-level GPU faults that typically occur when:- The driver misprograms the GPU.
- There's a corruption in the command stream sent to the GPU.
- A hardware failure or instability affects GPU operation.

For more information, see

[XID errors on NVIDIA GPUs](https://docs.nvidia.com/deploy/xid-errors/index.html).**NVLink Status**: For NVIDIA VM SKUs that support NVLink, this condition confirms that NVLink is active and functioning.- NVLink is a high-speed interconnect used to facilitate data transfer between multiple GPUs.
- If NVLink is inactive or degraded, multi-GPU workloads might experience reduced performance or communication bottlenecks.

For more information, see

[NVIDIA NVLink](https://www.nvidia.com/en-us/data-center/nvlink/).**InfiniBand Link Flapping**: NPD monitors for InfiniBand (IB) link flapping, or intermittent connectivity of the IB network device.- Link flapping shouldn't occur under normal operating conditions and might result in degraded inter-node communication for distributed workloads.
- It can also signal physical layer issues, misconfigured firmware, or driver instability.

**NVIDIA GRID Driver License Check**: For NVIDIA VM SKUs that support GRID driver, this condition verifies license status of the installed GRID driver on[supported NVIDIA VM SKUs](/en-us/azure/virtual-machines/sizes/gpu-accelerated/nvadsa10v5-series).- Invalid might indicate the installed GRID driver is not licensed.


## Frequently asked questions

### Does Node Problem Detector (NPD) automatically remediate GPU node issues?

NPD doesn't take direct action to remediate GPU-enabled node issues. NPD detects and reports problems by publishing Kubernetes node conditions and events. Any remediation (for example: draining a node, restarting workloads, or replacing faulty hardware) must be handled manually, through external automation, or alerting systems configured by the Kubernetes operator.

### On which Azure VM sizes does AKS conduct GPU health monitoring through NPD?

Currently, NPD conducts health checks on GPU nodes provisioned with the `Standard_ND96asr_v4`

or `Standard_ND96isr_H100_v5`

VM size on AKS. Also on [A10 SKU](/en-us/azure/virtual-machines/sizes/gpu-accelerated/nvadsa10v5-series) for GRID Driver License checks.

### Does NPD monitor the health of multi-instance GPU (MIG) node pools?

Yes, NPD health monitoring is supported on [MIG-enabled AKS node pools](gpu-multi-instance).

## Next steps

- Provision GPUs on
[Linux](use-nvidia-gpu)or[Windows](use-windows-gpu)node pools in your AKS cluster. - Learn more about the
[types of node conditions and events](node-problem-detector)set by NPD on AKS. [Monitor general GPU metrics](monitor-gpu-metrics)using a self-managed metrics exporter.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/long-term-support -->

# Long-term support for Azure Kubernetes Service (AKS) versions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Kubernetes community releases a new minor version approximately every four months, with a support window for each version for one year. In Azure Kubernetes Service (AKS), this support window is called *community support*.

AKS supports versions of Kubernetes that are within this *community support* window to push bug fixes and security updates from community releases. While the community support release cadence provides benefits, it requires that you keep up to date with Kubernetes releases, which can be difficult depending on your application's dependencies and the pace of change in the Kubernetes ecosystem.

To help you manage your Kubernetes version upgrades, AKS provides a *long-term support* (LTS) option, which extends the support window for a Kubernetes version to give you more time to plan and test upgrades to newer Kubernetes versions.

## AKS support types

After approximately one year, a given Kubernetes minor version exits *community support*, making bug fixes and security updates unavailable for your AKS clusters.

AKS offers one year of *community support* and one year of *long-term support* to backport security fixes from the upstream community. The upstream LTS working group contributes to the community, extending the support window. LTS provides more time to plan and test upgrades over two years from the Kubernetes version's general availability (GA).

| Community support | Long-term support | |
|---|---|---|
When to use |
When you can keep up with upstream Kubernetes releases | When you need control over when to migrate from one version to another |
Supported versions |
Three most recent GA minor versions | All supported Kubernetes versions from 1.27 onward are eligible for Long-Term Support (LTS). |

## LTS Patch process

LTS supports only the two most recent patch versions. This differs from Community support, where all patch versions are supported. However, AKS reserves the right to deprecate any patch version in response to critical security vulnerabilities (CVEs). For more details on community support policy, see [Kubernetes version support policy](supported-kubernetes-versions#kubernetes-version-support-policy).

To identify the latest supported patch versions, refer to the [AKS release tracker](https://releases.aks.azure.com/webpage/index.html).

We recommend enabling the [auto-upgrade patch channel](auto-upgrade-cluster) to ensure your clusters remain up-to-date with the latest patches.

## Enable long-term support

**Enabling LTS requires moving your cluster to the Premium tier and explicitly selecting the LTS support plan**. While it's possible to enable LTS when the cluster is in *community support*, you're charged once you enable the Premium tier.

Note

We strongly recommend enabling the patch auto-upgrade channel to ensure your cluster always receives the latest supported patches. LTS only supports the last two patch versions for each minor version. Clusters not on the latest patches may lose support.

### Enable LTS on a new cluster

Create a new cluster with LTS enabled using the

command.`az aks create`

The following command creates a new AKS cluster with LTS enabled using Kubernetes version 1.27 as an example. To review available Kubernetes releases, see the

[AKS release tracker](release-tracker).`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --tier premium \ --k8s-support-plan AKSLongTermSupport \ --kubernetes-version 1.27 \ --auto-upgrade-channel patch \ --generate-ssh-keys`


### Enable LTS on an existing cluster

Enable LTS on an existing cluster using the

command.`az aks update`

`az aks update --resource-group <resource-group-name> --name <cluster-name> --tier premium --k8s-support-plan AKSLongTermSupport --auto-upgrade-channel patch`


Tip

To see which Kubernetes versions you can upgrade to, use the [AKS release tracker](https://releases.aks.azure.com/webpage/index.html) or run `az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name>`

.

## Migrate to the latest LTS version

The upstream Kubernetes community supports a two-minor-version upgrade path. The process migrates the objects in your Kubernetes cluster as part of the upgrade process, and provides a tested and accredited migration path.

If you want to carry out an in-place migration, the AKS service migrates your control plane from the previous LTS version to the latest, and then migrate your data plane. To carry out an in-place upgrade to the latest LTS version, you need to specify an LTS enabled Kubernetes version as the upgrade target.

Migrate to the latest LTS version using the

command.`az aks upgrade`

The following command uses Kubernetes version 1.32.2 as an example version. To review available Kubernetes releases, see the

[AKS release tracker](release-tracker).`az aks upgrade --resource-group <resource-group-name> --name <cluster-name> --kubernetes-version 1.32.2`

Note

Moving forward, all AKS Kubernetes versions will be LTS-compatible. For the latest LTS calendar, visit the

[AKS Kubernetes Release Calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar). To view available LTS releases and their patches by region, see the[AKS release tracker](release-tracker).

## Disable long-term support on an existing cluster

**Disabling LTS on an existing cluster requires moving your cluster to the free or standard tier and explicitly selecting the KubernetesOfficial support plan**.

There are approximately two years between one LTS version and the next. In lieu of upstream support for migrating more than two minor versions, there's a high likelihood your application depends on Kubernetes APIs that are deprecated. We recommend you thoroughly test your application on the target LTS Kubernetes version and carry out a blue/green deployment from one version to another.

Disable LTS on an existing cluster using the

command.`az aks update`

`az aks update --resource-group <resource-group-name> --name <cluster-name> --tier [free|standard] --k8s-support-plan KubernetesOfficial`

Upgrade the cluster to a later supported version using the

command.`az aks upgrade`

The following command uses Kubernetes version 1.28.3 as an example version. To review available Kubernetes releases, see the

[AKS release tracker](release-tracker).`az aks upgrade --resource-group <resource-group-name> --name <cluster-name> --kubernetes-version 1.28.3`


## Unsupported add-ons and features

The AKS team currently tracks add-on versions where Kubernetes community support exists. Once a version leaves community support, we rely on open-source projects for managed add-ons to continue that support. Due to various external factors, some add-ons and features might not support Kubernetes versions outside these upstream community support windows.

The following table provides a list of add-ons and features that aren't supported and the reasons they're unsupported:

| Add-on / Feature | Reason it's unsupported |
|---|---|
| Calico | Requires Calico Enterprise agreement past community support. |
| Key Management Service (KMS) | KMSv2 replaces KMS during this LTS cycle. |
| Dapr | AKS extensions aren't supported. |
| Application Gateway Ingress Controller | Migration to App Gateway for Containers happens during LTS period. |
| Open Service Mesh | OSM is deprecated. |
| AAD Pod Identity | Deprecated in place of Workload Identity. |

Note

You can't move your cluster to long-term support if any of these add-ons or features are enabled.

While these AKS managed add-ons aren't supported by Microsoft, you can install their open-source versions on your cluster if you want to use them past community support.

## How we decide the next LTS version

Versions of Kubernetes LTS are available for two years from GA, and we mark a higher version of Kubernetes as LTS based on the following criteria:

- That sufficient time elapsed for customers to migrate from the prior LTS version to the current LTS version.
- The previous version completed a two year support window.

Read the [AKS release notes](https://github.com/Azure/AKS/releases) to stay informed of when you're able to plan your migration.

## Frequently asked questions

### Can I create a new AKS cluster with an LTS version after community support ends?

Yes, you can create a new AKS cluster using an LTS version even after its community support period has ended, provided you have opted into LTS. However, this is only valid until the end of the LTS version's lifecycle. After that, you must upgrade to the next supported LTS version. For more details, see the [AKS Kubernetes Release Calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar).

### Can I enable and disable LTS on an AKS-supported version after community support ends?

Yes, you can enable the LTS support plan on any AKS-supported version even after its community support period has ended. However, once the community support period has ended, you can't disable LTS for that version.

### Does a community-supported AKS cluster automatically become LTS eligible after End of Life?

No, you must explicitly enable LTS on the cluster to receive support. This also requires upgrading to the Premium tier. Refer to the [Premium tier pricing](https://azure.microsoft.com/pricing/details/kubernetes-service/) for more information.

### Will every AKS version support Long-Term Support (LTS)?

Yes, AKS ensures that all supported Kubernetes versions are eligible for Long-Term Support (LTS). You can opt into LTS for any supported version available today.

### What is the pricing model for LTS?

LTS is available on the Premium tier refer to the [Premium tier pricing](https://azure.microsoft.com/pricing/details/kubernetes-service/) for more information.

### Will enabling LTS disrupt workloads?

No. It’s a configuration-only change; it doesn’t reimage nodes or disrupt workloads, so no downtime is expected.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ingress-basic -->

# Create an unmanaged ingress controller

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An ingress controller is a piece of software that provides reverse proxy, configurable traffic routing, and TLS termination for Kubernetes services. Kubernetes ingress resources are used to configure the ingress rules and routes for individual Kubernetes services. When you use an ingress controller and ingress rules, a single IP address can be used to route traffic to multiple services in a Kubernetes cluster.

This article shows you how to deploy the [NGINX ingress controller](https://github.com/kubernetes/ingress-nginx) in an Azure Kubernetes Service (AKS) cluster. Two applications are then run in the AKS cluster, each of which is accessible over the single IP address.

Important

The Application routing add-on is recommended for ingress in AKS. For more information, see [Managed nginx Ingress with the application routing add-on](/en-us/azure/aks/app-routing).

Note

There are two open source ingress controllers for Kubernetes based on Nginx: one is maintained by the Kubernetes community ([kubernetes/ingress-nginx](https://github.com/kubernetes/ingress-nginx)), and one is maintained by NGINX, Inc. ([nginxinc/kubernetes-ingress](https://github.com/nginxinc/kubernetes-ingress)). This article will be using the Kubernetes community ingress controller.

## Before you begin

- This article uses Helm 3 to install the NGINX ingress controller on a
[supported version of Kubernetes](/en-us/azure/aks/supported-kubernetes-versions). Make sure that you're using the latest release of Helm and have access to the*ingress-nginx*Helm repository. The steps outlined in this article may not be compatible with previous versions of the Helm chart, NGINX ingress controller, or Kubernetes. - This article assumes you have an existing AKS cluster with an integrated Azure Container Registry (ACR). For more information on creating an AKS cluster with an integrated ACR, see
[Authenticate with Azure Container Registry from Azure Kubernetes Service](/en-us/azure/aks/cluster-container-registry-integration#create-a-new-acr). - The Kubernetes API health endpoint,
`healthz`

was deprecated in Kubernetes v1.16. You can replace this endpoint with the`livez`

and`readyz`

endpoints instead. See[Kubernetes API endpoints for health](https://kubernetes.io/docs/reference/using-api/health-checks/#api-endpoints-for-health)to determine which endpoint to use for your scenario. - If you're using Azure CLI, this article requires that you're running the Azure CLI version 2.0.64 or later. Run
`az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI][azure-cli-install]. - If you're using Azure PowerShell, this article requires that you're running Azure PowerShell version 5.9.0 or later. Run
`Get-InstalledModule -Name Az`

to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-azure-powershell).

## Basic configuration

To create a basic NGINX ingress controller without customizing the defaults, you'll use Helm. The following configuration uses the default configuration for simplicity. You can add parameters for customizing the deployment, like `--set controller.replicaCount=3`

.

Note

If you would like to enable [client source IP preservation](/en-us/azure/aks/concepts-network-ingress#ingress-controllers) for requests to containers in your cluster, add `--set controller.service.externalTrafficPolicy=Local`

to the Helm install command. The client source IP is stored in the request header under *X-Forwarded-For*. When you're using an ingress controller with client source IP preservation enabled, TLS pass-through won't work.

```
NAMESPACE=ingress-basic
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
helm install ingress-nginx ingress-nginx/ingress-nginx \
--create-namespace \
--namespace $NAMESPACE \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.service.externalTrafficPolicy=Local
```


Note

In this tutorial, `service.beta.kubernetes.io/azure-load-balancer-health-probe-request-path`

is being set to `/healthz`

. This means if the response code of the requests to `/healthz`

is not `200`

, the entire ingress controller will be down. You can modify the value to other URI in your own scenario. You cannot delete this part or unset the value, or the ingress controller will still be down.
The package `ingress-nginx`

used in this tutorial, which is provided by [Kubernetes official](https://github.com/kubernetes/ingress-nginx), will always return `200`

response code if requesting `/healthz`

, as it is designed as [default backend](https://kubernetes.github.io/ingress-nginx/user-guide/default-backend/) for users to have a quick start, unless it is being overwritten by ingress rules.

## Customized configuration

As an alternative to the basic configuration presented in the above section, the next set of steps will show how to deploy a customized ingress controller. You'll have the option of using an internal static IP address, or using a dynamic public IP address.

### Import the images used by the Helm chart into your ACR

To control image versions, you'll want to import them into your own Azure Container Registry. The [NGINX ingress controller Helm chart](https://github.com/kubernetes/ingress-nginx/tree/main/charts/ingress-nginx) relies on three container images. Use `az acr import`

to import those images into your ACR.

```
REGISTRY_NAME=<REGISTRY_NAME>
SOURCE_REGISTRY=registry.k8s.io
CONTROLLER_IMAGE=ingress-nginx/controller
CONTROLLER_TAG=v1.8.1
PATCH_IMAGE=ingress-nginx/kube-webhook-certgen
PATCH_TAG=v20230407
DEFAULTBACKEND_IMAGE=defaultbackend-amd64
DEFAULTBACKEND_TAG=1.5
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$CONTROLLER_IMAGE:$CONTROLLER_TAG --image $CONTROLLER_IMAGE:$CONTROLLER_TAG
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$PATCH_IMAGE:$PATCH_TAG --image $PATCH_IMAGE:$PATCH_TAG
az acr import --name $REGISTRY_NAME --source $SOURCE_REGISTRY/$DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG --image $DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG
```


Note

In addition to importing container images into your ACR, you can also import Helm charts into your ACR. For more information, see [Push and pull Helm charts to an Azure Container Registry](/en-us/azure/container-registry/container-registry-helm-repos).

### Create an ingress controller

To create the ingress controller, use Helm to install *ingress-nginx*. The ingress controller needs to be scheduled on a Linux node. Windows Server nodes shouldn't run the ingress controller. A node selector is specified using the `--set nodeSelector`

parameter to tell the Kubernetes scheduler to run the NGINX ingress controller on a Linux-based node.

For added redundancy, two replicas of the NGINX ingress controllers are deployed with the `--set controller.replicaCount`

parameter. To fully benefit from running replicas of the ingress controller, make sure there's more than one node in your AKS cluster.

The following example creates a Kubernetes namespace for the ingress resources named *ingress-basic* and is intended to work within that namespace. Specify a namespace for your own environment as needed. If your AKS cluster isn't Kubernetes role-based access control enabled, add `--set rbac.create=false`

to the Helm commands.

Note

If you would like to enable [client source IP preservation](/en-us/azure/aks/concepts-network-ingress#ingress-controllers) for requests to containers in your cluster, add `--set controller.service.externalTrafficPolicy=Local`

to the Helm install command. The client source IP is stored in the request header under *X-Forwarded-For*. When you're using an ingress controller with client source IP preservation enabled, TLS pass-through won't work.

```
# Add the ingress-nginx repository
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
# Set variable for ACR location to use for pulling images
ACR_LOGIN_SERVER=<REGISTRY_LOGIN_SERVER>
# Use Helm to deploy an NGINX ingress controller
helm install ingress-nginx ingress-nginx/ingress-nginx \
--version 4.7.1 \
--namespace ingress-basic \
--create-namespace \
--set controller.replicaCount=2 \
--set controller.nodeSelector."kubernetes\.io/os"=linux \
--set controller.image.registry=$ACR_LOGIN_SERVER \
--set controller.image.image=$CONTROLLER_IMAGE \
--set controller.image.tag=$CONTROLLER_TAG \
--set controller.image.digest="" \
--set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.service.externalTrafficPolicy=Local \
--set controller.admissionWebhooks.patch.image.registry=$ACR_LOGIN_SERVER \
--set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \
--set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \
--set controller.admissionWebhooks.patch.image.digest="" \
--set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
--set defaultBackend.image.registry=$ACR_LOGIN_SERVER \
--set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \
--set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \
--set defaultBackend.image.digest=""
```


### Create an ingress controller using an internal IP address

By default, an NGINX ingress controller is created with a dynamic public IP address assignment. A common configuration requirement is to use an internal, private network and IP address. This approach allows you to restrict access to your services to internal users, with no external access.

Use the `--set controller.service.loadBalancerIP`

and `--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-internal"=true`

parameters to assign an internal IP address to your ingress controller. Provide your own internal IP address for use with the ingress controller. Make sure that this IP address isn't already in use within your virtual network. If you're using an existing virtual network and subnet, you must configure your AKS cluster with the correct permissions to manage the virtual network and subnet. For more information, see [Use kubenet networking with your own IP address ranges in Azure Kubernetes Service (AKS)](/en-us/azure/aks/configure-kubenet) or [Configure Azure CNI networking in Azure Kubernetes Service (AKS)](/en-us/azure/aks/configure-azure-cni?tabs=configure-networking-portal).

```
# Add the ingress-nginx repository
helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx
helm repo update
# Set variable for ACR location to use for pulling images
ACR_LOGIN_SERVER=<REGISTRY_LOGIN_SERVER>
# Use Helm to deploy an NGINX ingress controller
helm install ingress-nginx ingress-nginx/ingress-nginx \
--version 4.7.1 \
--namespace ingress-basic \
--create-namespace \
--set controller.replicaCount=2 \
--set controller.nodeSelector."kubernetes\.io/os"=linux \
--set controller.image.registry=$ACR_LOGIN_SERVER \
--set controller.image.image=$CONTROLLER_IMAGE \
--set controller.image.tag=$CONTROLLER_TAG \
--set controller.image.digest="" \
--set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \
--set controller.service.loadBalancerIP=10.224.0.42 \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-internal"=true \
--set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \
--set controller.admissionWebhooks.patch.image.registry=$ACR_LOGIN_SERVER \
--set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \
--set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \
--set controller.admissionWebhooks.patch.image.digest="" \
--set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \
--set defaultBackend.image.registry=$ACR_LOGIN_SERVER \
--set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \
--set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \
--set defaultBackend.image.digest=""
```


## Check the load balancer service

Check the load balancer service by using `kubectl get services`

.

```
kubectl get services --namespace ingress-basic -o wide -w ingress-nginx-controller
```


When the Kubernetes load balancer service is created for the NGINX ingress controller, an IP address is assigned under *EXTERNAL-IP*, as shown in the following example output:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE SELECTOR
ingress-nginx-controller LoadBalancer 10.0.65.205 EXTERNAL-IP 80:30957/TCP,443:32414/TCP 1m app.kubernetes.io/component=controller,app.kubernetes.io/instance=ingress-nginx,app.kubernetes.io/name=ingress-nginx
```


If you browse to the external IP address at this stage, you see a 404 page displayed. This is because you still need to set up the connection to the external IP, which is done in the next sections.

## Run demo applications

To see the ingress controller in action, run two demo applications in your AKS cluster. In this example, you use `kubectl apply`

to deploy two instances of a simple *Hello world* application.

Create an

`aks-helloworld-one.yaml`

file and copy in the following example YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aks-helloworld-one spec: replicas: 1 selector: matchLabels: app: aks-helloworld-one template: metadata: labels: app: aks-helloworld-one spec: containers: - name: aks-helloworld-one image: mcr.microsoft.com/azuredocs/aks-helloworld:v1 ports: - containerPort: 80 env: - name: TITLE value: "Welcome to Azure Kubernetes Service (AKS)" --- apiVersion: v1 kind: Service metadata: name: aks-helloworld-one spec: type: ClusterIP ports: - port: 80 selector: app: aks-helloworld-one`

Create an

`aks-helloworld-two.yaml`

file and copy in the following example YAML:`apiVersion: apps/v1 kind: Deployment metadata: name: aks-helloworld-two spec: replicas: 1 selector: matchLabels: app: aks-helloworld-two template: metadata: labels: app: aks-helloworld-two spec: containers: - name: aks-helloworld-two image: mcr.microsoft.com/azuredocs/aks-helloworld:v1 ports: - containerPort: 80 env: - name: TITLE value: "AKS Ingress Demo" --- apiVersion: v1 kind: Service metadata: name: aks-helloworld-two spec: type: ClusterIP ports: - port: 80 selector: app: aks-helloworld-two`

Run the two demo applications using

`kubectl apply`

:`kubectl apply -f aks-helloworld-one.yaml --namespace ingress-basic kubectl apply -f aks-helloworld-two.yaml --namespace ingress-basic`


## Create an ingress route

Both applications are now running on your Kubernetes cluster. To route traffic to each application, create a Kubernetes ingress resource. The ingress resource configures the rules that route traffic to one of the two applications.

In the following example, traffic to *EXTERNAL_IP/hello-world-one* is routed to the service named `aks-helloworld-one`

. Traffic to *EXTERNAL_IP/hello-world-two* is routed to the `aks-helloworld-two`

service. Traffic to *EXTERNAL_IP/static* is routed to the service named `aks-helloworld-one`

for static assets.

Create a file named

`hello-world-ingress.yaml`

and copy in the following example YAML:`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: hello-world-ingress annotations: nginx.ingress.kubernetes.io/ssl-redirect: "false" nginx.ingress.kubernetes.io/use-regex: "true" nginx.ingress.kubernetes.io/rewrite-target: /$2 spec: ingressClassName: nginx rules: - http: paths: - path: /hello-world-one(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80 - path: /hello-world-two(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-two port: number: 80 - path: /(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80 --- apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: hello-world-ingress-static annotations: nginx.ingress.kubernetes.io/ssl-redirect: "false" nginx.ingress.kubernetes.io/rewrite-target: /static/$2 spec: ingressClassName: nginx rules: - http: paths: - path: /static(/|$)(.*) pathType: Prefix backend: service: name: aks-helloworld-one port: number: 80`

Create the ingress resource using the

`kubectl apply`

command.`kubectl apply -f hello-world-ingress.yaml --namespace ingress-basic`


## Test the ingress controller

To test the routes for the ingress controller, browse to the two applications. Open a web browser to the IP address of your NGINX ingress controller, such as *EXTERNAL_IP*. The first demo application is displayed in the web browser, as shown in the following example:

Now add the */hello-world-two* path to the IP address, such as *EXTERNAL_IP/hello-world-two*. The second demo application with the custom title is displayed:

### Test an internal IP address

Create a test pod and attach a terminal session to it.

`kubectl run -it --rm aks-ingress-test --image=mcr.microsoft.com/dotnet/runtime-deps:6.0 --namespace ingress-basic`

Install

`curl`

in the pod using`apt-get`

.`apt-get update && apt-get install -y curl`

Access the address of your Kubernetes ingress controller using

`curl`

, such as. Provide your own internal IP address specified when you deployed the ingress controller.[http://10.224.0.42](http://10.224.0.42)`curl -L http://10.224.0.42`

No path was provided with the address, so the ingress controller defaults to the

*/*route. The first demo application is returned, as shown in the following condensed example output:`<!DOCTYPE html> <html xmlns="http://www.w3.org/1999/xhtml"> <head> <link rel="stylesheet" type="text/css" href="/static/default.css"> <title>Welcome to Azure Kubernetes Service (AKS)</title> [...]`

Add the

*/hello-world-two*path to the address, such as.[http://10.224.0.42/hello-world-two](http://10.224.0.42/hello-world-two)`curl -L -k http://10.224.0.42/hello-world-two`

The second demo application with the custom title is returned, as shown in the following condensed example output:

`<!DOCTYPE html> <html xmlns="http://www.w3.org/1999/xhtml"> <head> <link rel="stylesheet" type="text/css" href="/static/default.css"> <title>AKS Ingress Demo</title> [...]`


## Clean up resources

This article used Helm to install the ingress components and sample apps. When you deploy a Helm chart, many Kubernetes resources are created. These resources include pods, deployments, and services. To clean up these resources, you can either delete the entire sample namespace, or the individual resources.

### Delete the sample namespace and all resources

To delete the entire sample namespace, use the `kubectl delete`

command and specify your namespace name. All the resources in the namespace are deleted.

```
kubectl delete namespace ingress-basic
```


### Delete resources individually

Alternatively, a more granular approach is to delete the individual resources created.

List the Helm releases with the

`helm list`

command.`helm list --namespace ingress-basic`

Look for charts named

*ingress-nginx*and*aks-helloworld*, as shown in the following example output:`NAME NAMESPACE REVISION UPDATED STATUS CHART APP VERSION ingress-nginx ingress-basic 1 2020-01-06 19:55:46.358275 -0600 CST deployed nginx-ingress-1.27.1 0.26.1`

Uninstall the releases with the

`helm uninstall`

command.`helm uninstall ingress-nginx --namespace ingress-basic`

Remove the two sample applications.

`kubectl delete -f aks-helloworld-one.yaml --namespace ingress-basic kubectl delete -f aks-helloworld-two.yaml --namespace ingress-basic`

Remove the ingress route that directed traffic to the sample apps.

`kubectl delete -f hello-world-ingress.yaml`

Delete the namespace using the

`kubectl delete`

command and specifying your namespace name.`kubectl delete namespace ingress-basic`


## Next steps

To configure TLS with your existing ingress components, see [Use TLS with an ingress controller](/en-us/previous-versions/azure/aks/ingress-tls).

To configure your AKS cluster to use application routing, see [Application routing add-on](/en-us/azure/aks/app-routing).

This article included some external components to AKS. To learn more about these components, see the following project pages:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-blob-csi -->

# Azure storage CSI driver and volume provisioning

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Blob storage Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant driver used by Azure Kubernetes Service (AKS) to
manage the lifecycle of Azure Blob storage. The CSI is a standard for exposing arbitrary block and
file storage systems to containerized workloads on Kubernetes.

By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids having to touch the core Kubernetes code and wait for its release cycles.

When you mount Azure Blob storage as a file system into a container or pod, it enables you to use blob storage with many applications that work massive amounts of unstructured data. For example:

- Log file data
- Images, documents, and streaming video or audio
- Disaster recovery data

Applications access data stored in Azure Blob storage using either BlobFuse or the Network File System (NFS) 3.0 protocol. Before the introduction of the Azure Blob storage CSI driver, the only option was to manually install an unsupported driver to access Blob storage from your application running on AKS. When the Azure Blob storage CSI driver is enabled on AKS, there are two built-in storage classes:

- azureblob-fuse-premium
- azureblob-nfs-premium

To create an AKS cluster with CSI drivers support, see [CSI drivers on AKS](csi-storage-drivers). To
learn more about the differences in access between each of the Azure storage types using the NFS
protocol, see
[Compare access to Azure Files, Blob Storage, and Azure NetApp Files with NFS](/en-us/azure/storage/common/nfs-comparison).

The Azure Disks Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant
driver used by Azure Kubernetes Service (AKS) to manage the lifecycle of Azure Disk.

The CSI is a standard for exposing arbitrary block and file storage systems to containerized
workloads on Kubernetes. By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins
to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids
having to touch the core Kubernetes code and wait for its release cycles. To create an AKS cluster
with CSI driver support, see [Enable CSI driver on AKS](csi-storage-drivers).

For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

Note

*In-tree drivers* refer to the current storage drivers that are part of the core Kubernetes code versus the new CSI drivers, which are plug-ins.

The Azure Files Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant driver used by Azure Kubernetes Service (AKS) to
manage the lifecycle of Azure file shares. The CSI is a standard for exposing arbitrary block and
file storage systems to containerized workloads on Kubernetes.

By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids having to touch the core Kubernetes code and wait for its release cycles.

To create an AKS cluster with CSI drivers support, see [Enable CSI drivers on AKS](csi-storage-drivers).

Note

*In-tree drivers* refer to the current storage drivers that are part of the core Kubernetes code versus the new CSI drivers, which are plug-ins.

## Azure CSI driver features

Azure Blob storage CSI driver supports the following features:

- BlobFuse
- NFS 3.0 protocol

In addition to in-tree driver features, Azure Disk CSI driver supports the following features:

Performance improvements during concurrent disk attach and detach

- In-tree drivers attach or detach disks in serial, while CSI drivers attach or detach disks in batch. There's significant improvement when there are multiple disks attaching to one node.

Premium SSD v1 and v2 are supported.

`PremiumV2_LRS`

only supports`None`

caching mode

Zone-redundant storage (ZRS) disk support

`Premium_ZRS`

,`StandardSSD_ZRS`

disk types are supported. ZRS disk could be scheduled on the zone or non-zone node, without the restriction that disk volume should be colocated in the same zone as a given node. For more information, including which regions are supported, see[Zone-redundant storage for managed disks](/en-us/azure/virtual-machines/disks-redundancy).


Note

Depending on the VM SKU that's being used, the Azure Disk CSI driver might have a per-node volume limit. For some powerful VMs (for example, 16 cores), the limit is 64 volumes per node. To identify the limit per VM SKU, review the **Max data disks** column for each VM SKU offered. For a list of VM SKUs offered and their corresponding detailed capacity limits, see [General purpose virtual machine sizes](/en-us/azure/virtual-machines/sizes-general).

## Prerequisites

You must have the Azure CLI version 2.42 or later installed and configured. To find the version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you installed the Azure CLI`aks-preview`

extension, make sure that you update the extension to the latest version by calling`az extension update --name aks-preview`

.Perform the following steps to

[clean up the open source driver](https://github.com/kubernetes-sigs/blob-csi-driver/blob/master/docs/install-csi-driver-master.md#clean-up-blob-csi-driver)if you previously installed the[CSI Blob Storage open-source driver](https://github.com/kubernetes-sigs/blob-csi-driver)to access Azure Blob storage from your cluster.Your AKS cluster

*Control plane*identity (your AKS cluster name) is added to the[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)role on the VNet and network security group.To support an [Azure Data Lake Storage Gen2 account][azure-datalake-storage-account] (ADLS) when using BlobFuse mount, perform the following actions:

- To create an ADLS account using the driver in dynamic provisioning, specify
`isHnsEnabled: "true"`

in the storage class parameters. - To enable BlobFuse access to an ADLS account in static provisioning, specify the mount option
`--use-adls=true`

in the persistent volume. - If you're going to enable a storage account with Hierarchical Namespace, existing persistent volumes (PVs) should be remounted with
`--use-adls=true`

mount option.

- To create an ADLS account using the driver in dynamic provisioning, specify
By default, the BlobFuse cache is located in the

`/mnt`

directory. If the virtual machine (VM) SKU provides a temporary disk, the`/mnt`

directory is mounted on the temporary disk. However, if the VM SKU doesn't provide a temporary disk, the`/mnt`

directory is mounted on the OS disk, you could set`--tmp-path=`

mount option to specify a different cache directory.

Note

If the **blobfuse-proxy** isn't enabled during the installation of the open source driver, the uninstallation of the open source driver disrupts existing blobfuse mounts. However, NFS mounts remain unaffected.

You must have an AKS cluster with the Azure Disk CSI driver enabled. The CSI driver is enabled by default on AKS clusters running Kubernetes version 1.21 or later.

Azure CLI version 2.37.0 or later is installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`kubectl`

command-line tool is installed and configured to connect to your AKS cluster.A storage class configured to use the Azure Disk CSI driver (

`disk.csi.azure.com`

).The Azure Disk CSI driver has a per-node volume limit. The volume count changes based on the size of the node/node pool. Run the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command to determine the number of volumes that can be allocated per node:`kubectl get CSINode <nodename> -o yaml`

If the per-node volume limit is an issue for your workload, consider using

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for persistent volumes instead of CSI drivers.

**General requirements:**

You must have an AKS cluster with the Azure Files CSI driver enabled. The Azure Files CSI driver is enabled by default on AKS clusters running Kubernetes version 1.21 or later.

Azure CLI version 2.37.0 or later is installed and configured. To check your version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`kubectl`

command-line tool is installed and configured to connect to your AKS cluster.A storage class configured to use the Azure Files CSI driver (

`file.csi.azure.com`

).When choosing between standard and premium file shares, it's important you understand the provisioning model and requirements of the expected usage pattern you plan to run on Azure Files. For more information, see

[Choosing an Azure Files performance tier based on usage patterns](/en-us/azure/storage/files/understand-performance#choosing-a-performance-tier-based-on-usage-patterns).

**Network File Share (NFS) requirements:**

Your AKS cluster

*Control plane*identity (your AKS cluster name) is added to the[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)role on the VNet and**NetworkSecurityGroup**.Your AKS cluster's service principal or managed service identity (MSI) must be added to the

**Contributor**role to the storage account.

**Managed Identity requirements:**

Ensure the

[user-assigned Kubelet identity](use-managed-identity#create-a-kubelet-managed-identity)is granted the`Storage File Data SMB MI Admin`

role on the storage account. If you use your own storage account, you need to assign`Storage File Data SMB MI Admin`

role to the user-assigned Kubelet identity on that storage account.If the CSI driver creates the storage account, grant the

`Storage File Data SMB MI Admin`

role to the resource group where the storage account resides.If you use the default built-in user-assigned Kubelet identity, it already has the required

`Storage File Data SMB MI Admin`

role on the managed node resource group.

Note

The Azure File CSI driver only permits the mounting of SMB file shares using key-based (NTLM v2) authentication, and therefore doesn't support the maximum security profile of Azure File share settings. On the other hand, mounting NFS file shares doesn't require key-based authentication.

## Enable CSI driver on a new or existing AKS cluster

Using the Azure CLI, you can enable the Blob storage CSI driver on a new or existing AKS cluster before you configure a persistent volume for use by pods in the cluster.

To enable the driver on a new cluster, include the

`--enable-blob-driver`

parameter with the`az aks create`

command as shown in the following example:`az aks create \ --enable-blob-driver \ --name myAKSCluster \ --resource-group myResourceGroup \ --generate-ssh-keys`

To enable the driver on an existing cluster, include the

`--enable-blob-driver`

parameter with the`az aks update`

command as shown in the following example:`az aks update --enable-blob-driver --name myAKSCluster --resource-group myResourceGroup`


You're prompted to confirm there isn't an open-source Blob CSI driver installed. After you confirm, it might take several minutes to complete this action. Once it's complete, you should see in the output the status of enabling the driver on your cluster. The following example resembles the section indicating the results of the previous command:

```
"storageProfile": {
"blobCsiDriver": {
"enabled": true
},
...
}
```


## Disable CSI driver on an existing AKS cluster

Using the Azure CLI, you can disable the Blob storage CSI driver on an existing AKS cluster after you remove the persistent volume from the cluster.

To disable the driver on an existing cluster, include the

`--disable-blob-driver`

parameter with the`az aks update`

command as shown in the following example:`az aks update --disable-blob-driver --name myAKSCluster --resource-group myResourceGroup`


## Use a persistent volume for storage

Kubernetes assigns a [persistent volume](concepts-storage#persistent-volumes) (PV) as a storage resource to one or more pods. You can provision PVs dynamically through Kubernetes or statically as an administrator.

If multiple pods need concurrent access to the same storage volume, you can use Azure Blob storage to connect by using NFS or BlobFuse. This article shows you how to dynamically create an Azure Blob storage container for use by multiple pods in an AKS cluster.

For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

This article shows you how to dynamically create a PV with Azure disk for use by a single pod in an AKS cluster.

If multiple pods need concurrent access to the same storage volume, you can use Azure Files to
connect by using the [Server Message Block (SMB)](/en-us/windows/desktop/FileIO/microsoft-smb-protocol-and-cifs-protocol-overview) or
[Network File System (NFS)](/en-us/windows-server/storage/nfs/nfs-overview). This article shows you how to dynamically create an Azure
Files share for use by multiple pods in an AKS cluster.

**Dynamically provisioned volume:** Use this approach when you want Kubernetes to automatically
create and manage storage resources. It's ideal for scenarios where you need on-demand scaling,
prefer infrastructure-as-code, and want to minimize manual configuration steps.

**Statically provisioned volume:** Choose this method if you already have an Azure Blob storage
account or container that you want to use. It provides more control over storage setup, access, and
lifecycle, and is suitable when you need to connect to existing resources or reuse storage across
multiple clusters or workloads.

This section provides guidance for cluster administrators who want to provision one or more persistent volumes that include details of Blob storage for use by a workload. A persistent volume claim (PVC) uses the storage class object to dynamically provision an Azure Blob storage container.

To provision a persistent volume using Azure Blob storage with the provided storage class, follow these steps:

Create the

`StorageClass`

manifest by saving the following YAML to a file named`blob-fuse-sc.yaml`

:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: blob-fuse provisioner: blob.csi.azure.com parameters: skuName: Premium_LRS # available values: Standard_LRS, Premium_LRS, Standard_GRS, Standard_RAGRS, Standard_ZRS, Premium_ZRS protocol: fuse2 networkEndpointType: privateEndpoint reclaimPolicy: Delete volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - -o allow_other - --file-cache-timeout-in-seconds=120 - --use-attr-cache=true - --cancel-list-on-mount-seconds=10 # prevent billing charges on mounting - -o attr_timeout=120 - -o entry_timeout=120 - -o negative_timeout=120 - --log-level=LOG_WARNING # LOG_WARNING, LOG_INFO, LOG_DEBUG - --cache-size-mb=1000 # Default will be 80% of available memory, eviction will happen beyond specified value.`

To create the storage class in your cluster, apply the

`StorageClass`

by running the following command:`kubectl apply -f blob-fuse-sc.yaml`


## Create a PVC using built-in storage class

A storage class is used to define how an Azure Blob storage container is created. A storage account is automatically created in the node resource group for use with the storage class to hold the Azure Blob storage container. Choose one of the following Azure storage redundancy SKUs for skuName:

Note

Modifying any resource under the node resource group in an AKS cluster is an unsupported action and will cause cluster operation failures. For more information, see [Why are two resource groups created with AKS?](faq)

**Standard_LRS**: Standard locally redundant storage**Premium_LRS**: Premium locally redundant storage**Standard_ZRS**: Standard zone redundant storage**Premium_ZRS**: Premium zone redundant storage**Standard_GRS**: Standard geo-redundant storage**Standard_RAGRS**: Standard read-access geo-redundant storage

When you use storage CSI drivers on AKS, there are two other built-in `StorageClasses`

that use the Azure Blob CSI storage driver.

The reclaim policy on both storage classes ensures that the underlying Azure Blob storage is deleted
when the respective PV is deleted. The storage classes also configure the container to be expandable
by default, as the `set allowVolumeExpansion`

parameter is set to **true**.

Note

Shrinking persistent volumes isn't supported.

Use the [kubectl get sc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command to see the storage classes. The following example
shows the `azureblob-fuse-premium`

and `azureblob-nfs-premium`

storage classes available within an
AKS cluster:

```
NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE
azureblob-fuse-premium blob.csi.azure.com Delete Immediate true 23h
azureblob-nfs-premium blob.csi.azure.com Delete Immediate true 23h
```


To use these storage classes, create a PVC and respective pod that references and uses them. A PVC is used to automatically allocate storage based on a storage class. You can create a PVC using one of the built-in storage classes or a custom storage class. This PVC creates an Azure Blob storage container with your specified SKU, size, and protocol. When you create a pod definition, the PVC is specified to request the desired storage.

A PVC uses the storage class object to dynamically provision an Azure Blob storage container. The following YAML can be used to create a 5 GB PVC with *ReadWriteMany* access, using the built-in storage class. For more information on access modes, see the [Kubernetes persistent volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) documentation.

Create a file named

`blob-nfs-pvc.yaml`

and copy the following YAML:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azure-blob-storage spec: accessModes: - ReadWriteMany storageClassName: azureblob-nfs-premium resources: requests: storage: 5Gi`

Create the PVC with the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command:`kubectl create -f blob-nfs-pvc.yaml`


Once complete, the Blob storage container is created. You can use the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)
command to view the status of the PVC:

```
kubectl get pvc azure-blob-storage
```


The output of the command resembles the following example:

```
NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE
azure-blob-storage Bound pvc-b88e36c5-c518-4d38-a5ee-337a7dda0a68 5Gi RWX azureblob-nfs-premium 92m
```


## Mount the PVC

The following YAML creates a pod that uses the PVC **azure-blob-storage** to mount the Azure Blob storage at the `/mnt/blob`

path.

Create a file named

`blob-nfs-pv`

, and copy the following YAML. Make sure that the**claimName**matches the PVC created in the previous step.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/blob" name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: azure-blob-storage`

Create the pod with the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f blob-nfs-pv.yaml`

After the pod is in the running state, run the following command to create a new file called

`test.txt`

.`kubectl exec mypod -- touch /mnt/blob/test.txt`

To validate the disk is correctly mounted, run the following command, and verify you see the

`test.txt`

file in the output:`kubectl exec mypod -- ls /mnt/blob`

The output of the command resembles the following example:

`test.txt`


## Create an Azure Blob custom storage class

The default storage classes suit the most common scenarios, but not all. In some cases, you might want to have your own storage class customized with your own parameters. In this section, we provide two examples with the first one using the NFS protocol, and the second one using BlobFuse.

In this example, the following manifest configures mounting a Blob storage container using the NFS
protocol. Use it to add the `tags`

parameter.

Create a file named

`blob-nfs-sc.yaml`

, and paste the following example manifest:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azureblob-nfs-premium provisioner: blob.csi.azure.com parameters: protocol: nfs tags: environment=Development volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - nconnect=4`

Create the storage class with the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f blob-nfs-sc.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/blob-nfs-premium created`


## Mount an NFS or BlobFuse PV

In this section, you mount the PV using the NFS protocol or BlobFuse.

Mounting Blob storage using the NFS v3 protocol doesn't authenticate using an account key. Your AKS
cluster needs to reside in the same or peered virtual network as the agent node. The only way to
secure the data in your storage account is by using a virtual network and other network security
settings. For more information on how to set up NFS access to your storage account, see
[Mount Blob Storage by using the Network File System (NFS) 3.0 protocol](/en-us/azure/storage/blobs/network-file-system-protocol-support-how-to).

The following example demonstrates how to mount a Blob storage container as a persistent volume using the NFS protocol.

Create a file named

`pv-blob-nfs.yaml`

and copy in the following YAML. Under`storageClass`

, update`resourceGroup`

,`storageAccount`

, and`containerName`

.Note

The

`volumeHandle`

value within your YAML should be a unique volumeID for every identical storage blob container in the cluster.The characters

`#`

and`/`

are reserved for internal use and can't be used.`apiVersion: v1 kind: PersistentVolume metadata: annotations: pv.kubernetes.io/provisioned-by: blob.csi.azure.com name: pv-blob spec: capacity: storage: 1Pi accessModes: - ReadWriteMany persistentVolumeReclaimPolicy: Retain # If set as "Delete" container would be removed after pvc deletion storageClassName: azureblob-nfs-premium mountOptions: - nconnect=4 csi: driver: blob.csi.azure.com # make sure volumeid is unique for every identical storage blob container in the cluster # character `#` and `/` are reserved for internal use and cannot be used in volumehandle volumeHandle: account-name_container-name volumeAttributes: resourceGroup: resourceGroupName storageAccount: storageAccountName containerName: containerName protocol: nfs`

Note

While the

[Kubernetes API](https://github.com/kubernetes/kubernetes/blob/release-1.26/pkg/apis/core/types.go#L303-L306)**capacity**attribute is mandatory, this value isn't used by the Azure Blob storage CSI driver because you can flexibly write data until you reach your storage account's capacity limit. The value of the`capacity`

attribute is used only for size matching between*PVs*and*PVCs*. We recommend using a fictitious high value. The pod sees a mounted volume with a fictitious size of 5 Petabytes.Run the following command to create the persistent volume using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command referencing the YAML file created earlier:`kubectl create -f pv-blob-nfs.yaml`

Create a

`pvc-blob-nfs.yaml`

file with a*PersistentVolumeClaim*. For example:`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: pvc-blob spec: accessModes: - ReadWriteMany resources: requests: storage: 10Gi volumeName: pv-blob storageClassName: azureblob-nfs-premium`

Run the following command to create the persistent volume claim using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command referencing the YAML file created earlier:`kubectl create -f pvc-blob-nfs.yaml`


## Create a pod

The following YAML creates a pod that uses the PV or PVC named **pvc-blob** created earlier, to mount the Azure Blob storage at the `/mnt/blob`

path.

Create a file named

`nginx-pod-blob.yaml`

, and copy in the following YAML. Make sure that the**claimName**matches the PVC created in the previous step when creating a PV for NFS or BlobFuse.`kind: Pod apiVersion: v1 metadata: name: nginx-blob spec: nodeSelector: "kubernetes.io/os": linux containers: - image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine name: nginx-blob volumeMounts: - name: blob01 mountPath: "/mnt/blob" readOnly: false volumes: - name: blob01 persistentVolumeClaim: claimName: pvc-blob`

Run the following command to create the pod and mount the PVC using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command:`kubectl create -f nginx-pod-blob.yaml`

Run the following command to create an interactive shell session with the pod to verify if the Blob storage is mounted:

`kubectl exec -it nginx-blob -- df -h`

The output from the command resembles the following example:

`Filesystem Size Used Avail Use% Mounted on ... blobfuse 14G 41M 13G 1% /mnt/blob ...`


## Create a StatefulSet

To ensure your workload retains its storage volume across pod restarts or replacements, use a StatefulSet. StatefulSets simplify the process of associating persistent storage with pods, so that new pods created to replace failed ones can automatically access the same storage volumes. The following examples demonstrate how to set up a StatefulSet for Blob storage using either BlobFuse or the NFS protocol.

Create a file named

`azure-blob-nfs-ss.yaml`

and copy in the following YAML.`apiVersion: apps/v1 kind: StatefulSet metadata: name: statefulset-blob-nfs labels: app: nginx spec: serviceName: statefulset-blob-nfs replicas: 1 template: metadata: labels: app: nginx spec: nodeSelector: "kubernetes.io/os": linux containers: - name: statefulset-blob-nfs image: mcr.microsoft.com/azurelinux/base/nginx:1.25 volumeMounts: - name: persistent-storage mountPath: /mnt/blob updateStrategy: type: RollingUpdate selector: matchLabels: app: nginx volumeClaimTemplates: - metadata: name: persistent-storage spec: storageClassName: azureblob-nfs-premium accessModes: ["ReadWriteMany"] resources: requests: storage: 100Gi`

Create the StatefulSet with the

`kubectl create`

command:`kubectl create -f azure-blob-nfs-ss.yaml`


### Dynamic PVC storage class parameters

The following table includes parameters you can use to define a custom storage class for your dynamic PVC.

| Name | Description | Example | Mandatory | Default value |
|---|---|---|---|---|
| skuName | Specify an Azure storage account type (alias: `storageAccountType` ). |
`Standard_LRS` , `Premium_LRS` , `Standard_GRS` , `Standard_RAGRS` |
No | `Standard_LRS` |
| location | Specify an Azure location. | `eastus` |
No | If empty, the driver uses the same location name as current cluster. |
| resourceGroup | Specify an Azure resource group name. | myResourceGroup | No | If empty, the driver uses the same resource group name as current cluster. |
| storageAccount | Specify an Azure storage account name. | storageAccountName | No | When a specific storage account name isn't provided, the driver looks for a suitable storage account that matches the account settings within the same resource group. If it fails to find a matching storage account, it creates a new one. However, if a storage account name is specified, the storage account must already exist. |
networkEndpointType 1 |
Specify network endpoint type for the storage account created by driver. If privateEndpoint is specified, a
|

`privateEndpoint`

`fuse`

, `nfs`

`fuse`

`pvc-fuse`

for BlobFuse or `pvc-nfs`

for NFS v3.`<storage-account>.blob.core.windows.net`

.`<storage-account>.blob.core.windows.net`

or other sovereign cloud storage account DNS domain name.`true`

,`false`

`false`

`core.windows.net`

`true`

,`false`

`false`

1 If the storage account is created by the driver, then you only need to specify `networkEndpointType: privateEndpoint`

parameter in storage class. The CSI driver creates the private endpoint and private DNS zone (named `privatelink.blob.core.windows.net`

) together with the account. If you bring your own storage account, then you need to [create the private endpoint](/en-us/azure/storage/common/storage-private-endpoints) for the storage account. If you're using Azure Blob storage in a network isolated cluster, you must create a custom storage class with `networkEndpointType: privateEndpoint`

.

### Static PV provisioning parameters

The following table includes parameters you can use to define your static PV.

| Name | Description | Example | Mandatory | Default value |
|---|---|---|---|---|
| volumeHandle | Specify a value the driver can use to uniquely identify the storage blob container in the cluster. | A recommended way to produce a unique value is to combine the globally unique storage account name and container name: `{account-name}_{container-name}` . The `#` and `/` characters are reserved for internal use and can't be used in a volume handle. |
Yes | |
| volumeAttributes.resourceGroup | Specify Azure resource group name. | myResourceGroup | No | If empty, driver uses the same resource group name as current cluster. |
| volumeAttributes.storageAccount | Specify an existing Azure storage account name. | storageAccountName | Yes | |
| volumeAttributes.containerName | Specify existing container name. | container | Yes | |
| volumeAttributes.protocol | Specify BlobFuse mount or NFS v3 mount. | `fuse` , `nfs` |
No | `fuse` |

## Create Azure Disk PVs using built-in storage classes

A storage class is used to define how a unit of storage is dynamically created with a PV. For more information on Kubernetes storage classes, see [Kubernetes storage classes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

When you use the Azure Disk CSI driver on AKS, there are two more built-in `StorageClasses`

that use the Azure Disk CSI storage driver. The other CSI storage classes are created with the cluster alongside the in-tree default storage classes.

`managed-csi`

: Creates managed disks using Azure Standard SSD with locally redundant storage (LRS). With Kubernetes version 1.29 for AKS clusters deployed across multiple availability zones, this storage class uses Azure Standard SSD zone-redundant storage (ZRS) to provision managed disks.`managed-csi-premium`

: Provisions managed disks using Azure Premium LRS. Beginning with Kubernetes version 1.29, for AKS clusters spanning multiple availability zones, this storage class automatically uses Azure Premium ZRS to create managed disks.

Effective starting with Kubernetes version 1.29, when you deploy Azure Kubernetes Service (AKS) clusters across multiple availability zones, AKS now utilizes zone-redundant storage (ZRS) to create managed disks within built-in storage classes.

ZRS ensures synchronous replication of your Azure managed disks across multiple Azure availability zones in your chosen region. This redundancy strategy enhances the resilience of your applications and safeguards your data against datacenter failures.

However, it's important to note that zone-redundant storage (ZRS) comes at a higher cost compared to locally redundant storage (LRS). If cost optimization is a priority, you can create a new storage class with the LRS SKU name parameter and use it in your persistent volume claim.


Reducing the size of a PVC isn't supported due to the risk of data loss. You can edit an existing storage class using the `kubectl edit sc`

command, or you can create your own custom storage class. For example, if you want to use a disk of size 4 TiB, you must create a storage class that defines `cachingmode: None`

because [disk caching isn't supported for disks 4 TiB and larger][disk-host-cache-setting]. For more information about storage classes and creating your own storage class, see [Storage options for applications in AKS](concepts-storage#storage-classes).

The reclaim policy in both storage classes ensures that the underlying Azure Disks are deleted when the respective PV is deleted. The storage classes also configure the PVs to be expandable. You just need to edit the PVC with the new size.

To use these storage classes, create a [PVC](concepts-storage#persistent-volume-claims) and respective pod that references and uses them. A PVC is used to automatically provision storage based on a storage class. A PVC can use one of the precreated storage classes or a user-defined storage class to create an Azure-managed disk for the desired SKU and size. When you create a pod definition, the PVC is specified to request the desired storage.

Note

Persistent volume claims are specified in GiB but Azure managed disks are billed based on the SKU for a specific size. These SKUs range from 32GiB for S4 or P4 disks to 32TiB for S80 or P80 disks (in preview). The throughput and IOPS performance of a Premium managed disk depends on both the SKU and the instance size of the nodes in the AKS cluster. For more information, see [Pricing and performance of managed disks](https://azure.microsoft.com/pricing/details/managed-disks/).

You can see the precreated storage classes using the [ kubectl get sc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. The following example shows the precreated storage classes available within an AKS cluster:

```
kubectl get sc
```


The output of the command resembles the following example:

```
NAME PROVISIONER AGE
default (default) disk.csi.azure.com 1h
managed-csi disk.csi.azure.com 1h
```


A PVC automatically provisions storage based on a storage class. In this case, a PVC can use one of the precreated storage classes to create a standard or premium Azure managed disk.

Create a file named

`azure-pvc.yaml`

and copy in the following manifest. The claim requests a disk named`azure-managed-disk`

that's`5 GB`

in size with`ReadWriteOnce`

access. The*managed-csi*storage class is specified as the storage class.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azure-managed-disk spec: accessModes: - ReadWriteOnce storageClassName: managed-csi resources: requests: storage: 5Gi`

Tip

To create a disk that uses premium storage, use

`storageClassName: managed-csi-premium`

rather than*managed-csi*.Create the persistent volume claim using the

command and specify your`kubectl apply`

*azure-pvc.yaml*file.`kubectl apply -f azure-pvc.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/azure-managed-disk created`


## Apply a PVC to a pod

After you create the persistent volume claim, you must verify it has a status of `Pending`

. The `Pending`

status indicates it's ready to be used by a pod.

Verify the status of the PVC using the

`kubectl describe pvc`

command.`kubectl describe pvc azure-managed-disk`

The output of the command resembles the following condensed example:

`Name: azure-managed-disk Namespace: default StorageClass: managed-csi Status: Pending [...]`

Create a file named

`azure-pvc-disk.yaml`

and copy in the following manifest. This manifest creates a basic NGINX pod that uses the persistent volume claim named`azure-managed-disk`

to mount the Azure Disk at the path`/mnt/azure`

. For Windows Server containers, specify a`mountPath`

using the Windows path convention, such as*'D:'*.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/azure" name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: azure-managed-disk`

Create the pod using the

command.`kubectl apply`

`kubectl apply -f azure-pvc-disk.yaml`

The output of the command resembles the following example:

`pod/mypod created`

You now have a running pod with your Azure Disk mounted in the

`/mnt/azure`

directory. Check the pod configuration using thecommand.`kubectl describe`

`kubectl describe pod mypod`

The output of the command resembles the following example:

`[...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: azure-managed-disk ReadOnly: false default-token-smm2n: Type: Secret (a volume populated by a Secret) SecretName: default-token-smm2n Optional: false [...] Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Scheduled 2m default-scheduler Successfully assigned mypod to aks-nodepool1-79590246-0 Normal SuccessfulMountVolume 2m kubelet, aks-nodepool1-79590246-0 MountVolume.SetUp succeeded for volume "default-token-smm2n" Normal SuccessfulMountVolume 1m kubelet, aks-nodepool1-79590246-0 MountVolume.SetUp succeeded for volume "pvc-faf0f176-8b8d-11e8-923b-deb28c58d242" [...]`


## Dynamic storage class parameters for PVCs

The following table includes parameters you can use to define a custom storage class for your PVCs.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| skuName | Azure Disks storage account type (alias: `storageAccountType` ) |
`Standard_LRS` , `Premium_LRS` , `StandardSSD_LRS` , `PremiumV2_LRS` , `UltraSSD_LRS` , `Premium_ZRS` , `StandardSSD_ZRS` |
No | `StandardSSD_LRS` |
| fsType | File System Type | `ext4` , `ext3` , `ext2` , `xfs` , `btrfs` for Linux, `ntfs` for Windows |
No | `ext4` for Linux, `ntfs` for Windows |
| cachingMode | [Azure Data Disk Host Cache Setting][disk-host-cache-setting](PremiumV2_LRS and UltraSSD_LRS only support `None` caching mode) |
`None` , `ReadOnly` , `ReadWrite` |
No | `ReadOnly` |
| resourceGroup | Specify the resource group for the Azure Disks | Existing resource group name | No | If empty, driver uses the same resource group name as current AKS cluster |
| DiskIOPSReadWrite | [UltraSSD disk][ultra-ssd-disks] or [Premium SSD v2][premiumv2_lrs_disks] IOPS Capability (minimum: 2 IOPS/GiB) | 100~160000 | No | `500` |
| DiskMBpsReadWrite | [UltraSSD disk][ultra-ssd-disks] or [Premium SSD v2][premiumv2_lrs_disks] Throughput Capability(minimum: 0.032/GiB) | 1~2000 | No | `100` |
| LogicalSectorSize | Logical sector size in bytes for ultra disk. Supported values are 512 ad 4096. 4096 is the default. | `512` , `4096` |
No | `4096` |
| tags | Azure Disk [tags][azure-tags] | Tag format: `key1=val1,key2=val2` |
No | "" |
| diskEncryptionSetID | ResourceId of the disk encryption set to use for [enabling encryption at rest][disk-encryption] | format: `/subscriptions/{subs-id}/resourceGroups/{rg-name}/providers/Microsoft.Compute/diskEncryptionSets/{diskEncryptionSet-name}` |
No | "" |
| diskEncryptionType | Encryption type of the disk encryption set. | `EncryptionAtRestWithCustomerKey` (by default), `EncryptionAtRestWithPlatformAndCustomerKeys` |
No | "" |
| writeAcceleratorEnabled | [Write Accelerator on Azure Disks][azure-disk-write-accelerator] | `true` , `false` |
No | "" |
| networkAccessPolicy | NetworkAccessPolicy property to prevent generation of the SAS URI for a disk or a snapshot | `AllowAll` , `DenyAll` , `AllowPrivate` |
No | `AllowAll` |
| diskAccessID | Azure Resource ID of the DiskAccess resource to use private endpoints on disks | No | `` | |
| enableBursting | [Enable on-demand bursting][on-demand-bursting] beyond the provisioned performance target of the disk. On-demand bursting should only be applied to Premium disk and when the disk size > 512 GB. Ultra and shared disk isn't supported. Bursting is disabled by default. | `true` , `false` |
No | `false` |
| userAgent | The user agent is used for [customer usage attribution][customer-usage-attribution] | No | The generated user agent is formatted as `driverName/driverVersion compiler/version (OS-ARCH)` |
|
| subscriptionID | Specify Azure subscription ID where the Azure Disks is created. | Azure subscription ID | No | If not empty, `resourceGroup` must be provided. |

## Static provisioning parameters for a PV

The following table includes parameters you can use to define a PV.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| volumeHandle | Azure disk URI | `/subscriptions/{sub-id}/resourcegroups/{group-name}/providers/microsoft.compute/disks/{disk-id}` |
Yes | N/A |
| volumeAttributes.fsType | File system type | `ext4` , `ext3` , `ext2` , `xfs` , `btrfs` for Linux, `ntfs` for Windows |
No | `ext4` for Linux, `ntfs` for Windows |
| volumeAttributes.partition | Partition number of the existing disk (only supported on Linux) | `1` , `2` , `3` |
No | Empty (no partition) - Make sure partition format is like `-part1` |
| volumeAttributes.cachingMode | [Disk host cache setting][disk-host-cache-setting] | `None` , `ReadOnly` , `ReadWrite` |
No | `ReadOnly` |

## Create an Azure Disk custom storage class

The default storage classes are suitable for most common scenarios. For some cases, you might want
to have your own storage class customized with your own parameters. For example, you might want to
change the `volumeBindingMode`

class.

You can use a `volumeBindingMode: Immediate`

class that guarantees it occurs immediately once the
persistent volume claim (PVC) is created. When your node pools are topology constrained, for example
when using availability zones, PVs would be bound or provisioned without knowledge of the pod's
scheduling requirements.

To address this scenario, you can use `volumeBindingMode: WaitForFirstConsumer`

, which delays the binding and provisioning of a PV until a pod that uses the PVC is created. This approach ensures that the persistent volume (PV) is provisioned in the same availability zone or topology as required per the pod's scheduling constraints. The default storage classes use `volumeBindingMode: WaitForFirstConsumer`

class.

Create a file named

`sc-azuredisk-csi-waitforfirstconsumer.yaml`

, and then paste the following manifest. The storage class is the same as our`managed-csi`

storage class, but with a different`volumeBindingMode`

class. For example:`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: azuredisk-csi-waitforfirstconsumer provisioner: disk.csi.azure.com parameters: skuname: StandardSSD_LRS allowVolumeExpansion: true reclaimPolicy: Delete volumeBindingMode: WaitForFirstConsumer`

Create the storage class by running the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify your`sc-azuredisk-csi-waitforfirstconsumer.yaml`

file:`kubectl apply -f sc-azuredisk-csi-waitforfirstconsumer.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/azuredisk-csi-waitforfirstconsumer created`


## Learn about volume snapshots

The Azure Disk CSI driver supports [volume snapshots](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html), enabling you to capture the state of persistent volumes at specific points in time for backup and restore operations. Volume snapshots let you create point-in-time copies of your persistent data without interrupting running applications. You can use these snapshots to create new volumes or restore existing ones to a previous state.

You can create two types of snapshots:

**Full snapshots**: Capture the complete state of the disk.**Incremental snapshots**: Capture only the changes since the last snapshot, offering better storage efficiency and cost savings.[Incremental snapshots](/en-us/azure/virtual-machines/disks-incremental-snapshots)are the default behavior when the`incremental`

parameter is set to`true`

in your VolumeSnapshotClass.

The following table provides details for these parameters.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| resourceGroup | Resource group for storing snapshot shots | EXISTING RESOURCE GROUP | No | If not specified, snapshots are stored in the same resource group as source Azure Disks |
| incremental | Take
|

`true`

, `false`

`true`

[tags](/en-us/azure/azure-resource-manager/management/tag-resources)[customer usage attribution](/en-us/azure/marketplace/azure-partner-customer-usage-attribution)`driverName/driverVersion compiler/version (OS-ARCH)`

`resourceGroup`

must be provided, `incremental`

must set as `false`

Volume snapshots support the following scenarios:

**Backup and restore**: Create point-in-time backups of stateful application data and restore when needed.**Data cloning**: Clone existing volumes to create new persistent volumes with the same data.**Disaster recovery**: Quickly recover from data loss or corruption.

### Create a volume snapshot

Note

Before proceeding, ensure that the application isn't writing data to the source disk.

For an example of this capability, create a

[volume snapshot class](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/storageclass-azuredisk-snapshot.yaml)with the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/storageclass-azuredisk-snapshot.yaml`

The output of the command resembles the following example:

`volumesnapshotclass.snapshot.storage.k8s.io/csi-azuredisk-vsc created`

Create a

[volume snapshot](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/azuredisk-volume-snapshot.yaml)from the PVC that was created earlier in this article.`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/azuredisk-volume-snapshot.yaml`

The output of the command resembles the following example:

`volumesnapshot.snapshot.storage.k8s.io/azuredisk-volume-snapshot created`

To verify that the snapshot was created correctly, run the following command:

`kubectl describe volumesnapshot azuredisk-volume-snapshot`

The output of the command resembles the following example:

`Name: azuredisk-volume-snapshot Namespace: default Labels: <none> Annotations: API Version: snapshot.storage.k8s.io/v1 Kind: VolumeSnapshot Metadata: Creation Timestamp: 2020-08-27T05:27:58Z Finalizers: snapshot.storage.kubernetes.io/volumesnapshot-as-source-protection snapshot.storage.kubernetes.io/volumesnapshot-bound-protection Generation: 1 Resource Version: 714582 Self Link: /apis/snapshot.storage.k8s.io/v1/namespaces/default/volumesnapshots/azuredisk-volume-snapshot UID: dd953ab5-6c24-42d4-ad4a-f33180e0ef87 Spec: Source: Persistent Volume Claim Name: pvc-azuredisk Volume Snapshot Class Name: csi-azuredisk-vsc Status: Bound Volume Snapshot Content Name: snapcontent-dd953ab5-6c24-42d4-ad4a-f33180e0ef87 Creation Time: 2020-08-31T05:27:59Z Ready To Use: true Restore Size: 10Gi Events: <none>`


### Create a new PVC based on a volume snapshot

You can create a new PVC based on a volume snapshot.

Use the snapshot created in the previous step, and create a

[new PVC](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/pvc-azuredisk-snapshot-restored.yaml)and a[new pod](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/nginx-pod-restored-snapshot.yaml)to consume it:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/pvc-azuredisk-snapshot-restored.yaml kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/nginx-pod-restored-snapshot.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk-snapshot-restored created pod/nginx-restored created`

To make sure it's the same PVC created before, check the contents by running the following command:

`kubectl exec nginx-restored -- ls /mnt/azuredisk`

The output of the command resembles the following example:

`lost+found outfile test.txt`


We can still see our previously created `test.txt`

file as expected.

## Clone volumes

A cloned volume is defined as a duplicate of an existing Kubernetes volume. For more information on cloning volumes in Kubernetes, see [volume cloning](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#volume-cloning).

Create a

[cloned volume](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml)of the[previously created](#create-azure-disk-pvs-using-built-in-storage-classes)`azuredisk-pvc`

and a[new pod](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml)to consume it.`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/cloning/pvc-azuredisk-cloning.yaml kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk-cloning created pod/nginx-restored-cloning created`

You can verify the content of the cloned volume by running the following command and confirming the file

`test.txt`

is created:`kubectl exec nginx-restored-cloning -- ls /mnt/azuredisk`

The output of the command resembles the following example:

`lost+found outfile test.txt`


## Resize an Azure Disk PV without downtime

You can request a larger volume for a PVC. Edit the PVC object, and specify a larger size. This change triggers the expansion of the underlying volume that backs the PV.

Note

A new PV is never created to satisfy the claim. Instead, an existing volume is resized.

In AKS, the built-in `managed-csi`

storage class already supports expansion, so use the [previously created](#create-azure-disk-pvs-using-built-in-storage-classes) one. The PVC requested a 10-Gi persistent volume. You can confirm by running the following command:

```
kubectl exec -it nginx-azuredisk -- df -h /mnt/azuredisk
```


The output of the command resembles the following example:

```
Filesystem Size Used Avail Use% Mounted on
/dev/sdc 9.8G 42M 9.8G 1% /mnt/azuredisk
```


Expand the PVC by increasing the

`spec.resources.requests.storage`

field running the following command:`kubectl patch pvc pvc-azuredisk --type merge --patch '{"spec": {"resources": {"requests": {"storage": "15Gi"}}}}'`

Note

Shrinking PVs is currently not supported. Trying to patch an existing PVC with a smaller size than the current one leads to the following error message:

`The persistentVolumeClaim "pvc-azuredisk" is invalid: spec.resources.requests.storage: Forbidden: field can not be less than previous value.`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk patched`

Run the following command to confirm the volume size increased:

`kubectl get pv`

The output of the command resembles the following example:

`NAME CAPACITY ACCESS MODES RECLAIM POLICY STATUS CLAIM STORAGECLASS REASON AGE pvc-391ea1a6-0191-4022-b915-c8dc4216174a 15Gi RWO Delete Bound default/pvc-azuredisk managed-csi 2d2h (...)`

And after a few minutes, run the following commands to confirm the size of the PVC:

`kubectl get pvc pvc-azuredisk`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE pvc-azuredisk Bound pvc-391ea1a6-0191-4022-b915-c8dc4216174a 15Gi RWO managed-csi 2d2h`

Run the following command to confirm the size of the disk inside the pod:

`kubectl exec -it nginx-azuredisk -- df -h /mnt/azuredisk`

The output of the command resembles the following example:

`Filesystem Size Used Avail Use% Mounted on /dev/sdc 15G 46M 15G 1% /mnt/azuredisk`


If your pod has *multiple containers*, you can specify which container by running the following command:

```
kubectl exec -it nginx-azuredisk -c <ContainerName> -- df -h /mnt/azuredisk
```


## Windows containers

The Azure Disk CSI driver supports Windows nodes and containers. If you want to use Windows containers, follow the [Windows containers quickstart](learn/quick-kubernetes-deploy-cli) to add a Windows node pool.

After you have a Windows node pool, you can now use the built-in storage classes like

`managed-csi`

. You can deploy an example[Windows-based stateful set](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/windows/statefulset.yaml)that saves timestamps into the file`data.txt`

by running the following[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/windows/statefulset.yaml`

The output of the command resembles the following example:

`statefulset.apps/busybox-azuredisk created`

To validate the content of the volume, run the following command:

`kubectl exec -it statefulset-azuredisk-win-0 -- powershell -c "type c:/mnt/azuredisk/data.txt"`

The output of the command resembles the following example:

`2020-08-27 08:13:41Z 2020-08-27 08:13:42Z 2020-08-27 08:13:44Z (...)`


## On-demand bursting

On-demand disk bursting model allows disk bursts whenever its needs exceed its current capacity. This model generates extra charges anytime the disk bursts. On-demand bursting is only available for premium SSDs larger than 512 GiB. For more information on premium SSDs provisioned IOPS and throughput per disk, see [Premium SSD size](/en-us/azure/virtual-machines/disks-types#premium-ssds). Alternatively, credit-based bursting is where the disk will burst only if it has burst credits accumulated in its credit bucket. Credit-based bursting doesn't generate extra charges when the disk bursts. Credit-based bursting is only available for premium SSDs 512 GiB and smaller, and standard SSDs 1,024 GiB and smaller. For more information on on-demand bursting, see [On-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting).

Important

The default `managed-csi-premium`

storage class has on-demand bursting disabled and uses credit-based bursting. Any premium SSD dynamically created by a persistent volume claim based on the default `managed-csi-premium`

storage class also has on-demand bursting disabled.

To create a premium SSD persistent volume with [on-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting) enabled, you can create a new storage class with the [enableBursting](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/docs/driver-parameters.md) parameter set to `true`

as shown in the following YAML template. For more information on enabling on-demand bursting, see [On-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting). For more information on building your own storage class with on-demand bursting enabled, see [Create a Burstable Managed CSI Premium Storage Class](https://github.com/Azure-Samples/burstable-managed-csi-premium).

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: burstable-managed-csi-premium
provisioner: disk.csi.azure.com
parameters:
skuname: Premium_LRS
enableBursting: "true"
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```


## Clean up resources

When you're done with the resources created in this article, you can remove them using the
`kubectl delete`

command.

```
# Remove the pod
kubectl delete -f azure-pvc-disk.yaml
# Remove the persistent volume claim
kubectl delete -f azure-pvc.yaml
```


## Provision Azure Files PVs

Azure Files supports Azure Premium file shares. The minimum file share capacity is 100 GiB. We recommend using Azure Premium file shares instead of Standard file shares because Premium file shares offer higher performance, low-latency disk support for I/O-intensive workloads. With Azure Files shares, there's no limit as to how many can be mounted on a node. For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

When you use storage CSI drivers on AKS, there are two more built-in `StorageClasses`

that uses the Azure Files CSI storage drivers. The other CSI storage classes are created with the cluster alongside the in-tree default storage classes.

`azurefile-csi`

: Uses Azure Standard Storage to create an Azure file share.`azurefile-csi-premium`

: Uses Azure Premium Storage to create an Azure file share.

The reclaim policy on both storage classes ensures that the underlying Azure files share is deleted when the respective PV is deleted. Since the storage classes also configure the file shares to be expandable, you just need to edit the [PVC](concepts-storage#persistent-volume-claims) with the new size.

Note

To have the best experience with Azure Files, follow these best practices. The location to configure mount options (`mountOptions`

) depends on whether you're provisioning dynamic or static persistent volumes.

- If you're dynamically provisioning a volume with a storage class, specify the mount options on the storage class object (kind:
`StorageClass`

). - If you're statically provisioning a volume, specify the mount options on the PersistentVolume object (kind:
`PersistentVolume`

). - If you're mounting the file share as an inline volume, specify the mount options on the Pod object (kind:
`Pod`

).

We recommend FIO when running benchmarking tests. For more information, see [benchmarking tools and tests](/en-us/azure/storage/files/nfs-performance#benchmarking-tools-and-tests).

A storage class is used to define how an Azure file share is created. A storage account is automatically created in the [node resource group](faq) for use with the storage class to hold the Azure files share. Choose one of the following [Azure storage redundancy SKUs](/en-us/azure/storage/common/storage-redundancy) for *skuName*:

Note

Modifying any resource under the node resource group in an AKS cluster is an unsupported action and will cause cluster operation failures. For more information, see [Why are two resource groups created with AKS?](faq)

**Standard_LRS**: Standard locally redundant storage**Standard_GRS**: Standard geo-redundant storage**Standard_ZRS**: Standard zone-redundant storage**Standard_RAGRS**: Standard read-access geo-redundant storage**Standard_RAGZRS**: Standard read-access geo-zone-redundant storage**Premium_LRS**: Premium locally redundant storage**Premium_ZRS**: Premium zone-redundant storage

For more information on Kubernetes storage classes for Azure Files, see [Kubernetes Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/#azure-file).

Create a file named

`azure-file-sc.yaml`

and copy in the following example manifest. For more information on`mountOptions`

, see the[Mount options](#mount-options)section.`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: my-azurefile provisioner: file.csi.azure.com # replace with "kubernetes.io/azure-file" if aks version is less than 1.21 allowVolumeExpansion: true mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict - actimeo=30 - nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks parameters: skuName: Premium_LRS`

Create the storage class using the

command.`kubectl apply`

`kubectl apply -f azure-file-sc.yaml`


### Create a PVC

A PVC uses the storage class object to dynamically provision an Azure file share. You can use the following YAML to create a PVC that's *100 GB* in size with *ReadWriteMany* access. For more information on access modes, see [Kubernetes persistent volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes).

Create a file named

`azure-file-pvc.yaml`

and copy in the following YAML. Make sure the`storageClassName`

matches the storage class you created in the previous step.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: my-azurefile spec: accessModes: - ReadWriteMany storageClassName: my-azurefile resources: requests: storage: 100Gi`

Note

If using the

`Premium_LRS`

SKU for your storage class, the minimum value for`storage`

must be`100Gi`

.Create the PVC using the

command.`kubectl apply`

`kubectl apply -f azure-file-pvc.yaml`

Once completed, the file share is created. A Kubernetes secret is also created that includes connection information and credentials. You can use the

command to view the status of the PVC:`kubectl get`

`kubectl get pvc my-azurefile`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE my-azurefile Bound pvc-8436e62e-a0d9-11e5-8521-5a8664dc0477 100Gi RWX my-azurefile 5m`


### Mount the PVC

The following YAML creates a pod that uses the PVC *my-azurefile* to mount the Azure Files file share at the */mnt/azure* path. For Windows Server containers, specify a `mountPath`

using the Windows path convention, such as *"D:"*.

Create a file named

`azure-pvc-files.yaml`

, and copy in the following YAML. Make sure the`claimName`

matches the PVC you created in the previous step.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: /mnt/azure name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: my-azurefile`

Create the pod using the

command.`kubectl apply`

`kubectl apply -f azure-pvc-files.yaml`

You now have a running pod with your Azure Files file share mounted in the

*/mnt/azure*directory. This configuration can be seen when inspecting your pod using thecommand. The following condensed example output shows the volume mounted in the container.`kubectl describe`

`Containers: mypod: Container ID: docker://053bc9c0df72232d755aa040bfba8b533fa696b123876108dec400e364d2523e Image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine Image ID: docker-pullable://nginx@sha256:d85914d547a6c92faa39ce7058bd7529baacab7e0cd4255442b04577c4d1f424 State: Running Started: Fri, 01 Mar 2019 23:56:16 +0000 Ready: True Mounts: /mnt/azure from volume (rw) /var/run/secrets/kubernetes.io/serviceaccount from default-token-8rv4z (ro) [...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: my-azurefile ReadOnly: false [...]`


### Mount options

For Kubernetes versions 1.13.0 and later, the default values for `fileMode`

and `dirMode`

are `0777`

. When dynamically provisioning PVs using a storage class, you can define mount options directly in the storage class manifest. For details, see [Mount options](https://kubernetes.io/docs/concepts/storage/storage-classes/#mount-options). The following example demonstrates setting these permissions to `0777`

:

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: my-azurefile
provisioner: file.csi.azure.com # replace with "kubernetes.io/azure-file" if aks version is less than 1.21
allowVolumeExpansion: true
mountOptions:
- dir_mode=0777
- file_mode=0777
- uid=0
- gid=0
- mfsymlinks
- cache=strict
- actimeo=30
- nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks
parameters:
skuName: Premium_LRS
```


## Storage class parameters for dynamic volumes

The following table includes parameters you can use to define a custom storage class for your PVC.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| accountAccessTier |
|

`Hot`

or `Cool`

, and Premium account can only choose `Premium`

.`102400`

`true`

or `false`

`false`

`true`

or `false`

`false`

`true`

or `false`

`false`

`eastus`

.`true`

or `false`

`false`

1`privateEndpoint`

is specified, a private endpoint is created for the storage account. For other cases, a service endpoint is created by default.`privateEndpoint`

`smb`

, `nfs`

`smb`

`true`

or `false`

`false`

`true`

or `false`

`false`

`accountname.privatelink.file.core.windows.net`

.`accountname.file.core.windows.net`

or other sovereign cloud account address.[Access tier for file share](/en-us/azure/storage/files/storage-files-planning#storage-tiers)`TransactionOptimized`

(default), `Hot`

, and `Cool`

. Premium storage account type for file shares only.`storageAccountType`

)`Standard_LRS`

, `Standard_ZRS`

, `Standard_GRS`

, `Standard_RAGRS`

, `Standard_RAGZRS`

,`Premium_LRS`

, `Premium_ZRS`

, `StandardV2_LRS`

, `StandardV2_ZRS`

, `StandardV2_GRS`

, `StandardV2_GZRS`

, `PremiumV2_LRS`

, `PremiumV2_ZRS`

`Standard_LRS`

Minimum file share size for Premium account type is 100 GB.

ZRS account type is supported in limited regions.

NFS file share only supports Premium account type.

Standard V2 SKU names are for

[Azure Files provisioned v2 model](/en-us/azure/storage/files/understanding-billing#provisioned-v2-model).`core.windows.net`

, `core.chinacloudapi.cn`

, etc.`core.windows.net`

.[Tags](/en-us/azure/azure-resource-manager/management/tag-resources)are created in new storage account.1 If the storage account is created by the driver, then you only need to specify
`networkEndpointType: privateEndpoint`

parameter in storage class. The CSI driver creates the
private endpoint and private DNS zone (named `privatelink.file.core.windows.net`

) together with the
account. If you bring your own storage account, then you need to
[create the private endpoint](/en-us/azure/storage/common/storage-private-endpoints) for the storage account. If you're
using Azure Files storage in a network isolated cluster, you must create a custom storage class with
"networkEndpointType: privateEndpoint". You can follow this sample for reference:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: azurefile-csi
provisioner: file.csi.azure.com
allowVolumeExpansion: true
parameters:
skuName: Premium_LRS # available values: Premium_LRS, Premium_ZRS, Standard_LRS, Standard_GRS, Standard_ZRS, Standard_RAGRS, Standard_RAGZRS
networkEndpointType: privateEndpoint
reclaimPolicy: Delete
volumeBindingMode: Immediate
mountOptions:
- dir_mode=0777 # modify this permission if you want to enhance the security
- file_mode=0777
- mfsymlinks
- cache=strict # https://linux.die.net/man/8/mount.cifs
- nosharesock # reduce probability of reconnect race
- actimeo=30 # reduce latency for metadata-heavy workload
- nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks
```


## Static provisioning parameters for PVs

The following table includes parameters you can use to define a PV.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| volumeAttributes.resourceGroup | Specify an Azure resource group name. | myResourceGroup | No | If empty, driver uses the same resource group name as current cluster. |
| volumeAttributes.storageAccount | Specify an existing Azure storage account name. | storageAccountName | Yes | |
| volumeAttributes.shareName | Specify an Azure file share name. | fileShareName | Yes | |
| volumeAttributes.folderName | Specify a folder name in Azure file share. | folderName | No | If folder name doesn't exist in file share, mount would fail. |
| volumeAttributes.protocol | Specify file share protocol. | `smb` , `nfs` |
No | `smb` |
| volumeAttributes.server | Specify Azure storage account server address | Existing server address, for example `accountname.privatelink.file.core.windows.net` . |
No | If empty, driver uses default `accountname.file.core.windows.net` or other sovereign cloud account address. |

## Create a PV snapshot class

The Azure Files CSI driver supports creating [snapshots of persistent volumes](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html) and the underlying file shares.

Create a

[volume snapshot class](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/snapshot/volumesnapshotclass-azurefile.yaml)with the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/snapshot/volumesnapshotclass-azurefile.yaml`

The output of the command resembles the following example:

`volumesnapshotclass.snapshot.storage.k8s.io/csi-azurefile-vsc created`

Create a

[volume snapshot](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/snapshot/volumesnapshot-azurefile.yaml)from the PVC created earlier (`pvc-azurefile`

).`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/snapshot/volumesnapshot-azurefile.yaml`

The output of the command resembles the following example:

`volumesnapshot.snapshot.storage.k8s.io/azurefile-volume-snapshot created`

Verify the snapshot was created correctly by running the following command:

`kubectl describe volumesnapshot azurefile-volume-snapshot`

The output of the command resembles the following example:

`Name: azurefile-volume-snapshot Namespace: default Labels: <none> Annotations: API Version: snapshot.storage.k8s.io/v1beta1 Kind: VolumeSnapshot Metadata: Creation Timestamp: 2020-08-27T22:37:41Z Finalizers: snapshot.storage.kubernetes.io/volumesnapshot-as-source-protection snapshot.storage.kubernetes.io/volumesnapshot-bound-protection Generation: 1 Resource Version: 955091 Self Link: /apis/snapshot.storage.k8s.io/v1beta1/namespaces/default/volumesnapshots/azurefile-volume-snapshot UID: c359a38f-35c1-4fb1-9da9-2c06d35ca0f4 Spec: Source: Persistent Volume Claim Name: pvc-azurefile Volume Snapshot Class Name: csi-azurefile-vsc Status: Bound Volume Snapshot Content Name: snapcontent-c359a38f-35c1-4fb1-9da9-2c06d35ca0f4 Ready To Use: false Events: <none>`


## Resize an Azure Files PV

You can request a larger volume for a PVC. Edit the PVC object, and specify a larger size. This change triggers the expansion of the underlying volume that backs the PV.

Note

A new PV is never created to satisfy the claim. Instead, an existing volume is resized. Shrinking persistent volumes is currently not supported.

In AKS, the built-in `azurefile-csi`

storage class already supports expansion, so use the PVC we created earlier with this storage class. The PVC requested a 100 GiB file share. We can confirm that by running:

```
kubectl exec -it nginx-azurefile -- df -h /mnt/azurefile
```


The output of the command resembles the following example:

```
Filesystem Size Used Avail Use% Mounted on
//f149b5a219bd34caeb07de9.file.core.windows.net/pvc-5e5d9980-da38-492b-8581-17e3cad01770 100G 128K 100G 1% /mnt/azurefile
```


Expand the PVC by increasing the

`spec.resources.requests.storage`

field:`kubectl patch pvc pvc-azurefile --type merge --patch '{"spec": {"resources": {"requests": {"storage": "200Gi"}}}}'`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azurefile patched`

Verify that both the PVC and the file system inside the pod show the new size:

`kubectl get pvc pvc-azurefile NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE pvc-azurefile Bound pvc-5e5d9980-da38-492b-8581-17e3cad01770 200Gi RWX azurefile-csi 64m kubectl exec -it nginx-azurefile -- df -h /mnt/azurefile Filesystem Size Used Avail Use% Mounted on //f149b5a219bd34caeb07de9.file.core.windows.net/pvc-5e5d9980-da38-492b-8581-17e3cad01770 200G 128K 200G 1% /mnt/azurefile`


## Use a PV with private Azure Files storage (private endpoint)

If your Azure Files resources are protected with a private endpoint, you must create your own storage class. Make sure to configure your [DNS settings to resolve the private endpoint IP address to the FQDN of the connection string](/en-us/azure/private-link/private-endpoint-dns#azure-services-dns-zone-configuration).

Customize the following parameters:

`resourceGroup`

: The resource group where the storage account is deployed.`storageAccount`

: The storage account name.`server`

: The FQDN of the storage account's private endpoint.

Create a file named

`private-azure-file-sc.yaml`

, and then paste the following example manifest in the file. Replace the values for`<resourceGroup>`

and`<storageAccountName>`

. For example:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: private-azurefile-csi provisioner: file.csi.azure.com allowVolumeExpansion: true parameters: resourceGroup: <resourceGroup> storageAccount: <storageAccountName> server: <storageAccountName>.file.core.windows.net reclaimPolicy: Delete volumeBindingMode: Immediate mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict # https://linux.die.net/man/8/mount.cifs - nosharesock # reduce probability of reconnect race - actimeo=30 # reduce latency for metadata-heavy workload`

Create the storage class by using the

`kubectl apply`

command:`kubectl apply -f private-azure-file-sc.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/private-azurefile-csi created`

Create a file named

`private-pvc.yaml`

, and then paste the following example manifest in the file:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: private-azurefile-pvc spec: accessModes: - ReadWriteMany storageClassName: private-azurefile-csi resources: requests: storage: 100Gi`

Create the PVC by using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f private-pvc.yaml`


## Use Managed Identity to access Azure Files storage (Preview)

Azure Files now supports managed identity-based authentication for SMB access. With this capability, your applications running in AKS can securely access Azure Files shares without the need to store or manage storage account keys or credentials. Managed identities provide a streamlined and secure authentication mechanism, simplifying access management and reducing the risk associated with credential exposure. You can create a dynamic volume or a static volume.

Note

Managed identity support for Azure Files in AKS is available in preview starting with AKS version 1.34 on Linux nodes.

To enable managed identity for dynamically provisioned volumes, follow these steps:

Create a storage class with managed identity enabled using a YAML file, for example,

`azurefile-csi-managed-identity.yaml`

with the following sample content. Set`mountWithManagedIdentity: "true"`

under`parameters`

:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azurefile-csi provisioner: file.csi.azure.com parameters: resourceGroup: EXISTING_RESOURCE_GROUP_NAME # optional, node resource group by default if it's not provided storageAccount: EXISTING_STORAGE_ACCOUNT_NAME # optional, a new account will be created if it's not provided mountWithManagedIdentity: "true" # optional, clientID of the managed identity, kubelet identity would be used by default if it's not provided clientID: "xxxxx-xxxx-xxx-xxx-xxxxxxx" reclaimPolicy: Delete volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - dir_mode=0777 # modify this permission if you want to enhance the security - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict # https://linux.die.net/man/8/mount.cifs - nosharesock # reduce probability of reconnect race - actimeo=30 # reduce latency for metadata-heavy workload - nobrl # disable sending byte range lock requests to the server`

Apply this storage class by running the following command:

`kubectl apply -f azurefile-csi-managed-identity.yaml`

Deploy your

**StatefulSet**or workload using the new storage class that references this PVC to ensure that the volume is provisioned using managed identity authentication. In your PVC manifest, set`storageClassName: azurefile-csi-managed-identity`

. For example:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azurefile-managed-identity-pvc spec: accessModes: - ReadWriteMany storageClassName: azurefile-csi-managed-identity resources: requests: storage: 100Gi`


## Learn about Azure Files NFS

Azure Files supports the
[NFS v4.1 protocol](/en-us/azure/storage/files/storage-files-how-to-create-nfs-shares). NFS version 4.1
support for Azure Files provides you with a fully managed NFS system as a service built on highly
available, highly durable distributed resilient storage platform.

This option is optimized for random access workloads with in-place data updates and provides full POSIX file system support. This section shows you how to use NFS shares with the Azure File CSI driver on an AKS cluster.

Note

You can use a private endpoint instead of allowing access to the selected VNet.

This section explains how to maximize performance and security when using Azure Files NFS 4.1 with AKS. Learn how to:

Optimize NFS read and write size settings

Create and configure an NFS storage class

Deploy workloads that use NFS-backed volumes

Enable Encryption in Transit (EiT) to protect data as it moves between your AKS cluster and Azure Files.


This section provides information about how to approach performance tuning NFS with the Azure Files
CSI driver with the `rsize`

(read size) and `wsize`

(write size) options. The `rsize`

and `wsize`

options set the maximum transfer size of an NFS operation. If `rsize`

or `wsize`

aren't specified on
mount, the client and server negotiate the largest size supported by the two. Currently, both Azure
Files and modern Linux distributions support read and write sizes as large as 1,048,576 bytes (1
MiB).

Optimal performance is based on efficient client-server communication. Increasing or decreasing the
**mount** read and write option size values can improve NFS performance. The default size of the
read/write packets transferred between client and server are 8 KB for NFS version 2, and 32 KB for
NFS version 3 and 4. These defaults might be too large or too small. Reducing the `rsize`

and
`wsize`

might improve NFS performance in a congested network by sending smaller packets for each
NFS-read reply and write request. However, this reduction can increase the number of packets needed
to send data across the network, increasing total network traffic and CPU utilization on the client
and server.

It's important that you perform testing to find an `rsize`

and `wsize`

that sustains efficient
packet transfer, where it doesn't decrease throughput and increase latency.

For example, to configure a maximum `rsize`

and `wsize`

of 256-KiB, configure the `mountOptions`

in
the storage class as follows:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: azurefile-csi-nfs
provisioner: file.csi.azure.com
allowVolumeExpansion: true
parameters:
protocol: nfs
mountOptions:
- nconnect=4
- noresvport
- actimeo=30
- rsize=262144
- wsize=262144
```


## Other storage class examples

## Windows containers

The Azure Files CSI driver also supports Windows nodes and containers. To use Windows containers, follow the [Windows containers quickstart](learn/quick-windows-container-deploy-cli) to add a Windows node pool.

After you have a Windows node pool, use the built-in storage classes like

`azurefile-csi`

or create a custom one. You can deploy an example[Windows-based stateful set](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/windows/statefulset.yaml)that saves timestamps into a file`data.txt`

by running the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/windows/statefulset.yaml`

The output of the command resembles the following example:

`statefulset.apps/busybox-azurefile created`

Validate the contents of the volume by running the following

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command:`kubectl exec -it busybox-azurefile-0 -- cat c:\\mnt\\azurefile\\data.txt # on Linux or MacOS Bash kubectl exec -it busybox-azurefile-0 -- cat c:\mnt\azurefile\data.txt # on Windows Powershell or CMD`

The output of the commands resembles the following example:

`2020-08-27 22:11:01Z 2020-08-27 22:11:02Z 2020-08-27 22:11:04Z (...)`


## Next steps

- For Azure Files CSI driver parameters, see
[CSI driver parameters](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/docs/driver-parameters.md#static-provisionbring-your-own-file-share). - For more information about disk-based storage solutions, see
[Disk-based solutions in AKS](/en-us/azure/cloud-adoption-framework/scenarios/app-platform/aks/storage#disk-based-solutions). - For more information about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service](operator-best-practices-storage). - For more information about Azure ultra disk, see [Use ultra disks on Azure Kubernetes Service (AKS)][use-ultra-disks].
- For more information about Azure tags, see
[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-disk-csi -->

# Azure storage CSI driver and volume provisioning

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Blob storage Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant driver used by Azure Kubernetes Service (AKS) to
manage the lifecycle of Azure Blob storage. The CSI is a standard for exposing arbitrary block and
file storage systems to containerized workloads on Kubernetes.

By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids having to touch the core Kubernetes code and wait for its release cycles.

When you mount Azure Blob storage as a file system into a container or pod, it enables you to use blob storage with many applications that work massive amounts of unstructured data. For example:

- Log file data
- Images, documents, and streaming video or audio
- Disaster recovery data

Applications access data stored in Azure Blob storage using either BlobFuse or the Network File System (NFS) 3.0 protocol. Before the introduction of the Azure Blob storage CSI driver, the only option was to manually install an unsupported driver to access Blob storage from your application running on AKS. When the Azure Blob storage CSI driver is enabled on AKS, there are two built-in storage classes:

- azureblob-fuse-premium
- azureblob-nfs-premium

To create an AKS cluster with CSI drivers support, see [CSI drivers on AKS](csi-storage-drivers). To
learn more about the differences in access between each of the Azure storage types using the NFS
protocol, see
[Compare access to Azure Files, Blob Storage, and Azure NetApp Files with NFS](/en-us/azure/storage/common/nfs-comparison).

The Azure Disks Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant
driver used by Azure Kubernetes Service (AKS) to manage the lifecycle of Azure Disk.

The CSI is a standard for exposing arbitrary block and file storage systems to containerized
workloads on Kubernetes. By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins
to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids
having to touch the core Kubernetes code and wait for its release cycles. To create an AKS cluster
with CSI driver support, see [Enable CSI driver on AKS](csi-storage-drivers).

For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

Note

*In-tree drivers* refer to the current storage drivers that are part of the core Kubernetes code versus the new CSI drivers, which are plug-ins.

The Azure Files Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant driver used by Azure Kubernetes Service (AKS) to
manage the lifecycle of Azure file shares. The CSI is a standard for exposing arbitrary block and
file storage systems to containerized workloads on Kubernetes.

By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids having to touch the core Kubernetes code and wait for its release cycles.

To create an AKS cluster with CSI drivers support, see [Enable CSI drivers on AKS](csi-storage-drivers).

Note

*In-tree drivers* refer to the current storage drivers that are part of the core Kubernetes code versus the new CSI drivers, which are plug-ins.

## Azure CSI driver features

Azure Blob storage CSI driver supports the following features:

- BlobFuse
- NFS 3.0 protocol

In addition to in-tree driver features, Azure Disk CSI driver supports the following features:

Performance improvements during concurrent disk attach and detach

- In-tree drivers attach or detach disks in serial, while CSI drivers attach or detach disks in batch. There's significant improvement when there are multiple disks attaching to one node.

Premium SSD v1 and v2 are supported.

`PremiumV2_LRS`

only supports`None`

caching mode

Zone-redundant storage (ZRS) disk support

`Premium_ZRS`

,`StandardSSD_ZRS`

disk types are supported. ZRS disk could be scheduled on the zone or non-zone node, without the restriction that disk volume should be colocated in the same zone as a given node. For more information, including which regions are supported, see[Zone-redundant storage for managed disks](/en-us/azure/virtual-machines/disks-redundancy).


Note

Depending on the VM SKU that's being used, the Azure Disk CSI driver might have a per-node volume limit. For some powerful VMs (for example, 16 cores), the limit is 64 volumes per node. To identify the limit per VM SKU, review the **Max data disks** column for each VM SKU offered. For a list of VM SKUs offered and their corresponding detailed capacity limits, see [General purpose virtual machine sizes](/en-us/azure/virtual-machines/sizes-general).

## Prerequisites

You must have the Azure CLI version 2.42 or later installed and configured. To find the version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you installed the Azure CLI`aks-preview`

extension, make sure that you update the extension to the latest version by calling`az extension update --name aks-preview`

.Perform the following steps to

[clean up the open source driver](https://github.com/kubernetes-sigs/blob-csi-driver/blob/master/docs/install-csi-driver-master.md#clean-up-blob-csi-driver)if you previously installed the[CSI Blob Storage open-source driver](https://github.com/kubernetes-sigs/blob-csi-driver)to access Azure Blob storage from your cluster.Your AKS cluster

*Control plane*identity (your AKS cluster name) is added to the[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)role on the VNet and network security group.To support an [Azure Data Lake Storage Gen2 account][azure-datalake-storage-account] (ADLS) when using BlobFuse mount, perform the following actions:

- To create an ADLS account using the driver in dynamic provisioning, specify
`isHnsEnabled: "true"`

in the storage class parameters. - To enable BlobFuse access to an ADLS account in static provisioning, specify the mount option
`--use-adls=true`

in the persistent volume. - If you're going to enable a storage account with Hierarchical Namespace, existing persistent volumes (PVs) should be remounted with
`--use-adls=true`

mount option.

- To create an ADLS account using the driver in dynamic provisioning, specify
By default, the BlobFuse cache is located in the

`/mnt`

directory. If the virtual machine (VM) SKU provides a temporary disk, the`/mnt`

directory is mounted on the temporary disk. However, if the VM SKU doesn't provide a temporary disk, the`/mnt`

directory is mounted on the OS disk, you could set`--tmp-path=`

mount option to specify a different cache directory.

Note

If the **blobfuse-proxy** isn't enabled during the installation of the open source driver, the uninstallation of the open source driver disrupts existing blobfuse mounts. However, NFS mounts remain unaffected.

You must have an AKS cluster with the Azure Disk CSI driver enabled. The CSI driver is enabled by default on AKS clusters running Kubernetes version 1.21 or later.

Azure CLI version 2.37.0 or later is installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`kubectl`

command-line tool is installed and configured to connect to your AKS cluster.A storage class configured to use the Azure Disk CSI driver (

`disk.csi.azure.com`

).The Azure Disk CSI driver has a per-node volume limit. The volume count changes based on the size of the node/node pool. Run the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command to determine the number of volumes that can be allocated per node:`kubectl get CSINode <nodename> -o yaml`

If the per-node volume limit is an issue for your workload, consider using

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for persistent volumes instead of CSI drivers.

**General requirements:**

You must have an AKS cluster with the Azure Files CSI driver enabled. The Azure Files CSI driver is enabled by default on AKS clusters running Kubernetes version 1.21 or later.

Azure CLI version 2.37.0 or later is installed and configured. To check your version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`kubectl`

command-line tool is installed and configured to connect to your AKS cluster.A storage class configured to use the Azure Files CSI driver (

`file.csi.azure.com`

).When choosing between standard and premium file shares, it's important you understand the provisioning model and requirements of the expected usage pattern you plan to run on Azure Files. For more information, see

[Choosing an Azure Files performance tier based on usage patterns](/en-us/azure/storage/files/understand-performance#choosing-a-performance-tier-based-on-usage-patterns).

**Network File Share (NFS) requirements:**

Your AKS cluster

*Control plane*identity (your AKS cluster name) is added to the[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)role on the VNet and**NetworkSecurityGroup**.Your AKS cluster's service principal or managed service identity (MSI) must be added to the

**Contributor**role to the storage account.

**Managed Identity requirements:**

Ensure the

[user-assigned Kubelet identity](use-managed-identity#create-a-kubelet-managed-identity)is granted the`Storage File Data SMB MI Admin`

role on the storage account. If you use your own storage account, you need to assign`Storage File Data SMB MI Admin`

role to the user-assigned Kubelet identity on that storage account.If the CSI driver creates the storage account, grant the

`Storage File Data SMB MI Admin`

role to the resource group where the storage account resides.If you use the default built-in user-assigned Kubelet identity, it already has the required

`Storage File Data SMB MI Admin`

role on the managed node resource group.

Note

The Azure File CSI driver only permits the mounting of SMB file shares using key-based (NTLM v2) authentication, and therefore doesn't support the maximum security profile of Azure File share settings. On the other hand, mounting NFS file shares doesn't require key-based authentication.

## Enable CSI driver on a new or existing AKS cluster

Using the Azure CLI, you can enable the Blob storage CSI driver on a new or existing AKS cluster before you configure a persistent volume for use by pods in the cluster.

To enable the driver on a new cluster, include the

`--enable-blob-driver`

parameter with the`az aks create`

command as shown in the following example:`az aks create \ --enable-blob-driver \ --name myAKSCluster \ --resource-group myResourceGroup \ --generate-ssh-keys`

To enable the driver on an existing cluster, include the

`--enable-blob-driver`

parameter with the`az aks update`

command as shown in the following example:`az aks update --enable-blob-driver --name myAKSCluster --resource-group myResourceGroup`


You're prompted to confirm there isn't an open-source Blob CSI driver installed. After you confirm, it might take several minutes to complete this action. Once it's complete, you should see in the output the status of enabling the driver on your cluster. The following example resembles the section indicating the results of the previous command:

```
"storageProfile": {
"blobCsiDriver": {
"enabled": true
},
...
}
```


## Disable CSI driver on an existing AKS cluster

Using the Azure CLI, you can disable the Blob storage CSI driver on an existing AKS cluster after you remove the persistent volume from the cluster.

To disable the driver on an existing cluster, include the

`--disable-blob-driver`

parameter with the`az aks update`

command as shown in the following example:`az aks update --disable-blob-driver --name myAKSCluster --resource-group myResourceGroup`


## Use a persistent volume for storage

Kubernetes assigns a [persistent volume](concepts-storage#persistent-volumes) (PV) as a storage resource to one or more pods. You can provision PVs dynamically through Kubernetes or statically as an administrator.

If multiple pods need concurrent access to the same storage volume, you can use Azure Blob storage to connect by using NFS or BlobFuse. This article shows you how to dynamically create an Azure Blob storage container for use by multiple pods in an AKS cluster.

For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

This article shows you how to dynamically create a PV with Azure disk for use by a single pod in an AKS cluster.

If multiple pods need concurrent access to the same storage volume, you can use Azure Files to
connect by using the [Server Message Block (SMB)](/en-us/windows/desktop/FileIO/microsoft-smb-protocol-and-cifs-protocol-overview) or
[Network File System (NFS)](/en-us/windows-server/storage/nfs/nfs-overview). This article shows you how to dynamically create an Azure
Files share for use by multiple pods in an AKS cluster.

**Dynamically provisioned volume:** Use this approach when you want Kubernetes to automatically
create and manage storage resources. It's ideal for scenarios where you need on-demand scaling,
prefer infrastructure-as-code, and want to minimize manual configuration steps.

**Statically provisioned volume:** Choose this method if you already have an Azure Blob storage
account or container that you want to use. It provides more control over storage setup, access, and
lifecycle, and is suitable when you need to connect to existing resources or reuse storage across
multiple clusters or workloads.

This section provides guidance for cluster administrators who want to provision one or more persistent volumes that include details of Blob storage for use by a workload. A persistent volume claim (PVC) uses the storage class object to dynamically provision an Azure Blob storage container.

To provision a persistent volume using Azure Blob storage with the provided storage class, follow these steps:

Create the

`StorageClass`

manifest by saving the following YAML to a file named`blob-fuse-sc.yaml`

:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: blob-fuse provisioner: blob.csi.azure.com parameters: skuName: Premium_LRS # available values: Standard_LRS, Premium_LRS, Standard_GRS, Standard_RAGRS, Standard_ZRS, Premium_ZRS protocol: fuse2 networkEndpointType: privateEndpoint reclaimPolicy: Delete volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - -o allow_other - --file-cache-timeout-in-seconds=120 - --use-attr-cache=true - --cancel-list-on-mount-seconds=10 # prevent billing charges on mounting - -o attr_timeout=120 - -o entry_timeout=120 - -o negative_timeout=120 - --log-level=LOG_WARNING # LOG_WARNING, LOG_INFO, LOG_DEBUG - --cache-size-mb=1000 # Default will be 80% of available memory, eviction will happen beyond specified value.`

To create the storage class in your cluster, apply the

`StorageClass`

by running the following command:`kubectl apply -f blob-fuse-sc.yaml`


## Create a PVC using built-in storage class

A storage class is used to define how an Azure Blob storage container is created. A storage account is automatically created in the node resource group for use with the storage class to hold the Azure Blob storage container. Choose one of the following Azure storage redundancy SKUs for skuName:

Note

Modifying any resource under the node resource group in an AKS cluster is an unsupported action and will cause cluster operation failures. For more information, see [Why are two resource groups created with AKS?](faq)

**Standard_LRS**: Standard locally redundant storage**Premium_LRS**: Premium locally redundant storage**Standard_ZRS**: Standard zone redundant storage**Premium_ZRS**: Premium zone redundant storage**Standard_GRS**: Standard geo-redundant storage**Standard_RAGRS**: Standard read-access geo-redundant storage

When you use storage CSI drivers on AKS, there are two other built-in `StorageClasses`

that use the Azure Blob CSI storage driver.

The reclaim policy on both storage classes ensures that the underlying Azure Blob storage is deleted
when the respective PV is deleted. The storage classes also configure the container to be expandable
by default, as the `set allowVolumeExpansion`

parameter is set to **true**.

Note

Shrinking persistent volumes isn't supported.

Use the [kubectl get sc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command to see the storage classes. The following example
shows the `azureblob-fuse-premium`

and `azureblob-nfs-premium`

storage classes available within an
AKS cluster:

```
NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE
azureblob-fuse-premium blob.csi.azure.com Delete Immediate true 23h
azureblob-nfs-premium blob.csi.azure.com Delete Immediate true 23h
```


To use these storage classes, create a PVC and respective pod that references and uses them. A PVC is used to automatically allocate storage based on a storage class. You can create a PVC using one of the built-in storage classes or a custom storage class. This PVC creates an Azure Blob storage container with your specified SKU, size, and protocol. When you create a pod definition, the PVC is specified to request the desired storage.

A PVC uses the storage class object to dynamically provision an Azure Blob storage container. The following YAML can be used to create a 5 GB PVC with *ReadWriteMany* access, using the built-in storage class. For more information on access modes, see the [Kubernetes persistent volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) documentation.

Create a file named

`blob-nfs-pvc.yaml`

and copy the following YAML:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azure-blob-storage spec: accessModes: - ReadWriteMany storageClassName: azureblob-nfs-premium resources: requests: storage: 5Gi`

Create the PVC with the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command:`kubectl create -f blob-nfs-pvc.yaml`


Once complete, the Blob storage container is created. You can use the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)
command to view the status of the PVC:

```
kubectl get pvc azure-blob-storage
```


The output of the command resembles the following example:

```
NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE
azure-blob-storage Bound pvc-b88e36c5-c518-4d38-a5ee-337a7dda0a68 5Gi RWX azureblob-nfs-premium 92m
```


## Mount the PVC

The following YAML creates a pod that uses the PVC **azure-blob-storage** to mount the Azure Blob storage at the `/mnt/blob`

path.

Create a file named

`blob-nfs-pv`

, and copy the following YAML. Make sure that the**claimName**matches the PVC created in the previous step.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/blob" name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: azure-blob-storage`

Create the pod with the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f blob-nfs-pv.yaml`

After the pod is in the running state, run the following command to create a new file called

`test.txt`

.`kubectl exec mypod -- touch /mnt/blob/test.txt`

To validate the disk is correctly mounted, run the following command, and verify you see the

`test.txt`

file in the output:`kubectl exec mypod -- ls /mnt/blob`

The output of the command resembles the following example:

`test.txt`


## Create an Azure Blob custom storage class

The default storage classes suit the most common scenarios, but not all. In some cases, you might want to have your own storage class customized with your own parameters. In this section, we provide two examples with the first one using the NFS protocol, and the second one using BlobFuse.

In this example, the following manifest configures mounting a Blob storage container using the NFS
protocol. Use it to add the `tags`

parameter.

Create a file named

`blob-nfs-sc.yaml`

, and paste the following example manifest:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azureblob-nfs-premium provisioner: blob.csi.azure.com parameters: protocol: nfs tags: environment=Development volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - nconnect=4`

Create the storage class with the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f blob-nfs-sc.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/blob-nfs-premium created`


## Mount an NFS or BlobFuse PV

In this section, you mount the PV using the NFS protocol or BlobFuse.

Mounting Blob storage using the NFS v3 protocol doesn't authenticate using an account key. Your AKS
cluster needs to reside in the same or peered virtual network as the agent node. The only way to
secure the data in your storage account is by using a virtual network and other network security
settings. For more information on how to set up NFS access to your storage account, see
[Mount Blob Storage by using the Network File System (NFS) 3.0 protocol](/en-us/azure/storage/blobs/network-file-system-protocol-support-how-to).

The following example demonstrates how to mount a Blob storage container as a persistent volume using the NFS protocol.

Create a file named

`pv-blob-nfs.yaml`

and copy in the following YAML. Under`storageClass`

, update`resourceGroup`

,`storageAccount`

, and`containerName`

.Note

The

`volumeHandle`

value within your YAML should be a unique volumeID for every identical storage blob container in the cluster.The characters

`#`

and`/`

are reserved for internal use and can't be used.`apiVersion: v1 kind: PersistentVolume metadata: annotations: pv.kubernetes.io/provisioned-by: blob.csi.azure.com name: pv-blob spec: capacity: storage: 1Pi accessModes: - ReadWriteMany persistentVolumeReclaimPolicy: Retain # If set as "Delete" container would be removed after pvc deletion storageClassName: azureblob-nfs-premium mountOptions: - nconnect=4 csi: driver: blob.csi.azure.com # make sure volumeid is unique for every identical storage blob container in the cluster # character `#` and `/` are reserved for internal use and cannot be used in volumehandle volumeHandle: account-name_container-name volumeAttributes: resourceGroup: resourceGroupName storageAccount: storageAccountName containerName: containerName protocol: nfs`

Note

While the

[Kubernetes API](https://github.com/kubernetes/kubernetes/blob/release-1.26/pkg/apis/core/types.go#L303-L306)**capacity**attribute is mandatory, this value isn't used by the Azure Blob storage CSI driver because you can flexibly write data until you reach your storage account's capacity limit. The value of the`capacity`

attribute is used only for size matching between*PVs*and*PVCs*. We recommend using a fictitious high value. The pod sees a mounted volume with a fictitious size of 5 Petabytes.Run the following command to create the persistent volume using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command referencing the YAML file created earlier:`kubectl create -f pv-blob-nfs.yaml`

Create a

`pvc-blob-nfs.yaml`

file with a*PersistentVolumeClaim*. For example:`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: pvc-blob spec: accessModes: - ReadWriteMany resources: requests: storage: 10Gi volumeName: pv-blob storageClassName: azureblob-nfs-premium`

Run the following command to create the persistent volume claim using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command referencing the YAML file created earlier:`kubectl create -f pvc-blob-nfs.yaml`


## Create a pod

The following YAML creates a pod that uses the PV or PVC named **pvc-blob** created earlier, to mount the Azure Blob storage at the `/mnt/blob`

path.

Create a file named

`nginx-pod-blob.yaml`

, and copy in the following YAML. Make sure that the**claimName**matches the PVC created in the previous step when creating a PV for NFS or BlobFuse.`kind: Pod apiVersion: v1 metadata: name: nginx-blob spec: nodeSelector: "kubernetes.io/os": linux containers: - image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine name: nginx-blob volumeMounts: - name: blob01 mountPath: "/mnt/blob" readOnly: false volumes: - name: blob01 persistentVolumeClaim: claimName: pvc-blob`

Run the following command to create the pod and mount the PVC using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command:`kubectl create -f nginx-pod-blob.yaml`

Run the following command to create an interactive shell session with the pod to verify if the Blob storage is mounted:

`kubectl exec -it nginx-blob -- df -h`

The output from the command resembles the following example:

`Filesystem Size Used Avail Use% Mounted on ... blobfuse 14G 41M 13G 1% /mnt/blob ...`


## Create a StatefulSet

To ensure your workload retains its storage volume across pod restarts or replacements, use a StatefulSet. StatefulSets simplify the process of associating persistent storage with pods, so that new pods created to replace failed ones can automatically access the same storage volumes. The following examples demonstrate how to set up a StatefulSet for Blob storage using either BlobFuse or the NFS protocol.

Create a file named

`azure-blob-nfs-ss.yaml`

and copy in the following YAML.`apiVersion: apps/v1 kind: StatefulSet metadata: name: statefulset-blob-nfs labels: app: nginx spec: serviceName: statefulset-blob-nfs replicas: 1 template: metadata: labels: app: nginx spec: nodeSelector: "kubernetes.io/os": linux containers: - name: statefulset-blob-nfs image: mcr.microsoft.com/azurelinux/base/nginx:1.25 volumeMounts: - name: persistent-storage mountPath: /mnt/blob updateStrategy: type: RollingUpdate selector: matchLabels: app: nginx volumeClaimTemplates: - metadata: name: persistent-storage spec: storageClassName: azureblob-nfs-premium accessModes: ["ReadWriteMany"] resources: requests: storage: 100Gi`

Create the StatefulSet with the

`kubectl create`

command:`kubectl create -f azure-blob-nfs-ss.yaml`


### Dynamic PVC storage class parameters

The following table includes parameters you can use to define a custom storage class for your dynamic PVC.

| Name | Description | Example | Mandatory | Default value |
|---|---|---|---|---|
| skuName | Specify an Azure storage account type (alias: `storageAccountType` ). |
`Standard_LRS` , `Premium_LRS` , `Standard_GRS` , `Standard_RAGRS` |
No | `Standard_LRS` |
| location | Specify an Azure location. | `eastus` |
No | If empty, the driver uses the same location name as current cluster. |
| resourceGroup | Specify an Azure resource group name. | myResourceGroup | No | If empty, the driver uses the same resource group name as current cluster. |
| storageAccount | Specify an Azure storage account name. | storageAccountName | No | When a specific storage account name isn't provided, the driver looks for a suitable storage account that matches the account settings within the same resource group. If it fails to find a matching storage account, it creates a new one. However, if a storage account name is specified, the storage account must already exist. |
networkEndpointType 1 |
Specify network endpoint type for the storage account created by driver. If privateEndpoint is specified, a
|

`privateEndpoint`

`fuse`

, `nfs`

`fuse`

`pvc-fuse`

for BlobFuse or `pvc-nfs`

for NFS v3.`<storage-account>.blob.core.windows.net`

.`<storage-account>.blob.core.windows.net`

or other sovereign cloud storage account DNS domain name.`true`

,`false`

`false`

`core.windows.net`

`true`

,`false`

`false`

1 If the storage account is created by the driver, then you only need to specify `networkEndpointType: privateEndpoint`

parameter in storage class. The CSI driver creates the private endpoint and private DNS zone (named `privatelink.blob.core.windows.net`

) together with the account. If you bring your own storage account, then you need to [create the private endpoint](/en-us/azure/storage/common/storage-private-endpoints) for the storage account. If you're using Azure Blob storage in a network isolated cluster, you must create a custom storage class with `networkEndpointType: privateEndpoint`

.

### Static PV provisioning parameters

The following table includes parameters you can use to define your static PV.

| Name | Description | Example | Mandatory | Default value |
|---|---|---|---|---|
| volumeHandle | Specify a value the driver can use to uniquely identify the storage blob container in the cluster. | A recommended way to produce a unique value is to combine the globally unique storage account name and container name: `{account-name}_{container-name}` . The `#` and `/` characters are reserved for internal use and can't be used in a volume handle. |
Yes | |
| volumeAttributes.resourceGroup | Specify Azure resource group name. | myResourceGroup | No | If empty, driver uses the same resource group name as current cluster. |
| volumeAttributes.storageAccount | Specify an existing Azure storage account name. | storageAccountName | Yes | |
| volumeAttributes.containerName | Specify existing container name. | container | Yes | |
| volumeAttributes.protocol | Specify BlobFuse mount or NFS v3 mount. | `fuse` , `nfs` |
No | `fuse` |

## Create Azure Disk PVs using built-in storage classes

A storage class is used to define how a unit of storage is dynamically created with a PV. For more information on Kubernetes storage classes, see [Kubernetes storage classes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

When you use the Azure Disk CSI driver on AKS, there are two more built-in `StorageClasses`

that use the Azure Disk CSI storage driver. The other CSI storage classes are created with the cluster alongside the in-tree default storage classes.

`managed-csi`

: Creates managed disks using Azure Standard SSD with locally redundant storage (LRS). With Kubernetes version 1.29 for AKS clusters deployed across multiple availability zones, this storage class uses Azure Standard SSD zone-redundant storage (ZRS) to provision managed disks.`managed-csi-premium`

: Provisions managed disks using Azure Premium LRS. Beginning with Kubernetes version 1.29, for AKS clusters spanning multiple availability zones, this storage class automatically uses Azure Premium ZRS to create managed disks.

Effective starting with Kubernetes version 1.29, when you deploy Azure Kubernetes Service (AKS) clusters across multiple availability zones, AKS now utilizes zone-redundant storage (ZRS) to create managed disks within built-in storage classes.

ZRS ensures synchronous replication of your Azure managed disks across multiple Azure availability zones in your chosen region. This redundancy strategy enhances the resilience of your applications and safeguards your data against datacenter failures.

However, it's important to note that zone-redundant storage (ZRS) comes at a higher cost compared to locally redundant storage (LRS). If cost optimization is a priority, you can create a new storage class with the LRS SKU name parameter and use it in your persistent volume claim.


Reducing the size of a PVC isn't supported due to the risk of data loss. You can edit an existing storage class using the `kubectl edit sc`

command, or you can create your own custom storage class. For example, if you want to use a disk of size 4 TiB, you must create a storage class that defines `cachingmode: None`

because [disk caching isn't supported for disks 4 TiB and larger][disk-host-cache-setting]. For more information about storage classes and creating your own storage class, see [Storage options for applications in AKS](concepts-storage#storage-classes).

The reclaim policy in both storage classes ensures that the underlying Azure Disks are deleted when the respective PV is deleted. The storage classes also configure the PVs to be expandable. You just need to edit the PVC with the new size.

To use these storage classes, create a [PVC](concepts-storage#persistent-volume-claims) and respective pod that references and uses them. A PVC is used to automatically provision storage based on a storage class. A PVC can use one of the precreated storage classes or a user-defined storage class to create an Azure-managed disk for the desired SKU and size. When you create a pod definition, the PVC is specified to request the desired storage.

Note

Persistent volume claims are specified in GiB but Azure managed disks are billed based on the SKU for a specific size. These SKUs range from 32GiB for S4 or P4 disks to 32TiB for S80 or P80 disks (in preview). The throughput and IOPS performance of a Premium managed disk depends on both the SKU and the instance size of the nodes in the AKS cluster. For more information, see [Pricing and performance of managed disks](https://azure.microsoft.com/pricing/details/managed-disks/).

You can see the precreated storage classes using the [ kubectl get sc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. The following example shows the precreated storage classes available within an AKS cluster:

```
kubectl get sc
```


The output of the command resembles the following example:

```
NAME PROVISIONER AGE
default (default) disk.csi.azure.com 1h
managed-csi disk.csi.azure.com 1h
```


A PVC automatically provisions storage based on a storage class. In this case, a PVC can use one of the precreated storage classes to create a standard or premium Azure managed disk.

Create a file named

`azure-pvc.yaml`

and copy in the following manifest. The claim requests a disk named`azure-managed-disk`

that's`5 GB`

in size with`ReadWriteOnce`

access. The*managed-csi*storage class is specified as the storage class.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azure-managed-disk spec: accessModes: - ReadWriteOnce storageClassName: managed-csi resources: requests: storage: 5Gi`

Tip

To create a disk that uses premium storage, use

`storageClassName: managed-csi-premium`

rather than*managed-csi*.Create the persistent volume claim using the

command and specify your`kubectl apply`

*azure-pvc.yaml*file.`kubectl apply -f azure-pvc.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/azure-managed-disk created`


## Apply a PVC to a pod

After you create the persistent volume claim, you must verify it has a status of `Pending`

. The `Pending`

status indicates it's ready to be used by a pod.

Verify the status of the PVC using the

`kubectl describe pvc`

command.`kubectl describe pvc azure-managed-disk`

The output of the command resembles the following condensed example:

`Name: azure-managed-disk Namespace: default StorageClass: managed-csi Status: Pending [...]`

Create a file named

`azure-pvc-disk.yaml`

and copy in the following manifest. This manifest creates a basic NGINX pod that uses the persistent volume claim named`azure-managed-disk`

to mount the Azure Disk at the path`/mnt/azure`

. For Windows Server containers, specify a`mountPath`

using the Windows path convention, such as*'D:'*.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/azure" name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: azure-managed-disk`

Create the pod using the

command.`kubectl apply`

`kubectl apply -f azure-pvc-disk.yaml`

The output of the command resembles the following example:

`pod/mypod created`

You now have a running pod with your Azure Disk mounted in the

`/mnt/azure`

directory. Check the pod configuration using thecommand.`kubectl describe`

`kubectl describe pod mypod`

The output of the command resembles the following example:

`[...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: azure-managed-disk ReadOnly: false default-token-smm2n: Type: Secret (a volume populated by a Secret) SecretName: default-token-smm2n Optional: false [...] Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Scheduled 2m default-scheduler Successfully assigned mypod to aks-nodepool1-79590246-0 Normal SuccessfulMountVolume 2m kubelet, aks-nodepool1-79590246-0 MountVolume.SetUp succeeded for volume "default-token-smm2n" Normal SuccessfulMountVolume 1m kubelet, aks-nodepool1-79590246-0 MountVolume.SetUp succeeded for volume "pvc-faf0f176-8b8d-11e8-923b-deb28c58d242" [...]`


## Dynamic storage class parameters for PVCs

The following table includes parameters you can use to define a custom storage class for your PVCs.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| skuName | Azure Disks storage account type (alias: `storageAccountType` ) |
`Standard_LRS` , `Premium_LRS` , `StandardSSD_LRS` , `PremiumV2_LRS` , `UltraSSD_LRS` , `Premium_ZRS` , `StandardSSD_ZRS` |
No | `StandardSSD_LRS` |
| fsType | File System Type | `ext4` , `ext3` , `ext2` , `xfs` , `btrfs` for Linux, `ntfs` for Windows |
No | `ext4` for Linux, `ntfs` for Windows |
| cachingMode | [Azure Data Disk Host Cache Setting][disk-host-cache-setting](PremiumV2_LRS and UltraSSD_LRS only support `None` caching mode) |
`None` , `ReadOnly` , `ReadWrite` |
No | `ReadOnly` |
| resourceGroup | Specify the resource group for the Azure Disks | Existing resource group name | No | If empty, driver uses the same resource group name as current AKS cluster |
| DiskIOPSReadWrite | [UltraSSD disk][ultra-ssd-disks] or [Premium SSD v2][premiumv2_lrs_disks] IOPS Capability (minimum: 2 IOPS/GiB) | 100~160000 | No | `500` |
| DiskMBpsReadWrite | [UltraSSD disk][ultra-ssd-disks] or [Premium SSD v2][premiumv2_lrs_disks] Throughput Capability(minimum: 0.032/GiB) | 1~2000 | No | `100` |
| LogicalSectorSize | Logical sector size in bytes for ultra disk. Supported values are 512 ad 4096. 4096 is the default. | `512` , `4096` |
No | `4096` |
| tags | Azure Disk [tags][azure-tags] | Tag format: `key1=val1,key2=val2` |
No | "" |
| diskEncryptionSetID | ResourceId of the disk encryption set to use for [enabling encryption at rest][disk-encryption] | format: `/subscriptions/{subs-id}/resourceGroups/{rg-name}/providers/Microsoft.Compute/diskEncryptionSets/{diskEncryptionSet-name}` |
No | "" |
| diskEncryptionType | Encryption type of the disk encryption set. | `EncryptionAtRestWithCustomerKey` (by default), `EncryptionAtRestWithPlatformAndCustomerKeys` |
No | "" |
| writeAcceleratorEnabled | [Write Accelerator on Azure Disks][azure-disk-write-accelerator] | `true` , `false` |
No | "" |
| networkAccessPolicy | NetworkAccessPolicy property to prevent generation of the SAS URI for a disk or a snapshot | `AllowAll` , `DenyAll` , `AllowPrivate` |
No | `AllowAll` |
| diskAccessID | Azure Resource ID of the DiskAccess resource to use private endpoints on disks | No | `` | |
| enableBursting | [Enable on-demand bursting][on-demand-bursting] beyond the provisioned performance target of the disk. On-demand bursting should only be applied to Premium disk and when the disk size > 512 GB. Ultra and shared disk isn't supported. Bursting is disabled by default. | `true` , `false` |
No | `false` |
| userAgent | The user agent is used for [customer usage attribution][customer-usage-attribution] | No | The generated user agent is formatted as `driverName/driverVersion compiler/version (OS-ARCH)` |
|
| subscriptionID | Specify Azure subscription ID where the Azure Disks is created. | Azure subscription ID | No | If not empty, `resourceGroup` must be provided. |

## Static provisioning parameters for a PV

The following table includes parameters you can use to define a PV.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| volumeHandle | Azure disk URI | `/subscriptions/{sub-id}/resourcegroups/{group-name}/providers/microsoft.compute/disks/{disk-id}` |
Yes | N/A |
| volumeAttributes.fsType | File system type | `ext4` , `ext3` , `ext2` , `xfs` , `btrfs` for Linux, `ntfs` for Windows |
No | `ext4` for Linux, `ntfs` for Windows |
| volumeAttributes.partition | Partition number of the existing disk (only supported on Linux) | `1` , `2` , `3` |
No | Empty (no partition) - Make sure partition format is like `-part1` |
| volumeAttributes.cachingMode | [Disk host cache setting][disk-host-cache-setting] | `None` , `ReadOnly` , `ReadWrite` |
No | `ReadOnly` |

## Create an Azure Disk custom storage class

The default storage classes are suitable for most common scenarios. For some cases, you might want
to have your own storage class customized with your own parameters. For example, you might want to
change the `volumeBindingMode`

class.

You can use a `volumeBindingMode: Immediate`

class that guarantees it occurs immediately once the
persistent volume claim (PVC) is created. When your node pools are topology constrained, for example
when using availability zones, PVs would be bound or provisioned without knowledge of the pod's
scheduling requirements.

To address this scenario, you can use `volumeBindingMode: WaitForFirstConsumer`

, which delays the binding and provisioning of a PV until a pod that uses the PVC is created. This approach ensures that the persistent volume (PV) is provisioned in the same availability zone or topology as required per the pod's scheduling constraints. The default storage classes use `volumeBindingMode: WaitForFirstConsumer`

class.

Create a file named

`sc-azuredisk-csi-waitforfirstconsumer.yaml`

, and then paste the following manifest. The storage class is the same as our`managed-csi`

storage class, but with a different`volumeBindingMode`

class. For example:`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: azuredisk-csi-waitforfirstconsumer provisioner: disk.csi.azure.com parameters: skuname: StandardSSD_LRS allowVolumeExpansion: true reclaimPolicy: Delete volumeBindingMode: WaitForFirstConsumer`

Create the storage class by running the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify your`sc-azuredisk-csi-waitforfirstconsumer.yaml`

file:`kubectl apply -f sc-azuredisk-csi-waitforfirstconsumer.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/azuredisk-csi-waitforfirstconsumer created`


## Learn about volume snapshots

The Azure Disk CSI driver supports [volume snapshots](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html), enabling you to capture the state of persistent volumes at specific points in time for backup and restore operations. Volume snapshots let you create point-in-time copies of your persistent data without interrupting running applications. You can use these snapshots to create new volumes or restore existing ones to a previous state.

You can create two types of snapshots:

**Full snapshots**: Capture the complete state of the disk.**Incremental snapshots**: Capture only the changes since the last snapshot, offering better storage efficiency and cost savings.[Incremental snapshots](/en-us/azure/virtual-machines/disks-incremental-snapshots)are the default behavior when the`incremental`

parameter is set to`true`

in your VolumeSnapshotClass.

The following table provides details for these parameters.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| resourceGroup | Resource group for storing snapshot shots | EXISTING RESOURCE GROUP | No | If not specified, snapshots are stored in the same resource group as source Azure Disks |
| incremental | Take
|

`true`

, `false`

`true`

[tags](/en-us/azure/azure-resource-manager/management/tag-resources)[customer usage attribution](/en-us/azure/marketplace/azure-partner-customer-usage-attribution)`driverName/driverVersion compiler/version (OS-ARCH)`

`resourceGroup`

must be provided, `incremental`

must set as `false`

Volume snapshots support the following scenarios:

**Backup and restore**: Create point-in-time backups of stateful application data and restore when needed.**Data cloning**: Clone existing volumes to create new persistent volumes with the same data.**Disaster recovery**: Quickly recover from data loss or corruption.

### Create a volume snapshot

Note

Before proceeding, ensure that the application isn't writing data to the source disk.

For an example of this capability, create a

[volume snapshot class](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/storageclass-azuredisk-snapshot.yaml)with the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/storageclass-azuredisk-snapshot.yaml`

The output of the command resembles the following example:

`volumesnapshotclass.snapshot.storage.k8s.io/csi-azuredisk-vsc created`

Create a

[volume snapshot](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/azuredisk-volume-snapshot.yaml)from the PVC that was created earlier in this article.`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/azuredisk-volume-snapshot.yaml`

The output of the command resembles the following example:

`volumesnapshot.snapshot.storage.k8s.io/azuredisk-volume-snapshot created`

To verify that the snapshot was created correctly, run the following command:

`kubectl describe volumesnapshot azuredisk-volume-snapshot`

The output of the command resembles the following example:

`Name: azuredisk-volume-snapshot Namespace: default Labels: <none> Annotations: API Version: snapshot.storage.k8s.io/v1 Kind: VolumeSnapshot Metadata: Creation Timestamp: 2020-08-27T05:27:58Z Finalizers: snapshot.storage.kubernetes.io/volumesnapshot-as-source-protection snapshot.storage.kubernetes.io/volumesnapshot-bound-protection Generation: 1 Resource Version: 714582 Self Link: /apis/snapshot.storage.k8s.io/v1/namespaces/default/volumesnapshots/azuredisk-volume-snapshot UID: dd953ab5-6c24-42d4-ad4a-f33180e0ef87 Spec: Source: Persistent Volume Claim Name: pvc-azuredisk Volume Snapshot Class Name: csi-azuredisk-vsc Status: Bound Volume Snapshot Content Name: snapcontent-dd953ab5-6c24-42d4-ad4a-f33180e0ef87 Creation Time: 2020-08-31T05:27:59Z Ready To Use: true Restore Size: 10Gi Events: <none>`


### Create a new PVC based on a volume snapshot

You can create a new PVC based on a volume snapshot.

Use the snapshot created in the previous step, and create a

[new PVC](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/pvc-azuredisk-snapshot-restored.yaml)and a[new pod](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/nginx-pod-restored-snapshot.yaml)to consume it:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/pvc-azuredisk-snapshot-restored.yaml kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/nginx-pod-restored-snapshot.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk-snapshot-restored created pod/nginx-restored created`

To make sure it's the same PVC created before, check the contents by running the following command:

`kubectl exec nginx-restored -- ls /mnt/azuredisk`

The output of the command resembles the following example:

`lost+found outfile test.txt`


We can still see our previously created `test.txt`

file as expected.

## Clone volumes

A cloned volume is defined as a duplicate of an existing Kubernetes volume. For more information on cloning volumes in Kubernetes, see [volume cloning](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#volume-cloning).

Create a

[cloned volume](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml)of the[previously created](#create-azure-disk-pvs-using-built-in-storage-classes)`azuredisk-pvc`

and a[new pod](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml)to consume it.`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/cloning/pvc-azuredisk-cloning.yaml kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk-cloning created pod/nginx-restored-cloning created`

You can verify the content of the cloned volume by running the following command and confirming the file

`test.txt`

is created:`kubectl exec nginx-restored-cloning -- ls /mnt/azuredisk`

The output of the command resembles the following example:

`lost+found outfile test.txt`


## Resize an Azure Disk PV without downtime

You can request a larger volume for a PVC. Edit the PVC object, and specify a larger size. This change triggers the expansion of the underlying volume that backs the PV.

Note

A new PV is never created to satisfy the claim. Instead, an existing volume is resized.

In AKS, the built-in `managed-csi`

storage class already supports expansion, so use the [previously created](#create-azure-disk-pvs-using-built-in-storage-classes) one. The PVC requested a 10-Gi persistent volume. You can confirm by running the following command:

```
kubectl exec -it nginx-azuredisk -- df -h /mnt/azuredisk
```


The output of the command resembles the following example:

```
Filesystem Size Used Avail Use% Mounted on
/dev/sdc 9.8G 42M 9.8G 1% /mnt/azuredisk
```


Expand the PVC by increasing the

`spec.resources.requests.storage`

field running the following command:`kubectl patch pvc pvc-azuredisk --type merge --patch '{"spec": {"resources": {"requests": {"storage": "15Gi"}}}}'`

Note

Shrinking PVs is currently not supported. Trying to patch an existing PVC with a smaller size than the current one leads to the following error message:

`The persistentVolumeClaim "pvc-azuredisk" is invalid: spec.resources.requests.storage: Forbidden: field can not be less than previous value.`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk patched`

Run the following command to confirm the volume size increased:

`kubectl get pv`

The output of the command resembles the following example:

`NAME CAPACITY ACCESS MODES RECLAIM POLICY STATUS CLAIM STORAGECLASS REASON AGE pvc-391ea1a6-0191-4022-b915-c8dc4216174a 15Gi RWO Delete Bound default/pvc-azuredisk managed-csi 2d2h (...)`

And after a few minutes, run the following commands to confirm the size of the PVC:

`kubectl get pvc pvc-azuredisk`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE pvc-azuredisk Bound pvc-391ea1a6-0191-4022-b915-c8dc4216174a 15Gi RWO managed-csi 2d2h`

Run the following command to confirm the size of the disk inside the pod:

`kubectl exec -it nginx-azuredisk -- df -h /mnt/azuredisk`

The output of the command resembles the following example:

`Filesystem Size Used Avail Use% Mounted on /dev/sdc 15G 46M 15G 1% /mnt/azuredisk`


If your pod has *multiple containers*, you can specify which container by running the following command:

```
kubectl exec -it nginx-azuredisk -c <ContainerName> -- df -h /mnt/azuredisk
```


## Windows containers

The Azure Disk CSI driver supports Windows nodes and containers. If you want to use Windows containers, follow the [Windows containers quickstart](learn/quick-kubernetes-deploy-cli) to add a Windows node pool.

After you have a Windows node pool, you can now use the built-in storage classes like

`managed-csi`

. You can deploy an example[Windows-based stateful set](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/windows/statefulset.yaml)that saves timestamps into the file`data.txt`

by running the following[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/windows/statefulset.yaml`

The output of the command resembles the following example:

`statefulset.apps/busybox-azuredisk created`

To validate the content of the volume, run the following command:

`kubectl exec -it statefulset-azuredisk-win-0 -- powershell -c "type c:/mnt/azuredisk/data.txt"`

The output of the command resembles the following example:

`2020-08-27 08:13:41Z 2020-08-27 08:13:42Z 2020-08-27 08:13:44Z (...)`


## On-demand bursting

On-demand disk bursting model allows disk bursts whenever its needs exceed its current capacity. This model generates extra charges anytime the disk bursts. On-demand bursting is only available for premium SSDs larger than 512 GiB. For more information on premium SSDs provisioned IOPS and throughput per disk, see [Premium SSD size](/en-us/azure/virtual-machines/disks-types#premium-ssds). Alternatively, credit-based bursting is where the disk will burst only if it has burst credits accumulated in its credit bucket. Credit-based bursting doesn't generate extra charges when the disk bursts. Credit-based bursting is only available for premium SSDs 512 GiB and smaller, and standard SSDs 1,024 GiB and smaller. For more information on on-demand bursting, see [On-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting).

Important

The default `managed-csi-premium`

storage class has on-demand bursting disabled and uses credit-based bursting. Any premium SSD dynamically created by a persistent volume claim based on the default `managed-csi-premium`

storage class also has on-demand bursting disabled.

To create a premium SSD persistent volume with [on-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting) enabled, you can create a new storage class with the [enableBursting](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/docs/driver-parameters.md) parameter set to `true`

as shown in the following YAML template. For more information on enabling on-demand bursting, see [On-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting). For more information on building your own storage class with on-demand bursting enabled, see [Create a Burstable Managed CSI Premium Storage Class](https://github.com/Azure-Samples/burstable-managed-csi-premium).

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: burstable-managed-csi-premium
provisioner: disk.csi.azure.com
parameters:
skuname: Premium_LRS
enableBursting: "true"
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```


## Clean up resources

When you're done with the resources created in this article, you can remove them using the
`kubectl delete`

command.

```
# Remove the pod
kubectl delete -f azure-pvc-disk.yaml
# Remove the persistent volume claim
kubectl delete -f azure-pvc.yaml
```


## Provision Azure Files PVs

Azure Files supports Azure Premium file shares. The minimum file share capacity is 100 GiB. We recommend using Azure Premium file shares instead of Standard file shares because Premium file shares offer higher performance, low-latency disk support for I/O-intensive workloads. With Azure Files shares, there's no limit as to how many can be mounted on a node. For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

When you use storage CSI drivers on AKS, there are two more built-in `StorageClasses`

that uses the Azure Files CSI storage drivers. The other CSI storage classes are created with the cluster alongside the in-tree default storage classes.

`azurefile-csi`

: Uses Azure Standard Storage to create an Azure file share.`azurefile-csi-premium`

: Uses Azure Premium Storage to create an Azure file share.

The reclaim policy on both storage classes ensures that the underlying Azure files share is deleted when the respective PV is deleted. Since the storage classes also configure the file shares to be expandable, you just need to edit the [PVC](concepts-storage#persistent-volume-claims) with the new size.

Note

To have the best experience with Azure Files, follow these best practices. The location to configure mount options (`mountOptions`

) depends on whether you're provisioning dynamic or static persistent volumes.

- If you're dynamically provisioning a volume with a storage class, specify the mount options on the storage class object (kind:
`StorageClass`

). - If you're statically provisioning a volume, specify the mount options on the PersistentVolume object (kind:
`PersistentVolume`

). - If you're mounting the file share as an inline volume, specify the mount options on the Pod object (kind:
`Pod`

).

We recommend FIO when running benchmarking tests. For more information, see [benchmarking tools and tests](/en-us/azure/storage/files/nfs-performance#benchmarking-tools-and-tests).

A storage class is used to define how an Azure file share is created. A storage account is automatically created in the [node resource group](faq) for use with the storage class to hold the Azure files share. Choose one of the following [Azure storage redundancy SKUs](/en-us/azure/storage/common/storage-redundancy) for *skuName*:

Note

Modifying any resource under the node resource group in an AKS cluster is an unsupported action and will cause cluster operation failures. For more information, see [Why are two resource groups created with AKS?](faq)

**Standard_LRS**: Standard locally redundant storage**Standard_GRS**: Standard geo-redundant storage**Standard_ZRS**: Standard zone-redundant storage**Standard_RAGRS**: Standard read-access geo-redundant storage**Standard_RAGZRS**: Standard read-access geo-zone-redundant storage**Premium_LRS**: Premium locally redundant storage**Premium_ZRS**: Premium zone-redundant storage

For more information on Kubernetes storage classes for Azure Files, see [Kubernetes Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/#azure-file).

Create a file named

`azure-file-sc.yaml`

and copy in the following example manifest. For more information on`mountOptions`

, see the[Mount options](#mount-options)section.`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: my-azurefile provisioner: file.csi.azure.com # replace with "kubernetes.io/azure-file" if aks version is less than 1.21 allowVolumeExpansion: true mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict - actimeo=30 - nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks parameters: skuName: Premium_LRS`

Create the storage class using the

command.`kubectl apply`

`kubectl apply -f azure-file-sc.yaml`


### Create a PVC

A PVC uses the storage class object to dynamically provision an Azure file share. You can use the following YAML to create a PVC that's *100 GB* in size with *ReadWriteMany* access. For more information on access modes, see [Kubernetes persistent volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes).

Create a file named

`azure-file-pvc.yaml`

and copy in the following YAML. Make sure the`storageClassName`

matches the storage class you created in the previous step.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: my-azurefile spec: accessModes: - ReadWriteMany storageClassName: my-azurefile resources: requests: storage: 100Gi`

Note

If using the

`Premium_LRS`

SKU for your storage class, the minimum value for`storage`

must be`100Gi`

.Create the PVC using the

command.`kubectl apply`

`kubectl apply -f azure-file-pvc.yaml`

Once completed, the file share is created. A Kubernetes secret is also created that includes connection information and credentials. You can use the

command to view the status of the PVC:`kubectl get`

`kubectl get pvc my-azurefile`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE my-azurefile Bound pvc-8436e62e-a0d9-11e5-8521-5a8664dc0477 100Gi RWX my-azurefile 5m`


### Mount the PVC

The following YAML creates a pod that uses the PVC *my-azurefile* to mount the Azure Files file share at the */mnt/azure* path. For Windows Server containers, specify a `mountPath`

using the Windows path convention, such as *"D:"*.

Create a file named

`azure-pvc-files.yaml`

, and copy in the following YAML. Make sure the`claimName`

matches the PVC you created in the previous step.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: /mnt/azure name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: my-azurefile`

Create the pod using the

command.`kubectl apply`

`kubectl apply -f azure-pvc-files.yaml`

You now have a running pod with your Azure Files file share mounted in the

*/mnt/azure*directory. This configuration can be seen when inspecting your pod using thecommand. The following condensed example output shows the volume mounted in the container.`kubectl describe`

`Containers: mypod: Container ID: docker://053bc9c0df72232d755aa040bfba8b533fa696b123876108dec400e364d2523e Image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine Image ID: docker-pullable://nginx@sha256:d85914d547a6c92faa39ce7058bd7529baacab7e0cd4255442b04577c4d1f424 State: Running Started: Fri, 01 Mar 2019 23:56:16 +0000 Ready: True Mounts: /mnt/azure from volume (rw) /var/run/secrets/kubernetes.io/serviceaccount from default-token-8rv4z (ro) [...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: my-azurefile ReadOnly: false [...]`


### Mount options

For Kubernetes versions 1.13.0 and later, the default values for `fileMode`

and `dirMode`

are `0777`

. When dynamically provisioning PVs using a storage class, you can define mount options directly in the storage class manifest. For details, see [Mount options](https://kubernetes.io/docs/concepts/storage/storage-classes/#mount-options). The following example demonstrates setting these permissions to `0777`

:

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: my-azurefile
provisioner: file.csi.azure.com # replace with "kubernetes.io/azure-file" if aks version is less than 1.21
allowVolumeExpansion: true
mountOptions:
- dir_mode=0777
- file_mode=0777
- uid=0
- gid=0
- mfsymlinks
- cache=strict
- actimeo=30
- nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks
parameters:
skuName: Premium_LRS
```


## Storage class parameters for dynamic volumes

The following table includes parameters you can use to define a custom storage class for your PVC.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| accountAccessTier |
|

`Hot`

or `Cool`

, and Premium account can only choose `Premium`

.`102400`

`true`

or `false`

`false`

`true`

or `false`

`false`

`true`

or `false`

`false`

`eastus`

.`true`

or `false`

`false`

1`privateEndpoint`

is specified, a private endpoint is created for the storage account. For other cases, a service endpoint is created by default.`privateEndpoint`

`smb`

, `nfs`

`smb`

`true`

or `false`

`false`

`true`

or `false`

`false`

`accountname.privatelink.file.core.windows.net`

.`accountname.file.core.windows.net`

or other sovereign cloud account address.[Access tier for file share](/en-us/azure/storage/files/storage-files-planning#storage-tiers)`TransactionOptimized`

(default), `Hot`

, and `Cool`

. Premium storage account type for file shares only.`storageAccountType`

)`Standard_LRS`

, `Standard_ZRS`

, `Standard_GRS`

, `Standard_RAGRS`

, `Standard_RAGZRS`

,`Premium_LRS`

, `Premium_ZRS`

, `StandardV2_LRS`

, `StandardV2_ZRS`

, `StandardV2_GRS`

, `StandardV2_GZRS`

, `PremiumV2_LRS`

, `PremiumV2_ZRS`

`Standard_LRS`

Minimum file share size for Premium account type is 100 GB.

ZRS account type is supported in limited regions.

NFS file share only supports Premium account type.

Standard V2 SKU names are for

[Azure Files provisioned v2 model](/en-us/azure/storage/files/understanding-billing#provisioned-v2-model).`core.windows.net`

, `core.chinacloudapi.cn`

, etc.`core.windows.net`

.[Tags](/en-us/azure/azure-resource-manager/management/tag-resources)are created in new storage account.1 If the storage account is created by the driver, then you only need to specify
`networkEndpointType: privateEndpoint`

parameter in storage class. The CSI driver creates the
private endpoint and private DNS zone (named `privatelink.file.core.windows.net`

) together with the
account. If you bring your own storage account, then you need to
[create the private endpoint](/en-us/azure/storage/common/storage-private-endpoints) for the storage account. If you're
using Azure Files storage in a network isolated cluster, you must create a custom storage class with
"networkEndpointType: privateEndpoint". You can follow this sample for reference:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: azurefile-csi
provisioner: file.csi.azure.com
allowVolumeExpansion: true
parameters:
skuName: Premium_LRS # available values: Premium_LRS, Premium_ZRS, Standard_LRS, Standard_GRS, Standard_ZRS, Standard_RAGRS, Standard_RAGZRS
networkEndpointType: privateEndpoint
reclaimPolicy: Delete
volumeBindingMode: Immediate
mountOptions:
- dir_mode=0777 # modify this permission if you want to enhance the security
- file_mode=0777
- mfsymlinks
- cache=strict # https://linux.die.net/man/8/mount.cifs
- nosharesock # reduce probability of reconnect race
- actimeo=30 # reduce latency for metadata-heavy workload
- nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks
```


## Static provisioning parameters for PVs

The following table includes parameters you can use to define a PV.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| volumeAttributes.resourceGroup | Specify an Azure resource group name. | myResourceGroup | No | If empty, driver uses the same resource group name as current cluster. |
| volumeAttributes.storageAccount | Specify an existing Azure storage account name. | storageAccountName | Yes | |
| volumeAttributes.shareName | Specify an Azure file share name. | fileShareName | Yes | |
| volumeAttributes.folderName | Specify a folder name in Azure file share. | folderName | No | If folder name doesn't exist in file share, mount would fail. |
| volumeAttributes.protocol | Specify file share protocol. | `smb` , `nfs` |
No | `smb` |
| volumeAttributes.server | Specify Azure storage account server address | Existing server address, for example `accountname.privatelink.file.core.windows.net` . |
No | If empty, driver uses default `accountname.file.core.windows.net` or other sovereign cloud account address. |

## Create a PV snapshot class

The Azure Files CSI driver supports creating [snapshots of persistent volumes](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html) and the underlying file shares.

Create a

[volume snapshot class](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/snapshot/volumesnapshotclass-azurefile.yaml)with the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/snapshot/volumesnapshotclass-azurefile.yaml`

The output of the command resembles the following example:

`volumesnapshotclass.snapshot.storage.k8s.io/csi-azurefile-vsc created`

Create a

[volume snapshot](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/snapshot/volumesnapshot-azurefile.yaml)from the PVC created earlier (`pvc-azurefile`

).`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/snapshot/volumesnapshot-azurefile.yaml`

The output of the command resembles the following example:

`volumesnapshot.snapshot.storage.k8s.io/azurefile-volume-snapshot created`

Verify the snapshot was created correctly by running the following command:

`kubectl describe volumesnapshot azurefile-volume-snapshot`

The output of the command resembles the following example:

`Name: azurefile-volume-snapshot Namespace: default Labels: <none> Annotations: API Version: snapshot.storage.k8s.io/v1beta1 Kind: VolumeSnapshot Metadata: Creation Timestamp: 2020-08-27T22:37:41Z Finalizers: snapshot.storage.kubernetes.io/volumesnapshot-as-source-protection snapshot.storage.kubernetes.io/volumesnapshot-bound-protection Generation: 1 Resource Version: 955091 Self Link: /apis/snapshot.storage.k8s.io/v1beta1/namespaces/default/volumesnapshots/azurefile-volume-snapshot UID: c359a38f-35c1-4fb1-9da9-2c06d35ca0f4 Spec: Source: Persistent Volume Claim Name: pvc-azurefile Volume Snapshot Class Name: csi-azurefile-vsc Status: Bound Volume Snapshot Content Name: snapcontent-c359a38f-35c1-4fb1-9da9-2c06d35ca0f4 Ready To Use: false Events: <none>`


## Resize an Azure Files PV

You can request a larger volume for a PVC. Edit the PVC object, and specify a larger size. This change triggers the expansion of the underlying volume that backs the PV.

Note

A new PV is never created to satisfy the claim. Instead, an existing volume is resized. Shrinking persistent volumes is currently not supported.

In AKS, the built-in `azurefile-csi`

storage class already supports expansion, so use the PVC we created earlier with this storage class. The PVC requested a 100 GiB file share. We can confirm that by running:

```
kubectl exec -it nginx-azurefile -- df -h /mnt/azurefile
```


The output of the command resembles the following example:

```
Filesystem Size Used Avail Use% Mounted on
//f149b5a219bd34caeb07de9.file.core.windows.net/pvc-5e5d9980-da38-492b-8581-17e3cad01770 100G 128K 100G 1% /mnt/azurefile
```


Expand the PVC by increasing the

`spec.resources.requests.storage`

field:`kubectl patch pvc pvc-azurefile --type merge --patch '{"spec": {"resources": {"requests": {"storage": "200Gi"}}}}'`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azurefile patched`

Verify that both the PVC and the file system inside the pod show the new size:

`kubectl get pvc pvc-azurefile NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE pvc-azurefile Bound pvc-5e5d9980-da38-492b-8581-17e3cad01770 200Gi RWX azurefile-csi 64m kubectl exec -it nginx-azurefile -- df -h /mnt/azurefile Filesystem Size Used Avail Use% Mounted on //f149b5a219bd34caeb07de9.file.core.windows.net/pvc-5e5d9980-da38-492b-8581-17e3cad01770 200G 128K 200G 1% /mnt/azurefile`


## Use a PV with private Azure Files storage (private endpoint)

If your Azure Files resources are protected with a private endpoint, you must create your own storage class. Make sure to configure your [DNS settings to resolve the private endpoint IP address to the FQDN of the connection string](/en-us/azure/private-link/private-endpoint-dns#azure-services-dns-zone-configuration).

Customize the following parameters:

`resourceGroup`

: The resource group where the storage account is deployed.`storageAccount`

: The storage account name.`server`

: The FQDN of the storage account's private endpoint.

Create a file named

`private-azure-file-sc.yaml`

, and then paste the following example manifest in the file. Replace the values for`<resourceGroup>`

and`<storageAccountName>`

. For example:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: private-azurefile-csi provisioner: file.csi.azure.com allowVolumeExpansion: true parameters: resourceGroup: <resourceGroup> storageAccount: <storageAccountName> server: <storageAccountName>.file.core.windows.net reclaimPolicy: Delete volumeBindingMode: Immediate mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict # https://linux.die.net/man/8/mount.cifs - nosharesock # reduce probability of reconnect race - actimeo=30 # reduce latency for metadata-heavy workload`

Create the storage class by using the

`kubectl apply`

command:`kubectl apply -f private-azure-file-sc.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/private-azurefile-csi created`

Create a file named

`private-pvc.yaml`

, and then paste the following example manifest in the file:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: private-azurefile-pvc spec: accessModes: - ReadWriteMany storageClassName: private-azurefile-csi resources: requests: storage: 100Gi`

Create the PVC by using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f private-pvc.yaml`


## Use Managed Identity to access Azure Files storage (Preview)

Azure Files now supports managed identity-based authentication for SMB access. With this capability, your applications running in AKS can securely access Azure Files shares without the need to store or manage storage account keys or credentials. Managed identities provide a streamlined and secure authentication mechanism, simplifying access management and reducing the risk associated with credential exposure. You can create a dynamic volume or a static volume.

Note

Managed identity support for Azure Files in AKS is available in preview starting with AKS version 1.34 on Linux nodes.

To enable managed identity for dynamically provisioned volumes, follow these steps:

Create a storage class with managed identity enabled using a YAML file, for example,

`azurefile-csi-managed-identity.yaml`

with the following sample content. Set`mountWithManagedIdentity: "true"`

under`parameters`

:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azurefile-csi provisioner: file.csi.azure.com parameters: resourceGroup: EXISTING_RESOURCE_GROUP_NAME # optional, node resource group by default if it's not provided storageAccount: EXISTING_STORAGE_ACCOUNT_NAME # optional, a new account will be created if it's not provided mountWithManagedIdentity: "true" # optional, clientID of the managed identity, kubelet identity would be used by default if it's not provided clientID: "xxxxx-xxxx-xxx-xxx-xxxxxxx" reclaimPolicy: Delete volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - dir_mode=0777 # modify this permission if you want to enhance the security - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict # https://linux.die.net/man/8/mount.cifs - nosharesock # reduce probability of reconnect race - actimeo=30 # reduce latency for metadata-heavy workload - nobrl # disable sending byte range lock requests to the server`

Apply this storage class by running the following command:

`kubectl apply -f azurefile-csi-managed-identity.yaml`

Deploy your

**StatefulSet**or workload using the new storage class that references this PVC to ensure that the volume is provisioned using managed identity authentication. In your PVC manifest, set`storageClassName: azurefile-csi-managed-identity`

. For example:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azurefile-managed-identity-pvc spec: accessModes: - ReadWriteMany storageClassName: azurefile-csi-managed-identity resources: requests: storage: 100Gi`


## Learn about Azure Files NFS

Azure Files supports the
[NFS v4.1 protocol](/en-us/azure/storage/files/storage-files-how-to-create-nfs-shares). NFS version 4.1
support for Azure Files provides you with a fully managed NFS system as a service built on highly
available, highly durable distributed resilient storage platform.

This option is optimized for random access workloads with in-place data updates and provides full POSIX file system support. This section shows you how to use NFS shares with the Azure File CSI driver on an AKS cluster.

Note

You can use a private endpoint instead of allowing access to the selected VNet.

This section explains how to maximize performance and security when using Azure Files NFS 4.1 with AKS. Learn how to:

Optimize NFS read and write size settings

Create and configure an NFS storage class

Deploy workloads that use NFS-backed volumes

Enable Encryption in Transit (EiT) to protect data as it moves between your AKS cluster and Azure Files.


This section provides information about how to approach performance tuning NFS with the Azure Files
CSI driver with the `rsize`

(read size) and `wsize`

(write size) options. The `rsize`

and `wsize`

options set the maximum transfer size of an NFS operation. If `rsize`

or `wsize`

aren't specified on
mount, the client and server negotiate the largest size supported by the two. Currently, both Azure
Files and modern Linux distributions support read and write sizes as large as 1,048,576 bytes (1
MiB).

Optimal performance is based on efficient client-server communication. Increasing or decreasing the
**mount** read and write option size values can improve NFS performance. The default size of the
read/write packets transferred between client and server are 8 KB for NFS version 2, and 32 KB for
NFS version 3 and 4. These defaults might be too large or too small. Reducing the `rsize`

and
`wsize`

might improve NFS performance in a congested network by sending smaller packets for each
NFS-read reply and write request. However, this reduction can increase the number of packets needed
to send data across the network, increasing total network traffic and CPU utilization on the client
and server.

It's important that you perform testing to find an `rsize`

and `wsize`

that sustains efficient
packet transfer, where it doesn't decrease throughput and increase latency.

For example, to configure a maximum `rsize`

and `wsize`

of 256-KiB, configure the `mountOptions`

in
the storage class as follows:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: azurefile-csi-nfs
provisioner: file.csi.azure.com
allowVolumeExpansion: true
parameters:
protocol: nfs
mountOptions:
- nconnect=4
- noresvport
- actimeo=30
- rsize=262144
- wsize=262144
```


## Other storage class examples

## Windows containers

The Azure Files CSI driver also supports Windows nodes and containers. To use Windows containers, follow the [Windows containers quickstart](learn/quick-windows-container-deploy-cli) to add a Windows node pool.

After you have a Windows node pool, use the built-in storage classes like

`azurefile-csi`

or create a custom one. You can deploy an example[Windows-based stateful set](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/windows/statefulset.yaml)that saves timestamps into a file`data.txt`

by running the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/windows/statefulset.yaml`

The output of the command resembles the following example:

`statefulset.apps/busybox-azurefile created`

Validate the contents of the volume by running the following

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command:`kubectl exec -it busybox-azurefile-0 -- cat c:\\mnt\\azurefile\\data.txt # on Linux or MacOS Bash kubectl exec -it busybox-azurefile-0 -- cat c:\mnt\azurefile\data.txt # on Windows Powershell or CMD`

The output of the commands resembles the following example:

`2020-08-27 22:11:01Z 2020-08-27 22:11:02Z 2020-08-27 22:11:04Z (...)`


## Next steps

- For Azure Files CSI driver parameters, see
[CSI driver parameters](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/docs/driver-parameters.md#static-provisionbring-your-own-file-share). - For more information about disk-based storage solutions, see
[Disk-based solutions in AKS](/en-us/azure/cloud-adoption-framework/scenarios/app-platform/aks/storage#disk-based-solutions). - For more information about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service](operator-best-practices-storage). - For more information about Azure ultra disk, see [Use ultra disks on Azure Kubernetes Service (AKS)][use-ultra-disks].
- For more information about Azure tags, see
[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-files-csi -->

# Azure storage CSI driver and volume provisioning

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Blob storage Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant driver used by Azure Kubernetes Service (AKS) to
manage the lifecycle of Azure Blob storage. The CSI is a standard for exposing arbitrary block and
file storage systems to containerized workloads on Kubernetes.

By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids having to touch the core Kubernetes code and wait for its release cycles.

When you mount Azure Blob storage as a file system into a container or pod, it enables you to use blob storage with many applications that work massive amounts of unstructured data. For example:

- Log file data
- Images, documents, and streaming video or audio
- Disaster recovery data

Applications access data stored in Azure Blob storage using either BlobFuse or the Network File System (NFS) 3.0 protocol. Before the introduction of the Azure Blob storage CSI driver, the only option was to manually install an unsupported driver to access Blob storage from your application running on AKS. When the Azure Blob storage CSI driver is enabled on AKS, there are two built-in storage classes:

- azureblob-fuse-premium
- azureblob-nfs-premium

To create an AKS cluster with CSI drivers support, see [CSI drivers on AKS](csi-storage-drivers). To
learn more about the differences in access between each of the Azure storage types using the NFS
protocol, see
[Compare access to Azure Files, Blob Storage, and Azure NetApp Files with NFS](/en-us/azure/storage/common/nfs-comparison).

The Azure Disks Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant
driver used by Azure Kubernetes Service (AKS) to manage the lifecycle of Azure Disk.

The CSI is a standard for exposing arbitrary block and file storage systems to containerized
workloads on Kubernetes. By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins
to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids
having to touch the core Kubernetes code and wait for its release cycles. To create an AKS cluster
with CSI driver support, see [Enable CSI driver on AKS](csi-storage-drivers).

For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

Note

*In-tree drivers* refer to the current storage drivers that are part of the core Kubernetes code versus the new CSI drivers, which are plug-ins.

The Azure Files Container Storage Interface (CSI) driver is a
[CSI specification](https://github.com/container-storage-interface/spec/blob/master/spec.md)-compliant driver used by Azure Kubernetes Service (AKS) to
manage the lifecycle of Azure file shares. The CSI is a standard for exposing arbitrary block and
file storage systems to containerized workloads on Kubernetes.

By adopting and using CSI, AKS now can write, deploy, and iterate plug-ins to expose new or improve existing storage systems in Kubernetes. Using CSI drivers in AKS avoids having to touch the core Kubernetes code and wait for its release cycles.

To create an AKS cluster with CSI drivers support, see [Enable CSI drivers on AKS](csi-storage-drivers).

Note

*In-tree drivers* refer to the current storage drivers that are part of the core Kubernetes code versus the new CSI drivers, which are plug-ins.

## Azure CSI driver features

Azure Blob storage CSI driver supports the following features:

- BlobFuse
- NFS 3.0 protocol

In addition to in-tree driver features, Azure Disk CSI driver supports the following features:

Performance improvements during concurrent disk attach and detach

- In-tree drivers attach or detach disks in serial, while CSI drivers attach or detach disks in batch. There's significant improvement when there are multiple disks attaching to one node.

Premium SSD v1 and v2 are supported.

`PremiumV2_LRS`

only supports`None`

caching mode

Zone-redundant storage (ZRS) disk support

`Premium_ZRS`

,`StandardSSD_ZRS`

disk types are supported. ZRS disk could be scheduled on the zone or non-zone node, without the restriction that disk volume should be colocated in the same zone as a given node. For more information, including which regions are supported, see[Zone-redundant storage for managed disks](/en-us/azure/virtual-machines/disks-redundancy).


Note

Depending on the VM SKU that's being used, the Azure Disk CSI driver might have a per-node volume limit. For some powerful VMs (for example, 16 cores), the limit is 64 volumes per node. To identify the limit per VM SKU, review the **Max data disks** column for each VM SKU offered. For a list of VM SKUs offered and their corresponding detailed capacity limits, see [General purpose virtual machine sizes](/en-us/azure/virtual-machines/sizes-general).

## Prerequisites

You must have the Azure CLI version 2.42 or later installed and configured. To find the version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you installed the Azure CLI`aks-preview`

extension, make sure that you update the extension to the latest version by calling`az extension update --name aks-preview`

.Perform the following steps to

[clean up the open source driver](https://github.com/kubernetes-sigs/blob-csi-driver/blob/master/docs/install-csi-driver-master.md#clean-up-blob-csi-driver)if you previously installed the[CSI Blob Storage open-source driver](https://github.com/kubernetes-sigs/blob-csi-driver)to access Azure Blob storage from your cluster.Your AKS cluster

*Control plane*identity (your AKS cluster name) is added to the[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)role on the VNet and network security group.To support an [Azure Data Lake Storage Gen2 account][azure-datalake-storage-account] (ADLS) when using BlobFuse mount, perform the following actions:

- To create an ADLS account using the driver in dynamic provisioning, specify
`isHnsEnabled: "true"`

in the storage class parameters. - To enable BlobFuse access to an ADLS account in static provisioning, specify the mount option
`--use-adls=true`

in the persistent volume. - If you're going to enable a storage account with Hierarchical Namespace, existing persistent volumes (PVs) should be remounted with
`--use-adls=true`

mount option.

- To create an ADLS account using the driver in dynamic provisioning, specify
By default, the BlobFuse cache is located in the

`/mnt`

directory. If the virtual machine (VM) SKU provides a temporary disk, the`/mnt`

directory is mounted on the temporary disk. However, if the VM SKU doesn't provide a temporary disk, the`/mnt`

directory is mounted on the OS disk, you could set`--tmp-path=`

mount option to specify a different cache directory.

Note

If the **blobfuse-proxy** isn't enabled during the installation of the open source driver, the uninstallation of the open source driver disrupts existing blobfuse mounts. However, NFS mounts remain unaffected.

You must have an AKS cluster with the Azure Disk CSI driver enabled. The CSI driver is enabled by default on AKS clusters running Kubernetes version 1.21 or later.

Azure CLI version 2.37.0 or later is installed and configured. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`kubectl`

command-line tool is installed and configured to connect to your AKS cluster.A storage class configured to use the Azure Disk CSI driver (

`disk.csi.azure.com`

).The Azure Disk CSI driver has a per-node volume limit. The volume count changes based on the size of the node/node pool. Run the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command to determine the number of volumes that can be allocated per node:`kubectl get CSINode <nodename> -o yaml`

If the per-node volume limit is an issue for your workload, consider using

[Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction)for persistent volumes instead of CSI drivers.

**General requirements:**

You must have an AKS cluster with the Azure Files CSI driver enabled. The Azure Files CSI driver is enabled by default on AKS clusters running Kubernetes version 1.21 or later.

Azure CLI version 2.37.0 or later is installed and configured. To check your version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).The

`kubectl`

command-line tool is installed and configured to connect to your AKS cluster.A storage class configured to use the Azure Files CSI driver (

`file.csi.azure.com`

).When choosing between standard and premium file shares, it's important you understand the provisioning model and requirements of the expected usage pattern you plan to run on Azure Files. For more information, see

[Choosing an Azure Files performance tier based on usage patterns](/en-us/azure/storage/files/understand-performance#choosing-a-performance-tier-based-on-usage-patterns).

**Network File Share (NFS) requirements:**

Your AKS cluster

*Control plane*identity (your AKS cluster name) is added to the[Contributor](/en-us/azure/role-based-access-control/built-in-roles#contributor)role on the VNet and**NetworkSecurityGroup**.Your AKS cluster's service principal or managed service identity (MSI) must be added to the

**Contributor**role to the storage account.

**Managed Identity requirements:**

Ensure the

[user-assigned Kubelet identity](use-managed-identity#create-a-kubelet-managed-identity)is granted the`Storage File Data SMB MI Admin`

role on the storage account. If you use your own storage account, you need to assign`Storage File Data SMB MI Admin`

role to the user-assigned Kubelet identity on that storage account.If the CSI driver creates the storage account, grant the

`Storage File Data SMB MI Admin`

role to the resource group where the storage account resides.If you use the default built-in user-assigned Kubelet identity, it already has the required

`Storage File Data SMB MI Admin`

role on the managed node resource group.

Note

The Azure File CSI driver only permits the mounting of SMB file shares using key-based (NTLM v2) authentication, and therefore doesn't support the maximum security profile of Azure File share settings. On the other hand, mounting NFS file shares doesn't require key-based authentication.

## Enable CSI driver on a new or existing AKS cluster

Using the Azure CLI, you can enable the Blob storage CSI driver on a new or existing AKS cluster before you configure a persistent volume for use by pods in the cluster.

To enable the driver on a new cluster, include the

`--enable-blob-driver`

parameter with the`az aks create`

command as shown in the following example:`az aks create \ --enable-blob-driver \ --name myAKSCluster \ --resource-group myResourceGroup \ --generate-ssh-keys`

To enable the driver on an existing cluster, include the

`--enable-blob-driver`

parameter with the`az aks update`

command as shown in the following example:`az aks update --enable-blob-driver --name myAKSCluster --resource-group myResourceGroup`


You're prompted to confirm there isn't an open-source Blob CSI driver installed. After you confirm, it might take several minutes to complete this action. Once it's complete, you should see in the output the status of enabling the driver on your cluster. The following example resembles the section indicating the results of the previous command:

```
"storageProfile": {
"blobCsiDriver": {
"enabled": true
},
...
}
```


## Disable CSI driver on an existing AKS cluster

Using the Azure CLI, you can disable the Blob storage CSI driver on an existing AKS cluster after you remove the persistent volume from the cluster.

To disable the driver on an existing cluster, include the

`--disable-blob-driver`

parameter with the`az aks update`

command as shown in the following example:`az aks update --disable-blob-driver --name myAKSCluster --resource-group myResourceGroup`


## Use a persistent volume for storage

Kubernetes assigns a [persistent volume](concepts-storage#persistent-volumes) (PV) as a storage resource to one or more pods. You can provision PVs dynamically through Kubernetes or statically as an administrator.

If multiple pods need concurrent access to the same storage volume, you can use Azure Blob storage to connect by using NFS or BlobFuse. This article shows you how to dynamically create an Azure Blob storage container for use by multiple pods in an AKS cluster.

For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

This article shows you how to dynamically create a PV with Azure disk for use by a single pod in an AKS cluster.

If multiple pods need concurrent access to the same storage volume, you can use Azure Files to
connect by using the [Server Message Block (SMB)](/en-us/windows/desktop/FileIO/microsoft-smb-protocol-and-cifs-protocol-overview) or
[Network File System (NFS)](/en-us/windows-server/storage/nfs/nfs-overview). This article shows you how to dynamically create an Azure
Files share for use by multiple pods in an AKS cluster.

**Dynamically provisioned volume:** Use this approach when you want Kubernetes to automatically
create and manage storage resources. It's ideal for scenarios where you need on-demand scaling,
prefer infrastructure-as-code, and want to minimize manual configuration steps.

**Statically provisioned volume:** Choose this method if you already have an Azure Blob storage
account or container that you want to use. It provides more control over storage setup, access, and
lifecycle, and is suitable when you need to connect to existing resources or reuse storage across
multiple clusters or workloads.

This section provides guidance for cluster administrators who want to provision one or more persistent volumes that include details of Blob storage for use by a workload. A persistent volume claim (PVC) uses the storage class object to dynamically provision an Azure Blob storage container.

To provision a persistent volume using Azure Blob storage with the provided storage class, follow these steps:

Create the

`StorageClass`

manifest by saving the following YAML to a file named`blob-fuse-sc.yaml`

:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: blob-fuse provisioner: blob.csi.azure.com parameters: skuName: Premium_LRS # available values: Standard_LRS, Premium_LRS, Standard_GRS, Standard_RAGRS, Standard_ZRS, Premium_ZRS protocol: fuse2 networkEndpointType: privateEndpoint reclaimPolicy: Delete volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - -o allow_other - --file-cache-timeout-in-seconds=120 - --use-attr-cache=true - --cancel-list-on-mount-seconds=10 # prevent billing charges on mounting - -o attr_timeout=120 - -o entry_timeout=120 - -o negative_timeout=120 - --log-level=LOG_WARNING # LOG_WARNING, LOG_INFO, LOG_DEBUG - --cache-size-mb=1000 # Default will be 80% of available memory, eviction will happen beyond specified value.`

To create the storage class in your cluster, apply the

`StorageClass`

by running the following command:`kubectl apply -f blob-fuse-sc.yaml`


## Create a PVC using built-in storage class

A storage class is used to define how an Azure Blob storage container is created. A storage account is automatically created in the node resource group for use with the storage class to hold the Azure Blob storage container. Choose one of the following Azure storage redundancy SKUs for skuName:

Note

Modifying any resource under the node resource group in an AKS cluster is an unsupported action and will cause cluster operation failures. For more information, see [Why are two resource groups created with AKS?](faq)

**Standard_LRS**: Standard locally redundant storage**Premium_LRS**: Premium locally redundant storage**Standard_ZRS**: Standard zone redundant storage**Premium_ZRS**: Premium zone redundant storage**Standard_GRS**: Standard geo-redundant storage**Standard_RAGRS**: Standard read-access geo-redundant storage

When you use storage CSI drivers on AKS, there are two other built-in `StorageClasses`

that use the Azure Blob CSI storage driver.

The reclaim policy on both storage classes ensures that the underlying Azure Blob storage is deleted
when the respective PV is deleted. The storage classes also configure the container to be expandable
by default, as the `set allowVolumeExpansion`

parameter is set to **true**.

Note

Shrinking persistent volumes isn't supported.

Use the [kubectl get sc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command to see the storage classes. The following example
shows the `azureblob-fuse-premium`

and `azureblob-nfs-premium`

storage classes available within an
AKS cluster:

```
NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE
azureblob-fuse-premium blob.csi.azure.com Delete Immediate true 23h
azureblob-nfs-premium blob.csi.azure.com Delete Immediate true 23h
```


To use these storage classes, create a PVC and respective pod that references and uses them. A PVC is used to automatically allocate storage based on a storage class. You can create a PVC using one of the built-in storage classes or a custom storage class. This PVC creates an Azure Blob storage container with your specified SKU, size, and protocol. When you create a pod definition, the PVC is specified to request the desired storage.

A PVC uses the storage class object to dynamically provision an Azure Blob storage container. The following YAML can be used to create a 5 GB PVC with *ReadWriteMany* access, using the built-in storage class. For more information on access modes, see the [Kubernetes persistent volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/) documentation.

Create a file named

`blob-nfs-pvc.yaml`

and copy the following YAML:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azure-blob-storage spec: accessModes: - ReadWriteMany storageClassName: azureblob-nfs-premium resources: requests: storage: 5Gi`

Create the PVC with the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command:`kubectl create -f blob-nfs-pvc.yaml`


Once complete, the Blob storage container is created. You can use the [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)
command to view the status of the PVC:

```
kubectl get pvc azure-blob-storage
```


The output of the command resembles the following example:

```
NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE
azure-blob-storage Bound pvc-b88e36c5-c518-4d38-a5ee-337a7dda0a68 5Gi RWX azureblob-nfs-premium 92m
```


## Mount the PVC

The following YAML creates a pod that uses the PVC **azure-blob-storage** to mount the Azure Blob storage at the `/mnt/blob`

path.

Create a file named

`blob-nfs-pv`

, and copy the following YAML. Make sure that the**claimName**matches the PVC created in the previous step.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/blob" name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: azure-blob-storage`

Create the pod with the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f blob-nfs-pv.yaml`

After the pod is in the running state, run the following command to create a new file called

`test.txt`

.`kubectl exec mypod -- touch /mnt/blob/test.txt`

To validate the disk is correctly mounted, run the following command, and verify you see the

`test.txt`

file in the output:`kubectl exec mypod -- ls /mnt/blob`

The output of the command resembles the following example:

`test.txt`


## Create an Azure Blob custom storage class

The default storage classes suit the most common scenarios, but not all. In some cases, you might want to have your own storage class customized with your own parameters. In this section, we provide two examples with the first one using the NFS protocol, and the second one using BlobFuse.

In this example, the following manifest configures mounting a Blob storage container using the NFS
protocol. Use it to add the `tags`

parameter.

Create a file named

`blob-nfs-sc.yaml`

, and paste the following example manifest:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azureblob-nfs-premium provisioner: blob.csi.azure.com parameters: protocol: nfs tags: environment=Development volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - nconnect=4`

Create the storage class with the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f blob-nfs-sc.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/blob-nfs-premium created`


## Mount an NFS or BlobFuse PV

In this section, you mount the PV using the NFS protocol or BlobFuse.

Mounting Blob storage using the NFS v3 protocol doesn't authenticate using an account key. Your AKS
cluster needs to reside in the same or peered virtual network as the agent node. The only way to
secure the data in your storage account is by using a virtual network and other network security
settings. For more information on how to set up NFS access to your storage account, see
[Mount Blob Storage by using the Network File System (NFS) 3.0 protocol](/en-us/azure/storage/blobs/network-file-system-protocol-support-how-to).

The following example demonstrates how to mount a Blob storage container as a persistent volume using the NFS protocol.

Create a file named

`pv-blob-nfs.yaml`

and copy in the following YAML. Under`storageClass`

, update`resourceGroup`

,`storageAccount`

, and`containerName`

.Note

The

`volumeHandle`

value within your YAML should be a unique volumeID for every identical storage blob container in the cluster.The characters

`#`

and`/`

are reserved for internal use and can't be used.`apiVersion: v1 kind: PersistentVolume metadata: annotations: pv.kubernetes.io/provisioned-by: blob.csi.azure.com name: pv-blob spec: capacity: storage: 1Pi accessModes: - ReadWriteMany persistentVolumeReclaimPolicy: Retain # If set as "Delete" container would be removed after pvc deletion storageClassName: azureblob-nfs-premium mountOptions: - nconnect=4 csi: driver: blob.csi.azure.com # make sure volumeid is unique for every identical storage blob container in the cluster # character `#` and `/` are reserved for internal use and cannot be used in volumehandle volumeHandle: account-name_container-name volumeAttributes: resourceGroup: resourceGroupName storageAccount: storageAccountName containerName: containerName protocol: nfs`

Note

While the

[Kubernetes API](https://github.com/kubernetes/kubernetes/blob/release-1.26/pkg/apis/core/types.go#L303-L306)**capacity**attribute is mandatory, this value isn't used by the Azure Blob storage CSI driver because you can flexibly write data until you reach your storage account's capacity limit. The value of the`capacity`

attribute is used only for size matching between*PVs*and*PVCs*. We recommend using a fictitious high value. The pod sees a mounted volume with a fictitious size of 5 Petabytes.Run the following command to create the persistent volume using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command referencing the YAML file created earlier:`kubectl create -f pv-blob-nfs.yaml`

Create a

`pvc-blob-nfs.yaml`

file with a*PersistentVolumeClaim*. For example:`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: pvc-blob spec: accessModes: - ReadWriteMany resources: requests: storage: 10Gi volumeName: pv-blob storageClassName: azureblob-nfs-premium`

Run the following command to create the persistent volume claim using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command referencing the YAML file created earlier:`kubectl create -f pvc-blob-nfs.yaml`


## Create a pod

The following YAML creates a pod that uses the PV or PVC named **pvc-blob** created earlier, to mount the Azure Blob storage at the `/mnt/blob`

path.

Create a file named

`nginx-pod-blob.yaml`

, and copy in the following YAML. Make sure that the**claimName**matches the PVC created in the previous step when creating a PV for NFS or BlobFuse.`kind: Pod apiVersion: v1 metadata: name: nginx-blob spec: nodeSelector: "kubernetes.io/os": linux containers: - image: mcr.microsoft.com/oss/nginx/nginx:1.17.3-alpine name: nginx-blob volumeMounts: - name: blob01 mountPath: "/mnt/blob" readOnly: false volumes: - name: blob01 persistentVolumeClaim: claimName: pvc-blob`

Run the following command to create the pod and mount the PVC using the

[kubectl create](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#create)command:`kubectl create -f nginx-pod-blob.yaml`

Run the following command to create an interactive shell session with the pod to verify if the Blob storage is mounted:

`kubectl exec -it nginx-blob -- df -h`

The output from the command resembles the following example:

`Filesystem Size Used Avail Use% Mounted on ... blobfuse 14G 41M 13G 1% /mnt/blob ...`


## Create a StatefulSet

To ensure your workload retains its storage volume across pod restarts or replacements, use a StatefulSet. StatefulSets simplify the process of associating persistent storage with pods, so that new pods created to replace failed ones can automatically access the same storage volumes. The following examples demonstrate how to set up a StatefulSet for Blob storage using either BlobFuse or the NFS protocol.

Create a file named

`azure-blob-nfs-ss.yaml`

and copy in the following YAML.`apiVersion: apps/v1 kind: StatefulSet metadata: name: statefulset-blob-nfs labels: app: nginx spec: serviceName: statefulset-blob-nfs replicas: 1 template: metadata: labels: app: nginx spec: nodeSelector: "kubernetes.io/os": linux containers: - name: statefulset-blob-nfs image: mcr.microsoft.com/azurelinux/base/nginx:1.25 volumeMounts: - name: persistent-storage mountPath: /mnt/blob updateStrategy: type: RollingUpdate selector: matchLabels: app: nginx volumeClaimTemplates: - metadata: name: persistent-storage spec: storageClassName: azureblob-nfs-premium accessModes: ["ReadWriteMany"] resources: requests: storage: 100Gi`

Create the StatefulSet with the

`kubectl create`

command:`kubectl create -f azure-blob-nfs-ss.yaml`


### Dynamic PVC storage class parameters

The following table includes parameters you can use to define a custom storage class for your dynamic PVC.

| Name | Description | Example | Mandatory | Default value |
|---|---|---|---|---|
| skuName | Specify an Azure storage account type (alias: `storageAccountType` ). |
`Standard_LRS` , `Premium_LRS` , `Standard_GRS` , `Standard_RAGRS` |
No | `Standard_LRS` |
| location | Specify an Azure location. | `eastus` |
No | If empty, the driver uses the same location name as current cluster. |
| resourceGroup | Specify an Azure resource group name. | myResourceGroup | No | If empty, the driver uses the same resource group name as current cluster. |
| storageAccount | Specify an Azure storage account name. | storageAccountName | No | When a specific storage account name isn't provided, the driver looks for a suitable storage account that matches the account settings within the same resource group. If it fails to find a matching storage account, it creates a new one. However, if a storage account name is specified, the storage account must already exist. |
networkEndpointType 1 |
Specify network endpoint type for the storage account created by driver. If privateEndpoint is specified, a
|

`privateEndpoint`

`fuse`

, `nfs`

`fuse`

`pvc-fuse`

for BlobFuse or `pvc-nfs`

for NFS v3.`<storage-account>.blob.core.windows.net`

.`<storage-account>.blob.core.windows.net`

or other sovereign cloud storage account DNS domain name.`true`

,`false`

`false`

`core.windows.net`

`true`

,`false`

`false`

1 If the storage account is created by the driver, then you only need to specify `networkEndpointType: privateEndpoint`

parameter in storage class. The CSI driver creates the private endpoint and private DNS zone (named `privatelink.blob.core.windows.net`

) together with the account. If you bring your own storage account, then you need to [create the private endpoint](/en-us/azure/storage/common/storage-private-endpoints) for the storage account. If you're using Azure Blob storage in a network isolated cluster, you must create a custom storage class with `networkEndpointType: privateEndpoint`

.

### Static PV provisioning parameters

The following table includes parameters you can use to define your static PV.

| Name | Description | Example | Mandatory | Default value |
|---|---|---|---|---|
| volumeHandle | Specify a value the driver can use to uniquely identify the storage blob container in the cluster. | A recommended way to produce a unique value is to combine the globally unique storage account name and container name: `{account-name}_{container-name}` . The `#` and `/` characters are reserved for internal use and can't be used in a volume handle. |
Yes | |
| volumeAttributes.resourceGroup | Specify Azure resource group name. | myResourceGroup | No | If empty, driver uses the same resource group name as current cluster. |
| volumeAttributes.storageAccount | Specify an existing Azure storage account name. | storageAccountName | Yes | |
| volumeAttributes.containerName | Specify existing container name. | container | Yes | |
| volumeAttributes.protocol | Specify BlobFuse mount or NFS v3 mount. | `fuse` , `nfs` |
No | `fuse` |

## Create Azure Disk PVs using built-in storage classes

A storage class is used to define how a unit of storage is dynamically created with a PV. For more information on Kubernetes storage classes, see [Kubernetes storage classes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

When you use the Azure Disk CSI driver on AKS, there are two more built-in `StorageClasses`

that use the Azure Disk CSI storage driver. The other CSI storage classes are created with the cluster alongside the in-tree default storage classes.

`managed-csi`

: Creates managed disks using Azure Standard SSD with locally redundant storage (LRS). With Kubernetes version 1.29 for AKS clusters deployed across multiple availability zones, this storage class uses Azure Standard SSD zone-redundant storage (ZRS) to provision managed disks.`managed-csi-premium`

: Provisions managed disks using Azure Premium LRS. Beginning with Kubernetes version 1.29, for AKS clusters spanning multiple availability zones, this storage class automatically uses Azure Premium ZRS to create managed disks.

Effective starting with Kubernetes version 1.29, when you deploy Azure Kubernetes Service (AKS) clusters across multiple availability zones, AKS now utilizes zone-redundant storage (ZRS) to create managed disks within built-in storage classes.

ZRS ensures synchronous replication of your Azure managed disks across multiple Azure availability zones in your chosen region. This redundancy strategy enhances the resilience of your applications and safeguards your data against datacenter failures.

However, it's important to note that zone-redundant storage (ZRS) comes at a higher cost compared to locally redundant storage (LRS). If cost optimization is a priority, you can create a new storage class with the LRS SKU name parameter and use it in your persistent volume claim.


Reducing the size of a PVC isn't supported due to the risk of data loss. You can edit an existing storage class using the `kubectl edit sc`

command, or you can create your own custom storage class. For example, if you want to use a disk of size 4 TiB, you must create a storage class that defines `cachingmode: None`

because [disk caching isn't supported for disks 4 TiB and larger][disk-host-cache-setting]. For more information about storage classes and creating your own storage class, see [Storage options for applications in AKS](concepts-storage#storage-classes).

The reclaim policy in both storage classes ensures that the underlying Azure Disks are deleted when the respective PV is deleted. The storage classes also configure the PVs to be expandable. You just need to edit the PVC with the new size.

To use these storage classes, create a [PVC](concepts-storage#persistent-volume-claims) and respective pod that references and uses them. A PVC is used to automatically provision storage based on a storage class. A PVC can use one of the precreated storage classes or a user-defined storage class to create an Azure-managed disk for the desired SKU and size. When you create a pod definition, the PVC is specified to request the desired storage.

Note

Persistent volume claims are specified in GiB but Azure managed disks are billed based on the SKU for a specific size. These SKUs range from 32GiB for S4 or P4 disks to 32TiB for S80 or P80 disks (in preview). The throughput and IOPS performance of a Premium managed disk depends on both the SKU and the instance size of the nodes in the AKS cluster. For more information, see [Pricing and performance of managed disks](https://azure.microsoft.com/pricing/details/managed-disks/).

You can see the precreated storage classes using the [ kubectl get sc](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. The following example shows the precreated storage classes available within an AKS cluster:

```
kubectl get sc
```


The output of the command resembles the following example:

```
NAME PROVISIONER AGE
default (default) disk.csi.azure.com 1h
managed-csi disk.csi.azure.com 1h
```


A PVC automatically provisions storage based on a storage class. In this case, a PVC can use one of the precreated storage classes to create a standard or premium Azure managed disk.

Create a file named

`azure-pvc.yaml`

and copy in the following manifest. The claim requests a disk named`azure-managed-disk`

that's`5 GB`

in size with`ReadWriteOnce`

access. The*managed-csi*storage class is specified as the storage class.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azure-managed-disk spec: accessModes: - ReadWriteOnce storageClassName: managed-csi resources: requests: storage: 5Gi`

Tip

To create a disk that uses premium storage, use

`storageClassName: managed-csi-premium`

rather than*managed-csi*.Create the persistent volume claim using the

command and specify your`kubectl apply`

*azure-pvc.yaml*file.`kubectl apply -f azure-pvc.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/azure-managed-disk created`


## Apply a PVC to a pod

After you create the persistent volume claim, you must verify it has a status of `Pending`

. The `Pending`

status indicates it's ready to be used by a pod.

Verify the status of the PVC using the

`kubectl describe pvc`

command.`kubectl describe pvc azure-managed-disk`

The output of the command resembles the following condensed example:

`Name: azure-managed-disk Namespace: default StorageClass: managed-csi Status: Pending [...]`

Create a file named

`azure-pvc-disk.yaml`

and copy in the following manifest. This manifest creates a basic NGINX pod that uses the persistent volume claim named`azure-managed-disk`

to mount the Azure Disk at the path`/mnt/azure`

. For Windows Server containers, specify a`mountPath`

using the Windows path convention, such as*'D:'*.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: "/mnt/azure" name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: azure-managed-disk`

Create the pod using the

command.`kubectl apply`

`kubectl apply -f azure-pvc-disk.yaml`

The output of the command resembles the following example:

`pod/mypod created`

You now have a running pod with your Azure Disk mounted in the

`/mnt/azure`

directory. Check the pod configuration using thecommand.`kubectl describe`

`kubectl describe pod mypod`

The output of the command resembles the following example:

`[...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: azure-managed-disk ReadOnly: false default-token-smm2n: Type: Secret (a volume populated by a Secret) SecretName: default-token-smm2n Optional: false [...] Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Scheduled 2m default-scheduler Successfully assigned mypod to aks-nodepool1-79590246-0 Normal SuccessfulMountVolume 2m kubelet, aks-nodepool1-79590246-0 MountVolume.SetUp succeeded for volume "default-token-smm2n" Normal SuccessfulMountVolume 1m kubelet, aks-nodepool1-79590246-0 MountVolume.SetUp succeeded for volume "pvc-faf0f176-8b8d-11e8-923b-deb28c58d242" [...]`


## Dynamic storage class parameters for PVCs

The following table includes parameters you can use to define a custom storage class for your PVCs.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| skuName | Azure Disks storage account type (alias: `storageAccountType` ) |
`Standard_LRS` , `Premium_LRS` , `StandardSSD_LRS` , `PremiumV2_LRS` , `UltraSSD_LRS` , `Premium_ZRS` , `StandardSSD_ZRS` |
No | `StandardSSD_LRS` |
| fsType | File System Type | `ext4` , `ext3` , `ext2` , `xfs` , `btrfs` for Linux, `ntfs` for Windows |
No | `ext4` for Linux, `ntfs` for Windows |
| cachingMode | [Azure Data Disk Host Cache Setting][disk-host-cache-setting](PremiumV2_LRS and UltraSSD_LRS only support `None` caching mode) |
`None` , `ReadOnly` , `ReadWrite` |
No | `ReadOnly` |
| resourceGroup | Specify the resource group for the Azure Disks | Existing resource group name | No | If empty, driver uses the same resource group name as current AKS cluster |
| DiskIOPSReadWrite | [UltraSSD disk][ultra-ssd-disks] or [Premium SSD v2][premiumv2_lrs_disks] IOPS Capability (minimum: 2 IOPS/GiB) | 100~160000 | No | `500` |
| DiskMBpsReadWrite | [UltraSSD disk][ultra-ssd-disks] or [Premium SSD v2][premiumv2_lrs_disks] Throughput Capability(minimum: 0.032/GiB) | 1~2000 | No | `100` |
| LogicalSectorSize | Logical sector size in bytes for ultra disk. Supported values are 512 ad 4096. 4096 is the default. | `512` , `4096` |
No | `4096` |
| tags | Azure Disk [tags][azure-tags] | Tag format: `key1=val1,key2=val2` |
No | "" |
| diskEncryptionSetID | ResourceId of the disk encryption set to use for [enabling encryption at rest][disk-encryption] | format: `/subscriptions/{subs-id}/resourceGroups/{rg-name}/providers/Microsoft.Compute/diskEncryptionSets/{diskEncryptionSet-name}` |
No | "" |
| diskEncryptionType | Encryption type of the disk encryption set. | `EncryptionAtRestWithCustomerKey` (by default), `EncryptionAtRestWithPlatformAndCustomerKeys` |
No | "" |
| writeAcceleratorEnabled | [Write Accelerator on Azure Disks][azure-disk-write-accelerator] | `true` , `false` |
No | "" |
| networkAccessPolicy | NetworkAccessPolicy property to prevent generation of the SAS URI for a disk or a snapshot | `AllowAll` , `DenyAll` , `AllowPrivate` |
No | `AllowAll` |
| diskAccessID | Azure Resource ID of the DiskAccess resource to use private endpoints on disks | No | `` | |
| enableBursting | [Enable on-demand bursting][on-demand-bursting] beyond the provisioned performance target of the disk. On-demand bursting should only be applied to Premium disk and when the disk size > 512 GB. Ultra and shared disk isn't supported. Bursting is disabled by default. | `true` , `false` |
No | `false` |
| userAgent | The user agent is used for [customer usage attribution][customer-usage-attribution] | No | The generated user agent is formatted as `driverName/driverVersion compiler/version (OS-ARCH)` |
|
| subscriptionID | Specify Azure subscription ID where the Azure Disks is created. | Azure subscription ID | No | If not empty, `resourceGroup` must be provided. |

## Static provisioning parameters for a PV

The following table includes parameters you can use to define a PV.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| volumeHandle | Azure disk URI | `/subscriptions/{sub-id}/resourcegroups/{group-name}/providers/microsoft.compute/disks/{disk-id}` |
Yes | N/A |
| volumeAttributes.fsType | File system type | `ext4` , `ext3` , `ext2` , `xfs` , `btrfs` for Linux, `ntfs` for Windows |
No | `ext4` for Linux, `ntfs` for Windows |
| volumeAttributes.partition | Partition number of the existing disk (only supported on Linux) | `1` , `2` , `3` |
No | Empty (no partition) - Make sure partition format is like `-part1` |
| volumeAttributes.cachingMode | [Disk host cache setting][disk-host-cache-setting] | `None` , `ReadOnly` , `ReadWrite` |
No | `ReadOnly` |

## Create an Azure Disk custom storage class

The default storage classes are suitable for most common scenarios. For some cases, you might want
to have your own storage class customized with your own parameters. For example, you might want to
change the `volumeBindingMode`

class.

You can use a `volumeBindingMode: Immediate`

class that guarantees it occurs immediately once the
persistent volume claim (PVC) is created. When your node pools are topology constrained, for example
when using availability zones, PVs would be bound or provisioned without knowledge of the pod's
scheduling requirements.

To address this scenario, you can use `volumeBindingMode: WaitForFirstConsumer`

, which delays the binding and provisioning of a PV until a pod that uses the PVC is created. This approach ensures that the persistent volume (PV) is provisioned in the same availability zone or topology as required per the pod's scheduling constraints. The default storage classes use `volumeBindingMode: WaitForFirstConsumer`

class.

Create a file named

`sc-azuredisk-csi-waitforfirstconsumer.yaml`

, and then paste the following manifest. The storage class is the same as our`managed-csi`

storage class, but with a different`volumeBindingMode`

class. For example:`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: azuredisk-csi-waitforfirstconsumer provisioner: disk.csi.azure.com parameters: skuname: StandardSSD_LRS allowVolumeExpansion: true reclaimPolicy: Delete volumeBindingMode: WaitForFirstConsumer`

Create the storage class by running the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify your`sc-azuredisk-csi-waitforfirstconsumer.yaml`

file:`kubectl apply -f sc-azuredisk-csi-waitforfirstconsumer.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/azuredisk-csi-waitforfirstconsumer created`


## Learn about volume snapshots

The Azure Disk CSI driver supports [volume snapshots](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html), enabling you to capture the state of persistent volumes at specific points in time for backup and restore operations. Volume snapshots let you create point-in-time copies of your persistent data without interrupting running applications. You can use these snapshots to create new volumes or restore existing ones to a previous state.

You can create two types of snapshots:

**Full snapshots**: Capture the complete state of the disk.**Incremental snapshots**: Capture only the changes since the last snapshot, offering better storage efficiency and cost savings.[Incremental snapshots](/en-us/azure/virtual-machines/disks-incremental-snapshots)are the default behavior when the`incremental`

parameter is set to`true`

in your VolumeSnapshotClass.

The following table provides details for these parameters.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| resourceGroup | Resource group for storing snapshot shots | EXISTING RESOURCE GROUP | No | If not specified, snapshots are stored in the same resource group as source Azure Disks |
| incremental | Take
|

`true`

, `false`

`true`

[tags](/en-us/azure/azure-resource-manager/management/tag-resources)[customer usage attribution](/en-us/azure/marketplace/azure-partner-customer-usage-attribution)`driverName/driverVersion compiler/version (OS-ARCH)`

`resourceGroup`

must be provided, `incremental`

must set as `false`

Volume snapshots support the following scenarios:

**Backup and restore**: Create point-in-time backups of stateful application data and restore when needed.**Data cloning**: Clone existing volumes to create new persistent volumes with the same data.**Disaster recovery**: Quickly recover from data loss or corruption.

### Create a volume snapshot

Note

Before proceeding, ensure that the application isn't writing data to the source disk.

For an example of this capability, create a

[volume snapshot class](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/storageclass-azuredisk-snapshot.yaml)with the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/storageclass-azuredisk-snapshot.yaml`

The output of the command resembles the following example:

`volumesnapshotclass.snapshot.storage.k8s.io/csi-azuredisk-vsc created`

Create a

[volume snapshot](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/azuredisk-volume-snapshot.yaml)from the PVC that was created earlier in this article.`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/azuredisk-volume-snapshot.yaml`

The output of the command resembles the following example:

`volumesnapshot.snapshot.storage.k8s.io/azuredisk-volume-snapshot created`

To verify that the snapshot was created correctly, run the following command:

`kubectl describe volumesnapshot azuredisk-volume-snapshot`

The output of the command resembles the following example:

`Name: azuredisk-volume-snapshot Namespace: default Labels: <none> Annotations: API Version: snapshot.storage.k8s.io/v1 Kind: VolumeSnapshot Metadata: Creation Timestamp: 2020-08-27T05:27:58Z Finalizers: snapshot.storage.kubernetes.io/volumesnapshot-as-source-protection snapshot.storage.kubernetes.io/volumesnapshot-bound-protection Generation: 1 Resource Version: 714582 Self Link: /apis/snapshot.storage.k8s.io/v1/namespaces/default/volumesnapshots/azuredisk-volume-snapshot UID: dd953ab5-6c24-42d4-ad4a-f33180e0ef87 Spec: Source: Persistent Volume Claim Name: pvc-azuredisk Volume Snapshot Class Name: csi-azuredisk-vsc Status: Bound Volume Snapshot Content Name: snapcontent-dd953ab5-6c24-42d4-ad4a-f33180e0ef87 Creation Time: 2020-08-31T05:27:59Z Ready To Use: true Restore Size: 10Gi Events: <none>`


### Create a new PVC based on a volume snapshot

You can create a new PVC based on a volume snapshot.

Use the snapshot created in the previous step, and create a

[new PVC](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/pvc-azuredisk-snapshot-restored.yaml)and a[new pod](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/snapshot/nginx-pod-restored-snapshot.yaml)to consume it:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/pvc-azuredisk-snapshot-restored.yaml kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/snapshot/nginx-pod-restored-snapshot.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk-snapshot-restored created pod/nginx-restored created`

To make sure it's the same PVC created before, check the contents by running the following command:

`kubectl exec nginx-restored -- ls /mnt/azuredisk`

The output of the command resembles the following example:

`lost+found outfile test.txt`


We can still see our previously created `test.txt`

file as expected.

## Clone volumes

A cloned volume is defined as a duplicate of an existing Kubernetes volume. For more information on cloning volumes in Kubernetes, see [volume cloning](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#volume-cloning).

Create a

[cloned volume](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml)of the[previously created](#create-azure-disk-pvs-using-built-in-storage-classes)`azuredisk-pvc`

and a[new pod](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml)to consume it.`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/cloning/pvc-azuredisk-cloning.yaml kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/cloning/nginx-pod-restored-cloning.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk-cloning created pod/nginx-restored-cloning created`

You can verify the content of the cloned volume by running the following command and confirming the file

`test.txt`

is created:`kubectl exec nginx-restored-cloning -- ls /mnt/azuredisk`

The output of the command resembles the following example:

`lost+found outfile test.txt`


## Resize an Azure Disk PV without downtime

You can request a larger volume for a PVC. Edit the PVC object, and specify a larger size. This change triggers the expansion of the underlying volume that backs the PV.

Note

A new PV is never created to satisfy the claim. Instead, an existing volume is resized.

In AKS, the built-in `managed-csi`

storage class already supports expansion, so use the [previously created](#create-azure-disk-pvs-using-built-in-storage-classes) one. The PVC requested a 10-Gi persistent volume. You can confirm by running the following command:

```
kubectl exec -it nginx-azuredisk -- df -h /mnt/azuredisk
```


The output of the command resembles the following example:

```
Filesystem Size Used Avail Use% Mounted on
/dev/sdc 9.8G 42M 9.8G 1% /mnt/azuredisk
```


Expand the PVC by increasing the

`spec.resources.requests.storage`

field running the following command:`kubectl patch pvc pvc-azuredisk --type merge --patch '{"spec": {"resources": {"requests": {"storage": "15Gi"}}}}'`

Note

Shrinking PVs is currently not supported. Trying to patch an existing PVC with a smaller size than the current one leads to the following error message:

`The persistentVolumeClaim "pvc-azuredisk" is invalid: spec.resources.requests.storage: Forbidden: field can not be less than previous value.`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azuredisk patched`

Run the following command to confirm the volume size increased:

`kubectl get pv`

The output of the command resembles the following example:

`NAME CAPACITY ACCESS MODES RECLAIM POLICY STATUS CLAIM STORAGECLASS REASON AGE pvc-391ea1a6-0191-4022-b915-c8dc4216174a 15Gi RWO Delete Bound default/pvc-azuredisk managed-csi 2d2h (...)`

And after a few minutes, run the following commands to confirm the size of the PVC:

`kubectl get pvc pvc-azuredisk`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE pvc-azuredisk Bound pvc-391ea1a6-0191-4022-b915-c8dc4216174a 15Gi RWO managed-csi 2d2h`

Run the following command to confirm the size of the disk inside the pod:

`kubectl exec -it nginx-azuredisk -- df -h /mnt/azuredisk`

The output of the command resembles the following example:

`Filesystem Size Used Avail Use% Mounted on /dev/sdc 15G 46M 15G 1% /mnt/azuredisk`


If your pod has *multiple containers*, you can specify which container by running the following command:

```
kubectl exec -it nginx-azuredisk -c <ContainerName> -- df -h /mnt/azuredisk
```


## Windows containers

The Azure Disk CSI driver supports Windows nodes and containers. If you want to use Windows containers, follow the [Windows containers quickstart](learn/quick-kubernetes-deploy-cli) to add a Windows node pool.

After you have a Windows node pool, you can now use the built-in storage classes like

`managed-csi`

. You can deploy an example[Windows-based stateful set](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/deploy/example/windows/statefulset.yaml)that saves timestamps into the file`data.txt`

by running the following[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azuredisk-csi-driver/master/deploy/example/windows/statefulset.yaml`

The output of the command resembles the following example:

`statefulset.apps/busybox-azuredisk created`

To validate the content of the volume, run the following command:

`kubectl exec -it statefulset-azuredisk-win-0 -- powershell -c "type c:/mnt/azuredisk/data.txt"`

The output of the command resembles the following example:

`2020-08-27 08:13:41Z 2020-08-27 08:13:42Z 2020-08-27 08:13:44Z (...)`


## On-demand bursting

On-demand disk bursting model allows disk bursts whenever its needs exceed its current capacity. This model generates extra charges anytime the disk bursts. On-demand bursting is only available for premium SSDs larger than 512 GiB. For more information on premium SSDs provisioned IOPS and throughput per disk, see [Premium SSD size](/en-us/azure/virtual-machines/disks-types#premium-ssds). Alternatively, credit-based bursting is where the disk will burst only if it has burst credits accumulated in its credit bucket. Credit-based bursting doesn't generate extra charges when the disk bursts. Credit-based bursting is only available for premium SSDs 512 GiB and smaller, and standard SSDs 1,024 GiB and smaller. For more information on on-demand bursting, see [On-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting).

Important

The default `managed-csi-premium`

storage class has on-demand bursting disabled and uses credit-based bursting. Any premium SSD dynamically created by a persistent volume claim based on the default `managed-csi-premium`

storage class also has on-demand bursting disabled.

To create a premium SSD persistent volume with [on-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting) enabled, you can create a new storage class with the [enableBursting](https://github.com/kubernetes-sigs/azuredisk-csi-driver/blob/master/docs/driver-parameters.md) parameter set to `true`

as shown in the following YAML template. For more information on enabling on-demand bursting, see [On-demand bursting](/en-us/azure/virtual-machines/disk-bursting#on-demand-bursting). For more information on building your own storage class with on-demand bursting enabled, see [Create a Burstable Managed CSI Premium Storage Class](https://github.com/Azure-Samples/burstable-managed-csi-premium).

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: burstable-managed-csi-premium
provisioner: disk.csi.azure.com
parameters:
skuname: Premium_LRS
enableBursting: "true"
reclaimPolicy: Delete
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```


## Clean up resources

When you're done with the resources created in this article, you can remove them using the
`kubectl delete`

command.

```
# Remove the pod
kubectl delete -f azure-pvc-disk.yaml
# Remove the persistent volume claim
kubectl delete -f azure-pvc.yaml
```


## Provision Azure Files PVs

Azure Files supports Azure Premium file shares. The minimum file share capacity is 100 GiB. We recommend using Azure Premium file shares instead of Standard file shares because Premium file shares offer higher performance, low-latency disk support for I/O-intensive workloads. With Azure Files shares, there's no limit as to how many can be mounted on a node. For more information on Kubernetes volumes, see [Storage options for applications in AKS](concepts-storage).

When you use storage CSI drivers on AKS, there are two more built-in `StorageClasses`

that uses the Azure Files CSI storage drivers. The other CSI storage classes are created with the cluster alongside the in-tree default storage classes.

`azurefile-csi`

: Uses Azure Standard Storage to create an Azure file share.`azurefile-csi-premium`

: Uses Azure Premium Storage to create an Azure file share.

The reclaim policy on both storage classes ensures that the underlying Azure files share is deleted when the respective PV is deleted. Since the storage classes also configure the file shares to be expandable, you just need to edit the [PVC](concepts-storage#persistent-volume-claims) with the new size.

Note

To have the best experience with Azure Files, follow these best practices. The location to configure mount options (`mountOptions`

) depends on whether you're provisioning dynamic or static persistent volumes.

- If you're dynamically provisioning a volume with a storage class, specify the mount options on the storage class object (kind:
`StorageClass`

). - If you're statically provisioning a volume, specify the mount options on the PersistentVolume object (kind:
`PersistentVolume`

). - If you're mounting the file share as an inline volume, specify the mount options on the Pod object (kind:
`Pod`

).

We recommend FIO when running benchmarking tests. For more information, see [benchmarking tools and tests](/en-us/azure/storage/files/nfs-performance#benchmarking-tools-and-tests).

A storage class is used to define how an Azure file share is created. A storage account is automatically created in the [node resource group](faq) for use with the storage class to hold the Azure files share. Choose one of the following [Azure storage redundancy SKUs](/en-us/azure/storage/common/storage-redundancy) for *skuName*:

Note

Modifying any resource under the node resource group in an AKS cluster is an unsupported action and will cause cluster operation failures. For more information, see [Why are two resource groups created with AKS?](faq)

**Standard_LRS**: Standard locally redundant storage**Standard_GRS**: Standard geo-redundant storage**Standard_ZRS**: Standard zone-redundant storage**Standard_RAGRS**: Standard read-access geo-redundant storage**Standard_RAGZRS**: Standard read-access geo-zone-redundant storage**Premium_LRS**: Premium locally redundant storage**Premium_ZRS**: Premium zone-redundant storage

For more information on Kubernetes storage classes for Azure Files, see [Kubernetes Storage Classes](https://kubernetes.io/docs/concepts/storage/storage-classes/#azure-file).

Create a file named

`azure-file-sc.yaml`

and copy in the following example manifest. For more information on`mountOptions`

, see the[Mount options](#mount-options)section.`kind: StorageClass apiVersion: storage.k8s.io/v1 metadata: name: my-azurefile provisioner: file.csi.azure.com # replace with "kubernetes.io/azure-file" if aks version is less than 1.21 allowVolumeExpansion: true mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict - actimeo=30 - nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks parameters: skuName: Premium_LRS`

Create the storage class using the

command.`kubectl apply`

`kubectl apply -f azure-file-sc.yaml`


### Create a PVC

A PVC uses the storage class object to dynamically provision an Azure file share. You can use the following YAML to create a PVC that's *100 GB* in size with *ReadWriteMany* access. For more information on access modes, see [Kubernetes persistent volume](https://kubernetes.io/docs/concepts/storage/persistent-volumes/#access-modes).

Create a file named

`azure-file-pvc.yaml`

and copy in the following YAML. Make sure the`storageClassName`

matches the storage class you created in the previous step.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: my-azurefile spec: accessModes: - ReadWriteMany storageClassName: my-azurefile resources: requests: storage: 100Gi`

Note

If using the

`Premium_LRS`

SKU for your storage class, the minimum value for`storage`

must be`100Gi`

.Create the PVC using the

command.`kubectl apply`

`kubectl apply -f azure-file-pvc.yaml`

Once completed, the file share is created. A Kubernetes secret is also created that includes connection information and credentials. You can use the

command to view the status of the PVC:`kubectl get`

`kubectl get pvc my-azurefile`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE my-azurefile Bound pvc-8436e62e-a0d9-11e5-8521-5a8664dc0477 100Gi RWX my-azurefile 5m`


### Mount the PVC

The following YAML creates a pod that uses the PVC *my-azurefile* to mount the Azure Files file share at the */mnt/azure* path. For Windows Server containers, specify a `mountPath`

using the Windows path convention, such as *"D:"*.

Create a file named

`azure-pvc-files.yaml`

, and copy in the following YAML. Make sure the`claimName`

matches the PVC you created in the previous step.`kind: Pod apiVersion: v1 metadata: name: mypod spec: containers: - name: mypod image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine resources: requests: cpu: 100m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - mountPath: /mnt/azure name: volume readOnly: false volumes: - name: volume persistentVolumeClaim: claimName: my-azurefile`

Create the pod using the

command.`kubectl apply`

`kubectl apply -f azure-pvc-files.yaml`

You now have a running pod with your Azure Files file share mounted in the

*/mnt/azure*directory. This configuration can be seen when inspecting your pod using thecommand. The following condensed example output shows the volume mounted in the container.`kubectl describe`

`Containers: mypod: Container ID: docker://053bc9c0df72232d755aa040bfba8b533fa696b123876108dec400e364d2523e Image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine Image ID: docker-pullable://nginx@sha256:d85914d547a6c92faa39ce7058bd7529baacab7e0cd4255442b04577c4d1f424 State: Running Started: Fri, 01 Mar 2019 23:56:16 +0000 Ready: True Mounts: /mnt/azure from volume (rw) /var/run/secrets/kubernetes.io/serviceaccount from default-token-8rv4z (ro) [...] Volumes: volume: Type: PersistentVolumeClaim (a reference to a PersistentVolumeClaim in the same namespace) ClaimName: my-azurefile ReadOnly: false [...]`


### Mount options

For Kubernetes versions 1.13.0 and later, the default values for `fileMode`

and `dirMode`

are `0777`

. When dynamically provisioning PVs using a storage class, you can define mount options directly in the storage class manifest. For details, see [Mount options](https://kubernetes.io/docs/concepts/storage/storage-classes/#mount-options). The following example demonstrates setting these permissions to `0777`

:

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: my-azurefile
provisioner: file.csi.azure.com # replace with "kubernetes.io/azure-file" if aks version is less than 1.21
allowVolumeExpansion: true
mountOptions:
- dir_mode=0777
- file_mode=0777
- uid=0
- gid=0
- mfsymlinks
- cache=strict
- actimeo=30
- nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks
parameters:
skuName: Premium_LRS
```


## Storage class parameters for dynamic volumes

The following table includes parameters you can use to define a custom storage class for your PVC.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| accountAccessTier |
|

`Hot`

or `Cool`

, and Premium account can only choose `Premium`

.`102400`

`true`

or `false`

`false`

`true`

or `false`

`false`

`true`

or `false`

`false`

`eastus`

.`true`

or `false`

`false`

1`privateEndpoint`

is specified, a private endpoint is created for the storage account. For other cases, a service endpoint is created by default.`privateEndpoint`

`smb`

, `nfs`

`smb`

`true`

or `false`

`false`

`true`

or `false`

`false`

`accountname.privatelink.file.core.windows.net`

.`accountname.file.core.windows.net`

or other sovereign cloud account address.[Access tier for file share](/en-us/azure/storage/files/storage-files-planning#storage-tiers)`TransactionOptimized`

(default), `Hot`

, and `Cool`

. Premium storage account type for file shares only.`storageAccountType`

)`Standard_LRS`

, `Standard_ZRS`

, `Standard_GRS`

, `Standard_RAGRS`

, `Standard_RAGZRS`

,`Premium_LRS`

, `Premium_ZRS`

, `StandardV2_LRS`

, `StandardV2_ZRS`

, `StandardV2_GRS`

, `StandardV2_GZRS`

, `PremiumV2_LRS`

, `PremiumV2_ZRS`

`Standard_LRS`

Minimum file share size for Premium account type is 100 GB.

ZRS account type is supported in limited regions.

NFS file share only supports Premium account type.

Standard V2 SKU names are for

[Azure Files provisioned v2 model](/en-us/azure/storage/files/understanding-billing#provisioned-v2-model).`core.windows.net`

, `core.chinacloudapi.cn`

, etc.`core.windows.net`

.[Tags](/en-us/azure/azure-resource-manager/management/tag-resources)are created in new storage account.1 If the storage account is created by the driver, then you only need to specify
`networkEndpointType: privateEndpoint`

parameter in storage class. The CSI driver creates the
private endpoint and private DNS zone (named `privatelink.file.core.windows.net`

) together with the
account. If you bring your own storage account, then you need to
[create the private endpoint](/en-us/azure/storage/common/storage-private-endpoints) for the storage account. If you're
using Azure Files storage in a network isolated cluster, you must create a custom storage class with
"networkEndpointType: privateEndpoint". You can follow this sample for reference:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: azurefile-csi
provisioner: file.csi.azure.com
allowVolumeExpansion: true
parameters:
skuName: Premium_LRS # available values: Premium_LRS, Premium_ZRS, Standard_LRS, Standard_GRS, Standard_ZRS, Standard_RAGRS, Standard_RAGZRS
networkEndpointType: privateEndpoint
reclaimPolicy: Delete
volumeBindingMode: Immediate
mountOptions:
- dir_mode=0777 # modify this permission if you want to enhance the security
- file_mode=0777
- mfsymlinks
- cache=strict # https://linux.die.net/man/8/mount.cifs
- nosharesock # reduce probability of reconnect race
- actimeo=30 # reduce latency for metadata-heavy workload
- nobrl # disable sending byte range lock requests to the server and for applications which have challenges with posix locks
```


## Static provisioning parameters for PVs

The following table includes parameters you can use to define a PV.

| Name | Meaning | Available Value | Mandatory | Default value |
|---|---|---|---|---|
| volumeAttributes.resourceGroup | Specify an Azure resource group name. | myResourceGroup | No | If empty, driver uses the same resource group name as current cluster. |
| volumeAttributes.storageAccount | Specify an existing Azure storage account name. | storageAccountName | Yes | |
| volumeAttributes.shareName | Specify an Azure file share name. | fileShareName | Yes | |
| volumeAttributes.folderName | Specify a folder name in Azure file share. | folderName | No | If folder name doesn't exist in file share, mount would fail. |
| volumeAttributes.protocol | Specify file share protocol. | `smb` , `nfs` |
No | `smb` |
| volumeAttributes.server | Specify Azure storage account server address | Existing server address, for example `accountname.privatelink.file.core.windows.net` . |
No | If empty, driver uses default `accountname.file.core.windows.net` or other sovereign cloud account address. |

## Create a PV snapshot class

The Azure Files CSI driver supports creating [snapshots of persistent volumes](https://kubernetes-csi.github.io/docs/snapshot-restore-feature.html) and the underlying file shares.

Create a

[volume snapshot class](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/snapshot/volumesnapshotclass-azurefile.yaml)with the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/snapshot/volumesnapshotclass-azurefile.yaml`

The output of the command resembles the following example:

`volumesnapshotclass.snapshot.storage.k8s.io/csi-azurefile-vsc created`

Create a

[volume snapshot](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/snapshot/volumesnapshot-azurefile.yaml)from the PVC created earlier (`pvc-azurefile`

).`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/snapshot/volumesnapshot-azurefile.yaml`

The output of the command resembles the following example:

`volumesnapshot.snapshot.storage.k8s.io/azurefile-volume-snapshot created`

Verify the snapshot was created correctly by running the following command:

`kubectl describe volumesnapshot azurefile-volume-snapshot`

The output of the command resembles the following example:

`Name: azurefile-volume-snapshot Namespace: default Labels: <none> Annotations: API Version: snapshot.storage.k8s.io/v1beta1 Kind: VolumeSnapshot Metadata: Creation Timestamp: 2020-08-27T22:37:41Z Finalizers: snapshot.storage.kubernetes.io/volumesnapshot-as-source-protection snapshot.storage.kubernetes.io/volumesnapshot-bound-protection Generation: 1 Resource Version: 955091 Self Link: /apis/snapshot.storage.k8s.io/v1beta1/namespaces/default/volumesnapshots/azurefile-volume-snapshot UID: c359a38f-35c1-4fb1-9da9-2c06d35ca0f4 Spec: Source: Persistent Volume Claim Name: pvc-azurefile Volume Snapshot Class Name: csi-azurefile-vsc Status: Bound Volume Snapshot Content Name: snapcontent-c359a38f-35c1-4fb1-9da9-2c06d35ca0f4 Ready To Use: false Events: <none>`


## Resize an Azure Files PV

You can request a larger volume for a PVC. Edit the PVC object, and specify a larger size. This change triggers the expansion of the underlying volume that backs the PV.

Note

A new PV is never created to satisfy the claim. Instead, an existing volume is resized. Shrinking persistent volumes is currently not supported.

In AKS, the built-in `azurefile-csi`

storage class already supports expansion, so use the PVC we created earlier with this storage class. The PVC requested a 100 GiB file share. We can confirm that by running:

```
kubectl exec -it nginx-azurefile -- df -h /mnt/azurefile
```


The output of the command resembles the following example:

```
Filesystem Size Used Avail Use% Mounted on
//f149b5a219bd34caeb07de9.file.core.windows.net/pvc-5e5d9980-da38-492b-8581-17e3cad01770 100G 128K 100G 1% /mnt/azurefile
```


Expand the PVC by increasing the

`spec.resources.requests.storage`

field:`kubectl patch pvc pvc-azurefile --type merge --patch '{"spec": {"resources": {"requests": {"storage": "200Gi"}}}}'`

The output of the command resembles the following example:

`persistentvolumeclaim/pvc-azurefile patched`

Verify that both the PVC and the file system inside the pod show the new size:

`kubectl get pvc pvc-azurefile NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE pvc-azurefile Bound pvc-5e5d9980-da38-492b-8581-17e3cad01770 200Gi RWX azurefile-csi 64m kubectl exec -it nginx-azurefile -- df -h /mnt/azurefile Filesystem Size Used Avail Use% Mounted on //f149b5a219bd34caeb07de9.file.core.windows.net/pvc-5e5d9980-da38-492b-8581-17e3cad01770 200G 128K 200G 1% /mnt/azurefile`


## Use a PV with private Azure Files storage (private endpoint)

If your Azure Files resources are protected with a private endpoint, you must create your own storage class. Make sure to configure your [DNS settings to resolve the private endpoint IP address to the FQDN of the connection string](/en-us/azure/private-link/private-endpoint-dns#azure-services-dns-zone-configuration).

Customize the following parameters:

`resourceGroup`

: The resource group where the storage account is deployed.`storageAccount`

: The storage account name.`server`

: The FQDN of the storage account's private endpoint.

Create a file named

`private-azure-file-sc.yaml`

, and then paste the following example manifest in the file. Replace the values for`<resourceGroup>`

and`<storageAccountName>`

. For example:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: private-azurefile-csi provisioner: file.csi.azure.com allowVolumeExpansion: true parameters: resourceGroup: <resourceGroup> storageAccount: <storageAccountName> server: <storageAccountName>.file.core.windows.net reclaimPolicy: Delete volumeBindingMode: Immediate mountOptions: - dir_mode=0777 - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict # https://linux.die.net/man/8/mount.cifs - nosharesock # reduce probability of reconnect race - actimeo=30 # reduce latency for metadata-heavy workload`

Create the storage class by using the

`kubectl apply`

command:`kubectl apply -f private-azure-file-sc.yaml`

The output of the command resembles the following example:

`storageclass.storage.k8s.io/private-azurefile-csi created`

Create a file named

`private-pvc.yaml`

, and then paste the following example manifest in the file:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: private-azurefile-pvc spec: accessModes: - ReadWriteMany storageClassName: private-azurefile-csi resources: requests: storage: 100Gi`

Create the PVC by using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f private-pvc.yaml`


## Use Managed Identity to access Azure Files storage (Preview)

Azure Files now supports managed identity-based authentication for SMB access. With this capability, your applications running in AKS can securely access Azure Files shares without the need to store or manage storage account keys or credentials. Managed identities provide a streamlined and secure authentication mechanism, simplifying access management and reducing the risk associated with credential exposure. You can create a dynamic volume or a static volume.

Note

Managed identity support for Azure Files in AKS is available in preview starting with AKS version 1.34 on Linux nodes.

To enable managed identity for dynamically provisioned volumes, follow these steps:

Create a storage class with managed identity enabled using a YAML file, for example,

`azurefile-csi-managed-identity.yaml`

with the following sample content. Set`mountWithManagedIdentity: "true"`

under`parameters`

:`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: azurefile-csi provisioner: file.csi.azure.com parameters: resourceGroup: EXISTING_RESOURCE_GROUP_NAME # optional, node resource group by default if it's not provided storageAccount: EXISTING_STORAGE_ACCOUNT_NAME # optional, a new account will be created if it's not provided mountWithManagedIdentity: "true" # optional, clientID of the managed identity, kubelet identity would be used by default if it's not provided clientID: "xxxxx-xxxx-xxx-xxx-xxxxxxx" reclaimPolicy: Delete volumeBindingMode: Immediate allowVolumeExpansion: true mountOptions: - dir_mode=0777 # modify this permission if you want to enhance the security - file_mode=0777 - uid=0 - gid=0 - mfsymlinks - cache=strict # https://linux.die.net/man/8/mount.cifs - nosharesock # reduce probability of reconnect race - actimeo=30 # reduce latency for metadata-heavy workload - nobrl # disable sending byte range lock requests to the server`

Apply this storage class by running the following command:

`kubectl apply -f azurefile-csi-managed-identity.yaml`

Deploy your

**StatefulSet**or workload using the new storage class that references this PVC to ensure that the volume is provisioned using managed identity authentication. In your PVC manifest, set`storageClassName: azurefile-csi-managed-identity`

. For example:`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: azurefile-managed-identity-pvc spec: accessModes: - ReadWriteMany storageClassName: azurefile-csi-managed-identity resources: requests: storage: 100Gi`


## Learn about Azure Files NFS

Azure Files supports the
[NFS v4.1 protocol](/en-us/azure/storage/files/storage-files-how-to-create-nfs-shares). NFS version 4.1
support for Azure Files provides you with a fully managed NFS system as a service built on highly
available, highly durable distributed resilient storage platform.

This option is optimized for random access workloads with in-place data updates and provides full POSIX file system support. This section shows you how to use NFS shares with the Azure File CSI driver on an AKS cluster.

Note

You can use a private endpoint instead of allowing access to the selected VNet.

This section explains how to maximize performance and security when using Azure Files NFS 4.1 with AKS. Learn how to:

Optimize NFS read and write size settings

Create and configure an NFS storage class

Deploy workloads that use NFS-backed volumes

Enable Encryption in Transit (EiT) to protect data as it moves between your AKS cluster and Azure Files.


This section provides information about how to approach performance tuning NFS with the Azure Files
CSI driver with the `rsize`

(read size) and `wsize`

(write size) options. The `rsize`

and `wsize`

options set the maximum transfer size of an NFS operation. If `rsize`

or `wsize`

aren't specified on
mount, the client and server negotiate the largest size supported by the two. Currently, both Azure
Files and modern Linux distributions support read and write sizes as large as 1,048,576 bytes (1
MiB).

Optimal performance is based on efficient client-server communication. Increasing or decreasing the
**mount** read and write option size values can improve NFS performance. The default size of the
read/write packets transferred between client and server are 8 KB for NFS version 2, and 32 KB for
NFS version 3 and 4. These defaults might be too large or too small. Reducing the `rsize`

and
`wsize`

might improve NFS performance in a congested network by sending smaller packets for each
NFS-read reply and write request. However, this reduction can increase the number of packets needed
to send data across the network, increasing total network traffic and CPU utilization on the client
and server.

It's important that you perform testing to find an `rsize`

and `wsize`

that sustains efficient
packet transfer, where it doesn't decrease throughput and increase latency.

For example, to configure a maximum `rsize`

and `wsize`

of 256-KiB, configure the `mountOptions`

in
the storage class as follows:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: azurefile-csi-nfs
provisioner: file.csi.azure.com
allowVolumeExpansion: true
parameters:
protocol: nfs
mountOptions:
- nconnect=4
- noresvport
- actimeo=30
- rsize=262144
- wsize=262144
```


## Other storage class examples

## Windows containers

The Azure Files CSI driver also supports Windows nodes and containers. To use Windows containers, follow the [Windows containers quickstart](learn/quick-windows-container-deploy-cli) to add a Windows node pool.

After you have a Windows node pool, use the built-in storage classes like

`azurefile-csi`

or create a custom one. You can deploy an example[Windows-based stateful set](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/deploy/example/windows/statefulset.yaml)that saves timestamps into a file`data.txt`

by running the[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/azurefile-csi-driver/master/deploy/example/windows/statefulset.yaml`

The output of the command resembles the following example:

`statefulset.apps/busybox-azurefile created`

Validate the contents of the volume by running the following

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command:`kubectl exec -it busybox-azurefile-0 -- cat c:\\mnt\\azurefile\\data.txt # on Linux or MacOS Bash kubectl exec -it busybox-azurefile-0 -- cat c:\mnt\azurefile\data.txt # on Windows Powershell or CMD`

The output of the commands resembles the following example:

`2020-08-27 22:11:01Z 2020-08-27 22:11:02Z 2020-08-27 22:11:04Z (...)`


## Next steps

- For Azure Files CSI driver parameters, see
[CSI driver parameters](https://github.com/kubernetes-sigs/azurefile-csi-driver/blob/master/docs/driver-parameters.md#static-provisionbring-your-own-file-share). - For more information about disk-based storage solutions, see
[Disk-based solutions in AKS](/en-us/azure/cloud-adoption-framework/scenarios/app-platform/aks/storage#disk-based-solutions). - For more information about storage best practices, see
[Best practices for storage and backups in Azure Kubernetes Service](operator-best-practices-storage). - For more information about Azure ultra disk, see [Use ultra disks on Azure Kubernetes Service (AKS)][use-ultra-disks].
- For more information about Azure tags, see
[Use Azure tags in Azure Kubernetes Service (AKS)](use-tags).
