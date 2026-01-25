---
merged_at: 2026-01-25T12:06:27.791526
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: kubernetes-helm.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kubernetes-helm -->

# Install existing applications with Helm in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Helm](https://github.com/kubernetes/helm/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications. Similar to Linux package managers, such as *APT* and *Yum*, you can use Helm to manage Kubernetes charts, which are packages of preconfigured Kubernetes resources.

This article shows you how to configure and use Helm in a Kubernetes cluster on Azure Kubernetes Service (AKS).

## Before you begin

- This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[Azure portal](learn/quick-kubernetes-deploy-portal). - Your AKS cluster needs to have
**an integrated ACR**. For details on creating an AKS cluster with an integrated ACR, see[Authenticate with Azure Container Registry from Azure Kubernetes Service](cluster-container-registry-integration#create-a-new-acr). - You also need the Helm CLI installed, which is the client that runs on your development system. It allows you to start, stop, and manage applications with Helm. If you use the Azure Cloud Shell, the Helm CLI is already installed. For installation instructions on your local platform, see
[Installing Helm](https://helm.sh/docs/intro/install/).

Important

Helm is intended to run on Linux nodes. If you have Windows Server nodes in your cluster, you must ensure that Helm pods are only scheduled to run on Linux nodes. You also need to ensure that any Helm charts you install are also scheduled to run on the correct nodes. The commands in this article use [node-selectors](https://kubernetes.io/docs/concepts/scheduling-eviction/assign-pod-node/#nodeselector) to make sure pods are scheduled to the correct nodes, but not all Helm charts may expose a node selector. You can also consider using other options on your cluster, such as [taints](operator-best-practices-advanced-scheduler).

## Verify your version of Helm

Use the

`helm version`

command to verify you have Helm 3 installed.`helm version`

The following example output shows Helm version 3.0.0 installed:

`version.BuildInfo{Version:"v3.0.0", GitCommit:"e29ce2a54e96cd02ccfce88bee4f58bb6e2a28b6", GitTreeState:"clean", GoVersion:"go1.13.4"}`


## Install an application with Helm v3

### Add Helm repositories

Add the

*ingress-nginx*repository using the[helm repo](https://helm.sh/docs/intro/quickstart/#initialize-a-helm-chart-repository)command.`helm repo add ingress-nginx https://kubernetes.github.io/ingress-nginx`


### Find Helm charts

Search for precreated Helm charts using the

[helm search](https://helm.sh/docs/intro/using_helm/#helm-search-finding-charts)command.`helm search repo ingress-nginx`

The following condensed example output shows some of the Helm charts available for use:

`NAME CHART VERSION APP VERSION DESCRIPTION ingress-nginx/ingress-nginx 4.7.0 1.8.0 Ingress controller for Kubernetes using NGINX a...`

Update the list of charts using the

[helm repo update](https://helm.sh/docs/intro/using_helm/#helm-repo-working-with-repositories)command.`helm repo update`

The following example output shows a successful repo update:

`Hang tight while we grab the latest from your chart repositories... ...Successfully got an update from the "ingress-nginx" chart repository Update Complete. ⎈ Happy Helming!⎈`


## Import the Helm chart images into your ACR

This article uses the [NGINX ingress controller Helm chart](https://github.com/kubernetes/ingress-nginx/tree/main/charts/ingress-nginx), which relies on three container images.

Use

`az acr import`

to import the NGINX ingress controller images into your ACR.`REGISTRY_NAME=<REGISTRY_NAME> CONTROLLER_REGISTRY=registry.k8s.io CONTROLLER_IMAGE=ingress-nginx/controller CONTROLLER_TAG=v1.8.0 PATCH_REGISTRY=registry.k8s.io PATCH_IMAGE=ingress-nginx/kube-webhook-certgen PATCH_TAG=v20230407 DEFAULTBACKEND_REGISTRY=registry.k8s.io DEFAULTBACKEND_IMAGE=defaultbackend-amd64 DEFAULTBACKEND_TAG=1.5 az acr import --name $REGISTRY_NAME --source $CONTROLLER_REGISTRY/$CONTROLLER_IMAGE:$CONTROLLER_TAG --image $CONTROLLER_IMAGE:$CONTROLLER_TAG az acr import --name $REGISTRY_NAME --source $PATCH_REGISTRY/$PATCH_IMAGE:$PATCH_TAG --image $PATCH_IMAGE:$PATCH_TAG az acr import --name $REGISTRY_NAME --source $DEFAULTBACKEND_REGISTRY/$DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG --image $DEFAULTBACKEND_IMAGE:$DEFAULTBACKEND_TAG`

Note

In addition to importing container images into your ACR, you can also import Helm charts into your ACR. For more information, see

[Push and pull Helm charts to an Azure container registry](/en-us/azure/container-registry/container-registry-helm-repos).

### Run Helm charts

Install Helm charts using the

[helm install](https://helm.sh/docs/intro/using_helm/#helm-install-installing-a-package)command and specify a release name and the name of the chart to install.Tip

The following example creates a Kubernetes namespace for the ingress resources named

*ingress-basic*and is intended to work within that namespace. Specify a namespace for your own environment as needed.`ACR_URL=<REGISTRY_URL> # Create a namespace for your ingress resources kubectl create namespace ingress-basic # Use Helm to deploy an NGINX ingress controller helm install ingress-nginx ingress-nginx/ingress-nginx \ --version 4.0.13 \ --namespace ingress-basic \ --set controller.replicaCount=2 \ --set controller.nodeSelector."kubernetes\.io/os"=linux \ --set controller.image.registry=$ACR_URL \ --set controller.image.image=$CONTROLLER_IMAGE \ --set controller.image.tag=$CONTROLLER_TAG \ --set controller.image.digest="" \ --set controller.admissionWebhooks.patch.nodeSelector."kubernetes\.io/os"=linux \ --set controller.service.annotations."service\.beta\.kubernetes\.io/azure-load-balancer-health-probe-request-path"=/healthz \ --set controller.admissionWebhooks.patch.image.registry=$ACR_URL \ --set controller.admissionWebhooks.patch.image.image=$PATCH_IMAGE \ --set controller.admissionWebhooks.patch.image.tag=$PATCH_TAG \ --set defaultBackend.nodeSelector."kubernetes\.io/os"=linux \ --set defaultBackend.image.registry=$ACR_URL \ --set defaultBackend.image.image=$DEFAULTBACKEND_IMAGE \ --set defaultBackend.image.tag=$DEFAULTBACKEND_TAG \ --set defaultBackend.image.digest=""`

The following condensed example output shows the deployment status of the Kubernetes resources created by the Helm chart:

`NAME: nginx-ingress LAST DEPLOYED: Wed Jul 28 11:35:29 2021 NAMESPACE: ingress-basic STATUS: deployed REVISION: 1 TEST SUITE: None NOTES: The ingress-nginx controller has been installed. It may take a few minutes for the LoadBalancer IP to be available. You can watch the status by running 'kubectl --namespace ingress-basic get services -o wide -w nginx-ingress-ingress-nginx-controller' ...`

Get the

*EXTERNAL-IP*of your service using the`kubectl get services`

command.`kubectl --namespace ingress-basic get services -o wide -w ingress-nginx-ingress-nginx-controller`

The following example output shows the

*EXTERNAL-IP*for the*ingress-nginx-ingress-nginx-controller*service:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE SELECTOR nginx-ingress-ingress-nginx-controller LoadBalancer 10.0.254.93 <EXTERNAL_IP> 80:30004/TCP,443:30348/TCP 61s app.kubernetes.io/component=controller,app.kubernetes.io/instance=nginx-ingress,app.kubernetes.io/name=ingress-nginx`


### List releases

Get a list of releases installed on your cluster using the

`helm list`

command.`helm list --namespace ingress-basic`

The following example output shows the

*ingress-nginx*release deployed in the previous step:`NAME NAMESPACE REVISION UPDATED STATUS CHART APP VERSION ingress-nginx ingress-basic 1 2021-07-28 11:35:29.9623734 -0500 CDT deployed ingress-nginx-3.34.0 0.47.0`


### Clean up resources

Deploying a Helm chart creates Kubernetes resources like pods, deployments, and services.

Clean up resources using the

[helm uninstall](https://helm.sh/docs/intro/using_helm/#helm-uninstall-uninstalling-a-release)command and specify your release name.`helm uninstall --namespace ingress-basic ingress-nginx`

The following example output shows the release named

*ingress-nginx*has been uninstalled:`release "nginx-ingress" uninstalled`

Delete the entire sample namespace along with the resources using the

`kubectl delete`

command and specify your namespace name.`kubectl delete namespace ingress-basic`


## Next steps

For more information about managing Kubernetes application deployments with Helm, see the Helm documentation.


---

<!-- DOCUMENTO FUSIONADO: quickstart-helm.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/quickstart-helm -->

# Quickstart: Develop on Azure Kubernetes Service (AKS) with Helm

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Helm](https://helm.sh/) is an open-source packaging tool that helps you install and manage the lifecycle of Kubernetes applications. Similar to Linux package managers like *APT* and *Yum*, Helm manages Kubernetes charts, which are packages of pre-configured Kubernetes resources.

In this quickstart, you use Helm to package and run an application on AKS. For information on installing an existing application using Helm, see [Install existing applications with Helm in AKS](kubernetes-helm).

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). [Azure CLI](/en-us/cli/azure/install-azure-cli)or[Azure PowerShell](/en-us/powershell/azure/install-az-ps)installed.[Helm v3 installed](https://helm.sh/docs/intro/install/).

## Create an Azure Container Registry

You need to store your container images in an Azure Container Registry (ACR) to run your application in your AKS cluster using Helm. Your registry name must be unique within Azure and contain 5-50 alphanumeric characters. Only lowercase characters are allowed. The *Basic* SKU is a cost-optimized entry point for development purposes that provides a balance of storage and throughput.

Create an Azure resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command. The following example creates a resource group named*myResourceGroup*in the*eastus*location.`az group create --name myResourceGroup --location eastus`

Create an Azure Container Registry with a unique name by calling the

[az acr create](/en-us/cli/azure/acr#az-acr-create)command. The following example creates an ACR named*myhelmacr*with the*Basic*SKU.`az acr create --resource-group myResourceGroup --name myhelmacr --sku Basic`

Your output should look similar to the following condensed example output. Take note of your

*loginServer*value for your ACR to use in a later step.`{ "adminUserEnabled": false, "creationDate": "2023-12-26T22:36:23.998425+00:00", "id": "/subscriptions/<ID>/resourceGroups/myResourceGroup/providers/Microsoft.ContainerRegistry/registries/myhelmacr", "location": "eastus", "loginServer": "myhelmacr.azurecr.io", "name": "myhelmacr", "networkRuleSet": null, "provisioningState": "Succeeded", "resourceGroup": "myResourceGroup", "sku": { "name": "Basic", "tier": "Basic" }, "status": null, "storageAccount": null, "tags": {}, "type": "Microsoft.ContainerRegistry/registries" }`


## Create an AKS cluster

Your new AKS cluster needs access to your ACR to pull the container images and run them.

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command with the`--attach-acr`

parameter to grant the cluster access to your ACR. The following example creates an AKS cluster named*myAKSCluster*and grants it access to the*myhelmacr*ACR. Make sure you replace`myhelmacr`

with the name of your ACR.`az aks create --resource-group myResourceGroup --name myAKSCluster --location eastus --attach-acr myhelmacr --generate-ssh-keys`


## Connect to your AKS cluster

To connect a Kubernetes cluster locally, you use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell.

Install

`kubectl`

locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.`az aks install-cli`

Configure

`kubectl`

to connect to your Kubernetes cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. The following command gets credentials for the AKS cluster named*myAKSCluster*in*myResourceGroup*.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`


## Download the sample application

This quickstart uses the [Azure Vote application](https://github.com/Azure-Samples/azure-voting-app-redis.git).

Clone the application from GitHub using the

`git clone`

command.`git clone https://github.com/Azure-Samples/azure-voting-app-redis.git`

Navigate to the

`azure-vote`

directory using the`cd`

command.`cd azure-voting-app-redis/azure-vote/`


## Build and push the sample application to ACR

Build and push the image to your ACR using the

[az acr build](/en-us/cli/azure/acr#az-acr-build)command. The following example builds an image named*azure-vote-front:v1*and pushes it to the*myhelmacr*ACR. Make sure you replace`myhelmacr`

with the name of your ACR.`az acr build --image azure-vote-front:v1 --registry myhelmacr --file Dockerfile .`


Note

You can also import Helm charts into your ACR. For more information, see [Push and pull Helm charts to an Azure container registry](/en-us/azure/container-registry/container-registry-helm-repos).

## Create your Helm chart

Generate your Helm chart using the

`helm create`

command.`helm create azure-vote-front`

Update

*azure-vote-front/Chart.yaml*to add a dependency for the*redis*chart from the`https://charts.bitnami.com/bitnami`

chart repository and update`appVersion`

to`v1`

, as shown in the following example:Note

The container image versions shown in this guide have been tested to work with this example but may not be the latest version available.

`apiVersion: v2 name: azure-vote-front description: A Helm chart for Kubernetes dependencies: - name: redis version: 17.3.17 repository: https://charts.bitnami.com/bitnami ... # This is the version number of the application being deployed. This version number should be # incremented each time you make changes to the application. appVersion: v1`

Update your Helm chart dependencies using the

`helm dependency update`

command.`helm dependency update azure-vote-front`

Update

*azure-vote-front/values.yaml*with the following changes.- Add a
*redis*section to set the image details, container port, and deployment name. - Add a
*backendName*for connecting the frontend portion to the*redis*deployment. - Change
*image.repository*to`<loginServer>/azure-vote-front`

. - Change
*image.tag*to`v1`

. - Change
*service.type*to*LoadBalancer*.

For example:

`replicaCount: 1 backendName: azure-vote-backend-master redis: image: registry: mcr.microsoft.com repository: oss/bitnami/redis tag: 6.0.8 fullnameOverride: azure-vote-backend auth: enabled: false image: repository: myhelmacr.azurecr.io/azure-vote-front pullPolicy: IfNotPresent tag: "v1" ... service: type: LoadBalancer port: 80 ...`

- Add a
Add an

`env`

section to*azure-vote-front/templates/deployment.yaml*to pass the name of the*redis*deployment.`... containers: - name: {{ .Chart.Name }} securityContext: {{- toYaml .Values.securityContext | nindent 12 }} image: "{{ .Values.image.repository }}:{{ .Values.image.tag | default .Chart.AppVersion }}" imagePullPolicy: {{ .Values.image.pullPolicy }} env: - name: REDIS value: {{ .Values.backendName }} ...`


## Run your Helm chart

Install your application using your Helm chart using the

`helm install`

command.`helm install azure-vote-front azure-vote-front/`

It takes a few minutes for the service to return a public IP address. Monitor progress using the

`kubectl get service`

command with the`--watch`

argument.`kubectl get service azure-vote-front --watch`

When the service is ready, the

`EXTERNAL-IP`

value changes from`<pending>`

to an IP address. Press`CTRL+C`

to stop the`kubectl`

watch process.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE azure-vote-front LoadBalancer 10.0.18.228 <pending> 80:32021/TCP 6s ... azure-vote-front LoadBalancer 10.0.18.228 52.188.140.81 80:32021/TCP 2m6s`

Navigate to your application's load balancer in a browser using the

`<EXTERNAL-IP>`

to see the sample application.

## Delete the cluster

Remove your resource group, AKS cluster, Azure container registry, container images stored in the ACR, and all related resources using the

[az group delete](/en-us/cli/azure/group#az-group-delete)command with the`--yes`

parameter to confirm deletion and the`--no-wait`

parameter to return to the command prompt without waiting for the operation to complete.`az group delete --name myResourceGroup --yes --no-wait`


Note

If you created your AKS cluster with a system-assigned managed identity (the default identity option in this quickstart), the identity is managed by the platform and doesn't require removal.

If you created your AKS cluster with a service principal, the service principal isn't removed when you delete the cluster. To remove the service principal, see [AKS service principal considerations and deletion](kubernetes-service-principal#considerations-when-using-a-service-principal).

## Next steps

For more information about using Helm, see the [Helm documentation](https://helm.sh/docs/).
