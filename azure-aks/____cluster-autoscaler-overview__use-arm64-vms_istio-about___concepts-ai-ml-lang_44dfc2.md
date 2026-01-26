---
merged_at: 2026-01-26T20:54:26.175287
merged_files: 2
---


---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __cluster-autoscaler-overview__use-arm64-vms_istio-about___concepts-ai-ml-langua_09e80f.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _cluster-autoscaler-overview__use-arm64-vms_istio-about.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: cluster-autoscaler-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/cluster-autoscaler-overview -->

# Cluster autoscaling in Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To keep up with application demands in Azure Kubernetes Service (AKS), you might need to adjust the number of nodes that run your workloads. The cluster autoscaler component watches for pods in your cluster that can't be scheduled because of resource constraints. When the cluster autoscaler detects unscheduled pods, it scales up the number of nodes in the node pool to meet the application demand. It also regularly checks nodes that don't have any scheduled pods and scales down the number of nodes as needed.

This article helps you understand how the cluster autoscaler works in AKS. It also provides guidance, best practices, and considerations when configuring the cluster autoscaler for your AKS workloads. If you want to enable, disable, or update the cluster autoscaler for your AKS workloads, see [Use the cluster autoscaler in AKS](cluster-autoscaler).

## About the cluster autoscaler

Clusters often need a way to scale automatically to adjust to changing application demands, such as between workdays and evenings or weekends. AKS clusters can scale in the following ways:

- The
**cluster autoscaler**periodically checks for pods that can't be scheduled on nodes because of resource constraints. The cluster then automatically increases the number of nodes. Manual scaling is disabled when you use the cluster autoscaler. For more information, see[How does scale up work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-up-work). - The
uses the Metrics Server in a Kubernetes cluster to monitor the resource demand of pods. If an application needs more resources, the number of pods is automatically increased to meet the demand.[Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler) - The
automatically sets resource requests and limits on containers per workload based on past usage to ensure pods are scheduled onto nodes that have the required CPU and memory resources.[Vertical Pod Autoscaler](vertical-pod-autoscaler)


It's a common practice to enable cluster autoscaler for nodes and either the Vertical Pod Autoscaler or Horizontal Pod Autoscaler for pods. When you enable the cluster autoscaler, it applies the specified scaling rules when the node pool size is lower than the minimum node count, up to the maximum node count. The cluster autoscaler waits to take effect until a new node is needed in the node pool or until a node might be safely deleted from the current node pool. For more information, see [How does scale down work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-down-work)

## Best practices and considerations

When implementing

**availability zones with the cluster autoscaler**, we recommend using a single node pool for each zone. You can set the`--balance-similar-node-groups`

parameter to`True`

to maintain a balanced distribution of nodes across zones for your workloads during scale up operations. When this approach isn't implemented, scale down operations can disrupt the balance of nodes across zones.For

**clusters with more than 400 nodes**, we recommend using Azure CNI or Azure CNI Overlay.To

**effectively run workloads concurrently on both Spot and On-demand node pools**, consider using. This approach allows you to scale out nodepools based on assigned priority. The following configuration illustrates this setup.*priority expanders*`apiVersion: v1 kind: ConfigMap metadata: name: cluster-autoscaler-priority-expander namespace: kube-system data: priorities: |- 10: - .*spotpool1.* - .*spotpool2.* 50: - .*ondemandpool1.*`

Exercise caution when

**assigning CPU/Memory requests on pods**. The cluster autoscaler scales up based on pending pods rather than CPU/Memory pressure on nodes.For

