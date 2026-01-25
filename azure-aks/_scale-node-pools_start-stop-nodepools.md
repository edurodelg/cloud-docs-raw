---
merged_at: 2026-01-25T12:06:27.682867
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: scale-node-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/scale-node-pools -->

# Scale node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your application workload demands change, you might need to scale the number of nodes in a node pool in Azure Kubernetes Service (AKS). In this article, you learn how to manually and automatically scale node pools in AKS.

## Prerequisites for AKS node pool scaling

- An existing AKS cluster with at least one node pool. If you need to create one, see
[Create an AKS cluster with node pools](create-node-pools). - You need the Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Scale a node pool manually

Scale the number of nodes in a node pool using the [

`az aks nodepool scale`

][az-aks-nodepool-scale] command. The`--node-count`

flag specifies the desired number of nodes in the node pool. In this example, the node pool is scaled to five nodes.`az aks nodepool scale \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --node-count 5 \ --no-wait`

Check the status of your node pools using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name>`

The following example output shows the node pool is in the

*Scaling*state with a new count of five nodes:`[ { ... "count": 5, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Scaling", ... "vmSize": "Standard_DS2_v2", ... }, { ... "count": 2, ... "name": "<node-pool-name-2>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Succeeded", ... "vmSize": "Standard_DS2_v2", ... } ]`

It takes a few minutes for the scale operation to complete. After the scale operation is complete, the node pool's

`provisioningState`

changes to*Succeeded*.

## Scale a node pool automatically with the cluster autoscaler

You can use the [cluster autoscaler](cluster-autoscaler-overview) with multiple node pools, and you can enable it on individual node pools and pass unique autoscaling rules to them.

Enable the cluster autoscaler on an existing node pool using the [

`az aks nodepool update`

][az-aks-nodepool-update] command with the`--update-cluster-autoscaler`

flag. The`--min-count`

and`--max-count`

flags specify the minimum and maximum number of nodes in the node pool. In this example, the cluster autoscaler is enabled with a minimum count of one node and a maximum count of five nodes:`az aks nodepool update \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --update-cluster-autoscaler \ --min-count 1 \ --max-count 5`


Note

If you want to disable the cluster autoscaler on a node pool, use the [`az aks nodepool update`

][az-aks-nodepool-update] command with the `--disable-cluster-autoscaler`

flag instead of `--update-cluster-autoscaler`

.

## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).


---

<!-- DOCUMENTO FUSIONADO: start-stop-nodepools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/start-stop-nodepools -->

# Start and stop an Azure Kubernetes Service (AKS) node pool

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might not need to continuously run your AKS workloads. For example, you might have a development cluster that has node pools running specific workloads. To optimize your compute costs, you can completely stop your node pools in your AKS cluster.

## Features and limitations

- You can't stop system pools.
- Spot node pools are supported.
- Stopped node pools can be upgraded.
- The cluster and node pool must be running.
- You can't stop node pools from clusters which use the
[Node Autoprovisioning (NAP)](node-autoprovision)feature.

Tip

You can use Azure Copilot to stop and start your node pools in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#start-and-stop-node-pools).

## Before you begin

This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using the [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

## Stop an AKS node pool

Stop a running AKS node pool using the

command.`az aks nodepool stop`

`az aks nodepool stop --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

Verify your node pool stopped using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

The following condensed example output shows the

`powerState`

as`Stopped`

:`{ [...] "osType": "Linux", "podSubnetId": null, "powerState": { "code": "Stopped" }, "provisioningState": "Succeeded", "proximityPlacementGroupId": null, [...] }`

Note

If the

`provisioningState`

shows`Stopping`

, your node pool is still in the process of stopping.Note

Stopping the node pool will stop its Cluster Autoscaler, and starts it back when starting the node pool. So if you manually modify the number of VMSS instances in the pool while it's stopped, Cluster Autoscaler might show inconsistencies.


## Start a stopped AKS node pool

Restart a stopped node pool using the

command.`az aks nodepool start`

`az aks nodepool start --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

Verify your node pool started using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

The following condensed example output shows the

`powerState`

as`Running`

:`{ [...] "osType": "Linux", "podSubnetId": null, "powerState": { "code": "Running" }, "provisioningState": "Succeeded", "proximityPlacementGroupId": null, [...] }`

Note

If the

`provisioningState`

shows`Starting`

, your node pool is still in the process of starting.

## Next steps

- To learn how to scale
`User`

pools to 0, see[scale](scale-cluster#scale-user-node-pools-to-0).`User`

pools to 0 - To learn how to stop your cluster, see
[cluster start/stop](start-stop-cluster). - To learn how to save costs using Spot instances, see
[add a spot node pool to AKS](spot-node-pool). - To learn more about the AKS support policies, see
[AKS support policies](support-policies).
