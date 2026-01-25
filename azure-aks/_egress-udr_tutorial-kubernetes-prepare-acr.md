---
merged_at: 2026-01-25T12:25:33.864547
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: egress-udr.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/egress-udr -->

# Customize cluster egress with a user-defined routing table in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You can customize the egress for your Azure Kubernetes Service (AKS) clusters to fit specific scenarios. AKS provisions a `Standard`

SKU load balancer for egress by default. However, the default setup may not meet the requirements of all scenarios if public IPs are disallowed or the scenario requires extra hops for egress.

This article walks through how to customize a cluster's egress route to support custom network scenarios. These scenarios include ones which disallow public IPs and require the cluster to sit behind a network virtual appliance (NVA).

## Prerequisites

- Azure CLI version 2.0.81 or greater. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - API version
`2020-01-01`

or greater.

## Requirements and limitations

Using outbound type is an advanced networking scenario and requires proper network configuration. The following requirements and limitations apply to using outbound type:

- Setting
`outboundType`

requires AKS clusters with a`vm-set-type`

of`VirtualMachineScaleSets`

and a`load-balancer-sku`

of`Standard`

. - Setting
`outboundType`

to a value of`UDR`

requires a user-defined route with valid outbound connectivity for the cluster. - Setting
`outboundType`

to a value of`UDR`

implies the ingress source IP routed to the load-balancer may**not match**the cluster's outgoing egress destination address.

## Overview of customizing egress with a user-defined routing table

AKS doesn't automatically configure egress paths if `userDefinedRouting`

is set, which means you must configure the egress.

When you don't use standard load balancer (SLB) architecture, you must establish explicit egress. You must deploy your AKS cluster into an existing virtual network with a subnet that has been previously configured. This architecture requires explicitly sending egress traffic to an appliance like a firewall, gateway, or proxy, so a public IP assigned to the standard load balancer or appliance can handle the Network Address Translation (NAT).

### Load balancer creation with `userDefinedRouting`


AKS clusters with an outbound type of UDR get a standard load balancer only when the first Kubernetes service of type `loadBalancer`

is deployed. The load balancer is configured with a public IP address for *inbound* requests and a backend pool for *inbound* requests. The Azure cloud provider configures inbound rules, but it **doesn't configure outbound public IP address or outbound rules**. Your UDR is the only source for egress traffic.

Note

Azure load balancers [don't incur a charge until a rule is placed](https://azure.microsoft.com/pricing/details/load-balancer/).

## Deploy a cluster with outbound type of UDR and Azure Firewall

To see an application of a cluster with outbound type using a user-defined route, see this [restrict egress traffic with Azure firewall example](limit-egress-traffic).

Important

Outbound type of UDR requires a route for 0.0.0.0/0 and a next hop destination of NVA in the route table.
The route table already has a default 0.0.0.0/0 to the Internet. Without a public IP address for Azure to use for Source Network Address Translation (SNAT), simply adding this route won't provide you outbound Internet connectivity. AKS validates that you don't create a 0.0.0.0/0 route pointing to the Internet but instead to a gateway, NVA, etc.
When using an outbound type of UDR, a load balancer public IP address for **inbound requests** isn't created unless you configure a service of type *loadbalancer*. AKS never creates a public IP address for **outbound requests** if you set an outbound type of UDR.

## Next steps

For more information on user-defined routes and Azure networking, see:


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
