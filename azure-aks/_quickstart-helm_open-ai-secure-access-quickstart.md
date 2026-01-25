---
merged_at: 2026-01-25T12:25:33.930073
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



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


---

<!-- DOCUMENTO FUSIONADO: open-ai-secure-access-quickstart.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/open-ai-secure-access-quickstart -->

# Secure access to Azure OpenAI from Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to secure access to Azure OpenAI from Azure Kubernetes Service (AKS) using Microsoft Entra Workload ID. You learn how to:

- Enable workload identities on an AKS cluster.
- Create an Azure user-assigned managed identity.
- Create a Microsoft Entra ID federated credential.
- Enable workload identity on a Kubernetes Pod.

Note

We recommend using Microsoft Entra Workload ID and managed identities on AKS for Azure OpenAI access because it enables a secure, passwordless authentication process for accessing Azure resources.

## Before you begin

- You need an Azure account with an active subscription. If you don't have one,
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - This article builds on
[Deploy an application that uses OpenAI on AKS](open-ai-quickstart). You should complete that article before you begin this one. - You need a custom domain name enabled on your Azure OpenAI account to use for Microsoft Entra authorization. For more information, see
[Custom subdomain names for Azure AI services](/en-us/azure/ai-services/cognitive-services-custom-subdomains).

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Enable Microsoft Entra Workload ID on an AKS cluster

The Microsoft Entra Workload ID and OIDC Issuer Endpoint features aren't enabled on AKS by default. You must enable them on your AKS cluster before you can use them.

Set the resource group name and AKS cluster resource group name variables.

`# Set the resource group variable RG_NAME=myResourceGroup # Set the AKS cluster name based on the resource group variable AKS_NAME=$(az resource list --resource-group $RG_NAME --resource-type Microsoft.ContainerService/managedClusters --query "[0].name" -o tsv)`

Enable the Microsoft Entra Workload ID and OIDC Issuer Endpoint features on your existing AKS cluster using the

command.`az aks update`

`az aks update \ --resource-group $RG_NAME \ --name $AKS_NAME \ --enable-workload-identity \ --enable-oidc-issuer`

Get the AKS OIDC Issuer Endpoint URL using the

command.`az aks show`

`AKS_OIDC_ISSUER=$(az aks show --resource-group $RG_NAME --name $AKS_NAME --query "oidcIssuerProfile.issuerUrl" -o tsv)`


## Create an Azure user-assigned managed identity

Create an Azure user-assigned managed identity using the

command.`az identity create`

`# Set the managed identity name variable MANAGED_IDENTITY_NAME=myIdentity # Create the managed identity az identity create \ --resource-group $RG_NAME \ --name $MANAGED_IDENTITY_NAME`

Get the managed identity client ID and object ID using the

command.`az identity show`

`# Get the managed identity client ID MANAGED_IDENTITY_CLIENT_ID=$(az identity show --resource-group $RG_NAME --name $MANAGED_IDENTITY_NAME --query clientId -o tsv) # Get the managed identity object ID MANAGED_IDENTITY_OBJECT_ID=$(az identity show --resource-group $RG_NAME --name $MANAGED_IDENTITY_NAME --query principalId -o tsv)`

Get the Azure OpenAI resource ID using the

command.`az resource list`

`AOAI_RESOURCE_ID=$(az resource list --resource-group $RG_NAME --resource-type Microsoft.CognitiveServices/accounts --query "[0].id" -o tsv)`

Grant the managed identity access to the Azure OpenAI resource using the

command.`az role assignment create`

`az role assignment create \ --role "Cognitive Services OpenAI User" \ --assignee-object-id $MANAGED_IDENTITY_OBJECT_ID \ --assignee-principal-type ServicePrincipal \ --scope $AOAI_RESOURCE_ID`


## Create a Microsoft Entra ID federated credential

Set the federated credential, namespace, and service account variables.

`# Set the federated credential name variable FEDERATED_CREDENTIAL_NAME=myFederatedCredential # Set the namespace variable SERVICE_ACCOUNT_NAMESPACE=default # Set the service account variable SERVICE_ACCOUNT_NAME=ai-service-account`

