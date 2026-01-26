---
merged_at: 2026-01-26T23:04:05.996418
merged_files: 2
---


---
<!-- Source: N/A -->

---
<!-- Source: N/A -->

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/image-integrity -->

# Use Image Integrity to validate signed images before deploying them to your Azure Kubernetes Service (AKS) clusters (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Azure Kubernetes Service (AKS) and its underlying container model provide increased scalability and manageability for cloud native applications. With AKS, you can launch flexible software applications according to the runtime needs of your system. However, this flexibility can introduce new challenges.

In these application environments, using signed container images helps verify that your deployments are built from a trusted entity and that images haven't been tampered with since their creation. Image Integrity is a service that allows you to add an Azure Policy built-in definition to verify that only signed images are deployed to your AKS clusters.

Note

Image Integrity is a feature based on [Ratify](https://github.com/deislabs/ratify). On an AKS cluster, the feature name and property name is `ImageIntegrity`

, while the relevant Image Integrity pods' names contain `Ratify`

.

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

## Prerequisites

An Azure subscription. If you don't have an Azure subscription, you can create a

[free account](https://azure.microsoft.com/free).`aks-preview`

CLI extension version 0.5.96 or later.Ensure that the Azure Policy add-on for AKS is enabled on your cluster. If you don't have this add-on installed, see

[Install Azure Policy add-on for AKS](/en-us/azure/governance/policy/concepts/policy-for-kubernetes#install-azure-policy-add-on-for-aks).An AKS cluster enabled with OIDC Issuer. To create a new cluster or update an existing cluster, see

[Configure an AKS cluster with OIDC Issuer](use-oidc-issuer).The

`EnableImageIntegrityPreview`

feature flags registered on your Azure subscription. Register the feature flags using the following commands:Register the

`EnableImageIntegrityPreview`

feature flags using thecommand.`az feature register`

`# Register the EnableImageIntegrityPreview feature flag az feature register --namespace "Microsoft.ContainerService" --name "EnableImageIntegrityPreview" It may take a few minutes for the status to show as *Registered*.`

Verify the registration status using the

command.`az feature show`

`# Verify the EnableImageIntegrityPreview feature flag registration status az feature show --namespace "Microsoft.ContainerService" --name "EnableImageIntegrityPreview"`

Once the status shows

*Registered*, refresh the registration of the`Microsoft.ContainerService`

resource provider using thecommand.`az provider register`

`az provider register --namespace Microsoft.ContainerService`


## Considerations and limitations

- Your AKS clusters must run Kubernetes version 1.26 or above.
- You shouldn't use this feature for production Azure Container Registry (ACR) registries or workloads.
- Image Integrity supports a maximum of 200 unique signatures concurrently cluster-wide.
- Notation is the only supported verifier.
- Audit is the only supported verification policy effect.

## How Image Integrity works

Image Integrity uses Ratify, Azure Policy, and Gatekeeper to validate signed images before deploying them to your AKS clusters. Enabling Image Integrity on your cluster deploys a `Ratify`

pod. This `Ratify`

pod performs the following tasks:

- Reconciles certificates from Azure Key Vault per the configuration you set up through
`Ratify`

CRDs. - Accesses images stored in ACR when validation requests come from
[Azure Policy](/en-us/azure/governance/policy/concepts/policy-for-kubernetes). To enable this experience, Azure Policy extends Gatekeeper, an admission controller webhook for[Open Policy Agent (OPA)](https://www.openpolicyagent.org/). - Determines whether the target image is signed with a trusted cert and therefore considered as
*trusted*. `AzurePolicy`

and`Gatekeeper`

consume the validation results as the compliance state to decide whether to allow the deployment request.

## Enable Image Integrity on your AKS cluster

Note

Image signature verification is a governance-oriented scenario and leverages [Azure Policy](/en-us/azure/governance/policy/concepts/policy-for-kubernetes) to verify image signatures on AKS clusters at-scale. We recommend using AKS's Image Integrity built-in Azure Policy initiative, which is available in [Azure Policy's built-in definition library](/en-us/azure/governance/policy/samples/built-in-policies#kubernetes).

Create a policy assignment with the AKS policy initiative

using the`[Preview]: Use Image Integrity to ensure only trusted images are deployed`

command.`az policy assignment create`

`export SCOPE="/subscriptions/${SUBSCRIPTION}/resourceGroups/${RESOURCE_GROUP}" export LOCATION=$(az group show --name ${RESOURCE_GROUP} --query location -o tsv) az policy assignment create --name 'deploy-trustedimages' --policy-set-definition 'af28bf8b-c669-4dd3-9137-1e68fdc61bd6' --display-name 'Audit deployment with unsigned container images' --scope ${SCOPE} --mi-system-assigned --role Contributor --identity-scope ${SCOPE} --location ${LOCATION}`

The

`Ratify`

pod deploys after you enable the feature.

Note

The policy deploys the Image Integrity feature on your cluster when it detects any update operation on the cluster. If you want to enable the feature immediately, you need to create a policy remediation using the [ az policy remediation create](/en-us/cli/azure/policy/remediation#az-policy-remediation-create) command.

```
assignment_id=$(az policy assignment show --name 'deploy-trustedimages' --scope ${SCOPE} --query id -o tsv)
az policy remediation create --policy-assignment "$assignment_id" --definition-reference-id deployAKSImageIntegrity --name remediation --resource-group ${RESOURCE_GROUP}
```


## Set up verification configurations

For Image Integrity to properly verify the target signed image, you need to set up `Ratify`

configurations through K8s [CRDs](https://kubernetes.io/docs/concepts/extend-kubernetes/api-extension/custom-resources/#customresourcedefinitions) using `kubectl`

.

In this article, we use a self-signed CA cert from the official Ratify documentation to set up verification configurations. For more examples, see [Ratify CRDs](https://ratify.dev/docs/1.0/ratify-configuration).

Create a

`VerifyConfig`

file named`verify-config.yaml`

and copy in the following YAML:`apiVersion: config.ratify.deislabs.io/v1beta1 kind: KeyManagementProvider metadata: name: certstore-inline spec: provider: inline parameters: value: | -----BEGIN CERTIFICATE----- MIIDQzCCAiugAwIBAgIUDxHQ9JxxmnrLWTA5rAtIZCzY8mMwDQYJKoZIhvcNAQEL BQAwKTEPMA0GA1UECgwGUmF0aWZ5MRYwFAYDVQQDDA1SYXRpZnkgU2FtcGxlMB4X DTIzMDYyOTA1MjgzMloXDTMzMDYyNjA1MjgzMlowKTEPMA0GA1UECgwGUmF0aWZ5 MRYwFAYDVQQDDA1SYXRpZnkgU2FtcGxlMIIBIjANBgkqhkiG9w0BAQEFAAOCAQ8A MIIBCgKCAQEAshmsL2VM9ojhgTVUUuEsZro9jfI27VKZJ4naWSHJihmOki7IoZS8 3/3ATpkE1lGbduJ77M9UxQbEW1PnESB0bWtMQtjIbser3mFCn15yz4nBXiTIu/K4 FYv6HVdc6/cds3jgfEFNw/8RVMBUGNUiSEWa1lV1zDM2v/8GekUr6SNvMyqtY8oo ItwxfUvlhgMNlLgd96mVnnPVLmPkCmXFN9iBMhSce6sn6P9oDIB+pr1ZpE4F5bwa gRBg2tWN3Tz9H/z2a51Xbn7hCT5OLBRlkorHJl2HKKRoXz1hBgR8xOL+zRySH9Qo 3yx6WvluYDNfVbCREzKJf9fFiQeVe0EJOwIDAQABo2MwYTAdBgNVHQ4EFgQUKzci EKCDwPBn4I1YZ+sDdnxEir4wHwYDVR0jBBgwFoAUKzciEKCDwPBn4I1YZ+sDdnxE ir4wDwYDVR0TAQH/BAUwAwEB/zAOBgNVHQ8BAf8EBAMCAgQwDQYJKoZIhvcNAQEL BQADggEBAGh6duwc1MvV+PUYvIkDfgj158KtYX+bv4PmcV/aemQUoArqM1ECYFjt BlBVmTRJA0lijU5I0oZje80zW7P8M8pra0BM6x3cPnh/oZGrsuMizd4h5b5TnwuJ hRvKFFUVeHn9kORbyQwRQ5SpL8cRGyYp+T6ncEmo0jdIOM5dgfdhwHgb+i3TejcF 90sUs65zovUjv1wa11SqOdu12cCj/MYp+H8j2lpaLL2t0cbFJlBY6DNJgxr5qync cz8gbXrZmNbzC7W5QK5J7fcx6tlffOpt5cm427f9NiK2tira50HU7gC3HJkbiSTp Xw10iXXMZzSbQ0/Hj2BF4B40WfAkgRg= -----END CERTIFICATE----- --- apiVersion: config.ratify.deislabs.io/v1beta1 kind: Store metadata: name: store-oras spec: name: oras # If you want to you use Workload Identity for Ratify to access Azure Container Registry, # uncomment the following lines, and fill the proper ClientID: # See more: https://ratify.dev/docs/reference/oras-auth-provider # parameters: # authProvider: # name: azureWorkloadIdentity # clientID: XXX --- apiVersion: config.ratify.deislabs.io/v1beta1 kind: Verifier metadata: name: verifier-notary-inline spec: name: notation artifactTypes: application/vnd.cncf.notary.signature parameters: verificationCertStores: # certificates for validating signatures certs: # name of the trustStore - certstore-inline # name of the certificate store CRD to include in this trustStore trustPolicyDoc: # policy language that indicates which identities are trusted to produce artifacts version: "1.0" trustPolicies: - name: default registryScopes: - "*" signatureVerification: level: strict trustStores: - ca:certs trustedIdentities: - "*"`

Apply the

`VerifyConfig`

to your cluster using the`kubectl apply`

command.`kubectl apply -f verify-config.yaml`


## Deploy sample images to your AKS cluster

Deploy a signed image using the

`kubectl run demo`

command.`kubectl run demo-signed --image=ghcr.io/deislabs/ratify/notary-image:signed`

The following example output shows that Image Integrity allows the deployment:

`ghcr.io/deislabs/ratify/notary-image:signed pod/demo-signed created`


If you want to use your own images, see the [guidance for image signing](/en-us/azure/container-registry/container-registry-tutorial-sign-build-push).

## Disable Image Integrity

### Remove policy initiative

First you should remove the policy initiative using the

command.`az policy assignment delete`

`az policy assignment delete --name 'deploy-trustedimages'`


### Diable add-on

Then disable Image Integrity add-on on your cluster using the

command with the`az aks update`

`--disable-image-integrity`

flag.`az aks update --resource-group myResourceGroup --name MyManagedCluster --disable-image-integrity`


## Next steps

In this article, you learned how to use Image Integrity to validate signed images before deploying them to your Azure Kubernetes Service (AKS) clusters. If you want to learn how to sign your own containers, see [Build, sign, and verify container images using Notary and Azure Key Vault (Preview)](/en-us/azure/container-registry/container-registry-tutorial-sign-build-push).

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/kueue-overview -->

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
<!-- Source: N/A -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/managed-gateway-api -->

# Install Managed Gateway API CRDs (Preview)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Important

AKS preview features are available on a self-service, opt-in basis. Previews are provided "as is" and "as available," and they're excluded from the service-level agreements and limited warranty. AKS previews are partially covered by customer support on a best-effort basis. As such, these features aren't meant for production use. For more information, see the following support articles:

The [Kubernetes Gateway API](https://gateway-api.sigs.k8s.io/) is a specification for traffic management on Kubernetes clusters. It was designed as a successor and enhancement of the [Ingress API](https://kubernetes.io/docs/concepts/services-networking/ingress/), which lacked a unified and provider-agnostic approach for advanced traffic routing.

The Managed Gateway API Installation for Azure Kubernetes Service (AKS) installs the Custom Resource Definitions (CRDs) for the Kubernetes Gateway API. With the Managed Gateway API installation, you can use Gateway API functionality in a fully supported mode on AKS. However, you must also use an AKS add-on or extension that implements the Gateway API, such as [the Istio add-on](istio-gateway-api).

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

or higher.- If you already have an existing installation of the Gateway API CRDs on your cluster, then you must only have
`standard`

channel CRDs installed, and the Gateway API bundle version must be compatible with your cluster's Kubernetes version. See the table for the[bundle version associated with each Kubernetes version](#gateway-api-bundle-version-and-aks-kubernetes-version-mapping).

- If you already have an existing installation of the Gateway API CRDs on your cluster, then you must only have
Install the

`aks-preview`

extension using thecommand if you're using Azure CLI. You must use`az extension add`

`aks-preview`

version`19.0.0b4`

or higher.`az extension add --name aks-preview`

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

`az aks create`

command to install the Managed Gateway API CRDs on a newly created cluster. You must also enable an implementation of the Gateway API to enable the managed CRD installation.`# Example: enable the managed Gateway API installation with the Istio service mesh add-on az aks create -g $RESOURCE_GROUP -n $CLUSTER_NAME --enable-gateway-api --enable-azure-service-mesh`

To install the Managed Gateway API CRDs on an existing cluster with a supported implementation enabled, run the following command:

`az aks update -g $RESOURCE_GROUP -n $CLUSTER_NAME --enable-gateway-api`

To view the CRDs installed on your cluster, run the following command:

`kubectl get crds | grep "gateway.networking.k8s.io"`

`gatewayclasses.gateway.networking.k8s.io 2025-08-29T17:52:36Z gateways.gateway.networking.k8s.io 2025-08-29T17:52:36Z grpcroutes.gateway.networking.k8s.io 2025-08-29T17:52:36Z httproutes.gateway.networking.k8s.io 2025-08-29T17:52:37Z referencegrants.gateway.networking.k8s.io 2025-08-29T17:52:37Z`

Verify that the CRDs have the expected annotations and that the bundle version matches the

[expected Kubernetes version](#gateway-api-bundle-version-and-aks-kubernetes-version-mapping)for your cluster.`kubectl get crd gateways.gateway.networking.k8s.io -ojsonpath={.metadata.annotations} | jq`

`{ "api-approved.kubernetes.io": "https://github.com/kubernetes-sigs/gateway-api/pull/3328", "app.kubernetes.io/managed-by": "aks", "app.kubernetes.io/part-of": <hash>, "gateway.networking.k8s.io/bundle-version": "v1.2.1", "gateway.networking.k8s.io/channel": "standard" }`

---
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/open-service-mesh-about -->

# Open Service Mesh (OSM) add-on in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

[Open Service Mesh (OSM)](https://docs.openservicemesh.io/) is a lightweight, extensible, cloud native service mesh that allows you to uniformly manage, secure, and get out-of-the-box observability features for highly dynamic microservice environments.

OSM runs an Envoy-based control plane on Kubernetes and can be configured with [SMI](https://smi-spec.io/) APIs. OSM works by injecting an Envoy proxy as a sidecar container with each instance of your application. The Envoy proxy contains and executes rules around access control policies, implements routing configuration, and captures metrics. The control plane continually configures the Envoy proxies to ensure policies and routing rules are up to date and proxies are healthy.

Microsoft started the OSM project, but it's now governed by the [Cloud Native Computing Foundation (CNCF)](https://www.cncf.io/).

Warning

Microsoft has announced the retirement of the [Open Service Mesh (OSM) add-on for AKS](https://azure.microsoft.com/updates?id=open-service-mesh-add-on-for-aks-will-be-retired-on-september-30-2027). The upstream OSM project has also been retired by the [Cloud Native Computing Foundation (CNCF)](https://docs.openservicemesh.io/). Identify any existing OSM configurations and migrate them to equivalent Istio configurations. For migration steps, see [Migration guidance for Open Service Mesh (OSM) configurations to Istio](open-service-mesh-istio-migration-guidance).

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/egress-outboundtype -->

# Customize cluster egress with outbound types in Azure Kubernetes Service (AKS)

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

Note

After [31 March 2026](https://azure.microsoft.com/updates?id=default-outbound-access-for-vms-in-azure-will-be-retired-transition-to-a-new-method-of-internet-access), new AKS clusters that use the **AKS-managed virtual network** option will place cluster subnets into [private subnets](/en-us/azure/virtual-network/ip-services/default-outbound-access#why-is-disabling-default-outbound-access-recommended) by default (`defaultOutboundAccess = false`

).

This setting **does not impact AKS-managed cluster traffic**, which uses explicitly configured outbound paths. It may affect **unsupported scenarios**, such as deploying other resources (e.g., VMs) into the same subnet.

**Clusters using BYO VNets are unaffected** by this change. In supported configurations, no action is required.

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
<!-- Source: N/A -->

---
<!-- Source: N/A -->

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
<!-- Source: https://learn.microsoft.com/en-us/azure/aks/release-tracker -->

# AKS release tracker

Note

Access to this page requires authorization. You can try [signing in](#) or [changing directories].

Access to this page requires authorization. You can try [changing directories].

AKS releases weekly rounds of fixes and feature and component updates that affect all clusters and customers. It's important for you to know when a particular AKS release is hitting your region, and the AKS release tracker provides these details in real time by versions and regions.

Important

As of **November 30, 2025**, Azure Kubernetes Service (AKS) no longer supports or provides security updates for Azure Linux 2.0. The Azure Linux 2.0 node image is frozen at the [202512.06.0 release](https://raw.githubusercontent.com/Azure/AgentBaker/main/vhdbuilder/release-notes/AKSCBLMarinerV2/gen2/202512.06.0.txt). Beginning **March 31, 2026**, node images will be removed, and you'll be unable to scale your node pools. Migrate to a supported Azure Linux version by [upgrading your node pools](/en-us/azure/aks/upgrade-aks-cluster) to a supported Kubernetes version or migrating to [osSku AzureLinux3](/en-us/azure/aks/upgrade-os-version). For more information, see [[Retirement] Azure Linux 2.0 node pools on AKS](https://github.com/Azure/AKS/issues/4988).

## Overview

With AKS release tracker, you can follow specific component updates present in an AKS version release, such as fixes shipped to a core add-on, and node image updates for Azure Linux, Ubuntu, and Windows. The tracker provides links to the specific version of the AKS [release notes](https://github.com/Azure/AKS/releases) to help you identify relevant release instances. Real time data updates allow you to track the release order and status of each region.

## Use the release tracker

To view the release tracker, visit the [AKS release status webpage](https://releases.aks.azure.com/webpage/index.html).

### AKS releases

The top half of the tracker shows the current latest version and three previously available release versions for each region and links to the corresponding release notes entries. This view is helpful when you want to track the available versions by region.


The bottom half of the tracker shows the release order. The table has two views: *By Region* and *By Version*.


### AKS node image updates

The top half of the tracker shows the current latest node image version and three previously available node image versions for each region. This view is helpful when you want to track the available node image versions by region.


The bottom half of the tracker shows the node image update order. The table has two views: *By Region* and *By Version*.

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
