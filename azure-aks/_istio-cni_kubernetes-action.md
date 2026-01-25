---
merged_at: 2026-01-25T12:25:33.924897
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: istio-cni.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-cni -->

# Enable Istio CNI for Istio-based service mesh add-on for Azure Kubernetes Service (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to enable Istio CNI for the Istio-based service mesh add-on on Azure Kubernetes Service (AKS). Istio CNI improves security by eliminating the need for privileged network capabilities in application workloads within the service mesh.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Overview

By default, Istio service mesh uses privileged init containers (`istio-init`

) in each application pod to configure network traffic redirection to the Envoy sidecar proxy. These init containers require `NET_ADMIN`

and `NET_RAW`

capabilities, which are often flagged as security concerns in enterprise environments.

Istio CNI addresses this security concern by moving the network configuration responsibilities from individual pod init containers to a cluster-level CNI plugin. This approach:

**Improves security**: Removes the need for privileged network capabilities (`NET_ADMIN`

,`NET_RAW`

) from application workloads**Simplifies pod security policies**: Application pods only require minimal capabilities**Maintains functionality**: Provides the same traffic management capabilities as the traditional init container approach

When Istio CNI is enabled, application pods use a minimal `istio-validation`

init container that drops all capabilities instead of the privileged `istio-init`

container.

Note

Istio CNI is **not** a replacement for [Azure CNI](concepts-network-cni-overview) and will not interfere with your normal AKS networking. It is a separate plugin designed to handle Istio’s traffic redirection setup at the node level, improving security by removing the need for privileged init containers in application pods.

## Before you begin

Install the Azure CLI version 2.77.0 or later. You can run

`az --version`

to verify the version. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).Install the

`aks-preview`

Azure CLI extension version 19.0.0b5 or later:`az extension add --name aks-preview`

If you already have the

`aks-preview`

extension, update it to the latest version:`az extension update --name aks-preview`

Register the

`IstioCNIPreview`

feature flag on your Azure subscription:`az feature register --namespace "Microsoft.ContainerService" --name "IstioCNIPreview"`

Use the following command to check the registration status:

`az feature show --namespace "Microsoft.ContainerService" --name "IstioCNIPreview"`

It takes a few minutes for the feature to register. Verify the registration state shows

`Registered`

:`{ "id": "/subscriptions/xxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/providers/Microsoft.Features/providers/Microsoft.ContainerService/features/IstioCNIPreview", "name": "Microsoft.ContainerService/IstioCNIPreview", "properties": { "state": "Registered" }, "type": "Microsoft.Features/providers/features" }`

You need an AKS cluster with the Istio-based service mesh add-on enabled. If you don't have this setup, see

[Deploy Istio-based service mesh add-on for Azure Kubernetes Service](istio-deploy-addon).Ensure your Istio service mesh is using revision

`asm-1-25`

or later. You can check the current revision with:`az aks show --resource-group <resource-group-name> --name <cluster-name> --query 'serviceMeshProfile.istio.revisions'`


Note

Istio CNI is not compatible with Ubuntu 20.04 node pools. Ensure your cluster uses Ubuntu 22.04 or Azure Linux node pools.

### Set environment variables

```
export CLUSTER=<cluster-name>
export RESOURCE_GROUP=<resource-group-name>
```


## Enable Istio CNI

Use the following command to enable Istio CNI on your AKS cluster:

```
az aks mesh enable-istio-cni --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


## Verify Istio CNI is enabled

Use `az aks get-credentials`

to get the credentials for your AKS cluster:

```
az aks get-credentials --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


After enabling Istio CNI, verify the installation by checking that the CNI DaemonSet is running:

```
kubectl get daemonset -n aks-istio-system
```


You should see the Istio CNI DaemonSet running:

```
NAME DESIRED CURRENT READY UP-TO-DATE AVAILABLE NODE SELECTOR AGE
azure-service-mesh-istio-cni-addon-node 3 3 3 3 3 kubernetes.io/os=linux 94s
```


## Deploy workloads and verify behavior

