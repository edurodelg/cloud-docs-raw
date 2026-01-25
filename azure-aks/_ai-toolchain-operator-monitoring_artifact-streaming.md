---
merged_at: 2026-01-25T12:25:33.915349
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: ai-toolchain-operator-monitoring.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-monitoring -->

# Monitor and visualize AI inference metrics on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Monitoring and observability play a key role in maintaining high performance and low cost of your AI workload deployments in Azure Kubernetes Service (AKS). Visibility into system and performance metrics can indicate the limits of your underlying infrastructure and motivate real-time adjustments and optimizations to reduce workload interruptions. Monitoring also provides valuable insights into resource utilization for cost-effective management of computational resources and accurate provisioning.

The Kubernetes AI Toolchain Operator (KAITO) is a managed add-on for AKS that simplifies deployment and operations for AI models in your AKS cluster.

In [KAITO version 0.4.4](https://github.com/kaito-project/kaito/releases/tag/v0.4.4) and later versions, the vLLM inference runtime is enabled by default in the AKS managed add-on. [vLLM](https://docs.vllm.ai/en/latest/) is a library for language model inference and serving. It surfaces key system performance, resource usage, and request processing for [Prometheus metrics](https://docs.vllm.ai/en/latest/design/v1/metrics.html) that you can use to evaluate your KAITO inference deployments.

In this article, you'll learn how to monitor and visualize vLLM inference metrics using the AI toolchain operator add-on with Azure Managed Prometheus and Azure Managed Grafana on your AKS cluster.

## Before you begin

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Install and configure Azure CLI version 2.47.0 or later. To find your version, run
`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli).

## Prerequisites

- Install and configure kubectl, the Kubernetes command-line client. For more information, see
[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - Enable the
[AI toolchain operator add-on](ai-toolchain-operator)in your AKS cluster. - If you already have the AI toolchain operator add-on enabled, update your AKS cluster to the latest version to run KAITO v0.4.4 or later.
- Enable
[the managed service for Prometheus and Azure Managed Grafana](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable)in your AKS cluster. - Have permissions to
[create or update Azure Managed Grafana instances](/en-us/azure/managed-grafana/how-to-manage-access-permissions-users-identities)in your Azure subscription.

## Deploy a KAITO inference service

In this example, you collect metrics for the [Qwen-2.5-coder-7B-instruct language model](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml).

Start by applying the following KAITO workspace custom resource to your cluster:

`kubectl apply -f https://raw.githubusercontent.com/Azure/kaito/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml`

Track the live resource changes in your KAITO workspace:

`kubectl get workspace workspace-qwen-2-5-coder-7b-instruct -w`

Note

Machine readiness can take up to 10 minutes, and workspace readiness can take up to 20 minutes depending on the size of your language model.

Confirm that your inference service is running and get the service IP address:

`export SERVICE_IP=$(kubectl get svc workspace-qwen-2-5-coder-7b-instruct -o jsonpath='{.spec.clusterIP}') echo $SERVICE_IP`


## Surface KAITO inference metrics to the managed service for Prometheus

Prometheus metrics are collected by default at the KAITO [ /metrics endpoint](https://github.com/kaito-project/kaito/tree/main).

Add the following label to your KAITO inference service so that a Kubernetes

`ServiceMonitor`

deployment can detect it:`kubectl label svc workspace-qwen-2-5-coder-7b-instruct App=qwen-2-5-coder`

Create a

`ServiceMonitor`

resource to define the inference service endpoints and the required configurations to scrape the vLLM Prometheus metrics. Export these metrics to the managed service for Prometheus by deploying the following`ServiceMonitor`

YAML manifest in the`kube-system`

namespace:`cat <<EOF | kubectl apply -n kube-system -f - apiVersion: azmonitoring.coreos.com/v1 kind: ServiceMonitor metadata: name: prometheus-kaito-monitor spec: selector: matchLabels: App: qwen-2-5-coder endpoints: - port: http interval: 30s path: /metrics scheme: http EOF`

Check for the following output to verify that

`ServiceMonitor`

is created:`servicemonitor.azmonitoring.coreos.com/prometheus-kaito-monitor created`

Verify that your

`ServiceMonitor`

deployment is running successfully:`kubectl get servicemonitor prometheus-kaito-monitor -n kube-system`

In the Azure portal, verify that vLLM metrics are successfully collected in the managed service for Prometheus.

In your Azure Monitor workspace, go to

**Managed Prometheus**>**Prometheus explorer**.Select the

**Grid**tab and confirm that a metrics item is associated with the job named`workspace-qwen-2-5-coder-7b-instruct`

.Note

The

`up`

value of this item should be`1`

. A value of`1`

indicates that Prometheus metrics are successfully being scraped from your AI inference service endpoint.


## Visualize KAITO inference metrics in Azure Managed Grafana

The vLLM project provides a Grafana dashboard configuration named

[grafana.json](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)for inference workload monitoring. Navigate to the bottom of this[page](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)and copy the entire contents of the`grafana.json`

file.Go to the bottom of the

[examples page](https://docs.vllm.ai/en/stable/examples/online_serving/prometheus_grafana.html#example-materials)and copy the entire contents of the`grafana.json`

file:Complete the steps to

[import the Grafana configurations into a new dashboard](/en-us/azure/managed-grafana/how-to-create-dashboard#import-a-json-dashboard)in Azure Managed Grafana.Go to your Managed Grafana endpoint, view the available dashboards, and select the

**vLLM**dashboard.To begin collecting data for your selected model deployment, confirm that the

**datasource**value shown at the top left of the Grafana dashboard is your instance of the managed service for Prometheus you created for this example.Copy the inference preset name defined in your KAITO workspace to the

**model_name**field in the Grafana dashboard. In this example, the model name is[qwen2.5-coder-7b-instruct](https://github.com/kaito-project/kaito/blob/main/examples/inference/kaito_workspace_qwen_2.5_coder_7b-instruct.yaml).In a few moments, verify that the metrics for your KAITO inference service appear in the vLLM Grafana dashboard.

Note

The value of these inference metrics remains

**0**until the requests are submitted to the model inference server.

## Related content

[Monitor and visualize](monitor-aks)your AKS deployments at scale.- Test and monitor
[tool calling with KAITO inference](ai-toolchain-operator-tool-calling)on your cluster. [Fine-tune an AI model](ai-toolchain-operator-fine-tune)by using the AI toolchain operator add-on in AKS.- Learn about AKS GPU workload deployment options on
[Linux](gpu-cluster)and[Windows](use-windows-gpu)nodes.


---

<!-- DOCUMENTO FUSIONADO: artifact-streaming.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/artifact-streaming -->

# Reduce image pull time with Artifact Streaming on Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

High performance compute workloads often involve large images, which can cause long image pull times and slow down your workload deployments. Artifact Streaming on AKS allows you to stream container images from Azure Container Registry (ACR) to AKS. AKS only pulls the necessary layers for initial pod startup, reducing the time it takes to pull images and deploy your workloads.

Artifact Streaming can reduce time to pod readiness by over 15%, depending on the size of the image, and it works best for images <30GB. Based on our testing, we saw reductions in pod start-up times for images <10GB from minutes to seconds. If you have a pod that needs access to a large file (>30GB), then you should mount it as a volume instead of building it as a layer. This is because if your pod requires that file to start, it congests the node. Artifact Streaming isn't ideal for read heavy images from your filesystem if you need that on startup. With Artifact Streaming, pod start-up becomes concurrent, whereas without it, pods start in serial.

This article describes how to enable the Artifact Streaming feature on your AKS node pools to stream artifacts from ACR.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

Important

Artifact Streaming (preview) is a suggested alternative for customers previously using Teleport (preview).
[Teleport (preview)](https://github.com/Azure/acr/blob/main/docs/teleport/aks-getting-started.md) on AKS will be retired on 15 July 2025. Please migrate to Artifact Streaming (preview) on AKS or update your node pools to set `--aks-custom-headers EnableACRTeleport=false`

.
Azure Container Registry removed the Teleport API, meaning that any nodes with Teleport enabled will pull images from Azure Container Registry like any other AKS node without Teleport.
After 15 July 2025, AKS node pools with Teleport enabled might experience breakage and node provisioning failures. For more information, see [aka.ms/aks/teleport-retirement](https://aka.ms/aks/teleport-retirement).

## Limitations

- Artifact Steaming isn't supported for the following OS options:
[Windows Server versions](windows-best-practices),[Flatcar Container Linux for AKS](flatcar-container-linux-for-aks), and[Azure Linux with OS Guard for AKS](use-azure-linux-os-guard).

## Prerequisites

- You need an existing AKS cluster with ACR integration. If you don't have one, you can create one using
[Authenticate with ACR from AKS](cluster-container-registry-integration). [Enable Artifact Streaming on ACR](#enable-artifact-streaming-on-acr).- This feature requires Kubernetes version 1.25 or later. To check your AKS cluster version, see
[Check for available AKS cluster upgrades](upgrade-cluster).

Note

Artifact Streaming is only supported on Ubuntu 22.04, Ubuntu 20.04, and Azure Linux node pools. Windows node pools aren't supported.

## Install the `aks-preview`

CLI extension

Install the

`aks-preview`

CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update the extension to ensure you have the latest version installed using the

command.`az extension update`

`az extension update --name aks-preview`


## Register the `ArtifactStreamingPreview`

feature flag in your subscription

Register the

`ArtifactStreamingPreview`

feature flag in your subscription using thecommand.`az feature register`

`az feature register --namespace Microsoft.ContainerService --name ArtifactStreamingPreview`


## Enable Artifact Streaming on ACR

Enablement on ACR is a prerequisite for Artifact Streaming on AKS. For more information, see [Artifact Streaming on ACR](https://aka.ms/acr/artifact-streaming).

Create an Azure resource group to hold your ACR instance using the

command.`az group create`

`az group create --name myStreamingTest --location westus`

Create a new premium SKU Azure Container Registry using the

command with the`az acr create`

`--sku Premium`

flag.`az acr create --resource-group myStreamingTest --name mystreamingtest --sku Premium`

Configure the default ACR instance for your subscription using the

command.`az configure`

`az configure --defaults acr="mystreamingtest"`

Push or import an image to the registry using the

command.`az acr import`

`az acr import --source docker.io/jupyter/all-spark-notebook:latest --repository jupyter/all-spark-notebook:latest`

Create a streaming artifact from the image using the

command.`az acr artifact-streaming create`

`az acr artifact-streaming create --image jupyter/all-spark-notebook:latest`

Verify the generated Artifact Streaming using the

command.`az acr manifest list-referrers`

`az acr manifest list-referrers --name jupyter/all-spark-notebook:latest`


## Enable Artifact Streaming on AKS

### Enable Artifact Streaming on a new node pool

Create a new node pool with Artifact Streaming enabled using the

command with the`az aks nodepool add`

`--enable-artifact-streaming`

.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myNodePool \ --enable-artifact-streaming`


### Enable Artifact Streaming on an existing node pool

Update an existing node pool to enable Artifact Streaming using the

command with the`az aks nodepool update`

`--enable-artifact-streaming`

.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name myNodePool \ --enable-artifact-streaming`


## Check if Artifact Streaming is enabled

Now that you enabled Artifact Streaming on a premium ACR and connected that to an AKS node pool with Artifact Streaming enabled, any new pod deployments on this cluster with an image pull from the ACR with Artifact Streaming enabled will see reductions in image pull times.

Check if your node pool has Artifact Streaming enabled using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --name myNodePool --query artifactStreamingProfile`

In the output, check that the

`Enabled`

field is set to`true`

.

## Next steps

This article described how to enable Artifact Streaming on your AKS node pools to stream artifacts from ACR and reduce image pull time. To learn more about working with container images in AKS, see [Best practices for container image management and security in AKS](operator-best-practices-container-image-management).
