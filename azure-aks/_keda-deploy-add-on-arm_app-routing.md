---
merged_at: 2026-01-25T12:06:27.771851
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: keda-deploy-add-on-arm.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/keda-deploy-add-on-arm -->

# Install the Kubernetes Event-driven Autoscaling (KEDA) add-on using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

The KEDA add-on for AKS doesn't currently support modifying the CPU requests or limits and other Helm values for the [Metrics Server](https://keda.sh/docs/2.14/operate/metrics-server/) or [Operator](https://keda.sh/docs/2.14/operate/cluster/). Keep this limitation in mind when using the add-on. If you have any questions, feel free to reach out [here](https://github.com/Azure/AKS/issues).

This article shows you how to deploy the Kubernetes Event-driven Autoscaling (KEDA) add-on to Azure Kubernetes Service (AKS) using an [ARM template](/en-us/azure/azure-resource-manager/templates/).

Important

Your cluster Kubernetes version determines what KEDA version will be installed on your AKS cluster. To see which KEDA version maps to each AKS version, see the **AKS managed add-ons** column of the [Kubernetes component version table](/en-us/azure/aks/supported-kubernetes-versions#aks-components-breaking-changes-by-version).

For GA Kubernetes versions, AKS offers full support of the corresponding KEDA minor version in the table. Kubernetes preview versions and the latest KEDA patch are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Note

KEDA version 2.15+ introduces a breaking change that [removes pod identity support](https://github.com/kedacore/keda/issues/5035). We recommend moving over to workload identity for your authentication if you're using pod identity. While the KEDA managed add-on doesn't currently run KEDA version 2.15+, it will begin running it in the AKS preview version 1.31.

For more information on how to securely scale your applications with workload identity, please read our [tutorial](keda-workload-identity). To view KEDA's breaking change/deprecation policy, please read their [official documentation](https://github.com/kedacore/governance/blob/main/DEPRECATIONS.md).

## Before you begin

- You need an Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - You need the
[Azure CLI installed](/en-us/cli/azure/install-azure-cli). - This article assumes you have an existing Azure resource group. If you don't have an existing resource group, you can create one using the
command.`az group create`

- Ensure you have firewall rules configured to allow access to the Kubernetes API server. For more information, see
[Outbound network and FQDN rules for Azure Kubernetes Service (AKS) clusters](outbound-rules-control-egress#azure-global-required-network-rules). [Create an SSH key pair](#create-an-ssh-key-pair).

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

## Create an SSH key pair

Navigate to the

[Azure Cloud Shell](https://shell.azure.com/).Create an SSH key pair using the

command.`az sshkey create`

`az sshkey create --name <sshkey-name> --resource-group <resource-group-name>`


## Enable the KEDA add-on with an ARM template

Deploy the

[ARM template for an AKS cluster](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fquickstarts%2Fmicrosoft.kubernetes%2Faks%2Fazuredeploy.json).Select

**Edit template**.Enable the KEDA add-on by specifying the

`workloadAutoScalerProfile`

field in the ARM template, as shown in the following example:`"workloadAutoScalerProfile": { "keda": { "enabled": true } }`

Select

**Save**.Update the required values for the ARM template:

**Subscription**: Select the Azure subscription to use for the deployment.**Resource group**: Select the resource group to use for the deployment.**Region**: Select the region to use for the deployment.**Dns Prefix**: Enter a unique DNS name to use for the cluster.**Linux Admin Username**: Enter a username for the cluster.**SSH public key source**: Select**Use existing key stored in Azure**.**Store Keys**: Select the key pair you created earlier in the article.

Select

**Review + create**>**Create**.

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local device, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client.

If you use the Azure Cloud Shell, `kubectl`

is already installed. You can also install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

- Configure
`kubectl`

to connect to your Kubernetes cluster, use the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. The following example gets credentials for the AKS cluster named*MyAKSCluster*in the*MyResourceGroup*:

```
az aks get-credentials --resource-group MyResourceGroup --name MyAKSCluster
```


## Example deployment

The following snippet is a sample deployment that creates a cluster with KEDA enabled with a single node pool comprised of three `DS2_v5`

nodes.

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"resources": [
{
"apiVersion": "2023-03-01",
"dependsOn": [],
"type": "Microsoft.ContainerService/managedClusters",
"location": "westcentralus",
"name": "myAKSCluster",
"properties": {
"kubernetesVersion": "1.27",
"enableRBAC": true,
"dnsPrefix": "myAKSCluster",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": 200,
"count": 3,
"enableAutoScaling": false,
"vmSize": "Standard_D2S_v5",
"osType": "Linux",
"type": "VirtualMachineScaleSets",
"mode": "System",
"maxPods": 110,
"availabilityZones": [],
"nodeTaints": [],
"enableNodePublicIP": false
}
],
"networkProfile": {
"loadBalancerSku": "standard",
"networkPlugin": "kubenet"
},
"workloadAutoScalerProfile": {
"keda": {
"enabled": true
}
}
},
"identity": {
"type": "SystemAssigned"
}
}
]
}
```


## Start scaling apps with KEDA

You can autoscale your apps with KEDA using custom resource definitions (CRDs). For more information, see the [KEDA documentation](https://keda.sh/docs/scalers/).

## Remove resources

Remove the resource group and all related resources using the

command.`az group delete`

`az group delete --name <resource-group-name>`


## Next steps

This article showed you how to install the KEDA add-on on an AKS cluster, and then verify that it's installed and running. With the KEDA add-on installed on your cluster, you can [deploy a sample application](https://github.com/kedacore/sample-dotnet-worker-servicebus-queue) to start scaling apps.

For information on KEDA troubleshooting, see [Troubleshoot the Kubernetes Event-driven Autoscaling (KEDA) add-on](/en-us/troubleshoot/azure/azure-kubernetes/troubleshoot-kubernetes-event-driven-autoscaling-add-on?context=/azure/aks/context/aks-context).

To learn more, view the [upstream KEDA docs](https://keda.sh/docs/2.12/).


---

<!-- DOCUMENTO FUSIONADO: app-routing.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/app-routing -->

# Managed NGINX ingress with the application routing add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

One way to route Hypertext Transfer Protocol (HTTP) and secure (HTTPS) traffic to applications running on an Azure Kubernetes Service (AKS) cluster is to use the [Kubernetes Ingress object](https://kubernetes.io/docs/concepts/services-networking/ingress/). When you create an Ingress object that uses the application routing add-on NGINX Ingress classes, the add-on creates, configures, and manages one or more Ingress controllers in your AKS cluster.

This article shows you how to deploy and configure a basic Ingress controller in your AKS cluster.

## Application routing add-on with NGINX features

The application routing add-on with NGINX delivers the following:

- Easy configuration of managed NGINX Ingress controllers based on
[Kubernetes NGINX Ingress controller](https://kubernetes.github.io/ingress-nginx/). - Integration with
[Azure DNS](/en-us/azure/dns/dns-overview)for public and private zone management - SSL termination with certificates stored in Azure Key Vault.

For other configurations, see:

[DNS and SSL configuration](app-routing-dns-ssl)[Application routing add-on configuration](app-routing-nginx-configuration)[Configure internal NGIX ingress controller for Azure private DNS zone](create-nginx-ingress-private-controller).

With the retirement of [Open Service Mesh](https://release-v1-2.docs.openservicemesh.io/) (OSM) by the Cloud Native Computing Foundation (CNCF), using the application routing add-on with OSM is not recommended.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.54.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

- The application routing add-on supports up to five Azure DNS zones.
- The application routing add-on can only be enabled on AKS clusters with
[managed identity](use-managed-identity). - All global Azure DNS zones integrated with the add-on have to be in the same resource group.
- All private Azure DNS zones integrated with the add-on have to be in the same resource group.
- Editing the ingress-nginx
`ConfigMap`

in the`app-routing-system`

namespace isn't supported. - The following snippet annotations are blocked and will prevent an Ingress from being configured:
`load_module`

,`lua_package`

,`_by_lua`

,`location`

,`root`

,`proxy_pass`

,`serviceaccount`

,`{`

,`}`

,`'`

.

## Enable application routing using Azure CLI

### Enable on a new cluster

To enable application routing on a new cluster, use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command, specifying the

`--enable-app-routing`

flag.```
az aks create \
--resource-group <ResourceGroupName> \
--name <ClusterName> \
--location <Location> \
--enable-app-routing \
--generate-ssh-keys
```


### Enable on an existing cluster

To enable application routing on an existing cluster, use the [ az aks approuting enable](/en-us/cli/azure/aks/approuting#az-aks-approuting-enable) command.

```
az aks approuting enable --resource-group <ResourceGroupName> --name <ClusterName>
```


## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client. You can install it locally using the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell,

`kubectl`

is already installed.Configure `kubectl`

to connect to your Kubernetes cluster using the [az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --resource-group <ResourceGroupName> --name <ClusterName>
```


## Deploy an application

The application routing add-on uses annotations on Kubernetes Ingress objects to create the appropriate resources.

Create the application namespace called

`aks-store`

to run the example pods using the`kubectl create namespace`

command.`kubectl create namespace aks-store`

Deploy the AKS store application using the following YAML manifest file:

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/sample-manifests/docs/app-routing/aks-store-deployments-and-services.yaml -n aks-store`


This manifest will create the necessary deployments and services for the AKS store application.

### Create the Ingress object

The application routing add-on creates an Ingress class on the cluster named *webapprouting.kubernetes.azure.com*. When you create an Ingress object with this class, it activates the add-on.

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: store-front namespace: aks-store spec: ingressClassName: webapprouting.kubernetes.azure.com rules: - http: paths: - backend: service: name: store-front port: number: 80 path: / pathType: Prefix`

Create the ingress resource using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n aks-store`

The following example output shows the created resource:

`ingress.networking.k8s.io/store-front created`


## Verify the managed Ingress was created

You can verify the managed Ingress was created using the `kubectl get ingress`

command.

```
kubectl get ingress -n aks-store
```


The following example output shows the created managed Ingress:

```
NAME CLASS HOSTS ADDRESS PORTS AGE
store-front webapprouting.kubernetes.azure.com * 51.8.10.109 80 110s
```


You can verify that the AKS store works pointing your browser to the public IP address of the Ingress controller. Find the IP address with kubectl:

```
kubectl get service -n app-routing-system nginx -o jsonpath="{.status.loadBalancer.ingress[0].ip}"
```


## Remove the application routing add-on

To remove the associated namespace, use the `kubectl delete namespace`

command.

```
kubectl delete namespace aks-store
```


To remove the application routing add-on from your cluster, use the [ az aks approuting disable](/en-us/cli/azure/aks/approuting#az-aks-approuting-disable) command.

```
az aks approuting disable --name <ClusterName> --resource-group <ResourceGroupName>
```


Note

To avoid potential disruption of traffic into the cluster when the application routing add-on is disabled, some Kubernetes resources, including *configMaps*, *secrets*, and the *deployment* that runs the controller, will remain on the cluster. These resources are in the *app-routing-system* namespace. You can remove these resources if they're no longer needed by deleting the namespace with `kubectl delete ns app-routing-system`

.

## Next steps

[Configure custom ingress configurations](app-routing-nginx-configuration)shows how to create an advanced Ingress configuration and[configure a custom domain using Azure DNS to manage DNS zones and setup a secure ingress](app-routing-dns-ssl).To integrate with an Azure internal load balancer and configure a private Azure DNS zone to enable DNS resolution for the private endpoints to resolve specific domains, see

[Configure internal NGINX ingress controller for Azure private DNS zone](create-nginx-ingress-private-controller).Learn about monitoring the ingress-nginx controller metrics included with the application routing add-on with

[with Prometheus in Grafana](app-routing-nginx-prometheus)(preview) as part of analyzing the performance and usage of your application.
