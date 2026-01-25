---
merged_at: 2026-01-25T12:06:27.672817
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: node-resource-group-lockdown.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-resource-group-lockdown -->

# Deploy a fully managed resource group using node resource group lockdown in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS deploys infrastructure into your subscription for connecting to and running your applications. Changes made directly to resources in the [node resource group](concepts-clusters-workloads#node-resource-group) can affect cluster operations or cause future issues. For example, scaling, storage, or network configurations should be made through the Kubernetes API and not directly on these resources.

To prevent changes from being made to the node resource group, you can apply a deny assignment and block users from modifying resources created as part of the AKS cluster.

## Before you begin

Before you begin, you need the following resources installed and configured:

- The Azure CLI version 2.44.0 or later. Run
`az --version`

to find the current version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an AKS cluster with node resource group lockdown

Create a cluster with node resource group lockdown using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with the

`--nrg-lockdown-restriction-level`

flag set to `ReadOnly`

. This configuration allows you to view the resources but not modify them.```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--nrg-lockdown-restriction-level ReadOnly \
--generate-ssh-keys
```


## Update an existing cluster with node resource group lockdown

Update an existing cluster with node resource group lockdown using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--nrg-lockdown-restriction-level`

flag set to `ReadOnly`

. This configuration allows you to view the resources but not modify them.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --nrg-lockdown-restriction-level ReadOnly
```


## Remove node resource group lockdown from a cluster

Remove node resource group lockdown from an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--nrg-restriction-level`

flag set to `Unrestricted`

. This configuration allows you to view and modify the resources.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --nrg-lockdown-restriction-level Unrestricted
```


## Next steps

To learn more about the node resource group in AKS, see [Node resource group](concepts-clusters-workloads#node-resource-group).


---

<!-- DOCUMENTO FUSIONADO: node-pool-unique-subnet.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-pool-unique-subnet -->

# Create node pools with unique subnets in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Certain workloads might require splitting cluster nodes into separate pools for logical isolation. Separate subnets dedicated to each node pool in the cluster can help support this isolation, which can address requirements such as having noncontiguous virtual network address space to split across node pools.

In this article, you learn how to create node pools with unique subnets in Azure Kubernetes Service (AKS).

## Prerequisites

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.35.0 or later. Run`az version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).- An existing AKS cluster with a system node pool. If you need to create one, see
[Create an AKS cluster with a single node pool](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli).

## Limitations

- All subnets assigned to node pools must belong to the same virtual network (VNet).
- System pods must have access to all nodes and pods in the cluster to provide critical functionality, such as DNS resolution and tunneling kubectl logs/exec/port-forward proxy.
- If you expand your VNet after creating the cluster, you must update your cluster before adding a subnet outside the original CIDR block. While AKS errors out on the agent pool add, the
`aks-preview`

Azure CLI extension (version 0.5.66 and higher) now supports running`az aks update`

command with only the required`--resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

arguments. This command performs an update operation without making any changes, which can recover a cluster stuck in a failed state. - In clusters with Kubernetes version less than 1.23.3, kube-proxy SNATs traffic from new subnets, which can cause Azure Network Policy to drop the packets.
- Windows nodes SNAT traffic to the new subnets until the node pool is reimaged.
- Internal load balancers default to one of the node pool subnets.

## Add a node pool with a unique subnet

Add a node pool with a unique subnet into your existing AKS cluster using the

command and the`az aks nodepool add`

`--vnet-subnet-id`

parameter specified.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 3 \ --vnet-subnet-id $SUBNET_RESOURCE_ID`


## Next steps

For more information about node pools in AKS, see [Manage node pools for a cluster in Azure Kubernetes Service (AKS)](manage-node-pools).
