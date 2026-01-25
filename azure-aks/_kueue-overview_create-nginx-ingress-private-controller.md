---
merged_at: 2026-01-25T12:25:33.945847
merged_files: 2
---

# Documentos Fusionados

Este archivo contiene 2 documentos fusionados para reducir el número total de archivos.
Cada documento está marcado con su fuente original.



---

<!-- DOCUMENTO FUSIONADO: kueue-overview.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/kueue-overview -->

# Install and Configure Kueue on Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

In this article, you learn how to install and configure Kueue to schedule batch workloads on an Azure Kubernetes Service (AKS) cluster. You also explore different Kueue concepts, installation methods to enable advanced Kueue features, and learn how to verify your deployments.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

## What are batch workloads?

Batch deployments are typically non-interactive workloads that are retriable, have a finite duration, and might experience spiky or bursty resource usage. These workloads include, but aren't limited to:

- Data processing jobs.
- Security vulnerability scans.
- Media encoding or video transcoding.
- Report generation or financial analysis.
- GPU workloads that require all resources to be available and might tolerate a delayed start but can't tolerate partial GPU allocation.

These workloads are often modeled using a Kubernetes Job, CronJob, or custom resource definition (CRD) like [RayJob](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started/rayjob-quick-start.html) or [Kubeflow MPIJob](https://www.kubeflow.org/docs/components/trainer/legacy-v1/user-guides/mpi/). Batch deployments present the following set of distinct requirements from general purpose deployments:

- Scheduling logic beyond selecting the first available node.
- Fairness, queueing, and resource awareness.
- Lifecycle awareness of jobs and pods.

The default AKS scheduler satisfies the requirements of Kubernetes services but provides limited configuration for batch workloads that require a job queueing system.

## What is Kueue?

[Kueue](https://kueue.sigs.k8s.io/docs/overview/) is an open-source Kubernetes-native job queueing project designed to manage batch workloads and ensure efficient, fair, and policy-driven scheduling in Kubernetes clusters. Kueue integrates with the [Kubernetes scheduling](https://github.com/kubernetes/community/blob/master/sig-scheduling/README.md) ecosystem to coordinate resource allocation, prioritization, and capacity control for batch jobs.

Important

Open-source software is mentioned throughout AKS documentation and samples. Software that you deploy is excluded from AKS service-level agreements, limited warranty, and Azure support. As you use open-source technology alongside AKS, consult the support options available from the respective communities and project maintainers to develop a plan.

Microsoft takes responsibility for building the open-source packages that we deploy on AKS. That responsibility includes having complete ownership of the build, scan, sign, validate, and hotfix process, along with control over the binaries in container images. For more information, see [Vulnerability management for AKS](concepts-vulnerability-management#aks-container-images) and [AKS support coverage](support-policies#aks-support-coverage).

Kueue introduces a two-level queuing model:

- A
`ClusterQueue`

represents shared resource pools (such as CPU, memory, GPU quotas). - A
`LocalQueue`

represents a tenant-facing queue in a namespace (where users submit their batch jobs).

Workloads submitted to a `LocalQueue`

are matched to a `ClusterQueue`

to determine if they can be admitted.

Note

A `LocalQueue`

is always needed for users to submit batch workloads, and the `LocalQueue`

tells Kueue about which ClusterQueue to assign the job to. The `ClusterQueue`

determines if sufficient resources are available for the job to be admitted and run.

## Who can use Kueue?

Batch workload administrators (including platform or cluster administrators and DevOps engineers) and batch users (data scientists, developers, and ML engineers) can benefit from deploying workloads with Kueue on AKS.

A batch admin focuses on configuring, managing, and securing the platform-level infrastructure to support batch workloads, and have the following responsibilities:

- Provision and manage AKS node pools.
- Define resource quotas, ClusterQueues, and policies for workload isolation.
- Tune autoscaling and cost-efficiency (such as the Cluster Autoscaler or Kueue quotas).
- Monitor cluster and queue health.
- Create and maintain templates and reusable workflows.

A batch user runs compute-intensive or parallel jobs using the platform-level infrastructure configured by a batch admin, and typically:

- Submit batch jobs (such as Job, Workload, or custom controller CRDs) and monitor job status and outputs
- Select appropriate queue or resource flavor for jobs (based on guidance from batch admins)
- Optimize job specs for resource and performance needs

| Queue Type | Scope | Created By | Used For |
|---|---|---|---|
ClusterQueue |
Cluster-wide | Platform admin | Define shared compute capacity and quota management |
LocalQueue |
Namespace | Namespace owner | Enable workload submission, mapped to ClusterQueue |

## Prerequisites

- An existing AKS cluster. If you don't have a cluster, create one using the
[Azure CLI](learn/quick-kubernetes-deploy-cli),[Azure PowerShell](learn/quick-kubernetes-deploy-powershell), or the[Azure portal](learn/quick-kubernetes-deploy-portal). - Azure CLI installed on your local machine. To install or upgrade, see
[Install the Azure CLI](/en-us/cli/azure/install-azure-cli). [Helm version 3 or above](https://helm.sh/docs/intro/install/)installed.

## Install Kueue with Helm

While most features and scheduling policies that you might require are enabled by default, some aren't like `TopologyAwareScheduling`

. If needed, reconfigure your Kueue installation by changing the default [Feature Gates](https://kueue.sigs.k8s.io/docs/installation/#feature-gates-for-alpha-and-beta-features) or by configuring [Kueue paramater values](https://github.com/kubernetes-sigs/kueue/blob/main/charts/kueue/README.md#configuration) in the `values.yaml`

file of the Helm chart.

Kueue supports multiple workload [Frameworks](https://kueue.sigs.k8s.io/docs/tasks/run/) that you need to explicitly enable to use Kueue’s scheduling and resource management capabilities when running [MPI Operator](https://www.kubeflow.org/docs/components/training/mpi/) MPIJobs, [KubeRay's](https://github.com/ray-project/kuberay) [RayJob](https://docs.ray.io/en/latest/cluster/kubernetes/getting-started/rayjob-quick-start.html) and more.

In this guide, Kueue is configured to include `LocalQueueMetrics`

and `Topology Aware Scheduling`

and frameworks from Kubeflow, Ray, and [JobSet](https://jobset.sigs.k8s.io/docs/concepts/).

`LocalQueueMetrics`

provides detailed Prometheus metrics specific to the state and activity of LocalQueues, enabling fine-grained monitoring of workload admission, quota reservation, and resource utilization.`TopologyAwareScheduling`

allows scheduling of pods based on the topology of nodes in a pool or cluster to improve available bandwidth between the pods.

Note

Update version as needed: [kueue/releases](https://github.com/kubernetes-sigs/kueue/releases)

Create and save a

`values.yaml`

file to optionally customize your Kueue configuration.`cat <<EOF > values.yaml controllerManager: featureGates: - name: TopologyAwareScheduling enabled: true - name: LocalQueueMetrics enabled: true managerConfig: controllerManagerConfigYaml: | apiVersion: config.kueue.x-k8s.io/v1beta1 kind: Configuration integrations: frameworks: - batch/job - kubeflow.org/mpijob - ray.io/rayjob - ray.io/raycluster - jobset.x-k8s.io/jobset - kubeflow.org/paddlejob - kubeflow.org/pytorchjob - kubeflow.org/tfjob - kubeflow.org/xgboostjob - kubeflow.org/jaxjob EOF`

Install the latest version of the Kueue controller and CRDs in a dedicated namespace using the

`helm install`

command.`LATEST_VERSION=$(curl -s https://api.github.com/repos/kubernetes-sigs/kueue/releases/latest | grep tag_name | cut -d '"' -f 4 | sed 's/^v//') helm install kueue oci://registry.k8s.io/kueue/charts/kueue \ --version=${LATEST_VERSION} \ --create-namespace --namespace=kueue-system \ --values values.yaml`

Confirm the deployment status using the

`helm list`

command.`helm list --namespace kueue-system`

Your output should include a

`Status`

of`deployed`

and look like:`Pulled: registry.k8s.io/kueue/charts/kueue:0.13.4 Digest: - NAME: kueue LAST DEPLOYED: - NAMESPACE: kueue-system STATUS: deployed REVISION: 1 TEST SUITE: None`


## Confirm deployment status

Verify that controller pods are running properly.

`kubectl get deploy -n kueue-system`

Your output should look similar to the following example output:

`NAME READY UP-TO-DATE AVAILABLE AGE kueue-controller-manager 1/1 1 1 7s`

Confirm the installation of Kueue resources on your AKS cluster:

`kubectl get crds | grep kueue`

Your output should include the following Kueue CRDs:

`admissionchecks.kueue.x-k8s.io 2025-09-11T18:20:48Z clusterqueues.kueue.x-k8s.io 2025-09-11T18:20:48Z cohorts.kueue.x-k8s.io 2025-09-11T18:20:48Z localqueues.kueue.x-k8s.io 2025-09-11T18:20:48Z multikueueclusters.kueue.x-k8s.io 2025-09-11T18:20:48Z multikueueconfigs.kueue.x-k8s.io 2025-09-11T18:20:48Z provisioningrequestconfigs.kueue.x-k8s.io 2025-09-11T18:20:48Z resourceflavors.kueue.x-k8s.io 2025-09-11T18:20:48Z topologies.kueue.x-k8s.io 2025-09-11T18:20:48Z workloadpriorityclasses.kueue.x-k8s.io 2025-09-11T18:20:48Z workloads.kueue.x-k8s.io 2025-09-11T18:20:48Z`


## Uninstall Kueue

If you no longer need to use the Kueue controller manager or Kueue custom resources in your AKS cluster, you can uninstall the Helm repository and remove the dedicated namespace and resources.

Uninstall the Kueue Helm repository using the

`helm uninstall`

command.`helm uninstall kueue --namespace kueue-system`

Remove the dedicated namespace and resources using the

`kubectl delete`

command.`kubectl delete namespace kueue-system`


---

<!-- DOCUMENTO FUSIONADO: create-nginx-ingress-private-controller.md -->
<!-- URL ORIGINAL: https://learn.microsoft.com/en-us/azure/aks/create-nginx-ingress-private-controller -->

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
