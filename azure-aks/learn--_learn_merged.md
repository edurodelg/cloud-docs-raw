---
merged_at: 2026-01-26T20:54:25.734164
merged_files: 11
---


---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-terraform -->

# Quickstart: Create a Windows-based Azure Kubernetes Service (AKS) cluster using Terraform

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this quickstart, you create an Azure Kubernetes cluster with a Windows node pool using Terraform. Azure Kubernetes Service (AKS) is a managed container orchestration service provided by Azure. It simplifies the deployment, scaling, and operations of containerized applications. The service uses Kubernetes, an open-source system for automating the deployment, scaling, and management of containerized applications. The Windows node pool allows you to run Windows containers in your Kubernetes cluster.

[Terraform](https://www.terraform.io) enables the definition, preview, and deployment of cloud infrastructure. Using Terraform, you create configuration files using [HCL syntax](https://developer.hashicorp.com/terraform/language/syntax/configuration). The HCL syntax allows you to specify the cloud provider - such as Azure - and the elements that make up your cloud infrastructure. After you create your configuration files, you create an *execution plan* that allows you to preview your infrastructure changes before they're deployed. Once you verify the changes, you apply the execution plan to deploy the infrastructure.

- Generate a random resource group name.
- Create an Azure resource group.
- Create an Azure virtual network.
- Create an Azure Kubernetes cluster.
- Create an Azure Kubernetes cluster node pool.

## Prerequisites

Create an Azure account with an active subscription. You can

[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn).

## Implement the Terraform code

Note

The sample code for this article is located in the [Azure Terraform GitHub repo](https://github.com/Azure/terraform/tree/master/quickstart/101-aks-cluster-windows). You can view the log file containing the [test results from current and previous versions of Terraform](https://github.com/Azure/terraform/tree/master/quickstart/101-aks-cluster-windows/TestRecord.md).

See more [articles and sample code showing how to use Terraform to manage Azure resources](/en-us/azure/terraform)

Create a directory in which to test and run the sample Terraform code and make it the current directory.

Create a file named

`providers.tf`

and insert the following code.`terraform { required_version = ">= 1.0" required_providers { azurerm = { source = "hashicorp/azurerm" version = "~>3.0" } random = { source = "hashicorp/random" version = "~>3.0" } } } provider "azurerm" { features { } }`

Create a file named

`main.tf`

and insert the following code.`# Generate random resource group name resource "random_pet" "rg_name" { prefix = var.resource_group_name_prefix } resource "azurerm_resource_group" "rg" { location = var.resource_group_location name = random_pet.rg_name.id } resource "random_pet" "azurerm_kubernetes_cluster_name" { prefix = "cluster" } resource "random_pet" "azurerm_kubernetes_cluster_dns_prefix" { prefix = "dns" } resource "random_string" "azurerm_kubernetes_cluster_node_pool" { length = 6 special = false numeric = false lower = true upper = false } resource "azurerm_virtual_network" "vnet" { name = "myvnet" location = azurerm_resource_group.rg.location resource_group_name = azurerm_resource_group.rg.name address_space = ["10.1.0.0/16"] subnet { name = "subnet1" address_prefix = "10.1.1.0/24" } } resource "azurerm_kubernetes_cluster" "aks" { name = random_pet.azurerm_kubernetes_cluster_name.id location = azurerm_resource_group.rg.location resource_group_name = azurerm_resource_group.rg.name dns_prefix = random_pet.azurerm_kubernetes_cluster_dns_prefix.id identity { type = "SystemAssigned" } default_node_pool { name = "agentpool" vm_size = "Standard_D2_v2" node_count = var.node_count_linux vnet_subnet_id = element(tolist(azurerm_virtual_network.vnet.subnet), 0).id } windows_profile { admin_username = var.admin_username admin_password = var.admin_password } network_profile { network_plugin = "azure" load_balancer_sku = "standard" } } resource "azurerm_kubernetes_cluster_node_pool" "win" { name = random_string.azurerm_kubernetes_cluster_node_pool.result kubernetes_cluster_id = azurerm_kubernetes_cluster.aks.id vm_size = "Standard_D4s_v3" node_count = var.node_count_windows os_type = "Windows" }`

Create a file named

`variables.tf`

and insert the following code.`variable "resource_group_location" { type = string default = "eastus" description = "Location of the resource group." } variable "resource_group_name_prefix" { type = string default = "rg" description = "Prefix of the resource group name that's combined with a random ID so name is unique in your Azure subscription." } variable "node_count_linux" { type = number description = "The initial quantity of Linux nodes for the node pool." default = 1 } variable "node_count_windows" { type = number description = "The initial quantity of Windows nodes for the node pool." default = 1 } variable "admin_username" { type = string description = "The admin username for the Windows node pool." default = "azureuser" } variable "admin_password" { type = string description = "The admin password for the Windows node pool." default = "Passw0rd1234Us!" }`

Create a file named

`outputs.tf`

and insert the following code.`output "resource_group_name" { value = azurerm_resource_group.rg.name } output "kubernetes_cluster_name" { value = azurerm_kubernetes_cluster.aks.name } output "kubernetes_cluster_dns_prefix" { value = azurerm_kubernetes_cluster.aks.dns_prefix } output "kubernetes_cluster_node_pool_name" { value = azurerm_kubernetes_cluster_node_pool.win.name } output "kubernetes_cluster_kube_config_raw" { value = azurerm_kubernetes_cluster.aks.kube_config_raw sensitive = true }`


## Initialize Terraform

Run [terraform init](https://www.terraform.io/docs/commands/init.html) to initialize the Terraform deployment. This command downloads the Azure provider required to manage your Azure resources.

```
terraform init -upgrade
```


**Key points:**

- The
`-upgrade`

parameter upgrades the necessary provider plugins to the newest version that complies with the configuration's version constraints.

## Create a Terraform execution plan

Run [terraform plan](https://www.terraform.io/docs/commands/plan.html) to create an execution plan.

```
terraform plan -out main.tfplan
```


**Key points:**

- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

## Apply a Terraform execution plan

Run [terraform apply](https://www.terraform.io/docs/commands/apply.html) to apply the execution plan to your cloud infrastructure.

```
terraform apply main.tfplan
```


**Key points:**

- The example
`terraform apply`

command assumes you previously ran`terraform plan -out main.tfplan`

. - If you specified a different filename for the
`-out`

parameter, use that same filename in the call to`terraform apply`

. - If you didn't use the
`-out`

parameter, call`terraform apply`

without any parameters.

## Verify the results

Run [kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) to print the cluster's nodes.

```
kubectl get node -o wide
```


## Clean up resources

When you no longer need the resources created via Terraform, do the following steps:

Run

[terraform plan](https://www.terraform.io/docs/commands/plan.html)and specify the`destroy`

flag.`terraform plan -destroy -out main.destroy.tfplan`

**Key points:**- The
`terraform plan`

command creates an execution plan, but doesn't execute it. Instead, it determines what actions are necessary to create the configuration specified in your configuration files. This pattern allows you to verify whether the execution plan matches your expectations before making any changes to actual resources. - The optional
`-out`

parameter allows you to specify an output file for the plan. Using the`-out`

parameter ensures that the plan you reviewed is exactly what is applied.

- The
Run

[terraform apply](https://www.terraform.io/docs/commands/apply.html)to apply the execution plan.`terraform apply main.destroy.tfplan`


## Troubleshoot Terraform on Azure

[Troubleshoot common problems when using Terraform on Azure](/en-us/azure/developer/terraform/troubleshoot).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-portal -->

# Deploy a Windows Server container on an Azure Kubernetes Service (AKS) cluster using the Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this article, you deploy an AKS cluster that runs Windows Server containers using the Azure portal. You also deploy an ASP.NET sample application in a Windows Server container to the cluster.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - If you're unfamiliar with the Azure Cloud Shell, review
[Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview). - Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

## Create an AKS cluster

Sign in to the

[Azure portal](https://portal.azure.com).On the Azure portal home page, select

**Create a resource**.In the

**Categories**section, select**Containers**>**Azure Kubernetes Service (AKS)**.On the

**Basics**tab, configure the following settings:- Under
**Project details**:**Subscription**: Select the Azure subscription you want to use for this AKS cluster.**Resource group**: Select**Create new**, enter a resource group name, such as*myResourceGroup*, and then select**Ok**. While you can select an existing resource group, for testing or evaluation purposes, we recommend creating a resource group to temporarily host these resources and avoid impacting your production or development workloads.

- Under
**Cluster details**:**Cluster preset configuration**: Select**Dev/Test**. For more details on preset configurations, see[Cluster configuration presets in the Azure portal](../quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal).**Kubernetes cluster name**: Enter a cluster name, such as*myAKSCluster*.**Region**: Select a region, such as*East US 2*.**Availability zones**: Select**None**.**AKS pricing tier**: Select**Free**.Leave the default values for the remaining settings, and select

**Next**.


- Under
On the

**Node pools**tab, configure the following settings:Select

**Add node pool**and enter a**Node pool name**, such as*npwin*. For a Windows node pool, the name must be*six characters or fewer*.**Mode**: Select**User**.**OS SKU**: Select**Windows 2022**.**Availability zones**: Select**None**.Leave the

**Enable Azure Spot instances**checkbox unchecked.**Node size**: Select**Choose a size**. On the**Select a VM size**page, select**D2s_v3**, and then select**Select**.Leave the default values for the remaining settings, and select

**Add**.

Select

**Review + create**to run validation on the cluster configuration. After validation completes, select**Create**.It takes a few minutes to create the AKS cluster. When your deployment is complete, navigate to your resource by selecting

**Go to resource**, or by browsing to the AKS cluster resource group and selecting the AKS resource.

## Connect to the cluster

You use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client, to manage your Kubernetes clusters. `kubectl`

is already installed if you use Azure Cloud Shell. If you're unfamiliar with the Cloud Shell, review [Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview).

Open Cloud Shell by selecting the

`>_`

button at the top of the Azure portal page.Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. The following command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

`kubectl get nodes`

command, which returns a list of the cluster nodes.`kubectl get nodes`

The following sample output shows all the nodes in the cluster. Make sure the status of all nodes is

*Ready*:`NAME STATUS ROLES AGE VERSION aks-agentpool-11741175-vmss000000 Ready agent 8m17s v1.29.9 aks-agentpool-11741175-vmss000001 Ready agent 8m17s v1.29.9 aksnpwin000000 Ready agent 8m17s v1.29.9 aks-userpool-11741175-vmss000000 Ready agent 8m17s v1.29.9 aks-userpool-11741175-vmss000001 Ready agent 8m17s v1.29.9`


## Deploy the application

A Kubernetes manifest file defines a desired state for the cluster, such as which container images to run. In this quickstart, you use a manifest file to create all objects needed to run the ASP.NET sample application in a Windows Server container. This manifest file includes a [Kubernetes deployment](../concepts-clusters-workloads#deployments-and-yaml-manifests) for the ASP.NET sample application and an external [Kubernetes service](../concepts-network-services) to access the application from the internet.

The ASP.NET sample application is provided as part of the [.NET Framework Samples](https://hub.docker.com/_/microsoft-dotnet-framework-samples/) and runs in a Windows Server container. The Kubernetes manifest file must define a [node selector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) to tell your AKS cluster to run your ASP.NET sample application's pod on a node that can run Windows Server containers.

Create a file named

`sample.yaml`

and paste in the following YAML definition.`apiVersion: apps/v1 kind: Deployment metadata: name: sample labels: app: sample spec: replicas: 1 template: metadata: name: sample labels: app: sample spec: nodeSelector: "kubernetes.io/os": windows containers: - name: sample image: mcr.microsoft.com/dotnet/framework/samples:aspnetapp resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 selector: matchLabels: app: sample --- apiVersion: v1 kind: Service metadata: name: sample spec: type: LoadBalancer ports: - protocol: TCP port: 80 selector: app: sample`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f sample.yaml`

The following sample output shows the deployment and service created successfully:

`deployment.apps/sample created service/sample created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete. Occasionally, the service can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

Check the status of the deployed pods using the

command. Make all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service sample --watch`

Initially, the output shows the

*EXTERNAL-IP*for the sample service as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE sample LoadBalancer 10.0.37.27 <pending> 80:30572/TCP 6s`

When the

*EXTERNAL-IP*address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.See the sample app in action by opening a web browser to the external IP address of your service.


## Delete resources

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), you should delete your cluster to avoid incurring Azure charges.

In the Azure portal, navigate to your resource group.

Select

**Delete resource group**.Enter the name of your resource group to confirm deletion and select

**Delete**.In the

**Delete confirmation**dialog box, select**Delete**.Note

The AKS cluster was created with system-assigned managed identity (default identity option used in this quickstart), the identity is managed by the platform and does not require removal.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed an ASP.NET sample application in a Windows Server container to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS, and to walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-powershell -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using Azure PowerShell

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Deploy an AKS cluster using Azure PowerShell.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This article assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. For ease of use, try the PowerShell environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Quickstart for Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you want to use PowerShell locally, then install the

[Az PowerShell](/en-us/powershell/azure/new-azureps-module-az)module and connect to your Azure account using the[Connect-AzAccount](/en-us/powershell/module/az.accounts/Connect-AzAccount)cmdlet. Make sure that you run the commands with administrative privileges. For more information, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps).Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).If you have more than one Azure subscription, set the subscription that you wish to use for the quickstart by calling the

[Set-AzContext](/en-us/powershell/module/az.accounts/set-azcontext)cmdlet. For more information, see[Manage Azure subscriptions with Azure PowerShell](/en-us/powershell/azure/manage-subscriptions-azureps#change-the-active-subscription).

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the

cmdlet.`New-AzResourceGroup`

`New-AzResourceGroup -Name myResourceGroup -Location eastus`

The following example output resembles successful creation of the resource group:

`ResourceGroupName : myResourceGroup Location : eastus ProvisioningState : Succeeded Tags : ResourceId : /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup`


## Create AKS cluster

To create an AKS cluster, use the [ New-AzAksCluster](/en-us/powershell/module/az.aks/new-azakscluster) cmdlet. The following example creates a cluster named

*myAKSCluster*with one node and enables a system-assigned managed identity.

```
New-AzAksCluster -ResourceGroupName myResourceGroup `
-Name myAKSCluster `
-NodeCount 1 `
-EnableManagedIdentity `
-GenerateSshKey
```


After a few minutes, the command completes and returns information about the cluster.

Note

When you create an AKS cluster, a second resource group called the *node resource group* is automatically created to store the AKS resources. For more information, see [Node resource group](../core-aks-concepts#node-resource-group). When you [delete the resource group](#delete-resources) for the AKS cluster, the node resource group is also deleted. You also see a *NetworkWatcherRG* resource group created by default. This resource group is used by Azure Network Watcher to store monitoring data. You can safely ignore this resource group. For more information, see [Enable or disable Azure Network Watcher](/en-us/azure/network-watcher/network-watcher-create).

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, call the `Install-AzAksCliTool`

cmdlet.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecmdlet. This command downloads credentials and configures the Kubernetes CLI to use them.`Import-AzAksCredential`

`Import-AzAksCredential -ResourceGroupName myResourceGroup -Name myAKSCluster`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the single node created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-nodepool1-11853318-vmss000000 Ready agent 2m26s v1.27.7`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Create a file named

`aks-store-quickstart.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: rabbitmq spec: replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 resources: requests: cpu: 1m memory: 1Mi limits: cpu: 1m memory: 7Mi --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make all pods are`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete resources

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges. Remove the resource group, container service, and all related resources by calling the [ Remove-AzResourceGroup](/en-us/powershell/module/az.resources/remove-azresourcegroup) cmdlet.

```
Remove-AzResourceGroup -Name myResourceGroup
```


Note

The AKS cluster was created with system-assigned managed identity (default identity option used in this quickstart), the identity is managed by the platform and doesn't require removal.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-portal -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using Azure portal

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Deploy an AKS cluster using the Azure portal.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - If you're unfamiliar with the Azure Cloud Shell, review
[Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview). - Make sure that the identity you use to create your cluster has the appropriate minimum permissions. For more information about access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Create an AKS cluster

Sign in to the

[Azure portal](https://portal.azure.com).On the Azure portal home page, select

**Create a resource**.In the

**Categories**section, select**Infrastructure Services**>**Azure Kubernetes Service (AKS)**.On the

**Basics**tab, configure the following settings:Under

**Project details**:**Subscription**: Select the Azure subscription you want to use for this AKS cluster.**Resource group**: Select**Create new**, enter a resource group name, like*myResourceGroup*, and then select**Ok**. While you can select an existing resource group, for testing or evaluation purposes, we recommend creating a resource group to temporarily host these resources and avoid impacting your production or development workloads.

Under

**Cluster details**:**Cluster preset configuration**: Select**Dev/Test**. For more details about preset configurations, see[Cluster configuration presets in the Azure portal](../quotas-skus-regions#cluster-configuration-presets-in-the-azure-portal). You can change the preset configuration when creating your cluster by selecting**Compare presets**and choosing a different option.


On the

**Node pools**tab, configure the following settings:Select

**Add node pool**and select**Add a Virtual Machine Scale Set node pool****Name**: Enter a name like*nplinux*.**Mode**: Select**User**.**OS SKU**: Select**Ubuntu Linux**.**Availability zones**: Select**None**.Leave the

**Enable Azure Spot instances**checkbox unchecked.**Node size**: Select**Choose a size**. On the**Select a VM size**page, search for**D2s_v5**, select that VM size, and**Select**.Use the default values for the remaining settings, and select

**Add**.

Select

**Review + create**to run validation on the cluster configuration. After validation completes, select**Create**.It takes a few minutes to create the AKS cluster. When your deployment is complete, navigate to your resource by selecting

**Go to resource**, or by browsing to the AKS cluster resource group and selecting the AKS resource.

## Connect to the cluster

You use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/), to manage Kubernetes clusters. `kubectl`

is already installed if you use Azure Cloud Shell. If you're unfamiliar with the Cloud Shell, review [Overview of Azure Cloud Shell](/en-us/azure/cloud-shell/overview).

If you're using Cloud Shell, open it with the `>_`

button on the top of the Azure portal. If you're using PowerShell locally, connect to Azure via the `Connect-AzAccount`

command. If you're using Azure CLI locally, connect to Azure via the `az login`

command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using

`kubectl get`

to return a list of the cluster nodes.`kubectl get nodes`

The following example output shows the single node created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-nodepool1-31718369-0 Ready agent 6m44s v1.15.10`


## Deploy the application

You use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A Kubernetes manifest file defines a cluster's desired state, like which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, like Rabbit MQ, without persistent storage for production. These containers are used here for simplicity, but we recommend using managed services, like Azure Cosmos DB or Azure Service Bus.

In the Cloud Shell, open an editor and create a file named

`aks-store-quickstart.yaml`

.Paste the following manifest into the editor:

`apiVersion: apps/v1 kind: StatefulSet metadata: name: rabbitmq spec: serviceName: rabbitmq replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 env: - name: AI_SERVICE_URL value: "http://ai-service:5001/" resources: requests: cpu: 1m memory: 1Mi limits: cpu: 2m memory: 20Mi readinessProbe: httpGet: path: /health port: 3002 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3002 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi startupProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 5 periodSeconds: 5 readinessProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 3 livenessProbe: httpGet: path: /health port: 8080 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest:`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

command. Make sure all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the

`store-front`

application. Monitor progress using thecommand with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial series](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges.

In the Azure portal, navigate to your AKS cluster resource group.

Select

**Delete resource group**.Enter the name of the resource group to delete, and then select

**Delete**>**Delete**.Note

The AKS cluster was created with a system-assigned managed identity. This identity is managed by the platform and doesn't require removal.


## Next steps

In this quickstart, you deployed a Kubernetes cluster, and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial series.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-cli -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you learn how to:

- Deploy an AKS cluster using the Azure CLI.
- Run a sample multi-container application with a group of microservices and web front ends that simulate a retail scenario.

Note

This article includes steps to deploy a cluster with default settings for evaluation purposes only. Before you deploy a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more information on access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
[az account set](/en-us/cli/azure/account#az-account-set)command. For more information, see[How to manage Azure subscriptions – Azure CLI](/en-us/cli/azure/manage-azure-subscriptions-azure-cli?tabs=bash#change-the-active-subscription). - Dependent upon your Azure subscription, you might need to request a vCPU quota increase. For more information, see
[Increase VM-family vCPU quotas](/en-us/azure/quotas/per-vm-quota-requests).

## Register resource providers

You might need to register resource providers in your Azure subscription. For example, `Microsoft.ContainerService`

is required.

Run the following command to check the registration status.

```
az provider show --namespace Microsoft.ContainerService --query registrationState
```


If necessary, register the resource provider.

```
az provider register --namespace Microsoft.ContainerService
```


## Define environment variables

Define the following environment variables for use throughout this quickstart.

```
export RANDOM_ID="$(openssl rand -hex 3)"
export MY_RESOURCE_GROUP_NAME="myAKSResourceGroup$RANDOM_ID"
export REGION="westus"
export MY_AKS_CLUSTER_NAME="myAKSCluster$RANDOM_ID"
export MY_DNS_LABEL="mydnslabel$RANDOM_ID"
```


The `RANDOM_ID`

variable's value is a six character alphanumeric value appended to the resource group and cluster name so that the names are unique. Use the `echo`

command to view variable values like `echo $RANDOM_ID`

.

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

Create a resource group using the [az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name $MY_RESOURCE_GROUP_NAME --location $REGION
```


The result looks like the following example.

```
{
"id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myAKSResourceGroup<randomIDValue>",
"location": "westus",
"managedBy": null,
"name": "myAKSResourceGroup<randomIDValue>",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


## Create an AKS cluster

Create an AKS cluster using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a cluster with one node and enables a system-assigned managed identity.

```
az aks create \
--resource-group $MY_RESOURCE_GROUP_NAME \
--name $MY_AKS_CLUSTER_NAME \
--node-count 1 \
--generate-ssh-keys
```


Note

When you create a new cluster, AKS automatically creates a second resource group to store the AKS resources. For more information, see [Why are two resource groups created with AKS?](../faq)

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, use the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials --resource-group $MY_RESOURCE_GROUP_NAME --name $MY_AKS_CLUSTER_NAME`

Verify the connection to your cluster using the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. This command returns a list of the cluster nodes.`kubectl get nodes`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A Kubernetes manifest file defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

- Store front: Web application for customers to view products and place orders.
- Product service: Shows product information.
- Order service: Places orders.
`RabbitMQ`

: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as `RabbitMQ`

, without persistent storage for production. We use it here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Create a file named

*aks-store-quickstart.yaml*and copy in the following manifest.`apiVersion: apps/v1 kind: StatefulSet metadata: name: rabbitmq spec: serviceName: rabbitmq replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 env: - name: AI_SERVICE_URL value: "http://ai-service:5001/" resources: requests: cpu: 1m memory: 1Mi limits: cpu: 2m memory: 20Mi readinessProbe: httpGet: path: /health port: 3002 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3002 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi startupProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 5 periodSeconds: 5 readinessProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 3 livenessProbe: httpGet: path: /health port: 8080 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in Cloud Shell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest.`kubectl apply -f aks-store-quickstart.yaml`


## Test the application

You can validate that the application is running by visiting the public IP address or the application URL.

Get the application URL using the following commands:

```
runtime="5 minutes"
endtime=$(date -ud "$runtime" +%s)
while [[ $(date -u +%s) -le $endtime ]]
do
STATUS=$(kubectl get pods -l app=store-front -o 'jsonpath={..status.conditions[?(@.type=="Ready")].status}')
echo $STATUS
if [ "$STATUS" == 'True' ]
then
export IP_ADDRESS=$(kubectl get service store-front --output 'jsonpath={..status.loadBalancer.ingress[0].ip}')
echo "Service IP Address: $IP_ADDRESS"
break
else
sleep 10
fi
done
```


```
curl $IP_ADDRESS
```


Results:

```
<!doctype html>
<html lang="">
<head>
<meta charset="utf-8">
<meta http-equiv="X-UA-Compatible" content="IE=edge">
<meta name="viewport" content="width=device-width,initial-scale=1">
<link rel="icon" href="/favicon.ico">
<title>store-front</title>
<script defer="defer" src="/js/chunk-vendors.df69ae47.js"></script>
<script defer="defer" src="/js/app.7e8cfbb2.js"></script>
<link href="/css/app.a5dc49f6.css" rel="stylesheet">
</head>
<body>
<div id="app"></div>
</body>
</html>
```


```
echo "You can now visit your web server at $IP_ADDRESS"
```


To view the application website, open a browser and enter the IP address. The page looks like the following example.

## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure billing charges. You can remove the resource group, container service, and all related resources using the [az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name $MY_RESOURCE_GROUP_NAME
```


The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance about how to create full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and do a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-flatcar-deploy-cli -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you learn how to:

- Create an AKS cluster using Flatcar Container Linux for AKS (preview).
- Deploy an AKS cluster using the Azure CLI.
- Run a sample multi-container application with a group of microservices and web front ends that simulate a retail scenario.

Note

This article includes steps to deploy a cluster with default settings for evaluation purposes only. Before you deploy a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more information on access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command. For more information, see`az account set`

[How to manage Azure subscriptions – Azure CLI](/en-us/cli/azure/manage-azure-subscriptions-azure-cli?tabs=bash#change-the-active-subscription). - Dependent upon your Azure subscription, you might need to request a vCPU quota increase. For more information, see
[Increase VM-family vCPU quotas](/en-us/azure/quotas/per-vm-quota-requests).

## Register resource providers

You might need to register resource providers in your Azure subscription. For example, `Microsoft.ContainerService`

is required.

Check the registration status using the [ az provider show](/en-us/cli/azure/provider#az-provider-show) command.

```
az provider show --namespace Microsoft.ContainerService --query registrationState
```


If necessary, register the resource provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command.

```
az provider register --namespace Microsoft.ContainerService
```


## Install `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Flatcar Container Linux requires a minimum of 18.0.0b42**.`az extension update --name aks-preview`


## Register `AKSFlatcarPreview`

feature flag

Register the

`AKSFlatcarPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AKSFlatcarPreview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AKSFlatcarPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Define environment variables

- Define the following environment variables for use throughout this quickstart:

```
export RANDOM_ID="$(openssl rand -hex 3)"
export MY_RESOURCE_GROUP_NAME="myAKSResourceGroup$RANDOM_ID"
export REGION="westus"
export MY_AKS_CLUSTER_NAME="myAKSCluster$RANDOM_ID"
```


The `RANDOM_ID`

variable's value is a six-character alphanumeric value appended to the resource group and cluster name so that the names are unique. Use the `echo`

command to view variable values like `echo $RANDOM_ID`

.

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

- Create a resource group using the
command.`az group create`


```
az group create \
--name $MY_RESOURCE_GROUP_NAME \
--location $REGION
```


Example output:

```
{
"id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myAKSResourceGroup<randomIDValue>",
"location": "westus",
"managedBy": null,
"name": "myAKSResourceGroup<randomIDValue>",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null,
"type": "Microsoft.Resources/resourceGroups"
}
```


## Create an AKS cluster

- Create an AKS cluster using the
command. The following example creates a cluster with one node and enables a system-assigned managed identity:`az aks create`


```
az aks create \
--resource-group $MY_RESOURCE_GROUP_NAME \
--name $MY_AKS_CLUSTER_NAME \
--os-sku flatcar \
--node-count 1 \
--generate-ssh-keys
```


Note

When you create a new cluster, AKS automatically creates a second resource group to store the AKS resources. For more information, see [Why are two resource groups created with AKS?](../faq)

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials \ --resource-group $MY_RESOURCE_GROUP_NAME \ --name $MY_AKS_CLUSTER_NAME`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A Kubernetes manifest file defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

- Store front: Web application for customers to view products and place orders.
- Product service: Shows product information.
- Order service: Places orders.
`RabbitMQ`

: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as `RabbitMQ`

, without persistent storage for production. We use it here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a file named

*aks-store-quickstart.yaml*and copy in the following manifest.`apiVersion: apps/v1 kind: StatefulSet metadata: name: rabbitmq spec: serviceName: rabbitmq replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 env: - name: AI_SERVICE_URL value: "http://ai-service:5001/" resources: requests: cpu: 1m memory: 1Mi limits: cpu: 2m memory: 20Mi readinessProbe: httpGet: path: /health port: 3002 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3002 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi startupProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 5 periodSeconds: 5 readinessProbe: httpGet: path: /health port: 8080 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 3 livenessProbe: httpGet: path: /health port: 8080 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3 --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in Cloud Shell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

command. Make sure all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the

`store-front`

application. Monitor progress using thecommand with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure billing charges.

Remove the resource group, container service, and all related resources using the

command.`az group delete`

`az group delete --name $MY_RESOURCE_GROUP_NAME`

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity so you don't need to manually remove it.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance about how to create full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and do a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-powershell -->

# Deploy a Windows Server container on an Azure Kubernetes Service (AKS) cluster using PowerShell

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this article, you use Azure PowerShell to deploy an AKS cluster that runs Windows Server containers. You also deploy an ASP.NET sample application in a Windows Server container to the cluster.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. For ease of use, try the PowerShell environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Quickstart for Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you want to use PowerShell locally, then install the

[Az PowerShell](/en-us/powershell/azure/new-azureps-module-az)module and connect to your Azure account using the[Connect-AzAccount](/en-us/powershell/module/az.accounts/Connect-AzAccount)cmdlet. Make sure that you run the commands with administrative privileges. For more information, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps).Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).If you have more than one Azure subscription, set the subscription that you wish to use for the quickstart by calling the

[Set-AzContext](/en-us/powershell/module/az.accounts/set-azcontext)cmdlet. For more information, see[Manage Azure subscriptions with Azure PowerShell](/en-us/powershell/azure/manage-subscriptions-azureps#change-the-active-subscription).If you're using osSku

`Windows2025`

, you need to install the`aks-preview`

extension and register the preview flag.Specifying the

`OsSKU`

parameter requires PowerShell Az module version 9.2.0 or higher.

### Install the `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

- Install the
`aks-preview`

Azure CLI extension using thecommand.`az extension add`


```
az extension add --name aks-preview
```


- Update to the latest version of the extension using the
command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b40**.

```
az extension update --name aks-preview
```


### Register the `AksWindows2025Preview`

feature flag

- Register the
`AksWindows2025Preview`

feature flag using the [`az feature register`

][az-feature-register] command.

```
az feature register --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


- Verify the registration status using the [
`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.

```
az feature show --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're asked to specify a location. This location is where resource group metadata is stored and where your resources run in Azure if you don't specify another region during resource creation.

Create a resource group using the

cmdlet. The following example creates a resource group named`New-AzResourceGroup`

*myResourceGroup*in the*eastus*region.`New-AzResourceGroup -Name myResourceGroup -Location eastus`

The following example output shows that the resource group was created successfully:

`ResourceGroupName : myResourceGroup Location : eastus ProvisioningState : Succeeded Tags : ResourceId : /subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/myResourceGroup`


## Create an AKS cluster

In this section, we create an AKS cluster with the following configuration:

- The cluster is configured with two nodes to ensure it operates reliably. A
[node](../concepts-clusters-workloads#nodes)is an Azure virtual machine (VM) that runs the Kubernetes node components and container runtime. - The
`-WindowsProfileAdminUserName`

and`-WindowsProfileAdminUserPassword`

parameters set the administrator credentials for any Windows Server nodes on the cluster and must meet the[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference). - The node pool uses
`VirtualMachineScaleSets`

.

Use the following steps to create the AKS cluster with Azure PowerShell:

Create the administrator credentials for your Windows Server containers using the following command. This command prompts you to enter a

`WindowsProfileAdminUserName`

and`WindowsProfileAdminUserPassword`

. The password must be a minimum of 14 characters and meet the[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).`$AdminCreds = Get-Credential ` -Message 'Please create the administrator credentials for your Windows Server containers'`

Create your cluster using the

cmdlet and specify the`New-AzAksCluster`

`WindowsProfileAdminUserName`

and`WindowsProfileAdminUserPassword`

parameters.`New-AzAksCluster -ResourceGroupName myResourceGroup ` -Name myAKSCluster ` -NodeCount 2 ` -NetworkPlugin azure ` -NodeVmSetType VirtualMachineScaleSets ` -WindowsProfileAdminUserName $AdminCreds.UserName ` -WindowsProfileAdminUserPassword $secureString ` -GenerateSshKey`

After a few minutes, the command completes and returns JSON-formatted information about the cluster. Occasionally, the cluster can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

If you get a password validation error, and the password that you set meets the length and complexity requirements, try creating your resource group in another region. Then try creating the cluster with the new resource group.

If you don't specify an administrator username and password when creating the node pool, the username is set to

*azureuser*and the password is set to a random value. For more information, see the[Windows Server FAQ](../windows-faq).The administrator username can't be changed, but you can change the administrator password that your AKS cluster uses for Windows Server nodes using

`az aks update`

. For more information, see the[Windows Server FAQ](../windows-faq).To run an AKS cluster that supports node pools for Windows Server containers, your cluster needs to use a network policy that uses

[Azure CNI (advanced)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md)network plugin. The`-NetworkPlugin azure`

parameter specifies Azure CNI.

## Add a node pool

By default, an AKS cluster is created with a node pool that can run Linux containers. You must add another node pool that can run Windows Server containers alongside the Linux node pool.

To create a Windows node pool, you need to specify a supported `OsType`

and `OsSku`

. Use the information in the following table to determine which is appropriate for your cluster:

`OsType` |
`OsSku` |
Default | Supported K8s versions | Details |
|---|---|---|---|---|
`windows` |
`Windows2025` |
Currently in preview. Not default. | 1.32+ | Updated defaults: containerd 2.0, Generation 2 image is used by default. |
`windows` |
`Windows2022` |
Default in K8s 1.25-1.35 | Not available in K8s 1.36+ | Retires in March 2027. Updated defaults: FIPS is enabled by default. |
`windows` |
`Windows2019` |
Default in K8s 1.24 and below | Not available in K8s 1.33+ | Retires in March 2026. |

Windows Server 2022 is the default operating system for Kubernetes versions 1.25-1.35. Windows Server 2019 is the default OS for earlier versions. If you don't specify a particular OS SKU, Azure creates the new node pool with the default SKU for the version of Kubernetes used by the cluster.

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

Add a Windows Server node pool using the

cmdlet. The following command creates a new node pool named`New-AzAksNodePool`

*npwin*and adds it to*myAKSCluster*. The command also uses the default subnet in the default virtual network created when running`New-AzAksCluster`

:`New-AzAksNodePool -ResourceGroupName myResourceGroup ` -ClusterName myAKSCluster ` -VmSetType VirtualMachineScaleSets ` -OsType Windows ` -OsSKU Windows2022 ` -Name npwin`


## Connect to the cluster

You use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client, to manage your Kubernetes clusters. If you use Azure Cloud Shell, `kubectl`

is already installed. If you want to install `kubectl`

locally, you can use the `Install-AzAzAksCliTool`

cmdlet.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecmdlet. This command downloads credentials and configures the Kubernetes CLI to use them.`Import-AzAksCredential`

`Import-AzAksCredential -ResourceGroupName myResourceGroup -Name myAKSCluster`

Verify the connection to your cluster using the

command, which returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows all the nodes in the cluster. Make sure the status of all nodes is

**Ready**:`NAME STATUS ROLES AGE VERSION aks-nodepool1-20786768-vmss000000 Ready agent 22h v1.27.7 aks-nodepool1-20786768-vmss000001 Ready agent 22h v1.27.7 aksnpwin000000 Ready agent 21h v1.27.7`


## Deploy the application

A Kubernetes manifest file defines a desired state for the cluster, such as what container images to run. In this article, you use a manifest to create all objects needed to run the ASP.NET sample application in a Windows Server container. This manifest includes a [Kubernetes deployment](../concepts-clusters-workloads#deployments-and-yaml-manifests) for the ASP.NET sample application and an external [Kubernetes service](../concepts-network-services) to access the application from the internet.

The ASP.NET sample application is provided as part of the [.NET Framework Samples](https://hub.docker.com/_/microsoft-dotnet-framework-samples/) and runs in a Windows Server container. AKS requires Windows Server containers to be based on images of *Windows Server 2019* or greater. The Kubernetes manifest file must also define a [node selector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) to tell your AKS cluster to run your ASP.NET sample application's pod on a node that can run Windows Server containers.

Create a file named

`sample.yaml`

and copy in the following YAML definition:`apiVersion: apps/v1 kind: Deployment metadata: name: sample labels: app: sample spec: replicas: 1 template: metadata: name: sample labels: app: sample spec: nodeSelector: "kubernetes.io/os": windows containers: - name: sample image: mcr.microsoft.com/dotnet/framework/samples:aspnetapp resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 selector: matchLabels: app: sample --- apiVersion: v1 kind: Service metadata: name: sample spec: type: LoadBalancer ports: - protocol: TCP port: 80 selector: app: sample`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f sample.yaml`

The following example output shows the deployment and service created successfully:

`deployment.apps/sample created service/sample created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete. Occasionally, the service can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

Check the status of the deployed pods using the

command. Make all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service sample --watch`

Initially, the output shows the

*EXTERNAL-IP*for the sample service as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE sample LoadBalancer 10.0.37.27 <pending> 80:30572/TCP 6s`

When the

*EXTERNAL-IP*address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`sample LoadBalancer 10.0.37.27 52.179.23.131 80:30572/TCP 2m`

See the sample app in action by opening a web browser to the external IP address of your service.


## Delete resources

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), then delete your cluster to avoid incurring Azure charges.

Remove the resource group, container service, and all related resources using the

cmdlet.`Remove-AzResourceGroup`

`Remove-AzResourceGroup -Name myResourceGroup`

Note

The AKS cluster was created with system-assigned managed identity (default identity option used in this quickstart). The Azure platform manages this identity, so it doesn't require removal.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed an ASP.NET sample application in a Windows Server container to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS, and to walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-deploy-rm-template -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Deploy an AKS cluster using an Azure Resource Manager template.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

An [Azure Resource Manager template](/en-us/azure/azure-resource-manager/templates/overview) is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This article assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. Make sure that the identity you use to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine, you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

After you deploy the cluster from the template, you can use either Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


This article requires Azure CLI version 2.0.64 or later. If you're using Azure Cloud Shell, the latest version is already installed there.

### Create an SSH key pair

To create an AKS cluster using an ARM template, you provide an SSH public key. If you need this resource, follow the steps in this section. Otherwise, skip to the [Review the template](#review-the-template) section.

To access AKS nodes, you connect using an SSH key pair (public and private). To create an SSH key pair:

Go to

[https://shell.azure.com](https://shell.azure.com)to open Cloud Shell in your browser.Create an SSH key pair using the

[az sshkey create](/en-us/cli/azure/sshkey#az-sshkey-create)command or the`ssh-keygen`

command.`# Create an SSH key pair using Azure CLI az sshkey create --name "mySSHKey" --resource-group "myResourceGroup" # or # Create an SSH key pair using ssh-keygen ssh-keygen -t rsa -b 4096`

To deploy the template, you must provide the public key from the SSH pair. To retrieve the public key, call

[az sshkey show](/en-us/cli/azure/sshkey#az-sshkey-show):`az sshkey show --name "mySSHKey" --resource-group "myResourceGroup" --query "publicKey"`


By default, the SSH key files are created in the *~/.ssh* directory. Running the `az sshkey create`

or `ssh-keygen`

command will overwrite any existing SSH key pair with the same name.

For more information about creating SSH keys, see [Create and manage SSH keys for authentication in Azure](/en-us/azure/virtual-machines/linux/create-ssh-keys-detailed).

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/aks/).

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"metadata": {
"_generator": {
"name": "bicep",
"version": "0.26.170.59819",
"templateHash": "14823542069333410776"
}
},
"parameters": {
"clusterName": {
"type": "string",
"defaultValue": "aks101cluster",
"metadata": {
"description": "The name of the Managed Cluster resource."
}
},
"location": {
"type": "string",
"defaultValue": "[resourceGroup().location]",
"metadata": {
"description": "The location of the Managed Cluster resource."
}
},
"dnsPrefix": {
"type": "string",
"metadata": {
"description": "Optional DNS prefix to use with hosted Kubernetes API server FQDN."
}
},
"osDiskSizeGB": {
"type": "int",
"defaultValue": 0,
"minValue": 0,
"maxValue": 1023,
"metadata": {
"description": "Disk size (in GB) to provision for each of the agent pool nodes. This value ranges from 0 to 1023. Specifying 0 will apply the default disk size for that agentVMSize."
}
},
"agentCount": {
"type": "int",
"defaultValue": 3,
"minValue": 1,
"maxValue": 50,
"metadata": {
"description": "The number of nodes for the cluster."
}
},
"agentVMSize": {
"type": "string",
"defaultValue": "standard_d2s_v3",
"metadata": {
"description": "The size of the Virtual Machine."
}
},
"linuxAdminUsername": {
"type": "string",
"metadata": {
"description": "User name for the Linux Virtual Machines."
}
},
"sshRSAPublicKey": {
"type": "string",
"metadata": {
"description": "Configure all linux machines with the SSH RSA public key string. Your key should include three parts, for example 'ssh-rsa AAAAB...snip...UcyupgH azureuser@linuxvm'"
}
}
},
"resources": [
{
"type": "Microsoft.ContainerService/managedClusters",
"apiVersion": "2024-02-01",
"name": "[parameters('clusterName')]",
"location": "[parameters('location')]",
"identity": {
"type": "SystemAssigned"
},
"properties": {
"dnsPrefix": "[parameters('dnsPrefix')]",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": "[parameters('osDiskSizeGB')]",
"count": "[parameters('agentCount')]",
"vmSize": "[parameters('agentVMSize')]",
"osType": "Linux",
"mode": "System"
}
],
"linuxProfile": {
"adminUsername": "[parameters('linuxAdminUsername')]",
"ssh": {
"publicKeys": [
{
"keyData": "[parameters('sshRSAPublicKey')]"
}
]
}
}
}
}
],
"outputs": {
"controlPlaneFQDN": {
"type": "string",
"value": "[reference(resourceId('Microsoft.ContainerService/managedClusters', parameters('clusterName')), '2024-02-01').fqdn]"
}
}
}
```


The resource type defined in the ARM template is [ Microsoft.ContainerService/managedClusters](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template).

For more AKS samples, see the [AKS quickstart templates](https://azure.microsoft.com/resources/templates/?term=Azure+Kubernetes+Service) site.

## Deploy the template

Select

**Deploy to Azure**to sign in and open a template.On the

**Basics**page, leave the default values for the*OS Disk Size GB*,*Agent Count*,*Agent VM Size*, and*OS Type*, and configure the following template parameters:**Subscription**: Select an Azure subscription.**Resource group**: Select**Create new**. Enter a unique name for the resource group, such as*myResourceGroup*, then select**OK**.**Location**: Select a location, such as**East US**.**Cluster name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**DNS prefix**: Enter a unique DNS prefix for your cluster, such as*myakscluster*.**Linux Admin Username**: Enter a username to connect using SSH, such as*azureuser*.**SSH public key source**: Select**Use existing public key**.**Key pair name**: Copy and paste the*public*part of your SSH key pair (by default, the contents of*~/.ssh/id_rsa.pub*).

Select

**Review + Create**>**Create**.

It takes a few minutes to create the AKS cluster. Wait for the cluster to be successfully deployed before you move on to the next step.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/).

If you use Azure Cloud Shell, `kubectl`

is already installed. To install and run `kubectl`

locally, call the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using the[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

[kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. This command returns a list of the cluster nodes.`kubectl get nodes`

The following example output shows the three nodes created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-agentpool-27442051-vmss000000 Ready agent 10m v1.27.7 aks-agentpool-27442051-vmss000001 Ready agent 10m v1.27.7 aks-agentpool-27442051-vmss000002 Ready agent 11m v1.27.7`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Create a file named

`aks-store-quickstart.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: rabbitmq spec: replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 resources: requests: cpu: 1m memory: 1Mi limits: cpu: 1m memory: 7Mi --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify the name of your YAML manifest.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make all pods are`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges.

Remove the resource group, container service, and all related resources by calling the [az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name myResourceGroup --yes --no-wait
```


Note

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-windows-container-deploy-cli -->

# Deploy a Windows Server container on an Azure Kubernetes Service (AKS) cluster using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this article, you use Azure CLI to deploy an AKS cluster that runs Windows Server containers. You also deploy an ASP.NET sample application in a Windows Server container to the cluster.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.0.64 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- Make sure that the identity you're using to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see
[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command. For more information, see`az account set`

[How to manage Azure subscriptions – Azure CLI](/en-us/cli/azure/manage-azure-subscriptions-azure-cli?tabs=bash#change-the-active-subscription). - If you're using
`--os-sku Windows2025`

, you need to install the`aks-preview`

extension and register the preview flag. The minimum version is 18.0.0b40.

### Install the `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

- Install the
`aks-preview`

Azure CLI extension using thecommand.`az extension add`


```
az extension add --name aks-preview
```


- Update to the latest version of the extension using the
command.`az extension update`

**Windows Server 2025 requires a minimum of 18.0.0b40**.

```
az extension update --name aks-preview
```


### Register the `AksWindows2025Preview`

feature flag

- Register the
`AksWindows2025Preview`

feature flag using the [`az feature register`

][az-feature-register] command.

```
az feature register --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


- Verify the registration status using the [
`az feature show`

][az-feature-show] command. It takes a few minutes for the status to show*Registered*.

```
az feature show --name AksWindows2025Preview --namespace Microsoft.ContainerService
```


When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using the [`az provider register`

][az-provider-register] command.`az provider register --namespace Microsoft.ContainerService`


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're asked to specify a location. This location is where resource group metadata is stored and where your resources run in Azure if you don't specify another region during resource creation.

Create a resource group using the

command. The following example creates a resource group named`az group create`

*myResourceGroup*in the*WestUS2*location.`export RANDOM_SUFFIX=$(openssl rand -hex 3) export REGION="canadacentral" export MY_RESOURCE_GROUP_NAME="myAKSResourceGroup$RANDOM_SUFFIX" az group create --name $MY_RESOURCE_GROUP_NAME --location $REGION`

Results:

`{ "id": "/subscriptions/xxxxx-xxxxx-xxxxx-xxxxx/resourceGroups/myResourceGroupxxxxx", "location": "WestUS2", "managedBy": null, "name": "myResourceGroupxxxxx", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`


## Create an AKS cluster

In this section, we create an AKS cluster with the following configuration:

- The cluster is configured with two nodes to ensure it operates reliably. A
[node](../concepts-clusters-workloads#nodes)is an Azure virtual machine (VM) that runs the Kubernetes node components and container runtime. - The
`--windows-admin-password`

and`--windows-admin-username`

parameters set the administrator credentials for any Windows Server nodes on the cluster and must meet[Windows Server password requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference). - The node pool uses
`VirtualMachineScaleSets`

.

Use the following steps to create the AKS cluster with Azure CLI:

Create a username to use as administrator credentials for the Windows Server nodes on your cluster.

`export WINDOWS_USERNAME="winadmin"`

Create a password for the administrator username you created in the previous step. The password must be a minimum of 14 characters and meet the

[Windows Server password complexity requirements](/en-us/windows/security/threat-protection/security-policy-settings/password-must-meet-complexity-requirements#reference).`export WINDOWS_PASSWORD=$(echo "P@ssw0rd$(openssl rand -base64 10 | tr -dc 'A-Za-z0-9!@#$%^&*()' | cut -c1-6)")`

Create your cluster using the

command and specify the`az aks create`

`--windows-admin-username`

and`--windows-admin-password`

parameters. The following example command creates a cluster using the values from`WINDOWS_USERNAME`

and`WINDOWS_PASSWORD`

you set in the previous commands. A random suffix is appended to the cluster name for uniqueness.`export MY_AKS_CLUSTER="myAKSCluster$RANDOM_SUFFIX" az aks create \ --resource-group $MY_RESOURCE_GROUP_NAME \ --name $MY_AKS_CLUSTER \ --node-count 2 \ --enable-addons monitoring \ --generate-ssh-keys \ --windows-admin-username $WINDOWS_USERNAME \ --windows-admin-password $WINDOWS_PASSWORD \ --vm-set-type VirtualMachineScaleSets \ --network-plugin azure`

After a few minutes, the command completes and returns JSON-formatted information about the cluster. Occasionally, the cluster can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

If you get a password validation error, and the password that you set meets the length and complexity requirements, try creating your resource group in another region. Then try creating the cluster with the new resource group.

If you don't specify an administrator username and password when creating the node pool, the username is set to

*azureuser*and the password is set to a random value. For more information, see the[Windows Server FAQ](../windows-faq)You can't change the administrator username, but you can change the administrator password that your AKS cluster uses for Windows Server nodes using

`az aks update`

. For more information, see[Windows Server FAQ](../windows-faq).To run an AKS cluster that supports node pools for Windows Server containers, your cluster needs to use a network policy that uses

[Azure CNI (advanced)](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md)network plugin. The`--network-plugin azure`

parameter specifies Azure CNI.

## Add a node pool

By default, all AKS clusters are created with a node pool that can run Linux containers. You must add a Windows node pool that can run Windows Server containers alongside the Linux node pool. To check if you have a Windows node pool in your cluster, you can view the nodes on your cluster using the `kubectl get nodes -o wide`

command.

To create a Windows node pool, you need to specify a supported `OsType`

and `OsSku`

. Use the information in the following table to determine which is appropriate for your cluster:

`OsType` |
`OsSku` |
Default | Supported K8s versions | Details |
|---|---|---|---|---|
`windows` |
`Windows2025` |
Currently in preview. Not default. | 1.32+ | Updated defaults: containerd 2.0, Generation 2 image is used by default. |
`windows` |
`Windows2022` |
Default in K8s 1.25-1.35 | Not available in K8s 1.36+ | Retires in March 2027. Updated defaults: FIPS is enabled by default. |
`windows` |
`Windows2019` |
Default in K8s 1.24 and below | Not available in K8s 1.33+ | Retires in March 2026. |

Windows Server 2022 is the default operating system for Kubernetes versions 1.25-1.35. Windows Server 2019 is the default OS for earlier versions. If you don't specify a particular OS SKU, Azure creates the new node pool with the default SKU for the version of Kubernetes used by the cluster.

Note

[Windows Server 2019 retires on March 1, 2026](https://github.com/Azure/AKS/issues/4091). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2019 on any Kubernetes version. All existing node pools with Windows Server 2019 will be unsupported. Windows Server 2019 is not supported in Kubernetes version 1.33 and above. Starting on April 1, 2027, AKS will remove all existing node images for Windows Server 2019, meaning that scaling operations will fail.[Windows Server 2022 retires on March 15, 2027](https://github.com/Azure/AKS/issues/4168). After that date, AKS will no longer produce new node images or provide security patches. After that date, you will not be able to create new node pools with Windows Server 2022 on any Kubernetes version. All existing node pools with Windows Server 2022 will be unsupported. Windows Server 2022 is not supported in Kubernetes version 1.36 and above. Starting on April 1, 2028, AKS will remove all existing node images for Windows Server 2022, meaning that scaling operations will fail.

For more information, see [AKS release notes](https://github.com/Azure/AKS/releases). To stay up to date on the latest Windows Server OS versions and learn more about our roadmap of what's planned for support on AKS, see our [AKS public roadmap](https://github.com/azure/aks/projects/1).

Add a Windows node pool using the

command with a specified`az aks nodepool add`

`OsType`

and`OsSku`

. If you don't specify a particular OS SKU, Azure creates the new node pool with the default SKU for the version of Kubernetes used by the cluster.`az aks nodepool add \ --resource-group $MY_RESOURCE_GROUP_NAME \ --cluster-name $MY_AKS_CLUSTER \ --os-type Windows \ --os-sku Windows2022 \ --name npwin \ --node-count 1`

This command creates a new node pool named

*npwin*and adds it to*myAKSCluster*. The command also uses the default subnet in the default virtual network created when running`az aks create`

.

## Connect to the cluster

You use [kubectl](https://kubernetes.io/docs/reference/kubectl/), the Kubernetes command-line client, to manage your Kubernetes clusters. If you use Azure Cloud Shell, `kubectl`

is already installed. If you want to install and run `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group $MY_RESOURCE_GROUP_NAME --name $MY_AKS_CLUSTER`

Verify the connection to your cluster using the

command, which returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes -o wide`

The following example output shows all nodes in the cluster. Make sure the status of all nodes is

*Ready*:`NAME STATUS ROLES AGE VERSION INTERNAL-IP EXTERNAL-IP OS-IMAGE KERNEL-VERSION CONTAINER-RUNTIME aks-nodepool1-20786768-vmss000000 Ready agent 22h v1.27.7 10.224.0.4 <none> Ubuntu 22.04.3 LTS 5.15.0-1052-azure containerd://1.7.5-1 aks-nodepool1-20786768-vmss000001 Ready agent 22h v1.27.7 10.224.0.33 <none> Ubuntu 22.04.3 LTS 5.15.0-1052-azure containerd://1.7.5-1 aksnpwin000000 Ready agent 20h v1.27.7 10.224.0.62 <none> Windows Server 2022 Datacenter 10.0.20348.2159 containerd://1.6.21+azure`

Note

The container runtime for each node pool is shown under

*CONTAINER-RUNTIME*. The container runtime values begin with`containerd://`

, which means that they each use`containerd`

for the container runtime.

## Deploy the application

A Kubernetes manifest file defines a desired state for the cluster, such as what container images to run. In this article, you use a manifest to create all objects needed to run the ASP.NET sample application in a Windows Server container. This manifest includes a [Kubernetes deployment](../concepts-clusters-workloads#deployments-and-yaml-manifests) for the ASP.NET sample application and an external [Kubernetes service](../concepts-network-services) to access the application from the internet.

The ASP.NET sample application is provided as part of the [.NET Framework Samples](https://hub.docker.com/_/microsoft-dotnet-framework-samples/) and runs in a Windows Server container. AKS requires Windows Server containers to be based on images of *Windows Server 2019* or greater. The Kubernetes manifest file must also define a [node selector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/) to tell your AKS cluster to run your ASP.NET sample application's pod on a node that can run Windows Server containers.

Create a file named

`sample.yaml`

and copy in the following YAML definition:`apiVersion: apps/v1 kind: Deployment metadata: name: sample labels: app: sample spec: replicas: 1 template: metadata: name: sample labels: app: sample spec: nodeSelector: "kubernetes.io/os": windows containers: - name: sample image: mcr.microsoft.com/dotnet/framework/samples:aspnetapp resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 selector: matchLabels: app: sample --- apiVersion: v1 kind: Service metadata: name: sample spec: type: LoadBalancer ports: - protocol: TCP port: 80 selector: app: sample`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f sample.yaml`

The following example output shows the deployment and service created successfully:

`{ "deployment.apps/sample": "created", "service/sample": "created" }`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete. Occasionally, the service can take longer than a few minutes to provision. Allow up to 10 minutes for provisioning.

Check the status of the deployed pods using the

command. Make sure all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`while true; do export EXTERNAL_IP=$(kubectl get service sample -o jsonpath="{.status.loadBalancer.ingress[0].ip}" 2>/dev/null) if [[ -n "$EXTERNAL_IP" && "$EXTERNAL_IP" != "<pending>" ]]; then kubectl get service sample break fi echo "Still waiting for external IP assignment..." sleep 5 done`

Initially, the output shows the

*EXTERNAL-IP*for the sample service as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE sample LoadBalancer xx.xx.xx.xx pending xx:xxxx/TCP 2m`

When the

*EXTERNAL-IP*address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`{ "NAME": "sample", "TYPE": "LoadBalancer", "CLUSTER-IP": "10.0.37.27", "EXTERNAL-IP": "52.179.23.131", "PORT(S)": "80:30572/TCP", "AGE": "2m" }`

See the sample app in action by opening a web browser to the external IP address of your service after a few minutes.


## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed an ASP.NET sample application in a Windows Server container to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS, and to walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-flatcar-deploy-arm-template -->

# Quickstart: Deploy an Azure Kubernetes Service (AKS) cluster with Flatcar Container Linux for AKS (preview) using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) is a managed Kubernetes service that lets you quickly deploy and manage clusters. In this quickstart, you:

- Create an AKS cluster using Flatcar Container Linux for AKS (preview).
- Deploy an AKS cluster using an Azure Resource Manager template.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

An [Azure Resource Manager template](/en-us/azure/azure-resource-manager/templates/overview) is a JavaScript Object Notation (JSON) file that defines the infrastructure and configuration for your project. The template uses declarative syntax. You describe your intended deployment without writing the sequence of programming commands to create the deployment.

Note

To get started with quickly provisioning an AKS cluster, this article includes steps to deploy a cluster with default settings for evaluation purposes only. Before deploying a production-ready cluster, we recommend that you familiarize yourself with our [baseline reference architecture](/en-us/azure/architecture/reference-architectures/containers/aks/baseline-aks?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json) to consider how it aligns with your business requirements.

## Before you begin

This article assumes a basic understanding of Kubernetes concepts. For more information, see [Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads).

-
If you don't have an Azure account, create a

[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. Make sure that the identity you use to create your cluster has the appropriate minimum permissions. For more details on access and identity for AKS, see

[Access and identity options for Azure Kubernetes Service (AKS)](../concepts-identity).To deploy an ARM template, you need write access on the resources you're deploying and access to all operations on the

`Microsoft.Resources/deployments`

resource type. For example, to deploy a virtual machine, you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

After you deploy the cluster from the template, you can use either Azure CLI or Azure PowerShell to connect to the cluster and deploy the sample application.

## Register resource providers

You might need to register resource providers in your Azure subscription. For example, `Microsoft.ContainerService`

is required.

Check the registration status using the [ az provider show](/en-us/cli/azure/provider#az-provider-show) command.

```
az provider show --namespace Microsoft.ContainerService --query registrationState
```


If necessary, register the resource provider using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command.

```
az provider register --namespace Microsoft.ContainerService
```


## Install `aks-preview`

extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

Azure CLI extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension using the

command.`az extension update`

**Flatcar Container Linux requires a minimum of 18.0.0b42**.`az extension update --name aks-preview`


## Register `AKSFlatcarPreview`

feature flag

Register the

`AKSFlatcarPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AKSFlatcarPreview"`

Verify the registration status using the

command. It takes a few minutes for the status to show`az feature show`

*Registered*.`az feature show --namespace Microsoft.ContainerService --name AKSFlatcarPreview`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


### Create an SSH key pair

To create an AKS cluster using an ARM template, you provide an SSH public key. If you need this resource, follow the steps in this section. Otherwise, skip to the [Review the template](#review-the-template) section.

To access AKS nodes, you connect using an SSH key pair (public and private). To create an SSH key pair:

Go to

[https://shell.azure.com](https://shell.azure.com)to open Cloud Shell in your browser.Create a resource group using the

[az group create](/en-us/cli/azure/group#az-group-create)command.`az group create \ --name myResourceGroup \ --location eastus`

Create an SSH key pair using the

[az sshkey create](/en-us/cli/azure/sshkey#az-sshkey-create)command or the`ssh-keygen`

command.`az sshkey create --name mySSHKey --resource-group myResourceGroup`

Or create an SSH key pair using ssh-keygen

`ssh-keygen -t rsa -b 4096`

To deploy the template, you must provide the public key from the SSH pair. Retrieve the public key using the

command.`az sshkey show`

`az sshkey show --name mySSHKey --resource-group myResourceGroup --query publicKey`

By default, the SSH key files are created in the

*~/.ssh*directory. Running the`az sshkey create`

or`ssh-keygen`

command overwrites any existing SSH key pair with the same name.For more information about creating SSH keys, see

[Create and manage SSH keys for authentication in Azure](/en-us/azure/virtual-machines/linux/create-ssh-keys-detailed).

## Review the template

The template used in this quickstart is from [Azure Quickstart Templates](https://azure.microsoft.com/resources/templates/aks/).

```
{
"$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#",
"contentVersion": "1.0.0.0",
"metadata": {
"_generator": {
"name": "bicep",
"version": "0.26.170.59819",
"templateHash": "14823542069333410776"
}
},
"parameters": {
"clusterName": {
"type": "string",
"defaultValue": "aks101cluster",
"metadata": {
"description": "The name of the Managed Cluster resource."
}
},
"location": {
"type": "string",
"defaultValue": "[resourceGroup().location]",
"metadata": {
"description": "The location of the Managed Cluster resource."
}
},
"dnsPrefix": {
"type": "string",
"metadata": {
"description": "Optional DNS prefix to use with hosted Kubernetes API server FQDN."
}
},
"osDiskSizeGB": {
"type": "int",
"defaultValue": 0,
"minValue": 0,
"maxValue": 1023,
"metadata": {
"description": "Disk size (in GB) to provision for each of the agent pool nodes. This value ranges from 0 to 1023. Specifying 0 will apply the default disk size for that agentVMSize."
}
},
"agentCount": {
"type": "int",
"defaultValue": 3,
"minValue": 1,
"maxValue": 50,
"metadata": {
"description": "The number of nodes for the cluster."
}
},
"agentVMSize": {
"type": "string",
"defaultValue": "standard_d2s_v3",
"metadata": {
"description": "The size of the Virtual Machine."
}
},
"linuxAdminUsername": {
"type": "string",
"metadata": {
"description": "User name for the Linux Virtual Machines."
}
},
"sshRSAPublicKey": {
"type": "string",
"metadata": {
"description": "Configure all linux machines with the SSH RSA public key string. Your key should include three parts, for example 'ssh-rsa AAAAB...snip...UcyupgH azureuser@linuxvm'"
}
}
},
"resources": [
{
"type": "Microsoft.ContainerService/managedClusters",
"apiVersion": "2024-02-01",
"name": "[parameters('clusterName')]",
"location": "[parameters('location')]",
"identity": {
"type": "SystemAssigned"
},
"properties": {
"dnsPrefix": "[parameters('dnsPrefix')]",
"agentPoolProfiles": [
{
"name": "agentpool",
"osDiskSizeGB": "[parameters('osDiskSizeGB')]",
"count": "[parameters('agentCount')]",
"vmSize": "[parameters('agentVMSize')]",
"osType": "Linux",
"mode": "System"
}
],
"linuxProfile": {
"adminUsername": "[parameters('linuxAdminUsername')]",
"ssh": {
"publicKeys": [
{
"keyData": "[parameters('sshRSAPublicKey')]"
}
]
}
}
}
}
],
"outputs": {
"controlPlaneFQDN": {
"type": "string",
"value": "[reference(resourceId('Microsoft.ContainerService/managedClusters', parameters('clusterName')), '2024-02-01').fqdn]"
}
}
}
```


The resource type defined in the ARM template is [ Microsoft.ContainerService/managedClusters](/en-us/azure/templates/microsoft.containerservice/managedclusters?pivots=deployment-language-arm-template).

For more AKS samples, see the [AKS quickstart templates](https://azure.microsoft.com/resources/templates/?term=Azure+Kubernetes+Service) site.

## Deploy the template

Select

**Deploy to Azure**to sign in and open a template.On the

**Basics**page, leave the default values for the*OS Disk Size GB*,*Agent Count*,*Agent VM Size*, and*OS Type*, and configure the following template parameters:**Subscription**: Select an Azure subscription.**Resource group**: Select**Create new**. Enter a unique name for the resource group, such as*myResourceGroup*, then select**OK**.**OS SKU**: Specify**flatcar**, if you do not update OS SKU, the default will be`Ubuntu`

.**Location**: Select a location, such as**East US**.**Cluster name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**DNS prefix**: Enter a unique DNS prefix for your cluster, such as*myakscluster*.**Linux Admin Username**: Enter a username to connect using SSH, such as*azureuser*.**SSH public key source**: Select**Use existing public key**.**Key pair name**: Copy and paste the*public*part of your SSH key pair (by default, the contents of*~/.ssh/id_rsa.pub*).

Select

**Review + Create**>**Create**.

It takes a few minutes to create the AKS cluster. Wait for the cluster to be successfully deployed before you move on to the next step.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/).

If you use Azure Cloud Shell, `kubectl`

is already installed. To install and run `kubectl`

locally, use the [ az aks install-cli](/en-us/cli/azure/aks#az_aks_install_cli) command.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials \ --resource-group myResourceGroup \ --name myAKSCluster`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the three nodes created in the previous steps. Make sure the node status is

*Ready*:`NAME STATUS ROLES AGE VERSION aks-agentpool-38955149-vmss000000 Ready <none> 5m53s v1.32.7 aks-agentpool-38955149-vmss000001 Ready <none> 6m31s v1.32.7 aks-agentpool-238955149-vmss000002 Ready <none> 6m35s v1.32.7`


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a file named

`aks-store-quickstart.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: rabbitmq spec: replicas: 1 selector: matchLabels: app: rabbitmq template: metadata: labels: app: rabbitmq spec: nodeSelector: "kubernetes.io/os": linux containers: - name: rabbitmq image: mcr.microsoft.com/mirror/docker/library/rabbitmq:3.10-management-alpine ports: - containerPort: 5672 name: rabbitmq-amqp - containerPort: 15672 name: rabbitmq-http env: - name: RABBITMQ_DEFAULT_USER value: "username" - name: RABBITMQ_DEFAULT_PASS value: "password" resources: requests: cpu: 10m memory: 128Mi limits: cpu: 250m memory: 256Mi volumeMounts: - name: rabbitmq-enabled-plugins mountPath: /etc/rabbitmq/enabled_plugins subPath: enabled_plugins volumes: - name: rabbitmq-enabled-plugins configMap: name: rabbitmq-enabled-plugins items: - key: rabbitmq_enabled_plugins path: enabled_plugins --- apiVersion: v1 data: rabbitmq_enabled_plugins: | [rabbitmq_management,rabbitmq_prometheus,rabbitmq_amqp1_0]. kind: ConfigMap metadata: name: rabbitmq-enabled-plugins --- apiVersion: v1 kind: Service metadata: name: rabbitmq spec: selector: app: rabbitmq ports: - name: rabbitmq-amqp port: 5672 targetPort: 5672 - name: rabbitmq-http port: 15672 targetPort: 15672 type: ClusterIP --- apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: ghcr.io/azure-samples/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "rabbitmq" - name: ORDER_QUEUE_PORT value: "5672" - name: ORDER_QUEUE_USERNAME value: "username" - name: ORDER_QUEUE_PASSWORD value: "password" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi initContainers: - name: wait-for-rabbitmq image: busybox command: ['sh', '-c', 'until nc -zv rabbitmq 5672; do echo waiting for rabbitmq; sleep 2; done;'] resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: order-service spec: type: ClusterIP ports: - name: http port: 3000 targetPort: 3000 selector: app: order-service --- apiVersion: apps/v1 kind: Deployment metadata: name: product-service spec: replicas: 1 selector: matchLabels: app: product-service template: metadata: labels: app: product-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: product-service image: ghcr.io/azure-samples/aks-store-demo/product-service:latest ports: - containerPort: 3002 resources: requests: cpu: 1m memory: 1Mi limits: cpu: 1m memory: 7Mi --- apiVersion: v1 kind: Service metadata: name: product-service spec: type: ClusterIP ports: - name: http port: 3002 targetPort: 3002 selector: app: product-service --- apiVersion: apps/v1 kind: Deployment metadata: name: store-front spec: replicas: 1 selector: matchLabels: app: store-front template: metadata: labels: app: store-front spec: nodeSelector: "kubernetes.io/os": linux containers: - name: store-front image: ghcr.io/azure-samples/aks-store-demo/store-front:latest ports: - containerPort: 8080 name: store-front env: - name: VUE_APP_ORDER_SERVICE_URL value: "http://order-service:3000/" - name: VUE_APP_PRODUCT_SERVICE_URL value: "http://product-service:3002/" resources: requests: cpu: 1m memory: 200Mi limits: cpu: 1000m memory: 512Mi --- apiVersion: v1 kind: Service metadata: name: store-front spec: ports: - port: 80 targetPort: 8080 selector: app: store-front type: LoadBalancer`

For a breakdown of YAML manifest files, see

[Deployments and YAML manifests](https://kubernetes.io/docs/concepts/workloads/controllers/deployment/).If you create and save the YAML file locally, then you can upload the manifest file to your default directory in CloudShell by selecting the

**Upload/Download files**button and selecting the file from your local file system.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the deployments and services:

`deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created`


## Test the application

Check the status of the deployed pods using the

command. Make all pods are`kubectl get pods`

`Running`

before proceeding.`kubectl get pods`

Check for a public IP address for the store-front application. Monitor progress using the

command with the`kubectl get service`

`--watch`

argument.`kubectl get service store-front --watch`

The

**EXTERNAL-IP**output for the`store-front`

service initially shows as*pending*:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 <pending> 80:30025/TCP 4h4m`

Once the

**EXTERNAL-IP**address changes from*pending*to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following example output shows a valid public IP address assigned to the service:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-front LoadBalancer 10.0.100.10 20.62.159.19 80:30025/TCP 4h5m`

Open a web browser to the external IP address of your service to see the Azure Store app in action:


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges.

- Remove the resource group, container service, and all related resources using the
command.`az group delete`


```
az group delete --name myResourceGroup
```


Note

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity, so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS and walk through a complete code-to-deployment example, continue to the Kubernetes cluster tutorial.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/learn/quick-kubernetes-automatic-deploy -->

# Quickstart: Create an Azure Kubernetes Service (AKS) Automatic cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

**Applies to:** ✔️ AKS Automatic

[Azure Kubernetes Service (AKS) Automatic](../intro-aks-automatic) provides the easiest managed Kubernetes experience for developers, DevOps engineers, and platform engineers. Ideal for modern and AI applications, AKS Automatic automates AKS cluster setup and operations and embeds best practice configurations. Users of any skill level can benefit from the security, performance, and dependability of AKS Automatic for their applications. AKS Automatic also includes a [pod readiness SLA](https://www.microsoft.com/licensing/docs/view/Service-Level-Agreements-SLA-for-Online-Services) that guarantees 99.9% of pod readiness operations complete within 5 minutes, guaranteeing reliable, self-healing infrastructure for your applications.

In this quickstart, you learn to:

- Deploy an AKS Automatic cluster.
- Run a sample multi-container application with a group of microservices and web front ends simulating a retail scenario.

## Before you begin

- This quickstart assumes a basic understanding of Kubernetes concepts. For more information, see
[Kubernetes core concepts for Azure Kubernetes Service (AKS)](../concepts-clusters-workloads). - AKS Automatic will
[enable Azure Policy on your AKS cluster](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks), but you should pre-register the`Microsoft.PolicyInsights`

resource provider in your subscription for a smoother experience. See[Azure resource providers and types](/en-us/cli/azure/provider#az-provider-register)for more information.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.77.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command.`az account set`


- To deploy a Bicep file, you need to write access on the resources you create and access to all operations on the
`Microsoft.Resources/deployments`

resource type. For example, to create a virtual machine, you need`Microsoft.Compute/virtualMachines/write`

and`Microsoft.Resources/deployments/*`

permissions. For a list of roles and permissions, see[Azure built-in roles](/en-us/azure/role-based-access-control/built-in-roles).

## Limitations

- AKS Automatic clusters' system nodepool require deployment in Azure regions that support at least three
[availability zones](/en-us/azure/reliability/regions-list), ephemeral OS disk, and Azure Linux OS. - You can only create AKS Automatic clusters in regions where
[API Server VNet Integration](../api-server-vnet-integration)is generally available (GA).

Important

AKS Automatic tries to dynamically select a virtual machine size for the `system`

node pool based on the capacity available in the subscription. Make sure your subscription has quota for 16 vCPUs of any of the following sizes in the region you're deploying the cluster to: [Standard_D4lds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series), [Standard_D4ads_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dadsv5-series), [Standard_D4ds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v5](/en-us/azure/virtual-machines/sizes/general-purpose/ddv5-series), [Standard_D4d_v4](/en-us/azure/virtual-machines/sizes/general-purpose/dv4-series), [Standard_DS3_v2](/en-us/azure/virtual-machines/sizes/general-purpose/dsv3-series), [Standard_DS12_v2](/en-us/azure/virtual-machines/sizes/memory-optimized/dv2-dsv2-series-memory), [Standard_D4alds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/daldsv6-series), [Standard_D4lds_v6](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv6-series), or [Standard_D4alds_v5](/en-us/azure/virtual-machines/sizes/general-purpose/dldsv5-series). You can [view quotas for specific VM-families and submit quota increase requests](/en-us/azure/quotas/per-vm-quota-requests) through the Azure portal.
If you have additional questions, learn more through the [troubleshooting docs](/en-us/troubleshoot/azure/azure-kubernetes/create-upgrade-delete/aks-automatic-troubleshoot/).

## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name myResourceGroup --location eastus
```


The following sample output resembles successful creation of the resource group:

```
{
"id": "/subscriptions/<guid>/resourceGroups/myResourceGroup",
"location": "eastus",
"managedBy": null,
"name": "myResourceGroup",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null
}
```


## Create an AKS Automatic cluster

To create an AKS Automatic cluster, use the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command. The following example creates a cluster named

*myAKSAutomaticCluster*with Managed Prometheus and Container Insights integration enabled.

```
az aks create \
--resource-group myResourceGroup \
--name myAKSAutomaticCluster \
--sku automatic
```


After a few minutes, the command completes and returns JSON-formatted information about the cluster.

## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [ az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with

[Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

Note

When you create a cluster using the Azure CLI, your user is [assigned built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) for `Azure Kubernetes Service RBAC Cluster Admin`

.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSAutomaticCluster
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Create Automatic Kubernetes cluster

To create an AKS Automatic cluster, search for

**Kubernetes Services**, and select**Automatic Kubernetes cluster**from the drop-down options.On the

**Basics**tab, fill in all the mandatory fields (Subscription, Resource group, Kubernetes cluster name, and Region) required to get started:On the

**Monitoring**tab, choose your monitoring configurations from Azure Monitor, Managed Prometheus, Grafana Dashboards, Container Network Observability (ACNS) and/or configure alerts. Enable Managed Grafana (optional), add tags (optional), and proceed to create the cluster.On the

**Advanced**tab, update your networking (optional), managed identity (optional), security and managed namespaces (optional) settings and proceed to create the cluster.Get started with configuring your first application from GitHub and set up an automated deployment pipeline.


## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac). When you create a cluster using the Azure portal, your user is [assigned built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) for `Azure Kubernetes Service RBAC Cluster Admin`

.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name myAKSAutomaticCluster
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which Azure resources are deployed and managed. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the [ az group create](/en-us/cli/azure/group#az-group-create) command.

```
az group create --name myResourceGroup --location eastus
```


The following sample output resembles successful creation of the resource group:

```
{
"id": "/subscriptions/<guid>/resourceGroups/myResourceGroup",
"location": "eastus",
"managedBy": null,
"name": "myResourceGroup",
"properties": {
"provisioningState": "Succeeded"
},
"tags": null
}
```


## Review the Bicep file

This Bicep file defines an AKS Automatic cluster. While in preview, you need to specify the *system nodepool* agent pool profile.

```
@description('The name of the managed cluster resource.')
param clusterName string = 'myAKSAutomaticCluster'
@description('The location of the managed cluster resource.')
param location string = resourceGroup().location
resource aks 'Microsoft.ContainerService/managedClusters@2024-03-02-preview' = {
name: clusterName
location: location
sku: {
name: 'Automatic'
}
properties: {
agentPoolProfiles: [
{
name: 'systempool'
mode: 'System'
count: 3
}
]
}
identity: {
type: 'SystemAssigned'
}
}
```


For more information about the resource defined in the Bicep file, see the [ Microsoft.ContainerService/managedClusters](/en-us/azure/templates/microsoft.containerservice/managedclusters?tabs=bicep&pivots=deployment-language-bicep) reference.

## Deploy the Bicep file

Save the Bicep file as

**main.bicep**to your local computer.Important

The Bicep file sets the

`clusterName`

param to the string*myAKSAutomaticCluster*. If you want to use a different cluster name, make sure to update the string to your preferred cluster name before saving the file to your computer.Deploy the Bicep file using the Azure CLI.

`az deployment group create --resource-group myResourceGroup --template-file main.bicep`

It takes a few minutes to create the AKS cluster. Wait for the cluster to be successfully deployed before you move on to the next step.


## Connect to the cluster

To manage a Kubernetes cluster, use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell. To install `kubectl`

locally, run the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. AKS Automatic clusters are configured with [Microsoft Entra ID for Kubernetes role-based access control (RBAC)](/en-us/azure/aks/manage-azure-rbac).

Important

When you create a cluster using Bicep, you need to [assign one of the built-in roles](/en-us/azure/aks/manage-azure-rbac#create-role-assignments-for-users-to-access-the-cluster) such as `Azure Kubernetes Service RBAC Reader`

, `Azure Kubernetes Service RBAC Writer`

, `Azure Kubernetes Service RBAC Admin`

, or `Azure Kubernetes Service RBAC Cluster Admin`

to your users, scoped to the cluster or a specific namespace, example using `az role assignment create --role "Azure Kubernetes Service RBAC Cluster Admin" --scope <AKS cluster resource id> --assignee user@contoso.com`

. Also make sure your users have the `Azure Kubernetes Service Cluster User`

built-in role to be able to do run `az aks get-credentials`

, and then get the kubeconfig of your AKS cluster using the `az aks get-credentials`

command.

Configure `kubectl`

to connect to your Kubernetes cluster using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command. This command downloads credentials and configures the Kubernetes CLI to use them.

```
az aks get-credentials --resource-group myResourceGroup --name
```


Verify the connection to your cluster using the [ kubectl get](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command. This command returns a list of the cluster nodes.

```
kubectl get nodes
```


The following sample output shows how you're asked to log in.

```
To sign in, use a web browser to open the page https://microsoft.com/devicelogin and enter the code AAAAAAAAA to authenticate.
```


After you log in, the following sample output shows the managed system node pools. Make sure the node status is *Ready*.

```
NAME STATUS ROLES AGE VERSION
aks-nodepool1-13213685-vmss000000 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000001 Ready agent 2m26s v1.28.5
aks-nodepool1-13213685-vmss000002 Ready agent 2m26s v1.28.5
```


## Deploy the application

To deploy the application, you use a manifest file to create all the objects required to run the [AKS Store application](https://github.com/Azure-Samples/aks-store-demo). A [Kubernetes manifest file](../concepts-clusters-workloads#deployments-and-yaml-manifests) defines a cluster's desired state, such as which container images to run. The manifest includes the following Kubernetes deployments and services:

**Store front**: Web application for customers to view products and place orders.**Product service**: Shows product information.**Order service**: Places orders.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as Rabbit MQ, without persistent storage for production. These are used here for simplicity, but we recommend using managed services, such as Azure Cosmos DB or Azure Service Bus.

Create a namespace

`aks-store-demo`

to deploy the Kubernetes resources into.`kubectl create ns aks-store-demo`

Deploy the application using the

command into the`kubectl apply`

`aks-store-demo`

namespace. The YAML file defining the deployment is on[GitHub](https://github.com/Azure-Samples/aks-store-demo).`kubectl apply -n aks-store-demo -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-ingress-quickstart.yaml`

The following sample output shows the deployments and services:

`statefulset.apps/rabbitmq created configmap/rabbitmq-enabled-plugins created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created ingress/store-front created`


## Test the application

When the application runs, a Kubernetes service exposes the application front end to the internet. This process can take a few minutes to complete.

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command. Make sure all pods are`Running`

before proceeding. If this is the first workload you deploy, it may take a few minutes for[node auto provisioning](../node-autoprovision)to create a node pool to run the pods.`kubectl get pods -n aks-store-demo`

Check for a public IP address for the store-front application. Monitor progress using the

[kubectl get service](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command with the`--watch`

argument.`kubectl get ingress store-front -n aks-store-demo --watch`

The

**ADDRESS**output for the`store-front`

service initially shows empty:`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 80 12m`

Once the

**ADDRESS**changes from blank to an actual public IP address, use`CTRL-C`

to stop the`kubectl`

watch process.The following sample output shows a valid public IP address assigned to the service:

`NAME CLASS HOSTS ADDRESS PORTS AGE store-front webapprouting.kubernetes.azure.com * 4.255.22.196 80 12m`

Open a web browser to the external IP address of your ingress to see the Azure Store app in action.


## Delete the cluster

If you don't plan on going through the [AKS tutorial](../tutorial-kubernetes-prepare-app), clean up unnecessary resources to avoid Azure charges. Run the [az group delete](/en-us/cli/azure/group#az-group-delete) command to remove the resource group, container service, and all related resources.

```
az group delete --name myResourceGroup --yes --no-wait
```


Note

The AKS cluster was created with a system-assigned managed identity, which is the default identity option used in this quickstart. The platform manages this identity, so you don't need to manually remove it.

## Next steps

In this quickstart, you deployed a Kubernetes cluster using [AKS Automatic](../intro-aks-automatic) and then deployed a simple multi-container application to it. This sample application is for demo purposes only and doesn't represent all the best practices for Kubernetes applications. For guidance on creating full solutions with AKS for production, see [AKS solution guidance](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

To learn more about AKS Automatic, continue to the introduction.
