---
merged_at: 2026-02-01T07:48:55.762537
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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-clusters-workloads -->

# Core concepts for Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes core concepts of Azure Kubernetes Service (AKS), a managed Kubernetes service that you can use to deploy and operate containerized applications at scale on Azure.

Important

Starting on **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning on **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see the [Retirement GitHub issue](https://github.com/Azure/AKS/issues/4988) and the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=500645). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## What is Kubernetes?

Kubernetes is an open-source container orchestration platform for automating the deployment, scaling, and management of containerized applications. For more information, see the official [Kubernetes documentation](https://kubernetes.io/docs/home/).

## What is AKS?

AKS is a managed Kubernetes service that simplifies deploying, managing, and scaling containerized applications that use Kubernetes. For more information, see [What is Azure Kubernetes Service (AKS)?](what-is-aks).

## Cluster components

An AKS cluster is divided into two main components:

**Control plane**: The control plane provides the core Kubernetes services and orchestration of application workloads.**Nodes**: Nodes are the underlying virtual machines (VMs) that run your applications.

Note

AKS managed components have the label `kubernetes.azure.com/managedby`

: `aks`

.

AKS manages the Helm releases with the prefix `aks-managed`

. Continuously increasing revisions on these releases are expected and safe.

### Control plane

The Azure managed control plane is composed of several components that help manage the cluster:

| Component | Description |
|---|---|
`kube-apiserver` |
The API server (
|

`etcd`

[etcd](https://kubernetes.io/docs/concepts/overview/components/#etcd)helps to maintain the state of your Kubernetes cluster and configuration.`kube-scheduler`

[kube-scheduler](https://kubernetes.io/docs/concepts/overview/components/#kube-scheduler)) helps to make scheduling decisions. It watches for new pods with no assigned node and selects a node for them to run on.`kube-controller-manager`

[kube-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#kube-controller-manager)) runs controller processes, such as noticing and responding when nodes go down.`cloud-controller-manager`

[cloud-controller-manager](https://kubernetes.io/docs/concepts/overview/components/#cloud-controller-manager)) embeds cloud-specific control logic to run controllers specific to the cloud provider.### Nodes

Each AKS cluster has at least one node, which is an Azure VM that runs Kubernetes node components. The following components run on each node:

| Component | Description |
|---|---|
`kubelet` |
The
|

`kube-proxy`

[kube-proxy](https://kubernetes.io/docs/concepts/overview/components/#kube-proxy)is a network proxy that maintains network rules on nodes.`container runtime`

[container runtime](https://kubernetes.io/docs/concepts/overview/components/#container-runtime)manages the execution and lifecycle of containers.## Node configuration

Configure the following settings for nodes.

### VM size and image

The *Azure VM size* for your nodes defines CPUs, memory, size, and the storage type available, such as a high-performance solid-state drive or a regular hard-disk drive. The VM size you choose depends on the workload requirements and the number of pods that you plan to run on each node. As of May 2025, the default VM SKU and size will be dynamically selected by AKS based on available capacity and quota if the parameter is left blank during deployment. For more information, see [Supported VM sizes in Azure Kubernetes Service (AKS)](quotas-skus-regions#supported-vm-sizes).

In AKS, the *VM image* for your cluster's nodes is based on Ubuntu Linux, [Azure Linux](use-azure-linux), or Windows Server 2022. When you create an AKS cluster or scale out the number of nodes, the Azure platform automatically creates and configures the requested number of VMs. Agent nodes are billed as standard VMs. Any VM size discounts, including [Azure reservations](/en-us/azure/cost-management-billing/reservations/save-compute-costs-reservations), are automatically applied.

### OS disks

Default OS disk sizing is used on new clusters or node pools only when a default OS disk size isn't specified. This behavior applies to both managed and ephemeral OS disks. For more information, see [Default OS disk sizing](concepts-storage#default-os-disk-sizing).

### Resource reservations

AKS uses node resources to help the nodes function as part of the cluster. This usage can cause a discrepancy between the node's total resources and the allocatable resources in AKS. To maintain node performance and functionality, AKS reserves two types of resources, CPU and memory, on each node. For more information, see [Resource reservations in AKS](node-resource-reservations).

### OS

AKS supports two linux distros: Ubuntu and Azure Linux. Ubuntu is the default Linux distro on AKS. Windows node pools are also supported on AKS with the [Long Term Servicing Channel (LTSC)](/en-us/windows-server/get-started/servicing-channels-comparison) as the default channel on AKS. For more information on default OS versions, see documentation on [node images](node-images).

### Container runtime

A container runtime is software that executes containers and manages container images on a node. The runtime helps abstract away system calls or OS-specific functionality to run containers on Linux or Windows. For Linux node pools, [containerd](https://containerd.io/) is used on Kubernetes version 1.19 and higher. For Windows Server 2019 and 2022 node pools, [containerd](https://containerd.io/) is generally available and is the only runtime option on Kubernetes version 1.23 and higher.

## Pods

A *pod* is a group of one or more containers that share the same network and storage resources and a specification for how to run the containers. Pods typically have a 1:1 mapping with a container, but you can run multiple containers in a pod.

## Node pools

In AKS, nodes of the same configuration are grouped together into *node pools*. These node pools contain the underlying virtual machine scale sets and virtual machines (VMs) that run your applications.

When you create an AKS cluster, you define the initial number of nodes and their size (version), which creates a [system node pool](use-system-pools). System node pools serve the primary purpose of hosting critical system pods, such as CoreDNS and `konnectivity`

.

To support applications that have different compute or storage demands, you can create *user node pools*. User node pools serve the primary purpose of hosting your application pods.

For more information, see [Create node pools in AKS](create-node-pools) and [Manage node pools in AKS](manage-node-pools).

## Node resource group

When you create an AKS cluster in an Azure resource group, the AKS resource provider automatically creates a second resource group called the *node resource group*. This resource group contains all the infrastructure resources associated with the cluster, including VMs, virtual machine scale sets, and storage.

For more information, see the following resources:

[Why are two resource groups created with AKS?](faq)[Can I provide my own name for the AKS node resource group?](faq)[Can I modify tags and other properties of the resources in the AKS node resource group?](faq)

## Namespaces

Kubernetes resources, such as pods and deployments, are logically grouped into *namespaces* to divide an AKS cluster and create, view, or manage access to resources.

The following namespaces are created by default in an AKS cluster:

| Namespace | Description |
|---|---|
`default` |
The
|

`kube-node-lease`

[kube-node-lease](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace enables nodes to communicate their availability to the control plane.`kube-public`

[kube-public](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace isn't typically used, but you can use it so that resources are visible across the whole cluster by any user.`kube-system`

[kube-system](https://kubernetes.io/docs/concepts/overview/working-with-objects/namespaces/#initial-namespaces)namespace is used by Kubernetes to manage cluster resources, such as`coredns`

, `konnectivity-agent`

, and `metrics-server`

. It is not recommended to deploy your own applications to this namespace. For rare cases where deploying your own applications to this namespace is necessary, see the [FAQ](faq#can-admission-controller-webhooks-affect-kube-system-and-internal-aks-namespaces-)to learn how.## Cluster modes

In AKS, you can create a cluster with the Automatic or Standard mode. AKS Automatic provides a more fully managed experience. You can manage cluster configuration, including nodes, scaling, security, and other preconfigured settings. AKS Standard provides more control over the cluster configuration, including the ability to manage node pools, scaling, and other settings.

For more information, see [AKS Automatic and Standard feature comparison](intro-aks-automatic#aks-automatic-and-standard-feature-comparison).

## Pricing tiers

AKS offers three pricing tiers for cluster management: Free, Standard, and Premium. The pricing tier you choose determines the features that are available for managing your cluster.

For more information, see [Pricing tiers for AKS cluster management](free-standard-pricing-tiers).

## Supported Kubernetes versions

For more information, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

## Related content

For information on more core concepts for AKS, see the following resources:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/create-nginx-ingress-private-controller -->

# Configure NGINX ingress controller to support Azure private DNS zone with application routing add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to configure an NGINX ingress controller to work with an Azure internal load balancer. It also explains how to configure a private Azure DNS zone to enable DNS resolution for the private endpoints to resolve specific domains.

## Before you begin

An AKS cluster with the

[application routing add-on](app-routing).To attach an Azure private DNS Zone, you need the

[Owner](/en-us/azure/role-based-access-control/built-in-roles#owner),[Azure account administrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles), or[Azure coadministrator](/en-us/azure/role-based-access-control/rbac-and-directory-admin-roles#classic-subscription-administrator-roles)role on your Azure subscription.

## Connect to your AKS cluster

To connect to the Kubernetes cluster from your local computer, you use `kubectl`

, the Kubernetes command-line client. You can install it locally using the [az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli) command. If you use the Azure Cloud Shell, `kubectl`

is already installed.

The following example configures connecting to your cluster named *aks-cluster* in the *test-rg* using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials \
--resource-group test-rg \
--name aks-cluster
```


## Create a virtual network

To publish a private DNS zone to your virtual network, specify a list of virtual networks that are allowed to resolve records within the zone with [virtual network links](/en-us/azure/dns/private-dns-virtual-network-links).

The following example creates a virtual network named *vnet-1* in the *test-rg* resource group, and one subnet named *subnet-1* to create within the virtual network with a specific address prefix.

```
az network vnet create \
--name vnet-1 \
--resource-group test-rg \
--location eastus \
--address-prefix 10.2.0.0/16 \
--subnet-name subnet-1 \
--subnet-prefixes 10.2.0.0/24
```


## Create an Azure private DNS zone

Note

You can configure the application routing add-on to automatically create records on one or more Azure global and private DNS zones for hosts defined on ingress resources. All global Azure DNS zones and all private Azure DNS zones must be in the same resource group.

Create a DNS zone using the [az network private-dns zone create](/en-us/cli/azure/network/private-dns/zone?#az-network-private-dns-zone-create) command, specifying the name of the zone and the resource group to create it in. The following example creates a DNS zone named *private.contoso.com* in the *test-rg* resource group.

```
az network private-dns zone create \
--resource-group test-rg \
--name private.contoso.com
```


You create a virtual network link to the DNS zone created earlier using the [az network private-dns link vnet create](/en-us/cli/azure/network/private-dns/link/vnet#az-network-private-dns-link-vnet-create) command. The following example creates a link named *dns-link* to the zone *private.contoso.com* for the virtual network *vnet-1*. Include the `--registration-enabled`

parameter to specify the link isn't registration enabled.

```
az network private-dns link vnet create \
--resource-group test-rg \
--name dns-link \
--zone-name private.contoso.com \
--virtual-network vnet-1 \
--registration-enabled false
```


The Azure DNS private zone auto registration feature manages DNS records for virtual machines deployed in a virtual network. When you link a virtual network with a private DNS zone with this setting enabled, a DNS record gets created for each Azure virtual machine for your AKS node deployed in the virtual network.

## Attach an Azure private DNS zone to the application routing add-on

Note

The `az aks approuting zone add`

command uses the permissions of the user running the command to create the [Azure DNS Zone](/en-us/azure/dns/dns-protect-private-zones-recordsets) role assignment. The **Private DNS Zone Contributor** role is a built-in role for managing private DNS resources and is assigned to the add-on's managed identity. For more information on AKS managed identities, see [Summary of managed identities](managed-identity-overview#summary-of-managed-identities-used-by-aks).

Retrieve the resource ID for the DNS zone using the

command and set the output to a variable named`az network dns zone show`

`ZONEID`

. The following example queries the zone*private.contoso.com*in the resource group*test-rg*.`ZONEID=$(az network private-dns zone show \ --resource-group test-rg \ --name private.contoso.com \ --query "id" \ --output tsv)`

Update the add-on to enable integration with Azure DNS using the

command. You can pass a comma-separated list of DNS zone resource IDs. The following example updates the AKS cluster`az aks approuting zone`

*aks-cluster*in the resource group*test-rg*.`az aks approuting zone add \ --resource-group test-rg \ --name aks-cluster \ --ids=${ZONEID} \ --attach-zones`


## Create an NGINX ingress controller with a private IP address and an internal load balancer

The application routing add-on uses a Kubernetes [custom resource definition (CRD)](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/) called [ NginxIngressController](https://aka.ms/aks/approuting/nginxingresscontrollercrd) to configure NGINX ingress controllers. You can create more ingress controllers or modify an existing configuration.

`NginxIngressController`

CRD has a `loadBalancerAnnotations`

field to control the behavior of the NGINX ingress controller's service by setting load balancer annotations. For more information about load balancer annotations, see [Customizations via Kubernetes annotations](configure-load-balancer-standard#customizations-via-kubernetes-annotations).

Perform the following steps to create an NGINX ingress controller with an internal facing Azure Load Balancer with a private IP address.

Copy the following YAML manifest into a new file named

**nginx-internal-controller.yaml**and save the file to your local computer.`apiVersion: approuting.kubernetes.azure.com/v1alpha1 kind: NginxIngressController metadata: name: nginx-internal spec: ingressClassName: nginx-internal controllerNamePrefix: nginx-internal loadBalancerAnnotations: service.beta.kubernetes.io/azure-load-balancer-internal: "true"`

Create the NGINX ingress controller resources using the

command.`kubectl apply`

`kubectl apply -f nginx-internal-controller.yaml`

The following example output shows the created resource:

`nginxingresscontroller.approuting.kubernetes.azure.com/nginx-internal created`

Verify the ingress controller was created

You can verify the status of the NGINX ingress controller using the

command.`kubectl get nginxingresscontroller`

`kubectl get nginxingresscontroller`

The following example output shows the created resource. It might take a few minutes for the controller to be available:

`NAME INGRESSCLASS CONTROLLERNAMEPREFIX AVAILABLE default webapprouting.kubernetes.azure.com nginx True nginx-internal nginx-internal nginx-internal True`


## Deploy an application

The application routing add-on uses annotations on Kubernetes Ingress objects to create the appropriate resources.

Create the application namespace called

`aks-store`

to run the example pods using the`kubectl create namespace`

command.`kubectl create namespace aks-store`

Deploy the AKS store application using the following YAML manifest file:

`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/sample-manifests/docs/app-routing/aks-store-deployments-and-services.yaml -n aks-store`


This manifest creates the necessary deployments and services for the AKS store application.

## Create the Ingress resource that uses a host name on the Azure private DNS zone and a private IP address

Update ** host** with the name of your DNS host, for example,

**store-front.private.contoso.com**. Verify you're specifying nginx-internal for the ingressClassName.

Copy the following YAML manifest into a new file named

**ingress.yaml**and save the file to your local computer.`apiVersion: networking.k8s.io/v1 kind: Ingress metadata: name: store-front namespace: aks-store spec: ingressClassName: nginx-internal rules: - host: store-front.private.contoso.com http: paths: - backend: service: name: store-front port: number: 80 path: / pathType: Prefix`

Create the ingress resource using the

command.`kubectl apply`

`kubectl apply -f ingress.yaml -n aks-store`

The following example output shows the created resource:

`ingress.networking.k8s.io/store-front created`


## Verify the managed Ingress was created

You can verify the managed Ingress was created using the [ kubectl get ingress](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get) command.

```
kubectl get ingress -n aks-store
```


The following example output shows the created managed Ingress:

```
NAME CLASS HOSTS ADDRESS PORTS AGE
store-front nginx-internal store-front.private.contoso.com 80 10s
```


## Verify the Azure private DNS zone was updated

In a few minutes, run the [az network private-dns record-set a list](/en-us/cli/azure/network/private-dns/record-set/a#az-network-private-dns-record-set-a-list) command to view the A records for your Azure private DNS zone. Specify the name of the resource group and the name of the DNS zone. In this example, the resource group is *test-rg* and DNS zone is *private.contoso.com*.

```
az network private-dns record-set a list \
--resource-group test-rg \
--zone-name private.contoso.com
```


The following example output shows the created record:

```
[
{
"aRecords": [
{
"ipv4Address": "10.224.0.7"
}
],
"etag": "ecc303c5-4577-4ca2-b545-d34e160d1c2d",
"fqdn": "store-front.private.contoso.com.",
"id": "/subscriptions/aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e/resourceGroups/test-rg/providers/Microsoft.Network/privateDnsZones/private.contoso.com/A/store-front",
"isAutoRegistered": false,
"name": "store-front",
"resourceGroup": "test-rg",
"ttl": 300,
"type": "Microsoft.Network/privateDnsZones/A"
}
]
```


## Next steps

For other configuration information related to SSL encryption other advanced NGINX ingress controller and ingress resource configuration, review [DNS and SSL configuration](app-routing-dns-ssl) and [application routing add-on configuration](app-routing-nginx-configuration).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-gateway-api -->

# Install Managed Gateway API CRDs (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

The [Kubernetes Gateway API](https://gateway-api.sigs.k8s.io/) is a specification for traffic management on Kubernetes clusters. It was designed as a successor and enhancement of the [Ingress API](https://kubernetes.io/docs/concepts/services-networking/ingress/), which lacked a unified and provider-agnostic approach for advanced traffic routing.

The Managed Gateway API Installation for Azure Kubernetes Service (AKS) installs the Custom Resource Definitions (CRDs) for the Kubernetes Gateway API. With the Managed Gateway API installation, you can use Gateway API functionality in a fully supported mode on AKS. However, you must also use an AKS add-on or extension that implements the Gateway API, such as the [Istio add-on](istio-gateway-api).

## Gateway API bundle version and AKS Kubernetes version mapping

The following table outlines the supported Kubernetes versions for your AKS cluster for each Gateway API bundle version for the `standard`

channel. `Experimental`

channel CRDs are disallowed and must be uninstalled before enabling the Managed Gateway API installation.

| Gateway API Bundle Version | Supported Kubernetes Versions |
|---|---|
| v1.2.1 | v1.26.0 - v1.33.x |
| v1.3.0 | v1.34.0+ |

Note

If you upgrade your AKS cluster to a new minor version after installing the Managed Gateway API CRDs, the CRDs will automatically be upgraded to the new supported Gateway API bundle version for that Kubernetes version. For instance, if you upgrade from AKS `v1.33.0`

to `v1.34.0`

and previously had the Managed Gateway API installed for bundle version `v1.2.1`

, the CRDs are automatically upgraded to bundle version `v1.3.0`

.

## Prerequisites

Ensure that you have at least one of the following implementations of the Gateway API installed and enabled on your cluster:

[Istio add-on](istio-deploy-addon)minor revision`asm-1-26`

and later.- If you already have an existing installation of the Gateway API CRDs on your cluster, then you must only have
`standard`

channel CRDs installed, and the Gateway API bundle version must be compatible with your cluster's Kubernetes version. See the table for the[bundle version associated with each Kubernetes version](#gateway-api-bundle-version-and-aks-kubernetes-version-mapping).

- If you already have an existing installation of the Gateway API CRDs on your cluster, then you must only have
Install the

`aks-preview`

extension using thecommand if you're using Azure CLI. You must use`az extension add`

`aks-preview`

version`19.0.0b4`

and later.`az extension add --name aks-preview`

Update to the latest version of the extension using the

command:`az extension update`

`az extension update --name aks-preview`


## Manage the Managed Gateway API preview feature

You can register the `ManagedGatewayAPIPreview`

feature flag by using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command:

```
az feature register --namespace "Microsoft.ContainerService" --name "ManagedGatewayAPIPreview"
```


Then you can install or uninstall the Managed Gateway API CRDs.

You can run the

command to install the Managed Gateway API CRDs on a newly created cluster. You must also enable an implementation of the Gateway API to enable the managed CRD installation.`az aks create`

`# Example: enable the managed Gateway API installation with the Istio service mesh add-on az aks create -g $RESOURCE_GROUP -n $CLUSTER_NAME --enable-gateway-api --enable-azure-service-mesh`

To install the Managed Gateway API CRDs on an existing cluster with a supported implementation enabled, run the following command:

`az aks update -g $RESOURCE_GROUP -n $CLUSTER_NAME --enable-gateway-api`

To view the CRDs installed on your cluster, run the following command:

`kubectl get crds | grep "gateway.networking.k8s.io"`

`gatewayclasses.gateway.networking.k8s.io 2025-08-29T17:52:36Z gateways.gateway.networking.k8s.io 2025-08-29T17:52:36Z grpcroutes.gateway.networking.k8s.io 2025-08-29T17:52:36Z httproutes.gateway.networking.k8s.io 2025-08-29T17:52:37Z referencegrants.gateway.networking.k8s.io 2025-08-29T17:52:37Z`

Verify that the CRDs have the expected annotations and that the bundle version matches the

[expected Kubernetes version](#gateway-api-bundle-version-and-aks-kubernetes-version-mapping)for your cluster.`kubectl get crd gateways.gateway.networking.k8s.io -ojsonpath={.metadata.annotations} | jq`

`{ "api-approved.kubernetes.io": "https://github.com/kubernetes-sigs/gateway-api/pull/3328", "app.kubernetes.io/managed-by": "aks", "app.kubernetes.io/part-of": <hash>, "gateway.networking.k8s.io/bundle-version": "v1.2.1", "gateway.networking.k8s.io/channel": "standard" }`

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/deploy-application-template -->

# Deploy an Azure Kubernetes application by using an ARM template

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To deploy a Kubernetes application programmatically through Azure CLI, you select the Kubernetes application and settings, generate an ARM template, accept legal terms and conditions, and finally deploy the ARM template.

## Select Kubernetes application

First, you need to select the Kubernetes application that you want to deploy in the Azure portal.

In the Azure portal, go to the

[Marketplace page](https://portal.azure.com/#view/Microsoft_Azure_Marketplace/MarketplaceOffersBlade/selectedMenuItemId/home/fromContext/AKS).Select your Kubernetes application.

Select the required plan.

Select the

**Usage Information + Support**tab. Copy the values for`publisherID`

,`productID`

, and`planID`

. You'll need these values later.

## Generate ARM template

Continue on to generate the ARM template for your deployment.

Select the

**Create**button.Fill out all the application (extension) details.

At the bottom of the

**Review + Create**tab, select**Download a template for automation**.If all the validations are passed, you'll see the ARM template in the editor.

Download the ARM template and save it to a file on your computer.


## Accept terms and agreements

Before you can deploy a Kubernetes application, you need to accept its terms and agreements. To do so, use [Azure CLI](/en-us/cli/azure/vm/image/terms) or [Azure PowerShell](/en-us/powershell/module/az.marketplaceordering/). Be sure to use the values you copied for `plan-publisher`

, `plan-offerID`

, and `plan-name`

in your command.

```
az vm image terms accept --offer <Product ID> --plan <Plan ID> --publisher <Publisher ID>
```


Note

Although this Azure CLI command is for VMs, it also works for containers. For more information, see the [ az cm image terms reference](/en-us/cli/azure/vm/image/terms).

```
## Get-AzMarketplaceTerms -Publisher <Publisher ID> -Product <Product ID> -Name <Plan ID>
```


## Deploy ARM template

Once you've accepted the terms, you can deploy your ARM template. For instructions, see [Tutorial: Create and deploy your first ARM template](/en-us/azure/azure-resource-manager/templates/template-tutorial-create-first-template).

## Next steps

- Learn about
[Kubernetes applications available through Marketplace](deploy-marketplace). - Learn about
[cluster extensions](cluster-extensions).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/understand-aks-costs -->

# Understand Azure Kubernetes Service (AKS) usage and costs

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article provides resources you can use to better understand your Azure Kubernetes Service (AKS) usage and costs and identify cost optimization opportunities.

## About cost analysis

[Microsoft Cost Management](/en-us/azure/cost-management-billing/costs/reporting-get-started) is a suite of FinOps tools that help you analyze, monitor, and optimize your cloud costs. It's available for Azure customers with access to a billing account, subscription, resource group, or management group. For more information, see [What is Microsoft Cost Management?](/en-us/azure/cost-management-billing/costs/overview-cost-management)

[Cost analysis](/en-us/azure/cost-management-billing/costs/reporting-get-started#cost-analysis) is a feature of Cost Management that helps you understand your costs and usage. It provides insights into how your resources are being used and helps you identify opportunities to reduce costs. For more information, see [Start analyzing costs in Azure](/en-us/azure/cost-management-billing/costs/quick-acm-cost-analysis).

## Cost analysis resources

### Cost analysis add-on for AKS

The cost analysis add-on for AKS allows you to view comprehensive cost data scoped to Kubernetes constructs, such as clusters and namespaces, and Azure Compute, Network, and Storage resources. Enable it on your AKS cluster by following the steps in [Enable the Azure Kubernetes Service (AKS) cost analysis add-on](cost-analysis). To learn more about viewing the cost data, see [View Kubernetes costs](/en-us/azure/cost-management-billing/costs/view-kubernetes-costs).

### Azure Cost Optimization workbook

The [Azure Cost Optimization workbook](/en-us/azure/advisor/advisor-workbook-cost-optimization) provides a comprehensive view of your Azure costs and recommendations for optimizing them. For more information, see [Cost Optimization workbook](/en-us/azure/advisor/advisor-workbook-cost-optimization).

### Azure Orphaned Resources workbook

The [Azure Orphaned Resources workbook](https://github.com/dolevshor/azure-orphan-resources) helps you identify and manage unused resources in your Azure environment. For more information, see [Orphaned Resources workbook](https://techcommunity.microsoft.com/blog/fasttrackforazureblog/azure-orphan-resources/3492198).

## Next steps

For more information about managing your AKS costs, see [Best practices for cost optimization in Azure Kubernetes Service (AKS)](best-practices-cost).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/ai-toolchain-operator-mcp -->

# Integrate an MCP server with an LLM Inference Service on Azure Kubernetes Service (AKS) with the AI toolchain operator add-on

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you connect an MCP-compliant tool server with an AI toolchain operator (KAITO) inference workspace on Azure Kubernetes Service (AKS), enabling secure and modular tool calling for LLM applications. You also learn how to validate end-to-end tool invocation by integrating the model with the MCP server and monitoring real-time function execution through structured responses.

## Model Context Protocol (MCP)

As an extension of [KAITO inference with tool calling](ai-toolchain-operator-tool-calling), the [Model Context Protocol (MCP)](https://modelcontextprotocol.io/) provides a standardized way to define and expose tools for language models to call.

Tool calling with MCP makes it easier to connect language models to real services and actions without tightly coupling logic into the model itself. Instead of embedding every function or API call into your application code, MCP lets you run a standalone tool server that exposes standardized tools or APIs that any compatible LLM can use. This clean separation means you can update tools independently, share them across models, and manage them like any other microservice.

You can bring-your-own (BYO) internal or connect external MCP servers seamlessly with your KAITO inference workspace on AKS.

## MCP with AI toolchain operator (KAITO) on AKS

You can register an external MCP server in a uniform, schema-driven format and serve it to any compatible inference endpoint, including those [deployed with a KAITO workspace](https://kaito-project.github.io/kaito/docs/tool-calling/#model-context-protocol-mcp). This approach allows for externalizing business logic, decoupling model behavior from tool execution, and reusing tools across agents, models, and environments.

In this guide, you register a pre-defined MCP server, test real calls issued by an LLM running in a KAITO inference workspace, and confirm the entire tool execution path (from model prompt to MCP function invocation) works as intended. You have flexibility to scale or swap tools independent of your model.

## Prerequisites

- This article assumes that you have an existing AKS cluster. If you don't have a cluster, create one by using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Your AKS cluster is running on Kubernetes version
`1.33`

or higher. To upgrade your cluster, see[Upgrade your AKS cluster](upgrade-aks-cluster). - Install and configure Azure CLI version
`2.77.0`

or later. To find your version, run`az --version`

. To install or update, see[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). - You have the
[AI toolchain operator add-on enabled](ai-toolchain-operator)on your cluster and a[KAITO workspace with tool calling support](ai-toolchain-operator-tool-calling)deployed on your cluster. - An external MCP server available at an accessible URL (e.g.,
`https://mcp.example.com/mcp`

) that returns valid`/list_tools`

and has`stream`

transport.

## Connect to a reference MCP server

In this example, we'll use a reference [Time MCP Server](https://github.com/modelcontextprotocol/servers/tree/main/src/time#time-mcp-server), which provides time zone conversion capabilities and enables LLMs to get current time information and perform conversions using standardized names.

## Port-forward the KAITO inference service

Confirm that your KAITO workspace is ready and retrieve the inference service endpoint using the

`kubectl get`

command.`kubectl get svc workspace‑phi‑4-mini-toolcall`

Note

The output might be a

`ClusterIP`

or internal address. Check which port(s) the service listens on. The default KAITO inference API is on port`80`

for HTTP. If it's only internal, you can port‑forward locally.Port-forward the inference service for testing using the

`kubectl port-forward`

command.`kubectl port-forward svc/workspace‑phi‑4‑mini-toolcall 8000:80`

Check

`/v1/models`

endpoint to confirm that`Phi-4-mini-instruct`

LLM is available using`curl`

.`curl http://localhost:8000/v1/models`

Your

`Phi-4-mini-instruct`

OpenAI-compatible inference API will be available at:`http://localhost:8000/v1/chat/completions`


## Confirm the reference MCP server is valid

This example assumes that the Time MCP server is hosted at `https://mcp.example.com`

.

Confirm the server returns tools using

`curl`

.`curl https://mcp.example.com/mcp/list_tools`

Expected output:

`{ "tools": [ { "name": "get_current_time", "description": "Get the current time in a specific timezone", "arguments": { "timezone": "string" } }, { "name": "convert_time", "description": "Convert time between two timezones", "arguments": { "source_timezone": "string", "time": "string", "target_timezone": "string" } } ] }`


## Connect MCP server to the KAITO workspace using API request

KAITO automatically fetches tool definitions from **tools declared in API requests** or registered dynamically inside the inference runtime (vLLM + MCP tool loader).

In this guide, we create a Python virtual environment to send a tool-calling request to the `Phi-4-mini-instruct`

inference endpoint using the MCP definition and pointing to the server.

Define a new working directory for this test project.

`mkdir kaito-mcp cd kaito-mcp`

Create a Python virtual environment and activate it so that all packages are local to your test project.

`uv venv source .venv/bin/activate`

Use the open-source

[Autogen](https://microsoft.github.io/autogen/stable//index.html)framework to test the tool calling functionality and install its dependencies:`uv pip install "autogen-ext[openai]" "autogen-agentchat" "autogen-ext[mcp]"`

Create a test file named

`test.py`

that:- Connects to the Time MCP server and loads
`get_current_time`

tool. - Connects to your KAITO inference service running at
`localhost:8000`

. - Sends an example query like “What time is it in Europe/Paris?”
- Enables automatic selection and calling of the
`get_current_time`

tool.

`import asyncio from autogen_agentchat.agents import AssistantAgent from autogen_agentchat.ui import Console from autogen_core import CancellationToken from autogen_core.models import ModelFamily, ModelInfo from autogen_ext.models.openai import OpenAIChatCompletionClient from autogen_ext.tools.mcp import (StreamableHttpMcpToolAdapter, StreamableHttpServerParams) from openai import OpenAI async def main() -> None: # Create server params for the Time MCP service server_params = StreamableHttpServerParams( url="https://mcp.example.com/mcp", timeout=30.0, terminate_on_close=True, ) # Load the get_current_time tool from the server adapter = await StreamableHttpMcpToolAdapter.from_server_params(server_params, "get_current_time") # Fetch model name from KAITO's local OpenAI-compatible API model = OpenAI(base_url="http://localhost:8000/v1", api_key="dummy").models.list().data[0].id model_info: ModelInfo = { "vision": False, "function_calling": True, "json_output": True, "family": ModelFamily.UNKNOWN, "structured_output": True, "multiple_system_messages": True, } # Connect to the KAITO inference workspace model_client = OpenAIChatCompletionClient( base_url="http://localhost:8000/v1", api_key="dummy", model=model, model_info=model_info ) # Define the assistant agent agent = AssistantAgent( name="time-assistant", model_client=model_client, tools=[adapter], system_message="You are a helpful assistant that can provide time information." ) # Run a test task that invokes the tool await Console( agent.run_stream( task="What time is it in Europe/Paris?", cancellation_token=CancellationToken() ) ) if __name__ == "__main__": asyncio.run(main())`

- Connects to the Time MCP server and loads
Run the test script in your virtual environment.

`uv run test.py`

In the output of this test, you should expect the following:

- The model correctly generates a tool call using the MCP name and expected arguments.
- Autogen sends the tool call to the MCP server, the MCP server runs the logic and returns a result.
- The
`Phi-4-mini-instruct`

LLM interprets the raw tool output and provides a natural language response.

`---------- TextMessage (user) ---------- What time is it in Europe/Paris? ---------- ToolCallRequestEvent (time-assistant) ---------- [FunctionCall(id='chatcmpl-tool-xxxx', arguments='{"timezone": "Europe/Paris"}', name='get_current_time')] ---------- ToolCallExecutionEvent (time-assistant) ---------- [FunctionExecutionResult(content='{"timezone":"Europe/Paris","datetime":"2025-09-17T17:43:05+02:00","is_dst":true}', name='get_current_time', call_id='chatcmpl-tool-xxxx', is_error=False)] ---------- ToolCallSummaryMessage (time-assistant) ---------- The current time in Europe/Paris is 5:43 PM (CEST).`


## Experiment with more MCP tools

You can test the various tools available to this MCP server, such as `convert_time`

.

In your

`test.py`

file from the previous step, update your`adapter`

definition to the following:`adapter = await StreamableHttpMcpToolAdapter.from_server_params(server_params, "convert_time")`

Update your

`task`

definition to invoke the new tool. For example:`task="Convert 9:30 AM New York time to Tokyo time."`

Save and run the Python script.

`uv run test.py`

Expected output:

`9:30 AM in New York is 10:30 PM in Tokyo.`


## Troubleshooting

The following table outlines common errors when testing KAITO inference with an external MCP server and how to resolve them:

| Error | How to resolve |
|---|---|
`Tool not found` |
Ensure that your tool name matches the one declared in `/mcp/list_tools` . |
`401 Unauthorized` |
If your MCP server requires an Auth token, make sure to update `server_params` to include headers with the Auth token. |
`connection refused` |
Ensure the KAITO inference service is port-forwarded properly (e.g. to `localhost:8000` ). |
`tool call ignored` |
Review the
|

## Next steps

In this article, you learned how to connect a KAITO workspace to an external reference MCP server using Autogen to enable tool calling through the OpenAI-compatible API. You also validated that the LLM could discover, invoke, and integrate results from MCP-compliant tools on AKS. To learn more, see the following resources:

[Deploy and test tool calls](ai-toolchain-operator-tool-calling)with the AI toolchain operator add-on on AKS.- KAITO tool calling and
[MCP official documentation](https://kaito-project.github.io/kaito/docs/tool-calling).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/virtual-nodes-cli -->

# Create and configure an Azure Kubernetes Services (AKS) cluster to use virtual nodes using Azure CLI

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Virtual nodes enable network communication between pods that run in Azure Container Instances (ACI) and AKS clusters. To provide this communication, you create a virtual network subnet and assign delegated permissions. Virtual nodes only work with AKS clusters created using *advanced* networking (Azure CNI). By default, AKS clusters are created with *basic* networking (kubenet). This article shows you how to create a virtual network and subnets, then deploy an AKS cluster that uses advanced networking.

This article shows you how to use the Azure CLI to create and configure virtual network resources and an AKS cluster enabled with virtual nodes.

## Before you begin

Important

Before using virtual nodes with AKS, review both the [limitations of AKS virtual nodes](virtual-nodes) and the [virtual networking limitations of ACI](/en-us/azure/container-instances/container-instances-virtual-network-concepts). These limitations affect the location, networking configuration, and other configuration details of both your AKS cluster and the virtual nodes.

You need the ACI service provider registered with your subscription. You can check the status of the ACI provider registration using the

command.`az provider list`

`az provider list --query "[?contains(namespace,'Microsoft.ContainerInstance')]" -o table`

The

*Microsoft.ContainerInstance*provider should report as*Registered*, as shown in the following example output:`Namespace RegistrationState RegistrationPolicy --------------------------- ------------------- -------------------- Microsoft.ContainerInstance Registered RegistrationRequired`

If the provider shows as

*NotRegistered*, register the provider using the.`az provider register`

`az provider register --namespace Microsoft.ContainerInstance`

If using Azure CLI, this article requires Azure CLI version 2.0.49 or later. Run

`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). You can also use[Azure Cloud Shell](#launch-azure-cloud-shell).

### Launch Azure Cloud Shell

The Azure Cloud Shell is a free interactive shell you can use to run the steps in this article. It has common Azure tools preinstalled and configured.

To open the Cloud Shell, select **Try it** from the upper right corner of a code block. You can also launch Cloud Shell in a separate browser tab by going to [https://shell.azure.com/bash](https://shell.azure.com/bash). Select **Copy** to copy the blocks of code, paste it into the Cloud Shell, and press enter to run it.

## Create a resource group

An Azure resource group is a logical group in which Azure resources are deployed and managed.

Create a resource group using the

command.`az group create`

`az group create --name myResourceGroup --location eastus`


## Create a virtual network

Important

Virtual node requires a custom virtual network and associated subnet. It can't be associated with the same virtual network as the AKS cluster.

Create a virtual network using the

command. The following example creates a virtual network named`az network vnet create`

*myVnet*with an address prefix of*10.0.0.0/8*and a subnet named*myAKSSubnet*. The address prefix of this subnet defaults to*10.240.0.0/16*.`az network vnet create \ --resource-group myResourceGroup \ --name myVnet \ --address-prefixes 10.0.0.0/8 \ --subnet-name myAKSSubnet \ --subnet-prefix 10.240.0.0/16`

Create an extra subnet for the virtual nodes using the

command. The following example creates a subnet named`az network vnet subnet create`

*myVirtualNodeSubnet*with an address prefix of*10.241.0.0/16*.`az network vnet subnet create \ --resource-group myResourceGroup \ --vnet-name myVnet \ --name myVirtualNodeSubnet \ --address-prefixes 10.241.0.0/16`


## Create an AKS cluster with managed identity

Get the subnet ID using the

command.`az network vnet subnet show`

`az network vnet subnet show --resource-group myResourceGroup --vnet-name myVnet --name myAKSSubnet --query id -o tsv`

Create an AKS cluster using the

command and replace`az aks create`

`<subnetId>`

with the ID obtained in the previous step. The following example creates a cluster named*myAKSCluster*with five nodes.`az aks create \ --resource-group myResourceGroup \ --name myAKSCluster \ --node-count 5 \ --network-plugin azure \ --vnet-subnet-id <subnetId> \ --generate-ssh-keys`

After several minutes, the command completes and returns JSON-formatted information about the cluster.


For more information on managed identities, see [Use managed identities](use-managed-identity).

## Enable the virtual nodes addon

Note

If you have an existing Azure Kubernetes Service Cluster created that uses Azure CNI for the Advanced Networking you should be able to enable virtual nodes as an add-on using the CLI.

Enable virtual nodes using the

command. The following example uses the subnet named`az aks enable-addons`

*myVirtualNodeSubnet*created in a previous step.`az aks enable-addons \ --resource-group myResourceGroup \ --name myAKSCluster \ --addons virtual-node \ --subnet-name myVirtualNodeSubnet`


## Connect to the cluster

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This step downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

Verify the connection to your cluster using the

command, which returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`

The following example output shows the single VM node created and the virtual node for Linux,

*virtual-node-aci-linux*:`NAME STATUS ROLES AGE VERSION virtual-node-aci-linux Ready agent 28m v1.11.2 aks-agentpool-14693408-0 Ready agent 32m v1.11.2`


## Deploy a sample app

Create a file named

`virtual-node.yaml`

and copy in the following YAML. The YAML schedules the container on the node by defining a[nodeSelector](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/)and[toleration](https://kubernetes.io/docs/concepts/configuration/taint-and-toleration/).`apiVersion: apps/v1 kind: Deployment metadata: name: aci-helloworld spec: replicas: 1 selector: matchLabels: app: aci-helloworld template: metadata: labels: app: aci-helloworld spec: containers: - name: aci-helloworld image: mcr.microsoft.com/azuredocs/aci-helloworld ports: - containerPort: 80 nodeSelector: kubernetes.io/role: agent kubernetes.io/os: linux type: virtual-kubelet tolerations: - key: virtual-kubelet.io/provider operator: Exists - key: azure.com/aci effect: NoSchedule`

Run the application using the

command.`kubectl apply`

`kubectl apply -f virtual-node.yaml`

Get a list of pods and the scheduled node using the

command with the`kubectl get pods`

`-o wide`

argument.`kubectl get pods -o wide`

The pod is scheduled on the virtual node

*virtual-node-aci-linux*, as shown in the following example output:`NAME READY STATUS RESTARTS AGE IP NODE aci-helloworld-9b55975f-bnmfl 1/1 Running 0 4m 10.241.0.4 virtual-node-aci-linux`

The pod is assigned an internal IP address from the Azure virtual network subnet delegated for use with virtual nodes.


Note

If you use images stored in Azure Container Registry, [configure and use a Kubernetes secret](https://kubernetes.io/docs/tasks/configure-pod-container/pull-image-private-registry/). A current limitation of virtual nodes is you can't use integrated Microsoft Entra service principal authentication. If you don't use a secret, pods scheduled on virtual nodes fail to start and report the error `HTTP response status code 400 error code "InaccessibleImage"`

.

## Test the virtual node pod

Test the pod running on the virtual node by browsing to the demo application with a web client. As the pod is assigned an internal IP address, you can quickly test this connectivity from another pod on the AKS cluster.

Create a test pod and attach a terminal session to it using the following

`kubectl run -it`

command.`kubectl run -it --rm testvk --image=mcr.microsoft.com/dotnet/runtime-deps:6.0`

Install

`curl`

in the pod using`apt-get`

.`apt-get update && apt-get install -y curl`

Access the address of your pod using

`curl`

, such as. Provide your own internal IP address shown in the previous[http://10.241.0.4](http://10.241.0.4)`kubectl get pods`

command.`curl -L http://10.241.0.4`

The demo application is displayed, as shown in the following condensed example output:

`<html> <head> <title>Welcome to Azure Container Instances!</title> </head> [...]`

Close the terminal session to your test pod with

`exit`

. When your session is ends, the pod is deleted.

## Remove virtual nodes

Delete the

`aci-helloworld`

pod running on the virtual node using the`kubectl delete`

command.`kubectl delete -f virtual-node.yaml`

Disable the virtual nodes using the

command.`az aks disable-addons`

`az aks disable-addons --resource-group myResourceGroup --name myAKSCluster --addons virtual-node`

Remove the virtual network resources and resource group using the following commands.

`# Change the name of your resource group, cluster and network resources as needed RES_GROUP=myResourceGroup AKS_CLUSTER=myAKScluster AKS_VNET=myVnet AKS_SUBNET=myVirtualNodeSubnet # Get AKS node resource group NODE_RES_GROUP=$(az aks show --resource-group $RES_GROUP --name $AKS_CLUSTER --query nodeResourceGroup --output tsv) # Get network profile ID NETWORK_PROFILE_ID=$(az network profile list --resource-group $NODE_RES_GROUP --query "[0].id" --output tsv) # Delete the network profile az network profile delete --id $NETWORK_PROFILE_ID -y # Grab the service association link ID SAL_ID=$(az network vnet subnet show --resource-group $RES_GROUP --vnet-name $AKS_VNET --name $AKS_SUBNET --query id --output tsv)/providers/Microsoft.ContainerInstance/serviceAssociationLinks/default # Delete the service association link for the subnet az resource delete --ids $SAL_ID --api-version 2021-10-01 # Delete the subnet delegation to Azure Container Instances az network vnet subnet update --resource-group $RES_GROUP --vnet-name $AKS_VNET --name $AKS_SUBNET --remove delegations`


## Next steps

In this article, you scheduled a pod on the virtual node and assigned a private internal IP address. You could instead create a service deployment and route traffic to your pod through a load balancer or ingress controller. For more information, see [Create a basic ingress controller in AKS](ingress-basic).

Virtual nodes are often one component of a scaling solution in AKS. For more information on scaling solutions, see the following articles:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-advanced-scheduler -->

# Best practices for advanced scheduler features in Azure Kubernetes Service (AKS) using the kube-scheduler

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you manage clusters in Azure Kubernetes Service (AKS), you often need to isolate teams and workloads. Advanced features provided by the Kubernetes scheduler let you control:

- Which pods can be scheduled on certain nodes.
- How multi-pod applications can be appropriately distributed across the cluster.

This best practices article focuses on advanced Kubernetes scheduling features for cluster operators. In this article, you learn how to:

- Use taints and tolerations to limit what pods can be scheduled on nodes.
- Give preference to pods to run on certain nodes with node selectors or node affinity.
- Split apart or group together pods with inter-pod affinity or anti-affinity.
- Restrict scheduling of workloads that require GPUs only on nodes with schedulable GPUs.

If additional capabilities or ML frameworks are needed to schedule and queue batch workloads, you can [install and configure Kueue on AKS](kueue-overview) to ensure efficient, policy-driven scheduling in AKS clusters.

If fine-grained scheduler configuration is needed to optimize how pods and jobs prioritize specific nodes, storage resources, topology, and more, you can [configure a scheduler on AKS](concepts-scheduler-configuration).

## Provide dedicated nodes using taints and tolerations


Best practice guidance:Limit access for resource-intensive applications, such as ingress controllers, to specific nodes. Keep node resources available for workloads that require them, and don't allow scheduling of other workloads on the nodes.


When you create your AKS cluster, you can deploy nodes with GPU support or a large number of powerful CPUs. For more information, see [Use GPUs on AKS](gpu-cluster). You can use these nodes for large data processing workloads such as machine learning (ML) or artificial intelligence (AI).

Because this node resource hardware is typically expensive to deploy, limit the workloads that can be scheduled on these nodes. Instead, dedicate some nodes in the cluster to run ingress services and prevent other workloads.

This support for different nodes is provided by using multiple node pools. An AKS cluster supports one or more node pools.

The Kubernetes scheduler uses taints and tolerations to restrict what workloads can run on nodes.

- Apply a
**taint**to a node to indicate only specific pods can be scheduled on them. - Then apply a
**toleration**to a pod, allowing them to*tolerate*a node's taint.

When you deploy a pod to an AKS cluster, Kubernetes only schedules pods on nodes whose taint aligns with the toleration. Taints and tolerations work together to ensure that pods aren't scheduled onto inappropriate nodes. One or more taints are applied to a node, marking the node so that it doesn't accept any pods that don't tolerate the taints.

For example, assume you added a node pool in your AKS cluster for nodes with GPU support. You define name, such as *gpu*, then a value for scheduling. Setting this value to *NoSchedule* restricts the Kubernetes scheduler from scheduling pods with undefined toleration on the node.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name taintnp \
--node-taints sku=gpu:NoSchedule \
--no-wait
```


With a taint applied to nodes in the node pool, you define a toleration in the pod specification that allows scheduling on the nodes. The following example defines the `sku: gpu`

and `effect: NoSchedule`

to tolerate the taint applied to the node pool in the previous step:

```
kind: Pod
apiVersion: v1
metadata:
name: app
spec:
containers:
- name: app
image: <your-workload>:gpu
resources:
requests:
cpu: 0.5
memory: 2Gi
limits:
cpu: 4.0
memory: 16Gi
tolerations:
- key: "sku"
operator: "Equal"
value: "gpu"
effect: "NoSchedule"
```


When this pod is deployed using `kubectl apply -f gpu-toleration.yaml`

, Kubernetes can successfully schedule the pod on the nodes with the taint applied. This logical isolation lets you control access to resources within a cluster.

When you apply taints, work with your application developers and owners to allow them to define the required tolerations in their deployments.

For more information about how to use multiple node pools in AKS, see [Create multiple node pools for a cluster in AKS](create-node-pools).

### Behavior of taints and tolerations in AKS

When you upgrade a node pool in AKS, taints and tolerations follow a set pattern as they're applied to new nodes:

#### Default clusters that use Azure Virtual Machine Scale Sets

You can [taint a node pool](manage-node-pools#specify-a-taint-label-or-tag-for-a-node-pool) from the AKS API to have newly scaled out nodes receive API specified node taints.

Let's assume:

- You begin with a two-node cluster:
*node1*and*node2*. - You upgrade the node pool.
- Two other nodes are created:
*node3*and*node4*. - The taints are passed on respectively.
- The original
*node1*and*node2*are deleted.

#### Clusters without Virtual Machine Scale Sets support

Again, let's assume:

- You have a two-node cluster:
*node1*and*node2*. - You upgrade the node pool.
- An extra node is created:
*node3*. - The taints from
*node1*are applied to*node3*. *node1*is deleted.- A new
*node1*is created to replace to original*node1*. - The
*node2*taints are applied to the new*node1*. *node2*is deleted.

In essence, *node1* becomes *node3*, and *node2* becomes the new *node1*.

When you scale a node pool in AKS, taints and tolerations don't carry over by design.

## Control pod scheduling using node selectors and affinity


Best practice guidanceControl the scheduling of pods on nodes using node selectors, node affinity, or inter-pod affinity. These settings allow the Kubernetes scheduler to logically isolate workloads, such as by hardware in the node.


Taints and tolerations logically isolate resources with a hard cut-off. If the pod doesn't tolerate a node's taint, it isn't scheduled on the node.

Alternatively, you can use node selectors. For example, you label nodes to indicate locally attached SSD storage or a large amount of memory, and then define in the pod specification a node selector. Kubernetes schedules those pods on a matching node.

Unlike tolerations, pods without a matching node selector can still be scheduled on labeled nodes. This behavior allows unused resources on the nodes to consume, but prioritizes pods that define the matching node selector.

Let's look at an example of nodes with a high amount of memory. These nodes prioritize pods that request a high amount of memory. To ensure the resources don't sit idle, they also allow other pods to run. The following example command adds a node pool with the label *hardware=highmem* to the *myAKSCluster* in the *myResourceGroup*. All nodes in that node pool have this label.

```
az aks nodepool add \
--resource-group myResourceGroup \
--cluster-name myAKSCluster \
--name labelnp \
--node-count 1 \
--labels hardware=highmem \
--no-wait
```


A pod specification then adds the `nodeSelector`

property to define a node selector that matches the label set on a node:

```
kind: Pod
apiVersion: v1
metadata:
name: app
spec:
containers:
- name: app
image: <your-workload>:gpu
resources:
requests:
cpu: 0.5
memory: 2Gi
limits:
cpu: 4.0
memory: 16Gi
nodeSelector:
hardware: highmem
```


When you use these scheduler options, work with your application developers and owners to allow them to correctly define their pod specifications.

For more information about using node selectors, see [Assigning Pods to Nodes](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/).

### Node affinity

A node selector is a basic solution for assigning pods to a given node. *Node affinity* provides more flexibility, allowing you to define what happens if the pod can't be matched with a node. You can:

*Require*that Kubernetes scheduler matches a pod with a labeled host. Or,*Prefer*a match but allow the pod to be scheduled on a different host if no match is available.

The following example sets the node affinity to *requiredDuringSchedulingIgnoredDuringExecution*. This affinity requires the Kubernetes schedule to use a node with a matching label. If no node is available, the pod has to wait for scheduling to continue. To allow the pod to be scheduled on a different node, you can instead set the value to * preferredDuringSchedulingIgnoreDuringExecution*:

```
kind: Pod
apiVersion: v1
metadata:
name: app
spec:
containers:
- name: app
image: <your-workload>:gpu
resources:
requests:
cpu: 0.5
memory: 2Gi
limits:
cpu: 4.0
memory: 16Gi
affinity:
nodeAffinity:
requiredDuringSchedulingIgnoredDuringExecution:
nodeSelectorTerms:
- matchExpressions:
- key: hardware
operator: In
values:
- highmem
```


The *IgnoredDuringExecution* part of the setting indicates that the pod shouldn't be evicted from the node if the node labels change. The Kubernetes scheduler only uses the updated node labels for new pods being scheduled, not pods already scheduled on the nodes.

For more information, see [Affinity and anti-affinity](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#affinity-and-anti-affinity).

### Inter-pod affinity and anti-affinity

One final approach for the Kubernetes scheduler to logically isolate workloads is using inter-pod affinity or anti-affinity. These settings define that pods either *shouldn't* or *should* be scheduled on a node that has an existing matching pod. By default, the Kubernetes scheduler tries to schedule multiple pods in a replica set across nodes. You can define more specific rules around this behavior.

For example, you have a web application that also uses an Azure Cache for Redis.

- You use pod anti-affinity rules to request that the Kubernetes scheduler distributes replicas across nodes.
- You use affinity rules to ensure each web app component is scheduled on the same host as a corresponding cache.

The distribution of pods across nodes looks like the following example:

Node 1 |
Node 2 |
Node 3 |
|---|---|---|
| webapp-1 | webapp-2 | webapp-3 |
| cache-1 | cache-2 | cache-3 |

Inter-pod affinity and anti-affinity provide a more complex deployment than node selectors or node affinity. With the deployment, you logically isolate resources and control how Kubernetes schedules pods on nodes.

For a complete example of this web application with Azure Cache for Redis example, see [Co-locate pods on the same node](https://kubernetes.io/docs/concepts/configuration/assign-pod-node/#always-co-located-in-the-same-node).

## Next steps

This article focused on advanced Kubernetes scheduler features. For more information about cluster operations in AKS, see the following best practices:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-smb -->

# Provision Azure NetApp Files SMB volumes for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

After you [configure Azure NetApp Files for Azure Kubernetes Service](azure-netapp-files), you can provision Azure NetApp Files volumes for Azure Kubernetes Service.

Azure NetApp Files supports volumes using [NFS](azure-netapp-files-nfs) (NFSv3 or NFSv4.1), SMB, and [dual-protocol](azure-netapp-files-dual-protocol) (NFSv3 and SMB, or NFSv4.1 and SMB).

- This article describes details for provisioning SMB volumes statically or dynamically.
- For information about provisioning NFS volumes statically or dynamically, see
[Provision Azure NetApp Files NFS volumes for Azure Kubernetes Service](azure-netapp-files-nfs). - For information about provisioning dual-protocol volumes statically, see
[Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service](azure-netapp-files-dual-protocol)

## Statically configure for applications that use SMB volumes

This section describes how to create an SMB volume on Azure NetApp Files and expose the volume statically to Kubernetes for a containerized application to consume.

### Create an SMB Volume

Define variables for later usage. Replace

*myresourcegroup*,*mylocation*,*myaccountname*,*mypool1*,*premium*,*myfilepath*,*myvolsize*,*myvolname*, and*virtnetid*with an appropriate value for your environment. The filepath must be unique within all ANF accounts.`RESOURCE_GROUP="myresourcegroup" LOCATION="mylocation" ANF_ACCOUNT_NAME="myaccountname" POOL_NAME="mypool1" SERVICE_LEVEL="premium" # Valid values are standard, premium, and ultra UNIQUE_FILE_PATH="myfilepath" VOLUME_SIZE_GIB="myvolsize" VOLUME_NAME="myvolname" VNET_ID="vnetId" SUBNET_ID="anfSubnetId"`

Create a volume using the

command.`az netappfiles volume create`

`az netappfiles volume create \ --resource-group $RESOURCE_GROUP \ --location $LOCATION \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --name "$VOLUME_NAME" \ --service-level $SERVICE_LEVEL \ --vnet $VNET_ID \ --subnet $SUBNET_ID \ --usage-threshold $VOLUME_SIZE_GIB \ --file-path $UNIQUE_FILE_PATH \ --protocol-types CIFS`


### Create a secret with the domain credentials

Create a secret on your AKS cluster to access the Active Directory (AD) server using the

command. This secret will be used by the Kubernetes persistent volume to access the Azure NetApp Files SMB volume. Use the following command to create the secret, replacing`kubectl create secret`

`USERNAME`

with your username,`PASSWORD`

with your password, and`DOMAIN_NAME`

with your domain name for your AD.`kubectl create secret generic smbcreds --from-literal=username=USERNAME --from-literal=password="PASSWORD" --from-literal=domain='DOMAIN_NAME'`

Check the secret has been created.

`kubectl get secret NAME TYPE DATA AGE smbcreds Opaque 2 20h`


### Install an SMB CSI driver

You must install a Container Storage Interface (CSI) driver to create a Kubernetes SMB `PersistentVolume`

.

Install the SMB CSI driver on your cluster using helm. Be sure to set the

`windows.enabled`

option to`true`

:`helm repo add csi-driver-smb https://raw.githubusercontent.com/kubernetes-csi/csi-driver-smb/master/charts helm install csi-driver-smb csi-driver-smb/csi-driver-smb --namespace kube-system --version v1.13.0 --set windows.enabled=true`

For other methods of installing the SMB CSI Driver, see

[Install SMB CSI driver master version on a Kubernetes cluster](https://github.com/kubernetes-csi/csi-driver-smb/blob/master/docs/install-csi-driver-master.md).Verify that the

`csi-smb`

controller pod is running and each worker node has a pod running using thecommand:`kubectl get pods`

`kubectl get pods -n kube-system | grep csi-smb csi-smb-controller-68df7b4758-xf2m9 3/3 Running 0 3m46s csi-smb-node-s6clj 3/3 Running 0 3m47s csi-smb-node-win-tfxvk 3/3 Running 0 3m47s`


### Create the persistent volume

List the details of your volume using

. Replace the variables with appropriate values from your Azure NetApp Files account and environment if not defined in a previous step.`az netappfiles volume show`

`az netappfiles volume show \ --resource-group $RESOURCE_GROUP \ --account-name $ANF_ACCOUNT_NAME \ --pool-name $POOL_NAME \ --volume-name "$VOLUME_NAME -o JSON`

The following output is an example of the above command executed with real values.

`{ ... "creationToken": "myvolname", ... "mountTargets": [ { ... " "smbServerFqdn": "ANF-1be3.contoso.com", ... } ], ... }`

Create a file named

`pv-smb.yaml`

and copy in the following YAML. If necessary, replace`myvolname`

with the`creationToken`

and replace`ANF-1be3.contoso.com\myvolname`

with the value of`smbServerFqdn`

from the previous step. Be sure to include your AD credentials secret along with the namespace where the secret is located that you created in a prior step.`apiVersion: v1 kind: PersistentVolume metadata: name: anf-pv-smb spec: storageClassName: "" capacity: storage: 100Gi accessModes: - ReadWriteMany persistentVolumeReclaimPolicy: Retain mountOptions: - dir_mode=0777 - file_mode=0777 - vers=3.0 csi: driver: smb.csi.k8s.io readOnly: false volumeHandle: myvolname # make sure it's a unique name in the cluster volumeAttributes: source: \\ANF-1be3.contoso.com\myvolname nodeStageSecretRef: name: smbcreds namespace: default`

Create the persistent volume using the

command:`kubectl apply`

`kubectl apply -f pv-smb.yaml`

Verify the status of the persistent volume is

*Available*using thecommand:`kubectl describe`

`kubectl describe pv pv-smb`


### Create a persistent volume claim

Create a file name

`pvc-smb.yaml`

and copy in the following YAML.`apiVersion: v1 kind: PersistentVolumeClaim metadata: name: anf-pvc-smb spec: accessModes: - ReadWriteMany volumeName: anf-pv-smb storageClassName: "" resources: requests: storage: 100Gi`

Create the persistent volume claim using the

command:`kubectl apply`

`kubectl apply -f pvc-smb.yaml`

Verify the status of the persistent volume claim is

*Bound*by using the[kubectl describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe)command:`kubectl describe pvc pvc-smb`


### Mount with a pod

Create a file named

`iis-smb.yaml`

and copy in the following YAML. This file will be used to create an Internet Information Services pod to mount the volume to path`/inetpub/wwwroot`

.`apiVersion: v1 kind: Pod metadata: name: iis-pod labels: app: web spec: nodeSelector: "kubernetes.io/os": windows volumes: - name: smb persistentVolumeClaim: claimName: anf-pvc-smb containers: - name: web image: mcr.microsoft.com/windows/servercore/iis:windowsservercore resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 volumeMounts: - name: smb mountPath: "/inetpub/wwwroot" readOnly: false`

Create the pod using the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command:`kubectl apply -f iis-smb.yaml`

Verify the pod is

*Running*and`/inetpub/wwwroot`

is mounted from SMB by using the[kubectl describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe)command:`kubectl describe pod iis-pod`

The output of the command resembles the following example:

`Name: iis-pod Namespace: default Priority: 0 Node: akswin000001/10.225.5.246 Start Time: Fri, 05 May 2023 09:34:41 -0400 Labels: app=web Annotations: <none> Status: Running IP: 10.225.5.248 IPs: IP: 10.225.5.248 Containers: web: Container ID: containerd://39a1659b6a2b6db298df630237b2b7d959d1b1722edc81ce9b1bc7f06237850c Image: mcr.microsoft.com/windows/servercore/iis:windowsservercore Image ID: mcr.microsoft.com/windows/servercore/iis@sha256:0f0114d0f6c6ee569e1494953efdecb76465998df5eba951dc760ac5812c7409 Port: 80/TCP Host Port: 0/TCP State: Running Started: Fri, 05 May 2023 09:34:55 -0400 Ready: True Restart Count: 0 Limits: cpu: 1 memory: 800M Requests: cpu: 1 memory: 800M Environment: <none> Mounts: /inetpub/wwwroot from smb (rw) /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-mbnv8 (ro) ...`

Verify your volume has been mounted on the pod by using the

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command to connect to the pod, and then use`dir`

command in the correct directory to check if the volume is mounted and the size matches the size of the volume you provisioned.`kubectl exec -it iis-pod –- cmd.exe`

The output of the command resembles the following example:

`Microsoft Windows [Version 10.0.20348.1668] (c) Microsoft Corporation. All rights reserved. C:\>cd /inetpub/wwwroot C:\inetpub\wwwroot>dir Volume in drive C has no label. Volume Serial Number is 86BB-AA55 Directory of C:\inetpub\wwwroot 05/04/2023 08:15 PM <DIR> . 05/04/2023 08:15 PM <DIR> .. 0 File(s) 0 bytes 2 Dir(s) 107,373,838,336 bytes free`


## Dynamically configure for applications that use SMB volumes

This section covers how to use Trident to dynamically create an SMB volume on Azure NetApp Files and automatically mount it to a containerized windows application.

### Install Trident

To dynamically provision SMB volumes, you need to install Trident version 22.10 or later. Dynamically provisioning SMB volumes requires windows worker nodes.

Trident is NetApp's dynamic storage provisioner that is purpose-built for Kubernetes. Simplify the consumption of storage for Kubernetes applications using Trident's industry-standard [Container Storage Interface (CSI)](https://kubernetes-csi.github.io/docs/) driver. Trident deploys on Kubernetes clusters as pods and provides dynamic storage orchestration services for your Kubernetes workloads.

Trident can be installed using the Trident operator (manually or using [Helm](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-operator.html)) or [ tridentctl](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy-tridentctl.html). To learn more about these installation methods and how they work, see the

[Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html).

#### Install Trident using Helm

[Helm](https://helm.sh/) must be installed on your workstation to install Trident using this method. For other methods of installing Trident, see the [Trident Install Guide](https://docs.netapp.com/us-en/trident/trident-get-started/kubernetes-deploy.html). If you have windows worker nodes in the cluster, ensure to enable windows with any installation method.

To install Trident using Helm for a cluster with windows worker nodes, run the following commands:

`helm repo add netapp-trident https://netapp.github.io/trident-helm-chart helm install trident netapp-trident/trident-operator --version 23.04.0 --create-namespace --namespace trident –-set windows=true`

The output of the command resembles the following example:

`NAME: trident LAST DEPLOYED: Fri May 5 14:23:05 2023 NAMESPACE: trident STATUS: deployed REVISION: 1 TEST SUITE: None NOTES: Thank you for installing trident-operator, which will deploy and manage NetApp's Trident CSI storage provisioner for Kubernetes. Your release is named 'trident' and is installed into the 'trident' namespace. Please note that there must be only one instance of Trident (and trident-operator) in a Kubernetes cluster. To configure Trident to manage storage resources, you will need a copy of tridentctl, which is available in pre-packaged Trident releases. You may find all Trident releases and source code online at https://github.com/NetApp/trident. To learn more about the release, try: $ helm status trident $ helm get all trident`

To confirm Trident was installed successfully, run the following

command:`kubectl describe`

`kubectl describe torc trident`

The output of the command resembles the following example:

`Name: trident Namespace: Labels: app.kubernetes.io/managed-by=Helm Annotations: meta.helm.sh/release-name: trident meta.helm.sh/release-namespace: trident API Version: trident.netapp.io/v1 Kind: TridentOrchestrator Metadata: ... Spec: IPv6: false Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: <nil> Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent k8sTimeout: 0 Kubelet Dir: <nil> Log Format: text Log Layers: <nil> Log Workflows: <nil> Namespace: trident Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Windows: true Status: Current Installation Params: IPv6: false Autosupport Hostname: Autosupport Image: docker.io/netapp/trident-autosupport:23.04 Autosupport Proxy: Autosupport Serial Number: Debug: false Disable Audit Log: true Enable Force Detach: false Http Request Timeout: 90s Image Pull Policy: IfNotPresent Image Pull Secrets: Image Registry: k8sTimeout: 30 Kubelet Dir: /var/lib/kubelet Log Format: text Log Layers: Log Level: info Log Workflows: Probe Port: 17546 Silence Autosupport: false Trident Image: docker.io/netapp/trident:23.04.0 Message: Trident installed Namespace: trident Status: Installed Version: v23.04.0 Events: Type Reason Age From Message ---- ------ ---- ---- ------- Normal Installing 74s trident-operator.netapp.io Installing Trident Normal Installed 46s trident-operator.netapp.io Trident installed`


### Create a backend

A backend must be created to instruct Trident about the Azure NetApp Files subscription and where it needs to create volumes. For more information about backends, see [Azure NetApp Files backend configuration options and examples](https://docs.netapp.com/us-en/trident/trident-use/anf-examples.html).

Create a file named

`backend-secret-smb.yaml`

and copy in the following YAML. Change the`Client ID`

and`clientSecret`

to the correct values for your environment.`apiVersion: v1 kind: Secret metadata: name: backend-tbc-anf-secret type: Opaque stringData: clientID: 00001111-aaaa-2222-bbbb-3333cccc4444 clientSecret: rR0rUmWXfNioN1KhtHisiSAnoTherboGuskey6pU`

Create a file named

`backend-anf-smb.yaml`

and copy in the following YAML. Change the`ClientID`

,`clientSecret`

,`subscriptionID`

,`tenantID`

,`location`

, and`serviceLevel`

to the correct values for your environment. The`tenantID`

,`clientID`

, and`clientSecret`

can be found from an application registration in Microsoft Entra ID with sufficient permissions for the Azure NetApp Files service. The application registration includes the Owner or Contributor role predefined by Azure. The Azure location must contain at least one delegated subnet. The`serviceLevel`

must match the`serviceLevel`

configured for the capacity pool in[Configure Azure NetApp Files for AKS workloads](azure-netapp-files#configure-azure-netapp-files-for-aks-workloads).`apiVersion: trident.netapp.io/v1 kind: TridentBackendConfig metadata: name: backend-tbc-anf-smb spec: version: 1 storageDriverName: azure-netapp-files subscriptionID: aaaa0a0a-bb1b-cc2c-dd3d-eeeeee4e4e4e tenantID: aaaabbbb-0000-cccc-1111-dddd2222eeee location: eastus serviceLevel: Premium credentials: name: backend-tbc-anf-secret nasType: smb`

Create the secret and backend using the

command.`kubectl apply`

Create the secret:

`kubectl apply -f backend-secret.yaml -n trident`

The output of the command resembles the following example:

`secret/backend-tbc-anf-secret created`

Create the backend:

`kubectl apply -f backend-anf.yaml -n trident`

The output of the command resembles the following example:

`tridentbackendconfig.trident.netapp.io/backend-tbc-anf created`

Verify the backend was created by running the following command:

`kubectl get tridentbackends -n trident`

The output of the command resembles the following example:

`NAME BACKEND BACKEND UUID tbe-9shfq backend-tbc-anf-smb 09cc2d43-8197-475f-8356-da7707bae203`


### Create a secret with the domain credentials for SMB

Create a secret on your AKS cluster to access the AD server using the

command. This information will be used by the Kubernetes persistent volume to access the Azure NetApp Files SMB volume. Use the following command, replacing`kubectl create secret`

`DOMAIN_NAME\USERNAME`

with your domain name and username and`PASSWORD`

with your password.`kubectl create secret generic smbcreds --from-literal=username=DOMAIN_NAME\USERNAME –from-literal=password="PASSWORD"`

Verify that the secret has been created.

`kubectl get secret`

The output resembles the following example:

`NAME TYPE DATA AGE smbcreds Opaque 2 2h`


### Create a storage class

A storage class is used to define how a unit of storage is dynamically created with a persistent volume. To consume Azure NetApp Files volumes, a storage class must be created.

Create a file named

`anf-storageclass-smb.yaml`

and copy in the following YAML.`apiVersion: storage.k8s.io/v1 kind: StorageClass metadata: name: anf-sc-smb provisioner: csi.trident.netapp.io allowVolumeExpansion: true parameters: backendType: "azure-netapp-files" trident.netapp.io/nasType: "smb" csi.storage.k8s.io/node-stage-secret-name: "smbcreds" csi.storage.k8s.io/node-stage-secret-namespace: "default"`

Create the storage class using the

command:`kubectl apply`

`kubectl apply -f anf-storageclass-smb.yaml`

The output of the command resembles the following example:

`storageclass/anf-sc-smb created`

Run the

command to view the status of the storage class:`kubectl get`

`kubectl get sc anf-sc-smb NAME PROVISIONER RECLAIMPOLICY VOLUMEBINDINGMODE ALLOWVOLUMEEXPANSION AGE anf-sc-smb csi.trident.netapp.io Delete Immediate true 13s`


### Create a PVC

A persistent volume claim (PVC) is a request for storage by a user. Upon the creation of a persistent volume claim, Trident automatically creates an Azure NetApp Files SMB share and makes it available for Kubernetes workloads to consume.

Create a file named

`anf-pvc-smb.yaml`

and copy the following YAML. In this example, a 100-GiB volume is created with`ReadWriteMany`

access and uses the storage class created in[Create a storage class](#create-a-storage-class).`kind: PersistentVolumeClaim apiVersion: v1 metadata: name: anf-pvc-smb spec: accessModes: - ReadWriteMany resources: requests: storage: 100Gi storageClassName: anf-sc-smb`

Create the persistent volume claim with the

command:`kubectl apply`

`kubectl apply -f anf-pvc-smb.yaml`

The output of the command resembles the following example:

`persistentvolumeclaim/anf-pvc-smb created`

To view information about the persistent volume claim, run the

command:`kubectl get`

`kubectl get pvc`

The output of the command resembles the following example:

`NAME STATUS VOLUME CAPACITY ACCESS MODES STORAGECLASS AGE anf-pvc-smb Bound pvc-209268f5-c175-4a23-b61b-e34faf5b6239 100Gi RWX anf-sc-smb 5m38s`

To view the persistent volume created by Trident, run the following

command:`kubectl get`

`kubectl get pv NAME CAPACITY ACCESS MODES RECLAIM POLICY STATUS CLAIM STORAGECLASS REASON AGE pvc-209268f5-c175-4a23-b61b-e34faf5b6239 100Gi RWX Delete Bound default/anf-pvc-smb anf-sc-smb 5m52s`


### Use the persistent volume

After the PVC is created, a pod can be spun up to access the Azure NetApp Files volume. The following manifest can be used to define an Internet Information Services (IIS) pod that mounts the Azure NetApp Files SMB share created in the previous step. In this example, the volume is mounted at `/inetpub/wwwroot`

.

Create a file named

`anf-iis-pod.yaml`

and copy in the following YAML:`apiVersion: v1 kind: Pod metadata: name: iis-pod labels: app: web spec: nodeSelector: "kubernetes.io/os": windows volumes: - name: smb persistentVolumeClaim: claimName: anf-pvc-smb containers: - name: web image: mcr.microsoft.com/windows/servercore/iis:windowsservercore resources: limits: cpu: 1 memory: 800M ports: - containerPort: 80 volumeMounts: - name: smb mountPath: "/inetpub/wwwroot" readOnly: false`

Create the deployment using the

command:`kubectl apply`

`kubectl apply -f anf-iis-deploy-pod.yaml`

The output of the command resembles the following example:

`pod/iis-pod created`

Verify that the pod is running and is mounted via SMB to

`/inetpub/wwwroot`

by using thecommand:`kubectl describe`

`kubectl describe pod iis-pod`

The output of the command resembles the following example:

`Name: iis-pod Namespace: default Priority: 0 Node: akswin000001/10.225.5.246 Start Time: Fri, 05 May 2023 15:16:36 -0400 Labels: app=web Annotations: <none> Status: Running IP: 10.225.5.252 IPs: IP: 10.225.5.252 Containers: web: Container ID: containerd://1e4959f2b49e7ad842b0ec774488a6142ac9152ca380c7ba4d814ae739d5ed3e Image: mcr.microsoft.com/windows/servercore/iis:windowsservercore Image ID: mcr.microsoft.com/windows/servercore/iis@sha256:0f0114d0f6c6ee569e1494953efdecb76465998df5eba951dc760ac5812c7409 Port: 80/TCP Host Port: 0/TCP State: Running Started: Fri, 05 May 2023 15:16:44 -0400 Ready: True Restart Count: 0 Limits: cpu: 1 memory: 800M Requests: cpu: 1 memory: 800M Environment: <none> Mounts: /inetpub/wwwroot from smb (rw) /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-zznzs (ro)`

Verify that your volume has been mounted on the pod by using

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)to connect to the pod. And then use the`dir`

command in the correct directory to check if the volume is mounted and the size matches the size of the volume you provisioned.`kubectl exec -it iis-pod –- cmd.exe`

The output of the command resembles the following example:

`Microsoft Windows [Version 10.0.20348.1668] (c) Microsoft Corporation. All rights reserved. C:\>cd /inetpub/wwwroot C:\inetpub\wwwroot>dir Volume in drive C has no label. Volume Serial Number is 86BB-AA55 Directory of C:\inetpub\wwwroot 05/05/2023 01:38 AM <DIR> . 05/05/2023 01:38 AM <DIR> .. 0 File(s) 0 bytes 2 Dir(s) 107,373,862,912 bytes free C:\inetpub\wwwroot>exit`


## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-storage -->

# Storage options for applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Applications running in Azure Kubernetes Service (AKS) might need to store and retrieve data. While some application workloads can use local, fast storage on unneeded, emptied nodes, others require storage that persists on more regular data volumes within the Azure platform.

Multiple pods might need to:

- Share the same data volumes.
- Reattach data volumes if the pod is rescheduled on a different node.

You also might need to collect and store sensitive data or application configuration information into pods.

This article introduces the core concepts that provide storage to your applications in AKS:

## Default OS disk sizing

### Ephemeral OS disks

If you select a VM SKU that supports Ephemeral OS disks but don't specify an OS disk size, AKS by default provisions an Ephemeral OS disk with a size that scales according to the total temp storage of the VM SKU so long as the temp is *at least 128GiB*. For example, the `Standard_D8ds_v5`

SKU with a temp disk size of 300GiB will receive a 300GiB Ephemeral OS disk by default if the disk parameters are unspecified.

If you want to use the temp storage of the VM SKU, you need to specify the OS disk size during deployment, otherwise it's consumed by default.

Important

Default Ephemeral OS disk sizing is only used on new clusters or node pools where Ephemeral OS disks are supported and a default OS disk size isn't specified. The default OS disk size might impact the performance or cost of your cluster. You can't change the OS disk size after cluster or node pool creation. This default Ephemeral sizing affects clusters or node pools created in March 2025 or later.

### Managed OS disks

When you create a new cluster or add a new node pool to an existing cluster, the number for vCPUs by default determines the OS disk size. The number of vCPUs is based on the VM SKU. The following table lists the default OS disk size for each VM SKU:

| VM SKU Cores (vCPUs) | Default OS Disk Tier | Provisioned IOPS | Provisioned Throughput (Mbps) |
|---|---|---|---|
| 1 - 7 | P10/128G | 500 | 100 |
| 8 - 15 | P15/256G | 1100 | 125 |
| 16 - 63 | P20/512G | 2300 | 150 |
| 64+ | P30/1024G | 5000 | 200 |

Important

Default Managed OS disk sizing is only used on new clusters or node pools when Ephemeral OS disks aren't supported and a default OS disk size isn't specified. The default OS disk size might impact the performance or cost of your cluster. You can't change the OS disk size after cluster or node pool creation. We recommend a minimum disk size of 512G if ephemeral OS disk cannot be used. This default Managed sizing affects clusters or node pools created in July 2022 or later.

## Ephemeral OS disk

By default, Azure automatically replicates the operating system disk for a virtual machine to Azure Storage to avoid data loss when the VM is relocated to another host. However, since containers aren't designed to have local state persisted, this behavior offers limited value while providing some drawbacks. These drawbacks include, but aren't limited to, slower node provisioning and higher read/write latency.

By contrast, Ephemeral OS disks are stored only on the host machine, just like a temporary disk. With this configuration, you get lower read/write latency with faster node scaling and cluster upgrades. Therefore, we strongly **recommend using Ephemeral OS disks whenever possible**.

Note

When you don't explicitly request [Azure managed disks](/en-us/azure/virtual-machines/managed-disks-overview) for the OS, AKS defaults to ephemeral OS if possible for a given node pool configuration.

Size requirements and recommendations for ephemeral OS disks are available in the [Azure VM documentation](/en-us/azure/virtual-machines/ephemeral-os-disks). The following are some general sizing considerations:

If you chose to use the AKS default VM size

[Standard_DS2_v2](/en-us/azure/virtual-machines/dv2-dsv2-series#dsv2-series)SKU with the default OS disk size of 100 GiB, the default VM size supports ephemeral OS, but only has 86 GiB of cache size. This configuration would default to managed disks if you don't explicitly specify it. If you do request an ephemeral OS, you receive a validation error.If you request the same

[Standard_DS2_v2](/en-us/azure/virtual-machines/dv2-dsv2-series#dsv2-series)SKU with a 60-GiB OS disk, this configuration would default to ephemeral OS. The requested size of 60 GiB is smaller than the maximum cache size of 86 GiB.If you select the

[Standard_D8s_v3](/en-us/azure/virtual-machines/dv3-dsv3-series#dsv3-series)SKU with 100-GB OS disk, this VM size supports ephemeral OS and has 200 GiB of cache space. If you don't specify the OS disk type, the node pool would receive ephemeral OS by default.

The latest generation of VM series doesn't have a dedicated cache, but only temporary storage. For example, if you selected the [Standard_E2bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series) VM size with the default OS disk size of 100 GiB, it supports ephemeral OS disks, but only has 75 GB of temporary storage. This configuration would default to managed OS disks if you don't explicitly specify it. If you do request an ephemeral OS disk, you receive a validation error.

If you request the same

[Standard_E2bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series)VM size with a 60-GiB OS disk, this configuration defaults to ephemeral OS disks. The requested size of 60 GiB is smaller than the maximum temporary storage of 75 GiB.If you select

[Standard_E4bds_v5](/en-us/azure/virtual-machines/ebdsv5-ebsv5-series#ebdsv5-series)SKU with 100-GiB OS disk, this VM size supports ephemeral OS and has 150 GiB of temporary storage. If you don't specify the OS disk type, by default Azure provisions an ephemeral OS disk to the node pool.

### Customer-managed keys

You can manage encryption for your ephemeral OS disk with your own keys on an AKS cluster. For more information, see [Use Customer Managed key with Azure disk on AKS](azure-disk-customer-managed-keys).

## Ephemeral NVMe data disks

Ephemeral NVMe data disks provide high-performance, low-latency storage directly attached to the physical host of your Azure VM. These disks are ideal for workloads that require fast, temporary storage for intermediate data processing, such as caching, scratch space, or high-throughput analytics.

Ephemeral NVMe data disks were initially available only on Azure VM L-series, E-series, and GPU VMs. With the introduction of Azure VM v6 and v7 generations, support for ephemeral NVMe data disks has expanded to a much wider range of VM sizes, including D-series, F-series, H-series, and more. NVMe disks deliver significantly higher IOPS and throughput compared to traditional HDD or SSD options. However, data stored on these disks is temporary and will be lost if the VM is deallocated or redeployed.

To simplify management and provisioning of ephemeral NVMe data disks in AKS, use [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction). Azure Container Storage can automatically detect and orchestrate NVMe data disks, allowing you to create and manage persistent volumes for your Kubernetes workloads with minimal configuration. This approach is recommended for scenarios where high-performance, temporary storage is required, such as:

- High-speed caching layers, such as datasets and checkpoints for AI training, or model files used for AI inference
- High-performance, self-hosted databases that include built-in replication and backup features
- Data-intensive analytics and processing pipelines that require fast, temporary storage
- Temporary scratch space for batch jobs

Important

Ephemeral NVMe data disks are not suitable for storing critical or persistent data. Ensure your application can tolerate data loss and that important data is stored on persistent volumes backed by Azure Disk, Azure Files, or other durable storage options.

For more information on using Azure Container Storage with ephemeral NVMe data disks, see [Use Azure Container Storage with AKS](/en-us/azure/storage/container-storage/use-container-storage-with-local-disk).

## Volumes

Kubernetes typically treats individual pods as ephemeral, disposable resources. Applications have different approaches available to them for using and persisting data. A *volume* represents a way to store, retrieve, and persist data across pods and through the application lifecycle.

Traditional volumes are created as Kubernetes resources backed by Azure Storage. You can manually create data volumes to be assigned to pods directly or have Kubernetes automatically create them. Data volumes can use: [Azure Disk](/en-us/azure/virtual-machines/disks-types), [Azure Files](/en-us/azure/storage/files/storage-files-planning), [Azure NetApp Files](/en-us/azure/azure-netapp-files/azure-netapp-files-service-levels), or [Azure Blobs](/en-us/azure/storage/common/storage-account-overview).

Note

Depending on the VM SKU you're using, the Azure Disk CSI driver might have a per-node volume limit. For some high performance VMs (for example, 16 cores), the limit is 64 volumes per node. To identify the limit per VM SKU, review the **Max data disks** column for each VM SKU offered. For a list of VM SKUs offered and their corresponding detailed capacity limits, see [General purpose virtual machine sizes](/en-us/azure/virtual-machines/sizes-general).

To help determine best fit for your workload between Azure Files and Azure NetApp Files, review the information provided in the article [Azure Files and Azure NetApp Files comparison](/en-us/azure/storage/files/storage-files-netapp-comparison).

### Azure Disk

Use [Azure Disk](azure-disk-csi) to create a Kubernetes *DataDisk* resource. Disks types include:

- Premium SSDs (recommended for most workloads)
- Ultra disks
- Standard SSDs
- Standard HDDs

Tip

For most production and development workloads, use Premium SSDs.

Because an Azure Disk is mounted as *ReadWriteOnce*, it's only available to a single node. For storage volumes accessible by pods on multiple nodes simultaneously, use Azure Files.

### Azure Files

Use [Azure Files](azure-files-csi) to mount a Server Message Block (SMB) version 3.1.1 share or Network File System (NFS) version 4.1 share. Azure Files let you share data across multiple nodes and pods and can use:

- Azure Premium storage backed by high-performance SSDs
- Azure Standard storage backed by regular HDDs

### Azure NetApp Files

- Ultra Storage
- Premium Storage
- Standard Storage

### Azure Blob Storage

Use [Azure Blob Storage](azure-blob-csi) to create a blob storage container and mount it using the NFS v3.0 protocol or BlobFuse.

- Block blobs

### Volume types

Kubernetes volumes represent more than just a traditional disk for storing and retrieving information. Kubernetes volumes can also be used as a way to inject data into a pod for use by its containers.

Common volume types in Kubernetes include:

#### emptyDir

Commonly used as temporary space for a pod. All containers within a pod can access the data on the volume. Data written to this volume type persists only for the lifespan of the pod. Once you delete the pod, the volume is deleted. This volume typically uses the underlying local node disk storage, though it can also exist only in the node's memory.

#### secret

You can use *secret* volumes to inject sensitive data into pods, such as passwords.

- Create a secret using the Kubernetes API.
- Define your pod or deployment and request a specific secret.
- Secrets are only provided to nodes with a scheduled pod that requires them.
- The secret is stored in
*tmpfs*, not written to disk.

- When you delete the last pod on a node requiring a secret, the secret is deleted from the node's tmpfs.
- Secrets are stored within a given namespace and are only accessed by pods within the same namespace.


#### configMap

You can use *configMap* to inject key-value pair properties into pods, such as application configuration information. Define application configuration information as a Kubernetes resource, easily updated and applied to new instances of pods as they're deployed.

Like using a secret:

- Create a ConfigMap using the Kubernetes API.
- Request the ConfigMap when you define a pod or deployment.
- ConfigMaps are stored within a given namespace and are only accessed by pods within the same namespace.


## Persistent volumes

Volumes defined and created as part of the pod lifecycle only exist until you delete the pod. Pods often expect their storage to remain if a pod is rescheduled on a different host during a maintenance event, especially in StatefulSets. A *persistent volume* (PV) is a storage resource created and managed by the Kubernetes API that can exist beyond the lifetime of an individual pod.

You can use the following Azure Storage services to provide the persistent volume:

As noted in the [Volumes](#volumes) section, the choice of Azure Disks or Azure Files is often determined by the need for concurrent access to the data or the performance tier.

A cluster administrator can *statically* create a persistent volume, or a volume can be created *dynamically* by the Kubernetes API server. If a pod is scheduled and requests storage that is currently unavailable, Kubernetes can create the underlying Azure Disk or File storage and attach it to the pod. Dynamic provisioning uses a *storage class* to identify what type of resource needs to be created.

Important

Persistent volumes can't be shared by Windows and Linux pods due to differences in file system support between the two operating systems.

If you want a fully managed solution for block-level access to data, consider using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction) instead of CSI drivers. Azure Container Storage integrates with Kubernetes, allowing dynamic and automatic provisioning of persistent volumes. Azure Container Storage supports Azure Disks, Ephemeral Disks, and Azure Elastic SAN (preview) as backing storage, offering flexibility and scalability for stateful applications running on Kubernetes clusters.

## Storage classes

To specify different tiers of storage, such as premium or standard, you can create a *storage class*.

A storage class also defines a *reclaim policy*. When you delete the persistent volume, the reclaim policy controls the behavior of the underlying Azure Storage resource. The underlying resource can either be deleted or kept for use with a future pod.

For clusters using [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction), you'll see an additional storage class called `acstor-<storage-pool-name>`

. An internal storage class is also created.

For clusters using [Container Storage Interface (CSI) drivers](csi-storage-drivers), the following extra storage classes are created:

| Storage class | Description |
|---|---|
`managed-csi` |
Uses Azure Standard SSD locally redundant storage (LRS) to create a managed disk. The reclaim policy ensures that the underlying Azure Disk is deleted when the persistent volume that used it is deleted. The storage class also configures the persistent volumes to be expandable. You can edit the persistent volume claim to specify the new size. Effective starting with Kubernetes version 1.29, in Azure Kubernetes Service (AKS) clusters deployed across multiple availability zones, this storage class utilizes Azure Standard SSD zone-redundant storage (ZRS) to create managed disks. |
`managed-csi-premium` |
Uses Azure Premium locally redundant storage (LRS) to create a managed disk. The reclaim policy again ensures that the underlying Azure Disk is deleted when the persistent volume that used it is deleted. Similarly, this storage class allows for persistent volumes to be expanded. Effective starting with Kubernetes version 1.29, in Azure Kubernetes Service (AKS) clusters deployed across multiple availability zones, this storage class utilizes Azure Premium zone-redundant storage (ZRS) to create managed disks. |
`azurefile-csi` |
Uses Azure Standard storage to create an Azure file share. The reclaim policy ensures that the underlying Azure file share is deleted when the persistent volume that used it is deleted. |
`azurefile-csi-premium` |
Uses Azure Premium storage to create an Azure file share. The reclaim policy ensures that the underlying Azure file share is deleted when the persistent volume that used it is deleted. |
`azureblob-nfs-premium` |
Uses Azure Premium storage to create an Azure Blob storage container and connect using the NFS v3 protocol. The reclaim policy ensures that the underlying Azure Blob storage container is deleted when the persistent volume that used it is deleted. |
`azureblob-fuse-premium` |
Uses Azure Premium storage to create an Azure Blob storage container and connect using BlobFuse. The reclaim policy ensures that the underlying Azure Blob storage container is deleted when the persistent volume that used it is deleted. |

Unless you specify a storage class for a persistent volume, the default storage class is used. Ensure volumes use the appropriate storage you need when requesting persistent volumes.

Important

Starting with Kubernetes version 1.21, AKS uses CSI drivers by default, and CSI migration is enabled. While existing in-tree persistent volumes continue to function, starting with version 1.26, AKS will no longer support volumes created using in-tree driver and storage provisioned for files and disk.

The `default`

class will be the same as `managed-csi`

.

Effective starting with Kubernetes version 1.29, when you deploy Azure Kubernetes Service (AKS) clusters across multiple availability zones, AKS now utilizes zone-redundant storage (ZRS) to create managed disks within built-in storage classes. ZRS ensures synchronous replication of your Azure managed disks across multiple Azure availability zones in your chosen region. This redundancy strategy enhances the resilience of your applications and safeguards your data against datacenter failures.

However, it's important to note that zone-redundant storage (ZRS) comes at a higher cost compared to locally redundant storage (LRS). If cost optimization is a priority, you can create a new storage class with the `skuname`

parameter set to LRS. You can then use the new storage class in your Persistent Volume Claim (PVC).

You can create a storage class for other needs using `kubectl`

. The following example uses premium managed disks and specifies that the underlying Azure Disk should be *retained* when you delete the pod:

```
apiVersion: storage.k8s.io/v1
kind: StorageClass
metadata:
name: managed-premium-retain
provisioner: disk.csi.azure.com
parameters:
skuName: Premium_ZRS
reclaimPolicy: Retain
volumeBindingMode: WaitForFirstConsumer
allowVolumeExpansion: true
```


Note

AKS reconciles the default storage classes and will overwrite any changes you make to those storage classes.

For more information about storage classes, see [StorageClass in Kubernetes](https://kubernetes.io/docs/concepts/storage/storage-classes/).

## Persistent volume claims

A persistent volume claim (PVC) requests storage of a particular storage class, access mode, and size. The Kubernetes API server can dynamically provision the underlying Azure Storage resource if no existing resource can fulfill the claim based on the defined storage class.

The pod definition includes the volume mount once the volume has been connected to the pod.

Once an available storage resource has been assigned to the pod requesting storage, the persistent volume is *bound* to a persistent volume claim. Persistent volumes are mapped to claims in a 1:1 mapping.

The following example YAML manifest shows a persistent volume claim that uses the *managed-premium* storage class and requests an Azure Disk that is *5Gi* in size:

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: azure-managed-disk
spec:
accessModes:
- ReadWriteOnce
storageClassName: managed-premium-retain
resources:
requests:
storage: 5Gi
```


When you create a pod definition, you also specify:

- The persistent volume claim to request the desired storage.
- The
*volume mount*for your applications to read and write data.

The following example YAML manifest shows how the previous persistent volume claim can be used to mount a volume at */mnt/azure*:

```
kind: Pod
apiVersion: v1
metadata:
name: nginx
spec:
containers:
- name: myfrontend
image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
volumeMounts:
- mountPath: "/mnt/azure"
name: volume
volumes:
- name: volume
persistentVolumeClaim:
claimName: azure-managed-disk
```


For mounting a volume in a Windows container, specify the drive letter and path. For example:

```
...
volumeMounts:
- mountPath: "d:"
name: volume
- mountPath: "c:\k"
name: k-dir
...
```


## Next steps

For associated best practices, see [Best practices for storage and backups in AKS](operator-best-practices-storage) and [AKS storage considerations](/en-us/azure/cloud-adoption-framework/scenarios/app-platform/aks/storage).

For more information on Azure Container Storage, see the following articles:

For more information on using CSI drivers, see the following articles:

[Container Storage Interface (CSI) drivers for Azure Disk, Azure Files, and Azure Blob storage on Azure Kubernetes Service](csi-storage-drivers)[Use Azure Disk CSI driver in Azure Kubernetes Service](azure-disk-csi)[Use Azure Files CSI driver in Azure Kubernetes Service](azure-files-csi)[Use Azure Blob storage CSI driver in Azure Kubernetes Service](azure-blob-csi)[Configure Azure NetApp Files with Azure Kubernetes Service](azure-netapp-files)

For more information on core Kubernetes and AKS concepts, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-network-ingress -->

# Ingress in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Ingress in AKS is a Kubernetes resource that manages external HTTP-like traffic access to [services](concepts-network-services) within a cluster. An AKS ingress may provide services like load balancing, SSL termination, and name-based virtual hosting. For more information about Kubernetes Ingress, see the [Kubernetes Ingress documentation](https://kubernetes.io/docs/concepts/services-networking/ingress/).

## Ingress controllers

When managing application traffic, Ingress controllers provide advanced capabilities by operating at layer 7. They can route HTTP traffic to different applications based on the inbound URL, allowing for more intelligent and flexible traffic distribution rules. For example, an ingress controller can direct traffic to different microservices depending on the URL path, enhancing the efficiency and organization of your services.

On the other hand, a LoadBalancer-type Service, when created, sets up an underlying Azure load balancer resource. This load balancer works at layer 4, distributing traffic to the pods in your Service on a specified port. However, layer 4 services are unaware of the actual applications and can't implement these types of complex routing rules.

Understanding the distinction between these two approaches helps in selecting the right tool for your traffic management needs.

## Compare ingress options

The following table lists the feature differences between the different ingress controller options:

| Feature | Application Routing addon | Application Gateway for Containers | Azure Service Mesh/Istio-based service mesh |
|---|---|---|---|
Ingress/Gateway controller |
NGINX ingress controller | Azure Application Gateway for Containers | Istio Ingress Gateway |
API |
Ingress API | Ingress API and Gateway API |
|

**Hosting****Scaling****Load balancing****SSL termination****mTLS****Static IP Address****Azure Key Vault stored SSL certificates****Azure DNS integration for DNS zone management**The following table lists the different scenarios where you might use each ingress controller:

| Ingress option | When to use |
|---|---|
Managed NGINX - Application Routing addon |
• In-cluster hosted, customizable, and scalable NGINX ingress controllers. • Basic load balancing and routing capabilities. • Internal and external load balancer configuration. • Static IP address configuration. • Integration with Azure Key Vault for certificate management. • Integration with Azure DNS Zones for public and private DNS management. • Supports the Ingress API. |
Application Gateway for Containers |
• Azure hosted ingress gateway. • Flexible deployment strategies managed by the controller or bring your own Application Gateway for Containers. • Advanced traffic management features such as automatic retries, availability zone resiliency, mutual authentication (mTLS) to backend target, traffic splitting / weighted round robin, and autoscaling. • Integration with Azure Key Vault for certificate management. • Integration with Azure DNS Zones for public and private DNS management. • Supports the Ingress and Gateway APIs. |
Istio Ingress Gateway |
• Based on Envoy, when using with Istio for a service mesh. • Advanced traffic management features such as rate limiting and circuit breaking. • Support for mTLS |

Note

Gateway API for [Istio ingress traffic](istio-deploy-ingress) is not yet supported for the Istio add-on, but is currently under active development.

## Create an Ingress resource

The application routing addon is the recommended way to configure an Ingress controller in AKS. The application routing addon is a fully managed ingress controller for Azure Kubernetes Service (AKS) that provides the following features:

Easy configuration of managed NGINX Ingress controllers based on Kubernetes NGINX Ingress controller.

Integration with Azure DNS for public and private zone management.

SSL termination with certificates stored in Azure Key Vault.


For more information about the application routing addon, see [Managed NGINX ingress with the application routing add-on](app-routing).

## Client source IP preservation

Configure your ingress controller to preserve the client source IP on requests to containers in your AKS cluster. When your ingress controller routes a client's request to a container in your AKS cluster, the original source IP of that request is unavailable to the target container. When you enable *client source IP preservation*, the source IP for the client is available in the request header under *X-Forwarded-For*.

If you're using client source IP preservation on your ingress controller, you can't use TLS pass-through. Client source IP preservation and TLS pass-through can be used with other services, such as the *LoadBalancer* type.

To learn more about client source IP preservation, see [How client source IP preservation works for LoadBalancer Services in AKS](https://techcommunity.microsoft.com/t5/fasttrack-for-azure/how-client-source-ip-preservation-works-for-loadbalancer/ba-p/3033722#:%7E:text=Enable%20Client%20source%20IP%20preservation%201%20Edit%20loadbalancer,is%20the%20same%20as%20the%20source%20IP%20%28srjumpbox%29.).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kubelet-logs -->

# Get kubelet logs from Azure Kubernetes Service cluster nodes

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

You might need to review logs to troubleshoot a problem in your Azure Kubernetes Service (AKS) cluster. You can use tools in the Azure portal to view logs for AKS [main components](monitor-aks-reference#resource-logs) and [cluster containers](/en-us/azure/azure-monitor/containers/container-insights-overview). Occasionally, you might need to get *kubelet* logs from AKS nodes to help you troubleshoot an issue.

This article shows you how to use `journalctl`

to view kubelet logs on an AKS node.

Alternatively, you can collect kubelet logs by using the [syslog collection feature in Container insights in Azure Monitor](https://aka.ms/CISyslog).

## Before you begin

This article assumes that you have an existing AKS cluster. If you need an AKS cluster, create one by using the [Azure CLI](learn/quick-kubernetes-deploy-cli), [Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the [Azure portal](learn/quick-kubernetes-deploy-portal).

## Connect to your AKS cluster

To interact with your AKS cluster, first get the cluster credentials by using the Azure CLI:

```
export RESOURCE_GROUP_NAME="<ResourceGroupName>"
export AKS_CLUSTER_NAME="<AKSClusterName>"
az aks get-credentials --resource-group $RESOURCE_GROUP_NAME --name $AKS_CLUSTER_NAME
```


This command configures kubectl to use the credentials for your AKS cluster.

## Use the kubectl raw command

You can quickly view any node's kubelet logs by using the following command:

```
export NODE_NAME="aks-agentpool-xxxxxxx-0"
kubectl get --raw "/api/v1/nodes/$NODE_NAME/proxy/logs/messages" | grep kubelet
```


Results:

```
I0508 12:26:17.905042 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:27.943494 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:28.920125 8672 server.go:796] GET /stats/summary: (10.370874ms) 200 [[Ruby] 10.244.0.x:52492]
I0508 12:26:37.964650 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
...
```


## Create an SSH connection

You must create a Secure Shell Protocol (SSH) connection with the node you need to view kubelet logs for. To create this connection, complete the steps that are described in [SSH into AKS cluster nodes](ssh).

## Get kubelet logs

After you connect to the node by using `kubectl debug`

, run the following command to pull the kubelet logs:

```
chroot /host
journalctl -u kubelet -o cat
```


Note

For Windows nodes, the log data is in `C:\k`

and can be viewed by using the `more`

command:

```
more C:\k\kubelet.log
```


The following example output shows kubelet log data:

```
I0508 12:26:17.905042 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:27.943494 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:28.920125 8672 server.go:796] GET /stats/summary: (10.370874ms) 200 [[Ruby] 10.244.0.x:52292]
I0508 12:26:37.964650 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:47.996449 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:26:58.019746 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:05.107680 8672 server.go:796] GET /stats/summary/: (24.853838ms) 200 [[Go-http-client/1.1] 10.244.0.x:44660]
I0508 12:27:08.041736 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:18.068505 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:28.094889 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:38.121346 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:44.015205 8672 server.go:796] GET /stats/summary: (30.236824ms) 200 [[Ruby] 10.244.0.x:52588]
I0508 12:27:48.145640 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:27:58.178534 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:05.040375 8672 server.go:796] GET /stats/summary/: (27.78503ms) 200 [[Go-http-client/1.1] 10.244.0.x:44660]
I0508 12:28:08.214158 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:18.242160 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:28.274408 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:38.296074 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:48.321952 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
I0508 12:28:58.344656 8672 kubelet_node_status.go:497] Using Node Hostname from cloudprovider: "aks-agentpool-xxxxxxx-0"
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-pod-sandboxing -->

# Pod Sandboxing with Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

To help secure and protect your container workloads from untrusted or potentially malicious code, AKS now includes a mechanism called Pod Sandboxing. Pod Sandboxing provides an isolation boundary between the container application and the shared kernel and compute resources of the container host such as CPU, memory, and networking. Applications are spun up in isolated, lightweight pod virtual machines (VMs). Pod Sandboxing complements other security measures or data protection controls with your overall architecture to help you meet regulatory, industry, or governance compliance requirements for securing sensitive information.

This article helps you understand this new feature, and how to implement it.

## Prerequisites

The Azure CLI version 2.80.0 or later. Run

`az --version`

to find the version of your Azure CLI, and run`az upgrade`

to upgrade. For more details, see the steps at[Install Azure CLI](/en-us/cli/azure/install-azure-cli).AKS supports Pod Sandboxing on Kubernetes version 1.27.0 and higher.

To manage a Kubernetes cluster, use the Kubernetes command-line client

[kubectl](https://kubernetes.io/docs/reference/kubectl/). Azure Cloud Shell comes with`kubectl`

. You can install kubectl locally using the[az aks install-cli](/en-us/cli/azure/aks#az-aks-install-cli)command.

## Limitations

The following are constraints applicable to Pod Sandboxing:

Kata containers might not reach the IOPS performance limits that traditional containers can reach on Azure Files and high-performance local SSD.

[Microsoft Defender for Containers](/en-us/azure/defender-for-cloud/defender-for-containers-introduction)doesn't support assessing Kata runtime pods.[Kata](https://github.com/kata-containers/kata-containers/blob/main/docs/Limitations.md#host-network)host-network access isn't supported. It isn't possible to directly access the host networking configuration from within the VM.CPU and memory allocation with Pod Sandboxing has other considerations compared to

`runc`

. Reference the memory management sections in the[considerations page](considerations-pod-sandboxing).

## How it works

Pod Sandboxing on AKS builds on top of the open-source [Kata Containers](https://katacontainers.io/) project. Kata Containers running on the Azure Linux container host for AKS provides VM based isolation and a separate kernel for each pod. Pod Sandboxing allows users to allocate resources for each pod and doesn't share them with other Kata Containers or namespace containers running on the same host.

The solution architecture is based on the following main components:

- The
[Azure Linux container host for AKS](use-azure-linux) - Microsoft Hyper-V Hypervisor
- Open-source
[Cloud-Hypervisor](https://www.cloudhypervisor.org)Virtual Machine Monitor (VMM) - Integration with
[Kata Container](https://katacontainers.io)for the runtime

Deploying Pod Sandboxing using Kata Containers is similar to the standard `containerd`

workflow to deploy containers. Clusters with Pod Sandboxing enabled come with a specific runtime class that can be referenced in a pod manifest (`runtimeClassName: kata-vm-isolation`

).

To use this feature with a pod, the only difference is to add the **runtimeClassName**, `kata-vm-isolation`

to the pod spec. When a pod uses the `kata-vm-isolation`

runtimeClass, the hypervisor spins up a lightweight virtual machine with its own kernel, for the workload to operate in.

## Deploy new cluster

Perform the following steps to deploy an Azure Linux AKS cluster using the Azure CLI.

Create an AKS cluster using the

[az aks create](/en-us/cli/azure/aks#az-aks-create)command and specifying the following parameters:**--workload-runtime**: Specify*KataVmIsolation*to enable the Pod Sandboxing feature on the node pool. With this parameter, these other parameters should satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameters.**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature.**--node-vm-size**: Any Azure VM size that is a generation 2 VM and supports nested virtualization works. For example,[Dsv3](/en-us/azure/virtual-machines/dv3-dsv3-series#dsv3-series)VMs.

The following example creates a cluster named

*myAKSCluster*with one node in the*myResourceGroup*:`az aks create --name myAKSCluster \ --resource-group myResourceGroup \ --os-sku AzureLinux \ --workload-runtime KataVmIsolation \ --node-vm-size Standard_D4s_v3 \ --node-count 3 \ --generate-ssh-keys`

Run the following command to get access credentials for the Kubernetes cluster. Use the

[az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials)command and replace the values for the cluster name and the resource group name.`az aks get-credentials --resource-group myResourceGroup --name myAKSCluster`

List all Pods in all namespaces using the

[kubectl get pods](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#get)command.`kubectl get pods --all-namespaces`


## Deploy to an existing cluster

To use this feature with an existing AKS cluster, the following requirements must be met:

- Verify the cluster is running Kubernetes version 1.27.0 and higher.

Use the following command to enable Pod Sandboxing by creating a node pool to host it.

Add a node pool to your AKS cluster using the

[az aks nodepool add](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add)command. Specify the following parameters:**--resource-group**: Enter the name of an existing resource group to create the AKS cluster in.**--cluster-name**: Enter a unique name for the AKS cluster, such as*myAKSCluster*.**--name**: Enter a unique name for your clusters node pool, such as*nodepool2*.**--workload-runtime**: Specify*KataVmIsolation*to enable the Pod Sandboxing feature on the node pool. Along with the`--workload-runtime`

parameter, these other parameters shall satisfy the following requirements. Otherwise, the command fails and reports an issue with the corresponding parameter.**--os-sku**:*AzureLinux*. Only the Azure Linux os-sku supports this feature.**--node-vm-size**: Any Azure VM size that is a generation 2 VM and supports nested virtualization works. For example,[Dsv3](/en-us/azure/virtual-machines/dv3-dsv3-series#dsv3-series)VMs.


The following example adds a node pool to

*myAKSCluster*with one node in*nodepool2*in the*myResourceGroup*:`az aks nodepool add --cluster-name myAKSCluster --resource-group myResourceGroup --name nodepool2 --os-sku AzureLinux --workload-runtime KataVmIsolation --node-vm-size Standard_D4s_v3`

Run the

[az aks update](/en-us/cli/azure/aks#az-aks-update)command to enable pod sandboxing on the cluster.`az aks update --name myAKSCluster --resource-group myResourceGroup`


## Deploying your applications

With Pod Sandboxing, you can deploy a mix of "normal" pods that don't utilize the Kata runtime alongside Kata pods that do utilize the runtime. The main difference between the two, when deploying, lies in the fact that a Kata pod has the line `runtimeClassName: kata-vm-isolation`

in its spec.

### Deploy an application with the Kata runtime

To deploy a pod with the Kata runtime on your AKS cluster, perform the following steps.

Create a file named

*kata-app.yaml*to describe your kata pod, and then paste the following manifest.`kind: Pod apiVersion: v1 metadata: name: isolated-pod spec: runtimeClassName: kata-vm-isolation containers: - name: kata image: mcr.microsoft.com/aks/fundamental/base-ubuntu:v0.0.11 command: ["/bin/sh", "-ec", "while :; do echo '.'; sleep 5 ; done"]`

The value for

**runtimeClassNameSpec**is`kata-vm-isolation`

.Deploy the Kubernetes pod by running the

[kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply)command and specify your*kata-app.yaml*file:`kubectl apply -f kata-app.yaml`

The output of the command resembles the following example:

`pod/isolated-pod created`


## (Optional) Verify Kernel Isolation configuration

If you would like to verify the difference between the kernel of a Kata and non-Kata pod, you can spin up another workload that doesn't have the Kata runtime.

```
kind: Pod
apiVersion: v1
metadata:
name: normal-pod
spec:
containers:
- name: non-kata
image: mcr.microsoft.com/aks/fundamental/base-ubuntu:v0.0.11
command: ["/bin/sh", "-ec", "while :; do echo '.'; sleep 5 ; done"]
```


To access a container inside the AKS cluster, start a shell session by running the

[kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec)command. In this example, you're accessing the container inside*kata-pod*.`kubectl exec -it isolated-pod -- /bin/sh`

Kubectl connects to your cluster, runs

`/bin/sh`

inside the first container within`isolated-pod`

, and forwards your terminal's input and output streams to the container's process. You can also start a shell session to the container hosting the non-Kata pod to see the differences.After starting a shell session to the container from

*kata-pod*, you can run commands to verify that the*kata*container is running in a pod sandbox. Notice that it has a different kernel version compared to the non-Kata container outside the sandbox.To see the kernel version run the following command:

`uname -r`

The following example resembles output from the pod sandbox kernel:

`[user]/# uname -r 6.6.96.mshv1`

Start a shell session to the container from

*normal-pod*to verify the kernel output:`kubectl exec -it normal-pod -- /bin/bash`

To see the kernel version run the following command:

`uname -r`

The following example resembles output from the VM that's running

*normal-pod*, which is a different kernel than the Kata pod running within the pod sandbox:`6.6.100.mshv1-1.azl3`


## Cleanup

When you're finished evaluating this feature, to avoid Azure charges, clean up your unnecessary resources. If you deployed a new cluster as part of your evaluation or testing, you can delete the cluster using the [az aks delete](/en-us/cli/azure/aks#az-aks-delete) command.

```
az aks delete --resource-group myResourceGroup --name myAKSCluster
```


If you deployed Pod Sandboxing on an existing cluster, you can remove the pods using the [kubectl delete pod](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#delete) command.

```
kubectl get pods
kubectl delete pod <kata-pod-name>
```


## Next steps

- Learn more about
[Azure Dedicated hosts](use-azure-dedicated-hosts)for nodes with your AKS cluster to use hardware isolation and control over Azure platform maintenance events. - To further explore Pod Sandboxing isolation and explore workload scenarios, try out the
[Pod Sandboxing labs](https://azure-samples.github.io/aks-labs/docs/security/pod-sandboxing-on-aks).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-about -->

# Open Service Mesh (OSM) add-on in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Open Service Mesh (OSM)](https://docs.openservicemesh.io/) is a lightweight, extensible, cloud native service mesh that allows you to uniformly manage, secure, and get out-of-the-box observability features for highly dynamic microservice environments.

OSM runs an Envoy-based control plane on Kubernetes and can be configured with [SMI](https://smi-spec.io/) APIs. OSM works by injecting an Envoy proxy as a sidecar container with each instance of your application. The Envoy proxy contains and executes rules around access control policies, implements routing configuration, and captures metrics. The control plane continually configures the Envoy proxies to ensure policies and routing rules are up to date and proxies are healthy.

Microsoft started the OSM project, but it's now governed by the [Cloud Native Computing Foundation (CNCF)](https://www.cncf.io/).

Important

Starting on **September 30, 2027**, Azure Kubernetes Service (AKS) no longer supports the Open Service Mesh (OSM) add-on. The [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/) retired the upstream OSM project. [Migrate any existing OSM configurations to equivalent Istio configurations](/en-us/azure/aks/open-service-mesh-istio-migration-guidance). For more information on this retirement, see the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

## Enable the OSM add-on

OSM can be added to your Azure Kubernetes Service (AKS) cluster by enabling the OSM add-on using the [Azure CLI](open-service-mesh-deploy-addon-az-cli) or a [Bicep template](open-service-mesh-deploy-addon-bicep). The OSM add-on provides a fully supported installation of OSM that's integrated with AKS.

Important

Based on the version of Kubernetes your cluster is running, the OSM add-on installs a different version of OSM.

| Kubernetes version | OSM version installed |
|---|---|
| 1.24.0 or greater | 1.2.5 |
| Between 1.23.5 and 1.24.0 | 1.1.3 |
| Below 1.23.5 | 1.0.0 |

Older versions of OSM may not be available for install or be actively supported if the corresponding AKS version has reached end of life. You can check the [AKS Kubernetes release calendar](supported-kubernetes-versions#aks-kubernetes-release-calendar) for information on AKS version support windows.

## Capabilities and features

OSM provides the following capabilities and features:

- Secure service-to-service communication by enabling mutual TLS (mTLS).
- Onboard applications onto the OSM mesh using automatic sidecar injection of Envoy proxy.
- Transparently configure traffic shifting on deployments.
- Define and execute fine-grained access control policies for services.
- Monitor and debug services using observability and insights into application metrics.
- Encrypt communications between service endpoints deployed in the cluster.
- Enable traffic authorization of both HTTP/HTTPS and TCP traffic.
- Configure weighted traffic controls between two or more services for A/B testing or canary deployments.
- Collect and view KPIs from application traffic.
- Integrate with external certificate management.
- Integrate with existing ingress solutions such as
[NGINX](https://github.com/kubernetes/ingress-nginx),[Contour](https://projectcontour.io/), and[Application Routing](app-routing).

For more information on ingress and OSM, see [Using ingress to manage external access to services within the cluster](https://release-v1-2.docs.openservicemesh.io/docs/guides/traffic_management/ingress/) and [Integrate OSM with Contour for ingress](https://release-v1-2.docs.openservicemesh.io/docs/demos/ingress_contour). For an example of how to integrate OSM with ingress controllers using the `networking.k8s.io/v1`

API, see [Ingress with Kubernetes Nginx ingress controller](https://release-v1-2.docs.openservicemesh.io/docs/demos/ingress_k8s_nginx). For more information on using Application Routing, which automatically integrates with OSM, see [Application Routing](app-routing).

## Limitations

The OSM AKS add-on has the following limitations:

- After installation, you must enable Iptables redirection for port IP address and port range exclusion using
`kubectl patch`

. For more information, see[iptables redirection](https://release-v1-2.docs.openservicemesh.io/docs/guides/traffic_management/iptables_redirection/). - Any pods that need access to IMDS, Azure DNS, or the Kubernetes API server must have their IP addresses added to the global list of excluded outbound IP ranges using
[Global outbound IP range exclusions](https://release-v1-2.docs.openservicemesh.io/docs/guides/traffic_management/iptables_redirection/#global-outbound-ip-range-exclusions).

- The add-on doesn't work on AKS clusters that are using
[Istio based service mesh addon for AKS](istio-about).

- OSM doesn't support Windows Server containers.

## Next steps

After enabling the OSM add-on using the [Azure CLI](open-service-mesh-deploy-addon-az-cli) or a [Bicep template](open-service-mesh-deploy-addon-bicep), you can:

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/app-routing-nginx-prometheus -->

# Monitor the ingress-nginx controller metrics in the application routing add-on with Prometheus and Grafana

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

The ingress-nginx controller in the application routing add-on exposes many metrics for requests, the nginx process, and the controller that can be helpful in analyzing the performance and usage of your application.

The application routing add-on exposes the Prometheus metrics endpoint at `/metrics`

on port 10254 and a private Service `nginx-metrics`

.

## Prerequisites

- An Azure Kubernetes Service (AKS) cluster with the
[application routing add-on enabled](/en-us/azure/aks/app-routing). - A Prometheus instance, such as Azure Monitor managed service for Prometheus.

## Validating the metrics endpoint

To validate the metrics are being collected, you can set up a port forward from a local port to port 10254 on the `nginx-metrics`

service.

```
kubectl port-forward -n app-routing-system service/nginx-metrics :10254
```


```
Forwarding from 127.0.0.1:43307 -> 10254
Forwarding from [::1]:43307 -> 10254
```


Note the local port (`43307`

in this case) and open http://localhost:43307/metrics in your browser. You should see the ingress-nginx controller metrics loading.

You can now terminate the `port-forward`

process to close the forwarding.

## Configuring Azure Monitor managed service for Prometheus

Azure Monitor managed service for Prometheus is a fully managed Prometheus-compatible service that supports industry standard features such as PromQL, Grafana dashboards, and Prometheus alerts. This service requires configuring the metrics addon for the Azure Monitor agent, which sends data to Prometheus. If your cluster isn't configured with the add-on, you can follow this article to configure your Azure Kubernetes Service (AKS) cluster to send data to Azure Monitor managed service for Prometheus.

### Enable Service Monitor based scraping

Once your cluster is updated with the Azure Monitor agent, you need to configure the agent to enable scraping the metrics endpoint. You can [create a Pod or a Service Monitor](/en-us/azure/azure-monitor/containers/prometheus-metrics-scrape-crd) to accomplish this.

The following creates a Service Monitor scrape metrics from the ingress-nginx controller deployed by the application routing add-on.

```
kubectl apply -f - <<EOF
apiVersion: azmonitoring.coreos.com/v1
kind: ServiceMonitor
metadata:
name: nginx-monitor
namespace: app-routing-system
spec:
labelLimit: 63
labelNameLengthLimit: 511
labelValueLengthLimit: 1023
selector:
matchLabels:
app.kubernetes.io/component: ingress-controller
app.kubernetes.io/managed-by: aks-app-routing-operator
app.kubernetes.io/name: nginx
endpoints:
- port: prometheus
EOF
```


In a few minutes, the `ama-metrics`

pods in the `kube-system`

namespace should restart and pick up the new configuration.

## Review visualization of metrics in Azure Managed Grafana

Now that you have Azure Monitor managed service for Prometheus and Azure Managed Grafana configured, you should [access your Managed Grafana instance](/en-us/azure/managed-grafana/quickstart-managed-grafana-portal#access-your-managed-grafana-instance).

There are two [official ingress-nginx dashboards](https://github.com/kubernetes/ingress-nginx/tree/main/deploy/grafana/dashboards) dashboards that you can download and import into your Grafana instance:

- Ingress-nginx controller dashboard
- Request handling performance dashboard

### Ingress-nginx controller dashboard

This dashboard gives you visibility of request volume, connections, success rates, config reloads and configs out of sync. You can also use it to view the network IO pressure, memory and CPU use of the ingress controller. Finally, it also shows the P50, P95, and P99 percentile response times of your ingresses and their throughput.

You can download this dashboard from [GitHub](https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/grafana/dashboards/nginx.json).

### Request handling performance dashboard

This dashboard gives you visibility into the request handling performance of the different ingress upstream destinations, which are your applications' endpoints that the ingress controller is forwarding traffic to. It shows the P50, P95 and P99 percentile of total request and upstream response times. You can also view aggregates of request errors and latency. Use this dashboard to review and improve the performance and scalability of your applications.

You can download this dashboard from [GitHub](https://raw.githubusercontent.com/kubernetes/ingress-nginx/main/deploy/grafana/dashboards/request-handling-performance.json).

### Importing a dashboard

To import a Grafana dashboard, expand the left menu and click on **Import** under Dashboards.

Then upload the desired dashboard file and click on **Load**.

## Next steps

- You can configure scaling your workloads using ingress metrics scraped with Prometheus using
[Kubernetes Event Driven Autoscaler (KEDA)](/en-us/azure/aks/keda-about). Learn more about[integrating KEDA with AKS](/en-us/azure/azure-monitor/essentials/integrate-keda#scalers). - Create and run a load test with
[Azure Load Testing](/en-us/azure/load-testing/quickstart-create-and-run-load-test)to test workload performance and optimize the scalability of your applications.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-fqdn-filtering-policies -->

# Set up FQDN filtering feature for Container Network Security in Advanced Container Networking Services

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to set up Advanced Container Networking Services with Container Network Security feature in AKS clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.71.0. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations:

- Wildcard FQDN policies are partially supported. This means you can create policies that match specific patterns with a leading wildcard (for example,
*.example.com), but you can't use a universal wildcard (*) to match all domains on the field`spec.egress.toPorts.rules.dns.matchPattern`


Supported Pattern:

`*.example.com`

- This allows traffic to all subdomains under example.com.`app*.example.com`

- This rule is more specific and only allows traffic to subdomains that start with "app" under example.comUnsupported Pattern

`*`

This attempt to match any domain name, which isn't supported.

- FQDN filtering is currently not supported with node-local DNS.
- Kubernetes service names aren't supported.
- Other L7 policies aren't supported.
- FQDN pods might exhibit performance degradation when handling more than 1,000 requests per second.
- If Advanced Container Networking Services(ACNS) security is disabled, FQDN and L7 policies (HTTP, HTTPS, Kafka, and gRPC) will be blocked.
- Alpine-based container images might encounter DNS resolution issues when used with Cilium Network Policies. This is due to musl libc's limited search domain iteration. To work around this, explicitly define all search domains in the Network Policy's DNS rules using wildcard patterns, like the below example

```
rules:
dns:
- matchPattern: "*.example.com"
- matchPattern: "*.example.com.*.*"
- matchPattern: "*.example.com.*.*.*"
- matchPattern: "*.example.com.*.*.*.*"
- matchPattern: "*.example.com.*.*.*.*.*"
- toFQDNs:
- matchPattern: "*.example.com"
```


### Enable Advanced Container Networking Services

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability).**Container Network Security:**Offers security features like Fully Qualified Domain Name (FQDN) filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security).

```
# Set an environment variable for the AKS cluster name. Make sure to replace the placeholder with your own value.
export CLUSTER_NAME="<aks-cluster-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--generate-ssh-keys \
--location eastus \
--network-plugin azure \
--network-dataplane cilium \
--node-count 2 \
--enable-acns
```


### Enable Advanced Container Networking Services on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features which includes [Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security)feature

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns
```


## Get cluster credentials

Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Test connectivity with a policy

This section demonstrates how to observe a policy being enforced through the Cilium Agent. A DNS request is made to an allowed FQDN and another case where it's blocked.

Create a file named `demo-policy.yaml`

and paste the following YAML manifest:

Note

The field `spec.egress.toPorts.rules.dns.matchPattern`

is **mandatory** when using to FQDNs in a policy. This section tells Cilium to inspect DNS queries and match them against specified patterns. Without this section, Cilium only allows the DNS traffic and not inspect its contents to learn which IPs are associated with the FQDNs. As a result, connections to those IPs (i.e., non-DNS traffic) are blocked because Cilium can't associate them with the allowed domain.

Make sure to check the [limitations](#limitations) section first.

```
apiVersion: "cilium.io/v2"
kind: CiliumNetworkPolicy
metadata:
name: "allow-bing-fqdn"
spec:
endpointSelector:
matchLabels:
app: demo-container
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: ANY
rules:
dns:
- matchPattern: "*.bing.com"
- toFQDNs:
- matchPattern: "*.bing.com"
```


Specify the name of your YAML manifest and apply it by using [kubectl apply][kubectl-apply]:

```
kubectl create ns demo
kubectl apply -f demo-policy.yaml -n demo
```


### Create a demo pod

Create a `client`

pod running Bash:

```
kubectl run -it client -n demo --image=k8s.gcr.io/e2e-test-images/agnhost:2.43 --labels="app=demo-container" --command -- bash
```


A shell with utilities for testing FQDN should open with the following output:

```
If you don't see a command prompt, try pressing enter.
bash-5.0#
```


In a separate window, run the following command to get the node of the running pod.

```
kubectl get po -n demo --sort-by="{spec.nodeName}" -o wide
```


The output should look similar to the following example:

```
NAME READY STATUS RESTARTS AGE IP NODE NOMINATED NODE READINESS GATES
client 1/1 Running 0 5m50s 192.168.0.139 aks-nodepool1-22058664-vmss000001 <none> <none>
```


The pod is running on a node named `aks-nodepool1-22058664-vmss000001`

. Obtain the Cilium Agent instance running on that node:

```
kubectl get po -n kube-system -o wide --field-selector spec.nodeName="aks-nodepool1-22058664-vmss000001" | grep "cilium"
```


The expected `cilium-s4x24`

should be in the output.

```
cilium-s4x24 1/1 Running 0 47m 10.224.0.4 aks-nodepool1-22058664-vmss000001 <none> <none>
```


### Inspect a Cilium Agent

Use the `cilium`

CLI to monitor traffic being blocked.

```
kubectl exec -it -n kube-system cilium-s4x24 -- sh
```


```
Defaulted container "cilium-agent" out of: cilium-agent, install-cni-binaries (init), mount-cgroup (init), apply-sysctl-overwrites (init), mount-bpf-fs (init), clean-cilium-state (init), block-wireserver (init)
#
```


Inside this shell, run `cilium monitor -t drop`

:

```
Listening for events on 2 CPUs with 64x4096 of shared memory
Press Ctrl-C to quit
time="2024-10-08T17:48:27Z" level=info msg="Initializing dissection cache..." subsys=monitor
```


### Verify policy

From the first shell, create a request to the allowed FQDN, `*.bing.com`

, as specified by the policy. This request should succeed and allowed by the agent.

```
./agnhost connect www.bing.com:80
```


Then create another request to an FQDN expected to be blocked:

```
./agnhost connect www.example.com:80
```


Cilium Agent blocked the request with the output:

```
xx drop (Policy denied) flow 0xfddd76f6 to endpoint 0, ifindex 29, file bpf_lxc.c:1274, , identity 48447->world: 192.168.0.149:45830 -> 93.184.215.14:80 tcp SYN
```


### Supported by CiliumClusterwideNetworkPolicy(CCNP)

`CiliumClusterwideNetworkPolicy`

supports FQDN filtering.

Note

[Namespace specific information](https://docs.cilium.io/en/latest/security/policy/kubernetes/#namespace-specific-information) such as `io.kubernetes.pod.namespace`

is only supported in cluster-wide policies.

```
apiVersion: cilium.io/v2
kind: CiliumClusterwideNetworkPolicy
metadata:
name: allow-bing-fqdn
spec:
endpointSelector: {} # Applies to all pods in the cluster
egress:
- toEndpoints:
- matchLabels:
"k8s:io.kubernetes.pod.namespace": kube-system
"k8s:k8s-app": kube-dns
toPorts:
- ports:
- port: "53"
protocol: ANY
rules:
dns:
- matchPattern: "*.bing.com"
- toFQDNs:
- matchPattern: "*.bing.com"
```


## Clean up resources

If you don't plan on using this application, delete the other resources you created in this article using the [ az group delete](/en-us/cli/azure/#az-group-delete) command.

```
az group delete --name $RESOURCE_GROUP
```


## Next steps

In this how-to article, you learned how to install and enable security features with Advanced Container Networking Services for your AKS cluster.

- For more information about Advanced Container Networking Services for Azure Kubernetes Service (AKS), see
[What is Advanced Container Networking Services for Azure Kubernetes Service (AKS)?](advanced-container-networking-services-overview).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/egress-outboundtype -->

# Customize cluster egress with outbound types in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

Starting on **March 31, 2026**, Azure Kubernetes Service (AKS) no longer supports default outbound access for virtual machines (VMs). New AKS clusters that use the **AKS-managed virtual network** option will place cluster subnets into [private subnets](/en-us/azure/virtual-network/ip-services/default-outbound-access#why-is-disabling-default-outbound-access-recommended) by default (`defaultOutboundAccess = false`

). This setting **doesn't impact AKS-managed cluster traffic**, which uses explicitly configured outbound paths. It might affect **unsupported scenarios**, such as deploying other resources into the same subnet. Clusters using **BYO VNets are unaffected** by this change. In supported configurations, no action is required. For more information on this retirement, see the [Azure Updates retirement announcement](https://azure.microsoft.com/updates?id=default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access). To stay informed on announcements and updates, follow the [AKS release notes](https://github.com/Azure/AKS/releases).

You can customize egress for an AKS cluster to fit specific scenarios. By default, AKS creates a Standard Load Balancer to be set up and used for egress. However, the default setup may not meet the requirements of all scenarios if public IPs are disallowed or extra hops are required for egress.

This article covers the various types of outbound connectivity that are available in AKS clusters.

Note

You can now update the `outboundType`

after cluster creation.

Important

In nonprivate clusters, API server cluster traffic is routed and processed through the clusters outbound type. To prevent API server traffic from being processed as public traffic, consider using a [private cluster](private-clusters), or check out the [API Server VNet Integration](api-server-vnet-integration) feature.

## Limitations

- Setting
`outboundType`

requires AKS clusters with a`vm-set-type`

of`VirtualMachineScaleSets`

and`load-balancer-sku`

of`Standard`

.

## Outbound types in AKS

You can configure an AKS cluster using the following outbound types: load balancer, NAT gateway, or user-defined routing. The outbound type impacts only the egress traffic of your cluster. For more information, see [setting up ingress controllers](ingress-basic).

### Outbound type of `loadBalancer`


The load balancer is used for egress through an AKS-assigned public IP. An outbound type of `loadBalancer`

supports Kubernetes services of type `loadBalancer`

, which expect egress out of the load balancer created by the AKS resource provider.

If `loadBalancer`

is set, AKS automatically completes the following configuration:

- A public IP address is created for cluster egress.
- The public IP address is assigned to the load balancer resource.
- Backend pools for the load balancer are set up for agent nodes in the cluster.

For more information, see [using a standard load balancer in AKS](load-balancer-standard).

### Outbound type of `managedNatGateway`

or `userAssignedNatGateway`


If `managedNatGateway`

or `userAssignedNatGateway`

are selected for `outboundType`

, AKS relies on [Azure Networking NAT gateway](/en-us/azure/virtual-network/nat-gateway/manage-nat-gateway) for cluster egress.

- Select
`managedNatGateway`

when using managed virtual networks. AKS provisions a NAT gateway and attach it to the cluster subnet. - Select
`userAssignedNatGateway`

when using bring-your-own virtual networking. This option requires that you have a NAT gateway created before cluster creation.

For more information, see [using NAT gateway with AKS](nat-gateway).

### Outbound type of `userDefinedRouting`


Note

The `userDefinedRouting`

outbound type is an advanced networking scenario and requires proper network configuration.

If `userDefinedRouting`

is set, AKS doesn't automatically configure egress paths. The egress setup is completed by you.

You must deploy the AKS cluster into an existing virtual network with a subnet that is configured. Since you're not using a standard load balancer (SLB) architecture, you must establish explicit egress. This architecture requires explicitly sending egress traffic to an appliance like a firewall, gateway, proxy or to allow NAT to be done by a public IP assigned to the standard load balancer or appliance.

For more information, see [configuring cluster egress via user-defined routing](egress-udr).

### Outbound type of `none`


Important

The `none`

outbound type is only available with [Network Isolated Cluster](concepts-network-isolated) and requires careful planning to ensure the cluster operates as expected without unintended dependencies on external services. For fully isolated clusters, see [isolated cluster considerations](concepts-network-isolated).

If `none`

is set, AKS won't automatically configure egress paths. This option is similar to `userDefinedRouting`

but does **not** require a default route as part of validation.

The `none`

outbound type is supported in both bring-your-own (BYO) virtual network scenarios and managed VNet scenarios. However, you must ensure that the AKS cluster is deployed into a network environment where explicit egress paths are defined if needed. For BYO VNet scenarios, the cluster must be deployed into an existing virtual network with a subnet that is already configured. Since AKS doesn't create a standard load balancer or any egress infrastructure, you must establish explicit egress paths if needed. Egress options can include routing traffic to a firewall, proxy, gateway, or other custom network configurations.

### Outbound type of `block`

(Preview)

Important

The `block`

outbound type is only available with [Network Isolated Cluster](concepts-network-isolated) and requires careful planning to ensure no unintended network dependencies exist. For fully isolated clusters, see [isolated cluster considerations](concepts-network-isolated).

If `block`

is set, AKS configures network rules to **actively block all egress traffic** from the cluster. This option is useful for highly secure environments where outbound connectivity must be restricted.

When using `block`

:

- AKS ensures that no public internet traffic can leave the cluster through network security group (NSG) rules. VNet traffic isn't affected.
- You must explicitly allow any required egress traffic through extra network configurations.

The `block`

option provides another level of network isolation but requires careful planning to avoid breaking workloads or dependencies.

## Updating `outboundType`

after cluster creation

Changing the outbound type after cluster creation deploys or removes resources as required to put the cluster into the new egress configuration.

The following tables show the supported migration paths between outbound types for managed and BYO virtual networks.

### Supported Migration Paths for Managed VNet

Each row shows whether the outbound type can be migrated to the types listed across the top. "Supported" means migration is possible, while "Not Supported" or "N/A" means it isn't.

| From|To | `loadBalancer` |
`managedNATGateway` |
`userAssignedNATGateway` |
`userDefinedRouting` |
`none` |
`block` |
|---|---|---|---|---|---|---|
`loadBalancer` |
N/A | Supported | Not Supported | Not Supported | Supported | Supported |
`managedNATGateway` |
Supported | N/A | Not Supported | Not Supported | Supported | Supported |
`userAssignedNATGateway` |
Not Supported | Not Supported | N/A | Not Supported | Not Supported | Not Supported |
`none` |
Supported | Supported | Not Supported | Not Supported | N/A | Supported |
`block` |
Supported | Supported | Not Supported | Not Supported | Supported | N/A |

### Supported Migration Paths for BYO VNet

| From|To | `loadBalancer` |
`managedNATGateway` |
`userAssignedNATGateway` |
`userDefinedRouting` |
`none` |
`block` |
|---|---|---|---|---|---|---|
`loadBalancer` |
N/A | Not Supported | Supported | Supported | Supported | Not Supported |
`managedNATGateway` |
Not Supported | N/A | Not Supported | Not Supported | Not Supported | Not Supported |
`userAssignedNATGateway` |
Supported | Not Supported | N/A | Supported | Supported | Not Supported |
`userDefinedRouting` |
Supported | Not Supported | Supported | N/A | Supported | Not Supported |
`none` |
Supported | Not Supported | Supported | Supported | N/A | Not Supported |

Migration is only supported between `loadBalancer`

, `managedNATGateway`

(if using a managed virtual network), `userAssignedNATGateway`

and `userDefinedRouting`

(if using a custom virtual network).

Warning

Migrating the outbound type to user managed types (`userAssignedNATGateway`

or `userDefinedRouting`

) will change the outbound public IP addresses of the cluster.
if [Authorized IP ranges](api-server-authorized-ip-ranges) is enabled, ensure new outbound IP range is appended to authorized IP range.

Warning

Changing the outbound type on a cluster is disruptive to network connectivity and results in a change of the cluster's egress IP address. If any firewall rules are configured to restrict traffic from the cluster, you need to update them to match the new egress IP address.

### Update cluster to use a new outbound type

Note

You must use a version >= 2.56 of Azure CLI to migrate outbound type. Use `az upgrade`

to update to the latest version of Azure CLI.

- Update the outbound configuration of your cluster using the
command.`az aks update`


### Update cluster from loadbalancer to managedNATGateway

```
az aks update --resource-group <resourceGroup> --name <clusterName> --outbound-type managedNATGateway --nat-gateway-managed-outbound-ip-count <number of managed outbound ip>
```


### Update cluster from managedNATGateway to loadbalancer

```
az aks update --resource-group <resourceGroup> --name <clusterName> \
--outbound-type loadBalancer \
<--load-balancer-managed-outbound-ip-count <number of managed outbound ip>| --load-balancer-outbound-ips <outbound ip ids> | --load-balancer-outbound-ip-prefixes <outbound ip prefix ids> >
```


Warning

Don't reuse an IP address that is already in use in prior outbound configurations.

### Update cluster from managedNATGateway to userDefinedRouting

- Add route
`0.0.0.0/0`

default route table. Please see[Customize cluster egress with a user-defined routing table in Azure Kubernetes Service (AKS)](egress-udr)

```
az aks update --resource-group <resourceGroup> --name <clusterName> --outbound-type userDefinedRouting
```


### Update cluster from loadbalancer to userAssignedNATGateway in BYO vnet scenario

- Associate nat gateway with subnet where the workload is associated with. Refer to
[Create a managed or user-assigned NAT gateway](nat-gateway)

```
az aks update --resource-group <resourceGroup> --name <clusterName> --outbound-type userAssignedNATGateway
```

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/image-cleaner -->

# Use Image Cleaner to clean up vulnerable stale images on your Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

It's common to use pipelines to build and deploy images on Azure Kubernetes Service (AKS) clusters. While great for image creation, this process often doesn't account for the stale images left behind and can lead to image bloat on cluster nodes. These images might contain vulnerabilities, which might create security issues. To remove security risks in your clusters, you can clean these unreferenced images. Manually cleaning images can be time intensive. Image Cleaner performs automatic image identification and removal, which mitigates the risk of stale images and reduces the time required to clean them up.

Note

Image Cleaner is a feature based on [Eraser](https://eraser-dev.github.io/eraser).
On an AKS cluster, the feature name and property name is `Image Cleaner`

, while the relevant Image Cleaner pods' names contain `Eraser`

.

## Prerequisites

- An Azure subscription. If you don't have an Azure subscription, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version 2.49.0 or later. Run
`az --version`

to find your version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Limitations

Image Cleaner doesn't yet support Windows node pools or AKS virtual nodes.

## How Image Cleaner works

After you enable Image Cleaner, there will be a controller manager pod named `eraser-controller-manager`

deployed to your cluster.


With Image Cleaner, you can choose between manual and automatic mode and the following configuration options:

## Configuration options

| Name | Description | Required |
|---|---|---|
`--enable-image-cleaner` |
Enable the Image Cleaner feature for an AKS cluster | Yes, unless disable is specified |
`--disable-image-cleaner` |
Disable the Image Cleaner feature for an AKS cluster | Yes, unless enable is specified |
`--image-cleaner-interval-hours` |
This parameter determines the interval time (in hours) Image Cleaner uses to run. The default value for Azure CLI is one week, the minimum value is 24 hours and the maximum is three months. | Not required for Azure CLI, required for ARM template or other clients |

### Automatic mode

Once `eraser-controller-manager`

is deployed, the following steps will be taken automatically:

- It immediately starts the cleanup process and creates
`eraser-aks-xxxxx`

worker pods for each node. - There are three containers in each worker pod:
- A
**collector**, which collects unused images. - A
**trivy-scanner**, which leverages[trivy](https://github.com/aquasecurity/trivy)to scan image vulnerabilities. - A
**remover**, which removes unused images with vulnerabilities.

- A
- After the cleanup process completes, the worker pod is deleted and the next scheduled cleanup happens according to the
`--image-cleaner-interval-hours`

you define.

### Manual mode

You can manually trigger the cleanup by defining a CRD object,`ImageList`

. This triggers the `eraser-contoller-manager`

to create `eraser-aks-xxxxx`

worker pods for each node and complete the manual removal process.

Note

After disabling Image Cleaner, the old configuration still exists. This means if you enable the feature again without explicitly passing configuration, the existing value is used instead of the default.

## Enable Image Cleaner on your AKS cluster

### Enable Image Cleaner on a new cluster

Enable Image Cleaner on a new AKS cluster using the

command with the`az aks create`

`--enable-image-cleaner`

parameter.`az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner \ --generate-ssh-keys`


### Enable Image Cleaner on an existing cluster

Enable Image Cleaner on an existing AKS cluster using the

command.`az aks update`

`az aks update \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner`


### Update the Image Cleaner interval on a new or existing cluster

Update the Image Cleaner interval on a new or existing AKS cluster using the

`--image-cleaner-interval-hours`

parameter.`# Create a new cluster with specifying the interval az aks create \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner \ --image-cleaner-interval-hours 48 \ --generate-ssh-keys # Update the interval on an existing cluster az aks update \ --resource-group myResourceGroup \ --name myManagedCluster \ --enable-image-cleaner \ --image-cleaner-interval-hours 48`


## Manually remove images using Image Cleaner

Important

The `name`

must be set to `imagelist`

.

Manually remove an image using the following

`kubectl apply`

command. This example removes the`docker.io/library/alpine:3.7.3`

image if it's unused.`cat <<EOF | kubectl apply -f - apiVersion: eraser.sh/v1 kind: ImageList metadata: name: imagelist spec: images: - docker.io/library/alpine:3.7.3 EOF`


The manual cleanup is a one-time operation and is only triggered when a new `imagelist`

is created or changes are made to the existing `imagelist`

. After the image is deleted, the `imagelist`

won't be deleted automatically.

If you need to trigger another manual cleanup, you have to create a new `imagelist`

or make changes to an existing one. If you want to remove the same image again, you need to create a new `imagelist`

.

### Delete an existing ImageList and create a new one

Delete the old

`imagelist`

using the`kubectl delete`

command.`kubectl delete ImageList imagelist`

Create a new

`imagelist`

with the same image name. The following example uses the same image as the[previous example](#manually-remove-images-using-image-cleaner).`cat <<EOF | kubectl apply -f - apiVersion: eraser.sh/v1 kind: ImageList metadata: name: imagelist spec: images: - docker.io/library/alpine:3.7.3 EOF`


### Modify an existing ImageList

Modify the existing

`imagelist`

using the`kubectl edit`

command.`kubectl edit ImageList imagelist # Add a new image to the list apiVersion: eraser.sh/v1 kind: ImageList metadata: name: imagelist spec: images: docker.io/library/python:alpine3.18`


When using manual mode, the `eraser-aks-xxxxx`

pod deletes within 10 minutes after work completion.

## Image exclusion list

Images specified in the exclusion list aren't removed from the cluster. Image Cleaner supports system and user-defined exclusion lists. It's not supported to edit the system exclusion list.

### Check the system exclusion list

Check the system exclusion list using the following

`kubectl get`

command.`kubectl get -n kube-system configmap eraser-system-exclusion -o yaml`


### Create a user-defined exclusion list

Create a sample JSON file to contain excluded images.

`cat > sample.json <<EOF {"excluded": ["excluded-image-name"]} EOF`

Create a

`configmap`

using the sample JSON file using the following`kubectl create`

and`kubectl label`

command.`kubectl create configmap excluded --from-file=sample.json --namespace=kube-system kubectl label configmap excluded eraser.sh/exclude.list=true -n kube-system`


## Disable Image Cleaner

Disable Image Cleaner on your cluster using the

command with the`az aks update`

`--disable-image-cleaner`

parameter.`az aks update \ --resource-group myResourceGroup \ --name myManagedCluster \ --disable-image-cleaner`


## FAQ

### How can I check which version Image Cleaner is using?

```
kubectl describe configmap -n kube-system eraser-manager-config | grep tag -C 3
```


### Does Image Cleaner support other vulnerability scanners besides trivy-scanner?

No.

### Can I specify vulnerability levels for images to clean?

No. The default settings for vulnerability levels include:

`LOW`

,`MEDIUM`

,`HIGH`

, and`CRITICAL`


You can't customize the default settings.

### How to review images were cleaned up by Image Cleaner?

Image logs are stored in the `eraser-aks-xxxxx`

worker pod. When `eraser-aks-xxxxx`

is alive, you can run the following commands to view deletion logs:

```
kubectl logs -n kube-system <worker-pod-name> -c collector
kubectl logs -n kube-system <worker-pod-name> -c trivy-scanner
kubectl logs -n kube-system <worker-pod-name> -c remover
```


The `eraser-aks-xxxxx`

pod deletes within 10 minutes after work completion. You can follow these steps to enable the [Azure Monitor add-on](monitor-aks) and use the Container Insights pod log table. After that, historical logs will be stored and you can review them even `eraser-aks-xxxxx`

is deleted.

Ensure Azure Monitoring is enabled on your cluster. For detailed steps, see

[Enable Container Insights on AKS clusters](/en-us/azure/azure-monitor/containers/container-insights-enable-aks#existing-aks-cluster).Logs for the containers running in

`kube-system`

namespace are not collected by default. Remove the`kube-system`

namespace from`exclude_namespaces`

in the configmap and apply the config map to enable collection of these logs. See[Configure Container insights data collection](/en-us/azure/azure-monitor/containers/container-insights-data-collection-configure#configure-data-collection-using-configmap)for details.Get the Log Analytics resource ID using the

command.`az aks show`

`az aks show --resource-group myResourceGroup --name myManagedCluster`

After a few minutes, the command returns JSON-formatted information about the solution, including the workspace resource ID:

`"addonProfiles": { "omsagent": { "config": { "logAnalyticsWorkspaceResourceID": "/subscriptions/<WorkspaceSubscription>/resourceGroups/<DefaultWorkspaceRG>/providers/Microsoft.OperationalInsights/workspaces/<defaultWorkspaceName>" }, "enabled": true } }`

In the Azure portal, search for the workspace resource ID, then select

**Logs**.Copy one of the following queries and paste into the query window.

Use the following query if your cluster is using the

[ContainerLogV2 schema](/en-us/azure/azure-monitor/containers/container-insights-logs-schema). If you're still using`ContainerLog`

, you should upgrade to ContainerlogV2.`ContainerLogV2 | where PodName startswith "eraser-aks-" and PodNamespace == "kube-system" | project TimeGenerated, PodName, LogMessage, LogSource`

If you want continue to use

`ContainerLog`

, use the following query instead:`let startTimestamp = ago(1h); KubePodInventory | where TimeGenerated > startTimestamp | project ContainerID, PodName=Name, Namespace | where PodName startswith "eraser-aks-" and Namespace == "kube-system" | distinct ContainerID, PodName | join ( ContainerLog | where TimeGenerated > startTimestamp ) on ContainerID // at this point before the next pipe, columns from both tables are available to be "projected". Due to both // tables having a "Name" column, we assign an alias as PodName to one column which we actually want | project TimeGenerated, PodName, LogEntry, LogEntrySource | summarize by TimeGenerated, LogEntry | order by TimeGenerated desc`


Select

**Run**. Any deleted image logs appear in the**Results**area.

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/azure-netapp-files-dual-protocol -->

# Provision Azure NetApp Files dual-protocol volumes for Azure Kubernetes Service

After you [configure Azure NetApp Files for Azure Kubernetes Service](azure-netapp-files), you can provision Azure NetApp Files volumes for Azure Kubernetes Service.

Azure NetApp Files supports volumes using [NFS](azure-netapp-files-nfs) (NFSv3 or NFSv4.1), [SMB](azure-netapp-files-smb), and dual-protocol (NFSv3 and SMB, or NFSv4.1 and SMB).

This article shows you how to statically provisioning volumes for dual-protocol access using NFS or SMB.

## Before you begin

## Provision a dual-protocol volume in Azure Kubernetes Service

This section describes how to expose an Azure NetApp Files dual-protocol volume statically to Kubernetes. Instructions are provided for both SMB and NFS protocols. You can expose the same volume via SMB to Windows worker nodes and via NFS to Linux worker nodes.

### Create the persistent volume for NFS

Define variables for later usage. Replace *myresourcegroup*, *myaccountname*, *mypool1*, *myvolname* with an appropriate value from your dual-protocol volume.

```
RESOURCE_GROUP="myresourcegroup"
ANF_ACCOUNT_NAME="myaccountname"
POOL_NAME="mypool1"
VOLUME_NAME="myvolname"
```


List the details of your volume using the `az netappfiles volume show`

command.

```
az netappfiles volume show \
--resource-group $RESOURCE_GROUP \
--account-name $ANF_ACCOUNT_NAME \
--pool-name $POOL_NAME \
--volume-name $VOLUME_NAME -o JSON
```


The following output is an example of the above command executed with real values.

```
{
...
"creationToken": "myfilepath2",
...
"mountTargets": [
{
...
"ipAddress": "10.0.0.4",
...
}
],
...
}
```


Create a file named `pv-nfs.yaml`

and copy in the following YAML. Make sure the server matches the output IP address from the previous step, and the path matches the output from `creationToken`

above. The capacity must also match the volume size from Step 2.

```
apiVersion: v1
kind: PersistentVolume
metadata:
name: pv-nfs
spec:
capacity:
storage: 100Gi
accessModes:
- ReadWriteMany
mountOptions:
- vers=3
nfs:
server: 10.0.0.4
path: /myfilepath2
```


Create the persistent volume using the `kubectl apply`

command:

```
kubectl apply -f pv-nfs.yaml
```


Verify the status of the persistent volume is *Available* by using the `kubectl describe`

command:

```
kubectl describe pv pv-nfs
```


### Create a persistent volume claim for NFS

Create a file named `pvc-nfs.yaml`

and copy in the following YAML. This manifest creates a PVC named `pvc-nfs`

for 100Gi storage and `ReadWriteMany`

access mode, matching the PV you created.

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: pvc-nfs
spec:
accessModes:
- ReadWriteMany
storageClassName: ""
resources:
requests:
storage: 100Gi
```


Create the persistent volume claim using the `kubectl apply`

command:

```
kubectl apply -f pvc-nfs.yaml
```


Verify the *Status* of the persistent volume claim is *Bound* by using the `kubectl describe`

command:

```
kubectl describe pvc pvc-nfs
```


### Mount within a pod using NFS

Create a file named `nginx-nfs.yaml`

and copy in the following YAML. This manifest defines a `nginx`

pod that uses the persistent volume claim.

```
kind: Pod
apiVersion: v1
metadata:
name: nginx-nfs
spec:
containers:
- image: mcr.microsoft.com/oss/nginx/nginx:1.15.5-alpine
name: nginx-nfs
command:
- "/bin/sh"
- "-c"
- while true; do echo $(date) >> /mnt/azure/outfile; sleep 1; done
volumeMounts:
- name: disk01
mountPath: /mnt/azure
volumes:
- name: disk01
persistentVolumeClaim:
claimName: pvc-nfs
```


Create the pod using the `kubectl apply`

[kubectl-apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command:

```
kubectl apply -f nginx-nfs.yaml
```


Verify the pod is *Running* by using the `kubectl apply`

command:

```
kubectl describe pod nginx-nfs
```


Verify your volume has been mounted on the pod by using `kubectl exec`

to connect to the pod, and then use `df -h`

to check if the volume is mounted.

```
kubectl exec -it nginx-nfs -- sh
```


```
/ # df -h
Filesystem Size Used Avail Use% Mounted on
...
10.0.0.4:/myfilepath2 100T 384K 100T 1% /mnt/azure
...
```


### Create a secret with the domain credentials

- Create a secret on your AKS cluster to access the AD server using the
`kubectl create secret`

command. This secret will be used by the Kubernetes persistent volume to access the Azure NetApp Files SMB volume. Use the following command to create the secret, replacing `USERNAME`

with your username, `PASSWORD`

with your password, and `DOMAIN_NAME`

with your Active Directory domain name.

```
kubectl create secret generic smbcreds --from-literal=username=USERNAME --from-literal=password="PASSWORD" --from-literal=domain='DOMAIN_NAME'
```


- To verify the secret has been created, run the
`kubectl get`

command.

```
kubectl get secret
```


```
NAME TYPE DATA AGE
smbcreds Opaque 2 20h
```


### Install an SMB CSI driver

You must install a Container Storage Interface (CSI) driver to create a Kubernetes SMB `PersistentVolume`

.

Install the SMB CSI driver on your cluster using helm. Be sure to set the `windows.enabled`

option to `true`

:

```
helm repo add csi-driver-smb https://raw.githubusercontent.com/kubernetes-csi/csi-driver-smb/master/charts
helm install csi-driver-smb csi-driver-smb/csi-driver-smb --namespace kube-system --version v1.10.0 –-set windows.enabled=true
```


For other methods of installing the SMB CSI Driver, see [Install SMB CSI driver master version on a Kubernetes cluster](https://github.com/kubernetes-csi/csi-driver-smb/blob/master/docs/install-csi-driver-master.md).

Verify the `csi-smb`

controller pod is running and each worker node has a pod running using the `kubectl get pods`

command:

```
kubectl get pods -n kube-system | grep csi-smb
```


```
csi-smb-controller-68df7b4758-xf2m9 3/3 Running 0 3m46s
csi-smb-node-s6clj 3/3 Running 0 3m47s
csi-smb-node-win-tfxvk 3/3 Running 0 3m47s
```


### Create the persistent volume for SMB

Define variables for later usage. Replace *myresourcegroup*, *myaccountname*, *mypool1*, *myvolname* with an appropriate value from your dual-protocol volume.

```
RESOURCE_GROUP="myresourcegroup"
ANF_ACCOUNT_NAME="myaccountname"
POOL_NAME="mypool1"
VOLUME_NAME="myvolname"
```


List the details of your volume using `az netappfiles volume show`

command.

```
az netappfiles volume show \
--resource-group $RESOURCE_GROUP \
--account-name $ANF_ACCOUNT_NAME \
--pool-name $POOL_NAME \
--volume-name "$VOLUME_NAME -o JSON
```


The following output is an example of the above command executed with real values.

```
{
...
"creationToken": "myvolname",
...
"mountTargets": [
{
...
"
"smbServerFqdn": "ANF-1be3.contoso.com",
...
}
],
...
}
```


Create a file named `pv-smb.yaml`

and copy in the following YAML. If necessary, replace `myvolname`

with the `creationToken`

and replace `ANF-1be3.contoso.com\myvolname`

with the value of `smbServerFqdn`

from the previous step. Be sure to include your AD credentials secret along with the namespace where it's located that you created in a prior step.

```
apiVersion: v1
kind: PersistentVolume
metadata:
name: anf-pv-smb
spec:
storageClassName: ""
capacity:
storage: 100Gi
accessModes:
- ReadWriteMany
persistentVolumeReclaimPolicy: Retain
mountOptions:
- dir_mode=0777
- file_mode=0777
- vers=3.0
csi:
driver: smb.csi.k8s.io
readOnly: false
volumeHandle: myvolname # make sure it's a unique name in the cluster
volumeAttributes:
source: \\ANF-1be3.contoso.com\myvolname
nodeStageSecretRef:
name: smbcreds
namespace: default
```


Create the persistent volume using the `kubectl apply`

command:

```
kubectl apply -f pv-smb.yaml
```


Verify the status of the persistent volume is *Available* using the `kubectl describe`

command:

```
kubectl describe pv anf-pv-smb
```


### Create a persistent volume claim for SMB

Create a file name `pvc-smb.yaml`

and copy in the following YAML.

```
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
name: anf-pvc-smb
spec:
accessModes:
- ReadWriteMany
volumeName: anf-pv-smb
storageClassName: ""
resources:
requests:
storage: 100Gi
```


Create the persistent volume claim using the `kubectl apply`

command:

```
kubectl apply -f pvc-smb.yaml
```


Verify the status of the persistent volume claim is *Bound* by using the `kubectl describe`

command:

```
kubectl describe pvc anf-pvc-smb
```


### Mount within a pod using SMB

Create a file named `iis-smb.yaml`

and copy in the following YAML. This file will be used to create an Internet Information Services pod to mount the volume to path `/inetpub/wwwroot`

.

```
apiVersion: v1
kind: Pod
metadata:
name: iis-pod
labels:
app: web
spec:
nodeSelector:
"kubernetes.io/os": windows
volumes:
- name: smb
persistentVolumeClaim:
claimName: anf-pvc-smb
containers:
- name: web
image: mcr.microsoft.com/windows/servercore/iis:windowsservercore
resources:
limits:
cpu: 1
memory: 800M
ports:
- containerPort: 80
volumeMounts:
- name: smb
mountPath: "/inetpub/wwwroot"
readOnly: false
```


Create the pod using the [kubectl apply](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#apply) command:

```
kubectl apply -f iis-smb.yaml
```


Verify the pod is *Running* and `/inetpub/wwwroot`

is mounted from SMB by using the `kubectl describe`

command:

```
kubectl describe pod iis-pod
```


The output of the command resembles the following example:

```
Name: iis-pod
Namespace: default
Priority: 0
Node: akswin000001/10.225.5.246
Start Time: Fri, 05 May 2023 09:34:41 -0400
Labels: app=web
Annotations: <none>
Status: Running
IP: 10.225.5.248
IPs:
IP: 10.225.5.248
Containers:
web:
Container ID: containerd://39a1659b6a2b6db298df630237b2b7d959d1b1722edc81ce9b1bc7f06237850c
Image: mcr.microsoft.com/windows/servercore/iis:windowsservercore
Image ID: mcr.microsoft.com/windows/servercore/iis@sha256:0f0114d0f6c6ee569e1494953efdecb76465998df5eba951dc760ac5812c7409
Port: 80/TCP
Host Port: 0/TCP
State: Running
Started: Fri, 05 May 2023 09:34:55 -0400
Ready: True
Restart Count: 0
Limits:
cpu: 1
memory: 800M
Requests:
cpu: 1
memory: 800M
Environment: <none>
Mounts:
/inetpub/wwwroot from smb (rw)
/var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-mbnv8 (ro)
...
```


Verify your volume has been mounted on the pod by using the [kubectl exec](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#exec) command to connect to the pod. Then use the `dir`

command in the correct directory to check if the volume is mounted and the size matches the size of the volume you provisioned.

```
kubectl exec -it iis-pod –- cmd.exe
```


The output of the command resembles the following example:

```
Microsoft Windows [Version 10.0.20348.1668]
(c) Microsoft Corporation. All rights reserved.
C:\>cd /inetpub/wwwroot
C:\inetpub\wwwroot>dir
Volume in drive C has no label.
Volume Serial Number is 86BB-AA55
Directory of C:\inetpub\wwwroot
05/04/2023 08:15 PM <DIR> .
05/04/2023 08:15 PM <DIR> ..
0 File(s) 0 bytes
2 Dir(s) 107,373,838,336 bytes free
```


## Next steps

Trident supports many features with Azure NetApp Files. For more information, see:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-auto-provisioning-custom-vnet -->

# Create a node auto-provisioning (NAP) cluster in a custom virtual network in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to create a virtual network (VNet) and subnet, create a managed identity with permissions to access the VNet, and create an Azure Kubernetes Service (AKS) cluster in your custom VNet with node auto-provisioning (NAP) enabled.

## Prerequisites

- An Azure subscription. If you don't have one, you can create a
[free account](https://azure.microsoft.com/free). - Azure CLI version
`2.76.0`

or later. To find the version, run`az --version`

. For more information about installing or upgrading the Azure CLI, see[Install Azure CLI](/en-us/cli/azure/get-started-with-azure-cli). - Read the
[Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning)article, which details[how NAP works](node-auto-provisioning#how-does-node-auto-provisioning-work). - Read the
[Overview of networking configurations for node auto-provisioning (NAP) in Azure Kubernetes Service (AKS)](node-auto-provisioning-networking).

## Limitations

- When creating a NAP cluster in a custom virtual network (VNet), you must use a
[Standard Load Balancer](load-balancer-standard). The Basic Load Balancer isn't supported. - To review other limitations and unsupported features for NAP, see the
[Overview of node auto-provisioning (NAP) in AKS](node-auto-provisioning#limitations-and-unsupported-features)article.

## Create a virtual network and subnet

Important

When using a custom VNet with NAP keep the following information in mind:

- You must create and delegate an API server subnet to
`Microsoft.ContainerService/managedClusters`

, which grants the AKS service permissions to inject the API server pods and internal load balancer into that subnet. You can't use the subnet for any other workloads, but you can use it for multiple AKS clusters located in the same VNet. The minimum supported API server subnet size is*/28*. - All traffic within the VNet is allowed by default. However, if you added network security group (NSG) rules to restrict traffic between different subnets, you need to ensure you configure the proper permissions. For more information, see the
[Network security group documentation](/en-us/azure/virtual-network/network-security-groups-overview).

Create a VNet using the

command.`az network vnet create`

`az network vnet create \ --name $VNET_NAME \ --resource-group $RG_NAME \ --location $LOCATION \ --address-prefixes 172.19.0.0/16`

Create a subnet using the

command and delegate it to`az network vnet subnet create`

`Microsoft.ContainerService/managedClusters`

.`az network vnet subnet create \ --resource-group $RG_NAME \ --vnet-name $VNET_NAME \ --name $SUBNET_NAME \ --delegations Microsoft.ContainerService/managedClusters \ --address-prefixes 172.19.0.0/28`


## Create a managed identity and give it permissions to access the VNet

Create a managed identity using the

command.`az identity create`

`az identity create \ --resource-group $RG_NAME \ --name $IDENTITY_NAME \ --location $LOCATION`

Get the principal ID of the managed identity and set it to an environment variable using the [

`az identity show`

][az-identity-show] command.`IDENTITY_PRINCIPAL_ID=$(az identity show --resource-group $RG_NAME --name $IDENTITY_NAME --query principalId -o tsv)`

Assign the

*Network Contributor*role to the managed identity using thecommand.`az role assignment create`

`az role assignment create \ --scope "/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$RG_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME" \ --role "Network Contributor" \ --assignee $IDENTITY_PRINCIPAL_ID`


## Create an AKS cluster with node auto-provisioning (NAP) in a custom VNet

Create an AKS cluster with NAP enabled in your custom VNet using the

command. Make sure to set the`az aks create`

`--node-provisioning-mode`

flag to`Auto`

to enable NAP.The following command also sets the

`--network-plugin`

to`azure`

,`--network-plugin-mode`

to`overlay`

, and`--network-dataplane`

to`cilium`

. For more information on networking configurations supported with NAP, see[Configure networking for node auto-provisioning on AKS](node-autoprovision-networking).`az aks create \ --name $CLUSTER_NAME \ --resource-group $RG_NAME \ --location $LOCATION \ --assign-identity "/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$RG_NAME/providers/Microsoft.ManagedIdentity/userAssignedIdentities/$IDENTITY_NAME" \ --network-dataplane cilium \ --network-plugin azure \ --network-plugin-mode overlay \ --vnet-subnet-id "/subscriptions/$SUBSCRIPTION_ID/resourceGroups/$RG_NAME/providers/Microsoft.Network/virtualNetworks/$CUSTOM_VNET_NAME/subnets/$SUBNET_NAME" \ --node-provisioning-mode Auto`

After a few minutes, the command completes and returns JSON-formatted information about the cluster.

Configure

`kubectl`

to connect to your Kubernetes cluster using thecommand. This command downloads credentials and configures the Kubernetes CLI to use them.`az aks get-credentials`

`az aks get-credentials \ --resource-group $RG_NAME \ --name $CLUSTER_NAME`

Verify the connection to your cluster using the

command. This command returns a list of the cluster nodes.`kubectl get`

`kubectl get nodes`


## Next steps

For more information on node auto-provisioning in AKS, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-resource-group-lockdown -->

# Deploy a fully managed resource group using node resource group lockdown in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS deploys infrastructure into your subscription for connecting to and running your applications. Changes made directly to resources in the [node resource group](concepts-clusters-workloads#node-resource-group) can affect cluster operations or cause future issues. For example, scaling, storage, or network configurations should be made through the Kubernetes API and not directly on these resources.

To prevent changes from being made to the node resource group, you can apply a deny assignment and block users from modifying resources created as part of the AKS cluster.

## Before you begin

Before you begin, you need the following resources installed and configured:

- The Azure CLI version 2.44.0 or later. Run
`az --version`

to find the current version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Create an AKS cluster with node resource group lockdown

Create a cluster with node resource group lockdown using the [ az aks create](/en-us/cli/azure/aks#az-aks-create) command with the

`--nrg-lockdown-restriction-level`

flag set to `ReadOnly`

. This configuration allows you to view the resources but not modify them.```
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--nrg-lockdown-restriction-level ReadOnly \
--generate-ssh-keys
```


## Update an existing cluster with node resource group lockdown

Update an existing cluster with node resource group lockdown using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--nrg-lockdown-restriction-level`

flag set to `ReadOnly`

. This configuration allows you to view the resources but not modify them.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --nrg-lockdown-restriction-level ReadOnly
```


## Remove node resource group lockdown from a cluster

Remove node resource group lockdown from an existing cluster using the [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the

`--nrg-restriction-level`

flag set to `Unrestricted`

. This configuration allows you to view and modify the resources.```
az aks update --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --nrg-lockdown-restriction-level Unrestricted
```


## Next steps

To learn more about the node resource group in AKS, see [Node resource group](concepts-clusters-workloads#node-resource-group).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-pool-unique-subnet -->

# Create node pools with unique subnets in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Certain workloads might require splitting cluster nodes into separate pools for logical isolation. Separate subnets dedicated to each node pool in the cluster can help support this isolation, which can address requirements such as having noncontiguous virtual network address space to split across node pools.

In this article, you learn how to create node pools with unique subnets in Azure Kubernetes Service (AKS).

## Prerequisites

[Azure CLI](/en-us/cli/azure/install-azure-cli)version 2.35.0 or later. Run`az version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).- An existing AKS cluster with a system node pool. If you need to create one, see
[Create an AKS cluster with a single node pool](create-node-pools#create-an-aks-cluster-with-a-single-node-pool-using-the-azure-cli).

## Limitations

- All subnets assigned to node pools must belong to the same virtual network (VNet).
- System pods must have access to all nodes and pods in the cluster to provide critical functionality, such as DNS resolution and tunneling kubectl logs/exec/port-forward proxy.
- If you expand your VNet after creating the cluster, you must update your cluster before adding a subnet outside the original CIDR block. While AKS errors out on the agent pool add, the
`aks-preview`

Azure CLI extension (version 0.5.66 and higher) now supports running`az aks update`

command with only the required`--resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`

arguments. This command performs an update operation without making any changes, which can recover a cluster stuck in a failed state. - In clusters with Kubernetes version less than 1.23.3, kube-proxy SNATs traffic from new subnets, which can cause Azure Network Policy to drop the packets.
- Windows nodes SNAT traffic to the new subnets until the node pool is reimaged.
- Internal load balancers default to one of the node pool subnets.

## Add a node pool with a unique subnet

Add a node pool with a unique subnet into your existing AKS cluster using the

command and the`az aks nodepool add`

`--vnet-subnet-id`

parameter specified.`az aks nodepool add \ --resource-group $RESOURCE_GROUP_NAME \ --cluster-name $CLUSTER_NAME \ --name $NODE_POOL_NAME \ --node-count 3 \ --vnet-subnet-id $SUBNET_RESOURCE_ID`


## Next steps

For more information about node pools in AKS, see [Manage node pools for a cluster in Azure Kubernetes Service (AKS)](manage-node-pools).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/operator-best-practices-storage -->

# Best practices for storage and backups in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

As you create and manage clusters in Azure Kubernetes Service (AKS), your applications often need storage. Make sure you understand pod performance needs and access methods so that you can select the best storage for your application. The AKS node size may impact your storage choices. Plan for ways to back up and test the restore process for attached storage.

This best practices article focuses on storage considerations for cluster operators. In this article, you learn:

- What types of storage are available.
- How to correctly size AKS nodes for storage performance.
- Differences between dynamic and static provisioning of volumes.
- Ways to back up and secure your data volumes.

## Choose the appropriate storage type


Best practice guidanceUnderstand the needs of your application to pick the right storage. Use high performance, SSD-backed storage for production workloads. Plan for network-based storage when you need multiple concurrent connections.


Applications often require different types and speeds of storage. Determine the most appropriate storage type by asking the following questions.

- Do your applications need storage that connects to individual pods?
- Do your applications need storage shared across multiple pods?
- Is the storage for read-only access to data?
- Will the storage be used to write large amounts of structured data?

The following table outlines the available storage types and their capabilities:

| Use case | Volume plugin | Read/write once | Read-only many | Read/write many | Windows Server container support |
|---|---|---|---|---|---|
| Shared configuration | Azure Files | Yes | Yes | Yes | Yes |
| Structured app data | Azure Disks | Yes | No | No | Yes |
| Unstructured data, file system operations |
|

AKS provides two primary types of secure storage for volumes backed by Azure Disks or Azure Files. Both use the default Azure Storage Service Encryption (SSE) that encrypts data at rest. Disks cannot be encrypted using Azure Disk Encryption at the AKS node level. With Azure Files shares, there is no limit as to how many can be mounted on a node.

Both Azure Files and Azure Disks are available in Standard and Premium performance tiers:

*Premium*disks- Backed by high-performance solid-state disks (SSDs).
- Recommended for all production workloads.

*Standard*disks- Backed by regular spinning disks (HDDs).
- Good for archival or infrequently accessed data.


While the default storage tier for the Azure Disk CSI driver is Premium SSD, your custom StorageClass can use Premium SSD, Standard SSD, or Standard HDD.

Understand the application performance needs and access patterns to choose the appropriate storage tier. For more information about Managed Disks sizes and performance tiers, see [Azure Managed Disks overview](/en-us/azure/virtual-machines/managed-disks-overview).

### Create and use storage classes to define application needs

Define the type of storage you want using Kubernetes *storage classes*. The storage class is then referenced in the pod or deployment specification. Storage class definitions work together to create the appropriate storage and connect it to pods.

For more information, see [Storage classes in AKS](concepts-storage#storage-classes).

## Size the nodes for storage needs


Best practice guidanceEach node size supports a maximum number of disks. Different node sizes also provide different amounts of local storage and network bandwidth. Plan appropriately for your application demands to deploy the right size of nodes.


AKS nodes run as various Azure VM types and sizes. Each VM size provides:

- A different amount of core resources such as CPU and memory.
- A maximum number of disks that can be attached.

Storage performance also varies between VM sizes for the maximum local and attached disk IOPS (input/output operations per second).

If your applications require Azure Disks as their storage solution, strategize an appropriate node VM size. Storage capabilities and CPU and memory amounts play a major role when deciding on a VM size.

For example, while both the *Standard_B2ms* and *Standard_DS2_v2* VM sizes include a similar amount of CPU and memory resources, their potential storage performance is different:

| Node type and size | vCPU | Memory (GiB) | Max data disks | Max uncached disk IOPS | Max uncached throughput (MBps) |
|---|---|---|---|---|---|
| Standard_B2ms | 2 | 8 | 4 | 1,920 | 22.5 |
| Standard_DS2_v2 | 2 | 7 | 8 | 6,400 | 96 |

In this example, the *Standard_DS2_v2* offers twice as many attached disks, and three to four times the amount of IOPS and disk throughput. If you only compared core compute resources and compared costs, you might have chosen the *Standard_B2ms* VM size with poor storage performance and limitations.

Work with your application development team to understand their storage capacity and performance needs. Choose the appropriate VM size for the AKS nodes to meet or exceed their performance needs. Regularly baseline applications to adjust VM size as needed.

Note

By default, disk size and performance for managed disks is assigned according to the selected VM SKU and vCPU count. Default OS disk sizing is only used on new clusters or node pools when Ephemeral OS disks are not supported and a default OS disk size is not specified. For more information, see [Default OS disk sizing](cluster-configuration#default-os-disk-sizing).

For more information about available VM sizes, see [Sizes for Linux virtual machines in Azure](/en-us/azure/virtual-machines/sizes).

### Consider ephemeral NVMe data disks for maximum performance


Best practice guidanceConsider ephemeral NVMe data disks when you need the highest storage throughput and IOPS, and your workload can tolerate the temporary nature of local node storage. Ephemeral NVMe data disks provide low-latency, host-attached storage that delivers the highest IOPS and throughput available in Azure. NVMe disks are available on L-series, E-series, and GPU VMs, with expanding support for the newer Azure VM v6 and v7 families such as the D-series, F-series, H-series.


NVMe-backed storage enhances workloads that demand high-speed caching, temporary storage, or transient data processing. It eliminates the reliance on high-performance remote disks, which typically require the largest and most costly VM configurations to achieve optimal performance.

Common scenarios that benefit from ephemeral NVMe data disks include:

- AI training or inference pipelines that stage large datasets or checkpoints between iterations
- High-performance databases or streaming engines that maintain replicas or logs across pods
- Batch analytics jobs that require temporary scratch space or shuffle storage

Because NVMe data is tied to the node instance, plan for pod disruption budgets and ensure your application can quickly rebuild from durable storage or replication. Data placed on these disks is lost whenever a node is deallocated, reimaged, or fails.

For further recommendations on ephemeral NVMe data disks, see [Best practices for ephemeral NVMe data disks in Azure Kubernetes Service (AKS)](best-practices-storage-nvme). To expose NVMe capacity to pods, use [Azure Container Storage](/en-us/azure/storage/container-storage/container-storage-introduction), which will can orchestrate and create ephemeral **or** persistent volumes backed by local NVMe disks. For implementation guidance, see [Use Azure Container Storage with AKS](/en-us/azure/storage/container-storage/container-storage-aks-quickstart).

Important

Use NVMe data disks only for workloads that can tolerate data loss and recover quickly. Keep business-critical data on durable storage such as Azure Disk or Azure Files.

## Dynamically provision volumes


Best practice guidanceTo reduce management overhead and enable scaling, avoid statically create and assign persistent volumes. Use dynamic provisioning. In your storage classes, define the appropriate reclaim policy to minimize unneeded storage costs once pods are deleted.


To attach storage to pods, use persistent volumes. Persistent volumes can be created manually or dynamically. Creating persistent volumes manually adds management overhead and limits your ability to scale. Instead, provision persistent volume dynamically to simplify storage management and allow your applications to grow and scale as needed.

A persistent volume claim (PVC) lets you dynamically create storage as needed. Underlying Azure disks are created as pods request them. In the pod definition, request a volume to be created and attached to a designated mount path.

For the concepts on how to dynamically create and use volumes, see [Persistent Volumes Claims](concepts-storage#persistent-volume-claims).

To see these volumes in action, see how to dynamically create and use a persistent volume with [Azure Disks](azure-disk-csi) or [Azure Files](azure-files-csi).

As part of your storage class definitions, set the appropriate *reclaimPolicy*. This reclaimPolicy controls the behavior of the underlying Azure storage resource when the pod is deleted. The underlying storage resource can either be deleted or retained for future pod use. Set the reclaimPolicy to *retain* or *delete*.

Understand your application needs, and implement regular checks for retained storage to minimize the amount of unused and billed storage.

For more information about storage class options, see [storage reclaim policies](concepts-storage#storage-classes).

## Secure and back up your data


Best practice guidanceBack up your data using an appropriate tool for your storage type, such as Velero or Azure Backup. Verify the integrity and security of those backups.


When your applications store and consume data persisted on disks or in files, you need to take regular backups or snapshots of that data. Azure Disks can use built-in snapshot technologies. Your applications may need to flush writes-to-disk before you perform the snapshot operation. [Velero](https://github.com/heptio/velero) can back up persistent volumes along with additional cluster resources and configurations. If you can't [remove state from your applications](operator-best-practices-multi-region#remove-service-state-from-inside-containers), back up the data from persistent volumes and regularly test the restore operations to verify data integrity and the processes required.

Understand the limitations of the different approaches to data backups and if you need to quiesce your data prior to snapshot. Data backups don't necessarily let you restore your application environment of cluster deployment. For more information about those scenarios, see [Best practices for business continuity and disaster recovery in AKS](operator-best-practices-multi-region).

## Next steps

This article focused on storage best practices in AKS. For more information about storage basics in Kubernetes, see [Storage concepts for applications in AKS](concepts-storage).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/draft -->

# Draft for Azure Kubernetes Service (AKS) (preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Draft](https://github.com/Azure/draft) is an open-source project that streamlines Kubernetes development by taking a non-containerized application and generating the Dockerfiles, Kubernetes manifests, Helm charts, Kustomize configurations, and other artifacts associated with a containerized application. Draft can also create a GitHub Action workflow file to quickly build and deploy applications onto any Kubernetes cluster.

## How it works

Draft has the following commands to help ease your development on Kubernetes:

`draft create`

: Creates the Dockerfile and the proper manifest files.`draft setup-gh`

: Sets up your GitHub OIDC.`draft generate-workflow`

: Generates the GitHub Action workflow file for deployment onto your cluster.`draft up`

: Sets up your GitHub OIDC and generates a GitHub Action workflow file, combining the previous two commands.

## Prerequisites

- If you don't have an Azure subscription, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin. - Install the latest version of the
[Azure CLI](/en-us/cli/azure/install-azure-cli-windows)and the*aks-preview*extension. - If you don't have one already, you need to create an
[AKS cluster](tutorial-kubernetes-deploy-cluster)and an Azure Container Registry instance.

### Install the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install the

`aks-preview`

extension using thecommand.`az extension add`

`az extension add --name aks-preview`

Update the extension to make sure you have the latest version using the

command.`az extension update`

`az extension update --name aks-preview`


## Create artifacts using `draft create`


You can use `draft create`

to create Dockerfiles, Helm charts, Kubernetes manifests, or Kustomize files needed to deploy your application onto an AKS cluster.

Create an artifact using the

command.`az aks draft create`

`az aks draft create`

You can also run the command on a specific directory using the

`--destination`

flag, as shown in the following example:`az aks draft create --destination /Workspaces/ContosoAir`


## Set up GitHub OIDC using `draft setup-gh`


To use Draft, you have to register your application with GitHub using `draft setup-gh`

. This step only needs to be done once per repository.

Register your application with GitHub using the

command.`az aks draft setup-gh`

`az aks draft setup-gh`


## Generate a GitHub Action workflow file for deployment using `draft generate-workflow`


After you create your artifacts and set up GitHub OIDC, you can use `draft generate-workflow`

to generate a GitHub Action workflow file, creating an action that deploys your application onto your AKS cluster. Once your workflow file is generated, you must commit it into your repository in order to initiate the GitHub Action.

Generate a GitHub Action workflow file using the

command.`az aks draft generate-workflow`

`az aks draft generate-workflow`

You can also run the command on a specific directory using the

`--destination`

flag, as shown in the following example:`az aks draft generate-workflow --destination /Workspaces/ContosoAir`


## Set up GitHub OpenID Connect (OIDC) and generate a GitHub Action workflow file using `draft up`


`draft up`

is a single command to accomplish GitHub OIDC setup and generate a GitHub Action workflow file for deployment. It effectively combines the `draft setup-gh`

and `draft generate-workflow`

commands, meaning it's most commonly used when getting started in a new repository for the first time, and only needs to be run once. Subsequent updates to the GitHub Action workflow file can be made using `draft generate-workflow`

.

Set up GitHub OIDC and generate a GitHub Action workflow file using the

command.`az aks draft up`

`az aks draft up`

You can also run the command on a specific directory using the

`--destination`

flag, as shown in the following example:`az aks draft up --destination /Workspaces/ContosoAir`


## Use Application Routing with Draft to make your application accessible over the internet

Application Routing][app-routing](app-routing) is the easiest way to get your web application up and running in Kubernetes securely. Application Routing removes the complexity of ingress controllers and certificate and DNS management, and it offers configuration for enterprises looking to bring their own. Application Routing offers a managed ingress controller based on nginx that you can use without restrictions and integrates out of the box with Open Service Mesh to secure intra-cluster communications.

Set up Draft with Application Routing using the

and pass in the DNS name and Azure Key Vault-stored certificate when prompted.`az aks draft update`

`az aks draft update`

You can also run the command on a specific directory using the

`--destination`

flag, as shown in the following example:`az aks draft update --destination /Workspaces/ContosoAir`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/aks-extension-kaito -->

# Deploy and test inference models with the AI toolchain operator (KAITO) in Visual Studio Code

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to use the AI toolchain operator (KAITO) add-on in the Azure Kubernetes Service (AKS) extension for Visual Studio Code. KAITO automatically provisions the right-sized GPU nodes and sets up the inference server as an endpoint server to your AI model(s), allowing you to test and experiment with AI on AKS with ease.

## Prerequisites

- The Azure Kubernetes Service (AKS) extension for Visual Studio Code needs to be installed to use the KAITO experience. For more information, see
[Install the Azure Kubernetes Service (AKS) extension for Visual Studio Code](aks-extension-vs-code#installation). - The cluster that you are deploying to is a Standard Cluster
*(Kaito cannot currently be installed on Automatic clusters)*. - Verify that your Azure subscription has GPU quota for your chosen model by checking the
[KAITO model workspaces](https://github.com/kaito-project/kaito/tree/main/presets).

## Install KAITO on your cluster

- In the Kubernetes tab, under
**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Install KAITO**. - Once on the page, select
**Install KAITO**to start the KAITO installation process. - When the installation completes, you will see a
**Generate Workspace**button that redirects you to the model deployment page.

## Create a KAITO workspace

When creating a KAITO workspace, you can either deploy the default workspace CRD directly into your AKS cluster or save the CRD and customize it for your needs.

- In the Kubernetes tab, under
**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Create KAITO workspace**. - Find and select the model you want to deploy.
- Select
**Deploy default workspace CRD**or**Customize workspace CRD**. - Select
**Deploy default workspace CRD**to deploy the model. It tracks the progress of the model and notifies you once the model successfully deploys. It also notifies you if the model was already deployed unsuccessfully onto your cluster. - When the deployment completes, you see a
**View Deployed Models**button that redirects you to the deployment management page.

## Manage KAITO models

The **Manage KAITO models** page allows you to see all models deployed in your AKS cluster along with their status (*ongoing*, *successful*, or *failed*).

In the Kubernetes tab, under

**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Manage KAITO models**.From this page, you can choose to perform one of the following actions:

**Get logs**: Select**Get Logs**to access the latest logs from the KAITO workspace pods for your deployment. This action generates a new text file containing the most recent 500 lines of logs.**Delete a model**: Select**Delete Workspace**(or**Cancel**for ongoing deployments). For failed deployments, select**Redeploy Default CRD**to remove the current deployment and restart the model deployment process from scratch.**Test a model**: Select**Test**. This action brings you to a new page where you can interact with the deployed model through a chat interface.


## Test your model

In the Kubernetes tab, under

**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Manage KAITO models**.Select

**Test**. This action brings you to a new page where you can interact with the deployed model through the**Prompt**box chat interface.You can optionally adjust the parameters:

**Temperature**: Controls the randomness of the model's output. A low temperature is good for tasks needing precision, like math problems, while a high temperature is better for tasks like creative writing.**Top P**: Limits the next-word choices to a dynamic subset of the vocabulary, determined by a cumulative probability threshold.**Top K**: Limits the next-word selection to the top`K`

most probable words. Smaller`K`

values lead to more predictable outputs, while larger values increase variability.**Repetition Penalty**: Penalizes the model for repeating the same phrases, words, or sequences. This is useful for avoiding repetitive or looping outputs, especially in longer generations.**Max Length**: Defines the maximum number of tokens (words or subwords) in the generated output.


For more information, see [AKS extension for Visual Studio Code features](https://code.visualstudio.com/docs/azure/aksextensions#_features).

## Delete your model inference deployment

- Once you've finished testing the model(s) and you want to free up the allocated GPU resources on your cluster, go to the Kubernetes tab, and under
**Clouds**>**Azure**>**your subscription**>**Deploy a LLM with KAITO**, right click on your cluster and select**Manage KAITO models**. - For each deployed model, select
**Delete Workspace**to clear all allocated resources created by the inference deployment.

## Product support and feedback

If you have a question or want to offer product feedback, please open an issue on the [AKS extension GitHub repository](https://github.com/Azure/vscode-aks-tools/issues/new/choose).

## Next steps

To learn more about other AKS add-ons and extensions, see [Add-ons, extensions, and other integrations for AKS](integrations).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-node-public-ips -->

# Use instance-level public IPs in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS nodes don't require their own public IP addresses for communication. However, scenarios may require nodes in a node pool to receive their own dedicated public IP addresses. A common scenario is for gaming workloads, where a console needs to make a direct connection to a cloud virtual machine to minimize hops. This scenario can be achieved on AKS by using Node Public IP.

First, create a new resource group.

```
az group create --name <resourceGroup> --location <region>
```


Create a new AKS cluster and attach a public IP for your nodes. Each of the nodes in the node pool receives a unique public IP. You can verify this by looking at the Virtual Machine Scale Set instances.

```
az aks create \
--resource-group <resourceGroup> \
--name <aksClusterName> \
--location <region> \
--enable-node-public-ip \
--generate-ssh-keys
```


For existing AKS clusters, you can also add a new node pool, and attach a public IP for your nodes.

```
az aks nodepool add --resource-group <resourceGroup> --cluster-name <aksClusterName> --name <newNodePool> --enable-node-public-ip
```


## Use a public IP prefix

There are a number of [benefits to using a public IP prefix](/en-us/azure/virtual-network/ip-services/public-ip-address-prefix). AKS supports using addresses from an existing public IP prefix for your nodes by passing the resource ID with the flag `--node-public-ip-prefix-id`

when creating a new cluster or adding a node pool.

First, create a public IP prefix using [az network public-ip prefix create](/en-us/cli/azure/network/public-ip/prefix#az-network-public-ip-prefix-create):

```
az network public-ip prefix create --length 28 --location <region> --name <publicIPPrefixName> --resource-group <resourceGroup>
```


View the output, and take note of the `id`

for the prefix:

```
{
...
"id": "/subscriptions/<subscription-id>/resourceGroups/<resourceGroup>/providers/Microsoft.Network/publicIPPrefixes/<publicIPPrefixName>",
...
}
```


Finally, when creating a new cluster or adding a new node pool, use the flag `--node-public-ip-prefix-id`

and pass in the prefix's resource ID:

```
az aks create \
--resource-group <resourceGroup> \
--name <aksClusterName> \
--location <region> \
--enable-node-public-ip \
--node-public-ip-prefix-id /subscriptions/<subscription-id>/resourceGroups/<resourceGroup>/providers/Microsoft.Network/publicIPPrefixes/<publicIPPrefixName> \
--generate-ssh-keys
```


## Locate public IPs for nodes

You can locate the public IPs for your nodes in various ways:

- Use the Azure CLI command
.`az vmss list-instance-public-ips`

- Use
[PowerShell or Bash commands](/en-us/azure/virtual-machine-scale-sets/virtual-machine-scale-sets-networking#public-ipv4-per-virtual-machine). - You can also view the public IPs in the Azure portal by viewing the instances in the Virtual Machine Scale Set.

Important

The [node resource group](faq) contains the nodes and their public IPs. Use the node resource group when executing commands to find the public IPs for your nodes.

```
az vmss list-instance-public-ips --resource-group <MC_region_aksClusterName_region> --name <virtualMachineScaleSetName>
```


## Use public IP tags on node public IPs

Public IP tags can be utilized on node public IPs to utilize the [Azure Routing Preference](/en-us/azure/virtual-network/ip-services/routing-preference-overview) feature.

### Requirements

- AKS version 1.29 or greater is required.

### Create a new cluster using routing preference internet

```
az aks create \
--name <aksClusterName> \
--location <region> \
--resource-group <resourceGroup> \
--enable-node-public-ip \
--node-public-ip-tags RoutingPreference=Internet \
--generate-ssh-keys
```


### Add a node pool with routing preference internet

```
az aks nodepool add --cluster-name <aksClusterName> \
--name <nodePoolName> \
--location <region> \
--resource-group <resourceGroup> \
--enable-node-public-ip \
--node-public-ip-tags RoutingPreference=Internet
```


## Allow host port connections and add node pools to application security groups

AKS nodes utilizing node public IPs that host services on their host address need to have an NSG rule added to allow the traffic. Adding the desired ports in the node pool configuration will create the appropriate allow rules in the cluster network security group.

If a network security group is in place on the subnet with a cluster using bring-your-own virtual network, an allow rule must be added to that network security group. This can be limited to the nodes in a given node pool by adding the node pool to an [application security group (ASG)](/en-us/azure/virtual-network/network-security-groups-overview#application-security-groups). A managed ASG will be created by default in the managed resource group if allowed host ports are specified. Nodes can also be added to one or more custom ASGs by specifying the resource ID of the NSG(s) in the node pool parameters.

### Host port specification format

When specifying the list of ports to allow, use a comma-separate list with entries in the format of `port/protocol`

or `startPort-endPort/protocol`

.

Examples:

- 80/tcp
- 80/tcp,443/tcp
- 53/udp,80/tcp
- 50000-60000/tcp

### Requirements

- AKS version 1.29 or greater is required.

### Create a new cluster with allowed ports and application security groups

```
az aks create \
--resource-group <resourceGroup> \
--name <aksClusterName> \
--nodepool-name <nodePoolName> \
--nodepool-allowed-host-ports 80/tcp,443/tcp,53/udp,40000-60000/tcp,40000-50000/udp\
--nodepool-asg-ids "<asgId>,<asgId>" \
--generate-ssh-keys
```


### Add a new node pool with allowed ports and application security groups

```
az aks nodepool add \
--resource-group <resourceGroup> \
--cluster-name <aksClusterName> \
--name <nodePoolName> \
--allowed-host-ports 80/tcp,443/tcp,53/udp,40000-60000/tcp,40000-50000/udp \
--asg-ids "<asgId>,<asgId>"
```


### Update the allowed ports and application security groups for a node pool

```
az aks nodepool update \
--resource-group <resourceGroup> \
--cluster-name <aksClusterName> \
--name <nodePoolName> \
--allowed-host-ports 80/tcp,443/tcp,53/udp,40000-60000/tcp,40000-50000/udp \
--asg-ids "<asgId>,<asgId>"
```


## Automatically assign host ports for pod workloads (PREVIEW)

When public IPs are configured on nodes, host ports can be utilized to allow pods to directly receive traffic without having to configure a load balancer service. This is especially useful in scenarios like gaming, where the ephemeral nature of the node IP and port is not a problem because a matchmaker service at a well-known hostname can provide the correct host and port to use at connection time. However, because only one process on a host can be listening on the same port, using applications with host ports can lead to problems with scheduling. To avoid this issue, AKS provides the ability to have the system dynamically assign an available port at scheduling time, preventing conflicts.

Warning

Pod host port traffic will be blocked by the default NSG rules in place on the cluster. This feature should be combined with allowing host ports on the node pool to allow traffic to flow.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

### Requirements

- AKS version 1.29 or greater is required.

### Register the 'PodHostPortAutoAssignPreview' feature flag

Register the `PodHostPortAutoAssignPreview`

feature flag by using the [az feature register](/en-us/cli/azure/feature#az-feature-register) command, as shown in the following example:

```
az feature register --namespace "Microsoft.ContainerService" --name "PodHostPortAutoAssignPreview"
```


It takes a few minutes for the status to show *Registered*. Verify the registration status by using the [az feature show](/en-us/cli/azure/feature#az-feature-show) command:

```
az feature show --namespace "Microsoft.ContainerService" --name "PodHostPortAutoAssignPreview"
```


When the status reflects *Registered*, refresh the registration of the *Microsoft.ContainerService* resource provider by using the [az provider register](/en-us/cli/azure/provider#az-provider-register) command:

```
az provider register --namespace Microsoft.ContainerService
```


### Automatically assign a host port to a pod

Triggering host port auto assignment is done by deploying a workload without any host ports and applying the `kubernetes.azure.com/assign-hostports-for-containerports`

annotation with the list of ports that need host port assignments. The value of the annotation should be specified as a comma-separated list of entries like `port/protocol`

, where the port is an individual port number that is defined in the Pod spec and the protocol is `tcp`

or `udp`

.

Ports will be assigned from the range `40000-59999`

and will be unique across the cluster. The assigned ports will also be added to environment variables inside the pod so that the application can determine what ports were assigned. The environment variable name will be in the following format (example below): `<deployment name>_PORT_<port number>_<protocol>_HOSTPORT`

, so an example would be `mydeployment_PORT_8080_TCP_HOSTPORT: 41932`

.

Here is an example `echoserver`

deployment, showing the mapping of host ports for ports 8080 and 8443:

```
apiVersion: apps/v1
kind: Deployment
metadata:
name: echoserver-hostport
labels:
app: echoserver-hostport
spec:
replicas: 3
selector:
matchLabels:
app: echoserver-hostport
template:
metadata:
annotations:
kubernetes.azure.com/assign-hostports-for-containerports: 8080/tcp,8443/tcp
labels:
app: echoserver-hostport
spec:
nodeSelector:
kubernetes.io/os: linux
containers:
- name: echoserver-hostport
image: k8s.gcr.io/echoserver:1.10
ports:
- name: http
containerPort: 8080
protocol: TCP
- name: https
containerPort: 8443
protocol: TCP
```


When the deployment is applied, the `hostPort`

entries will be in the YAML of the individual pods:

```
$ kubectl describe pod echoserver-hostport-75dc8d8855-4gjfc
<cut for brevity>
Containers:
echoserver-hostport:
Container ID: containerd://d0b75198afe0612091f412ee7cf7473f26c80660143a96b459b3e699ebaee54c
Image: k8s.gcr.io/echoserver:1.10
Image ID: k8s.gcr.io/echoserver@sha256:cb5c1bddd1b5665e1867a7fa1b5fa843a47ee433bbb75d4293888b71def53229 Ports: 8080/TCP, 8443/TCP
Host Ports: 46645/TCP, 49482/TCP
State: Running
Started: Thu, 12 Jan 2023 18:02:50 +0000
Ready: True
Restart Count: 0
Environment:
echoserver-hostport_PORT_8443_TCP_HOSTPORT: 49482
echoserver-hostport_PORT_8080_TCP_HOSTPORT: 46645
```


## Next steps

Learn about

[using multiple node pools in AKS](create-node-pools).Learn about

[using standard load balancers in AKS](load-balancer-standard)

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/how-to-apply-wireguard -->

# Deploy WireGuard encryption with Advanced Container Networking Services (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

WireGuard encryption with Advanced Cluster Networking Services is currently in PREVIEW.

See the [Supplemental Terms of Use for Microsoft Azure Previews](https://azure.microsoft.com/support/legal/preview-supplemental-terms/) for legal terms that apply to Azure features that are in beta, preview, or otherwise not yet released into general availability.

This article shows you how to deploy WireGuard encryption with Advanced Container Networking Services in Azure Kubernetes Service (AKS) clusters.

## Prerequisites

- An Azure account with an active subscription. If you don't have one, create a
[free account](https://azure.microsoft.com/pricing/purchase-options/azure-account?cid=msft_learn)before you begin.

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


The minimum version of Azure CLI required for the steps in this article is 2.71.0. To find the version, run

`az --version`

. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).WireGuard encryption is only supported with the Azure CNI powered by Cilium. If you're using any other network plugin, WireGuard encryption isn't supported. See

[Configure Azure CNI Powered by Cilium](/en-us/azure/aks/azure-cni-powered-by-cilium).WireGuard establishes encrypted tunnels over UDP port 51871, which is exposed on each AKS node. Ensure UDP port 51871 is allowed between all node IPs, especially if your environment uses firewalls.


### Install the `aks-preview`

Azure CLI extension

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Install or update the Azure CLI preview extension using the [ az extension add](/en-us/cli/azure/extension#az-extension-add) or

[command.](/en-us/cli/azure/extension#az-extension-update)

`az extension update`

The minimum version of the aks-preview Azure CLI extension is `14.0.0b6`


```
# Install the aks-preview extension
az extension add --name aks-preview
# Update the extension to make sure you have the latest version installed
az extension update --name aks-preview
```


### Register the `AdvancedNetworkingWireGuardPreview`

feature flag

Register the `AdvancedNetworkingWireGuardPreview`

feature flag using the [ az feature register](/en-us/cli/azure/feature#az-feature-register) command.

```
az feature register --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingWireGuardPreview"
```


Verify successful registration using the [ az feature show](/en-us/cli/azure/feature#az-feature-show) command. It takes a few minutes for the registration to complete.

```
az feature show --namespace "Microsoft.ContainerService" --name "AdvancedNetworkingWireGuardPreview"
```


Once the feature shows `Registered`

, refresh the registration of the `Microsoft.ContainerService`

resource provider using the [ az provider register](/en-us/cli/azure/provider#az-provider-register) command.

### Enable Advanced Container Networking Services and WireGuard

To proceed, you must have an AKS cluster with [Advanced Container Networking Services](advanced-container-networking-services-overview) enabled.

The `az aks create`

command with the Advanced Container Networking Services flag, `--enable-acns`

, creates a new AKS cluster with all Advanced Container Networking Services features. These features encompass:

**Container Network Observability:**Provides insights into your network traffic. To learn more visit[Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability).**Container Network Security:**Offers security features like Fully Qualified Domain Name (FQDN) filtering. To learn more visit[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security).

Note

Clusters with the Cilium data plane support Container Network Observability and Container Network security starting with Kubernetes version 1.29.
WireGuard is disabled by default even after enabling ACNS. To enable WireGuard set the encryption type by using the flag `--acns-transit-encryption-type wireguard`

.

```
# Set environment variables for the AKS cluster name and resource group. Make sure to replace the placeholders with your own values.
export CLUSTER_NAME="<aks-cluster-name>"
export RESOURCE_GROUP="<resourcegroup-name>"
# Create an AKS cluster
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP \
--location eastus \
--network-plugin azure \
--network-plugin-mode overlay \
--network-dataplane cilium \
--enable-acns \
--acns-transit-encryption-type wireguard \
--generate-ssh-keys
```


## Enable Advanced Container Networking Services and WireGuard on an existing cluster

The [ az aks update](/en-us/cli/azure/aks#az-aks-update) command with the Advanced Container Networking Services flag,

`--enable-acns`

, updates an existing AKS cluster with all Advanced Container Networking Services features, which includes [Container Network Observability](advanced-container-networking-services-overview?tabs=cilium#container-network-observability)and the

[Container Network Security](advanced-container-networking-services-overview?tabs=cilium#container-network-security)feature.

Important

Enabling WireGuard on an existing cluster will trigger a rollout restart of the Cilium agent across all nodes. For large clusters, this process can take some time and may temporarily impact workloads. It's recommended to plan the update during a maintenance window or low-traffic period to minimise disruption

Note

Only clusters with the Cilium data plane support Container Network Security features of Advanced Container Networking Services.

WireGuard is disabled by default even after enabling ACNS. To enable WireGuard set the encryption type by using the flag `--acns-transit-encryption-type wireguard`

.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-transit-encryption-type wireguard
```


## Get cluster credentials

Get your cluster credentials using the [ az aks get-credentials](/en-us/cli/azure/aks#az-aks-get-credentials) command.

```
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP
```


## Validate the setup

Validate that WireGuard is enabled successfully using cilium-dbg cli

Note

It might take a few minutes for WireGuard to be fully enabled and configured across all nodes after activation.

- Run a bash shell in one of the Cilium pods

```
kubectl -n kube-system exec -ti ds/cilium -- bash
```


- Check that WireGuard is enabled

```
cilium-dbg encrypt status
```


Expected output:

```
Encryption: Wireguard
Interface: cilium_wg0
Public key: jikeOvVATORm/1GD0kZLxKhw1lofdsfdgiXWVyVIR3T0=
Number of peers: 2
```


The number of peers should equal the number of nodes minus one.

## Troubleshooting

When WireGuard encryption is enabled in an AKS cluster using Cilium CNI, you can use the cilium-dbg CLI tool to inspect tunnel status, verify peer connectivity, and debug encryption-related issues.

### Inspect WireGuard peers

You can inspect peer status and configuration on each node using:

```
kubectl exec -n kube-system ds/cilium -- cilium-dbg debuginfo --output json | jq .encryption
```


Expected output:

```
{
"wireguard": {
"interfaces": [
{
"listen-port": 51871,
"name": "cilium_wg0",
"peer-count": 1,
"peers": [
{
"allowed-ips": [
"10.244.1.31/32",
"10.244.1.206/32",
"10.224.0.6/32"
],
"endpoint": "10.224.0.6:51871",
"last-handshake-time": "2025-04-24T11:13:49.102Z",
"public-key": "3qwZEQLdK5IcFcdXxtr1m8RkDqznPVWEEirJ88+zDyk=",
"transfer-rx": 2457024,
"transfer-tx": 15746568
}
],
"public-key": "jikeOvVATORm/1GD0kZLxKhw1lofdsfdgiXWVyVIR3T0="
}
],
"node-encryption": "Disabled"
}
}
```


This output shows the current state of WireGuard encryption on the node.

- listen-port: The UDP port (51871) where this node is listening for encrypted traffic from peers.
- peer-count: The number of remote WireGuard peers configured for this node.
- peers:
- allowed-ips: list of pod IP addresses routed through the encrypted tunnel to this peer.
- endpoint: The IP and port of the remote peer's WireGuard interface.
- last-handshake-time: Timestamp of the most recent successful key exchange with this peer.
- public-key: The public key of the remote peer.
- transfer-rx / transfer-tx: The total number of bytes received/transmitted over the tunnel.

- public-key: The local WireGuard interface’s public key.
- node-encryption: Encrypts traffic originating from the node itself or from host-network pods. At present, only pod traffic is encrypted. Node encryption is not yet supported and remains disabled by default.

## Disabling WireGuard on an existing cluster

WireGuard can be disabled independently without affecting other ACNS features. To disable it, set the flag `--acns-transit-encryption-type=none`

.

```
az aks update \
--resource-group $RESOURCE_GROUP \
--name $CLUSTER_NAME \
--enable-acns \
--acns-transit-encryption-type none
```


## Known issues

- Packets might be dropped when configuring the WireGuard device leading to connectivity issues. This issue happens when endpoints are added or removed or when node updates occur. In some cases, this issue might lead to failed calls to
[sendmsg](https://man7.org/linux/man-pages/man2/sendmsg.2.html)and[sendto](https://man7.org/linux/man-pages/man2/sendto.2.html). For more information, see[GitHub issue 33159](https://github.com/cilium/cilium/issues/33159).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/secure-container-access -->

# Secure container access to resources for Azure Kubernetes Service (AKS) workloads using built-in Linux security features

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to secure container access to resources for your Azure Kubernetes Service (AKS) workloads using the *user namespaces*, *AppArmor*, and *seccomp* built-in Linux security features.

## Overview of container access security

In the same way that you should grant users or groups the minimum privileges required, you should also limit containers to only necessary actions and processes. To minimize the risk of attack, avoid configuring applications and containers that require escalated privileges or root access.

You can use built-in Kubernetes *pod security contexts* to define more permissions, such as the user or group to run as, the Linux capabilities to expose, or setting `allowPrivilegeEscalation: false`

in the pod manifest. For more best practices, see [Secure pod access to resources](https://kubernetes.io/docs/concepts/security/pod-security-standards/).

To improve the host isolation and decrease lateral movement on Linux, you can use *user namespaces*. For even more granular control of container actions, you can use built-in Linux security features such as *AppArmor* and *seccomp*. These features help you limit the actions that containers can perform by defining Linux security features at the node level and implementing them through a pod manifest.

Built-in Linux security features are only available on Linux nodes and pods.

Note

Currently, Kubernetes environments aren't safe for hostile multitenant usage. Other security features, like *Microsoft Defender for Containers*, *AppArmor*, *seccomp*, *user namespaces*, *Pod Security Admission*, or *Kubernetes Role-Based Access Control (RBAC) for nodes*, efficiently block exploits.

For true security when running hostile multitenant workloads, only trust a hypervisor. The security domain for Kubernetes becomes the entire cluster, not an individual node.

For these types of hostile multitenant workloads, you should use physically isolated clusters.

## Prerequisites for user namespaces

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Minimum Kubernetes version 1.33 for the control plane and worker nodes. If you're not using Kubernetes version 1.33 or higher, you need to
[upgrade your Kubernetes version](upgrade-aks-cluster). - Worker nodes running Azure Linux 3.0 or Ubuntu 24.04 to ensure you meet the minimum
[stack requirements](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/#before-you-begin)to enable user namespaces. If you need to upgrade your operating system (OS) version, see[upgrade your OS version](upgrade-os-version).

## Limitations for user namespaces

- The user namespaces feature is for the Linux kernel and isn't supported for Windows node pools.
- Check the
[Kubernetes documentation for user namespaces](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/)for any other limitations.

## Overview of user namespaces

Linux pods run using several namespaces by default: a network namespaces to isolate the network identity and a PID namespace to isolate the processes. A [user namespace (user_namespace)](https://man7.org/linux/man-pages/man7/user_namespaces.7.html) isolates the users inside the container from the users on the host. It also limits the scope of capabilities and the pod's interactions with the rest of the system.

The UIDs and GIDs inside the container are mapped to unprivileged users on the host, so all interaction with the rest of the host happen as those unprivileged UID and GID. For example, root inside the container (UID 0) can be mapped to user 65536 on the host. Kubernetes creates the mapping to guarantee it doesn't overlap with other pods using user-namespaces on the system.

The Kubernetes implementation has some key benefits. To learn more, see the [Kubernetes User Namespaces documentation](https://kubernetes.io/docs/concepts/workloads/pods/user-namespaces/).

## Enable user namespaces

Create a file named

`mypod.yaml`

and copy in the following manifest. To use user-namespaces, the YAML needs to have the field`hostUsers: false`

.`apiVersion: v1 kind: Pod metadata: name: userns spec: hostUsers: false containers: - name: shell command: ["sleep", "infinity"] image: debian`

Deploy the application using the

`kubectl apply`

command and specify the name of your YAML manifest.`kubectl apply -f mypod.yaml`

Check the status of the deployed pods using the

`kubectl get pods`

command.`kubectl get pods`

Exec into the pod using the

`kubectl exec`

command.`kubectl exec -ti userns -- bash`

Inside the pod, check

`/proc/self/uid_map`

using the following command:`cat /proc/self/uid_map`

The output should have

*65536*in the last column. For example:`0 833617920 65536`

This output indicates that root inside the container (UID 0) is mapped to user 65536 on the host.


## Common vulnerabilities and exposures (CVEs) mitigated by user namespaces

The following table outlines some common vulnerabilities and exposures (CVEs) that are either partially or fully mitigated by using user_namespaces:

| CVE | Severity score | Severity level |
|---|---|---|
|

[CVE 2024-21262](https://github.com/opencontainers/runc/security/advisories/GHSA-xr7r-f8xq-vfvv)[CVE 2022-0492](https://unit42.paloaltonetworks.com/cve-2022-0492-cgroups/)[CVE-2021-25741](https://nvd.nist.gov/vuln/detail/CVE-2021-25741)[CVE-2017-1002101](https://nvd.nist.gov/vuln/detail/CVE-2017-1002101)Keep in mind that this list isn't exhaustive. To learn more, see [Kubernetes v1.33: User Namespaces enabled by default](https://kubernetes.io/blog/2025/04/25/userns-enabled-by-default/).

## AppArmor prerequisites

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal).

Note

Azure Linux 3.0 supports AppArmor as of the November 7, 2025 VHD release.

## Overview of AppArmor

To limit container actions, you can use the [AppArmor](https://kubernetes.io/docs/tutorials/clusters/apparmor/) Linux kernel security module. AppArmor is available as part of the underlying AKS node operating system (OS) and is enabled by default. You can create AppArmor profiles that restrict read, write, or execute actions, or system functions like mounting filesystems. Default AppArmor profiles restrict access to various `/proc`

and `/sys`

locations and provide a means to logically isolate containers from the underlying node. AppArmor works for any application that runs on Linux, not just Kubernetes pods.

Note

Before Kubernetes v1.30, AppArmor was specified through annotations. From v1.30 onwards, AppArmor is specified through the `securityContext`

field in the pod specification. For more information, see the [Kubernetes AppArmor documentation](https://kubernetes.io/docs/tutorials/clusters/apparmor/).

## Secure pods with AppArmor

You can specify AppArmor profiles at the pod or container level. The container AppArmor profile takes precedence over the pod AppArmor profile. If neither is specified, the container runs unconfined. For more information on AppArmor profiles, see the [Securing a Pod with AppArmor Kubernetes documentation](https://kubernetes.io/docs/tutorials/clusters/apparmor/).

## Configure a custom AppArmor profile

The following example creates a profile that prevents writing to files from within a container.

[SSH](manage-ssh-node-access)to an AKS node.Create a file named

*deny-write.profile*and paste in the following content:`#include <tunables/global> profile k8s-apparmor-example-deny-write flags=(attach_disconnected) { #include <abstractions/base> file, # Deny all file writes. deny /** w, }`

Load the AppArmor profile onto the node.

`# This example assumes that node names match host names, and are reachable via SSH. NODES=($( kubectl get node -o jsonpath='{.items[*].status.addresses[?(.type == "Hostname")].address}' )) for NODE in ${NODES[*]}; do ssh $NODE 'sudo apparmor_parser -q <<EOF #include <tunables/global> profile k8s-apparmor-example-deny-write flags=(attach_disconnected) { #include <abstractions/base> file, # Deny all file writes. deny /** w, } EOF' done`


## Deploy a pod with the custom AppArmor profile

Deploy a

*"Hello AppArmor"*pod with the deny-write profile.`apiVersion: v1 kind: Pod metadata: name: hello-apparmor spec: securityContext: appArmorProfile: type: Localhost localhostProfile: k8s-apparmor-example-deny-write containers: - name: hello image: busybox:1.28 command: [ "sh", "-c", "echo 'Hello AppArmor!' && sleep 1h" ]`

Apply the pod manifest using the

`kubectl apply`

command.`kubectl apply -f hello-apparmor.yaml`

Exec into the pod and verify the container is running with the AppArmor profile.

`kubectl exec hello-apparmor -- cat /proc/1/attr/current`

The output should show the AppArmor profile in use. For example:

`k8s-apparmor-example-deny-write (enforce)`


## Seccomp prerequisites

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - You need to
[register the](#register-the-kubeletdefaultseccompprofilepreview-feature-flag)to use default seccomp profiles on your node pools.`KubeletDefaultSeccompProfilePreview`

feature flag

### Register the `KubeletDefaultSeccompProfilePreview`

feature flag

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Register the

`KubeletDefaultSeccompProfilePreview`

feature flag using thecommand.`az feature register`

`az feature register --namespace "Microsoft.ContainerService" --name "KubeletDefaultSeccompProfilePreview"`

It takes a few minutes for the status to show

*Registered*.Verify the registration status using the

command.`az feature show`

`az feature show --namespace "Microsoft.ContainerService" --name "KubeletDefaultSeccompProfilePreview"`

When the status reflects

*Registered*, refresh the registration of the*Microsoft.ContainerService*resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Seccomp limitations

- AKS only supports the default seccomp profiles (
`RuntimeDefault`

and`Unconfined`

). Custom seccomp profiles aren't supported. `SeccompDefault`

isn't a supported parameter for Windows node pools.

## Overview of default seccomp profiles (preview)

While AppArmor works for any Linux application, [seccomp (or secure computing)](https://kubernetes.io/docs/reference/node/seccomp/) works at the process level. Seccomp is also a Linux kernel security module. The

`containerd`

runtime used by AKS nodes provides native support for seccomp. With seccomp, you can limit a container's system calls. Seccomp establishes an extra layer of protection against common system call vulnerabilities exploited by malicious actors and allows you to specify a default profile for all workloads in the node.You can apply default seccomp profiles using [custom node configurations](/en-us/azure/aks/custom-node-configuration) when creating a new Linux node pool. AKS supports the `RuntimeDefault`

and `Unconfined`

values. Some workloads might require a lower number of syscall restrictions than others. This means that they can fail during runtime with the `RuntimeDefault`

profile. To mitigate such a failure, you can specify the `Unconfined`

profile. If your workload requires a custom profile, see [Configure a custom seccomp profile](#configure-a-custom-seccomp-profile).

### Restrict container system calls with seccomp

[Follow steps to apply a seccomp profile in your kubelet configuration](/en-us/azure/aks/custom-node-configuration)by specifying`"seccompDefault": "RuntimeDefault"`

.[Connect to the host](node-access).- Verify the configuration was applied to the nodes.

#### Resolve workload failures with seccomp

When `SeccompDefault`

is enabled, the container runtime default seccomp profile is used by default for all workloads scheduled on the node, which might cause workloads to fail due to blocked syscalls. If a workload failure occurs, you might see errors such as:

- Workload is exiting unexpectedly after the feature is enabled, with "permission denied" error.
- Seccomp error messages can also be seen in auditd or syslog by replacing SCMP_ACT_ERRNO with SCMP_ACT_LOG in the default profile.

If you experience these errors, we recommend that you change your seccomp profile to `Unconfined`

. `Unconfined`

places no restrictions on syscalls, allowing all system calls to be executed.

## Overview of custom seccomp profiles

With a custom seccomp profile, you have more granular control over restricted syscalls for your containers. You can create your own seccomp profiles by:

- Using filters to specify what actions to allow or deny.
- Annotating within a pod YAML manifest to associate with the seccomp filter.

Note

For help with troubleshooting your seccomp profile, see [Troubleshoot seccomp profile configuration in Azure Kubernetes Service (AKS)](/en-us/troubleshoot/azure/azure-kubernetes/security/troubleshoot-seccomp-profiles).

### Configure a custom seccomp profile

To see seccomp in action, create a filter that prevents changing permissions on a file.

[SSH](manage-ssh-node-access)to an AKS node.Create a seccomp filter named

*/var/lib/kubelet/seccomp/prevent-chmod*.Copy and paste the following content:

`{ "defaultAction": "SCMP_ACT_ALLOW", "syscalls": [ { "name": "chmod", "action": "SCMP_ACT_ERRNO" }, { "name": "fchmodat", "action": "SCMP_ACT_ERRNO" }, { "name": "chmodat", "action": "SCMP_ACT_ERRNO" } ] }`

In version 1.19 and later, you need to configure:

`{ "defaultAction": "SCMP_ACT_ALLOW", "syscalls": [ { "names": ["chmod","fchmodat","chmodat"], "action": "SCMP_ACT_ERRNO" } ] }`

From your local machine, create a pod manifest named

*aks-seccomp.yaml*and paste the following content. This manifest defines an annotation for`seccomp.security.alpha.kubernetes.io`

and references the existing*prevent-chmod*filter.`apiVersion: v1 kind: Pod metadata: name: chmod-prevented annotations: seccomp.security.alpha.kubernetes.io/pod: localhost/prevent-chmod spec: containers: - name: chmod image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: - "chmod" args: - "777" - /etc/hostname restartPolicy: Never`

In version 1.19 and later, you need to configure:

`apiVersion: v1 kind: Pod metadata: name: chmod-prevented spec: securityContext: seccompProfile: type: Localhost localhostProfile: prevent-chmod containers: - name: chmod image: mcr.microsoft.com/dotnet/runtime-deps:6.0 command: - "chmod" args: - "777" - /etc/hostname restartPolicy: Never`

Deploy the sample pod using the

command:`kubectl apply`

`kubectl apply -f ./aks-seccomp.yaml`

View the pod status using the

command.`kubectl get pods`

`kubectl get pods`

In the output, you should see the pod reports an error. The

`chmod`

command is prevented from running by the seccomp filter, as shown in the example output:`NAME READY STATUS RESTARTS AGE chmod-prevented 0/1 Error 0 7s`


## Seccomp security profile options

Seccomp security profiles are a set of defined syscalls that are allowed or restricted. Most container runtimes have a default seccomp profile that's similar if not the same as the one Docker uses. For more information about available profiles, see the [Docker](https://kubernetes.io/docs/reference/node/seccomp/) or [containerd](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) default seccomp profiles.

AKS uses the [containerd](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) default seccomp profile for the `RuntimeDefault`

when you configure seccomp using [custom node configuration](/en-us/azure/aks/custom-node-configuration).

### Significant syscalls blocked by default profile

Both [Docker](https://kubernetes.io/docs/reference/node/seccomp/) and [containerd](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51) maintain allow lists of safe syscalls. When changes are made to [Docker](https://kubernetes.io/docs/reference/node/seccomp/) and [containerd](https://github.com/containerd/containerd/blob/f0a32c66dad1e9de716c9960af806105d691cd78/contrib/seccomp/seccomp_default.go#L51), AKS updates the default configuration to match. Updates to this list might cause workload failure. For release updates, see [AKS release notes](https://github.com/Azure/AKS/releases).

The following table lists significant syscalls that are effectively blocked because they aren't on the allow list. This list isn't exhaustive. If your workload requires any of the blocked syscalls, don't use the `RuntimeDefault`

seccomp profile.

| Blocked syscall | Description |
|---|---|
`acct` |
Accounting syscall, which could let containers disable their own resource limits or process accounting. Also gated by `CAP_SYS_PACCT` . |
`add_key` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`bpf` |
Deny loading potentially persistent bpf programs into kernel, already gated by `CAP_SYS_ADMIN` . |
`clock_adjtime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`clock_settime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`clone` |
Deny cloning new namespaces. Also gated by `CAP_SYS_ADMIN for CLONE_*` flags, except `CLONE_NEWUSER` . |
`create_module` |
Deny manipulation and functions on kernel modules. Obsolete. Also gated by `CAP_SYS_MODULE` . |
`delete_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`finit_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`get_kernel_syms` |
Deny retrieval of exported kernel and module symbols. Obsolete. |
`get_mempolicy` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`init_module` |
Deny manipulation and functions on kernel modules. Also gated by `CAP_SYS_MODULE` . |
`ioperm` |
Prevent containers from modifying kernel I/O privilege levels. Already gated by `CAP_SYS_RAWIO` . |
`iopl` |
Prevent containers from modifying kernel I/O privilege levels. Already gated by `CAP_SYS_RAWIO` . |
`kcmp` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`kexec_file_load` |
Sister syscall of kexec_load that does the same thing, slightly different arguments. Also gated by `CAP_SYS_BOOT` . |
`kexec_load` |
Deny loading a new kernel for later execution. Also gated by `CAP_SYS_BOOT` . |
`keyctl` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`lookup_dcookie` |
Tracing/profiling syscall, which could leak information on the host. Also gated by `CAP_SYS_ADMIN` . |
`mbind` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`mount` |
Deny mounting, already gated by `CAP_SYS_ADMIN` . |
`move_pages` |
Syscall that modifies kernel memory and NUMA settings. |
`nfsservctl` |
Deny interaction with the kernel nfs daemon. Obsolete since Linux 3.1. |
`open_by_handle_at` |
Cause of an old container breakout. Also gated by `CAP_DAC_READ_SEARCH` . |
`perf_event_open` |
Tracing/profiling syscall, which could leak information on the host. |
`personality` |
Prevent container from enabling BSD emulation. Not inherently dangerous, but poorly tested, potential for kernel vulns. |
`pivot_root` |
Deny pivot_root, should be privileged operation. |
`process_vm_readv` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`process_vm_writev` |
Restrict process inspection capabilities, already blocked by dropping `CAP_SYS_PTRACE` . |
`ptrace` |
Tracing/profiling syscall. Blocked in Linux kernel versions before 4.8 to avoid seccomp bypass. Tracing/profiling arbitrary processes is already blocked by dropping `CAP_SYS_PTRACE` , because it could leak information on the host. |
`query_module` |
Deny manipulation and functions on kernel modules. Obsolete. |
`quotactl` |
Quota syscall, which could let containers disable their own resource limits or process accounting. Also gated by `CAP_SYS_ADMIN` . |
`reboot` |
Don't let containers reboot the host. Also gated by `CAP_SYS_BOOT` . |
`request_key` |
Prevent containers from using the kernel keyring, which isn't namespaced. |
`set_mempolicy` |
Syscall that modifies kernel memory and NUMA settings. Already gated by `CAP_SYS_NICE` . |
`setns` |
Deny associating a thread with a namespace. Also gated by `CAP_SYS_ADMIN` . |
`settimeofday` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`stime` |
Time/date isn't namespaced. Also gated by `CAP_SYS_TIME` . |
`swapon` |
Deny start/stop swapping to file/device. Also gated by `CAP_SYS_ADMIN` . |
`swapoff` |
Deny start/stop swapping to file/device. Also gated by `CAP_SYS_ADMIN` . |
`sysfs` |
Obsolete syscall. |
`_sysctl` |
Obsolete, replaced by `/proc/sys` . |
`umount` |
Should be a privileged operation. Also gated by `CAP_SYS_ADMIN` . |
`umount2` |
Should be a privileged operation. Also gated by `CAP_SYS_ADMIN` . |
`unshare` |
Deny cloning new namespaces for processes. Also gated by `CAP_SYS_ADMIN` (except for `unshare --user` ). |
`uselib` |
Older syscall related to shared libraries, unused for a long time. |
`userfaultfd` |
Userspace page fault handling, largely needed for process migration. |
`ustat` |
Obsolete syscall. |
`vm86` |
In kernel x86 real mode virtual machine. Also gated by `CAP_SYS_ADMIN` . |
`vm86old` |
In kernel x86 real mode virtual machine. Also gated by `CAP_SYS_ADMIN` . |

## Related content

To learn more about securing your AKS cluster, see the following articles:

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/limit-egress-traffic -->

# Limit network traffic with Azure Firewall in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to use the [outbound network and fully qualified domain name (FQDN) rules for AKS clusters](outbound-rules-control-egress) to control egress traffic using Azure Firewall. To simplify this configuration, Azure Firewall provides an Azure Kubernetes Service (`AzureKubernetesService`

) FQDN tag that restricts outbound traffic from the AKS cluster.

## Firewall frontend IP requirements

**Production minimum**: Use at least 20 frontend IPs on Azure Firewall to avoid source network address translation (SNAT) port exhaustion.**High-traffic clusters**: If your cluster creates many outbound connections to the same destinations, you might need more frontend IPs to avoid maxing out ports per IP**API server protection**: Add the firewall's public frontend IP to[API server authorized IP ranges](api-server-authorized-ip-ranges)for enhanced security**Developer access**: When using authorized IP ranges, either use a jumpbox in the firewall's virtual network (VNet) or add developer endpoint IPs to the authorized range

This guidance applies throughout the configuration process described in this article.

Note

The FQDN tag contains all the FQDNs listed in [outbound network and FQDN rules for AKS clusters](outbound-rules-control-egress) and is automatically updated.

## Architecture overview

The following diagram illustrates the architecture of an AKS cluster with restricted egress traffic using Azure Firewall:

Key components of this architecture include:

**Public ingress is forced to flow through firewall filters**:- AKS agent nodes are isolated in a dedicated subnet.
[Azure Firewall](/en-us/azure/firewall/overview)is deployed in its own subnet.- A DNAT rule translates the firewall public IP into the load balancer frontend IP.

**Outbound requests start from agent nodes to the Azure Firewall internal IP using a**:[user-defined route (UDR)](egress-outboundtype)- Requests from AKS agent nodes follow a UDR that has been placed on the subnet the AKS cluster was deployed into.
- Azure Firewall egresses out of the VNet from a public IP frontend.
- Access to the public internet or other Azure services flows to and from the firewall frontend IP address.
- You can protect access to the AKS control plane using
[API server authorized IP ranges](api-server-authorized-ip-ranges), including the firewall public frontend IP address.

**Internal traffic**:- You can use an
[internal load balancer](internal-lb)for internal traffic, which you could isolate on its own subnet, instead of or alongside a[public load balancer](load-balancer-standard).

- You can use an

## Configure environment variables

The following table lists the environment variables used in this article. Set these variables in your shell before proceeding, or modify the commands to use your own values.

| Variable | Description | Example value |
|---|---|---|
`PREFIX` |
Prefix for resource names | `aks-egress` |
`RESOURCE_GROUP` |
Name of the resource group | `aks-egress-rg` |
`LOCATION` |
Azure region for resources | `eastus` |
`PLUGIN` |
Network plugin for AKS | `azure` |
`CLUSTER_NAME` |
Name of the AKS cluster | `aks-egress` |
`VNET_NAME` |
Name of the virtual network | `aks-egress-vnet` |
`AKS_SUBNET_NAME` |
Name of the subnet for AKS | `aks-subnet` |
`FW_SUBNET_NAME` |
Name of the subnet for Azure Firewall | `AzureFirewallSubnet` |
`FW_NAME` |
Name of the Azure Firewall | `aks-egress-fw` |
`FW_PUBLICIP_NAME` |
Name of the public IP for Azure Firewall | `aks-egress-fwpublicip` |
`FW_IPCONFIG_NAME` |
Name of the IP configuration for Azure Firewall | `aks-egress-fwconfig` |
`FW_ROUTE_TABLE_NAME` |
Name of the route table for Azure Firewall | `aks-egress-fwrt` |
`FW_ROUTE_NAME_1` |
Name of the route for Azure Firewall | `aks-egress-fwrn` |
`FW_ROUTE_NAME_2` |
Name of the internet route for Azure Firewall | `aks-egress-fwrn-internet` |

## Create a resource group

Create a resource group using the

command.`az group create`

`az group create --name $RESOURCE_GROUP --location $LOCATION`


## Create a virtual network with multiple subnets

Provision a VNet with two separate subnets: one for the cluster and one for the firewall. Optionally, you can create one for internal service ingress. The following diagram illustrates the empty network topology before deploying any resources:

Create a VNet using the

command.`az network vnet create`

`az network vnet create \ --resource-group $RESOURCE_GROUP \ --name $VNET_NAME \ --location $LOCATION \ --address-prefixes 10.42.0.0/16 \ --subnet-name $AKS_SUBNET_NAME \ --subnet-prefix 10.42.1.0/24`

Create a subnet for Azure Firewall using the

command.`az network vnet subnet create`

`# Dedicated subnet for Azure Firewall (subnet must be named "AzureFirewallSubnet") az network vnet subnet create \ --resource-group $RESOURCE_GROUP \ --vnet-name $VNET_NAME \ --name $FW_SUBNET_NAME \ --address-prefix 10.42.2.0/24`


## Create a public IP for Azure Firewall

Create a standard SKU public IP resource using the

command. This resource is used as the frontend IP address for the Azure Firewall.`az network public-ip create`

`az network public-ip create --resource-group $RESOURCE_GROUP --name $FW_PUBLICIP_NAME --location $LOCATION --sku "Standard"`


## Install the Azure Firewall CLI extension

Register the

[Azure Firewall CLI extension](https://github.com/Azure/azure-cli-extensions/tree/main/src/azure-firewall)to create an Azure Firewall using thecommand.`az extension add`

`az extension add --name azure-firewall`


## Create an Azure Firewall and enable DNS proxy

Note

For high-traffic scenarios, see the [firewall frontend IP requirements](#firewall-frontend-ip-requirements) section.

For more information on how to create an Azure Firewall with multiple IPs, see [Create an Azure Firewall with multiple public IP addresses using Bicep](/en-us/azure/firewall/quick-create-multiple-ip-bicep).

Create an Azure Firewall and enable DNS proxy using the

command with`az network firewall create`

`--enable-dns-proxy`

set to`true`

.`az network firewall create --resource-group $RESOURCE_GROUP --name $FW_NAME --location $LOCATION --enable-dns-proxy true`

Setting up the public IP address to the Azure Firewall might take a few minutes. Once it's ready, you can assign the IP address to the firewall front end.

Note

To use FQDN on network rules, you need DNS proxy enabled. When DNS proxy is enabled, the firewall listens on port 53 and forwards DNS requests to the DNS server you specify. This setting allows the firewall to automatically translate the FQDN.


## Create an IP configuration for Azure Firewall

Create an Azure Firewall IP configuration using the

command.`az network firewall ip-config create`

`az network firewall ip-config create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --name $FW_IPCONFIG_NAME --public-ip-address $FW_PUBLICIP_NAME --vnet-name $VNET_NAME`


## Get the Azure Firewall IP addresses

Save the public and private firewall frontend IP addresses for configuration later using the following commands:

`export FW_PUBLIC_IP=$(az network public-ip show --resource-group $RESOURCE_GROUP --name $FW_PUBLICIP_NAME --query "ipAddress" -o tsv) export FW_PRIVATE_IP=$(az network firewall show --resource-group $RESOURCE_GROUP --name $FW_NAME --query "ipConfigurations[0].privateIPAddress" -o tsv)`

Note

For API server security, see the

[firewall frontend IP requirements](#firewall-frontend-ip-requirements)section.

## UDR configuration for AKS egress through Azure Firewall

Azure automatically routes traffic between Azure subnets, VNets, and on-premises networks. To modify default routing, create a route table with the following requirements:

**Required route parameters**:

**Route destination**:`0.0.0.0/0`

(all traffic)**Next hop type**: Network virtual appliance (NVA)**Next hop IP**: Azure Firewall private IP address**Association**: One route table per subnet (*zero*or*one*allowed)

**UDR constraints**:

- Default internet route (
`0.0.0.0/0`

) already exists but requires public IP for SNAT. - Route must point to gateway/NVA, not directly to internet.
- AKS validates route configuration and prevents direct internet routes.
- Each subnet supports maximum of
*one*associated route table.

**Outbound type impact**:

**UDR (**: No load balancer public IP created for outbound requests.`userDefinedRouting`

)**Load Balancer public IP**: Only created for inbound requests with`LoadBalancer`

service type.**SNAT configuration**: Requires proper public IP configuration for outbound connectivity.

For more information, see [Outbound rules for Azure Load Balancer](/en-us/azure/load-balancer/outbound-rules#scenario6out).

## Create a route with a hop to Azure Firewall

Create an empty route table using the

command. The route table defines the Azure Firewall as the next hop. Each subnet can have`az network route-table create`

*zero*or*one*route table associated to it.`az network route-table create --resource-group $RESOURCE_GROUP --location $LOCATION --name $FW_ROUTE_TABLE_NAME`

Create routes in the route table for the subnets using the

command.`az network route-table route create`

`az network route-table route create --resource-group $RESOURCE_GROUP --name $FW_ROUTE_NAME_1 --route-table-name $FW_ROUTE_TABLE_NAME --address-prefix 0.0.0.0/0 --next-hop-type VirtualAppliance --next-hop-ip-address $FW_PRIVATE_IP az network route-table route create --resource-group $RESOURCE_GROUP --name $FW_ROUTE_NAME_2 --route-table-name $FW_ROUTE_TABLE_NAME --address-prefix $FW_PUBLIC_IP/32 --next-hop-type Internet`


For information on how to override Azure's default system routes or add more routes to a subnet's route table, see the [Virtual network route table documentation](/en-us/azure/virtual-network/virtual-networks-udr-overview#user-defined).

## Azure Firewall outbound rules for AKS

Note

For applications outside of the `kube-system`

or `gatekeeper-system`

namespaces that need to talk to the API server, an extra network rule to allow TCP communication to port 443 for the API server IP in addition to adding application rule for `fqdn-tag`

of `AzureKubernetesService`

is required.

The following network rules are required for AKS egress traffic control through Azure Firewall:

- The first network rule allows access to port 9000 via TCP.
- The second network rule allows access to port 1194 via UDP. If you're deploying to Microsoft Azure operated by 21Vianet, see the
[Azure operated by 21Vianet required network rules](outbound-rules-control-egress#microsoft-azure-operated-by-21vianet-required-network-rules). In this article, the commands use the`AzureCloud.$LOCATION`

service tag as the destination address. Service tags represent groups of IP address prefixes for Azure services in specific regions. This automatically includes the appropriate CIDR ranges for Azure services without requiring manual IP range specification. - The third network rule opens port 123 to
`ntp.ubuntu.com`

FQDN via UDP. Adding an FQDN as a network rule is one of the specific features of Azure Firewall, so you need to adapt it when using your own options. - The fourth and fifth network rules allow access to pull containers from GitHub Container Registry (
`ghcr.io`

) and Docker Hub (`docker.io`

).

## Create network rules on Azure Firewall

Create the network rules using the following

commands.`az network firewall network-rule create`

`az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'apitcp' --protocols 'TCP' --source-addresses '*' --destination-addresses "AzureCloud.$LOCATION" --destination-ports 9000 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'apiudp' --protocols 'UDP' --source-addresses '*' --destination-addresses "AzureCloud.$LOCATION" --destination-ports 1194 --action allow --priority 100 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'time' --protocols 'UDP' --source-addresses '*' --destination-fqdns 'ntp.ubuntu.com' --destination-ports 123 az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'ghcr' --protocols 'TCP' --source-addresses '*' --destination-fqdns ghcr.io pkg-containers.githubusercontent.com --destination-ports '443' az network firewall network-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwnr' --name 'docker' --protocols 'TCP' --source-addresses '*' --destination-fqdns docker.io registry-1.docker.io production.cloudflare.docker.com --destination-ports '443'`


## Create application rules on Azure Firewall

Create the application rule using the

command.`az network firewall application-rule create`

`az network firewall application-rule create --resource-group $RESOURCE_GROUP --firewall-name $FW_NAME --collection-name 'aksfwar' --name 'fqdn' --source-addresses '*' --protocols 'http=80' 'https=443' --fqdn-tags "AzureKubernetesService" --action allow --priority 100`


To learn more about Azure Firewall, see the [Azure Firewall documentation](/en-us/azure/firewall/overview).

## Associate the route table to AKS

To associate the cluster with the firewall, the dedicated subnet for the cluster's subnet must reference the route table.

Associate the route table to AKS using the

command.`az network vnet subnet update`

`az network vnet subnet update --resource-group $RESOURCE_GROUP --vnet-name $VNET_NAME --name $AKS_SUBNET_NAME --route-table $FW_ROUTE_TABLE_NAME`


## Deploy an AKS cluster that follows your outbound rules

You can now deploy an AKS cluster into the existing VNet. You use the [ userDefinedRouting outbound type](egress-outboundtype), which ensures that any outbound traffic is forced through the firewall and no other egress paths exist. You can also use the

[.](egress-outboundtype#outbound-type-of-loadbalancer)

`loadBalancer`

outbound typeSet an environment variable for the subnet ID of the target subnet using the following command:

`SUBNET_ID=$(az network vnet subnet show --resource-group $RESOURCE_GROUP --vnet-name $VNET_NAME --name $AKS_SUBNET_NAME --query id -o tsv)`


You define the outbound type to use the UDR that already exists on the subnet. This configuration enables AKS to skip the setup and IP provisioning for the load balancer.

Tip

You can add extra features to the cluster deployment, such as [ private clusters](private-clusters).

For API server authorized IP ranges setup and developer access considerations, see the [firewall frontend IP requirements](#firewall-frontend-ip-requirements) section.

## Create an AKS cluster with system-assigned identities

Note

AKS creates a system-assigned kubelet identity in the node resource group if you don't [specify your own kubelet managed identity](use-managed-identity#create-a-kubelet-managed-identity).

For user-defined routing, system-assigned identity only supports the CNI network plugin.

Create an AKS cluster using a system-assigned managed identity with the CNI network plugin using the

command.`az aks create`

`az aks create --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --location $LOCATION \ --node-count 3 \ --network-plugin azure \ --outbound-type userDefinedRouting \ --vnet-subnet-id $SUBNET_ID \ --api-server-authorized-ip-ranges $FW_PUBLIC_IP \ --generate-ssh-keys`


## Create user-assigned identities

If you don't have user-assigned identities, follow the steps in this section. If you already have user-assigned identities, skip to [Create an AKS cluster with user-assigned identities](#create-an-aks-cluster-with-user-assigned-identities).

Create a managed identity using the

command.`az identity create`

`az identity create --name myIdentity --resource-group $RESOURCE_GROUP`

The output should resemble the following example output:

`{ ... "id": "/subscriptions/<subscriptionid>/resourcegroups/aks-egress-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myIdentity", "location": "eastus", "name": "myIdentity", ... "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`

Create a kubelet managed identity using the

command.`az identity create`

`az identity create --name myKubeletIdentity --resource-group $RESOURCE_GROUP`

The output should resemble the following example output:

`{ ... "id": "/subscriptions/<subscriptionid>/resourcegroups/aks-egress-rg/providers/Microsoft.ManagedIdentity/userAssignedIdentities/myKubeletIdentity", "location": "eastus", "name": "myKubeletIdentity", ... "resourceGroup": "aks-egress-rg", ... "type": "Microsoft.ManagedIdentity/userAssignedIdentities" }`


Note

If you create your own VNet and route table where the resources are outside of the worker node resource group, the CLI automatically adds the role assignment. If you're using an ARM template or other method, you need to use the principal ID of the cluster managed identity to perform a [role assignment](use-managed-identity#add-a-role-assignment-for-a-system-assigned-managed-identity).

## Create an AKS cluster with user-assigned identities

Create an AKS cluster with your existing user-assigned managed identities in the subnet using the

command. Provide the resource ID of the managed identity for the control plane and the resource ID of the kubelet identity.`az aks create`

`az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --location $LOCATION \ --node-count 3 \ --network-plugin kubenet \ --outbound-type userDefinedRouting \ --vnet-subnet-id $SUBNET_ID \ --api-server-authorized-ip-ranges $FW_PUBLIC_IP \ --assign-identity <identity-resource-id> \ --assign-kubelet-identity <kubelet-identity-resource-id> \ --generate-ssh-keys`


## Enable developer access to the API server

If you used authorized IP ranges for your cluster in the previous step, you need to add your developer tooling IP addresses to the AKS cluster list of approved IP ranges so you access the API server from there. You can also configure a jumpbox with the needed tooling inside a separate subnet in the firewall's VNet.

Retrieve your IP address using the following command:

`CURRENT_IP=$(dig @resolver1.opendns.com ANY myip.opendns.com +short)`

Add the IP address to the approved ranges using the

command.`az aks update`

`az aks update --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME --api-server-authorized-ip-ranges $CURRENT_IP/32`


## Connect to the AKS cluster

Configure

`kubectl`

to connect to your AKS cluster using thecommand.`az aks get-credentials`

`az aks get-credentials --resource-group $RESOURCE_GROUP --name $CLUSTER_NAME`


## Deploy a public service on AKS

You can now start exposing services and deploying applications to this cluster. This example exposes a public service, but you also might want to expose an internal service using an [internal load balancer](internal-lb).

Review the

[AKS Store Demo quickstart](https://github.com/Azure-Samples/aks-store-demo/blob/main/aks-store-quickstart.yaml)manifest to understand the deployed components.Deploy the service using the

`kubectl apply`

command.`kubectl apply -f https://raw.githubusercontent.com/Azure-Samples/aks-store-demo/main/aks-store-quickstart.yaml`


## Get the load balancer internal IP and service IP

Get the internal IP address assigned to the load balancer using the

`kubectl get services`

command.`kubectl get services`

The IP address should be listed in the

`EXTERNAL-IP`

column, as shown in the following example output:`NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE kubernetes ClusterIP 10.0.0.1 <none> 443/TCP 9m10s order-service ClusterIP 10.0.104.144 <none> 3000/TCP 11s product-service ClusterIP 10.0.237.60 <none> 3002/TCP 10s rabbitmq ClusterIP 10.0.161.128 <none> 5672/TCP,15672/TCP 11s store-front LoadBalancer 10.0.89.139 20.39.18.6 80:32271/TCP 10s`

Get the service IP using the

`kubectl get svc store-front`

command.`SERVICE_IP=$(kubectl get svc store-front -o jsonpath='{.status.loadBalancer.ingress[*].ip}')`


## Create a DNAT rule on Azure Firewall

Important

When you use Azure Firewall to restrict egress traffic and create a UDR to force all egress traffic, make sure you create an appropriate DNAT rule in Azure Firewall to correctly allow ingress traffic. Using Azure Firewall with a UDR breaks the ingress setup due to asymmetric routing. The issue occurs if the AKS subnet has a default route that goes to the firewall's private IP address, but you're using a public load balancer - ingress or Kubernetes service of type `loadBalancer`

. In this case, the incoming load balancer traffic is received via its public IP address, but the return path goes through the firewall's private IP address. Because the firewall is stateful, it drops the returning packet because the firewall isn't aware of an established session. To learn how to integrate Azure Firewall with your ingress or service load balancer, see [Integrate Azure Firewall with Azure Standard Load Balancer](/en-us/azure/firewall/integrate-lb).

To configure inbound connectivity, you need to write a DNAT rule to the Azure Firewall. To test connectivity to your cluster, a rule is defined for the firewall frontend public IP address to route to the internal IP exposed by the internal service. You can customize the destination address. The translated address must be the IP address of the internal load balancer. The translated port must be the exposed port for your Kubernetes service. You also need to specify the internal IP address assigned to the load balancer created by the Kubernetes service.

Add the NAT rule using the

command.`az network firewall nat-rule create`

`az network firewall nat-rule create --collection-name exampleset --destination-addresses $FW_PUBLIC_IP --destination-ports 80 --firewall-name $FW_NAME --name inboundrule --protocols Any --resource-group $RESOURCE_GROUP --source-addresses '*' --translated-port 80 --action Dnat --priority 100 --translated-address $SERVICE_IP`


## Validate connectivity

Navigate to the Azure Firewall frontend IP address in a browser to validate connectivity. You should see the AKS store app. In this example, the firewall public IP was

`52.253.228.132`

:, you can view products, add them to your cart, and then place an order.


## Clean up resources

If you no longer need the resources created in this article, you can delete them to avoid incurring future costs.

Delete the AKS resource group using the

command.`az group delete`

`az group delete --name $RESOURCE_GROUP`

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/dns-concepts -->

# DNS Resolution in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Domain Name System (DNS) resolution is a critical component in Azure Kubernetes Service (AKS), enabling pods and services to communicate using human-readable names instead of IP addresses. AKS provides built-in DNS services to ensure seamless name resolution for both internal cluster resources and external endpoints. Understanding how DNS works in AKS helps cluster operators and developers ensure reliable connectivity, optimize performance, and troubleshoot networking issues effectively.

## CoreDNS in Azure Kubernetes Service

[CoreDNS](https://coredns.io/) is the default DNS service in Azure Kubernetes Service (AKS), providing internal name resolution and service discovery for workloads running in the cluster. It operates as a set of pods in the kube-system namespace and is tightly integrated with Kubernetes networking.

When a pod in AKS issues a DNS query—such as resolving the name of another service—the request is routed to the CoreDNS pods. These pods process the query and return the appropriate IP address or forward the request to an upstream DNS server for external domains.

This architecture ensures a balance between flexibility and operational safety in a managed environment. For details on how to customize CoreDNS in AKS, refer to the [CoreDNS customization guide](coredns-custom).

For information on the CoreDNS project, see [the CoreDNS upstream project page](https://coredns.io/).

## LocalDNS in Azure Kubernetes Service

Note

This document provides an overview of what LocalDNS is and its benefits in AKS. It doesn't include setup instructions. For guidance on enabling and configuring LocalDNS, see the [LocalDNS how-to guide](localdns-custom).

### Overview

LocalDNS is an advanced feature in Azure Kubernetes Service (AKS) that deploys a Domain Name System (DNS) proxy on each node to provide highly resilient, low-latency DNS resolution. By handling DNS queries locally, this proxy reduces traffic to the CoreDNS addon pods, improving overall DNS reliability and performance in the cluster. LocalDNS is especially beneficial in large clusters or environments with high DNS query volumes, where centralized DNS resolution can become a bottleneck.

When LocalDNS is enabled, AKS deploys a local DNS cache as a `systemd`

service on each node. Pods on the node send their DNS queries to this local cache, enabling faster resolution by reducing network hops. This approach also minimizes `conntrack`

table usage, lowering the risk of table exhaustion. Additionally, if upstream DNS becomes unavailable, LocalDNS can continue serving cached responses for a configurable duration, helping maintain pod connectivity and service reliability.

### Key capabilities

**Reduced DNS resolution latency:**Each AKS node runs a LocalDNS`systemd`

service. Workloads running on the node send DNS queries to this service, which resolves them locally, reducing network hops and speeding up DNS lookups.**Customizable DNS behavior:**You can use`kubeDNSOverrides`

and`vnetDNSOverrides`

to control DNS behavior in the cluster.**Avoid conntrack races and conntrack table exhaustion:**Pods send DNS queries to the LocalDNS service on the same node without creating new`conntrack`

table entries. Skipping the connection tracking helps reduce[conntrack races](https://github.com/kubernetes/kubernetes/issues/56903)and avoids User Datagram Protocol (UDP) DNS entries from filling up`conntrack`

tables. This optimization prevents dropped and rejected connections caused by`conntrack`

table exhaustion and race conditions.**Connection upgraded to TCP:**The connection from the`localdns`

cache to the cluster’s CoreDNS service uses Transmission Control Protocol (TCP). TCP allows for connection rebalancing and removes`conntrack`

table entries when the server closes the connection (in contrast to UDP connections, which have a default 30-second timeout). Applications don't need changes, because the`localdns`

service still listens for UDP traffic.**Caching:**The LocalDNS cache plugin can be configured with serveStale and Time to Live (TTL) settings.`serveStale`

,`serveStaleDurationInSeconds`

, and`cacheDurationInSeconds`

parameters can be configured to achieve DNS resiliency, even during an upstream DNS outage.**Protocol control:**You can set the DNS query protocol (such as PreferUDP or ForceTCP) for each domain. This flexibility lets you optimize DNS traffic for specific domains or meet network requirements.

### Other benefits and considerations

| Benefits | Considerations |
|---|---|
Better scalability: Reduces load on centralized CoreDNS pods |
Minimal resource overhead: Uses a small amount of CPU and memory on each node |
Seamless integration: Does not require changes to existing application connections |
Configuration changes: Updates require node image upgrades, which can cause temporary disruptions |
Block invalid search domains: Prevents invalid DNS queries at the node level |

By using LocalDNS, you get faster and more reliable DNS resolution for your workloads, reduce the risk of DNS-related outages, and gain more control over DNS traffic in your AKS environment.

## Next steps

To learn how to enable LocalDNS and configure its settings in your AKS cluster, see the [LocalDNS how-to guide](localdns-custom).

To learn more about core network concepts, see [Network concepts for applications in AKS](concepts-network).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/container-network-security-concepts -->

# Advanced Container Networking Services for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services is a suite of services designed to enhance the networking capabilities of Azure Kubernetes Service (AKS) clusters. Advanced Container Networking Services offers the following key feature sets: [ Container Network Observability](#container-network-observability),

[, and](#container-network-security)

**Container Network Security**[. These features provide deep insights into network traffic, strengthen security measures, and optimize network performance for containerized applications running in AKS.](#container-network-performance)

**Container Network Performance**## Container Network Observability

Container Network Observability provides deep insights into network traffic and performance across containerized environments. This feature set **works across both Cilium and non-Cilium data planes**, offering flexibility for diverse networking needs. The feature uses eBPF to enhance scalability and performance by identifying potential bottlenecks and network congestion before applications are affected.

Key benefits of Container Network Observability include:

- Compatibility with all Container Networking Interface (CNI) variants in Azure.
, including node-level metrics and Hubble metrics for detailed network insights.*Container network metrics*- Hubble metrics for Domain Name System (DNS) resolution, pod-to-pod communication, and service interactions.
that capture essential metadata such as IPs, ports, and traffic flow for troubleshooting, monitoring, and security enforcement.*Container network logs*- Integration with the managed service for Prometheus in Azure Monitor and Azure Managed Grafana for simplified metrics storage and visualization.

### Container network metrics

This feature collects node-level metrics, including CPU, memory, and network performance, to monitor the health of cluster nodes. For deeper insights, Hubble metrics provide data on DNS resolution times, service-to-service communication, and pod-level network behavior. These metrics help you analyze application performance, detect anomalies, and optimize workloads.

For more information, see the [metrics overview](container-network-observability-metrics).

### Container network logs

Container network logs give you detailed insight into traffic within and across clusters by capturing metadata like source and destination IP addresses, ports, protocols, and flow direction. These logs enable monitoring network behavior, troubleshooting connectivity issues, and enforcing security policies. Persistent and real-time logging options ensure comprehensive, actionable network observability.

For more information, see the [container network logs overview](container-network-observability-logs).

## Container Network Security

Container Network Security enhances the security posture of AKS clusters by providing advanced network security features. It leverages eBPF technology to enforce network policies at the kernel level, ensuring efficient and effective security controls for containerized applications. **Container Network Security is available only on clusters with Azure CNI Powered by Cilium**.

### FQDN-based filtering

FQDN-based filtering allows you to create network policies based on fully qualified domain names (FQDNs) rather than IP addresses. This capability simplifies policy management, especially in dynamic environments where IP addresses frequently change. By using FQDNs, you can ensure that your applications communicate only with trusted external services, enhancing security and compliance.

For more information, see the [FQDN-based filtering overview](container-network-security-fqdn-filtering-concepts).

### Layer 7 policy

Layer 7 policy enables application-layer traffic control, allowing you to define policies based on specific application protocols. This feature provides granular control over network traffic, enabling you to enforce security policies that align with application behavior. With Layer 7 policy, you can monitor and restrict traffic based on HTTP methods, URLs, headers, and other application-level attributes.

For more information, see the [Layer 7 policy overview](container-network-security-l7-policy-concepts).

### WireGuard Encryption (preview)

WireGuard Encryption leverages the WireGuard protocol to provide secure, encrypted communication between Cilium-managed endpoints within your AKS cluster. This feature ensures that data transmitted over the network is protected from eavesdropping and tampering, enhancing the overall security of your containerized applications.

For more information, see the [WireGuard encryption overview](container-network-security-wireguard-encryption-concepts).

## Container Network Performance

Container Network Performance optimizes network performance for containerized applications running in AKS clusters. It leverages eBPF technology to enhance network routing and reduce latency, ensuring that applications can communicate efficiently and effectively. **Container Network Performance is available only on clusters with Azure CNI Powered by Cilium**.

### eBPF Host Routing

eBPF Host Routing uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in AKS clusters.

For more information, see the [eBPF Host Routing overview](container-network-performance-ebpf-host-routing).

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/advanced-container-networking-services-overview -->

# Advanced Container Networking Services for Azure Kubernetes Service (AKS) overview

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Advanced Container Networking Services is a suite of services designed to enhance the networking capabilities of Azure Kubernetes Service (AKS) clusters. Advanced Container Networking Services offers the following key feature sets: [ Container Network Observability](#container-network-observability),

[, and](#container-network-security)

**Container Network Security**[. These features provide deep insights into network traffic, strengthen security measures, and optimize network performance for containerized applications running in AKS.](#container-network-performance)

**Container Network Performance**## Container Network Observability

Container Network Observability provides deep insights into network traffic and performance across containerized environments. This feature set **works across both Cilium and non-Cilium data planes**, offering flexibility for diverse networking needs. The feature uses eBPF to enhance scalability and performance by identifying potential bottlenecks and network congestion before applications are affected.

Key benefits of Container Network Observability include:

- Compatibility with all Container Networking Interface (CNI) variants in Azure.
, including node-level metrics and Hubble metrics for detailed network insights.*Container network metrics*- Hubble metrics for Domain Name System (DNS) resolution, pod-to-pod communication, and service interactions.
that capture essential metadata such as IPs, ports, and traffic flow for troubleshooting, monitoring, and security enforcement.*Container network logs*- Integration with the managed service for Prometheus in Azure Monitor and Azure Managed Grafana for simplified metrics storage and visualization.

### Container network metrics

This feature collects node-level metrics, including CPU, memory, and network performance, to monitor the health of cluster nodes. For deeper insights, Hubble metrics provide data on DNS resolution times, service-to-service communication, and pod-level network behavior. These metrics help you analyze application performance, detect anomalies, and optimize workloads.

For more information, see the [metrics overview](container-network-observability-metrics).

### Container network logs

Container network logs give you detailed insight into traffic within and across clusters by capturing metadata like source and destination IP addresses, ports, protocols, and flow direction. These logs enable monitoring network behavior, troubleshooting connectivity issues, and enforcing security policies. Persistent and real-time logging options ensure comprehensive, actionable network observability.

For more information, see the [container network logs overview](container-network-observability-logs).

## Container Network Security

Container Network Security enhances the security posture of AKS clusters by providing advanced network security features. It leverages eBPF technology to enforce network policies at the kernel level, ensuring efficient and effective security controls for containerized applications. **Container Network Security is available only on clusters with Azure CNI Powered by Cilium**.

### FQDN-based filtering

FQDN-based filtering allows you to create network policies based on fully qualified domain names (FQDNs) rather than IP addresses. This capability simplifies policy management, especially in dynamic environments where IP addresses frequently change. By using FQDNs, you can ensure that your applications communicate only with trusted external services, enhancing security and compliance.

For more information, see the [FQDN-based filtering overview](container-network-security-fqdn-filtering-concepts).

### Layer 7 policy

Layer 7 policy enables application-layer traffic control, allowing you to define policies based on specific application protocols. This feature provides granular control over network traffic, enabling you to enforce security policies that align with application behavior. With Layer 7 policy, you can monitor and restrict traffic based on HTTP methods, URLs, headers, and other application-level attributes.

For more information, see the [Layer 7 policy overview](container-network-security-l7-policy-concepts).

### WireGuard Encryption (preview)

WireGuard Encryption leverages the WireGuard protocol to provide secure, encrypted communication between Cilium-managed endpoints within your AKS cluster. This feature ensures that data transmitted over the network is protected from eavesdropping and tampering, enhancing the overall security of your containerized applications.

For more information, see the [WireGuard encryption overview](container-network-security-wireguard-encryption-concepts).

## Container Network Performance

Container Network Performance optimizes network performance for containerized applications running in AKS clusters. It leverages eBPF technology to enhance network routing and reduce latency, ensuring that applications can communicate efficiently and effectively. **Container Network Performance is available only on clusters with Azure CNI Powered by Cilium**.

### eBPF Host Routing

eBPF Host Routing uses extended Berkeley Packet Filter (eBPF) technology to optimize traffic flow in AKS clusters.

For more information, see the [eBPF Host Routing overview](container-network-performance-ebpf-host-routing).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/use-oidc-issuer -->

# Create an OpenID Connect provider on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article describes how to create and manage an OpenID Connect (OIDC) provider for your Azure Kubernetes Service (AKS) cluster. The OIDC issuer allows your AKS cluster to integrate with identity providers like Microsoft Entra ID, enabling secure authentication and single sign-on (SSO) capabilities for applications running within the cluster.

## About OpenID Connect (OIDC) on AKS

[OpenID Connect](/en-us/azure/active-directory/fundamentals/auth-oidc) (OIDC) extends the OAuth 2.0 authorization protocol for use as another authentication protocol issued by Microsoft Entra ID. You can use OIDC to enable single sign-on (SSO) between OAuth-enabled applications on your Azure Kubernetes Service (AKS) cluster using a security token called an ID token. You can enable the OIDC issuer on your AKS clusters, which allows Microsoft Entra ID (or another cloud provider's identity and access management platform) to discover the API server's public signing keys.

## Prerequisites

**Platform requirements**:

- Azure CLI version 2.42.0+ (
`az --version`

to check version,[install or upgrade Azure CLI](/en-us/cli/azure/install-azure-cli)if needed) - Minimum Kubernetes version is 1.22+

**Version-specific behavior**:

- OIDC issuer enabled by default (no
`--enable-oidc-issuer`

flag needed) for Kubernetes version 1.34+ - Token auto-extension disabled (
`--service-account-extend-token-expiration=false`

) for Kubernetes version 1.30.0+ - Manual enablement required if not previously configured for Kubernetes version earlier than 1.34

**Important considerations**:

- You can't disable OIDC issuer once enabled
- Enabling OIDC issuer on existing clusters requires API server restart (brief downtime)
- Maximum token lifetime is 24 hours (one day)
- Projected service account tokens required for Kubernetes 1.30+ clusters

## Create an AKS cluster with the OIDC issuer

Create an AKS cluster using the

command with the`az aks create`

`--enable-oidc-issuer`

parameter.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Create the AKS cluster with OIDC issuer enabled (OIDC issuer enabled by default for Kubernetes 1.34+) az aks create \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --node-count 1 \ --enable-oidc-issuer \ --generate-ssh-keys`


## Enable the OIDC issuer on an existing AKS cluster

Enable the OIDC issuer on an existing AKS cluster using the

command with the`az aks update`

`--enable-oidc-issuer`

parameter.`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Enable the OIDC issuer on the existing AKS cluster az aks update \ --resource-group $RESOURCE_GROUP \ --name $CLUSTER_NAME \ --enable-oidc-issuer`


## Get the OIDC issuer URL

Get the OIDC issuer URL using the

command.`az aks show`

`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Get the OIDC issuer URL az aks show \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP \ --query "oidcIssuerProfile.issuerUrl" \ -o tsv`

By default, the issuer is set to use the base URL

`https://{region}.oic.prod-aks.azure.com`

, where the value for`{region}`

matches the location the AKS cluster is deployed in.

## Rotate the OIDC key

Important

Keep the following considerations in mind when rotating the OIDC key:

- If you want to invalidate the old key immediately after key rotation, you must rotate the OIDC key twice and restart the pods using projected service account tokens.
- Both old and new keys remain valid for 24 hours after rotation.
- Manual token refresh required every 24 hours (unless using
[Azure Identity SDK](workload-identity-overview#azure-identity-client-libraries), which rotates automatically).

Rotate the OIDC key using the

command.`az aks oidc-issuer`

`# Set environment variables RESOURCE_GROUP=<your-resource-group-name> CLUSTER_NAME=<your-aks-cluster-name> # Rotate the OIDC signing keys az aks oidc-issuer rotate-signing-keys \ --name $CLUSTER_NAME \ --resource-group $RESOURCE_GROUP`


## Get the discovery document

Navigate to your

[OIDC issuer URL](#get-the-oidc-issuer-url)in your browser and append`/.well-known/openid-configuration`

to the URL. For example:`https://eastus.oic.prod-aks.azure.com/.well-known/openid-configuration`

.Your output should resemble the following example output:

`{ "issuer": "https://eastus.oic.prod-aks.azure.com/ffffffff-eeee-dddd-cccc-bbbbbbbbbbb0/00000000-0000-0000-0000-000000000000/", "jwks_uri": "https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/openid/v1/jwks", "response_types_supported": [ "id_token" ], "subject_types_supported": [ "public" ], "id_token_signing_alg_values_supported": [ "RS256" ] }`


## Get the JWK Set document

Navigate to the

in your browser. For example:**jwks_uri**from the discovery document`https://eastus.oic.prod-aks.azure.com/00000000-0000-0000-0000-000000000000/00000000-0000-0000-0000-000000000000/openid/v1/jwks`

.Your output should resemble the following example output:

`{ "keys": [ { "use": "sig", "kty": "RSA", "kid": "xxx", "alg": "RS256", "n": "xxxx", "e": "AQAB" }, { "use": "sig", "kty": "RSA", "kid": "xxx", "alg": "RS256", "n": "xxxx", "e": "AQAB" } ] }`

Note

During key rotation, there's one other key present in the discovery document.

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/network-isolated -->

# Create a network isolated Azure Kubernetes Service (AKS) cluster

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Organizations typically have strict security and compliance requirements to regulate egress (outbound) network traffic from a cluster to eliminate risks of data exfiltration. By default, standard SKU Azure Kubernetes Service (AKS) clusters have unrestricted outbound internet access. This level of network access allows nodes and services you run to access external resources as needed. If you wish to restrict egress traffic, a limited number of ports and addresses must be accessible to maintain healthy cluster maintenance tasks. The conceptual document on [outbound network and FQDN rules for AKS clusters](outbound-rules-control-egress) provides a list of required endpoints for the AKS cluster and its optional add-ons and features.

One common solution to restricting outbound traffic from the cluster is to use a [firewall device](limit-egress-traffic) to restrict traffic based on firewall rules. Firewall is applicable when your application requires outbound access, but when outbound requests have to be inspected and secured. Configuring a firewall manually with required egress rules and *FQDNs* is a cumbersome process especially if your only requirement is to create an isolated AKS cluster with no outbound dependencies for the cluster bootstrapping.

To reduce risk of data exfiltration, network isolated cluster allows for bootstrapping the AKS cluster without any outbound network dependencies, even for fetching cluster components/images from Microsoft Artifact Registry (MAR). The cluster operator could incrementally set up allowed outbound traffic for each scenario they want to enable. This article walks you through the steps of creating a network isolated cluster.

## Before you begin

- Read the
[conceptual overview of this feature](concepts-network-isolated), which provides an explanation of how network isolated clusters work. The overview article also:- Explains two options for private Azure Container Registry (ACR) resource used for cluster bootstrapping - AKS-managed ACR or bring-your-own ACR.
- Explains two private cluster modes for creating private access to API server -
[private link-based](private-clusters)or[API Server Vnet Integration](api-server-vnet-integration). - Explains the two outbound types for cluster egress control -
`none`

or`block`

(preview). - Describes the
[current limitations of network isolated clusters](concepts-network-isolated#limitations).


Note

Outbound type `none`

is generally available.
Outbound type`block`

is in preview.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

Use the Bash environment in

[Azure Cloud Shell](/en-us/azure/cloud-shell/overview). For more information, see[Get started with Azure Cloud Shell](/en-us/azure/cloud-shell/quickstart).If you prefer to run CLI reference commands locally,

[install](/en-us/cli/azure/install-azure-cli)the Azure CLI. If you're running on Windows or macOS, consider running Azure CLI in a Docker container. For more information, see[How to run the Azure CLI in a Docker container](/en-us/cli/azure/run-azure-cli-docker).If you're using a local installation, sign in to the Azure CLI by using the

[az login](/en-us/cli/azure/reference-index#az-login)command. To finish the authentication process, follow the steps displayed in your terminal. For other sign-in options, see[Authenticate to Azure using Azure CLI](/en-us/cli/azure/authenticate-azure-cli).When you're prompted, install the Azure CLI extension on first use. For more information about extensions, see

[Use and manage extensions with the Azure CLI](/en-us/cli/azure/azure-cli-extensions-overview).Run

[az version](/en-us/cli/azure/reference-index?#az-version)to find the version and dependent libraries that are installed. To upgrade to the latest version, run[az upgrade](/en-us/cli/azure/reference-index?#az-upgrade).


- This article requires version 2.71.0 or later of the Azure CLI. If you're using Azure Cloud Shell, the latest version is already installed there.
- You should install the
`aks-preview`

Azure CLI extension version*9.0.0b2*or later if you are using outbound type`block`

(preview).- If you don't already have the
`aks-preview`

extension, install it using thecommand.`az extension add`

`az extension add --name aks-preview`

- If you already have the
`aks-preview`

extension, update it to make sure you have the latest version using thecommand.`az extension update`

`az extension update --name aks-preview`


- If you don't already have the
- Network isolated clusters are supported on AKS clusters using Kubernetes version 1.30 or higher.
- If you're choosing to use the Bring your own (BYO) Azure Container Registry (ACR) option, you need to ensure the ACR is
[Premium SKU service tier](/en-us/azure/container-registry/container-registry-skus). - If you are using a network isolated cluster configured with API Server VNet Integration, you should follow the prerequisites and guidance in this
[document](api-server-vnet-integration).

## Deploy a network isolated cluster with AKS-managed ACR

AKS creates, manages, and reconciles an ACR resource in this option. You don't need to assign any permissions or manage the ACR. AKS manages the cache rules, private link, and private endpoint used in the network isolated cluster.

### Create a network isolated cluster

When creating a network isolated AKS cluster, you can choose one of the following private cluster modes - private link-based or API Server Vnet Integration.

Regardless of the mode you select, you should set `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

The `--bootstrap-artifact-source`

can be set to either `Direct`

or `Cache`

corresponding to using direct MAR (NOT network isolated) and private ACR (network isolated) for image pulls respectively.

The `--outbound-type parameter`

can be set to either `none`

or `block`

(preview). If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

#### Private link-based

Create a private link-based network isolated cluster by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with `--bootstrap-artifact-source`

, `--enable-private-cluster`

, and `--outbound-type`

parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --bootstrap-artifact-source Cache --outbound-type none --network-plugin azure --enable-private-cluster
```


#### API Server VNet integration

Create a network isolated cluster configured with API Server VNet Integration by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with `--bootstrap-artifact-source`

, `--enable-private-cluster`

, `--enable-apiserver-vnet-integration`

and `--outbound-type`

parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --bootstrap-artifact-source Cache --outbound-type none --network-plugin azure --enable-private-cluster --enable-apiserver-vnet-integration
```


### Update an existing AKS cluster to network isolated type

If you'd rather enable network isolation on an existing AKS cluster instead of creating a new cluster, use the [az aks update](/en-us/cli/azure/aks#az-aks-update) command.

To enable the network isolated feature on an existing AKS cluster, first run the following command to update `bootstrap-artifact-source`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache
```


Then you need to manually reimage all the exisiting nodepools:

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Note

You need to ensure the outbound exists until the first reimage completes. To check if the reimage completes, run:

```
NODEPOOLS=$(az aks nodepool list \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--query "[].name" -o tsv)
for NODEPOOL in $NODEPOOLS; do
echo "Waiting for node pool $NODEPOOL to finish upgrading..."
az aks nodepool wait \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--name "$NODEPOOL" \
--updated
echo "Node pool $NODEPOOL upgrade succeeded."
done
```


Wait and ensure the reimage completes, then run the following command to update `outbound-type`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --outbound-type none
```


Important

Remember to reimage the cluster's node pools instantly after you update the artifact source to Cache. Otherwise, the feature won't take effect for the cluster.

## Deploy a network isolated cluster with bring your own ACR

AKS supports bringing your own (BYO) ACR. To support the BYO ACR scenario, you have to configure an ACR private endpoint and a private DNS zone before you create the AKS cluster.

The following steps show how to prepare these resources:

- Custom virtual network and subnets for AKS and ACR.
- ACR, ACR cache rule, private endpoint, and private DNS zone.
- Custom control plane identity and kubelet identity.

### Step 1: Create the virtual network and subnets

```
az group create --name ${RESOURCE_GROUP} --location ${LOCATION}
az network vnet create --resource-group ${RESOURCE_GROUP} --name ${VNET_NAME} --address-prefixes 192.168.0.0/16
az network vnet subnet create --name ${AKS_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.1.0/24
SUBNET_ID=$(az network vnet subnet show --name ${AKS_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' --output tsv)
az network vnet subnet create --name ${ACR_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.2.0/24 --private-endpoint-network-policies Disabled
```


### Step 2: Disable virtual network outbound connectivity (Optional)

There are multiple ways to [disable the virtual network outbound connectivity](/en-us/azure/virtual-network/ip-services/default-outbound-access#how-can-i-transition-to-an-explicit-method-of-public-connectivity-and-disable-default-outbound-access).

### Step 3: Create the ACR and enable artifact cache

Create the ACR with the private link.

`az acr create --resource-group ${RESOURCE_GROUP} --name ${REGISTRY_NAME} --sku Premium --public-network-enabled false REGISTRY_ID=$(az acr show --name ${REGISTRY_NAME} -g ${RESOURCE_GROUP} --query 'id' --output tsv)`

Create an ACR cache rule following the below command to allow users to cache MAR container images and binaries in the new ACR, note the cache rule name and repo names must be strictly aligned with the guidance below.

`az acr cache create -n aks-managed-mcr -r ${REGISTRY_NAME} -g ${RESOURCE_GROUP} --source-repo "mcr.microsoft.com/*" --target-repo "aks-managed-repository/*"`


Note

With BYO ACR, it is your responsibility to ensure the ACR cache rule is created and maintained correctly as above. This step is critical to cluster creation, functioning and upgrading. This cache rule should NOT be modified.

### Step 4: Create a private endpoint for the ACR

```
az network private-endpoint create --name myPrivateEndpoint --resource-group ${RESOURCE_GROUP} --vnet-name ${VNET_NAME} --subnet ${ACR_SUBNET_NAME} --private-connection-resource-id ${REGISTRY_ID} --group-id registry --connection-name myConnection
NETWORK_INTERFACE_ID=$(az network private-endpoint show --name myPrivateEndpoint --resource-group ${RESOURCE_GROUP} --query 'networkInterfaces[0].id' --output tsv)
REGISTRY_PRIVATE_IP=$(az network nic show --ids ${NETWORK_INTERFACE_ID} --query "ipConfigurations[?privateLinkConnectionProperties.requiredMemberName=='registry'].privateIPAddress" --output tsv)
DATA_ENDPOINT_PRIVATE_IP=$(az network nic show --ids ${NETWORK_INTERFACE_ID} --query "ipConfigurations[?privateLinkConnectionProperties.requiredMemberName=='registry_data_$LOCATION'].privateIPAddress" --output tsv)
```


### Step 5: Create a private DNS zone and add records

Create a private DNS zone named `privatelink.azurecr.io`

. Add the records for the registry REST endpoint `{REGISTRY_NAME}.azurecr.io`

, and the registry data endpoint `{REGISTRY_NAME}.{REGISTRY_LOCATION}.data.azurecr.io`

.

```
az network private-dns zone create --resource-group ${RESOURCE_GROUP} --name "privatelink.azurecr.io"
az network private-dns link vnet create --resource-group ${RESOURCE_GROUP} --zone-name "privatelink.azurecr.io" --name MyDNSLink --virtual-network ${VNET_NAME} --registration-enabled false
az network private-dns record-set a create --name ${REGISTRY_NAME} --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP}
az network private-dns record-set a add-record --record-set-name ${REGISTRY_NAME} --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP} --ipv4-address ${REGISTRY_PRIVATE_IP}
az network private-dns record-set a create --name ${REGISTRY_NAME}.${LOCATION}.data --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP}
az network private-dns record-set a add-record --record-set-name ${REGISTRY_NAME}.${LOCATION}.data --zone-name "privatelink.azurecr.io" --resource-group ${RESOURCE_GROUP} --ipv4-address ${DATA_ENDPOINT_PRIVATE_IP}
```


### Step 6: Create control plane and kubelet identities

#### Control plane identity

```
az identity create --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP}
CLUSTER_IDENTITY_RESOURCE_ID=$(az identity show --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' -o tsv)
CLUSTER_IDENTITY_PRINCIPAL_ID=$(az identity show --name ${CLUSTER_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'principalId' -o tsv)
```


#### Kubelet identity

```
az identity create --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP}
KUBELET_IDENTITY_RESOURCE_ID=$(az identity show --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'id' -o tsv)
KUBELET_IDENTITY_PRINCIPAL_ID=$(az identity show --name ${KUBELET_IDENTITY_NAME} --resource-group ${RESOURCE_GROUP} --query 'principalId' -o tsv)
```


#### Grant AcrPull permissions for the Kubelet identity

```
az role assignment create --role AcrPull --scope ${REGISTRY_ID} --assignee-object-id ${KUBELET_IDENTITY_PRINCIPAL_ID} --assignee-principal-type ServicePrincipal
```


After you configure these resources, you can proceed to create the network isolated AKS cluster with BYO ACR.

### Step 7: Create network isolated cluster using BYO ACR

When creating a network isolated cluster, you can choose one of the following private cluster modes - private link-based or API Server Vnet Integration.

Regardless of the mode you select, you should set `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

The `--bootstrap-artifact-source`

can be set to either `Direct`

or `Cache`

corresponding to using direct Microsoft Artifact Registry (MAR) (NOT network isolated) and private ACR (network isolated) for image pulls respectively.

The `--outbound-type parameter`

can be set to either `none`

or `block`

(preview). If the outbound type is set to `none`

, then AKS doesn't set up any outbound connections for the cluster, allowing the user to configure them on their own. If the outbound type is set to `block`

, then all outbound connections are blocked.

#### Private link-based

Create a private link-based network isolated cluster that accesses your ACR by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with the required parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --vnet-subnet-id ${SUBNET_ID} --assign-identity ${CLUSTER_IDENTITY_RESOURCE_ID} --assign-kubelet-identity ${KUBELET_IDENTITY_RESOURCE_ID} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID} --outbound-type none --network-plugin azure --enable-private-cluster
```


#### API Server VNet integration

For a network isolated cluster configured with API server VNet integration, first create a subnet and assign the correct role with the following commands:

```
az network vnet subnet create --name ${APISERVER_SUBNET_NAME} --vnet-name ${VNET_NAME} --resource-group ${RESOURCE_GROUP} --address-prefixes 192.168.3.0/24
export APISERVER_SUBNET_ID=$(az network vnet subnet show --resource-group ${RESOURCE_GROUP} --vnet-name ${VNET_NAME} --name ${APISERVER_SUBNET_NAME} --query id -o tsv)
```


```
az role assignment create --scope ${APISERVER_SUBNET_ID} --role "Network Contributor" --assignee-object-id ${CLUSTER_IDENTITY_PRINCIPAL_ID} --assignee-principal-type ServicePrincipal
```


Create a network isolated cluster configured with API Server VNet Integration and access your ACR by running the [az aks create](/en-us/cli/azure/aks#az-aks-create) command with the required parameters.

```
az aks create --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --kubernetes-version 1.30.3 --vnet-subnet-id ${SUBNET_ID} --assign-identity ${CLUSTER_IDENTITY_RESOURCE_ID} --assign-kubelet-identity ${KUBELET_IDENTITY_RESOURCE_ID} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID} --outbound-type none --network-plugin azure --enable-apiserver-vnet-integration --apiserver-subnet-id ${APISERVER_SUBNET_ID}
```


### Update an existing AKS cluster

If you'd rather enable network isolation on an existing AKS cluster instead of creating a new cluster, use the [az aks update](/en-us/cli/azure/aks#az-aks-update) command.

When creating the private endpoint and private DNS zone for the BYO ACR, use the existing virtual network and subnets of the existing AKS cluster. When you assign the **AcrPull** permission to the kubelet identity, use the existing kubelet identity of the existing AKS cluster.

To enable the network isolated feature on an existing AKS cluster, first run the following command to update `bootstrap-artifact-source`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id ${REGISTRY_ID}
```


Then you need to manually reimage all the exisiting nodepools:

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Note

You need to ensure the outbound exists until the first reimage completes. To check if the reimage completes, run:

```
NODEPOOLS=$(az aks nodepool list \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--query "[].name" -o tsv)
for NODEPOOL in $NODEPOOLS; do
echo "Waiting for node pool $NODEPOOL to finish upgrading..."
az aks nodepool wait \
--resource-group "${RESOURCE_GROUP}" \
--cluster-name "${AKS_NAME}" \
--name "$NODEPOOL" \
--updated
echo "Node pool $NODEPOOL upgrade succeeded."
done
```


Wait and ensure the reimage completes, then run the following command to update `outbound-type`

:

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --outbound-type none
```


Important

Remember to reimage the cluster's node pools instantly after you update the artifact source to Cache. Otherwise, the feature won't take effect for the cluster.

### Update your ACR ID

It's possible to update the private ACR used with a network isolated cluster. To identify the ACR resource ID, use the `az aks show`

command.

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME}
```


Updating the ACR ID is performed by running the `az aks update`

command with the `--bootstrap-artifact-source`

and `--bootstrap-container-registry-resource-id`

parameters.

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Cache --bootstrap-container-registry-resource-id <New BYO ACR resource ID>
```


When you update the ACR ID on an existing cluster, you need to manually reimage all existing nodes.

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Important

Remember to reimage the cluster's node pools after you enable the network isolated cluster feature. Otherwise, the feature won't take effect for the cluster.

## Validate that network isolated cluster is enabled

To validate the network isolated cluster feature is enabled, use the `[az aks show](/en-us/cli/azure/aks#az-aks-show) command

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME}
```


The following output shows that the feature is enabled, based on the values of the `outboundType`

property (none or blocked) and `artifactSource`

property (Cached).

```
"kubernetesVersion": "1.30.3",
"name": "myAKSCluster"
"type": "Microsoft.ContainerService/ManagedClusters"
"properties": {
...
"networkProfile": {
...
"outboundType": "none",
...
},
...
"bootstrapProfile": {
"artifactSource": "Cache",
"containerRegistryId": "/subscriptions/my-subscription-id/my-node-resource-group-name/providers/Microsoft.ContainerRegistry/registries/my-registry-name"
},
...
}
```


## Disable network isolated cluster

Disable the network isolated cluster feature by running the `az aks update`

command with the `--bootstrap-artifact-source`

and `--outbound-type`

parameters.

```
az aks update --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --bootstrap-artifact-source Direct --outbound-type LoadBalancer
```


When you disable the feature on an existing cluster, you need to manually reimage all existing nodes.

```
az aks upgrade --resource-group ${RESOURCE_GROUP} --name ${AKS_NAME} --node-image-only
```


Important

Remember to reimage the cluster's node pools after you disable the network isolated cluster feature. Otherwise, the feature won't take effect for the cluster.

## Troubleshooting

If you're experiencing issues, such as image pull fails, see [Troubleshoot network isolated Azure Kubernetes Service (AKS) clusters issues](/en-us/troubleshoot/azure/azure-kubernetes/extensions/troubleshoot-network-isolated-cluster).

## Next steps

If you want to set up outbound restriction configuration using Azure Firewall, visit [Control egress traffic using Azure Firewall in AKS](limit-egress-traffic).

If you want to restrict how pods communicate between themselves and East-West traffic restrictions within cluster, see [Secure traffic between pods using network policies in AKS](use-network-policies).

---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/tutorial-kubernetes-scale -->

# Tutorial - Scale applications in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

If you followed the previous tutorials, you have a working Kubernetes cluster and Azure Store Front app.

In this tutorial, you scale out the pods in the app, try pod autoscaling, and scale the number of Azure VM nodes to change the cluster's capacity for hosting workloads. You learn how to:

- Scale the Kubernetes nodes.
- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.

## Before you begin

In previous tutorials, you packaged an application into a container image, uploaded the image to Azure Container Registry, created an AKS cluster, deployed an application, and used Azure Service Bus to redeploy an updated application. If you haven't completed these steps and want to follow along, start with [Tutorial 1 - Prepare application for AKS](tutorial-kubernetes-prepare-app).

This tutorial requires Azure CLI version 2.34.1 or later. Run `az --version`

to find the version. If you need to install or upgrade, see [Install Azure CLI](/en-us/cli/azure/install-azure-cli).

## Manually scale pods

View the pods in your cluster using the

command.`kubectl get`

`kubectl get pods`

The following example output shows the pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE order-service-848767080-tf34m 1/1 Running 0 31m product-service-4019737227-2q2qz 1/1 Running 0 31m store-front-2606967446-2q2qz 1/1 Running 0 31m`

Manually change the number of pods in the

*store-front*deployment using thecommand.`kubectl scale`

`kubectl scale --replicas=5 deployment.apps/store-front`

Verify the additional pods were created using the

command.`kubectl get pods`

`kubectl get pods --selector app=store-front`

The following example output shows the additional pods running the Azure Store Front app:

`NAME READY STATUS RESTARTS AGE store-front-3309479140-2hfh0 1/1 Running 0 3m store-front-3309479140-bzt05 1/1 Running 0 3m store-front-3309479140-fvcvm 1/1 Running 0 3m store-front-3309479140-hrbf2 1/1 Running 0 15m store-front-3309479140-qphz8 1/1 Running 0 3m`


## Autoscale pods

To use the horizontal pod autoscaler, all containers must have defined CPU requests and limits, and pods must have specified requests. In the `aks-store-quickstart`

deployment, the *front-end* container requests 1m CPU with a limit of 1000m CPU.

These resource requests and limits are defined for each container, as shown in the following condensed example YAML:

```
...
containers:
- name: store-front
image: ghcr.io/azure-samples/aks-store-demo/store-front:latest
ports:
- containerPort: 8080
name: store-front
...
resources:
requests:
cpu: 1m
...
limits:
cpu: 1000m
...
```


### Autoscale pods using a manifest file

Create a manifest file to define the autoscaler behavior and resource limits, as shown in the following condensed example manifest file

`aks-store-quickstart-hpa.yaml`

:`apiVersion: autoscaling/v2 kind: HorizontalPodAutoscaler metadata: name: store-front-hpa spec: maxReplicas: 10 # define max replica count minReplicas: 3 # define min replica count scaleTargetRef: apiVersion: apps/v1 kind: Deployment name: store-front metrics: - type: Resource resource: name: cpu target: type: Utilization averageUtilization: 50`

Apply the autoscaler manifest file using the

`kubectl apply`

command.`kubectl apply -f aks-store-quickstart-hpa.yaml`

Check the status of the autoscaler using the

`kubectl get hpa`

command.`kubectl get hpa`

After a few minutes, with minimal load on the Azure Store Front app, the number of pod replicas decreases to three. You can use

`kubectl get pods`

command again to see the unneeded pods being removed.

Note

You can enable the Kubernetes-based Event-Driven Autoscaler (KEDA) AKS add-on to your cluster to drive scaling based on the number of events needing to be processed. For more information, see [Enable simplified application autoscaling with the Kubernetes Event-Driven Autoscaling (KEDA) add-on (Preview)](keda-about).

## Manually scale AKS nodes

If you created your Kubernetes cluster using the commands in the previous tutorials, your cluster has two nodes. If you want to increase or decrease this amount, you can manually adjust the number of nodes.

The following example increases the number of nodes to three in the Kubernetes cluster named *myAKSCluster*. The command takes a couple of minutes to complete.

Scale your cluster nodes using the

command.`az aks scale`

`az aks scale --resource-group myResourceGroup --name myAKSCluster --node-count 3`

Once the cluster successfully scales, your output will be similar to following example output:

`"aadProfile": null, "addonProfiles": null, "agentPoolProfiles": [ { ... "count": 3, "mode": "System", "name": "nodepool1", "osDiskSizeGb": 128, "osDiskType": "Managed", "osType": "Linux", "ports": null, "vmSize": "Standard_DS2_v2", "vnetSubnetId": null ... } ... ]`


You can also autoscale the nodes in your cluster. For more information, see [Use the cluster autoscaler with node pools](cluster-autoscaler#use-the-cluster-autoscaler-on-node-pools).

## Next steps

In this tutorial, you used different scaling features in your Kubernetes cluster. You learned how to:

- Manually scale Kubernetes pods that run your application.
- Configure autoscaling pods that run the app front end.
- Manually scale the Kubernetes nodes.

In the next tutorial, you learn how to upgrade Kubernetes in your AKS cluster.

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/node-pool-snapshot -->

# Azure Kubernetes Service (AKS) node pool snapshot

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS releases a new node image weekly. Every new cluster, new node pool, or upgrade cluster always receives the latest image, which can make it hard to maintain consistency and have repeatable environments.

Node pool snapshots allow you to take a configuration snapshot of your node pool and then create new node pools or new clusters based of that snapshot for as long as that configuration and kubernetes version is supported. For more information on the supportability windows, see [Supported Kubernetes versions in AKS](supported-kubernetes-versions).

The snapshot is an Azure resource that contains the configuration information from the source node pool, such as the node image version, kubernetes version, OS type, and OS SKU. You can then reference this snapshot resource and the respective values of its configuration to create any new node pool or cluster based off of it.

## Before you begin

This article assumes that you have an existing AKS cluster. If you don't have an AKS cluster, for guidance on a designing an enterprise-scale implementation of AKS, see [Plan your AKS design](/en-us/azure/architecture/reference-architectures/containers/aks-start-here?toc=/azure/aks/toc.json&bc=/azure/aks/breadcrumb/toc.json).

### Limitations

- Any node pool or cluster created from a snapshot must use a VM from the same virtual machine family as the snapshot, for example, you can't create a new N-Series node pool based of a snapshot captured from a D-Series node pool because the node images in those cases are structurally different.
- Snapshots must be created same region as the source node pool, those snapshots can be used to create or update clusters and node pools in other regions.

## Take a node pool snapshot

In order to take a snapshot from a node pool, you need the node pool resource ID, which you can get from the following command:

```
NODEPOOL_ID=$(az aks nodepool show --name nodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --query id -o tsv)
```


Important

Your AKS node pool must be created or upgraded after Nov 10th, 2021 in order for a snapshot to be taken from it.
If you are using the `aks-preview`

Azure CLI extension version `0.5.59`

or newer, the commands for node pool snapshot have changed. For updated commands, see the [Node Pool Snapshot CLI reference](/en-us/cli/azure/aks/nodepool#az-aks-nodepool-add).

Now, to take a snapshot from the previous node pool, you use the `az aks snapshot`

CLI command.

```
az aks nodepool snapshot create --name MySnapshot --resource-group MyResourceGroup --nodepool-id $NODEPOOL_ID --location eastus
```


## Create a node pool from a snapshot

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use the following command to add a new node pool based off of this snapshot.

```
az aks nodepool add --name np2 --cluster-name myAKSCluster --resource-group myResourceGroup --snapshot-id $SNAPSHOT_ID
```


## Upgrading a node pool to a snapshot

You can upgrade a node pool to a snapshot configuration if the snapshot Kubernetes version and node image version are more recent than the current node pool versions. And the snapshot node image version is within 90 days of the node image publish date.

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use this command to upgrade this node pool to this snapshot configuration.

```
az aks nodepool upgrade --name nodepool1 --cluster-name myAKSCluster --resource-group myResourceGroup --snapshot-id $SNAPSHOT_ID
```


Note

Your node pool image version is the same contained in the snapshot and remains the same throughout every scale operation. However, if this node pool is upgraded or a node image upgrade is performed without providing a snapshot-id the node image is upgraded to the latest version.

Note

To upgrade only the node version for your node pool, use the `--node-image-only`

flag. This is required when upgrading the node image version for a node pool based on a snapshot with an identical Kubernetes version.

## Create a cluster from a snapshot

When you create a cluster from a snapshot, the snapshot configuration creates the cluster original system pool.

First, you need the resource ID from the snapshot that was previously created, which you can get from the following command:

```
SNAPSHOT_ID=$(az aks nodepool snapshot show --name MySnapshot --resource-group myResourceGroup --query id -o tsv)
```


Now, we can use this command to create this cluster off of the snapshot configuration.

```
az aks create \
--name myAKSCluster2 \
--resource-group myResourceGroup \
--snapshot-id $SNAPSHOT_ID \
--generate-ssh-keys
```


## Next steps

- See the
[AKS release notes](https://github.com/Azure/AKS/releases)for information about the latest node images. - Learn how to upgrade the Kubernetes version with
[Upgrade an AKS cluster](upgrade-cluster). - Learn how to upgrade your node image version with
[Node Image Upgrade](node-image-upgrade) - Learn more about multiple node pools with
[Create multiple node pools](create-node-pools).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/concepts-scheduler-configuration -->

# Scheduler configuration concepts for workload placement in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article covers scheduler configuration and advanced scheduling concepts for workload placement in Azure Kubernetes Service (AKS), including configurable scheduler profiles, scheduling plugins, and scheduling constraints.

## About the AKS scheduler

In AKS, the default mechanism of workload placement across nodes within a cluster is through the scheduler. The default scheduler is a control plane component responsible for assigning AKS deployment pods to nodes. Once the AKS scheduler selects a node, the deployment pod is bound to it, and the rest of the lifecycle continues.

When a pod is created without a specified node, the scheduler selects an optimal node based on several criteria, including (but not limited to):

- Available resources (CPU, memory)
[Node affinity/anti-affinity](operator-best-practices-advanced-scheduler#node-affinity)[Pod affinity/anti-affinity](operator-best-practices-advanced-scheduler#inter-pod-affinity-and-anti-affinity)[Taints and tolerations](operator-best-practices-advanced-scheduler#provide-dedicated-nodes-using-taints-and-tolerations)

### AKS scheduler configuration and scheduling strategies

By default, the AKS scheduler comes with a set of built-in rules that work well for general-purpose workloads. However, advanced use cases might require custom scheduling strategies. For example:

- Batch jobs might prefer collocating in a few nodes (for better performance) over topology-aware spreading (for reliability).
- Cost-sensitive workloads might benefit from node binpacking to consolidate jobs and minimize idle compute node costs.

To support these use cases, AKS allows you to set one or more in-tree scheduling plugins through a Kubernetes custom resource (CRD) to configure the scheduling behavior on your AKS cluster.

## Configurable scheduler profiles

A scheduler profile is a set of one or more in-tree scheduling plugins and configurations that dictate how to schedule a pod. Previously, AKS managed the scheduler configuration, and it wasn't accessible to users. Starting from Kubernetes version `1.33`

, you can now configure and set a scheduler profile (preview) for the Kubernetes scheduler on your cluster.

Each scheduler profile has the following components:

- A unique name.
- A set of
[scheduling plugins](#supported-in-tree-scheduling-plugins). - Custom arguments for fine-grained behavior (applicable to certain plugins).

## Supported in-tree scheduling plugins

AKS supports configuration of 18 in-tree Kubernetes scheduling plugins that allow pods to be placed on specific nodes, ensure pods are matched with specific storage resources, optimize for nodes with container images, and more.

The following sections walk you through these plugins, which are grouped into the following categories:

[Scheduling constraints and order-based plugins](#scheduling-constraints-and-order-based-plugins)[Node selection constraints scheduling plugins](#node-selection-constraints-scheduling-plugins)[Resource and topology optimization scheduling plugins](#resource-and-topology-optimization-scheduling-plugins)

To learn more about these plugins and configuration options, see the [Kubernetes Scheduling Plugin documentation](https://kubernetes.io/docs/reference/scheduling/config/#scheduling-plugins).

### Scheduling constraints and order-based plugins

`DefaultBinder`

: Responsible for binding the pod to a node after the scheduler selects a suitable node. Once the node is selected, the`DefaultBinder`

creates a binding object to ensure the pod is scheduled onto that node.`DefaultPreemption`

: Handles preemption, which is the process of evicting lower-priority pods to make room for higher-priority pods. If a pod can't be scheduled because there aren’t enough resources on the node, this plugin preempts other pods to make space. This plugin can receive the following arguments:`PodPriority`

: Defines the priority of the pod being scheduled.`PreemptionPolicy`

: The policy for handling pod preemption (for example:`"PreemptLowerPriority"`

or`"DoNotPreempt"`

).`PodPriorityClass`

: The priority class associated with the pod.`PodInfo`

: Information about the pods that are candidates for preemption.`Node`

: Information about the node on which preemption is considered.

`SchedulingGates`

: Introduces the concept of scheduling gates, which are conditions that must be satisfied before a pod is scheduled. For example, it can enforce the completion of certain tasks or operations before the scheduler attempts to schedule a pod.`PrioritySort`

: Sorts the list of pods according to their priority class. Pods with higher priority are scheduled first. It helps with the preemption decision-making and determines which pods to consider for priority scheduling.

### Node selection constraints scheduling plugins

`InterPodAffinity`

: Takes into account*affinity*rules specified by the user that influences scheduling based on the proximity of other pods. If a pod has affinity rules, it tries to schedule the pod on the same node or in the same topology as other pods that it has an affinity for (for example: for performance reasons or tight coupling). This plugin can receive the following arguments:`Affinity`

: Defines required or preferred affinity rules for the pod, which specifies other pods that the pod should or shouldn't be scheduled nearby.`TopologyKey`

: The key representing the failure domain to which the affinity rule applies (for example:`"kubernetes.io/hostname"`

for node-level affinity or`"topology.kubernetes.io/zone"`

for zone-level).`Weight`

: Defines how strongly the scheduler should consider a specific affinity rule.`Pod`

: The pod being scheduled.`OtherPods`

: List of other pods to consider in relation to the affinity rules.

`NodeAffinity`

: Enables scheduling based on node labels. It allows users to specify rules for which nodes a pod can be scheduled on based on the node's labels and provides fine-grained control over pod placement on nodes. This plugin can receive the following arguments:`NodeAffinity`

: Defines the required or preferred node affinity rules, such as`requiredDuringSchedulingIgnoredDuringExecution`

or`preferredDuringSchedulingIgnoredDuringExecution`

.`NodeSelectorTerms`

: Defines the set of node labels and values that must match.`Pod`

: The pod being scheduled.`Node`

: A potential node for scheduling.`LabelSelector`

: A selector for choosing nodes based on labels.

`NodeName`

: Forces pods to be scheduled on a specific node. When you specify the exact node name, the scheduler places the pod on that node if possible.`NodePorts`

: Ensures that a pod with a service of type`NodePort`

can be scheduled on a node that has the required ports available for binding. It checks whether the node has enough resources to support the node port allocations for the service.`NodeUnschedulable`

: Ensures that pods aren't scheduled on nodes marked as*unschedulable*. If a node is tainted with`node.kubernetes.io/unschedulable`

, the scheduler doesn't place any new pods on that node.`TaintToleration`

: Checks if a pod has the required tolerations to be scheduled on a node that has taints. Taints on nodes prevent pods from being scheduled unless the pod has a matching toleration.`NodeVolumeLimits`

: Checks whether a node has exceeded its volume limit. Each node has a maximum number of volumes it can attach, and this plugin ensures that the pod isn't scheduled on a node that has already reached that supported limit.`VolumeBinding`

: Ensures that persistent volumes (PVs) are properly bound to pods. It checks whether the volume that a pod requires can be bound to a node and ensures the volume is available on the selected node. This plugin can receive the following arguments:`VolumeClaims`

: The persistent volume claims (PVCs) made by the pod being scheduled.`Node`

: The candidate node being considered for scheduling.`VolumeAvailable`

: Checks if the persistent volume is available on the node or within the appropriate zone.`Pod`

: The pod that is requesting volume binding.`StorageClass`

: The storage class associated with the persistent volume.`VolumeBindingMode`

: Defines whether the volume binding mode is`Immediate`

or`WaitForFirstConsumer`

(for delayed binding until a pod is scheduled).

`VolumeRestrictions`

: Ensures that volume restrictions (such as limitations on the number of volumes a node can have attached) are respected when scheduling a pod. It prevents scheduling a pod on a node where the volume restrictions would be violated.`VolumeZone`

: Ensures that volumes are scheduled in the same availability zone as the pod. For example, if a pod requests a volume that must be in a specific zone, the plugin ensures that both the pod and the volume are in the same zone.

### Resource and topology optimization scheduling plugins

`NodeResourcesBalancedAllocation`

: Aims to balance the resource allocation on nodes. When scheduling a pod, it considers how resources like CPU and memory are allocated across nodes to avoid overprovisioning or underutilizing resources. This plugin can receive the following arguments:`ResourceRequests`

: The resource requests (CPU, memory, etc.) of the pod being scheduled.`Node`

: A candidate node for scheduling.`NodeResources`

: The available resources (CPU, memory, etc.) of the node.`ClusterResourceUsage`

: Cluster-wide resource usage metrics to help decide the best node to balance resources.

`NodeResourcesFit`

: Checks whether a node has enough available resources (CPU, memory, etc.) to run the pod. It ensures that a pod is only scheduled on a node that has sufficient resources available. This plugin can receive the following arguments:`ResourceRequests`

: The resource requests of the pod.`Node`

: The candidate node being considered for scheduling.`NodeCapacity`

: The available capacity of resources on the node.`Pod`

: The pod being scheduled, with its resource requests.

`ImageLocality`

: Helps the scheduler decide whether to schedule a pod onto a node based on the presence of a required container image. It tries to schedule pods on nodes where the required image is already present, reducing the time needed to pull the image.`PodTopologySpread`

: Ensures that pods are spread evenly across the topology (like zones or regions) to achieve high availability and fault tolerance. It tries to avoid placing multiple replicas of a pod in the same failure domain. This plugin can receive the following arguments:`TopologySpreadConstraints`

: Defines the constraints for how pods should be spread across failure domains, including the key (for example:`topology.kubernetes.io/zone`

) and the number of pods to be placed in each domain.`Pod`

: The pod being scheduled.`FailureDomain`

: The failure domain key (for example: zone or region).`PodAffinity`

: Information about pod affinity, which could also impact how the pods are distributed.`Node`

: Potential nodes for placement.`PodSpreadScore`

: Used to determine how much "spread" the pod should have across domains (higher scores indicate better spreading).


## Next step


[Configure and deploy a scheduler profile (preview) on your AKS cluster].