To verify the security improvement, you can deploy the bookinfo sample application and check that workloads use the secure `istio-validation`

init container instead of the privileged `istio-init`

container.

### Deploy sample application

First, enable sidecar injection for the default namespace:

```
# Get the current Istio revision
REVISION=$(az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.istio.revisions[0]' -o tsv)
# Label the namespace for sidecar injection
kubectl label namespace default istio.io/rev=${REVISION}
```


Deploy the bookinfo sample application:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.25/samples/bookinfo/platform/kube/bookinfo.yaml
```


### Verify secure init container usage

Check that the deployed pods use the secure `istio-validation`

init container instead of `istio-init`

:

```
kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.initContainers[0].name}{"\t"}{.spec.initContainers[0].securityContext.capabilities}{"\n"}{end}'
```


Expected output should show `istio-validation`

as the init container with dropped capabilities:

```
details-v1-799dc5d847-7x9gl istio-validation {"drop":["ALL"]}
productpage-v1-99d6d698f-89gpj istio-validation {"drop":["ALL"]}
ratings-v1-7545c4bb6c-m7t42 istio-validation {"drop":["ALL"]}
reviews-v1-8679d76d6c-jz4vg istio-validation {"drop":["ALL"]}
reviews-v2-5b9c77895c-b2b7m istio-validation {"drop":["ALL"]}
reviews-v3-5b57874f5f-kk9rt istio-validation {"drop":["ALL"]}
```


You can also describe a specific pod to verify the security context:

```
kubectl describe pod <pod-name> | grep -A 10 -B 5 "istio-validation"
```


The output should show that the `istio-validation`

init container has no privileged capabilities:

```
Init Containers:
istio-validation:
Container ID: containerd://...
Image: mcr.microsoft.com/oss/istio/proxyv2:...
...
Security Context:
capabilities:
drop:
- ALL
runAsGroup: 1337
runAsNonRoot: true
runAsUser: 1337
```


## Disable Istio CNI

To disable Istio CNI and return to using traditional init containers, use the following command:

```
az aks mesh disable-istio-cni --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


After disabling Istio CNI:

The CNI DaemonSet will be removed:

`kubectl get daemonset azure-service-mesh-istio-cni-addon-node -n aks-istio-system`

Expected output (no CNI DaemonSet):

`Error from server (NotFound): daemonsets.apps "azure-service-mesh-istio-cni-addon-node" not found`

New workloads will use the traditional

`istio-init`

init container with network capabilities. Restart all existing deployments to pick up the change:`kubectl rollout restart deployment/details-v1 kubectl rollout restart deployment/productpage-v1 kubectl rollout restart deployment/ratings-v1 kubectl rollout restart deployment/reviews-v1 kubectl rollout restart deployment/reviews-v2 kubectl rollout restart deployment/reviews-v3`

Verify init container name and capabilities:

`kubectl get pods -o jsonpath='{range .items[*]}{.metadata.name}{"\t"}{.spec.initContainers[0].name}{"\t"}{.spec.initContainers[0].securityContext.capabilities}{"\n"}{end}'`

Expected output should show

`istio-init`

with network capabilities:`details-v1-57bc58c559-722v8 istio-init {"drop":["ALL"]} productpage-v1-7bb64f657c-jw6gs istio-init {"drop":["ALL"]} ratings-v1-57d5594c75-4zd49 istio-init {"drop":["ALL"]} reviews-v1-7fd8f9cd59-mdcf9 istio-init {"drop":["ALL"]} reviews-v2-7b8bdc9cdf-k9qgb istio-init {"drop":["ALL"]} reviews-v3-588854d9d7-s2f7j istio-init {"drop":["ALL"]}`


---

<!-- DOCUMENTO FUSIONADO: kubernetes-action.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kubernetes-action -->

