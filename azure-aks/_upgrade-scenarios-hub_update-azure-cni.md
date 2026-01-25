---
merged_at: 2026-01-25T12:25:33.875731
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: upgrade-scenarios-hub.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/upgrade-scenarios-hub -->

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

<!-- DOCUMENTO FUSIONADO: update-azure-cni.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/update-azure-cni -->

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
