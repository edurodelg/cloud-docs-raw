---
merged_at: 2026-01-25T12:25:33.852172
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: generation-2-vm.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/generation-2-vm -->

# Use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS), including how to check available Gen 2 VM sizes, create AKS node pools with Gen 2 VMs, migrate from Gen 1 to Gen 2 VMs on AKS, and verify the VM generation of your AKS nodes.

## Before you begin

- Review the
[Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)](aks-virtual-machine-sizes)article to understand VM generations and features supported on AKS.

## Check available Gen 2 VM sizes

Check available Gen 2 VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
# Set environment variables
export LOCATION=<your-region>
export VM_SIZE=<vm-size-to-check>
# Check if the VM size is available in the specified location
az vm list-skus --location $LOCATION --size $VM_SIZE --output table
```


For a breakdown of what VM sizes support Gen 2, see [Support for Gen 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## Create a node pool with a Gen 2 VM

By default, Linux uses the Gen 2 node image unless the VM size doesn't support Gen 2.

Create a Linux node pool with a Gen 2 VM using the default [node pool creation](create-node-pools) process.

## Migrate an existing node pool to Gen 2

If you're using a VM size that only supports Gen 1, you can update your node pool to a VM size that supports Gen 2 using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. This update changes your node image from Gen 1 to Gen 2.

```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
export VM_SIZE=<supported-generation-2-vm-size>
# Update a Linux node pool to use a Gen 2 VM
az aks nodepool update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --node-vm-size $VM_SIZE --os-type Linux
```


## Check if you're using a Gen 2 node image

Verify a successful node pool creation using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and check that the

`nodeImageVersion`

contains `gen2`

in the output.```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
# Show node pool details
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --output table
```


## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)


---

<!-- DOCUMENTO FUSIONADO: generation-2-vms.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/generation-2-vms -->

# Use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use Generation 2 (Gen 2) virtual machines (VMs) on Azure Kubernetes Service (AKS), including how to check available Gen 2 VM sizes, create AKS node pools with Gen 2 VMs, migrate from Gen 1 to Gen 2 VMs on AKS, and verify the VM generation of your AKS nodes.

## Before you begin

- Review the
[Virtual machine (VM) sizes, generations, and features for Azure Kubernetes Service (AKS)](aks-virtual-machine-sizes)article to understand VM generations and features supported on AKS.

## Check available Gen 2 VM sizes

Check available Gen 2 VM sizes using the [ az vm list-skus](/en-us/cli/azure/vm#az-vm-list-skus) command.

```
# Set environment variables
export LOCATION=<your-region>
export VM_SIZE=<vm-size-to-check>
# Check if the VM size is available in the specified location
az vm list-skus --location $LOCATION --size $VM_SIZE --output table
```


For a breakdown of what VM sizes support Gen 2, see [Support for Gen 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2).

## Create a node pool with a Gen 2 VM

By default, Linux uses the Gen 2 node image unless the VM size doesn't support Gen 2.

Create a Linux node pool with a Gen 2 VM using the default [node pool creation](create-node-pools) process.

## Migrate an existing node pool to Gen 2

If you're using a VM size that only supports Gen 1, you can update your node pool to a VM size that supports Gen 2 using the [ az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update) command. This update changes your node image from Gen 1 to Gen 2.

```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
export VM_SIZE=<supported-generation-2-vm-size>
# Update a Linux node pool to use a Gen 2 VM
az aks nodepool update --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --node-vm-size $VM_SIZE --os-type Linux
```


## Check if you're using a Gen 2 node image

Verify a successful node pool creation using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and check that the

`nodeImageVersion`

contains `gen2`

in the output.```
# Set environment variables
export RESOURCE_GROUP=<resource-group-name>
export CLUSTER_NAME=<cluster-name>
export NODE_POOL_NAME=<node-pool-name>
# Show node pool details
az aks nodepool show --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --name $NODE_POOL_NAME --output table
```


## Next steps

- To learn more about Gen 2 VMs, see
[Support for Generation 2 VMs on Azure](/en-us/azure/virtual-machines/generation-2) - To learn more about supported Gen 2 node images, see
[Node images](node-images)