# Build, test, and deploy containers to Azure Kubernetes Service (AKS) using GitHub Actions

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[GitHub Actions](https://docs.github.com/en/actions) gives you the flexibility to build an automated software development lifecycle workflow. You can use multiple Kubernetes actions to deploy to containers from Azure Container Registry (ACR) to Azure Kubernetes Service (AKS) with GitHub Actions.

## Prerequisites

- An Azure account with an active subscription. If you don't have one,
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - A GitHub account. If you don't have one,
[sign up for free](https://github.com/join).- When using GitHub Actions, you need to configure the integration between Azure and your GitHub repository. To configure the integration, see
[Use GitHub Actions to connect to Azure](/en-us/azure/developer/github/connect-from-azure?tabs=azure-cli%2Clinux).

- When using GitHub Actions, you need to configure the integration between Azure and your GitHub repository. To configure the integration, see
- An existing AKS cluster with an attached ACR. If you don't have one, see
[Authenticate with ACR from AKS](cluster-container-registry-integration).

## GitHub Actions for AKS

With GiHub Actions, you can automate your software development workflows from within GitHub. For more information, see [GitHub Actions for Azure](/en-us/azure/developer/github/github-actions).

The following table lists the available actions for AKS:

| Name | Description | More details |
|---|---|---|
`azure/aks-set-context` |
Set the target AKS cluster context for other actions to use or run any kubectl commands. |
|

`azure/k8s-set-context`

[azure/k8s-set-context](https://github.com/Azure/k8s-set-context)`azure/k8s-bake`

[azure/k8s-bake](https://github.com/Azure/k8s-bake)`azure/k8s-create-secret`

[azure/k8s-create-secret](https://github.com/Azure/k8s-create-secret)`azure/k8s-deploy`

[azure/k8s-deploy](https://github.com/Azure/k8s-deploy)`azure/k8s-lint`

[azure/k8s-lint](https://github.com/Azure/k8s-lint)`azure/setup-helm`

[azure/setup-helm](https://github.com/Azure/setup-helm)`azure/setup-kubectl`

[azure/setup-kubectl](https://github.com/Azure/setup-kubectl)`azure/k8s-artifact-substitute`

[azure/k8s-artifact-substitute](https://github.com/Azure/k8s-artifact-substitute)`azure/aks-create-action`

[azure/aks-create-action](https://github.com/Azure/aks-create-action)`azure/aks-github-runner`

[azure/aks-github-runner](https://github.com/Azure/aks-github-runner)`azure/acr-build`

[azure/acr-build](https://github.com/Azure/acr-build)## Use GitHub Actions with AKS

As an example, you can use GitHub Actions to deploy an application to your AKS cluster every time a change is pushed to your GitHub repository. This example uses the [Azure Vote](https://github.com/Azure-Samples/azure-voting-app-redis) application.

Note

This example uses a service principal for authentication with your ACR and AKS cluster. Alternatively, you can configure Open ID Connect (OIDC) and update the `azure/login`

action to use OIDC. For more information, see [Set up Azure Login with OpenID Connect authentication](/en-us/azure/developer/github/connect-from-azure?tabs=azure-cli%2Clinux#use-the-azure-login-action-with-openid-connect).

### Fork and update the repository

Navigate to the

[Azure Vote](https://github.com/Azure-Samples/azure-voting-app-redis)repository and select**Fork**.Update the

`azure-vote-all-in-one-redis.yaml`

to use your ACR for the`azure-vote-front`

image. Replace`<registryName>`

with the name of your registry.`... containers: - name: azure-vote-front image: <registryName>.azurecr.io/azuredocs/azure-vote-front:v1 ...`

Commit the updated

`azure-vote-all-in-one-redis.yaml`

to your repository.

### Create secrets

Create a service principal to access your resource group with the

`Contributor`

role using thecommand. Replace`az ad sp create-for-rbac`

`<SUBSCRIPTION_ID>`

with the subscription ID of your Azure account and`<RESOURCE_GROUP>`

with the name of the resource group containing your ACR.`az ad sp create-for-rbac \ --name "ghActionAzureVote" \ --scope /subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP> \ --role Contributor \ --json-auth`

Your output should look similar to the following example output:

`{ "clientId": <clientId>, "clientSecret": <clientSecret>, "subscriptionId": <subscriptionId>, "tenantId": <tenantId>, ... }`

Navigate to your GitHub repository settings and select

**Security**>**Secrets and variables**>**Actions**.For each secret, select

**New Repository Secret**and enter the name and value of the secret.Secret name Secret value AZURE_CREDENTIALS The entire JSON output from the `az ad sp create-for-rbac`

command.service_principal The value of `<clientId>`

.service_principal_password The value of `<clientSecret>`

.subscription The value of `<subscriptionId>`

.tenant The value of `<tenantId>`

.registry The name of your registry. repository azuredocs resource_group The name of your resource group. cluster_name The name of your cluster.

For more information about creating secrets, see [Encrypted Secrets](https://docs.github.com/actions/security-guides/encrypted-secrets#creating-encrypted-secrets-for-a-repository).

### Create actions file

In your repository, create a

`.github/workflows/main.yml`

and paste in the following contents:`name: build_deploy_aks on: push: paths: - "azure-vote/**" jobs: build: runs-on: ubuntu-latest steps: - name: Checkout source code uses: actions/checkout@v3 - name: ACR build id: build-push-acr uses: azure/acr-build@v1 with: service_principal: ${{ secrets.service_principal }} service_principal_password: ${{ secrets.service_principal_password }} tenant: ${{ secrets.tenant }} registry: ${{ secrets.registry }} repository: ${{ secrets.repository }} image: azure-vote-front folder: azure-vote branch: master tag: ${{ github.sha }} - name: Azure login id: login uses: azure/login@v1.4.3 with: creds: ${{ secrets.AZURE_CREDENTIALS }} - name: Set AKS context id: set-context uses: azure/aks-set-context@v3 with: resource-group: '${{ secrets.resource_group }}' cluster-name: '${{ secrets.cluster_name }}' - name: Setup kubectl id: install-kubectl uses: azure/setup-kubectl@v3 - name: Deploy to AKS id: deploy-aks uses: Azure/k8s-deploy@v4 with: namespace: 'default' manifests: | azure-vote-all-in-one-redis.yaml images: '${{ secrets.registry }}.azurecr.io/${{ secrets.repository }}/azure-vote-front:${{ github.sha }}' pull-images: false`

The

`on`

section contains the event that triggers the action. In the example file, the action triggers when a change is pushed to the`azure-vote`

directory.The

`steps`

section contains each distinct action:*Checkout source code*uses the[GitHub Actions Checkout Action](https://github.com/actions/checkout)to clone the repository.*ACR build*uses the[Azure Container Registry Build Action](https://github.com/Azure/acr-build)to build the image and upload it to your registry.*Azure login*uses the[Azure Login Action](https://github.com/Azure/login)to sign in to your Azure account.*Set AKS context*uses the[Azure AKS Set Context Action](https://github.com/Azure/aks-set-context)to set the context for your AKS cluster.*Setup kubectl*uses the[Azure AKS Setup Kubectl Action](https://github.com/Azure/setup-kubectl)to install kubectl on your runner.*Deploy to AKS*uses the[Azure Kubernetes Deploy Action](https://github.com/Azure/k8s-deploy)to deploy the application to your Kubernetes cluster.

Commit the

`.github/workflows/main.yml`

file to your repository.To confirm the action is working, update the

`azure-vote/azure-vote/config_file.cfg`

with the following contents:`# UI Configurations TITLE = 'Azure Voting App' VOTE1VALUE = 'Fish' VOTE2VALUE = 'Dogs' SHOWHOST = 'false'`

Commit the updated

`azure-vote/azure-vote/config_file.cfg`

to your repository.In your repository, select

**Actions**and confirm a workflow is running. Then, confirm the workflow has a green checkmark and the updated application is deployed to your cluster.

## Next steps

Review the following starter workflows for AKS. For more information, see [Using starter workflows](https://docs.github.com/actions/using-workflows/using-starter-workflows#using-starter-workflows).
