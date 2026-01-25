---
merged_at: 2026-01-25T12:25:33.905633
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: vertical-pod-autoscaler-api-reference.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/vertical-pod-autoscaler-api-reference -->

# Vertical Pod Autoscaler API reference

This article provides the API reference for the Vertical Pod Autoscaler feature of Azure Kubernetes Service.

This reference is based on version 0.13.0 of the AKS implementation of VPA.

## VerticalPodAutoscaler

| Name |
Object |
Description |
| metadata |
ObjectMeta |
Standard [object metadata](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#metadata). |
| spec |
VerticalPodAutoscalerSpec |
The desired behavior of the Vertical Pod Autoscaler. |
| status |
VerticalPodAutoscalerStatus |
The most recently observed status of the Vertical Pod Autoscaler. |

## VerticalPodAutoscalerSpec

| Name |
Object |
Description |
| targetRef |
CrossVersionObjectReference |
Reference to the controller managing the set of pods for the autoscaler to control. For example, a Deployment or a StatefulSet. You can point a Vertical Pod Autoscaler at any controller that has a [Scale](https://v1-25.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.25/#scalespec-v1-autoscaling) subresource. Typically, the Vertical Pod Autoscaler retrieves the pod set from the controller's ScaleStatus. |
| updatePolicy |
PodUpdatePolicy |
Specifies whether recommended updates are applied when a pod is started and whether recommended updates are applied during the life of a pod. |
| resourcePolicy |
PodResourcePolicy |
Specifies policies for how CPU and memory requests are adjusted for individual containers. The resource policy can be used to set constraints on the recommendations for individual containers. If not specified, the autoscaler computes recommended resources for all containers in the pod, without additional constraints. |
| recommenders |
VerticalPodAutoscalerRecommenderSelector |
Recommender is responsible for generating recommendation for the VPA object. Leave empty to use the default recommender. Otherwise the list can contain exactly one entry for a user-provided alternative recommender. |

## VerticalPodAutoscalerList

| Name |
Object |
Description |
| metadata |
ObjectMeta |
Standard [object metadata](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#metadata). |
| items |
VerticalPodAutoscaler (array) |
A list of Vertical Pod Autoscaler objects. |

## PodUpdatePolicy

| Name |
Object |
Description |
| updateMode |
string |
A string that specifies whether recommended updates are applied when a pod is started and whether recommended updates are applied during the life of a pod. Possible values are `Off` , `Initial` , `Recreate` , and `Auto` . The default is `Auto` if you don't specify a value. |
| minReplicas |
int32 |
A value representing the minimal number of replicas which need to be alive for Updater to attempt pod eviction (pending other checks like Pod Disruption Budget). Only positive values are allowed. Defaults to global `--min-replicas` flag, which is set to `2` . |

## PodResourcePolicy

| Name |
Object |
Description |
| conainerPolicies |
ContainerResourcePolicy |
An array of resource policies for individual containers. There can be at most one entry for every named container, and optionally a single wildcard entry with `containerName = '*'` , which handles all containers that do not have individual policies. |

## ContainerResourcePolicy

| Name |
Object |
Description |
| containerName |
string |
A string that specifies the name of the container that the policy applies to. If not specified, the policy serves as the default policy. |
| mode |
ContainerScalingMode |
Specifies whether recommended updates are applied to the container when it is started and whether recommended updates are applied during the life of the container. Possible values are `Off` and `Auto` . The default is `Auto` if you don't specify a value. |
| minAllowed |
ResourceList |
Specifies the minimum CPU request and memory request allowed for the container. By default, there is no minimum applied. |
| maxAllowed |
ResourceList |
Specifies the maximum CPU request and memory request allowed for the container. By default, there is no maximum applied. |
| ControlledResources |
[]ResourceName |
Specifies the type of recommendations that are computed (and possibly applied) by the Vertical Pod Autoscaler. If empty, the default of [ResourceCPU, ResourceMemory] is used. |

## VerticalPodAutoscalerRecommenderSelector

| Name |
Object |
Description |
| name |
string |
A string that specifies the name of the recommender responsible for generating recommendation for this object. |

## VerticalPodAutoscalerStatus

| Name |
Object |
Description |
| recommendation |
RecommendedPodResources |
The most recently recommended CPU and memory requests. |
| conditions |
VerticalPodAutoscalerCondition |
An array that describes the current state of the Vertical Pod Autoscaler. |

## RecommendedPodResources

| Name |
Object |
Description |
| containerRecommendation |
RecommendedContainerResources |
An array of resources recommendations for individual containers. |

## RecommendedContainerResources

| Name |
Object |
Description |
| containerName |
string |
A string that specifies the name of the container that the recommendation applies to. |
| target |
ResourceList |
The recommended CPU request and memory request for the container. |
| lowerBound |
ResourceList |
The minimum recommended CPU request and memory request for the container. This amount is not guaranteed to be sufficient for the application to be stable. Running with smaller CPU and memory requests is likely to have a significant impact on performance or availability. |
| upperBound |
ResourceList |
The maximum recommended CPU request and memory request for the container. CPU and memory requests higher than these values are likely to be wasted. |
| uncappedTarget |
ResourceList |
The most recent resource recommendation computed by the autoscaler, based on actual resource usage, not taking into account the **Container Resource Policy**. If actual resource usage causes the target to violate the **Container Resource Policy**, this might be different from the bounded recommendation. This field does not affect actual resource assignment. It is used only as a status indication. |

## VerticalPodAutoscalerCondition

| Name |
Object |
Description |
| type |
VerticalPodAutoscalerConditionType |
The type of condition being described. Possible values are `RecommendationProvided` , `LowConfidence` , `NoPodsMatched` , and `FetchingHistory` . |
| status |
ConditionStatus |
The status of the condition. Possible values are `True` , `False` , and `Unknown` . |
| lastTransitionTime |
Time |
The last time the condition made a transition from one status to another. |
| reason |
string |
The reason for the last transition from one status to another. |
| message |
string |
A human-readable string that gives details about the last transition from one status to another. |

## Next steps

See [Vertical Pod Autoscaler](vertical-pod-autoscaler) to understand how to improve cluster resource utilization and free up CPU and memory for other pods.


---

<!-- DOCUMENTO FUSIONADO: use-node-auto-provisioning.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-node-auto-provisioning -->

# Enable or disable node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to enable or disable node auto-provisioning (NAP) in Azure Kubernetes Service (AKS) using the Azure CLI or Azure Resource Manager (ARM) templates.

If you want to create a NAP-enabled AKS cluster with a custom virtual network (VNet) and subnets, see [Create a node auto-provisioning (NAP) cluster in a custom virtual network](node-auto-provisioning-custom-vnet).

## Before you begin

Before you begin, review the [Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning) article, which details [how NAP works](node-auto-provisioning#how-does-node-auto-provisioning-work), [prerequisites](node-auto-provisioning#prerequisites) and [limitations](node-auto-provisioning#limitations-and-unsupported-features).

## Enable node auto-provisioning (NAP) on an AKS cluster

The following sections explain how to enable NAP on a new or existing AKS cluster:

Note

You can enable [control plane metrics](monitor-control-plane-metrics) to see the logs and operations from [node auto-provisioning](control-plane-metrics-default-list#minimal-ingestion-for-default-off-targets) with the [Azure Monitor managed service for Prometheus add-on](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).

### Enable NAP on a new cluster

Enable node auto-provisioning on a new cluster using the

command with the`az aks create`

`--node-provisioning-mode`

flag set to`Auto`

. The following command also sets the`--network-plugin`

to`azure`

,`--network-plugin-mode`

to`overlay`

, and`--network-dataplane`

to`cilium`

.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --node-provisioning-mode Auto \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --generate-ssh-keys`


Create a file named

`nap.json`

and add the following ARM template configuration with the`properties.nodeProvisioningProfile.mode`

field set to`Auto`

, which enables NAP. (The default setting is`Manual`

.)`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#", "contentVersion": "1.0.0.0", "metadata": {}, "parameters": {}, "resources": [ { "type": "Microsoft.ContainerService/managedClusters", "apiVersion": "2025-05-01", "sku": { "name": "Base", "tier": "Standard" }, "name": "napcluster", "location": "uksouth", "identity": { "type": "SystemAssigned" }, "properties": { "networkProfile": { "networkPlugin": "azure", "networkPluginMode": "overlay", "networkPolicy": "cilium", "networkDataplane":"cilium", "loadBalancerSku": "Standard" }, "dnsPrefix": "napcluster", "agentPoolProfiles": [ { "name": "agentpool", "count": 3, "vmSize": "standard_d2s_v3", "osType": "Linux", "mode": "System" } ], "nodeProvisioningProfile": { "mode": "Auto" } } } ] }`

Enable node auto-provisioning on a new cluster using the

command with the`az deployment group create`

`--template-file`

flag set to the path of the ARM template file.`az deployment group create --resource-group $RESOURCE_GROUP --template-file ./nap.json`


### Enable NAP on an existing cluster

Enable node auto-provisioning on an existing cluster using the

command with the`az aks update`

`--node-provisioning-mode`

flag set to`Auto`

.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --node-provisioning-mode Auto`


## Disable node auto-provisioning (NAP) on an AKS cluster

Important

You can only disable NAP on a cluster if the following conditions are met:

- There are no existing NAP nodes. You can use the
`kubectl get nodes -l karpenter.sh/nodepool`

command to check for existing NAP-managed nodes. - All existing Karpenter
have their`NodePools`

`spec.limits.cpu`

field set to`0`

. This action prevents new nodes from being created, but doesn't disrupt currently running nodes.

Set the

`spec.limits.cpu`

field to`0`

for every existing Karpenter`NodePool`

. For example:`apiVersion: karpenter.sh/v1 kind: NodePool metadata: name: default spec: limits: cpu: 0`

Important

If you don't want to ensure that every pod previously running on a NAP node is safely migrated to a non-NAP node before disabling NAP, you can skip steps 2 and 3 and instead use the

`kubectl delete node`

command for each NAP-managed node. However,**we don't recommend skipping these steps**, as it might leave some pods pending and doesn't honor Pod Disruption Budgets (PDBs).When using the

`kubectl delete node`

command, be careful to only delete NAP-managed nodes. You can identify NAP-managed nodes using the`kubectl get nodes -l karpenter.sh/nodepool`

command.Add the

`karpenter.azure.com/disable:NoSchedule`

taint to every Karpenter`NodePool`

. For example:`apiVersion: karpenter.sh/v1 kind: NodePool metadata: name: default spec: template: spec: ... taints: - key: karpenter.azure.com/disable effect: NoSchedule`

This action starts the process of migrating the workloads on the NAP-managed nodes to non-NAP nodes, honoring PDBs and disruption limits. Pods migrate to non-NAP nodes if they can fit. If there isn't enough fixed-size capacity, some node NAP-managed nodes remain.

Scale up existing fixed-size

`ManagedCluster`

`AgentPools`

or create new fixed-size`AgentPools`

to take the load from the node NAP-managed nodes. As these nodes are added to the cluster, the node NAP-managed nodes are drained, and work is migrated to the fixed-size nodes.Delete all NAP-managed nodes using the

`kubectl get nodes -l karpenter.sh/nodepool`

command. If NAP-managed nodes still exist, the cluster likely lacks fixed-size capacity. In this case, you should add more nodes so the remaining workloads can be migrated.

Update the NAP mode to

`Manual`

using theAzure CLI command with the`az aks update`

`--node-provisioning-mode`

flag set to`Manual`

.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --node-provisioning-mode Manual`


Update the

`properties.nodeProvisioningProfile.mode`

field to`Manual`

in your ARM template and redeploy it.`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#", "contentVersion": "1.0.0.0", "metadata": {}, "parameters": {}, "resources": [ { "type": "Microsoft.ContainerService/managedClusters", "apiVersion": "2025-05-01", "sku": { "name": "Base", "tier": "Standard" }, "name": "napcluster", "location": "uksouth", "identity": { "type": "SystemAssigned" }, "properties": { "networkProfile": { "networkPlugin": "azure", "networkPluginMode": "overlay", "networkPolicy": "cilium", "networkDataplane":"cilium", "loadBalancerSku": "Standard" }, "dnsPrefix": "napcluster", "agentPoolProfiles": [ { "name": "agentpool", "count": 3, "vmSize": "standard_d2s_v3", "osType": "Linux", "mode": "System" } ], "nodeProvisioningProfile": { "mode": "Manual" } } } ] }`


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:
