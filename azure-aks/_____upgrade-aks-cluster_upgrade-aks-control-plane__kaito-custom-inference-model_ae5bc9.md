---
merged_at: 2026-01-26T20:54:26.176681
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-cluster -->

# Upgrade the Azure Kubernetes Service (AKS) cluster control plane

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) clusters consist of two main components: the **control plane managed by Azure** and the **node pools where your workloads run**. This article focuses on upgrading the control plane independently, which allows you to adopt new Kubernetes versions for API server features while separately managing node pool upgrades.

## Before you begin

- If you're using the Azure CLI, this article requires Azure CLI version 2.34.1 or later. Use the
`az --version`

command to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this article requires Azure PowerShell version 5.9.0 or later. Use the
`Get-InstalledModule -Name Az`

cmdlet to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - Performing upgrade operations requires the
`Microsoft.ContainerService/managedClusters/agentPools/write`

RBAC role. For more on Azure RBAC roles, see the[Azure resource provider operations](/en-us/azure/role-based-access-control/built-in-roles#containers). - Starting with Kubernetes version 1.30 and 1.27 LTS versions, beta APIs are disabled by default when you upgrade to them.

Warning

Ensure you have sufficient compute quota before upgrading. If quota is low, the upgrade might fail. For more information, see [increase quotas](/en-us/azure/azure-portal/supportability/regional-quota-requests).

## Overview of AKS upgrade types

The following table outlines three types of AKS upgrades, highlighting their scope and use cases:

| Upgrade type | Scope | Use case |
|---|---|---|
|

[Full cluster](#upgrade-the-full-aks-cluster)[Node pool only](upgrade-aks-node-pools-rolling)Tip

Upgrading the control plane first allows you to validate Kubernetes API compatibility before affecting running workloads. For node pool upgrade strategies, see [Configure rolling upgrades](upgrade-aks-node-pools-rolling).

## Kubernetes version upgrade rules

When you upgrade a supported AKS cluster, you can't skip Kubernetes minor versions. You must perform all upgrades sequentially by minor version number. For example, upgrades between *1.28.x* -> *1.29.x* or *1.29.x* -> *1.30.x* are allowed. *1.28.x* -> *1.30.x* isn't allowed.

The control plane can be up to two minor versions ahead of node pools. For example, if your control plane is at *1.30.x*, your node pools can be at *1.28.x*, *1.29.x*, or *1.30.x*.

## Check for available AKS upgrades

Tip

To stay up to date with the latest AKS releases and updates, see the [AKS release tracker](release-tracker).

Check for available Kubernetes releases for your AKS cluster using the [ az aks get-upgrades](/en-us/cli/azure/aks#az-aks-get-upgrades) command.

```
az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name> --output table
```


The following example output shows the current version as *1.28.9* and lists the available versions under `upgrades`

:

```
Name ResourceGroup MasterVersion Upgrades
------- --------------- --------------- --------------
default <resource-group-name> 1.28.9 1.29.2, 1.29.4
```


## Upgrade the AKS control plane only

Upgrade the control plane using the

command with the`az aks upgrade`

`--control-plane-only`

flag. The following example upgrades the control plane to Kubernetes version*1.29.4*:`az aks upgrade \ --resource-group <resource-group-name> \ --name <cluster-name> \ --kubernetes-version 1.29.4 \ --control-plane-only`

Confirm the control plane upgrade was successful using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> --name <cluster-name> --output table`

The following example output shows the control plane now runs

*1.29.4*:`Name Location ResourceGroup KubernetesVersion ProvisioningState Fqdn ------------ ---------- --------------- ------------------- ------------------- ------------------------------------------------ <cluster-name> eastus <resource-group-name> 1.29.4 Succeeded <cluster-name>-dns-123abcd4.hcp.eastus.azmk8s.io`

Verify the node pool versions remain unchanged using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name> --query "[].{Name:name,Version:orchestratorVersion}" --output table`

In the output, the node pools should still show the previous Kubernetes version.


## Upgrade the full AKS cluster

Note

During a full cluster upgrade, AKS upgrades the control plane first, then upgrades each node pool sequentially. For more control over node pool upgrades, see [Configure rolling upgrades](upgrade-aks-node-pools-rolling).

Upgrade the full cluster (control plane and all node pools) using the [ az aks upgrade](/en-us/cli/azure/aks#az-aks-upgrade) command. The following example upgrades the cluster to Kubernetes version

*1.29.4*:

```
az aks upgrade \
--resource-group <resource-group-name> \
--name <cluster-name> \
--kubernetes-version 1.29.4
```


## Frequently asked questions (FAQs)

### Why were my node pools upgraded when I only upgraded the control plane?

AKS might trigger a rolling node pool upgrade alongside a control plane upgrade to keep the cluster compliant and healthy. This upgrade typically occurs when a previous node upgrade failed or left nodes on mixed versions.

### Can I upgrade node pools before the control plane?

No. The control plane version must always be equal to or greater than any node pool version. You must upgrade the control plane first.

### How long does a control plane upgrade take?

Control plane upgrades typically complete within 5-15 minutes, depending on cluster configuration and Azure region load. Node pool upgrades take longer as they involve draining and reimaging nodes.

## Resolve control plane upgrade issues

### No upgrades available

If `az aks get-upgrades`

shows no available upgrades, your cluster might be:

- Already on the latest supported version.
- On an unsupported version that requires migration.

For unsupported versions, create a new cluster with a supported version and migrate your workloads.

### Upgrade failed due to deprecated APIs

Before upgrading, check for deprecated APIs using tools like [kube-no-trouble (kubent)](https://github.com/doitintl/kube-no-trouble):

```
kubent
```


Update your manifests to use supported API versions before upgrading.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/upgrade-aks-control-plane -->

# Upgrade the Azure Kubernetes Service (AKS) cluster control plane

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) clusters consist of two main components: the **control plane managed by Azure** and the **node pools where your workloads run**. This article focuses on upgrading the control plane independently, which allows you to adopt new Kubernetes versions for API server features while separately managing node pool upgrades.

## Before you begin

- If you're using the Azure CLI, this article requires Azure CLI version 2.34.1 or later. Use the
`az --version`

command to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this article requires Azure PowerShell version 5.9.0 or later. Use the
`Get-InstalledModule -Name Az`

cmdlet to find the version. If you need to install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - Performing upgrade operations requires the
`Microsoft.ContainerService/managedClusters/agentPools/write`

RBAC role. For more on Azure RBAC roles, see the[Azure resource provider operations](/en-us/azure/role-based-access-control/built-in-roles#containers). - Starting with Kubernetes version 1.30 and 1.27 LTS versions, beta APIs are disabled by default when you upgrade to them.

Warning

Ensure you have sufficient compute quota before upgrading. If quota is low, the upgrade might fail. For more information, see [increase quotas](/en-us/azure/azure-portal/supportability/regional-quota-requests).

## Overview of AKS upgrade types

The following table outlines three types of AKS upgrades, highlighting their scope and use cases:

| Upgrade type | Scope | Use case |
|---|---|---|
|

[Full cluster](#upgrade-the-full-aks-cluster)[Node pool only](upgrade-aks-node-pools-rolling)Tip

Upgrading the control plane first allows you to validate Kubernetes API compatibility before affecting running workloads. For node pool upgrade strategies, see [Configure rolling upgrades](upgrade-aks-node-pools-rolling).

## Kubernetes version upgrade rules

When you upgrade a supported AKS cluster, you can't skip Kubernetes minor versions. You must perform all upgrades sequentially by minor version number. For example, upgrades between *1.28.x* -> *1.29.x* or *1.29.x* -> *1.30.x* are allowed. *1.28.x* -> *1.30.x* isn't allowed.

The control plane can be up to two minor versions ahead of node pools. For example, if your control plane is at *1.30.x*, your node pools can be at *1.28.x*, *1.29.x*, or *1.30.x*.

## Check for available AKS upgrades

Tip

To stay up to date with the latest AKS releases and updates, see the [AKS release tracker](release-tracker).

Check for available Kubernetes releases for your AKS cluster using the [ az aks get-upgrades](/en-us/cli/azure/aks#az-aks-get-upgrades) command.

```
az aks get-upgrades --resource-group <resource-group-name> --name <cluster-name> --output table
```


The following example output shows the current version as *1.28.9* and lists the available versions under `upgrades`

:

```
Name ResourceGroup MasterVersion Upgrades
------- --------------- --------------- --------------
default <resource-group-name> 1.28.9 1.29.2, 1.29.4
```


## Upgrade the AKS control plane only

Upgrade the control plane using the

command with the`az aks upgrade`

`--control-plane-only`

flag. The following example upgrades the control plane to Kubernetes version*1.29.4*:`az aks upgrade \ --resource-group <resource-group-name> \ --name <cluster-name> \ --kubernetes-version 1.29.4 \ --control-plane-only`

Confirm the control plane upgrade was successful using the

command.`az aks show`

`az aks show --resource-group <resource-group-name> --name <cluster-name> --output table`

The following example output shows the control plane now runs

*1.29.4*:`Name Location ResourceGroup KubernetesVersion ProvisioningState Fqdn ------------ ---------- --------------- ------------------- ------------------- ------------------------------------------------ <cluster-name> eastus <resource-group-name> 1.29.4 Succeeded <cluster-name>-dns-123abcd4.hcp.eastus.azmk8s.io`

Verify the node pool versions remain unchanged using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name> --query "[].{Name:name,Version:orchestratorVersion}" --output table`

In the output, the node pools should still show the previous Kubernetes version.


## Upgrade the full AKS cluster

Note

During a full cluster upgrade, AKS upgrades the control plane first, then upgrades each node pool sequentially. For more control over node pool upgrades, see [Configure rolling upgrades](upgrade-aks-node-pools-rolling).

Upgrade the full cluster (control plane and all node pools) using the [ az aks upgrade](/en-us/cli/azure/aks#az-aks-upgrade) command. The following example upgrades the cluster to Kubernetes version

*1.29.4*:

```
az aks upgrade \
--resource-group <resource-group-name> \
--name <cluster-name> \
--kubernetes-version 1.29.4
```


## Frequently asked questions (FAQs)

### Why were my node pools upgraded when I only upgraded the control plane?

AKS might trigger a rolling node pool upgrade alongside a control plane upgrade to keep the cluster compliant and healthy. This upgrade typically occurs when a previous node upgrade failed or left nodes on mixed versions.

### Can I upgrade node pools before the control plane?

No. The control plane version must always be equal to or greater than any node pool version. You must upgrade the control plane first.

### How long does a control plane upgrade take?

Control plane upgrades typically complete within 5-15 minutes, depending on cluster configuration and Azure region load. Node pool upgrades take longer as they involve draining and reimaging nodes.

## Resolve control plane upgrade issues

### No upgrades available

If `az aks get-upgrades`

shows no available upgrades, your cluster might be:

- Already on the latest supported version.
- On an unsupported version that requires migration.

For unsupported versions, create a new cluster with a supported version and migrate your workloads.

### Upgrade failed due to deprecated APIs

Before upgrading, check for deprecated APIs using tools like [kube-no-trouble (kubent)](https://github.com/doitintl/kube-no-trouble):

```
kubent
```


Update your manifests to use supported API versions before upgrading.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kaito-custom-inference-model -->

# Onboard custom models for inferencing with the AI toolchain operator (KAITO) on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As an AI engineer or developer, you might have to prototype and deploy AI workloads with a range of different model weights. AKS provides the option to deploy inferencing workloads using open-source presets supported out-of-box and managed in the KAITO [model registry](https://github.com/kaito-project/kaito/tree/main/presets) or to dynamically download from the [HuggingFace registry](https://huggingface.co/models) at runtime onto your AKS cluster.

In this article, you learn how to onboard a sample HuggingFace model for inferencing with the AI toolchain operator add-on without having to manage custom images on Azure Kubernetes Service (AKS).

## Prerequisites

An Azure account with an active subscription. If you don't have an account, you can

[create one for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).An AKS cluster with the AI toolchain operator add-on enabled. For more information, see

[Enable KAITO on an AKS cluster](ai-toolchain-operator#enable-the-ai-toolchain-operator-add-on-on-an-aks-cluster).This example deployment requires quota for the

`Standard_NCads_A100_v4`

virtual machine (VM) family in your Azure subscription. If you don't have quota for this VM family, please[request a quota increase](/en-us/azure/quotas/quickstart-increase-quota-portal).Note

Currently, only the HuggingFace runtime supports inference with the KAITO custom model deployment template.


## Choose an open-source language model from HuggingFace

In this example, we use the [BigScience Bloom-1B7](https://huggingface.co/bigscience/bloom-1b7) small language model. Alternatively, you can choose from thousands of text-generation models supported on [HuggingFace](https://huggingface.co/models?pipeline_tag=text-generation).

Connect to your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group <resource-group-name> --name <aks-cluster-name>`

Clone the KAITO project GitHub repository using the

`git clone`

command.`git clone https://github.com/kaito-project/kaito.git`


## Deploy your model inferencing workload using the KAITO workspace template

Navigate to the

`kaito`

directory and copy the[sample deployment YAML](https://github.com/kaito-project/kaito/tree/main/examples/custom-model-integration/custom-model-deployment.yaml)manifest. Replace the default values in the following fields with your model's requirements. For this example, we specify the**bloom-1b7**HuggingFace model ID for[BigScience Bloom-1B7](https://huggingface.co/bigscience/bloom-1b7)model:`instanceType`

: The minimum VM size for this inference service deployment is`Standard_NC24ads_A100_v4`

. For larger model sizes you can choose a VM in thefamily with higher memory capacity.`Standard_NCads_A100_v4`

`MODEL_ID`

: Replace with your model's specific HuggingFace identifier, which can be found after`https://huggingface.co/`

in the model card URL.`"--torch_dtype"`

: Set to`"float16"`

for compatibility with V100 GPUs. For A100, H100 or newer GPUs, use`"bfloat16"`

.- (Optional)
`HF_TOKEN`

: Specify the values in this section only if you are deploying a private or gated Hugging Face model for inference.

`apiVersion: kaito.sh/v1beta1 kind: Workspace metadata: name: workspace-custom-llm resource: instanceType: "Standard_NC24ads_A100_v4" # Replace with the required VM SKU based on model requirements labelSelector: matchLabels: apps: custom-llm inference: template: spec: containers: - name: custom-llm-container image: mcr.microsoft.com/aks/kaito/kaito-base:0.0.8 # KAITO base image which includes hf runtime livenessProbe: failureThreshold: 3 httpGet: path: /health port: 5000 scheme: HTTP initialDelaySeconds: 600 periodSeconds: 10 successThreshold: 1 timeoutSeconds: 1 readinessProbe: failureThreshold: 3 httpGet: path: /health port: 5000 scheme: HTTP initialDelaySeconds: 30 periodSeconds: 10 successThreshold: 1 timeoutSeconds: 1 resources: requests: nvidia.com/gpu: 1 # Request 1 GPU; adjust as needed limits: nvidia.com/gpu: 1 # Optional: Limit to 1 GPU command: - "accelerate" args: - "launch" - "--num_processes" - "1" - "--num_machines" - "1" - "--gpu_ids" - "all" - "tfs/inference_api.py" - "--pipeline" - "text-generation" - "--trust_remote_code" - "--allow_remote_files" - "--pretrained_model_name_or_path" - "bloom-1b7" - "--torch_dtype" - "bfloat16" # env: # HF_TOKEN is required only for private or gated Hugging Face models # Uncomment and configure this block if needed # - name: HF_TOKEN # valueFrom: # secretKeyRef: # name: hf-token-secret # Replace with your Kubernetes Secret name # key: HF_TOKEN # Replace with the specific key holding the token volumeMounts: - name: dshm mountPath: /dev/shm volumes: - name: dshm emptyDir: medium: Memory`

Save these changes to your

`custom-model-deployment.yaml`

file.Run the deployment in your AKS cluster using the

`kubectl apply`

command.`kubectl apply -f custom-model-deployment.yaml`


## Test your custom model inferencing service

Track the live resource changes in your KAITO workspace using the

`kubectl get workspace`

command.`kubectl get workspace workspace-custom-llm -w`

Note

Note that machine readiness can take

*up to 10 minutes*, and workspace readiness*up to 20 minutes*.Check your language model inference service and get the service IP address using the

`kubectl get svc`

command.`export SERVICE_IP=$(kubectl get svc workspace-custom-llm -o jsonpath='{.spec.clusterIP}')`

Test your custom model inference service with a sample input of your choice using the

[OpenAI API format](https://platform.openai.com/docs/api-reference/chat):`kubectl run -it --rm --restart=Never curl --image=curlimages/curl -- curl -X POST http://$SERVICE_IP/v1/completions \ -H "Content-Type: application/json" \ -d '{ "model": "bloom-1b7", "prompt": "What sport should I play in rainy weather?", "max_tokens": 20 }'`


## Clean up resources

If you no longer need these resources, you can delete them to avoid incurring extra Azure compute charges.

Delete the KAITO inference workspace using the `kubectl delete workspace`

command.

```
kubectl delete workspace workspace-custom-llm
```


## Next steps

In this article, you learned how to onboard a HuggingFace model for inferencing with the AI toolchain operator add-on directly to your AKS cluster. To learn more about AI and machine learning on AKS, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/resize-cluster -->

# Resize Azure Kubernetes Service (AKS) clusters

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to resize an Azure Kubernetes Service (AKS) cluster. It's important to right-size your clusters to optimize costs and performance. You can manually resize a cluster by adding or removing the nodes to meet the needs of your applications. You can also autoscale your cluster to automatically adjust the number of nodes in response to changing demands.

## Cluster right-sizing

When you create an AKS cluster, you specify the number of nodes and the size of the nodes, which determines the compute capacity of the cluster. Oversized clusters can lead to unnecessary costs, while undersized clusters can lead to performance issues. You can adjust the number and size of the nodes in the cluster to right-size the cluster to meet the needs of your applications.

Consider the following factors when right-sizing your cluster:

**Resource requirements**: Understand the resource requirements of your applications to determine the number of nodes and the size of the nodes needed to run your workloads.**Performance requirements**: Determine the performance requirements of your applications to ensure that the cluster can meet the demands of your workloads.**Cost considerations**: Optimize costs by right-sizing your cluster to avoid unnecessary costs associated with oversized clusters.**Application demands**: Monitor the demands of your applications to adjust the size of the cluster in response to changing demands.**Infrastructure constraints**: Consider the infrastructure constraints of your environment, such as capacity or reserved instance limiting to specific SKUs, to ensure that the cluster can be right-sized within the limits of your environment.

## Monitor cluster performance and cost

Closely monitor the performance and cost of your clusters to ensure they're right-sized to meet the needs of your application and make adjustments as needed. You can use the following resources for monitoring:

[Identify high CPU usage in Azure Kubernetes Service (AKS) clusters](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/identify-high-cpu-consuming-containers-aks)[Troubleshoot memory saturation in Azure Kubernetes Service (AKS) clusters](/en-us/troubleshoot/azure/azure-kubernetes/availability-performance/identify-memory-saturation-aks)[Cost analysis add-on for Azure Kubernetes Service (AKS)](cost-analysis)[Configure the Metrics Server Vertical Pod Autoscaler (VPA) in Azure Kubernetes Service (AKS)](use-metrics-server-vertical-pod-autoscaler)

## When to resize a cluster

You might want to resize a cluster in scenarios such as the following:

- If you see that CPU and memory usage is consistently low, consider
*downsizing*the cluster. If usage is consistently high, make sure you have[autoscaling enabled](#automatically-resize-an-aks-cluster)and increase the maximum node count if necessary. - The
[cost analysis add-on for AKS](cost-analysis)shows you details about node usage and cost that indicate you might benefit from cluster resizing. For example, if you see that your nodes have a*high idle cost*with a*low usage cost*, you might consider resizing your cluster to reduce costs. - The
[Metrics Server VPA](use-metrics-server-vertical-pod-autoscaler)shows you that your requests and/or limits are too high or low based on historical usage. You can use this information to adjust your cluster size to better match your workload. - You experience performance issues such as resource starvation. This might be a result of the cluster being undersized for the demands of your applications.

## What happens when I resize a cluster?

### Increasing cluster size

You can increase the size of an AKS cluster by adding nodes to the cluster. You can [add nodes to the cluster manually](scale-cluster) or [configure autoscaling to automatically adjust the number of nodes](#automatically-resize-an-aks-cluster) in response to changing demands.

When you increase the size of a cluster, the following changes occur:

- New node instances are created using the same configuration as the existing nodes in the cluster.
- New pods might be scheduled on the new nodes to distribute the workload across the cluster.
- Existing pods don't move to the new nodes unless they are rescheduled due to node failures or other reasons.

### Decreasing cluster size

You can decrease the size of an AKS cluster by removing nodes from the cluster. When you remove nodes from the cluster, the nodes are automatically drained and removed from the cluster. You can remove nodes from the cluster manually or configure autoscaling to automatically adjust the number of nodes in response to changing demands.

When you decrease the size of a cluster, the following changes occur:

- AKS gracefully terminates the nodes and drains the pods running on the nodes before removing the nodes from the cluster.
- Any pods managed by a replication controller are rescheduled on other node instances in the cluster.
- Any pods that aren't managed by a replication controller aren't restarted.

## Manually resize an AKS cluster

- Resize an AKS cluster using the
command with the`az aks scale`

`--node-count`

and`--nodepool-name`

parameters.

Before running the resize command, set the required environment variables with your own values. The example values should be substituted with your actual resource group, cluster, desired node count, and node pool name.

```
az aks scale --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --node-count $NUM_NODES --nodepool-name $NODE_POOL_NAME
```


Results:

```
{
"agentPoolProfiles": [
{
"count": 4,
"maxCount": null,
"minCount": null,
"name": "nodepool1",
...
}
],
"dnsPrefix": "xxxxx",
"fqdn": "xxxxx.xxxxx.xxxxxx.cloudapp.azure.com",
...
}
```


Repeat this command for each node pool in the cluster that you want to resize. If your cluster has only one node pool, you can omit the `--nodepool-name`

parameter.

## Automatically resize an AKS cluster

Use the [cluster autoscaler](cluster-autoscaler-overview) to automatically resize your node pools in response to changing demands.

For more information, see the [Cluster autoscaling in Azure Kubernetes Service (AKS) overview](cluster-autoscaler-overview). To configure cluster autoscaling in AKS, see [Use the cluster autoscaler in Azure Kubernetes Service (AKS)](cluster-autoscaler).

## Next steps

In this article, you learned how to right-size an AKS cluster. To learn more about managing AKS clusters, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-batch-jobs-with-kueue -->

# Schedule and deploy batch jobs with Kueue on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to schedule and deploy sample batch jobs on Azure Kubernetes Service (AKS) using Kueue. Also, this guide covers installing Kueue, configuring ResourceFlavors and ClusterQueues for fine-grained resource management, and submitting jobs via LocalQueues. You also learn how to use Kueue to queue up a sample batch job and track the results across Pending, Running, and Finished states.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

To learn more about Kueue and common uses cases for batch workload administrators and users, see [Kueue overview on AKS](kueue-overview).

## Prerequisites

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Azure CLI installed on your local machine. To install or upgrade, see
[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). [Helm version 3 or above](https://helm.sh/docs/intro/install/)installed.[The latest version of Kueue installed in a dedicated namespace on your cluster](kueue-overview#prerequisites).

## Define a ResourceFlavor object

In Kueue, a ResourceFlavors enables fine-grained resource management by associating workloads with specific nodes, taints, tolerations, or availability zones. For nodes, `ResourceFlavors`

can define the characteristics like pricing, availability, brands, models, and architecture (that is, x86 versus ARM CPUs). A `ClusterQueue`

uses these flavors to manage quotas and admission policies for workloads.

This configuration defines a `ResourceFlavor`

without any labels or taints, known as an empty `ResourceFlavor`

. This configuration is perfect when quotas for different flavors don't need to be managed.

Create and save a

`ResourceFlavor`

in a file named`resourceflavor-sample.yaml`

with the following manifest:`cat << EOF > resourceflavor-sample.yaml apiVersion: kueue.x-k8s.io/v1beta1 kind: ResourceFlavor metadata: name: on-demand EOF`

apply

`kubectl apply -f resourceflavor-sample.yaml`

verify

`kubectl get resourceflavors`

Example output

`NAME AGE on-demand 5m32s`


## Create a ClusterQueue

A ClusterQueue is a cluster-scoped resource that governs a pool of resources, defining usage limits and Fair Sharing rules. Where applicable, Fair Sharing rules allow another ClusterQueue in the **same** cohort to unused quota for pending jobs. Each ClusterQueue specifies which flavors it supports and how much quota is available for each.

This sample `ClusterQueue`

defines:

: Indicates that`namespaceSelector: {}`

`sample-jobs`

accepts workloads from any namespace that references this`ClusterQueue`

via a`LocalQueue`

(you can restrict usage (for example, to only team A's namespace) with a label selector).: Defines the standard CPU and memory resource types managed by this`coveredResources: ["cpu", "memory"]`

in`resourceGroups`

`ClusterQueue`

.: Only workloads scheduled on`flavor`

of`on-demand`

nodes with`4`

CPUs,`8Gi`

memory`on-demand`

nodes consume this quota. If the cluster uses up this quota, it doesn't admit any other workloads using this flavor (unless you allow borrowing from the`cohort`

).

Create and save a Kueue

`ClusterQueue`

in a file named`clusterqueue-sample.yaml`

with the following manifest:`cat <<EOF > clusterqueue-sample.yaml apiVersion: kueue.x-k8s.io/v1beta1 kind: ClusterQueue metadata: name: sample-jobs spec: cohort: general namespaceSelector: {} # Accept workloads from any namespace resourceGroups: - coveredResources: ["cpu", "memory"] flavors: - name: on-demand resources: - name: "cpu" nominalQuota: 4 - name: "memory" nominalQuota: 8Gi EOF`

Apply the

`ClusterQueue`

manifest using the`kubectl apply`

command.`kubectl apply -f clusterqueue-sample.yaml`

Verify the ClusterQueue` manifest was applied

`kubectl get clusterqueues`

Example output

`NAME COHORT PENDING WORKLOADS sample-jobs general 0`


Note

The `ClusterQueue`

isn't ready for use until a `ResourceFlavor`

object is configured. If you create a `ClusterQueue`

without any existing `ResourceFlavor`

, workloads referencing it are marked as `Inadmissible`

.

## Create a LocalQueue

A LocalQueue is a namespace-scoped resource that acts as a gateway for users to submit jobs. A `LocalQueue`

is assigned to one `ClusterQueue`

from which resources are allocated to run its workloads.

This sample `LocalQueue`

configures the following settings:

- Enables users in the
`batch-jobs`

namespace to submit batch workloads to Kueue. - Route the batch workloads to the
`sample-jobs`

`ClusterQueue`

, which manages the actual compute resource quotas and scheduling policies.

Create a namespace named

*batch-jobs*using the`kubectl create`

command.`kubectl create ns batch-jobs`

Create and save a

`LocalQueue`

in a file named`localqueue-sample.yaml`

with the following YAML manifest:`cat <<EOF > localqueue-sample.yaml apiVersion: kueue.x-k8s.io/v1beta1 kind: LocalQueue metadata: name: sample-queue namespace: batch-jobs spec: clusterQueue: sample-jobs EOF`

Apply the

`LocalQueue`

manifest using the`kubectl apply`

command.`kubectl apply -f localqueue-sample.yaml`

Verify the

`LocalQueue`

manifest was applied`kubectl get localqueues --all-namespaces`

Exampmle output

`NAMESPACE NAME CLUSTERQUEUE PENDING WORKLOADS ADMITTED WORKLOADS batch-jobs sample-queue sample-jobs 0 0`


## Create 2 batch jobs

This configuration defines two Kubernetes batch jobs submitted to the batch-jobs namespace and assigned to the sample-queue managed by Kueue. Both jobs are single-instance (parallelism: 1, completions: 1) and are configured with `Never`

restart policy. The fields `parallelism`

and `completions`

control how many pods are run and how the job is considered complete. So `parallelism`

and `completions`

of 1 means that one pod can run at once, and the job is marked as complete once one pod finishes successfully, per batch job.

- Job test-batch-1: Requests one CPU and 500Mi memory
- Job test-batch-2: Requests two CPUs and 1Gi memory

Create two sample batch jobs to deploy in the

*batch-jobs*namespace using the following YAML manifest named`batch-workloads.yaml`

:`cat <<EOF > batch-workloads.yaml apiVersion: batch/v1 kind: Job metadata: name: test-batch-1 namespace: batch-jobs labels: kueue.x-k8s.io/queue-name: sample-queue spec: parallelism: 1 completions: 1 template: spec: containers: - name: dummy-job image: registry.k8s.io/e2e-test-images/agnhost:2.53 command: ["sh", "-c", "echo Running test-batch-1; sleep 60"] resources: requests: cpu: "1" memory: "500Mi" limits: cpu: "1" memory: "500Mi" restartPolicy: Never --- apiVersion: batch/v1 kind: Job metadata: name: test-batch-2 namespace: batch-jobs labels: kueue.x-k8s.io/queue-name: sample-queue spec: parallelism: 1 completions: 1 template: spec: containers: - name: dummy-job image: registry.k8s.io/e2e-test-images/agnhost:2.53 command: ["sh", "-c", "echo Waiting in queue for CPUs...; sleep 30"] resources: requests: cpu: "2" memory: "1Gi" limits: cpu: "2" memory: "1Gi" restartPolicy: Never EOF`

Apply the manifest for the batch jobs using the

`kubectl apply`

command.`kubectl apply -f batch-workloads.yaml`


## Verify Batch Jobs are Submitted to `LocalQueue`


View the status of the batched workloads using the

`kubectl get`

command.`kubectl get workloads --namespace batch-jobs`

Example output

`NAME ADMITTED AGE test-batch-1 True 10s test-batch-2 False 5s`

Run the following command for

`test-batch-2`

while it is in a`Pending`

state`kubectl get workloads test-batch-2 -o yaml`

Expected output

`... ... Status: Conditions: Type: Admitted Status: False Reason: QuotaUnavailable Message: Insufficient quota in ClusterQueue sample-jobs (flavor on-demand): requested 2 CPUs, available 1 ... ...`

After

`test-batch-1`

completes,`test-batch-2`

will be admitted and run.Now, the output should look like the following example output:

`Status: Conditions: Type: Admitted Status: True Last Transition Time: 1234-56-78T00:00:00Z Admission: ClusterQueue: sample-jobs PodSetAssignments: Name: main Flavors: cpu: on-demand memory: on-demand ResourceUsage: cpu: 2 memory: 1Gi`

View the final status of the

`batch-jobs`

namespace using the`kubectl get`

command.`kubectl get job,deploy,rs,pod,workload --namespace batch-jobs`

Example output

`NAME STATUS COMPLETIONS DURATION AGE job.batch/test-batch-1 Complete 1/1 97s 3m15s job.batch/test-batch-2 Complete 1/1 35s 3m15s NAME READY STATUS RESTARTS AGE pod/test-batch-1-hb8zl 0/1 Completed 0 3m15s pod/test-batch-2-dx9hk 0/1 Completed 0 3m15s NAME QUEUE RESERVED IN ADMITTED FINISHED AGE workload.kueue.x-k8s.io/job-test-batch-1-6fb85 sample-queue sample-jobs True True 3m15s workload.kueue.x-k8s.io/job-test-batch-2-84f49 sample-queue sample-jobs True True 3m15s`


## FAQ

### Question 1: How can I confirm that the Kueue controller is available and running as expected?

Confirm the Kueue controller manager pod is running using the

`kubectl get`

command.`kubectl get pods --namespace kueue-system`

The Kueue controller manager pod should be in a

`Running`

state with`1/1`

containers ready, as shown in the following example output:`NAME READY STATUS RESTARTS AGE kueue-controller-manager-xxxxxxx 1/1 Running 0 2m`

If the

`Status`

shows`CrashLoopBackOff`

or`Pending`

, check the deployment logs using the`kubectl logs`

command.`kubectl logs --namespace kueue-system deployment/kueue-controller-manager`


### Question 2: One or more of the Kueue custom resources (CRDs) are missing when I install via Helm. How can I ensure all of the CRDs are installed?

After installing Kueue with the

[Kueue overview on AKS](kueue-overview)guidance, confirm that all of the CRDs are installed using the`kubectl get`

command.`kubectl get crds | grep kueue`

These CRDs should be listed, as shown in the following example output:

`admissionchecks.kueue.x-k8s.io clusterqueues.kueue.x-k8s.io cohorts.kueue.x-k8s.io localqueues.kueue.x-k8s.io multikueueclusters.kueue.x-k8s.io multikueueconfigs.kueue.x-k8s.io provisioningrequestconfigs.kueue.x-k8s.io resourceflavors.kueue.x-k8s.io topologies.kueue.x-k8s.io workloadpriorityclasses.kueue.x-k8s.io workloads.kueue.x-k8s.io`

If one or more of the CRDs are missing, you might see errors in controller logs, failed job queuing,

`CrashLoopBackOff`

for the controller, or inability to admit or schedule workloads. In this case, you can manually reinstall the Kueue CRDs using the`kubectl apply`

command.`kubectl apply -f https://github.com/kubernetes-sigs/kueue/releases/latest/download/kueue-crds.yaml`

Note

Note that if you manually install the CRDs, you need to manually delete them once you're finished using the

`kubectl delete`

command.

### Question 3: What's the difference between a LocalQueue and a ClusterQueue

A ClusterQueue is a cluster-scoped resource that defines and governs a pool of compute resources like CPU, memory, pods, and accelerators across the entire Kubernetes cluster. A LocalQueue is a namespace-scoped resource that acts as a gateway for users to submit jobs within the defined Kubernetes cluster. This separation allows for fine-grained control over resource allocation and multi-tenant scheduling without exposing cluster-wide quotas directly to users.

How they work together:

- A user submits a job to a LocalQueue in their namespace.
- Kueue routes the job to the referenced ClusterQueue.
- The ClusterQueue checks resource availability and quota limits.
- If admitted, the job is unsuspended and scheduled.

## Next steps

In this article, you:

- Installed Kueue on your Azure Kubernetes Service (AKS) cluster using Helm and verified CRDs, controller health, and namespace setup.
- Configured
`ClusterQueue`

and`LocalQueue`

for general-purpose workloads with resource quotas and flavors (such as on-demand). - Submitted two batch jobs to demonstrate queuing: one admitted immediately, the second held due to quota limits, then admitted when resources became available.
- Monitored workload status and controller logs to confirm scheduling behavior and queuing logic.

To learn more about Kueue, visit the following resources:

[Multi-cluster scheduling and resource placement with Kueue and KubeFleet on AKS](https://blog.aks.azure.com/2025/04/02/Scaling-Kubernetes-for-AI-and-Data-intensive-Workloads).[Kueue developer tools](https://kueue.sigs.k8s.io/docs/tasks/dev/)official documentation.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/workload-identity-migrate-from-pod-identity -->

# Migrate Azure Kubernetes Service (AKS) pods from pod-managed identity to Microsoft Entra Workload ID

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Migrate AKS pods from pod-managed identities to [Microsoft Entra Workload ID](workload-identity-overview) (workload identity) using one of three approaches based on your current [Azure Identity SDK](/en-us/entra/identity-platform/reference-v2-libraries) version: latest SDK parallel deployment, migration sidecar proxy (Linux only), or SDK rewrite.

## Prerequisites

- Azure CLI version 2.47.0 or later. Run the
`az --version`

command to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Set environment variables

The following table lists the environment variables used in the commands throughout this article. Make sure to replace the placeholder values with your own values.

| Environment variable | Description | Example value |
|---|---|---|
`SUBSCRIPTION_ID` |
The ID of the Azure subscription where the AKS cluster and managed identity are created. | `00000000-0000-0000-0000-000000000000` |
`RESOURCE_GROUP` |
The name of the resource group where the AKS cluster and managed identity are created. | `myResourceGroup` |
`LOCATION` |
The Azure region where the AKS cluster and managed identity are created. | `eastus` |
`CLUSTER_NAME` |
The name of the AKS cluster. | `myAKSCluster` |
`MANAGED_IDENTITY_NAME` |
The name of the user-assigned managed identity. | `myManagedIdentity` |
`SERVICE_ACCOUNT_NAME` |
The name of the Kubernetes service account to create or associate with the managed identity. | `workload-identity-sa` |
`SERVICE_ACCOUNT_NAMESPACE` |
The namespace of the Kubernetes service account. | `default` |
`FEDERATED_IDENTITY_NAME` |
The name of the federated identity credential to create. | `myFederatedIdentity` |

## Choose a migration path

Select the appropriate migration approach based on your current Azure Identity SDK version:

**Latest Azure Identity SDK**: If your application already uses the latest version of Azure Identity SDK, you can migrate by deploying Microsoft Entra Workload ID in parallel with existing pod-managed identity.**Older SDK with migration sidecar**- If your application uses an older SDK version and runs on Linux containers, you can use a temporary migration sidecar to proxy Instance Metadata Service (IMDS) transactions while planning your SDK upgrade.**Older SDK rewrite approach**: If your application uses an older SDK version, you can update your application code to use the latest Azure Identity SDK, then migrate to workload identity.

## Prepare for migration

For all migration paths, you need to have the federated trust set up before you update your application to use Microsoft Entra Workload ID. The following are the minimum steps required:

[Create a managed identity](#create-a-managed-identity)credential.- Associate the user-assigned managed identity with the Kubernetes service account already used for the pod-managed identity or
[create a new Kubernetes service account](#create-kubernetes-service-account)and then associate it with the managed identity. [Establish a federated trust relationship](#establish-federated-identity-credential-trust)between the managed identity and Microsoft Entra ID using the[OpenID Connect (OIDC)](/en-us/azure/active-directory/develop/v2-protocols-oidc)issuer URL and the service account.

## Migrate from latest version of Azure Identity SDK

**This migration path applies when** your application already uses the latest version of the Azure Identity SDK and you want to migrate with minimal code changes.

**Migration approach**: Deploy Microsoft Entra Workload ID in parallel with pod-managed identity, verify functionality, then remove pod-managed identity.

**Steps**:

- Deploy Microsoft Entra Workload ID in parallel with existing pod-managed identity.
- Restart your application deployment to begin using Microsoft Entra Workload ID (OIDC annotations are injected automatically).
- Verify the application can authenticate successfully using workload identity.
[Remove the pod-managed identity](#remove-pod-managed-identity)annotations from your application.- Remove the pod-managed identity add-on from your cluster.

## Use a migration sidecar (Linux containers only)

**This migration path applies when** your application uses an older version of the Azure Identity SDK, runs on Linux containers, and you need a temporary solution while planning SDK updates.

**Migration approach**: Deploy a migration sidecar that proxies IMDS transactions to OIDC, allowing your existing application code to work without immediate changes.

**Important limitations**:

**Linux containers only**. Windows containers aren't supported.**Temporary solution**that's not intended for long-term production use.**Planning required**to schedule SDK updates for long-term support.

**Steps**:

[Deploy the workload with migration sidecar](#deploy-the-workload-with-migration-sidecar)to proxy IMDS transactions.- Verify authentication transactions complete successfully.
- Schedule application SDK updates to supported Azure Identity versions.
- Once SDKs are updated, remove the proxy sidecar and redeploy applications.

## Rewrite application for latest Azure Identity SDK

**This migration path applies when** your application uses an older version of the Azure Identity SDK and you want to update to the latest supported SDK before migrating.

**Migration approach**: Update your application code to use the latest Azure Identity SDK, then migrate to Microsoft Entra Workload ID with the updated code.

**Technical outcomes**:

- Uses current Azure Identity SDK versions (no deprecation timeline).
- Supports both Linux and Windows containers (unlike sidecar approach).
- Eliminates proxy components and IMDS translation overhead.

**Steps**:

- Update your application code to use the latest
[Azure Identity SDK](workload-identity-overview#prerequisites). - Test the updated application with pod-managed identity.
- Restart your application deployment to begin authenticating using Microsoft Entra Workload ID (OIDC annotations are injected automatically).
- Verify authentication transactions complete successfully.
[Remove the pod-managed identity](#remove-pod-managed-identity)annotations and add-on.

## Set an active Azure subscription

Set a specific Azure subscription as the current active subscription using the

command.`az account set`

`az account set --subscription $SUBSCRIPTION_ID`


## Create a managed identity

Create a managed identity using the

command.`az identity create`

`az identity create --name $MANAGED_IDENTITY_NAME --resource-group $RESOURCE_GROUP --location $LOCATION --subscription $SUBSCRIPTION_ID`


## Get managed identity client ID

Get the client ID of the managed identity and save it to an environmental variable using the

command.`az identity show`

`export USER_ASSIGNED_CLIENT_ID="$(az identity show --resource-group $RESOURCE_GROUP --name $MANAGED_IDENTITY_NAME --query 'clientId' -otsv)"`


## Grant managed identity access to Azure resources

- Grant the managed identity the permissions needed to access the required Azure resources. Follow the steps in
[Assign a managed identity access to a resource](/en-us/azure/role-based-access-control/role-assignments-portal-managed-identity)to assign the appropriate role to the managed identity.

## Get OIDC issuer URL

Get the OIDC issuer URL and save it to an environmental variable using the

command.`az aks show`

`export AKS_OIDC_ISSUER="$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query "oidcIssuerProfile.issuerUrl" -o tsv)"`

The variable should contain an issuer URL similar to the following example:

`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/`

By default, the issuer uses the base URL

`https://{region}.oic.prod-aks.azure.com/{uuid}`

, where the value for`{region}`

matches the location the AKS cluster is deployed in. The value`{uuid}`

represents the OIDC key.

## Get AKS cluster credentials

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP`


## Create Kubernetes service account

Create a Kubernetes service account and annotate it with the managed identity client ID using the

`kubectl apply`

command. Make sure to replace the placeholder values with your own values.`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${USER_ASSIGNED_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`

The following output resembles successful creation of the identity:

`Serviceaccount/workload-identity-sa created`


## Establish federated identity credential trust

Create the federated identity credential between the managed identity, service account issuer, and subject using the

command.`az identity federated-credential create`

`az identity federated-credential create --name $FEDERATED_IDENTITY_NAME --identity-name $MANAGED_IDENTITY_NAME --resource-group $RESOURCE_GROUP --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME} --audience api://AzureADTokenExchange`

The federated identity credential takes a few minutes to propagate after being added. If a token request is made immediately after adding the federated identity credential, the token request might fail because the Azure AD directory cache contains outdated information.


## Deploy the workload with migration sidecar

If your application uses user-assigned managed identity and still relies on IMDS to get an access token you can use the migration sidecar to start migrating to Microsoft Entra Workload ID. In long-term applications, you should modify the code to use the latest Azure Identity SDKs that support client assertion.

To update or deploy the workload, add the following [pod annotations](workload-identity-overview#pod-annotations) to your pod specification (only if you want to use the migration sidecar):

| Pod annotation | Description | Value |
|---|---|---|
`azure.workload.identity/inject-proxy-sidecar` |
Indicates whether to inject the proxy sidecar into the pod. | `true` or `false` |
`azure.workload.identity/proxy-sidecar-port` |
Desired port for the proxy sidecar. | Default value: `8000` |

When you create a pod with these annotations, the Microsoft Entra Workload ID mutating webhook automatically injects the `init-container`

and proxy sidecar to the pod spec. The following YAML shows an example of what the mutating webhook adds to the pod deployment:

```
apiVersion: v1
kind: Pod
metadata:
name: httpbin-pod
labels:
app: httpbin
azure.workload.identity/use: "true"
annotations:
azure.workload.identity/inject-proxy-sidecar: "true"
spec:
serviceAccountName: workload-identity-sa
initContainers:
- name: init-networking
image: mcr.microsoft.com/oss/azure/workload-identity/proxy-init:v1.1.0
securityContext:
capabilities:
add:
- NET_ADMIN
drop:
- ALL
privileged: true
runAsUser: 0
env:
- name: PROXY_PORT
value: "8000"
containers:
- name: nginx
image: nginx:alpine
ports:
- containerPort: 80
- name: proxy
image: mcr.microsoft.com/oss/azure/workload-identity/proxy:v1.1.0
ports:
- containerPort: 8000
```


## Verify the workload with migration sidecar

Verify the pod is in a running state using the

command. Replace`kubectl describe pod`

`<pod-name>`

with the name of your pod.`kubectl describe pods <pod-name>`

Verify the pod is passing IMDS transactions using the

command. Replace`kubectl logs`

`<pod-name>`

with the name of your pod.`kubectl logs <pod-name>`

The following example log output resembles successful communication through the proxy sidecar. Verify the logs show a token is successfully acquired and the

`GET`

operation is successful.`I0926 00:29:29.968723 1 proxy.go:97] proxy "msg"="starting the proxy server" "port"=8080 "userAgent"="azure-workload-identity/proxy/v0.13.0-12-gc8527f3 (linux/amd64) c8527f3/2022-09-26-00:19" I0926 00:29:29.972496 1 proxy.go:173] proxy "msg"="received readyz request" "method"="GET" "uri"="/readyz" I0926 00:29:30.936769 1 proxy.go:107] proxy "msg"="received token request" "method"="GET" "uri"="/metadata/identity/oauth2/token?resource=https://management.core.windows.net/api-version=2018-02-01&client_id=<client_id>" I0926 00:29:31.101998 1 proxy.go:129] proxy "msg"="successfully acquired token" "method"="GET" "uri"="/metadata/identity/oauth2/token?resource=https://management.core.windows.net/api-version=2018-02-01&client_id=<client_id>"`


## Remove pod-managed identity

After you complete your testing and the application can successfully get a token using the proxy sidecar, you can remove the identity and pod-managed identity mapping from your AKS cluster

Remove the pod-managed identity binding from your pod using the

command. Replace`az aks pod-identity delete`

`<pod-identity-name>`

and`<pod-identity-namespace>`

with the name and namespace of your pod identity.`az aks pod-identity delete --name <pod-identity-name> --namespace <pod-identity-namespace> --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME`


## Related content

For more information about Microsoft Entra Workload ID, see the [Overview](workload-identity-overview) article.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-settings -->

# Configure the Dapr extension for your Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes project

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After [completing the prerequisites for installing the Dapr extension](dapr), you can configure the [Dapr](https://dapr.io/) extension to work best for you and your project using various configuration options, like:

- Rotating expiring certificates
- Provisioning Dapr with high availability (HA) enabled
- Limiting which of your nodes use the Dapr extension
- Setting automatic custom resource definition (CRD) updates
- Configuring the Dapr release namespace

The extension enables you to set Dapr configuration options by using the `--configuration-settings`

parameter in the Azure CLI or `configurationSettings`

property in a Bicep template.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Update configuration settings

Important

Some configuration options cannot be modified post-creation. Adjustments to these options require deletion and recreation of the extension, applicable to the following settings:

`global.ha.*`

`dapr_placement.*`


HA is enabled by default. Disabling it requires deletion and recreation of the extension.

To update your Dapr configuration settings, recreate the extension with the desired state. For example, let's say you previously created and installed the extension using the following configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2"
```


To update the `dapr_operator.replicaCount`

from two to three, use the following command:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=3"
```


## Manage mTLS certificates

The Dapr extension supports in-transit encryption of communication between Dapr instances using the Dapr Sentry service control plane, which is a central Certificate Authority (CA). With the Sentry service, you can encrypt communication using self-signed or user-supplied x.509 certificates. [Learn more about setting up mTLS certificates in the open-source Dapr documentation.](https://docs.dapr.io/operations/security/mtls/#dapr-generated-self-signed-certificates)

You can [bring in your own certificates](https://docs.dapr.io/operations/security/mtls/#bringing-your-own-certificates), or let [Dapr automatically create and persist self-signed root and issuer certificates](https://docs.dapr.io/operations/security/mtls/#dapr-generated-self-signed-certificates).

Important

If you don't explicitly configure certificates, [Dapr defaults to generating self-signed certificates](#manage-dapr-generated-self-signed-certificates), which are generally valid for 1 year. **Currently, using self-signed certificates generated by Dapr is not recommended.** Best practice is to generate custom certificates and update them manually.

### Manage Dapr-generated self-signed certificates

If you haven't provided any custom certificates, Dapr automatically creates and persists self-signed certificates, valid for 1 year. The Dapr extension installs the `dapr-trust-bundle`

secret, which contains certificate information under the default `dapr-system`

namespace.

#### Check expiry of current Dapr-generated self-signed certificates

You can check when the Dapr root certificate of your Kubernetes cluster expires by using [the Dapr CLI](https://docs.dapr.io/getting-started/install-dapr-cli/).

```
dapr mtls expiry
```


**Expected output:**

```
Root certificate expires in 8759 hours. Expiry date: 2025-12-06 18:14:20 +0000 UTC
```


You can also find the expiration date for your current certificate in the Kubernetes `dapr-trust-bundle`

secret data.

```
kubectl get secret dapr-trust-bundle -n dapr-system -o jsonpath='{.data.issuer\.crt}' | base64 -d | openssl x509 -noout -dates
```


**Expected output:**

```
notBefore=Dec 6 17:59:20 2024 GMT
notAfter=Dec 6 18:14:20 2025 GMT
```


#### Generate a new Dapr-generated self-signed certificate

**Via the Dapr CLI (recommended)**

Refer to Dapr's[Root and issuer certificate upgrade using CLI](https://docs.dapr.io/operations/security/mtls/#root-and-issuer-certificate-upgrade-using-cli-recommended)guide.**Via**Refer to Dapr's`kubectl`

commands[Updating root or issuer certs using Kubectl](https://docs.dapr.io/operations/security/mtls/#updating-root-or-issuer-certs-using-kubectl)guide.

### Manage your own user-supplied x.509 certificates

You can also bring your own custom certificates.

**Generate custom certificates**

Create your own custom certificate; for example,[an Azure Key Vault certificate](/en-us/azure/key-vault/certificates/certificate-scenarios).**Update your custom certficate manually**

Follow[the instructions provided in the Dapr open source documentation to update your custom certificates manually](https://docs.dapr.io/operations/security/mtls/#custom-certificates-bring-your-own)using.`kubectl`


## Provision Dapr with high availability (HA) enabled

Provision Dapr with high availability (HA) enabled by setting the `global.ha.enabled`

parameter to `true`

.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2"
```


Note

If configuration settings are sensitive and need to be protected (for example, cert-related information), pass the `--configuration-protected-settings`

parameter and the value will be protected from being read.

If no configuration-settings are passed, the Dapr configuration defaults to:

```
ha:
enabled: true
replicaCount: 3
disruption:
minimumAvailable: ""
maximumUnavailable: "25%"
prometheus:
enabled: true
port: 9090
mtls:
enabled: true
workloadCertTTL: 24h
allowedClockSkew: 15m
```


For a list of available options, see [Dapr configuration](https://github.com/dapr/dapr/blob/master/charts/dapr/README.md#configuration).

## Limit the extension to certain nodes

In some configurations, you may only want to run Dapr on certain nodes. You can limit the extension by passing a `nodeSelector`

in the extension configuration. If the desired `nodeSelector`

contains `.`

, you must escape them from the shell and the extension. For example, the following configuration installs Dapr only to nodes with `topology.kubernetes.io/zone: "us-east-1c"`

:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2" \
--configuration-settings "global.nodeSelector.kubernetes\.io/zone=us-east-1c"
```


For managing OS and architecture, use the [supported versions](https://github.com/dapr/dapr/blob/b8ae13bf3f0a84c25051fcdacbfd8ac8e32695df/docker/docker.mk#L50) of the `global.daprControlPlaneOs`

and `global.daprControlPlaneArch`

configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2" \
--configuration-settings "global.daprControlPlaneOs=linux" \
--configuration-settings "global.daprControlPlaneArch=amd64"
```


## Install Dapr in multiple availability zones while in HA mode

By default, the placement service uses a storage class of type `standard_LRS`

. It's recommended to create a **zone redundant storage class** while installing Dapr in HA mode across multiple availability zones. For example, to create a `zrs`

type storage class, add the `storageaccounttype`

parameter:

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: custom-zone-redundant-storage
provisioner: disk.csi.azure.com
reclaimPolicy: Delete
allowVolumeExpansion: true
volumeBindingMode: WaitForFirstConsumer
parameters:
storageaccounttype: Premium_ZRS
```


When installing Dapr, use the storage class you used in the YAML file:

```
az k8s-extension create --cluster-type managedClusters
--cluster-name XXX
--resource-group XXX
--name XXX
--extension-type Microsoft.Dapr
--auto-upgrade-minor-version XXX
--version XXX
--configuration-settings "dapr_placement.volumeclaims.storageClassName=custom-zone-redundant-storage"
```


## Configure the Dapr release namespace

You can configure the release namespace.

The Dapr extension gets installed in the `dapr-system`

namespace by default. To override it, use `--release-namespace`

. To redefine the namespace, include the cluster `--scope`

.

```
az k8s-extension create \
--cluster-type managedClusters \
--cluster-name dapr-aks \
--resource-group dapr-rg \
--name my-dapr-ext \
--extension-type microsoft.dapr \
--release-train stable \
--auto-upgrade false \
--version 1.9.2 \
--scope cluster \
--release-namespace dapr-custom
```


## Show current configuration settings

Use the `az k8s-extension show`

command to show the current Dapr configuration settings:

```
az k8s-extension show --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr
```


## Set Dapr monitoring log levels

You can configure settings for the Dapr monitoring component with your AKS cluster extension. For exmaple, to update `dapr_monitoring`

log levels to "warn" (only notified when receiving a warning or error), set the following `configuration-settings`

:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_monitoring.logLevel=warn"
```


## Set the outbound proxy for Dapr extension for Azure Arc on-premises

If you want to use an outbound proxy with the Dapr extension for AKS, you can do so by:

- Setting the proxy environment variables using the
:`dapr.io/env`

annotations`HTTP_PROXY`

`HTTPS_PROXY`

`NO_PROXY`


[Installing the proxy certificate in the sidecar](https://docs.dapr.io/operations/configuration/install-certificates/).

## Updating your Dapr installation version

If you are on a specific Dapr version and you don't have `--auto-upgrade-minor-version`

available, you can use the following command to upgrade or downgrade Dapr:

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--version 1.12.0 # Version to upgrade or downgrade to
```


The preceding command updates the Dapr control plane *only.* To update the Dapr sidecars, restart your application deployments:

```
kubectl rollout restart deploy/<DEPLOYMENT-NAME>
```


## Using Azure Linux-based images

From Dapr version 1.8.0, you can use Azure Linux images with the Dapr extension. To use them, set the `global.tag`

flag:

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--set global.tag=1.10.0-mariner
```


[Learn more about using Mariner-based images with Dapr](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-deploy/#using-mariner-based-images).[Learn more about deploying Azure Linux on AKS](cluster-configuration#azure-linux-container-host-for-aks).

## Disable automatic CRD updates

From Dapr version 1.9.2, CRDs are automatically upgraded when the extension upgrades. To disable this setting, you can set `hooks.applyCrds`

to `false`

.

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--configuration-settings "hooks.applyCrds=false"
```


Note

CRDs are only applied in case of upgrades and are skipped during downgrades.

## Meet network requirements

The Dapr extension requires the following outbound URLs on `https://:443`

to function on AKS and Arc for Kubernetes:

`https://mcr.microsoft.com/daprio`

URL for pulling Dapr artifacts.- The
[outbound URLs required for AKS or Arc for Kubernetes](/en-us/azure/azure-arc/kubernetes/network-requirements).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-node-taints -->

# Use node taints in an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to use node taints in an Azure Kubernetes Service (AKS) cluster.

## Overview

The AKS scheduling mechanism is responsible for placing pods onto nodes and is based upon the upstream Kubernetes scheduler, [kube-scheduler](https://kubernetes.io/docs/concepts/scheduling-eviction/kube-scheduler/). You can constrain a pod to run on particular nodes by attaching the pods to a set of nodes using [node affinity](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#affinity-and-anti-affinity) or by instructing the node to repel a set of pods using [node taints](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/), which interact with the AKS scheduler.

Node taints work by marking a node so that the scheduler avoids placing certain pods on the marked nodes. You can place [tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/) on a pod to allow the scheduler to schedule that pod on a node with a matching taint. Taints and tolerations work together to help you control how the scheduler places pods onto nodes. For more information, see [example use cases of taints and tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#example-use-cases:%7E:text=not%20be%20evicted.-,Example%20Use%20Cases,-Taints%20and%20tolerations).

Taints are key-value pairs with an [effect](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/). There are three values for the effect field when using node taints: `NoExecute`

, `NoSchedule`

, and `PreferNoSchedule`

.

`NoExecute`

: Pods already running on the node are immediately evicted if they don't have a matching toleration. If a pod has a matching toleration, it might be evicted if`tolerationSeconds`

are specified.`NoSchedule`

: Only pods with a matching toleration are placed on this node. Existing pods aren't evicted.`PreferNoSchedule`

: The scheduler avoids placing any pods that don't have a matching toleration.

### Node taint options

There are two types of node taints that can be applied to your AKS nodes: **node taints** and **node initialization taints**.

**Node taints**are meant to remain permanently on the node for scheduling pods with node affinity. Node taints can only be added, updated, or removed completely using the AKS API.**Node initialization taints**are placed on the node at boot time and are meant to be used temporarily, such as in scenarios where you might need extra time to set up your nodes. You can remove node initialization taint using the Kubernetes API and they aren't guaranteed during the node lifecycle. They will appear on new replicas of the node when it is scaled up or on all replicas when a node is upgraded. If you want to remove the initialization taints completely, you can remove them using the AKS API after untainting the nodes using the Kubernetes API. Once you remove the initialization taints from the cluster spec using the AKS API, newly created nodes don't come up with those initialization taints. If the initialization taint is still present on existing nodes, you can permanently remove it by performing a node image upgrade operation.

Note

Node taints and labels applied using the AKS node pool API aren't modifiable from the Kubernetes API and vice versa. Modifications to system taints aren't allowed.

This doesn't apply to node initialization taints.

## Use node taints

### Prerequisites

This article assumes you have an existing AKS cluster. If you need an AKS cluster, you can create one using [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

### Create a node pool with a node taint

Create a node pool with a taint using the

command and use the`az aks nodepool add`

`--node-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 1 \ --node-taints "sku=gpu:NoSchedule" \ --no-wait`


### Update a node pool to add a node taint

Update a node pool to add a node taint using the

command and use the`az aks nodepool update`

`--node-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.`az aks nodepool update \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-taints "sku=gpu:NoSchedule" \ --no-wait`


## Use node initialization taints (preview)

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Prerequisites and limitations

- You need the Azure CLI version
`3.0.0b3`

or later installed and configured. Run`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - You can only apply initialization taints via cluster create or upgrade when using the AKS API. If using ARM template that will result in a Managed Cluster level operation, you can specify node initialization taints during node pool creation and update. Agentpool level operations are blocked when
`NodeInitializationTaints`

are present in the request body. - You can't apply initialization taints to Windows node pools using the Azure CLI.

### Get the credentials for your cluster

Get the credentials for your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $CLUSTER_NAME`


### Install the `aks-preview`

Azure CLI extension

Register or update the aks-preview extension using the

or`az extension add`

command.`az extension update`

`# Register the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the `NodeInitializationTaintsPreview`

feature flag

Register the

`NodeInitializationTaintsPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "NodeInitializationTaintsPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "NodeInitializationTaintsPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create a cluster with a node initialization taint

Create a cluster with a node initialization taint using the

command and the`az aks create`

`--node-initialization-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.Important

The node initialization taints you specify apply to all of the node pools in the cluster. To apply the initialization taint to a specific node, you can use an ARM template instead of the CLI.

`az aks create \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-count 1 \ --node-init-taints "sku=gpu:NoSchedule" \ --generate-ssh-keys`


### Update a cluster to add a node initialization taint

Update a cluster to add a node initialization taint using the

command and the`az aks update`

`--node-initialization-taints`

parameter to specify`sku=gpu:NoSchedule`

for the taint.Important

When updating a cluster with a node initialization taint, the taints apply to all node pools in the cluster. If your nodes are using VMSS, you can view updates to node initialization taints on the node after the node's VMSS model is updated (for example, after a node image version upgrade operation). Initialization taints will not appear on your nodes until an operation that triggers a VMSS model update occurs.

`az aks update \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-init-taints "sku=gpu:NoSchedule"`


## Check the status of the node pool

After applying the node taint or initialization taint, check the status of the node pool using the

command.`az aks nodepool list`

`az aks nodepool list --resource-group $RESOURCE_GROUP_NAME --cluster-name $CLUSTER_NAME`

If you applied node taints, the following example output shows that the

`<node-pool-name>`

node pool is`Creating`

nodes with the specified`nodeTaints`

:`[ { ... "count": 1, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Creating", ... "nodeTaints": [ "sku=gpu:NoSchedule" ], ... }, ... ]`

If you applied node initialization taints, the following example output shows that the

`<node-pool-name>`

node pool is`Creating`

nodes with the specified`nodeInitializationTaints`

:`[ { ... "count": 1, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Creating", ... "nodeInitializationTaints": [ "sku=gpu:NoSchedule" ], ... }, ... ]`


## Check that the taint is set on the node

Check the node taints and node initialization taints in the node configuration using the

`kubectl describe node`

command.`kubectl describe node $NODE_NAME`

If you applied node taints, the following example output shows that the

`<node-pool-name>`

node pool has the specified`Taints`

:`[ ... Name: <node-pool-name> ... Taints: sku=gpu:NoSchedule ... ], ... ... ]`


Important

If your nodes are using VMSS, node initialization taints will not be visible on actual nodes in your cluster until an operation that triggers VMSS model update occurs (for example, Kubernetes version upgrade or node image version upgrade).

## Remove node taints

### Remove a specific node taint

Remove node taints using the

command. The following example command removes the`az aks nodepool update`

`"sku=gpu:NoSchedule"`

node taint from the node pool.`az aks nodepool update \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --node-taints ""`


### Remove all node taints

Remove all node taints from a node pool using the

command. The following example command removes all node taints from the node pool.`az aks nodepool update`

`az aks nodepool update \ --cluster-name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP_NAME \ --name $NODE_POOL_NAME \ --node-taints ""`


## Remove node initialization taints

You have the following options to remove node initialization taints from the node:

**Remove node initialization taints temporarily**using the Kubernetes API. If you remove them this way, the taints reappear after node scaling or upgrade occurs. New nodes still have the node initialization taint after scaling. Node initialization taints appear on all nodes after upgrading.**Remove node initialization taints permanently**by untainting the node using the Kubernetes API, and then removing the taint using the AKS API. Once the initialization taints are removed from cluster spec using AKS API, newly created nodes after reimage operations no longer have initialization taints.

When you remove all initialization taint occurrences from node pool replicas, the existing initialization taint might reappear after an upgrade with any new initialization taints.

### Remove node initialization taints temporarily

Remove node initialization taints temporarily using the

`kubectl taint nodes`

command.This command removes the taint from only the specified node. If you want to remove the taint from every node in the node pool, you need to run the command for every node that you want the taint removed from.

`kubectl taint nodes $NODE_POOL_NAME sku=gpu:NoSchedule-`

Once removed, node initialization taints reappear after node scaling or upgrading occurs.


### Remove node initialization taints permanently

Follow steps in

[Remove node initialization taints temporarily](#remove-node-initialization-taints-temporarily)to remove the node initialization taint using the Kubernetes API.Remove the taint from the node using the AKS API using the

command. This command removes the node initialization taint from every node in the cluster.`az aks update`

`az aks update \ --resource-group $RESOURCE_GROUP_NAME \ --name $CLUSTER_NAME \ --node-init-taints ""`


## Check that the taint has been removed from the node

Check the node taints and node initialization taints in the node configuration using the

`kubectl describe node`

command.`kubectl describe node $NODE_NAME`

If you removed a node taint, the following example output shows that the

`<node-pool-name>`

node pool doesn't have the removed taint under`Taints`

:`[ ... Name: <node-pool-name> ... Taints: ... ], ... ... ]`


## Next steps

- Learn more about example use cases for
[taints and tolerations](https://kubernetes.io/docs/concepts/scheduling-eviction/taint-and-toleration/#example-use-cases:%7E:text=not%20be%20evicted.-,Example%20Use%20Cases,-Taints%20and%20tolerations). - Learn more about
[best practices for advanced AKS scheduler features](operator-best-practices-advanced-scheduler). - Learn more about Kubernetes labels in the
[Kubernetes labels documentation](https://kubernetes.io/docs/concepts/overview/working-with-objects/labels/).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/enable-fips-nodes -->

# Enable Federal Information Process Standard (FIPS) for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Federal Information Processing Standard (FIPS) 140-2 is a US government standard that defines minimum security requirements for cryptographic modules in information technology products and systems. Azure Kubernetes Service (AKS) allows you to create Linux and Windows node pools with FIPS 140-2 enabled. Deployments running on FIPS-enabled node pools can use those cryptographic modules to provide increased security and help meet security controls as part of FedRAMP compliance. For more information on FIPS 140-2, see [Federal Information Processing Standard (FIPS) 140](/en-us/azure/compliance/offerings/offering-fips-140-2).

Caution

In this article, there are references to a feature that may be using Ubuntu OS versions that are being deprecated for AKS.

- Starting on March 17, 2027, AKS will no longer support Ubuntu 20.04. Existing node images will be deleted and AKS will no longer provide security updates. You'll no longer be able to scale your node pools.
[Upgrade your node pools](upgrade-aks-cluster)to kubernetes version 1.35+ to migrate to a supported Ubuntu version. For more information on this retirement, see[AKS GitHub Issues](https://github.com/Azure/AKS/issues)

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

Azure CLI version 2.32.0 or later installed and configured. To find the version, run `az --version`

. For more information about installing or upgrading the Azure CLI, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Note

AKS Monitoring Addon supports FIPS enabled node pools with Ubuntu, Azure Linux, and Windows starting with Agent version 3.1.17 (Linux) and Win-3.1.17 (Windows).

## Limitations

- FIPS-enabled node pools have the following limitations:
- FIPS-enabled node pools require Kubernetes version 1.19 and greater.
- To update the underlying packages or modules used for FIPS, you must use
[Node Image Upgrade](node-image-upgrade). - Container images on the FIPS nodes aren't assessed for FIPS compliance.
- Mounting of a CIFS share fails because FIPS disables some authentication modules. To work around this issue, see
[Errors when mounting a file share on a FIPS-enabled node pool](/en-us/troubleshoot/azure/azure-kubernetes/fail-to-mount-azure-file-share#fipsnodepool). - FIPS-enabled node pools with
[Arm64 VMs](use-arm64-vms)are only supported with Azure Linux 3.0+. - FIPS isn't supported with
[Flatcar Container Linux for AKS (preview)](flatcar-container-linux-for-aks).


Important

The FIPS-enabled Linux image is a different image than the default Linux image used for Linux-based node pools.

FIPS-enabled node images can have different version numbers, such as kernel version, than images that aren't FIPS-enabled. The update cycle for FIPS-enabled node pools and node images can differ from node pools and images that aren't FIPS-enabled.

## Supported OS Versions

You can create FIPS-enabled node pools on all supported OS types (Linux and Windows). However, not all OS versions support FIPS-enabled node pools. After a new OS version is released, there's typically a waiting period before it's FIPS compliant.

This table includes the supported OS versions:

| OS Type | OS SKU | FIPS Compliance |
|---|---|---|
| Linux | Ubuntu | Supported |
| Linux | Azure Linux | Supported |
| Windows | Windows Server 2019 | Supported |
| Windows | Windows Server 2022 | Supported |

When requesting FIPS enabled Ubuntu, if the default Ubuntu version doesn't support FIPS, AKS defaults to the most recent FIPS-supported version of Ubuntu. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support FIPS, AKS defaults to Ubuntu 20.04 for Linux FIPS-enabled node pools.

Note

Previously, you could use the GetOSOptions API to determine whether a given OS supported FIPS. The GetOSOptions API is now deprecated and it will no longer be included in new AKS API versions starting with 2024-05-01.

## Create a FIPS-enabled Linux node pool

Create a FIPS-enabled Linux node pool using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command with the`--enable-fips-image`

parameter.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name fipsnp \ --enable-fips-image`

Note

You can also use the

`--enable-fips-image`

parameter with the[az aks create](/en-us/cli/azure/aks#az-aks-create)command when creating a cluster to enable FIPS on the default node pool. When adding node pools to a cluster created in this way, you still must use the`--enable-fips-image`

parameter when adding node pools to create a FIPS-enabled node pool.Verify your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows the

*fipsnp*node pool is FIPS-enabled:`Name enableFips --------- ------------ fipsnp True nodepool1 False`

List the nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

The following example output shows a list of the nodes in the cluster. The nodes starting with

`aks-fipsnp`

are part of the FIPS-enabled node pool.`NAME STATUS ROLES AGE VERSION aks-fipsnp-12345678-vmss000000 Ready agent 6m4s v1.19.9 aks-fipsnp-12345678-vmss000001 Ready agent 5m21s v1.19.9 aks-fipsnp-12345678-vmss000002 Ready agent 6m8s v1.19.9 aks-nodepool1-12345678-vmss000000 Ready agent 34m v1.19.9`

Run a deployment with an interactive session on one of the nodes in the FIPS-enabled node pool using the

`kubectl debug`

command.`kubectl debug node/aks-fipsnp-12345678-vmss000000 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

From the interactive session output, verify the FIPS cryptographic libraries are enabled. Your output should look similar to the following example output:

`root@aks-fipsnp-12345678-vmss000000:/# cat /proc/sys/crypto/fips_enabled 1`

FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Create a FIPS-enabled Windows node pool

Create a FIPS-enabled Windows node pool using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command with the`--enable-fips-image`

parameter. Unlike Linux-based node pools, Windows node pools share the same image set.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name fipsnp \ --enable-fips-image \ --os-type Windows`

Verify your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

Verify Windows node pools have access to the FIPS cryptographic libraries by

[creating an RDP connection to a Windows node](rdp)in a FIPS-enabled node pool and check the registry. From the**Run**application, enter`regedit`

.Look for

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\FIPSAlgorithmPolicy`

in the registry.If

`Enabled`

is set to*1*, then FIPS is enabled.FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Update an existing node pool to enable or disable FIPS

Existing Linux node pools can be updated to enable or disable FIPS. If you're planning to migrate your node pools from non-FIPS to FIPS, first validate that your application is working properly in a test environment before migrating it to a production environment. Validating your application in a test environment should prevent issues caused by the FIPS kernel blocking some weak cipher or encryption algorithm, such as an MD4 algorithm that isn't FIPS compliant.

Note

When updating an existing Linux node pool to enable or disable FIPS, the node pool update moves between the fips and non-fips image. This node pool update triggers a reimage to complete the update. This can cause the node pool update to take a few minutes to complete.

### Prerequisites

Azure CLI version 2.64.0 or later. To find the version, run `az --version`

. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Enable FIPS on an existing node pool

Existing Linux node pools can be updated to enable FIPS. When you update an existing node pool, the node image changes from the current image to the recommended FIPS image of the same OS SKU.

Update a node pool using the

[az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)command with the`--enable-fips-image`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

Verify that your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows that the

*np*node pool is FIPS-enabled:`Name enableFips --------- ------------ np True nodepool1 False`

List the nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

The following example output shows a list of the nodes in the cluster. The nodes starting with

`aks-np`

are part of the FIPS-enabled node pool.`NAME STATUS ROLES AGE VERSION aks-np-12345678-vmss000000 Ready agent 6m4s v1.19.9 aks-np-12345678-vmss000001 Ready agent 5m21s v1.19.9 aks-np-12345678-vmss000002 Ready agent 6m8s v1.19.9 aks-nodepool1-12345678-vmss000000 Ready agent 34m v1.19.9`

Run a deployment with an interactive session on one of the nodes in the FIPS-enabled node pool using the

`kubectl debug`

command.`kubectl debug node/aks-np-12345678-vmss000000 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

From the interactive session output, verify the FIPS cryptographic libraries are enabled. Your output should look similar to the following example output:

`root@aks-np-12345678-vmss000000:/# cat /proc/sys/crypto/fips_enabled 1`

FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Disable FIPS on an existing node pool

Existing Linux node pools can be updated to disable FIPS. When updating an existing node pool, the node image changes from the current FIPS image to the recommended non-FIPS image of the same OS SKU. The node image change will occur after a reimage.

Update a Linux node pool using the

[az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)command with the`--disable-fips-image`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --disable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

Verify that your node pool isn't FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows that the

*np*node pool isn't FIPS-enabled:`Name enableFips --------- ------------ np False nodepool1 False`


## Message of the Day

Pass the `--message-of-the-day`

flag with the location of the file to replace the Message of the Day on Linux nodes at cluster creation or node pool creation.

Create a cluster with message of the day using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command.

```
az aks create --cluster-name myAKSCluster --resource-group myResourceGroup --message-of-the-day ./newMOTD.txt
```


Add a node pool with message of the day using the [az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --message-of-the-day ./newMOTD.txt
```


## Next steps

To learn more about AKS security, see [Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-security).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-support-policy -->

# Support policy for Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article outlines the support policy for the Istio-based service mesh add-on for Azure Kubernetes Service (AKS).

## Versioning and support policy

### Service mesh add-on release calendar

The Istio-based service mesh add-on release calendar indicates each revision's AKS compatibility and estimated release and deprecation dates.

New minor revisions and patches are rolled out as part of AKS releases. Announcements about the releases of new minor revisions or patches to the Istio-based service mesh add-on are published in the [AKS release notes](https://github.com/Azure/AKS/releases). To see real-time updates of regional release status and AKS release notes containing updates about Istio revision support, visit the [AKS release status webpage](https://releases.aks.azure.com/).

| Service mesh revision | Upstream release | AKS release | End of life | Compatible AKS versions | Compatible AKS LTS versions |
|---|---|---|---|---|---|
| asm-1-17 | Feb 2023 | Apr 2023 | Jan 2024 | 1.23, 1.24, 1.25, 1.26, 1.27, 1.28 | |
| asm-1-18 | Jun 2023 | Nov 2023 | Feb 2024 | 1.24, 1.25, 1.26, 1.27, 1.28 | |
| asm-1-19 | Sept 2023 | Jan 2024 | Jun 2024 | 1.25, 1.26, 1.27, 1.28 | |
| asm-1-20 | Nov 2023 | Feb 2024 | Sept 2024 | 1.25, 1.26, 1.27, 1.28, 1.29 | |
| asm-1-21 | Mar 2024 | Apr 2024 | Oct 2024 | 1.26, 1.27, 1.28, 1.29, 1.30 | |
| asm-1-22 | May 2024 | Jul 2024 | March 2025 | 1.27, 1.28, 1.29, 1.30 | |
| asm-1-23 | Aug 2024 | Sept 2024 | June 2025 | 1.27, 1.28, 1.29, 1.30, 1.31, 1.32 | |
| asm-1-24 | Nov 2024 | Feb 2025 | Sept 2025 | 1.28, 1.29, 1.30, 1.31, 1.32, 1.33 | |
| asm-1-25 | Mar 2025 | May 2025 | Jan 2026 | 1.29, 1.30, 1.31, 1.32, 1.33 | 1.28, 1.29, 1.30, 1.31, 1.32, 1.33 |
| asm-1-26 | May 2025 | July 2025 | ~Feb 2026 (expected) | 1.29, 1.30, 1.31, 1.32, 1.33, 1.34 | 1.28, 1.29, 1.30, 1.31, 1.32, 1.33, 1.34 |
| asm-1-27 | Aug 2025 | Sept 2025 | ~May 2026 (expected) | 1.29, 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 | 1.29, 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 |
| asm-1-28 | Nov 2025 | Jan 2026 | ~Aug 2026 (expected) | 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 | 1.30, 1.31, 1.32, 1.33, 1.34, 1.35 |

If using an AKS [long term-support (LTS) cluster](long-term-support), a newer revision may be declared as compatible when a previous compatible Istio revision reaches end of life before the AKS LTS version's end of life. For more details, read Istio's [AKS compatibility policy](#aks-compatibility).

### Supported revisions

**Minor revision**:- At any given time, at least two revisions of the Istio-based service mesh add-on are supported.
- An older revision
`n-2`

will continue to be supported until six weeks after the newest revision`n`

starts rolling out to all regions. For example, if`asm-1-22`

just started rolling out to all regions,`asm-1-20`

will be deprecated after six weeks. - Deprecation means no new mesh installations can be done with this revision. While clusters already having this revision continue to work, for support issues and security patches, it's recommended to
[upgrade to a newer supported mesh revision](istio-upgrade#minor-revision-upgrade).

**Patch version**:- Patches to Istio control plane (istiod) and Istio ingresses are rolled out as part of AKS releases. User is expected to follow AKS release notes on availability of newer patch versions and to then
[upgrade istio-proxy sidecars by restarting their workloads](istio-upgrade#patch-version-upgrade). - AKS reserves the right to deprecate patches if a critical Common Vulnerability and Exposure (CVE) or security vulnerability is detected. For awareness on patch availability and any ad-hoc deprecation, refer to
[AKS release notes](https://github.com/Azure/AKS/releases)and visit the[AKS release status webpage](https://releases.aks.azure.com/).

- Patches to Istio control plane (istiod) and Istio ingresses are rolled out as part of AKS releases. User is expected to follow AKS release notes on availability of newer patch versions and to then

### Default revision

If a revision isn't explicitly provided by user during installation, the `n-1`

revision is installed by default. For example, if `asm-1-22`

is the latest revision, the default is `asm-1-21`

.

### AKS compatibility

Each revision of the add-on is compatible with a set of AKS minor versions established by the [upstream Istio support and release calendar](https://istio.io/latest/docs/releases/supported-releases/#support-status-of-istio-releases).

**AKS LTS clusters may be compatible with additional revisions beyond upstream Istio's support table.** For Istio revisions `asm-1-25`

+ and AKS LTS versions 1.28+, every supported AKS LTS version will have *at least one* compatible Istio revision.

To check the compatible AKS versions for an Istio revision, use the command [ az aks mesh get-revisions](/en-us/cli/azure/aks/mesh#az-aks-mesh-get-revisions):

```
az aks mesh get-revisions --location <location> -o table
```


This command has been updated to include separate `CompatibleWith`

outputs for `KubernetesOfficial`

(standard tier) and `AKSLongTermSupport`

, replacing the earlier response that only included `kubernetes`

(standard tier).

If using the Azure portal to enable the Istio add-on for an existing cluster, the available Istio revisions will be filtered based on the cluster's tier.

Each Istio add-on revision follows upstream lifecycle for end of life and patch availability. This means:

Every Istio revision will not be compatible with every AKS LTS version, but every AKS LTS version will be compatible with at least one Istio add-on revision.

If an Istio revision reaches end of life before the AKS LTS version it is compatible with, a newer revision will be declared compatible with that LTS version. The add-on will need to be upgraded to stay in support.

For example, if

`asm-1-26`

is compatible with AKS LTS 1.28, and`asm-1-26`

reaches end of life,`asm-1-27`

may become compatible with 1.28 LTS instead.

## Allowed, supported, and blocked customizations

The Istio-based service mesh add-on for AKS designates features and [configuration options](istio-meshconfig#allowed-supported-and-blocked-meshconfig-values) as `allowed`

, `supported`

, or `blocked`

.

**Blocked**: Disallowed features and configuration options are blocked via add-on managed admission webhooks. The API server immediately publishes the error message to the user that the feature is disallowed.**Supported**: Supported features receive support from Azure support.**Allowed**: Allowed features are open and available to Istio add-on users but aren't covered by Azure support.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/developer-best-practices-resource-management -->

# Best practices for application developers to manage resources in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you develop and run applications in Azure Kubernetes Service (AKS), there are a few key areas to consider. The way you manage your application deployments can negatively impact the end-user experience of services you provide.

This article focuses on running your clusters and workloads from an application developer perspective. For information about administrative best practices, see [Cluster operator best practices for isolation and resource management in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-isolation).

This article covers the following topics:

- Pod resource requests and limits.
- Ways to develop, debug, and deploy applications with Bridge to Kubernetes and Visual Studio Code.

## Define pod resource requests and limits


Best practice guidanceSet pod requests and limits on all pods in your YAML manifests. If the AKS cluster uses

resource quotasand you don't define these values, your deployment may be rejected.

Use pod requests and limits to manage compute resources within an AKS cluster. Pod requests and limits inform the Kubernetes scheduler of the compute resources to assign to a pod.

### Pod CPU/Memory requests

*Pod requests* define a set amount of CPU and memory the pod needs regularly.

In your pod specifications, it's important you define these requests and limits based on the above information. If you don't include these values, the Kubernetes scheduler can't consider the resources your applications require to help with scheduling decisions.

Monitor the performance of your application to adjust pod requests. If you underestimate pod requests, your application may receive degraded performance due to over-scheduling a node. If requests are overestimated, your application may have increased scheduling difficulty.

### Pod CPU/Memory limits

*Pod limits* set the maximum amount of CPU and memory a pod can use. *Memory limits* define which pods should be removed when nodes are unstable due to insufficient resources. Without proper limits set, pods are removed until resource pressure is lifted. While a pod may exceed the *CPU limit* periodically, the pod isn't removed for exceeding the CPU limit.

Pod limits define when a pod loses control of resource consumption. When it exceeds the limit, the pod is marked for removal. This behavior maintains node health and minimizes impact to pods sharing the node. If you don't set a pod limit, it defaults to the highest available value on a given node.

Avoid setting a pod limit higher than your nodes can support. Each AKS node reserves a set amount of CPU and memory for the core Kubernetes components. Your application may try to consume too many resources on the node for other pods to successfully run.

Monitor the performance of your application at different times during the day or week. Determine peak demand times and align the pod limits to the resources required to meet maximum needs.

Important

In your pod specifications, define these requests and limits based on the above information. Failing to include these values prevents the Kubernetes scheduler from accounting for resources your applications require to help with scheduling decisions.

If the scheduler places a pod on a node with insufficient resources, application performance is degraded. Cluster administrators **must set resource quotas** on a namespace that requires you to set resource requests and limits. For more information, see

[resource quotas on AKS clusters](operator-best-practices-scheduler#enforce-resource-quotas).

When you define a CPU request or limit, the value is measured in CPU units.

*1.0*CPU equates to one underlying virtual CPU core on the node.- The same measurement is used for GPUs.

- You can define fractions measured in millicores. For example,
*100 m*is*0.1*of an underlying vCPU core.

In the following basic example for a single NGINX pod, the pod requests *100 m* of CPU time and *128Mi* of memory. The resource limits for the pod are set to *250 m* CPU and *256Mi* memory.

```
kind: Pod
apiVersion: v1
metadata:
name: mypod
spec:
containers:
- name: mypod
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
resources:
requests:
cpu: 100m
memory: 128Mi
limits:
cpu: 250m
memory: 256Mi
```


For more information about resource measurements and assignments, see [Managing compute resources for containers](https://kubernetes.io/docs/concepts/configuration/manage-compute-resources-container/).

## Develop and debug applications against an AKS cluster


Best practice guidanceDevelopment teams should deploy and debug against an AKS cluster using Bridge to Kubernetes.


With Bridge to Kubernetes, you can develop, debug, and test applications directly against an AKS cluster. Developers within a team collaborate to build and test throughout the application lifecycle. You can continue to use existing tools such as Visual Studio or Visual Studio Code with the Bridge to Kubernetes extension.

Using integrated development and test process with Bridge to Kubernetes reduces the need for local test environments like [minikube](https://kubernetes.io/docs/setup/minikube/). Instead, you develop and test against an AKS cluster, even in secured and isolated clusters.

Note

Bridge to Kubernetes is intended for use with applications running on Linux pods and nodes.

## Use the Visual Studio Code (VS Code) extension for Kubernetes


Best practice guidanceInstall and use the VS Code extension for Kubernetes when you write YAML manifests. You can also use the extension for integrated deployment solution, which may help application owners that infrequently interact with the AKS cluster.


The [Visual Studio Code extension for Kubernetes](https://github.com/Azure/vscode-kubernetes-tools) helps you develop and deploy applications to AKS. The extension provides the following features:

Intellisense for Kubernetes resources, Helm charts, and templates.

The ability to browse, deploy, and edit capabilities for Kubernetes resources from within VS Code.

Intellisense checks for resource requests or limits being set in the pod specifications:


## Next steps

This article focused on how to run your cluster and workloads from a cluster operator perspective. For information about administrative best practices, see [Cluster operator best practices for isolation and resource management in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-isolation).

To implement some of these best practices, see [Develop with Bridge to Kubernetes](/en-us/visualstudio/containers/overview-bridge-to-kubernetes).

---
<!-- Source: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __deploy-extensions-az-cli___generation-2-vm_generation-2-vms_tutorial-kubernete_5dae70.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _deploy-extensions-az-cli___generation-2-vm_generation-2-vms_tutorial-kubernetes_0a80b9.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: deploy-extensions-az-cli.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/deploy-extensions-az-cli -->

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

<!-- DOCUMENTO FUSIONADO: __generation-2-vm_generation-2-vms_tutorial-kubernetes-prepare-app.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _generation-2-vm_generation-2-vms.md -->
<!-- URL ORIGINAL: N/A -->

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


---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-prepare-app.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-app -->

# Tutorial - Prepare an application for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this tutorial, you prepare a multi-container application to use in Kubernetes. You use existing development tools like Docker Compose to locally build and test the application. You learn how to:

- Clone a sample application source from GitHub.
- Create a container image from the sample application source.
- Test the multi-container application in a local Docker environment.

Once completed, the following application runs in your local development environment:

In later tutorials, you upload the container image to an Azure Container Registry (ACR), and then deploy it into an AKS cluster.

## Before you begin

This tutorial assumes a basic understanding of core Docker concepts such as containers, container images, and `docker`

commands. For a primer on container basics, see [Get started with Docker](https://docs.docker.com/get-started/).

To complete this tutorial, you need a local Docker development environment running Linux containers. Docker provides packages that configure Docker on a [Mac](https://docs.docker.com/desktop/install/mac-install/), [Windows](https://docs.docker.com/desktop/install/windows-install/), or [Linux](https://docs.docker.com/desktop/install/linux-install/) system.

Note

Azure Cloud Shell doesn't include the Docker components required to complete every step in these tutorials. Therefore, we recommend using a full Docker development environment.

## Get application code

The [sample application](https://github.com/Azure-Samples/aks-store-demo) used in this tutorial is a basic store front app including the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Use

[git](https://git-scm.com/downloads)to clone the sample application to your development environment.`git clone https://github.com/Azure-Samples/aks-store-demo.git`

Change into the cloned directory.

`cd aks-store-demo`


## Review Docker Compose file

The sample application you create in this tutorial uses the [ docker-compose-quickstart YAML file](https://github.com/Azure-Samples/aks-store-demo/blob/main/docker-compose-quickstart.yml) from the

[repository](https://github.com/Azure-Samples/aks-store-demo/tree/main)you cloned.

```
services:
rabbitmq:
image: rabbitmq:3.13.2-management-alpine
container_name: 'rabbitmq'
restart: always
environment:
- "RABBITMQ_DEFAULT_USER=username"
- "RABBITMQ_DEFAULT_PASS=password"
ports:
- 15672:15672
- 5672:5672
healthcheck:
test: ["CMD", "rabbitmqctl", "status"]
interval: 30s
timeout: 10s
retries: 5
volumes:
- ./rabbitmq_enabled_plugins:/etc/rabbitmq/enabled_plugins
networks:
- backend_services
order-service:
build: src/order-service
container_name: 'order-service'
restart: always
ports:
- 3000:3000
healthcheck:
test: ["CMD", "wget", "-O", "/dev/null", "-q", "http://order-service:3000/health"]
interval: 30s
timeout: 10s
retries: 5
environment:
- ORDER_QUEUE_HOSTNAME=rabbitmq
- ORDER_QUEUE_PORT=5672
- ORDER_QUEUE_USERNAME=username
- ORDER_QUEUE_PASSWORD=password
- ORDER_QUEUE_NAME=orders
- ORDER_QUEUE_RECONNECT_LIMIT=3
networks:
- backend_services
depends_on:
rabbitmq:
condition: service_healthy
product-service:
build: src/product-service
container_name: 'product-service'
restart: always
ports:
- 3002:3002
healthcheck:
test: ["CMD", "wget", "-O", "/dev/null", "-q", "http://product-service:3002/health"]
interval: 30s
timeout: 10s
retries: 5
environment:
- AI_SERVICE_URL=http://ai-service:5001/
networks:
- backend_services
store-front:
build: src/store-front
container_name: 'store-front'
restart: always
ports:
- 8080:8080
healthcheck:
test: ["CMD", "wget", "-O", "/dev/null", "-q", "http://store-front:80/health"]
interval: 30s
timeout: 10s
retries: 5
environment:
- VUE_APP_PRODUCT_SERVICE_URL=http://product-service:3002/
- VUE_APP_ORDER_SERVICE_URL=http://order-service:3000/
networks:
- backend_services
depends_on:
- product-service
- order-service
networks:
backend_services:
driver: bridge
```


## Create container images and run application

You can use [Docker Compose](https://docs.docker.com/compose/) to automate building container images and the deployment of multi-container applications.

### Docker

Create the container image, download the RabbitMQ image, and start the application using the

`docker compose`

command:`docker compose -f docker-compose-quickstart.yml up -d`

View the created images using the

command.`docker images`

`docker images`

The following condensed example output shows the created images:

`REPOSITORY TAG IMAGE ID aks-store-demo-product-service latest 72f5cd7e6b84 aks-store-demo-order-service latest 54ad5de546f9 aks-store-demo-store-front latest 1125f85632ae ...`

View the running containers using the

command.`docker ps`

`docker ps`

The following condensed example output shows four running containers:

`CONTAINER ID IMAGE f27fe74cfd0a aks-store-demo-product-service df1eaa137885 aks-store-demo-order-service b3ce9e496e96 aks-store-demo-store-front 31df28627ffa rabbitmq:3.13.2-management-alpine`


## Test application locally

To see your running application, navigate to `http://localhost:8080`

in a local web browser. The sample application loads, as shown in the following example:

, you can view products, add them to your cart, and then place an order.

## Clean up resources

Since you validated the application's functionality, you can stop and remove the running containers. * Do not delete the container images* - you use them in the next tutorial.

Stop and remove the container instances and resources using the

command.`docker-compose down`

`docker compose down`


## Next steps

In this tutorial, you created a sample application, created container images for the application, and then tested the application. You learned how to:

- Clone a sample application source from GitHub.
- Create a container image from the sample application source.
- Test the multi-container application in a local Docker environment.

In the next tutorial, you learn how to store container images in an ACR.


---

<!-- DOCUMENTO FUSIONADO: _nat-gateway_concepts-network-legacy-cni.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: nat-gateway.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/nat-gateway -->

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

<!-- DOCUMENTO FUSIONADO: concepts-network-legacy-cni.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-network-legacy-cni -->

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

<!-- DOCUMENTO FUSIONADO: ___coredns-autoscale_keda-about_kubernetes-service-principal__deploy-batch-jobs-_1b45c7.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: __coredns-autoscale_keda-about_kubernetes-service-principal.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: _coredns-autoscale_keda-about.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: coredns-autoscale.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/coredns-autoscale -->

# Autoscaling CoreDNS in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to configure and customize CoreDNS autoscaling in Azure Kubernetes Service (AKS) clusters.

## Configure CoreDNS horizontal pod scaling

Due to the elastic nature of AKS, it's common to experience sudden spikes in DNS traffic within your clusters. These spikes can lead to an increase in memory consumption by CoreDNS pods. In some cases, this increased memory consumption can cause `Out of memory`

issues.

To preempt this issue, AKS clusters autoscale CoreDNS pods to reduce memory usage per pod. The default settings for this autoscaling logic are stored in the `coredns-autoscaler`

ConfigMap. However, you might observe that the default autoscaling of CoreDNS pods isn't always aggressive enough to prevent `Out of memory`

issues for your CoreDNS pods. In this case, you can directly modify the `coredns-autoscaler`

ConfigMap. Keep in mind that simply increasing the number of CoreDNS pods without addressing the root cause of the `Out of memory`

issue might only provide a temporary fix. If there's not enough memory available across the nodes where the CoreDNS pods are running, increasing the number of CoreDNS pods won't help. You might need to investigate further and implement appropriate solutions such as optimizing resource usage, adjusting resource requests and limits, or adding more memory to the nodes.

CoreDNS uses the [horizontal cluster proportional autoscaler](https://github.com/kubernetes-sigs/cluster-proportional-autoscaler) for pod autoscaling. You can edit the `coredns-autoscaler`

to configure the scaling logic for the number of CoreDNS pods. The `coredns-autoscaler`

ConfigMap currently supports two different ConfigMap key values: `linear`

and `ladder`

, which correspond to two supported control modes.

- The
`linear`

controller yields a number of replicas in [min,max] range equivalent to`max( ceil( cores * 1/coresPerReplica ) , ceil( nodes * 1/nodesPerReplica ) )`

. - The
`ladder`

controller calculates the number of replicas by consulting two different step functions, one for core scaling and another for node scaling, yielding the max of the two replica values.

For more information on the control modes and ConfigMap format, see the [upstream documentation](https://github.com/kubernetes-sigs/cluster-proportional-autoscaler#control-patterns-and-configmap-formats).

Important

We recommend a minimum of *two* CoreDNS pod replicas per cluster.

### View the current `coredns-autoscaler`

ConfigMap

Get the current

`coredns-autoscaler`

ConfigMap using thecommand.`kubectl get configmaps`

`kubectl get configmap coredns-autoscaler --namespace kube-system --output yaml`

Your output should resemble the following example output:

`apiVersion: v1 data: ladder: '{"coresToReplicas":[[1,2],[512,3],[1024,4],[2048,5]],"nodesToReplicas":[[1,2],[8,3],[16,4],[32,5]]}' kind: ConfigMap metadata: name: coredns-autoscaler namespace: kube-system resourceVersion: "..." creationTimestamp: "..."`


Note

The configuration provided serves as a potential starting point, but you should customize the values based on your specific cluster requirements and DNS traffic patterns. One way to determine the appropriate number of replicas for your environment is to use the linear scaling formula: `replicas = max( ceil( cores * 1/coresPerReplica ) , ceil( nodes * 1/nodesPerReplica ) )`

to determine replica counts based on core / node count in the cluster.

## CoreDNS vertical pod autoscaling behavior

CoreDNS uses the original provided resource requests/limits when enabling the [add-on autoscaling feature](optimized-addon-scaling) to prevent service unavailability during the CoreDNS pod restart process.

The following table outlines the default requests/limits and request-to-limit ratios for the AKS CoreDNS add-on:

| Resource | Requests/limits | Request-to-limit ratio |
|---|---|---|
| CPU | `100 m / 3 cores` |
Approximately 1:30 |
| Memory | `70 Mi / 500 Mi` |
Approximately 1:7 |

If the recommended CPU requests are *500 m*, VPA adjusts the CPU limits to *15* to maintain this ratio. Similarly, if the recommended memory requests are *700 Mi*, VPA adjusts the memory limit to *5000 Mi*.

VPA sets CoreDNS CPU and memory limits to large values based on the VPA recommended CPU/Memory request and AKS defined request-to-limit ratio. These adjustments are beneficial for handling multiple requests during peak service times. The drawback is that CoreDNS might consume all the CPU and memory available resource on the node when the peak service time.

It's difficult to set a single ideal CPU and memory requests/limits value to meet the requirements of both large cluster and small cluster at the same time. By enabling optimized add-on scaling, you have the flexibility to customize the CoreDNS CPU and memory requests/limits or use VPA to autoscale CoreDNS to meet specific cluster requirements. Keep the following scenarios in mind when deciding whether to customize the resource configuration or use VPA:

- You're considering whether VPA is suitable for your CoreDNS service and want to only view the VPA recommendations. You can disable VPA for CoreDNS by enabling the override VPA update mode to
*Off*if you don't want VPA to automatically update the pods.[Customize the resource configuration in Deployment](customize-resource-configuration)to set the CPU/Memory requests/limits to the value you prefer. - You're considering using VPA but want to restrict the ratio of request-to-limit so VPA won't bump the CPU and Memory limit to large values at one time. You can customize resources in the Deployment and update the CPU and Memory requests/limits value to keep the ratio of request-to-limit to
*1:2*or*1:3*. - If a VPA container policy sets maxAllowed CPU and Memory, the recommended resource requests won't exceed those limits. Customizing the resource configuration allows you to increase or decrease the maxAllowed values and control the recommendations of VPA.

For more information, see [Enable add-on autoscaling on your AKS cluster (Preview)](optimized-addon-scaling).

## Next steps

To learn how to troubleshoot CoreDNS issues, see [Troubleshoot issues with CoreDNS on Azure Kubernetes Service (AKS)](coredns-troubleshoot).


---

<!-- DOCUMENTO FUSIONADO: keda-about.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/keda-about -->

# Simplified application autoscaling with Kubernetes Event-driven Autoscaling (KEDA) add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

Kubernetes Event-driven Autoscaling (KEDA) is a single-purpose and lightweight component that strives to make application autoscaling simple and is a Cloud Native Computing Federation (CNCF) Graduate project.

It applies event-driven autoscaling to scale your application to meet demand in a sustainable and cost-efficient manner with scale-to-zero.

The KEDA add-on makes it even easier by deploying a managed KEDA installation, providing you with [a rich catalog of Azure KEDA scalers](https://keda.sh/docs/scalers/) that you can scale your applications with on your Azure Kubernetes Services (AKS) cluster.

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.32.

For more information on how to securely scale your applications with workload identity, read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Architecture

[KEDA](https://keda.sh/) provides two main components:

**KEDA operator**allows end-users to scale workloads in or out from 0 to N instances with support for Kubernetes Deployments, Jobs,`StatefulSets`

, or any custom resource that defines`/scale`

subresource.**Metrics server**exposes external metrics to Horizontal Pod Autoscaler (HPA) in Kubernetes for autoscaling purposes such as messages in a Kafka topic, or number of events in an Azure event hub. Due to upstream limitations, KEDA must be the only installed external metric adapter.


Learn more about how KEDA works in the [official KEDA documentation](https://keda.sh/docs/latest/concepts/).

## Installation

KEDA can be added to your Azure Kubernetes Service (AKS) cluster by enabling the KEDA add-on using an [ARM template](keda-deploy-add-on-arm) or [Azure CLI](keda-deploy-add-on-cli).

The KEDA add-on provides a fully supported installation of KEDA that is integrated with AKS.

## Capabilities and features

KEDA provides the following capabilities and features:

- Build sustainable and cost-efficient applications with scale-to-zero
- Scale application workloads to meet demand using
[a rich catalog of Azure KEDA scalers](https://keda.sh/docs/scalers/) - Autoscale applications with
`ScaledObjects`

, such as Deployments,`StatefulSets`

, or any custom resource that defines`/scale`

subresource - Autoscale job-like workloads with
`ScaledJobs`

- Use production-grade security by decoupling autoscaling authentication from workloads
- Bring-your-own external scaler to use tailor-made autoscaling decisions
- Integrate with
[Microsoft Entra Workload ID](workload-identity-overview)for authentication

Note

If you plan to use workload identity, [enable the workload identity add-on](workload-identity-deploy-cluster) before enabling the KEDA add-on.

## Add-on limitations

The KEDA AKS add-on has the following limitations:

- KEDA's
[HTTP add-on (preview)](https://github.com/kedacore/http-add-on)to scale HTTP workloads isn't installed with the extension, but can be deployed separately. - KEDA's
[external scaler for Azure Cosmos DB](https://github.com/kedacore/external-scaler-azure-cosmos-db)to scale based on Azure Cosmos DB change feed isn't installed with the extension, but can be deployed separately. - Only one external metric server is allowed in the Kubernetes cluster. Because of that the KEDA add-on should be the only external metrics server inside the cluster.
- Multiple KEDA installations aren't supported

- It's not recommended to combine KEDA's
`ScaledObject`

with a Horizontal Pod Autoscaler (HPA) to scale the same workload. They compete with each other because KEDA uses Horizontal Pod Autoscaler (HPA) in the background and results in odd scaling behavior.- If an HPA is created first, then a KEDA
`ScaledObject`

is created and the KEDA`ScaledObject`

would fail to be created. - If a KEDA
`ScaledObject`

is created first and then an HPA is created, the HPA creation isn't blocked.

- If an HPA is created first, then a KEDA

For general KEDA questions, we recommend [visiting the FAQ overview](https://keda.sh/docs/2.14/reference/faq/).

Note

If you're using [Microsoft Entra Workload ID](/en-us/azure/aks/workload-identity-overview) and you enable KEDA before Workload ID, you need to restart the KEDA operator pods so the proper environment variables can be injected:

Restart the pods by running

`kubectl rollout restart deployment keda-operator -n kube-system`

.Obtain KEDA operator pods using

`kubectl get pod -n kube-system`

and finding pods that begin with`keda-operator`

.Verify successful injection of the environment variables by running

`kubectl describe pod <keda-operator-pod> -n kube-system`

. Under`Environment`

, you should see values for`AZURE_TENANT_ID`

,`AZURE_FEDERATED_TOKEN_FILE`

, and`AZURE_AUTHORITY_HOST`

.

## Supported Kubernetes and KEDA versions

Your cluster Kubernetes version determines which KEDA version is installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:


---

<!-- DOCUMENTO FUSIONADO: kubernetes-service-principal.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kubernetes-service-principal -->

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


---

<!-- DOCUMENTO FUSIONADO: _deploy-batch-jobs-with-kueue_workload-identity-migrate-from-pod-identity.md -->
<!-- URL ORIGINAL: N/A -->

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: deploy-batch-jobs-with-kueue.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/deploy-batch-jobs-with-kueue -->

# Schedule and deploy batch jobs with Kueue on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to schedule and deploy sample batch jobs on Azure Kubernetes Service (AKS) using Kueue. Also, this guide covers installing Kueue, configuring ResourceFlavors and ClusterQueues for fine-grained resource management, and submitting jobs via LocalQueues. You also learn how to use Kueue to queue up a sample batch job and track the results across Pending, Running, and Finished states.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

To learn more about Kueue and common uses cases for batch workload administrators and users, see [Kueue overview on AKS](kueue-overview).

## Prerequisites

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Azure CLI installed on your local machine. To install or upgrade, see
[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). [Helm version 3 or above](https://helm.sh/docs/intro/install/)installed.[The latest version of Kueue installed in a dedicated namespace on your cluster](kueue-overview#prerequisites).

## Define a ResourceFlavor object

In Kueue, a ResourceFlavors enables fine-grained resource management by associating workloads with specific nodes, taints, tolerations, or availability zones. For nodes, `ResourceFlavors`

can define the characteristics like pricing, availability, brands, models, and architecture (that is, x86 versus ARM CPUs). A `ClusterQueue`

uses these flavors to manage quotas and admission policies for workloads.

This configuration defines a `ResourceFlavor`

without any labels or taints, known as an empty `ResourceFlavor`

. This configuration is perfect when quotas for different flavors don't need to be managed.

Create and save a

`ResourceFlavor`

in a file named`resourceflavor-sample.yaml`

with the following manifest:`cat << EOF > resourceflavor-sample.yaml apiVersion: kueue.x-k8s.io/v1beta1 kind: ResourceFlavor metadata: name: on-demand EOF`

apply

`kubectl apply -f resourceflavor-sample.yaml`

verify

`kubectl get resourceflavors`

Example output

`NAME AGE on-demand 5m32s`


## Create a ClusterQueue

A ClusterQueue is a cluster-scoped resource that governs a pool of resources, defining usage limits and Fair Sharing rules. Where applicable, Fair Sharing rules allow another ClusterQueue in the **same** cohort to unused quota for pending jobs. Each ClusterQueue specifies which flavors it supports and how much quota is available for each.

This sample `ClusterQueue`

defines:

: Indicates that`namespaceSelector: {}`

`sample-jobs`

accepts workloads from any namespace that references this`ClusterQueue`

via a`LocalQueue`

(you can restrict usage (for example, to only team A's namespace) with a label selector).: Defines the standard CPU and memory resource types managed by this`coveredResources: ["cpu", "memory"]`

in`resourceGroups`

`ClusterQueue`

.: Only workloads scheduled on`flavor`

of`on-demand`

nodes with`4`

CPUs,`8Gi`

memory`on-demand`

nodes consume this quota. If the cluster uses up this quota, it doesn't admit any other workloads using this flavor (unless you allow borrowing from the`cohort`

).

Create and save a Kueue

`ClusterQueue`

in a file named`clusterqueue-sample.yaml`

with the following manifest:`cat <<EOF > clusterqueue-sample.yaml apiVersion: kueue.x-k8s.io/v1beta1 kind: ClusterQueue metadata: name: sample-jobs spec: cohort: general namespaceSelector: {} # Accept workloads from any namespace resourceGroups: - coveredResources: ["cpu", "memory"] flavors: - name: on-demand resources: - name: "cpu" nominalQuota: 4 - name: "memory" nominalQuota: 8Gi EOF`

Apply the

`ClusterQueue`

manifest using the`kubectl apply`

command.`kubectl apply -f clusterqueue-sample.yaml`

Verify the ClusterQueue` manifest was applied

`kubectl get clusterqueues`

Example output

`NAME COHORT PENDING WORKLOADS sample-jobs general 0`


Note

The `ClusterQueue`

isn't ready for use until a `ResourceFlavor`

object is configured. If you create a `ClusterQueue`

without any existing `ResourceFlavor`

, workloads referencing it are marked as `Inadmissible`

.

## Create a LocalQueue

A LocalQueue is a namespace-scoped resource that acts as a gateway for users to submit jobs. A `LocalQueue`

is assigned to one `ClusterQueue`

from which resources are allocated to run its workloads.

This sample `LocalQueue`

configures the following settings:

- Enables users in the
`batch-jobs`

namespace to submit batch workloads to Kueue. - Route the batch workloads to the
`sample-jobs`

`ClusterQueue`

, which manages the actual compute resource quotas and scheduling policies.

Create a namespace named

*batch-jobs*using the`kubectl create`

command.`kubectl create ns batch-jobs`

Create and save a

`LocalQueue`

in a file named`localqueue-sample.yaml`

with the following YAML manifest:`cat <<EOF > localqueue-sample.yaml apiVersion: kueue.x-k8s.io/v1beta1 kind: LocalQueue metadata: name: sample-queue namespace: batch-jobs spec: clusterQueue: sample-jobs EOF`

Apply the

`LocalQueue`

manifest using the`kubectl apply`

command.`kubectl apply -f localqueue-sample.yaml`

Verify the

`LocalQueue`

manifest was applied`kubectl get localqueues --all-namespaces`

Exampmle output

`NAMESPACE NAME CLUSTERQUEUE PENDING WORKLOADS ADMITTED WORKLOADS batch-jobs sample-queue sample-jobs 0 0`


## Create 2 batch jobs

This configuration defines two Kubernetes batch jobs submitted to the batch-jobs namespace and assigned to the sample-queue managed by Kueue. Both jobs are single-instance (parallelism: 1, completions: 1) and are configured with `Never`

restart policy. The fields `parallelism`

and `completions`

control how many pods are run and how the job is considered complete. So `parallelism`

and `completions`

of 1 means that one pod can run at once, and the job is marked as complete once one pod finishes successfully, per batch job.

- Job test-batch-1: Requests one CPU and 500Mi memory
- Job test-batch-2: Requests two CPUs and 1Gi memory

Create two sample batch jobs to deploy in the

*batch-jobs*namespace using the following YAML manifest named`batch-workloads.yaml`

:`cat <<EOF > batch-workloads.yaml apiVersion: batch/v1 kind: Job metadata: name: test-batch-1 namespace: batch-jobs labels: kueue.x-k8s.io/queue-name: sample-queue spec: parallelism: 1 completions: 1 template: spec: containers: - name: dummy-job image: registry.k8s.io/e2e-test-images/agnhost:2.53 command: ["sh", "-c", "echo Running test-batch-1; sleep 60"] resources: requests: cpu: "1" memory: "500Mi" limits: cpu: "1" memory: "500Mi" restartPolicy: Never --- apiVersion: batch/v1 kind: Job metadata: name: test-batch-2 namespace: batch-jobs labels: kueue.x-k8s.io/queue-name: sample-queue spec: parallelism: 1 completions: 1 template: spec: containers: - name: dummy-job image: registry.k8s.io/e2e-test-images/agnhost:2.53 command: ["sh", "-c", "echo Waiting in queue for CPUs...; sleep 30"] resources: requests: cpu: "2" memory: "1Gi" limits: cpu: "2" memory: "1Gi" restartPolicy: Never EOF`

Apply the manifest for the batch jobs using the

`kubectl apply`

command.`kubectl apply -f batch-workloads.yaml`


## Verify Batch Jobs are Submitted to `LocalQueue`


View the status of the batched workloads using the

`kubectl get`

command.`kubectl get workloads --namespace batch-jobs`

Example output

`NAME ADMITTED AGE test-batch-1 True 10s test-batch-2 False 5s`

Run the following command for

`test-batch-2`

while it is in a`Pending`

state`kubectl get workloads test-batch-2 -o yaml`

Expected output

`... ... Status: Conditions: Type: Admitted Status: False Reason: QuotaUnavailable Message: Insufficient quota in ClusterQueue sample-jobs (flavor on-demand): requested 2 CPUs, available 1 ... ...`

After

`test-batch-1`

completes,`test-batch-2`

will be admitted and run.Now, the output should look like the following example output:

`Status: Conditions: Type: Admitted Status: True Last Transition Time: 1234-56-78T00:00:00Z Admission: ClusterQueue: sample-jobs PodSetAssignments: Name: main Flavors: cpu: on-demand memory: on-demand ResourceUsage: cpu: 2 memory: 1Gi`

View the final status of the

`batch-jobs`

namespace using the`kubectl get`

command.`kubectl get job,deploy,rs,pod,workload --namespace batch-jobs`

Example output

`NAME STATUS COMPLETIONS DURATION AGE job.batch/test-batch-1 Complete 1/1 97s 3m15s job.batch/test-batch-2 Complete 1/1 35s 3m15s NAME READY STATUS RESTARTS AGE pod/test-batch-1-hb8zl 0/1 Completed 0 3m15s pod/test-batch-2-dx9hk 0/1 Completed 0 3m15s NAME QUEUE RESERVED IN ADMITTED FINISHED AGE workload.kueue.x-k8s.io/job-test-batch-1-6fb85 sample-queue sample-jobs True True 3m15s workload.kueue.x-k8s.io/job-test-batch-2-84f49 sample-queue sample-jobs True True 3m15s`


## FAQ

### Question 1: How can I confirm that the Kueue controller is available and running as expected?

Confirm the Kueue controller manager pod is running using the

`kubectl get`

command.`kubectl get pods --namespace kueue-system`

The Kueue controller manager pod should be in a

`Running`

state with`1/1`

containers ready, as shown in the following example output:`NAME READY STATUS RESTARTS AGE kueue-controller-manager-xxxxxxx 1/1 Running 0 2m`

If the

`Status`

shows`CrashLoopBackOff`

or`Pending`

, check the deployment logs using the`kubectl logs`

command.`kubectl logs --namespace kueue-system deployment/kueue-controller-manager`


### Question 2: One or more of the Kueue custom resources (CRDs) are missing when I install via Helm. How can I ensure all of the CRDs are installed?

After installing Kueue with the

[Kueue overview on AKS](kueue-overview)guidance, confirm that all of the CRDs are installed using the`kubectl get`

command.`kubectl get crds | grep kueue`

These CRDs should be listed, as shown in the following example output:

`admissionchecks.kueue.x-k8s.io clusterqueues.kueue.x-k8s.io cohorts.kueue.x-k8s.io localqueues.kueue.x-k8s.io multikueueclusters.kueue.x-k8s.io multikueueconfigs.kueue.x-k8s.io provisioningrequestconfigs.kueue.x-k8s.io resourceflavors.kueue.x-k8s.io topologies.kueue.x-k8s.io workloadpriorityclasses.kueue.x-k8s.io workloads.kueue.x-k8s.io`

If one or more of the CRDs are missing, you might see errors in controller logs, failed job queuing,

`CrashLoopBackOff`

for the controller, or inability to admit or schedule workloads. In this case, you can manually reinstall the Kueue CRDs using the`kubectl apply`

command.`kubectl apply -f https://github.com/kubernetes-sigs/kueue/releases/latest/download/kueue-crds.yaml`

Note

Note that if you manually install the CRDs, you need to manually delete them once you're finished using the

`kubectl delete`

command.

### Question 3: What's the difference between a LocalQueue and a ClusterQueue

A ClusterQueue is a cluster-scoped resource that defines and governs a pool of compute resources like CPU, memory, pods, and accelerators across the entire Kubernetes cluster. A LocalQueue is a namespace-scoped resource that acts as a gateway for users to submit jobs within the defined Kubernetes cluster. This separation allows for fine-grained control over resource allocation and multi-tenant scheduling without exposing cluster-wide quotas directly to users.

How they work together:

- A user submits a job to a LocalQueue in their namespace.
- Kueue routes the job to the referenced ClusterQueue.
- The ClusterQueue checks resource availability and quota limits.
- If admitted, the job is unsuspended and scheduled.

## Next steps

In this article, you:

- Installed Kueue on your Azure Kubernetes Service (AKS) cluster using Helm and verified CRDs, controller health, and namespace setup.
- Configured
`ClusterQueue`

and`LocalQueue`

for general-purpose workloads with resource quotas and flavors (such as on-demand). - Submitted two batch jobs to demonstrate queuing: one admitted immediately, the second held due to quota limits, then admitted when resources became available.
- Monitored workload status and controller logs to confirm scheduling behavior and queuing logic.

To learn more about Kueue, visit the following resources:

[Multi-cluster scheduling and resource placement with Kueue and KubeFleet on AKS](https://blog.aks.azure.com/2025/04/02/Scaling-Kubernetes-for-AI-and-Data-intensive-Workloads).[Kueue developer tools](https://kueue.sigs.k8s.io/docs/tasks/dev/)official documentation.


---

<!-- DOCUMENTO FUSIONADO: workload-identity-migrate-from-pod-identity.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/workload-identity-migrate-from-pod-identity -->

# Migrate Azure Kubernetes Service (AKS) pods from pod-managed identity to Microsoft Entra Workload ID

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Migrate AKS pods from pod-managed identities to [Microsoft Entra Workload ID](workload-identity-overview) (workload identity) using one of three approaches based on your current [Azure Identity SDK](/en-us/entra/identity-platform/reference-v2-libraries) version: latest SDK parallel deployment, migration sidecar proxy (Linux only), or SDK rewrite.

## Prerequisites

- Azure CLI version 2.47.0 or later. Run the
`az --version`

command to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Set environment variables

The following table lists the environment variables used in the commands throughout this article. Make sure to replace the placeholder values with your own values.

| Environment variable | Description | Example value |
|---|---|---|
`SUBSCRIPTION_ID` |
The ID of the Azure subscription where the AKS cluster and managed identity are created. | `00000000-0000-0000-0000-000000000000` |
`RESOURCE_GROUP` |
The name of the resource group where the AKS cluster and managed identity are created. | `myResourceGroup` |
`LOCATION` |
The Azure region where the AKS cluster and managed identity are created. | `eastus` |
`CLUSTER_NAME` |
The name of the AKS cluster. | `myAKSCluster` |
`MANAGED_IDENTITY_NAME` |
The name of the user-assigned managed identity. | `myManagedIdentity` |
`SERVICE_ACCOUNT_NAME` |
The name of the Kubernetes service account to create or associate with the managed identity. | `workload-identity-sa` |
`SERVICE_ACCOUNT_NAMESPACE` |
The namespace of the Kubernetes service account. | `default` |
`FEDERATED_IDENTITY_NAME` |
The name of the federated identity credential to create. | `myFederatedIdentity` |

## Choose a migration path

Select the appropriate migration approach based on your current Azure Identity SDK version:

**Latest Azure Identity SDK**: If your application already uses the latest version of Azure Identity SDK, you can migrate by deploying Microsoft Entra Workload ID in parallel with existing pod-managed identity.**Older SDK with migration sidecar**- If your application uses an older SDK version and runs on Linux containers, you can use a temporary migration sidecar to proxy Instance Metadata Service (IMDS) transactions while planning your SDK upgrade.**Older SDK rewrite approach**: If your application uses an older SDK version, you can update your application code to use the latest Azure Identity SDK, then migrate to workload identity.

## Prepare for migration

For all migration paths, you need to have the federated trust set up before you update your application to use Microsoft Entra Workload ID. The following are the minimum steps required:

[Create a managed identity](#create-a-managed-identity)credential.- Associate the user-assigned managed identity with the Kubernetes service account already used for the pod-managed identity or
[create a new Kubernetes service account](#create-kubernetes-service-account)and then associate it with the managed identity. [Establish a federated trust relationship](#establish-federated-identity-credential-trust)between the managed identity and Microsoft Entra ID using the[OpenID Connect (OIDC)](/en-us/azure/active-directory/develop/v2-protocols-oidc)issuer URL and the service account.

## Migrate from latest version of Azure Identity SDK

**This migration path applies when** your application already uses the latest version of the Azure Identity SDK and you want to migrate with minimal code changes.

**Migration approach**: Deploy Microsoft Entra Workload ID in parallel with pod-managed identity, verify functionality, then remove pod-managed identity.

**Steps**:

- Deploy Microsoft Entra Workload ID in parallel with existing pod-managed identity.
- Restart your application deployment to begin using Microsoft Entra Workload ID (OIDC annotations are injected automatically).
- Verify the application can authenticate successfully using workload identity.
[Remove the pod-managed identity](#remove-pod-managed-identity)annotations from your application.- Remove the pod-managed identity add-on from your cluster.

## Use a migration sidecar (Linux containers only)

**This migration path applies when** your application uses an older version of the Azure Identity SDK, runs on Linux containers, and you need a temporary solution while planning SDK updates.

**Migration approach**: Deploy a migration sidecar that proxies IMDS transactions to OIDC, allowing your existing application code to work without immediate changes.

**Important limitations**:

**Linux containers only**. Windows containers aren't supported.**Temporary solution**that's not intended for long-term production use.**Planning required**to schedule SDK updates for long-term support.

**Steps**:

[Deploy the workload with migration sidecar](#deploy-the-workload-with-migration-sidecar)to proxy IMDS transactions.- Verify authentication transactions complete successfully.
- Schedule application SDK updates to supported Azure Identity versions.
- Once SDKs are updated, remove the proxy sidecar and redeploy applications.

## Rewrite application for latest Azure Identity SDK

**This migration path applies when** your application uses an older version of the Azure Identity SDK and you want to update to the latest supported SDK before migrating.

**Migration approach**: Update your application code to use the latest Azure Identity SDK, then migrate to Microsoft Entra Workload ID with the updated code.

**Technical outcomes**:

- Uses current Azure Identity SDK versions (no deprecation timeline).
- Supports both Linux and Windows containers (unlike sidecar approach).
- Eliminates proxy components and IMDS translation overhead.

**Steps**:

- Update your application code to use the latest
[Azure Identity SDK](workload-identity-overview#prerequisites). - Test the updated application with pod-managed identity.
- Restart your application deployment to begin authenticating using Microsoft Entra Workload ID (OIDC annotations are injected automatically).
- Verify authentication transactions complete successfully.
[Remove the pod-managed identity](#remove-pod-managed-identity)annotations and add-on.

## Set an active Azure subscription

Set a specific Azure subscription as the current active subscription using the

command.`az account set`

`az account set --subscription $SUBSCRIPTION_ID`


## Create a managed identity

Create a managed identity using the

command.`az identity create`

`az identity create --name $MANAGED_IDENTITY_NAME --resource-group $RESOURCE_GROUP --location $LOCATION --subscription $SUBSCRIPTION_ID`


## Get managed identity client ID

Get the client ID of the managed identity and save it to an environmental variable using the

command.`az identity show`

`export USER_ASSIGNED_CLIENT_ID="$(az identity show --resource-group $RESOURCE_GROUP --name $MANAGED_IDENTITY_NAME --query 'clientId' -otsv)"`


## Grant managed identity access to Azure resources

- Grant the managed identity the permissions needed to access the required Azure resources. Follow the steps in
[Assign a managed identity access to a resource](/en-us/azure/role-based-access-control/role-assignments-portal-managed-identity)to assign the appropriate role to the managed identity.

## Get OIDC issuer URL

Get the OIDC issuer URL and save it to an environmental variable using the

command.`az aks show`

`export AKS_OIDC_ISSUER="$(az aks show --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --query "oidcIssuerProfile.issuerUrl" -o tsv)"`

The variable should contain an issuer URL similar to the following example:

`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/`

By default, the issuer uses the base URL

`https://{region}.oic.prod-aks.azure.com/{uuid}`

, where the value for`{region}`

matches the location the AKS cluster is deployed in. The value`{uuid}`

represents the OIDC key.

## Get AKS cluster credentials

Get the AKS cluster credentials using the

command.`az aks get-credentials`

`az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP`


## Create Kubernetes service account

Create a Kubernetes service account and annotate it with the managed identity client ID using the

`kubectl apply`

command. Make sure to replace the placeholder values with your own values.`cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${USER_ASSIGNED_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`

The following output resembles successful creation of the identity:

`Serviceaccount/workload-identity-sa created`


## Establish federated identity credential trust

Create the federated identity credential between the managed identity, service account issuer, and subject using the

command.`az identity federated-credential create`

`az identity federated-credential create --name $FEDERATED_IDENTITY_NAME --identity-name $MANAGED_IDENTITY_NAME --resource-group $RESOURCE_GROUP --issuer ${AKS_OIDC_ISSUER} --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME} --audience api://AzureADTokenExchange`

The federated identity credential takes a few minutes to propagate after being added. If a token request is made immediately after adding the federated identity credential, the token request might fail because the Azure AD directory cache contains outdated information.


## Deploy the workload with migration sidecar

If your application uses user-assigned managed identity and still relies on IMDS to get an access token you can use the migration sidecar to start migrating to Microsoft Entra Workload ID. In long-term applications, you should modify the code to use the latest Azure Identity SDKs that support client assertion.

To update or deploy the workload, add the following [pod annotations](workload-identity-overview#pod-annotations) to your pod specification (only if you want to use the migration sidecar):

| Pod annotation | Description | Value |
|---|---|---|
`azure.workload.identity/inject-proxy-sidecar` |
Indicates whether to inject the proxy sidecar into the pod. | `true` or `false` |
`azure.workload.identity/proxy-sidecar-port` |
Desired port for the proxy sidecar. | Default value: `8000` |

When you create a pod with these annotations, the Microsoft Entra Workload ID mutating webhook automatically injects the `init-container`

and proxy sidecar to the pod spec. The following YAML shows an example of what the mutating webhook adds to the pod deployment:

```
apiVersion: v1
kind: Pod
metadata:
name: httpbin-pod
labels:
app: httpbin
azure.workload.identity/use: "true"
annotations:
azure.workload.identity/inject-proxy-sidecar: "true"
spec:
serviceAccountName: workload-identity-sa
initContainers:
- name: init-networking
image: mcr.microsoft.com/oss/azure/workload-identity/proxy-init:v1.1.0
securityContext:
capabilities:
add:
- NET_ADMIN
drop:
- ALL
privileged: true
runAsUser: 0
env:
- name: PROXY_PORT
value: "8000"
containers:
- name: nginx
image: nginx:alpine
ports:
- containerPort: 80
- name: proxy
image: mcr.microsoft.com/oss/azure/workload-identity/proxy:v1.1.0
ports:
- containerPort: 8000
```


## Verify the workload with migration sidecar

Verify the pod is in a running state using the

command. Replace`kubectl describe pod`

`<pod-name>`

with the name of your pod.`kubectl describe pods <pod-name>`

Verify the pod is passing IMDS transactions using the

command. Replace`kubectl logs`

`<pod-name>`

with the name of your pod.`kubectl logs <pod-name>`

The following example log output resembles successful communication through the proxy sidecar. Verify the logs show a token is successfully acquired and the

`GET`

operation is successful.`I0926 00:29:29.968723 1 proxy.go:97] proxy "msg"="starting the proxy server" "port"=8080 "userAgent"="azure-workload-identity/proxy/v0.13.0-12-gc8527f3 (linux/amd64) c8527f3/2022-09-26-00:19" I0926 00:29:29.972496 1 proxy.go:173] proxy "msg"="received readyz request" "method"="GET" "uri"="/readyz" I0926 00:29:30.936769 1 proxy.go:107] proxy "msg"="received token request" "method"="GET" "uri"="/metadata/identity/oauth2/token?resource=https://management.core.windows.net/api-version=2018-02-01&client_id=<client_id>" I0926 00:29:31.101998 1 proxy.go:129] proxy "msg"="successfully acquired token" "method"="GET" "uri"="/metadata/identity/oauth2/token?resource=https://management.core.windows.net/api-version=2018-02-01&client_id=<client_id>"`


## Remove pod-managed identity

After you complete your testing and the application can successfully get a token using the proxy sidecar, you can remove the identity and pod-managed identity mapping from your AKS cluster

Remove the pod-managed identity binding from your pod using the

command. Replace`az aks pod-identity delete`

`<pod-identity-name>`

and`<pod-identity-namespace>`

with the name and namespace of your pod identity.`az aks pod-identity delete --name <pod-identity-name> --namespace <pod-identity-namespace> --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME`


## Related content

For more information about Microsoft Entra Workload ID, see the [Overview](workload-identity-overview) article.
