---
merged_at: 2026-01-30T23:42:48.964267
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-ai-quickstart -->

# Deploy an application that uses OpenAI on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy an application that uses Azure OpenAI or OpenAI on AKS. With OpenAI, you can easily adapt different AI models, such as content generation, summarization, semantic search, and natural language to code generation, for your specific tasks. You start by deploying an AKS cluster in your Azure subscription. Then, you deploy your OpenAI service and the sample application.

The sample cloud native application is representative of real-world implementations. The multi-container application is comprised of applications written in multiple languages and frameworks, including:

- Golang with Gin
- Rust with Actix-Web
- JavaScript with Vue.js and Fastify
- Python with FastAPI

These applications provide front ends for customers and store admins, REST APIs for sending data to RabbitMQ message queue and MongoDB database, and console apps to simulate traffic.

Note

We don't recommend running stateful containers, such as MongoDB and Rabbit MQ, without persistent storage for production. We use them here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

To access the GitHub codebase for the sample application, see [AKS Store Demo](https://github.com/Azure-Samples/aks-store-demo).

## Before you begin

- You need an Azure account with an active subscription. If you don't have one,
[create an account for free](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn). - For this demo, you can either use Azure OpenAI service or OpenAI service.
- If you plan on using Azure OpenAI service, you need to request access to enable it on your Azure subscription using the
[Request access to Azure OpenAI Service form](https://aka.ms/oai/access). - If you plan on using OpenAI, sign up on the
[OpenAI website](https://openai.com/).

- If you plan on using Azure OpenAI service, you need to request access to enable it on your Azure subscription using the

## Prerequisites

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


## Create a resource group

An [Azure resource group](/en-us/azure/azure-resource-manager/management/overview) is a logical group in which you deploy and manage Azure resources. When you create a resource group, you're prompted to specify a location. This location is the storage location of your resource group metadata and where your resources run in Azure if you don't specify another region during resource creation.

The following example creates a resource group named *myResourceGroup* in the *eastus* location.

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`

The following example output shows successful creation of the resource group:

`{ "id": "/subscriptions/<guid>/resourceGroups/myResourceGroup", "location": "eastus", "managedBy": null, "name": "myResourceGroup", "properties": { "provisioningState": "Succeeded" }, "tags": null, "type": "Microsoft.Resources/resourceGroups" }`


## Create an AKS cluster

The following example creates a cluster named *myAKSCluster* in *myResourceGroup*.

Create an AKS cluster using the

command.`az aks create`

`az aks create --resource-group myResourceGroup --name myAKSCluster --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Connect to the cluster

To manage a Kubernetes cluster, you use the Kubernetes command-line client, [kubectl](https://kubernetes.io/docs/reference/kubectl/). `kubectl`

is already installed if you use Azure Cloud Shell.

Install

`kubectl`

locally using thecommand.`az aks install-cli`

`az aks install-cli`

Note

If your Linux-based system requires elevated permissions, you can use the

`sudo az aks install-cli`

command.Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand.`az aks get-credentials`

This command executes the following operations:

- Downloads credentials and configures the Kubernetes CLI to use them.
- Uses
`~/.kube/config`

, the default location for the[Kubernetes configuration file](https://kubernetes.io/docs/concepts/configuration/organize-cluster-access-kubeconfig/). Specify a different location for your Kubernetes configuration file using*--file*argument.

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the nodes created in the previous steps. Make sure the node status is

*Ready*.`NAME STATUS ROLES AGE VERSION aks-nodepool1-31469198-vmss000000 Ready agent 3h29m v1.25.6 aks-nodepool1-31469198-vmss000001 Ready agent 3h29m v1.25.6 aks-nodepool1-31469198-vmss000002 Ready agent 3h29m v1.25.6`


Note

For private clusters, the nodes might be unreachable if you try to connect to them through the public IP address. In order to fix this, you need to create an endpoint within the same VNET as the cluster to connect from. Follow the instructions to [Create a private AKS cluster](private-clusters) and then connect to it.

## Deploy the application

The [AKS Store application](https://github.com/Azure-Samples/aks-store-demo) manifest includes the following Kubernetes deployments and services:

**Product service**: Shows product information.**Order service**: Places orders.**Makeline service**: Processes orders from the queue and completes the orders.**Store front**: Web application for customers to view products and place orders.**Store admin**: Web application for store employees to view orders in the queue and manage product information.**Virtual customer**: Simulates order creation on a scheduled basis.**Virtual worker**: Simulates order completion on a scheduled basis.**Mongo DB**: NoSQL instance for persisted data.**Rabbit MQ**: Message queue for an order queue.

Note

We don't recommend running stateful containers, such as MongoDB and Rabbit MQ, without persistent storage for production. We use them here for simplicity, but we recommend using managed services, such as Azure CosmosDB or Azure Service Bus.

Review the

[YAML manifest](https://github.com/Azure-Samples/aks-store-demo/blob/main/aks-store-all-in-one.yaml)for the application.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-all-in-one.yaml`

The following example output shows the successfully created deployments and services:

`deployment.apps/mongodb created service/mongodb created deployment.apps/rabbitmq created service/rabbitmq created deployment.apps/order-service created service/order-service created deployment.apps/makeline-service created service/makeline-service created deployment.apps/product-service created service/product-service created deployment.apps/store-front created service/store-front created deployment.apps/store-admin created service/store-admin created deployment.apps/virtual-customer created deployment.apps/virtual-worker created`


## Deploy OpenAI

You can either use Azure OpenAI or OpenAI and run your application on AKS.

- In the Azure portal, create an Azure OpenAI instance.
- Navigate to the Azure OpenAI instance you created.
- From the
**Overview**blade, navigate to the[Azure AI Foundry portal](https://oai.azure.com/portal/). - Create a new
**Chat**deployment using the**gpt-4o-mini**base model.

For more information on how to create a deployment in Azure OpenAI, see [Get started generating text using Azure OpenAI Service](/en-us/azure/ai-services/openai/quickstart).

## Deploy the AI service

Now that the application is deployed, you can deploy the Python-based microservice that uses OpenAI to automatically generate descriptions for new products being added to the store's catalog.

Create a file named

`ai-service.yaml`

and copy in the following manifest:`apiVersion: apps/v1 kind: Deployment metadata: name: ai-service spec: replicas: 1 selector: matchLabels: app: ai-service template: metadata: labels: app: ai-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: ai-service image: ghcr.io/azure-samples/aks-store-demo/ai-service:latest ports: - containerPort: 5001 env: - name: USE_AZURE_OPENAI value: "True" - name: AZURE_OPENAI_DEPLOYMENT_NAME value: "" - name: AZURE_OPENAI_ENDPOINT value: "" - name: OPENAI_API_KEY value: "" resources: requests: cpu: 20m memory: 50Mi limits: cpu: 50m memory: 128Mi --- apiVersion: v1 kind: Service metadata: name: ai-service spec: type: ClusterIP ports: - name: http port: 5001 targetPort: 5001 selector: app: ai-service`

Set the environment variable

`USE_AZURE_OPENAI`

to`"True"`

.Get your Azure OpenAI deployment name from

[Azure AI Foundry](https://oai.azure.com/portal/)and fill in the`AZURE_OPENAI_DEPLOYMENT_NAME`

value.Get your Azure OpenAI endpoint and Azure OpenAI API key from the Azure portal by selecting

**Keys and Endpoint**in the left blade of the resource. Update the`AZURE_OPENAI_ENDPOINT`

and`OPENAI_API_KEY`

in the YAML accordingly.Deploy the application using the

command and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f ai-service.yaml`

The following example output shows the successfully created deployments and services:

`deployment.apps/ai-service created service/ai-service created`


Note

Directly adding sensitive information, such as API keys, to your Kubernetes manifest files isn't secure and may accidentally get committed to code repositories. We added it here for simplicity. For production workloads, use [Managed Identity](/en-us/azure/ai-services/openai/how-to/managed-identity#authorize-access-to-managed-identities) to authenticate to Azure OpenAI service instead or store your secrets in [Azure Key Vault](csi-secrets-store-driver).

## Test the application

Check the status of the deployed pods using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.`kubectl get pods`

Make sure all the pods are

*Running*before continuing to the next step.`NAME READY STATUS RESTARTS AGE makeline-service-7db94dc7d4-8g28l 1/1 Running 0 99s mongodb-78f6d95f8-nptbz 1/1 Running 0 99s order-service-55cbd784bb-6bmfb 1/1 Running 0 99s product-service-6bf4d65f74-7cbvk 1/1 Running 0 99s rabbitmq-9855984f9-94nlm 1/1 Running 0 99s store-admin-7f7d768c48-9hn8l 1/1 Running 0 99s store-front-6786c64d97-xq5s9 1/1 Running 0 99s virtual-customer-79498f8667-xzsb7 1/1 Running 0 99s virtual-worker-6d77fff4b5-7g7rj 1/1 Running 0 99s`

Get the IP of the store admin web application and store front web application using the

`kubectl get service`

command.`kubectl get service store-admin`

The application exposes the Store Admin site to the internet via a public load balancer provisioned by the Kubernetes service. This process can take a few minutes to complete.

**EXTERNAL IP**initially shows*pending*until the service comes up and shows the IP address.`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE store-admin LoadBalancer 10.0.142.228 40.64.86.161 80:32494/TCP 50m`

Repeat the same step for the service named `store-front``.

Open a web browser and browse to the external IP address of your service. In the example shown here, open

*40.64.86.161*to see Store Admin in the browser. Repeat the same step for Store Front.In store admin, select the products tab, then select

**Add Products**.When the `ai-service`` is running successfully, you should see the Ask OpenAI button next to the description field. Fill in the name, price, and keywords, then generate a product description by selecting

**Ask OpenAI**>**Save product**.You can now see the new product you created on Store Admin used by sellers. In the picture, you can see Dog Smart Collar is added.

You can also see the new product you created on Store Front used by buyers. In the picture, you can see Dog Smart Collar is added. Remember to get the IP address of store front using the

command.`kubectl get service`


## Next steps

Now that you added OpenAI functionality to an AKS application, you can [Secure access to Azure OpenAI from Azure Kubernetes Service (AKS)](open-ai-secure-access-quickstart).

To learn more about generative AI use cases, see the following resources:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-flyte -->

# Build and deploy data and machine learning pipelines with Flyte on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use Flyte on Azure Kubernetes Service (AKS). Flyte is an open-source workflow orchestrator that unifies machine learning, data engineering, and data analytics stacks to help you build robust and reliable applications. When using Flyte as a Kubernetes-native workflow automation tool, you can focus on experimentation and providing business value without increasing your scope to infrastructure and resource management. Keep in mind that Flyte isn't officially supported by Microsoft, so use it at your own discretion.

For more information, see [Introduction to Flyte](https://www.union.ai/docs/flyte/user-guide/).

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## Flyte use cases

Flyte can be used for a variety of use cases, including:

- Deliver models for streamlined profit and loss financial calculations.
- Process petabytes of data to efficiently conduct 3D mapping of new areas.
- Quickly rollback to previous versions and minimize impact of bugs in your pipelines.

For more information, see [Flyte tutorials](https://www.union.ai/docs/flyte/tutorials/).

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free).- If you have multiple subscriptions, make sure you select the correct one using the
`az account set --subscription <subscription-id>`

command.

- If you have multiple subscriptions, make sure you select the correct one using the
- The Azure CLI installed and configured. Check your version using the
`az --version`

command. If you need to install or upgrade, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - The Helm CLI installed and updated. Check your version using the
`helm version`

command. If you need to install or upgrade, see[Install Helm](https://helm.sh/docs/intro/install/). - The
`kubectl`

CLI installed and updated. Install it locally using the`az aks install-cli`

command or using[Install kubectl](https://kubernetes.io/docs/tasks/tools/install-kubectl/). - A local Docker development environment. For more information, see
[Get Docker](https://docs.docker.com/get-docker/). `flytekit`

and`flytectl`

installed. For more information, see[Flyte installation](https://www.union.ai/docs/flyte/user-guide/getting-started/local-setup/).

Note

If you're using the Azure Cloud Shell, the Azure CLI, Helm, and kubectl are already installed.

### Set environment variables

Set environment variables for use throughout the article. Replace the placeholder values with your own values.

`export RESOURCE_GROUP="<resource-group-name>" export LOCATION="<location>" export CLUSTER_NAME="<cluster-name>" export DNS_NAME_PREFIX="<dns-name-prefix>"`


## Create an AKS cluster

Create an Azure resource group for the AKS cluster using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster using the

command with the`az aks create`

`--enable-azure-rbac`

,`--enable-managed-identity`

,`--enable-aad`

, and`--dns-name-prefix`

parameters.`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --enable-azure-rbac --enable-managed-identity --enable-aad --dns-name-prefix $DNS_NAME_PREFIX --generate-ssh-keys`


## Connect to your AKS cluster

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Add the Flyte Helm repository

Add the Flyte Helm repository using the

`helm repo add`

command.`helm repo add flyteorg https://flyteorg.github.io/flyte`


## Find Flyte Helm charts

Search for Flyte Helm charts using the

`helm search repo`

command.`helm search repo flyteorg`

The following example output shows some of the available Flyte Helm charts:

`NAME CHART VERSION APP VERSION DESCRIPTION flyteorg/flyte v1.12.0 A Helm chart for Flyte Sandbox flyteorg/flyte-binary v1.12.0 1.16.0 Chart for basic single Flyte executable deployment flyteorg/flyte-core v1.12.0 A Helm chart for Flyte core flyteorg/flyte-deps v1.12.0 A Helm chart for Flyte dependencies flyteorg/flyte-sandbox 0.1.0 1.16.1 A Helm chart for the Flyte local sandbox flyteorg/flyteagent v0.1.10 A Helm chart for Flyte Agent`

Update the repository using the

`helm repo update`

command.`helm repo update`


## Deploy a Flyte chart on AKS

In this section, you deploy the flyte-binary Helm chart so you can begin building and deploying data and machine learning pipelines with Flyte on AKS. The flyte-binary chart is a basic single Flyte executable deployment.

Create a namespace for your Flyte deployment using the

`kubectl create namespace`

command.`kubectl create namespace <namespace-name>`

Install a Flyte Helm chart using the

`helm install`

command. In this example, we use the`flyte-binary`

chart.`helm install flyte-binary flyteorg/flyte-core --namespace <namespace-name>`

Verify that the Flyte deployment is running using the

`kubectl get services`

command.`kubectl get services --namespace <namespace-name> --output wide`

The following condensed example output shows the Flyte deployment:

`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE flyteorg-flyte-binary-grpc ClusterIP xx.x.xx.xxx <none> 81/TCP 1m flyteorg-flyte-binary-http ClusterIP xx.x.xx.xxx <none> 80/TCP 1m flyteorg-flyte-binary-webhook ClusterIP xx.x.xx.xxx <none> 80/TCP 1m`


## Next steps

In this article, you learned how to install Flyte on AKS using a Helm chart.
The Flyte project also maintains a [reference implementation for AKS](https://github.com/unionai-oss/deploy-flyte/tree/main/environments/azure/flyte-core#readme) that automatically configures all the dependencies and deploys a production grade Flyte cluster.

To start building and deploying data and machine learning pipelines, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/scale-node-pools -->

# Scale node pools in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As your application workload demands change, you might need to scale the number of nodes in a node pool in Azure Kubernetes Service (AKS). In this article, you learn how to manually and automatically scale node pools in AKS.

## Prerequisites for AKS node pool scaling

- An existing AKS cluster with at least one node pool. If you need to create one, see
[Create an AKS cluster with node pools](create-node-pools). - You need the Azure CLI version 2.2.0 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Scale a node pool manually

Scale the number of nodes in a node pool using the [

`az aks nodepool scale`

][az-aks-nodepool-scale] command. The`--node-count`

flag specifies the desired number of nodes in the node pool. In this example, the node pool is scaled to five nodes.`az aks nodepool scale \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --node-count 5 \ --no-wait`

Check the status of your node pools using the [

`az aks nodepool list`

][az-aks-nodepool-list] command.`az aks nodepool list --resource-group <resource-group-name> --cluster-name <cluster-name>`

The following example output shows the node pool is in the

*Scaling*state with a new count of five nodes:`[ { ... "count": 5, ... "name": "<node-pool-name>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Scaling", ... "vmSize": "Standard_DS2_v2", ... }, { ... "count": 2, ... "name": "<node-pool-name-2>", "orchestratorVersion": "1.15.7", ... "provisioningState": "Succeeded", ... "vmSize": "Standard_DS2_v2", ... } ]`

It takes a few minutes for the scale operation to complete. After the scale operation is complete, the node pool's

`provisioningState`

changes to*Succeeded*.

## Scale a node pool automatically with the cluster autoscaler

You can use the [cluster autoscaler](cluster-autoscaler-overview) with multiple node pools, and you can enable it on individual node pools and pass unique autoscaling rules to them.

Enable the cluster autoscaler on an existing node pool using the [

`az aks nodepool update`

][az-aks-nodepool-update] command with the`--update-cluster-autoscaler`

flag. The`--min-count`

and`--max-count`

flags specify the minimum and maximum number of nodes in the node pool. In this example, the cluster autoscaler is enabled with a minimum count of one node and a maximum count of five nodes:`az aks nodepool update \ --resource-group <resource-group-name> \ --cluster-name <cluster-name> \ --name <node-pool-name> \ --update-cluster-autoscaler \ --min-count 1 \ --max-count 5`


Note

If you want to disable the cluster autoscaler on a node pool, use the [`az aks nodepool update`

][az-aks-nodepool-update] command with the `--disable-cluster-autoscaler`

flag instead of `--update-cluster-autoscaler`

.

## Next steps: Manage node pools in AKS

To learn more about managing node pools in AKS, see [Manage node pools in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/start-stop-nodepools -->

# Start and stop an Azure Kubernetes Service (AKS) node pool

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might not need to continuously run your AKS workloads. For example, you might have a development cluster that has node pools running specific workloads. To optimize your compute costs, you can completely stop your node pools in your AKS cluster.

## Features and limitations

- You can't stop system pools.
- Spot node pools are supported.
- Stopped node pools can be upgraded.
- The cluster and node pool must be running.
- You can't stop node pools from clusters which use the
[Node Autoprovisioning (NAP)](node-autoprovision)feature.

Tip

You can use Azure Copilot to stop and start your node pools in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#start-and-stop-node-pools).

## Before you begin

This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using the [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

## Stop an AKS node pool

Stop a running AKS node pool using the

command.`az aks nodepool stop`

`az aks nodepool stop --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

Verify your node pool stopped using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

The following condensed example output shows the

`powerState`

as`Stopped`

:`{ [...] "osType": "Linux", "podSubnetId": null, "powerState": { "code": "Stopped" }, "provisioningState": "Succeeded", "proximityPlacementGroupId": null, [...] }`

Note

If the

`provisioningState`

shows`Stopping`

, your node pool is still in the process of stopping.Note

Stopping the node pool will stop its Cluster Autoscaler, and starts it back when starting the node pool. So if you manually modify the number of VMSS instances in the pool while it's stopped, Cluster Autoscaler might show inconsistencies.


## Start a stopped AKS node pool

Restart a stopped node pool using the

command.`az aks nodepool start`

`az aks nodepool start --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

Verify your node pool started using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

The following condensed example output shows the

`powerState`

as`Running`

:`{ [...] "osType": "Linux", "podSubnetId": null, "powerState": { "code": "Running" }, "provisioningState": "Succeeded", "proximityPlacementGroupId": null, [...] }`

Note

If the

`provisioningState`

shows`Starting`

, your node pool is still in the process of starting.

## Next steps

- To learn how to scale
`User`

pools to 0, see[scale](scale-cluster#scale-user-node-pools-to-0).`User`

pools to 0 - To learn how to stop your cluster, see
[cluster start/stop](start-stop-cluster). - To learn how to save costs using Spot instances, see
[add a spot node pool to AKS](spot-node-pool). - To learn more about the AKS support policies, see
[AKS support policies](support-policies).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-upgrade -->

# Upgrade Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article addresses upgrade experiences for Istio-based service mesh add-on for Azure Kubernetes Service (AKS).

Announcements about the releases of new minor revisions or patches to the Istio-based service mesh add-on are published in the [AKS release notes](https://github.com/Azure/AKS/releases). To learn more about the release schedule and support for service mesh add-on revisions, read the [support policy](istio-support-policy#versioning-and-support-policy).

## Minor revision upgrade

Istio add-on allows upgrading the minor revision using [canary upgrade process](https://istio.io/latest/docs/setup/upgrade/canary/). When an upgrade is initiated, the control plane of the new (canary) revision is deployed alongside the initial (stable) revision's control plane. You can then manually roll over data plane workloads while using monitoring tools to track the health of workloads during this process. If you don't observe any issues with the health of your workloads, you can complete the upgrade so that only the new revision remains on the cluster. Else, you can roll back to the previous revision of Istio.

Available upgrades depend on whether the current Istio revision and AKS cluster version are supported:

- You can upgrade to the
**next supported revision (**or skip one and upgrade to`n+1`

), as long as both are supported and compatible with the cluster version.`n+2`

- If both your current revision (
`n`

) and the next revision (`n+1`

) are unsupported, you can only upgrade to the**nearest supported revision (**, but not beyond it.`n+2`

or higher) - If the cluster version and Istio revision are both unsupported, the cluster version must be upgraded before an Istio upgrade can be initiated.

Note

Once an AKS version or mesh revision falls outside the support window, upgrading either version becomes error-prone. While such upgrades are **allowed** to recover to a supported version, **the upgrade process and the out-of-support versions themselves are both not supported by Microsoft**. We strongly recommend keeping AKS version and mesh revision up to date to avoid running into unsupported scenarios. Refer to the [Istio add-on support calendar](istio-support-policy#service-mesh-add-on-release-calendar) for estimated release and end-of-life dates and the [upstream Istio release notes](https://istio.io/latest/news/releases/) for the new revision for notable changes.

The following example illustrates how to upgrade from revision `asm-1-23`

to `asm-1-24`

with all workloads in the `default`

namespace. The steps are the same for all minor upgrades and may be used for any number of namespaces.

Use the

[az aks mesh get-upgrades](/en-us/cli/azure/aks/mesh#az-aks-mesh-get-upgrades)command to check which revisions are available for the cluster as upgrade targets:`az aks mesh get-upgrades --resource-group $RESOURCE_GROUP --name $CLUSTER`

If you expect to see a newer revision not returned by this command, you may need to upgrade your AKS cluster first so that it's compatible with the newest revision.

If you set up

[mesh configuration](istio-meshconfig)for the existing mesh revision on your cluster, you need to create a separate ConfigMap corresponding to the new revision in the`aks-istio-system`

namespace**before initiating the canary upgrade**in the next step. This configuration is applicable the moment the new revision's control plane is deployed on cluster. More details can be found[here](istio-meshconfig#mesh-configuration-and-upgrades).Initiate a canary upgrade from revision

`asm-1-23`

to`asm-1-24`

using[az aks mesh upgrade start](/en-us/cli/azure/aks/mesh/upgrade#az-aks-mesh-upgrade-start):`az aks mesh upgrade start --resource-group $RESOURCE_GROUP --name $CLUSTER --revision asm-1-24`

A canary upgrade means the 1.24 control plane is deployed alongside the 1.23 control plane. They continue to coexist until you either complete or roll back the upgrade.

While a canary upgrade is in progress, the higher revision is considered the

*default revision*used for validation of Istio resources.Optionally, revision tags may be used to roll over the data plane to the new revision without needing to manually relabel each namespace. Manually relabeling namespaces when moving them to a new revision can be tedious and error-prone.

[Revision tags](https://istio.io/latest/docs/setup/upgrade/canary/#stable-revision-labels)solve this problem by serving as stable identifiers that point to revisions.Rather than relabeling each namespace, a cluster operator can change the tag to point to a new revision. All namespaces labeled with that tag are updated at the same time. However, you still need to restart the workloads to make sure the correct version of

`istio-proxy`

sidecars are injected.To use revision tags during an upgrade:

Create a revision tag for the initial revision. In this example, we name it

`prod-stable`

:`istioctl tag set prod-stable --revision asm-1-23 --istioNamespace aks-istio-system`

Create a revision tag for the revision installed during the upgrade. In this example, we name it

`prod-canary`

:`istioctl tag set prod-canary --revision asm-1-24 --istioNamespace aks-istio-system`

Label application namespaces to map to revision tags:

`# label default namespace to map to asm-1-23 kubectl label ns default istio.io/rev=prod-stable --overwrite`

You may also label namespaces with

`istio.io/rev=prod-canary`

for the newer revision. However, the workloads in those namespaces aren't updated to a new sidecar until they're restarted.If a new application is created in a namespace after it is labeled, a sidecar will be injected corresponding to the revision tag on that namespace.


Verify control plane pods corresponding to both

`asm-1-23`

and`asm-1-24`

exist:Verify

`istiod`

pods:`kubectl get pods -n aks-istio-system`

Example output:

`NAME READY STATUS RESTARTS AGE istiod-asm-1-23-55fccf84c8-dbzlt 1/1 Running 0 58m istiod-asm-1-23-55fccf84c8-fg8zh 1/1 Running 0 58m istiod-asm-1-24-f85f46bf5-7rwg4 1/1 Running 0 51m istiod-asm-1-24-f85f46bf5-8p9qx 1/1 Running 0 51m`

If ingress is enabled, verify ingress pods:

`kubectl get pods -n aks-istio-ingress`

Example output:

`NAME READY STATUS RESTARTS AGE aks-istio-ingressgateway-external-asm-1-23-58f889f99d-qkvq2 1/1 Running 0 59m aks-istio-ingressgateway-external-asm-1-23-58f889f99d-vhtd5 1/1 Running 0 58m aks-istio-ingressgateway-external-asm-1-24-7466f77bb9-ft9c8 1/1 Running 0 51m aks-istio-ingressgateway-external-asm-1-24-7466f77bb9-wcb6s 1/1 Running 0 51m aks-istio-ingressgateway-internal-asm-1-23-579c5d8d4b-4cc2l 1/1 Running 0 58m aks-istio-ingressgateway-internal-asm-1-23-579c5d8d4b-jjc7m 1/1 Running 0 59m aks-istio-ingressgateway-internal-asm-1-24-757d9b5545-g89s4 1/1 Running 0 51m aks-istio-ingressgateway-internal-asm-1-24-757d9b5545-krq9w 1/1 Running 0 51m`

Observe that ingress gateway pods of both revisions are deployed side-by-side. However, the service and its IP remain immutable.


Relabel the namespace so that any new pods are mapped to the Istio sidecar associated with the new revision and its control plane:

If using revision tags, overwrite the

`prod-stable`

tag itself to change its mapping:`istioctl tag set prod-stable --revision asm-1-24 --istioNamespace aks-istio-system --overwrite`

Verify the tag-to-revision mappings:

`istioctl tag list`

Both tags should point to the newly installed revision:

`TAG REVISION NAMESPACES prod-canary asm-1-24 default prod-stable asm-1-24 ...`

In this case, you don't need to relabel each namespace individually.

If not using revision tags, data plane namespaces must be relabeled to point to the new revision:

`kubectl label namespace default istio.io/rev=asm-1-24 --overwrite`


Relabeling doesn't affect your workloads until they're restarted.

Individually roll over each of your application workloads by restarting them. For example:

`kubectl rollout restart deployment <deployment name> -n <deployment namespace>`

Check your monitoring tools and dashboards to determine whether your workloads are all running in a healthy state after the restart. Based on the outcome, you have two options:

**Complete the canary upgrade**: If you're satisfied that the workloads are all running in a healthy state as expected, you can complete the canary upgrade. Completion of the upgrade removes the previous revision's control plane and leaves behind the new revision's control plane on the cluster. Run the following command to complete the canary upgrade:`az aks mesh upgrade complete --resource-group $RESOURCE_GROUP --name $CLUSTER`

**Rollback the canary upgrade**: In case you observe any issues with the health of your workloads, you can roll back to the previous revision of Istio:

Relabel the namespace to the previous revision: If using revision tags:

`istioctl tag set prod-stable --revision asm-1-23 --istioNamespace aks-istio-system --overwrite`

Or, if not using revision tags:

`kubectl label namespace default istio.io/rev=asm-1-23 --overwrite`

Roll back the workloads to use the sidecar corresponding to the previous Istio revision by restarting these workloads again:

`kubectl rollout restart deployment <deployment name> -n <deployment namespace>`

Roll back the control plane to the previous revision:

`az aks mesh upgrade rollback --resource-group $RESOURCE_GROUP --name $CLUSTER`


The

`prod-canary`

revision tag can be removed:`istioctl tag remove prod-canary --istioNamespace aks-istio-system`

If

[mesh configuration](istio-meshconfig)was previously set up for the revisions, you can now delete the ConfigMap for the revision that was removed from the cluster during complete/rollback.

### Minor revision upgrades with ingress and egress gateways

If you're currently using [Istio ingress gateways](istio-deploy-ingress) or [egress gateways](istio-deploy-egress) and are performing a minor revision upgrade, keep in mind that Istio ingress and egress gateway pods / deployments are deployed per-revision, but the service is shared across both revisions.

We provide a single `LoadBalancer`

service across all ingress gateway pods over multiple revisions, so the external/internal IP address of the ingress gateways remains unchanged throughout the course of an upgrade. Thus, during the canary upgrade, when two revisions exist simultaneously on the cluster, the ingress gateway pods of both revisions serve incoming traffic.

Likewise, during a canary upgrade, all pods for an egress gateway across both revisions will be served by a single `ClusterIP`

service.

### Minor revision upgrades with horizontal pod autoscaling customizations

If you have customized [horizontal pod autoscaling (HPA) settings for Istiod or the ingress gateways](istio-scale#horizontal-pod-autoscaling-customization), note the following behavior for how HPA settings are applied across both revisions to maintain consistency during a canary upgrade:

- If you update the HPA spec before initiating an upgrade, the settings from the existing (stable) revision will be applied to the HPAs of the canary revision when the new control plane is installed.
- If you update the HPA spec while a canary upgrade is in progress, the HPA spec of the stable revision will take precedence and be applied to the HPA of the canary revision.
- If you update the HPA of the stable revision during an upgrade, the HPA spec of the canary revision will be updated to reflect the new settings applied to the stable revision.
- If you update the HPA of the canary revision during an upgrade, the HPA spec of the canary revision will be reverted to the HPA spec of the stable revision.


## Patch version upgrade

- Istio add-on patch version availability information is published in
[AKS release notes](https://github.com/Azure/AKS/releases). - Patches are rolled out automatically for istiod and ingress pods as part of these AKS releases, which respect the
`default`

[planned maintenance window](planned-maintenance)set up for the cluster. - User needs to initiate patches to Istio proxy in their workloads by restarting the pods for reinjection:
Check the version of the Istio proxy intended for new or restarted pods. This version is the same as the version of the istiod and Istio ingress pods after they were patched:

`kubectl get cm -n aks-istio-system -o yaml | grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`"image": "mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless", "image": "mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless"`

Check the Istio proxy image version for all pods in a namespace:

`kubectl get pods --all-namespaces -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' |\ sort |\ grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`productpage-v1-979d4d9fc-p4764: docker.io/istio/examples-bookinfo-productpage-v1:1.23.0, mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless`

To trigger reinjection, restart the workloads. For example:

`kubectl rollout restart deployments/productpage-v1 -n default`

To verify that they're now on the newer versions, check the Istio proxy image version again for all pods in the namespace:

`kubectl get pods --all-namespaces -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' |\ sort |\ grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`productpage-v1-979d4d9fc-p4764: docker.io/istio/examples-bookinfo-productpage-v1:1.2.0, mcr.microsoft.com/oss/istio/proxyv2:1.24.0-distroless`


Note

In case of any issues encountered during upgrades, refer to [article on troubleshooting mesh revision upgrades](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-minor-revision-upgrade)

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/automated-deployments -->

# Automated deployments for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Automated Deployments streamline the process of setting up a GitHub Action or Azure DevOps Pipeline, making it easy to create a continuous deployment pipeline for your application to Azure Kubernetes Service (AKS). Once connected, every new commit automatically triggers the pipeline, delivering updates to your application seamlessly. You can either bring your own deployment files for quick pipeline creation or generate Dockerfiles and Kubernetes manifests to containerize and deploy non-containerized applications with minimal effort.

## Prerequisites

- A GitHub account or an Azure DevOps organization.
- An AKS cluster. If you don't have one, you can create one using the steps in
[Deploy an Azure Kubernetes Service (AKS) cluster](learn/quick-kubernetes-deploy-portal). - An Azure Container Registry (ACR). If you don't have one, you can create one using the steps in
[Integrate Azure Container Registry (ACR) with an Azure Kubernetes Service (AKS) cluster](cluster-container-registry-integration). - An application to deploy.

### Connect to source code repository

Create an automated deployment workflow and authorize it to connect to the desired source code repository.

- In the Azure portal, navigate to your AKS cluster resource.
- From the service menu, under
**Settings**, select**Automated deployments**>**Create**. - Under
**Repository details**, enter a name for the workflow, then select**GitHub or ADO**for your repository location. - Select
**Authorize access**to connect to the desired repository. - Choose the
**Repository**and**Branch**, and then select**Next**.

### Choose the container image configuration

To get an application ready for Kubernetes, you need to build it into a container image and store it in a container registry. You use a Dockerfile to provide instructions on how to build the container image. If your source code repository doesn't already have a Dockerfile, Automated Deployments can generate one for you. Otherwise, you can use an existing Dockerfile.

Use Automated Deployments to generate a Dockerfile for many languages and frameworks such as Go, C#, Node.js, Python, Java, Gradle, Clojure, PHP, Ruby, Erlang, Swift, and Rust. The language support is built on what's available in [draft.sh](https://draft.sh).

- Select
**Auto-containerize (generate Dockerfile)**for the container configuration. - Select the
**location of where to save the generated Dockerfile**in the repository. - Select the
**application environment**from the list of supported languages and frameworks. - Enter the
**application port**. - Provide the
**Dockerfile build context**path. - Select an existing
**Azure Container Registry**or create a new one. This registry is used to store the built application image.

### Choose the Kubernetes manifest configuration

Note

The Generate Manifests option also supports advanced features like Service Connector integration, auto-generated Ingress resources, and more detailed, customizable Kubernetes manifest files.

An application running on Kubernetes consists of many Kubernetes primitive components. These components describe what container image to use, how many replicas to run, if there's a public IP required to expose the application, etc. For more information, see the official [Kubernetes documentation][kubernetes-documentation]. If your source code repository doesn't already have the basic Kubernetes manifests to deploy, Automated Deployments can generate them for you. Otherwise, you can use a set of existing manifests. You can also choose an existing Helm chart.

If your code repository already has a Dockerfile, you can select it to be used to build the application image.

- Select
**Use existing Kubernetes manifest deployment files**for the deployment options. - Select the
**Kubernetes manifest file or folder**from your repository. - Select
**Next**.

## (Optional) Use a managed ingress and/or Service Connector

When generating Kubernetes manifests with Automated Deployments, you can optionally enable App Routing to set up an ingress controller for your application. You can also use Service Connector to create a new connection or seamlessly integrate your app with an existing Azure service backend.

App Routing provides a fully managed NGINX-based ingress controller out of the box, complete with built-in SSL/TLS encryption using certificates stored in Azure Key Vault and DNS zone management through Azure DNS. When using Automated Deployments, the expose ingress command integrates seamlessly with App Routing, making it easy to expose your application to external traffic under a secure, custom DNS name—with minimal configuration.

- Select the
**Expose ingress**box. - Choose between an
**Existing ingress controller**or a**New ingress controller**. - Choose between using a
**SSL/TLS enabled**or**Insecure**ingress controller. - (Optional) Enter
**Certificate details**if choosing a**SSL/TLS enabled**ingress controller. - Choose between using
**Azure DNS**or a**3rd party provider**. - Enter the
**Azure DNS Zone**and**Subdomain name**.

## (Optional) Add environment variables

Define environment variables for a container in Kubernetes by specifying name-value pairs. Environment variables are important as they help enable easier management of settings, secure handling of sensitive information, and flexibility across environments.

## Review configuration and deploy

Review the configuration for the application, and Kubernetes manifests, then select **Deploy**. A pull request (PR) will be generated against the repository that you selected, so don't navigate away from deployment page.

### Review and merge pull request

When the deployment succeeds, select **View pull request** to view the details of the generated pull request on your code repository.

- Review the changes under
**Files changed**and make any desired edits. - Select
**Merge pull request**to merge the changes into your code repository.

Merging the change runs the GitHub Actions workflow that builds your application into a container image, stores it in Azure Container Registry, and deploys it to the cluster.

### Check the deployed resources

After the pipeline is completed, you can review the created Kubernetes `Service`

in the Azure portal by selecting **Services and ingresses** under the **Kubernetes resources** section of the service menu.

Selecting the **External IP** should open up a new browser page with the running application.

## Delete resources

Once you're done with your cluster, use the following steps to delete it to avoid incurring Azure charges:

- In the Azure portal, navigate to
**Automated deployments** - Select
**...**on the pipeline of your choice. - Select
**Delete**.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-dedicated-hosts -->

# Add Azure Dedicated Host to an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Dedicated Host is a service that provides physical servers - able to host one or more virtual machines - dedicated to one Azure subscription. Dedicated hosts are the same physical servers used in our data centers, provided as a resource. You can provision dedicated hosts within a region, availability zone, and fault domain. Then, you can place VMs directly into your provisioned hosts, in whatever configuration best meets your needs.

Using Azure Dedicated Hosts for nodes with your AKS cluster has the following benefits:

- Hardware isolation at the physical server level. No other VMs will be placed on your hosts. Dedicated hosts are deployed in the same data centers and share the same network and underlying storage infrastructure as other, non-isolated hosts.
- Control over maintenance events initiated by the Azure platform. While most maintenance events have little to no impact on your virtual machines, there are some sensitive workloads where each second of pause can have an impact. With dedicated hosts, you can opt in to a maintenance window to reduce the impact to your service.

## Before you begin

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Before you start, ensure that your version of the Azure CLI is 2.39.0 or later. If it's an earlier version,
[install the latest version](/en-us/cli/azure/install-azure-cli).

## Limitations

The following limitations apply when you integrate Azure Dedicated Host with Azure Kubernetes Service:

- Accelerated Networking
- An existing agent pool can't be converted from non-ADH to ADH or ADH to non-ADH.
- It isn't supported to update agent pool from host group A to host group B.
- Using ADH across subscriptions.

## Planning for ADH Capacity on AKS

Not all host SKUs are available in all regions, and availability zones. You can list host availability, and any offer restrictions before you start provisioning dedicated hosts.

```
az vm list-skus --location eastus --resource-type hostGroups/hosts -o table
```


Note

First, when using host group, the nodepool fault domain count is always the same as the host group fault domain count. In order to use cluster auto-scaling to work with ADH and AKS, please make sure your host group fault domain count and capacity is enough. Secondly, only change fault domain count from the default of 1 to any other number if you know what they are doing as a misconfiguration could lead to a unscalable configuration.

[Determine how many hosts you would need based on the expected VM Utilization](/en-us/azure/virtual-machines/dedicated-host-general-purpose-skus).

Evaluate [host utilization](/en-us/azure/virtual-machines/dedicated-hosts-how-to#check-the-status-of-the-host) to determine the number of allocatable VMs by size before you deploy.

```
az vm host get-instance-view --resource-group myDHResourceGroup --host-group MyHostGroup --name MyHost
```


## Add a Dedicated Host Group to an AKS cluster

A host group is a resource that represents a collection of dedicated hosts. You create a host group in a region and an availability zone, and add hosts to it. When planning for high availability, there are more options. You can use one or both of the following options with your dedicated hosts:

- Span across multiple availability zones. In this case, you're required to have a host group in each of the zones you wish to use.
- Span across multiple fault domains, which are mapped to physical racks.

In either case, you need to provide the fault domain count for your host group. If you don't want to span fault domains in your group, use a fault domain count of 1.

You can also decide to use both availability zones and fault domains.

## Create a Host Group

Now create a dedicated host in the host group. In addition to a name for the host, you're required to provide the SKU for the host. Host SKU captures the supported VM series and the hardware generation for your dedicated host.

For more information about the host SKUs and pricing, see [Azure Dedicated Host pricing](https://azure.microsoft.com/pricing/details/virtual-machines/dedicated-host/).

Use az vm host create to create a host. If you set a fault domain count for your host group, you'll be asked to specify the fault domain for your host.

In this example, we'll use [az vm host group create](/en-us/cli/azure/vm/host/group#az-vm-host-group-create) to create a host group using both availability zones and fault domains.

```
az vm host group create \
--name myHostGroup \
--resource-group myDHResourceGroup \
--zone 1 \
--platform-fault-domain-count 1 \
--automatic-placement true
```


## Create a Dedicated Host

Now create a dedicated host in the host group. In addition to a name for the host, you're required to provide the SKU for the host. Host SKU captures the supported VM series and the hardware generation for your dedicated host.

If you set a fault domain count for your host group, you'll need to specify the fault domain for your host.

```
az vm host create \
--host-group myHostGroup \
--name myHost \
--sku DSv3-Type1 \
--platform-fault-domain 1 \
--resource-group myDHResourceGroup
```


## Use a user-assigned Identity

Important

A user-assigned Identity with "contributor" role on the Resource Group of the Host Group is required.

First, create a Managed Identity

```
az identity create --resource-group <Resource Group> --name <Managed Identity name>
```


Assign Managed Identity

```
az role assignment create --assignee <id> --role "Contributor" --scope <Resource id>
```


## Create an AKS cluster using the Host Group

Create an AKS cluster, and add the Host Group you just configured.

```
az aks create \
--resource-group MyResourceGroup \
--name MyManagedCluster \
--location eastus \
--nodepool-name agentpool1 \
--node-count 1 \
--host-group-id <id> \
--node-vm-size Standard_D2s_v3 \
--assign-identity <id> \
--generate-ssh-keys
```


## Add a Dedicated Host Node Pool to an existing AKS cluster

Add a Host Group to an already existing AKS cluster.

```
az aks nodepool add --cluster-name MyManagedCluster --name agentpool3 --resource-group MyResourceGroup --node-count 1 --host-group-id <id> --node-vm-size Standard_D2s_v3
```


## Remove a Dedicated Host Node Pool from an AKS cluster

```
az aks nodepool delete --cluster-name MyManagedCluster --name agentpool3 --resource-group MyResourceGroup
```


## Next steps

In this article, you learned how to create an AKS cluster with a Dedicated host, and to add a dedicated host to an existing cluster. For more information about Dedicated Hosts, see [dedicated-hosts](/en-us/azure/virtual-machines/dedicated-hosts).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-communication-manager -->

# Set up the Azure Kubernetes Service communication manager

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Kubernetes Service (AKS) communication manager streamlines notifications for all your AKS maintenance tasks by using Azure Resource Notifications and Azure Resource Graph frameworks. The communication manager gives you timely alerts on event triggers and outcomes, so that you can closely monitor your upgrades.

If maintenance fails, the communication manager notifies you with the reasons for the failure. This information reduces operational hassles related to observability and follow-ups.

By following the steps in this article, you can set up notifications for all types of automatic upgrades that use maintenance windows.

## Prerequisites

Configure your cluster for either the

[automatic upgrade channel](auto-upgrade-cluster)or the[automatic upgrade channel for nodes](auto-upgrade-node-os-image).Create a

[planned maintenance window](planned-maintenance)for your configuration of automatic upgrades.

## Set up the communication manager

In the Azure portal, go to the resource.

Select

**Monitoring**>**Alerts**>**Alert Rules**, and then select**Create**.On the

**Condition**tab, for**Signal name**, select**Custom log search**.In the

**Search query**box, paste one of the following custom queries. Be sure to update the`where id contains`

path to reference your resources for subscription ID, resource group name, and cluster name.The following query is for notifications of automatic upgrades for clusters:

`arg("").containerserviceeventresources | where type == "microsoft.containerservice/managedclusters/scheduledevents" | where id contains "/subscriptions/<subid>/resourcegroups/<rgname>/providers/Microsoft.ContainerService/managedClusters/<clustername>" | where properties has "eventStatus" | extend status = substring(properties, indexof(properties, "eventStatus") + strlen("eventStatus") + 3, 50) | extend status = substring(status, 0, indexof(status, ",") - 1) | where status != "" | where properties has "eventDetails" | extend upgradeType = case( properties has "K8sVersionUpgrade", "K8sVersionUpgrade", properties has "NodeOSUpgrade", "NodeOSUpgrade", "" ) | extend details = parse_json(tostring(properties.eventDetails)) | where properties has "lastUpdateTime" | extend eventTime = substring(properties, indexof(properties, "lastUpdateTime") + strlen("lastUpdateTime") + 3, 50) | extend eventTime = substring(eventTime, 0, indexof(eventTime, ",") - 1) | extend eventTime = todatetime(tostring(eventTime)) | where eventTime >= ago(30m) // Ensure this matches aggregation granularity & frequency | where upgradeType == "K8sVersionUpgrade" | project eventTime, upgradeType, status, properties, name, details | order by eventTime asc`

The following query is for notifications of automatic upgrades for NodeOS:

`arg("").containerserviceeventresources | where type == "microsoft.containerservice/managedclusters/scheduledevents" | where id contains "/subscriptions/<subid>/resourcegroups/<rgname>/providers/Microsoft.ContainerService/managedClusters/<clustername>" | where properties has "eventStatus" | extend status = substring(properties, indexof(properties, "eventStatus") + strlen("eventStatus") + 3, 50) | extend status = substring(status, 0, indexof(status, ",") - 1) | where status != "" | where properties has "eventDetails" | extend upgradeType = case( properties has "K8sVersionUpgrade", "K8sVersionUpgrade", properties has "NodeOSUpgrade", "NodeOSUpgrade", "" ) | extend details = parse_json(tostring(properties.eventDetails)) | where properties has "lastUpdateTime" | extend eventTime = substring(properties, indexof(properties, "lastUpdateTime") + strlen("lastUpdateTime") + 3, 50) | extend eventTime = substring(eventTime, 0, indexof(eventTime, ",") - 1) | extend eventTime = todatetime(tostring(eventTime)) | where eventTime >= ago(30m) // Ensure this matches aggregation granularity & frequency | where upgradeType == "NodeOSUpgrade" | project eventTime, upgradeType, status, properties, name, details | order by eventTime asc`

Go to the

**Condition**tab. Configure the alert conditions with the following settings:**Measure**: Select**Table rows**.**Aggregation type**: Select**Count**.**Aggregation granularity**: Select**30 minutes**.**Threshold value**: Keep at**0**.**Split by dimensions**: For**Dimension name**, select**status**. Then select the**Include all future values**checkbox.

In the

**Split by dimensions**area, for**Dimension values**, select a value. Because you selected**status**for the dimension name, the available values are**Scheduled**,**Started**,**Completed**,**Canceled**, and**Failed**.Note

These status values appear only if your cluster previously executed automatic upgrade operations. For new clusters or for clusters that haven't undergone automatic upgrades yet, the dropdown list might appear empty or show no available dimensions. After your cluster performs its first automatic upgrade, these status values become available for selection.

Go to the

**Actions**tab. Make sure that an action group with the correct email address exists, so that you can receive the notifications:Select

**Use action groups**>**Create an action group**.For

**Notification type**, select**Email/SMS_message/Push/Voice**.Select the

**Email**checkbox, and then enter the email address in the**Email**box.

Go to the

**Details**tab. Assign a managed identity so that you can grant access to the necessary resources. In the**Identity**area, select**System assigned managed identity**.Go to the

**Review + create**tab, and then select**Create**.Now that you've created the alert rule, you can assign the appropriate roles for the managed identity:

- In the alert rule, go to
**Settings**>**Identity**>**System assigned managed identity**>**Azure role assignments**. - Select
**Add role assignment**, select the**Reader**role, and assign it to the resource group. - Select
**Add role assignment**again, select the**Reader**role, and assign it to the subscription.

Tip

If you don't see the

**Identity**option, make sure that you created your alert rule and that you have the necessary permissions.- In the alert rule, go to

After you set up the communication manager, it sends advance notices one week before maintenance starts and one day before maintenance starts. It also sends you timely alerts during the maintenance operation.

## Verify the configuration

To upgrade the cluster, wait for the automatic upgrader to start. Then verify that you promptly receive notices on the email address that you configured to receive notices.

Check the Azure Resource Graph database for the scheduled notification record. Each scheduled event notification should be listed as one record in the `ContainerServiceEventResources`

table.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-l7-policy-concepts -->

# Overview of Layer 7 (L7) policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Network policies are essential for securing Kubernetes clusters by defining and controlling pod communication. They mitigate unauthorized access and potential security breaches by regulating traffic flow. Advanced Container Networking Services strengthens security with [FQDN-based network policies](container-network-security-fqdn-filtering-concepts). Expanding on this foundation, Advanced Container Networking Services now provides L7 policy support, enabling detailed inspection and management of application-level traffic. This advancement enhances both the security and efficiency of network communications within AKS clusters. The offering includes comprehensive support for widely adopted protocols, including HTTP, gRPC, and Kafka.

## Components of L7 policy

**Envoy proxy**: Envoy, part of ACNS security agent acts as the enforcement point for L7 policies. A TPROXY inspects application traffic, comparing it against the defined L7 policies. To enhance scalability and resource management, Envoy is deployed as a separate DaemonSet, decoupled from the Cilium Agent.

## How L7 policy works

When L7 policy enforcement is enabled for an application or pod, outgoing network traffic is first evaluated to determine compliance with the configured application-level rules. The eBPF probe attached to the source pod’s network interface marks the packets, which are then redirected to a node-local Envoy Proxy. This redirection occurs only for pods enforcing L7 policies, ensuring that policy enforcement is applied selectively.

The Envoy proxy, augmented with Cilium network filters, then decides whether to forward the traffic to the destination pod based on policy criteria. If permitted, the traffic proceeds; if not, Envoy returns an appropriate error code to the originating pod. Upon successful authorization, the Envoy proxy facilitates the traffic flow, providing application-level visibility and control. This allows the Cilium agent to enforce detailed network policies within the policy engine. The following diagram illustrates the high-level flow of L7 policy enforcement.

## Monitoring L7 traffic with Hubble and Grafana

To gain insights into L7 traffic flows, specifically HTTP, gRPC, and Kafka, Azure CNI Powered by Cilium leverages Hubble agent, which is enabled by default with Advanced Container Networking Services. Hubble provides detailed flow-level metrics.

To simplify the analysis of these L7 metrics, we provide pre-configured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

These dashboards offer granular visibility into L7 flow data at the cluster, namespace, and workload levels.

Note

These dashboards will only display data if you have this feature enabled on your cluster and have relevant policies applied.
Additionally, the monitoring metrics are **not** required to flow through Envoy, a component of the ACNS security agent. Rather, these metrics are collected by the Hubble agent, which is installed on your cluster as part of the Advanced Container Networking Service's observability feature.

## Key benefits

**Granular Application-Level Control**: L7 policies allow for fine-grained control over network traffic based on application-specific attributes, such as HTTP methods, gRPC paths, and Kafka topics. This extends beyond the basic IP address and port-based control of traditional network policies.

**Enhanced Security**: By inspecting application-level traffic, L7 policies can prevent attacks that exploit vulnerabilities at the application layer. This includes blocking unauthorized access to specific APIs or services. Furthermore, L7 policies are an important component of a Zero Trust security strategy, enabling the enforcement of the principle of least privilege at the application layer.

**Graceful Error Handling**: Unlike L3/L4 policies that typically drop unauthorized traffic silently, L7 policies can return application-level error codes (for example, HTTP 403, Kafka authorization failures), allowing applications to handle errors more gracefully.

**Observability**: With observability enabled for Advanced Container Networking Services and L7 policies applied to your AKS cluster, you can monitor traffic and policy effectiveness using Grafana dashboards.

## Limitations and considerations

- Current feature support relies on Cilium's Layer 7 policy enforcement based on HTTP, HTTPS, gRPC, and Kafka.
- The maximum supported cluster size is up to 1,000 nodes or 40,000 pods, whichever is greater.
- Traffic traversing Envoy proxies do come with latency. Users may experience noticeable latency degradation beyond 3,000 requests per second.
- As part of our observability solution, we provide envoy_http_rq_total metrics. These metrics give the total request count, which could be used to derive requests per seconds (rps).
- During a Cilium upgrade or rollout, existing sessions can be gracefully closed. Applications are expected to handle these interruptions gracefully—typically by implementing retry mechanisms at the connection or request level. New connections initiated during the rollout aren't impacted.
- L7 policy isn't supported by CiliumClusterwideNetworkPolicy(CCNP).
- L7 policy through Advanced Container Networking Services (ACNS) isn't compatible with L7 policies implemented via alternate methods such as Istio. The following table summarizes the supported scenarios.

| Feature/Component | L7 Policies using AKS, Istio - Managed addon |
|---|---|
| K8s network policies by Azure CNI powered by Cilium | Supported |
| L4 (FQDN) Policies by Azure CNI powered by Cilium and ACNS | Supported |
| L7 (HTTP(s)/GRPC/Kafka) Policies by Azure CNI powered by Cilium and ACNS | Not Supported |

## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[L7 policies](how-to-apply-l7-policies)on AKS.Explore how the open source community builds

[Cilium Network Policies](https://docs.cilium.io/en/latest/security/policy/).For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](advanced-container-networking-services-overview#container-network-observability)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/considerations-pod-sandboxing -->

# Pod Sandboxing considerations

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For Pod Sandboxing deployments on Azure Kubernetes Service (AKS) there are several items to consider in regard to resource management, memory management, CPU management, and security.

## Resource management

Memory and CPU management behavior with Pod Sandboxing might be unfamiliar to some users. These considerations are relevant when specifying resources in a deployment, especially for larger and resource sensitive workloads.

### Kata components

In a Kata deployment, there are generally two families of components that get deployed. You have **host components** and **guest components**.

- The main
**host components**comprise of the*Kata shim*,*Cloud Hypervisor*, and*virtiofsd*.- The
*Kata shim*manages a pod VM lifecycle. *Cloud Hypervisor*is the Virtual Machine Monitor (VMM) used by the Kata shim.*virtiofsd*is a daemon used to share files between each Pod VM and its container host.

- The
- The main
**guest components**include the*user's workloads*,*pod VM kernel*, and the*Kata agent*.- The
*Kata agent*manages containers inside of the Pod VMs

- The

### Memory management

With Kata pods, you have the ability to specify the amount of memory of the Pod VM that hosts your workloads. It's crucial that you configure the values accordingly so that a pod has sufficient resources, but doesn't result in unused memory being allocated to the pod.

### Pod VM memory size

There's an amount of memory allocated to each pod VM that runs a container. This VM memory size is inclusive of all the memory necessary to run Kata guest components. Users should take care to ensure that they buffer some extra memory beyond the expected consumption of their workloads to account for the consumption of other guest components, such as the kata agent or VM kernel. Examples are given on typical memory values later on in this article.

The pod VM memory size is equivalent to the [Kubernetes pod memory limit](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/#specify-a-memory-request-and-a-memory-limit) the user specifies. A user can change the value by changing their pod memory limit; if no values are specified, a default size of 512Mi is applied. Once the pod starts, this size becomes fixed.

As the pod VM memory size increases, the runtime class memory overhead should be expected to increase alongside it.

### Runtime class memory overhead

Pod Sandboxing workloads come with a default kata runtime class (`kata-vm-isolation`

) which comes with default overheads for resources. Users that want finer grain control of their resource quotas can [set up a custom runtime class](https://kubernetes.io/docs/concepts/containers/runtime-class/#setup) with specific resource overheads. When doing so, users should ensure that the memory overhead value of the runtime class is enough that covers all expected usage for the **host components** of a kata deployment. The runtime class memory overhead does *not* need to account for the expected memory consumption of the **guest components**.

You can create a specialized runtime and specify the memory overhead in your runtime class through the `overhead`

field in your `RuntimeClass`

manifest. [As an example](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/#usage-example), let's assume I want to create a runtime for workloads I expect to be smaller in consumption:

```
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
name: small-kata-pods
handler: kata
overhead:
podFixed:
memory: "120Mi"
```


Specifying overheads isn't required, and suggested if you want finer control over the resources being set aside for your workloads. If you use the default `kata-vm-isolation`

runtime class and don't specify any overheads in your YAML, the overhead of the Pod VM size defaults to 512Mi and the runtime class overhead defaults to 600Mi. This default runtime overhead is calculated with the default pod VM size (512Mi) plus to approximate memory needed by host components for such a VM size (~88Mi).

### User workloads

When a user deploys a Kata workload, they're able to use memory up to the configured *pod VM memory size* minus the other guest components, such as the Kata agent or the guest VM kernel.

If you would like to get an approximation of the memory used by these components:

- Connect to the pod VM (either via
`kubectl exec`

or`kubectl debug`

to open a shell inside your pod). - Run the
`free`

command. - Inspect the "used" column in the output to get an idea of the memory consumed by the guest kernel/kata agent.

### Memory cgroups

When a Kata pod is scheduled to run, kubelet assigns the pod to a memory `cgroup`

. This `cgroup`

enforces the pod's memory limits/requests, allowing a user to define the resource quotas available to a pod.

Within the memory `cgroup`

, there are two important fields to consider:

`memory.current`

defines how many bytes of memory the host components and the pod VM memory size allocates.`memory.max`

optional, user defined upper limit of memory.current for pods where users want to impose a memory limit.- The kubelet computes this value as the sum of a pod's memory limit and its runtime class memory overhead.


At any point, if the `memory.current`

value exceeds that of `memory.max`

, [the kernel might trigger an OOMKill on the pod if memory pressure is detected](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#requests-and-limits).

### Reference usage values

Users can utilize these values to serve as a reference for the typical memory usage and values across the different variables covered. Pod VM memory sizes under 128Mi aren't supported.

| Pod VM Memory Size | Runtime class overhead | memory.current | memory.max | Free memory available to Host components |
|---|---|---|---|---|
| 128Mi | 16Mi | 133Mi | 144Mi | 11Mi |
| 256Mi | 32Mi | 263Mi | 288Mi | 25Mi |
| 1Gi | 128Mi | 1034Mi | 1152Mi | 118Mi |
| 2Gi | 256Mi | 2063Mi | 2304Mi | 241Mi |
| 4Gi | 374Mi | 4122Mi | 4470Mi | 348Mi |
| 8Gi | 512Mi | 8232Mi | 8704Mi | 472Mi |
| 32Gi | 640Mi | 32918Mi | 33408Mi | 490Mi |
| 64Gi | 768Mi | 65825Mi | 66304Mi | 479Mi |
| 96Gi | 896Mi | 98738Mi | 99200Mi | 462Mi |
| 128Gi | 1Gi | 131646Mi | 132096Mi | 450Mi |

## CPU management

In a similar vein to memory, you can also allocate CPU resources to your Kata workloads. Doing so is recommended; without declaring a CPU limit for your Kata pod, Kata host components are able to use any CPU capacity available on the node.

### Reserving CPU

When reserving CPUs for your Kata workloads, you have two fields you can choose to set.

- The
*runtime class CPU overhead* - The
*pod CPU limit*

When at least one of the two values is specified, the control plane reserves the specified number of CPUs on the node for your workload. Other pods on the same node can't access this reserved capacity.

### Pod CPU limit

You can declare your [pod CPU limit](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/) in your application's manifest. A specified pod CPU limit defines the limit of the CPUs that containers in the associated pod VM can use.

If you specify fractions of CPUs for the pod CPU limit, those fractions will get rounded up to the next integer. The rounded up number becomes the number of vCPUs allocated to the Pod VM, but a `cgroup`

will limit the workload to only consume the fraction specified in the pod CPU limit.

If no number is declared, one vCPU will be allocated to the pod VM if the capacity is available on the node. There's no limit on the CPU consumption of the Kata host components.

### Runtime class CPU overhead

The runtime class overhead should be specified if you'd like to preemptively reserve some node capacity for the Kata host components.

You can specify the memory overhead in your runtime class through the `overhead`

field in your `RunTimeClass`

manifest. [As an example](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/#usage-example):

```
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
name: custom-kata-runtime
handler: kata
overhead:
podFixed:
cpu: "250m"
```


### Best practices

#### Memory management

- Ensure you specify pod VM memory sizes (defined by the
`limits.memory`

in your manifest) and suitable resource quotas for all your deployments.- Ensure you use a nonzero
*pod request*if you want to ensure that some node capacity is reserved for the pod VM before that VM starts up. The request should account for the pod VM and containers that are expected to run on it. - Ensure you use a nonzero
*runtime class overhead*if you want to reserve some node capacity for the Kata host components before those components start up.

- Ensure you use a nonzero
- If you expect your pod workloads to be especially resource hungry, you can specify limits accordingly for the pod VM to ensure that there are ample resources available for your workloads.
- Declare a suitable runtime class memory overhead such that it gives enough memory for your host components but doesn't take too much to avoid allocating unused memory.

#### CPU management

If your node typically has plenty of free CPU capacity, these reservations might be unnecessary.

If your nodes typically run to the limit with CPU consumption, then a nonzero reservation ensures your pods can be executed more reliably.

- You can utilize pod CPU requests to ensure that some CPU node capacity is reserved for the Kata host components. Reserved capacity for a specific workload is
*not*available to other workloads on the node.

- You can utilize pod CPU requests to ensure that some CPU node capacity is reserved for the Kata host components. Reserved capacity for a specific workload is
Make sure you specify CPU requests that your infrastructure can accommodate. If your available capacity runs near 0, or your request is too large, your workloads might

[fail to start](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/#specify-a-cpu-request-that-is-too-big-for-your-nodes)Align your CPU requests with your CPU limits. The Kata shim doesn't have visibility into requests. Therefore, if no CPU limit is declared, the pod VM is limited to one vCPU. The Kata host components, which do have visibility into request values, consumes the rest of the requested CPU count and have no limit to CPU consumption.

Reserved capacity for a specific workload is

*not*available to other workloads on the node.

### Example declarations

| Runtime class CPU overhead | Pod CPU Request/Limit | Expected behavior |
|---|---|---|
| 1 | 1 | The control plane reserves two CPUs on the node. The pod VM gets one CPU, and containers on the pod can use up to the one vCPU capacity. The Kata host components and pod VM together can use up to two CPUs from the reserved capacity on the node. |
| 1 | 2.5 | The control plane reserves 3.5 CPUs on the node. The pod VM gets three vCPUs, but containers on the pod VM can use up to 2.5 vCPU capacity. The Kata host components and pod VM together can use up to 3.5 CPUs from the reserved capacity on the node. |
| None | 1 | The control plane reserves one CPU on the node. The pod VM gets one vCPU, and containers on the pod VM can use up to one vCPU capacity. The Kata host components and the pod VM together are allowed to use up to one CPU from the reserved capacity on the node. One CPU is always available to the pod VM due to the CPU request. |
| 1 | None | The control plane reserves one CPU on the node. The pod VM gets one vCPU, and containers on the pod VM can use up to one vCPU capacity. The kata host components and the pod VM can use any CPU capacity available on the node. At least one CPU is always available due to the overhead reservation. |

## Security

Pod Sandboxing offers users a compelling option to isolate their workloads from other workloads and the host. There are, nonetheless, important security concerns that should be taken into account.

### Privileged pods

There are scenarios in which privileged pods might be required. Users are able to spin up privileged pods, but no [host devices are attached to the pod](https://github.com/kata-containers/kata-containers/blob/main/docs/how-to/privileged.md#containerd).

Using privileged containers lead to root access in the guest VM, but remain isolated from the host.

Privileged pods, even on Pod Sandboxing, should only be used when necessary. Privileged pods should continue to be [managed by trusted users](https://kubernetes.io/docs/concepts/security/pod-security-standards/#privileged).

### Host path storage volumes

`hostPath`

volumes can be mounted into Kata pods. In Pod Sandboxing, using `hostPath`

volumes can potentially undermine the isolation that Kata provides; since part of the host filesystem is exposed directly to the container, a potential attack vector is opened. The warnings posed by [upstream](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath) should be considered as relevant for Pod Sandboxing as well.

There are some exceptions; files under `/dev`

are mounted into the container from the guest system instead of the host system. This helps maintain pod isolation for situations where this path must be mounted to function.

Warning

Unless necessary, the recommendation is to *avoid* using hostPath storage volumes.

#### Blocking hostPath via Azure Policy

[Azure Policy](/en-us/azure/governance/policy/concepts/policy-for-kubernetes) allows users to apply at-scale enforcements and safeguards on their cluster components in a centralized, consistent manner.

There is a set of [built-in policy sets](policy-reference) for AKS that enforce best practices. Users can take advantage of one of these policies to block deployments that attempt to mount hostPaths.

## Next steps

Once you're ready, learn how to [deploy pod sandboxing on AKS](use-pod-sandboxing).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/control-plane-metrics-monitor -->

# Monitor Azure Kubernetes Service control plane metrics (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to monitor the Azure Kubernetes Service (AKS) control plane by using control plane metrics in Azure Monitor.

AKS supports a subset of control plane metrics free through [Azure Monitor platform metrics](monitor-aks#aks-monitoring-data-metrics-logs-integrations). The control plane metrics feature gives you visibility into the availability and performance of critical control plane components like the API server, etcd, the scheduler, the autoscaler, and the controller manager in AKS. The feature is also fully compatible with the managed service for Prometheus and Azure Managed Grafana. You can use these metrics to maximize overall observability and to maintain operational excellence for your AKS cluster.

## Control plane platform metrics

AKS offers some free control plane metrics for monitoring the API server and etcd. These metrics are automatically collected for all AKS clusters at no cost. You can analyze the metrics by using the [metrics explorer](/en-us/azure/azure-monitor/essentials/analyze-metrics) in the Azure portal. You can also create metrics-based alerts by using the metrics data.

To see the full list of supported control plane platform metrics, see the [AKS monitoring reference](monitor-aks-reference#metrics).

## Prerequisites and limitations

- The control plane metrics (preview) feature supports only the
[managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)in Azure Monitor. [Azure Private Link](/en-us/azure/azure-monitor/logs/private-link-security)isn't supported.- You can customize only the default
configmap file. No other customization is supported.`ama-metrics-settings-configmap.yaml`

- Your AKS cluster must use
[managed identity authentication](use-managed-identity).

### Install the aks-preview extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install or update the

`aks-preview`

Azure CLI extension by using theor`az extension add`

command:`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the AzureMonitorMetricsControlPlanePreview feature flag

Register the

`AzureMonitorMetricsControlPlanePreview`

feature flag by using thecommand:`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`

It takes a few minutes for the status to show as

**Registered**.Verify the registration status by using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`

When the status is

**Registered**, refresh the registration of the Microsoft.ContainerService resource provider by using thecommand:`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`


## Enable control plane metrics on an AKS cluster

Enable control plane metrics by using the managed service for Prometheus add-on when you create a new cluster or update an existing cluster.

Note

Unlike the metrics that are collected from cluster nodes, control plane metrics are collected by a component that isn't part of the `ama-metrics`

add-on. Enabling the `AzureMonitorMetricsControlPlanePreview`

feature flag and the managed service for Prometheus add-on ensures that control plane metrics are collected. After you enable metrics collection, it can take several minutes for the data to appear in the workspace.

### New AKS cluster

To learn how to collect managed service for Prometheus metrics from your AKS cluster, see [Enable Prometheus and Grafana for AKS clusters](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana). For an AKS cluster, complete the steps described on the **CLI** tab.

### Existing AKS cluster

If your cluster already has the managed service for Prometheus add-on, update the cluster to ensure that it collects control plane metrics by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command:

```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Query control plane metrics

Control plane metrics are stored in an Azure Monitor workspace in the cluster's region. You can query the metrics directly in the workspace or by using the Azure Managed Grafana instance that's connected to the workspace.

In the

[Azure portal](https://portal.azure.com), go to your AKS cluster resource.On the left menu, select

**Monitor**>**Monitor Settings**.Go to the Azure Monitor workspace that is linked to the cluster.

In the Azure Monitor workspace, under

**Managed Prometheus**, query the metrics by using the Prometheus explorer.

Note

AKS provides dashboard templates to help you view and analyze your control plane telemetry data in real time. If you use Azure Managed Grafana to visualize the data, you can import the following dashboards:

## Customize control plane metrics

AKS includes a preconfigured set of metrics to collect and store for each component. Metrics for the API server and etcd are collected by default. You can customize the list of metrics that are collected by modifying the [ ama-metrics-settings-configmap.yaml](https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) configmap file.

Default targets include the following values:

```
controlplane-apiserver = true
controlplane-cluster-autoscaler = false
controlplace-node-auto-provisioning = false
controlplane-kube-scheduler = false
controlplane-kube-controller-manager = false
controlplane-etcd = true
```


All configmap files should be applied to the `kube-system`

namespace for any cluster.

### Customize an ingestion profile

You can customize an ingestion file for collected metrics. For more information, see [Minimal ingestion profile for control plane metrics in managed service for Prometheus](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal#minimal-ingestion-for-default-on-targets).

#### Ingest only minimal metrics from default targets

- Set
`default-targets-metrics-keep-list.minimalIngestionProfile`

to`true`

, so it ingests only the minimal set of metrics for each of the default targets:`controlplane-apiserver`

and`controlplane-etcd`

.

#### Ingest all metrics from all targets

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`false`

.Under

`default-scrape-settings-enabled`

, verify that the targets you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplace-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Apply the configmap file by using the

command:`kubectl apply`

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

#### Ingest more than minimal metrics

Using the `minimalingestionprofile`

setting helps reduce the ingestion volume of metrics. If set to `true`

, only default recording rules, default alerts, and metrics that appear in the default dashboards are collected.

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`true`

.Under

`default-scrape-settings-enabled`

, verify that the targets you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Under

`default-targets-metrics-keep-list`

, specify the list of metrics for the`true`

targets.For example:

`controlplane-apiserver= "apiserver_admission_webhook_admission_duration_seconds|apiserver_longrunning_requests"`

Apply the configmap file by using the

command:`kubectl apply`

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

#### Ingest specific metrics from specific targets

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`false`

.Under

`default-scrape-settings-enabled`

, verify that the targets that you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Under

`default-targets-metrics-keep-list`

, specify the list of metrics for the`true`

targets.For example:

`controlplane-apiserver= "apiserver_admission_webhook_admission_duration_seconds|apiserver_longrunning_requests"`

Apply the configmap file:

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

## Troubleshoot control plane metrics issues

Make sure that the `AzureMonitorMetricsControlPlanePreview`

feature flag is enabled and that the `ama-metrics`

pods are running.

Note

The [troubleshooting methods](/en-us/azure/azure-monitor/containers/prometheus-metrics-troubleshoot) for the managed service for Prometheus don't apply directly in this scenario. The components that scrape the control plane aren't included in the managed service for Prometheus add-on.

**Configmap file formatting**: Make sure that you use the correct formatting in the configmap file. Verify that the fields`default-targets-metrics-keep-list`

,`minimal-ingestion-profile`

, and`default-scrape-settings-enabled`

and other fields are correctly populated with their intended values.**Isolate the control plane from the data plane**: Start by setting some of the[node-related metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default)to`true`

, and then verify that the metrics are forwarded to the workspace. Completing these steps helps you determine whether an issue is specific to scraping control plane metrics.**A change in the number of events ingested**: After you apply the changes, you can open the metrics explorer in the Azure portal. Go to the Azure Monitor overview pane for the cluster or go to the**Monitoring**section of the selected cluster. Check for an increase or a decrease in the number of events ingested per minute. This information can help you determine whether a specific metric is missing or if all metrics are missing.**A specific metric isn't exposed**: In some scenarios, a metric is documented, but it isn't exposed from the target and isn't forwarded to the Azure Monitor workspace. In this case, it's necessary to verify that other metrics are forwarded to the workspace.Note

If you want to collect the

`apiserver_request_duration_seconds`

metric or another bucket metric, you must set the entire series in the histogram family:`controlplane-apiserver = "apiserver_request_duration_seconds_bucket|apiserver_request_duration_seconds_sum|apiserver_request_duration_seconds_count"`

**No access to the Azure Monitor workspace**: When you enable the add-on, you might specify an existing workspace that you can't access. In that scenario, it appears that metrics aren't collected and forwarded. Make sure that you create a new workspace to use to collect metrics when you enable the add-on or when you create the cluster.

## Disable control plane metrics on your AKS cluster

You can disable control plane metrics at any time by disabling the managed service for Prometheus add-on and unregistering the `AzureMonitorMetricsControlPlanePreview`

feature flag.

Remove the metrics add-on that scrapes Prometheus metrics by using the

command:`az aks update`

`az aks update --disable-azure-monitor-metrics --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP`

To disable scraping control plane metrics on the AKS cluster, unregister the

`AzureMonitorMetricsControlPlanePreview`

feature flag via thecommand:`az feature unregister`

`az feature unregister "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`


## Frequently asked questions

### Can I scrape control plane metrics by using self-hosted Prometheus?

No. Currently, you can't scrape control plane metrics by using self-hosted Prometheus. Self-hosted Prometheus can scrape only a single instance, depending on the load balancer, so the metrics aren't reliable. Often, multiple replicas of the control plane metrics are visible only through the managed service for Prometheus.

### Why isn't the user agent available in the control plane metrics?

In AKS, [control plane metrics](https://kubernetes.io/docs/reference/instrumentation/metrics/) don't have the user agent. The user agent is available only through the control plane logs that you access in [diagnostic settings](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-network -->

# Best practices for network connectivity and security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

As you create and manage clusters in Azure Kubernetes Service (AKS), you provide network connectivity for your nodes and applications. These network resources include IP address ranges, load balancers, and ingress controllers.

This best practices article focuses on network connectivity and security for cluster operators. In this article, you learn how to:

- Explain Azure Container Networking Interface (CNI) network mode in AKS.
- Plan for required IP addressing and connectivity.
- Distribute traffic using load balancers, ingress controllers, or a web application firewall (WAF).
- Securely connect to cluster nodes.

## Choose the appropriate network model


Best practice guidanceUse Azure CNI networking in AKS for integration with existing virtual networks or on-premises networks. This network model allows greater separation of resources and controls in an enterprise environment.


Virtual networks provide the basic connectivity for AKS nodes and customers to access your applications. There are two different ways to deploy AKS clusters into virtual networks:

**Azure CNI networking**: Deploys into a virtual network and uses the[Azure CNI](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md)Kubernetes plugin. Pods receive individual IPs that can route to other network services or on-premises resources.

Azure CNI is a valid option for production deployments.

### CNI Networking

Azure CNI is a vendor-neutral protocol that lets the container runtime make requests to a network provider. It assigns IP addresses to pods and nodes, and provides IP address management (IPAM) features as you connect to existing Azure virtual networks. Each node and pod resource receives an IP address in the Azure virtual network. There's no need for extra routing to communicate with other resources or services.

Notably, Azure CNI networking for production allows for separation of control and management of resources. From a security perspective, you often want different teams to manage and secure those resources. With Azure CNI networking, you connect to existing Azure resources, on-premises resources, or other services directly via IP addresses assigned to each pod.

When you use Azure CNI networking, the virtual network resource is in a separate resource group to the AKS cluster. Delegate permissions for the AKS cluster identity to access and manage these resources. The cluster identity used by the AKS cluster must have at least [Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor) permissions on the subnet within your virtual network.

If you wish to define a [custom role](/en-us/azure/role-based-access-control/custom-roles) instead of using the built-in Network Contributor role, the following permissions are required:

`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


By default, AKS uses a managed identity for its cluster identity. However, you can use a service principal instead.

- For more information about AKS service principal delegation, see
[Delegate access to other Azure resources](kubernetes-service-principal#delegate-access-to-other-azure-resources). - For more information about managed identities, see
[Use managed identities](use-managed-identity).

As each node and pod receives its own IP address, plan out the address ranges for the AKS subnets. Keep the following criteria in mind:

- The subnet must be large enough to provide IP addresses for every node, pod, and network resource you deploy.
- With Azure CNI networking, each running node has default limits to the number of pods.

- Avoid using IP address ranges that overlap with existing network resources.
- It's necessary to allow connectivity to on-premises or peered networks in Azure.

- To handle scale-out events or cluster upgrades, you need extra IP addresses available in the assigned subnet.
- This extra address space is especially important if you use Windows Server containers, as those node pools require an upgrade to apply the latest security patches. For more information on Windows Server nodes, see
[Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

- This extra address space is especially important if you use Windows Server containers, as those node pools require an upgrade to apply the latest security patches. For more information on Windows Server nodes, see

To calculate the IP address required, see [Configure Azure CNI networking in AKS](configure-azure-cni).

When creating a cluster with Azure CNI networking, you specify other address ranges for the cluster, such as the Docker bridge address, DNS service IP, and service address range. In general, make sure these address ranges don't overlap each other or any networks associated with the cluster, including any virtual networks, subnets, on-premises and peered networks.

For the specific details around limits and sizing for these address ranges, see [Configure Azure CNI networking in AKS](configure-azure-cni).

## Distribute ingress traffic


Best practice guidanceTo distribute HTTP or HTTPS traffic to your applications, use ingress resources and controllers. Compared to an Azure load balancer, ingress controllers provide extra features and can be managed as native Kubernetes resources.


While an Azure load balancer can distribute customer traffic to applications in your AKS cluster, it's limited in understanding that traffic. A load balancer resource works at *layer 4* and distributes traffic based on protocol or ports.

Most web applications using HTTP or HTTPS should use Kubernetes ingress resources and controllers, which work at *layer 7*. Ingress can distribute traffic based on the URL of the application and handle TLS/SSL termination. Ingress also reduces the number of IP addresses you expose and map.

With a load balancer, each application typically needs a public IP address assigned and mapped to the service in the AKS cluster. With an ingress resource, a single IP address can distribute traffic to multiple applications.

There are two components for ingress:

- An ingress
*resource* - An ingress
*controller*

### Ingress resource

The *ingress resource* is a YAML manifest of `kind: Ingress`

. It defines the host, certificates, and rules to route traffic to services running in your AKS cluster.

The following example YAML manifest distributes traffic for *myapp.com* to one of two services, *blogservice* or *storeservice*, and directs the customer to one service or the other based on the URL they access.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: myapp-ingress
spec:
ingressClassName: PublicIngress
tls:
- hosts:
- myapp.com
secretName: myapp-secret
rules:
- host: myapp.com
http:
paths:
- path: /blog
backend:
service:
name: blogservice
port: 80
- path: /store
backend:
service:
name: storeservice
port: 80
```


### Ingress controller

An *ingress controller* is a daemon that runs on an AKS node and watches for incoming requests. Traffic is then distributed based on the rules defined in the ingress resource. While the most common ingress controller is based on [NGINX](https://www.nginx.com/products/nginx/kubernetes-ingress-controller), AKS doesn't restrict you to a specific controller. You can use [Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview), [Contour](https://github.com/heptio/contour), [HAProxy](https://www.haproxy.org), [Traefik](https://github.com/containous/traefik), etc.

Ingress controllers must be scheduled on a Linux node. Indicate that the resource should run on a Linux-based node using a node selector in your YAML manifest or Helm chart deployment. For more information, see [Use node selectors to control where pods are scheduled in AKS](concepts-clusters-workloads#node-selectors).

## Ingress with the application routing addon

The application routing addon is the recommended way to configure an Ingress controller in AKS. The application routing addon is a fully managed, ingress controller for Azure Kubernetes Service (AKS) that provides the following features:

Easy configuration of managed NGINX Ingress controllers based on Kubernetes NGINX Ingress controller.

Integration with Azure DNS for public and private zone management.

SSL termination with certificates stored in Azure Key Vault.


For more information about the application routing add-on, see [Managed NGINX ingress with the application routing add-on](app-routing).

## Secure traffic with a web application firewall (WAF)


Best practice guidanceTo scan incoming traffic for potential attacks, use a web application firewall (WAF) such as

[Barracuda WAF for Azure]or[Azure Application Gateway for Containers]. These more advanced network resources can also route traffic beyond just HTTP and HTTPS connections or basic TLS termination.

Typically, an ingress controller is a Kubernetes resource in your AKS cluster that distributes traffic to services and applications. The controller runs as a daemon on an AKS node, and consumes some of the node's resources, like CPU, memory, and network bandwidth. In larger environments, you may want to consider the following:

- Offload some of this traffic routing or TLS termination to a network resource outside of the AKS cluster.
- Scan incoming traffic for potential attacks.

For that extra layer of security, a web application firewall (WAF) filters the incoming traffic. With a set of rules, the Open Web Application Security Project (OWASP) watches for attacks like cross-site scripting or cookie poisoning. [Azure Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview) is a WAF that integrates with AKS clusters, locking in these security features before the traffic reaches your AKS cluster and applications.

Since other third-party solutions also perform these functions, you can continue to use existing investments or expertise in your preferred product.

Load balancer or ingress resources continually run in your AKS cluster and refine the traffic distribution. [Azure Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview) can be centrally managed as an ingress controller with a resource definition. To get started, [create an Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/quickstart-deploy-application-gateway-for-containers-alb-controller).

## Control traffic flow with network policies


Best practice guidanceUse network policies to allow or deny traffic to pods. By default, all traffic is allowed between pods within a cluster. For improved security, define rules that limit pod communication.


Network policy is a Kubernetes feature available in AKS that lets you control the traffic flow between pods. You allow or deny traffic to the pod based on settings such as assigned labels, namespace, or traffic port. Network policies are a cloud-native way to control the flow of traffic for pods. As pods are dynamically created in an AKS cluster, required network policies can be automatically applied.

To use [network policies in AKS](use-network-policies), the feature can be enabled either during cluster creation or on an existing AKS cluster. If you are planning to use network policies, ensure the feature is enabled on your AKS cluster.

Note

Network policies could be used for Linux-based or Windows-based nodes and pods in AKS.

You create a network policy as a Kubernetes resource using a YAML manifest. Policies are applied to defined pods, with ingress or egress rules defining traffic flow.

The following example applies a network policy to pods with the *app: backend* label applied to them. The ingress rule only allows traffic from pods with the *app: frontend* label.

```
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
name: backend-policy
spec:
podSelector:
matchLabels:
app: backend
ingress:
- from:
- podSelector:
matchLabels:
app: frontend
```


To get started with policies, see [Secure traffic between pods using network policies in Azure Kubernetes Service (AKS)](use-network-policies).

## Securely connect to nodes through a bastion host


Best practice guidanceDon't expose remote connectivity to your AKS nodes. Create a bastion host, or jump box, in a management virtual network. Use the bastion host to securely route traffic into your AKS cluster to remote management tasks.


You can complete most operations in AKS using the Azure management tools or through the Kubernetes API server. AKS nodes are only available on a private network and aren't connected to the public internet. To connect to nodes and provide maintenance and support, route your connections through a bastion host, or jump box. Verify this host lives in a separate, securely peered management virtual network to the AKS cluster virtual network.

You should also secure the management network for the bastion host. Use an [Azure ExpressRoute](/en-us/azure/expressroute/expressroute-introduction) or [VPN gateway](/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways) to connect to an on-premises network and control access using network security groups.

## Next steps

This article focused on network connectivity and security. For more information about network basics in Kubernetes, see [Network concepts for applications in Azure Kubernetes Service (AKS)](concepts-network)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-multiple-standard-load-balancer -->

# Use multiple load balancers in Azure Kubernetes Service (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) normally provisions one Standard Load Balancer (SLB) for all `LoadBalancer`

Services in a cluster. Because each node NIC is limited to [ 300 inbound load‑balancing rules and 8 private‑link services](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#load-balancer), large clusters or port‑heavy workloads can quickly exhaust these limits.

The **multiple SLB preview** removes that bottleneck by letting you create several SLBs inside the same cluster and shard nodes and Services across them. You define *load‑balancer configurations*, each tied to a primary agent pool and optional namespace, label, or node selectors—and AKS automatically places nodes and Services on the appropriate SLB. Outbound SNAT behavior is unchanged if `outboundType`

is `loadBalancer`

. Outbound traffic still flows through the first SLB.

Use this feature to:

- Scale beyond 300 inbound rules without adding clusters.
- Isolate tenant or workload traffic by binding a dedicated SLB to its own agent pool.
- Distribute private‑link services across multiple SLBs when you approach the per‑SLB limit.

## Prerequisites

`aks-preview`

extension 18.0.0b1 or later.- Subscription feature flag
`Microsoft.ContainerService/MultipleStandardLoadBalancersPreview`

registered. - Kubernetes version 1.28 or later.
- Cluster created with
`--load-balancer-backend-pool-type nodeIP`

or update and existing cluster using`az aks update`

.

### Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the aks-preview extension using the

command.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension released using the

command.`az extension update`

`az extension update --name aks-preview`


### Register the `MultipleStandardLoadBalancersPreview`

feature flag

Register the

`MultipleStandardLoadBalancersPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "MultipleStandardLoadBalancersPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "MultipleStandardLoadBalancersPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## How AKS chooses a load balancer (node & Service placement)

AKS uses multiple inputs to determine where to place nodes and expose LoadBalancer Services. These inputs are defined in each load balancer configuration and influence which SLB is selected for each resource.

| Input type | Applies to | Description |
|---|---|---|
Primary agent pool`--primary-agent-pool-name` |
Nodes | Required. All nodes in this pool are always added to the SLB’s backend pool. Ensures each SLB has at least one healthy node. |
Node selector`--node-selector` |
Nodes | Optional. Adds any node with matching labels to the SLB, in addition to the primary pool. |
Service namespace selector`--service-namespace-selector` |
Services | Optional. Only Services in namespaces with matching labels are considered for this SLB. |
Service label selector`--service-label-selector` |
Services | Optional. Only Services with matching labels are eligible for this SLB. |
Service annotation`service.beta.kubernetes.io/azure-load-balancer-configurations` |
Services | Optional. Limits placement to one or more explicitly named SLB configurations. Without it, any matching configuration is eligible. |

Note

Selectors define eligibility. The annotation (if used) restricts the controller to a specific subset of SLBs.

### How AKS uses these inputs

The AKS control plane continuously reconciles node and Service state using the rules above:

#### Node placement

When a node is added or updated, AKS checks which SLBs it qualifies for based on primary pool and node selector.

- If multiple SLBs match, the controller picks the one with the fewest current nodes.
- The node is added to that SLB’s backend pool.

#### Service placement

When a LoadBalancer Service is created or updated:

- AKS finds SLBs whose namespace and label selectors match the Service.
- If the Service annotation is present, only those named SLBs are considered.
- SLBs that have allowServicePlacement=false or that would exceed Azure limits (300 rules or 8 private-link services) are excluded.
- Among valid options, the SLB with the fewest rules is chosen.

### externalTrafficPolicy (ETP) behavior

AKS handles Services differently depending on the value of `externalTrafficPolicy`

.

| Mode | How load balancer selection works | How backend pool membership is built | Notes |
|---|---|---|---|
Cluster (default) |
The controller follows the standard placement rules described above. A single load-balancing rule targets the shared kubernetes backend pool on the chosen SLB. |
All nodes in that SLB’s `kubernetes` pool are healthy targets. Nodes without matching Pods are removed automatically by health probes. |
Same behavior as today in single-SLB clusters. |
Local |
The controller still uses the selector-based algorithm to pick an SLB, but creates a dedicated backend pool per Service instead of using the shared pool. |
Membership is synced from the Service’s `EndpointSlice` objects, so only nodes that actually host ready Pods are added. Health probes continue to use `healthCheckNodePort` to drop unhealthy nodes. |
Guarantees client IP preservation and avoids routing through nodes that lack Pods, even when nodes are sharded across multiple SLBs. |


Why a dedicated pool for ETP Local?

In multi-SLB mode, nodes that host Pods for a given Service may reside on different SLBs from the client-facing VIP. A shared backend pool would often contain zero eligible nodes, breaking traffic. By allocating a per-Service pool and syncing it from`EndpointSlice`

, AKS ensures the Service’s SLB always points at the correct nodes.

**Impact on quotas**

- Each ETP Local Service adds one backend pool and one load-balancing rule to its SLB.
- These count toward the 300-rule limit, so monitor rule usage when you have many ETP Local Services.

**No change to outbound traffic**

Outbound SNAT still flows through the first SLB’s `aksOutboundBackendPool`

when `outboundType`

is `loadBalancer`

, independent of ETP settings.

#### Optional: Rebalancing

You can manually rebalance node distribution later using `az aks loadbalancer rebalance`

.

This design lets you define flexible, label-driven routing for both infrastructure and workloads, while AKS handles placement automatically to maintain balance and avoid quota issues.

## Add the first load balancer configuration

Add a configuration named `kubernetes`

and bind it to a *primary* agent pool that always has at least one node. Removing every configuration switches the cluster back to single‑SLB mode.

Important

To enable multiple‑SLB mode you **must** add a load‑balancer configuration named `kubernetes`

and attach it to a *primary* agent pool that always has at least one ready node.

The presence of this configuration toggles multi‑SLB support; in service selection, it has no special priority and is treated like any other load balancer configuration.

If you delete every load‑balancer configuration, the cluster automatically falls back to single‑SLB mode, which can briefly disrupt service routing or SNAT flows.

Set environment variables for use throughout this tutorial. You can replace all placeholder values with your own except

`DEFAULT_LB_NAME`

, which must remain as`kubernetes`

.`RESOURCE_GROUP="rg-aks-multislb" CLUSTER_NAME="aks-multi-slb" LOCATION="westus" DEFAULT_LB_NAME="kubernetes" PRIMARY_POOL="nodepool1"`

Create resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster using the

command.\`az aks create`

`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME \ --load-balancer-backend-pool-type nodeIP \ --node-count 3`

Add a default load balancer using the

command.`az aks loadbalancer add`

`az aks loadbalancer add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $DEFAULT_LB_NAME \ --primary-agent-pool-name $PRIMARY_POOL \ --allow-service-placement true`


## Add additional load balancers

Create tenant‑specific configurations by specifying a different primary pool plus optional namespace, label, or node selectors.

Team 1 will run its own workloads in a separate node pool. Assign a

`tenant=team1`

label so workloads can be scheduled using selectors:`TEAM1_POOL="team1pool" TEAM1_LB_NAME="team1-lb"`

Create a second node pool for team 1 using the

command.`az aks nodepool add`

`az aks nodepool add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $TEAM1_POOL \ --labels tenant=team1 \ --node-count 2`

Create a load balancer for team 1 using the

command.`az aks loadbalancer add`

`az aks loadbalancer add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $TEAM1_LB_NAME \ --primary-agent-pool-name $TEAM1_POOL \ --service-namespace-selector "tenant=team1" \ --node-selector "tenant=team1"`

Label the target namespace (e.g.,

`team1-apps`

) to match the selector using thecommand.`az aks command invoke`

`az aks command invoke \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --command " kubectl create namespace team1-apps --dry-run=client -o yaml | kubectl apply -f - kubectl label namespace team1-apps tenant=team1 --overwrite "`

You can now list the load balancers in the cluster to see the multiple configurations using the

command.`az aks loadbalancer list`

`az aks loadbalancer list --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --output table`

Example output:

`AllowServicePlacement ETag Name PrimaryAgentPoolName ProvisioningState ResourceGroup ----------------------- ------- ---------- ---------------------- ------------------- --------------- True <ETAG> kubernetes nodepool1 Succeeded rg-aks-multislb True <ETAG> team1-lb team1pool Succeeded rg-aks-multislb`


### Deploy a Service to a specific load balancer

Add the annotation `service.beta.kubernetes.io/azure-load-balancer-configurations`

with a comma‑separated list of configuration names. If the annotation is omitted, the controller chooses automatically.

```
az aks command invoke \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--command "
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Service
metadata:
name: lb-svc-1
namespace: team1-apps
labels:
app: nginx-test
annotations:
service.beta.kubernetes.io/azure-load-balancer-configurations: \"team1-lb\"
# service.beta.kubernetes.io/azure-load-balancer-internal: "true" # If you want to create an internal load balancer.
spec:
selector:
app: nginx-test
ports:
- name: port1
port: 80
targetPort: 80
protocol: TCP
type: LoadBalancer
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-test
namespace: team1-apps
labels:
app: nginx
spec:
replicas: 1
selector:
matchLabels:
app: nginx-test
template:
metadata:
labels:
app: nginx-test
spec:
containers:
- image: nginx
imagePullPolicy: Always
name: nginx
ports:
- containerPort: 80
protocol: TCP
resources:
limits:
cpu: \"150m\"
memory: \"300Mi\"
EOF
"
```


### Rebalance nodes (optional)

Run a rebalance operation after scaling if rule counts become unbalanced using the [ az aks loadbalancer rebalance](/en-us/cli/azure/aks/loadbalancer#az-aks-loadbalancer-rebalance) command. This command disrupts active flows, so schedule it during a maintenance window.

```
az aks loadbalancer rebalance --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME
```


## Monitoring and troubleshooting

- Watch controller events (
`kubectl get events …`

) to confirm that Services are reconciled. - If external connectivity is blocked, open a node shell and curl the Service VIP to confirm kube‑proxy routing.

## Limitations and known issues

| Limitation | Details |
|---|---|
| Outbound SNAT | Always uses the first SLB; outbound flows aren’t sharded. |
| Backend pool type | Create or update and existing cluster to use `nodeIP` backend pools. |
| Autoscaler zeros | A primary agent pool can’t scale to 0 nodes. |
ETP `local` Rule Growth |
Each ETP `local` Service uses its own rule and backend pool, so rule counts can grow faster than with `cluster` mode. |
| Rebalance disruption | Removing a node from a backend pool drops in‑flight connections. Plan maintenance windows. |
| Configuration reload timing | After running `az aks loadbalancer` , changes may not take effect immediately. The AKS operation finishes quickly, but the cloud-controller-manager may take longer to apply updates. Wait for the `EnsuredLoadBalancer` event to confirm the changes are active. |

## Clean up resources

Delete the resource group when you’re finished to remove the cluster and load balancers using the [ az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP --yes --no-wait
```


## Next steps

The multiple SLB feature helps scale and isolate workloads at the networking layer while maintaining simplicity through Azure-managed configuration. For more information, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/workload-identity-deploy-cluster -->

# Deploy and configure Microsoft Entra Workload ID on an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy and configure an Azure Kubernetes Service (AKS) cluster with [Microsoft Entra Workload ID](workload-identity-overview). The steps in this article include:

- Create a new or update an existing AKS cluster using the Azure CLI with OpenID Connect (OIDC) issuer and Microsoft Entra Workload ID enabled.
- Create a workload identity and Kubernetes service account.
- Configure the managed identity for token federation.
- Deploy the workload and verify authentication with the workload identity.
- Optionally grant a pod in the cluster access to secrets in an Azure key vault.

## Prerequisites

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - This article requires version 2.47.0 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.
- Make sure that the identity that you're using to create your cluster has the appropriate minimum permissions. For more information, see
[Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command.`az account set`


Note

You can use *Service Connector* to help you configure some steps automatically. For more information, see [Tutorial: Connect to Azure storage account in Azure Kubernetes Service (AKS) with Service Connector using Microsoft Entra Workload ID](/en-us/azure/service-connector/tutorial-python-aks-storage-workload-identity).

## Create a resource group

Create a resource group using the

command.`az group create`

`export RANDOM_ID="$(openssl rand -hex 3)" export RESOURCE_GROUP="myResourceGroup$RANDOM_ID" export LOCATION="<your-preferred-region>" az group create --name "${RESOURCE_GROUP}" --location "${LOCATION}"`


## Enable OIDC issuer and Microsoft Entra Workload ID on an AKS cluster

You can enable OIDC issuer and Microsoft Entra Workload ID on a new or existing AKS cluster.

Create an AKS cluster using the

command with the`az aks create`

`--enable-oidc-issuer`

parameter to enable OIDC issuer and the`--enable-workload-identity`

parameter to enable Microsoft Entra Workload ID. The following example creates a cluster with a single node:`export CLUSTER_NAME="myAKSCluster$RANDOM_ID" az aks create \ --resource-group "${RESOURCE_GROUP}" \ --name "${CLUSTER_NAME}" \ --enable-oidc-issuer \ --enable-workload-identity \ --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Retrieve the OIDC issuer URL

Get the OIDC issuer URL and save it to an environmental variable using the [

`az aks show`

][az-aks-show] command.`export AKS_OIDC_ISSUER="$(az aks show --name "${CLUSTER_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --query "oidcIssuerProfile.issuerUrl" \ --output tsv)"`

The environment variable should contain the issuer URL, similar to the following example:

`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/11111111-1111-1111-1111-111111111111/`

By default, the issuer is set to use the base URL

`https://{region}.oic.prod-aks.azure.com/{tenant_id}/{uuid}`

, where the value for`{region}`

matches the location to which the AKS cluster is deployed. The value`{uuid}`

represents the OIDC key, which is a randomly generated and immutable GUID for each cluster.

## Create a managed identity

Get your subscription ID and save it to an environment variable using the [

`az account show`

][az-account-show] command.`export SUBSCRIPTION="$(az account show --query id --output tsv)"`

Create a user-assigned managed identity using the

command.`az identity create`

`export USER_ASSIGNED_IDENTITY_NAME="myIdentity$RANDOM_ID" az identity create \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --location "${LOCATION}" \ --subscription "${SUBSCRIPTION}"`

The following output example shows successful creation of a managed identity:

`{ "clientId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxxxxx/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentityxxxxxx", "location": "eastus", "name": "myIdentityxxxxxx", "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "resourceGroup": "myResourceGroupxxxxxx", "systemData": null, "tags": {}, "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`

Get the client ID of the managed identity and save it to an environment variable using the [

`az identity show`

][az-identity-show] command.`export USER_ASSIGNED_CLIENT_ID="$(az identity show \ --resource-group "${RESOURCE_GROUP}" \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --query 'clientId' \ --output tsv)"`


## Create a Kubernetes service account

Connect to your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --name "${CLUSTER_NAME}" --resource-group "${RESOURCE_GROUP}"`

Create a Kubernetes service account and annotate it with the client ID of the managed identity by applying the following manifest using the

`kubectl apply`

command:`export SERVICE_ACCOUNT_NAME="workload-identity-sa$RANDOM_ID" export SERVICE_ACCOUNT_NAMESPACE="default" cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: "${USER_ASSIGNED_CLIENT_ID}" name: "${SERVICE_ACCOUNT_NAME}" namespace: "${SERVICE_ACCOUNT_NAMESPACE}" EOF`

The following output shows successful creation of the workload identity:

`serviceaccount/workload-identity-sa created`


## Create the federated identity credential

Create a federated identity credential between the managed identity, the service account issuer, and the subject using the

command.`az identity federated-credential create`

`export FEDERATED_IDENTITY_CREDENTIAL_NAME="myFedIdentity$RANDOM_ID" az identity federated-credential create \ --name ${FEDERATED_IDENTITY_CREDENTIAL_NAME} \ --identity-name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --issuer "${AKS_OIDC_ISSUER}" \ --subject system:serviceaccount:"${SERVICE_ACCOUNT_NAMESPACE}":"${SERVICE_ACCOUNT_NAME}" \ --audience api://AzureADTokenExchange`

Note

It takes a few seconds for the federated identity credential to propagate after it's added. If a token request is made immediately after adding the federated identity credential, the request might fail until the cache is refreshed. To avoid this issue, you can add a slight delay after adding the federated identity credential.


For more information about federated identity credentials in Microsoft Entra, see [Overview of federated identity credentials in Microsoft Entra ID](/en-us/graph/api/resources/federatedidentitycredentials-overview).

## Create a key vault with Azure RBAC authorization

The following example shows how to use the Azure role-based access control (Azure RBAC) permission model to grant the pod access to the key vault. For more information about the Azure RBAC permission model for Azure Key Vault, see [Grant permission to applications to access an Azure key vault using Azure RBAC](/en-us/azure/key-vault/general/rbac-guide).

Create a key vault with purge protection and Azure RBAC authorization enabled using the [

`az keyvault create`

][az-keyvault-create] command. You can also use an existing key vault if it's configured for both purge protection and Azure RBAC authorization:`export KEYVAULT_NAME="keyvault-workload-id$RANDOM_ID" # Ensure the key vault name is between 3-24 characters az keyvault create \ --name "${KEYVAULT_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --location "${LOCATION}" \ --enable-purge-protection \ --enable-rbac-authorization`

Get the key vault resource ID and save it to an environment variable using the [

`az keyvault show`

][az-keyvault-show] command.`export KEYVAULT_RESOURCE_ID=$(az keyvault show --resource-group "${RESOURCE_GROUP}" \ --name "${KEYVAULT_NAME}" \ --query id \ --output tsv)`


### Assign RBAC permissions for key vault management

Get the caller object ID and save it to an environment variable using the [

`az ad signed-in-user show`

][az-ad-signed-in-user-show] command.`export CALLER_OBJECT_ID=$(az ad signed-in-user show --query id -o tsv)`

Assign yourself the Azure RBAC

[Key Vault Secrets Officer](/en-us/azure/role-based-access-control/built-in-roles/security#key-vault-secrets-officer)role so that you can create a secret in the new key vault using the [`az role assignment create`

][az-role-assignment-create] command.`az role assignment create --assignee "${CALLER_OBJECT_ID}" \ --role "Key Vault Secrets Officer" \ --scope "${KEYVAULT_RESOURCE_ID}"`


### Create and configure secret access

Create a secret in the key vault using the [

`az keyvault secret set`

][az-keyvault-secret-set] command.`export KEYVAULT_SECRET_NAME="my-secret$RANDOM_ID" az keyvault secret set \ --vault-name "${KEYVAULT_NAME}" \ --name "${KEYVAULT_SECRET_NAME}" \ --value "Hello\!"`

Get the principal ID of the user-assigned managed identity and save it to an environment variable using the [

`az identity show`

][az-identity-show] command.`export IDENTITY_PRINCIPAL_ID=$(az identity show \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --query principalId \ --output tsv)`

Assign the

[Key Vault Secrets User](/en-us/azure/role-based-access-control/built-in-roles/security#key-vault-secrets-user)role to the user-assigned managed identity using the [`az role assignment create`

][az-role-assignment-create] command. This step gives the managed identity permission to read secrets from the key vault.`az role assignment create \ --assignee-object-id "${IDENTITY_PRINCIPAL_ID}" \ --role "Key Vault Secrets User" \ --scope "${KEYVAULT_RESOURCE_ID}" \ --assignee-principal-type ServicePrincipal`

Create an environment variable for the key vault URL using the [

`az keyvault show`

][az-keyvault-show] command:`export KEYVAULT_URL="$(az keyvault show \ --resource-group "${RESOURCE_GROUP}" \ --name ${KEYVAULT_NAME} \ --query properties.vaultUri \ --output tsv)"`


## Deploy a verification pod and test access

Deploy a pod to verify that the workload identity can access the secret in the key vault. The following example uses the

`ghcr.io/azure/azure-workload-identity/msal-go`

image, which contains a sample application that retrieves a secret from Azure Key Vault using Microsoft Entra Workload ID:`kubectl apply -f - <<EOF apiVersion: v1 kind: Pod metadata: name: sample-workload-identity-key-vault namespace: ${SERVICE_ACCOUNT_NAMESPACE} labels: azure.workload.identity/use: "true" spec: serviceAccountName: ${SERVICE_ACCOUNT_NAME} containers: - image: ghcr.io/azure/azure-workload-identity/msal-go name: oidc env: - name: KEYVAULT_URL value: ${KEYVAULT_URL} - name: SECRET_NAME value: ${KEYVAULT_SECRET_NAME} nodeSelector: kubernetes.io/os: linux EOF`

Wait for the pod to be in the

`Ready`

state using the`kubectl wait`

command.`kubectl wait --namespace ${SERVICE_ACCOUNT_NAMESPACE} --for=condition=Ready pod/sample-workload-identity-key-vault --timeout=120s`

Check that the

`SECRET_NAME`

environment variable is set in the pod using thecommand.`kubectl describe`

`kubectl describe pod sample-workload-identity-key-vault | grep "SECRET_NAME:"`

If successful, the output should be similar to the following example:

`SECRET_NAME: ${KEYVAULT_SECRET_NAME}`

Verify that pods can get a token and access the resource using the

`kubectl logs`

command.`kubectl logs sample-workload-identity-key-vault`

If successful, the output should be similar to the following example:

`I0114 10:35:09.795900 1 main.go:63] "successfully got secret" secret="Hello\\!"`

Important

Azure RBAC role assignments can take up to 10 minutes to propagate. If the pod is unable to access the secret, you might need to wait for the role assignment to propagate. For more information, see

[Troubleshoot Azure RBAC](/en-us/azure/role-based-access-control/troubleshooting#).

## Disable Microsoft Entra Workload ID on an AKS cluster

Disable Microsoft Entra Workload ID on the AKS cluster where it's been enabled and configured, update the AKS cluster using the

command with the`az aks update`

`--disable-workload-identity`

parameter.`az aks update \ --resource-group "${RESOURCE_GROUP}" \ --name "${CLUSTER_NAME}" \ --disable-workload-identity`


## Related content

In this article, you deployed a Kubernetes cluster and configured it to use Microsoft Entra Workload ID in preparation for application workloads to authenticate with that credential. Now you're ready to deploy your application and configure it to use the workload identity with the latest version of the [Azure Identity](/en-us/azure/active-directory/develop/reference-v2-libraries) client library. If you can't rewrite your application to use the latest client library version, you can [set up your application pod](workload-identity-migrate-from-pod-identity) to authenticate using managed identity with workload identity as a short-term migration solution.

The [Service Connector](/en-us/azure/service-connector/overview) integration helps simplify the connection configuration for AKS workloads and Azure backing services. It securely handles authentication and network configurations and follows best practices for connecting to Azure services. For more information, see [Connect to Azure OpenAI in Foundry Models in AKS using Microsoft Entra Workload Identity](/en-us/azure/service-connector/tutorial-python-aks-openai-workload-identity) and the [Service Connector introduction](https://blog.aks.azure.com/2024/05/23/service-connector-intro).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-identity -->

# Best practices for authentication and authorization in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you deploy and maintain clusters in Azure Kubernetes Service (AKS), you implement ways to manage access to resources and services. Without these controls:

- Accounts could have access to unnecessary resources and services.
- Tracking credentials used to make changes can be difficult.

In this article, we discuss what recommended practices a cluster operator can follow to manage access and identity for AKS clusters. You'll learn how to:

- Authenticate AKS cluster users with Microsoft Entra ID.
- Control access to resources with Kubernetes role-based access control (Kubernetes RBAC).
- Use Azure RBAC to granularly control access to the AKS resource, the Kubernetes API at scale, and the
`kubeconfig`

. - Use a
[workload identity](workload-identity-overview)to access Azure resources from your pods.

Warning

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service has been deprecated as of 10/24/2022.

If you have [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) enabled on your AKS cluster or are considering implementing it,
we recommend you **review the workload identity overview article** to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.

## Use Microsoft Entra ID


Best practice guidanceDeploy AKS clusters with

[Microsoft Entra integration]. Using Microsoft Entra ID centralizes the identity management layer. Any change in user account or group status is automatically updated in access to the AKS cluster. Scope users or groups to the minimum permissions amount using[Roles, ClusterRoles, or Bindings].

Your Kubernetes cluster developers and application owners need access to different resources. Kubernetes lacks an identity management solution for you to control the resources with which users can interact. Instead, you can integrate your cluster with an existing identity solution like Microsoft Entra ID, an enterprise-ready identity management solution.

With Microsoft Entra integrated clusters in AKS, you create *Roles* or *ClusterRoles* defining access permissions to resources. You then *bind* the roles to users or groups from Microsoft Entra ID. Learn more about these Kubernetes RBAC in [the next section](#use-kubernetes-role-based-access-control-kubernetes-rbac). Microsoft Entra integration and how you control access to resources can be seen in the following diagram:

- Developer authenticates with Microsoft Entra ID.
- The Microsoft Entra token issuance endpoint issues the access token.
- The developer performs an action using the Microsoft Entra token, such as
`kubectl create pod`

. - Kubernetes validates the token with Microsoft Entra ID and fetches the developer's group memberships.
- Kubernetes RBAC and cluster policies are applied.
- The developer's request is successful based on previous validation of Microsoft Entra group membership and Kubernetes RBAC and policies.

To create an AKS cluster that uses Microsoft Entra ID, see [Integrate Microsoft Entra ID with AKS](enable-authentication-microsoft-entra-id).

## Use Kubernetes role-based access control (Kubernetes RBAC)


Best practice guidanceDefine user or group permissions to cluster resources with Kubernetes RBAC. Create roles and bindings that assign the least amount of permissions required. Integrate with Microsoft Entra ID to automatically update any user status or group membership change and keep access to cluster resources current.


In Kubernetes, you provide granular access control to cluster resources. You define permissions at the cluster level, or to specific namespaces. You determine what resources can be managed and with what permissions. You then apply these roles to users or groups with a binding. For more information about *Roles*, *ClusterRoles*, and *Bindings*, see [Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).

For example, you create a role with full access to resources in the namespace named *finance-app*, as shown in the following example YAML manifest:

```
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
name: finance-app-full-access-role
namespace: finance-app
rules:
- apiGroups: [""]
resources: ["*"]
verbs: ["*"]
```


You then create a *RoleBinding* and bind the Microsoft Entra user *developer1@contoso.com* to it, as shown in the following YAML manifest:

```
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
name: finance-app-full-access-role-binding
namespace: finance-app
subjects:
- kind: User
name: developer1@contoso.com
apiGroup: rbac.authorization.k8s.io
roleRef:
kind: Role
name: finance-app-full-access-role
apiGroup: rbac.authorization.k8s.io
```


When *developer1@contoso.com* is authenticated against the AKS cluster, they have full permissions to resources in the *finance-app* namespace. In this way, you logically separate and control access to resources. Use Kubernetes RBAC with Microsoft Entra ID-integration.

To learn how to use Microsoft Entra groups to control access to Kubernetes resources using Kubernetes RBAC, see [Control access to cluster resources using role-based access control and Microsoft Entra identities in AKS](azure-ad-rbac).

## Use Azure RBAC


Best practice guidanceUse Azure RBAC to define the minimum required user and group permissions to AKS resources in one or more subscriptions.


There are two levels of access needed to fully operate an AKS cluster:

Access the AKS resource on your Azure subscription.

This access level allows you to:

- Control scaling or upgrading your cluster using the AKS APIs
- Pull your
`kubeconfig`

.

To learn how to control access to the AKS resource and the

`kubeconfig`

, see[Limit access to cluster configuration file](control-kubeconfig-access).Access to the Kubernetes API.

This access level is controlled either by:

[Kubernetes RBAC](#use-kubernetes-role-based-access-control-kubernetes-rbac)(traditionally) or- By integrating Azure RBAC with AKS for kubernetes authorization.

To learn how to granularly grant permissions to the Kubernetes API using Azure RBAC, see

[Use Azure RBAC for Kubernetes authorization](manage-azure-rbac).

## Use pod-managed identities

Warning

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service has been deprecated as of 10/24/2022.

If you have [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) enabled on your AKS cluster or are considering implementing it,
we recommend you **review the workload identity overview article** to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.

Don't use fixed credentials within pods or container images, as they are at risk of exposure or abuse. Instead, use *pod identities* to automatically request access using Microsoft Entra ID.

To access other Azure resources, like Azure Cosmos DB, Key Vault, or Blob storage, the pod needs authentication credentials. You could define authentication credentials with the container image or inject them as a Kubernetes secret. Either way, you would need to manually create and assign them. Usually, these credentials are reused across pods and aren't regularly rotated.

With pod-managed identities (preview) for Azure resources, you automatically request access to services through Microsoft Entra ID. Pod-managed identities is currently in preview for AKS. Refer to the [Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (Preview)](use-azure-ad-pod-identity) documentation to get started.

Microsoft Entra pod-managed identity (preview) supports two modes of operation:

**Standard**mode: In this mode, the following 2 components are deployed to the AKS cluster:[Managed Identity Controller(MIC)](https://azure.github.io/aad-pod-identity/docs/concepts/mic/): A Kubernetes controller that watches for changes to pods,[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/)and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)through the Kubernetes API Server. When it detects a relevant change, the MIC adds or deletes[AzureAssignedIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureassignedidentity/)as needed. Specifically, when a pod is scheduled, the MIC assigns the managed identity on Azure to the underlying virtual machine scale set used by the node pool during the creation phase. When all pods using the identity are deleted, it removes the identity from the virtual machine scale set of the node pool, unless the same managed identity is used by other pods. The MIC takes similar actions when AzureIdentity or AzureIdentityBinding are created or deleted.[Node Managed Identity (NMI)](https://azure.github.io/aad-pod-identity/docs/concepts/nmi/): is a pod that runs as a DaemonSet on each node in the AKS cluster. NMI intercepts security token requests to the[Azure Instance Metadata Service](/en-us/azure/virtual-machines/linux/instance-metadata-service?tabs=linux)on each node. It redirects requests to itself and validates if the pod has access to the identity it's requesting a token for, and fetch the token from the Microsoft Entra tenant on behalf of the application.

**Managed**mode: In this mode, there's only NMI. The identity needs to be manually assigned and managed by the user. For more information, see[Pod Identity in Managed Mode](https://azure.github.io/aad-pod-identity/docs/configure/pod_identity_in_managed_mode/). In this mode, when you use the[az aks pod-identity add](/en-us/cli/azure/aks/pod-identity#az-aks-pod-identity-add)command to add a pod identity to an Azure Kubernetes Service (AKS) cluster, it creates the[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/)and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)in the namespace specified by the`--namespace`

parameter, while the AKS resource provider assigns the managed identity specified by the`--identity-resource-id`

parameter to virtual machine scale set of each node pool in the AKS cluster.

Note

If you instead decide to install the Microsoft Entra pod-managed identity using the [AKS cluster add-on](use-azure-ad-pod-identity), setup uses the `managed`

mode.

The `managed`

mode provides the following advantages over the `standard`

:

- Identity assignment on the virtual machine scale set of a node pool can take up 40-60s. With cronjobs or applications that require access to the identity and can't tolerate the assignment delay, it's best to use
`managed`

mode as the identity is pre-assigned to the virtual machine scale set of the node pool. Either manually or using the[az aks pod-identity add](/en-us/cli/azure/aks/pod-identity#az-aks-pod-identity-add)command. - In
`standard`

mode, MIC requires write permissions on the virtual machine scale set used by the AKS cluster and`Managed Identity Operator`

permission on the user-assigned managed identities. When running in`managed mode`

, since there's no MIC, the role assignments aren't required.

Instead of manually defining credentials for pods, pod-managed identities request an access token in real time, using it to access only their assigned resources. In AKS, there are two components that handle the operations to allow pods to use managed identities:

**The Node Management Identity (NMI) server**is a pod that runs as a DaemonSet on each node in the AKS cluster. The NMI server listens for pod requests to Azure services.**The Azure Resource Provider**queries the Kubernetes API server and checks for an Azure identity mapping that corresponds to a pod.

When pods request a security token from Microsoft Entra ID to access to an Azure resource, network rules redirect the traffic to the NMI server.

The NMI server:

- Identifies pods requesting access to Azure resources based on their remote address.
- Queries the Azure Resource Provider.

The Azure Resource Provider checks for Azure identity mappings in the AKS cluster.

The NMI server requests an access token from Microsoft Entra ID based on the pod's identity mapping.

Microsoft Entra ID provides access to the NMI server, which is returned to the pod.

- This access token can be used by the pod to then request access to resources in Azure.


In the following example, a developer creates a pod that uses a managed identity to request access to Azure SQL Database:

- Cluster operator creates a service account to map identities when pods request access to resources.
- The NMI server is deployed to relay any pod requests, along with the Azure Resource Provider, for access tokens to Microsoft Entra ID.
- A developer deploys a pod with a managed identity that requests an access token through the NMI server.
- The token is returned to the pod and used to access Azure SQL Database

To use Pod-managed identities, see [Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (preview)](use-azure-ad-pod-identity).

## Next steps

This best practices article focused on authentication and authorization for your cluster and resources. To implement some of these best practices, see the following articles:

[Integrate Microsoft Entra ID with AKS](enable-authentication-microsoft-entra-id)[Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (preview)](use-azure-ad-pod-identity)

For more information about cluster operations in AKS, see the following best practices:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-configure-container-network-metrics-filtering -->

# Configure container network metrics filtering for Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure container network metrics filtering for Azure Kubernetes Service (AKS) with Cilium to optimize data collection, reduce storage costs, and focus on the metrics most relevant to your monitoring needs.

Configure container network metrics filtering enables dynamic management of Hubble metrics cardinality through Kubernetes Custom Resource Definitions (CRDs). This feature allows you to dynamically control the cardinality, dimensions, and targets of Hubble metrics without restarting Cilium agents or Prometheus servers.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of the Azure CLI required to complete the steps in this article is

**2.73.0**. To find your version, run`az --version`

in the Azure CLI. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).An AKS cluster with Cilium data plane and

[Advanced Container Networking Services](advanced-container-networking-services-overview)enabled.Kubernetes version 1.32 or later.

Container network metrics filtering works specifically with Cilium data planes.

The minimum version of the

`aks-preview`

Azure CLI extension to complete the steps in this article is`18.0.0b2`

.

### Install the aks-preview Azure CLI extension

Install or update the Azure CLI preview extension by using the [ az extension add](/en-us/cli/azure/extension#az_extension_add) or

[command.](/en-us/cli/azure/extension#az_extension_update)

`az extension update`

```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the AdvancedNetworkingDynamicMetricsPreview feature flag

- First, register the AdvancedNetworkingDynamicMetricsPreview feature flag by using the
command:`az feature register`


```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
```


- Verify successful registration by using the
command. It takes a few minutes for registration to complete.`az feature show`


```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
```


- When the feature shows
**Registered**, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand.`az provider register`


```
az provider register --namespace Microsoft.ContainerService
```


### Create a new AKS cluster with Cilium

If you already have an existing cluster, you can skip this step.

Use the `az aks create`

command with the `--enable-acns`

flag to create a new AKS cluster that has all Advanced Container Networking Services features. These features include:

**Container Network Observability:**Provides insight into your network traffic. To learn more, see[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, see[Container Network Security](advanced-container-networking-services-overview#container-network-security).

```
# Set environment variables
export RESOURCE_GROUP="cnm-testing-rg"
export CLUSTER_NAME="cnm-cilium-cluster"
export LOCATION="eastus2euap" # Use canary region for preview features
# Create resource group
az group create --name $RESOURCE_GROUP --location $LOCATION
# Create AKS cluster with Cilium and ACNS enabled
az aks create \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--location $LOCATION \
--network-plugin azure \
--network-dataplane cilium \
--enable-acns \
--enable-managed-identity \
--generate-ssh-keys \
--kubernetes-version 1.32
```


### Get cluster credentials

Get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az_aks_get_credentials) command:

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --overwrite-existing
```


## Configure custom resources for metrics filtering

Container network metrics filtering uses the `ContainerNetworkMetric`

Custom Resource Definition (CRD) to define filtering rules. Only one CRD can exist per cluster, and changes take approximately 30 seconds to reconcile. If the CRD is not applied, all metrics will be collected.

```
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: : container-network-metric # Cluster scoped
spec:
filters:
- metric: flow
includeFilters: # List of include filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
matchExpressions:
- key: environment
operator: In
values:
- production
- staging
ip: # List of source IPs; can be CIDR
- "192.168.1.10"
- "10.0.0.1"
to:
namespacedPod:
- sample-namespace2/sample-pod2
labelSelector:
matchLabels:
app: backend
k8s.io/namespace: sample-namespace2
matchExpressions:
- key: tier
operator: NotIn
values:
- dev
ip:
- "192.168.1.20"
- "10.0.1.1"
protocol: # List of protocols; can be tcp, udp, dns
- tcp
- udp
- dns
verdict: # List of verdicts; can be forwarded, dropped
- forwarded
- dropped
metric: dns
excludeFilters: # List of exclude filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
```


The following table describes the fields in the custom resource definition:

| Field | Type | Description | Required |
|---|---|---|---|
`filters.metric` |
String | Name of the metric you would like to apply the filter on. This is mandatory. The supported values are `dns` , `flow` , `tcp` , `drop` |
Mandatory |
`includeFilters` or `excludeFilters` |
[]filter | A list of filters that define network flows to include. Each filter specifies the source, destination, protocol, and other matching criteria. You must have at least one include or exclude filter. | Mandatory |
`filters.name` |
String | The name of the filter. | Optional |
`filters.protocol` |
[]string | The protocols to match for this filter. Valid values are `tcp` , `udp` , and `dns` . Because it's an optional parameter, if it isn't specified, logs with all protocols are included. |
Optional |
`filters.verdict` |
[]string | The verdict of the flow to match. Valid values are `forwarded` and `dropped` . Because it's an optional parameter, if it isn't specified, logs with all verdicts are included. |
Optional |
`filters.from` |
Endpoint | Specifies the source of the network flow. Can include IP addresses, label selectors, and namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector is a mechanism to filter and query resources based on labels, so you can identify specific subsets of resources. A label selector can include two components: `matchLabels` and `matchExpressions` . Use `matchLabels` for straightforward matching by specifying a key/value pair (for example, `{"app": "frontend"}` ). For more advanced criteria, use `matchExpressions` , where you define a label key, an operator (such as `In` , `NotIn` , `Exists` , or `DoesNotExist` ), and an optional list of values. Ensure that the conditions in both `matchLabels` and `matchExpressions` are met, because they're logically combined by `AND` . If no conditions are specified, the selector matches all resources. To match none, leave the selector null. Carefully define your label selector to target the correct set of resources. |
Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) for matching the source. `name` should match the RegEx pattern `^.+$` . |
Optional |
`filters.to` |
Endpoint | Specifies the destination of the network flow. Can include IP addresses, label selectors, or namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector to match resources based on their labels. | Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) to match the destination. |
Optional |

Apply the `ContainerNetworkMetric`

custom resource to enable log collection at the cluster:

```
kubectl apply -f <crd.yaml>
```


## Clean up and reset

To clean up filtering configuration:

```
# Delete the CRD
kubectl delete ContainerNetworkMetric container-network-metric
```


## Example filtering configuration

- Create a basic filtering configuration that focuses on DNS metrics:

```
# basic-dns-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: dns # Supported: dns, flow, tcp, drop
excludeFilters:
- from:
namespacedPod: ["kube-system/coredns"]
```


- Configure filtering for TCP metrics with include and exclude filters:

```
# tcp-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: tcp
includeFilters:
- from:
labelSelector:
matchLabels:
tier: "frontend"
excludeFilters:
- to:
namespacedPod: ["kube-system/metrics-server"]
```


- Configure filtering for network flow metrics:

```
# flow-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: flow
includeFilters:
- from:
labelSelector:
matchLabels:
tier: "frontend"
- to:
labelSelector:
matchLabels:
tier: "backend"
excludeFilters:
- from:
namespacedPod: ["default/test"]
```


- Configure filtering for dropped packet metrics:

```
# drop-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: drop
excludeFilters:
- from:
namespacedPod: ["kube-system/"]
```


- Configure filtering for multiple metric types in a single CRD:

```
# multi-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: dns
includeFilters:
- protocol: ["dns"]
excludeFilters:
- from:
namespacedPod: ["kube-system/*"]
- metric: tcp
includeFilters:
- protocol: ["tcp"]
- from:
labelSelector:
matchLabels:
environment: "production"
- metric: flow
excludeFilters:
- from:
namespacedPod: ["default/debug-*"]
- metric: drop
includeFilters:
- reason: ["Policy denied", "Invalid"]
```


## Best practices

Ensure you do not have conflicting include and exclude filter on the CRD.

Leverage Kubernetes label selectors for flexible filtering.

Always validate filtering configurations in development or staging

Regularly review filtered metrics to ensure important data isn't lost.

Remember that only one CRD can exist per cluster.


## Troubleshooting

### Common issues

**Issue**: CRD configuration not applied

**Solution**: Check that the feature flag is registered and only one CRD exists:

```
# Verify feature registration
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
# Check existing CRDs
kubectl get ContainerNetworkMetric
```


**Issue**: Metrics still showing after applying excludeFilters

**Solution**: Remember that preexisting metrics persist in Prometheus. You may need to wait for new metrics to be generated to see the filtering effects.

## Limitations

- This feature is specifically designed for Cilium data planes only
- Only one
`ContainerNetworkMetric`

CRD can exist per cluster - Preexisting metrics persist in Prometheus; new filtering rules apply to newly generated metrics
- Requires Kubernetes version 1.32 or later

## Related content

- To learn about container network metrics capabilities, see
[Container network metrics overview](container-network-observability-metrics). - To create an AKS cluster with Advanced Container Networking Services, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-l7-policy-concepts -->

# Overview of Layer 7 (L7) policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Network policies are essential for securing Kubernetes clusters by defining and controlling pod communication. They mitigate unauthorized access and potential security breaches by regulating traffic flow. Advanced Container Networking Services strengthens security with [FQDN-based network policies](container-network-security-fqdn-filtering-concepts). Expanding on this foundation, Advanced Container Networking Services now provides L7 policy support, enabling detailed inspection and management of application-level traffic. This advancement enhances both the security and efficiency of network communications within AKS clusters. The offering includes comprehensive support for widely adopted protocols, including HTTP, gRPC, and Kafka.

## Components of L7 policy

**Envoy proxy**: Envoy, part of ACNS security agent acts as the enforcement point for L7 policies. A TPROXY inspects application traffic, comparing it against the defined L7 policies. To enhance scalability and resource management, Envoy is deployed as a separate DaemonSet, decoupled from the Cilium Agent.

## How L7 policy works

When L7 policy enforcement is enabled for an application or pod, outgoing network traffic is first evaluated to determine compliance with the configured application-level rules. The eBPF probe attached to the source pod’s network interface marks the packets, which are then redirected to a node-local Envoy Proxy. This redirection occurs only for pods enforcing L7 policies, ensuring that policy enforcement is applied selectively.

The Envoy proxy, augmented with Cilium network filters, then decides whether to forward the traffic to the destination pod based on policy criteria. If permitted, the traffic proceeds; if not, Envoy returns an appropriate error code to the originating pod. Upon successful authorization, the Envoy proxy facilitates the traffic flow, providing application-level visibility and control. This allows the Cilium agent to enforce detailed network policies within the policy engine. The following diagram illustrates the high-level flow of L7 policy enforcement.

## Monitoring L7 traffic with Hubble and Grafana

To gain insights into L7 traffic flows, specifically HTTP, gRPC, and Kafka, Azure CNI Powered by Cilium leverages Hubble agent, which is enabled by default with Advanced Container Networking Services. Hubble provides detailed flow-level metrics.

To simplify the analysis of these L7 metrics, we provide pre-configured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

These dashboards offer granular visibility into L7 flow data at the cluster, namespace, and workload levels.

Note

These dashboards will only display data if you have this feature enabled on your cluster and have relevant policies applied.
Additionally, the monitoring metrics are **not** required to flow through Envoy, a component of the ACNS security agent. Rather, these metrics are collected by the Hubble agent, which is installed on your cluster as part of the Advanced Container Networking Service's observability feature.

## Key benefits

**Granular Application-Level Control**: L7 policies allow for fine-grained control over network traffic based on application-specific attributes, such as HTTP methods, gRPC paths, and Kafka topics. This extends beyond the basic IP address and port-based control of traditional network policies.

**Enhanced Security**: By inspecting application-level traffic, L7 policies can prevent attacks that exploit vulnerabilities at the application layer. This includes blocking unauthorized access to specific APIs or services. Furthermore, L7 policies are an important component of a Zero Trust security strategy, enabling the enforcement of the principle of least privilege at the application layer.

**Graceful Error Handling**: Unlike L3/L4 policies that typically drop unauthorized traffic silently, L7 policies can return application-level error codes (for example, HTTP 403, Kafka authorization failures), allowing applications to handle errors more gracefully.

**Observability**: With observability enabled for Advanced Container Networking Services and L7 policies applied to your AKS cluster, you can monitor traffic and policy effectiveness using Grafana dashboards.

## Limitations and considerations

- Current feature support relies on Cilium's Layer 7 policy enforcement based on HTTP, HTTPS, gRPC, and Kafka.
- The maximum supported cluster size is up to 1,000 nodes or 40,000 pods, whichever is greater.
- Traffic traversing Envoy proxies do come with latency. Users may experience noticeable latency degradation beyond 3,000 requests per second.
- As part of our observability solution, we provide envoy_http_rq_total metrics. These metrics give the total request count, which could be used to derive requests per seconds (rps).
- During a Cilium upgrade or rollout, existing sessions can be gracefully closed. Applications are expected to handle these interruptions gracefully—typically by implementing retry mechanisms at the connection or request level. New connections initiated during the rollout aren't impacted.
- L7 policy isn't supported by CiliumClusterwideNetworkPolicy(CCNP).
- L7 policy through Advanced Container Networking Services (ACNS) isn't compatible with L7 policies implemented via alternate methods such as Istio. The following table summarizes the supported scenarios.

| Feature/Component | L7 Policies using AKS, Istio - Managed addon |
|---|---|
| K8s network policies by Azure CNI powered by Cilium | Supported |
| L4 (FQDN) Policies by Azure CNI powered by Cilium and ACNS | Supported |
| L7 (HTTP(s)/GRPC/Kafka) Policies by Azure CNI powered by Cilium and ACNS | Not Supported |

## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[L7 policies](how-to-apply-l7-policies)on AKS.Explore how the open source community builds

[Cilium Network Policies](https://docs.cilium.io/en/latest/security/policy/).For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](advanced-container-networking-services-overview#container-network-observability)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-paas-services -->

# Tutorial - Use PaaS services with an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Kubernetes, you can use PaaS services, such as [Azure Service Bus](/en-us/azure/service-bus-messaging/service-bus-messaging-overview), to develop and run your applications.

In this tutorial, you create an Azure Service Bus namespace and queue to test your application. You learn how to:

- Create an Azure Service Bus namespace and queue.
- Update the Kubernetes manifest file to use the Azure Service Bus queue.
- Test the updated application by placing an order.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created a Kubernetes cluster, and deployed an application. To complete this tutorial, you need the pre-created `aks-store-quickstart.yaml`

Kubernetes manifest file. This file download was included with the application source code in a previous tutorial. Make sure you cloned the repo and changed directories into the cloned repo. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create environment variables

Create the following environment variables to use for the commands in this tutorial:

`LOC_NAME=westus2 RAND=$RANDOM RG_NAME=myResourceGroup AKS_NAME=myAKSCluster SB_NS=sb-store-demo-$RAND`


## Create Azure Service Bus namespace and queue

In previous tutorials, you used a RabbitMQ container to store orders submitted by the `order-service`

. In this tutorial, you use an Azure Service Bus namespace to provide a scoping container for the Service Bus resources within the application. You also use an Azure Service bus queue to send and receive messages between the application components. For more information on Azure Service Bus, see [Create an Azure Service Bus namespace and queue](/en-us/azure/service-bus-messaging/service-bus-quickstart-cli).

Create an Azure Service Bus namespace using the

command.`az servicebus namespace create`

`az servicebus namespace create --name $SB_NS --resource-group $RG_NAME --location $LOC_NAME`

Create an Azure Service Bus queue using the

command.`az servicebus queue create`

`az servicebus queue create --name orders --resource-group $RG_NAME --namespace-name $SB_NS`

Create an Azure Service Bus authorization rule using the

command.`az servicebus queue authorization-rule create`

`az servicebus queue authorization-rule create \ --name sender \ --namespace-name $SB_NS \ --resource-group $RG_NAME \ --queue-name orders \ --rights Send`

Get the Azure Service Bus credentials for later use by using the

and`az servicebus namespace show`

commands.`az servicebus queue authorization-rule keys list`

`az servicebus namespace show --name $SB_NS --resource-group $RG_NAME --query name -o tsv az servicebus queue authorization-rule keys list --namespace-name $SB_NS --resource-group $RG_NAME --queue-name orders --name sender --query primaryKey -o tsv`


## Update Kubernetes manifest file

Configure

`kubectl`

to connect to your cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Open the

`aks-store-quickstart.yaml`

file in a text editor.Remove the existing

`rabbitmq`

StatefulSet, ConfigMap, and Service sections and replace the existing`order-service`

Deployment section with the following content:`apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: <REPLACE_WITH_YOUR_ACR_NAME>.azurecr.io/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "<REPLACE_WITH_YOUR_SB_NS_HOSTNAME>" # Example: sb-store-demo-123456.servicebus.windows.net - name: ORDER_QUEUE_PORT value: "5671" - name: ORDER_QUEUE_TRANSPORT value: "tls" - name: ORDER_QUEUE_USERNAME value: "sender" - name: ORDER_QUEUE_PASSWORD value: "<REPLACE_WITH_YOUR_SB_SENDER_PASSWORD>" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3`

Note

Directly adding sensitive information, such as API keys, to your Kubernetes manifest files isn't secure and may accidentally get committed to code repositories. We added it here for simplicity. For production workloads, use

[Managed Identity](use-managed-identity)to authenticate with Azure Service Bus or store your secrets in[Azure Key Vault](csi-secrets-store-driver).Save and close the updated

`aks-store-quickstart.yaml`

file.

## Deploy the updated application

Deploy the updated application using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the successfully updated resources:

`deployment.apps/order-service configured service/order-service unchanged deployment.apps/product-service unchanged service/product-service unchanged deployment.apps/store-front configured service/store-front unchanged`


## Test the application

### Place a sample order

Get the external IP address of the

`store-front`

service using the`kubectl get service`

command.`kubectl get service store-front`

Navigate to the external IP address of the

`store-front`

service in your browser using`http://<external-ip>`

.Place an order by choosing a product and selecting

**Add to cart**.Select

**Cart**to view your order, and then select**Checkout**.

### View the order in the Azure Service Bus queue

- Navigate to the Azure portal and open the Azure Service Bus namespace you created earlier.
- Under
**Entities**, select**Queues**, and then select the**orders**queue. - In the
**orders**queue, select**Service Bus Explorer**. - Select
**Peek from start**to view the order you submitted.

## Next steps

In this tutorial, you used Azure Service Bus to update and test the sample application. You learned how to:

- Create an Azure Service Bus namespace and queue.
- Update the Kubernetes manifest file to use the Azure Service Bus queue.
- Test the updated application by placing an order.

In the next tutorial, you learn how to scale an application in AKS.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-how-to -->

# Set up Container Network Observability for Azure Kubernetes Service (AKS) - Azure managed Prometheus and Grafana

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to set up Container Network Observability for Azure Kubernetes Service (AKS) using Managed Prometheus and Grafana and BYO Prometheus and Grafana and to visualize the scraped metrics

You can use Container Network Observability to collect data about the network traffic of your AKS clusters. It enables a centralized platform for monitoring application and network health. Currently, metrics are stored in Prometheus and Grafana can be used to visualize them. Container Network Observability also offers the ability to enable Hubble. These capabilities are supported for both Cilium and non-Cilium clusters.

Container Network Observability is one of the features of Advanced Container Networking Services. For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see [What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview)

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- The minimum version of Azure CLI required for the steps in this article is 2.56.0. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.

```
# Set an environment variable for the AKS cluster name. Make sure to replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location eastus \
--max-pods 250 \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--node-count 2 \
--pod-cidr 192.168.0.0/16 \
--kubernetes-version 1.29 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features that includes [Container Network Observability](advanced-container-networking-services-overview#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview#container-network-security)feature.

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


## Get cluster credentials

Once you have Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Azure managed Prometheus and Grafana

Skip this Section if using BYO Prometheus and Grafana

Use the following example to install and enable Prometheus and Grafana for your AKS cluster.

### Create Azure Monitor resource

```
#Set an environment variable for the Grafana name. Make sure to replace the placeholder with your own value.
export AZURE_MONITOR_NAME="<azure-monitor-name>"
# Create Azure monitor resource
az resource create \
--resource-group $RESOURCE_GROUP \
--namespace microsoft.monitor \
--resource-type accounts \
--name $AZURE_MONITOR_NAME \
--location eastus \
--properties '{}'
```


### Create Azure Managed Grafana instance

Use [az grafana create](/en-us/cli/azure/grafana#az-grafana-create) to create a Grafana instance. The name of the Grafana instance must be unique.

```
# Set an environment variable for the Grafana name. Make sure to replace the placeholder with your own value.
export GRAFANA_NAME="<grafana-name>"
# Create Grafana instance
az grafana create \
--name $GRAFANA_NAME \
--resource-group $RESOURCE_GROUP
```


### Place the Azure Managed Grafana and Azure Monitor resource IDs in variables

Use [az grafana show](/en-us/cli/azure/grafana#az-grafana-show) to place the Grafana resource ID in a variable. Use [az resource show](/en-us/cli/azure/resource#az-resource-show) to place the Azure Monitor resource ID in a variable. Replace **myGrafana** with the name of your Grafana instance.

```
grafanaId=$(az grafana show \
--name $GRAFANA_NAME \
--resource-group $RESOURCE_GROUP \
--query id \
--output tsv)
azuremonitorId=$(az resource show \
--resource-group $RESOURCE_GROUP \
--name $AZURE_MONITOR_NAME \
--resource-type "Microsoft.Monitor/accounts" \
--query id \
--output tsv)
```


### Link Azure Monitor and Azure Managed Grafana to the AKS cluster

Use [az aks update](/en-us/cli/azure/aks#az-aks-update) to link the Azure Monitor and Grafana resources to your AKS cluster.

```
az aks update \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--enable-azure-monitor-metrics \
--azure-monitor-workspace-resource-id $azuremonitorId \
--grafana-resource-id $grafanaId
```


## Visualization

### Visualization using Azure Managed Grafana

Skip this step if using BYO Grafana

Note

The `hubble_flows_processed_total`

metric isn't scraped by default due to high metric cardinality in large scale clusters.
Because of this, the *Pods Flows* dashboards have panels with missing data. To enable this metric and populate the missing data, you need to modify the ama-metrics-settings-configmap. Specifically, update the default-targets-metrics-keep-list section. Follow the below steps to update the configmap:

- Get the latest ama-metrics-settings-configmap.(
[https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml](https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml)) - Locate the networkobservabilityHubble = ""
- Change it to networkobservabilityHubble = "hubble.*"
- Now the Pod flow metrics should populate.

To learn more about what minimal ingestion, see the [Minimal Ingestion Documentation](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal).

Make sure the Azure Monitor pods are running using the

`kubectl get pods`

command.`kubectl get pods -o wide -n kube-system | grep ama-`

Your output should look similar to the following example output:

`ama-metrics-5bc6c6d948-zkgc9 2/2 Running 0 (21h ago) 26h ama-metrics-ksm-556d86b5dc-2ndkv 1/1 Running 0 (26h ago) 26h ama-metrics-node-lbwcj 2/2 Running 0 (21h ago) 26h ama-metrics-node-rzkzn 2/2 Running 0 (21h ago) 26h ama-metrics-win-node-gqnkw 2/2 Running 0 (26h ago) 26h ama-metrics-win-node-tkrm8 2/2 Running 0 (26h ago) 26h`

We have created sample dashboards. They can be found under the

**Dashboards > Azure Managed Prometheus**folder. They have names like**"Kubernetes / Networking /**. The suite of dashboards includes:`<name>`

"**Clusters:**shows Node-level metrics for your clusters.**DNS (Cluster):**shows DNS metrics on a cluster or selection of Nodes.**DNS (Workload):**shows DNS metrics for the specified workload (for example, Pods of a DaemonSet or Deployment such as CoreDNS).**Drops (Workload):**shows drops to/from the specified workload (for example, Pods of a Deployment or DaemonSet).**Pod Flows (Namespace):**shows L4/L7 packet flows to/from the specified namespace (i.e. Pods in the Namespace).**Pod Flows (Workload):**shows L4/L7 packet flows to/from the specified workload (for example, Pods of a Deployment or DaemonSet).


### Visualization using BYO Grafana

Skip this step if using Azure managed Grafana

Add the following scrape job to your existing Prometheus configuration and restart your Prometheus server:

`- job_name: networkobservability-hubble kubernetes_sd_configs: - role: pod relabel_configs: - target_label: cluster replacement: myAKSCluster action: replace - source_labels: [__meta_kubernetes_namespace, __meta_kubernetes_pod_label_k8s_app] regex: kube-system;(retina|cilium) action: keep - source_labels: [__address__] action: replace regex: ([^:]+)(?::\d+)? replacement: $1:9965 target_label: __address__ - source_labels: [__meta_kubernetes_pod_node_name] target_label: instance action: replace metric_relabel_configs: - source_labels: [__name__] regex: '|hubble_dns_queries_total|hubble_dns_responses_total|hubble_drop_total|hubble_tcp_flags_total' # if desired, add |hubble_flows_processed_total action: keep`

In

**Targets**of Prometheus, verify the**network-obs-pods**are present.Sign in to Grafana and import following example dashboards using the following IDs:

**Clusters:**shows Node-level metrics for your clusters. (ID:[18814](https://grafana.com/grafana/dashboards/18814-kubernetes-networking-clusters/))**DNS (Cluster):**shows DNS metrics on a cluster or selection of Nodes.(ID:[20925](https://grafana.com/grafana/dashboards/20925-kubernetes-networking-dns-cluster/))**DNS (Workload):**shows DNS metrics for the specified workload (for example, Pods of a DaemonSet or Deployment such as CoreDNS). (ID: [20926][https://grafana.com/grafana/dashboards/20926-kubernetes-networking-dns-workload/](https://grafana.com/grafana/dashboards/20926-kubernetes-networking-dns-workload/))**Drops (Workload):**shows drops to/from the specified workload (for example, Pods of a Deployment or DaemonSet).(ID:[20927](https://grafana.com/grafana/dashboards/20927-kubernetes-networking-drops-workload/)).**Pod Flows (Namespace):**shows L4/L7 packet flows to/from the specified namespace (i.e. Pods in the Namespace). (ID:[20928](https://grafana.com/grafana/dashboards/20928-kubernetes-networking-pod-flows-namespace/))**Pod Flows (Workload):**shows L4/L7 packet flows to/from the specified workload (for example, Pods of a Deployment or DaemonSet). (ID:[20929](https://grafana.com/grafana/dashboards/20929-kubernetes-networking-pod-flows-workload/))

Note

- Depending on your Prometheus/Grafana instances' settings, some dashboard panels require specific tweaks to display all data.
- Cilium doesn't currently support DNS metrics/dashboards.


## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to install and enable Container Network Observability for your AKS cluster.

For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).For more information on Container Network Security and its capabilities, see

[What is Container Network Security?](container-network-security-concepts).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/stateful-workload-upgrades -->

# Stateful workload upgrade patterns

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrade clusters that run databases and stateful applications without data loss by using these proven patterns.

## What this article covers

This article provides database-specific upgrade patterns for Azure Kubernetes Service (AKS) clusters with stateful workloads, such as:

- PostgreSQL Ferris wheel pattern for ~30-second downtime.
- Redis rolling replacement for zero-downtime cache upgrades.
- MongoDB step-down cascades for replica set safety.
- Emergency upgrade checklists for security responses.
- Validation and rollback procedures for data protection.

These patterns are best for use by database administrators for applications with persistent data and mission-critical stateful services.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service cluster](upgrade-aks-cluster). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

For a quick start, select a link for instructions:

[Do you need an emergency upgrade?](#emergency-upgrade-checklist)[Do you need help with a PostgreSQL cluster?](#the-ferris-wheel-pattern-postgresql)[Do you need a Redis cache rolling replace?](#redis-cluster-rolling-replace)

## Choose your pattern

| Database type | Upgrade pattern | Downtime | Complexity | Best for |
|---|---|---|---|---|
| PostgreSQL |
|

[Rolling replace](#redis-cluster-rolling-replace)[Step-down cascade](#mongodb-replica-set-step-down)*(coming soon)**(coming soon)*## Emergency upgrade checklist

Do you need to upgrade now because of security issues?

Run the following commands for an immediate safety check (two minutes):

`# Verify all replicas are healthy kubectl get pods -l tier=database -o wide # Check replication lag ./scripts/check-replica-health.sh # Ensure recent backup exists kubectl get job backup-job -o jsonpath='{.status.completionTime}'`

Choose an emergency pattern (one minute):

**PostgreSQL/MySQL:**Use[Ferris wheel](#the-ferris-wheel-pattern-postgresql)(30-second downtime).**Redis/Memcached:**Use[Rolling replace](#redis-cluster-rolling-replace)(zero downtime).**MongoDB/CouchDB:**Use[Step-down cascade](#mongodb-replica-set-step-down)(10-second downtime).

Run with a safety net (15-minute to 30-minute window):

- Always test rollback procedures in advance.
- Monitor application metrics during the upgrade.
- Keep the database team on standby.


## The Ferris wheel pattern: PostgreSQL

This pattern is best for 3-node PostgreSQL clusters with primary/replica setup across availability zones.

Visual pattern:

```
Initial: [PRIMARY] [REPLICA-1] [REPLICA-2]
Step 1: [PRIMARY] [REPLICA-1] [NEW-NODE] ← Add new node
Step 2: [REPLICA-1] [NEW-NODE] [REPLICA-2] ← Promote & remove old primary
Step 3: [NEW-PRIMARY] [NEW-NODE] [REPLICA-2] ← Complete rotation
```


### Quick implementation (20 minutes)

```
# 1. Add new node to cluster
kubectl scale statefulset postgres-cluster --replicas=4
# 2. Wait for new replica to sync
kubectl wait --for=condition=ready pod postgres-cluster-3 --timeout=300s
# 3. Promote new primary and failover (30-second downtime window)
kubectl exec postgres-cluster-3 -- pg_ctl promote -D /var/lib/postgresql/data
# 4. Update service endpoint
kubectl patch service postgres-primary --patch '{"spec":{"selector":{"app":"postgres-cluster","role":"primary","pod":"postgres-cluster-3"}}}'
# 5. Remove old primary node
kubectl delete pod postgres-cluster-0
```


**Detailed step-by-step guide**

#### Prerequisites validation

```
#!/bin/bash
# pre-upgrade-validation.sh
echo "=== PostgreSQL Cluster Health Check ==="
# Check replication status
kubectl exec postgres-primary-0 -- psql -c "SELECT * FROM pg_stat_replication;"
# Verify sync replication (must show 'sync' state)
SYNC_COUNT=$(kubectl exec postgres-primary-0 -- psql -t -c "SELECT count(*) FROM pg_stat_replication WHERE sync_state='sync';")
if [ "$SYNC_COUNT" -lt 2 ]; then
echo "ERROR: Need at least 2 synchronous replicas"
exit 1
fi
# Confirm recent backup exists
LAST_BACKUP=$(kubectl get job postgres-backup -o jsonpath='{.status.completionTime}')
echo "Last backup: $LAST_BACKUP"
# Test failover capability in staging first
echo "✅ Prerequisites validated"
```


#### Step 1: Scale up with a new node

```
# Add new node with upgraded Kubernetes version
kubectl patch statefulset postgres-cluster --patch '{
"spec": {
"replicas": 4,
"template": {
"spec": {
"nodeSelector": {
"kubernetes.io/arch": "amd64",
"aks-nodepool": "upgraded-pool"
}
}
}
}
}'
# Monitor new pod startup
kubectl get pods -l app=postgres-cluster -w
# Verify new replica joins cluster
kubectl exec postgres-cluster-3 -- psql -c "SELECT * FROM pg_stat_replication;"
```


#### Step 2: Run a controlled failover

```
#!/bin/bash
# controlled-failover.sh
echo "=== Starting Controlled Failover ==="
# Ensure minimal replication lag (< 0.1-second)
LAG=$(kubectl exec postgres-primary-0 -- psql -t -c "SELECT EXTRACT(EPOCH FROM now() - pg_last_xact_replay_timestamp());")
if (( $(echo "$LAG > 0.1" | bc -l) )); then
echo "ERROR: Replication lag too high ($LAG seconds)"
exit 1
fi
# Pause application writes (use connection pool drain)
kubectl patch configmap pgbouncer-config --patch '{"data":{"pgbouncer.ini":"[databases]\napp_db = host=postgres-primary port=5432 dbname=appdb pool_mode=statement max_db_connections=0"}}'
# Wait for active transactions to complete
sleep 10
# Promote new primary (this is the 30-second downtime window)
kubectl exec postgres-cluster-3 -- pg_ctl promote -D /var/lib/postgresql/data
# Update service selector to new primary
kubectl patch service postgres-primary --patch '{
"spec": {
"selector": {
"statefulset.kubernetes.io/pod-name": "postgres-cluster-3"
}
}
}'
# Resume application writes
kubectl patch configmap pgbouncer-config --patch '{"data":{"pgbouncer.ini":"[databases]\napp_db = host=postgres-primary port=5432 dbname=appdb pool_mode=statement"}}'
echo "✅ Failover completed"
```


#### Step 3: Clean up and validate

```
# Remove old primary node
kubectl delete pod postgres-cluster-0 --force
# Scale back to 3 replicas
kubectl patch statefulset postgres-cluster --patch '{"spec":{"replicas":3}}'
# Validate cluster health
kubectl exec postgres-cluster-3 -- psql -c "SELECT * FROM pg_stat_replication;"
# Test application connectivity
kubectl run test-db-connection --image=postgres:15 --rm -it -- psql -h postgres-primary -U app_user -d app_db -c "SELECT version();"
```


### Advanced configuration

For mission-critical databases that require a <10-second downtime:

```
# Use synchronous replication with multiple standbys
# postgresql.conf
synchronous_standby_names = 'ANY 2 (standby1, standby2, standby3)'
synchronous_commit = 'remote_apply'
```


### Success validation

To validate your progress, use the following checklist:

- New primary accepts reads and writes.
- All replicas show healthy replication.
- Application reconnects automatically.
- No data loss detected.
- Backup/restore tested on new primary.

### Emergency rollback

##### For immediate issues (<2 minutes)

Redirect traffic to the previous primary:

```
kubectl patch service postgres-primary --patch '{
"spec": {
"selector": {
"statefulset.kubernetes.io/pod-name": "postgres-cluster-1"
}
}
}'
```


##### For comprehensive failover recovery (5-10 minutes)

Stop writes to the current primary:

`kubectl exec postgres-primary-0 -- psql -c "SELECT pg_reload_conf();"`

Redirect service to a healthy replica:

`kubectl patch service postgres-primary --patch '{"spec":{"selector":{"statefulset.kubernetes.io/pod-name":"postgres-replica-1-0"}}}'`

Promote a replica to the new primary:

`kubectl exec postgres-replica-1-0 -- pg_ctl promote -D /var/lib/postgresql/data kubectl wait --for=condition=ready pod postgres-replica-1-0 --timeout=60s`

Update connection strings:

`kubectl patch configmap postgres-config --patch '{"data":{"primary-host":"postgres-replica-1-0.postgres"}}'`

Verify that the new primary accepts writes:

`kubectl exec postgres-replica-1-0 -- psql -c "CREATE TABLE upgrade_test (id serial, timestamp timestamp default now());" kubectl exec postgres-replica-1-0 -- psql -c "INSERT INTO upgrade_test DEFAULT VALUES;"`


**Expected outcome:** Approximately 30-second downtime, zero data loss, and an upgraded node that runs the current version of Kubernetes.

#### Step 3: Upgrade Node1 (former primary)

```
#!/bin/bash
# upgrade-node1.sh
echo "=== Step 3: Upgrade Node1 (Former Primary) ==="
# Drain Node1 gracefully
kubectl drain aks-nodepool1-12345678-vmss000000 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
# Trigger node upgrade
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Monitor upgrade progress
while kubectl get node aks-nodepool1-12345678-vmss000000 -o jsonpath='{.status.conditions[?(@.type=="Ready")].status}' | grep -q "False"; do
echo "Waiting for node upgrade to complete..."
sleep 30
done
echo "Node1 upgrade completed"
```


#### Step 4: Rejoin Node1 as a replica

```
#!/bin/bash
# rejoin-node1.sh
echo "=== Step 4: Rejoin Node1 as Replica ==="
# Wait for postgres pod to be scheduled on upgraded node
kubectl wait --for=condition=ready pod postgres-primary-0 --timeout=300s
# Reconfigure as replica pointing to new primary (Node2)
kubectl exec postgres-primary-0 -- bash -c "
echo 'standby_mode = on' >> /var/lib/postgresql/data/recovery.conf
echo 'primary_conninfo = \"host=postgres-replica-1-0.postgres port=5432\"' >> /var/lib/postgresql/data/recovery.conf
"
# Restart postgres to apply replica configuration
kubectl delete pod postgres-primary-0
kubectl wait --for=condition=ready pod postgres-primary-0 --timeout=120s
# Verify replication is working
kubectl exec postgres-replica-1-0 -- psql -c "SELECT * FROM pg_stat_replication WHERE application_name='postgres-primary-0';"
echo "Node1 successfully rejoined as replica"
```


#### Step 5: Upgrade Node3 (Replica-2)

```
#!/bin/bash
# upgrade-node3.sh
echo "=== Step 5: Upgrade Node3 (Replica-2) ==="
# Similar process for Node3
kubectl drain aks-nodepool1-12345678-vmss000002 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Wait for upgrade and pod readiness
kubectl wait --for=condition=ready pod postgres-replica-2-0 --timeout=300s
# Verify all replicas are in sync
kubectl exec postgres-replica-1-0 -- psql -c "SELECT application_name, state, sync_state FROM pg_stat_replication;"
```


#### Step 6: Final failover (Node2 → Node3)

```
#!/bin/bash
# final-failover.sh
echo "=== Step 6: Final Failover and Node2 Upgrade ==="
# Failover primary from Node2 to Node3
kubectl patch service postgres-primary --patch '{"spec":{"selector":{"statefulset.kubernetes.io/pod-name":"postgres-replica-2-0"}}}'
kubectl exec postgres-replica-2-0 -- pg_ctl promote -D /var/lib/postgresql/data
# Upgrade Node2
kubectl drain aks-nodepool1-12345678-vmss000001 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Rejoin Node2 as replica
kubectl wait --for=condition=ready pod postgres-replica-1-0 --timeout=300s
echo "All nodes upgraded successfully. PostgreSQL cluster operational."
```


### Validation and monitoring

```
#!/bin/bash
# post-upgrade-validation.sh
echo "=== Post-Upgrade Validation ==="
# Verify cluster topology
kubectl get pods -l app=postgres -o wide
# Check all replicas are connected
kubectl exec postgres-replica-2-0 -- psql -c "SELECT application_name, client_addr, state FROM pg_stat_replication;"
# Validate data integrity
kubectl exec postgres-replica-2-0 -- psql -c "SELECT COUNT(*) FROM upgrade_test;"
# Performance validation
kubectl exec postgres-replica-2-0 -- psql -c "EXPLAIN ANALYZE SELECT * FROM pg_stat_activity;"
echo "Upgrade validation completed successfully"
```


## Redis cluster rolling replace

In this scenario, a six-node Redis cluster (three primaries and three replicas) requires zero downtime.

### Implementation

```
#!/bin/bash
# redis-cluster-upgrade.sh
echo "=== Redis Cluster Rolling Upgrade ==="
# Get cluster topology
kubectl exec redis-0 -- redis-cli cluster nodes
# Upgrade replica nodes first (no impact to writes)
for replica in redis-1 redis-3 redis-5; do
echo "Upgrading replica: $replica"
# Remove replica from cluster temporarily
REPLICA_ID=$(kubectl exec redis-0 -- redis-cli cluster nodes | grep $replica | cut -d' ' -f1)
kubectl exec redis-0 -- redis-cli cluster forget $REPLICA_ID
# Drain and upgrade node
kubectl delete pod $replica
kubectl wait --for=condition=ready pod $replica --timeout=120s
# Rejoin cluster
kubectl exec redis-0 -- redis-cli cluster meet $(kubectl get pod $replica -o jsonpath='{.status.podIP}') 6379
echo "Replica $replica upgraded and rejoined"
done
# Upgrade master nodes with failover
for master in redis-0 redis-2 redis-4; do
echo "Upgrading master: $master"
# Trigger failover to replica
kubectl exec $master -- redis-cli cluster failover
# Wait for failover completion
sleep 10
# Upgrade the demoted master (now replica)
kubectl delete pod $master
kubectl wait --for=condition=ready pod $master --timeout=120s
echo "Master $master upgraded"
done
echo "Redis cluster upgrade completed"
```


## MongoDB replica set step-down

In this scenario, a three-member MongoDB replica set requires coordinated primary step-down.

### Implementation

```
#!/bin/bash
# MongoDB upgrade script
Echo "=== MongoDB Replica Set Upgrade ==="
# Check replica set status
kubectl exec mongo-0 --mongo --eval "rs.status()"
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-logs -->

# What is container network logs (preview)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Component renaming (starting November 11, 2025)

We are renaming components in the Container Network Logs feature to improve clarity and consistency:

What's changing

**CRD**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`

**CLI flag**:`--enable-retinanetworkflowlog`

→`--enable-container-network-logs`

**Log Analytics table**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`


Action items for existing users to enable new naming

**Update Azure CLI**(MUST - First step!):`az upgrade`

**Update Preview CLI Extension**(MUST):`az extension update --name aks-preview`

**Disable Monitoring**:`az aks disable-addons -a monitoring -n <cluster-name> -g <resource-group>`

**Re-enable Monitoring**:`az aks enable-addons -a monitoring --enable-high-log-scale-mode -g <resource-group> -n <cluster-name>`

**Re-enable ACNS Container Network Logs**:`az aks update --enable-acns --enable-container-network-logs -g <resource-group> -n <cluster-name>`

**Apply new ContainerNetworkLog CRD**: Apply your updated CRD configuration with the new naming.**Reimport Grafana Dashboards**: Import the updated dashboards to reflect the new table names.

Note

- Previously collected data stays in your workspace in old table RetinaNetworkFlowLogs.
- After re-enabling, allow a short delay before new data appears in new table ContainerNetworkLog.

Container network logs in [Advanced Container Networking Services](advanced-container-networking-services-overview) for Azure Kubernetes Service (AKS) provide comprehensive, context-rich visibility into every network flow within your cluster. While metrics tell you *what* is happening in your network (such as bandwidth usage or error rates), container network logs tell you *why* by capturing the complete story of each connection—including who initiated it, what protocols were used, and whether the traffic was allowed or blocked.

These logs capture essential metadata for every network flow, including source and destination IP addresses, pod and service names, namespaces, ports, protocols, traffic direction, and policy verdicts. This deep contextual information enables you to correlate network behavior with specific workloads, troubleshoot connectivity issues, validate security policies, and perform forensic analysis.

Container network logs capture Layer 3 (IP), Layer 4 (TCP/UDP), and Layer 7 (HTTP/gRPC/Kafka) traffic, providing the detailed insights you need to monitor connectivity, troubleshoot issues, visualize network topology, enforce security policies, and ensure compliance.

Choose from two modes:

- Stored logs
- On-demand logs

## Stored logs

Stored logs mode ensures continuous log generation and collection in the AKS cluster when you enable Advanced Container Networking Services and set up custom filters. By default, log collection is disabled.

To enable log collection, you define *custom resources* to specify the types of traffic to monitor. Examples include namespaces, pods, services, and protocols. This feature remains active until you disable it.

Stored logs mode supports extended log retention and traffic filtering. For reduced storage costs and easier analysis, you can collect and retain only the logs that are relevant to you.

### How stored logs mode works

Advanced Container Networking Services uses eBPF technology with Cilium to fetch logs from nodes in your cluster. To start collecting logs, you define one or more custom resources to specify the types of traffic to monitor.

Custom resources provide fine-grained control to define and capture the traffic that is relevant to you. The Cilium agent running on each node collects network traffic that matches the criteria set in the custom resources. The logs are stored in JSON format on the host, providing a structured and accessible format for further use.

Alternatively, if the Azure Monitoring add-on is enabled, agents for Container insights collect the logs from the host, apply the default throttling limits, and send them to a Log Analytics workspace. The system aggregates and stores logs efficiently to provide visibility into network traffic for monitoring, troubleshooting, and security enforcement.

To read more about throttling and Container insights, see the [Container insights documentation](https://aka.ms/ContainerNetworkLogsDoc_CI).

### Key capabilities of stored logs mode

*Customizable filters.*You can configure logging by defining custom resources of the[ContainerNetworkLog](how-to-configure-container-network-logs#containernetworklog-crd-template)type. Use custom resources to apply granular filters by namespace, pod, service, port, protocol, verdict, or traffic direction (ingress or egress). This flexibility ensures precise data collection tailored to specific use cases. Only relevant traffic is logged, and storage is optimized for improved performance, compliance, and troubleshooting.*Log storage options.*The container network logs feature has two primary storage options: unmanaged storage and managed storage.**Unmanaged storage:**When a custom resource is applied to begin log collection, network flow logs are stored locally on the host nodes at the`/var/log/acns/hubble`

fixed mount location. This storage location is temporary because the node itself isn't a persistent storage solution. When the log files reach a size of 50 MB, they're automatically rotated and older logs are overwritten. This storage solution is suitable for real-time monitoring, but it doesn't support long-term storage or retention.For additional log management capabilities, you can integrate partner logging services like an OpenTelemetry collector. Partner integrations provide flexibility to manage logs outside the Azure ecosystem and are useful if you've already deployed a specific log management platform.

**Managed storage:**For long-term retention and advanced analytics, we recommend that you configure Azure monitoring in your AKS cluster to collect and store logs in a Log Analytics workspace. This setup ensures secure and compliant log storage. It also provides access to powerful capabilities like anomaly detection, performance tuning, and historical data analysis. You can use historical logs to identify trends, baseline behaviors, and proactively address recurring issues.For example, you can use the managed service for Prometheus to configure alerts on both metrics and logs for real-time monitoring and rapid detection of outliers.

You use the same workspace for log storage. You set up log storage space during onboarding. Both Analytics and Basic log table plans are supported for this feature. For more detailed information on table plans, see

[Azure Monitor Logs](/en-us/azure/azure-monitor/logs/data-platform-logs).

*Simple visualization in Log Analytics and Grafana dashboards.*Logs and data presented in Grafana dashboards simplify complex information, facilitate data comprehension, and help you make decisions more quickly.

### Logs visualization in the Azure portal

You can visualize, query, and analyze flow logs in the Azure portal in the Log Analytics workspace for your cluster.

### Logs visualization in Grafana dashboards

Access the flow logs in an Azure Managed Grafana instance.

To simplify your analysis of logs, we provide two preconfigured Grafana dashboards:

Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs**. This dashboard shows which AKS workloads are communicating with each other, including network requests, responses, drops, and errors. Currently, as an interim step during preview, you must import Grafana dashboards by using a user ID to view the flow logs dashboard in the Azure portal.Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs (External Traffic)**. This dashboard shows which AKS workloads send and receive communications from outside an AKS cluster, including network requests, responses, drops, and errors.For more information, see

[Set up Azure Managed Grafana with Advanced Container Networking Services](how-to-configure-container-network-logs#visualization-in-grafana-dashboards).

Access the flow logs in the Azure portal via the

**Dashboards with Grafana**option.

The Azure portal dashboards have the following major components:

*A comprehensive overview of network health.*You see key metrics like total flow logs, unique requests, dropped requests, and forwarded requests for quick anomaly detection and efficient troubleshooting. The dashboard categorizes statistics by protocol and behavior, including DNS dropped requests, HTTP 2xx responses, Layer 4 request and response rates, and dropped request counts. A service dependency graph visualizes application or cluster interactions, highlighting traffic flow, bottlenecks, and dependencies for performance optimization.*Flow logs and error logs for quick analysis.*You can filter flow logs for root-cause analysis. For example, to troubleshoot Domain Name System (DNS) issues, filter error logs by the DNS protocol.Separating flow logs and error logs helps you analyze issues more quickly. You can identify and address errors without sifting through unrelated information, which improves efficiency in troubleshooting and debugging processes.

Use clear labels and timestamps for each log entry to more easily pinpoint specific events or errors in your systems or processes.

*Top namespaces, workloads, and DNS errors.*Network flow log visualization is vital for monitoring and analyzing communication in an AKS cluster. It provides insight into namespaces, workloads, port usage, and query usage. It helps you identify trends, detect bottlenecks, and diagnose issues. Spot significant network activity, view dropped requests, and assess protocol distribution (for example, TCP versus UDP). This overview section of the dashboard supports cluster health, resource optimization, and security by detecting and displaying unusual traffic patterns.

## On-demand logs

Advanced Container Networking Services offers on-demand capture of network flow logs. Get real-time visibility without prior configuration or persistent storage by using the Hubble CLI and the Hubble UI. This on-demand logs mode is available. To learn how to set up on-demand log storage, see [Configure the Hubble CLI and Hubble UI](how-to-configure-container-network-logs#configure-on-demand-logs-mode).

### Hubble CLI

The Hubble command-line interface (CLI) provides a flexible and interactive way to query, filter, and analyze flow logs directly in the terminal. You can execute real-time commands to inspect traffic flows, view packet metadata, and troubleshoot network issues without leaving your operational environment.

### Hubble UI

The Hubble web-based interface offers an intuitive and visual platform for monitoring. With features like live traffic dashboards, flow summaries, and searchable logs, you can easily track service-to-service communication, detect anomalies, and gain insights into cluster activity.

The Hubble UI tools provide real-time visibility and actionable insights for faster troubleshooting and improved network management.

### Key benefits of on-demand logs

*Faster issue resolution.*With detailed and actionable insights into network traffic, you can identify and resolve connectivity or performance issues more quickly, minimizing downtime and disruptions.*Optimized operational efficiency.*Aggregated and efficiently stored logs reduce data management overhead. Your team can focus on analysis and decision-making instead of managing large volumes of raw data.*Enhanced application reliability.*By monitoring service-to-service communication and detecting anomalies, you can proactively address potential issues and ensure a smoother and more reliable application experience.*Improved decision-making.*Visualizing network patterns in Azure Managed Grafana and applying service maps provide clear insights into your application's network behavior. This leads to improved infrastructure planning and optimization.*Cost savings.*Efficient log aggregation and customizable logging scopes reduce storage and data ingestion costs, providing a cost-effective solution for long-term network monitoring.*Streamlined compliance and security.*Persistent and comprehensive logs support audit trails, regulatory compliance, and quick identification of suspicious traffic. They help you maintain a secure and compliant environment.

## Limitations

- Container network logs in stored logs mode currently works only with the Cilium data plane.
- Layer 7 flow logs are captured only when Layer 7 policy support is enabled. For more information, see
[Configure a Layer 7 policy](how-to-apply-l7-policies). - DNS flows and metrics are captured only when a Cilium Fully Qualified Domain (FQDN) network policy is applied. For more information, see
[Configure an FQDN policy](how-to-apply-fqdn-filtering-policies). - Onboarding by using Terraform currently isn't supported.
- When Log Analytics isn't configured for log storage, container network logs are limited to a maximum of 50 MB of storage. When this limit is reached, new entries overwrite older logs.
- If the table plan is set to Basic logs, prebuilt Grafana dashboards don't work.
- The Auxiliary logs table plan isn't supported.

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- Learn how to set up
[container network logs](how-to-configure-container-network-logs). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dapr-settings -->

# Configure the Dapr extension for your Azure Kubernetes Service (AKS) and Arc-enabled Kubernetes project

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After [completing the prerequisites for installing the Dapr extension](dapr), you can configure the [Dapr](https://dapr.io/) extension to work best for you and your project using various configuration options, like:

- Rotating expiring certificates
- Provisioning Dapr with high availability (HA) enabled
- Limiting which of your nodes use the Dapr extension
- Setting automatic custom resource definition (CRD) updates
- Configuring the Dapr release namespace

The extension enables you to set Dapr configuration options by using the `--configuration-settings`

parameter in the Azure CLI or `configurationSettings`

property in a Bicep template.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Update configuration settings

Important

Some configuration options cannot be modified post-creation. Adjustments to these options require deletion and recreation of the extension, applicable to the following settings:

`global.ha.*`

`dapr_placement.*`


HA is enabled by default. Disabling it requires deletion and recreation of the extension.

To update your Dapr configuration settings, recreate the extension with the desired state. For example, let's say you previously created and installed the extension using the following configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2"
```


To update the `dapr_operator.replicaCount`

from two to three, use the following command:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=3"
```


## Manage mTLS certificates

The Dapr extension supports in-transit encryption of communication between Dapr instances using the Dapr Sentry service control plane, which is a central Certificate Authority (CA). With the Sentry service, you can encrypt communication using self-signed or user-supplied x.509 certificates. [Learn more about setting up mTLS certificates in the open-source Dapr documentation.](https://docs.dapr.io/operations/security/mtls/#dapr-generated-self-signed-certificates)

You can [bring in your own certificates](https://docs.dapr.io/operations/security/mtls/#bringing-your-own-certificates), or let [Dapr automatically create and persist self-signed root and issuer certificates](https://docs.dapr.io/operations/security/mtls/#dapr-generated-self-signed-certificates).

Important

If you don't explicitly configure certificates, [Dapr defaults to generating self-signed certificates](#manage-dapr-generated-self-signed-certificates), which are generally valid for 1 year. **Currently, using self-signed certificates generated by Dapr is not recommended.** Best practice is to generate custom certificates and update them manually.

### Manage Dapr-generated self-signed certificates

If you haven't provided any custom certificates, Dapr automatically creates and persists self-signed certificates, valid for 1 year. The Dapr extension installs the `dapr-trust-bundle`

secret, which contains certificate information under the default `dapr-system`

namespace.

#### Check expiry of current Dapr-generated self-signed certificates

You can check when the Dapr root certificate of your Kubernetes cluster expires by using [the Dapr CLI](https://docs.dapr.io/getting-started/install-dapr-cli/).

```
dapr mtls expiry
```


**Expected output:**

```
Root certificate expires in 8759 hours. Expiry date: 2025-12-06 18:14:20 +0000 UTC
```


You can also find the expiration date for your current certificate in the Kubernetes `dapr-trust-bundle`

secret data.

```
kubectl get secret dapr-trust-bundle -n dapr-system -o jsonpath='{.data.issuer\.crt}' | base64 -d | openssl x509 -noout -dates
```


**Expected output:**

```
notBefore=Dec 6 17:59:20 2024 GMT
notAfter=Dec 6 18:14:20 2025 GMT
```


#### Generate a new Dapr-generated self-signed certificate

**Via the Dapr CLI (recommended)**

Refer to Dapr's[Root and issuer certificate upgrade using CLI](https://docs.dapr.io/operations/security/mtls/#root-and-issuer-certificate-upgrade-using-cli-recommended)guide.**Via**Refer to Dapr's`kubectl`

commands[Updating root or issuer certs using Kubectl](https://docs.dapr.io/operations/security/mtls/#updating-root-or-issuer-certs-using-kubectl)guide.

### Manage your own user-supplied x.509 certificates

You can also bring your own custom certificates.

**Generate custom certificates**

Create your own custom certificate; for example,[an Azure Key Vault certificate](/en-us/azure/key-vault/certificates/certificate-scenarios).**Update your custom certficate manually**

Follow[the instructions provided in the Dapr open source documentation to update your custom certificates manually](https://docs.dapr.io/operations/security/mtls/#custom-certificates-bring-your-own)using.`kubectl`


## Provision Dapr with high availability (HA) enabled

Provision Dapr with high availability (HA) enabled by setting the `global.ha.enabled`

parameter to `true`

.

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2"
```


Note

If configuration settings are sensitive and need to be protected (for example, cert-related information), pass the `--configuration-protected-settings`

parameter and the value will be protected from being read.

If no configuration-settings are passed, the Dapr configuration defaults to:

```
ha:
enabled: true
replicaCount: 3
disruption:
minimumAvailable: ""
maximumUnavailable: "25%"
prometheus:
enabled: true
port: 9090
mtls:
enabled: true
workloadCertTTL: 24h
allowedClockSkew: 15m
```


For a list of available options, see [Dapr configuration](https://github.com/dapr/dapr/blob/master/charts/dapr/README.md#configuration).

## Limit the extension to certain nodes

In some configurations, you may only want to run Dapr on certain nodes. You can limit the extension by passing a `nodeSelector`

in the extension configuration. If the desired `nodeSelector`

contains `.`

, you must escape them from the shell and the extension. For example, the following configuration installs Dapr only to nodes with `topology.kubernetes.io/zone: "us-east-1c"`

:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2" \
--configuration-settings "global.nodeSelector.kubernetes\.io/zone=us-east-1c"
```


For managing OS and architecture, use the [supported versions](https://github.com/dapr/dapr/blob/b8ae13bf3f0a84c25051fcdacbfd8ac8e32695df/docker/docker.mk#L50) of the `global.daprControlPlaneOs`

and `global.daprControlPlaneArch`

configuration:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_operator.replicaCount=2" \
--configuration-settings "global.daprControlPlaneOs=linux" \
--configuration-settings "global.daprControlPlaneArch=amd64"
```


## Install Dapr in multiple availability zones while in HA mode

By default, the placement service uses a storage class of type `standard_LRS`

. It's recommended to create a **zone redundant storage class** while installing Dapr in HA mode across multiple availability zones. For example, to create a `zrs`

type storage class, add the `storageaccounttype`

parameter:

```
kind: StorageClass
apiVersion: storage.k8s.io/v1
metadata:
name: custom-zone-redundant-storage
provisioner: disk.csi.azure.com
reclaimPolicy: Delete
allowVolumeExpansion: true
volumeBindingMode: WaitForFirstConsumer
parameters:
storageaccounttype: Premium_ZRS
```


When installing Dapr, use the storage class you used in the YAML file:

```
az k8s-extension create --cluster-type managedClusters
--cluster-name XXX
--resource-group XXX
--name XXX
--extension-type Microsoft.Dapr
--auto-upgrade-minor-version XXX
--version XXX
--configuration-settings "dapr_placement.volumeclaims.storageClassName=custom-zone-redundant-storage"
```


## Configure the Dapr release namespace

You can configure the release namespace.

The Dapr extension gets installed in the `dapr-system`

namespace by default. To override it, use `--release-namespace`

. To redefine the namespace, include the cluster `--scope`

.

```
az k8s-extension create \
--cluster-type managedClusters \
--cluster-name dapr-aks \
--resource-group dapr-rg \
--name my-dapr-ext \
--extension-type microsoft.dapr \
--release-train stable \
--auto-upgrade false \
--version 1.9.2 \
--scope cluster \
--release-namespace dapr-custom
```


## Show current configuration settings

Use the `az k8s-extension show`

command to show the current Dapr configuration settings:

```
az k8s-extension show --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr
```


## Set Dapr monitoring log levels

You can configure settings for the Dapr monitoring component with your AKS cluster extension. For exmaple, to update `dapr_monitoring`

log levels to "warn" (only notified when receiving a warning or error), set the following `configuration-settings`

:

```
az k8s-extension create --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--extension-type Microsoft.Dapr \
--auto-upgrade-minor-version true \
--configuration-settings "global.ha.enabled=true" \
--configuration-settings "dapr_monitoring.logLevel=warn"
```


## Set the outbound proxy for Dapr extension for Azure Arc on-premises

If you want to use an outbound proxy with the Dapr extension for AKS, you can do so by:

- Setting the proxy environment variables using the
:`dapr.io/env`

annotations`HTTP_PROXY`

`HTTPS_PROXY`

`NO_PROXY`


[Installing the proxy certificate in the sidecar](https://docs.dapr.io/operations/configuration/install-certificates/).

## Updating your Dapr installation version

If you are on a specific Dapr version and you don't have `--auto-upgrade-minor-version`

available, you can use the following command to upgrade or downgrade Dapr:

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--version 1.12.0 # Version to upgrade or downgrade to
```


The preceding command updates the Dapr control plane *only.* To update the Dapr sidecars, restart your application deployments:

```
kubectl rollout restart deploy/<DEPLOYMENT-NAME>
```


## Using Azure Linux-based images

From Dapr version 1.8.0, you can use Azure Linux images with the Dapr extension. To use them, set the `global.tag`

flag:

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--set global.tag=1.10.0-mariner
```


[Learn more about using Mariner-based images with Dapr](https://docs.dapr.io/operations/hosting/kubernetes/kubernetes-deploy/#using-mariner-based-images).[Learn more about deploying Azure Linux on AKS](cluster-configuration#azure-linux-container-host-for-aks).

## Disable automatic CRD updates

From Dapr version 1.9.2, CRDs are automatically upgraded when the extension upgrades. To disable this setting, you can set `hooks.applyCrds`

to `false`

.

```
az k8s-extension update --cluster-type managedClusters \
--cluster-name myAKSCluster \
--resource-group myResourceGroup \
--name dapr \
--configuration-settings "hooks.applyCrds=false"
```


Note

CRDs are only applied in case of upgrades and are skipped during downgrades.

## Meet network requirements

The Dapr extension requires the following outbound URLs on `https://:443`

to function on AKS and Arc for Kubernetes:

`https://mcr.microsoft.com/daprio`

URL for pulling Dapr artifacts.- The
[outbound URLs required for AKS or Arc for Kubernetes](/en-us/azure/azure-arc/kubernetes/network-requirements).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/istio-upgrade -->

# Upgrade Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article addresses upgrade experiences for Istio-based service mesh add-on for Azure Kubernetes Service (AKS).

Announcements about the releases of new minor revisions or patches to the Istio-based service mesh add-on are published in the [AKS release notes](https://github.com/Azure/AKS/releases). To learn more about the release schedule and support for service mesh add-on revisions, read the [support policy](istio-support-policy#versioning-and-support-policy).

## Minor revision upgrade

Istio add-on allows upgrading the minor revision using [canary upgrade process](https://istio.io/latest/docs/setup/upgrade/canary/). When an upgrade is initiated, the control plane of the new (canary) revision is deployed alongside the initial (stable) revision's control plane. You can then manually roll over data plane workloads while using monitoring tools to track the health of workloads during this process. If you don't observe any issues with the health of your workloads, you can complete the upgrade so that only the new revision remains on the cluster. Else, you can roll back to the previous revision of Istio.

Available upgrades depend on whether the current Istio revision and AKS cluster version are supported:

- You can upgrade to the
**next supported revision (**or skip one and upgrade to`n+1`

), as long as both are supported and compatible with the cluster version.`n+2`

- If both your current revision (
`n`

) and the next revision (`n+1`

) are unsupported, you can only upgrade to the**nearest supported revision (**, but not beyond it.`n+2`

or higher) - If the cluster version and Istio revision are both unsupported, the cluster version must be upgraded before an Istio upgrade can be initiated.

Note

Once an AKS version or mesh revision falls outside the support window, upgrading either version becomes error-prone. While such upgrades are **allowed** to recover to a supported version, **the upgrade process and the out-of-support versions themselves are both not supported by Microsoft**. We strongly recommend keeping AKS version and mesh revision up to date to avoid running into unsupported scenarios. Refer to the [Istio add-on support calendar](istio-support-policy#service-mesh-add-on-release-calendar) for estimated release and end-of-life dates and the [upstream Istio release notes](https://istio.io/latest/news/releases/) for the new revision for notable changes.

The following example illustrates how to upgrade from revision `asm-1-23`

to `asm-1-24`

with all workloads in the `default`

namespace. The steps are the same for all minor upgrades and may be used for any number of namespaces.

Use the

[az aks mesh get-upgrades](/en-us/cli/azure/aks/mesh#az-aks-mesh-get-upgrades)command to check which revisions are available for the cluster as upgrade targets:`az aks mesh get-upgrades --resource-group $RESOURCE_GROUP --name $CLUSTER`

If you expect to see a newer revision not returned by this command, you may need to upgrade your AKS cluster first so that it's compatible with the newest revision.

If you set up

[mesh configuration](istio-meshconfig)for the existing mesh revision on your cluster, you need to create a separate ConfigMap corresponding to the new revision in the`aks-istio-system`

namespace**before initiating the canary upgrade**in the next step. This configuration is applicable the moment the new revision's control plane is deployed on cluster. More details can be found[here](istio-meshconfig#mesh-configuration-and-upgrades).Initiate a canary upgrade from revision

`asm-1-23`

to`asm-1-24`

using[az aks mesh upgrade start](/en-us/cli/azure/aks/mesh/upgrade#az-aks-mesh-upgrade-start):`az aks mesh upgrade start --resource-group $RESOURCE_GROUP --name $CLUSTER --revision asm-1-24`

A canary upgrade means the 1.24 control plane is deployed alongside the 1.23 control plane. They continue to coexist until you either complete or roll back the upgrade.

While a canary upgrade is in progress, the higher revision is considered the

*default revision*used for validation of Istio resources.Optionally, revision tags may be used to roll over the data plane to the new revision without needing to manually relabel each namespace. Manually relabeling namespaces when moving them to a new revision can be tedious and error-prone.

[Revision tags](https://istio.io/latest/docs/setup/upgrade/canary/#stable-revision-labels)solve this problem by serving as stable identifiers that point to revisions.Rather than relabeling each namespace, a cluster operator can change the tag to point to a new revision. All namespaces labeled with that tag are updated at the same time. However, you still need to restart the workloads to make sure the correct version of

`istio-proxy`

sidecars are injected.To use revision tags during an upgrade:

Create a revision tag for the initial revision. In this example, we name it

`prod-stable`

:`istioctl tag set prod-stable --revision asm-1-23 --istioNamespace aks-istio-system`

Create a revision tag for the revision installed during the upgrade. In this example, we name it

`prod-canary`

:`istioctl tag set prod-canary --revision asm-1-24 --istioNamespace aks-istio-system`

Label application namespaces to map to revision tags:

`# label default namespace to map to asm-1-23 kubectl label ns default istio.io/rev=prod-stable --overwrite`

You may also label namespaces with

`istio.io/rev=prod-canary`

for the newer revision. However, the workloads in those namespaces aren't updated to a new sidecar until they're restarted.If a new application is created in a namespace after it is labeled, a sidecar will be injected corresponding to the revision tag on that namespace.


Verify control plane pods corresponding to both

`asm-1-23`

and`asm-1-24`

exist:Verify

`istiod`

pods:`kubectl get pods -n aks-istio-system`

Example output:

`NAME READY STATUS RESTARTS AGE istiod-asm-1-23-55fccf84c8-dbzlt 1/1 Running 0 58m istiod-asm-1-23-55fccf84c8-fg8zh 1/1 Running 0 58m istiod-asm-1-24-f85f46bf5-7rwg4 1/1 Running 0 51m istiod-asm-1-24-f85f46bf5-8p9qx 1/1 Running 0 51m`

If ingress is enabled, verify ingress pods:

`kubectl get pods -n aks-istio-ingress`

Example output:

`NAME READY STATUS RESTARTS AGE aks-istio-ingressgateway-external-asm-1-23-58f889f99d-qkvq2 1/1 Running 0 59m aks-istio-ingressgateway-external-asm-1-23-58f889f99d-vhtd5 1/1 Running 0 58m aks-istio-ingressgateway-external-asm-1-24-7466f77bb9-ft9c8 1/1 Running 0 51m aks-istio-ingressgateway-external-asm-1-24-7466f77bb9-wcb6s 1/1 Running 0 51m aks-istio-ingressgateway-internal-asm-1-23-579c5d8d4b-4cc2l 1/1 Running 0 58m aks-istio-ingressgateway-internal-asm-1-23-579c5d8d4b-jjc7m 1/1 Running 0 59m aks-istio-ingressgateway-internal-asm-1-24-757d9b5545-g89s4 1/1 Running 0 51m aks-istio-ingressgateway-internal-asm-1-24-757d9b5545-krq9w 1/1 Running 0 51m`

Observe that ingress gateway pods of both revisions are deployed side-by-side. However, the service and its IP remain immutable.


Relabel the namespace so that any new pods are mapped to the Istio sidecar associated with the new revision and its control plane:

If using revision tags, overwrite the

`prod-stable`

tag itself to change its mapping:`istioctl tag set prod-stable --revision asm-1-24 --istioNamespace aks-istio-system --overwrite`

Verify the tag-to-revision mappings:

`istioctl tag list`

Both tags should point to the newly installed revision:

`TAG REVISION NAMESPACES prod-canary asm-1-24 default prod-stable asm-1-24 ...`

In this case, you don't need to relabel each namespace individually.

If not using revision tags, data plane namespaces must be relabeled to point to the new revision:

`kubectl label namespace default istio.io/rev=asm-1-24 --overwrite`


Relabeling doesn't affect your workloads until they're restarted.

Individually roll over each of your application workloads by restarting them. For example:

`kubectl rollout restart deployment <deployment name> -n <deployment namespace>`

Check your monitoring tools and dashboards to determine whether your workloads are all running in a healthy state after the restart. Based on the outcome, you have two options:

**Complete the canary upgrade**: If you're satisfied that the workloads are all running in a healthy state as expected, you can complete the canary upgrade. Completion of the upgrade removes the previous revision's control plane and leaves behind the new revision's control plane on the cluster. Run the following command to complete the canary upgrade:`az aks mesh upgrade complete --resource-group $RESOURCE_GROUP --name $CLUSTER`

**Rollback the canary upgrade**: In case you observe any issues with the health of your workloads, you can roll back to the previous revision of Istio:

Relabel the namespace to the previous revision: If using revision tags:

`istioctl tag set prod-stable --revision asm-1-23 --istioNamespace aks-istio-system --overwrite`

Or, if not using revision tags:

`kubectl label namespace default istio.io/rev=asm-1-23 --overwrite`

Roll back the workloads to use the sidecar corresponding to the previous Istio revision by restarting these workloads again:

`kubectl rollout restart deployment <deployment name> -n <deployment namespace>`

Roll back the control plane to the previous revision:

`az aks mesh upgrade rollback --resource-group $RESOURCE_GROUP --name $CLUSTER`


The

`prod-canary`

revision tag can be removed:`istioctl tag remove prod-canary --istioNamespace aks-istio-system`

If

[mesh configuration](istio-meshconfig)was previously set up for the revisions, you can now delete the ConfigMap for the revision that was removed from the cluster during complete/rollback.

### Minor revision upgrades with ingress and egress gateways

If you're currently using [Istio ingress gateways](istio-deploy-ingress) or [egress gateways](istio-deploy-egress) and are performing a minor revision upgrade, keep in mind that Istio ingress and egress gateway pods / deployments are deployed per-revision, but the service is shared across both revisions.

We provide a single `LoadBalancer`

service across all ingress gateway pods over multiple revisions, so the external/internal IP address of the ingress gateways remains unchanged throughout the course of an upgrade. Thus, during the canary upgrade, when two revisions exist simultaneously on the cluster, the ingress gateway pods of both revisions serve incoming traffic.

Likewise, during a canary upgrade, all pods for an egress gateway across both revisions will be served by a single `ClusterIP`

service.

### Minor revision upgrades with horizontal pod autoscaling customizations

If you have customized [horizontal pod autoscaling (HPA) settings for Istiod or the ingress gateways](istio-scale#horizontal-pod-autoscaling-customization), note the following behavior for how HPA settings are applied across both revisions to maintain consistency during a canary upgrade:

- If you update the HPA spec before initiating an upgrade, the settings from the existing (stable) revision will be applied to the HPAs of the canary revision when the new control plane is installed.
- If you update the HPA spec while a canary upgrade is in progress, the HPA spec of the stable revision will take precedence and be applied to the HPA of the canary revision.
- If you update the HPA of the stable revision during an upgrade, the HPA spec of the canary revision will be updated to reflect the new settings applied to the stable revision.
- If you update the HPA of the canary revision during an upgrade, the HPA spec of the canary revision will be reverted to the HPA spec of the stable revision.


## Patch version upgrade

- Istio add-on patch version availability information is published in
[AKS release notes](https://github.com/Azure/AKS/releases). - Patches are rolled out automatically for istiod and ingress pods as part of these AKS releases, which respect the
`default`

[planned maintenance window](planned-maintenance)set up for the cluster. - User needs to initiate patches to Istio proxy in their workloads by restarting the pods for reinjection:
Check the version of the Istio proxy intended for new or restarted pods. This version is the same as the version of the istiod and Istio ingress pods after they were patched:

`kubectl get cm -n aks-istio-system -o yaml | grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`"image": "mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless", "image": "mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless"`

Check the Istio proxy image version for all pods in a namespace:

`kubectl get pods --all-namespaces -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' |\ sort |\ grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`productpage-v1-979d4d9fc-p4764: docker.io/istio/examples-bookinfo-productpage-v1:1.23.0, mcr.microsoft.com/oss/istio/proxyv2:1.23.0-distroless`

To trigger reinjection, restart the workloads. For example:

`kubectl rollout restart deployments/productpage-v1 -n default`

To verify that they're now on the newer versions, check the Istio proxy image version again for all pods in the namespace:

`kubectl get pods --all-namespaces -o jsonpath='{range .items[*]}{"\n"}{.metadata.name}{":\t"}{range .spec.containers[*]}{.image}{", "}{end}{end}' |\ sort |\ grep "mcr.microsoft.com\/oss\/istio\/proxyv2"`

Example output:

`productpage-v1-979d4d9fc-p4764: docker.io/istio/examples-bookinfo-productpage-v1:1.2.0, mcr.microsoft.com/oss/istio/proxyv2:1.24.0-distroless`


Note

In case of any issues encountered during upgrades, refer to [article on troubleshooting mesh revision upgrades](/en-us/troubleshoot/azure/azure-kubernetes/extensions/istio-add-on-minor-revision-upgrade)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/automated-deployments -->

# Automated deployments for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Automated Deployments streamline the process of setting up a GitHub Action or Azure DevOps Pipeline, making it easy to create a continuous deployment pipeline for your application to Azure Kubernetes Service (AKS). Once connected, every new commit automatically triggers the pipeline, delivering updates to your application seamlessly. You can either bring your own deployment files for quick pipeline creation or generate Dockerfiles and Kubernetes manifests to containerize and deploy non-containerized applications with minimal effort.

## Prerequisites

- A GitHub account or an Azure DevOps organization.
- An AKS cluster. If you don't have one, you can create one using the steps in
[Deploy an Azure Kubernetes Service (AKS) cluster](learn/quick-kubernetes-deploy-portal). - An Azure Container Registry (ACR). If you don't have one, you can create one using the steps in
[Integrate Azure Container Registry (ACR) with an Azure Kubernetes Service (AKS) cluster](cluster-container-registry-integration). - An application to deploy.

### Connect to source code repository

Create an automated deployment workflow and authorize it to connect to the desired source code repository.

- In the Azure portal, navigate to your AKS cluster resource.
- From the service menu, under
**Settings**, select**Automated deployments**>**Create**. - Under
**Repository details**, enter a name for the workflow, then select**GitHub or ADO**for your repository location. - Select
**Authorize access**to connect to the desired repository. - Choose the
**Repository**and**Branch**, and then select**Next**.

### Choose the container image configuration

To get an application ready for Kubernetes, you need to build it into a container image and store it in a container registry. You use a Dockerfile to provide instructions on how to build the container image. If your source code repository doesn't already have a Dockerfile, Automated Deployments can generate one for you. Otherwise, you can use an existing Dockerfile.

Use Automated Deployments to generate a Dockerfile for many languages and frameworks such as Go, C#, Node.js, Python, Java, Gradle, Clojure, PHP, Ruby, Erlang, Swift, and Rust. The language support is built on what's available in [draft.sh](https://draft.sh).

- Select
**Auto-containerize (generate Dockerfile)**for the container configuration. - Select the
**location of where to save the generated Dockerfile**in the repository. - Select the
**application environment**from the list of supported languages and frameworks. - Enter the
**application port**. - Provide the
**Dockerfile build context**path. - Select an existing
**Azure Container Registry**or create a new one. This registry is used to store the built application image.

### Choose the Kubernetes manifest configuration

Note

The Generate Manifests option also supports advanced features like Service Connector integration, auto-generated Ingress resources, and more detailed, customizable Kubernetes manifest files.

An application running on Kubernetes consists of many Kubernetes primitive components. These components describe what container image to use, how many replicas to run, if there's a public IP required to expose the application, etc. For more information, see the official [Kubernetes documentation][kubernetes-documentation]. If your source code repository doesn't already have the basic Kubernetes manifests to deploy, Automated Deployments can generate them for you. Otherwise, you can use a set of existing manifests. You can also choose an existing Helm chart.

If your code repository already has a Dockerfile, you can select it to be used to build the application image.

- Select
**Use existing Kubernetes manifest deployment files**for the deployment options. - Select the
**Kubernetes manifest file or folder**from your repository. - Select
**Next**.

## (Optional) Use a managed ingress and/or Service Connector

When generating Kubernetes manifests with Automated Deployments, you can optionally enable App Routing to set up an ingress controller for your application. You can also use Service Connector to create a new connection or seamlessly integrate your app with an existing Azure service backend.

App Routing provides a fully managed NGINX-based ingress controller out of the box, complete with built-in SSL/TLS encryption using certificates stored in Azure Key Vault and DNS zone management through Azure DNS. When using Automated Deployments, the expose ingress command integrates seamlessly with App Routing, making it easy to expose your application to external traffic under a secure, custom DNS name—with minimal configuration.

- Select the
**Expose ingress**box. - Choose between an
**Existing ingress controller**or a**New ingress controller**. - Choose between using a
**SSL/TLS enabled**or**Insecure**ingress controller. - (Optional) Enter
**Certificate details**if choosing a**SSL/TLS enabled**ingress controller. - Choose between using
**Azure DNS**or a**3rd party provider**. - Enter the
**Azure DNS Zone**and**Subdomain name**.

## (Optional) Add environment variables

Define environment variables for a container in Kubernetes by specifying name-value pairs. Environment variables are important as they help enable easier management of settings, secure handling of sensitive information, and flexibility across environments.

## Review configuration and deploy

Review the configuration for the application, and Kubernetes manifests, then select **Deploy**. A pull request (PR) will be generated against the repository that you selected, so don't navigate away from deployment page.

### Review and merge pull request

When the deployment succeeds, select **View pull request** to view the details of the generated pull request on your code repository.

- Review the changes under
**Files changed**and make any desired edits. - Select
**Merge pull request**to merge the changes into your code repository.

Merging the change runs the GitHub Actions workflow that builds your application into a container image, stores it in Azure Container Registry, and deploys it to the cluster.

### Check the deployed resources

After the pipeline is completed, you can review the created Kubernetes `Service`

in the Azure portal by selecting **Services and ingresses** under the **Kubernetes resources** section of the service menu.

Selecting the **External IP** should open up a new browser page with the running application.

## Delete resources

Once you're done with your cluster, use the following steps to delete it to avoid incurring Azure charges:

- In the Azure portal, navigate to
**Automated deployments** - Select
**...**on the pipeline of your choice. - Select
**Delete**.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-linux -->

# Use the Azure Linux container host for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Linux container host for AKS is an open-source Linux distribution created by Microsoft, and it's generally available as a container host on Azure Kubernetes Service (AKS). The Azure Linux container host provides reliability and consistency from cloud to edge across the AKS, AKS-HCI, and Arc products. You can deploy Azure Linux node pools in a new cluster, add Azure Linux node pools to your existing Ubuntu clusters, or migrate your Ubuntu nodes to Azure Linux nodes. To learn more about Azure Linux, see the [Azure Linux documentation](/en-us/azure/azure-linux/intro-azure-linux).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Why use Azure Linux

The Azure Linux container host on AKS uses a native AKS image that provides one place to do all Linux development. Every package is built from source and validated, ensuring your services run on proven components. Azure Linux is lightweight, only including the necessary set of packages needed to run container workloads. It provides a reduced attack surface and eliminates patching and maintenance of unnecessary packages. At the base layer, it has a Microsoft hardened kernel tuned for Azure. Learn more about the [key capabilities of Azure Linux](/en-us/azure/azure-linux/intro-azure-linux#azure-linux-container-host-key-benefits).

## How to use Azure Linux on AKS

To get started using the Azure Linux container host for AKS, see:

[Creating a cluster with Azure Linux](/en-us/azure/azure-linux/quickstart-azure-cli)[How to upgrade Azure Linux clusters](/en-us/azure/azure-linux/tutorial-azure-linux-upgrade)[Add an Azure Linux node pool to your existing cluster](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli)[Ubuntu to Azure Linux migration](/en-us/azure/azure-linux/tutorial-azure-linux-migration)[Azure Linux supported GPU SKUs](/en-us/azure/azure-linux/intro-azure-linux#azure-linux-container-host-supported-gpu-skus)

## Regional availability

The Azure Linux container host is available for use in the same regions as AKS.

## Next steps

To learn more about Azure Linux, see the [Azure Linux documentation](/en-us/azure/azure-linux/intro-azure-linux).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/start-stop-nodepools -->

# Start and stop an Azure Kubernetes Service (AKS) node pool

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might not need to continuously run your AKS workloads. For example, you might have a development cluster that has node pools running specific workloads. To optimize your compute costs, you can completely stop your node pools in your AKS cluster.

## Features and limitations

- You can't stop system pools.
- Spot node pools are supported.
- Stopped node pools can be upgraded.
- The cluster and node pool must be running.
- You can't stop node pools from clusters which use the
[Node Autoprovisioning (NAP)](node-autoprovision)feature.

Tip

You can use Azure Copilot to stop and start your node pools in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#start-and-stop-node-pools).

## Before you begin

This article assumes you have an existing AKS cluster. If you need an AKS cluster, create one using the [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

## Stop an AKS node pool

Stop a running AKS node pool using the

command.`az aks nodepool stop`

`az aks nodepool stop --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

Verify your node pool stopped using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

The following condensed example output shows the

`powerState`

as`Stopped`

:`{ [...] "osType": "Linux", "podSubnetId": null, "powerState": { "code": "Stopped" }, "provisioningState": "Succeeded", "proximityPlacementGroupId": null, [...] }`

Note

If the

`provisioningState`

shows`Stopping`

, your node pool is still in the process of stopping.Note

Stopping the node pool will stop its Cluster Autoscaler, and starts it back when starting the node pool. So if you manually modify the number of VMSS instances in the pool while it's stopped, Cluster Autoscaler might show inconsistencies.


## Start a stopped AKS node pool

Restart a stopped node pool using the

command.`az aks nodepool start`

`az aks nodepool start --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

Verify your node pool started using the

command.`az aks nodepool show`

`az aks nodepool show --resource-group myResourceGroup --cluster-name myAKSCluster --nodepool-name testnodepool`

The following condensed example output shows the

`powerState`

as`Running`

:`{ [...] "osType": "Linux", "podSubnetId": null, "powerState": { "code": "Running" }, "provisioningState": "Succeeded", "proximityPlacementGroupId": null, [...] }`

Note

If the

`provisioningState`

shows`Starting`

, your node pool is still in the process of starting.

## Next steps

- To learn how to scale
`User`

pools to 0, see[scale](scale-cluster#scale-user-node-pools-to-0).`User`

pools to 0 - To learn how to stop your cluster, see
[cluster start/stop](start-stop-cluster). - To learn how to save costs using Spot instances, see
[add a spot node pool to AKS](spot-node-pool). - To learn more about the AKS support policies, see
[AKS support policies](support-policies).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-azure-dedicated-hosts -->

# Add Azure Dedicated Host to an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Dedicated Host is a service that provides physical servers - able to host one or more virtual machines - dedicated to one Azure subscription. Dedicated hosts are the same physical servers used in our data centers, provided as a resource. You can provision dedicated hosts within a region, availability zone, and fault domain. Then, you can place VMs directly into your provisioned hosts, in whatever configuration best meets your needs.

Using Azure Dedicated Hosts for nodes with your AKS cluster has the following benefits:

- Hardware isolation at the physical server level. No other VMs will be placed on your hosts. Dedicated hosts are deployed in the same data centers and share the same network and underlying storage infrastructure as other, non-isolated hosts.
- Control over maintenance events initiated by the Azure platform. While most maintenance events have little to no impact on your virtual machines, there are some sensitive workloads where each second of pause can have an impact. With dedicated hosts, you can opt in to a maintenance window to reduce the impact to your service.

## Before you begin

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Before you start, ensure that your version of the Azure CLI is 2.39.0 or later. If it's an earlier version,
[install the latest version](/en-us/cli/azure/install-azure-cli).

## Limitations

The following limitations apply when you integrate Azure Dedicated Host with Azure Kubernetes Service:

- Accelerated Networking
- An existing agent pool can't be converted from non-ADH to ADH or ADH to non-ADH.
- It isn't supported to update agent pool from host group A to host group B.
- Using ADH across subscriptions.

## Planning for ADH Capacity on AKS

Not all host SKUs are available in all regions, and availability zones. You can list host availability, and any offer restrictions before you start provisioning dedicated hosts.

```
az vm list-skus --location eastus --resource-type hostGroups/hosts -o table
```


Note

First, when using host group, the nodepool fault domain count is always the same as the host group fault domain count. In order to use cluster auto-scaling to work with ADH and AKS, please make sure your host group fault domain count and capacity is enough. Secondly, only change fault domain count from the default of 1 to any other number if you know what they are doing as a misconfiguration could lead to a unscalable configuration.

[Determine how many hosts you would need based on the expected VM Utilization](/en-us/azure/virtual-machines/dedicated-host-general-purpose-skus).

Evaluate [host utilization](/en-us/azure/virtual-machines/dedicated-hosts-how-to#check-the-status-of-the-host) to determine the number of allocatable VMs by size before you deploy.

```
az vm host get-instance-view --resource-group myDHResourceGroup --host-group MyHostGroup --name MyHost
```


## Add a Dedicated Host Group to an AKS cluster

A host group is a resource that represents a collection of dedicated hosts. You create a host group in a region and an availability zone, and add hosts to it. When planning for high availability, there are more options. You can use one or both of the following options with your dedicated hosts:

- Span across multiple availability zones. In this case, you're required to have a host group in each of the zones you wish to use.
- Span across multiple fault domains, which are mapped to physical racks.

In either case, you need to provide the fault domain count for your host group. If you don't want to span fault domains in your group, use a fault domain count of 1.

You can also decide to use both availability zones and fault domains.

## Create a Host Group

Now create a dedicated host in the host group. In addition to a name for the host, you're required to provide the SKU for the host. Host SKU captures the supported VM series and the hardware generation for your dedicated host.

For more information about the host SKUs and pricing, see [Azure Dedicated Host pricing](https://azure.microsoft.com/pricing/details/virtual-machines/dedicated-host/).

Use az vm host create to create a host. If you set a fault domain count for your host group, you'll be asked to specify the fault domain for your host.

In this example, we'll use [az vm host group create](/en-us/cli/azure/vm/host/group#az-vm-host-group-create) to create a host group using both availability zones and fault domains.

```
az vm host group create \
--name myHostGroup \
--resource-group myDHResourceGroup \
--zone 1 \
--platform-fault-domain-count 1 \
--automatic-placement true
```


## Create a Dedicated Host

Now create a dedicated host in the host group. In addition to a name for the host, you're required to provide the SKU for the host. Host SKU captures the supported VM series and the hardware generation for your dedicated host.

If you set a fault domain count for your host group, you'll need to specify the fault domain for your host.

```
az vm host create \
--host-group myHostGroup \
--name myHost \
--sku DSv3-Type1 \
--platform-fault-domain 1 \
--resource-group myDHResourceGroup
```


## Use a user-assigned Identity

Important

A user-assigned Identity with "contributor" role on the Resource Group of the Host Group is required.

First, create a Managed Identity

```
az identity create --resource-group <Resource Group> --name <Managed Identity name>
```


Assign Managed Identity

```
az role assignment create --assignee <id> --role "Contributor" --scope <Resource id>
```


## Create an AKS cluster using the Host Group

Create an AKS cluster, and add the Host Group you just configured.

```
az aks create \
--resource-group MyResourceGroup \
--name MyManagedCluster \
--location eastus \
--nodepool-name agentpool1 \
--node-count 1 \
--host-group-id <id> \
--node-vm-size Standard_D2s_v3 \
--assign-identity <id> \
--generate-ssh-keys
```


## Add a Dedicated Host Node Pool to an existing AKS cluster

Add a Host Group to an already existing AKS cluster.

```
az aks nodepool add --cluster-name MyManagedCluster --name agentpool3 --resource-group MyResourceGroup --node-count 1 --host-group-id <id> --node-vm-size Standard_D2s_v3
```


## Remove a Dedicated Host Node Pool from an AKS cluster

```
az aks nodepool delete --cluster-name MyManagedCluster --name agentpool3 --resource-group MyResourceGroup
```


## Next steps

In this article, you learned how to create an AKS cluster with a Dedicated host, and to add a dedicated host to an existing cluster. For more information about Dedicated Hosts, see [dedicated-hosts](/en-us/azure/virtual-machines/dedicated-hosts).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-communication-manager -->

# Set up the Azure Kubernetes Service communication manager

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Azure Kubernetes Service (AKS) communication manager streamlines notifications for all your AKS maintenance tasks by using Azure Resource Notifications and Azure Resource Graph frameworks. The communication manager gives you timely alerts on event triggers and outcomes, so that you can closely monitor your upgrades.

If maintenance fails, the communication manager notifies you with the reasons for the failure. This information reduces operational hassles related to observability and follow-ups.

By following the steps in this article, you can set up notifications for all types of automatic upgrades that use maintenance windows.

## Prerequisites

Configure your cluster for either the

[automatic upgrade channel](auto-upgrade-cluster)or the[automatic upgrade channel for nodes](auto-upgrade-node-os-image).Create a

[planned maintenance window](planned-maintenance)for your configuration of automatic upgrades.

## Set up the communication manager

In the Azure portal, go to the resource.

Select

**Monitoring**>**Alerts**>**Alert Rules**, and then select**Create**.On the

**Condition**tab, for**Signal name**, select**Custom log search**.In the

**Search query**box, paste one of the following custom queries. Be sure to update the`where id contains`

path to reference your resources for subscription ID, resource group name, and cluster name.The following query is for notifications of automatic upgrades for clusters:

`arg("").containerserviceeventresources | where type == "microsoft.containerservice/managedclusters/scheduledevents" | where id contains "/subscriptions/<subid>/resourcegroups/<rgname>/providers/Microsoft.ContainerService/managedClusters/<clustername>" | where properties has "eventStatus" | extend status = substring(properties, indexof(properties, "eventStatus") + strlen("eventStatus") + 3, 50) | extend status = substring(status, 0, indexof(status, ",") - 1) | where status != "" | where properties has "eventDetails" | extend upgradeType = case( properties has "K8sVersionUpgrade", "K8sVersionUpgrade", properties has "NodeOSUpgrade", "NodeOSUpgrade", "" ) | extend details = parse_json(tostring(properties.eventDetails)) | where properties has "lastUpdateTime" | extend eventTime = substring(properties, indexof(properties, "lastUpdateTime") + strlen("lastUpdateTime") + 3, 50) | extend eventTime = substring(eventTime, 0, indexof(eventTime, ",") - 1) | extend eventTime = todatetime(tostring(eventTime)) | where eventTime >= ago(30m) // Ensure this matches aggregation granularity & frequency | where upgradeType == "K8sVersionUpgrade" | project eventTime, upgradeType, status, properties, name, details | order by eventTime asc`

The following query is for notifications of automatic upgrades for NodeOS:

`arg("").containerserviceeventresources | where type == "microsoft.containerservice/managedclusters/scheduledevents" | where id contains "/subscriptions/<subid>/resourcegroups/<rgname>/providers/Microsoft.ContainerService/managedClusters/<clustername>" | where properties has "eventStatus" | extend status = substring(properties, indexof(properties, "eventStatus") + strlen("eventStatus") + 3, 50) | extend status = substring(status, 0, indexof(status, ",") - 1) | where status != "" | where properties has "eventDetails" | extend upgradeType = case( properties has "K8sVersionUpgrade", "K8sVersionUpgrade", properties has "NodeOSUpgrade", "NodeOSUpgrade", "" ) | extend details = parse_json(tostring(properties.eventDetails)) | where properties has "lastUpdateTime" | extend eventTime = substring(properties, indexof(properties, "lastUpdateTime") + strlen("lastUpdateTime") + 3, 50) | extend eventTime = substring(eventTime, 0, indexof(eventTime, ",") - 1) | extend eventTime = todatetime(tostring(eventTime)) | where eventTime >= ago(30m) // Ensure this matches aggregation granularity & frequency | where upgradeType == "NodeOSUpgrade" | project eventTime, upgradeType, status, properties, name, details | order by eventTime asc`

Go to the

**Condition**tab. Configure the alert conditions with the following settings:**Measure**: Select**Table rows**.**Aggregation type**: Select**Count**.**Aggregation granularity**: Select**30 minutes**.**Threshold value**: Keep at**0**.**Split by dimensions**: For**Dimension name**, select**status**. Then select the**Include all future values**checkbox.

In the

**Split by dimensions**area, for**Dimension values**, select a value. Because you selected**status**for the dimension name, the available values are**Scheduled**,**Started**,**Completed**,**Canceled**, and**Failed**.Note

These status values appear only if your cluster previously executed automatic upgrade operations. For new clusters or for clusters that haven't undergone automatic upgrades yet, the dropdown list might appear empty or show no available dimensions. After your cluster performs its first automatic upgrade, these status values become available for selection.

Go to the

**Actions**tab. Make sure that an action group with the correct email address exists, so that you can receive the notifications:Select

**Use action groups**>**Create an action group**.For

**Notification type**, select**Email/SMS_message/Push/Voice**.Select the

**Email**checkbox, and then enter the email address in the**Email**box.

Go to the

**Details**tab. Assign a managed identity so that you can grant access to the necessary resources. In the**Identity**area, select**System assigned managed identity**.Go to the

**Review + create**tab, and then select**Create**.Now that you've created the alert rule, you can assign the appropriate roles for the managed identity:

- In the alert rule, go to
**Settings**>**Identity**>**System assigned managed identity**>**Azure role assignments**. - Select
**Add role assignment**, select the**Reader**role, and assign it to the resource group. - Select
**Add role assignment**again, select the**Reader**role, and assign it to the subscription.

Tip

If you don't see the

**Identity**option, make sure that you created your alert rule and that you have the necessary permissions.- In the alert rule, go to

After you set up the communication manager, it sends advance notices one week before maintenance starts and one day before maintenance starts. It also sends you timely alerts during the maintenance operation.

## Verify the configuration

To upgrade the cluster, wait for the automatic upgrader to start. Then verify that you promptly receive notices on the email address that you configured to receive notices.

Check the Azure Resource Graph database for the scheduled notification record. Each scheduled event notification should be listed as one record in the `ContainerServiceEventResources`

table.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/considerations-pod-sandboxing -->

# Pod Sandboxing considerations

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

For Pod Sandboxing deployments on Azure Kubernetes Service (AKS) there are several items to consider in regard to resource management, memory management, CPU management, and security.

## Resource management

Memory and CPU management behavior with Pod Sandboxing might be unfamiliar to some users. These considerations are relevant when specifying resources in a deployment, especially for larger and resource sensitive workloads.

### Kata components

In a Kata deployment, there are generally two families of components that get deployed. You have **host components** and **guest components**.

- The main
**host components**comprise of the*Kata shim*,*Cloud Hypervisor*, and*virtiofsd*.- The
*Kata shim*manages a pod VM lifecycle. *Cloud Hypervisor*is the Virtual Machine Monitor (VMM) used by the Kata shim.*virtiofsd*is a daemon used to share files between each Pod VM and its container host.

- The
- The main
**guest components**include the*user's workloads*,*pod VM kernel*, and the*Kata agent*.- The
*Kata agent*manages containers inside of the Pod VMs

- The

### Memory management

With Kata pods, you have the ability to specify the amount of memory of the Pod VM that hosts your workloads. It's crucial that you configure the values accordingly so that a pod has sufficient resources, but doesn't result in unused memory being allocated to the pod.

### Pod VM memory size

There's an amount of memory allocated to each pod VM that runs a container. This VM memory size is inclusive of all the memory necessary to run Kata guest components. Users should take care to ensure that they buffer some extra memory beyond the expected consumption of their workloads to account for the consumption of other guest components, such as the kata agent or VM kernel. Examples are given on typical memory values later on in this article.

The pod VM memory size is equivalent to the [Kubernetes pod memory limit](https://kubernetes.io/docs/tasks/configure-pod-container/assign-memory-resource/#specify-a-memory-request-and-a-memory-limit) the user specifies. A user can change the value by changing their pod memory limit; if no values are specified, a default size of 512Mi is applied. Once the pod starts, this size becomes fixed.

As the pod VM memory size increases, the runtime class memory overhead should be expected to increase alongside it.

### Runtime class memory overhead

Pod Sandboxing workloads come with a default kata runtime class (`kata-vm-isolation`

) which comes with default overheads for resources. Users that want finer grain control of their resource quotas can [set up a custom runtime class](https://kubernetes.io/docs/concepts/containers/runtime-class/#setup) with specific resource overheads. When doing so, users should ensure that the memory overhead value of the runtime class is enough that covers all expected usage for the **host components** of a kata deployment. The runtime class memory overhead does *not* need to account for the expected memory consumption of the **guest components**.

You can create a specialized runtime and specify the memory overhead in your runtime class through the `overhead`

field in your `RuntimeClass`

manifest. [As an example](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/#usage-example), let's assume I want to create a runtime for workloads I expect to be smaller in consumption:

```
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
name: small-kata-pods
handler: kata
overhead:
podFixed:
memory: "120Mi"
```


Specifying overheads isn't required, and suggested if you want finer control over the resources being set aside for your workloads. If you use the default `kata-vm-isolation`

runtime class and don't specify any overheads in your YAML, the overhead of the Pod VM size defaults to 512Mi and the runtime class overhead defaults to 600Mi. This default runtime overhead is calculated with the default pod VM size (512Mi) plus to approximate memory needed by host components for such a VM size (~88Mi).

### User workloads

When a user deploys a Kata workload, they're able to use memory up to the configured *pod VM memory size* minus the other guest components, such as the Kata agent or the guest VM kernel.

If you would like to get an approximation of the memory used by these components:

- Connect to the pod VM (either via
`kubectl exec`

or`kubectl debug`

to open a shell inside your pod). - Run the
`free`

command. - Inspect the "used" column in the output to get an idea of the memory consumed by the guest kernel/kata agent.

### Memory cgroups

When a Kata pod is scheduled to run, kubelet assigns the pod to a memory `cgroup`

. This `cgroup`

enforces the pod's memory limits/requests, allowing a user to define the resource quotas available to a pod.

Within the memory `cgroup`

, there are two important fields to consider:

`memory.current`

defines how many bytes of memory the host components and the pod VM memory size allocates.`memory.max`

optional, user defined upper limit of memory.current for pods where users want to impose a memory limit.- The kubelet computes this value as the sum of a pod's memory limit and its runtime class memory overhead.


At any point, if the `memory.current`

value exceeds that of `memory.max`

, [the kernel might trigger an OOMKill on the pod if memory pressure is detected](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/#requests-and-limits).

### Reference usage values

Users can utilize these values to serve as a reference for the typical memory usage and values across the different variables covered. Pod VM memory sizes under 128Mi aren't supported.

| Pod VM Memory Size | Runtime class overhead | memory.current | memory.max | Free memory available to Host components |
|---|---|---|---|---|
| 128Mi | 16Mi | 133Mi | 144Mi | 11Mi |
| 256Mi | 32Mi | 263Mi | 288Mi | 25Mi |
| 1Gi | 128Mi | 1034Mi | 1152Mi | 118Mi |
| 2Gi | 256Mi | 2063Mi | 2304Mi | 241Mi |
| 4Gi | 374Mi | 4122Mi | 4470Mi | 348Mi |
| 8Gi | 512Mi | 8232Mi | 8704Mi | 472Mi |
| 32Gi | 640Mi | 32918Mi | 33408Mi | 490Mi |
| 64Gi | 768Mi | 65825Mi | 66304Mi | 479Mi |
| 96Gi | 896Mi | 98738Mi | 99200Mi | 462Mi |
| 128Gi | 1Gi | 131646Mi | 132096Mi | 450Mi |

## CPU management

In a similar vein to memory, you can also allocate CPU resources to your Kata workloads. Doing so is recommended; without declaring a CPU limit for your Kata pod, Kata host components are able to use any CPU capacity available on the node.

### Reserving CPU

When reserving CPUs for your Kata workloads, you have two fields you can choose to set.

- The
*runtime class CPU overhead* - The
*pod CPU limit*

When at least one of the two values is specified, the control plane reserves the specified number of CPUs on the node for your workload. Other pods on the same node can't access this reserved capacity.

### Pod CPU limit

You can declare your [pod CPU limit](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/) in your application's manifest. A specified pod CPU limit defines the limit of the CPUs that containers in the associated pod VM can use.

If you specify fractions of CPUs for the pod CPU limit, those fractions will get rounded up to the next integer. The rounded up number becomes the number of vCPUs allocated to the Pod VM, but a `cgroup`

will limit the workload to only consume the fraction specified in the pod CPU limit.

If no number is declared, one vCPU will be allocated to the pod VM if the capacity is available on the node. There's no limit on the CPU consumption of the Kata host components.

### Runtime class CPU overhead

The runtime class overhead should be specified if you'd like to preemptively reserve some node capacity for the Kata host components.

You can specify the memory overhead in your runtime class through the `overhead`

field in your `RunTimeClass`

manifest. [As an example](https://kubernetes.io/docs/concepts/scheduling-eviction/pod-overhead/#usage-example):

```
apiVersion: node.k8s.io/v1
kind: RuntimeClass
metadata:
name: custom-kata-runtime
handler: kata
overhead:
podFixed:
cpu: "250m"
```


### Best practices

#### Memory management

- Ensure you specify pod VM memory sizes (defined by the
`limits.memory`

in your manifest) and suitable resource quotas for all your deployments.- Ensure you use a nonzero
*pod request*if you want to ensure that some node capacity is reserved for the pod VM before that VM starts up. The request should account for the pod VM and containers that are expected to run on it. - Ensure you use a nonzero
*runtime class overhead*if you want to reserve some node capacity for the Kata host components before those components start up.

- Ensure you use a nonzero
- If you expect your pod workloads to be especially resource hungry, you can specify limits accordingly for the pod VM to ensure that there are ample resources available for your workloads.
- Declare a suitable runtime class memory overhead such that it gives enough memory for your host components but doesn't take too much to avoid allocating unused memory.

#### CPU management

If your node typically has plenty of free CPU capacity, these reservations might be unnecessary.

If your nodes typically run to the limit with CPU consumption, then a nonzero reservation ensures your pods can be executed more reliably.

- You can utilize pod CPU requests to ensure that some CPU node capacity is reserved for the Kata host components. Reserved capacity for a specific workload is
*not*available to other workloads on the node.

- You can utilize pod CPU requests to ensure that some CPU node capacity is reserved for the Kata host components. Reserved capacity for a specific workload is
Make sure you specify CPU requests that your infrastructure can accommodate. If your available capacity runs near 0, or your request is too large, your workloads might

[fail to start](https://kubernetes.io/docs/tasks/configure-pod-container/assign-cpu-resource/#specify-a-cpu-request-that-is-too-big-for-your-nodes)Align your CPU requests with your CPU limits. The Kata shim doesn't have visibility into requests. Therefore, if no CPU limit is declared, the pod VM is limited to one vCPU. The Kata host components, which do have visibility into request values, consumes the rest of the requested CPU count and have no limit to CPU consumption.

Reserved capacity for a specific workload is

*not*available to other workloads on the node.

### Example declarations

| Runtime class CPU overhead | Pod CPU Request/Limit | Expected behavior |
|---|---|---|
| 1 | 1 | The control plane reserves two CPUs on the node. The pod VM gets one CPU, and containers on the pod can use up to the one vCPU capacity. The Kata host components and pod VM together can use up to two CPUs from the reserved capacity on the node. |
| 1 | 2.5 | The control plane reserves 3.5 CPUs on the node. The pod VM gets three vCPUs, but containers on the pod VM can use up to 2.5 vCPU capacity. The Kata host components and pod VM together can use up to 3.5 CPUs from the reserved capacity on the node. |
| None | 1 | The control plane reserves one CPU on the node. The pod VM gets one vCPU, and containers on the pod VM can use up to one vCPU capacity. The Kata host components and the pod VM together are allowed to use up to one CPU from the reserved capacity on the node. One CPU is always available to the pod VM due to the CPU request. |
| 1 | None | The control plane reserves one CPU on the node. The pod VM gets one vCPU, and containers on the pod VM can use up to one vCPU capacity. The kata host components and the pod VM can use any CPU capacity available on the node. At least one CPU is always available due to the overhead reservation. |

## Security

Pod Sandboxing offers users a compelling option to isolate their workloads from other workloads and the host. There are, nonetheless, important security concerns that should be taken into account.

### Privileged pods

There are scenarios in which privileged pods might be required. Users are able to spin up privileged pods, but no [host devices are attached to the pod](https://github.com/kata-containers/kata-containers/blob/main/docs/how-to/privileged.md#containerd).

Using privileged containers lead to root access in the guest VM, but remain isolated from the host.

Privileged pods, even on Pod Sandboxing, should only be used when necessary. Privileged pods should continue to be [managed by trusted users](https://kubernetes.io/docs/concepts/security/pod-security-standards/#privileged).

### Host path storage volumes

`hostPath`

volumes can be mounted into Kata pods. In Pod Sandboxing, using `hostPath`

volumes can potentially undermine the isolation that Kata provides; since part of the host filesystem is exposed directly to the container, a potential attack vector is opened. The warnings posed by [upstream](https://kubernetes.io/docs/concepts/storage/volumes/#hostpath) should be considered as relevant for Pod Sandboxing as well.

There are some exceptions; files under `/dev`

are mounted into the container from the guest system instead of the host system. This helps maintain pod isolation for situations where this path must be mounted to function.

Warning

Unless necessary, the recommendation is to *avoid* using hostPath storage volumes.

#### Blocking hostPath via Azure Policy

[Azure Policy](/en-us/azure/governance/policy/concepts/policy-for-kubernetes) allows users to apply at-scale enforcements and safeguards on their cluster components in a centralized, consistent manner.

There is a set of [built-in policy sets](policy-reference) for AKS that enforce best practices. Users can take advantage of one of these policies to block deployments that attempt to mount hostPaths.

## Next steps

Once you're ready, learn how to [deploy pod sandboxing on AKS](use-pod-sandboxing).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/enable-fips-nodes -->

# Enable Federal Information Process Standard (FIPS) for Azure Kubernetes Service (AKS) node pools

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The Federal Information Processing Standard (FIPS) 140-2 is a US government standard that defines minimum security requirements for cryptographic modules in information technology products and systems. Azure Kubernetes Service (AKS) allows you to create Linux and Windows node pools with FIPS 140-2 enabled. Deployments running on FIPS-enabled node pools can use those cryptographic modules to provide increased security and help meet security controls as part of FedRAMP compliance. For more information on FIPS 140-2, see [Federal Information Processing Standard (FIPS) 140](/en-us/azure/compliance/offerings/offering-fips-140-2).

Important

Starting on **March 17, 2027**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Ubuntu 20.04. Any existing node images will be deleted, and you'll be unable to scale any node pools running Ubuntu 20.04. Migrate to a supported Ubuntu version by [upgrading your node pools](upgrade-aks-cluster) to Kubernetes version 1.35+. For more information on this retirement, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4874) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=485795). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Prerequisites

Azure CLI version 2.32.0 or later installed and configured. To find the version, run `az --version`

. For more information about installing or upgrading the Azure CLI, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

Note

AKS Monitoring Addon supports FIPS enabled node pools with Ubuntu, Azure Linux, and Windows starting with Agent version 3.1.17 (Linux) and Win-3.1.17 (Windows).

## Limitations

- FIPS-enabled node pools have the following limitations:
- FIPS-enabled node pools require Kubernetes version 1.19 and greater.
- To update the underlying packages or modules used for FIPS, you must use
[Node Image Upgrade](node-image-upgrade). - Container images on the FIPS nodes aren't assessed for FIPS compliance.
- Mounting of a CIFS share fails because FIPS disables some authentication modules. To work around this issue, see
[Errors when mounting a file share on a FIPS-enabled node pool](/en-us/troubleshoot/azure/azure-kubernetes/fail-to-mount-azure-file-share#fipsnodepool). - FIPS-enabled node pools with
[Arm64 VMs](use-arm64-vms)are only supported with Azure Linux 3.0+. - FIPS isn't supported with
[Flatcar Container Linux for AKS (preview)](flatcar-container-linux-for-aks).


Important

The FIPS-enabled Linux image is a different image than the default Linux image used for Linux-based node pools.

FIPS-enabled node images can have different version numbers, such as kernel version, than images that aren't FIPS-enabled. The update cycle for FIPS-enabled node pools and node images can differ from node pools and images that aren't FIPS-enabled.

## Supported OS Versions

You can create FIPS-enabled node pools on all supported OS types (Linux and Windows). However, not all OS versions support FIPS-enabled node pools. After a new OS version is released, there's typically a waiting period before it's FIPS compliant.

This table includes the supported OS versions:

| OS Type | OS SKU | FIPS Compliance |
|---|---|---|
| Linux | Ubuntu | Supported |
| Linux | Azure Linux | Supported |
| Windows | Windows Server 2019 | Supported |
| Windows | Windows Server 2022 | Supported |

When requesting FIPS enabled Ubuntu, if the default Ubuntu version doesn't support FIPS, AKS defaults to the most recent FIPS-supported version of Ubuntu. For example, Ubuntu 22.04 is default for Linux node pools. Since 22.04 doesn't currently support FIPS, AKS defaults to Ubuntu 20.04 for Linux FIPS-enabled node pools.

Note

Previously, you could use the GetOSOptions API to determine whether a given OS supported FIPS. The GetOSOptions API is now deprecated and it will no longer be included in new AKS API versions starting with 2024-05-01.

## Create a FIPS-enabled Linux node pool

Create a FIPS-enabled Linux node pool using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command with the`--enable-fips-image`

parameter.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name fipsnp \ --enable-fips-image`

Note

You can also use the

`--enable-fips-image`

parameter with the[az aks create](/en-us/cli/azure/aks#az-aks-create)command when creating a cluster to enable FIPS on the default node pool. When adding node pools to a cluster created in this way, you still must use the`--enable-fips-image`

parameter when adding node pools to create a FIPS-enabled node pool.Verify your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows the

*fipsnp*node pool is FIPS-enabled:`Name enableFips --------- ------------ fipsnp True nodepool1 False`

List the nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

The following example output shows a list of the nodes in the cluster. The nodes starting with

`aks-fipsnp`

are part of the FIPS-enabled node pool.`NAME STATUS ROLES AGE VERSION aks-fipsnp-12345678-vmss000000 Ready agent 6m4s v1.19.9 aks-fipsnp-12345678-vmss000001 Ready agent 5m21s v1.19.9 aks-fipsnp-12345678-vmss000002 Ready agent 6m8s v1.19.9 aks-nodepool1-12345678-vmss000000 Ready agent 34m v1.19.9`

Run a deployment with an interactive session on one of the nodes in the FIPS-enabled node pool using the

`kubectl debug`

command.`kubectl debug node/aks-fipsnp-12345678-vmss000000 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

From the interactive session output, verify the FIPS cryptographic libraries are enabled. Your output should look similar to the following example output:

`root@aks-fipsnp-12345678-vmss000000:/# cat /proc/sys/crypto/fips_enabled 1`

FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Create a FIPS-enabled Windows node pool

Create a FIPS-enabled Windows node pool using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command with the`--enable-fips-image`

parameter. Unlike Linux-based node pools, Windows node pools share the same image set.`az aks nodepool add \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name fipsnp \ --enable-fips-image \ --os-type Windows`

Verify your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

Verify Windows node pools have access to the FIPS cryptographic libraries by

[creating an RDP connection to a Windows node](rdp)in a FIPS-enabled node pool and check the registry. From the**Run**application, enter`regedit`

.Look for

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\Lsa\FIPSAlgorithmPolicy`

in the registry.If

`Enabled`

is set to*1*, then FIPS is enabled.FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Update an existing node pool to enable or disable FIPS

Existing Linux node pools can be updated to enable or disable FIPS. If you're planning to migrate your node pools from non-FIPS to FIPS, first validate that your application is working properly in a test environment before migrating it to a production environment. Validating your application in a test environment should prevent issues caused by the FIPS kernel blocking some weak cipher or encryption algorithm, such as an MD4 algorithm that isn't FIPS compliant.

Note

When updating an existing Linux node pool to enable or disable FIPS, the node pool update moves between the fips and non-fips image. This node pool update triggers a reimage to complete the update. This can cause the node pool update to take a few minutes to complete.

### Prerequisites

Azure CLI version 2.64.0 or later. To find the version, run `az --version`

. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

### Enable FIPS on an existing node pool

Existing Linux node pools can be updated to enable FIPS. When you update an existing node pool, the node image changes from the current image to the recommended FIPS image of the same OS SKU.

Update a node pool using the

[az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)command with the`--enable-fips-image`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --enable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

Verify that your node pool is FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows that the

*np*node pool is FIPS-enabled:`Name enableFips --------- ------------ np True nodepool1 False`

List the nodes using the

`kubectl get nodes`

command.`kubectl get nodes`

The following example output shows a list of the nodes in the cluster. The nodes starting with

`aks-np`

are part of the FIPS-enabled node pool.`NAME STATUS ROLES AGE VERSION aks-np-12345678-vmss000000 Ready agent 6m4s v1.19.9 aks-np-12345678-vmss000001 Ready agent 5m21s v1.19.9 aks-np-12345678-vmss000002 Ready agent 6m8s v1.19.9 aks-nodepool1-12345678-vmss000000 Ready agent 34m v1.19.9`

Run a deployment with an interactive session on one of the nodes in the FIPS-enabled node pool using the

`kubectl debug`

command.`kubectl debug node/aks-np-12345678-vmss000000 -it --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

From the interactive session output, verify the FIPS cryptographic libraries are enabled. Your output should look similar to the following example output:

`root@aks-np-12345678-vmss000000:/# cat /proc/sys/crypto/fips_enabled 1`

FIPS-enabled node pools also have a

*kubernetes.azure.com/fips_enabled=true*label, which deployments can use to target those node pools.

## Disable FIPS on an existing node pool

Existing Linux node pools can be updated to disable FIPS. When updating an existing node pool, the node image changes from the current FIPS image to the recommended non-FIPS image of the same OS SKU. The node image change will occur after a reimage.

Update a Linux node pool using the

[az aks nodepool update](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-update)command with the`--disable-fips-image`

parameter.`az aks nodepool update \ --resource-group myResourceGroup \ --cluster-name myAKSCluster \ --name np \ --disable-fips-image`

This command triggers a reimage of the node pool immediately to deploy the FIPS compliant Operating System. This reimage occurs during the node pool update. No extra steps are required.

Verify that your node pool isn't FIPS-enabled using the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the*enableFIPS*value in*agentPoolProfiles*.`az aks show \ --resource-group myResourceGroup \ --name myAKSCluster \ --query="agentPoolProfiles[].{Name:name enableFips:enableFips}" \ -o table`

The following example output shows that the

*np*node pool isn't FIPS-enabled:`Name enableFips --------- ------------ np False nodepool1 False`


## Message of the Day

Pass the `--message-of-the-day`

flag with the location of the file to replace the Message of the Day on Linux nodes at cluster creation or node pool creation.

Create a cluster with message of the day using the [az aks create](/en-us/cli/azure/aks#az-aks-create) command.

```
az aks create --cluster-name myAKSCluster --resource-group myResourceGroup --message-of-the-day ./newMOTD.txt
```


Add a node pool with message of the day using the [az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add) command.

```
az aks nodepool add --name mynodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --message-of-the-day ./newMOTD.txt
```


## Next steps

To learn more about AKS security, see [Best practices for cluster security and upgrades in Azure Kubernetes Service (AKS)](operator-best-practices-cluster-security).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/control-plane-metrics-monitor -->

# Monitor Azure Kubernetes Service control plane metrics (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to monitor the Azure Kubernetes Service (AKS) control plane by using control plane metrics in Azure Monitor.

AKS supports a subset of control plane metrics free through [Azure Monitor platform metrics](monitor-aks#aks-monitoring-data-metrics-logs-integrations). The control plane metrics feature gives you visibility into the availability and performance of critical control plane components like the API server, etcd, the scheduler, the autoscaler, and the controller manager in AKS. The feature is also fully compatible with the managed service for Prometheus and Azure Managed Grafana. You can use these metrics to maximize overall observability and to maintain operational excellence for your AKS cluster.

## Control plane platform metrics

AKS offers some free control plane metrics for monitoring the API server and etcd. These metrics are automatically collected for all AKS clusters at no cost. You can analyze the metrics by using the [metrics explorer](/en-us/azure/azure-monitor/essentials/analyze-metrics) in the Azure portal. You can also create metrics-based alerts by using the metrics data.

To see the full list of supported control plane platform metrics, see the [AKS monitoring reference](monitor-aks-reference#metrics).

## Prerequisites and limitations

- The control plane metrics (preview) feature supports only the
[managed service for Prometheus](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview)in Azure Monitor. [Azure Private Link](/en-us/azure/azure-monitor/logs/private-link-security)isn't supported.- You can customize only the default
configmap file. No other customization is supported.`ama-metrics-settings-configmap.yaml`

- Your AKS cluster must use
[managed identity authentication](use-managed-identity).

### Install the aks-preview extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install or update the

`aks-preview`

Azure CLI extension by using theor`az extension add`

command:`az extension update`

`# Install the aks-preview extension az extension add --name aks-preview # Update the aks-preview extension az extension update --name aks-preview`


### Register the AzureMonitorMetricsControlPlanePreview feature flag

Register the

`AzureMonitorMetricsControlPlanePreview`

feature flag by using thecommand:`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`

It takes a few minutes for the status to show as

**Registered**.Verify the registration status by using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`

When the status is

**Registered**, refresh the registration of the Microsoft.ContainerService resource provider by using thecommand:`az provider register`

`az provider register --namespace "Microsoft.ContainerService"`


## Enable control plane metrics on an AKS cluster

Enable control plane metrics by using the managed service for Prometheus add-on when you create a new cluster or update an existing cluster.

Note

Unlike the metrics that are collected from cluster nodes, control plane metrics are collected by a component that isn't part of the `ama-metrics`

add-on. Enabling the `AzureMonitorMetricsControlPlanePreview`

feature flag and the managed service for Prometheus add-on ensures that control plane metrics are collected. After you enable metrics collection, it can take several minutes for the data to appear in the workspace.

### New AKS cluster

To learn how to collect managed service for Prometheus metrics from your AKS cluster, see [Enable Prometheus and Grafana for AKS clusters](/en-us/azure/azure-monitor/containers/kubernetes-monitoring-enable#enable-prometheus-and-grafana). For an AKS cluster, complete the steps described on the **CLI** tab.

### Existing AKS cluster

If your cluster already has the managed service for Prometheus add-on, update the cluster to ensure that it collects control plane metrics by using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command:

```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Query control plane metrics

Control plane metrics are stored in an Azure Monitor workspace in the cluster's region. You can query the metrics directly in the workspace or by using the Azure Managed Grafana instance that's connected to the workspace.

In the

[Azure portal](https://portal.azure.com), go to your AKS cluster resource.On the left menu, select

**Monitor**>**Monitor Settings**.Go to the Azure Monitor workspace that is linked to the cluster.

In the Azure Monitor workspace, under

**Managed Prometheus**, query the metrics by using the Prometheus explorer.

Note

AKS provides dashboard templates to help you view and analyze your control plane telemetry data in real time. If you use Azure Managed Grafana to visualize the data, you can import the following dashboards:

## Customize control plane metrics

AKS includes a preconfigured set of metrics to collect and store for each component. Metrics for the API server and etcd are collected by default. You can customize the list of metrics that are collected by modifying the [ ama-metrics-settings-configmap.yaml](https://github.com/Azure/prometheus-collector/blob/main/otelcollector/configmaps/ama-metrics-settings-configmap.yaml) configmap file.

Default targets include the following values:

```
controlplane-apiserver = true
controlplane-cluster-autoscaler = false
controlplace-node-auto-provisioning = false
controlplane-kube-scheduler = false
controlplane-kube-controller-manager = false
controlplane-etcd = true
```


All configmap files should be applied to the `kube-system`

namespace for any cluster.

### Customize an ingestion profile

You can customize an ingestion file for collected metrics. For more information, see [Minimal ingestion profile for control plane metrics in managed service for Prometheus](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-configuration-minimal#minimal-ingestion-for-default-on-targets).

#### Ingest only minimal metrics from default targets

- Set
`default-targets-metrics-keep-list.minimalIngestionProfile`

to`true`

, so it ingests only the minimal set of metrics for each of the default targets:`controlplane-apiserver`

and`controlplane-etcd`

.

#### Ingest all metrics from all targets

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`false`

.Under

`default-scrape-settings-enabled`

, verify that the targets you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplace-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Apply the configmap file by using the

command:`kubectl apply`

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

#### Ingest more than minimal metrics

Using the `minimalingestionprofile`

setting helps reduce the ingestion volume of metrics. If set to `true`

, only default recording rules, default alerts, and metrics that appear in the default dashboards are collected.

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`true`

.Under

`default-scrape-settings-enabled`

, verify that the targets you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Under

`default-targets-metrics-keep-list`

, specify the list of metrics for the`true`

targets.For example:

`controlplane-apiserver= "apiserver_admission_webhook_admission_duration_seconds|apiserver_longrunning_requests"`

Apply the configmap file by using the

command:`kubectl apply`

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

#### Ingest specific metrics from specific targets

Download the

configmap file.`ama-metrics-settings-configmap.yaml`

Rename the configmap file

`configmap-controlplane.yaml`

.Set

`minimalingestionprofile`

to`false`

.Under

`default-scrape-settings-enabled`

, verify that the targets that you want to scrape are set to`true`

.The targets you can set are:

`controlplane-apiserver`

`controlplane-cluster-autoscaler`

`controlplane-node-auto-provisioning`

`controlplane-kube-scheduler`

`controlplane-kube-controller-manager`

`controlplane-etcd`


Under

`default-targets-metrics-keep-list`

, specify the list of metrics for the`true`

targets.For example:

`controlplane-apiserver= "apiserver_admission_webhook_admission_duration_seconds|apiserver_longrunning_requests"`

Apply the configmap file:

`kubectl apply -f configmap-controlplane.yaml`


After you apply the configuration, it takes several minutes for the metrics from the specified targets that are scraped from the control plane to appear in the Azure Monitor workspace.

## Troubleshoot control plane metrics issues

Make sure that the `AzureMonitorMetricsControlPlanePreview`

feature flag is enabled and that the `ama-metrics`

pods are running.

Note

The [troubleshooting methods](/en-us/azure/azure-monitor/containers/prometheus-metrics-troubleshoot) for the managed service for Prometheus don't apply directly in this scenario. The components that scrape the control plane aren't included in the managed service for Prometheus add-on.

**Configmap file formatting**: Make sure that you use the correct formatting in the configmap file. Verify that the fields`default-targets-metrics-keep-list`

,`minimal-ingestion-profile`

, and`default-scrape-settings-enabled`

and other fields are correctly populated with their intended values.**Isolate the control plane from the data plane**: Start by setting some of the[node-related metrics](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-default)to`true`

, and then verify that the metrics are forwarded to the workspace. Completing these steps helps you determine whether an issue is specific to scraping control plane metrics.**A change in the number of events ingested**: After you apply the changes, you can open the metrics explorer in the Azure portal. Go to the Azure Monitor overview pane for the cluster or go to the**Monitoring**section of the selected cluster. Check for an increase or a decrease in the number of events ingested per minute. This information can help you determine whether a specific metric is missing or if all metrics are missing.**A specific metric isn't exposed**: In some scenarios, a metric is documented, but it isn't exposed from the target and isn't forwarded to the Azure Monitor workspace. In this case, it's necessary to verify that other metrics are forwarded to the workspace.Note

If you want to collect the

`apiserver_request_duration_seconds`

metric or another bucket metric, you must set the entire series in the histogram family:`controlplane-apiserver = "apiserver_request_duration_seconds_bucket|apiserver_request_duration_seconds_sum|apiserver_request_duration_seconds_count"`

**No access to the Azure Monitor workspace**: When you enable the add-on, you might specify an existing workspace that you can't access. In that scenario, it appears that metrics aren't collected and forwarded. Make sure that you create a new workspace to use to collect metrics when you enable the add-on or when you create the cluster.

## Disable control plane metrics on your AKS cluster

You can disable control plane metrics at any time by disabling the managed service for Prometheus add-on and unregistering the `AzureMonitorMetricsControlPlanePreview`

feature flag.

Remove the metrics add-on that scrapes Prometheus metrics by using the

command:`az aks update`

`az aks update --disable-azure-monitor-metrics --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP`

To disable scraping control plane metrics on the AKS cluster, unregister the

`AzureMonitorMetricsControlPlanePreview`

feature flag via thecommand:`az feature unregister`

`az feature unregister "Microsoft.ContainerService" --name "AzureMonitorMetricsControlPlanePreview"`


## Frequently asked questions

### Can I scrape control plane metrics by using self-hosted Prometheus?

No. Currently, you can't scrape control plane metrics by using self-hosted Prometheus. Self-hosted Prometheus can scrape only a single instance, depending on the load balancer, so the metrics aren't reliable. Often, multiple replicas of the control plane metrics are visible only through the managed service for Prometheus.

### Why isn't the user agent available in the control plane metrics?

In AKS, [control plane metrics](https://kubernetes.io/docs/reference/instrumentation/metrics/) don't have the user agent. The user agent is available only through the control plane logs that you access in [diagnostic settings](/en-us/azure/azure-monitor/essentials/diagnostic-settings).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-network -->

# Best practices for network connectivity and security in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

On **31 March 2028**, kubenet networking for Azure Kubernetes Service (AKS) will be retired.

To avoid service disruptions, **you'll need to** [upgrade to Azure Container Networking Interface (CNI) overlay](/en-us/azure/aks/upgrade-aks-ipam-and-dataplane#upgrade-an-existing-cluster-to-azure-cni-overlay) **before that date**, when workloads running on kubenet for AKS will no longer be supported.

As you create and manage clusters in Azure Kubernetes Service (AKS), you provide network connectivity for your nodes and applications. These network resources include IP address ranges, load balancers, and ingress controllers.

This best practices article focuses on network connectivity and security for cluster operators. In this article, you learn how to:

- Explain Azure Container Networking Interface (CNI) network mode in AKS.
- Plan for required IP addressing and connectivity.
- Distribute traffic using load balancers, ingress controllers, or a web application firewall (WAF).
- Securely connect to cluster nodes.

## Choose the appropriate network model


Best practice guidanceUse Azure CNI networking in AKS for integration with existing virtual networks or on-premises networks. This network model allows greater separation of resources and controls in an enterprise environment.


Virtual networks provide the basic connectivity for AKS nodes and customers to access your applications. There are two different ways to deploy AKS clusters into virtual networks:

**Azure CNI networking**: Deploys into a virtual network and uses the[Azure CNI](https://github.com/Azure/azure-container-networking/blob/master/docs/cni.md)Kubernetes plugin. Pods receive individual IPs that can route to other network services or on-premises resources.

Azure CNI is a valid option for production deployments.

### CNI Networking

Azure CNI is a vendor-neutral protocol that lets the container runtime make requests to a network provider. It assigns IP addresses to pods and nodes, and provides IP address management (IPAM) features as you connect to existing Azure virtual networks. Each node and pod resource receives an IP address in the Azure virtual network. There's no need for extra routing to communicate with other resources or services.

Notably, Azure CNI networking for production allows for separation of control and management of resources. From a security perspective, you often want different teams to manage and secure those resources. With Azure CNI networking, you connect to existing Azure resources, on-premises resources, or other services directly via IP addresses assigned to each pod.

When you use Azure CNI networking, the virtual network resource is in a separate resource group to the AKS cluster. Delegate permissions for the AKS cluster identity to access and manage these resources. The cluster identity used by the AKS cluster must have at least [Network Contributor](/en-us/azure/role-based-access-control/built-in-roles#network-contributor) permissions on the subnet within your virtual network.

If you wish to define a [custom role](/en-us/azure/role-based-access-control/custom-roles) instead of using the built-in Network Contributor role, the following permissions are required:

`Microsoft.Network/virtualNetworks/subnets/join/action`

`Microsoft.Network/virtualNetworks/subnets/read`


By default, AKS uses a managed identity for its cluster identity. However, you can use a service principal instead.

- For more information about AKS service principal delegation, see
[Delegate access to other Azure resources](kubernetes-service-principal#delegate-access-to-other-azure-resources). - For more information about managed identities, see
[Use managed identities](use-managed-identity).

As each node and pod receives its own IP address, plan out the address ranges for the AKS subnets. Keep the following criteria in mind:

- The subnet must be large enough to provide IP addresses for every node, pod, and network resource you deploy.
- With Azure CNI networking, each running node has default limits to the number of pods.

- Avoid using IP address ranges that overlap with existing network resources.
- It's necessary to allow connectivity to on-premises or peered networks in Azure.

- To handle scale-out events or cluster upgrades, you need extra IP addresses available in the assigned subnet.
- This extra address space is especially important if you use Windows Server containers, as those node pools require an upgrade to apply the latest security patches. For more information on Windows Server nodes, see
[Upgrade a node pool in AKS](manage-node-pools#upgrade-a-single-node-pool).

- This extra address space is especially important if you use Windows Server containers, as those node pools require an upgrade to apply the latest security patches. For more information on Windows Server nodes, see

To calculate the IP address required, see [Configure Azure CNI networking in AKS](configure-azure-cni).

When creating a cluster with Azure CNI networking, you specify other address ranges for the cluster, such as the Docker bridge address, DNS service IP, and service address range. In general, make sure these address ranges don't overlap each other or any networks associated with the cluster, including any virtual networks, subnets, on-premises and peered networks.

For the specific details around limits and sizing for these address ranges, see [Configure Azure CNI networking in AKS](configure-azure-cni).

## Distribute ingress traffic


Best practice guidanceTo distribute HTTP or HTTPS traffic to your applications, use ingress resources and controllers. Compared to an Azure load balancer, ingress controllers provide extra features and can be managed as native Kubernetes resources.


While an Azure load balancer can distribute customer traffic to applications in your AKS cluster, it's limited in understanding that traffic. A load balancer resource works at *layer 4* and distributes traffic based on protocol or ports.

Most web applications using HTTP or HTTPS should use Kubernetes ingress resources and controllers, which work at *layer 7*. Ingress can distribute traffic based on the URL of the application and handle TLS/SSL termination. Ingress also reduces the number of IP addresses you expose and map.

With a load balancer, each application typically needs a public IP address assigned and mapped to the service in the AKS cluster. With an ingress resource, a single IP address can distribute traffic to multiple applications.

There are two components for ingress:

- An ingress
*resource* - An ingress
*controller*

### Ingress resource

The *ingress resource* is a YAML manifest of `kind: Ingress`

. It defines the host, certificates, and rules to route traffic to services running in your AKS cluster.

The following example YAML manifest distributes traffic for *myapp.com* to one of two services, *blogservice* or *storeservice*, and directs the customer to one service or the other based on the URL they access.

```
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
name: myapp-ingress
spec:
ingressClassName: PublicIngress
tls:
- hosts:
- myapp.com
secretName: myapp-secret
rules:
- host: myapp.com
http:
paths:
- path: /blog
backend:
service:
name: blogservice
port: 80
- path: /store
backend:
service:
name: storeservice
port: 80
```


### Ingress controller

An *ingress controller* is a daemon that runs on an AKS node and watches for incoming requests. Traffic is then distributed based on the rules defined in the ingress resource. While the most common ingress controller is based on [NGINX](https://www.nginx.com/products/nginx/kubernetes-ingress-controller), AKS doesn't restrict you to a specific controller. You can use [Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview), [Contour](https://github.com/heptio/contour), [HAProxy](https://www.haproxy.org), [Traefik](https://github.com/containous/traefik), etc.

Ingress controllers must be scheduled on a Linux node. Indicate that the resource should run on a Linux-based node using a node selector in your YAML manifest or Helm chart deployment. For more information, see [Use node selectors to control where pods are scheduled in AKS](concepts-clusters-workloads#node-selectors).

## Ingress with the application routing addon

The application routing addon is the recommended way to configure an Ingress controller in AKS. The application routing addon is a fully managed, ingress controller for Azure Kubernetes Service (AKS) that provides the following features:

Easy configuration of managed NGINX Ingress controllers based on Kubernetes NGINX Ingress controller.

Integration with Azure DNS for public and private zone management.

SSL termination with certificates stored in Azure Key Vault.


For more information about the application routing add-on, see [Managed NGINX ingress with the application routing add-on](app-routing).

## Secure traffic with a web application firewall (WAF)


Best practice guidanceTo scan incoming traffic for potential attacks, use a web application firewall (WAF) such as

[Barracuda WAF for Azure]or[Azure Application Gateway for Containers]. These more advanced network resources can also route traffic beyond just HTTP and HTTPS connections or basic TLS termination.

Typically, an ingress controller is a Kubernetes resource in your AKS cluster that distributes traffic to services and applications. The controller runs as a daemon on an AKS node, and consumes some of the node's resources, like CPU, memory, and network bandwidth. In larger environments, you may want to consider the following:

- Offload some of this traffic routing or TLS termination to a network resource outside of the AKS cluster.
- Scan incoming traffic for potential attacks.

For that extra layer of security, a web application firewall (WAF) filters the incoming traffic. With a set of rules, the Open Web Application Security Project (OWASP) watches for attacks like cross-site scripting or cookie poisoning. [Azure Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview) is a WAF that integrates with AKS clusters, locking in these security features before the traffic reaches your AKS cluster and applications.

Since other third-party solutions also perform these functions, you can continue to use existing investments or expertise in your preferred product.

Load balancer or ingress resources continually run in your AKS cluster and refine the traffic distribution. [Azure Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/overview) can be centrally managed as an ingress controller with a resource definition. To get started, [create an Application Gateway for Containers](/en-us/azure/application-gateway/for-containers/quickstart-deploy-application-gateway-for-containers-alb-controller).

## Control traffic flow with network policies


Best practice guidanceUse network policies to allow or deny traffic to pods. By default, all traffic is allowed between pods within a cluster. For improved security, define rules that limit pod communication.


Network policy is a Kubernetes feature available in AKS that lets you control the traffic flow between pods. You allow or deny traffic to the pod based on settings such as assigned labels, namespace, or traffic port. Network policies are a cloud-native way to control the flow of traffic for pods. As pods are dynamically created in an AKS cluster, required network policies can be automatically applied.

To use [network policies in AKS](use-network-policies), the feature can be enabled either during cluster creation or on an existing AKS cluster. If you are planning to use network policies, ensure the feature is enabled on your AKS cluster.

Note

Network policies could be used for Linux-based or Windows-based nodes and pods in AKS.

You create a network policy as a Kubernetes resource using a YAML manifest. Policies are applied to defined pods, with ingress or egress rules defining traffic flow.

The following example applies a network policy to pods with the *app: backend* label applied to them. The ingress rule only allows traffic from pods with the *app: frontend* label.

```
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
name: backend-policy
spec:
podSelector:
matchLabels:
app: backend
ingress:
- from:
- podSelector:
matchLabels:
app: frontend
```


To get started with policies, see [Secure traffic between pods using network policies in Azure Kubernetes Service (AKS)](use-network-policies).

## Securely connect to nodes through a bastion host


Best practice guidanceDon't expose remote connectivity to your AKS nodes. Create a bastion host, or jump box, in a management virtual network. Use the bastion host to securely route traffic into your AKS cluster to remote management tasks.


You can complete most operations in AKS using the Azure management tools or through the Kubernetes API server. AKS nodes are only available on a private network and aren't connected to the public internet. To connect to nodes and provide maintenance and support, route your connections through a bastion host, or jump box. Verify this host lives in a separate, securely peered management virtual network to the AKS cluster virtual network.

You should also secure the management network for the bastion host. Use an [Azure ExpressRoute](/en-us/azure/expressroute/expressroute-introduction) or [VPN gateway](/en-us/azure/vpn-gateway/vpn-gateway-about-vpngateways) to connect to an on-premises network and control access using network security groups.

## Next steps

This article focused on network connectivity and security. For more information about network basics in Kubernetes, see [Network concepts for applications in Azure Kubernetes Service (AKS)](concepts-network)

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-multiple-standard-load-balancer -->

# Use multiple load balancers in Azure Kubernetes Service (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) normally provisions one Standard Load Balancer (SLB) for all `LoadBalancer`

Services in a cluster. Because each node NIC is limited to [ 300 inbound load‑balancing rules and 8 private‑link services](/en-us/azure/azure-resource-manager/management/azure-subscription-service-limits#load-balancer), large clusters or port‑heavy workloads can quickly exhaust these limits.

The **multiple SLB preview** removes that bottleneck by letting you create several SLBs inside the same cluster and shard nodes and Services across them. You define *load‑balancer configurations*, each tied to a primary agent pool and optional namespace, label, or node selectors—and AKS automatically places nodes and Services on the appropriate SLB. Outbound SNAT behavior is unchanged if `outboundType`

is `loadBalancer`

. Outbound traffic still flows through the first SLB.

Use this feature to:

- Scale beyond 300 inbound rules without adding clusters.
- Isolate tenant or workload traffic by binding a dedicated SLB to its own agent pool.
- Distribute private‑link services across multiple SLBs when you approach the per‑SLB limit.

## Prerequisites

`aks-preview`

extension 18.0.0b1 or later.- Subscription feature flag
`Microsoft.ContainerService/MultipleStandardLoadBalancersPreview`

registered. - Kubernetes version 1.28 or later.
- Cluster created with
`--load-balancer-backend-pool-type nodeIP`

or update and existing cluster using`az aks update`

.

### Install the aks-preview Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the aks-preview extension using the

command.`az extension add`

`az extension add --name aks-preview`

Update to the latest version of the extension released using the

command.`az extension update`

`az extension update --name aks-preview`


### Register the `MultipleStandardLoadBalancersPreview`

feature flag

Register the

`MultipleStandardLoadBalancersPreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "MultipleStandardLoadBalancersPreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command:`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "MultipleStandardLoadBalancersPreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## How AKS chooses a load balancer (node & Service placement)

AKS uses multiple inputs to determine where to place nodes and expose LoadBalancer Services. These inputs are defined in each load balancer configuration and influence which SLB is selected for each resource.

| Input type | Applies to | Description |
|---|---|---|
Primary agent pool`--primary-agent-pool-name` |
Nodes | Required. All nodes in this pool are always added to the SLB’s backend pool. Ensures each SLB has at least one healthy node. |
Node selector`--node-selector` |
Nodes | Optional. Adds any node with matching labels to the SLB, in addition to the primary pool. |
Service namespace selector`--service-namespace-selector` |
Services | Optional. Only Services in namespaces with matching labels are considered for this SLB. |
Service label selector`--service-label-selector` |
Services | Optional. Only Services with matching labels are eligible for this SLB. |
Service annotation`service.beta.kubernetes.io/azure-load-balancer-configurations` |
Services | Optional. Limits placement to one or more explicitly named SLB configurations. Without it, any matching configuration is eligible. |

Note

Selectors define eligibility. The annotation (if used) restricts the controller to a specific subset of SLBs.

### How AKS uses these inputs

The AKS control plane continuously reconciles node and Service state using the rules above:

#### Node placement

When a node is added or updated, AKS checks which SLBs it qualifies for based on primary pool and node selector.

- If multiple SLBs match, the controller picks the one with the fewest current nodes.
- The node is added to that SLB’s backend pool.

#### Service placement

When a LoadBalancer Service is created or updated:

- AKS finds SLBs whose namespace and label selectors match the Service.
- If the Service annotation is present, only those named SLBs are considered.
- SLBs that have allowServicePlacement=false or that would exceed Azure limits (300 rules or 8 private-link services) are excluded.
- Among valid options, the SLB with the fewest rules is chosen.

### externalTrafficPolicy (ETP) behavior

AKS handles Services differently depending on the value of `externalTrafficPolicy`

.

| Mode | How load balancer selection works | How backend pool membership is built | Notes |
|---|---|---|---|
Cluster (default) |
The controller follows the standard placement rules described above. A single load-balancing rule targets the shared kubernetes backend pool on the chosen SLB. |
All nodes in that SLB’s `kubernetes` pool are healthy targets. Nodes without matching Pods are removed automatically by health probes. |
Same behavior as today in single-SLB clusters. |
Local |
The controller still uses the selector-based algorithm to pick an SLB, but creates a dedicated backend pool per Service instead of using the shared pool. |
Membership is synced from the Service’s `EndpointSlice` objects, so only nodes that actually host ready Pods are added. Health probes continue to use `healthCheckNodePort` to drop unhealthy nodes. |
Guarantees client IP preservation and avoids routing through nodes that lack Pods, even when nodes are sharded across multiple SLBs. |


Why a dedicated pool for ETP Local?

In multi-SLB mode, nodes that host Pods for a given Service may reside on different SLBs from the client-facing VIP. A shared backend pool would often contain zero eligible nodes, breaking traffic. By allocating a per-Service pool and syncing it from`EndpointSlice`

, AKS ensures the Service’s SLB always points at the correct nodes.

**Impact on quotas**

- Each ETP Local Service adds one backend pool and one load-balancing rule to its SLB.
- These count toward the 300-rule limit, so monitor rule usage when you have many ETP Local Services.

**No change to outbound traffic**

Outbound SNAT still flows through the first SLB’s `aksOutboundBackendPool`

when `outboundType`

is `loadBalancer`

, independent of ETP settings.

#### Optional: Rebalancing

You can manually rebalance node distribution later using `az aks loadbalancer rebalance`

.

This design lets you define flexible, label-driven routing for both infrastructure and workloads, while AKS handles placement automatically to maintain balance and avoid quota issues.

## Add the first load balancer configuration

Add a configuration named `kubernetes`

and bind it to a *primary* agent pool that always has at least one node. Removing every configuration switches the cluster back to single‑SLB mode.

Important

To enable multiple‑SLB mode you **must** add a load‑balancer configuration named `kubernetes`

and attach it to a *primary* agent pool that always has at least one ready node.

The presence of this configuration toggles multi‑SLB support; in service selection, it has no special priority and is treated like any other load balancer configuration.

If you delete every load‑balancer configuration, the cluster automatically falls back to single‑SLB mode, which can briefly disrupt service routing or SNAT flows.

Set environment variables for use throughout this tutorial. You can replace all placeholder values with your own except

`DEFAULT_LB_NAME`

, which must remain as`kubernetes`

.`RESOURCE_GROUP="rg-aks-multislb" CLUSTER_NAME="aks-multi-slb" LOCATION="westus" DEFAULT_LB_NAME="kubernetes" PRIMARY_POOL="nodepool1"`

Create resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`

Create an AKS cluster using the

command.\`az aks create`

`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME \ --load-balancer-backend-pool-type nodeIP \ --node-count 3`

Add a default load balancer using the

command.`az aks loadbalancer add`

`az aks loadbalancer add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $DEFAULT_LB_NAME \ --primary-agent-pool-name $PRIMARY_POOL \ --allow-service-placement true`


## Add additional load balancers

Create tenant‑specific configurations by specifying a different primary pool plus optional namespace, label, or node selectors.

Team 1 will run its own workloads in a separate node pool. Assign a

`tenant=team1`

label so workloads can be scheduled using selectors:`TEAM1_POOL="team1pool" TEAM1_LB_NAME="team1-lb"`

Create a second node pool for team 1 using the

command.`az aks nodepool add`

`az aks nodepool add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $TEAM1_POOL \ --labels tenant=team1 \ --node-count 2`

Create a load balancer for team 1 using the

command.`az aks loadbalancer add`

`az aks loadbalancer add --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME \ --name $TEAM1_LB_NAME \ --primary-agent-pool-name $TEAM1_POOL \ --service-namespace-selector "tenant=team1" \ --node-selector "tenant=team1"`

Label the target namespace (e.g.,

`team1-apps`

) to match the selector using thecommand.`az aks command invoke`

`az aks command invoke \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --command " kubectl create namespace team1-apps --dry-run=client -o yaml | kubectl apply -f - kubectl label namespace team1-apps tenant=team1 --overwrite "`

You can now list the load balancers in the cluster to see the multiple configurations using the

command.`az aks loadbalancer list`

`az aks loadbalancer list --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME --output table`

Example output:

`AllowServicePlacement ETag Name PrimaryAgentPoolName ProvisioningState ResourceGroup ----------------------- ------- ---------- ---------------------- ------------------- --------------- True <ETAG> kubernetes nodepool1 Succeeded rg-aks-multislb True <ETAG> team1-lb team1pool Succeeded rg-aks-multislb`


### Deploy a Service to a specific load balancer

Add the annotation `service.beta.kubernetes.io/azure-load-balancer-configurations`

with a comma‑separated list of configuration names. If the annotation is omitted, the controller chooses automatically.

```
az aks command invoke \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--command "
cat <<EOF | kubectl apply -f -
apiVersion: v1
kind: Service
metadata:
name: lb-svc-1
namespace: team1-apps
labels:
app: nginx-test
annotations:
service.beta.kubernetes.io/azure-load-balancer-configurations: \"team1-lb\"
# service.beta.kubernetes.io/azure-load-balancer-internal: "true" # If you want to create an internal load balancer.
spec:
selector:
app: nginx-test
ports:
- name: port1
port: 80
targetPort: 80
protocol: TCP
type: LoadBalancer
---
apiVersion: apps/v1
kind: Deployment
metadata:
name: nginx-test
namespace: team1-apps
labels:
app: nginx
spec:
replicas: 1
selector:
matchLabels:
app: nginx-test
template:
metadata:
labels:
app: nginx-test
spec:
containers:
- image: nginx
imagePullPolicy: Always
name: nginx
ports:
- containerPort: 80
protocol: TCP
resources:
limits:
cpu: \"150m\"
memory: \"300Mi\"
EOF
"
```


### Rebalance nodes (optional)

Run a rebalance operation after scaling if rule counts become unbalanced using the [ az aks loadbalancer rebalance](/en-us/cli/azure/aks/loadbalancer#az-aks-loadbalancer-rebalance) command. This command disrupts active flows, so schedule it during a maintenance window.

```
az aks loadbalancer rebalance --resource-group $RESOURCE_GROUP --cluster-name $CLUSTER_NAME
```


## Monitoring and troubleshooting

- Watch controller events (
`kubectl get events …`

) to confirm that Services are reconciled. - If external connectivity is blocked, open a node shell and curl the Service VIP to confirm kube‑proxy routing.

## Limitations and known issues

| Limitation | Details |
|---|---|
| Outbound SNAT | Always uses the first SLB; outbound flows aren’t sharded. |
| Backend pool type | Create or update and existing cluster to use `nodeIP` backend pools. |
| Autoscaler zeros | A primary agent pool can’t scale to 0 nodes. |
ETP `local` Rule Growth |
Each ETP `local` Service uses its own rule and backend pool, so rule counts can grow faster than with `cluster` mode. |
| Rebalance disruption | Removing a node from a backend pool drops in‑flight connections. Plan maintenance windows. |
| Configuration reload timing | After running `az aks loadbalancer` , changes may not take effect immediately. The AKS operation finishes quickly, but the cloud-controller-manager may take longer to apply updates. Wait for the `EnsuredLoadBalancer` event to confirm the changes are active. |

## Clean up resources

Delete the resource group when you’re finished to remove the cluster and load balancers using the [ az group delete](/en-us/cli/azure/group#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP --yes --no-wait
```


## Next steps

The multiple SLB feature helps scale and isolate workloads at the networking layer while maintaining simplicity through Azure-managed configuration. For more information, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/workload-identity-deploy-cluster -->

# Deploy and configure Microsoft Entra Workload ID on an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to deploy and configure an Azure Kubernetes Service (AKS) cluster with [Microsoft Entra Workload ID](workload-identity-overview). The steps in this article include:

- Create a new or update an existing AKS cluster using the Azure CLI with OpenID Connect (OIDC) issuer and Microsoft Entra Workload ID enabled.
- Create a workload identity and Kubernetes service account.
- Configure the managed identity for token federation.
- Deploy the workload and verify authentication with the workload identity.
- Optionally grant a pod in the cluster access to secrets in an Azure key vault.

## Prerequisites

- If you don't have an Azure account, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - This article requires version 2.47.0 or later of the Azure CLI. If using Azure Cloud Shell, the latest version is already installed.
- Make sure that the identity that you're using to create your cluster has the appropriate minimum permissions. For more information, see
[Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity). - If you have multiple Azure subscriptions, select the appropriate subscription ID in which the resources should be billed using the
command.`az account set`


Note

You can use *Service Connector* to help you configure some steps automatically. For more information, see [Tutorial: Connect to Azure storage account in Azure Kubernetes Service (AKS) with Service Connector using Microsoft Entra Workload ID](/en-us/azure/service-connector/tutorial-python-aks-storage-workload-identity).

## Create a resource group

Create a resource group using the

command.`az group create`

`export RANDOM_ID="$(openssl rand -hex 3)" export RESOURCE_GROUP="myResourceGroup$RANDOM_ID" export LOCATION="<your-preferred-region>" az group create --name "${RESOURCE_GROUP}" --location "${LOCATION}"`


## Enable OIDC issuer and Microsoft Entra Workload ID on an AKS cluster

You can enable OIDC issuer and Microsoft Entra Workload ID on a new or existing AKS cluster.

Create an AKS cluster using the

command with the`az aks create`

`--enable-oidc-issuer`

parameter to enable OIDC issuer and the`--enable-workload-identity`

parameter to enable Microsoft Entra Workload ID. The following example creates a cluster with a single node:`export CLUSTER_NAME="myAKSCluster$RANDOM_ID" az aks create \ --resource-group "${RESOURCE_GROUP}" \ --name "${CLUSTER_NAME}" \ --enable-oidc-issuer \ --enable-workload-identity \ --generate-ssh-keys`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.


## Retrieve the OIDC issuer URL

Get the OIDC issuer URL and save it to an environmental variable using the [

`az aks show`

][az-aks-show] command.`export AKS_OIDC_ISSUER="$(az aks show --name "${CLUSTER_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --query "oidcIssuerProfile.issuerUrl" \ --output tsv)"`

The environment variable should contain the issuer URL, similar to the following example:

`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/11111111-1111-1111-1111-111111111111/`

By default, the issuer is set to use the base URL

`https://{region}.oic.prod-aks.azure.com/{tenant_id}/{uuid}`

, where the value for`{region}`

matches the location to which the AKS cluster is deployed. The value`{uuid}`

represents the OIDC key, which is a randomly generated and immutable GUID for each cluster.

## Create a managed identity

Get your subscription ID and save it to an environment variable using the [

`az account show`

][az-account-show] command.`export SUBSCRIPTION="$(az account show --query id --output tsv)"`

Create a user-assigned managed identity using the

command.`az identity create`

`export USER_ASSIGNED_IDENTITY_NAME="myIdentity$RANDOM_ID" az identity create \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --location "${LOCATION}" \ --subscription "${SUBSCRIPTION}"`

The following output example shows successful creation of a managed identity:

`{ "clientId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "id": "/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups/myResourceGroupxxxxxx/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentityxxxxxx", "location": "eastus", "name": "myIdentityxxxxxx", "principalId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "resourceGroup": "myResourceGroupxxxxxx", "systemData": null, "tags": {}, "tenantId": "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx", "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`

Get the client ID of the managed identity and save it to an environment variable using the [

`az identity show`

][az-identity-show] command.`export USER_ASSIGNED_CLIENT_ID="$(az identity show \ --resource-group "${RESOURCE_GROUP}" \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --query 'clientId' \ --output tsv)"`


## Create a Kubernetes service account

Connect to your AKS cluster using the

command.`az aks get-credentials`

`az aks get-credentials --name "${CLUSTER_NAME}" --resource-group "${RESOURCE_GROUP}"`

Create a Kubernetes service account and annotate it with the client ID of the managed identity by applying the following manifest using the

`kubectl apply`

command:`export SERVICE_ACCOUNT_NAME="workload-identity-sa$RANDOM_ID" export SERVICE_ACCOUNT_NAMESPACE="default" cat <<EOF | kubectl apply -f - apiVersion: v1 kind: ServiceAccount metadata: annotations: azure.workload.identity/client-id: "${USER_ASSIGNED_CLIENT_ID}" name: "${SERVICE_ACCOUNT_NAME}" namespace: "${SERVICE_ACCOUNT_NAMESPACE}" EOF`

The following output shows successful creation of the workload identity:

`serviceaccount/workload-identity-sa created`


## Create the federated identity credential

Create a federated identity credential between the managed identity, the service account issuer, and the subject using the

command.`az identity federated-credential create`

`export FEDERATED_IDENTITY_CREDENTIAL_NAME="myFedIdentity$RANDOM_ID" az identity federated-credential create \ --name ${FEDERATED_IDENTITY_CREDENTIAL_NAME} \ --identity-name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --issuer "${AKS_OIDC_ISSUER}" \ --subject system:serviceaccount:"${SERVICE_ACCOUNT_NAMESPACE}":"${SERVICE_ACCOUNT_NAME}" \ --audience api://AzureADTokenExchange`

Note

It takes a few seconds for the federated identity credential to propagate after it's added. If a token request is made immediately after adding the federated identity credential, the request might fail until the cache is refreshed. To avoid this issue, you can add a slight delay after adding the federated identity credential.


For more information about federated identity credentials in Microsoft Entra, see [Overview of federated identity credentials in Microsoft Entra ID](/en-us/graph/api/resources/federatedidentitycredentials-overview).

## Create a key vault with Azure RBAC authorization

The following example shows how to use the Azure role-based access control (Azure RBAC) permission model to grant the pod access to the key vault. For more information about the Azure RBAC permission model for Azure Key Vault, see [Grant permission to applications to access an Azure key vault using Azure RBAC](/en-us/azure/key-vault/general/rbac-guide).

Create a key vault with purge protection and Azure RBAC authorization enabled using the [

`az keyvault create`

][az-keyvault-create] command. You can also use an existing key vault if it's configured for both purge protection and Azure RBAC authorization:`export KEYVAULT_NAME="keyvault-workload-id$RANDOM_ID" # Ensure the key vault name is between 3-24 characters az keyvault create \ --name "${KEYVAULT_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --location "${LOCATION}" \ --enable-purge-protection \ --enable-rbac-authorization`

Get the key vault resource ID and save it to an environment variable using the [

`az keyvault show`

][az-keyvault-show] command.`export KEYVAULT_RESOURCE_ID=$(az keyvault show --resource-group "${RESOURCE_GROUP}" \ --name "${KEYVAULT_NAME}" \ --query id \ --output tsv)`


### Assign RBAC permissions for key vault management

Get the caller object ID and save it to an environment variable using the [

`az ad signed-in-user show`

][az-ad-signed-in-user-show] command.`export CALLER_OBJECT_ID=$(az ad signed-in-user show --query id -o tsv)`

Assign yourself the Azure RBAC

[Key Vault Secrets Officer](/en-us/azure/role-based-access-control/built-in-roles/security#key-vault-secrets-officer)role so that you can create a secret in the new key vault using the [`az role assignment create`

][az-role-assignment-create] command.`az role assignment create --assignee "${CALLER_OBJECT_ID}" \ --role "Key Vault Secrets Officer" \ --scope "${KEYVAULT_RESOURCE_ID}"`


### Create and configure secret access

Create a secret in the key vault using the [

`az keyvault secret set`

][az-keyvault-secret-set] command.`export KEYVAULT_SECRET_NAME="my-secret$RANDOM_ID" az keyvault secret set \ --vault-name "${KEYVAULT_NAME}" \ --name "${KEYVAULT_SECRET_NAME}" \ --value "Hello\!"`

Get the principal ID of the user-assigned managed identity and save it to an environment variable using the [

`az identity show`

][az-identity-show] command.`export IDENTITY_PRINCIPAL_ID=$(az identity show \ --name "${USER_ASSIGNED_IDENTITY_NAME}" \ --resource-group "${RESOURCE_GROUP}" \ --query principalId \ --output tsv)`

Assign the

[Key Vault Secrets User](/en-us/azure/role-based-access-control/built-in-roles/security#key-vault-secrets-user)role to the user-assigned managed identity using the [`az role assignment create`

][az-role-assignment-create] command. This step gives the managed identity permission to read secrets from the key vault.`az role assignment create \ --assignee-object-id "${IDENTITY_PRINCIPAL_ID}" \ --role "Key Vault Secrets User" \ --scope "${KEYVAULT_RESOURCE_ID}" \ --assignee-principal-type ServicePrincipal`

Create an environment variable for the key vault URL using the [

`az keyvault show`

][az-keyvault-show] command:`export KEYVAULT_URL="$(az keyvault show \ --resource-group "${RESOURCE_GROUP}" \ --name ${KEYVAULT_NAME} \ --query properties.vaultUri \ --output tsv)"`


## Deploy a verification pod and test access

Deploy a pod to verify that the workload identity can access the secret in the key vault. The following example uses the

`ghcr.io/azure/azure-workload-identity/msal-go`

image, which contains a sample application that retrieves a secret from Azure Key Vault using Microsoft Entra Workload ID:`kubectl apply -f - <<EOF apiVersion: v1 kind: Pod metadata: name: sample-workload-identity-key-vault namespace: ${SERVICE_ACCOUNT_NAMESPACE} labels: azure.workload.identity/use: "true" spec: serviceAccountName: ${SERVICE_ACCOUNT_NAME} containers: - image: ghcr.io/azure/azure-workload-identity/msal-go name: oidc env: - name: KEYVAULT_URL value: ${KEYVAULT_URL} - name: SECRET_NAME value: ${KEYVAULT_SECRET_NAME} nodeSelector: kubernetes.io/os: linux EOF`

Wait for the pod to be in the

`Ready`

state using the`kubectl wait`

command.`kubectl wait --namespace ${SERVICE_ACCOUNT_NAMESPACE} --for=condition=Ready pod/sample-workload-identity-key-vault --timeout=120s`

Check that the

`SECRET_NAME`

environment variable is set in the pod using thecommand.`kubectl describe`

`kubectl describe pod sample-workload-identity-key-vault | grep "SECRET_NAME:"`

If successful, the output should be similar to the following example:

`SECRET_NAME: ${KEYVAULT_SECRET_NAME}`

Verify that pods can get a token and access the resource using the

`kubectl logs`

command.`kubectl logs sample-workload-identity-key-vault`

If successful, the output should be similar to the following example:

`I0114 10:35:09.795900 1 main.go:63] "successfully got secret" secret="Hello\\!"`

Important

Azure RBAC role assignments can take up to 10 minutes to propagate. If the pod is unable to access the secret, you might need to wait for the role assignment to propagate. For more information, see

[Troubleshoot Azure RBAC](/en-us/azure/role-based-access-control/troubleshooting#).

## Disable Microsoft Entra Workload ID on an AKS cluster

Disable Microsoft Entra Workload ID on the AKS cluster where it's been enabled and configured, update the AKS cluster using the

command with the`az aks update`

`--disable-workload-identity`

parameter.`az aks update \ --resource-group "${RESOURCE_GROUP}" \ --name "${CLUSTER_NAME}" \ --disable-workload-identity`


## Related content

In this article, you deployed a Kubernetes cluster and configured it to use Microsoft Entra Workload ID in preparation for application workloads to authenticate with that credential. Now you're ready to deploy your application and configure it to use the workload identity with the latest version of the [Azure Identity](/en-us/azure/active-directory/develop/reference-v2-libraries) client library. If you can't rewrite your application to use the latest client library version, you can [set up your application pod](workload-identity-migrate-from-pod-identity) to authenticate using managed identity with workload identity as a short-term migration solution.

The [Service Connector](/en-us/azure/service-connector/overview) integration helps simplify the connection configuration for AKS workloads and Azure backing services. It securely handles authentication and network configurations and follows best practices for connecting to Azure services. For more information, see [Connect to Azure OpenAI in Foundry Models in AKS using Microsoft Entra Workload Identity](/en-us/azure/service-connector/tutorial-python-aks-openai-workload-identity) and the [Service Connector introduction](https://blog.aks.azure.com/2024/05/23/service-connector-intro).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-identity -->

# Best practices for authentication and authorization in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you deploy and maintain clusters in Azure Kubernetes Service (AKS), you implement ways to manage access to resources and services. Without these controls:

- Accounts could have access to unnecessary resources and services.
- Tracking credentials used to make changes can be difficult.

In this article, we discuss what recommended practices a cluster operator can follow to manage access and identity for AKS clusters. You'll learn how to:

- Authenticate AKS cluster users with Microsoft Entra ID.
- Control access to resources with Kubernetes role-based access control (Kubernetes RBAC).
- Use Azure RBAC to granularly control access to the AKS resource, the Kubernetes API at scale, and the
`kubeconfig`

. - Use a
[workload identity](workload-identity-overview)to access Azure resources from your pods.

Warning

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service has been deprecated as of 10/24/2022.

If you have [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) enabled on your AKS cluster or are considering implementing it,
we recommend you **review the workload identity overview article** to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.

## Use Microsoft Entra ID


Best practice guidanceDeploy AKS clusters with

[Microsoft Entra integration]. Using Microsoft Entra ID centralizes the identity management layer. Any change in user account or group status is automatically updated in access to the AKS cluster. Scope users or groups to the minimum permissions amount using[Roles, ClusterRoles, or Bindings].

Your Kubernetes cluster developers and application owners need access to different resources. Kubernetes lacks an identity management solution for you to control the resources with which users can interact. Instead, you can integrate your cluster with an existing identity solution like Microsoft Entra ID, an enterprise-ready identity management solution.

With Microsoft Entra integrated clusters in AKS, you create *Roles* or *ClusterRoles* defining access permissions to resources. You then *bind* the roles to users or groups from Microsoft Entra ID. Learn more about these Kubernetes RBAC in [the next section](#use-kubernetes-role-based-access-control-kubernetes-rbac). Microsoft Entra integration and how you control access to resources can be seen in the following diagram:

- Developer authenticates with Microsoft Entra ID.
- The Microsoft Entra token issuance endpoint issues the access token.
- The developer performs an action using the Microsoft Entra token, such as
`kubectl create pod`

. - Kubernetes validates the token with Microsoft Entra ID and fetches the developer's group memberships.
- Kubernetes RBAC and cluster policies are applied.
- The developer's request is successful based on previous validation of Microsoft Entra group membership and Kubernetes RBAC and policies.

To create an AKS cluster that uses Microsoft Entra ID, see [Integrate Microsoft Entra ID with AKS](enable-authentication-microsoft-entra-id).

## Use Kubernetes role-based access control (Kubernetes RBAC)


Best practice guidanceDefine user or group permissions to cluster resources with Kubernetes RBAC. Create roles and bindings that assign the least amount of permissions required. Integrate with Microsoft Entra ID to automatically update any user status or group membership change and keep access to cluster resources current.


In Kubernetes, you provide granular access control to cluster resources. You define permissions at the cluster level, or to specific namespaces. You determine what resources can be managed and with what permissions. You then apply these roles to users or groups with a binding. For more information about *Roles*, *ClusterRoles*, and *Bindings*, see [Access and identity options for Azure Kubernetes Service (AKS)](concepts-identity).

For example, you create a role with full access to resources in the namespace named *finance-app*, as shown in the following example YAML manifest:

```
kind: Role
apiVersion: rbac.authorization.k8s.io/v1
metadata:
name: finance-app-full-access-role
namespace: finance-app
rules:
- apiGroups: [""]
resources: ["*"]
verbs: ["*"]
```


You then create a *RoleBinding* and bind the Microsoft Entra user *developer1@contoso.com* to it, as shown in the following YAML manifest:

```
kind: RoleBinding
apiVersion: rbac.authorization.k8s.io/v1
metadata:
name: finance-app-full-access-role-binding
namespace: finance-app
subjects:
- kind: User
name: developer1@contoso.com
apiGroup: rbac.authorization.k8s.io
roleRef:
kind: Role
name: finance-app-full-access-role
apiGroup: rbac.authorization.k8s.io
```


When *developer1@contoso.com* is authenticated against the AKS cluster, they have full permissions to resources in the *finance-app* namespace. In this way, you logically separate and control access to resources. Use Kubernetes RBAC with Microsoft Entra ID-integration.

To learn how to use Microsoft Entra groups to control access to Kubernetes resources using Kubernetes RBAC, see [Control access to cluster resources using role-based access control and Microsoft Entra identities in AKS](azure-ad-rbac).

## Use Azure RBAC


Best practice guidanceUse Azure RBAC to define the minimum required user and group permissions to AKS resources in one or more subscriptions.


There are two levels of access needed to fully operate an AKS cluster:

Access the AKS resource on your Azure subscription.

This access level allows you to:

- Control scaling or upgrading your cluster using the AKS APIs
- Pull your
`kubeconfig`

.

To learn how to control access to the AKS resource and the

`kubeconfig`

, see[Limit access to cluster configuration file](control-kubeconfig-access).Access to the Kubernetes API.

This access level is controlled either by:

[Kubernetes RBAC](#use-kubernetes-role-based-access-control-kubernetes-rbac)(traditionally) or- By integrating Azure RBAC with AKS for kubernetes authorization.

To learn how to granularly grant permissions to the Kubernetes API using Azure RBAC, see

[Use Azure RBAC for Kubernetes authorization](manage-azure-rbac).

## Use pod-managed identities

Warning

The open source Microsoft Entra pod-managed identity (preview) in Azure Kubernetes Service has been deprecated as of 10/24/2022.

If you have [Microsoft Entra pod-managed identity](use-azure-ad-pod-identity) enabled on your AKS cluster or are considering implementing it,
we recommend you **review the workload identity overview article** to understand our
recommendations and options to set up your cluster to use a Microsoft Entra Workload ID (preview).
This authentication method replaces pod-managed identity (preview), which integrates with the Kubernetes native capabilities
to federate with any external identity providers.

Don't use fixed credentials within pods or container images, as they are at risk of exposure or abuse. Instead, use *pod identities* to automatically request access using Microsoft Entra ID.

To access other Azure resources, like Azure Cosmos DB, Key Vault, or Blob storage, the pod needs authentication credentials. You could define authentication credentials with the container image or inject them as a Kubernetes secret. Either way, you would need to manually create and assign them. Usually, these credentials are reused across pods and aren't regularly rotated.

With pod-managed identities (preview) for Azure resources, you automatically request access to services through Microsoft Entra ID. Pod-managed identities is currently in preview for AKS. Refer to the [Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (Preview)](use-azure-ad-pod-identity) documentation to get started.

Microsoft Entra pod-managed identity (preview) supports two modes of operation:

**Standard**mode: In this mode, the following 2 components are deployed to the AKS cluster:[Managed Identity Controller(MIC)](https://azure.github.io/aad-pod-identity/docs/concepts/mic/): A Kubernetes controller that watches for changes to pods,[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/)and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)through the Kubernetes API Server. When it detects a relevant change, the MIC adds or deletes[AzureAssignedIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureassignedidentity/)as needed. Specifically, when a pod is scheduled, the MIC assigns the managed identity on Azure to the underlying virtual machine scale set used by the node pool during the creation phase. When all pods using the identity are deleted, it removes the identity from the virtual machine scale set of the node pool, unless the same managed identity is used by other pods. The MIC takes similar actions when AzureIdentity or AzureIdentityBinding are created or deleted.[Node Managed Identity (NMI)](https://azure.github.io/aad-pod-identity/docs/concepts/nmi/): is a pod that runs as a DaemonSet on each node in the AKS cluster. NMI intercepts security token requests to the[Azure Instance Metadata Service](/en-us/azure/virtual-machines/linux/instance-metadata-service?tabs=linux)on each node. It redirects requests to itself and validates if the pod has access to the identity it's requesting a token for, and fetch the token from the Microsoft Entra tenant on behalf of the application.

**Managed**mode: In this mode, there's only NMI. The identity needs to be manually assigned and managed by the user. For more information, see[Pod Identity in Managed Mode](https://azure.github.io/aad-pod-identity/docs/configure/pod_identity_in_managed_mode/). In this mode, when you use the[az aks pod-identity add](/en-us/cli/azure/aks/pod-identity#az-aks-pod-identity-add)command to add a pod identity to an Azure Kubernetes Service (AKS) cluster, it creates the[AzureIdentity](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentity/)and[AzureIdentityBinding](https://azure.github.io/aad-pod-identity/docs/concepts/azureidentitybinding/)in the namespace specified by the`--namespace`

parameter, while the AKS resource provider assigns the managed identity specified by the`--identity-resource-id`

parameter to virtual machine scale set of each node pool in the AKS cluster.

Note

If you instead decide to install the Microsoft Entra pod-managed identity using the [AKS cluster add-on](use-azure-ad-pod-identity), setup uses the `managed`

mode.

The `managed`

mode provides the following advantages over the `standard`

:

- Identity assignment on the virtual machine scale set of a node pool can take up 40-60s. With cronjobs or applications that require access to the identity and can't tolerate the assignment delay, it's best to use
`managed`

mode as the identity is pre-assigned to the virtual machine scale set of the node pool. Either manually or using the[az aks pod-identity add](/en-us/cli/azure/aks/pod-identity#az-aks-pod-identity-add)command. - In
`standard`

mode, MIC requires write permissions on the virtual machine scale set used by the AKS cluster and`Managed Identity Operator`

permission on the user-assigned managed identities. When running in`managed mode`

, since there's no MIC, the role assignments aren't required.

Instead of manually defining credentials for pods, pod-managed identities request an access token in real time, using it to access only their assigned resources. In AKS, there are two components that handle the operations to allow pods to use managed identities:

**The Node Management Identity (NMI) server**is a pod that runs as a DaemonSet on each node in the AKS cluster. The NMI server listens for pod requests to Azure services.**The Azure Resource Provider**queries the Kubernetes API server and checks for an Azure identity mapping that corresponds to a pod.

When pods request a security token from Microsoft Entra ID to access to an Azure resource, network rules redirect the traffic to the NMI server.

The NMI server:

- Identifies pods requesting access to Azure resources based on their remote address.
- Queries the Azure Resource Provider.

The Azure Resource Provider checks for Azure identity mappings in the AKS cluster.

The NMI server requests an access token from Microsoft Entra ID based on the pod's identity mapping.

Microsoft Entra ID provides access to the NMI server, which is returned to the pod.

- This access token can be used by the pod to then request access to resources in Azure.


In the following example, a developer creates a pod that uses a managed identity to request access to Azure SQL Database:

- Cluster operator creates a service account to map identities when pods request access to resources.
- The NMI server is deployed to relay any pod requests, along with the Azure Resource Provider, for access tokens to Microsoft Entra ID.
- A developer deploys a pod with a managed identity that requests an access token through the NMI server.
- The token is returned to the pod and used to access Azure SQL Database

To use Pod-managed identities, see [Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (preview)](use-azure-ad-pod-identity).

## Next steps

This best practices article focused on authentication and authorization for your cluster and resources. To implement some of these best practices, see the following articles:

[Integrate Microsoft Entra ID with AKS](enable-authentication-microsoft-entra-id)[Use Microsoft Entra pod-managed identities in Azure Kubernetes Service (preview)](use-azure-ad-pod-identity)

For more information about cluster operations in AKS, see the following best practices:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-configure-container-network-metrics-filtering -->

# Configure container network metrics filtering for Azure Kubernetes Service (AKS) (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure container network metrics filtering for Azure Kubernetes Service (AKS) with Cilium to optimize data collection, reduce storage costs, and focus on the metrics most relevant to your monitoring needs.

Configure container network metrics filtering enables dynamic management of Hubble metrics cardinality through Kubernetes Custom Resource Definitions (CRDs). This feature allows you to dynamically control the cardinality, dimensions, and targets of Hubble metrics without restarting Cilium agents or Prometheus servers.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of the Azure CLI required to complete the steps in this article is

**2.73.0**. To find your version, run`az --version`

in the Azure CLI. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).An AKS cluster with Cilium data plane and

[Advanced Container Networking Services](advanced-container-networking-services-overview)enabled.Kubernetes version 1.32 or later.

Container network metrics filtering works specifically with Cilium data planes.

The minimum version of the

`aks-preview`

Azure CLI extension to complete the steps in this article is`18.0.0b2`

.

### Install the aks-preview Azure CLI extension

Install or update the Azure CLI preview extension by using the [ az extension add](/en-us/cli/azure/extension#az_extension_add) or

[command.](/en-us/cli/azure/extension#az_extension_update)

`az extension update`

```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the AdvancedNetworkingDynamicMetricsPreview feature flag

- First, register the AdvancedNetworkingDynamicMetricsPreview feature flag by using the
command:`az feature register`


```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
```


- Verify successful registration by using the
command. It takes a few minutes for registration to complete.`az feature show`


```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
```


- When the feature shows
**Registered**, refresh the registration of the`Microsoft.ContainerService`

resource provider by using thecommand.`az provider register`


```
az provider register --namespace Microsoft.ContainerService
```


### Create a new AKS cluster with Cilium

If you already have an existing cluster, you can skip this step.

Use the `az aks create`

command with the `--enable-acns`

flag to create a new AKS cluster that has all Advanced Container Networking Services features. These features include:

**Container Network Observability:**Provides insight into your network traffic. To learn more, see[Container Network Observability](advanced-container-networking-services-overview#container-network-observability).**Container Network Security:**Offers security features like FQDN filtering. To learn more, see[Container Network Security](advanced-container-networking-services-overview#container-network-security).

```
# Set environment variables
export RESOURCE_GROUP="cnm-testing-rg"
export CLUSTER_NAME="cnm-cilium-cluster"
export LOCATION="eastus2euap" # Use canary region for preview features
# Create resource group
az group create --name $RESOURCE_GROUP --location $LOCATION
# Create AKS cluster with Cilium and ACNS enabled
az aks create \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--location $LOCATION \
--network-plugin azure \
--network-dataplane cilium \
--enable-acns \
--enable-managed-identity \
--generate-ssh-keys \
--kubernetes-version 1.32
```


### Get cluster credentials

Get your cluster credentials by using the [ az aks get-credentials](/en-us/cli/azure/aks#az_aks_get_credentials) command:

```
az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --overwrite-existing
```


## Configure custom resources for metrics filtering

Container network metrics filtering uses the `ContainerNetworkMetric`

Custom Resource Definition (CRD) to define filtering rules. Only one CRD can exist per cluster, and changes take approximately 30 seconds to reconcile. If the CRD is not applied, all metrics will be collected.

```
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: : container-network-metric # Cluster scoped
spec:
filters:
- metric: flow
includeFilters: # List of include filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
matchExpressions:
- key: environment
operator: In
values:
- production
- staging
ip: # List of source IPs; can be CIDR
- "192.168.1.10"
- "10.0.0.1"
to:
namespacedPod:
- sample-namespace2/sample-pod2
labelSelector:
matchLabels:
app: backend
k8s.io/namespace: sample-namespace2
matchExpressions:
- key: tier
operator: NotIn
values:
- dev
ip:
- "192.168.1.20"
- "10.0.1.1"
protocol: # List of protocols; can be tcp, udp, dns
- tcp
- udp
- dns
verdict: # List of verdicts; can be forwarded, dropped
- forwarded
- dropped
metric: dns
excludeFilters: # List of exclude filters
- name: sample-filter # Filter name
from:
namespacedPod: # List of source namespace/pods. Prepend namespace with /
- sample-namespace/sample-pod
labelSelector: # Standard k8s label selector
matchLabels:
app: frontend
k8s.io/namespace: sample-namespace
```


The following table describes the fields in the custom resource definition:

| Field | Type | Description | Required |
|---|---|---|---|
`filters.metric` |
String | Name of the metric you would like to apply the filter on. This is mandatory. The supported values are `dns` , `flow` , `tcp` , `drop` |
Mandatory |
`includeFilters` or `excludeFilters` |
[]filter | A list of filters that define network flows to include. Each filter specifies the source, destination, protocol, and other matching criteria. You must have at least one include or exclude filter. | Mandatory |
`filters.name` |
String | The name of the filter. | Optional |
`filters.protocol` |
[]string | The protocols to match for this filter. Valid values are `tcp` , `udp` , and `dns` . Because it's an optional parameter, if it isn't specified, logs with all protocols are included. |
Optional |
`filters.verdict` |
[]string | The verdict of the flow to match. Valid values are `forwarded` and `dropped` . Because it's an optional parameter, if it isn't specified, logs with all verdicts are included. |
Optional |
`filters.from` |
Endpoint | Specifies the source of the network flow. Can include IP addresses, label selectors, and namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector is a mechanism to filter and query resources based on labels, so you can identify specific subsets of resources. A label selector can include two components: `matchLabels` and `matchExpressions` . Use `matchLabels` for straightforward matching by specifying a key/value pair (for example, `{"app": "frontend"}` ). For more advanced criteria, use `matchExpressions` , where you define a label key, an operator (such as `In` , `NotIn` , `Exists` , or `DoesNotExist` ), and an optional list of values. Ensure that the conditions in both `matchLabels` and `matchExpressions` are met, because they're logically combined by `AND` . If no conditions are specified, the selector matches all resources. To match none, leave the selector null. Carefully define your label selector to target the correct set of resources. |
Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) for matching the source. `name` should match the RegEx pattern `^.+$` . |
Optional |
`filters.to` |
Endpoint | Specifies the destination of the network flow. Can include IP addresses, label selectors, or namespace/pod pairs. | Optional |
`Endpoint.ip` |
[]string | It can be a single IP or a CIDR. | Optional |
`Endpoint.labelSelector` |
Object | A label selector to match resources based on their labels. | Optional |
`Endpoint.namespacedPod` |
[]string | A list of namespace and pod pairs (formatted as `namespace/pod` ) to match the destination. |
Optional |

Apply the `ContainerNetworkMetric`

custom resource to enable log collection at the cluster:

```
kubectl apply -f <crd.yaml>
```


## Clean up and reset

To clean up filtering configuration:

```
# Delete the CRD
kubectl delete ContainerNetworkMetric container-network-metric
```


## Example filtering configuration

- Create a basic filtering configuration that focuses on DNS metrics:

```
# basic-dns-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: dns # Supported: dns, flow, tcp, drop
excludeFilters:
- from:
namespacedPod: ["kube-system/coredns"]
```


- Configure filtering for TCP metrics with include and exclude filters:

```
# tcp-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: tcp
includeFilters:
- from:
labelSelector:
matchLabels:
tier: "frontend"
excludeFilters:
- to:
namespacedPod: ["kube-system/metrics-server"]
```


- Configure filtering for network flow metrics:

```
# flow-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: flow
includeFilters:
- from:
labelSelector:
matchLabels:
tier: "frontend"
- to:
labelSelector:
matchLabels:
tier: "backend"
excludeFilters:
- from:
namespacedPod: ["default/test"]
```


- Configure filtering for dropped packet metrics:

```
# drop-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: drop
excludeFilters:
- from:
namespacedPod: ["kube-system/"]
```


- Configure filtering for multiple metric types in a single CRD:

```
# multi-metrics-filter.yaml
apiVersion: acn.azure.com/v1alpha1
kind: ContainerNetworkMetric
metadata:
name: container-network-metric
spec:
filters:
- metric: dns
includeFilters:
- protocol: ["dns"]
excludeFilters:
- from:
namespacedPod: ["kube-system/*"]
- metric: tcp
includeFilters:
- protocol: ["tcp"]
- from:
labelSelector:
matchLabels:
environment: "production"
- metric: flow
excludeFilters:
- from:
namespacedPod: ["default/debug-*"]
- metric: drop
includeFilters:
- reason: ["Policy denied", "Invalid"]
```


## Best practices

Ensure you do not have conflicting include and exclude filter on the CRD.

Leverage Kubernetes label selectors for flexible filtering.

Always validate filtering configurations in development or staging

Regularly review filtered metrics to ensure important data isn't lost.

Remember that only one CRD can exist per cluster.


## Troubleshooting

### Common issues

**Issue**: CRD configuration not applied

**Solution**: Check that the feature flag is registered and only one CRD exists:

```
# Verify feature registration
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingDynamicMetricsPreview"
# Check existing CRDs
kubectl get ContainerNetworkMetric
```


**Issue**: Metrics still showing after applying excludeFilters

**Solution**: Remember that preexisting metrics persist in Prometheus. You may need to wait for new metrics to be generated to see the filtering effects.

## Limitations

- This feature is specifically designed for Cilium data planes only
- Only one
`ContainerNetworkMetric`

CRD can exist per cluster - Preexisting metrics persist in Prometheus; new filtering rules apply to newly generated metrics
- Requires Kubernetes version 1.32 or later

## Related content

- To learn about container network metrics capabilities, see
[Container network metrics overview](container-network-observability-metrics). - To create an AKS cluster with Advanced Container Networking Services, see
[Set up Container Network Observability for AKS](container-network-observability-how-to). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-l7-policy-concepts -->

# Overview of Layer 7 (L7) policy

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Network policies are essential for securing Kubernetes clusters by defining and controlling pod communication. They mitigate unauthorized access and potential security breaches by regulating traffic flow. Advanced Container Networking Services strengthens security with [FQDN-based network policies](container-network-security-fqdn-filtering-concepts). Expanding on this foundation, Advanced Container Networking Services now provides L7 policy support, enabling detailed inspection and management of application-level traffic. This advancement enhances both the security and efficiency of network communications within AKS clusters. The offering includes comprehensive support for widely adopted protocols, including HTTP, gRPC, and Kafka.

## Components of L7 policy

**Envoy proxy**: Envoy, part of ACNS security agent acts as the enforcement point for L7 policies. A TPROXY inspects application traffic, comparing it against the defined L7 policies. To enhance scalability and resource management, Envoy is deployed as a separate DaemonSet, decoupled from the Cilium Agent.

## How L7 policy works

When L7 policy enforcement is enabled for an application or pod, outgoing network traffic is first evaluated to determine compliance with the configured application-level rules. The eBPF probe attached to the source pod’s network interface marks the packets, which are then redirected to a node-local Envoy Proxy. This redirection occurs only for pods enforcing L7 policies, ensuring that policy enforcement is applied selectively.

The Envoy proxy, augmented with Cilium network filters, then decides whether to forward the traffic to the destination pod based on policy criteria. If permitted, the traffic proceeds; if not, Envoy returns an appropriate error code to the originating pod. Upon successful authorization, the Envoy proxy facilitates the traffic flow, providing application-level visibility and control. This allows the Cilium agent to enforce detailed network policies within the policy engine. The following diagram illustrates the high-level flow of L7 policy enforcement.

## Monitoring L7 traffic with Hubble and Grafana

To gain insights into L7 traffic flows, specifically HTTP, gRPC, and Kafka, Azure CNI Powered by Cilium leverages Hubble agent, which is enabled by default with Advanced Container Networking Services. Hubble provides detailed flow-level metrics.

To simplify the analysis of these L7 metrics, we provide pre-configured Azure Managed Grafana dashboards. You can find them under the **Dashboards > Azure Managed Prometheus** folder, with filenames like **"Kubernetes/Networking/L7 (Namespace)"** and **"Kubernetes/Networking/L7 (Workload)"**.

These dashboards offer granular visibility into L7 flow data at the cluster, namespace, and workload levels.

Note

These dashboards will only display data if you have this feature enabled on your cluster and have relevant policies applied.
Additionally, the monitoring metrics are **not** required to flow through Envoy, a component of the ACNS security agent. Rather, these metrics are collected by the Hubble agent, which is installed on your cluster as part of the Advanced Container Networking Service's observability feature.

## Key benefits

**Granular Application-Level Control**: L7 policies allow for fine-grained control over network traffic based on application-specific attributes, such as HTTP methods, gRPC paths, and Kafka topics. This extends beyond the basic IP address and port-based control of traditional network policies.

**Enhanced Security**: By inspecting application-level traffic, L7 policies can prevent attacks that exploit vulnerabilities at the application layer. This includes blocking unauthorized access to specific APIs or services. Furthermore, L7 policies are an important component of a Zero Trust security strategy, enabling the enforcement of the principle of least privilege at the application layer.

**Graceful Error Handling**: Unlike L3/L4 policies that typically drop unauthorized traffic silently, L7 policies can return application-level error codes (for example, HTTP 403, Kafka authorization failures), allowing applications to handle errors more gracefully.

**Observability**: With observability enabled for Advanced Container Networking Services and L7 policies applied to your AKS cluster, you can monitor traffic and policy effectiveness using Grafana dashboards.

## Limitations and considerations

- Current feature support relies on Cilium's Layer 7 policy enforcement based on HTTP, HTTPS, gRPC, and Kafka.
- The maximum supported cluster size is up to 1,000 nodes or 40,000 pods, whichever is greater.
- Traffic traversing Envoy proxies do come with latency. Users may experience noticeable latency degradation beyond 3,000 requests per second.
- As part of our observability solution, we provide envoy_http_rq_total metrics. These metrics give the total request count, which could be used to derive requests per seconds (rps).
- During a Cilium upgrade or rollout, existing sessions can be gracefully closed. Applications are expected to handle these interruptions gracefully—typically by implementing retry mechanisms at the connection or request level. New connections initiated during the rollout aren't impacted.
- L7 policy isn't supported by CiliumClusterwideNetworkPolicy(CCNP).
- L7 policy through Advanced Container Networking Services (ACNS) isn't compatible with L7 policies implemented via alternate methods such as Istio. The following table summarizes the supported scenarios.

| Feature/Component | L7 Policies using AKS, Istio - Managed addon |
|---|---|
| K8s network policies by Azure CNI powered by Cilium | Supported |
| L4 (FQDN) Policies by Azure CNI powered by Cilium and ACNS | Supported |
| L7 (HTTP(s)/GRPC/Kafka) Policies by Azure CNI powered by Cilium and ACNS | Not Supported |

## Pricing

Important

Advanced Container Networking Services is a paid offering. For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Next steps

Learn how to apply

[L7 policies](how-to-apply-l7-policies)on AKS.Explore how the open source community builds

[Cilium Network Policies](https://docs.cilium.io/en/latest/security/policy/).For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see

[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).Explore Container Network Observability features in Advanced Container Networking Services in

[What is Container Network Observability?](advanced-container-networking-services-overview#container-network-observability)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-paas-services -->

# Tutorial - Use PaaS services with an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

With Kubernetes, you can use PaaS services, such as [Azure Service Bus](/en-us/azure/service-bus-messaging/service-bus-messaging-overview), to develop and run your applications.

In this tutorial, you create an Azure Service Bus namespace and queue to test your application. You learn how to:

- Create an Azure Service Bus namespace and queue.
- Update the Kubernetes manifest file to use the Azure Service Bus queue.
- Test the updated application by placing an order.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created a Kubernetes cluster, and deployed an application. To complete this tutorial, you need the pre-created `aks-store-quickstart.yaml`

Kubernetes manifest file. This file download was included with the application source code in a previous tutorial. Make sure you cloned the repo and changed directories into the cloned repo. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create environment variables

Create the following environment variables to use for the commands in this tutorial:

`LOC_NAME=westus2 RAND=$RANDOM RG_NAME=myResourceGroup AKS_NAME=myAKSCluster SB_NS=sb-store-demo-$RAND`


## Create Azure Service Bus namespace and queue

In previous tutorials, you used a RabbitMQ container to store orders submitted by the `order-service`

. In this tutorial, you use an Azure Service Bus namespace to provide a scoping container for the Service Bus resources within the application. You also use an Azure Service bus queue to send and receive messages between the application components. For more information on Azure Service Bus, see [Create an Azure Service Bus namespace and queue](/en-us/azure/service-bus-messaging/service-bus-quickstart-cli).

Create an Azure Service Bus namespace using the

command.`az servicebus namespace create`

`az servicebus namespace create --name $SB_NS --resource-group $RG_NAME --location $LOC_NAME`

Create an Azure Service Bus queue using the

command.`az servicebus queue create`

`az servicebus queue create --name orders --resource-group $RG_NAME --namespace-name $SB_NS`

Create an Azure Service Bus authorization rule using the

command.`az servicebus queue authorization-rule create`

`az servicebus queue authorization-rule create \ --name sender \ --namespace-name $SB_NS \ --resource-group $RG_NAME \ --queue-name orders \ --rights Send`

Get the Azure Service Bus credentials for later use by using the

and`az servicebus namespace show`

commands.`az servicebus queue authorization-rule keys list`

`az servicebus namespace show --name $SB_NS --resource-group $RG_NAME --query name -o tsv az servicebus queue authorization-rule keys list --namespace-name $SB_NS --resource-group $RG_NAME --queue-name orders --name sender --query primaryKey -o tsv`


## Update Kubernetes manifest file

Configure

`kubectl`

to connect to your cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Open the

`aks-store-quickstart.yaml`

file in a text editor.Remove the existing

`rabbitmq`

StatefulSet, ConfigMap, and Service sections and replace the existing`order-service`

Deployment section with the following content:`apiVersion: apps/v1 kind: Deployment metadata: name: order-service spec: replicas: 1 selector: matchLabels: app: order-service template: metadata: labels: app: order-service spec: nodeSelector: "kubernetes.io/os": linux containers: - name: order-service image: <REPLACE_WITH_YOUR_ACR_NAME>.azurecr.io/aks-store-demo/order-service:latest ports: - containerPort: 3000 env: - name: ORDER_QUEUE_HOSTNAME value: "<REPLACE_WITH_YOUR_SB_NS_HOSTNAME>" # Example: sb-store-demo-123456.servicebus.windows.net - name: ORDER_QUEUE_PORT value: "5671" - name: ORDER_QUEUE_TRANSPORT value: "tls" - name: ORDER_QUEUE_USERNAME value: "sender" - name: ORDER_QUEUE_PASSWORD value: "<REPLACE_WITH_YOUR_SB_SENDER_PASSWORD>" - name: ORDER_QUEUE_NAME value: "orders" - name: FASTIFY_ADDRESS value: "0.0.0.0" resources: requests: cpu: 1m memory: 50Mi limits: cpu: 75m memory: 128Mi startupProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 20 periodSeconds: 10 readinessProbe: httpGet: path: /health port: 3000 failureThreshold: 3 initialDelaySeconds: 3 periodSeconds: 5 livenessProbe: httpGet: path: /health port: 3000 failureThreshold: 5 initialDelaySeconds: 3 periodSeconds: 3`

Note

Directly adding sensitive information, such as API keys, to your Kubernetes manifest files isn't secure and may accidentally get committed to code repositories. We added it here for simplicity. For production workloads, use

[Managed Identity](use-managed-identity)to authenticate with Azure Service Bus or store your secrets in[Azure Key Vault](csi-secrets-store-driver).Save and close the updated

`aks-store-quickstart.yaml`

file.

## Deploy the updated application

Deploy the updated application using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart.yaml`

The following example output shows the successfully updated resources:

`deployment.apps/order-service configured service/order-service unchanged deployment.apps/product-service unchanged service/product-service unchanged deployment.apps/store-front configured service/store-front unchanged`


## Test the application

### Place a sample order

Get the external IP address of the

`store-front`

service using the`kubectl get service`

command.`kubectl get service store-front`

Navigate to the external IP address of the

`store-front`

service in your browser using`http://<external-ip>`

.Place an order by choosing a product and selecting

**Add to cart**.Select

**Cart**to view your order, and then select**Checkout**.

### View the order in the Azure Service Bus queue

- Navigate to the Azure portal and open the Azure Service Bus namespace you created earlier.
- Under
**Entities**, select**Queues**, and then select the**orders**queue. - In the
**orders**queue, select**Service Bus Explorer**. - Select
**Peek from start**to view the order you submitted.

## Next steps

In this tutorial, you used Azure Service Bus to update and test the sample application. You learned how to:

- Create an Azure Service Bus namespace and queue.
- Update the Kubernetes manifest file to use the Azure Service Bus queue.
- Test the updated application by placing an order.

In the next tutorial, you learn how to scale an application in AKS.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/stateful-workload-upgrades -->

# Stateful workload upgrade patterns

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Upgrade clusters that run databases and stateful applications without data loss by using these proven patterns.

## What this article covers

This article provides database-specific upgrade patterns for Azure Kubernetes Service (AKS) clusters with stateful workloads, such as:

- PostgreSQL Ferris wheel pattern for ~30-second downtime.
- Redis rolling replacement for zero-downtime cache upgrades.
- MongoDB step-down cascades for replica set safety.
- Emergency upgrade checklists for security responses.
- Validation and rollback procedures for data protection.

These patterns are best for use by database administrators for applications with persistent data and mission-critical stateful services.

For more information, see these related articles:

- To upgrade your production AKS clusters, see
[AKS production upgrade strategies](aks-production-upgrade-strategies). - To check for and apply basic upgrades to your AKS cluster, see
[Upgrade an Azure Kubernetes Service cluster](upgrade-aks-cluster). - To use the scenario hub to help you choose the right AKS upgrade approach, see
[AKS upgrade scenarios: Choose your path](upgrade-scenarios-hub).

For a quick start, select a link for instructions:

[Do you need an emergency upgrade?](#emergency-upgrade-checklist)[Do you need help with a PostgreSQL cluster?](#the-ferris-wheel-pattern-postgresql)[Do you need a Redis cache rolling replace?](#redis-cluster-rolling-replace)

## Choose your pattern

| Database type | Upgrade pattern | Downtime | Complexity | Best for |
|---|---|---|---|---|
| PostgreSQL |
|

[Rolling replace](#redis-cluster-rolling-replace)[Step-down cascade](#mongodb-replica-set-step-down)*(coming soon)**(coming soon)*## Emergency upgrade checklist

Do you need to upgrade now because of security issues?

Run the following commands for an immediate safety check (two minutes):

`# Verify all replicas are healthy kubectl get pods -l tier=database -o wide # Check replication lag ./scripts/check-replica-health.sh # Ensure recent backup exists kubectl get job backup-job -o jsonpath='{.status.completionTime}'`

Choose an emergency pattern (one minute):

**PostgreSQL/MySQL:**Use[Ferris wheel](#the-ferris-wheel-pattern-postgresql)(30-second downtime).**Redis/Memcached:**Use[Rolling replace](#redis-cluster-rolling-replace)(zero downtime).**MongoDB/CouchDB:**Use[Step-down cascade](#mongodb-replica-set-step-down)(10-second downtime).

Run with a safety net (15-minute to 30-minute window):

- Always test rollback procedures in advance.
- Monitor application metrics during the upgrade.
- Keep the database team on standby.


## The Ferris wheel pattern: PostgreSQL

This pattern is best for 3-node PostgreSQL clusters with primary/replica setup across availability zones.

Visual pattern:

```
Initial: [PRIMARY] [REPLICA-1] [REPLICA-2]
Step 1: [PRIMARY] [REPLICA-1] [NEW-NODE] ← Add new node
Step 2: [REPLICA-1] [NEW-NODE] [REPLICA-2] ← Promote & remove old primary
Step 3: [NEW-PRIMARY] [NEW-NODE] [REPLICA-2] ← Complete rotation
```


### Quick implementation (20 minutes)

```
# 1. Add new node to cluster
kubectl scale statefulset postgres-cluster --replicas=4
# 2. Wait for new replica to sync
kubectl wait --for=condition=ready pod postgres-cluster-3 --timeout=300s
# 3. Promote new primary and failover (30-second downtime window)
kubectl exec postgres-cluster-3 -- pg_ctl promote -D /var/lib/postgresql/data
# 4. Update service endpoint
kubectl patch service postgres-primary --patch '{"spec":{"selector":{"app":"postgres-cluster","role":"primary","pod":"postgres-cluster-3"}}}'
# 5. Remove old primary node
kubectl delete pod postgres-cluster-0
```


**Detailed step-by-step guide**

#### Prerequisites validation

```
#!/bin/bash
# pre-upgrade-validation.sh
echo "=== PostgreSQL Cluster Health Check ==="
# Check replication status
kubectl exec postgres-primary-0 -- psql -c "SELECT * FROM pg_stat_replication;"
# Verify sync replication (must show 'sync' state)
SYNC_COUNT=$(kubectl exec postgres-primary-0 -- psql -t -c "SELECT count(*) FROM pg_stat_replication WHERE sync_state='sync';")
if [ "$SYNC_COUNT" -lt 2 ]; then
echo "ERROR: Need at least 2 synchronous replicas"
exit 1
fi
# Confirm recent backup exists
LAST_BACKUP=$(kubectl get job postgres-backup -o jsonpath='{.status.completionTime}')
echo "Last backup: $LAST_BACKUP"
# Test failover capability in staging first
echo "✅ Prerequisites validated"
```


#### Step 1: Scale up with a new node

```
# Add new node with upgraded Kubernetes version
kubectl patch statefulset postgres-cluster --patch '{
"spec": {
"replicas": 4,
"template": {
"spec": {
"nodeSelector": {
"kubernetes.io/arch": "amd64",
"aks-nodepool": "upgraded-pool"
}
}
}
}
}'
# Monitor new pod startup
kubectl get pods -l app=postgres-cluster -w
# Verify new replica joins cluster
kubectl exec postgres-cluster-3 -- psql -c "SELECT * FROM pg_stat_replication;"
```


#### Step 2: Run a controlled failover

```
#!/bin/bash
# controlled-failover.sh
echo "=== Starting Controlled Failover ==="
# Ensure minimal replication lag (< 0.1-second)
LAG=$(kubectl exec postgres-primary-0 -- psql -t -c "SELECT EXTRACT(EPOCH FROM now() - pg_last_xact_replay_timestamp());")
if (( $(echo "$LAG > 0.1" | bc -l) )); then
echo "ERROR: Replication lag too high ($LAG seconds)"
exit 1
fi
# Pause application writes (use connection pool drain)
kubectl patch configmap pgbouncer-config --patch '{"data":{"pgbouncer.ini":"[databases]\napp_db = host=postgres-primary port=5432 dbname=appdb pool_mode=statement max_db_connections=0"}}'
# Wait for active transactions to complete
sleep 10
# Promote new primary (this is the 30-second downtime window)
kubectl exec postgres-cluster-3 -- pg_ctl promote -D /var/lib/postgresql/data
# Update service selector to new primary
kubectl patch service postgres-primary --patch '{
"spec": {
"selector": {
"statefulset.kubernetes.io/pod-name": "postgres-cluster-3"
}
}
}'
# Resume application writes
kubectl patch configmap pgbouncer-config --patch '{"data":{"pgbouncer.ini":"[databases]\napp_db = host=postgres-primary port=5432 dbname=appdb pool_mode=statement"}}'
echo "✅ Failover completed"
```


#### Step 3: Clean up and validate

```
# Remove old primary node
kubectl delete pod postgres-cluster-0 --force
# Scale back to 3 replicas
kubectl patch statefulset postgres-cluster --patch '{"spec":{"replicas":3}}'
# Validate cluster health
kubectl exec postgres-cluster-3 -- psql -c "SELECT * FROM pg_stat_replication;"
# Test application connectivity
kubectl run test-db-connection --image=postgres:15 --rm -it -- psql -h postgres-primary -U app_user -d app_db -c "SELECT version();"
```


### Advanced configuration

For mission-critical databases that require a <10-second downtime:

```
# Use synchronous replication with multiple standbys
# postgresql.conf
synchronous_standby_names = 'ANY 2 (standby1, standby2, standby3)'
synchronous_commit = 'remote_apply'
```


### Success validation

To validate your progress, use the following checklist:

- New primary accepts reads and writes.
- All replicas show healthy replication.
- Application reconnects automatically.
- No data loss detected.
- Backup/restore tested on new primary.

### Emergency rollback

##### For immediate issues (<2 minutes)

Redirect traffic to the previous primary:

```
kubectl patch service postgres-primary --patch '{
"spec": {
"selector": {
"statefulset.kubernetes.io/pod-name": "postgres-cluster-1"
}
}
}'
```


##### For comprehensive failover recovery (5-10 minutes)

Stop writes to the current primary:

`kubectl exec postgres-primary-0 -- psql -c "SELECT pg_reload_conf();"`

Redirect service to a healthy replica:

`kubectl patch service postgres-primary --patch '{"spec":{"selector":{"statefulset.kubernetes.io/pod-name":"postgres-replica-1-0"}}}'`

Promote a replica to the new primary:

`kubectl exec postgres-replica-1-0 -- pg_ctl promote -D /var/lib/postgresql/data kubectl wait --for=condition=ready pod postgres-replica-1-0 --timeout=60s`

Update connection strings:

`kubectl patch configmap postgres-config --patch '{"data":{"primary-host":"postgres-replica-1-0.postgres"}}'`

Verify that the new primary accepts writes:

`kubectl exec postgres-replica-1-0 -- psql -c "CREATE TABLE upgrade_test (id serial, timestamp timestamp default now());" kubectl exec postgres-replica-1-0 -- psql -c "INSERT INTO upgrade_test DEFAULT VALUES;"`


**Expected outcome:** Approximately 30-second downtime, zero data loss, and an upgraded node that runs the current version of Kubernetes.

#### Step 3: Upgrade Node1 (former primary)

```
#!/bin/bash
# upgrade-node1.sh
echo "=== Step 3: Upgrade Node1 (Former Primary) ==="
# Drain Node1 gracefully
kubectl drain aks-nodepool1-12345678-vmss000000 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
# Trigger node upgrade
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Monitor upgrade progress
while kubectl get node aks-nodepool1-12345678-vmss000000 -o jsonpath='{.status.conditions[?(@.type=="Ready")].status}' | grep -q "False"; do
echo "Waiting for node upgrade to complete..."
sleep 30
done
echo "Node1 upgrade completed"
```


#### Step 4: Rejoin Node1 as a replica

```
#!/bin/bash
# rejoin-node1.sh
echo "=== Step 4: Rejoin Node1 as Replica ==="
# Wait for postgres pod to be scheduled on upgraded node
kubectl wait --for=condition=ready pod postgres-primary-0 --timeout=300s
# Reconfigure as replica pointing to new primary (Node2)
kubectl exec postgres-primary-0 -- bash -c "
echo 'standby_mode = on' >> /var/lib/postgresql/data/recovery.conf
echo 'primary_conninfo = \"host=postgres-replica-1-0.postgres port=5432\"' >> /var/lib/postgresql/data/recovery.conf
"
# Restart postgres to apply replica configuration
kubectl delete pod postgres-primary-0
kubectl wait --for=condition=ready pod postgres-primary-0 --timeout=120s
# Verify replication is working
kubectl exec postgres-replica-1-0 -- psql -c "SELECT * FROM pg_stat_replication WHERE application_name='postgres-primary-0';"
echo "Node1 successfully rejoined as replica"
```


#### Step 5: Upgrade Node3 (Replica-2)

```
#!/bin/bash
# upgrade-node3.sh
echo "=== Step 5: Upgrade Node3 (Replica-2) ==="
# Similar process for Node3
kubectl drain aks-nodepool1-12345678-vmss000002 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Wait for upgrade and pod readiness
kubectl wait --for=condition=ready pod postgres-replica-2-0 --timeout=300s
# Verify all replicas are in sync
kubectl exec postgres-replica-1-0 -- psql -c "SELECT application_name, state, sync_state FROM pg_stat_replication;"
```


#### Step 6: Final failover (Node2 → Node3)

```
#!/bin/bash
# final-failover.sh
echo "=== Step 6: Final Failover and Node2 Upgrade ==="
# Failover primary from Node2 to Node3
kubectl patch service postgres-primary --patch '{"spec":{"selector":{"statefulset.kubernetes.io/pod-name":"postgres-replica-2-0"}}}'
kubectl exec postgres-replica-2-0 -- pg_ctl promote -D /var/lib/postgresql/data
# Upgrade Node2
kubectl drain aks-nodepool1-12345678-vmss000001 --grace-period=300 --delete-emptydir-data --ignore-daemonsets
az aks nodepool upgrade \
--resource-group production-rg \
--cluster-name aks-prod \
--name nodepool1 \
--kubernetes-version 1.29.0 \
--max-surge 0 \
--max-unavailable 1
# Rejoin Node2 as replica
kubectl wait --for=condition=ready pod postgres-replica-1-0 --timeout=300s
echo "All nodes upgraded successfully. PostgreSQL cluster operational."
```


### Validation and monitoring

```
#!/bin/bash
# post-upgrade-validation.sh
echo "=== Post-Upgrade Validation ==="
# Verify cluster topology
kubectl get pods -l app=postgres -o wide
# Check all replicas are connected
kubectl exec postgres-replica-2-0 -- psql -c "SELECT application_name, client_addr, state FROM pg_stat_replication;"
# Validate data integrity
kubectl exec postgres-replica-2-0 -- psql -c "SELECT COUNT(*) FROM upgrade_test;"
# Performance validation
kubectl exec postgres-replica-2-0 -- psql -c "EXPLAIN ANALYZE SELECT * FROM pg_stat_activity;"
echo "Upgrade validation completed successfully"
```


## Redis cluster rolling replace

In this scenario, a six-node Redis cluster (three primaries and three replicas) requires zero downtime.

### Implementation

```
#!/bin/bash
# redis-cluster-upgrade.sh
echo "=== Redis Cluster Rolling Upgrade ==="
# Get cluster topology
kubectl exec redis-0 -- redis-cli cluster nodes
# Upgrade replica nodes first (no impact to writes)
for replica in redis-1 redis-3 redis-5; do
echo "Upgrading replica: $replica"
# Remove replica from cluster temporarily
REPLICA_ID=$(kubectl exec redis-0 -- redis-cli cluster nodes | grep $replica | cut -d' ' -f1)
kubectl exec redis-0 -- redis-cli cluster forget $REPLICA_ID
# Drain and upgrade node
kubectl delete pod $replica
kubectl wait --for=condition=ready pod $replica --timeout=120s
# Rejoin cluster
kubectl exec redis-0 -- redis-cli cluster meet $(kubectl get pod $replica -o jsonpath='{.status.podIP}') 6379
echo "Replica $replica upgraded and rejoined"
done
# Upgrade master nodes with failover
for master in redis-0 redis-2 redis-4; do
echo "Upgrading master: $master"
# Trigger failover to replica
kubectl exec $master -- redis-cli cluster failover
# Wait for failover completion
sleep 10
# Upgrade the demoted master (now replica)
kubectl delete pod $master
kubectl wait --for=condition=ready pod $master --timeout=120s
echo "Master $master upgraded"
done
echo "Redis cluster upgrade completed"
```


## MongoDB replica set step-down

In this scenario, a three-member MongoDB replica set requires coordinated primary step-down.

### Implementation

```
#!/bin/bash
# MongoDB upgrade script
Echo "=== MongoDB Replica Set Upgrade ==="
# Check replica set status
kubectl exec mongo-0 --mongo --eval "rs.status()"
```

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-observability-logs -->

# What is container network logs (preview)?

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Component renaming (starting November 11, 2025)

We are renaming components in the Container Network Logs feature to improve clarity and consistency:

What's changing

**CRD**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`

**CLI flag**:`--enable-retinanetworkflowlog`

→`--enable-container-network-logs`

**Log Analytics table**:`RetinaNetworkFlowLogs`

→`ContainerNetworkLog`


Action items for existing users to enable new naming

**Update Azure CLI**(MUST - First step!):`az upgrade`

**Update Preview CLI Extension**(MUST):`az extension update --name aks-preview`

**Disable Monitoring**:`az aks disable-addons -a monitoring -n <cluster-name> -g <resource-group>`

**Re-enable Monitoring**:`az aks enable-addons -a monitoring --enable-high-log-scale-mode -g <resource-group> -n <cluster-name>`

**Re-enable ACNS Container Network Logs**:`az aks update --enable-acns --enable-container-network-logs -g <resource-group> -n <cluster-name>`

**Apply new ContainerNetworkLog CRD**: Apply your updated CRD configuration with the new naming.**Reimport Grafana Dashboards**: Import the updated dashboards to reflect the new table names.

Note

- Previously collected data stays in your workspace in old table RetinaNetworkFlowLogs.
- After re-enabling, allow a short delay before new data appears in new table ContainerNetworkLog.

Container network logs in [Advanced Container Networking Services](advanced-container-networking-services-overview) for Azure Kubernetes Service (AKS) provide comprehensive, context-rich visibility into every network flow within your cluster. While metrics tell you *what* is happening in your network (such as bandwidth usage or error rates), container network logs tell you *why* by capturing the complete story of each connection—including who initiated it, what protocols were used, and whether the traffic was allowed or blocked.

These logs capture essential metadata for every network flow, including source and destination IP addresses, pod and service names, namespaces, ports, protocols, traffic direction, and policy verdicts. This deep contextual information enables you to correlate network behavior with specific workloads, troubleshoot connectivity issues, validate security policies, and perform forensic analysis.

Container network logs capture Layer 3 (IP), Layer 4 (TCP/UDP), and Layer 7 (HTTP/gRPC/Kafka) traffic, providing the detailed insights you need to monitor connectivity, troubleshoot issues, visualize network topology, enforce security policies, and ensure compliance.

Choose from two modes:

- Stored logs
- On-demand logs

## Stored logs

Stored logs mode ensures continuous log generation and collection in the AKS cluster when you enable Advanced Container Networking Services and set up custom filters. By default, log collection is disabled.

To enable log collection, you define *custom resources* to specify the types of traffic to monitor. Examples include namespaces, pods, services, and protocols. This feature remains active until you disable it.

Stored logs mode supports extended log retention and traffic filtering. For reduced storage costs and easier analysis, you can collect and retain only the logs that are relevant to you.

### How stored logs mode works

Advanced Container Networking Services uses eBPF technology with Cilium to fetch logs from nodes in your cluster. To start collecting logs, you define one or more custom resources to specify the types of traffic to monitor.

Custom resources provide fine-grained control to define and capture the traffic that is relevant to you. The Cilium agent running on each node collects network traffic that matches the criteria set in the custom resources. The logs are stored in JSON format on the host, providing a structured and accessible format for further use.

Alternatively, if the Azure Monitoring add-on is enabled, agents for Container insights collect the logs from the host, apply the default throttling limits, and send them to a Log Analytics workspace. The system aggregates and stores logs efficiently to provide visibility into network traffic for monitoring, troubleshooting, and security enforcement.

To read more about throttling and Container insights, see the [Container insights documentation](https://aka.ms/ContainerNetworkLogsDoc_CI).

### Key capabilities of stored logs mode

*Customizable filters.*You can configure logging by defining custom resources of the[ContainerNetworkLog](how-to-configure-container-network-logs#containernetworklog-crd-template)type. Use custom resources to apply granular filters by namespace, pod, service, port, protocol, verdict, or traffic direction (ingress or egress). This flexibility ensures precise data collection tailored to specific use cases. Only relevant traffic is logged, and storage is optimized for improved performance, compliance, and troubleshooting.*Log storage options.*The container network logs feature has two primary storage options: unmanaged storage and managed storage.**Unmanaged storage:**When a custom resource is applied to begin log collection, network flow logs are stored locally on the host nodes at the`/var/log/acns/hubble`

fixed mount location. This storage location is temporary because the node itself isn't a persistent storage solution. When the log files reach a size of 50 MB, they're automatically rotated and older logs are overwritten. This storage solution is suitable for real-time monitoring, but it doesn't support long-term storage or retention.For additional log management capabilities, you can integrate partner logging services like an OpenTelemetry collector. Partner integrations provide flexibility to manage logs outside the Azure ecosystem and are useful if you've already deployed a specific log management platform.

**Managed storage:**For long-term retention and advanced analytics, we recommend that you configure Azure monitoring in your AKS cluster to collect and store logs in a Log Analytics workspace. This setup ensures secure and compliant log storage. It also provides access to powerful capabilities like anomaly detection, performance tuning, and historical data analysis. You can use historical logs to identify trends, baseline behaviors, and proactively address recurring issues.For example, you can use the managed service for Prometheus to configure alerts on both metrics and logs for real-time monitoring and rapid detection of outliers.

You use the same workspace for log storage. You set up log storage space during onboarding. Both Analytics and Basic log table plans are supported for this feature. For more detailed information on table plans, see

[Azure Monitor Logs](/en-us/azure/azure-monitor/logs/data-platform-logs).

*Simple visualization in Log Analytics and Grafana dashboards.*Logs and data presented in Grafana dashboards simplify complex information, facilitate data comprehension, and help you make decisions more quickly.

### Logs visualization in the Azure portal

You can visualize, query, and analyze flow logs in the Azure portal in the Log Analytics workspace for your cluster.

### Logs visualization in Grafana dashboards

Access the flow logs in an Azure Managed Grafana instance.

To simplify your analysis of logs, we provide two preconfigured Grafana dashboards:

Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs**. This dashboard shows which AKS workloads are communicating with each other, including network requests, responses, drops, and errors. Currently, as an interim step during preview, you must import Grafana dashboards by using a user ID to view the flow logs dashboard in the Azure portal.Go to

**Azure**>**Insights**>**Containers**>**Networking**>**Flow Logs (External Traffic)**. This dashboard shows which AKS workloads send and receive communications from outside an AKS cluster, including network requests, responses, drops, and errors.For more information, see

[Set up Azure Managed Grafana with Advanced Container Networking Services](how-to-configure-container-network-logs#visualization-in-grafana-dashboards).

Access the flow logs in the Azure portal via the

**Dashboards with Grafana**option.

The Azure portal dashboards have the following major components:

*A comprehensive overview of network health.*You see key metrics like total flow logs, unique requests, dropped requests, and forwarded requests for quick anomaly detection and efficient troubleshooting. The dashboard categorizes statistics by protocol and behavior, including DNS dropped requests, HTTP 2xx responses, Layer 4 request and response rates, and dropped request counts. A service dependency graph visualizes application or cluster interactions, highlighting traffic flow, bottlenecks, and dependencies for performance optimization.*Flow logs and error logs for quick analysis.*You can filter flow logs for root-cause analysis. For example, to troubleshoot Domain Name System (DNS) issues, filter error logs by the DNS protocol.Separating flow logs and error logs helps you analyze issues more quickly. You can identify and address errors without sifting through unrelated information, which improves efficiency in troubleshooting and debugging processes.

Use clear labels and timestamps for each log entry to more easily pinpoint specific events or errors in your systems or processes.

*Top namespaces, workloads, and DNS errors.*Network flow log visualization is vital for monitoring and analyzing communication in an AKS cluster. It provides insight into namespaces, workloads, port usage, and query usage. It helps you identify trends, detect bottlenecks, and diagnose issues. Spot significant network activity, view dropped requests, and assess protocol distribution (for example, TCP versus UDP). This overview section of the dashboard supports cluster health, resource optimization, and security by detecting and displaying unusual traffic patterns.

## On-demand logs

Advanced Container Networking Services offers on-demand capture of network flow logs. Get real-time visibility without prior configuration or persistent storage by using the Hubble CLI and the Hubble UI. This on-demand logs mode is available. To learn how to set up on-demand log storage, see [Configure the Hubble CLI and Hubble UI](how-to-configure-container-network-logs#configure-on-demand-logs-mode).

### Hubble CLI

The Hubble command-line interface (CLI) provides a flexible and interactive way to query, filter, and analyze flow logs directly in the terminal. You can execute real-time commands to inspect traffic flows, view packet metadata, and troubleshoot network issues without leaving your operational environment.

### Hubble UI

The Hubble web-based interface offers an intuitive and visual platform for monitoring. With features like live traffic dashboards, flow summaries, and searchable logs, you can easily track service-to-service communication, detect anomalies, and gain insights into cluster activity.

The Hubble UI tools provide real-time visibility and actionable insights for faster troubleshooting and improved network management.

### Key benefits of on-demand logs

*Faster issue resolution.*With detailed and actionable insights into network traffic, you can identify and resolve connectivity or performance issues more quickly, minimizing downtime and disruptions.*Optimized operational efficiency.*Aggregated and efficiently stored logs reduce data management overhead. Your team can focus on analysis and decision-making instead of managing large volumes of raw data.*Enhanced application reliability.*By monitoring service-to-service communication and detecting anomalies, you can proactively address potential issues and ensure a smoother and more reliable application experience.*Improved decision-making.*Visualizing network patterns in Azure Managed Grafana and applying service maps provide clear insights into your application's network behavior. This leads to improved infrastructure planning and optimization.*Cost savings.*Efficient log aggregation and customizable logging scopes reduce storage and data ingestion costs, providing a cost-effective solution for long-term network monitoring.*Streamlined compliance and security.*Persistent and comprehensive logs support audit trails, regulatory compliance, and quick identification of suspicious traffic. They help you maintain a secure and compliant environment.

## Limitations

- Container network logs in stored logs mode currently works only with the Cilium data plane.
- Layer 7 flow logs are captured only when Layer 7 policy support is enabled. For more information, see
[Configure a Layer 7 policy](how-to-apply-l7-policies). - DNS flows and metrics are captured only when a Cilium Fully Qualified Domain (FQDN) network policy is applied. For more information, see
[Configure an FQDN policy](how-to-apply-fqdn-filtering-policies). - Onboarding by using Terraform currently isn't supported.
- When Log Analytics isn't configured for log storage, container network logs are limited to a maximum of 50 MB of storage. When this limit is reached, new entries overwrite older logs.
- If the table plan is set to Basic logs, prebuilt Grafana dashboards don't work.
- The Auxiliary logs table plan isn't supported.

## Pricing

Important

Advanced Container Networking Services is a paid offering.

For more information about pricing, see [Advanced Container Networking Services - Pricing](https://azure.microsoft.com/pricing/details/azure-container-networking-services/).

## Related content

- Learn how to set up
[container network logs](how-to-configure-container-network-logs). - Get more information about
[Advanced Container Networking Services for AKS](advanced-container-networking-services-overview). - Explore the
[Container Network Observability feature](advanced-container-networking-services-overview#container-network-observability)in Advanced Container Networking Services. - Explore the
[Container Network Security feature](advanced-container-networking-services-overview#container-network-security)in Advanced Container Networking Services.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/vertical-pod-autoscaler-api-reference -->

# Vertical Pod Autoscaler API reference

This article provides the API reference for the Vertical Pod Autoscaler feature of Azure Kubernetes Service.

This reference is based on version 0.13.0 of the AKS implementation of VPA.

## VerticalPodAutoscaler

| Name |
Object |
Description |
| metadata |
ObjectMeta |
Standard [object metadata](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#metadata). |
| spec |
VerticalPodAutoscalerSpec |
The desired behavior of the Vertical Pod Autoscaler. |
| status |
VerticalPodAutoscalerStatus |
The most recently observed status of the Vertical Pod Autoscaler. |

## VerticalPodAutoscalerSpec

| Name |
Object |
Description |
| targetRef |
CrossVersionObjectReference |
Reference to the controller managing the set of pods for the autoscaler to control. For example, a Deployment or a StatefulSet. You can point a Vertical Pod Autoscaler at any controller that has a [Scale](https://v1-25.docs.kubernetes.io/docs/reference/generated/kubernetes-api/v1.25/#scalespec-v1-autoscaling) subresource. Typically, the Vertical Pod Autoscaler retrieves the pod set from the controller's ScaleStatus. |
| updatePolicy |
PodUpdatePolicy |
Specifies whether recommended updates are applied when a pod is started and whether recommended updates are applied during the life of a pod. |
| resourcePolicy |
PodResourcePolicy |
Specifies policies for how CPU and memory requests are adjusted for individual containers. The resource policy can be used to set constraints on the recommendations for individual containers. If not specified, the autoscaler computes recommended resources for all containers in the pod, without additional constraints. |
| recommenders |
VerticalPodAutoscalerRecommenderSelector |
Recommender is responsible for generating recommendation for the VPA object. Leave empty to use the default recommender. Otherwise the list can contain exactly one entry for a user-provided alternative recommender. |

## VerticalPodAutoscalerList

| Name |
Object |
Description |
| metadata |
ObjectMeta |
Standard [object metadata](https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md#metadata). |
| items |
VerticalPodAutoscaler (array) |
A list of Vertical Pod Autoscaler objects. |

## PodUpdatePolicy

| Name |
Object |
Description |
| updateMode |
string |
A string that specifies whether recommended updates are applied when a pod is started and whether recommended updates are applied during the life of a pod. Possible values are `Off` , `Initial` , `Recreate` , and `Auto` . The default is `Auto` if you don't specify a value. |
| minReplicas |
int32 |
A value representing the minimal number of replicas which need to be alive for Updater to attempt pod eviction (pending other checks like Pod Disruption Budget). Only positive values are allowed. Defaults to global `--min-replicas` flag, which is set to `2` . |

## PodResourcePolicy

| Name |
Object |
Description |
| conainerPolicies |
ContainerResourcePolicy |
An array of resource policies for individual containers. There can be at most one entry for every named container, and optionally a single wildcard entry with `containerName = '*'` , which handles all containers that do not have individual policies. |

## ContainerResourcePolicy

| Name |
Object |
Description |
| containerName |
string |
A string that specifies the name of the container that the policy applies to. If not specified, the policy serves as the default policy. |
| mode |
ContainerScalingMode |
Specifies whether recommended updates are applied to the container when it is started and whether recommended updates are applied during the life of the container. Possible values are `Off` and `Auto` . The default is `Auto` if you don't specify a value. |
| minAllowed |
ResourceList |
Specifies the minimum CPU request and memory request allowed for the container. By default, there is no minimum applied. |
| maxAllowed |
ResourceList |
Specifies the maximum CPU request and memory request allowed for the container. By default, there is no maximum applied. |
| ControlledResources |
[]ResourceName |
Specifies the type of recommendations that are computed (and possibly applied) by the Vertical Pod Autoscaler. If empty, the default of [ResourceCPU, ResourceMemory] is used. |

## VerticalPodAutoscalerRecommenderSelector

| Name |
Object |
Description |
| name |
string |
A string that specifies the name of the recommender responsible for generating recommendation for this object. |

## VerticalPodAutoscalerStatus

| Name |
Object |
Description |
| recommendation |
RecommendedPodResources |
The most recently recommended CPU and memory requests. |
| conditions |
VerticalPodAutoscalerCondition |
An array that describes the current state of the Vertical Pod Autoscaler. |

## RecommendedPodResources

| Name |
Object |
Description |
| containerRecommendation |
RecommendedContainerResources |
An array of resources recommendations for individual containers. |

## RecommendedContainerResources

| Name |
Object |
Description |
| containerName |
string |
A string that specifies the name of the container that the recommendation applies to. |
| target |
ResourceList |
The recommended CPU request and memory request for the container. |
| lowerBound |
ResourceList |
The minimum recommended CPU request and memory request for the container. This amount is not guaranteed to be sufficient for the application to be stable. Running with smaller CPU and memory requests is likely to have a significant impact on performance or availability. |
| upperBound |
ResourceList |
The maximum recommended CPU request and memory request for the container. CPU and memory requests higher than these values are likely to be wasted. |
| uncappedTarget |
ResourceList |
The most recent resource recommendation computed by the autoscaler, based on actual resource usage, not taking into account the **Container Resource Policy**. If actual resource usage causes the target to violate the **Container Resource Policy**, this might be different from the bounded recommendation. This field does not affect actual resource assignment. It is used only as a status indication. |

## VerticalPodAutoscalerCondition

| Name |
Object |
Description |
| type |
VerticalPodAutoscalerConditionType |
The type of condition being described. Possible values are `RecommendationProvided` , `LowConfidence` , `NoPodsMatched` , and `FetchingHistory` . |
| status |
ConditionStatus |
The status of the condition. Possible values are `True` , `False` , and `Unknown` . |
| lastTransitionTime |
Time |
The last time the condition made a transition from one status to another. |
| reason |
string |
The reason for the last transition from one status to another. |
| message |
string |
A human-readable string that gives details about the last transition from one status to another. |

## Next steps

See [Vertical Pod Autoscaler](vertical-pod-autoscaler) to understand how to improve cluster resource utilization and free up CPU and memory for other pods.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-node-auto-provisioning -->

# Enable or disable node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article explains how to enable or disable node auto-provisioning (NAP) in Azure Kubernetes Service (AKS) using the Azure CLI or Azure Resource Manager (ARM) templates.

If you want to create a NAP-enabled AKS cluster with a custom virtual network (VNet) and subnets, see [Create a node auto-provisioning (NAP) cluster in a custom virtual network](node-auto-provisioning-custom-vnet).

## Before you begin

Before you begin, review the [Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning) article, which details [how NAP works](node-auto-provisioning#how-does-node-auto-provisioning-work), [prerequisites](node-auto-provisioning#prerequisites) and [limitations](node-auto-provisioning#limitations-and-unsupported-features).

## Enable node auto-provisioning (NAP) on an AKS cluster

The following sections explain how to enable NAP on a new or existing AKS cluster:

Note

You can enable [control plane metrics](monitor-control-plane-metrics) to see the logs and operations from [node auto-provisioning](control-plane-metrics-default-list#minimal-ingestion-for-default-off-targets) with the [Azure Monitor managed service for Prometheus add-on](/en-us/azure/azure-monitor/essentials/prometheus-metrics-overview).

### Enable NAP on a new cluster

Enable node auto-provisioning on a new cluster using the

command with the`az aks create`

`--node-provisioning-mode`

flag set to`Auto`

. The following command also sets the`--network-plugin`

to`azure`

,`--network-plugin-mode`

to`overlay`

, and`--network-dataplane`

to`cilium`

.`az aks create \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --node-provisioning-mode Auto \ --network-plugin azure \ --network-plugin-mode overlay \ --network-dataplane cilium \ --generate-ssh-keys`


Create a file named

`nap.json`

and add the following ARM template configuration with the`properties.nodeProvisioningProfile.mode`

field set to`Auto`

, which enables NAP. (The default setting is`Manual`

.)`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#", "contentVersion": "1.0.0.0", "metadata": {}, "parameters": {}, "resources": [ { "type": "Microsoft.ContainerService/managedClusters", "apiVersion": "2025-05-01", "sku": { "name": "Base", "tier": "Standard" }, "name": "napcluster", "location": "uksouth", "identity": { "type": "SystemAssigned" }, "properties": { "networkProfile": { "networkPlugin": "azure", "networkPluginMode": "overlay", "networkPolicy": "cilium", "networkDataplane":"cilium", "loadBalancerSku": "Standard" }, "dnsPrefix": "napcluster", "agentPoolProfiles": [ { "name": "agentpool", "count": 3, "vmSize": "standard_d2s_v3", "osType": "Linux", "mode": "System" } ], "nodeProvisioningProfile": { "mode": "Auto" } } } ] }`

Enable node auto-provisioning on a new cluster using the

command with the`az deployment group create`

`--template-file`

flag set to the path of the ARM template file.`az deployment group create --resource-group $RESOURCE_GROUP --template-file ./nap.json`


### Enable NAP on an existing cluster

Enable node auto-provisioning on an existing cluster using the

command with the`az aks update`

`--node-provisioning-mode`

flag set to`Auto`

.`az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP --node-provisioning-mode Auto`


## Disable node auto-provisioning (NAP) on an AKS cluster

Important

You can only disable NAP on a cluster if the following conditions are met:

- There are no existing NAP nodes. You can use the
`kubectl get nodes -l karpenter.sh/nodepool`

command to check for existing NAP-managed nodes. - All existing Karpenter
have their`NodePools`

`spec.limits.cpu`

field set to`0`

. This action prevents new nodes from being created, but doesn't disrupt currently running nodes.

Set the

`spec.limits.cpu`

field to`0`

for every existing Karpenter`NodePool`

. For example:`apiVersion: karpenter.sh/v1 kind: NodePool metadata: name: default spec: limits: cpu: 0`

Important

If you don't want to ensure that every pod previously running on a NAP node is safely migrated to a non-NAP node before disabling NAP, you can skip steps 2 and 3 and instead use the

`kubectl delete node`

command for each NAP-managed node. However,**we don't recommend skipping these steps**, as it might leave some pods pending and doesn't honor Pod Disruption Budgets (PDBs).When using the

`kubectl delete node`

command, be careful to only delete NAP-managed nodes. You can identify NAP-managed nodes using the`kubectl get nodes -l karpenter.sh/nodepool`

command.Add the

`karpenter.azure.com/disable:NoSchedule`

taint to every Karpenter`NodePool`

. For example:`apiVersion: karpenter.sh/v1 kind: NodePool metadata: name: default spec: template: spec: ... taints: - key: karpenter.azure.com/disable effect: NoSchedule`

This action starts the process of migrating the workloads on the NAP-managed nodes to non-NAP nodes, honoring PDBs and disruption limits. Pods migrate to non-NAP nodes if they can fit. If there isn't enough fixed-size capacity, some node NAP-managed nodes remain.

Scale up existing fixed-size

`ManagedCluster`

`AgentPools`

or create new fixed-size`AgentPools`

to take the load from the node NAP-managed nodes. As these nodes are added to the cluster, the node NAP-managed nodes are drained, and work is migrated to the fixed-size nodes.Delete all NAP-managed nodes using the

`kubectl get nodes -l karpenter.sh/nodepool`

command. If NAP-managed nodes still exist, the cluster likely lacks fixed-size capacity. In this case, you should add more nodes so the remaining workloads can be migrated.

Update the NAP mode to

`Manual`

using theAzure CLI command with the`az aks update`

`--node-provisioning-mode`

flag set to`Manual`

.`az aks update \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --node-provisioning-mode Manual`


Update the

`properties.nodeProvisioningProfile.mode`

field to`Manual`

in your ARM template and redeploy it.`{ "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentTemplate.json#", "contentVersion": "1.0.0.0", "metadata": {}, "parameters": {}, "resources": [ { "type": "Microsoft.ContainerService/managedClusters", "apiVersion": "2025-05-01", "sku": { "name": "Base", "tier": "Standard" }, "name": "napcluster", "location": "uksouth", "identity": { "type": "SystemAssigned" }, "properties": { "networkProfile": { "networkPlugin": "azure", "networkPluginMode": "overlay", "networkPolicy": "cilium", "networkDataplane":"cilium", "loadBalancerSku": "Standard" }, "dnsPrefix": "napcluster", "agentPoolProfiles": [ { "name": "agentpool", "count": 3, "vmSize": "standard_d2s_v3", "osType": "Linux", "mode": "System" } ], "nodeProvisioningProfile": { "mode": "Manual" } } } ] }`


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:
