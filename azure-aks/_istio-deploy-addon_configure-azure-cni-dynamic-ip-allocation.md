---
merged_at: 2026-01-25T12:25:33.936623
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: istio-deploy-addon.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/istio-deploy-addon -->

# Deploy Istio-based service mesh add-on for Azure Kubernetes Service

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

This article shows you how to install the Istio-based service mesh add-on for Azure Kubernetes Service (AKS) cluster.

For more information on Istio and the service mesh add-on, see [Istio-based service mesh add-on for Azure Kubernetes Service](istio-about).

Tip

You can use Azure Copilot to help deploy Istio to your AKS clusters in the Azure portal. For more information, see [Work with AKS clusters efficiently using Azure Copilot](/en-us/azure/copilot/work-aks-clusters#install-and-work-with-istio).

## Before you begin

The add-on requires Azure CLI version 2.57.0 or later installed. You can run

`az --version`

to verify version. To install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli).To find information about which Istio add-on revisions are available in a region and their compatibility with AKS standard and LTS cluster versions, use the command

:`az aks mesh get-revisions`

`az aks mesh get-revisions --location <location> -o table`

For more information on the Istio add-on's compatibility with AKS, refer to the

[compatibility support policy](istio-support-policy#aks-compatibility).In some cases, Istio CRDs from previous installations may not be automatically cleaned up on uninstall. Ensure existing Istio CRDs are deleted:

`kubectl delete crd $(kubectl get crd -A | grep "istio.io" | awk '{print $1}')`

It is recommended to also clean up other resources from self-managed installations of Istio such as ClusterRoles, MutatingWebhookConfigurations and ValidatingWebhookConfigurations.

Note that if you choose to use any

`istioctl`

CLI commands, you will need to include a flag to point to the add-on installation of Istio:`--istioNamespace aks-istio-system`


### Set environment variables

```
export CLUSTER=<cluster-name>
export RESOURCE_GROUP=<resource-group-name>
export LOCATION=<location>
```


## Install Istio add-on

This section includes steps to install the Istio add-on during cluster creation or enable for an existing cluster using the Azure CLI. If you want to install the add-on using Bicep, see the guide for [installing an AKS cluster with the Istio service mesh add-on using Bicep](https://github.com/Azure-Samples/aks-istio-addon-bicep). To learn more about the Bicep resource definition for an AKS cluster, see [Bicep managedCluster reference](/en-us/azure/templates/microsoft.containerservice/managedclusters).

Note

If you need the `istiod`

and ingress/egress gateway pods scheduled onto particular nodes, you can use [AKS system nodes](/en-us/azure/aks/use-system-pools) or the `azureservicemesh/istio.replica.preferred`

node label. The pods have node affinities with a weighted preference of `100`

for AKS system nodes (labeled `kubernetes.azure.com/mode: system`

), and a weighted preference of `50`

for nodes labeled `azureservicemesh/istio.replica.preferred: true`

.

### Revision selection

If you enable the add-on without specifying a revision, a default supported revision is installed for you.

To specify a revision, perform the following steps.

- Use the
command to check which revisions are available for different AKS cluster versions in a region.`az aks mesh get-revisions`

- Based on the available revisions, you can include the
`--revision asm-X-Y`

(ex:`--revision asm-1-24`

) flag in the enable command you use for mesh installation.

### Install mesh during cluster creation

To install the Istio add-on when creating the cluster, use the `--enable-azure-service-mesh`

or`--enable-asm`

parameter.

```
az group create --name ${RESOURCE_GROUP} --location ${LOCATION}
az aks create \
--resource-group ${RESOURCE_GROUP} \
--name ${CLUSTER} \
--enable-asm \
--generate-ssh-keys
```


### Install mesh for existing cluster

The following example enables Istio add-on for an existing AKS cluster:

Important

You can't enable the Istio add-on on an existing cluster if an OSM add-on is already on your cluster. Uninstall the OSM add-on before installing the Istio add-on.
For more information, see [uninstall the OSM add-on from your AKS cluster](open-service-mesh-uninstall-add-on).
Istio add-on can only be enabled on AKS clusters of version >= 1.23.

```
az aks mesh enable --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


## Verify successful installation

To verify the Istio add-on is installed on your cluster, run the following command:

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.mode'
```


Confirm the output shows `Istio`

.

Use `az aks get-credentials`

to get the credentials for your AKS cluster:

```
az aks get-credentials --resource-group ${RESOURCE_GROUP} --name ${CLUSTER}
```


Use `kubectl`

to verify that `istiod`

(Istio control plane) pods are running successfully:

```
kubectl get pods -n aks-istio-system
```


Confirm the `istiod`

pod has a status of `Running`

. For example:

```
NAME READY STATUS RESTARTS AGE
istiod-asm-1-24-74f7f7c46c-xfdtl 1/1 Running 0 2m
istiod-asm-1-24-74f7f7c46c-4nt2v 1/1 Running 0 2m
```


## Enable sidecar injection

To automatically install sidecar to any new pods, you need to annotate your namespaces with the revision label corresponding to the control plane revision currently installed.

If you're unsure which revision is installed, use:

```
az aks show --resource-group ${RESOURCE_GROUP} --name ${CLUSTER} --query 'serviceMeshProfile.istio.revisions'
```


Apply the revision label:

```
kubectl label namespace default istio.io/rev=asm-X-Y
```


Important

Explicit versioning matching the control plane revision (ex: `istio.io/rev=asm-1-24`

) is required.

The default `istio-injection=enabled`

label will not work and will **cause the sidecar injection to skip the namespace** for the add-on.

For manual injection of sidecar using `istioctl kube-inject`

, you need to specify extra parameters for `istioNamespace`

(`-i`

) and `revision`

(`-r`

). For example:

```
kubectl apply -f <(istioctl kube-inject -f sample.yaml -i aks-istio-system -r asm-X-Y) -n foo
```


## Trigger sidecar injection

You can either deploy the sample application provided for testing, or trigger sidecar injection for existing workloads.

### Existing applications

If you have existing applications to be added to the mesh, ensure their namespaces are labeled as in the previous step, and then restart their deployments to trigger sidecar injection:

```
kubectl rollout restart -n <namespace> <deployment name>
```


Verify that sidecar injection succeeded by ensuring all containers are ready and looking for the `istio-proxy`

container in the `kubectl describe`

output, for example:

```
kubectl describe pod -n namespace <pod name>
```


The `istio-proxy`

container is the Envoy sidecar. Your application is now part of the data plane.

### Deploy sample application

Use `kubectl apply`

to deploy the sample application on the cluster:

```
kubectl apply -f https://raw.githubusercontent.com/istio/istio/release-1.24/samples/bookinfo/platform/kube/bookinfo.yaml
```


Note

Clusters using an HTTP proxy for outbound internet access will need to set up a Service Entry. For setup instructions see [HTTP proxy support in Azure Kubernetes Service](http-proxy)

Confirm several deployments and services are created on your cluster. For example:

```
service/details created
serviceaccount/bookinfo-details created
deployment.apps/details-v1 created
service/ratings created
serviceaccount/bookinfo-ratings created
deployment.apps/ratings-v1 created
service/reviews created
serviceaccount/bookinfo-reviews created
deployment.apps/reviews-v1 created
deployment.apps/reviews-v2 created
deployment.apps/reviews-v3 created
service/productpage created
serviceaccount/bookinfo-productpage created
deployment.apps/productpage-v1 created
```


Use `kubectl get services`

to verify that the services were created successfully:

```
kubectl get services
```


Confirm the following services were deployed:

```
NAME TYPE CLUSTER-IP EXTERNAL-IP PORT(S) AGE
details ClusterIP 10.0.180.193 <none> 9080/TCP 87s
kubernetes ClusterIP 10.0.0.1 <none> 443/TCP 15m
productpage ClusterIP 10.0.112.238 <none> 9080/TCP 86s
ratings ClusterIP 10.0.15.201 <none> 9080/TCP 86s
reviews ClusterIP 10.0.73.95 <none> 9080/TCP 86s
```


```
kubectl get pods
```


```
NAME READY STATUS RESTARTS AGE
details-v1-558b8b4b76-2llld 2/2 Running 0 2m41s
productpage-v1-6987489c74-lpkgl 2/2 Running 0 2m40s
ratings-v1-7dc98c7588-vzftc 2/2 Running 0 2m41s
reviews-v1-7f99cc4496-gdxfn 2/2 Running 0 2m41s
reviews-v2-7d79d5bd5d-8zzqd 2/2 Running 0 2m41s
reviews-v3-7dbcdcbc56-m8dph 2/2 Running 0 2m41s
```


Confirm that all the pods have status of `Running`

with two containers in the `READY`

column. The second container (`istio-proxy`

) added to each pod is the Envoy sidecar injected by Istio, and the other is the application container.

To test this sample application against ingress, check out [next-steps](#next-steps).

## Next steps

[Deploy external or internal ingresses for Istio service mesh add-on](istio-deploy-ingress)[Scale istiod and ingress gateway HPA](istio-scale#scaling)[Collect metrics for Istio service mesh add-on workloads in Azure Managed Prometheus](istio-metrics-managed-prometheus)[Deploy egress gateways for the Istio service mesh add-on](istio-deploy-egress)[Enable Istio CNI for Istio service mesh add-on (Preview)](istio-cni)


---

<!-- DOCUMENTO FUSIONADO: configure-azure-cni-dynamic-ip-allocation.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/configure-azure-cni-dynamic-ip-allocation -->

# Configure Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

A drawback with the traditional CNI is the exhaustion of pod IP addresses as the AKS cluster grows, which results in the need to rebuild your entire cluster in a bigger subnet. The new dynamic IP allocation capability in Azure CNI solves this problem by allocating pod IPs from a subnet separate from the subnet hosting the AKS cluster.

It offers the following benefits:

**Better IP utilization**: IPs are dynamically allocated to cluster Pods from the Pod subnet. This leads to better utilization of IPs in the cluster compared to the traditional CNI solution, which does static allocation of IPs for every node.**Scalable and flexible**: Node and pod subnets can be scaled independently. A single pod subnet can be shared across multiple node pools of a cluster or across multiple AKS clusters deployed in the same VNet. You can also configure a separate pod subnet for a node pool.**High performance**: Since pods are assigned virtual network IPs, they have direct connectivity to other cluster pod and resources in the VNet. The solution supports very large clusters without any degradation in performance.**Separate VNet policies for pods**: Since pods have a separate subnet, you can configure separate VNet policies for them that are different from node policies. This enables many useful scenarios such as allowing internet connectivity only for pods and not for nodes, fixing the source IP for pod in a node pool using an Azure NAT Gateway, and using NSGs to filter traffic between node pools.**Kubernetes network policies**: Both the Azure Network Policies and Calico work with this new solution.

This article shows you how to use Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support in AKS.

## Prerequisites

Review the

[prerequisites](configure-azure-cni#prerequisites)for configuring basic Azure CNI networking in AKS, as the same prerequisites apply to this article.Review the

[deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS, as the same parameters apply.AKS Engine and DIY clusters aren't supported.

Azure CLI version

`2.37.0`

or later.If you have an existing cluster, you need to enable Container Insights for monitoring IP subnet usage. You can enable Container Insights using the

command, as shown in the following example:`az aks enable-addons`

`az aks enable-addons --addons monitoring --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME`


## Plan IP addressing

Planning your IP addressing is much simpler with this feature. Since the nodes and pods scale independently, their address spaces can also be planned separately. Since pod subnets can be configured to the granularity of a node pool, you can always add a new subnet when you add a node pool. The system pods in a cluster/node pool also receive IPs from the pod subnet, so this behavior needs to be accounted for.

IPs are allocated to nodes in batches of 16. Pod subnet IP allocation should be planned with a minimum of 16 IPs per node in the cluster; nodes will request 16 IPs on startup and will request another batch of 16 any time there are <8 IPs unallocated in their allotment.

The planning of IPs for Kubernetes services and Docker bridge remain unchanged.

To view and verify the NodeNetworkConfiguration (NNC) resources responsible for these IP allocations, you can run the following command:

```
kubectl get nodenetworkconfigs -n kube-system -o wide
```


## Maximum pods per node in a cluster with Pod Subnet - Dynamic IP Allocation and enhanced subnet support

The pods per node value when using Azure CNI Pod Subnet - Dynamic IP Allocation is slightly different from the traditional CNI behavior:

| CNI | Default | Configurable at deployment |
|---|---|---|
| Traditional Azure CNI | 30 | Yes (up to 250) |
| Azure CNI Pod Subnet - Dynamic IP Allocation | 250 | Yes (up to 250) |

All other guidance related to configuring the maximum pods per node remains the same.

## Deployment parameters

The [deployment parameters](azure-cni-overview#deployment-parameters)for configuring basic Azure CNI networking in AKS are all valid, with two exceptions:

- The
**subnet**parameter now refers to the subnet related to the cluster's nodes. - An additional parameter
**pod subnet**is used to specify the subnet whose IP addresses will be dynamically allocated to pods.

## Configure Pod Subnet - Dynamic IP Allocation and enhanced subnet support - Azure CLI

Using Pod Subnet - Dynamic IP Allocation and enhanced subnet support in your cluster is similar to the default method for configuring a cluster Azure CNI. The following example walks through creating a new virtual network with a subnet for nodes and a subnet for pods, and creating a cluster that uses Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support. Be sure to replace variables such as `$subscription`

with your own values.

Create the virtual network with two subnets.

```
RESOURCE_GROUP_NAME="myResourceGroup"
VNET_NAME="myVirtualNetwork"
LOCATION="westcentralus"
SUBNET_NAME_1="nodesubnet"
SUBNET_NAME_2="podsubnet"
# Create the resource group
az group create --name $RESOURCE_GROUP_NAME --location $LOCATION
# Create our two subnet network
az network vnet create --resource-group $RESOURCE_GROUP_NAME --location $LOCATION --name $VNET_NAME --address-prefixes 10.0.0.0/8 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_1 --address-prefixes 10.240.0.0/16 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_2 --address-prefixes 10.241.0.0/16 -o none
```


Create the cluster, referencing the node subnet using `--vnet-subnet-id`

and the pod subnet using `--pod-subnet-id`

and enabling the monitoring add-on.

```
CLUSTER_NAME="myAKSCluster"
SUBSCRIPTION="aaaaaaa-aaaaa-aaaaaa-aaaa"
az aks create \
--name $CLUSTER_NAME \
--resource-group $RESOURCE_GROUP_NAME \
--location $LOCATION \
--max-pods 250 \
--node-count 2 \
--network-plugin azure \
--vnet-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_1 \
--pod-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_2 \
--enable-addons monitoring \
--generate-ssh-keys
```


### Adding node pool

When adding node pool, reference the node subnet using `--vnet-subnet-id`

and the pod subnet using `--pod-subnet-id`

. The following example creates two new subnets that are then referenced in the creation of a new node pool:

```
SUBNET_NAME_3="node2subnet"
SUBNET_NAME_4="pod2subnet"
NODE_POOL_NAME="mynodepool"
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_3 --address-prefixes 10.242.0.0/16 -o none
az network vnet subnet create --resource-group $RESOURCE_GROUP_NAME --vnet-name $VNET_NAME --name $SUBNET_NAME_4 --address-prefixes 10.243.0.0/16 -o none
az aks nodepool add --cluster-name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME --name $NODE_POOL_NAME \
--max-pods 250 \
--node-count 2 \
--vnet-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_3 \
--pod-subnet-id /subscriptions/$SUBSCRIPTION/resourceGroups/$RESOURCE_GROUP_NAME/providers/Microsoft.Network/virtualNetworks/$VNET_NAME/subnets/$SUBNET_NAME_4 \
--no-wait
```


## Monitor IP subnet usage

Azure CNI provides the capability to monitor IP subnet usage. To enable IP subnet usage monitoring, follow the steps below:

### Get the YAML file

Download or grep the file named container-azm-ms-agentconfig.yaml from

[GitHub](https://raw.githubusercontent.com/microsoft/Docker-Provider/ci_prod/kubernetes/container-azm-ms-agentconfig.yaml).Find

in integrations. Set`azure_subnet_ip_usage`

`enabled`

to`true`

.Save the file.


### Get the AKS credentials

Set the variables for subscription, resource group and cluster. Consider the following as examples:

```
az account set --subscription $SUBSCRIPTION
az aks get-credentials --name $CLUSTER_NAME --resource-group $RESOURCE_GROUP_NAME
```


### Apply the config

- Open the terminal in the folder in which the downloaded
**container-azm-ms-agentconfig.yaml**file is saved. - Apply the config using the
`kubectl apply -f container-azm-ms-agentconfig.yaml`

command. This will restart the pod and after 5-10 minutes, the metrics will be visible. - View the metrics on the cluster by navigating to Workbooks on the cluster page in the Azure portal, and find the workbook named
*Subnet IP Usage*.

## Azure CNI Pod Subnet - Dynamic IP Allocation and enhanced subnet support FAQs

**Can I assign multiple pod subnets to a cluster/node pool?**Only one subnet can be assigned to a cluster or node pool. However, multiple clusters or node pools can share a single subnet.

**Can I assign Pod subnets from a different VNet altogether?**No, the pod subnet should be from the same VNet as the cluster.

**Can some node pools in a cluster use the traditional CNI while others use the new CNI?**The entire cluster should use only one type of CNI.


## Next steps

Learn more about networking in AKS in the following articles:
