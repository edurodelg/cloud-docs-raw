---
merged_at: 2026-01-26T23:04:05.999677
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-pool-snapshot -->

# Azure Kubernetes Service (AKS) node pool snapshot

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS releases a new node image weekly. Every new cluster, new node pool, or upgrade cluster always receives the latest image, which can make it hard to maintain consistency and have repeatable environments.

Node pool snapshots allow you to take a configuration snapshot of your node pool and then create new node pools or new clusters based of that snapshot for as long as that configuration and kubernetes version is supported. For more information on the supportability windows, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

The snapshot is an Azure resource that contains the configuration information from the source node pool, such as the node image version, kubernetes version, OS type, and OS SKU. You can then reference this snapshot resource and the respective values of its configuration to create any new node pool or cluster based off of it.

## Before you begin

This article assumes that you have an existing AKS cluster. If you don't have an AKS cluster, for guidance on a designing an enterprise-scale implementation of AKS, see [Plan your AKS design](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

### Limitations

- Any node pool or cluster created from a snapshot must use a VM from the same virtual machine family as the snapshot, for example, you can't create a new N-Series node pool based of a snapshot captured from a D-Series node pool because the node images in those cases are structurally different.
- Snapshots must be created same region as the source node pool, those snapshots can be used to create or update clusters and node pools in other regions.

## Take a node pool snapshot

In order to take a snapshot from a node pool, you need the node pool resource ID, which you can get from the following command:

```
NODEPOOL_ID=$(az aks nodepool show --name nodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --query id -o tsv)
```


Important

Your AKS node pool must be created or upgraded after Nov 10th, 2021 in order for a snapshot to be taken from it.
If you are using the `aks-preview`

Azure CLI extension version `0.5.59`

or newer, the commands for node pool snapshot have changed. For updated commands, see the [Node Pool Snapshot CLI reference](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add).

Now, to take a snapshot from the previous node pool, you use the `az aks snapshot`

CLI command.

```
az aks nodepool snapshot create --name MySnapshot --resource-group MyResourceGroup --nodepool-id $NODEPOOL_ID --location eastus
```


## Create a node pool from a snapshot

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use the following command to add a new node pool based off of this snapshot.

```
az aks nodepool add --name np2 --cluster-name myAKSCluster --resource-group myResourceGroup --snapshot-id $SNAPSHOT_ID
```


## Upgrading a node pool to a snapshot

You can upgrade a node pool to a snapshot configuration if the snapshot Kubernetes version and node image version are more recent than the current node pool versions. And the snapshot node image version is within 90 days of the node image publish date.

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use this command to upgrade this node pool to this snapshot configuration.

```
az aks nodepool upgrade --name nodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --snapshot-id $SNAPSHOT_ID
```


Note

Your node pool image version is the same contained in the snapshot and remains the same throughout every scale operation. However, if this node pool is upgraded or a node image upgrade is performed without providing a snapshot-id the node image is upgraded to the latest version.

Note

To upgrade only the node version for your node pool, use the `--node-image-only`

flag. This is required when upgrading the node image version for a node pool based on a snapshot with an identical Kubernetes version.

## Create a cluster from a snapshot

When you create a cluster from a snapshot, the snapshot configuration creates the cluster original system pool.

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use this command to create this cluster off of the snapshot configuration.

```
az aks create \
--name myAKSCluster2 \
--resource-group myResourceGroup \
--snapshot-id $SNAPSHOT_ID \
--generate-ssh-keys
```


## Next steps

