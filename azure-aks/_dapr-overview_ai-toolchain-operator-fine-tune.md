---
merged_at: 2026-01-25T12:25:33.932734
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: dapr-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/dapr-overview -->

# Dapr extension for Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Distributed Application Runtime (Dapr)](https://docs.dapr.io/) offers APIs that help you write and implement simple, portable, resilient, and secured microservices. Dapr APIs run as a sidecar process in tandem with your applications and abstract away common complexities you may encounter when building distributed applications, such as:

- Service discovery
- Message broker integration
- Encryption
- Observability
- Secret management

Dapr is incrementally adoptable. You can use any of the API building blocks as needed. [Learn the support level Microsoft offers for the Dapr extension.](#issue-handling)

## Capabilities and features

[Using the Dapr extension to provision Dapr on your AKS or Arc-enabled Kubernetes cluster](dapr) eliminates the overhead of:

- Downloading Dapr tooling
- Manually installing and managing the Dapr runtime on your AKS cluster

Additionally, the extension offers support for all [native Dapr configuration capabilities](dapr-settings) through simple command-line arguments.

Dapr provides the following set of capabilities to help with your microservice development on AKS:

- Easy provisioning of Dapr on AKS through
[cluster extensions](cluster-extensions) - Portability enabled through HTTP and gRPC APIs which abstract underlying technologies choices
- Reliable, secure, and resilient service-to-service calls through HTTP and gRPC APIs
- Publish and subscribe messaging made easy with support for CloudEvent filtering and "at-least-once" semantics for message delivery
- Pluggable observability and monitoring through Open Telemetry API collector
- Independent of language, while also offering language specific software development kits (SDKs)
- Integration with Visual Studio Code through the Dapr extension
[More APIs for solving distributed application challenges](https://docs.dapr.io/concepts/building-blocks-concept/)

## Issue handling

Microsoft categorizes issues raised against the Dapr extension into two parts:

- Extension operations
- Dapr runtime (including APIs and components)

The following table breaks down support priority levels for each of these categories.

| Description | Security risks/Regressions | Functional issues | |
|---|---|---|---|
Extension operations |
Issues encountered during extension operations, such as installing/uninstalling or upgrading the Dapr extension. | Microsoft prioritizes for immediate resolution. | Microsoft investigates and addresses as needed. |
Dapr runtime |
Issues encountered when using the Dapr runtime, APIs, and components via the extension, like cert expiration and unexpected component behavior. |
|

[Discuss issues with the Dapr open source project](https://github.com/dapr/dapr/issues/new/choose)to resolve in a hotfix or future Dapr open source release. Known open source functional issues won't be investigated by Microsoft at this time.### Clouds/regions

Global Azure cloud is supported with AKS and Arc support on the following regions:

| Region | AKS support | Arc for Kubernetes support |
|---|---|---|
`australiaeast` |
✔️ | ✔️ |
`australiasoutheast` |
✔️ | ❌ |
`brazilsouth` |
✔️ | ❌ |
`canadacentral` |
✔️ | ✔️ |
`canadaeast` |
✔️ | ✔️ |
`centralindia` |
✔️ | ✔️ |
`centralus` |
✔️ | ✔️ |
`eastasia` |
✔️ | ✔️ |
`eastus` |
✔️ | ✔️ |
`eastus2` |
✔️ | ✔️ |
`eastus2euap` |
❌ | ✔️ |
`francecentral` |
✔️ | ✔️ |
`francesouth` |
✔️ | ❌ |
`germanywestcentral` |
✔️ | ✔️ |
`japaneast` |
✔️ | ✔️ |
`japanwest` |
✔️ | ❌ |
`koreacentral` |
✔️ | ✔️ |
`koreasouth` |
✔️ | ❌ |
`northcentralus` |
✔️ | ✔️ |
`northeurope` |
✔️ | ✔️ |
`norwayeast` |
✔️ | ❌ |
`southafricanorth` |
✔️ | ❌ |
`southcentralus` |
✔️ | ✔️ |
`southeastasia` |
✔️ | ✔️ |
`southindia` |
✔️ | ❌ |
`swedencentral` |
✔️ | ✔️ |
`switzerlandnorth` |
✔️ | ✔️ |
`uaenorth` |
✔️ | ❌ |
`uksouth` |
✔️ | ✔️ |
`ukwest` |
✔️ | ❌ |
`westcentralus` |
✔️ | ✔️ |
`westeurope` |
✔️ | ✔️ |
`westus` |
✔️ | ✔️ |
`westus2` |
✔️ | ✔️ |
`westus3` |
✔️ | ✔️ |

## Frequently asked questions

### How do Dapr and Service meshes compare?

While Dapr and service meshes do offer some overlapping capabilities, a service mesh is focused on networking concerns, whereas Dapr is focused on providing building blocks that make building applications as microservices easier. Dapr is developer-centric, while service meshes are infrastructure-centric.

Some common capabilities that Dapr shares with service meshes include:

- Secure service-to-service communication with mTLS encryption
- Service-to-service metric collection
- Service-to-service distributed tracing
- Resiliency through retries

Dapr provides other application-level building blocks for state management, pub/sub messaging, actors, and more. However, Dapr doesn't provide capabilities for traffic behavior, such as routing or traffic splitting. If your solution would benefit from the traffic splitting a service mesh provides, consider using [Open Service Mesh](open-service-mesh-about).

For more information on Dapr and service meshes, and how they can be used together, visit the [Dapr documentation](https://docs.dapr.io/).

### How does the Dapr secrets API compare to the Secrets Store CSI driver?

Both the Dapr secrets API and the managed Secrets Store CSI driver allow for the integration of secrets held in an external store, abstracting secret store technology from application code.

The Secrets Store CSI driver mounts secrets held in Azure Key Vault as a CSI volume for consumption by an application.

Dapr exposes secrets via a RESTful API that can be:

- Called by application code
- Configured with assorted secret stores

The following table lists the capabilities of each offering:

| Dapr secrets API | Secrets Store CSI driver | |
|---|---|---|
Supported secrets stores |
Local environment variables (for Development); Local file (for Development); Kubernetes Secrets; AWS Secrets Manager; Azure Key Vault secret store; Azure Key Vault with Managed Identities on Kubernetes; GCP Secret Manager; HashiCorp Vault | Azure Key Vault secret store |
Accessing secrets in application code |
Call the Dapr secrets API | Access the mounted volume or sync mounted content as a Kubernetes secret and set an environment variable |
Secret rotation |
New API calls obtain the updated secrets | Polls for secrets and updates the mount at a configurable interval |
Logging and metrics |
The Dapr sidecar generates logs, which can be configured with collectors such as Azure Monitor, emits metrics via Prometheus, and exposes an HTTP endpoint for health checks | Emits driver and Azure Key Vault provider metrics via Prometheus |

For more information on the secret management in Dapr, see the [secrets management overview](https://docs.dapr.io/developing-applications/building-blocks/secrets/secrets-overview/).

For more information on the Secrets Store CSI driver and Azure Key Vault provider, see the [Secrets Store CSI driver overview](csi-secrets-store-driver).

### How does the managed Dapr cluster extension compare to the open source Dapr offering?

The managed Dapr cluster extension is the easiest method to provision Dapr on an AKS cluster. With the extension, you're able to offload management of the Dapr runtime version by opting into automatic upgrades. Additionally, the extension installs Dapr with smart defaults (for example, provisioning the Dapr control plane in high availability mode).

When installing Dapr open source via helm or the Dapr CLI, developers and cluster maintainers are also responsible for runtime versions and configuration options.

Lastly, the Dapr extension is an extension of AKS, therefore you can expect the same support policy as other AKS features.

[Learn more about migrating from Dapr open source to the Dapr extension for AKS](dapr-migration).

### How can I authenticate Dapr components with Microsoft Entra ID using managed identities?

- Learn how
[Dapr components authenticate with Microsoft Entra ID](https://docs.dapr.io/developing-applications/integrations/azure/azure-authentication). - Learn about
[using managed identities with AKS](use-managed-identity).

### How can I switch to using the Dapr extension if I've already installed Dapr via a method, such as Helm?

Recommended guidance is to completely uninstall Dapr from the AKS cluster and reinstall it via the cluster extension. [You can also check for the existing Dapr installation and migrate it to AKS.](dapr-migration)

If you install Dapr through the AKS extension, our recommendation is to continue using the extension for future management of Dapr instead of the Dapr CLI. Combining the two tools can cause conflicts and result in undesired behavior.


---

<!-- DOCUMENTO FUSIONADO: ai-toolchain-operator-fine-tune.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-fine-tune -->

# Fine-tune and deploy an AI model for inferencing on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to fine-tune and deploy a language model inferencing workload on AKS with the AI toolchain operator add-on. You learn how to accomplish the following tasks:

[Set environment variables](#export-environmental-variables)to reference your Azure Container Registry (ACR) and repository details.[Create your container registry image push/pull secret](#create-a-new-secret-for-your-private-registry)to store and retrieve private fine-tuning adapter images.[Select a supported model and fine-tune it to your data](#fine-tune-an-ai-model).[Test the inference service endpoint](#test-the-model-inference-service-endpoint).[Clean up resources](#clean-up-resources).

The AI toolchain operator (KAITO) is a managed add-on for AKS that simplifies the deployment and operations for AI models on your AKS clusters. Starting with [KAITO version 0.3.1](https://github.com/kaito-project/kaito/releases/tag/v0.3.1) and above, you can use the AKS managed add-on to fine-tune supported foundation models with new data and enhance the accuracy of your AI models. To learn more about parameter efficient fine-tuning methods and their use cases, see [Concepts - Fine-tuning language models for AI and machine learning workflows on AKS](concepts-fine-tune-language-models).

## Before you begin

- This article assumes you have an existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Azure CLI version 2.47.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Prerequisites

- The Kubernetes command-line client, kubectl, installed and configured. For more information, see
[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - Configure
[Azure Container Registry (ACR) integration](aks-extension-attach-azure-container-registry)of a new or existing ACR with your AKS cluster. - Install the
[AI toolchain operator add-on](ai-toolchain-operator)on your AKS cluster. - If you already have the AI toolchain operator add-on installed, update your AKS cluster to the latest version to run KAITO v0.3.1+ and ensure that the AI toolchain operator add-on feature flag is enabled.

## Export environmental variables

To simplify the configuration steps in this article, you can define environment variables using the following commands. Make sure to replace the placeholder values with your own.

```
ACR_NAME="myACRname"
ACR_USERNAME="myACRusername"
REPOSITORY="myRepository"
VERSION="repositoryVersion'
ACR_PASSWORD=$(az acr token create --name $ACR_USERNAME --registry $ACR_NAME --expiration-in-days 10 --repository $REPOSITORY content/write content/read --query "credentials.passwords[0].value" --output tsv)
```


## Create a new secret for your private registry

In this example, your KAITO fine-tuning deployment produces a containerized adapter output, and the KAITO workspace requires a new push secret as authorization to push the adapter image to your ACR.

Generate a new secret to provide the KAITO fine-tuning workspace access to push the model fine-tuning output image to your ACR using the `kubectl create secret docker-registry`

command.

```
kubectl create secret docker-registry myregistrysecret --docker-server=$ACR_NAME.azurecr.io --docker-username=$ACR_USERNAME --docker-password=$ACR_PASSWORD
```


## Fine-tune an AI model

In this example, you fine-tune the [Phi-3-mini small language model](https://huggingface.co/docs/transformers/main/en/model_doc/phi3) using the qLoRA tuning method by applying the following Phi-3-mini KAITO fine-tuning workspace CRD:

```
apiVersion: kaito.sh/v1alpha1
kind: Workspace
metadata:
name: workspace-tuning-phi-3-mini
resource:
instanceType: "Standard_NC24ads_A100_v4"
labelSelector:
matchLabels:
apps: tuning-phi-3-mini-pycoder
tuning:
preset:
name: phi3mini128kinst
method: qlora
input:
urls:
- “myDatasetURL”
output:
image: “$ACR_NAME.azurecr.io/$REPOSITORY:$VERSION”
imagePushSecret: myregistrysecret
```


This example uses a public dataset specified by a URL in the input. If choosing an image as the source of your fine-tuning data, please refer to the [KAITO fine-tuning API](https://github.com/kaito-project/kaito/tree/main) specification to adjust the input to pull an image from your ACR.

Note

The choice of GPU SKU is critical since model fine-tuning normally requires more GPU memory compared to model inference. To avoid GPU Out-Of-Memory errors, we recommend using NVIDIA A100 or higher tier GPUs.

Apply the KAITO fine-tuning workspace CRD using the

`kubectl apply`

command.`kubectl apply workspace-tuning-phi-3-mini.yaml`

Track the readiness of your GPU resources, fine-tuning job, and workspace using the

`kubectl get workspace`

command.`kubectl get workspace -w`

Your output should look similar to the following example output:

`NAME INSTANCE RESOURCE READY INFERENCE READY JOB STARTED WORKSPACE SUCCEEDED AGE workspace-tuning-phi-3-mini Standard_NC24ads_A100_v4 True True 3m 45s`

Check the status of your fine-tuning job pods using the

`kubectl get pods`

command.`kubectl get pods`


Note

You can store the adapter to your specific output location as a container image or any storage type supported by Kubernetes.

## Deploy the fine-tuned model for inferencing

Now, you use the Phi-3-mini adapter image created in the previous section for a new inferencing deployment with this model.

The KAITO inference workspace CRD below consists of the following resources and adapter(s) to deploy on your AKS cluster:

```
apiVersion: kaito.sh/v1alpha1
kind: Workspace
metadata:
name: workspace-phi-3-mini-adapter
resource:
instanceType: "Standard_NC6s_v3"
labelSelector:
matchLabels:
apps: phi-3-adapter
inference:
preset:
name: “phi-3-mini-128k-instruct“
adapters:
-source:
name: kubernetes-adapter
image: $ACR_NAME.azurecr.io/$REPOSITORY:$VERSION
imagePullSecrets:
- myregistrysecret
strength: “1.0”
```


Note

Optionally, you can pull in several adapters created from fine-tuning deployments with the same model on different data sets by defining additional "source" fields. Inference with different adapters to compare the performance of your fine-tuned model in varying contexts.

Apply the KAITO inference workspace CRD using the

`kubectl apply`

command.`kubectl apply -f workspace-phi-3-mini-adapter.yaml`

Track the readiness of your GPU resources, inference server, and workspace using the

`kubectl get workspace`

command.`kubectl get workspace -w`

Your output should look similar to the following example output:

`NAME INSTANCE RESOURCE READY INFERENCE READY JOB STARTED WORKSPACE SUCCEEDED AGE workspace-phi-3-mini-adapter Standard_NC6s_v3 True True True 5m 47s`

Check the status of your inferencing workload pods using the

`kubectl get pods`

command.`kubectl get pods`

It might take several minutes for your pods to show the

`Running`

status.

## Test the model inference service endpoint

Check your model inferencing service and retrieve the service IP address using the

`kubectl get svc`

command.`export SERVICE_IP=$(kubectl get svc workspace-phi-3-mini-adapter -o jsonpath=’{.spec.clusterIP}’)`

Run your fine-tuned Phi-3-mini model with a sample input of your choice using the

`kubectl run`

command. The following example asks the generative AI model,*"What is AKS?"*:`kubectl run -it --rm --restart=Never curl --image=curlimages/curl -- curl -X POST http://$SERVICE_IP/chat -H "accept: application/json" -H "Content-Type: application/json" -d "{\"prompt\":\"What is AKS?\"}"`

Your output might look similar to the following example output:

`"Kubernetes on Azure" is the official name. https://learn.microsoft.com/en-us/azure/aks/ ...`


## Clean up resources

If you no longer need these resources, you can delete them to avoid incurring extra Azure charges. To calculate the estimated cost of your resources, you can use the [Azure pricing calculator](https://azure.microsoft.com/pricing/calculator/?service=kubernetes-service).

Delete the KAITO workspaces and their allocated resources on your AKS cluster using the `kubectl delete workspace`

command.

```
kubectl delete workspace workspace-tuning-phi-3-mini
kubectl delete workspace workspace-phi-3-mini-adapter
```


## Next steps

- Learn more about fine-tuning language models with KAITO in this
[AKS Engineering Blog](https://blog.aks.azure.com/2024/08/23/fine-tuning-language-models-with-kaito)! - Explore
[MLOps for AI and machine learning workflows](concepts-machine-learning-ops)and best practices on AKS - Learn about supported families of
[GPUs on Azure Kubernetes Service](gpu-cluster)
