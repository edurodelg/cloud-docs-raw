---
merged_at: 2026-01-25T12:25:33.901405
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: kaito-custom-inference-model.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kaito-custom-inference-model -->

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

<!-- DOCUMENTO FUSIONADO: resize-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/resize-cluster -->

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