- See the
[AKS release notes](https://github.com/Azure/AKS/releases)for information about the latest node images. - Learn how to upgrade the Kubernetes version with
[Upgrade an AKS cluster](upgrade-cluster). - Learn how to upgrade your node image version with
[Node Image Upgrade](node-image-upgrade) - Learn more about multiple node pools with
[Create multiple node pools](create-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-fine-tune-language-models -->

# Concepts - Fine-tuning language models for AI and machine learning workflows

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about fine-tuning [language models](concepts-ai-ml-language-models), including some common methods and how applying the tuning results can improve the performance of your AI and machine learning workflows on Azure Kubernetes Service (AKS).

## Pre-trained language models

*Pre-trained language models (PLMs)* offer an accessible way to get started with AI inferencing and are widely used in natural language processing (NLP). PLMs are trained on large-scale text corpora from the internet using deep neural networks and can be fine-tuned on smaller datasets for specific tasks. These models typically consist of billions of parameters, or *weights*, that are learned during the pre-training process.

PLMs can learn universal language representations that capture the statistical properties of natural language, such as the probability of words or sequences of words occurring in a given context. These representations can be transferred to downstream tasks, such as text classification, named entity recognition, and question answering, by fine-tuning the model on task-specific datasets.

### Pros and cons

The following table lists some pros and cons of using PLMs in your AI and machine learning workflows:

| Pros | Cons |
|---|---|
| • Get started quickly with deployment in your machine learning lifecycle. • Avoid heavy compute costs associated with model training. • Reduces the need to store large, labeled datasets. |
• Might provide generalized or outdated responses based on pre-training data sources. • Might not be suitable for all tasks or domains. • Performance can vary depending on inferencing context. |

## Fine-tuning methods

### Parameter efficient fine-tuning

*Parameter efficient fine-tuning (PEFT)* is a method for fine-tuning PLMs on relatively small datasets with limited compute resources. PEFT uses a combination of techniques, like additive and selective methods to update weights, to improve the performance of the model on specific tasks. PEFT requires minimal compute resources and flexible quantities of data, making it suitable for low-resource settings. This method retains most of the weights of the original pre-trained model and updates the remaining weights to fit context-specific, labeled data.

### Low rank adaptation

*Low rank adaptation (LoRA)* is a PEFT method commonly used to customize large language models for new tasks. This method tracks changes to model weights and efficiently stores smaller weight matrices that represent only the model's trainable parameters, reducing memory usage and the compute power needed for fine-tuning. LoRA creates fine-tuning results, known as *adapter layers*, that can be temporarily stored and pulled into the model's architecture for new inferencing jobs.

*Quantized low rank adaptation (QLoRA)* is an extension of LoRA that further reduces memory usage by introducing quantization to the adapter layers. For more information, see [Making LLMs even more accessible with bitsandbites, 4-bit quantization, and QLoRA](https://huggingface.co/blog/4bit-transformers-bitsandbytes#:%7E:text=We%20present%20QLoRA%2C%20an%20efficient%20finetuning%20approach%20that,pretrained%20language%20model%20into%20Low%20Rank%20Adapters%7E%20%28LoRA%29.).

## Experiment with fine-tuning language models on AKS

Kubernetes AI Toolchain Operator (KAITO) is an open-source operator that automates small and large language model deployments in Kubernetes clusters. The AI toolchain operator add-on leverages KAITO to simplify onboarding, save on infrastructure costs, and reduce the time-to-inference for open-source models on an AKS cluster. The add-on automatically provisions right-sized GPU nodes and sets up the associated inference server as an endpoint server to your chosen model.

With KAITO version 0.3.0 or later, you can efficiently fine-tune supported MIT and Apache 2.0 licensed models with the following features:

- Store your retraining data as a container image in a private container registry.
- Host the new adapter layer image in a private container registry.
- Efficiently pull the image for inferencing with adapter layers in new scenarios.

For guidance on getting started with fine-tuning on KAITO, see the [Kaito Tuning Workspace API documentation][kaito-fine-tuning]. To learn more about deploying language models with KAITO in your AKS clusters, see the [KAITO model GitHub repository](https://github.com/Azure/kaito/tree/main/presets).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Next steps

To learn more about containerized AI and machine learning workloads on AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-scheduler-configuration -->

# Scheduler configuration concepts for workload placement in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers scheduler configuration and advanced scheduling concepts for workload placement in Azure Kubernetes Service (AKS), including configurable scheduler profiles, scheduling plugins, and scheduling constraints.

## About the AKS scheduler

In AKS, the default mechanism of workload placement across nodes within a cluster is through the scheduler. The default scheduler is a control plane component responsible for assigning AKS deployment pods to nodes. Once the AKS scheduler selects a node, the deployment pod is bound to it, and the rest of the lifecycle continues.

When a pod is created without a specified node, the scheduler selects an optimal node based on several criteria, including (but not limited to):

- Available resources (CPU, memory)
[Node affinity/anti-affinity](operator-best-practices-advanced-scheduler#node-affinity)[Pod affinity/anti-affinity](operator-best-practices-advanced-scheduler#inter-pod-affinity-and-anti-affinity)[Taints and tolerations](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

### AKS scheduler configuration and scheduling strategies

By default, the AKS scheduler comes with a set of built-in rules that work well for general-purpose workloads. However, advanced use cases might require custom scheduling strategies. For example:

- Batch jobs might prefer collocating in a few nodes (for better performance) over topology-aware spreading (for reliability).
- Cost-sensitive workloads might benefit from node binpacking to consolidate jobs and minimize idle compute node costs.

To support these use cases, AKS allows you to set one or more in-tree scheduling plugins through a Kubernetes custom resource (CRD) to configure the scheduling behavior on your AKS cluster.

## Configurable scheduler profiles

A scheduler profile is a set of one or more in-tree scheduling plugins and configurations that dictate how to schedule a pod. Previously, AKS managed the scheduler configuration, and it wasn't accessible to users. Starting from Kubernetes version `1.33`

, you can now configure and set a scheduler profile (preview) for the Kubernetes scheduler on your cluster.

Each scheduler profile has the following components:

- A unique name.
- A set of
[scheduling plugins](#supported-in-tree-scheduling-plugins). - Custom arguments for fine-grained behavior (applicable to certain plugins).

## Supported in-tree scheduling plugins

AKS supports configuration of 18 in-tree Kubernetes scheduling plugins that allow pods to be placed on specific nodes, ensure pods are matched with specific storage resources, optimize for nodes with container images, and more.

The following sections walk you through these plugins, which are grouped into the following categories:

[Scheduling constraints and order-based plugins](#scheduling-constraints-and-order-based-plugins)[Node selection constraints scheduling plugins](#node-selection-constraints-scheduling-plugins)[Resource and topology optimization scheduling plugins](#resource-and-topology-optimization-scheduling-plugins)

To learn more about these plugins and configuration options, see the [Kubernetes Scheduling Plugin documentation](https://kubernetes.io/docs/reference/scheduling/config/#scheduling-plugins).

### Scheduling constraints and order-based plugins

`DefaultBinder`

: Responsible for binding the pod to a node after the scheduler selects a suitable node. Once the node is selected, the`DefaultBinder`

creates a binding object to ensure the pod is scheduled onto that node.`DefaultPreemption`

: Handles preemption, which is the process of evicting lower-priority pods to make room for higher-priority pods. If a pod can't be scheduled because there aren’t enough resources on the node, this plugin preempts other pods to make space. This plugin can receive the following arguments:`PodPriority`

: Defines the priority of the pod being scheduled.`PreemptionPolicy`

: The policy for handling pod preemption (for example:`"PreemptLowerPriority"`

or`"DoNotPreempt"`

).`PodPriorityClass`

: The priority class associated with the pod.`PodInfo`

: Information about the pods that are candidates for preemption.`Node`

: Information about the node on which preemption is considered.

`SchedulingGates`

: Introduces the concept of scheduling gates, which are conditions that must be satisfied before a pod is scheduled. For example, it can enforce the completion of certain tasks or operations before the scheduler attempts to schedule a pod.`PrioritySort`

: Sorts the list of pods according to their priority class. Pods with higher priority are scheduled first. It helps with the preemption decision-making and determines which pods to consider for priority scheduling.

### Node selection constraints scheduling plugins

`InterPodAffinity`

: Takes into account*affinity*rules specified by the user that influences scheduling based on the proximity of other pods. If a pod has affinity rules, it tries to schedule the pod on the same node or in the same topology as other pods that it has an affinity for (for example: for performance reasons or tight coupling). This plugin can receive the following arguments:`Affinity`

: Defines required or preferred affinity rules for the pod, which specifies other pods that the pod should or shouldn't be scheduled nearby.`TopologyKey`

: The key representing the failure domain to which the affinity rule applies (for example:`"kubernetes.io/hostname"`

for node-level affinity or`"topology.kubernetes.io/zone"`

for zone-level).`Weight`

: Defines how strongly the scheduler should consider a specific affinity rule.`Pod`

: The pod being scheduled.`OtherPods`

: List of other pods to consider in relation to the affinity rules.

`NodeAffinity`

: Enables scheduling based on node labels. It allows users to specify rules for which nodes a pod can be scheduled on based on the node's labels and provides fine-grained control over pod placement on nodes. This plugin can receive the following arguments:`NodeAffinity`

: Defines the required or preferred node affinity rules, such as`requiredDuringSchedulingIgnoredDuringExecution`

or`preferredDuringSchedulingIgnoredDuringExecution`

.`NodeSelectorTerms`

: Defines the set of node labels and values that must match.`Pod`

: The pod being scheduled.`Node`

: A potential node for scheduling.`LabelSelector`

: A selector for choosing nodes based on labels.

`NodeName`

: Forces pods to be scheduled on a specific node. When you specify the exact node name, the scheduler places the pod on that node if possible.`NodePorts`

: Ensures that a pod with a service of type`NodePort`

can be scheduled on a node that has the required ports available for binding. It checks whether the node has enough resources to support the node port allocations for the service.`NodeUnschedulable`

: Ensures that pods aren't scheduled on nodes marked as*unschedulable*. If a node is tainted with`node.kubernetes.io/unschedulable`

, the scheduler doesn't place any new pods on that node.`TaintToleration`

: Checks if a pod has the required tolerations to be scheduled on a node that has taints. Taints on nodes prevent pods from being scheduled unless the pod has a matching toleration.`NodeVolumeLimits`

: Checks whether a node has exceeded its volume limit. Each node has a maximum number of volumes it can attach, and this plugin ensures that the pod isn't scheduled on a node that has already reached that supported limit.`VolumeBinding`

: Ensures that persistent volumes (PVs) are properly bound to pods. It checks whether the volume that a pod requires can be bound to a node and ensures the volume is available on the selected node. This plugin can receive the following arguments:`VolumeClaims`

: The persistent volume claims (PVCs) made by the pod being scheduled.`Node`

: The candidate node being considered for scheduling.`VolumeAvailable`

: Checks if the persistent volume is available on the node or within the appropriate zone.`Pod`

: The pod that is requesting volume binding.`StorageClass`

: The storage class associated with the persistent volume.`VolumeBindingMode`

: Defines whether the volume binding mode is`Immediate`

or`WaitForFirstConsumer`

(for delayed binding until a pod is scheduled).

`VolumeRestrictions`

: Ensures that volume restrictions (such as limitations on the number of volumes a node can have attached) are respected when scheduling a pod. It prevents scheduling a pod on a node where the volume restrictions would be violated.`VolumeZone`

: Ensures that volumes are scheduled in the same availability zone as the pod. For example, if a pod requests a volume that must be in a specific zone, the plugin ensures that both the pod and the volume are in the same zone.

### Resource and topology optimization scheduling plugins

`NodeResourcesBalancedAllocation`

: Aims to balance the resource allocation on nodes. When scheduling a pod, it considers how resources like CPU and memory are allocated across nodes to avoid overprovisioning or underutilizing resources. This plugin can receive the following arguments:`ResourceRequests`

: The resource requests (CPU, memory, etc.) of the pod being scheduled.`Node`

: A candidate node for scheduling.`NodeResources`

: The available resources (CPU, memory, etc.) of the node.`ClusterResourceUsage`

: Cluster-wide resource usage metrics to help decide the best node to balance resources.

`NodeResourcesFit`

: Checks whether a node has enough available resources (CPU, memory, etc.) to run the pod. It ensures that a pod is only scheduled on a node that has sufficient resources available. This plugin can receive the following arguments:`ResourceRequests`

: The resource requests of the pod.`Node`

: The candidate node being considered for scheduling.`NodeCapacity`

: The available capacity of resources on the node.`Pod`

: The pod being scheduled, with its resource requests.

`ImageLocality`

: Helps the scheduler decide whether to schedule a pod onto a node based on the presence of a required container image. It tries to schedule pods on nodes where the required image is already present, reducing the time needed to pull the image.`PodTopologySpread`

: Ensures that pods are spread evenly across the topology (like zones or regions) to achieve high availability and fault tolerance. It tries to avoid placing multiple replicas of a pod in the same failure domain. This plugin can receive the following arguments:`TopologySpreadConstraints`

: Defines the constraints for how pods should be spread across failure domains, including the key (for example:`topology.kubernetes.io/zone`

) and the number of pods to be placed in each domain.`Pod`

: The pod being scheduled.`FailureDomain`

: The failure domain key (for example: zone or region).`PodAffinity`

: Information about pod affinity, which could also impact how the pods are distributed.`Node`

: Potential nodes for placement.`PodSpreadScore`

: Used to determine how much "spread" the pod should have across domains (higher scores indicate better spreading).


## Next step


[Configure and deploy a scheduler profile (preview) on your AKS cluster].

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/keda-workload-identity -->

# Securely scale your applications using the KEDA add-on and workload identity on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to securely scale your applications with the Kubernetes Event-driven Autoscaling (KEDA) add-on and workload identity on Azure Kubernetes Service (AKS).

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules).

## Create a resource group

Create a resource group using the

command. Make sure you replace the placeholder values with your own values.`az group create`

`LOCATION=<azure-region> RG_NAME=<resource-group-name> az group create --name $RG_NAME --location $LOCATION`


## Create an AKS cluster

Create an AKS cluster with the KEDA add-on, workload identity, and OIDC issuer enabled using the

command with the`az aks create`

`--enable-workload-identity`

,`--enable-keda`

, and`--enable-oidc-issuer`

flags. Make sure you replace the placeholder value with your own value.`AKS_NAME=<cluster-name> az aks create \ --name $AKS_NAME \ --resource-group $RG_NAME \ --enable-workload-identity \ --enable-oidc-issuer \ --enable-keda \ --generate-ssh-keys`

Validate the deployment was successful and make sure the cluster has KEDA, workload identity, and OIDC issuer enabled using the

command with the`az aks show`

`--query`

flag set to`"[workloadAutoScalerProfile, securityProfile, oidcIssuerProfile]"`

.`az aks show \ --name $AKS_NAME \ --resource-group $RG_NAME \ --query "[workloadAutoScalerProfile, securityProfile, oidcIssuerProfile]"`

Connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --name $AKS_NAME \ --resource-group $RG_NAME \ --overwrite-existing`


## Create an Azure Service Bus

Create an Azure Service Bus namespace using the

command. Make sure to replace the placeholder value with your own value.`az servicebus namespace create`

`SB_NAME=<service-bus-name> SB_HOSTNAME="${SB_NAME}.servicebus.windows.net" az servicebus namespace create \ --name $SB_NAME \ --resource-group $RG_NAME \ --disable-local-auth`

Create an Azure Service Bus queue using the

command. Make sure to replace the placeholder value with your own value.`az servicebus queue create`

`SB_QUEUE_NAME=<service-bus-queue-name> az servicebus queue create \ --name $SB_QUEUE_NAME \ --namespace $SB_NAME \ --resource-group $RG_NAME`


## Create a managed identity

Create a managed identity using the

command. Make sure to replace the placeholder value with your own value.`az identity create`

`MI_NAME=<managed-identity-name> MI_CLIENT_ID=$(az identity create \ --name $MI_NAME \ --resource-group $RG_NAME \ --query "clientId" \ --output tsv)`

Get the OIDC issuer URL using the

command with the`az aks show`

`--query`

flag set to`oidcIssuerProfile.issuerUrl`

.`AKS_OIDC_ISSUER=$(az aks show \ --name $AKS_NAME \ --resource-group $RG_NAME \ --query oidcIssuerProfile.issuerUrl \ --output tsv)`

Create a federated credential between the managed identity and the namespace and service account used by the workload using the

command. Make sure to replace the placeholder value with your own value.`az identity federated-credential create`

`FED_WORKLOAD=<federated-credential-workload-name> az identity federated-credential create \ --name $FED_WORKLOAD \ --identity-name $MI_NAME \ --resource-group $RG_NAME \ --issuer $AKS_OIDC_ISSUER \ --subject system:serviceaccount:default:$MI_NAME \ --audience api://AzureADTokenExchange`

Create a second federated credential between the managed identity and the namespace and service account used by the keda-operator using the

command. Make sure to replace the placeholder value with your own value.`az identity federated-credential create`

`FED_KEDA=<federated-credential-keda-name> az identity federated-credential create \ --name $FED_KEDA \ --identity-name $MI_NAME \ --resource-group $RG_NAME \ --issuer $AKS_OIDC_ISSUER \ --subject system:serviceaccount:kube-system:keda-operator \ --audience api://AzureADTokenExchange`


## Create role assignments

Get the object ID for the managed identity using the

command with the`az identity show`

`--query`

flag set to`"principalId"`

.`MI_OBJECT_ID=$(az identity show \ --name $MI_NAME \ --resource-group $RG_NAME \ --query "principalId" \ --output tsv)`

Get the Service Bus namespace resource ID using the

command with the`az servicebus namespace show`

`--query`

flag set to`"id"`

.`SB_ID=$(az servicebus namespace show \ --name $SB_NAME \ --resource-group $RG_NAME \ --query "id" \ --output tsv)`

Assign the Azure Service Bus Data Owner role to the managed identity using the

command.`az role assignment create`

`az role assignment create \ --role "Azure Service Bus Data Owner" \ --assignee-object-id $MI_OBJECT_ID \ --assignee-principal-type ServicePrincipal \ --scope $SB_ID`


## Enable Workload Identity on KEDA operator

After creating the federated credential for the

`keda-operator`

ServiceAccount, you will need to manually restart the`keda-operator`

pods to ensure Workload Identity environment variables are injected into the pod.`kubectl rollout restart deploy keda-operator -n kube-system`

Confirm the keda-operator pods restart

`kubectl get pod -n kube-system -lapp=keda-operator -w`

Once you've confirmed the keda-operator pods have finished rolling hit

`Ctrl+c`

to break the previous watch command then confirm the Workload Identity environment variables have been injected.`KEDA_POD_ID=$(kubectl get po -n kube-system -l app.kubernetes.io/name=keda-operator -ojsonpath='{.items[0].metadata.name}') kubectl describe po $KEDA_POD_ID -n kube-system`

You should see output similar to the following under

**Environment**.`--- AZURE_CLIENT_ID: AZURE_TENANT_ID: xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxx AZURE_FEDERATED_TOKEN_FILE: /var/run/secrets/azure/tokens/azure-identity-token AZURE_AUTHORITY_HOST: https://login.microsoftonline.com/ ---`

Deploy a KEDA TriggerAuthentication resource that includes the User-Assigned Managed Identity's Client ID.

`kubectl apply -f - <<EOF apiVersion: keda.sh/v1alpha1 kind: TriggerAuthentication metadata: name: azure-servicebus-auth namespace: default # this must be same namespace as the ScaledObject/ScaledJob that will use it spec: podIdentity: provider: azure-workload identityId: $MI_CLIENT_ID EOF`

Note

With the TriggerAuthentication in place, KEDA will be able to authenticate via workload identity. The

`keda-operator`

Pods use the`identityId`

to authenticate against Azure resources when evaluating scaling triggers.

## Publish messages to Azure Service Bus

At this point everything is configured for scaling with KEDA and Microsoft Entra Workload Identity. We will test this by deploying producer and consumer workloads.

Create a new ServiceAccount for the workloads.

`kubectl apply -f - <<EOF apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: $MI_CLIENT_ID name: $MI_NAME EOF`

Deploy a Job to publish 100 messages.

`kubectl apply -f - <<EOF apiVersion: batch/v1 kind: Job metadata: name: myproducer spec: template: metadata: labels: azure.workload.identity/use: "true" spec: serviceAccountName: $MI_NAME containers: - image: ghcr.io/azure-samples/aks-app-samples/servicebusdemo:latest name: myproducer resources: {} env: - name: OPERATION_MODE value: "producer" - name: MESSAGE_COUNT value: "100" - name: AZURE_SERVICEBUS_QUEUE_NAME value: $SB_QUEUE_NAME - name: AZURE_SERVICEBUS_HOSTNAME value: $SB_HOSTNAME restartPolicy: Never EOF`


## Consume messages from Azure Service Bus

Now that we have published messages to the Azure Service Bus queue, we will deploy a ScaledJob to consume the messages. This ScaledJob will use the KEDA TriggerAuthentication resource to authenticate against the Azure Service Bus queue using the workload identity and scale out every 10 messages.

Deploy a ScaledJob resource to consume the messages. The scale trigger will be configured to scale out every 10 messages. The KEDA scaler will create 10 jobs to consume the 100 messages.

`kubectl apply -f - <<EOF apiVersion: keda.sh/v1alpha1 kind: ScaledJob metadata: name: myconsumer-scaledjob spec: jobTargetRef: template: metadata: labels: azure.workload.identity/use: "true" spec: serviceAccountName: $MI_NAME containers: - image: ghcr.io/azure-samples/aks-app-samples/servicebusdemo:latest name: myconsumer env: - name: OPERATION_MODE value: "consumer" - name: MESSAGE_COUNT value: "10" - name: AZURE_SERVICEBUS_QUEUE_NAME value: $SB_QUEUE_NAME - name: AZURE_SERVICEBUS_HOSTNAME value: $SB_HOSTNAME restartPolicy: Never triggers: - type: azure-servicebus metadata: queueName: $SB_QUEUE_NAME namespace: $SB_NAME messageCount: "10" authenticationRef: name: azure-servicebus-auth EOF`

Note

ScaledJob creates a Kubernetes Job resource whenever a scaling event occurs and thus a Job template needs to be passed in when creating the resource. As new Jobs are created, Pods will be deployed with workload identity bits to consume messages.

Verify the KEDA scaler worked as intended.

`kubectl describe scaledjob myconsumer-scaledjob`

You should see events similar to the following.

`Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal KEDAScalersStarted 10m scale-handler Started scalers watch Normal ScaledJobReady 10m keda-operator ScaledJob is ready for scaling Warning KEDAScalerFailed 10m scale-handler context canceled Normal KEDAJobsCreated 10m scale-handler Created 10 jobs`


## Clean up resources

After you verify that the deployment is successful, you can clean up the resources to avoid incurring Azure costs.

Delete the Azure resource group and all resources in it using the [

`az group delete`

][az-group-delete] command.`az group delete --name $RG_NAME --yes --no-wait`


## Next steps

This article showed you how to securely scale your applications using the KEDA add-on and workload identity in AKS.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more about KEDA, see the [upstream KEDA docs](https://keda.sh/docs/2.12/).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ha-dr-overview -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/csi-secrets-store-identity-access -->

# Connect your Azure identity provider to the Azure Key Vault Secrets Store CSI Driver in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Secrets Store Container Storage Interface (CSI) Driver on Azure Kubernetes Service (AKS) provides various methods of identity-based access to your Azure Key Vault. This article outlines these methods and best practices for when to use Azure role-based access control (Azure RBAC) or OpenID Connect (OIDC) security models to access your key vault and AKS cluster.

You can use one of the following access methods:

- Service Connector with managed identity
- Workload ID
- User-assigned managed identity

Learn how to connect to Azure Key Vault with the Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster using Service Connector. In this article, you complete the following tasks:

- Create an AKS cluster and an Azure Key Vault.
- Create a connection between the AKS cluster and the Azure Key Vault with Service Connector.
- Create a
`SecretProviderClass`

CRD and a`Pod`

that consumes the CSI provider to test the connection. - Clean up resources.

## Prerequisites

- An Azure account with an active subscription.
[Create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - The
[Azure CLI](/en-us/cli/azure/install-azure-cli). Sign in using thecommand.`az login`

[Docker](https://docs.docker.com/get-docker/)and[kubectl](https://kubernetes.io/docs/tasks/tools/). To install kubectl locally, use thecommand.`az aks install-cli`

- A basic understanding of containers and AKS. Get started by
[preparing an application for AKS](/en-us/azure/aks/tutorial-kubernetes-prepare-app). - Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster.

## Initial set-up

If you're using Service Connector for the first time, start by running the command

[az provider register](/en-us/cli/azure/provider#az-provider-register)to register the Service Connector and Kubernetes Configuration resource providers.`az provider register -n Microsoft.ServiceLinker`

`az provider register -n Microsoft.KubernetesConfiguration`

Tip

You can check if these resource providers have already been registered by running the commands

`az provider show -n "Microsoft.ServiceLinker" --query registrationState`

and`az provider show -n "Microsoft.KubernetesConfiguration" --query registrationState`

.Optionally, use the Azure CLI command to get a list of supported target services for AKS cluster.

`az aks connection list-support-types --output table`


## Create Azure resources

Create a resource group using the

command.`az group create`

`az group create \ --name <resource-group-name> \ --location <location>`

Create an AKS cluster using the

command. The following example creates a single-node AKS cluster with managed identity enabled.`az aks create`

`az aks create \ --resource-group <resource-group-name> \ --name <cluster-name> \ --enable-managed-identity \ --node-count 1`

Connect to the cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group <resource-group-name> \ --name <cluster-name>`

Create an Azure key vault using the

command.`az keyvault create`

`az keyvault create \ --resource-group <resource-group-name> \ --name <key-vault-name> \ --location <location>`

Create a secret in the key vault using the

command.`az keyvault secret set`

`az keyvault secret set \ --vault-name <key-vault-name> \ --name <secret-name> \ --value <secret-value>`


## Create a service connection in AKS with Service Connector

You can create a service connection to Azure Key Vault using the Azure portal or Azure CLI.

In the Azure portal, navigate to your AKS cluster resource.

From the service menu, under

**Settings**, select**Service Connector**>**Create**.On the

**Create connection**page, configure the following settings in the**Basics**tab:**Kubernetes namespace**: Select**default**.**Service type**: Select**Key Vault**and select the checkbox to enable the Azure Key Vault CSI Provider.**Connection name**: Enter a name for the connection.**Subscription**: Select the subscription that contains the key vault.**Key vault**: Select the key vault you created.**Client type**: Select**None**.

Select

**Review + create**, and then select**Create**to create the connection.

## Test the connection

### Clone the sample repo and deploy manifest files

Clone the sample repository using the

`git clone`

command.`git clone https://github.com/Azure-Samples/serviceconnector-aks-samples.git`

Change directories to the Azure Key Vault CSI provider sample.

`cd serviceconnector-aks-samples/azure-keyvault-csi-provider`

In the

`secret_provider_class.yaml`

file, replace the following placeholders with your Azure Key Vault information:- Replace
`<AZURE_KEYVAULT_NAME>`

with the name of the key vault you created and connected. - Replace
`<AZURE_KEYVAULT_TENANTID>`

with the tenant ID of the key vault. - Replace
`<AZURE_KEYVAULT_CLIENTID>`

with identity client ID of the`azureKeyvaultSecretsProvider`

addon. - Replace
`<KEYVAULT_SECRET_NAME>`

with the key vault secret you created. For example,`ExampleSecret`

.

- Replace
Deploy the

`SecretProviderClass`

CRD using the`kubectl apply`

command.`kubectl apply -f secret_provider_class.yaml`

Deploy the

`Pod`

manifest file using the`kubectl apply`

command.The command creates a pod named

`sc-demo-keyvault-csi`

in the default namespace of your AKS cluster.`kubectl apply -f pod.yaml`


### Verify the connection

Verify the pod was created successfully using the

`kubectl get`

command.`kubectl get pod/sc-demo-keyvault-csi`

After the pod starts, the mounted content at the volume path specified in your deployment YAML is available.

Show the secrets held in the secrets store using the

`kubectl exec`

command.`kubectl exec sc-demo-keyvault-csi -- ls /mnt/secrets-store/`

Display a secret using the

`kubectl exec`

command.This example command shows a test secret named

`ExampleSecret`

.`kubectl exec sc-demo-keyvault-csi -- cat /mnt/secrets-store/ExampleSecret`


## Prerequisites for CSI Driver

- Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster. - Microsoft Entra Workload ID supports both Windows and Linux clusters.

## Access with a Microsoft Entra Workload ID

A [Microsoft Entra Workload ID](workload-identity-overview) is an identity that an application running on a pod uses to authenticate itself against other Azure services, such as workloads in software. The Secret Store CSI Driver integrates with native Kubernetes capabilities to federate with external identity providers.

In this security model, the AKS cluster acts as token issuer. Microsoft Entra ID then uses OIDC to discover public signing keys and verify the authenticity of the service account token before exchanging it for a Microsoft Entra token. For your workload to exchange a service account token projected to its volume for a Microsoft Entra token, you need the Azure Identity client library in the Azure SDK or the Microsoft Authentication Library (MSAL)

Note

- This authentication method replaces Microsoft Entra pod-managed identity (preview). The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service was deprecated as of October 24, 2022.
- Microsoft Entra Workload ID supports both Windows and Linux clusters.

### Configure workload identity

Set your subscription using the

command.`az account set`

`export SUBSCRIPTION_ID=<subscription id> export RESOURCE_GROUP=<resource group name> export UAMI=<name for user assigned identity> export KEYVAULT_NAME=<existing keyvault name> export CLUSTER_NAME=<aks cluster name> az account set --subscription $SUBSCRIPTION_ID`

Create a managed identity using the

command.`az identity create`

Note

This step assumes you have an existing AKS cluster with workload identity enabled. If workload identity isn't enabled, see

[Enable workload identity on an existing AKS cluster](workload-identity-deploy-cluster#enable-oidc-issuer-and-microsoft-entra-workload-id-on-an-aks-cluster)to enable it.`az identity create --name $UAMI --resource-group $RESOURCE_GROUP export USER_ASSIGNED_CLIENT_ID="$(az identity show --resource-group $RESOURCE_GROUP --name $UAMI --query 'clientId' -o tsv)" export IDENTITY_TENANT=$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query identity.tenantId -o tsv)`

Create a role assignment that grants the workload identity permission to access the key vault secrets, access keys, and certificates using the

command.`az role assignment create`

Important

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`key`

or`certificate`

type, assign therole to give permissions.`Key Vault Certificate User`

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`secret`

type, assign therole.`Key Vault Secrets User`

- If your key vault isn't set with
`--enable-rbac-authorization`

, you can use thecommand with the`az keyvault set-policy`

`--key-permissions get`

,`--certificate-permissions get`

, or`--secret-permissions get`

parameter to create a key vault policy to grant access for keys, certificates, or secrets. For example:

`az keyvault set-policy --name $KEYVAULT_NAME --key-permissions get --object-id $IDENTITY_OBJECT_ID`

`export KEYVAULT_SCOPE=$(az keyvault show --name $KEYVAULT_NAME --query id -o tsv) # Example command for key vault with Azure RBAC enabled using `key` type az role assignment create --role "Key Vault Certificate User" --assignee $USER_ASSIGNED_CLIENT_ID --scope $KEYVAULT_SCOPE`

- If your key vault is set with
Get the AKS cluster OIDC Issuer URL using the

command.`az aks show`

Note

This step assumes you have an existing AKS cluster with the OIDC Issuer URL enabled. If the OIDC Issuer URL isn't enabled, see

[Update an AKS cluster with OIDC Issuer](use-oidc-issuer#enable-the-oidc-issuer-on-an-existing-aks-cluster)to enable it.`export AKS_OIDC_ISSUER="$(az aks show --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --query "oidcIssuerProfile.issuerUrl" -o tsv)" echo $AKS_OIDC_ISSUER`

Establish a federated identity credential between the Microsoft Entra application, service account issuer, and subject. Get the object ID of the Microsoft Entra application using the following commands. Make sure to update the values for

`serviceAccountName`

and`serviceAccountNamespace`

with the Kubernetes service account name and its namespace.`export SERVICE_ACCOUNT_NAME="workload-identity-sa" # sample name; can be changed export SERVICE_ACCOUNT_NAMESPACE="default" # can be changed to namespace of your workload cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${USER_ASSIGNED_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`

Create the federated identity credential between the managed identity, service account issuer, and subject using the

command.`az identity federated-credential create`

`export FEDERATED_IDENTITY_NAME="aksfederatedidentity" # can be changed as needed az identity federated-credential create --name $FEDERATED_IDENTITY_NAME --identity-name $UAMI --resource-group $RESOURCE_GROUP --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME}`

Deploy a

`SecretProviderClass`

using the`kubectl apply`

command and the following YAML script.`cat <<EOF | kubectl apply -f - # This is a SecretProviderClass example using workload identity to access your key vault apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-kvname-wi # needs to be unique per namespace spec: provider: azure parameters: usePodIdentity: "false" clientID: "${USER_ASSIGNED_CLIENT_ID}" # Setting this to use workload identity keyvaultName: ${KEYVAULT_NAME} # Set to the name of your key vault cloudName: "" # [OPTIONAL for Azure] if not provided, the Azure environment defaults to AzurePublicCloud objects: | array: - | objectName: secret1 # Set to the name of your secret objectType: secret # object types: secret, key, or cert objectVersion: "" # [OPTIONAL] object versions, default to latest if empty - | objectName: key1 # Set to the name of your key objectType: key objectVersion: "" tenantId: "${IDENTITY_TENANT}" # The tenant ID of the key vault EOF`

Note

If you use

`objectAlias`

instead of`objectName`

, update the YAML script to account for it.Note

In order for the

`SecretProviderClass`

to function properly, make sure to populate your Azure Key Vault with secrets, keys, or certificates before referencing them in the`objects`

section.Deploy a sample pod using the

`kubectl apply`

command and the following YAML script.`cat <<EOF | kubectl apply -f - # This is a sample pod definition for using SecretProviderClass and workload identity to access your key vault kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline-wi labels: azure.workload.identity/use: "true" spec: serviceAccountName: "workload-identity-sa" containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-kvname-wi" EOF`


## Prerequisites for CSI Driver

- Before you begin, make sure you finish the steps in
[Use the Azure Key Vault provider for Secrets Store CSI Driver in an Azure Kubernetes Service (AKS) cluster](csi-secrets-store-driver)to enable the Azure Key Vault Secrets Store CSI Driver in your AKS cluster.

## Access with managed identity

A [Microsoft Entra Managed ID](/en-us/entra/identity/managed-identities-azure-resources/overview) is an identity that an administrator uses to authenticate themselves against other Azure services. The managed identity uses Azure RBAC to federate with external identity providers.

In this security model, you can grant access to your cluster's resources to team members or tenants sharing a managed role. The role is checked for scope to access the keyvault and other credentials. When you [enabled the Azure Key Vault provider for Secrets Store CSI Driver on your AKS Cluster](csi-secrets-store-driver#create-an-aks-cluster-with-azure-key-vault-provider-for-secrets-store-csi-driver-support), it created a user identity.

### Configure managed identity

Access your key vault using the

command and the user-assigned managed identity created by the add-on. You should also retrieve the identity's`az aks show`

`clientId`

, which you use in later steps when creating a`SecretProviderClass`

.`az aks show --resource-group <resource-group> --name <cluster-name> --query addonProfiles.azureKeyvaultSecretsProvider.identity.objectId -o tsv az aks show --resource-group <resource-group> --name <cluster-name> --query addonProfiles.azureKeyvaultSecretsProvider.identity.clientId -o tsv`

Alternatively, you can create a new managed identity and assign it to your virtual machine (VM) scale set or to each VM instance in your availability set using the following commands.

`az identity create --resource-group <resource-group> --name <identity-name> az vmss identity assign --resource-group <resource-group> --name <agent-pool-vmss> --identities <identity-resource-id> az vm identity assign --resource-group <resource-group> --name <agent-pool-vm> --identities <identity-resource-id> az identity show --resource-group <resource-group> --name <identity-name> --query 'clientId' -o tsv`

Create a role assignment that grants the identity permission to access the key vault secrets, access keys, and certificates using the

command.`az role assignment create`

Important

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`key`

or`certificate`

type, assign therole.`Key Vault Certificate User`

- If your key vault is set with
`--enable-rbac-authorization`

and you're using`secret`

type, assign therole.`Key Vault Secrets User`

- If your key vault isn't set with
`--enable-rbac-authorization`

, you can use thecommand with the`az keyvault set-policy`

`--key-permissions get`

,`--certificate-permissions get`

, or`--secret-permissions get`

parameter to create a key vault policy to grant access for keys, certificates, or secrets. For example:

`az keyvault set-policy --name $KEYVAULT_NAME --key-permissions get --object-id $IDENTITY_OBJECT_ID`

`export IDENTITY_OBJECT_ID="$(az identity show --resource-group <resource-group> --name <identity-name> --query 'principalId' -o tsv)" export KEYVAULT_SCOPE=$(az keyvault show --name <key-vault-name> --query id -o tsv) # Example command for key vault with Azure RBAC enabled using `key` type az role assignment create --role "Key Vault Certificate User" --assignee $USER_ASSIGNED_CLIENT_ID --scope $KEYVAULT_SCOPE`

- If your key vault is set with
Create a

`SecretProviderClass`

using the following YAML. Make sure to use your own values for`userAssignedIdentityID`

,`keyvaultName`

,`tenantId`

, and the objects to retrieve from your key vault.`# This is a SecretProviderClass example using user-assigned identity to access your key vault apiVersion: secrets-store.csi.x-k8s.io/v1 kind: SecretProviderClass metadata: name: azure-kvname-user-msi spec: provider: azure parameters: usePodIdentity: "false" useVMManagedIdentity: "true" # Set to true for using managed identity userAssignedIdentityID: <client-id> # Set the clientID of the user-assigned managed identity to use keyvaultName: <key-vault-name> # Set to the name of your key vault cloudName: "" # [OPTIONAL for Azure] if not provided, the Azure environment defaults to AzurePublicCloud objects: | array: - | objectName: secret1 objectType: secret # object types: secret, key, or cert objectVersion: "" # [OPTIONAL] object versions, default to latest if empty - | objectName: key1 objectType: key objectVersion: "" tenantId: <tenant-id> # The tenant ID of the key vault`

Note

If you use

`objectAlias`

instead of`objectName`

, make sure to update the YAML script.Note

In order for the

`SecretProviderClass`

to function properly, make sure to populate your Azure Key Vault with secrets, keys, or certificates before referencing them in the`objects`

section.Apply the

`SecretProviderClass`

to your cluster using the`kubectl apply`

command.`kubectl apply -f secretproviderclass.yaml`

Create a pod using the following YAML.

`# This is a sample pod definition for using SecretProviderClass and the user-assigned identity to access your key vault kind: Pod apiVersion: v1 metadata: name: busybox-secrets-store-inline-user-msi spec: containers: - name: busybox image: registry.k8s.io/e2e-test-images/busybox:1.29-4 command: - "/bin/sleep" - "10000" volumeMounts: - name: secrets-store01-inline mountPath: "/mnt/secrets-store" readOnly: true volumes: - name: secrets-store01-inline csi: driver: secrets-store.csi.k8s.io readOnly: true volumeAttributes: secretProviderClass: "azure-kvname-user-msi"`

Apply the pod to your cluster using the

`kubectl apply`

command.`kubectl apply -f pod.yaml`


## Validate Key Vault secrets

After the pod starts, the mounted content at the volume path specified in your deployment YAML is available. Use the following commands to validate your secrets and print a test secret.

Show secrets held in the secrets store using the following command.

`kubectl exec busybox-secrets-store-inline-user-msi -- ls /mnt/secrets-store/`

Display a secret in the store using the following command. This example command shows the test secret

`ExampleSecret`

.`kubectl exec busybox-secrets-store-inline-user-msi -- cat /mnt/secrets-store/ExampleSecret`


## Obtain certificates and keys

The Azure Key Vault design makes sharp distinctions between keys, secrets, and certificates. The certificate features of the Key Vault service are designed to make use of key and secret capabilities. When you create a key vault certificate, it creates an addressable key and secret with the same name. This key allows authentication operations, and the secret allows the retrieval of the certificate value as a secret.

A key vault certificate also contains public x509 certificate metadata. The key vault stores both the public and private components of your certificate in a secret. You can obtain each individual component by specifying the `objectType`

in `SecretProviderClass`

. The following table shows which objects map to the various resources associated with your certificate:

| Object | Return value | Returns entire certificate chain |
|---|---|---|
`key` |
The public key, in Privacy Enhanced Mail (PEM) format. | N/A |
`cert` |
The certificate, in PEM format. | No |
`secret` |
The private key and certificate, in PEM format. | Yes |

## Disable the addon on existing clusters

Note

Before you disable the add-on, ensure that *no* `SecretProviderClass`

is in use. Trying to disable the add-on while a `SecretProviderClass`

exists results in an error.

Disable the Azure Key Vault provider for Secrets Store CSI Driver capability in an existing cluster using the [ az aks disable-addons](/en-us/cli/azure/aks#az-aks-disable-addons) command with the

`azure-keyvault-secrets-provider`

add-on.```
az aks disable-addons --addons azure-keyvault-secrets-provider --resource-group myResourceGroup --name myAKSCluster
```


Note

When you disable the add-on, existing workloads should have no issues or see any updates in the mounted secrets. If the pod restarts or a new pod is created as part of scale-up event, the pod fails to start because the driver is no longer running.

## Next steps

In this article, you learned how to create and provide an identity to access your Azure Key Vault. The [Service Connector](/en-us/azure/service-connector/overview) integration helps simplify the connection configuration for AKS workloads and Azure backing services. It securely handles authentication and network configurations and follows best practices for connecting to Azure services. For more information, see [Use the Azure Key Vault provider for Secrets Store CSI Driver in an AKS cluster](/en-us/azure/service-connector/tutorial-python-aks-keyvault-csi-driver) and the [Service Connector introduction](https://blog.aks.azure.com/2024/05/23/service-connector-intro).

If you want to configure extra configuration options or perform troubleshooting, see [Configuration options and troubleshooting resources for Azure Key Vault provider with Secrets Store CSI Driver in AKS](csi-secrets-store-configuration-options).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-multi-region -->

# Multi-region deployment models for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) provides a managed Kubernetes environment for deploying, managing, and scaling containerized applications. To provide resiliency to regional outages for your applications running on AKS, you can implement various multi-region deployment models. This article provides an overview of these models, their pros and cons, and best practices for maintaining application uptime.

AKS provides a range of capabilities that support both high availability (HA) and disaster recovery (DR) for your cluster and the applications running on AKS. For more information on how AKS supports reliability requirements, see [Reliability in AKS](/en-us/azure/reliability/reliability-aks#multi-region-support).

## Considerations

Below are some important considerations when implementing multi-region deployment models in AKS:

### Regional and global resources

**Regional resources** are provisioned as part of a *deployment stamp* to a single Azure region. These resources share nothing with resources in other regions, and they can be independently removed or replicated to other regions. For more information, see [Regional resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#regional-resources).

**Global resources** share the lifetime of the system, and they can be globally available within the context of a multi-region deployment. For more information, see [Global resources](/en-us/azure/architecture/reference-architectures/containers/aks-mission-critical/mission-critical-intro#global-resources).

### Global load balancing

Global load balancing services distribute traffic across regional backends, clouds, or hybrid on-premises services. These services route end-user traffic to the closest available backend. They also react to changes in service reliability or performance to maximize availability and performance. The following Azure services provide global load balancing:

[Azure Front Door](/en-us/azure/frontdoor/front-door-overview)[Azure Traffic Manager](/en-us/azure/traffic-manager/traffic-manager-overview)[Cross-region Azure Load Balancer](/en-us/azure/load-balancer/cross-region-overview)[Azure Kubernetes Fleet Manager](/en-us/azure/kubernetes-fleet/overview)

### Scope definition

Application uptime becomes important as you manage AKS clusters. By default, AKS provides high availability by using multiple nodes in a [Virtual Machine Scale Set](/en-us/azure/virtual-machine-scale-sets/overview), but these nodes don’t protect your system from a region failure. To maximize your uptime, plan ahead to maintain business continuity and prepare for disaster recovery using the following best practices:

- Plan for AKS clusters in multiple regions.
- Route traffic across multiple clusters using Azure Traffic Manager.
- Use geo-replication for your container image registries.
- Plan for application state across multiple clusters.
- Replicate storage across multiple regions.

## Multi-region deployment model implementations

The following table summarizes the three main multi-region deployment models in AKS, along with their pros and cons:

| Deployment model | Pros | Cons |
|---|---|---|
|

• High resiliency

• Better utilization of resources with higher performance

• Higher cost

• Requires a load balancer and form of traffic routing

[Active-passive](#active-passive-disaster-recovery-deployment-model)• Lower cost

• Doesn't require a load balancer or traffic manager

• Longer recovery time and downtime

• Underutilization of resources

[Passive-cold](#passive-cold-failover-deployment-model)• Doesn't require synchronization, replication, load balancer, or traffic manager

• Suitable for low-priority, non-critical workloads

• Longest recovery time and downtime

• Requires manual intervention to activate cluster and trigger backup

### Active-active high availability deployment model

In the active-active high availability (HA) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes between both regions. If one region becomes unavailable, traffic automatically routes to a region closest to the user who issued the request.
- There's a deployed hub-spoke pair for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Azure Front Door load balances and routes traffic to a regional Azure Application Gateway instance, which sits in front of each AKS cluster.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-active deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Create two instances of your web app.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- Two origin groups, each with a priority of
*one*. - A route.

Limit network traffic to the web apps only from the Azure Front Door instance. 5. Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both web apps with continuous deployment.


For more information, see the [ Recommended active-active high availability solution overview for AKS](active-active-solution).

### Active-passive disaster recovery deployment model

In the active-passive disaster recovery (DR) deployment model, you have two independent AKS clusters deployed in two different Azure regions (typically paired regions, such as Canada Central and Canada East or US East 2 and US Central) that actively serve traffic. Only one of the clusters actively serves traffic at any given time. The other cluster contains the same configuration and application data as the active cluster, but doesn't accept traffic unless directed by a traffic manager.

With this example architecture:

- You deploy two AKS clusters in separate Azure regions.
- During normal operations, network traffic routes to the primary AKS cluster, which you set in the Azure Front Door configuration.
- Priority needs to be set between
*1-5*with 1 being the highest and 5 being the lowest. - You can set multiple clusters to the same priority level and can specify the weight of each.

- Priority needs to be set between
- If the primary cluster becomes unavailable (disaster occurs), traffic automatically routes to the next region selected in the Azure Front Door.
- All traffic must go through the Azure Front Door traffic manager for this system to work.

- Azure Front Door routes traffic to the Azure App Gateway in the primary region (cluster must be marked with priority 1). If this region fails, the service redirects traffic to the next cluster in the priority list.
- Rules come from Azure Front Door.

- A hub-spoke pair is deployed for each regional AKS instance. Azure Firewall Manager policies manage the firewall rules across the regions.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs.
- The container images for the workload are stored in a managed container registry. A single Azure Container Registry is used for all Kubernetes instances in the cluster. Geo-replication for Azure Container Registry enables replicating images to the selected Azure regions and provides continued access to images, even if a region experiences an outage.

To create an active-passive deployment model in AKS, you perform the following steps:

Create two identical deployments in two different Azure regions.

Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up. This helps reduce costs.

Create two instances of your web application, with one on each cluster.

Create an Azure Front Door profile with the following resources:

- An endpoint.
- An origin group with a priority of
*one*for the primary region. - A second origin group with a priority of
*two*for the secondary region. - A route.

Limit network traffic to the web applications from only the Azure Front Door instance.

Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.

Deploy code to both the web applications with continuous deployment.


For more information, see the [ Recommended active-passive disaster recovery solution overview for AKS](active-passive-solution).

### Passive-cold failover deployment model

The passive-cold failover deployment model is configured in the same way as the [active-passive disaster recovery deployment model](#active-passive-disaster-recovery-deployment-model), except the clusters remain inactive until a user activates them in the event of a disaster. We consider this approach *out-of-scope* because it involves a similar configuration to active-passive, but with the added complexity of manual intervention to activate the cluster and trigger a backup.

With this example architecture:

- You create two AKS clusters, preferably in different regions or zones for better resiliency.
- When you need to fail over, you activate the deployment to take over the traffic flow.
- In the case the primary passive cluster goes down, you need to manually activate the cold cluster to take over the traffic flow.
- This condition needs to be set either by a manual input every time or a certain event as specified by you.
- Azure Key Vault is provisioned in each region to store secrets and keys.
- Regional Log Analytics instances store regional networking metrics and diagnostic logs for each cluster.

To create a passive-cold failover deployment model in AKS, you perform the following steps:

- Create two identical deployments in different zones/regions.
- Configure autoscaling rules for the secondary application so it scales to the same instance count as the primary when the primary region becomes inactive. While inactive, it doesn't need to be scaled up, which helps reduce costs.
- Create two instances of your web application, with one on each cluster.
- Configure all other backend Azure services, such as databases, storage accounts, and authentication providers.
- Set a condition when the cold cluster should be triggered. You can use a load balancer if you need.

For more information, see the [ Recommended passive-cold failover solution overview for AKS](passive-cold-solution).

For more information, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr -->

# Install the Dapr extension for Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Dapr](dapr-overview) simplifies building resilient, stateless, and stateful applications that run on the cloud and edge and embrace the diversity of languages and developer frameworks. With Dapr's sidecar architecture, you can keep your code platform agnostic while tackling challenges around building microservices, like:

- Calling other services reliably and securely
- Building event-driven apps with pub/sub
- Building applications that are portable across multiple cloud services and hosts (for example, Kubernetes vs. a virtual machine)

Note

If you plan on installing Dapr in a Kubernetes production environment, see the [Dapr guidelines for production usage](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-production) documentation page.

## How it works

The Dapr extension uses the Azure CLI or a Bicep template to provision the Dapr control plane on your AKS or Arc-enabled Kubernetes cluster, creating the following Dapr services:

| Dapr service | Description |
|---|---|
`dapr-operator` |
Manages component updates and Kubernetes services endpoints for Dapr (state stores, pub/subs, etc.) |
`dapr-sidecar-injector` |
Injects Dapr into annotated deployment pods and adds the environment variables `DAPR_HTTP_PORT` and `DAPR_GRPC_PORT` to enable user-defined applications to easily communicate with Dapr without hard-coding Dapr port values. |
`dapr-placement` |
Used for actors only. Creates mapping tables that map actor instances to pods. |
`dapr-sentry` |
Manages mTLS between services and acts as a certificate authority. For more information, read the
|

Once Dapr is installed on your cluster, you can begin to develop using the Dapr building block APIs by [adding a few annotations](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-overview/#adding-dapr-to-a-kubernetes-deployment) to your deployments. For a more in-depth overview of the building block APIs and how to best use them, see the [Dapr building blocks overview](https://docs.dapr.io/developing-applications/building-blocks/).

Warning

If you install Dapr through the AKS or Arc-enabled Kubernetes extension, our recommendation is to continue using the extension for future management of Dapr instead of the Dapr CLI. Combining the two tools can cause conflicts and result in undesired behavior.

## Prerequisites

- An Azure subscription.
[Don't have one? Create a free account.](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn) - The latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli). - An existing
[AKS cluster](tutorial-kubernetes-deploy-cluster)or connected[Arc-enabled Kubernetes cluster](/en-us/azure/azure-arc/kubernetes/quickstart-connect-cluster). [An Azure Kubernetes Service Role-Based Access Control Admin role](/en-us/azure/role-based-access-control/built-in-roles#azure-kubernetes-service-rbac-admin)

Select how you'd like to install, deploy, and configure the Dapr extension.

## Before you begin

### Add the Azure CLI extension for cluster extensions

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

If you aren't already using cluster extensions, you may need to register the resource provider with your subscription. You can check the status of the provider registration using the [az provider list](/en-us/cli/azure/provider#az-provider-list) command, as shown in the following example:

```
az provider list --query "[?contains(namespace,'Microsoft.KubernetesConfiguration')]" -o table
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


### Register the `ExtensionTypes`

feature to your Azure subscription

The `ExtensionTypes`

feature needs to be registered to your Azure subscription. In the terminal, verify you're in the correct subscription:

```
az account set --subscription <YOUR-AZURE-SUBSCRIPTION-ID>
```


Register the `ExtensionTypes`

feature.

```
az feature registration create --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


Feature registration may take some time. After a few minutes, check the registration status using the following command:

```
az feature show --namespace Microsoft.KubernetesConfiguration --name ExtensionTypes
```


## Create the extension and install Dapr on your AKS or Arc-enabled Kubernetes cluster

When installing the Dapr extension, use the flag value that corresponds to your cluster type:

**AKS cluster**:`--cluster-type managedClusters`

.**Arc-enabled Kubernetes cluster**:`--cluster-type connectedClusters`

.

Note

If you're using Dapr OSS on your AKS cluster and would like to install the Dapr extension for AKS, read more about [how to successfully migrate to the Dapr extension](dapr-migration).

Create the Dapr extension, which installs Dapr on your AKS or Arc-enabled Kubernetes cluster.

For example, install the latest version of Dapr via the Dapr extension on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false
```


### Keep your managed AKS cluster updated to the latest version

Based on your environment (dev, test, or production), you can keep up-to-date with the latest stable Dapr versions.

#### Choosing a release train

When configuring the extension, you can choose to install Dapr from a particular release train. Specify one of the two release train values:

| Value | Description |
|---|---|
`stable` |
Default. |
`dev` |
Early releases that can contain experimental features. Not suitable for production. |

For example:

```
--release-train stable
```


#### Configuring automatic updates to Dapr control plane

Warning

Auto-upgrade is not suitable for production environments. Only enable automatic updates to the Dapr control plane in dev or test environments. [Learn how to manually upgrade to the latest Dapr version for production environments.](#viewing-the-latest-stable-dapr-versions-available)

If you install Dapr without specifying a version, `--auto-upgrade-minor-version`

*is automatically enabled*, configuring the Dapr control plane to automatically update its minor version on new releases.

You can disable auto-update by specifying the `--auto-upgrade-minor-version`

parameter and setting the value to `false`

.

[Dapr versioning is in MAJOR.MINOR.PATCH format](https://docs.dapr.io/operations/support/support-versioning/#versioning), which means

`1.11.0`

to `1.12.0`

is a *minor*version upgrade.

```
--auto-upgrade-minor-version true
```


#### Viewing the latest stable Dapr versions available

To upgrade to the latest Dapr version in a production environment, you need to manually upgrade. Start by viewing a list of the stable Dapr versions available to your managed AKS cluster. Run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable
```


To see the latest stable Dapr version available to your managed AKS cluster, run the following command:

```
az k8s-extension extension-types list-versions-by-cluster --resource-group <myResourceGroup> --cluster-name <myCluster> --cluster-type managedClusters --extension-type microsoft.dapr --release-train stable --show-latest
```


To view a list of the stable Dapr versions available *by location*:

[Make sure you've registered the](dapr#register-the-extensiontypes-feature-to-your-azure-subscription)`ExtensionTypes`

feature to your Azure subscription.- Run the following command.

```
az k8s-extension extension-types list-versions-by-location --location westus --extension-type microsoft.dapr
```


[Next, manually update Dapr to the latest stable version.](#targeting-a-specific-dapr-version)

#### Targeting a specific Dapr version

Note

Dapr is supported with a rolling window, including only the current and previous versions. It is your operational responsibility to remain up to date with these supported versions. If you have an older version of Dapr, you may have to do intermediate upgrades to get to a supported version.

The same command-line argument is used for installing a specific version of Dapr or rolling back to a previous version. Set `--auto-upgrade-minor-version`

to `false`

and `--version`

to the version of Dapr you wish to install. If the `version`

parameter is omitted, the extension installs the latest version of Dapr. The following example command installs Dapr version `1.14.4-msft.10`

on your AKS cluster:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name <myAKSCluster> \
--resource-group <myResourceGroup> \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version false \
--version 1.14.4-msft.10
```


## Troubleshooting

### Troubleshooting extension management errors

If the extension fails to create or update, try suggestions and solutions in the [Dapr extension troubleshooting guide](dapr-troubleshooting).

### Troubleshooting Dapr functional errors

Troubleshoot Dapr open source errors unrelated to the extension via the [common Dapr issues and solutions guide](https://docs.dapr.io/operations/troubleshooting/common_issues/).

## Support

Note

Learn more about [how Microsoft handles issues raised for the Dapr extension](dapr-overview#issue-handling).

If you're experiencing Dapr runtime security risks and regressions while using the extension, open an issue with the [Dapr open source project](https://github.com/dapr/dapr/issues/new/choose).

You could also start a discussion in the Dapr project Discord:

## Delete the Dapr extension from your cluster

The process of uninstalling the Dapr extension from AKS does not delete the CRDs created during installation. These CRDs remain in the cluster as residual components, essential for the reconciler during the installation and uninstallation of the extension.

To clean the cluster of these CRDs, you can manually delete them **after** the Dapr extension has been completely uninstalled from AKS.

### Uninstalling the extension

Delete the extension from your AKS cluster using the following command:

```
az k8s-extension delete --resource-group <myResourceGroup> --cluster-name <myAKSCluster> --cluster-type managedClusters --name dapr
```


Or, if using a Bicep template, you can delete the template.

### Listing the CRDs in your cluster

To find the CRDs you'd like to remove, run the following command:

```
kubectl get crds | findstr dapr.io
```
