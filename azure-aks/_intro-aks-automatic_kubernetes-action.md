---
merged_at: 2026-01-25T12:06:27.782042
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: intro-aks-automatic.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/intro-aks-automatic -->

# What is Azure Kubernetes Service (AKS) Automatic?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

Azure Kubernetes Service (AKS) Automatic offers an experience that makes the most common tasks on Kubernetes fast and frictionless, while preserving the flexibility, extensibility, and consistency of Kubernetes. Azure takes care of your cluster setup, including node management, scaling, security, and preconfigured settings that follow AKS well-architected recommendations. Automatic clusters dynamically allocate compute resources based on your specific workload requirements and are tuned for running production applications.

**Production ready by default**: Clusters are preconfigured for optimal production use, suitable for most applications. They offer fully managed node pools that automatically allocate and scale resources based on your workload needs. Pods are bin packed efficiently, to maximize resource utilization.**Built-in best practices and safeguards**: AKS Automatic clusters have a hardened default configuration, with many cluster, application, and networking security settings enabled by default. AKS automatically patches your nodes and cluster components while adhering to any planned maintenance schedules.**Code to Kubernetes in minutes**: Go from a container image to a deployed application that adheres to best practices patterns within minutes, with access to the comprehensive capabilities of the Kubernetes API and its rich ecosystem.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## AKS Automatic and Standard feature comparison

The following table provides a comparison of options that are available, preconfigured, and default in both AKS Automatic and AKS Standard. For more information on whether specific features are available in Automatic, you can check the documentation for that feature.

**Preconfigured** features are always enabled and you can't disable or change their settings. **Default** features are configured for you but can be changed. **Optional** features are available for you to configure and aren't enabled by default.

When enabling optional features, you can follow the linked feature documentation. When you reach a step for cluster creation, follow steps to create an [AKS Automatic cluster](learn/quick-kubernetes-automatic-deploy) instead of creating an AKS Standard cluster.

### Application deployment, monitoring, and observability

Application deployment can be streamlined using [automated deployments](automated-deployments) from source control, which creates Kubernetes manifest and generates CI/CD workflows. Additionally, the cluster is configured with monitoring tools such as Managed Prometheus for metrics, Managed Grafana for visualization, and Container Insights for log collection.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Application deployment | Optional: * Use
* Create deployment pipelines using
* Bring your own CI/CD pipeline. |
Optional: * Use
* Create deployment pipelines using
* Bring your own CI/CD pipeline. |
| Monitoring, logging, and visualization | Default: *
*
*
*
Optional: *
|
Default:
Optional: *
*
*
*
|

### Node management, scaling, and cluster operations

Node management is automatically handled without the need for manual node pool creation. Scaling is seamless, with nodes created based on workload requests. Additionally, features for workload scaling like Horizontal Pod Autoscaler (HPA), [Kubernetes Event Driven Autoscaling (KEDA)](keda-about), and [Vertical Pod Autoscaler (VPA)](vertical-pod-autoscaler) are enabled. Clusters are configured for automatic node repair, automatic cluster upgrades, and detection of deprecated Kubernetes standard API usage. You can also set a planned maintenance schedule for upgrades if needed.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Node management | Preconfigured: AKS Automatic manages the node pools using
|
Default: You create and manage system and user node pools Optional: AKS Standard manages user node pools using
|
| Scaling | Preconfigured: AKS Automatic creates nodes based on workload requests using
|
Default: Manual scaling of node pools. Optional: *
*
*
*
|
| Cluster tier and Service Level Agreement (SLA) | Preconfigured: Standard tier cluster with up to 5,000 nodes, a
|
Default: Free tier cluster with 10 nodes but can support up to 1,000 nodes. Optional: * Standard tier cluster with up to 5,000 nodes and a
* Premium tier cluster with up to 5,000 nodes,
|
| Node operating system | Preconfigured:
|
Default: Ubuntu Optional: *
*
|
| Node resource group | Preconfigured: Fully managed node resource group to prevent accidental or intentional changes to cluster resources. |
Default: Unrestricted Optional:
|
| Node auto-repair | Preconfigured: Continuously monitors the health state of worker nodes and performs
|
Preconfigured: Continuously monitors the health state of worker nodes and performs
|
| Cluster upgrades | Preconfigured: Clusters are
|
Default: Manual upgrade. Optional: Automatic upgrade using a selectable
|
| Kubernetes API breaking change detection | Preconfigured: Cluster upgrades are stopped on detection of
|
Preconfigured: Cluster upgrades are stopped on detection of
|
| Planned maintenance windows | Default: Set
|
Optional: Set
|

### Security and policies

Cluster authentication and authorization use [Azure Role-based Access Control (RBAC) for Kubernetes authorization](manage-azure-rbac) and applications can use features like [workload identity with Microsoft Entra Workload ID](workload-identity-overview) and [OpenID Connect (OIDC) cluster issuer](use-oidc-issuer) to have secure communication with Azure services. [Deployment safeguards](deployment-safeguards) enforce Kubernetes best practices through Azure Policy controls and the built-in [image cleaner](image-cleaner) removes unused images with vulnerabilities, enhancing image security.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Cluster authentication and authorization | Preconfigured:
|
Default: Local accounts. Optional: *
*
|
| Cluster security | Preconfigured:
|
Optional:
|
| Application security | Preconfigured: *
*
Optional:*
|
Optional: *
*
Optional:*
|
| Image security | Preconfigured:
|
Optional:
|
| Policy enforcement | Preconfigured:
Optional:*
|
Optional:
Optional:*
|
| Managed namespaces | Optional: Use
|
Optional: Use
|

### Networking

AKS Automatic clusters use [managed Virtual Network powered by Azure CNI Overlay with Cilium](azure-cni-powered-by-cilium) for high-performance networking and robust security. Ingress is handled by [managed NGINX using the application routing add-on](app-routing), integrating seamlessly with Azure DNS and Azure Key Vault. Egress uses a [managed NAT gateway](nat-gateway#create-an-aks-cluster-with-a-managed-nat-gateway) for scalable outbound connections. Additionally, you have the flexibility to enable [Istio-based service mesh add-on for AKS](istio-about) or bring your own service mesh.

| Option | AKS Automatic | AKS Standard |
|---|---|---|
| Virtual network | Default:
Optional: *
*
|
Default:
Optional: *
*
*
*
|
| Ingress | Preconfigured:
Optional: *
* Bring your own ingress or gateway. |
Optional: *
*
* Bring your own ingress or gateway. |
| Egress | Preconfigured:
Optional (with custom virtual network): *
*
*
|
Default:
Optional: *
*
*
|
| Service mesh | Optional: *
* Bring your own service mesh. |
Optional: *
* Bring your own service mesh. |

## Next steps

To learn more about AKS Automatic, follow the quickstart to create a cluster.


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