**clusters concurrently hosting both long-running workloads, like web apps, and short/bursty job workloads**, we recommend separating them into distinct node pools with[Affinity Rules](operator-best-practices-advanced-scheduler#node-affinity)/[expanders](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-are-expanders).Use

[PodDisruptionBudget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)to help prevent unnecessary node drain or scale down operations. Specifying the annotation[cluster-autoscaler.kubernetes.io/safe-to-evict: "false"](https://kubernetes.io/docs/reference/labels-annotations-taints/#cluster-autoscaler-kubernetes-io-safe-to-evict)on the Pod spec will also prevent the pods from being evicted. Use this annotation with caution, as it may cause the Cluster Autoscaler encounter issues when draining a node with a running Pod that includes this annotation.In an autoscaler-enabled node pool, scale down nodes by removing workloads, instead of manually reducing the min/ max count of the node pool. This can be problematic if the node pool is already at maximum capacity or if there are active workloads running on the nodes, potentially causing unexpected behavior by the cluster autoscaler.

Nodes don't scale up if pods have a PriorityClass value below -10. Priority -10 is reserved for

[overprovisioning pods](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-can-i-configure-overprovisioning-with-cluster-autoscaler). For more information, see[Using the cluster autoscaler with Pod Priority and Preemption](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-cluster-autoscaler-work-with-pod-priority-and-preemption).**Don't combine other node autoscaling mechanisms**, such as Virtual Machine Scale Set autoscalers, with the cluster autoscaler.The cluster autoscaler

**might be unable to scale down if pods can't move, such as in the following situations**:- A directly created pod not backed by a controller object, such as a Deployment or ReplicaSet.
- A pod disruption budget (PDB) that's too restrictive and doesn't allow the number of pods to fall below a certain threshold.
- A pod uses node selectors or anti-affinity that can't be honored if scheduled on a different node.
For more information, see
[What types of pods can prevent the cluster autoscaler from removing a node?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-types-of-pods-can-prevent-ca-from-removing-a-node).


Important

**Don't make changes to individual nodes within the autoscaled node pools**. All nodes in the same node group should have uniform capacity, labels, taints and system pods running on them.

- The cluster autoscaler isn't responsible for enforcing a "maximum node count" in a cluster node pool irrespective of pod scheduling considerations. If any non-cluster autoscaler actor sets the node pool count to a number beyond the cluster autoscaler's configured maximum, the cluster autoscaler doesn't automatically remove nodes. The cluster autoscaler scale down behaviors remain scoped to removing underutilized nodes. The sole purpose of the cluster autoscaler's max node count configuration is to enforce an upper limit for scale up operations. It doesn't have any effect on scale down considerations.

## Cluster autoscaler profile

The [cluster autoscaler profile](cluster-autoscaler#cluster-autoscaler-profile-settings) is a set of parameters that control the behavior of the cluster autoscaler. You can configure the cluster autoscaler profile when you create a cluster or update an existing cluster.

### Optimizing the cluster autoscaler profile

You should fine-tune the cluster autoscaler profile settings according to your specific workload scenarios while also considering tradeoffs between performance and cost. This section provides examples that demonstrate those tradeoffs.

It's important to note that the cluster autoscaler profile settings are cluster-wide and applied to all autoscale-enabled node pools. Any scaling actions that take place in one node pool can affect the autoscaling behavior of other node pools, which can lead to unexpected results. Make sure you apply consistent and synchronized profile configurations across all relevant node pools to ensure you get your desired results.

#### Example 1: Optimizing for performance

For clusters that handle substantial and bursty workloads with a primary focus on performance, we recommend increasing the `scan-interval`

and decreasing the `scale-down-utilization-threshold`

. These settings help batch multiple scaling operations into a single call, optimizing scaling time and the utilization of compute read/write quotas. It also helps mitigate the risk of swift scale down operations on underutilized nodes, enhancing the pod scheduling efficiency. Also increase `ok-total-unready-count`

and `max-total-unready-percentage`

.

For clusters with daemonset pods, we recommend setting `ignore-daemonsets-utilization`

to `true`

, which effectively ignores node utilization by daemonset pods and minimizes unnecessary scale down operations. See [profile for bursty workloads](cluster-autoscaler#configure-cluster-autoscaler-profile-for-bursty-workloads)

#### Example 2: Optimizing for cost

If you want a [cost-optimized profile](cluster-autoscaler#configure-cluster-autoscaler-profile-for-aggressive-scale-down), we recommend setting the following parameter configurations:

- Reduce
`scale-down-unneeded-time`

, which is the amount of time a node should be unneeded before it's eligible for scale down. - Reduce
`scale-down-delay-after-add`

, which is the amount of time to wait after a node is added before considering it for scale down. - Increase
`scale-down-utilization-threshold`

, which is the utilization threshold for removing nodes. - Increase
`max-empty-bulk-delete`

, which is the maximum number of nodes that can be deleted in a single call. - Set
`skip-nodes-with-local-storage`

to false. - Increase
`ok-total-unready-count`

and`max-total-unready-percentage`

.

## Common issues and mitigation recommendations

View scaling failures and scale-up not triggered events via [CLI or Portal](cluster-autoscaler#retrieve-cluster-autoscaler-logs-and-status).

### Not triggering scale up operations

| Common causes | Mitigation recommendations |
|---|---|
| PersistentVolume node affinity conflicts, which can arise when using the cluster autoscaler with multiple availability zones or when a pod's or persistent volume's zone differs from the node's zone. | Use one node pool per availability zone and enabling `--balance-similar-node-groups` . You can also set the
`volumeBindingMode` field to `WaitForFirstConsumer` |
| Taints and Tolerations/Node affinity conflicts | Assess the taints assigned to your nodes and review the tolerations defined in your pods. If necessary, make adjustments to the
|

### Scale up operation failures

| Common causes | Mitigation recommendations |
|---|---|
| IP address exhaustion in the subnet | Add another subnet in the same virtual network and add another node pool into the new subnet. |
| Core quota exhaustion | Approved core quota has been exhausted.
|

[429 Too Many Requests errors](/en-us/troubleshoot/azure/azure-kubernetes/429-too-many-requests-errors).### Scale down operation failures

| Common causes | Mitigation recommendations |
|---|---|
| Pod preventing node drain/Unable to evict pod | • View
• For pods using local storage, such as hostPath and emptyDir, set the cluster autoscaler profile flag `skip-nodes-with-local-storage` to `false` . • In the pod specification, set the `cluster-autoscaler.kubernetes.io/safe-to-evict` annotation to `true` . • Check your
|

[429 Too Many Requests errors](/en-us/troubleshoot/azure/azure-kubernetes/429-too-many-requests-errors).[fully managed AKS resource group](cluster-configuration#fully-managed-resource-group-preview)(see[AKS support policies](support-policies)). Remove or reset any[resource locks](/en-us/azure/azure-resource-manager/management/lock-resources)you previously applied to the resource group.### Other issues

| Common causes | Mitigation recommendations |
|---|---|
| PriorityConfigMapNotMatchedGroup | Make sure that you add all the node groups requiring autoscaling to the
|

### Node pool in backoff

Node pool in backoff was introduced in version 0.6.2 and causes the cluster autoscaler to back off from scaling a node pool after a failure.

Depending on how long the scaling operations have been experiencing failures, it may take up to 30 minutes before making another attempt. You can reset the node pool's backoff state by disabling and then re-enabling autoscaling.


---

<!-- DOCUMENTO FUSIONADO: _use-arm64-vms_istio-about.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: use-arm64-vms.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-arm64-vms -->

# Use Arm-based processor (Arm64) Virtual Machines (VMs) in an Azure Kubernetes Service (AKS) cluster for cost effectiveness

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview) are power-efficient and cost-effective, but don't compromise on performance. These Arm64 VMs are engineered to efficiently run dynamic, scalable workloads and can deliver up to 50% better price-performance than comparable x86-based VMs for scale-out workloads.

Because of their ability to scale workloads efficiently, Arm64 VMs are well-suited for web or application servers, open-source databases, cloud-native applications, gaming servers, and other high traffic applications.

Note

While a combination of CPU, memory, and networking capacity configurations heavily influences the cost effectiveness of a SKU, Arm64 VM types are recommended for cost optimization.

In this article, you'll learn how to add a Arm64 VM to an existing node pool.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

Before you begin, make sure you have:

## Limitations

- Arm64 VMs aren't supported for Windows node pools.
- Existing node pools can't be updated to use an Arm64 VM.
- Federal Information Process Standard (FIPS)-enabled node pools are only supported with Arm64 SKUs when using Azure Linux 3.0+.
- Arm64 node pools aren't supported on Defender-enabled clusters with Kubernetes version 1.29.0 or lower.

## Create node pools with Arm64 VMs

The Arm64 processor provides low power compute for your Kubernetes workloads. Arm64 virtual machines can be added to existing clusters even mixing Intel and Arm architecture node pools within a cluster. To create an Arm64 node pool, you need to choose a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series), [Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or [Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series) series virtual machine.

### Add a node pool with an Arm64 VM

Use [ az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) to add a node pool with an Arm64 VM to an existing cluster. Alternatively, if you're using

[Azure Linux 3.0+](/en-us/azure/azure-linux/how-to-enable-azure-linux-3), you can add a node pool with an Arm64 VM and

[FIPS](enable-fips-nodes)enabled.

Add a node pool with an Arm64 VM

`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --node-count 3 \ --node-vm-size Standard_D2pds_v5`

Add a FIPS-enabled node pool with an Arm64 VM

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use the

with`az aks nodepool add`

`--enable-fips-image`

and`--os-sku`

parameters.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $ARM_NODE_POOL_NAME \ --os-sku AzureLinux --enable-fips-image --kubernetes-version 1.31 --node-count 3 \ --node-vm-size Standard_D2pds_v5`

For more information on verifying FIPS enablement and disabling FIPS, see

[Enable FIPS node pools](enable-fips-nodes).- Node pools with Arm64 VMs and
Update a node pool with an Arm64 VM to enable FIPS

Limitations:

- Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)enabled aren't supported with Ubuntu OS. - Node pools with Arm64 VMs and
[FIPS](enable-fips-nodes)require kubernetes version 1.31+.

Use

command with the`az aks nodepool update`

`--enable-fips-image`

parameter to enable FIPS on an existing node pool.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

- Node pools with Arm64 VMs and

For more information on verifying FIPS enablement and disabling FIPS, see [Enable FIPS node pools](enable-fips-nodes).

## Verify the node pool uses Arm64

Verify a node pool uses Arm64 using the [ az aks nodepool show](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-show) command and verify the

`vmSize`

is a [Dpsv5](/en-us/azure/virtual-machines/dpsv5-dpdsv5-series),

[Dplsv5](/en-us/azure/virtual-machines/dplsv5-dpldsv5-series), or

[Epsv5](/en-us/azure/virtual-machines/epsv5-epdsv5-series)series.

```
az aks nodepool show \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name mynodepool \
--query vmSize
```


The following example output shows the node pool uses Arm64:

```
"Standard_D2pds_v5"
```


## Next steps

In this article, you learned how to add a node pool with an Arm64 VM to an AKS cluster.

- For more recommendations for cost savings, see
[Best practices for cost optimization in Azure Kubernetes Service (AKS)](best-practices-cost). - For more information about Arm64, see
[Cobalt Arm-based processors (Arm64)](/en-us/azure/virtual-machines/sizes/cobalt-overview). - For more information on verifying FIPS enablement and disabling FIPS, see
[Enable FIPS node pools](enable-fips-nodes). - For Azure Linux 3.0 enablement and support details, see
[Enable Azure Linux 3.0](/en-us/azure/azure-linux/how-to-enable-azure-linux-3).


---

<!-- DOCUMENTO FUSIONADO: istio-about.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-about -->

# Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Istio](https://istio.io/latest/) addresses the challenges developers and operators face with a distributed or microservices architecture. The Istio-based service mesh add-on provides an officially supported and tested integration for Azure Kubernetes Service (AKS).

## What is a Service Mesh?

Modern applications are typically architected as distributed collections of microservices, with each collection of microservices performing some discrete business function. A service mesh is a dedicated infrastructure layer that you can add to your applications. It allows you to transparently add capabilities like observability, traffic management, and security, without adding them to your own code. The term **service mesh** describes both the type of software you use to implement this pattern, and the security or network domain that is created when you use that software.

As the deployment of distributed services, such as in a Kubernetes-based system, grows in size and complexity, it can become harder to understand and manage. You may need to implement capabilities such as discovery, load balancing, failure recovery, metrics, and monitoring. A service mesh can also address more complex operational requirements like A/B testing, canary deployments, rate limiting, access control, encryption, and end-to-end authentication.

Service-to-service communication is what makes a distributed application possible. Routing this communication, both within and across application clusters, becomes increasingly complex as the number of services grow. Istio helps reduce this complexity while easing the strain on development teams.

## What is Istio?

Istio is an open-source service mesh that layers transparently onto existing distributed applications. Istio’s powerful features provide a uniform and more efficient way to secure, connect, and monitor services. Istio enables load balancing, service-to-service authentication, and monitoring – with few or no service code changes. Its powerful control plane brings vital features, including:

- Secure service-to-service communication in a cluster with TLS (Transport Layer Security) encryption, strong identity-based authentication, and authorization.
- Automatic load balancing for HTTP, gRPC, WebSocket, and TCP traffic.
- Fine-grained control of traffic behavior with rich routing rules, retries, failovers, and fault injection.
- A pluggable policy layer and configuration API supporting access controls, rate limits, and quotas.
- Automatic metrics, logs, and traces for all traffic within a cluster, including cluster ingress and egress.

## How is the add-on different from open-source Istio?

This service mesh add-on uses and builds on top of open-source Istio. The add-on flavor provides the following extra benefits:

- Istio versions are tested and verified to be compatible with supported versions of Azure Kubernetes Service.
- Microsoft handles scaling and configuration of Istio control plane
- Microsoft adjusts scaling of AKS components like
`coredns`

when Istio is enabled. - Microsoft provides managed lifecycle (upgrades) for Istio components when triggered by user.
- Verified external and internal ingress set-up.
- Verified to work with
[Azure Monitor managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)and[Azure Managed Grafana](/en-us/azure/managed-grafana/overview). - Official Azure support provided for the add-on.

## Limitations

Istio-based service mesh add-on for AKS has the following limitations:

- The add-on doesn't work on AKS clusters that are using
[Open Service Mesh addon for AKS](open-service-mesh-about). - The add-on doesn't work on AKS clusters with self-managed installations of Istio.
- The add-on doesn't support adding pods associated with virtual nodes to be added under the mesh.
- The add-on doesn't yet support the sidecar-less Ambient mode. Microsoft is currently contributing to Ambient workstream under Istio open source. Product integration for Ambient mode is on the roadmap and is being continuously evaluated as the Ambient workstream evolves.
- The add-on doesn't yet support multi-cluster deployments.
- The add-on doesn't yet support Windows Server containers. Windows Server containers aren't yet supported in open source Istio right now. Issue tracking this feature ask can be found
[here](https://github.com/istio/istio/issues/27893). - Customization of mesh through the following custom resources is currently blocked -
`ProxyConfig, WorkloadEntry, WorkloadGroup, IstioOperator, WasmPlugin`

. - While the add-on allows the use of
`EnvoyFilter`

's, issues arising from them (for example from the Lua script or from the compression library) are outside the support scope of the Istio add-on. See the[support policy document](istio-support-policy#allowed-supported-and-blocked-customizations)for more information about the support categories for Istio add-on features and configuration options. - Gateway API for Istio ingress gateway or managing mesh traffic (GAMMA) is currently not yet supported with Istio add-on. However, Gateway API for Istio ingress traffic management is currently under active development for the add-on. While the add-on supports
[annotation and](istio-deploy-ingress#ingress-gateway-service-customizations), port or protocol configuration is currently not supported.`externalTrafficPolicy`

customization for the Istio ingress gateways - The add-on supports customization of a subset of the fields in
[MeshConfig](https://istio.io/latest/docs/reference/config/istio.mesh.v1alpha1/). Other customizations may be allowed but unsupported or disallowed entirely, as detailed[here](istio-meshconfig#allowed-supported-and-blocked-meshconfig-values).

## Feedback and feature ask

Feedback and feature ask for the Istio add-on can be provided by creating [issues with label 'service-mesh' on AKS GitHub repository](https://github.com/Azure/AKS/issues?q=is%3Aopen+is%3Aissue+label%3Aservice-mesh).


---

<!-- DOCUMENTO FUSIONADO: __concepts-ai-ml-language-models_use-advanced-container-networking-services__red_248d00.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _concepts-ai-ml-language-models_use-advanced-container-networking-services.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: concepts-ai-ml-language-models.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-ai-ml-language-models -->

# Concepts - Small and large language models

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about small and large language models, including when to use them and how you can use them with your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## What are language models?

Language models are powerful machine learning models used for natural language processing (NLP) tasks, such as text generation and sentiment analysis. These models represent natural language based on the probability of words or sequences of words occurring in a given context.

*Conventional language models* have been used in supervised settings for research purposes where the models are trained on well-labeled text datasets for specific tasks. *Pre-trained language models* offer an accessible way to get started with AI and have become more widely used in recent years. These models are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks.

The size of a language model is determined by its number of parameters, or *weights*, that determine how the model processes input data and generates output. Parameters are learned during the training process by adjusting the weights within layers of the model to minimize the difference between the model's predictions and the actual data. The more parameters a model has, the more complex and expressive it is, but also the more computationally expensive it is to train and use.

In general, **small language models** have *fewer than 10 billion parameters*, and **large language models** have *more than 10 billion parameters*. For example, the new Microsoft Phi-3 model family has three versions with different sizes: mini (3.8 billion parameters), small (7 billion parameters), and medium (14 billion parameters).

## When to use small language models

### Advantages

Small language models are a good choice if you want models that are:

**Faster and more cost-effective to train and run**: They require less data and compute power.**Easy to deploy and maintain**: They have smaller storage and memory footprints.**Less prone to**, which is when a model learns the noise or specific patterns of the training data and fails to generalize new data.*overfitting***Interpretable and explainable**: They have fewer parameters and components to understand and analyze.

### Use cases

Small language models are suitable for use cases that require:

**Limited data or resources**, and you need a quick and simple solution.**Well-defined or narrow tasks**, and you don't need much creativity in the output.**High-precision and low-recall tasks**, and you value accuracy and quality over coverage and quantity.**Sensitive or regulated tasks**, and you need to ensure the transparency and accountability of the model.

The following table lists some popular, high-performance small language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-mini (3.8 billion), Phi-3-small (7 billion) | MIT license |
| Microsoft Phi-2 | Phi-2 (2.7 billion) | MIT license |
| Falcon | Falcon-7B (7 billion) | Apache 2.0 license |

## When to use large language models

### Advantages

Large language models are a good choice if you want models that are:

**Powerful and expressive**: They can capture more complex patterns and relationships in the data.**General and adaptable**: They can handle a wider range of tasks and transfer knowledge across domains.**Robust and consistent**: They can handle noisy or incomplete inputs and avoid common errors and biases.

### Use cases

Large language models are suitable for use cases that require:

**Abundant data and resources**, and you have the budget to build and maintain a complex solution.**Low-precision and high-recall tasks**, and you value coverage and quantity over accuracy and quality.**Challenging or exploratory tasks**, and you want to leverage the model's capacity to learn and adapt.

The following table lists some popular, high-performance large language models:

| Model family | Model sizes (Number of parameters) | Software license |
|---|---|---|
| Microsoft Phi-3 | Phi-3-medium (14 billion) | MIT license |
| Falcon | Falcon-40B (40 billion) | Apache 2.0 license |

## Experiment with small and large language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The KAITO add-on for AKS simplifies onboarding and reduces the time-to-inference for open-source models on your AKS clusters. The add-on automatically provisions right-sized GPU nodes and sets up the associated interference server as an endpoint server to your chosen model.

For more information, see [Deploy an AI model on AKS with the AI toolchain operator](ai-toolchain-operator). To get started with a range of supported small and large language models for your inference workflows, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:


---

<!-- DOCUMENTO FUSIONADO: use-advanced-container-networking-services.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/use-advanced-container-networking-services -->

# Use Advanced Container Networking Services on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to enable and disable Advanced Container Networking Services, including [Container Network Observability](advanced-container-networking-services-overview#container-network-observability) and [Container Network Security](advanced-container-networking-services-overview#container-network-security), on your AKS clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Azure CLI version 2.71.0 or higher. Find your version using the
`az --version`

command. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). [Install the](#install-the-aks-preview-azure-cli-extension)version`aks-preview`

Azure CLI extension`14.0.0b6`

or higher.[Register the](#register-the-advancednetworkingl7policypreview-feature-flag)in your subscription.`AdvancedNetworkingL7PolicyPreview`

feature flag- Clusters that have the Cilium data plane support
*Container Network Observability*and*Container Network Security*in Kubernetes version 1.29 and later.

## Install the `aks-preview`

Azure CLI extension

Install or update the Azure CLI preview extension using the

or`az extension add`

command.`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the extension to make sure you have the latest version installed az extension update --name aks-preview`


## Register the `AdvancedNetworkingL7PolicyPreview`

feature flag

Register the

`AdvancedNetworkingL7PolicyPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`

Registration takes a few minutes to complete.

Verify successful registration using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingL7PolicyPreview"`


## Set environment variables

The examples in this article use the following environment variables:

| Variable | Description | Example value |
|---|---|---|
`RESOURCE_GROUP` |
Name of the Azure resource group | `myResourceGroup` |
`LOCATION` |
Azure region for resources | `eastus` |
`CLUSTER_NAME` |
Name of the AKS cluster | `myAKSCluster` |

**All commands in this article assume these environment variables are set**. Make sure to replace the example values with your own values.

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a new AKS cluster with Advanced Container Networking Services

Note

When the `--acns-advanced-networkpolicies`

parameter is set to `L7`

, both Layer 7 and fully qualified domain name (FQDN) filtering policies are enabled. If you want to enable only FQDN filtering, set the parameter to `FQDN`

.

Create an AKS cluster with Advanced Container Networking Services and Cilium using the

command with the`az aks create`

`--enable-acns`

and`--network-dataplane cilium`

flags.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --kubernetes-version 1.29 \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Important

The [Container Network Security](advanced-container-networking-services-overview#container-network-security) feature isn't available for non-Cilium clusters.

Create an AKS cluster with Advanced Container Networking Services using the

command with the`az aks create`

`--enable-acns`

flag.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --network-plugin azure \ --network-plugin-mode overlay \ --enable-acns`


## Enable Advanced Container Networking Services on an existing cluster

Enable Advanced Container Networking Services on an existing AKS cluster with Cilium using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --acns-advanced-networkpolicies <L7/FQDN>`


Enable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--enable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns`


## Disable Advanced Container Networking Services on an AKS cluster

Disable Advanced Container Networking Services on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Observability on an AKS cluster

Disable the Container Network Observability feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-observability`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-observability`


Container Network Observability is the only feature available for non-Cilium clusters, so you can disable it only by disabling the entire Advanced Container Networking Services suite.

Disable the Container Network Observability feature on an existing AKS cluster using the

command with the`az aks update`

`--disable-acns`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --disable-acns`


## Disable Container Network Security on an AKS cluster

Disable the Container Network Security feature without affecting other Advanced Container Networking Services features using the

command with the`az aks update`

`--disable-acns-security`

flag.`az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-acns \ --disable-acns-security`


---

<!-- DOCUMENTO FUSIONADO: _reduce-latency-ppg_customize-resource-configuration.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: reduce-latency-ppg.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/reduce-latency-ppg -->

# Use proximity placement groups to reduce latency for Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

When using proximity placement groups on AKS, colocation only applies to the agent nodes. Node to node and the corresponding hosted pod to pod latency is improved. The colocation doesn't affect the placement of a cluster's control plane.

When deploying your application in Azure, you can create network latency by spreading virtual machine (VM) instances across regions or availability zones, which may impact the overall performance of your application. A proximity placement group is a logical grouping used to make sure Azure compute resources are physically located close to one another. Some applications, such as gaming, engineering simulations, and high-frequency trading (HFT) require low latency and tasks that can complete quickly. For similar high-performance computing (HPC) scenarios, consider using [proximity placement groups (PPG)](/en-us/azure/virtual-machines/co-location#proximity-placement-groups) for your cluster's node pools.

## Before you begin

This article requires Azure CLI version 2.14 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Limitations

- A proximity placement group can map to only
*one*availability zone. - A node pool must use Virtual Machine Scale Sets to associate a proximity placement group.
- A node pool can associate a proximity placement group at node pool create time only.

## Node pools and proximity placement groups

The first resource you deploy with a proximity placement group attaches to a specific data center. Any extra resources you deploy with the same proximity placement group are colocated in the same data center. Once all resources using the proximity placement group are stopped (deallocated) or deleted, it's no longer attached.

- You can associate multiple node pools with a single proximity placement group.
- You can only associate a node pool with a single proximity placement group.

### Configure proximity placement groups with availability zones

Note

While proximity placement groups require a node pool to use only *one* availability zone, the [baseline Azure VM SLA of 99.9%](https://azure.microsoft.com/support/legal/sla/virtual-machines/v1_9/) is still in effect for VMs in a single zone.

Proximity placement groups are a node pool concept and associated with each individual node pool. Using a PPG resource has no impact on AKS control plane availability, which can impact how you should design your cluster with zones. To ensure a cluster is spread across multiple zones, we recommend using the following design:

- Provision a cluster with the first system pool using
*three*zones and no proximity placement group associated to ensure the system pods land in a dedicated node pool, which spreads across multiple zones. - Add extra user node pools with a unique zone and proximity placement group associated to each pool. An example is
*nodepool1*in zone one and PPG1,*nodepool2*in zone two and PPG2, and*nodepool3*in zone 3 with PPG3. This configuration ensures that, at a cluster level, nodes are spread across multiple zones and each individual node pool is colocated in the designated zone with a dedicated PPG resource.

## Create a new AKS cluster with a proximity placement group

Accelerated networking greatly improves networking performance of virtual machines. Ideally, use proximity placement groups with accelerated networking. By default, AKS uses accelerated networking on [supported virtual machine instances](/en-us/azure/virtual-network/accelerated-networking-overview?toc=/azure/virtual-machines/linux/toc.json#limitations-and-constraints), which include most Azure virtual machine with two or more vCPUs.

Create an Azure resource group using the

command.`az group create`

`az group create --name myResourceGroup --location centralus`

Create a proximity placement group using the

command. Make sure to note the ID value in the output.`az ppg create`

`az ppg create --name myPPG --resource-group myResourceGroup --location centralus --type standard`

The command produces an output similar to the following example output, which includes the

*ID*value you need for upcoming CLI commands.`{ "availabilitySets": null, "colocationStatus": null, "id": "/subscriptions/yourSubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.Compute/proximityPlacementGroups/myPPG", "location": "centralus", "name": "myPPG", "proximityPlacementGroupType": "Standard", "resourceGroup": "myResourceGroup", "tags": {}, "type": "Microsoft.Compute/proximityPlacementGroups", "virtualMachineScaleSets": null, "virtualMachines": null }`

Create an AKS cluster using the

command and replace the`az aks create`

*myPPGResourceID*value with your proximity placement group resource ID from the previous step.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --ppg myPPGResourceID --generate-ssh-keys`


## Add a proximity placement group to an existing cluster

You can add a proximity placement group to an existing cluster by creating a new node pool. You can then optionally migrate existing workloads to the new node pool and delete the original node pool.

Use the same proximity placement group that you created earlier to ensure agent nodes in both node pools in your AKS cluster are physically located in the same data center.

Create a new node pool using the

command and replace the`az aks nodepool add`

*myPPGResourceID*value with your proximity placement group resource ID.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name mynodepool \ --node-count 1 \ --ppg myPPGResourceID`


## Clean up

Delete the Azure resource group along with its resources using the

command.`az group delete`

`az group delete --name myResourceGroup --yes --no-wait`


## Next steps

Learn more about [proximity placement groups](/en-us/azure/virtual-machines/co-location#proximity-placement-groups).


---

<!-- DOCUMENTO FUSIONADO: customize-resource-configuration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/customize-resource-configuration -->

# Customize the resource configuration for managed add-ons

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides an overview of how to customize the resource configuration for Azure Kubernetes Service (AKS) managed add-ons with [cost optimized add-on scaling (Preview)](optimized-addon-scaling).

## Overview

Enabling the cost optimized add-on scaling feature in your AKS cluster installs the Vertical Pod Autoscaler (VPA) add-on and VPA custom resources for AKS managed add-ons that support this capability. This feature also allows you to manually customize the resource CPU and memory requests and limits in Deployments and DaemonSets. You can also customize the maximum and minimum allowed CPU and memory and the VPA update mode within VPA custom resources.

## Prerequisites

- Review the
[supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons)and[limitations](optimized-addon-scaling)for this feature. - You need an AKS cluster enabled with the cost optimized add-on scaling feature. If you don't have one, see
[Enable cost optimized add-on scaling on your AKS cluster (Preview)](optimized-addon-scaling).

## Customize resource annotations

| Annotation | Description | Values |
|---|---|---|
`kubernetes.azure.com/override-requests-limits` |
Supports the capability to customize the container resource CPU/memory requests/limits in a Deployment or DaemonSet if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-min-max` |
Supports the capability to customize the container policy maximum/minimum allowed CPU/memory value in VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. | "enabled" or "disabled" |
`kubernetes.azure.com/override-update-mode` |
Supports the capability to customize the update policy `updateMode` value in a VPA custom resource if the value is "enabled". Set the value to "disabled" to reset to AKS defaults. |
"enabled" or "disabled" |

## Customize resource CPU/memory requests/limits

After setting the `kubernetes.azure.com/override-requests-limits`

annotation to "enabled" in a Deployment or DaemonSet, you can customize the resource CPU/memory requests and limits. The following example shows how to customize the resource CPU/memory requests and limits in a Deployment:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-requests-limits: "enabled"
spec:
...
containers:
- name: coredns
resources:
limits:
# update cpu limits value won't be reconciled back
cpu: "3"
# update memory limits value won't be reconciled back
memory: "500Mi"
requests:
# update cpu requests value won't be reconciled back
cpu: "100m"
# update memory requests value won't be reconciled back
memory: "70Mi"
```


## Customize resource maximum/minimum allowed CPU/memory

After setting the `kubernetes.azure.com/override-min-max`

annotation to "enabled" in a VPA custom resource, you can customize the maximum and minimum allowed CPU and memory values in a VPA custom resource. The following example shows how to customize the maximum and minimum allowed CPU and memory values in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-min-max: "enabled"
spec:
resourcePolicy:
containerPolicies:
- containerName: coredns
maxAllowed:
# update maxAllowed cpu value won't be reconciled back
cpu: 3
# update maxAllowed memory value won't be reconciled back
memory: 500Mi
minAllowed:
# update minAllowed cpu value won't be reconciled back
cpu: 10m
# update minAllowed memory value won't be reconciled back
memory: 10Mi
...
```


## Customize resource update mode

After setting the `kubernetes.azure.com/override-update-mode`

annotation to "enabled" in a VPA custom resource, you can customize the update policy `updateMode`

value in a VPA custom resource to "Off" or "Initial" (default). The following example shows how to customize the update policy `updateMode`

value to "Initial" in a VPA custom resource:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# update value from "disabled" to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# update updateMode won't be reconciled back
updateMode: "Initial"
```


## Disable VPA on a specific AKS managed add-on

To disable VPA on a specific AKS managed add-on, you need to update the VPA custom resource YAML file to set the `kubernetes.azure.com/override-update-mode`

annotation to `"enabled"`

and the `updateMode`

to `"Off"`

. With *Off* mode, the VPA only provides CPU and memory recommendations and doesn't apply the changes to the pod.

The following example shows how to disable VPA on the CoreDNS add-on:

```
apiVersion: autoscaling.k8s.io/v1
kind: VerticalPodAutoscaler
metadata:
name: coredns
namespace: kube-system
annotations:
# Set value to "enabled"
kubernetes.azure.com/override-update-mode: "enabled"
spec:
...
updatePolicy:
# Set value to "Off"
updateMode: "Off"
```


## Troubleshooting

- Make sure the AKS managed add-on supports the cost optimized add-on scaling feature. For more information, see
[Supported AKS managed add-ons](optimized-addon-scaling#supported-aks-add-ons). - Verify that the
`kubernetes.azure.com/override-requests-limits`

annotation in the Deployment or DaemonSet is set to "enabled". - Verify that the
`kubernetes.azure.com/override-min-max`

annotation in the VPA custom resource is set to "enabled". - Verify that the
`kubernetes.azure.com/override-update-mode`

annotation in the VPA custom resource is set to "enabled".

## Next steps

To further configure cluster resource utilization and free up CPU/memory for AKS managed add-on pods, see [Vertical pod autoscaling in AKS](vertical-pod-autoscaler).


---

<!-- DOCUMENTO FUSIONADO: _network-policy-best-practices___tutorial-kubernetes-deploy-application_operator_1150b5.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: network-policy-best-practices.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/network-policy-best-practices -->

# Best practices for network policies in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes, by default, operates as a flat network where all pods can communicate freely with each other. This unrestricted connectivity can be convenient for developers but poses significant security risks as applications scale. Imagine an organization deploying multiple microservices, each handling sensitive data, customer transactions, or backend operations. Without any restrictions, any compromised pod could potentially access unauthorized data or disrupt services.

To address these security concerns, [Network Policies in Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/) allow administrators to control and restrict traffic between workloads. They provide a declarative way to enforce traffic rules, ensuring secure and controlled network behavior within a cluster.

## What is Kubernetes Network Policy?

A Network Policy in Kubernetes is a set of rules that control how pods communicate with each other and with external services. It provides fine-grained control over network traffic, allowing administrators to enforce security and segmentation at the namespace level. By implementing Network Policies, you gain:

**Stronger security posture**: Prevent unauthorized lateral movement within the cluster.**Compliance and governance**: Enforce regulatory requirements by controlling communication pathways.**Reduced blast radius**: Limit the impact of a compromised workload by restricting its network access.

Initially, Network Policies were designed to operate at Layer 3 (IP) and Layer 4 (TCP/UDP) of the OSI model, enabling basic control over pod-to-pod and external communications. However, advanced network policy engines like Cilium have extended Network Policies to Layer 7 (Application Layer), allowing deeper control over application traffic for modern cloud-native applications.

Network Policies are defined at the namespace level, meaning each policy applies to workloads within a specific namespace. The main components of a Network Policy include:

**Pod selector**: Defines which pods the policy applies to based on labels.**Ingress rules**: Specify the allowed incoming connections.**Egress rules**: Specify the allowed outgoing connections.**Policy types**: Define whether the policy applies to ingress (incoming), egress (outgoing), or both.

## Foundations of building effective network policies

Building effective network policies in Kubernetes isn't just about writing YAML configurations—it requires a deep understanding of your application architecture, traffic patterns, and security requirements. Without a clear picture of how workloads communicate, enforcing security policies can lead to unintended disruptions or gaps in protection. The following sections cover how to systematically approach network policy design.

### Understanding your workload connectivity

Before implementing network policies, you need visibility into how workloads communicate with each other and external services. This step ensures that policies don’t inadvertently block critical traffic while effectively limiting unnecessary exposure.

**Leverage Visibility Tools:**in addition to the network requirements provided by application team you can use tools like[Cilium Hubble](https://github.com/cilium/hubble), and[Retina](https://retina.sh/)help you analyze pod-to-pod traffic, identify which services need to communicate and define their ingress and egress dependencies. For example, a frontend might need to reach a backend API, but it shouldn’t talk directly to a database. Identify which services need to communicate and define their ingress and egress dependencies. For example, a frontend might need to reach a backend API, but it shouldn’t talk directly to a database.**The importance of labels in network policies:**Traditionally, network security policies have relied on static IP addresses to define traffic rules. This approach is problematic in Kubernetes because pods are ephemeral—created and destroyed frequently, often with dynamically assigned IP addresses. Maintaining security rules based on constantly changing IPs would require continuous updates, making policy management inefficient and error-prone.

Labels solve this challenge by providing a stable way to group workloads. Instead of relying on fixed IPs, Kubernetes Network Policies use labels to define security rules that remain consistent even as pods restart or shift across nodes. For example, a policy can allow communication between pods labeled `app: frontend`

and `app: backend`

, ensuring traffic flows as intended regardless of pod IP changes. This label-based approach is critical for achieving scalable, intent-driven network security in cloud-native environments.

A well-defined labeling strategy simplifies policy management, reduces misconfigurations, and enhances security enforcement across clusters.

**Define Micro-segmentation:**Organizing workloads into security zones (e.g., frontend, backend, database) helps enforce the principle of least privilege. For instance, microservices handling customer transactions should be isolated from general-purpose applications.

### Layered security approach for Kubernetes

Relying solely on basic Kubernetes Network Policies might not be sufficient for all security needs. A layered approach ensures comprehensive protection across different levels of network communication.

**(L3/L4) policies**: The foundation of network security, controlling traffic based on pod labels and namespaces at the IP, port, and protocol level.**FQDN-based policies**: Restrict egress traffic to specific external domains, ensuring workloads can only reach approved external services (for example: only allowing access to*microsoft.com*for API calls).**Layer 7 policies**: Introduces fine-grained control over traffic by filtering requests based on HTTP methods, headers, and paths. This is useful for securing APIs and enforcing application-layer security policies.

### Management of Network Policies

Who should manage network policies? This often depends on an organization’s structure and security requirements. A well-balanced approach allows both security teams and application developers to collaborate effectively.

**Centralized security administration**: Security or networking teams should define baseline policies to enforce global security requirements, such as default deny-all rules or compliance-driven restrictions.**Developer autonomy with guardrails**: Application teams should be able to define service-specific network policies within their namespaces, enabling security while maintaining agility.**Policy lifecycle management**: Regularly reviewing and updating policies ensures that security remains aligned with evolving application architectures. Observability tools can help detect policy misconfigurations and missing rules.

#### Example: Securing a multi-tier web application with Network Policies

**Step 1: Understanding workload connectivity**

- Visibility tools: Use Cilium Hubble to observe how pods communicate.


Mapping connectivity:

Source Destination Protocol Port Frontend Backend TCP 8080 Backend Database TCP 5432 Backend External Payment Gateway TCP 443

**Step 2: Applying labels for policy enforcement**

By labeling workloads correctly, policies can remain stable even if pod IPs change.

`app: frontend`

for UI pods.`app: backend`

for API pods.`app: database`

for DB pods.

**Step 3: Implementing application-level Network Policies**

In this example, we use two layers of network policies: an L3/L4 basic policy to control traffic between microservices and a fully qualified domain name (FQDN) policy to control egress traffic with external payment gateway.

| Allow frontend to communicate with backend | Allow backend to access the database | Allow backend to reach external payment API |
|---|---|---|
Policy 1: Frontend egress`to:` ` - podSelector:` ` matchLabels:` ` app: backend` ` ports:` ` - protocol: TCP` ` port: 8080` Policy 2: Backend ingress`from:` ` - podSelector:` ` matchLabels:` ` app: frontend` ` ports:` ` - protocol: TCP` ` port: 8080` |
Policy 1: Backend egress`to:` ` - podSelector:` ` matchLabels:` ` app: database` ` ports:` ` - protocol: TCP` ` port: 5432` Policy 2: Database ingress`from:` ` - podSelector:` ` matchLabels:` ` app: backend` ` ports:` ` - protocol: TCP` ` port: 5432` |
Policy 1: Backend`spec:` ` endpointSelector:` ` matchLabels:` ` app: backend` ` egress:` ` - toFQDNs:` ` - matchName: payments.example.com` ` ports:` ` - protocol: TCP` ` port: 443` |

**Step 4: Managing and maintaining policies**

Security and platform teams enforce baseline deny rules.

Baseline policy Platform policy Security - Default deny all traffic - Allow DNS

- Allow Logs- Block traffic

to known

malicious IPs

and domainsEnsuring that the application's network policies comply with platform and security requirements while avoiding any policy violations.

**Baseline****Platform policy****Security policy****Allow frontend to communicate with backend****Allow backend to access the database****Allow backend to reach external payment API**- Default deny all traffic - Allow DNS

- Allow Logs- Block traffic to known malicious IPs and domains **Policy 1: Frontend egress:**

- to:

-**podSelector:**

**matchLabels:**

app: backend

ports:

-**protocol:**TCP

port: 8080


**Policy 2: Backend ingress:**

- from:

-**podSelector:**

**matchLabels:**

app: frontend

ports:

-**protocol:**TCP

port: 8080**Policy 1: Backend egress:**

- to:

-**podSelector:**

**matchLabels:**

app: database

ports:

-**protocol:**TCP

port: 5432


**Policy 2: Database ingress:**

- from:

-**podSelector:**

**matchLabels:**

app: backend

ports:

-**protocol:**TCP

port: 5432**Policy 1: Backend**

**spec:**

**endpointSelector:**

**matchLabels:**

app: backend

**egress:**

-**toFQDNs:**

-**matchName:**payments.example.com

**ports:**

-**protocol:**TCP

port: 443This structured approach ensures security without disrupting application functionality.


## Azure Powered by Cilium

[Azure Container Network Interface (CNI) powered by Cilium](/en-us/azure/aks/azure-cni-powered-by-cilium) leverages eBPF (extended Berkeley Packet Filter) to provide high-performance networking, observability, and security for Kubernetes workloads. Unlike traditional CNIs that rely on iptables-based packet filtering, Azure CNI powered by Cilium uses eBPF to operate at the kernel level, enabling efficient and scalable network policy enforcement. On Azure Kubernetes Service (AKS), Cilium is the only supported network policy engine, reflecting Azure’s investment in performance, scalability, and security.
Azure Kubernetes Service integrates Cilium as a managed component, simplifying network security enforcement. Administrators can define Cilium Network Policies directly within their AKS clusters without requiring external controllers.

Cilium extends the usage of labels with Identities. Large clusters with many pods might experience scale issues where constantly updating IP filters occurs with a high pod churn rate. Under the hood, Identities map to labels and allow connections to initiate as soon as the identity resolves rather than needing to update rules on nodes.

With Azure CNI powered by Cilium you don't need to install a separate network policy engine such as Azure Network Policy Manager or Calico.

Use the following command to create a cluster with Azure CNI powered by cilium

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--network-dataplane cilium \
--generate-ssh-keys
```


### Anatomy of the Cilium Network Policy

With Azure CNI powered by Cilium, you can configure network policies natively in Kubernetes using two available formats:

**The standard**, which supports L3 and L4 policies at ingress or egress of the Pod.`NetworkPolicy`

resource**The extended**, which is available as a CustomResourceDefinition that supports specification of policies at Layers 3-7 for both ingress and egress.`CiliumNetworkPolicy`

format

With these CRDs, we can define security policies, and Kubernetes automatically distributes these policies to all the nodes in the cluster.

A Network Policy consists of several key components:

**Pod selector**: Specifies which pods the policy applies to using labels.**Policy types**: Determines whether the policy applies to ingress (incoming traffic), egress (outgoing traffic), or both.**Ingress rules**: Defines allowed sources (pods, namespaces, or IP ranges) and ports.**Egress rules**: Defines allowed destinations and ports.`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: frontend-egress namespace: default spec: podSelector: matchLabels: app: frontend policyTypes: - Egress egress: - to: - podSelector: matchLabels: app: backend ports: - protocol: TCP port: 8080`


## Advanced Network Policy

Azure Kubernetes services offers the [Advanced Container Networking Service (ACNS)](/en-us/azure/aks/advanced-container-networking-services-overview?tabs=cilium) a suite of services designed to enhance the networking capabilities of AKS clusters.

A key feature of ACNS is Container Network Security, which offers advanced security functionalities to safeguard containerized workloads. One notable aspect is the ability to implement advanced network policies, including Fully Qualified Domain Name (FQDN) filtering and Layer 7 (L7) policies, allowing for more granular control over both egress traffic and application-layer communication.

### Secure Egress traffic with FQDN Filtering

Traditionally, network policies in Kubernetes are based on IP addresses. However, in dynamic environments where pod IPs frequently change, managing such policies becomes cumbersome. [FQDN filtering](/en-us/azure/aks/container-network-security-concepts#overview-of-fqdn-filtering) simplifies this by allowing policies to be defined using domain names instead of IP addresses. This approach provides a more intuitive and user-friendly method of controlling network traffic, allowing organizations to enforce security policies with greater precision and flexibility.

Implementing FQDN filtering in AKS clusters requires enabling ACNS and configuring the necessary policies to define allowed or blocked domains, thereby enhancing the security posture of your containerized applications.

To enable Advanced Container Networking Services (ACNS) in Azure Kubernetes Service (AKS), use the flag --enable-acns

#### Example: Enable Advanced Container Networking Services on an existing cluster

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


#### Example: Build a network policy that allows traffic to “bing.com”

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: "allow-bing-fqdn"
spec:
endpointSelector:
matchLabels:
app: demo-container
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: ANY
rules:
dns:
- matchPattern: "*.bing.com"
- toFQDNs:
- matchPattern: "*.bing.com"
```


### Protection and security for APIs with L7 policies

As modern applications increasingly rely on APIs for communication, securing these interactions at the network layer alone is no longer sufficient. Standard network policies operate at Layer 3 (IP) and Layer 4 (TCP/UDP), controlling which pods can communicate, but they lack visibility into the actual API requests being made.

Layer 7 (L7) policies provide the following benefits and features:

**Granular API security**: Enforce policies based on HTTP, gRPC, or Kafka request data, rather than just IP addresses and ports.**Reduced attack surface**: Prevent unauthorized access and mitigate API-based attacks by filtering traffic at the application layer.**Compliance and auditing**: Ensure adherence to security standards by logging and controlling specific API interactions.**Simplified policy management**: Avoid the operational burden of additional sidecar proxies by leveraging built-in Cilium-powered L7 controls.

L7 policies AKS are enabled through ACNS and are available to customers using Azure CNI powered by Cilium. These policies support HTTP, gRPC, and Kafka protocols.

To enforce L7 policies, customers define `CiliumNetworkPolicy`

resources, specifying rules for application-layer traffic control.

#### Example: Enable ACNS on an existing cluster

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


#### Example: Allow only GET requests to /api from the frontend pod to the backend service on port 8080

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: frontend-l7-policy
namespace: default
spec:
endpointSelector:
matchLabels:
app: frontend
egress:
- toEndpoints:
- matchLabels:
app: backend
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/api"
```


## Strategies for network policies

Securing Kubernetes workloads requires a thoughtful approach to defining and enforcing network policies. A well-designed strategy ensures that applications communicate only as intended, reducing the risk of unauthorized access, lateral movement, and potential breaches. The following sections cover key strategies for implementing effective Kubernetes Network Policies.

### Adopt a Zero-Trust model

By default, Kubernetes allows unrestricted communication between all pods in a cluster. A Zero-Trust approach dictates that no traffic should be trusted by default, and only explicitly allowed communication paths should be permitted. Implementing a default deny-all network policy ensures that only necessary traffic flows between workloads.

Example of a deny-all policy:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: default-deny
namespace: default
spec:
podSelector: {}
policyTypes:
- Ingress
- Egress
```


### Namespace and multi-tenancy segmentation

In multi-tenant environments, namespaces help isolate workloads. Different teams typically manage their applications within dedicated namespaces, ensuring logical isolation between workloads. This separation is critical when multiple applications run alongside each other. Applying network policies at the namespace scope is often the first step in securing workloads, as it prevents unrestricted lateral movement between applications managed by different teams.

For example, restrict all ingress traffic to a namespace, allowing only traffic from the same namespace:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: restrict-cross-namespace
namespace: team-a
spec:
podSelector: {}
policyTypes:
- Ingress
ingress:
- from:
- namespaceSelector:
matchLabels:
name: team-a
```


### Microsegmentation for workload isolation

While namespace-based segmentation is an essential first step in securing multi-tenant Kubernetes clusters, application-level microsegmentation provides fine-grained control over how workloads interact within a namespace. Namespace isolation alone does not prevent unintended or unauthorized communication between different applications within the same namespace. This is where pod-level segmentation becomes critical.

For instance, if a frontend service should only talk to a backend service within the same namespace, a policy using pod labels can enforce this restriction:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: frontend-to-backend
namespace: team-a
spec:
podSelector:
matchLabels:
app: frontend
policyTypes:
- Egress
egress:
- to:
- podSelector:
matchLabels:
app: backend
ports:
- protocol: TCP
port: 8080
```


This prevents frontend pods from making unintended connections to other services, reducing the risk of unauthorized access or lateral movement inside the namespace.

By combining namespace-wide isolation with fine-grained application-level policies, teams can implement a multi-layered security model that prevents unauthorized traffic while allowing necessary communication for application functionality.

### Layered security approach

Network security should be implemented in layers, combining multiple levels of enforcement:

**L3/L4 policies**: Restrict traffic at the IP and port level (for example: allow TCP traffic on port 443).**FQDN-based filtering**: Restrict external communication based on domain names rather than IP addresses.**L7 policies**: Control communication based on application-layer attributes (for example: allow only HTTP GET requests to specific API paths).

For example, a Cilium L7 policy can restrict frontend services to only issue GET requests to the backend API:

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: frontend-l7-policy
namespace: default
spec:
endpointSelector:
matchLabels:
app: frontend
egress:
- toEndpoints:
- matchLabels:
app: backend
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/api"
```


This prevents the frontend from making POST or DELETE requests, limiting the attack surface.

### Integrating RBAC with Network Policy management

Role-based access control (RBAC) plays a crucial role in ensuring that only authorized users or teams can create, modify, or delete network policies. Without proper access controls, a misconfigured policy could either expose workloads to unauthorized access or unintentionally block critical application traffic.

By leveraging Kubernetes RBAC in conjunction with network policies, organizations can enforce separation of duties between platform administrators, security teams, and application developers. A typical approach is:

- Platform or security teams define baseline security policies that enforce compliance and restrict external access.
- Application teams are granted limited permissions to create or update network policies only for their respective namespaces.

For example, the following RBAC policy allows developers to create and modify network policies but only within their assigned namespace:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
name: network-policy-editor
namespace: team-a
rules:
- apiGroups: ["networking.k8s.io"]
resources: ["networkpolicies"]
verbs: ["get", "list", "create", "update", "delete"]
```


This role can then be bound to a specific team using a RoleBinding:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
name: team-a-network-policy-binding
namespace: team-a
subjects:
- kind: User
name: developer@example.com
apiGroup: rbac.authorization.k8s.io
roleRef:
kind: Role
name: network-policy-editor
apiGroup: rbac.authorization.k8s.io
```


By restricting network policy modifications to designated teams and namespaces, organizations can prevent accidental misconfigurations or unauthorized changes while still allowing flexibility for developers to implement application-specific security policies.

This approach reinforces the principle of least privilege while ensuring that network segmentation strategies remain consistent, secure, and aligned with organizational policies.

## Legacy and third-party solutions

### Azure Network Policy Manager (NPM)

Azure Network Policy Manager (NPM) is a legacy solution for enforcing Kubernetes network policies on AKS. As we continue to evolve our networking stack, we intend to deprecate NPM soon.

We strongly recommend all customers transition to Cilium Network Policy, which provides better performance, scalability, and enhanced security through eBPF-based enforcement. Cilium is the future of network policy in AKS and offers a more flexible and feature-rich alternative to NPM.

### NetworkPolicy support for Windows nodes

AKS doesn't natively support Kubernetes NetworkPolicy for Windows nodes out of the box. To enable network policies for Windows workloads, you can use Calico for Windows nodes, which is integrated into AKS to simplify deployment. You can enable it using the `--network-policy calico`

flag when creating a cluster.

Microsoft doesn't maintain the Calico images used in this integration. Our support is limited to ensuring Calico is properly integrated with AKS and functions as expected within the platform. Any issues related to Calico upstream bugs, feature requests, or troubleshooting beyond AKS integration should be directed to the Calico open-source community or Tigera, the maintainers of Calico.

### Calico open source – Third-party solution

Calico open source is a widely used third-party solution for enforcing Kubernetes network policies. It supports both Linux and Windows nodes and provides advanced networking and security capabilities, including network policy enforcement, workload identity, and encryption.

While Calico is integrated with AKS for Windows network policies (`--network-policy calico`

), it remains an open-source project maintained by Tigera. Microsoft doesn't maintain Calico images and provides limited support focused on ensuring proper integration with AKS. For advanced troubleshooting, feature requests, or issues beyond AKS integration, we recommend reaching out to the Calico open-source community or Tigera.

For Linux nodes, we strongly recommend using Cilium for network policy enforcement. For Windows nodes, we recommend using Calico.

## Conclusion

Network policies are a fundamental part of Kubernetes security, enabling organizations to control traffic flow, enforce workload isolation, and reduce the attack surface. As cloud-native environments evolve, relying solely on basic Layer 3/4 policies is no longer sufficient. Advanced solutions, such as Layer 7 filtering and FQDN-based policies, provide the granular security and flexibility needed to protect modern applications.

By following best practices including zero-trust model, microsegmentation, and adopting scalable solutions like Azure managed Cilium teams can enhance security while maintaining operational efficiency. As Kubernetes networking continues to evolve, adopting modern, observability-driven approaches will be key to securing workloads effectively.


---

<!-- DOCUMENTO FUSIONADO: __tutorial-kubernetes-deploy-application_operator-best-practices-scheduler_api-s_806380.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _tutorial-kubernetes-deploy-application_operator-best-practices-scheduler.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-deploy-application.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-application -->

# Tutorial - Deploy an application to Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes provides a distributed platform for containerized applications. You build and deploy your own applications and services into a Kubernetes cluster and let the cluster manage the availability and connectivity.

In this tutorial, you deploy a sample application into a Kubernetes cluster. You learn how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

Tip

With AKS, you can use the following approaches for configuration management:

**GitOps**: Enables declarations of your cluster's state to automatically apply to the cluster. To learn how to use GitOps to deploy an application with an AKS cluster, see the[prerequisites for Azure Kubernetes Service clusters](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json#for-azure-kubernetes-service-clusters)in the[GitOps with Flux v2](/en-us/azure/azure-arc/kubernetes/tutorial-use-gitops-flux2?toc=/azure/aks/toc.json)tutorial.**DevOps**: Enables you to build, test, and deploy with continuous integration (CI) and continuous delivery (CD). To see examples of how to use DevOps to deploy an application with an AKS cluster, see[Build and deploy to AKS with Azure Pipelines](devops-pipeline)or[GitHub Actions for deploying to Kubernetes](kubernetes-action).

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, and created a Kubernetes cluster. To complete this tutorial, you need the precreated `aks-store-quickstart.yaml`

Kubernetes manifest file. This file was downloaded in the application source code from [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Check your version with `az --version`

. To install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Update the manifest file

In these tutorials, your Azure Container Registry (ACR) instance stores the container images for the sample application. To deploy the application, you must update the image names in the Kubernetes manifest file to include your ACR login server name.

Get your login server address using the

command and query for your login server.`az acr list`

`az acr list --resource-group myResourceGroup --query "[].{acrLoginServer:loginServer}" --output table`

Make sure you're in the cloned

*aks-store-demo*directory, and then open the`aks-store-quickstart.yaml`

manifest file with a text editor.Update the

`image`

property for the containers by replacing*ghcr.io/azure-samples*with your ACR login server name.`containers: ... - name: order-service image: <acrName>.azurecr.io/aks-store-demo/order-service:latest ... - name: product-service image: <acrName>.azurecr.io/aks-store-demo/product-service:latest ... - name: store-front image: <acrName>.azurecr.io/aks-store-demo/store-front:latest ...`

Save and close the file.


## Run the application

Deploy the application using the

command, which parses the manifest file and creates the defined Kubernetes objects.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the resources successfully created in the AKS cluster:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`

Check the deployment is successful by viewing the pods with the

`kubectl get pods`

command.`kubectl get pods`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

### Command Line

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

Initially, the

`EXTERNAL-IP`

for the`store-front`

service shows as`<pending>`

:`store-front LoadBalancer 10.0.34.242 <pending> 80:30676/TCP 5s`

When the

`EXTERNAL-IP`

address changes from`<pending>`

to a public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`store-front LoadBalancer 10.0.34.242 52.179.23.131 80:30676/TCP 67s`

View the application in action by opening a web browser and navigating to the external IP address of your service:

`http://<external-ip>`

.

If the application doesn't load, it might be an authorization problem with your image registry. To view the status of your containers, use the `kubectl get pods`

command. If you can't pull the container images, see [Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration).

### Azure portal

Navigate to the Azure portal to find your deployment information.

Navigate to your AKS cluster resource.

From the service menu, under

**Kubernetes Resources**, select**Services and ingresses**.Copy the External IP shown in the column for the

`store-front`

service.Paste the IP into your browser to visit your store page.


## Clean up resources

Since you validated the application's functionality, you can now remove the cluster from the application. We will deploy the application again in the next tutorial.

Stop and remove the container instances and resources using the

`kubectl delete`

command.`kubectl delete -f aks-store-quickstart.yaml`

Check that all the application pods have been removed using the

`kubectl get pods`

command.`kubectl get pods`


## Next steps

In this tutorial, you deployed a sample Azure application to a Kubernetes cluster in AKS. You learned how to:

- Update a Kubernetes manifest file.
- Run an application in Kubernetes.
- Test the application.

In the next tutorial, you learn how to use PaaS services for stateful workloads in Kubernetes.


---

<!-- DOCUMENTO FUSIONADO: operator-best-practices-scheduler.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-scheduler -->

# Best practices for basic scheduler features in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. The Kubernetes scheduler lets you control the distribution of compute resources, or limit the impact of maintenance events.

This best practices article focuses on basic Kubernetes scheduling features for cluster operators. In this article, you learn how to:

- Use resource quotas to provide a fixed amount of resources to teams or workloads
- Limit the impact of scheduled maintenance using pod disruption budgets

## Enforce resource quotas


Best practice guidancePlan and apply resource quotas at the namespace level. If pods don't define resource requests and limits, reject the deployment. Monitor resource usage and adjust quotas as needed.


Resource requests and limits are placed in the pod specification. Requests are used by the Kubernetes scheduler at deployment time to find an available node in the cluster. Limits and requests work at the individual pod level. For more information about how to define these values, see [Define pod resource requests and limits](developer-best-practices-resource-management#define-pod-resource-requests-and-limits).

To provide a way to reserve and limit resources across a development team or project, you should use *resource quotas*. These quotas are defined on a namespace, and can be used to set quotas on the following basis:

**Compute resources**, such as CPU and memory, or GPUs.**Storage resources**, including the total number of volumes or amount of disk space for a given storage class.**Object count**, such as maximum number of secrets, services, or jobs can be created.

Kubernetes doesn't overcommit resources. Once your cumulative resource request total passes the assigned quota, all further deployments will be unsuccessful.

When you define resource quotas, all pods created in the namespace must provide limits or requests in their pod specifications. If they don't provide these values, you can reject the deployment. Instead, you can [configure default requests and limits for a namespace](https://kubernetes.io/docs/tasks/administer-cluster/manage-resources/memory-default-namespace/).

The following example YAML manifest named *dev-app-team-quotas.yaml* sets a hard limit of a total of *10* CPUs, *20Gi* of memory, and *10* pods:

```
apiVersion: v1
kind: ResourceQuota
metadata:
name: dev-app-team
spec:
hard:
cpu: "10"
memory: 20Gi
pods: "10"
```


This resource quota can be applied by specifying the namespace, such as *dev-apps*:

```
kubectl apply -f dev-app-team-quotas.yaml --namespace dev-apps
```


Work with your application developers and owners to understand their needs and apply the appropriate resource quotas.

For more information about available resource objects, scopes, and priorities, see [Resource quotas in Kubernetes](https://kubernetes.io/docs/concepts/policy/resource-quotas/).

## Plan for availability using pod disruption budgets


Best practice guidanceTo maintain the availability of applications, define Pod Disruption Budgets (PDBs) to make sure that a minimum number of pods are available in the cluster.


There are two disruptive events that cause pods to be removed:

### Involuntary disruptions

*Involuntary disruptions* are events beyond the typical control of the cluster operator or application owner. Include:

- Hardware failure on the physical machine
- Kernel panic
- Deletion of a node VM

Involuntary disruptions can be mitigated by:

- Using multiple replicas of your pods in a deployment.
- Running multiple nodes in the AKS cluster.

### Voluntary disruptions

*Voluntary disruptions* are events requested by the cluster operator or application owner. Include:

- Cluster upgrades
- Updated deployment template
- Accidentally deleting a pod

Kubernetes provides *pod disruption budgets* for voluntary disruptions, letting you plan for how deployments or replica sets respond when a voluntary disruption event occurs. Using pod disruption budgets, cluster operators can define a minimum available or maximum unavailable resource count.

If you upgrade a cluster or update a deployment template, the Kubernetes scheduler will schedule extra pods on other nodes before allowing voluntary disruption events to continue. The scheduler waits to reboot a node until the defined number of pods are successfully scheduled on other nodes in the cluster.

Let's look at an example of a replica set with five pods that run NGINX. The pods in the replica set are assigned the label `app: nginx-frontend`

. During a voluntary disruption event, such as a cluster upgrade, you want to make sure at least three pods continue to run. The following YAML manifest for a *PodDisruptionBudget* object defines these requirements:

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: nginx-pdb
spec:
minAvailable: 3
selector:
matchLabels:
app: nginx-frontend
```


You can also define a percentage, such as *60%*, which allows you to automatically compensate for the replica set scaling up the number of pods.

You can define a maximum number of unavailable instances in a replica set. Again, a percentage for the maximum unavailable pods can also be defined. The following pod disruption budget YAML manifest defines that no more than two pods in the replica set be unavailable:

```
apiVersion: policy/v1
kind: PodDisruptionBudget
metadata:
name: nginx-pdb
spec:
maxUnavailable: 2
selector:
matchLabels:
app: nginx-frontend
```


Once your pod disruption budget is defined, you create it in your AKS cluster as with any other Kubernetes object:

```
kubectl apply -f nginx-pdb.yaml
```


Work with your application developers and owners to understand their needs and apply the appropriate pod disruption budgets.

For more information about using pod disruption budgets, see [Specify a disruption budget for your application](https://kubernetes.io/docs/tasks/run-application/configure-pdb/).

## Next steps

This article focused on basic Kubernetes scheduler features. For more information about cluster operations in AKS, see the following best practices:


---

<!-- DOCUMENTO FUSIONADO: api-server-vnet-integration.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/api-server-vnet-integration -->

# Create an Azure Kubernetes Service cluster with API Server VNet Integration

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

An Azure Kubernetes Service (AKS) cluster configured with API Server VNet Integration projects the API server endpoint directly into a delegated subnet in the VNet where AKS is deployed. API Server VNet Integration enables network communication between the API server and the cluster nodes without requiring a private link or tunnel. The API server is available behind an internal load balancer VIP in the delegated subnet, which the nodes are configured to utilize. By using API Server VNet Integration, you can ensure network traffic between your API server and your node pools remains on the private network only.

## API server connectivity

The control plane or API server is in an AKS-managed Azure subscription. Your cluster or node pool is in your Azure subscription. The server and the virtual machines that make up the cluster nodes can communicate with each other through the API server VIP and pod IPs that are projected into the delegated subnet.

API Server VNet Integration is supported for public or private clusters. You can add or remove public access after cluster provisioning. Unlike non-VNet integrated clusters, the agent nodes always communicate directly with the private IP address of the API server internal load balancer (ILB) IP without using DNS. All node to API server traffic is kept on private networking, and no tunnel is required for API server to node connectivity. Out-of-cluster clients needing to communicate with the API server can do so normally if public network access is enabled. If public network access is disabled, you should follow the same private DNS setup methodology as standard [private clusters](private-clusters).

## Prerequisites

- You must have Azure CLI version 2.73.0 or later installed. You can check your version using the
`az --version`

command.

## Limitations

- API Server VNet Integration does not support
[Virtual Network Encryption](/en-us/azure/virtual-network/virtual-network-encryption-overview). Clusters deployed on**v3 or earlier AKS node SKUs**(which do not support VNet Encryption) are allowed but traffic will not be encrypted. Clusters deployed on**v4 or later AKS node SKUs**(which support VNet Encryption) are blocked because encrypted VNets are incompatible with API Server VNet Integration. See[AKS supported VM SKUs](quotas-skus-regions#supported-vm-sizes)for details.

## Availability

- API Server VNet Integration is available in all GA public cloud regions except eastus2 and qatarcentral. We are continually working on enabling this feature in these regions and will update this page when these regions become available.

## Create an AKS cluster with API Server VNet Integration using managed VNet

You can configure your AKS clusters with API Server VNet Integration in managed VNet or bring-your-own VNet mode. You can create them as public clusters (with API server access available via a public IP) or private clusters (where the API server is only accessible via private VNet connectivity). You can also toggle between a public and private state without redeploying your cluster.

### Create a resource group

Create a resource group using the

command.`az group create`

`az group create --location westus2 --name <resource-group>`


### Deploy a public cluster

Deploy a public AKS cluster with API Server VNet integration for managed VNet using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

flag.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-apiserver-vnet-integration \ --generate-ssh-keys`


### Deploy a private cluster

Deploy a private AKS cluster with API Server VNet integration for managed VNet using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

and`--enable-private-cluster`

flags.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-private-cluster \ --enable-apiserver-vnet-integration \ --generate-ssh-keys`


## Create a private AKS cluster with API Server VNet Integration using bring-your-own VNet

When using bring-your-own VNet, you must create and delegate an API server subnet to `Microsoft.ContainerService/managedClusters`

, which grants the AKS service permissions to inject the API server pods and internal load balancer into that subnet. You can't use the subnet for any other workloads, but you can use it for multiple AKS clusters located in the same virtual network. The minimum supported API server subnet size is a */28*.

The cluster identity needs permissions to both the API server subnet and the node subnet. Lack of permissions at the API server subnet can cause a provisioning failure.

Warning

An AKS cluster reserves at least 9 IPs in the subnet address space. Running out of IP addresses may prevent API server scaling and cause an API server outage.

### Create a resource group

- Create a resource group using the
command.`az group create`


```
az group create --location <location> --name <resource-group>
```


### Create a virtual network

Create a virtual network using the

command.`az network vnet create`

`az network vnet create --name <vnet-name> \ --resource-group <resource-group> \ --location <location> \ --address-prefixes 172.19.0.0/16`

Create an API server subnet using the

command.`az network vnet subnet create`

`az network vnet subnet create --resource-group <resource-group> \ --vnet-name <vnet-name> \ --name <apiserver-subnet-name> \ --delegations Microsoft.ContainerService/managedClusters \ --address-prefixes 172.19.0.0/28`

Create a cluster subnet using the

command.`az network vnet subnet create`

`az network vnet subnet create --resource-group <resource-group> \ --vnet-name <vnet-name> \ --name <cluster-subnet-name> \ --address-prefixes 172.19.1.0/24`


### Create a managed identity and give it permissions on the virtual network

Create a managed identity using the

command.`az identity create`

`az identity create --resource-group <resource-group> --name <managed-identity-name> --location <location>`

Assign the Network Contributor role to the API server subnet using the

command.`az role assignment create`

`az role assignment create --scope <apiserver-subnet-resource-id> \ --role "Network Contributor" \ --assignee <managed-identity-client-id>`

Assign the Network Contributor role to the cluster subnet using the

command.`az role assignment create`

`az role assignment create --scope <cluster-subnet-resource-id> \ --role "Network Contributor" \ --assignee <managed-identity-client-id>`


### Deploy a public cluster

Deploy a public AKS cluster with API Server VNet integration using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

flag.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-apiserver-vnet-integration \ --vnet-subnet-id <cluster-subnet-resource-id> \ --apiserver-subnet-id <apiserver-subnet-resource-id> \ --assign-identity <managed-identity-resource-id> \ --generate-ssh-keys`


### Deploy a private cluster

Deploy a private AKS cluster with API Server VNet integration using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

and`--enable-private-cluster`

flags.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --network-plugin azure \ --enable-private-cluster \ --enable-apiserver-vnet-integration \ --vnet-subnet-id <cluster-subnet-resource-id> \ --apiserver-subnet-id <apiserver-subnet-resource-id> \ --assign-identity <managed-identity-resource-id> \ --generate-ssh-keys`


## Convert an existing AKS cluster to API Server VNet Integration

Warning

**API Server VNet Integration is a one-way, capacity-sensitive feature.**

**Manual restart required.**

After enabling API Server VNet Integration using`az aks update --enable-apiserver-vnet-integration`

, due to control plane resource transition, you must immediately restart the cluster for the change to take effect. This restart is not automated. Delaying the restart increases the risk of capacity becoming unavailable, which can prevent the API server from starting. The cluster restart also ensures that all nodes reliably reconnect to the new API server endpoint.**Capacity is validated, but not reserved.**

AKS validates regional capacity when you enable the feature on an existing cluster, but this validation does not reserve capacity. If the restart is delayed and capacity becomes unavailable in the meantime, the cluster may fail to start after a stop or restart. Clusters that enabled this feature before general availability (GA), or that have not yet restarted since enablement, will not undergo capacity validation.**Feature cannot be disabled.**

Once enabled, the feature is permanent. You cannot disable API Server VNet Integration.

This upgrade performs a node-image version upgrade on all node pools and restarts all workloads while they undergo a rolling image upgrade.

Warning

Converting a cluster to API Server VNet Integration results in a change of the API Server IP address, though the hostname remains the same. If the IP address of the API server has been configured in any firewalls or network security group rules, those rules may need to be updated.

Update your cluster to API Server VNet Integration using the

command with the`az aks update`

`--enable-apiserver-vnet-integration`

flag.`az aks update --name <cluster-name> \ --resource-group <resource-group> \ --enable-apiserver-vnet-integration \ --apiserver-subnet-id <apiserver-subnet-resource-id>`


## Enable or disable private cluster mode on an existing cluster with API Server VNet Integration

AKS clusters configured with API Server VNet Integration can have public network access/private cluster mode enabled or disabled without redeploying the cluster. The API server hostname doesn't change, but public DNS entries are modified or removed if necessary.

Note

`--disable-private-cluster`

is currently in preview. For more information, see [Reference and support levels](/en-us/cli/azure/reference-types-and-status).

### Enable private cluster mode

Enable private cluster mode using the

command with the`az aks update`

`--enable-private-cluster`

flag.`az aks update --name <cluster-name> \ --resource-group <resource-group> \ --enable-private-cluster`


### Disable private cluster mode

Disable private cluster mode using the

command with the`az aks update`

`--disable-private-cluster`

flag.`az aks update --name <cluster-name> \ --resource-group <resource-group> \ --disable-private-cluster`


## Connect to cluster using kubectl

Configure

`kubectl`

to connect to your cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group <resource-group> --name <cluster-name>`


## Expose the API server through Private Link

You can expose the API server endpoint of a private cluster with API Server VNet Integration using Azure Private Link. The following steps show how to create a Private Link Service (PLS) in the cluster VNet and connect to it from another VNet or subscription using a Private Endpoint.

### Create an API Server VNet Integration Private cluster

Create a private AKS cluster with API Server VNet Integration using the

command with the`az aks create`

`--enable-api-server-vnet-integration`

and`--enable-private-cluster`

flags.`az aks create --name <cluster-name> \ --resource-group <resource-group> \ --location <location> \ --enable-private-cluster \ --enable-apiserver-vnet-integration`


For more guidance on how to set up Private Link with API Server VNet Integration, see [Private Link with API Server VNet Integration](private-apiserver-vnet-integration-cluster).

## NSG security rules

All traffic within the VNet is allowed by default. But if you have added NSG rules to restrict traffic between different subnets, ensure that the NSG security rules permit the following types of communication:

| Destination | Source | Protocol | Port | Use |
|---|---|---|---|---|
| APIServer Subnet CIDR | Cluster Subnet | TCP | 443 and 4443 | Required to enable communication between Nodes and the API server. |
| APIServer Subnet CIDR | Azure Load Balancer | TCP | 9988 | Required to enable communication between Azure Load Balancer and the API server. You can also enable all communications between the Azure Load Balancer and the API Server Subnet CIDR. |

## Next steps

- For associated best practices, see
[Best practices for network connectivity and security in AKS](operator-best-practices-network). - For guidance on how to set up private link with API Server VNet Integration, see
[Private Link with API Server VNet Integration](private-apiserver-vnet-integration-cluster).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/network-policy-best-practices -->

# Best practices for network policies in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes, by default, operates as a flat network where all pods can communicate freely with each other. This unrestricted connectivity can be convenient for developers but poses significant security risks as applications scale. Imagine an organization deploying multiple microservices, each handling sensitive data, customer transactions, or backend operations. Without any restrictions, any compromised pod could potentially access unauthorized data or disrupt services.

To address these security concerns, [Network Policies in Kubernetes](https://kubernetes.io/docs/concepts/services-networking/network-policies/) allow administrators to control and restrict traffic between workloads. They provide a declarative way to enforce traffic rules, ensuring secure and controlled network behavior within a cluster.

## What is Kubernetes Network Policy?

A Network Policy in Kubernetes is a set of rules that control how pods communicate with each other and with external services. It provides fine-grained control over network traffic, allowing administrators to enforce security and segmentation at the namespace level. By implementing Network Policies, you gain:

**Stronger security posture**: Prevent unauthorized lateral movement within the cluster.**Compliance and governance**: Enforce regulatory requirements by controlling communication pathways.**Reduced blast radius**: Limit the impact of a compromised workload by restricting its network access.

Initially, Network Policies were designed to operate at Layer 3 (IP) and Layer 4 (TCP/UDP) of the OSI model, enabling basic control over pod-to-pod and external communications. However, advanced network policy engines like Cilium have extended Network Policies to Layer 7 (Application Layer), allowing deeper control over application traffic for modern cloud-native applications.

Network Policies are defined at the namespace level, meaning each policy applies to workloads within a specific namespace. The main components of a Network Policy include:

**Pod selector**: Defines which pods the policy applies to based on labels.**Ingress rules**: Specify the allowed incoming connections.**Egress rules**: Specify the allowed outgoing connections.**Policy types**: Define whether the policy applies to ingress (incoming), egress (outgoing), or both.

## Foundations of building effective network policies

Building effective network policies in Kubernetes isn't just about writing YAML configurations—it requires a deep understanding of your application architecture, traffic patterns, and security requirements. Without a clear picture of how workloads communicate, enforcing security policies can lead to unintended disruptions or gaps in protection. The following sections cover how to systematically approach network policy design.

### Understanding your workload connectivity

Before implementing network policies, you need visibility into how workloads communicate with each other and external services. This step ensures that policies don’t inadvertently block critical traffic while effectively limiting unnecessary exposure.

**Leverage Visibility Tools:**in addition to the network requirements provided by application team you can use tools like[Cilium Hubble](https://github.com/cilium/hubble), and[Retina](https://retina.sh/)help you analyze pod-to-pod traffic, identify which services need to communicate and define their ingress and egress dependencies. For example, a frontend might need to reach a backend API, but it shouldn’t talk directly to a database. Identify which services need to communicate and define their ingress and egress dependencies. For example, a frontend might need to reach a backend API, but it shouldn’t talk directly to a database.**The importance of labels in network policies:**Traditionally, network security policies have relied on static IP addresses to define traffic rules. This approach is problematic in Kubernetes because pods are ephemeral—created and destroyed frequently, often with dynamically assigned IP addresses. Maintaining security rules based on constantly changing IPs would require continuous updates, making policy management inefficient and error-prone.

Labels solve this challenge by providing a stable way to group workloads. Instead of relying on fixed IPs, Kubernetes Network Policies use labels to define security rules that remain consistent even as pods restart or shift across nodes. For example, a policy can allow communication between pods labeled `app: frontend`

and `app: backend`

, ensuring traffic flows as intended regardless of pod IP changes. This label-based approach is critical for achieving scalable, intent-driven network security in cloud-native environments.

A well-defined labeling strategy simplifies policy management, reduces misconfigurations, and enhances security enforcement across clusters.

**Define Micro-segmentation:**Organizing workloads into security zones (e.g., frontend, backend, database) helps enforce the principle of least privilege. For instance, microservices handling customer transactions should be isolated from general-purpose applications.

### Layered security approach for Kubernetes

Relying solely on basic Kubernetes Network Policies might not be sufficient for all security needs. A layered approach ensures comprehensive protection across different levels of network communication.

**(L3/L4) policies**: The foundation of network security, controlling traffic based on pod labels and namespaces at the IP, port, and protocol level.**FQDN-based policies**: Restrict egress traffic to specific external domains, ensuring workloads can only reach approved external services (for example: only allowing access to*microsoft.com*for API calls).**Layer 7 policies**: Introduces fine-grained control over traffic by filtering requests based on HTTP methods, headers, and paths. This is useful for securing APIs and enforcing application-layer security policies.

### Management of Network Policies

Who should manage network policies? This often depends on an organization’s structure and security requirements. A well-balanced approach allows both security teams and application developers to collaborate effectively.

**Centralized security administration**: Security or networking teams should define baseline policies to enforce global security requirements, such as default deny-all rules or compliance-driven restrictions.**Developer autonomy with guardrails**: Application teams should be able to define service-specific network policies within their namespaces, enabling security while maintaining agility.**Policy lifecycle management**: Regularly reviewing and updating policies ensures that security remains aligned with evolving application architectures. Observability tools can help detect policy misconfigurations and missing rules.

#### Example: Securing a multi-tier web application with Network Policies

**Step 1: Understanding workload connectivity**

- Visibility tools: Use Cilium Hubble to observe how pods communicate.


Mapping connectivity:

Source Destination Protocol Port Frontend Backend TCP 8080 Backend Database TCP 5432 Backend External Payment Gateway TCP 443

**Step 2: Applying labels for policy enforcement**

By labeling workloads correctly, policies can remain stable even if pod IPs change.

`app: frontend`

for UI pods.`app: backend`

for API pods.`app: database`

for DB pods.

**Step 3: Implementing application-level Network Policies**

In this example, we use two layers of network policies: an L3/L4 basic policy to control traffic between microservices and a fully qualified domain name (FQDN) policy to control egress traffic with external payment gateway.

| Allow frontend to communicate with backend | Allow backend to access the database | Allow backend to reach external payment API |
|---|---|---|
Policy 1: Frontend egress`to:` ` - podSelector:` ` matchLabels:` ` app: backend` ` ports:` ` - protocol: TCP` ` port: 8080` Policy 2: Backend ingress`from:` ` - podSelector:` ` matchLabels:` ` app: frontend` ` ports:` ` - protocol: TCP` ` port: 8080` |
Policy 1: Backend egress`to:` ` - podSelector:` ` matchLabels:` ` app: database` ` ports:` ` - protocol: TCP` ` port: 5432` Policy 2: Database ingress`from:` ` - podSelector:` ` matchLabels:` ` app: backend` ` ports:` ` - protocol: TCP` ` port: 5432` |
Policy 1: Backend`spec:` ` endpointSelector:` ` matchLabels:` ` app: backend` ` egress:` ` - toFQDNs:` ` - matchName: payments.example.com` ` ports:` ` - protocol: TCP` ` port: 443` |

**Step 4: Managing and maintaining policies**

Security and platform teams enforce baseline deny rules.

Baseline policy Platform policy Security - Default deny all traffic - Allow DNS

- Allow Logs- Block traffic

to known

malicious IPs

and domainsEnsuring that the application's network policies comply with platform and security requirements while avoiding any policy violations.

**Baseline****Platform policy****Security policy****Allow frontend to communicate with backend****Allow backend to access the database****Allow backend to reach external payment API**- Default deny all traffic - Allow DNS

- Allow Logs- Block traffic to known malicious IPs and domains **Policy 1: Frontend egress:**

- to:

-**podSelector:**

**matchLabels:**

app: backend

ports:

-**protocol:**TCP

port: 8080


**Policy 2: Backend ingress:**

- from:

-**podSelector:**

**matchLabels:**

app: frontend

ports:

-**protocol:**TCP

port: 8080**Policy 1: Backend egress:**

- to:

-**podSelector:**

**matchLabels:**

app: database

ports:

-**protocol:**TCP

port: 5432


**Policy 2: Database ingress:**

- from:

-**podSelector:**

**matchLabels:**

app: backend

ports:

-**protocol:**TCP

port: 5432**Policy 1: Backend**

**spec:**

**endpointSelector:**

**matchLabels:**

app: backend

**egress:**

-**toFQDNs:**

-**matchName:**payments.example.com

**ports:**

-**protocol:**TCP

port: 443This structured approach ensures security without disrupting application functionality.


## Azure Powered by Cilium

[Azure Container Network Interface (CNI) powered by Cilium](/en-us/azure/aks/azure-cni-powered-by-cilium) leverages eBPF (extended Berkeley Packet Filter) to provide high-performance networking, observability, and security for Kubernetes workloads. Unlike traditional CNIs that rely on iptables-based packet filtering, Azure CNI powered by Cilium uses eBPF to operate at the kernel level, enabling efficient and scalable network policy enforcement. On Azure Kubernetes Service (AKS), Cilium is the only supported network policy engine, reflecting Azure’s investment in performance, scalability, and security.
Azure Kubernetes Service integrates Cilium as a managed component, simplifying network security enforcement. Administrators can define Cilium Network Policies directly within their AKS clusters without requiring external controllers.

Cilium extends the usage of labels with Identities. Large clusters with many pods might experience scale issues where constantly updating IP filters occurs with a high pod churn rate. Under the hood, Identities map to labels and allow connections to initiate as soon as the identity resolves rather than needing to update rules on nodes.

With Azure CNI powered by Cilium you don't need to install a separate network policy engine such as Azure Network Policy Manager or Calico.

Use the following command to create a cluster with Azure CNI powered by cilium

```
az aks create \
--name <clusterName> \
--resource-group <resourceGroupName> \
--location <location> \
--network-plugin azure \
--network-plugin-mode overlay \
--pod-cidr 192.168.0.0/16 \
--network-dataplane cilium \
--generate-ssh-keys
```


### Anatomy of the Cilium Network Policy

With Azure CNI powered by Cilium, you can configure network policies natively in Kubernetes using two available formats:

**The standard**, which supports L3 and L4 policies at ingress or egress of the Pod.`NetworkPolicy`

resource**The extended**, which is available as a CustomResourceDefinition that supports specification of policies at Layers 3-7 for both ingress and egress.`CiliumNetworkPolicy`

format

With these CRDs, we can define security policies, and Kubernetes automatically distributes these policies to all the nodes in the cluster.

A Network Policy consists of several key components:

**Pod selector**: Specifies which pods the policy applies to using labels.**Policy types**: Determines whether the policy applies to ingress (incoming traffic), egress (outgoing traffic), or both.**Ingress rules**: Defines allowed sources (pods, namespaces, or IP ranges) and ports.**Egress rules**: Defines allowed destinations and ports.`apiVersion: networking.k8s.io/v1 kind: NetworkPolicy metadata: name: frontend-egress namespace: default spec: podSelector: matchLabels: app: frontend policyTypes: - Egress egress: - to: - podSelector: matchLabels: app: backend ports: - protocol: TCP port: 8080`


## Advanced Network Policy

Azure Kubernetes services offers the [Advanced Container Networking Service (ACNS)](/en-us/azure/aks/advanced-container-networking-services-overview?tabs=cilium) a suite of services designed to enhance the networking capabilities of AKS clusters.

A key feature of ACNS is Container Network Security, which offers advanced security functionalities to safeguard containerized workloads. One notable aspect is the ability to implement advanced network policies, including Fully Qualified Domain Name (FQDN) filtering and Layer 7 (L7) policies, allowing for more granular control over both egress traffic and application-layer communication.

### Secure Egress traffic with FQDN Filtering

Traditionally, network policies in Kubernetes are based on IP addresses. However, in dynamic environments where pod IPs frequently change, managing such policies becomes cumbersome. [FQDN filtering](/en-us/azure/aks/container-network-security-concepts#overview-of-fqdn-filtering) simplifies this by allowing policies to be defined using domain names instead of IP addresses. This approach provides a more intuitive and user-friendly method of controlling network traffic, allowing organizations to enforce security policies with greater precision and flexibility.

Implementing FQDN filtering in AKS clusters requires enabling ACNS and configuring the necessary policies to define allowed or blocked domains, thereby enhancing the security posture of your containerized applications.

To enable Advanced Container Networking Services (ACNS) in Azure Kubernetes Service (AKS), use the flag --enable-acns

#### Example: Enable Advanced Container Networking Services on an existing cluster

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


#### Example: Build a network policy that allows traffic to “bing.com”

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: "allow-bing-fqdn"
spec:
endpointSelector:
matchLabels:
app: demo-container
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: ANY
rules:
dns:
- matchPattern: "*.bing.com"
- toFQDNs:
- matchPattern: "*.bing.com"
```


### Protection and security for APIs with L7 policies

As modern applications increasingly rely on APIs for communication, securing these interactions at the network layer alone is no longer sufficient. Standard network policies operate at Layer 3 (IP) and Layer 4 (TCP/UDP), controlling which pods can communicate, but they lack visibility into the actual API requests being made.

Layer 7 (L7) policies provide the following benefits and features:

**Granular API security**: Enforce policies based on HTTP, gRPC, or Kafka request data, rather than just IP addresses and ports.**Reduced attack surface**: Prevent unauthorized access and mitigate API-based attacks by filtering traffic at the application layer.**Compliance and auditing**: Ensure adherence to security standards by logging and controlling specific API interactions.**Simplified policy management**: Avoid the operational burden of additional sidecar proxies by leveraging built-in Cilium-powered L7 controls.

L7 policies AKS are enabled through ACNS and are available to customers using Azure CNI powered by Cilium. These policies support HTTP, gRPC, and Kafka protocols.

To enforce L7 policies, customers define `CiliumNetworkPolicy`

resources, specifying rules for application-layer traffic control.

#### Example: Enable ACNS on an existing cluster

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


#### Example: Allow only GET requests to /api from the frontend pod to the backend service on port 8080

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: frontend-l7-policy
namespace: default
spec:
endpointSelector:
matchLabels:
app: frontend
egress:
- toEndpoints:
- matchLabels:
app: backend
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/api"
```


## Strategies for network policies

Securing Kubernetes workloads requires a thoughtful approach to defining and enforcing network policies. A well-designed strategy ensures that applications communicate only as intended, reducing the risk of unauthorized access, lateral movement, and potential breaches. The following sections cover key strategies for implementing effective Kubernetes Network Policies.

### Adopt a Zero-Trust model

By default, Kubernetes allows unrestricted communication between all pods in a cluster. A Zero-Trust approach dictates that no traffic should be trusted by default, and only explicitly allowed communication paths should be permitted. Implementing a default deny-all network policy ensures that only necessary traffic flows between workloads.

Example of a deny-all policy:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: default-deny
namespace: default
spec:
podSelector: {}
policyTypes:
- Ingress
- Egress
```


### Namespace and multi-tenancy segmentation

In multi-tenant environments, namespaces help isolate workloads. Different teams typically manage their applications within dedicated namespaces, ensuring logical isolation between workloads. This separation is critical when multiple applications run alongside each other. Applying network policies at the namespace scope is often the first step in securing workloads, as it prevents unrestricted lateral movement between applications managed by different teams.

For example, restrict all ingress traffic to a namespace, allowing only traffic from the same namespace:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: restrict-cross-namespace
namespace: team-a
spec:
podSelector: {}
policyTypes:
- Ingress
ingress:
- from:
- namespaceSelector:
matchLabels:
name: team-a
```


### Microsegmentation for workload isolation

While namespace-based segmentation is an essential first step in securing multi-tenant Kubernetes clusters, application-level microsegmentation provides fine-grained control over how workloads interact within a namespace. Namespace isolation alone does not prevent unintended or unauthorized communication between different applications within the same namespace. This is where pod-level segmentation becomes critical.

For instance, if a frontend service should only talk to a backend service within the same namespace, a policy using pod labels can enforce this restriction:

```
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
name: frontend-to-backend
namespace: team-a
spec:
podSelector:
matchLabels:
app: frontend
policyTypes:
- Egress
egress:
- to:
- podSelector:
matchLabels:
app: backend
ports:
- protocol: TCP
port: 8080
```


This prevents frontend pods from making unintended connections to other services, reducing the risk of unauthorized access or lateral movement inside the namespace.

By combining namespace-wide isolation with fine-grained application-level policies, teams can implement a multi-layered security model that prevents unauthorized traffic while allowing necessary communication for application functionality.

### Layered security approach

Network security should be implemented in layers, combining multiple levels of enforcement:

**L3/L4 policies**: Restrict traffic at the IP and port level (for example: allow TCP traffic on port 443).**FQDN-based filtering**: Restrict external communication based on domain names rather than IP addresses.**L7 policies**: Control communication based on application-layer attributes (for example: allow only HTTP GET requests to specific API paths).

For example, a Cilium L7 policy can restrict frontend services to only issue GET requests to the backend API:

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: frontend-l7-policy
namespace: default
spec:
endpointSelector:
matchLabels:
app: frontend
egress:
- toEndpoints:
- matchLabels:
app: backend
toPorts:
- ports:
- port: "8080"
protocol: TCP
rules:
http:
- method: "GET"
path: "/api"
```


This prevents the frontend from making POST or DELETE requests, limiting the attack surface.

### Integrating RBAC with Network Policy management

Role-based access control (RBAC) plays a crucial role in ensuring that only authorized users or teams can create, modify, or delete network policies. Without proper access controls, a misconfigured policy could either expose workloads to unauthorized access or unintentionally block critical application traffic.

By leveraging Kubernetes RBAC in conjunction with network policies, organizations can enforce separation of duties between platform administrators, security teams, and application developers. A typical approach is:

- Platform or security teams define baseline security policies that enforce compliance and restrict external access.
- Application teams are granted limited permissions to create or update network policies only for their respective namespaces.

For example, the following RBAC policy allows developers to create and modify network policies but only within their assigned namespace:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: Role
metadata:
name: network-policy-editor
namespace: team-a
rules:
- apiGroups: ["networking.k8s.io"]
resources: ["networkpolicies"]
verbs: ["get", "list", "create", "update", "delete"]
```


This role can then be bound to a specific team using a RoleBinding:

```
apiVersion: rbac.authorization.k8s.io/v1
kind: RoleBinding
metadata:
name: team-a-network-policy-binding
namespace: team-a
subjects:
- kind: User
name: developer@example.com
apiGroup: rbac.authorization.k8s.io
roleRef:
kind: Role
name: network-policy-editor
apiGroup: rbac.authorization.k8s.io
```


By restricting network policy modifications to designated teams and namespaces, organizations can prevent accidental misconfigurations or unauthorized changes while still allowing flexibility for developers to implement application-specific security policies.

This approach reinforces the principle of least privilege while ensuring that network segmentation strategies remain consistent, secure, and aligned with organizational policies.

## Legacy and third-party solutions

### Azure Network Policy Manager (NPM)

Azure Network Policy Manager (NPM) is a legacy solution for enforcing Kubernetes network policies on AKS. As we continue to evolve our networking stack, we intend to deprecate NPM soon.

We strongly recommend all customers transition to Cilium Network Policy, which provides better performance, scalability, and enhanced security through eBPF-based enforcement. Cilium is the future of network policy in AKS and offers a more flexible and feature-rich alternative to NPM.

### NetworkPolicy support for Windows nodes

AKS doesn't natively support Kubernetes NetworkPolicy for Windows nodes out of the box. To enable network policies for Windows workloads, you can use Calico for Windows nodes, which is integrated into AKS to simplify deployment. You can enable it using the `--network-policy calico`

flag when creating a cluster.

Microsoft doesn't maintain the Calico images used in this integration. Our support is limited to ensuring Calico is properly integrated with AKS and functions as expected within the platform. Any issues related to Calico upstream bugs, feature requests, or troubleshooting beyond AKS integration should be directed to the Calico open-source community or Tigera, the maintainers of Calico.

### Calico open source – Third-party solution

Calico open source is a widely used third-party solution for enforcing Kubernetes network policies. It supports both Linux and Windows nodes and provides advanced networking and security capabilities, including network policy enforcement, workload identity, and encryption.

While Calico is integrated with AKS for Windows network policies (`--network-policy calico`

), it remains an open-source project maintained by Tigera. Microsoft doesn't maintain Calico images and provides limited support focused on ensuring proper integration with AKS. For advanced troubleshooting, feature requests, or issues beyond AKS integration, we recommend reaching out to the Calico open-source community or Tigera.

For Linux nodes, we strongly recommend using Cilium for network policy enforcement. For Windows nodes, we recommend using Calico.

## Conclusion

Network policies are a fundamental part of Kubernetes security, enabling organizations to control traffic flow, enforce workload isolation, and reduce the attack surface. As cloud-native environments evolve, relying solely on basic Layer 3/4 policies is no longer sufficient. Advanced solutions, such as Layer 7 filtering and FQDN-based policies, provide the granular security and flexibility needed to protect modern applications.

By following best practices including zero-trust model, microsegmentation, and adopting scalable solutions like Azure managed Cilium teams can enhance security while maintaining operational efficiency. As Kubernetes networking continues to evolve, adopting modern, observability-driven approaches will be key to securing workloads effectively.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-extensions-az-cli -->

# Deploy and manage cluster extensions by using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can create extension instances in an AKS cluster, setting required and optional parameters including options related to updates and configurations. You can also view, list, update, and delete extension instances.

Before you begin, read about [cluster extensions](cluster-extensions).

Note

The examples provided in this article are not complete, and are only meant to showcase functionality. For a comprehensive list of commands and their parameters, see the [az k8s-extension CLI reference](/en-us/cli/azure/k8s-extension).

## Prerequisites

An Azure subscription. If you don't have an Azure subscription, you can create a

[free account](https://azure.microsoft.com/free).The

`Microsoft.ContainerService`

and`Microsoft.KubernetesConfiguration`

resource providers must be registered on your subscription. To register these providers, run the following command:`az provider register --namespace Microsoft.ContainerService --wait az provider register --namespace Microsoft.KubernetesConfiguration --wait`

An AKS cluster. This cluster must have been created with a managed identity, as cluster extensions won't work with service principal-based clusters. For new clusters created with

`az aks create`

, managed identity is configured by default. For existing service principal-based clusters, switch to manage identity by running`az aks update`

with the`--enable-managed-identity`

flag. For more information, see[Use managed identity](use-managed-identity).[Azure CLI](/en-us/cli/azure/install-azure-cli)version >= 2.16.0 installed. We recommend using the latest version.The latest version of the

`k8s-extension`

Azure CLI extensions. Install the extension by running the following command:`az extension add --name k8s-extension`

If the extension is already installed, make sure you're running the latest version by using the following command:

`az extension update --name k8s-extension`


## Create extension instance

Create a new extension instance with `k8s-extension create`

, passing in values for the mandatory parameters. This example command creates an Azure Machine Learning extension instance on your AKS cluster:

```
az k8s-extension create --name azureml --extension-type Microsoft.AzureML.Kubernetes --scope cluster --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters --configuration-settings enableInference=True allowInsecureConnections=True inferenceRouterServiceType=LoadBalancer
```


This example command creates a sample Kubernetes application (published on Marketplace) on your AKS cluster:

```
az k8s-extension create --name voteapp --extension-type Contoso.AzureVoteKubernetesAppTest --scope cluster --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters --plan-name testPlanID --plan-product testOfferID --plan-publisher testPublisherID --configuration-settings title=VoteAnimal value1=Cats value2=Dogs
```


Note

The Cluster Extensions service is unable to retain sensitive information for more than 48 hours. If the cluster extension agents don't have network connectivity for more than 48 hours and can't determine whether to create an extension on the cluster, then the extension transitions to `Failed`

state. Once in `Failed`

state, you'll need to run `k8s-extension create`

again to create a fresh extension instance.

### Required parameters

| Parameter name | Description |
|---|---|
`--name` |
Name of the extension instance |
`--extension-type` |
The type of extension you want to install on the cluster. For example: `Microsoft.AzureML.Kubernetes` |
`--cluster-name` |
Name of the AKS cluster on which the extension instance has to be created |
`--resource-group` |
The resource group containing the AKS cluster |
`--cluster-type` |
The cluster type on which the extension instance has to be created. Specify `managedClusters` as it maps to AKS clusters |

### Optional parameters

| Parameter name | Description |
|---|---|
`--auto-upgrade-minor-version` |
Boolean property that specifies if the extension minor version will be upgraded automatically or not. Default: `true` . If this parameter is set to true, you can't set `version` parameter, as the version will be dynamically updated. If set to `false` , extension won't be auto-upgraded even for patch versions. |
`--version` |
Version of the extension to be installed (specific version to pin the extension instance to). Must not be supplied if auto-upgrade-minor-version is set to `true` . |
`--configuration-settings` |
Settings that can be passed into the extension to control its functionality. Pass values as space separated `key=value` pairs after the parameter name. If this parameter is used in the command, then `--configuration-settings-file` can't be used in the same command. |
`--configuration-settings-file` |
Path to the JSON file having key value pairs to be used for passing in configuration settings to the extension. If this parameter is used in the command, then `--configuration-settings` can't be used in the same command. |
`--configuration-protected-settings` |
These settings are not retrievable using `GET` API calls or `az k8s-extension show` commands, and are thus used to pass in sensitive settings. Pass values as space separated `key=value` pairs after the parameter name. If this parameter is used in the command, then `--configuration-protected-settings-file` can't be used in the same command. |
`--configuration-protected-settings-file` |
Path to the JSON file having key value pairs to be used for passing in sensitive settings to the extension. If this parameter is used in the command, then `--configuration-protected-settings` can't be used in the same command. |
`--scope` |
Scope of installation for the extension - `cluster` or `namespace` |
`--release-namespace` |
This parameter indicates the namespace within which the release is to be created. This parameter is only relevant if `scope` parameter is set to `cluster` . |
`--release-train` |
Extension authors can publish versions in different release trains such as `Stable` , `Preview` , etc. If this parameter isn't set explicitly, `Stable` is used as default. This parameter can't be used when `--auto-upgrade-minor-version` parameter is set to `false` . |
`--target-namespace` |
This parameter indicates the namespace within which the release will be created. Permission of the system account created for this extension instance will be restricted to this namespace. This parameter is only relevant if the `scope` parameter is set to `namespace` . |
`--plan-name` |
Plan ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. |
`--plan-product` |
Product ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. An example of this is the name of the ISV offering used. |
`--plan-publisher` |
Publisher ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. |

## Show details of an extension instance

To view details of a currently installed extension instance, use `k8s-extension show`

, passing in values for the mandatory parameters.

```
az k8s-extension show --name azureml --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters
```


## List all extensions installed on the cluster

To list all extensions installed on a cluster, use `k8s-extension list`

, passing in values for the mandatory parameters.

```
az k8s-extension list --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters
```


## Update extension instance

Note

Refer to documentation for the specific extension type to understand the specific settings in `--configuration-settings`

and `--configuration-protected-settings`

that are able to be updated. For `--configuration-protected-settings`

, all settings are expected to be provided, even if only one setting is being updated. If any of these settings are omitted, those settings will be considered obsolete and deleted.

To update an existing extension instance, use `k8s-extension update`

, passing in values for the mandatory parameters. The following command updates the auto-upgrade setting for an Azure Machine Learning extension instance:

```
az k8s-extension update --name azureml --extension-type Microsoft.AzureML.Kubernetes --scope cluster --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters
```


### Required parameters for update

| Parameter name | Description |
|---|---|
`--name` |
Name of the extension instance |
`--extension-type` |
The type of extension you want to install on the cluster. For example: Microsoft.AzureML.Kubernetes |
`--cluster-name` |
Name of the AKS cluster on which the extension instance has to be created |
`--resource-group` |
The resource group containing the AKS cluster |
`--cluster-type` |
The cluster type on which the extension instance has to be created. Specify `managedClusters` as it maps to AKS clusters |

If updating a Kubernetes application procured through Marketplace, the following parameters are also required:

| Parameter name | Description |
|---|---|
`--plan-name` |
Plan ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. |
`--plan-product` |
Product ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. An example of this is the name of the ISV offering used. |
`--plan-publisher` |
Publisher ID of the extension, found on the Marketplace page in the Azure portal under Usage Information + Support. |

### Optional parameters for update

| Parameter name | Description |
|---|---|
`--auto-upgrade-minor-version` |
Boolean property that specifies if the extension minor version will be upgraded automatically or not. Default: `true` . If this parameter is set to true, you cannot set `version` parameter, as the version will be dynamically updated. If set to `false` , extension won't be auto-upgraded even for patch versions. |
`--version` |
Version of the extension to be installed (specific version to pin the extension instance to). Must not be supplied if auto-upgrade-minor-version is set to `true` . |
`--configuration-settings` |
Settings that can be passed into the extension to control its functionality. Only the settings that require an update need to be provided. The provided settings would be replaced with the provided values. Pass values as space separated `key=value` pairs after the parameter name. If this parameter is used in the command, then `--configuration-settings-file` can't be used in the same command. |
`--configuration-settings-file` |
Path to the JSON file having key value pairs to be used for passing in configuration settings to the extension. If this parameter is used in the command, then `--configuration-settings` can't be used in the same command. |
`--configuration-protected-settings` |
These settings are not retrievable using `GET` API calls or `az k8s-extension show` commands, and are thus used to pass in sensitive settings. When you update a setting, all settings are expected to be specified. If some settings are omitted, those settings would be considered obsolete and deleted. Pass values as space separated `key=value` pairs after the parameter name. If this parameter is used in the command, then `--configuration-protected-settings-file` can't be used in the same command. |
`--configuration-protected-settings-file` |
Path to the JSON file having key value pairs to be used for passing in sensitive settings to the extension. If this parameter is used in the command, then `--configuration-protected-settings` can't be used in the same command. |
`--scope` |
Scope of installation for the extension - `cluster` or `namespace` |
`--release-train` |
Extension authors can publish versions in different release trains such as `Stable` , `Preview` , etc. If this parameter isn't set explicitly, `Stable` is used as default. This parameter can't be used when `autoUpgradeMinorVersion` parameter is set to `false` . |

## Delete extension instance

To delete an extension instance on a cluster, use `k8s-extension-delete`

, passing in values for the mandatory parameters.

```
az k8s-extension delete --name azureml --cluster-name <clusterName> --resource-group <resourceGroupName> --cluster-type managedClusters
```


Note

The Azure resource representing this extension gets deleted immediately. The Helm release on the cluster associated with this extension is only deleted when the agents running on the Kubernetes cluster have network connectivity and can reach out to Azure services again to fetch the desired state.

## Next steps

- View the list of
[currently available cluster extensions](cluster-extensions#currently-available-extensions). - Learn about
[Kubernetes applications available through Marketplace](deploy-marketplace).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/nat-gateway -->

# Create a managed or user-assigned NAT gateway for your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

While you can route egress traffic through an Azure Load Balancer, there are limitations on the number of outbound flows of traffic you can have. Azure NAT Gateway allows up to 64,512 outbound UDP and TCP traffic flows per IP address with a maximum of 16 IP addresses.

This article shows you how to create an Azure Kubernetes Service (AKS) cluster with a managed NAT gateway and a user-assigned NAT gateway for egress traffic. It also shows you how to disable OutboundNAT on Windows.

## Before you begin

- Make sure you're using the latest version of
[Azure CLI](/en-us/cli/azure/install-azure-cli). - Make sure you're using Kubernetes version 1.20.x or above.
- Managed NAT gateway is incompatible with custom virtual networks.

Important

In non-private clusters, API server cluster traffic is routed and processed through the clusters outbound type. To prevent API server traffic from being processed as public traffic, consider using a [private cluster](private-clusters), or check out the [API Server VNet Integration](api-server-vnet-integration) feature.

## Create an AKS cluster with a managed NAT gateway

- Create an AKS cluster with a new managed NAT gateway using the
command with the`az aks create`

`--outbound-type managedNATGateway`

,`--nat-gateway-managed-outbound-ip-count`

, and`--nat-gateway-idle-timeout`

parameters. If you want the NAT gateway to operate out of a specific availability zone, specify the zone using`--zones`

. - If no zone is specified when creating a managed NAT gateway, then NAT gateway is deployed to "no zone" by default. When NAT gateway is placed in
**no zone**, Azure places the resource in a zone for you. For more information on non-zonal deployment model, see[non-zonal NAT gateway](/en-us/azure/nat-gateway/nat-availability-zones#non-zonal). - A managed NAT gateway resource can't be used across multiple availability zones.

The following commands first create the required resource group, then the AKS cluster with a managed NAT gateway.

```
export RANDOM_SUFFIX=$(openssl rand -hex 3)
export MY_RG="myResourceGroup$RANDOM_SUFFIX"
export MY_AKS="myNatCluster$RANDOM_SUFFIX"
az group create --name $MY_RG --location "eastus2"
```


Results:

```
{
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx",
"location": "eastus2",
"managedBy": null,
"name": "myResourceGroupxxx",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


```
az aks create \
--resource-group $MY_RG \
--name $MY_AKS \
--node-count 3 \
--outbound-type managedNATGateway \
--nat-gateway-managed-outbound-ip-count 2 \
--nat-gateway-idle-timeout 4 \
--generate-ssh-keys
```


Results:

```
{
"aadProfile": null,
"agentPoolProfiles": [
{
...
"name": "nodepool1",
...
"provisioningState": "Succeeded",
...
}
],
"dnsPrefix": "myNatClusterxxx-dns-xxx",
"fqdn": "myNatClusterxxx-dns-xxx.xxxxx.xxxxxx.cloudapp.azure.com",
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx",
"name": "myNatClusterxxx",
...
"resourceGroup": "myResourceGroupxxx",
...
"provisioningState": "Succeeded",
...
"type": "Microsoft.ContainerService/ManagedClusters"
}
```


- Update the outbound IP address or idle timeout using the
command with the`az aks update`

`--nat-gateway-managed-outbound-ip-count`

or`--nat-gateway-idle-timeout`

parameter.

The following example updates the NAT gateway managed outbound IP count for the AKS cluster to 5.

```
az aks update \
--resource-group $MY_RG \
--name $MY_AKS \
--nat-gateway-managed-outbound-ip-count 5
```


Results:

```
{
"aadProfile": null,
"agentPoolProfiles": [
{
...
"name": "nodepool1",
...
"provisioningState": "Succeeded",
...
}
],
"dnsPrefix": "myNatClusterxxx-dns-xxx",
"fqdn": "myNatClusterxxx-dns-xxx.xxxxx.xxxxxx.cloudapp.azure.com",
"id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx",
"name": "myNatClusterxxx",
...
"resourceGroup": "myResourceGroupxxx",
...
"provisioningState": "Succeeded",
...
"type": "Microsoft.ContainerService/ManagedClusters"
}
```


## Create an AKS cluster with a user-assigned NAT gateway

This configuration requires bring-your-own networking (via [Kubenet](configure-kubenet) or [Azure CNI](configure-azure-cni)) and that the NAT gateway is preconfigured on the subnet. The following commands create the required resources for this scenario.

Create a resource group using the

command.`az group create`

`export RANDOM_SUFFIX=$(openssl rand -hex 3) export MY_RG="myResourceGroup$RANDOM_SUFFIX" az group create --name $MY_RG --location southcentralus`

Results:

`{ "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx", "location": "southcentralus", "managedBy": null, "name": "myResourceGroupxxx", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`

Create a managed identity for network permissions and store the ID to

`$IDENTITY_ID`

for later use.`export IDENTITY_NAME="myNatClusterId$RANDOM_SUFFIX" export IDENTITY_ID=$(az identity create \ --resource-group $MY_RG \ --name $IDENTITY_NAME \ --location southcentralus \ --query id \ --output tsv)`

Results:

`/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myNatClusterIdxxx`

Create a public IP for the NAT gateway using the

command.`az network public-ip create`

`export PIP_NAME="myNatGatewayPip$RANDOM_SUFFIX" az network public-ip create \ --resource-group $MY_RG \ --name $PIP_NAME \ --location southcentralus \ --sku standard`

Results:

`{ "publicIp": { "ddosSettings": null, "dnsSettings": null, "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/publicIPAddresses/myNatGatewayPipxxx", "ipAddress": null, "ipTags": [], "location": "southcentralus", "name": "myNatGatewayPipxxx", ... "provisioningState": "Succeeded", ... "sku": { "name": "Standard", "tier": "Regional" }, "type": "Microsoft.Network/publicIPAddresses", ... } }`

Create the NAT gateway using the

command.`az network nat gateway create`

`export NATGATEWAY_NAME="myNatGateway$RANDOM_SUFFIX" az network nat gateway create \ --resource-group $MY_RG \ --name $NATGATEWAY_NAME \ --location southcentralus \ --public-ip-addresses $PIP_NAME`

Results:

`{ "etag": "W/\"xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx\"", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/natGateways/myNatGatewayxxx", "location": "southcentralus", "name": "myNatGatewayxxx", "provisioningState": "Succeeded", "publicIpAddresses": [ { "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/publicIPAddresses/myNatGatewayPipxxx" } ], ... "type": "Microsoft.Network/natGateways" }`

Important

A single NAT gateway resource can't be used across multiple availability zones. To ensure zone-resiliency, it is recommended to deploy a NAT gateway resource to each availability zone and assign to subnets containing AKS clusters in each zone. For more information on this deployment model, see

[NAT gateway for each zone](/en-us/azure/nat-gateway/nat-availability-zones#zonal-nat-gateway-resource-for-each-zone-in-a-region-to-create-zone-resiliency). If no zone is configured for NAT gateway, the default zone placement is "no zone", in which Azure places NAT gateway into a zone for you.Create a virtual network using the

command.`az network vnet create`

`export VNET_NAME="myVnet$RANDOM_SUFFIX" az network vnet create \ --resource-group $MY_RG \ --name $VNET_NAME \ --location southcentralus \ --address-prefixes 172.16.0.0/20`

Results:

`{ "newVNet": { "addressSpace": { "addressPrefixes": [ "172.16.0.0/20" ] }, ... "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/virtualNetworks/myVnetxxx", "location": "southcentralus", "name": "myVnetxxx", "provisioningState": "Succeeded", ... "type": "Microsoft.Network/virtualNetworks", ... } }`

Create a subnet in the virtual network using the NAT gateway and store the ID to

`$SUBNET_ID`

for later use.`export SUBNET_NAME="myNatCluster$RANDOM_SUFFIX" export SUBNET_ID=$(az network vnet subnet create \ --resource-group $MY_RG \ --vnet-name $VNET_NAME \ --name $SUBNET_NAME \ --address-prefixes 172.16.0.0/22 \ --nat-gateway $NATGATEWAY_NAME \ --query id \ --output tsv)`

Results:

`/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.Network/virtualNetworks/myVnetxxx/subnets/myNatClusterxxx`

Create an AKS cluster using the subnet with the NAT gateway and the managed identity using the

command.`az aks create`

`export AKS_NAME="myNatCluster$RANDOM_SUFFIX" az aks create \ --resource-group $MY_RG \ --name $AKS_NAME \ --location southcentralus \ --network-plugin azure \ --vnet-subnet-id $SUBNET_ID \ --outbound-type userAssignedNATGateway \ --assign-identity $IDENTITY_ID \ --generate-ssh-keys`

Results:

`{ "aadProfile": null, "agentPoolProfiles": [ { ... "name": "nodepool1", ... "provisioningState": "Succeeded", ... } ], "dnsPrefix": "myNatClusterxxx-dns-xxx", "fqdn": "myNatClusterxxx-dns-xxx.xxxxx.xxxxxx.cloudapp.azure.com", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx", "name": "myNatClusterxxx", ... "resourceGroup": "myResourceGroupxxx", ... "provisioningState": "Succeeded", ... "type": "Microsoft.ContainerService/ManagedClusters" }`


## Disable OutboundNAT for Windows

Windows OutboundNAT can cause certain connection and communication issues with your AKS pods. An example issue is node port reuse. In this example, Windows OutboundNAT uses ports to translate your pod IP to your Windows node host IP, which can cause an unstable connection to the external service due to a port exhaustion issue.

Windows enables OutboundNAT by default. You can now manually disable OutboundNAT when creating new Windows agent pools.

### Prerequisites

- Existing AKS cluster with v1.26 or above. If you're using Kubernetes version 1.25 or older, you need to
[update your deployment configuration](tutorial-kubernetes-upgrade-cluster).

### Limitations

- You can't set cluster outbound type to LoadBalancer. You can set it to NAT Gateway or UDR:
[NAT Gateway](nat-gateway): NAT Gateway can automatically handle NAT connection and is more powerful than Standard Load Balancer. You might incur extra charges with this option.[UDR (UserDefinedRouting)](limit-egress-traffic): You must keep port limitations in mind when configuring routing rules.- If you need to switch from a load balancer to NAT Gateway, you can either add a NAT gateway into the VNet or run
to update the outbound type.`az aks upgrade`


Note

UserDefinedRouting has the following limitations:

- SNAT by Load Balancer (must use the default OutboundNAT) has "64 ports on the host IP".
- SNAT by Azure Firewall (disable OutboundNAT) has 2496 ports per public IP.
- SNAT by NAT Gateway (disable OutboundNAT) has 64512 ports per public IP.
- If the Azure Firewall port range isn't enough for your application, you need to use NAT Gateway.
- Azure Firewall doesn't SNAT with Network rules when the destination IP address is in a private IP address range per
[IANA RFC 1918 or shared address space per IANA RFC 6598](/en-us/azure/firewall/snat-private-range).

### Manually disable OutboundNAT for Windows

Manually disable OutboundNAT for Windows when creating new Windows agent pools using the

command with the`az aks nodepool add`

`--disable-windows-outbound-nat`

flag.Note

You can use an existing AKS cluster, but you might need to update the outbound type and add a node pool to enable

`--disable-windows-outbound-nat`

.The following command adds a Windows node pool to an existing AKS cluster, disabling OutboundNAT.

`export WIN_NODEPOOL_NAME="win$(head -c 1 /dev/urandom | xxd -p)" az aks nodepool add \ --resource-group $MY_RG \ --cluster-name $MY_AKS \ --name $WIN_NODEPOOL_NAME \ --node-count 3 \ --os-type Windows \ --disable-windows-outbound-nat`

Results:

`{ "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourceGroups/myResourceGroupxxx/providers/Microsoft.ContainerService/managedClusters/myNatClusterxxx/agentPools/mynpxxx", "name": "mynpxxx", "osType": "Windows", "provisioningState": "Succeeded", "resourceGroup": "myResourceGroupxxx", "type": "Microsoft.ContainerService/managedClusters/agentPools" }`


## Next steps

For more information on Azure NAT Gateway, see [Azure NAT Gateway](/en-us/azure/virtual-network/nat-gateway/nat-overview).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-legacy-cni -->

# AKS Legacy Container Networking Interfaces (CNI)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

In Azure Kubernetes Service (AKS), while [Azure CNI Overlay](concepts-network-azure-cni-overlay) and [Azure CNI Pod Subnet](concepts-network-azure-cni-pod-subnet) are recommended for most scenarios, legacy networking models such as Azure CNI Node Subnet and kubenet are still available and supported. These legacy models offer different approaches to pod IP address management and networking, each with its own set of capabilities and considerations. This article provides an overview of these legacy networking options, detailing their prerequisites, deployment parameters, and key characteristics to help you understand their roles and how they can be used effectively within your AKS clusters.

## Prerequisites

The following prerequisites are required for Azure CNI Node Subnet:

The virtual network for the AKS cluster must allow outbound internet connectivity.

AKS clusters can't use

`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

for the Kubernetes service address range, pod address range, or cluster virtual network address range.The cluster identity used by the AKS cluster must have at least

[Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor)permissions on the subnet within the virtual network. If you want to define a[custom role](/en-us/azure/role-based-access-control/custom-roles)instead of using the built-in Network Contributor role, the following permissions are required:`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`

`Microsoft.Authorization/roleAssignments/write`


The subnet assigned to the AKS node pool can't be a

[delegated subnet](/en-us/azure/virtual-network/subnet-delegation-overview).

- AKS doesn't apply Network Security Groups (NSGs) to its subnet and doesn't modify any of the NSGs associated with that subnet. If you provide your own subnet and add NSGs associated with that subnet, make sure the security rules in the NSGs allow traffic within the node CIDR range. For more information, see
[Network security groups](concepts-network#network-security-groups).

## Azure CNI Node Subnet

With [Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod. These IP addresses must be unique across your network space and must be planned in advance. Each node has a configuration parameter for the maximum number of pods that it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow.

With Azure CNI Node Subnet, each pod receives an IP address in the IP subnet and can communicate directly with other pods and services. Your clusters can be as large as the IP address range you specify. However, you must plan the IP address range in advance, and all the IP addresses are consumed by the AKS nodes based on the maximum number of pods they can support. Advanced network features and scenarios such as [virtual nodes](virtual-nodes-cli) or Network Policies (either Azure or Calico) are supported with Azure CNI.

### Deployment parameters

When you create an AKS cluster, the following parameters are configurable for Azure CNI networking:

**Virtual network**: The virtual network into which you want to deploy the Kubernetes cluster. You can create a new virtual network or use an existing one. If you want to use an existing virtual network, make sure it's in the same location and Azure subscription as your Kubernetes cluster. For information about the limits and quotas for an Azure virtual network, see [Azure subscription and service limits, quotas, and constraints](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#azure-resource-manager-virtual-networking-limits).

**Subnet**: The subnet within the virtual network where you want to deploy the cluster. You can add new subnets into the virtual network during the cluster creation process. For hybrid connectivity, the address range shouldn't overlap with any other virtual networks in your environment.

**Azure Network Plugin**: When Azure network plugin is used, the internal LoadBalancer service with "externalTrafficPolicy=Local" can't be accessed from VMs with an IP in clusterCIDR that doesn't belong to AKS cluster.

**Kubernetes service address range**: This parameter is the set of virtual IPs that Kubernetes assigns to internal [services](concepts-network-services) in your cluster. This range can't be updated after you create your cluster. You can use any private address range that satisfies the following requirements:

- Must not be within the virtual network IP address range of your cluster.
- Must not overlap with any other virtual networks with which the cluster virtual network peers.
- Must not overlap with any on-premises IPs.
- Must not be within the ranges
`169.254.0.0/16`

,`172.30.0.0/16`

,`172.31.0.0/16`

, or`192.0.2.0/24`

.

While it's possible to specify a service address range within the same virtual network as your cluster, we don't recommend it. Overlapping IP ranges can result in unpredictable behavior. For more information, see the [FAQ](#azure-cni-pod-subnet-frequently-asked-questions). For more information on Kubernetes services, see [Services](concepts-network-services) in the Kubernetes documentation.

**Kubernetes DNS service IP address**: The IP address for the cluster's DNS service. This address must be within the *Kubernetes service address range*. Don't use the first IP address in your address range. The first address in your subnet range is used for the *kubernetes.default.svc.cluster.local* address.

**Azure CNI**: That same basic*/24*subnet range can only support a maximum of*8*nodes in the cluster. This node count can only support up to*240*pods, with a default maximum of 30 pods per node.

Note

These maximums don't take into account upgrade or scale operations. In practice, you can't run the maximum number of nodes the subnet IP address range supports. You must leave some IP addresses available for scaling or upgrading operations.

## Virtual network peering and ExpressRoute connections

You can use [Azure virtual network peering](/en-us/azure/virtual-network/virtual-network-peering-overview) or [ExpressRoute connections](/en-us/azure/expressroute/expressroute-introduction) with *Azure CNI* to provide on-premises connectivity. Make sure you plan your IP addresses carefully to prevent overlap and incorrect traffic routing. For example, many on-premises networks use a *10.0.0.0/8* address range that's advertised over the ExpressRoute connection. We recommend creating your AKS clusters in Azure virtual network subnets outside of this address range, such as *172.16.0.0/16*.

For more information, see [Compare network models and their support scopes](concepts-network-cni-overview).

## Azure CNI Pod Subnet frequently asked questions

**Can I deploy VMs in my cluster subnet?**Yes for Azure CNI Node Subnet, the VMs can be deployed in the same subnet as the AKS cluster.

**What source IP do external systems see for traffic that originates in an Azure CNI-enabled pod?**Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod. But for

[Azure CNI dynamic IP allocation](concepts-network-azure-cni-pod-subnet#dynamic-ip-allocation-mode), no matter the connection is inside the same virtual network or cross virtual networks, the pod IP is always the source address for any traffic from the pod. This is because the[Azure CNI for dynamic IP allocation](concepts-network-azure-cni-pod-subnet#dynamic-ip-allocation-mode)implements[Microsoft Azure Container Networking](https://github.com/Azure/azure-container-networking)infrastructure, which gives end-to-end experience. Hence, it eliminates the use of, which is still used by traditional Azure CNI.`ip-masq-agent`

**Can I configure per-pod network policies?**Yes, Kubernetes network policy is available in AKS. To get started, see

[Secure traffic between pods by using network policies in AKS](use-network-policies).**Is the maximum number of pods deployable to a node configurable?**With

[Azure Container Networking Interface (CNI)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md), every pod gets an IP address from the subnet and can be accessed directly. Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod. These IP addresses must be unique across your network space and must be planned in advance. Each node has a configuration parameter for the maximum number of pods that it supports. The equivalent number of IP addresses per node are then reserved up front for that node. This approach requires more planning, and often leads to IP address exhaustion or the need to rebuild clusters in a larger subnet as your application demands grow.**Can I deploy VMs in my cluster subnet?**Yes. But for

[Azure CNI for dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation), the VMs cannot be deployed in pod's subnet.**What source IP do external systems see for traffic that originates in an Azure CNI-enabled pod?**Systems in the same virtual network as the AKS cluster see the pod IP as the source address for any traffic from the pod. Systems outside the AKS cluster virtual network see the node IP as the source address for any traffic from the pod.

But for

[Azure CNI for dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation), no matter the connection is inside the same virtual network or cross virtual networks, the pod IP is always the source address for any traffic from the pod. This is because the[Azure CNI for dynamic IP allocation](configure-azure-cni-dynamic-ip-allocation)implements[Microsoft Azure Container Networking](https://github.com/Azure/azure-container-networking)infrastructure, which gives end-to-end experience. Hence, it eliminates the use of, which is still used by traditional Azure CNI.`ip-masq-agent`

**Can I use a different subnet within my cluster virtual network for the***Kubernetes service address range*?It's not recommended, but this configuration is possible. The service address range is a set of virtual IPs (VIPs) that Kubernetes assigns to internal services in your cluster. Azure Networking has no visibility into the service IP range of the Kubernetes cluster. The lack of visibility into the cluster's service address range can lead to issues. It's possible to later create a new subnet in the cluster virtual network that overlaps with the service address range. If such an overlap occurs, Kubernetes could assign a service an IP that's already in use by another resource in the subnet, causing unpredictable behavior or failures. By ensuring you use an address range outside the cluster's virtual network, you can avoid this overlap risk. Yes, when you deploy a cluster with the Azure CLI or a Resource Manager template. See

[Maximum pods per node](concepts-network-ip-address-planning#maximum-pods-per-node).**Can I use a different subnet within my cluster virtual network for the***Kubernetes service address range*?It's not recommended, but this configuration is possible. The service address range is a set of virtual IPs (VIPs) that Kubernetes assigns to internal services in your cluster. Azure Networking has no visibility into the service IP range of the Kubernetes cluster. The lack of visibility into the cluster's service address range can lead to issues. It's possible to later create a new subnet in the cluster virtual network that overlaps with the service address range. If such an overlap occurs, Kubernetes could assign a service an IP that's already in use by another resource in the subnet, causing unpredictable behavior or failures. By ensuring you use an address range outside the cluster's virtual network, you can avoid this overlap risk.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-fqdn-filtering-concepts -->

# Overview of FQDN filtering

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Containerized environments present unique security challenges. Traditional network security methods, often reliant on IP-based filtering, can become cumbersome and less effective as IP addresses frequently change. Additionally, understanding network traffic patterns and identifying potential threats can be complex.

FQDN filtering offers an efficient and user-friendly approach for managing network policies. By defining these policies based on domain names rather than IP addresses, organizations can significantly simplify the process of policy management. This approach eliminates the need for frequent updates that are typically required when IP addresses change, as a result reducing the administrative burden and minimizing the risk of configuration errors.

In a Kubernetes cluster, pod IP addresses can change often, which makes it challenging to secure the pods with security policies using IP addresses. FQDN filtering allows you to create pod level policies using domain names rather than IP addresses, which eliminates the need to update policies when an IP address changes.

Note

Azure CNI Powered by Cilium and Kubernetes version 1.29 or greater is required in order to use Container Network security features of Advanced Container Networking Services.

## Components of FQDN filtering

**Cilium Agent**: The Cilium Agent is a critical networking component that runs as a DaemonSet within Azure CNI clusters powered by Cilium. It handles networking, load balancing, and network policies for pods in the cluster. For pods with enforced FQDN policies, the Cilium Agent redirects packets to the ACNS Security Agent for DNS resolution and updates the network policy using the FQDN-IP mappings obtained from the ACNS Security Agent.

**ACNS Security Agent**: ACNS Security Agent runs as DaemonSet in Azure CNI powered by Cilium cluster with Advanced Container Networking services enabled. It handles DNS resolution for pods and on successful DNS resolution, it updates Cilium Agent with FQDN to IP mappings.

## How FQDN filtering works

When FQDN Filtering is enabled, DNS requests are first evaluated to determine if they should be allowed after which pods can only access specified domain names based on the network policy. The Cilium Agent marks DNS request packets originating from the pods, redirecting them to the ACNS Security Agent. This redirection occurs only for pods that are enforcing FQDN policies.

The ACNS Security Agent then decides whether to forward a DNS request to the DNS server based on the policy criteria. If permitted, the request is sent to the DNS server, and upon receiving the response, the ACNS Security Agent updates the Cilium Agent with FQDN mappings. This allows the Cilium Agent to update the network policy within the policy engine. The following image illustrates the high-level flow of FQDN Filtering.

## Key benefits

**Scalable security policy management**: Cluster and security admins don't have to update security policies each time an IP address changes making operations more efficient.

**Enhanced security compliance**: FQDN filtering supports a Zero Trust security model. Network traffic is restricted to trusted domains only mitigating risks from unauthorized access.

**Resilient Policy enforcement**: The ACNS Security Agent that is implemented with FQDN filtering ensures that DNS resolution continues seamlessly even if the Cilium agent goes down and policies continue to remain enforced. This implementation critically ensures that security and stability are maintained in dynamic and distributed environments.

## Considerations:

Container Network Security features require Azure CNI Powered by Cilium and Kubernetes version 1.29 and above.

Supported by

`CiliumClusterwideNetworkPolicy`

(CCNP): FQDN filtering can be applied cluster wide via`CiliumClusterwideNetworkPolicy`

.

## Limitations:

- Wildcard FQDN policies are partially supported. This means you can create policies that match specific patterns with a leading wildcard (for example,
*.example.com), but you cannot use a universal wildcard (*) to match all domains on the field`spec.egress.toPorts.rules.dns.matchPattern`


Supported Pattern:

`*.example.com`

- This allows traffic to all subdomains under example.com.`app*.example.com`

- This rule is more specific and only allows traffic to subdomains that start with "app" under example.comUnsupported Pattern

`*`

This attempts to match any domain name, which isn't supported.

- FQDN filtering is currently not supported with node-local DNS.
- Kubernetes service names aren't supported.
- Other L7 policies aren't supported.
- FQDN pods may exhibit performance degradation when handling more than 1,000 requests per second.
- If Advanced Container Networking Services(ACNS) security is disabled, FQDN and L7 policies (HTTP(s), Kafka and gRPC) will be blocked.
- Alpine-based container images may encounter DNS resolution issues when used with Cilium Network Policies. This is due to musl libc's limited search domain iteration. To work around this, explicitly define all search domains in the Network Policy's DNS rules using wildcard patterns, like the below example

```
rules:
dns:
- matchPattern: "*.example.com"
- matchPattern: "*.example.com.*.*"
- matchPattern: "*.example.com.*.*.*"
- matchPattern: "*.example.com.*.*.*.*"
- matchPattern: "*.example.com.*.*.*.*.*"
- toFQDNs:
- matchPattern: "*.example.com"
```


## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[fqdn filtering policies](how-to-apply-fqdn-filtering-policies)on AKS.Explore how the open source community builds

[Cilium Network Policies](https://docs.cilium.io/en/latest/security/policy/).For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](advanced-container-networking-services-overview#container-network-observability).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-app-configuration -->

# Install Azure App Configuration AKS extension

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Azure App Configuration](/en-us/azure/azure-app-configuration/overview) provides a service to centrally manage application settings and feature flags. [Azure App Configuration Kubernetes Provider](https://mcr.microsoft.com/en-us/product/azure-app-configuration/kubernetes-provider/about) is a Kubernetes operator that gets key-values, Key Vault references and feature flags from Azure App Configuration and builds them into Kubernetes ConfigMaps and Secrets. Azure App Configuration extension for Azure Kubernetes Service (AKS) allows you to install and manage Azure App Configuration Kubernetes Provider on your AKS cluster via Azure Resource Manager (ARM).

## Prerequisites

- An Azure subscription.
[Create a free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli). - An Azure Kubernetes Service (AKS) cluster.
[Create an AKS cluster](/en-us/azure/aks/tutorial-kubernetes-deploy-cluster#create-a-kubernetes-cluster). - Permission with the
[Azure Kubernetes Service RBAC Admin](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)role.

### Set up the Azure CLI extension for cluster extensions

Install the `k8s-extension`

Azure CLI extension by running the following commands:

```
az extension add --name k8s-extension
```


If the `k8s-extension`

extension is already installed, you can update it to the latest version using the following command:

```
az extension update --name k8s-extension
```


### Register the `KubernetesConfiguration`

resource provider

If you haven't previously used cluster extensions, you may need to register the resource provider with your subscription. You can check the status of the provider registration using the [az provider list](/en-us/cli/azure/provider#az-provider-list) command, as shown in the following example:

```
az provider list --query "[?namespace=='Microsoft.KubernetesConfiguration']" -o table
```


The *Microsoft.KubernetesConfiguration* provider should report as *Registered*, as shown in the following example output:

```
Namespace RegistrationState RegistrationPolicy
--------------------------------- ------------------- --------------------
Microsoft.KubernetesConfiguration Registered RegistrationRequired
```


If the provider shows as *NotRegistered*, register the provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) as shown in the following example:

```
az provider register --namespace Microsoft.KubernetesConfiguration
```


## Install the extension on your AKS cluster

Create the Azure App Configuration extension, which installs Azure App Configuration Kubernetes Provider on your AKS.

For example, install the latest version of Azure App Configuration Kubernetes Provider via the Azure App Configuration extension on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration
```


Important

The Azure App Configuration AKS extension is installed into the `azappconfig-system`

namespace by default. If you have Azure Policy assignments that validate or mutate pod specifications (for example, the built-in policy "Kubernetes clusters should disable automounting API credentials" which enforces `automountServiceAccountToken: false`

), exclude the `azappconfig-system`

namespace from those policies by adding it to the policy's namespace exclusion list so the extension can function correctly. Not excluding it may cause the extension pods to fail validation or appear non-compliant.

### Configure automatic updates

If you create Azure App Configuration extension without specifying a version, `--auto-upgrade-minor-version`

*is automatically enabled*, configuring the Azure App Configuration extension to automatically update its minor version on new releases.

You can disable auto update by specifying the `--auto-upgrade-minor-version`

parameter and setting the value to `false`

.

### Targeting a specific version

The same command-line argument is used for installing a specific version of Azure App Configuration Kubernetes Provider or rolling back to a previous version. Set `--auto-upgrade-minor-version`

to `false`

and `--version`

to the version of Azure App Configuration Kubernetes Provider you wish to install. If the `version`

parameter is omitted, the extension installs the latest version.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name appconfigurationkubernetesprovider \
--extension-type Microsoft.AppConfiguration \
--auto-upgrade-minor-version false
--version 2.1.0
```


## Extension versions

The Azure App Configuration extension supports the following version of Azure App Configuration Kubernetes Provider:

`2.1.0`

`2.0.0`


## Troubleshoot extension installation errors

If the extension fails to create or update, try suggestions and solutions in the [Azure App Configuration extension troubleshooting guide](/en-us/troubleshoot/azure/azure-kubernetes/extensions/troubleshoot-app-configuration-extension-installation-errors).

## Troubleshoot Azure App Configuration Kubernetes Provider

Troubleshoot Azure App Configuration Kubernetes Provider errors via the [troubleshooting guide](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service#troubleshooting).

## Delete the extension

If you need to delete the extension and remove Azure App Configuration Kubernetes Provider from your AKS cluster, you can use the following command:

```
az k8s-extension delete --resource-group myResourceGroup --cluster-name myAKSCluster --cluster-type managedClusters --name appconfigurationkubernetesprovider
```


## Next Steps

- Learn more about
[extra settings and preferences you can set on the Azure App Configuration extension](azure-app-configuration-settings). - Once you successfully install Azure App Configuration extension in your AKS cluster, try
[quickstart](/en-us/azure/azure-app-configuration/quickstart-azure-kubernetes-service)to learn how to use it. - See all the supported features of
[Azure App Configuration Kubernetes Provider](/en-us/azure/azure-app-configuration/reference-kubernetes-provider).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/cluster-autoscaler-overview -->

# Cluster autoscaling in Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To keep up with application demands in Azure Kubernetes Service (AKS), you might need to adjust the number of nodes that run your workloads. The cluster autoscaler component watches for pods in your cluster that can't be scheduled because of resource constraints. When the cluster autoscaler detects unscheduled pods, it scales up the number of nodes in the node pool to meet the application demand. It also regularly checks nodes that don't have any scheduled pods and scales down the number of nodes as needed.

This article helps you understand how the cluster autoscaler works in AKS. It also provides guidance, best practices, and considerations when configuring the cluster autoscaler for your AKS workloads. If you want to enable, disable, or update the cluster autoscaler for your AKS workloads, see [Use the cluster autoscaler in AKS](cluster-autoscaler).

## About the cluster autoscaler

Clusters often need a way to scale automatically to adjust to changing application demands, such as between workdays and evenings or weekends. AKS clusters can scale in the following ways:

- The
**cluster autoscaler**periodically checks for pods that can't be scheduled on nodes because of resource constraints. The cluster then automatically increases the number of nodes. Manual scaling is disabled when you use the cluster autoscaler. For more information, see[How does scale up work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-up-work). - The
uses the Metrics Server in a Kubernetes cluster to monitor the resource demand of pods. If an application needs more resources, the number of pods is automatically increased to meet the demand.[Horizontal Pod Autoscaler](concepts-scale#horizontal-pod-autoscaler) - The
automatically sets resource requests and limits on containers per workload based on past usage to ensure pods are scheduled onto nodes that have the required CPU and memory resources.[Vertical Pod Autoscaler](vertical-pod-autoscaler)


It's a common practice to enable cluster autoscaler for nodes and either the Vertical Pod Autoscaler or Horizontal Pod Autoscaler for pods. When you enable the cluster autoscaler, it applies the specified scaling rules when the node pool size is lower than the minimum node count, up to the maximum node count. The cluster autoscaler waits to take effect until a new node is needed in the node pool or until a node might be safely deleted from the current node pool. For more information, see [How does scale down work?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-scale-down-work)

## Best practices and considerations

- When implementing
**availability zones with the cluster autoscaler**, we recommend using a single node pool for each zone. You can set the`--balance-similar-node-groups`

parameter to`True`

to maintain a balanced distribution of nodes across zones for your workloads during scale up operations. When this approach isn't implemented, scale down operations can disrupt the balance of nodes across zones.

Note

The Cluster Autoscaler is not zone-aware, and zone allocation is handled by the underlying Virtual Machine Scale Sets. The above best practice becomes even more relevant when using zone-based [pod topology spread constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/) on a single multi-zonal node pool, as restrictive constraints may leave pods in a pending state, especially in capacity-constrained regions or during zone-down scenarios.

For

**clusters with more than 400 nodes**, we recommend using Azure CNI or Azure CNI Overlay.To

**effectively run workloads concurrently on both Spot and On-demand node pools**, consider using. This approach allows you to scale out nodepools based on assigned priority. The following configuration illustrates this setup.*priority expanders*`apiVersion: v1 kind: ConfigMap metadata: name: cluster-autoscaler-priority-expander namespace: kube-system data: priorities: |- 10: - .*spotpool1.* - .*spotpool2.* 50: - .*ondemandpool1.*`

Exercise caution when

**assigning CPU/Memory requests on pods**. The cluster autoscaler scales up based on pending pods rather than CPU/Memory pressure on nodes.For

**clusters concurrently hosting both long-running workloads, like web apps, and short/bursty job workloads**, we recommend separating them into distinct node pools with[Affinity Rules](operator-best-practices-advanced-scheduler#node-affinity)/[expanders](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-are-expanders).Use

[PodDisruptionBudget](https://kubernetes.io/docs/tasks/run-application/configure-pdb/)to help prevent unnecessary node drain or scale down operations. Specifying the annotation[cluster-autoscaler.kubernetes.io/safe-to-evict: "false"](https://kubernetes.io/docs/reference/labels-annotations-taints/#cluster-autoscaler-kubernetes-io-safe-to-evict)on the Pod spec will also prevent the pods from being evicted. Use this annotation with caution, as it may cause the Cluster Autoscaler encounter issues when draining a node with a running Pod that includes this annotation.In an autoscaler-enabled node pool, scale down nodes by removing workloads, instead of manually reducing the min/ max count of the node pool. This can be problematic if the node pool is already at maximum capacity or if there are active workloads running on the nodes, potentially causing unexpected behavior by the cluster autoscaler.

Nodes don't scale up if pods have a PriorityClass value below -10. Priority -10 is reserved for

[overprovisioning pods](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-can-i-configure-overprovisioning-with-cluster-autoscaler). For more information, see[Using the cluster autoscaler with Pod Priority and Preemption](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#how-does-cluster-autoscaler-work-with-pod-priority-and-preemption).**Don't combine other node autoscaling mechanisms**, such as Virtual Machine Scale Set autoscalers, with the cluster autoscaler.The cluster autoscaler

**might be unable to scale down if pods can't move, such as in the following situations**:- A directly created pod not backed by a controller object, such as a Deployment or ReplicaSet.
- A pod disruption budget (PDB) that's too restrictive and doesn't allow the number of pods to fall below a certain threshold.
- A pod uses node selectors or anti-affinity that can't be honored if scheduled on a different node.
For more information, see
[What types of pods can prevent the cluster autoscaler from removing a node?](https://github.com/kubernetes/autoscaler/blob/master/cluster-autoscaler/FAQ.md#what-types-of-pods-can-prevent-ca-from-removing-a-node).


Important

**Don't make changes to individual nodes within the autoscaled node pools**. All nodes in the same node group should have uniform capacity, labels, taints and system pods running on them.

- The cluster autoscaler isn't responsible for enforcing a "maximum node count" in a cluster node pool irrespective of pod scheduling considerations. If any non-cluster autoscaler actor sets the node pool count to a number beyond the cluster autoscaler's configured maximum, the cluster autoscaler doesn't automatically remove nodes. The cluster autoscaler scale down behaviors remain scoped to removing underutilized nodes. The sole purpose of the cluster autoscaler's max node count configuration is to enforce an upper limit for scale up operations. It doesn't have any effect on scale down considerations.

## Cluster autoscaler profile

The [cluster autoscaler profile](cluster-autoscaler#cluster-autoscaler-profile-settings) is a set of parameters that control the behavior of the cluster autoscaler. You can configure the cluster autoscaler profile when you create a cluster or update an existing cluster.

### Optimizing the cluster autoscaler profile

You should fine-tune the cluster autoscaler profile settings according to your specific workload scenarios while also considering tradeoffs between performance and cost. This section provides examples that demonstrate those tradeoffs.

It's important to note that the cluster autoscaler profile settings are cluster-wide and applied to all autoscale-enabled node pools. Any scaling actions that take place in one node pool can affect the autoscaling behavior of other node pools, which can lead to unexpected results. Make sure you apply consistent and synchronized profile configurations across all relevant node pools to ensure you get your desired results.

#### Example 1: Optimizing for performance

For clusters that handle substantial and bursty workloads with a primary focus on performance, we recommend increasing the `scan-interval`

and decreasing the `scale-down-utilization-threshold`

. These settings help batch multiple scaling operations into a single call, optimizing scaling time and the utilization of compute read/write quotas. It also helps mitigate the risk of swift scale down operations on underutilized nodes, enhancing the pod scheduling efficiency. Also increase `ok-total-unready-count`

and `max-total-unready-percentage`

.

For clusters with daemonset pods, we recommend setting `ignore-daemonsets-utilization`

to `true`

, which effectively ignores node utilization by daemonset pods and minimizes unnecessary scale down operations. See [profile for bursty workloads](cluster-autoscaler#configure-cluster-autoscaler-profile-for-bursty-workloads)

#### Example 2: Optimizing for cost

If you want a [cost-optimized profile](cluster-autoscaler#configure-cluster-autoscaler-profile-for-aggressive-scale-down), we recommend setting the following parameter configurations:

- Reduce
`scale-down-unneeded-time`

, which is the amount of time a node should be unneeded before it's eligible for scale down. - Reduce
`scale-down-delay-after-add`

, which is the amount of time to wait after a node is added before considering it for scale down. - Increase
`scale-down-utilization-threshold`

, which is the utilization threshold for removing nodes. - Increase
`max-empty-bulk-delete`

, which is the maximum number of nodes that can be deleted in a single call. - Set
`skip-nodes-with-local-storage`

to false. - Increase
`ok-total-unready-count`

and`max-total-unready-percentage`

.

## Common issues and mitigation recommendations

View scaling failures and scale-up not triggered events via [CLI or Portal](cluster-autoscaler#retrieve-cluster-autoscaler-logs-and-status).

### Not triggering scale up operations

| Common causes | Mitigation recommendations |
|---|---|
| PersistentVolume node affinity conflicts, which can arise when using the cluster autoscaler with multiple availability zones or when a pod's or persistent volume's zone differs from the node's zone. | Use one node pool per availability zone and enabling `--balance-similar-node-groups` . You can also set the
`volumeBindingMode` field to `WaitForFirstConsumer` |
| Taints and Tolerations/Node affinity conflicts | Assess the taints assigned to your nodes and review the tolerations defined in your pods. If necessary, make adjustments to the
|

[Restrictive Pod Topology Spread Constraints](https://kubernetes.io/docs/concepts/scheduling-eviction/topology-spread-constraints/)### Scale up operation failures

| Common causes | Mitigation recommendations |
|---|---|
| IP address exhaustion in the subnet | Add another subnet in the same virtual network and add another node pool into the new subnet. |
| Core quota exhaustion | Approved core quota has been exhausted.
|

[429 Too Many Requests errors](/en-us/troubleshoot/azure/azure-kubernetes/429-too-many-requests-errors).### Scale down operation failures

| Common causes | Mitigation recommendations |
|---|---|
| Pod preventing node drain/Unable to evict pod | • View
• For pods using local storage, such as hostPath and emptyDir, set the cluster autoscaler profile flag `skip-nodes-with-local-storage` to `false` . • In the pod specification, set the `cluster-autoscaler.kubernetes.io/safe-to-evict` annotation to `true` . • Check your
|

[429 Too Many Requests errors](/en-us/troubleshoot/azure/azure-kubernetes/429-too-many-requests-errors).[fully managed AKS resource group](cluster-configuration#fully-managed-resource-group-preview)(see[AKS support policies](support-policies)). Remove or reset any[resource locks](/en-us/azure/azure-resource-manager/management/lock-resources)you previously applied to the resource group.### Other issues

| Common causes | Mitigation recommendations |
|---|---|
| PriorityConfigMapNotMatchedGroup | Make sure that you add all the node groups requiring autoscaling to the
|

### Node pool in backoff

Node pool in backoff was introduced in version 0.6.2 and causes the cluster autoscaler to back off from scaling a node pool after a failure.

Depending on how long the scaling operations have been experiencing failures, it may take up to 30 minutes before making another attempt. You can reset the node pool's backoff state by disabling and then re-enabling autoscaling.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubernetes-service-principal -->

# Use a service principal with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) clusters require either a [Microsoft Entra service principal](/en-us/entra/identity-platform/app-objects-and-service-principals) or a [managed identity](/en-us/azure/active-directory/managed-identities-azure-resources/overview) to dynamically create and manage other Azure resources. This article describes how to create a Microsoft Entra service principal and use it with your AKS cluster.

Note

For optimal security and ease of use, we recommend using managed identities instead of service principals to authorize access from an AKS cluster to other resources in Azure. A managed identity is a special type of service principal that you can use to get Microsoft Entra credentials without the need to manage and secure credentials. For more information, see [Use a managed identity in AKS](use-managed-identity).

## Prerequisites

- You need Azure CLI version 2.0.59 or higher. Find your version using the
`az --version`

command. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

- If using Azure PowerShell, you need Azure PowerShell version 5.0.0 or higher. Find your version using the
`Get-InstalledModule -Name Az`

cmdlet. If you need to install or upgrade, see[Install the Azure Az PowerShell module](/en-us/powershell/azure/install-az-ps).

- You need permissions to register an application with your Microsoft Entra tenant and to assign the application to a role in your subscription. If you don't have the necessary permissions, you need to ask your Microsoft Entra ID or subscription administrator to assign the necessary permissions or create the service principal for you.

## Considerations when using a service principal

Keep the following considerations in mind when using a Microsoft Entra service principal with AKS:

- The service principal for Kubernetes is a part of the cluster configuration, but don't use this identity to deploy the cluster. Instead,
[create a service principal](#create-a-service-principal)first, then use that service principal to create the AKS cluster. - Every service principal is associated with a Microsoft Entra application. You can associate the service principal for a Kubernetes cluster with any valid Microsoft Entra application name (for example:
`https://www.contoso.org/example`

). The URL for the application doesn't have to be a real endpoint. - When you specify the service principal
**client ID**, use the value of the application ID (`appId`

for Azure CLI or`ApplicationId`

for Azure PowerShell). - On the agent node virtual machines (VMs) in the AKS cluster, the service principal credentials are stored in the
`/etc/kubernetes/azure.json`

file. - When you delete an AKS cluster that you created using the
command or the`az aks create`

cmdlet, the service principal created isn't automatically deleted. See the`New-AzAksCluster`

[steps to delete a service principal](#delete-a-service-principal). - If you're using a service principal from a different Microsoft Entra tenant, there are other considerations around the permissions available when you deploy the cluster. You might not have the appropriate permissions to read and write directory information. For more information, see
[What are the default user permissions in Microsoft Entra ID?](/en-us/azure/active-directory/fundamentals/users-default-permissions)

## Create a service principal

Create a service principal using the

command.`az ad sp create-for-rbac`

`# Set environment variable SERVICE_PRINCIPAL_NAME=<your-service-principal-name> # Create the service principal az ad sp create-for-rbac --name $SERVICE_PRINCIPAL_NAME`

Your output should be similar to the following example output:

`{ "appId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "displayName": "myAKSClusterServicePrincipal", "name": "http://myAKSClusterServicePrincipal", "password": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "tenant": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx" }`

Copy the values for

`appId`

and`password`

from the output to use when creating the AKS cluster.

Create a service principal using the

command.`New-AzADServicePrincipal`

`# Set environment variable $SpName = <your-service-principal-name> # Create the service principal New-AzADServicePrincipal -DisplayName $SpName -OutVariable sp`

Your output should be similar to the following example output:

`Secret : System.Security.SecureString ServicePrincipalNames : {xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx, http://myAKSClusterServicePrincipal} ApplicationId : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx ObjectType : ServicePrincipal DisplayName : myAKSClusterServicePrincipal Id : xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx Type :`

The values are stored in a variable that you use when creating the AKS cluster.

Decrypt the value stored in the

**Secret**secure string using the following command.`$BSTR = [System.Runtime.InteropServices.Marshal]::SecureStringToBSTR($sp.Secret) [System.Runtime.InteropServices.Marshal]::PtrToStringAuto($BSTR)`


## Create an AKS cluster with an existing service principal

Create an AKS cluster with an existing service principal using the

command with the`az aks create`

`--service-principal`

and`--client-secret`

parameters set to specify the`appId`

and`password`

values.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> APP_ID=<app-id> CLIENT_SECRET=<password-value> # Create the AKS cluster az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --service-principal $APP_ID \ --client-secret $CLIENT_SECRET \ --generate-ssh-keys`


Convert the service principal

`ApplicationId`

and`Secret`

to a**PSCredential**object using the following command.`$Cred = New-Object -TypeName System.Management.Automation.PSCredential ($sp.ApplicationId, $sp.Secret)`

Create an AKS cluster with an existing service principal using the

cmdlet and specify the`New-AzAksCluster`

`ServicePrincipalIdAndSecret`

parameter with the**PSCredential**object as its value.`# Set environment variables $ResourceGroupName = <your-resource-group-name> $ClusterName = <your-aks-cluster-name> # Create the AKS cluster New-AzAksCluster -ResourceGroupName $ResourceGroupName -Name $ClusterName -ServicePrincipalIdAndSecret $Cred`


Note

If you're using an existing service principal with customized secret, make sure the secret isn't longer than 190 bytes.

## Delegate access to other Azure resources

You can use the service principal for the AKS cluster to access other resources. For example, if you want to deploy your AKS cluster into an existing Azure virtual network (VNet) subnet, connect to ACR, or access keys or secrets in a key vault from your cluster, then you need to delegate access to those resources to the service principal. To delegate access, assign an Azure role-based access control (Azure RBAC) role to the service principal.

When you assign roles, you specify the scope for the role assignment, such as a resource group or VNet resource. The role assignment determines what permissions the service principal has on the resource and at what scope.

Important

Permissions granted to a service principal associated with a cluster can take up 60 minutes to propagate.

## Create a role assignment

Note

The scope for a resource needs to be a full resource ID, such as `/subscriptions/\<guid\>/resourceGroups/myResourceGroup`

or `/subscriptions/\<guid\>/resourceGroups/myResourceGroupVnet/providers/Microsoft.Network/virtualNetworks/myVnet`

.

Create a role assignment using the

command. Specify the value of the service principal app ID for the`az role assignment create`

`--assignee`

parameter and the scope for the role assignment for the`--scope`

parameter. The following example assigns the service principal permissions to access secrets in a key vault:`az role assignment create \ --assignee <app-id> \ --scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.KeyVault/vaults/<vault-name>" \ --role "Key Vault Secrets User"`


Create a role assignment using the

cmdlet. Specify the value of the service principal app ID for the`New-AzRoleAssignment`

`-ApplicationId`

parameter and the scope for the role assignment for the`-Scope`

parameter. The following example assigns the service principal permissions to access secrets in a key vault:`New-AzRoleAssignment -ApplicationId <app-id> ` -Scope "/subscriptions/<subscription-id>/resourceGroups/<resource-group>/providers/Microsoft.KeyVault/vaults/<vault-name>" ` -RoleDefinitionName "Key Vault Secrets User"`


## Grant access to Azure Container Registry

If you use Azure Container Registry (ACR) as your container image store, you need to grant permissions to the service principal for your AKS cluster to read and pull images. We recommend following the steps in [Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration) to integrate with a registry and assign the appropriate role for the service principal.

## Grant access to networking resources

If you're using advanced networking with a VNet and subnet or public IP addresses in different resource group, you can assign the [Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor) built-in role on the subnet within the VNet. Alternatively, you can create a [custom role](/en-us/azure/role-based-access-control/custom-roles) with permissions to access the network resources in that resource group. For more information, see [AKS service permissions](concepts-identity#aks-service-permissions).

## Grant access to storage disks

If you need to access existing disk resources in another resource group, assign one of the following sets of role permissions:

- Create a
[custom role](/en-us/azure/role-based-access-control/custom-roles)and define the*Microsoft.Compute/disks/read*and*Microsoft.Compute/disks/write*role permissions. - Assign the
[Virtual Machine Contributor](/en-us/azure/role-based-access-control/built-in-roles#virtual-machine-contributor)built-in role on the resource group.

## Grant access to Azure Container Instances

If you use virtual kubelet to integrate with AKS and run Azure Container Instances (ACI) in resource group separate from the AKS cluster, you need to assign *Contributor* permissions to the AKS cluster service principal for the ACI resource group.

## Delete a service principal

Query for the service principal client ID (

`servicePrincipalProfile.clientId`

) and delete the service principal using thecommand with the`az ad sp delete`

`--id`

parameter. The [`az aks show`

][az-aks-show] command retrieves the client ID for the specified AKS cluster.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Delete the service principal az ad sp delete --id $(az aks show \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --query servicePrincipalProfile.clientId \ --output tsv)`


Query for the service principal client ID (

`ServicePrincipalProfile.ClientId`

) and delete the service principal using thecmdlet with the`Remove-AzADServicePrincipal`

`-ApplicationId`

parameter. The [`Get-AzAksCluster`

][get-azakscluster] cmdlet retrieves the client ID for the specified AKS cluster.`# Set environment variables $ResourceGroupName = <your-resource-group-name> $ClusterName = <your-aks-cluster-name> $ClientId = (Get-AzAksCluster -ResourceGroupName myResourceGroup -Name myAKSCluster ).ServicePrincipalProfile.ClientId # Delete the service principal Remove-AzADServicePrincipal -ApplicationId $ClientId`


## Resolve service principal credential issues

Azure CLI caches the service principal credentials for AKS clusters.

Azure PowerShell caches the service principal credentials for AKS clusters.

If these credentials expire, you might encounter errors during AKS cluster deployment. If there's an issue with the cached credentials, you might receive an error message similar to the following error message:

```
Operation failed with status: 'Bad Request'.
Details: The credentials in ServicePrincipalProfile were invalid. Please see https://aka.ms/aks-sp-help for more details.
Details: adal: Refresh request failed. Status Code = '401'.
```


You can check the expiration date of your service principal credentials using the [ az ad app credential list](/en-us/cli/azure/ad/app/credential#az-ad-app-credential-list) command with the

`"[].endDateTime"`

query. The output shows you the `endDateTime`

of your credentials.```
az ad app credential list \
--id <app-id> \
--query "[].endDateTime" \
--output tsv
```


- Check the expiration date of your service principal credentials using the
cmdlet. The output shows you the`Get-AzADAppCredential`

`EndDate`

of your credentials.

```
Get-AzADAppCredential -ApplicationId <app-id>
```


**The default expiration time for the service principal credentials is one year**. If your credentials are older than one year, you can [reset the existing credentials](update-credentials#reset-the-existing-service-principal-credentials) or [create a new service principal](update-credentials#create-a-new-service-principal).
