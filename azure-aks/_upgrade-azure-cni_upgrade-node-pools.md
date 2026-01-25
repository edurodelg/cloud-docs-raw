---
merged_at: 2026-01-25T12:25:33.876753
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: upgrade-azure-cni.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-azure-cni -->

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

<!-- DOCUMENTO FUSIONADO: upgrade-node-pools.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-node-pools -->

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
