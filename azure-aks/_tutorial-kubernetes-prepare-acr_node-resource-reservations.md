---
merged_at: 2026-01-25T12:06:27.694727
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-prepare-acr.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-prepare-acr -->

# Tutorial - Create an Azure Container Registry (ACR) and build images

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Container Registry (ACR) is a private registry for container images. A private container registry allows you to securely build and deploy your applications and custom code.

In this tutorial, you deploy an ACR instance and push a container image to it. You learn how to:

- Create an ACR instance.
- Use
[ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-overview)to build and push container images to ACR. - View images in your registry.

## Before you begin

In the [previous tutorial](tutorial-kubernetes-prepare-app), you used Docker to create a container image for a simple Azure Store Front application. If you haven't created the Azure Store Front app image, return to [Tutorial 1 - Prepare an application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.0.53 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an Azure Container Registry

Before creating an ACR instance, you need a resource group. An Azure resource group is a logical container into which you deploy and manage Azure resources.

Important

This tutorial uses *myResourceGroup* as a placeholder for the resource group name. If you want to use a different name, replace *myResourceGroup* with your own resource group name.

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location westus2`

Create an ACR instance using the

command and provide your own unique registry name. The registry name must be unique within Azure and contain 5-50 lowercase alphanumeric characters. This tutorial series uses an environment variable,`az acr create`

`$ACRNAME`

, as a placeholder for the container registry name. You can set this environment variable to your unique ACR name to use in future commands. The*Basic*SKU is a cost-optimized entry point for development purposes that provides a balance of storage and throughput.`az acr create --resource-group myResourceGroup --name $ACRNAME --sku Basic`


## Build and push container images to registry

Build and push the images to your ACR using the Azure CLI

command.`az acr build`

Note

For this step, there isn't an equivalent Azure PowerShell cmdlet that performs this task.

In the following example, we don't build the

`product-service`

image. This image can take a long time to build, and there's a container image already available in the GitHub Container Registry (GHCR). You can use thecommand to import the image from the GHCR to your ACR instance. We also don't build the`az acr import`

`rabbitmq`

image. This image is available from the Docker Hub public repository and doesn't need to be built or pushed to your ACR instance.`az acr import --name $ACRNAME --source ghcr.io/azure-samples/aks-store-demo/product-service:latest --image aks-store-demo/product-service:latest az acr build --registry $ACRNAME --image aks-store-demo/order-service:latest ./src/order-service/ az acr build --registry $ACRNAME --image aks-store-demo/store-front:latest ./src/store-front/`


## List images in registry

View the images in your ACR instance using the

command.`az acr repository list`

`az acr repository list --name $ACRNAME --output table`

The following example output lists the available images in your registry:

`Result ---------------- aks-store-demo/product-service aks-store-demo/order-service aks-store-demo/store-front`


## Next steps

In this tutorial, you created an ACR and pushed images to it to use in an AKS cluster. You learned how to:

- Create an ACR instance.
- Use
[ACR Tasks](/en-us/azure/container-registry/container-registry-tasks-overview)to build and push container images to ACR. - View images in your registry.

In the next tutorial, you learn how to deploy a Kubernetes cluster in Azure.


---

<!-- DOCUMENTO FUSIONADO: node-resource-reservations.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/node-resource-reservations -->

# Node resource reservations in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn about node resource reservations in Azure Kubernetes Service (AKS).

## Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS.

AKS reserves two types of resources, **CPU** and **memory**, on each node to maintain node performance and functionality. As a node grows larger in resources, the resource reservations also grow due to a higher need for management of user-deployed pods. Keep in mind that you can't change resource reservations on a node.

### CPU reservations

Reserved CPU is dependent on node type and cluster configuration, which might result in less allocatable CPU due to running extra features. The following table shows CPU reservations in millicores:

| CPU cores on host | 1 core | 2 cores | 4 cores | 8 cores | 16 cores | 32 cores | 64 cores |
|---|---|---|---|---|---|---|---|
| Kube-reserved CPU (millicores) | 60 | 100 | 140 | 180 | 260 | 420 | 740 |

### Memory reservations

In AKS, reserved memory consists of the sum of two values:

**AKS 1.29 and later**

has the`kubelet`

daemon*memory.available < 100 Mi*eviction rule by default. This rule ensures that a node has at least 100 Mi allocatable at all times. When a host is below that available memory threshold, the`kubelet`

triggers the termination of one of the running pods and frees up memory on the host machine.**A rate of memory reservations**set according to the lesser value of:*20 MB * Max Pods supported on the Node + 50 MB*or*25% of the total system memory resources*.**Examples**:- If the virtual machine (VM) provides 8 GB of memory and the node supports up to 30 pods, AKS reserves
*20 MB * 30 Max Pods + 50 MB = 650 MB*for kube-reserved.`Allocatable space = 8 GB - 0.65 GB (kube-reserved) - 0.1 GB (eviction threshold) = 7.25 GB or 90.625% allocatable.`

- If the VM provides 4 GB of memory and the node supports up to 70 pods, AKS reserves
*25% * 4 GB = 1000 MB*for kube-reserved, as this is less than*20 MB * 70 Max Pods + 50 MB = 1450 MB*.

For more information, see

[Configure maximum pods per node in an AKS cluster](concepts-network-ip-address-planning#maximum-pods-per-node).- If the virtual machine (VM) provides 8 GB of memory and the node supports up to 30 pods, AKS reserves

**AKS versions prior to 1.29**

has the`kubelet`

daemon*memory.available < 750 Mi*eviction rule by default. This rule ensures that a node has at least 750 Mi allocatable at all times. When a host is below that available memory threshold, the`kubelet`

triggers the termination of one of the running pods and free up memory on the host machine.**A regressive rate of memory reservations**for the kubelet daemon to properly function (*kube-reserved*).- 25% of the first 4 GB of memory
- 20% of the next 4 GB of memory (up to 8 GB)
- 10% of the next 8 GB of memory (up to 16 GB)
- 6% of the next 112 GB of memory (up to 128 GB)
- 2% of any memory more than 128 GB


Note

AKS reserves an extra 2 GB for system processes in Windows nodes that isn't part of the calculated memory.

Memory and CPU allocation rules are designed to:

- Keep agent nodes healthy, including some hosting system pods critical to cluster health.
- Cause the node to report less allocatable memory and CPU than it would report if it weren't part of a Kubernetes cluster.

For example, if a node offers 7 GB, it reports 34% of memory not allocatable including the 750 Mi hard eviction threshold.

`0.75 + (0.25*4) + (0.20*3) = 0.75 GB + 1 GB + 0.6 GB = 2.35 GB / 7 GB = 33.57% reserved`


In addition to reservations for Kubernetes itself, the underlying node OS also reserves an amount of CPU and memory resources to maintain OS functions.

For associated best practices, see [Best practices for basic scheduler features in AKS](operator-best-practices-scheduler).
