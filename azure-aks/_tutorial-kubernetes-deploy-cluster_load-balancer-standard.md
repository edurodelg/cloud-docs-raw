---
merged_at: 2026-01-25T12:06:27.760134
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: tutorial-kubernetes-deploy-cluster.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-deploy-cluster -->

# Tutorial - Create an Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Kubernetes provides a distributed platform for containerized applications. With Azure Kubernetes Service (AKS), you can quickly create a production ready Kubernetes cluster.

In this tutorial, you deploy a Kubernetes cluster in AKS. You learn how to:

- Deploy an AKS cluster that can authenticate to an Azure Container Registry (ACR).
- Install the Kubernetes CLI,
`kubectl`

. - Configure
`kubectl`

to connect to your AKS cluster.

## Before you begin

In previous tutorials, you created a container image and uploaded it to an ACR instance. Start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app) to follow along.

- If you're using Azure CLI, this tutorial requires that you're running the Azure CLI version 2.35.0 or later. Check your version with
`az --version`

. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - If you're using Azure PowerShell, this tutorial requires that you're running Azure PowerShell version 5.9.0 or later. Check your version with
`Get-InstalledModule -Name Az`

. To install or upgrade, see[Install Azure PowerShell](/en-us/powershell/azure/install-az-ps). - If you're using Azure Developer CLI, this tutorial requires that you're running the Azure Developer CLI version 1.5.1 or later. Check your version with
`azd version`

. To install or upgrade, see[Install Azure Developer CLI](/en-us/azure/developer/azure-developer-cli/install-azd).

## Create a Kubernetes cluster

AKS clusters can use [Kubernetes role-based access control (Kubernetes RBAC)](https://kubernetes.io/docs/reference/access-authn-authz/rbac/), which allows you to define access to resources based on roles assigned to users. If a user is assigned multiple roles, permissions are combined. Permissions can be scoped to either a single namespace or across the whole cluster.

To learn more about AKS and Kubernetes RBAC, see [Control access to cluster resources using Kubernetes RBAC and Microsoft Entra identities in AKS](azure-ad-rbac).

This tutorial requires Azure CLI version 2.35.0 or later. Check your version with `az --version`

. To install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli). If you're using the Bash environment in Azure Cloud Shell, the latest version is already installed.

## Install the Kubernetes CLI