Create the federated credential using the

command.`az identity federated-credential create`

`az identity federated-credential create \ --name ${FEDERATED_CREDENTIAL_NAME} \ --resource-group ${RG_NAME} \ --identity-name ${MANAGED_IDENTITY_NAME} \ --issuer ${AKS_OIDC_ISSUER} \ --subject system:serviceaccount:${SERVICE_ACCOUNT_NAMESPACE}:${SERVICE_ACCOUNT_NAME}`


## Use Microsoft Entra Workload ID on AKS

To use Microsoft Entra Workload ID on AKS, you need to make a few changes to the `ai-service`

deployment manifest.

### Create a ServiceAccount

Get the kubeconfig for your cluster using the

command.`az aks get-credentials`

`az aks get-credentials \ --resource-group $RG_NAME \ --name $AKS_NAME`

Create a Kubernetes ServiceAccount using the

command.`kubectl apply`

`kubectl apply -f - <<EOF apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: ${MANAGED_IDENTITY_CLIENT_ID} name: ${SERVICE_ACCOUNT_NAME} namespace: ${SERVICE_ACCOUNT_NAMESPACE} EOF`


### Enable Microsoft Entra Workload ID on the Pod

Set the Azure OpenAI resource name, endpoint, and deployment name variables.

`# Get the Azure OpenAI resource name AOAI_NAME=$(az resource list \ --resource-group $RG_NAME \ --resource-type Microsoft.CognitiveServices/accounts \ --query "[0].name" -o tsv) # Get the Azure OpenAI endpoint AOAI_ENDPOINT=$(az cognitiveservices account show \ --resource-group $RG_NAME \ --name $AOAI_NAME \ --query properties.endpoint -o tsv) # Get the Azure OpenAI deployment name AOAI_DEPLOYMENT_NAME=$(az cognitiveservices account deployment list \ --resource-group $RG_NAME \ --name $AOAI_NAME \ --query "[0].name" -o tsv)`

Redeploy the

`ai-service`

with the ServiceAccount and the`azure.workload.identity/use`

annotation set to`true`

using thecommand.`kubectl apply`

`kubectl apply -f - <<EOF apiVersion: apps/v1 kind: Deployment metadata: name: ai-service spec: replicas: 1 selector: matchLabels: app: ai-service template: metadata: labels: app: ai-service azure.workload.identity/use: "true" spec: serviceAccountName: $SERVICE_ACCOUNT_NAME nodeSelector: "kubernetes.io/os": linux containers: - name: ai-service image: ghcr.io/azure-samples/aks-store-demo/ai-service:latest ports: - containerPort: 5001 env: - name: USE_AZURE_OPENAI value: "True" - name: USE_AZURE_AD value: "True" - name: AZURE_OPENAI_DEPLOYMENT_NAME value: "${AOAI_DEPLOYMENT_NAME}" - name: AZURE_OPENAI_ENDPOINT value: "${AOAI_ENDPOINT}" resources: requests: cpu: 20m memory: 50Mi limits: cpu: 50m memory: 128Mi EOF`


### Test the application

Verify the new pod is running using the

command.`kubectl get pods`

`kubectl get pods --selector app=ai-service`

Get the pod environment variables using the

command. The output demonstrates that the Azure OpenAI API key no longer exists in the Pod's environment variables.`kubectl describe pod`

`kubectl describe pod --selector app=ai-service`

Open a new terminal and get the IP of the store admin service using the following

`echo`

command.`echo "http://$(kubectl get svc/store-admin -o jsonpath='{.status.loadBalancer.ingress[0].ip}')"`

Open a web browser and navigate to the IP address from the previous step.

Select

**Products**. You should be able to add a new product and get a description for it using Azure OpenAI.

## Next steps

In this article, you learned how to secure access to Azure OpenAI from Azure Kubernetes Service (AKS) using Microsoft Entra Workload ID.

For more information on Microsoft Entra Workload ID, see [Microsoft Entra Workload ID](workload-identity-overview).
