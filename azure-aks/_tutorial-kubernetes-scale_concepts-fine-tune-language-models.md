---
merged_at: 2026-01-25T12:25:33.889431
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-scale.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-scale -->

# Tutorial - Scale applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you followed the previous tutorials, you have a working Kubernetes cluster and Azure Store Front app.

In this tutorial, you scale out the pods in the app, try pod autoscaling, and scale the number of Azure VM nodes to change the cluster's capacity for hosting workloads. You learn how to:

- Scale the Kubernetes nodes.
- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created an AKS cluster, deployed an application, and used Azure Service Bus to redeploy an updated application. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Manually scale pods

View the pods in your cluster using the

command.`kubectl get`

`kubectl get pods`

The following example output shows the pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE order-service-848767080-tf34m 1/1 Running 0 31m product-service-4019737227-2q2qz 1/1 Running 0 31m store-front-2606967446-2q2qz 1/1 Running 0 31m`

Manually change the number of pods in the

*store-front*deployment using thecommand.`kubectl scale`

`kubectl scale --replicas=5 deployment.apps/store-front`

Verify the additional pods were created using the

command.`kubectl get pods`

`kubectl get pods --selector app=store-front`

The following example output shows the additional pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE store-front-3309479140-2hfh0 1/1 Running 0 3m store-front-3309479140-bzt05 1/1 Running 0 3m store-front-3309479140-fvcvm 1/1 Running 0 3m store-front-3309479140-hrbf2 1/1 Running 0 15m store-front-3309479140-qphz8 1/1 Running 0 3m`


## Autoscale pods

To use the horizontal pod autoscaler, all containers must have defined CPU requests and limits, and pods must have specified requests. In the `aks-store-quickstart`

deployment, the *front-end* container requests 1m CPU with a limit of 1000m CPU.

These resource requests and limits are defined for each container, as shown in the following condensed example YAML:

```
...
containers:
- name: store-front
image: ghcr.io/azure-samples/aks-store-demo/store-front:latest
ports:
- containerPort: 8080
name: store-front
...
resources:
requests:
cpu: 1m
...
limits:
cpu: 1000m
...
```


### Autoscale pods using a manifest file

Create a manifest file to define the autoscaler behavior and resource limits, as shown in the following condensed example manifest file

`aks-store-quickstart-hpa.yaml`

:`apiVersion: autoscaling/v2 kind: HorizontalPodAutoscaler metadata: name: store-front-hpa spec: maxReplicas: 10 # define max replica count minReplicas: 3 # define min replica count scaleTargetRef: apiVersion: apps/v1 kind: Deployment name: store-front metrics: - type: Resource resource: name: cpu target: type: Utilization averageUtilization: 50`

Apply the autoscaler manifest file using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart-hpa.yaml`

Check the status of the autoscaler using the

`kubectl get hpa`

command.`kubectl get hpa`

After a few minutes, with minimal load on the Azure Store Front app, the number of pod replicas decreases to three. You can use

`kubectl get pods`

command again to see the unneeded pods being removed.

Note

You can enable the Kubernetes-based Event-Driven Autoscaler (KEDA) AKS add-on to your cluster to drive scaling based on the number of events needing to be processed. For more information, see [Enable simplified application autoscaling with the Kubernetes Event-Driven Autoscaling (KEDA) add-on (Preview)](keda-about).

## Manually scale AKS nodes

If you created your Kubernetes cluster using the commands in the previous tutorials, your cluster has two nodes. If you want to increase or decrease this amount, you can manually adjust the number of nodes.

The following example increases the number of nodes to three in the Kubernetes cluster named *myAKSCluster*. The command takes a couple of minutes to complete.

Scale your cluster nodes using the

command.`az aks scale`

`az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 3`

Once the cluster successfully scales, your output will be similar to following example output:

`"aadProfile": null, "addonProfiles": null, "agentPoolProfiles": [ { ... "count": 3, "mode": "System", "name": "nodepool1", "osDiskSizeGb": 128, "osDiskType": "Managed", "osType": "Linux", "ports": null, "vmSize": "Standard_DS2_v2", "vnetSubnetId": null ... } ... ]`


You can also autoscale the nodes in your cluster. For more information, see [Use the cluster autoscaler with node pools](cluster-autoscaler#use-the-cluster-autoscaler-on-node-pools).

## Next steps

In this tutorial, you used different scaling features in your Kubernetes cluster. You learned how to:

- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.
- Manually scale the Kubernetes nodes.

In the next tutorial, you learn how to upgrade Kubernetes in your AKS cluster.


---

<!-- DOCUMENTO FUSIONADO: concepts-fine-tune-language-models.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/concepts-fine-tune-language-models -->

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