You use the Kubernetes CLI, [ kubectl](https://kubernetes.io/docs/reference/kubectl/), to connect to your Kubernetes cluster. If you use the Azure Cloud Shell,

`kubectl`

is already installed. If you're running the commands locally, you can use the Azure CLI or Azure PowerShell to install `kubectl`

.Install

`kubectl`

locally using thecommand.`az aks install-cli`

`az aks install-cli`


## Create an AKS cluster

AKS clusters can use [Kubernetes role-based access control (Kubernetes RBAC)](https://kubernetes.io/docs/reference/access-authn-authz/rbac/), which allows you to define access to resources based on roles assigned to users. Permissions are combined when users are assigned multiple roles. Permissions can be scoped to either a single namespace or across the whole cluster. For more information, see [Control access to cluster resources using Kubernetes RBAC and Microsoft Entra ID in AKS](azure-ad-rbac).

For information about AKS resource limits and region availability, see [Quotas, virtual machine size restrictions, and region availability in AKS](quotas-skus-regions).

Important

This tutorial creates a three-node cluster. To ensure your cluster operates reliably, you should run at least two nodes. A minimum of three nodes is required to use Azure Container Storage. If you get an error message when trying to create the cluster, then you might need to request a quota increase for your Azure subscription or try a different Azure region. Alternatively, you can omit the node VM size parameter to use the default VM size.

To allow an AKS cluster to interact with other Azure resources, the Azure platform automatically creates a cluster identity. In this example, the cluster identity is [granted the right to pull images](cluster-container-registry-integration) from the ACR instance you created in the previous tutorial. To execute the command successfully, you must have an **Owner** or **Azure account administrator** role in your Azure subscription.

Create an AKS cluster using the

command. The following example creates a cluster named`az aks create`

*myAKSCluster*in the resource group named*myResourceGroup*. This resource group was created in the[previous tutorial](tutorial-kubernetes-prepare-acr)in the*westus2*region. We'll continue to use the environment variable,`$ACRNAME`

, that we set in the[previous tutorial](tutorial-kubernetes-prepare-acr). If you don't have this environment variable set, set it now to the same value you used previously.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 3 \ --node-vm-size standard_l8s_v3 \ --generate-ssh-keys \ --attach-acr $ACRNAME`

Note

If you already generated SSH keys, you might encounter an error similar to

`linuxProfile.ssh.publicKeys.keyData is invalid`

. To proceed, retry the command without the`--generate-ssh-keys`

parameter.

To avoid needing an **Owner** or **Azure account administrator** role, you can also manually configure a service principal to pull images from ACR. For more information, see [ACR authentication with service principals](/en-us/azure/container-registry/container-registry-auth-service-principal) or [Authenticate from Kubernetes with a pull secret](/en-us/azure/container-registry/container-registry-auth-kubernetes). Alternatively, you can use a [managed identity](use-managed-identity) instead of a service principal for easier management.

## Connect to cluster using kubectl

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. The following example gets credentials for the AKS cluster named`az aks get-credentials`

*myAKSCluster*in*myResourceGroup*.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify connection to your cluster using the

command, which returns a list of cluster nodes.`kubectl get nodes`

`kubectl get nodes`

The following example output shows a list of the cluster nodes:

`NAME STATUS ROLES AGE VERSION aks-nodepool1-19366578-vmss000000 Ready agent 47h v1.30.9 aks-nodepool1-19366578-vmss000001 Ready agent 47h v1.30.9 aks-nodepool1-19366578-vmss000002 Ready agent 47h v1.30.9`


## Next step

In this tutorial, you deployed a Kubernetes cluster in AKS and configured `kubectl`

to connect to the cluster. You learned how to:

- Deploy an AKS cluster that can authenticate to an ACR.
- Install the Kubernetes CLI,
`kubectl`

. - Configure
`kubectl`

to connect to your AKS cluster.

In the next tutorial, you learn how to deploy Azure Container Storage on your cluster and create a generic ephemeral volume. If you're using Azure Developer CLI, or if you weren't able to use a storage optimized VM type due to quota issues, proceed directly to the [Deploy containerized application](tutorial-kubernetes-deploy-application) tutorial.


---

<!-- DOCUMENTO FUSIONADO: load-balancer-standard.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/load-balancer-standard -->

# Use a public standard load balancer in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The [Azure Load Balancer](/en-us/azure/load-balancer/load-balancer-overview) operates at layer 4 of the Open Systems Interconnection (OSI) model that supports both inbound and outbound scenarios. It distributes inbound flows that arrive at the load balancer's front end to the back end pool instances.

A **public** load balancer integrated with AKS serves two purposes:

- Provide outbound connections to the cluster nodes inside the AKS virtual network (VNet) by translating the private IP address to a public IP address part of its
*outbound pool*. - Provide access to applications via Kubernetes services of type
`LoadBalancer`

, enabling you to easily scale your applications and create highly available services.

This article covers integration with a public load balancer on AKS. For internal load balancer integration, see [Use an internal load balancer in AKS](internal-lb).

## Prerequisites

- Azure Load Balancer is available in two SKUs:
*Basic*and*Standard*. The*Standard*SKU is used by default when you create an AKS cluster. The*Standard*SKU gives you access to added functionality, such as a larger backend pool,[multiple node pools](create-node-pools),[Availability Zones](availability-zones), and is[secure by default](/en-us/azure/load-balancer/load-balancer-overview#securebydefault). It's the recommended load balancer SKU for AKS. For more information on the*Basic*and*Standard*SKUs, see[Azure Load Balancer SKU comparison](/en-us/azure/load-balancer/skus). - For a full list of the supported annotations for Kubernetes services with type
`LoadBalancer`

, see[LoadBalancer annotations](https://cloud-provider-azure.sigs.k8s.io/topics/loadbalancer/#loadbalancer-annotations). - This article assumes you have an AKS cluster with the
*Standard*SKU Azure Load Balancer. If you need an AKS cluster, you can create one using[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or[the Azure portal](learn/quick-kubernetes-deploy-portal).

Important

If you'd prefer to use your own gateway, firewall, or proxy to provide outbound connection, you can skip the creation of the load balancer outbound pool and respective frontend IP by using [ outbound type as UserDefinedRouting (UDR)](egress-outboundtype). The outbound type defines the egress method for a cluster and defaults to type

`LoadBalancer`

.## Limitations

The following limitations apply when you create and manage AKS clusters that support a load balancer with the *Standard* SKU:

AKS manages the lifecycle and operations of agent nodes. Modifying the IaaS resources associated with the agent nodes isn't supported. An example of an unsupported operation is making manual changes to the load balancer resource group.

At least one public IP or IP prefix is required for allowing egress traffic from the AKS cluster. The public IP or IP prefix is required to maintain connectivity between the control plane and agent nodes and to maintain compatibility with previous versions of AKS. You have the following options for specifying public IPs or IP prefixes with a

*Standard*SKU load balancer:- Provide your own public IPs.
- Provide your own public IP prefixes.
- Specify a number up to 100 to allow the AKS cluster to create that many
*Standard*SKU public IPs in the same resource group as the AKS cluster. This resource group is usually named with`MC_`

at the beginning. AKS assigns the public IP to the*Standard*SKU load balancer. By default, one public IP is automatically created in the same resource group as the AKS cluster if no public IP, public IP prefix, or number of IPs is specified. You also must allow public addresses and avoid creating any Azure policies that ban IP creation.

A public IP created by AKS can't be reused as a custom bring your own (BYO) public IP address. You must create and manage all custom IP addresses.

You can only define the load balancer SKU when you create an AKS cluster. You can't change the load balancer SKU after an AKS cluster has been created.

You can only use one type of load balancer SKU (

*Basic*or*Standard*) in a single cluster.*Standard*SKU load balancers only support*Standard*SKU IP addresses.[Private Link Service](/en-us/azure/private-link/private-link-service-overview)isn't supported when the load balancer backend pool type is set to`nodeIP`

.

## Create a load balancer service in AKS

After you create an AKS cluster with outbound type `LoadBalancer`

(default), your cluster is ready to use the load balancer to expose services.

Create a service manifest named

`public-svc.yaml`

, which creates a public service of type`LoadBalancer`

.`apiVersion: v1 kind: Service metadata: name: public-svc spec: type: LoadBalancer ports: - port: 80 selector: app: public-app`


## Specify the load balancer IP address

If you want to use a specific IP address with the load balancer, you have two options to specify the IP address:

**Set service annotations**(recommended): Use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address.**Add the**: Add the*LoadBalancerIP*property to the load balancer YAML manifest`Service.Spec.LoadBalancerIP`

property to the load balancer YAML manifest. This field is deprecating following[upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235), and it can't support dual-stack. Current usage remains the same and existing services are expected to work without modification.

## Deploy the load balancer service manifest

Deploy the public service manifest using

and specify the name of your YAML manifest.`kubectl apply`

`kubectl apply -f public-svc.yaml`

The Azure Load Balancer is configured with a new public IP that fronts the new service. Since the Azure Load Balancer can have multiple frontend IPs, each new service that you deploy gets a new dedicated frontend IP to be uniquely accessed.

Confirm your service is created and the load balancer is configured using the

`kubectl get service`

command.`kubectl get service public-svc`

When you view the service details, the public IP address created for this service on the load balancer is shown in the

*EXTERNAL-IP*column of the output. It might take a few minutes for the IP address to change from*<pending>*to an actual public IP address. The following example output shows successful creation of the service:`NAMESPACE NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE default public-svc LoadBalancer 10.0.39.110 203.0.113.187 80:32068/TCP 52s`

Get more detailed information about your service using the

`kubectl describe service`

command.`kubectl describe service public-svc`

The following example output is a condensed version of the output after you run

`kubectl describe service`

.*LoadBalancer Ingress*shows the external IP address exposed by your service.*IP*shows the internal addresses.`Name: public-svc Namespace: default Labels: <none> Annotations: <none> Selector: app=public-app ... IP: 10.0.39.110 ... LoadBalancer Ingress: 203.0.113.187 ... TargetPort: 80/TCP NodePort: 32068/TCP ... Session Affinity: None External Traffic Policy: Cluster ...`
