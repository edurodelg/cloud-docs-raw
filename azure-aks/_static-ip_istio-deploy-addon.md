---
merged_at: 2026-01-25T12:06:27.802290
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: static-ip.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/static-ip -->

# Use a static public IP address and DNS label with the Azure Kubernetes Service (AKS) load balancer

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

When you create a load balancer resource in an Azure Kubernetes Service (AKS) cluster, the public IP address assigned to it is only valid for the lifespan of that resource. If you delete the Kubernetes service, the associated load balancer and IP address are also deleted. If you want to assign a specific IP address or retain an IP address for redeployed Kubernetes services, you can create and use a static public IP address.

This article shows you how to create a static public IP address and assign it to your Kubernetes service.

## Before you begin

- You need the Azure CLI version 2.0.59 or later installed and configured. Run
`az --version`

to find the version. If you need to install or upgrade, see[Install Azure CLI](/en-us/cli/azure/install-azure-cli). - This article covers using a
*Standard*SKU IP with a*Standard*SKU load balancer. For more information, see[IP address types and allocation methods in Azure](/en-us/azure/virtual-network/ip-services/public-ip-addresses#sku).

## Create an AKS cluster

Create an Azure resource group using the

command.`az group create`

`az group create --name myNetworkResourceGroup --location eastus`

Create an AKS cluster using the

command.`az aks create`

`az aks create --name myAKSCluster --resource-group myNetworkResourceGroup --generate-ssh-keys`


## Create a static IP address

Get the name of the node resource group using the

command and query for the`az aks show`

`nodeResourceGroup`

property.`az aks show --name myAKSCluster --resource-group myNetworkResourceGroup --query nodeResourceGroup -o tsv`

Create a static public IP address in the node resource group using the

command.`az network public ip create`

`az network public-ip create \ --resource-group <node resource group name> \ --name myAKSPublicIP \ --sku Standard \ --allocation-method static`

Note

If you're using a

*Basic*SKU load balancer in your AKS cluster, use*Basic*for the`--sku`

parameter when defining a public IP. Only*Basic*SKU IPs work with the*Basic*SKU load balancer and only*Standard*SKU IPs work with*Standard*SKU load balancers.Get the static public IP address using the

command. Specify the name of the node resource group and public IP address you created, and query for the`az network public-ip list`

`ipAddress`

.`az network public-ip show --resource-group <node resource group name> --name myAKSPublicIP --query ipAddress --output tsv`


## Create a service using the static IP address

First, determine which type of managed identity your AKS cluster is using, system-assigned or user-assigned. If you're not certain, call the

[az aks show](/en-us/cli/azure/aks#az-aks-show)command and query for the identity's*type*property.`az aks show \ --name myAKSCluster \ --resource-group myResourceGroup \ --query identity.type \ --output tsv`

If the cluster is using a managed identity, the value of the

*type*property will be either**SystemAssigned**or**UserAssigned**.If the cluster is using a service principal, the value of the

*type*property will be null. Consider upgrading your cluster to use a managed identity.If your AKS cluster uses a system-assigned managed identity, then query for the managed identity's principal ID as follows:

`# Get the principal ID for a system-assigned managed identity. CLIENT_ID=$(az aks show \ --name myAKSCluster \ --resource-group myNetworkResourceGroup \ --query identity.principalId \ --output tsv)`

If your AKS cluster uses a user-assigned managed identity, then the principal ID will be null. Query for the user-assigned managed identity's client ID instead:

`# Get the client ID for a user-assigned managed identity. CLIENT_ID=$(az aks show \ --name myAKSCluster \ --resource-group myNetworkResourceGroup \ --query identity.userAssignedIdentities.*.clientId \ --output tsv`

Assign delegated permissions for the managed identity used by the AKS cluster for the public IP's resource group by calling the

command.`az role assignment create`

`# Get the resource ID for the node resource group. RG_SCOPE=$(az group show \ --name <node resource group> \ --query id \ --output tsv) # Assign the Network Contributor role to the managed identity, # scoped to the node resource group. az role assignment create \ --assignee ${CLIENT_ID} \ --role "Network Contributor" \ --scope ${RG_SCOPE}`

Important

If you customized your outbound IP, make sure your cluster identity has permissions to both the outbound public IP and the inbound public IP.

Create a file named

`load-balancer-service.yaml`

and copy in the contents of the following YAML file, providing your own public IP address created in the previous step and the node resource group name.Important

Adding the

`loadBalancerIP`

property to the load balancer YAML manifest is deprecating following[upstream Kubernetes](https://github.com/kubernetes/kubernetes/pull/107235). While current usage remains the same and existing services are expected to work without modification, we**highly recommend setting service annotations**instead. To set service annotations, you can either use`service.beta.kubernetes.io/azure-pip-name`

for public IP name, or use`service.beta.kubernetes.io/azure-load-balancer-ipv4`

for an IPv4 address and`service.beta.kubernetes.io/azure-load-balancer-ipv6`

for an IPv6 address, as shown in the example YAML.`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: <node resource group name> service.beta.kubernetes.io/azure-pip-name: myAKSPublicIP name: azure-load-balancer spec: type: LoadBalancer ports: - port: 80 selector: app: azure-load-balancer`

Note

Adding the

`service.beta.kubernetes.io/azure-pip-name`

annotation ensures the most efficient LoadBalancer creation and is highly recommended to avoid potential throttling.Set a public-facing DNS label to the service using the

`service.beta.kubernetes.io/azure-dns-label-name`

service annotation. This publishes a fully qualified domain name (FQDN) for your service using Azure's public DNS servers and top-level domain. The annotation value must be unique within the Azure location, so we recommend you use a sufficiently qualified label. Azure automatically appends a default suffix in the location you selected, such as`<location>.cloudapp.azure.com`

, to the name you provide, creating the FQDN.Note

If you want to publish the service on your own domain, see

[Azure DNS](https://azure.microsoft.com/services/dns/)and the[external-dns](https://github.com/kubernetes-sigs/external-dns)project.`apiVersion: v1 kind: Service metadata: annotations: service.beta.kubernetes.io/azure-load-balancer-resource-group: <node resource group name> service.beta.kubernetes.io/azure-pip-name: myAKSPublicIP service.beta.kubernetes.io/azure-dns-label-name: <unique-service-label> name: azure-load-balancer spec: type: LoadBalancer ports: - port: 80 selector: app: azure-load-balancer`

Create the service and deployment using the

`kubectl apply`

command.`kubectl apply -f load-balancer-service.yaml`

To see the DNS label for your load balancer, use the

`kubectl describe service`

command.`kubectl describe service azure-load-balancer`

The DNS label will be listed under the

`Annotations`

, as shown in the following condensed example output:`Name: azure-load-balancer Namespace: default Labels: <none> Annotations: service.beta.kuberenetes.io/azure-dns-label-name: <unique-service-label>`


## Troubleshoot

If the static IP address defined in the `loadBalancerIP`

property of the Kubernetes service manifest doesn't exist or hasn't been created in the node resource group and there are no other delegations configured, the load balancer service creation fails. To troubleshoot, review the service creation events using the [ kubectl describe](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands#describe) command. Provide the name of the service specified in the YAML manifest, as shown in the following example:

```
kubectl describe service azure-load-balancer
```


The output shows you information about the Kubernetes service resource. The following example output shows a `Warning`

in the `Events`

: "`user supplied IP address was not found`

." In this scenario, make sure you created the static public IP address in the node resource group and that the IP address specified in the Kubernetes service manifest is correct.

```
Name: azure-load-balancer
Namespace: default
Labels: <none>
Annotations: <none>
Selector: app=azure-load-balancer
Type: LoadBalancer
IP: 10.0.18.125
IP: 40.121.183.52
Port: <unset> 80/TCP
TargetPort: 80/TCP
NodePort: <unset> 32582/TCP
Endpoints: <none>
Session Affinity: None
External Traffic Policy: Cluster
Events:
Type Reason Age From Message
---- ------ ---- ---- -------
Normal CreatingLoadBalancer 7s (x2 over 22s) service-controller Creating load balancer
Warning CreatingLoadBalancerFailed 6s (x2 over 12s) service-controller Error creating load balancer (will retry): Failed to create load balancer for service default/azure-load-balancer: user supplied IP Address 40.121.183.52 was not found
```


## Next steps

For more control over the network traffic to your applications, use the application routing addon for AKS. For more information about the app routing addon, see [Managed NGINX ingress with the application routing add-on](app-routing).


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
