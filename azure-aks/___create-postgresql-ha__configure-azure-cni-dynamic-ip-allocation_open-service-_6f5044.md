---
merged_at: 2026-01-26T20:54:26.151049
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _create-postgresql-ha__configure-azure-cni-dynamic-ip-allocation_open-service-me_f44d7a.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: create-postgresql-ha.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/create-postgresql-ha -->

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

<!-- DOCUMENTO FUSIONADO: _configure-azure-cni-dynamic-ip-allocation_open-service-mesh-deploy-addon-bicep.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: configure-azure-cni-dynamic-ip-allocation.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/configure-azure-cni-dynamic-ip-allocation -->

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

<!-- DOCUMENTO FUSIONADO: open-service-mesh-deploy-addon-bicep.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-deploy-addon-bicep -->

# Deploy the Open Service Mesh add-on using Bicep in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to deploy the Open Service Mesh (OSM) add-on to Azure Kubernetes Service (AKS) using a [Bicep](/en-us/azure/azure-resource-manager/bicep/) template.

Note

With the retirement of [Open Service Mesh (OSM)](https://docs.openservicemesh.io/) by the Cloud Native Computing Foundation (CNCF), we recommend identifying your OSM configurations and migrating them to an equivalent Istio configuration. For information about migrating from OSM to Istio, see [Migration guidance for Open Service Mesh (OSM) configurations to Istio](open-service-mesh-istio-migration-guidance).

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

<!-- DOCUMENTO FUSIONADO: __tutorial-kubernetes-upgrade-cluster_availability-zones__managed-azure-ad_enabl_c929e5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _tutorial-kubernetes-upgrade-cluster_availability-zones.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-upgrade-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-upgrade-cluster -->

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

<!-- DOCUMENTO FUSIONADO: availability-zones.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/availability-zones -->

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

On September 30, 2025, Basic Load Balancer will be retired. For more information, see the [official announcement](https://azure.microsoft.com/updates/azure-basic-load-balancer-will-be-retired-on-30-september-2025-upgrade-to-standard-load-balancer/). If you use Basic Load Balancer, make sure to [upgrade](/en-us/azure/load-balancer/load-balancer-basic-upgrade-guidance) to Standard Load Balancer before the retirement date.

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

<!-- DOCUMENTO FUSIONADO: _managed-azure-ad_enable-authentication-microsoft-entra-id.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: managed-azure-ad.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/managed-azure-ad -->

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

<!-- DOCUMENTO FUSIONADO: enable-authentication-microsoft-entra-id.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/enable-authentication-microsoft-entra-id -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/localdns-custom -->

# Configure LocalDNS in Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

LocalDNS is a feature in Azure Kubernetes Service (AKS) designed to enhance the Domain Name System (DNS) resolution performance and resiliency for workloads running in your cluster. When you deploy a DNS proxy on each node, LocalDNS reduces DNS query latency, improves reliability during network disruptions, and provides advanced configuration options for DNS caching and forwarding. This article explains how LocalDNS works, its configuration options, and how to enable, verify, and troubleshoot LocalDNS in your AKS clusters.

To learn about what LocalDNS is, including architecture details, and key capabilities, refer to [DNS Resolution in Azure Kubernetes Service (AKS)](dns-concepts).

## Best practices for LocalDNS configuration

When implementing LocalDNS in your AKS clusters, consider the following best practices:

**Start with a minimal configuration**: Begin with a simple configuration that uses the`Preferred`

mode before moving to`Required`

mode. This setup allows you to validate that LocalDNS works as expected without breaking your cluster.**Implement proper caching strategies**: Configure cache settings based on your workload characteristics:- For frequently changing records, use shorter
`cacheDurationInSeconds`

values. When doing so, it's important to note that cacheDurationInSeconds acts as a cap on the DNS record TTL but doesn't increase it. The resulting TTL is the smaller of what is returned from upstream or what is set in the cache plugin. - For stable records, use longer cache durations to reduce DNS queries.
- Enable
`serveStale`

with appropriate settings to maintain service during DNS outages. - Caching with LocalDNS operates on a best effort basis and doesn't guarantee stale responses. The cache is divided into 256 shards and with a default maximum of 10,000 entries, allowing each shard to hold about 39 entries. When a shard is full and a new entry needs to be added, one of the existing entries is chosen at random to be evicted. There's no preference for older or expires entries. As a result, a stale record might not always be available, especially under high query volume.

- For frequently changing records, use shorter
**Monitor DNS performance**: After enabling LocalDNS, monitor your application's DNS performance using:- Application performance metrics.
- Node metrics to detect reduced network pressure.
- Log entries when
`queryLogging`

is set to`Log`

.

**Follow least privilege principle**: When configuring DNS forwarding rules, only allow access to the required DNS servers and domains.**Test before production deployment**: Always test LocalDNS configuration in a nonproduction environment before rolling it out to production clusters.**Use Infrastructure as Code (IaC)**: Store your*localdnsconfig.json*file in your infrastructure repository and include it in your AKS deployment templates.**Network configuration for TCP forwarding**: When using TCP for DNS forwarding to VnetDNS, ensure that your Network Security Groups (NSGs), firewalls, or Network Virtual Appliances (NVAs) don't block TCP traffic between CoreDNS/LocalDNS and VnetDNS servers.**Avoid enabling both NodeLocal DNSCache and LocalDNS**: It isn't recommended to enable both the upstream Kubernetes NodeLocal DNSCache and LocalDNS in your node pool. While AKS doesn't block this configuration, all DNS traffic is routed through LocalDNS, which might lead to unexpected behavior or reduced benefits from NodeLocal DNSCache.

## Prerequisites

- You must have an existing AKS cluster with Kubernetes versions 1.31 or later to use LocalDNS. If you need an AKS cluster, you can create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - This article requires version 2.80.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed.
- LocalDNS is only supported on node pools running Azure Linux or Ubuntu 22.04 or newer.
- The Virtual Machine (VM) SKU used for your node pool must have at least 4 vCPUs (cores) to support LocalDNS.
- LocalDNS isn't compatible with
[applied FQDN filter policies in Advanced Container Networking Services (ACNS)](how-to-apply-fqdn-filtering-policies).

## Manage LocalDNS on an AKS cluster

LocalDNS is configured at the node pool level in AKS, meaning you can enable or disable LocalDNS independently for each node pool in your cluster. This tailors DNS resolution behavior based on the specific requirements of different workloads or environments. To enable LocalDNS on a node pool, you need to provide a configuration file: *localdnsconfig.json* that defines how LocalDNS should operate for that node pool.

If you don't specify a custom configuration file, AKS automatically applies a default LocalDNS configuration.

Note

If you're using Node Auto-Provisioning (NAP), see [LocalDNS configuration](node-auto-provisioning-aksnodeclass#localdns-configuration) for instructions on how to enable LocalDNS with NAP.

To enable LocalDNS during node pool creation, use the following command with your custom configuration file:

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


To enable LocalDNS on an existing node pool, use the following command with your custom configuration file:

```
az aks nodepool update --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --localdns-config ./localdnsconfig.json
```


Important

Enabling LocalDNS on a node pool initiates a reimage operation on all nodes within that pool. This process can cause temporary disruption to running workloads and might lead to application downtime if not properly managed. You should plan for potential service interruptions and ensure that the applications are configured for high availability or have appropriate disruption budgets in place before enabling this setting.

## Create a custom server block in LocalDNS

CoreDNS matches queries to a specific server block based on an exact match for domain being queried and not on partial matches. If you have the need for custom server blocks, you can add them to your LocalDNS configuration by creating a file called *localdnsconfig.json* with the added configurations.

For example, if you have specific DNS needs when accessing microsoft.com, you could use the following server block:

```
"microsoft.com": {
"queryLogging": "Error",
"protocol": "ForceTCP",
"forwardDestination": "ClusterCoreDNS",
"forwardPolicy": "Sequential",
"maxConcurrent": 1000,
"cacheDurationInSeconds": 3600,
"serveStaleDurationInSeconds": 3600,
"serveStale": "Immediate"
}
```


## Monitor LocalDNS

LocalDNS exposes Prometheus metrics that you can use for monitoring and alerting. These [metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default#coredns) are exposed on port `9253`

of the Node IP and can be scraped from there.

The following example YAML shows a scrape configuration you can use with the [Azure Managed Prometheus add on as a DaemonSet](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-configuration):

```
kind: ConfigMap
apiVersion: v1
metadata:
name: ama-metrics-prometheus-config-node
namespace: kube-system
data:
prometheus-config: |-
global:
scrape_interval: 1m
scrape_configs:
- job_name: localdns-metrics
scrape_interval: 1m
scheme: http
metrics_path: /metrics
relabel_configs:
- source_labels: [__metrics_path__]
regex: (.*)
target_label: metrics_path
- source_labels: [__address__]
replacement: '$NODE_NAME'
target_label: instance
static_configs:
- targets: ['$NODE_IP:9253']
```


## Troubleshoot LocalDNS

### DNS queries to specific domains are failing

If DNS queries to specific domains are failing after enabling LocalDNS:

- Check if you have domain-specific overrides in your
*localdnsconfig.json*that might be misconfigured. - Temporarily try removing domain-specific overrides and using only the default
`.`

configuration. - Check if the issue occurs with both User Datagram Protocol (UDP) and Transmission Control Protocol (TCP) by adjusting the
`protocol`

setting.

### Update VNet DNS servers for LocalDNS

When you update custom DNS servers directly in the VNet configuration (using the Azure portal or CLI), these changes aren't automatically applied to your AKS cluster nodes. This happens because updating DNS settings at the VNet level only informs the Network Resource Provider (NRP), but doesn't notify the AKS Resource Provider. As a result, AKS nodes continue to use the previous DNS server settings until further action is taken.

To ensure AKS nodes pick up the new VNet DNS server settings:

Update the VNet DNS configuration using the Azure portal or APIs as needed.

Reimage the node pool through the AKS Resource Provider to apply and persist the DNS changes:

`az aks nodepool upgrade --resource-group myResourceGroup --cluster-name myAKSCluster --name mynodepool --node-image-only`


This process ensures the AKS Resource Provider is aware of the DNS changes and applies them to all nodes in the node pool.

## Next steps

For information on LocalDNS in AKS, see [LocalDNS in Azure Kubernetes Service (conceptual)](dns-concepts).

For comprehensive troubleshooting guidance on DNS issues when using LocalDNS, see [Troubleshoot LocalDNS issues in AKS](/en-us/troubleshoot/azure/azure-kubernetes/connectivity/dns/troubleshoot-localdns).

For details on how to customize CoreDNS in AKS, refer to the [CoreDNS customization guide](coredns-custom).

For information on the CoreDNS project, see [the CoreDNS upstream project page](https://coredns.io/).

To learn more about core network concepts, see [Network concepts for applications in AKS](concepts-network).

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-metrics -->

# What is container network metrics?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services in Azure Kubernetes Service (AKS) facilitates the collection of comprehensive container network metrics to give you valuable insights into the performance of your containerized environment. The capability continuously captures essential metrics at the node level and pod level, including traffic volume, dropped packets, connection states, and Domain Name System (DNS) resolution times for effective monitoring and optimizing network performance.

Capturing these metrics is essential for understanding how containers communicate, how traffic flows between services, and where bottlenecks or disruptions might occur. Advanced Container Networking Services integrates seamlessly with monitoring tools like Prometheus and Grafana to give you a complete view of networking metrics. Use the metrics for in-depth troubleshooting, network optimization, and performance tuning.

In a cloud-native world, maintaining a healthy and efficient network in a dynamic containerized environment is vital to ensuring that applications perform as expected. Without proper visibility into network traffic and its patterns, identifying potential issues or inefficiencies becomes challenging.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Key benefits

Deep visibility into network performance

Enhanced troubleshooting and optimization

Proactive anomaly detection

Better resource management and scaling

Capacity planning and compliance

Source-level metrics filtering for cost optimization and noise reduction with

[container network metrics filtering](#container-network-metrics-filtering-preview)Simplified metrics storage and visualization options. Choose between:

**Azure managed service for Prometheus and Azure Managed Grafana**: Azure manages the infrastructure and maintenance, so you can focus on configuring metrics and visualizing metrics.**Bring your own (BYO) Prometheus and Grafana**: You deploy and configure your own instances of Prometheus and Grafana, and you manage the underlying infrastructure.


## Metrics captured

### Node-level metrics

Understanding the health of your container network at the node-level is crucial for maintaining optimal application performance. These metrics provide insights into traffic volume, dropped packets, number of connections, and other data by node. The metrics are stored in Prometheus format, so, you can view them in Grafana.

The following metrics are aggregated per node. All metrics include one of these labels:

`cluster`

`instance`

(node name)

For Cilium data plane scenarios, Container Network Observability provides metrics only for Linux. Windows is currently not supported. Cilium exposes several metrics including the following used by Container Network Observability.

| Metric name | Description | Extra labels | Linux | Windows |
|---|---|---|---|---|
cilium_forward_count_total |
Total forwarded packet count | `direction` |
✅ | ❌ |
cilium_forward_bytes_total |
Total forwarded byte count | `direction` |
✅ | ❌ |
cilium_drop_count_total |
Total dropped packet count | `direction` , `reason` |
✅ | ❌ |
cilium_drop_bytes_total |
Total dropped byte count | `direction` , `reason` |
✅ | ❌ |

### Pod-level metrics (Hubble metrics)

These Prometheus metrics include source and destination pod information so that you can pinpoint network-related issues at a granular level. Metrics cover information like traffic volume, dropped packets, TCP resets, and Layer 4/Layer 7 packet flows. DNS metrics like DNS errors and DNS requests missing responses are collected by default for non-Cilium data planes. For Cilium data planes, a Cilium FQDN network policy is required to collect DNS metrics, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.

The following table describes the metrics that are aggregated per pod (node information is preserved).

All metrics include labels:

`cluster`

`instance`

(node name)`source`

or`destination`

For

*outgoing traffic*, a`source`

label that indicates the source pod namespace and name is applied.For

*incoming traffic*, a`destination`

label that indicates the destination pod namespace and name is applied.


| Metric name | Description | Extra Labels | Linux | Windows |
|---|---|---|---|---|
hubble_dns_queries_total |
Total DNS requests by query | `source` or `destination` , `query` , `qtypes` (query type) |
✅ | ❌ |
hubble_dns_responses_total |
Total DNS responses by query/response | `source` or `destination` , `query` , `qtypes` (query type), `rcode` (return code), `ips_returned` (number of IPs) |
✅ | ❌ |
hubble_drop_total |
Total dropped packet count | `source` or `destination` , `protocol` , `reason` |
✅ | ❌ |
hubble_tcp_flags_total |
Total TCP packets count by flag | `source` or `destination` , `flag` |
✅ | ❌ |
hubble_flows_processed_total |
Total network flows processed (Layer 4/Layer 7 traffic) | `source` or `destination` , `protocol` , `verdict` , `type` , `subtype` |
✅ | ❌ |

## Container network metrics filtering (Preview)

Now that you have the ability to collect comprehensive metrics at both node and pod levels, you might find yourself dealing with a significant volume of data. To help reduce noise and optimize storage costs, Container Network Observability introduces **container network metrics filtering**. This feature enables you to filter metrics at the source before they are collected and stored, giving you control over which metrics are most relevant to your specific monitoring and troubleshooting needs. This feature is only available for Cilium clusters.

Container network metrics filtering is particularly valuable in large-scale production environments where the sheer volume of metrics can impact storage costs and query performance. By filtering out unnecessary metrics early in the collection process, you can focus on the data that matters most to your operations while maintaining the visibility you need for effective network monitoring.

The filtering capability supports multiple dimensions including namespace-based filtering to focus on specific applications, pod and label-based filtering for targeted monitoring, and metric-specific filtering to collect only the types of metrics that are essential for your use case. This flexibility allows you to strike the right balance between comprehensive observability and cost-effective operations.

To learn more on how to enable container network metrics filtering, see [How to Configure Container Network Metrics Filtering ](how-to-configure-container-network-metrics-filtering).

### Limitations

- Pod-level metrics are available only on Linux.
- Cilium data plane is supported starting with Kubernetes version 1.29.
- Metric labels have subtle differences between Cilium and non-Cilium clusters.
- For Cilium based clusters, DNS metrics are only available for pods that have Cilium Network policies (CNP) configured on their clusters, or customers can also troubleshoot DNS using Hubble CLI and observing real-time logs.
- Flow logs are not currently available in the air gapped cloud.
- Hubble relay may crash if one of the Hubble node agents goes down and may cause interruptions to Hubble CLI.
- When using Advanced Container Networking Services (ACNS) on non-Cilium data planes, FIPS support isn't available on Ubuntu 20.04 nodes due to kernel restrictions. To enable FIPS in this scenario, you must use an Azure Linux node pool. This limitation is expected to be resolved with the release of Ubuntu 22 FIPS. For updates, see the
[AKS issue tracker](https://github.com/Azure/AKS/issues/4857). - Container network metrics filtering is only available for Cilium Clusters.

Refer to the FIPS support matrix below:

| Operating System | FIPS Support |
|---|---|
| Azure Linux 3.0 | Yes |
| Azure Linux 2.0 | Yes |
| Ubuntu 20.04 | No |

This limitation does not apply when ACNS is running on Cilium data planes.

### Scale

The managed service for Prometheus in Azure Monitor and Azure Managed Grafana impose service-specific scale limitations. For more information, see [Scrape Prometheus metrics at scale in Azure Monitor](/en-us/azure/azure-monitor/essentials/prometheus-metrics-scrape-scale).

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- To create an AKS cluster by using Container Network Observability to capture metrics, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-byo-cni -->

# Bring your own CNI plugin with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes doesn't provide a network interface system by default. Instead, [network plugins](https://kubernetes.io/docs/concepts/extend-kubernetes/compute-storage-net/network-plugins/) provide this functionality. Azure Kubernetes Service (AKS) provides several supported Container Network Interface (CNI) plugins. For information on supported plugins, see [Networking concepts for applications in Azure Kubernetes Service](concepts-network).

The supported plugins meet most networking needs in Kubernetes. However, advanced AKS users might want the same CNI plugin that they used in on-premises Kubernetes environments. Or these users might want to use advanced functionalities available in other CNI plugins.

This article shows how to deploy an AKS cluster with no CNI plugin preinstalled. From there, you can install any CNI plugin that works in Azure.

## Support

Microsoft support can't assist with CNI-related issues in clusters that you deploy by bringing your own CNI plugin. For example, CNI-related issues would cover most east/west (pod to pod) traffic, along with `kubectl proxy`

and similar commands. If you want CNI-related support, use a supported AKS network plugin or seek support from the CNI plugin vendor.

Microsoft still provides support for issues that aren't related to CNI.

## Prerequisites

- For Azure Resource Manager or Bicep, use at least template version 2022-01-02-preview or 2022-06-01.
- For the Azure CLI, use at least version 2.39.0.
- The virtual network for the AKS cluster must allow outbound internet connectivity.
- AKS clusters can't use
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the address range for the Kubernetes service, pods, or cluster virtual network. - The cluster identity that the AKS cluster uses must have at least
[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within your virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


- The subnet assigned to the AKS node pool can't be a
[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview). - AKS doesn't apply network security groups (NSGs) to its subnet or modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, you must ensure that the security rules in the NSGs allow traffic within the node's Classless Inter-Domain Routing (CIDR) range. For more information, see
[Network security groups](concepts-network#network-security-groups). - AKS doesn't create a route table in the managed virtual network.
- You must specify a Pod CIDR (IP address range for pods). The AKS control plane uses this range for internal traffic routing to pods, even though pod IP assignment will be managed by your custom CNI. If no pod CIDR is provided, control plane to pod communication may fail or be misrouted. You must select a pod CIDR that does not conflict with any other network in your environment and avoids Azure reserved ranges, such as,
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

. For example, you might use a range such as`10.XX.0.0/16`

that is unique to your cluster. This ensures that the control plane can route directly to pod IPs on your nodes, and no IP overlap will occur if you integrate with other networks or clusters.

## Create an AKS cluster with no CNI plugin preinstalled

Create an Azure resource group for your AKS cluster by using the

command.`az group create`

`az group create --location eastus --name myResourceGroup`

Create an AKS cluster by using the

command. Pass the`az aks create`

`--network-plugin`

parameter with the parameter value of`none`

.`az aks create \ --location eastus \ --resource-group myResourceGroup \ --name myAKSCluster \ --network-plugin none \ --pod-cidr "10.10.0.0/16" \ --generate-ssh-keys`


## Deploy a CNI plugin

After AKS provisioning finishes, the cluster is online. But all the nodes are in a `NotReady`

state, as shown in the following example:

```
$ kubectl get nodes
NAME STATUS ROLES AGE VERSION
aks-nodepool1-23902496-vmss000000 NotReady agent 6m9s v1.21.9
$ kubectl get node -o custom-columns='NAME:.metadata.name,STATUS:.status.conditions[?(@.type=="Ready")].message'
NAME STATUS
aks-nodepool1-23902496-vmss000000 container runtime network not ready: NetworkReady=false reason:NetworkPluginNotReady message:Network plugin returns error: cni plugin not initialized
```


At this point, the cluster is ready for installation of a CNI plugin.
